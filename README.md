# InvoicePlane en Docker

Usar InvoicePlane (1.7.1) pero dockerizado.
La instalacion sigue siendo un linux con un php 8.3 con apache, y una BD mariadb 11.
- Contenedor 1: aplicacion
- Contenedor 2: BD maridb. Con un volumen sobre esta para poder persistir los datos.

## Instalar correctamente

Primera instalacion:
- "/app/invoiceplane/", "ipconfig.php.example" lo copias y renombras como "ipconfig.php" en la misma ruta
- Levantas docker y accedes a http://localhost:8080
  - Hay debes completar la configuracion propia de la aplicacion InvoicePlane
    - NOTA: los datos de la BD estan en docker-compose.yml (deberian cambiar los defecto que salen hay)
      - Nombre del Host: db
      - Puerto: 3306
      - Nombre del usuario: ipuser
      - Contraseña: ippassword
      - Base de datos: invoiceplane
  - Esto modifica el "ipconfig.php" actualizando variables variables para que no se vuelve a lanzar el setup asi como una key
- Si paras y vuelves a levantar, se machaca el "ipconfig.php" con el plano, por lo que al acceder a la url, vuelve a pedir toda la configuración y genera otros key, que no permiten persistencia.
- Asi que tras configurar en primer lanzamiento, copias el archivo "ipconfig.php" del docker a tu host:
```bash
sudo docker cp invoiceplane-app:/var/www/html/ipconfig.php ./app/invoiceplane/ipconfig.php
```
- Entonces si, puedes parar y volver a levantar, que ahora si va a copiar el "ipconfig.php" ya modificado con los identificadores apropiados, y al acceder a http://localhost:8080 te mandara a login/pass de aplicación correctamente

> Por esto en .gitignore de invoiceplane esta para que no se suba este ipconfig.php nunca


## Levantar docker:
```bash
sudo docker compose up -d --build
```


## Parar docker:
```bash
sudo docker compose down

# Con -v se limpia los volumnes anteriores... para hacerlo todo de 0. Nos borraria la BD y datos persistidos
sudo docker compose down -v
```

## Otra version de InvoicePlane
Para ello habria que sustituir los archivos de app/invoiceplane por los de la nueva versión.
