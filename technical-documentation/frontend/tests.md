# Tests

### Run tests

To run the tests you can use the following command:

```text
gulp test
```

It will build all source files including tests and run Web Component Tester.

### Tests architecture

All test files will have `.spec`  postfix extention. For instance `permission-controller.spec.html` . Test files are placed in elements src directories.

Entry point file `index.spec.html`  for tests is located in the`application_root/src/tests` directory. It has only one single line for tests loading :

```text
WCT.loadSuites([<!--testSources-->]);
```

`<!--testSources-->` comment will be replaced with resolved tests pathes during build process.

