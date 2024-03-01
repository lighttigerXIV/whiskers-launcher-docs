# Main.rs
## Context

When the extension is executed it can receive a context. This context is responsible to provide the type of action the
extension will do. Depending on the type of action it will send other fields.
If the action is the type of **GetResults**, the extension should send the results.
If the action is the type of **RunAction**, the extension should see what action it is and run the appropriate code.

Basic usage:

```rust
let context = get_extension_context().unwrap();

match context.action{
    api::extensions::Action::GetResults => {
        // Send The Results Here
    },
    api::extensions::Action::RunAction => {
        // Run custom action code
    }   
}
```

## Results

The api supports 3 types of results.

| Type         | What it shows                                                 |
|--------------|---------------------------------------------------------------|
| Text         | Shows a text result, it supports icons too                    |
| TitleAndText | Shows a title, a smaller text below and it supports icons too |
| Divider      | Shows a divider                                               |

### Text

The text result requires a text and an action. The optional fields are icon, tint icon, tint color

```rust
let result = WhiskersResult::Text(
    results::Text::new(
        "Text Result With A Custom Tinted Icon",
        actions::Action::Nothing,
    )
    .icon("your_icon_path_here")
    .tint_icon(true)
    .tint_color("#FF0000"),
);
```

### TitleAndText

The title and text result requires a title, a text and an action. The optional fields are icon, tint icon and tint
color.

```rust
let result = WhiskersResult::TitleAndText(
    results::TitleAndText::new(
        "Title And Text With A Custom Tinted Icon",
        "Text",
        actions::Action::Nothing,
    )
    .icon("your_icon_path_here")
    .tint_icon(true)
    .tint_color("#00FF00"),
);
```

### Actions

The api supports 6 types of actions.

| Type            | What it does                                                         |
|-----------------|----------------------------------------------------------------------|
| OpenApp         | Opens a app, given the path to it                                    |
| OpenUrl         | Opens a url in the default browser                                   |
| CopyToClipboard | Copies the text to the clipboard                                     |
| Extension       | Run a action inside the extension                                    |
| Dialog          | Opens a dialog with some fields and then the extension can read them |
| Nothing         | Does Nothing                                                         |

### OpenApp

It requires the path for it's related file. On Linux, it's a .desktop file and on Windows is a .lnk file.

Example:

```rust
let action = actions::Action::OpenApp(
    actions::OpenApp::new("exec_path_as_string")
);
```

### OpenUrl

It requires the url that will be opened.

Example:

```rust
let action = actions::Action::OpenUrl(
    actions::OpenUrl::new("https://google.com")
);
```

### CopyToClipboard

It requires the url that will be opened.

Example:

```rust
let action = actions::Action::CopyToClipboard(
    actions::CopyToClipboard::new("text_to_copy")
);
```

### Extension

It requires the extension id (used in manifest) and .

```rust
let action = actions::Action::Extension(actions::Extension::new(
    "extension_id",
    "action_name",
);
```

### Dialog

A dialog requires an extension id (used in manifest), a title, an action name and some dialog fields

#### Action

```rust
let action = Action::Dialog(
    actions::Dialog::new(
        EXTENSION_ID,
        "Random Fields About Pokemon",
        "show_dialog_results",
        dialog_fields, //This is a vector of fields
    )
    .primary_button_text("Custom Button Text"),
);
```

#### Dialog Fields

| Type       | What id does                        |
|------------|-------------------------------------|
| Input      | Shows a input field                 |
| Toggle     | Shows a toggle field                |
| Select     | Shows a select field                |
| TextArea   | Shows a text area field             |
| SelectFile | Shows a select file/directory field |

#### Input

The input field requires an id, a title and a value. The optional fields are description, placeholder and custom_args.

Example:

```rust
let field = DialogField::Input(
    dialog::Input::new("best_pokemon", "Best Pokemon", "")
        .placeholder("Best pokemon")
        .description("Type the best pokemon in your opinion"),
);
```

#### Toggle

The toggle field requires an id, a toggled bool and a title. The optional fields are description and custom_args.

Example:

```rust
let field = DialogField::Toggle(
    dialog::Toggle::new("pokemon_master", "Are you a pokemon master?", true)
        .description("Toggle if you are pokemon master :D"),
);
```

#### Select

The select field requires an id, a default_field_id and a title. The optional fields are description, fields and
custom_args.

Example:

