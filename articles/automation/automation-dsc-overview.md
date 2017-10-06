---
title: "Przegląd usługi Konfiguracja DSC automatyzacji aaaAzure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a>Przegląd usługi Konfiguracja DSC automatyzacji Azure

Konfiguracja DSC usługi Automatyzacja Azure jest usługą platformy Azure, która pozwala toowrite, zarządzanie i skompilować konfiguracji żądanego stanu środowiska PowerShell (DSC) [konfiguracje](https://msdn.microsoft.com/powershell/dsc/configurations), zaimportuj [zasobów DSC](https://msdn.microsoft.com/powershell/dsc/resources)i przypisz węzły tootarget konfiguracje w chmurze hello.

## <a name="why-use-azure-automation-dsc"></a>Dlaczego warto korzystać z usługi Konfiguracja DSC automatyzacji Azure

Konfiguracja DSC automatyzacji Azure zapewnia kilka zalet w porównaniu z używaniem konfiguracji DSC poza platformą Azure.

### <a name="built-in-pull-server"></a>Serwerem ściągania wbudowane

Udostępnia usługi Automatyzacja Azure [serwera ściągania usługi Konfiguracja DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) tak, aby węzły docelowe automatycznie otrzymują konfiguracje, jest zgodna z toohello żądany stan i raportować o swojej zgodności.
powitania serwera ściągania wbudowanych w automatyzacji Azure eliminuje hello tooset muszą się i obsługa serwera ściągania.
Automatyzacja Azure można kierować wirtualnych lub fizycznych systemu Windows lub Linux maszyny, w chmurze hello lub lokalnie.

### <a name="management-of-all-your-dsc-artifacts"></a>Zarządzanie artefaktów DSC

Konfiguracja DSC automatyzacji Azure oferuje zbyt hello tego samego warstwa zarządzania[konfiguracji żądanego stanu programu PowerShell](https://msdn.microsoft.com/powershell/dsc/overview) jako usługi Automatyzacja Azure oferuje dla skryptów środowiska PowerShell.

Z hello portalu Azure lub programu PowerShell można zarządzać wszystkie Twoje DSC konfiguracje, zasobów i węzły docelowe.

![Zrzut ekranu przedstawiający blok usługi Automatyzacja Azure hello](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a>Importowanie danych raportowania do analizy dzienników

Węzły, które są zarządzane w usłudze Konfiguracja DSC automatyzacji Azure Wyślij szczegółowy stan danych toohello ściągania wbudowanego serwera raportowania.
Konfiguracja DSC automatyzacji Azure toosend można skonfigurować tego obszaru roboczego analizy dzienników programu Microsoft Operations Management Suite (OMS) tooyour danych.
toolearn toosend DSC stan danych tooyour obszaru roboczego analizy dzienników, zobacz temat [do przodu Konfiguracja DSC automatyzacji Azure raportowania tooOMS danych analizy dzienników](automation-dsc-diagnostics.md).

## <a name="introduction-video"></a>Wideo z wprowadzeniem

Preferowane jest obserwowanie tooreading? Ma wygląd na powitania po wideo z maja 2015 roku, po raz pierwszy ogłoszono Konfiguracja DSC automatyzacji Azure.

>[!NOTE]
>Pojęcia hello i cyklem życia omówione w tym wideo są poprawne, konfiguracja DSC automatyzacji Azure zanotowano znacznie, ponieważ ten film został zapisany.
>Teraz jest ogólnie dostępna, ma znacznie bardziej rozległych interfejsu użytkownika w portalu Azure hello i obsługuje wiele dodatkowych funkcji.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a>Następne kroki

* toolearn tooonboard toobe węzłów zarządzanych za pomocą usługi Konfiguracja DSC automatyzacji Azure, zobacz [dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure](automation-dsc-onboarding.md)
* tooget uruchomiony przy użyciu usługi Konfiguracja DSC automatyzacji Azure, zobacz [wprowadzenie do korzystania z usługi Konfiguracja DSC automatyzacji Azure](automation-dsc-getting-started.md)
* Zobacz toolearn o kompilowania konfiguracji DSC, dzięki czemu można je przypisać węzłów tootarget [kompilowania konfiguracji DSC automatyzacji Azure](automation-dsc-compile.md)
* Dokumentacja poleceń cmdlet programu PowerShell dla usługi Konfiguracja DSC automatyzacji Azure, aby zapoznać [poleceń cmdlet usługi Konfiguracja DSC automatyzacji Azure](/powershell/module/azurerm.automation/#automation)
* Aby uzyskać informacje o cenach, zobacz [cennik usługi Konfiguracja DSC automatyzacji Azure](https://azure.microsoft.com/pricing/details/automation/)
* Zobacz toosee przykładem w potoku ciągłe wdrażanie przy użyciu usługi Konfiguracja DSC automatyzacji Azure [tooIaaS ciągłe wdrażanie maszyn wirtualnych przy użyciu usługi Azure Automation DSC i Chocolatey](automation-dsc-cd-chocolatey.md)
