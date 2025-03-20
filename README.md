
This guide will help you package a Vue.js project using Electron Forge. The Vue app consists of an `index.html` and `vue.js` file inside a folder. This guide works for students using VS Code's terminal on both Windows and macOS.

## Prerequisites

### 1. **Install Node.js (Portable Method)**

Since students don’t have Node.js installed, they can use a portable version:
- **Windows**: Download the **Node.js ZIP** from [Node.js official site](https://nodejs.org/en/download) and extract it.
- **macOS**: Install Node.js using [Homebrew](https://brew.sh/) with:
  ```bash
  brew install node
  ```

Once installed, open a new terminal and verify Node.js installation:
```bash
node -v
npm -v
```

### 2. **Initialize an Electron Forge Project**

1. Open **VS Code** and launch the **terminal**.
2. Navigate to the project folder:
   ```bash
   cd path/to/your/project
   ```
3. Initialize the project:
   ```bash
   npx create-electron-app my-electron-app --template=forge
   ```
   Replace `my-electron-app` with the desired project name.

### 3. **Add Vue.js Files to the Project**

1. Copy your `index.html` and `vue.js` file into the `src` folder of your Electron project.
2. Modify `index.html` to load inside the Electron window:
   ```html
   <script>
     const { ipcRenderer } = require('electron');
   </script>
   ```

### 4. **Modify `main.js` to Load the Vue App**

In `src/main.js`, modify the `BrowserWindow` configuration:
```javascript
const { app, BrowserWindow } = require('electron');
const path = require('path');

function createWindow() {
  const win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true
    },
    icon: path.join(__dirname, 'assets', 'appIcon.png') // Ensure the icon path is correct
  });
  win.loadFile('src/index.html');
}

app.whenReady().then(createWindow);
```

### 5. **Set Up Electron Forge Config for Packaging**

In `package.json`, add `config.packagerConfig`:
```json
"config": {
  "forge": {
    "packagerConfig": {
      "icon": "assets/appIcon"
    },
    "makers": [
      {
        "name": "@electron-forge/maker-squirrel",
        "config": {}
      },
      {
        "name": "@electron-forge/maker-zip",
        "platforms": ["darwin", "linux"]
      }
    ]
  }
}
```

### 6. **Run and Test the App**

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

