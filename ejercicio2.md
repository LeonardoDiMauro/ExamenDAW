# Examen DAW 1era EV. 
_**Autor**_: _Leonardo Di Mauro. 19/11/2021_
## Ejercicio 2:

Crea un script de bash que modifique el contenido del archivo **/etc/hosts**. Debe tener dos atributos o tres parámetros de entrada como uso normal y uno de especial. Uso:

Comando de ejemplo: 

```
./ejercicio2.sh <enable/disable> <dirección_web> <ip>
```

### Código archivo **ejercicio2.sh**:

```
#!/bin/bash

if [[ ("$1") && ("$2") && ("$3")]]
then
    echo "-Parametro recibido: "$1" , "$2" , "$3

    if [ $1 == "enable" ]
    then 
        linea=$(awk '/'$2'/{print NR}' etc/hosts)
        #echo $linea
        sed -i "11d" hosts
        echo -e $3" "$2 >> etc/hosts
        echo "IP de "$2" cambiada corractamente, nueva IP: "$3

    elif [ $1 == "disable" ]
    then
        echo "Cambiando IP a 127.0.0.1"

    else
   	    echo "Error"
    fi

elif [[ ("$1") && ("$2")]]
then

   echo "-Parametro recibido: "$1" , "$2
   
    if [ $1 == "-> enable" ]
    then 
        echo "es enable"
        temp=$(grep -l "$2" /etc/hosts)        
        echo "${temp}"
        if [ "${temp}" == "hosts" ]
        then 
            echo "Existe la direccion web"
        else
   	        echo "No existe la direccion web, se añadira: 127.0.0.1 "$2
            echo -e "127.0.0.1 "$2 >> hosts 
            
        fi

    elif [ $1 == "disable" ]
    then
        echo "-> disable"
        linea=$(awk '/'$2'/{print NR}' hosts)
        #echo $linea
        sed -i "11d" hosts
        echo "servidor virtual: "$2" BORRADO con exito"

    else
   	    echo "Error"
    fi

elif [ "$1" ]
then
   echo "-Parametro recibido: "$1
   echo " "

   
   if [ $1 == "--help" ]
   then   	
   	echo "############ Manual para el Usuario: ############"
    echo " "
    echo "-Para activar un servidor virtual ejecuta el comando: "
    echo "./ejercicio2.sh enable <direccion-web>"
    echo " "
    echo "-Para desactivar un servidor virtual ejecuta el comando:"
    echo "./ejercicio2.sh disable <direccion-web>"
    echo " "
    echo "-Para cambiar la IP de un servidor virtual ejecuta el comando:"
    echo "./ejercicio2.sh enable <direccion-web> <ip>"
    echo " "
    echo "-Para cambiar a IP por defecto (127.0.0.1) de un servidor virtual ejecuta el comando:"
    echo "./ejercicio2.sh disable <direccion-web> <ip>"
    echo " "
   elif [ $1 == "--cat" ]
   then
   	echo "contenido..."
   	
   else
   	echo "Error-> Parametro invalido."
    echo "Consulte el Manual del Usuario con el comando:  /ejercicio2.sh --help"
   fi

else
    echo "Error -> No se ha recibido ningun parametro."
    echo "Consulte el Manual del Usuario con el comando:  /ejercicio2.sh --help"
fi
```

Para crear este codigo se han creado 3 bloques de código, dependiendo de la cantidad de parámetros introducidos entraremos en un bloque u otro.

### Explicación Comandos:

Con este comando buscamos el número de la linea donde se encuentra nuestro parámetro:

```
linea=$(awk '/'$2'/{print NR}' etc/hosts)
```

Con este comando borramos la linea 11 del fichero hosts:
```
sed -i "11d" etc/hosts

```
Este comando nos dice si el texto indicado existe dentro del archivo, si existe, devuelve el nombre del archivo:
```
temp=$(grep -l "$2" /etc/hosts) 
```

##Conclusión:

Esta programa bash ahorra tiempo a la hora de crear o modificar nuevos host virtuales o uno ya existente. Con solo añadir los parámetros los archivos clave se modifican cumpliendo las condiciones establecidas en el programa.





