---
title: '방법: 디자이너를 사용 하 여 Windows Forms DataGridView 컨트롤에서 열 다시 정렬 사용'
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], column order
- Windows Forms, columns
- columns [Windows Forms], reordering
- data [Windows Forms], displaying
ms.assetid: d82bd69c-6799-4439-a32c-91139c5901d1
ms.openlocfilehash: d0617ddcca4c6f94f69179fadb2d436bff476660
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54700340"
---
# <a name="how-to-enable-column-reordering-in-the-windows-forms-datagridview-control-using-the-designer"></a>방법: 디자이너를 사용 하 여 Windows Forms DataGridView 컨트롤에서 열 다시 정렬 사용
Windows Forms에 표시 된 데이터를 볼 때 <xref:System.Windows.Forms.DataGridView> 컨트롤을 특정 열에 값을 비교할 사용자가 원하는 경우가 있습니다. 이 불편할 수 있습니다 열 컨트롤에서 광범위 하 게 분리 되어 있으면 사용자가 관심 있는 모든 열을 표시 하려면 가로 앞뒤로 스크롤해야 하는 경우에 특히 합니다. 사용자가 열의 순서를 변경 하려면를 사용 하 여 열 값을 쉽게 비교 작업을 할 수 있습니다. 열 다시 정렬을 사용 하도록 설정 하면 사용자는 마우스로 열 헤더를 끌어 열을 새 위치로 이동할 수 있습니다.  
  
 다음 절차를 수행 하려면을 **Windows 응용 프로그램** 포함 하는 양식을 사용 하 여 프로젝트를 <xref:System.Windows.Forms.DataGridView> 제어 합니다. 이러한 프로젝트 설정에 대 한 자세한 내용은 [방법: Windows 응용 프로그램 프로젝트를 만듭니다](https://msdn.microsoft.com/library/b2f93fed-c635-4705-8d0e-cf079a264efa) 고 [방법: Windows Forms에 컨트롤 추가](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)합니다.  
  
> [!NOTE]
>  표시되는 대화 상자와 메뉴 명령은 활성 설정이나 버전에 따라 도움말에서 설명하는 것과 다를 수 있습니다. 설정을 변경하려면 **도구** 메뉴에서 **설정 가져오기 및 내보내기** 를 선택합니다. 자세한 내용은 [Visual Studio IDE 개인 설정](/visualstudio/ide/personalizing-the-visual-studio-ide)을 참조하세요.  
  
### <a name="to-enable-column-reordering"></a>열 다시 정렬을 활성화 하려면  
  
-   스마트 태그 문자 모양을 클릭 (![스마트 태그 문자 모양](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.gif "VS_WinFormSmtTagGlyph"))의 오른쪽 위 모서리에는 <xref:System.Windows.Forms.DataGridView> 컨트롤을 선택한 후 **열 다시 정렬 사용**.  
  
## <a name="see-also"></a>참고자료
- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.AllowUserToOrderColumns%2A?displayProperty=nameWithType>
- [방법: 디자이너를 사용 하 여 Windows Forms DataGridView 컨트롤에서 열 고정](../../../../docs/framework/winforms/controls/freeze-columns-in-the-datagrid-using-the-designer.md)
- [방법: Windows 애플리케이션 프로젝트 만들기](https://msdn.microsoft.com/library/b2f93fed-c635-4705-8d0e-cf079a264efa)
- [방법: Windows Forms에 컨트롤 추가](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)
