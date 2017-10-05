---
title: "Zbieranie dzienników przy użyciu diagnostyki Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak skonfigurować diagnostyki Azure do zbierania dzienników z klastra sieci szkieletowej usług działających na platformie Azure."
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
ms.openlocfilehash: 190a8a393f2e7d74a792db4efa81f94a18b02221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Zbieranie dzienników za pomocą Diagnostyki Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Jeśli korzystasz z klastra usługi sieć szkieletowa usług Azure, jest dobrym pomysłem jest zebrać dzienniki ze wszystkich węzłów w centralnej lokalizacji. Posiadanie dzienniki w centralnej lokalizacji ułatwiają analizowanie i rozwiązywanie problemów w klastrze lub problemy w aplikacji i usług działających w klastrze.

Jednym ze sposobów przekazywania i zbierania dzienników jest używane rozszerzenie diagnostyki Azure, która przekazuje dzienniki do magazynu Azure, Azure Application Insights lub usługi Azure Event Hubs. Dzienniki nie są to przydatne, bezpośrednio w magazynie lub w usłudze Event Hubs. Proces zewnętrzny można używać do odczytywania zdarzenia z magazynu i umieszczenie ich w produkcie takich jak [analizy dzienników](../log-analytics/log-analytics-service-fabric.md) lub innego rozwiązania do analizowania dziennika. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) zawiera kompleksowe dziennik wyszukiwania i analiza usługi wbudowanych.

## <a name="prerequisites"></a>Wymagania wstępne
Za pomocą tych narzędzi do wykonywania niektórych czynności w tym dokumencie:

