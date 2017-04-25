### jQuery 6. attr(), prop()

#### 속성의 차이?
> .attr() 은 HTML의 속성을 취급
> .prop() 는 Javascript의 프로퍼티를 취급

```{.javascript}
1. <a id="to_comments" href="#comments">코멘트 일람</a>
var $link = $('#to_comments')

.attr() → #to_comment
.prop() → http://example.com/path/to/page#to_comment

2. <checkbox id="private" type="checkbox" checked />

var $checkbox = $('#private');
alert($checkbox.attr('checked'));  // checked속성의 값을 표시
alert($checkbox.prop('checked'));  // checked프로파티값을 표시

.attr() → "checked"
.prop() → true

```
