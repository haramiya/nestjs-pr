## Nest.js の基本アーキテクチャ　

![Nest.jsの基本構成](/memos/architecture.png)

## Module とは

- 関連する Controller や Service などをまとめ、アプリケーションとして利用できるように Nestjs に登録する役割
- Nestjs アプリケーションには必ず 1 つ以上のルートモジュールと、0 個以上の Feature モジュールが必要となる

### Module の定義

- class に `@Module()` デコレータをつける
- @Module()デコレータのプロパティを記述する

### Module デコレータのプロパティ

- providers: @Injectable デコレータがついたクラスを記述
- controllers: @Controller デコレータがついたクラスを記述
- imports: モジュール内部で必要な外部モジュールを記述
- exports: 外部のモジュールにエクスポートしたいものを記述

![Moduleサンプル](/memos/module-sample.png)

## Controller とは

- クライアントからのリクエストを受け付け、クライアントにレスポンスを返す
  → Controller がルーティングの機能を担う
- 特定のパスと Controller が紐づけられる（ex: /users と UsersController）
- HTTP メソッドとパスを指定したメソッド（ハンドラー）を実装する

  ![Controllerサンプル](/memos/controller-sample.png)

## Controller の定義

- class に `@Controller()` デコレーターをつける
- メソッド（ハンドラー）に HTTP メソッドデコレータ（ex: `@Post()`）をつける
