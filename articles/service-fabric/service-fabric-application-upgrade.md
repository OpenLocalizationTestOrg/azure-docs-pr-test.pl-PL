---
title: "Uaktualnianie aplikacji sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera wprowadzenie do uaktualniania aplikacji usługi Service Fabric, w tym wyboru między trybami uaktualniania i zostanie wykonana kontroli kondycji."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 803c9c63-373a-4d6a-8ef2-ea97e16e88dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 5fed3b5b127a2b398b99ab2b46c762920e9dc249
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="service-fabric-application-upgrade"></a>Uaktualnianie aplikacji usługi Service Fabric
Aplikacja Azure Service Fabric jest kolekcja usług. Podczas uaktualniania usługi sieć szkieletowa porównuje nowe [manifest aplikacji](service-fabric-application-and-service-manifests.md) z poprzedniej wersji i określa usług w aplikacji wymagają aktualizacji. Sieć szkieletowa usług porównuje wersji numery w usłudze manifesty numery wersji w poprzedniej wersji. Jeśli usługa nie została zmieniona, czy usługa nie jest uaktualniony.

## <a name="rolling-upgrades-overview"></a>Omówienie uaktualnienia stopniowego
W uaktualnienia stopniowego aplikacji uaktualnienia jest wykonywane w etapach. Na każdym etapie uaktualnienie ma zostać zastosowane do podzbioru węzłów w klastrze o nazwie domeny aktualizacji. W związku z tym aplikacja pozostaje dostępne w całej uaktualnienia. Podczas uaktualniania klastra może zawierać mieszanie starej i nowej wersji.

Z tego powodu dwie wersje musi być do przodu i do tyłu zgodne. Jeśli nie są zgodne, administrator aplikacji jest odpowiedzialny za przemieszczania uaktualnienia fazy, aby zachować dostępność. Uaktualnianie fazy pierwszym krokiem jest uaktualnienie do pośredniego wersji aplikacji, która jest zgodna z poprzednią wersją. Drugim krokiem jest uaktualnienie z ostateczną wersją dzieli zgodności z wersją przed aktualizacją, ale jest niezgodny z wersją pośrednich.

Domen aktualizacji są określone w manifeście klastra podczas konfigurowania klastra. Aktualizacja domeny nie otrzymywać aktualizacje w określonej kolejności. Domena aktualizacji jest jednostka logiczna wdrożenia dla aplikacji. Aktualizacja domen Zezwalaj usługom ma pozostać w wysokiej dostępności podczas uaktualniania.

Uaktualnienia stopniowego nie są możliwe, jeśli uaktualnienie ma zostać zastosowane do wszystkich węzłów w klastrze, co ma miejsce w przypadku aplikacji ma tylko jedną domenę aktualizacji. Ta metoda nie jest zalecane, ponieważ usługa ulegnie awarii i nie jest dostępny w czasie uaktualniania. Ponadto Azure nie daje żadnej gwarancji, po skonfigurowaniu klastra z tylko jedną aktualizację domeny.

Po zakończeniu uaktualniania wszystkich usług i replicas(instances) może pozostać w tej samej wersji-np. Jeśli uaktualnienie zakończy się powodzeniem, zostaną one zaktualizowane do nowej wersji; Jeśli uaktualnienie nie powiedzie się i jest wycofana, ich będzie z powrotem obniżyć do starej wersji.

## <a name="health-checks-during-upgrades"></a>Sprawdzanie kondycji podczas uaktualniania
W przypadku uaktualnienia zasady dotyczące kondycji muszą być ustawione lub mogą zostać użyte wartości domyślne. Uaktualnienie jest określane powiodło się po uaktualnieniu wszystkich domen aktualizacji w ramach określonego limitu czasu i wszystkich domen aktualizacji zostaną uznane za dobrej kondycji.  Domeny aktualizacji w dobrej kondycji oznacza, że domeny aktualizacji przekazywany kontroli kondycji określonym w zasadach kondycji. Na przykład zasadę może wprowadzić, że wszystkie usługi w ramach wystąpienia aplikacji musi być *dobrej kondycji*, jak kondycji jest definiowana za pomocą sieci szkieletowej usług.

Zasady dotyczące kondycji i kontroli podczas uaktualniania przez sieć szkieletowa usług są niezależne od usług i aplikacji. Oznacza to, że są wykonywane żadne testy specyficzne dla usługi.  Na przykład usługa może mieć wymaganie przepływności, ale usługi sieć szkieletowa nie ma informacji, aby sprawdzić przepływności. Zapoznaj się [artykuły kondycji](service-fabric-health-introduction.md) dla testów, które są wykonywane. Sprawdza, czy mają miejsce podczas testów uaktualniania include dla tego, czy pakiet aplikacji został skopiowany poprawnie, czy wystąpienie zostało uruchomione itd.

