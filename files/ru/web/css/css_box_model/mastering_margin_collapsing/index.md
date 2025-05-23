---
title: Схлопывание внешних отступов
slug: Web/CSS/CSS_box_model/Mastering_margin_collapsing
---

{{CSSRef}}

Отступы [margin-top](/ru/docs/Web/CSS/margin-top) и [margin-bottom](/ru/docs/Web/CSS/margin-bottom) иногда объединяются в один, с размером равным наибольшему из них (или размеру одного, если они равны).
Это поведение известно как **схлопывание внешних отступов (margin collapsing).**
Обратите внимание, что отступы [плавающих](/ru/docs/Web/CSS/float) и [абсолютно позиционированных](/ru/docs/Web/CSS/position#absolute) элементов никогда не схлопываются.

Схлопывание внешних отступов происходит в трёх случаях:

- Соседние элементы (siblings)
  - : Схлопываются отступы соседних элементов (за исключением случая, когда к последнему элементу применено свойство {{cssxref("clear")}}).
- Родительский и первый/последний дочерние элементы
  - : Если отсутствуют границы (border), внутренние отступы (padding), строчное содержимое (inline/inline-block) или промежуток для отделения {{cssxref("margin-top")}} родительского элемента, от {{cssxref("margin-top")}} одного или нескольких его дочерних элементов/блоков или отсутствуют границы (border), внутренние отступы (padding), строчное содержимое (inline/inline-block), {{cssxref("height")}}, {{cssxref("min-height")}} или {{cssxref("max-height")}} для отделения отступов {{cssxref("margin-bottom")}} родительского блока от {{cssxref("margin-bottom")}} отступов одного или нескольких его дочерних элементов/блоков, то внешние отступы схлопываются. Схлопнутые отступы заканчиваются за пределами родительского элемента.
- Пустые блоки
  - : Если отсутствуют границы (border), внутренние отступы (padding), строчное содержимое (inline/inline-block), {{cssxref("height")}} или {{cssxref("min-height")}} для отделения {{cssxref("margin-top")}} верхнего отступа этого блока от его {{cssxref("margin-bottom")}} нижнего отступа, то верхние и нижние внешние отступы этого блока схлопываются.

**На заметку:**

- Более сложное схлопывание отступов (более, чем двух) происходит, когда описанные случаи сочетаются.
- Эти правила применяются даже к отступам, равным 0, поэтому отступ первого/последнего дочернего элемента заканчивается за пределами его родителя (согласно правилу выше) независимо от того, равен ли отступ родителя нулю.
- При использовании отрицательных отступов, размер схлопнутого отступа вычисляется, как сумма наибольшего положительного и наименьшего отрицательного (наибольшего по модулю) отступа.
- Если все отступы отрицательные, размер схлопнутого отступа равен наименьшему (наибольшему по модулю) отступу. Это относится как к вложенным элементам, так и к соседним.
- Внешние отступы [плавающих](/ru/docs/Web/CSS/float) и [абсолютно позиционируемых](/ru/docs/Web/CSS/position) элементов никогда не схлопываются.

## Примеры

### HTML

```html
<p>Нижний отступ этого абзаца схлопнулся …</p>
<p>
  … с верхним отступом этого абзаца, объеденив отступы между ними в один, равный
  <code>1.2rem</code>.
</p>

<div>
  Этот родительский элемент содержит два абзаца!
  <p>Этот абзац имеет отступ <code>.4rem</code> между ним и текстом выше.</p>
  <p>
    Нижний отступ этого абзаца схлопывается с отступом родителя, принимая
    значение <code>2rem</code>.
  </p>
</div>

<p>Этот абзац имеет отступ <code>2rem</code> от элемента выше.</p>
```

### CSS

```css
div {
  margin: 2rem 0;
  background: lavender;
}

p {
  margin: 0.4rem 0 1.2rem 0;
  background: yellow;
}
```

### Результат

{{EmbedLiveSample('Примеры', 'auto', 350)}}

## Смотрите также

- [CSS Reference](/ru/docs/Web/CSS/Reference)
