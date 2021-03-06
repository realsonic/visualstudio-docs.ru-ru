---
title: Обработка исключения параллельности
ms.date: 09/11/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- concurrency control, exceptions
- datasets [Visual Basic], errors
- exception handling, concurrency issues
- data concurrency, walkthroughs
- updating datasets, errors
- concurrency control, walkthroughs
ms.assetid: 73ee9759-0a90-48a9-bf7b-9d6fc17bff93
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 24338b2a6bc49a9a1a2a77e6395f60013c4465b7
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="handle-a-concurrency-exception"></a>Обработка исключения параллельности
Исключения параллелизма (<xref:System.Data.DBConcurrencyException>) возникают при попытке двух пользователей изменить те же данные в базе данных в то же время. В этом пошаговом руководстве, создание приложения Windows, которое показывает, как перехватить <xref:System.Data.DBConcurrencyException>, найдите строку, которая вызвала ошибку и Узнайте стратегии для их обработки.

 В этом пошаговом руководстве рассматривается процесс.

1.  Создайте проект **приложения Windows Forms**.

2.  Создать новый набор данных на основании Northwind `Customers` таблицы.

3.  Создание формы с <xref:System.Windows.Forms.DataGridView> для отображения данных.

4.  Заполнить набор данных данными из `Customers` таблицы в базе данных "Борей".

5.  Используйте **Показать таблицу данных** компонентов в **обозревателя серверов** для доступа к `Customers` данных и запись изменений таблицы.

6.  Изменить ту же запись с другим значением, обновление набора данных и попытка записать изменения в базу данных, что приводит к возникновению ошибки одновременного доступа.

7.  Перехватить ошибку, а затем отобразить различные версии записей, предоставляя пользователю возможность продолжить обновление базы данных, либо отменить обновление.

## <a name="prerequisites"></a>Предварительные требования
В этом пошаговом руководстве используется SQL Server Express LocalDB и базе данных Northwind.

