---
title: "Odkryj, jakie oprogramowanie jest zainstalowane na Twoich maszynach, za pomocą usługi Azure Automation | Microsoft Docs"
description: "Użyj spisu, aby dowiedzieć się, jakie oprogramowanie jest zainstalowane na maszynach w Twoim środowisku."
services: automation
keywords: "spis, automatyzacja, zmiana, śledzenie"
author: jennyhunter-msft
ms.author: jehunte
ms.date: 12/14/2017
ms.topic: tutorial
ms.service: automation
ms.custom: mvc
manager: carmonm
ms.openlocfilehash: bdd638d0612a8ddee1a0ddb4fd4579f8da14b887
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/10/2018
---
# <a name="discover-what-software-is-installed-on-your-azure-and-non-azure-machines"></a>Wykrywanie, jakie oprogramowanie jest zainstalowane na maszynach na platformie Azure i poza platformą Azure

W tym samouczku dowiesz się, jak wykryć, jakie oprogramowanie jest zainstalowane w danym środowisku. Możesz zbierać i wyświetlać spis oprogramowania, plików, demonów systemu Linux, usług systemu Windows i kluczy rejestru systemu Windows znajdujących się na Twoich komputerach. Śledzenie konfiguracji maszyn ułatwia identyfikowanie problemów operacyjnych w środowisku oraz lepsze rozumienie stanu maszyn.

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Dodawanie maszyny wirtualnej do śledzenia zmian i spisu
> * Wyświetlanie zainstalowanego oprogramowania
> * Dzienniki przeszukiwania zapasów dla zainstalowanego oprogramowania

## <a name="prerequisites"></a>Wymagania wstępne

Do ukończenia tego samouczka niezbędne są następujące elementy:

* Subskrypcja platformy Azure. Jeśli nie masz subskrypcji, możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
* [Konto automatyzacji](automation-offering-get-started.md) do przechowywania obserwatora i elementów Runbook akcji oraz zadania obserwatora.
* [Maszyna wirtualna](../virtual-machines/windows/quick-create-portal.md) do dołączenia.

## <a name="log-in-to-azure"></a>Zaloguj się do platformy Azure.

Zaloguj się w witrynie Azure Portal pod adresem http://portal.azure.com.

## <a name="enable-change-tracking-and-inventory"></a>Włączanie śledzenia zmian i spisu

Najpierw musisz włączyć śledzenie zmian i spisu dla maszyny wirtualnej w tym samouczku. Jeśli inne rozwiązanie automatyzacji zostało wcześniej włączone dla maszyny wirtualnej, ten krok nie jest konieczny.

1. W menu po lewej stronie wybierz pozycję **Maszyny wirtualne** i wybierz z listy maszynę wirtualną
2. W menu po lewej stronie w obszarze **Operacje** kliknij pozycję **Spis**. Zostanie otwarta strona **Włączanie śledzenia zmian i spisu**.

Jest przeprowadzana walidacja w celu ustalenia, czy spis jest włączony dla tej maszyny wirtualnej.
Walidacja obejmuje kontrole obszaru roboczego usługi Log Analytics i powiązanego konta usługi Automation i tego, czy rozwiązanie znajduje się w obszarze roboczym.

Obszar roboczy usługi [Log Analytics](../log-analytics/log-analytics-overview.md?toc=%2fazure%2fautomation%2ftoc.json) służy do zbierania danych generowanych przez funkcje i usługi, takie jak spis.
Obszar roboczy zawiera pojedynczą lokalizację do przeglądania i analizowania danych z wielu źródeł.

Proces walidacji sprawdza również, czy maszyna wirtualna jest aprowizowana za pomocą programu Microsoft Monitoring Agent (MMA) i hybrydowego procesu roboczego.
Ten agent jest używany do komunikacji z maszyną wirtualną i uzyskiwania informacji dotyczących zainstalowanego oprogramowania.
Proces walidacji sprawdza również, czy maszyna wirtualna jest aprowizowana za pomocą programu Microsoft Monitoring Agent (MMA) i hybrydowego procesu roboczego elementu Runbook usługi Automation.

Jeśli te wymagania wstępne nie są spełnione, zostanie wyświetlony transparent zawierający opcję włączenia rozwiązania.

![Transparent konfiguracji dołączony do spisu](./media/automation-tutorial-installed-software/enableinventory.png)

Kliknij transparent, aby włączyć rozwiązanie.
Jeśli którekolwiek z następujących wymagań wstępnych nie będzie występować po walidacji, zostanie ono automatycznie dodane:

* Obszar roboczy usługi [Log Analytics](../log-analytics/log-analytics-overview.md?toc=%2fazure%2fautomation%2ftoc.json)
* [Automatyzacja](./automation-offering-get-started.md)
* [Hybrydowy proces roboczy elementu Runbook](./automation-hybrid-runbook-worker.md) jest włączony na maszynie wirtualnej

