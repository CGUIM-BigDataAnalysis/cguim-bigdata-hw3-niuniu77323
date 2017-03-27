長庚大學 大數據分析方法 作業三
================

網站資料爬取
------------

``` r
#這是R Code Chunk
 ##第一次使用要先安裝 install.packages("rvest")
##install.packages("rvest")
library(rvest)
```

    ## Warning: package 'rvest' was built under R version 3.3.3

    ## Loading required package: xml2

    ## Warning: package 'xml2' was built under R version 3.3.3

``` r
HTML <-read_html("https://www.ptt.cc/bbs/Tech_Job/index.html")
btnURL<-HTML %>% html_nodes("a[class='btn wide']") %>% html_attr("href")
indexNum <- as.numeric(gsub("/bbs/Tech_Job/index|.html"," ",btnURL[2]))
 
totalPTT<-NULL
  
 
for (i in (indexNum-4):(indexNum+1)){
    #print(i)
    HTML=paste("https://www.ptt.cc/bbs/Tech_Job/index",i,".html",sep="")
    Title <- read_html(HTML) %>%html_nodes(".title") %>% html_text()
   
    PushNum<-read_html(HTML) %>%html_nodes(".nrec") %>% html_text()
    
    Author<-read_html(HTML) %>%html_nodes(".author") %>% html_text()
   
   
   
    

    PTT<-data.frame(Title,PushNum,Author)
   #dataframeAll<-rbind(dataframe1,dataframe2) 
    totalPTT<-rbind(totalPTT,PTT)
 
 
   
   }
       View(totalPTT)
```

爬蟲結果呈現
------------

``` r
#這是R Code Chunk
knitr::kable(totalPTT)
```

