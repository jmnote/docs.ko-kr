---
title: Key(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.AnonymousKey
helpviewer_keywords:
- anonymous types [Visual Basic], key
- Key [Visual Basic]
- Key keyword [Visual Basic]
ms.assetid: 7697a928-7d14-4430-a72a-c9e96e8d6c11
ms.openlocfilehash: 695f356f44bfd6ea5ad3c0a977ec31ddfbea2b05
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54668225"
---
# <a name="key-visual-basic"></a>Key(Visual Basic)
`Key` 키워드를 사용 하면 익명 형식의 속성에 대 한 동작을 지정할 수 있습니다. 키 속성 익명 형식 인스턴스 또는 해시 코드 값입니다. 계산이 간에 같음 테스트에 참여 하는 대로 속성만 지정 합니다. 키 속성의 값을 변경할 수 없습니다.  
  
 키워드를 배치 하 여 키 속성으로 익명 형식의 속성을 지정 `Key` 초기화 목록에 선언 앞에 있습니다. 다음 예에서 `Airline` 하 고 `FlightNo` 키 속성은 있지만 `Gate` 아닙니다.  
  
 [!code-vb[VbVbalrAnonymousTypes#26](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_1.vb)]  
  
 직접 상속 하는 새로운 무명 형식 만들어지면 <xref:System.Object>합니다. 컴파일러는 세 명의 상속 된 멤버를 재정의: <xref:System.Object.Equals%2A>, <xref:System.Object.GetHashCode%2A>, 및 <xref:System.Object.ToString%2A>합니다. 생성 된 재정의 코드는 <xref:System.Object.Equals%2A> 및 <xref:System.Object.GetHashCode%2A> 키 속성에 기반 합니다. 형식에 키 속성이 없는 경우 <xref:System.Object.GetHashCode%2A> 고 <xref:System.Object.Equals%2A> 은 무시 되지 않습니다.  
  
## <a name="equality"></a>같음  
 동일한 형식의 인스턴스인 경우 및 해당 키 속성의 값이 같으면 두 익명 형식 인스턴스 같습니다. 다음 예에서 `flight2` 값과 같음 `flight1` 이전 예제에서 인스턴스의 동일한 익명 이기 때문에 형식이 있으며 일치 하는 키 속성의 값입니다. 그러나 `flight3` 같지 `flight1` 키 속성에 대해 다른 값이 있어 `FlightNo`합니다. 인스턴스 `flight4` 와 동일한 형식이 아닌 `flight1` 키 속성으로 다른 속성을 지정 하므로 합니다.  
  
 [!code-vb[VbVbalrAnonymousTypes#27](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_2.vb)]  
  
 두 인스턴스 키가 아닌 속성만 동일한 이름, 형식, 순서 및 값을 사용 하 여 선언 된 경우 두 인스턴스가 같지 않습니다. 키 속성 없이 인스턴스 자체에 같습니다.  
  
 두 개의 익명 형식 인스턴스는 동일한 익명 형식의 인스턴스는 조건에 대 한 자세한 내용은 참조 하세요. [익명 형식](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)합니다.  
  
## <a name="hash-code-calculation"></a>해시 코드 계산  
 와 같은 <xref:System.Object.Equals%2A>, 해시 함수에 정의 된 <xref:System.Object.GetHashCode%2A> 무명 형식을 형식의 키 속성을 기반에 대 한 합니다. 다음 예제에서는 키 속성 및 해시 간의 상호 작용 코드 값을 표시 합니다.  
  
 모든 키 속성에 대해 동일한 값이 있는 무명 형식의 인스턴스 키가 아닌 속성 값을 일치 하는 있지 않은 경우에 동일한 해시 코드 값을 가집니다. 다음 문은 반환 `True`합니다.  
  
 [!code-vb[VbVbalrAnonymousTypes#37](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_3.vb)]  
  
 하나 이상의 키 속성에 대해 다른 값이 있는 무명 형식의 인스턴스는 서로 다른 해시 코드 값을 가집니다. 다음 문은 반환 `False`합니다.  
  
 [!code-vb[VbVbalrAnonymousTypes#38](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_4.vb)]  
  
 키 속성으로 다른 속성을 지정 하는 무명 형식의 인스턴스는 동일한 형식의 인스턴스 않습니다. 경우에 모든 속성의 값과 이름이 같은 다른 해시 코드 값 갖습니다. 다음 문은 반환 `False`합니다.  
  
 [!code-vb[VbVbalrAnonymousTypes#39](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_5.vb)]  
  
## <a name="read-only-values"></a>읽기 전용 값  
 키 속성의 값을 변경할 수 없습니다. 예를 들어 `flight1` 앞의 예제에는 `Airline` 및 `FlightNo` 필드는 읽기 전용 있지만 `Gate` 변경할 수 있습니다.  
  
 [!code-vb[VbVbalrAnonymousTypes#28](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/key_6.vb)]  
  
## <a name="see-also"></a>참고자료
- [익명 형식 정의](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-type-definition.md)
- [방법: 무명 형식 선언에서 속성 이름 및 형식 유추](../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)
- [익명 형식](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
