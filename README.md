# learn_spring_jpa
[study] 실전! 스프링 부트와 JPA 활용1 - 웹 애플리케이션 개발

## 기능목록
#### 회원 기능
- 회원 등록
- 회원 조회
#### 상품 기능
- 상품 등록
- 상품 수정
- 상품 조회
#### 주문 기능
- 상품 주문
- 주문 내역 조회
- 주문 취소
#### 기타 요구사항
- 상품은 재고 관리가 필요하다.
- 상품의 종류는 도서, 음반, 영화가 있다.
- 상품을 카테고리로 구분할 수 있다.
- 상품 주문시 배송 정보를 입력할 수 있다.

---

## 엔티티 설계
![image](https://github.com/duyankim/learn_spring_jpa/assets/46421950/0e40c727-d45c-45d9-8355-9ddf32e12521)

#### 회원 `Member`
- 이름
- 주소(임베디드 타입)
- 주문 list

#### 주문 `Order`
- OrderItem:Order = 1:n 관계
- 주문한 회원
- 배송정보
- 주문 날짜
- 주문 상태(ORDER, CANCEL)

#### 주문상품 `OrderItem`
- 상품 정보
- 주문 금액
- 주문 수량

#### 상품 `Item`
- 이름
- 가격
- 재고 수량 (상품 주문시 재고 수량이 줄어든다)
- 종류 (도서, 음반, 영화)

#### 배송 `Delivery`
- 주문시 하나의 배송정보 생성
- 주문:배송 = 1:1

#### 카테고리 `Category`
- 상품:카테고리 = m:n
- parent, child로 부모 자식 카테고리 연결

#### 주소 `Address`
- 값 타입(임베디드 타입)
- 회원, 배송에서 사용

---
### 회원 테이블 분석
![image](https://github.com/duyankim/learn_spring_jpa/assets/46421950/9f73ad9d-23ae-425f-8021-f2fb196a51fd)

- Member와 Delivery에 Address 임베디드 타입 정보가 그대로 들어간다.
- Item의 타입은 DTYPE 컬럼으로 구분한다.
