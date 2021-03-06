---
title: Смешанный режим отладки для x64 поддерживается только при использовании Microsoft.NET Framework 4 или более поздней | Документы Microsoft
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.error.interop_unsupported_x64
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: b7495655-54c0-4315-8422-43bf63b8c22e
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5ceb332fab5e09fa4aaf57d3a89e20270643b705
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/18/2018
---
# <a name="mixed-mode-debugging-for-x64-processes-is-only-supported-when-using-microsoftnet-framework-4-or-greater"></a>На 64-разрядных платформах Windows отладка в смешанном режиме поддерживается только при использовании платформы Microsoft.NET Framework версии 4.0 или выше
Версии платформы .NET Framework, предшествующие версии 4, не поддерживают отладку в смешанном режиме для процессов x64. Это значит, что при выполнении отладки переход из управляемого кода в неуправляемый (как и обратный переход) невозможен.  
  
### <a name="workarounds"></a>Методы обхода проблемы  
  
-   Обновить проект так, чтобы в нем использовалась платформа Microsoft .NET Framework версии 4 или позднее.  
  
     - или -  
  
     Вести отладку управляемого и машинного кода в отдельных сеансах отладки.  
  
     - или -  
  
     Вести отладку смешанного кода в 32-разрядном процессе в соответствии со следующими процедурами:  
  
### <a name="to-change-the-platform-to-32-bit-visual-basic-or-c"></a>Изменение платформы на 32-разрядную версию (Visual Basic или C#)  
  
1.  В **обозревателе решений**, щелкните правой кнопкой мыши проект и выберите команду **свойства**.  
  
2.  На страницах свойств нажмите кнопку **компиляции** или **отладки** вкладки.  
  
3.  Нажмите кнопку **платформы** и выберите в списке платформ x86.  
  
     По умолчанию компиляторы Visual Basic и С# создают код, который можно использовать на любом ЦП. На 64-разрядном компьютере такие двоичные файлы работают как 64-разрядные процессы. Чтобы запустить 32-разрядный процесс, необходимо выбрать **Win32**, а не **AnyCPU**.  
  
### <a name="to-change-the-platform-to-32-bit-cc"></a>Изменение платформы на 32-разрядную версию (C или C++)  
  
1.  В **обозревателе решений**, щелкните правой кнопкой мыши проект, а затем нажмите кнопку **свойства**.  
  
2.  На страницах свойств нажмите кнопку **платформы** и в списке платформ выберите Win32.  
  
### <a name="to-correct-this-error"></a>Исправление ошибки  
  
-   В разделе [настройки отладки SQL](http://msdn.microsoft.com/en-us/3db09e68-edcc-42de-9c22-4e97cfd55ab3).  
  
## <a name="see-also"></a>См. также  
 [Отладка 64-разрядных приложений](../debugger/debug-64-bit-applications.md)