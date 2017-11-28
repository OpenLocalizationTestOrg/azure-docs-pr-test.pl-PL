---
title: "błędy wdrożenia usługi Azure aaaUnderstand | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toolearn o błędach wdrożenia usługi Azure."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Błąd wdrażania, wdrożenia usługi azure wdrażanie tooazure"
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: a335e121e9b908a763374907e34b1f6e823d6e96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-deployment-errors"></a><span data-ttu-id="c6638-104">Zrozumienie błędy wdrożenia usługi Azure</span><span class="sxs-lookup"><span data-stu-id="c6638-104">Understand Azure deployment errors</span></span>
<span data-ttu-id="c6638-105">W tym temacie opisano błędy wdrożenia i jak mogą odnajdować więcej informacji o błędzie.</span><span class="sxs-lookup"><span data-stu-id="c6638-105">This topic describes deployment errors and how you can discover more information about an error.</span></span> <span data-ttu-id="c6638-106">Błędy wdrożenia toocommon rozwiązania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="c6638-106">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="two-types-of-errors"></a><span data-ttu-id="c6638-107">Dwa typy błędów</span><span class="sxs-lookup"><span data-stu-id="c6638-107">Two types of errors</span></span>
<span data-ttu-id="c6638-108">Istnieją dwa typy błędów, które mogą odbierać:</span><span class="sxs-lookup"><span data-stu-id="c6638-108">There are two types of errors you can receive:</span></span>

* <span data-ttu-id="c6638-109">Błędy sprawdzania poprawności</span><span class="sxs-lookup"><span data-stu-id="c6638-109">validation errors</span></span>
* <span data-ttu-id="c6638-110">Błędy wdrożenia</span><span class="sxs-lookup"><span data-stu-id="c6638-110">deployment errors</span></span>

<span data-ttu-id="c6638-111">powitania po obraz zawiera dziennik aktywności hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c6638-111">hello following image shows hello activity log for a subscription.</span></span> <span data-ttu-id="c6638-112">Reprezentuje dwa wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c6638-112">It represents two deployments.</span></span> <span data-ttu-id="c6638-113">W przypadku wdrożenia jednego szablonu hello nie przeszedł sprawdzania poprawności (**weryfikacji**) i nie kontynuować.</span><span class="sxs-lookup"><span data-stu-id="c6638-113">In one deployment, hello template failed validation (**Validate**) and did not proceed.</span></span> <span data-ttu-id="c6638-114">W hello inne wdrożenia, szablon hello przeszły sprawdzanie poprawności, ale nie powiodło się podczas tworzenia zasobów hello (**zapisu wdrożeń**).</span><span class="sxs-lookup"><span data-stu-id="c6638-114">In hello other deployment, hello template passed validation but failed when creating hello resources (**Write Deployments**).</span></span> 