1.  Если у вас нет SQL Server Express LocalDB, установите его из [страницы загрузки SQL Server Express](https://www.microsoft.com/sql-server/sql-server-editions-express), либо с помощью **установщик Visual Studio**. Установщик Visual Studio можно установить SQL Server Express LocalDB в рамках **хранения и обработки данных** рабочей нагрузки, или в отдельных компонентов.

2.  Установка образца базы данных Northwind, выполните следующие действия:

    1. В Visual Studio откройте **обозреватель объектов SQL Server** окна. (Обозреватель объектов SQL Server устанавливается как часть **хранения и обработки данных** рабочей нагрузки в установщик Visual Studio.) Разверните **SQL Server** узла. Щелкните правой кнопкой мыши на экземпляре LocalDB и выберите **нового запроса...** .

       Откроется окно редактора запросов.

    2. Копировать [сценарий Northwind Transact-SQL](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) в буфер обмена. Этот скрипт T-SQL создает базу данных Northwind с нуля и заполняет ее данными.

    3. Вставьте скрипт T-SQL в редакторе запросов, а затем выберите **Execute** кнопки.

       Через некоторое время завершения выполнения запроса и создания базы данных "Борей".

> [!NOTE]
>  Диалоговые окна и команды меню могут отличаться от описанных в справке в зависимости от текущих параметров или выпуска, которую вы используете. Чтобы изменить параметры, выберите в меню **Сервис** пункт **Импорт и экспорт параметров** . Дополнительные сведения см. в разделе [Персонализация интегрированной среды разработки Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="create-a-new-project"></a>Создание нового проекта
 Пошаговое руководство начинается с создания нового приложения Windows Forms.

#### <a name="to-create-a-new-windows-forms-application-project"></a>Создание проекта приложения Windows Forms

1. В Visual Studio на **файл** последовательно выберите пункты **New**, **проекта...** .

2. Разверните **Visual C#** или **Visual Basic** на левой панели, затем выберите **классического Windows**.

3. В средней области выберите **приложение Windows Forms** тип проекта.

4. Назовите проект **ConcurrencyWalkthrough**, а затем выберите **ОК**.

     **ConcurrencyWalkthrough** создается и добавляется в проект **обозревателе решений**, и открывает новую форму в конструкторе.

## <a name="create-the-northwind-dataset"></a>Создать набор данных "Борей"
 В этом разделе создается набор данных с именем `NorthwindDataSet`.

#### <a name="to-create-the-northwinddataset"></a>Создание NorthwindDataSet

1.  На **данные** меню, выберите **добавить новый источник данных**.

     [Мастер настройки источника данных](../data-tools/media/data-source-configuration-wizard.png) открывается.

2.  На **Выбор типа источника данных** выберите **базы данных**.

3.  Выберите подключение к учебной базе данных "Борей" в списке доступных подключений. Если подключение недоступно в списке подключений, выберите **нового подключения**

    > [!NOTE]
    >  Если вы подключаетесь к файлу локальной базы данных, выберите **нет** ответ на вопрос о том, как добавить файл в проект.

4.  На **Сохранение строки подключения в файле конфигурации приложения** выберите **Далее**.

5.  Разверните **таблиц** , а затем выберите `Customers` таблицы. Имя по умолчанию для набора данных должен быть `NorthwindDataSet`.

6.  Выберите **Готово** Добавление набора данных в проект.

## <a name="create-a-data-bound-datagridview-control"></a>Создание элемента управления DataGridView с привязкой к данным
 В этом разделе создайте <xref:System.Windows.Forms.DataGridView> , перетащив **клиентов** элемента из **источники данных** на форму Windows.

#### <a name="to-create-a-datagridview-control-that-is-bound-to-the-customers-table"></a>Создание элемента управления DataGridView, к которому привязана к таблице Customers

1.  На **данные** меню, выберите **Показать источники данных** Открытие **окно "Источники данных"**.

2.  В **источники данных** окна, разверните **NorthwindDataSet** узел, а затем выберите **клиентов** таблицы.

3.  Щелкните стрелку вниз на узле таблицы, а затем выберите **DataGridView** в раскрывающемся списке.

4.  Перетащите таблицу в пустую область формы.

     Объект <xref:System.Windows.Forms.DataGridView> управления с именем `CustomersDataGridView` и <xref:System.Windows.Forms.BindingNavigator> с именем `CustomersBindingNavigator` добавляются в форму, которая привязана к <xref:System.Windows.Forms.BindingSource>. Это в свою очередь привязан к `Customers` в таблицу `NorthwindDataSet`.

## <a name="test-the-form"></a>Проверить форму
 Теперь можно проверить форму, чтобы убедиться в том, что она работает так, как ожидалось до этой точки.

#### <a name="to-test-the-form"></a>Чтобы проверить форму

1.  Выберите **F5** для запуска приложения

     Появится форма с <xref:System.Windows.Forms.DataGridView> управления, который заполняется данными из `Customers` таблицы.

2.  На **отладки** последовательно выберите пункты **остановить отладку**.

## <a name="handle-concurrency-errors"></a>Обработка ошибок параллелизма
 Способ обработки ошибок зависит от конкретных бизнес-правила, управляющие приложения. В данном пошаговом руководстве мы используем следующие стратегии в качестве примера для обработки ошибок параллелизма.

 Приложение предоставляет пользователю три версии записи:

-   Текущая запись в базе данных

-   Исходная запись, которая загружается в наборе данных

-   Предлагаемые изменения в наборе данных

Затем пользователь может выполнять либо перезаписать базу данных предложенными изменениями или отменить обновление и обновить набор данных с новыми значениями из базы данных.

#### <a name="to-enable-the-handling-of-concurrency-errors"></a>Чтобы включить обработку ошибок параллелизма

1.  Создание настраиваемого обработчика ошибок.

2.  Параметры отображения для пользователя.

3.  Обработать ответ пользователя.

4.  Отправьте обновления или сбросьте данные в наборе данных.

### <a name="add-code-to-handle-the-concurrency-exception"></a>Добавьте код для обработки исключения параллельности
 При попытке выполнить обновление, и возникает исключение, обычно требуется сделать что-либо сведения, предоставляемые возникшее исключение.

 В этом разделе добавляется код, который пытается обновить базу данных. Можно также обрабатывать все <xref:System.Data.DBConcurrencyException> , могут возникать, а также любые другие исключения.

> [!NOTE]
>  `CreateMessage` И `ProcessDialogResults` методы, которые будут добавлены позже в этом пошаговом руководстве.

##### <a name="to-add-error-handling-for-the-concurrency-error"></a>Чтобы добавить обработку ошибок совместного доступа

1.  Добавьте следующий код ниже `Form1_Load` метод:

     [!code-csharp[VbRaddataConcurrency#1](../data-tools/codesnippet/CSharp/handle-a-concurrency-exception_1.cs)]
     [!code-vb[VbRaddataConcurrency#1](../data-tools/codesnippet/VisualBasic/handle-a-concurrency-exception_1.vb)]

2.  Замените `CustomersBindingNavigatorSaveItem_Click` метод, вызываемый `UpdateDatabase` метод, чтобы он выглядел следующим образом:

     [!code-csharp[VbRaddataConcurrency#2](../data-tools/codesnippet/CSharp/handle-a-concurrency-exception_2.cs)]
     [!code-vb[VbRaddataConcurrency#2](../data-tools/codesnippet/VisualBasic/handle-a-concurrency-exception_2.vb)]

### <a name="display-choices-to-the-user"></a>Параметры отображения для пользователя
 Код, который только что написанный вызывает `CreateMessage` процедуру для отображения сведений об ошибке пользователю. В этом пошаговом руководстве используется окно сообщения для отображения различных версий записи для пользователя. Это позволяет пользователю выбрать, следует ли перезаписать запись с изменениями или отменить изменения. Когда пользователь выбирает параметр (нажимает кнопку) в окне сообщения, ответ передается `ProcessDialogResult` метод.

##### <a name="to-create-the-message-to-display-to-the-user"></a>Чтобы создать сообщение, отображаемое для пользователя

-   Создать сообщение, добавив следующий код в **редактор кода**. Введите следующий код ниже `UpdateDatabase` метод.

     [!code-csharp[VbRaddataConcurrency#4](../data-tools/codesnippet/CSharp/handle-a-concurrency-exception_3.cs)]
     [!code-vb[VbRaddataConcurrency#4](../data-tools/codesnippet/VisualBasic/handle-a-concurrency-exception_3.vb)]

### <a name="process-the-users-response"></a>Обработка ответа пользователя
 Также требуется код для обработки ответа пользователя для окна сообщения. Параметры, чтобы перезаписать текущую запись в базе данных с помощью предлагаемого изменения или отменить локальные изменения и обновить таблицу данных с записью в данный момент базы данных. Если Да, пользователь <xref:System.Data.DataTable.Merge%2A> метод вызывается с *preserveChanges* аргументу присвоено `true`. В результате попытки обновления было успешным, поскольку исходная версия записи теперь совпадает с записью в базе данных.

##### <a name="to-process-the-user-input-from-the-message-box"></a>Для обработки пользовательского ввода из окна сообщений

-   Добавьте следующий код ниже кода, который был добавлен в предыдущем разделе.

     [!code-csharp[VbRaddataConcurrency#3](../data-tools/codesnippet/CSharp/handle-a-concurrency-exception_4.cs)]
     [!code-vb[VbRaddataConcurrency#3](../data-tools/codesnippet/VisualBasic/handle-a-concurrency-exception_4.vb)]

## <a name="test-the-form"></a>Проверить форму
 Теперь можно проверить форму, чтобы убедиться в том, что оно правильно работает. Для имитации нарушение параллелизма, вам нужно изменить данные в базе данных после заполнения NorthwindDataSet.

#### <a name="to-test-the-form"></a>Чтобы проверить форму

1.  Выберите **F5** для запуска приложения.

2.  После отображения формы оставьте ее запущенной и переключитесь в Интегрированной среде разработки Visual Studio.

3.  На **представление** меню, выберите **обозревателя серверов**.

4.  В **обозревателя серверов**, разверните подключение с помощью приложения, а затем разверните **таблиц** узла.

5.  Щелкните правой кнопкой мыши **клиентов** таблицы, а затем выберите **Показать таблицу данных**.

6.  В первой записи (`ALFKI`) изменить `ContactName` для `Maria Anders2`.

    > [!NOTE]
    >  Перейдите в другую строку, чтобы применить изменение.

7.  Переключитесь в `ConcurrencyWalkthrough`на запущенную форму.

8.  В первой записи в форме (`ALFKI`), изменить`ContactName` для `Maria Anders1`.

9. Выберите **Сохранить** кнопки.

     Возникает ошибка параллелизма, и появится окно сообщения.

10. При выборе **нет** отменяет обновление и обновление набора данных со значениями, которые в данный момент в базе данных. При выборе **Да** записывает предложенное значение в базу данных.

## <a name="see-also"></a>См. также

- [Сохранение данных обратно в базу данных](../data-tools/save-data-back-to-the-database.md)