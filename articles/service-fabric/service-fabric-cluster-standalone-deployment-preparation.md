---
title: "Przygotowanie wdrażania autonomicznej klastra sieci szkieletowej usługi Azure | Dokumentacja firmy Microsoft"
description: "Dokumentację dotyczącą przygotowania środowiska i Tworzenie konfiguracji klastra, należy wziąć pod uwagę przed wdrożeniem klastra przeznaczone do obsługi obciążeń produkcyjnych."
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 1/17/2017
ms.author: maburlik;chackdan
ms.openlocfilehash: f332193f9a53260173a1010b8bf9f08726bea427
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
<a id="preparemachines"></a>

## <a name="plan-and-prepare-your-service-fabric-standalone-cluster-deployment"></a>Planowanie i przygotowanie wdrożenia klastra usługi sieć szkieletowa autonomiczny
Przed utworzeniem klastra, wykonaj następujące kroki.

### <a name="step-1-plan-your-cluster-infrastructure"></a>Krok 1: Plan infrastruktury klastra
Zamierzasz utworzyć klaster sieci szkieletowej usług na maszynach, którego jesteś właścicielem, można zdecydować, jakiego rodzaju błędów ma klaster na przetrwanie. Na przykład czy potrzebujesz oddzielnych, linie zasilania lub połączenia z Internetem dostarczane na tych komputerach? Ponadto należy wziąć pod uwagę zabezpieczenia fizyczne tych komputerów. Gdy wszystkie maszyny znajdują się i który musi mieć dostęp do nich? Po wprowadzeniu tych decyzji logicznie można mapować maszyny do różnych domen błędów (zobacz krok 4). Dla klastrów produkcyjnych przy planowaniu infrastruktury jest bardziej skomplikowane niż w przypadku klastrów testu.

### <a name="step-2-prepare-the-machines-to-meet-the-prerequisites"></a>Krok 2: Przygotowanie maszyny, aby spełnić wymagania wstępne
Wymagania wstępne dla każdego komputera, który ma zostać dodany do klastra:

