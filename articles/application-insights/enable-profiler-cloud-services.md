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
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a><span data-ttu-id="8a783-103">Application Insights profilera, Włącz zasobu usługi w chmurze Azure</span><span class="sxs-lookup"><span data-stu-id="8a783-103">Enable Application Insights Profiler on an Azure Cloud Services resource</span></span>

<span data-ttu-id="8a783-104">W tym przewodniku pokazano, jak tooenable Azure Application Insights profilera w aplikacji ASP.NET obsługiwanych przez zasób usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="8a783-104">This walkthrough demonstrates how tooenable Azure Application Insights Profiler on an ASP.NET application hosted by an Azure Cloud Services resource.</span></span> <span data-ttu-id="8a783-105">Przykładami Hello obsługę maszyn wirtualnych platformy Azure, zestawy skalowania maszyny wirtualnej i sieci szkieletowej usług Azure.</span><span class="sxs-lookup"><span data-stu-id="8a783-105">hello examples include support for Azure Virtual Machines, virtual machine scale sets, and Azure Service Fabric.</span></span> <span data-ttu-id="8a783-106">wszystkie przykłady Hello korzystają z szablonów, które obsługują modelu wdrażania usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="8a783-106">hello examples all rely on templates that support hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="8a783-107">Aby uzyskać więcej informacji na temat modelu wdrażania hello Przejrzyj [usługi Azure Resource Manager, a wdrożenie klasyczne: zrozumienie modele wdrażania i stan zasobów hello](/azure-resource-manager/resource-manager-deployment-model).</span><span class="sxs-lookup"><span data-stu-id="8a783-107">For more information about hello deployment model, review [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](/azure-resource-manager/resource-manager-deployment-model).</span></span>

## <a name="overview"></a><span data-ttu-id="8a783-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8a783-108">Overview</span></span>

<span data-ttu-id="8a783-109">powitania po diagram pokazano, jak działa hello profilera dla zasobów usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="8a783-109">hello following diagram illustrates how hello profiler works for Azure Cloud Services resources.</span></span> <span data-ttu-id="8a783-110">Maszyna wirtualna platformy Azure jest używany jako przykład.</span><span class="sxs-lookup"><span data-stu-id="8a783-110">It uses an Azure virtual machine as an example.</span></span>

<span data-ttu-id="8a783-111">![Omówienie](./media/enable-profiler-compute/overview.png) toocollect informacji do przetwarzania i wyświetlania na hello portalu Azure, należy zainstalować składnik agenta diagnostyki hello hello zasobów usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="8a783-111">![Overview](./media/enable-profiler-compute/overview.png) toocollect information for processing and display on hello Azure portal, you must install hello Diagnostics Agent component for hello Azure Cloud Services resources.</span></span> <span data-ttu-id="8a783-112">Witaj rest wskazówki hello znajdują się wskazówki dotyczące tooinstall i skonfigurować tooenable agenta diagnostyki hello Application Insights profilera.</span><span class="sxs-lookup"><span data-stu-id="8a783-112">hello rest of hello walkthrough provides guidance on how tooinstall and configure hello Diagnostics Agent tooenable Application Insights Profiler.</span></span>

## <a name="prerequisites-for-hello-walkthrough"></a><span data-ttu-id="8a783-113">Wymagania wstępne dotyczące hello wskazówki</span><span class="sxs-lookup"><span data-stu-id="8a783-113">Prerequisites for hello walkthrough</span></span>

* <span data-ttu-id="8a783-114">Wdrożenie szablonu usługi Resource Manager, który instaluje agentów profiler hello na powitania maszyn wirtualnych ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) lub skalowanie zestawów ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span><span class="sxs-lookup"><span data-stu-id="8a783-114">A deployment Resource Manager template that installs hello profiler agents on hello VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) or scale sets ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span></span>

