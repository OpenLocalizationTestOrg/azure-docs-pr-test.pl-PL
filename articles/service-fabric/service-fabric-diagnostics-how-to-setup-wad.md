---
title: "Dzienniki aaaCollect za pomocą diagnostyki Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób rejestrowania tooset się toocollect diagnostyki Azure z klastra usługi sieć szkieletowa usług działających na platformie Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Zbieranie dzienników za pomocą Diagnostyki Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Jeśli korzystasz z klastra usługi sieć szkieletowa usług Azure, jest dobrze toocollect hello dzienniki ze wszystkich węzłów hello w centralnej lokalizacji. O dzienniki hello w centralnej lokalizacji ułatwiają analizowanie i rozwiązywanie problemów w klastrze, lub problemy w hello aplikacje i usługi działające w klastrze.

Jednym ze sposobów tooupload i zbieranie dzienników jest toouse hello Azure Diagnostics rozszerzenia, które przekazywania dzienników tooAzure magazynu Azure Application Insights i usługi Azure Event Hubs. Witaj dzienniki nie są to przydatne, bezpośrednio w magazynie lub w usłudze Event Hubs. Można jednak użyć procesu zewnętrznego tooread hello zdarzenia z magazynu i umieszczenie ich w produkcie takich jak [analizy dzienników](../log-analytics/log-analytics-service-fabric.md) lub innego rozwiązania do analizowania dziennika. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) zawiera kompleksowe dziennik wyszukiwania i analiza usługi wbudowanych.

## <a name="prerequisites"></a>Wymagania wstępne
Użyj tych narzędzi tooperform niektóre operacje hello w tym dokumencie:

