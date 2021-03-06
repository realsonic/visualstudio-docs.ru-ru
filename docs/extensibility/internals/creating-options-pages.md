---
title: Создание страниц "Параметры" | Документы Microsoft
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- managed package framework, creating Tools Options pages
- Tools Options pages [Visual Studio SDK], creating using managed package framework
ms.assetid: 1bf11fec-dece-4943-8053-6de1483c43eb
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 51e05c5f2660adfe8d7a35c816e5f94706631c8f
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="creating-options-pages"></a>Создание страницы параметров
В [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] платформы управляемых пакетов классы, производные от <xref:Microsoft.VisualStudio.Shell.DialogPage> расширить [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] интегрированной среды разработки, добавив **параметры** страниц в группе **средства** меню.  
  
 Объект, реализующий данный **в наборе средств** страница связана с определенной пакеты VSPackage, <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> объекта.  
  
 Поскольку среда создает объект, реализующий определенный **Сервис — Параметры** страницы при соответствующих страниц отображается в интегрированной среде разработки:  
  
-   Объект **в наборе средств** страницы должен быть реализован в своем объекте, а не на объект, реализующий VSPackage.  
  
-   Объект не может реализовывать несколько **Сервис — Параметры** страниц.  
  
## <a name="registering-as-a-tools-options-page-provider"></a>Регистрация в качестве поставщика страницы параметров средств  
 VSPackage вспомогательные пользовательскую конфигурацию через **Сервис — Параметры** страниц показывает объекты, предоставляющем эти **Сервис — Параметры** страниц, применяя экземпляров <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> применены к <xref:Microsoft.VisualStudio.Shell.Package>реализации.  
  
 Должен быть один экземпляр <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> для каждого <xref:Microsoft.VisualStudio.Shell.DialogPage>-производный тип, реализующий **Сервис — Параметры** страницы.  
  
 Каждый экземпляр <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> использует тип, реализующий **Сервис — Параметры** страницы, строки, содержащие категории и подкатегории, используемое для идентификации **Сервис — Параметры** страницы и ресурсов сведения для регистрации типа как поставщик **Сервис — Параметры** страницы.  
  
## <a name="persisting-tools-options-page-state"></a>Сохранение состояния страницы параметров средств  
 Если **Сервис — Параметры** реализация страниц зарегистрирован с включенной поддержкой автоматизации, IDE сохраняет состояние страницы, а также все остальные **Сервис — Параметры** страниц.  
  
 VSPackage может управлять собственный сохраняемости с помощью <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>. Следует использовать только один или другой метод сохраняемости.  
  
## <a name="implementing-dialogpage-class"></a>Реализация класса DialogPage  
 Объект, предоставляющий реализацию VSPackage <xref:Microsoft.VisualStudio.Shell.DialogPage>-производный тип можно воспользоваться преимуществами следующих наследуемыми функциями:  
  
-   Окно пользовательского интерфейса по умолчанию.  
  
-   Значение по умолчанию механизм сохранения доступны либо если <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> применяется к классу, или если <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute.SupportsProfiles%2A> свойству `true` для <xref:Microsoft.VisualStudio.Shell.ProvideOptionPageAttribute> , применяемый к классу.  
  
-   Поддержка модели автоматизации.  
  
 Минимальным требованием для объекта, реализующего **Сервис — Параметры** страницу с использованием <xref:Microsoft.VisualStudio.Shell.DialogPage> заключается в добавлении открытые свойства.  
  
 Если класс должным образом зарегистрирован как **Сервис — Параметры** страницы поставщика, а затем его открытые свойства доступны на **параметры** раздел **средства** меню в форме Сетка свойств.  
  
 Все эти функции по умолчанию можно переопределить. Например, для создания более сложных пользователя интерфейс требует только переопределение реализация по умолчанию <xref:Microsoft.VisualStudio.Shell.DialogPage.Window%2A>.  
  
## <a name="example"></a>Пример  
 Ниже приведен простой реализации «hello world» страницы параметров. Добавив следующий код в проект по умолчанию созданные шаблона пакета Visual Studio с **команду меню** выбран параметр адекватно продемонстрируют параметр функциональных возможностей страницы.  
  
### <a name="description"></a>Описание  
 Следующий класс определяет минимальные параметры страницы «hello world». При открытии, пользователь может задать открытый `HelloWorld` свойства в сетке свойств.  
  
### <a name="code"></a>Код  
 [!code-csharp[UI_UserSettings_ToolsOptionPages#11](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_1.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#11](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_1.vb)]  
  
### <a name="description"></a>Описание  
 Применение в класс пакета следующий атрибут доступны параметры страницы при загрузке пакета. Произвольные идентификаторы ресурсов категории и страницы, числа и логическое значение в конце указывает, поддерживает ли странице автоматизации.  
  
### <a name="code"></a>Код  
 [!code-csharp[UI_UserSettings_ToolsOptionPages#07](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_2.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#07](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_2.vb)]  
  
### <a name="description"></a>Описание  
 Следующий обработчик событий выводит результат в зависимости от значения свойства, заданного на странице параметров. Она использует <xref:Microsoft.VisualStudio.Shell.Package.GetDialogPage%2A> метод с результатом явно привести тип страницы настраиваемый параметр для доступа к свойствам на странице.  
  
 В случае проектов, созданных с помощью шаблона пакета, вызовите эту функцию из `MenuItemCallback` добавлена функция, чтобы присоединить его к команды по умолчанию для **средства** меню.  
  
### <a name="code"></a>Код  
 [!code-csharp[UI_UserSettings_ToolsOptionPages#08](../../extensibility/internals/codesnippet/CSharp/creating-options-pages_3.cs)]
 [!code-vb[UI_UserSettings_ToolsOptionPages#08](../../extensibility/internals/codesnippet/VisualBasic/creating-options-pages_3.vb)]  
  
## <a name="see-also"></a>См. также  
 [Расширение настройки пользователя и параметры](../../extensibility/extending-user-settings-and-options.md)   
 [Поддержка автоматизации страниц параметров](../../extensibility/internals/automation-support-for-options-pages.md)