Został otwarty ekran **Śledzenie zmian i spis**. Skonfiguruj lokalizację, obszar roboczy usługi Log Analytics i konto usługi Automation, a następnie kliknij pozycję **Włącz**. Jeśli pola są wygaszone, oznacza to, że inne rozwiązanie automatyzacji jest włączone dla maszyny wirtualnej, a tym samym należy użyć tego samego obszaru roboczego i konta automatyzacji.

![Okno włączania rozwiązania do śledzenia zmian](./media/automation-tutorial-installed-software/installed-software-enable.png)

Włączanie rozwiązania może potrwać do 15 minut. W tym czasie nie należy zamykać okna przeglądarki.
Po włączeniu rozwiązania informacje dotyczące zainstalowanego oprogramowania i zmian w maszynie wirtualnej są przekazywane do usługi Log Analytics.
Udostępnienie danych do analizy może potrwać od 30 minut do 6 godzin.

## <a name="view-installed-software"></a>Wyświetlanie zainstalowanego oprogramowania

Po włączeniu rozwiązania śledzenia zmian i spisu możesz wyświetlić wyniki na stronie **Spis**.

W ramach maszyny wirtualnej zaznacz pozycję **Spis** w obszarze **OPERACJE**.

Na stronie **Spis** kliknij kartę **Oprogramowanie**.

Na karcie **Oprogramowanie** znajduje się lista tabelowa oprogramowania, które zostało odnalezione. Oprogramowanie jest grupowane według nazwy i wersji oprogramowania.

Szczegółowe informacje wysokiego poziomu dotyczące każdego rekordu oprogramowania są wyświetlane w tabeli. Te szczegółowe informacje obejmują nazwę oprogramowania, wersję, wydawcę, czas ostatniego odświeżenia (ostatni czas odświeżania zgłoszony przez maszynę w grupie) i maszyny (liczba maszyn z tym oprogramowaniem).

![Spis oprogramowania](./media/automation-tutorial-installed-software/inventory-software.png)

Kliknij wiersz, aby wyświetlić właściwości rekordu oprogramowania i nazwy maszyn z tym oprogramowaniem.

Aby znaleźć określone oprogramowanie lub grupę oprogramowania, możesz je wyszukać w polu tekstowym bezpośrednio nad listą oprogramowania.
Filtr umożliwia wyszukiwanie na podstawie nazwy oprogramowania, wersji lub wydawcy.

Na przykład wyszukiwanie „Contoso” zwraca całe oprogramowanie mające w nazwie, wydawcy lub wersji ciąg „Contoso”.

## <a name="search-inventory-logs-for-installed-software"></a>Dzienniki przeszukiwania zapasów dla zainstalowanego oprogramowania

Spis generuje dane dziennika, które są wysyłane do usługi Log Analytics. Aby wyszukiwać w dziennikach za pomocą uruchamiania zapytań, wybierz pozycję **Log Analytics** w górnej części okna **Spis**.

Dane spisu są przechowywane w obszarze typu **ConfigurationData**.
Następujące przykładowe zapytanie usługi Log Analytics zwraca wydawców zawierających słowo „Microsoft” i liczbę rekordów oprogramowania (pogrupowanych według typu SoftwareName i Computer) dla każdego wydawcy.

```
ConfigurationData
| summarize arg_max(TimeGenerated, *) by SoftwareName, Computer
| where ConfigDataType == "Software"
| search Publisher:"Microsoft"
| summarize count() by Publisher
```

Aby dowiedzieć się więcej na temat uruchamiania i wyszukiwania plików dziennika w usłudze Log Analytics, zobacz [Azure Log Analytics](https://docs.loganalytics.io/index).

### <a name="single-machine-inventory"></a>Spis dla pojedynczego komputera

Aby wyświetlić spis oprogramowania dla pojedynczego komputera, możesz uzyskać dostęp do spisu ze strony zasobu maszyny wirtualnej platformy Azure lub użyć usługi Log Analytics do odfiltrowania odpowiedniej maszyny. Poniższe przykładowe zapytanie usługi Log Analytics zwraca listę oprogramowania dla maszyny o nazwie ContosoVM.

```
ConfigurationData
| where ConfigDataType == "Software" 
| summarize arg_max(TimeGenerated, *) by SoftwareName, CurrentVersion
| where Computer =="ContosoVM"
| render table
```

## <a name="next-steps"></a>Kolejne kroki

W tym samouczku przedstawiono sposób wyświetlania spisu oprogramowania, np.:

> [!div class="checklist"]
> * Dodawanie maszyny wirtualnej do śledzenia zmian i spisu
> * Wyświetlanie zainstalowanego oprogramowania
> * Dzienniki przeszukiwania zapasów dla zainstalowanego oprogramowania

Przejdź do omówienia rozwiązania śledzenia zmian i spisu, aby uzyskać więcej informacji.

> [!div class="nextstepaction"]
> [Change management and Inventory solution](../log-analytics/log-analytics-change-tracking.md?toc=%2fazure%2fautomation%2ftoc.json) (Rozwiązanie zarządzania zmianami i spisem)