* [Diagnostyka Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (dotyczących tooAzure usługi w chmurze, lecz jest dobrym informacje i przykłady)
* [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Klient usługi Azure Resource Manager](https://github.com/projectkudu/ARMClient)
* [Szablon usługi Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a>Dziennik źródeł rozważ toocollect
* **Dzienniki usługi sieć szkieletowa**: wysyłanego z hello platformy toostandard funkcji Śledzenie zdarzeń systemu Windows () i EventSource kanałów. Dzienniki może być jednym z kilku typów:
  * Zdarzenia operacyjne: dzienniki dla operacji, które hello wykonuje platformy sieci szkieletowej usług. Tworzenie aplikacji i usług, zmian stanu węzła i informacje o uaktualnianiu przykładami.
  * [Reliable Actors zdarzeń modelu programowania](service-fabric-reliable-actors-diagnostics.md)
  * [Niezawodne usługi zdarzeń modelu programowania](service-fabric-reliable-services-diagnostics.md)
* **Zdarzenia aplikacji**: zdarzenia wysyłanego z kodu z usługą i zapisany przy użyciu klasy pomocy EventSource hello w hello szablony programu Visual Studio. Aby uzyskać więcej informacji dotyczących sposobu toowrite logowania z aplikacji, zobacz [monitora i diagnozowania usług w Instalatorze programowanie komputera lokalnego](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Wdrażanie rozszerzenia diagnostyki hello
pierwszym krokiem Hello zbierania dzienników jest rozszerzeniem diagnostyki hello toodeploy na poszczególnych maszyn wirtualnych hello w klastrze usługi sieć szkieletowa hello. Hello rozszerzenia diagnostyki zbiera dzienniki na każdej maszynie Wirtualnej i przekazuje je toohello konta magazynu, który określisz. kroki Hello zależą od nieco przy użyciu hello portalu Azure lub usługi Azure Resource Manager. kroki Hello również różnić w zależności od czy wdrożenia hello jest częścią tworzenia klastra lub dla klastra, który już istnieje. Przyjrzyjmy się hello kroki dla każdego scenariusza.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a>Wdrażanie rozszerzenia diagnostyki hello w ramach tworzenia klastra za pośrednictwem portalu hello
toodeploy hello diagnostyki rozszerzenia toohello maszyn wirtualnych w klastrze hello w ramach tworzenia klastra, możesz użyć panel ustawień diagnostyki hello pokazano powitania po obrazu. tooenable Reliable Actors lub niezawodne usługi zbierania zdarzeń, sprawdź, czy diagnostyki jest ustawiony za**na** (hello ustawienie domyślne). Po utworzeniu klastra hello, nie możesz zmienić te ustawienia przy użyciu portalu hello.

![Azure ustawień diagnostyki w portalu hello tworzenia klastra](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

Witaj zespołu pomocy technicznej platformy Azure *wymaga* Obsługa dzienniki toohelp Rozwiąż wszelkie tworzenia żądania obsługi. Te dzienniki są zbierane w czasie rzeczywistym i są przechowywane w jednym z kont magazynu hello utworzonych w grupie zasobów hello. ustawienia diagnostyki Hello skonfigurować zdarzenia na poziomie aplikacji. Te zdarzenia zawierają [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) zdarzenia, [niezawodne usługi](service-fabric-reliable-services-diagnostics.md) zdarzenia, a niektóre zdarzenia toobe sieci szkieletowej usług poziom systemu przechowywane w usłudze Azure Storage.

Produkty, takie jak [Elasticsearch](https://www.elastic.co/guide/index.html) lub własnego procesu można uzyskać hello zdarzenia z hello konta magazynu. Nie ma żadnych sposób toofilter lub Oczyść hello zdarzenia, które są wysyłane toohello tabeli. Jeśli nie implementują zdarzenia tooremove procesu z tabeli hello, hello tabeli będzie toogrow.

Podczas tworzenia klastra przy użyciu portalu hello, zalecamy pobranie szablonu hello **przed kliknięciem przycisku OK** toocreate hello klastra. Aby uzyskać więcej informacji, zobacz zbyt[Konfigurowanie klastra sieci szkieletowej usług za pomocą szablonu usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Zmiany toomake szablonu hello będą potrzebne później, ponieważ nie można wprowadzić kilka zmian przy użyciu portalu hello.

Możesz wyeksportować szablony z portalu hello przy użyciu hello następujące kroki. Jednak te szablony może być trudniejsze toouse, ponieważ mogą one mieć wartości null, których brakuje wymaganych informacji.

1. Otwórz grupie zasobów.
2. Wybierz **ustawienia** toodisplay hello ustawienia panelu.
3. Wybierz **wdrożeń** toodisplay hello wdrożenia historii panelu.
4. Wybierz szczegóły hello toodisplay wdrożenia hello wdrożenia.
5. Wybierz **Eksportuj szablon** toodisplay hello szablonu panelu.
6. Wybierz **zapisać toofile** tooexport plik zip zawierający hello szablonu, parametrów i pliki programu PowerShell.

Po wyeksportowaniu hello plików należy toomake modyfikację. Edytuj plik parameters.JSON następującym kodem hello i Usuń hello **adminPassword** elementu. Spowoduje to monit o hasło powitania po uruchomieniu skryptu wdrażania hello. Po uruchomieniu skryptu wdrażania hello może mieć wartości null parametrów toofix.

Witaj toouse pobrać tooupdate szablonu konfiguracji:

1. Wyodrębnij hello zawartość tooa folderu na komputerze lokalnym.
2. Zmodyfikuj hello zawartość tooreflect hello nowej konfiguracji.
3. Uruchom program PowerShell i zmień toohello folder, w którym wyodrębniono zawartość hello.
4. Uruchom **deploy.ps1** i podaj identyfikator subskrypcji hello, nazwa grupy zasobów hello (Użyj hello sama konfiguracja hello tooupdate nazwy) oraz nazwę unikatowego wdrożenia.

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Wdrażanie rozszerzenia diagnostyki hello w ramach tworzenia klastra przy użyciu usługi Azure Resource Manager
toocreate klastra za pomocą Menedżera zasobów, należy tooadd hello diagnostyki konfiguracji szablonu JSON w toohello pełne klastra Menedżera zasobów przed utworzeniem klastra hello. Udostępniamy przykładowy szablon Menedżera zasobów klastra maszyny Wirtualnej pięciu o konfiguracji diagnostyki dodane tooit jako część nasze przykłady szablonu usługi Resource Manager. Można to sprawdzić w tej lokalizacji w galerii Azure przykładów hello: [pięcioma węzłami klastra z przykładowy szablon Menedżera zasobów diagnostyki](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).

ustawienia diagnostyki hello toosee hello szablonu usługi Resource Manager, hello Otwórz plik azuredeploy.json i wyszukaj **IaaSDiagnostics**. toocreate klastra przy użyciu tego szablonu, wybierz opcję hello **wdrażanie tooAzure** przycisk dostępne pod adresem hello poprzedniej konsolidacji.

Alternatywnie można pobrać hello próbki Menedżera zasobów, wprowadzić zmiany tooit i utworzyć klaster przy użyciu szablonu modyfikacji hello przy użyciu hello `New-AzureRmResourceGroupDeployment` polecenie w oknie programu PowerShell systemu Azure. Zobacz hello następującego kodu dla parametrów hello, które przekazujesz w poleceniu toohello. Aby uzyskać szczegółowe informacje dotyczące sposobu toodeploy zasób grupy przy użyciu programu PowerShell, zobacz artykuł hello [wdrażanie grupy zasobów z szablonem usługi Azure Resource Manager hello](../azure-resource-manager/resource-group-template-deploy.md).

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

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

## <a name="update-diagnostics-toocollect-health-and-load-events"></a>Aktualizowanie zdarzenia kondycji i obciążenia toocollect diagnostyki

Począwszy od wersji platformy Service Fabric hello 5.4 metryki zdarzenia kondycji i obciążenia są dostępne dla kolekcji. Te zdarzenia odzwierciedlają zdarzeń generowanych przez hello system lub kodu za pomocą kondycji hello lub załadować API raportowania, takie jak [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) lub [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Dzięki temu agregowanie i wyświetlanie stanu systemu wraz z upływem czasu oraz alerty na podstawie kondycji lub obciążenia zdarzeń. tooview dodać tych zdarzeń w Podglądzie zdarzeń diagnostycznych programu Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000008" toohello listy dostawców ETW.

zdarzenia hello toocollect, zmodyfikuj tooinclude szablon Menedżera zasobów hello

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

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a>Zaktualizuj toocollect diagnostyki i przekazywania dzienników z nowych kanałów źródła zdarzeń
Dzienniki toocollect diagnostyki tooupdate nowych kanałów EventSource reprezentujących nowej aplikacji, który zajmie około toodeploy, wykonaj kroki takie same jak hello hello [poprzedniej sekcji](#deploywadarm) ustawień diagnostycznych dla istniejącej klaster.

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

## <a name="next-steps"></a>Następne kroki
toounderstand bardziej szczegółowo jakie zdarzenia należy szukać podczas rozwiązywania problemów, zobacz hello zdarzeń diagnostycznych wysyłanego do [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) i [niezawodne usługi](service-fabric-reliable-services-diagnostics.md).

## <a name="related-articles"></a>Pokrewne artykuły:
* [Dowiedz się, jak toocollect liczników wydajności lub dzienniki przy użyciu hello rozszerzenia diagnostyki](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Rozwiązania sieci szkieletowej usług analizy dzienników](../log-analytics/log-analytics-service-fabric.md)

