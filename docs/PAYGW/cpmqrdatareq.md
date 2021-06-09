# CPM QR 결제 데이터 요청

### Description

Offline 결제에 사용할 CPM QR 데이터를 받는다.

### Endpoint

```js
POST http://paygwdev.bccard.com/paygw/cpmqrdatareq
```

### Request

| HEADER                                                                 | TYPE   | REQUIRED     |
| :--------------------------------------------------------------------- | :----- | :----------- |
| **`Authorization`** <br> API 인증을 위해 미리 공유된 credential을 설정 | String | **Required** |

<br>

| REQUEST PARAMETER                                                                                                                                  | TYPE     | REQUIRED     |
| :------------------------------------------------------------------------------------------------------------------------------------------------- | :------- | :----------- | --- | ------ | ------------ |
| **`REQUESTOR_ID`** <br> TSP서비스 계약시 발급된 ID                                                                                                 | String   | **Required** |
| **`MSG_ID`** <br> 메시지 ID                                                                                                                        | String   | **Required** |
| **`MSG_VER`** <br> API 버전                                                                                                                        | String   | **Required** |
| **`CRTPYO_TYPE`** <br> [TSP 암호화구분 코드]()                                                                                                     | String   | **Required** |
| **`CRYPTO_KEY_VER`** <br> 암호화 키 버전                                                                                                           | String   | **Required** |
| **`TRNS_TRACE_NO`** <br> 한 API 트랜잭션간 유일한 거래추적번호. Client에서 40Byte 이하로 자유롭게 생성한다.                                        | String   | **Required** |
| **`ENC_DATA`** <br> 암호화 항목을 요청한 CRYPTO_TYPE으로 암호화 한 byte array를 Base64방식으로 인코딩 한 데이터<br><br> 암호화항목: `디지털PAN번호 | 요청시간 | 거래추적번호 | `   | String | **Required** |

### Sample Request Data

```json
{
  "PAYGW": {
    "REQID": "cpmqrdatareq",
    "VERSION": "1.0",
    "REQUEST": {
      "CRYPTO_KEY_VER": "00",
      "CRYPTO_TYPE": "00",
      "HASH_CRC": "Vbo9SiU/ZsD7D/tRaJjpz7PJl3rpVSUV091c17+X5rE=",
      "MSG_VER": "01",
      "RSLT_TYPE": "JSON",
      "REQUESTOR_ID": "42000000066",
      "MSG_CD": "Q200",
      "REG_ATON": "20200623090000",
      "TRNS_TRCE_NO": "NPAY202009XX123XXXX35",
      "REQ_KEY_DV": "1",
      "ENC_DATA": "hQVDUFYwMWFaTwfUEAAAAUAQVxNTUCBpAAAAZtIAdgEAAAAAAAmfXzQBAmM2nyYImERHcznr1n2fJwGAnxAUBQmgAAgAAAAAAAAAICAGERdRIQGfNgIAi4ICAACfNwRm4DtF",
      "CPMQR_DATA_CLSS": "1",
      "DNF_DV": "1",
      "APP_DV": ""
    }
  }
}
```

### Response

에러가 발생하지 않았다면, HTTP 상태코드 '200 OK' 와 함께 응답 바디에 JSON형식의 Object를 반환한다.

| RESPONSE PARAMETER                                                                            | TYPE   | REQUIRED     |
| :-------------------------------------------------------------------------------------------- | :----- | :----------- |
| **`REQUESTOR_ID`** <br> TSP서비스 계약시 발급된 ID                                            | String | **Required** |
| **`MSG_ID`** <br> 메시지 ID                                                                   | String | **Required** |
| **`CRYPTO_KEY_VER`** <br> 암호화 키 버전                                                      | String | **Required** |
| **`RSLT_CD`** <br> [TSP 응답코드]()                                                           | String | **Required** |
| **`RSLT_MSG`** <br> 응답코드 설명메시지                                                       | String | **Required** |
| **`CPMQR_DATA`** <br> CPM QR데이터. 월렛 App에서는 해당 데이터 그대로 QR코드로 생성해야 한다. | String | **Required** |

### Sample Response Data

```json
{
  "PAYGW": {
    "REQID": "cpmqrdatareq",
    "VERSION": "1.0",
    "RESPONSE": {
      "CPMQR_DATA": "hQVDUFYwMWFaTwfUEAAAAUAQVxNTUCBpAAAAZtIAdgEAAAAAAAmfXzQBAmM2nyYImERHcznr1n2fJwGAnxAUBQmgAAgAAAAAAAAAICAGERdRIQGfNgIAi4ICAACfNwRm4DtF",
      "CRYPTO_KEY_VER": "00",
      "CRYPTO_TYPE": "00",
      "HASH_CRC": "Vbo9SiU/ZsD7D/tRaJjpz7PJl3rpVSUV091c17+X5rE=",
      "MSG_VER": "01",
      "RSLT_TYPE": "JSON",
      "MSG_CD": "Q200",
      "REQUESTOR_ID": "42000000066",
      "QR_DATA_MAPP_VAL": "95050000000800900019F26084934E9FD0E3E169",
      "RSLT_CD": "0000",
      "RSLT_MSG": "성공"
    }
  }
}
```
