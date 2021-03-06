---
title: -nologo (Visual Basic)
ms.date: 03/13/2018
helpviewer_keywords:
- -nologo compiler option [Visual Basic]
- banners [Visual Basic], suppressing startup
- nologo compiler option [Visual Basic]
- /nologo compiler option [Visual Basic]
ms.assetid: 25ef54b6-d676-4639-a2d2-a747a158bc07
ms.openlocfilehash: 1b9cedc3e45795a66c203d4c86bb071045a1d3f5
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54550476"
---
# <a name="-nologo-visual-basic"></a>-nologo (Visual Basic)
컴파일하는 동안 저작권 배너 및 정보 메시지를 표시를 하지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```  
-nologo  
```  
  
## <a name="remarks"></a>설명  
 지정 하는 경우 `-nologo`, 컴파일러를 저작권 배너를 표시 하지 않습니다. 기본적으로 `-nologo`은 적용되지 않습니다.  
  
> [!NOTE]
>  `-nologo` 옵션은 Visual Studio 개발 환경 내에서 사용할 수 있는 명령줄에서 컴파일할 경우에 사용할 수 있는 것입니다.  
  
## <a name="example"></a>예제  
 다음 코드에서는 `T2.vb` 를 저작권 배너를 표시 하지 않습니다.  
  
```console
vbc -nologo t2.vb  
```  
  
## <a name="see-also"></a>참고자료
- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
