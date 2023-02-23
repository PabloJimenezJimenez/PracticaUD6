# PRACTICA UD6
#### PARTE 1 SCRIPT BASH
Para ejecutatar el script los apartados de instalar y desinstalar hace falta hacerlo como administrador. El de ejecución no hace falta.
```bash
#!/bin/bash

#Declaración de funcines
##Función instalar
instalar(){
    echo "Introduzca el directorio en el que deseas instalarlo"
    read directorio
    comprobarDir
    echo "Introduce elnombre de usuario al que quieres dar el permiso de ejecucion"
    read nombreUsuario
    useradd $nombreUsuario
    echo "Introduce el grupo al que quieres dar el permiso de ejecucion"
    read nombreGrupo
    permisosDir
    moverArchivo
    comprobarJava
    echo "Directorio creado"
    echo "Usuario creado $nombreUsuario"
    echo "Grupo creado $nombreGrupo"
    echo "Permisos dados"
    echo "Java comprobado"
}

##Función ejecutar
ejecucion(){
    
    echo "introduce un archivo"
    read archivo
    comprobarArchivo
    echo "Elige el color R, Y, G"
    read color
    java $directorio pizarra.java $archivo $color
}
##Función desinstalar
desinstalar(){
    pregunta
    echo "Escriba el directorio donde tienes el archivo"
    read direct
    rm -r $direct
    echo "DIRECTORIO ELIMINADO"
}

##Función ayuda
ayuda(){
   echo "Opciones disponibles (Introduce la palabra)"
   echo "1. 'instalar'"
   echo "2. 'ejecutar'"
   echo "3. 'desinstalar'" 
}

#Creación de funciones para la funcion instalar
##Función que comprueba si el directorio existe y si no existe crea uno
comprobarDir(){
    if [ -e $directorio ]
    then
        echo "$directorio YA EXISTE"
    else 
        mkdir $directorio
    fi
}

##Funcion que añade el grupo y el usuario al grupo
sacarGrupo(){
    groupadd $nombreGrupo
    usermod -a -G $nombreGrupo $nombreUsuario

}

##Función para mover el script y el archivo .java
moverArchivo(){
    cp instalador.sh $directorio
    cp pizarra.java $directorio
}

##Función que da permisos 777 al directorio y cambia el owner del directorio
permisosDir(){
    sacarGrupo
    chown $nombreUsuario:$nombreGrupo $directorio
    chmod 777 $directorio
}

##Función que comprueba si está instalado java y si no esta instalado lo instala
comprobarJava(){
    test -h /usr/bin/java 
    if [ $? -eq 1 ]
    then
        echo "Instalando java..."
        apt install default-jre
    fi
}

#Creacion de funciones para ejecutar
##Función para comprobar si existe el archivo y si no te crea uno
comprobarArchivo(){
    test -f $archivo
    if [ $? -eq 1 ]
    then
        nano $archivo
    fi
}


#Creación de funciones para desinstalar
##Función para preguntar si desea desinstalar el programa 
pregunta(){
    echo "Desea desinstalar el programa [S/N]"
    read resp
    if [ $resp == 'S' ]
    then
        echo "Comenzando desintalacion..."
    else
        exit
    fi
}

#Inicio del programa
case  "$1"  in
    "instalar") instalar;;
    "ejecutar") ejecucion;;
    "desinstalar") desinstalar;;
    *) ayuda
esac
```

#### PARTE 2 SCRIPT POWERSHELL
En powershell es una versión demo que al entrar en cada una de las funciones lo único que hace es un timer que dura x segundos. Además en vez de pasarle una variable por paramtro se la pido dentro del script. 

```powershell

#Función menu
function Get-Menu {
    Clear-Host
    Write-Host "1. instalar"
    Write-Host "2. ejecutar"
    Write-Host "3. desinstalar"
    Write-Host "4. exit"
}

#Funció instalar
function instalar {
    Write-Host "INSTALANDO......."
    Start-Sleep -Seconds 3
    
}

#Función ejecutar
function ejecutar {
    Write-Host "EJECUTANDO......."
    Start-Sleep -Seconds 1
    
}

#Función desinstalar
function desinstalar {
    Write-Host "DESINSTALANDO......."
    Start-Sleep -Seconds 2
    
}
#Función ayuda
function ayuda {
    Write-Host "Escribe el numero de la opcion"
    Write-Host "1. instalar"
    Write-Host "2. ejecutar"
    Write-Host "3. desinstalar"
    Write-Host "4. exit"
    
}

#Inicio de programa
do{
    Get-Menu
    $opcion=Read-Host "Elija una opcion"
    switch($opcion){
        '1'{instalar}
        '2'{ejecutar}
        '3'{desinstalar}
        '4'{exit}
        default{ayuda}
    } 
}while ($true) 
```