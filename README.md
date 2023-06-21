# Zora

### Add your Laravel language translations to your asset pipeline for use in Javascript packages like Vue or React.

### Requires Laravel > 8, 9\* compatible.

## Installation
Install the package via composer:
``` bash
composer require jetstreamlabs/zora --dev
```

It requires 2 aliases in vite config (vite.config.js):

zora: resolve(__dirname, 'vendor/jetstreamlabs/zora/dist/vue.js'),
'zora-js': resolve(__dirname, 'vendor/jetstreamlabs/zora/dist/index.js'),

```js
resolve: {
    alias: {
        ...
        zora: resolve(__dirname, 'vendor/jetstreamlabs/zora/dist/vue.js'),
        'zora-js': resolve(__dirname, 'vendor/jetstreamlabs/zora/dist/index.js'),
    },
},
```

Compile the translations to resources/js in your dev and build steps in package.json:
``` bash
"build:assets": "php artisan zora:generate",
```

OR

You can directly run the following artisan command. This has to run whenever you change translations in vue file.
``` bash
php artisan zora:generate
```

### VueJS
Import zora and your compiled translations in app.js or wherever you implement your Inertia setup:

```js
import { ZoraVue } from 'zora'
import { Zora } from '../zora.js'
```

Then use it in your app (register Zora plugin):
```js
...
.use(ZoraVue, Zora)
```

## Usage
Then in your Vue components you can use {{ __('Dashboard') }} or {{ trans('app.whatever') }}
```js
__(key: string, replacers: array)

//or

trans(key: string, replacers: array)
```

## Final Setup

Add following code to your app.blade.php so that lib trans function will catch current locale.

```js
<script>
        window.locale = '{{ app()->getLocale() }}';
</script>
```