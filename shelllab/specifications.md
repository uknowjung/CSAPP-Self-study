# specifications

## Functions to implement

* eval: Main routine that parses and interprets the commnad line.

* builtin_cmd: Recognizes and interprets the built-in commands: quit, fg, bg and jobs.

* do_bgfb: Implements the bg and fg built-in commands.

* waitfg: Waits for a foreground job to complete.

* sigchld_handler: Catches SIGCHILD signals.

* sigint_handler: Caches SIGINT(ctrl-c) signals.

* sigstp_handler: Catches SIGSTP(ctrl-z) signals.

## What is commandline?

The command line is a sequence of ASCII test words delimited by whitespace.

The first word in the command line is either the name of a built-in command or the pathname of an executable file.

The remaining words are command-line arguments.

### Command type

1. Built-in command: The shell executes command in the current process.

2. Executable file: The shell forks a child process(a.k.a job), then loads and runs the program(exec()) in the context of the child.

### Foreground? Background?

1. Foreground job: The shell waits for the job to terminate before awaiting the next command line. At most one job can be running in the foreground. (ex, tsh> /bin/ls -l -d)

2. Background job: The command line ends with an ampersand  "&". The shell does not wait for the job to terminate before printing the prompt and awaiting the next command line. An arbitrary number of jobs can run in the background. (ex, tsh> /bin/ls -l -d &)

### Job controls?

Move jobs back and forth between background and foreground and change the process state(running, stopped, or terminated).

* ctrl-c: Causes a SIGINT signal to be delivered to each process in the foreground job. Default action is to terminate the process.

* ctrl-z: Causes a SIGSTP signal to be delivered to each process in the foreground job. Defualt action is to place a process in the stopped state, where it remains until it is awakened by the receipt of a SIGCONT signal.

* jobs: List the running and stopped background jobs.

* bg <job>: Change a stopped background job to a running background job.

* fg <job>: Change a stopped or running background job running in the foreground.

* kill <job>: Terminate a job.
