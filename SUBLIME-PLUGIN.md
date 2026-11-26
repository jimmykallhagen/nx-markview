# Sublime Text Plugin for `nx-markview`

**A lightweight, zero-bloat Sublime Text 4 plugin to view your Markdown projects in a full rendered view styled with the Nordix color palette.**

- Featuring GitHub-style Markdown rendering with support for embedded raw HTML
- Powered by `nx-markview`
- Built with Tauri

**Install `nx-markview` from source code:**
[**nx-markview source code**](https://github.com/jimmykallhagen/nx-markview)

**AUR:**
[**Arch Linux nx-markview - AUR**](https://aur.archlinux.org/packages/nx-markview)

**Install from AUR:**
```bash
paru -S nx-markview
```
```bash
yay -S nx-markview
```

---

## Project Structure

Create a directory named `nx-markview` inside your Sublime Text `Packages` folder (`~/.config/sublime-text/Packages/nx-markview/`):

```text
nx-markview/
├── Context.sublime-menu
├── Default (Linux).sublime-keymap
├── Default.sublime-commands
├── Main.sublime-menu
├── nx-markview.sublime-settings
├── nx_markview.py
└── README.md
```

---

## Plugin Files

### 1. `nx_markview.py`

```python
import shutil
import subprocess
import sublime
import sublime_plugin


class OpenInNxMarkviewCommand(sublime_plugin.WindowCommand):
    def run(self):
        view = self.window.active_view()
        if not view or not view.file_name():
            sublime.status_message("nx-markview: Please save the file first.")
            return

        if view.is_dirty():
            view.run_command("save")

        settings = sublime.load_settings("nx-markview.sublime-settings")
        binary = settings.get("binary_path", "nx-markview")

        if not shutil.which(binary):
            sublime.error_message(
                "Could not find '{}' in PATH. Make sure nx-markview is installed.".format(binary)
            )
            return

        subprocess.Popen([binary, view.file_name()])

    def is_visible(self):
        view = self.window.active_view()
        if not view:
            return False
        syntax = view.settings().get("syntax", "").lower()
        return "markdown" in syntax
```

### 2. `nx-markview.sublime-settings`

```json
{
    "binary_path": "nx-markview"
}
```

### 3. `Default.sublime-commands`

Makes the command searchable in the Command Palette (`Ctrl+Shift+P`):

```json
[
    {
        "caption": "nx-markview: Open Current File",
        "command": "open_in_nx_markview"
    }
]
```

### 4. `Context.sublime-menu`

Adds the action to the right-click context menu when editing Markdown files:

```json
[
    { "caption": "-" },
    {
        "caption": "Open in nx-markview",
        "command": "open_in_nx_markview"
    }
]
```

### 5. `Main.sublime-menu`

Adds the action under **Tools** in the top menu bar and **Preferences -> Package Settings**:

```json
[
    {
        "id": "tools",
        "children": [
            {
                "caption": "Open in nx-markview",
                "command": "open_in_nx_markview"
            }
        ]
    },
    {
        "id": "preferences",
        "children": [
            {
                "id": "package-settings",
                "children": [
                    {
                        "caption": "nx-markview",
                        "children": [
                            {
                                "caption": "Settings",
                                "command": "edit_settings",
                                "args": {
                                    "base_file": "\${packages}/nx-markview/nx-markview.sublime-settings",
                                    "default": "{\n\t\$0\n}\n"
                                }
                            },
                            {
                                "caption": "Key Bindings",
                                "command": "edit_settings",
                                "args": {
                                    "base_file": "packages/nx-markview/Default (platform).sublime-keymap",
                                    "default": "[\n\t\$0\n]\n"
                                }
                            }
                        ]
                    }
                ]
            }
        ]
    }
]
```

### 6. `Default (Linux).sublime-keymap`

```json
[
    {
        "keys": ["ctrl+shift+v"],
        "command": "open_in_nx_markview",
        "context": [
            { "key": "selector", "operator": "equal", "operand": "text.html.markdown" }
        ]
    }
]
```

---

## Installation

### Prerequisites

Install `nx-markview` from the AUR:

```bash
yay -S nx-markview
```

### Manual / Git Installation

Clone the plugin repository directly into Sublime Text's `Packages` directory:

```bash
git clone https://github.com ~/.config/sublime-text/Packages/nx-markview
```

### System-Wide / Distro Skeleton Setup (e.g. Nordix)

To pre-configure the plugin for all newly created users, place the plugin directory in `/etc/skel`:

```bash
sudo mkdir -p /etc/skel/.config/sublime-text/Packages
sudo cp -r nx-markview /etc/skel/.config/sublime-text/Packages/
```

---

## Usage

1. Open any `.md` file in Sublime Text.
2. Press **`Ctrl+Shift+V`**, right-click inside the editor and select **Open in nx-markview**, or open the Command Palette (`Ctrl+Shift+P`) and run **`nx-markview: Open Current File`**.
