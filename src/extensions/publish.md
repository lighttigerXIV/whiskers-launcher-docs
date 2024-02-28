# Publish To Store

To publish the extension in the extensions store you firstlly need a repository on github or gitlab to host the extension and it's source code. Then can either open
an [issue](https://github.com/lighttigerXIV/whiskers-launcher-extensions/issues) on
its [repository](https://github.com/lighttigerXIV/whiskers-launcher-extensions) and give the required data, or you can
do a pull request with the new data.

## Required Data

| Key         | What it does                                                                             |
| ----------- | ---------------------------------------------------------------------------------------- |
| id          | Provides the extension id (used in manifest.json)                                                               |
| name        | Provides the extension name                                                              |
| description | Provides the extension description                                                       |
| repo        | The link to the extension repo                                                           |
| preview     | The link to the image preview                                                            |
| os          | The os that the extension can run. Must be one of the following ["*", "linux", "windows"] |

## Example

```json
{
    "id": "lighttigerxiv/session-manager",
    "name": "Session Manager",
    "description": "This extension adds options to shutdown, reboot, suspend, hibernate and logout",
    "repo": "https://github.com/lighttigerXIV/whiskers-launcher-session-manager-extension",
    "preview": "https://raw.githubusercontent.com/lighttigerXIV/whiskers-launcher-session-manager-extension/master/preview.webp",
    "os":["*"]
}
```
