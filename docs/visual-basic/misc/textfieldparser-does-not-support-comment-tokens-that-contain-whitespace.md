---
title: TextFieldParser는 공백이 포함 된 주석 토큰을 지원 하지 않습니다.
ms.date: 07/20/2015
f1_keywords:
- vbrTextFieldParser_WhitespaceInToken
ms.assetid: 55107656-270e-4bbb-841a-478904df8e07
ms.openlocfilehash: 9a14bc29ecfa917b6213f32cd170aa83d6f60f58
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54525016"
---
# <a name="textfieldparser-does-not-support-comment-tokens-that-contain-white-space"></a>TextFieldParser는 공백이 포함 된 주석 토큰을 지원 하지 않습니다.
공백이 포함된 주석 토큰이 제공되었습니다. 토큰의 시작 부분에 공백이 발생하지 않는 한 `TextFieldParser` 는 공백을 포함하는 주석 토큰을 지원하지 않습니다. 토큰의 시작 부분에 있는 공백은 무시됩니다.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
-   올바른 주석 토큰을 제공합니다.  
  
## <a name="see-also"></a>참고자료

- [TextFieldParser.CommentTokens Property](xref:Microsoft.VisualBasic.FileIO.TextFieldParser.CommentTokens%2A)
- [TextFieldParser 개체를 사용하여 텍스트 파일 구문 분석](../../visual-basic/developing-apps/programming/drives-directories-files/parsing-text-files-with-the-textfieldparser-object.md)
- [TextFieldParser 개체](../../visual-basic/language-reference/objects/textfieldparser-object.md)