* [Diagnostyka Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (związane z usług Azure Cloud Services, ale ma dobrej informacje i przykłady)
* [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
* [Azure PowerShell](/powershell/azure/overview)
* [Klient usługi Azure Resource Manager](https://github.com/projectkudu/ARMClient)
* [Szablon usługi Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-to-collect"></a>Dziennik źródła, które mają być zbierane
* **Dzienniki usługi sieć szkieletowa**: emitowanych przez platformę do standardowych kanałów funkcji Śledzenie zdarzeń systemu Windows () i EventSource. Dzienniki może być jednym z kilku typów:
  * Zdarzenia operacyjne: dzienniki dla operacji, które wykonuje platformy sieć szkieletowa usług. Tworzenie aplikacji i usług, zmian stanu węzła i informacje o uaktualnianiu przykładami.
  * [Reliable Actors zdarzeń modelu programowania](service-fabric-reliable-actors-diagnostics.md)
  * [Niezawodne usługi zdarzeń modelu programowania](service-fabric-reliable-services-diagnostics.md)
* **Zdarzenia aplikacji**: zdarzenia wysyłanego z kodu z usługą i zapisany przy użyciu Pomocnika EventSource — klasa w szablony programu Visual Studio. Aby uzyskać więcej informacji na temat zapisywania dzienników z aplikacji, zobacz [monitora i diagnozowania usług w Instalatorze programowanie komputera lokalnego](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-the-diagnostics-extension"></a>Wdrażanie rozszerzenia diagnostyki
Pierwszym etapem zbierania dzienników jest wdrażanie rozszerzenia diagnostyki na wszystkich maszynach wirtualnych w klastrze usługi sieć szkieletowa usług. Rozszerzenie diagnostycznych zbiera dzienniki na każdej maszynie Wirtualnej i przekazuje je do konta magazynu, który określisz. Kroki zależą od nieco przy użyciu portalu Azure lub usługi Azure Resource Manager. Kroki również różnić w zależności od tego, czy wdrożenie jest częścią tworzenia klastra lub jest dla klastra, który już istnieje. Oto kroki dla każdego scenariusza.

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-through-the-portal"></a>Wdrażanie rozszerzenia diagnostyki w ramach tworzenia klastra za pośrednictwem portalu
Aby wdrożyć rozszerzenie diagnostyki maszyny wirtualne w klastrze, w ramach tworzenia klastra, należy użyć panelu Ustawienia diagnostyki pokazano na poniższej ilustracji. Aby włączyć zbieranie zdarzeń Reliable Actors lub niezawodne usługi, upewnij się, że diagnostyki jest ustawiona na **na** (ustawienie domyślne). Po utworzeniu klastra, nie możesz zmienić te ustawienia przy użyciu portalu.

![Azure ustawień diagnostycznych w portalu do tworzenia klastra](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

Zespół pomocy technicznej platformy Azure *wymaga* obsługuje dzienniki, aby ułatwić żądań pomocy technicznej utworzonych przez Ciebie. Te dzienniki są zbierane w czasie rzeczywistym i są przechowywane w jednym z kont magazynu utworzonych w grupie zasobów. Ustawienia diagnostyki skonfigurować zdarzenia na poziomie aplikacji. Te zdarzenia zawierają [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) zdarzenia, [niezawodne usługi](service-fabric-reliable-services-diagnostics.md) zdarzenia i niektóre zdarzenia platformy Service Fabric systemowe mają być przechowywane w usłudze Azure Storage.

Produkty, takie jak [Elasticsearch](https://www.elastic.co/guide/index.html) lub własnego procesu można pobrać zdarzenia z konta magazynu. Nie ma można filtrować lub czyścić zdarzenia, które są wysyłane do tabeli. Nie można wdrożyć proces Usuń zdarzenia z tabeli, będzie nadal wzrostu tabeli.

Podczas tworzenia klastra przy użyciu portalu, zalecamy pobranie szablonu **przed kliknięciem przycisku OK** do utworzenia klastra. Aby uzyskać więcej informacji, zapoznaj się [Konfigurowanie klastra sieci szkieletowej usług za pomocą szablonu usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Musisz szablonu, aby wprowadzić zmiany później, ponieważ nie można wprowadzić kilka zmian za pomocą portalu.

Możesz wyeksportować szablony z portalu, za pomocą poniższych kroków. Jednak te szablony może być trudne do użycia, ponieważ mogą one mieć wartości null, których brakuje wymaganych informacji.

1. Otwórz grupie zasobów.
2. Wybierz **ustawienia** Aby wyświetlić panel ustawień.
3. Wybierz **wdrożeń** Aby wyświetlić panel historii wdrożenia.
4. Wybierz wdrożenie, aby wyświetlić szczegóły wdrożenia.
5. Wybierz **Eksportuj szablon** Aby wyświetlić panel szablonu.
6. Wybierz **Zapisz do pliku** można wyeksportować plik zip zawierający szablonu, parametrów i pliki programu PowerShell.

Po wyeksportowaniu plików należy wprowadzić zmiany. Przeprowadź edycję pliku parameters.JSON następującym kodem, a następnie usuń **adminPassword** elementu. To spowoduje, że monit o hasło po uruchomieniu skryptu wdrażania. Po uruchomieniu skryptu wdrażania, trzeba będzie naprawić zerowe wartości parametrów.

Aby użyć pobranego szablonu, aby zaktualizować konfigurację:

1. Wyodrębnij zawartość do folderu na komputerze lokalnym.
2. Zmodyfikuj zawartość w celu uwzględnienia nowej konfiguracji.
3. Uruchom program PowerShell i przejdź do folderu, w którym została rozpakowana zawartość.
4. Uruchom **deploy.ps1** i podaj identyfikator subskrypcji, nazwa grupy zasobów (Użyj takie same nazwy, można zaktualizować konfiguracji) i nazwę unikatowego wdrożenia.

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a>Wdrażanie rozszerzenia diagnostyki w ramach tworzenia klastra przy użyciu usługi Azure Resource Manager
Aby utworzyć klaster przy użyciu usługi Resource Manager, należy dodać konfiguracji diagnostyki JSON do szablonu usługi Resource Manager pełne klastra przed utworzeniem klastra. Udostępniamy przykładowy szablon Menedżera zasobów klastra maszyny Wirtualnej pięciu o konfiguracji diagnostyki dodana jako część nasze przykłady szablonu usługi Resource Manager. Można to sprawdzić w tej lokalizacji w galerii Azure przykładów: [pięcioma węzłami klastra z przykładowy szablon Menedżera zasobów diagnostyki](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).

Aby wyświetlić ustawienia diagnostyki w szablonie usługi Resource Manager, otwórz plik azuredeploy.json i wyszukaj **IaaSDiagnostics**. Aby utworzyć klaster przy użyciu tego szablonu, wybierz **wdrażanie na platformie Azure** przycisk dostępny w poprzedniej konsolidacji.

Alternatywnie można pobrać przykładowych Menedżera zasobów, wprowadzić zmiany i utworzyć klaster przy użyciu szablonu modyfikacji, przy użyciu `New-AzureRmResourceGroupDeployment` polecenie w oknie programu PowerShell systemu Azure. Zobacz poniższy kod dla parametrów, które przekazujesz do polecenia. Aby uzyskać szczegółowe informacje na temat wdrażania grupy zasobów za pomocą programu PowerShell, zobacz artykuł [wdrażanie grupy zasobów przy użyciu szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-the-diagnostics-extension-to-an-existing-cluster"></a>Wdrażanie rozszerzenia diagnostyki do istniejącego klastra
Jeśli masz istniejący klaster nie ma wdrożonych diagnostyki lub jeśli chcesz zmodyfikować istniejącą konfigurację, można dodać lub zaktualizować. Zmodyfikuj szablonu usługi Resource Manager, który służy do tworzenia istniejącego klastra lub pobrać szablonu z portalu zgodnie z wcześniejszym opisem. Zmodyfikuj plik template.json, wykonując następujące zadania.

Dodaj nowy zasób magazynu do szablonu przez dodanie do sekcji zasobów.

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

 Następnie dodaj do sekcji Parametry zaraz po definicji konta magazynu, między `supportLogStorageAccountName` i `vmNodeType0Name`. Zastąp tekst zastępczy *nazwy konta magazynu tu* z nazwą konta magazynu.

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for the application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for the storage account that contains application diagnostics data from the cluster"
      }
    },
```
Następnie zaktualizuj `VirtualMachineProfile` sekcji pliku template.json przez dodanie poniższego kodu w tablicy rozszerzeń. Pamiętaj dodać przecinek na początku lub na końcu, w zależności od tego, gdzie jest wstawiana.

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

Po zmodyfikowaniu pliku template.json zgodnie z opisem, ponownie opublikować szablonu usługi Resource Manager. Jeśli szablon został wyeksportowany, uruchamiania pliku deploy.ps1 je opublikuje szablonu. Po wdrożeniu, upewnij się, że **ProvisioningState** jest **zakończyło się pomyślnie**.

## <a name="update-diagnostics-to-collect-health-and-load-events"></a>Zaktualizuj diagnostyki do zbierania kondycji i załadować zdarzenia

Począwszy od wersji 5.4 sieci szkieletowej usług kondycji i obciążenia metryki zdarzenia są dostępne dla kolekcji. Te zdarzenia odzwierciedlają zdarzeń generowanych przez system lub kodu za pomocą kondycji lub załadować API raportowania, takie jak [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) lub [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx). Dzięki temu agregowanie i wyświetlanie stanu systemu wraz z upływem czasu oraz alerty na podstawie kondycji lub obciążenia zdarzeń. Aby wyświetlić te zdarzenia w Podglądzie zdarzeń diagnostycznych programu Visual Studio Dodaj "Microsoft-ServiceFabric:4:0x4000000000000008" do listy dostawców ETW.

Aby zbierać zdarzenia, zmodyfikuj szablon usługi resource manager do uwzględnienia

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

## <a name="update-diagnostics-to-collect-and-upload-logs-from-new-eventsource-channels"></a>Zaktualizuj diagnostyki do gromadzenia i przekazywania dzienników z nowych kanałów źródła zdarzeń
Aby zaktualizować diagnostykę, aby zbieranie dzienników z nowego kanałów źródła zdarzeń, które reprezentują nowej aplikacji, które zamierzasz wdrożyć, wykonaj te same czynności co w [poprzedniej sekcji](#deploywadarm) ustawień diagnostycznych dla istniejącego klastra.

Zaktualizuj `EtwEventSourceProviderConfiguration` sekcji w pliku template.json można dodawać nowych kanałów EventSource przed zastosowaniem konfiguracji aktualizacji przy użyciu `New-AzureRmResourceGroupDeployment` polecenia programu PowerShell. Nazwa źródła zdarzeń jest zdefiniowany jako części kodu w pliku ServiceEventSource.cs generowanych przez program Visual Studio.

Na przykład jeśli źródło zdarzenia jest o nazwie Mój Eventsource, Dodaj następujący kod, aby umieścić zdarzenia Moje Eventsource w tabeli o nazwie MyDestinationTableName.

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

Aby zebrać liczników wydajności lub dzienniki zdarzeń, należy modyfikować szablonu usługi Resource Manager za pomocą przykłady podane w [Utwórz maszynę wirtualną systemu Windows z monitorowania i diagnostyki za pomocą szablonu usługi Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Następnie należy ponownie opublikować szablonu usługi Resource Manager.

## <a name="next-steps"></a>Następne kroki
Aby bardziej szczegółowo zrozumieć, jakie zdarzenia należy szukać podczas rozwiązywania problemów, zobacz zdarzeń diagnostycznych wysyłanego do [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) i [niezawodne usługi](service-fabric-reliable-services-diagnostics.md).

## <a name="related-articles"></a>Pokrewne artykuły:
* [Dowiedz się, jak zbierania liczników wydajności lub dzienniki przy użyciu rozszerzenia diagnostyki](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Rozwiązania sieci szkieletowej usług analizy dzienników](../log-analytics/log-analytics-service-fabric.md)

