# Emojie iPhone images

Replace emoji unicode code points with Apple emoji images. Depends on
[emojie](https://github.com/lautis/emojie).

## Usage

First add emojie.js and emojie-iphone.js to HTML document, make `/images`
available. Then you should be able to

```javascript
emojie(document.body);
emojie(document.querySelector(".emoji-content")); // only replace a subtree with images
```

Use `Emojie.canRender` to detech when browser can render native colour emoji.

```javascript
Emojie.canRender("\ud83d\ude04") // smiley face emoji
// => returns true on Safari, false on Chrome, FF
```

## Hacking

1. bundle install
2. bundle exec rake js
3. bundle exec rake images
