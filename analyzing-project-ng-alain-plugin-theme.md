---
title: "Analyzing Project: ng-alain/plugin-theme - 01"
date: "2024-03-25"
categories: 
  - "code-learning"
  - "learn-open-source-project"
tags: 
  - "less"
  - "open-source"
  - "typescript"
coverImage: "845d4d0fec8347e2ac28c0fa0dd76745-scaled.jpg"
---

# Checklist

- Project: [https://github.com/ng-alain/plugin-theme](https://github.com/ng-alain/plugin-theme)
- Template Project: [https://github.com/ng-alain/ng-alain](https://github.com/ng-alain/ng-alain)
- Library: [https://github.com/NG-ZORRO/ng-zorro-antd](https://github.com/NG-ZORRO/ng-zorro-antd)

# Features

- themeCss Generate theme styles for theme switching
- colorLess Generate color.less, dynamically customize colors

# Usage

```
# Generate theme styles for theme switching
npx ng-alain-plugin-theme -t=themeCss
# Generate `color.less`, dynamically customize colors
npx ng-alain-plugin-theme -t=colorLess

# DEBUG MODE
npx ng-alain-plugin-theme -t=themeCss -debug
```

# package.json

```json
 "bin": {
    "ng-alain-plugin-theme": "lib/index.js"
  },
    "sideEffects": false,
  "scripts": {
    "tsc": "tsc",
    "watch": "tsc --w",
    "lint": "eslint 'lib/**/*.ts'",
    "build": "bash ./build.sh",
    "build:test": "bash ./build.sh -t",
    "test": "TS_NODE_PROJECT=./test/tsconfig.json npm run mocha --recursive ./test/**/*.spec.ts",
    "mocha": "mocha -r ts-node/register",
    "release": "npm run build && cd dist && npm publish --access public",
    "release:next": "npm run build && cd dist && npm publish --access public --tag next"
  },
```

- `bin` points to a packaged program entry.

# index.ts

```typescript
const cli = meow({
  help: `
  Usage
    ng-alain-plugin-theme
  Example
    ng-alain-plugin-theme -t=themeCss -c=ng-alain.json
  Options
    -t, --type    Can be set 'themeCss', 'colorLess'
    -n, --name    Angular project name
    -c, --config  A filepath of NG-ALAIN config script
    -d, --debug   Debug mode
  `,
  flags: {
    type: {
      type: 'string',
      default: 'themeCss',
      alias: 't',
    },
    name: {
      type: 'string',
      alias: 'n',
    },
    config: {
      type: 'string',
      default: 'ng-alain.json',
      alias: 'c',
    },
    debug: {
      type: 'boolean',
      default: false,
      alias: 'd',
    },
  },
});
```

- Define a `command line` tool using `memow`
    
- Example `ng-alain-plugin-theme -t=themeCss -c=ng-alain.json`
    

```ts
let config: { theme: Config; colorLess: Config; [key: string]: Config };
```

- Define a variable named `config`, Here are its types.

```typescript
{ 
    theme: Config;
    colorLess: Config;
    [key: string]: Config 
};

// The type of Config
export interface Config {
  debug?: boolean;
  name?: string;
  // less compile configuration
  buildLessOptions?: Less.Options;
}
```

# Start executing function

```typescript
try {
// Get configuration file path from command line
  const configFile = resolve(process.cwd(), cli.flags.config);
  // Determine whether the file exists, and read JSON if it exists.
  if (existsSync(configFile)) {
    config = getJSON(configFile);
  } else {
    console.error(`The config file '${cli.flags.config}' will not found`);
    process.exit(1);
  }
} catch (err) {
  console.error('Invalid config file', err);
  process.exit(1);
}

// Pass the name and debug in the command line to the corresponding object
['theme', 'colorLess'].forEach(key => {
  if (config[key] == null) config[key] = {};
  config[key].name = cli.flags.name;
  config[key].debug = cli.flags.debug === true;
});

// Execute function according to type type
if (cli.flags.type === 'themeCss') {
  buildThemeCSS(config.theme);
} else if (cli.flags.type === 'colorLess') {
  genColorLess(config.colorLess);
} else {
  throw new Error(`Invalid type, can be set themeCss or colorLess value`);
}
```

- By switching config and command line control, we end up running two different functions `buildThemeCss`,`genColorLess`
- The theme script of `ng-alalin` is actually

```
"theme": "ng-alain-plugin-theme -t=themeCss",
```

- ng-alain.json

```json
{
  "$schema": "./node_modules/ng-alain/schema.json",
  "theme": {
    "list": [
      {
        "theme": "dark"
      },
      {
        "theme": "compact"
      },
       {
        "theme": "yuhong",
        "modifyVars": {
          "@primary-color": "#C04851",
          "@yunzai-default-header-bg": "#C04851",
          "@yunzai-default-aside-nav-text-hover-color": "#C04851",
          "@yunzai-default-aside-nav-selected-text-color": "#C04851",
          "@yz-application-bgColor": "#FFF",
          "@yz-application-border-shadow": "#888",
          "@yz-application-topic-bgColor": "#B54049",
          "@yz-application-topic-text-color": "#FFF",
          "@yz-application-topic-text-hover-bgColor": "#FFF",
          "@yz-application-topic-text-hover-color": "#C04851",
          "@yz-application-list-ul-h5-color": "#000",
          "@yz-application-list-ul-a-color": "#000",
          "@yz-application-list-ul-a-hover-color": "#FFF",
          "@yz-application-list-ul-a-hover-bgColor": "#C04851",
          "@yz-application-list-item-h4p-color": "#000",
          "@yz-application-list-item-p-color": "#000",
          "@yz-application-list-item-li-hover-color": "#FFF",
          "@yz-application-list-item-li-hover-bgColor": "#C04851"
        }
      },
    ]
  }
}
```

```ts
// The function is called with the param: config.name
buildThemeCSS(config.theme);
export async function buildThemeCSS(config: ThemeCssConfig): Promise<void> {}
```

- typeof `config` and `ThemeCssConfig`

```ts
export interface Config {
  debug?: boolean;
  name?: string;
  buildLessOptions?: Less.Options;
}

export interface ThemeCssConfig extends Config {
  /** Specify the node_modules directory, default: `node_modules` */
  nodeModulesPath?: string;
  /** Project entry style file path, default: `src/styles.less` */
  projectStylePath?: string;
  /** Additional library style entries */
  additionalLibraries?: string[];
  /** Additional theme variables entries */
  additionalThemeVars?: string[];
  /** Whether to compress, default: `true` */
  min?: boolean;
  /** Theme list */
  list?: ThemeCssItem[];
}

export interface ThemeCssItem {
  /**
   * Unique identifier
   */
  key?: string;
  /**
   * Save path after generation, default: `src/assets/style.{key}.css`
   */
  filePath?: string;
  /**
   * Theme type, can be set `dark` and `compact`, must choose between `theme` and `modifyVars`
   */
  theme?: 'dark' | 'compact';
  /**
   * Project theme less variables, except for `ng-zorro-antd`, `@delon/*`, and the specified `projectStylePath` file
   */
  projectThemeVar?: string[];
  /**
   * Custom Less variables, must choose between `theme` and `modifyVars`
   */
  modifyVars?: { [key: string]: string };
}
```

- Okay, let’s go through the index file process again and figure out what is passed in the config.
- When the program starts, `-t=themeCss` is passed in externally, and nothing else.
- The program starts running

```ts
let config: { theme: Config; colorLess: Config; [key: string]: Config };
```

- A config variable is defined, which contains two attributes: theme and colorless. The type is the above-mentioned Config type.
- Now its value is `undefined`

```ts
const configFile = resolve(process.cwd(), cli.flags.config);
```

- `process.cwd` get execution path.
- `cli.flag.config` default was `ng-alain.json`

```ts
// get ng-alain.json
config = getJSON(configFile);
// Append variables to config
['theme', 'colorLess'].forEach(key => {
  if (config[key] == null) config[key] = {};
  config[key].name = cli.flags.name;
  config[key].debug = cli.flags.debug === true;
});
```

- The current configuration value is

```json
{
   "theme":{
      "list":[
         {
            "theme":"dark"
         },
         {
            "theme":"compact"
         },
         {
            "theme":"yuhong",
            "modifyVars":{...}
         }
      ],
      "name":"",
      "debug":false
   },
   "colorLess":{
      "name":"",
      "debug":false
   }
}
```

# Build Theme

```ts
export async function buildThemeCSS(config: ThemeCssConfig): Promise<void> {
 node_modulesPath = config.nodeModulesPath || 'node_modules';
 config = fixConfig(config);
 ...
 }
```

- `fixConfig` funciton

```ts
function fixConfig(config: ThemeCssConfig): ThemeCssConfig {
  let styleSourceRoot = 'src';
  // Now we know that name represents the name of the project in angular.json
  // But we didn't pass in
  if (config.name) {
    const angularJsonPath = join(root, 'angular.json');
    const sourceRoot = getJSON(angularJsonPath)?.projects[config.name!].sourceRoot;
    if (sourceRoot != null) {
      styleSourceRoot = sourceRoot;
    }
  }
  ...
}
```

- The following is a sample file of angular.json

```json
{
  "$schema": "./node_modules/@angular/cli/lib/config/schema.json",
  "version": 1,
  "newProjectRoot": "projects",
  "projects": {
    "pc": {
      "projectType": "application",
      "schematics": {
        "@schematics/angular:component": {
          "skipTests": false,
          "flat": false,
          "inlineStyle": true,
          "inlineTemplate": false,
          "style": "less"
        },
        "ng-yunzai:module": {
          "routing": true
        },
        "ng-yunzai:list": {
          "skipTests": false
        },
        "ng-yunzai:edit": {
          "skipTests": false,
          "modal": true
        },
        "ng-yunzai:view": {
          "skipTests": false,
          "modal": true
        },
        "ng-yunzai:curd": {
          "skipTests": false
        },
        "@schematics/angular:module": {
          "routing": true
        },
        "@schematics/angular:directive": {
          "skipTests": false
        },
        "@schematics/angular:service": {
          "skipTests": false
        }
      },
      "root": "",
      "sourceRoot": "src",
      "prefix": "app",
      "architect": {
        "build": {
          "builder": "@angular-devkit/build-angular:application",
          "options": {
            "outputPath": "../../src/main/resources/static/pc",
            "index": "src/index.html",
            "browser": "src/main.ts",
            "polyfills": [
              "zone.js"
            ],
            "tsConfig": "tsconfig.app.json",
            "inlineStyleLanguage": "less",
            "assets": [
              "src/favicon.ico",
              "src/assets"
            ],
            "styles": [
              "src/styles.less",
              "node_modules/prismjs/themes/prism-okaidia.css",
              "node_modules/prismjs/plugins/line-numbers/prism-line-numbers.css",
              "node_modules/prismjs/plugins/line-highlight/prism-line-highlight.css",
              "node_modules/prismjs/plugins/command-line/prism-command-line.css",
              "node_modules/katex/dist/katex.min.css"
            ],
            "scripts": [
              "node_modules/prismjs/prism.js",
              "node_modules/prismjs/components/prism-markdown.js",
              "node_modules/prismjs/components/prism-markup.js",
              "node_modules/prismjs/components/prism-less.js",
              "node_modules/prismjs/components/prism-css.js",
              "node_modules/prismjs/components/prism-json.js",
              "node_modules/prismjs/components/prism-java.js",
              "node_modules/prismjs/components/prism-javascript.js",
              "node_modules/prismjs/components/prism-typescript.js",
              "node_modules/prismjs/plugins/line-numbers/prism-line-numbers.js",
              "node_modules/prismjs/plugins/line-highlight/prism-line-highlight.js",
              "node_modules/prismjs/plugins/command-line/prism-command-line.js",
              "node_modules/emoji-toolkit/lib/js/joypixels.min.js",
              "node_modules/katex/dist/katex.min.js",
              "node_modules/katex/dist/contrib/auto-render.min.js",
              "node_modules/mermaid/dist/mermaid.min.js",
              "node_modules/clipboard/dist/clipboard.min.js"
            ],
            "allowedCommonJsDependencies": [
              "ajv",
              "ajv-formats",
              "extend",
              "file-saver",
              "mockjs"
            ],
            "stylePreprocessorOptions": {
              "includePaths": [
                "node_modules/"
              ]
            }
          },
          "configurations": {
            "production": {
              "budgets": [
                {
                  "type": "initial",
                  "maximumWarning": "20mb",
                  "maximumError": "30mb"
                },
                {
                  "type": "anyComponentStyle",
                  "maximumWarning": "20kb",
                  "maximumError": "40kb"
                }
              ],
              "outputHashing": "all",
              "fileReplacements": [
                {
                  "replace": "src/environments/environment.ts",
                  "with": "src/environments/environment.prod.ts"
                }
              ]
            },
            "development": {
              "optimization": false,
              "extractLicenses": false,
              "sourceMap": true
            }
          },
          "defaultConfiguration": "production"
        },
        "serve": {
          "builder": "@angular-devkit/build-angular:dev-server",
          "configurations": {
            "production": {
              "buildTarget": "pc:build:production"
            },
            "development": {
              "buildTarget": "pc:build:development"
            }
          },
          "defaultConfiguration": "development",
          "options": {
            "proxyConfig": "proxy.conf.js"
          }
        },
        "extract-i18n": {
          "builder": "@angular-devkit/build-angular:extract-i18n",
          "options": {
            "buildTarget": "pc:build"
          }
        },
        "test": {
          "builder": "@angular-devkit/build-angular:karma",
          "options": {
            "polyfills": [
              "zone.js",
              "zone.js/testing"
            ],
            "tsConfig": "tsconfig.spec.json",
            "inlineStyleLanguage": "less",
            "assets": [
              "src/favicon.ico",
              "src/assets"
            ],
            "styles": [
              "src/styles.less"
            ],
            "scripts": []
          }
        },
        "lint": {
          "builder": "@angular-eslint/builder:lint",
          "options": {
            "lintFilePatterns": [
              "src/**/*.ts",
              "src/**/*.html"
            ]
          }
        }
      }
    }
  },
  "cli": {
    "schematicCollections": [
      "@schematics/angular",
      "ng-yunzai"
    ]
  }
}
```

- Various operations in the first half of this function are to determine the source directory of the project

```ts
config = deepMergeKey(
    {
      additionalLibraries: [],
      additionalThemeVars: [],
      list: [],
      min: true,
      projectStylePath: mergePath(styleSourceRoot, 'styles.less'),
    } as ThemeCssConfig,
    true,
    config,
  );
```

- By merging objects, add to config `projectStylePath` value is `src/style.less`
    
- Now `config` becomes
    

```json
{
   "theme":{
      "list":[
         {
            "theme":"dark"
         },
         {
            "theme":"compact"
         },
         {
            "theme":"yuhong",
            "modifyVars":{...}
         }
      ],
      "name":"",
      "debug":false,
      "additionalLibraries": [],
      "additionalThemeVars": [],
      "list": [],
      "min": true,
      "projectStylePath":  'src/styles.less'
   },
   "colorLess":{
      "name":"",
      "debug":false
   }
}
```

go on

```ts
  const list: ThemeCssItem[] = [];
  config.list!.forEach(item => {
    if (!item.theme && !item.modifyVars) {
      return;
    }
    if (!item.key) {
      item.key = item.theme || 'invalid-key';
    }
    if (!item.filePath) {
      item.filePath = mergePath(styleSourceRoot, `assets/style.${item.key || 'invalid-name'}.css`);
    }
    list.push({ projectThemeVar: [], ...item });
  });
```

- This code traverses the list configuration under the theme and adds the filePath attribute
    
- Now config becomes
    

```json
{
   "theme":{
      "list":[
         {
            "theme":"dark",
            "filePath":"src/assets/style.dark.css",
            "projectThemeVar":[]
         },
         {
            "theme":"compact",
            "filePath":"src/assets/style.compact.css",
            "projectThemeVar":[]
         },
         {
            "theme":"yuhong",
            "modifyVars":{...},
            "filePath":"src/assets/style.yuhong.css",
            "projectThemeVar":[]
         }
      ],
      "name":"",
      "debug":false,
      "additionalLibraries": [],
      "additionalThemeVars": [],
      "list": [],
      "min": true,
      "projectStylePath":  'src/styles.less'
   },
   "colorLess":{
      "name":"",
      "debug":false
   }
}
```

- go back to `buildThemeCss`

```ts
export async function buildThemeCSS(config: ThemeCssConfig): Promise<void> {
  node_modulesPath = config.nodeModulesPath || 'node_modules';
  config = fixConfig(config);

  const promises = config.list?.map(item => {})
  await Promise.all(promises!);
```

- Start looping the list, and finally execute the Promise function together
- What is in the loop body is the core css generation logic
