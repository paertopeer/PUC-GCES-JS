# Usa uma imagem base do Node.js
FROM node:14 as build

# Define o diretório de trabalho dentro do contêiner
WORKDIR /app

# Copia o arquivo package.json para o diretório de trabalho
COPY package.json .

# Instala as dependências do projeto
RUN npm install

# Copia todo o conteúdo do diretório atual para o diretório de trabalho
COPY . .

# Expõe a porta 3000 para acesso externo
EXPOSE 3000

# Define o comando de inicialização do contêiner
RUN npm run build


# Estágio de produção
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
