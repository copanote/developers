---
layout: default
title: MPM QR코드 검증
nav_order: 2
parent: QR API
grand_parent: MPM
has_children: false
---

# MPM QR 데이터 검증

## 개요

올바른 BC MPM QR 데이터인지 검증

## 선행조건

없음

## Endpoint

| Environment | BASE URL                                               |
| ----------- | ------------------------------------------------------ |
| Development | https://apidev.bccard.com/pay/qrdev/v1.0/mpm/qr_verify |
| Production  | https://api.bccard.com/pay/qr/v1.0/mpm/qr_verify       |

```html
POST https://apidev.bccard.com/pay/qrdev/v1.0/mpm/qr_verify
```

### 요청

| HEADER                                                                                                                                                                                                     |  TYPE  | REQUIRED |
| :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----: | :------: |
| **`x-bc-txid`** <br> API 트랜잭션 ID. 클라이언트에서 필요시 Unique ID로 생성하여 설정. API서버에선 요청 값 그대로 반환한다. 만약 설정하지 않는다면, API서버에서 생성하여 반환한다.                         | String | Optional |
| **`Content-Type`** <br> Http Body의 ContentType을 나타내는 HTTP표준헤더. <br><br> 지원하는 ContentType목록<br> - _application/json;charset=utf-8_ <br> - _application/x-www-form-urlencoded;charset=utf-8_ | String | Required |

| Request Body Parameter                                                                                                                                                                            |  TYPE  | REQUIRED |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :----: | :------: |
| **`QR_DATA`** <br> QR Code 이미지의 데이터. 읽어들인 그대로의 데이터를 전달해야한다. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | String | Required |
| **`AFFI_CO_ID`** <br> 제휴사 ID                                                                                                                                                                   | String | Required |

### Sample 요청 데이터

```json
application/json
{
  "qr_data": "0002010102121531260004102600041075112872400000026310014D41000000140100509000000001520472105303410540432515802KR5910CleanTopia6010KYUNGGI-DO610513204625603090000000010515MQ202090000979306081000011407080000000164210002ko0104비씨카드0203경기도630439F0",
  "affi_co_id": "BCQRCPAY"
}
```

```json
application/x-www-form-urlencoded
qr_data="BCQRCPAY"&affi_co_id="0002010102121531260004102600041075112872400000026310014D41000000140100509000000001520472105303410540432515802KR5910CleanTopia6010KYUNGGI-DO610513204625603090000000010515MQ202090000979306081000011407080000000164210002ko0104비씨카드0203경기도630439F0"
```

### 응답

| Response Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |  TYPE  | REQUIRED |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :----: | :------: |
| **`code`** <br> 응답코드                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | String | Required |
| **`description`** <br> 응답코드 설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | String | Optional |

### 응답코드

| 응답코드 | 설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| :------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  MP0000  | 정상&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|  MP3205  | QR데이터가 다르거나 없음                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|  MP3206  | QR 데이터 파싱 실패                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

### Sample 응답 데이터

```json
application/json
{
  "code": "MP0000",
  "description": "정상"
}
```
