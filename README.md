# cider-debugger-stops-working

## Reproducing the issue

Demonstrates the bug in the cider debugger where a break point can only be used once.

To exhibit the behavior, start a REPL, switch to the `cider-debugger-stops-working.handler` namespace, run `(start)`, set a breakpoint on `hello-world` with `C-u C-M-x`, then in your browser visit http://localhost:3000/.

When the breakpoint activates, press `c` to continue execution (or in cider 0.20 and later press `C`).

Refresh your browser and notice the breakpoint does not activate a second time.

## Working around the issue

To work around the issue change `debug?` to `true`, restart your REPL, then follow the above steps, but when you refresh your browser the breakpoint will activate again.

## The issue

The issue appears to be that when there is no binding established for `*skip-breaks*` the root value of the var is modified, and it is never reset.
