# Nordix Markdown Viewer

**Part of:** `[Nordix](https://github.com/jimmykallhagen/Nordix)`  
**Author:** `Jimmy Källhagen`  
**License:** `GPL-3.0-or-later`

> **A simple local Markdown viewer with simple HTML support. Build with Cargo Tauri**:

---

# Functions

 - Preeview Markdown files like `README.md`
 - "Drop in" to other projekt to show documantations
 - Support simple HTML tags like `<kbd>`, `<br>`, `<div>`, `<img>`
 - Supports webb links
 - Supports local images (not images from web pages, security restrictions in Linux WebKitt)

---

## Usage 

```Fish
nx-markview /path/to/file
```

---

## Install

**From Git:**
```Fish
git clone https://github.com/jimmykallhagen/nx-markview.git
cd ./nx-markview.git
npm install
cargo tauri build
```

**Arch linux**
```Fish
mkdir -p ~/Builds
cd ~/Builds
git clone https://github.com/jimmykallhagen/nx-markview.git
cd ./nx-markview.git
makepkg -si
```

**Arch linux with Paru and Yay**
```Fish
paru -Sy nx-markview
yay -Sy nx-markview
```

---

## Screenshots
![1](https://github.com/jimmykallhagen/nx-markview/blob/main/screenshots/Screenshot-Sat%20May%2030%2007%3A06%3A29%20PM%20CEST%202026.png)
![2](https://github.com/jimmykallhagen/nx-markview/blob/main/screenshots/Screenshot-Sat%20May%2030%2007%3A09%3A09%20PM%20CEST%202026.png)
