---
title: RemoveHandler 문 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.RemoveHandlerMethod
- vb.RemoveHandler
- RemoveHandler
helpviewer_keywords:
- RemoveHandler keyword [Visual Basic]
- RemoveHandler statement [Visual Basic]
ms.assetid: 647cd825-e877-4910-b4f1-8d168beebe6a
ms.openlocfilehash: 27cdd2753507c6fc4d5c5041607e2ccb425b81b8
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54560622"
---
# <a name="removehandler-statement"></a>RemoveHandler 문
이벤트와 이벤트 처리기 간의 연결을 제거합니다.  
  
## <a name="syntax"></a>구문  
  
```  
RemoveHandler event, AddressOf eventhandler  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`event`|처리 중인 이벤트의 이름입니다.|  
|`eventhandler`|현재 이벤트를 처리 하는 프로시저의 이름입니다.|  
  
## <a name="remarks"></a>설명  
 합니다 `AddHandler` 및 `RemoveHandler` 문을 시작 하 고 언제 든 지 프로그램 실행 중 특정 이벤트에 대 한 이벤트 처리를 중지할 수 있습니다.  
  
> [!NOTE]
>  사용자 지정 이벤트에 대 한 합니다 `RemoveHandler` 문은 호출 이벤트의 `RemoveHandler` 접근자입니다. 사용자 지정 이벤트에 대 한 자세한 내용은 참조 하세요. [이벤트 연결 문으로](../../../visual-basic/language-reference/statements/event-statement.md)합니다.  
  
## <a name="example"></a>예제  
 [!code-vb[VbVbalrEvents#17](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/removehandler-statement_1.vb)]  
  
## <a name="see-also"></a>참고자료
- [AddHandler 문](../../../visual-basic/language-reference/statements/addhandler-statement.md)
- [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)
- [Event 문](../../../visual-basic/language-reference/statements/event-statement.md)
- [이벤트](../../../visual-basic/programming-guide/language-features/events/index.md)
