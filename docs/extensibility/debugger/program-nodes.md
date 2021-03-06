---
title: Программирование узлы | Документы Microsoft
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- program nodes, debugging context
- debugging [Debugging SDK], program nodes
- program nodes, adding
- program nodes, superceding
ms.assetid: 1c5a5c13-c14d-42c3-af11-4c63f1032c8d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 50ab93c31a340bf8a2f4e2deb5f202707d7826b8
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="program-nodes"></a>Программа узлов
С точки зрения архитектуры отладчик **узел программы**:  
  
-   Представляет собой упрощенный описание программы.  
  
-   Можно определить себя и процесс его выполнение в и может быть присоединен, следует отсоединить от и описать отладчик (DE), она создана, если таковые имеются.  
  
-   Представленный [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) интерфейс, обычно создается путем DE или порт. Программа узлы добавляются к порту, вызвав [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md). При добавлении узла программы к порту добавляется процесс, содержащий программу, которая представляет этот узел программы.  
  
 Некоторое время после запуска сеанса отладки, в зависимости от реализации отладки пакета, программа узлы используются для создания соответствующих программ. Когда процесс запрашиваются его программ, перечислены программы, один для каждого узла программы.  
  
 Перед исполняемой программы, интегрированной среды разработки требуется упрощенные сведения о программе. Эти сведения можно получить из узла "программы". После прикрепления программы для интегрированной среды разработки требуется отобразить более подробные сведения, такие как список всех потоков в программе. Эти сведения будут получены из самой программы.  
  
## <a name="see-also"></a>См. также  
 [Программы](../../extensibility/debugger/programs.md)   
 [Процессы](../../extensibility/debugger/processes.md)   
 [Отладка ядра](../../extensibility/debugger/debug-engine.md)   
 [Основные понятия отладчика](../../extensibility/debugger/debugger-concepts.md)   
 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)