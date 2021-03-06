---
title: Устранение неполадок при развертывании решения Office | Документы Microsoft
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ClickOnce deployment [Office development in Visual Studio], troubleshooting
- Office development in Visual Studio, troubleshooting
- deploying applications [Office development in Visual Studio], troubleshooting
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 29c3cfdcf31609eb5b6aec0111fe2297ba8c01ef
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="troubleshooting-office-solution-deployment"></a>Устранение неполадок, связанных с развертыванием решения Office
  В этом разделе содержатся сведения об устранении неполадок, которые могут возникнуть при развертывании решений Office.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
## <a name="troubleshooting-office-solutions-by-using-the-event-viewer"></a>Устранение неполадок решений Office с помощью средства просмотра событий  
 Вы можете использовать средство просмотра событий в Windows для просмотра сообщений об ошибках, записанных средой выполнения [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] при установке или удалении решений Office. Эти сообщения из журнала событий можно использовать для разрешения проблем развертывания и установки. Для получения дополнительной информации см. [Event Logging for Office Solutions](../vsto/event-logging-for-office-solutions.md).  
  
## <a name="changing-the-assembly-name-causes-conflicts"></a>Изменение имени сборки приводит к конфликтам  
 При изменении **имя сборки** значение в **приложения** страница **конструктора проектов** после уже развертывания решения средства публикации изменяют Пакет установки, чтобы включить один файл Setup.exe и два манифеста развертывания. При развертывании двух файлов манифеста могут возникнуть следующие обстоятельства.  
  
-   Если конечный пользователь установит обе версии, приложение будет загружать обе надстройки VSTO.  
  
-   Если надстройка VSTO была установлена до изменения имени сборки, конечный пользователь никогда не будет получать обновления.  
  
 Чтобы избежать этих обстоятельств, не изменяйте **имя сборки** значение после развертывания решения.  
  
## <a name="checking-for-updates-takes-a-long-time"></a>Проверка обновлений занимает много времени  
 Набор инструментов Visual Studio 2010 для среды выполнения Office предоставляет запись реестра, в которой администраторы могут установить значение времени ожидания для загрузки манифестов и решения.  
  
#### <a name="to-set-the-time-out-value"></a>Установка значения времени ожидания.  
  
1.  В реестре перейдите в следующий раздел:  
  
     HKEY_CURRENT_USER\Software\Microsoft\VSTA  
  
2.  В подразделе **AddInTimeout** задайте значение времени ожидания в миллисекундах.  
  
     Если подраздел **AddInTimeout** не существует, создайте его как DWORD.  
  
## <a name="cant-update-or-publish-to-a-network-file-share"></a>Не удается обновить или опубликовать в сетевом файловом ресурсе  
 Решения Office, которые находятся в сетевом файловом ресурсе, во время обновлений могут отображать вводящее в заблуждение сообщение, если файл Setup.exe решения блокируется в процессе при публикации обновления. Сообщение может говорить следующее: "Не удается добавить ’setup.exe’ на веб-сайт. Файл ’setup.exe’ уже существует на этом веб-сайте".  
  
 Чтобы предотвратить блокировку файла, можно сделать этот файловый ресурс доступным конечным пользователям только для чтения. Однако если в этом файловом ресурсе имеются документы, они также становятся доступными конечным пользователям только для чтения.  
  
## <a name="prerequisites-for-microsoft-office-arent-installed"></a>Необходимые компоненты для Microsoft Office не установлены  
 Вы можете добавить .NET Framework, [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]и основные сборки взаимодействия Office в пакет установки в качестве необходимых компонентов, развертываемых вместе с решением Office. Сведения о том, как установка основных сборок взаимодействия см. в разделе [Настройка компьютера для разработки решений Office](../vsto/configuring-a-computer-to-develop-office-solutions.md) и [как: установить основные сборки взаимодействия Office](../vsto/how-to-install-office-primary-interop-assemblies.md).  
  
## <a name="publishing-using-localhost-can-cause-installation-problems"></a>Публикация с использованием Localhost может вызвать проблемы установки  
 При использовании «http://localhost» в качестве местоположения публикации или установки для решений уровня документа **мастер публикации** не преобразует строку в имя компьютера. В таком случае необходимо установить решение на компьютере разработки. Чтобы развернутые решения могли использовать службы IIS на компьютере разработки, вместо localhost указывайте полное имя для всех расположений HTTP, HTTPS и FTP.  
  
## <a name="cached-assemblies-are-loaded-instead-of-updated-assemblies"></a>Вместо обновленных сборок загружаются кэшированные сборки  
 Fusion, загрузчик сборок .NET Framework, загружает кэшированную копию сборок, если выходной путь проекта указывает на сетевой файловый ресурс, сборка подписана строгим именем и версия сборки настройки не изменена. При обновлении сборки, которая удовлетворяет этим условиям, обновление не будет отображаться при следующем запуске проекта, поскольку будет загружена кэшированная копия.  
  
 Вы можете настроить Visual Studio так, чтобы Fusion загружал сборки при каждом запуске проекта.  
  
#### <a name="to-download-assemblies-instead-of-loading-cached-copies"></a>Загрузка сборок вместо загрузки кэшированных копий  
  
1.  В строке меню выберите **проекта**, * имя_проекта ***свойства**.  
  
2.  На странице **Приложения** выберите **Сведения о сборке**.  
  
3.  В первом **версии сборки** введите звездочку (\*), а затем выберите **ОК** кнопки.  
  
 После изменения версии сборки вы можете продолжить подписывать сборку строгим именем, и Fusion будет загружать последнюю версию настройки.  
  
