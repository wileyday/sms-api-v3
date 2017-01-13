# POST groups/{group_id}/add_messages

그룹에 발송할 문자메시지를 추가합니다.

## Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group_id}/add_messages](https://api.coolsms.co.kr/sms/2/groups/{group_id}/add_messages)

## Parameters

| Mandatory | Field | Description |
| --------- | ----- | ----------- |
| Ο         | 인증정보 | 인증데이터는 필수입니다.<br>[Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고 |
| O         | to     | 수신번호 입력<br>콤마(,)로 구분된 수신번호 입력가능<br>예) 01012345678,01023456789,01034567890 |
| O         | from   | 발신번호 입력<br>2015/10/16 발신번호 사전등록제에 의해 반드시 등록된 번호만 허용됩니다. (해외문자 제외)<br>예) 0212345678 |
| O         | text   | 문자내용 |
|           | type   | CTA(친구톡), ATA(알림톡), SMS(90바이트), LMS(장문 2,000바이트), MMS(장문+이미지)<br>미입력시 SMS<br>해외문자인 경우 SMS만 가능 |
|           | image_id | 발송할 이미지의 아이디<br>type이 MMS일 때 필수 |
|           | refname | 참조내용(이름) |
|           | country | 한국: 82, 일본: 81, 중국: 86, 미국: 1, 기타 등등 (기본 한국)<br>http://countrycode.org 참고 |
|           | datetime | 예약시간을 YYYYMMDDHHMISS 포맷으로 입력 (입력 없거나 지난날짜를 입력하면 바로 전송)<br>예) 20131216090510 (2013년 12월 16일 9시 5분 10초에 발송되도록 예약) |
|           | subject | LMS, MMS 일때 제목 (40바이트) |
|           | template_code | 알림톡 Template Code |
|           | sender_key | 알림톡 Sender Key |

## 제한 사항

to 필드의 전화번호 수는 최대 1,000개이며 넘을 경우 오류를 발생 (RecipientsTooMany)

한번의 Request의 총 데이터 크기는 2MB를 넘을 수 없습니다 (HTTP ERROR 413 발생)

## 발송형태별 제한사항

이동통신사 내부적으로 완성형한글로 변환되므로 영어 1바이트, 한글 2바이트로 취급됩니다.


| 구분 | 제한사항 |
| --- | ------ |
| SMS | 90바이트 까지 전송가능 (한글 45자) |
| LMS | 2,000바이트 까지 전송가능 (한글 1,000자) |
| MMS | 2,000바이트 텍스트 (한글 1,000자)<br>1개의 이미지 전송 (300KB. 2048x2048픽셀 이하인 JPEG, PNG, GIF 형식 파일) |
| ATA | 카카오톡 알림톡으로 1,000자까지 발송<br>이미지 첨부 불가 |

## Response

JSON 포맷으로 리턴 됩니다.

| Mandatory | Field | Description |
| --------- | ----- | ----------- |
| O         | success_count | 접수 성공 갯수 |
| O         | error_count   | 접수 오류 갯수 |
|           | error_list    | 오류 발생 문자메시지 아이디 목록<br>["{인덱스}": "{오류코드}", ...] 형식<br>인덱스값은 0부터 시작 |

## Request Syntax

```
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
```
 
## Response Syntax

```
{
  "Count": Numeric,
  "ResultList": [
    {
      "Code": String,
      "Message": String
    }
  ]
}
```


## Sameple Request

```
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
 ```

## Sample Response

```
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
```

추가하신 메시지의 전체 개수가 success_count로 리턴되면 정상적으로 서버에 접수 완료된 것이며, 에러가 발생한 메시지는 error count 와 error_list 가 리턴됩니다.  
리턴된 error_code의 정보는 http://www.coolsms.co.kr/Legacy_Result_Codes 을 참고하시면 됩니다. 여기서 리턴되는 Response의 내용은 서버에 전송 요청한 것에 대한 정보이며 실제 휴대전화로 전송한 것에 대한 정보가 아닙니다.  sent 조회로 실제 전송된 결과를 확인하실 수 있습니다.


