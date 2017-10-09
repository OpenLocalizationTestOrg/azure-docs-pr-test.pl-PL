---
title: "aaaAzure usługi sieć szkieletowa autonomiczny klastra wdrożenia przygotowania | Dokumentacja firmy Microsoft"
description: "Dokumentacji związane środowiskiem hello toopreparing i tworzenia konfiguracji klastra hello toobe uznane za toodeploying wcześniejsze klastra przeznaczone do obsługi obciążeń produkcyjnych."
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
ms.openlocfilehash: e503c61a64b408af3f22bd75ab02f1c34ac9f380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
<a id="preparemachines"></a>

## <a name="plan-and-prepare-your-service-fabric-standalone-cluster-deployment"></a>Planowanie i przygotowanie wdrożenia klastra usługi sieć szkieletowa autonomiczny
Wykonaj hello przed utworzeniem klastra wykonaj następujące kroki.

### <a name="step-1-plan-your-cluster-infrastructure"></a>Krok 1: Plan infrastruktury klastra
Zamierzasz toocreate klastra sieci szkieletowej usług na komputerach, których właścicielem, możesz zdecydować, jakiego rodzaju błędów ma hello toosurvive klastra. Na przykład potrzebujesz wiersze oddzielne zasilania lub połączenia z Internetem dostarczone toothese maszyny? Ponadto należy wziąć pod uwagę hello zabezpieczenia fizyczne tych maszyn. Witaj maszyny lokalizację i który musi toothem dostępu? Po wprowadzeniu tych decyzji można logicznie mapować toohello maszyny hello różnych domen błędów (zobacz krok 4). dla klastrów produkcyjnych przy planowaniu infrastruktury Hello jest bardziej skomplikowane niż w przypadku klastrów testu.

### <a name="step-2-prepare-hello-machines-toomeet-hello-prerequisites"></a>Krok 2: Przygotowanie toomeet maszyny hello hello wymagania wstępne
Wymagania wstępne dla każdej maszyny, które mają tooadd toohello klastra:

