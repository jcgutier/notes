
- [Tracing](#tracing)

# Tracing

It is a debugging technique that helps to understand how a script is being executed
To enable tracing in a script we can do to with `set -x`
We can set the tracing output to other file descriptor, and send the file descriptor to a file for example:

```
exec 18>> "$LOGFILE" # Open 18 file descriptor pointing to log file.                                                    
BASH_XTRACEFD=18    # Setting variable to xtrace send output to previous file descriptior.
```
