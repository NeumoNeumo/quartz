---
tags:
  - terminal
  - linux
  - CLI
aliases: []
id: TTY
---

At first, a large box with lights and switches on it is used to control the huge computer and display output. That large box is called **console**(because it is used to control) or **terminal**(because it is IO handler at the user's end)

Then a device that can both type and print characters is invented to remotely control that computer. That is teletype(**tty**), a.k.a. teleprinter and teletypewriter.

A user interacts with the master side (`ptmx`) of a "pseudo tty"(`pty`). And a program interacts with the slave side (`pts`) of an `pty`. In modern linux, `pty` is implemented by `pts`(slave) and `ptmx`(master). Every time `ptmx` is opened, a associated `pts` file is created. If you want to execute a command, the command is written into the `ptmx` file then to `pts` and then transferred to the shell program behind it. Interestingly, they superficially opens the same `ptmx` but those `ptmx`s are different underneath. For more information about how the terminal multiplexer works, check [this repo](https://github.com/deadpixi/mtm)  and [this linux man](https://linux.die.net/man/4/ptmx) please. 

The terminal's ECHO flag is on by default. When the kernel places characters into the buffer, it copies them unchanged and sends them back to the PTY master, which are then displayed on the screen. This explains the echo delays in ssh with network latency.

![](https://www.linusakesson.net/programming/tty/case3.png)

![](https://www.linusakesson.net/programming/tty/case4.png)

`terminfo` is a dataset recording the capability and standard of different kinds of terminals so that program knowns which feature is supported like color display and which sequence to output to do some special function like clear the screen (Different terminals have different "dialects".). The environment variable `$TERM` specifies which terminal is being used. Except for the data that has already been set in `terminfo`, we still have some variables to set like for this terminal like "raw mode/canonical mode(cooked mode)". These variables can be tweaked by `stty`. You can use `libtinfo` to query the dataset. `tput` is a cli of `libtinfo`.

`ncursors` is like QT or GTK in the world of TUI.

# Reference
https://www.linusakesson.net/programming/tty/index.php
