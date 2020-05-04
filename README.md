# spin-wheel
抽獎旋轉盤，參考: https://mirari.cc/2019/06/25/CSS3实现转盘抽奖/

**使用 Vue CLI 建立的專案，但主要是裡面的 src/components/SpinWheel.vue**

## props 
| 屬性名           | 型態    | 說明            | 範例                                          |
|-----------------  |-------- |---------------- |---------------------------------------------- |
| prizeList         | Array   | 獎項列表        | [{icon: "", name: ""}]                        |
| time              | Number  | 旋轉動畫的時間   | 5 (5秒)                                        |
| wheelBackground   | String  | 轉盤背景        | #7eef97 or url(.png) no-repeat center center  |