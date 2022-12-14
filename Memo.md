# Nest.js の基本アーキテクチャ　

![Nest.jsの基本構成](/memos/architecture.png)

# Module とは

- 関連する Controller や Service などをまとめ、アプリケーションとして利用できるように Nestjs に登録する役割
- Nestjs アプリケーションには必ず 1 つ以上のルートモジュールと、0 個以上の Feature モジュールが必要となる

## Module の定義

- class に `@Module()` デコレータをつける
- @Module()デコレータのプロパティを記述する

## Module デコレータのプロパティ

- providers: @Injectable デコレータがついたクラスを記述
- controllers: @Controller デコレータがついたクラスを記述
- imports: モジュール内部で必要な外部モジュールを記述
- exports: 外部のモジュールにエクスポートしたいものを記述

![Moduleサンプル](/memos/module-sample.png)

# Controller とは

- クライアントからのリクエストを受け付け、クライアントにレスポンスを返す
  → Controller がルーティングの機能を担う
- 特定のパスと Controller が紐づけられる（ex: /users と UsersController）
- HTTP メソッドとパスを指定したメソッド（ハンドラー）を実装する

  ![Controllerサンプル](/memos/controller-sample.png)

## Controller の定義

- class に `@Controller()` デコレーターをつける
- メソッド（ハンドラー）に HTTP メソッドデコレータ（ex: `@Post()`）をつける

# Service とは

- ビジネスロジックを定義する
- Controller から呼び出すことで、ユースケースを実現する
  →Controller にビジネスロジックを書いてもプログラムは動作する
  責務ごとに分割することで、保守性・拡張性などが上がりよい設計となる

## Dependency Injection（DI）

- 日本語にすると「依存性の注入）
- 依存性のあるオブジェクトを外部から渡す

例）UsersController → UsersService<br/>
`UsersController` は `UsersService` がないと動かない。<br/>
これは「UsersController は UsersService に依存している」状態

![DIサンプル](/memos/di.png)
上記のように Controllers の中で、インスタンス化すると運用が複雑になるため、外部でインスタンス化して外部から依存オブジェクトを渡す

## DI のメリット

- 依存元のプログラムを書き換えることなく、依存先の切り替えを行なえるようになる

## 具体的な用途

- 本番用のプログラムとテスト用のモックを切り替える
- ログの出力先をファイルから DB に切り替える　など

# Service の定義

![Serviceサンプル](/memos/service.png)
![Controller-Serviceサンプル](/memos/controller-to-service.png)
