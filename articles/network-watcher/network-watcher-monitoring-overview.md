---
title: tooAzure aaaIntroduction obserwatora sieciowego | Dokumentacja firmy Microsoft
description: "Ta strona zawiera omówienie hello obserwatora sieciowego usługę do monitorowania i Środek wywołujący sieć połączona zasobami na platformie Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 14bc2266-99e3-42a2-8d19-bd7257fec35e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 283b3fa6add05d9bad6d5dbdae1524344d1bfc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-monitoring-overview"></a>Omówienie monitorowania sieci platformy Azure

Klienci kompilacji na trasie sieci na platformie Azure poprzez organizowanie i tworzenia różnych zasobów poszczególnych sieci, takich jak sieci wirtualnej, ExpressRoute, bramy aplikacji i usług równoważenia obciążenia. Monitorowanie jest dostępne na każdym z zasobów sieciowych hello. Firma Microsoft można znaleźć toothis monitorowanie jako poziomu monitorowania zasobów.

Witaj zakończenia tooend sieci może mieć złożonych konfiguracji i interakcje między zasobami, tworzenie złożonych scenariuszy, które wymagają oparta na scenariuszu monitorowanie za pomocą Monitora sieci.

W tym artykule opisano scenariusz oraz monitorowania poziomu zasobów. Monitorowanie sieci na platformie Azure jest kompleksowy i obejmuje dwie szerokie kategorie:

