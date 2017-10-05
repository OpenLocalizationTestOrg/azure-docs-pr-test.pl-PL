---
title: "Konfigurowanie klastra autonomiczny sieć szkieletowa usług Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować autonomiczny lub prywatnej klastra sieci szkieletowej usług."
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
ms.openlocfilehash: 9885dce18dabac4a945dafd219e3ae190e34a83b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a>Ustawienia konfiguracji dla autonomicznych klastra systemu Windows
W tym artykule opisano sposób konfigurowania autonomicznej usługi sieć szkieletowa klastra za pomocą ***pliku ClusterConfig.JSON*** pliku. Ten plik służy do określ informacje, takie jak węzłów sieci szkieletowej usług i ich adresy IP, różne typy węzłów na klaster, konfiguracjach zabezpieczeń, a także topologii sieci pod względem błędów/uaktualnienia domen, dla klastra autonomicznych.

Gdy można [Pobierz autonomiczny pakiet sieci szkieletowej usług](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), na komputerze pracy są pobierane kilka przykładów pliku pliku ClusterConfig.JSON. Próbki o *DevCluster* w nazwach zawierają informacje pomocne podczas tworzenia klastra ze wszystkich trzech węzłów na tym samym komputerze, takich jak logicznej węzłów. Poza tym przypadku co najmniej jeden węzeł może być oznaczona jako węzła podstawowego. Ten klaster jest przydatne w środowisku projektowania lub testowym i nie jest obsługiwany jako klastra produkcyjnego. Próbki o *MultiMachine* w nazwach, pomoże utworzyć klaster jakości produkcyjnych z każdego węzła na osobnym komputerze.

1. *ClusterConfig.Unsecure.DevCluster.JSON* i *ClusterConfig.Unsecure.MultiMachine.JSON* pokazują, jak utworzyć odpowiednio niezabezpieczona testowym lub produkcyjnym klastra. 
2. *ClusterConfig.Windows.DevCluster.JSON* i *ClusterConfig.Windows.MultiMachine.JSON* pokazują, jak utworzyć klaster testowym lub produkcyjnym chronione za pomocą [zabezpieczenia systemu Windows](service-fabric-windows-cluster-windows-security.md).
3. *ClusterConfig.X509.DevCluster.JSON* i *ClusterConfig.X509.MultiMachine.JSON* pokazują, jak utworzyć klaster testowym lub produkcyjnym chronione za pomocą [X509 zabezpieczeń oparte na certyfikatach](service-fabric-windows-cluster-x509-security.md). 

Teraz zostanie omówione różnych części ***pliku ClusterConfig.JSON*** plików zgodnie z poniższymi instrukcjami.

## <a name="general-cluster-configurations"></a>Konfiguracje klastrów ogólne
Obejmuje określonej konfiguracji klastra szerokie, jak pokazano poniżej fragment kodu JSON.

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

Może być dowolną przyjazną nazwę klastra sieci szkieletowej usług przez przypisanie go do **nazwa** zmiennej. **ClusterConfigurationVersion** jest numer wersji klastra; należy zwiększyć jego każdorazowego uaktualnienia klastra sieci szkieletowej usług. Jednak należy pozostawić **apiVersion** na wartość domyślną.

<a id="clusternodes"></a>

## <a name="nodes-on-the-cluster"></a>Węzły w klastrze
Węzły w klastrze usługi sieć szkieletowa można skonfigurować przy użyciu **węzłów** sekcji jako poniższy fragment kodu przedstawia.

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

Klaster sieci szkieletowej usług musi zawierać co najmniej 3 węzłach. Zgodnie z ustawień, można dodać więcej węzłów do tej sekcji. W poniższej tabeli opisano ustawienia konfiguracji dla każdego węzła.

