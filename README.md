# EGG-APOLLO-CLIENT
[![NPM version][npm-image]][npm-url]

[npm-image]: https://img.shields.io/npm/v/@gaoding/egg-apollo-client.svg?style=flat-square
[npm-url]: https://npmjs.org/package/@gaoding/egg-apollo-client

    ******************************************************************
    ******************************************************************
    **********              代码千万行，注释第一行              **********
    **********              编码不规范，同事泪两行              **********
    ******************************************************************
    ******************************************************************

携程 Apollo 配置中心 egg 客户端版本

## Installation
```bash
npm i @gaoding/egg-apollo-client [--save]
```

## Usage
add plugin
```js
// config/plugin.js or config/plugin.ts
exports.apollo = {
    enable: true,
    package: '@gaoding/egg-apollo-client'
}
```

add apollo plugin config
```js
// config/config.[env].js
config.apollo = {
    config_server_url: 'http[s]://xxxxxxx', // required, 配置中心服务地址
    app_id: 'xxx',                          // required, 需要加载的配置
    cluster_name: 'xxx',                    // optional, 加载配置的集群名称, default: 'default'
    namespace_name: 'xxx',                  // optional, 加载配置的命名空间, default: 'application'
    release_key: 'xxx',                     // optional, 加载配置的版本 key, default: ''
    ip: 'xxx'                               // optional,

    set_env_file: false,                    // optional, 是否写入到 env 文件, default: false
    env_file_path: 'xxxx',                  // optional, 写入的 env 文件路径, default: ${app.baseDir}/.env.apollo
    watch: false,                           // optional, 长轮询查看配置是否更新, default: false
}
```

在 config 目录下添加新文件 config.apollo.js
```js
// config.apollo.js
module.exports = (apollo, appConfig) => {
    return {
        logger: {
            ...appConfig.logger,
            level: apollo.get('LOGGER_LEVEL')
        }
        ....
    }
}
```

## Tips
- ✅ 支持初始化的同步加载配置，解决远程加载配置是异步的问题
- ✅ config.apollo.js 是 apollo 的配置文件，会在所有配置加载之后覆盖原有配置
- ✅ 支持将配置写入到本地文件，需要开启 set_env_file
- ✅ 当读取远程配置出错时，兼容本地 env 文件读取, 需要开启 set_env_file

## Todo
- ✅ 支持配置订阅模式，暂时没想到已有项目的实用性，因为插件的加载是不可修改的，更新配置要让插件生效就要重启进程
- 🔥 支持多集群加载
