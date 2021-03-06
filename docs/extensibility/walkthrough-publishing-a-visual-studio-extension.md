---
title: 'Пошаговое руководство: Публикация расширение Visual Studio | Документы Microsoft'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- publishing web controls
- web controls, publishing
ms.assetid: a7816161-0490-4043-86f5-0f7331ed83b3
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: f823334f3686bdba3406daac69b2a98d203780a7
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="walkthrough-publishing-a-visual-studio-extension"></a>Пошаговое руководство: Публикация расширение Visual Studio

В этом пошаговом руководстве показано, как для публикации расширения Visual Studio в Visual Studio Marketplace. При добавлении расширения в Marketplace, разработчики могут использовать **расширения и обновления** для поиска новых и обновленных расширений.

## <a name="prerequisites"></a>Предварительные требования

 Для выполнения этого пошагового руководства необходимо установить пакет SDK для Visual Studio. Дополнительные сведения см. в разделе [Установка пакета SDK для Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-visual-studio-extension"></a>Создайте расширение Visual Studio

В этом случае будет использовать расширение по умолчанию VSPackage, но допустимы те же действия для каждого типа используемого модуля.

1. Создайте пакет VSPackage в C# с именем «TestPublish», содержащую команду меню. Дополнительные сведения см. в разделе [созданию вашей первой расширения: Hello World](../extensibility/extensibility-hello-world.md).

## <a name="package-your-extension"></a>Пакет расширения

1. Обновление расширения vsixmanifest с правильными данными о название продукта, автор и версии.

  ![Обновление расширения vsixmanifest](media/update-extension-vsixmanifest.png)

2. Построение расширения **выпуска** режим. Теперь расширение упаковываются как VSIX в папку \bin\Release.

3. Дважды щелкните VSIX для проверки установки.

## <a name="test-the-extension"></a>Тестирование расширения

 Перед распространением расширения построения и тестирования, чтобы убедиться, что она правильно установлена в экспериментальном экземпляре Visual Studio.

1. В Visual Studio начните отладку. Чтобы открыть экспериментальный экземпляр Visual Studio.

2. В экспериментальном экземпляре откройте **средства** меню и выберите пункт **расширения и обновления...** . Расширение TestPublish должны отображаться в центральной области и включаться.

3. На **средства** меню, убедитесь, что вы видите команду проверки.

## <a name="publish-the-extension-to-the-visual-studio-marketplace"></a>Публикация расширения для Visual Studio Marketplace

1. Убедитесь, что вы создали версии модуля и оно не устаревает.

2. В веб-браузере откройте [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) веб-сайта.

3. В правом верхнем углу, щелкните **входа**.

4. Войдите с помощью своей учетной записи Майкрософт. Если у вас учетной записи Майкрософт, можно создать один на этом этапе.

5. Нажмите кнопку **публикации расширения**.  Это произойдет переход на страницу "Управление" для всех расширений.  При отсутствии учетной записи издателя, будет предложено создать его в данный момент.

  ![Отправить в Marketplace](media/upload-to-marketplace.png)

6. Выберите издателя, которого вы хотите использовать для отправки расширения.  Издатели можно изменить, щелкнув имена издателей, перечисленные в левой части экрана.  Щелкните **новое расширение** и выберите **Visual Studio**.

7. В **1: загрузить расширение**, вы можете отправить VSIX-файл непосредственно в Visual Studio Marketplace или просто добавить ссылку на собственных веб-сайта. В этом случае нам потребуется отправить расширения, TestPublish.vsix.  Перетяните или использовать расширение **щелкните** ссылку, чтобы перейти к файлу.  Расширения можно найти в папке \bin\Release проекта.  Нажмите кнопку **Продолжить**.

8. В **2: предоставляют сведения о расширении**, некоторые поля заполняются автоматически в файле source.extension.vsixmanifest из расширения.  Дополнительные сведения о каждом находятся ниже:

    * **Внутреннее имя** будет использоваться URL-адрес страницы сведений о расширении. Например, публикации расширения в списке имя издателя «myname» и указав внутреннее имя для «myextension» приведет к URL-адрес «marketplace.visualstudio\.com/items?itemName=myname.myextension» для конкретного модуля страница сведений.
    
    * **Отображаемое имя** расширения.  Это автоматически заполняется из файла source.extension.vsixmanifest.
   
    * **Версия** номеров расширения, которые вы отправляете.  Это автоматически заполняется из файла source.extension.vsixmanifest.
    
    * **Идентификатор VSIX** — уникальный идентификатор, используемый Visual Studio для расширения.  Это необходимо, если вы хотите расширением будет обновлен автоматически.  Это автоматически заполняется из файла source.extension.vsixmanifest.
    
   * **Эмблема** будет использоваться для модуля.  Это будет автоматически заполняется из файла source.extension.vsixmanifest, если указано.
    
    * **Краткое описание** делает расширения.  Это будет автоматически заполняется из файла source.extension.vsixmanifest.
    
    * **Общие сведения о** удобен для включения снимки экрана и подробные сведения о назначении расширения.
    
    * **Поддерживаемые версии Visual Studio** позволяет выбрать, какие версии Visual Studio расширение будет работать на.  Расширение будет установлено только для этих версий.
    
    * **Поддерживаемые выпуски Visual Studio** позволяет выбрать, какие выпуски Visual Studio расширение будет работать на.  Расширение будет установлено только в этих выпусках.
    
    * **Тип**.  Наиболее распространенный тип расширения, **средства**.
    
    * **Категории**.  Выберите до трех файлов, которые лучше всего подходит для вашего расширения.
    
    * **Теги** являются ключевые слова, которые помогают пользователям найти расширение. Теги можно повысить Релевантность поиска расширений в Marketplace.
    
    * **Ценовой категории** затраты расширения.
    
    * **Репозиторий исходного кода** позволяет совместно использовать ссылку на исходный код с сообществом.
    
    * **Разрешить вопросы и ответы для модуля** даст пользователям возможность оставить вопросы на странице входа расширения.

9. Нажмите кнопку **сохранить и отправить**. Откроется страница управления обратно к издателю.  Расширение не опубликован.  Чтобы опубликовать модуль, щелкните правой кнопкой мыши расширение и выберите пункт **сделать общедоступным**.  Можно просмотреть, как расширение будет выглядеть как на Marketplace, выбрав **расширения представления**.  Для получения числа, нажмите кнопку **отчеты**.  Чтобы внести изменения в модуль, щелкните **изменить*.

  ![Элемент меню расширения](media/extension-entry-menu.png)

10. После нажатия кнопки **сделать общедоступным**, расширение теперь является открытым.  Поиск в Visual Studio Marketplace для модуля.

## <a name="add-additional-users-to-manage-your-publisher-account"></a>Добавить дополнительных пользователей, управление учетной записью издателя

Marketplace поддерживает предоставление дополнительным пользователям разрешения на доступ и управление учетной записью издателя.

1. Перейдите к учетной записи издателя, который вы хотите добавить дополнительных пользователей.

2. Выберите **элементы** и выберите команду **добавить**

  ![Добавить дополнительных пользователей](media/add-users.png)

3. Затем можно указать адрес электронной почты пользователя, который вы хотите добавить и предоставить правый уровень доступа в разделе **выберите роль**.  Доступны следующие варианты.

  * **Создатель**: пользователь публикации расширения, но не может просматривать и управлять расширения, опубликованные другими пользователями.
  
  * **Модуль чтения**: пользователь может просматривать расширения, но нельзя опубликовать или управлять расширениями.
  
  * **Участник**: пользователь может публикации и управления расширениями, но нельзя изменить настройки издателя или Управление доступом.
  
  * **Владелец**: пользователь может публиковать и управлять расширениями, изменить настройки издателя и управление доступом.
  
## <a name="install-the-extension-from-the-visual-studio-marketplace"></a>Установить расширение в Visual Studio Marketplace

Теперь, когда публикуется расширения, установите его в Visual Studio и протестируйте его.

1. В Visual Studio на **средства** меню, нажмите кнопку **расширения и обновления...** .

2. Нажмите кнопку **Online** и выполните поиск TestPublish.

3. Нажмите **Загрузить**. Затем модуль будут запланированы для установки.

4. Чтобы завершить установку, закройте все экземпляры Visual Studio.

## <a name="remove-the-extension"></a>Удалите расширение

Расширение можно удалить из Visual Studio Marketplace и с вашего компьютера.

### <a name="to-remove-the-extension-from-the-visual-studio-marketplace"></a>Чтобы удалить модуль из Visual Studio Marketplace

1. Откройте [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) веб-сайта.

2. В правом верхнем углу щелкните **публикации** расширения.  Выберите издателя, используемый для публикации TestPublish.  Отображается список для TestPublish.

3. Щелкните правой кнопкой мыши щелкните запись расширения и нажмите кнопку **удалить** будет предложено подтвердить, следует ли удалить расширение.  Нажмите кнопку **ОК**.

### <a name="to-remove-the-extension-from-your-computer"></a>Чтобы удалить расширение с компьютера

1. В Visual Studio на **средства** меню, нажмите кнопку **расширения и обновления...** .

2. Выберите TestPublish и нажмите кнопку **удаления**. Расширение планируется для удаления.

3. Чтобы завершить удаление, закройте все экземпляры Visual Studio.
