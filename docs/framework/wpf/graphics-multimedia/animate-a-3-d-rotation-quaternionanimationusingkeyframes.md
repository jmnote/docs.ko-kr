---
title: '방법: 키 프레임을 사용하여 3차원 회전에 애니메이션 효과 주기(QuaternionAnimationUsingKeyFrames)'
ms.date: 03/30/2017
helpviewer_keywords:
- 3-D translations [WPF], animating [WPF], with key frames (QuaternionAnimationUsingKeyFrames)
- key frames [WPF], QuaternionAnimationUsingKeyFrames
- animation [WPF], 3-D translations [WPF], with key frames (QuaternionAnimationUsingKeyFrames)
ms.assetid: 09e5707b-7523-4a08-9aa7-bb13cbedccdf
ms.openlocfilehash: 6cb58c2ed97cad1539f3703c98b9af57b0af22fb
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54637718"
---
# <a name="how-to-animate-a-3-d-rotation-using-key-frames-quaternionanimationusingkeyframes"></a>방법: 키 프레임을 사용하여 3차원 회전에 애니메이션 효과 주기(QuaternionAnimationUsingKeyFrames)
다음 예에서 <xref:System.Windows.Media.Animation.QuaternionAnimationUsingKeyFrames> 회전 3D 개체를 만드는 데 사용 됩니다. 이 애니메이션에는 다음 키 프레임을 사용합니다.  
  
1.  <xref:System.Windows.Media.Animation.LinearRotation3DKeyFrame> 만드는 값 사이 매끄러운 선형 보간을 사용 됩니다.  
  
2.  <xref:System.Windows.Media.Animation.DiscreteRotation3DKeyFrame> 갑작스러운 이동을 만듭니다 "" 값 (보간 없음) 사이 사용 됩니다.  
  
3.  <xref:System.Windows.Media.Animation.SplineRotation3DKeyFrame> 에 따라 값 사이 가변 전환을 만드는 데 사용 되는 <xref:System.Windows.Media.Animation.SplineRotation3DKeyFrame.KeySpline%2A> 속성입니다. 아래 예제에서 애니메이션의이 부분 느린 해제 하지만 시간 세그먼트의 끝에 다가가 시작, 면 기하급수적으로 빨라집니다.  
  
## <a name="example"></a>예제  
 [!code-xaml[Animation3DGallery_snip#QuaternionAnimationUsingKeyFramesExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/QuaternionAnimationUsingKeyFramesExample.xaml#quaternionanimationusingkeyframesexamplewholepage)]  
  
## <a name="see-also"></a>참고자료
- [Storyboard를 사용하여 3차원 회전에 애니메이션 효과 주기](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-storyboards.md)
- [Rotation3DAnimation을 사용하여 3차원 회전에 애니메이션 효과 주기](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-rotation3danimation.md)
- [4원수를 사용하여 3차원 회전에 애니메이션 효과 주기](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-quaternions.md)
- [키 프레임을 사용하여 3차원 회전에 애니메이션 효과 주기(Rotation3DAnimationUsingKeyFrames)](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-3-d-rotation-using-key-frames.md)
- [3차원 그래픽 개요](../../../../docs/framework/wpf/graphics-multimedia/3-d-graphics-overview.md)
- [키 프레임 애니메이션 개요](../../../../docs/framework/wpf/graphics-multimedia/key-frame-animations-overview.md)
