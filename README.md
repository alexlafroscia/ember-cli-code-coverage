# ember-cli-code-coverage

Code coverage using [Istanbul](https://github.com/gotwarlost/istanbul) for Ember apps.

## Installation

* `ember install ember-cli-code-coverage`

## Usage

Coverage will only be generated when an environment variable is true (by default `COVERAGE`) and running your test command like normal.

For example: 

`COVERAGE=true ember test`

## Configuration

Configuration is optional. It should be put in a file at `config/coverage-config.js`.

#### Options

- `coverageEnvVar`: Defaults to 'COVERAGE'. This is the environment variable that when set will cause coverage metrics to be generated. 

- `reporters`: Defaults to ['lcov', 'html']. The `json-summary` reporter will be added to anything set here, it is required. This can be any [reporters supported by Istanbul](https://github.com/gotwarlost/istanbul/tree/master/lib/report)s.

- `excludes`: Defaults to ['*/mirage/**/*']. An array of globs to exclude from instrumentation. Useful to exclude files from coverage statistics.

- `coverageFolder`: Defaults to 'coverage'. A folder relative to the root of your project to store coverage results.

## Using when intercepting all ajax requests in tests

Aka when using ember-cli-mirage or Pretender. 

To work, this addon has to post coverage results back to a middleware at `/write-coverage`.

```
// in mirage/config.js

  this.passthrough('/write-coverage');
  this.namespace = 'api';  // It's important that the passthrough for coverage is before the namespace, otherwise it will be prefixed. 
```


## Inspiration

This addon was inspired by [`ember-cli-blanket`](https://github.com/sglanzer/ember-cli-blanket). 
The primary differences are that this addon uses Istanbul rather than Blanket for coverage and it instruments your application code as part of the build, when enabled. 
