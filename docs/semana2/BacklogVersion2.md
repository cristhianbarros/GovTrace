# Backlog de la versión 2

**Nombre del proyecto:** GovTrace

Estas historias quedan por fuera del MVP porque el recorrido básico funciona sin ellas: el ciudadano avisa, el veedor reporta desde el celular, el reporte se sella en Stellar y los contratos llegan del SECOP II. Lo que sigue lo vuelve más robusto en campo, más útil para las veedurías y más fuerte frente a lo que prometimos en el Problem Brief.

Están organizadas por los mismos frentes del MVP, para que cada uno siga con lo suyo. Cada historia tiene una prioridad (alta, media o baja) y sus criterios de aceptación, para pasarla al tablero cuando le llegue el turno.

---

## 1. Super Administrador y sellado en Stellar (Cristhian Barros)

| # | Historia | Criterios de aceptación | Prioridad |
| :---: | --- | --- | :---: |
| 1 | Como usuario registrado quiero recuperar mi contraseña con un enlace que me llega al correo, para no depender de un administrador. | El enlace vale 60 minutos y se usa una sola vez.<br>La respuesta es la misma exista o no el correo. | Alta |
| 2 | Como Super Administrador quiero ver los reportes cuyo sellado falló después de varios intentos y volver a encolarlos desde el panel, para que ninguno se quede sin sello. | Los reintentos esperan cada vez más (1, 5, 15 y 60 minutos).<br>Tras 5 intentos el reporte queda en "Falla de Sellado" y se puede volver a encolar, uno o varios a la vez. | Alta |
| 3 | Como Super Administrador quiero recibir una alerta por correo cuando el saldo de la cuenta patrocinadora baje de un umbral, para recargarla antes de que se detenga el sellado. | El saldo se revisa cada 15 minutos.<br>La alerta trae el saldo y el umbral. | Alta |
| 4 | Como Super Administrador quiero recibir en una bandeja las solicitudes de alta que las veedurías envían desde la página de inicio, y aprobarlas o rechazarlas con un motivo, para que ninguna tenga que buscarnos por otro lado. | La solicitud pide nombre, correo de contacto y resolución de la personería.<br>Si se rechaza, el motivo le llega por correo a la veeduría. | Media |
| 5 | Como Super Administrador quiero suspender o reactivar una veeduría, para bloquear su acceso ante un problema sin perder sus datos. | Una veeduría suspendida no puede reportar ni publicar.<br>Su mapa sigue a la vista con un aviso. | Media |
| 6 | Como equipo de GovTrace queremos pasar el sellado de testnet a la red principal de Stellar, para que los sellos tengan validez permanente. | El contrato se despliega en la red principal con sus cuentas.<br>Las llaves nunca quedan en el repositorio. | Media |

## 2. Administrador de la veeduría (Meliza Posada)

