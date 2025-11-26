# Actividad 2.1 — Instalación y despliegue básico con Apache

## Despregamento de aplicacións web
**Autor:** Matías Pérez Bustelo

En esta actividad instalaremos y desplegaremos nuestra web sobre **Apache2**.



---

## 1. Preparación de la máquina
Hacemos un **clon enlazado** de la máquina proporcionada para hacer el ejercicio.
<img width="1004" height="65" alt="image" src="https://github.com/user-attachments/assets/e31fb2b5-791e-4b2b-a540-2c8f66649158" />


### 1.1 Configuración de la red
- Configuramos la **redirección de puertos**:
  - Eliminamos la configuración anterior.
     <img width="997" height="91" alt="image" src="https://github.com/user-attachments/assets/5639449f-6253-43bd-a630-1cefa25fe648" />

  - Añadimos las nuevas reglas de NAT.
    <img width="997" height="91" alt="image" src="https://github.com/user-attachments/assets/bffc7f4a-d657-4f0e-b624-8226ada332f2" />
    <img width="1000" height="44" alt="image" src="https://github.com/user-attachments/assets/a39cdaa1-d88e-4857-8a49-da6d6f2540cc" />
    <img width="1004" height="46" alt="image" src="https://github.com/user-attachments/assets/a18864fe-9259-466d-98c2-5a35161cd0d6" />


  
- Iniciamos la máquina.

---

## 2. Conexión por SSH
Nos conectamos a la VM mediante SSH usando el puerto que configuramos en las reglas:


```bash
ssh -p <puerto> usuario@localhost
```
<img width="736" height="114" alt="image" src="https://github.com/user-attachments/assets/91085ade-d235-4c8f-ae17-a04fc799afc6" />

---

## 3. Instalación de Apache2 y configuración del firewall
1. Actualizamos los paquetes:

```bash
sudo apt update && sudo apt upgrade -y
```
<img width="696" height="253" alt="image" src="https://github.com/user-attachments/assets/b4976319-b8c1-415b-8f8b-4b1619de8e44" />


2. Instalamos Apache2:

```bash
sudo apt install apache2 -y
```
<img width="1004" height="335" alt="image" src="https://github.com/user-attachments/assets/77f569a5-acba-4fda-bfce-45adfd5bcdb8" />


3. Permitimos Apache y SSH en el firewall:

```bash
sudo ufw allow 'Apache Full'
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https
sudo ufw enable
```
<img width="1004" height="477" alt="image" src="https://github.com/user-attachments/assets/8cfadc95-0d90-4d8e-b1eb-22cb76ca0502" />
<img width="778" height="409" alt="image" src="https://github.com/user-attachments/assets/4b4bbc3a-17ec-441d-9904-38c26b0953f6" />


4. Comprobamos el servicio de Apache2:

```bash
sudo systemctl status apache2
```
<img width="1004" height="304" alt="image" src="https://github.com/user-attachments/assets/965f62e4-6705-442e-bcbc-e96e420a34e8" />



---

## 4. Comprobación de la página por defecto
- Navegamos en el host a: [http://localhost:8081/](http://localhost:8081/)  
- Deberíamos ver la página por defecto de Apache2.
<img width="898" height="722" alt="image" src="https://github.com/user-attachments/assets/684748f2-558a-43ee-9901-e6930ef423ef" />

---

## 5. Despliegue de nuestra web
### 5.1 Crear el directorio raíz del sitio
- Creamos el directorio raíz de nuestro sitio web y borramos cualquier contenido anterior:

```bash
sudo rm -rf /var/www/html/*
sudo mkdir -p /var/www/html
```
- <img width="720" height="70" alt="image" src="https://github.com/user-attachments/assets/3249b09f-0dbb-4931-a369-f2220cec3d38" />
- <img width="758" height="38" alt="image" src="https://github.com/user-attachments/assets/6af69827-18ad-4f12-aeaa-45071578857a" />

### 5.2 Copiar los archivos de la web
- Copiamos todos los archivos de nuestro proyecto al directorio `/var/www/html`.
- <img width="1004" height="215" alt="image" src="https://github.com/user-attachments/assets/0e88b149-4124-4e1c-bb79-58703b570c14" />


### 5.3 Comprobación inicial
- Al recargar la página en el navegador veremos un `indexOf` o un error de **Forbidden**, porque aún no hay permisos adecuados.
- <img width="1004" height="369" alt="image" src="https://github.com/user-attachments/assets/fd387166-98af-4482-9594-5978c1d38569" />
-Vemos que todo el contenido no puede acceder a él con las herramientas del navegador.
<img width="1004" height="267" alt="image" src="https://github.com/user-attachments/assets/0bc5f63b-3b92-4d9c-aa0e-08bbe10a8cbe" />



---

## 6. Configuración de permisos
1. Damos permisos al usuario de Apache (`www-data`):



```bash
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html/

```


2. Recargamos Apache para aplicar cambios:

```bash
sudo systemctl restart apache2
```
<img width="1004" height="156" alt="image" src="https://github.com/user-attachments/assets/81bd7029-736f-4090-b62d-6090ccae50f7" />

---

## 7. Resultado final
- Al recargar [http://localhost:8081/](http://localhost:8081/) podremos **acceder a todos los archivos**, incluyendo CSS e imágenes.  
- El sitio web se muestra correctamente con todos los permisos dados.
<img width="1273" height="865" alt="image" src="https://github.com/user-attachments/assets/e489490b-8f13-4c5e-84a4-cad3ca35ca86" />
