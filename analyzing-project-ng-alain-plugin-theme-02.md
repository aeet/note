---
title: "Analyzing Project: ng-alain/plugin-theme - 02"
date: "2024-04-03"
categories: 
  - "code-learning"
  - "learn-open-source-project"
tags: 
  - "open-source"
  - "typescript"
coverImage: "2dbcf65f626f4e93b157b0aec18ffbb5.jpg"
---

```ts
const promises = config.list?.map(item => {
    const modifyVars = genVar(config, item);

    ...
}
```

- call `genVar` function

```ts
function genVar(config: ThemeCssConfig, item: ThemeCssItem): { [key: string]: string } {
  const fileContent = item.projectThemeVar?.map(path => readFileSync(join(root, path), 'utf-8'))!;
  fileContent.push(readFileSync(join(root, config.projectStylePath!), 'utf-8'));
}
```

- Read the `style file` of `projectThemeVar`.
- Default was `src/style.less`.
- Note that what is read here is the `file content`.

```less
@import '@delon/theme/system/index';
@import '@delon/abc/index';
@import '@delon/chart/index';
@import '@delon/theme/layout-default/style/index';
@import '@delon/theme/layout-blank/style/index';
@import './styles/index';
@import './styles/theme';
```

```ts
let projectTheme: { [key: string]: string } = {};
if (fileContent) {
  projectTheme = lessToJs(fileContent.join(''), {
    stripPrefix: true,
    resolveVariables: false,
  });
}
```

- Key function `lessToJs`
- `lessToJs` is a function in the `less-vars-to-js` package.
- Through this entry less, all variables are turned into js.
    - stripPrefix: Removes the `@` or `$` in the returned object keys.
    - resolveVariables: Resolves variables when they are defined in the same file.

```
// this is a example
@prefix: 'theme';
@primary-color: #1890ff;
@secondary-color: #f5222d;
---
stripPrefix: true
resolveVariables: false
---
{
  'prefix': 'theme',
  'primary-color': '@primary-color',
  'secondary-color': '@secondary-color'
};
```

- There is now a less variable object in `projectTheme`
- Next line

```ts
const modifyVars = item.modifyVars || {};
```

- Get custom variables in json.

```json
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
```

```ts
const stripPrefixOfModifyVars: { [key: string]: string } = {};
Object.keys(modifyVars).forEach(key => {
    const newKey = key.startsWith('@') ? key.substr(1) : key;
    stripPrefixOfModifyVars[newKey] = modifyVars[key];
  });
```

- Remove `@` from each line of the variable list in json and save it to stripPrefixOfModifyVars

```ts
 const additionalThemeVars = config.additionalThemeVars!;
```

- Read additional variable list

```ts
 return {
    ...genThemeVars('default', additionalThemeVars),
    ...(item.theme === 'dark' ? genThemeVars('dark', additionalThemeVars) : null),
    ...(item.theme === 'compact' ? genThemeVars('compact', additionalThemeVars) : null),
    ...projectTheme,
    ...stripPrefixOfModifyVars,
  };
```

- Finally, an object of variable collection is returned, and the latter one overwrites the previous one.
    
- Before returning to the `buildThemeCss` function, we first enter `genThemeVars`.
    

```ts
 const contents: string[] = [];
  // ng-zorro-antd
  const ngZorroAntdStylePath = join(root, node_modulesPath, 'ng-zorro-antd', 'style');
  if (existsSync(ngZorroAntdStylePath)) {
    contents.push(readFileSync(join(ngZorroAntdStylePath, 'color', 'colors.less'), 'utf-8'));
    contents.push(readFileSync(join(ngZorroAntdStylePath, 'themes', `${type}.less`), 'utf-8'));
  }
```

- Get the color variables and entry less file content in the ng-zorro component library.

```ts
// @delon
  const delonPath = join(root, node_modulesPath, '@delon');
  // @delon/theme/system
  const delonSystem = join(delonPath, 'theme');
  if (existsSync(delonSystem)) {
    [
      join(delonSystem, 'system', `theme-${type}.less`),
      join(delonSystem, 'layout-default', 'style', `theme-${type}.less`),
      join(delonSystem, 'layout-blank', 'style', `theme-${type}.less`),
    ].forEach(filePath => {
      if (!existsSync(filePath)) {
        console.warn(`主题路径 ${filePath} 不存在`);
        return;
      }
      contents.push(readFileSync(filePath, 'utf-8'));
    });
  }
  ['abc', 'chart'].forEach(libName => {
    const libThemePath = join(delonPath, libName, `theme-${type}.less`);
    if (existsSync(libThemePath)) {
      contents.push(readFileSync(libThemePath, 'utf-8'));
    }
  });
```

- Get `all style` content in `@delon package.`

```ts
 // 外部样式 extraThemeVars
  if (Array.isArray(extraThemeVars) && extraThemeVars.length > 0) {
    contents.push(
      ...extraThemeVars.map(path => {
        // 自动处理 src/app/layout/name/styles/theme-#NAME#.less之类的
        const lessFilePath = join(root, path.replace(`#NAME#`, type));
        if (!existsSync(lessFilePath)) {
          return '';
        }
        return readFileSync(lessFilePath, 'utf-8');
      }),
    );
  }
```

- Handle additionalThemeVars styles passed in json.

```ts
 return lessToJs(contents.join(''), {
    stripPrefix: true,
    resolveVariables: false,
  });
```

- Finally use lessToJS to convert to JavaScript variables.
    
- Okay, now let's go back to the top level call.
    

```ts
const promises = config.list?.map(item => {
    const modifyVars = genVar(config, item);
...
}
```

- Now we have all the javascript variables ready for the style.

```ts
const options: BuildThemeCSSOptions = {
      min: config.min,
      content,
      modifyVars,
    };
    if (existsSync(item.filePath!)) {
      unlinkSync(item.filePath!);
    }
    return buildCss(options, config).then(css => {
      writeFileSync(item.filePath!, css);
      console.log(`✅ Style '${item.key}' generated successfully. Output: ${item.filePath!}`);
    });
```

- Construct CSS options, pass in the less entry file content of the entire project, and the variables we read, and finally call buildCSS.

```ts
async function buildCss(options: BuildThemeCSSOptions, config: ThemeCssConfig): Promise<string> {
  // eslint-disable-next-line @typescript-eslint/no-explicit-any
  const plugins: any[] = [];
  if (options.min === true) {
    plugins.push(new LessPluginCleanCSS({ advanced: true }));
  }
  return less
    .render(options.content, {
      javascriptEnabled: true,
      plugins,
      paths: ['node_modules/'],
      ...config.buildLessOptions,
      modifyVars: {
        ...options.modifyVars,
      },
    })
    .then(res => res.css);
}
```

- Here you can directly use the render function provided by less to generate css.
    
- The logic of the entire project ends here.
