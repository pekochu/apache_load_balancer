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

## Instalación

Instalación recomendada

```zsh
git clone https://github.com/pekochu/apache_load_balancer
# Utilicen la branch del HTTP_ONLY
git checkout http_only
# Creen sus contenedores
docker-compose up -d --build
# Configuren su nginx
sudo cp /PATH/TO/REPO/nginx/sites-available/default /etc/nginx/sites-available/.
# Linkeen el archivo a sites-enabled
ln -s /etc/nginx/sites-available/default /etc/nginx/sites-enabled/default
# Todo debería funcionar correctamente
```

***Si quieren configurar su SSL, vean el archivo docker-compose.yml para de la main branch para poder configurar los certificados en cada servidor apache y en el servidor de nginx***

## Dashboard: Grafana
Utilizamos Grafana para poder visualizar los recursos utilizados por cada contenedor Docker en el servidor. Se utilizaron los servicios `cAdvisor`, `prometheus`, `promtail` y `loki`. Importamos el dashboard de grafana con ID = `193`. Posteriormente lo modificamos para mostrar los logs de los servicios `apache` con Loki y Promtail en la parte posterior del dashboard. Se puede ingresar a través de [este link](//grafana.team.angelbrv.com). Para ingresar se necesita una cuenta de usuario de tipo `viewer`.

## Notas del desarrollo
Por favor, toma un vistazo a [nuestras notas](./NOTES.md). Contiene referencias y links utiles de los servicios que utilizamos.