# Curso de Git y Github

## Comandos Generales
`pwd`: Para ver donde estoy en la consola   
`ls -s`: Listar carpetas   
`git config -l` : Ver configuración   
`git config --global user.mail "correo"` : Actualizar correo electronico
`git config --global --unser user.mailo` : Para borrar parametro mal ingresado
`git remote -v`: Ver url remota
`git commit -am ""` 
`history` : Muestra el listado de comandos utilizados.   
`ESC+ SHIFT+ZZ` : Volver a la consola git.   

## Comandos Llaves SSH en local
`ssh -keygen -t rsa -b 4096 -c "correo"`: 
- Crear llave
- Despues ingresar ruta
- Ingresar contraseña con espacios
- Queda en carpeta .ssh/id_rsa

`eval $(ssh-agent-s)` : Ver si esta corriendo el proceso
`ssh-add /.ssh/id_rsa` : Para agregar llave al servidor
`git remote set-url origin "ruta repo ssh"`: Cambiar url del repositorio remoto

## Tags y Versiones
`git log`   
`git log --all`   
`git log --all --graph`   
`git log --all --graph --decorate --oneline`   
`alias arbolito = "git log --all --graph --decorate --oneline"`   
`arbolito`

### Creación de tags    
`git tag -a "nombre" -m "comentario" (v0.1) "hash"`    
`git tag` : Ver listado de tags   
`git show-ref --tags` : Muestra a que hash esta relacionado el tag   
Despues de crear un tag es necesario hacer un pull y un push : `git push origin --tags`   

### Borrar tags    
`git tag -d "nombre tag"`: Al borrar hay qye hacer push de los tags.    
`git push origin :refs/tags/"nombre_tag"` : Borrar tag en remoto.    

##  Manejo de ramas
`git checkout "cabecera"`: Cambia a la rama con nombre "Cabecera"    
`git branch`: ver ramas   
`git show-branch`: ver ramas y su historia   
`git push origin cabecera`: Subir rama al remoto   

##  Multiples colaboradores en GitHub
`git clone "URL"`: Descarga proyecto publico.   
En settings del repositorio se pueden agregar colaboradores por correo o por nombre de usuario.

###  Flujo de Trabajo   
`git config --global alias arbolito "log --graph --decorate"` : Creando un alias como comando de git.   
`git arbolito` : Para llamrlo como comando de git.   
`git merge "header"` : Haciendo un merge desde Master con header.   

###  Pull request   
Funcionalidad de github(en gitlab se llama Merge Request y Bitbucket push request) en la que un colaborador pide que revisen sus cambios antes de hacer merge a una rama, normalmente master.   
Al hacer un pull request se genera una conversación que pueden seguir los demas usuarios del repositorio, asi como autorizar los cambios.   
El flujo es el siguiente:    
* Se trabaja en una rama paralela los cambios que se desean (`git checkout -b "rama"`)   
* Se hace un commit a la rama (`git commit -am "comentario"`)   
* Se suban al remoto los cambios (`git push origin "rama"`)   
* En github se hace el pull reques comparando la rama master con la rama de fix.   
* Uno o varios colaboradores revisan que el codigo sea correcto y dan el feedback (en el chat del pull request)   
* El colaborador hace los cambios que desea en la rama y vuelve a subir al remoto (automaticamente toma la historia de los cambios que se hagan en la rama al remoto)   
* Se aceptan los cambios en Github.   
* Se hace el merge al master desde Github.   

###  Creando un Fork   
O bifurcación es una caracteristica unica de Github en la que se crea una copia exacta del estado actual de un repositorio directamente en Github, este repositorio podra servir como otro origen y se podrá clonar (como cualquier otro repositorio).   
un fork es como una bifurcación del repositorio completo, tiene una historia en comun, pero derrepente se bifurcan y pueden variar los cambios ya que ambos proyectos podrán ser modificados en paralelo y para estar al dia un colaborador tendra que estar actualizacndo su fork con la información del original.   
Al hacer un fork de un proyecto en Github, te conviertes en dueño del repositorio fork, puedes trabajar en este con todos los permisos, pero es un repositorio completamente diferente, teniendo alguna historia en comun.   
Los  forks son importantes porque es la manera en que funciona el OpenSource, ya que una persona puede no ser colaborador de un proyecto, pero puedes contribuir al mismo haciendo mejor SW que pueda ser utilizado por cualquiera.   
Al hacer un fork, GitHub sabe que se hizo el fork del proyecto, por lo que se le permite al colaborador hacer pull request desde su repositorio.   

###  Trabajando con + de 1 repositorio remoto    
Cuando trabajas en un proyecto que existe en diferentes repositorios remotos (normalmente a causa de un fork) es muy probable que desees poder trabajar con ambos, para esto puedes crear un remoto adicional desde consola.   
`git remote add "nombre_del_remoto" URL_DEL_REMOTO` .Ejemplo: git remote add "upstream" https://github.com/freddier/hyperblog       
Al crear un remoto adicional podremos hacer pull desde el nuevo origen.   
`git pull "remoto" "rama"` .Ejemplo: git pull upstream master   
Este pull nos traerá los cambios del remoto por lo que estará al dia en el proyecto, el flujo del trabajo cambia, en adelante se estará trabajando haciendo pull desde el upstream y push al origen para pasar a hacer el pull request.   
`git pull upstream master`   
`git push origin master`   
