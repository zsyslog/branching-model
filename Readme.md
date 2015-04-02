# BRANCH MASTER Y DEVEL

"devel" nace del branch "master". Todas las nuevas funcionalidades nacen del branch "devel"

> git checkout -b nueva_funcionalidad devel

Luego de finalizar la nueva funcionalidad se deben llevar los cambios al branch "devel"

> git checkout devel // Cambia al branch devel
> git rebase nueva_funcionalidad // Actualiza sin fast-forward
> git branch -d nueva_funcionalidad // borrar el branch "nueva_funcionalidad"
> git push origin devel // Actualiza los nuevos cambios en el branch "devel"

# BRANCH RELEASE

Branch con los cambios listos para producción.
Debe llamarse release-NUMERO_VERSION, donde NUMERO_VERSION es el identificador de la próxima versión que será lanzada. (Ejemplo: release-2.3)

> git checkout -b release-NUMERO_VERSION develop // Crea el branch para el nuevo release

Crear un archivo llamado Release-NUMERO_VERSION.txt con el siguiente contenido:

-----------------------
Versión: NUMERO_VERSION
Fecha: FECHA_DE_CREACION
Equipo de trabajo: 
- developer 1: nombre developer 1
- developer 2: nombre developer 2
- developer 3: nombre developer 3
- developer 4: nombre developer 4
-----------------------

> git commit -a -m "Inicializando Versión NUMERO_VERSION" // incializa la versión NUMERO_VERSION

Liberacióbn de una versión a producción

> git checkout master
Cambia al branch "master"
> git merge --no-ff release-NUMERO_VERSION
Combina los cambios realizados desde el nuevo relase a "master"
> git tag -a NUMERO_VERSION
Se numera la versión del release en "master"

Además se deben incorporar los cambios a "devel"

> git checkout devel // Cambia al branch "devel"
> git merge --no-ff release-NUMERO_VERSION

Opcional: eliminar el branch del release

> git branch -d release-NUMERO_VERSION

# BRANCHES PARA BUGFIXES

Todos nacen de "master", Una vez realizados los arreglos, deben hacer merge hacia "master" y "devel". Deben llamarse bugfix-NUMERO_VERSION.NUMERO_SECUENCIA_BUG, donde NUMERO_SECUENCIA_BUG es un numero secuencial, identificador del bug (ejemplo: bugfix-2.3.1)

> git checkout -b bugfix-NUMERO_VERSION.NUMERO_SECUENCIA_BUG master // creal el branch bugfix-NUMERO_VERSION.NUMERO_SECUENCIA_BUG

Añade el nombre del bug al archivo Release-NUMERO_VERSION.txt:
-----------------------
Versión: NUMERO_VERSION
Fecha: FECHA_DE_CREACION
Equipo de trabajo: 
- developer 1: nombre developer 1
- developer 2: nombre developer 2
- developer 3: nombre developer 3
- developer 4: nombre developer 4
-----------------------
Bugfix NUMERO_VERSION.1: Corrige el bug [Descripción del bug]

Se incializa la numeración del branch

> git commit -a -m "Bugfix NUMERO_VERSION.NUMERO_SECUENCIA_BUG"

realizar los cambios en uno o mas commits y aplicar el cambio.

> git commit -m "Corrige el bug [Descripción del bug]" // Crea el commit
> git checkout master // Cambia al branch "master"
> git merge --no-ff bugfix-NUMERO_VERSION.NUMERO_SECUENCIA_BUG // Realiza el merge de los cambios hacia el branch master
> git tag -a NUMERO_VERSION.NUMERO_SECUENCIA_BUG // se numera la versión del release en "master", que incluye el identificador del bug
> git branch -d hotfix-NUMERO_VERSION.NUMERO_SECUENCIA_BUG // elimina el branch del bug