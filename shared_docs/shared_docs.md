[中大氣象坪資訊](https://docs.google.com/document/d/15_iQngdlKuIoBaQdeyikBd8gIJgmlIbgr2jjm_rM4YE/edit)

2022/04/25 線上會議：國網平台說明與操作示範
https://youtu.be/OAbcVe3QZJw
https://youtu.be/2aHKGIbPnM0

### 檔案命名
由於之後農試所的資料也會進來，關於資料我希望之後能依循以下原則命名：
物理量放前面、附註放後綴
除了縮寫外，不使用不必要的大寫
避免籠統 (例如 air_temperature 比 temperature好)
如果同一物理量有新增不同儀器的資料，以底線附註於後綴。例如有一個新的氣溫溫度計，可以命名為 air_temperature_bla。後綴(例如這邊的"bla")基本上不限制、用覺得好記的方式命名就好，但就是要始終一致、不能搞錯。
是單字的話不要拼錯。
具體範例：
CWB_Humidity :x: (物理量應放最前面、附註放後面；不必要的大寫)
CWB_humidity :x: (物理量應放最前面、附註放後面)
Humidity_CWB :x: (不必要的大寫)
humidity_CWB :o:
humidity :o:
Soil_water_content_blabla :x: (不必要的大寫)
soil_water_content_blabla :o:
air_temperature :o:
soil_water_content_2_10cm :o: (附註於後綴的順序不拘，就是務必始終保持一致性)
soil_water_level_10cm_2 :o: (附註於後綴的順序不拘，就是務必始終保持一致性)
Temperature :x: (不必要的大寫；溫度有土水氣溫，temperature過於籠統)
preciptation:x: (拼錯單字)
因此，根據這些規則，我想要把
1. 雨量的部分，Rain01 改成 precipitation_01mm；原本精度 0.5mm的precipitation改成 precipitation_05mm
2. 氣溫一律使用 air_temperature(在2019、2020的資料為Temperature)
3. Soil_water_content 改成 soil_water_content(其他井水位、土溫也比照辦理取消不必要的大寫)


### 測站:九份二山(C1I23)
資料解析度:5分鐘(資料缺失多)
經度:120.854
緯度:23.950
資料:土壤含水量及降水量
測站:國姓(C0I420)
資料解析度:1小時
經度:120.8550
緯度:24.0378
資料:降水量、氣溫、相對溼度、氣壓、風速及風向。
上傳檔案的資料時間解析度:1小時
資料整理方式:
1.降雨量:1點的資料為1:5+1:10...+1:55累加值。
2.其餘參數:1點的資料為1:5+1:10...+1:55後平均。


吳宗羲
  1 個月前
@鍾孟儒
 九份二山的土壤水含量深度是多少呢? (欄位名為soil_water_content_C1I230)


鍾孟儒
  1 個月前
@吳宗羲
 我上水保局網站查了，但目前沒看到放置深度相關資訊，我已經寄信詢問，可能明天看看有沒有回覆，同時我再繼續看有沒有文獻也有用這些資料，可能上面會有寫。