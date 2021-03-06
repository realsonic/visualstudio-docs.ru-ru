---
title: 'CA1820: проверьте наличие пустых строк путем проверки длины строки'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- TestForEmptyStringsUsingStringLength
- CA1820
helpviewer_keywords:
- TestForEmptyStringsUsingStringLength
- CA1820
ms.assetid: da1e70c8-b1dc-46b9-8b8f-4e6e48339681
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 68e644a4e880f5468ec657f19efbf1a4f2d0c3d7
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="ca1820-test-for-empty-strings-using-string-length"></a>CA1820: проверьте наличие пустых строк путем проверки длины строки
|||
|-|-|
|TypeName|TestForEmptyStringsUsingStringLength|
|CheckId|CA1820|
|Категория|Microsoft.Performance|
|Критическое изменение|Не критическое|

## <a name="cause"></a>Причина
 Строка сравнивается с пустой строкой, используя <xref:System.Object.Equals%2A?displayProperty=fullName>.

## <a name="rule-description"></a>Описание правила
 Сравнение строк с помощью <xref:System.String.Length%2A?displayProperty=fullName> свойство или <xref:System.String.IsNullOrEmpty%2A?displayProperty=fullName> значительно быстрее, чем использование метода <xref:System.Object.Equals%2A>. Это вызвано <xref:System.Object.Equals%2A> выполняется значительно больший инструкции MSIL, чем любая <xref:System.String.IsNullOrEmpty%2A> или количество инструкций, который получает <xref:System.String.Length%2A> свойство значения, сравнивая ее с нуля.

 Следует иметь в виду, <xref:System.Object.Equals%2A> и <xref:System.String.Length%2A> == 0 ведут себя по-разному для строки null. При попытке получить значение <xref:System.String.Length%2A> на пустую строку, общеязыковая среда выполнения вызывает <xref:System.NullReferenceException?displayProperty=fullName>. При выполнении сравнения строку null и пустые строки, общеязыковая среда выполнения не возникает исключения; Операция сравнения возвращает `false`. Проверка значений null не оказывает существенного влияния на относительную производительность этих двух подходов. При разработке для [!INCLUDE[dnprdnlong](../code-quality/includes/dnprdnlong_md.md)], используйте <xref:System.String.IsNullOrEmpty%2A> метод. В противном случае используйте <xref:System.String.Length%2A> == сравнения, когда это возможно.

## <a name="how-to-fix-violations"></a>Устранение нарушений
 Чтобы устранить нарушение данного правила, измените выражение, чтобы использовать <xref:System.String.Length%2A> свойства и выполнить проверку пустой строкой. Если код предназначен для [!INCLUDE[dnprdnlong](../code-quality/includes/dnprdnlong_md.md)], используйте <xref:System.String.IsNullOrEmpty%2A> метод.

## <a name="when-to-suppress-warnings"></a>Отключение предупреждений
 Это безопасно подавить предупреждение из этого правила, если производительность не является проблемой.

## <a name="example"></a>Пример
 В следующем примере показано разных методов, которые используются для поиска пустой строкой.

 [!code-csharp[FxCop.Performance.StringTest#1](../code-quality/codesnippet/CSharp/ca1820-test-for-empty-strings-using-string-length_1.cs)]