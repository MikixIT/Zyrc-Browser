# Zyrc Browser

**Zyrc Browser** is a modern, lightweight, and customizable desktop browser built with **Vue.js** and originally planned with **Tauri**.
Inspired by innovative browsers like Arc, Zyrc aims to revolutionize browsing by offering a clean interface and smart features to boost productivity and user experience.

> ⚠️ **Note:** Due to current limitations in **Tauri v2** (no native support for embedding a full browser engine like Chromium), we are switching the core runtime to **Electron** to enable full browsing capabilities.

---

## 🚀 Key Features

* **Vertical tabs** for more intuitive tab management
* **Drag & drop** support for easy tab rearrangement
* **Dark/Light theme** with quick toggle and system preference support
* **Quick Commands** (similar to Cmd+K) for fast access to functions and sites
* **Integrated mini-apps** like notes, to-do list, and calculator for productivity on the go
* **Built-in screenshot tool** to quickly capture page content

---

## 🛠️ Technology

* **Frontend:** Vue.js 3 with Composition API
* **Runtime:** **Electron** (Chromium-based) for full browser support
* **Styling:** Tailwind CSS for modern and responsive design
* **State management:** Pinia
* **Drag & drop:** VueDraggable (Sortable.js)
* **Persistence:** IndexedDB / SQLite (local storage)

---

## 📅 Installation

Make sure you have installed:

* [Node.js](https://nodejs.org/en/) (v16+)
* [Electron](https://www.electronjs.org/) (installed via npm)

Clone the repo:

```bash
git clone https://github.com/yourusername/zyrc-browser.git
cd zyrc-browser
npm install
```

Run the app in development mode:

```bash
npm run dev
```

Build the app for production:

```bash
npm run build
```

---

## 📂 Project Structure

```
/src
  /components     # Reusable Vue components
  /pages          # Pages and layouts
  /stores         # Pinia stores for global state
  /assets         # Images and static resources
/electron         # Electron main process config
```

---

## 🤝 Contributing

Contributions, bug reports, and feature requests are welcome!
Please open an issue or pull request and we’ll get back to you as soon as possible.

---

## 📄 License

MIT License - see the LICENSE file for details.

---

Made with ❤️ by Michael
