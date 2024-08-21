# ACTIVIDAD 4   - Servicio de Saludo

### Paso 1: Crear el script

Primero, crea un script llamado `saludo.sh` que imprima un saludo y la fecha actual cada segundo.
```bash
sudo nano /usr/local/bin/saludo.sh
```

```bash
#!/bin/bash

while true; do
    echo "Hola, la hora del logg es: $(date)"
    sleep 1
done
```

Guarda este archivo en `/usr/local/bin/saludo.sh` y asegúrate de que sea ejecutable:

```bash
sudo chmod +x /usr/local/bin/saludo.sh
```

### Paso 2: Crear el archivo de unidad `systemd`

Crea un archivo de unidad `systemd` llamado `saludo.service` en `/etc/systemd/system/`.

```bash
sudo nano /etc/systemd/system/saludo.service
```

```ini
[Unit]
Description=Servicio de saludo, generalmente esto es metadata descriptiva jej

[Service]
ExecStart=/usr/local/bin/saludo.sh
Restart=always

[Install]
WantedBy=multi-user.target
```

### Paso 3: Habilitar y arrancar el servicio

Recarga los archivos de unidad `systemd`, habilita el servicio para que se inicie con el sistema y arráncalo.

```bash
sudo systemctl daemon-reload
sudo systemctl enable saludo.service
sudo systemctl start saludo.service
```
Recarga los archivos de unidad `systemd` para que reconozca el nuevo servicio:
```bash
sudo systemctl daemon-reload
```

Habilita el servicio para que se inicie automáticamente con el sistema:
```bash
sudo systemctl enable saludo.service
```

Arranca el servicio:
```bash
sudo systemctl start saludo.service
```

### Paso 4: Verificar los logs del servicio

Puedes verificar los logs del servicio utilizando `journalctl`.

```bash
sudo journalctl -u saludo.service
```


# Detener el servicio

1. Para detener el servicio en ejecución:
    ```bash
    sudo systemctl stop saludo.service
    ```

### Deshabilitar el servicio

2. Para deshabilitar el servicio y evitar que se inicie automáticamente al arrancar el sistema:
    ```bash
    sudo systemctl disable saludo.service
    ```

### Verificar el estado del servicio

3. Para verificar que el servicio está detenido y deshabilitado:
    ```bash
    sudo systemctl status saludo.service
    ```

### Eliminar el archivo de unidad (opcional)

4. Si deseas eliminar completamente el servicio, puedes eliminar el archivo de unidad:
    ```bash
    sudo rm /etc/systemd/system/saludo.service
    ```

5. Luego, recarga los archivos de unidad `systemd` para aplicar los cambios:
    ```bash
    sudo systemctl daemon-reload
    ```