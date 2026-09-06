# Akkhara-Libraries

Community package repository for the [Akkhara programming language](https://github.com/XhaStudio/Akkhara-Programming-Language).

Anyone running `akk install <name>` downloads a library straight from
this repo's `main` branch (via `raw.githubusercontent.com` and the
GitHub contents API — no releases or tags needed here, unlike the
interpreter itself).

## How installation works

Running:

```
akk install ဂညန်းကိရိယာ
```

downloads everything under `Libraries/ဂညန်းကိရိယာ/` in this repo and
drops it into the `libraries/` folder next to your `akk` binary:

```
Libraries/ဂညန်းကိရိယာ/main/*         -> libraries/ဂညန်းကိရိယာ/main/*
Libraries/ဂညန်းကိရိယာ/index.json     -> libraries/ဂညန်းကိရိယာ/index.json
```

From then on, any `.akk` program can load it at runtime with:

```
နည်းပညာများ ဂညန်းကိရိယာ ကို အသုံးပြုပါ။
```

If `akk install` can't find an exact match, it fetches this folder's
`index.json` (the catalog below) and prints any library names that look
related, so people can browse what's published here instead of
guessing.

## Repo layout

```
LICENSE
Libraries/
  README.md                 <- this file
  index.json                <- flat catalog of every published library name
  <library-name>/
    main/
      main.akk               <- entry file (more files can live here too)
    index.json                <- this library's manifest: name, version,
                                  description, author, entry
    README.md                 <- this library's own docs
```

## Publishing a new library

1. Create `Libraries/<name>/main/main.akk`. Write it exactly like a
   normal Akkhara program — top-level `လုပ်ငန်း ... ပြီး။` function (and
   `နည်းလမ်း ... ပြီး။` class) definitions are what get registered when
   someone imports it. Anything else at the top level (variable
   declarations, print statements) runs immediately at import time too,
   so keep those out unless that's genuinely what you want. If your
   library needs more than one file, add them alongside `main.akk`
   inside the same `main/` folder — `akk install` downloads every file
   in there.

2. **Akkhara functions take a single argument and have no `return`
   statement** — they can only produce output as a side effect (printing,
   or writing to the global environment). The convention every library
   in this repo follows: write your result into a global variable named
   `ရလဒ်` (*"result"*), which the caller reads right after the call. See
   `Libraries/ဂညန်းကိရိယာ/main/main.akk` for a working example of this
   pattern.

3. Add `Libraries/<name>/index.json`, this library's manifest:

   ```json
   {
     "name": "<name>",
     "version": "1.0.0",
     "description": "One line describing what it does.",
     "author": "your name or handle",
     "entry": "main/main.akk"
   }
   ```

4. Add `Libraries/<name>/README.md` documenting how to install and use
   your library.

5. Add `"<name>"` to the `packages` array in `Libraries/index.json` at
   the repo root, so `akk install` can suggest it on a near-miss.

6. Open a PR. Once merged to `main`, the library is live immediately —
   there's no release/publish step, `akk install` always reads straight
   off the `main` branch.

## Versioning

Each library's `index.json`'s `version` field is informational only
right now — `akk install <name>` always fetches whatever is currently
on `main`. There's no way yet to pin or request an older version of a
library.

## Example library

`Libraries/ဂညန်းကိရိယာ` (Math Tools) ships two functions, `စတုရန်း`
(square) and `နှစ်ဆ` (double), demonstrating the `ရလဒ်` result-variable
convention described above. See its own
`Libraries/ဂညန်းကိရိယာ/README.md` for usage.
