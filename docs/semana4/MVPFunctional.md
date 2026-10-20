# MVP funcional

**Proyecto:** GovTrace · **Producto en línea (testnet):** https://govtrace.duckdns.org · **Video:** [youtube.com/shorts/jOcInB0UXSc](https://youtube.com/shorts/jOcInB0UXSc) · **Código de la aplicación:** la carpeta [`govtrace-app/`](../../govtrace-app) de este repositorio, una copia de [github.com/cristhianbarros/govtrace-app](https://github.com/cristhianbarros/govtrace-app), donde se desarrolla

---

## Evidencia verificable

Todo se puede comprobar sin cuenta y sin depender de nosotros:

| Qué | Enlace |
|---|---|
| Producto en línea, en la testnet de Stellar | https://govtrace.duckdns.org |
| Video del producto con el pitch (máximo 3 minutos) | [youtube.com/shorts/jOcInB0UXSc](https://youtube.com/shorts/jOcInB0UXSc) |
| Contrato de sellado, desplegado en testnet | [`CAKUYPROMNYKZCMCNI2N5RTWZE3JZ7RR4Q2W5FNVQNPANNMQPLJ4PLDY`](https://stellar.expert/explorer/testnet/contract/CAKUYPROMNYKZCMCNI2N5RTWZE3JZ7RR4Q2W5FNVQNPANNMQPLJ4PLDY) |
| Transacción que desplegó el contrato (29 de septiembre de 2026) | [`64e5c481…0574f5`](https://stellar.expert/explorer/testnet/tx/64e5c481160139c3801365c57078e7664121531a69e5f7de4516463a570574f5) |
| Transacción de un sello (la selladora llama a `seal` y la patrocinadora paga la comisión) | [`0fcba4ce…c5724a`](https://stellar.expert/explorer/testnet/tx/0fcba4ceca9ca1898a91b575b59917ac1a4ddcf886bef7b362036d1687c5724a) |
| Cuenta selladora: la única que puede sellar | [`GCUCPDHR…PXD3NJM`](https://stellar.expert/explorer/testnet/account/GCUCPDHRG3AVSYBBEHNB3A5QQ4NEFHAKLTGR74FQZJQQCEOMKPXD3NJM) |
| Cuenta patrocinadora: paga las comisiones con *fee bump* | [`GCOQRTRH…SXR6S6KU`](https://stellar.expert/explorer/testnet/account/GCOQRTRH6KYDSAGEGF4R7O4OUM5F5NZJD5ESVFVUALCZ7TOXSXR6S6KU) |
| Una evidencia publicada, con su sello y el validador | [La escuela San Javier, en Medellín](https://veeduria-prueba.govtrace.duckdns.org/worksite/01m55z4w7jtvnw2052xq6n9yer) |
| Código del contrato (Soroban, Rust) | [`govtrace-app/contracts/sealing`](../../govtrace-app/contracts/sealing) |
| Verificador independiente, que comprueba una evidencia sin GovTrace | [`govtrace-app/tools/verify`](../../govtrace-app/tools/verify) |

Al 19 de octubre de 2026, el contrato lleva 72 sellos y ningún error. Todos los pagó la cuenta patrocinadora.

El servidor de pruebas puede apagarse de noche para ahorrar costos; durante la evaluación queda encendido todo el día.

---

## Lo construido

Elegimos la **opción A, contrato propio** (semana 3). El contrato está escrito, desplegado en testnet y conectado al front, y el back hace el resto del recorrido.

### El contrato y cómo se conecta con el front

El contrato tiene tres funciones: `__constructor(sealer)` fija para siempre la cuenta selladora, `seal(obra, raíz)` guarda la huella de un reporte con el ledger y la hora de la red, y `get_seal(raíz)` deja que cualquiera la consulte. No hay forma de modificar ni de borrar un sello. Lo prueban `make contract-test`, con el entorno de pruebas de Soroban, y `make contract-smoke`, con transacciones reales: sella, rechaza a una cuenta externa y rechaza un duplicado.

| Dónde, en el front | Qué pasa con el contrato |
|---|---|
| App del veedor: **Enviar** el reporte | El servidor calcula la huella del reporte (la raíz de Merkle de sus fotos y sus datos) y la sella con `seal`. En **Mis reportes**, el reporte pasa a "Sellado" con su ledger y el enlace **Ver en Stellar Expert**. |
| Página de una obra: **Comprobar que es original** | El validador calcula en el navegador la huella del archivo y le pregunta al contrato por ese sello directamente en el RPC público de Stellar, sin pasar por nuestro servidor. Si cambió un solo píxel, responde "Archivo Alterado o Falso". |
| Página de una obra: **Descargar archivo original** y **Descargar su prueba** | El archivo sellado y su prueba de inclusión, para verificarlos con `tools/verify`, también sin GovTrace. |
| Panel del Super Administrador: **Sellado** y **Uso** | El saldo en XLM de la patrocinadora, leído de la red, y lo pagado en comisiones por cada veeduría. |

### Qué queda en Stellar y qué protege

Por cada reporte, el contrato guarda una huella SHA-256 de 64 caracteres, la raíz, que resume las huellas de todas sus fotos y la de sus datos (hora, comentario, ubicación y el seudónimo del veedor). Guarda también otra huella que identifica la obra, y el ledger y la hora, que pone la red. Las fotos, el comentario, la ubicación y el nombre del veedor no salen de GovTrace. A partir de una huella no se puede reconstruir la foto, y si cambia un solo píxel la huella es otra.

- **Nadie puede cambiar, borrar ni antedatar un sello, ni siquiera nosotros.** El contrato no tiene función para eso ni para reemplazar su código, y la hora la pone la red.
- **Solo la selladora puede sellar.** Si se filtrara su llave, alguien podría agregar sellos falsos, pero no tocar los que ya existen; desplegaríamos otro contrato. Por eso, en la red principal, firmará desde AWS KMS.
- **La verificación no depende de nosotros.** El navegador le pregunta directamente a Stellar.
- **Lo que el sello no prueba** es que la foto diga la verdad. Prueba que no ha cambiado desde que se selló, y desde cuándo existe. Que sea de la obra lo controlan la geocerca y la revisión de la veeduría antes de publicar.

### El resto del back

- **Sellado en cola y por turnos.** Stellar admite una transacción pendiente por cuenta, así que la selladora sella una por ledger, reintenta si la red falla y confirma cada sello con `getTransaction`. Guarda el recibo: la transacción, el ledger, la hora y la comisión.
- **El veedor no necesita billetera.** La selladora firma y la patrocinadora paga con *fee bump*. Si se filtrara la llave de la patrocinadora, nadie podría sellar con ella.
- **Saldo vigilado.** El Super Administrador recibe una alerta cuando el saldo de la patrocinadora baja del umbral, y el sellado se pausa por debajo de 2 XLM sin perder los reportes.
- **SECOP II.** Una sincronización diaria trae los contratos de obra del territorio de cada veeduría.
- **Una base de datos por veeduría** y un log de auditoría que no se puede editar.
- **Privacidad antes de sellar.** El celular difumina los rostros y quita los metadatos de cada foto. Lo que se sella es la huella de la foto ya difuminada.

### Lo nuevo de esta semana

| Mejora | Qué cambia para el usuario |
|---|---|
| El ciudadano informa sobre cualquier obra | Una obra sin ubicación también se puede reportar: el ciudadano propone el punto en un mapa y la veeduría lo confirma. |
| La tarjeta de la obra en el mapa | Tocar un pin abre una tarjeta con el estado de la obra, su valor, la fecha de la última evidencia y hasta 3 miniaturas. |
| GovTrace sugiere la veeduría | El inicio empieza por la obra: el ciudadano la busca por nombre, municipio o cercanía (su ubicación no sale del teléfono), y GovTrace le dice qué veeduría puede atenderlo y por qué. |
| Costos y seguridad del servidor | El servidor de pruebas puede apagarse de noche, tiene presupuesto con alertas y suma controles: buckets solo por HTTPS y protección contra el borrado de la máquina. |

**Calidad:** 1.297 pruebas de backend, 820 de frontend y 68 de punta a punta en un navegador real. Cada uno de los 548 escenarios Gherkin tiene un test con su nombre. GitHub Actions corre todo en cada PR, y un PR con fallas no entra a `main`.

---

## 1. Aprendizajes y ajustes priorizados

Lo que aprendimos esta semana salió de usar el producto en testnet y de recorrerlo como un ciudadano que no conoce la plataforma.

1. **Un sello cuesta más de lo estimado.** En el Blueprint calculamos unos 0,25 XLM por sello. Los primeros 70 sellos reales en testnet promediaron 0,37 XLM, entre 0,27 y 0,40. Un piloto de 200 reportes al mes pasa de unos 50 a unos 74 XLM.
2. **Una obra sin ubicación era invisible.** El SECOP II no trae coordenadas, así que esas obras no salían en el mapa y el ciudadano no podía reportarlas.
3. **El ciudadano no sabe a qué veeduría escribir.** El inicio le pedía elegir una veeduría antes de mostrarle la obra.
4. **Un pin sin contexto obliga a salir del mapa** para saber si la obra va bien o mal.
5. **Un servidor encendido las 24 horas** gasta de noche sin que nadie lo use.

| Ajuste | Impacto | Esfuerzo | Cuándo |
|---|:---:|:---:|---|
| El ciudadano propone la ubicación y la veeduría la confirma (2) | Alto | Medio | Hecho |
| GovTrace sugiere la veeduría (3) | Alto | Medio | Hecho |
| La tarjeta con miniaturas (4) | Medio | Bajo | Hecho |
| Apagado nocturno y presupuesto (5) | Medio | Bajo | Hecho |
| Tope mensual de sellos gratis por veeduría (1) | Alto | Medio | Antes del cierre |
| Verificar en Stellar Expert que el código desplegado es el de nuestro repositorio | Medio | Bajo | Antes del cierre |
| Un sello más compacto, que pague menos renta (1) | Medio | Alto | Pendiente |
| Red principal, con la llave de la selladora en AWS KMS | Alto | Alto | Pendiente |

---

## 2. Riesgos y pendientes

**Riesgos identificados**

- **La testnet se reinicia cada cierto tiempo.** Con ella desaparecen el contrato y los sellos, y los enlaces de este documento dejarían de abrir. Si pasa, volvemos a desplegar con `make testnet-setup` y actualizamos los enlaces. En la red principal este riesgo no existe.
- **Los sellos viejos se archivan.** Cada sello paga renta por unos 180 días. Falta comprobar que una evidencia se puede verificar cuando su sello se archiva. Si no se puede, habría que extender cada sello, y ese costo no está en el presupuesto.
- **El costo por sello.** Medimos 0,37 XLM, no 0,25. Sin un tope por veeduría, el gasto de la patrocinadora crece con el uso y una veeduría muy activa puede vaciarla.
- **El valor legal del sello no está probado.** Ningún juez ni contraloría ha recibido todavía una evidencia sellada por GovTrace. El supuesto 1 del Problem Brief (Ley 527 de 1999) sigue sin validar. Antes de la red principal también hay que definir qué entidad opera GovTrace y responde por los datos personales (Ley 1581 de 2012).
- **Un solo servidor pequeño.** Tiene 2 GB de memoria y no tiene réplica. Para el piloto alcanza, pero producción necesita estar encendida siempre y tener un plan si la máquina falla.
- **Dependemos de los datos abiertos del SECOP II.** Si el Estado cambia o limita la API, la sincronización diaria se detiene. Los reportes ya sellados no se pierden.
- **Las llaves.** En testnet se guardan cifradas en AWS. Para la red principal, la selladora debe firmar desde AWS KMS, sin que la llave salga de allí.
- **Todavía no hay usuarios reales.** Todo lo probado usa datos de prueba. No sabemos cómo lo usan en campo veedores de distintas edades, con celulares de gama media y mala señal.
- **El equipo es de una sola persona.** Si su único integrante se detiene, el proyecto se detiene. Lo mitigan el código abierto, las pruebas automáticas y una documentación con la que otra persona puede levantarlo con `make setup`.

**Qué queda por resolver**

1. El tope mensual de sellos gratis por veeduría.
2. La verificación del código del contrato en Stellar Expert.
3. La prueba de un sello archivado y el sello compacto.
4. La salida a la red principal: KMS, proveedor de RPC y la entidad que opera el servicio.
5. Un piloto con una veeduría real en Medellín.

---

## 3. Plan de validación con usuarios

**A quiénes.** Al usuario del Problem Brief: el veedor ciudadano, la veeduría u ONG anticorrupción y el periodista de investigación. También al ciudadano que avisa sin crear cuenta. Buscamos una veeduría de Medellín para un piloto de 4 semanas en testnet, con 5 a 8 veedores. Entre ellos queremos adultos mayores: la interfaz se diseñó pensando en ellos y hay que comprobarlo en campo.

**Con qué métodos.** Son tres, en este orden, y cada uno comprueba hipótesis concretas de la tabla siguiente.

1. **Antes del piloto, una prueba en campo con 5 veedores (H1).** Al menos 2 son adultos mayores. Cada uno va a una obra cercana, como en su recorrido de siempre, y con su propio celular envía un reporte, encuentra su sello y comprueba una foto. No le ayudamos ni le decimos dónde tocar: lo acompañamos, anotamos cuánto tarda, dónde se detiene y si termina, y al final le preguntamos qué le costó más. Lo que falle se corrige antes de empezar el piloto.
2. **Semanas 1 a 4, el piloto con la veeduría (H1, H3 y H4).** Sus veedores reportan obras reales de Medellín, y la veeduría invita por sus redes a los ciudadanos a avisarle por GovTrace. Medimos con lo que el producto ya registra: el tiempo de cada reporte y de su sello, las comisiones, los rechazos por la geocerca, los informes ciudadanos y cuánto tardan en recibir respuesta.
3. **Durante el piloto, 4 abogados o periodistas de Medellín (H2).** Les damos el expediente de una obra del piloto y, sin explicarles nada, les pedimos que comprueben una foto con el validador. Después les preguntamos si lo usarían en un derecho de petición o una denuncia, y qué le falta.

**Las condiciones.** Cada participante firma un consentimiento informado y sabe que el piloto corre en la red de pruebas, así que sus evidencias todavía no tienen valor legal. El piloto tiene que terminar antes del 16 de diciembre de 2026: ese día la fundación de Stellar reinicia la testnet y borra los sellos.

**Qué hipótesis comprobamos y cuándo se cumplen.**

| Hipótesis | Se cumple si |
|---|---|
| H1. Un veedor reporta sin ayuda, como si mandara un mensaje. | 4 de 5 veedores envían su primer reporte en menos de 3 minutos, sin ayuda. Menos del 10 % de los reportes del piloto se rechazan por la geocerca. |
| H2. El sello hace la evidencia más creíble. | 3 de 4 abogados o periodistas dicen que usarían el expediente, y durante el piloto se radica al menos un derecho de petición o una denuncia con él. |
| H3. El ciudadano avisa sin cuenta y recibe respuesta. | Llegan 10 o más informes ciudadanos en 4 semanas, y el 70 % recibe respuesta en 5 días hábiles o menos. |
| H4. Sellar es rápido y barato. | El 95 % de los reportes queda "Sellado" en menos de un minuto, con una comisión media de 0,40 XLM o menos. |

**Qué hacemos con el resultado.** Si H1 o H2 fallan, corregimos el producto antes de pensar en la red principal: H1 es la condición para que los veedores lo usen, y H2 es la razón para que lo usen. Si H4 falla, el tope de sellos y el sello compacto pasan a ser lo primero.

---

## 4. Participación del equipo

El equipo quedó de una sola persona: Meliza Posada y Brayan Henao ya no hacen parte de él.

| Integrante | Usuario de GitHub | Aporte en este entregable |
|---|---|---|
| Cristhian Barros | [@cristhianbarros](https://github.com/cristhianbarros) | Todo el entregable. Diseñó las mejoras de esta semana (ubicación propuesta por el ciudadano, tarjeta del mapa, sugerencia de la veeduría y costos del servidor) y las dejó desplegadas en https://govtrace.duckdns.org, con el contrato de sellado en testnet. Preparó las dos veedurías de prueba (Medellín y Bogotá), grabó el video y escribió esta documentación. |
