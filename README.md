# jest-coveragedata-null

This repro was created to reproduce [jest #7758](https://github.com/facebook/jest/issues/7758)

## Setup

Clone and then:

    $ npm i
    $ npm test

## Expected output

    $ npm test                                                                           
    
    > jest-coveragedata-null@1.0.0 test ~/git/jest-coveragedata-null
    > jest --coverage

    PASS  ./coveredFile-test.js
    coveredFile
        ✓ returns false (3ms)

    -------------------|----------|----------|----------|----------|-------------------|
    File               |  % Stmts | % Branch |  % Funcs |  % Lines | Uncovered Line #s |
    -------------------|----------|----------|----------|----------|-------------------|
    All files          |       50 |       50 |       50 |    66.67 |                   |
    coveredFile.js     |    66.67 |       50 |      100 |      100 |                 2 |
    notcoveredFile.js  |        0 |      100 |        0 |        0 |                 2 |
    -------------------|----------|----------|----------|----------|-------------------|
    Test Suites: 1 passed, 1 total
    Tests:       1 passed, 1 total
    Snapshots:   0 total
    Time:        1.549s
    Ran all test suites.


## Actual output

    npm test

    > jest-coveragedata-null@1.0.0 test ~/git/jest-coveragedata-null
    > jest --coverage

    PASS  ./coveredFile-test.js
    coveredFile
        ✓ returns false (2ms)

    Running coverage on untested files...Failed to collect coverage from ~/git/jest-coveragedata-null/notcoveredFile.js
    ERROR: Cannot read property 'coverageData' of null
    STACK: TypeError: Cannot read property 'coverageData' of null
        at _default (~/git/jest-coveragedata-null/node_modules/jest/node_modules/jest-cli/build/generateEmptyCoverage.js:72:44)
        at Object.worker (~/git/jest-coveragedata-null/node_modules/jest/node_modules/jest-cli/build/reporters/coverage_worker.js:51:45)
        at execFunction (~/git/jest-coveragedata-null/node_modules/jest-worker/build/workers/processChild.js:165:17)
        at execHelper (~/git/jest-coveragedata-null/node_modules/jest-worker/build/workers/processChild.js:149:5)
        at execMethod (~/git/jest-coveragedata-null/node_modules/jest-worker/build/workers/processChild.js:153:5)
        at process.on.request (~/git/jest-coveragedata-null/node_modules/jest-worker/build/workers/processChild.js:72:7)
        at process.emit (events.js:182:13)
        at emit (internal/child_process.js:812:12)
        at process._tickCallback (internal/process/next_tick.js:63:19)
    ----------------|----------|----------|----------|----------|-------------------|
    File            |  % Stmts | % Branch |  % Funcs |  % Lines | Uncovered Line #s |
    ----------------|----------|----------|----------|----------|-------------------|
    All files       |    66.67 |       50 |      100 |      100 |                   |
    coveredFile.js |    66.67 |       50 |      100 |      100 |                 2 |
    ----------------|----------|----------|----------|----------|-------------------|
    Test Suites: 1 passed, 1 total
    Tests:       1 passed, 1 total
    Snapshots:   0 total
    Time:        1.73s
    Ran all test suites.


## How I fixed it

On my machine, updating `babel-jest` to `^24.0.0` solves the issue.