* Zaleca się co najmniej 16 GB pamięci RAM.
* Zaleca się co najmniej 40 GB dostępnego miejsca na dysku.
* 4 rdzenie lub większa procesora CPU jest zalecane.
* Łączność tooa bezpiecznej sieci lub sieci dla wszystkich maszyn.
* Windows Server 2012 R2 lub Windows Server 2016. 
* [.NET framework 4.5.1 lub nowszej](https://www.microsoft.com/download/details.aspx?id=40773), pełnej instalacji.
* [Środowisko Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell).
* Witaj [usługi RemoteRegistry](https://technet.microsoft.com/library/cc754820) powinna być uruchomiona na wszystkich komputerach hello.

Witaj administrator klastra, wdrażanie i konfigurowanie klastra hello musi mieć [uprawnień administratora](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) na każdym hello maszyn. Usługi Service Fabric nie można zainstalować na kontrolerze domeny.

### <a name="step-3-determine-hello-initial-cluster-size"></a>Krok 3: Określanie hello rozmiar klastra
Każdy węzeł w klastrze usługi sieć szkieletowa autonomiczny ma hello sieci szkieletowej usług środowiska uruchomieniowego wdrożony i jest członkiem klastra hello. Typowe wdrożenie produkcyjne ma jeden węzeł na każde wystąpienie systemu operacyjnego (fizycznych lub wirtualnych). rozmiar klastra Hello zależy od potrzeb firmy. Jednak musi mieć rozmiar minimalny klastra trzy węzły (maszyny lub maszyn wirtualnych).
Do celów programistycznych może mieć więcej niż jeden węzeł na danym komputerze. W środowisku produkcyjnym usługi sieć szkieletowa obsługuje tylko jeden węzeł na maszynie fizycznej lub wirtualnej.

### <a name="step-4-determine-hello-number-of-fault-domains-and-upgrade-domains"></a>Krok 4: Hello liczba domen błędów i uaktualnienia domen
A *domeny błędów* (FD) jest miejscem, awarii i jest z nią bezpośrednio powiązane toohello infrastruktury fizycznej w centrach danych hello. Domeny błędów zawiera składniki sprzętowe (komputery, przełączniki sieci i więcej), które współużytkują pojedynczy punkt awarii. Nie ma mapowania między stojakami i domen błędów 1:1, ale słabo rzecz biorąc, każdy Stojak jest uznawana za domeny błędów. Rozważając hello węzłów w klastrze, zdecydowanie zaleca się czy węzły hello dzielone między co najmniej trzy domen błędów.

Po określeniu FDs w pliku ClusterConfig.json można hello nazwę każdego FD. Hierarchiczna FDs jest obsługiwana w sieci szkieletowej usług, dzięki czemu można uwzględnić w nich topologii infrastruktury.  Na przykład po FDs hello są prawidłowe:

* "faultDomain": "fd: / Komputer1-Room1/szafa1"
* "faultDomain": "fd: / FD1"
* "faultDomain": "fd: / Room1/szafa1/PDU1 znajdującego/M1"

*Domeny uaktualnienia* (UD) to jednostka logiczna węzłów. Podczas uaktualniania usługi sieć szkieletowa zorkiestrowana (uaktualnienie aplikacji lub Uaktualnianie klastra) wszystkie węzły w UD są pobierane w dół tooperform hello uaktualnienia dopóki węzłów w innych UDs pozostają dostępne tooserve żądań. Witaj aktualizacje oprogramowania, które należy wykonać na maszynach, nie uznają UDs, więc musisz je jednego komputera na raz.

Hello najprostszy sposób toothink dotyczących tych pojęć jest tooconsider FDs jako zespół hello nieplanowanych awarii i UDs hello jednostki zaplanowanej konserwacji.

Po określeniu UDs w pliku ClusterConfig.json można hello nazwę każdego UD. Na przykład następujące nazwy hello są prawidłowe:

* "upgradeDomain": "UD0"
* "upgradeDomain": "UD1A"
* "upgradeDomain": "DomainRed"
* "upgradeDomain": "Blue"

Aby uzyskać bardziej szczegółowe informacje dotyczące uaktualniania domen i domen błędów, zobacz [opisujące klastra sieci szkieletowej usług](service-fabric-cluster-resource-manager-cluster-description.md).

### <a name="step-5-download-hello-service-fabric-standalone-package-for-windows-server"></a>Krok 5: Pobierz hello sieci szkieletowej usług wersjach systemu Windows Server
[Pobierz Link - pakietu autonomicznego sieci szkieletowej usług - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) i Rozpakuj pakiet hello, albo wdrożenie tooa czyli komputera nie jest częścią klastra hello lub tooone hello maszyn, które będzie częścią klastra.

### <a name="step-6-modify-cluster-configuration"></a>Krok 6: Zmodyfikuj konfigurację klastra
toocreate klastra autonomiczny masz toocreate autonomiczny plik pliku ClusterConfig.json konfiguracji klastra, opisujący specyfikacji hello hello klastra. Można utworzyć pliku konfiguracji hello w szablonach hello znaleźć pod adresem hello poniżej łącze. <br>
[Konfiguracje klastrów autonomiczny](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

Aby uzyskać szczegółowe informacje na powitania sekcje w tym pliku, zobacz [ustawienia konfiguracji dla klastra systemu Windows autonomiczny](service-fabric-cluster-manifest.md).

Otwórz jeden z plików pliku ClusterConfig.json hello z hello pakietu, który został pobrany i zmodyfikować hello następujące ustawienia:
| **Ustawienie konfiguracji** | **Opis** |
| --- | --- |
| **Elementów NodeType** |Typy węzłów pozwala tooseparate węzły klastra w różnych grupach. Klaster musi mieć co najmniej jeden typ NodeType. Wszystkie węzły w grupie mają następujące cechy wspólne hello: <br> **Nazwa** -to jest nazwa typu węzła hello. <br>**Porty punktów końcowych** — te są nazywane różnych punktów końcowych (porty), które są skojarzone z tym typem węzła. Można użyć dowolnego numeru portu, mają tak długo, jak nie powodują konfliktów z już niczego więcej w tym manifeście i nie są już używane przez inne aplikacji uruchomionych na maszynie hello/maszyny Wirtualnej. <br> **Właściwości umieszczania** -opisano te właściwości dla tego typu węzła używanej jako ograniczenia umieszczania usług systemowych hello lub usługi. Te właściwości są pary klucz wartość zdefiniowana przez użytkownika, które zapewniają dodatkowe metadane dla danego węzła. Przykłady właściwości węzła byłoby, czy węzeł hello ma dysk twardy lub karty graficznej, hello liczba jednostek w jego dysk twardy, rdzeni i inne właściwości fizyczne. <br> **Możliwości** -możliwości węzła Zdefiniuj nazwę hello i ilość określonego zasobu określonego węzła i dysponuje zużycia. Na przykład węzeł mogą określić, czy ma ona wydajności dla metryki o nazwie "MemoryInMb" i ma 2048 MB pamięci, które są dostępne, domyślnie. Te możliwości są używane w tooensure środowiska uruchomieniowego, że usługi, które wymagają określonej ilości zasobów są umieszczane w węzłach hello czy tych zasobów, które są dostępne w hello wymagać kwoty.<br>**IsPrimary** — Jeśli masz więcej niż jeden NodeType zdefiniowane upewnij się, czy jest tylko jedna wartość tooprimary z wartością hello *true*, czyli gdzie hello system usług uruchomienia. Wszystkie inne typy węzła powinna być ustawiona wartość toohello *false* |
| **Węzły** |Są to hello szczegółów dla każdego z węzłów hello, które są częścią klastra hello (typ węzła, nazwa węzła IP adres, domena awarii i domeny uaktualnień hello węzła). Hello maszyny, które mają toobe klastra hello utworzone na potrzeby toobe wymienione w tym miejscu przy użyciu ich adresów IP. <br> Jeśli używasz hello utworzenia tego samego adresu IP dla wszystkich węzłów hello, a następnie klastra jednego pola, które służy do celów testowych. Nie należy używać jednego pola klastrów wdrażania obciążeń produkcyjnych. |

Po konfiguracji klastra hello miał wszystkie skonfigurowane ustawienia toohello środowisku, można testowana hello środowiska klastra (krok 7).

<a id="environmentsetup"></a>

### <a name="step-7-environment-setup"></a>Krok 7. Konfiguracja środowiska

Administrator klastra konfiguruje klaster sieci szkieletowej usług autonomiczny, środowiska hello jest wymaga toobe z hello następujące kryteria: <br>
1. Użytkownik Hello tworzenie hello klastra powinien mieć maszyny tooall uprawnienia zabezpieczeń na poziomie administratora, które są wyświetlane jako węzły w pliku konfiguracji klastra hello.
2. Komputer, z których hello tworzenia klastra, a także każdego komputera węzła klastra musi:
* Odinstalowano zestawu SDK sieci szkieletowej usług
* Ma środowisko uruchomieniowe usługi sieć szkieletowa odinstalowane 
* Witaj usługa Zapora systemu Windows (mpssvc) włączono
* Czy włączono hello usługa Rejestr zdalny (remoteregistry)
* Plik włączona udostępniania (SMB)
* Ma niezbędne porty otwarty, na podstawie portów konfiguracji klastra
* Mieć niezbędne porty otworzyć usługi systemu Windows protokołu SMB i Rejestr zdalny: 135, 137 138, 139 i 445
* Ma tooone łączności sieciowej innego
3. Brak maszyn węzła klastra hello powinien być kontrolerem domeny.
4. Toobe klastra hello wdrożone w przypadku klastra bezpieczny, sprawdzanie poprawności hello zabezpieczeń niezbędne wymagania wstępne zostały umieścić i są poprawnie skonfigurowane przed hello konfiguracji.
5. Jeśli hello klastra maszyny nie są dostępne z Internetu, ustaw następujące hello w hello klastra konfiguracji:
* Wyłączanie telemetrii: w obszarze *właściwości* ustawić *"enableTelemetry": wartość false*
* Wyłącz automatyczne pobieranie wersji sieci szkieletowej & bieżącej wersji klastra tego hello zbliża się koniec obsługi powiadomień: w obszarze *właściwości* ustawić *"fabricClusterAutoupgradeEnabled": wartość false*
* Możesz też jeśli dostęp do Internetu w sieci jest ograniczona wymienione toowhite domen, hello domen poniżej są wymagane do automatycznego uaktualniania: witrynie download.microsoft.com go.microsoft.com

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
Witaj skryptu TestConfiguration.ps1 znajdują się w hello autonomicznych pakietu. Jest używany jako toovalidate Analizator najlepszych rozwiązań część kryteriów hello powyżej i powinny być używane jako toovalidate wyboru związane z poprawnością, czy klaster może zostać wdrożony w danym środowisku. W przypadku niezgodności, można znaleźć listy toohello w obszarze [konfigurowania środowiska](service-fabric-cluster-standalone-deployment-preparation.md) do rozwiązywania problemów. 

Ten skrypt można uruchomić na dowolnym komputerze, że administrator dostępu tooall hello maszyny, które są wyświetlane jako węzły w pliku konfiguracji klastra hello. Ten skrypt jest uruchamiany na maszynie Hello nie ma toobe częścią klastra hello.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
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

Obecnie ten moduł testowania konfiguracji nie można zweryfikować konfiguracji zabezpieczeń hello, to ma toobe wykonywane niezależnie.  

> [!NOTE]
> Będziemy stale wprowadzać ulepszenia toomake ten moduł bardziej niezawodne, więc jeśli jest uszkodzony lub brak liter, co sądzisz nie jest aktualnie przechwycony przez TestConfiguration, prosimy o kontakt za pośrednictwem naszego [kanały obsługuje](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).   
> 
> 

## <a name="next-steps"></a>Następne kroki
* [Tworzenie autonomicznych klastra w systemie Windows Server](service-fabric-cluster-creation-for-windows-server.md)
