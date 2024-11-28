
**COMO MANEJARIAS 1M DE PETICIONES POR SEGUNDO**
me aseguraria que la base de datos use un sistema de coneccion por pullings, manejamos mas eficientemente los costos de abrir y cerrar conexiones

cache para dar respuestas prefabricadas a solicitudes

podriamos hacer un cache completo de toda la respuesta para evitar que el backend tenga que procesar mas de la cuenta o evitar la comunicacion co la base de datos

podriamos implementar una base de datos redis para mejorar la velocidad de respuesta y acceso a la informacion solicitada

**RESTFULL API**
aplication program interface,
solicitudes http para acceder a lo endpoints
get put post patch delete
desacoplat el cliente y el servidor
son stateless, no establecemos una comunicación activa con los clientes
podemos manejar caches
la autenticacion y autorizacion son opcionales, podes tener apis publicas

**GRAPHQL**
es un endpoint http que responde a todas las solicitudes posibles, se puede expluir la autenticacion.
todo el graphql esta protegido bajo autenticacion y autorizacion
es un endpoint que permite al cliente autoservirse de la informacion que necesita
responde exactamente la informacion que se solicita
la restfullapi envia todos los datos aun los no solicitados

**AUTENTICACION Y AUTORIZACION**
autenticacion acto de identificar un usuario o dispositivo
autorizacion permite o deniega algun tipo de recurso solicitado de acuerdo a su rol o provilegios otorgados 

**COMO ASEGURAR LA CONSISTENCIA DE LA DATA EN UNA APLICACION**
base de datos, asegurar de guardar datos de calidad, constraints, checks de validacion necesarios para permitir insersiones de la data
tablas asociadas
evitar la eliminacion de registros y en su lugar ocultarlos
utsar herramientas de validacion en cada capa
asegurar privacidad y acceso a la data de produccion
realizar pruebas y auditorias periodicas sobre la misma

**ESTRATEGIAS DE CACHE PARA MEJORAR EL PERFORMANCE DEL BACKEND**


**COMO REALIZARIAS EL TESTING EN EL BACKEND**
jest
luego pasar por el end to end testing; probar de extremo a extremo de forma automatica
desplegar la aplicacion en una capa de staging donde se puede usar soft para pruebas de estres ( louder.io ) para simular miles de peticiones automaticas

ASEGURARIA ALMACENAR INFORMACION SENSIBLE
si es una tarjeta de credito, habilitar que el disco duro este encriptado, todos los dispositivos vinculador al manejo de esta info tambien encriptados
restringir el acceso al equipo donde esta almacenada esa informacion
no transferir nada de informacion que no este encriptada, end to end encryption como hace whatsapp
aunque la info sea interceptada, va a recibir info encriptada
borrar toda informacion sensible cuando ya no es necesaria
encriptar respaldos
no mas de una copia de seguridad

EL PROCESO DE DESPLIEGUE A RPODUCCION DEBERIA SER AUTOMATIZADO Y VERSIONIZADO
proceso automatico desde un repositorio
no desplegar en produccion, en caso de errores de ultimo momento tenemos que ser capaces de volver a una version anterior mediante docker por ejemplo e imagenes

COMO MANEJARÍAS LOS ERRORES Y LOGS DE LA APLICACIÓN
primero preguntar como manejan los logs los programadores de la empresa para estandarizar logs y alertas
si no hay sistema de logs usaria algun tipo de software especializado para logs en el backend
realizar los logs a un nivel apropiado, dependiendo en el punto en el cual haya sucedido
los logs adicionales puede ser que sean necesarios por parte d ela gerencia se pueden añadir en otro punto
categorizar los logs que te diga que tipo de log estas viendo
los mensajes de logs deben ser en ingles porque es un estandar
crear logs en un formato parseable
establecer la estrategia de como grabar los logs, estructura unificada entre aplicaciones
separar y estandarizar los logs, pueden estar en el backend o de alguna frma externa que no im'plique recurrir al backend

