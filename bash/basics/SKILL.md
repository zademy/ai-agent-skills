---
name: basics
description: Bash scripting basics and best practices
---

# Bash Scripting Basics

## Shebang y Configuración

```bash
#!/usr/bin/env bash
set -euo pipefail  # Exit on error, undefined vars, pipe failures

# Debug mode
set -x
```

## Arrays y Dictionaries

```bash
#!/usr/bin/env bash

# Array
frutas=("manzana" "pera" "uva")
echo "${frutas[0]}"  # man
echo "${frutas[@]}"  # todos
echo "${#frutas[@]}" # longitud

# Iterar array
for fruta in "${frutas[@]}"; do
    echo "$fruta"
done

# Associative array (bash 4+)
declare -A colores
colores["rojo"]="#ff0000"
colores["verde"]="#00ff00"
echo "${colores[rojo]}"
```

## Strings y Manipulación

```bash
#!/usr/bin/env bash

texto="Hola mundo"

# Longitud
echo ${#texto}

# Substring
echo ${texto:0:4}  # Hola

# Reemplazar
echo ${texto/mundo/Bash}  # Hola Bash
echo ${texto//o/a}        # Hala munda

# Convertir a mayúsculas/minúsculas
echo ${texto^^}  # HOLA MUNDO
echo ${texto,,}  # hola mundo

# Trim whitespace
texto="  espacios  "
echo "${texto}" | xargs
```

## Process Substitution

```bash
#!/usr/bin/env bash

# Comparar archivos diff con process substitution
diff <(sort archivo1.txt) <(sort archivo2.txt)

# While loop con process substitution
while IFS= read -r linea; do
    echo "$linea"
done < <(grep "patron" archivo.txt)
```

## Expansión de Parámetros

```bash
#!/usr/bin/env bash

var=${variable:-"default"}   # Si no existe, usar default
var=${variable:="asignar"}   # Si no existe, asignar
var=${variable:+"alternativo"} # Si existe, usar alternativo
var=${variable:?Error}       # Error si no existe

# Extraer ruta y nombre
archivo="/ruta/al/archivo.txt"
echo "Directorio: ${archivo%/*}"
echo "Nombre: ${archivo##*/}"
echo "Extensión: ${archivo##*.}"
```

## Pipelines y Redirección

```bash
#!/usr/bin/env bash

# Pipeline con control de errores
comando1 | comando2 || { echo "Error en pipeline"; exit 1; }

# Redirección
# 1 = stdout, 2 = stderr
./script.sh > salida.txt 2> errores.txt
./script.sh &> todo.txt    # stdout y stderr
./script.sh 2>&1 | grep error

# Here strings
read -r linea <<< "texto inicial"
```

## Pattern Matching

```bash
#!/usr/bin/env bash

archivo="documento.pdf"

# Comparar patrones
if [[ $archivo == *.pdf ]]; then
    echo "Es PDF"
fi

# Comparar con regex
if [[ $email =~ ^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$ ]]; then
    echo "Email válido"
fi
```

## Paralelización

```bash
#!/usr/bin/env bash

# Ejecutar en paralelo con xargs
echo {1..10} | xargs -n1 -P4 -I{} sh -c 'echo "Procesando {}"'

# wait para sincronizar
proceso1 &
proceso2 &
wait  # Esperar a que terminen
echo "Todos los procesos finalizaron"
```
