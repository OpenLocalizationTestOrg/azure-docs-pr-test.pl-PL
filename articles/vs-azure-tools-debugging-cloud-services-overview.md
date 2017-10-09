---
title: "usługi w chmurze aaaOptions do debugowania Azure | Dokumentacja firmy Microsoft"
description: "Debugowanie usług w chmurze Azure"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 80755da7-8350-4f5c-97ce-2962beabb36d
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/18/2017
ms.author: kraigb
ms.openlocfilehash: 8b7779ca33cfd82fd5fbccf229ea822c311bdea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-hello-various-ways-toodebug-an-azure-cloud-service"></a>Dowiedz się hello różne sposoby toodebug usługi w chmurze Azure
Ten artykuł zawiera łącza toohello różne sposoby toodebug usługi w chmurze Azure. 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a>Debugowanie usługi w chmurze platformy Azure w programie Visual Studio
Można zapisać czas i pieniądze za pomocą toodebug emulatora obliczeń platformy Azure hello usługi w chmurze na komputerze lokalnym. Przez lokalnie debugowania usługi przed wdrożeniem, można zwiększyć niezawodność i wydajność bez płatności dla czasu obliczeniowego. Jednak niektóre błędy mogą wystąpić tylko w przypadku uruchamiania usługi w chmurze na platformie Azure. Przez włączenie zdalnego debugowania podczas publikowania usługi, a następnie dołączania wystąpienia roli tooa debugera hello może być debugowany błędy występujące tylko w przypadku uruchamiania usługi w chmurze na platformie Azure. Aby uzyskać więcej informacji, zobacz [debugowania usługi w chmurze na komputerze lokalnym](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer).

## <a name="using-azure-diagnostics"></a>Za pomocą diagnostyki Azure 
Można użyć diagnostyki Azure toolog szczegółowe informacje o uruchamianiu kodu w ramach ról, czy role hello są uruchomione w środowisku projektowym hello lub na platformie Azure. Aby uzyskać więcej informacji, zobacz [Włączanie diagnostyki Azure w usług Azure Cloud Services](http://go.microsoft.com/fwlink/p/?LinkId=400450).

## <a name="using-intellitrace"></a>Używanie funkcji IntelliTrace 
Jeśli używasz programu Visual Studio Enterprise toowrite ról docelową programu .NET Framework 4.5, można włączyć funkcji IntelliTrace w czasie hello wdrożenie usługi w chmurze platformy Azure w programie Visual Studio. IntelliTrace zawiera dziennik czy za pomocą programu Visual Studio toodebug aplikacji tak, jakby były uruchomione w systemie Azure. Aby uzyskać więcej informacji, zobacz [debugowania usługi opublikowana chmura za pomocą funkcji IntelliTrace i Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623016).

## <a name="remote-debugging"></a>Debugowanie zdalne 
Umożliwia zdalne debugowanie usług w chmurze w czasie hello podczas wdrażania usługi w chmurze hello z programu Visual Studio. Jeśli wybierzesz tooenable zdalnego debugowania dla wdrożenia usługi zdalnego debugowania są zainstalowane na powitania maszyn wirtualnych, które Uruchom każde wystąpienie roli. Te usługi — takie jak `msvsmon.exe` — nie wpływają na wydajność lub spowodować dodatkowych kosztów. Aby uzyskać więcej informacji, zobacz [debugowania usługi w chmurze na platformie Azure](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure).

## <a name="next-steps"></a>Następne kroki
- [Debugowanie usługi w chmurze Azure lub maszyny Wirtualnej w programie Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md) — Dowiedz się, jak usługi w chmurze toodebug Azure hello szczegóły.
