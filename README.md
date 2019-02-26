# shared.ea.spinnakertest

## Introduction

This project was scaffolded using the [EBSCO Node Express](https://github.com/EBSCOIS/platform.infrastructure.generator-node-express) generator.

## Dependencies

Dependencies are found in the `package.json` file.

## Local Development Setup

### Starting the server

1.  `npm ci`
2.  `npm run dev`

* Web server listens at http://localhost:8080
* Browse your REST API at http://localhost:8080/docs

### Docker

1.  `aws ecr get-login --no-include-email --registry-ids 201777367430`
2.  Execute the `docker login ...` command that was generated from the previous command
3.  `docker build --tag spinnakertestnodeservice:latest .`
4.  `docker run -p 8080:8080 spinnakertestnodeservice:latest`

* `docker ps` # prints active containers
* `docker stop <container name>` # shuts down the container

## Linting

This project comes with [ESLint](http://eslint.org/) and [Prettier](https://prettier.io) pre-configured. It uses [husky](https://github.com/typicode/husky) and [lint-staged](https://github.com/okonet/lint-staged/releases) to automatically detect and, if possible, fix linting errors prior to running `git commit`.

This project extends the [ESLint Recommended](https://eslint.org/docs/rules/) preset.

## Testing

### Unit/Integration tests

* To execute unit/integration tests, run: `npm test`. This runs in `watch` mode by default.
* Unit/Integration tests are written using [Jest](https://jestjs.io/)
* All test files should be placed within a `__tests__` directory.

### Contract tests

* To execute contract tests locally, run

```sh
./contract/run-tests.sh 201777367430.dkr.ecr.us-east-1.amazonaws.com
```

* All contract tests should be placed within a `contract/tests` directory
* This project uses [Spring Cloud Contract](https://spring.io/projects/spring-cloud-contract) to run contract tests
* By default, contract tests will execute against the stubs specified for each service in the `src/config/services.json` file. The `stubRunnerId` property specifies the location of the stubs in artifactory, and follows the format: `<STUB_GROUP>:<STUB_ARTIFACT>:<STUB_VERSION>`

### E2E tests

* To start E2E tests, run: `npm run e2e`
* E2E tests are written using Jest
* These tests should be placed within a `e2e/` directory

### Performance tests

* This project comes preconfigured to run [JMeter](https://jmeter.apache.org/) performance tests on the pipeline.
* Simply add your `.jmx` files under a `performance/` directory at the project root and then specify the test configurations in the `runPerformanceTests` function in the `Jenkinsfile`

## Middleware

This project comes preconfigured with the Logging, Tracing, and Metrics middleware from the [EBSCO Node Platfrom Development Kit (PDK)](https://github.com/EBSCOIS/platform.shared.node-express-pdk). The PDK also adds a service health endpoint for liveness and readiness probes. [Click here](https://github.com/EBSCOIS/platform.infrastructure.hydra/wiki/Deployment-Manifest#service-health-policy-optional) for more information on customizing the service health policy.
