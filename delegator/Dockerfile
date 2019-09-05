FROM nginx:alpine
COPY nginx/default.conf /etc/nginx/conf.d/default.conf
COPY /app /usr/share/nginx/html
EXPOSE 80
# CMD ["nginx", "-g", "daemon off;"]
ENTRYPOINT ["nginx","-g","daemon off;"]