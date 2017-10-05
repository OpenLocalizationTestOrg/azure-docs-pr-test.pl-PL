---
title: "Zrozumienie błędy wdrożenia usługi Azure | Dokumentacja firmy Microsoft"
description: "Opisuje sposób dowiedzieć się więcej o błędach wdrożenia usługi Azure."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Błąd wdrażania, wdrożenia usługi azure wdrażanie na platformie azure"
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: b67bb30fa259fa08e37e11afec724c8b8c3eb633
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="understand-azure-deployment-errors"></a><span data-ttu-id="683d9-104">Zrozumienie błędy wdrożenia usługi Azure</span><span class="sxs-lookup"><span data-stu-id="683d9-104">Understand Azure deployment errors</span></span>
<span data-ttu-id="683d9-105">W tym temacie opisano błędy wdrożenia i jak mogą odnajdować więcej informacji o błędzie.</span><span class="sxs-lookup"><span data-stu-id="683d9-105">This topic describes deployment errors and how you can discover more information about an error.</span></span> <span data-ttu-id="683d9-106">Dla rozwiązania typowych błędów wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="683d9-106">For resolutions to common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="two-types-of-errors"></a><span data-ttu-id="683d9-107">Dwa typy błędów</span><span class="sxs-lookup"><span data-stu-id="683d9-107">Two types of errors</span></span>
<span data-ttu-id="683d9-108">Istnieją dwa typy błędów, które mogą odbierać:</span><span class="sxs-lookup"><span data-stu-id="683d9-108">There are two types of errors you can receive:</span></span>

* <span data-ttu-id="683d9-109">Błędy sprawdzania poprawności</span><span class="sxs-lookup"><span data-stu-id="683d9-109">validation errors</span></span>
* <span data-ttu-id="683d9-110">Błędy wdrożenia</span><span class="sxs-lookup"><span data-stu-id="683d9-110">deployment errors</span></span>

<span data-ttu-id="683d9-111">Poniższa ilustracja przedstawia przykładowy dziennik aktywności subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="683d9-111">The following image shows the activity log for a subscription.</span></span> <span data-ttu-id="683d9-112">Reprezentuje dwa wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="683d9-112">It represents two deployments.</span></span> <span data-ttu-id="683d9-113">Jedno wdrożenie szablonu nie powiodło się sprawdzanie poprawności (**weryfikacji**) i nie kontynuować.</span><span class="sxs-lookup"><span data-stu-id="683d9-113">In one deployment, the template failed validation (**Validate**) and did not proceed.</span></span> <span data-ttu-id="683d9-114">W ramach wdrożenia, szablon przeszły sprawdzanie poprawności, ale nie powiodło się podczas tworzenia zasobów (**zapisu wdrożeń**).</span><span class="sxs-lookup"><span data-stu-id="683d9-114">In the other deployment, the template passed validation but failed when creating the resources (**Write Deployments**).</span></span> 

