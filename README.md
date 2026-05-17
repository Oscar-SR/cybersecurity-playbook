# Cybersecurity Playbook

This repository is a collection of knowledge and write-ups about **cyber threat intelligence**, **ethical hacking**, **digital forensics** and **malware analysis**, that can be applied in practical scenarios. It is designed for analysts, researchers, and security professionals, and aims to support real-world investigations, incident response, and strategic decision-making by offering a quick, structured, and continuously updated resource.

The project uses **MkDocs** with the **Material** theme as a web interface for the documentation. This web interface is automatically deployed to GitHub Pages whenever changes are pushed to the main branch.

---

## Install

First, you must ensure that you have `python`installed with one of these commands:

```bash
# Linux/macOS
which python

# Windows (Command Prompt)
where python
```

And also check that `pip` is installed:

```bash
pip --version
```

It is recommended to setup [Python virtual environment](https://realpython.com/what-is-pip/#using-pip-in-a-python-virtual-environment) to avoid conflicts with system packages:

```bash
python -m venv venv
```

And then, you can use one of the following commands to activate the virtual environment:

```bash
# Linux/macOS
source venv/bin/activate

# Windows (Command Prompt)
.\venv\Scripts\activate
```

Now, we can simply install MkDocs Material:

```bash
pip install mkdocs-material
```

## Usage

For running the project locally, use this command:

```bash
mkdocs serve
```

After that, the website will be available at `http://127.0.0.1:8000` by default.
