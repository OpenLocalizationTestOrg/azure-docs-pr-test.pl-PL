---
title: "Włączanie monitorowania i diagnostyki w Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować diagnostykę dla zasobów na platformie Azure."
author: rboucher
manager: carolz
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: af1947a9-c211-4aa1-8924-880a86240be4
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: b82bb1ab419831e803689edb2a2a7fe256dde5a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-monitoring-and-diagnostics"></a>Włączanie monitorowania i diagnostyki
W [Azure Portal](https://portal.azure.com), można skonfigurować rozbudowane, często, monitorowania i diagnostyki danych dotyczących zasobów. Można również użyć [interfejsu API REST](https://msdn.microsoft.com/library/azure/dn931932.aspx) lub [zestawu .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) programowe Konfigurowanie diagnostyki.

Dane diagnostykę, monitorowanie i metryki na platformie Azure są zapisywane do wybranego konta magazynu. Dzięki temu można użyć dowolnego narzędzia, które chcesz odczytać danych z Eksploratora magazynu do usługi Power BI do narzędzi innych firm.

## <a name="when-you-create-a-resource"></a>Podczas tworzenia zasobu
Większość usług umożliwiają Włącz diagnostykę, podczas tworzenia ich w [Azure Portal](https://portal.azure.com).

1. Przejdź do **nowy** i wybierz zasób planuje się.
2. Wybierz **konfiguracji opcjonalnej**.
    ![Diagnostyka bloku](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)
3. Wybierz **diagnostyki**i kliknij przycisk **na**. Należy wybrać konta magazynu, które mają diagnostyki do zapisania. Będzie można z naliczaniem normalnych stawek za magazynu i transakcji dane wysyłanie danych diagnostycznych na konto magazynu.
4. Kliknij przycisk **OK** i utworzenia zasobu.

## <a name="change-settings-for-an-existing-resource"></a>Zmiany ustawień dla istniejącego zasobu
Jeśli utworzono już zasobu i chcesz zmienić ustawienia diagnostyczne (Aby zmienić poziom zbierania danych, na przykład), możesz to zrobić to prawo w portalu Azure.

1. Przejdź do zasobów i kliknij przycisk **ustawienia** polecenia.
2. Wybierz **diagnostyki**.
3. **Diagnostyki** blok zawiera wszystkie możliwe diagnostyki i monitorowania danych kolekcji dla tego zasobu. Dla niektórych zasobów można także **przechowywania** zasady dla danych, aby wyczyścić z konta magazynu.
    ![Diagnostyka magazynu](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)
4. Po wybraniu ustawienia, kliknij przycisk **zapisać** polecenia. Może upłynąć trochę podczas do monitorowania danych wyświetlani, Jeśli włączasz go po raz pierwszy.

### <a name="categories-of-data-collection-for-virtual-machines"></a>Kategorie zbierania danych dla maszyn wirtualnych
W przypadku maszyn wirtualnych wszystkie metryki i dzienniki będą rejestrowane w odstępach, więc mogą zawsze się najbardziej aktualne informacje o komputerze.

* **Podstawowe metryki** : kondycji metryk dotyczących Twojej maszyny wirtualnej, takie jak procesor i pamięć
* **Metryki sieci i sieci web** : metryki o połączeń sieciowych i usług sieci web
* **Metryki .NET** : metryk dotyczących aplikacji .NET i platformy ASP.NET działających na maszynie wirtualnej
* **Metryki SQL** : Jeśli używasz usługi SQL firmy Microsoft, jej metryki wydajności
* **Dzienniki aplikacji zdarzeń systemu Windows** : zdarzeń systemu Windows, które są wysyłane do kanału aplikacji
* **Dzienniki systemu zdarzeń systemu Windows** : zdarzeń systemu Windows, które są wysyłane do kanału systemu. Obejmuje to także wszystkie zdarzenia z [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).
* **Dzienniki zabezpieczeń zdarzeń systemu Windows** : zdarzeń systemu Windows, które są wysyłane do kanału zabezpieczeń
* **Diagnostyka infrastruktury dzienniki** : rejestrowanie dotyczące infrastruktury kolekcji diagnostyki
* **Dzienniki programu IIS** : dzienniki o serwerze IIS

Należy pamiętać, że w tym momencie niektórych dystrybucji systemu Linux nie są obsługiwane i musi być zainstalowany Agent gościa na maszynie wirtualnej.

## <a name="next-steps"></a>Następne kroki
* [Odbieraj powiadomienia o alertach](insights-receive-alert-notifications.md) zawsze, gdy wystąpią zdarzenia operacyjne lub metryki przekroczą próg.
* [Monitorowanie metryk usługi](insights-how-to-customize-monitoring.md) się upewnić, że usługa jest dostępna i elastyczny.
* [Automatyczne skalowanie liczby wystąpień](insights-how-to-scale.md) aby upewnić się na skalę usługi na podstawie zapotrzebowania.
* [Monitorowanie wydajności aplikacji](../application-insights/app-insights-azure-web-apps.md) Jeśli chcesz zrozumieć, dokładnie tak jak wykonywanie kodu w chmurze.
* [Wyświetl zdarzenia i dziennik aktywności](insights-debugging-with-events.md) Aby dowiedzieć się wszystkie zasoby, które miało miejsce w usłudze.
* [Kondycja usługi śledzenia](insights-service-health.md) Aby dowiedzieć się, gdy Azure napotkał wydajności degradacji lub usługi przerw w działaniu.

