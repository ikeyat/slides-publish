SpringCore5の新機能
=====
 
Spring5 5.0.0.RC1  
2017/5/24


### きっかけ1/2

[SpringI/O 2017@Barcelona](http://2017.springio.net/)に参加したが、  
Spring5リリース間近にもかかわらず  
Spring5のコアな新機能について紹介した講演が全然無く幻滅。  

講演は相変わらずリアクティブ関連ばかり。

### きっかけ2/2

その旨伝えたら、「wiki見てくれ」と言われたので見てみた。

https://github.com/spring-projects/spring-framework/wiki/What%27s-New-in-the-Spring-Framework#whats-new-in-spring-framework-5x

2017/5/24時点ではググった限り、  
日本語訳してる人見当たらなかったので、  
ここぞとばかりに日本語で簡単に紹介してみる。

### Disclaimer

* 短時間で見たので間違ってるかもです。
* リアクティブ関連(webflux)とKotlin対応を除いたSpring Coreに限定
    * Spring4ユーザ目線
* インパクトの大きい変更に絞って紹介


JDK 8+ and Java EE 7+ Baseline
---

### 1. JDK 8+ and Java EE 7+ Baseline
- JDK8ベースに内部コードをリファクタ
    - 当然、実行にはJDK8以上が必須となった
- JDK9の[モジュールシステム](https://www.infoq.com/jp/news/2017/05/jigsaw-public-review)にランタイムレベルで対応
- Java EE 7 APIが必須
    - Servlet 3.1, JMS 2.0, JPA 2.1, Bean Validation 1.1
    - 最新のアプリケーションサーバがベースライン
        - e.g. Tomcat 8.5+, Jetty 9.4+, WildFly 10+
- Java EE 8 APIにランタイムレベルで互換
    - Servlet 4.0, Bean Validation 2.0, JSON Binding API


Core Container
---

### candidate component index
- 本機能追加の背景
    - Spring Bootや大規模Springアプリの起動時間が遅い理由
        - 大量無差別のComponent-Scanが原因の一つ
- 概要
    - 「コンパイル時」にASMにより``@Component``なBeanをスキャン
        - 実際は``@Component``のメタアノテーション``@Indexed``
    - スキャン結果を``META-INF/spring.components``に保存。
    - 実行時にインデクスファイル(前述)が存在すればクラスパススキャンの代替として使用。
    - jarが大きく``@Component``なBeanの比率が少ない際に効果的
        - 従来のスキャンと異なりjarのサイズに比例しないため。

### candidate component index
- 利用方法
    - pom.xmlに以下を追加

```xml
<dependencies>
        <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-context-indexer</artifactId>
                <version>5.0.0.RC1</version>
                <optional>true</optional>
        </dependency>
</dependencies>
```

### candidate component index
- 注意事項
    - コンパイル時にアプリ全体をインデクス化に対応できない場合がある。
        - その場合はフォールバックのための設定が必要。
            - ``spring.index.ignore=true``
        - どういうときに対応できないのかは記載がなく謎。
- 参考
    - [本家リファレンス](https://docs.spring.io/spring/docs/5.0.0.RC1/spring-framework-reference/core.html#beans-scanning-index)
    - [本家JIRA](https://jira.spring.io/browse/SPR-11890)


### インジェクション対象に``@Nullable``を指定可能
- 本機能追加の背景
    - インジェクション対象の存在が必須でない場合
        - Spring流なら``@Autowired(required = false) Hoge hoge``
        - JSR-330流だと``@Inject Optional<Hoge> hoge``
- 概要
    - JDK8の``@Nullable``を使い、JSR-330流でも表現を簡単に！
        - ``@Inject @Nullable Hoge hoge``
    - JSR-330流とSpring流の差が縮まることは良いこと。
- 参考
    - 本家リファレンスRC1版では記述が見つからず・・・
    - [本家JIRA](https://jira.spring.io/browse/SPR-15028)

### Lamda式によるBean登録とカスタム
 - 本機能追加の背景
     - Bean登録をJavaコードで制御したい場合がある。
         - 繰り返してBeanを生成、登録したい
         - Beanのプロパティを動的に指定したい、等
     - 従来のSpring4でも可能だったが使い辛い。
         - ``GenericApplicationContext#registerBeanDefinition(String, BeanDefinition)``

### Lamda式によるBean登録とカスタム
 - 概要
     - Bean生成をJavaコード1行で登録可能に。
     - Lambda式でBeanをカスタムでき、他Beanとの関係が設定可能。
         - 適切なタイミングでLambda式が実行されるため、
    
```java
context.registerBean(Hoge.class,
    () -> new Hoge(context.getBean("fuga")),
    hoge -> hoge.setPiyo(context.getBean("piyo")));
```

- 参考
    - [本家javadoc](http://docs.spring.io/spring/docs/5.0.0.RC1/javadoc-api/org/springframework/context/support/GenericApplicationContext.html#registerBean-java.lang.Class-java.util.function.Supplier-org.springframework.beans.factory.config.BeanDefinitionCustomizer...-)

### その他
-Consistent detection of transaction, caching, async annotations on interface methods.
    - In case of CGLIB proxies.
- XML configuration namespaces streamlined towards unversioned schemas.
    - Always resolved against latest xsd files; no support for deprecated features.
    - Version-specific declarations still supported but validated against latest schema.

Spring WebMVC
---

Testing Improvements
---

Removed Packages, Classes and Methods
---

General Core Revision
---

番外編
---

- Referenceの見た目が変わった
    - Single Page HTMLやPDF版が無くなった!?
    - What's newがwikiに移動されている
        - Spring4では一番上にいたのでバージョン重ねてくと邪魔だった
    - 構成自体はさほど変わっていない模様
    - WebFluxの分量が全体比で見ると少なくて意外・・・
    - [before](https://docs.spring.io/spring/docs/4.3.x/spring-framework-reference/htmlsingle/)-[after](https://docs.spring.io/spring/docs/5.0.0.RC1/spring-framework-reference/)
