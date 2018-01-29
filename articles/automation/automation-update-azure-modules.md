---
title: "Zaktualizuj Azure modułów w automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak można teraz zaktualizować typowymi modułami programu Azure PowerShell domyślne automatyzacji Azure."
services: automation
documentationcenter: 
author: georgewallace
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: f5e7c66cfd26bd6927d48ffd8bc0f82e9a3e2d13
ms.sourcegitcommit: 0e4491b7fdd9ca4408d5f2d41be42a09164db775
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="how-to-update-azure-powershell-modules-in-azure-automation"></a>Jak zaktualizować modułów programu Azure PowerShell w usłudze Automatyzacja Azure

Najbardziej typowe moduły programu PowerShell systemu Azure znajdują się domyślnie każdego konta automatyzacji.  Zespół Azure aktualizuje Azure modułów regularnie, więc w ramach konta automatyzacji udostępniamy sposób aktualizowania modułów w ramach konta, gdy nowe wersje są dostępne w portalu.  

Ponieważ moduły są regularnie aktualizowane przez grupę, zmiany mogą być uwzględnione polecenia cmdlet, które może niekorzystnie wpłynąć na elementach runbook, w zależności od rodzaju zmiany, takie jak zmiana nazwy parametru lub całkowicie wycofano polecenia cmdlet. Aby uniknąć wpływu na elementy runbook i ich automatyzacji procesów, zdecydowanie zaleca się testowanie i zweryfikować przed kontynuowaniem.  Jeśli nie masz dedykowane konto automatyzacji przeznaczone do tego celu, należy rozważyć utworzenie jednego, dzięki czemu można przetestować wiele różnych scenariuszy i permutacji podczas tworzenia elementów runbook, oprócz do iteracji zmian, takich jak aktualizowanie Moduły programu PowerShell.  Po zweryfikowaniu wyniki i wszelkie wymagane zmiany zostały zastosowane, kontynuować koordynowanie migracji wszystkie elementy runbook, który wymagany modyfikacji i wykonać aktualizację, zgodnie z poniższym opisem w środowisku produkcyjnym.     

## <a name="updating-azure-modules"></a>Aktualizowanie Azure modułów

1. Na stronie moduły konto automatyzacji jest opcję o nazwie **modułów Azure aktualizacji**. Jest zawsze włączone.<br><br> ![Zaktualizuj opcja modułów Azure na stronie moduły](media/automation-update-azure-modules/automation-update-azure-modules-option.png)

2. Kliknij przycisk **modułów Azure aktualizacji** i otrzymasz powiadomienie z potwierdzeniem z pytaniem, czy chcesz kontynuować.<br><br> ![Zaktualizuj powiadomień Azure modułów](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)

3. Kliknij przycisk **tak** i rozpocznie się proces aktualizacji modułu. Proces aktualizacji trwa około 15-20 minut, można zaktualizować następujących modułów:

  * Azure
  * Azure.Storage
  * AzureRm.Automation
  * AzureRm.Compute
  * AzureRm.Profile
  * AzureRm.Resources
  * AzureRm.Sql
  * AzureRm.Storage

    Jeśli moduły są już aktualne, proces zostanie zakończony w ciągu kilku sekund. Po zakończeniu procesu aktualizacji, otrzymasz powiadomienie.<br><br> ![Zaktualizuj stan aktualizacji modułów Azure](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> Po uruchomieniu nowe zadanie zaplanowane usługi Automatyzacja Azure korzysta z modułów najnowszego na Twoim koncie automatyzacji.    

Jeśli używasz poleceń cmdlet z tych modułów programu Azure PowerShell w elementach runbook do zarządzania zasobami Azure, następnie chcesz przeprowadzić proces aktualizacji co miesiąc lub tak, aby mieć pewność, że masz najnowszą modułów.

## <a name="next-steps"></a>Następne kroki

* Aby dowiedzieć się więcej o moduły integracji oraz sposobu tworzenia niestandardowych modułów do dalszej integracji z innymi systemami, usług lub rozwiązań automatyzacji, zobacz [moduły integracji](automation-integration-modules.md).

* Należy rozważyć użycie integracji kontroli źródła [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) lub [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) centralne zarządzanie i sterowanie wersjach portfela automatyzacji elementu runbook i konfiguracji.  