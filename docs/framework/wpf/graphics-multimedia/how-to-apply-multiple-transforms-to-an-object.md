---
title: '방법: 개체에 다중 변환 적용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- grouping Transform objects [WPF]
- Transform objects [WPF], grouping
- graphics [WPF], grouping Transform objects
- TransformGroup [WPF]
ms.assetid: 98cd1921-12bc-4bf5-8193-529228fb7402
ms.openlocfilehash: dc9b7c052d9deb4d1167c813a6ce652c99983a9f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54649455"
---
# <a name="how-to-apply-multiple-transforms-to-an-object"></a>방법: 개체에 다중 변환 적용
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.TransformGroup> 둘 이상의 그룹에 <xref:System.Windows.Media.Transform> 개체를 단일 복합 <xref:System.Windows.Media.Transform>합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Windows.Media.TransformGroup> 적용 하는 <xref:System.Windows.Media.ScaleTransform> 및 <xref:System.Windows.Media.RotateTransform> 에 <xref:System.Windows.Controls.Button>.  
  
 [!code-xaml[Transforms_snip#MultipleTransformExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/MultipleTransformExample.xaml#multipletransformexamplewholepage)]  
  
 [!code-csharp[Transforms_Procedural_snip#MultipleTransformsCodeExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Transforms_Procedural_snip/CSharp/MultipleTransformsExample.cs#multipletransformscodeexamplewholepage)]
 [!code-vb[Transforms_Procedural_snip#MultipleTransformsCodeExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Transforms_Procedural_snip/VisualBasic/MultipleTransformsExample.vb#multipletransformscodeexamplewholepage)]  
  
## <a name="see-also"></a>참고자료
- <xref:System.Windows.UIElement.RenderTransform%2A>
- <xref:System.Windows.Media.TransformGroup>
- [Transform 개요](../../../../docs/framework/wpf/graphics-multimedia/transforms-overview.md)
- [2차원 변환 샘플](https://go.microsoft.com/fwlink/?LinkID=158252)
