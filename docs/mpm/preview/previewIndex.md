---
layout: default
title: 시작하기전에
nav_order: 1
parent: MPM
has_children: false
---

# 시작하기 전에

## API키

일부 API를 제외한 BCMPM의 API호출을 위해 API키를 발급받아야 합니다. Development/Production환경에서 사용할 API키를 발급받으려면 API담당자로부터 발급을 받아야합니다. Test를 위한 API키는 아래와 같습니다.

> apikey: `1231231231`

## 제휴사ID

MPM QR의 생성/결제/취소/조회 과정에서 특정 제휴동작을 하려면 미리 제휴사ID를 등록해야 합니다. 제휴사ID는 API담당자로부터 발급을 받아야 합니다.

## 서명검증을 위한 RSA키

특정 API의 경우 메시지의 무결성 및 부인방지를 위해 서명데이터를 요구하고 있습니다. 서명 생성 및 API서버에서 서명데이터 검증을 위해 Development/Production 환경에서 사용할 RSA키를 생성합니다. 제휴사에서는 API담당자에게 공개키를 전달합니다.

## 오류처리

### 시스템 오류

시스템 오류인 경우 error와 error_description항목을 응답합니다.

##### Sample: Invalid API Key Error

```json
400 Bad Request
{
  "error": "invalid_apikey",
  "error_description": "Invalid API Key"
}
```

### 그 외의 오류

시스템 오류 이외의 비즈니스 오류등은 API 문서에 정의된 내용으로 응답합니다.

