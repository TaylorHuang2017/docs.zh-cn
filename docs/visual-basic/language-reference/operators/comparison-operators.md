---
title: 比较运算符
ms.date: 07/20/2015
f1_keywords:
- vb.<>
- vb.>=
- vb.<=
- vb.>
- vb.<
helpviewer_keywords:
- greater than or equal to operator [Visual Basic]
- '>= operator [Visual Basic]'
- = operator [Visual Basic]
- < operator [Visual Basic]
- less than operator [Visual Basic]
- relational operators [Visual Basic], syntax
- Like operator [Visual Basic]
- <> operator [Visual Basic]
- '> operator [Visual Basic]'
- equal operator [Visual Basic]
- less than or equal to operator [Visual Basic]
- symbols, operators
- greater than operator [Visual Basic]
- comparing values [Visual Basic]
- operators [Visual Basic], relational
- string comparison [Visual Basic]
- not equal to comparison operator [Visual Basic]
- <= operator [Visual Basic]
- operators [Visual Basic], comparison
- Is operator [Visual Basic]
- comparison operators [Visual Basic], Visual Basic
ms.assetid: d6cb12a8-e52e-46a7-8aaf-f804d634a825
ms.openlocfilehash: ea7604626ede66da818e4bc22fe4922bc752dc2c
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74336086"
---
# <a name="comparison-operators-visual-basic"></a>比较运算符 (Visual Basic)
下面是 Visual Basic 中定义的比较运算符。

 `<` 运算符

 `<=` 运算符

 `>` 运算符

 `>=` 运算符

 `=` 运算符

 `<>` 运算符

 [Is 运算符](../../../visual-basic/language-reference/operators/is-operator.md)

 [IsNot 运算符](../../../visual-basic/language-reference/operators/isnot-operator.md)

 [Like 运算符](../../../visual-basic/language-reference/operators/like-operator.md)

 这些运算符比较两个表达式以确定它们是否相等，如果不相等，则确定它们之间的差异。 在单独的帮助页上详细讨论 `Is`、`IsNot`和 `Like`。 此页上详细讨论了关系比较运算符。

## <a name="syntax"></a>语法
  
```vb
result = expression1 comparisonoperator expression2  
result = object1 [Is | IsNot] object2  
result = string Like pattern  
```  
  
## <a name="parts"></a>部件
 `result`  
 必需。 一个 `Boolean` 值，该值表示比较的结果。

 `expression1`, `expression2`  
 必需。 任意表达式。

 `comparisonoperator`  
 必需。 任何关系比较运算符。

 `object1`, `object2`  
 必需。 任何引用对象的名称。

 `string`  
 必需。 任何 `String` 表达式。

 `pattern`  
 必需。 任何 `String` 的表达式或字符范围。

## <a name="remarks"></a>备注
 下表包含关系比较运算符和确定 `result` 是 `True` 还是 `False`的条件的列表。

|运算符|`True` 是否|`False` 是否|
|--------------|---------------|----------------|
|`<` （小于）|`expression1` < `expression2`|`expression1` >= `expression2`|
|`<=` （小于或等于）|`expression1` <= `expression2`|`expression1` > `expression2`|
|`>` （大于）|`expression1` > `expression2`|`expression1` <= `expression2`|
|`>=` （大于或等于）|`expression1` >= `expression2`|`expression1` < `expression2`|
|`=` （等于）|`expression1` = `expression2`|`expression1` <> `expression2`|
|`<>` （不等于）|`expression1` <> `expression2`|`expression1` = `expression2`|

> [!NOTE]
> [= 运算符](../../../visual-basic/language-reference/operators/assignment-operator.md)也用作赋值运算符。

 `Is` 运算符、`IsNot` 运算符和 `Like` 运算符具有特定的比较功能，这些功能不同于上表中的运算符。

## <a name="comparing-numbers"></a>比较数字
 将 `Single` 类型的表达式与 `Double`类型之一进行比较时，`Single` 表达式将转换为 `Double`。 此行为与 Visual Basic 6 中的行为相反。

 同样，将 `Decimal` 类型的表达式与 `Single` 或 `Double`类型的表达式进行比较时，`Decimal` 表达式会转换为 `Single` 或 `Double`。 对于 `Decimal` 表达式，可能会丢失小于 1E-28 的任何小数值。 此类小数值损失可能导致两个值在不时比较为相等。 出于此原因，应小心使用相等（`=`）来比较两个浮点变量。 更安全的做法是测试两个数字之差的绝对值是否小于可接受的小容差。