## <a name="installation-fails-when-the-uri-has-characters-that-aret-us-ascii"></a>Установка завершается неудачно, если в URI входят символы не из набора US-ASCII  
 При публикации решения Office в расположении HTTP, HTTPS и FTP путь не может содержать какие-либо символы Юникода, не входящие в набор US-ASCII. Такие символы могут привести к непредсказуемому поведению программы установки. Используйте для пути установки только символы US-ASCII.  
  
## <a name="prompt-to-manually-uninstall-appears-when-you-publish-and-install-a-solution-on-the-development-computer"></a>При публикации и установке решения на компьютере разработки появляется запрос на удаление вручную  
 При сборке решения Office версия сборки регистрируется автоматически. Если ранее вы опубликовали и установили то же решение на свой компьютер разработки, то после следующей сборки, перестроения или публикации решения среда выполнения [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] обнаруживает, что путь установки для опубликованной версии и версия сборки отличаются. Появляется сообщение об ошибке "Не удается установить настройку, поскольку уже установлена другая версия, обновление которой из этой папки невозможно". Разделы реестра обновляются при каждом перестроении решения. Таким образом, необходимо удалить предыдущую версию перед публикацией, отладкой или запуском новой версии.  
  
 Чтобы предотвратить появление этого сообщения, создайте другую учетную запись пользователя на компьютере разработки для тестирования развертывания. Вы также можете удалить версию из списка программ, установленных на компьютере, перед следующей публикацией, отладкой или перестроением решения.  
  
## <a name="uncaught-exception-or-method-not-found-error-when-you-install-a-solution"></a>Ошибка "Неперехваченное исключение или "Метод не найден" при установке решения  
 При установке решения Office путем открытия манифеста развертывания (VSTO-файла), могут появиться сообщения об ошибке приложения, документа или книги Office для следующих условий.  
  
-   Метод не найден.  
  
-   MissingMethodException.  
  
-   Неперехваченное исключение.  
  
 Чтобы предотвратить эти сообщения об ошибках, устанавливайте решение путем запуска программы установки.  
  
 При установке решения без запуска программы установки установщик не проверяет и не устанавливает необходимые компоненты. Программа установки проверяет наличие соответствующих версий необходимых компонентов и устанавливает их по мере необходимости.  
  
## <a name="manifest-registry-keys-for-add-ins-change-after-an-installshield-limited-edition-project-is-built"></a>Разделы реестра манифеста для надстроек изменяются после сборки проекта InstallShield Limited Edition  
 Раздел реестра манифеста, который является частью программы установки надстройки VSTO, иногда изменяется с .vsto.manifest на .dll.manifest при сборке проекта InstallShield Limited Edition.  
  
 Чтобы обойти эту проблему, создайте проект InstallShield Limited Edition в другом решении или используйте CompanyName.AddinName в качестве значения раздела реестра, содержащего имя надстройки VSTO.  
  
## <a name="the-clickonce-installer-for-your-office-solution-doesnt-install-the-primary-interop-assemblies"></a>Установщик ClickOnce для решения Office не устанавливает основные сборки взаимодействия  
 При запуске программы установки, созданной ClickOnce для решения Office, установщик для основных сборок взаимодействия Office запускается только в том случае, если никакие основные сборки взаимодействия еще не установлены.  
  
 Если программа установки не устанавливает основные сборки взаимодействия правильно, установите их вручную, запустив файл установщика с именем o2007pia.msi из каталога установки.  
  
## <a name="reinstalling-office-solutions-causes-an-argument-out-of-range-exception"></a>Повторная установка решений Office приводит к возникновению исключения "Аргумент вне допустимого диапазона"  
 При повторной установке решения Office может возникать исключение <xref:System.ArgumentOutOfRangeException> со следующим сообщением об ошибке: "Заданный аргумент находится вне диапазона допустимых значений".  
  
 Такая ситуация возникает, если регистр URL-адреса для местоположения установки отличается. Например, эта ошибка будет отображаться при установке решения Office от [ http://fabrikam.com/ExcelSolution.vsto ](http://fabrikam.com/ExcelSolution.vsto) в первый раз, а затем использовать [ http://fabrikam.com/excelsolution.vsto ](http://fabrikam.com/excelsolution.vsto) во второй раз.  
  
 Чтобы предотвратить появление этого сообщения, используйте один и тот же регистр при установке решения Office.  
  
## <a name="cant-install-a-clickonce-solution-by-opening-the-deployment-manifest-from-the-web"></a>Не удается установить решение Office путем открытия манифеста развертывания из Интернета  
 Пользователи могут установить решение Office путем открытия манифеста развертывания из Интернета. Однако в некоторых установках Internet Information Services (IIS) имя файла с расширением VSTO блокируется. Прежде чем использовать его для развертывания решения Office, необходимо задать тип MIME в IIS.  
  
 Сведения о том, как задать тип MIME в IIS 6, см. в разделе [Настройка типов MIME (IIS 6.0)](http://www.microsoft.com/technet/prodtechnol/WindowsServer2003/Library/IIS/cd72c0dc-c5b8-42e4-96c2-b3c656f99ead.mspx?mfr=true).  
  
 Сведения о том, как задать тип MIME в IIS 7, см. в разделе [Добавление типа MIME (IIS7)](http://technet.microsoft.com/library/cc725608(WS.10).aspx).  
  
 Установите **.vsto** в качестве расширения и **application/x-ms-vsto**в качестве типа MIME.  
  
## <a name="see-also"></a>См. также  
 [Устранение неполадок развертывания ClickOnce](/visualstudio/deployment/troubleshooting-clickonce-deployments)   
 [Развертывание решения Office](../vsto/deploying-an-office-solution.md)  
  
  