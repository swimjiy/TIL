## Hash

#### Hash Table

- 해쉬 테이블은 dynamic set을 구현하는 효과적인 방법 중 하나
- 평균 탐색, 삽입, 삭제 시간 O(1)
  - 최악의 경우 θ (n)
- 해쉬 함수 (hash function) h를 사용하여 키 k를 T[h(k)]에 저장



#### 충돌

- 두 개 이상의 키가 동일한 위치로 해슁되는 경우
- 즉, 서로 다른 두 키 k₁과 k₂에 대해서 h(k₁) = h(k₂)인 상황
- 대표적인 두 가지 충돌 해결 방법 : chaning과 open addressing



#### Chaning에 의한 충돌 해결

동일한 장소로 해슁될 모든 키들을 하나의 연결리스트로 저장

- 키의 삽입
  - 키 k를 리스트 T[h(k)]의 맨 앞에 삽입: 시간복잡도 O(1)
  - 중복된 키가 들어올 수 있고 중복 저장이 허용되지 않는다면 삽입 시 리스트를 검색해야 함. 따라서 시간복잡도는 리스트의 길이에 비례
- 키의 검색
  - 리스트 T[h(k)]에서 순차검색
  - 시간복잡도는 키가 저장된 리스트의 길이에 비례
- 키의 삭제
  - 리스트 T[h(k)]로부터 키를 검색 후 삭제
  - 일단 키를 검색해서 찾을 후에는 O(1)시간에 삭제 가능

- 최악의 경우는 모든 키가 하나의 슬롯으로 해슁되는 경우
  - 길이가 n인 하나의 연결리스트가 만들어짐
  - 따라서 최악의 경우 탐색시간은 θ(n) + 해쉬함수 계산시간
- 평균시간복잡도는 키들이 여러 슬롯에 얼마나 잘 분배되느냐에 의해서 결정.



#### SUHA (Simple Uniform Hashing Assumption)

각각의 키가 모든 슬롯에 균등한 확률로 독립적을 해쉰된다는 가정

만약 n=O(m)이면 평균검색시간은 O(1)



#### Open Addressing에 의한 충돌 해결

- 모든 키를 해쉬 테이블 자체에 저장
- 테이블의 각 칸(slot)에는 1개의 키만 저장
- 충돌 해결 기법
  - Linear probing
  - Quadratic probing
  - Double hashing
- 단점 : 단순히 키를 삭제할 경우 문제가 발생.



##### Linear Probing

- h(k), h(k) +1, h(k)+2...순서로 검사하여 처음으로 빈 슬롯에 저장

- 테이블의 끝에 도달하면 다시 처음으로 circular하게 돌아감.

- 단점 : 연속된 슬롯들인 cluster가 생성되면 점점 더 커지는 경향이 생김.

- 해결방안 1 : Quadratic probing

  - 충돌 발생 시 h(k), h(k)+1², h(k)+2², h(k)+3², ... 순서로 시도

- 해결방안 2 : Double hashing

  - Quadratic probing과 유사

  - 서로 다른 두 해쉬 함수 h₁와 h₂를 이용하여

    h(k, i) = (h₁(k) + i·h₂(k)) mod m



#### 좋은 해쉬 함수란?

- 어떤 해쉬 함수를 사용하는지가 해쉬의 성능을 결정. 
- 현실에서는 키들이 랜덤하지 않음.
- 만약 키들의 통계적 분포에 대해 알고 있다면 이를 이용해서 해쉬 함수를 고안하는 ㅓㅅ이 가능하겠지만 현실적으로 어려움
- 키들이 어떤 특정한 패턴을 가지더라도 해쉬함수값이 불규칙적이 되도록 하는게 바람직
  - 해쉬함수값이 키의 특정 부분에 의해서만 결정되지 않아야



#### 해쉬 함수 구현 기법

- Division 기법
  - h(k) = k mod m
- Multiplication
  - 0에서 1 사이의 상수 A를 선택: 0<A<1
  - kA의 소수부분만을 택한다.
  - 소수 부분에 m을 곱한 후 소수점 아래를 버린다.
  - 아무리 유사한 키들이라도 예측하기 어려운 해쉬 함수값을 얻을 수 있다.



