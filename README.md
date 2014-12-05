Objetivo, usando un CSV de contratos de gobierno construir un API con SailsJS y un frontend con angular que lo utilize. El proyecto se llamara contratobook

Requisitos:
NodeJS, npm,sails,bower

Instalar sails y bower
npm -g install sails
npm -g insall bower

Tips:
Nodejs funciona como un servidor independiente, es decir cada app es un server; Usar nodemon para manter el servidor ejecutandose y para que se reinicie automaticamente cuando hay cambios en el codigo del backend:
ej: nodemon -w api -w config

Si sails new no te funciona despues de instalar sails intenta desintalar node e isntalarlo via el metodo recomendado oficialmente:
https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager#debian-and-ubuntu-based-linux-distributions



Paso 1
Importar la base de datos a mongo en terminal usar (mongoimport --help para entender que significan estos parametros): 
*mongoimport -d contratobook -c contrato --type csv --headerline /ruta/al/archivo.csv

Ingresar a la interfaz de comandos de mongo y verificar que tenga registros nuestra collection (tabla) deben ser 101 registros;
*mongo
*use contratobook;
db.contrato.count();

Paso 2

En terminal navegar a carpeta de desarollo (ej. ~/dev) desde ahi ejecutar:

*sails new contratobook


Paso 3
Configurar nuestra DB de mongo con nuestro app(desde ahora en adelante todos los comandos son en la raiz de nuestro project; ~/dev/contratobook)

*npm install --save sails-mongo

En el archivo config/connections.js cambiar "someMongoServer" a mongo y cambiar las config con el nombre de nuestra db (contratobook) y el user y pass en blanco ('').
En el archvio config/model.js cambiar conection a mongo y migrate a 'safe' (descomentar)

Paso 4
Generar el api para nuestra collection "contrato"; dentro de la carpeta del proyecto ejecutar:

*sails generate api contrato

Esto genera un archivo en api/models y otro en api/controllers ya con esto y nuestros datos tenemos una api funcional pero tenemos que habilitarla; en el archivo config/blueprints.js setear actions y prefix a true y prefix a '/api'

