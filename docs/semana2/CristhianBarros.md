# Historias de usuario individuales

**Nombre:** Cristhian Barros

**Usuario de GitHub:** cristhianbarros

**Mi frente:** el Super Administrador, que opera la plataforma y el sellado en Stellar.

---

## Mis historias de usuario

1. Como Super Administrador quiero registrar una veeduría u ONG con su nombre y su NIT y asignarle su propio subdominio, para habilitarla en GovTrace y que nadie se haga pasar por ella.
2. Como Super Administrador quiero asignar el administrador inicial de cada veeduría, para que ella gestione su propio equipo sin depender de nosotros.
3. Como Super Administrador quiero desplegar en Stellar el contrato inteligente de sellado, en el que solo la cuenta selladora de GovTrace puede escribir, para que nadie registre sellos falsos.
4. Como Super Administrador quiero que la huella de cada reporte recibido se registre en ese contrato y que la cuenta patrocinadora de GovTrace pague la comisión, para que los veedores no tengan que manejar criptomonedas.
5. Como Super Administrador quiero ver el saldo de la cuenta patrocinadora y lo que se ha pagado en comisiones, para recargarla a tiempo y saber cuánto cuesta el sellado.

## La más importante y por qué

| Orden de importancia | Historia # | Por qué |
| :---: | :---: | --- |
| 1 (la más importante) | 4 | Es el corazón del proyecto. Sin el registro en Stellar la foto sigue siendo un archivo que cualquier abogado puede tachar de editado, que es justo la fragilidad probatoria del Problem Brief. |
| 2 | 3 | Si cualquiera pudiera escribir en el contrato, los sellos no valdrían nada. Es la base de la confianza en todo lo que se sella. |
| 3 | 1 | Es la puerta de entrada de cada organización. Validar el NIT protege a las veedurías serias de la suplantación. |
| 4 | 2 | Le entrega a la veeduría el control de su equipo. Sin esto, cada veedor tendría que pasar por nosotros. |
| 5 (la menos importante) | 5 | Si la cuenta se queda sin saldo el sellado se detiene, pero al principio el volumen es bajo y se puede revisar a mano. |
