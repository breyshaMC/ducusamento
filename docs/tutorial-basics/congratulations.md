---
sidebar_position: 4
---

# Instalación del Facturador

## Docker | Linux | SSL externo

## Pasos
<ul>
    <li>
    Para instalar debe ejecutar el script evitando instalar el SSL, le será consultado en el proceso y deberá ingresar "n"
    </li>
    <li>
    Finalizada la instalación debe dirigirse a la ruta de instalación
    </li>
    ```bash
    cd /root/facturadorpro31/
    ```
    <li>
    Debe editar el archivo .env
    </li>
    ```bash
    nano .env
    ```
</ul>

Dentro del editor ubicar los parámetros y cambiarlos:

**Antes**
```bash
APP_URL=http://${APP_URL_BASE}
FORCE_HTTPS=false
```

**Despues**
```bash
APP_URL=https://${APP_URL_BASE}
FORCE_HTTPS=true
```
<ul>
    <li>
    Una vez finalizado, guarde y salga del editor
    ejecute los siguientes comandos para eliminar la caché de la aplicación.
    </li>
    ```bash
    php artisan config:Cache
    ```
    <li>
    Con eso habrá completado el lado de la herramienta, en ese momento hasta no tener un SSL configurado no podrá acceder a la herramienta.
    </li>
</ul>
## Importante
<ul>
    <li>
    recuerde habilitar el puerto 443 para poder tener acceso a la herramienta.
    </li>
</ul>
