# 🧠 REPACSS User Guide

Welcome to the official documentation repository for the **REPACSS High-Performance Computing (HPC) Cluster** at **Texas Tech University**.

This guide provides comprehensive, organized, and beginner-friendly documentation for users of the REPACSS system — including students, researchers, and faculty across various departments.

---

## 📚 Documentation Contents

This repository powers a structured, searchable documentation site built with **[MkDocs](https://www.mkdocs.org/)** and the **Material for MkDocs** theme. The site is organized into major sections:

- ✅ Getting Started
- 🔐 Connecting to REPACSS
- 🧮 Running Jobs with Slurm
- 💾 Software & Modules
- 🚀 Performance Optimization
- 🛠 Troubleshooting & Reference
- 🧠 Understanding the REPACSS System

Explore the full documentation by visiting the deployed site (coming soon).

---

## 📦 Project Structure

```
📁 docs/
├── index.md
├── getting-started-at-REPACSS.md
├── account/
├── connecting/
├── running-jobs/
├── software/
├── performance/
├── reference/
├── understanding/
├── assets/
│   └── stylesheets/
│       └── extra.css
└── unix-permissions.md
```

Configuration is controlled in [`mkdocs.yml`](mkdocs.yml).

---

## 🚀 Getting Started Locally

You can preview the site locally using MkDocs:

### Install MkDocs (with Homebrew)
```bash
brew install mkdocs
```

### Clone and Serve
```bash
git clone https://github.com/TalkingJupiter/repacss-user-guide.git
cd repacss-user-guide
mkdocs serve
```

Visit `http://localhost:8000` to view it.

> ℹ️ Note: You can also install the Material theme with `pip install mkdocs-material`.

---

## 🌐 Deployment

This site can be deployed using GitHub Pages or any static site host.

To build static files:

```bash
mkdocs build
```

To deploy using `gh-pages`:

```bash
mkdocs gh-deploy
```

---

## 🤝 Contributing

We welcome contributions! If you’d like to:

- Fix a typo
- Add a new section
- Improve examples or formatting

Feel free to [open a pull request](https://github.com/nsfcac/repacss-user-guide/pulls) or file an issue.

---

## 📜 License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

