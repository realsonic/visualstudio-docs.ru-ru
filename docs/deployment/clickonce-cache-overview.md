---
title: Общие сведения о кэше ClickOnce | Документы Microsoft
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows applications, ClickOnce deployemtn
- ClickOnce applications, cache
- ClickOnce deployment, cache
ms.assetid: e379921e-9ef1-4326-bbf3-53ba67925526
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0ff72cd106f39b4573a0e1d61715dad4f8c65140
ms.sourcegitcommit: 42ea834b446ac65c679fa1043f853bea5f1c9c95
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/19/2018
---
# <a name="clickonce-cache-overview"></a>Общие сведения о кэше ClickOnce
Все [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] приложения, являются ли они установлены локально или размещаются в сети, хранятся на клиентском компьютере в [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]приложения *кэша*. Объект [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] кэша — это семейство скрытых каталогов в каталоге локальные параметры папки Documents and Settings текущего пользователя. Этот кэш содержит файлы приложения, включая сборки, файлы конфигурации, приложения и пользовательские параметры и каталог данных. Кэш также отвечает за перенос каталог данных приложения до последней версии. Дополнительные сведения о миграции данных см. в разделе [доступ к локальным и удаленным данным в приложениях ClickOnce](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md).  
  
 Предоставляя одно местоположение для хранилища приложения [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] берет на себя задачи управления физической установкой приложения от пользователя. Кэш также помогает изолировать приложения путем хранения сборок и файлов данных для всех приложений и их разных версий отдельно друг от друга. Например, при обновлении [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] приложения, версия и ее информационные ресурсы предоставляются с их собственными каталогами в кэше.  
  
## <a name="cache-storage-quota"></a>Квота хранилища кэша  
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] приложения, размещенного в сети, ограничиваются по объему занимаемого квотой, которая ограничивает размер [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] кэша. Размер кэша применяется для всех пользователей сети приложений; одно приложение с частичным доверием, в Интернете может занимать не более половины пространства квоты. Установленные приложения не ограничены размером кэша и не учитываются счетчиком предельный размер кэша. Для всех [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] приложений в кэше сохраняются только текущая версия и ранее установленная версия.  
  
 По умолчанию клиентские компьютеры имеют 250 МБ хранилища для, сети [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] приложений. Это ограничение не учитываются файлы данных. Системный администратор можно увеличивать и уменьшать эту квоту на определенный компьютер, изменив раздел реестра HKEY_CURRENT_USER\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment\OnlineAppQuotaInKB, который является значением типа DWORD выражается размер кэша, в килобайтах. Например чтобы уменьшить размер кэша до 50 МБ, нужно изменить это значение равным 51200.  
  
## <a name="see-also"></a>См. также  
 [Доступ к локальным и удаленным данным в приложениях ClickOnce](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)