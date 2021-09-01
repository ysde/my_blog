---
title: "將靜態網站內容上傳至Github"
date: 2021-09-01T16:31:08+08:00
draft: true
---
> 根據上一篇 [利用Hugo產生靜態網站]({{< ref "/posts/20210901_using_hugo_generate_blog.md" >}})完成靜態blog網站製作後，要開始來上傳到`Github`了!

1. 登入`Github`，在上面創建一個repository，比如說`my_blog`
2. 創建後跟著指示，將網站的資料夾加入到git內並push至`Github`
3. 點選 `Settings` -> `Pages`，會看到如下的圖，目前`Github Pages`是disabled

	按下`None`會可以選擇Branch，要你選一個Branch當作`Github Pages`的來源，會發現只有剛剛按照指示的 `main` Branch可以選

	![alt](/my_blog/posts/images/2021090102.png)
	
> 接下來有兩種做法可以選
>> 1. 在本機用`hugo`指令，先將剛剛的靜態網站轉換成真正的html格式，然後上傳至`Github`
>> 2. 利用`Github Action`，當我們在本機編輯靜態網站文章後，push到`Github`上，讓`Github Action`自動將我們編輯的內容轉成真正的html格式
>
> 這裡比較偏好 方法 2，省去了在本機轉換成html的麻煩
>
> 方法 1 可以參考這一篇的做法 [在 Github Pages 建立 Hugo 靜態網站](https://kaichu.io/2015/07/12/my-first-post/)

1.  在剛剛的repository頁面，會看到 `Actions` 的頁籤，點進去後會看到如下的畫面，按下`set up a workflow yourself`連結

	![alt](/my_blog/posts/images/2021090103.png)

	貼上這一段code幫你將`main`的內容，自動轉換成html後放到`gh-pages`這個branch	

		name: github-pages
		
		on:
		  push:
		    branches: [ main ]
		
		  workflow_dispatch:
		
		jobs:
		  build:
		    runs-on: ubuntu-latest
		
		    steps:
		      - uses: actions/checkout@v2
		        with:
		          submodules: true
		      
		      - name: Setup Hugo
		        uses: peaceiris/actions-hugo@v2
		        with:
		          hugo-version: 'latest'
		          extended: true
		
		      - name: Build
		        run: hugo --gc --minify --cleanDestinationDir --buildDrafts
		
		      - name: Deploy
		        uses: peaceiris/actions-gh-pages@v3
		        with:
		          github_token: ${{ secrets.GITHUB_TOKEN }}
		          publish_branch: gh-pages
		          force_orphan: true

2. 然後可以隨便修改一下檔案，比如說文章加個空白，重新push至`main`，`Github Action` 會自動幫你建立 `gh-pages` 這個 branch

3. 重新回到 `Settings` -> `Pages` ，按 `None` 下拉式選單，選擇 `gh-pages` ，按下 `Save`，將Github告訴你的網址，更新回 `config.toml` 檔案的 `baseUrl` 欄位。再push一次至 `main`。

> 然後就大功告成啦，`Github`給你的網址應該會是像這樣 `https://你的帳號.github.io/repository名稱/`，用這網址就可以看到你的網站囉
