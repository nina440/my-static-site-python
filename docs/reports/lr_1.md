# Лабораторная работа 1

---

### 1. Проверка версии pyhton

Установлен в системе по умолчанию.

```bash
python3 --version
```

> `Python 3.12.3`

### 2. Установка virtualenv

```bash
python3 -m pip install --user virtualenv
```

### 3. Создаём и активируем venv

``` bash
mkdir my-static-site-python
cd my-static-site-python
```

```bash
virtualenv venv
```

```bash
source venv/bin/activate
```

### 4. Устанавливаем MkDocs

```bash
pip install mkdocs
```

### 5. Генерируем проект

```bash
mkdocs new ./
```

### 6. Редактируем конфиг

Файл `mkdocs.yml`.

```yml
site_name: My Static Site
site_author: Budzinskaya Nina

theme:
  name: mkdocs
  color_mode: auto
  user_color_mode_toggle: true
  custom_dir: 'custom_theme/'
```

### 7. Редактируем содержимое

Файл `docs/index.md`.

```md
# Главная

Добро пожаловать
Это мой статический сайт, созданный с использованием MkDocs.

```

### 8. Загружаем на GitHub

### 9. Создаём Action для сборки

Файл `.github/workflows/mkdocs.yml`.

```yml
name: Deploy MkDocs to GitHub Pages

on:
  push:
    branches:
      - main
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: windows-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: 3.12

      - name: Install MkDocs
        run: pip install mkdocs

      - name: Build site with MkDocs
        run: mkdocs build

      - name: Upload artifact for Pages deployment
        uses: actions/upload-pages-artifact@v3
        with:
          path: 'site/'

      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### 10. Результат

После успешного выполнения сценария получаем сайт по адресу [https://nina440.github.io/my-static-site-python/]