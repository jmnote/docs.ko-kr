---
title: '방법: 데이터 개체에 여러 데이터 형식 저장'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataObject class [WPF], storing multiple formats
- DataFormats class [WPF], storing multiple formats
- drag-and-drop [WPF], storing multiple formats
ms.assetid: 941ace29-29c4-4c26-b75b-ea7d06aa0d69
ms.openlocfilehash: 33415dd3cb1a05263cf9fb9ecafcbc857d364d57
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54555676"
---
# <a name="how-to-store-multiple-data-formats-in-a-data-object"></a>방법: 데이터 개체에 여러 데이터 형식 저장
다음 예제에서는 사용 하는 방법의 <xref:System.Windows.DataObject.SetData%28System.String%2CSystem.Object%29> 여러 형식의 데이터 개체에 데이터를 추가 하는 방법입니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>설명  
  
### <a name="code"></a>코드  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_StoreMultipleFormats](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_storemultipleformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_StoreMultipleFormats](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_storemultipleformats)]  
  
## <a name="see-also"></a>참고자료
- <xref:System.Windows.IDataObject>
- [끌어서 놓기 개요](../../../../docs/framework/wpf/advanced/drag-and-drop-overview.md)
