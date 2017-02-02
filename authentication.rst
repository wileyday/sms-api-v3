API Key 인증
===========

HTTP Header 사용
---------------

HTTP 헤더에 Authorization 정보를 추가하여 인증 받을 수 있습니다.
::
  Authorization: HMAC-SHA256 apiKey=xxxxxx, date=xxxxxx, salt=xxxxxx, signature=xxxxxx

+-----------+-------------+
| Field     | Description |
+-----------+-------------+
| apiKey    | ApiKey      |
+-----------+-------------+
| date      | ISO 규격     |
+-----------+-------------+
| salt      |             |
+-----------+-------------+
| signature |             |
+-----------+-------------+