| # | Historia | Criterios de aceptación | Prioridad |
| :---: | --- | --- | :---: |
| 7 | Como administrador de una veeduría quiero que me avisen cuando el SECOP II cambia la fecha, el estado o el valor de una obra que ya tiene evidencias selladas, para actuar a tiempo. | El aviso llega por correo y queda visible en la página de la obra, con el valor anterior y el nuevo. | Alta |
| 8 | Como administrador de una veeduría quiero desactivar y reactivar veedores, y reenviar o revocar invitaciones, para mantener el equipo al día. | Un veedor desactivado no puede entrar ni reportar.<br>Una invitación revocada ya no sirve. | Alta |
| 9 | Como veeduría quiero tener más de un administrador, para no quedar sin quién la gestione si uno se va. | La organización nunca puede quedar sin un administrador activo. | Media |
| 10 | Como administrador de una veeduría quiero retirar una evidencia publicada dejando a la vista que se retiró y por qué, para corregir un error sin borrar el rastro. | La evidencia retirada queda como una lápida con la fecha y el motivo.<br>Su sello sigue vigente. | Media |
| 11 | Como administrador de una veeduría quiero corregir la ubicación de una obra cuando la del SECOP II está mal, para que no bloquee los reportes de mis veedores. | El cambio queda registrado con quién lo hizo y la ubicación anterior. | Media |
| 12 | Como administrador de una veeduría quiero descargar desde una obra un expediente con sus evidencias, sus sellos y las plantillas del derecho de petición y de la denuncia, para llevar la evidencia ante las autoridades. | El expediente se descarga en PDF con las plantillas ya llenas con los datos de la obra. | Media |
| 13 | Como administrador de una veeduría quiero agrupar varios contratos en una misma obra, para que una obra con varias fases se vea como una sola. | La obra muestra todos sus contratos y sus evidencias juntas. | Baja |
| 14 | Como administrador de una veeduría quiero consultar el registro de quién hizo qué y cuándo en mi organización, para responder por cada cambio. | Cada acción queda con su autor, su fecha y lo que cambió. | Baja |
| 15 | Como administrador de una veeduría quiero recibir una vez al día un correo con las evidencias que esperan mi revisión, para que ninguna se quede sin publicar. | El correo solo sale si hay evidencias pendientes. | Baja |

## 3. Veedor de campo (Brayan Henao)

| # | Historia | Criterios de aceptación | Prioridad |
| :---: | --- | --- | :---: |
| 16 | Como veedor ciudadano quiero que, si no hay señal en la obra, el reporte se guarde en mi celular y se envíe solo cuando vuelva la conexión, para no perder la visita. | El reporte queda guardado con su lugar y su hora.<br>Se envía solo al volver la conexión.<br>Guarda hasta 10 reportes durante 7 días y avisa antes de que venza uno. | Alta |
| 17 | Como veedor ciudadano quiero ver primero las obras que están cerca de mí, para no tener que buscarlas cuando ya estoy en el lugar. | Muestra las obras a menos de 500 m, con su distancia.<br>Si no hay ninguna cerca, ofrece la búsqueda. | Alta |
| 18 | Como veedor ciudadano quiero recibir un correo cuando mi reporte se publica o se rechaza, para no tener que entrar a revisarlo. | El correo dice qué pasó y, si se rechazó, el motivo. | Media |
| 19 | Como veedor ciudadano quiero instalar GovTrace en mi celular como una aplicación, para abrirla con un toque. | Se instala desde el navegador, con el nombre y el logo de la veeduría.<br>Abre directo en "Nuevo reporte". | Media |
| 20 | Como veedor ciudadano quiero declarar, al activar mi cuenta, que no tengo impedimentos para ser veedor, para que mis reportes no queden en duda por un conflicto de interés. | La declaración sigue el artículo 19 de la Ley 850 de 2003.<br>Sin ella no se puede reportar. | Media |
| 21 | Como veedor ciudadano quiero adjuntar un video corto a mi reporte, para mostrar mejor una obra parada. | Tiene un límite de duración y de tamaño.<br>El video se sella igual que las fotos. | Baja |

## 4. SECOP II y sitio público (Camilo Hernández)

