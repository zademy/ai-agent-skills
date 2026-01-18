---
name: basics
description: Shell scripting basics and best practices
---

# Shell Scripting Basics

## Script Básico

```shell
#!/bin/bash

# Comentario
echo "Hola mundo"

# Variables
NOMBRE="Juan"
EDAD=30

echo "Hola $NOMBRE, tienes $EDAD años"
```

## Condicionales

```shell
#!/bin/bash

edad=18

if [ $edad -ge 18 ]; then
    echo "Eres mayor de edad"
elif [ $edad -ge 13 ]; then
    echo "Eres adolescente"
else
    echo "Eres menor de edad"
fi

# Comparaciones de strings
if [ "$nombre" = "admin" ]; then
    echo "Bienvenido administrador"
fi

# Operadores
# -eq (igual), -ne (diferente)
# -gt (mayor), -lt (menor)
# -ge (mayor o igual), -le (menor o igual)
# -z (string vacío), -n (string no vacío)
```

## Bucles

```shell
#!/bin/bash

# For loop
for i in 1 2 3 4 5; do
    echo "Número: $i"
done

# For con rango
for i in {1..10}; do
    echo $i
done

# While
contador=0
while [ $contador -lt 5 ]; do
    echo "Contador: $contador"
    contador=$((contador + 1))
done

# Leer archivo línea por línea
while IFS= read -r linea; do
    echo "$linea"
done < archivo.txt
```

## Funciones

```shell
#!/bin/bash

saludar() {
    local nombre=$1
    echo "Hola $nombre"
}

sumar() {
    local resultado=$(($1 + $2))
    echo $resultado
}

# Llamar funciones
saludar "María"
suma=$(sumar 5 3)
echo "La suma es: $suma"
```

## Argumentos

```shell
#!/bin/bash

# $0 = nombre del script
# $1 = primer argumento
# $2 = segundo argumento
# $# = número de argumentos
# $@ = todos los argumentos

echo "Script: $0"
echo "Argumentos: $@"
echo "Cantidad: $#"

for arg in "$@"; do
    echo "Argumento: $arg"
done
```
