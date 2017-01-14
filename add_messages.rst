POST groups/{group_id}/add_messages
===================================

그룹에 발송할 문자메시지를 추가합니다.

Resource URL
------------

https://coolsms.co.kr/sms/3/group/{group_id}/add_messages

Parameters
----------

- To
  수신번호 입력<br>콤마(,)로 구분된 수신번호 입력가능
  예) 01012345678,01023456789,01034567890
- From
  발신번호 입력
  2015/10/16 발신번호 사전등록제에 의해 반드시 등록된 번호만 허용됩니다. (해외문자 제외)
  예) 0212345678
- Text
  문자내용
- Type
  CTA(친구톡), ATA(알림톡), SMS(90바이트), LMS(장문 2,000바이트), MMS(장문+이미지)
  미입력시 SMS
  해외문자인 경우 SMS만 가능
- ImageID
  발송할 이미지의 아이디<br>type이 MMS일 때 필수
- Country
  한국: 82, 일본: 81, 중국: 86, 미국: 1, 기타 등등 (기본 한국)<br>http://countrycode.org 참고
- ScheduledDate
  예약시간을 YYYYMMDDHHMISS 포맷으로 입력 (입력 없거나 지난날짜를 입력하면 바로 전송)<br>예) 20131216090510 (2013년 12월 16일 9시 5분 10초에 발송되도록 예약)
- Subject
  LMS, MMS 일때 제목 (40바이트)


제한 사항
--------

to 필드의 전화번호 수는 최대 1,000개이며 넘을 경우 오류를 발생 (RecipientsTooMany)

한번의 Request의 총 데이터 크기는 2MB를 넘을 수 없습니다 (HTTP ERROR 413 발생)

발송형태별 제한사항
---------------

이동통신사 내부적으로 완성형한글로 변환되므로 영어 1바이트, 한글 2바이트로 취급됩니다.

- SMS
  90바이트 까지 전송가능 (한글 45자)
- LMS
  2,000바이트 까지 전송가능 (한글 1,000자)
- MMS
  2,000바이트 텍스트 (한글 1,000자)<br>1개의 이미지 전송 (300KB. 2048x2048픽셀 이하인 JPEG, PNG, GIF 형식 파일)


Request Syntax
--------------

::

  {
    "Authorization" : {
      "ApiKey": String,
      "Date": String,
      "Salt": String,
      "Signature": String,
    },
    "To": [
      String,
      ...
    ],
    "From": String,
    "Text": String,
    "Type": String,
    "ImageID": String,
    "Country": String,
    "ScheduledDate": String,
    "Subject": String
  }

 
Response Syntax
---------------

::

  {
    "Count": Number,
    "ResultList": [
      {
        "Code": String,
        "Message": String
      }
    ]
  }

Sameple Request
---------------

::

  {
    "Authorization" : {
      "ApiKey": "xxxx",
      "Date": "2017-01-14T13:10:30+09:00",
      "Salt": "SALT-123456789",
      "Signature": "SIGNATURExxxxx",
    },
    "To": [
      "01048597580",
      "01048597581",
      "01048597582",
      "01048597583",
      "01048597584"
    ],
    "From": "029302266",
    "Text": "테스트 문자",
    "Type": "SMS",
    "ImageID": "IMGABCDEFGGHIJKL",
    "Country": "82",
    "ScheduledDate": "2017-01-14T14:20:30+09:00",
    "Subject": "MMS 제목"
  }


Sample Response
---------------

::

  {
    "Count": 3,
    "ResultList": [
      {
        "Code": "1030",
        "Message": "잔액 "
      },
      {
        "Code": "1030",
        "Message": "잔액 소진"
      },
      {
        "Code": "1030",
        "Message": "잔액 소진"
      }
    ]
  }

Response의 내용은 서버에 전송 요청한 것에 대한 정보이며 실제 휴대전화로 전송한 것에 대한 정보가 아닙니다.  sent 조회로 실제 전송된 결과를 확인하실 수 있습니다.
