---
title: "Windows 컨테이너를 배포 하지 않는 경우"
description: "컨테이너 화 된.NET 응용 프로그램에 대 한.NET Microservices 아키텍처 | Windows 컨테이너를 배포 하지 않는 경우"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 10/26/2017
ms.openlocfilehash: 538cb518cd169f42b3e8b7324ca108a1d366137a
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="when-not-to-deploy-to-windows-containers"></a><span data-ttu-id="ad1c7-103">Windows 컨테이너를 배포 하지 않는 경우</span><span class="sxs-lookup"><span data-stu-id="ad1c7-103">When not to deploy to Windows Containers</span></span>

<span data-ttu-id="ad1c7-104">일부 Windows 기술은 Windows 컨테이너에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad1c7-104">Some Windows technologies are not supported by Windows Containers.</span></span> <span data-ttu-id="ad1c7-105">이 경우 여전히 창과 IIS와 일반적으로 표준 Vm에 마이그레이션해야 할.</span><span class="sxs-lookup"><span data-stu-id="ad1c7-105">In those cases, you still need to migrate to standards VMs, usually with just Windows and IIS.</span></span>

<span data-ttu-id="ad1c7-106">사례 2017 중순 현재 Windows 컨테이너에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad1c7-106">Cases not supported in Windows Containers, as of mid-2017:</span></span>

-   <span data-ttu-id="ad1c7-107">Microsoft 메시지 큐 (MSMQ) 현재 지원 되지 않습니다 Windows 컨테이너에서.</span><span class="sxs-lookup"><span data-stu-id="ad1c7-107">Microsoft Message Queuing (MSMQ) currently is not supported in Windows Containers.</span></span>

    -   [<span data-ttu-id="ad1c7-108">UserVoice 요청 포럼</span><span class="sxs-lookup"><span data-stu-id="ad1c7-108">UserVoice request forum</span></span>](https://windowsserver.uservoice.com/forums/304624-containers/suggestions/15719031-create-base-container-image-with-msmq-server)

    -   [<span data-ttu-id="ad1c7-109">토론 포럼</span><span class="sxs-lookup"><span data-stu-id="ad1c7-109">Discussion forum</span></span>](https://social.msdn.microsoft.com/Forums/bce99a7d-aa60-44fa-a348-450855650810/msmqserver-is-it-supported?forum=windowscontainers)

-   <span data-ttu-id="ad1c7-110">Microsoft Distributed Transaction Coordinator (MSDTC) 현재 Windows 컨테이너에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad1c7-110">Microsoft Distributed Transaction Coordinator (MSDTC) currently is not supported in Windows Containers</span></span>

    -   [<span data-ttu-id="ad1c7-111">GitHub 문제</span><span class="sxs-lookup"><span data-stu-id="ad1c7-111">GitHub issue</span></span>](https://github.com/MicrosoftDocs/Virtualization-Documentation/issues/494)

-   <span data-ttu-id="ad1c7-112">Microsoft Office 컨테이너를 현재 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad1c7-112">Microsoft Office currently does not support containers</span></span>

    -   [<span data-ttu-id="ad1c7-113">UserVoice 요청 포럼</span><span class="sxs-lookup"><span data-stu-id="ad1c7-113">UserVoice request forum</span></span>](https://windowsserver.uservoice.com/forums/304624-containers/suggestions/19686220-provide-office-support-for-containers)

<span data-ttu-id="ad1c7-114">Windows 컨테이너에 대 한 추가 지원 되지 않는 시나리오 및 커뮤니티에서 요청에 대 한 UserVoice 포럼을 참조: <https://windowsserver.uservoice.com/forums/304624-containers>합니다.</span><span class="sxs-lookup"><span data-stu-id="ad1c7-114">For additional not-supported scenarios and requests from the community, see the UserVoice forum for Windows Containers: <https://windowsserver.uservoice.com/forums/304624-containers>.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="ad1c7-115">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ad1c7-115">Additional resources</span></span>

-   <span data-ttu-id="ad1c7-116">**가상 컴퓨터와 Azure의 컨테이너**</span><span class="sxs-lookup"><span data-stu-id="ad1c7-116">**Virtual machines and containers in Azure**</span></span>

    [<span data-ttu-id="ad1c7-117">https://docs.microsoft.com/azure/virtual-machines/windows/containers</span><span class="sxs-lookup"><span data-stu-id="ad1c7-117">https://docs.microsoft.com/azure/virtual-machines/windows/containers</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/containers)

>[!div class="step-by-step"]
<span data-ttu-id="ad1c7-118">[이전](deploy-existing-net-apps-as-windows-containers.md)
[다음](when-to-deploy-windows-containers-in-your-on-premises-iaas-vm-infrastructure.md)</span><span class="sxs-lookup"><span data-stu-id="ad1c7-118">[Previous](deploy-existing-net-apps-as-windows-containers.md)
[Next](when-to-deploy-windows-containers-in-your-on-premises-iaas-vm-infrastructure.md)</span></span>