| **Konfiguracja węzła** | **Opis** |
| --- | --- |
| nodeName |Można nadać dowolną przyjazną nazwę do węzła. |
| Adres IP |Sprawdzić adres IP węzła, otwierając okno polecenia i wpisując `ipconfig`. Zanotuj adres IPV4 i przypisz go do **iPAddress** zmiennej. |
| wartość nodetyperef równą |Każdy węzeł można przypisać typu innego węzła. [Typy węzłów](#nodetypes) są zdefiniowane w poniższej sekcji. |
| faultDomain |Domen błędów umożliwiają administratorom klastra zdefiniuj węzłów fizycznych, które może zakończyć się niepowodzeniem w tym samym czasie, z powodu zależności fizycznej udostępnionego. |
| upgradeDomain |Domen uaktualnienia opisano zestaw węzłów, które są wyłączone uaktualnienia sieci szkieletowej usług na o tym samym czasie. Możesz węzły, które można przypisać do uaktualnienia domen, ponieważ nie są ograniczone przez wszystkie fizyczne wymagania. |

## <a name="cluster-properties"></a>Właściwości klastra
**Właściwości** sekcji w pliku ClusterConfig.JSON jest używany do konfigurowania klastra w następujący sposób.

<a id="reliability"></a>

### <a name="reliability"></a>Niezawodność
Pojęcie **reliabilityLevel** definiuje liczbę replik lub wystąpień usług systemowych sieci szkieletowej usług, które można uruchamiać na głównej węzłów klastra. Określa niezawodności tych usług i tym samym klastrze. Wartość jest obliczeniowa przez system podczas tworzenia i uaktualniania klastra.

### <a name="diagnostics"></a>Diagnostyka
**DiagnosticsStore** sekcji pozwala na skonfigurowanie parametrów, aby włączyć diagnostyki i rozwiązywania problemów z węzła lub awarii klastra, jak pokazano w poniższy fragment kodu. 

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

**Metadanych** znajduje się opis diagnostycznej klastra i można ustawić odpowiednią konfigurację. Te zmienne pomocy zbierania ETW dzienniki śledzenia, zrzuty awaryjne także liczników wydajności. Odczyt [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) i [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) dzienniki śledzenia Aby uzyskać więcej informacji dotyczących funkcji ETW. Wszystkie dzienniki tym [awarii zrzuty](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) i [liczniki wydajności](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) może zostać skierowany do **connectionString** folderu na komputerze. Można również użyć *AzureStorage* do przechowywania diagnostyki. Poniżej znajduje się fragment próbki.

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a>Bezpieczeństwo
**Zabezpieczeń** sekcja jest niezbędne do bezpiecznego autonomicznej klastra sieci szkieletowej usług. Poniższy fragment kodu przedstawia części tej sekcji.

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

**Metadanych** opis klastra bezpiecznego a może ustawić odpowiednią konfigurację. **ClusterCredentialType** i **ServerCredentialType** określają typ zabezpieczeń, który będzie implementowany klastra oraz węzłów. Mogą być ustawione jako *X509* zabezpieczeń oparte na certyfikatach lub *Windows* dla zabezpieczeń opartych na usłudze Azure Active Directory. Pozostała część **zabezpieczeń** sekcji będą oparte na typ zabezpieczeń. Odczytu [zabezpieczenia oparte na certyfikaty w klastrze autonomiczny](service-fabric-windows-cluster-x509-security.md) lub [zabezpieczenia systemu Windows w klastrze autonomiczny](service-fabric-windows-cluster-windows-security.md) informacji dotyczących wypełniania reszty **zabezpieczeń** sekcja.

<a id="nodetypes"></a>

### <a name="node-types"></a>Typy węzłów
**Elementów NodeType** sekcja opisuje typ węzłów, które ma w klastrze. Należy określić typ co najmniej jeden węzeł klastra, jak pokazano w poniższy fragment. 

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

**Nazwa** jest przyjazną nazwę dla tego typu określonego węzła. Aby utworzyć węzeł tego typu węzła, przypisz przyjazną nazwę, którą **wartość nodetyperef równą** zmiennej dla tego węzła, jak wspomniano [powyżej](#clusternodes). Zdefiniuj punkty końcowe połączenia, które będą używane dla każdego typu węzła. Można wybrać dowolny inny numer portu na te punkty końcowe połączenia, tak długo, jak nie powodują konfliktów z innymi punktami końcowymi w tym klastrze. W klastrze z wieloma węzłami, będzie co najmniej jeden węzeł podstawowy (tj. **isPrimary** ustawioną *true*), w zależności od [ **reliabilityLevel** ](#reliability). Odczyt [zagadnienia związane z planowaniem pojemności klastra usługi sieć szkieletowa](service-fabric-cluster-capacity.md) uzyskać informacji o **elementów NodeType** i **reliabilityLevel**oraz określenie, jakie są podstawowego i typy węzłów innych niż podstawowe. 

#### <a name="endpoints-used-to-configure-the-node-types"></a>Punkty końcowe umożliwiają skonfigurowanie typy węzłów
* *clientConnectionEndpointPort* to port używany przez klienta, aby połączyć się z klastrem, podczas korzystania z interfejsów API klienta. 
* *clusterConnectionEndpointPort* jest port, na jaką węzły komunikują się ze sobą.
* *leaseDriverEndpointPort* jest port używany przez sterownik dzierżawę klastra, aby sprawdzić, czy węzły są nadal aktywne. 
* *serviceConnectionEndpointPort* jest port używany przez aplikacje i usługi wdrożone w węźle do komunikacji z klientem usługi sieć szkieletowa na dany węzeł.
* *httpGatewayEndpointPort* jest port używany przez Service Fabric Explorer, aby połączyć się z klastrem.
* *ephemeralPorts* zastąpienia [dynamiczne porty używane przez system operacyjny](https://support.microsoft.com/kb/929851). Sieć szkieletowa usług użyje części tych portów aplikacji i pozostałe będą dostępne dla systemu operacyjnego. On również przypisze ten zakres do istniejący zakres obecne w systemie operacyjnym, więc dla wszystkich celów, można użyć zakresów podany w przykładowych plików JSON. Należy się upewnić, że różnica między początek i koniec portów jest co najmniej 255. Jeśli różnica jest zbyt niski, ponieważ ten zakres jest udostępniony w systemie operacyjnym, może wystąpiły konflikty. Zobacz skonfigurowany dynamicznego zakresu portów, uruchamiając `netsh int ipv4 show dynamicport tcp`.
* *applicationPorts* portów, które będą używane przez aplikacje, sieć szkieletowa usług. Zakres portów aplikacji powinien być wystarczająco duży, aby pokryć zapotrzebowanie punkt końcowy aplikacji. Ten zakres powinien być wyłączne z dynamicznego zakresu portów na komputerze, tj. *ephemeralPorts* zakresu zgodnie z ustawieniami w konfiguracji.  Usługa sieci szkieletowej będą one używane przy każdym nowe porty są wymagane, a także zajmie się otwarcie tych portów zapory. 
* *reverseProxyEndpointPort* jest punktem końcowym opcjonalne zwrotnego serwera proxy. Zobacz [serwera Proxy usługi sieci szkieletowej wstecznego](service-fabric-reverseproxy.md) więcej szczegółów. 

### <a name="log-settings"></a>Ustawienia dziennika
**FabricSettings** sekcji pozwala ustawić katalogów głównych dla dzienników i danych sieci szkieletowej usług. Można dostosować te tylko podczas tworzenia klastra. Poniżej znajduje się fragment próbki w tej sekcji.

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

Firma Microsoft zaleca użycie dysku z systemem innym niż system operacyjny jako zmiennej FabricDataRoot i lokalizacji FabricLogRoot jako zapewnia niezawodność więcej względem systemu operacyjnego ulegnie awarii. Należy pamiętać, że jeśli możesz dostosować tylko główny danych, następnie głównego dziennika zostaną umieszczone jeden poziom w dół w katalogu głównym danych.

### <a name="stateful-reliable-service-settings"></a>Ustawienia usługi stanowej niezawodnej
**KtlLogger** sekcja umożliwia ustawienie globalne ustawienia konfiguracji dla usług niezawodne. Aby uzyskać więcej informacji na temat tych ustawień do odczytu [skonfigurować niezawodne usługi stanowej](service-fabric-reliable-services-configuration.md).
W poniższym przykładzie pokazano, jak zmienić dziennika transakcji udostępnionego, który jest tworzony kopii wszystkie kolekcje niezawodnych usług stanowych.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a>Dodatkowe funkcje
Aby skonfigurować dodatkowe funkcje, apiVersion powinien być skonfigurowany jako "04-2017' lub nowszej, a addonFeatures należy skonfigurować:

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a>Obsługa kontenerów
Aby włączyć obsługę kontenera systemu windows server kontenera i kontener autonomicznych klastrów funkcji hyper-v, funkcja dodatku "DnsService" musi być włączona.


## <a name="next-steps"></a>Następne kroki
Po utworzeniu pełny plik pliku ClusterConfig.JSON skonfigurowane zgodnie z autonomicznego Instalatora klastra, wykonując tego artykułu można wdrożyć klastra [tworzenia klastra usługi sieć szkieletowa autonomiczny](service-fabric-cluster-creation-for-windows-server.md) , a następnie przejdź do [ Wizualizowanie klastra za pomocą Eksploratora usługi sieć szkieletowa](service-fabric-visualizing-your-cluster.md).

