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

* おなじみとなったJuergen氏による「Modern Java...」

![Spring4.3](./img/Spring4.3.jpg)

### Spring 4.3の新機能

![making](./img/making.png)

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

### コンストラクタの``@Autowired``省略

```java
public class MyBookService {
  private MyBookRepository repository;

  // @Autowired <- 省略可能となった
  public MyBookService(MyBookRepository repository) {
    this.repository = repository;
  }
}
```

### コンストラクタの``@Autowired``省略

* Lombokを使用してBeanのコンストラクタを生成する場合

```java
// @RequiredArgsConstructor(onConstructor = @__(@Autowired)) 
// @Autowiredをコンストラクタに付けるために必要だった呪文が不要に
public class MyBookService {
  private MyBookRepository repository;

  // コンストラクタがLombokによりコンパイル時に生成される
}
```

### 各種合成アノテーションの提供1

* ``@RequestMapping`` の合成アノテーション
    * ``@GetMapping``, ``@PostMapping``, ``@PutMapping``, ``@DeleteMapping``, ``@PatchMapping``
    * HEADとOPTIONSが無い理由は後ほど
* **アノテーションがシンプルに！**

```java
// Before
@RequestMapping(value = "/books", method = RequestMethod.GET)
public String getBooks() {...}

// After
@GetMapping("/books")
public String getBooks() {...}
```

### 各種合成アノテーションの提供2

* ``@Scope`` の合成アノテーション
    * ``@RequestScope``, ``@SessionScope``, ``@ApplicationScope``
* **アノテーションがシンプルに！(大事なのでもう一度)**

```java
// Before
@Scope(value = WebApplicationContext.SCOPE_SESSION,
        target = ScopedProxyMode.TARGET_CLASS)
public class SessionScopedService { ... }

// After
@SessionScope
public class SessionScopedService { ... }
```

### 暗黙的なHEADとOPTIONSのレスポンス作成

* HEAD: GETメソッドに対するレスポンスのボディ無しで返却
* OPTIONS: Allowヘッダに、対応するHTTPメソッドの一覧を返却
* なぜ``@HeadMapping``と``@OptionsMapping``が無い？
   * Springが暗黙的に応答するようになり開発者が使う必要が無くなったから

実装
```java
@GetMapping("/books")
public String getBooks() {...}
```

OPTOPNSメソッドのリクエストに対するレスポンス
```consolne
HTTP/1.1 200 OK
Server: Apache-Coyote/1.1
Allow: GET,HEAD
Content-Length: 0
Date: Sun, 29 May 2016 14:46:12 GMT
```

### ``@SessionAttribute``や``@RequestAttribute``の追加

* ``HttpSession``や``HttpServletRequest`` へのアクセスを宣言的に実現
* 型キャストにも対応
* ``@SessionAttributes``と間違えないように

```java
// Before
@RequestMapping(value = "/books", method = RequestMethod.GET)
public String getBooks(HttpSession session) {
   String id = (String) session.getAttribute("bookId");
   // ...
}

// After
@RequestMapping("/books")
public String getBooks(@SessionAttribute("bookId") String bookId) {
   String id = bookId;
   // ...
}
```

### Spring 4.3 個人的な感想

* Spring 4.2に比べると大きな機能追加はない（行き着くところまで行き着いた？）
* よく使う合成アノテーションを提供することでコード量をスマートに
    * Spring 4.3へUpdateした既存アプリのアノテーションは合成アノテーションに変えるべき？


### agenda

* Spring 4.3の新機能
* **Spring Dataの新機能**
* Spring Integrationを使ってみよう
 
### Spring Dataの新機能


### agenda

* Spring 4.3の新機能
* Spring Dataの新機能
* **Spring Integrationを使ってみよう**


### Spring Integrationを使ってみよう

