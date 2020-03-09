# templ.electron

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).


### Debugging in VSCode

https://github.com/nklayman/vue-cli-plugin-electron-builder/issues/80

#### .vscode/launch.json
```json
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Electron: Main",
      "type": "node",
      "request": "launch",
      "protocol": "inspector",
      "runtimeExecutable": "${workspaceRoot}/node_modules/.bin/electron",
      "windows": {
        "runtimeExecutable": "${workspaceRoot}/node_modules/.bin/electron.cmd"
      },
      "preLaunchTask": "electron-debug",
      "args": [
        "--remote-debugging-port=9223",
        "./dist_electron"
      ],
      "outFiles": [
        "${workspaceFolder}/dist_electron/**/*.js"
      ]
    },
    {
      "name": "Electron: Renderer",
      "type": "chrome",
      "request": "attach",
      "port": 9223,
      "urlFilter": "http://localhost:*",
      "timeout": 30000,
      "webRoot": "${workspaceFolder}",
      "sourceMapPathOverrides": {
        "webpack:///./*": "${webRoot}/*"
      }
    }
  ],
  "compounds": [
    {
      "name": "Electron: All",
      "configurations": [
        "Electron: Main",
        "Electron: Renderer"
      ]
    }
  ]
}
```

#### .vscode/tasks.json
```json
{
  // See https://go.microsoft.com/fwlink/?LinkId=733558
  // for the documentation about the tasks.json format
  "version": "2.0.0",
  "tasks": [
      {
          "label": "electron-debug",
          "type": "process",
          "command": "./node_modules/.bin/vue-cli-service",
          "windows": {
              "command": "./node_modules/.bin/vue-cli-service.cmd"
          },
          "isBackground": true,
          "args": [
              "electron:serve",
              "--debug"
          ],
          "problemMatcher": {
              "owner": "custom",
              "pattern": {
                  "regexp": ""
              },
              "background": {
                  "beginsPattern": "Starting development server\\.\\.\\.",
                  "endsPattern": "Not launching electron as debug argument was passed\\."
              }
          }
      }
  ]
}
```
