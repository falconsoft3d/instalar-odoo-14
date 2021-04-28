# Instalación de Odoo 14 CE

Marlon Falcón Hernández | Madrid, España
- ERP, CRM y Software
- WhatsApp: +34 662 47 06 45
- Telegram: falconsoft
- Email: mfalconsoft@gmail.com , falconsoft.3d@gmail.com
- Github: https://github.com/falconsoft3d
- linkedin: https://linkedin.com/in/marlon-falcón-3a2aa9a4


![Alt text](https://github.com/falconsoft3d/instalar-odoo-10/blob/master/img/logo-ynext.png?raw=true "Ynext")

## 0- Creamos una cuenta en Digital Ocean
https://m.do.co/c/7f5c3af8d6bb


## 1- Actualizamos el sistema

```linux
apt-get update && apt-get upgrade -y
```

## 2- Instalamos odoo 14
```linux
wget -O - https://nightly.odoo.com/odoo.key | apt-key add -
echo "deb http://nightly.odoo.com/14.0/nightly/deb/ ./" >> /etc/apt/sources.list
apt-get update && apt-get install odoo
```


## 3 - Instalamos ngix para cambiar el puerto
```linux
sudo apt-get install nginx -y
cd /etc/nginx/sites-available
git clone https://github.com/falconsoft3d/ngix-para-odoo-erp/
cd ngix-para-odoo-erp/
sudo cp /etc/nginx/sites-available/ngix-para-odoo-erp/default.conf /etc/nginx/sites-available/default.conf
cd ..
mv default default-temp
mv default.conf default

cd /etc/nginx/sites-available
nano default
server_name j.wemakeyourdayeasy.com 11.64.123.12;
nginx -s reload
```

## 4 - Creamos Carpeta Extra-addons
```linux
mkdir /opt/extra-addons
chown odoo: /opt/extra-addons/ -R
```

## 5 - Creamos Carpeta Respaldos
```linux
mkdir /opt/backup
chown odoo: /opt/backup/ -R
```


## 6- Instalar wkhtmltopdf para generar PDF en odoo
```
wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.focal_amd64.deb
dpkg -i wkhtmltox_0.12.5-1.focal_amd64.deb
apt install -f
```

# 7- Configuramos el conf de odoo
```
nano /etc/odoo/odoo.conf
limit_time_real = 360
```

# 8- Tools
```
service odoo restart
tail -f /var/log/odoo/odoo-server.log
```

# 9- Generamos la clave publica
```
ssh-keygen
cat ~/.ssh/id_rsa.pub
```
# 9a- Librerias complementarias
```
sudo pip3 install paramiko
sudo pip3 install xmltodict
sudo pip3 install xmlsig
sudo pip3 install num2words
sudo pip3 install pandas
sudo pip3 install phonenumbers
```

# 10- Instalamos las librerias de Python
```
pip3 install xmltodict
pip3 install dicttoxml
pip3 install cchardet
pip3 install cryptography
sudo pip3 install pyOpenSSL
6) M2Crypto
  - sudo apt-get install python-m2crypto
  - sudo apt-get install libssl-dev swig python3-dev gcc
  - sudo pip3 install M2Crypto
sudo pip3 install SOAPpy
sudo pip3 install signxml
sudo pip3 install pdf417gen
```

# 10b- Instalando m2crypto en MAC.
```
$> brew install openssl
$> brew install swig
$> env LDFLAGS="-L$(brew --prefix openssl)/lib" \
CFLAGS="-I$(brew --prefix openssl)/include" \
SWIG_FEATURES="-cpperraswarn -includeall -I$(brew --prefix openssl)/include" \
pip install m2crypto
```


```
pip3 install pycrypto
```
```
sudo apt-get install python-m2crypto
```

# 10- Instalando el certificado digital ( https://certbot.eff.org/lets-encrypt/ubuntuxenial-nginx )
```
sudo apt-get update
sudo apt-get install software-properties-common
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install python-certbot-nginx

sudo certbot --nginx
-A
- 2
Dentro de Odoo configuras los parámetros.
Configuración > Parámetros > Parámetros del sistema

web.base.url
http -> https

web.base.url.freeze
True
```

# 11- buscamos los repos oficiales de odoo
```
mkdir /opt/extra-addons-odoo
chown odoo: /opt/extra-addons-odoo/ -R
cd /opt/extra-addons-odoo/
git clone https://github.com/odoo/odoo.git
git checkout 14.0
```

# 12- Actualizar Odoo all
```
/etc/init.d/odoo stop
su - odoo -s /bin/bash
odoo -d db11-spain -u all --stop-after-init --logfile=/dev/stdout
/etc/init.d/odoo start
```

# 13- Buscar Odoo en Linux
```
find / -name "odoo"
```

# 14- Shell Odoo
```
/etc/init.d/odoo stop
su - odoo -s /bin/bash
odoo shell -d db11-spain

mod=env['ir.module.module'].search([('name','=','purchase_request')])
print(mod)

products=env['product.template'].search([('type', '=', 'consu')])
for product in products:
    try:
        print(product.id)
        print('Modificando')
        product.type = 'product'
    except:
        print('error')

env.cr.commit()

/etc/init.d/odoo start
```


conf
```
addons_path = /usr/lib/python3/dist-packages/odoo/addons,/opt/extra-addons/addons_general,/opt/extra-addons/addons_3ros,/opt/extra-addons/credit
admin_passwd = $pbkdf2-sha512$25000$1poTYiylFOKcs3YuxVgLYQ$EJYtGA5.NwOm0V.VRXhSnCD7SvB30Q1prQ7MA.uzbfKVPRbwihg0eukjNP4wikRdnHYiXrcoOM75fhT6fuspzQ
csv_internal_sep = ,
data_dir = /var/lib/odoo/.local/share/Odoo
db_host = False
db_maxconn = 64
db_name = False
db_password = False
db_port = False
db_sslmode = prefer
db_template = template0
db_user = odoo
dbfilter =
demo = {}
email_from = False
geoip_database = /usr/share/GeoIP/GeoLite2-City.mmdb
http_enable = True
http_interface =
http_port = 8069
import_partial =
limit_memory_hard = 2684354560
limit_memory_soft = 2147483648
limit_request = 8192
limit_time_cpu = 60
limit_time_real = 120
limit_time_real_cron = -1
list_db = True
log_db = False
log_db_level = warning
log_handler = :INFO
log_level = info
logfile = /var/log/odoo/odoo-server.log
longpolling_port = 8072
max_cron_threads = 2
osv_memory_age_limit = False
osv_memory_count_limit = False
pg_path =
pidfile =
proxy_mode = False
reportgz = False
screencasts =
screenshots = /tmp/odoo_tests
server_wide_modules = base,web
smtp_password = False
smtp_port = 25
smtp_server = localhost
smtp_ssl = False
smtp_user = False
syslog = False
test_enable = False
test_file =
test_tags = None
transient_age_limit = 1.0
translate_modules = ['all']
unaccent = False
upgrade_path =
without_demo = False
workers = 0
```

```
proxy_mode = True
longpolling_port = 8072
xmlrpc_port = 8069
xmlrpc_interface = 127.0.0.1
netrpc_interface = 127.0.0.1

workers = 17
limit_time_real = 1200
limit_time_cpu = 600
```

# Log en el odoo.conf
```
log_level = info
(choose from 'info', 'debug_rpc', 'warn', 'test', 'critical', 'runbot', 'debug_sql', 'error', 'debug', 'debug_rpc_answer', 'notset')
```

# Ver el log
```
tail -f /var/log/odoo/odoo-server.log
Trae las 50 lineas antes de ese Error
grep "2021-04-28 06:55:52,330 43141" /var/log/odoo/odoo-server.log -B 50
```
