# Files and Network Access


<img width="298" alt="image" src="https://user-images.githubusercontent.com/66829812/203046406-db3a338c-a3f4-43e3-8c09-1f0f2021493e.png">

See that? Users may have this box unchecked which can silently make your script fail and make it very hard to understnad why.
This setting can be found under:
> MacOS: After-Effects > Preferences > Scripting and Expressions

or
> Windows: Edit -> Preferences > Scripting and Expressions

### Solution
You can detect the state of this preference in your script. If it's off, you might want to prompt the user to turn it on by using a dialog window, or a simple alert.
Use this function to detect the current setting:
```js
function AeHasAccessToFilesAndWeb() {
    try {
        var securitySetting = app.preferences.getPrefAsLong(
            "Main Pref Section",
            "Pref_SCRIPTING_FILE_NETWORK_SECURITY"
        );
        return securitySetting == 1;
    } catch (e) {
        // something went wrong, so assume access is denied. You can choose what ot do if that happens.
        return false;
    }
}
```
> You can ommit the try catch blocks to be more strict.

Then you can call this function, and if the result is false, display an error to your liking.
```js
var userGivenAccess = AeHasAccessToFilesAndWeb(); // true of false
if (!userGivenAccess) {
    alert("You need to allow access to files and the web in the preferences.");
}
```

<img width="372" alt="image" src="https://user-images.githubusercontent.com/66829812/203049001-df0b176b-79ca-46c2-9dc7-c8cb912a3df3.png">

