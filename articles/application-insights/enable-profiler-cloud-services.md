---
title: "aaaEnable Azure Application Insights Profiler do zasobu usługi w chmurze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset się profilera hello w aplikacji ASP.NET obsługiwanych przez zasób usługi w chmurze Azure."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: b9ac3bca513bf4518f44780389a9f2945f6ccc98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a>Application Insights profilera, Włącz zasobu usługi w chmurze Azure

W tym przewodniku pokazano, jak tooenable Azure Application Insights profilera w aplikacji ASP.NET obsługiwanych przez zasób usługi w chmurze Azure. Przykładami Hello obsługę maszyn wirtualnych platformy Azure, zestawy skalowania maszyny wirtualnej i sieci szkieletowej usług Azure. wszystkie przykłady Hello korzystają z szablonów, które obsługują modelu wdrażania usługi Azure Resource Manager hello. Aby uzyskać więcej informacji na temat modelu wdrażania hello Przejrzyj [usługi Azure Resource Manager, a wdrożenie klasyczne: zrozumienie modele wdrażania i stan zasobów hello](/azure-resource-manager/resource-manager-deployment-model).

## <a name="overview"></a>Omówienie

powitania po diagram pokazano, jak działa hello profilera dla zasobów usługi w chmurze Azure. Maszyna wirtualna platformy Azure jest używany jako przykład.

![Omówienie](./media/enable-profiler-compute/overview.png) toocollect informacji do przetwarzania i wyświetlania na hello portalu Azure, należy zainstalować składnik agenta diagnostyki hello hello zasobów usługi w chmurze Azure. Witaj rest wskazówki hello znajdują się wskazówki dotyczące tooinstall i skonfigurować tooenable agenta diagnostyki hello Application Insights profilera.

## <a name="prerequisites-for-hello-walkthrough"></a>Wymagania wstępne dotyczące hello wskazówki

* Wdrożenie szablonu usługi Resource Manager, który instaluje agentów profiler hello na powitania maszyn wirtualnych ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) lub skalowanie zestawów ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).

* Wystąpienie usługi Application Insights dla profilowania włączone. Aby uzyskać instrukcje, zobacz [włączyć profil hello](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).

* .NET framework 4.6.1 lub nowszy zainstalowany na powitania docelowego zasobu usługi w chmurze Azure.

## <a name="create-a-resource-group-in-your-azure-subscription"></a>Tworzenie grupy zasobów w Twojej subskrypcji platformy Azure
Witaj poniższy przykład pokazuje, jak toocreate zasób grupy za pomocą skryptu programu PowerShell:

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a>Tworzenie zasobu usługi Application Insights w grupie zasobów hello
Na powitania **usługi Application Insights** bloku, wprowadź hello informacje o zasobie, jak pokazano w poniższym przykładzie: 

