Spring I/O 2015報告
=====

2015/6/XX JSUG定例

### agenda

* 自己紹介
* 概要
* Key Note 「Springの歴史」
* Spring 4.2
* Boot
* Web
* Batch
* Others
* 総評

### 自己紹介

* BASIC→VB→VC++→Java
* フレームワークに興味を持ち、なぜかSIerに入社@2010
* 初めてのSpringへの印象はXML地獄。
    * Annotation-drivenを知らなかった。
    * Java Based Configurationはまだ無かった。
* Spring Core/MVC/Batch/Data

### 概要

* 2015/4/29-30@バルセロナ
* 基調講演＋39セッション＋6ワークショップ
* 41プレゼンター（日本からは槙さん）
* Spring/Groovy/Grails
    * G2Xな皆様ごめんなさい

### バルセロナ

* 偉大なるアーキテクト、ガウディーの街
    * ガウディーは女性恐怖症で生涯独身!?
* 何といってもサグラダファミリアは必見
* **来年のI/Oもバルセロナで開催するらしい**

![サグラダファミリア](https://github.com/ikeyat/slides/blob/master/201506XX_SpringIO2015Summary/img/familia1.JPG)
![サグラダファミリア](https://github.com/ikeyat/slides/blob/master/201506XX_SpringIO2015Summary/img/familia2.JPG)

### 会場

* AXA Auditorium
* 中心街から少し外れた場所なので、食事や観光に若干不便。

![会場](https://github.com/ikeyat/slides/blob/master/201506XX_SpringIO2015Summary/img/theater.jpg)
![会場](https://github.com/ikeyat/slides/blob/master/201506XX_SpringIO2015Summary/img/theater2.jpg)

### 戦利品

![ノベルティ](https://github.com/ikeyat/slides/blob/master/201506XX_SpringIO2015Summary/img/novelty.jpg)

Key Note 「Springの歴史」
---

### Key Note

Spring 4.2
---

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
