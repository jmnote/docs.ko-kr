---
title: Visual Basic에서 상속된 이벤트 처리기 관련 문제 해결
ms.date: 07/20/2015
helpviewer_keywords:
- troubleshooting events [Visual Basic]
- inherited events [Visual Basic]
- troubleshooting Visual Basic, event handlers
- event handling, troubleshooting
- event handlers, troubleshooting
ms.assetid: e1c8759f-5370-4308-8476-8c48b73509bf
ms.openlocfilehash: e7c56757d18a22a65b4ef8e81d2a05e5f4f4dffc
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54680202"
---
# <a name="troubleshooting-inherited-event-handlers-in-visual-basic"></a>Visual Basic에서 상속된 이벤트 처리기 관련 문제 해결
이 항목에서는 상속 된 구성 요소에서 이벤트 처리기를 사용 하 여 발생 하는 일반적인 문제를 나열 합니다.  
  
## <a name="procedures"></a>절차  
  
#### <a name="code-in-event-handler-executes-twice-for-every-call"></a>이벤트 처리기의 코드는 모든 호출에 대 한 두 번 실행  
  
-   상속 된 이벤트 처리기를 포함할 수 없습니다는 [처리](../../../../visual-basic/language-reference/statements/handles-clause.md) 절. 기본 클래스의 메서드 이벤트와 이미 연결 되어 있으며 그에 따라 실행 됩니다. 제거 된 `Handles` 상속 된 메서드에서 절.  
  
     [!code-vb[VbVbalrEvents#32](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/troubleshooting-inherited-event-handlers_1.vb)]  
  
-   상속 된 메서드에 없는 경우는 `Handles` 키워드를 추가 코드는 포함 되지 않았는지 확인 [AddHandler 문](../../../../visual-basic/language-reference/statements/addhandler-statement.md) 또는 동일한 이벤트를 처리 하는 추가 메서드가 있습니다.  
  
## <a name="see-also"></a>참고자료
- [이벤트](../../../../visual-basic/programming-guide/language-features/events/index.md)
