---
title: Развертывание решения Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ClickOnce deployment [Office development in Visual Studio], event viewer
- deploying applications [Office development in Visual Studio], event viewer
- Office applications [Office development in Visual Studio], deploying Office solutions
- Office development in Visual Studio, deploying Office solutions
- ClickOnce deployment [Office development in Visual Studio], troubleshooting
- deploying applications [Office development in Visual Studio], Office solutions (2007 system)
- Office development in Visual Studio, troubleshooting
- Office development in Visual Studio, event viewer
- ClickOnce deployment [Office development in Visual Studio], about ClickOnce solution deployments
- Office solutions [Office development in Visual Studio], deploying
- deploying applications [Office development in Visual Studio], troubleshooting
- solutions [Office development in Visual Studio], deploying Office solutions (2007 system)
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 58e485384f80b2f0fdfc46a91caf305754a87301
ms.sourcegitcommit: 209c2c068ff0975994ed892b62aa9b834a7f6077
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2018
---
# <a name="deploy-an-office-solution"></a>Развертывание решения Office
  Решения Office можно развертывать с помощью ClickOnce или установщика Windows. Использование ClickOnce позволяет сократить число шагов, необходимых для развертывания и обновления решения. При использовании установщика Windows разработчик получает больший контроль над процессом установки решения и над тем, какие именно страницы программы установки отображаются, когда пользователь устанавливает решение.  
  
> [!NOTE]  
>  Заинтересованы в разработке решений, расширяющих возможности Office через [нескольких платформ](https://dev.office.com/add-in-availability)? Ознакомьтесь с новой [модель надстроек Office](https://dev.office.com/docs/add-ins/overview/office-add-ins). Надстройки Office имеют небольшого размера, по сравнению с надстроек VSTO и решения, и их можно создавать с помощью почти любой технологии веб-программирования, таких как HTML5, JavaScript, CSS3 и XML.  
  
## <a name="deploy-a-solution-by-using-clickonce"></a>Развертывание решения с помощью ClickOnce  
 При развертывании решения с помощью ClickOnce оно публикуется в центральном расположении, откуда пользователи могут устанавливать и запускать его. Решение можно обновить без необходимости передачи пользователям новой программы установки.  Этот вариант развертывания проще, но он не позволяет работать с пользовательскими страницами мастера установки. Кроме того, на компьютерах с несколькими пользователями решения должны устанавливаться по несколько раз. В разделе [развертывание решения Office с помощью ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md).  
  
## <a name="deploy-a-solution-by-using-windows-installer"></a>Развертывание решения с помощью установщика Windows  
 При развертывании решения с помощью установщика Windows программа установки распространяется среди пользователей, а пользователи, в свою очередь, устанавливают решение с помощью этой программы. Программа установки позволяет установить решение сразу для всех пользователей компьютера, а не только для текущего пользователя. Также она дает больший контроль над тем, какие параметры видны пользователям при установке решения. Например, можно показать пользователям лицензионное соглашение или позволить им установить только часть компонентов решения. Однако при обновлении решения необходимо передать пользователям новую программу установки. В разделе [развертывание решения Office с помощью установщика Windows](../vsto/deploying-an-office-solution-by-using-windows-installer.md).  
  
## <a name="see-also"></a>См. также  
 [Безопасные решения Office](../vsto/securing-office-solutions.md)   
 [Развертывание решения Office с помощью ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md)   
 [Развертывание решения Office с помощью установщика Windows](../vsto/deploying-an-office-solution-by-using-windows-installer.md)   
 [Устранение неполадок развертывания решения Office](../vsto/troubleshooting-office-solution-deployment.md)  
  
  