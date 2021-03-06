---
title: Отладка многопоточных приложений
description: Отладка с помощью окну «потоки» и панель инструментов Место отладки в Visual Studio
ms.custom: ''
ms.date: 05/18/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- multithreaded debugging, tutorial
- tutorials, multithreaded debugging
ms.assetid: adfbe002-3d7b-42a9-b42a-5ac0903dfc25
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 37a9161011031c53ed16a9ab0918eb498f5fa270
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="walkthrough-debug-a-multithreaded-application-in-visual-studio-using-the-threads-window"></a>Пошаговое руководство: Отладка многопоточных приложений в Visual Studio, используя окно "Потоки"
Visual Studio предоставляет **потоков** окна и другие пользовательского интерфейса элементов для отладки многопоточных приложений. Этот учебник показывает, как использовать **потоков** окна и **место отладки** инструментов. Сведения о других средствах см. в разделе [Начало отладки многопоточных приложений](../debugger/get-started-debugging-multithreaded-apps.md). Этот учебник занимает всего несколько минут, но оно позволит ознакомиться со средствами для отладки многопоточных приложений.   
  
Чтобы начать работу с учебником, необходим проект многопоточного приложения. Выполните следующие действия для создания этого проекта.  
  
#### <a name="to-create-the-multithreaded-app-project"></a>Чтобы создать проект многопоточного приложения  
  
1.  На **файл** меню, выберите **New** и нажмите кнопку **проекта**.  
  
     Откроется диалоговое окно **Новый проект** .  
  
2.  В **тип проекта**s выберите язык: **Visual Basic**, **Visual C#**, или **Visual C++**.  
  
3.  В **шаблоны** выберите **консольного приложения**.  
  
4.  В **имя** введите имя MyThreadWalkthroughApp.  
  
5.  Нажмите кнопку **ОК**.  
  
     Появится новый проект консольного приложения. Когда проект будет создан, откроется файл исходного кода. В зависимости от выбранного языка файл исходного кода может называться Module1.vb, Program.cs или MyThreadWalkthroughApp.cpp  
  
6.  Удалите код, который отображается в исходном файле и замените пример кода, который отображается в разделе «Создание потока» раздела [создание потоков и передача данных во время запуска](/dotnet/standard/threading/creating-threads-and-passing-data-at-start-time).  
  
7.  На **файл** меню, нажмите кнопку **сохранить все**.  
  
#### <a name="to-begin-the-tutorial"></a>Чтобы приступить к изучению учебника  
  
-   В редакторе исходного кода найдите следующий код:  
  
    ```VB  
    Thread.Sleep(3000)   
    Console.WriteLine()
    ```  
  
    ```csharp  
    Thread.Sleep(3000);  
    Console.WriteLine();  
    ```  
  
    ```C++  
    Thread::Sleep(3000);  
    Console.WriteLine();  
    ```  
  
#### <a name="to-start-debugging"></a>Начало отладки  
  
1.  Щелкните в левом поле `Console.WriteLine` инструкцию, чтобы добавить новую точку останова.  
  
     Во внутренней области левой части редактора исходного кода появится красный кружок. Это означает, что точка останова установлена в этом месте.  
  
2.  На **отладки** меню, нажмите кнопку **начать отладку** (**F5**).  
  
     Начнется отладка, консольное приложение запустится и прервется на точке останова.  
  
3.  Если в этот момент фокус находится на окне консольного приложения, щелкните окно [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] для возвращения фокуса в [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].  
  
4.  В редакторе исходного кода найдите строку, содержащую следующий код:  
  
    ```VB  
    Thread.Sleep(5000)   
    ```  
  
    ```csharp  
    Thread.Sleep(3000);  
    ```  
  
    ```C++  
    Thread::Sleep(3000);  
    ```
  
#### <a name="to-discover-the-thread-marker"></a>Чтобы обнаружить маркер потока  

1.  В панели инструментов отладки нажмите **Показать потоки в исходном коде** кнопку ![Показать потоки в исходном коде](../debugger/media/dbg-multithreaded-show-threads.png "ThreadMarker"). 
  
2.  Посмотрите на переплет в левой части окна. В этой строке, вы увидите *маркер потока* значок ![маркер потока](../debugger/media/dbg-thread-marker.png "ThreadMarker") имеет вид 2 тряпичных нити. маркер потока указывает, что некий поток остановлен в этом месте.  
  
3.  Наведите указатель мыши на маркер потока. Появится подсказка. Подсказка сообщает имя и идентификационный номер каждого остановившегося тут потока. В нашем случае существует только один поток, имя которого, вероятно, `<noname>`.  

    > [!TIP]
    > Могут оказаться полезными для определения безымянных потоков, переименовав их. В окне «потоки» выберите **переименование** , щелкнув **имя** столбца в строке потока.
  
