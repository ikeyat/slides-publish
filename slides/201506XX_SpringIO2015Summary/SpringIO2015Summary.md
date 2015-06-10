Spring I/O 2015報告会
=====

2015/6/22 JSUG

### agenda

|内容        |時間|発表者      |
|:-----------|:---|:-----------|
|概要        |5min|池谷        |
|Key Note 「Springの歴史」|10min|本橋  |
|Spring 4.2  |45min|岩塚、池谷  |
|セッションサマリ|30min|岩塚、池谷|

### 自己紹介

* 池谷 智行（いけや ともゆき）
* BASIC→VB→VC++→Java
* フレームワークに興味を持ち、なぜかSIerに入社@2010
* 初めてのSpringへの印象はXML地獄。
    * Annotation-drivenを知らなかった。
    * Java Based Configurationはまだ無かった。
* Spring Core/MVC/Boot/Batch/Dataに関心あり

### 概要

* 2015/4/29-30@バルセロナ
* 基調講演＋39セッション＋6ワークショップ
* 41プレゼンター（日本からは槙さん）
* Spring/Groovy/Grails
    * G2Xな皆様ごめんなさい
* 聴講者含めアジア系は我々4名のみの模様

### バルセロナ

* 偉大なるアーキテクト、ガウディの街
    * ガウディは女性恐怖症で生涯独身!?
* **来年のI/Oもバルセロナで開催するらしい**

![サグラダファミリア](./img/familia1.JPG)
![サグラダファミリア](./img/familia2.JPG)

### 会場

* AXA Auditorium
* 中心街から少し外れた場所なので、食事や観光に若干不便。

![会場](./img/theater.jpg)
![会場](./img/theater2.jpg)

### 戦利品

![ノベルティ](./img/novelty.jpg)

Key Note 「Springの歴史」
---

### Key Note

Spring 4.2
---

### Spring 4.2

* 2015/5末に4.2.0.RC1が公開
* 2015/7/15にリリース予定
* Spring IO Platform 2.0.0に載る予定
    * Spring 4.2.0
    * Spring Security 4.0.1
    * Spring Boot 1.3.0

### Spring 4.1の新機能（おさらい）

|カテゴリ    |新機能      |
|:-----------|:-----------|
|Web|静的リソース制御の改善|
|   |Controller引数のOptionalサポート|
|   |Controllerの返値の```ListenableFuture```サポート|
|   |Jacksonの```@JsonView```サポート|
|   |JSONPサポート|
|   |```ResponseBodyAdvice```追加|
|   |新しい```HttpMessageConverter```追加|
|   |EL関数```s:mvcUrl```追加|
|   |```ResponseEntity```ビルダーサポート|
|   |```GroovyMarkupTemplate```サポート|

### Spring 4.1の新機能（おさらい）

|カテゴリ    |新機能      |
|:-----------|:-----------|
|JMS|```@JmsListener```サポート|
|   |```spring-messaging```サポート|
|Cache|JCache(JSR-107)サポート|
|WebSocket|SockJSのクライアントサイドサポート|
|   |STOMPのSubscribeイベントサポート|
|   |websocketスコープの追加|
|Test|GroovyスクリプトによるTestContext設定サポート|
|   |```@Sql```/```@SqlConfig```のサポート|
|   |```@TestPropertySource```のサポート|

詳細は、
http://www.slideshare.net/makingx/springone-2gx-2014-spring-41-jsug

### Spring 4.2の新機能（カテゴリ）

|4.1新機能    |4.2新機能      |
|:------------|:--------------|
|Web<br>JMS<br>WebSocket<br>Test<br>Cache|Web<br>JMS<br>WebSocket<br>Test<br>**Container**<br>**Data Access**|

### Spring 4.2の新機能

|カテゴリ    |新機能      |詳細|
|:-----------|:-----------|:-------|
|Container   |```@Bean```のJava8 defaultメソッド対応|○|
|            |```@Import```の改善|○|
|            |```@Order```のConfigurationクラス対応|○|
|            |```@Resource```の```@Lazy```対応|-|
|            |```@EventListener```による任意メソッドでのイベント検知|○|
|            |```@AliasFor```によるアノテーション属性のエイリアス対応|○|
|            |```DefaultConversionService```の改善|-|
|            |```DefaultFormattingConversionService```のJSR-354 Money & Currency対応|-|
|            |```@NumberFormat```のmeta-annotation対応|-|
|            |```JavaMailSenderImpl```への```testConnection()```メソッド追加|-|
|            |```ScheduledTaskRegistrar```の改善|-|
|            |Apache ```commons-pool2```のサポート|-|
|Data Access |AspectJによる```javax.transaction.Transactional```の対応 |-|
|            |```SimpleJdbcCallOperations```の名前バインディング対応|?|
|            |Hibernate ORM 5.0のフルサポート|?|
|            |```<jdbc:embedded-database>```への```database-name```属性追加|?|
|JMS         |省略|-|
|Web         |||
|WebSocket   |||
|Test        |||

