---
title: "Usługi sieci szkieletowej zdarzeń agregacji z systemu Windows Azure Diagnostics aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat agregowania i zbierania zdarzeń przy użyciu WAD monitorowania i diagnostyki klastrów sieci szkieletowej usług Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 4827ce66620e61c5b4a8682db55952333113188a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a>Agregacja zdarzeń i kolekcji przy użyciu systemu Windows Azure Diagnostics
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Jeśli korzystasz z klastra usługi sieć szkieletowa usług Azure, jest dobrze toocollect hello dzienniki ze wszystkich węzłów hello w centralnej lokalizacji. O dzienniki hello w centralnej lokalizacji ułatwiają analizowanie i rozwiązywanie problemów w klastrze, lub problemy w hello aplikacje i usługi działające w klastrze.

Zbieranie dzienników i tooupload jedną z metod jest rozszerzenie systemu Windows Azure Diagnostics (WAD) hello toouse, który przekazuje dzienniki tooAzure magazynu, a także ma hello opcja toosend dzienniki tooAzure usługi Application Insights lub Event Hubs. Można również użyć procesu zewnętrznego tooread hello zdarzenia z magazynu i umieścić w produkcie platformy analizy, takich jak [analizy dzienników OMS](../log-analytics/log-analytics-service-fabric.md) lub innego rozwiązania do analizowania dziennika.

## <a name="prerequisites"></a>Wymagania wstępne
Te narzędzia są używane tooperform niektóre operacje hello w tym dokumencie:

