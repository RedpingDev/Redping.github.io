---
title: "NodePath 로 삽질했던 이야기와 해결법 공유!"
subtitle: 처음 작성해보기
author: "Redping"
date: 2024-11-02 18:00:00 +0900
categories: [Indie Game, DevLog-ko]
tags: [indiegame, devlog, pixelart]
lang: ko
---

## 삽질의 시작 - NodePath 가져왔는데... 이게 왜?

처음에는 **NodePath**로 노드를 가져와서 간단히 다루려고 했어요. 근데 이게 웬일? export로 노드를 지정해도 이상하게 작동하는 겁니다. **NodePath**를 가져왔는데, 내가 의도한 노드가 아니라 다른 쪽을 참조해서 엉뚱한 결과가 나오더군요.


문제를 확인해보니, NodePath가 상대 경로로 노드를 찾아가는 방식 때문이었어요. “음… 그러면 이걸 절대 경로로 바꿔야 하나?” 생각이 들어 다른 방법을 찾아봤습니다.

![NodePath game Image](/img/nodepath_post.png)

## 해결법 찾기 - Node + get_path()로 절대 경로 활용하기


해결책은 생각보다 간단했어요. **Node**의 **get_path**() 메서드를 사용해서 절대 경로를 가져오는 방식으로 수정해봤습니다. **NodePath** 대신 절대 경로를 사용하면 참조 문제를 피할 수 있더라고요.


```gdscript
var my_node_path = $Node.get_path()
# NodePath 대신 절대 경로 가져오기
var target_node = get_node(my_node_path)
```


이렇게 수정한 뒤에는 예상대로 노드를 잘 불러올 수 있었습니다. 문제없이 실행되는 걸 보니 마음이 좀 놓였어요.


## 요약하자면...


**NodePath**는 상대 경로로 동작하기 때문에 생각지 못한 참조 문제가 생길 수 있어요.


**Node**의 **get_path()**를 활용해 절대 경로를 쓰면 더 정확하게 노드를 참조할 수 있습니다.


작은 경로 참조 문제지만, **NodePath**와 경로 방식의 차이를 이해하는 것이 중요하다는 걸 다시 한번 깨달았어요.


이번 삽질을 통해 경로 참조가 작은 디테일 같지만 큰 차이를 만든다는 걸 알았습니다. 앞으로는 NodePath 관련 작업할 때 더 신중히 접근해야겠어요!


### 마무리:


이 글이 NodePath 때문에 고민하는 다른 개발자분들께 작은 도움이 되길 바라며, 또 삽질하지 않도록 같이 화이팅입니다! 😊

혹시 이 글이 도움이 되었다면, 작은 커피 한 잔으로 응원해 주시면 큰 힘이 될 거예요. 덕분에 더 많은 개발 팁과 삽질 이야기로 찾아올 수 있습니다!
☕ [[Github 후원 링크](https://github.com/sponsors/RedpingDev)]


또 다른 이야기나 개발 여정을 보고 싶다면, 아래 제 링크 트리에서 다양한 소셜 채널도 확인해 주세요. 재미있게 봐 주시면 감사하겠습니다! 
🌲[[my Link tree](https://linktr.ee/RedpingGames)]


저와 이 프로젝트의 배경 이야기가 궁금하시다면, 🕵️ [About Me 포스트](/posts/ko/about)에서 자세한 내용을 확인하세요. 여러분의 관심과 응원은 이 게임을 함께 완성해 나가는 데 큰 힘이 됩니다.

끝까지 읽어주셔서 감사합니다. 앞으로도 같이 배우고 성장해요! 🙌
