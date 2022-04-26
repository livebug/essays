# docker 配置Nodejs开发环境

## 配置私有npm库

详见 [Running Verdaccio using Docker](./docker%20Verdaccio%E9%95%9C%E5%83%8F(docker%20run%20%E5%91%BD%E4%BB%A4).md)

注意：` docker network  inspect bridge` 查看 Verdaccio 容器地址


## 拉取镜像并启动

    docker pull node:16.14.2 # LTS版本

    docker run -itd --name node-dev node:16.14.2 # 启动

## 配置NPM源为 私有库

    npm set registry http://localhost:4873/  # localhost 换为 Verdaccio 容器地址

## 试运行

     npm install -g @angular/cli

能成功运行即可