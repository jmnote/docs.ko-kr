---
title: <exception>(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- <exception> XML tag
- exception XML tag
ms.assetid: c0517549-171e-4dae-ab88-a9c1700b6eee
ms.openlocfilehash: b2475bd5eaeadc12e4c8c9b0fb77a2fa5cb88911
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2019
ms.locfileid: "55283938"
---
# <a name="exception-visual-basic"></a>\<예외 > (Visual Basic)
예외를 throw 할 수를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
<exception cref="member">description</exception>  
```  
  
#### <a name="parameters"></a>매개 변수  
 `member`  
 현재 컴파일 환경에서 사용할 수 있는 예외에 대한 참조입니다. 컴파일러는 지정된 예외가 있으며 `member`를 출력 XML의 정식 요소 이름으로 변환하는지 확인합니다. `member`는 큰따옴표(" ")로 묶어야 합니다.  
  
 `description`  
 설명.  
  
## <a name="remarks"></a>설명  
 사용 된 `<exception>` 는 예외를 throw 할 수를 지정 하는 태그입니다. 이 태그는 메서드 정의에 적용됩니다.  
  
 [/doc](../../../visual-basic/reference/command-line-compiler/doc.md)로 컴파일하여 문서 주석을 파일로 처리합니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 합니다 `<exception>` 예외를 설명 하는 태그는는 `IntDivide` 함수가 throw 할 수 있습니다.  
  
 [!code-vb[VbVbcnXmlDocComments#3](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/exception_1.vb)]  
  
## <a name="see-also"></a>참고자료
- [XML 주석 태그](../../../visual-basic/language-reference/xmldoc/index.md)
