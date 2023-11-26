# typical _yi_ project structure
```bash
.
|-> /bin
|    |-> /.trash
|    |-> /debug
|    |-> /release
|   ...
|-> /src
|-> project.yi
```
## _/bin_
Directory used to contain binary data produced from compilation process.
## _/bin/.trash_
Directory used to contain all kind of compile time dependency files, objects or intermediate representations for every file in a project.
## _/bin/debug_
Default output directory for debug version of the target. Same situation for _/bin/release_
## _/src_
All sources contains here.
## _project.yi_
This file is used to provide project configuration in yi programming language itself.