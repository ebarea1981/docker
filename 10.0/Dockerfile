FROM odoo:10.0
MAINTAINER FSLIBRE <desarrollo@fslibre.com>

user root

RUN apt-get update

RUN set -x; \
        pip3 install \
	        zeep \
            xmltodict \
            odoorpc \
            openupgradelib \
            openpyxl \
            pyzk \
            viivakoodi \
            raven \
            email_validator \
            phonenumbers
user odoo
