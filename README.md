# InvoicePlane en Docker

Como instalarlo con este archivo.

OJO:
- que para la primera instalacion: "/invoiceplane-docker/app/invoiceplane/"
  - "ipconfig.php.example" lo copio y renombro como "ipconfig.php"
  - por los motivos que se veran, esto no se crea en el respositorio (de hecho esta en el .gitignore de invoiceplane por defecto para que no se suba nunca)
- Cuando levantes y accedas a la url de InvoicePlane desplegada, tienes que rellenar la  configuracion para ella, eso reemplaza datos importantes en "ipconfig.php" de dentro del contenedor. Tras completar esto es necesario llevar ese archivo a los fuentes que se copian al entrar "/app/invoiceplane/ipconfig.php"
```bash
# copiar el del contenedor que fue actualizado y reemplazar el que hemos puesto en el docker
sudo docker cp invoiceplane-app:/var/www/html/ipconfig.php ./app/invoiceplane/ipconfig.php
```
- Entonces si, cuando pares el contenedor y vuelvas a entrar, al acceder a la url, no te pedira InvoicePlane que vuelvas a hacer la configuracion
- Sino haces eso, cada vez que levantas el contenedor y accedes a la url de InvoicePlane, te pide hacer la configuracion de nuevo, y no se ven los datos persistidos de la BD


Revisa en "docker-compose.yml" las variables de la BD asi como el usu/pass para poner el que quieras.


## Levantarlo:
```bash
sudo docker compose up -d --build
```


## Para pararlo:
```bash
sudo docker compose down

# Con -v se limpia los volumnes anteriores... para hacerlo todo de 0. Nos borraria la BBDD y datos persistidos
sudo docker compose down -v
```


