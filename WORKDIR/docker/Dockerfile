FROM node:20
EXPOSE 8080
ENV DB_HOST="mysql"
RUN mkdir /opt/server
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install
CMD ["node", "index.js"]


-------

FROM node:20 AS builder
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install


FROM node:20.18.0-alpine3.20
EXPOSE 8080
ENV DB_HOST="mysql"
RUN addgroup -S user && adduser -S user -G user && \
    mkdir /opt/server && \
    chown -R user:user /opt/server
WORKDIR /opt/server
COPY --from=builder /opt/server /opt/server
USER user
CMD ["node", "index.js"]