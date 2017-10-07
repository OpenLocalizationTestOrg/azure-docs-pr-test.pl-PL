---
title: aaaAdvanced tematy uaktualniania aplikacji | Dokumentacja firmy Microsoft
description: "W tym artykule omówiono niektóre tematy zaawansowane dotyczące tooupgrading aplikacji sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a>Uaktualnianie aplikacji usługi Service Fabric: Tematy zaawansowane
## <a name="adding-or-removing-services-during-an-application-upgrade"></a>Dodawanie lub usuwanie usługi podczas uaktualniania aplikacji
Jeśli nowa usługa zostanie dodany tooan aplikacji, która jest już wdrożony i opublikowane jako uaktualnienie, hello nowej usługi jest dodany toohello wdrożonych aplikacji.  Takie uaktualnienia nie wpływa na powitania usług, które były częścią aplikacji hello. Jednak wystąpienia usługi hello, która została dodana musi być uruchomiona hello nowej usługi toobe active (przy użyciu hello `New-ServiceFabricService` polecenia cmdlet).

Usługi może zostać także usunięty z aplikacji w ramach uaktualnienia. Jednak wszystkie bieżącego wystąpienia usługi usunięte być do hello musi zostać zatrzymana przed kontynuacją uaktualniania hello (przy użyciu hello `Remove-ServiceFabricService` polecenia cmdlet).

## <a name="manual-upgrade-mode"></a>Ręczny tryb uaktualniania
> [!NOTE]
> należy rozważyć Hello niemonitorowane ręczny tryb tylko w przypadku uaktualniania nie powiodło się lub został wstrzymany. Tryb monitorowanych Hello jest hello zalecane tryb uaktualniania aplikacji sieci szkieletowej usług.
>
>

Azure Service Fabric zawiera wielu trybów uaktualnienia klastrów toosupport rozwoju i produkcji. Wybrane opcje wdrażania może się różnić w różnych środowiskach.

uaktualnienie stopniowe aplikacji Hello monitorowane jest hello najczęstszych toouse uaktualnienia w środowisku produkcyjnym hello. Podczas uaktualniania hello określić zasady, zapewnia sieć szkieletowa usług aplikacji hello jest dobrej kondycji, aby mogła być kontynuowana hello uaktualnienia.

 administrator aplikacji Hello służy hello ręczne wprowadzanie aplikacji tryb uaktualniania toohave całkowitą kontrolę nad hello postęp uaktualnienia za pośrednictwem hello różnych domen uaktualnienia. Ten tryb jest przydatne, gdy wymagane są zasady oceny kondycji dostosowane lub złożonych lub wykonywane jest uaktualnienie nietypowe (na przykład aplikacja hello jest już utraty danych).

Na koniec hello automatycznego uaktualnienia stopniowego aplikacji przydaje się do rozwoju lub testowania tooprovide środowisk cykl iteracji szybkiego podczas tworzenia usługi.

## <a name="change-toomanual-upgrade-mode"></a>Zmień tryb uaktualniania toomanual
**Ręczne**— uaktualnienie aplikacji hello Stop w hello bieżącego hello UD i zmień uaktualnienia tooUnmonitored tryb ręczny. Witaj administrator musi wywołania toomanually **MoveNextApplicationUpgradeDomainAsync** tooproceed z hello wyzwalacza wycofanie inicjując nowego uaktualnienia lub uaktualnienia. Po uaktualnieniu hello wejścia ręczny tryb hello, pozostaje w trybie ręcznym hello do momentu zainicjowania nowego uaktualnienia. Witaj **GetApplicationUpgradeProgressAsync** polecenie zwraca sieci SZKIELETOWEJ\_aplikacji\_uaktualnienia\_stanu\_STOPNIOWYCH\_do przodu\_OCZEKUJE.

