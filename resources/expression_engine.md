# Expression Engine
Your expression might fail on the user's machine since they have a different expression engine setting.
After-Effects has 2 expression engines:
* Legacy ExtendScript
* JavaScript

In 2022, you are most likely using the JavaScript engine and are writing modern JavaScript expressions.
Either way, you want to make sure the user is using the same setting as yours.

# Solution
You can use this function to check whether the new JavaScript expression engine is set
```js
function isJavaScriptExpressionEngineSet() {
    // Returns true if JavaScript, false if Legacy ExtendScript or undefined if check failed.
    if (!app || !app.project) {
        return undefined;
    }

    var currentEnginge = app.project.expressionEngine || "";
    return currentEnginge.toLowerCase().indexOf("javascript") >= 0; 
}
```

Then you can decide what to do in either case:
```js
var isJSExpressionEngine = isJavaScriptExpressionEngineSet();
if (isJSExpressionEngine === false) {
    // Engine is set to Legacy ExtendScript
} else if (isJSExpressionEngine === true) {
    // Engine is set to JavaScript
} else {
    // Check failed
}
```

### Change the setting or prompt the user
If you want, you can change the expression engine setting yourself using this function:
```js
function setExpressionEngineToJS() {
    if (!app || !app.project) {
        // failed to get the project
        return;
    }

    // Unfortunatelly, this setting is buggy and doesn't work as expected.
    // To fix that and make sure it works, we set the engine multiple times, then change the bitrate of the project to make sure the changes are applied.

    // Set the engine to JavaScript
    app.project.expressionEngine = "javascript-1.0";
        try {
            app.project.expressionEngine = "0";
        } catch (e) { }
    app.project.expressionEngine = "javascript-1.0";
    
    // Set the engine to JavaScript
    temp = app.project.bitsPerChannel;
    app.project.bitsPerChannel = 8;
    app.project.bitsPerChannel = 16;
    app.project.bitsPerChannel = 32;
    app.project.bitsPerChannel = temp;
    
    return app.project.expressionEngine === "javascript-1.0"; // return true if successful
}

```

However, some users might not like that (let's say they intend to use the legacy expression engine).
In that case, you can ask them for premission to change that setting like so:
```js
var userAllowedChangeToJSEngine = confirm("I must be set to JavaScript to work properly. Pretty please?");
if (userAllowedChangeToJSEngine) {
    setExpressionEngineToJS();
} else {
    alert("I can't work without JavaScript.\nPlease go to File -> Project Settings -> Expressions -> Expressions Engine and set it to JavaScript. Bye now!");
}
```
<img width="372" alt="image" src="https://user-images.githubusercontent.com/66829812/203055870-69b3f5bf-0d13-42ef-9da4-4757eaa7ffc0.png">
<img width="372" alt="image" src="https://user-images.githubusercontent.com/66829812/203055906-f6f2ffc5-7f7a-4333-98dd-962ecbeb1281.png">
