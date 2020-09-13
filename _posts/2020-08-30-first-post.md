---
layout: post
title:  "[Git] 블로그 첫 포스트"
date:   2020-08-30 11:59:13 +0800
categories: Git
tags: git
---
개발을 하면서 기록해야겠다고 느끼게 되면서<br>
깃블로그를 시작하게 되었다<br>


##### 깃 블로그 만들기

[깃블로그1](https://honbabzone.com/jekyll/start-gitHubBlog/)<br>
[깃블로그2](https://zoomkoding.github.io/gitblog/2019/08/15/git-blog-1.html)<br>

깃 블로그는 위의 두 블로그를 보며 만들었다.<br>
마음에 드는 템플릿을 다운 받아 커스터마이즈만 하면 되기 때문에 비교적 쉽다.<br>
앞으로 개발을 하면서 기록을 남기려고 한다. <br>

###### Git 에러 CRLF will be replaced by LF (혹은 반대) 핸들링
[에러핸들링](https://blog.jaeyoon.io/2018/01/git-crlf.html)<br>

유닉스 시스템에서는 한 줄의 끝이 LF(Line Feed)로 이루어지는 반면, 윈도우에서는 줄 하나가 CR(Carriage Return)와 LF(Line Feed), 즉 CRLF로 이루어지기 때문이다. 따라서 어느 한 쪽을 선택할지 Git에게 혼란이 와 에러가 발생한다.<br>
```
git config -—global core.autocrlf true (input)
git add .
git commit -m "text"
git push
```

###### MarkDown언어 사용법
[마크다운](https://gist.github.com/ihoneymon/652be052a0727ad59601)<br>

