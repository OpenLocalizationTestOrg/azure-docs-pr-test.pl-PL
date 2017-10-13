---
title: "Przegląd usługi Konfiguracja DSC automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Omówienie programu żądanego stanu konfiguracji (Konfiguracja DSC automatyzacji Azure), jego warunki i znane problemy"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "PowerShell dsc, konfiguracji żądanego stanu, azure dsc środowiska powershell"
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 468321fa6863d78bc0d179fbe5c2ed6195040d50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-dsc-overview"></a>Przegląd usługi Konfiguracja DSC automatyzacji Azure

Konfiguracja DSC usługi Automatyzacja Azure jest usługą platformy Azure, która umożliwia zapis, zarządzanie i skompilować konfiguracji żądanego stanu środowiska PowerShell (DSC) [konfiguracje](https://msdn.microsoft.com/powershell/dsc/configurations), zaimportuj [zasobów DSC](https://msdn.microsoft.com/powershell/dsc/resources)i przypisz konfiguracje do węzły docelowe w chmurze.

## <a name="why-use-azure-automation-dsc"></a>Dlaczego warto korzystać z usługi Konfiguracja DSC automatyzacji Azure

Konfiguracja DSC automatyzacji Azure zapewnia kilka zalet w porównaniu z używaniem konfiguracji DSC poza platformą Azure.

### <a name="built-in-pull-server"></a>Serwerem ściągania wbudowane

Udostępnia usługi Automatyzacja Azure [serwera ściągania usługi Konfiguracja DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) tak, aby węzły docelowe automatycznie otrzymują konfiguracje, dostosowywać się do żądanego stanu i raportować o swojej zgodności.
Z serwerem ściągania wbudowanych w automatyzacji Azure eliminuje konieczność Konfigurowanie i konserwacja serwera ściągania.
Automatyzacja Azure można kierować wirtualnych lub fizycznych systemu Windows lub Linux maszyny, w chmurze lub lokalnie.

### <a name="management-of-all-your-dsc-artifacts"></a>Zarządzanie artefaktów DSC

Konfiguracja DSC automatyzacji Azure oferuje tej samej warstwie zarządzania [konfiguracji żądanego stanu środowiska PowerShell](https://msdn.microsoft.com/powershell/dsc/overview) jako usługi Automatyzacja Azure oferuje dla skryptów środowiska PowerShell.

Z portalu Azure lub programu PowerShell można zarządzać wszystkie Twoje DSC konfiguracje, zasobów i węzły docelowe.

![Zrzut ekranu przedstawiający blok usługi Automatyzacja Azure](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a>Importowanie danych raportowania do analizy dzienników

Węzły, które są zarządzane w usłudze Konfiguracja DSC automatyzacji Azure wysyłać szczegółowe dane raportów o stanie do serwera ściągania wbudowanych.
Można skonfigurować do wysyłania tych danych do swojego obszaru roboczego analizy dzienników programu Microsoft Operations Management Suite (OMS), konfiguracja DSC automatyzacji Azure.
Aby dowiedzieć się, jak wysyłać dane o stanie DSC do obszaru roboczego analizy dzienników, zobacz [do przodu Konfiguracja DSC automatyzacji Azure raportowania danych do analizy dzienników OMS](automation-dsc-diagnostics.md).

## <a name="introduction-video"></a>Wideo z wprowadzeniem

Wolisz obejrzeć film niż przeczytać artykuł? Ma wygląd w poniższym klipie wideo z maja 2015 roku, po raz pierwszy ogłoszono Konfiguracja DSC automatyzacji Azure.

>[!NOTE]
>Koncepcje i cyklu życia omówione w tym wideo są poprawne, konfiguracja DSC automatyzacji Azure zanotowano znacznie, ponieważ ten film został zapisany.
>Teraz jest ogólnie dostępna, ma znacznie bardziej rozległych interfejsu użytkownika w portalu Azure i obsługuje wiele dodatkowych funkcji.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a>Następne kroki

* Aby dowiedzieć się, aby dodać węzły mają być zarządzane w usłudze Konfiguracja DSC automatyzacji Azure, zobacz temat [dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure](automation-dsc-onboarding.md)
* Aby rozpocząć korzystanie z usługi Konfiguracja DSC automatyzacji Azure, zobacz [wprowadzenie do korzystania z usługi Konfiguracja DSC automatyzacji Azure](automation-dsc-getting-started.md)
* Aby uzyskać informacje dotyczące kompilowania konfiguracji DSC, dzięki czemu można je przypisać do węzły docelowe, zobacz [kompilowania konfiguracji DSC automatyzacji Azure](automation-dsc-compile.md)
* Dokumentacja poleceń cmdlet programu PowerShell dla usługi Konfiguracja DSC automatyzacji Azure, aby zapoznać [poleceń cmdlet usługi Konfiguracja DSC automatyzacji Azure](/powershell/module/azurerm.automation/#automation)
* Aby uzyskać informacje o cenach, zobacz [cennik usługi Konfiguracja DSC automatyzacji Azure](https://azure.microsoft.com/pricing/details/automation/)
* Aby zapoznać się z przykładem w potoku ciągłe wdrażanie przy użyciu usługi Konfiguracja DSC automatyzacji Azure, zobacz [ciągłe wdrażanie DSC automatyzacji Azure przy użyciu maszyn wirtualnych IaaS i Chocolatey](automation-dsc-cd-chocolatey.md)