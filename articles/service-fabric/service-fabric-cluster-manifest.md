---
title: "aaaConfigure autonomicznej klastra sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure z autonomicznej lub prywatnej klastra sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a>Ustawienia konfiguracji dla autonomicznych klastra systemu Windows
W tym artykule opisano, jak hello tooconfigure using klastra usługi sieć szkieletowa autonomiczny ***pliku ClusterConfig.JSON*** pliku. Możesz użyć tych informacji toospecify plików takich jak hello węzłów sieci szkieletowej usług i ich adresy IP, różne typy węzłów w hello klastra, hello konfiguracji zabezpieczeń, a także topologii sieci hello pod względem błędów/uaktualnienia domen, dla Twojej autonomicznej klaster.

Gdy możesz [Pobierz hello wersjach usługi sieć szkieletowa](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), kilka przykładów hello pliku ClusterConfig.JSON pliku są pobierane tooyour pracy maszyny. Witaj próbki o *DevCluster* w nazwach pomoże utworzyć klaster z wszystkie trzy węzły na hello komputera takie same, jak logicznej węzłów. Poza tym przypadku co najmniej jeden węzeł może być oznaczona jako węzła podstawowego. Ten klaster jest przydatne w środowisku projektowania lub testowym i nie jest obsługiwany jako klastra produkcyjnego. Witaj próbki o *MultiMachine* w nazwach, pomoże utworzyć klaster jakości produkcyjnych z każdego węzła na osobnym komputerze.

1. *ClusterConfig.Unsecure.DevCluster.JSON* i *ClusterConfig.Unsecure.MultiMachine.JSON* Pokaż jak toocreate niezabezpieczona testu lub produkcji klastra odpowiednio. 
2. *ClusterConfig.Windows.DevCluster.JSON* i *ClusterConfig.Windows.MultiMachine.JSON* Pokaż jak toocreate testowym lub produkcyjnym klastra zabezpieczone za pomocą [zabezpieczenia systemu Windows](service-fabric-windows-cluster-windows-security.md).
3. *ClusterConfig.X509.DevCluster.JSON* i *ClusterConfig.X509.MultiMachine.JSON* Pokaż jak toocreate testowym lub produkcyjnym klastra zabezpieczone za pomocą [X509 zabezpieczeń oparte na certyfikatach](service-fabric-windows-cluster-x509-security.md). 

Teraz zostanie hello różnych części ***pliku ClusterConfig.JSON*** plików zgodnie z poniższymi instrukcjami.

## <a name="general-cluster-configurations"></a>Konfiguracje klastrów ogólne
Obejmuje to hello szerokie klastra określonej konfiguracji, jak pokazano w poniższy fragment hello JSON.

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

Można nadać dowolnego klastra usługi sieć szkieletowa tooyour przyjaznej nazwy, przypisując toohello **nazwa** zmiennej. Witaj **clusterConfigurationVersion** jest numer wersji hello klastra; należy zwiększyć jego każdorazowego uaktualnienia klastra sieci szkieletowej usług. Jednak należy pozostawić hello **apiVersion** toohello wartości domyślnej.

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a>Węzły w klastrze hello
Można skonfigurować hello węzłów w klastrze usługi sieć szkieletowa usług za pomocą hello **węzłów** sekcji jako powitania po fragment kodu przedstawia.

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

Klaster sieci szkieletowej usług musi zawierać co najmniej 3 węzłach. Możesz dodać więcej węzłów toothis sekcji zgodnie z konfiguracji. Witaj w poniższej tabeli opisano hello ustawienia konfiguracji dla każdego węzła.