4.  Щелкните правой кнопкой мыши маркер потока, чтобы просмотреть доступные параметры контекстного меню. 
    
  
## <a name="flagging-and-unflagging-threads"></a>Пометка потоков и ее снятие  
Можно пометить поток, требуется уделить особое внимание. Пометка потоков — хороший способ, чтобы отслеживать важные потоки и игнорировать потоков, которые не важна.  
  
#### <a name="to-flag-threads"></a>Чтобы пометить потоки   

1.  На **представление** последовательно выберите пункты **панели инструментов**.  
  
    Убедитесь, что **место отладки** выбранных инструментов.

2.  Последовательно выберите пункты **место отладки** инструментов и выберите команду **потоков** списка.  
  
    > [!NOTE]
    >  Эта панель инструментов можно узнать по трем заметным спискам: **процесс**, **потоков**, и **кадр стека**.  
  
3.  Обратите внимание, сколько потоков отображается в списке.  
  
4.  Вернитесь в редакторе исходного кода и щелкните правой кнопкой мыши маркер потока ![маркер потока](../debugger/media/dbg-thread-marker.png "ThreadMarker") еще раз.  
  
5.  В контекстном меню пункты **флаг**и затем щелкните имя потока и ИД.  
  
6.  Вернитесь к **место отладки** инструментов и найдите **Показывать только отмеченные потоки** значок ![Показывать отмеченные потоки](../debugger/media/dbg-threads-show-flagged.png "ThreadMarker") для справа от **потоков** списка.  
  
    Значок флаги на кнопке ранее был тусклым. Теперь это активной кнопка.  
  
7.  Нажмите кнопку **Показывать только отмеченные потоки** значок.  
  
    Теперь в списке отображаются только отмеченные потоки. (Можно щелкнуть кнопку одного флага для переключения обратно в **Показывать все потоки** режиме.)

