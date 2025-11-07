# gif-display

This allows you to have an animated GIF that floats above your Linux desktop — built with Python and PyQt6.

## 🎬 Demo

Here’s a preview:

![Image](https://github.com/user-attachments/assets/e4148694-2951-4825-ab3b-64feb683b022)

This allows you to have an animated GIF that floats above your Linux desktop — built with Python and PyQt6.

# 🧿 Desktop Gif

A way to have an animated GIF float above your desktop.  
Built with **Python** and **PyQt6**, this simple project creates a way for you to have an animated gif that stays above all windows and can be moved freely.

---
Add the path to your gif
# Path to GIF
gif_path = " "

Adjust the scale_factor to your liking
# Fixed scale factor to reduce size by 60%
scale_factor = 0.4

## ✨ Features

- 🖱️ **Draggable** — click and move the gif anywhere  
- 🌀 **Resizable** — via code scale_factor 
- 🪟 **Transparent background**  
- 🎞️ **Animated GIF support**  
- ⚡ **Always on top of other windows**  
- ⌨️ **Hotkeys**
  - **F1** — hide/show the sprite (might not work as expected if using a window manager) 
  - **ESC** — quit the app  

---

## 🧰 Requirements

- Python 3.10+  
- [PyQt6](https://pypi.org/project/PyQt6/)  
- [Pillow](https://pypi.org/project/Pillow/)

Install dependencies:
```bash
pip install PyQt6 Pillow
