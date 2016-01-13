# mimosa-comment-defeature

A mimosa module for allowing you to specify lines or blocks of code as features to be enabled or disabled dynamically.

## Usage

In your app's `mimosa-config.js`, define `commentDefeature` options on your app instance as such:

```javascript
  commentDefeature: {
    features: {
      'shiny': false,
      'mapping.wgs84': process.env.BUILD_PROFILE !== 'customer1'
    }
  }
```

Then you're ready to start decorating your code with feature descriptors.

### In JavaScript

#### Before
```javascript
export default Ember.Component.extend({
  tagName: 'span',

  /* feature shiny */
  shiny: Ember.inject.service(),

  /* feature shiny:start */
  demonstrateShininess: Ember.observer('model', function () {
    this.get('shiny').makeNoise('Totes shiny');
  })
  /* feature shiny:end */
});
```

#### After

```javascript
export default Ember.Component.extend({
  tagName: 'span',

  /* feature shiny */
//   shiny: Ember.inject.service(),

  /* feature shiny:start */
//   demonstrateShininess: Ember.observer('model', function () {
//     this.get('shiny').makeNoise('Totes shiny')
//   })
  /* feature shiny:end */
});
```


### In Handlebars

#### Before

```handlebars
{{!-- feature shiny --}}
{{shiny-feature model=shiny}}

<h1>Some Page</h1>

{{!-- feature shiny:start --}}
<div>
  <h2>Shiny is enabled!</h2>
  <p>This text will only be visible if feature "shiny" is enabled.</p>
</div>
{{!-- feature shiny:end --}}
```

#### After

```handlebars
{{!-- feature shiny --}}
{{!-- {{shiny-feature model=shiny}} --}}

<h1>Some Page</h1>

{{!-- feature shiny:start --}}
{{!-- <div> --}}
{{!--   <h2>Shiny is enabled!</h2> --}}
{{!--   <p>This text will only be visible if feature "shiny" is enabled.</p> --}}
{{!-- </div> --}}
{{!-- feature shiny:end --}}
```

### In CSS/SCSS

#### Before

```css
/* feature shiny */
.shiny-one-liner {}

.some-container {
  background-color: gold;
  /* feature shiny:start */
  color: red;
  border-color: lime;
  /* feature shiny:end */
}
```

#### After

```css
/* feature shiny */
/* .shiny-one-liner {} */

.some-container {
  background-color: gold;
/* feature shiny:start */
/*   color: red; */
/*   border-color: lime; */
/* feature shiny:end */
}
```


## Options

### commentDefeature.features: `object`

A key-value hash of your features.  Defaults to `{}`.

### commentDefeature.extensions: `string[]`

An array of file extensions that will be processed.  Defaults to `['js', 'hbs', 'css', 'scss']`.


## Credits

Inspired by the following projects:

- [ember-cli-defeatureify](https://github.com/jkarsrud/ember-cli-defeatureify)
- [broccoli-defeatureify](https://github.com/sindresorhus/broccoli-defeatureify)
- [mimosa-defeature](https://github.com/peluja1012/mimosa-defeature)
