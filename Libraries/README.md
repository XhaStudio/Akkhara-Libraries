# Akkhara-Libraries

Community package repository for the [Akkhara programming language](https://github.com/XhaStudio/Akkhara-Programming-Language).

Anyone running `akk install <name>` downloads packages straight from this
repo's `main` branch (via `raw.githubusercontent.com` — no releases or
tags needed here, unlike the interpreter itself).

## How installation works

Running:

```
akk install ဂညန်းကိရိယာ
```

downloads two files from this repo and drops them into the `libraries/`
folder next to your `akk` binary:

```
packages/ဂညန်းကိရိယာ/main.akk        -> libraries/ဂညန်းကိရိယာ/main.akk
packages/ဂညန်းကိရိယာ/metadata.json  -> libraries/ဂညန်းကိရိယာ/metadata.json
```

From then on, any `.akk` program can load it at runtime with:

```
နည်းပညာများ ဂညန်းကိရိယာ ကို အသုံးပြုပါ။
```

If `akk install` can't find an exact match, it fetches `index.json` and
prints any package names that look related, so people can browse what's
published here instead of guessing.

## Repo layout

```
index.json                    <- flat list of every published package name
packages/
  <package-name>/
    main.akk                  <- the library's source, in plain Akkhara
    metadata.json             <- name, version, description, author, entry
```

## Publishing a new package

1. Create `packages/<name>/main.akk`. Write it exactly like a normal
   Akkhara program — top-level `လုပ်ငန်း ... ပြီး။` function (and
   `နည်းလမ်း ... ပြီး။` class) definitions are what get registered when
   someone imports it. Anything else at the top level (variable
   declarations, print statements) runs immediately at import time too, so
   keep those out unless that's genuinely what you want.

2. **Akkhara functions take a single argument and have no `return`
   statement** — they can only produce output as a side effect (printing,
   or writing to the global environment). The convention every package in
   this repo follows: write your result into a global variable named
   `ရလဒ်` (*"result"*), which the caller reads right after the call. See
   `packages/ဂညန်းကိရိယာ/main.akk` for a working example of this pattern.

3. Add `packages/<name>/metadata.json`:

   ```json
   {
     "name": "<name>",
     "version": "1.0.0",
     "description": "One line describing what it does.",
     "author": "your name or handle",
     "entry": "main.akk"
   }
   ```

4. Add `"<name>"` to the `packages` array in `index.json` at the repo
   root, so `akk install` can suggest it on a near-miss.

5. Open a PR. Once merged to `main`, the package is live immediately —
   there's no release/publish step, `akk install` always reads straight
   off the `main` branch.

## Versioning

`metadata.json`'s `version` field is informational only right now —
`akk install <name>` always fetches whatever is currently on `main`.
There's no way yet to pin or request an older version of a package.

## Example package

`packages/ဂညန်းကိရိယာ` (Math Tools) ships two functions, `စတုရန်း`
(square) and `နှစ်ဆ` (double), demonstrating the `ရလဒ်` result-variable
convention described above.
