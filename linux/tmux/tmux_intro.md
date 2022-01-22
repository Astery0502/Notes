# Introduction to TMUX #

## Definition and Implementation ##

Main uses of Tmux

1. Protect running programs on a remote server from connection drops by running them inside tmux.  
> tmux is seperated from the ssh process, which is running without ssh connect.

2. Allow programs running on a remote server to be accessed from multiple different local computers.  
> tmux can be attatched from different users as it is a global process behind the terminal.

3. Work with multiple programs and shells together in one terminal, a bit like a window manager.  
> inside the tmux running under one terminal, there can be other terminals. And in each terminal, the window of which is also under controled.

## Tmux Concepts ##
### tmux servers and tmux clients ###

1. Tmux keeps its all states in one process, called tmux server. Tmux server runs in the background and manage all the program running inside tmux and keeps track of the outputs. The tmux server is started automatically when the user runs a tmux command and by default exits when there are no running programs.

2. Users attach to the tmux server by starting a client. tmux client takes over the terminal and talks to the server using a socket file in **/tmp**. Each client runs in one terminal (even the tmux itself), each client is identified by the name of the outside terminal where it is started.

### Sessions, windows and panes ###

1. Every terminal in the tmux belongs to a pane, which is a rectangular area showing the content of the terminal. Each termninal only shows in one pane, thus the term pane can be pointed to all of the panes, terminals and programs inside it. 

2. Each pane appears in one window. A window can be composed of multiple panes which together cover the entire window. A window normally takes up the terminal where the tmux is started. The sizes and positions of all the panes in the window is called the window layout. 

3. There is one pane in each window called active pane, this is where any text typed is sent and is the default pane used for command that target the window.

4. Multiple windows are together grouped into sessions. If a window is part of a session, it is said to be linked to that session. Windows may be attached to different windows at the same time, but mostly only one session attached to. 

5. Each session has current window. It is the window displayed when session is attached and is the default window used for command that target the session. The window becomes the last window as the current window is changed from which.

6. A session may be attached to multiple clients, which means it is shown in the outside terminal where the client is running. Any text typed into the outside terminal is sent to the active pane in the current window of the attached session. Sessions do not have an index but a unique name .

Summary: 
- Programs runs in terminals in panes, which each belong to one window. 
- Each window has a name and an active pane.
- Windows are linked to various sessions.
- Each session has a list of windows, each with an index.
- One of the windows in a session is the current window.
- Sessions are attached to zero or more clients.
- Each client is attached to one sessions.

Summary of terms:

| Term           | Description                                                                          |
|----------------|--------------------------------------------------------------------------------------|
| Client         | Attaches a tmux session from an outside terminal such as xterm(1)                    |
| Session        | Groups one or more windows together                                                  |
| Window         | Groups one or more panes together, linked to one or more sessions                    |
| Pane           | Contains a terminal and running program, appears in one window                       |
| Active pane    | The pane in the current window where typing is sent; one per window                  |
| Current window | The window in the attached session where typing is sent; one per session             |
| Last window    | The previous current window                                                          |
| Session name   | The name of a session, defaults to a number starting from zero                       |
| Window list    | The list of windows in a session in order by number                                  |
| Window name    | The name of a window, defaults to the name of the running program in the active pane |
| Window index   | The number of a window in a session's window list                                    |
| Window layout  | The size and position of the panes in a window                                       |

## Using Tmux Interactively ##

### Creating new sessions ###

To create a tmux simply without sending any argument:
```
tmux new
tmux new-session
```

By defaut, the first session will be called **0**, and the second **1** and so on. new-session allows a name to be specified for the session with the *-s* flag.
```
tmux new -ssessionname
```

A command can be given instead of running a shell by passing additional arguments. If one argument is given, tmux will pass it to the shell, if more than one it runs the command directly.
```
tmux new 'vim ./setup.py'
tmux new -- vim ./setup.py
```

By default, the tmux runs the first window in the session after whatever is running in it. The *-n* flag gives a name to use instead.
```
tmux new -nmytopwindow top
```

### prefix keys and help keys
<kbd>Ctrl-b</kbd> serves as the prefix key for any keys sent to control the tmux itself. While the other keys are forwarded to the program running in the active pane of the current window.

<kbd>C-b ?</kbd> enters view mode to show help text.  
<kbd>C-b /</kbd> shows the description of a single key:  
```
C-b ? List key bindings
```

### The command prompt

Call the interactive command prompt by pressing <kbd>C-b :</kbd>

Multiple commands can be entered together at the command prompt by separating them with a colon (;). This is called a command sequence.

### Attaching and detaching

- Detaching from tmux means that the client exits and detaches from the outside terminal, returning to the shell and leaving the tmux session and any programs inside it running in the background. 

- To detach tmux, the <kbd>C-b d</kbd> key binding is used.  
When tmux detaches , it will print a message with the session name.  

- The <kbd>attach-session</kbd> command attaches to an existing session. Without any arguments, it will attach to the most recently used session that is not already attached.

```
tmux attach
```

Or <kbd>-t</kbd> gives the name of a session to attach to:
```
tmux attach -dtsessionname
```

- The <kbd>new-session</kbd> command has a <kbd>-A</kbd> flag to attach to an existing session if it exists, or create a new one if it does not. For a session named <kbd>mysession</kbd>:  
```
tmux new -Asmysession
```

- The -D flag may be added to make new-session also behave like attach-session with -d and detach any other clients attached to the session.

### Listing sessions ###
The list0session (alias ls) shows a list of available sessions that can be attached.
```
tmux ls
```

### Killing tmux entirely ###
- If there are no sessions, windows or panes inside tmux, the server will exit.
- Or using the *kill-server* command.

### Creating new windows ###
1. <kbd>C-b c</kbd> keybinding or the <kbd>new-window</kbd> command.
2. the useful flag of the <kbd>new-window</kbd> command in the command prompt:
    - -d flag creates the window but does not make it the current window.
    - -n allows a name for the new window to be given. 
```
:neww -dnmynewwindow
```
    - 0t specifies a target for the window. Command targets have a special syntax, often given a window index. This creates a window at index 999:
```
neww -t999
```

