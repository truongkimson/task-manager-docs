# Testing

## REST Endpoint testing

For REST Endpoint testing, Postman is used to create test suites. Test suites and environment files can be found in `/rest-endpoint-test` directory

1. `production.postman_environment.json` - environment file containing environment variables values. Needed to be modified according to testing environment before running test

2. `Task_API_test.postman_collection.json` - test suites file containing test information

In order to run the test suite, ensure newman is installed. More from [here](https://www.npmjs.com/package/newman)

Run

```bash
newman run Task_API_test.postman_collection.json -e production.postman_environment.json
```

A sample test report can be found in `\rest-endpoint-test\newman`
   
## ReactJs app testing

For ReactJs app, testing is done using Jest and React Testing Libraries

Test files are located inside `__test__` folders and/or suffixed with `.test.js`

At the `/task-manage-client` directory, run tests with

```bash
    npm run test
```
