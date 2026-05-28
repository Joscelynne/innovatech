#etapa 1
#creo la maquina virtual
FROM node:18-alpine AS build
#creo el directorio de trabajo
WORKDIR /app
#copio el package.json al directorio de trabajo
COPY package*.json ./
#instalo las dependencias
RUN npm ci
#copio el resto de los archivos al directorio de trabajo
COPY . .
#compilamos el proyecto
RUN npm run build

#etapa 2
FROM nginx:alpine AS production

# copio los archivos compilados de la etapa 1 al directorio de nginx
COPY --from=build /app/dist /usr/share/nginx/html
# copio el archivo de configuracion de nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf

# exponemos el puerto 80
EXPOSE 80
# comando para iniciar nginx
CMD ["nginx", "-g", "daemon off;"]





