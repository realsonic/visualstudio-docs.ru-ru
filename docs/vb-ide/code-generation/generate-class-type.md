---
title: "Создайте класс или тип - формирования кода (Visual Basic) | Документы Microsoft"
ms.custom: 
ms.date: 11/17/2016
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
ms.devlang: VB
ms.assetid: ebc361fe-d9b1-4c7a-ae28-5e71b5775460
author: gewarren
ms.author: gewarren
manager: ghogen
f1_keywords: vsl.GenerateFromUsage
dev_langs: VB
ms.openlocfilehash: 1524d2899d8c775a20943d2695065bfe36885a25
ms.sourcegitcommit: f40311056ea0b4677efcca74a285dbb0ce0e7974
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2017
---
# <a name="generate-a-class-or-type-in-visual-basic"></a>Создание класса или типа в Visual Basic
**Что:** позволяет немедленно создать код для класса или типа. 

**Когда:** вводит новый класс или тип и чтобы правильно объявите ее, автоматически.  

**Почему:** можно объявить класс или тип перед их использованием, однако эта функция будет создать класс, или введите автоматически. 

**Как:**

1. Поместите курсор в строке которого красной волнистой линией, указывающее, используется класс, который еще не существует.

   ![Выделенный код](media/class_highlight.png)

1. Затем выполните одно из следующих действий.
   * **Клавиатура**
     * Нажмите клавишу **Ctrl +.** для запуска **Быстрые действия и рефакторинг** меню и выберите один из параметров из контекстного меню окна предварительного просмотра.
   * **Мышь**
     * Щелкните правой кнопкой мыши и выберите **Быстрые действия и рефакторинг** меню и выберите один из параметров из контекстного меню окна предварительного просмотра.
     * Наведите указатель мыши на красной волнистой линией и нажмите кнопку ![Лампочки](media/bulb.png) значок, который отображается.
     * Нажмите кнопку ![Лампочки](media/bulb.png) значок, который отображается в левом поле, если текст курсор уже находится в строке с красной волнистой линией.

   ![Создание предварительного просмотра класса](media/class_preview.png)

   Выбранное | Описание
   --- | ---
   Создание класса*TypeName*"в новый файл | Создает класс с именем *TypeName* в файле с именем *TypeName*.cs или .vb
   Создание класса*TypeName*" | Создает класс с именем *TypeName* в текущем файле.
   Создание вложенных классов*TypeName*" | Создает класс с именем *TypeName* вложена в текущем классе.
   Создать новый тип... | Создает новый класс или структура с все заданные свойства.

   >[!TIP]
   >Используйте [ **предварительного просмотра изменений** ](../../ide/preview-changes.md) ссылку в нижней части окна предварительного просмотра для просмотра всех изменений, сделанных перед началом выделения.

1. При выборе **сформировать новый тип...**  элемента, диалоговое окно появится всплывающее окно, позволяющий выполнить некоторые дополнительные действия.

   ![Создать тип](media/class_newtype.png)

   Выбранное | Описание
   --- | ---
   Access | Задайте тип иметь *по умолчанию*, *внутренний* или *открытый* доступа.
   Тип | Это можно задать в качестве *класса* или *структуры*.
   Имя | Это не может быть изменен и будет иметь имя, которое вы уже ввели.
   Проект | При наличии нескольких проектов в решении, можно выбрать место жизни класса или структуры.
   Имя файла | Можно создать новый файл или тип можно добавить в существующий файл.

1. Класса или структуры будут автоматически созданы с помощью конструктора выводиться из использования.

   ![Создать класс](media/class_result.png)

## <a name="see-also"></a>См. также  
[Создание кода (Visual Basic)](../code-generation-vb.md)  
[Просмотр изменений](../../ide/preview-changes.md)