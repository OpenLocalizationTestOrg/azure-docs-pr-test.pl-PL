---
title: "operacje aaaDeployment z usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak hello tooview operacje wdrażania usługi Azure Resource Manager z portalu, programu PowerShell, interfejsu wiersza polecenia Azure i interfejsu API REST."
services: azure-resource-manager,virtual-machines
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: infrastructure
ms.date: 01/13/2017
ms.author: tomfitz
ms.openlocfilehash: ba4823ca73caca83dfc07c99d736344ef8b7b54d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="ca710-103">Operacje wdrażania widoku z usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ca710-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="ca710-104">Można wyświetlić operacje hello wdrożenia za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ca710-104">You can view hello operations for a deployment through hello Azure portal.</span></span> <span data-ttu-id="ca710-105">Może być najbardziej interesujące wyświetlanie hello operacji, gdy otrzymano wystąpił błąd podczas wdrażania, ten artykuł skupia się na wyświetlanie operacje, które nie powiodły.</span><span class="sxs-lookup"><span data-stu-id="ca710-105">You may be most interested in viewing hello operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="ca710-106">Hello portal udostępnia interfejs, który umożliwia tooeasily Znajdź hello błędów, aby ustalić możliwe rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ca710-106">hello portal provides an interface that enables you tooeasily find hello errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="ca710-107">Portal</span><span class="sxs-lookup"><span data-stu-id="ca710-107">Portal</span></span>
<span data-ttu-id="ca710-108">operacje wdrażania hello toosee, użyj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ca710-108">toosee hello deployment operations, use hello following steps:</span></span>

