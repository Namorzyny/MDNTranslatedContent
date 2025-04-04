---
title: <cursor>
slug: Web/SVG/Reference/Element/cursor
original_slug: Web/SVG/Element/cursor
l10n:
  sourceCommit: 2e5fc06de139c56873a20ec4bc3bf5600ea3cbef
---

{{SVGRef}}{{Deprecated_Header}}

> [!NOTE]
> この要素の代わりに CSS の {{cssxref("cursor")}} プロパティを使用してください。

**`<cursor>`** は [SVG](/ja/docs/Web/SVG) の要素で、プラットフォームに依存しないカスタムカーソルを定義するために使用することができます。プラットフォームに依存しないカスタムカーソルを定義するために推奨される手法は、 PNG 画像を作成した上で、 PNG 画像を参照する `cursor` 要素を定義し、画像内でポインター位置（すなわち、ホットスポット）である正確な位置を特定するすることです。

PNG 形式が推奨されるのは、アルファチャンネルによって透過マスクを定義する機能に対応しているからです。別の画像形式を使用する場合、この形式は透過マスクを定義することに対応している必要があります（明示的にアルファチャンネルを提供するか、具体的なピクセル色を使用して透過率を示すかの 2 つの選択肢があります）。透過マスクが指定できる場合、マスクはカーソルの形状を定義します。そうでない場合、カーソルは不透明の長方形になります。通常、他のピクセル情報（例えば、R、G、B チャンネル）は、カーソルのマスクされていない部分の色を定義します。カーソルがほとんどの背景で見えるように、カーソルは通常 2 色以上を含むことに注意してください。

## 使用コンテキスト

{{SVGInfo}}

## 属性

- {{SVGAttr("x")}} {{Deprecated_Inline}}
- {{SVGAttr("y")}} {{Deprecated_Inline}}
- {{SVGAttr("xlink:href")}} {{deprecated_inline}}

## DOM インターフェイス

この要素は {{DOMxRef("SVGCursorElement")}} インターフェイスを実装しています。

## 仕様書

{{Specifications}}

## ブラウザーの互換性

{{Compat}}
