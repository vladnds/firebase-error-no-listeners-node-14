## Repository to reproduce error registering error handler

This issue appeared after upgrading functions from node 10 to node 14.
Cannot use Sentry because of it - it registers `uncaughtException` handlers.

To reproduce issus:
1. Run functions shell
```shell
npm run build
firebase functions:shell --project <specify you project id here>
```

2. Add some uncaught exception handler
```javascript
process.on("uncaughtException", function(err) {
    console.error("uncaughtException");
})
```

3. See error:
```
Uncaught:
TypeError [ERR_INVALID_REPL_INPUT]: Listeners for `uncaughtException` cannot be used in the REPL
    at process.<anonymous> (repl.js:309:15)
    at process.emit (events.js:387:35)
    at _addListener (events.js:418:14)
    at process.addListener (events.js:466:10)
    at REPL7:1:9
    at Script.runInContext (vm.js:144:12)
    at REPLServer.defaultEval (repl.js:488:29)
    at bound (domain.js:416:15)
    at REPLServer.runBound [as eval] (domain.js:427:12)
    at REPLServer.onLine (repl.js:819:10)
    at REPLServer.emit (events.js:375:28)
    at REPLServer.emit (domain.js:470:12)
    at REPLServer.Interface._onLine (readline.js:364:10)
    at REPLServer.Interface._line (readline.js:700:8)
    at REPLServer.Interface._ttyWrite (readline.js:1045:14)
    at REPLServer.self._ttyWrite (repl.js:912:9) {
  code: 'ERR_INVALID_REPL_INPUT'
}
```
