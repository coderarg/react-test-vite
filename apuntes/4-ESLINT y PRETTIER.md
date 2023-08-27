## ESLINT Y PRETTIER
### ESLINT
Este es un corrector automático que detecta errores en los archivos, cómo por ejemplo, variables que no se usan, espacios demás en arrays, etc.
Nos fuerza a utilizar el mismo estilo de código.

### Instalación

```shell
npm i -D eslint

npm init @eslint/config

npx eslint src/main.jsx ## Muestra los errores

npx eslint src/main.jsx --fix ## Corrige los errores
```

Para que Visual Studio Code nos muestre los errores a través de Eslint, vamos a descargar e instalar el plugin de ESLint.  
[ESLint pluggin](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)


### PRETTIER (FORMATEADOR)
Vamos a instalar un formateador ya que este es configurable para todo el proyecto. Nos permite trabajar en equipo, contando todos con el mismo formato.

```shell
npm i -D prettier

npx prettier src/main.jsx

npx prettier src/main.jsx --write ##Para que modifique
```

Para configurar prettier y que no tenga problemas con Eslint, vamos a realizar la configuración del mismo.  
Para ello vamos a crear un archivo .prettierrc en la carpeta base y, teniendo en cuenta la documentación de Prettier, vamos a ajustar lo que queramos.  

[Prettier Docs](https://prettier.io/docs/en/options)

Cuando hayamos finalizado podemos descargar e instalar el plugin de Prettier - Code formatter

[Prettier Plugin](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)


En caso que tengamos contradicciones entre la configuración de Eslint y Prettier, deberemos descargar el paquete siguiente

```shell
npm i -D eslint-config-prettier
```

en el archivo de .eslintrc.cjs vamos a agregar una linea de configuración dentro de 
```json
"extends":{
  'eslint-config-prettier'
}   
```

De esta manera, cada vez que haya una confusión entre prettier y eslint, se queda con la configuración de prettier.

Deberemos realizar un .prettierignore y un .eslintignore para ignorar carpetas que no queremos formatear, por ejemplo la carpeta dist que cuenta con la app para producción.  

### .prettierignore
```
dist
package-lock.json
apuntes
```

### .eslintignore
```
dist
```

En la configuración de .eslintrc.cjs deberemos agregar la configuración de "settings" debajo de env quedando así:

```javascript
module.exports = {
  env: {
    browser: true,
    es2021: true,
  },
  settings: { //Configuración agregada
    react: {
      version: 'detect'
    }
  },
  extends: [
    'standard',
    'plugin:react/jsx-runtime',
    'plugin:react/recommended',
    'eslint-config-prettier',
  ],
  overrides: [
    {
      env: {
        node: true,
      },
      files: ['.eslintrc.{js,cjs}'],
      parserOptions: {
        sourceType: 'script',
      },
    },
  ],
  parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module',
  },
  plugins: ['react'],
  rules: {},
}

```