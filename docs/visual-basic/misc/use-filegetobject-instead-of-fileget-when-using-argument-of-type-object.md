---
title: "'Object' 형식의 인수를 사용하는 경우 'FileGet' 대신 'FileGetObject'를 사용합니다."
ms.date: 07/20/2015
ms.assetid: 090b8088-895a-482a-9362-606596bac304
ms.openlocfilehash: 60eaabc686070aced908116728f06d4e82b5cecb
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54723396"
---
# <a name="use-filegetobject-instead-of-fileget-when-using-argument-of-type-object"></a>'Object' 형식의 인수를 사용하는 경우 'FileGet' 대신 'FileGetObject'를 사용합니다.
`FileGet` 메서드는 `Object`형식의 인수를 포함합니다. 모호성을 피하기 위해`FileGetObject` 대신 `FileGet` 를 사용해야 합니다.  
  
 `My.Computer.Filesystem`에서 제공하는 기능이 `FileGet` 또는 `FileGetObject`보다 사용하기 쉽고 성능이 뛰어납니다.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1.  `FileGet` 을 `FileGetObject`로 바꿉니다.  
  
2.  `Object` 인수를 더 구체적인 형식으로 캐스트합니다.  
  
## <a name="see-also"></a>참고자료

- [My.Computer.FileSystem](xref:Microsoft.VisualBasic.FileIO.FileSystem)
