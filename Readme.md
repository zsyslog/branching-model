# ESQUEMA DE BRANCHING

![Esquema de branching](https://raw.githubusercontent.com/zsyslog/branching-model/master/modelo-branching.png)

# BRANCH MASTER Y DEVEL

El branch "devel" nace del branch "master". Todas las nuevas funcionalidades nacerán del branch "devel"

```bash
git checkout -b devel master
```
1. <i>Crea el branch devel</i>

# BRANCH PARA NUEVA FUNCIONALIDAD

```bash
git checkout -b nueva_funcionalidad devel
```
1. <i>Crea el branch nueva_funcionalidad</i>

Luego de finalizar la nueva funcionalidad se deben llevar los cambios al branch "devel"

```
git checkout devel
git merge --no-ff nueva_funcionalidad
git branch -d nueva_funcionalidad
git push origin devel
```

<p>1. <i>Cambia al branch devel</i></p>
<p>2. <i>Actualiza sin fast-forward</i></p>
<p>3. <i>Borra el branch "nueva_funcionalidad"</i></p>
<p>4. <i>Actualiza los nuevos cambios en el branch "devel"</i></p>

[1. Branch de nuevo desarrollo](https://github.com/zsyslog/branching-model/blob/master/screencast/01.crear-nueva-funcion-desde-devel.mov?raw=true)

# BRANCH RELEASE

Branch con los cambios listos para producción.
Debe llamarse release-NUMERO_VERSION, donde NUMERO_VERSION es el identificador de la próxima versión que será lanzada. (Ejemplo: release-2.3)
```
git checkout -b release-NUMERO_VERSION devel
```

1. <i>Crea el branch para el nuevo release</i>

Crear un archivo llamado Release-NUMERO_VERSION.txt con el siguiente contenido:

> Versión: NUMERO_VERSION<br>
> Fecha: FECHA_DE_CREACION<br>
> Equipo de trabajo: 
> - developer 1: nombre developer 1
> - developer 2: nombre developer 2
> - developer 3: nombre developer 3
 

```
git add Release-NUMERO_VERSION.txt
git commit -a -m "Inicializando Versión NUMERO_VERSION"
```

1. <i>Incializa la versión NUMERO_VERSION</i>

Liberación de una versión a producción

```
git checkout master
git merge --no-ff release-NUMERO_VERSION
git tag -a NUMERO_VERSION
```

<p>1. <i>Cambia al branch "master"</i></p>
<p>2. <i>Combina los cambios realizados desde el nuevo relase a "master"</i></p>
<p>3. <i>Se numera la versión del release en "master"</i></p>

Además se deben incorporar los cambios a "devel"

```
git checkout devel
git merge --no-ff release-NUMERO_VERSION
```

<p>1. <i>Cambia al branch "devel"</i></p>
<p>2. <i>Realiza el merge</i></p>

Opcional: eliminar el branch del release

```
git branch -d release-NUMERO_VERSION
```

# BRANCHES PARA BUGFIXES

Todos nacen de "master", Una vez realizados los arreglos, deben hacer merge hacia "master" y "devel". Deben llamarse bugfix-NUMERO_VERSION.NUMERO_SECUENCIA_BUG, donde NUMERO_SECUENCIA_BUG es un numero secuencial, identificador del bug (ejemplo: bugfix-2.3.1)

```
git checkout -b bugfix-NUMERO_VERSION.NUMERO_SECUENCIA_BUG master
```

1. <i>Crea el branch bugfix-NUMERO_VERSION.NUMERO_SECUENCIA_BUG</i>

Añade el nombre del bug al archivo Release-NUMERO_VERSION.txt:

> Versión: NUMERO_VERSION<br>
> Fecha: FECHA_DE_CREACION<br>
> Equipo de trabajo: 
> - developer 1: nombre developer 1
> - developer 2: nombre developer 2
> - developer 3: nombre developer 3
> 
> Bugfix NUMERO_VERSION.1: Corrige el bug 1 (esta línea es nueva)

Se incializa la numeración del branch

```
git add Release-NUMERO_VERSION.txt
git commit -a -m "Bugfix NUMERO_VERSION.NUMERO_SECUENCIA_BUG"
```

1. <i>Inicializa la numeración de versión y bug en el branch</i>

Realizar los cambios en uno o mas commits y aplicar el cambio.

```
git commit -m "Corrige el bug [Descripción del bug]" 
git checkout master 
git merge --no-ff bugfix-NUMERO_VERSION.NUMERO_SECUENCIA_BUG 
git tag -a NUMERO_VERSION.NUMERO_SECUENCIA_BUG 
git branch -d bugfix-NUMERO_VERSION.NUMERO_SECUENCIA_BUG 
```

<p>1. <i>Crea el commit</i></p>
<p>2. <i>Cambia al branch "master"</i></p>
<p>3. <i>Realiza el merge de los cambios hacia el branch master</i></p>
<p>4. <i>Se numera la versión del release en "master", que incluye el identificador del bug</i></p>
<p>5. <i>Elimina el branch del bug</i></p>

#Resumen de Videos Screencast
[1. Branch de nuevo desarrollo](https://github.com/zsyslog/branching-model/blob/master/screencast/01.crear-nueva-funcion-desde-devel.mov?raw=true)
<br>
[2. Branch para trabajar en un nuevo release (beta)](https://github.com/zsyslog/branching-model/blob/master/screencast/02.nuevo-release-beta-inicializacion.mov?raw=true)
<br>
[3. Branch para trabajar en un bugfix](https://github.com/zsyslog/branching-model/blob/master/screencast/03.procedimiento-branching-bugfix.mov?raw=true)
<br>