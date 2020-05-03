# CSS

웹 페이지의 스타일을 책임지는 CSS 영역이다. 만만히 보기 쉽지만, 결코 쉽지 않으며 잘 다루면 판타스틱한 뷰를 만들어낼 수 있는 실용적인 기술이다. 그러나 정말 쉽지 않다. 앞으로 유용한 코드는 여기에 기록해두고 꺼내보려고 한다.

<br>

- [word-break](#word-break)
- [복수의 id에 CSS 적용](#apply-style-to-multiple-ids)
- [margin과 padding 차이](#margin-and-padding)
- [이미지 흑백 전환 효과주기](#mix-blend-mode)
- [텍스트/이미지 정렬](#align)

<br>

## <a name="word-break"></a>word-break

가끔 포털 뉴스나 기사를 읽다보면, 문장을 띄우는 포인트가 애매해서 보기 어려울 때가 있다. 애매하다는 의미는 단어간격으로 문장의 줄을 나누는게 아니라 "한 글자" 단위로 자르다보니 단어중간에 줄이 띄어지는 경우가 있다.

`word-break: keep-all;` 을 적용하지 않은 문장이 출력되는 화면이다. `"대한민국"`이라는 한 단어가 완성되지 못하고 잘린 상태에서 줄이 나뉘었다. 이 경우에는 기사를 읽는 독자관점에서 좀 불편할 수 있다. 따라서 이 때엔 `"대한민국"` 을 다음 줄로 넘겨서 보여주는게 훨씬 나을 것이다.

![](http://www.mediafire.com/convkey/cbb1/eeqzb4niwbls0c3zg.jpg)

다음은 `word-break: keep-all;` 을 적용한 모습이다.

![](http://www.mediafire.com/convkey/0b2b/zwlwz6qc4uazsg2zg.jpg)

<br>

아직 CSS에 대해 아는게 거의 없을정도로 무지하지만, 지금까지 배운 CSS 코드중 `display: flex;` 만큼 매력적인 코드였다.

![](https://i.ytimg.com/vi/in9SX3enCHU/maxresdefault.jpg)

아래 출처에 링크를 통해 알게 된 사실을 추가한다.

 `word-break: keep-all;` 로만 하면, 텍스트가 박스를 벗어날 수 있다고 한다. 따라서 이를 방지하기 위해 `word-wrap: break-word;` 를 추가하면, 어떤 언어도 원하는대로 단어가 중간에 끊기지않고 줄을 띄울 수 있다.

출처 : [김유리님 WIT블로그 - word-break 속성과 word-wrap 속성 알아보기](https://wit.nts-corp.com/2017/07/25/4675)

<br>

##<a name="apply-style-to-multiple-ids"></a>복수의 id에 CSS 적용

HTML 문서의 스타일 코드를 적용할 때 class, id로 구분해서 스타일을 따로 적용하는 편인데, 이 때 서로다른 id에 같은 스타일의 적용이 필요할 때가 있다. 이 땐 그냥 `,` 로 구분해서 복수의 id에 스타일을 적용할 수 있다.

<p class="codepen" data-height="265" data-theme-id="default" data-default-tab="html,result" data-user="youngjinmo" data-slug-hash="LYEdypN" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Apply style to multiple ids.">
  <span>See the Pen <a href="https://codepen.io/youngjinmo/pen/LYEdypN">
  Apply style to multiple ids.</a> by DevAndy (<a href="https://codepen.io/youngjinmo">@youngjinmo</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

<br>

## <a name="margin-and-padding"></a>margin과 padding 차이

![](https://i.stack.imgur.com/VlwVi.png)

위 이미지에서 빨간색 부분이 현재 CSS 코드를 적용중인 객체에 해당한다.

`margin`은 이 객체의 바깥 부분을 조정하는 프로퍼티이며, `padding`은 객체 안쪽을 조정하는 프로퍼티이다.

<br>

## <a name="mix-blend-mode"></a>이미지 흑백 전환효과 주기

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="css,result" data-user="youngjinmo" data-slug-hash="qBOVmjR" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="qBOVmjR">
  <span>See the Pen <a href="https://codepen.io/youngjinmo/pen/qBOVmjR">
  qBOVmjR</a> by DevAndy (<a href="https://codepen.io/youngjinmo">@youngjinmo</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

흑백이미지에 마우스를 올리면 다시 원래 색으로 돌아오는 효과이다.

이미지 반전을 이용한 효과인것 같다. 반전을 주기위해서는 먼저 이미지의 배경색을 주어야 한다. 이미지의 배경색을 주지 않으면 효과가 발생하지 않는다. 배경색을 무엇으로 주냐에 따라서 색 반전도 다르게 발생한다.

~~~css
#ki {
  background: white;
}
~~~



배경색을 넣었다면, 이제 이미지에 반전 효과를 준다.

~~~css
#ki img {
  mix-blend-mode: luminosity;
}
~~~

이제 색이 바뀐다. 마우스 오버시 다시 원래 색이 돌아오게 하려면 `:hover` 를 넣어준다.

~~~css
#ki img:hover {
  mix-blend-mode: normal;
}
~~~

출처 : <a href="https://studiomeal.com/archives/852" target="_blank">1분코딩 - CSS로 흑백이미지 만들기</a>

<br>

## <a name="align"></a>텍스트/이미지 정렬

### 텍스트 중앙정렬

`text-align` 속성값으로 center를 줌으로써 중앙정렬할 수 있다.

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="html,result" data-user="youngjinmo" data-slug-hash="GRpOmqy" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="text-align">
  <span>See the Pen <a href="https://codepen.io/youngjinmo/pen/GRpOmqy">
  text-align</a> by DevAndy (<a href="https://codepen.io/youngjinmo">@youngjinmo</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

### 이미지 중앙정렬

이미지는 `display` 속성으로 block을 주고, 좌우 margin을 auto를 주입하면, 자동으로 화면의 가운데로 정렬된다.

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="css,result" data-user="youngjinmo" data-slug-hash="yLYPbad" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="yLYPbad">
  <span>See the Pen <a href="https://codepen.io/youngjinmo/pen/yLYPbad">
  yLYPbad</a> by DevAndy (<a href="https://codepen.io/youngjinmo">@youngjinmo</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

출처 : [w3school - CSS Layout](https://www.w3schools.com/css/css_align.asp)

<br>