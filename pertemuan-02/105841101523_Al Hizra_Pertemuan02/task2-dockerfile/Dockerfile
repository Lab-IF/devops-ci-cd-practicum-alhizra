FROM nginx:alpine
# Karena index.html kamu ada di folder DEV, kita copy langsung
COPY index.html /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
