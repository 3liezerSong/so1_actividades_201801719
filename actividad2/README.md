# ACTIVIDAD 2   

### Script en BASH

```bash
#!/bin/bash

# Leer la variable de usuario de GitHub (puedes cambiar este valor)
github_user="3liezerSong"

# Hacer la consulta a la API de GitHub y guardar la respuesta en una variable
response=$(curl -s https://api.github.com/users/$github_user)

# Extraer los valores necesarios del JSON usando jq y guardarlos en variables
id=$(echo $response | jq -r '.id')
created_at=$(echo $response | jq -r '.created_at')

# Imprimir el mensaje con los valores extraídos
echo "Hola $github_user. User ID: $id. Cuenta fue creada el: $created_at."

# Obtener la fecha actual en el formato deseado (YYYY-MM-DD)
fecha=$(date +%Y-%m-%d)

# Crear el directorio de registro si aún no existe
if [ ! -d "/tmp/$fecha" ]; then
    mkdir -p "/tmp/$fecha"
fi

# Crear el archivo de registro con el mensaje anterior
echo "Hola $github_user. User ID: $id. Cuenta fue creada el: $created_at." >> "/tmp/$fecha/saludos.log"
```

### Agregar el cronjob

1. Abrir y editarlo:
```bash
   crontab -e
```

2. Añadir al final del archivo crontab para que el script se ejecute cada 5 minutos:
```bash
   */5 * * * * /ruta/al/script.sh
```

Reemplazar `/ruta/al/script.sh` con la ruta completa donde guardaste tu script.

### Pasos adicionales

1. **Instalar `jq`:** 

```bash
   sudo apt-get install jq
```

2. **Permisos de ejecución:** permisos de ejecución:

```bash
   chmod +x nombre_del_archivo.sh
```
