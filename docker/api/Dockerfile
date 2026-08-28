FROM node:18-alpine

WORKDIR /app

# Copia primeiro os manifests para otimizar o cache de camadas do Docker
COPY package*.json ./

RUN npm install

# Copia o restante do código da aplicação
COPY . .

EXPOSE 3000

CMD ["npm", "start"]