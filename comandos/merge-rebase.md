# MERGE Y REBASE

<p>Regla</p>
<ul>
	<li>Cuando se lleven cambios desde origin/devel hacia el desarrollo local, usar rebase</li>
	<li>Cuando se finalicen cambios de una nueva funcionalidad (o bugfix) usar merge hacia el remoto</li>
</ul>


rebase
------
Herramienta para unir branches, reproduce los cambios que consolidamos uno a uno en nuestra rama de trabajo y los lleva a la rama a donde queremos unirlos
No usar "rebase" posterior a la realización de un "git push" o sobre "commits" que ya se encuentren en el repositorio remoto.

```
git pull --rebase origin BRANCH
```

Se obtendrá un historial lineal en el desarrollo local con los cambios realizados por el equipo.

merge
-----
Herramienta para unir branches. Conserva el historial no lineal

```
git checkout master
git merge BRANCH
```

