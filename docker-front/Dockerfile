# as front 设置别名 为后面从这COPY做准备
FROM node:lts-alpine as front
ENV NODE_ENV=development
WORKDIR /usr/src/app
COPY . .
RUN npm install --development --silent && mv node_modules ../
# # EXPOSE主要用于在构建阶段声明容器需要使用的端口，而ports主要用于在运行阶段定义主机和容器之间的端口映射关系
# # EXPOSE 5173
RUN chown -R node /usr/src/app
USER node
RUN npm run build

FROM nginx:latest
# USER root
COPY --from=front /usr/src/app/dist /usr/share/nginx/html
EXPOSE 80

CMD ["nginx","-g","daemon off;"]