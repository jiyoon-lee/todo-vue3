# Todos

vue3 기본 문법을 공부하고 간단한 투두리스트를 만들어봤다.

### 주요 기능

1. todo 추가
2. todo 삭제
3. todo 수정
4. todo 활성화/비활성화 변경
5. 모든 todos 조회
6. 활성화된 todos만 조회
7. 완료된 todos만 조회
8. 전체 지우기

### 궁금한 점

```
const todos = reactive([]);

// todo 삭제
todos = todos.filter(element => element.id !== id);
```

위와 같이 하면 안된다.

```
cost todos = reactive({
    list: []
})
todos.list = todos.filter(element => element.id !== id);
```

위와 같이 작성해야한다.
그럼 매번 의미없이 한 단계를 더 감싸야하는데 더 좋은 방법이 없을까.
