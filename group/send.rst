그룹메시지 발송
==============
 
그룹메시지를 발송합니다.
 
Method
------
POST
 
Path
----
group/{groupId}/send
 
Resource URL
------------
`<https://solapi.com/sms/3/group/{groupId}/send>`_
 
Parameters
----------
None
 
Response
--------
groupId
  - 그룹아이디
  
  
Request Syntax
--------------
None


Response Syntax
---------------
.. code-block:: javascript

  {
    "groupId": String
  }

groupId
  그룹ID가 리턴됩니다.
  
Example Request
---------------

.. code-block:: javascript

  POST / HTTP/1.1
  Content-Length: <PayloadSizeBytes>
  User-Agent: <UserAgentString>
  Content-Type: application/json
  Authorization: HMAC-SHA256 ApiKey=<API_KEY>, Date=<DATE>, Salt=<SALT>, Signature=<SIGNATURE>
 


Example Response
----------------

.. code-block:: javascript

  HTTP/1.1 200 OK
  Content-Type: application/json
  Content-Length: <PayloadSizeBytes>

  {
    "groupId": "GID587C220F0734A"
  }
  
  
