# Script
#!/bin/bash
#comprobar si no se ha introducido un parámetro.
usuario=$1

if [ -z "$usuario" ]
then
        read -p "Introduce el usuario: " usuario
fi
if [ -z "$usuario" ]
then
        echo "No has introducido un usuario"
        exit 1
fi
cat /etc/passwd | grep "$usuario" > /dev/null && existe=0 || existe=1
if [ $existe -eq 1 ]
then
        echo "el usuario $usuario no existe"
        exit 1
else
        echo "Información de $usuario:"
        echo -n "UID: "
        grep -w $usuario /etc/passwd | cut -d: -f3
        echo -n "GID: "
        grep -w $usuario /etc/passwd | cut -d: -f4
        echo -n "Home: "
        grep -w $usuario /etc/passwd | cut -d: -f6
        echo -n "Shell: "
        grep -w $usuario /etc/passwd | cut -d: -f7
fi
