---
title: "Korzystanie z platformy Azure zarządzanych aplikacji | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak klient tworzy platformy Azure zarządzanych aplikacji z plików publikowanych."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: ed8fbaf2a4546c8e31eeced11cd0b5627fd62c0c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="8d1bb-103">Korzystanie z wewnętrznej zarządzanej aplikacji</span><span class="sxs-lookup"><span data-stu-id="8d1bb-103">Consume an internal managed application</span></span>

<span data-ttu-id="8d1bb-104">Będzie można korzystać z usługi Azure [zarządzane aplikacje](managed-application-overview.md) które są przeznaczone do członków organizacji.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="8d1bb-105">Na przykład można wybrać aplikacje zarządzane przez dział IT, która zapewnić zgodność ze standardami w organizacji.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="8d1bb-106">Te aplikacje zarządzane są dostępne za pośrednictwem katalogu usług, a nie w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-106">These managed applications are available through the Service Catalog, not the Azure Marketplace.</span></span>

<span data-ttu-id="8d1bb-107">Przed kontynuowaniem w tym artykule, musi mieć zarządzanej aplikacji dostępnych w katalogu usług dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-107">Before proceeding with this article, you must have a managed application available in the service catalog for your subscription.</span></span> <span data-ttu-id="8d1bb-108">Jeśli ktoś w organizacji nie już utworzony zarządzanej aplikacji, zobacz [publikowania aplikacji zarządzanej na użytek wewnętrzny](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="8d1bb-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="8d1bb-109">Użycie aplikacji zarządzanej można obecnie używać interfejsu wiersza polecenia Azure lub w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-109">Currently, you can use either Azure CLI or the Azure portal to consume a managed application.</span></span>

## <a name="create-the-managed-application-by-using-the-portal"></a><span data-ttu-id="8d1bb-110">Tworzenie aplikacji zarządzanych za pomocą portalu</span><span class="sxs-lookup"><span data-stu-id="8d1bb-110">Create the managed application by using the portal</span></span>

<span data-ttu-id="8d1bb-111">Aby wdrożyć zarządzanych aplikacji za pośrednictwem portalu, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8d1bb-111">To deploy a managed application through the portal, follow these steps:</span></span>

