---
title: <discoveryClientSettings>
ms.date: 03/30/2017
ms.assetid: 02e1b823-a8bb-4074-90d5-8599f71e8f9d
ms.openlocfilehash: 5b60c7281b92a487ba3ee275f7405cb82bd6cd87
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55282245"
---
# <a name="discoveryclientsettings"></a>\<discoveryClientSettings>
응용 프로그램에서 서비스 검색 프로세스에 클라이언트로 참여하기 위해 필요한 설정이 포함됩니다.  
  
\<system.ServiceModel>  
\<standardEndpoints>  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.serviceModel>
  <standardEndpoints>
    <dynamicEndpoint>
      <standardEndpoint>
        <discoveryClientSettings discoveryEndpoint="String">
          <findCriteria duration="TimeSpan"
                        maxResults="Integer"
                        scopeMatchBy="Uri">
            <contractTypeNames>
              <add name="String"
                   namespace="String" />
            <contractTypeNames>
            <extensions />
            <scopes>
              <add scope="URI"/>
            </scopes>
          </findCriteria>
        </discoveryClientSettings>
      <standardEndpoint>
    </dynamicEndpoint>
  </standardEndpoints>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|discoveryEndpoint|클라이언트 응용 프로그램에서 런타임에 검색 가능한 서비스를 자동으로 검색하고 해당 주소를 찾을 수 있도록 하는 검색 엔드포인트의 이름을 포함하는 문자열입니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<standardEndpoints>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|클라이언트 응용 프로그램에서 검색 서비스를 찾기 위해 사용하는 조건 집합을 제공하는 구성 요소입니다. 조건 (찾으려는 서비스 지정) 하는 검색 조건으로 그룹화 할 수 있습니다 및 찾기 종료 조건 (검색 지속 기간).|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<standardEndpoints>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|응용 프로그램이 런타임에 엔드포인트 주소를 동적으로 찾을 수 있는 클라이언트 프로그램으로 기능하도록 설정하기 위한 정보를 포함하는 표준 엔드포인트를 정의합니다.|  
  
## <a name="see-also"></a>참고자료
- <xref:System.ServiceModel.Discovery.DiscoveryClientBindingElement>
- <xref:System.ServiceModel.Discovery.Configuration.DiscoveryClientSettingsElement>
