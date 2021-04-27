# 单词拼写

**中文** | [English](./README_EN.md)

## 简介

本项目使用虚拟键盘以支持单个字母的不同颜色高亮

虚拟键盘使用 [vue-touch-keyboard](https://github.com/icebob/vue-touch-keyboard) 开源项目

[在线预览](https://my-vue-starter-1255906278.cos-website.ap-guangzhou.myqcloud.com)（移动端访问效果更佳）

### 功能说明

虚拟键盘 **暂不支持** PC 键盘或者 iPad 外接键盘的输入

虚拟键盘上方附着部分功能键

字母拼写错误不能往前继续拼写（此处有 BUG），再输入字母会覆盖错误的字幕

字母拼写会绿色高亮正确字母，橙色错误字母

拼写完成后收起键盘

> 本项目模板使用 Tencent SCF 组件及其触发器能力，方便的在腾讯云创建，配置和管理一个 vue-starter 应用。

## 快速开始

### 1. 安装

```bash
# 安装 Serverless Framework
npm install -g serverless
```

### 2. 创建

通过如下命令直接下载该例子：

```bash
serverless init vue-starter --name example
cd example
```

### 3. 部署

在 `serverless.yml` 文件所在的项目根目录，运行以下指令，将会弹出二维码，直接扫码授权进行部署：

```bash
serverless deploy
```

> **说明**：如果鉴权失败，请参考 [权限配置](https://cloud.tencent.com/document/product/1154/43006) 进行授权。

### 4. 查看状态

执行以下命令，查看您部署的项目信息：

```bash
serverless info
```

### 5. 移除

可以通过以下命令移除 vue-starter 应用

```bash
serverless remove
```

### 账号配置（可选）

serverless 默认支持扫描二维码登录，用户扫描二维码后会自动生成一个 `.env` 文件并将密钥存入其中.
如您希望配置持久的环境变量/秘钥信息，也可以本地创建 `.env` 文件,
把从[API 密钥管理](https://console.cloud.tencent.com/cam/capi)中获取的 `SecretId` 和`SecretKey` 填入其中.

> 如果没有腾讯云账号，可以在此[注册新账号](https://cloud.tencent.com/register)。

```bash
# 腾讯云的配置信息
touch .env
```

```
# .env file
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```
