---
title: IDebugDefaultPort2 | Документы Microsoft
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugDefaultPort2
helpviewer_keywords:
- IDebugDefaultPort2 interface
ms.assetid: 7b3452af-9a96-4c4c-9946-4339b72d3d7b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: c6d131ab24cc57af1846f89b61afa2d89ae2cacb
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="idebugdefaultport2"></a>IDebugDefaultPort2
Этот интерфейс предоставляет несколько методов для доступа к средства уведомления и порт сервера.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
IDebugDefaultPort2 : IDebugPort2  
```  
  
## <a name="notes-for-implementers"></a>Примечания для разработчиков  
 Visual Studio реализует этот интерфейс для представления порт отладки для доступа к программам. Поставщик другой номер порта также можно реализовать этот интерфейс, если он обрабатывает удаленной отладки.  
  
## <a name="notes-for-callers"></a>Примечания для вызывающих объектов  
 Аргумент с методами [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md) интерфейс поддерживает этот интерфейс. Вызов [QueryInterface](/cpp/atl/queryinterface) на [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) интерфейс можно также получить этот интерфейс.  
  
## <a name="methods-in-vtable-order"></a>Методы в порядке таблицы Vtable  
 Помимо методов, определенных в [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md), этот интерфейс реализует следующие методы:  
  
|Метод|Описание|  
|------------|-----------------|  
|[GetPortNotify](../../../extensibility/debugger/reference/idebugdefaultport2-getportnotify.md)|Возвращает интерфейс порта уведомление от данного порта.|  
|[GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)|Возвращает интерфейс, сервер, содержащий этот порт.|  
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugdefaultport2-queryislocal.md)|Определяет, выполняется ли этот порт на локальном компьютере.|  
  
## <a name="remarks"></a>Примечания  
 Имя «`IDebugDefaultPort2`» — немного неверно, поскольку он не представляет порт по умолчанию. Он может вызываться «IDebugPort3».  
  
## <a name="requirements"></a>Требования  
 Заголовок: msdbg.h  
  
 Пространство имен: Microsoft.VisualStudio.Debugger.Interop  
  
 Сборка: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>См. также  
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)   
 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)