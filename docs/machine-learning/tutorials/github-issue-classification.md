---
title: GitHub 문제 다중 클래스 분류 시나리오에서 ML.NET 사용
description: 다중 클래스 분류 시나리오에서 ML.NET을 사용하여 GitHub 문제를 분류하여 지정된 영역에 할당하는 방법을 알아봅니다.
ms.date: 01/24/2019
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 6f01357906fd4398f68dadfb35dbce816f4302c0
ms.sourcegitcommit: d9a0071d0fd490ae006c816f78a563b9946e269a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55066209"
---
# <a name="tutorial-use-mlnet-in-a-multiclass-classification-scenario-to-classify-github-issues"></a>자습서: 다중 클래스 분류 시나리오에서 ML.NET을 사용하여 GitHub 문제를 분류합니다.

이 샘플 자습서에서는 ML.NET을 사용하여 Visual Studio 2017에서 C#을 사용하는 .NET Core 콘솔 애플리케이션을 통해 GitHub 문제 분류자를 만드는 방법에 대해 설명합니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.
> [!div class="checklist"]
> * 문제 이해
> * 적절한 기계 학습 작업 선택
> * 데이터 준비
> * 학습 파이프라인 만들기
> * 분류자 로드
> * 모델 학습
> * 다른 데이터 세트를 사용하여 모델 평가
> * 모델을 사용하여 테스트 데이터 결과의 단일 인스턴스 예측
> * 로드된 모델을 사용하여 테스트 데이터 결과 예측

