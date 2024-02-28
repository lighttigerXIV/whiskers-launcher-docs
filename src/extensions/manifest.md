# Manifest

To make an extension you must have a manifest.json file in order for the launcher to read its name, settings and more.
The manifest has the possible fields:

**Fields marked with \* are required**

#### Main Options

| Key            | What it means                         | Possible Options          |
| -------------- | ------------------------------------- | ------------------------- |
| id\*           | The extension id                      | -                         |
| name\*         | The extension name                    | -                         |
| version_name\* | The version name                      | -                         |
| version_code\* | The version code                      | -                         |
| description\*  | The extension description             | -                         |
| os\*           | Supported os for the extension        | ["*", "linux", "windows"] |
| keyword\*      | The default keyword for the extension | -                         |
| settings       | The extension settings                | **Settings Options**      |

#### Settings Options

| Key             | What it means                                                                                               | Possible Options             |
| --------------- | ----------------------------------------------------------------------------------------------------------- | ---------------------------- |
| id\*            | The setting id                                                                                              | -                            |
| title\*         | The setting title                                                                                           | -                            |
| description\*   | The setting description                                                                                     | -                            |
| setting_type\*  | The setting type                                                                                            | ["text", "select", "toggle"] |
| default_value\* | The setting default value                                                                                   | -                            |
| os\*            | The supported os for the setting                                                                            | ["*", "linux", "windows"]    |
| select_options  | The select options in case the types is "select"                                                            | **Select Options**           |
| show_condition  | The show condition for the setting. You may want to hide a setting if another doesn't have a specific value | **Show Conditions**          |

#### Select Options

| Key    | What it does           | Possible Options |
| ------ | ---------------------- | ---------------- |
| id\*   | The select option id   | -                |
| text\* | The select option text | -                |

#### Settings Conditions

| Key             | What it does      | Possible Options |
| --------------- | ----------------- | ---------------- |
| setting_id\*    | The setting id    | -                |
| setting_value\* | The setting value | -                |

## Full Example

```json
{
  "id": "lighttigerxiv/extensions-example",
  "name": "Extensions Example",
  "version_name": "1.0.0",
  "version_code": 1,
  "description": "A extension with all possible options. It serves as documentation too",
  "os": ["*"],
  "keyword": "ee",
  "settings": [
    {
      "id": "favourite_pokemon",
      "title": "Favourite Pokemon",
      "description": "Just a setting to say your favorite pokemon",
      "setting_type": "text",
      "default_value": "Sprigatito",
      "os": ["*"]
    },
    {
      "id": "favourite_penguin_pokemon",
      "title": "Favourite Penguin Pokemon (Only Shows In Linux)",
      "description": "Just a setting to say your favorite penguin pokemon",
      "setting_type": "text",
      "default_value": "Piplup",
      "os": ["linux"]
    },
    {
      "id": "best_gen1_pokemon",
      "title": "Best Gen 1 Pokemon",
      "description": "Select the best generation 1 starter",
      "setting_type": "select",
      "default_value": "bulbasaur",
      "os": ["*"],
      "select_options": [
        {
          "id": "bulbasaur",
          "text": "Bulbasaur"
        },
        {
          "id": "charmander",
          "text": "Charmander"
        },
        {
          "id": "squirtle",
          "text": "Squirtle"
        },
        {
          "id": "other",
          "text": "Other"
        }
      ]
    },
    {
      "id": "custom_best_gen1_starter",
      "title": "Custom Favourite Gen 1 Pokemon",
      "description": "Type the custom best generation 1 starter",
      "setting_type": "text",
      "default_value": "",
      "os": ["*"],
      "show_conditions": [
        {
          "setting_id": "best_gen1_pokemon",
          "setting_value": "other"
        }
      ]
    },
    {
      "id": "pokemon_master",
      "title": "Pokemon Master",
      "description": "Toggle this if you are pokemon master",
      "setting_type": "toggle",
      "default_value": "false",
      "os": ["*"]
    }
  ]
}
```
