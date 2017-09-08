---
title: "Использование лабораторной среды для DevOps | Документы Майкрософт"
ms.custom: 
ms.date: 05/02/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- lab environment, test lab
ms.assetid: b435eb39-dc7c-46fa-a91b-6e6dd614f01c
caps.latest.revision: 56
ms.author: douge
manager: douge
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: 45d36934cf1c46902cac566203cddf4a118b7fe4
ms.openlocfilehash: 29b1343159cb91d3d5e4b9769c4103cc3565f986
ms.contentlocale: ru-ru
ms.lasthandoff: 06/02/2017

---
# <a name="use-a-lab-environment-for-your-devops"></a>Использование лабораторной среды для DevOps

Лабораторная среда — это коллекция виртуальных и физических машин, которую можно использовать для разработки и тестирования приложений. Лабораторная среда может содержать несколько ролей, необходимых для тестирования многоуровневых приложений, например рабочих станций, веб-серверов и серверов баз данных. Кроме того, в лабораторной среде можно использовать рабочий процесс "сборка-развертывание-тестирование" для автоматизации процесса сборки, развертывания и выполнения автоматических тестов приложения.

* **Использование плана тестирования для выполнения автоматических тестов**. Можно запустить набор автоматических тестов, называемый *планом тестирования*, и просмотреть ход его выполнения.  
  
* **Использование рабочего процесса "сборка-развертывание-тестирование"**. Рабочий процесс "сборка-развертывание-тестирование" можно использовать для автоматического тестирования многоуровневых приложений. Типичным примером является рабочий процесс, который начинается со сборки, развертывает файлы сборки на соответствующих компьютерах в лабораторной среде, а затем выполняет автоматические тесты. Кроме того, можно запланировать рабочий процесс так, чтобы он выполнялся с указанными интервалами.  
  
* **Сбор данных диагностики со всех компьютеров (даже во время ручного тестирования)**. Данные диагностики можно собирать с нескольких компьютеров одновременно. Например, во время одного тестового запуска можно собирать данные IntelliTrace, данные о влиянии теста и другие данные с веб-сервера, сервера базы данных и клиента.  
  
Ниже приведены примеры распространенных типов лабораторных сред:  
  
