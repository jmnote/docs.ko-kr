---
title: '방법: 패널의 자식 표시'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- adorners [WPF], binding to children of Panels
- Panel control [WPF], binding adorners to children
ms.assetid: 4cc9b972-b472-4e5c-bdf3-3702d7fbb1f5
ms.openlocfilehash: ae039243ded93eb2bc7f85f9f07fad1dbe0eac2e
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54544980"
---
# <a name="how-to-adorn-the-children-of-a-panel"></a>방법: 패널의 자식 표시
지정된 된 자식에 표시기를 프로그래밍 방식으로 바인딩하는 방법을 보여 주는이 예제 <xref:System.Windows.Controls.Panel>합니다.  
  
## <a name="example"></a>예제  
 자식에 표시기를 바인딩할는 <xref:System.Windows.Controls.Panel>, 다음이 단계를 수행 합니다.  
  
1.  선언 <xref:System.Windows.Documents.AdornerLayer> 개체를 호출 합니다 `static` <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A> 자식을 표시할 요소에 대 한 표시기 계층을 찾을 방법입니다.  
  
2.  부모 요소와 호출의 자식을 열거는 <xref:System.Windows.Documents.AdornerLayer.Add%2A> 표시기 각 자식 요소를 바인딩하는 방법입니다.  
  
 다음 예제에서는 바인딩합니다 (위에 표시 됨)의 자식 항목에는 <xref:System.Windows.Controls.StackPanel> 라는 *myStackPanel*합니다.  
  
 [!code-csharp[Adorners_SimpleCircleAdorner#_AdornChildren](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_adornchildren)]
 [!code-vb[Adorners_SimpleCircleAdorner#_AdornChildren](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_adornchildren)]  
  
> [!NOTE]
>  [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]를 사용하여 표시기를 다른 요소에 바인딩하는 것은 현재 지원되지 않습니다.  
  
## <a name="see-also"></a>참고자료
- [표시기 개요](../../../../docs/framework/wpf/controls/adorners-overview.md)