> [!NOTE]
> 이 항목은 현재 미리 보기로 제공되는 ML.NET을 참조하며, 자료는 변경될 수 있습니다. 자세한 내용은 [ML.NET 소개](https://www.microsoft.com/net/learn/apps/machine-learning-and-ai/ml-dotnet)를 참조하세요.

## <a name="github-issue-sample-overview"></a>GitHub 문제 샘플 개요

샘플은 ML.NET을 사용하여 GitHub 문제에 대한 영역 레이블을 분류하고 예측하는 모델을 학습시키는 콘솔 앱입니다. 또한 품질 분석을 위해 두 번째 데이터 세트를 사용하여 모델을 평가합니다. 문제 데이터 세트는 dotnet/corefx GitHub 리포지토리에서 가져온 것입니다.

## <a name="prerequisites"></a>전제 조건

* “.NET Core 플랫폼 간 개발” 워크로드가 설치된 [Visual Studio 2017 15.6 이상](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).

* [Github에서 탭 분리 파일(issues_train.tsv)](https://github.com/dotnet/samples/machine-learning/tutorials/GitHubIssueClassification/Data/issues_train.tsv)을 발행합니다.
* [Github에서 테스트 탭 분리 파일(issues_test.tsv)](https://github.com/dotnet/samples/machine-learning/tutorials/GitHubIssueClassification/Data/issues_test.tsv)을 발행합니다.

## <a name="machine-learning-workflow"></a>기계 학습 워크플로

이 자습서는 프로세스가 체계적으로 이동할 수 있도록 하는 기계 학습 워크플로를 따릅니다.

워크플로 단계는 다음과 같습니다.

1. **문제 이해**
2. **데이터 준비**
   * **데이터 로드**
   * **기능 추출(데이터 변환)**
3. **빌드 및 학습** 
   * **모델 학습**
   * **모델 평가**
4. **실행**
   * **모델 사용**

### <a name="understand-the-problem"></a>문제 이해

먼저 문제를 이해해야 하므로 모델 빌드 및 학습을 지원할 수 있는 부분으로 문제를 구분할 수 있습니다. 문제를 구분하면 결과를 예측하고 평가할 수 있습니다.

이 자습서의 문제점은 들어오는 GitHub 문제가 속해 있는 영역을 이해하여 우선순위 지정 및 스케줄링을 위해 올바르게 레이블을 지정하는 것입니다.

다음과 같이 문제를 구분할 수 있습니다.

* 문제 제목 텍스트
* 문제 설명 텍스트
* 모델 학습 데이터에 대한 영역 값
* 평가한 다음, 작동 가능하게 사용할 수 있는 예측된 영역 값

그런 다음, 기계 학습 작업 선택에 도움이 되는 영역을 **확인**해야 합니다.

## <a name="select-the-appropriate-machine-learning-task"></a>적절한 기계 학습 작업 선택

이 문제에서 다음 사실을 알 수 있습니다.

학습 데이터:

다음 예제와 같이 GitHub 문제는 여러 영역(**Area**)에 레이블을 지정할 수 있습니다.

* area-System.Numerics
* area-System.Xml
* area-Infrastructure
* area-System.Linq
* area-System.IO

다음 예제와 같이 새 GitHub 문제의 **영역**을 예측합니다.

* Contract.Assert 대 Debug.Assert
* System.Xml에서 읽기 전용으로 필드 만들기

분류 기계 학습 작업이 이 시나리오에 가장 적합합니다.

### <a name="about-the-classification-task"></a>분류 작업 정보

분류는 데이터를 사용하여 데이터 항목 또는 행의 범주, 형식 또는 클래스를 **확인**하는 기계 학습 작업입니다. 예를 들어 분류를 사용하여 다음을 수행할 수 있습니다.

* 감정을 긍정적 또는 부정적으로 식별합니다.
* 전자 메일을 스팸, 정크 또는 정상으로 분류합니다.
* 환자의 실험실 샘플이 종양성인지 확인합니다.
* 영업 캠페인에 응답하는 고객의 성향을 기준으로 고객을 분류합니다.

일반적으로 분류 작업은 다음 형식 중 하나입니다.

* 이진: A 또는 B.
* 다중 클래스: 단일 모델을 사용하여 예측할 수 있는 여러 범주.

## <a name="create-a-console-application"></a>콘솔 애플리케이션 만들기

### <a name="create-a-project"></a>프로젝트 만들기

1. Visual Studio 2017을 엽니다. 메뉴 모음에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다. **새 프로젝트** 대화 상자에서 **Visual C#** 노드와 **.NET Core** 노드를 차례로 선택합니다. 그런 다음 **콘솔 앱(.NET Core)** 프로젝트 템플릿을 선택합니다. **이름** 텍스트 상자에 “SentimentAnalysis”를 입력한 다음, **확인** 단추를 선택합니다.

2. 프로젝트에서 *Data* 디렉터리를 만들어 데이터 집합 파일을 저장합니다.

    **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 폴더**를 선택합니다. “Data”를 입력하고 Enter 키를 누릅니다.

3. **Microsoft.ML NuGet 패키지**를 설치합니다.

    솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다. “nuget.org”를 패키지 소스로 선택하고, [찾아보기] 탭을 선택하고, **Microsoft.ML**을 검색하고, 목록에서 해당 패키지를 선택하고, **설치** 단추를 선택합니다. **변경 내용 미리 보기** 대화 상자에서 **확인** 단추를 선택한 다음, 나열된 패키지의 사용 조건에 동의하는 경우 **라이선스 승인** 대화 상자에서 **동의함** 단추를 선택합니다.

### <a name="prepare-your-data"></a>데이터 준비

1. [issues-train.csv](https://github.com/dotnet/samples/machine-learning/tutorials/GitHubIssueClassification/Data/issues_train.tsv) 및 [issues-test.tsv](https://github.com/dotnet/samples/machine-learning/tutorials/GitHubIssueClassification/Data/issues_test.tsv) 데이터 세트를 다운로드하여 이전에 만든 *Data* 폴더에 저장합니다. 첫 번째 데이터 세트는 기계 학습 모델을 교육하고 두 번째 데이터 세트는 모델이 얼마나 정확한지 평가하는 데 사용할 수 있습니다.

2. 솔루션 탐색기에서 각 \*.tsv 파일을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **고급** 아래에서 **출력 디렉터리에 복사** 값을 **변경된 내용만 복사**로 변경합니다.

### <a name="create-classes-and-define-paths"></a>클래스 만들기 및 경로 정의

*Program.cs* 파일 맨 위에 다음 추가 `using` 문을 추가합니다.

[!code-csharp[AddUsings](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#AddUsings)]

최근에 다운로드한 파일의 경로와 `TextLoader`의 전역 변수가 포함될 세 개의 전역 필드를 만들어야 합니다.

* `_trainDataPath`에는 모델을 학습시키는 데 사용되는 데이터 세트의 경로가 포함됩니다.
* `_testDataPath`에는 모델을 평가하는 데 사용되는 데이터 세트의 경로가 포함됩니다.
* `_modelPath`에는 학습된 모델이 저장되는 경로가 포함됩니다.
* `_mlContext`는 처리 컨텍스트를 제공하는 <xref:Microsoft.ML.MLContext>입니다.
* `_trainingDataView`는 학습 데이터 세트를 처리하는 데 사용되는 <xref:Microsoft.ML.Data.IDataView>입니다.
* `_predEngine`은 단일 예측에 사용되는 <xref:Microsoft.ML.PredictionEngine%602>입니다.
* `_reader`는 데이터 세트를 로드하고 변환하는 데 사용되는 <xref:Microsoft.ML.Data.TextLoader>입니다.

`Main` 메서드 바로 위의 줄에 다음 코드를 추가하여 해당 경로와 다른 변수를 지정합니다.

[!code-csharp[DeclareGlobalVariables](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#DeclareGlobalVariables)]

입력 데이터 및 예측에 대한 일부 클래스를 만들어야 합니다. 새 클래스를 프로젝트에 추가합니다.

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **새 항목**을 선택합니다.

1. **새 항목 추가** 대화 상자에서 **클래스**를 선택하고 **이름** 필드를 *GitHubIssueData.cs*로 변경합니다. 그런 다음, **추가** 단추를 선택합니다.

    *GitHubIssueData.cs* 파일이 코드 편집기에서 열립니다. 다음 `using` 문을 *GitHubIssueData.cs*의 맨 위에 추가합니다.

[!code-csharp[AddUsings](../../../samples/machine-learning/tutorials/GitHubIssueClassification/GitHubIssueData.cs#AddUsings)]

기존 클래스 정의를 제거하고 두 개의 클래스 `GitHubIssue` 및 `IssuePrediction`이 있는 다음 코드를 *GitHubIssueData.cs* 파일에 추가합니다.

[!code-csharp[DeclareTypes](../../../samples/machine-learning/tutorials/GitHubIssueClassification/GitHubIssueData.cs#DeclareTypes)]

`GitHubIssue`는 다음 입력 데이터 세트 클래스이며 다음 <xref:System.String> 필드를 포함합니다.

* `ID`에 GitHub 문제 ID에 대한 값 포함
* `Area`에 `Area` 레이블에 대한 값 포함
* `Title`에 GitHub 문제 제목 포함
* `Description`에 GitHub 문제 설명 포함

`IssuePrediction`은 모델이 학습된 후 예측에 사용되는 클래스입니다. 여기에는 단일 `string`(`Area`) 및 `PredictedLabel` `ColumnName` 특성이 포함됩니다. `Label`은 세트를 만들고 학습시키는 데 사용되며 두 번째 데이터 세트와 함께 모델을 평가하는 데도 사용됩니다. `PredictedLabel`은 예측 및 평가 중에 사용됩니다. 평가를 위해 학습 데이터가 있는 입력, 예측 값 및 모델이 사용됩니다.

ML.NET를 사용하여 모델을 빌드하는 경우 먼저 <xref:Microsoft.ML.MLContext>를 만듭니다. 이는 Entity Framework에서 `DbContext`를 사용하는 것과 개념이 비슷합니다. 환경은 예외 추적 및 로깅에 사용할 수 있는 ML 작업의 컨텍스트를 제공합니다.

### <a name="initialize-variables-in-main"></a>Main에서 변수 초기화

여러 학습에서 반복 가능한/결정적 결과를 얻기 위해 임의의 시드(`seed: 0`)가 있는 `MLContext`의 새 인스턴스로 `_mlContext` 글로벌 변수를 초기화합니다.  `Main` 메서드에서 `Console.WriteLine("Hello World!")` 줄을 다음 코드로 바꿉니다.

[!code-csharp[CreateMLContext](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CreateMLContext)]

## <a name="load-the-data"></a>데이터 로드

그런 다음, `_trainingDataView` <xref:Microsoft.ML.Data.IDataView> 글로벌 변수 초기화하고 `_trainDataPath` 매개 변수를 사용하여 데이터를 로드합니다.

 `Transforms`의 입력 및 출력으로 사용되는 `DataView`는 `LINQ`의 `IEnumerable`과 비슷한 기본적인 데이터 파이프라인 형식입니다.

ML.NET에서 데이터는 `SQL view`와 유사합니다. 지연 계산되고, 스키마화되며, 형식이 다릅니다. 개체가 파이프라인의 첫 번째 부분이며 데이터를 로드합니다. 이 자습서에서는 문제 제목, 설명 및 해당 영역 GitHub 레이블이 있는 데이터 세트를 로드합니다. `DataView`는 모델을 만들고 학습시키는 데 사용됩니다.

이전에 만든 `GitHubIssue` 데이터 모델 유형이 데이터 세트 스키마와 일치하므로 초기화, 매핑 및 데이터 세트 로드를 한 줄의 코드로 결합할 수 있습니다.

줄의 첫 번재 부분(`CreateTextReader<GitHubIssue>(hasHeader: true)`)에서는 `GitHubIssue` 데이터 모델 유형의 데이터 세트 스키마를 추론하고 데이터 세트 헤더를 사용하여 <xref:Microsoft.ML.Data.TextLoader>를 만듭니다.

이전에 `GitHubIssue` 클래스를 만들 때 데이터 스키마를 정의했습니다. 스키마의 경우:

* 첫 번째 열 `ID`(GitHub 문제 ID)
* 두 번째 열 `Area`(학습 예측)
* 세 번째 열 `Title`(GitHub 문제 제목)은 `Area`를 예측하는 데 사용되는 첫 번째 [기능](../resources/glossary.md##feature)입니다.
* 네 번째 열 `Description`은 `Area`를 예측하는 데 사용되는 두 번째 기능입니다.

줄의 두 번째 부분(`.Read(_trainDataPath)`)에서는 `_trainDataPath`를 통해 `IDataView`(`_trainingDataView`) 글로벌 변수에 학습 텍스트 파일을 로드하는 데 <xref:Microsoft.ML.Data.TextLoader.Read%2A> 메서드를 사용합니다.  

`_trainingDataView` 글로벌 변수를 파이프라인에 사용하기 위해 초기화 및 로드하려면 `mlContext` 초기화 후에 다음 코드를 추가합니다.

[!code-csharp[LoadTrainData](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#LoadTrainData)]


`Main` 메서드에 아래 코드를 다음 코드 줄로 추가합니다.

[!code-csharp[CallProcessData](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CallProcessData)]

`ProcessData` 메서드는 다음 작업을 실행합니다.

* 데이터를 추출하고 변환합니다.
* 처리 파이프라인을 반환합니다.

다음 코드를 사용하여 `Main` 메서드 바로 뒤에 `ProcessData` 메서드를 만듭니다.

```csharp
public static EstimatorChain<ITransformer> ProcessData()
{

}
```

## <a name="extract-and-transform-the-data"></a>데이터 추출 및 변환

데이터 전처리 및 정리는 데이터 세트가 기계 학습에 효과적으로 사용되기 전에 수행되는 중요한 작업입니다. 원시 데이터는 종종 정리되지 않고 불안정하며 값이 누락될 수 있습니다. 이러한 모델링 작업 없이 데이터를 사용하면 잘못된 결과를 얻을 수 있습니다.

ML.NET의 변환 파이프라인은 학습 또는 테스트 전에 데이터에 적용되는 사용자 지정 변환 세트로 구성됩니다. 변환의 기본 목적은 데이터 [기능화](../resources/glossary.md#feature-engineering)입니다. 기계 학습 알고리즘은 [기능화된](../resources/glossary.md#feature) 데이터를 인식하므로 다음 단계는 텍스트 데이터를 ML 알고리즘이 인식하는 형식으로 변환하는 것입니다. 해당 형식은 [숫자 벡터](../resources/glossary.md#numerical-feature-vector)입니다.

다음 단계에서는 `GitHubIssue` 클래스에 정의된 이름으로 해당 열을 참조합니다.

모델을 학습하고 평가할 때 기본적으로 **Label** 열의 값이 예측할 올바른 값으로 간주됩니다. `GitHubIssue`에 대한 Area GitHub 레이블을 예측하려면 `Area` 열을 **Label** 열로 복사합니다. 이렇게 하려면 <xref:Microsoft.ML.ConversionsExtensionsCatalog.MapValueToKey%2A> 변환 클래스의 래퍼인 `MLContext.Transforms.Conversion.MapValueToKey`를 사용합니다.  `MapValueToKey`는 실제로 파이프라인이 될 <xref:Microsoft.ML.Data.EstimatorChain%601>을 반환합니다. 이 학습자를 `EstimatorChain`에 추가할 때 `pipeline`으로 이름을 지정합니다. 아래 코드를 다음 코드 줄로 추가합니다.

[!code-csharp[MapValueToKey](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#MapValueToKey)]

모델을 학습하는 알고리즘은 **숫자** 기능이 필요하므로, 다음으로 `mlContext.Transforms.Text.FeaturizeText`를 호출하여 텍스트(`Title` 및 `Description`) 열을 각각 `TitleFeaturized` 및 `DescriptionFeaturized`라는 숫자 벡터로 기능화합니다. 기능화는 각 열의 다른 값에 서로 다른 숫자 키 값을 할당하고 기계 학습 알고리즘에서 사용됩니다.
다음 코드를 사용하여 두 열에 대한 기능화(featurization)를 파이프라인에 추가합니다.

[!code-csharp[FeaturizeText](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#FeaturizeText)]

데이터 준비의 마지막 단계에서는 `Concatenate` 변환 클래스를 사용하여 모든 기능 열을 **Features** 열에 결합합니다. 기본적으로, 학습 알고리즘은 **Features** 열의 기능만 처리합니다. 다음 코드를 사용하여 이 변환을 파이프라인에 추가합니다.

[!code-csharp[Concatenate](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#Concatenate)]

 그런 다음, <xref:Microsoft.ML.Data.EstimatorChain`1.AppendCacheCheckpoint%2A>를 추가하여 DataView를 여러 번 캐시합니다. 따라서 캐시를 사용하여 데이터를 여러 번 반복할 때 다음 코드와 같이 성능이 향상될 수 있습니다.

[!code-csharp[AppendCache](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#AppendCache)]

`ProcessData` 메서드의 끝에 파이프라인을 반환합니다.

[!code-csharp[ReturnPipeline](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#ReturnPipeline)]

이 단계는 전처리/기능화를 처리합니다. ML.NET에서 사용 가능한 추가 구성 요소를 사용하면 모델에서 더 나은 결과를 얻을 수 있습니다.

## <a name="build-and-train-the-model"></a>모델 빌드 및 학습

`BuildAndTrainModel` 메서드에 다음 호출을 `Main` 메서드의 다음 코드 줄로 추가합니다.

[!code-csharp[CallBuildAndTrainModel](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CallBuildAndTrainModel)]

`BuildAndTrainModel` 메서드는 다음 작업을 실행합니다.

* 학습 알고리즘 클래스를 만듭니다.
* 모델을 학습시킵니다.
* 학습 데이터를 기반으로 영역을 예측합니다.
* 모델을 `.zip` 파일에 저장합니다.
* 모델을 반환합니다.

다음 코드를 사용하여 `Main` 메서드 바로 뒤에 `BuildAndTrainModel` 메서드를 만듭니다.

```csharp
public static void BuildAndTrainModel()
{

}
```

BuildAndTrainModel 메서드에는 학습 데이터 세트(`trainingDataView`)에 대한 `IDataView` 및 ProcessData(`pipeline`)에서 만든 처리 파이프라인에 대한 <xref:Microsoft.ML.Data.EstimatorChain%601>이라는 두 개의 매개 변수가 전달됩니다.

 다음 코드를 `BuildAndTrainModel` 메서드의 첫 번째 줄로 추가합니다.

### <a name="choose-a-trainer-algorithm"></a>강사 알고리즘 선택

강사 알고리즘을 추가하려면 <xref:Microsoft.ML.Trainers.SdcaMultiClassTrainer> 개체를 반환하는 `mlContext.Transforms.Text.FeaturizeText` 래퍼 메서드를 호출합니다. 이 개체는 이 파이프라인에서 사용할 의사 결정 트리 학습자입니다. `SdcaMultiClassTrainer`는 `pipeline`에 추가되고 기록 데이터에서 학습할 기능화된 `Title`, `Description`(`Features`) 및 `Label` 입력 매개 변수를 수락합니다.

`BuildAndTrainModel` 메서드에 다음 코드를 추가합니다.

[!code-csharp[SdcaMultiClassTrainer](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#SdcaMultiClassTrainer)]

이제 강사 알고리즘을 만들었으므로 `pipeline`에 추가합니다. 또한 레이블을 원래 읽기 가능한 상태로 반환하려면 값에 매핑해야 합니다. 다음 코드를 사용하여 해당 작업 모두를 수행합니다.

[!code-csharp[AddTrainer](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#AddTrainer)]

### <a name="train-the-model"></a>모델 학습

로드되고 변환된 데이터 세트를 기반으로 <xref:Microsoft.ML.Data.TransformerChain%601> 모델을 학습시킵니다. 추정기가 정의된 후, 이미 로드된 학습 데이터를 제공하는 동시에 <xref:Microsoft.ML.Data.EstimatorChain%601.Fit%2A>을 사용하여 모델을 학습시킵니다. 그러면 예측에 사용할 모델이 반환됩니다. `trainingPipeline.Fit()`은 파이프라인을 학습시키고, 전달된 `DataView`에 따라 `Transformer`를 반환합니다. 이 문제가 발생할 때까지 실험이 실행되지 않습니다.

`BuildAndTrainModel` 메서드에 다음 코드를 추가합니다.

[!code-csharp[TrainModel](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#TrainModel)]

`model`은 여러 데이터 행에서 작동하는 `transformer`이지만, 일반적인 프로덕션 시나리오에서는 개별 예제에 대한 예측이 필요합니다. <xref:Microsoft.ML.PredictionEngine%602>은 `CreatePredictionEngine` 메서드에서 반환되는 래퍼입니다. 다음 코드를 추가하여 `PredictionEngine`을 `BuildAndTrainModel` 메서드의 다음 줄로 만듭니다.

[!code-csharp[CreatePredictionEngine](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CreatePredictionEngine)]

`GitHubIssue`의 인스턴스를 만들어 GitHub 문제를 추가하여 `Predict` 메서드에서 학습된 모델의 예측을 테스트합니다.

[!code-csharp[CreateTestIssue1](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CreateTestIssue1)]

문제 데이터의 단일 인스턴스에 대한 `Area` 레이블을 예측하는 데 사용할 수 있습니다. 예측을 가져오려면 데이터에 대해 <xref:Microsoft.ML.PredictionEngine%602.Predict%2A>을 사용합니다. 입력 데이터는 문자열이고 모델은 기능화를 포함합니다. 파이프라인은 학습 및 예측 중에 동기화됩니다. 특별히 예측을 위해 전처리/기능화 코드를 작성할 필요가 없고 동일한 API가 배치 및 일회성 예측을 둘 다 처리합니다.

[!code-csharp[Predict](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#Predict)]

### <a name="model-operationalization-prediction"></a>모델 연산화: 예측

결과를 공유하고 이에 따라 작업을 수행하기 위해 `GitHubIssue` 및 해당 `Area` 레이블 예측을 표시합니다. 이것을 반환된 데이터를 운영 정책의 일부로 사용하는 연산화라고 합니다. 다음 <xref:System.Console.WriteLine?displayProperty=nameWithType> 코드를 사용하여 결과 표시를 만듭니다.

[!code-csharp[OutputPrediction](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#OutputPrediction)]

### <a name="save-and-return-the-model-trained-to-use-for-evaluation"></a>평가에 사용하기 위해 학습된 모델 저장 및 반환

이 시점에는 기존 또는 새 .NET 애플리케이션에 통합할 수 있는 <xref:Microsoft.ML.Data.TransformerChain%601> 형식의 모델이 있습니다. 학습된 모델을 .zip 파일로 저장하려면 다음 코드를 추가하여 `SaveModelAsFile` 메서드를 `BuildAndTrainModel`에 다음 줄로 호출합니다.

[!code-csharp[CallSaveModel](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CallSaveModel)]

`BuildAndTrainModel` 메서드의 끝에 모델을 반환합니다.

[!code-csharp[ReturnModel](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#ReturnModel)]

## <a name="save-the-model-as-azip-file"></a>모델을 .zip 파일로 저장

다음 코드를 사용하여 `BuildAndTrainModel` 메서드 바로 뒤에 `SaveModelAsFile` 메서드를 만듭니다.

```csharp
private static void SaveModelAsFile(MLContext mlContext, ITransformer model)
{

}
```

`SaveModelAsFile` 메서드는 다음 작업을 실행합니다.

* 모델을 .zip 파일로 저장합니다.

다음으로, 다른 애플리케이션에서 다시 사용하고 이용할 수 있도록 모델을 저장하는 메서드를 만듭니다. `ITransformer`에는 `_modelPath` 전역 필드를 사용하는 <xref:Microsoft.ML.Data.TransformerChain%601.SaveTo(Microsoft.ML.IHostEnvironment,System.IO.Stream)> 메서드와 <xref:System.IO.Stream>이 있습니다. 이 파일을 zip 파일로 저장하기 위해 `SaveTo` 메서드를 호출하기 직전에 `FileStream`을 만들겠습니다. `SaveModelAsFile` 메서드에 아래 코드를 다음 줄로 추가합니다.

[!code-csharp[SaveModel](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#SaveModel)]

다음 코드를 사용해서 `_modelPath`가 포함된 콘솔 메시지를 작성하여 파일이 작성된 위치를 표시할 수도 있습니다.

```csharp
Console.WriteLine("The model is saved to {0}", _modelPath);
```

## <a name="evaluate-the-model"></a>모델 평가

이제 모델을 만들고 학습시켰으므로 품질 보증 및 유효성 검사를 위해 다른 데이터 세트를 사용하여 평가해야 합니다. `Evaluate` 메서드에서는 `BuildAndTrainModel`에서 만들어진 모델을 전달하여 평가합니다. 다음 코드와 같이 `BuildAndTrainModel` 바로 뒤에 `Evaluate` 메서드를 만듭니다.

```csharp
public static void Evaluate()
{

}
```

`Evaluate` 메서드는 다음 작업을 실행합니다.

* 테스트 데이터 세트를 로드합니다.
* 다중 클래스 평가자를 만듭니다.
* 모델을 평가하고 메트릭을 만듭니다.
* 메트릭을 표시합니다.

다음 코드를 사용하여 `BuildAndTrainModel` 메서드 호출 바로 아래에 `Main` 메서드의 새 메서드 호출을 추가합니다.

[!code-csharp[CallEvaluate](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CallEvaluate)]

이전에 학습 데이터 세트를 사용했을 때처럼 초기화, 매핑 및 테스트 데이터 세트 로드를 하나의 코드 행에 결합할 수 있습니다. 이 데이터 세트를 품질 검사로 사용하여 모델을 평가할 수 있습니다. `Evaluate` 메서드에 다음 코드를 추가합니다.

[!code-csharp[LoadTestDataset](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#LoadTestDataset)]

`MulticlassClassificationContext.Evaluate`는 지정된 데이터 세트를 사용하여 모델의 품질 메트릭을 계산하는 <xref:Microsoft.ML.MulticlassClassificationContext.Evaluate%2A> 메서드의 래퍼입니다. 다중 클래스 분류 평가자가 계산한 전체 메트릭을 포함하는 <xref:Microsoft.ML.Data.MultiClassClassifierMetrics> 개체를 반환합니다.
모델의 품질을 확인하기 위해 이러한 메트릭을 표시하려면 먼저 메트릭을 가져와야 합니다.
기계 학습 `_trainedModel` 글로벌 변수(변환기)의 `Transform` 메서드를 사용하여 기능을 입력하고 예측을 반환합니다. `Evaluate` 메서드에 아래 코드를 다음 줄로 추가합니다.

[!code-csharp[Evaluate](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#Evaluate)]

다중 클래스 분류에 대한 다음 메트릭이 계산됩니다.

* 마이크로 정확도 - 모든 샘플 클래스 쌍은 정확도 메트릭에 동일하게 기여합니다.  마이크로 정확도를 가능한 한 1에 가깝게 합니다.

* 매크로 정확도 - 모든 클래스 정확도 메트릭에 동일하게 기여합니다. 소수 클래스는 큰 클래스와 같은 가중치를 부여받습니다. 매크로 정확도를 가능한 한 1에 가깝게 합니다.

* 로그 손실 - [로그 손실](../resources/glossary.md#log-loss)을 참조하세요. 로그 손실을 가능한 한 0에 가깝게 합니다.

* 로그 손실 감소 - [-inf, 100]의 범위입니다. 여기서 100은 완벽한 예측이고 0은 평균 예측을 나타냅니다. 로그 손실 감소를 가능한 한 0에 가깝게 합니다.

### <a name="displaying-the-metrics-for-model-validation"></a>모델 유효성 검사를 위해 메트릭 표시

다음 코드를 사용하여 메트릭을 표시하고, 결과를 공유한 다음, 작업을 수행합니다.

[!code-csharp[DisplayMetrics](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#DisplayMetrics)]

## <a name="predict-the-test-data-outcome-with-the-saved-model"></a>저장된 모델을 사용하여 테스트 데이터 결과 예측

다음 코드를 사용하여 `Evaluate` 메서드 호출 바로 아래에 `Main` 메서드의 새 메서드 호출을 추가합니다.

[!code-csharp[CallPredictIssue](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CallPredictIssue)]

다음 코드를 사용하여 `Evaluate` 메서드 바로 뒤에 `PredictIssue` 메서드를 만듭니다.

```csharp
private static void PredictIssue()
{

}
```

`PredictIssue` 메서드는 다음 작업을 실행합니다.

* 테스트 데이터의 단일 문제를 만듭니다.
* 테스트 데이터를 기반으로 영역을 예측합니다.
* 보고를 위해 테스트 데이터 및 예측을 결합합니다.
* 예측 결과를 표시합니다.

먼저 다음 코드를 사용하여 이전에 저장한 모델을 로드합니다.

[!code-csharp[LoadModel](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#LoadModel)]

`GitHubIssue`의 인스턴스를 만들어 GitHub 문제를 추가하여 `Predict` 메서드에서 학습된 모델의 예측을 테스트합니다.

[!code-csharp[AddTestIssue](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#AddTestIssue)]

[!code-csharp[CreatePredictionEngine](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CreatePredictionEngine)]
  
이제 모델을 설정했으므로 GitHub 문제 데이터의 단일 인스턴스에 대한 Area GitHub 레이블을 예측하는 데 사용할 수 있습니다. 예측을 가져오려면 데이터에 대해 <xref:Microsoft.ML.PredictionEngine%602.Predict%2A>을 사용합니다. 입력 데이터는 문자열이고 모델은 기능화를 포함합니다. 파이프라인은 학습 및 예측 중에 동기화됩니다. 특별히 예측을 위해 전처리/기능화 코드를 작성할 필요가 없고 동일한 API가 배치 및 일회성 예측을 둘 다 처리합니다. 예측을 위해 `PredictIssue` 메서드에 다음 코드를 추가합니다.

[!code-csharp[PredictIssue](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CreatePredictionEngine)]

### <a name="model-operationalization-prediction"></a>모델 연산화: 예측

문제를 분류하고 이에 따라 조치를 취하기 위해 `Area`를 표시합니다. 이것을 반환된 데이터를 운영 정책의 일부로 사용하는 연산화라고 합니다. 다음 <xref:System.Console.WriteLine?displayProperty=nameWithType> 코드를 사용하여 결과 표시를 만듭니다.

[!code-csharp[DisplayResults](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#DisplayResults)]

## <a name="results"></a>결과

다음과 같은 결과가 나타나야 합니다. 파이프라인이 처리할 때 메시지를 표시합니다. 경고 또는 메시지 처리를 확인할 수 있습니다. 이해하기 쉽도록 이러한 결과는 다음 결과에서 제거되었습니다.

```console
=============== Single Prediction just-trained-model - Result: area-System.Net ===============
The model is saved to C:\Users\johalex\dotnet-samples\samples\machine-learning\tutorials\GitHubIssueClassification\bin\Debug\netcoreapp2.0\..\..\..\Models\model.zip
*************************************************************************************************************
*       Metrics for Multi-class Classification model - Test Data
*------------------------------------------------------------------------------------------------------------
*       MicroAccuracy:    0.74
*       MacroAccuracy:    0.687
*       LogLoss:          .932
*       LogLossReduction: 63.852
*************************************************************************************************************
=============== Single Prediction - Result: area-System.Data ===============
```

지금까지 이제 GitHub 문제의 영역 레이블을 분류하고 예측하기 위한 기계 학습 모델을 성공적으로 빌드했습니다. [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/GitHubIssueClassification) 리포지토리에서 이 자습서의 소스 코드를 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계

본 자습서에서는 다음 작업에 관한 방법을 학습했습니다.
> [!div class="checklist"]
> * 문제 이해
> * 적절한 기계 학습 작업 선택
> * 데이터 준비
> * 학습 파이프라인 만들기
> * 분류자 로드
> * 모델 학습
> * 다른 데이터 세트를 사용하여 모델 평가
> * 모델을 사용하여 테스트 데이터 결과 예측

다음 자습서로 이동하여 자세히 알아보기
> [!div class="nextstepaction"]
> [택시 요금 예측기](taxi-fare.md)