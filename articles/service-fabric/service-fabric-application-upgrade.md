---
title: Uaktualnianie aplikacji Fabric aaaService | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera tooupgrading wprowadzenie aplikacji usługi Service Fabric, w tym wyboru między trybami uaktualniania i zostanie wykonana kontroli kondycji."
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
ms.openlocfilehash: 6f649ef4a5c0afab682522bcba7d2d66a4268ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade"></a>Uaktualnianie aplikacji usługi Service Fabric
Aplikacja Azure Service Fabric jest kolekcja usług. Podczas uaktualniania usługi sieć szkieletowa porównuje hello nowe [manifest aplikacji](service-fabric-application-model.md#describe-an-application) z poprzednią wersją hello i określa, które usługi w aplikacji hello wymagają aktualizacji. Sieć szkieletowa usług porównuje wersję hello numery w usłudze hello manifesty z numerami wersji hello hello poprzedniej wersji. Jeśli usługa nie została zmieniona, czy usługa nie jest uaktualniony.

## <a name="rolling-upgrades-overview"></a>Omówienie uaktualnienia stopniowego
W uaktualnienia stopniowego aplikacji hello uaktualnienia jest wykonywane w etapach. Na każdym etapie uaktualnianie hello jest stosowane tooa podzbioru węzłów w klastrze hello o nazwie domeny aktualizacji. W związku z tym aplikacji hello pozostaje dostępne w całej hello uaktualnienia. Podczas uaktualniania hello hello klastra może zawierać kombinację hello starej i nowej wersji.

Z tego powodu Witaj dwie wersje muszą być do przodu i do tyłu zgodne. Jeśli nie są zgodne, administrator aplikacji hello jest odpowiedzialny za przemieszczania dostępności fazy toomaintain uaktualnienia. Uaktualnianie fazy hello pierwszym krokiem jest uaktualnienie tooan pośrednich wersji aplikacji hello, która jest zgodna z poprzednią wersją hello. drugi etap Hello jest tooupgrade hello ostateczną wersją dzieli zgodności z wersją przed aktualizacją hello, ale jest niezgodny z wersją pośredniego hello.

Domen aktualizacji są określone w manifeście klastra hello podczas konfigurowania klastra hello. Aktualizacja domeny nie otrzymywać aktualizacje w określonej kolejności. Domena aktualizacji jest jednostka logiczna wdrożenia dla aplikacji. Domen aktualizacji Zezwalaj hello tooremain usług o wysokiej dostępności podczas uaktualniania.

Uaktualnienia stopniowego nie są możliwe w przypadku uaktualniania hello tooall zastosowane węzłów w klastrze hello sytuacja hello aplikacji hello ma tylko jedną domenę aktualizacji. Ta metoda nie jest zalecane, ponieważ usługa hello ulegnie awarii i nie jest dostępny w czasie hello uaktualnienia. Ponadto Azure nie daje żadnej gwarancji, po skonfigurowaniu klastra z tylko jedną aktualizację domeny.

## <a name="health-checks-during-upgrades"></a>Sprawdzanie kondycji podczas uaktualniania
W przypadku uaktualnienia zasady dotyczące kondycji mają toobe ustawić lub mogą zostać użyte wartości domyślne. Uaktualnienie jest określane jako powiodło się po uaktualnieniu wszystkich domen aktualizacji w ramach hello określić limity czasu i aktualizacji wszystkich domen zostaną uznane za dobrej kondycji.  Domeny aktualizacji w dobrej kondycji oznacza, że wszystkie sprawdzenia kondycji hello określonym w zasadach kondycji hello przekazany tej domeny aktualizacji hello. Na przykład zasadę może wprowadzić, że wszystkie usługi w ramach wystąpienia aplikacji musi być *dobrej kondycji*, jak kondycji jest definiowana za pomocą sieci szkieletowej usług.

Zasady dotyczące kondycji i kontroli podczas uaktualniania przez sieć szkieletowa usług są niezależne od usług i aplikacji. Oznacza to, że są wykonywane żadne testy specyficzne dla usługi.  Na przykład usługa może mieć wymaganie przepływności, ale usługi sieć szkieletowa nie ma hello informacji toocheck przepływności. Zobacz toohello [artykuły kondycji](service-fabric-health-introduction.md) hello kontroli, które są wykonywane. Witaj testów, które mają miejsce podczas testów uaktualniania include dla tego, czy pakiet aplikacji hello skopiowano poprawnie, czy wystąpienie hello została uruchomiona i tak dalej.

Kondycja aplikacji Hello jest agregacją jednostek podrzędnych hello aplikacji hello. Innymi słowy sieć szkieletowa usług oblicza hello kondycji aplikacji hello za pośrednictwem hello kondycji, który jest zgłaszany w aplikacji hello. Oblicza również hello kondycję wszystkich usług hello aplikacji hello w ten sposób. Dodatkowe sieci szkieletowej usług oblicza kondycję hello usług aplikacji hello agregowania kondycji hello ich elementy podrzędne, takie jak hello repliki usługi. Po spełnieniu zasady kondycji aplikacji hello hello uaktualnienia można kontynuować. Naruszenia zasad dotyczących kondycji hello uaktualniania aplikacji hello kończy się niepowodzeniem.

## <a name="upgrade-modes"></a>Tryby uaktualnienia
Tryb Hello, zalecane w przypadku uaktualniania aplikacji jest monitorowane hello tryb, w którym jest tryb hello najczęściej używanych. Tryb monitorowanych przeprowadzają jedna aktualizacja domeny uaktualnienia hello i jeśli sprawdza wszystkie dane kondycji przebiegu (na powitania zasady określone), przenosi toohello dalej domeny aktualizacji automatycznie.  Niepowodzenie sprawdzania kondycji i/lub osiągnięcia limitów czasu, uaktualnienie hello albo jest przywracana hello aktualizacji domeny, czy tryb hello jest ręczne toounmonitored zmienione. Można skonfigurować hello toochoose uaktualnienia, jeden z tych dwóch trybów uaktualnienia nie powiodło się. 

Niemonitorowane ręczny tryb wymaga ręcznej interwencji po każdym uaktualnienia w domenie aktualizacji, tookick poza uaktualniania hello na powitania dalej domeny aktualizacji. Nie sieci szkieletowej usług kondycji są sprawdzane. Hello administrator sprawdza hello kondycji lub stanu przed rozpoczęciem uaktualniania hello hello dalej domeny aktualizacji.

## <a name="upgrade-default-services"></a>Uaktualnij usługi domyślne
Podczas procesu uaktualniania hello aplikacji można uaktualnić usługi domyślnej aplikacji sieci szkieletowej usług. Domyślne usługi są zdefiniowane w hello [manifest aplikacji](service-fabric-application-model.md#describe-an-application). Standardowe reguły Hello uaktualniania usług domyślnych są następujące:

1. Domyślne usługi w nowych hello [manifest aplikacji](service-fabric-application-model.md#describe-an-application) które nie istnieją w klastrze hello są tworzone.
> [!TIP]
> [EnableDefaultServicesUpgrade](service-fabric-cluster-fabric-settings.md#fabric-settings-that-you-can-customize) potrzeb toobe określonych hello tooenable tootrue reguły. Ta funkcja jest obsługiwana w wersji 5.5.

2. Domyślne usługi istniejących w obu poprzednich [manifest aplikacji](service-fabric-application-model.md#describe-an-application) i nowej wersji zostały zaktualizowane. Opisy usług w nowej wersji hello zastąpiłaby znajdującymi się już hello klastra. Uaktualnianie aplikacji czy wycofywania automatycznie po aktualizacji awaria usługi domyślne.
3. Domyślne usługi w poprzednim hello [manifest aplikacji](service-fabric-application-model.md#describe-an-application) , ale nie w nowej wersji hello są usuwane. **Należy zwrócić uwagę, to usunięcie usług domyślnych nie można przywrócić.**

W przypadku aplikacji uaktualniania zostanie wycofana, usługi domyślne są toohello przywróconego stanu przed rozpoczęciem uaktualniania. Ale usługami usunięto nigdy nie mogą być tworzone.

## <a name="application-upgrade-flowchart"></a>Schemat blokowy uaktualniania aplikacji
Schemat blokowy Hello dalej w tym temacie pomogą zrozumieć hello procesu uaktualniania aplikacji sieci szkieletowej usług. W szczególności przepływu hello w tym artykule opisano sposób hello limity czasu, w tym *HealthCheckStableDuration*, *HealthCheckRetryTimeout*, i *UpgradeHealthCheckInterval*, kontrolować hello uaktualnienia w domenie jedna aktualizacja jest uznawany za powodzenie lub niepowodzenie.

![proces uaktualniania Hello aplikacji sieci szkieletowej usług][image]

## <a name="next-steps"></a>Następne kroki
[Uaktualnianie aplikacji za pomocą Visual Studio](service-fabric-application-upgrade-tutorial.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu Visual Studio.

[Uaktualnienie z aplikacji przy użyciu programu Powershell](service-fabric-application-upgrade-tutorial-powershell.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu PowerShell.

Kontrolowanie sposobu uaktualnienia aplikacji przy użyciu [uaktualnienia parametrów](service-fabric-application-upgrade-parameters.md).

Uzyskania uaktualnień aplikacji zgodnych przez uczenia jak toouse [szeregowanie danych](service-fabric-application-upgrade-data-serialization.md).

Dowiedz się, jak toouse zaawansowanych funkcji podczas uaktualniania aplikacji, odnosząc się zbyt[Tematy zaawansowane](service-fabric-application-upgrade-advanced.md).

Rozwiązywania typowych problemów w aplikacji uaktualnień, odnosząc się kroki toohello [Rozwiązywanie problemów z uaktualnieniami aplikacji](service-fabric-application-upgrade-troubleshooting.md).

[image]: media/service-fabric-application-upgrade/service-fabric-application-upgrade-flowchart.png
