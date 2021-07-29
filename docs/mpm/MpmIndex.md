---
layout: default
title: MPM
nav_order: 2
has_children: true
---

## MPM(Merchant Presented Mode)이란

가맹점(Merchant)에서 생성한 QR코드(거치형 or App생성)를 고객의 결제 App에서 Scan하여 결제하는 방식을 의미합니다. 비씨카드에서 MPM서비스를 제공하는 시스템을 BCMPM이라고 합니다.

BCMPM에서는 가맹점(Merchant)에 MPM-QR 서비스를 위한 API를 크게 3가지 종류로 구성되어 있습니다.

1. QR API
   * QR코드 생성에 필요한 API입니다.
2. Payment API
   * 가맹점(Merchant)에서 가능한 거래(취소)에 사용하는 API입니다.
3. Transaction Inquiry API
   * 거래내역을 확인할 수 있는 API입니다.