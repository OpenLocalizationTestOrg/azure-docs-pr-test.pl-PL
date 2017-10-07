---
title: aaaOverview metryk w Microsoft Azure | Dokumentacja firmy Microsoft
description: "Omówienie metryki i ich użycie w Microsoft Azure"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 405ec51c-0946-4ec9-b535-60f65c4a5bd1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: johnkem
ms.openlocfilehash: 2b97f51e0554dae95a929241ae1f0e25e5c215ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Omówienie metryk w Microsoft Azure
W tym artykule opisano, jakie są metryk w Microsoft Azure, ich zalety oraz sposób toostart za ich pomocą.  

## <a name="what-are-metrics"></a>Co to są metryk?
Azure Monitor umożliwia tooconsume telemetrii toogain wgląd w hello wydajności i kondycji obciążeń na platformie Azure. Typ najważniejszych Hello danych telemetrycznych platformy Azure jest metryki hello (nazywanych również liczniki wydajności) emitowane przez zasoby najbardziej platformy Azure. Azure Monitor udostępnia kilka sposobów tooconfigure i korzystać z tych metryk do monitorowania i rozwiązywania problemów.

## <a name="what-can-you-do-with-metrics"></a>Co należy zrobić z metryk
Metryki są cenne źródła danych telemetrycznych i umożliwiają hello toodo następujące zadania:

* **Śledzenie wydajności hello** zasobu (np. maszyna wirtualna, witryny sieci Web lub logiki aplikacji) kreślenia jego metryki na wykresie portalu i przypinanie tego pulpitu nawigacyjnego tooa wykresu.
* **Otrzymuj powiadomienia o problemie** czy wpływ metrykę przecina pewnej wartości progowej, hello wydajności zasobu.
* **Konfigurowanie automatycznych akcji**, takich jak skalowanie automatyczne zasobu lub wyzwalania elementu runbook, gdy metryki przecina pewnej wartości progowej.
* **Wykonywać zaawansowane analizy** lub zgłaszanie trendów wydajności lub użycia zasobu.
* **Archiwum** hello historii wydajności lub kondycji zasobu **zgodności lub inspekcji** celów.

## <a name="what-are-hello-characteristics-of-metrics"></a>Co to są właściwości hello metryk?
Metryki są hello następujące cechy:

* Wszystkie metryki ma **częstotliwość co minutę**. Pojawi się wartość metryki co minutę z zasobu, umożliwiając niemal w czasie rzeczywistym wgląd w stan hello i kondycji zasobu.
* Metryki są **dostępne natychmiast**. Nie należy tooopt w lub konfigurowanie dodatkowych diagnostyczne.
* Dostęp można uzyskać **30 dni historii** dla każdego metryki. Można szybko przyjrzeć się hello ostatnie i miesięczne trendów wydajności hello lub kondycji zasobu.

Możesz również:

* Skonfiguruj metrykę **alert regułę, która wyśle powiadomienie, lub przyjmuje automatycznego akcji** po Metryka hello przecina hello próg, która została zdefiniowana. Skalowania automatycznego jest akcję do automatycznego specjalną, która włącza tooscale limit żądań przychodzących toomeet zasobów lub obciążenia na witrynie sieci Web lub zasobów obliczeniowych. Można skonfigurować ustawienie tooscale reguły przychodzący lub wychodzący oparciu metryki przekroczenia progu skalowania automatycznego.

* **Trasy** wszystkie metryki usługi Application Insights lub analizy dzienników (OMS) tooenable błyskawicznych analytics, wyszukiwanie i niestandardowe alerty dla danych metryk z Twoich zasobów. Można również strumienia tooan metryki Centrum zdarzeń, umożliwiając toothen kierowania ich tooAzure Stream Analytics lub toocustom aplikacji do analizy w czasie niemal rzeczywistym. Możesz skonfigurować Centrum zdarzeń przesyłania strumieniowego przy użyciu ustawień diagnostycznych.