* <span data-ttu-id="8a783-115">Wystąpienie usługi Application Insights dla profilowania włączone.</span><span class="sxs-lookup"><span data-stu-id="8a783-115">An Application Insights instance enabled for profiling.</span></span> <span data-ttu-id="8a783-116">Aby uzyskać instrukcje, zobacz [włączyć profil hello](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span><span class="sxs-lookup"><span data-stu-id="8a783-116">For instructions, see [Enable hello profile](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span></span>

* <span data-ttu-id="8a783-117">.NET framework 4.6.1 lub nowszy zainstalowany na powitania docelowego zasobu usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="8a783-117">.NET Framework 4.6.1 or later installed on hello target Azure Cloud Services resource.</span></span>

## <a name="create-a-resource-group-in-your-azure-subscription"></a><span data-ttu-id="8a783-118">Tworzenie grupy zasobów w Twojej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8a783-118">Create a resource group in your Azure subscription</span></span>
<span data-ttu-id="8a783-119">Witaj poniższy przykład pokazuje, jak toocreate zasób grupy za pomocą skryptu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8a783-119">hello following example demonstrates how toocreate a resource group by using a PowerShell script:</span></span>

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a><span data-ttu-id="8a783-120">Tworzenie zasobu usługi Application Insights w grupie zasobów hello</span><span class="sxs-lookup"><span data-stu-id="8a783-120">Create an Application Insights resource in hello resource group</span></span>
<span data-ttu-id="8a783-121">Na powitania **usługi Application Insights** bloku, wprowadź hello informacje o zasobie, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="8a783-121">On hello **Application Insights** blade, enter hello information for your resource, as shown in this example:</span></span> 

![Application Insights bloku](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a><span data-ttu-id="8a783-123">Zastosowanie klucza Instrumentacji usługi Application Insights w szablonie usługi Azure Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="8a783-123">Apply an Application Insights instrumentation key in hello Azure Resource Manager template</span></span>

1. <span data-ttu-id="8a783-124">Jeśli nie zostały jeszcze pobrane hello szablonu, pobierz go z [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span><span class="sxs-lookup"><span data-stu-id="8a783-124">If you haven't downloaded hello template yet, download it from [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span></span>

2. <span data-ttu-id="8a783-125">Znajdowanie hello klucza usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8a783-125">Find hello Application Insights key.</span></span>
   
   ![Lokalizacja hello klucza](./media/enable-profiler-compute/copyaikey.png)

3. <span data-ttu-id="8a783-127">Zastąp wartość szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="8a783-127">Replace hello template value.</span></span>
   
   ![Wartość w hello szablonu](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a><span data-ttu-id="8a783-129">Tworzenie aplikacji sieci web hello toohost maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="8a783-129">Create an Azure VM toohost hello web application</span></span>
1. <span data-ttu-id="8a783-130">Utwórz hasło hello toosave bezpieczny ciąg.</span><span class="sxs-lookup"><span data-stu-id="8a783-130">Create a secure string toosave hello password.</span></span>

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. <span data-ttu-id="8a783-131">Wdrażanie szablonu usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="8a783-131">Deploy hello Azure Resource Manager template.</span></span>

   <span data-ttu-id="8a783-132">Zmień katalog hello w folderze toohello konsoli programu PowerShell hello, który zawiera szablon usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8a783-132">Change hello directory in hello PowerShell console toohello folder that contains your Resource Manager template.</span></span> <span data-ttu-id="8a783-133">toodeploy hello szablon, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="8a783-133">toodeploy hello template, run hello following command:</span></span>

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

<span data-ttu-id="8a783-134">Po pomyślnym uruchomieniu skryptu hello powinien znajdować się maszyny Wirtualnej o nazwie **MyWindowsVM** w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="8a783-134">After hello script runs successfully, you should find a VM named **MyWindowsVM** in your resource group.</span></span>

## <a name="configure-web-deploy-on-hello-vm"></a><span data-ttu-id="8a783-135">Konfiguruje narzędzie Web Deploy na powitania maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="8a783-135">Configure Web Deploy on hello VM</span></span>
<span data-ttu-id="8a783-136">Upewnij się, że narzędzia Web Deploy jest włączony na maszynie Wirtualnej, dlatego można opublikować aplikację sieci web w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8a783-136">Make sure that Web Deploy is enabled on your VM so you can publish your web application from Visual Studio.</span></span>

<span data-ttu-id="8a783-137">tooinstall narzędzia Web Deploy na maszynie Wirtualnej ręcznie za pośrednictwem WebPI, zobacz [Instalowanie i Konfigurowanie narzędzia Web Deploy w programie IIS 8.0 lub później](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span><span class="sxs-lookup"><span data-stu-id="8a783-137">tooinstall Web Deploy on a VM manually via WebPI, see [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span></span> <span data-ttu-id="8a783-138">Na przykład jak tooautomate instalowanie narzędzia Web Deploy za pomocą szablonu usługi Azure Resource Manager, zobacz [tworzenie, konfigurowanie i wdrażanie tooan aplikacji sieci web Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span><span class="sxs-lookup"><span data-stu-id="8a783-138">For an example of how tooautomate installing Web Deploy by using an Azure Resource Manager template, see [Create, configure, and deploy a web application tooan Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span></span>

<span data-ttu-id="8a783-139">Jeśli wdrażasz aplikacji platformy ASP.NET MVC, przejdź tooServer Manager, wybierz **Dodaj role i funkcje** > **serwer sieci Web (IIS)** > **serwera sieci Web**  >  **Projektowanie aplikacji**i Włącz funkcję ASP.NET 4.5 na serwerze.</span><span class="sxs-lookup"><span data-stu-id="8a783-139">If you are deploying an ASP.NET MVC application, go tooServer Manager, select **Add Roles and Features** > **Web Server (IIS)** > **Web Server** > **Application Development**, and enable ASP.NET 4.5 on your server.</span></span>

![Dodaj ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a><span data-ttu-id="8a783-141">Zainstaluj hello zestaw SDK usługi Azure Application Insights do projektu</span><span class="sxs-lookup"><span data-stu-id="8a783-141">Install hello Azure Application Insights SDK for your project</span></span>
1. <span data-ttu-id="8a783-142">Otwórz aplikację sieci web ASP.NET w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8a783-142">Open your ASP.NET web application in Visual Studio.</span></span>

2. <span data-ttu-id="8a783-143">Kliknij prawym przyciskiem myszy projekt hello i wybierz **Dodaj** > **usług połączonych**.</span><span class="sxs-lookup"><span data-stu-id="8a783-143">Right-click hello project and select **Add** > **Connected Services**.</span></span>

3. <span data-ttu-id="8a783-144">Wybierz **usługi Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="8a783-144">Select **Application Insights**.</span></span>

4. <span data-ttu-id="8a783-145">Wykonaj instrukcje hello na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="8a783-145">Follow hello instructions on hello page.</span></span> <span data-ttu-id="8a783-146">Wybierz zasób usługi Application Insights hello, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="8a783-146">Select hello Application Insights resource that you created earlier.</span></span>

5. <span data-ttu-id="8a783-147">Wybierz hello **zarejestrować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8a783-147">Select hello **Register** button.</span></span>


## <a name="publish-hello-project-tooan-azure-vm"></a><span data-ttu-id="8a783-148">Publikowanie hello projektu tooan maszyny Wirtualnej Azure</span><span class="sxs-lookup"><span data-stu-id="8a783-148">Publish hello project tooan Azure VM</span></span>
<span data-ttu-id="8a783-149">Istnieje kilka sposobów toopublish tooan aplikacji maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8a783-149">There are several ways toopublish an application tooan Azure VM.</span></span> <span data-ttu-id="8a783-150">Jednym ze sposobów jest toouse programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8a783-150">One way is toouse Visual Studio 2017.</span></span>

1. <span data-ttu-id="8a783-151">Kliknij prawym przyciskiem myszy projekt hello i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="8a783-151">Right-click hello project and select **Publish**.</span></span>

2. <span data-ttu-id="8a783-152">Wybierz **maszyny wirtualne Microsoft Azure** jako hello publikowanie docelowego i wykonaj kroki hello.</span><span class="sxs-lookup"><span data-stu-id="8a783-152">Select **Microsoft Azure Virtual Machines** as hello publish target and follow hello steps.</span></span>

   ![Publikowanie FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. <span data-ttu-id="8a783-154">Uruchamianie testów obciążenia względem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8a783-154">Run a load test against your application.</span></span> <span data-ttu-id="8a783-155">Wyniki powinny być widoczne w portalu sieci Web hello usługi Application Insights wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="8a783-155">You should see results on hello Application Insights instance portal webpage.</span></span>


## <a name="enable-hello-profiler"></a><span data-ttu-id="8a783-156">Włącz hello profilera</span><span class="sxs-lookup"><span data-stu-id="8a783-156">Enable hello profiler</span></span>
1. <span data-ttu-id="8a783-157">Przejdź do usługi Application Insights tooyour **wydajności** bloku, a następnie wybierz **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="8a783-157">Go tooyour Application Insights **Performance** blade and select **Configure**.</span></span>
   
   ![Ikona konfigurowania](./media/enable-profiler-compute/enableprofiler1.png)
 
2. <span data-ttu-id="8a783-159">Wybierz **włączyć profilera**.</span><span class="sxs-lookup"><span data-stu-id="8a783-159">Select **Enable Profiler**.</span></span>
   
   ![Włącz ikona profilera](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a><span data-ttu-id="8a783-161">Dodawanie aplikacji tooyour testów wydajności</span><span class="sxs-lookup"><span data-stu-id="8a783-161">Add a performance test tooyour application</span></span>
<span data-ttu-id="8a783-162">Dlatego firma Microsoft może zbierać niektórych toobe dane przykładowe wyświetlane w programie Application Insights Profiler, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8a783-162">Follow these steps so we can collect some sample data toobe displayed in Application Insights Profiler:</span></span>

1. <span data-ttu-id="8a783-163">Przeglądaj toohello zasobu usługi Application Insights, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="8a783-163">Browse toohello Application Insights resource that you created earlier.</span></span> 

2. <span data-ttu-id="8a783-164">Przejdź toohello **dostępności** bloku i Dodaj test wydajności, który wysyła adres URL aplikacji tooyour żądania sieci web.</span><span class="sxs-lookup"><span data-stu-id="8a783-164">Go toohello **Availability** blade and add a performance test that sends web requests tooyour application URL.</span></span> 

   ![Dodawanie testów wydajności](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a><span data-ttu-id="8a783-166">Wyświetlanie danych dotyczących wydajności</span><span class="sxs-lookup"><span data-stu-id="8a783-166">View your performance data</span></span>

1. <span data-ttu-id="8a783-167">Zaczekaj 10 – 15 minut na toocollect profilera hello i analizowanie danych hello.</span><span class="sxs-lookup"><span data-stu-id="8a783-167">Wait 10-15 minutes for hello profiler toocollect and analyze hello data.</span></span> 

2. <span data-ttu-id="8a783-168">Przejdź toohello **wydajności** bloku zasobu usługi Application Insights i widoku jak aplikacja działa po pod obciążeniem.</span><span class="sxs-lookup"><span data-stu-id="8a783-168">Go toohello **Performance** blade in your Application Insights resource and view how your application is performing when it's under load.</span></span>

   ![Wyświetlanie wydajności](./media/enable-profiler-compute/aiperformance.png)

3. <span data-ttu-id="8a783-170">Witaj wybierz ikonę w obszarze **przykłady** tooopen hello **widoku śledzenia** bloku.</span><span class="sxs-lookup"><span data-stu-id="8a783-170">Select hello icon under **Examples** tooopen hello **Trace View** blade.</span></span>

   ![Otwieranie bloku przeglądania śledzenia hello](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a><span data-ttu-id="8a783-172">Praca z istniejącego szablonu</span><span class="sxs-lookup"><span data-stu-id="8a783-172">Work with an existing template</span></span>

1. <span data-ttu-id="8a783-173">Zlokalizuj deklaracja zasobów Azure Diagnostics hello w szablonie wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="8a783-173">Locate hello Azure Diagnostics resource declaration in your deployment template.</span></span>
   
   <span data-ttu-id="8a783-174">Jeśli nie masz deklaracji, można utworzyć jedną podobny hello deklaracji w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="8a783-174">If you don't have a declaration, you can create one that resembles hello declaration in hello following example.</span></span> <span data-ttu-id="8a783-175">Można aktualizować hello szablonu z hello [Eksploratora zasobów Azure witryny sieci Web](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8a783-175">You can update hello template from hello [Azure Resource Explorer website](https://resources.azure.com).</span></span>

2. <span data-ttu-id="8a783-176">Wydawca zmiany hello z `Microsoft.Azure.Diagnostics` zbyt`AIP.Diagnostics.Test`.</span><span class="sxs-lookup"><span data-stu-id="8a783-176">Change hello publisher from `Microsoft.Azure.Diagnostics` too`AIP.Diagnostics.Test`.</span></span>

3. <span data-ttu-id="8a783-177">Aby uzyskać `typeHandlerVersion`, użyj `0.0`.</span><span class="sxs-lookup"><span data-stu-id="8a783-177">For `typeHandlerVersion`, use `0.0`.</span></span>

4. <span data-ttu-id="8a783-178">Upewnij się, że `autoUpgradeMinorVersion` ustawiono zbyt`true`.</span><span class="sxs-lookup"><span data-stu-id="8a783-178">Make sure that `autoUpgradeMinorVersion` is set too`true`.</span></span>

5. <span data-ttu-id="8a783-179">Dodaj nowy hello `ApplicationInsightsProfiler` wystąpienie obiektu sink hello `WadCfg` obiekt ustawień, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="8a783-179">Add hello new `ApplicationInsightsProfiler` sink instance in hello `WadCfg` settings object, as shown in hello following example:</span></span>

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

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a><span data-ttu-id="8a783-180">Włącz profilera hello na zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="8a783-180">Enable hello profiler on virtual machine scale sets</span></span>
<span data-ttu-id="8a783-181">toosee jak tooenable hello profilera, Pobierz hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) szablonu.</span><span class="sxs-lookup"><span data-stu-id="8a783-181">toosee how tooenable hello profiler, download hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) template.</span></span> <span data-ttu-id="8a783-182">Zastosuj hello same zmiany w zasobie rozszerzenia diagnostyki toohello szablonu maszyny Wirtualnej dla zestawu skalowania maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="8a783-182">Apply hello same changes in a VM template toohello diagnostics extension resource for hello virtual machine scale set.</span></span>

<span data-ttu-id="8a783-183">Upewnij się, że każde wystąpienie w zestawie skalowania hello ma toohello dostęp do Internetu.</span><span class="sxs-lookup"><span data-stu-id="8a783-183">Make sure that each instance in hello scale set has access toohello internet.</span></span> <span data-ttu-id="8a783-184">Hello agentów Profiler może następnie wyślij próbki hello zbierane tooApplication wgląd do wyświetlania i analizy.</span><span class="sxs-lookup"><span data-stu-id="8a783-184">hello Profiler Agent can then send hello collected samples tooApplication Insights for display and analysis.</span></span>

## <a name="enable-hello-profiler-on-service-fabric-applications"></a><span data-ttu-id="8a783-185">Włącz profilera hello w przypadku aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="8a783-185">Enable hello profiler on Service Fabric applications</span></span>
1. <span data-ttu-id="8a783-186">Hello świadczenia usługi sieć szkieletowa klastra toohave hello Azure Diagnostics rozszerzenia, które instaluje hello agentów Profiler.</span><span class="sxs-lookup"><span data-stu-id="8a783-186">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent.</span></span>

2. <span data-ttu-id="8a783-187">Zainstaluj hello zestaw SDK usługi Application Insights w projekcie hello i skonfiguruj hello klucza usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8a783-187">Install hello Application Insights SDK in hello project and configure hello Application Insights key.</span></span>

3. <span data-ttu-id="8a783-188">Dodaj telemetrię tooinstrument kodu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8a783-188">Add application code tooinstrument telemetry.</span></span>

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a><span data-ttu-id="8a783-189">Zainicjuj obsługę hello sieci szkieletowej usług klastra toohave hello rozszerzenia diagnostyki Azure, które instaluje hello agentów Profiler</span><span class="sxs-lookup"><span data-stu-id="8a783-189">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent</span></span>
<span data-ttu-id="8a783-190">Klaster sieci szkieletowej usług może być bezpieczne lub które nie są bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="8a783-190">A Service Fabric cluster can be secure or non-secure.</span></span> <span data-ttu-id="8a783-191">Można ustawić jedną toobe klastra bramy niezabezpieczone, certyfikat nie wymaga dostępu.</span><span class="sxs-lookup"><span data-stu-id="8a783-191">You can set one gateway cluster toobe non-secure so it doesn't require a certificate for access.</span></span> <span data-ttu-id="8a783-192">Klastry obsługujące logikę biznesową i danych powinny być bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="8a783-192">Clusters that host business logic and data should be secure.</span></span> <span data-ttu-id="8a783-193">Można włączyć profilera hello na bezpieczne i niezabezpieczone klastry sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="8a783-193">You can enable hello profiler on both secure and non-secure Service Fabric clusters.</span></span> <span data-ttu-id="8a783-194">W tym przewodniku zastosowano niezabezpieczonego klastra jako przykład tooexplain, jakie zmiany są wymagane tooenable hello profilera.</span><span class="sxs-lookup"><span data-stu-id="8a783-194">This walkthrough uses a non-secure cluster as an example tooexplain what changes are required tooenable hello profiler.</span></span> <span data-ttu-id="8a783-195">Umożliwia obsługę bezpiecznej klastra w hello tak samo.</span><span class="sxs-lookup"><span data-stu-id="8a783-195">You can provision a secure cluster in hello same way.</span></span>

1. <span data-ttu-id="8a783-196">Pobierz [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span><span class="sxs-lookup"><span data-stu-id="8a783-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span></span> <span data-ttu-id="8a783-197">Tak samo jak dla maszyn wirtualnych i zestawy skalowania maszyny wirtualnej, Zastąp `Application_Insights_Key` z kluczem usługi Application Insights:</span><span class="sxs-lookup"><span data-stu-id="8a783-197">As you did for VMs and virtual machine scale sets, replace `Application_Insights_Key` with your Application Insights key:</span></span>

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

2. <span data-ttu-id="8a783-198">Wdrażanie szablonu hello przy użyciu skryptu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8a783-198">Deploy hello template by using a PowerShell script:</span></span>

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a><span data-ttu-id="8a783-199">Zainstaluj hello zestaw SDK usługi Application Insights w projekcie hello i skonfiguruj hello klucza usługi Application Insights</span><span class="sxs-lookup"><span data-stu-id="8a783-199">Install hello Application Insights SDK in hello project and configure hello Application Insights key</span></span>
<span data-ttu-id="8a783-200">Zainstaluj zestaw SDK usługi Application Insights hello z hello [pakietu NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="8a783-200">Install hello Application Insights SDK from hello [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="8a783-201">Upewnij się, czy zainstalować stabilną wersję, 2.3 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="8a783-201">Make sure that you install a stable version, 2.3 or later.</span></span> 

<span data-ttu-id="8a783-202">Aby uzyskać informacje o konfigurowaniu usługi Application Insights w projektach, zobacz [przy użyciu usługi sieć szkieletowa z usługą Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span><span class="sxs-lookup"><span data-stu-id="8a783-202">For information about configuring Application Insights in your projects, see [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span></span>

### <a name="add-application-code-tooinstrument-telemetry"></a><span data-ttu-id="8a783-203">Dodaj telemetrię tooinstrument kodu aplikacji</span><span class="sxs-lookup"><span data-stu-id="8a783-203">Add application code tooinstrument telemetry</span></span>
1. <span data-ttu-id="8a783-204">Dla części kodu, które mają tooinstrument dodać za pomocą instrukcji wokół niego.</span><span class="sxs-lookup"><span data-stu-id="8a783-204">For any piece of code that you want tooinstrument, add a using statement around it.</span></span> 

   <span data-ttu-id="8a783-205">W hello poniższy przykład, hello `RunAsync` metody jest wykonanie dodatkowych czynności, a hello `telemetryClient` klasy przechwytuje dane telemetryczne powitania po jego uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="8a783-205">In hello following  example, hello `RunAsync` method is doing some work, and hello `telemetryClient` class captures hello telemetry after it starts.</span></span> <span data-ttu-id="8a783-206">Zdarzenie Hello musi unikatową nazwę w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8a783-206">hello event needs a unique name across hello application.</span></span>

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

2. <span data-ttu-id="8a783-207">Wdrażanie klastra usługi sieć szkieletowa toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8a783-207">Deploy your application toohello Service Fabric cluster.</span></span> <span data-ttu-id="8a783-208">Poczekaj toorun aplikacji hello przez 10 minut.</span><span class="sxs-lookup"><span data-stu-id="8a783-208">Wait for hello app toorun for 10 minutes.</span></span> <span data-ttu-id="8a783-209">Aby lepiej efekt można uruchomić testu obciążenia w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8a783-209">For better effect, you can run a load test on hello app.</span></span> <span data-ttu-id="8a783-210">Portal usługi Application Insights Przejdź toohello **wydajności** bloku, a powinien przykłady śladów profilowania są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="8a783-210">Go toohello Application Insights portal's **Performance** blade, and you should see examples of profiling traces appear.</span></span>

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a><span data-ttu-id="8a783-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8a783-211">Next steps</span></span>

- <span data-ttu-id="8a783-212">Znaleźć pomoc dotyczącą rozwiązywania problemów profilera w [profilera Rozwiązywanie problemów z](app-insights-profiler.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="8a783-212">Find help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span></span>

- <span data-ttu-id="8a783-213">Dowiedz się więcej o profilera hello w [Application Insights profilera](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="8a783-213">Read more about hello profiler in [Application Insights Profiler](app-insights-profiler.md).</span></span>
