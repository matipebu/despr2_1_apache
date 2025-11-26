# Actividad 2.1 — Instalación y despliegue básico con Apache

## Despregamento de aplicacións web
**Autor:** Matías Pérez Bustelo

En esta actividad instalaremos y desplegaremos nuestra web sobre **Apache2**.

---

## 1. Preparación de la máquina
Hacemos un **clon enlazado** de la máquina proporcionada para hacer el ejercicio.

### 1.1 Configuración de la red
- Configuramos la **redirección de puertos**:
  - Eliminamos la configuración anterior.
  - Añadimos las nuevas reglas de NAT.
- Iniciamos la máquina.

---

## 2. Conexión por SSH
Nos conectamos a la VM mediante SSH usando el puerto que configuramos en las reglas:

```bash
ssh -p <puerto> usuario@localhost
```

---

## 3. Instalación de Apache2 y configuración del firewall
1. Actualizamos los paquetes:

```bash
sudo apt update && sudo apt upgrade -y
```

2. Instalamos Apache2:

```bash
sudo apt install apache2 -y
```

3. Permitimos Apache y SSH en el firewall:

```bash
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https
sudo ufw enable
```

4. Comprobamos el servicio de Apache2:

```bash
sudo systemctl status apache2
```

---

## 4. Comprobación de la página por defecto
- Navegamos en el host a: [http://localhost:8081/](http://localhost:8081/)  
- Deberíamos ver la página por defecto de Apache2.

---

## 5. Despliegue de nuestra web
### 5.1 Crear el directorio raíz del sitio
- Creamos el directorio raíz de nuestro sitio web y borramos cualquier contenido anterior:

```bash
sudo rm -rf /var/www/html/*
sudo mkdir -p /var/www/html
```

### 5.2 Copiar los archivos de la web
- Copiamos todos los archivos de nuestro proyecto al directorio `/var/www/html`.

### 5.3 Comprobación inicial
- Al recargar la página en el navegador veremos un `indexOf` o un error de **Forbidden**, porque aún no hay permisos adecuados.

---

## 6. Configuración de permisos
1. Damos permisos al usuario de Apache (`www-data`):

```bash
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html
```

2. Recargamos Apache para aplicar cambios:

```bash
sudo systemctl restart apache2
```

---

## 7. Resultado final
- Al recargar [http://localhost:8081/](http://localhost:8081/) podremos **acceder a todos los archivos**, incluyendo CSS e imágenes.  
- El sitio web se muestra correctamente con todos los permisos dados.
<img width="1273" height="865" alt="image" src="https://github.com/user-attachments/assets/e489490b-8f13-4c5e-84a4-cad3ca35ca86" />
