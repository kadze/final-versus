FROM python:3.7-slim

ENV PYTHONUNBUFFERED=1

WORKDIR /backend

COPY requirements.txt .

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        default-libmysqlclient-dev \
        gcc \
    && pip install --no-cache-dir -r requirements.txt \
    && apt-get purge -y --auto-remove gcc \
    && rm -rf /var/lib/apt/lists/*

COPY . .

EXPOSE 8080
ENTRYPOINT ["gunicorn", "-w", "4", "main.wsgi:application", "-b", "0.0.0.0:8080"]
