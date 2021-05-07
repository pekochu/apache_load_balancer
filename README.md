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

```bash
git clone https://github.com/pekochu/apache_load_balancer
# Utilicen la branch del HTTP_ONLY
git checkout http_only
# Creen sus contenedores
docker-compose up -d --build
# Configuren su nginx
sudo cp /PATH/TO/REPO/nginx/sites-available/default /etc/nginx/sites-available/.
# Linkeen el archivo a sites-enabled
ln -s /etc/nginx/sites-available/default /etc/nginx/sites-enabled/default
# Reiniciar nginx
systemctl restart nginx
# Arreglar los permisos
cd httpd
chown -R www-data:www-data htdocs
```

## Para instalar Grafana
```bash
# Distro red hat
yum install httpd
wget https://dl.grafana.com/oss/release/grafana-7.5.5-1.x86_64.rpm
sudo yum install grafana-7.5.5-1.x86_64.rpm
# Distro basada en debian
sudo apt install -y adduser libfontconfig1 apache2
wget https://dl.grafana.com/oss/release/grafana_7.5.5_amd64.deb
sudo dpkg -i grafana_7.5.5_amd64.deb
```

## Para utilizar el certificado SSL
```bash
# Para más info vayan a https://acme.sh
sudo apt install -y socat
curl https://get.acme.sh | sh -s email=my@example.com
acme.sh --issue --nginx -d example.com --keylength ec-384 -w /var/www/html
# Linkeen los archivos a donde lo necesiten
ln -s /root/.acme.sh/example.com_ecc/fullchain.cer .
ln -s /root/.acme.sh/example.com_ecc/example.com.cer .
ln -s /root/.acme.sh/example.com_ecc/example.com.key .
# Usan la rama que esta lista para SSL
git checkout main
# Reiniciar contenedores
docker-compose up -d
# Copiar nuevamente el archivo default
sudo cp /PATH/TO/REPO/nginx/sites-available/default /etc/nginx/sites-available/.
# Reiniciar nginx
systemctl restart nginx
# Ya debería funcionar el HTTPS
```

## Dashboard: Grafana
Utilizamos Grafana para poder visualizar los recursos utilizados por cada contenedor Docker en el servidor. Se utilizaron los servicios `cAdvisor`, `prometheus`, `promtail` y `loki`. Importamos el dashboard de grafana con ID = `193`. Posteriormente lo modificamos para mostrar los logs de los servicios `apache` con Loki y Promtail en la parte posterior del dashboard. Se puede ingresar a través de [este link](//grafana.team.angelbrv.com). Para ingresar se necesita una cuenta de usuario de tipo `viewer`.

## Notas del desarrollo
Por favor, toma un vistazo a [nuestras notas](./NOTES.md). Contiene referencias y links utiles de los servicios que utilizamos.