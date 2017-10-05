---
title: "Włącz Azure Application Insights Profiler do zasobu usługi w chmurze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować profilera w aplikacji ASP.NET obsługiwanych przez zasób usługi w chmurze Azure."
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
ms.openlocfilehash: 5ff062ac81dca9d8b205cec966d2a9c11a4005b6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a>Application Insights profilera, Włącz zasobu usługi w chmurze Azure

W tym przewodniku pokazano, jak włączyć Azure Application Insights profilera aplikacji ASP.NET obsługiwanych przez zasób usługi w chmurze Azure. Przykłady obejmują obsługę maszyn wirtualnych platformy Azure, zestawy skalowania maszyny wirtualnej i sieci szkieletowej usług Azure. Wszystkie przykłady korzystają z szablonów, które obsługują modelu wdrażania usługi Azure Resource Manager. Aby uzyskać więcej informacji na temat modelu wdrażania, przejrzyj [usługi Azure Resource Manager, a wdrożenie klasyczne: zrozumienie modele wdrażania i stan zasobów](/azure-resource-manager/resource-manager-deployment-model).

## <a name="overview"></a>Omówienie

Na poniższym diagramie przedstawiono, jak działa profilera dla zasobów usługi w chmurze Azure. Maszyna wirtualna platformy Azure jest używany jako przykład.

![Omówienie](./media/enable-profiler-compute/overview.png) do zbierania informacji do przetwarzania i wyświetlania w portalu Azure, należy zainstalować składnik agenta diagnostyki dla zasobów usługi w chmurze Azure. Pozostała część przewodnika znajdują się wskazówki dotyczące sposobu instalowania i konfigurowania agenta diagnostyki, aby włączyć Application Insights profilera.

## <a name="prerequisites-for-the-walkthrough"></a>Wymagania wstępne dotyczące przewodnika

* Wdrożenie szablonu usługi Resource Manager, który instaluje agentów profiler na maszynach wirtualnych ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) lub skalowanie zestawów ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).

* Wystąpienie usługi Application Insights dla profilowania włączone. Aby uzyskać instrukcje, zobacz [włączyć profil](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).

* .NET framework 4.6.1 lub nowszej w celu zasobu usługi w chmurze Azure.

## <a name="create-a-resource-group-in-your-azure-subscription"></a>Tworzenie grupy zasobów w Twojej subskrypcji platformy Azure
W poniższym przykładzie pokazano, jak utworzyć grupę zasobów za pomocą skryptu programu PowerShell:

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-the-resource-group"></a>Tworzenie zasobu usługi Application Insights w grupie zasobów
Na **usługi Application Insights** bloku, wprowadź informacje o zasobie, jak pokazano w poniższym przykładzie: 

