Spring I/O 2016報告会
=====

* Spring 4.3の新機能
* Spring Data、Spring Integrationの紹介

2016/6/22 JSUG

### 自己紹介

* 池谷 智行（いけや ともゆき）
* BASIC→VB→VC++→Java
* フレームワークに興味を持ち、なぜかSIerに入社@2010
* 初めてのSpringへの印象はXML地獄。
    * Annotation-drivenを知らなかった。
    * Java Based Configurationはまだ無かった。
* Spring Core/MVC/Boot/Batch/Dataに関心あり

### agenda

* **Spring 4.3の新機能**
* Spring Dataの新機能
* Spring Integrationを使ってみよう

### Spring 4.3の新機能

* おなじみとなったJurgen氏による「Modern Java...」

![Spring4.3](./img/spring4.3.jpg)

### Spring 4.3の新機能

![making](./img/making.jpg)

* [すでにJJUG CCC 2016 Springにて紹介されています！](http://www.slideshare.net/makingx/jjugccc-cccgh5-whats-new-in-spring-framework-43-boot-14-pivotals-cloud-native-approach)
* より詳細は
    * [公式リファレンス](http://docs.spring.io/spring/docs/4.3.0.RELEASE/spring-framework-reference/htmlsingle/)
    * [@kazuki43zoo氏による日本語解説](http://qiita.com/kazuki43zoo/items/8cee2692dcf3d70ad538)

### 紹介するSpring 4.3の新機能

|分類    |新機能      |
|:-----------|:-----------|
|Container   |コンストラクタの``@Autowired``省略に対応|
|Web         |各種合成アノテーションの提供|
|            |暗黙的なHEADとOPTIONのレスポンス作成|
|            |``@SessionAttribute``や``@RequestAttribute``の追加|
|Boot/Test   |別セッションで|

###

### Spring 4.3 個人的な感想

* Spring 4.2に比べると大きな機能追加はない
* よく使う合成アノテーションを提供することで

### Spring Dataの新機能

### Spring Integrationを使ってみよう

