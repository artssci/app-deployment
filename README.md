
> [!NOTE]  
> Electron is an open-source framework that lets you build desktop applications using familiar web technologies like JavaScript, HTML, and CSS. Normally, creating apps for Windows, macOS, and Linux requires different programming languages and tools for each platform—for example, C# with .NET for Windows, Swift or Objective-C for macOS, and C++ or Python for cross-platform development. However, Electron simplifies this process by combining the Chromium browser engine and Node.js runtime, allowing you to build cross-platform apps from a single codebase.

This guide will help you package a Vue.js project using Electron Forge. This guide works for students using VS Code's terminal on both Windows and macOS.

## Prerequisites

### 1. **Install Node.js (Portable Method)**

1. Install Node.js:
- **Windows**: Download the **Node.js ZIP** from [Node.js official site](https://nodejs.org/en/download) and extract it.
- **macOS**: Download the **Node.js pkg** from [Node.js official site](https://nodejs.org/en/download) and install it following the installation wizard.
 

2. Once installed, open **VS Code**, launch the **terminal**, and verify Node.js installation by typing each line of code below one at a time. If the terminal shows the version of node and npm, you can continue to the next step as it means the installation was successful.

```bash
node -v
npm -v
```

### 2. **Create the Electron Entry File**

1. Open your app's project folder in VS Code
2. Create a new file inside your project folder called **main.js** and copy the following code. Don't forget to save your changes:

```js
const { app, BrowserWindow } = require('electron');
const path = require('path');

function createWindow() {
  const win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true,
    },
  });

  win.loadFile('index.html');
}

app.whenReady().then(createWindow);

app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') {
    app.quit();
  }
});

app.on('activate', () => {
  if (BrowserWindow.getAllWindows().length === 0) {
    createWindow();
  }
});
```

### 3. **Initialize an Electron Project**


1. Open a new terminal in VS Code
   
2. Initialize the Electron project by typing the following lines of code, one at a time. Some of them will trigger some processes in the terminal. Wait until each process is done before typing the next line of code:
   
   ```bash
   npm init -y
   npm install --save-dev @electron-forge/cli
   npx electron-forge import
   ```
3. Open your package.json file find the "description" field and add a description like the example below. Don't forget to save your changes (File > Save):
   
```json
  "description": "A simple app built with Vue.js and SVG.",
```




### 4. **Run and Test the App**

To start the app in development mode type in the terminal:
```bash
npm start
```

### 5. **Package the App**

1. Open another terminal in VS Code.
2. Generate installation files by typing the code below. This installation files will be saved inside the `out` directory:

```bash
npm run make
```

### 8. **Install and Test the Packaged App**

- On **Windows**, run the `.exe` file from `out/`.
- On **macOS**, run the `.app` file from `out/`.

### 9. **Uninstall the App (If Needed)**

- **Windows:** Open `Control Panel > Programs > Uninstall a program` and remove it.
- **macOS:** Delete the `.app` file from `Applications`.

