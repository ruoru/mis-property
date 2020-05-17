# node镜像仅仅是用来打包文件
FROM node:alpine as builder

ENV PROJECT_ENV production
ENV NODE_ENV production

COPY package*.json /webroot/

WORKDIR /webroot

RUN npm install

COPY . /webroot

RUN npm run build

# 选择更小体积的基础镜像
FROM nginx:alpine

COPY nginx.conf /etc/nginx/conf.d/default.conf

COPY --from=builder /webroot/build /webroot/mis-property-web

RUN chmod -R 777 /webroot/mis-property-web/

# CMD ["nginx", "-g"]

## 单镜像构建

# # 基于node12
# FROM node:12

# # 设置环境变量
# ENV PROJECT_ENV production
# ENV NODE_ENV production

# # 安装nginx
# RUN apt-get update && apt-get install -y nginx

# # 把 package.json package-lock.json 复制到/webroot目录下
# # 为了npm install可以缓存
# COPY package*.json /webroot/

# # 切换到app目录
# WORKDIR /webroot

# # 安装依赖
# RUN npm install

# # 把所有源代码拷贝到/app
# COPY . /webroot

# # 打包构建
# RUN npm run build

# # 拷贝配置文件到nginx
# COPY nginx.conf /etc/nginx/conf.d/default.conf

# EXPOSE 80

# # 启动nginx，关闭守护式运行，否则容器启动后会立刻关闭
# CMD ["nginx", "-g", "daemon off;"]
