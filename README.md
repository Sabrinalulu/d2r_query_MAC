# d2rq_query
Display my procedure of installation and solutions of difficulties I encountered (Mac OS)  

根據官方文件指南: http://d2rq.org/getting-started
需要:
Java 1.5 or newer on the path (check with java -version if you're not sure),
A supported database,such as Oracle, SQL Server, PostgreSQL, MySQL or HSQLDB.

d2rq的檔案：
因為下載的d2rq是資料夾檔(非dmg，單純zip，tar解壓後還是純資料夾)，mac上容易碰上command not found沒有設定讓terminal能直接辨認的問題。
我根據網址(https://github.com/d2rq/d2rq)：
先安裝了Apache ant(用了homebrew套件管理安裝)之後要用git指令直接裝d2rq，
結果遇上了字樣-- "Permission denied (publickey)" error when pushing with Git
最終在此連結(https://gist.github.com/adamjohnson/5682757)找到解決方法：需要設定SSH，即能執行git clone git@github.com:d2rq/d2rq.git下載到檔案。d2rq會被安裝在.ssh資料夾中，用terminal移動到當前資料夾(d2rq)，執行ant jar，把執行d2rq還需要的檔案再添加上去。

官方指南有說需要JDBC，不過MySQL本來就有自帶，不需額外下載。我在安裝好MySQL後嘗試在terminal到.ssh/d2rq中執行放進去的ttl檔案(我用知乎上SimmerChan提供的檔案：https://zhuanlan.zhihu.com/p/32880610)，因為connection failed依然無法成功。(有可能關鍵字沒下對，所以google的答案都不直接ＱＡＱ)
最後決定用XAMPP直接架Apache和MySQL。

database:
到XAMPP官網： https://www.apachefriends.org/download.html 下載dmg檔案安裝，
可以看這個網站的指引：http://itcathk.blogspot.com/2016/04/mac-xampp.html
因為mac有自己開著的Apache，必須先把它關掉才能夠開啟XAMPP的伺服器，防止通道因為已佔用無法讓XAMPP使用。
在terminal執行：(參考：https://stackoverflow.com/questions/37888222/unable-to-start-xampp-apache-server-on-macos-sierra/37892935)
```shell
sudo apachectl stop
sudo /Applications/XAMPP/xamppfiles/bin/apachectl start
```
開啟XAMPP的control panel看是否Apache web server已被開啟，再把MySQL Database也打開，就可以在瀏覽器網址欄輸入http://localhost/phpMyAdmin
成功看到phpMyAdmin的介面，匯入知乎的movie sql檔案。最後到Terminal的.ssh/d2rq資料夾中執行./d2r-server kg_demo_movie_mapping.ttl可以成功開啟介面。
