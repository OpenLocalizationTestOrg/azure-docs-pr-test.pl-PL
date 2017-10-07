---
title: aaaAdd monitorowania i diagnostyki tooan maszyny wirtualnej platformy Azure | Dokumentacja firmy Microsoft
description: "Toocreate szablon Menedżera zasobów platformy Azure nowej maszyny wirtualnej systemu Windows za pomocą diagnostyki Azure rozszerzenia."
services: virtual-machines-windows
documentationcenter: 
author: sbtron
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8cde8fe7-977b-43d2-be74-ad46dc946058
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: saurabh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d8a831421a0f9d38c09d51cf8c2e6dff913c77ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-monitoring-and-diagnostics-with-a-windows-vm-and-azure-resource-manager-templates"></a>Użyj monitorowania i diagnostyki z szablonów maszyny Wirtualnej systemu Windows i usługi Azure Resource Manager
Hello rozszerzenia diagnostyki Azure udostępnia hello monitorowania i diagnostyki możliwości systemu Windows na podstawie maszyny wirtualnej platformy Azure. Te możliwości w maszynie wirtualnej hello można włączyć w tym rozszerzenia hello jako część hello szablonu usługi azure resource manager. Zobacz [tworzenia szablonów usługi Azure Resource Manager z rozszerzeń maszyny Wirtualnej](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) uzyskać więcej informacji o tym wszystkie rozszerzenia w ramach szablonu maszyny wirtualnej. W tym artykule opisano sposób dodawania szablonu maszyny wirtualnej systemu windows hello Azure Diagnostics rozszerzenia tooa.  

## <a name="add-hello-azure-diagnostics-extension-toohello-vm-resource-definition"></a>Dodawanie definicji zasobu hello Azure Diagnostics rozszerzenia toohello maszyny Wirtualnej
tooenable hello diagnostyki rozszerzenia na maszynie wirtualnej systemu Windows należy rozszerzenia hello tooadd jako zasób maszyny Wirtualnej w hello szablonu usługi Resource manager.

Dla prostego Menedżera zasobów opartych na maszynie wirtualnej dodać hello rozszerzenia konfiguracji toohello *zasobów* tablicy dla hello maszyny wirtualnej: 

    "resources": [
                {
                    "name": "Microsoft.Insights.VMDiagnosticsSettings",
                    "type": "extensions",
                    "location": "[resourceGroup().location]",
                    "apiVersion": "2015-06-15",
                    "dependsOn": [
                        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
                    ],
                    "tags": {
                        "displayName": "AzureDiagnostics"
                    },
                    "properties": {
                        "publisher": "Microsoft.Azure.Diagnostics",
                        "type": "IaaSDiagnostics",
                        "typeHandlerVersion": "1.5",
                        "autoUpgradeMinorVersion": true,
                        "settings": {
                            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
                            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
                        },
                        "protectedSettings": {
                            "storageAccountName": "[parameters('existingdiagnosticsStorageAccountName')]",
                            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
                            "storageAccountEndPoint": "https://core.windows.net"
                        }
                    }
                }
            ]


Innym wspólnej Konwencji jest dodać Konfiguracja rozszerzenia hello na hello zasobów korzenia hello szablonu zamiast definiować go w węźle zasobów hello maszyny wirtualnej. Z tej metody ma tooexplicitly Określ hierarchicznych relacji między rozszerzenie hello i hello maszyny wirtualnej z hello *nazwa* i *typu* wartości. Na przykład: 

    "name": "[concat(variables('vmName'),'Microsoft.Insights.VMDiagnosticsSettings')]",
    "type": "Microsoft.Compute/virtualMachines/extensions",

rozszerzenia Hello jest zawsze skojarzony z maszyną wirtualną hello, możesz bezpośrednio zdefiniować go bezpośrednio w węźle zasobu maszyny wirtualnej hello lub zdefiniować ją na poziomie podstawowym hello i użyj tooassociate konwencji nazewnictwa hierarchiczna hello go przy użyciu hello wirtualnego maszyny.

Zestawy skalowania maszyny wirtualnej hello rozszerzeń określana jest konfiguracja w hello *extensionProfile* właściwości hello *VirtualMachineProfile*.

