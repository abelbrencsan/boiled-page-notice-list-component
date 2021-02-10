# Boiled Page notice list component

Notice list SCSS component for Boiled Page frontend framework. It is intended to create notices.

## Install

Place `_notice-list.scss` file to `/assets/css/components` directory, and add its path to components block in `assets/css/app.scss` file. You will also need to add notice script to make it working properly.

- Notice script: <https://www.github.com/abelbrencsan/boiled-page-notice-script>

## Usage

### Classes

Class name | Description | Example
---------- | ----------- | -------
`notice-list` | Applies a notice list. | `<ul class="notice-list"></ul>`
`notice-list-item` | Applies a notice list item inside list. | `<li class="notice-list-item"></li>`
`notice-list-item-buttons` | Applies accept and/or dismiss buttons inside notice list item. | `<ul class="notice-list-item-buttons"></ul>`

### Examples

#### Example 1

The following example shows a notice with accept and dismiss buttons. `data-notice` attributes are used for notice script.

```html
<ul class="notice-list">
  <li class="notice-list-item" data-notice>
    <div class="grid grid--gutter">
      <div class="grid-col grid-col--fit">
        <p>This is a default notice.<p>
      </div>
      <div class="grid-col">
        <ul class="notice-list-item-buttons grid grid--gutter grid--gutter--half grid--uniform">
          <li class="grid-col">
            <button type="button" aria-label="Accept notice" data-notice-accept>✓</button>
          </li>
          <li class="grid-col">
            <button type="button" aria-label="Dismiss notice" data-notice-dismiss>✕</button>
          </li>
        </ul>
      </div>
    </div>
  </li>
</ul>
```

#### Example 2

The following example shows an error and a warning notice with dismiss buttons. `data-notice` attributes are used for notice script.

```html
<ul class="notice-list">
  <li class="notice-list-item notice-list-item--success" data-notice>
    <div class="grid grid--gutter">
      <div class="grid-col grid-col--fit">
        <p>This is a success notice.<p>
      </div>
      <div class="grid-col">
        <ul class="notice-list-item-buttons grid grid--gutter grid--gutter--half grid--uniform">
          <li class="grid-col">
            <button type="button" aria-label="Dismiss notice" data-notice-dismiss>✕</button>
          </li>
        </ul>
      </div>
    </div>
  </li>
  <li class="notice-list-item notice-list-item--warning" data-notice>
    <div class="grid grid--gutter">
      <div class="grid-col grid-col--fit">
        <p>This is a warning notice.<p>
      </div>
      <div class="grid-col">
        <ul class="notice-list-item-buttons grid grid--gutter grid--gutter--half grid--uniform">
          <li class="grid-col">
            <button type="button" aria-label="Dismiss notice" data-notice-dismiss>✕</button>
          </li>
        </ul>
      </div>
    </div>
  </li>
</ul>
```

### Script for examples

Add `notices` property to `app` object in `assets/js/app.js`.

```js
notices: []
```

Place the following code inside `assets/js/app.js` to initialize elements with `data-notices` attribute as notices.

```js
// Initialize notices
var noticeElems = document.querySelectorAll('[data-notice]');
for (var i = 0; i < noticeElems.length; i++) {
  app.notices[i] = new Notice({
    element: noticeElems[i],
    dismissTrigger: noticeElems[i].querySelector('[data-notice-dismiss]'),
    acceptTrigger: noticeElems[i].querySelector('[data-notice-accept]')
  });
  app.notices[i].init();
}
```

### Extension ideas

#### State colored notices

Add `generate-notice` to each state in SCSS variables with the value of true or false. Then you can use notices in colors of enabled states.

```scss
/* Notice component extensions */
ul.notice-list {

  // State colored notices
  @each $state in map-keys($states) {
    @if (map-val($states, $state, generate-notice)) {
      > li.notice-list-item.notice-list-item--#{$state} {
        background-color: map-val($states, $state, bg-color);
        color: map-val($states, $state, fg-color);
      }
    }
  }
}
```
