# Curso básico de Git y GitHub

**Autor:** David Tubío González  
**Entorno:** Debian GNU/Linux  
**Herramientas:** Git y GitHub  
**Nivel:** Iniciación

---

# Índice

1. Introducción a Git
2. Diferencias entre Git y GitHub
3. Instalación de Git
4. Configuración inicial
5. Conceptos fundamentales
6. Creación de un repositorio
7. Gestión de archivos
8. Área de preparación (Staging Area)
9. Commits e historial
10. Ramas (Branches)
11. Fusionar ramas (Merge)
12. Deshacer cambios
13. Repositorios remotos
14. Subir proyectos a GitHub
15. Clonar repositorios
16. Actualizar repositorios
17. Archivo .gitignore
18. Buenas prácticas
19. Comandos esenciales
20. Ejercicio práctico final

---

# 1. Introducción a Git

Git es un sistema de control de versiones distribuido que permite registrar los cambios realizados en los archivos de un proyecto.

Su principal utilidad es mantener un historial de modificaciones, permitiendo recuperar versiones anteriores, comparar cambios y trabajar simultáneamente con otras personas.

Git es especialmente utilizado en el desarrollo de software, administración de sistemas y proyectos de documentación técnica.

### Ventajas de Git

- Permite mantener un historial de versiones.
- Facilita la recuperación de archivos anteriores.
- Permite trabajar con diferentes ramas.
- Facilita el trabajo colaborativo.
- Permite conocer quién realizó cada modificación.
- Funciona localmente sin necesidad de conexión a Internet.

# 2. Diferencias entre Git y GitHub

Aunque suelen utilizarse conjuntamente, son herramientas diferentes.

| Git | GitHub |
|---|---|
| Sistema de control de versiones. | Plataforma de alojamiento de repositorios. |
| Se instala en el ordenador. | Se utiliza principalmente desde Internet. |
| Gestiona versiones y cambios. | Permite compartir proyectos. |
| Funciona sin conexión. | Necesita conexión para sincronizar. |

GitHub permite alojar repositorios Git y facilita el trabajo colaborativo mediante herramientas como Pull Requests, Issues y revisiones de código.

