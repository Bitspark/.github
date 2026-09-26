# Naming Bitspark projects

## The rule

**A Bitspark project is written exactly as its GitHub repository is named,
character for character, everywhere.**

"Everywhere" covers prose, headings, titles, the first word of a sentence,
issue and pull-request titles, commit messages, code comments, log and error
text, user-interface text, and package and module names.

| Write | Not |
| --- | --- |
| bitwire | `Bitwire`, `BitWire` |
| nightseam | `Nightseam` |
| bittree | `BitTree`, `Bittree` |
| bitsystem3 | `Bit System 3`, `BitSystem3` |
| logos-db | `Logos DB`, `LogosDB`, `Logos-db` |
| bitwire-svc | `Bitwire Service` |
| BitMachine | `bitmachine`: a repository named with capitals keeps them |

The organization is written as GitHub writes it: **Bitspark**.

## Why

- **One rule, no table.** Bitspark has more than 250 repositories, and about
  two thirds of the names contain hyphens. A rule that capitalises names in
  prose either produces forms nobody writes (`Logos-db`, `Bb-hub`,
  `Bitagent-ci`) or needs a table of chosen spellings, which is a decision
  left to every writer. The repository name is already unique and fixed, so
  it decides.
- **One name at every address.** Module paths, package names, commands,
  domains and service hosts are already written this way
  (`github.com/Bitspark/bitwire`, `@bitspark/bitwire`, `bitwire.dev`). Prose
  now matches them, so a name read in a sentence can be typed as an address
  unchanged.

## Details

- **Sentence starts stay as the name.** Write "bitwire holds the contract.",
  not "Bitwire holds the contract.".
- **Possessives and plurals attach to the unchanged name:** "bitwire's
  contract", "two nightseam peers".
- **Identifiers follow their language, not this rule.** A Go type `Logos`, a
  Haskell module `Bitwire` or a class `NightseamPeer` is an identifier that
  contains a name, and its language decides how it is written. Only the
  standalone name is governed.
- **Quotations stay verbatim.** This covers quoted text from people and other
  projects, and records whose purpose is to preserve what was sent or received
  (for example a consultation's submitted document and its reply). Everything
  else, including decision records and changelogs, is respelled; spelling
  changes no decision.
- **Other people's projects keep their own spelling**, even when Bitspark keeps
  a fork: GitHub, TypeScript, WebSocket, GORM.
- **Renames.** After a repository is renamed, write the new name.
- **A project that has no repository yet** is written as the repository name it
  will have. Choose that name before writing about the project.
- **Things that are not repositories** (protocols, packages, formats) are
  written as their own specification defines them: `bitwire/1`,
  `nightseam.duplex/1`, `@nightseam/runtime`.

## Checking it

[`naming/naming.mjs`](naming/naming.mjs) checks a repository's Markdown and
text files against [`naming/bitspark-repositories.txt`](naming/bitspark-repositories.txt),
a snapshot of the organization's repository names. The snapshot leaves out
forks, whose names belong to their upstream projects.

Copy both files into a repository (for example into `scripts/`) and run the
check in CI:

```sh
node scripts/naming.mjs            # report every other spelling, exit 1 if any
node scripts/naming.mjs --fix      # rewrite those spellings in place, then review
node scripts/naming.mjs --update   # refresh the snapshot from GitHub (needs gh)
```

What the check does and does not cover:

- **It reads prose.** It skips code blocks, inline code, link targets, URLs,
  HTML tags and quotations, but it does read ` ```text ` blocks as prose.
- **Paths can be exempted.** List them in `.namingignore` at the repository
  root: one path prefix or `*` glob per line, with `#` starting a comment.
- **It cannot see everything.** It cannot tell a project from an ordinary word
  for names such as `stack`, `graph` or `schema`, which it lists and skips. It
  does not find spaced forms such as `Logos DB`, and it does not read code
  comments or user-interface text. The rule still applies to all of these;
  review catches them.
