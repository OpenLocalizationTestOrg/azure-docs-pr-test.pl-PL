---
title: "aaaUpdate Azure modułów w automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak można teraz zaktualizować typowymi modułami programu Azure PowerShell domyślne automatyzacji Azure."
services: automation
documentationcenter: 
author: MGoedtel
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
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a>Jak tooupdate programu Azure PowerShell modułów w automatyzacji Azure

najbardziej typowe modułów programu Azure PowerShell Hello znajdują się domyślnie każdego konta automatyzacji.  Hello Azure zespołu aktualizacje hello Azure modułów regularnie, więc w hello konta automatyzacji zapewniamy, sposób dla Ciebie tooupdate hello modułów na koncie hello gdy są dostępne w portalu hello nowe wersje.  

Ponieważ moduły są regularnie aktualizowane przez grupę produktu hello, zmiany mogą wystąpić z poleceniami cmdlet hello uwzględnione, które może niekorzystnie wpłynąć na elementach runbook, w zależności od typu hello zmiany, takie jak zmiana nazwy parametru lub całkowicie wycofano polecenia cmdlet. tooavoid wpływu na Twoje elementy runbook i hello procesów one zautomatyzować, zdecydowanie zaleca się testowanie i zweryfikować przed kontynuowaniem.  Jeśli nie masz dedykowane konto automatyzacji przeznaczone do tego celu, należy rozważyć utworzenie tak, aby można było testować wiele różnych scenariuszy i permutacji podczas tworzenia hello elementów runbook, w dodanie tooiterative zmian, takich jak aktualizowanie hello Moduły programu PowerShell.  Po hello wyniki są weryfikowane i wszelkie wymagane zmiany zostały zastosowane, kontynuować koordynowanie migracji hello elementów runbook, wszelkie wymagane zmiany i zaktualizować hello zgodnie z poniższym opisem w środowisku produkcyjnym.     

## <a name="updating-azure-modules"></a>Aktualizowanie Azure modułów

1. W modułach hello bloku Twoje konto usługi Automatyzacja jest opcję o nazwie **modułów Azure aktualizacji**.  Jest zawsze włączone.<br><br> ![Aktualizowanie opcji Azure modułów w bloku modułów](media/automation-update-azure-modules/automation-update-azure-modules-option.png)

2. Kliknij przycisk **modułów Azure aktualizacji** i wyświetlone zostanie okno z pytaniem, czy ma toocontinue powiadomienie z potwierdzeniem.<br><br> ![Zaktualizuj powiadomień Azure modułów](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)

3. Kliknij przycisk **tak** i rozpocznie się proces aktualizacji hello modułu.  proces aktualizacji Hello trwa około 15-20 minut tooupdate hello następujących modułów:

  * Azure
  * Azure.Storage
  * AzureRm.Automation
  * AzureRm.Compute
  * AzureRm.Profile
  * AzureRm.Resources
  * AzureRm.Sql
  * AzureRm.Storage

    Jeśli moduły hello są już włączone toodate, hello proces zostanie zakończony w ciągu kilku sekund.  Po zakończeniu procesu aktualizacji hello otrzymasz powiadomienie.<br><br> ![Zaktualizuj stan aktualizacji modułów Azure](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> Automatyzacja Azure użyje modułów najnowszego hello na Twoim koncie automatyzacji po uruchomieniu nowego zaplanowanego zadania.    

Jeśli używasz poleceń cmdlet z tych modułów programu Azure PowerShell w Twojej toomanage elementów runbook Azure zasobów, możesz dokonać tooperform proces aktualizacji co miesiąc lub tak tooassure, czy masz hello najnowsze modułów.

## <a name="next-steps"></a>Następne kroki

* toolearn więcej informacji na temat moduły integracji i jak toocreate toofurther niestandardowe moduły integracji automatyzacji z innych systemów, usługi lub rozwiązania, zobacz [moduły integracji](automation-integration-modules.md).

* Należy rozważyć użycie integracji kontroli źródła [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) lub [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally zarządzanie i sterowanie wersjach portfela automatyzacji elementu runbook i konfiguracji.  
