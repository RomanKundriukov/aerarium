# Basis-Image für den Build
FROM node:22 AS builder

# Arbeitsverzeichnis setzen
WORKDIR /app

# Abhängigkeiten kopieren und installieren
COPY package.json package-lock.json ./
RUN npm install

# Den gesamten Code kopieren und das Frontend bauen
COPY . .
RUN npm run build

# Basis-Image für die Bereitstellung mit Nginx
FROM nginx:alpine

# Build-Ergebnisse in Nginx-Ordner kopieren
COPY --from=builder /app/dist /usr/share/nginx/html

# Exponiere Port 80 für den Webserver
EXPOSE 80

# Startbefehl (nginx läuft automatisch)
CMD ["nginx", "-g", "daemon off;"]