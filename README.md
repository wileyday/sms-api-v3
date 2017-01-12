<div class="section">

# Overview

<span style="letter-spacing: 0.05em; line-height: 2.1;">이 문서는 REST기반의 문자메시지 API로 </span><span style="font-size: 12px; letter-spacing: 0.05em; line-height: 2.1;">예약 문자를 포함한 문자전송, 전송된 문자의 상태 확인, 잔액정보 및 예약취소 등의 작업을 요청하는 방법을 기술하고 있습니다. </span><span style="font-size: 12px; letter-spacing: 0.05em; line-height: 2.1;">PHP, Java, Python 등 다양한 언어로 구현된 샘플을</span> [SDK](http://www.coolsms.co.kr/SDK_ko)<span style="font-size: 12px; letter-spacing: 0.05em; line-height: 2.1;"> 페이지에서 제공하고 있습니다..</span>

모든 Request 호출에는 API Key를 비롯한 인증정보를 포함하여 서버의 인증을 거쳐야 합니다. 인증에 대한 상세한 내용은 [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 을 확인하세요.

인증을 위한 API Key 및 API Secret 코드는 [문자메시지 > 환경설정 > API Key 관리](http://www.coolsms.co.kr/index.php?mid=service_setup&act=dispSmsconfigCredentials) 메뉴에서 발급 및 관리가 가능합니다. [API Key 관리](http://www.coolsms.co.kr/Man_Credentials) 문서를 참고하세요.

<span style="line-height: 1.5;">아래는 각 Resource의 역할을 테이블로 정리하였습니다. 상세한 설명을 보시려면 해당 Resource를 클릭하여 주세요.</span>

<table>

<tbody>

<tr>

<th>Part</th>

<th>Resource</th>

<th>Description</th>

</tr>

<tr>

<td rowspan="9">그룹메시지</td>

<td>[GET new_group](#GETnew_group)</td>

<td>그룹 생성</td>

</tr>

<tr>

<td>[GET group_list](#GETgroup_list)</td>

<td>그룹 목록</td>

</tr>

<tr>

<td>[POST delete_groups](#POSTdelete_groups)</td>

<td>그룹 삭제</td>

</tr>

<tr>

<td>[GET groups/{group_id}](#GETgroupsgroup_id)</td>

<td>그룹 정보 리턴</td>

</tr>

<tr>

<td>[POST groups/{group_id}/add_messages](#POSTgroupsgroup_idadd_messages)</td>

<td>메시지 추가</td>

</tr>

<tr>

<td>[POST groups/{group_id}/add_messages.json](#POSTgroupsgroup_idadd_messagesjson)</td>

<td>JSON형식으로  메시지 추가</td>

</tr>

<tr>

<td>[GET groups/{group_id}/message_list](#GETgroupsgroup_idmessage_list)</td>

<td>추가된 메시지 목록</td>

</tr>

<tr>

<td>[GET groups/{group_id}/delete_messages](#POSTgroupsgroup_iddelete_messages)</td>

<td>메시지 삭제</td>

</tr>

<tr>

<td>[POST groups/{group_id}/send](#POSTgroupsgroup_idsend)</td>

<td>메시지 발송</td>

</tr>

<tr>

<td rowspan="4">이미지</td>

<td>[POST upload_image](#POSTupload_image)</td>

<td>이미지 업로드</td>

</tr>

<tr>

<td>[GET image_list](#GETimage_list)</td>

<td>이미지 목록</td>

</tr>

<tr>

<td>[GET images/{image_id}](#GETimagesimage_id)</td>

<td>이미지 정보</td>

</tr>

<tr>

<td>[POST delete_images](#POSTdelete_images)</td>

<td>이미지 </td>

</tr>

<tr>

<td rowspan="5">기타</td>

<td>[POST send](#POSTsend)</td>

<td>문자발송 요청</td>

</tr>

<tr>

<td>[GET sent](#GETsent)</td>

<td>발송된 문자정보 조회</td>

</tr>

<tr>

<td>[POST cancel](#POSTcancel)</td>

<td>예약문자 취소</td>

</tr>

<tr>

<td>[GET balance](#GETbalance)</td>

<td>전액정보 조회</td>

</tr>

<tr>

<td>[GET status](#GETstatus)</td>

<td>전송채널 상태 조회</td>

</tr>

</tbody>

</table>

요청에 대한 응답의 상세는 [Response](http://www.coolsms.co.kr/REST_API#Response) 를 확인하세요.

<span style="letter-spacing: 0.05em; line-height: 2.1;">REST API 관련 질의 응답 및 정보 공유는</span> [개발자포럼](http://www.coolsms.co.kr/devforum)<span style="letter-spacing: 0.05em; line-height: 2.1;">을 이용해주세요.</span>

</div>

<div class="section">

# Change Log

<table>

<tbody>

<tr>

<th>Version</th>

<th>Description</th>

</tr>

<tr>

<td>1.1</td>

<td>

Android 누리고 푸시 지원  
1만건 전송을 40초 이하로 단축

후불제 회원 지원

</td>

</tr>

<tr>

<td>1.2</td>

<td>iOS 누리고 푸시 지원  
1만건 전송을 20초 이하로 단축</td>

</tr>

<tr>

<td>1.3</td>

<td>쿨서포터즈 정책 지원 반영</td>

</tr>

<tr>

<td>1.4</td>

<td>status 리소스에 시간별, 일별 전송현황을 위한 date, unit 필드 추가</td>

</tr>

<tr>

<td>1.5</td>

<td>Agent 정보 전송</td>

</tr>

<tr>

<td>1.6</td>

<td>카카오 알림톡 기능 추가</td>

</tr>

<tr>

<td>2.0</td>

<td>그룹 메시징 추가</td>

</tr>

<tr>

<td>3.0</td>

<td>

Full JSON 지원

유니코드 단일 지원

</td>

</tr>

</tbody>

</table>

</div>

<div class="section">

# 그룹메시지

대용량의 메시지를 안전하고 빠르게 전송하도록 그룹메시지를 위한 API를 제공합니다.  
아래의 API 호출 흐름으로 대량의 그룹메시지를 보낼 수 있습니다.

<pre class="prettyprint">new_group  ->  add_messages  ->  send</pre>

<span style="font-size: 12px; letter-spacing: 0.6px; line-height: 28px; background-color: rgb(255, 255, 255);">new_group 호출로 메시지를 담을 그룹을 생성하고 리턴된 그룹아이디를 키로 add_messages 호출로 메시지를 접수하고 send 호출로 접수된 메시지를 서버단에 전송을 수행합니다. 이로 인해 한번 접수된 메시지는 유실 없이 안정적으로 발송이 보장됩니다.</span><span style="font-size: 12px; letter-spacing: 0.05em; line-height: 2.1;"> </span>

</div>

<div class="section">

## GET new_group

메시지를 담을 그룹을 생성하여 그룹아이디를 리턴합니다.

<div style="letter-spacing: 0.6px; line-height: 22.9091px;">

### Resource URL

https://coolsms.co.kr/sms/3/new_group

### Parameters

<table>

<thead>

<tr>

<th style="width: 64px;">Mandatory</th>

<th style="width: 162px;">Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td style="width: 64px;">Ο</td>

<td style="width: 162px;">인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

<tr>

<td style="width: 198px;">srk</td>

<td>솔루션 제공 수수료를 정산받을 솔루션 등록키  
자세한 안내는 http://www.coolsms.co.kr/sp 을 참고하세요.</td>

</tr>

<tr>

<td style="width: 198px;">mode (현재 미지원)</td>

<td>

test로 입력할 경우 CARRIER 시뮬레이터로 시뮬레이션됩니다.

** 수신번호를 반드시 01000000000 으로 테스트 **  
예약필드 datetime는 무시됩니다.

결과값은 60 잔액에서 실제 차감되며 다음날 새벽에 재충전됩니다.

</td>

</tr>

<tr>

<td style="width: 198px;">force_sms<span style="font-family: &quot;Nanum Gothic&quot;; letter-spacing: 0.6px; line-height: 22.9091px; background-color: rgb(255, 255, 255);"> (현재 미지원)</span></td>

<td>

누리고푸시를 사용하더라도 강제로 문자 발송.

true 혹은 false(기본)

</td>

</tr>

<tr>

<td style="width: 198px;">only_ata</td>

<td>알림톡이 실패해도 문자메시지로 대체하여 발송하지 않습니다.  
true 혹은 false(기본)</td>

</tr>

<tr>

<td style="width: 198px;">site_user</td>

<td>

API를 호출하는 사이트에서 관리하는 유저 아이디 입력.

미입력시 __private__ 으로 입력됩니다.  
해당 아이디 앞으로 등록된 발신번호를 확인합니다.  
발신번호 등록 API를 참고하세요.  
http://www.coolsms.co.kr/SenderID_API

</td>

</tr>

<tr>

<td style="width: 198px;">os_platform</td>

<td>

클라이언트의 OS 및 플랫폼 버전

예) CentOS 6.6

(v1.5에서 추가됨)

</td>

</tr>

<tr>

<td style="width: 198px;">dev_lang</td>

<td>

개발 프로그래밍 언어

예) PHP 5.3.3

(v1.5에서 추가됨)

</td>

</tr>

<tr>

<td style="width: 198px;">sdk_version</td>

<td>

SDK 버전

예) PHP SDK 1.5

(v1.5에서 추가됨)

</td>

</tr>

<tr>

<td style="width: 198px;">app_version</td>

<td>

어플리케이션 버전

예) Purplebook 4.1

(v1.5에서 추가됨)

</td>

</tr>

</tbody>

</table>

### Response

JSON 포맷으로 리턴 됩니다.

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>group_id</td>

<td>그룹 아이디</td>

</tr>

</tbody>

</table>

### Example Request

<pre class="lang:xhtml decode:true">curl -XGET 'https://api.coolsms.co.kr/sms/2/new_group?api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125'</pre>

### Example Response

<pre class="lang:default decode:true crayon-selected">{
  "group_id":"565ba3d7d216a"
}</pre>

</div>

</div>

<div class="section">

## GET group_list

<span style="background-color: rgb(255, 255, 255);">생성된 그룹 목록을 리턴합니다.</span>

<div style="letter-spacing: 0.6px; line-height: 22.9091px;">

### Resource URL

https://api.coolsms.co.kr/sms/2/group_list

### Parameters

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

</tbody>

</table>

### Response

JSON 포맷으로 리턴 됩니다.

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>-</td>

<td>array 형식의 그룹아이디 목록 리턴</td>

</tr>

</tbody>

</table>

### Example Request

<pre class="lang:xhtml decode:true">curl -XGET 'https://api.coolsms.co.kr/sms/2/group_list?api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125'</pre>

### Example Response

<pre class="lang:default decode:true crayon-selected">[
    <span class="s1">"565ba3d7d216a",
    "565ba3dea161b"</span>
]
</pre>

</div>

</div>

<div class="section">

## POST delete_groups

<span style="background-color: rgb(255, 255, 255);">그룹을 삭제합니다. 담겨 있는 메시지도 함께 삭제됩니다.</span>

<div style="letter-spacing: 0.6px; line-height: 22.9091px;">

### Resource URL

https://api.coolsms.co.kr/sms/2/delete_groups

### Parameters

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

<tr>

<td>O</td>

<td>group_ids</td>

<td>

삭제할 그룹 아이디

콤마(,)로 구분된 아이디 목록 입력 가능

</td>

</tr>

</tbody>

</table>

### Response

JSON 포맷으로 리턴 됩니다.

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>success_count</td>

<td>삭제된 그룹 갯수</td>

</tr>

<tr>

<td>O</td>

<td>error_count</td>

<td>오류 처리된 그룹 갯수</td>

</tr>

<tr>

<td>O</td>

<td>error_list</td>

<td>오류 내역  
["{인덱스}": "{오류코드}", ...] 형식</td>

</tr>

</tbody>

</table>

### Example Request

<pre class="lang:xhtml decode:true">curl -XPOST 'https://api.coolsms.co.kr/sms/2/delete_groups' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&group_ids=565ba3d7d216a'</pre>

### Example Response

<pre class="lang:default decode:true crayon-selected">{
  "success_count": 3,
  "error_count": 2,
  "error_list": [
    4: "62",
    5: "54"
  ]
}</pre>

</div>

</div>

<div class="section">

## GET groups/{group_id}

<span style="background-color: rgb(255, 255, 255);">그룹 정보를 리턴합니다.</span>

<div style="letter-spacing: 0.6px; line-height: 22.9091px;">

### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group_id}](https://api.coolsms.co.kr/sms/2/groups/{group_id})

### Parameters

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

<tr>

<td>O</td>

<td>group_id</td>

<td>그룹 아이디</td>

</tr>

</tbody>

</table>

### Response

JSON 포맷으로 리턴 됩니다.

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>group_id</td>

<td>그룹 아이디</td>

</tr>

<tr>

<td>O</td>

<td>message_count</td>

<td>그룹에 담긴 메시지 갯수</td>

</tr>

</tbody>

</table>

### Example Request

<pre class="lang:xhtml decode:true">curl -XGET 'https://api.coolsms.co.kr/sms/2/groups/{group_id}' -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&group_id=565ba3d7d216a'</pre>

### Example Response

<pre class="lang:default decode:true crayon-selected">{
  "group_id":"565ba3d7d216a",
  "message_count":970
}</pre>

</div>

</div>

<div class="section" style="letter-spacing: 0.6px; line-height: 22.9091px;">

## POST groups/{group_id}/add_messages

그룹에 발송할 문자메시지를 추가합니다.

### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group_id}/add_messages](https://api.coolsms.co.kr/sms/2/groups/{group_id}/add_messages)

### Parameters

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

<tr>

<td>O</td>

<td>to</td>

<td>수신번호 입력  
콤마(,)로 구분된 수신번호 입력가능  
예) 01012345678,01023456789,01034567890</td>

</tr>

<tr>

<td>O</td>

<td>from</td>

<td>

발신번호 입력  
2015/10/16 발신번호 사전등록제에 의해 반드시 등록된 번호만 허용됩니다. (해외문자 제외)  
<span style="font-family: 'Nanum Gothic'; letter-spacing: 0.6px; line-height: 22.9091px; background-color: rgb(255, 255, 255);">예) 0212345678</span>

</td>

</tr>

<tr>

<td>O</td>

<td>text</td>

<td>문자내용</td>

</tr>

<tr>

<td>type</td>

<td>CTA(친구톡), ATA(알림톡), SMS(90바이트), LMS(장문 2,000바이트), MMS(장문+이미지)  
미입력시 SMS  
해외문자인 경우 SMS만 가능</td>

</tr>

<tr>

<td>image_id</td>

<td>

발송할 이미지의 아이디

type이 MMS일 때 필수

</td>

</tr>

<tr>

<td>refname</td>

<td>참조내용(이름)</td>

</tr>

<tr>

<td>country</td>

<td>

<span style="line-height: 2.1; letter-spacing: 0.05em;">한국: 82, 일본: 81, 중국: 86, 미국: 1, 기타 등등 (기본 한국)</span>

http://countrycode.org 참고

</td>

</tr>

<tr>

<td>datetime</td>

<td>예약시간을 YYYYMMDDHHMISS 포맷으로 입력 (입력 없거나 지난날짜를 입력하면 바로 전송)  
예) 20131216090510 (2013년 12월 16일 9시 5분 10초에 발송되도록 예약)</td>

</tr>

<tr>

<td>subject</td>

<td>LMS, MMS 일때 제목 (40바이트)</td>

</tr>

<tr>

<td>template_code</td>

<td>알림톡 Template Code</td>

</tr>

<tr>

<td>sender_key</td>

<td>알림톡 Sender Key</td>

</tr>

</tbody>

</table>

#### 제한 사항

<span style="letter-spacing: 0.6px; line-height: 22.9091px;">to 필드의 전화번호 수는 최대 1,000개이며 넘을 경우 오류를 발생 (RecipientsTooMany)</span>

한번의 Request의 총 데이터 크기는 2MB를 넘을 수 없습니다 (HTTP ERROR 413 발생)

#### 발송형태별 제한사항

이동통신사 내부적으로 완성형한글로 변환되므로 영어 1바이트, 한글 2바이트로 취급됩니다.

<table>

<tbody>

<tr>

<th>구분</th>

<th>제한사항</th>

</tr>

<tr>

<td>SMS</td>

<td>90바이트 까지 전송가능 (한글 45자)</td>

</tr>

<tr>

<td>LMS</td>

<td>2,000바이트 까지 전송가능 (한글 1,000자)</td>

</tr>

<tr>

<td>MMS</td>

<td>

2,000바이트 텍스트 (한글 1,000자)

1개의 이미지 전송 (300KB. 2048x2048픽셀 이하인 JPEG, PNG, GIF 형식 파일)

</td>

</tr>

<tr>

<td>ATA</td>

<td>카카오톡 알림톡으로 1,000자까지 발송  
이미지 첨부 불가</td>

</tr>

</tbody>

</table>

### Response

JSON 포맷으로 리턴 됩니다.

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>success_count</td>

<td>접수 성공 갯수</td>

</tr>

<tr>

<td>O</td>

<td>error_count</td>

<td>접수 오류 갯수</td>

</tr>

<tr>

<td>error_list</td>

<td>

오류 발생 문자메시지 아이디 목록  
["{인덱스}": "{오류코드}", ...] 형식  
인덱스값은 0부터 시작

</td>

</tr>

</tbody>

</table>

### Example Request

<pre class="lang:xhtml decode:true">curl -XPOST https://api.coolsms.co.kr/sms/2/groups/GID<span class="s1">565bA3D7D216A</span>/add_messages -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&to=01012345678&from=029302266&text=Hello'
</pre>

### Example Response

<pre class="lang:default decode:true">{
  "success_count": 3,
  "error_count": 2,
  "error_list": [
    0: "62",
    4: "54"
  ]
}</pre>

추가하신 메시지의 전체 개수가 success_count로 리턴되면 정상적으로 서버에 접수 완료된 것이며, 에러가 발생한 메시지는 error count 와 error_list 가 리턴됩니다.  
리턴된 error_code의 정보는 http://www.coolsms.co.kr/Legacy_Result_Codes 을 참고하시면 됩니다. 여기서 리턴되는 Response의 내용은 서버에 전송 요청한 것에 대한 정보이며 실제 휴대전화로 전송한 것에 대한 정보가 아닙니다.  sent 조회로 실제 전송된 결과를 확인하실 수 있습니다.

</div>

<div class="section">

## POST groups/{group_id}/add_messages.json

그룹에 발송할 문자메시지를 JSON 형식으로 접수합니다. 대량의 문자를 각각 다른 내용과 타입으로 보내고 싶을 때 용이 합니다.

### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group_id}/add_messages.json](https://api.coolsms.co.kr/sms/2/groups/{group_id}/add_messages.json)

### Parameters

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

<tr>

<td>O</td>

<td>messages</td>

<td>

JSON 형식의 메시지 데이터

</td>

</tr>

</tbody>

</table>

#### JSON Fields

<div>

<table style="width: 642px; letter-spacing: 0.6px; line-height: 22.9091px;">

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>to</td>

<td>수신번호 입력  
콤마(,)로 구분된 수신번호 입력가능  
예) 01012345678,01023456789,01034567890</td>

</tr>

<tr>

<td>O</td>

<td>from</td>

<td>

발신번호 입력  
2015/10/16 발신번호 사전등록제에 의해 반드시 등록된 번호만 허용됩니다. (해외문자 제외)  
<span style="letter-spacing: 0.6px; line-height: 22.9091px; background-color: rgb(255, 255, 255);">예) 0212345678</span>

</td>

</tr>

<tr>

<td>O</td>

<td>text</td>

<td>문자내용</td>

</tr>

<tr>

<td>type</td>

<td>ATA(알림톡), SMS(90바이트), LMS(장문 2,000바이트), MMS(장문+이미지)  
미입력시 SMS  
해외문자인 경우 SMS만 가능</td>

</tr>

<tr>

<td>image_id</td>

<td>

발송할 이미지의 아이디

type이 MMS일 때 필수

</td>

</tr>

<tr>

<td>refname</td>

<td>참조내용(이름)</td>

</tr>

<tr>

<td>country</td>

<td>

<span style="line-height: 2.1; letter-spacing: 0.05em;">한국: 82, 일본: 81, 중국: 86, 미국: 1, 기타 등등 (기본 한국)</span>

http://countrycode.org 참고

</td>

</tr>

<tr>

<td>datetime</td>

<td>예약시간을 YYYYMMDDHHMISS 포맷으로 입력 (입력 없거나 지난날짜를 입력하면 바로 전송)  
예) 20131216090510 (2013년 12월 16일 9시 5분 10초에 발송되도록 예약)</td>

</tr>

<tr>

<td>subject</td>

<td>LMS, MMS 일때 제목 (40바이트)</td>

</tr>

<tr>

<td>template_code</td>

<td><span style="font-family: &quot;Nanum Gothic&quot;; letter-spacing: 0.6px; line-height: 22.9091px; background-color: rgb(255, 255, 255);">알림톡 Template Code</span></td>

</tr>

<tr>

<td>sender_key</td>

<td>알림톡 Sender Key</td>

</tr>

</tbody>

</table>

</div>

### messages 포맷

[ ] 안에 { } 가 여러 개 들어 갈 수 있는 구조로 되어있으며 각각의 { } 안에는 to, from, text 필드가 필수요소입니다.

<pre class="lang:default decode:true" style="font-size: 12px; letter-spacing: 0.6px; line-height: 28px;">[
  {
    "type": "SMS",
    "to": "01000000000,01011111111,01022222222",
    "from": "021234567",
    "text": "Hello A"
  },
  {
    "type": "LMS",
    "to": "01000000000,01011111111,01022222222",
    "from": "021234567",
    "text": "Hello B"
    "subject": "LMS Subject",
  },
  {
    "type": "MMS",
    "to": "01000000000,01011111111,01022222222",
    "from": "021234567",
    "text": "Hello C",
    "subject": "MMS Subject",
    "image_id": "abcdefg"
  }
]
</pre>

#### <span style="letter-spacing: 0.6px; line-height: 22.9091px;">제한 사항</span>

<span style="letter-spacing: 0.6px; line-height: 22.9091px;">수신받을 전화번호 총 수(to 필드 전화번호 합계)는 최대 1,000개이며 넘을 경우 오류 발생. (RecipientsTooMany)</span>

한번의 Request의 총 데이터 크기는 2MB를 넘을 수 없습니다 (HTTP ERROR 413 발생)

#### 발송형태에 따른 제한사항

이동통신사 내부적으로 완성형한글로 변환되므로 영어 1바이트, 한글 2바이트로 취급됩니다.

<table>

<tbody>

<tr>

<th>구분</th>

<th>제한사항</th>

</tr>

<tr>

<td>SMS</td>

<td>90바이트 까지 전송가능 (한글 45자)</td>

</tr>

<tr>

<td>LMS</td>

<td>2,000바이트 까지 전송가능 (한글 1,000자)</td>

</tr>

<tr>

<td>MMS</td>

<td>

2,000바이트 텍스트 (한글 1,000자)  
1개의 이미지 전송 (300KB. 2048x2048픽셀 이하인 JPEG, PNG, GIF 형식 파일)

</td>

</tr>

<tr>

<td>ATA</td>

<td>카카오톡 알림톡으로 1,000자까지 발송  
이미지 첨부 불가</td>

</tr>

</tbody>

</table>

### Response

JSON 포맷으로 리턴 됩니다.

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>success_count</td>

<td>접수 성공 갯수</td>

</tr>

<tr>

<td>O</td>

<td>error_count</td>

<td>접수 오류 갯수</td>

</tr>

<tr>

<td>error_list</td>

<td>오류 발생 문자메시지 아이디 목록  
["{인덱스}": "{오류코드}", ...] 형식  
인덱스값은 0부터 시작</td>

</tr>

</tbody>

</table>

### Example Request

<pre class="lang:xhtml decode:true" style="font-size: 12px; letter-spacing: 0.6px; line-height: 22.9091px;">curl -XPOST https://api.coolsms.co.kr/sms/2/groups/<span class="s1">565ba3d7d216a</span>/add_messages -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&messages=JSONArray
</pre>

### Example Response

<pre class="lang:default decode:true" style="font-size: 12px; letter-spacing: 0.6px; line-height: 22.9091px;">[
  {
    "success_count": 3,
    "error_count": 0,
  },
  {
    "success_count": 1,
    "error_count": 2,
    "error_list": [
      0: "62",
      1: "54"
    ]
  },
  {
    "success_count": 3,
    "error_count": 0,
  }
]</pre>

추가하신 메시지의 전체 개수가 success_count로 리턴되면 정상적으로 서버에 접수 완료된 것이며, 에러가 발생한 메시지는 error count 와 error_list 가 리턴됩니다.  
리턴된 error_code의 정보는 http://www.coolsms.co.kr/Legacy_Result_Codes 을 참고하시면 됩니다. 여기서 리턴되는 Response의 내용은 서버에 전송 요청한 것에 대한 정보이며 실제 휴대전화로 전송한 것에 대한 정보가 아닙니다.  sent 조회로 실제 전송된 결과를 확인하실 수 있습니다.

</div>

<div class="section" style="letter-spacing: 0.6px; line-height: 22.9091px;">

## GET groups/{group_id}/message_list

문자메시지 목록을 리턴합니다.

### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group_id}/message_list](https://api.coolsms.co.kr/sms/2/groups/{group_id}/message_list)

### Parameters

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

<tr>

<td>offset</td>

<td>

조회할 목록의 시작 위치

Default) 0

</td>

</tr>

<tr>

<td>limit</td>

<td>

가져올 메시지의 갯수

Default) 20

</td>

</tr>

</tbody>

</table>

### Response

JSON 포맷으로 리턴 됩니다.

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>total_count</td>

<td>전체 메시지 갯수</td>

</tr>

<tr>

<td>O</td>

<td>offset</td>

<td>조회 목록의 시작 위치</td>

</tr>

<tr>

<td>O</td>

<td>limit</td>

<td>가져올 메시지의 갯수</td>

</tr>

<tr>

<td>O</td>

<td>list</td>

<td>Array 형식의 메시지 목록</td>

</tr>

</tbody>

</table>

### Example Request

<pre class="lang:xhtml decode:true"><span class="s1">curl -XGET 'https://api.coolsms.co.kr/sms/2/groups/{group_id}/message_list' -d 'api_key=</span>NCS52A57F48C3D32<span class="s1">&</span>signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125<span class="s1">'</span></pre>

### Example Response

<pre class="lang:default decode:true">{
  "total_count":2,
  "offset":0,
  "limit":20,
  "list":[
     "565ba4e7d316b",
     "565ab383dabcd"
  ]
}</pre>

</div>

<div class="section" style="letter-spacing: 0.6px; line-height: 22.9091px;">

## POST groups/{group_id}/delete_messages

그룹에 추가된 메시지를 삭제합니다.

### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group_id}/delete_messages](https://api.coolsms.co.kr/sms/2/groups/{group_id}/delete_messages)

### Parameters

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

<tr>

<td>O</td>

<td>message_ids</td>

<td>

콤마로 구분된 삭제할 메시지 아이디 목록

ex) MID565BA6D7E325C,MID565433E7D233A

</td>

</tr>

</tbody>

</table>

### Response

JSON 포맷으로 리턴 됩니다.

<table style="width: 642px; letter-spacing: 0.6px; line-height: 25.2px;">

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>success_count</td>

<td>삭제 성공 갯수</td>

</tr>

<tr>

<td>O</td>

<td>error_count</td>

<td> 오류 갯수</td>

</tr>

<tr>

<td>error_list</td>

<td>오류 발생 코드 목록  
["{인덱스}": "{오류코드}", ...] 형식  
인덱스값은 0부터 시작</td>

</tr>

</tbody>

</table>

### <span style="letter-spacing: 0.6px; line-height: 22.9091px;">Example Request</span>

<pre class="lang:xhtml decode:true"><span class="s1">curl -XPOST 'https://api.coolsms.co.kr/sms/2/groups/{group_id}/delete_messages' -d 'api_key=</span>NCS52A57F48C3D32<span class="s1">&</span>signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&message_ids=MID565BA6D7E325C,MID565433E7D233A,MID565643A66AB21<span class="s1">'</span>
</pre>

### Example Response

서버는 json 포맷으로 삭제된 갯수를 리턴합니다.

<pre class="lang:default decode:true">{
  "success_count": 1,
  "error_count": 2,
  "error_list": [
    0: "1021",
    2: "1021"
  ]
}</pre>

</div>

<div class="section">

## POST groups/{group_id}/send

<span style="background-color: rgb(255, 255, 255);">그룹메시지를 전송 요청합니다.</span>

### Resource URL

[https://api.coolsms.co.kr/sms/2/groups/{group_id}/send](https://api.coolsms.co.kr/sms/2/groups/{group_id}/send)

### Parameters

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

</tbody>

</table>

### Response

JSON 포맷으로 리턴 됩니다.

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>group_id</td>

<td>전송 요청된 그룹 아이디</td>

</tr>

</tbody>

</table>

### Example Request

<pre class="lang:xhtml decode:true" style="font-size: 12px; letter-spacing: 0.6px; line-height: 22.9091px;"><span class="s1">curl -XPOST 'https://api.coolsms.co.kr/sms/2/groups/{group_id}/send' -d 'api_key=</span>NCS52A57F48C3D32<span class="s1">&</span>signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125<span class="s1">'</span></pre>

### Example Response

<pre class="lang:default decode:true" style="font-size: 12px; letter-spacing: 0.6px; line-height: 28px;">{
  "group_id": "565ba3d7d216a"
}</pre>

</div>

<div class="section">

# 이미지

이미지를 서버에 안전하게 미리 업로드하여 문자발송 때 사용할 수 있어 더욱 안정적인 발송을 보장합니다.

</div>

<div class="section">

## POST upload_image

MMS 발송에 필요한 이미지 파일을 업로드 합니다.

MMS 발송 때 미리 업로드 된 이미지 파일을 사용하므로 발송과정에서 발생하는 오류률 현저히 줄어듭니다.

이미지 보관 기간은 7일입니다.

### Resource URL

https://api.coolsms.co.kr/sms/2/upload_image

### Parameters

<table style="width: 642px; letter-spacing: 0.6px; line-height: 25.2px;">

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

<tr>

<td>O</td>

<td>image</td>

<td>

이미지 내용 (파일명이 아니라 내용입니다.)  
Form Submit 옵션 : method=POST enc-type=multipart/form  
제한사항) 300KB, 2048x2048 이하, JPEG, PNG, GIF

</td>

</tr>

<tr>

<td>image_encoding</td>

<td>

이미지 인코딩 방식 binary(Default), base64

</td>

</tr>

</tbody>

</table>

### Response

JSON 포맷으로 리턴 됩니다.  
리턴되는 image_id를 MMS 발송 시 {group_id}/add_messages 파라메터로 입력하셔야 합니다.

<table style="width: 642px; letter-spacing: 0.6px; line-height: 25.2px;">

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>image_id</td>

<td>이미지 아이디</td>

</tr>

</tbody>

</table>

### Example Request

<pre class="lang:xhtml decode:true" style="letter-spacing: 0.6px; line-height: 22.9091px;"><span class="s1">curl -XPOST 'https://api.coolsms.co.kr/sms/2/upload_image' -d 'api_key=</span>NCS52A57F48C3D32<span class="s1">&</span>signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125<span class="s1">'</span> -F 'image=@/path/to/my/file'</pre>

### Example Response

<pre class="lang:default decode:true" style="letter-spacing: 0.6px; line-height: 22.9091px;">{
  "image_id": IMG565BA2D9E4239"
}</pre>

</div>

<div class="section">

## GET image_list

서버에 업로드 되어 있는 이미지 목록을 리턴합니다.

### Resource URL

https://api.coolsms.co.kr/sms/2/image_list

### Parameters

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

<tr>

<td>offset</td>

<td>조회할 목록의 시작 위치  
Default) 0</td>

</tr>

<tr>

<td>limit</td>

<td>가져올 이미지 아이디의 갯수  
Default) 20</td>

</tr>

</tbody>

</table>

### Response

JSON 포맷으로 리턴 됩니다.

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>total_count</td>

<td>전체 메시지 갯수</td>

</tr>

<tr>

<td>O</td>

<td>offset</td>

<td>조회 목록의 시작 위치</td>

</tr>

<tr>

<td>O</td>

<td>limit</td>

<td>가져올 이미지 아이디의 갯수</td>

</tr>

<tr>

<td>O</td>

<td>list</td>

<td>Array 형식의 이미지 아이디 목록</td>

</tr>

</tbody>

</table>

### Example Request

<pre class="lang:xhtml decode:true" style="letter-spacing: 0.6px; line-height: 22.9091px;"><span class="s1">curl -XGET 'https://api.coolsms.co.kr/sms/2/image_list' -d 'api_key=</span>NCS52A57F48C3D32<span class="s1">&</span>signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125<span class="s1">'</span></pre>

### Example Response

<pre class="lang:default decode:true" style="letter-spacing: 0.6px; line-height: 22.9091px;">{
  "total_count":3,
  "offset":0,
  "limit":20,
  "list":[
    "IMG565BA6D7D327C",
    "IMG565BA7ABD338B",
    "IMG565BB9D7D21C7"
  ]
}</pre>

</div>

<div class="section">

## GET images/{image_id}

업로드된 이미지 정보를 리턴합니다.

### Resource URL

[https://api.coolsms.co.kr/sms/2/images/{image_id}](https://api.coolsms.co.kr/sms/2/images/{image_id})

### Parameters

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

</tbody>

</table>

### Response

해당 이미지의 정보가 JSON 포맷으로 리턴 됩니다.

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>image_id</td>

<td>이미지 아이디</td>

</tr>

<tr>

<td>O</td>

<td>file_name</td>

<td>파일 명</td>

</tr>

<tr>

<td>O</td>

<td>original_name</td>

<td>원본 파일 명</td>

</tr>

<tr>

<td>O</td>

<td>file_size</td>

<td>파일 크기 (Byte 단위)</td>

</tr>

<tr>

<td>O</td>

<td>width</td>

<td>이미지 가로 픽셀</td>

</tr>

<tr>

<td>O</td>

<td>height</td>

<td>이미지 세로 픽셀</td>

</tr>

</tbody>

</table>

### Example Request

<pre class="lang:xhtml decode:true" style="letter-spacing: 0.6px; line-height: 22.9091px;"><span class="s1">curl -XGET 'https://api.coolsms.co.kr/sms/2/images/{image_id}' -d 'api_key=</span>NCS52A57F48C3D32<span class="s1">&</span>signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125<span class="s1">'</span></pre>

### Example Response

<pre class="lang:default decode:true" style="letter-spacing: 0.6px; line-height: 22.9091px;">{
  "image_id":"566fb2266316f",
  "file_name","566fb2266316f.jpg",
  "original_name":"nurigo-200x100.jpg",
  "file_size":"4990",
  "width":"200",
  "height":"100"
}</pre>

</div>

<div class="section">

## POST delete_images

이미지 파일을 삭제합니다.

### Resource URL

https://api.coolsms.co.kr/sms/2/delete_images

### Parameters

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

<tr>

<td>O</td>

<td>image_ids</td>

<td>

콤마로 구분된 삭제 할 이미지 ID 목록  
예) IMG565BA6D7E325C,IMG565433E7D233A

</td>

</tr>

</tbody>

</table>

### Response

JSON 포맷으로 리턴 됩니다.

<table style="width: 642px; letter-spacing: 0.6px; line-height: 25.2px;">

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>success_count</td>

<td>삭제 성공 갯수</td>

</tr>

<tr>

<td>O</td>

<td>error_count</td>

<td>삭제 오류 갯수</td>

</tr>

<tr>

<td>error_list</td>

<td>오류 발생 문자메시지 아이디 목록  
["{인덱스}": "{오류코드}", ...] 형식  
인덱스값은 0부터 시작</td>

</tr>

</tbody>

</table>

### Example Request

<pre class="lang:xhtml decode:true" style="letter-spacing: 0.6px; line-height: 22.9091px;"><span class="s1">curl -XPOST 'https://api.coolsms.co.kr/sms/2/delete_images' -d 'api_key=</span>NCS52A57F48C3D32<span class="s1">&</span>signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125<span class="s1">&image_ids=IMG</span>565BA2D9E4239,IMG565AB2E4A5134,IMG565BB3A4B4342<span class="s1">'</span></pre>

### Example Response

<pre class="lang:default decode:true" style="letter-spacing: 0.6px; line-height: 22.9091px;">{
  "success_count": 1,
  "error_count": 2,
  "error_list": [
    0: "1023",
    2: "1024"
  ]
}</pre>

</div>

<div class="section">

# POST send

<span style="background-color: rgb(255, 255, 255);">문자메시지를 전송 요청합니다. 전송 요청에 대한 Response</span>는 휴대전화까지 전송된 결과가 아닙니다.

## Resource URL

https://api.coolsms.co.kr/sms/2/send

## Parameters

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

<tr>

<td>O</td>

<td>to</td>

<td>수신번호 입력 콤마(,)로 구분된 수신번호 입력가능 예) 01012345678,01023456789,01034567890</td>

</tr>

<tr>

<td>O</td>

<td>from</td>

<td>

발신번호 예) 0212345678  
2015/10/16 발신번호 사전등록제에 의해 반드시 등록된 번호만 허용됩니다. (해외문자 제외)

</td>

</tr>

<tr>

<td>O</td>

<td>text</td>

<td>문자내용</td>

</tr>

<tr>

<td>type</td>

<td>CTA(친구톡), ATA(알림톡), SMS(80바이트), LMS(장문 2,000바이트), MMS(장문+이미지) 입력 없으면 SMS가 기본 국가코드가 KR이 아니면 SMS로 강제</td>

</tr>

<tr>

<td>template_code</td>

<td>알림톡 Template Code</td>

</tr>

<tr>

<td>sender_key</td>

<td>알림톡 Sender Key</td>

</tr>

<tr>

<td>image</td>

<td>지원형식 : 300KB 이하의 JPEG, PNG, GIF 형식의 파일 2048x2048 픽셀이하</td>

</tr>

<tr>

<td>image_encoding</td>

<td>이미지 인코딩 방식 binary(Default), base64</td>

</tr>

<tr>

<td>refname</td>

<td>참조내용(이름)</td>

</tr>

<tr>

<td>country</td>

<td>

<span style="line-height: 2.1; letter-spacing: 0.05em;">한국: 82, 일본: 81, 중국: 86, 미국: 1, 기타 등등 (기본 한국)</span>

http://countrycode.org 참고

</td>

</tr>

<tr>

<td>datetime</td>

<td>예약시간을 YYYYMMDDHHMISS 포맷으로 입력 (입력 없거나 지난날짜를 입력하면 바로 전송) 예) 20131216090510 (2013년 12월 16일 9시 5분 10초에 발송되도록 예약)</td>

</tr>

<tr>

<td>subject</td>

<td>LMS, MMS 일때 제목 (40바이트)</td>

</tr>

<tr>

<td>charset</td>

<td>한글 인코딩 방식 지정 유니코드 UTF-8 일 경우 utf8 완성형 한글(EUC-KR) 일 경우 euckr 으로 입력 입력 없으면 utf8가 기본</td>

</tr>

<tr>

<td>srk</td>

<td>솔루션 제공 수수료를 정산받을 솔루션 등록키</td>

</tr>

<tr>

<td>mode<span style="font-family: &quot;Nanum Gothic&quot;; letter-spacing: 0.6px; line-height: 22.9091px; background-color: rgb(255, 255, 255);"> (현재 미지원)</span></td>

<td>test로 입력할 경우 CARRIER 시뮬레이터로 시뮬레이션됨 수신번호를 반드시 01000000000 으로 테스트하세요. 예약필드 datetime는 무시됨 결과값은 60 잔액에서 실제 차감되며 다음날 새벽에 재충전됨</td>

</tr>

<tr>

<td>force_sms<span style="font-family: &quot;Nanum Gothic&quot;; letter-spacing: 0.6px; line-height: 22.9091px; background-color: rgb(255, 255, 255);"> (현재 미지원)</span></td>

<td>

누리고푸시를 사용하더라도 SMS로 발송되도록 강제

true 혹은 false(기본)

</td>

</tr>

<tr>

<td>only_ata</td>

<td>

알림톡이 실패해도 문자메시지로 대체하여 발송하지 않습니다.

true 혹은 false(기본)

</td>

</tr>

<tr>

<td>os_platform</td>

<td>

클라이언트의 OS 및 플랫폼 버전) CentOS 6.6

(v1.5에서 추가됨)

</td>

</tr>

<tr>

<td>dev_lang</td>

<td>

개발 프로그래밍 언어 예) PHP 5.3.3

(v1.5에서 추가됨)

</td>

</tr>

<tr>

<td>sdk_version</td>

<td>

SDK 버전 예) PHP SDK 1.5

(v1.5에서 추가됨)

</td>

</tr>

<tr>

<td>app_version</td>

<td>

어플리케이션 버전 예) Purplebook 4.1

(v1.5에서 추가됨)

</td>

</tr>

</tbody>

</table>

Mandatory가 Ο 인 필드는 반드시 입력하여야 합니다.

srk 는 [http://www.coolsms.co.kr/provider](http://www.coolsms.co.kr/provider) 을 참고하세요.

<span style="font-size: 12px; letter-spacing: 0.05em; line-height: 2.1;">한번의 Request에 extension을 포함하여 총 받는사람(to) 수는 1000개 까지가 제한이며 1000개가 넘을 경우 오류를 발생시킵니다. (RecipientsTooMany)</span>

한번의 Request의 총 크기는 2MB를 넘을 수 없습니다. (HTTP ERROR 413 발생)

### 발송형태에 따른 제한사항

이동통신사 내부적으로 완성형한글로 변환되므로 영어 1바이트, 한글 2바이트로 취급됩니다.

<table>

<tbody>

<tr>

<th>구분</th>

<th>제한사항</th>

</tr>

<tr>

<td>SMS</td>

<td>90바이트 까지 전송가능 (한글 45자)</td>

</tr>

<tr>

<td>LMS</td>

<td>2,000바이트 까지 전송가능 (한글 1,000자)</td>

</tr>

<tr>

<td>MMS</td>

<td>

2,000바이트 텍스트(한글 1,000자)

1개의 이미지 전송(300KB 이하의 JPEG, PNG, GIF 형식의 파일 2048x2048 픽셀이하)

</td>

</tr>

<tr>

<td>ATA</td>

<td>

카카오톡 알림톡으로 1,000자까지 발송

이미지 첨부 

</td>

</tr>

</tbody>

</table>

## Response

<table style="width: 642px; letter-spacing: 0.6px; line-height: 25.2px;">

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>group_id</td>

<td>그룹아이디</td>

</tr>

<tr>

<td>O</td>

<td>success_count</td>

<td>성공 건수</td>

</tr>

<tr style="transition: all 0.1s ease-in-out; background: rgb(249, 249, 249);">

<td>O</td>

<td>error_count</td>

<td>오류 건수</td>

</tr>

<tr>

<td>O</td>

<td>result_code</td>

<td>마지막 오류 코드</td>

</tr>

<tr>

<td>O</td>

<td>result_message</td>

<td>마지막 오류 메시지</td>

</tr>

</tbody>

</table>

result_code 가 00 이면 정상적인 접수이며 이 외의 코드는 http://www.coolsms.co.kr/Legacy_Result_Codes 을 참고하세요. 여기서 리턴되는 Response의 내용은 서버에게 전송을 요청한 것에 대한 정보이지 실제 휴대전화로 전송한 것에 대한 정보가 아닙니다. 예를 들어 요청 건수 중 success_count가 10개라면 서버의 DB에 안전하게 INSERT된 건이 10개라는 의미이며, 나중 sent 리소스를 통해 조회시 이통사를 통해 실제 전송성공된 건수는 8개이고 올바르지 못한 수신번호로 2개로 실패라는 결과가 나올 수 있습니다.

메시지그룹ID(group_id)는 Request된 메시지들의대표하는 아이디값으로 메시지상태 및 예약취소할 때 키값으로 사용될 수 있습니다. 10건의 문자메시지를 발송할 경우 그 10건의 문자메시지를 대표하는 group_id 가 리턴되며 sent 리소스를 통해서 10건에 대한 전송상태를 조회할 수 있습니다.

## **Example Request**

<pre class="lang:xhtml decode:true">curl -XPOST https://api.coolsms.co.kr/sms/2/send -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&to=01012345678,01023456789,01034567890&from=029302266&text=Hello'
</pre>

## **Example Response**

서버는 json 포맷으로 접수결과를 리턴합니다.

<pre class="lang:default decode:true">{
  "group_id": "20120217103829612403761364",
  "success_count": 2,
  "error_count": 0,
  "result_code": "00",
  "result_message": "Success"
}</pre>

</div>

<div class="section">

# GET sent

<span style="background-color: rgb(255, 255, 255);">발송된 문자메시지의 목록을 가져옵니다.</span> 

<div>

## Resource URL

https://api.coolsms.co.kr/sms/2/sent

## Parameters

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

<tr>

<td>offset</td>

<td>가져올 목록의 시작 위치</td>

</tr>

<tr>

<td>limit</td>

<td>기본값 20이며 20개의 목록을 받을 수 있음. 40입력시 40개의 목록이 리턴</td>

</tr>

<tr>

<td>rcpt</td>

<td>수신번호로 검색</td>

</tr>

<tr>

<td>start</td>

<td>검색 시작일시 접수 날짜와 시간으로 검색 YYYY-MM-DD HH:MI:SS 포맷의 날짜와 시간</td>

</tr>

<tr>

<td>end</td>

<td>검색 종료일시 접수 날짜와 시간으로 검색 YYYY-MM-DD HH:MI:SS 포맷의 날짜와 시간</td>

</tr>

<tr>

<td>status</td>

<td>메시지 상태 값으로 검색</td>

</tr>

<tr>

<td>resultcode</td>

<td>전송결과 값으로 검색</td>

</tr>

<tr>

<td>notin_resultcode</td>

<td>입력된 전송결과 값 이외의 건들만 조회</td>

</tr>

<tr>

<td>message_id</td>

<td>메시지ID</td>

</tr>

<tr>

<td>group_id</td>

<td> ID</td>

</tr>

</tbody>

</table>

검색 옵션이 없는 경우 가장 최신의 발송건부터 20일 전까지 내림차순으로 페이지 단위의 목록을 리턴합니다.

## Response

JSON 포맷으로 리턴 됩니다.

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>total_count</td>

<td>전체 카운트</td>

</tr>

<tr>

<td>O</td>

<td>list_count</td>

<td>...</td>

</tr>

</tbody>

</table>

## Example Request

<pre class="lang:xhtml decode:true">curl -XGET https://api.coolsms.co.kr/sms/2/sent -d 'api_key=NCS52A57F48C3D32&signature=202b4d499fbd71813c170a415f84097a&timestamp=1456364125&salt=abc&offset=0&limit=20'</pre>

## **Example Response**

Response Format은 json을 사용합니다.

<pre class="lang:default decode:true crayon-selected">{
  "total_count":"169",
  "list_count":4,
  "page":1,
  "data":[
    {
      "type":"SMS",
      "accepted_time":"2014-01-07 18:14:54",
      "recipient_number":"01000000000",
      "group_id":"G52CBC596955F0",
      "message_id":"M52CBC59695B31",
      "status":"2",
      "result_code":"58",
      "result_message":"\uc804\uc1a1\uacbd\ub85c \uc5c6\uc74c",
      "sent_time":"201401071814",
      "text":"Test Message",
      "carrier":"SKT",
      "scheduled_time":"SKT"
    },
    {
      "type":"SMS",
      "accepted_time":"2014-01-07 18:14:41",
      "recipient_number":"01000000000",
      "group_id":"G52CBC5897645A",
      "message_id":"M52CBC58976A64",
      "status":"2",
      "result_code":"58",
      "result_message":"\uc804\uc1a1\uacbd\ub85c \uc5c6\uc74c",
      "sent_time":"201401071814",
      "text":"message\nhere",
      "carrier":"KTF",
      "scheduled_time":"SKT"
    },
    {
      "type":"SMS",
      "accepted_time":"2014-01-07 18:11:23",
      "recipient_number":"01000000000",
      "group_id":"G52CBC4C35B3A8",
      "message_id":"M52CBC4C35BA70",
      "status":"2",
      "result_code":"58",
      "result_message":"\uc804\uc1a1\uacbd\ub85c \uc5c6\uc74c",
      "sent_time":"201401071811",
      "text":"message\nhere",
      "carrier":"LGT",
      "scheduled_time":"SKT"
    },
    {
      "type":"SMS",
      "accepted_time":"2014-01-06 12:42:32",
      "recipient_number":"01012345678",
      "group_id":"G52CA262EC447D",
      "message_id":"M52CA262EC49D8",
      "status":"2",
      "result_code":"00",
      "result_message":"\uc815\uc0c1",
      "sent_time":"201401061257",
      "text":"\ud14c\uc2a4\ud305hi there~",
      "carrier":"KTF",
      "scheduled_time":"SKT"
    }
  ]
}</pre>

### status

<table>

<thead>

<tr>

<th>Status Code</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>0</td>

<td>대기중</td>

</tr>

<tr>

<td>1</td>

<td>이통사로 전송중</td>

</tr>

<tr>

<td>2</td>

<td>이통사로부터 리포트 도착</td>

</tr>

</tbody>

</table>

result_code 는 [http://www.coolsms.co.kr/Legacy_Result_Codes](http://www.coolsms.co.kr/Legacy_Result_Codes) 페이지를 참고 하세요.

</div>

</div>

<div class="section">

# POST cancel

<span style="line-height: 2.1; letter-spacing: 0.05em;">예약된 문자메시지를 취소합니다.</span> 예약되지 않았거나, 예약되었으나 이미 발송된 문자메시지는 취소 할 수 없습니다.

## Resource URL

https://api.coolsms.co.kr/sms/2/cancel

## Parameters

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

<tr>

<td>message_id</td>

<td>메시지ID</td>

</tr>

<tr>

<td>group_id</td>

<td>그룹ID</td>

</tr>

</tbody>

</table>

message_id 혹은 group_id 중 하나는 반드시 입력하세요.

## Response

JSON 포맷으로 리턴 됩니다.

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>total_count</td>

<td>전체 카운트</td>

</tr>

<tr>

<td>O</td>

<td>list_count</td>

<td>...</td>

</tr>

</tbody>

</table>

</div>

<div class="section">

# GET balance

<span style="line-height: 2.1; letter-spacing: 0.05em;">잔액을 확인합니다.</span>

## Resource URL

https://api.coolsms.co.kr/sms/2/balance

## Parameters

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

</tbody>

</table>

## Response

Response Format은 json을 사용합니다.

<pre>{
  "cash": "23900",
  "point": "890"
}</pre>

</div>

<div class="section">

# GET status

<span style="line-height: 2.1; letter-spacing: 0.05em;">전송채널의 상태를 조회합니다.</span>

## Resource URL

https://api.coolsms.co.kr/sms/2/status

## Parameters

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>Ο</td>

<td>인증정보</td>

<td>인증데이터는 필수입니다. [Authentication](http://www.coolsms.co.kr/REST_API#Authentication) 참고</td>

</tr>

<tr>

<td>count</td>

<td>기본값 1이며 1개의 최신의 레코드를 받을 수 있음, 10입력시 10분 동안의 레코드 목록을 리턴</td>

</tr>

<tr>

<td>unit</td>

<td>minute(default), hour, day 중 하나  
minute : 분 단위의 현황  
hour : 시간 단위의 평균  
day : 일 단위의 평균  
(v1.4에서 추가)</td>

</tr>

<tr>

<td>date</td>

<td>

데이터를 읽어오는 기준 시각으로 YYYYMMDDHHMISS 형식의 14자리 값  
예) 20150331095101 (2015년 3월 31일 오전 9시 51분 1초)  
기본값 : <span style="color: rgb(102, 102, 102); line-height: 22.9px; letter-spacing: 0.6px; font-family: &quot;Nanum Gothic&quot;; background-color: rgb(255, 255, 255);">현재시각</span>

(v1.4에서 추가)

</td>

</tr>

<tr>

<td>channel</td>

<td>

1: 1건 발송 채널 (기본 값)

2: 대량 발송 채널  
(v1.4에서 추가)

</td>

</tr>

</tbody>

</table>

<span style="line-height: 1.5;"> </span>

## Response

JSON 포맷으로 리턴 됩니다.

<table>

<thead>

<tr>

<th>Mandatory</th>

<th>Field</th>

<th>Description</th>

</tr>

</thead>

<tbody>

<tr>

<td>O</td>

<td>registdate</td>

<td>입력일</td>

</tr>

<tr>

<td>O</td>

<td>sms_average</td>

<td>...</td>

</tr>

</tbody>

</table>

모든 항목의 값은 초단위(seconds)값입니다. sms_average와 mms_average는 각각 SMS채널과 MMS채널의 문자가 접수된 때부터 실제 수신되기까지 걸린 시간으로 계산된 평균값으로 리포트가 오지않은 대기중인 메시지를 합산한 값이므로 다소 높게 나와도 정상입니다. sk, kt, lg 의 경우 수신시각이 분단위로만 제공되어서 약간의 차이가 날 수 있습니다.

## Response Example

<pre class="lang:default decode:true crayon-selected">[
  {
    "registdate": "2014-02-25 10:34:01",
    "sms_average": "23",
    "sms_sk_average": "9",
    "sms_kt_average": "10",
    "sms_lg_average": "11",
    "mms_average": "52",
    "mms_sk_average": "20",
    "mms_kt_average": "25",
    "mms_lg_average": "36"
  }
]</pre>

</div>

<div class="section">

# 메시지 상태 코드

<span style="letter-spacing: 0.05em;">아래 참고자료와 같이 천번대의 숫자별로 의미가 다르며 보통 문자전송시에 나오는 오류메시지는 1000번대 입니다.</span>

## 참고자료

<table border="1" cellpadding="1" cellspacing="1" style="width:100%;">

<thead>

<tr>

<th scope="col">코드</th>

<th scope="col">내용</th>

</tr>

</thead>

<tbody>

<tr>

<td>1xxx</td>

<td>접수(전) 상태 코드</td>

</tr>

<tr>

<td>2xxx</td>

<td>쿨에스엠에스 게이트웨이 내에서 발송중 상태 코드</td>

</tr>

<tr>

<td>3xxx</td>

<td>연동망에서 발송 상태 코드</td>

</tr>

<tr>

<td>4xxx</td>

<td>

발송완료 상태 코드

</td>

</tr>

</tbody>

</table>

## 상태코드

<table border="1" cellpadding="1" cellspacing="1" style="width:100%;">

<thead>

<tr>

<th scope="col">코드</th>

<th scope="col">내용</th>

</tr>

</thead>

<tbody>

<tr>

<td>1010</td>

<td>필수 입력 값 미입력</td>

</tr>

<tr>

<td>1020</td>

<td>등록된 계정이 아니거나 패스워드가 틀림</td>

</tr>

<tr>

<td>1021</td>

<td>해당 메시지가 없음</td>

</tr>

<tr>

<td>1022</td>

<td>해당 그룹이 없음</td>

</tr>

<tr>

<td>1023</td>

<td>해당 이미지가 없음</td>

</tr>

<tr>

<td>1024</td>

<td>서버 오류</td>

</tr>

<tr>

<td>1025</td>

<td>이미지 입력되었으나 타입이 MMS가 아님</td>

</tr>

<tr>

<td>1026</td>

<td>중복 수신번호</td>

</tr>

<tr>

<td>1030</td>

<td>잔액 부족</td>

</tr>

<tr>

<td>1061</td>

<td>사용자에 의해 수신거부 됨(080무료수신거부)</td>

</tr>

<tr>

<td>1062</td>

<td>발신번호 미등록</td>

</tr>

<tr>

<td>2000</td>

<td>정상 접수</td>

</tr>

<tr>

<td>2100</td>

<td>(예약) 대기중</td>

</tr>

<tr>

<td>2160</td>

<td>예약 취소</td>

</tr>

<tr>

<td>2230</td>

<td>잔액 부족</td>

</tr>

<tr>

<td>2254</td>

<td>스팸처리(쿨에스엠에스 게이트웨이)</td>

</tr>

<tr>

<td>3000</td>

<td>이통사로 접수 완료(정상)</td>

</tr>

<tr>

<td>3054</td>

<td>스팸처리(이통사)</td>

</tr>

<tr>

<td>3032</td>

<td>미가입자</td>

</tr>

<tr>

<td>3040</td>

<td>전송시간 초과</td>

</tr>

<tr>

<td>3041</td>

<td>단말기 busy</td>

</tr>

<tr>

<td>3042</td>

<td>음영지역</td>

</tr>

<tr>

<td>3043</td>

<td>단말기 Power off</td>

</tr>

<tr>

<td>3044</td>

<td>단말기 메시지 저장갯수 초과</td>

</tr>

<tr>

<td>3045</td>

<td>단말기 일시 서비스 정지</td>

</tr>

<tr>

<td>3046</td>

<td>기타 단말기 문제</td>

</tr>

<tr>

<td>3047</td>

<td>착신거절</td>

</tr>

<tr>

<td>3049</td>

<td>Format Error</td>

</tr>

<tr>

<td>3050</td>

<td>SMS서비스 불가 단말기</td>

</tr>

<tr>

<td>3051</td>

<td>착신측의 호불가 상태</td>

</tr>

<tr>

<td>3052</td>

<td>이통사 서버 운영자 삭제</td>

</tr>

<tr>

<td>3053</td>

<td>서버 메시지 Que Full</td>

</tr>

<tr>

<td>3054</td>

<td>SPAM</td>

</tr>

<tr>

<td>3055</td>

<td>SPAM, nospam.or.kr 에 등록된 번호</td>

</tr>

<tr>

<td>3056</td>

<td>전송실패(무선망단)</td>

</tr>

<tr>

<td>3057</td>

<td>전송실패(무선망->단말기단)</td>

</tr>

<tr>

<td>3058</td>

<td>전송경로 없음</td>

</tr>

<tr>

<td>3059</td>

<td>변작된 발신번호.</td>

</tr>

<tr>

<td>4000</td>

<td>수신완료</td>

</tr>

</tbody>

</table>

</div>
