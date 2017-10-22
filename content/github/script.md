使用自动化脚本，一个命令来上一节中的所有操作。

### 自动化创建和更新 gh-pages

所以，我们采用一个 npm 包，来帮助我们完成上面的操作

```
cd my-note/
npm i gh-pages
```

然后创建 my-note/scripts/deploy-gh-pages.js

里面的内容是：

```js
'use strict';

var ghpages = require('gh-pages');

main();

function main() {
    ghpages.publish('./gh-pages', console.error.bind(console));
}
```

上面的脚本的作用，就是把当前文件夹下的 gh-pages 文件夹中的所有内容，push 到本仓库的 gh-pages 分支。

然后添加几个 npm 脚本 deploy （ deploy 就是部署的意思），还有 build （意思是编译），还有 publish（意思是发布），如下：

```json
"scripts": {
 "start": "gitbook serve ./content ./gh-pages",
 "build": "gitbook build ./content ./gh-pages",
 "deploy": "node ./scripts/deploy-gh-pages.js",
 "publish": "npm run build&&npm run deploy"
},
```

这样，以后我修改了书稿，只需运行

```
npm run publish
```

注：如果最后返回 `undefined` 字样，表示没有出现错误，部署成功。

就可以把编译后的书稿 push 到远端仓库的 gh-pages 分支了。也就是可以到 https://happypeter.github.io/my-note 这个链接，看到书了。

这样，大功告成。
视频：http://digicity-1253322599.costj.myqcloud.com/gitbook-8-script.mp4
