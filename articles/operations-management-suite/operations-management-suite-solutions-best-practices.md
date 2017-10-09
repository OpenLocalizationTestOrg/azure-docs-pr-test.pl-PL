---
title: "najlepsze praktyki rozwiązania aaaOMSManagement | Dokumentacja firmy Microsoft"
description: 
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 08cf1c101e301d24fb5c2bf4bc02a978e508a198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-management-solutions-in-operations-management-suite-oms-preview"></a>Najlepsze rozwiązania dotyczące tworzenia rozwiązań do zarządzania w Operations Management Suite (OMS) (wersja zapoznawcza)
> [!NOTE]
> To jest wstępna dokumentacji do tworzenia rozwiązań do zarządzania w OMS, które są obecnie w wersji zapoznawczej. Żadnego schematu opisanych poniżej jest toochange podmiotu.  

W tym artykule przedstawiono najlepsze rozwiązania dotyczące [Tworzenie pliku rozwiązania zarządzania](operations-management-suite-solutions-solution-file.md) w Operations Management Suite (OMS).  Te informacje zostaną zaktualizowane określonych dodatkowych najlepszych rozwiązań.

## <a name="data-sources"></a>Źródła danych
- Źródła danych może być [skonfigurowany przy użyciu szablonu usługi Resource Manager](../log-analytics/log-analytics-template-workspace-configuration.md), ale nie powinny znajdować się w pliku rozwiązania.  Przyczyna Hello jest, że Konfigurowanie źródeł danych nie jest obecnie idempotentności, co oznacza, że rozwiązania można zastąpić istniejącą konfigurację w obszarze roboczym hello użytkownika.<br><br>Na przykład rozwiązania może wymagać ostrzeżeń i błędów zdarzenia z dziennika zdarzeń aplikacji hello.  Jeśli określisz to jako źródło danych w rozwiązaniu, istnieje ryzyko, usuwanie informacje o zdarzeniach, gdyby hello użytkownika to skonfigurowanych w ich obszaru roboczego.  Jeśli dołączysz wszystkie zdarzenia następnie użytkownik może zbierać nadmiernego informacje o zdarzeniach w obszarze roboczym hello użytkownika.

- Jeśli rozwiązanie wymaga danych z jednego źródła danych standardowe hello, następnie należy zdefiniować to jako warunek wstępny.  Stanu w dokumentacji powitania klienta należy skonfigurować źródło danych hello na ich własnych.  
- Dodaj [Weryfikacja przepływu danych](../log-analytics/log-analytics-view-designer-tiles.md) komunikat tooany widoków w użytkownika hello tooinstruct rozwiązania do źródeł danych tego toobe potrzeby skonfigurowany dla toobe wymagane dane zbierane.  Ten komunikat jest wyświetlany na kafelku hello hello widoku, gdy nie można odnaleźć wymaganych danych.


## <a name="runbooks"></a>Elementy Runbook
- Dodaj [Harmonogram automatyzacji](../automation/automation-schedules.md) dla każdego elementu runbook w rozwiązaniu wymagające toorun zgodnie z harmonogramem.
- Zawierają hello [modułu IngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) w toobe Twojego rozwiązania, używany przez elementy runbook zapisywania danych toohello analizy dzienników repozytorium.  Konfigurowanie rozwiązania hello zbyt[odwołania](operations-management-suite-solutions-solution-file.md#solution-resource) tego zasobu, tak że pozostaje usunięcie hello rozwiązania.  Dzięki temu wiele modułu hello tooshare rozwiązania.
- Użyj [zmienne automatyzacji](../automation/automation-schedules.md) tooprovide wartości toohello rozwiązania, które użytkownicy mogą później będą toochange.  Nawet jeśli rozwiązanie hello jest zmienna hello toocontain skonfigurowane, nadal można zmienić jej wartości.

## <a name="views"></a>Widoki
- Wszystkie rozwiązania powinny obejmować jeden widok, która jest wyświetlana w portalu użytkownika hello.  Witaj widok może zawierać wielu [części wizualizacji](../log-analytics/log-analytics-view-designer-parts.md) tooillustrate różnych zestawów danych.
- Dodaj [Weryfikacja przepływu danych](../log-analytics/log-analytics-view-designer-tiles.md) komunikat tooany widoków w użytkownika hello tooinstruct rozwiązania do źródeł danych tego toobe potrzeby skonfigurowany dla toobe wymagane dane zbierane.
- Konfigurowanie rozwiązania hello zbyt[zawierają](operations-management-suite-solutions-solution-file.md#solution-resource) hello widoku, dzięki czemu zostanie usunięty, jeśli rozwiązanie hello zostanie usunięty.

## <a name="alerts"></a>Alerty
- Zdefiniuj listy odbiorców hello jako parametru w pliku rozwiązania hello tak użytkownika hello je zdefiniować podczas instalacji hello rozwiązania.
- Konfigurowanie rozwiązania hello zbyt[odwołania](operations-management-suite-solutions-solution-file.md#solution-resource) reguły alertu, że użytkownik może zmienić ich konfiguracji.  Może chcą toomake zmiany, takie jak zmodyfikowanie listy adresatów hello, zmiana hello próg alertu hello lub wyłączenie hello reguły alertów. 


## <a name="next-steps"></a>Następne kroki
* Zapoznaj się z artykułem hello podstawowego procesu [projektowania i konfigurowania rozwiązania do zarządzania](operations-management-suite-solutions-creating.md).
* Dowiedz się, jak za[Utwórz plik rozwiązania](operations-management-suite-solutions-solution-file.md).
* [Dodaj zapisanych wyszukiwań i alerty](operations-management-suite-solutions-resources-searches-alerts.md) tooyour rozwiązania do zarządzania.
* [Dodawanie widoków](operations-management-suite-solutions-resources-views.md) tooyour rozwiązania do zarządzania.
* [Dodaj element runbook usługi Automatyzacja i innych zasobów](operations-management-suite-solutions-resources-automation.md) tooyour rozwiązania do zarządzania.

