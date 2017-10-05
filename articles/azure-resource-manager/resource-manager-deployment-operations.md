---
title: "Operacje wdrażania z usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Opisuje sposób wyświetlania operacje wdrażania usługi Azure Resource Manager z portalu, programu PowerShell, interfejsu wiersza polecenia Azure i interfejsu API REST."
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
ms.openlocfilehash: fb6b3b357fd1f66184e480115a9c863ba31ac193
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="f2893-103">Operacje wdrażania widoku z usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f2893-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="f2893-104">Można wyświetlić operacje wdrożenia za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f2893-104">You can view the operations for a deployment through the Azure portal.</span></span> <span data-ttu-id="f2893-105">Może być najbardziej interesujące wyświetlanie operacje, gdy otrzymano wystąpił błąd podczas wdrażania, ten artykuł skupia się na wyświetlanie operacje, które nie powiodły.</span><span class="sxs-lookup"><span data-stu-id="f2893-105">You may be most interested in viewing the operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="f2893-106">Portal zawiera interfejs, który umożliwia łatwe znajdowanie błędów i ustalić potencjalne rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f2893-106">The portal provides an interface that enables you to easily find the errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="f2893-107">Portal</span><span class="sxs-lookup"><span data-stu-id="f2893-107">Portal</span></span>
<span data-ttu-id="f2893-108">Aby wyświetlić operacje wdrażania, użyj następujących kroków:</span><span class="sxs-lookup"><span data-stu-id="f2893-108">To see the deployment operations, use the following steps:</span></span>

