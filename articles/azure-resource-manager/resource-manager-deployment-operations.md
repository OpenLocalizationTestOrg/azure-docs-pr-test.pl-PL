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
# <a name="view-deployment-operations-with-azure-resource-manager"></a>Operacje wdrażania widoku z usługi Azure Resource Manager


Można wyświetlić operacje hello wdrożenia za pośrednictwem hello portalu Azure. Może być najbardziej interesujące wyświetlanie hello operacji, gdy otrzymano wystąpił błąd podczas wdrażania, ten artykuł skupia się na wyświetlanie operacje, które nie powiodły. Hello portal udostępnia interfejs, który umożliwia tooeasily Znajdź hello błędów, aby ustalić możliwe rozwiązania.

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a>Portal
operacje wdrażania hello toosee, użyj hello następujące kroki:

1. Dla grupy zasobów hello objętego wdrożenia hello Zwróć uwagę, stan hello hello ostatniego wdrożenia. Ten stan tooget można wybrać więcej szczegółów.
   
    ![Stan wdrożenia](./media/resource-manager-deployment-operations/deployment-status.png)
2. Możesz sprawdzić hello niedawną historię wdrażania. Wybierz wdrożenie hello, które zakończyły się niepowodzeniem.
   
    ![Stan wdrożenia](./media/resource-manager-deployment-operations/select-deployment.png)
3. Wybierz toosee łącze hello opis dlaczego hello wdrażanie nie powiodło się. W poniższym obrazie hello hello rekord DNS nie jest unikatowa.  
   
    ![Wyświetl wdrożenia nie powiodło się](./media/resource-manager-deployment-operations/view-error.png)
   
    Ten komunikat o błędzie powinny wystarczyć dla Ciebie toobegin rozwiązywania problemów. Jednak jeśli potrzebujesz więcej szczegółów, o których zadania zostały ukończone, można wyświetlić operacje hello pokazane na powitania następujące kroki.
4. Można wyświetlić wszystkie operacje wdrażania hello w hello **wdrożenia** bloku. Wybierz wszystkie toosee operacji więcej szczegółów.
   
    ![Wyświetlanie operacji](./media/resource-manager-deployment-operations/view-operations.png)
   
    W takim przypadku zobaczysz, że hello konta magazynu, sieci wirtualnej i zestawu dostępności zostały pomyślnie utworzone. Hello publiczny adres IP nie powiodło się, a nie podjęto inne zasoby.
5. Można wyświetlać zdarzenia hello wdrożenia, wybierając **zdarzenia**.
   
    ![Wyświetl zdarzenia](./media/resource-manager-deployment-operations/view-events.png)
6. Zobacz wszystkie zdarzenia hello hello wdrożenia i zaznacz jeden więcej szczegółów. Zwróć uwagę, zbyt hello identyfikatorów korelacji. Ta wartość może być przydatne podczas pracy z działem pomocy technicznej tootroubleshoot wdrożenia.
   
    ![Zobacz zdarzenia](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a>PowerShell
1. ogólny stan wdrożenia, użyj hello hello tooget **Get-AzureRmResourceGroupDeployment** polecenia. 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   Alternatywnie można filtrować wyniki hello tylko wdrożenia, które nie powiodły.

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. Dla każdego wdrożenia zawiera wiele operacji. Każda operacja reprezentuje krokiem w procesie wdrażania hello. toodiscover co poszło problem z wdrożeniem, należy zwykle toosee szczegóły hello operacje wdrażania. Można wyświetlić stan hello operacji hello z **Get-AzureRmResourceGroupDeploymentOperation**.

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    Polecenie to zwraca wiele operacji z każdym z nich hello następującego formatu:

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. tooget więcej szczegółów na temat nieudane operacje pobierania właściwości powitania dla operacji o **** stanu.

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    Które zwraca wszystkie hello nieudane operacje z każdą z nich w hello następującego formatu:

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

    Zanotuj hello serviceRequestId i trackingId hello hello operacji. Witaj serviceRequestId mogą być pomocne podczas pracy z działem pomocy technicznej tootroubleshoot wdrożenia. Użyjesz hello trackingId w hello następny krok toofocus na określonej operacji.
4. tooget hello komunikatu o stanie określonej operacji nie powiodło się, hello Użyj następującego polecenia:

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    Polecenie to zwraca:

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. Każda operacja wdrażania na platformie Azure jest przechowywana zawartość żądania i odpowiedzi. zawartość żądania Hello jest co wysłano tooAzure podczas wdrażania (na przykład utworzyć Maszynę wirtualną, dysk systemu operacyjnego i innych zasobów). zawartość odpowiedzi Hello jest Azure wysyłane z żądania wdrożenia. Podczas wdrażania można używać **DeploymentDebugLogLevel** toospecify paramenter, który hello żądań i/lub odpowiedzi są przechowywane w dzienniku hello. 

  Uzyskiwanie informacji z dziennika hello i zapisać go lokalnie, używając następujących poleceń programu PowerShell hello:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

1. Pobierz hello ogólny stan wdrożenia z hello **Pokaż wdrożenia grupy azure** polecenia.

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  Jednym z hello zwracane wartości jest hello **correlationId**. Ta wartość jest używana zdarzenia związane z tootrack i może być przydatne w przypadku pracy z tootroubleshoot pomocy technicznej wdrożenia.

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. Użyj operacji hello toosee w przypadku wdrożenia:

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a>REST

1. Uzyskiwanie informacji o wdrażaniu z hello [uzyskać informacje na temat wdrażania szablonu](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operacji.

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    W odpowiedzi hello, należy pamiętać, w szczególności hello **provisioningState**, **correlationId**, i **błąd** elementów. Witaj **correlationId** służy zdarzenia związane z tootrack i może być przydatne w przypadku pracy z tootroubleshoot pomocy technicznej wdrożenia.

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

2. Pobierz informacje o operacji wdrażania z hello [listy wszystkich operacji wdrożenia szablonu](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operacji. 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    odpowiedź Hello zawiera informacje żądania i/lub odpowiedzi, w zależności od określonych w hello **debugSetting** właściwości podczas wdrażania.

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


## <a name="next-steps"></a>Następne kroki
* Aby uzyskać pomoc przy rozwiązywaniu problemów z błędami konkretnego wdrożenia, zobacz [Rozwiąż typowe błędy podczas wdrażania tooAzure zasobów z usługi Azure Resource Manager](resource-manager-common-deployment-errors.md).
* toolearn o używaniu hello działania w dziennikach toomonitor inne typy akcji, zobacz [toomanage Azure Dzienniki aktywności widok zasobów](resource-group-audit.md).
* Zobacz wdrożenia przed jego wykonaniem toovalidate [wdrażanie grupy zasobów za pomocą szablonu usługi Azure Resource Manager](resource-group-template-deploy.md).

