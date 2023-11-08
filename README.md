D3Engineering

[Documentation](https://squidfunk.github.io/mkdocs-material/)

[Markup examples](https://squidfunk.github.io/mkdocs-material/reference/)

# Add third-level-navigation template to all pages
Example:
```
---
template: third-level-navigation.html
---

# Page title
```

# Run locally
For first time
```python
python -m venv venv
source venv/bin/activate
pip install mkdocs-material
mkdocs serve -f documentation/mkdocs.yml
```
After installation
```python
source venv/bin/activate
mkdocs serve -f documentation/mkdocs.yml
```
