---
title: 'Создание нового проекта: За кулисами, часть | Документы Microsoft'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 73ce91d8-0ab1-4a1f-bf12-4d3c49c01e13
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 69174be20a0961a6074650471bcb4b9d1df9fa98
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2018
---
# <a name="new-project-generation-under-the-hood-part-two"></a>Создание нового проекта: За кулисами, часть 2
В [Создание нового проекта: В механизме, часть 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md) мы узнали, как **новый проект** диалоговое окно заполняется значениями. Предположим, что вы выбрали **приложения Windows Visual C#**, заполненных **имя** и **расположение** текстовые поля и выборе ОК.  
  
## <a name="generating-the-solution-files"></a>Создание файлов решения  
 Выбор шаблона приложения направляет [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] распаковка и открытие соответствующего VSTEMPLATE-файл и для запуска шаблона для интерпретации команд XML в этом файле. Эти команды создают проектов и элементов проектов в новом или существующем решении.  
  
 Шаблон распаковывает источника файлов, называемых шаблонов элементов из той же папки расширением ZIP, содержащий VSTEMPLATE-файл. Шаблон копирует эти файлы в новый проект, настройка их соответствующим образом.  
  
### <a name="template-parameter-replacement"></a>Замена параметров шаблона  
 Когда шаблон копирует шаблона элемента в новый проект, он заменяет любые параметры шаблона строк в файле. Параметр шаблона — это специальный маркер, который является и стоять знак доллара, например $date$.  
  
 Рассмотрим типичный шаблон элемента. Извлечение и изучите Program.cs в папке Program Files\Microsoft Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip.  
  
```  
using System;  
using System.Collections.Generic;  
using System.Windows.Forms;  
  
namespace $safeprojectname$  
{  
    static class Program  
    {  
        // source code deleted here for brevity  
    }  
}  
```  
  
 При создании нового проекта приложения Windows с именем Simple, он заменяет `$safeprojectname$` параметр с именем проекта.  
  
```  
using System;  
using System.Collections.Generic;  
using System.Windows.Forms;  
  
namespace Simple  
{  
    static class Program  
    {  
        // source code deleted here for brevity  
    }  
}  
```  
  
 Полный список параметров шаблона см. в разделе [Параметры шаблона](../../ide/template-parameters.md).  
  
## <a name="a-look-inside-a-vstemplate-file"></a>Вид внутри. Файл VSTemplate  
 Формат имеет базовый VSTEMPLATE-файл  
  
```  
<VSTemplate Version="2.0.0"     xmlns="http://schemas.microsoft.com/developer/vstemplate/2005"     Type="Project">  
    <TemplateData>  
    </TemplateData>  
    <TemplateContent>  
    </TemplateContent>  
</VSTemplate>  
```  
  
 Мы рассмотрели \<TemplateData > статьи [Создание нового проекта: В механизме, часть 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md). Теги в этом разделе используются для управления внешним видом **новый проект** диалоговое окно.  
  
 Теги в \<TemplateContent > статьи управления создание новых проектов и элементов проектов. Вот \<TemplateContent > раздел cswindowsapplication.vstemplate-файла в папке 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip \Program Files\Microsoft Visual Studio.  
  
```  
<TemplateContent>  
  <Project File="WindowsApplication.csproj" ReplaceParameters="true">  
    <ProjectItem ReplaceParameters="true"  
      TargetFileName="Properties\AssemblyInfo.cs">  
      AssemblyInfo.cs  
    </ProjectItem>  
    <ProjectItem TargetFileName="Properties\Resources.resx">  
      Resources.resx  
    </ProjectItem>  
    <ProjectItem ReplaceParameters="true"       TargetFileName="Properties\Resources.Designer.cs">  
      Resources.Designer.cs  
    </ProjectItem>  
    <ProjectItem TargetFileName="Properties\Settings.settings">  
      Settings.settings  
    </ProjectItem>  
    <ProjectItem ReplaceParameters="true"       TargetFileName="Properties\Settings.Designer.cs">  
      Settings.Designer.cs  
    </ProjectItem>  
    <ProjectItem ReplaceParameters="true" OpenInEditor="true">  
      Form1.cs  
    </ProjectItem>  
    <ProjectItem ReplaceParameters="true">  
      Form1.Designer.cs  
    </ProjectItem>  
    <ProjectItem ReplaceParameters="true">  
      Program.cs  
    </ProjectItem>  
  </Project>  
</TemplateContent>  
```  
  
 \<Проекта > тег контролирует Создание проекта и \<ProjectItem > тег контролирует Создание элемента проекта. Если параметр ReplaceParameters имеет значение true, шаблон будет выполнена настройка всех параметров шаблона в файле проекта или элемента. В этом случае все элементы проекта создаются пользователем, за исключением Settings.settings.  
  
 Параметр TargetFileName указывает имя и относительный путь, полученный файл проекта или элемента. Это позволяет создать структуру папок для проекта. Если этот аргумент не указан, элемент проекта будет иметь имя, совпадающее с именем шаблона элемента проекта.  
  
 Полученный Windows приложения выглядит следующим образом:  
  
 ![SimpleSolution](../../extensibility/internals/media/simplesolution.png "SimpleSolution")  
  
 Первым и единственным \<проекта > тег в операции чтения шаблона:  
  
```  
<Project File="WindowsApplication.csproj" ReplaceParameters="true">  
```  
  
 Это указывает, что шаблон нового проекта для создания файла проекта Simple.csproj путем копирования и настройка windowsapplication.csproj элемента шаблона.  
  
### <a name="designers-and-references"></a>Конструкторы и ссылки  
 Появится в обозревателе решений папку свойства существует и содержит ожидаемые файлы. Но что насчет проект ссылается на и файл конструктора зависимостей, таких как местоположении Resources.resx для Resources.resx и Form1.Designer.cs для Form1.cs?  Они настраиваются в файле Simple.csproj при его создании.  
  
 Вот \<ItemGroup > из Simple.csproj, которая создает ссылки на проект:  
  
```  
<ItemGroup>  
    <Reference Include="System" />  
    <Reference Include="System.Data" />  
    <Reference Include="System.Deployment" />  
    <Reference Include="System.Drawing" />  
    <Reference Include="System.Windows.Forms" />  
    <Reference Include="System.Xml" />  
</ItemGroup>  
```  
  
 Вы увидите, что они ссылки шесть проекта, которые отображаются в обозревателе решений. Ниже приведен раздел из другого \<ItemGroup >. Количество строк кода были удалены для ясности. В этом разделе делает Settings.Designer.cs зависимым от Settings.settings:  
  
```  
<ItemGroup>  
    <Compile Include="Properties\Settings.Designer.cs">  
        <DependentUpon>Settings.settings</DependentUpon>  
    </Compile>  
</ItemGroup>  
```  
  
## <a name="see-also"></a>См. также  
 [Создание нового проекта. Как это работает, часть 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)  
 [MSBuild](../../msbuild/msbuild.md)