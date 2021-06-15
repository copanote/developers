---
layout: default
title: MPM QR코드 정보 조회
nav_order: 3
parent: QR API
grand_parent: MPM
has_children: false
---

# MPM QR 정보조회

## 개요

MPM QR코드의 가맹점정보를 조회한다.

## 선행조건

### API인증/권한

API호출에 대한 API키를 발급받아야 합니다. Development/Production환경에서 사용할 API키를 발급받으려면 API담당자로부터 발급을 받아야합니다. Test를 위한 API키는 아래와 같습니다.

> apikey: `1231231231`

## Endpoint

| Environment | BASE URL                                                 |
| ----------- | -------------------------------------------------------- |
| Development | https://apidev.bccard.com/pay/qrdev/v1.0/mpm/get_qr_info |
| Production  | https://api.bccard.com/pay/qr/v1.0/mpm/get_qr_info       |

```html
POST https://apidev.bccard.com/pay/qrdev/v1.0/mpm/get_qr_info
```

## 요청

| HEADER                                                                                                                                                                                                     |  TYPE  | REQUIRED |
| :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----: | :------: |
| **`x-bc-txid`** <br> API 트랜잭션 ID. 클라이언트에서 필요시 Unique ID로 생성하여 설정. API서버에선 요청 값 그대로 반환한다. 만약 설정하지 않는다면, API서버에서 생성하여 반환한다.                         | String | Optional |
| **`Content-Type`** <br> Http Body의 ContentType을 나타내는 HTTP표준헤더. <br><br> 지원하는 ContentType목록<br> - _application/json;charset=utf-8_ <br> - _application/x-www-form-urlencoded;charset=utf-8_ | String | Required |
| **`apikey`** <br> API클라이언트에게 발급된 API키. [_API인증/권한 보기_](#api인증권한)                                                                                                                      | String | Required |

| Request Body Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |  TYPE  | REQUIRED |
| :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----: | :------: |
| **`AFFI_CO_TRNS_UNIQ_NO`** <br> 제휴사거래고유번호                                                                                                                                                                                                                                                                                                                                                                                                                                        | String | Required |
| **`QR_DATA`** <br> QR코드 데이터                                                                                                                                                                                                                                                                                                                                                                                                                                                          | String | Required |

## Sample 요청 데이터

```json
application/json
{
  "affi_co_trns_uniq_no": "1182083830311",
  "qr_data": "0002010102121531260004102600041075112872400000026310014D41000000140100509000000001520472105303410540432515802KR5910CleanTopia6010KYUNGGI-DO610513204625603090000000010515MQ202090000979306081000011407080000000164210002ko0104비씨카드0203경기도630439F0",
}
```

```json
application/x-www-form-urlencoded
affi_co_trns_uniq_no="1182083830311"&qr_data="0002010102121531260004102600041075112872400000026310014D41000000140100509000000001520472105303410540432515802KR5910CleanTopia6010KYUNGGI-DO610513204625603090000000010515MQ202090000979306081000011407080000000164210002ko0104비씨카드0203경기도630439F0"
```

## 응답

| Response Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |  TYPE  | REQUIRED |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :----: | :------: |
| **`code`** <br> 응답코드                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | String | Required |
| **`description`** <br> 응답코드 설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | String | Optional |
| **`AFFI_CO_TRNS_UNIQ_NO`** <br> 제휴사거래고유번호                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | String | Optional |
| **`CARD_CO_MER_MGMT_NO`** <br> 카드사 가맹점번호                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | String | Optional |
| **`CARD_CO_MER_NM`** <br> 카드사 가맹점 명                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | String | Optional |

## 응답코드

| 응답코드 | 설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| :------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  MP0000  | 정상&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|  MP9999  | QR코드 정보 조회 실패                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

## Sample 응답 데이터

```json
application/json
{
    "code": "MP0000",
    "description": "성공",
    "AFFI_CO_TRNS_UNIQ_NO": "1182083830311",
    "CARD_CO_MER_MGMT_NO": "751128724",
    "CARD_CO_MER_NM": "비씨카드"
}
```