http://docs.spring.io/spring/docs/4.2.0.RC1/spring-framework-reference/htmlsingle/

Boot
---

### [Spring Boot is made for tooling](http://www.springio.net/spring-boot-is-made-for-tooling/)(Yann Cébron/Stéphane Nicoll)

 - IntelliJ 14のSpring Boot連携機能を実演しながら紹介
     - オートコンプリート（propertiesも）
     - JSON生成支援
 - ついていけなかったがあっという間にアプリが作られていった。
 - STSを使っている講演者は全体通して少なかった。STSの今後が気になる。

Web
---

### [Modern Java Component Design with Spring 4.2](http://www.springio.net/wp-content/uploads/2014/11/spring-4.2-component-design-juergen-hoeller.pdf) (Juergen Hoeller)

 - Spring 4.2（ほぼMVC？）をコード例付きで一個ずつ紹介
 
 

### [Spring 4 Web Apps](http://www.springio.net/wp-content/uploads/2014/11/springio2015-spring-4-web-apps-rossen-stoyanchev.pdf) (Rossen Stoyanchev)

- Spring MVC 4系の新たな機能を淡々と紹介
    - @RestController
    - @ControllerAdvice
    - Static Resources
        - ブラウザキャッシュのため、静的リソースにバージョンハッシュを付けてくれる 
        - Example: “/css/font-awesome.min **-7fbe76cdac**.css”

### [Spring 4 Web Apps](http://www.springio.net/wp-content/uploads/2014/11/springio2015-spring-4-web-apps-rossen-stoyanchev.pdf) (Rossen Stoyanchev)

- Spring MVC 4系の新たな機能を淡々と紹介
    - WebSocketでは、アプリレベルのSTOMPを使うのが良い
    - WebSocketのブロードキャスト実装例

    ```java
    @Controller
    public class PortfolioController {
     @RequestMapping("/greetings", method=POST)
     public String send() {
     this.messagingTemplate.convertAndSend(
     “/topic/greetings”, payload);
     }
    }
    ```

### [Spring 4 Web Apps](http://www.springio.net/wp-content/uploads/2014/11/springio2015-spring-4-web-apps-rossen-stoyanchev.pdf) (Rossen Stoyanchev)

- Spring MVC 4.2の新機能
    - HTTP Streaming
        - 連続したオブジェクトを返却するインタフェース。ResponseBodyEmitterが戻り値。
        - ResponseBodyEmitterを拡張してServer sent event対応している。
    - HTTP Caching Updates (Cache-Control/E-Tag)
    - CORS Support (@CrossOrigin)
    - @RequestMapping as Meta Annotation
    - JavaScript View Templating
        - サーバ側でjavascriptで画面をレンダリング
        - 一部をサーバ、一部をクライアント見たいな異も可能
        - JDK1.8のNashornを利用
    - STOMP Client

Batch
---

### [Spring Batch for Large Enterprises Operations](http://www.springio.net/spring-batch-for-large-enterprises-operations/) (Ignasi Gonzalez)

- 簡単なSpring Batchの紹介とエンタープライズ開発事例紹介
- 公式サイトのPDFリンクは正しくない・・・
- 事例１：銀行系
    - プロフィール
        - 7,000 tps
        - 30,000 users
        - 30 developers
    - ホストとの統合のため、商用ツールと連携する必要があった。
    - 商用ツールに合わせスケジューラやランチャーをカスタマイズした。
    
### [Spring Batch for Large Enterprises Operations](http://www.springio.net/spring-batch-for-large-enterprises-operations/) (Ignasi Gonzalez)

- 事例２：電力系
    - プロフィール
        - 300 developers
    - ポイント
        - 現行のスクラッチ実装のバッチをどのようにSpring Batchに移行するか。
        - 300人の開発でいかに品質を確保するか。
    - ポイントに対しPoCを実施した。
        - CheckstyleやSonar等を用いコードの品質確保を確認した。
        - reportingとschedulingが弱いので拡張が必要だった。
        - 例えば、既存データの件数から実効時間を予測したり、プログレスをレポートするようにした。

Others
---

### Code Highlight

```java
public class Hoge {
  public static void main(String[] args) {
    System.out.println("Hello World!");
  }
}
```

### Reference

http://www.springio.net