* [Diagnostyka Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (dotyczących tooAzure usługi w chmurze, lecz jest dobrym informacje i przykłady)
* [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Klient usługi Azure Resource Manager](https://github.com/projectkudu/ARMClient)
* [Szablon usługi Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a>Źródła dziennika i zdarzenie

### <a name="service-fabric-platform-events"></a>Zdarzenia platformy Service Fabric
Zgodnie z opisem w [w tym artykule](service-fabric-diagnostics-event-generation-infra.md), Service Fabric konfiguruje możesz z kilku kanałów rejestrowania poza pole, z którym hello następujących kanałów łatwo są skonfigurowane przy użyciu WAD toosend monitorowania i diagnostyki danych tooa tabeli magazynu lub w innym miejscu:
  * Zdarzenia operacyjne: operacje wyższego poziomu, które hello wykonuje platformy sieci szkieletowej usług. Tworzenie aplikacji i usług, zmian stanu węzła i informacje o uaktualnianiu przykładami. Te są emitowane jako dzienniki zdarzeń śledzenia dla systemu Windows (ETW)
  * [Reliable Actors zdarzeń modelu programowania](service-fabric-reliable-actors-diagnostics.md)
  * [Niezawodne usługi zdarzeń modelu programowania](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a>Zdarzenia aplikacji
 Zdarzenia wysyłanego z Twojej aplikacji i usług kodu i zapisany przy użyciu klasy pomocy EventSource hello postanowień hello szablony programu Visual Studio. Aby uzyskać więcej informacji dotyczących sposobu toowrite źródła zdarzeń logowania z aplikacji, zobacz [monitora i diagnozowania usług w Instalatorze programowanie komputera lokalnego](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Wdrażanie rozszerzenia diagnostyki hello
pierwszym krokiem Hello zbierania dzienników jest rozszerzeniem diagnostyki hello toodeploy na poszczególnych maszyn wirtualnych hello w klastrze usługi sieć szkieletowa hello. Hello rozszerzenia diagnostyki zbiera dzienniki na każdej maszynie Wirtualnej i przekazuje je toohello konta magazynu, który określisz. kroki Hello zależą od nieco przy użyciu hello portalu Azure lub usługi Azure Resource Manager. kroki Hello również różnić w zależności od czy wdrożenia hello jest częścią tworzenia klastra lub dla klastra, który już istnieje. Przyjrzyjmy się hello kroki dla każdego scenariusza.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a>Wdrażanie rozszerzenia diagnostyki hello w ramach tworzenia klastra za pośrednictwem portalu Azure
toodeploy hello diagnostyki rozszerzenia toohello maszyn wirtualnych w klastrze hello w ramach tworzenia klastra, użyj panelu Ustawienia diagnostyki hello pokazano poniżej hello obrazu — upewnij się, że diagnostyki ustawiono zbyt**na** (hello ustawienie domyślne) . Po utworzeniu klastra hello, nie możesz zmienić te ustawienia przy użyciu portalu hello.

![Azure ustawień diagnostyki w portalu hello tworzenia klastra](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

Podczas tworzenia klastra przy użyciu portalu hello, zalecamy pobranie szablonu hello **przed kliknięciem przycisku OK** toocreate hello klastra. Aby uzyskać więcej informacji, zobacz zbyt[Konfigurowanie klastra sieci szkieletowej usług za pomocą szablonu usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Zmiany toomake szablonu hello będą potrzebne później, ponieważ nie można wprowadzić kilka zmian przy użyciu portalu hello.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Wdrażanie rozszerzenia diagnostyki hello w ramach tworzenia klastra przy użyciu usługi Azure Resource Manager
toocreate klastra za pomocą Menedżera zasobów, należy tooadd hello diagnostyki konfiguracji szablonu JSON w toohello pełne klastra Menedżera zasobów przed utworzeniem klastra hello. Udostępniamy przykładowy szablon Menedżera zasobów klastra maszyny Wirtualnej pięciu o konfiguracji diagnostyki dodane tooit jako część nasze przykłady szablonu usługi Resource Manager. Można to sprawdzić w tej lokalizacji w galerii Azure przykładów hello: [pięcioma węzłami klastra z przykładowy szablon Menedżera zasobów diagnostyki](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).

ustawienia diagnostyki hello toosee hello szablonu usługi Resource Manager, hello Otwórz plik azuredeploy.json i wyszukaj **IaaSDiagnostics**. toocreate klastra przy użyciu tego szablonu, wybierz opcję hello **wdrażanie tooAzure** przycisk dostępne pod adresem hello poprzedniej konsolidacji.

Alternatywnie można pobrać hello próbki Menedżera zasobów, wprowadzić zmiany tooit i utworzyć klaster przy użyciu szablonu modyfikacji hello przy użyciu hello `New-AzureRmResourceGroupDeployment` polecenie w oknie programu PowerShell systemu Azure. Zobacz hello następującego kodu dla parametrów hello, które przekazujesz w poleceniu toohello. Aby uzyskać szczegółowe informacje dotyczące sposobu toodeploy zasób grupy przy użyciu programu PowerShell, zobacz artykuł hello [wdrażanie grupy zasobów z szablonem usługi Azure Resource Manager hello](../azure-resource-manager/resource-group-template-deploy.md).

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a>Wdrażanie hello diagnostyki rozszerzenia tooan istniejącego klastra
Jeśli masz istniejący klaster nie ma wdrożonych diagnostyki lub jeśli chcesz toomodify istniejącej konfiguracji, można dodać lub zaktualizować. Zmodyfikuj szablon Menedżera zasobów hello, która jest używana toocreate hello istniejącego klastra lub pobrać hello szablonu z portalu hello zgodnie z wcześniejszym opisem. Zmodyfikuj plik template.json hello, wykonując następujące zadania hello.

Dodaj nowy szablon toohello zasobów magazynu przez dodanie toohello sekcja zasobów.

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 Następnie dodaj parametry toohello sekcji zaraz po definicji konta magazynu hello, między `supportLogStorageAccountName` i `vmNodeType0Name`. Zastąp tekst zastępczy hello *nazwy konta magazynu tu* o nazwie hello hello konta magazynu.

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
Następnie zaktualizuj hello `VirtualMachineProfile` sekcji pliku template.json hello przez dodanie hello następującego kodu w ramach hello tablica rozszerzeń. Należy się tooadd przecinkami hello początek lub koniec hello, w zależności od tego, gdzie jest wstawiana.

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

Po zmodyfikowaniu pliku template.json hello zgodnie z opisem ponownie opublikować hello szablonu usługi Resource Manager. Jeśli został wyeksportowany szablon hello, uruchamianie pliku deploy.ps1 hello je opublikuje hello szablonu. Po wdrożeniu, upewnij się, że **ProvisioningState** jest **zakończyło się pomyślnie**.

## <a name="collect-health-and-load-events"></a>Zbieranie kondycji i załadować zdarzenia

Począwszy od wersji platformy Service Fabric hello 5.4 metryki zdarzenia kondycji i obciążenia są dostępne dla kolekcji. Te zdarzenia odzwierciedlają zdarzeń generowanych przez hello system lub kodu za pomocą kondycji hello lub załadować API raportowania, takie jak [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) lub [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Dzięki temu agregowanie i wyświetlanie stanu systemu wraz z upływem czasu oraz alerty na podstawie kondycji lub obciążenia zdarzeń. tooview dodać tych zdarzeń w Podglądzie zdarzeń diagnostycznych programu Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000008" toohello listy dostawców ETW.

zdarzenia hello toocollect, zmodyfikuj tooinclude szablonu usługi Resource Manager hello

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="collect-reverse-proxy-events"></a>Zbieranie zdarzeń zwrotnego serwera proxy

Począwszy od wersji hello 5.7 usługi sieci szkieletowej, [odwrotny serwer proxy](service-fabric-reverseproxy.md) zdarzenia są dostępne dla kolekcji.
Zwrotny serwer proxy emituje zdarzenia do dwa kanały, jeden błąd zawierający zdarzenia w czasie wykonywania odbicia błędów przetwarzania żądań i hello drugi zawierający pełne zdarzenia dotyczące wszystkich żądań hello przetwarzane w hello zwrotnego serwera proxy. 

1. Zbieranie zdarzeń błędu: tooview dodać tych zdarzeń w Podglądzie zdarzeń diagnostycznych programu Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000010" toohello listy dostawców ETW.
zdarzenia hello toocollect z klastrami platformy Azure, zmodyfikuj tooinclude szablonu usługi Resource Manager hello

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. Zbieranie wszystkie żądania przetwarzania zdarzeń: W programie Visual Studio diagnostycznych podglądu zdarzeń wpisu hello ServiceFabric programu Microsoft update w hello zbyt listy dostawców ETW "Microsoft-ServiceFabric:4:0x4000000000000020".
W przypadku klastrów sieci szkieletowej usług Azure zmodyfikuj tooinclude szablon Menedżera zasobów hello

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> To zbiera cały ruch przez zwrotny serwer proxy hello i może wymagać pojemności zaleca się toojudiciously Włącz zbieranie zdarzeń z tego kanału.

W przypadku klastrów sieci szkieletowej usług Azure hello zdarzenia ze wszystkich węzłów hello są gromadzone i zagregowane w hello SystemEventTable.
Szczegółowe Rozwiązywanie problemów z hello zdarzeń zwrotnego serwera proxy, zobacz hello [przewodnik diagnostyki zwrotnego serwera proxy](service-fabric-reverse-proxy-diagnostics.md).

## <a name="collect-from-new-eventsource-channels"></a>Zbierać z nowych kanałów źródła zdarzeń

Dzienniki toocollect diagnostyki tooupdate nowych kanałów EventSource reprezentujących nowej aplikacji, który zajmie około toodeploy, wykonuje hello te same czynności jak opisano wcześniej hello ustawienia diagnostyki dla istniejącego klastra.

Zaktualizuj hello `EtwEventSourceProviderConfiguration` sekcji hello template.json wpisy tooadd hello nowych kanałów EventSource przed zastosowaniem konfiguracji hello aktualizacji przy użyciu hello `New-AzureRmResourceGroupDeployment` polecenia programu PowerShell. Nazwa Hello źródła zdarzeń hello jest zdefiniowany jako części kodu w pliku generowanych przez program Visual Studio ServiceEventSource.cs hello.

Na przykład źródło zdarzenia jest o nazwie Mój Eventsource, dodać hello następujące zdarzenia hello tooplace kodu z Moje Eventsource do tabeli o nazwie MyDestinationTableName.

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

liczniki wydajności toocollect lub dzienniki zdarzeń, modyfikować szablonu usługi Resource Manager hello za pomocą hello przykłady podane w [Utwórz maszynę wirtualną systemu Windows z monitorowania i diagnostyki za pomocą szablonu usługi Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Następnie należy ponownie opublikować hello szablonu usługi Resource Manager.

## <a name="collect-performance-counters"></a>Zebrać liczników wydajności

metryki wydajności toocollect z klastra, Dodaj tooyour liczniki wydajności hello "WadCfg > DiagnosticMonitorConfiguration" w szablonie usługi Resource Manager powitania dla klastra. Zobacz [liczniki wydajności sieci szkieletowej usług](service-fabric-diagnostics-event-generation-perf.md) dla liczników wydajności zalecamy zbierania.

Na przykład, w tym miejscu możemy ustawić jeden licznik wydajności, próbkowany co 15 s (można zmienić tę wartość i sposób hello format "PT\<czasu >\<jednostki >", na przykład PT3M czy przykładowe co trzy minut), a przekazywane toohello Tabela magazynu odpowiednie co minutę.

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
Jeśli używasz zbiornika usługi Application Insights zgodnie z opisem w poniższej sekcji hello i mają te metryki tooshow się w usłudze Application Insights, upewnij się, że nazwa obiektu sink hello tooadd w sekcji "sink" hello, jak pokazano powyżej. Ponadto należy rozważyć utworzenie toosend osobnej tabeli liczniki wydajności, więc ich nie tłumu limit hello dane pochodzące z hello innych kanałów rejestrowania została włączona.


## <a name="send-logs-tooapplication-insights"></a>Wyślij dzienniki tooApplication Insights

Wysyłanie tooApplication danych monitorowania i diagnostyki Insights (AI) może zostać wykonane jako część konfiguracji WAD hello. Jeśli zdecydujesz toouse AI analizy zdarzeń i wizualizacji odczytu [analiza zdarzeń i wizualizacji z usługą Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset się zbiornika AI jako część programu "WadCfg".

## <a name="next-steps"></a>Następne kroki

Po diagnostyki Azure zostały prawidłowo skonfigurowane, zostanie wyświetlona dane w tabelach magazynu z hello ETW i dzienniki EventSource. Jeśli wybierzesz toouse OMS Kibana, lub wszelkie inne dane analizy i wizualizacji platformy, które nie skonfigurowano bezpośrednio w szablonie usługi Resource Manager hello, upewnij się, że tooset się hello platforma tooread Twojego wybór hello danych z tych tabel do przechowywania. W ten sposób dla OMS jest względnie proste i zostało wyjaśnione w dokumencie [zdarzeń i dziennika analizy za pośrednictwem OMS](service-fabric-diagnostics-event-analysis-oms.md). Usługa Application Insights jest nieco szczególnych przypadkach, w tym sensie, ponieważ może być skonfigurowana jako część konfiguracji rozszerzenia diagnostyki hello, dlatego można znaleźć toohello [odpowiedniego artykułu](service-fabric-diagnostics-event-analysis-appinsights.md) po wybraniu toouse AI.

>[!NOTE]
>Nie ma żadnych sposób toofilter lub Oczyść hello zdarzenia, które są wysyłane toohello tabeli. Jeśli nie implementują zdarzenia tooremove procesu z tabeli hello, hello tabeli będzie toogrow. Obecnie jest przykładem usługi pielęgnacji danych działa w hello [próbki programu alarmowego](https://github.com/Azure-Samples/service-fabric-watchdog-service), i zaleca zapisu jedną dla siebie również, chyba że powody dla Ciebie dzienniki toostore poza przedział czasu dnia 30 lub 90.

* [Dowiedz się, jak toocollect liczników wydajności lub dzienniki przy użyciu hello rozszerzenia diagnostyki](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Analiza zdarzeń i wizualizacji z usługą Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)
* [Analiza zdarzeń i wizualizacji z OMS](service-fabric-diagnostics-event-analysis-oms.md)