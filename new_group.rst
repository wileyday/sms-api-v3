그룹생성
======

메시지를 담을 그룹을 생성하여 그룹아이디를 리턴합니다. 생성된 그룹은 2시간 후에 자동 삭제됩니다.

Resource URL
------------
`<https://coolsms.co.kr/sms/3/new_group>`_

Parameters
----------
SRK
  - 솔루션 제공 수수료를 정산받을 솔루션 등록키
  - 자세한 안내는 http://www.coolsms.co.kr/sp 을 참고하세요.  
Mode
  - test로 입력할 경우 CARRIER 시뮬레이터로 시뮬레이션됩니다.<br>** 수신번호를 반드시 01000000000 으로 테스트 **<br>예약필드 datetime는 무시됩니다.<br>결과값은 60 잔액에서 실제 차감되며 다음날 새벽에 재충전됩니다.
ForceSMS
  - 누리고푸시를 사용하더라도 강제로 문자 발송.
  - true 혹은 false(기본)
OnlyATA
  - 알림톡이 실패해도 문자메시지로 대체하여 발송하지 않습니다.
  - true 혹은 false(기본)
SiteUser
  - API를 호출하는 사이트에서 관리하는 유저 아이디 입력.
  - 미입력시 __private__ 으로 입력됩니다.
  - 해당 아이디 앞으로 등록된 발신번호를 확인합니다.
  - 발신번호 등록 API를 참고하세요.
  - http://www.coolsms.co.kr/SenderID_API
OSPlatform
  - 클라이언트의 OS 및 플랫폼 버전
  - 예) CentOS 6.6<br>(v1.5에서 추가됨)
DevLanguage
  - 개발 프로그래밍 언어
  - 예) PHP 5.3.3<br>(v1.5에서 추가됨)
SDKVersion
  - SDK 버전<br>예) PHP SDK 1.5
  - (v1.5에서 추가됨)
APPVersion
  - 어플리케이션 버전
  - 예) Purplebook 4.1<br>(v1.5에서 추가됨)

Response
--------

JSON 포맷으로 리턴 됩니다.

GroupID
  - 그룹아이디


Example Request
---------------



Example Response
----------------

.. code-block:: javascript

  {
    "group_id": "565ba3d7d216a"
  }
