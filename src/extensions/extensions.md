# Extensions

This chapter will provide you information on how to build an extension for whiskers launcher.

In short an extension needs a **manifest.json** file and an **extension** (binary/exe) to run it.
The extension purpose is to get the context and make it send results to the app or run some custom code.

## Init Project
The first step is to create a rust project:
```bash 
cargo new extension-name 
```

## Needed Files In The Project Root

| File Name     | What it does                                                      |
|---------------|-------------------------------------------------------------------|
| manifest.json | Provides the manifest for the launcher to read its properties     |
| extension     | The program to give the results or run actions from the extension |
| extension.exe | The same as above but if the extension runs on windows too        |