![Application Insights bloku](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a>Zastosowanie klucza Instrumentacji usługi Application Insights w szablonie usługi Azure Resource Manager hello

1. Jeśli nie zostały jeszcze pobrane hello szablonu, pobierz go z [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).

2. Znajdowanie hello klucza usługi Application Insights.
   
   ![Lokalizacja hello klucza](./media/enable-profiler-compute/copyaikey.png)

3. Zastąp wartość szablonu hello.
   
   ![Wartość w hello szablonu](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a>Tworzenie aplikacji sieci web hello toohost maszyny Wirtualnej Azure
1. Utwórz hasło hello toosave bezpieczny ciąg.

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. Wdrażanie szablonu usługi Azure Resource Manager hello.

   Zmień katalog hello w folderze toohello konsoli programu PowerShell hello, który zawiera szablon usługi Resource Manager. toodeploy hello szablon, uruchom następujące polecenie hello:

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

Po pomyślnym uruchomieniu skryptu hello powinien znajdować się maszyny Wirtualnej o nazwie **MyWindowsVM** w grupie zasobów.

## <a name="configure-web-deploy-on-hello-vm"></a>Konfiguruje narzędzie Web Deploy na powitania maszyny Wirtualnej
Upewnij się, że narzędzia Web Deploy jest włączony na maszynie Wirtualnej, dlatego można opublikować aplikację sieci web w programie Visual Studio.

tooinstall narzędzia Web Deploy na maszynie Wirtualnej ręcznie za pośrednictwem WebPI, zobacz [Instalowanie i Konfigurowanie narzędzia Web Deploy w programie IIS 8.0 lub później](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later). Na przykład jak tooautomate instalowanie narzędzia Web Deploy za pomocą szablonu usługi Azure Resource Manager, zobacz [tworzenie, konfigurowanie i wdrażanie tooan aplikacji sieci web Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).

Jeśli wdrażasz aplikacji platformy ASP.NET MVC, przejdź tooServer Manager, wybierz **Dodaj role i funkcje** > **serwer sieci Web (IIS)** > **serwera sieci Web**  >  **Projektowanie aplikacji**i Włącz funkcję ASP.NET 4.5 na serwerze.

![Dodaj ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a>Zainstaluj hello zestaw SDK usługi Azure Application Insights do projektu
1. Otwórz aplikację sieci web ASP.NET w programie Visual Studio.

2. Kliknij prawym przyciskiem myszy projekt hello i wybierz **Dodaj** > **usług połączonych**.

3. Wybierz **usługi Application Insights**.

4. Wykonaj instrukcje hello na stronie powitania. Wybierz zasób usługi Application Insights hello, który został utworzony wcześniej.

5. Wybierz hello **zarejestrować** przycisku.


## <a name="publish-hello-project-tooan-azure-vm"></a>Publikowanie hello projektu tooan maszyny Wirtualnej Azure
Istnieje kilka sposobów toopublish tooan aplikacji maszyny Wirtualnej platformy Azure. Jednym ze sposobów jest toouse programu Visual Studio 2017 r.

1. Kliknij prawym przyciskiem myszy projekt hello i wybierz **publikowania**.

2. Wybierz **maszyny wirtualne Microsoft Azure** jako hello publikowanie docelowego i wykonaj kroki hello.

   ![Publikowanie FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. Uruchamianie testów obciążenia względem aplikacji. Wyniki powinny być widoczne w portalu sieci Web hello usługi Application Insights wystąpienia.


## <a name="enable-hello-profiler"></a>Włącz hello profilera
1. Przejdź do usługi Application Insights tooyour **wydajności** bloku, a następnie wybierz **Konfiguruj**.
   
   ![Ikona konfigurowania](./media/enable-profiler-compute/enableprofiler1.png)
 
2. Wybierz **włączyć profilera**.
   
   ![Włącz ikona profilera](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a>Dodawanie aplikacji tooyour testów wydajności
Dlatego firma Microsoft może zbierać niektórych toobe dane przykładowe wyświetlane w programie Application Insights Profiler, wykonaj następujące kroki:

1. Przeglądaj toohello zasobu usługi Application Insights, który został utworzony wcześniej. 

2. Przejdź toohello **dostępności** bloku i Dodaj test wydajności, który wysyła adres URL aplikacji tooyour żądania sieci web. 

   ![Dodawanie testów wydajności](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a>Wyświetlanie danych dotyczących wydajności

1. Zaczekaj 10 – 15 minut na toocollect profilera hello i analizowanie danych hello. 

2. Przejdź toohello **wydajności** bloku zasobu usługi Application Insights i widoku jak aplikacja działa po pod obciążeniem.

   ![Wyświetlanie wydajności](./media/enable-profiler-compute/aiperformance.png)

3. Witaj wybierz ikonę w obszarze **przykłady** tooopen hello **widoku śledzenia** bloku.

   ![Otwieranie bloku przeglądania śledzenia hello](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a>Praca z istniejącego szablonu

1. Zlokalizuj deklaracja zasobów Azure Diagnostics hello w szablonie wdrożenia.
   
   Jeśli nie masz deklaracji, można utworzyć jedną podobny hello deklaracji w hello poniższy przykład. Można aktualizować hello szablonu z hello [Eksploratora zasobów Azure witryny sieci Web](https://resources.azure.com).

2. Wydawca zmiany hello z `Microsoft.Azure.Diagnostics` zbyt`AIP.Diagnostics.Test`.

3. Aby uzyskać `typeHandlerVersion`, użyj `0.0`.

4. Upewnij się, że `autoUpgradeMinorVersion` ustawiono zbyt`true`.

5. Dodaj nowy hello `ApplicationInsightsProfiler` wystąpienie obiektu sink hello `WadCfg` obiekt ustawień, jak pokazano w hello poniższy przykład:

```
"resources": [
        {
          "type": "extensions",
          "name": "Microsoft.Insights.VMDiagnosticsSettings",
          "apiVersion": "2016-03-30",
          "properties": {
            "publisher": "AIP.Diagnostics.Test",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "0.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "WadCfg": {
                "SinksConfig": {
                  "Sink": [
                    {
                      "name": "Give a descriptive short name. E.g.: MyApplicationInsightsProfilerSink",
                      "ApplicationInsightsProfiler": "Enter hello Application Insights instance instrumentation key guid here"
                    }
                  ]
                },
                "DiagnosticMonitorConfiguration": {
                    ...
                }
                ...
              }
              ...
            }
            ...
          }
          ...
]
```

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a>Włącz profilera hello na zestawy skalowania maszyny wirtualnej
toosee jak tooenable hello profilera, Pobierz hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) szablonu. Zastosuj hello same zmiany w zasobie rozszerzenia diagnostyki toohello szablonu maszyny Wirtualnej dla zestawu skalowania maszyny wirtualnej hello.

Upewnij się, że każde wystąpienie w zestawie skalowania hello ma toohello dostęp do Internetu. Hello agentów Profiler może następnie wyślij próbki hello zbierane tooApplication wgląd do wyświetlania i analizy.

## <a name="enable-hello-profiler-on-service-fabric-applications"></a>Włącz profilera hello w przypadku aplikacji sieci szkieletowej usług
1. Hello świadczenia usługi sieć szkieletowa klastra toohave hello Azure Diagnostics rozszerzenia, które instaluje hello agentów Profiler.

2. Zainstaluj hello zestaw SDK usługi Application Insights w projekcie hello i skonfiguruj hello klucza usługi Application Insights.

3. Dodaj telemetrię tooinstrument kodu aplikacji.

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a>Zainicjuj obsługę hello sieci szkieletowej usług klastra toohave hello rozszerzenia diagnostyki Azure, które instaluje hello agentów Profiler
Klaster sieci szkieletowej usług może być bezpieczne lub które nie są bezpieczne. Można ustawić jedną toobe klastra bramy niezabezpieczone, certyfikat nie wymaga dostępu. Klastry obsługujące logikę biznesową i danych powinny być bezpieczne. Można włączyć profilera hello na bezpieczne i niezabezpieczone klastry sieci szkieletowej usług. W tym przewodniku zastosowano niezabezpieczonego klastra jako przykład tooexplain, jakie zmiany są wymagane tooenable hello profilera. Umożliwia obsługę bezpiecznej klastra w hello tak samo.

1. Pobierz [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json). Tak samo jak dla maszyn wirtualnych i zestawy skalowania maszyny wirtualnej, Zastąp `Application_Insights_Key` z kluczem usługi Application Insights:

   ```
   "publisher": "AIP.Diagnostics.Test",
                 "settings": {
                   "WadCfg": {
                     "SinksConfig": {
                       "Sink": [
                         {
                           "name": "MyApplicationInsightsProfilerSinkVMSS",
                           "ApplicationInsightsProfiler": "[Application_Insights_Key]"
                         }
                       ]
                     },
   ```

2. Wdrażanie szablonu hello przy użyciu skryptu programu PowerShell:

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a>Zainstaluj hello zestaw SDK usługi Application Insights w projekcie hello i skonfiguruj hello klucza usługi Application Insights
Zainstaluj zestaw SDK usługi Application Insights hello z hello [pakietu NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). Upewnij się, czy zainstalować stabilną wersję, 2.3 lub nowszej. 

Aby uzyskać informacje o konfigurowaniu usługi Application Insights w projektach, zobacz [przy użyciu usługi sieć szkieletowa z usługą Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).

### <a name="add-application-code-tooinstrument-telemetry"></a>Dodaj telemetrię tooinstrument kodu aplikacji
1. Dla części kodu, które mają tooinstrument dodać za pomocą instrukcji wokół niego. 

   W hello poniższy przykład, hello `RunAsync` metody jest wykonanie dodatkowych czynności, a hello `telemetryClient` klasy przechwytuje dane telemetryczne powitania po jego uruchomieniu. Zdarzenie Hello musi unikatową nazwę w aplikacji hello.

   ```
   protected override async Task RunAsync(CancellationToken cancellationToken)
       {
           // TODO: Replace hello following sample code with your own logic
           //       or remove this RunAsync override if it's not needed in your service.

           while (true)
           {
               using( var operation = telemetryClient.StartOperation<RequestTelemetry>("[Insert_Event_Unique_Name]"))
               {
                   cancellationToken.ThrowIfCancellationRequested();

                   ++this.iterations;

                   ServiceEventSource.Current.ServiceMessage(this.Context, "Working-{0}", this.iterations);

                   await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
               }

           }
       }
   ```

2. Wdrażanie klastra usługi sieć szkieletowa toohello aplikacji. Poczekaj toorun aplikacji hello przez 10 minut. Aby lepiej efekt można uruchomić testu obciążenia w aplikacji hello. Portal usługi Application Insights Przejdź toohello **wydajności** bloku, a powinien przykłady śladów profilowania są wyświetlane.

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a>Następne kroki

- Znaleźć pomoc dotyczącą rozwiązywania problemów profilera w [profilera Rozwiązywanie problemów z](app-insights-profiler.md#troubleshooting).

- Dowiedz się więcej o profilera hello w [Application Insights profilera](app-insights-profiler.md).