1. <span data-ttu-id="8d1bb-112">Przejdź do portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-112">Go to the Azure portal.</span></span> <span data-ttu-id="8d1bb-113">Wyszukaj **katalogu usług zarządzanych aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Katalog usług zarządzanych aplikacji](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="8d1bb-115">Wybierz aplikację, którą ma zostać utworzona z listy dostępnych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-115">Select the managed application you want to create from the list of available solutions.</span></span> <span data-ttu-id="8d1bb-116">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-116">Select **Create**.</span></span>

   ![Wybór aplikacji zarządzanej](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="8d1bb-118">Podaj wartości parametrów, które są wymagane w celu zapewnienia zasobów.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-118">Provide values for the parameters that are required to provision the resources.</span></span> <span data-ttu-id="8d1bb-119">Wybierz **zachodnie centralnej nam** dla lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-119">Select **West Central US** for location.</span></span> <span data-ttu-id="8d1bb-120">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-120">Select **OK**.</span></span>

   ![Parametry aplikacji zarządzanych](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="8d1bb-122">Szablon weryfikuje podanych wartości.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-122">The template validates the values you provided.</span></span> <span data-ttu-id="8d1bb-123">Jeśli weryfikacja zakończy się powodzeniem, wybierz **OK** do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-123">If validation succeeds, select **OK** to start the deployment.</span></span>

   ![Sprawdzanie poprawności zarządzanej aplikacji](./media/managed-application-consumption/validation.png)

<span data-ttu-id="8d1bb-125">Po zakończeniu wdrożenia odpowiednie zasoby zdefiniowane w szablonie są udostępniane w grupie zasobów zarządzanych podane.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-125">After the deployment finishes, the appropriate resources defined in the template are provisioned in the managed resource group you provided.</span></span>

## <a name="create-the-managed-application-by-using-azure-cli"></a><span data-ttu-id="8d1bb-126">Tworzenie aplikacji zarządzanych za pomocą wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8d1bb-126">Create the managed application by using Azure CLI</span></span>

<span data-ttu-id="8d1bb-127">Istnieją dwa sposoby tworzenia aplikacji zarządzanej przy użyciu wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="8d1bb-127">There are two ways to create a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="8d1bb-128">Polecenie służące do tworzenia aplikacji zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-128">Use the command for creating managed applications.</span></span>
* <span data-ttu-id="8d1bb-129">Polecenie wdrożenia regularne szablonu.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-129">Use the regular template deployment command.</span></span>

### <a name="use-the-template-deployment-command"></a><span data-ttu-id="8d1bb-130">Polecenie wdrożenia szablonu</span><span class="sxs-lookup"><span data-stu-id="8d1bb-130">Use the template deployment command</span></span>

<span data-ttu-id="8d1bb-131">Wdróż plik applianceMainTemplate.json, utworzony przez dostawcę.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-131">Deploy the applianceMainTemplate.json file that the vendor created.</span></span>

<span data-ttu-id="8d1bb-132">Następnie należy utworzyć dwie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-132">Then create two resource groups.</span></span> <span data-ttu-id="8d1bb-133">Pierwsza grupa zasobów jest miejsce tworzenia zasobów zarządzanych aplikacji: Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-133">The first resource group is where the managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="8d1bb-134">Drugi grupa zasobów zawiera wszystkie zasoby zdefiniowane w mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-134">The second resource group contains all the resources defined in mainTemplate.json.</span></span> <span data-ttu-id="8d1bb-135">Ta grupa zasobów jest zarządzana przez niezależnego dostawcy oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-135">This resource group is managed by the ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="8d1bb-136">Użyj `westcentralus` jako lokalizacja grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-136">Use `westcentralus` as the location of the resource group.</span></span>
>

<span data-ttu-id="8d1bb-137">Aby wdrożyć applianceMainTemplate.json w mainResourceGroup, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8d1bb-137">To deploy applianceMainTemplate.json in mainResourceGroup, use the following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="8d1bb-138">Po uruchomieniu Powyższy szablon monituje o wartości parametrów, które są zdefiniowane w szablonie.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-138">After the preceding template runs, it prompts you for the values of the parameters that are defined in the template.</span></span> <span data-ttu-id="8d1bb-139">Oprócz parametrów, które są wymagane w celu zapewnienia zasobów w szablonie potrzebne są dwie wartości parametrów klucza:</span><span class="sxs-lookup"><span data-stu-id="8d1bb-139">In addition to the parameters that are needed to provision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="8d1bb-140">**managedResourceGroupId**: identyfikator zawierającego zasoby zdefiniowane w applianceMainTemplate.json grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-140">**managedResourceGroupId**: The ID of the resource group containing the resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="8d1bb-141">Identyfikator ma postać `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-141">The ID is of the form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="8d1bb-142">W powyższym przykładzie jest Identyfikatorem `managedResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-142">In the preceding example, it's the ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="8d1bb-143">**applianceDefinitionId**: identyfikator zasobu definicji zarządzanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-143">**applianceDefinitionId**: The ID of the managed application definition resource.</span></span> <span data-ttu-id="8d1bb-144">Ta wartość jest dostarczana przez niezależnego dostawcy oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-144">This value is provided by the ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="8d1bb-145">Wydawca muszą udzielić dostępu do grupy zasobów, który zawiera definicję aplikacji zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-145">The publisher must grant access to the resource group that contains the managed application definition.</span></span> <span data-ttu-id="8d1bb-146">Definicja zasobu jest tworzony w subskrypcji wydawcy.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-146">The definition resource is created in the publisher subscription.</span></span> <span data-ttu-id="8d1bb-147">W związku z tym użytkownika, grupy użytkowników lub aplikacji w dzierżawie klienta musi dostęp do odczytu do tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-147">Therefore, a user, user group, or application in the customer tenant needs read access to this resource.</span></span>

<span data-ttu-id="8d1bb-148">Po pomyślnym wdrożeniu, zobacz tworzone aplikacja zarządzana w mainResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-148">After the deployment finishes successfully, you see the managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="8d1bb-149">Zasób konto magazynu jest tworzony w managedResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-149">The storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-the-create-command"></a><span data-ttu-id="8d1bb-150">Użyj polecenia create</span><span class="sxs-lookup"><span data-stu-id="8d1bb-150">Use the create command</span></span>

<span data-ttu-id="8d1bb-151">Można użyć `az managedapp create` polecenie, aby utworzyć zarządzaną aplikację z definicji zarządzanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-151">You can use the `az managedapp create` command to create a managed application from the managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="8d1bb-152">**Identyfikator urządzenia definicji**: identyfikator zasobu w definicji zarządzanych aplikacji utworzony w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-152">**appliance-definition-Id**: The resource ID of the managed application definition created in the preceding step.</span></span> <span data-ttu-id="8d1bb-153">Aby uzyskać ten identyfikator, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="8d1bb-153">To obtain this ID, run the following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="8d1bb-154">To polecenie zwraca definicji zarządzanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-154">This command returns the managed application definition.</span></span> <span data-ttu-id="8d1bb-155">Należy wartość właściwości identyfikator.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-155">You need the value of the ID property.</span></span>

* <span data-ttu-id="8d1bb-156">**zarządzane-zarządcy zasobów id**: Nazwa grupy zasobów, zawierające zasoby zdefiniowane w applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-156">**managed-rg-id**: The name of the resource group containing the resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="8d1bb-157">Ta grupa zasobów to grupa zasobów zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-157">This resource group is the managed resource group.</span></span> <span data-ttu-id="8d1bb-158">Jest on zarządzany przez wydawcę.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-158">It's managed by the publisher.</span></span> <span data-ttu-id="8d1bb-159">Jeśli nie istnieje, jest tworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="8d1bb-160">**Grupa zasobów**: grupy zasobów, w którym utworzono zasób zarządzanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-160">**resource-group**: The resource group where the managed application resource is created.</span></span> <span data-ttu-id="8d1bb-161">Zasób Microsoft.Solutions/appliance znajduje się w tej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-161">The Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="8d1bb-162">**Parametry**: parametry, które są wymagane przez zasoby zdefiniowane w applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-162">**parameters**: The parameters that are needed for the resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="8d1bb-163">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="8d1bb-163">Known issues</span></span>

<span data-ttu-id="8d1bb-164">Ta wersja zapoznawcza zawiera następujące problemy:</span><span class="sxs-lookup"><span data-stu-id="8d1bb-164">This preview release includes the following issues:</span></span>

* <span data-ttu-id="8d1bb-165">Podczas tworzenia aplikacji zarządzanej pojawia się 500 Wewnętrzny błąd serwera.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-165">A 500 internal server error appears during the creation of the managed application.</span></span> <span data-ttu-id="8d1bb-166">Jeśli napotkasz problem prawdopodobnie występować sporadycznie.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-166">If you run into this issue, it's likely to be intermittent.</span></span> <span data-ttu-id="8d1bb-167">Spróbuj ponownie wykonać operację.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-167">Retry the operation.</span></span>
* <span data-ttu-id="8d1bb-168">Nowa grupa zasobów jest wymagany dla grupy zasobów zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-168">A new resource group is needed for the managed resource group.</span></span> <span data-ttu-id="8d1bb-169">Jeśli używasz istniejącej grupy zasobów, wdrożenie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-169">If you use an existing resource group, the deployment fails.</span></span>
* <span data-ttu-id="8d1bb-170">Należy utworzyć grupę zasobów, która zawiera zasób Microsoft.Solutions/appliances w **westcentralus** lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="8d1bb-170">The resource group that contains the Microsoft.Solutions/appliances resource must be created in the **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d1bb-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8d1bb-171">Next steps</span></span>

* <span data-ttu-id="8d1bb-172">Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [Omówienie aplikacji zarządzanych](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8d1bb-172">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="8d1bb-173">Aby dowiedzieć się, jak publikowanie aplikacji zarządzanych katalogu usług, zobacz [Utwórz i publikowanie aplikacji katalogu usług zarządzanych](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="8d1bb-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="8d1bb-174">Informacje dotyczące publikowania zarządzanych aplikacji w portalu Azure Marketplace, zobacz [Azure zarządzanych aplikacji w witrynie Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="8d1bb-174">For information about publishing managed applications to the Azure Marketplace, see [Azure managed applications in the Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="8d1bb-175">Aby dowiedzieć się, jak korzystanie z zarządzanych aplikacji z portalu Marketplace, zobacz [korzystać z platformy Azure zarządzanych aplikacji w witrynie Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="8d1bb-175">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