![Application Insights bloku](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-the-azure-resource-manager-template"></a>Zastosowanie klucza Instrumentacji usługi Application Insights w szablonie usługi Azure Resource Manager

1. Jeśli nie zostały jeszcze pobrane szablonu, pobierz go z [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).

2. Znajdź klucz usługi Application Insights.
   
   ![Lokalizacja klucza](./media/enable-profiler-compute/copyaikey.png)

3. Zastąp wartość szablonu.
   
   ![Wartość w szablonie](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-to-host-the-web-application"></a>Tworzenie maszyny Wirtualnej platformy Azure w celu hostowania aplikacji sieci web
1. Utwórz bezpieczny ciąg, aby zapisać hasło.

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. Wdrażanie szablonu usługi Azure Resource Manager.

   Zmień katalog, w konsoli programu PowerShell do folderu, który zawiera szablon usługi Resource Manager. Aby wdrożyć szablon, uruchom następujące polecenie:

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

Po pomyślnym uruchomieniu skryptu, należy odnaleźć maszyny Wirtualnej o nazwie **MyWindowsVM** w grupie zasobów.

## <a name="configure-web-deploy-on-the-vm"></a>Konfigurowanie sieci Web wdrażanie na maszynie Wirtualnej
Upewnij się, że narzędzia Web Deploy jest włączony na maszynie Wirtualnej, dlatego można opublikować aplikację sieci web w programie Visual Studio.

Aby zainstalować narzędzie Web Deploy na maszynie Wirtualnej ręcznie za pośrednictwem WebPI, zobacz [Instalowanie i Konfigurowanie narzędzia Web Deploy w programie IIS 8.0 lub później](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later). Na przykład sposobu automatyzacji instalowanie narzędzia Web Deploy za pomocą szablonu usługi Azure Resource Manager zobacz [tworzenie, konfigurowanie i wdrażanie aplikacji sieci web do maszyny Wirtualnej platformy Azure](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).

Jeśli wdrażasz aplikacji platformy ASP.NET MVC, przejdź do Menedżera serwera, wybierz **Dodaj role i funkcje** > **serwer sieci Web (IIS)** > **serwera sieci Web** > **projektowanie aplikacji**i włączyć funkcję ASP.NET 4.5 na serwerze.

![Dodaj ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-the-azure-application-insights-sdk-for-your-project"></a>Zainstaluj zestaw SDK szczegółowych informacji o aplikacji Azure dla projektu
1. Otwórz aplikację sieci web ASP.NET w programie Visual Studio.

2. Kliknij prawym przyciskiem myszy projekt i wybierz **Dodaj** > **usług połączonych**.

3. Wybierz **usługi Application Insights**.

4. Postępuj zgodnie z instrukcjami na stronie. Wybierz wcześniej utworzony zasób usługi Application Insights.

5. Wybierz **zarejestrować** przycisku.


## <a name="publish-the-project-to-an-azure-vm"></a>Publikowania projektu na maszynie Wirtualnej platformy Azure
Istnieje kilka sposobów, aby opublikować aplikację na maszynie Wirtualnej platformy Azure. Jednym ze sposobów jest używać programu Visual Studio 2017 r.

1. Kliknij prawym przyciskiem myszy projekt i wybierz **publikowania**.

2. Wybierz **maszyny wirtualne Microsoft Azure** jako publikowanie docelowego, a następnie postępuj zgodnie z instrukcjami.

   ![Publikowanie FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. Uruchamianie testów obciążenia względem aplikacji. Wyniki powinny zostać wyświetlone na stronie usługi Application Insights wystąpienia portalu sieci Web.


## <a name="enable-the-profiler"></a>Włącz profilera
1. Przejdź do Twojej usługi Application Insights **wydajności** bloku, a następnie wybierz **Konfiguruj**.
   
   ![Ikona konfigurowania](./media/enable-profiler-compute/enableprofiler1.png)
 
2. Wybierz **włączyć profilera**.
   
   ![Włącz ikona profilera](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-to-your-application"></a>Dodaj test wydajności do aplikacji
Dlatego firma Microsoft może zbierać przykładowych danych do wyświetlenia w programie Application Insights Profiler, wykonaj następujące kroki:

1. Przejdź do zasobu usługi Application Insights, który został utworzony wcześniej. 

2. Przejdź do **dostępności** bloku i Dodaj test wydajności, który wysyła żądania sieci web do adres URL aplikacji. 

   ![Dodawanie testów wydajności](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a>Wyświetlanie danych dotyczących wydajności

1. Zaczekaj 10 – 15 minut na profilera do zbierania i analizowania danych. 

2. Przejdź do **wydajności** bloku zasobu usługi Application Insights i widoku jak aplikacja działa po pod obciążeniem.

   ![Wyświetlanie wydajności](./media/enable-profiler-compute/aiperformance.png)

3. Wybierz ikonę w obszarze **przykłady** otworzyć **widoku śledzenia** bloku.

   ![Otwieranie bloku przeglądania śledzenia](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a>Praca z istniejącego szablonu

1. Zlokalizuj deklaracja zasobów diagnostyki Azure do wdrożenia szablonu.
   
   Jeśli nie masz deklaracji, można utworzyć jedną podobny deklaracji w poniższym przykładzie. Możesz zaktualizować szablon z [Eksploratora zasobów Azure witryny sieci Web](https://resources.azure.com).

2. Zmień wydawcy z `Microsoft.Azure.Diagnostics` do `AIP.Diagnostics.Test`.

3. Aby uzyskać `typeHandlerVersion`, użyj `0.0`.

4. Upewnij się, że `autoUpgradeMinorVersion` ma ustawioną wartość `true`.

5. Dodaj nowe `ApplicationInsightsProfiler` wystąpienie obiektu sink `WadCfg` obiekt ustawień, jak pokazano w poniższym przykładzie:

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
                      "ApplicationInsightsProfiler": "Enter the Application Insights instance instrumentation key guid here"
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

## <a name="enable-the-profiler-on-virtual-machine-scale-sets"></a>Włącz profilera na zestawy skalowania maszyny wirtualnej
Aby zobaczyć, jak włączyć profilera, Pobierz [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) szablonu. Zastosuj te same zmiany w szablonie maszyny Wirtualnej do diagnostyki rozszerzenia zasobu dla zestawu skalowania maszyny wirtualnej.

Upewnij się, że każde wystąpienie w zestawie skalowania ma dostęp do Internetu. Agentów Profiler może wysłać zebrane próbki do usługi Application Insights do wyświetlania i analizy.

## <a name="enable-the-profiler-on-service-fabric-applications"></a>Włącz profilera w przypadku aplikacji sieci szkieletowej usług
1. Udostępnianie klastra sieci szkieletowej usług rozszerzenie diagnostyki Azure, która instaluje agenta programu Profiler.

2. Zainstaluj zestaw SDK usługi Application Insights w projekcie i skonfiguruj klucz usługi Application Insights.

3. Dodaj do dokumentu telemetrii kod aplikacji.

### <a name="provision-the-service-fabric-cluster-to-have-the-azure-diagnostics-extension-that-installs-the-profiler-agent"></a>Udostępnianie klastra sieci szkieletowej usług rozszerzenie diagnostyki Azure, która instaluje agenta programu Profiler
Klaster sieci szkieletowej usług może być bezpieczne lub które nie są bezpieczne. Można ustawić jednego klastra bramy do być niezabezpieczone, więc nie wymaga certyfikatu do dostępu. Klastry obsługujące logikę biznesową i danych powinny być bezpieczne. Można włączyć profilera na bezpieczne i niezabezpieczone klastry sieci szkieletowej usług. W tym przewodniku zastosowano niezabezpieczonego klastra jako przykład wyjaśniający, jakie zmiany są wymagane do włączenia profilera. Bezpieczne klastra można udostępnić w taki sam sposób.

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

2. Wdrażanie szablonu przy użyciu skryptu programu PowerShell:

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-the-application-insights-sdk-in-the-project-and-configure-the-application-insights-key"></a>Zainstaluj zestaw SDK usługi Application Insights w projekcie i skonfiguruj klucz usługi Application Insights
Zainstaluj zestaw SDK usługi Application Insights z [pakietu NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). Upewnij się, czy zainstalować stabilną wersję, 2.3 lub nowszej. 

Aby uzyskać informacje o konfigurowaniu usługi Application Insights w projektach, zobacz [przy użyciu usługi sieć szkieletowa z usługą Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).

### <a name="add-application-code-to-instrument-telemetry"></a>Dodaj kod aplikacji, aby dane telemetryczne dokumentu
1. Dla dowolnego elementu kodu, który ma zostać Instrumentacja, dodać za pomocą instrukcji wokół niego. 

   W poniższym przykładzie `RunAsync` — metoda jest wykonanie dodatkowych czynności i `telemetryClient` klasy przechwytuje dane telemetryczne po jego uruchomieniu. Zdarzenie musi unikatową nazwę w aplikacji.

   ```
   protected override async Task RunAsync(CancellationToken cancellationToken)
       {
           // TODO: Replace the following sample code with your own logic
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

2. Wdrażanie aplikacji do klastra usługi sieć szkieletowa usług. Poczekaj, aż aplikacji do uruchomienia przez 10 minut. Aby lepiej efekt można uruchomić testu obciążenia w aplikacji. Przejdź do portalu usługi Application Insights **wydajności** bloku, a powinien przykłady śladów profilowania są wyświetlane.

<!---
Commenting out these sections for now
## Enable the Profiler on Cloud Services applications
[TODO]
## Enable the Profiler on classic Azure Virtual Machines
[TODO]
## Enable the Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a>Następne kroki

- Znaleźć pomoc dotyczącą rozwiązywania problemów profilera w [profilera Rozwiązywanie problemów z](app-insights-profiler.md#troubleshooting).

- Dowiedz się więcej o profilera w [Application Insights profilera](app-insights-profiler.md).
