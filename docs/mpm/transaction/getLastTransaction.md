---
layout: default
title: 마지막 거래 조회
nav_order: 1
parent: Transaction Inquiry API
grand_parent: MPM
has_children: false
---

# 마지막 거래 조회

## 개요

MPM QR로 처리된 거래에 대해 요청식별정보(타입 및 데이터)에 해당 하는 승인거래를 조회합니다.

## 선행조건

* [API키](../preview/previewIndex.html#api키)
* [제휴사ID](../preview/previewIndex.html#제휴사id)

## URL

| Environment | BASE URL                                                    |
| ----------- | ----------------------------------------------------------- |
| Development | https://apidev.bccard.com/pay/qrdev/v1.0/mpm/last_trns_info |
| Production  | https://api.bccard.com/pay/qr/v1.0/mpm/last_trns_info       |

```html
POST https://apidev.bccard.com/pay/qrdev/v1.0/mpm/last_trns_info
```

## 요청

| HEADER                                                       |  TYPE  | REQUIRED |
| :----------------------------------------------------------- | :----: | :------: |
| **`x-bc-txid`** <br> API 트랜잭션 ID. 클라이언트에서 필요시 Unique ID로 생성하여 설정. API서버에선 요청 값 그대로 반환한다. 만약 설정하지 않는다면, API서버에서 생성하여 반환 | String | Optional |
| **`Content-Type`** <br> Http Body의 ContentType을 나타내는 HTTP표준헤더. <br><br> 지원하는 ContentType목록<br> - _application/json;charset=utf-8_ <br> - _application/x-www-form-urlencoded;charset=utf-8_ | String | Required |
| **`apikey`** <br>API클라이언트에게 발급된 API키 [_API키 보기_](../preview/previewIndex.html#api키) | String | Required |

| Request Body Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |  TYPE  | REQUIRED |
| :----------------------------------------------------------- | :----: | :------: |
| **`REQ_DATA_TYPE`** <br> 요청데이터 타입 <br><br> 사용 가능한 코드 <br> - **4**: QR일련번호(QR Reference Id) | String | Required |
| **`REQ_DATA_VALUE`** <br> `REQ_DATA_TYPE`에서 설정한 코드가 의미하는 데이터 | String | Required |
| **`AFFI_CO_ID`** <br> BCMPM에 등록된 제휴사 ID. 미리 발급받은 제휴ID를 설정 | String | Required |

## Sample 요청 데이터

```json
application/json
{
  "req_data_type": "4",
  "req_data_value": "MQ2019900086199",
  "affi_co_id": "bcqrcpay",
}
```

```json
application/x-www-form-urlencoded
req_data_type="4"&req_data_value="MQ2019900086199"&affi_co_id="bcqrcpay"
```

## 응답

| Response Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |  TYPE  | REQUIRED |
| :----------------------------------------------------------- | :----: | :------: |
| **`code`** <br> [응답코드](#응답코드)                        | String | Required |
| **`description`** <br> 응답코드 설명                         | String | Optional |
| **`TRNS_UNIQ_NO`** <br> BCMPM에서 사용한 거래고유번호        | String | Optional |
| **`TRNS_ATON`** <br> 거래일시(yyyyMMddHHmmss)                | String | Optional |
| **`TRNS_KND_CLSS`** <br> 거래구분코드 <br> - **10**: 승인 <br> - **90**: 취소 | String | Optional |
| **`SVC_CLSS`** <br> 서비스구분코드 <br> - **B**: 비씨 <br> - **U**: 은련 | String | Optional |
| **`TRNS_STAT`** <br> 승인상태코드<br> - **10**: 승인요청 <br> - **15**: 승인성공 <br> - **18**: Reversal(취소진행중) <br> - **19**: 승인실패 <br> - **90**: 취소요청 <br> - **95**: 승인취소 <br> - **99**: 취소실패 | String | Optional |
| **`TRNS_AMT`** <br> 거래금액                                 | String | Optional |

## 응답코드

| 응답코드 | 설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| :------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  MP0000  | 정상&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|  MP9999  | 조회 실패                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

## Sample 응답 데이터

```json
application/json
{
    "code": "MP0000",
    "description": "성공",
    "TRNS_UNIQ_NO": "2375123571737",
    "TRNS_ATON": "20190916105353",
    "TRNS_KND_CLSS": "10",
    "SVC_CLSS": "B",
    "TRNS_STAT": "15",
    "TRNS_AMT": "4100",
}
```
