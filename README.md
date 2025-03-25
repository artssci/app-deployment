
This guide will help you package a Vue.js project using Electron Forge. This guide works for students using VS Code's terminal on both Windows and macOS.

## Prerequisites

### 1. **Install Node.js (Portable Method)**

Since students don’t have Node.js installed, they can use a portable version:
- **Windows**: Download the **Node.js ZIP** from [Node.js official site](https://nodejs.org/en/download) and extract it.
- **macOS**: Download the **Node.js pkg** from [Node.js official site](https://nodejs.org/en/download) and install it following the installation wizard.
 

Once installed, open **VS Code**, launch the **terminal**, and verify Node.js installation by typing the following:
```bash
node -v
npm -v
```
If the terminal shows the version of node and npm, you can continue to the next step as it means the installation was successful.

### 2. **Create the Electron Entry File**
In your project folder, create a new file called main.js and copy the following code.  Don't forget to save your changes:

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

### 3. **Initialize an Electron Forge Project**

1. In VS Code open your project folder
   
2. Open a new terminal in VS Code
   
3. Initialize the Electron project by typing the following lines of code, one at a time. Some of them will trigger some processes in the terminal. Wait until each process is done before typing the next line of code:
   
   ```bash
   npm init -y
   npm install --save-dev @electron-forge/cli
   npx electron-forge import
   ```
4. Open your package.json file find the "description" field and add a description like the example below. Don't forget to save your changes (File > Save):
   
```json
  "description": "A simple app built with Vue.js and SVG.",
```




### 4. **Run and Test the App**

To start the app in development mode type in the terminal:
```bash
npm start
```

### 5. **Package the App**

To create an installer type:
```bash
npm run make
```
This will generate installation files inside the `out` directory.

### 8. **Install and Test the Packaged App**

- On **Windows**, run the `.exe` file from `out/`.
- On **macOS**, run the `.app` file from `out/`.

### 9. **Uninstall the App (If Needed)**

- **Windows:** Open `Control Panel > Programs > Uninstall a program` and remove it.
- **macOS:** Delete the `.app` file from `Applications`.
- **Ubuntu/Linux:** Run:
  ```bash
  sudo apt remove your-app-name
  ```

---

This guide provides a structured process for packaging Vue.js apps with Electron Forge. Let me know if you need adjustments!