8. Откройте окно "Потоки", выбрав **Отладка > Windows > потоков**.

    ![Окно потоков](../debugger/media/dbg-threads-window.png "ThreadsWindow")  
  
    В **потоков** окно, отмеченному потоку имеет красный прикреплен заметный значок флага на него.

    > [!TIP]
    > Когда отметкой некоторые потоки можно правой кнопкой мыши строку кода в редакторе кода и выбрать **запуска отмеченные потоки до курсора** (не забудьте выбрать код, что все отмеченные потоки достигнет). Это приостанавливает потоки в выбранной строке кода, делая его проще управлять порядком выполнения по [Замораживание и размораживание потоков](#bkmk_freeze).
  
11. В редакторе исходного кода щелкните правой кнопкой мыши маркер потока еще раз.  
  
     Обратите внимание, какие варианты сейчас доступны в контекстном меню. Вместо **флаг**, теперь отображается **снять отметку**. Не нажимайте кнопку **снять отметку**.  

     Чтобы узнать, как снять отметку с потока, перейдите к следующей процедуре.  
  
#### <a name="to-unflag-threads"></a>Чтобы снять отметку с потока  
  
1.  В **потоков** окно, щелкните правой кнопкой мыши строку, соответствующую отмеченному потоку.  
  
     Появится контекстное меню. Он содержит параметры, **снять отметку** и **снять пометку со всех потоков**.  
  
2.  Чтобы снять отметку с потока, щелкните **снять отметку**.  

    Посмотрите на **место отладки** инструментов еще раз. **Показывать только отмеченные потоки** кнопка затемнена еще раз. Вы сняли отметку с только что отмеченного потока. Поскольку отсутствуют отмеченные потоки, панель инструментов вернулась в **Показывать все потоки** режим. Нажмите кнопку **потоков** и убедитесь, что отображаются все потоки.  
  
5.  Вернитесь к **потоков** окна и просмотрите колонки сведений.  
  
    В первом столбце можно заметить структуры значок флага в каждой строке списка потоков. (Контур означает, что поток не отмечен).  
  
6.  Щелкните значок флага структуры для двух потоков, второго и третьего снизу в списке. 

    Вместо контуров будут отображаться значки красных флагов.  
  
7.  Нажмите кнопку в заголовке колонки флагов.  
  
    Порядок в списке потоков изменился, когда была нажата кнопка. Список потоков теперь отсортирован так, что отмеченные потоки располагаются в верху списка.  
  
8.  Снова нажмите кнопку в заголовке колонки флагов.  
  
    Порядок сортировки изменился еще раз.  
  
## <a name="more-about-the-threads-window"></a>Дополнительные сведения об окне "Потоки"  
  
#### <a name="to-learn-more-about-the-threads-window"></a>Чтобы получить дополнительные сведения об окне "Потоки"  
  
1.  В **потоков** окна, просмотрите третий столбец слева. Кнопка в верхней части этого столбца называется **идентификатор**.  
  
2.  Нажмите кнопку **идентификатор**.  
  
     Теперь список потоков отсортирован по идентификатору потока.  
  
3.  Щелкните правой кнопкой мыши любой поток в списке. В контекстном меню щелкните **Шестнадцатеричный вывод**.  
  
     Формат идентификаторов потоков изменился.  
  
4.  Наведите указатель мыши на **расположение** столбца для любой поток в списке.  
  
     После небольшой задержки появится Подсказка Данных. Она отображает частичный стек вызова для этого потока.

     > [!TIP]
     > Графическое представление стеки вызовов для потоков, откройте [Параллельные стеки](../debugger/using-the-parallel-stacks-window.md) окна (во время отладки, выберите **отладка / Windows / Параллельные стеки**).  
  
5.  Просмотрите четвертый столбец слева, который называется **категории**. Потоки делятся на категории.  
  
     Первый поток, созданный в процессе, называется "основной поток". Найдите его в списке потоков.  
  
6.  Щелкните правой кнопкой мыши основной поток и выберите **переключиться на поток**.  
  
     Объект **прервать режим** появится окно. Он указывает, что отладчик не выполняется в настоящее время любой код, который он может отображать (так как он является основным потоком).   
  
7.  Посмотрите на **стек вызовов** окна и **место отладки** инструментов.  
  
     Содержимое **стек вызовов** окна были изменены. 

## <a name="bkmk_freeze"></a> Замораживание и размораживание потоков 

Можно заморозить или разморозить (приостанавливать и возобновлять) потоки для управления порядком, в котором потоки выполнения работы. Это может помочь при устранении проблем параллелизма, например взаимоблокировки и состояние гонки.

> [!TIP]
> Если вы хотите следовать один поток не замораживание других потоков (также отладки чаще) см. в разделе [Начало отладки многопоточных приложений](../debugger/get-started-debugging-multithreaded-apps.md#bkmk_follow_a_thread).
  
#### <a name="to-freeze-and-unfreeze-threads"></a>Чтобы заморозить и разморозить потоки  
  
1.  В **потоков** , щелкните правой кнопкой мыши любой поток и выберите **закрепить**.  
  
2.  Просмотрите второй столбец (текущий поток столбец). Существует появится значок паузы. Эти значок паузы указывает, что поток заморожен.  
  
3.  Показать **счетчик приостановок** столбца, выбрав ее в **столбцы** списка.

    Счетчик приостановки для потока теперь имеет значение 1.  
  
4.  Щелкните правой кнопкой мыши замороженный поток и выберите **Разморозить**.  
  
     Столбец текущего потока и **счетчик приостановок** изменения столбцов. 
  
## <a name="switching-the-to-another-thread"></a>Переключение на другой поток 
  
#### <a name="to-switch-threads"></a>Чтобы переключаться между потоками  
  
1.  В **потоков** окна, просмотрите второй столбец слева (текущий поток столбец). Кнопка в верхней части этого столбца не содержит текста или значка.
  
2.  Посмотрите на столбец текущего потока и обратите внимание, что у одного потока есть желтая стрелка. Желтая стрелка указывает на этот поток текущий поток (это в настоящий момент указатель выполнения).
  
    Запишите идентификатор потока где появится значок текущего потока. Значок текущего потока будет переместить в другой поток, но необходимо будет скопировать обратно после завершения. 
  
3.  Щелкните правой кнопкой мыши другой поток, а затем нажмите кнопку **переключиться на поток**.  
  
4.  Посмотрите на **стек вызовов** окно в редакторе исходного кода. Его содержимое изменилось.  
  
5.  Посмотрите на **место отладки** инструментов. Значок текущего потока изменилась в существует, слишком.  
  
6.  Последовательно выберите пункты **место отладки** инструментов. Выберите другой поток, **поток** списка.  
  
7.  Посмотрите на **потоков** окна. Значок текущего потока был изменен.  
  
8. В редакторе исходного кода щелкните правой кнопкой мыши маркер потока. В контекстном меню пункты **переключиться на поток** и щелкните имя или идентификатор потока.  
  
     Было рассмотрено три способа изменения значок текущего потока на другой поток: с помощью **потоков** окне **поток** списка в **место отладки** инструментов и маркер потока в редакторе исходного кода.  
  
     С маркер потока можно переключаться только на потоки, остановленные в этом конкретном расположении. С помощью **потоков** окна и **место отладки** инструментов, можно переключиться на любой поток.   
  
## <a name="see-also"></a>См. также  
 [Отладка многопоточных приложений](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [Практическое руководство. Переключение на другой поток при отладке](../debugger/how-to-switch-to-another-thread-while-debugging.md)