1. <span data-ttu-id="ca710-109">Dla grupy zasobów hello objętego wdrożenia hello Zwróć uwagę, stan hello hello ostatniego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ca710-109">For hello resource group involved in hello deployment, notice hello status of hello last deployment.</span></span> <span data-ttu-id="ca710-110">Ten stan tooget można wybrać więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="ca710-110">You can select this status tooget more details.</span></span>
   
    ![Stan wdrożenia](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="ca710-112">Możesz sprawdzić hello niedawną historię wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ca710-112">You see hello recent deployment history.</span></span> <span data-ttu-id="ca710-113">Wybierz wdrożenie hello, które zakończyły się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="ca710-113">Select hello deployment that failed.</span></span>
   
    ![Stan wdrożenia](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="ca710-115">Wybierz toosee łącze hello opis dlaczego hello wdrażanie nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="ca710-115">Select hello link toosee a description of why hello deployment failed.</span></span> <span data-ttu-id="ca710-116">W poniższym obrazie hello hello rekord DNS nie jest unikatowa.</span><span class="sxs-lookup"><span data-stu-id="ca710-116">In hello image below, hello DNS record is not unique.</span></span>  
   
    ![Wyświetl wdrożenia nie powiodło się](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="ca710-118">Ten komunikat o błędzie powinny wystarczyć dla Ciebie toobegin rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="ca710-118">This error message should be enough for you toobegin troubleshooting.</span></span> <span data-ttu-id="ca710-119">Jednak jeśli potrzebujesz więcej szczegółów, o których zadania zostały ukończone, można wyświetlić operacje hello pokazane na powitania następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="ca710-119">However, if you need more details about which tasks were completed, you can view hello operations as shown in hello following steps.</span></span>
4. <span data-ttu-id="ca710-120">Można wyświetlić wszystkie operacje wdrażania hello w hello **wdrożenia** bloku.</span><span class="sxs-lookup"><span data-stu-id="ca710-120">You can view all hello deployment operations in hello **Deployment** blade.</span></span> <span data-ttu-id="ca710-121">Wybierz wszystkie toosee operacji więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="ca710-121">Select any operation toosee more details.</span></span>
   
    ![Wyświetlanie operacji](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="ca710-123">W takim przypadku zobaczysz, że hello konta magazynu, sieci wirtualnej i zestawu dostępności zostały pomyślnie utworzone.</span><span class="sxs-lookup"><span data-stu-id="ca710-123">In this case, you see that hello storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="ca710-124">Hello publiczny adres IP nie powiodło się, a nie podjęto inne zasoby.</span><span class="sxs-lookup"><span data-stu-id="ca710-124">hello public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="ca710-125">Można wyświetlać zdarzenia hello wdrożenia, wybierając **zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="ca710-125">You can view events for hello deployment by selecting **Events**.</span></span>
   
    ![Wyświetl zdarzenia](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="ca710-127">Zobacz wszystkie zdarzenia hello hello wdrożenia i zaznacz jeden więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="ca710-127">You see all hello events for hello deployment and select any one for more details.</span></span> <span data-ttu-id="ca710-128">Zwróć uwagę, zbyt hello identyfikatorów korelacji.</span><span class="sxs-lookup"><span data-stu-id="ca710-128">Notice too hello correlation IDs.</span></span> <span data-ttu-id="ca710-129">Ta wartość może być przydatne podczas pracy z działem pomocy technicznej tootroubleshoot wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ca710-129">This value can be helpful when working with technical support tootroubleshoot a deployment.</span></span>
   
    ![Zobacz zdarzenia](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="ca710-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca710-131">PowerShell</span></span>
1. <span data-ttu-id="ca710-132">ogólny stan wdrożenia, użyj hello hello tooget **Get-AzureRmResourceGroupDeployment** polecenia.</span><span class="sxs-lookup"><span data-stu-id="ca710-132">tooget hello overall status of a deployment, use hello **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="ca710-133">Alternatywnie można filtrować wyniki hello tylko wdrożenia, które nie powiodły.</span><span class="sxs-lookup"><span data-stu-id="ca710-133">Or, you can filter hello results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="ca710-134">Dla każdego wdrożenia zawiera wiele operacji.</span><span class="sxs-lookup"><span data-stu-id="ca710-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="ca710-135">Każda operacja reprezentuje krokiem w procesie wdrażania hello.</span><span class="sxs-lookup"><span data-stu-id="ca710-135">Each operation represents a step in hello deployment process.</span></span> <span data-ttu-id="ca710-136">toodiscover co poszło problem z wdrożeniem, należy zwykle toosee szczegóły hello operacje wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ca710-136">toodiscover what went wrong with a deployment, you usually need toosee details about hello deployment operations.</span></span> <span data-ttu-id="ca710-137">Można wyświetlić stan hello operacji hello z **Get-AzureRmResourceGroupDeploymentOperation**.</span><span class="sxs-lookup"><span data-stu-id="ca710-137">You can see hello status of hello operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="ca710-138">Polecenie to zwraca wiele operacji z każdym z nich hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="ca710-138">Which returns multiple operations with each one in hello following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="ca710-139">tooget więcej szczegółów na temat nieudane operacje pobierania właściwości powitania dla operacji o **** stanu.</span><span class="sxs-lookup"><span data-stu-id="ca710-139">tooget more details about failed operations, retrieve hello properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="ca710-140">Które zwraca wszystkie hello nieudane operacje z każdą z nich w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="ca710-140">Which returns all hello failed operations with each one in hello following format:</span></span>

  ```powershell
  provisioningOperation : Create
  provisioningState     : Failed
  timestamp             : 2016-06-14T21:54:55.1468068Z
  duration              : PT3.1449887S
  trackingId            : f4ed72f8-4203-43dc-958a-15d041e8c233
  serviceRequestId      : a426f689-5d5a-448d-a2f0-9784d14c900a
  statusCode            : BadRequest
  statusMessage         : @{error=}
  targetResource        : @{id=/subscriptions/{guid}/resourceGroups/ExampleGroup/providers/
                          Microsoft.Network/publicIPAddresses/myPublicIP;
                          resourceType=Microsoft.Network/publicIPAddresses; resourceName=myPublicIP}
  ```

    <span data-ttu-id="ca710-141">Zanotuj hello serviceRequestId i trackingId hello hello operacji.</span><span class="sxs-lookup"><span data-stu-id="ca710-141">Note hello serviceRequestId and hello trackingId for hello operation.</span></span> <span data-ttu-id="ca710-142">Witaj serviceRequestId mogą być pomocne podczas pracy z działem pomocy technicznej tootroubleshoot wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ca710-142">hello serviceRequestId can be helpful when working with technical support tootroubleshoot a deployment.</span></span> <span data-ttu-id="ca710-143">Użyjesz hello trackingId w hello następny krok toofocus na określonej operacji.</span><span class="sxs-lookup"><span data-stu-id="ca710-143">You will use hello trackingId in hello next step toofocus on a particular operation.</span></span>
4. <span data-ttu-id="ca710-144">tooget hello komunikatu o stanie określonej operacji nie powiodło się, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ca710-144">tooget hello status message of a particular failed operation, use hello following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="ca710-145">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="ca710-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="ca710-146">Każda operacja wdrażania na platformie Azure jest przechowywana zawartość żądania i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="ca710-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="ca710-147">zawartość żądania Hello jest co wysłano tooAzure podczas wdrażania (na przykład utworzyć Maszynę wirtualną, dysk systemu operacyjnego i innych zasobów).</span><span class="sxs-lookup"><span data-stu-id="ca710-147">hello request content is what you sent tooAzure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="ca710-148">zawartość odpowiedzi Hello jest Azure wysyłane z żądania wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ca710-148">hello response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="ca710-149">Podczas wdrażania można używać **DeploymentDebugLogLevel** toospecify paramenter, który hello żądań i/lub odpowiedzi są przechowywane w dzienniku hello.</span><span class="sxs-lookup"><span data-stu-id="ca710-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter toospecify that hello request and/or response are retained in hello log.</span></span> 

  <span data-ttu-id="ca710-150">Uzyskiwanie informacji z dziennika hello i zapisać go lokalnie, używając następujących poleceń programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="ca710-150">You get that information from hello log, and save it locally by using hello following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="ca710-151">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ca710-151">Azure CLI</span></span>

1. <span data-ttu-id="ca710-152">Pobierz hello ogólny stan wdrożenia z hello **Pokaż wdrożenia grupy azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="ca710-152">Get hello overall status of a deployment with hello **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="ca710-153">Jednym z hello zwracane wartości jest hello **correlationId**.</span><span class="sxs-lookup"><span data-stu-id="ca710-153">One of hello returned values is hello **correlationId**.</span></span> <span data-ttu-id="ca710-154">Ta wartość jest używana zdarzenia związane z tootrack i może być przydatne w przypadku pracy z tootroubleshoot pomocy technicznej wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ca710-154">This value is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="ca710-155">Użyj operacji hello toosee w przypadku wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="ca710-155">toosee hello operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="ca710-156">REST</span><span class="sxs-lookup"><span data-stu-id="ca710-156">REST</span></span>

1. <span data-ttu-id="ca710-157">Uzyskiwanie informacji o wdrażaniu z hello [uzyskać informacje na temat wdrażania szablonu](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operacji.</span><span class="sxs-lookup"><span data-stu-id="ca710-157">Get information about a deployment with hello [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="ca710-158">W odpowiedzi hello, należy pamiętać, w szczególności hello **provisioningState**, **correlationId**, i **błąd** elementów.</span><span class="sxs-lookup"><span data-stu-id="ca710-158">In hello response, note in particular hello **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="ca710-159">Witaj **correlationId** służy zdarzenia związane z tootrack i może być przydatne w przypadku pracy z tootroubleshoot pomocy technicznej wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ca710-159">hello **correlationId** is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

  ```json
  { 
    ...
    "properties": {
      "provisioningState":"Failed",
      "correlationId":"d5062e45-6e9f-4fd3-a0a0-6b2c56b15757",
      ...
      "error":{
        "code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see http://aka.ms/arm-debug for usage details.",
        "details":[{"code":"Conflict","message":"{\r\n  \"error\": {\r\n    \"message\": \"Conflict\",\r\n    \"code\": \"Conflict\"\r\n  }\r\n}"}]
      }  
    }
  }
  ```

2. <span data-ttu-id="ca710-160">Pobierz informacje o operacji wdrażania z hello [listy wszystkich operacji wdrożenia szablonu](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operacji.</span><span class="sxs-lookup"><span data-stu-id="ca710-160">Get information about deployment operations with hello [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="ca710-161">odpowiedź Hello zawiera informacje żądania i/lub odpowiedzi, w zależności od określonych w hello **debugSetting** właściwości podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ca710-161">hello response includes request and/or response information based on what you specified in hello **debugSetting** property during deployment.</span></span>

  ```json
  {
    ...
    "properties": 
    {
      ...
      "request":{
        "content":{
          "location":"West US",
          "properties":{
            "accountType": "Standard_LRS"
          }
        }
      },
      "response":{
        "content":{
          "error":{
            "message":"Conflict","code":"Conflict"
          }
        }
      }
    }
  }
  ```


## <a name="next-steps"></a><span data-ttu-id="ca710-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ca710-162">Next steps</span></span>
* <span data-ttu-id="ca710-163">Aby uzyskać pomoc przy rozwiązywaniu problemów z błędami konkretnego wdrożenia, zobacz [Rozwiąż typowe błędy podczas wdrażania tooAzure zasobów z usługi Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="ca710-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="ca710-164">toolearn o używaniu hello działania w dziennikach toomonitor inne typy akcji, zobacz [toomanage Azure Dzienniki aktywności widok zasobów](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="ca710-164">toolearn about using hello activity logs toomonitor other types of actions, see [View activity logs toomanage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="ca710-165">Zobacz wdrożenia przed jego wykonaniem toovalidate [wdrażanie grupy zasobów za pomocą szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ca710-165">toovalidate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

