---
title: "aaaCreate autonomicznej klastra sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie klastra usługi sieć szkieletowa usług Azure na dowolnym komputerze (fizycznych lub wirtualnych) systemem Windows Server, czy jest lokalnie lub w dowolnym chmury."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a>Tworzenie autonomicznych klastra w systemie Windows Server
Za pomocą usługi Azure Service Fabric toocreate sieci szkieletowej usług klastrów na dowolnym maszyn wirtualnych lub komputerach z systemem Windows Server. Oznacza to, można wdrażać i uruchamianie aplikacji platformy Service Fabric w dowolnym środowisku, które zawiera zestaw połączonych komputerów z systemem Windows Server, lokalnie i z każdego dostawcy chmury. Sieć szkieletowa usług zawiera pakiet Windows Server autonomiczny hello o nazwie toocreate pakiet Instalatora, które klastrów sieci szkieletowej usług.

W tym artykule przedstawiono kroki hello tworzenia klastra usługi sieć szkieletowa autonomicznych.

> [!NOTE]
> Ten pakiet Windows Server autonomiczny jest dostępnych na rynku, może być używany we wdrożeniach produkcyjnych. Ten pakiet może zawierać nowe funkcje sieci szkieletowej usług, które znajdują się w "W wersji zapoznawczej". Przewiń w dół za"[Podgląd funkcje zawarte w tym pakiecie](#previewfeatures_anchor)." sekcja listy hello hello funkcje w wersji zapoznawczej. Możesz [Pobierz kopię hello umowy licencyjnej](http://go.microsoft.com/fwlink/?LinkID=733084) teraz.
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a>Uzyskaj pomoc dotyczącą hello pakietu sieci szkieletowej usług dla systemu Windows Server
* Zapytaj społeczności hello o pakiet autonomiczny hello sieci szkieletowej usług dla systemu Windows Server w hello [forum usługi Azure Service Fabric](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).
* Otwórz bilet dla [Professional obsługę sieci szkieletowej usług](http://support.microsoft.com/oas/default.aspx?prid=16146).  Dowiedz się więcej na temat pomocy technicznej Professional firmy Microsoft [tutaj](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).
* Można również uzyskać pomoc techniczną dla tego pakietu, jako część [pomocy technicznej Microsoft Premier](https://support.microsoft.com/en-us/premier).
* Aby uzyskać więcej informacji, zobacz [opcje pomocy technicznej usługi Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).
* Dzienniki toocollect na potrzeby obsługi Uruchom hello [logowania do usługi sieci szkieletowej autonomiczny moduł zbierający](service-fabric-cluster-standalone-package-contents.md).

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a>Pobierz pakiet sieci szkieletowej usług dla systemu Windows Server hello
toocreate hello klastra, użyj pakietu sieci szkieletowej usług dla systemu Windows Server hello (Windows Server 2012 R2 i nowszych) znaleźć tutaj: <br>
[Pobierz Link - pakietu autonomicznego sieci szkieletowej usług - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)

Znajduje szczegóły na zawartość pakietu hello [tutaj](service-fabric-cluster-standalone-package-contents.md).

Pakiet środowiska uruchomieniowego platformy Service Fabric Hello jest automatycznie pobierana podczas tworzenia klastra. Jeśli wdrażania na komputerze nie podłączony toohello Internetu, Pobierz pakiet środowiska uruchomieniowego hello poza pasmem w tym miejscu: <br>
[Pobierz łącze — środowisko uruchomieniowe usługi sieć szkieletowa - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)

Szukaj przykładowych autonomicznej konfiguracji klastra na: <br>
[Przykłady konfiguracji autonomicznej klastra](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a>Tworzenie klastra hello
Sieć szkieletowa usług może być klastrem programowanie jednej maszyny tooa wdrożone za pomocą hello *ClusterConfig.Unsecure.DevCluster.json* zawarte w pliku [przykłady](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

Rozpakuj hello autonomicznych pakietu tooyour maszyny, kopiowania hello przykładowej konfiguracji pliku toohello komputera lokalnego, a następnie uruchom hello *CreateServiceFabricCluster.ps1* skryptu za pomocą sesji programu PowerShell administratora z autonomicznego hello folder pakietu:
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a>Krok 1A: tworzenie niezabezpieczona lokalnego klastra projektowego
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

Zobacz hello sekcji konfigurowania środowiska w [planowanie i przygotowanie wdrożenia klastra](service-fabric-cluster-standalone-deployment-preparation.md) dla szczegóły dotyczące rozwiązywania problemów.

Zakończeniu uruchomionych scenariusze programowania, można usunąć klastra sieci szkieletowej usług hello z hello maszyny, odwołując się toosteps w sekcji "[usunąć klaster](#removecluster_anchor)". 

### <a name="step-1b-create-a-multi-machine-cluster"></a>Krok 1B: tworzenie obsługi wielu komputerów klastra
Po przejściu hello planowania, szczegółowe kroki przygotowania na powitania poniżej łącza, gotowe toocreate klastra produkcyjnego przy użyciu pliku konfiguracji klastra. <br>
[Planowanie i przygotowanie wdrożenia klastra](service-fabric-cluster-standalone-deployment-preparation.md)

1. Sprawdzanie poprawności pliku konfiguracji hello zostały zapisane, uruchamiając hello *TestConfiguration.ps1* skryptu z folderu pakietu autonomicznego hello:  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    Powinny pojawić się dane wyjściowe, takich jak poniżej. Jeśli pole dolnej hello "Zakończony pomyślnie", jest zwracana jako "True", związane z poprawnością sprawdzenie powiodło się i hello klastra wygląda toobe do wdrożenia na podstawie konfiguracji wejściowych hello.

    ```
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

2. Tworzenie klastra hello: Uruchom hello *CreateServiceFabricCluster.ps1* klastra sieci szkieletowej usług hello toodeploy skrypt na każdej maszynie w konfiguracji hello. 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> Wdrożenie śledzenia są zapisywane toohello maszyny Wirtualnej/maszyny, na których uruchomiono skrypt programu PowerShell CreateServiceFabricCluster.ps1 hello. Te znajdują się w podfolderze hello DeploymentTraces, na podstawie w katalogu hello, z których hello uruchomienia skryptu. toosee, jeśli sieć szkieletowa usług został poprawnie wdrożony tooa maszyny, Znajdź hello zainstalowane pliki w katalogu zmiennej FabricDataRoot hello, zgodnie z opisem w pliku konfiguracji klastra hello sekcji FabricSettings (c:\ProgramData\SF domyślną). Jak również procesy FabricHost.exe i Fabric.exe są widoczne w Menedżerze zadań.
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a>Krok 1C: Tworzenie klastra w trybie offline (odłączony od Internetu)
Pakiet środowiska uruchomieniowego platformy Service Fabric Hello jest automatycznie pobierana podczas tworzenia klastra. Gdy wdrażanie toomachines klastra nie podłączone toohello internet, trzeba będzie hello toodownload sieci szkieletowej usług środowisko uruchomieniowe pakietu oddzielnie i podaj hello tooit ścieżki, podczas tworzenia klastra.
Witaj środowisko uruchomieniowe pakietu można pobrać oddzielnie, z innego komputera podłączony toohello internet, w [łącze Pobierz — środowisko uruchomieniowe usługi sieć szkieletowa - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354). Skopiuj hello środowisko uruchomieniowe pakietu toowhere wdrażasz hello klastra w trybie offline z i utworzyć klaster hello uruchamiając `CreateServiceFabricCluster.ps1` z hello `-FabricRuntimePackagePath` parametru, jak pokazano poniżej: 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
gdzie `.\ClusterConfig.json` i `.\MicrosoftAzureServiceFabric.cab` są odpowiednio hello ścieżki toohello konfiguracji klastra i pliku cab hello środowiska wykonawczego.


### <a name="step-2-connect-toohello-cluster"></a>Krok 2: Łączenie toohello klastra
tooconnect tooa bezpiecznego klastra, zobacz [sieci szkieletowej usług połączenia klastra toosecure](service-fabric-connect-to-secure-cluster.md).

tooconnect tooan niezabezpieczone klastra, uruchom następujące polecenia programu PowerShell hello:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
Przykład:
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a>Krok 3: Wywołaj okno Eksploratora usługi sieć szkieletowa
Teraz możesz połączyć toohello klastra z Eksploratora usługi sieć szkieletowa albo bezpośrednio z maszyn hello http://localhost:19080/Explorer/index.html lub zdalnie http://<*IPAddressofaMachine*>: 19080 / Explorer/index.HTML.

## <a name="add-and-remove-nodes"></a>Dodawanie i usuwanie węzłów
Można dodać lub usunąć klastra sieci szkieletowej usług autonomiczny tooyour węzłów, ponieważ zmieniających się potrzeb firmy. Zobacz [dodać lub usunąć klaster autonomicznej usługi Service Fabric tooa węzłów](service-fabric-cluster-windows-server-add-remove-nodes.md) szczegółowy opis kroków.

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a>Usuwanie klastra
tooremove klastra, uruchom hello *RemoveServiceFabricCluster.ps1* skrypt programu PowerShell z folderu pakietu hello i przekazać w pliku konfiguracji JSON hello ścieżki toohello. Opcjonalnie można określić lokalizację dziennika hello hello usuwania.

Ten skrypt można uruchomić na dowolnym komputerze, że administrator dostępu tooall hello maszyny, które są wyświetlane jako węzły w pliku konfiguracji klastra hello. Ten skrypt jest uruchamiany na maszynie Hello nie ma toobe częścią klastra hello.

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a>Dane telemetryczne zbierane i jak tooopt od niego
Domyślnie produktu hello zbiera dane telemetryczne hello sieci szkieletowej usług użycia tooimprove hello produktu. Analizator najlepszych rozwiązań, który działa jako część instalacji hello sprawdza łączność za Hello[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1). Jeśli nie jest dostępny, hello instalacja zakończy się niepowodzeniem, Jeśli zrezygnujesz z telemetrii.

1. Hello potoku telemetrii próbuje hello tooupload następujące dane zbyt[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) raz każdego dnia. Jest przekazywanie optymalnych i nie ma wpływu na funkcjonalność klastra hello. telemetrii Hello jest wysyłane tylko z węzła hello czy działa hello podstawowy menedżera trybu failover. Nie inne węzły wysłać dane telemetryczne.
2. dane telemetryczne Hello składa się z następujących hello:

* Liczba usług
* Liczba Serivcetype
* Liczba aplikacji
* Liczba ApplicationUpgrades
* Liczba jednostek trybu failover
* Liczba stanie Inbuild
* Liczba UnhealthyFailoverUnits
* Liczba replik
* Liczba InBuildReplicas
* Liczba StandByReplicas
* Liczba OfflineReplicas
* CommonQueueLength
* QueryQueueLength
* FailoverUnitQueueLength
* CommitQueueLength
* Liczba węzłów
* IsContextComplete: PRAWDA/FAŁSZ
* ClusterId: Jest to identyfikator GUID generowany losowo dla każdego klastra
* ServiceFabricVersion
* Adres IP maszyny wirtualnej hello lub komputera, z którym hello jest przekazywany telemetrii

telemetria toodisable dodaje hello zbyt*właściwości* w pliku config klastra: *enableTelemetry: false*.

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a>Funkcje w wersji zapoznawczej zawarte w tym pakiecie
Brak.


> [!NOTE]
> Zaczynając od nowego hello [wersją GA hello autonomiczny klastra w systemie Windows Server (wersja 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), Twojej wersji toofuture klastra, możesz uaktualnić ręcznie lub automatycznie. Odwołuje się zbyt[uaktualnienie wersji autonomicznej klastra sieci szkieletowej usług](service-fabric-cluster-upgrade-windows-server.md) dokumentu, aby uzyskać szczegółowe informacje.
> 
> 

## <a name="next-steps"></a>Następne kroki
* [Wdrażanie i usunąć aplikacje przy użyciu programu PowerShell](service-fabric-deploy-remove-applications.md)
* [Ustawienia konfiguracji dla autonomicznych klastra systemu Windows](service-fabric-cluster-manifest.md)
* [Dodawanie lub usuwanie klastra sieci szkieletowej usług autonomiczny tooa węzłów](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Uaktualnienie wersji autonomicznej klastra sieci szkieletowej usług](service-fabric-cluster-upgrade-windows-server.md)
* [Tworzenie klastra usługi sieć szkieletowa autonomiczny z systemem Windows maszynach wirtualnych platformy Azure](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [Zabezpieczanie klastra autonomicznego w systemie Windows przy użyciu zabezpieczeń systemu Windows](service-fabric-windows-cluster-windows-security.md)
* [Secure autonomiczny klastra w systemie Windows przy użyciu X509 certyfikatów](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
