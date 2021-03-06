---
title: orderby 子句 - C# 参考
ms.date: 07/20/2015
f1_keywords:
- orderby
- orderby_CSharpKeyword
helpviewer_keywords:
- orderby clause [C#]
- orderby keyword [C#]
ms.assetid: 21f87f48-d69d-4e95-9a52-6fec47b37e1f
ms.openlocfilehash: d88b2b40f63f0616cfd54e8abb62f1bc2183f776
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/07/2020
ms.locfileid: "75713300"
---
# <a name="orderby-clause-c-reference"></a>orderby 子句（C# 参考）

在查询表达式中，`orderby` 子句可导致返回的序列或子序列（组）以升序或降序排序。 若要执行一个或多个次级排序操作，可以指定多个键。 元素类型的默认比较器执行排序。 默认排序顺序为升序。 还可以指定自定义比较器。 但是，只适用于使用基于方法的语法。 有关详细信息，请参阅[对数据进行排序](../../programming-guide/concepts/linq/sorting-data.md)。

## <a name="example"></a>示例

在以下示例中，第一个查询按字母顺序从 A 开始对字词排序，而第二个查询则按降序对相同的字词排序。 （`ascending` 关键字是默认排序值，可省略。）

[!code-csharp[cscsrefQueryKeywords#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Orderby.cs#20)]

## <a name="example"></a>示例

以下示例对学生的姓氏进行主要排序，然后对其名字进行次要排序。

[!code-csharp[cscsrefQueryKeywords#22](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Orderby.cs#22)]

## <a name="remarks"></a>备注

编译时，`orderby` 子句将转换为对 <xref:System.Linq.Enumerable.OrderBy%2A> 方法的调用。 `orderby` 子句中的多个关键值将转换为 <xref:System.Linq.Enumerable.ThenBy%2A> 方法调用。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [查询关键字 (LINQ)](query-keywords.md)
- [语言集成查询 (LINQ)](../../linq/index.md)
- [group 子句](group-clause.md)
- [C# 中的 LINQ 入门](/dotnet/csharp/programming-guide/concepts/linq/)
