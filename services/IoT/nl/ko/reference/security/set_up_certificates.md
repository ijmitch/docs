---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# 인증서 설정
{: #set_up_certificates.md}
마지막 업데이트 날짜: 2016년 11월 15일
{: .last-updated}

위험 및 보안 관리 추가 기능을 사용하면 인증서가 디바이스 인증에 사용되거나 MQTT 메시징을 위한 기본 IBM Watson IoT Platform 서버 인증서를 대체합니다. 서명된 유효한 인증서가 없는 디바이스는 액세스가 거부되고 서버와 통신할 수 없습니다. 

디바이스에 대해 인증서 및 서버 액세스를 구성하기 위해 시스템 운영자는 연관된 인증 기관(CA) 인증서와 선택적으로 메시지 서버 인증서를 Watson IoT Platform에 등록합니다. 

## 인증서 요구사항

등록하는 인증서에는 디바이스 ID가 CN(Common Name) 또는 SubjectAltName으로 입력되어 있어야 합니다. *CN* 필드의 경우 형식은 CN=d:devtype:devid입니다. SubjectAltName 필드의 경우 형식은 SubjectAltName=d:devtype:devid이며, 여기서 devtype은 디바이스의 디바이스 유형이고 devid는 디바이스의 클라이언트 ID입니다. 

더 이상 연결할 수 없는 디바이스를 표시하는 인증서 폐기 목록(CRL)의 사용은 베타 릴리스에서 지원되지 않습니다. 

CA 인증서를 추가하거나 메시징 서버 인증서를 대체하는 경우 모든 디바이스는 SNI(Server Name Indication)를 지원하는 MQTT 클라이언트를 사용하여 연결해야 합니다. 다중 테넌시 아키텍처의 경우 SNI는 MQTT 서버에 각 조직/테넌트 연결에 사용될 인증서를 알려줍니다. 

##디바이스 인증을 위한 인증 기관(CA) 인증서 등록

1. Watson IoT Platform에 로그인하여 **일반 설정**으로 이동하십시오.
2. **위험 관리** 섹션의 **CA 인증서**에서 **인증서 추가**를 클릭하십시오.
3. 찾아보기를 사용하여 업로드할 인증서 파일을 선택하거나 **인증서 추가** 창에서 파일을 끌어서 놓으십시오. 파일에는 인증서가 하나만 포함될 수 있으며 인증서 날짜가 유효해야 합니다. 확장자가 .pem, .cer, .cert 또는 .crt인 파일이 허용됩니다. 선택된 파일 내의 인증서 정보를 미리볼 수 있습니다. 
4. 인증서 파일의 설명을 입력하십시오. 
5. 올바른 파일이 선택되었는지 확인한 후 **저장**을 클릭하십시오. 선택한 인증서가 테이블에 나열되며 기본적으로 활성 상태입니다. 

## 메시징 서버 인증서 등록

플랫폼에서는 기본 서버 인증서를 제공합니다. 기본 인증서 중 하나를 사용하거나 조직의 인증서를 업로드할 수 있습니다. 아직 사용할 인증서가 없는 경우에는 새 인증서에 대한 요청을 작성할 수 있습니다. 새 인증서를 수신하면 서명 후에 다시 플랫폼에 업로드해야 합니다. 

기본 인증서 중 하나를 사용하거나 이미 업로드된 다른 인증서를 사용하려면 **메시징 서버 인증서** 아래의 테이블에 있는 **기본 메시징 서버 인증서** 드롭 다운 목록에서 사용할 인증서를 선택하십시오. 

### <a name="upload"> </a> 조직의 인증서 업로드

1. **일반 설정**의 **위험 관리** 섹션에서 **메시징 서버 인증서** 아래에 있는 **인증서 추가**를 클릭하십시오. 
2. 찾아보기를 사용하여 업로드할 인증서 파일을 선택하거나 **인증서 추가** 창에서 파일을 끌어서 놓으십시오. 
3. 찾아보기를 사용하여 업로드할 개인 키 파일을 선택하거나 **인증서 추가** 창에서 파일을 끌어서 놓으십시오.   
4. 개인 키가 비밀번호 문구로 암호화된 경우 개인 키의 비밀번호 문구를 입력하십시오.
5. 올바른 파일이 선택되었는지 확인한 후 **저장**을 클릭하십시오. 
6. **기본 메시징 서버 인증서** 드롭 다운 목록에서 새로 업로드한 인증서를 선택하십시오. 선택한 인증서가 테이블에 활성 인증서로 나열됩니다. 


### 새 인증서 요청

 새 메시징 서버 인증서를 사용하려는 경우 인증서 서명 요청(CSR)을 생성하여 새 인증서를 요청할 수 있습니다. 

 1. **일반 설정**의 **위험 관리** 섹션에서 **메시징 서버 인증서** 아래에 있는 **CSR 생성**을 클릭하십시오. 
 2. 서버에 대한 인증서 서명 요청(CSR)을 요청하기 위한 세부사항을 입력하고 **생성**을 클릭하십시오. 테이블에 CSR이 표시됩니다. 
 3. 요청을 다운로드하여 서명을 위해 인증 기관에 제출하십시오. 
 4. 인증서를 획득한 후에는 조직의 인증서 업로드 단계에 따라 인증서를 업로드할 수 있습니다. 인증서가 업로드되면 테이블의 CSR이 업로드된 인증서로 대체됩니다. 