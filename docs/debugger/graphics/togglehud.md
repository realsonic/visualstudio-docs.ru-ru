---
title: ToggleHUD | Документы Microsoft
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 7261e01d-3c72-46ce-9fb3-5f33b2ddb901
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 86ce582ab49d4d079f01f7231f49aa761baa1069
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/18/2018
---
# <a name="togglehud"></a>ToggleHUD
Переключает диагностики графики *HUD* наложения (головной дисплей) или отключить.  
  
## <a name="syntax"></a>Синтаксис  
  
```C++  
void ToggleHUD();  
```  
  
## <a name="remarks"></a>Примечания  
 Головной дисплей (HUD) диагностики графики отображается в левом верхнем углу приложения, которое работает в режиме диагностики графики. В нем отображаются данные времени выполнения для приложений, а также о захвате данных графики и сообщений, которые добавляются путем вызова [AddMessage](addmessage.md) функции-члена.  
  
 Чтобы переключиться на HUD, не нужно активно захват графической информации — то есть, он может включаться через экземпляр `VsgDbg` класса, но [Init](init.md) функции-члена не должен вызываться сначала.