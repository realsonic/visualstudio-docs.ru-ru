---
title: Создание столбцов сайта, типов содержимого и списков для SharePoint | Документы Microsoft
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.ListDesigner.ContentTypeSetting
- VS.SharePointTools.ContentTypeDesigner.CommonPropertiesPage
- VS.SharePointTools.ListDesigner.CreatingLists
- VS.SharePointTools.ListDesigner.ListPage
- VS.SharePointTools.ListDesigner.ViewPage
- VS.SharePointTools.ListDesigner.CommonPropertiesPage
- VS.SharePointTools.ContentTypeDesigner.ColumnsPage
dev_langs:
- VB
- CSharp
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 1025884bb23290c616a42a8cbbdcbad1d5814b67
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="creating-site-columns-content-types-and-lists-for-sharepoint"></a>Создание столбцов сайта, типов содержимого и списков для SharePoint
  Visual Studio предоставляет шаблоны элементов проекта для различных основных элементов SharePoint, включая *перечислены* и *типы содержимого*, которые могут включать столбцы сайтов (или  *поля*). Конструкторы для новых типов содержимого и списков позволяют создать эти элементы проще, чем когда-либо.  
  
## <a name="site-columns"></a>Столбцы сайта  
 Столбцы сайта являются одним из основных элементов, которые можно добавлять в проект SharePoint. Столбец сайта представляет собой тип данных, например, телефонный номер, текстовый комментарий или название города контакта в списке контактов.  
  
 Новый шаблон проекта столбца сайта делает создание столбцов сайта проще, чем в предыдущей версии Visual Studio. После создания нового столбца сайта вы можете изменить XML в файле Elements.xml столбца сайта, чтобы включить необходимые сведения, такие как его отображаемое имя, тип данных и группу, в которую необходимо поместить столбец сайта в SharePoint. Дополнительные сведения о столбцах сайта см. в разделе [Общие сведения о столбцах](http://go.microsoft.com/fwlink/?LinkId=224996).  
  
## <a name="content-types-and-lists"></a>Типы содержимого и списки  
 Типы содержимого и списки являются наиболее часто используемыми элементами в SharePoint.  
  
 Тип содержимого определяет метаданные, рабочий процесс и поведение для категории элементов в списке SharePoint или библиотеке документов. Например, можно создать тип содержимого для информации в списке контактов или списке задач. Тип содержимого контактов может включать такие столбцы как: имя, электронная почта, номер телефона и адрес. Тип содержимого, определенного на уровне сайта, не зависит от какого-либо списка или библиотеки документов на сайте. Вы можете использовать один и тот же тип содержимого с различными списками или библиотеками документов на сайте SharePoint. Вы также можете использовать несколько типов содержимого в одном списке или библиотеке документов.  
  
 Список — это набор информации в SharePoint, который может использоваться совместно с другими. Список состоит из строк и столбцов, содержащих данные. Некоторые примеры списков: список задач, список контактов и список извещений.  
  
 Новые конструкторы типов содержимого и списков в [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] дают возможность создавать типы содержимого сайта и списки гораздо проще и интуитивнее, чем в предыдущей версии Visual Studio. Пользовательский интерфейс позволяет визуально создавать типы содержимого и списки знакомым способом, а также сортировать и группировать данные в списках и использовать заголовки групп. Дополнительные сведения о типах содержимого см. в разделе [типы содержимого](http://go.microsoft.com/fwlink/?LinkId=224997). Дополнительные сведения о списках см. в разделе [списка форм](http://go.microsoft.com/fwlink/?LinkId=224998) и [представления списка](http://go.microsoft.com/fwlink/?LinkId=224999).  
  
## <a name="related-topics"></a>См. также  
  
|Заголовок|Описание|  
|-----------|-----------------|  
|[Пошаговое руководство. Создание столбца сайта, типа содержимого и списка для SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)|Показывает способы создания столбцов сайта, используемые в пользовательском типе содержимого. Тип содержимого затем используется в пользовательском списке.|  
  
## <a name="see-also"></a>См. также  
 [Начало разработки для SharePoint 2010](http://go.microsoft.com/fwlink/?LinkId=225000)  
  
  