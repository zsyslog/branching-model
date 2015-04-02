# BRANCH MASTER Y DEVEL

El branch "devel" nace del branch "master". Todas las nuevas funcionalidades nacerán del branch "devel"
```bash
git checkout -b nueva_funcionalidad devel
```
> Crea el branch devel

Luego de finalizar la nueva funcionalidad se deben llevar los cambios al branch "devel"

```
git checkout devel
git merge --no-ff nueva_funcionalidad
git branch -d nueva_funcionalidad
git push origin devel
```

<p>
	hola
</p>
> 1. Cambia al branch devel
> 2. Actualiza sin fast-forward
> 3. Borra el branch "nueva_funcionalidad"
> 4. Actualiza los nuevos cambios en el branch "devel"

# BRANCH RELEASE

Branch con los cambios listos para producción.
Debe llamarse release-NUMERO_VERSION, donde NUMERO_VERSION es el identificador de la próxima versión que será lanzada. (Ejemplo: release-2.3)
```
git checkout -b release-NUMERO_VERSION devel
```
> Crea el branch para el nuevo release

Crear un archivo llamado Release-NUMERO_VERSION.txt con el siguiente contenido:

> 
> Versión: NUMERO_VERSION
> Fecha: FECHA_DE_CREACION
> Equipo de trabajo: 
> - developer 1: nombre developer 1
> - developer 2: nombre developer 2
> - developer 3: nombre developer 3
 

```
git commit -a -m "Inicializando Versión NUMERO_VERSION"
```

> Incializa la versión NUMERO_VERSION

Liberación de una versión a producción

```
git checkout master
git merge --no-ff release-NUMERO_VERSION
git tag -a NUMERO_VERSION
```

> 1. Cambia al branch "master"
> 2. Combina los cambios realizados desde el nuevo relase a "master"
> 3. Se numera la versión del release en "master"

Además se deben incorporar los cambios a "devel"

```
git checkout devel
git merge --no-ff release-NUMERO_VERSION
```

> 1. Cambia al branch "devel"
> 2. Realiza el merge

Opcional: eliminar el branch del release

```
git branch -d release-NUMERO_VERSION
```

# BRANCHES PARA BUGFIXES

Todos nacen de "master", Una vez realizados los arreglos, deben hacer merge hacia "master" y "devel". Deben llamarse bugfix-NUMERO_VERSION.NUMERO_SECUENCIA_BUG, donde NUMERO_SECUENCIA_BUG es un numero secuencial, identificador del bug (ejemplo: bugfix-2.3.1)

```
git checkout -b bugfix-NUMERO_VERSION.NUMERO_SECUENCIA_BUG master
```

> Crea el branch bugfix-NUMERO_VERSION.NUMERO_SECUENCIA_BUG

Añade el nombre del bug al archivo Release-NUMERO_VERSION.txt:

> 
> Versión: NUMERO_VERSION
> Fecha: FECHA_DE_CREACION
> Equipo de trabajo: 
> - developer 1: nombre developer 1
> - developer 2: nombre developer 2
> - developer 3: nombre developer 3
> 
> Bugfix NUMERO_VERSION.1: Corrige el bug 1 (esta línea es nueva)

Se incializa la numeración del branch

```
git commit -a -m "Bugfix NUMERO_VERSION.NUMERO_SECUENCIA_BUG"
```

> Inicializa la numeración de versión y bug en el branch

Realizar los cambios en uno o mas commits y aplicar el cambio.

```
git commit -m "Corrige el bug [Descripción del bug]" 
git checkout master 
git merge --no-ff bugfix-NUMERO_VERSION.NUMERO_SECUENCIA_BUG 
git tag -a NUMERO_VERSION.NUMERO_SECUENCIA_BUG 
git branch -d hotfix-NUMERO_VERSION.NUMERO_SECUENCIA_BUG 
```

> 1. Crea el commit
> 2. Cambia al branch "master"
> 3. Realiza el merge de los cambios hacia el branch master
> 4. Se numera la versión del release en "master", que incluye el identificador del bug
> 5. Elimina el branch del bug