# vue-oss
ali-oss和vue结合的demo项目，使用了OSS JavaScript SDK。（对该SDK的不清楚的同学请参考：https://cnodejs.org/topic/56ab1c0526d02fc6626bb383 )

### 使用方法：
1. git clone本项目

2. npm install 安装好依赖包

3. 修改 src/components/Oss.vue 中的 bucket以及STS令牌（STS令牌的生成，参加ali-oss文档：https://help.aliyun.com/document_detail/31935.html?spm=5176.doc32069.2.4.AxKPsA）

4. npm run dev，即可运行本项目

### 遇到的几个坑
这个问题看起来简单，但是却困扰了我好几天，遇到了好多坑。
1. 一开始是尝试使用 import 'aliyun-oss'，但是这个npm包依赖 fs 等 node.js 核心包，导致无法运行。

2. 后来尝试直接使用<script src="http://gosspublic.alicdn.com/aliyun-oss-sdk-4.1.4.min.js"></script>，在代码中直接 new OSS这种方式来运行。但是atom会提示出错“OSS is not defined”。最后试了下 new window.OSS这种方式来初始化客户端，就不会报错了。

3. 虽然可以正常运行，但是request在提交阿里云服务器的时候，在header的authorization和Content-MD5的结尾会莫名其妙的多了5个AAAAA字符串，导致sign校验通不过。找了很久，发现是js版本不对，最后引用了：<script type="text/javascript" src="http://gosspublic.alicdn.com/aliyun-oss-sdk.min.js"></script> 就没问题了。
