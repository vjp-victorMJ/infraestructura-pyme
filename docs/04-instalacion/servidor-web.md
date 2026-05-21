# Instalación y Configuración del Servidor Web (Apache2)

## Introducción

Este documento describe el proceso de instalación y configuración de Apache2 como servidor web para la infraestructura LAMP de la PYME.

## Requisitos Previos

- Sistema operativo: Ubuntu Server 22.04 LTS
- Acceso root o permisos sudo
- Conexión a Internet
- Completar los pasos de análisis y diseño de la infraestructura

## 1. Actualización del Sistema

```bash
sudo apt update
sudo apt upgrade -y
```

## 2. Instalación de Apache2

```bash
sudo apt install apache2 -y
```

## 3. Habilitación de Apache2

```bash
# Iniciar el servicio
sudo systemctl start apache2

# Habilitar en el arranque
sudo systemctl enable apache2

# Verificar estado
sudo systemctl status apache2
```

## 4. Habilitación de Módulos Necesarios

```bash
# Reescritura de URLs
sudo a2enmod rewrite

# Proxy para PHP (si se usa PHP-FPM)
sudo a2enmod proxy proxy_fcgi

# SSL/TLS (para HTTPS)
sudo a2enmod ssl

# Reiniciar Apache
sudo systemctl restart apache2
```

## 5. Configuración de VirtualHost

### Crear estructura de directorios

```bash
sudo mkdir -p /var/www/miempresa.local/html
sudo mkdir -p /var/www/miempresa.local/log
sudo chown -R www-data:www-data /var/www/miempresa.local
sudo chmod -R 755 /var/www/miempresa.local
```

### Crear archivo de configuración del VirtualHost

```bash
sudo nano /etc/apache2/sites-available/miempresa.local.conf
```

Contenido:

```apache
<VirtualHost *:80>
    ServerName miempresa.local
    ServerAlias www.miempresa.local
    ServerAdmin admin@miempresa.local

    DocumentRoot /var/www/miempresa.local/html

    ErrorLog ${APACHE_LOG_DIR}/miempresa.local-error.log
    CustomLog ${APACHE_LOG_DIR}/miempresa.local-access.log combined

    <Directory /var/www/miempresa.local/html>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

### Habilitar el VirtualHost

```bash
sudo a2ensite miempresa.local.conf
sudo a2dissite 000-default.conf
sudo apache2ctl configtest
sudo systemctl restart apache2
```

## 6. Verificación de la Instalación

```bash
# Comprobar versión
apache2 -v

# Verificar módulos habilitados
apache2ctl -M

# Comprobar acceso al servidor
curl http://localhost
```

## 7. Página de Bienvenida

Crear archivo de prueba:

```bash
sudo nano /var/www/miempresa.local/html/index.html
```

```html
<!DOCTYPE html>
<html>
<head>
    <title>Bienvenido - Mi Empresa</title>
</head>
<body>
    <h1>Servidor Apache2 Funcionando Correctamente</h1>
    <p>La infraestructura LAMP está lista para la instalación de aplicaciones.</p>
</body>
</html>
```

## 8. Configuración Básica de Seguridad

### Ocultar versión de Apache

```bash
sudo nano /etc/apache2/conf-available/security.conf
```

Añadir o modificar:

```apache
ServerTokens Prod
ServerSignature Off
```

### Habilitar la configuración

```bash
sudo a2enconf security
sudo systemctl restart apache2
```

## 9. Verificación Final

- [ ] Apache2 está instalado y en ejecución
- [ ] Módulos rewrite, proxy y ssl están habilitados
- [ ] VirtualHost está configurado correctamente
- [ ] Página de prueba es accesible
- [ ] Versión de Apache está oculta

## Próximos Pasos

1. Instalar PHP 8.x - Ver [base-de-datos.md](./base-de-datos.md)
2. Configurar base de datos MariaDB - Ver [base-de-datos.md](./base-de-datos.md)
3. Configurar SSH y Firewall - Ver [ssh-firewall.md](./ssh-firewall.md)
4. Implementar monitorización - Ver [monitorizacion.md](./monitorizacion.md)

## Referencias

- [Documentación oficial Apache2](https://httpd.apache.org/)
- [Ubuntu Server 22.04 Documentation](https://ubuntu.com/server/docs)
- [Mozilla Web Security Guidelines](https://infosec.mozilla.org/guidelines/web_security)

## Notas

- Este documento es parte de la documentación de infraestructura LAMP para PYME
- Se asume entorno de desarrollo/prueba inicial
- Para producción, revisar políticas adicionales de seguridad

## Reglas UFW
- Permitir SSH solo desde IP de la oficina: `ufw allow from 192.168.1.0/24 to any port 22`
- Permitir tráfico web: `ufw allow 80/tcp` y `ufw allow 443/tcp`
- Permitir tráfico web: `ufw allow 80/tcp` y `ufw allow 443/tcp`
- Permitir tráfico web: `ufw allow 80/tcp` y `ufw allow 443/tcp`

---

*Última actualización: 2026*
*Estado: Borrador*
