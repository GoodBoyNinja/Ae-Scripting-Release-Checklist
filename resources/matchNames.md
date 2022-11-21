## What are Match Names?
Items in After-Effects often have secondary names. Those names are called **Match Names** and are consistent across all copies of After-Effects, no matter the language.



## How the I know what Match Names to use?
* You can use the official [After-Effects Scripting Guide](https://ae-scripting.docsforadobe.dev/index.html). Scroll down to find the **Match Names** category.


## Example

Let's say we have a layer
```js
var layer = app.project.activeItem.selectedLayers[0];
```

In this example, we want to reference the Position property of the layer.
This expression will fail in non English versions of After-Effects

```js
var positionPropBad = layer("Transform")("Position");
// ❌ Will fail on non eng versions since "Transform" and "Position" may have different names
```

To fix this, we can use Match Names instead.
```js
var positionPropGood = layer("ADBE Transform Group")("ADBE Position");
// ✅ Should work since matchnames are universal and apply to all languages
```

---
Alternative Solutions
Some properties (such as position, rotation, scale, opacity) are embeded into ExtendScript and can be directly referenced without passing in a string:
```js
var positionPropGood2 = layer.position;
// ✅ .position is not a string so it should work regardless to the language of After-Effects
```

Alternatively, you can also reference items by index, like so:
```js
var positionPropGood3 = layer.property(5).property(2);
// ✅ this will also get the position regardless to the language, but isn't very readable. 
```
