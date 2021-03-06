---
title: Практическое руководство. Определение среды выполнения .NET Framework | Документы Майкрософт
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools, .NET Framework versions
- .NET Framework versions,profililng
ms.assetid: d39f3579-719a-4f47-a97d-5b4232fe4c64
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: c52cecb30bdaa4daab46c7359e255d52d71d1597
ms.sourcegitcommit: 42ea834b446ac65c679fa1043f853bea5f1c9c95
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/19/2018
---
# <a name="how-to-specify-the-net-framework-runtime"></a>Практическое руководство. Определение среды выполнения .NET Framework

В выпуске [!INCLUDE[net_v40_long](../code-quality/includes/net_v40_long_md.md)] можно составлять приложения из модулей, построенных с помощью разных версий среды выполнения [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)]. По умолчанию средства профилирования Visual Studio обрабатывают первую среду выполнения, загруженную приложением. Можно указать среду выполнения для профилирования при запуске приложения с помощью профилировщика и при подключении профилировщика к уже запущенному приложению.

## <a name="to-specify-the-net-framework-run-time-to-profile-when-starting-an-application-with-the-profiler"></a>Указание профилируемой среды выполнения .NET Framework при запуске приложения с помощью профилировщика

1. В **обозревателе производительности** щелкните правой кнопкой мыши сеанс анализа производительности, выберите пункт **Свойства**, а затем **Дополнительно**.

     В списке **Целевая версия CLR** отображается **Автоматически** и версия среды выполнения [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)], которая установлена на компьютере.

2. Выполните одно из следующих действий.

    - Выберите версию среды CLR для профилирования.

    - Щелкните пункт **Автоматически**, чтобы выполнить профилирование первой версии, загруженной приложением.

## <a name="to-specify-the-net-framework-run-time-to-profile-when-attaching-the-profiler-to-an-application"></a>Указание профилируемой среды выполнения .NET Framework при подключении профилировщика к приложению

1. В меню "Анализ" наведите указатель мыши на пункт "Профилировщик" и щелкните "Присоединить/отсоединить".

2. В диалоговом окне "Присоединить профилировщик к процессу" щелкните процесс, который необходимо профилировать.

     В списке **Целевая версия CLR** отображается **Автоматически** и версии среды выполнения [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)], установленные на компьютере.

3. Выполните одно из следующих действий.

    - Выберите версию среды CLR для профилирования.

    - Щелкните **Автоматически** для профилирования версии, загружаемой при подключении профилировщика к приложению.