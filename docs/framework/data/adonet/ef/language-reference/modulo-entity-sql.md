---
title: '% (모듈로)(Entity SQL)'
ms.date: 03/30/2017
ms.assetid: 243ddc4f-3c4e-41e1-a3ef-4ed39e36248b
ms.openlocfilehash: 543c35c56955fb0a9909fced23357444bc78197a
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54732598"
---
# <a name="modulo-entity-sql"></a>% (모듈로)(Entity SQL)
한 식을 다른 식으로 나눈 나머지를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
dividend % divisor  
```  
  
## <a name="arguments"></a>인수  
 `dividend`  
 나눌 숫자 식입니다. `dividend` 는 숫자 데이터 형식의 유효한 식입니다.  
  
 `divisor`  
 피제수를 나눌 숫자 식입니다. `divisor` 는 숫자 데이터 형식의 유효한 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 Edm.Int32  
  
## <a name="example"></a>예제  
 다음 Entity SQL 쿼리에서는 % 산술 연산자를 사용하여 한 식을 다른 식으로 나눈 나머지를 반환합니다. 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다. 이 쿼리를 컴파일하고 실행하려면 다음 단계를 수행하세요.  
  
1.  절차에 따라 [방법: StructuralType 결과 반환 하는 쿼리 실행](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md)합니다.  
  
2.  다음 쿼리를 `ExecuteStructuralTypeQuery` 메서드에 인수로 전달합니다.  
  
 [!code-csharp[DP EntityServices Concepts 2#MODULO](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#modulo)]  
  
## <a name="see-also"></a>참고자료
- [엔터티 SQL 참조](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)
