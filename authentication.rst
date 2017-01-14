Request 인증받기
==============

HTTP Header 사용
---------------

HTTP 헤더에 Authorization 정보를 추가하여 인증 받을 수 있습니다.
::
  Authorization: HMAC-SHA256 ApiKey=xxxxxx, Date=xxxxxx, Salt=xxxxxx, Signature=xxxxxx

+-----------+-------------+
| Field     | Description |
+-----------+-------------+
| ApiKey    | ApiKey      |
+-----------+-------------+
| Date      | ISO 규격     |
+-----------+-------------+
| Salt      |             |
+-----------+-------------+
| Signature |             |
+-----------+-------------+


HTTP body에 포함
---------------
HTTP body에 JSON 취상위에 Authorization 정보를 추가하여 인증 받을 수 있습니다.
::
  {
    "Authorization" : {
      "ApiKey": String,
      "Date": String,
      "Salt": String,
      "Signature": String,
    },
    ...
  }
