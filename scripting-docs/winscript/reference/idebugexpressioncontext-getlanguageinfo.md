---
title: "IDebugExpressionContext::GetLanguageInfo | Документы Microsoft"
ms.custom: 
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- IDebugExpressionContext.GetLanguageInfo
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugExpressionContext::GetLanguageInfo
ms.assetid: 35e25662-0b2a-4c3f-bce4-f01726bc04a8
caps.latest.revision: 
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 68c22d5dfcd16fb3d8f1dc3750bbfb23c4821176
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/27/2017
---
# <a name="idebugexpressioncontextgetlanguageinfo"></a>IDebugExpressionContext::GetLanguageInfo
Возвращает имя и идентификатор GUID для языка, которому принадлежит этот контекст.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT GetLanguageInfo(  
   BSTR*  pbstrLanguageName,  
   GUID*  pLanguageID  
);  
```  
  
#### <a name="parameters"></a>Параметры  
 `pbstrLanguageName`  
 [out] Имя языка.  
  
 `pLanguageID`  
 [out] Уникальный идентификатор языка.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Метод возвращает `HRESULT`. Допустимые значения включают, но не ограничиваются, значения, приведенные в следующей таблице.  
  
|Значение|Описание|  
|-----------|-----------------|  
|`S_OK`|Метод успешно выполнен.|  
  
## <a name="remarks"></a>Примечания  
 Этот метод возвращает имя и идентификатор GUID для языка, которому принадлежит этот контекст.  
  
## <a name="see-also"></a>См. также  
 [Интерфейс IDebugExpressionContext](../../winscript/reference/idebugexpressioncontext-interface.md)