Kondycja aplikacji jest agregacją obiektów podrzędnych w aplikacji. Innymi słowy sieć szkieletowa usług ocenia kondycję aplikację przez usługę kondycji, który jest zgłaszany w aplikacji. Oblicza również kondycję wszystkich usług dla aplikacji w ten sposób. Dodatkowe sieci szkieletowej usług ocenia kondycję usługi aplikacji przez agregowanie ich elementy podrzędne, takie jak repliki usługi kondycji. Po spełnieniu zasad dotyczących kondycji aplikacji, można kontynuować uaktualnienie. Naruszenia zasad dotyczących kondycji uaktualniania aplikacji nie powiedzie się.

## <a name="upgrade-modes"></a>Tryby uaktualnienia
Tryb, w którym firma Microsoft zaleca się uaktualnienie aplikacji jest monitorowane tryb, który jest powszechnie używany tryb. Tryb monitorowanych wykonuje uaktualnienia w domenie jedna aktualizacja, a jeśli sprawdza wszystkie dane kondycji przebiegu (na zasady określone), przechodzi do następnej domeny aktualizacji automatycznie.  Niepowodzenie sprawdzania kondycji i/lub osiągnięcia limitów czasu, uaktualnienia albo jest przywracana w domenie aktualizacji, czy tryb zostanie zmieniona na niemonitorowane ręcznie. Można skonfigurować uaktualnienia można wybrać jeden z tych dwóch trybów uaktualnienia nie powiodło się. 

Niemonitorowane ręczny tryb wymaga ręcznej interwencji po każdym uaktualnieniu domeny aktualizacji, aby rozpocząć poza uaktualniania do następnej domeny aktualizacji. Nie sieci szkieletowej usług kondycji są sprawdzane. Administrator przeprowadza kontrole kondycji lub stanu przed rozpoczęciem uaktualniania w następnej domeny aktualizacji.

## <a name="upgrade-default-services"></a>Uaktualnij usługi domyślne
Podczas procesu uaktualniania aplikacji można uaktualnić usługi domyślnej aplikacji sieci szkieletowej usług. Domyślne usługi są zdefiniowane w [manifest aplikacji](service-fabric-application-and-service-manifests.md). Standardowe reguły uaktualniania usług domyślnych są następujące:

1. Domyślne usługi w nowym [manifest aplikacji](service-fabric-application-and-service-manifests.md) który nie istnieje w klastrze są tworzone.
> [!TIP]
> [EnableDefaultServicesUpgrade](service-fabric-cluster-fabric-settings.md) musi być ustawiona na true, aby włączyć następujące reguły. Ta funkcja jest obsługiwana w wersji 5.5.

2. Domyślne usługi istniejących w obu poprzednich [manifest aplikacji](service-fabric-application-and-service-manifests.md) i nowej wersji zostały zaktualizowane. Opisy usług w nowej wersji zastąpiłaby już w klastrze. Uaktualnianie aplikacji czy wycofywania automatycznie po aktualizacji awaria usługi domyślne.
3. Domyślne usługi w poprzedniej [manifest aplikacji](service-fabric-application-and-service-manifests.md) , ale nie w nowej wersji są usuwane. **Należy zwrócić uwagę, to usunięcie usług domyślnych nie można przywrócić.**

W przypadku uaktualniania zostanie wycofana, domyślne, które usługi są przywracane do stanu przed rozpoczęciem uaktualniania. Ale usługami usunięto nigdy nie mogą być tworzone.

## <a name="application-upgrade-flowchart"></a>Schemat blokowy uaktualniania aplikacji
Schemat blokowy dalej w tym temacie mogą pomóc zrozumieć proces uaktualniania aplikacji sieci szkieletowej usług. W szczególności przepływ w tym artykule opisano sposób limity czasu, w tym *HealthCheckStableDuration*, *HealthCheckRetryTimeout*, i *UpgradeHealthCheckInterval*, pomoc Formant podczas uaktualniania w domenie jedna aktualizacja jest uznawany za powodzenie lub niepowodzenie.

![Proces uaktualniania dla aplikacji sieci szkieletowej usług][image]

## <a name="next-steps"></a>Następne kroki
[Uaktualnianie aplikacji za pomocą Visual Studio](service-fabric-application-upgrade-tutorial.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu Visual Studio.

[Uaktualnienie z aplikacji przy użyciu programu Powershell](service-fabric-application-upgrade-tutorial-powershell.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu PowerShell.

Kontrolowanie sposobu uaktualnienia aplikacji przy użyciu [uaktualnienia parametrów](service-fabric-application-upgrade-parameters.md).

Uzyskania uaktualnień aplikacji zgodnych przez poznanie [szeregowanie danych](service-fabric-application-upgrade-data-serialization.md).

Dowiedz się, jak korzystać z zaawansowanych funkcji podczas uaktualniania aplikacji, odwołując się do [Tematy zaawansowane](service-fabric-application-upgrade-advanced.md).

Rozwiązywania typowych problemów w uaktualnień aplikacji, korzystając z procedury opisanej w [Rozwiązywanie problemów z uaktualnieniami aplikacji](service-fabric-application-upgrade-troubleshooting.md).

[image]: media/service-fabric-application-upgrade/service-fabric-application-upgrade-flowchart.png
