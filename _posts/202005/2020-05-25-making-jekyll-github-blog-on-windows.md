---
layout: post
title: Window에서 jekyll github blog 만들기
subtitle: Window에서 jekyll github blog 만들기
description: Window에서 jekyll theme를 이용한 github blog 만들기. jekyll theme jekflix-template 참조.
image: https://res.cloudinary.com/douayt92p/image/upload/c_scale,h_399,q_auto,w_760/v1590619942/samples/landscapes/landscape-panorama.jpg
category: css
tags:
  - jekyll
  - github
  - ruby
  - gulp
author: jw2471358
---

1. [git](https://git-scm.com/downloads) 설치  
2. [ruby](https://rubyinstaller.org/downloads/) 설치  
Start Command Prompt with Ruby  
<code>$ ruby --version</code>
3. jekyll 설치  
Start Command Prompt with Ruby 실행  
<code>$ gem install jekyll bundle</code>  
<code>$ jekyll -version</code>

4. gulp 설치  
<code>$ npm install gulp-cli -g</code>
5. jekyll theme template forking & jekyll 서버 실행  
git clone https://github.com/your-github-username/jekflix-template.git  
또는  
https://github.com/thiagorossener/jekflix-template  
에서 Use this template 클릭

### jekflix-template guide
1. Fork the Jekflix Template
2. Clone the repo you just forked:  
<code>$ git clone https://github.com/<your-github-username>/jekflix-template.git</code>
3. Access the local project:  
<code>$ cd path/to/jekyll-template</code>
4. Install npm packages:  
<code>$ npm install</code>
5. Install Ruby dependencies:  
<code>$ bundle install</code>
6. Build Jekyll:  
<code>$ bundle exec jekyll build</code>  
<code>$ bundle exec jekyll serve</code>  
<code>C:\blog\jekflix-template>bundle exec jekyll serve</code>
7. Then run Gulp:  
<code>$ gulp</code>

- Running local  
After the steps above, to run Jekyll locally, you'll just need to run Gulp:

- $ gulp  
<em>Customization</em>  
Jekflix Template allows you to personalize your site with several settings. See the docs for more details.

For advanced theme customization, check the directory _sass for style files.


### Node.js command prompt

>gulp  
bundle exec jekyll build  
bundle exec jekyll serve  
gulp 또는 build 에 오류 발생하더라고 serve하면 문제없이 된다.

```cmd
C:\blog\jekflix-template>gulp
[02:11:25] Using gulpfile C:\blog\jekflix-template\gulpfile.js
[02:11:25] Starting 'default'...
[02:11:25] Starting 'images'...
[02:11:25] Starting 'mainJs'...
[02:11:25] Starting 'previewJs'...
[02:11:25] Starting 'yamlTheme'...
[02:11:26] Finished 'yamlTheme' after 1.79 s
[02:11:26] Starting 'jsonTheme'...
[02:11:27] Finished 'previewJs' after 1.95 s
[02:11:27] Finished 'jsonTheme' after 163 ms
[02:11:27] Starting 'cleanTheme'...
[02:11:27] Finished 'cleanTheme' after 132 ms
[02:11:27] Finished 'mainJs' after 2.41 s
[02:11:27] gulp-imagemin: Minified 22 images (saved 74.8 kB - 18.6%)
[02:11:27] Finished 'images' after 2.58 s
[02:11:27] Starting 'config'...
[02:11:27] Finished 'config' after 80 ms
[02:11:27] Starting 'jekyll'...
[02:11:27] 'jekyll' errored after 6.27 ms
[02:11:27] Error: spawn bundle.bat ENOENT
    at Process.ChildProcess._handle.onexit (internal/child_process.js:267:19)
    at onErrorNT (internal/child_process.js:469:16)
    at processTicksAndRejections (internal/process/task_queues.js:84:21)
[02:11:27] 'default' errored after 2.68 s
```
```cmd
C:\blog\jekflix-template>bundle exec jekyll serve
Configuration file: C:/blog/jekflix-template/_config.yml
            Source: C:/blog/jekflix-template
       Destination: C:/blog/jekflix-template/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
   PaginateContent: 1 item could not be split (no separators?)
                    done in 2.834 seconds.
  Please add the following to your Gemfile to avoid polling for changes:
    gem 'wdm', '>= 0.1.0' if Gem.win_platform?
 Auto-regeneration: enabled for 'C:/blog/jekflix-template'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```

>서버 재구동이 필요한 필요한 경우 : _config.xml 변경시 ex) pagination, two column 등  
_post : md 파일명에 한글 넣으면 안됨 -.-;


### github 연동 클라우드
[Cloudinary](https://cloudinary.com/)

### The Disqus Blog 
[disqus](https://disqus.com/)

#### References
<https://jekyllrb-ko.github.io/docs/posts/>
