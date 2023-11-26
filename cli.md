# CLI - command line interface
---
The "cli" utility application is a complex tool for creating and managing _yi_ projects. (take a look into **"project.md"**)

## Commands
```bash
yi-cli help
```
Prints typical 'help-like' text onto a console. Shows all general commands and simple descriptions to them.

---
```bash
yi-cli help CMD
```
Prints more describable information about certain CMD (command)

---
```bash
yi-cli help-all-cmd
```
Prints ALL possible commands and small descriptions to them.

---
```bash
yi-cli create NAME [options]
```
 + [no-options] - creates small hello world project in _NAME_ directory.
 + [--output-dir=DIR] - setup output directory to _DIR_ directory.
 + [--target-arch=x86_64|...] - setup target architecture.
 + [--target-kind=executable|static-lib|shared-lib|_module_] - setup target kind. _(recommended to set)_
 + [--depends-from="PROJECT0;PROJECT1;...;PROJECTN"] - setup with dependency from other project(-s).
 + [todo - add more]

---