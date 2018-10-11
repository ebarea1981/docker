FROM debian:jessie
MAINTAINER Odoo S.A. <info@odoo.com>

# Install some deps, lessc and less-plugin-clean-css, and wkhtmltopdf
RUN apt-get update

RUN set -x; \
        apt-get install -y --no-install-recommends \
            wget \
            curl \
            python \
            ca-certificates

RUN wget --no-check-certificate https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py

RUN set -x; \
        apt-get install -y --no-install-recommends \
            node-less \
            python-gevent \
            python-renderpm \
            python-support \
            python-watchdog \
            python-pandas \
            libpng-dev \
            zlib1g-dev \
            cabextract \
            fonts-liberation \
            vim \
            nano \
            default-jdk \
            default-jre  \
        && curl -o wkhtmltox.deb -SL http://nightly.odoo.com/extra/wkhtmltox-0.12.1.2_linux-jessie-amd64.deb \
        && echo '40e8b906de658a2221b15e4e8cd82565a47d7ee8 wkhtmltox.deb' | sha1sum -c - \
        && dpkg --force-depends -i wkhtmltox.deb \
        && apt-get -y install -f --no-install-recommends \
        && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false -o APT::AutoRemove::SuggestsImportant=false npm \
        && rm -rf /var/lib/apt/lists/* wkhtmltox.deb

RUN set -x; \
        pip install psycogreen==1.0 \
        && pip install xmltodict \
           openpyxl \
           xlsxwriter \
           xlrd \
           simplejson \
           odoorpc \
           checksumdir \
           xlutils \
           openupgradelib \ 
           ofxparse \
           pyserial \
           pyusb>=1.0.0b1 \
           qrcode \
           suds-jurko \
           python-chart

# MS Fonts.
RUN echo "deb http://gce_debian_mirror.storage.googleapis.com wheezy contrib non-free" >> /etc/apt/sources.list \
  && echo "deb http://gce_debian_mirror.storage.googleapis.com wheezy-updates contrib non-free" >> /etc/apt/sources.list \
  && echo "deb http://security.debian.org/ wheezy/updates contrib non-free" >> /etc/apt/sources.list
RUN apt-get update

RUN echo ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula \
    select true | debconf-set-selections

RUN apt-get install --no-install-recommends -y -q \
    ttf-mscorefonts-installer

# Install Odoo
ENV ODOO_VERSION 9.0
ENV ODOO_RELEASE 20170815
RUN set -x; \
        curl -o odoo.deb -SL http://nightly.odoo.com/${ODOO_VERSION}/nightly/deb/odoo_${ODOO_VERSION}c.${ODOO_RELEASE}_all.deb \
        && echo '3d3b34cbbcd5f3fb739e85a2c855955322c0f328 odoo.deb' | sha1sum -c - \
        && dpkg --force-depends -i odoo.deb \
        && apt-get update \
        && apt-get -y install -f --no-install-recommends \
        && rm -rf /var/lib/apt/lists/* odoo.deb

# Instalamos zeep al terminar para no tener errores de compilación.
RUN pip install zeep
RUN pip install pyzk
RUN pip install viivakoodi
RUN pip install num2words

# Copy entrypoint script and Odoo configuration file
COPY ./entrypoint.sh /
COPY ./openerp-server.conf /etc/odoo/
RUN chown odoo /etc/odoo/openerp-server.conf

COPY ./patch/ /usr/lib/python2.7/dist-packages/openerp/

RUN rm -r /usr/lib/python2.7/dist-packages/openerp/addons/base_vat
# Mount /var/lib/odoo to allow restoring filestore and /mnt/extra-addons for users addons
RUN mkdir -p /mnt/extra-addons \
        && chown -R odoo /mnt/extra-addons
VOLUME ["/var/lib/odoo", "/mnt/extra-addons"]

# Expose Odoo services
EXPOSE 8069 8071 8072

# Set the default config file
ENV OPENERP_SERVER /etc/odoo/openerp-server.conf

# Set default user when running the container
USER odoo

ENTRYPOINT ["/entrypoint.sh"]
CMD ["openerp-server"]
