
# Step-by-step tutorial to package your app for distribution (so users can install it on their computers)




> **Electron is an open-source framework that lets you build desktop applications** using familiar web technologies like JavaScript and HTML.

> **Normally, creating apps for Windows, macOS, and Linux requires different programming languages and tools for each platform**—for example, C# with .NET for Windows, Swift or Objective-C for macOS, and C++ or Python for cross-platform development. However, **Electron simplifies this process by using the Chromium browser engine to build cross-platform apps from a single codebase**.

> **By following the step-by-step guide, you'll gain hands-on experience in configuring your development environment, integrating Vue.js with Electron, and preparing your application for deployment across various operating systems.**


### 1. **Install Node.js and Git**

> Typically, JavaScript only runs in web browsers. Node.js lets you run JavaScript outside of a web browser. This helps JavaScript work for building apps and more.

1. Install Node.js:
- **Windows**: Download the **Node.js ZIP** from [Node.js official site](https://nodejs.org/en/download), extract it, and install it following the installation wizard.
- **macOS**: Download the **Node.js pkg** from [Node.js official site](https://nodejs.org/en/download) and install it following the installation wizard.
 

2. Once installed, open **VS Code**, launch the **terminal**, and verify Node.js installation by typing each line of code below one at a time. If the terminal shows the version of node and npm, you can continue to the next step as it means the installation was successful.

```bash
node -v
npm -v
```
3. Install Git:
- **Windows**: Download **Standalone Installer** from [Git official site](https://git-scm.com/downloads/win), and install it following the installation wizard. When you reach the screen "Adjusting your PATH environment", select the option: "Git from the command line and also from 3rd-party software".
- **macOS**: Type ```git``` in the terminal, then click **install** in the prompt asking if you want to install Command Line Developer Tools.

4. Verify **Git** installed correctly by typing:

```bash
git --version
```


### 2. **Create the Electron Entry File**

> The Electron entry file is the starting point of your Electron app. It acts like the "main control center" that launches your application and manages its windows.

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

> Before building an Electron app, you need to set up the project so that Electron knows how to run it. Among other things, this process creates a **package.json** file, which acts like a guide for Electron, listing your app’s details and dependencies (i.e., libaries).


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

> Once your Electron project is set up, you need to launch it in development mode to test how it works: Electron reads your project setup, then it runs your entry file (i.e, main.js), and opens your app window, letting you see it in action!

To start the app in development mode type in the terminal:
```bash
npm start
```

### 5. **Package the App**

> Once you’ve finished developing your app you can package it for distribution, so users can install it on their computers.

1. Open another terminal in VS Code.
2. Generate installation files by typing the code below. This installation files will be saved inside the `out` directory:

```bash
npm run make
```

### 6. **Install and Test the Packaged App**

> After packaging your app in the previous step, you'll see a new folder called **out**. This folder contains your installable app. To run it, open the out folder in Finder, then launch your app.

- On **Windows**, double click the `.exe` file from `out` folder.
- On **macOS**, double click the `.app` file from `out` folder.

### 7. **Uninstall the App (If Needed)**

- **Windows:** Open `Control Panel > Programs > Uninstall a program` and remove it.
- **macOS:** Delete the `.app` file from `Applications`.

