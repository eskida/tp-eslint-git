# TP ESLint Git

## 1. Initialisation du projet et installation d'ESLint

### Instructions du sujet :
- `mkdir tp-eslint-git && cd tp-eslint-git`
- `git init`
- `npm init -y`
- `npm install eslint --save-dev`
- `npx eslint --init`
- `echo "node_modules/" >> .gitignore`
- `echo ".eslintcache" >> .gitignore`

### Ce que j'ai fait :
```
cd '/Users/mobileminute/Desktop/Bureau - MacBook Pro Dan/CoursESGIIABD/Outil et pratique du code'
mkdir tp-eslint-git && cd tp-eslint-git
git init
npm init -y
npm install eslint --save-dev
npx eslint --init
echo "node_modules/" >> .gitignore
echo ".eslintcache" >> .gitignore
```

## 2. Test d'ESLint sur un fichier JavaScript

### Instructions du sujet :
- Créer un fichier `app.js` contenant :
```
const x = 10;
console.log(x);
function test(){
  console.log('test')
}
test();
```
- Lancer ESLint : `npx eslint app.js`
- Corriger avec `npx eslint --fix app.js`

### Ce que j'ai fait :
```
npx eslint app.js
npx eslint --fix app.js
```

## 3. Intégration avec Git Hooks (Husky)

### Instructions du sujet :
- Installer Husky : `npm install husky --save-dev`
- Initialiser Husky : `npx husky install`
- Ajouter un hook pre-commit : `npx husky add .husky/pre-commit "npx eslint ."`
- Tester : 
  ```
  git add .
  git commit -m "Test du hook ESLint"
  ```

### Ce que j'ai fait :
```
npm install husky --save-dev
npx husky install    // Message: command is DEPRECATED
npx husky init
npx husky add .husky/pre-commit "npx eslint ."  // Message: command is DEPRECATED
git add .
git commit -m "Test du hook ESLint"
```

**Remarque :** Les commandes Husky ont affiché des avertissements de dépréciation et des erreurs (permissions, module non trouvé). J'ai résolu le problème en ajustant les permissions avec `chmod +x .husky/pre-commit` et en utilisant une commande alternative via le binaire.

## 4. Configuration avancée d'ESLint (Airbnb)

### Instructions du sujet :
- Modifier la config pour étendre `"airbnb-base"` et personnaliser les règles.
- Ajouter le script `"lint": "eslint ."` dans package.json.
- Tester avec `npm run lint`

### Ce que j'ai fait :
```
npm install --save-dev eslint-config-airbnb-base eslint-plugin-import
```

**Remarque :** La commande a généré un conflit de version, car `eslint-config-airbnb-base@15.0.0` exigeait ESLint compatible avec ^7.32.0 ou ^8.2.0. J'ai donc désinstallé ESLint 9 puis installé ESLint version 8 via :
```
npm uninstall eslint
npm install --save-dev "eslint@^8.2.0" eslint-config-airbnb-base eslint-plugin-import
```

## 5. Mise en place de GitHub Actions

### Instructions du sujet :
- Créer un dépôt GitHub et lier le remote.
- Créer un workflow CI dans `.github/workflows/lint.yml` avec :
  ```yaml
  name: Lint Code

  on: [push, pull_request]

  jobs:
    lint:
      runs-on: ubuntu-latest
      steps:
        - uses: actions/checkout@v3
        - uses: actions/setup-node@v3
          with:
            node-version: 18
        - run: npm ci
        - run: npm run lint
  ```
- Ajouter, committer et pousser :
  ```
  git add .github/workflows/lint.yml
  git commit -m "Ajout du workflow GitHub Actions pour le linting"
  git push
  ```

### Ce que j'ai fait :
```
mkdir -p .github/workflows
vim .github/workflows/lint.yml
git add .github/workflows/lint.yml
git commit -m "Ajout du workflow GitHub Actions pour le linting"
git push
```

**Remarque :** Le fichier a été correctement ajouté puis poussé sur GitHub.

## 6. Simulation d'un travail d'équipe

### Ce que j'ai fait :
- Créer une branche `feature/ajout-fonction` :
  ```
  git checkout -b feature/ajout-fonction
  ```
- Ajouter un fichier avec des erreurs (ex. `utils.js`) et tenter de commit :
  ```
  git add utils.js
  git commit -m "Code non conforme"
  ```
- Corriger avec `npx eslint --fix .` puis commit et pousser :
  ```
  npx eslint --fix .
  git add .
  git commit -m "Correction des erreurs ESLint"
  git push --set-upstream origin feature/ajout-fonction
  ```
