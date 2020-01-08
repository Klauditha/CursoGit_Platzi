# Curso de Git y Github

## Comandos Generales
`pwd`: Para ver donde estoy en la consola   
`ls -s`: Listar carpetas   
`git congif -l` : Ver configuración   
`git congif --global user.mail "correo"` : Actualizar correo electronico
`git config --global --unser user.mailo` : Para borrar parametro mal ingresado
`git remote -v`: Ver url remota
`git commit -am ""` 


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