## <a name="upgrade-with-a-diff-package"></a>Uaktualnienie z pakietem różnicowego
Można uaktualnić aplikacji usługi Service Fabric przy inicjowania obsługi administracyjnej z pakietem aplikacji pełne, niezależne. Aplikację można również uaktualnić przy użyciu pakietu różnicowego, który zawiera tylko pliki aplikacji hello zaktualizowane, hello zaktualizowane manifest aplikacji i pliki manifestu usługi hello.

Pakiet aplikacji pełne zawiera wszystkie toostart niezbędne pliki hello i uruchomienia aplikacji sieci szkieletowej usług. Pakiet różnicowego zawiera hello tylko te pliki, które w klientach hello ostatniego udostępniania i uaktualniania bieżące hello oraz manifest pełnej aplikacji hello i usługa hello pliki manifestu. Wszystkie odwołania w manifeście aplikacji hello lub manifestu usługi, której nie można znaleźć w układzie kompilacji hello jest wyszukiwany w hello magazynu obrazów.

Pakiety aplikacji pełne są wymagane dla pierwszej instalacji klastra toohello aplikacji hello. Kolejne aktualizacje mogą być pakiet pełnej aplikacji lub pakietu różnic.

Sytuacji, gdy przy użyciu pakietu różnicowego dobrym wyborem będzie:

* Pakiet różnicowego jest preferowane w przypadku pakietu dużej aplikacji, który odwołuje się wiele plików manifestu usługi i/lub kilka pakietów kodu, pakiety konfiguracji lub pakietów danych.
* Pakiet różnicowego jest preferowane w przypadku systemu wdrożenia, w którym generuje układu kompilacji hello bezpośrednio w procesie kompilacji aplikacji. W takim przypadku mimo że nie zmieniła się hello kodu, nowo zbudowany zestawy uzyskać różne sumy kontrolnej. Przy użyciu pakietu pełnej aplikacji wymaga możesz tooupdate hello wersji na wszystkie pakiety kodu. Przy użyciu pakietu różnicowego, tylko podanie hello zmienione pliki oraz pliki manifestu hello, gdzie hello wersja została zmieniona.

Po uaktualnieniu aplikacji przy użyciu programu Visual Studio, hello różnicowego pakietu jest automatycznie publikowany. toocreate pakietu różnicowego ręcznie, hello manifest aplikacji i hello usługi manifesty muszą zostać zaktualizowane, ale tylko pakietów hello zmienione powinny być uwzględnione w pakiet końcowego aplikacji hello.

Na przykład Zacznijmy powitania po aplikacji (dostępne w celu ułatwienia zrozumienia numery wersji):

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

Teraz załóżmy, że żądana tooupdate tylko hello pakietu kodu z service1 przy użyciu pakietu różnicowego przy użyciu programu PowerShell. Zaktualizowano aplikacji ma teraz, hello następujące struktury folderów:

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

W takim przypadku należy zaktualizować too2.0.0 manifestu aplikacji hello i hello manifestu usługi service1 tooreflect hello kod pakietu aktualizacji. folder Hello pakietu aplikacji musi hello następujące struktury:

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a>Następne kroki
[Uaktualnianie aplikacji za pomocą Visual Studio](service-fabric-application-upgrade-tutorial.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu Visual Studio.

[Uaktualnienie z aplikacji przy użyciu programu Powershell](service-fabric-application-upgrade-tutorial-powershell.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu PowerShell.

Kontrolowanie sposobu uaktualnienia aplikacji przy użyciu [uaktualnienia parametrów](service-fabric-application-upgrade-parameters.md).

Uzyskania uaktualnień aplikacji zgodnych przez uczenia jak toouse [szeregowanie danych](service-fabric-application-upgrade-data-serialization.md).

Rozwiązywania typowych problemów w aplikacji uaktualnień, odnosząc się kroki toohello [Rozwiązywanie problemów z uaktualnieniami aplikacji](service-fabric-application-upgrade-troubleshooting.md).
