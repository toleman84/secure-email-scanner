# Imagen base ligera con Postfix
FROM debian:bullseye-slim

# Mantendor profesional
LABEL maintainer="gdponcemarsiglia@gmail.com"
LABEL description="Secure Postfix server configured for external scanning"

# Instalar Postfix y utilidades necesarias
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    postfix \
    ca-certificates \
    libsasl2-modules \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Crear estrucutura de trabajo
RUN mkdir -p /etc/postfix

# Copiar configuraciones de Postfix personalizadas
COPY main.cf /etc/postfix/main.cf
COPY master.cf /etc/postfix/master.cf

# Variables de entorno (opcional para parametrizar el dominio, et. pueden sobreescribirse en docker-compose)
ENV MAIL_DOMAIN=securemail.local

# Exponer el puerto SMTP
EXPOSE 25

# Comando por defecto para ejecutar Postfix en foreground
CMD ["sh", "-c", "postfix start-fg"]

# Para ejecutar el contenedor, usar el siguiente comando:
# docker run -d -p 25:25 --name postfix_server -v /path/to/postfix:/etc/postfix postfix_server

# Para ejecutar el contenedor en modo interactivo, usar el siguiente comando:
# docker run -it --rm -p 25:25 --name postfix_server -v /path/to/postfix:/etc/postfix postfix_server

# Para ejecutar el contenedor en modo interactivo y acceder a la consola de Postfix, usar el siguiente comando:
# docker run -it --rm -p 25:25 --name postfix_server -v /path/to/postfix:/etc/postfix postfix_server /bin/bash
