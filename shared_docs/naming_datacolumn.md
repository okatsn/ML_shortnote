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


