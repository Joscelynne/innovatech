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
#creacion de la imagen
FROM nginx:alpine AS production
#copio los archivos compilados de la etapa 1 al directorio de nginx
#se queda solamente el compilado y no el codigo fuente
COPY --from=build /app/dist /usr/share/nginx/html
#exponemos el puerto 80
EXPOSE 80
#comando para iniciar nginx
CMD ["nginx", "-g", "daemon off;"]





