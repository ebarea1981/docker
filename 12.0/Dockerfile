FROM odoo:12.0
MAINTAINER Fabrica de Software Libre <info@fslibre.com>

user root

RUN apt-get update
RUN set -x; \
        apt-get install -y --no-install-recommends \
            default-jdk \
            default-jre

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
