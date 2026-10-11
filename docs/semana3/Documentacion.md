# Documentación: Functional Proof

**Proyecto:** GovTrace · **Front en línea (testnet):** https://govtrace.duckdns.org · **Código de la aplicación:** [github.com/cristhianbarros/govtrace-app](https://github.com/cristhianbarros/govtrace-app)

---

## 1. Front construido

<!-- Extensión total de la sección: 400 a 2000 palabras.
     Capturas en docs/semana3/img/<persona>/: se reemplaza el archivo provisional por el pantallazo, con el mismo nombre. -->

El front está desplegado en https://govtrace.duckdns.org, conectado a la testnet de Stellar. Cubre el recorrido básico del MVP definido en el Blueprint, de punta a punta: desde que el Super Administrador registra una veeduría hasta que un ciudadano comprueba en el validador que una evidencia no fue alterada.

| Paso del flujo (Blueprint, sección 3) | Pantallas | Responsable |
|---|---|---|
| 1. El Super Administrador registra la veeduría | Organizaciones, Nueva organización | Cristhian |
| 2. El administrador activa su cuenta, elige municipios e invita veedores | Crear contraseña, Territorio, Veedores | Cristhian |
| 3. Sincronización con el SECOP II | SECOP, Contratos | Cristhian |
| 4. El ciudadano envía un informe a la veeduría | Informar a esta veeduría | Meliza |
| 5. El administrador lee el informe y responde | Informes ciudadanos | Meliza |
| 6. El veedor busca la obra y envía el reporte | Crear contraseña, Iniciar sesión, Nuevo reporte, Mis reportes | Brayan |
| 7. El reporte se sella en Stellar | Sellado, Uso | Cristhian |
| 8. El administrador revisa y publica | Bandeja | Meliza |
| 9. El ciudadano ve la evidencia y la valida | Mapa, Página de la obra, Validador | Cristhian |

### 1.1 Alta de la veeduría, SECOP II y sellado (Cristhian)

| Paso | Pantalla | Qué muestra la captura |
|:---:|---|---|
| 1 | Organizaciones | La lista de veedurías registradas, cada una con su administrador y el estado de su invitación. |
| 1 | Nueva organización | El formulario: NIT con dígito de verificación, subdominio y administrador inicial. |
| 2 | Crear contraseña | El administrador activa su cuenta desde el enlace de la invitación. |
| 2 | Territorio | Los municipios que vigila la veeduría. |
| 2 | Veedores | La invitación de un veedor por correo y su estado. |
| 3 | SECOP | El estado de la sincronización diaria y el botón «Sincronizar ahora». |
| 3 | Contratos | Los contratos de obra del territorio que llegaron del SECOP II. |
| 7 | Sellado | El saldo en XLM de la cuenta patrocinadora, leído de la red. |
| 7 | Uso | Lo pagado en comisiones por organización. |

![Organizaciones](img/cristhian/p1-organizaciones.png)
![Nueva organización](img/cristhian/p1-nueva-organizacion.png)
![Crear contraseña del administrador](img/cristhian/p2-crear-contrasena.png)
![Territorio](img/cristhian/p2-territorio.png)
![Veedores](img/cristhian/p2-veedores.png)
![SECOP](img/cristhian/p3-secop.png)
![Contratos](img/cristhian/p3-contratos.png)
![Sellado](img/cristhian/p7-sellado.png)
![Uso](img/cristhian/p7-uso.png)

### 1.2 Informes ciudadanos y revisión de evidencias (Meliza)

| Paso | Pantalla | Qué muestra la captura |
|:---:|---|---|
| 4 | Informar a esta veeduría | El ciudadano escribe su correo, sin crear cuenta, y recibe un código de 6 dígitos. |
| 4 | Informar a esta veeduría (envío) | Con el código, el mensaje y las fotos opcionales, el informe se envía. |
| 5 | Informes ciudadanos | La lista de informes de la veeduría, sin el correo de quien los envió. |
| 5 | Responder un informe | La respuesta del administrador, que le llega al ciudadano por correo. |
| 8 | Bandeja | Las evidencias por revisar, con su obra, su municipio y quién la envió. |
| 8 | Publicar o rechazar | La decisión del administrador; el rechazo pide un motivo. |

![Informar a esta veeduría: correo y código](img/meliza/p4-informe-codigo.png)
![Informar a esta veeduría: envío](img/meliza/p4-informe-envio.png)
![Informes ciudadanos](img/meliza/p5-informes-ciudadanos.png)
![Responder un informe](img/meliza/p5-responder.png)
![Bandeja](img/meliza/p8-bandeja.png)
![Publicar o rechazar](img/meliza/p8-publicar-rechazar.png)

### 1.3 App del veedor (Brayan)

| Paso | Pantalla | Qué muestra la captura |
|:---:|---|---|
| 6 | Crear contraseña | El veedor activa su cuenta desde el enlace de la invitación. |
| 6 | Iniciar sesión | El ingreso desde el celular, en el sitio de su veeduría. |
| 6 | Nuevo reporte: la obra | La búsqueda por nombre, contratista o número de proceso, o las obras cercanas. |
| 6 | Nuevo reporte: qué vio | La clasificación (Avance, Retraso o Abandono) y la ubicación GPS. |
| 6 | Nuevo reporte: fotos y envío | Las fotos adjuntas y el botón de enviar. |
| 6 | Mis reportes | Cada reporte con su sello digital y su publicación por separado, y el enlace a su recibo. |

![Crear contraseña del veedor](img/brayan/p6-crear-contrasena.png)
![Iniciar sesión](img/brayan/p6-iniciar-sesion.png)
![Nuevo reporte: la obra](img/brayan/p6-reporte-obra.png)
![Nuevo reporte: qué vio](img/brayan/p6-reporte-que-vio.png)
![Nuevo reporte: fotos y envío](img/brayan/p6-reporte-fotos.png)
![Mis reportes](img/brayan/p6-mis-reportes.png)

