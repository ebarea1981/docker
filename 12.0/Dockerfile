FROM fslibre/odoo:12.2.0
MAINTAINER Odoo S.A. <info@odoo.com>

USER root

RUN apt-get update
RUN apt-get install -y wget
RUN sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt stretch-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -

RUN set -x; \
    apt-get update \
    && apt-get install -y --no-install-recommends \
        postgresql-client-12 \
        libpcap-dev \
        libpq-dev=12.3-1.pgdg90+1 \
        build-essential
            
RUN pip3 install ftpretty
RUN python3 -m pip install --upgrade psycopg2

USER odoo