1. <span data-ttu-id="f2893-109">Dla grupy zasobów objętego wdrożenia Zwróć uwagę, stan poprzedniego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f2893-109">For the resource group involved in the deployment, notice the status of the last deployment.</span></span> <span data-ttu-id="f2893-110">Możesz wybrać ten stan, aby uzyskać więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="f2893-110">You can select this status to get more details.</span></span>
   
    ![Stan wdrożenia](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="f2893-112">Zobaczysz niedawną historię wdrażania.</span><span class="sxs-lookup"><span data-stu-id="f2893-112">You see the recent deployment history.</span></span> <span data-ttu-id="f2893-113">Wybierz wdrożenie, które zakończyły się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="f2893-113">Select the deployment that failed.</span></span>
   
    ![Stan wdrożenia](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="f2893-115">Wybierz łącze, aby wyświetlić opis przyczyny niepowodzenia wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f2893-115">Select the link to see a description of why the deployment failed.</span></span> <span data-ttu-id="f2893-116">Na poniższej ilustracji rekord DNS nie jest unikatowa.</span><span class="sxs-lookup"><span data-stu-id="f2893-116">In the image below, the DNS record is not unique.</span></span>  
   
    ![Wyświetl wdrożenia nie powiodło się](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="f2893-118">Ten komunikat o błędzie powinny wystarczyć można zacząć Rozwiązywanie problemów.</span><span class="sxs-lookup"><span data-stu-id="f2893-118">This error message should be enough for you to begin troubleshooting.</span></span> <span data-ttu-id="f2893-119">Jeśli potrzebujesz więcej szczegółowych informacji o zadania, które zostały ukończone, można wyświetlić operacje, jak pokazano w poniższych krokach.</span><span class="sxs-lookup"><span data-stu-id="f2893-119">However, if you need more details about which tasks were completed, you can view the operations as shown in the following steps.</span></span>
4. <span data-ttu-id="f2893-120">Można wyświetlić wszystkie operacje wdrażania w **wdrożenia** bloku.</span><span class="sxs-lookup"><span data-stu-id="f2893-120">You can view all the deployment operations in the **Deployment** blade.</span></span> <span data-ttu-id="f2893-121">Wybierz żadnej operacji, aby zobaczyć więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="f2893-121">Select any operation to see more details.</span></span>
   
    ![Wyświetlanie operacji](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="f2893-123">W takim przypadku zobaczysz, że zostały pomyślnie utworzone konto magazynu, sieci wirtualnej i zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="f2893-123">In this case, you see that the storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="f2893-124">Publiczny adres IP nie powiodło się, a nie podjęto inne zasoby.</span><span class="sxs-lookup"><span data-stu-id="f2893-124">The public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="f2893-125">Można wyświetlać zdarzenia dla wdrożenia, wybierając **zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="f2893-125">You can view events for the deployment by selecting **Events**.</span></span>
   
    ![Wyświetl zdarzenia](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="f2893-127">Zobacz wszystkie zdarzenia dla wdrożenia i zaznacz jeden więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="f2893-127">You see all the events for the deployment and select any one for more details.</span></span> <span data-ttu-id="f2893-128">Zwróć uwagę, zbyt identyfikatorów korelacji.</span><span class="sxs-lookup"><span data-stu-id="f2893-128">Notice too the correlation IDs.</span></span> <span data-ttu-id="f2893-129">Ta wartość może być przydatne podczas pracy z pomocą techniczną w celu wdrożenia rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f2893-129">This value can be helpful when working with technical support to troubleshoot a deployment.</span></span>
   
    ![Zobacz zdarzenia](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="f2893-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2893-131">PowerShell</span></span>
1. <span data-ttu-id="f2893-132">Aby uzyskać ogólny stan wdrożenia, należy użyć **Get-AzureRmResourceGroupDeployment** polecenia.</span><span class="sxs-lookup"><span data-stu-id="f2893-132">To get the overall status of a deployment, use the **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="f2893-133">Alternatywnie można filtrować wyniki dla tych wdrożeń, które nie powiodły.</span><span class="sxs-lookup"><span data-stu-id="f2893-133">Or, you can filter the results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="f2893-134">Dla każdego wdrożenia zawiera wiele operacji.</span><span class="sxs-lookup"><span data-stu-id="f2893-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="f2893-135">Każda operacja reprezentuje krokiem w procesie wdrażania.</span><span class="sxs-lookup"><span data-stu-id="f2893-135">Each operation represents a step in the deployment process.</span></span> <span data-ttu-id="f2893-136">Aby dowiedzieć się, co poszło źle z wdrożeniem, zazwyczaj należy wyświetlić szczegółowe informacje o operacji wdrażania.</span><span class="sxs-lookup"><span data-stu-id="f2893-136">To discover what went wrong with a deployment, you usually need to see details about the deployment operations.</span></span> <span data-ttu-id="f2893-137">Można wyświetlić stan operacji z **Get-AzureRmResourceGroupDeploymentOperation**.</span><span class="sxs-lookup"><span data-stu-id="f2893-137">You can see the status of the operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="f2893-138">Polecenie to zwraca wiele operacji z każdym z nich w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="f2893-138">Which returns multiple operations with each one in the following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="f2893-139">Aby uzyskać więcej informacji na temat operacji nie powiodło się, można pobrać właściwości dla operacji o **** stanu.</span><span class="sxs-lookup"><span data-stu-id="f2893-139">To get more details about failed operations, retrieve the properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="f2893-140">Polecenie to zwraca wszystkie nieudane operacje z każdym z nich w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="f2893-140">Which returns all the failed operations with each one in the following format:</span></span>

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

    <span data-ttu-id="f2893-141">Zanotuj serviceRequestId i trackingId dla tej operacji.</span><span class="sxs-lookup"><span data-stu-id="f2893-141">Note the serviceRequestId and the trackingId for the operation.</span></span> <span data-ttu-id="f2893-142">ServiceRequestId mogą być pomocne podczas pracy z pomocą techniczną w celu wdrożenia rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f2893-142">The serviceRequestId can be helpful when working with technical support to troubleshoot a deployment.</span></span> <span data-ttu-id="f2893-143">Aby skoncentrować się na określonej operacji użyje trackingId w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="f2893-143">You will use the trackingId in the next step to focus on a particular operation.</span></span>
4. <span data-ttu-id="f2893-144">Aby uzyskać komunikatu o stanie o określonej operacji nie powiodło się, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f2893-144">To get the status message of a particular failed operation, use the following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="f2893-145">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="f2893-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="f2893-146">Każda operacja wdrażania na platformie Azure jest przechowywana zawartość żądania i odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="f2893-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="f2893-147">Zawartość żądania jest co wysłanych do usługi Azure podczas wdrażania (na przykład utworzyć Maszynę wirtualną, dysk systemu operacyjnego i innych zasobów).</span><span class="sxs-lookup"><span data-stu-id="f2893-147">The request content is what you sent to Azure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="f2893-148">Treść odpowiedzi jest Azure wysyłane z żądania wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f2893-148">The response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="f2893-149">Podczas wdrażania można używać **DeploymentDebugLogLevel** paramenter, aby określić, czy żądania i/lub odpowiedzi są przechowywane w dzienniku.</span><span class="sxs-lookup"><span data-stu-id="f2893-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter to specify that the request and/or response are retained in the log.</span></span> 

  <span data-ttu-id="f2893-150">Uzyskiwanie informacji z dziennika i zapisać go lokalnie, używając następujących poleceń programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f2893-150">You get that information from the log, and save it locally by using the following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="f2893-151">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f2893-151">Azure CLI</span></span>

1. <span data-ttu-id="f2893-152">Ogólny stan wdrożenia z **Pokaż wdrożenia grupy azure** polecenia.</span><span class="sxs-lookup"><span data-stu-id="f2893-152">Get the overall status of a deployment with the **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="f2893-153">Jedna z wartości zwracane jest **correlationId**.</span><span class="sxs-lookup"><span data-stu-id="f2893-153">One of the returned values is the **correlationId**.</span></span> <span data-ttu-id="f2893-154">Ta wartość służy do śledzenia zdarzenia powiązane i mogą być przydatne podczas pracy z pomocą techniczną w celu wdrożenia rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f2893-154">This value is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="f2893-155">Aby wyświetlić operacje we wdrożeniu, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="f2893-155">To see the operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="f2893-156">REST</span><span class="sxs-lookup"><span data-stu-id="f2893-156">REST</span></span>

1. <span data-ttu-id="f2893-157">Uzyskiwanie informacji o wdrażaniu z [uzyskać informacje na temat wdrażania szablonu](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operacji.</span><span class="sxs-lookup"><span data-stu-id="f2893-157">Get information about a deployment with the [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="f2893-158">W odpowiedzi, należy pamiętać, w szczególności **provisioningState**, **correlationId**, i **błąd** elementów.</span><span class="sxs-lookup"><span data-stu-id="f2893-158">In the response, note in particular the **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="f2893-159">**CorrelationId** służy do śledzenia zdarzenia powiązane i mogą być przydatne podczas pracy z pomocą techniczną w celu wdrożenia rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f2893-159">The **correlationId** is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

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

2. <span data-ttu-id="f2893-160">Pobierz informacje o operacji wdrażania z [listy wszystkich operacji wdrożenia szablonu](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operacji.</span><span class="sxs-lookup"><span data-stu-id="f2893-160">Get information about deployment operations with the [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="f2893-161">Odpowiedź zawiera informacje żądania i/lub odpowiedzi, w zależności od określonych w **debugSetting** właściwości podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="f2893-161">The response includes request and/or response information based on what you specified in the **debugSetting** property during deployment.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="f2893-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f2893-162">Next steps</span></span>
* <span data-ttu-id="f2893-163">Aby uzyskać pomoc przy rozwiązywaniu problemów z błędami konkretnego wdrożenia, zobacz [Rozwiąż typowe błędy podczas wdrażania zasobów na platformie Azure za pomocą Menedżera zasobów Azure](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="f2893-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="f2893-164">Aby dowiedzieć się więcej o używaniu Dzienniki aktywności do monitorowania innych typów działań, zobacz [wyświetlać dzienniki aktywności do zarządzania zasobami Azure](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="f2893-164">To learn about using the activity logs to monitor other types of actions, see [View activity logs to manage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="f2893-165">Aby sprawdzić poprawność wdrożenia przed jego wykonaniem, zobacz [wdrażanie grupy zasobów za pomocą szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="f2893-165">To validate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

