# Publish To Store

To publish the theme in the themes store you can either open
an [issue](https://github.com/lighttigerXIV/whiskers-launcher-themes/issues) on
its [repository](https://github.com/lighttigerXIV/whiskers-launcher-themes) and give the required data, or you can
do a pull request with the new data.

## Required Data

| Key      | What it does                                      |
| -------- | ------------------------------------------------- |
| id       | Provides the extension id (used in manifest.json) |
| name     | Provides the extension name                       |
| repo     | Provides the extension repo                       |
| preview  | The link to the image preview                     |
| variants | **Variants**                                      |

### Variants

| Key  | What it does                      |
| ---- | --------------------------------- |
| name | Provides the name of the variant  |
| file | Provides the raw file in the repo |

## Example

```json
{
  "id": "lighttigerxiv/material-dark",
  "name": "Material Dark",
  "repo": "https://github.com/lighttigerXIV/whiskers-launcher-material-themes",
  "preview": "https://raw.githubusercontent.com/lighttigerXIV/whiskers-launcher-material-themes/master/dark-preview.png",
  "variants": [
    {
      "name": "Yellow",
      "file": "https://raw.githubusercontent.com/lighttigerXIV/whiskers-launcher-material-themes/master/themes/Yellow-Dark.json"
    },
    {
      "name": "Purple",
      "file": "https://raw.githubusercontent.com/lighttigerXIV/whiskers-launcher-material-themes/master/themes/Purple-Dark.json"
    },
    {
      "name": "Red",
      "file": "https://raw.githubusercontent.com/lighttigerXIV/whiskers-launcher-material-themes/master/themes/Red-Dark.json"
    },
    {
      "name": "Green",
      "file": "https://raw.githubusercontent.com/lighttigerXIV/whiskers-launcher-material-themes/master/themes/Green-Dark.json"
    },
    {
      "name": "Blue",
      "file": "https://raw.githubusercontent.com/lighttigerXIV/whiskers-launcher-material-themes/master/themes/Blue-Dark.json"
    }
  ]
}
```
