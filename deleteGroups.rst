그룹 삭제
=========

생성된 그룹을 삭제합니다.

Method
------
POST

Path
----
deleteGroups

Resource URL
------------

`<https://coolsms.co.kr/sms/3/deleteGroups>`_

Request Syntax
--------------

.. code-block:: javascript

  {
    "groups": [
    ],
  }

 
Response Syntax
---------------

.. code-block:: javascript

  {
    "ErrorCount": Number,
    "ResultList": [
      {
        "MessageId": String,
        "StatusCode": String
      }
    ]
  }

ErrorCount
  오류 카운트
MessageId
  메시지ID
StatusCoe
  쿨에스엠에 메시지 상태 코드


Sameple Request
---------------

.. code-block:: javascript

  POST / HTTP/1.1
  Content-Length: <PayloadSizeBytes>     
  User-Agent: <UserAgentString>
  Content-Type: application/json
  Authorization: HMAC-SHA256 ApiKey=<API_KEY>, Date=<DATE>, Salt=<SALT>, Signature=<SIGNATURE>
  
  {
    "groups": [
    ]
  }


Sample Response
---------------

.. code-block:: javascript

  HTTP/1.1 200 OK
  Content-Type: application/json
  Content-Length: <PayloadSizeBytes>

  {
    "ErrorCount": 2,
    "ResultList": [
      {
        "MessageId": "MIDXXXXXXXXXXXX",
        "ResultCode": "2000"
      },
      {
        "MessageId": "MIDXXXXXXXXXXXX",
        "ResultCode": "1030"
      },
      {
        "MessageId": "MIDXXXXXXXXXXXX",
        "ResultCode": "1030"
      }      
    ]
  }

