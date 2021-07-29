---
layout: default
title: MPM QR코드 생성
nav_order: 1
parent: QR API
grand_parent: MPM
has_children: false
---

# MPM QR 데이터 생성

## 개요

BCMPM 등록 가맹점의 MPM QR코드 이미지 바이너리를 생성합니다.<br>생성 가능한 이미지 포맷은 다음과 같습니다.
* jpg / jpeg
* bmp
* gif
* png
* wbmp

## 선행조건

* [API키](../priview/previewIndex.html#api키)
* [제휴사ID](../priview/previewIndex.html#제휴사id)

## URL

| Environment | BASE URL                                                |
| ----------- | ------------------------------------------------------- |
| Development | https://apidev.bccard.com/pay/qrdev/v1.0/mpm/qrcode_gen |
| Production  | https://api.bccard.com/pay/qr/v1.0/mpm/qrcode_gen       |

```html
POST https://apidev.bccard.com/pay/qrdev/v1.0/mpm/qrcode_gen
```

## 요청

| HEADER                                                       |  TYPE  | REQUIRED |
| :----------------------------------------------------------- | :----: | :------: |
| **`x-bc-txid`** <br> API 트랜잭션 ID. 클라이언트에서 필요시 Unique ID로 생성하여 설정. API서버에선 요청 값 그대로 반환. 만약 설정하지 않는다면, API서버에서 생성하여 반환 | String | Optional |
| **`Content-Type`** <br> Http Body의 ContentType을 나타내는 HTTP표준헤더 <br><br> 지원하는 ContentType목록<br> - _application/json;charset=utf-8_ <br> - _application/x-www-form-urlencoded;charset=utf-8_ | String | Required |
| **`apikey`** <br> API클라이언트에게 발급된 API키 [_API키 보기_](../priview/previewIndex.html#api키) | String | Required |

| Request Body Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |  TYPE  |  REQUIRED   |
| :----------------------------------------------------------- | :----: | :---------: |
| **`REQ_DATA_TYPE`** <br> MPM QR 데이터를 위한 생성 방식. 3가지 생성 방식이 있고 해당 방식은 숫자형태의 코드값으로 표현. 각각의 코드가 의미하는 값을 `REQ_DATA_VALUE` 항목에 설정 <br><br> 사용 가능한 코드 <br> - **1**: MPM 가맹점번호 `MPM가맹점 등록 시 생성되는 MPM가맹점번호` <br> - **2**: [금융회사공동코드](http://www.kftc.or.kr/kftc/data/EgovBankListMove.do) \| 카드사 가맹점번호 `카드사를 의미하는 금융회사공동코드와 해당 카드사에서 발급받은 가맹점번호` <br> - **3** : MPM회원ID `QrpayForShop App.에 등록된 회원 ID` | String |  Required   |
| **`REQ_DATA_VALUE`** <br> `REQ_DATA_TYPE`에서 설정한 코드가 의미하는 데이터 | String |  Required   |
| **`QR_TYPE`** <br> 생성할 MPM QR 타입 <br><br> 사용 가능한 코드 <br> - **1**: 고정형 `금액이 입력되지 않은 QR코드` <br> - **2**: 변동형 `금액이 입력된 QR코드 AMOUNT항목에 금액을 입력` | String |  Required   |
| **`AMOUNT`** <br> QR_TYPE이 변동형일때 해당 QR코드의 가격. 고정형일때는 이 항목은 무시 | String | Conditional |
| **`TRANSACTION_CURRENCY`** <br> 통화코드 [ISO/IEC 4217](https://www.iso.org/iso-4217-currency-codes.html)을 따르며 3자리의 숫자로 표현 <br> 410:KRW(원화), 840:USD(US달러), 156:CNY(위안화) | String |  Required   |
| **`AFFI_CO_ID`** <br>BCMPM에 등록된 제휴사 ID. 미리 발급받은 제휴ID를 설정 | String |  Optional   |
| **`AFFI_CO_REQ_VAL`** <br> 해당 QR생성 시 제휴사가 설정하는 데이터. 특정 제휴활동의 기반 데이터로 사용. 예를들어 해당 MPM QR로 결제 발생시 제휴사에게 이 항목에 설정한 값을 푸시메시지로 보낼 수 있다. | String |  Optional   |
| **`IMAGE_SIZE`** <br> 응답 QR 이미지 데이터의 가로/세로 픽셀 크기 (기본값: 200 px). 이 항목이 설정되지 않으면 기본값으로 응답 | String |  Optional   |
| **`IMAGE_FORMAT`** <br> 응답 QR 이미지 데이터의 포맷. 이 항목이 설정되지 않으면 기본값으로 응답<br> 이용가능한 이미지 포맷<br> - **jpg**<br> - **jpeg** <br>- **bmp** <br>- **gif**<br>- **png**(기본값)<br>- **wbmp** | String |  Optional   |

## Sample 요청 데이터

```json
application/json
{
  "req_data_type": "2",
  "req_data_value": "361|7653937",
  "qr_type": "2",
  "amount": "1004",
  "transaction_currency": "410",
  "affi_co_id": "bcqrcpay",
  "affi_co_req_val": "QR1873937",
  "image_size": "200",
  "iimage_format": "png",
}
```

```json
application/x-www-form-urlencoded
req_data_type="1"&req_data_value="900003241"&qr_type="1"&transaction_currency="410"&affi_co_id="bcqrcpay"&affi_co_req_val="QR987662"&image_size="300"&iimage_format="jpg"
```

## 응답

| Response Parameter &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |  TYPE  | REQUIRED |
| :----------------------------------------------------------- | :----: | :------: |
| **`code`** <br>[응답코드](#응답코드)                         | String | Required |
| **`description`** <br> 응답코드 설명                         | String | Optional |
| **`QR_BASE64`** <br> base64로 인코딩된 QR 이미지 데이터      | String | Optional |
| **`REG_ATON`** <br> QR 생성시간                              | String | Optional |
| **`QR_REFERENCE_ID`** <br> QR코드 일련번호                   | String | Optional |

## 응답코드

| 응답코드 | 설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| :------: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|  MP0000  | 정상&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|  MP3204  | QR코드 생성 에러                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

## Sample 응답 데이터

```json
application/json
{
    "code": "MP0000",
    "description": "성공",
    "QR_BASE64": "iVBORw0KGgoAAAANSUhEUgAAAMgAAADIAQAAAACFI5MzAAAD4UlEQVR42t2YPa7rOAxGaahwl2xAgLbhTltyNuCfDdhbUudtGPAG4k6FEc2hfOfNTPGKcKqZ4AI38Akk5SP5kYqU373kP0pE2qvvrkdXltatxX26Y07SGEkom2/KNcQyl+PM+yO6eSunkfhm20WONe3P5F/sE3kiLzuRp+7jPi0fKSeP/xW5XhkiIr6Pbor+aSdogH5u6tDAzfqRa/ylzteE+PjX9s+/X5H7muhr4d/mzrpP3/09q74l0iRBzjWHNxoQqE0e3bEaiXt3R9k0PuvGAy9dWZMrRkLWXE2ued25E0Vb37fXaCRuibxlK1ImnNmPW2DD2UguAtJokN2ckOGYRBD1NBKSbh+o4BhOTRlEJVzOSsLC2q1IdyxtQYO+ZberMZKdqp0TEvpn0uUfsazIYCRhavderqETwtK3uIIMXVXUQvwTiyoyFnKnECvprmcKVkJseev7Lnzi3nc7gTrLrY6BkID+0TpyZ5Bj6cISA9KuRnLxoGSN9pzLFNlzp+ZOIwmfjpIlE8On1QcNT6TWnIVcvfC9Se39WUp1Poz5ehnJLpHwKnxmN/PBiLNWd7EQebQI6TEAcmcQlbaPVQML8WM+FtpFDGv6y6tmIwkYQKNmfHxYPlMu7kcDC9F2PcVjps4SKXOJkJvVXSyE7op9oqt7i/6dSfrbXSxEW+KZiA915h8RSeoTIwnz5t6RLqQHP7OeV53VSFjSj0kbBd27lovus1rJJAFF180zUzD4aO5I7dsWcpfIpd11O26vGu6OYSGEF3fXw7LbmconukX8y0jklVlbJ7ux6A4fZopUvcpCmLyuZvOc/aE2gwY7sTqNRPd5KSHsFIeXqAdfjcQPZCO+kos2/ywj6t4aWAgDNZ1W137XXsGGU3u7mIEw01EfzCnso7MYuSPVnk3ED51qMGagelWTj3c0E/duj6neSzjsW1uH5k5jJLwYK/SwYyGdd2nVq4qRCOXbx7p8x2WCsUKaLVjJjjnRMZ7YTKGhhTNVezYSjQ+rimZ04fGkreNHg+8Jozo1R8ExpNCukZYGzoY2QrfhcnmJCvAz+zd3xzCRNx5Q76yLcLEjd9QSZiO59M6UyMcwp4PplSr55WLfE/WDRodEGVquhgSnrPmXi31NmDHP6i6Y/Uy4ksjPHG8gmsJNZqAOtSWGSQ3eTKh+V5LOYqTzpJOsbvsyEiYvvnHtQiiRvY6fd2+0EO7oDj8ec72j3151a2AkzNR7w3CRdHmdxbZ7SjOSUy2hLK3OYgNDaLxeRqK/H3DXnPEqRtfMPMsN7E91vib6+wFHPrOeXWftFgvcGyP5v/3K9rvXHxJyPAXEEE3jAAAAAElFTkSuQmCC",
    "REG_ATON": "20210615130958",
    "QR_REFERENCE_ID": "MQ2021900010260"
}
```
