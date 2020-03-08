# open-md-lint

`open-md-lint` is an open source module for markdown file format checking.

## Getting start

### Install

`npm i open-md-lint`

### Demo

package.json

```json
{
  "scripts": {
    "md-lint": "open-md-lint"
  }
}
```

```shell
# npm run md-lint
```

## Docs

### The definition of Config

```typescript
interface Config {
  requires?: string;
  patterns: string[];
  options: {
    useGitIgnore?: boolean;
    usePackageJson?: boolean;
    configKey?: string;
    gitIgnoreFile?: string;
    ignore?: string[];
    cwd?: string;
  };
}
```

- requires(optional): Path to the js file containing the user deinfined rules, the default configuration is declare in the src/default_requires.js
- For the rest configuration, please refer to [deglob](https://www.npmjs.com/package/deglob)

#### Default config

```javascript
{
  patterns: [ '**/*.md' ],
  options: {
    useGitIgnore: true,
    ignore: [ 'node_modules/**/*' ],
  },
}
```

#### Customer configuration

Note: In order to facilitate the user to integrate the configuration into the package.json file, after loading the configuration file, the configuration will be read from the `open-md-lint` field, so the specific configuration should be included in the `open-md-lint` field, for example:

```json
{
  "open-md-lint": {
    "requires": "./requires.js",
    "patterns": [ "**/*.md" ],
    "options": {
      "useGitIgnore": true,
      "ignore": [ "node_modules/**/*" ]
    }
  }
}
```

You can place the configuration anywhere and specify the file location by setting the `MD_LINT_CONFIG_PATH` environment variable. E.g

```bash
# export MD_LINT_CONFIG_PATH=./open-md-lint.json
# npm run md-lint
```

#### Customer md-lint rules

You can specify which checks are enabled. This option requires a js file, for example:

```javascript
module.exports = [
  require('remark-lint-final-newline'),
  require('remark-lint-list-item-bullet-indent')
]
```

The js file can be placed in any location and specified by the `requires` field in the configuration. If it is a relative path, the current path is automatically added to form an absolute path.
