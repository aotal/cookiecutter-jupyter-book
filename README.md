# Cookiecutter Jupyter Book Arnau


<p align="center">
  <img src="{{cookiecutter.book_slug}}/data/img/logo.png" width="400">
</p>

Una plantilla de cookiecutter para crear un sencillo [Jupyter Book](https://jupyterbook.org/intro.html).

## Template

Ejemplo del arbol de directorios del proyecto. Los ficheros necesarios se ponen dentro de la carpeta de data y a su vez los de imagen en /data/img:

```
my_book
├── .github
│   └── workflows
│       └── deploy.yml
├── CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE
├── my_book
│   ├── _config.yml
│   ├── _toc.yml
│   ├── content.md
│   ├── intro.md
│   ├── markdown.md
│   ├── notebooks.ipynb
│   ├── references.bib
│   ├── data
│       ├──img
│          ├──logo.png
│          ├──favicon.png
│   
├── README.md
└── requirements.txt
```

## Usage

1. Instalar [Cookiecutter](https://github.com/cookiecutter/cookiecutter/tree/1.7.2) antes de crear el primer libro:

```bash
$ pip install -U cookiecutter
```
También es necesario que jupyter-book esté instalado a su vez

2. Usar `cookiecutter-jupyter-book` para generar el libro (los valores por defecto se muestran entre corchetes `[]`):

```bash
$ cookiecutter https://github.com/aotal/cookiecutter-jupyter-book.git

author_name [Captain Jupyter]: Tomas Beuzen
github_or_gitlab_username [tomasbeuzen]:
book_name [My Book]:
book_slug [my_book]:
Breve descripción del libro [Este proyecto crea un jupyter-book simple.]: My first Jupyter Book!
version ['0.1.0']:
Seleccionar licencia:
1 - MIT license
2 - BSD license
3 - ISC license
4 - Apache Software License 2.0
5 - GNU General Public License v3
6 - None
Choose from 1, 2, 3, 4, 5, 6 [1]:
Select include_ci_files:
1 - github
2 - gitlab
3 - no
Choose from 1, 2, 3 [1]:
```

3. Instalar las librerías necesarias para el proyecto incluídas en el fichero `requirements.txt`. Se recomienda hacerlo dentro de un entorno virtual. e.g., using [conda](https://docs.conda.io/en/latest/)):

```bash
# pasos para crear en entorno virtual
$ conda create --name mybook python=3.8 -y
$ conda activate mybook
```

```bash
$ cd my_book
$ pip install -r requirements.txt
```

4. Compilar el libro para crear los html:

```bash
$ cd ..
$ jupyter-book build my_book/
```

5. Chequear el libro en `my_book/_build/html/index.html`.

6. Añadir más contenido añadiendo ficheros y actualizando el índice de contenidos en  `my_book/_toc.yml`, y/o editando el fichero de configuración `my_book/_config.yml`. Ver [Jupyter Book documentation](https://jupyterbook.org/intro.html) para más información sobre configurar el libro.

7. `cookiecutter-jupyter-book` viene preparado para publicar los archivos on-line. Un fichero de  flujo de trabajo CI (Continous integration) puede incluirse si se elige `1 - github` o `2 - gitlab` para `Select include_ci_files:` en el paso 2. por ejemplo, eligiendo `1 - github`, y cuando el libro está listo para publicarlo on-line:
   1. Hay que asegurarse de que el libro se ha compilado bien (`jupyter-book build my_book/`) y que se han instalado las librerías necesarias incluídas en el fichero `requirements.txt` para compilar correctamente el libro;
   2.  En necesario crear un repositorio público [GitHub repository](https://github.com/new) para alojar el libro;
   3. "Push" la copia local del libro (incluyendo el directorio oculto `.github`) al repositorio de GitHub. Hay varias maneras de hacerlo. Un ejemplo sería:

      ```bash
      $ git init
      $ git add .
      $ git commit -m "first commit"
      $ git branch -M main
      $ git remote add origin git@github.com:<user>/<repository-name>.git
      $ git push -u origin main
      ```

   4. Los comandos incluídos mediante cookiecutter (`my_book/.github/workflows/deploy.yml`) publicarán automatiamente el libro en `gh-pages`en la rama correspondiente una vez "pushed". Estará disponible en la dirección `https://<user>.github.io/<myonlinebook>/` después de unos minutos. puede ser necesario ir a `Settings` en el repositorio y bajo la cabecera **GitHub Pages** , elegir `gh-pages branch` desde la lista desplegable**Source**. para ver otros métodos de publicación consultar [Jupyter Book documentation](https://jupyterbook.org/intro.html).

   > Note: by default, the GitHub Actions workflow file included with this cookiecutter builds the book with Ubuntu and Python 3.8. You can modify the OS/Python version for the build in the `.github/workflows/deploy.yml` file on lines 15 and 16 respectively.

   > Ver información adicional sobre GitHub pages [aquí](https://jupyterbook.org/publish/gh-pages.html#automatically-host-your-book-with-github-actions), o usando GitLab [aquí](https://docs.gitlab.com/ee/user/project/pages/getting_started/pages_from_scratch.html).