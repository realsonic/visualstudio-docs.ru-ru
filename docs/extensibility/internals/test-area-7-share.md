---
title: 'Область тестирования 7: Совместно использовать | Документы Microsoft'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], sharing items
- source control plug-ins, sharing items
ms.assetid: 6ec4780a-bda4-4327-bb3e-c6c9e7eabf35
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: fa74d6ff2291288a1ca0e7f17a2edb1e126f222b
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="test-area-7-share"></a>Тестирование области 7: общий ресурс
Эта область тестирования охватывает элементы управления доступом между расположениями через **общего ресурса** команды.  
  
 Операция hhare является очевидным дублирования между двумя или более местоположения в пределах иерархии файлов системы управления версиями файлов и папок. Дублирование не действительно возникает на сервере, но пользователь видеть один и тот же файл в двух или нескольких указанных расположениях. При внесении изменений в любом из общих элементов, эти изменения будут отражены в других общих папках.  
  
 Для управления доступом в папки работает, если выбрать папку с по крайней мере один файл в системе управления версиями в нем. Команда share отключен при следующих условиях:  
  
-   Если указанная папка является пустой папке.  
  
-   Если реальные папки, но он содержит нет файлов системы управления версиями.  
  
-   Если создается виртуальная папка, файлов системы управления версиями, являются ли в нем или нет.  
  
-   При наличии удаленного веб-сайта проекта.  
  
## <a name="command-menu-access"></a>Доступ к меню команд  
 Следующие [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] путей меню среды разработки, которые используются в тестовых случаях.  
  
 Общий ресурс: **файл**->**система управления версиями**->**общего ресурса**.  
  
## <a name="expected-behavior"></a>Ожидаемое поведение  
  
-   Общий файл появится в общей папке.  
  
-   Просмотр источника управления версии хранилища журнала показано на что файлы являются общими.  
  
-   Изменение общего файла изменяет оба расположения файла.  
  
## <a name="test-cases"></a>Тестовые случаи  
 Ниже приведены определенные тестовые случаи для области проверки общей папки.  
  
|Действие|Шаги теста|Ожидаемые результаты для проверки|  
|------------|----------------|--------------------------------|  
|Совместно использовать файл из одного проекта, загруженного в системе управления версиями в другой проект загружен|1.  Создайте новый проект.<br />2.  Добавьте второй проект в решение.<br />3.  Создайте файл с именем, которое не находится в первом проекте второго проекта.<br />4.  Добавьте решение в систему управления версиями.<br />5.  Выберите первый проект.<br />6.  Откройте **общего ресурса** диалоговое окно (**файл** -> **системы управления версиями** -> **общего ресурса**).<br />7.  Совместное использование файла из второй проект к первому проекту.<br />8.  Принять **извлечь** при появлении соответствующего запроса.|Общее ожидаемое поведение.|  
|Совместно использовать файл из одного проекта на другой|1.  Создайте новый проект.<br />2.  Добавьте в систему управления версиями.<br />3.  Закройте решение.<br />4.  Создайте второй проект (новое решение).<br />5.  Добавьте решение в систему управления версиями.<br />6.  Выберите проект.<br />7.  Откройте **общего ресурса** диалоговое окно (**файл** -> **системы управления версиями** -> **общего ресурса**).<br />8.  Совместное использование файла из проекта, ранее добавленный в открытый проект.<br />9. Принять **извлечь** при появлении соответствующего запроса.|Общее ожидаемое поведение.|  
|Совместно использовать файл не является частью проекта из системы управления версиями в загруженный проект|1.  Создайте новый проект.<br />2.  Добавьте решение в систему управления версиями.<br />3.  Добавьте файл в систему управления версиями, который не является частью проекта или решения.<br />4.  Выберите проект и откройте **общего ресурса** диалоговое окно (**файл** -> **системы управления версиями** -> **общего ресурса**).<br />5.  Выберите файл в **совместное использование** диалоговое окно, не существует в пределах текущего проекта или решения и предоставить к нему.<br />6.  Принять **извлечь** при появлении соответствующего запроса.|Хранилище системы управления версиями производит запрос Get, файл доступен в локальное расположение проекта.|  
|Общий доступ к файлам в том же проекте, в другую папку|1.  Выберите **извлекать автоматически** в **средства** -> **параметры** -> **системы управления версиями**.<br />2.  Создайте новый проект и добавить его в систему управления версиями.<br />3.  Добавление папки в проект.<br />4.  Добавьте файл в папку и проверьте в папке.<br />5.  Выберите папку.<br />6.  Откройте **общего ресурса** диалоговое окно (**файл** -> **системы управления версиями** -> **общего ресурса**).<br />7.  Совместное использование файла в выбранной папке.|Общее ожидаемое поведение.<br /><br /> Папки необходимо выбрать вход с помощью файла в его, прежде чем он может использоваться для общей папки.|  
|Общий доступ к папке в загруженном проекте, рекурсивные|1.  Создайте новый проект.<br />2.  Добавьте решение в систему управления версиями.<br />3.  Выберите проект.<br />4.  Откройте **общего ресурса** диалоговое окно (**файл** -> **системы управления версиями** -> **общего ресурса**).<br />5.  Выберите папку.<br />6.  Совместное использование рекурсивно папки в проект.|Общее ожидаемое поведение.|  
|Совместное использование нескольких файлов из одного проекта в другой|1.  Создание нового проекта с несколькими файлами в нем.<br />2.  Добавьте решение в систему управления версиями.<br />3.  Закройте решение.<br />4.  Создайте новый проект в новом решении.<br />5.  Добавьте решение в систему управления версиями.<br />6.  Выберите проект.<br />7.  Откройте **общего ресурса** диалоговое окно (**файл** -> **системы управления версиями** -> **общего ресурса**).<br />8.  Совместное использование нескольких файлов из ранее созданного проекта в открытый проект.|Общее ожидаемое поведение.|  
  
## <a name="see-also"></a>См. также  
 [Руководство по тестированию подключаемых модулей системы управления версиями](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)