| Title                                                       | PushNum | Author       |
|:------------------------------------------------------------|:--------|:-------------|
| \[請益\] 哪條路，若想轉職比較方便？                         | 10      | a40232145    |
| \[請益\] 戀人最近在忙什麼？                                 | 15      | leatica      |
| \[請益\] 想詢問面試狀況                                     | 1       | howdai123    |
| \[新聞\] 鐵血CEO蔡力行扮「殺手」？聯發科員工剉              | 48      | tw689        |
| \[請益\] 業務工程師 北區推薦                                | 7       | praive       |
| \[新聞\] 首年享13天特休！德州儀器徵100人　研究所畢起薪5-6萬 | 10      | wer11        |
| \[新聞\] 國防55級分 畢業「免當軍人」上班月領51K             | 4       | s6307        |
| \[新聞\] 科技RD「每天7點下班」超貼心　台女竟怒              | X1      | AK47shoot    |
| Re: \[新聞\] 科技RD「每天7點下班」超貼心　台女              | 2       | join183club  |
| \[心得\] 群聯不舒服的面試經驗                               | 49      | wears        |
| \[討論\] 面試有補助交通費的有那些公司?                      | 43      | magic704226  |
| \[新聞\] 聯發科Q1營業淨利恐季減70%                          | 38      | unrest       |
| \[請益\] offer選擇 力晶/景碩                                | 4       | blacksky124  |
| Re: \[公司\] 大船集團-達航科技                              |         | pinkowa      |
| \[請益\] 系統廠HW 能轉甚麼職缺?                             | 9       | sustaned     |
| \[聘書\] offer請益 華碩/彩富/矽創                           | 8       | wuhalala     |
| \[請益\] 正文是屬於ic design的公司嗎？                      |         | ghost1006    |
| \[請益\] 請問日本還有能打的半導體廠嗎                       | 9       | lin214       |
| \[請益\] 覆晶封裝製程轉職問題                               | 15      | KFCNTU       |
| \[新聞\] 華爾街日報：印度即將開始生產iPhone                 | 3       | Lanaroh      |
| \[徵才\] ucfunnel-媒體開發/PM/Node.js/Frontend              | 1       | livingroom   |
| \[請益\] 第一份工作薪水重要還是練功重要?                    | 爆      | s6307        |
| Re: \[請益\] 覆晶封裝製程轉職問題                           | 6       | gnh1021      |
| \[請益\] 研發替代役                                         | 6       | leo710215    |
| \[請益\]offer選擇                                           | 10      | david597     |
| \[心得\] 面試 大立光電/艾克爾/采鈺/百佳泰/美光              | 11      | goodboy8899  |
| \[請益\] 電機女生找工作                                     | 74      | alice2520200 |
| \[心得\] 我在拓凱(台中工業區)的日子                         | 71      | dash0804     |
| Re: \[心得\] 群聯不舒服的面試經驗                           | 10      | magic704226  |
| (本文已被刪除) \[catdogter\]                                | 31      | -            |
| (已被mmkntust刪除) <stan1111> 版規六                        |         | -            |
| \[請益\] 內湖緯創ＥＢＧ情況                                 | 11      | wort         |
| \[請益\] 在台灣工作未來方向                                 | 15      | omega0210    |
| \[請益\] 陶氏化學CDP面試詢問                                | 7       | chengyuche   |
| \[請益\] 做Power ICdesign的前景？                           | 29      | golover      |
| \[討論\] 關於機台零件是不是都撐到最後？                     | 21      | s4001        |
| \[討論\] 關於伺服器代工                                     | 15      | orz3qonz     |
| \[請益\] 請問有人了解三浦鍋爐嗎                             | 2       | skatopia     |
| \[新聞\]【台GG別走動畫】台積傳將赴美砸5千億建3              | 44      | DickMartin   |
| \[新聞\] 靠文青打敗台積電　新鮮人最嚮往企業出爐             | 58      | popoallan    |
| (已被mmkntust刪除) <sht255>                                 | 10      | -            |
| 〔疑惑〕台GG要在竹南設廠的傳聞有下文嗎？                    | 38      | q99518g      |
| \[聘書\] Offer請益 達創/新日興                              | 12      | lovetire     |
| \[請益\] Offer請益 英業達/鴻海                              | 34      | kusahara     |
| \[請益\] 聯電職務請益                                       | 11      | blacktea0930 |
| \[請益\] offer請益 garmin自動化機構/國外sales               | 8       | Blueicex     |
| \[面試\] 友達晶材IE面試與錄取                               | 12      | nick800418   |
| (本文已被刪除) \[pptgov\]                                   |         | -            |
| \[請益\] offer 選擇(美光vs力晶）                            | 42      | chsweet      |
| Fw: \[請益\] 科技工程師練英文                               | 5       | ggggggh      |
| \[請益\] offer 上無註明保障年月薪                           | 26      | ck49         |
| \[心得\] 面試心得(乾坤/正新/台灣荏原/Lam/)                  | 8       | Sorry5566    |
| \[徵才\] 汐止-徵求會PHP與SQL的工程師                        | 8       | MobileMan    |
| \[請益\] 頎邦科技                                           | 1       | popularman   |
| \[面試\] 台達化學公司(前鎮廠) 工作環境與福利                | 5       | tcl2830      |
| \[請益\] 點晶科技 推嗎                                      | 5       | okmijnuhb    |
| (本文已被刪除) \[tcl2830\]                                  |         | -            |
| \[心得\] 面試心得(基恩斯/精材/ASML/艾克爾)                  | 28      | Sorry5566    |
| \[請益\] offer選擇(虹晶 vs 小豬屎屋)                        | 6       | Kovainen     |
| (本文已被刪除) \[nntn\]                                     | 3       | -            |
| 敬鵬-資訊系統開發管理師                                     | 1       | incoterms    |
| \[請益\] 美亞科技                                           | 6       | key9028      |
| \[新聞\] 總經理巡廠要整理桌面　群創員工爆比當兵             | 35      | zzzz8931     |
| Re: \[討論\] 關於機台零件是不是都撐到最後？                 | 1       | c1823akimo   |
| 創群科技                                                    | 13      | jamiefly     |
| \[討論\] 有人因為辦公室太舊太髒離職的嗎??                   | 43      | yamakazi     |
| (本文已被刪除) \[VamYU\]                                    | 12      | -            |
| Re: \[心得\] 我在拓凱(台中工業區)的日子                     | 6       | simplep2002  |
| Re: \[新聞\]【台GG別走動畫】台積傳將赴美砸5千億建3          | 2       | egnaro123    |
| \[聘書\] 緯創/建漢/帆宣                                     | 3       | tomandjim    |
| (本文已被刪除) \[piggg\]                                    |         | -            |
| \[徵才\] 交大電子所誠徵碩士級研究助理                       | 1       | xgin         |
| \[情報\] 國網中心擴大舉辦工讀生/實習生徵才活動              |         | ZhaoYun      |
| \[請益\] 亞太國際電機 製程 疑問                             | 1       | ian00727     |
| \[徵才\] 掃描器/光學元件/韌體工程師 BioInspira, Inc         |         | Herc         |
| \[請益\] 漢民MFGP CNC 新竹                                  | 1       | Crosswise    |
| Re: \[心得\]小寶跟大寶 真的不一樣                           | 22      | ikeru        |
| Re: \[請益\] Offer請益 英業達/鴻海                          | 1       | wer11        |
| (本文已被刪除) \[pjc202\]                                   |         | -            |
| Re: \[請益\] 陶氏化學CDP面試詢問                            | 4       | piggg        |
| 捷普 綠點刀具                                               | 3       | tn372845     |
| \[請益\] 日商安立知                                         | 3       | pjc202       |
| \[情報\] 蘋果申請具備iPhone核心之Macbook產品                | 6       | zxcvxx       |
| \[請益\]有人收到德州儀器技術行銷工程師面試邀請?             | 2       | wer11        |
| \[請益\] 請問陸資的IC設計公司                               | 8       | DigiTalent   |
| \[請益\] 德州儀器設備工程師實習                             | 2       | oeys         |
| \[討論\] 國家光電好嗎                                       |         | chag06       |
| Re: \[請益\] 請問陸資的IC設計公司                           | 16      | DigiTalent   |
| \[請益\] 是否該調往偏鄉工作？                               | 44      | NakiXIII     |
| (本文已被刪除) \[lponnn\]                                   | 5       | -            |
| \[請益\] 關於科技業或是保險                                 | 2       | dfg512       |
| \[請益\] Advantest二手設備商                                | 4       | CA42         |
| Fw: \[請益\] 夜間進修                                       |         | neon2102     |
| \[請益\] 華通電腦                                           | 6       | jackjack0805 |
| \[討論\] 矽品好像沒有板上說的那麼不好吧~                    | 57      | goodlike     |
| \[討論\] 試用期超過三個月                                   | 12      | ScrewYou     |
| \[討論\] 台積電VS中油                                       | 9       | ej4g4        |
| (本文已被刪除) \[p4818046\]                                 | 1       | -            |
| \[請益\] 金屬工業中心面試                                   |         | huaygina     |
| \[請益\] 在職碩班選擇請益，中興vs中央                       | 4       | AKFG         |
| Re: \[討論\] 台積電VS中油                                   | 4       | tomtowin     |
| \[請益\] 台積vs世界                                         | 39      | q7w8s5       |
| \[請益\] 暑期實習請益                                       | 4       | quasi        |
| Fw: \[台北\] 推手媒體誠徵後端工程師                         |         | ssmartdan841 |
| (本文已被刪除) \[sheu123\]                                  | 1       | -            |
| \[請益\] Offer請益(仁寶/緯創)                               | 6       | johnnypk321  |
| \[新聞\] 台積i8單 下月量產                                  | 11      | unrest       |
| \[討論\] 聯穎光電面試                                       |         | key9028      |
| \[請益\] 大中積體電路                                       |         | pieceofacake |
| \[請益\] 弘馳公司 面試前的準備                              |         | AlioAlio     |
| \[討論\] 離職最後一根稻草                                   | 11      | NTUlosers    |
| \[請益\]力成panel fan-out 製程整合 & 群創製程               | 1       | vacfann      |
| Re: \[討論\] 試用期超過三個月                               |         | dakkk        |
| \[討論\] （樹林）瑞傳 smt                                   |         | usa71111     |
| 律師為您解惑－線上勞動法免費諮詢即日為勞工 …                | 爆      | pzs          |
| \[公告\] Tech\_Job板板規 2014.03.01                         | 7       | mmkntust     |
| \[公告\] 置底 檢舉/推薦 文章                                | 爆      | mmkntust     |
| \[免費\]工作人生顧問                                        | 爆      | zodiac       |

解釋爬蟲結果
------------

``` r
dim(totalPTT)
```

    ## [1] 118   3

↑總共爬出108筆文章標題

``` r
max(
    table(totalPTT$Author)

)
```

    ## [1] 12

``` r
 table(totalPTT$Author)
```

    ## 
    ##    a40232145    AK47shoot  blacksky124    ghost1006    howdai123 
    ##            1            1            1            1            1 
    ##  join183club       KFCNTU      Lanaroh      leatica       lin214 
    ##            1            1            1            1            1 
    ##  magic704226      pinkowa       praive        s6307     sustaned 
    ##            2            1            1            2            1 
    ##        tw689       unrest        wears        wer11     wuhalala 
    ##            1            2            1            3            1 
    ##            - alice2520200   chengyuche     dash0804     david597 
    ##           12            1            1            1            1 
    ##   DickMartin      gnh1021      golover  goodboy8899    leo710215 
    ##            1            1            1            1            1 
    ##   livingroom    omega0210     orz3qonz    popoallan        s4001 
    ##            1            1            1            1            1 
    ##     skatopia         wort blacktea0930     Blueicex      chsweet 
    ##            1            1            1            1            1 
    ##         ck49      ggggggh     Kovainen     kusahara     lovetire 
    ##            1            1            1            1            1 
    ##    MobileMan   nick800418    okmijnuhb   popularman      q99518g 
    ##            1            1            1            1            1 
    ##    Sorry5566      tcl2830   c1823akimo    Crosswise    egnaro123 
    ##            2            1            1            1            1 
    ##         Herc     ian00727        ikeru    incoterms     jamiefly 
    ##            1            1            1            1            1 
    ##      key9028        piggg  simplep2002    tomandjim         xgin 
    ##            2            1            1            1            1 
    ##     yamakazi      ZhaoYun     zzzz8931         AKFG         CA42 
    ##            1            1            1            1            1 
    ##       chag06       dfg512   DigiTalent        ej4g4     goodlike 
    ##            1            1            2            1            1 
    ##     huaygina jackjack0805     NakiXIII     neon2102         oeys 
    ##            1            1            1            1            1 
    ##       pjc202     ScrewYou     tn372845       zxcvxx     AlioAlio 
    ##            1            1            1            1            1 
    ##        dakkk  johnnypk321     mmkntust    NTUlosers pieceofacake 
    ##            1            1            2            1            1 
    ##          pzs       q7w8s5        quasi ssmartdan841     tomtowin 
    ##            1            1            1            1            1 
    ##     usa71111      vacfann       zodiac 
    ##            1            1            1

↑最多篇文章顯示九篇，作者顯示為"-"， 回版上看發現作者為"-"是已被刪除的文章..... 而第二多的是3篇，作者為"wer11"

↑人工結論 最有趣的地方是同意作者最多文章數竟然是被刪除的文章，另外工作版感覺不錯看呢!發現不可以面試放鳥公司，不然會被萬年黑名單
