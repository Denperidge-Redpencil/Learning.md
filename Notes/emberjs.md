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

## Commands

```sh
npm install -g ember-cli  # Install Ember-cli

ember new $projectname --no-welcome --embroider  # New project with embroider enabled

# Run Ember project
ember server  
ember s


```

## Install & use a CSS framework through NPM & PostCSS
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