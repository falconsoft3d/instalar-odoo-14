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
sudo wget http://se.archive.ubuntu.com/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1_amd64.deb
sudo dpkg -i libpng12-0_1.2.54-1ubuntu1_amd64.deb

sudo wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.1/wkhtmltox-0.12.1_linux-trusty-amd64.deb
sudo dpkg -i wkhtmltox-0.12.1_linux-trusty-amd64.deb
sudo cp /usr/local/bin/wkhtmltopdf /usr/bin
sudo cp /usr/local/bin/wkhtmltoimage /usr/bin
```

## 6a- Instalar wkhtmltopdf para generar PDF en odoo
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
