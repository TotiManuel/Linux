Vamos a crear un script que ordene archivos de forma automática en función de la extensión que tengan:
```bash
#!/bin/bash

# Crear las carpetas si no existen
mkdir -p imagenes videos documentos

# Iterar sobre cada archivo en el directorio actual
for archivo in *
do
  # Obtener el nombre base del archivo sin la ruta
  nombre_base=$(basename "$archivo")

  # Obtener la extensión del archivo usando awk
  extension=$(echo "$nombre_base" | awk -F '.' '{print $NF}')

  # Mover el archivo a la carpeta correspondiente según su extensión
  case "$extension" in
    jpg|png)
      mv "$archivo" imagenes/
      echo "Movido $archivo a la carpeta imagenes"
      ;;
    mp4|mkv)
      mv "$archivo" videos/
      echo "Movido $archivo a la carpeta videos"
      ;;
    txt|doc)
      mv "$archivo" documentos/
      echo "Movido $archivo a la carpeta documentos"
      ;;
    *)
      echo "Archivo $archivo no se movió, extensión desconocida: $extension"
      ;;
  esac
done
```