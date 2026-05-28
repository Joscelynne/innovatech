#etapa 1
#creo la maquina virtual
FROM maven:3.8.4-openjdk-17 AS build
#creo el directorio de trabajo
WORKDIR /app
#copio el pom.xml al directorio de trabajo
COPY pom.xml ./
#descargo las dependencias
RUN mvn dependency:go-offline 
#copio el resto de los archivos al directorio de trabajo
COPY src ./src
#compilamos el proyecto
RUN mvn clean package -DskipTests

#etapa 2
#creacion de la imagen
FROM eclipse-temurin:17-jre-alpine AS production
# crear usuario no root
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

WORKDIR /app
#copio el jar compilado de la etapa 1 al directorio de trabajo
COPY --from=build /app/target/*.jar app.jar
# permisos
RUN chown -R appuser:appgroup /app

# usar usuario no root
USER appuser
#exponemos el puerto 8080
EXPOSE 8080
#comando para iniciar la aplicacion
ENTRYPOINT ["java", "-jar", "app.jar"]


