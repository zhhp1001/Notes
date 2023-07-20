# VsCode 

## cannot edit in read-only editor

The default settings in vscode is a non-editable document. It acts as a way for you to view the default settings for native settings as well as extension default settings.

These defaults are also used to identify when a setting has changed with a 'blue' line indicator, when using the [settings editor](https://code.visualstudio.com/docs/getstarted/settings#_settings-editor):

> Changes to settings are reloaded by VS Code as you change them. Modified settings are now indicated with a blue line similar to modified lines in the editor. The gear icon opens a context menu with options to reset the setting to its default value as well as copy setting as JSON.

Currently, vscode only offers 2 editable settings:

> VS Code provides two different scopes for settings:
>
> - User Settings - Settings that apply globally to any instance of VS Code you open.
> - Workspace Settings - Settings stored inside your workspace and only apply when the workspace is opened.
>
> Workspace settings override user settings. Workspace settings are specific to a project and can be shared across developers on a project.
>
> > Note: A VS Code "workspace" is usually just your project root folder. Workspace settings as well as debugging and task configurations are stored at the root in a .vscode folder. You can also have more than one root folder in a VS Code workspace through a feature called Multi-root workspaces.

Edit your `settings.json` by:

```bash
File -> Preferences -> Settings
```



## Visiting remote container

After installing the extension `remote-container` . Attach the running container you want to study, then: 

1. `ctrl + shift + p`

2. `Remote-Containers:Attach to Running Container...`

3. `ctrl + k`   and  `ctrl + o` . Now you can explore files in the remote container!

**[Reference](https://segmentfault.com/a/1190000023095631)**



## #include errors detected

 Left 🖰 click on the bulb next to the squiggled code line.

Follow the guide to add your path.



## Comment

First use vim shortcut `v` to select the code chunk you want to comment,

then,  `ctrl + \` to comment the chunk.