### 1.4 Sitio público y validador (Cristhian)

| Paso | Pantalla | Qué muestra la captura |
|:---:|---|---|
| 9 | Mapa | Las obras de la veeduría como pines, con su estado. |
| 9 | Página de la obra | Los datos oficiales del contrato y las evidencias publicadas, cada una con el enlace a su sello. |
| 9 | Validador: auténtico | Una foto original: «Archivo Auténtico», con la fecha y el ledger del sello. |
| 9 | Validador: alterado | La misma foto retocada: «Alterado» o «No encontrado». |

![Mapa](img/cristhian/p9-mapa.png)
![Página de la obra](img/cristhian/p9-obra.png)
![Validador: auténtico](img/cristhian/p9-validador-autentico.png)
![Validador: alterado](img/cristhian/p9-validador-alterado.png)

---

## 2. Decisión técnica

**Opción elegida: A. Contrato propio.**

GovTrace necesita registrar en Stellar la huella de cada reporte de forma que nadie, ni siquiera nosotros, pueda antedatarla, cambiarla ni registrar un sello falso. Para eso creamos un contrato inteligente propio en Soroban (Rust), escrito desde cero: [`contracts/sealing`](https://github.com/cristhianbarros/govtrace-app/tree/main/contracts/sealing). Ya está escrito y desplegado en testnet como avance de la próxima semana.

**Qué hace el contrato.** Tiene tres funciones y nada más:

- `__constructor(sealer)`: al desplegarlo, fija para siempre cuál es la cuenta selladora de GovTrace.
- `seal(obra, raíz)`: guarda la raíz de Merkle del reporte (la huella de sus fotos y sus datos) con la referencia de la obra, el número de ledger y la hora que pone la red. Solo la cuenta selladora puede llamarla, y si la raíz ya estaba sellada la rechaza.
- `get_seal(raíz)`: cualquiera puede consultar si una huella está sellada y cuándo, sin cuenta y sin pasar por GovTrace.

No hay forma de modificar ni borrar un sello, de cambiar la cuenta selladora ni de reemplazar el código desplegado.

**Por qué un contrato propio y no el memo.** Primero evaluamos guardar la huella en el memo de una transacción normal. La huella cabe en el memo, pero no sirve para nuestro caso:

- **No impone reglas.** Cualquier cuenta puede enviar una transacción con cualquier memo, y la red no rechaza una huella repetida.
- **No se puede buscar por huella.** Para verificar habría que recorrer el historial de transacciones de la cuenta, y los nodos RPC solo guardan el historial reciente. El contrato, en cambio, guarda cada sello en el estado de la red y responde la consulta directamente.

También descartamos `manage_data`, que guarda datos en la propia cuenta: cada entrada sube la reserva mínima de la cuenta y hay un tope de entradas, así que no escala a miles de reportes.

**Cómo se paga la comisión.** La cuenta selladora firma cada sello y una cuenta patrocinadora, distinta, paga la comisión con una transacción *fee bump*, nativa de Stellar. Así el veedor no necesita billetera ni XLM, y la selladora no maneja fondos. Tenerlas separadas reduce el riesgo: si se filtrara la llave de la patrocinadora, nadie podría sellar con ella, porque el contrato solo acepta a la selladora.

---

## 3. Participación del equipo

El equipo es de tres personas.

| Integrante | Usuario de GitHub | Aporte en este entregable |
|---|---|---|
| Cristhian Barros | [@cristhianbarros](https://github.com/cristhianbarros) | Construyó y desplegó el front en https://govtrace.duckdns.org (testnet), junto con el contrato de sellado en Soroban. Documentó los pasos 1, 2, 3, 7 y 9 del flujo (alta de la veeduría, SECOP II, sellado, sitio público y validador), incluido el frente que tenía Camilo Hernández, que ya no hace parte del equipo. Redactó la decisión técnica, el README y la estructura de este documento, y organizó el reparto de pantallas. |
| Meliza Posada | [@Spathium](https://github.com/Spathium) | |
| Brayan Henao | [@brayanhenaoc](https://github.com/brayanhenaoc) | |

---

## 4. Bloqueos y siguiente paso

**Qué quedó pendiente**

- **El equipo pasó de cuatro a tres personas.** Las historias de Camilo Hernández (SECOP II, informe del ciudadano, mapa y validador) se repartieron entre Cristhian y Meliza. El alcance del MVP no cambió, pero queda menos gente para la misma carga.
- **El front vive en su propio repositorio** ([govtrace-app](https://github.com/cristhianbarros/govtrace-app)), no dentro de este. Este repositorio guarda la documentación del curso y enlaza al código y al despliegue.
- **Tres comprobaciones del contrato antes de la red principal:**
  - que el RPC devuelva un sello cuando su vigencia vence y la red lo archiva, porque si no lo devuelve habría que pagar para extender cada sello;
  - que la cuenta selladora no acumule los reembolsos de comisión;
  - que un analizador estático (Scout, de CoinFabrik) no encuentre problemas en el contrato.

**Siguiente paso hacia el MVP**

1. **Semana 4, contratos:** documentar el contrato que ya está desplegado en testnet, con su ID, sus tres funciones y sus pruebas (`make contract-test` y `make contract-smoke`), y mostrar un sello real consultado en Stellar Expert.
2. **Hacer las tres comprobaciones pendientes del contrato.**
3. **Hacer un piloto con una veeduría real en testnet:** reportes desde celulares en obras de verdad, para medir el costo real de cada sello y ajustar el flujo con lo que digan los veedores.

