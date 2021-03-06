---
title: '방법: PointAnimation을 사용하여 개체 위치에 애니메이션 효과 주기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], animation
- animation [WPF], PointAnimation
ms.assetid: 42310977-cc90-438a-8a47-0345898e01be
ms.openlocfilehash: e359e712f533c861a694c53848ca0eaeb289eb21
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54495555"
---
# <a name="how-to-animate-the-position-of-an-object-by-using-pointanimation"></a>방법: PointAnimation을 사용하여 개체 위치에 애니메이션 효과 주기
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.Animation.PointAnimation> 클래스를 따라 개체에 애니메이션 효과 주기는 <xref:System.Windows.Shapes.Path>합니다.  
  
## <a name="example"></a>예제  
 다음 예제를 따라 타원을 이동는 <xref:System.Windows.Shapes.Path> 다른 화면의 한 점에서 합니다. 예제 애니메이션의 위치는 <xref:System.Windows.Media.EllipseGeometry> 를 사용 하 여 <xref:System.Windows.Media.Animation.PointAnimation> 애니메이션 효과를 주는 <xref:System.Windows.Media.EllipseGeometry.Center%2A> 속성.  
  
 [!code-csharp[BasicAnimations_snip#PointAnimationWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BasicAnimations_snip/CSharp/PointAnimationExample.cs#pointanimationwholepage)]
 [!code-vb[BasicAnimations_snip#PointAnimationWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BasicAnimations_snip/VisualBasic/PointAnimationExample.vb#pointanimationwholepage)]  
  
## <a name="see-also"></a>참고자료
- <xref:System.Windows.Media.Animation.PointAnimation>
- <xref:System.Windows.Shapes.Path>
- <xref:System.Windows.Media.EllipseGeometry>
- <xref:System.Windows.Media.EllipseGeometry.Center%2A>
- [애니메이션 개요](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)
- [그래픽 및 멀티미디어](../../../../docs/framework/wpf/graphics-multimedia/index.md)
- [방법 항목](../../../../docs/framework/wpf/graphics-multimedia/graphics-how-to-topics.md)
- [애니메이션 및 타이밍](https://msdn.microsoft.com/library/7d83765b-d5ae-41b1-b423-80206e1124aa)
- [방법 항목](../../../../docs/framework/wpf/graphics-multimedia/animation-and-timing-how-to-topics.md)
