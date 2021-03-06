---
title: Мастер интерфейса (IDTWizard) | Документы Microsoft
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- IDTWizard interface
- wizards, interface
ms.assetid: 09618d9d-d115-45b6-bccc-de328994b39c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 7ebb605ed61cc06ef70fde97f3d5831c6d5c4503
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="wizard-interface-idtwizard"></a>Мастер интерфейса (IDTWizard)
Интегрированной среды разработки (IDE) использует <xref:EnvDTE.IDTWizard> интерфейс для взаимодействия с помощью мастеров. Мастера должен реализовывать этот интерфейс, чтобы можно было установить в Интегрированной среде разработки.  
  
 <xref:EnvDTE.IDTWizard.Execute%2A> — Единственный метод, связанный с <xref:EnvDTE.IDTWizard> интерфейса. Мастеры реализовать этот метод и интегрированной среды разработки вызывает метод в интерфейсе. В следующем примере показано сигнатуру метода.  
  
```  
/* IDTWizard Method */  
STDMETHOD(Execute)(THIS_  
   /* [in] */ IDispatch *Application,  
   /* [in] */ long hwndOwner,  
   /* [in] */ SAFEARRAY * *ContextParams,  
   /* [in] */ SAFEARRAY * *CustomParams,  
   /* [out] [in] */ wizardResult *RetVal  
   );  
```  
  
 Аналогично механизма запуска для обоих **новый проект** и **Добавление нового элемента**мастеров. Чтобы начать, либо, вызовите <xref:EnvDTE.IDTWizard> интерфейс, определенный в Dteinternal.h. Единственное отличие — это совокупность контекст и настраиваемые параметры, которые передаются на интерфейс, при вызове интерфейса.  
  
 Ниже описаны <xref:EnvDTE.IDTWizard> интерфейс, который должен быть реализован мастеров для работы в [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] интегрированной среды разработки. Интегрированная среда разработки вызовы <xref:EnvDTE.IDTWizard.Execute%2A> метод в мастере, передавая ему следующее:  
  
-   Объект DTE  
  
     Объект DTE является корнем модели автоматизации.  
  
-   Дескриптор диалоговое окна, как показано в сегмент кода `hwndOwner ([in] long)`.  
  
     Мастер использует это `hwndOwner` как родительский для диалоговое окно мастера.  
  
-   Параметры контекста передается интерфейс как данные variant для безопасного массива SAFEARRAY как показано в сегмент кода `[in] SAFEARRAY (VARIANT)* ContextParams`.  
  
     Параметры контекста содержит массив значений, характерные для типа запуска мастера и текущее состояние проекта. Мастер интегрированной среды разработки передает параметры контекста. Дополнительные сведения см. в разделе [параметры контекста](../../extensibility/internals/context-parameters.md).  
  
-   Пользовательские параметры передаче интерфейса как variant для безопасного массива SAFEARRAY как показано в сегмент кода `[in] SAFEARRAY (VARIANT)* CustomParams`.  
  
     Пользовательские параметры содержат массив пользовательских параметров. VSZ-файл передает пользовательские параметры интегрированной среды разработки. Значения определяются `Param=` инструкции. Дополнительные сведения см. в разделе [пользовательские параметры](../../extensibility/internals/custom-parameters.md).  
  
-   Возвращаемые значения для интерфейса:  
  
    ```  
    wizardResultSuccess = -1,  
    wizardResultFailure = 0  
    wizardResultCancel = 1  
    wizardResultBackout = 2  
    ```  
  
## <a name="see-also"></a>См. также  
 [Контекстные параметры](../../extensibility/internals/context-parameters.md)   
 [Пользовательские параметры](../../extensibility/internals/custom-parameters.md)   
 [Мастеры](../../extensibility/internals/wizards.md)   
 [Файл мастера (VSZ-файл)](../../extensibility/internals/wizard-dot-vsz-file.md)