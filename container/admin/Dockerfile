FROM python:3.10

# Làm việc trong thư mục Odoo
WORKDIR /opt/odoo

# Cài đặt thư viện hệ thống cần thiết
RUN apt-get update && apt-get install -y \
    git \
    build-essential \
    libpq-dev \
    libxml2-dev \
    libxslt1-dev \
    zlib1g-dev \
    libsasl2-dev \
    libldap2-dev \
    libssl-dev \
    libjpeg-dev \
    libffi-dev \
    && rm -rf /var/lib/apt/lists/*

# Cài các gói Python cần thiết
COPY ../../odoo-src/requirements.txt ./requirements.txt
RUN pip install --no-cache-dir -r requirements.txt || true
RUN pip install pypdf

# Copy file cấu hình
COPY ../../odoo.conf ./odoo.conf

# Lệnh chạy chính
CMD ["python", "odoo-src/odoo-bin", "-c", "odoo.conf"]
