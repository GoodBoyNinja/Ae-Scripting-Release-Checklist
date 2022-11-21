# JSX Scripts Release Checklist
---
> Developers, please feel free to contribute to this list based on your own experience



 &nbsp;
 
🔒 Protect your work
*  [Convert your file to JSXBIN](https://extendscript.docsforadobe.dev/vscode-debugger/vscode-extension-features.html#exporting-as-binary) to (partially) protect your code and reduce chance of privacy.

 &nbsp;
 
🌎 Make sure your script work across the globe
* Use [Match Names](/resources/matchNames.md) instead of Names when referencing items in After-Effects.
* *  If your script creates, appends or modifies expressions, make sure those expressions also use [Match Names](/resources/matchNames.md) instead of Names.
* If you are using Command IDs, [use them by numbers](https://hyperbrew.co/blog/after-effects-command-ids/) and **not** by name, sinces names change between languages (Thanks Justin Taylor)
*  When accessing files on the user's machine, [use the built in "Folder" class properties](https://extendscript.docsforadobe.dev/file-system-access/folder-object.html#folder-class-properties) whenever possible to avoid broken paths to directories and files due to language differences.

 &nbsp;
 
⚙️ Avoid preferences hell
* If your script contacts the internet, and / or writes, deletes or makes changes to local files on the user's machine, be aware of the fact that users may prevent you from doing so, by disabling "Allow Scripts to Write Files and Access Network". [You might want to warn users that access is denied to get your script to work.](resources/files_and_network_access.md)
* If your script injects, modifies or appends an expression, you might want to [make sure that the user is using the correct Expression Engine](resources/expression_engine.md), otherwise your expression might fail on their machine.

