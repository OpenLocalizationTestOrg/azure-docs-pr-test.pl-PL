---
title: "aaaAzure pakietu autonomicznego sieci szkieletowej usług dla systemu Windows Server | Dokumentacja firmy Microsoft"
description: "Opis i zawartość pakietu hello Azure Service Fabric autonomiczna dla systemu Windows Server."
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
ms.date: 8/10/2017
ms.author: chackdan;maburlik
ms.openlocfilehash: e4c6cb9128d659144e559fcad06bb78c9969dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="contents-of-service-fabric-standalone-package-for-windows-server"></a>Zawartość pakietu autonomicznego sieci szkieletowej usług dla systemu Windows Server
W hello [pobrane](http://go.microsoft.com/fwlink/?LinkId=730690) pakietu autonomicznego sieci szkieletowej usług można znaleźć hello następujące pliki:

| **Nazwa pliku** | **Krótki opis** |
| --- | --- |
| CreateServiceFabricCluster.ps1 |Skrypt programu PowerShell, który jest tworzony klaster hello przy użyciu ustawień hello w pliku ClusterConfig.json. |
| RemoveServiceFabricCluster.ps1 |Skrypt programu PowerShell, która usuwa klastra przy użyciu ustawień hello w pliku ClusterConfig.json. |
| AddNode.ps1 |Skrypt programu PowerShell umożliwiające dodawanie istniejących tooan węzła wdrożeniu klastra na komputerze bieżącym hello. |
| RemoveNode.ps1 |Skrypt programu PowerShell dla usuwania węzła z istniejącego wdrożyć klastra z hello bieżącego komputera. |
| CleanFabric.ps1 |Skrypt programu PowerShell czyszczenia autonomiczny instalacji usługi sieć szkieletowa poza hello bieżącego komputera. Poprzednie instalacje MSI powinny zostać usunięte przy użyciu własnych uninstallers skojarzone. |
| TestConfiguration.ps1 |Skrypt programu PowerShell do analizowania hello infrastruktury, jak określono w hello Cluster.json. |
| DownloadServiceFabricRuntimePackage.ps1 |Skrypt programu PowerShell, używany do pobierania hello najnowszy pakiet obsługi poza pasmem, dla scenariuszy, w których hello wdrażania maszyna nie jest połączonych toohello internet. |
| DeploymentComponentsAutoextractor.exe |Samowyodrębniający archiwum zawierający składniki wdrażania używany przez hello skryptów pakietu autonomicznego. |
| EULA_ENU.txt |Użyj Hello postanowień licencyjnych dotyczących hello pakietu systemu Windows Server autonomicznej usługi sieć szkieletowa usług Microsoft Azure. Możesz [Pobierz kopię hello umowy licencyjnej](http://go.microsoft.com/fwlink/?LinkID=733084) teraz. |
| Readme.txt |Toohello łącze informacje o wersji i instrukcje dotyczące instalacji podstawowych. Jest ona podzbiorem hello instrukcje w tym dokumencie. |
| ThirdPartyNotice.rtf |Powiadomienia o oprogramowania innych firm, które znajduje się w pakiecie hello. |
| Tools\Microsoft.Azure.ServiceFabric.WindowsServer.SupportPackage.zip |StandaloneLogCollector.exe uruchamiany na żądanie śledzenia toocollect i przekazywanie dzienników tooMicrosoft w celu obsługi. |
| Tools\ServiceFabricUpdateService.zip |Narzędzie używane tooenable automatycznego uaktualnienia kodu dla klastrów, które nie mają dostępu do Internetu. Więcej szczegółów można znaleźć [tutaj](service-fabric-cluster-upgrade-windows-server.md)|

**Szablony** 
| **Nazwa pliku** | **Krótki opis** |
| --- | --- |
| ClusterConfig.Unsecure.DevCluster.json |Klastra przykładowy plik konfiguracji zawierający ustawienia hello niezabezpieczonym, trzech węzłów pojedynczego komputera (lub maszyny wirtualnej) projektowanie klastra, wraz z informacjami powitania dla każdego węzła w klastrze hello. |
| ClusterConfig.Unsecure.MultiMachine.json |Klastra przykładowy plik konfiguracji zawierający ustawienia hello niezabezpieczony, wielu (lub maszyny wirtualnej) klastra, wraz z informacjami powitania dla każdego komputera w klastrze hello. |
| ClusterConfig.Windows.DevCluster.json |Klaster przykładowy plik konfiguracji zawierający wszystkie hello ustawienia dla bezpiecznego, trzech węzłów pojedynczego komputera (lub maszyn wirtualnych) klastra projektowego, wraz z informacjami hello na każdym węźle, który znajduje się w klastrze hello. klaster Hello jest zabezpieczony za pomocą [tożsamości systemu Windows](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.Windows.MultiMachine.json |Pliku przykładowej konfiguracji klastra, który zawiera wszystkie ustawienia hello bezpieczny, wielu (lub maszyny wirtualnej) klastra przy użyciu zabezpieczeń systemu Windows, w tym hello informacje dla każdego komputera, który znajduje się w klastrze bezpiecznego hello. klaster Hello jest zabezpieczony za pomocą [tożsamości systemu Windows](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.x509.DevCluster.json |Pliku przykładowej konfiguracji klastra, który zawiera wszystkie ustawienia hello bezpiecznego, trzech węzłów pojedynczego komputera (lub maszyny wirtualnej) programowanie klastrze, w tym hello informacje dla każdego węzła w klastrze hello. Witaj klastra jest zabezpieczone przy użyciu x509 certyfikatów. |
| ClusterConfig.x509.MultiMachine.json |Zabezpiecz plik przykładowy konfiguracji klastra, który zawiera wszystkie ustawienia hello hello klastra wielu (lub maszyny wirtualnej), w tym hello informacje dla każdego węzła w klastrze bezpiecznego hello. Witaj klastra jest zabezpieczone przy użyciu x509 certyfikatów. |
| ClusterConfig.gMSA.Windows.MultiMachine.json |Zabezpiecz plik przykładowy konfiguracji klastra, który zawiera wszystkie ustawienia hello hello klastra wielu (lub maszyny wirtualnej), w tym hello informacje dla każdego węzła w klastrze bezpiecznego hello. Witaj klastra jest zabezpieczone przy użyciu [kont usług zarządzanych grupy](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11).aspx). |

## <a name="cluster-configuration-samples"></a>Przykłady konfiguracji klastra
Najnowsze wersje szablonów konfiguracji klastra można znaleźć na stronie GitHub hello: [przykłady konfiguracji klastra autonomiczny](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

## <a name="independent-runtime-package"></a>Niezależnie od pakietu środowiska wykonawczego
Hello najnowsze środowisko uruchomieniowe pakietu jest automatycznie pobierana podczas wdrażania klastra z [łącze Pobierz — środowisko uruchomieniowe usługi sieć szkieletowa - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).

## <a name="related"></a>Powiązane
* [Tworzenie klastra sieci szkieletowej usług Azure autonomiczny](service-fabric-cluster-creation-for-windows-server.md)
* [Scenariusze zabezpieczeń klastra sieci szkieletowej usług](service-fabric-windows-cluster-windows-security.md)
