
This guide will help you package a Vue.js project using Electron Forge. This guide works for students using VS Code's terminal on both Windows and macOS.

## Prerequisites

### 1. **Install Node.js (Portable Method)**

Since students don’t have Node.js installed, they can use a portable version:
- **Windows**: Download the **Node.js ZIP** from [Node.js official site](https://nodejs.org/en/download) and extract it.
- **macOS**: Install Node.js using [Homebrew](https://brew.sh/) with:
  ```bash
  brew install node
  ```

Once installed, open **VS Code**, launch the **terminal**, and verify Node.js installation by typing the following:
```bash
node -v
npm -v
```

### 2. **Initialize an Electron Forge Project**

1. Initialize the project by typing:
   
   ```bash
   npm init -y
   npm install --save-dev @electron-forge/cli
   npx electron-forge import
   ```
2. Open your package.json file find the "description" field and add a description like the example below:
```json
  "description": "A simple app built with Vue.js and Electron.",
```



### 3. **Create the Electron Entry File**
In the project folder, create a new file called electron.js and copy the following code:
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


### 4. **Run and Test the App**

To start the app in development mode:
```bash
npm start
```

### 7. **Package the App**

To create an installer:
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