### <a name="floating-point-imprecision"></a>浮点不精确性
 使用浮点数时，请记住，它们在内存中不一定有精确的表示形式。 这可能会导致某些操作产生意外结果，如值比较和[Mod 运算符](../../../visual-basic/language-reference/operators/mod-operator.md)。 有关详细信息，请参阅[数据类型疑难解答](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)。

## <a name="comparing-strings"></a>比较字符串
 在比较字符串时，将根据其字母顺序排序来计算字符串表达式，具体取决于 `Option Compare` 设置。

 `Option Compare Binary` 对从字符的内部二进制表示形式派生的排序顺序进行字符串比较。 排序顺序由代码页确定。 下面的示例显示了一个典型的二进制排序顺序。

 `A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`

 `Option Compare Text` 基于不区分大小写的文本排序顺序对应用程序的区域设置进行字符串比较。 在上一示例中设置 `Option Compare Text` 并对字符进行排序时，将应用以下文本排序顺序：

 `(A=a) < (À= à) < (B=b) < (E=e) < (Ê= ê) < (Ø = ø) < (Z=z)`

### <a name="locale-dependence"></a>区域设置依赖关系
 设置 `Option Compare Text`时，字符串比较的结果可能取决于应用程序运行所在的区域设置。 在一个区域设置中，两个字符的比较结果可能不相同，而在另一个区域中 如果使用字符串比较来做出重要决策（例如是否接受登录尝试），则应注意区域设置的敏感性。 请考虑设置 `Option Compare Binary` 或调用 <xref:Microsoft.VisualBasic.Strings.StrComp%2A>，这会使区域设置生效。

## <a name="typeless-programming-with-relational-comparison-operators"></a>用关系比较运算符进行无方式编程
 `Option Strict On`下，不允许在 `Object` 表达式中使用关系比较运算符。 当 `Off``Option Strict` 并且 `expression1` 或 `expression2` 为 `Object` 表达式时，运行时类型将确定比较它们的方式。 下表显示了如何比较表达式和比较的结果，具体取决于操作数的运行时类型。

|如果操作数为|比较是|
|---------------------|-------------------|
|`String`|基于字符串排序特性的排序比较。|
|均为数值|转换为 `Double`，数值比较的对象。|
|一个数字和一个 `String`|`String` 转换为 `Double` 并执行数值比较。 如果 `String` 无法转换为 `Double`，则会引发 <xref:System.InvalidCastException>。|
|其中一个或两个都是引用类型，而不是 `String`|引发 <xref:System.InvalidCastException>。|

 数值比较将 `Nothing` 视为0。 字符串比较将 `Nothing` 视为 `""` （空字符串）。

## <a name="overloading"></a>重载
 关系比较运算符（`<`。 可以*重载*`<=`、`>`、`>=`、`=`、`<>`），这意味着当操作数具有该类或结构的类型时，该类或结构可以重新定义其行为。 如果你的代码在此类或结构上使用这些运算符中的任何一种，请确保了解重定义的行为。 有关更多信息，请参见 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。

 请注意， [= 运算符](../../../visual-basic/language-reference/operators/assignment-operator.md)只能作为关系比较运算符重载，而不能作为赋值运算符重载。

## <a name="example"></a>示例
 下面的示例演示了用于比较表达式的关系比较运算符的各种用法。 关系比较运算符返回一个 `Boolean` 结果，该结果表示指定的表达式的计算结果是否为 `True`。 将 `>` 和 `<` 运算符应用到字符串时，将使用字符串的正常字母排序顺序进行比较。 此顺序可能取决于区域设置。 排序是否区分大小写取决于 "[选项比较](../../../visual-basic/language-reference/statements/option-compare-statement.md)" 设置。

 [!code-vb[VbVbalrOperators#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#1)]

 在前面的示例中，第一个比较返回 `False`，其余比较返回 `True`。

## <a name="see-also"></a>另请参阅

- <xref:System.InvalidCastException>
- [= 运算符](../../../visual-basic/language-reference/operators/assignment-operator.md)
- [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [数据类型疑难解答](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [Visual Basic 中的比较运算符](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)
