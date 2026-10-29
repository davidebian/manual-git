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

Este comando recupera la última versión registrada en
