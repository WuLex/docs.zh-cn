---
title: "ISymUnmanagedReader::GetNamespaces 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name:
- ISymUnmanagedReader.GetNamespaces
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader::GetNamespaces
helpviewer_keywords:
- ISymUnmanagedReader::GetNamespaces method [.NET Framework debugging]
- GetNamespaces method, ISymUnmanagedReader interface [.NET Framework debugging]
ms.assetid: 3feb4796-2fab-45ce-beca-6f5bc530b971
topic_type:
- apiref
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 9db8875acfd4df2cd889cc2e6d606aba252fa33f
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2017
---
# <a name="isymunmanagedreadergetnamespaces-method"></a>ISymUnmanagedReader::GetNamespaces 方法
获取在此符号存储区中的全局范围内定义的命名空间。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT GetNamespaces (  
    [in]  ULONG32  cNameSpaces,  
    [out] ULONG32  *pcNameSpaces,  
    [out, size_is (cNameSpaces),  
        length_is (*pcNameSpaces)]  
        ISymUnmanagedNamespace*  namespaces[]);  
```  
  
#### <a name="parameters"></a>参数  
 `cNameSpaces`  
 [in]命名空间数组的大小。  
  
 `pcNameSpaces`  
 [out]指向接收命名空间列表的长度的变量的指针。  
  
 `namespaces`  
 [out]指向接收的命名空间列表的变量的指针。  
  
## <a name="return-value"></a>返回值  
 如果该方法成功; 则为 S_OK否则为 E_FAIL 或某些其他错误代码。  
  
## <a name="requirements"></a>惠?  
 **标头：** CorSym.idl、 CorSym.h  
  
## <a name="see-also"></a>请参阅  
 [ISymUnmanagedReader 接口](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-interface.md)
