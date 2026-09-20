# Portafolio (Hugo + CleanWhite)

Sitio personal hecho con Hugo y el tema [CleanWhite](https://themes.gohugo.io/themes/hugo-theme-cleanwhite/), desplegado en GitHub Pages.

## Requisitos

- **Hugo Extended 0.146 o posterior** (probado con 0.166.0). El tema usa la estructura de plantillas nueva (`_partials`, `_shortcodes`, `home.html`), que Hugo 0.117 no reconoce. Para actualizar, desde un PowerShell de administrador: `choco upgrade hugo-extended -y`, y comprueba con `hugo version`.
- Git.

## Primera vez en tu equipo

El tema se instala como submódulo de Git (no está copiado en este repositorio):

```powershell
cd C:\Hugo\portafolio
git init -b main
git submodule add https://github.com/zhaohuabing/hugo-theme-cleanwhite.git themes/hugo-theme-cleanwhite
hugo server -D      # vista previa en http://localhost:1313
```

Si clonas el repositorio en otro equipo: `git clone --recurse-submodules URL`.

## Estructura

- `hugo.toml`: configuración del sitio y del tema (título, menú, redes sociales, barra lateral).
- `content/post/`: publicaciones. Cada una lleva una categoría (`Proyectos`, `Notas`, ...) y las categorías aparecen solas en el menú superior.
- `content/acerca/`, `content/archive/`, `content/search/`: páginas fijas (Acerca de, Archivo, Búsqueda). No borres `content/search/`: la lupa del menú apunta ahí.
- `static/img/home-bg.jpg`: imagen de cabecera. Puedes reemplazarla por otra (el nombre se define en `params.header_image`).
- `archetypes/post.md`: plantilla para publicaciones nuevas.
- `.github/workflows/hugo.yml`: compila, genera el índice de búsqueda y publica en GitHub Pages en cada push a `main`.

No agregues una carpeta `layouts/` en la raíz a menos que quieras sobrescribir algo del tema: lo que esté ahí tiene prioridad sobre el tema.

## Escribir una publicación

```powershell
hugo new post/mi-proyecto.md
```

Edita el archivo generado (título, subtítulo, categorías, etiquetas), quita `draft: true` y guarda. Con `<!--more-->` defines hasta dónde llega el resumen que se ve en el inicio.

## Búsqueda

La búsqueda usa [Pagefind](https://pagefind.app/), que indexa el sitio ya compilado. En GitHub se genera automáticamente. Para probarla en local:

```powershell
hugo --minify
npx -y pagefind --site public --output-subdir _pagefind
```

Con `hugo server` la lupa no devuelve resultados, porque ahí no existe el índice.

## Publicar en GitHub

1. Crea un repositorio vacío en GitHub. Lo más simple es llamarlo `TU-USUARIO.github.io`: así la URL es `https://TU-USUARIO.github.io/` y la búsqueda funciona (el tema carga sus archivos desde la raíz del dominio).
2. Desde la carpeta del proyecto:

   ```powershell
   git add .
   git commit -m "Sitio inicial con CleanWhite"
   git remote add origin https://github.com/TU-USUARIO/TU-USUARIO.github.io.git
   git push -u origin main
   ```

3. En GitHub: Settings > Pages > Source: **GitHub Actions**.
4. Cada push a `main` publica el sitio.

## Cosas que conviene saber del tema

- Algunas etiquetas de la interfaz están en inglés en el propio tema (menú "All Posts", "Posted by ...", "Catalog"). Cambiarlas implica sobrescribir esas plantillas en una carpeta `layouts/` propia.
- Al compilar con Hugo 0.158 o posterior aparece un aviso de la plantilla base del tema (`.Site.LanguageCode`). Es del tema, no de este proyecto, y no afecta el resultado.
- El pie de página carga una librería pequeña (FastClick) desde `cdn.jsdelivr.net`.
- `upstreamAttribution = false` oculta el crédito del tema y un botón de GitHub de un tercero en el pie. Si quieres acreditar al autor, ponlo en `true`.
