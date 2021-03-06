---
title: EVALFLAGS | Документы Microsoft
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- EVALFLAGS
helpviewer_keywords:
- EVALFLAGS enumeration
ms.assetid: 7b2cb14a-511a-4fef-9e4f-308139719fba
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 7c718414749bb6c748f25fb90837644fe984a274
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="evalflags"></a>EVALFLAGS
Указывает флаги, управляющие вычисления выражения.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
enum enum_EVALFLAGS {  
   EVAL_RETURNVALUE = 0x0002,  
   EVAL_NOSIDEEFFECTS = 0x0004,  
   EVAL_ALLOWBPS = 0x0008,  
   EVAL_ALLOWERRORREPORT = 0x0010,  
   EVAL_FUNCTION_AS_ADDRESS = 0x0040,  
   EVAL_NOFUNCEVAL = 0x0080,  
   EVAL_NOEVENTS = 0x1000  
};  
typedef DWORD EVALFLAGS;  
```  
  
```csharp  
public enum enum_EVALFLAGS {  
   EVAL_RETURNVALUE = 0x0002,  
   EVAL_NOSIDEEFFECTS = 0x0004,  
   EVAL_ALLOWBPS = 0x0008,  
   EVAL_ALLOWERRORREPORT = 0x0010,  
   EVAL_FUNCTION_AS_ADDRESS = 0x0040,  
   EVAL_NOFUNCEVAL = 0x0080,  
   EVAL_NOEVENTS = 0x1000  
}  
```  
  
## <a name="members"></a>Участники  
 EVAL_RETURNVALUE  
 Указывает, вычисления и возвращаемое значение, если таковая имеется.  
  
 EVAL_NOSIDEEFFECTS  
 Указывает, не допускается побочные эффекты.  
  
 EVAL_ALLOWBPS  
 Указывает остановки точек останова.  
  
 EVAL_ALLOWERRORREPORT  
 Указывает отчетов для узла разрешаются. В основном используется для вычисления выражений в скрипте в Internet Explorer.  
  
 EVAL_FUNCTION_AS_ADDRESS  
 Принудительно вызывает функции для оценки в качестве адреса, вместо вызова функции.  
  
 EVAL_NOFUNCEVAL  
 Препятствует при вычислении функции. Например, рассмотрим `int` маркера в выражении `myExpression(int) + 10`. Эта функция может вычисляться неправильно, адрес, а не значение.  
  
 EVAL_NOEVENTS  
 Флаг, указывающий, не отправляются события, происходящие во время вычисления выражения для диспетчера сеанса отладки (SDM) или в интегрированную среду разработки.  
  
## <a name="remarks"></a>Примечания  
 Эти флаги передаются в качестве аргумента для [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) и [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) методы.  
  
 Эти флаги могут объединяться с Побитовый оператор или.  
  
## <a name="requirements"></a>Требования  
 Заголовок: msdbg.h  
  
 Пространство имен: Microsoft.VisualStudio.Debugger.Interop  
  
 Сборка: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>См. также  
 [Перечисления](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)   
 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)