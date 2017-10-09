---
title: aaaEnable monitorowania i diagnostyki w Microsoft Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooset się diagnostyki dla zasobów na platformie Azure."
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
ms.openlocfilehash: 865d010c5846fff6d871e20eca2bc4ac35028354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-monitoring-and-diagnostics"></a>Włączanie monitorowania i diagnostyki
W hello [Azure Portal](https://portal.azure.com), można skonfigurować rozbudowane, często, monitorowania i diagnostyki danych dotyczących zasobów. Można również użyć hello [interfejsu API REST](https://msdn.microsoft.com/library/azure/dn931932.aspx) lub [zestawu .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) diagnostyki tooconfigure programowo.

Dane diagnostykę, monitorowanie i metryki na platformie Azure są zapisywane do wybranego konta magazynu. Dzięki temu można toouse niezależnie od narzędzi tooread hello danych, z Eksploratora magazynu, narzędziami firm toothird BI tooPower.

## <a name="when-you-create-a-resource"></a>Podczas tworzenia zasobu
Większość usług umożliwiają diagnostyki tooenable po ich utworzeniu w hello [Azure Portal](https://portal.azure.com).

1. Przejdź za**nowy** i wybierz zasób hello planuje się.
2. Wybierz **konfiguracji opcjonalnej**.
    ![Diagnostyka bloku](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)
3. Wybierz **diagnostyki**i kliknij przycisk **na**. Konieczne będzie konto magazynu hello toochoose, które mają toobe diagnostyki zapisane. Będzie można z naliczaniem normalnych stawek dane magazynu i transakcji wysyłania konto magazynu diagnostyki tooa.
4. Kliknij przycisk **OK** i utworzyć hello zasobu.

## <a name="change-settings-for-an-existing-resource"></a>Zmiany ustawień dla istniejącego zasobu
Jeśli utworzono już zasobu i ustawienia diagnostyki hello toochange (toochange hello poziom zbierania danych, na przykład), należy to prawo w hello portalu Azure.

1. Przejdź toohello zasobów, a następnie kliknij przycisk hello **ustawienia** polecenia.
2. Wybierz **diagnostyki**.
3. Witaj **diagnostyki** blok zawiera wszystkie możliwe diagnostyki hello i zbierania danych monitorowania dla tego zasobu. Dla niektórych zasobów można także **przechowywania** zasady dla danych hello, tooclean go z Twojego konta magazynu.
    ![Diagnostyka magazynu](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)
4. Po wybraniu ustawienia, kliknij przycisk hello **zapisać** polecenia. Może upłynąć trochę podczas do monitorowania danych tooshow się, Jeśli włączasz go na powitania po raz pierwszy.

### <a name="categories-of-data-collection-for-virtual-machines"></a>Kategorie zbierania danych dla maszyn wirtualnych
W przypadku maszyn wirtualnych wszystkie metryki i dzienniki będą rejestrowane w odstępach, co pozwoli zawsze hello większości aktualne informacje o komputerze.

* **Podstawowe metryki** : kondycji metryk dotyczących Twojej maszyny wirtualnej, takie jak procesor i pamięć
* **Metryki sieci i sieci web** : metryki o połączeń sieciowych i usług sieci web
* **Metryki .NET** : metryk dotyczących aplikacji .NET i ASP.NET hello uruchomionych na maszynie wirtualnej
* **Metryki SQL** : Jeśli używasz usługi SQL firmy Microsoft, jej metryki wydajności
* **Dzienniki aplikacji zdarzeń systemu Windows** : zdarzeń systemu Windows, które są wysyłane toohello aplikacji kanału
* **Dzienniki systemu zdarzeń systemu Windows** : zdarzeń systemu Windows, które są wysyłane toohello systemu kanału. Obejmuje to także wszystkie zdarzenia z [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).
* **Dzienniki zabezpieczeń zdarzeń systemu Windows** : zdarzeń systemu Windows, które są wysyłane toohello kanału zabezpieczeń
* **Diagnostyka infrastruktury dzienniki** : rejestrowanie dotyczące hello diagnostyki kolekcji infrastruktury
* **Dzienniki programu IIS** : dzienniki o serwerze IIS

Należy zauważyć, że w tym momencie niektórych dystrybucji systemu Linux nie są obsługiwane i, hello Agent gościa musi być zainstalowany na maszynie wirtualnej hello.

## <a name="next-steps"></a>Następne kroki
* [Odbieraj powiadomienia o alertach](insights-receive-alert-notifications.md) zawsze, gdy wystąpią zdarzenia operacyjne lub metryki przekroczą próg.
* [Monitorowanie metryk usługi](insights-how-to-customize-monitoring.md) toomake się, że usługa jest dostępna i elastyczny.
* [Automatyczne skalowanie liczby wystąpień](insights-how-to-scale.md) toomake się, że Twoje skali usługi na podstawie zapotrzebowania.
* [Monitorowanie wydajności aplikacji](../application-insights/app-insights-azure-web-apps.md) Jeśli toounderstand dokładnie, jak kod działa w chmurze hello.
* [Wyświetl zdarzenia i dziennik aktywności](insights-debugging-with-events.md) toolearn wszystkie czynności, które miało miejsce w usłudze.
* [Kondycja usługi śledzenia](insights-service-health.md) toofind się po Azure napotkał wydajności degradacji lub usługi przerw w działaniu.