Witaj *wydawcy* właściwość z wartością hello **Microsoft.Azure.Diagnostics** i hello *typu* właściwość z wartością hello **IaaSDiagnostics** jednoznacznie zidentyfikować hello Azure Diagnostics rozszerzenia.

Witaj wartość hello *nazwa* właściwości mogą być używane toorefer toohello rozszerzenia w grupie zasobów hello. Ustawienie w szczególności za**Microsoft.Insights.VMDiagnosticsSettings** umożliwi toobe można zidentyfikować hello zapewnienie portalu Azure, która hello monitorowania wykresy będą wyświetlane poprawnie w hello portalu Azure.

Witaj *typeHandlerVersion* Określa wersję hello rozszerzenia hello chcesz toouse. Ustawienie *autoUpgradeMinorVersion* podrzędny numer wersji zbyt**true** zapewnia pobierze najnowszą wersję pomocniczą hello hello rozszerzenia, która jest dostępna. Zdecydowanie zaleca się, że możesz zawsze ustawić *autoUpgradeMinorVersion* można tooalways **true** tak, aby zawsze uzyskać toouse hello najnowsze diagnostyki dostępne rozszerzenia ze wszystkimi hello nowe funkcje i usterki poprawki. 

Witaj *ustawienia* element zawiera właściwości konfiguracji hello rozszerzenia, które można ustawić i ponownie odczytywana hello rozszerzenia (czasami określonego tooas publicznej konfiguracji). Witaj *xmlcfg* właściwość zawiera konfigurację xml na podstawie dzienników diagnostycznych hello, liczniki wydajności itp, które zostaną zebrane przez agenta diagnostyki hello. Zobacz [schemat konfiguracji diagnostyki](https://msdn.microsoft.com/library/azure/dn782207.aspx) uzyskać więcej informacji o schematu xml hello samej siebie. Popularną praktyką jest toostore hello rzeczywiste xml konfiguracji jako zmienną hello szablonu usługi Azure Resource Manager i następnie ZŁĄCZ.teksty i base64 zakodować je wartość hello tooset *xmlcfg*. Zobacz sekcję hello na [zmienne konfiguracji diagnostyki](#diagnostics-configuration-variables) toounderstand więcej informacji na temat sposobu toostore hello xml w zmiennych. Witaj *storageAccount* właściwość określa nazwę hello dane diagnostyczne toowhich konta magazynu hello zostanie przeniesiona. 

Witaj właściwości w *protectedSettings* (czasami określonego tooas konfiguracji prywatnej) można ustawić, ale nie można odczytać po ustawiany. Witaj tylko do zapisu rodzaj *protectedSettings* ułatwia przydatne w przypadku przechowywania kluczy tajnych, takie jak klucz konta magazynu hello której będą zapisywane dane diagnostyczne hello.    

## <a name="specifying-diagnostics-storage-account-as-parameters"></a>Określanie konta magazynu diagnostyki jako parametrów
powyżej fragment json rozszerzenia diagnostyki Hello przyjmuje dwa parametry *existingdiagnosticsStorageAccountName* i *existingdiagnosticsStorageResourceGroup* toospecify hello diagnostyki Konto magazynu, w którym będą przechowywane dane diagnostyczne. Określanie hello diagnostycznego konta magazynu, zgodnie z parametrem umożliwia łatwe toochange hello diagnostycznego konta magazynu różnych środowiskach np. Możesz toouse konto magazynu diagnostyki różnych testowanie i inne hasło dla użytkownika wdrożenia produkcyjnego.  

        "existingdiagnosticsStorageAccountName": {
            "type": "string",
            "metadata": {
        "description": "hello name of an existing storage account toowhich diagnostics data will be transfered."
            }        
        },
        "existingdiagnosticsStorageResourceGroup": {
            "type": "string",
            "metadata": {
        "description": "hello resource group for hello storage account specified in existingdiagnosticsStorageAccountName"
              }
        }

Jest najlepszym rozwiązaniem toospecify konto magazynu diagnostyki w innej grupie zasobów niż grupa zasobów hello hello maszyny wirtualnej. Grupa zasobów jest uznawana za toobe jednostki wdrożenia własnej okres istnienia, maszynę wirtualną można wdrożyć i wdrożone nowe aktualizacje konfiguracje są wprowadzane go tooit, ale może być toocontinue przechowywanie danych diagnostycznych hello w hello tego samego konta magazynu przez te wdrożenia maszyny wirtualnej. Problemy między mających hello konta magazynu w różnych zasobów umożliwia hello magazynu tooaccept dane z różnych wdrażania maszyn wirtualnych, dzięki czemu można łatwo tootroubleshoot hello różne wersje.

> [!NOTE]
> W przypadku utworzenia szablonu maszyny wirtualnej systemu windows z programu Visual Studio hello domyślne konto magazynu może być ustawiony toouse hello tego samego konta magazynu, w którym przekazaniu hello dysk VHD maszyny wirtualnej. Jest to toosimplify wstępnej instalacji hello maszyny Wirtualnej. Należy ponownie współczynnika hello szablonu toouse innego konta magazynu, który może być przekazany jako parametr. 
> 
> 

## <a name="diagnostics-configuration-variables"></a>Zmienne konfiguracji diagnostyki
Definiuje Hello diagnostyki rozszerzenia json fragment powyżej *accountid* toosimplify zmiennej pobierania hello klucz konta magazynu dla magazynu diagnostyki hello:   

    "accountid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/',parameters('existingdiagnosticsStorageResourceGroup'), '/providers/','Microsoft.Storage/storageAccounts/', parameters('existingdiagnosticsStorageAccountName'))]"


Witaj *xmlcfg* właściwości rozszerzenia diagnostyki hello jest definiowana za pomocą wielu zmiennych, które są połączone ze sobą. Hello wartości tych zmiennych są w formacie xml, więc potrzebna jest prawidłowo wpisywany podczas ustawiania zmiennych json hello toobe.

Witaj poniżej opisano hello diagnostyki konfiguracji xml, który zbiera dane liczników wydajności poziomu standardowych systemowych oraz niektóre dzienniki zdarzeń systemu windows i dzienników infrastruktury Diagnostyka. Ma zostały zmienione znaczenie i prawidłowo sformatowane, dzięki czemu hello konfiguracji można bezpośrednio wkleić do hello sekcji zmiennych szablonu. Zobacz hello [schemat konfiguracji diagnostyki](https://msdn.microsoft.com/library/azure/dn782207.aspx) więcej człowieka przykład czytelny hello konfiguracji XML.

        "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
        "wadperfcounters1": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Privileged Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU privileged time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% User Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU user time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor Information(_Total)\\Processor Frequency\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"CPU frequency\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\System\\Processes\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Processes\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Threads\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Handle Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Handles\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\% Committed Bytes In Use\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Memory usage\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Available Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory available\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Committed Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory committed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Commit Limit\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory commit limit\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active time\" locale=\"en-us\"/></PerformanceCounterConfiguration>",
        "wadperfcounters2": "<PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Read Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active read time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Write Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active write time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Transfers/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Reads/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk read operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Writes/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk write operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Read Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk read speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Write Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk write speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\LogicalDisk(_Total)\\% Free Space\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk free space (percentage)\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
        "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters1'), variables('wadperfcounters2'), '<Metrics resourceId=\"')]",
        "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name , '/providers/', 'Microsoft.Compute/virtualMachines/')]",
        "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>"

węzeł xml definicji metryk Hello w hello powyżej konfiguracji jest element konfiguracji ważne, ponieważ definiuje sposób hello liczników wydajności zdefiniowanych we wcześniejszej części hello xml w *PerformanceCounter* zostaną zagregowane węzłów i przechowywane. 

> [!IMPORTANT]
> Te metryki dysku hello monitorowania wykresów i alertach w hello portalu Azure.  Witaj **metryki** węzła o hello *resourceID* i **MetricAggregation** muszą być zawarte w hello konfiguracji diagnostyki dla maszyny Wirtualnej, jeśli chcesz hello toosee maszyny Wirtualnej dane monitorowania w hello portalu Azure. 
> 
> 

Witaj poniżej znajduje się przykład hello xml definicji metryk: 

        <Metrics resourceId="/subscriptions/subscription().subscriptionId/resourceGroups/resourceGroup().name/providers/Microsoft.Compute/virtualMachines/vmName">
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>

Witaj *resourceID* atrybutu unikatowo identyfikuje hello maszyny wirtualnej w ramach subskrypcji. Upewnij się, że subscription() hello toouse i resourceGroup() działa tak, aby hello szablonu automatycznie aktualizuje te wartości na podstawie grupy subskrypcji i zasobu hello, który jest wdrażany z.

Jeśli tworzysz wiele maszyn wirtualnych w pętli, konieczne będzie toopopulate hello *resourceID* wartości z toocorrectly funkcji copyIndex() rozróżnianie każdego poszczególnych maszyn wirtualnych. Witaj *xmlCfg* wartość może być zaktualizowany toosupport to w następujący sposób:  

    "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), concat(parameters('vmNamePrefix'), copyindex()), variables('wadcfgxend')))]", 

Witaj wartość MetricAggregation *PT1H* i *PT1M* oznaczającego agregacji na minutę i agregacji ponad godzinę.

## <a name="wadmetrics-tables-in-storage"></a>Tabele WADMetrics w magazynie
Konfiguracja metryki Hello powyżej wygeneruje tabel na koncie magazynu diagnostyki z hello następującej konwencji nazewnictwa:

* **WADMetrics** : standardowego prefiksu dla wszystkich tabel WADMetrics
* **PT1H** lub **PT1M** : oznacza, że hello zawierającej agregowanie danych ponad 1 godzina lub 1 minuta
* **P10D** : oznacza, że tabela hello będzie zawierać danych dla 10 dni od uruchomienia tabeli hello na zbieranie danych
* **V2S** : stała znakowa
* **RRRRMMDD** : hello Data, w których hello tabeli rozpoczęcia, zbieranie danych

Przykład: *WADMetricsPT1HP10DV2S20151108* zawierają zagregowane ponad godzinę 10 dni, począwszy od dnia 2015-11-lis dane metryk    

Każda tabela WADMetrics będzie zawierać hello następujące kolumny:

* **PartitionKey**: hello partitionkey jest tworzony na podstawie na powitania *resourceID* toouniquely wartość zidentyfikować hello zasobu maszyny Wirtualnej. na przykład: 002Fsubscriptions:<subscriptionID>: 002FresourceGroups:002F<ResourceGroupName>: 002Fproviders:002FMicrosoft:002ECompute:002FvirtualMachines:002F<vmName>  
* **RowKey** : format hello następujące <Descending time tick>:<Performance Counter Name>. Hello malejącej obliczanie osi czasu jest Takty maksymalny czas minus hello godzina rozpoczęcia hello hello agregacji okresu. Na przykład Jeśli okres próbkowania hello uruchomione w dniu 2015-10-lis i będzie Obliczanie czasu UTC, a następnie hello 00:00Hrs: DateTime.MaxValue.Ticks - (DateTime(2015,11,10,0,0,0,DateTimeKind.Utc) nowe. Znaczniki). Dla klucz wiersza hello licznika wydajności hello pamięci dostępne bajty będzie wyglądała, takich jak: 2519551871999999999__:005CMemory:005CAvailable:0020 bajtów
* **CounterName** : jest nazwą hello hello licznika wydajności. Odpowiada to hello *counterSpecifier* zdefiniowane w pliku konfiguracji xml hello.
* **Maksymalna** : hello maksymalna wartość licznika wydajności hello okresie hello agregacji.
* **Minimalna** : hello minimalną wartość licznika wydajności hello okresie hello agregacji.
* **Całkowita liczba** : hello sumę wszystkich wartości licznika wydajności hello zgłoszone w okresie agregacji hello.
* **Liczba** : zgłosił hello łączna liczba wartości licznika wydajności hello.
* **Średnia** : hello średniej (łączna/liczba) wartości licznika wydajności hello okresie hello agregacji.

## <a name="next-steps"></a>Następne kroki
* Dla kompletnego przykładowego szablonu maszyny wirtualnej systemu Windows z rozszerzeniem diagnostyki [201-rozszerzenia maszyny wirtualnej — monitorowanie diagnostycznych](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-monitoring-diagnostics-extension)   
* Wdróż hello resource manager szablonu przy użyciu [programu Azure PowerShell](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) lub [wiersza polecenia platformy Azure](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* Dowiedz się więcej o [tworzenia szablonów usługi Azure Resource Manager](../../resource-group-authoring-templates.md)

