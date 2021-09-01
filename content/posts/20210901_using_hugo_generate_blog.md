---
title: "利用Hugo產生靜態網站"
date: 2021-08-31T13:50:27+08:00
draft: true
---
> 步驟

1. 安裝Hugo：

	如果是mac的話可以用`brew`安裝 ([什麼是Homebrew](https://brew.sh/index_zh-tw))
 
		brew install hugo
	
2. 用hugo指令建立blog
	
		hugo new site your_blog_name
		
	會在本機建立一個 `your_blog_name`
	
	目錄結構如下：
		
		blog/
		├── archetypes
		│   └── default.md
		├── config.toml
		├── content
		├── data
		├── layouts
		├── static
		└── themes

3. 用`git submodule` 加入你喜歡的Theme到`themes`的目錄底下

	這裡示範選用`beautifulhugo`這個theme

		git submodule add https://github.com/appleboy/blog-theme.git themes/beautifulhugo

	設定`your_blog_name`資料夾底下的`config.toml`，告訴hugo使用`beautifulhugo`這個theme	
	
		echo 'theme = "beautifulhugo"' >> config.toml  

	`config.toml`內容會類似像這樣  
		
		baseURL = "https://example.site"
		languageCode = "en-us"
		title = "xxxxx"
		theme = "beautifulhugo"

4. 產生第一篇測試文章

		hugo new posts/first-post.md

5. 在本機利用`Hugo`將測試網站跑起來測試
		
		hugo server -D

	![img alt txt](/my_blog/posts/images/2021090101.png)		
6. 準備要上傳至github

	上傳前要修改 `config.toml` 裡面的 `baseURL`，將url改成Github頁面上告訴你的網址，然後請參考[下一篇]({{< ref "/posts/20210901_upload_static_site_to_github" >}} "About Us")

> 參考連結:

* [將部落格從 Wordpress 轉換到 Hugo](https://blog.wu-boy.com/2021/05/migrate-wordpress-to-hugo/?fbclid=IwAR0WfX20FPbgApwlw2p1-aSyT7OagEihL9hJf69NYWp3xF1b79UVqU_pmsA)
* [Hugo Quick Start](https://gohugo.io/getting-started/quick-start/)
* [ [Ting's筆記Day2] 在Github用Jekyll創建自己的blog ](https://ithelp.ithome.com.tw/articles/10198964)
* [在 Github Pages 建立 Hugo 靜態網站](https://kaichu.io/2015/07/12/my-first-post/)
