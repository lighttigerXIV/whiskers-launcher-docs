# Creating Project

## Init Project
To start a new project, create a new rust project with `cargo new extension-name` on the user extensions directory.

> **Linux**: $HOME/.local/share/com-lighttigerxiv-whiskers-launcher/UserExtensions
> 
> **Windows**: %APPDATA%/com-lighttigerxiv-whiskers-launcher/UserExtensions

## Adding dependency to cargo.toml
The extension requires the use of the launcher crate. To add it, add the following dependency in your cargo :
```toml
whiskers-launcher-rs = {git = "https://github.com/lighttigerXIV/whiskers-launcher-rs.git"}
``` 