| Топология | Описание |  
|---|---|  
|![Топология "Только сервер"](../media/topology_backend.png)| Эта лабораторная среда включает *топологию серверов*, которая часто используется для выполнения ручных тестов для серверных приложений. Кроме того, она позволяет тест-инженерам использовать собственные клиентские компьютеры для проверки ошибок в окружении. В топологии серверной части лабораторная среда будет содержать только серверы. При использовании топологии этого типа подключение к серверам в лабораторной среде выполняется с клиентского компьютера, который не является частью среды.|  
|![Облачная лабораторная среда](../media/topology_cloud.png)| Эта лабораторная среда предоставляет возможности и функции, аналогичные _топологии серверов_, но устраняет потребность в запуске физических компьютеров или виртуальных машин в локальной среде, что сокращает время настройки, упрощает обслуживание и минимизирует стоимость. Настройка нескольких веб-сайтов и виртуальных машин вместе с пользовательскими сетевыми компонентами осуществляется быстро и просто в облачной среде, такой как Microsoft Azure. [Дополнительные сведения](#usebandrm).|  
|![Лабораторная среда "клиент-сервер"](../media/topology_clientserver.png)| Эта лабораторная среда основана на *топологии "клиент-сервер"*, которая часто используется для тестирования приложений, имеющих серверные и клиентские компоненты. В топологии "клиент-сервер" все клиентские и серверные компьютеры, используемые для тестирования приложения, находятся в лабораторной среде. При использовании этой топологии можно собирать данные тестирования с каждого компьютера, влияющего на тесты.|  
  
См. [Видео. Управление лабораторными средами для тестирования](http://go.microsoft.com/fwlink/?LinkID=252614).  
  
Ниже перечислены типичные способы для настройки лабораторной среды: 
  
* **[Использование облака с функциями сборок и выпусков в Team Services или Team Foundation Server &amp;](#usebandrm)**

* **[Использование функций Visual Studio Lab Management в Microsoft Test Manager](#usemtmlm)**

<a name="usebandrm"></a>
## <a name="use-the-cloud-with-team-services-or-team-foundation-server-build-amp-release"></a>Использование облака с функциями сборок и выпусков в Team Services или Team Foundation Server &amp;

Вы можете выполнить автоматическое тестирование и автоматизацию процесса "сборка-развертывание-тестирование" с помощью функций [сборки &amp; и выпусков](https://www.visualstudio.com/team-services/continuous-integration/) в Team Foundation Server (TFS) и Visual Studio Team Services. Ниже указаны некоторые преимущества:

* Вам не требуется контроллер сборки или контроллер тестирования.
* Агент тестирования устанавливается с помощью задачи в рамках сборки или выпуска.
* Можно легко настроить этапы развертывания. Вы больше не ограничены одним скриптом. Кроме того, можно использовать множество задач, доступных как в продукте, так и в Visual Studio Marketplace.
* Не требуется обслуживать наборы тестов. Вы можете выполнять тесты напрямую из двоичных файлов.
* Вам доступен расширенный интерфейс отчетов для тестов, выполнявшихся в рамках каждой сборки или каждого выпуска.
* Вы можете отслеживать, какие активы (выпуск, сборка, рабочие элементы, фиксации) сейчас развернуты и протестированы в каждом окружении.
* Вы можете настроить и расширить автоматизацию, чтобы упростить развертывание в нескольких тестовых окружениях и даже в рабочей среде.
* Вы можете запланировать автоматизацию при совершении возврата или фиксации, а также на определенное время дня.

[Дополнительные сведения](use-build-or-rm-instead-of-lab-management.md).

<a name="usemtmlm"></a>
## <a name="use-the-visual-studio-lab-management-features-of-microsoft-test-manager"></a>Использование функций Visual Studio Lab Management в Microsoft Test Manager

Вы можете создавать лабораторные среды и управлять ими с помощью функций компонента Visual Studio Lab Management в Microsoft Test Manager при работе с Visual Studio Enterprise или Visual Studio Test Professional.

Компонент Lab Management автоматически устанавливает агенты тестирования на всех компьютерах в окружении.  
  
При использовании Lab Management совместно с System Center Virtual Machine Manager (SCVMM) доступны следующие преимущества лабораторных сред:  
  
* **Возможность быстро воспроизвести конфигурации компьютеров**. Вы можете хранить коллекции виртуальных машин, настроенные для воссоздания типичных рабочих сред, а затем выполнять тестовые запуски в новой копии хранимой среды.  
  
* **Воспроизведение точных условий возникновения ошибки**. В случае сбоя тестового запуска вы можете сохранить копию состояния в лабораторной среде, а затем получить к ней доступ из результатов сборки или рабочего элемента.  
  
* **Выполнение нескольких копий лабораторной среды одновременно**. Вы можете одновременно выполнять несколько копий лабораторной среды, не опасаясь конфликтов именования.  
  
### <a name="standard-environments-and-scvmm-environments"></a>Стандартные среды и среды SCVMM

Существует два типа лабораторных сред, которые можно создать с помощью Visual Studio Lab Management: **стандартные окружения** и **окружения SCVMM**.
Однако возможности этих сред различаются.  
  
> **Примечание**. Lab Management **не** поддерживает SCVMM 2016. Сведения о SCVMM см. в статье [Virtual Machine Manager](http://go.microsoft.com/fwlink/?LinkId=226332). 
  
**Стандартные окружения:** могут содержать как виртуальные, так и физические компьютеры. Кроме того, виртуальные машины можно добавлять в стандартную среду под управлением сторонней платформы виртуализации. Стандартные среды также не требуют дополнительных ресурсов сервера, таких как сервер SCVMM.  
  
**Окружения SCVMM:** могут включать только виртуальные машины под управлением SCVMM (System Center Virtual Machine Manager). Соответственно, виртуальные машины в таких средах могут выполняться только на платформе виртуализации Hyper-V. При этом среды SCVMM обеспечивают следующие возможности автоматизации и управления, недоступные в стандартных средах.  
  
- **Моментальные снимки окружения:** содержат состояние лабораторной среды, позволяя быстро восстановить чистое окружение или сохранить состояние измененного окружения. Кроме того, для автоматизации процесса сохранения и восстановления снимков экрана можно использовать рабочий процесс "сборка-развертывание-тестирование".  
  
- **Хранимые окружения:** можно сохранить копию окружения SCVMM, а затем развернуть несколько его копий.  
  
- **Сетевая изоляция:** позволяет одновременно выполнять несколько идентичных копий окружения SCVMM, не опасаясь конфликтов именования.  
  
- **Шаблоны виртуальных машин:** шаблон виртуальной машины — это виртуальная машина без имени и прочих идентификаторов. Когда шаблон виртуальной машины развертывается в окружении SCVMM, Microsoft Test Manager создает новые идентификаторы. Это позволяет развертывать несколько копий виртуальной машины в одной среде или нескольких средах, а затем выполнять их одновременно.  
  
- **Хранимые виртуальные машины:** виртуальные машины, хранимые в библиотеке командных проектов, которые включают уникальные идентификаторы.  
  
Дополнительные сведения об этих возможностях см. в разделе [Руководство по созданию окружений SCVMM и управлению ими](https://msdn.microsoft.com/en-gb/library/ee830480.aspx).  
  
Стандартные среды и среды SCVMM поддерживают много одинаковых возможностей. Тем не менее, есть некоторые существенные отличия. В таблице ниже приводится сравнение функций, доступных для стандартных сред и сред SCVMM.  
  
|Возможность|Среды SCVMM|Стандартные среды|  
|----------------|------------------------|---------------------------|  
|**Тестирование**|||  
|Выполнение тестов вручную|Поддерживается|Поддерживается|  
|Выполнение закодированных тестов пользовательского интерфейса и автоматических тестов|Поддерживается|Поддерживается|  
|Регистрация полнофункциональных ошибок с помощью адаптеров диагностики|Поддерживается|Поддерживается|  
|**Развертывание сборки**|||  
|Автоматические рабочие процессы "сборка-развертывание-тестирование"|Поддерживается|Поддерживается|  
|**Создание окружений и управление ими**|||  
|Использование физических компьютеров в дополнение к виртуальным машинам|Не поддерживаются|Поддерживается|  
|Использование сторонних виртуальных машин|Не поддерживаются|Поддерживается|  
|Автоматическая установка агентов тестирования на компьютеры в лабораторной среде|Поддерживается|Поддерживается|  
|Сохранение и развертывание состояния лабораторной среды с помощью снимков среды|Поддерживается|Не поддерживаются|  
|Создание лабораторных сред на основе шаблонов виртуальных машин|Поддерживается|Не поддерживаются|  
|Запуск, остановка и создание снимка среды|Поддерживается|Не поддерживаются|  
|Подключение к среде с помощью средства просмотра среды|Поддерживается|Поддерживается|  
|Запуск нескольких копий среды одновременно с помощью функции изоляции сети|Поддерживается|Не поддерживаются|  
  
### <a name="lab-management-concepts"></a>Понятия лабораторной среды

Ниже приводятся некоторые дополнительные понятия, с которыми необходимо ознакомиться перед продолжением работы.  
  
|Термин|Описание|  
|----------|-----------------|  
|Центр лабораторий|Область Microsoft Test Manager, в которой выполняется создание лабораторных сред и управление ими.|  
|Лаборатория командного проекта|Коллекция лабораторных сред, которые настроены таким образом, чтобы к ним можно было подключаться и запускать их виртуальные машины.|  
|Библиотека командных проектов|Архив, состоящий из хранимых виртуальных машин, шаблонов и хранимых лабораторных сред, которые были импортированы в группу узлов командного проекта. Элементы библиотеки можно использовать в средах SCVMM, однако их нельзя напрямую добавлять в стандартную среду. Элементы нельзя запускать в библиотеке: они используются для развертывания в новой среде.|  
|Развернутая среда|Лабораторная среда, которая была развернута в лаборатории командного проекта, чтобы можно было подключаться к ней и запускать ее компьютеры.|  

#### <a name="related-topics"></a>См. также

* [Планирование лабораторной работы](https://msdn.microsoft.com/library/ff756575%28v=vs.140%29.aspx) 
* [Администрирование лабораторной среды](https://msdn.microsoft.com/library/dd936084%28v=vs.140%29.aspx) 
* [Настройка окружений SCVMM](https://msdn.microsoft.com/library/dd380687%28v=vs.140%29.aspx) 
* [Обновление диспетчера SCVMM 2008 R2 до версии SCVMM 2012](upgrade-scvmm-2008-r2-scvmm-2012.md) 
* [Управление разрешениями](https://msdn.microsoft.com/library/dd380760%28v=vs.140%29.aspx) 
* [Настройка изменений](https://msdn.microsoft.com/library/ee704508%28v=vs.140%29.aspx) 
* [Устранение неполадок](https://msdn.microsoft.com/library/ee853230%28v=vs.140%29.aspx)
  
### <a name="set-up-environments"></a>Настройка окружений

* [Облачные окружения сборок и выпусков &amp;](use-build-or-rm-instead-of-lab-management.md)
* [Стандартные лабораторные среды](https://msdn.microsoft.com/en-gb/library/ee390842.aspx)
* [(Виртуальные) среды SCVMM](https://msdn.microsoft.com/en-gb/library/ee943322.aspx)
* [Создание и использование изолированной от сети среды](https://msdn.microsoft.com/en-gb/library/ee518924.aspx)
  
## <a name="see-also"></a>См. также
  
* [Установка и настройка агентов тестирования](install-configure-test-agents.md)
* [Руководство по Visual Studio Lab Management](http://go.microsoft.com/fwlink/?LinkID=230951)  
* [Управление лабораторными средами для тестирования](http://go.microsoft.com/fwlink/?LinkID=252614)  
* [Блог по Visual Studio DevOps + Team Foundation Server](http://go.microsoft.com/fwlink/?LinkID=254496)  
