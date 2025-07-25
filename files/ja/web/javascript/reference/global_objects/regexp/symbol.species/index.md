---
title: RegExp[Symbol.species]
slug: Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.species
l10n:
  sourceCommit: 8421c0cd94fa5aa237c833ac6d24885edbc7d721
---

{{JSRef}}

**`RegExp[Symbol.species]`** は静的なアクセサープロパティで、特定の `RegExp` メソッドのコピーされた正規表現を構築するのに使用されたコンストラクターを返します。

> [!WARNING]
> `[Symbol.species]` が存在すると、任意のコードの実行が可能になり、セキュリティ上の脆弱性が生じる可能性があります。また、ある種の最適化も非常に難しくなります。エンジンの実装者たちは、[この機能を削除するかどうか調査しています](https://github.com/tc39/proposal-rm-builtin-subclassing)。可能であれば、この機能に頼ることは避けてください。

{{InteractiveExample("JavaScript デモ: RegExp[Symbol.species]")}}

```js interactive-example
class MyRegExp extends RegExp {
  // Overwrite MyRegExp species to the parent RegExp constructor
  static get [Symbol.species]() {
    return RegExp;
  }
}

const regex1 = new MyRegExp("foo", "g");

console.log(regex1.test("football"));
// Expected output: true
```

## 構文

```js-nolint
RegExp[Symbol.species]
```

### 返値

`get [Symbol.species]` が呼び出されたコンストラクター (`this`) の値。この返値は、コピーした `RegExp` インスタンスを作成するために使用されます。

## 解説

`[Symbol.species]` アクセサープロパティは、 `RegExp` の既定のコンストラクターを返します。サブクラスのコンストラクターは、オーバーライドすることでコンストラクターの割り当てを変更することができます。既定の実装は基本的に次の通りです。

```js
// 説明のための架空の基礎実装
class RegExp {
  static get [Symbol.species]() {
    return this;
  }
}
```

この多相的な実装により、派生したサブクラスの `Symbol.species` も既定でコンストラクター自身を返すようになります。

```js
class SubRegExp extends SubRegExp {}
SubRegExp[Symbol.species] === SubRegExp; // true
```

一部の `RegExp` メソッドは、{{jsxref("RegExp/exec", "exec()")}} を実行する前に現在の正規表現インスタンスのコピーを作成します。そのため、{{jsxref("RegExp/lastIndex", "lastIndex")}} への変更が保持されないような副作用があります。`Symbol.species` プロパティは、新しいインスタンスのコンストラクターを決定するために使用されます。正規表現インスタンスをコピーするメソッドは以下の通りです。

- [`[Symbol.matchAll]()`](/ja/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.matchAll)
- [`[Symbol.split]()`](/ja/docs/Web/JavaScript/Reference/Global_Objects/RegExp/Symbol.split)

## 例

### 通常オブジェクトの species

`Symbol.species` プロパティは、既定のコンストラクターを返します。 `RegExp` オブジェクトであれば、 `RegExp` コンストラクターを返します。

```js
RegExp[Symbol.species]; // function RegExp()
```

### 派生オブジェクトの species

派生クラスのコレクションオブジェクト（たとえば、独自の正規表現を表す `MyRegExp`）では、 `MyRegExp` の species は `MyRegExp` コンストラクターです。しかし、派生クラスのメソッドで親である `RegExp` オブジェクトを返すようにこれをオーバーライドしたくなるかもしれません。

```js
class MyRegExp extends RegExp {
  // MyRegExp の species を親である RegExp コンストラクターにオーバーライドします。
  static get [Symbol.species]() {
    return RegExp;
  }
}
```

または、これを使用してコピープロセスを監視することができます。

```js
class MyRegExp extends RegExp {
  constructor(...args) {
    console.log("Creating a new MyRegExp instance with args:", args);
    super(...args);
  }
  static get [Symbol.species]() {
    console.log("Copying MyRegExp");
    return this;
  }
  exec(value) {
    console.log("Executing with lastIndex:", this.lastIndex);
    return super.exec(value);
  }
}

Array.from("aabbccdd".matchAll(new MyRegExp("[ac]", "g")));
// Creating a new MyRegExp instance with args: [ '[ac]', 'g' ]
// Copying MyRegExp
// Creating a new MyRegExp instance with args: [ MyRegExp /[ac]/g, 'g' ]
// Executing with lastIndex: 0
// Executing with lastIndex: 1
// Executing with lastIndex: 2
// Executing with lastIndex: 5
// Executing with lastIndex: 6
```

## 仕様書

{{Specifications}}

## ブラウザーの互換性

{{Compat}}

## 関連情報

- {{jsxref("RegExp")}}
- {{jsxref("Symbol.species")}}
