WIP: -DRAFT VERSION-

# How to override existing TypeScript with custom theme

You can download a theme showcasing the topic [here](/products/editions/enterprise-edition/b2b-suite/example-plugins/B2bOverrideTsPlugin.zip).

## Table of contents

* [Description](#description)
* [Setting the theme to compile ts](#setting-the-theme-to-compile-ts)
* [Extending an existing b2b plugin](#extending-an-existing-b2b-plugin)
* [Override the b2b plugin](#override-the-b2b-plugin)

## Description

This guide will go through the details on a way to extend and override b2b-suite typescript plugins.
Before learn how to extend a b2b plugin, we strongly recommend to read the shopware 6 storefront extension documentation 
https://developer.shopware.com/docs/guides/plugins/plugins/storefront/override-existing-javascript as we will only point 
out the specifications for extending b2b plugins in particular, assuming previous knowledge on how to do it for a
shopware 6 javascript plugin.

## Setting the theme to compile ts

You can create a new theme according to https://developer.shopware.com/docs/guides/plugins/themes/create-a-theme. 
Then, the default build process it's not configured to compile your typescript code, or the typescript you may want to import. 
Therefore, additional webpack configuration should be set according your needs. This should include the rule with a 
typescript loader, and the aliases you may need to ease the imports.

Here you can see an example '<PluginName>/src/Resources/app/storefront/build/webpack.config.js':
```typescript
const path = require('path');

module.exports = () => {
    return {
        module: {
            rules: [
                {
                    test: /\.tsx?$/,
                    use: [{
                        loader: path.resolve(__dirname, '..', 'node_modules', 'ts-loader')
                    }],
                    exclude: /node_modules/,
                },
            ],
        },
        resolve: {
            alias: {
                '@b2b': path.resolve(__dirname, './../../../../../../SwagB2bPlatform/SwagB2bPlatform/Resources/app/storefront/src/js'),
                apexcharts: path.resolve(__dirname, './../../../../../../SwagB2bPlatform/SwagB2bPlatform/Resources/app/storefront/node_modules/apexcharts')
            },
            extensions: [ '.ts', '.tsx', '.js', '.jsx', '.json', '.less', '.sass', '.scss', '.twig' ]
        }
    };
};
```

Additionally, it may be required to add some custom typescript compiler configuration. 
Here an example '<PluginName>/src/Resources/app/storefront/tsconfig.json'
```json
{
  "compilerOptions": {
    "sourceMap": true,
    "removeComments": true,
    "target": "es5",
    "module": "es6",
    "moduleResolution": "node",
    "allowJs": true,
    "noEmit": false,
    "esModuleInterop": true,
    "strict": false,
    "experimentalDecorators": true,
    "lib": ["es2017", "dom"],
    "types": ["node"]
  }
}
```

In order to have webpack, its loaders and typescript modules available, a package.json should be added and the modules 
installed via 'npm install' beforehand. 
Please note loader versions need to be fixed to support webpack 4 while the shopware 6 storefront its based on it.

Here an example '<PluginName>/src/Resources/app/storefront/package.json'
```json
{
    "name": "example-theme",
        "version": "1.0.0",
        "description": "Example theme",
        "main": "main.js",
        "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
    },
    "author": "shopware AG",
        "license": "MIT",
        "devDependencies": {
        "@types/node": "^18.6.1",
        "ts-loader": "8.1.0",
        "typescript": "^4.7.4",
        "webpack": "4.38.0"
    }
}
```

## Extending an existing b2b plugin

In your own typescript code, you could extend then the b2b plugins using the previously configured alias for the import.

Here and example '<PluginName>/src/Resources/app/storefront/src/plugins/my-modal.ts':
```typescript
import AjaxPanelModalPlugin from '@b2b/plugins/ajax-panel-modal.plugin';

export default class MyModal extends AjaxPanelModalPlugin {
    public init() {
        console.log('Nope.');
    }

    protected someMethod(event: MouseEvent): void {
        console.log(event);
    }
}
```

## Override the b2b plugin

To override the b2b plugin, you could use the same patterns as for platform

....mmmm, well, not that easy......still to be decided/continued ;)