```rust
let mut starters: Vec<SelectField> = vec![];
starters.push(SelectField::new("litten", "Litten"));
starters.push(SelectField::new("rowlet", "Rowlet"));
starters.push(SelectField::new("popplio", "Popplio"));
            
let field = DialogField::Select(
    dialog::Select::new(
        "best_gen7_starter",
        "Best gen 7 starter",
        "litten",
        starters,
    )
    .description("Type the best pokemon in your opinion"),
);
```

#### TextArea

The text area field requires an id, a title, and a value. The optional fields are description, placeholder, custom_args

Example:

```rust
let field = DialogField::TextArea(
    dialog::TextArea::new("describe_favourite", "Describe Favourite Pokemon", "")
        .description("Describe your favourite pokemon")
        .placeholder("Favourite Mon :P"),
)
```

#### SelectFile

The select file field requires an id, a title

Example:

```rust
let file_field = DialogField::SelectFile(
    dialog::SelectFile::new("select_file_example", "Select File")
        .description("Select a random picture")
        .filters(vec![
            dialog::FileFilter::new("Image Files")
                .add_extension("png")
                .add_extension("jpg")
                .add_extension("jepg")
                .add_extension("svg")
            ]
        ),
)

let dir_field = DialogField::SelectFile(
    dialog::SelectFile::new("select_dialog_example", "Select Directory")
        .description("Select a random directory")
        .select_dir(true),
)
```

## Sending Results
To send the results to the app you can call the send_extension_results function:

```rust
let mut results = Vec::<WhiskersResult>::new();
results.push(WhiskersResult::Text(results::Text::new(
    "First Result",
    actions::Action::Nothing,
)));
results.push(WhiskersResult::Text(results::Text::new(
    "Second Result",
    actions::Action::Nothing,
)));

send_extension_results(results);
```

## Get Dialog Results
To get the dialog results you need to get the response and then get the results.

```rust
let response = get_extension_dialog_response().unwrap();
let results = response.results;
```



## Extension Action

To run custom extension action you need the action itself. Note this should be done only when the context is
RunAction

```rust
let context = get_extension_context().unwrap();
let action = context.extension_action.unwrap();

if action == "do_something"{
    // Do Something
}
```

## Extension Setting
To get an extension setting you can call the following function:

```rust
let setting = get_extension_setting(EXTENSION_ID, "setting_id").unwrap();
```

## Sending Notifications
To send a notification you can call the following function:

```rust
send_notification("Title", "Notification message");
```

## Small Example
```rust
pub fn get_icon(name: impl Into<String>) -> String {
    let name = name.into();
    let mut path = get_extension_dir(EXTENSION_ID).unwrap();
    path.push(format!("src/resources/icons/{}", &name));

    path.into_os_string().into_string().unwrap()
}

fn main(){
    let context = get_extension_context().unwrap();
    
    
    match context.action{
        api::extensions::Action::GetResults => {
            let search_text = context.search_text.unwrap();
            let mut results = Vec::<WhiskersResult>::new();
            
            if search_text == "pika"{
                results.push(WhiskersResult::Text(
                    results::Text::new(
                        "Copy Pikachu",
                        actions::Action::CopyToClipboard(actions::CopyToClipboard::new("Pikachu")),
                    )
                    .icon(get_icon("pikachu.webp"))
                    .tint_icon(true),
                ))
            } 
            
            if search_text == "bul"{
                results.push(WhiskersResult::Text(
                    results::Text::new(
                        "Copy Bulbasaur",
                        actions::Action::CopyToClipboard(actions::CopyToClipboard::new("Bulbasaur")),
                    )
                    .icon(get_icon("bulbasaur.webp"))
                    .tint_icon(true),
                ))
            }
            
            if search_text == "custom"{
                results.push(WhiskersResult::Text(
                    results::Text::new(
                        "Custom Action",
                        actions::Action::Extension(
                            actions::Extension::new(EXTENSION_ID, "delete_group"),
                        ),
                    )
                    .icon(get_icon("trash.svg"))
                    .tint_icon(true),
                ))
            } 
            
            send_extension_results(results);
        },
        api::extensions::Action::RunAction => {
            let action = context.to_owned().extension_action.unwrap();
            
            if action == "custom"{
                //Do Something
                send_notification("Custom Action", "Custom extension action");
            }
        }   
    }
}
```

A full example can be found [here](https://github.com/lighttigerXIV/whiskers-launcher-extension-example)





