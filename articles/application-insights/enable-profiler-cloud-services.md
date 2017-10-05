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
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a><span data-ttu-id="c6851-103">Application Insights profilera, Włącz zasobu usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="c6851-103">Enable Application Insights Profiler on an Azure Cloud Services resource</span></span>

<span data-ttu-id="c6851-104">W tym przewodniku pokazano, jak włączyć Azure Application Insights profilera aplikacji ASP.NET obsługiwanych przez zasób usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="c6851-104">This walkthrough demonstrates how to enable Azure Application Insights Profiler on an ASP.NET application hosted by an Azure Cloud Services resource.</span></span> <span data-ttu-id="c6851-105">Przykłady obejmują obsługę maszyn wirtualnych platformy Azure, zestawy skalowania maszyny wirtualnej i sieci szkieletowej usług Azure.</span><span class="sxs-lookup"><span data-stu-id="c6851-105">The examples include support for Azure Virtual Machines, virtual machine scale sets, and Azure Service Fabric.</span></span> <span data-ttu-id="c6851-106">Wszystkie przykłady korzystają z szablonów, które obsługują modelu wdrażania usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6851-106">The examples all rely on templates that support the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="c6851-107">Aby uzyskać więcej informacji na temat modelu wdrażania, przejrzyj [usługi Azure Resource Manager, a wdrożenie klasyczne: zrozumienie modele wdrażania i stan zasobów](/azure-resource-manager/resource-manager-deployment-model).</span><span class="sxs-lookup"><span data-stu-id="c6851-107">For more information about the deployment model, review [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](/azure-resource-manager/resource-manager-deployment-model).</span></span>

## <a name="overview"></a><span data-ttu-id="c6851-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c6851-108">Overview</span></span>

<span data-ttu-id="c6851-109">Na poniższym diagramie przedstawiono, jak działa profilera dla zasobów usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="c6851-109">The following diagram illustrates how the profiler works for Azure Cloud Services resources.</span></span> <span data-ttu-id="c6851-110">Maszyna wirtualna platformy Azure jest używany jako przykład.</span><span class="sxs-lookup"><span data-stu-id="c6851-110">It uses an Azure virtual machine as an example.</span></span>

<span data-ttu-id="c6851-111">![Omówienie](./media/enable-profiler-compute/overview.png) do zbierania informacji do przetwarzania i wyświetlania w portalu Azure, należy zainstalować składnik agenta diagnostyki dla zasobów usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="c6851-111">![Overview](./media/enable-profiler-compute/overview.png) To collect information for processing and display on the Azure portal, you must install the Diagnostics Agent component for the Azure Cloud Services resources.</span></span> <span data-ttu-id="c6851-112">Pozostała część przewodnika znajdują się wskazówki dotyczące sposobu instalowania i konfigurowania agenta diagnostyki, aby włączyć Application Insights profilera.</span><span class="sxs-lookup"><span data-stu-id="c6851-112">The rest of the walkthrough provides guidance on how to install and configure the Diagnostics Agent to enable Application Insights Profiler.</span></span>

## <a name="prerequisites-for-the-walkthrough"></a><span data-ttu-id="c6851-113">Wymagania wstępne dotyczące przewodnika</span><span class="sxs-lookup"><span data-stu-id="c6851-113">Prerequisites for the walkthrough</span></span>

* <span data-ttu-id="c6851-114">Wdrożenie szablonu usługi Resource Manager, który instaluje agentów profiler na maszynach wirtualnych ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) lub skalowanie zestawów ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span><span class="sxs-lookup"><span data-stu-id="c6851-114">A deployment Resource Manager template that installs the profiler agents on the VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) or scale sets ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span></span>