![Pokaż kod błędu:](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

<span data-ttu-id="683d9-116">Błędy sprawdzania poprawności wynikają z scenariusze, które można określić przed przystąpieniem do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="683d9-116">Validation errors arise from scenarios that can be determined before deployment.</span></span> <span data-ttu-id="683d9-117">Obejmują one błędy składniowe w szablonie lub w trakcie wdrażania zasobów, które może spowodować przekroczenie przydziałami subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="683d9-117">They include syntax errors in your template, or trying to deploy resources that would exceed your subscription quotas.</span></span> <span data-ttu-id="683d9-118">Błędy wdrożenia wynikają z warunków, które występują w trakcie procesu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="683d9-118">Deployment errors arise from conditions that occur during the deployment process.</span></span> <span data-ttu-id="683d9-119">Obejmują one próby uzyskania dostępu do zasobu, który jest wdrażany jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="683d9-119">They include trying to access a resource that is being deployed in parallel.</span></span>

<span data-ttu-id="683d9-120">Oba typy błędów zwraca kod błędu, który umożliwia rozwiązywanie problemów z wdrażaniem.</span><span class="sxs-lookup"><span data-stu-id="683d9-120">Both types of errors return an error code that you use to troubleshoot the deployment.</span></span> <span data-ttu-id="683d9-121">Oba typy błędy są wyświetlane w [dziennik aktywności](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="683d9-121">Both types of errors appear in the [activity log](resource-group-audit.md).</span></span> <span data-ttu-id="683d9-122">Błędy sprawdzania poprawności nie pojawiają się jednak w historii wdrożenia, ponieważ wdrożenie nigdy nie jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="683d9-122">However, validation errors do not appear in your deployment history because the deployment never started.</span></span>

## <a name="determine-error-code"></a><span data-ttu-id="683d9-123">Określić kod błędu:</span><span class="sxs-lookup"><span data-stu-id="683d9-123">Determine error code</span></span>

<span data-ttu-id="683d9-124">Informacje na temat błędu analizując komunikat o błędzie i kod błędu.</span><span class="sxs-lookup"><span data-stu-id="683d9-124">You can learn about an error by looking at the error message and the error code.</span></span> <span data-ttu-id="683d9-125">[Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md) artykule wymieniono rozwiązania przez kod błędu.</span><span class="sxs-lookup"><span data-stu-id="683d9-125">The [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md) article lists resolutions by error code.</span></span> <span data-ttu-id="683d9-126">W tym temacie przedstawiono sposób użycia portalu Azure, aby dowiedzieć się, kod błędu.</span><span class="sxs-lookup"><span data-stu-id="683d9-126">This topic shows how to use the Azure portal to discover the error code.</span></span>

### <a name="validation-errors"></a><span data-ttu-id="683d9-127">Błędy sprawdzania poprawności</span><span class="sxs-lookup"><span data-stu-id="683d9-127">Validation errors</span></span>

<span data-ttu-id="683d9-128">W przypadku wdrażania za pośrednictwem portalu, zobaczysz błąd sprawdzania poprawności po przesłaniu wartości.</span><span class="sxs-lookup"><span data-stu-id="683d9-128">When deploying through the portal, you see a validation error after submitting your values.</span></span>

![Pokaż błąd sprawdzania poprawności portalu](./media/resource-manager-troubleshoot-tips/validation-error.png)

<span data-ttu-id="683d9-130">Zaznacz wiadomość, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="683d9-130">Select the message for more details.</span></span> <span data-ttu-id="683d9-131">Na poniższej ilustracji, zobacz **InvalidTemplateDeployment** błąd i komunikat informujący zasad zablokowane wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="683d9-131">In the following image, you see an **InvalidTemplateDeployment** error and a message that indicates a policy blocked deployment.</span></span>

![Pokaż szczegóły sprawdzania poprawności](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a><span data-ttu-id="683d9-133">Błędy wdrożenia</span><span class="sxs-lookup"><span data-stu-id="683d9-133">Deployment errors</span></span>

<span data-ttu-id="683d9-134">Podczas operacji pozytywnej weryfikacji, ale nie powiodło się podczas wdrażania, zostanie wyświetlony błąd w powiadomieniach.</span><span class="sxs-lookup"><span data-stu-id="683d9-134">When the operation passes validation, but fails during deployment, you see the error in the notifications.</span></span> <span data-ttu-id="683d9-135">Wybierz powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="683d9-135">Select the notification.</span></span>

![Błąd powiadomienia](./media/resource-manager-troubleshoot-tips/notification.png)

<span data-ttu-id="683d9-137">Możesz wyświetlić więcej szczegółów dotyczących wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="683d9-137">You see more details about the deployment.</span></span> <span data-ttu-id="683d9-138">Wybierz opcję, aby uzyskać więcej informacji o tym błędzie.</span><span class="sxs-lookup"><span data-stu-id="683d9-138">Select the option to find more information about the error.</span></span>

![Wdrażanie nie powiodło się](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

<span data-ttu-id="683d9-140">Zostanie wyświetlony komunikat o błędzie i kody błędów.</span><span class="sxs-lookup"><span data-stu-id="683d9-140">You see the error message and error codes.</span></span> <span data-ttu-id="683d9-141">Należy zauważyć, że istnieją dwa kody błędów.</span><span class="sxs-lookup"><span data-stu-id="683d9-141">Notice there are two error codes.</span></span> <span data-ttu-id="683d9-142">Pierwszy kod błędu (**niepowodzenia wdrożenia**) jest błąd ogólny, który nie zapewnia szczegółowe informacje, musisz poprawić błąd.</span><span class="sxs-lookup"><span data-stu-id="683d9-142">The first error code (**DeploymentFailed**) is a general error that does not provide the details you need to solve the error.</span></span> <span data-ttu-id="683d9-143">Drugi kod błędu (**StorageAccountNotFound**) zawiera szczegółowe informacje, należy.</span><span class="sxs-lookup"><span data-stu-id="683d9-143">The second error code (**StorageAccountNotFound**) provides the details you need.</span></span> 

![Szczegóły błędu](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a><span data-ttu-id="683d9-145">Włączenie rejestrowania debugowania</span><span class="sxs-lookup"><span data-stu-id="683d9-145">Enable debug logging</span></span>
<span data-ttu-id="683d9-146">Czasami możesz uzyskać więcej informacji dotyczących żądania i odpowiedzi, aby dowiedzieć się, co poszło źle.</span><span class="sxs-lookup"><span data-stu-id="683d9-146">Sometimes you need more information about the request and response to discover what went wrong.</span></span> <span data-ttu-id="683d9-147">Przy użyciu programu PowerShell lub interfejsu wiersza polecenia Azure, mogą żądać, aby uzyskać dodatkowe informacje jest rejestrowane podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="683d9-147">By using PowerShell or Azure CLI, you can request that additional information is logged during a deployment.</span></span>

- <span data-ttu-id="683d9-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="683d9-148">PowerShell</span></span>

   <span data-ttu-id="683d9-149">W programie PowerShell, należy ustawić **DeploymentDebugLogLevel** parametr do wszystkich, obiektu ResponseContent lub RequestContent.</span><span class="sxs-lookup"><span data-stu-id="683d9-149">In PowerShell, set the **DeploymentDebugLogLevel** parameter to All, ResponseContent, or RequestContent.</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   <span data-ttu-id="683d9-150">Sprawdź żądanie zawartości za pomocą następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="683d9-150">Examine the request content with the following cmdlet:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   <span data-ttu-id="683d9-151">Lub zawartości z odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="683d9-151">Or, the response content with:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   <span data-ttu-id="683d9-152">Te informacje mogą pomóc w określeniu, czy wartość w szablonie jest są ustawione niepoprawnie.</span><span class="sxs-lookup"><span data-stu-id="683d9-152">This information can help you determine whether a value in the template is being incorrectly set.</span></span>

- <span data-ttu-id="683d9-153">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="683d9-153">Azure CLI</span></span>

   <span data-ttu-id="683d9-154">Sprawdź operacje wdrażania przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="683d9-154">Examine the deployment operations with the following command:</span></span>

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- <span data-ttu-id="683d9-155">Szablon zagnieżdżony</span><span class="sxs-lookup"><span data-stu-id="683d9-155">Nested template</span></span>

   <span data-ttu-id="683d9-156">Rejestrowanie informacji debugowania dla szablonu zagnieżdżonego, należy użyć **debugSetting** elementu.</span><span class="sxs-lookup"><span data-stu-id="683d9-156">To log debug information for a nested template, use the **debugSetting** element.</span></span>

  ```json
  {
      "apiVersion": "2016-09-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri": "{template-uri}",
              "contentVersion": "1.0.0.0"
          },
          "debugSetting": {
             "detailLevel": "requestContent, responseContent"
          }
      }
  }
  ```


## <a name="create-a-troubleshooting-template"></a><span data-ttu-id="683d9-157">Tworzenie szablonu rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="683d9-157">Create a troubleshooting template</span></span>
<span data-ttu-id="683d9-158">W pewnych sytuacjach Najprostszym sposobem Rozwiązywanie problemów z szablonu jest przetestowanie jej części.</span><span class="sxs-lookup"><span data-stu-id="683d9-158">In some cases, the easiest way to troubleshoot your template is to test parts of it.</span></span> <span data-ttu-id="683d9-159">Uproszczona można utworzyć szablonu, który pozwala skupić się na części podejrzenie, że przyczyną jest błąd.</span><span class="sxs-lookup"><span data-stu-id="683d9-159">You can create a simplified template that enables you to focus on the part that you believe is causing the error.</span></span> <span data-ttu-id="683d9-160">Na przykład załóżmy, że otrzymujesz błąd podczas odwoływania się do zasobu.</span><span class="sxs-lookup"><span data-stu-id="683d9-160">For example, suppose you are receiving an error when referencing a resource.</span></span> <span data-ttu-id="683d9-161">Zamiast dotyczącą całą szablonu, utworzyć szablon, który zwraca składnik, który może być przyczyną tego problemu.</span><span class="sxs-lookup"><span data-stu-id="683d9-161">Rather than dealing with an entire template, create a template that returns the part that may be causing your problem.</span></span> <span data-ttu-id="683d9-162">Możesz określić, czy jest przekazywany w parametrach prawo poprawnie, przy użyciu funkcji szablonu i pobieranie zasobu oczekiwać może pomóc.</span><span class="sxs-lookup"><span data-stu-id="683d9-162">It can help you determine whether you are passing in the right parameters, using template functions correctly, and getting the resource you expect.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": {
        "type": "string"
    },
    "storageResourceGroup": {
        "type": "string"
    }
  },
  "variables": {},
  "resources": [],
  "outputs": {
    "exampleOutput": {
        "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageName')), '2016-05-01')]",
        "type" : "object"
    }
  }
}
```

<span data-ttu-id="683d9-163">Lub Załóżmy, że pojawiły się błędy wdrożenia, które Twoim zdaniem są związane z niepoprawnie ustawione zależności.</span><span class="sxs-lookup"><span data-stu-id="683d9-163">Or, suppose you are encountering deployment errors that you believe are related to incorrectly set dependencies.</span></span> <span data-ttu-id="683d9-164">Przetestuj szablonu przez podzielenie go na uproszczonej szablonów.</span><span class="sxs-lookup"><span data-stu-id="683d9-164">Test your template by breaking it into simplified templates.</span></span> <span data-ttu-id="683d9-165">Najpierw Utwórz szablon, który wdraża jednego zasobu (np. programu SQL Server).</span><span class="sxs-lookup"><span data-stu-id="683d9-165">First, create a template that deploys only a single resource (like a SQL Server).</span></span> <span data-ttu-id="683d9-166">Podczas pracy upewnić się, że ten zasób zdefiniowany prawidłowo, Dodaj zasób zależy od niego (na przykład baza danych SQL).</span><span class="sxs-lookup"><span data-stu-id="683d9-166">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span></span> <span data-ttu-id="683d9-167">Jeśli te dwa zasoby zdefiniowany prawidłowo, należy dodać inne zasoby zależne (na przykład zasady inspekcji).</span><span class="sxs-lookup"><span data-stu-id="683d9-167">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span></span> <span data-ttu-id="683d9-168">Between każdego wdrożenia testu Usuń grupę zasobów, aby mieć pewność, że odpowiednio testowania zależności.</span><span class="sxs-lookup"><span data-stu-id="683d9-168">In between each test deployment, delete the resource group to make sure you adequately testing the dependencies.</span></span> 

## <a name="check-deployment-sequence"></a><span data-ttu-id="683d9-169">Sprawdź wdrożenie sekwencji</span><span class="sxs-lookup"><span data-stu-id="683d9-169">Check deployment sequence</span></span>

<span data-ttu-id="683d9-170">Wiele błędów wdrażania się tak zdarzyć, gdy zasoby są wdrożone w nieoczekiwany sekwencji.</span><span class="sxs-lookup"><span data-stu-id="683d9-170">Many deployment errors happen when resources are deployed in an unexpected sequence.</span></span> <span data-ttu-id="683d9-171">Te błędy wystąpić, gdy zależności nie są poprawnie ustawione.</span><span class="sxs-lookup"><span data-stu-id="683d9-171">These errors arise when dependencies are not correctly set.</span></span> <span data-ttu-id="683d9-172">Brak wymaganych zależności, jeden zasób próbuje użyć wartości innego zasobu, ale innych jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="683d9-172">When you are missing a needed dependency, one resource attempts to use a value for another resource but the other does not yet exist.</span></span> <span data-ttu-id="683d9-173">Otrzymasz komunikat o błędzie informujący, że zasób nie został znaleziony.</span><span class="sxs-lookup"><span data-stu-id="683d9-173">You get an error stating that a resource is not found.</span></span> <span data-ttu-id="683d9-174">Mogą występować sporadycznie tego typu błędu dla każdego zasobu czas wdrażania może się różnić.</span><span class="sxs-lookup"><span data-stu-id="683d9-174">You may encounter this type of error intermittently because the deployment time for each resource can vary.</span></span> <span data-ttu-id="683d9-175">Na przykład pierwsza próba wdrażanie zasobów powiedzie się, ponieważ wymagany zasób jest przeprowadzany losowo w czasie.</span><span class="sxs-lookup"><span data-stu-id="683d9-175">For example, your first attempt to deploy your resources succeeds because a required resource randomly completes in time.</span></span> <span data-ttu-id="683d9-176">Jednak z druga próba nie powiedzie się, ponieważ wymagany zasób nie została ukończona w czasie.</span><span class="sxs-lookup"><span data-stu-id="683d9-176">However, your second attempt fails because the required resource did not complete in time.</span></span> 

<span data-ttu-id="683d9-177">Jednak aby uniknąć ustawienie zależności, które nie są wymagane.</span><span class="sxs-lookup"><span data-stu-id="683d9-177">But, you want to avoid setting dependencies that are not needed.</span></span> <span data-ttu-id="683d9-178">Gdy niepotrzebne zależności, można przedłużyć czas wdrażania, zapobiegając zasoby, które nie są wzajemnie zależne od wdrażany równolegle.</span><span class="sxs-lookup"><span data-stu-id="683d9-178">When you have unnecessary dependencies, you prolong the duration of the deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="683d9-179">Ponadto można utworzyć zależności cykliczne, które blokuje wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="683d9-179">In addition, you may create circular dependencies that block the deployment.</span></span> <span data-ttu-id="683d9-180">[Odwołania](resource-group-template-functions-resource.md#reference) funkcja tworzy zależność niejawnych na zasobu dołączonego przez odwołanie, po wdrożeniu tego zasobu w tym samym szablonie.</span><span class="sxs-lookup"><span data-stu-id="683d9-180">The [reference](resource-group-template-functions-resource.md#reference) function creates an implicit dependency on the referenced resource, when that resource is deployed in the same template.</span></span> <span data-ttu-id="683d9-181">W związku z tym może mieć zależności więcej niż określa zależności **dependsOn** właściwości.</span><span class="sxs-lookup"><span data-stu-id="683d9-181">Therefore, you may have more dependencies than the dependencies specified in the **dependsOn** property.</span></span> <span data-ttu-id="683d9-182">[ResourceId](resource-group-template-functions-resource.md#resourceid) funkcji nie utworzyć niejawnego zależności lub Sprawdzanie, czy zasób istnieje.</span><span class="sxs-lookup"><span data-stu-id="683d9-182">The [resourceId](resource-group-template-functions-resource.md#resourceid) function does not create an implicit dependency or validate that the resource exists.</span></span>

<span data-ttu-id="683d9-183">W przypadku wystąpienia problemów zależności, musisz uzyskać wgląd w kolejności wdrażania zasobów.</span><span class="sxs-lookup"><span data-stu-id="683d9-183">When you encounter dependency problems, you need to gain insight into the order of resource deployment.</span></span> <span data-ttu-id="683d9-184">Aby wyświetlić kolejność operacji wdrażania:</span><span class="sxs-lookup"><span data-stu-id="683d9-184">To view the order of deployment operations:</span></span>

1. <span data-ttu-id="683d9-185">Wybierz historii wdrożenia dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="683d9-185">Select the deployment history for your resource group.</span></span>

   ![Wybierz Historia wdrażania](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. <span data-ttu-id="683d9-187">Wybierz wdrożenie z historii, a następnie wybierz **zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="683d9-187">Select a deployment from the history, and select **Events**.</span></span>

   ![Wybierz zdarzenia wdrożenia](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. <span data-ttu-id="683d9-189">Sprawdź, czy sekwencję zdarzeń dla każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="683d9-189">Examine the sequence of events for each resource.</span></span> <span data-ttu-id="683d9-190">Należy zwrócić uwagę na stan każdej operacji.</span><span class="sxs-lookup"><span data-stu-id="683d9-190">Pay attention to the status of each operation.</span></span> <span data-ttu-id="683d9-191">Na przykład na poniższej ilustracji przedstawiono trzy konta magazynu, które wdrożone równolegle.</span><span class="sxs-lookup"><span data-stu-id="683d9-191">For example, the following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="683d9-192">Zwróć uwagę, że trzy konta magazynu są uruchamiane w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="683d9-192">Notice that the three storage accounts are started at the same time.</span></span>

   ![Wdrożenie równoległe](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   <span data-ttu-id="683d9-194">Na następnej ilustracji przedstawiono trzy konta magazynu, które nie są wdrażane równolegle.</span><span class="sxs-lookup"><span data-stu-id="683d9-194">The next image shows three storage accounts that are not deployed in parallel.</span></span> <span data-ttu-id="683d9-195">Pierwsze konto magazynu zależy od drugiego konta magazynu, a trzeci konta magazynu zależy od drugiego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="683d9-195">The second storage account depends on the first storage account, and the third storage account depends on the second storage account.</span></span> <span data-ttu-id="683d9-196">W związku z tym pierwsze konto magazynu jest uruchomiona, zaakceptowane i ukończone przed uruchomieniem następnego.</span><span class="sxs-lookup"><span data-stu-id="683d9-196">Therefore, the first storage account is started, accepted, and completed before the next is started.</span></span>

   ![kolejne wdrożenia](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

<span data-ttu-id="683d9-198">Nawet w przypadku bardziej złożonych zadań można użyć tę samą metodę, aby dowiedzieć się, gdy wdrożenie zostanie rozpoczęte i zakończone dla każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="683d9-198">Even for more complicated scenarios, you can use the same technique to discover when deployment is started and completed for each resource.</span></span> <span data-ttu-id="683d9-199">Przejrzyj zdarzeń wdrażania czy sekwencja jest inny niż oczekiwany.</span><span class="sxs-lookup"><span data-stu-id="683d9-199">Look through your deployment events to see if the sequence is different than you would expect.</span></span> <span data-ttu-id="683d9-200">Jeśli tak, można obliczyć ponownie zależności dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="683d9-200">If so, reevaluate the dependencies for this resource.</span></span>

<span data-ttu-id="683d9-201">Menedżer zasobów identyfikuje zależności cykliczne podczas walidacji szablonu.</span><span class="sxs-lookup"><span data-stu-id="683d9-201">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="683d9-202">Zwraca się, że istnieje komunikat o błędzie stwierdzający, w szczególności zależność cykliczną.</span><span class="sxs-lookup"><span data-stu-id="683d9-202">It returns an error message that specifically states a circular dependency exists.</span></span> <span data-ttu-id="683d9-203">Aby rozwiązać zależność cykliczną:</span><span class="sxs-lookup"><span data-stu-id="683d9-203">To solve a circular dependency:</span></span>

1. <span data-ttu-id="683d9-204">W szablonie można znaleźć zasobu określonego w zależność cykliczną.</span><span class="sxs-lookup"><span data-stu-id="683d9-204">In your template, find the resource identified in the circular dependency.</span></span> 
2. <span data-ttu-id="683d9-205">Dla tego zasobu, sprawdź **dependsOn** właściwości i wszelkie zastosowania **odwołania** sprawdzić zasobów, do których zależy od funkcji.</span><span class="sxs-lookup"><span data-stu-id="683d9-205">For that resource, examine the **dependsOn** property and any uses of the **reference** function to see which resources it depends on.</span></span> 
3. <span data-ttu-id="683d9-206">Sprawdź, czy te zasoby, aby wyświetlić zasobów, do których one zależą.</span><span class="sxs-lookup"><span data-stu-id="683d9-206">Examine those resources to see which resources they depend on.</span></span> <span data-ttu-id="683d9-207">Wykonaj zależności, dopóki zauważysz z zasobem, który jest zależny od zasobu oryginalnego.</span><span class="sxs-lookup"><span data-stu-id="683d9-207">Follow the dependencies until you notice a resource that depends on the original resource.</span></span>
5. <span data-ttu-id="683d9-208">Zasoby związane z zależność cykliczną, należy dokładnie zbadać wszystkie użycia **dependsOn** właściwości, aby zidentyfikować wszelkie zależności, które nie są wymagane.</span><span class="sxs-lookup"><span data-stu-id="683d9-208">For the resources involved in the circular dependency, carefully examine all uses of the **dependsOn** property to identify any dependencies that are not needed.</span></span> <span data-ttu-id="683d9-209">Usuń te zależności.</span><span class="sxs-lookup"><span data-stu-id="683d9-209">Remove those dependencies.</span></span> <span data-ttu-id="683d9-210">Jeśli nie wiesz, czy zależność jest potrzebny, spróbuj go usunąć.</span><span class="sxs-lookup"><span data-stu-id="683d9-210">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="683d9-211">Należy ponownie wdrożyć szablon.</span><span class="sxs-lookup"><span data-stu-id="683d9-211">Redeploy the template.</span></span>

<span data-ttu-id="683d9-212">Usuwanie wartości z **dependsOn** właściwości, które mogą powodować błędy podczas wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="683d9-212">Removing values from the **dependsOn** property can cause errors when you deploy the template.</span></span> <span data-ttu-id="683d9-213">Jeśli wystąpi błąd, Dodaj zależności do szablonu.</span><span class="sxs-lookup"><span data-stu-id="683d9-213">If you encounter an error, add the dependency back into the template.</span></span> 

<span data-ttu-id="683d9-214">Jeśli takie podejście nie rozwiązuje zależność cykliczną, rozważ migrację część logiki wdrażania zasobów podrzędnych (na przykład rozszerzenia lub ustawienia konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="683d9-214">If that approach does not solve the circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="683d9-215">Skonfiguruj te zasoby podrzędne do wdrożenia po zasoby związane z zależność cykliczną.</span><span class="sxs-lookup"><span data-stu-id="683d9-215">Configure those child resources to deploy after the resources involved in the circular dependency.</span></span> <span data-ttu-id="683d9-216">Załóżmy na przykład wdrażasz dwóch maszyn wirtualnych, ale należy ustawić na każdej z nich, która odwołuje się do innych właściwości.</span><span class="sxs-lookup"><span data-stu-id="683d9-216">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="683d9-217">Można je wdrożyć w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="683d9-217">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="683d9-218">vm1</span><span class="sxs-lookup"><span data-stu-id="683d9-218">vm1</span></span>
2. <span data-ttu-id="683d9-219">maszyny vm2</span><span class="sxs-lookup"><span data-stu-id="683d9-219">vm2</span></span>
3. <span data-ttu-id="683d9-220">Rozszerzenie na vm1 zależy od vm1 i maszyny vm2.</span><span class="sxs-lookup"><span data-stu-id="683d9-220">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="683d9-221">Rozszerzenie ustawia wartości vm1, który otrzymuje od maszyny vm2.</span><span class="sxs-lookup"><span data-stu-id="683d9-221">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="683d9-222">Rozszerzenie maszyny vm2 zależy od vm1 i maszyny vm2.</span><span class="sxs-lookup"><span data-stu-id="683d9-222">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="683d9-223">Rozszerzenie ustawia wartości maszyny vm2, który otrzymuje od vm1.</span><span class="sxs-lookup"><span data-stu-id="683d9-223">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="683d9-224">Te same podejście działa w przypadku aplikacji usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="683d9-224">The same approach works for App Service apps.</span></span> <span data-ttu-id="683d9-225">Rozważ przeniesienie wartości konfiguracji do zasobu podrzędnego zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="683d9-225">Consider moving configuration values into a child resource of the app resource.</span></span> <span data-ttu-id="683d9-226">Można wdrożyć dwie aplikacje sieci web w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="683d9-226">You can deploy two web apps in the following order:</span></span>

1. <span data-ttu-id="683d9-227">webapp1</span><span class="sxs-lookup"><span data-stu-id="683d9-227">webapp1</span></span>
2. <span data-ttu-id="683d9-228">webapp2</span><span class="sxs-lookup"><span data-stu-id="683d9-228">webapp2</span></span>
3. <span data-ttu-id="683d9-229">Konfiguracja webapp1 zależy od webapp1 i webapp2.</span><span class="sxs-lookup"><span data-stu-id="683d9-229">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="683d9-230">Zawiera ustawienia aplikacji wartościami z webapp2.</span><span class="sxs-lookup"><span data-stu-id="683d9-230">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="683d9-231">Konfiguracja webapp2 zależy od webapp1 i webapp2.</span><span class="sxs-lookup"><span data-stu-id="683d9-231">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="683d9-232">Zawiera ustawienia aplikacji wartościami z webapp1.</span><span class="sxs-lookup"><span data-stu-id="683d9-232">It contains app settings with values from webapp1.</span></span>


## <a name="next-steps"></a><span data-ttu-id="683d9-233">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="683d9-233">Next steps</span></span>
* <span data-ttu-id="683d9-234">Dla rozwiązania typowych błędów wdrażania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="683d9-234">For resolutions to common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="683d9-235">Aby dowiedzieć się więcej o inspekcji akcji, zobacz [inspekcji operacji za pomocą Menedżera zasobów](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="683d9-235">To learn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="683d9-236">Aby dowiedzieć się więcej o akcjach, aby określić błędy podczas wdrażania, zobacz [wyświetlić operacje wdrażania](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="683d9-236">To learn about actions to determine the errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
