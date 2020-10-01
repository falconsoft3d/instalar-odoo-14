# Instalación de Odoo 12

Marlon Falcón Hernández | Madrid, España
- ERP, CRM y Software
- WhatsApp: +34 662 47 06 45
- Telegram: falconsoft
- Email: mfalconsoft@gmail.com , falconsof.3d@gmail.com
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
echo "deb http://nightly.odoo.com/11.0/nightly/deb/ ./" >> /etc/apt/sources.list
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
chown odoo: /opt/odoo/ -R
```

## 5- Instalar wkhtmltopdf para generar PDF en odoo
```linux
sudo wget http://se.archive.ubuntu.com/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1_amd64.deb
sudo dpkg -i libpng12-0_1.2.54-1ubuntu1_amd64.deb
```

```linux
sudo wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.1/wkhtmltox-0.12.1_linux-trusty-amd64.deb
sudo dpkg -i wkhtmltox-0.12.1_linux-trusty-amd64.deb
sudo cp /usr/local/bin/wkhtmltopdf /usr/bin
sudo cp /usr/local/bin/wkhtmltoimage /usr/bin
```

# 6- configuramos el conf de odoo
```linux
nano /etc/odoo/odoo.conf
```

# Tools
```linux
service odoo restart
tail -f /var/log/odoo/odoo-server.log
```


