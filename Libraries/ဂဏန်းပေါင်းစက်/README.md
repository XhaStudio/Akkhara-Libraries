# ဂညန်းကိရိယာ (Math Tools)

Basic math helpers for Akkhara programs: `စတုရန်း` (square) and `နှစ်ဆ`
(double).

## Install

```
akk install ဂညန်းကိရိယာ
```

## Usage

```
နည်းပညာများ ဂညန်းကိရိယာ ကို အသုံးပြုပါ။

စတုရန်း ကို လုပ်ရန် 5 ဖြင့်။
ရလဒ် ကို ဖော်ပြပါ။          # prints 25

နှစ်ဆ ကို လုပ်ရန် 5 ဖြင့်။
ရလဒ် ကို ဖော်ပြပါ။          # prints 10
```

## How it works

Akkhara functions take a single argument and have no `return` statement
— they can only produce output as a side effect. This library follows
the repo-wide convention: it writes its result into a global variable
named `ရလဒ်` (*"result"*), which the caller reads right after the call.

## Files

```
main/
  main.akk      <- the library's source, in plain Akkhara
index.json      <- this library's manifest (name, version, description, entry)
README.md       <- this file
```
