# Sprint Scikit-learn - Salta, Argentina - Septiembre 2022

Un sprint es un evento donde un conjunto de personas se juntan para contribuir a un proyecto de software. En general, se lleva a cabo a lo largo de un día, en un período de 6 a 8 horas. El objetivo de la actividad depende del perfil de personas al que está dirigido. Si el sprint está dirigido a personas que están comenzando a contribuir a proyectos de código libre, el objetivo es introducirlos en los distintos pasos que deben seguir para comenzar a colaborar en un proyecto. Si el sprint está dirigido a desarrolladores experimentados en el proyecto particular, el objetivo es concentrar sus energías en la solución de una serie de errores o la implementación de nuevas funcionalidades. En este caso, llevaremos a cabo un sprint para personas que están dando sus primeros pasos en el mundo del código abierto.

En el sprint cada persona puede trabajar de forma individual en las partes del proyecto que considere interesante. Pero, cabe destacar que, uno de los aspectos principales de los sprints es su carácter colaborativo. Así, se alienta a los participantes a reunirse de a pares para trabajar. Ésto hace más amena la experiencia del sprint, fomenta la colaboración y permite ampliar la red de contactos de los participantes. Esta forma de trabajar se conoce con el nombre de programación de a pares ("pair programming"). Un enfoque comúnmente utilizado de programación de a pares es la técnica de [conductor-navegador](https://medium.com/@weblab_tech/pair-programming-guide-a76ca43ff389), donde el conductor escribe el código, mientras el navegador observa, verifica o sugiere cambios. A lo largo de la jornada, las personas pueden intercambiar roles a medida que lo sientan necesario. En general, es conveniente que la persona más experimentada sea la que toma el rol de navegadora, mientras la persona que está dando sus primero pasos sea la que maneja el teclado y mouse (conductora). Esto garantiza que ninguno de los miembros del equipo se pierda durante el desarrollo.

El sprint se basará en el proyecto de código abierto [Scikit-learn](https://github.com/scikit-learn/scikit-learn/). Scikit-learn es una librería de aprendizaje automático de código abierto que permite aplicar métodos del aprendizaje supervisado y no supervisado. También proporciona varias herramientas para el ajuste de modelos, preprocesamiento de datos, selección de modelos, evaluación de modelos y muchas otras utilidades.

El sprint contará con la presencia (física y virtual) de desarrolladores del proyecto que brindarán soporte durante el evento, contestando preguntas, ayudando con problemas y revisando los "Pull Requests". Los desarrolladores, previo al sprint, filtrarán "Issues" aptos para personas que están empezando a contribuir. Además, se contará con mentores que no necesariamente son experimentados en el código fuente de Scikit-learn, pero que con sus conocimientos pueden ayudar a resolver problemas con Git u otras herramientas generales como pre-commit, black o pytest. De esta forma, los sprint suelen ser sumamente beneficiosos para los participantes, ya que se reduce sustancialmente el tiempo que uno se encuentra "trabado" con algo (comparado con intentar empezar a colaborar individualmente, sin ayuda).

## Requisitos
Los requisitos para aprovechar el sprint son:
- Tener cuenta de [GitHub](https://github.com/).
- Conocimientos de Python.
- Tener algo de experiencia utilizando Scikit-learn.
- Algo de familiaridad con Git.

## Preparación para el sprint
En caso de ser la primera vez que se contribuye a un proyecto de código libre o si se quiere refrescar algunos conocimientos, recomendamos seguir los siguientes pasos:
- Crear cuenta de [GitHub](https://github.com/).
- Instalar Python. Para configurar el ambiente de desarrollo utilizaremos `conda`, por lo que recomendamos utilizar [miniconda](https://docs.conda.io/en/latest/miniconda.html) para instalar Python y conda (el administrador de paquetes).
- Instalar [Git](https://git-scm.com/).
- Instalar editor de texto (Visual Studio Code, Sublime Text, Atom, PyCharm, o el editor de preferencia).
- Mirar el video ["Scikit-learn sprint instructions"](https://www.youtube.com/watch?v=5OL8XoMMOfA) (30 minutos). [Transcripción del video en español](https://github.com/data-umbrella/data-umbrella-scikit-learn-sprint/blob/master/es/1_transcript_ACM_contributing_sklearn.md). Notar que las instrucciones de instalación han quedado desactualizadas. Para instalar todo lo necesario para contribuir, seguir [esta guía](https://scikit-learn.org/dev/developers/advanced_installation.html) (en ingles).
- Mirar el video ["Contributing to scikit-learn: An Example Pull Request (Reshama Shaikh)"](https://www.youtube.com/watch?v=PU1WyDPGePI) (30 minutos). [Transcripción del video en español](https://github.com/data-umbrella/data-umbrella-scikit-learn-sprint/blob/master/es/2_transcript_RS_example_PR.md).
- Mirar el video ["Sprint Instructions for scikit-learn Vol 2"](https://www.youtube.com/watch?v=p_2Uw2BxdhA) (14 minutos). [Transcripción del video en español](https://github.com/data-umbrella/data-umbrella-scikit-learn-sprint/blob/master/es/3_transcript_ACM_video_vol2.md).
- Mirar el video ["Mariatta Wijaya - Introduction to Sphinx Docs and reStructuredText"](https://www.youtube.com/watch?v=v4eoYpCON_c) (15 minutos).
- [OPCIONAL] Mirar el video ["Sphinx for Python Documentation Tutorial (Melissa Weber)"](https://www.youtube.com/watch?v=tXWscUSYdBs).
- Leer el tutorial ["Step-by-step guide to contributing on GitHub"](https://www.dataschool.io/how-to-contribute-on-github/).

## Clonar repositorio
Pasos para clonar el repositorio:
- Hacer un fork del [proyecto](https://github.com/scikit-learn/scikit-learn) con su usuario.
- Clonar el proyecto con `git clone git@github.com:USER/scikit-learn.git`.
- Dirigirse a la carpeta con `cd scikit-learn`.
- Agregar el repositorio original como repositorio remoto con `git remote add upstream https://github.com/scikit-learn/scikit-learn.git`.

## Configurar ambiente de desarrollo
En la documentación de Scikit-learn se encuentran los pasos para configurar el ambiente de desarrollo para distintos sistemas operativos ([CONTRIBUTING](https://scikit-learn.org/dev/developers/contributing.html#contributing-code), [compilando el código de Scikit-learn](https://scikit-learn.org/dev/developers/advanced_installation.html#building-from-source) y [paquetes necesarios para compilar la documentación](https://scikit-learn.org/stable/developers/contributing.html#documentation)).

En caso de utilizar Linux y `conda`, se pueden seguir los siguiente pasos para configurar el ambiente de desarrollo:
```bash
cd scikit-learn
conda create -n sklearn-dev -c conda-forge python=3.9 numpy scipy matplotlib pytest cython ipykernel jupyter pytest-cov flake8 mypy
conda activate sklearn-dev
pip install black==22.3.0 pre-commit
pip install --no-build-isolation --editable .
pre-commit install

# Para poder compilar la documentación.
pip install sphinx sphinx-gallery numpydoc Pillow pandas scikit-image packaging seaborn sphinx-prompt sphinxext-opengraph
```

### Nota sobre compilación de scikit-learn
Si se modifican archivos Cython (archivos que terminan en `.pyx` o `.pxd`), se tiene que re-compilar:
```bash
pip install --no-build-isolation -e .
```

## Pytest
Para correr test en un archivo particular que hayamos modificado usamos:
```
pytest --verbose ./<path_to_test_folder>/test_file.py
```

## Git/GitHub Workflow
Comandos normalmente utilizados para hacer un Pull Request:
```bash
# Partimos de nuestra rama "main"
git checkout main
# En caso de que nuestro fork no esté actualizado con lo último del repositorio hacemos:
git fetch upstream
git merge upstream main
# Creamos una rama para hacer todos los cambios
git checkout -b my_feature
# Hacemos los cambios para el Pull Request
git add modified_files
# En caso de que no quiera correr el pre-hook usar
# git commit --no-verify -m "Message"
git commit -m "Message"

# Para agregar co-autores a un commit, tenemos que usar
git commit -m "Message
>
>
Co-authored-by: name <name@example.com>
Co-authored-by: another-name <another-name@example.com>"

# Controlar que no hayan cambios del upstream que tengamos que rebasear
# Puede ocurrir que mientras estamos trabajando, nuevos commits entren al repositorio.
# En ese caso, tenemos que hacer un `rebase` para traer los nuevos cambios
# y llevar nuestros commits al final de la historia.

# Primero actualizamos los objetos y referencias del repositorio remoto
git fetch upstream

# En caso de tener miedo de que al realizar la operación, se borre nuestro trabajo
# podemos crear una rama temporal
# git branch tmp my_feature

git rebase upstream/main  # esto puede fallar, en ese caso hacemos lo siguiente
# git rebase --abort
# git reset --hard tmp

# Finalmente, subimos los cambios a nuestro fork
git push origin my_feature

# Si todo salio bien, se puede eliminar el branch temporal
# git branch -D tmp

# Una vez que el pull request es mergeado se puede borrar el branch
git branch -d my_feature
```

## Posibles Issues donde contribuir
Los desarrolladores de Scikit-learn han armado una [lista de Issues](https://github.com/scikit-learn/scikit-learn/issues?q=is%3Aopen+is%3Aissue+label%3ASprint) para trabajar durante el sprint.
La misma contiene Issues de distinta dificultad y en su mayoría pueden ser resueltos en el tiempo del sprint.

## Contacto
- [Scikit-learn Gitter](https://gitter.im/scikit-learn/sprint) (comunicación en inglés)
- Organizador local: [Juan Martin Loyola](mailto:jmloyola@outlook.com)
