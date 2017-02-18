### JSON

#### JSON.stringify 함수
```{.javascript}
JavaScript 값을 JSON(Javascript Object Notation) 문자열로 반환

Syntax
JSON.stringify(
value [, replacer] [, space])

매개변수
value
	필수 사항 일반적으로 변환할 개체 또는 배열
replacer
    선택 사항입니다.  결과를 변환하는 함수 또는 배열입니다.
    replacer가 함수이면 JSON.stringify는 키와 각 멤버의 값을 전달하여 함수를 호출.
    반환 값은 원래 값 대신 사용됩니다. 
    함수가 undefined를 반환하면 멤버가 제외됩니다. 
    루트 개체의 키는 빈 문자열인 ""입니다.  
    replacer가 배열이면 배열에 키 값이 있는 멤버만 변환됩니다.  
    멤버가 변환되는 순서는 배열의 키 순서와 같습니다.  
    replacer 배열은 value 인수도 배열인 경우 무시됩니다.  
space
    선택 사항입니다.  읽기 쉽도록 들여쓰기, 공백, 줄 바꿈 문자를 반환 값 JSON 텍스트에 추가합니다.  
    space가 생략되면 반환 값 텍스트가 추가 공백 없이 생성됩니다.
    space가 숫자이면 반환 값 텍스트가 각 수준의 지정된 공백 수로 들여쓰기됩니다.
    space가 10보다 크면 텍스트가 10칸 들여쓰기됩니다.  
    space가 '\t'와 같이 빈 문자열이 아니면 반환 값 텍스트가 각 수준에서 문자열의 문자로
    들여쓰기됩니다.
    space가 10자보다 긴 문자열이면 처음 10자가 사용됩니다.
```