![Pokaż kod błędu:](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

<span data-ttu-id="c6638-116">Błędy sprawdzania poprawności wynikają z scenariusze, które można określić przed przystąpieniem do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c6638-116">Validation errors arise from scenarios that can be determined before deployment.</span></span> <span data-ttu-id="c6638-117">Obejmują one błędy składniowe w szablonie lub w trakcie zasobów toodeploy przekraczające przydziałami subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c6638-117">They include syntax errors in your template, or trying toodeploy resources that would exceed your subscription quotas.</span></span> <span data-ttu-id="c6638-118">Błędy wdrożenia wynikają z warunki, jakie występują podczas procesu wdrażania hello.</span><span class="sxs-lookup"><span data-stu-id="c6638-118">Deployment errors arise from conditions that occur during hello deployment process.</span></span> <span data-ttu-id="c6638-119">Obejmują one próby tooaccess z zasobem, który jest wdrażany jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="c6638-119">They include trying tooaccess a resource that is being deployed in parallel.</span></span>

<span data-ttu-id="c6638-120">Oba typy błędy zwracany błąd o kodzie użycie tootroubleshoot hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c6638-120">Both types of errors return an error code that you use tootroubleshoot hello deployment.</span></span> <span data-ttu-id="c6638-121">Oba typy błędy są wyświetlane w hello [dziennik aktywności](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="c6638-121">Both types of errors appear in hello [activity log](resource-group-audit.md).</span></span> <span data-ttu-id="c6638-122">Błędy sprawdzania poprawności nie pojawiają się jednak w historii wdrożenia, ponieważ wdrożenie hello nigdy nie jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="c6638-122">However, validation errors do not appear in your deployment history because hello deployment never started.</span></span>

## <a name="determine-error-code"></a><span data-ttu-id="c6638-123">Określić kod błędu:</span><span class="sxs-lookup"><span data-stu-id="c6638-123">Determine error code</span></span>

<span data-ttu-id="c6638-124">Informacje na temat błędu analizując komunikat o błędzie hello i hello kod błędu.</span><span class="sxs-lookup"><span data-stu-id="c6638-124">You can learn about an error by looking at hello error message and hello error code.</span></span> <span data-ttu-id="c6638-125">Witaj [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md) artykule wymieniono rozwiązania przez kod błędu.</span><span class="sxs-lookup"><span data-stu-id="c6638-125">hello [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md) article lists resolutions by error code.</span></span> <span data-ttu-id="c6638-126">W tym temacie przedstawiono sposób toouse hello kod błędu hello toodiscover portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6638-126">This topic shows how toouse hello Azure portal toodiscover hello error code.</span></span>

### <a name="validation-errors"></a><span data-ttu-id="c6638-127">Błędy sprawdzania poprawności</span><span class="sxs-lookup"><span data-stu-id="c6638-127">Validation errors</span></span>

<span data-ttu-id="c6638-128">W przypadku wdrażania za pośrednictwem portalu hello, zobaczysz błąd sprawdzania poprawności po przesłaniu wartości.</span><span class="sxs-lookup"><span data-stu-id="c6638-128">When deploying through hello portal, you see a validation error after submitting your values.</span></span>

![Pokaż błąd sprawdzania poprawności portalu](./media/resource-manager-troubleshoot-tips/validation-error.png)

<span data-ttu-id="c6638-130">Wybierz wiadomość hello więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="c6638-130">Select hello message for more details.</span></span> <span data-ttu-id="c6638-131">W hello po obrazu, zobacz **InvalidTemplateDeployment** błąd i komunikat informujący zasad zablokowane wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c6638-131">In hello following image, you see an **InvalidTemplateDeployment** error and a message that indicates a policy blocked deployment.</span></span>

![Pokaż szczegóły sprawdzania poprawności](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a><span data-ttu-id="c6638-133">Błędy wdrożenia</span><span class="sxs-lookup"><span data-stu-id="c6638-133">Deployment errors</span></span>

<span data-ttu-id="c6638-134">Podczas operacji hello pozytywnej weryfikacji, ale nie powiodło się podczas wdrażania, zostanie wyświetlony błąd hello w powiadomieniach hello.</span><span class="sxs-lookup"><span data-stu-id="c6638-134">When hello operation passes validation, but fails during deployment, you see hello error in hello notifications.</span></span> <span data-ttu-id="c6638-135">Wybierz powiadomienie hello.</span><span class="sxs-lookup"><span data-stu-id="c6638-135">Select hello notification.</span></span>

![Błąd powiadomienia](./media/resource-manager-troubleshoot-tips/notification.png)

<span data-ttu-id="c6638-137">Możesz dowiedzieć się więcej o wdrażaniu hello.</span><span class="sxs-lookup"><span data-stu-id="c6638-137">You see more details about hello deployment.</span></span> <span data-ttu-id="c6638-138">Wybierz więcej informacji o błędzie hello hello toofind opcji.</span><span class="sxs-lookup"><span data-stu-id="c6638-138">Select hello option toofind more information about hello error.</span></span>

![Wdrażanie nie powiodło się](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

<span data-ttu-id="c6638-140">Zostanie wyświetlony kody błędów hello wiadomości i błędów.</span><span class="sxs-lookup"><span data-stu-id="c6638-140">You see hello error message and error codes.</span></span> <span data-ttu-id="c6638-141">Należy zauważyć, że istnieją dwa kody błędów.</span><span class="sxs-lookup"><span data-stu-id="c6638-141">Notice there are two error codes.</span></span> <span data-ttu-id="c6638-142">Witaj pierwszy kod błędu (**niepowodzenia wdrożenia**) jest błąd ogólny, który nie zapewnia hello szczegółowe informacje możesz potrzeby toosolve hello błąd.</span><span class="sxs-lookup"><span data-stu-id="c6638-142">hello first error code (**DeploymentFailed**) is a general error that does not provide hello details you need toosolve hello error.</span></span> <span data-ttu-id="c6638-143">Witaj drugi kod błędu (**StorageAccountNotFound**) zawiera szczegóły hello potrzebne.</span><span class="sxs-lookup"><span data-stu-id="c6638-143">hello second error code (**StorageAccountNotFound**) provides hello details you need.</span></span> 

![Szczegóły błędu](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a><span data-ttu-id="c6638-145">Włączenie rejestrowania debugowania</span><span class="sxs-lookup"><span data-stu-id="c6638-145">Enable debug logging</span></span>
<span data-ttu-id="c6638-146">Czasami uzyskać więcej informacji dotyczących toodiscover żądań i odpowiedzi hello co poszło źle.</span><span class="sxs-lookup"><span data-stu-id="c6638-146">Sometimes you need more information about hello request and response toodiscover what went wrong.</span></span> <span data-ttu-id="c6638-147">Przy użyciu programu PowerShell lub interfejsu wiersza polecenia Azure, mogą żądać, aby uzyskać dodatkowe informacje jest rejestrowane podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="c6638-147">By using PowerShell or Azure CLI, you can request that additional information is logged during a deployment.</span></span>

- <span data-ttu-id="c6638-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6638-148">PowerShell</span></span>

   <span data-ttu-id="c6638-149">W programie PowerShell, należy ustawić hello **DeploymentDebugLogLevel** tooAll parametru, obiektu ResponseContent lub RequestContent.</span><span class="sxs-lookup"><span data-stu-id="c6638-149">In PowerShell, set hello **DeploymentDebugLogLevel** parameter tooAll, ResponseContent, or RequestContent.</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   <span data-ttu-id="c6638-150">Sprawdź zawartość żądania hello z hello następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c6638-150">Examine hello request content with hello following cmdlet:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   <span data-ttu-id="c6638-151">Lub hello zawartości z odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="c6638-151">Or, hello response content with:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   <span data-ttu-id="c6638-152">Te informacje mogą pomóc w określeniu, czy wartość w szablonie hello jest są ustawione niepoprawnie.</span><span class="sxs-lookup"><span data-stu-id="c6638-152">This information can help you determine whether a value in hello template is being incorrectly set.</span></span>

- <span data-ttu-id="c6638-153">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c6638-153">Azure CLI</span></span>

   <span data-ttu-id="c6638-154">Sprawdź operacje wdrażania hello z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="c6638-154">Examine hello deployment operations with hello following command:</span></span>

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- <span data-ttu-id="c6638-155">Szablon zagnieżdżony</span><span class="sxs-lookup"><span data-stu-id="c6638-155">Nested template</span></span>

   <span data-ttu-id="c6638-156">toolog informacji debugowania dla zagnieżdżony szablon, użyj hello **debugSetting** elementu.</span><span class="sxs-lookup"><span data-stu-id="c6638-156">toolog debug information for a nested template, use hello **debugSetting** element.</span></span>

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


## <a name="create-a-troubleshooting-template"></a><span data-ttu-id="c6638-157">Tworzenie szablonu rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="c6638-157">Create a troubleshooting template</span></span>
<span data-ttu-id="c6638-158">W niektórych przypadkach hello Najprostszym sposobem tootroubleshoot szablon jest tootest jej części.</span><span class="sxs-lookup"><span data-stu-id="c6638-158">In some cases, hello easiest way tootroubleshoot your template is tootest parts of it.</span></span> <span data-ttu-id="c6638-159">Można utworzyć szablon uproszczony, umożliwiającą toofocus na części hello uważasz, że przyczyną jest błąd hello.</span><span class="sxs-lookup"><span data-stu-id="c6638-159">You can create a simplified template that enables you toofocus on hello part that you believe is causing hello error.</span></span> <span data-ttu-id="c6638-160">Na przykład załóżmy, że otrzymujesz błąd podczas odwoływania się do zasobu.</span><span class="sxs-lookup"><span data-stu-id="c6638-160">For example, suppose you are receiving an error when referencing a resource.</span></span> <span data-ttu-id="c6638-161">Zamiast dotyczącą całą szablonu, utworzyć szablon, który zwraca część hello, który może być przyczyną tego problemu.</span><span class="sxs-lookup"><span data-stu-id="c6638-161">Rather than dealing with an entire template, create a template that returns hello part that may be causing your problem.</span></span> <span data-ttu-id="c6638-162">Możesz określić, czy jest przekazywany hello prawo parametrów, przy użyciu funkcji szablonu prawidłowo, i pobieranie zasobu hello oczekiwać może pomóc.</span><span class="sxs-lookup"><span data-stu-id="c6638-162">It can help you determine whether you are passing in hello right parameters, using template functions correctly, and getting hello resource you expect.</span></span>

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

<span data-ttu-id="c6638-163">Lub Załóżmy, że pojawiły się błędy wdrożenia, które Twoim zdaniem są powiązane zestawu tooincorrectly zależności.</span><span class="sxs-lookup"><span data-stu-id="c6638-163">Or, suppose you are encountering deployment errors that you believe are related tooincorrectly set dependencies.</span></span> <span data-ttu-id="c6638-164">Przetestuj szablonu przez podzielenie go na uproszczonej szablonów.</span><span class="sxs-lookup"><span data-stu-id="c6638-164">Test your template by breaking it into simplified templates.</span></span> <span data-ttu-id="c6638-165">Najpierw Utwórz szablon, który wdraża jednego zasobu (np. programu SQL Server).</span><span class="sxs-lookup"><span data-stu-id="c6638-165">First, create a template that deploys only a single resource (like a SQL Server).</span></span> <span data-ttu-id="c6638-166">Podczas pracy upewnić się, że ten zasób zdefiniowany prawidłowo, Dodaj zasób zależy od niego (na przykład baza danych SQL).</span><span class="sxs-lookup"><span data-stu-id="c6638-166">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span></span> <span data-ttu-id="c6638-167">Jeśli te dwa zasoby zdefiniowany prawidłowo, należy dodać inne zasoby zależne (na przykład zasady inspekcji).</span><span class="sxs-lookup"><span data-stu-id="c6638-167">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span></span> <span data-ttu-id="c6638-168">Between każdego wdrożenia testu Usuń hello grupy toomake się, że należy odpowiednio testowania hello zależności między zasobami.</span><span class="sxs-lookup"><span data-stu-id="c6638-168">In between each test deployment, delete hello resource group toomake sure you adequately testing hello dependencies.</span></span> 

## <a name="check-deployment-sequence"></a><span data-ttu-id="c6638-169">Sprawdź wdrożenie sekwencji</span><span class="sxs-lookup"><span data-stu-id="c6638-169">Check deployment sequence</span></span>

<span data-ttu-id="c6638-170">Wiele błędów wdrażania się tak zdarzyć, gdy zasoby są wdrożone w nieoczekiwany sekwencji.</span><span class="sxs-lookup"><span data-stu-id="c6638-170">Many deployment errors happen when resources are deployed in an unexpected sequence.</span></span> <span data-ttu-id="c6638-171">Te błędy wystąpić, gdy zależności nie są poprawnie ustawione.</span><span class="sxs-lookup"><span data-stu-id="c6638-171">These errors arise when dependencies are not correctly set.</span></span> <span data-ttu-id="c6638-172">Jeśli brakuje wymaganych zależności, jeden zasób prób toouse wartość innego zasobu, ale hello innych jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="c6638-172">When you are missing a needed dependency, one resource attempts toouse a value for another resource but hello other does not yet exist.</span></span> <span data-ttu-id="c6638-173">Otrzymasz komunikat o błędzie informujący, że zasób nie został znaleziony.</span><span class="sxs-lookup"><span data-stu-id="c6638-173">You get an error stating that a resource is not found.</span></span> <span data-ttu-id="c6638-174">Mogą wystąpić błędy tego typu sporadycznie hello czasu wdrożenia dla każdego zasobu może się różnić.</span><span class="sxs-lookup"><span data-stu-id="c6638-174">You may encounter this type of error intermittently because hello deployment time for each resource can vary.</span></span> <span data-ttu-id="c6638-175">Na przykład Twojego pierwszego toodeploy próba zasobami powiedzie się, ponieważ wymagany zasób jest przeprowadzany losowo w czasie.</span><span class="sxs-lookup"><span data-stu-id="c6638-175">For example, your first attempt toodeploy your resources succeeds because a required resource randomly completes in time.</span></span> <span data-ttu-id="c6638-176">Jednak z druga próba nie powiedzie się z powodu hello wymaganych zasobów nie została ukończona w czasie.</span><span class="sxs-lookup"><span data-stu-id="c6638-176">However, your second attempt fails because hello required resource did not complete in time.</span></span> 

<span data-ttu-id="c6638-177">Ale ma tooavoid Ustawianie zależności, które nie są wymagane.</span><span class="sxs-lookup"><span data-stu-id="c6638-177">But, you want tooavoid setting dependencies that are not needed.</span></span> <span data-ttu-id="c6638-178">Gdy niepotrzebne zależności, można przedłużyć czas trwania hello hello wdrożenia, zapobiegając zasoby, które nie są wzajemnie zależne od wdrażany równolegle.</span><span class="sxs-lookup"><span data-stu-id="c6638-178">When you have unnecessary dependencies, you prolong hello duration of hello deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="c6638-179">Ponadto można utworzyć zależności cykliczne, które blokują hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c6638-179">In addition, you may create circular dependencies that block hello deployment.</span></span> <span data-ttu-id="c6638-180">Witaj [odwołania](resource-group-template-functions-resource.md#reference) funkcja tworzy niejawne zależności hello odwołuje się do zasobu, gdy zasób jest wdrażany w hello tego samego szablonu.</span><span class="sxs-lookup"><span data-stu-id="c6638-180">hello [reference](resource-group-template-functions-resource.md#reference) function creates an implicit dependency on hello referenced resource, when that resource is deployed in hello same template.</span></span> <span data-ttu-id="c6638-181">W związku z tym może mieć zależności więcej niż określona w hello zależności hello **dependsOn** właściwości.</span><span class="sxs-lookup"><span data-stu-id="c6638-181">Therefore, you may have more dependencies than hello dependencies specified in hello **dependsOn** property.</span></span> <span data-ttu-id="c6638-182">Witaj [resourceId](resource-group-template-functions-resource.md#resourceid) funkcji nie utworzyć niejawnego zależności lub zweryfikować, że istnieje zasób hello.</span><span class="sxs-lookup"><span data-stu-id="c6638-182">hello [resourceId](resource-group-template-functions-resource.md#resourceid) function does not create an implicit dependency or validate that hello resource exists.</span></span>

<span data-ttu-id="c6638-183">W przypadku wystąpienia problemów zależności, należy toogain wgląd w kolejności hello wdrożenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="c6638-183">When you encounter dependency problems, you need toogain insight into hello order of resource deployment.</span></span> <span data-ttu-id="c6638-184">kolejność hello tooview operacji wdrażania:</span><span class="sxs-lookup"><span data-stu-id="c6638-184">tooview hello order of deployment operations:</span></span>

1. <span data-ttu-id="c6638-185">Wybierz hello historii wdrożenia dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c6638-185">Select hello deployment history for your resource group.</span></span>

   ![Wybierz Historia wdrażania](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. <span data-ttu-id="c6638-187">Wybierz wdrożenie z historii hello, a następnie wybierz **zdarzenia**.</span><span class="sxs-lookup"><span data-stu-id="c6638-187">Select a deployment from hello history, and select **Events**.</span></span>

   ![Wybierz zdarzenia wdrożenia](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. <span data-ttu-id="c6638-189">Sprawdź, czy hello sekwencji zdarzeń dla każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="c6638-189">Examine hello sequence of events for each resource.</span></span> <span data-ttu-id="c6638-190">Należy zwrócić uwagę toohello stan każdej operacji.</span><span class="sxs-lookup"><span data-stu-id="c6638-190">Pay attention toohello status of each operation.</span></span> <span data-ttu-id="c6638-191">Na przykład hello poniższej ilustracji przedstawiono trzy konta magazynu, które wdrożone równolegle.</span><span class="sxs-lookup"><span data-stu-id="c6638-191">For example, hello following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="c6638-192">Należy zauważyć, że hello trzy konta magazynu są uruchamiane na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="c6638-192">Notice that hello three storage accounts are started at hello same time.</span></span>

   ![Wdrożenie równoległe](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   <span data-ttu-id="c6638-194">Następny obraz powitania zawiera trzy konta magazynu, które nie są wdrażane równolegle.</span><span class="sxs-lookup"><span data-stu-id="c6638-194">hello next image shows three storage accounts that are not deployed in parallel.</span></span> <span data-ttu-id="c6638-195">Hello drugiego konta magazynu zależy od hello pierwsze konto magazynu, a trzeci konta magazynu hello zależy hello drugiego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="c6638-195">hello second storage account depends on hello first storage account, and hello third storage account depends on hello second storage account.</span></span> <span data-ttu-id="c6638-196">W związku z tym hello pierwsze konto magazynu jest uruchomiona, zaakceptowane i zakończona, zanim hello obok została uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="c6638-196">Therefore, hello first storage account is started, accepted, and completed before hello next is started.</span></span>

   ![kolejne wdrożenia](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

<span data-ttu-id="c6638-198">Nawet w przypadku bardziej złożonych zadań, można użyć tego samego toodiscover technika Witaj, podczas wdrażania zostanie rozpoczęte i zakończone dla każdego zasobu.</span><span class="sxs-lookup"><span data-stu-id="c6638-198">Even for more complicated scenarios, you can use hello same technique toodiscover when deployment is started and completed for each resource.</span></span> <span data-ttu-id="c6638-199">Przejrzyj toosee zdarzenia z wdrożenia, jeśli sekwencja hello jest inny niż oczekiwany.</span><span class="sxs-lookup"><span data-stu-id="c6638-199">Look through your deployment events toosee if hello sequence is different than you would expect.</span></span> <span data-ttu-id="c6638-200">Jeśli tak, można obliczyć ponownie hello zależności dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="c6638-200">If so, reevaluate hello dependencies for this resource.</span></span>

<span data-ttu-id="c6638-201">Menedżer zasobów identyfikuje zależności cykliczne podczas walidacji szablonu.</span><span class="sxs-lookup"><span data-stu-id="c6638-201">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="c6638-202">Zwraca się, że istnieje komunikat o błędzie stwierdzający, w szczególności zależność cykliczną.</span><span class="sxs-lookup"><span data-stu-id="c6638-202">It returns an error message that specifically states a circular dependency exists.</span></span> <span data-ttu-id="c6638-203">toosolve zależność cykliczną:</span><span class="sxs-lookup"><span data-stu-id="c6638-203">toosolve a circular dependency:</span></span>

1. <span data-ttu-id="c6638-204">W szablonie należy znaleźć zasobu hello objęci hello zależność cykliczną.</span><span class="sxs-lookup"><span data-stu-id="c6638-204">In your template, find hello resource identified in hello circular dependency.</span></span> 
2. <span data-ttu-id="c6638-205">Dla tego zasobu, sprawdź hello **dependsOn** właściwości i wszelkie używa hello **odwołania** toosee zasobów, do których ona zależy od funkcji.</span><span class="sxs-lookup"><span data-stu-id="c6638-205">For that resource, examine hello **dependsOn** property and any uses of hello **reference** function toosee which resources it depends on.</span></span> 
3. <span data-ttu-id="c6638-206">Sprawdź, czy toosee tych zasobów, zasobów, do których one zależą od.</span><span class="sxs-lookup"><span data-stu-id="c6638-206">Examine those resources toosee which resources they depend on.</span></span> <span data-ttu-id="c6638-207">Wykonaj zależności hello dopóki zauważysz z zasobem, który jest zależny od zasobu oryginalnego hello.</span><span class="sxs-lookup"><span data-stu-id="c6638-207">Follow hello dependencies until you notice a resource that depends on hello original resource.</span></span>
5. <span data-ttu-id="c6638-208">Dla zasobów hello objętego hello zależność cykliczną, należy dokładnie zbadać wszystkich zastosowań hello **dependsOn** tooidentify właściwości wszelkie zależności, które nie są wymagane.</span><span class="sxs-lookup"><span data-stu-id="c6638-208">For hello resources involved in hello circular dependency, carefully examine all uses of hello **dependsOn** property tooidentify any dependencies that are not needed.</span></span> <span data-ttu-id="c6638-209">Usuń te zależności.</span><span class="sxs-lookup"><span data-stu-id="c6638-209">Remove those dependencies.</span></span> <span data-ttu-id="c6638-210">Jeśli nie wiesz, czy zależność jest potrzebny, spróbuj go usunąć.</span><span class="sxs-lookup"><span data-stu-id="c6638-210">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="c6638-211">Należy ponownie wdrożyć szablon hello.</span><span class="sxs-lookup"><span data-stu-id="c6638-211">Redeploy hello template.</span></span>

<span data-ttu-id="c6638-212">Usuwanie wartości z hello **dependsOn** właściwości, które mogą powodować błędy podczas wdrażania szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="c6638-212">Removing values from hello **dependsOn** property can cause errors when you deploy hello template.</span></span> <span data-ttu-id="c6638-213">Jeśli wystąpi błąd, należy dodać zależności hello do hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="c6638-213">If you encounter an error, add hello dependency back into hello template.</span></span> 

<span data-ttu-id="c6638-214">Jeśli takie podejście nie rozwiązuje hello zależność cykliczną, rozważ migrację część logiki wdrażania zasobów podrzędnych (na przykład rozszerzenia lub ustawienia konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="c6638-214">If that approach does not solve hello circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="c6638-215">Po hello zasoby związane z hello zależność cykliczną, należy skonfigurować te toodeploy zasoby podrzędne.</span><span class="sxs-lookup"><span data-stu-id="c6638-215">Configure those child resources toodeploy after hello resources involved in hello circular dependency.</span></span> <span data-ttu-id="c6638-216">Załóżmy na przykład wdrażasz dwóch maszyn wirtualnych, ale należy ustawić na każdej z nich, która odwołuje się toohello innych właściwości.</span><span class="sxs-lookup"><span data-stu-id="c6638-216">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="c6638-217">Można je wdrożyć w hello w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="c6638-217">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="c6638-218">vm1</span><span class="sxs-lookup"><span data-stu-id="c6638-218">vm1</span></span>
2. <span data-ttu-id="c6638-219">maszyny vm2</span><span class="sxs-lookup"><span data-stu-id="c6638-219">vm2</span></span>
3. <span data-ttu-id="c6638-220">Rozszerzenie na vm1 zależy od vm1 i maszyny vm2.</span><span class="sxs-lookup"><span data-stu-id="c6638-220">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="c6638-221">rozszerzenie Hello ustawia wartości vm1, który otrzymuje od maszyny vm2.</span><span class="sxs-lookup"><span data-stu-id="c6638-221">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="c6638-222">Rozszerzenie maszyny vm2 zależy od vm1 i maszyny vm2.</span><span class="sxs-lookup"><span data-stu-id="c6638-222">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="c6638-223">rozszerzenie Hello ustawia wartości maszyny vm2, który otrzymuje od vm1.</span><span class="sxs-lookup"><span data-stu-id="c6638-223">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="c6638-224">Witaj, które same podejście działa w przypadku aplikacji usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="c6638-224">hello same approach works for App Service apps.</span></span> <span data-ttu-id="c6638-225">Rozważ przeniesienie do zasobu podrzędnego zasób aplikacji hello wartości konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c6638-225">Consider moving configuration values into a child resource of hello app resource.</span></span> <span data-ttu-id="c6638-226">Można wdrożyć dwie aplikacje sieci web w hello w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="c6638-226">You can deploy two web apps in hello following order:</span></span>

1. <span data-ttu-id="c6638-227">webapp1</span><span class="sxs-lookup"><span data-stu-id="c6638-227">webapp1</span></span>
2. <span data-ttu-id="c6638-228">webapp2</span><span class="sxs-lookup"><span data-stu-id="c6638-228">webapp2</span></span>
3. <span data-ttu-id="c6638-229">Konfiguracja webapp1 zależy od webapp1 i webapp2.</span><span class="sxs-lookup"><span data-stu-id="c6638-229">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="c6638-230">Zawiera ustawienia aplikacji wartościami z webapp2.</span><span class="sxs-lookup"><span data-stu-id="c6638-230">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="c6638-231">Konfiguracja webapp2 zależy od webapp1 i webapp2.</span><span class="sxs-lookup"><span data-stu-id="c6638-231">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="c6638-232">Zawiera ustawienia aplikacji wartościami z webapp1.</span><span class="sxs-lookup"><span data-stu-id="c6638-232">It contains app settings with values from webapp1.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c6638-233">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6638-233">Next steps</span></span>
* <span data-ttu-id="c6638-234">Błędy wdrożenia toocommon rozwiązania, zobacz [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="c6638-234">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="c6638-235">toolearn o inspekcji akcji, zobacz [inspekcji operacji za pomocą Menedżera zasobów](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="c6638-235">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="c6638-236">toolearn o błędach hello toodetermine akcje podczas wdrażania, zobacz [wyświetlić operacje wdrażania](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="c6638-236">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
