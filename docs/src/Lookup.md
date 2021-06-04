---
layout: default
title: lookup
nav_order: 1
grand_parent: SRC
parent: SRC REST API
has_children: false

---

## 7.1 Identity Lookup

 

### 7.1.1 개요

* Http Verb : POST
* Path : /identities/lookup
* 설명 : 고객식별정보를 바탕으로 SRC에 등록되어 있는 고객이 있는지 확인


### 7.1.2 입출력 Parameter

* 입력 Parameter


| R/C/O | Name | Type | Description | Note |
| ----- | ---- | ---- | ----------- | ---- |
| R     | srcClientId       | UUID   | SRC에 접속하는 Client를 식별하기 위한 ID이며, 접속 Client의 UUID를 사용 (e.g. SRCI, DCF, SRCPI) |        |
| R    | consumerIdentity | [ConsumerIdentity](#consumeridentity) | SRCI에서  입력된 고객 식별 데이터 |  |


* 출력 Parameter

 | R/C/O | Name | Type | Description | Note |
| ----- | ---- | ---- | ----------- | ---- |
| C | consumerPresent | Boolean | SRC에서 현재 고객정보 존재 여부 | |
| C | consumerStatus | ENUM | SRC의 현재 고객 상태<br />* ACTIVE<br />* SUSPENDED<br />* LOCKED | |
| C | idLookupSessionId | String | Identity  Lookup Session을 유지하기 위한 값으로, Initiate Identity Validation의 요청값으로 입력 ||


### 7.1.3 처리 프로세스

 
1. 입력한 consumerIdentity 정보를 이용해 Consumer 테이블에서 고객정보를 조회

```js

/*
* consumerIdentity.identityType과 consumerIdentity.identityValue를 이용해 Consumer 테이블을 조회
* 가능한 consumerIdentity.identityType = MOBILE_PHONE_NUMBER만 가능
*/

```

2. 정상 조회된 경우 idLookupSessionId를 생성하여 응답

```js
/*
* 조회된 값이 있는 경우 응답값과 idLookupSessionId를 생성하여 리턴
* Session 관리는 ApiSessionService를 이용
*/
```