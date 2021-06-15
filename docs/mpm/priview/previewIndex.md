---
layout: default
title: 시작하기전에
nav_order: 1
parent: MPM
has_children: false
---

# 시작하기 전에

## MPM(Merchant Presented Mode)

TODO:: Description of MPM

## API G/W

MPM업무의 모든 API들은 API Gateway를 통과한다. API GateWay에서의 오류인 경우 error와 error_description항목을 응답한다. 이외의 경우 각 API에서 기술한 응답을 반환한다.

### Sample: Invalid API Key Error

```json
400 Bad Request
{
  "error": "invalid_apikey",
  "error_description": "Invalid API Key"
}
```
