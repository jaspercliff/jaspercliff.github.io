# minio

## docker compose 搭建

```
version: '3'
services:
  minio:
    image: "quay.io/minio/minio:RELEASE.2022-08-02T23-59-16Z"
    container_name: minio
    ports:
      - "9000:9000" # api 端口
      - "9001:9001" # 控制台端口
    environment:
      TZ: Asia/Shanghai # 时区上海
      MINIO_ROOT_USER: admin # 管理后台用户名
      MINIO_ROOT_PASSWORD: 123456789 # 管理后台密码，最小8个字符
      MINIO_SERVER_URL: "https://minio.mallchat.cn" # 指定分享的域名 告诉应用程序或服务，它应该连接到这个指定的URL来访问或存储对象数据
      MINIO_COMPRESS: "off" # 开启压缩 on 开启 off 关闭
      MINIO_COMPRESS_EXTENSIONS: "" # 扩展名 .pdf,.doc 为空 所有类型均压缩
      MINIO_COMPRESS_MIME_TYPES: "" # mime 类型 application/pdf 为空 所有类型均压缩
    volumes:
      - /data/minio/data:/data/ # 映射当前目录下的data目录至容器内/data目录  
      - /data/minio/config:/root/.minio/ # 映射配置目录
    command: server --address ':9000' --console-address ':9001' /data  # 指定容器中的目录 /data
    privileged: true
```

asd

## 基本概念

MinIO是一个高性能的对象存储服务，它是基于Apache License v2.0开源协议的。MinIO被设计用来存储非结构化数据，如照片、视频、日志文件、备份和容器/虚拟机映像。其接口兼容Amazon S3（Simple Storage Service）的云存储服务，这使得它可以用在许多需要大规模数据存储的场合。以下是MinIO的一些基本概念：

### 1. 对象存储

对象存储（Object Storage）是一种用于处理非结构化数据的存储架构，它管理数据作为一个对象，每个对象包含数据、元数据和全局唯一的标识符。MinIO将数据作为对象存储，这意味着可以存储任意大小的数据。

### 2. 存储桶（Buckets）

存储桶是用于组织存储空间的容器，在MinIO中用于存放对象。每个对象存储在一个存储桶内。存储桶可以被设定为公开或私有访问权限。

### 3. 对象（Objects）

对象是存储在MinIO中的基本单位，可以是任何形式的文件或数据。每个对象都包含数据和元数据，元数据包括对象的名称、大小、修改日期和其他描述信息。

### 4. 访问控制

MinIO支持细粒度的访问控制，可以为不同的用户和服务定义不同的访问权限。这包括对存储桶和对象的读写权限控制。

### 5. S3兼容API

MinIO提供了与Amazon S3兼容的API，这意味着可以使用S3的SDK和工具来与MinIO进行交互。这种兼容性使得MinIO可以轻松地集成到已经使用S3作为存储解决方案的应用程序中。

### 6. 分布式架构

MinIO可以配置为分布式模式，这允许它跨多台服务器分散存储数据，从而提高了容错能力和扩展性。分布式MinIO可以通过增加节点来水平扩展，以支持更大规模的存储需求。

### 7. 多租户支持

MinIO支持多租户环境，允许多个用户或组织在同一个MinIO实例上隔离地存储和管理数据。这通过使用前缀、存储桶策略和命名空间来实现数据的逻辑隔离。

MinIO以其高性能、简易部署、S3兼容性以及支持私有部署的特性，在企业和云原生环境中得到了广泛的应用。
