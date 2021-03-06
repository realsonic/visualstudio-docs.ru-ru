---
title: 'CA1403: типы макета Auto не должны быть видимыми для COM'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AutoLayoutTypesShouldNotBeComVisible
- CA1403
helpviewer_keywords:
- CA1403
- AutoLayoutTypesShouldNotBeComVisible
ms.assetid: a7007714-f9b4-4730-94e0-67d3dc68991f
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 056b1d254b8544f9a1f0abe364bcb40f15235e64
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="ca1403-auto-layout-types-should-not-be-com-visible"></a>CA1403: типы макета Auto не должны быть видимыми для COM
|||
|-|-|
|TypeName|AutoLayoutTypesShouldNotBeComVisible|
|CheckId|CA1403|
|Категория|Microsoft.Interoperability|
|Критическое изменение|Критическое|

## <a name="cause"></a>Причина
 Тип значений, видимых объектов модели компонентов (COM) помечен атрибутом <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=fullName> атрибуту присвоено значение <xref:System.Runtime.InteropServices.LayoutKind?displayProperty=fullName>.

## <a name="rule-description"></a>Описание правила
 <xref:System.Runtime.InteropServices.LayoutKind> Общеязыковая среда выполнения управляет типы макета. Макеты этих типов может меняться в различных версиях платформы .NET Framework, что нарушит работу клиентов COM, которые ожидают определенного макета. Обратите внимание, что если <xref:System.Runtime.InteropServices.StructLayoutAttribute> атрибут не указан, в C#, [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)], и компиляторы C++ указывают <xref:System.Runtime.InteropServices.LayoutKind> макета для типов значений.

 Если не указано иное, все открытые неуниверсальные типы являются видимыми для COM; все закрытые и универсальные типы являются невидимыми для COM. Однако во избежание ложных положительных результатов, это правило требует видимость COM типа требуется явно указывать; содержащей сборки должны быть отмечены <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> значение `false` и тип должен быть помечен атрибутом <xref:System.Runtime.InteropServices.ComVisibleAttribute> значение `true`.

## <a name="how-to-fix-violations"></a>Устранение нарушений
 Чтобы устранить нарушение данного правила, измените значение <xref:System.Runtime.InteropServices.StructLayoutAttribute> атрибут <xref:System.Runtime.InteropServices.LayoutKind> или <xref:System.Runtime.InteropServices.LayoutKind>, или сделайте тип невидимый в COM.

## <a name="when-to-suppress-warnings"></a>Отключение предупреждений
 Для этого правила отключать вывод предупреждений не следует.

## <a name="example"></a>Пример
 В следующем примере показано, тип, который нарушает правила и тип, соответствующий этому правилу.

 [!code-csharp[FxCop.Interoperability.AutoLayout#1](../code-quality/codesnippet/CSharp/ca1403-auto-layout-types-should-not-be-com-visible_1.cs)]
 [!code-vb[FxCop.Interoperability.AutoLayout#1](../code-quality/codesnippet/VisualBasic/ca1403-auto-layout-types-should-not-be-com-visible_1.vb)]

## <a name="related-rules"></a>Связанные правила
 [CA1408: не используйте AutoDual ClassInterfaceType](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>См. также
 [Уточнение типов .NET для взаимодействия](/dotnet/framework/interop/qualifying-net-types-for-interoperation) [взаимодействие с неуправляемым кодом](/dotnet/framework/interop/index)