Web oficial: [https://github.com](https://github.com)

# 3. Instalación de Git

En Debian podemos instalar Git utilizando el gestor de paquetes APT.

Actualizamos los repositorios:

```bash
sudo apt update
```

Instalamos Git:

```bash
sudo apt install git
```

Comprobamos la versión instalada:

```bash
git --version
```

# 4. Configuración inicial

Antes de empezar a utilizar Git debemos configurar nuestra identidad.

Establecemos el nombre:

```bash
git config --global user.name "David Tubío González"
```

Configuramos el correo electrónico:

```bash
git config --global user.email "correo@ejemplo.com"
```

Configuramos el nombre predeterminado de la rama inicial:

```bash
git config --global init.defaultBranch main
```

Consultamos la configuración:

```bash
git config --list
```

El parámetro `--global` indica que la configuración se aplicará a todos los repositorios del usuario.

# 5. Conceptos fundamentales

Git trabaja con diferentes estados y áreas que debemos conocer.

### Working Directory

Es el directorio de trabajo donde se encuentran los archivos del proyecto y donde realizamos las modificaciones.

### Staging Area

Es el área de preparación donde seleccionamos los cambios que queremos incluir en el siguiente commit.

### Local Repository

Es el repositorio local donde Git almacena el historial de versiones y los commits.

### Remote Repository

Es un repositorio alojado en un servidor remoto, como GitHub.

### Flujo de trabajo

```text
Working Directory
       |
       | git add
       v
  Staging Area
       |
       | git commit
       v
 Local Repository
       |
       | git push
       v
Remote Repository
     (GitHub)
```

# 6. Creación de un repositorio

Para crear un proyecto nuevo primero creamos su directorio:

```bash
mkdir curso-git
```

Accedemos al directorio:

```bash
cd curso-git
```

Inicializamos el repositorio:

```bash
git init
```

Git crea un directorio oculto llamado `.git` donde almacena toda la información necesaria para gestionar el proyecto.

Comprobamos su contenido:

```bash
ls -la
```

Podemos consultar el estado del repositorio:

```bash
git status
```

Para cambiar el nombre de la rama inicial a `main`:

```bash
git branch -m main
```

# 7. Gestión de archivos

Git permite realizar el seguimiento de los archivos de un proyecto.

Creamos un archivo:

```bash
nano README.md
```

Podemos introducir un contenido inicial:

```markdown
# Mi proyecto Git

Este es mi primer repositorio.
```

Guardamos el archivo y consultamos el estado:

```bash
git status
```

Git mostrará el archivo como `untracked`, es decir, todavía no está incluido en el seguimiento del repositorio.

# 8. Área de preparación (Staging Area)

Para indicar a Git qué archivos queremos incluir en el siguiente commit utilizamos `git add`.

Añadir un archivo concreto:

```bash
git add README.md
```

Añadir todos los archivos modificados y nuevos del directorio actual:

```bash
git add .
```

Comprobamos el estado:

```bash
git status
```

Ahora el archivo aparecerá como preparado para realizar un commit.

Para retirar un archivo del área de preparación sin eliminarlo del directorio de trabajo:

```bash
git restore --staged README.md
```

# 9. Commits e historial

Un commit es una instantánea de los cambios preparados en un momento determinado.

Para crear un commit:

```bash
git commit -m "Primer commit"
```

El parámetro `-m` permite añadir un mensaje que describe los cambios realizados.

Consultar el historial:

```bash
git log
```

Consultar el historial de forma resumida:

```bash
git log --oneline
```

Consultar los cambios entre versiones:

```bash
git diff
```

Consultar los cambios preparados para el siguiente commit:

```bash
git diff --staged
```

Es recomendable utilizar mensajes de commit claros y descriptivos.

Ejemplos:

```text
Añadir documentación inicial
Corregir errores en README
Actualizar configuración del proyecto
Añadir script de instalación
```

# 10. Ramas (Branches)

Las ramas permiten desarrollar nuevas funcionalidades o realizar modificaciones sin alterar directamente la rama principal.

La rama principal suele llamarse `main`.

Consultar las ramas existentes:

```bash
git branch
```

Crear una nueva rama:

```bash
git branch desarrollo
```

Cambiar a otra rama:

```bash
git switch desarrollo
```

Crear una rama y cambiar a ella directamente:

```bash
git switch -c nueva-funcionalidad
```

Volver a la rama principal:

```bash
git switch main
```

Eliminar una rama local:

```bash
git branch -d desarrollo
```

# 11. Fusionar ramas (Merge)

Cuando terminamos el trabajo de una rama podemos integrar sus cambios en otra.

Por ejemplo, queremos fusionar la rama `desarrollo` con `main`.

Primero cambiamos a la rama principal:

```bash
git switch main
```

Realizamos la fusión:

```bash
git merge desarrollo
```

Si no existen conflictos, Git integrará los cambios.

### Conflictos de fusión

Un conflicto aparece cuando Git no puede integrar automáticamente determinados cambios.

Debemos editar los archivos afectados, resolver las diferencias y después ejecutar:

```bash
git add archivo-modificado
git commit -m "Resolver conflicto de fusion"
```

# 12. Deshacer cambios

Git dispone de diferentes comandos para recuperar versiones o descartar modificaciones.

### Descartar cambios de un archivo no preparado

```bash
git restore README.md
```

Este comando recupera la última versión registrada en el repositorio. Los cambios no guardados se perderán.

### Retirar archivos del área de preparación

```bash
git restore --staged README.md
```

### Consultar el historial

```bash
git log --oneline
```

### Revertir un commit

```bash
git revert ID_DEL_COMMIT
```

Este comando crea un nuevo commit que deshace los cambios de otro commit, conservando el historial.

### Recuperar un commit anterior con reset

```bash
git reset --soft HEAD~1
```

Deshace el último commit, pero conserva los cambios preparados.

```bash
git reset --mixed HEAD~1
```

Deshace el último commit y deja los cambios en el directorio de trabajo sin preparar.

```bash
git reset --hard HEAD~1
```

Deshace el último commit y descarta los cambios correspondientes. Debe utilizarse con precaución.

# 13. Repositorios remotos

Un repositorio remoto es una copia del proyecto alojada en otro servidor.

Para consultar los repositorios remotos configurados:

```bash
git remote -v
```

Para añadir un repositorio remoto:

```bash
git remote add origin https://github.com/usuario/proyecto.git
```

`origin` es el nombre convencional que se utiliza para identificar el repositorio remoto principal.

Para cambiar su dirección:

```bash
git remote set-url origin NUEVA_URL
```

# 14. Subir proyectos a GitHub

Para publicar un proyecto local en GitHub debemos crear primero un repositorio vacío desde la plataforma.

Una vez creado, copiamos su dirección HTTPS.

Configuramos el repositorio remoto:

```bash
git remote add origin https://github.com/usuario/proyecto.git
```

Establecemos el nombre de la rama principal:

```bash
git branch -M main
```

Subimos el contenido:

```bash
git push -u origin main
```

El parámetro `-u` establece la rama remota de seguimiento. Así, en los siguientes envíos podremos utilizar simplemente:

```bash
git push
```

### Autenticación

GitHub no permite utilizar la contraseña habitual de la cuenta para operaciones Git mediante HTTPS.

Podemos utilizar:

- Personal Access Token (PAT).
- SSH mediante claves públicas y privadas.
- Un gestor de credenciales compatible.

Documentación oficial: [https://docs.github.com](https://docs.github.com)

# 15. Clonar repositorios

Clonar permite descargar una copia completa de un repositorio remoto.

```bash
git clone https://github.com/usuario/proyecto.git
```

Git creará automáticamente un directorio con el contenido del proyecto y su historial.

Para clonar en un directorio con un nombre diferente:

```bash
git clone https://github.com/usuario/proyecto.git mi-proyecto
```

# 16. Actualizar repositorios

Cuando trabajamos con un repositorio remoto es necesario sincronizar los cambios.

### Descargar e integrar cambios

```bash
git pull
```

Este comando descarga los cambios remotos y los integra en la rama actual.

### Descargar cambios sin integrarlos

```bash
git fetch
```

`git fetch` actualiza las referencias remotas, pero no modifica directamente nuestra rama de trabajo.

### Enviar cambios al repositorio remoto

```bash
git push
```

Es importante actualizar el repositorio antes de trabajar cuando otras personas también realizan modificaciones.

# 17. Archivo .gitignore

El archivo `.gitignore` permite indicar qué archivos o directorios no queremos que Git incluya en el seguimiento.

Creamos el archivo:

```bash
nano .gitignore
```

Ejemplo de contenido:

```gitignore
# Archivos temporales
*.tmp
*.log

# Directorios de configuración de editores
.vscode/
.idea/

# Archivos de sistema
.DS_Store
Thumbs.db

# Entornos virtuales de Python
venv/
__pycache__/

# Archivos de configuración sensibles
.env
```

De esta forma Git ignorará los archivos que coincidan con estos patrones, siempre que todavía no estén siendo seguidos.

**Importante:** `.gitignore` no elimina archivos que ya están versionados.

# 18. Buenas prácticas

Para trabajar correctamente con Git es recomendable seguir algunas pautas:

- Realizar commits pequeños y frecuentes.
- Utilizar mensajes descriptivos.
- No incluir contraseñas ni credenciales en los repositorios.
- Utilizar ramas para desarrollar nuevas funcionalidades.
- Comprobar los cambios antes de realizar un commit.
- Mantener actualizado el repositorio remoto.
- Utilizar `.gitignore` para excluir archivos innecesarios.
- Evitar utilizar `git reset --hard` sin comprobar previamente sus consecuencias.

# 19. Comandos esenciales

| Comando | Función |
|---|---|
| `git init` | Inicializa un repositorio. |
| `git clone` | Clona un repositorio remoto. |
| `git status` | Consulta el estado del repositorio. |
| `git add` | Añade archivos al área de preparación. |
| `git commit` | Registra una nueva versión. |
| `git log` | Consulta el historial. |
| `git diff` | Muestra diferencias entre cambios. |
| `git branch` | Consulta y gestiona ramas. |
| `git switch` | Cambia de rama. |
| `git merge` | Fusiona ramas. |
| `git restore` | Recupera archivos. |
| `git revert` | Deshace cambios mediante un nuevo commit. |
| `git remote` | Gestiona repositorios remotos. |
| `git push` | Envía cambios al remoto. |
| `git pull` | Descarga e integra cambios. |
| `git fetch` | Descarga referencias remotas. |

# 20. Ejercicio práctico final

Vamos a realizar un ejercicio que reúne los conceptos principales del curso.

### Paso 1. Crear el repositorio

```bash
mkdir practica-final
cd practica-final
git init
```

### Paso 2. Crear un archivo README

```bash
nano README.md
```

Introducimos:

```markdown
# Proyecto de prácticas

Repositorio para aprender Git y GitHub.
```

### Paso 3. Preparar y registrar los cambios

```bash
git add README.md
git commit -m "Crear documentación inicial"
```

### Paso 4. Modificar el archivo

Añadimos una nueva línea al README y guardamos.

```bash
nano README.md
```

Registramos los cambios:

```bash
git add README.md
git commit -m "Actualizar documentación"
```

### Paso 5. Crear una rama

```bash
git switch -c desarrollo
```

Creamos un nuevo archivo:

```bash
nano notas.txt
```

Añadimos contenido y registramos el cambio:

```bash
git add notas.txt
git commit -m "Añadir notas de desarrollo"
```

### Paso 6. Fusionar los cambios

Volvemos a la rama principal:

```bash
git switch main
```

Fusionamos la rama de desarrollo:

```bash
git merge desarrollo
```

### Paso 7. Consultar el resultado

```bash
git status
git log --oneline --graph --all
```

### Paso 8. Publicar en GitHub

Creamos un repositorio vacío en GitHub y conectamos nuestro repositorio local:

```bash
git remote add origin https://github.com/usuario/practica-final.git
git push -u origin main
```

Comprobamos que el proyecto aparece correctamente en GitHub.

---

# Recursos de aprendizaje

- [Documentación oficial de Git](https://git-scm.com/doc)
- [Libro oficial Pro Git](https://git-scm.com/book/es/v2)
- [Documentación de GitHub](https://docs.github.com/es)
- [GitHub Skills](https://skills.github.com/)

---

**Fin del curso básico de Git y GitHub.**

Material de aprendizaje elaborado para practicar el control de versiones en entornos GNU/Linux.
