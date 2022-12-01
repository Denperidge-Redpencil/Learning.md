# Ember.js

Some commands & principles I've learned from the [Rock And Roll with Ember Octane](https://balinterdi.com/rock-and-roll-with-emberjs/) that I might want to have in an overview!

## Design principles
### The rule of Least Power
For Ember, (I think) it boils down to this:
- You should use the least powerful language to fix problems
- No JavaScript in templating/handlebars means that future updates will have minimal breaking changes

Also see 11:30 in this [Emberweekend episode](https://emberweekend.com/episodes/the-rule-of-least-power/) and the [W3C piece on it](https://www.w3.org/2001/tag/doc/leastPower.html).

### Handlebars' fail-softness
undefined/null properties get ignored in Handlebars. This gives cleaner output and less conditional code, but is something to keep in mind when debugging.

### Routing & outlet
- Everything gets routed through the application.hbs, useful for:
    - Setting the language
    - Fetching data to render a common layout
    - Basically to define structure & common markup across your application
- Subroutes render their content into the parent template {{outlet}}
- ```js
    this.route('bands'); == this.route('bands', { path: 'bands' }, function () {});
  ```
- `bands.band.songs` = full name. Entities in:
    - `app/routes/bands/band/songs.js`
    - `app/templates/bands/band/songs.hbs`
- The top-level route will be executed once, and by using `this.modelFor("modelname");` things can be passed down to the lower levels 

## Links
- Ember Inspector for [Chrome](https://chrome.google.com/webstore/detail/ember-inspector/bmdblncegkenkacieihfhpjfppoconhi) & [Firefox](https://addons.mozilla.org/en-US/firefox/addon/ember-inspector/)

## Commands

```sh
# Install Ember-cli
npm install -g ember-cli

# New project with embroider enabled
ember new $projectname --no-welcome --embroider

# Run Ember project
ember server  
ember s

# Generate route
ember generate route $routename
ember g route $routename

# Generate dynamic route
ember g route bands/band --path=':id'
```

## How-to

### Tracked property
"If a property is used in the template, it should be marked as tracked"
```js
import { tracked } from '@glimmer/tracking';

class Band {
    @tracked name;
    // ...
```

### Install & use a CSS framework through NPM & PostCSS
```sh
npm install -D ember-cli-postcss  # Allows using postcss
npm install -D $npm-css-framework
```

```js
// ember-cli-build.js
const EmberApp = require('ember-cli/lib/broccoli/ember-app');

module.exports = function (defaults) {
    let app = new EmberApp(defaults, {
        // ...
        postcssOptions: {
            compile: {
                plugins: [{ module: require('tailwindcss') }],
            },
        },
        // ...
    });
    // ...
}
// ...
```

```css
/* app/styles/app.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Thanks to [Rock And Roll with Ember Octane](https://balinterdi.com/rock-and-roll-with-emberjs/)