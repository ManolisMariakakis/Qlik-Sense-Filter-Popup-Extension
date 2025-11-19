# Qlik Sense Filter Popup Extension

A lightweight Qlik Sense visualization extension that displays a **button** on the sheet.  
When the user clicks the button, it opens a **popup window** containing a Filter Pane.  
The Filter Pane used in the popup is **not hidden** on the sheet — instead, you create it **once as a Master Item**, and the extension loads it by using its **object ID** across all sheets.

This allows you to reuse a single, central filter panel without placing it visually on every sheet.

---

## Features

- 🔘 Configurable **button label** (e.g. “Άνοιγμα φίλτρων”)
- 🪟 Popup window with configurable **title**
- 🧊 Dedicated area inside the popup where you can place:
  - A Qlik **Filter Pane** (by object ID)
- 🎯 Centered overlay with background dimming
- 📱 Simple responsive behaviour (fixed width/height popup)
- 🎨 Styling isolated under `.filter-popup-*` CSS classes

The core layout and styling are defined in `MyFilterPopup.css`.

---

## Folder structure

Typical extension folder structure:

```text
my-filter-popup/
├─ my-filter-popup.qext       # Extension metadata (name, description, icon, etc.)
├─ my-filter-popup.js         # Main extension logic (define([...])...)
├─ MyFilterPopup.css          # Styles (uploaded file)
├─ icon.png                   # Icon for the asset panel
└─ README.md                  # This file

---

## 🧩 Installation

1. **Download the ZIP file** of the extension from GitHub.  
2. In **Qlik Sense Enterprise for Windows**, go to the **QMC (Qlik Management Console)**.  
3. Open the **Extensions** section.  
4. Click **Import**, then select the downloaded ZIP file (`MyFilterPopup.zip`).  
5. Once imported, open your Qlik Sense app and add **My-Filter-Popup** to any sheet.

> 🧪 Tested on **Qlik Sense Enterprise for Windows – May 2025 release**.

---

## Configuration (Properties Panel)

### **Button label**  
Text displayed on the button.  
Default: `Open Filters`

### **Popup title**  
Text displayed at the top of the popup.

### **Filter Pane Object ID**  
Here is the key concept of this extension:

- You **create a Filter Pane once**, save it as a **Master Item**, and note its **object ID** (e.g., `PMtQar`).
- You enter that same object ID in the extension properties.
- The extension will load that Filter Pane **inside the popup**, no matter which sheet the user is currently on.

This makes the filter experience consistent across all sheets.

> ⚠️ The Filter Pane is not hidden nor duplicated — it is a single master object reused via its ID.

---

## How It Works

When rendered, the extension:

- Shows a button (`.filter-popup-btn`)
- Opens a modal overlay (`.filter-popup-overlay`) when clicked
- Displays a popup window (`.filter-popup-window`)
- Loads the Filter Pane using `app.getObject(div, filterId)` into the popup body

The CSS file defines:

- Button appearance
- Overlay styling
- Popup layout
- Header & close button

For example:

```css
.filter-popup-btn {
padding: 6px 12px;
background-color: #1976d2;
color: #fff;
border-radius: 4px;
}
