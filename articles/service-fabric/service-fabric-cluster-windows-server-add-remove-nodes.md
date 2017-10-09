---
title: "aaaAdd lub usuń węzły tooa autonomicznej klastra sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd lub usuń węzły tooan sieć szkieletowa usług Azure klastra na fizyczne lub maszyny wirtualnej z systemem Windows Server, który może być lokalnym lub w dowolnej chmury."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a>Dodawanie lub usuwanie węzłów tooa autonomicznej klastra sieci szkieletowej usług w systemie Windows Server
Po utworzeniu [utworzone autonomicznej klastra sieci szkieletowej usług na komputerach z systemem Windows Server](service-fabric-cluster-creation-for-windows-server.md), może zmieniających się potrzeb biznesowych i może być konieczne tooadd lub usunąć węzły klastra tooyour. Ten artykuł zawiera szczegółowy opis kroków tooachieve to. Należy pamiętać, że dodawania i usuwania węzła funkcjonalność nie jest obsługiwana w klastrach rozwoju lokalnego.

## <a name="add-nodes-tooyour-cluster"></a>Dodaj węzły klastra tooyour
1. Witaj przygotowanie wirtualna/machine ma tooadd tooyour klastra, wykonując kroki hello wspomnianego hello [hello przygotowanie maszyny toomeet hello z wymagań wstępnych dotyczących wdrażania klastra](service-fabric-cluster-creation-for-windows-server.md) sekcji
2. Identyfikowanie które domeny błędów i są tooadd będzie tej maszyny Wirtualnej/maszyny do domeny uaktualnienia
3. Pulpitu zdalnego (RDP) do hello maszyny Wirtualnej/maszyny, które mają tooadd toohello klastra
4. Kopiowanie lub [Pobierz autonomiczny hello sieci szkieletowej usług w systemie Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello maszyny Wirtualnej/machine i Rozpakuj pakiet hello
5. Uruchom program Powershell z podwyższonym poziomem uprawnień i przejdź toohello lokalizacji rozpakowanej pakietu hello
6. Uruchom hello *AddNode.ps1* skryptu z parametrami hello opisujące hello nowego węzła tooadd. w poniższym przykładzie Hello dodaje nowy węzeł o nazwie VM5, z typem NodeType0 i adresów IP 182.17.34.52, UD1 i fd: / dc1/r0. Hello *ExistingClusterConnectionEndPoint* punktu końcowego połączenia dla węzła jest już hello istniejącego klastra, które mogą być hello adres IP *żadnych* węzła w klastrze hello.

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    Po zakończeniu hello skryptu można sprawdzić, czy nowy węzeł hello został dodany przez uruchomienie hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) polecenia cmdlet.

7. tooensure spójności w różnych węzłach w klastrze hello, musisz zainicjować uaktualnienie konfiguracji. Uruchom [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello najnowszego pliku konfiguracji i Dodaj hello nowo dodany węzeł zbyt sekcji "Węzłów". Zalecane jest również, tooalways hello najnowsze klastra konfiguracja jest dostępna w przypadku hello konieczność tooredploy klastra z hello tej samej konfiguracji.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. Uruchom [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello uaktualnienia.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    Możesz monitorować postęp hello hello uaktualnienia w narzędziu Service Fabric Explorer. Alternatywnie można uruchomić [Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a>Dodaj węzły tooclusters skonfigurowaną przy użyciu usługi zarządzane przez grupę zabezpieczeń systemu Windows
W przypadku klastrów skonfigurowano Account(gMSA) usług zarządzanych grupy (https://technet.microsoft.com/library/hh831782.aspx) przy użyciu uaktualniania programu configuration można dodać nowego węzła:
1. Uruchom [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) na żadnym z istniejących węzłów hello tooget hello najnowszego pliku konfiguracji i Dodaj szczegóły dotyczące hello nowy węzeł ma tooadd w sekcji węzły"hello". Upewnij się, że hello nowy węzeł jest częścią programu hello zarządzanego konta sam grupy. To konto powinno mieć uprawnienia administratora na wszystkich komputerach.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. Uruchom [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello uaktualnienia.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    Możesz monitorować postęp hello hello uaktualnienia w narzędziu Service Fabric Explorer. Alternatywnie można uruchomić [Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

### <a name="add-node-types-tooyour-cluster"></a>Dodaj węzły klastra tooyour typów
Kolejność tooadd nowego typu węzła, zmodyfikuj konfigurację tooinclude hello nowego węzła typu w sekcji "Elementów NodeType" w obszarze "Właściwości" i rozpocząć konfigurację aktualizację, używając [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps). Po zakończeniu uaktualniania hello, możesz dodać nowy klaster tooyour węzły z tym typem węzła.

## <a name="remove-nodes-from-your-cluster"></a>Usuń węzły z klastra
Można usunąć węzła z klastra przy użyciu uaktualniania konfiguracji, w następujące sposób hello:

1. Uruchom [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello najnowszego pliku konfiguracji i *Usuń* hello węzła z sekcji "Węzłów".
Dodaj hello "NodesToBeRemoved" parametr zbyt "ustawienia" sekcji wewnątrz sekcji "FabricSettings". Witaj "wartość" powinna być rozdzielana przecinkami lista nazwy węzła węzłów, które wymagają toobe usunięte.

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. Uruchom [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello uaktualnienia.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    Możesz monitorować postęp hello hello uaktualnienia w narzędziu Service Fabric Explorer. Alternatywnie można uruchomić [Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

> [!NOTE]
> Usuwanie węzłów może zainicjować kilku uaktualnień. Niektóre węzły są oznaczone ikoną z `IsSeedNode=”true”` tagu i mogą zostać zidentyfikowane przez wysyłanie zapytań klastra hello manifestu przy użyciu `Get-ServiceFabricClusterManifest`. Usunięcie tych węzłów może trwać dłużej niż inne, ponieważ hello inicjatora węzły będą mieć toobe przenoszenia w takich scenariuszach. Hello klastra musi obsługiwać co najmniej 3 węzłach typu węzła podstawowego.
> 
> 

### <a name="remove-node-types-from-your-cluster"></a>Usuń typy węzłów z klastra
Przed usunięciem typu węzła, sprawdź występują we wszystkich węzłach, odwołuje się do typu węzła hello. Usuń te węzły przed usunięciem hello odpowiedniego typu węzła. Po usunięciu wszystkich odpowiadających im węzłów, musisz usunąć hello NodeType z konfiguracji klastra hello i zacząć od konfiguracji aktualizację, używając [Start ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).


### <a name="replace-primary-nodes-of-your-cluster"></a>Zastąp głównej węzłów w klastrze
zastąpienie Hello głównej węzłów powinny być wykonywane jeden węzeł po kolei, zamiast usuwania, a następnie dodanie w partiach.


## <a name="next-steps"></a>Następne kroki
* [Ustawienia konfiguracji dla autonomicznych klastra systemu Windows](service-fabric-cluster-manifest.md)
* [Secure autonomiczny klastra w systemie Windows przy użyciu X509 certyfikatów](service-fabric-windows-cluster-x509-security.md)
* [Tworzenie klastra usługi sieć szkieletowa autonomiczny z systemem Windows maszynach wirtualnych platformy Azure](service-fabric-cluster-creation-with-windows-azure-vms.md)

