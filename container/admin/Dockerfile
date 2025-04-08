FROM python:3.10

# System dependencies
RUN apt-get update && apt-get install -y \
    git wget xfonts-75dpi xfonts-base \
    libpq-dev libxml2-dev libxslt1-dev \
    libjpeg-dev libldap2-dev libsasl2-dev \
    libffi-dev libssl-dev \
    && rm -rf /var/lib/apt/lists/*

# Install wkhtmltopdf (patched version)
RUN wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox_0.12.6-1.buster_amd64.deb && \
    apt-get update && apt-get install -y ./wkhtmltox_0.12.6-1.buster_amd64.deb && \
    rm wkhtmltox_0.12.6-1.buster_amd64.deb

# Create odoo user
RUN useradd -m -d /opt/odoo -U -r -s /bin/bash odoo

# Copy Odoo source code (adjust path depending on build context)
COPY ../.. /opt/odoo
WORKDIR /opt/odoo

# Install Python dependencies
RUN pip install --upgrade pip && \
    if [ -f requirements.txt ]; then pip install -r requirements.txt; fi

# Set ownership
RUN chown -R odoo:odoo /opt/odoo

# Switch to non-root user
USER odoo

# Run Odoo
CMD ["python3", "odoo-bin", "-c", "/etc/odoo/odoo.conf"]
