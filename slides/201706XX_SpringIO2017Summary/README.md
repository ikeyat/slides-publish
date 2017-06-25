Spring I/O 2017報告会
=====

* Functional Web Framework
* Spring DataのReactive対応

2017/6/29 JSUG勉強会

### 自己紹介

* 池谷 智行（いけや ともゆき）
* 某大手SIerに入社@2010
* JSUGの幹事を手伝ってます。
* [「Spring徹底入門(翔泳社)」](http://www.shoeisha.co.jp/book/detail/9784798142470)の執筆に参加しました。
* Spring I/Oは3回目の参加 

### お詫び

槙さん講演＠Java Day Tokyo 2017  
[「Spring Framework 5.0によるReactive Web Application」](http://www.oracle.com/technetwork/jp/ondemand/online2017-javaday-3719599-ja.html)

の激しい劣化版に結果的になってしまったこと  
ご了承ください。

### agenda

* **Reactiveのおさらい**
* Functional Web Framework
* Spring DataのReactive対応

## Reactive(Streams)とは

* non-blockingな処理をイベントドリブンに記述する方法
* back pressureによりpush型/pull型の両立を図る

```
Publisher ---[onNext()]--> Subscriber
          <--[request()]--
```

リアクティブプログラミングの詳細は、
[NTTの岩塚さん、堅田さんのスライド](https://www.slideshare.net/TakuyaIwatsuka/spring-5)

### MonoとFlux (Reactor)

* Reactorにおける``Publisher``の実装
* ``Mono``は0/1個、``Flux``は0個以上の値を発行可能

``TODO: sample code``

### Spring5でのReactive

* spring-flux

```java
@RestController
public class EchoController {
  @PostMapping("/echo")
  Flux<String> upperCase
      (@RequestBody Flux<String> body) {
    return body.map(String::toUpperCase);
  }
}
```

### agenda

* Reactiveのおさらい
* **Functional Web Framework**
* Spring DataのReactive対応

### Overview

### RouterFunction

### HandlerFunction

### HandlerFilterFunction

### agenda

* Reactiveのおさらい
* Functional Web Framework
* **Spring DataのReactive対応**

### Overview

``TODO: versionなど``

### APIの破壊的変更

``TODO: メソッド名とRepository拡張のアレ``

### Spring Dataが扱うデータソース

* **JPA(JDBC)**
* Redis
* MongoDB
* etc...

### JDBC

### Redis

### MongoDB

### ReactiveCrudRepository

```java
<S extends T> Mono<S> save(S entity);
<S extends T> Flux<S> saveAll(Publisher<S> entityStream);
Mono<T> findById(ID id);
Flux<T> findAll();
Mono<Long> count();
...
```

