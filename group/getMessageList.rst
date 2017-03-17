그룹메시지 목록
==============

그룹에 추가된 문자메시지 목록을 조회합니다.

Method
------
GET

Path
----
group/{GroupId}/getMessageList

Resource URL
------------

`<https://coolsms.co.kr/sms/3/group/{groupId}/getMessageList>`_

Parameters
----------
None

Request Syntax
--------------
None
 
Response Syntax
---------------

.. code-block:: javascript

  [
    String,
    ...
  ]

Sample Request
---------------

.. code-block:: javascript

  POST / HTTP/1.1
  Content-Length: <PayloadSizeBytes>     
  User-Agent: <UserAgentString>
  Content-Type: application/json
  Authorization: HMAC-SHA256 ApiKey=<API_KEY>, Date=<DATE>, Salt=<SALT>, Signature=<SIGNATURE>
  

Sample Response
---------------

.. code-block:: javascript

  HTTP/1.1 200 OK
  Content-Type: application/json
  Content-Length: <PayloadSizeBytes>

  [
    {
      "MessageId": "MIDXXXXXXXXXXXX",
      "ResultCode": "2000"
    },
    ...
  ]


