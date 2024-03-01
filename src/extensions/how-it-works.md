# How It Works

For the extension to work it needs to return results to the launcher. For that to happen the launcher must know the data about the extension. That data can be found in a **manifest.json** file in src folder. 

When the extension is executed it will receive a **context**. That context will provide information like the type of action to execute, the search text or some custom arguments. Then the extension is responsible to what it has to do depending on the type of action.

In order for the launcher to execute the extension it needs to have a binary or exe named **extension**

In summary, the launcher will execute the extension and depending on the context the extension will return some results or execute some custom actions.

## Files
This are the following required files:
- manifest.json
- extension (if it runs on linux)
- extension.exe (if it runs on windows)