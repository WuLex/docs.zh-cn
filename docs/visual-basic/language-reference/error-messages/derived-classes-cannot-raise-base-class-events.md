---
title: 派生类无法引发基类事件
ms.date: 07/20/2015
f1_keywords:
- vbc30029
- bc30029
helpviewer_keywords:
- BC30029
ms.assetid: 63afa1c6-2f93-4512-a2f0-372455979771
ms.openlocfilehash: 365ce6ece1d964d3fac2a44f7ed4c1e16f44c95d
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="derived-classes-cannot-raise-base-class-events"></a>派生类无法引发基类事件
只能从在其中声明的声明空间，可以引发一个事件。 因此，一个类不能引发从任何其他类，甚至一个派生自的事件。  
  
 **错误 ID:** BC30029  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   移动`Event`语句或`RaiseEvent`语句，使它们处于同一个类。  
  
## <a name="see-also"></a>请参阅  
 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)  
 [RaiseEvent 语句](../../../visual-basic/language-reference/statements/raiseevent-statement.md)
