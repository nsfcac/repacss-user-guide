# 🧠 REPACSS User Guide

Welcome to the official documentation repository for the **REPACSS High-Performance Computing (HPC) Cluster** at **Texas Tech University**.

This guide provides comprehensive, organized, and beginner-friendly documentation for users of the REPACSS system — including students, researchers, and faculty across various departments.

---

## 📚 Documentation Contents

This repository powers a structured, searchable documentation site built with **[MkDocs](https://www.mkdocs.org/)** and the **Material for MkDocs** theme. The site is organized into major sections:

- ✅ Getting Started
- 🔐 Connecting to REPACSS
- 🧮 Running Jobs with Slurm
- 💾 Software Management (Spack, Conda, Containers, Trending Applications)
- 🚀 Performance Optimization
- 🛠 Troubleshooting & Reference
- 🧠 Understanding the REPACSS System

Explore the full documentation by visiting the deployed site (coming soon).

Configuration is controlled in [`mkdocs.yml`](mkdocs.yml).

---

## 🚀 Getting Started Locally

You can preview the site locally using MkDocs:

### Prerequisites
- Python 3.8+ installed on your system

### Clone the repository
```bash
git clone https://github.com/nsfcac/repacss-user-guide.git
cd repacss-user-guide
```

### Set up a Python virtual environment
```bash
python -m venv .venv
source .venv/bin/activate  # On Windows, use `.venv\Scripts\activate`
```

### Install dependencies
```bash
pip install -r requirements.txt
```

### Serve the site
```bash
mkdocs serve
```

Visit `http://localhost:8000` to view it.


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

