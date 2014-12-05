#Contratobook

##Objetivo

Usando un CSV de contratos de gobierno construir un API con SailsJS y un frontend con angular que lo utilize. El proyecto se llamara contratobook.

###Requisitos:

* NodeJS
* npm
* mongo
* sails
* bower


###Importar DB
- En terminal usar (`mongoimport --help` para entender que significan estos parametros): 

`mongoimport -d contratobook -c contrato --type csv --headerline /ruta/al/archivo.csv`

- Ingresar a la interfaz de comandos de mongo y verificar que tenga registros nuestra collection (tabla) deben ser 101 registros;

```javascript
use contratobook;
db.contrato.count();`
```

###Inicializar APP

En terminal navegar a carpeta de este proyecto (ej. ~/dev/contratobook/) desde ahi ejecutar:

`sails new <tunombre>`

Despues puedes levantar el app con `sails lift`, `nodemon` ó `node app.js`

###Configurar DB

Desde ahora en adelante todos los comandos son en la raiz de nuestro project (~/dev/contratobook/<tunombre>)

-Instalar el adapator de mongo en nuestro proyecto

`npm install --save sails-mongo`

-En el archivo config/connections.js cambiar "someMongoServer" a mongo y cambiar las config con el nombre de nuestra db (contratobook) y el user y pass en blanco ('').
-En el archvio config/model.js cambiar conection a mongo y migrate a 'safe' (descomentar)

###Crear API y Probar
Para generar al API de contratos dentro de la carpeta del proyecto ejecutar:

`sails generate api contrato`

Esto genera un archivo en api/models y otro en api/controllers. Con esto y nuestros datos tenemos una api funcional pero tenemos que habilitarla:

En el archivo config/blueprints.js setear actions y prefix a true y prefix a '/api'

Para probar ejecutamos:
`sails lift`

Posteriormente en el navegador navegamos a: http://localhost:1337 y http://localhost:1337/api/contrato


###Tips:

####Instalacion de sails y bower

`npm -g install sails`
`npm -g insall bower`

####Nodemon

Nodejs funciona como un servidor independiente, es decir cada app es un server. Usar nodemon o foreverpara manter el servidor ejecutandose y para que se reinicie automaticamente cuando hay cambios en el codigo del backend ahorra mucho tiempo. 
Ej:

`nodemon -w api -w config`

####NPM
Si `sails new` no te funciona despues de instalar sails intenta desintalar node e instalarlo via el metodo recomendado oficialmente:
https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager#debian-and-ubuntu-based-linux-distributions

####Terminator
Puedes usar terminator para tener dos consolas visibles; una con el app ejecutandose y la otra libre para hacer otros comandos. Con ctrl+e agregas un panel horizontalmente y con ctrl+w lo cierras