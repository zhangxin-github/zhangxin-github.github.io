# 开始

## 安装 hexo
$ npm install hexo-cli -g
$ hexo init <blog>

## 一键本地启动
$ hexo clean && hexo g && hexo s

## 一键部署
$ hexo clean && hexo g && hexo d

## 应用主题
$ git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
$ npm install hexo-renderer-pug hexo-renderer-stylus --save

修改 Hexo 根目录下的 _config.yml，把主题改为 butterfly

## 参考网站
https://butterfly.js.org/posts/4aa8abbe/
https://nbchen.com/posts/hexo-butterfly.html
https://github.com/wugenqiang/NoteBook/blob/master/Project/Hexo-Butterfly/Hexo-Butterfly%E5%8D%9A%E5%AE%A2%E6%90%AD%E5%BB%BA%E6%8C%87%E5%8D%97.md
https://github.com/1976083684/hexo-blog/blob/master/source/_posts/Hexo%E6%90%AD%E5%BB%BAButterfly%E4%B8%BB%E9%A2%98%E5%B9%B6%E5%BF%AB%E9%80%9F%E7%BE%8E%E5%8C%96.md

# 写作

## 创建子目录文章
$ hexo new post -p "数据存储/数据库/MySQL.md"

## 新建草稿（一些不想立即发布的文章）
$ hexo new draft "draft-name" 

## 预览草稿
$ hexo s --drafts
