## 키
- 특정 튜플을 식별할 때 사용하는 속성 (혹은 속성의 집합)

    -> 각 튜플별 키는 반드시 달라야 함

- 각 릴레이션 간의 관계를 맺게 해줌

### 슈퍼키 (super key)
- 튜플을 유일하게 식별할 수 있는 하나의 속성 (혹은 속성의 집합)

    -> 필요 없는 속성 포함 가능

### 후보키 (candidate key)
- 튜플을 유일하게 식별할 수 있는 속성의 최소 집합

    -> 필요 없는 속성 제외

### 기본키 (primary key)
- 여러 후보키 중 하나를 선정해 대표로 삼는 키
- 기본 키 제약 조건
  - 튜플을 식별할 수 있는 고유한 값 필요
  - NULL 불가
  - 변동 불가
  - 최대한 적은 수의 속성
  - 키 사용에 있어 문제 발생 소지 없음

### 대리키 (surrogate key) / 인조키 (artificial key)
- 가상의 속성을 기본키로 사용

### 대체키 (alternate key)
- 기본키로 선정되지 않은 후보키

### 외래키 (foreign key)
- 다른 릴레이션의 기본키를 참조하는 속성
- 참조하고 참조되는 양쪽 릴레이션의 도메인이 서로 동일
- 기본치 값이 변경되면 외래키 또한 변경
- NULL 가능, 중복 가능
- 자기 자신의 기본 키 참조 가능


## 무결성 제약조건
### 무결성 (integrity)
- 저장된 데이터의 일관성과 정확성을 지키는 것

### 도메인 무결성 제약조건 (domain integrity constraint)
- 릴레이션의 튜플들이 각 속성의 도메인에 지정된 값만을 가져야 함

### 개체 무결성 제약조건 (entity integrity constraint)
- 기본키 제약(primary key constraint)이라고도 함
- 기본키는 NULL 값이 불가하고 릴레이션 내에 오직 하나의 값만 존재해야 함
- 튜플을 삽입하거나 수정할 때마다 확인

### 참조 무결성 제약조건(referential integrity constraint)
- 외래키 제약(foreign key constraint)이라고도 함
- 참조하는 릴레이션의 외래키는 참조되는 릴레이션의 기본키와 도메인이 동일해야 함
- 참조하는 릴레이션의 값이 변경될 때 참조되는 릴레이션의 제약을 받음
- 잘못된 삭제 시 옵션
  - RESTRICTED: 참조가 있을 경우 참조되는 삭제를 거부
  - CASCADE: 참조되는 튜플을 함께 삭제
  - DEFAULT: 참조되는 튜플을 미리 설정해둔 값으로 변경
  - NULL: 참조되는 튜플을 NULL으로 변경

## 관계대수 (relation algebra)
- 릴레이션에서 원하는 관계를 얻기 위해 대수와 같은 연산을 이용해 질의하는 방법을 기술하는 언어
- 절차적 언어

### 수학적 의미의 릴레이션
- 카티전 프로덕트(AXB): A 원소와 B 원소의 순서쌍의 집합
- 릴레이션(R): 카티전 프로덕트의 부분집합
- 도메인: 카티전 프로덕트의 기초 집합이 가질 수 있는 값의 범위

### 관계대수 연산자
- 순수 관계 연산: selection, projection, join, division, rename
- 일반 집합 연산: union, difference, intersection, cartesian product

### 관계대수식 (relation algebra expression)
- 관계대수 연산을 수행하기 위한 식
- 릴레이션과 연산자로 구성
- 괄호 안의 식이 우선, 왼쪽에서 오른쪽으로 진행
- 결과는 릴레이션으로 반환 (겹치는 튜플 존재하지 않음)
- 기본 형태
  - 단항 연산자: 연산자 릴레이션
  - 이항 연산자: 릴레이션1 연산자 릴레이션2

### 셀렉션 (selection)
- 단항 연산자
- 특정 조건에 해당하는 튜플 반환
- 결과 릴레이션의 차수는 대상 릴레이션과 동일, 카디날리티는 대상 릴레이션 이하
- and, or, not 기호 사용 가능

### 프로젝션 (projection)
- 단항 연산자
- 원하는 속성만 추출
- 결과 릴레이션의 차수는 대상 릴레이션 이하, 카디날리티는 대상 릴레이션과 동일

### 합집합 (union)
- 이항 연산자
- 두 릴레이션은 서로 같은 속성 순서와 도메인을 가져야 함
- 두 개의 릴레이션을 합해서 반환
- 결과는 첫 번째 릴레이션의 속성 이름을 가짐

### 교집합 (intersection)
- 이항 연산자
- 두 릴레이션은 서로 같은 속성 순서와 도메인을 가져야 함
- 두 개의 릴레이션에 공통인 튜플 반환

### 차집합 (set difference)
- 이항 연산자
- 두 릴레이션은 서로 같은 속성 순서와 도메인을 가져야 함
- 첫 릴레이션에만 속하는 튜플 반환

### 카티전 프로덕트 (cartesian product)
- 이항 연산자
- 첫 릴레이션의 오른쪽에 두번째 릴레이션의 모든 튜플을 순서대로 배열해 반환
- 결과 릴레이션의 차수는 두 릴레이션의 차수의 합, 카디날리티는 두 릴레이션의 카디날리티의 곱

### 조인 (join)
- 이항 연산자
- 두 릴레이션의 공통 속성을 기준으로 속성 값이 같은 튜플을 수평으로 결합
- 카티전 프로덕트 이후 셀렉션
- 조인에 참여하는 속성이 서로 동일한 도메인으로 구성되어야 함
- 종류
  - 세타조인(theta join): 두 릴레이션의 속성 값을 비교해 조건을 만족하는 튜플 반환
  - 동등조인(equi join): 세타조인 중 = 연산자 사용한 조인, 결과의 차수는 두 릴레이션의 차수의 합
  - 자연조인(natural join): 동등조인에서 조인에 참여한 속성 중 두 번째 속성 제거, 결과의 차수는 두 릴레이션의 차수의 합 - 1
  - 외부조인(outer join): 자연조인 시 조인에 실패한 튜플을 모두 보여주고 값이 없으면 NULL값 채움
  - 세미조인(semi join): 자연조인 후 두 릴레이션 중 한쪽 릴레이션의 결과만 반환