* <span data-ttu-id="c6851-115">Wystąpienie usługi Application Insights dla profilowania włączone.</span><span class="sxs-lookup"><span data-stu-id="c6851-115">An Application Insights instance enabled for profiling.</span></span> <span data-ttu-id="c6851-116">Aby uzyskać instrukcje, zobacz [włączyć profil](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span><span class="sxs-lookup"><span data-stu-id="c6851-116">For instructions, see [Enable the profile](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span></span>

* <span data-ttu-id="c6851-117">.NET framework 4.6.1 lub nowszej w celu zasobu usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="c6851-117">.NET Framework 4.6.1 or later installed on the target Azure Cloud Services resource.</span></span>

## <a name="create-a-resource-group-in-your-azure-subscription"></a><span data-ttu-id="c6851-118">Tworzenie grupy zasobów w Twojej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c6851-118">Create a resource group in your Azure subscription</span></span>
<span data-ttu-id="c6851-119">W poniższym przykładzie pokazano, jak utworzyć grupę zasobów za pomocą skryptu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c6851-119">The following example demonstrates how to create a resource group by using a PowerShell script:</span></span>

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-the-resource-group"></a><span data-ttu-id="c6851-120">Tworzenie zasobu usługi Application Insights w grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="c6851-120">Create an Application Insights resource in the resource group</span></span>
<span data-ttu-id="c6851-121">Na **usługi Application Insights** bloku, wprowadź informacje o zasobie, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c6851-121">On the **Application Insights** blade, enter the information for your resource, as shown in this example:</span></span> 

![Application Insights bloku](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-the-azure-resource-manager-template"></a><span data-ttu-id="c6851-123">Zastosowanie klucza Instrumentacji usługi Application Insights w szablonie usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c6851-123">Apply an Application Insights instrumentation key in the Azure Resource Manager template</span></span>

1. <span data-ttu-id="c6851-124">Jeśli nie zostały jeszcze pobrane szablonu, pobierz go z [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span><span class="sxs-lookup"><span data-stu-id="c6851-124">If you haven't downloaded the template yet, download it from [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span></span>

2. <span data-ttu-id="c6851-125">Znajdź klucz usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c6851-125">Find the Application Insights key.</span></span>
   
   ![Lokalizacja klucza](./media/enable-profiler-compute/copyaikey.png)

3. <span data-ttu-id="c6851-127">Zastąp wartość szablonu.</span><span class="sxs-lookup"><span data-stu-id="c6851-127">Replace the template value.</span></span>
   
   ![Wartość w szablonie](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-to-host-the-web-application"></a><span data-ttu-id="c6851-129">Tworzenie maszyny Wirtualnej platformy Azure w celu hostowania aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="c6851-129">Create an Azure VM to host the web application</span></span>
1. <span data-ttu-id="c6851-130">Utwórz bezpieczny ciąg, aby zapisać hasło.</span><span class="sxs-lookup"><span data-stu-id="c6851-130">Create a secure string to save the password.</span></span>

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. <span data-ttu-id="c6851-131">Wdrażanie szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6851-131">Deploy the Azure Resource Manager template.</span></span>

   <span data-ttu-id="c6851-132">Zmień katalog, w konsoli programu PowerShell do folderu, który zawiera szablon usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6851-132">Change the directory in the PowerShell console to the folder that contains your Resource Manager template.</span></span> <span data-ttu-id="c6851-133">Aby wdrożyć szablon, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c6851-133">To deploy the template, run the following command:</span></span>

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

<span data-ttu-id="c6851-134">Po pomyślnym uruchomieniu skryptu, należy odnaleźć maszyny Wirtualnej o nazwie **MyWindowsVM** w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="c6851-134">After the script runs successfully, you should find a VM named **MyWindowsVM** in your resource group.</span></span>

## <a name="configure-web-deploy-on-the-vm"></a><span data-ttu-id="c6851-135">Konfigurowanie sieci Web wdrażanie na maszynie Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c6851-135">Configure Web Deploy on the VM</span></span>
<span data-ttu-id="c6851-136">Upewnij się, że narzędzia Web Deploy jest włączony na maszynie Wirtualnej, dlatego można opublikować aplikację sieci web w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6851-136">Make sure that Web Deploy is enabled on your VM so you can publish your web application from Visual Studio.</span></span>

<span data-ttu-id="c6851-137">Aby zainstalować narzędzie Web Deploy na maszynie Wirtualnej ręcznie za pośrednictwem WebPI, zobacz [Instalowanie i Konfigurowanie narzędzia Web Deploy w programie IIS 8.0 lub później](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span><span class="sxs-lookup"><span data-stu-id="c6851-137">To install Web Deploy on a VM manually via WebPI, see [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span></span> <span data-ttu-id="c6851-138">Na przykład sposobu automatyzacji instalowanie narzędzia Web Deploy za pomocą szablonu usługi Azure Resource Manager zobacz [tworzenie, konfigurowanie i wdrażanie aplikacji sieci web do maszyny Wirtualnej platformy Azure](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span><span class="sxs-lookup"><span data-stu-id="c6851-138">For an example of how to automate installing Web Deploy by using an Azure Resource Manager template, see [Create, configure, and deploy a web application to an Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span></span>

<span data-ttu-id="c6851-139">Jeśli wdrażasz aplikacji platformy ASP.NET MVC, przejdź do Menedżera serwera, wybierz **Dodaj role i funkcje** > **serwer sieci Web (IIS)** > **serwera sieci Web** > **projektowanie aplikacji**i włączyć funkcję ASP.NET 4.5 na serwerze.</span><span class="sxs-lookup"><span data-stu-id="c6851-139">If you are deploying an ASP.NET MVC application, go to Server Manager, select **Add Roles and Features** > **Web Server (IIS)** > **Web Server** > **Application Development**, and enable ASP.NET 4.5 on your server.</span></span>

![Dodaj ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-the-azure-application-insights-sdk-for-your-project"></a><span data-ttu-id="c6851-141">Zainstaluj zestaw SDK szczegółowych informacji o aplikacji Azure dla projektu</span><span class="sxs-lookup"><span data-stu-id="c6851-141">Install the Azure Application Insights SDK for your project</span></span>
1. <span data-ttu-id="c6851-142">Otwórz aplikację sieci web ASP.NET w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6851-142">Open your ASP.NET web application in Visual Studio.</span></span>

2. <span data-ttu-id="c6851-143">Kliknij prawym przyciskiem myszy projekt i wybierz **Dodaj** > **usług połączonych**.</span><span class="sxs-lookup"><span data-stu-id="c6851-143">Right-click the project and select **Add** > **Connected Services**.</span></span>

3. <span data-ttu-id="c6851-144">Wybierz **usługi Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="c6851-144">Select **Application Insights**.</span></span>

4. <span data-ttu-id="c6851-145">Postępuj zgodnie z instrukcjami na stronie.</span><span class="sxs-lookup"><span data-stu-id="c6851-145">Follow the instructions on the page.</span></span> <span data-ttu-id="c6851-146">Wybierz wcześniej utworzony zasób usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c6851-146">Select the Application Insights resource that you created earlier.</span></span>

5. <span data-ttu-id="c6851-147">Wybierz **zarejestrować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6851-147">Select the **Register** button.</span></span>


## <a name="publish-the-project-to-an-azure-vm"></a><span data-ttu-id="c6851-148">Publikowania projektu na maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c6851-148">Publish the project to an Azure VM</span></span>
<span data-ttu-id="c6851-149">Istnieje kilka sposobów, aby opublikować aplikację na maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c6851-149">There are several ways to publish an application to an Azure VM.</span></span> <span data-ttu-id="c6851-150">Jednym ze sposobów jest używać programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="c6851-150">One way is to use Visual Studio 2017.</span></span>

1. <span data-ttu-id="c6851-151">Kliknij prawym przyciskiem myszy projekt i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="c6851-151">Right-click the project and select **Publish**.</span></span>

2. <span data-ttu-id="c6851-152">Wybierz **maszyny wirtualne Microsoft Azure** jako publikowanie docelowego, a następnie postępuj zgodnie z instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="c6851-152">Select **Microsoft Azure Virtual Machines** as the publish target and follow the steps.</span></span>

   ![Publikowanie FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. <span data-ttu-id="c6851-154">Uruchamianie testów obciążenia względem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6851-154">Run a load test against your application.</span></span> <span data-ttu-id="c6851-155">Wyniki powinny zostać wyświetlone na stronie usługi Application Insights wystąpienia portalu sieci Web.</span><span class="sxs-lookup"><span data-stu-id="c6851-155">You should see results on the Application Insights instance portal webpage.</span></span>


## <a name="enable-the-profiler"></a><span data-ttu-id="c6851-156">Włącz profilera</span><span class="sxs-lookup"><span data-stu-id="c6851-156">Enable the profiler</span></span>
1. <span data-ttu-id="c6851-157">Przejdź do Twojej usługi Application Insights **wydajności** bloku, a następnie wybierz **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="c6851-157">Go to your Application Insights **Performance** blade and select **Configure**.</span></span>
   
   ![Ikona konfigurowania](./media/enable-profiler-compute/enableprofiler1.png)
 
2. <span data-ttu-id="c6851-159">Wybierz **włączyć profilera**.</span><span class="sxs-lookup"><span data-stu-id="c6851-159">Select **Enable Profiler**.</span></span>
   
   ![Włącz ikona profilera](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-to-your-application"></a><span data-ttu-id="c6851-161">Dodaj test wydajności do aplikacji</span><span class="sxs-lookup"><span data-stu-id="c6851-161">Add a performance test to your application</span></span>
<span data-ttu-id="c6851-162">Dlatego firma Microsoft może zbierać przykładowych danych do wyświetlenia w programie Application Insights Profiler, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c6851-162">Follow these steps so we can collect some sample data to be displayed in Application Insights Profiler:</span></span>

1. <span data-ttu-id="c6851-163">Przejdź do zasobu usługi Application Insights, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c6851-163">Browse to the Application Insights resource that you created earlier.</span></span> 

2. <span data-ttu-id="c6851-164">Przejdź do **dostępności** bloku i Dodaj test wydajności, który wysyła żądania sieci web do adres URL aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6851-164">Go to the **Availability** blade and add a performance test that sends web requests to your application URL.</span></span> 

   ![Dodawanie testów wydajności](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a><span data-ttu-id="c6851-166">Wyświetlanie danych dotyczących wydajności</span><span class="sxs-lookup"><span data-stu-id="c6851-166">View your performance data</span></span>

1. <span data-ttu-id="c6851-167">Zaczekaj 10 – 15 minut na profilera do zbierania i analizowania danych.</span><span class="sxs-lookup"><span data-stu-id="c6851-167">Wait 10-15 minutes for the profiler to collect and analyze the data.</span></span> 

2. <span data-ttu-id="c6851-168">Przejdź do **wydajności** bloku zasobu usługi Application Insights i widoku jak aplikacja działa po pod obciążeniem.</span><span class="sxs-lookup"><span data-stu-id="c6851-168">Go to the **Performance** blade in your Application Insights resource and view how your application is performing when it's under load.</span></span>

   ![Wyświetlanie wydajności](./media/enable-profiler-compute/aiperformance.png)

3. <span data-ttu-id="c6851-170">Wybierz ikonę w obszarze **przykłady** otworzyć **widoku śledzenia** bloku.</span><span class="sxs-lookup"><span data-stu-id="c6851-170">Select the icon under **Examples** to open the **Trace View** blade.</span></span>

   ![Otwieranie bloku przeglądania śledzenia](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a><span data-ttu-id="c6851-172">Praca z istniejącego szablonu</span><span class="sxs-lookup"><span data-stu-id="c6851-172">Work with an existing template</span></span>

1. <span data-ttu-id="c6851-173">Zlokalizuj deklaracja zasobów diagnostyki Azure do wdrożenia szablonu.</span><span class="sxs-lookup"><span data-stu-id="c6851-173">Locate the Azure Diagnostics resource declaration in your deployment template.</span></span>
   
   <span data-ttu-id="c6851-174">Jeśli nie masz deklaracji, można utworzyć jedną podobny deklaracji w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c6851-174">If you don't have a declaration, you can create one that resembles the declaration in the following example.</span></span> <span data-ttu-id="c6851-175">Możesz zaktualizować szablon z [Eksploratora zasobów Azure witryny sieci Web](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c6851-175">You can update the template from the [Azure Resource Explorer website](https://resources.azure.com).</span></span>

2. <span data-ttu-id="c6851-176">Zmień wydawcy z `Microsoft.Azure.Diagnostics` do `AIP.Diagnostics.Test`.</span><span class="sxs-lookup"><span data-stu-id="c6851-176">Change the publisher from `Microsoft.Azure.Diagnostics` to `AIP.Diagnostics.Test`.</span></span>

3. <span data-ttu-id="c6851-177">Aby uzyskać `typeHandlerVersion`, użyj `0.0`.</span><span class="sxs-lookup"><span data-stu-id="c6851-177">For `typeHandlerVersion`, use `0.0`.</span></span>

4. <span data-ttu-id="c6851-178">Upewnij się, że `autoUpgradeMinorVersion` ma ustawioną wartość `true`.</span><span class="sxs-lookup"><span data-stu-id="c6851-178">Make sure that `autoUpgradeMinorVersion` is set to `true`.</span></span>

5. <span data-ttu-id="c6851-179">Dodaj nowe `ApplicationInsightsProfiler` wystąpienie obiektu sink `WadCfg` obiekt ustawień, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="c6851-179">Add the new `ApplicationInsightsProfiler` sink instance in the `WadCfg` settings object, as shown in the following example:</span></span>

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

## <a name="enable-the-profiler-on-virtual-machine-scale-sets"></a><span data-ttu-id="c6851-180">Włącz profilera na zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c6851-180">Enable the profiler on virtual machine scale sets</span></span>
<span data-ttu-id="c6851-181">Aby zobaczyć, jak włączyć profilera, Pobierz [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) szablonu.</span><span class="sxs-lookup"><span data-stu-id="c6851-181">To see how to enable the profiler, download the [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) template.</span></span> <span data-ttu-id="c6851-182">Zastosuj te same zmiany w szablonie maszyny Wirtualnej do diagnostyki rozszerzenia zasobu dla zestawu skalowania maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c6851-182">Apply the same changes in a VM template to the diagnostics extension resource for the virtual machine scale set.</span></span>

<span data-ttu-id="c6851-183">Upewnij się, że każde wystąpienie w zestawie skalowania ma dostęp do Internetu.</span><span class="sxs-lookup"><span data-stu-id="c6851-183">Make sure that each instance in the scale set has access to the internet.</span></span> <span data-ttu-id="c6851-184">Agentów Profiler może wysłać zebrane próbki do usługi Application Insights do wyświetlania i analizy.</span><span class="sxs-lookup"><span data-stu-id="c6851-184">The Profiler Agent can then send the collected samples to Application Insights for display and analysis.</span></span>

## <a name="enable-the-profiler-on-service-fabric-applications"></a><span data-ttu-id="c6851-185">Włącz profilera w przypadku aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c6851-185">Enable the profiler on Service Fabric applications</span></span>
1. <span data-ttu-id="c6851-186">Udostępnianie klastra sieci szkieletowej usług rozszerzenie diagnostyki Azure, która instaluje agenta programu Profiler.</span><span class="sxs-lookup"><span data-stu-id="c6851-186">Provision the Service Fabric cluster to have the Azure Diagnostics extension that installs the Profiler Agent.</span></span>

2. <span data-ttu-id="c6851-187">Zainstaluj zestaw SDK usługi Application Insights w projekcie i skonfiguruj klucz usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c6851-187">Install the Application Insights SDK in the project and configure the Application Insights key.</span></span>

3. <span data-ttu-id="c6851-188">Dodaj do dokumentu telemetrii kod aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6851-188">Add application code to instrument telemetry.</span></span>

### <a name="provision-the-service-fabric-cluster-to-have-the-azure-diagnostics-extension-that-installs-the-profiler-agent"></a><span data-ttu-id="c6851-189">Udostępnianie klastra sieci szkieletowej usług rozszerzenie diagnostyki Azure, która instaluje agenta programu Profiler</span><span class="sxs-lookup"><span data-stu-id="c6851-189">Provision the Service Fabric cluster to have the Azure Diagnostics extension that installs the Profiler Agent</span></span>
<span data-ttu-id="c6851-190">Klaster sieci szkieletowej usług może być bezpieczne lub które nie są bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="c6851-190">A Service Fabric cluster can be secure or non-secure.</span></span> <span data-ttu-id="c6851-191">Można ustawić jednego klastra bramy do być niezabezpieczone, więc nie wymaga certyfikatu do dostępu.</span><span class="sxs-lookup"><span data-stu-id="c6851-191">You can set one gateway cluster to be non-secure so it doesn't require a certificate for access.</span></span> <span data-ttu-id="c6851-192">Klastry obsługujące logikę biznesową i danych powinny być bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="c6851-192">Clusters that host business logic and data should be secure.</span></span> <span data-ttu-id="c6851-193">Można włączyć profilera na bezpieczne i niezabezpieczone klastry sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="c6851-193">You can enable the profiler on both secure and non-secure Service Fabric clusters.</span></span> <span data-ttu-id="c6851-194">W tym przewodniku zastosowano niezabezpieczonego klastra jako przykład wyjaśniający, jakie zmiany są wymagane do włączenia profilera.</span><span class="sxs-lookup"><span data-stu-id="c6851-194">This walkthrough uses a non-secure cluster as an example to explain what changes are required to enable the profiler.</span></span> <span data-ttu-id="c6851-195">Bezpieczne klastra można udostępnić w taki sam sposób.</span><span class="sxs-lookup"><span data-stu-id="c6851-195">You can provision a secure cluster in the same way.</span></span>

1. <span data-ttu-id="c6851-196">Pobierz [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span><span class="sxs-lookup"><span data-stu-id="c6851-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span></span> <span data-ttu-id="c6851-197">Tak samo jak dla maszyn wirtualnych i zestawy skalowania maszyny wirtualnej, Zastąp `Application_Insights_Key` z kluczem usługi Application Insights:</span><span class="sxs-lookup"><span data-stu-id="c6851-197">As you did for VMs and virtual machine scale sets, replace `Application_Insights_Key` with your Application Insights key:</span></span>

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

2. <span data-ttu-id="c6851-198">Wdrażanie szablonu przy użyciu skryptu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c6851-198">Deploy the template by using a PowerShell script:</span></span>

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-the-application-insights-sdk-in-the-project-and-configure-the-application-insights-key"></a><span data-ttu-id="c6851-199">Zainstaluj zestaw SDK usługi Application Insights w projekcie i skonfiguruj klucz usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="c6851-199">Install the Application Insights SDK in the project and configure the Application Insights key</span></span>
<span data-ttu-id="c6851-200">Zainstaluj zestaw SDK usługi Application Insights z [pakietu NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="c6851-200">Install the Application Insights SDK from the [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="c6851-201">Upewnij się, czy zainstalować stabilną wersję, 2.3 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="c6851-201">Make sure that you install a stable version, 2.3 or later.</span></span> 

<span data-ttu-id="c6851-202">Aby uzyskać informacje o konfigurowaniu usługi Application Insights w projektach, zobacz [przy użyciu usługi sieć szkieletowa z usługą Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span><span class="sxs-lookup"><span data-stu-id="c6851-202">For information about configuring Application Insights in your projects, see [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span></span>

### <a name="add-application-code-to-instrument-telemetry"></a><span data-ttu-id="c6851-203">Dodaj kod aplikacji, aby dane telemetryczne dokumentu</span><span class="sxs-lookup"><span data-stu-id="c6851-203">Add application code to instrument telemetry</span></span>
1. <span data-ttu-id="c6851-204">Dla dowolnego elementu kodu, który ma zostać Instrumentacja, dodać za pomocą instrukcji wokół niego.</span><span class="sxs-lookup"><span data-stu-id="c6851-204">For any piece of code that you want to instrument, add a using statement around it.</span></span> 

   <span data-ttu-id="c6851-205">W poniższym przykładzie `RunAsync` — metoda jest wykonanie dodatkowych czynności i `telemetryClient` klasy przechwytuje dane telemetryczne po jego uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="c6851-205">In the following  example, the `RunAsync` method is doing some work, and the `telemetryClient` class captures the telemetry after it starts.</span></span> <span data-ttu-id="c6851-206">Zdarzenie musi unikatową nazwę w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6851-206">The event needs a unique name across the application.</span></span>

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

2. <span data-ttu-id="c6851-207">Wdrażanie aplikacji do klastra usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="c6851-207">Deploy your application to the Service Fabric cluster.</span></span> <span data-ttu-id="c6851-208">Poczekaj, aż aplikacji do uruchomienia przez 10 minut.</span><span class="sxs-lookup"><span data-stu-id="c6851-208">Wait for the app to run for 10 minutes.</span></span> <span data-ttu-id="c6851-209">Aby lepiej efekt można uruchomić testu obciążenia w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c6851-209">For better effect, you can run a load test on the app.</span></span> <span data-ttu-id="c6851-210">Przejdź do portalu usługi Application Insights **wydajności** bloku, a powinien przykłady śladów profilowania są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="c6851-210">Go to the Application Insights portal's **Performance** blade, and you should see examples of profiling traces appear.</span></span>

<!---
Commenting out these sections for now
## Enable the Profiler on Cloud Services applications
[TODO]
## Enable the Profiler on classic Azure Virtual Machines
[TODO]
## Enable the Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a><span data-ttu-id="c6851-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6851-211">Next steps</span></span>

- <span data-ttu-id="c6851-212">Znaleźć pomoc dotyczącą rozwiązywania problemów profilera w [profilera Rozwiązywanie problemów z](app-insights-profiler.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="c6851-212">Find help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span></span>

- <span data-ttu-id="c6851-213">Dowiedz się więcej o profilera w [Application Insights profilera](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="c6851-213">Read more about the profiler in [Application Insights Profiler](app-insights-profiler.md).</span></span>