* Zaleca się co najmniej 16 GB pamięci RAM.
* Zaleca się co najmniej 40 GB dostępnego miejsca na dysku.
* 4 rdzenie lub większa procesora CPU jest zalecane.
* Łączność z bezpiecznej sieci lub sieci dla wszystkich maszyn.
* Windows Server 2012 R2 lub Windows Server 2016. 
* [.NET framework 4.5.1 lub nowszej](https://www.microsoft.com/download/details.aspx?id=40773), pełnej instalacji.
* [Środowisko Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell).
* [Usługi RemoteRegistry](https://technet.microsoft.com/library/cc754820) powinna być uruchomiona na wszystkich komputerach.

Administrator klastra, wdrażanie i konfigurowanie klastra musi mieć [uprawnień administratora](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) na każdym z tych maszyn. Usługi Service Fabric nie można zainstalować na kontrolerze domeny.

### <a name="step-3-determine-the-initial-cluster-size"></a>Krok 3: Określanie rozmiaru klastra
Każdy węzeł w klastrze usługi sieć szkieletowa autonomiczny ma sieci szkieletowej usług środowiska uruchomieniowego wdrożony i jest członkiem klastra. Typowe wdrożenie produkcyjne ma jeden węzeł na każde wystąpienie systemu operacyjnego (fizycznych lub wirtualnych). Rozmiar klastra zależy od potrzeb firmy. Jednak musi mieć rozmiar minimalny klastra trzy węzły (maszyny lub maszyn wirtualnych).
Do celów programistycznych może mieć więcej niż jeden węzeł na danym komputerze. W środowisku produkcyjnym usługi sieć szkieletowa obsługuje tylko jeden węzeł na maszynie fizycznej lub wirtualnej.

### <a name="step-4-determine-the-number-of-fault-domains-and-upgrade-domains"></a>Krok 4: Określenie liczby domen błędów i uaktualnienia domen
A *domeny błędów* (FD) jest miejscem, awarii i jest bezpośrednio powiązana z infrastruktury fizycznej w centrach danych. Domeny błędów zawiera składniki sprzętowe (komputery, przełączniki sieci i więcej), które współużytkują pojedynczy punkt awarii. Nie ma mapowania między stojakami i domen błędów 1:1, ale słabo rzecz biorąc, każdy Stojak jest uznawana za domeny błędów. Rozważając węzłów w klastrze, zdecydowanie zaleca się czy węzły dzielone między co najmniej trzy domen błędów.

Po określeniu FDs w pliku ClusterConfig.json, można wybrać nazwę dla każdego FD. Hierarchiczna FDs jest obsługiwana w sieci szkieletowej usług, dzięki czemu można uwzględnić w nich topologii infrastruktury.  Na przykład następujące FDs są prawidłowe:

* "faultDomain": "fd: / Komputer1-Room1/szafa1"
* "faultDomain": "fd: / FD1"
* "faultDomain": "fd: / Room1/szafa1/PDU1 znajdującego/M1"

*Domeny uaktualnienia* (UD) to jednostka logiczna węzłów. Podczas uaktualniania usługi sieć szkieletowa zorkiestrowana (uaktualnienie aplikacji lub Uaktualnianie klastra) wszystkie węzły w UD podjęto w dół do uaktualnienia, podczas gdy węzłów w innych UDs pozostają dostępne do obsługi żądań. Aktualizacje oprogramowania, należy wykonać na maszynach, nie uznają UDs, więc musisz je jednego komputera na raz.

Najprostszym sposobem, aby traktować te pojęcia jest należy wziąć pod uwagę FDs jednostką nieplanowanych awarii i UDs jednostką zaplanowanej konserwacji.

Po określeniu UDs w pliku ClusterConfig.json, można wybrać nazwę dla każdego UD. Na przykład następujące nazwy są prawidłowe:

* "upgradeDomain": "UD0"
* "upgradeDomain": "UD1A"
* "upgradeDomain": "DomainRed"
* "upgradeDomain": "Blue"

Aby uzyskać bardziej szczegółowe informacje dotyczące uaktualniania domen i domen błędów, zobacz [opisujące klastra sieci szkieletowej usług](service-fabric-cluster-resource-manager-cluster-description.md).

### <a name="step-5-download-the-service-fabric-standalone-package-for-windows-server"></a>Krok 5: Pobierz pakiet autonomicznej usługi sieć szkieletowa usług dla systemu Windows Server
[Pobierz Link - pakietu autonomicznego sieci szkieletowej usług - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) i Rozpakuj pakiet do wdrożenia maszyny, która nie jest częścią klastra lub do jednego z komputerów, które będzie częścią klastra.

### <a name="step-6-modify-cluster-configuration"></a>Krok 6: Zmodyfikuj konfigurację klastra
Aby utworzyć klaster autonomicznego należy utworzyć autonomiczny plik pliku ClusterConfig.json konfiguracji klastra, opisujący specyfikacji klastra. Można utworzyć pliku konfiguracji na tych szablonach znaleziono w linku poniżej. <br>
[Konfiguracje klastrów autonomiczny](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

Aby uzyskać więcej informacji na sekcje w tym pliku, zobacz [ustawienia konfiguracji dla klastra systemu Windows autonomiczny](service-fabric-cluster-manifest.md).

Otwórz jeden z plików w pliku ClusterConfig.json z pakietu, który został pobrany i zmodyfikować następujące ustawienia:
| **Ustawienie konfiguracji** | **Opis** |
| --- | --- |
| **Elementów NodeType** |Typy węzłów umożliwiają oddzielenie węzły klastra w różnych grupach. Klaster musi mieć co najmniej jeden typ NodeType. Wszystkie węzły w grupie mają następujące cechy wspólne: <br> **Nazwa** -to jest nazwa typu węzła. <br>**Porty punktów końcowych** — te są nazywane różnych punktów końcowych (porty), które są skojarzone z tym typem węzła. Można użyć dowolnego numeru portu, mają tak długo, jak nie powodują konfliktów z już niczego więcej w tym manifeście i nie są już używane przez inne aplikacji uruchomionych na komputerze/maszyny Wirtualnej. <br> **Właściwości umieszczania** -opisano te właściwości dla tego typu węzła używanej jako ograniczenia umieszczania usług systemowych lub usługi. Te właściwości są pary klucz wartość zdefiniowana przez użytkownika, które zapewniają dodatkowe metadane dla danego węzła. Przykłady właściwości węzła byłoby, czy węzeł ma dysk twardy lub karty graficznej, liczba jednostek w jego dysk twardy, rdzeni i inne właściwości fizyczne. <br> **Możliwości** -możliwości węzła zdefiniować nazwę i ilość określonego zasobu określonego węzła i dysponuje zużycia. Na przykład węzeł mogą określić, czy ma ona wydajności dla metryki o nazwie "MemoryInMb" i ma 2048 MB pamięci, które są dostępne, domyślnie. Te możliwości są używane w czasie wykonywania, aby upewnić się, że usługi, które wymagają określonej ilości zasobów są umieszczane w węzłach, które mają te zasoby dostępne w ilości wymagane.<br>**IsPrimary** — Jeśli masz więcej niż jeden typ NodeType zdefiniowane upewnij się, że jest tylko jedna wartość do podstawowej z wartością *true*, czyli gdzie system usługi uruchomienia. Wszystkie inne typy węzeł powinien być ustawiony na wartość *false* |
| **Węzły** |Są to szczegółowe informacje dla każdego z węzłów, które są częścią klastra (typ węzła, nazwa węzła, adres IP, domena awarii i domeny uaktualnień węzła). Maszyny ma klaster ma zostać utworzony na potrzeby wyświetlane w tym miejscu przy użyciu ich adresów IP. <br> Jeśli używasz tego samego adresu IP dla wszystkich węzłów klastra jednego pola tworzona jest, które służy do celów testowych. Nie należy używać jednego pola klastrów wdrażania obciążeń produkcyjnych. |

Po konfiguracji klastra ma wszystkie ustawienia skonfigurowane w środowisku, można testowana środowiska klastra (krok 7).

<a id="environmentsetup"></a>

### <a name="step-7-environment-setup"></a>Krok 7. Konfiguracja środowiska

Gdy administrator klastrów konfiguruje klaster sieci szkieletowej usług autonomiczny, środowisko jest konieczność można skonfigurować przy użyciu następujących kryteriów: <br>
1. Użytkownik tworzący klaster ma uprawnienia zabezpieczeń na poziomie administratora do wszystkich komputerów, które są wyświetlane jako węzły w pliku konfiguracji klastra.
2. Komputer, z którego jest tworzony klaster, a także każdego komputera węzła klastra musi:
* Odinstalowano zestawu SDK sieci szkieletowej usług
* Ma środowisko uruchomieniowe usługi sieć szkieletowa odinstalowane 
* Czy włączono usługi Zapora systemu Windows (mpssvc)
* Czy włączono usługi Rejestr zdalny (remoteregistry)
* Plik włączona udostępniania (SMB)
* Ma niezbędne porty otwarty, na podstawie portów konfiguracji klastra
* Mieć niezbędne porty otworzyć usługi systemu Windows protokołu SMB i Rejestr zdalny: 135, 137 138, 139 i 445
* Połączenie z siecią między nimi
3. Brak maszyn węzeł klastra powinien być kontrolerem domeny.
4. Jeśli można wdrożyć klaster jest klastrem bezpieczny, sprawdź niezbędne wymagania wstępne zostały umieścić i są poprawnie skonfigurowane dla konfiguracji zabezpieczeń.
5. Jeśli maszyn klastra nie są dostępne z Internetu, należy ustawić następującą w konfiguracji klastra:
* Wyłączanie telemetrii: w obszarze *właściwości* ustawić *"enableTelemetry": wartość false*
* Wyłącz automatyczne pobieranie wersji sieci szkieletowej & powiadomienia, że bieżąca wersja klastra zbliża się koniec obsługi: w obszarze *właściwości* ustawić *"fabricClusterAutoupgradeEnabled": wartość false*
* Można również dostęp do Internetu w sieci jest ograniczona do domeny wymienione białe, poniżej domeny są wymagane do automatycznego uaktualniania: witrynie download.microsoft.com go.microsoft.com

6. Ustaw odpowiednie sieci szkieletowej usług wyłączenia oprogramowania antywirusowego:

| **Katalogi wykluczone antywirusowe** |
| --- |
| Program Files\Microsoft usługi sieć szkieletowa |
| Zmiennej FabricDataRoot (z konfiguracji klastra) |
| Lokalizacji FabricLogRoot (z konfiguracji klastra) |

| **Procesy wykluczone antywirusowe** |
| --- |
| Fabric.exe |
| FabricHost.exe |
| FabricInstallerService.exe |
| FabricSetup.exe |
| FabricDeployer.exe |
| ImageBuilder.exe |
| FabricGateway.exe |
| FabricDCA.exe |
| FabricFAS.exe |
| FabricUOS.exe |
| FabricRM.exe |
| FileStoreService.exe |

### <a name="step-8-validate-environment-using-testconfiguration-script"></a>Krok 8. Sprawdź poprawność środowiska przy użyciu skryptu TestConfiguration
Skrypt TestConfiguration.ps1 można znaleźć w pakiecie autonomicznych. Jest używane jako Best Practices Analyzer można sprawdzić poprawności część kryteriów powyżej i do sprawdzania, czy klaster może zostać wdrożony w danym środowisku można użyć w celu sprawdzenia związane z poprawnością. W przypadku niezgodności, można znaleźć na liście w obszarze [konfigurowania środowiska](service-fabric-cluster-standalone-deployment-preparation.md) do rozwiązywania problemów. 

Ten skrypt można uruchomić na dowolnym komputerze, który ma dostęp administratora do wszystkich komputerów, które są wyświetlane jako węzły w pliku konfiguracji klastra. Ten skrypt uruchamiany na komputerze nie ma być częścią klastra.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
Trace folder already exists. Traces will be written to existing trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
Running Best Practices Analyzer...
Best Practices Analyzer completed successfully.


LocalAdminPrivilege        : True
IsJsonValid                : True
IsCabValid                 : True
RequiredPortsOpen          : True
RemoteRegistryAvailable    : True
FirewallAvailable          : True
RpcCheckPassed             : True
NoConflictingInstallations : True
FabricInstallable          : True
Passed                     : True
```

Obecnie ten moduł testowania konfiguracji nie można zweryfikować konfiguracji zabezpieczeń, to ma odbywać się niezależnie.  

> [!NOTE]
> Firma Microsoft stale wprowadzać ulepszenia wprowadzić bardziej niezawodne, ten moduł, jeśli wystąpi niezgodność uszkodzone lub brakujące który Twoim zdaniem nie jest aktualnie przechwycony przez TestConfiguration, prosimy o kontakt za pośrednictwem naszego [kanały obsługuje](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).   
> 
> 

## <a name="next-steps"></a>Następne kroki
* [Tworzenie autonomicznych klastra w systemie Windows Server](service-fabric-cluster-creation-for-windows-server.md)
