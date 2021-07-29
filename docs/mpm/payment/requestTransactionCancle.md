---
layout: default
title: 승인취소 요청
nav_order: 1
parent: Payment API
grand_parent: MPM
has_children: false
---

# 제휴사 승인 취소 요청

## 개요

등록된 제휴사로부터 MPM QR로 발생한 승인 건에 대해 취소를 요청합니다.

## 선행조건

* [API키](../priview/previewIndex.html#api키)
* [제휴사ID](../priview/previewIndex.html#제휴사id)
* [서명검증을 위한 RSA키](../priview/previewIndex.html#서명검증을-위한-RSA키)

## URL

| Environment | BASE URL                                                          |
| ----------- | ----------------------------------------------------------------- |
| Development | https://apidev.bccard.com/pay/qrdev/v1.0/mpm/affi_co_trans_cancle |
| Production  | https://api.bccard.com/pay/qr/v1.0/mpm/affi_co_trans_cancle       |

```html
POST https://apidev.bccard.com/pay/qrdev/v1.0/mpm/affi_co_trans_cancle
```

## 요청

| HEADER                                                       |  TYPE  | REQUIRED |
| :----------------------------------------------------------- | :----: | :------: |
| **`x-bc-txid`** <br> API 트랜잭션 ID. 클라이언트에서 필요시 Unique ID로 생성하여 설정. API서버에선 요청 값 그대로 반환한다. 만약 설정하지 않는다면, API서버에서 생성하여 반환 | String | Optional |
| **`Content-Type`** <br> Http Body의 ContentType을 나타내는 HTTP표준헤더. <br><br> 지원하는 ContentType목록<br> - _application/json;charset=utf-8_ <br> - _application/x-www-form-urlencoded;charset=utf-8_ | String | Required |
| **`apikey`** <br>API클라이언트에게 발급된 API키 [_API키 보기_](../priview/previewIndex.html#api키) | String | Required |

| Request Body Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |  TYPE  | REQUIRED |
| :----------------------------------------------------------- | :----: | :------: |
| **`AFFI_CO_TRNS_UNIQ_NO`** <br> 제휴사에서 거래를 식별하기 위해 Unique하게 채번한 거래고유번호. API서버는 전달받은 값은 그대로 응답 | String | Required |
| **`CARD_CO_AUTH_NO`** <br>원거래 카드사 승인번호             | String | Required |
| **`TRNS_ATON`** <br> 원거래 거래일시                         | String | Required |
| **`QR_REFERENCE_ID`** <br> 원거래 QR일련번호                 | String | Required |
| **`AFFI_CO_ID`** <br>BCMPM센터에 등록된 제휴사 ID. 미리 발급받은 제휴ID를 설정 | String | Required |
| **`SIGNATURE`** <br> Signature 대상 데이터에 대해 제휴사에서 생성한 서명검증을 위한 Private키를 이용해 SHA256withRSA 알고리즘으로 서명데이터를 생성 <br><br>아래 항목의 순서대로 각각의 데이터를 구분자 없이 연결(concatenation)하여 서명을 생성 <br> 1. `AFFI_CO_TRNS_UNIQ_NO` <br> 2. `CARD_CO_AUTH_NO` | String | Required |

## Sample 요청 데이터

```json
application/json
{
  "affi_co_trns_uniq_no": "11112234512",
  "card_co_auth_no": "98181361",
  "trns_aton": "20190916105353",
  "qr_reference_id": "MQ2019900086179",
  "affi_co_id": "bcqrcpay",
  "signature": "mjbCvTeqsZ6dkGwIcSkmKRV7RsjNysk/lcXaLaEGLVrflfViGMydm5J+TFpwUFjCtJ3nGhkpLly1VQriBCDa1IXJtlLG4vD/Fs2GLsOF0YQq5Ta0iACicTBQQwqYoaSiqs4l/hMQkgGOT8PGeQVuVs4YgVVi2d2W/KDG+lr7eTs=",
}
```

```json
application/x-www-form-urlencoded
affi_co_trns_uniq_no="11112234512"&card_co_auth_no="98181361"&trns_aton="20190916105353"&qr_reference_id="MQ2019900086179"&affi_co_id="bcqrcpay"&signature="mjbCvTeqsZ6dkGwIcSkmKRV7RsjNysk/lcXaLaEGLVrflfViGMydm5J+TFpwUFjCtJ3nGhkpLly1VQriBCDa1IXJtlLG4vD/Fs2GLsOF0YQq5Ta0iACicTBQQwqYoaSiqs4l/hMQkgGOT8PGeQVuVs4YgVVi2d2W/KDG+lr7eTs="
```

## 응답

| Response Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |  TYPE  | REQUIRED |
| :----------------------------------------------------------- | :----: | :------: |
| **`code`** <br>[응답코드](#응답코드)                         | String | Required |
| **`description`** <br> 응답코드 설명                         | String | Optional |
| **`CNCL_TRNS_STAT`** <br> 취소상태<br><br>상태가능 코드<br> - **90**(취소요청)<br> - **95**(취소성공) <br> - **99**(취소실패) | String | Optional |
| **`TRNS_UNIQ_NO`** <br>BCMPM에서 사용한 거래고유번호         | String | Optional |
| **`AFFI_CO_TRNS_UNIQ_NO`** <br> 제휴사에서 요청전문에 전달한 값을 그대로 응답 | String | Optional |
| **`CARD_CO_AUTH_NO`** <br> 카드사 승인번호                   | String | Optional |

## 응답코드

| 응답코드 | 설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| :------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  MP0000  | 정상&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|  MP3300  | 유효하지 않은 거래내역                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|  MP3301  | 취소가능한 거래내역이 아님                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|  MP3305  | 승인취소 실패                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|  MP3308  | 승인취소 권한 없음                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|  MP3312  | Signature검증 실패                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

## Sample 응답 데이터

```json
application/json
{
    "code": "MP0000",
    "description": "성공",
    "CNCL_TRNS_STAT": "95",
    "TRNS_UNIQ_NO": "2375123571737",
    "AFFI_CO_TRNS_UNIQ_NO": "11112234512",
    "CARD_CO_AUTH_NO": "98181361",
}
```
