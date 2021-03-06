---
title: Устранение неполадок установки
description: Иногда возникают проблемы. Если происходит сбой установки или обновления Visual Studio, эта страница может помочь решить проблему.
ms.date: 11/21/2017
ms.technology: vs-acquisition
ms.prod: visual-studio-dev15
ms.topic: troubleshooting
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 556EDD3F-E365-43EE-B3DD-03AA4353F75B
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f0009aa15919cf04c3ff8e56edf4f10adcb7e0ea
ms.sourcegitcommit: 4c0bc21d2ce2d8e6c9d3b149a7d95f0b4d5b3f85
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/20/2018
---
# <a name="troubleshooting-visual-studio-2017-installation-and-upgrade-issues"></a>Устранение неполадок при установке и обновлении Visual Studio 2017

## <a name="symptoms"></a>Симптомы

Операция установки или обновления Visual Studio 2017 завершается ошибкой.

## <a name="workaround"></a>Обходной путь

Чтобы обойти эту проблему, выполните следующие действия.

### <a name="step-1---check-whether-this-problem-is-a-known-issue"></a>Шаг 1. Проверьте, не связана ли эта ошибка с известными проблемами

Существуют несколько известных проблем с установщиком Visual Studio, и корпорация Майкрософт работает над их устранением. Чтобы найти способ обойти эту проблему, проверьте [раздел известных проблем в заметках о выпуске](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#known-issues).

### <a name="step-2---check-with-the-developer-community"></a>Шаг 2. Обратитесь к сообществу разработчиков

Попробуйте найти полученное сообщение об ошибке в [сообществе разработчиков Visual Studio](https://developercommunity.visualstudio.com/spaces/8/index.html). Возможно, другие члены сообщества уже описали решение для вашей проблемы.

### <a name="step-3---delete-the-visual-studio-installer-directory-to-fix-upgrade-problems"></a>Шаг 3. Удалите каталог с установщиком Visual Studio, чтобы устранить проблемы, связанные с обновлением

Загрузчик установщика Visual Studio представляет собой минимально необходимый исполняемый файл небольшого размера, который устанавливает остальную часть установщика Visual Studio. Если вы удалите файлы установщика Visual Studio и повторно запустите загрузчик, это может решить некоторые ошибки, связанные с обновлением.

>[!NOTE]
С помощью следующей процедуры можно переустановить файлы Visual Studio Installer и сбросить метаданные установки.

1. Закройте установщик Visual Studio.
2. Удалите каталог установщика Visual Studio. Как правило, это каталог `C:\Program Files (x86)\Microsoft Visual Studio\Installer`.
3. Запустите загрузчик установщика Visual Studio. Файл загрузчика вы можете найти в папке загрузок. Его имя будет соответствовать формату `vs_[Visual Studio edition]__*.exe`. Если вы не найдете это приложение, можно заново скачать загрузчик со [страницы загрузки Visual Studio](https://www.visualstudio.com/downloads/), нажав кнопку **Скачать** для нужного выпуска Visual Studio. Запустите этот исполняемый файл, чтобы сбросить метаданные установки.
4. Снова попробуйте установить или обновить Visual Studio. Если запуск установщика снова завершится ошибкой, переходите к следующему шагу.

### <a name="step-4---report-a-problem"></a>Шаг 4. Сообщите о проблеме

В некоторых ситуациях, например при повреждении файлов, может потребоваться рассмотреть конкретную ситуацию.

1. Соберите файлы журналов установки. Подробные сведения см. в разделе [Как получить журналы установки Visual Studio](#how-to-get-the-visual-studio-installation-logs).
2. Откройте установщик Visual Studio и нажмите кнопку **Сообщить о проблеме**, чтобы открыть средство обратной связи Visual Studio.
![Чтобы открыть средство обратной связи, можно перейти к кнопе "Предоставление отзыва" с помощью клавиши табуляции](media/report-a-problem.png)
3. Присвойте заголовок вашему отчету об ошибке и опишите все важные сведения. Нажмите кнопку **Далее**, чтобы перейти к разделу **Вложения**, а затем вложите созданный файл журнала (обычно этот файл находится по пути `%TEMP%\vslogs.zip`).
4. Щелкните **Далее**, чтобы просмотреть свой отчет об ошибках, а затем нажмите кнопку **Отправить**.

### <a name="step-5---run-installcleanupexe-to-remove-installation-files"></a>Шаг 5. Выполнение программы InstallCleanup.exe для удаления файлов установки

В качестве последнего средства можно [удалить Visual Studio](remove-visual-studio.md), чтобы удалить все файлы установки и сведения о продукте.

1. Следуйте инструкциям в разделе [Удаление Visual Studio](remove-visual-studio.md).
2. Повторно запустите загрузчик, описанный в разделе [Шаг 3. Удалите каталог с установщиком Visual Studio, чтобы устранить проблемы, связанные с обновлением](#step-3---delete-the-visual-studio-installer-directory-to-fix-upgrade-problems).
3. Снова попробуйте установить или обновить Visual Studio.

### <a name="step-6---contact-us-optional"></a>Шаг 6. Связь с нами (необязательно)

Если ни один из описанных выше шагов не позволил успешно выполнить установку, вы можете обратиться к нам за помощью в чате в реальном времени (только на английском языке). Дополнительные сведения см. на [странице поддержки Visual Studio](https://www.visualstudio.com/vs/support/#talktous).

## <a name="how-to-troubleshoot-an-offline-installer"></a>Устранение неполадок с автономным установщиком

Здесь мы приводим список известных проблем при установке из локального макета и варианты обходных действий, которые могут оказаться полезными.

| Проблеми       | Элемент                   | Решение |
| ----------- | ---------------------- | -------- |
| У пользователей отсутствуют права доступа к файлам. | Разрешения (ACL) | *Прежде* чем открывать общий доступ к автономной установке, необходимо настроить разрешения (ACL) и предоставить пользователям права на чтение. |
| Не удается установить новые рабочие нагрузки, компоненты или языки.  | `--layout`  | Если вы производите установку из частичного макета и выбираете рабочие нагрузки, компоненты или языки, которые не скачаны в этот макет, вам потребуется доступ в Интернет. |

## <a name="how-to-get-the-visual-studio-installation-logs"></a>Как получить журналы установки Visual Studio

Для устранения большинства неполадок при установке необходимы журналы установки. При отправке проблемы с помощью средства [сообщения о проблеме](../ide/how-to-report-a-problem-with-visual-studio-2017.md) в Visual Studio Installer эти журналы автоматически включаются в отчет.

Если вы обращаетесь в службу поддержки Майкрософт, для отправки этих журналов установки может понадобиться [средство сбора журналов для Microsoft Visual Studio и .NET Framework](https://aka.ms/vscollect). Средство сбора журналов собирает журналы установки для всех компонентов, устанавливаемых программой Visual Studio 2017, включая .NET Framework, пакет SDK для Windows и SQL Server. Оно также собирает сведения о компьютере, данные инвентаризации установщика Windows и сведения журнала событий Windows для Visual Studio Installer, установщика Windows и восстановления системы.

Чтобы собрать журналы, выполните указанные ниже действия.

1. [Скачайте средство](https://aka.ms/vscollect).
2. Откройте командную строку от имени администратора.
3. Запустите файл `Collect.exe` из каталога, в котором сохранено средство.
4. Найдите итоговый файл `vslogs.zip` в каталоге `%TEMP%`, например `C:\Users\YourName\AppData\Local\Temp\vslogs.zip`.

> [!NOTE]
> Запускайте средство с помощью той же учетной записи пользователя, с помощью которой запускалась завершившаяся сбоем установка. Если вы запускаете средство с помощью другой учетной записи, задайте параметр `–user:<name>`, чтобы указать учетную запись пользователя, с помощью которой запускалась завершившаяся сбоем установка. Чтобы просмотреть дополнительные параметры и сведения об использовании, запустите `Collect.exe -?` из командной строки администратора.

## <a name="more-support-options"></a>Дополнительные варианты поддержки

Если ни один из описанных выше шагов не позволил успешно выполнить установку, вы можете обратиться к нам за помощью в чате в реальном времени (только на английском языке). Дополнительные сведения см. на [странице поддержки Visual Studio](https://www.visualstudio.com/vs/support/#talktous).

Ниже приведены несколько дополнительных вариантов.

* Вы можете сообщить о проблемах с продуктом в корпорацию Майкрософт, используя средство [Сообщить о проблеме](../ide/how-to-report-a-problem-with-visual-studio-2017.md). Оно доступно как в Visual Studio Installer, так и в Visual Studio IDE.
* Вы можете оставить предложение о продукте на форуме [UserVoice](https://visualstudio.uservoice.com/forums/121579).
* Вы можете просматривать описания проблем и искать решения в [сообществе разработчиков Visual Studio](https://developercommunity.visualstudio.com/).
* Вы также можете связаться с нами и другими разработчиками Visual Studio, используя [средство для обсуждения Visual Studio в сообществе Gitter](https://gitter.im/Microsoft/VisualStudio). (Требуется учетная запись [GitHub](https://github.com/).)

## <a name="see-also"></a>См. также

* [Руководство администратора Visual Studio](visual-studio-administrator-guide.md)
* [Средства для обнаружения экземпляров Visual Studio и управления ими](tools-for-managing-visual-studio-instances.md)
* [Удаление Visual Studio 2017](remove-visual-studio.md)
