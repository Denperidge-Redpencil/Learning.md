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

### Handlebars expressions

| Expression    | ...is a...     | Definition location |
| ------------- | -------------- | ------------------- |
| {{data}}      | Block variable | Nearest block       |
| {{this.data}} | Property       | Template's context  |
| {{@data}}     | Argument       | Call site           |

(See pages 772 of [Rock and Roll with Ember Octane](https://balinterdi.com/rock-and-roll-with-emberjs/))

### Routing & outlet
- Everything gets routed through the application.hbs, useful for:
    - Setting the language
    - Fetching data to render a common layout
    - Basically to define structure & common markup across your application
- Subroutes render their content into the parent template {{outlet}}, & the child routes also inherit their parents' model()
- ```js
    this.route('bands'); == this.route('bands', { path: 'bands' }, function () {});
  ```
- `bands.band.songs` = full name. Entities in:
    - `app/routes/bands/band/songs.js`
    - `app/templates/bands/band/songs.hbs`
- The top-level route will be executed once, and by using `this.modelFor("modelname");` things can be passed down to the lower levels 

### Components
- Mostly self contained so they can be moved across applications
- Call using `<CamelisedName>` to distinguish from html
- Previously used to only be called using {curly braces}

### Controllers
- The `@action` decorator (from `'@ember/object'`) is only needed if the function gets called from the template
- Controllers are singletons (single instances). If that gives any issues, use `resetController(controller) { /* reset values here */ }`



### Routes hook order
1. [`beforeModel(transition){}`](https://api.emberjs.comember/release/classes/Route/methods/?anchor=beforeModel)
2. [`model(params, transition){}`](https://api.emberjs.comember/release/classes/Route/methods/?anchor=model)
3. [`afterModel(model, transition){}`](https://api.emberjscom/ember/release/classes/Route/methods/?anchor=afterModel)
4. [`setupController(controller, model, transitions)`(https://api.emberjs.com/ember/release/classes/Route/methodsanchor=setupController)

Sequence example: application(beforeModel -> model ->afterModel) --> route(beforeModel --> model --> afterModel)--> subroute(beforeModel --> model --> afterModel) -->application(setupController) --> route(setupController) --> subroute(setupController)

## Commands

```sh
# Install Ember-cli
npm install -g ember-cli

# New project with embroider enabled
ember new $projectname --no-welcome --embroider

# Run Ember project
ember server  
ember s

# Common ember generators
ember generate {route,template,controller,service} $routename
ember g {route,template,controller,service} $routename

# Generate component...
ember g component $componentname  # ...hbs
ember g component $componentname --with-component-class  # ...hbs & .js

# Generate dynamic route
ember g route bands/band --path=':id'

# Destroy route (removes corresponding routes/, templates/, tests/)
ember destroy route $routename
```

## How-to

### Tracked property
- "If a property is used in the template, it should be marked as tracked"
- Getters (in components at least) are auto-tracked
- Make sure to track the deepest object:
    - `this.storage.bands.push()` --> `this.storage` doesn't get changed, so tracking that won't work; track `this.storage.bands` instead.
    - You might have to use `this.storage.bands = tracked([])`, which you can get after running and importing `ember i tracked-built-ins`

```js
import { tracked } from '@glimmer/tracking';

class Band {
    @tracked name;
    // ...
```

### LinkTo dynamic path/model
```handlebars
{{!-- LinkTo using a single dynamic segment --}}
<LinkTo @route="bands.band.songs" @model={{band.id}}>
    {{band.name}}
</LinkTo>

{{!-- LinkTo using multiple dynamic segments --}}
<LinkTo @route="bands.band.songs" @model={{array band1.id, band2.id}}>
    {{band.name}}
</LinkTo>
```

### Component with optional block
```handlebars
{{#if (has-block)}}
    {{yield this.data}}
{{else}}
    {{#each this.data as |data|}}
        <input type="text"
            placeholder={{data}}
        />
    {{/each}}
{{/if}}
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

### Router service
```js
import { inject as service } from '@ember/service';

export default class NewController extends Controller {
    @service router;

    @action
    save() {
        // ...
        this.router.transitionTo('models.model.property', model.id);
    }
}
```


## Links
- Ember Inspector for [Chrome](https://chrome.google.com/webstore/detail/ember-inspector/bmdblncegkenkacieihfhpjfppoconhi) & [Firefox](https://addons.mozilla.org/en-US/firefox/addon/ember-inspector/)
- Thanks to [Rock And Roll with Ember Octane](https://balinterdi.com/rock-and-roll-with-emberjs/)