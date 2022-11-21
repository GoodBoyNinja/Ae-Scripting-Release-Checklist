# JSX Scripts Release Checklist
---
> Developers, please feel free to contribute to this list based on your own experience ❤️



 &nbsp;
 
🔒 Protect your work
*  [Convert your file to JSXBIN](https://extendscript.docsforadobe.dev/vscode-debugger/vscode-extension-features.html#exporting-as-binary) to (partially) protect your code and reduce chance of privacy.

 &nbsp;
 
🌎 Make sure your script works across the globe
* Use [Match Names](/resources/matchNames.md) instead of Names when referencing items in After-Effects.
* *  If your script creates, appends or modifies expressions, make sure those expressions also use [Match Names](/resources/matchNames.md) instead of Names.
* If you are using Command IDs, [use them by numbers](https://hyperbrew.co/blog/after-effects-command-ids/) and **not** by name, sinces names change between languages (Thanks Justin Taylor)
*  When accessing files on the user's machine, [use the built in "Folder" class properties](https://extendscript.docsforadobe.dev/file-system-access/folder-object.html#folder-class-properties) whenever possible to avoid broken paths to directories and files due to language differences.

 &nbsp;
 
⚙️ Avoid preferences hell
* If your script contacts the internet, and / or writes, deletes or makes changes to local files on the user's machine, be aware of the fact that users may prevent you from doing so, by disabling "Allow Scripts to Write Files and Access Network". [You might want to warn users that access is denied to get your script to work.](resources/files_and_network_access.md)
* If your script injects, modifies or appends an expression, you might want to [make sure that the user is using the correct Expression Engine](resources/expression_engine.md), otherwise your expression might fail on their machine.

&nbsp;

🤺 Avoid conflicts with other tools
* [Avoid using the prototype keyword.](https://www.tutorialsteacher.com/javascript/prototype-in-javascript). ```.prototype``` lets you add properties to existing functions / objects. When being done so on built in objects, such as `Array.prototype` or `String.prototype` these changes apply to any other script that After-Effects will run after yours, meaning you are making changes to the core features. By doing that you might be breaking other scripts.
* * It's worth noting that other scripts may break yours by doing the same thing.
* * Also worth noting that some built in After-Effects panels might break yours (HA!)
* * If in doubt, ask users to run your script in the "Minimal" After-Effects workspace where no other tools exist to make sure any errors are not introduced by others making changes to core language features.
* * Tell other developers to not do it.
* When using [Polyfills](https://developer.mozilla.org/en-US/docs/Glossary/Polyfill) try to make sure they do not make changes to core features using `.prototype`. If possible, make changes to those polyfills and turn them into objects with methods. The most common one is polyfilling `json` or `json2.js` by including it in your code.

&nbsp;

💻 Avoid operating system hell:
* Just because your script works on Windows doesn't mean it will work on MacOS, and vice versa.
* If possible, check your script or find beta testers to help you checking your script on the operating system that you don't use.
* MacOS paths are seperated by `/` while on Windows they can **also** be seperated by `\\`. When hard coding paths prefer `/`, and in general [follow these guidelines for Specifying Paths](https://extendscript.docsforadobe.dev/file-system-access/using-file-and-folder-objects.html#specifying-paths)


&nbsp;

🛡️ Prepare for the unexpected:
* If you are using `curl` in combination with `system.callSystem` ([to contact gumroad for example](https://github.com/Adobe-CEP/CEP-Resources/issues/237)) be aware that curl is not shipped with older versions of Windows which your users might be using. It's a shitty poopoo situation so good luck with that.
* Note that any network calls can be blocked by VPNs, Anti-Viruses and Firewalls. If a user is having issues and you can't find the problem, this might be the problem.
* Note that any file system access operations **May** be blocked by Firewalls, but are usually not.


&nbsp;

___
# Take a deep breath
You will never make your script bulletproof, but you can get pretty close.
If possible, always check on multiple machines, have users from various places on the planet beta test, and finally hope for the best and prepare for the worst. You've done a great job! Good Luck!

