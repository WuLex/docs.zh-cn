---
title: '&amp;= 运算符（C# 参考）'
ms.date: 07/20/2015
f1_keywords:
- '&=_CSharpKeyword'
helpviewer_keywords:
- AND assignment operator (&=) [C#]
- '&= operator [C#]'
ms.assetid: e8d58f3f-72dd-4b5a-b995-452fcce7e6bb
ms.openlocfilehash: 092f46ddd8ca52e2d705200768c93a3473f1520f
ms.sourcegitcommit: 89c93d05c2281b4c834f48f6c8df1047e1410980
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2018
---
# <a name="amp-operator-c-reference"></a>&amp;= 运算符（C# 参考）
AND 赋值运算符。  
  
## <a name="remarks"></a>备注  
 使用 `&=` 赋值运算符的表达式，如  
  
```csharp  
x &= y  
```  
  
 等效于  
  
```csharp  
x = x & y  
```  
  
 不同的是 `x` 只计算一次。 [& 运算符](../../../csharp/language-reference/operators/and-operator.md) 对整型操作数执行按位逻辑 AND 运算，对 `bool` 操作数执行逻辑 AND 运算。  
  
 不能直接重载 `&=` 运算符，但用户定义的类型可重载二元 [& 运算符](../../../csharp/language-reference/operators/and-operator.md)（参阅[运算符](../../../csharp/language-reference/keywords/operator.md)）。  
  
## <a name="example"></a>示例  
 [!code-csharp[csRefOperators#34](../../../csharp/language-reference/operators/codesnippet/CSharp/and-assignment-operator_1.cs)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)  
 [C# 编程指南](../../../csharp/programming-guide/index.md)  
 [C# 运算符](../../../csharp/language-reference/operators/index.md)
