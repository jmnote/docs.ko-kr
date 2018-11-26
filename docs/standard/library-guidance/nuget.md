---
title: NuGet 및 .NET 라이브러리
description: .NET 라이브러리용 NuGet을 사용하여 패키지하는 모범 사례 권장 사항입니다.
author: jamesnk
ms.author: mairaw
ms.date: 10/02/2018
ms.openlocfilehash: 479d1786c232ef1f843877169954e847453681c9
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50185627"
---
# <a name="nuget"></a><span data-ttu-id="a3062-103">NuGet</span><span class="sxs-lookup"><span data-stu-id="a3062-103">NuGet</span></span>

<span data-ttu-id="a3062-104">NuGet은 .NET 에코시스템의 패키지 관리자이며, 개발자가 .NET 오픈 소스 라이브러리를 검색하고 획득할 수 있는 기본 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-104">NuGet is a package manager for the .NET ecosystem and is the primary way developers discover and acquire .NET open-source libraries.</span></span> <span data-ttu-id="a3062-105">NuGet 패키지를 호스트하기 위해 Microsoft에서 제공하는 무료 서비스인 [NuGet.org](https://www.nuget.org/)가 공용 NuGet 패키지의 기본 호스트지만, [MyGet](https://www.myget.org/) 및 [Azure Artifacts](https://azure.microsoft.com/services/devops/artifacts/)와 같은 사용자 지정 NuGet 서비스에 게시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-105">[NuGet.org](https://www.nuget.org/), a free service provided by Microsoft for hosting NuGet packages, is the primary host for public NuGet packages, but you can publish to custom NuGet services like [MyGet](https://www.myget.org/) and [Azure Artifacts](https://azure.microsoft.com/services/devops/artifacts/).</span></span>

<span data-ttu-id="a3062-106">![NuGet](./media/nuget/nuget-logo.png "NuGet")</span><span class="sxs-lookup"><span data-stu-id="a3062-106">![NuGet](./media/nuget/nuget-logo.png "NuGet")</span></span>

## <a name="create-a-nuget-package"></a><span data-ttu-id="a3062-107">NuGet 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="a3062-107">Create a NuGet package</span></span>

<span data-ttu-id="a3062-108">NuGet 패키지(`*.nupkg`)는 .NET 어셈블리 및 관련 메타데이터를 포함하는 zip 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-108">A NuGet package (`*.nupkg`) is a zip file that contains .NET assemblies and associated metadata.</span></span>

<span data-ttu-id="a3062-109">NuGet 패키지를 만드는 방법에는 크게 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-109">There are two main ways to create a NuGet package.</span></span> <span data-ttu-id="a3062-110">최신 및 권장되는 방법은 SDK 스타일 프로젝트(콘텐츠가 `<Project Sdk="Microsoft.NET.Sdk">`로 시작하는 프로젝트 파일)에서 패키지를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-110">The newer and recommended way is to create a package from a SDK-style project (project file whose content starts with `<Project Sdk="Microsoft.NET.Sdk">`).</span></span> <span data-ttu-id="a3062-111">어셈블리 및 대상은 패키지에 자동으로 추가되고, 패키지 이름 및 버전 번호와 같은 나머지 메타데이터는 MSBuild 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-111">Assemblies and targets are automatically added to the package and remaining metadata is added to the MSBuild file, like package name and version number.</span></span> <span data-ttu-id="a3062-112">[`dotnet pack`](../../core/tools/dotnet-pack.md) 명령을 사용하여 컴파일하면 어셈블리 대신 `*.nupkg` 파일이 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-112">Compiling with the [`dotnet pack`](../../core/tools/dotnet-pack.md) command outputs a `*.nupkg` file instead of assemblies.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <AssemblyName>Contoso.Api</AssemblyName>
    <PackageVersion>1.1.0</PackageVersion>
    <Authors>John Doe</Authors>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="a3062-113">NuGet 패키지를 만드는 이전 방법은 `*.nuspec` 파일 및 `nuget.exe` 명령줄 도구를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-113">The older way of creating a NuGet package is with a `*.nuspec` file and the `nuget.exe` command-line tool.</span></span> <span data-ttu-id="a3062-114">nuspec 파일을 사용하면 제어 기능이 향상되지만 최종 NuGet 패키지에 포함할 어셈블리 및 대상을 신중하게 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-114">A nuspec file gives you great control but you must carefully specify what assemblies and targets to include in the final NuGet package.</span></span> <span data-ttu-id="a3062-115">실수하거나, 다른 사람이 변경할 때 nuspec 업데이트를 잊어버리기 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-115">It's easy to make a mistake or for someone to forget to update the nuspec when making changes.</span></span> <span data-ttu-id="a3062-116">nuspec의 장점은 아직 SDK 스타일 프로젝트 파일을 지원하지 않는 프레임워크에 대한 NuGet 패키지를 만드는 데 사용할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-116">The advantage of a nuspec is you can use it create NuGet packages for frameworks that don't yet support an SDK-style project file.</span></span>

<span data-ttu-id="a3062-117">**✔** SDK 스타일 프로젝트 파일을 사용하여 NuGet 패키지를 만드세요.</span><span class="sxs-lookup"><span data-stu-id="a3062-117">**✔️ CONSIDER** using an SDK-style project file to create the NuGet package.</span></span>

<span data-ttu-id="a3062-118">**✔️** SourceLink를 설정하여 어셈블리 및 NuGet 패키지에 소스 제어 메타데이터를 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="a3062-118">**✔️ CONSIDER** setting up SourceLink to add source control metadata to your assemblies and NuGet package.</span></span>

## <a name="package-dependencies"></a><span data-ttu-id="a3062-119">패키지 종속성</span><span class="sxs-lookup"><span data-stu-id="a3062-119">Package dependencies</span></span>

<span data-ttu-id="a3062-120">NuGet 패키지 종속성은 [종속성](./dependencies.md) 문서에서 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-120">NuGet package dependencies are covered in detail in the [Dependencies](./dependencies.md) article.</span></span>

## <a name="important-nuget-package-metadata"></a><span data-ttu-id="a3062-121">중요 NuGet 패키지 메타데이터</span><span class="sxs-lookup"><span data-stu-id="a3062-121">Important NuGet package metadata</span></span>

<span data-ttu-id="a3062-122">NuGet 패키지는 많은 [메타데이터 속성](/nuget/reference/nuspec)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-122">A NuGet package supports many [metadata properties](/nuget/reference/nuspec).</span></span> <span data-ttu-id="a3062-123">다음 표에는 모든 오픈 소스 프로젝트에서 제공해야 하는 핵심 메타데이터가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-123">The following table contains the core metadata that every open-source project should provide:</span></span>

| <span data-ttu-id="a3062-124">MSBuild 속성 이름</span><span class="sxs-lookup"><span data-stu-id="a3062-124">MSBuild Property name</span></span>              | <span data-ttu-id="a3062-125">Nuspec 이름</span><span class="sxs-lookup"><span data-stu-id="a3062-125">Nuspec name</span></span>              | <span data-ttu-id="a3062-126">설명</span><span class="sxs-lookup"><span data-stu-id="a3062-126">Description</span></span>  |
| ---------------------------------- | ------------------------ | ------------ |
| `PackageId`                        | `id`                       | <span data-ttu-id="a3062-127">패키지 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-127">The package identifier.</span></span> <span data-ttu-id="a3062-128">[조건](/nuget/reference/id-prefix-reservation)을 충족하는 경우 식별자의 접두사를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-128">A prefix from the identifier can be reserved if it meets the [criteria](/nuget/reference/id-prefix-reservation).</span></span> |
| `PackageVersion`                   | `version`                  | <span data-ttu-id="a3062-129">NuGet 패키지 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-129">NuGet package version.</span></span> <span data-ttu-id="a3062-130">자세한 내용은 [NuGet 패키지 버전](./versioning.md#nuget-package-version)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a3062-130">For more information, see [NuGet package version](./versioning.md#nuget-package-version).</span></span>             |
| `Title`                            | `title`                    | <span data-ttu-id="a3062-131">패키지의 제목입니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-131">A human-friendly title of the package.</span></span> <span data-ttu-id="a3062-132">기본값은 `PackageId`입니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-132">It defaults to the `PackageId`.</span></span>             |
| `Description`                      | `description`              | <span data-ttu-id="a3062-133">UI에 표시되는, 패키지에 대한 자세한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-133">A long description of the package displayed in UI.</span></span>             |
| `Authors`                          | `authors`                  | <span data-ttu-id="a3062-134">nuget.org의 프로필 이름과 일치하는 패키지 작성자의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-134">A comma-separated list of package authors, matching the profile names on nuget.org.</span></span>             |
| `PackageTags`                      | `tags`                     | <span data-ttu-id="a3062-135">패키지를 설명하는 태그 및 키워드의 공백으로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-135">A space-delimited list of tags and keywords that describe the package.</span></span> <span data-ttu-id="a3062-136">태그는 패키지를 검색할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-136">Tags are used when searching for packages.</span></span>             |
| `PackageIconUrl`                   | `iconUrl`                  | <span data-ttu-id="a3062-137">패키지의 아이콘으로 사용할 이미지의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-137">A URL for an image to use as the icon for the package.</span></span> <span data-ttu-id="a3062-138">URL은 HTTPS여야 하며, 이미지는 64x64이고 투명한 배경을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-138">URL should be HTTPS and the image should be 64x64 and have a transparent background.</span></span>             |
| `PackageProjectUrl`                | `projectUrl`               | <span data-ttu-id="a3062-139">프로젝트 홈페이지 또는 소스 리포지토리의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-139">A URL for the project homepage or source repository.</span></span>             |
| `PackageLicenseUrl`                | `licenseUrl`               | <span data-ttu-id="a3062-140">프로젝트 라이선스의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-140">A URL to the project license.</span></span> <span data-ttu-id="a3062-141">소스 제어의 `LICENSE` 파일에 대한 URL일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-141">Can be the URL to the `LICENSE` file in source control.</span></span>             |

<span data-ttu-id="a3062-142">**✔️** NuGet의 접두사 예약 [조건](/nuget/reference/id-prefix-reservation)을 충족하는 접두사를 가진 NuGet 패키지 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-142">**✔️ CONSIDER** choosing a NuGet package name with a prefix that meets NuGet's prefix reservation [criteria](/nuget/reference/id-prefix-reservation).</span></span>

<span data-ttu-id="a3062-143">**✔️** 소스 제어의 `LICENSE` 파일을 `LicenseUrl`로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-143">**✔️ CONSIDER** using the `LICENSE` file in source control as the `LicenseUrl`.</span></span> <span data-ttu-id="a3062-144">예를 들어 [LICENSE.md](https://github.com/JamesNK/Newtonsoft.Json/blob/c4af75c8e91ca0d75aa6c335e8c106780c4f7712/LICENSE.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-144">For example, [LICENSE.md](https://github.com/JamesNK/Newtonsoft.Json/blob/c4af75c8e91ca0d75aa6c335e8c106780c4f7712/LICENSE.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3062-145">라이선스가 없는 프로젝트의 기본값은 [배타적 저작권](https://choosealicense.com/no-permission/)으로 설정되므로 다른 사용자는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-145">A project without a license defaults to [exclusive copyright](https://choosealicense.com/no-permission/), making it impossible for other people to use.</span></span>

<span data-ttu-id="a3062-146">**✔️** 패키지 아이콘에 대한 HTTPS href를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-146">**✔️ DO** use an HTTPS href to your package icon.</span></span>

> <span data-ttu-id="a3062-147">HTTPS를 사용하여 실행되고 HTTPS가 아닌 이미지를 표시하는 NuGet.org 등의 사이트는 혼합 콘텐츠 경고를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-147">Sites like NuGet.org run with HTTPS enabled and displaying a non-HTTPS image will create a mixed content warning.</span></span>

<span data-ttu-id="a3062-148">**✔️** 보기 결과를 최적화하기 위해 64x64이고 투명한 배경을 가진 패키지 아이콘 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-148">**✔️ DO** use a package icon image that is 64x64 and has a transparent background for best viewing results.</span></span>

## <a name="pre-release-packages"></a><span data-ttu-id="a3062-149">시험판 패키지</span><span class="sxs-lookup"><span data-stu-id="a3062-149">Pre-release packages</span></span>

<span data-ttu-id="a3062-150">버전 접미사가 있는 NuGet 패키지는 [시험판](/nuget/create-packages/prerelease-packages)으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-150">NuGet packages with a version suffix are considered [pre-release](/nuget/create-packages/prerelease-packages).</span></span> <span data-ttu-id="a3062-151">기본적으로 NuGet 패키지 관리자 UI는 사용자가 시험판 패키지를 옵트인하지 않는 한 안정적인 릴리스를 표시하므로, 시험판 패키지는 제한된 사용자 테스트에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-151">By default, the NuGet Package Manager UI shows stable releases unless a user opts-in to pre-release packages, making pre-release packages ideal for limited user testing.</span></span>

```xml
<PackageVersion>1.0.1-beta1</PackageVersion>
```

> [!NOTE]
> <span data-ttu-id="a3062-152">안정적인 패키지는 시험판 패키지에 종속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-152">A stable package cannot depend on a pre-release package.</span></span> <span data-ttu-id="a3062-153">사용자 고유의 패키지를 시험판으로 설정하거나 이전의 안정적인 버전에 종속되도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-153">You must either make your own package pre-release or depend on an older stable version.</span></span>

<span data-ttu-id="a3062-154">![NuGet 시험판 패키지 종속성](./media/nuget/nuget-prerelease-package.png "NuGet 시험판 패키지 종속성")</span><span class="sxs-lookup"><span data-stu-id="a3062-154">![NuGet pre-release package dependency](./media/nuget/nuget-prerelease-package.png "NuGet pre-release package dependency")</span></span>

<span data-ttu-id="a3062-155">**✔️** 테스트, 미리 보기 또는 실험 시에는 시험판 패키지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-155">**✔️ DO** publish a pre-release package when testing, previewing, or experimenting.</span></span>

<span data-ttu-id="a3062-156">**✔️** 준비가 되면 안정적인 패키지를 게시하여 다른 안정적인 패키지가 참조할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-156">**✔️ DO** publish a stable package when its ready so other stable packages can reference it.</span></span>

## <a name="symbol-packages"></a><span data-ttu-id="a3062-157">기호 패키지</span><span class="sxs-lookup"><span data-stu-id="a3062-157">Symbol packages</span></span>

<span data-ttu-id="a3062-158">기호 파일(`*.pdb`)은 어셈블리와 함께 .NET 컴파일러에서 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-158">Symbol files (`*.pdb`) are produced by the .NET compiler alongside assemblies.</span></span> <span data-ttu-id="a3062-159">기호 파일은 실행 위치를 원래 소스 코드에 매핑하므로, 디버거를 사용하여 실행 중인 소스 코드를 한 단계씩 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-159">Symbol files map execution locations to the original source code so you can step through source code as it is running using a debugger.</span></span> <span data-ttu-id="a3062-160">NuGet은 .NET 어셈블리를 포함하는 주 패키지와 함께 기호 파일을 포함하는 [별도의 기호 패키지 생성](/nuget/create-packages/symbol-packages)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-160">NuGet supports [generating a separate symbol package](/nuget/create-packages/symbol-packages) containing symbol files alongside the main package containing .NET assemblies.</span></span> <span data-ttu-id="a3062-161">기호 패키지는 기호 서버에서 호스트되며 요청 시 Visual Studio와 같은 도구에서만 다운로드되도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-161">The idea of symbol packages is they're hosted on a symbol server and are only downloaded by a tool like Visual Studio on demand.</span></span>

<span data-ttu-id="a3062-162">현재, 기호의 기본 공용 호스트인 [SymbolSource](http://www.symbolsource.org/)는 SDK 스타일 프로젝트에서 생성되는 새로운 [이식 가능한 기호 파일](https://github.com/dotnet/core/blob/master/Documentation/diagnostics/portable_pdb.md)(`*.pdb`)을 지원하지 않으며, 기호 패키지가 유용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-162">Currently the main public host for symbols - [SymbolSource](http://www.symbolsource.org/) - doesn't support the new [portable symbol files](https://github.com/dotnet/core/blob/master/Documentation/diagnostics/portable_pdb.md) (`*.pdb`) created by SDK-style projects, and symbol packages aren't useful.</span></span> <span data-ttu-id="a3062-163">기호 패키지에 대한 권장 호스트가 있을 때까지 기호 파일을 기본 NuGet 패키지에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-163">Until there is a recommended host for symbol packages, symbol files can be embedded in the main NuGet package.</span></span> <span data-ttu-id="a3062-164">SDK 스타일 프로젝트를 사용하여 NuGet 패키지를 빌드하는 경우 `AllowedOutputExtensionsInPackageBuildOutputFolder` 속성을 설정하여 기호 파일을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-164">If you are building your NuGet package using an SDK-style project you can embed symbol files by setting the `AllowedOutputExtensionsInPackageBuildOutputFolder` property:</span></span> 

```xml
<Project Sdk="Microsoft.NET.Sdk">
 <PropertyGroup>
    <!-- Include symbol files (*.pdb) in the built .nupkg -->
    <AllowedOutputExtensionsInPackageBuildOutputFolder>$(AllowedOutputExtensionsInPackageBuildOutputFolder);.pdb</AllowedOutputExtensionsInPackageBuildOutputFolder>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="a3062-165">**✔️** 기호 파일을 기본 NuGet 패키지에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-165">**✔️ CONSIDER** embedding symbol files in the main NuGet package.</span></span>

<span data-ttu-id="a3062-166">**❌** 기호 파일을 포함하는 기호 패키지를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a3062-166">**❌ AVOID** creating a symbols package containing symbol files.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="a3062-167">[이전](./strong-naming.md)
[다음](./dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="a3062-167">[Previous](./strong-naming.md)
[Next](./dependencies.md)</span></span>