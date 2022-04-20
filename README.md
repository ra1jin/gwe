
![Drag Racing](https://img.shields.io/badge/lang-javascript-f39f37) ![Drag Racing](https://img.shields.io/badge/npm-v0.0.4-blue) ![Drag Racing](https://img.shields.io/badge/release-v0.0.4-blue) ![Drag Racing](https://img.shields.io/badge/dependencies-electron-brightgreen) 

Copyright © 2020-2022 [Raijin].

Nombreux sont les **développeurs web** qui souhaite créer leurs propre **jeu vidéo**, c'est maintenant possible grâce à **WGE**, un **moteur de jeu 2D/3D** basé sur les technologies du **web**.  
Pas besoin d'apprendre un nouvelle technologies, si vous maitrisez **HTML/JS/CSS** alors ce moteur est fait pour vous.

De plus, grâce à son projet de démarrage, ce moteur intègre tout le nécessaire pour commencer à développer un jeu vidéo avec un **minimum d'efforts**.

## Installation
Tout d'abord, vérifier que Node.js est bien installé sur votre environnement.  
Si c'est le cas, installer cette librairie dans votre projet avec la commande suivante : ```npm install --save gwe```

## Commencer
Voici le minimum requis pour commencer à travailler avec gwe.  
Commencer par créer un projet avec l'arborescence suivante.
```
├── assets
    ├──
├── src
│   ├── app.js
│   ├── main_screen.js
├── index.html
├── main.js
```

### main.js (electron)
```js
const { app, BrowserWindow } = require('electron');

app.whenReady().then(() => {
 createWindow()
});

function createWindow() {
  const win = new BrowserWindow({
    width: 800,
    height: 600, // +26 for window frame
    resizable: false,
    frame: false,
    webPreferences: {
      nodeIntegration: true,
      contextIsolation: false,
    }
  });

  win.setMenuBarVisibility(false)
  win.loadFile('index.html');
  win.openDevTools();
}
```

### index.html
```html
<!DOCTYPE html>
<html lang="fr">
  <head>
    <link rel="stylesheet" type="text/css" href="node_modules/gwe/core.css" />
    <script rel="preload" type="text/javascript" src="src/app.js"></script>
  </head>
  <body style="position:relative">
    <div id="APP">
      <canvas id="CANVAS" width="1px" height="1px"></canvas>
      <div id="UI_ROOT"></div>
      <div id="UI_FADELAYER"></div>
      <div id="UI_OVERLAYER"></div>
    </div>
  </body>
</html>
```

### src/app.js
```js
window.addEventListener('load', async () => {
  let { GWE } = require('gwe');
  let app = new GWE.Application(800, 800, GWE.SizeModeEnum.FIXED);
  requestAnimationFrame(ts => app.run(ts));
});
```

### src/main_screen.js
```js
let { GWE } = require('gwe');

class MainScreen  extends  GWE.Screen {
  constructor(app) {
    super(app);
  }

  onEnter() {
    // votre code d'initialisation doit être ici.
  }

  onExit() {
    // votre code de destruction doit être ici.
  }
	
  update(ts) {
    // votre code logique de mise à jour.
  }

  draw(viewIndex) {
    // votre code de dessin.
  }
}

module.exports.MainScreen = MainScreen;
```

Dans le fichier **app.js** ajouter l'écran au gestionnaire d'écran afin que celui-ci soit exécuté via la ligne suivante ```GWE.screenManager.requestSetScreen(new  MainScreen(app));```.  

## Documentation
Une documentation complète est disponible ici: https://ra1jin.github.io/gwe-doc/.

## Exemples
- [Boilerplate](https://github.com/ra1jin/gwe-boilerplate)
- [RolePlayingGame2000](https://github.com/ra1jin/gwe-boilerplate)

## Comment intégrer vos modèles 3D ?
L'extension Blender [blender-gwe-exporter](https://github.com/ra1jin/blender-gwe-exporter) vous permet d'exporter vos modèles statiques et animés dans les formats compatible GWE !