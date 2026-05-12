# Imagen liviana de Nginx para servir frontend estático
FROM nginx:alpine

# Eliminar contenido por defecto de Nginx
RUN rm -rf /usr/share/nginx/html/*

# Copiar archivos del frontend
COPY index.html /usr/share/nginx/html/index.html
COPY app.js /usr/share/nginx/html/app.js

# Copiar configuración personalizada de Nginx
COPY default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80