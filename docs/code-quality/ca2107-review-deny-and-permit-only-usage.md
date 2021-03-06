---
title: 'CA2107: проверьте использование deny и permit only'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2107
- ReviewDenyAndPermitOnlyUsage
helpviewer_keywords:
- ReviewDenyAndPermitOnlyUsage
- CA2107
ms.assetid: 366f4a56-ae93-4882-81d0-bd0a55ebbc26
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d777379cdf5dc5d6be36989f95aadd80ca757e69
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="ca2107-review-deny-and-permit-only-usage"></a>CA2107: проверьте использование deny и permit only
|||
|-|-|
|TypeName|ReviewDenyAndPermitOnlyUsage|
|CheckId|CA2107|
|Категория|Microsoft.Security|
|Критическое изменение|Критическое|

## <a name="cause"></a>Причина
 Метод содержит проверку безопасности, которая задает действие по обеспечению безопасности PermitOnly или Deny.

## <a name="rule-description"></a>Описание правила
 <xref:System.Security.CodeAccessPermission.Deny%2A?displayProperty=fullName> Действие по обеспечению безопасности следует использовать только те, кто имеет специальными знаниями из [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] безопасности. Код, который использует эти действия безопасности, должен быть тщательно проанализирован на предмет безопасности.

 Запретить изменяет поведение по умолчанию стека, которая происходит в ответ на запрос безопасности. Он позволяет указать разрешения, которые не должны предоставляться в течение метода отказа, независимо от фактических разрешений вызывающих методов в стеке вызовов. Если обход стека обнаруживается метод, защищенный действием Deny, и если запрошенное разрешение включается в отклоненные разрешения, обход стека не выполняется. Метод PermitOnly также изменяет поведение по умолчанию проверки стека. Он позволяет указать только те разрешения, которые могут быть предоставлены независимо от разрешений от вызывающих объектов кода. Если обход стека обнаруживается метод, защищенный действием PermitOnly, и если затребованное разрешение не включен в разрешения, которые определяются PermitOnly, обход стека не выполняется.

 Код, основанный на эти действия нужно тщательно оценить для уязвимости системы безопасности из-за ограниченной пригодностью и поведении. Рассмотрим следующий пример.

-   [Требования связывания](/dotnet/framework/misc/link-demands) не подвержены Deny или PermitOnly.

-   Если Deny или PermitOnly происходят в одном кадре стека как запрос, вызывающий обход стека, действия безопасности не действуют.

-   Значения, используемые для создания, разрешениями на основе пути обычно можно указать несколькими способами. Запрет доступа к одной форме пути не запрещает доступ для всех форм. Например, если общая папка \\\Server\Share сопоставляется с сетевой диск X:, чтобы запретить доступ к файлу в общую папку, необходимо запретить \\\Server\Share\File, X:\File и все остальные пути, обращающиеся к файлу.

-   <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName> Может завершить обход стека, до достижения Deny или PermitOnly.

-   Если Deny не дает результатов, а именно, когда вызывающий объект имеет разрешение, заблокированное действием Deny, вызывающий объект может доступ к защищенному ресурсу напрямую, минуя Deny. Аналогично Если вызывающий объект не имеет отказа в разрешении, обход стека завершится сбоем без Deny.

## <a name="how-to-fix-violations"></a>Устранение нарушений
 Любое использование этих действий безопасности вызовет нарушение. Чтобы устранить нарушение, не используйте эти действия безопасности.

## <a name="when-to-suppress-warnings"></a>Отключение предупреждений
 Отключайте предупреждение из этого правила только после завершения проверки безопасности.

## <a name="example"></a>Пример
 В следующем примере показано некоторые ограничения действия Deny.

 Следующая библиотека содержит класс, имеющий два метода, которые идентичны, за исключением требований к безопасности, которые защищают транзакции.

 [!code-csharp[FxCop.Security.PermitAndDeny#1](../code-quality/codesnippet/CSharp/ca2107-review-deny-and-permit-only-usage_1.cs)]

## <a name="example"></a>Пример
 В следующем приложении демонстрируется действие Deny с защищенными методами из библиотеки.

 [!code-csharp[FxCop.Security.TestPermitAndDeny#1](../code-quality/codesnippet/CSharp/ca2107-review-deny-and-permit-only-usage_2.cs)]

 В этом примере формируются следующие данные:

 **Запросу: Вызывающего Deny не оказывает влияния по требованию с утвержденного разрешения. ** 
 **LinkDemand: вызывающего Deny не оказывает влияния на LinkDemand с утвержденного разрешения.** 
 **LinkDemand: вызывающего Deny имеет смысл с кодом, защищенный LinkDemand.** 
 **LinkDemand: запретить это не оказывает влияния с кодом, защищенный LinkDemand.**
## <a name="see-also"></a>См. также
 <xref:System.Security.CodeAccessPermission.PermitOnly%2A?displayProperty=fullName> <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName> <xref:System.Security.CodeAccessPermission.Deny%2A?displayProperty=fullName> <xref:System.Security.IStackWalk.PermitOnly%2A?displayProperty=fullName> [Правила написания безопасного кода](/dotnet/standard/security/secure-coding-guidelines)