* **Archiwum toostorage metryki** dłużej okresu przechowywania lub używać ich na potrzeby raportowania w trybie offline. Można przekierować tooAzure Twojego metryki magazynu obiektów Blob, podczas konfigurowania ustawień diagnostycznych dla zasobu.

* Łatwo odnaleźć, dostęp, i **wyświetlić wszystkie metryki** za pośrednictwem hello portalu Azure, wybierz zasób i wykreślenia hello metryki na wykresie.

* **Korzystać z** metryki hello za pośrednictwem hello nowych interfejsów API REST Monitor Azure.

* **Zapytanie** metryki przy użyciu poleceń cmdlet programu PowerShell hello lub hello interfejsu API REST i Platform.

  ![Routing metryk w Monitorze systemu Azure](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-hello-portal"></a>Metryki dostęp za pośrednictwem portalu hello
Poniżej znajduje się Przewodnik Szybki sposób toocreate metryki wykresu przy użyciu hello portalu Azure.

### <a name="tooview-metrics-after-creating-a-resource"></a>metryki tooview po utworzeniu zasobu
1. Otwórz hello portalu Azure.
2. Tworzenie witryny sieci Web platformy Azure App Service.
3. Po utworzeniu witryny sieci Web, przejdź toohello **omówienie** bloku hello witryny sieci Web.
4. Możesz wyświetlić nowe metryki jako **monitorowanie** kafelka. Następnie możesz edytować kafelka hello i wybrać więcej metryki.

   ![Metryki dla zasobu w monitorze Azure](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="tooaccess-all-metrics-in-a-single-place"></a>tooaccess wszystkie metryki w jednym miejscu
1. Otwórz hello portalu Azure.
2. Przejdź toohello nowe **Monitor** kartę i hello, a następnie wybierz opcję **metryki** opcji podrzędne.
3. Wybierz Twojej subskrypcji, grupy zasobów i nazwy hello hello zasobu z listy rozwijanej hello.
4. Umożliwia wyświetlenie listy dostępnych metryk hello. Następnie wybierz metrykę hello interesuje i wykreślenia go.
5. Można przypiąć go toohello pulpitu nawigacyjnego, klikając pin hello na powitania prawym górnym rogu.

   ![Dostęp do wszystkich metryki w jednym miejscu w monitorze Azure](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> Dostępne metryki na poziomie hosta maszyn wirtualnych (w oparciu o usługi Azure Resource Manager) i zestawach skali maszyn wirtualnych bez żadnych dodatkowych diagnostyczne instalacji. Te nowe metryki poziomu hostów są dostępne dla wystąpień systemu Windows i Linux. Te metryki nie są toobe mylić z hello metryki poziomie systemu operacyjnego gościa, czy masz toowhen dostępu, który włączyć diagnostyki Azure na maszynach wirtualnych lub zestawy skalowania maszyny wirtualnej. toolearn więcej informacji o konfigurowaniu diagnostycznych, zobacz [co to jest Microsoft Azure Diagnostics](../azure-diagnostics.md).
>
>

## <a name="access-metrics-via-hello-rest-api"></a>Metryki dostęp za pośrednictwem hello interfejsu API REST
Metryki Azure są dostępne za pośrednictwem hello interfejsów API usługi Azure monitora. Istnieją dwa interfejsy API, które ułatwiają odnajdywanie i dostęp do metryk:

* Użyj hello [Metryka Monitor Azure definicji interfejsu API REST](https://msdn.microsoft.com/library/mt743621.aspx) tooaccess hello listy metryk, które są dostępne dla usługi.
* Użyj hello [interfejsu API REST Azure Monitor metryki](https://msdn.microsoft.com/library/mt743622.aspx) tooaccess hello metryki rzeczywiste dane.

> [!NOTE]
> W tym artykule opisano metryki hello za pośrednictwem hello [nowy interfejs API dla metryki](https://msdn.microsoft.com/library/dn931930.aspx) dla zasobów platformy Azure. wersja interfejsu API Hello hello nowe definicje metryki interfejsu API jest 2016-03-01, a wersja powitania dla metryki interfejsu API jest 2016-09-01. Hello starszej wersji definicji metryk i metryki są dostępne z hello interfejsu API w wersji 2014-04-01.
>
>

Bardziej szczegółowy przewodnik przy użyciu hello interfejsów API REST Monitor Azure, zobacz [interfejsu API REST Monitor Azure wskazówki](monitoring-rest-api-walkthrough.md).

## <a name="export-metrics"></a>Metryki eksportu
Można przejść toohello **ustawień diagnostycznych** bloku w obszarze hello **Monitor** kartę i widoku hello opcje eksportowania metryki. Można wybrać metryki (i dzienników diagnostycznych) toobe kierowane tooBlob magazynu, centra zdarzeń tooAzure lub tooOMS dla przypadków użycia, które zostały wymienione wcześniej w tym artykule.

 ![Opcji eksportu dla metryki w monitorze Azure](./media/monitoring-overview-metrics/MetricsOverview3.png)

Ustawienie to można skonfigurować za pomocą szablonów usługi Resource Manager [PowerShell](insights-powershell-samples.md), [interfejsu wiersza polecenia Azure](insights-cli-samples.md), lub [interfejsów API REST](https://msdn.microsoft.com/library/dn931943.aspx).

## <a name="take-action-on-metrics"></a>Podejmij działanie metryk
powiadomienia tooreceive lub podejmij automatyczne akcje na dane, można skonfigurować reguły alertów lub ustawienia skalowania automatycznego.

### <a name="configure-alert-rules"></a>Skonfiguruj reguły alertu
Reguły alertów można skonfigurować na metryki. Te reguły alertów można sprawdzić, czy metrykę przekroczyło określony próg. Następnie można powiadomienia pocztą e-mail lub wyzwalać elementu webhook, które mogą być używane toorun dowolnego skryptu niestandardowego. Umożliwia także hello elementu webhook tooconfigure produktów innych firm integracji.

 ![Metryki i reguły alertów w monitorze Azure](./media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a>Funkcja automatycznego skalowania Azure zasobów
Niektórych zasobów platformy Azure obsługuje hello skalowanie out lub w wielu wystąpień toohandle obciążeń. Funkcja automatycznego skalowania dotyczy tooApp usługi (aplikacji sieci Web), zestawy skalowania maszyny wirtualnej i klasycznym usługi w chmurze Azure. Można skonfigurować tooscale reguł skalowania automatycznego out lub w, gdy niektóre metryka ma wpływ na obciążenie przecina od wartości progowej. Aby uzyskać więcej informacji, zobacz [omówienie Skalowanie automatyczne](monitoring-overview-autoscale.md).

 ![Metryki i automatycznego skalowania w Monitorze systemu Azure](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a>Więcej informacji na temat obsługiwanych usług i metryki
Azure Monitor to nowa infrastruktura metryki. Obsługuje ona hello następujących usług platformy Azure w hello Azure portal i hello nowej wersji interfejsu API Azure Monitor hello:

* Maszyny wirtualne (na podstawie Menedżera zasobów Azure)
* Zestawy skalowania maszyn wirtualnych
* Batch
* Centra zdarzeń w przestrzeni nazw
* Przestrzeń nazw magistrali usług (tylko premium SKU)
* Baza danych SQL (wersja 12)
* Puli elastycznej SQL
* Witryny sieci Web
* Farmach serwerów sieci Web
* Logic Apps
* Centra IoT
* Pamięć podręczna Redis
* Sieci: Bramy aplikacji
* Wyszukiwanie

Można wyświetlić szczegółową listę wszystkich usług hello obsługiwane oraz ich metryk [Azure Monitor metryki — obsługiwanych metryki na typ zasobu](monitoring-supported-metrics.md).

## <a name="next-steps"></a>Następne kroki
Odnoszą się łącza toohello w tym artykule. Ponadto więcej informacji na temat:  

* [Typowe metryki skalowania automatycznego](insights-autoscale-common-metrics.md)
* [Jak toocreate reguły alertów](insights-alerts-portal.md)
* [Analizowanie dzienników z usługi Azure storage z analizy dzienników](../log-analytics/log-analytics-azure-storage.md)