| # | Historia | Criterios de aceptación | Prioridad |
| :---: | --- | --- | :---: |
| 22 | Como ONG anticorrupción quiero que GovTrace guarde el historial de cada contrato del SECOP II y selle cada día lo que dice el Estado, para demostrar cuándo alguien cambia una fecha hacia atrás. | Cada cambio de estado, fecha de fin o valor queda con la fecha en que lo vimos.<br>Una vez al día se registra en Stellar una sola huella con todo lo sincronizado. | Alta |
| 23 | Como sistema quiero marcar cada día como "en riesgo" las obras cuya fecha de terminación ya pasó, para que el mapa las muestre en rojo. | Solo cambia las obras en ejecución con la fecha de fin vencida.<br>El sitio aclara que es una alerta de GovTrace y no una decisión de una autoridad. | Media |
| 24 | Como Super Administrador quiero ver la última sincronización con el SECOP II, cuántos contratos trajo y si falló, para saber que la integración funciona. | Muestra la fecha de la última ejecución exitosa y los errores recientes. | Media |
| 25 | Como periodista de investigación quiero ver el recibo completo de cada sello (huella, ledger, hora de la red y enlace a Stellar Expert), para auditarlo en un explorador externo. | El recibo se ve junto a cada evidencia publicada, sin iniciar sesión. | Media |
| 26 | Como periodista de investigación quiero descargar el archivo original tal como se selló y su prueba de inclusión, para hacerle mi propio peritaje o anexarlo a una denuncia. | El archivo descargado tiene la misma huella que la sellada.<br>La prueba se descarga como un archivo aparte. | Media |
| 27 | Como periodista de investigación quiero un programa abierto que compruebe una evidencia directamente contra Stellar, para verificarla aunque GovTrace no esté disponible. | Funciona con el archivo y su prueba, sin conectarse a GovTrace.<br>Está publicado en el repositorio con sus instrucciones. | Media |
| 28 | Como ciudadano quiero seguir una obra con mi correo, para enterarme cuando haya evidencia nueva o cambie su estado. | El correo se confirma con un código, como en los informes.<br>Cada aviso trae un enlace para dejar de seguir la obra. | Media |
| 29 | Como entidad o contratista quiero responder a una evidencia publicada sobre mi obra, para dar mi versión junto a ella. | La respuesta se ve junto a la evidencia, sin cambiarla ni cambiar su sello. | Media |
| 30 | Como periodista de investigación quiero filtrar el mapa por estado, municipio o presupuesto, para enfocarme en las obras que me interesan. | Si nada coincide, el mapa lo dice. | Baja |
| 31 | Como ONG anticorrupción quiero ver estadísticas del territorio y descargar en CSV o JSON las evidencias publicadas con sus sellos, para hacer mis propios análisis. | Las ubicaciones van aproximadas y cada veedor aparece con un seudónimo. | Baja |

## 5. Sostenibilidad del proyecto (Cristhian Barros)

Estas historias salen del modelo de ingresos del [Product Blueprint](ProductBlueprint.md#modelo-de-ingresos-y-riesgo).

| # | Historia | Criterios de aceptación | Prioridad |
| :---: | --- | --- | :---: |
| 32 | Como Super Administrador quiero fijar un tope mensual de sellos gratis por organización, con un valor global y una excepción por organización, para cubrir a las veedurías pequeñas y pedir un aporte a las que sellan más. | El valor global empieza en 50 sellos al mes y se puede cambiar sin tocar el código.<br>El contador se reinicia cada mes y lo no usado no se acumula.<br>Al llegar al tope el reporte se sella igual y la veeduría recibe un aviso con la invitación a hacer el aporte de mantenimiento. | Alta |
| 33 | Como visitante quiero ver en el sitio una dirección pública de donación en Stellar y poder apadrinar a una veeduría, para ayudar a financiar los sellos y el servidor. | La dirección es visible sin iniciar sesión.<br>Se muestra cuánto se ha recibido y cuánto se ha gastado en sellos.<br>El donante no decide qué se sella ni qué se publica. | Media |

---

## Por dónde empezar

Las primeras en entrar serían la 22 y la 7, junto con el tope de sellos gratis (32), que es la base del modelo de ingresos, porque atacan la otra fricción del Problem Brief, el monopolio de la verdad: con ellas GovTrace no solo sella la foto del ciudadano, sino también lo que decía el Estado en cada momento, y avisa cuando eso cambia. Después, las que hacen el sistema confiable en campo y en operación: reportar sin señal (16), las obras cercanas (17), recuperar la contraseña (1), los sellos fallidos (2) y la alerta de saldo de la cuenta patrocinadora (3).
