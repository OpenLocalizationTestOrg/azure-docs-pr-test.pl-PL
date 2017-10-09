---
title: "aaaAzure usługi sieć szkieletowa kontenery monitorowania i diagnostyki | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor i diagnozowanie kontenery zorkiestrowana na usługi sieć szkieletowa usług Microsoft Azure z rozwiązaniem kontenery w OMS."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/10/2017
ms.author: dekapur
ms.openlocfilehash: cd79111cf78b9d76a60d489bb9953587aa06186d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-windows-server-containers-with-oms"></a>Monitorowanie kontenery systemu Windows Server z usługą OMS

## <a name="oms-containers-solution"></a>Rozwiązanie kontenery OMS

Witaj zespołu Operations Management Suite (OMS) został opublikowany rozwiązanie kontenery Diagnostyka i monitorowanie dla kontenerów. Równolegle z ich rozwiązanie sieci szkieletowej usług to rozwiązanie jest doskonałe narzędzie wdrożenia kontenera toomonitor zorkiestrowana w sieci szkieletowej usług. Poniżej przedstawiono prosty przykład jakie pulpitu nawigacyjnego hello w rozwiązaniu hello wygląda następująco:

![Pulpit nawigacyjny podstawowe OMS](./media/service-fabric-diagnostics-containers-windowsserver/oms-containers-dashboard.png)

Zbiera również różnych rodzajów dzienniki, które można wykonać zapytania w narzędziu analizy dzienników OMS hello, i może być używane toovisualize ani metryki zdarzenia są generowane. typy dziennika Hello, które są zbierane są:

1. ContainerInventory: zawiera informacje o lokalizacji kontenera, nazwy i obrazów
2. ContainerImageInventory: informacje o wdrożonej obrazów, w tym identyfikatory lub rozmiary
3. ContainerLog: dzienniki błędu, dzienniki docker (stdout itp.) i innych pozycji
4. ContainerServiceLog: docker demon poleceń, które zostały uruchomione
5. O wydajności: liczniki wydajności w tym kontenerze procesora cpu, pamięć, ruch sieciowy na We/Wy dysku i metryki niestandardowe z hello obsługi maszyn

W tym artykule omówiono tooset wymagane kroki hello zapasowej kontenera monitorowania dla klastra. więcej informacji na temat rozwiązania kontenery w OMS, toolearn wyewidencjonowania ich [dokumentacji](../log-analytics/log-analytics-containers.md).

## <a name="1-set-up-a-service-fabric-cluster"></a>1. Konfigurowanie klastra sieci szkieletowej usług

Tworzenie klastra przy użyciu szablonu usługi Azure Resource Manager hello znaleziono [tutaj](https://github.com/dkkapur/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Sample). Upewnij się, że tooadd unikatową nazwę obszaru roboczego OMS. Ten szablon również domyślnie toodeploying tworzenia klastra w wersji zapoznawczej hello usługi sieci szkieletowej (v255.255), co oznacza, że nie można używać w środowisku produkcyjnym, a nie można uaktualnić tooa inna wersja usługi Service Fabric. Jeśli zdecydujesz się toouse ten szablon do długoterminowych lub produkcji korzystać, Zmień numer wersji stabilnej tooa wersja hello.

Po skonfigurowaniu klastra hello Potwierdź zainstalowany odpowiedni certyfikat hello i upewnij się, że jesteś w stanie tooconnect toohello klastra.

Upewnij się, że grupy zasobów jest poprawnie skonfigurowane, nagłówek toohello [portalu Azure](https://portal.azure.com/) w celu znalezienia hello wdrożenia. Grupa zasobów Hello powinien zawierać wszystkie zasoby sieci szkieletowej usług hello, a także mieć rozwiązania analizy dzienników, a także rozwiązania sieci szkieletowej usług.

Do modyfikowania istniejącego klastra sieci szkieletowej usług:
* Potwierdź, że jest włączona diagnostyki (Jeśli nie, włącz je za pomocą [aktualizowanie zestawu skali maszyny wirtualnej hello](/rest/api/virtualmachinescalesets/create-or-update-a-set))
* Dodaj obszar roboczy OMS przez utworzenie rozwiązania "Analytics sieci szkieletowej usług" za pośrednictwem hello Azure Marketplace
* Edycja źródła danych hello toopick rozwiązania sieci szkieletowej usług hello zapasową danych z hello odpowiednie tabel usługi Azure Storage (Konfigurowanie przez WAD) w hello grupę zasobów, która hello klastra znajduje się w
* Dodanie agenta hello jako [zestaw skali maszyny wirtualnej toohello rozszerzenia](/powershell/module/azurerm.compute/add-azurermvmssextension) za pomocą programu PowerShell lub za pośrednictwem aktualizacji hello zestaw skali maszyny wirtualnej (tego samego łącza jak wyżej, szablon usługi Resource Manager hello toomodify)

## <a name="2-deploy-a-container"></a>2. Wdrażanie kontenera

Po hello klaster będzie gotowy i potwierdzeniu, że można do niego dostęp, należy wdrożyć tooit kontenera. W przypadku wybrania wersji zapoznawczej hello toouse zgodnie z ustawieniami w szablonie hello można również zapoznać się usługi sieć szkieletowa nowego rozwiązania docker compose funkcji. Opatrzone pamiętać, że hello po raz pierwszy obraz kontenera jest wdrożony tooa klastra, zajmuje kilka minut toodownload obraz powitania w zależności od rozmiaru.

## <a name="3-add-hello-containers-solution"></a>3. Dodaj rozwiązanie kontenery hello

W portalu Azure Witaj, utwórz zasób kontenerów (w obszarze hello monitorowanie i zarządzanie kategorii) za pośrednictwem portalu Azure Marketplace. 

![Dodawanie rozwiązania kontenerów](./media/service-fabric-diagnostics-containers-windowsserver/containers-solution.png)

W kroku tworzenia hello żądania obszarem roboczym pakietu OMS. Wybierz hello, który został utworzony z wdrożeniem hello powyżej. Ten krok dodaje rozwiązania kontenery w obszarze roboczym pakietu OMS i jest automatyczne wykrywany przez agenta pakietu OMS hello wdrożone przez szablon hello. Hello agent rozpocznie się zbieranie danych na procesach kontenery hello hello klastra, a w około 10 – 15 minut, powinna zostać wyświetlona rozwiązania hello światła się z danymi, tak jak obraz powitania pulpitu nawigacyjnego hello powyżej.

## <a name="4-next-steps"></a>4. Następne kroki

OMS oferuje różne narzędzia w toomake obszaru roboczego hello bardziej użyteczne dla Ciebie. Zapoznaj się z hello następujące opcje toocustomize hello rozwiązania tooyour potrzeb:
- Pobierz zapoznaniu się z hello [wyszukiwania i badania dziennika](../log-analytics/log-analytics-log-searches.md) funkcje dostępne w ramach analizy dzienników
- Skonfiguruj toopick agent pakietu OMS hello zapasowej konkretnych licznikach wydajności (Przejdź głównej obszaru roboczego toohello > Ustawienia > danych > liczników wydajności systemu Windows)
- Skonfiguruj OMS tooset się [automatycznego alerty](../log-analytics/log-analytics-alerts.md) tooaid reguł wykrywania i Diagnostyka