* [**Monitor sieci** ](#network-watcher) -oparta na scenariuszu monitorowania jest dostarczana z funkcji hello w obserwatora sieciowego. Ta usługa obejmuje przechwytywania pakietów, następnego przeskoku, przepływ IP Sprawdź widok grupy zabezpieczeń, dzienniki przepływu NSG. Scenariusz poziomu monitorowania udostępnia widok tooend zakończenia zasobów sieciowych w monitorowania zasobów sieciowych tooindividual kontrastu.
* [**Monitorowanie zasobów** ](#network-resource-level-monitoring) -poziomu monitorowania zasobów składa się z czterech funkcji, dzienników diagnostycznych metryki, rozwiązywanie problemów i kondycji zasobów. Te funkcje są tworzone na poziomie zasobów sieciowych hello.

## <a name="network-watcher"></a>Network Watcher

Obserwatora sieciowego jest usługą regionalnych, która umożliwia toomonitor możesz i diagnozowanie warunki na poziomie sieci scenariusz w, do i z platformy Azure. Diagnostyka sieci i narzędzi wizualizacji dostępnych z obserwatora sieciowego pomagają zrozumieć, diagnozowanie i uzyskać informacje na temat technologii sieci tooyour na platformie Azure.

Obserwatora sieciowego ma obecnie hello następujące możliwości:

* **[Topologia](network-watcher-topology-overview.md)**  — zapewnia hello przedstawiający widok poziomu sieci różnych połączeń i skojarzenia między zasobami sieci w grupie zasobów.
* **[Zmienna przechwytywania pakietów](network-watcher-packet-capture-overview.md)**  -przechwytuje pakiet danych do i z maszyny wirtualnej. Zaawansowane filtrowanie opcje i dostosować formanty, takie jak trwa stanie tooset czasu i wszechstronność Podaj ograniczenia rozmiaru. Witaj pakietu danych mogą być przechowywane w magazynie obiektów blob lub na dysku lokalnym hello w formacie CAP.
* **[Sprawdź przepływ IP](network-watcher-ip-flow-verify-overview.md)**  — sprawdza, czy pakiet jest dozwolony lub niedozwolony na podstawie przepływ informacji 5-elementowej pakietu parametrów (docelowy adres IP, źródłowy adres IP, Port docelowy, Port źródłowy i Protocol). Jeśli pakietów hello jest zabroniony przez grupę zabezpieczeń, hello reguły i grup, które odmowa pakietów hello jest zwracana.
* **[Następny przeskok](network-watcher-next-hop-overview.md)**  — określa hello następnego skoku dla pakietów przesyłane w hello Azure sieci szkieletowej, umożliwiając tras toodiagnose any nieprawidłowo zdefiniowane przez użytkownika.
* **[Widok grupy zabezpieczeń](network-watcher-security-group-view-overview.md)**  -pobiera hello zabezpieczeń skuteczne i zastosowanej reguły, które są stosowane na maszynie Wirtualnej.
* **[Przepływ NSG rejestrowania](network-watcher-nsg-flow-logging-overview.md)**  — dzienniki przepływu dla grup zabezpieczeń sieci Włącz toocapture dzienniki pokrewne tootraffic, który ma być dozwolony lub odrzucany przez reguły zabezpieczeń hello hello grupy. Przepływ Hello jest zdefiniowana przez informacji 5-elementowej — źródłowy adres IP, docelowy adres IP, Port źródłowy, Port docelowy i protokołu.
* **[Brama sieci wirtualnej i rozwiązywanie problemów z połączenia](network-watcher-troubleshoot-manage-rest.md)**  — zapewnia hello tootroubleshoot możliwości połączenia i bramy sieci wirtualnej.
* **[Limity subskrypcji sieci](#network-subscription-limits)**  — umożliwia użycie zasobów sieciowych tooview ograniczeń.
* **[Konfigurowanie dziennika diagnostyki](#diagnostic-logs)**  — zapewnia tooenable jednego okienka lub wyłącz dzienników diagnostycznych do zasobów sieciowych w grupie zasobów.
* **[Łączność (wersja zapoznawcza)](network-watcher-connectivity-overview.md)**  -sprawdza hello możliwość ustanowienia bezpośrednie połączenie TCP z tooa maszyny wirtualnej, danego punktu końcowego.

### <a name="role-based-access-control-rbac-in-network-watcher"></a>Kontrola dostępu oparta na rolach (RBAC) w obserwatora sieciowego

Obserwatora sieciowego używa hello [modelu based kontroli dostępu (RBAC)](../active-directory/role-based-access-control-what-is.md). Witaj następujące uprawnienia są wymagane przez hello obserwatora sieciowego. Jest ważne toomake się, że ta rola hello używane do inicjowania interfejsów API obserwatora sieciowego lub za pomocą Monitora sieci z portalu hello ma dostęp hello wymagane.

|Zasób| Uprawnienie|
|---|---| 
|Microsoft.Storage/ |Odczyt|
|Microsoft.Authorization/| Odczyt| 
|Microsoft.Resources/subscriptions/resourceGroups/| Odczyt|
|Microsoft.Storage/storageAccounts/listServiceSas/ | Akcja|
|Microsoft.Storage/storageAccounts/listAccountSas/ |Akcja|
|Microsoft.Storage/storageAccounts/listKeys/ | Akcja|
|Microsoft.Compute/virtualMachines/ |Odczyt|
|Microsoft.Compute/virtualMachines/ |Zapisywanie|
|Microsoft.Compute/virtualMachineScaleSets/ |Odczyt|
|Microsoft.Compute/virtualMachineScaleSets/ |Zapisywanie|
|Microsoft.Network/networkWatchers/packetCaptures/ |Odczyt|
|Microsoft.Network/networkWatchers/packetCaptures/| Zapisywanie|
|Microsoft.Network/networkWatchers/packetCaptures/| Usuwanie|
|Microsoft.Network/networkWatchers/ |Zapisywanie |
|Microsoft.Network/networkWatchers/| Odczyt |
|Microsoft.Insights/alertRules/ |*|
|Microsoft.Support/ | *|

### <a name="network-subscription-limits"></a>Limity subskrypcji sieci

Limity subskrypcji sieci zapewniają szczegółowe informacje dotyczące użycia hello każdego zasobu sieciowego hello w ramach subskrypcji w regionie przed hello maksymalną liczbę dostępnych zasobów.

![limit subskrypcji sieci][nsl]

## <a name="network-resource-level-monitoring"></a>Poziom monitorowania zasobów sieciowych

Witaj, następujące funkcje są dostępne dla poziomu monitorowania zasobów:

### <a name="audit-log"></a>Dziennik inspekcji

Operacje wykonywane w ramach konfiguracji hello sieci są rejestrowane. Dzienniki te mogą być wyświetlane w portalu Azure hello lub pobrany przy użyciu narzędzi firmy Microsoft, takich jak usługi Power BI lub narzędzi innych firm. Dzienniki inspekcji są dostępne za pośrednictwem portalu hello, programu PowerShell, interfejsu wiersza polecenia i interfejsu API Rest. Aby uzyskać więcej informacji na dziennikach inspekcji, zobacz [inspekcji operacji za pomocą Menedżera zasobów](../resource-group-audit.md)

Dzienniki inspekcji są dostępne dla operacje wykonywane na wszystkich zasobów sieciowych.

### <a name="metrics"></a>Metryki

Metryki są miar wydajności i liczniki zebrane w danym okresie czasu. Metryki są obecnie dostępne dla bramy aplikacji. Metryki mogą być używane tootrigger alerty oparte na wartości progowej. Zobacz [diagnostyki bramy aplikacji](../application-gateway/application-gateway-diagnostics.md) tooview jak metryki mogą być używane toocreate alertów.

![Widok wskaźników][metrics]

### <a name="diagnostic-logs"></a>Dzienniki diagnostyczne

Okresowe i spontanicznych zdarzenia są tworzone przez zasobów sieciowych i zarejestrowane na kontach magazynu, wysyłane tooan Centrum zdarzeń lub analizy dzienników. Te dzienniki wgląd w kondycję hello zasobu. Te dzienniki można wyświetlać w narzędzi, takich jak Power BI i analizy dzienników. toolearn jak tooview dzienników diagnostycznych, odwiedź stronę [analizy dzienników](../log-analytics/log-analytics-azure-networking-analytics.md).

Dzienniki diagnostyczne są dostępne dla [modułu równoważenia obciążenia](../load-balancer/load-balancer-monitor-log.md), [grup zabezpieczeń sieci](../virtual-network/virtual-network-nsg-manage-log.md), trasy i [brama aplikacji w](../application-gateway/application-gateway-diagnostics.md).

Wyświetl dzienniki diagnostyczne zawiera obserwatora sieciowego. Ten widok zawiera wszystkich zasobów sieciowych, które obsługują rejestrowania diagnostycznego. Z tego widoku można włączyć i wyłączyć zasobów sieciowych, łatwo i szybko.

![dzienniki][logs]

### <a name="troubleshooting"></a>Rozwiązywanie problemów

Rozwiązywanie problemów z bloku obsługi w portalu hello Hello podano z zasobów sieciowych dzisiaj toodiagnose występujących problemów związanych z pojedynczego zasobu. To środowisko jest dostępna dla hello następujące zasoby sieciowe - ExpressRoute, Brama sieci VPN bramy aplikacji, dzienniki zabezpieczeń sieciowych, trasy, DNS, usługi równoważenia obciążenia i Menedżera ruchu. toolearn więcej informacji na temat zasobów poziomu rozwiązywania problemów, odwiedź stronę [diagnozowanie i rozwiązywanie problemów z rozwiązywaniem problemów Azure](https://azure.microsoft.com/blog/azure-troubleshoot-diagonse-resolve-issues/)

![informacje dotyczące rozwiązywania problemów][TS]

### <a name="resource-health"></a>Kondycja zasobów

Hello kondycję zasobu sieciowego znajduje się w regularnych odstępach czasu. Takie zasoby obejmują bramy sieci VPN i tunel VPN. Kondycja zasobu jest dostępny na powitania portalu Azure. toolearn więcej informacji na temat kondycji zasobów, odwiedź stronę [Przegląd kondycji zasobów](../resource-health/resource-health-overview.md)

## <a name="next-steps"></a>Następne kroki

Po zapoznawanie obserwatora sieciowego, aby dowiedzieć się do:

Czy przechwytywania pakietów, na maszynie Wirtualnej, odwiedzając [przechwytywania pakietów zmiennej w hello portalu Azure](network-watcher-packet-capture-manage-portal.md)

Wykonywanie aktywnego monitorowania i diagnostyki za pomocą [alert wyzwolony przechwytywania pakietów](network-watcher-alert-triggered-packet-capture.md).

Wykrywanie luk w zabezpieczeniach z [analizowanie przechwytywania pakietów z programu Wireshark](network-watcher-deep-packet-inspection.md), za pomocą narzędzi typu open source.

Dowiedz się więcej o niektórych hello innego klucza [możliwości w zakresie obsługi](../networking/networking-overview.md) platformy Azure.

<!--Image references-->
[TS]: ./media/network-watcher-monitoring-overview/troubleshooting.png
[logs]: ./media/network-watcher-monitoring-overview/logs.png
[metrics]: ./media/network-watcher-monitoring-overview/metrics.png
[nsl]: ./media/network-watcher-monitoring-overview/nsl.png











