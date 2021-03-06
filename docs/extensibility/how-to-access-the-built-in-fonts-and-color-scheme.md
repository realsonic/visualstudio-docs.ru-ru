---
title: 'Как: доступ к встроенные шрифты и цветовую схему | Документы Microsoft'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- fonts, accessing built-in
- font and color control [Visual Studio SDK], categories
- colors, accessing built-in schemes
ms.assetid: 6905845e-e88e-4805-adcf-21da39108ec7
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 5f72640369152b03ef86383fda1162b1cfbacba8
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-access-the-built-in-fonts-and-color-scheme"></a>Как: доступ к встроенных шрифтов и цветов
Среда разработки Visual Studio (IDE) имеется схема шрифтов и цветов, связанный с окном редактора. Получить доступ к этой схеме через <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> интерфейса.

 Чтобы использовать встроенные шрифтов и цветов схемы, пакет VSPackage должен удовлетворять следующим требованиям:

-   Определите категорию для использования со службой шрифты и цвета по умолчанию.

-   Зарегистрируйте категорию на сервере по умолчанию шрифты и цвета.

-   Уведомления IDE с конкретным окном использует встроенные отображаемые элементы и категории с помощью <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer> и <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer> интерфейсов.

 Интегрированная среда разработки использует полученный категории как дескриптор окна. Имя категории отображается в **Показать параметры для:** раскрывающегося списка в **шрифты и цвета** страницу свойств.

### <a name="to-define-a-category-using-built-in-fonts-and-colors"></a>Для определения категории с помощью встроенных шрифты и цвета

1.  Создайте произвольный идентификатор GUID.

     Этот идентификатор GUID, используемый для уникальной идентификации категории**.** В этой категории используются повторно спецификация цвета и шрифты по умолчанию для интегрированной среды разработки.

    > [!NOTE]
    >  При получении данных шрифта и цвета с <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents> или других интерфейсов, пакеты VSPackage использовать этот идентификатор GUID для ссылки на встроенные сведения.

2.  Имя категории должны добавляться в таблицу строки в файл ресурсов (.rc) в пакете VSPackage, чтобы ее можно локализовать, при необходимости, при отображении в Интегрированной среде разработки.

     Дополнительные сведения см. в разделе [Добавление или удаление строки](/cpp/windows/adding-or-deleting-a-string).

### <a name="to-register-a-category-using-built-in-fonts-and-colors"></a>Чтобы зарегистрировать категории с помощью встроенных шрифты и цвета

1.  Создайте специальный тип записи реестра категории в следующем расположении:

     [HKLM\SOFTWARE\Microsoft \Visual Studio\\*\<версия Visual Studio >*\FontAndColors\\*\<категории >*]

     *\<Категория >* нелокализованное имя категории.

2.  Добавить в реестр для использования стандартных шрифтов и цветовой схемы с четырьмя значениями:

    |name|Тип|Данные|Описание|
    |----------|----------|----------|-----------------|
    |Категория|REG_SZ|Идентификатор GUID|Произвольный идентификатор GUID, который идентифицирует категорию, которая содержит биржевых шрифт и цветовую схему.|
    |Пакет|REG_SZ|Идентификатор GUID|{F5E7E71D-1401-11D1-883B-0000F87579D2}<br /><br /> Все пакеты VSPackage, используйте параметры шрифта и цвета по умолчанию используется идентификатор GUID.|
    |Идентификатора имени|REG_DWORD|ID|Идентификатор ресурса имя категории локализуемых в VSPackage.|
    |ToolWindowPackage|REG_SZ|Идентификатор GUID|Идентификатор GUID для реализации VSPackage <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> интерфейса.|

### <a name="to-initiate-the-use-of-system-provided-fonts-and-colors"></a>Чтобы начать использование системных шрифтов и цветов

1.  Создайте экземпляр класса <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer> интерфейс как часть реализации и инициализации окна.

2.  Вызовите <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyCategoryContainer.GetPropertyCategory%2A> метод, чтобы получить экземпляр <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer> интерфейса, связанного с текущим <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> экземпляра.

3.  Вызовите <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextEditorPropertyContainer.SetProperty%2A> дважды.

    -   Вызовите один раз с `VSEDITPROPID_ViewGeneral_ColorCategory`в качестве аргумента.

    -   Вызовите один раз с `VSEDITPROPID_ViewGeneral_FontCategory` в качестве аргумента.

     Это задает и предоставляет службы шрифты и цвета по умолчанию как свойство окна.

## <a name="example"></a>Пример
 В следующем примере инициируется использование встроенных шрифты и цвета.

```cpp
CComVariant vt;
CComQIPtr<IVsTextEditorPropertyCategoryContainer> spPropCatContainer(m_spView);
if (spPropCatContainer != NULL){
    CComPtr<IVsTextEditorPropertyContainer> spPropContainer;
    if (SUCCEEDED(spPropCatContainer->GetPropertyCategory(GUID_EditPropCategory_View_MasterSettings,
                                                          &spPropContainer))){
        CComVariant vt;CComVariant VariantGUID(bstrGuidText);
        spPropContainer->SetProperty(VSEDITPROPID_ViewGeneral_FontCategory, VariantGUID);
        spPropContainer->SetProperty(VSEDITPROPID_ViewGeneral_ColorCategory, VariantGUID);
    }
}
```

## <a name="see-also"></a>См. также

- [Шрифты и цвета](../extensibility/using-fonts-and-colors.md)
- [Получение шрифт и цвет шрифта для текста выделение цветом](../extensibility/getting-font-and-color-information-for-text-colorization.md)
- [Доступ к хранимой шрифта и цветов](../extensibility/accessing-stored-font-and-color-settings.md)
- [Обзор цвет и шрифт](../extensibility/font-and-color-overview.md)