FROM python:3.10

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git wget node-less \
    libpq-dev libxml2-dev libxslt1-dev \
    libjpeg-dev libldap2-dev libsasl2-dev \
    libffi-dev libssl-dev \
    wkhtmltopdf \
    && apt-get clean

# Create odoo user
RUN useradd -m -d /opt/odoo -U -r -s /bin/bash odoo

# Copy the source code into the image
COPY ./odoo-custom /opt/odoo/odoo
WORKDIR /opt/odoo/odoo

#
#Install Python requirements
RUN pip install -r requirements.txt

# Set permissions
RUN chown -R odoo:odoo /opt/odoo

USER odoo

CMD ["./odoo-bin", "-c", "/etc/odoo/odoo.conf"]