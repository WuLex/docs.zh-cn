---
title: ?? 运算符（C# 参考）
ms.date: 07/20/2015
f1_keywords:
- ??_CSharpKeyword
helpviewer_keywords:
- coalesce operator [C#]
- ?? operator [C#]
- conditional-AND operator (&&) [C#]
ms.assetid: 088b1f0d-c1af-4fe1-b4b8-196fd5ea9132
ms.openlocfilehash: 8fa751654acaf5939fb8f8068c7323e365f7bdab
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="-operator-c-reference"></a>?? 运算符（C# 参考）
`??` 运算符称作 null 合并运算符。  如果此运算符的左操作数不为 null，则此运算符将返回左操作数；否则返回右操作数。  
  
## <a name="remarks"></a>备注  
 可以为 null 的类型可以表示类型的域中的值，或者值可以是未定义的（在这种情况下，值为 null）。 如果左操作数具有一个值为 null 的可以为 null 的类型，则可使用 `??` 运算符的语法表现力来返回适当的值（右操作数）。 如果在尝试将可以为 null 值的类型分配给不可以为 null 值的类型时没有使用 `??` 运算符，则会生成编译时错误。 如果使用强制转换，且当前未定义可以为 null 值的类型，则会引发 `InvalidOperationException` 异常。  
  
 有关详细信息，请参阅[可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)。  
  
 ?? 的结果 不能将运算符视为常量，即使其两个参数都是常量。  
  
## <a name="example"></a>示例  
 [!code-csharp[csRefOperators#53](../../../csharp/language-reference/operators/codesnippet/CSharp/null-conditional-operator_1.cs)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)  
 [C# 编程指南](../../../csharp/programming-guide/index.md)  
 [C# 运算符](../../../csharp/language-reference/operators/index.md)  
 [可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)  
 [“提升”的准确含义是什么？](https://blogs.msdn.microsoft.com/ericlippert/2007/06/27/what-exactly-does-lifted-mean/)
