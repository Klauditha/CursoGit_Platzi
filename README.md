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

###  Ignorar archivos en el repositorio con .gitignore     
Por diversas razones, no todos los archivos que agregas a un proyecto deberian guardarse en un repositorio, esto porque hay archivos que al estar en el repositorio alentan el proceso de desarrollo (por ejemplo los binary large object, blob que tardan en descargarse).   
Para que no se suban estos archivos no deseados se puede crear un archivo con el nombre ".gitignore" en la raiz del repositorio con las reglas para los archivos que no se deberian subir (ver https://git-scm.com/docs/gitignore).   
Las razones principales para tomar la decision de no agregar un archivos a un repositorio son:   
* Es un archivo con contraseñas.   
* Es un blob, que son dificiles de gestionar en git.   
* Son archivos que se generan corriendo comandos.   

#### Herramientas para almacenar archivos    
* S3 AWS: https://aws.amazon.com/es/s3.   
* Imgur.com   
* git-lfs   
* https://postimages.org

Para los que no les ignora un archivo:   
`git -rm -r --chached`   
`git add.`   
`git commit -m "comentario"`   

Excluir archivos de ser ignorados:   
ignorar/*
!ignorar/no_ignorar.jpg   
!ignorar/no_ignorar

##  README.MD Excelente Practica
### Herramientas   
* editor.md   
* getemoji.com   
* typora    

### README.MD y markdown
Es el lugar donde se explica de que se trata el proyecto, como utilizarlo y demas información que se considere importante antes de utilizar el proyecto.   
Los archivos README.MD son escritos en un lenguaje llamado Markdown, por la extensión MD, que es un estandar de la escritura en diversos sitios.   
Los README.MD pueden estar en todas las carpetas, pero el mas importante es el que se encuentra en la raiz y ayudan a que los colaboradores sepan informacion importante del proyecto, modulo o sección, puedes crear cualquier archivo con la extension .md pero solo los README los mostrará por defecto gitHub.    

##  Git Rebase: Reorganizando el trabajo realizado   
El rebase es un comando que permite "fusionar" una rama en la otra sin dejar rastro de donde se hicieron los cambios. Es una mala practica enviar estas ramas al repositorio remoto.   
Rebase y merge se diferencian en que merge mezcla dos puntos finales de dos Snapshot y en cambio rebase aplica cada uno de los cambios a la rama en la que se hace el rebase.   

##  Git Stash   
`git stash`  
`git stash list`: Ver stash   
`git stash pop`: Traer stash   
`git stash branch "nombre_rama"`: Colocar stash en una rama   
`git stash drop`: Borrar stash   

###  Stashed
Nos sirve para guardar cambios para despues. es una lista de estados que nos guarda algunos cambios que hicimos en Stagging para poder cambiar de rama sin perder el trabajo que todavia no guardamos en un commit.   
Esto es especialmente util porque hay veces que no se permite cambiar de rama, ya sea por tener cambios sin guardar y no queremos perder ese codigo.   
El stashed nos permite cambiar de ramas, hacer cambios, trabajar en otras cosas y mas adelante volver al trabajo con los archivos que teniamos en stagging.  

###  Git Stash    
El comando guarda el trabajo en staging en una lista diseñada para ser temporal llamada stash, para que puedan ser recuperados en el futuro.   
Par agregar cambios utilizar : `git stash`  
Podemos poner un mensaje en el stash para diferenciarlos: `git stash save "mensaje identificador"`  

###  Obtener elementos del Stash    
El stashed se comporta como un stash de datos de tipo LIFO(ultimo en entrar primero en salir), asi podemos acceder al metodo pop.   
Pop recuperará y sacará de la lista el ultimo estado del stashed y lo insertará en staging area, por lo que es imporante saber en que branch te encuentras para poder recuperarlo, siempre recuperará los cambios en el lugar que lo llamas.   
`git stash pop`   
Para aplicar los cambios de un stash especifico y eliminarlo del stash: `git stash pop stash@{num_stash}`   
Para retomar los cam,bios de una posición especifica del stash: `git stash apply stash@{num_stash}`  
Donde {num_stash} se obtiene con: `git stash list`  

###  Crear rama con Stash    
Para crear una rama y aplicar el stash mas reciente: `git stash branch "nombre_rama"`   
Para crear rama de un stash especifico: `git stash branch "nombre_rama" stash@{num_stash}`   
Al utilizar estos comandos crearás una rama, te pasarás a ella y tendras el stash especificaso en tu staging area.   

###  Eliminar elementos del Stash    
Para eliminar los cambios mas recientes (elemento 0) utilizar: `git stash drop`  
Si se conoce el indice del stash utilizar: `git stash drop stash@{num_stash}`  
Para eliminar todos los elementos del stash: `git stash clear`  

###  Consideraciones   
* El cambio mas reciente siempre recibe el valor 0 y los que estaban antes aumentarán su valor.   
* Al crear un stash tomará los archivos que han sido modificados y eliminados. Para que tome un archivo cuando es necesario agregarlo al staging area con `git add [nombre_archivo]` con la intención de que git tenga un seguimiento de ese archivo, o tambien utilizar el comando `git stasg -u` (guardará en el stash los archivos que no esten en staging)    .
* Al aplicar un stash este no se elimina, es una practica eliminarlos.   