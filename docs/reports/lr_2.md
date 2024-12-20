# Лабораторная работа 2

---

### 1. Создаём новую директорию для темы

``` bash
mkdir custom_theme
cd custom_theme
```

### 2. Создаём корневой файл темы

```bash
touch index.html
```

### 3. Подключаем тему в конфиге

```yml
theme:
  name: mkdocs
  color_mode: auto
  user_color_mode_toggle: true
  custom_dir: 'custom_theme/'
```

### 4. Заполняем коневой файл темы

```html
{% extends "base_template.html" %}

{% block page_title %}
    <title>{{ config.site_name }}</title>
{% endblock %}

{% block custom_styles %}
    {{ parent() }}
    <link rel="stylesheet" href="{{ 'css/custom_style.css'|url }}">
{% endblock %}

{% block search_section %}
    <!-- Search button block intentionally left empty -->
{% endblock %}

{% block navigation_controls %}
    <!-- Next and previous buttons block intentionally left empty -->
{% endblock %}

{% block footer_content %}
    <footer>
        <div>
            <p>
                {{ config.site_author }}<br>
                &copy; {{ config.copyright }}<br>
                {{ config.site_description }}
            </p>
        </div>
    </footer>
{% endblock %}
```

### 5. Создаем css. Добавляем стили

```css
:root {
    --bs-font-sans-serif: "Roboto", sans-serif;
    --bs-primary: #FF5722; /* Deep Orange */
    --bs-primary-rgb: 255, 87, 34;

    --bs-link-color: #607D8B; /* Blue Grey */
    --bs-link-color-rgb: 96, 125, 139;

    --bs-link-hover-color: #455A64; /* Dark Blue Grey */
    --bs-link-hover-color-rgb: 69, 90, 100;
}

:root, [data-bs-theme="light"] {
    --bs-body-bg: #FFFFFF;
    --bs-body-color: #212121;
    --bs-border-color: #E0E0E0;
    --bs-card-bg: #FAFAFA;

    --bs-navbar-bg: #FF7043; /* Lighter Deep Orange */
    --bs-navbar-color: #FFFFFF;
}

[data-bs-theme="dark"] {
    --bs-body-bg: #263238; /* Dark Blue Grey */
    --bs-body-color: #CFD8DC; /* Lighter Blue Grey */
    --bs-border-color: #37474F;
    --bs-card-bg: #37474F;

    --bs-navbar-bg: #D32F2F; /* Darker Red */
    --bs-navbar-color: #FFFFFF;
}

body {
    font-family: var(--bs-font-sans-serif);
    background-color: var(--bs-body-bg);
    color: var(--bs-body-color);
}

a {
    color: var(--bs-link-color);
    text-decoration: none;
}

a:hover, a:focus {
    color: var(--bs-link-hover-color);
    text-decoration: underline;
}

.navbar {
    background-color: var(--bs-navbar-bg);
    color: var(--bs-navbar-color);
    padding: 1rem 2rem;
}

.navbar a {
    color: var(--bs-navbar-color);
}

.navbar a:hover, .navbar a:focus {
    color: var(--bs-link-hover-color);
}

.content-block {
    border: 2px solid var(--bs-border-color);
    background-color: var(--bs-card-bg);
    padding: 20px;
    margin: 15px 0;
    border-radius: 8px;
}

footer {
    font-weight: 300;
    font-size: 0.875rem;
    color: var(--bs-body-color);
    padding: 20px;
    background-color: var(--bs-card-bg);
    text-align: center;
}

footer a {
    color: var(--bs-link-color);
}

footer a:hover {
    color: var(--bs-link-hover-color);
}
```