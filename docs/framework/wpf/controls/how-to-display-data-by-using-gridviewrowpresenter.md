---
title: '방법: GridViewRowPresenter를 사용하여 데이터 표시'
ms.date: 03/30/2017
helpviewer_keywords:
- displaying data with GridViewRowPresenter [WPF]
- GridViewRowPresenter [WPF]
ms.assetid: bdb785a5-a262-44d5-a517-ea14383e5f70
ms.openlocfilehash: b60fe0e78883b166688377c42113a093c78d7751
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54607961"
---
# <a name="how-to-display-data-by-using-gridviewrowpresenter"></a>방법: GridViewRowPresenter를 사용하여 데이터 표시
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.GridViewRowPresenter> 및 <xref:System.Windows.Controls.GridViewHeaderRowPresenter> 열에 데이터를 표시할 개체입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 지정 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.GridViewColumnCollection> 표시 하는 합니다 <xref:System.DateTime.DayOfWeek%2A> 및 <xref:System.DateTime.Year%2A> 의 <xref:System.DateTime> 개체를 사용 하 여 <xref:System.Windows.Controls.GridViewRowPresenter> 및 <xref:System.Windows.Controls.GridViewHeaderRowPresenter> 개체입니다. 이 예제에서는 또한 정의 <xref:System.Windows.Style> 에 대 한는 <xref:System.Windows.Controls.GridViewColumn.Header%2A> 의 <xref:System.Windows.Controls.GridViewColumn>합니다.  
  
 [!code-xaml[GridViewRowPresenterSample#GridViewRowPresenter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GridViewRowPresenterSample/CS/Window1.xaml#gridviewrowpresenter)]  
  
## <a name="see-also"></a>참고자료
- <xref:System.Windows.Controls.GridViewHeaderRowPresenter>
- <xref:System.Windows.Controls.GridViewRowPresenter>
- <xref:System.Windows.Controls.GridViewColumnCollection>
- [GridView 개요](../../../../docs/framework/wpf/controls/gridview-overview.md)
