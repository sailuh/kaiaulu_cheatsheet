Below is a full view of the git.R executable's documentation in the CLI.
```r
exec$ rscript git.R -h
USAGE:
  git.R file_changes help
  git.R file_changes <tools.yml> <project_conf.yml> <save_file_name_path>
  git.R entity_changes help
  git.R entity_changes <tools.yml> <project_conf.yml> <save_file_name_path>
  git.R file_network help
  git.R file_network <tools.yml> <project_conf.yml> <node_save_file_name_path> <edge_save_file_name_path> (--author-file | --committer-file | --commit-file | --author-committer)
  git.R entity_network help
  git.R entity_network <tools.yml> <project_conf.yml> <node_save_file_name_path> <edge_save_file_name_path> (--author-entity | --committer-entity | --commit-entity | --author-committer)
  git.R (-h | --help)
  git.R --version

DESCRIPTION:
  Provides a suite of functions to interact with Git. Please see
  Kaiaulus README.md for instructions on how to create <tool.yml>
  and <project_conf.yml>.

COMMANDS:
   file_changes                 Outputs a git log using parse_gitlog().
   entity_changes               Outputs log of changed entities using parse_gitlog_entity(). An entity is a function, class, or method in R.
   file_network                 Outputs a csv of nodes and csv of edges of a network made using the selected mode.
   entity_network               Outputs a csv of nodes and csv of edges of a network made using the selected mode.

ARGUMENTS:
  <tools.yml>                   path to tools.yml file
  <project_conf.yml>            path to configuration file for project you want to analyze
  <save_file_name_path>         file path where output will be saved
  <node_save_file_name_path>    file path where csv of nodes of the network will be saved
  <edge_save_file_name_path>    file path where csv of edges of the network will be saved

OPTIONS:
  -h --help                     Show this screen.
  --version                     Show version.
  --author-file                 Mode that outputs which authors edited which files
  --author-entity               Mode that outputs which authors edited which entities
  --committer-file              Mode that outputs which committers edited which files
  --committer-entity            Mode that outputs which committers edited which entities
  --commit-file                 Mode that outputs which files were edited in each commit
  --commit-entity               Mode that outputs which entities were edited in each commit
  --author-committer            Mode that outputs which authors made changes with which committers 
```
exec $ rscript git.R file_changes help  
ℹ Outputs a git log to save_file_name_path using parse_gitlog().  
exec $ rscript git.R entity_changes help  
ℹ Outputs log of changed entities to save_file_name_path using parse_gitlog_entity. An entity is a function, class, or method in R.  
exec$ rscript git.R file_network help  
ℹ Outputs csv of nodes and csv of edges of a file co-change network made using the selected mode. Use git.R --help for mode descriptions.  
exec$ rscript git.R entity_network help  
ℹ Outputs csv of nodes and csv of edges of an entity network made using the selected mode. Use git.R --help for mode descriptions.  
  
Executable -help documentation follows the format shown above.  
The sections to be included are as follows;  
  
USAGE:  
Syntax of command execution with required arguments and options.  
  
DESCRIPTION:  
Breif description of what the executable does. Also references Kaiaulu's README.md for more info.  
  
COMMANDS:  
Descriptions of each command. This section can be ommitted in executables with only one command, since in those cases the description encapsulates the command's purpose.  
  
ARGUMENTS:  
Describes what each argument expects.  
  
OPTIONS:  
Describes what each optional flag does.  
  
Additionally there are help options for each command which provide a more in depth explanation of the command.  
  
Kaiaulu executables use docopt. See docopt's documentation for syntax explanations.  
