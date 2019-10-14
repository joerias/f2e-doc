## 前言

可通用的 vsCode 的代码格式化工具，新项目 eslint 严格模式（目前医全通后台）必须配置该项，不然会产生大量的手动修改的 eslint 细节修改  
"editor.fontFamily"和"editor.fontSize" 项不是必须的，请提前保留自己默认的项配置

```javascript
{
  // #每次保存的时候自动格式化
  "editor.formatOnSave": true,
  "workbench.startupEditor": "newUntitledFile",
  "editor.wordWrap": "on",
  "workbench.editor.enablePreview": false,
  "editor.fontFamily": "Consolas,Sarasa Mono SC,'Microsoft Yahei', 'Courier New'",
  "git.enableSmartCommit": true,
  "breadcrumbs.enabled": true,
  "explorer.confirmDelete": false,
  "editor.wordSeparators": "`~!@#$%^&*()=+[{]}\\|;:'\",.<>/?",
  "files.autoSave": "onFocusChange",
  "window.zoomLevel": 0,
  "editor.tabSize": 2,
  "vetur.format.defaultFormatter.html": "js-beautify-html",
  "vetur.format.defaultFormatter.js": "prettier",
  "vetur.format.defaultFormatter.less": "prettier",
  "vetur.format.defaultFormatterOptions": {
    "js-beautify-html": {
      "wrap_attributes": "force" //属性强制折行对齐 Wrap all attributes, except first, and align attributes
    },
    "prettier": {
      "printWidth": 80,
      "singleQuote": true, // 使用单引号
      "semi": false, // 末尾使用分号
      "tabWidth": 2,
      "arrowParens": "avoid",
      "bracketSpacing": true,
      "proseWrap": "preserve" // 代码超出是否要换行 preserve保留
    }
  },
  "prettier.singleQuote": true,
  "prettier.semi": false,
  "markdown.preview.fontFamily": "Sarasa Mono SC",
  "editor.fontSize": 15,
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "explorer.confirmDragAndDrop": false,
  "terminal.integrated.fontSize": 12,
  "debug.console.fontSize": 12,
}
```