| **Konfiguracja węzła** | **Opis** |
| --- | --- |
| nodeName |Aby zapewnić dowolnego węzła toohello przyjazną nazwę. |
| Adres IP |Sprawdzić hello adres IP węzła, otwierając okno polecenia i wpisując `ipconfig`. Zanotuj adres hello IPV4 i przypisać je toohello **iPAddress** zmiennej. |
| wartość nodetyperef równą |Każdy węzeł można przypisać typu innego węzła. Witaj [typy węzłów](#nodetypes) są zdefiniowane w poniższej sekcji hello. |
| faultDomain |Błąd domen Włącz klastra Administratorzy toodefine hello węzłów fizycznych, które może zakończyć się niepowodzeniem na powitania takie same czasu powodu tooshared fizycznych zależności. |
| upgradeDomain |Domen uaktualnienia opisano zestaw węzłów, które są zamykane dla sieci szkieletowej usług uaktualnia na temat hello sam czas. Można które toowhich tooassign węzłów domen uaktualnienia, ponieważ nie są ograniczone przez wszystkie fizyczne wymagania. |

## <a name="cluster-properties"></a>Właściwości klastra
Witaj **właściwości** sekcji w pliku ClusterConfig.JSON hello jest używany tooconfigure hello klastra w następujący sposób.

<a id="reliability"></a>

### <a name="reliability"></a>Niezawodność
pojęcie Hello **reliabilityLevel** definiuje hello liczby replik lub wystąpień hello usługi sieć szkieletowa systemu usług, które można uruchamiać na powitania głównej węzłów klastra hello. Określa hello niezawodności tych usług, a więc hello klastra. wartość Hello jest obliczeniowa przez hello system w czasie tworzenia i uaktualniania klastra.

### <a name="diagnostics"></a>Diagnostyka
Witaj **diagnosticsStore** sekcji pozwala tooconfigure parametry tooenable diagnostyki i rozwiązywania problemów z węzła lub awarii klastra, jak pokazano w hello następującego fragmentu. 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

Witaj **metadanych** znajduje się opis diagnostycznej klastra i można ustawić odpowiednią konfigurację. Te zmienne pomocy zbierania ETW dzienniki śledzenia, zrzuty awaryjne także liczników wydajności. Odczyt [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) i [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) dzienniki śledzenia Aby uzyskać więcej informacji dotyczących funkcji ETW. Wszystkie dzienniki tym [awarii zrzuty](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) i [liczniki wydajności](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) może być ukierunkowanej toohello **connectionString** folderu na komputerze. Można również użyć *AzureStorage* do przechowywania diagnostyki. Poniżej znajduje się fragment próbki.

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a>Bezpieczeństwo
Witaj **zabezpieczeń** sekcja jest niezbędne do bezpiecznego autonomicznej klastra sieci szkieletowej usług. powitania po fragment kodu przedstawia części tej sekcji.

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

Witaj **metadanych** opis klastra bezpiecznego a może ustawić odpowiednią konfigurację. Witaj **ClusterCredentialType** i **ServerCredentialType** ustalić typu hello zabezpieczeń, które wykona klaster hello i hello węzły. Mogą być ustawione tooeither *X509* zabezpieczeń oparte na certyfikatach lub *Windows* dla zabezpieczeń opartych na usłudze Azure Active Directory. Witaj rest hello **zabezpieczeń** sekcji będą oparte na typ hello hello zabezpieczeń. Odczyt [zabezpieczenia oparte na certyfikaty w klastrze autonomiczny](service-fabric-windows-cluster-x509-security.md) lub [zabezpieczenia systemu Windows w klastrze autonomiczny](service-fabric-windows-cluster-windows-security.md) Aby uzyskać informacje dotyczące sposobu toofill limit hello pozostałej części hello **zabezpieczeń**sekcji.

<a id="nodetypes"></a>

### <a name="node-types"></a>Typy węzłów
Witaj **elementów NodeType** sekcja opisuje typ hello hello węzłów, które ma w klastrze. Należy określić typ co najmniej jeden węzeł klastra, jak pokazano w poniższy fragment hello. 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

Witaj **nazwa** jest hello przyjazną nazwę dla tego typu określonego węzła. toocreate węzeł tego typu węzła przypisać jej toohello przyjazną nazwę **wartość nodetyperef równą** zmiennej dla tego węzła, jak wspomniano [powyżej](#clusternodes). Dla każdego typu węzła punkty końcowe połączenia hello, które będą używane. Można wybrać dowolny inny numer portu na te punkty końcowe połączenia, tak długo, jak nie powodują konfliktów z innymi punktami końcowymi w tym klastrze. W klastrze z wieloma węzłami, będzie co najmniej jeden węzeł podstawowy (tj. **isPrimary** ustawić także*true*), w zależności od hello [ **reliabilityLevel** ](#reliability). Odczyt [zagadnienia związane z planowaniem pojemności klastra sieci szkieletowej usług](service-fabric-cluster-capacity.md) uzyskać informacji o **elementów NodeType** i **reliabilityLevel**i tooknow co to są podstawowego i hello typy węzłów innych niż podstawowe. 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a>Typy węzłów hello tooconfigure używane punkty końcowe
* *clientConnectionEndpointPort* hello port jest używany przez powitania klienta tooconnect toohello klastra, używając powitania klienta interfejsów API. 
* *clusterConnectionEndpointPort* jest port hello jaką węzłów hello komunikują się ze sobą.
* *leaseDriverEndpointPort* hello port jest używany przez hello klastra dzierżawy sterownika toofind się, jeśli hello węzły są nadal aktywne. 
* *serviceConnectionEndpointPort* jest hello port używany przez program hello aplikacje i usługi wdrożone w węźle toocommunicate z klientem usługi sieć szkieletowa hello na dany węzeł.
* *httpGatewayEndpointPort* hello port jest używany przez hello Service Fabric Explorer tooconnect toohello klastra.
* *ephemeralPorts* zastąpienia hello [dynamiczne porty używane przez system operacyjny hello](https://support.microsoft.com/kb/929851). Sieć szkieletowa usług użyje części tych portów aplikacji i pozostałych hello będą dostępne dla hello systemu operacyjnego. Zostanie również mapować tego zakresu toohello istniejącego zakresu w hello systemu operacyjnego, więc dla wszystkich celów, można użyć zakresów hello podany w hello przykładowych plików JSON. Należy toomake się, że hello różnica między początkową hello i porty końcowe hello jest co najmniej 255. Jeśli różnica jest zbyt niski, ponieważ ten zakres jest współużytkowany z systemu operacyjnego hello może wystąpiły konflikty. Zobacz zakres portów dynamicznych hello skonfigurowany, uruchamiając `netsh int ipv4 show dynamicport tcp`.
* *applicationPorts* hello portów, które będą używane przez aplikacje platformy Service Fabric hello. zakres portów aplikacji Hello powinien być wystarczająco duży toocover hello punktu końcowego wymagań aplikacji. Ten zakres powinien być wyłączne z zakresu portów dynamicznych hello na powitania maszyny, tzn. hello *ephemeralPorts* zakresem określonym w konfiguracji hello.  Usługa sieci szkieletowej będą one używane przy każdym nowe porty są wymagane, a także zajmie się otwarcie zapory powitania dla tych portów. 
* *reverseProxyEndpointPort* jest punktem końcowym opcjonalne zwrotnego serwera proxy. Zobacz [serwera Proxy usługi sieci szkieletowej wstecznego](service-fabric-reverseproxy.md) więcej szczegółów. 

### <a name="log-settings"></a>Ustawienia dziennika
Witaj **fabricSettings** sekcja umożliwia katalogi główne hello tooset hello sieci szkieletowej usług danych i dzienniki. Można dostosować te tylko podczas tworzenia klastra hello. Poniżej znajduje się fragment próbki w tej sekcji.

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

Zaleca się przy użyciu dysku z systemem innym niż systemu operacyjnego jako hello zmiennej FabricDataRoot i lokalizacji FabricLogRoot zapewnia niezawodność więcej względem awarii systemu operacyjnego. Należy pamiętać, że jeśli możesz dostosować tylko hello danych głównych, następnie hello dziennika głównego zostaną umieszczone jeden poziom w dół hello danych głównych.

### <a name="stateful-reliable-service-settings"></a>Ustawienia usługi stanowej niezawodnej
Witaj **KtlLogger** sekcja umożliwia tooset hello globalne ustawienia konfiguracji dla usług niezawodne. Aby uzyskać więcej informacji na temat tych ustawień do odczytu [skonfigurować niezawodne usługi stanowej](service-fabric-reliable-services-configuration.md).
w poniższym przykładzie Hello pokazuje, jak dziennika transakcji udostępnionego hello hello toochange, który pobiera utworzone tooback wszystkie kolekcje niezawodnych usług stanowych.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a>Dodatkowe funkcje
tooconfigure dodatkowe funkcje, hello apiVersion powinien być skonfigurowany jako "04-2017' lub nowszej, a addonFeatures musi toobe skonfigurowane:

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a>Obsługa kontenerów
tooenable kontenera obsługę systemu windows server kontenera i kontener autonomicznych klastrów funkcji hyper-v, funkcja dodatku "DnsService" hello musi toobe włączone.


## <a name="next-steps"></a>Następne kroki
Po utworzeniu pełny plik pliku ClusterConfig.JSON skonfigurowane zgodnie z autonomicznego Instalatora klastra, można wdrożyć klaster w następującym artykule hello [tworzenia klastra usługi sieć szkieletowa autonomiczny](service-fabric-cluster-creation-for-windows-server.md) , a następnie kontynuować zbyt[wizualizacja klastra za pomocą Eksploratora usługi sieć szkieletowa](service-fabric-visualizing-your-cluster.md).

