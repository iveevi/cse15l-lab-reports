# Lab 5 Report

In this report, we will be covering additional commands in the Bash shell which
are useful for other general purposes.

## `which` and `where`

These commands are very useful for finding the location of binary files. For
example, when working with Java, it can be useful to know where the compiler and
interpreter reside in the system.

The `which` command reports the location of the requested command as it is used
normally:

```
$ which java
/usr/bin/java
```

Sometimes, more than one version of Java is available and preside in the system.
To find all such instances, the `where` command be used:

```
$ where javac
/usr/bin/javac
/usr/lib/jvm/default/bin/javac
```

## Time with `time`

This command can be used to gauge the time taken by arbitrary commands. There
are usually two versions of this command on most shells, one that acts as a
reserved keyword in the shell, and one stored as `/bin/time`.

```
$ where time
time: shell reserved word
/usr/bin/time
```

The former is a simplified version of the latter. For example, timing the `find`
command would yield an output similar to below:

```
$ time find ~ -name lab5.md
/home/venki/documents/cse15l-lab-reports/reports/lab5.md
[omitted]
find ~ -name lab5.md  0.63s user 0.88s system 98% cpu 1.531 total
```

This is informative as is, but we can get even more information with the
`/bin/time` version:

```
$ /bin/time find ~ -name lab5.md
/home/venki/documents/cse15l-lab-reports/reports/lab5.md
[omitted]
0.61user 1.21system 0:07.29elapsed 25%CPU (0avgtext+0avgdata 12496maxresident)k
508416inputs+0outputs (1major+10406minor)pagefaults 0swaps
```

This version gives much more detailed information aside from just the time
taken; it also shows system memory usage (peak and average), processor usage,
and more.

To obtain a cleaner view of this data, the verbose `-v` flag can be added:

```
$ /bin/time -v find ~ -name lab5.md
/home/venki/documents/cse15l-lab-reports/reports/lab5.md
[omitted]
Command exited with non-zero status 1
	Command being timed: "find /home/venki -name lab5.md"
	User time (seconds): 0.50
	System time (seconds): 0.97
	Percent of CPU this job got: 98%
	Elapsed (wall clock) time (h:mm:ss or m:ss): 0:01.50
	Average shared text size (kbytes): 0
	Average unshared data size (kbytes): 0
	Average stack size (kbytes): 0
	Average total size (kbytes): 0
	Maximum resident set size (kbytes): 12500
	Average resident set size (kbytes): 0
	Major (requiring I/O) page faults: 0
	Minor (reclaiming a frame) page faults: 10405
	Voluntary context switches: 1
	Involuntary context switches: 111
	Swaps: 0
	File system inputs: 0
	File system outputs: 0
	Socket messages sent: 0
	Socket messages received: 0
	Signals delivered: 0
	Page size (bytes): 4096
	Exit status: 1
```

## When am I, `date`?

A simple command that displays the current date and time:

```
$ date
Mon Mar 13 01:46:20 PM PDT 2023
```

The nice part of this command is that it offers format options to print the date
in a custom format. Examples are shown below:

```
$ date +"%H:%M:%S"
13:48:14
```

```
$ date +"%m/%d"
03/13
```

The `--help` option for `date` shows all available format options.
