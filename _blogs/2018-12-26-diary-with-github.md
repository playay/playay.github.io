---
title: 如何用 GitHub 写日记
connotation: true
layout: blogs-right
keywords: [陶笛日记, 陶笛, github, pages, jekyll]
publish: true
---

这篇文章，首先会解释下 GitHub 写日记是怎么一回事。    
然后是，在搭建过程中都会遇到哪些技术关键词，并且给出这些技术关键词对应的官方网站。    
以及，在成功搭建好项目、写出第一篇日记后，还有哪些工作要做。    
GitHub 写日记实际上有很多种玩法，这里介绍的只是我自己的使用方式。应该也是最主流的方式。     


### Pages 服务 

官网链接: [https://pages.github.com/](https://pages.github.com/)    

写出来的日记能够发布到网上，用的就是这个 Pages 服务：新建一个特定名称的代码仓库，把我们的日记内容放到这个仓库上，GitHub Pages 就能为我们搭建日记网站，并且解决几乎所有的运维问题，包括在全球范围都能有不错访问速度的 CDN 服务（对我们来说，这都是透明的）。       

还包括自定义域名的 https 证书。对，“https 证书”。不用再看 certbot 的文档，我们的网站直接就支持 https 了。


### 现成的网页模版

日记的内容可以是单纯的文字。也可以更进一步，用 [markdown](https://github.github.com/gfm/) 约定的文本格式来写日记。这样的话，套上新建仓库时选择的现成模版。马上就能拥有一个漂亮的网站。      

这些模版，有时也叫 [jekyll](https://jekyllrb.com/docs/) 模版。      

**到目前为止。知道了 pages、jekyll 这两个关键词的你，应该能达到用 GitHub 写日记的目的了。再往下都是进阶的内容。**

---

### 完全自己写页面

要熟练掌握 jekyll，不仅要熟悉 jekyll 项目的结构、变量。还要知道 [liquid](https://shopify.github.io/liquid/) 的语法、[yaml](https://yaml.org/) 的语法。       

配合 html、[vue.js](https://cn.vuejs.org/)、[uikit](https://getuikit.com/v2/docs/documentation_get-started.html) 这三类知识，我们就能完全自定义自己的网站。      

这里说的是这三“类”。就 vue 来说，就有很多同类的工具可以选择、替换。像 react、angular 之类的。       

### 后端服务

如果需要自己有后端服务。这样的小业务场景下，[阿里云](https://promotion.aliyun.com/ntms/yunparter/invite.html?userCode=b6wzfjp8)的函数计算 这类服务是一个不错的选择。     

还是说这“类”。亚马逊的 AWS Lambda、微软的 Azure Functions 都是同类的替代选择。      


### 收录

谷歌对网页的收录是非常快速的。Pages 服务也能正常被谷歌访问。    

对于百度，划重点！！！**Pages 搭的网站无法被百度访问，不特别处理的话，百度永远都收录不了你的网页**。    

我的处理方式是：    
1. 使用自定义域名       
2. 百度的域名解析指向自己的 nginx       
3. nginx 配置 proxy_pass 到 Pages。    

这里就需要在自己的 nginx 上用 [certbot](https://certbot.eff.org/) 配置 https 了。


by the way，已经有自定义域名，但是没有服务器搭 nginx 的小伙伴。     
可以邮件联系我: chenyan@feling.net        
主题：“nginx 共享”     
附上你的域名、是否需要帮忙配 https 证书。我会把域名解析需要的 ip 发给你。


### 关键字噪音

不是页面核心内容的文字，建议写在 script 里。再用 js 插入到网页中。举个例子：    

```html
<div id="tip" style="display:none;"></div>
<script>
    $('#tip').html(
        '<h5>提示：左侧栏目，可以折叠哦</h5>' +
        '<p>' +
        '   1. 使用快捷键：`ctrl + b` 或者 `command + b`。<br/>' +
        '   2. 光标放到左右两侧的分隔处，可以看到光标有变化，点击就行了。<br/>' +
        '   <button onclick="localStorage.tip=\'confirm\';$(\'#tip\').hide(400);">' +
        '     我知道啦</button>' +
        '</p>'
    );
    if (localStorage.tip != 'confirm') {
        $('#tip').show();
    }
</script>
```

相对的，有些链接、文字是核心内容，却只能写在 js 里。可以尝试重复写一份，放在隐藏的 div 里。



* 文章目录
{:toc}