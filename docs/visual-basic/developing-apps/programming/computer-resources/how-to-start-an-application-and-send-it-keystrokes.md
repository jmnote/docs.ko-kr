---
title: '방법: 애플리케이션 시작 및 키 입력 보내기(Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- keystrokes, sending
- Shell command example [Visual Basic]
- processes, starting and sending keystrokes
- SendKeys.SendWait examples
ms.assetid: f1303184-fce4-44fb-88b4-aac5f42d5d77
ms.openlocfilehash: 36d6110a9e0ccf20718e95e6d7601e21e8d8f22c
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54688391"
---
# <a name="how-to-start-an-application-and-send-it-keystrokes-visual-basic"></a>방법: 애플리케이션 시작 및 키 입력 보내기(Visual Basic)
이 예제에서는 `Shell` 함수를 사용하여 계산기 애플리케이션을 시작한 다음 `My.Computer.Keyboard.SendKeys` 메서드를 통해 키 입력을 전송하여 두 숫자를 곱합니다.  
  
## <a name="example"></a>예제  
 [!code-vb[VbVbalrMyComputer#25](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/how-to-start-an-application-and-send-it-keystrokes_1.vb)]  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 요청된 프로세스 식별자를 가진 애플리케이션을 찾을 수 없는 경우 <xref:System.ArgumentException> 예외가 발생합니다.  
  
## <a name="net-framework-security"></a>.NET Framework 보안  
 `Shell` 함수에 대한 호출은 완전 신뢰가 필요합니다(<xref:System.Security.SecurityException> 클래스).  
  
## <a name="see-also"></a>참고 항목
- <xref:Microsoft.VisualBasic.Devices.Keyboard.SendKeys%2A>
- <xref:Microsoft.VisualBasic.Interaction.Shell%2A>
- <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A>
