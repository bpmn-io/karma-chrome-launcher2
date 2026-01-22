# karma-chrome-launcher2


> Fork of unmaintained [karma-chrome-launcher](https://github.com/karma-runner/karma-chrome-launcher).

## Installation

The easiest way is to keep `karma-chrome-launcher2` as a devDependency in your `package.json`,
by running

```bash
$ npm i -D karma-chrome-launcher2
```

## Configuration

```js
// karma.conf.js
module.exports = function(config) {
  config.set({
    browsers: ['Chrome', 'Chrome_without_security'], // You may use 'ChromeCanary', 'Chromium' or any other supported browser

    // you can define custom flags
    customLaunchers: {
      Chrome_without_security: {
        base: 'Chrome',
        flags: ['--disable-web-security', '--disable-site-isolation-trials']
      }
    }
  })
}
```

The `--user-data-dir` is set to a temporary directory but can be overridden on a custom launcher as shown below.
One reason to do this is to have a permanent Chrome user data directory inside the project directory to be able to
install plugins there (e.g. JetBrains IDE Support plugin).

```js
customLaunchers: {
  Chrome_with_debugging: {
    base: 'Chrome',
    chromeDataDir: path.resolve(__dirname, '.chrome')
  }
}
```

You can pass list of browsers as a CLI argument too:

```bash
$ karma start --browsers Chrome,Chrome_without_security
```

## Headless Chromium with Puppeteer

The Chrome DevTools team created [Puppeteer](https://github.com/GoogleChrome/puppeteer) - it will automatically install Chromium for all
platforms and contains everything you need to run it from within your CI.

### Available Browsers
*Note: Headless mode requires a browser version >= 59*

- Chrome (CHROME_BIN)
- ChromeHeadless (CHROME_BIN)
- Chromium (CHROMIUM_BIN)
- ChromiumHeadless (CHROMIUM_BIN)
- ChromeCanary (CHROME_CANARY_BIN)
- ChromeCanaryHeadless (CHROME_CANARY_BIN)
- Dartium (DARTIUM_BIN)

#### Usage
```bash
$ npm i -D puppeteer karma-chrome-launcher
```

```js
// karma.conf.js
process.env.CHROME_BIN = require('puppeteer').executablePath()

module.exports = function(config) {
  config.set({
    browsers: ['ChromeHeadless']
  })
}
```

----

For more information on Karma see the [homepage].

[homepage]: https://karma-runner.github.io
