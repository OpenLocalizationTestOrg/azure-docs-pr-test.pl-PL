---
title: "aaaSet zapasowej autonomicznej klastra sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Utworzyć klaster autonomiczny programowanie z trzech węzłów uruchomionych na powitania tym samym komputerze. Po ukończeniu tej konfiguracji będzie gotowy toocreate klastrze z wieloma maszynami."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: e4d0ea9fc3b8475160bd8ed19fd3716463791cc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a>Tworzenie pierwszego autonomicznego klastra usługi Service Fabric
Można utworzyć klastra sieci szkieletowej usług autonomiczny żadnych maszyn wirtualnych lub komputerach z systemem Windows Server 2012 R2 lub Windows Server 2016, lokalnie lub w chmurze hello. Tego przewodnika Szybki Start pomaga toocreate klastra autonomiczny Programowanie w zaledwie kilka minut.  Po zakończeniu na pojedynczym komputerze będzie dostępny klaster z trzema węzłami, do którego można wdrażać aplikacje.

## <a name="before-you-begin"></a>Przed rozpoczęciem
Usługa Service Fabric realizuje konfiguracji pakietu toocreate sieci szkieletowej usług autonomicznych klastrów.  [Pobierz pakiet instalacyjny hello](http://go.microsoft.com/fwlink/?LinkId=730690).  Rozpakuj hello Instalatora tooa folderu pakietu na powitania komputer lub maszynę wirtualną których konfigurujesz hello tworzenia klastra.  szczegółowy opis Hello zawartość pakietu instalacyjnego hello [tutaj](service-fabric-cluster-standalone-package-contents.md).

administrator klastra Hello wdrażania i konfigurowania klastra hello musi mieć uprawnienia administratora na komputerze hello. Usługi Service Fabric nie można zainstalować na kontrolerze domeny.

## <a name="validate-hello-environment"></a>Sprawdź poprawność hello środowiska
Witaj *TestConfiguration.ps1* skryptu w pakiecie autonomiczny hello jest używany jako najlepsze rozwiązania w zakresie analizator toovalidate czy klastra może zostać wdrożony w danym środowisku. [Przygotowanie do wdrożenia](service-fabric-cluster-standalone-deployment-preparation.md) list hello wymagania wstępne i wymagania środowiska. Uruchom tooverify skryptu powitania po utworzeniu klastra projektowego hello:

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-hello-cluster"></a>Tworzenie klastra hello
Kilka przykładowych plików konfiguracji klastra są zainstalowane z pakietu instalacyjnego hello. *ClusterConfig.Unsecure.DevCluster.json* jest najprostsza konfiguracja klastra hello: niezabezpieczone, trzech węzłów klastra z systemem na pojedynczym komputerze.  Inne pliki konfiguracji zawierają opis klastrów dla jednej lub wielu maszyn, zabezpieczonych za pomocą certyfikatów X.509 lub zabezpieczeń systemu Windows.  Nie wymagają ustawienia konfiguracji domyślnej hello toomodify w tym samouczku, ale Przejrzyj hello pliku konfiguracji i zapoznać się z ustawieniami hello.  Witaj **węzłów** sekcji opisano hello trzy węzły w klastrze hello: nazwa, adres IP, [typu węzła domeny błędów i domena uaktualnienia](service-fabric-cluster-manifest.md#nodes-on-the-cluster).  Witaj **właściwości** sekcja definiuje hello [bezpieczeństwa, poziom niezawodności kolekcji diagnostyki i typy węzłów](service-fabric-cluster-manifest.md#cluster-properties) hello klastra.

Ten klaster jest niezabezpieczony.  Każda osoba może połączyć się z nim anonimowo i przeprowadzić operacje związane z zarządzaniem. Dlatego też klastry produkcyjne należy zawsze zabezpieczać przy użyciu certyfikatów X.509 lub zabezpieczeń systemu Windows.  Zabezpieczeń jest skonfigurowany tylko w czasie tworzenia klastra i nie jest możliwe tooenable zabezpieczeń po utworzeniu klastra hello.  Odczyt [Secure klastra](service-fabric-cluster-security.md) toolearn więcej informacji na temat zabezpieczeń klastra sieci szkieletowej usług.  

toocreate hello programowanie trzech węzłów klastra, uruchom hello *CreateServiceFabricCluster.ps1* skryptu z sesji programu PowerShell administratora:

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

Pakiet środowiska uruchomieniowego platformy Service Fabric Hello jest automatycznie pobierane i instalowane w czasie tworzenia klastra.

## <a name="connect-toohello-cluster"></a>Połącz toohello klastra
Klaster programowania z trzema węzłami został uruchomiony. Witaj modułu ServiceFabric programu PowerShell jest instalowany z hello środowiska wykonawczego.  Można sprawdzić klastra hello jest uruchomiona z hello tym samym komputerze lub na komputerze zdalnym ze środowiskiem uruchomieniowym usługi sieć szkieletowa hello.  Witaj [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet ustanawia połączenie toohello klastra.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
Zobacz [klastra bezpiecznego połączenia tooa](service-fabric-connect-to-secure-cluster.md) inne przykłady łączącego tooa klastra. Po łączącego toohello klastra, użyj hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay polecenia cmdlet listy węzłów w hello klastra oraz informacje o stanie dla każdego węzła. Element **HealthState** powinien mieć wartość *OK* dla każdego węzła.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Wizualizowanie klastra hello za pomocą Eksploratora usługi sieć szkieletowa
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) to odpowiednie narzędzie do wizualizowania klastra i zarządzania aplikacjami.  Service Fabric Explorer to usługa, która działa w klastrze hello, otwieranego w przeglądarce za przechodząc[http://localhost: 19080/Explorer](http://localhost:19080/Explorer). 

pulpit nawigacyjny klastra Hello Omówienie klastra, w tym podsumowanie aplikacji i kondycji węzła. Widok węzła Hello przedstawia hello fizycznego układu hello klastra. Dla danego węzła można sprawdzić, które aplikacje mają kod wdrożony w tym węźle.

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-hello-cluster"></a>Usuń hello klastra
tooremove klastra, uruchom hello *RemoveServiceFabricCluster.ps1* skrypt programu PowerShell z folderu pakietu hello i przekazać w pliku konfiguracji JSON hello ścieżki toohello. Opcjonalnie można określić lokalizację dziennika hello hello usuwania.

```powershell
# Removes Service Fabric cluster nodes from each computer in hello configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

tooremove hello środowiska uruchomieniowego platformy Service Fabric z hello komputera, uruchom hello następującego skryptu programu PowerShell z hello folderu pakietu.

```powershell
# Removes Service Fabric from hello current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a>Następne kroki
Po skonfigurowaniu klastra autonomiczny programowanie wypróbować hello następujące artykuły:
* [Konfigurowanie autonomicznego klastra dla wielu maszyn](service-fabric-cluster-creation-for-windows-server.md) i włączanie zabezpieczeń
* [Wdrażanie aplikacji przy użyciu programu PowerShell](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
