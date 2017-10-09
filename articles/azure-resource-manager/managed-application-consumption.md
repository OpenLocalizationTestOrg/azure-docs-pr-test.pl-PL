---
title: "zarządzana aplikacja — aaaConsume platformy Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="3ace6-103">Korzystanie z wewnętrznej zarządzanej aplikacji</span><span class="sxs-lookup"><span data-stu-id="3ace6-103">Consume an internal managed application</span></span>

<span data-ttu-id="3ace6-104">Będzie można korzystać z usługi Azure [zarządzane aplikacje](managed-application-overview.md) które są przeznaczone do członków organizacji.</span><span class="sxs-lookup"><span data-stu-id="3ace6-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="3ace6-105">Na przykład można wybrać aplikacje zarządzane przez dział IT, która zapewnić zgodność ze standardami w organizacji.</span><span class="sxs-lookup"><span data-stu-id="3ace6-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="3ace6-106">Te aplikacje zarządzane są dostępne za pośrednictwem hello katalogu usług, hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3ace6-106">These managed applications are available through hello Service Catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="3ace6-107">Przed kontynuowaniem w tym artykule, musi mieć zarządzanej aplikacji dostępne w katalogu usług powitania dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3ace6-107">Before proceeding with this article, you must have a managed application available in hello service catalog for your subscription.</span></span> <span data-ttu-id="3ace6-108">Jeśli ktoś w organizacji nie już utworzony zarządzanej aplikacji, zobacz [publikowania aplikacji zarządzanej na użytek wewnętrzny](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="3ace6-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="3ace6-109">Obecnie można użyć wiersza polecenia platformy Azure lub hello Azure tooconsume portalu zarządzanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3ace6-109">Currently, you can use either Azure CLI or hello Azure portal tooconsume a managed application.</span></span>

## <a name="create-hello-managed-application-by-using-hello-portal"></a><span data-ttu-id="3ace6-110">Tworzenie aplikacji hello zarządzane przy użyciu portalu hello</span><span class="sxs-lookup"><span data-stu-id="3ace6-110">Create hello managed application by using hello portal</span></span>

<span data-ttu-id="3ace6-111">toodeploy zarządzanych aplikacji za pośrednictwem portalu hello, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3ace6-111">toodeploy a managed application through hello portal, follow these steps:</span></span>

1. <span data-ttu-id="3ace6-112">Przejdź toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3ace6-112">Go toohello Azure portal.</span></span> <span data-ttu-id="3ace6-113">Wyszukaj **katalogu usług zarządzanych aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="3ace6-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Katalog usług zarządzanych aplikacji](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="3ace6-115">Wybierz hello zarządzana aplikacja ma toocreate z listy hello dostępnych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="3ace6-115">Select hello managed application you want toocreate from hello list of available solutions.</span></span> <span data-ttu-id="3ace6-116">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="3ace6-116">Select **Create**.</span></span>

   ![Wybór aplikacji zarządzanej](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="3ace6-118">Podaj wartości parametrów hello, które są wymagane tooprovision hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="3ace6-118">Provide values for hello parameters that are required tooprovision hello resources.</span></span> <span data-ttu-id="3ace6-119">Wybierz **zachodnie centralnej nam** dla lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="3ace6-119">Select **West Central US** for location.</span></span> <span data-ttu-id="3ace6-120">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ace6-120">Select **OK**.</span></span>

   ![Parametry aplikacji zarządzanych](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="3ace6-122">Szablon Hello sprawdza poprawność wartości hello, podane.</span><span class="sxs-lookup"><span data-stu-id="3ace6-122">hello template validates hello values you provided.</span></span> <span data-ttu-id="3ace6-123">Jeśli weryfikacja zakończy się powodzeniem, wybierz **OK** toostart hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="3ace6-123">If validation succeeds, select **OK** toostart hello deployment.</span></span>

   ![Sprawdzanie poprawności zarządzanej aplikacji](./media/managed-application-consumption/validation.png)

<span data-ttu-id="3ace6-125">Po zakończeniu wdrożenia hello hello odpowiednie zasoby zdefiniowane w szablonie hello są udostępniane w grupie zasobów zarządzanych hello, podane.</span><span class="sxs-lookup"><span data-stu-id="3ace6-125">After hello deployment finishes, hello appropriate resources defined in hello template are provisioned in hello managed resource group you provided.</span></span>

## <a name="create-hello-managed-application-by-using-azure-cli"></a><span data-ttu-id="3ace6-126">Tworzenie aplikacji hello zarządzane przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3ace6-126">Create hello managed application by using Azure CLI</span></span>

<span data-ttu-id="3ace6-127">Istnieją dwa sposoby toocreate zarządzaną aplikację za pomocą wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="3ace6-127">There are two ways toocreate a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="3ace6-128">Polecenie hello do tworzenia aplikacji zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="3ace6-128">Use hello command for creating managed applications.</span></span>
* <span data-ttu-id="3ace6-129">Polecenie wdrożenia szablonu regularne hello.</span><span class="sxs-lookup"><span data-stu-id="3ace6-129">Use hello regular template deployment command.</span></span>

### <a name="use-hello-template-deployment-command"></a><span data-ttu-id="3ace6-130">Polecenie wdrożenia szablonu hello</span><span class="sxs-lookup"><span data-stu-id="3ace6-130">Use hello template deployment command</span></span>

<span data-ttu-id="3ace6-131">Wdróż plik applianceMainTemplate.json hello hello dostawcy utworzone.</span><span class="sxs-lookup"><span data-stu-id="3ace6-131">Deploy hello applianceMainTemplate.json file that hello vendor created.</span></span>

<span data-ttu-id="3ace6-132">Następnie należy utworzyć dwie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="3ace6-132">Then create two resource groups.</span></span> <span data-ttu-id="3ace6-133">Witaj pierwszej grupy zasobów jest gdzie hello aplikacji zarządzanej jest utworzony zasób: Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="3ace6-133">hello first resource group is where hello managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="3ace6-134">Witaj drugi zawiera wszystkie hello zasoby zdefiniowane w mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="3ace6-134">hello second resource group contains all hello resources defined in mainTemplate.json.</span></span> <span data-ttu-id="3ace6-135">Ta grupa zasobów jest zarządzana przez hello niezależnego dostawcy oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="3ace6-135">This resource group is managed by hello ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="3ace6-136">Użyj `westcentralus` jako lokalizacji hello hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="3ace6-136">Use `westcentralus` as hello location of hello resource group.</span></span>
>

<span data-ttu-id="3ace6-137">applianceMainTemplate.json toodeploy w mainResourceGroup, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="3ace6-137">toodeploy applianceMainTemplate.json in mainResourceGroup, use hello following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="3ace6-138">Po hello szablonu przebiegów poprzedzających monituje o podanie wartości hello hello parametrów, które są zdefiniowane w szablonie hello.</span><span class="sxs-lookup"><span data-stu-id="3ace6-138">After hello preceding template runs, it prompts you for hello values of hello parameters that are defined in hello template.</span></span> <span data-ttu-id="3ace6-139">Ponadto toohello parametrów, które są potrzebne zasoby tooprovision w szablonie, należy dwóch wartości parametrów klucza:</span><span class="sxs-lookup"><span data-stu-id="3ace6-139">In addition toohello parameters that are needed tooprovision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="3ace6-140">**managedResourceGroupId**: hello identyfikator hello zasobów grupy zawierające hello zasoby zdefiniowane w applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="3ace6-140">**managedResourceGroupId**: hello ID of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="3ace6-141">Identyfikator Hello ma formę hello `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span><span class="sxs-lookup"><span data-stu-id="3ace6-141">hello ID is of hello form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="3ace6-142">W hello poprzedzających przykładzie, tego Identyfikatora hello `managedResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="3ace6-142">In hello preceding example, it's hello ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="3ace6-143">**applianceDefinitionId**: hello identyfikator hello zarządzanych zasobów definicji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3ace6-143">**applianceDefinitionId**: hello ID of hello managed application definition resource.</span></span> <span data-ttu-id="3ace6-144">Ta wartość jest dostarczana przez hello niezależnego dostawcy oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="3ace6-144">This value is provided by hello ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="3ace6-145">Wydawca Hello musi udzielić dostępu toohello zasobów grupy, która zawiera definicję aplikacji hello zarządzane.</span><span class="sxs-lookup"><span data-stu-id="3ace6-145">hello publisher must grant access toohello resource group that contains hello managed application definition.</span></span> <span data-ttu-id="3ace6-146">w subskrypcji wydawcy hello zostanie utworzona Hello definicji zasobu.</span><span class="sxs-lookup"><span data-stu-id="3ace6-146">hello definition resource is created in hello publisher subscription.</span></span> <span data-ttu-id="3ace6-147">W związku z tym użytkownika, grupy użytkowników lub aplikacji w dzierżawie klienta hello musi zasobów toothis dostęp do odczytu.</span><span class="sxs-lookup"><span data-stu-id="3ace6-147">Therefore, a user, user group, or application in hello customer tenant needs read access toothis resource.</span></span>

<span data-ttu-id="3ace6-148">Po hello wdrożenie zakończy się pomyślnie, zobacz hello zarządzane w mainResourceGroup tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3ace6-148">After hello deployment finishes successfully, you see hello managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="3ace6-149">Witaj storageAccount zasób został utworzony w managedResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="3ace6-149">hello storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-hello-create-command"></a><span data-ttu-id="3ace6-150">Użyj hello Utwórz polecenie</span><span class="sxs-lookup"><span data-stu-id="3ace6-150">Use hello create command</span></span>

<span data-ttu-id="3ace6-151">Można użyć hello `az managedapp create` toocreate polecenia zarządzanej aplikacji z hello zarządzane definicji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3ace6-151">You can use hello `az managedapp create` command toocreate a managed application from hello managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="3ace6-152">**Identyfikator urządzenia definicji**: identyfikator zasobu hello hello zarządzane utworzone w hello poprzedzających krok definicji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3ace6-152">**appliance-definition-Id**: hello resource ID of hello managed application definition created in hello preceding step.</span></span> <span data-ttu-id="3ace6-153">tooobtain ten identyfikator, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="3ace6-153">tooobtain this ID, run hello following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="3ace6-154">To polecenie zwraca definicji aplikacji hello zarządzane.</span><span class="sxs-lookup"><span data-stu-id="3ace6-154">This command returns hello managed application definition.</span></span> <span data-ttu-id="3ace6-155">Należy wartość hello hello identyfikator właściwości.</span><span class="sxs-lookup"><span data-stu-id="3ace6-155">You need hello value of hello ID property.</span></span>

* <span data-ttu-id="3ace6-156">**zarządzane-zarządcy zasobów id**: Nazwa hello hello zasobów grupy zawierające hello zasoby zdefiniowane w applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="3ace6-156">**managed-rg-id**: hello name of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="3ace6-157">Ta grupa zasobów to grupa zasobów zarządzanych hello.</span><span class="sxs-lookup"><span data-stu-id="3ace6-157">This resource group is hello managed resource group.</span></span> <span data-ttu-id="3ace6-158">Zarządza hello wydawcy.</span><span class="sxs-lookup"><span data-stu-id="3ace6-158">It's managed by hello publisher.</span></span> <span data-ttu-id="3ace6-159">Jeśli nie istnieje, jest tworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="3ace6-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="3ace6-160">**Grupa zasobów**: utworzono hello grupy zasobów, której hello zarządzanych zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3ace6-160">**resource-group**: hello resource group where hello managed application resource is created.</span></span> <span data-ttu-id="3ace6-161">Witaj Microsoft.Solutions/appliance zasobów znajduje się w tej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="3ace6-161">hello Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="3ace6-162">**Parametry**: hello parametrów, które są wymagane przez hello zasoby zdefiniowane w applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="3ace6-162">**parameters**: hello parameters that are needed for hello resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="3ace6-163">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="3ace6-163">Known issues</span></span>

<span data-ttu-id="3ace6-164">Ta wersja zapoznawcza zawiera hello następujące problemy:</span><span class="sxs-lookup"><span data-stu-id="3ace6-164">This preview release includes hello following issues:</span></span>

* <span data-ttu-id="3ace6-165">Podczas tworzenia hello hello zarządzanych aplikacji zostanie wyświetlony 500 Wewnętrzny błąd serwera.</span><span class="sxs-lookup"><span data-stu-id="3ace6-165">A 500 internal server error appears during hello creation of hello managed application.</span></span> <span data-ttu-id="3ace6-166">Jeśli napotkasz problem jest prawdopodobnie toobe tymczasowymi.</span><span class="sxs-lookup"><span data-stu-id="3ace6-166">If you run into this issue, it's likely toobe intermittent.</span></span> <span data-ttu-id="3ace6-167">Ponów operację hello.</span><span class="sxs-lookup"><span data-stu-id="3ace6-167">Retry hello operation.</span></span>
* <span data-ttu-id="3ace6-168">Nowa grupa zasobów jest wymagany dla grupy zasobów zarządzanych hello.</span><span class="sxs-lookup"><span data-stu-id="3ace6-168">A new resource group is needed for hello managed resource group.</span></span> <span data-ttu-id="3ace6-169">Jeśli używasz istniejącej grupy zasobów, hello wdrożenie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="3ace6-169">If you use an existing resource group, hello deployment fails.</span></span>
* <span data-ttu-id="3ace6-170">Witaj grupę zasobów zawierającą hello Microsoft.Solutions/appliances zasobów muszą być tworzone w hello **westcentralus** lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="3ace6-170">hello resource group that contains hello Microsoft.Solutions/appliances resource must be created in hello **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ace6-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3ace6-171">Next steps</span></span>

* <span data-ttu-id="3ace6-172">Wprowadzenie toomanaged aplikacji, zobacz [Omówienie aplikacji zarządzanych](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3ace6-172">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="3ace6-173">Aby dowiedzieć się, jak publikowanie aplikacji zarządzanych katalogu usług, zobacz [Utwórz i publikowanie aplikacji katalogu usług zarządzanych](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="3ace6-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="3ace6-174">Aby informacji na temat publikowania aplikacji zarządzanych toohello portalu Azure Marketplace, zobacz [Azure zarządzanych aplikacji w portalu Marketplace hello](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="3ace6-174">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="3ace6-175">Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanej z hello Marketplace, zobacz [korzystać z platformy Azure zarządzanych aplikacji w portalu Marketplace hello](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="3ace6-175">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
