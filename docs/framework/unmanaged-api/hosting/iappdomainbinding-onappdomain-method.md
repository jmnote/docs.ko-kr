---
title: IAppDomainBinding::OnAppDomain 메서드
ms.date: 03/30/2017
api_name:
- IAppDomainBinding.OnAppDomain
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- OnAppDomain
helpviewer_keywords:
- IAppDomainBinding::OnAppDomain method [.NET Framework hosting]
- OnAppDomain method [.NET Framework hosting]
ms.assetid: b419dcc9-e8aa-484b-af0d-0f40358edb99
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8dfd396568424c3a2300ed5d982e766afd5f925f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54725495"
---
# <a name="iappdomainbindingonappdomain-method"></a>IAppDomainBinding::OnAppDomain 메서드
CLR (공용 언어 런타임) 응용 프로그램 도메인이 만들어졌는지 호스트에 알리기 위해 호출 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT OnAppDomain (  
    [in] IUnknown* pAppdomain  
);  
```  
  
#### <a name="parameters"></a>매개 변수  
 `pAppdomain`  
 [in] 에 대 한 포인터를 [IUnknown](https://msdn.microsoft.com/library/94as6ehy(v=vs.110).aspx) 새 응용 프로그램 도메인을 나타내는 인터페이스 개체입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료
- [IAppDomainBinding 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iappdomainbinding-interface.md)
