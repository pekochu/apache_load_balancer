# Administración de Servicios en Red

Escuela Superior de Cómputo - IPN
Grupo: 4CV4

Miembros:
- Aguilar Morales Marco Antonio
- Bravo López Luis Ángel
- Salinas Franco Carlos Enrique
- Rodríguez Lara Oscar Jair
- Rueda Espinosa Edwin
- Torres Rosas Ricardo Erick

## Equipo 1: Servicio web
Balanceador de carga con nginx como frontend y tres servidores apache en contenedores Docker como upstreams backend. El servicio nginx está encargado de cifrar las peticiones con un certificado de tipo de cifrado `ECDSA`, sin redirigir a HTTPS. Cada servidor tiene también este mismo certificado HTTPS para cifrar las peticiones entre el servicio nginx y cada servicio apache. Se puede ingresar a través de [este link](//team.angelbrv.com). Aún no nos hemos puesto de acuerdo en cuanto a qué aplicación hostearemos en estos servicios.

## Dashboard: Grafana
Utilizamos Grafana para poder visualizar los recursos utilizados por cada contenedor Docker en el servidor. Se utilizaron los servicios `cAdvisor`, `prometheus`, `promtail` y `loki`. Importamos el dashboard de grafana con ID = `193`. Posteriormente lo modificamos para mostrar los logs de los servicios `apache` con Loki y Promtail en la parte posterior del dashboard. Se puede ingresar a través de [este link](//grafana.team.angelbrv.com). Para ingresar se necesita una cuenta de usuario de tipo `viewer`.

## Localización del servidor
El servidor está ubicado en el algún lugar de Alemania, por lo que el ping puede llegar a ser de `~130ms`. 

## Notas del desarrollo
Por favor, toma un vistazo a [nuestras notas](./NOTES.md). Contiene referencias y links utiles de los servicios que utilizamos.