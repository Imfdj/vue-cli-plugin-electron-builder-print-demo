# vue-cli-plugin-electron-builder-print-demo

<h3 align="center">
    <a href="https://github.com/Imfdj/electron-vue-printer">electron-vue-printer</a> 打印图片插件。简单的demo。
    <a href="https://github.com/Imfdj/electron-vue-printer">electron-vue-printer</a> print picture plugin. Simple demo。
</h3>
<h5 align="center">
    Based on <a href="https://github.com/nklayman/vue-cli-plugin-electron-builder">vue-cli-plugin-electron-builder</a>.
</h5>

### Hint
```
  background.js -->
  
  win = new BrowserWindow({
    width: 1920,
    height: 1080,
    webPreferences: {
      // Use pluginOptions.nodeIntegration, leave this alone
      // See nklayman.github.io/vue-cli-plugin-electron-builder/guide/security.html#node-integration for more info
      // nodeIntegration: process.env.ELECTRON_NODE_INTEGRATION
      nodeIntegration: true, // ！！！
      webviewTag: true // ！！！
    }
  })
```

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn electron:serve
```

### Compiles and minifies for production
```
yarn electron:build
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
