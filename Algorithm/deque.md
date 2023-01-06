# deque

- double ended queue 의 줄임말이다
- 장점
    - vector와 달리 양 끝에서 삽입/삭제가 가능
    - vector는 메모리가 찼을 떄 메모리 재 할당 후 이전 원소를 복사하여 성능이 저하 되지만 deque는 메모리 블럭을 하나 새로 할당한다. 여러 메모리에 쪼개져서 보관하고 위치를 기억한다.
- 원소를 앞쪽으로 추가/삭제 하려면 deque.push_front(원소), deque.pop_front(원소)를 사용한다.

# vector 
### 부족했던 부분

- iterator : 컨테이너 원소에 접근할 수 있는 포인터와 같은 객체
- tolower() : 한 글자씩 바꿔주기 때문에 string을 바꾸려면 반복문 돌리기.
- find() : (v.begin(),v.end(),찾을 것) / 없으면 벡터의 끝 반환됨. v.end()
- erase() : (iterator)