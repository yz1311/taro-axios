# taro-axios <a href="https://www.npmjs.com/package/taro-axios"><img src="https://badge.fury.io/js/taro-axios.svg" alt="NPM Version"></a> <a href="https://travis-ci.org/fjc0k/taro-axios"><img src="https://travis-ci.org/fjc0k/taro-axios.svg?branch=master" alt="Build Status"></a> <a href="https://codecov.io/gh/fjc0k/taro-axios"><img src="https://codecov.io/gh/fjc0k/taro-axios/branch/master/graph/badge.svg" alt="Coverage Status"></a> <img src="https://badgen.net/badgesize/normal/https://unpkg.com/taro-axios/lib/index.min.js" alt="Size"> <img src="https://badgen.net/badgesize/gzip/https://unpkg.com/taro-axios/lib/index.min.js" alt="Gzip Size"> <img src="https://badgen.net/github/license/fjc0k/taro-axios" alt="License">

在 [Taro](https://github.com/NervJS/taro) 中使用 [axios](https://github.com/axios/axios)。

## 特性

- 使用 TypeScript 编写，类型友好
- 支持 API 一致的多端上传文件

## 安装

```bash
# yarn
yarn add taro-axios

# 或, npm
npm i taro-axios --save
```

## 使用

使用方法同 [axios](https://github.com/axios/axios#axios)。

只不过你得这样引入 `axios`：

```ts
import { axios } from 'taro-axios'

axios
  .get('https://jsonplaceholder.typicode.com/todos/1')
  .then(res => {
    console.log(res.data)
  })
```

## 上传文件

为了支持多端上传文件，我们得引入 `PostData` 和 `FileData` 两个类，示例：

```ts
import { axios, PostData, FileData } from 'taro-axios'

function async uploadImage() {
  const { tempFilePaths } = await Taro.chooseImage({ count: 1 })
  Taro.showLoading({ title: '图片上传中...' })
  const res = await axios.post(
    'https://sm.ms/api/upload',
    new PostData({
      smfile: new FileData(tempFilePaths[0]),
      ssl: true,
      format: 'json',
    }),
  )
  Taro.hideLoading()
  Taro.showModal({
    title: '返回结果',
    content: JSON.stringify(res.data),
  })
}
```

## 许可

MIT ©️ Jay Fong
