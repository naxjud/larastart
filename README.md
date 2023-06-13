<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

# First Step

npm install && composer update 


# VS-Code Settings

These are some things you need to do in VS-Code to make you programming journey enjoyable:

## Add ons for VSCode

- Auto Close Tag

- ES Lint

- Laravel Extra intellisense

- PHP intelphense

- php namespace resolver

- tailwins css inteliisense

- vue language features


## Short-Cuts

- **Strg-B**: show/Hide side Bar

- **Strg-ö**: show Terminal

- **Strg-Shift-ö**: open new Terminal

- **Strg-D**: Find and mark next

- **Strg-Shift-L**: Find and mark all occurences

- **Strg-click**: Open Definition



## Auto Format

to autoformat your code every time you save the file do the following

1. create a .vscode folder

2. create a settings.json file

3. put this inside

```json
{
  "json.schemaDownload.enable": true,
  "eslint.validate": [
    "javascript",
    "javascriptvue",
    "vue"
  ],
  "eslint.format.enable": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "workbench.colorTheme": "Default Dark+",
  "editor.fontFamily": "Cascadia Code",
  "editor.fontWeight": "400",
  "html.format.wrapAttributes": "force"
}
```

4. run this command

```bash
npm install -g eslint
```

5. Using Linter to make easier Paths
   - make a file `jsconfig.json` and put this inside
  ```javascript
    {
    "compilerOptions": {
      "baseUrl": ".",
      "paths": {
        "@/*": [
          "resources/js/*"
        ]
      },
      "jsx": "preserve",
    },
    "exclude": [
      "node_modules",
      "public"
    ]
  }
  ```
  - install eslint as a dev depency
  
    ```npm install --save-dev eslint eslint-plugin-vue```

  - create a file `.eslintrc.js` and put this inside
  ```javascript
  module.exports = {
  extends: ['eslint:recommended', 'plugin:vue/vue3-recommended'],
  parserOptions: {
    ecmaVersion: 2020,
    sourceType: 'module',
  },
  env: {
    amd: true,
    browser: true,
    es6: true,
  },
  rules: {
    indent: ['error', 2],
    quotes: ['warn', 'single'],
    semi: ['warn', 'never'],
    'no-unused-vars': ['error', { vars: 'all', args: 'after-used', ignoreRestSiblings: true }],
    'comma-dangle': ['warn', 'always-multiline'],
    'vue/multi-word-component-names': 'off',
    'vue/max-attributes-per-line': 'off',
    'vue/no-v-html': 'off',
    'vue/require-default-prop': 'off',
    'vue/singleline-html-element-content-newline': 'off',
    'vue/html-self-closing': [
      'warn',
      {
        html: {
          void: 'always',
          normal: 'always',
          component: 'always',
        },
      },
    ],
    'vue/no-v-text-v-html-on-component': 'off',
  },
}
  ```
# What to Install

## 1. PHP
1. download the last php version (non thread save [zip](https://windows.php.net/download#php-8.2))
2. extract the zip to c:\php8
3. add the php to the path environment variable (move it to the top)
4. check php is ready: `$php -v`

## 2. Composer
1. download the last [Composer](https://getcomposer.org/download/) version 
2. install it
3. check it's installed: `$composer about`

## 3. Nodejs
1. download the last LTS version from [Nodejs.org](Nodejs.org)
2. install it
3. check it's installed: `$composer about`

## 4. Docker
1. download the last Docker version from [Docker](docker.com)
2. install and restart
3. if asked to install WSL 2 do that

# Start a Project
## create a new laravel project
- create a new laravel project
```bash
composer create-project laravel/laravel example-app
cd example-app
# to start the server
php artisan serve
```

## Add vue and vite to the project
- vite is a tool to manage all frontend related tasks
- it packages all frontend assets to optimized files for production very fast

1. install vue and vite:
```bash
npm install --save-dev vue @vitejs/plugin-vue
```

1. open the folder in vscode

```
code .
```

3. open `package.json` and `vite.config.js`

package.json has all the project dependencies you need to install

edit `vite.config.js`
```javascript
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
import vue from '@vitejs/plugin-vue';

export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
        vue({
            template: {
                base: null,
                includeAbsolute: false
            }
        })
    ],
});
```

4. always run this command to run vite 
```bash
npm run dev
```
dev is defined in the `package.json` file

## Configure inertia for the project

1. set up the [server side](https://inertiajs.com/server-side-setup)
```bash
composer require inertiajs/inertia-laravel
```

2. rename `welcome.blade.php` to `app.blade.php` because inertia needs that
3. put this inside the `app.blade.php` 
   ```html
   <!DOCTYPE html>
    <html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">

        <title>Muslimseiten</title>

        @vite('resources/js/app.js')
        @inertiaHead
    </head>
    <body>
        @inertia
    </body>
</html>
   ```

4. set up the [client side vue3](https://inertiajs.com/client-side-setup)
```bash
npm install @inertiajs/vue3
```

5. put this code inside `resources/js/app.js` and remove the `bootstrap.js`
   ```javascript
    import { createApp, h } from 'vue'
    import { createInertiaApp } from '@inertiajs/vue3'

    createInertiaApp({
      resolve: name => {
        const pages = import.meta.glob('./Pages/**/*.vue', { eager: true })
        return pages[`./Pages/${name}.vue`]
      },
      setup({ el, App, props, plugin }) {
        createApp({ render: () => h(App, props) })
          .use(plugin)
          .mount(el)
      },
    })
   ```

## Tailwind CSS [instruction](https://tailwindcss.com/docs/guides/vite)
  1. install tailwind in your project
   
      - `npm install -D tailwindcss postcss autoprefixer`

  2. initialize the tailwind config file (tailwind.config.js and postcss.config.js)
    
       - `npx tailwindcss init -p`

  3. run this to install a plugin for [tailwind-forms](https://github.com/tailwindlabs/tailwindcss-forms)
      - `npm install -D @tailwindcss/forms`

  4. put this inside your tailwind.config.js
   ```javascript
    /** @type {import('tailwindcss').Config} */
    export default {
      content: [
        './storage/framework/views/*.php',
        './resources/views/**/*.blade.php',
        './resources/js/**/*.vue',

      ],
      theme: {
        extend: {},
      },
      plugins: [
        require('@tailwindcss/forms')
      ],
    }
   ```
  5. put this inside your resources/app.css

    ```css
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
    ````
  6. import the app.css file in your app.js file
   `import '../css/app.css'`


# Basics
## Routing
- A route looks like this
```php
  Route::get('/',[YourController::class, 'yourFunction']);
```
to show all the routes in your App 
- `php artisan route:list`

## Controller
to create a new Controller 

  - `php artisan make:controller IndexController`

## Vue Components
- are in the Resources/js 
- to render them use `return inertia('PageName')`
- a component has a template section and a script section
- example Component
  ```javascript
    <template>
      <div>
          Hello {{ variable }}
      </div>
    </template>

    <script setup>

        const variable= 'Test'

    </script>
  
  ```
- you can add a link with
  ```javascript
  import {Link} from '@inertiajs/vue3'
  ```
  and then use `<Link :href="/">Main Page</Link>` in the template