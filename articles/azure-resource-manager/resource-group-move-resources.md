---
title: "Przenoszenie zasobów platformy Azure do nowej grupy zasobów lub subskrypcji | Dokumentacja firmy Microsoft"
description: "Umożliwia przenoszenie zasobów do nowej grupy zasobów lub subskrypcji usługi Azure Resource Manager."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: e138f80e808968ab4bf5c11cfd5fd46fe4a1bcce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="move-resources-to-new-resource-group-or-subscription"></a><span data-ttu-id="b136c-103">Przenoszenie zasobów do nowej grupy zasobów lub subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b136c-103">Move resources to new resource group or subscription</span></span>
<span data-ttu-id="b136c-104">W tym temacie przedstawiono sposób przenoszenia zasobów do nowej subskrypcji lub nowej grupy zasobów w tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b136c-104">This topic shows you how to move resources to either a new subscription or a new resource group in the same subscription.</span></span> <span data-ttu-id="b136c-105">Aby przenieść zasobu można użyć portalu, programu PowerShell, interfejsu wiersza polecenia Azure lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="b136c-105">You can use the portal, PowerShell, Azure CLI, or the REST API to move resource.</span></span> <span data-ttu-id="b136c-106">Operacji przenoszenia w tym temacie są dostępne bez pomocy w pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b136c-106">The move operations in this topic are available to you without any assistance from Azure support.</span></span>

<span data-ttu-id="b136c-107">Podczas przenoszenia zasobów, zarówno grupy źródłowej i docelowej grupy są zablokowane podczas operacji.</span><span class="sxs-lookup"><span data-stu-id="b136c-107">When moving resources, both the source group and the target group are locked during the operation.</span></span> <span data-ttu-id="b136c-108">Zapisu i usuwania działań są zablokowane na grupy zasobów, dopiero po zakończeniu przenoszenia.</span><span class="sxs-lookup"><span data-stu-id="b136c-108">Write and delete operations are blocked on the resource groups until the move completes.</span></span> <span data-ttu-id="b136c-109">Ta blokada oznacza, że nie można dodawać, aktualizować lub usuwać zasoby w grupie zasobów, ale nie oznacza to, że zasoby są zablokowane.</span><span class="sxs-lookup"><span data-stu-id="b136c-109">This lock means you cannot add, update, or delete resources in the resource groups, but it does not mean the resources are frozen.</span></span> <span data-ttu-id="b136c-110">Na przykład jeśli zostanie przeniesiony do nowej grupy zasobów programu SQL Server i jego bazy danych, aplikacji korzystającej z bazy danych napotyka bez przestojów.</span><span class="sxs-lookup"><span data-stu-id="b136c-110">For example, if you move a SQL Server and its database to a new resource group, an application that uses the database experiences no downtime.</span></span> <span data-ttu-id="b136c-111">Można nadal odczytu i zapisu w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="b136c-111">It can still read and write to the database.</span></span>

<span data-ttu-id="b136c-112">Nie można zmienić lokalizacji zasobu.</span><span class="sxs-lookup"><span data-stu-id="b136c-112">You cannot change the location of the resource.</span></span> <span data-ttu-id="b136c-113">Przeniesienie zasobu tylko przenosi je do nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="b136c-113">Moving a resource only moves it to a new resource group.</span></span> <span data-ttu-id="b136c-114">Nową grupę zasobów może zawierać innej lokalizacji, ale nie zmienia lokalizację zasobu.</span><span class="sxs-lookup"><span data-stu-id="b136c-114">The new resource group may have a different location, but that does not change the location of the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="b136c-115">W tym artykule opisano sposób przenoszenia zasobów w ramach platformy Azure istniejącego konta wysyłania ofert.</span><span class="sxs-lookup"><span data-stu-id="b136c-115">This article describes how to move resources within an existing Azure account offering.</span></span> <span data-ttu-id="b136c-116">Jeśli rzeczywiście chcesz zmienić konta platformy Azure oferty (takich jak uaktualnianie z płatność za rzeczywiste użycie wstępnie zapłacenia) podczas kontynuowanie pracy z istniejących zasobów, zobacz [Przełącz subskrypcji platformy Azure do innej oferty](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="b136c-116">If you actually want to change your Azure account offering (such as upgrading from pay-as-you-go to pre-pay) while continuing to work with your existing resources, see [Switch your Azure subscription to another offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="b136c-117">Lista kontrolna przed przeniesieniem zasobów</span><span class="sxs-lookup"><span data-stu-id="b136c-117">Checklist before moving resources</span></span>
<span data-ttu-id="b136c-118">Przed przeniesieniem zasobu należy wykonać kilka ważnych kroków.</span><span class="sxs-lookup"><span data-stu-id="b136c-118">There are some important steps to perform before moving a resource.</span></span> <span data-ttu-id="b136c-119">Dzięki sprawdzeniu tych warunków można uniknąć błędów.</span><span class="sxs-lookup"><span data-stu-id="b136c-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="b136c-120">Subskrypcje źródłowych i docelowych musi istnieć w tym samym [dzierżawy usługi Azure Active Directory](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="b136c-120">The source and destination subscriptions must exist within the same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="b136c-121">Aby sprawdzić, czy obie subskrypcje mają ten sam identyfikator dzierżawy, użyj programu Azure PowerShell lub interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b136c-121">To check that both subscriptions have the same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="b136c-122">Dla programu Azure PowerShell użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="b136c-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="b136c-123">Azure CLI 2.0 należy użyć:</span><span class="sxs-lookup"><span data-stu-id="b136c-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="b136c-124">Dzierżawy identyfikatorów subskrypcji źródłowych i docelowych nie są takie same, możesz spróbować zmienić katalogu dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b136c-124">If the tenant IDs for the source and destination subscriptions are not the same, you can attempt to change the directory for the subscription.</span></span> <span data-ttu-id="b136c-125">Jednak ta opcja jest dostępna tylko dla administratorów usługi, który jest zalogowany za pomocą konta Microsoft (nie konta organizacyjnego).</span><span class="sxs-lookup"><span data-stu-id="b136c-125">However, this option is only available to Service Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="b136c-126">Próba zmiany katalogu, zaloguj się do [klasyczny portal](https://manage.windowsazure.com/)i wybierz **ustawienia**i wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="b136c-126">To attempt changing the directory, log in to the [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select the subscription.</span></span> <span data-ttu-id="b136c-127">Jeśli **Edytuj katalog** ikona jest dostępna, zaznacz go, aby zmienić skojarzone usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b136c-127">If the **Edit Directory** icon is available, select it to change the associated Azure Active Directory.</span></span>

  ![Edytowanie katalogu](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="b136c-129">Jeśli tej ikony nie jest dostępna, należy się z pomocą techniczną przeniesienie zasobów do nowej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="b136c-129">If that icon is not available, you must contact support to move the resources to a new tenant.</span></span>

2. <span data-ttu-id="b136c-130">Usługa musi mieć możliwość przenoszenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="b136c-130">The service must enable the ability to move resources.</span></span> <span data-ttu-id="b136c-131">Ten temat zawiera listę usług, które umożliwiają przenoszenie zasobów i usług, które nie należy włączać przenoszenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="b136c-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="b136c-132">Subskrypcja docelowa musi być zarejestrowana dla dostawcy przenoszonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="b136c-132">The destination subscription must be registered for the resource provider of the resource being moved.</span></span> <span data-ttu-id="b136c-133">Jeśli nie, zostanie wyświetlony komunikat o błędzie informujący, że **subskrypcja nie jest zarejestrowana dla typu zasobu**.</span><span class="sxs-lookup"><span data-stu-id="b136c-133">If not, you receive an error stating that the **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="b136c-134">Ten problem może wystąpić podczas przenoszenia zasobu do nowej subskrypcji, która nigdy nie była używana z tym typem zasobu.</span><span class="sxs-lookup"><span data-stu-id="b136c-134">You might encounter this problem when moving a resource to a new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="b136c-135">Aby dowiedzieć się, jak sprawdzić stan rejestracji i zarejestrować dostawców zasobów, zobacz część [Resource providers and types](resource-manager-supported-services.md) (Dostawcy i typy zasobów).</span><span class="sxs-lookup"><span data-stu-id="b136c-135">To learn how to check the registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-to-call-support"></a><span data-ttu-id="b136c-136">Kiedy Zadzwoń do pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="b136c-136">When to call support</span></span>
<span data-ttu-id="b136c-137">Można przenieść najwięcej zasobów za pomocą operacji samoobsługi wyświetlany w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="b136c-137">You can move most resources through the self-service operations shown in this topic.</span></span> <span data-ttu-id="b136c-138">Użyj operacje samoobsługi:</span><span class="sxs-lookup"><span data-stu-id="b136c-138">Use the self-service operations to:</span></span>

* <span data-ttu-id="b136c-139">Przenieś zasoby usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b136c-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="b136c-140">Przenoszenie zasobów klasycznych zgodnie z [ograniczenia wdrażania klasycznego](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="b136c-140">Move classic resources according to the [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="b136c-141">Jeśli trzeba z działem pomocy technicznej:</span><span class="sxs-lookup"><span data-stu-id="b136c-141">Call support when you need to:</span></span>

* <span data-ttu-id="b136c-142">Przenoszenie zasobów dla nowego konta platformy Azure (i dzierżawy usługi Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="b136c-142">Move your resources to a new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="b136c-143">Przenoszenie zasobów klasycznych, ale występują problemy z ograniczeniami.</span><span class="sxs-lookup"><span data-stu-id="b136c-143">Move classic resources but are having trouble with the limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="b136c-144">Usługi, które pozwalają przenoszenia</span><span class="sxs-lookup"><span data-stu-id="b136c-144">Services that enable move</span></span>
<span data-ttu-id="b136c-145">Na razie usługi umożliwiające przeniesienie do nowej grupy zasobów i subskrypcji są:</span><span class="sxs-lookup"><span data-stu-id="b136c-145">For now, the services that enable moving to both a new resource group and subscription are:</span></span>

* <span data-ttu-id="b136c-146">API Management</span><span class="sxs-lookup"><span data-stu-id="b136c-146">API Management</span></span>
* <span data-ttu-id="b136c-147">Usługi aplikacji — aplikacje (aplikacje sieci web) — zobacz [ograniczenia usługi aplikacji](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="b136c-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="b136c-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="b136c-148">Application Insights</span></span>
* <span data-ttu-id="b136c-149">Automatyzacja</span><span class="sxs-lookup"><span data-stu-id="b136c-149">Automation</span></span>
* <span data-ttu-id="b136c-150">Batch</span><span class="sxs-lookup"><span data-stu-id="b136c-150">Batch</span></span>
* <span data-ttu-id="b136c-151">Mapy Bing</span><span class="sxs-lookup"><span data-stu-id="b136c-151">Bing Maps</span></span>
* <span data-ttu-id="b136c-152">CDN</span><span class="sxs-lookup"><span data-stu-id="b136c-152">CDN</span></span>
* <span data-ttu-id="b136c-153">Usługi w chmurze — zobacz [Classic deployment ograniczenia](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="b136c-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="b136c-154">Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="b136c-154">Cognitive Services</span></span>
* <span data-ttu-id="b136c-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="b136c-155">Content Moderator</span></span>
* <span data-ttu-id="b136c-156">Data Catalog</span><span class="sxs-lookup"><span data-stu-id="b136c-156">Data Catalog</span></span>
* <span data-ttu-id="b136c-157">Fabryka danych</span><span class="sxs-lookup"><span data-stu-id="b136c-157">Data Factory</span></span>
* <span data-ttu-id="b136c-158">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b136c-158">Data Lake Analytics</span></span>
* <span data-ttu-id="b136c-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b136c-159">Data Lake Store</span></span>
* <span data-ttu-id="b136c-160">DNS</span><span class="sxs-lookup"><span data-stu-id="b136c-160">DNS</span></span>
* <span data-ttu-id="b136c-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b136c-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="b136c-162">Usługa Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b136c-162">Event Hubs</span></span>
* <span data-ttu-id="b136c-163">Klastry HDInsight — zobacz [ograniczenia usługi HDInsight](#hdinsight-limitations)</span><span class="sxs-lookup"><span data-stu-id="b136c-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="b136c-164">Centra IoT</span><span class="sxs-lookup"><span data-stu-id="b136c-164">IoT Hubs</span></span>
* <span data-ttu-id="b136c-165">Usługa Key Vault</span><span class="sxs-lookup"><span data-stu-id="b136c-165">Key Vault</span></span>
* <span data-ttu-id="b136c-166">Moduły równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="b136c-166">Load Balancers</span></span>
* <span data-ttu-id="b136c-167">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="b136c-167">Logic Apps</span></span>
* <span data-ttu-id="b136c-168">Usługa Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b136c-168">Machine Learning</span></span>
* <span data-ttu-id="b136c-169">Media Services</span><span class="sxs-lookup"><span data-stu-id="b136c-169">Media Services</span></span>
* <span data-ttu-id="b136c-170">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="b136c-170">Mobile Engagement</span></span>
* <span data-ttu-id="b136c-171">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="b136c-171">Notification Hubs</span></span>
* <span data-ttu-id="b136c-172">Operational Insights</span><span class="sxs-lookup"><span data-stu-id="b136c-172">Operational Insights</span></span>
* <span data-ttu-id="b136c-173">Operations Management</span><span class="sxs-lookup"><span data-stu-id="b136c-173">Operations Management</span></span>
* <span data-ttu-id="b136c-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="b136c-174">Power BI</span></span>
* <span data-ttu-id="b136c-175">Pamięć podręczna Redis</span><span class="sxs-lookup"><span data-stu-id="b136c-175">Redis Cache</span></span>
* <span data-ttu-id="b136c-176">Scheduler</span><span class="sxs-lookup"><span data-stu-id="b136c-176">Scheduler</span></span>
* <span data-ttu-id="b136c-177">Wyszukiwanie</span><span class="sxs-lookup"><span data-stu-id="b136c-177">Search</span></span>
* <span data-ttu-id="b136c-178">Zarządzanie serwerem</span><span class="sxs-lookup"><span data-stu-id="b136c-178">Server Management</span></span>
* <span data-ttu-id="b136c-179">Service Bus</span><span class="sxs-lookup"><span data-stu-id="b136c-179">Service Bus</span></span>
* <span data-ttu-id="b136c-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b136c-180">Service Fabric</span></span>
* <span data-ttu-id="b136c-181">Magazyn</span><span class="sxs-lookup"><span data-stu-id="b136c-181">Storage</span></span>
* <span data-ttu-id="b136c-182">Magazyn (klasyczne) — zobacz [Classic deployment ograniczenia](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="b136c-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="b136c-183">Stream Analytics — usługi analiza strumienia zadania nie można przenieść uruchomionej w stanie.</span><span class="sxs-lookup"><span data-stu-id="b136c-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="b136c-184">Baza danych SQL server — bazy danych i serwera musi znajdować się w tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="b136c-184">SQL Database server - The database and server must reside in the same resource group.</span></span> <span data-ttu-id="b136c-185">W przypadku przenoszenia programu SQL server, również są przenoszone jej baz danych.</span><span class="sxs-lookup"><span data-stu-id="b136c-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="b136c-186">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="b136c-186">Traffic Manager</span></span>
* <span data-ttu-id="b136c-187">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="b136c-187">Virtual Machines</span></span>
* <span data-ttu-id="b136c-188">Maszyny wirtualne z certyfikatem przechowywane w magazynie kluczy - Przenieś do nowego zasobu, grupy w tej samej subskrypcji jest włączona, ale przenoszenia między subskrypcji nie jest włączona.</span><span class="sxs-lookup"><span data-stu-id="b136c-188">Virtual Machines with certificate stored in Key Vault - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="b136c-189">Maszyny wirtualne (klasyczne) — zobacz [Classic deployment ograniczenia](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="b136c-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="b136c-190">Zestawy skali maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="b136c-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="b136c-191">Sieci wirtualne — obecnie, peered sieci wirtualnej nie można przenieść do momentu równorzędna sieci wirtualnej zostały wyłączone.</span><span class="sxs-lookup"><span data-stu-id="b136c-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="b136c-192">Po wyłączeniu sieci wirtualnej mogą zostać przeniesione pomyślnie i równorzędna sieci wirtualnej można włączyć.</span><span class="sxs-lookup"><span data-stu-id="b136c-192">Once disabled, the Virtual Network can be moved successfully and the VNet peering can be enabled.</span></span> <span data-ttu-id="b136c-193">Ponadto sieci wirtualnej nie można przenieść do innej subskrypcji, jeśli sieć wirtualna zawiera żadnej podsieci z zasobów łącza nawigacji.</span><span class="sxs-lookup"><span data-stu-id="b136c-193">In addition, a Virtual Network cannot be moved to a different subscription if the Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="b136c-194">Na przykład podsieć sieci wirtualnej ma łącza nawigacji zasobu, gdy zasób redis Microsoft.Cache zostaje wdrożona do tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="b136c-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="b136c-195">VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="b136c-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="b136c-196">Usługi, które nie należy włączać przenoszenia</span><span class="sxs-lookup"><span data-stu-id="b136c-196">Services that do not enable move</span></span>
<span data-ttu-id="b136c-197">Usługi, które aktualnie nie należy włączać przenoszenie zasobu to:</span><span class="sxs-lookup"><span data-stu-id="b136c-197">The services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="b136c-198">Usługi domenowe AD</span><span class="sxs-lookup"><span data-stu-id="b136c-198">AD Domain Services</span></span>
* <span data-ttu-id="b136c-199">Usługa kondycji hybrydowe AD</span><span class="sxs-lookup"><span data-stu-id="b136c-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="b136c-200">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="b136c-200">Application Gateway</span></span>
* <span data-ttu-id="b136c-201">Zestawy dostępności z maszynami wirtualnymi z dyskami zarządzane</span><span class="sxs-lookup"><span data-stu-id="b136c-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="b136c-202">BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="b136c-202">BizTalk Services</span></span>
* <span data-ttu-id="b136c-203">Container Service</span><span class="sxs-lookup"><span data-stu-id="b136c-203">Container Service</span></span>
* <span data-ttu-id="b136c-204">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b136c-204">Express Route</span></span>
* <span data-ttu-id="b136c-205">Włączono DevTest Labs — aby przejść do nowej grupy zasobów w tej samej subskrypcji, ale przenoszenia między subskrypcji nie jest włączona.</span><span class="sxs-lookup"><span data-stu-id="b136c-205">DevTest Labs - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="b136c-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="b136c-206">Dynamics LCS</span></span>
* <span data-ttu-id="b136c-207">Obrazy utworzone na podstawie zarządzanych dysków</span><span class="sxs-lookup"><span data-stu-id="b136c-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="b136c-208">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="b136c-208">Managed Disks</span></span>
* <span data-ttu-id="b136c-209">Zarządzane aplikacje</span><span class="sxs-lookup"><span data-stu-id="b136c-209">Managed Applications</span></span>
* <span data-ttu-id="b136c-210">Magazyn usług odzyskiwania — czy też nie przeniesienie zasobów obliczeniowych, sieci i magazynu skojarzone z magazynu usług odzyskiwania, zobacz [ograniczenia usług odzyskiwania](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="b136c-210">Recovery Services vault - also do not move the Compute, Network, and Storage resources associated with the Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="b136c-211">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="b136c-211">Security</span></span>
* <span data-ttu-id="b136c-212">Migawek utworzonych z dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="b136c-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="b136c-213">Menedżer urządzeń StorSimple</span><span class="sxs-lookup"><span data-stu-id="b136c-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="b136c-214">Maszyny wirtualne z dyskami zarządzanych</span><span class="sxs-lookup"><span data-stu-id="b136c-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="b136c-215">Sieci wirtualne (klasyczne) — zobacz [Classic deployment ograniczenia](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="b136c-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="b136c-216">Nie można przenieść maszyny wirtualne utworzone na podstawie zasobów Marketplace - różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b136c-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="b136c-217">Zasób musi zostać anulowana w bieżącej subskrypcji i wdrożyć ponownie w nowej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b136c-217">Resource needs to be deprovisioned in the current subscription and deployed again in the new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="b136c-218">Ograniczenia usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b136c-218">App Service limitations</span></span>
<span data-ttu-id="b136c-219">Podczas pracy z aplikacjami usługi App Service, nie można przenieść plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b136c-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="b136c-220">Aby przenieść aplikacji usługi App Service, dostępne są następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="b136c-220">To move App Service apps, your options are:</span></span>

* <span data-ttu-id="b136c-221">Przenieś plan usługi aplikacji i innych zasobów usługi aplikacji w tej grupie zasobów do nowej grupy zasobów, które jeszcze nie ma zasobów usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b136c-221">Move the App Service plan and all other App Service resources in that resource group to a new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="b136c-222">Wymaganie to oznacza, że należy przenieść nawet zasoby usługi aplikacji, które nie są skojarzone z planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b136c-222">This requirement means you must move even the App Service resources that are not associated with the App Service plan.</span></span>
* <span data-ttu-id="b136c-223">Przenieś aplikacje na innej grupie zasobów, ale zachować wszystkie plany usługi App Service w oryginalnej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="b136c-223">Move the apps to a different resource group, but keep all App Service plans in the original resource group.</span></span>

<span data-ttu-id="b136c-224">Plan usługi aplikacji nie musi znajdować się w tej samej grupie zasobów co aplikacja dla aplikacji do poprawnego działania.</span><span class="sxs-lookup"><span data-stu-id="b136c-224">The App Service plan does not need to reside in the same resource group as the app for the app to function correctly.</span></span>

<span data-ttu-id="b136c-225">Na przykład, jeśli zawiera grupie zasobów:</span><span class="sxs-lookup"><span data-stu-id="b136c-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="b136c-226">**sieci Web a** skojarzony z **planu a**</span><span class="sxs-lookup"><span data-stu-id="b136c-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="b136c-227">**sieci Web-b** skojarzony z **plan-b**</span><span class="sxs-lookup"><span data-stu-id="b136c-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="b136c-228">Dostępne opcje to:</span><span class="sxs-lookup"><span data-stu-id="b136c-228">Your options are:</span></span>

* <span data-ttu-id="b136c-229">Przenieś **sieci web a**, **planu a**, **sieci web-b**, i **plan-b**</span><span class="sxs-lookup"><span data-stu-id="b136c-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="b136c-230">Przenieś **sieci web a** i **b sieci web**</span><span class="sxs-lookup"><span data-stu-id="b136c-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="b136c-231">Przenieś **w sieci web**</span><span class="sxs-lookup"><span data-stu-id="b136c-231">Move **web-a**</span></span>
* <span data-ttu-id="b136c-232">Przenieś **b sieci web**</span><span class="sxs-lookup"><span data-stu-id="b136c-232">Move **web-b**</span></span>

<span data-ttu-id="b136c-233">Wszystkie inne kombinacje obejmują, pozostawiając w niej typ zasobu, który nie może pozostać podczas przenoszenia planu usługi App Service (dowolny typ zasobu usługi App Service).</span><span class="sxs-lookup"><span data-stu-id="b136c-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="b136c-234">Jeśli aplikacja sieci web znajduje się w innej grupie zasobów niż swój plan usługi aplikacji, ale chcesz przenieść zarówno do nowej grupy zasobów, należy wykonać czynności w dwóch krokach.</span><span class="sxs-lookup"><span data-stu-id="b136c-234">If your web app resides in a different resource group than its App Service plan but you want to move both to a new resource group, you must perform the move in two steps.</span></span> <span data-ttu-id="b136c-235">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="b136c-235">For example:</span></span>

* <span data-ttu-id="b136c-236">**sieci Web a** znajduje się w **grupy sieci web**</span><span class="sxs-lookup"><span data-stu-id="b136c-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="b136c-237">**Plan a** znajduje się w **planu grupy**</span><span class="sxs-lookup"><span data-stu-id="b136c-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="b136c-238">Ma **sieci web a** i **planu a** do znajdują się w **połączeniu grupy**</span><span class="sxs-lookup"><span data-stu-id="b136c-238">You want **web-a** and **plan-a** to reside in **combined-group**</span></span>

<span data-ttu-id="b136c-239">Aby zrobić to przeniesienie, należy wykonać dwie operacje przenoszenia oddzielne w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="b136c-239">To accomplish this move, perform two separate move operations in the following sequence:</span></span>

1. <span data-ttu-id="b136c-240">Przenieś **sieci web a** do **planu grupy**</span><span class="sxs-lookup"><span data-stu-id="b136c-240">Move the **web-a** to **plan-group**</span></span>
2. <span data-ttu-id="b136c-241">Przenieś **sieci web a** i **planu a** do **łączyć grupy**.</span><span class="sxs-lookup"><span data-stu-id="b136c-241">Move **web-a** and **plan-a** to **combined-group**.</span></span>

<span data-ttu-id="b136c-242">Certyfikat usługi aplikacji można przenieść do nowej grupy zasobów lub subskrypcji, bez żadnych problemów.</span><span class="sxs-lookup"><span data-stu-id="b136c-242">You can move an App Service Certificate to a new resource group or subscription without any issues.</span></span> <span data-ttu-id="b136c-243">Jednak jeśli aplikacja sieci web zawiera certyfikat SSL zakupionych zewnętrznie i przekazane do aplikacji, należy usunąć certyfikatu przed przeniesieniem aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b136c-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded to the app, you must delete the certificate before moving the web app.</span></span> <span data-ttu-id="b136c-244">Na przykład można wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b136c-244">For example, you can perform the following steps:</span></span>

1. <span data-ttu-id="b136c-245">Usuń przekazany certyfikat z aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="b136c-245">Delete the uploaded certificate from the web app</span></span>
2. <span data-ttu-id="b136c-246">Przenoszenie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="b136c-246">Move the web app</span></span>
3. <span data-ttu-id="b136c-247">Przekaż certyfikat do aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="b136c-247">Upload the certificate to the web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="b136c-248">Ograniczenia usługi odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="b136c-248">Recovery Services limitations</span></span>
<span data-ttu-id="b136c-249">Przenieś nie jest włączona dla magazynu, sieci lub używana do konfigurowania odzyskiwania po awarii z usługą Azure Site Recovery zasoby obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="b136c-249">Move is not enabled for Storage, Network, or Compute resources used to set up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="b136c-250">Na przykład załóżmy, że skonfigurowano replikację maszyn lokalnych do konta magazynu (Storage1) i chcesz chronionej maszyny znaleziona po w tryb failover na platformie Azure jako maszynę wirtualną (VM1) dołączona do sieci wirtualnej (Network1).</span><span class="sxs-lookup"><span data-stu-id="b136c-250">For example, suppose you have set up replication of your on-premises machines to a storage account (Storage1) and want the protected machine to come up after failover to Azure as a virtual machine (VM1) attached to a virtual network (Network1).</span></span> <span data-ttu-id="b136c-251">Nie można przenieść żadnego z tych zasobów Azure - Storage1 VM1 i Network1 - między grupami zasobów w ramach tej samej subskrypcji lub różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b136c-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within the same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="b136c-252">Ograniczenia usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="b136c-252">HDInsight limitations</span></span>

<span data-ttu-id="b136c-253">Klastry usługi HDInsight można przenieść do nowej subskrypcji lub grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="b136c-253">You can move HDInsight clusters to a new subscription or resource group.</span></span> <span data-ttu-id="b136c-254">Jednak nie można przenieść w subskrypcjach zasoby sieciowe połączone z klastrem usługi HDInsight (na przykład sieci wirtualnej, karty Sieciowej lub usługi równoważenia obciążenia).</span><span class="sxs-lookup"><span data-stu-id="b136c-254">However, you cannot move across subscriptions the networking resources linked to the HDInsight cluster (such as the virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="b136c-255">Ponadto nie można przenieść do nowej grupy zasobów kart interfejsu Sieciowego, który jest dołączony do maszyny wirtualnej do klastra.</span><span class="sxs-lookup"><span data-stu-id="b136c-255">In addition, you cannot move to a new resource group a NIC that is attached to a virtual machine for the cluster.</span></span>

<span data-ttu-id="b136c-256">Podczas przenoszenia klastra usługi HDInsight na nową subskrypcję, należy najpierw przenieść innych zasobów (takich jak konta magazynu).</span><span class="sxs-lookup"><span data-stu-id="b136c-256">When moving an HDInsight cluster to a new subscription, first move other resources (like the storage account).</span></span> <span data-ttu-id="b136c-257">Następnie przenieś klastra usługi HDInsight przez samego siebie.</span><span class="sxs-lookup"><span data-stu-id="b136c-257">Then, move the HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="b136c-258">Wdrożenie klasyczne ograniczenia</span><span class="sxs-lookup"><span data-stu-id="b136c-258">Classic deployment limitations</span></span>
<span data-ttu-id="b136c-259">Opcje przenoszenia zasobów wdrażać przy użyciu modelu klasycznego różnią się w zależności od tego, czy są przenoszenia zasobów w ramach subskrypcji lub do nowej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="b136c-259">The options for moving resources deployed through the classic model differ based on whether you are moving the resources within a subscription or to a new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="b136c-260">Tej samej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b136c-260">Same subscription</span></span>
<span data-ttu-id="b136c-261">Przenoszenie zasobów między grupami zasobów w innej grupie zasobów w ramach tej samej subskrypcji, mają zastosowanie następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="b136c-261">When moving resources from one resource group to another resource group within the same subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="b136c-262">Nie można przenieść sieci wirtualnych (klasyczny).</span><span class="sxs-lookup"><span data-stu-id="b136c-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="b136c-263">Maszyny wirtualne (klasyczne) muszą zostać przeniesione z usługą w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b136c-263">Virtual machines (classic) must be moved with the cloud service.</span></span>
* <span data-ttu-id="b136c-264">Usługi w chmurze tylko przeniesienia po przeniesieniu obejmuje wszystkie maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="b136c-264">Cloud service can only be moved when the move includes all its virtual machines.</span></span>
* <span data-ttu-id="b136c-265">Usługi w chmurze tylko jeden mogą zostać przeniesione w czasie.</span><span class="sxs-lookup"><span data-stu-id="b136c-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="b136c-266">Jednocześnie można przenosić tylko jedno konto magazynu (klasyczne).</span><span class="sxs-lookup"><span data-stu-id="b136c-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="b136c-267">Nie można przenieść konta magazynu (klasyczne) w tej samej operacji z maszyny wirtualnej lub usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b136c-267">Storage account (classic) cannot be moved in the same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="b136c-268">Aby przenieść zasoby klasyczne do nowej grupy zasobów w ramach tej samej subskrypcji, użyj operacji przenoszenia standardowe, za pomocą [portal](#use-portal), [programu Azure PowerShell](#use-powershell), [interfejsu wiersza polecenia Azure](#use-azure-cli), lub [interfejsu API REST](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="b136c-268">To move classic resources to a new resource group within the same subscription, use the standard move operations through the [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="b136c-269">Możesz użyć tej samej operacji, ponieważ używane do przenoszenia zasoby usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b136c-269">You use the same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="b136c-270">Nowa subskrypcja</span><span class="sxs-lookup"><span data-stu-id="b136c-270">New subscription</span></span>
<span data-ttu-id="b136c-271">Podczas przenoszenia zasobów na nową subskrypcję, obowiązują następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="b136c-271">When moving resources to a new subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="b136c-272">Wszystkie zasoby klasyczne w subskrypcji muszą zostać przeniesione w tej samej operacji.</span><span class="sxs-lookup"><span data-stu-id="b136c-272">All classic resources in the subscription must be moved in the same operation.</span></span>
* <span data-ttu-id="b136c-273">Subskrypcja docelowa nie może zawierać inne zasoby klasyczne.</span><span class="sxs-lookup"><span data-stu-id="b136c-273">The target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="b136c-274">Przeniesienie się żądać tylko wtedy za pomocą osobnych interfejsu API REST dla przenosi klasycznego.</span><span class="sxs-lookup"><span data-stu-id="b136c-274">The move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="b136c-275">Standardowe polecenia move Menedżera zasobów nie działają podczas przenoszenia zasobów klasycznych na nową subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="b136c-275">The standard Resource Manager move commands do not work when moving classic resources to a new subscription.</span></span>

<span data-ttu-id="b136c-276">Aby przenieść zasoby klasyczne do nowej subskrypcji, użyj operacji REST, które są specyficzne dla zasobów klasycznych.</span><span class="sxs-lookup"><span data-stu-id="b136c-276">To move classic resources to a new subscription, use the REST operations that are specific to classic resources.</span></span> <span data-ttu-id="b136c-277">Aby używać REST, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b136c-277">To use REST, perform the following steps:</span></span>

1. <span data-ttu-id="b136c-278">Sprawdź, czy subskrypcja źródłowa mogą uczestniczyć w przeniesienia między subskrypcjami.</span><span class="sxs-lookup"><span data-stu-id="b136c-278">Check if the source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="b136c-279">Użyj następujących operacji:</span><span class="sxs-lookup"><span data-stu-id="b136c-279">Use the following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="b136c-280">W treści żądania obejmują:</span><span class="sxs-lookup"><span data-stu-id="b136c-280">In the request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="b136c-281">Odpowiedź dla operacji sprawdzania poprawności jest w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="b136c-281">The response for the validation operation is in the following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="b136c-282">Sprawdź, czy subskrypcji docelowej mogą uczestniczyć w przeniesienia między subskrypcjami.</span><span class="sxs-lookup"><span data-stu-id="b136c-282">Check if the destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="b136c-283">Użyj następujących operacji:</span><span class="sxs-lookup"><span data-stu-id="b136c-283">Use the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="b136c-284">W treści żądania obejmują:</span><span class="sxs-lookup"><span data-stu-id="b136c-284">In the request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="b136c-285">Odpowiedź jest w tym samym formacie co sprawdzania poprawności subskrypcji źródłowej.</span><span class="sxs-lookup"><span data-stu-id="b136c-285">The response is in the same format as the source subscription validation.</span></span>
3. <span data-ttu-id="b136c-286">Jeśli obie subskrypcje przeszedł sprawdzania poprawności, Przenieś wszystkie zasoby klasyczne z jedną subskrypcję, do innej subskrypcji z następujących operacji:</span><span class="sxs-lookup"><span data-stu-id="b136c-286">If both subscriptions pass validation, move all classic resources from one subscription to another subscription with the following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="b136c-287">W treści żądania obejmują:</span><span class="sxs-lookup"><span data-stu-id="b136c-287">In the request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="b136c-288">Operacja może trwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="b136c-288">The operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="b136c-289">Korzystanie z portalu</span><span class="sxs-lookup"><span data-stu-id="b136c-289">Use portal</span></span>
<span data-ttu-id="b136c-290">Instrukcję przenoszenia zasobów, wybierz grupę zasobów, zawierające te zasoby, a następnie wybierz **Przenieś** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b136c-290">To move resources, select the resource group containing those resources, and then select the **Move** button.</span></span>

![Przenoszenie zasobów](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="b136c-292">Określ, czy przenosisz zasobów do nowej grupy zasobów lub nową subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="b136c-292">Select whether you are moving the resources to a new resource group or a new subscription.</span></span>

<span data-ttu-id="b136c-293">Wybierz zasoby do przeniesienia i docelowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="b136c-293">Select the resources to move and the destination resource group.</span></span> <span data-ttu-id="b136c-294">Potwierdzić, że trzeba zaktualizować skrypty dla tych zasobów i wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="b136c-294">Acknowledge that you need to update scripts for these resources and select **OK**.</span></span> <span data-ttu-id="b136c-295">Jeśli w poprzednim kroku zostało wybrane ikonę Edytuj subskrypcję, musisz wybrać subskrypcji docelowej.</span><span class="sxs-lookup"><span data-stu-id="b136c-295">If you selected the edit subscription icon in the previous step, you must also select the destination subscription.</span></span>

![Wybierz miejsce docelowe](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="b136c-297">W **powiadomienia**, zobaczysz, że działa operacji przenoszenia.</span><span class="sxs-lookup"><span data-stu-id="b136c-297">In **Notifications**, you see that the move operation is running.</span></span>

![Pokaż stan przenoszenia](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="b136c-299">Po ukończeniu, użytkownik jest powiadamiany o wynik.</span><span class="sxs-lookup"><span data-stu-id="b136c-299">When it has completed, you are notified of the result.</span></span>

![Pokaż Przenieś wyników](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="b136c-301">Korzystanie z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b136c-301">Use PowerShell</span></span>
<span data-ttu-id="b136c-302">Aby przenieść istniejące zasoby do innej grupy zasobów lub subskrypcji, należy użyć `Move-AzureRmResource` polecenia.</span><span class="sxs-lookup"><span data-stu-id="b136c-302">To move existing resources to another resource group or subscription, use the `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="b136c-303">Pierwszym przykładzie pokazano, jak można przenieść jeden zasób do nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="b136c-303">The first example shows how to move one resource to a new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="b136c-304">Drugi przykład przedstawia sposób przenoszenia wielu zasobów do nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="b136c-304">The second example shows how to move multiple resources to a new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="b136c-305">Aby przejść do nowej subskrypcji, zawierają wartość `DestinationSubscriptionId` parametru.</span><span class="sxs-lookup"><span data-stu-id="b136c-305">To move to a new subscription, include a value for the `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="b136c-306">Zostanie wyświetlona prośba o potwierdzenie, że chcesz przenieść określonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="b136c-306">You are asked to confirm that you want to move the specified resources.</span></span>

```powershell
Confirm
Are you sure you want to move these resources to the resource group
'/subscriptions/{guid}/resourceGroups/newRG' the resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="b136c-307">Użyj interfejsu wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b136c-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="b136c-308">Aby przenieść istniejące zasoby do innej grupy zasobów lub subskrypcji, należy użyć `az resource move` polecenia.</span><span class="sxs-lookup"><span data-stu-id="b136c-308">To move existing resources to another resource group or subscription, use the `az resource move` command.</span></span> <span data-ttu-id="b136c-309">Podaj identyfikatorów zasobów przenoszenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="b136c-309">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="b136c-310">Można pobrać identyfikatorów zasobów za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b136c-310">You can get resource IDs with the following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="b136c-311">Poniższy przykład przedstawia sposób przenoszenia konta magazynu do nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="b136c-311">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="b136c-312">W `--ids` parametru, podaj rozdzieloną spacjami listę identyfikatorów przenoszenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="b136c-312">In the `--ids` parameter, provide a space-separated list of the resource IDs to move.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="b136c-313">Aby przejść do nowej subskrypcji, należy podać `--destination-subscription-id` parametru.</span><span class="sxs-lookup"><span data-stu-id="b136c-313">To move to a new subscription, provide the `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="b136c-314">Użyj interfejsu wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="b136c-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="b136c-315">Aby przenieść istniejące zasoby do innej grupy zasobów lub subskrypcji, należy użyć `azure resource move` polecenia.</span><span class="sxs-lookup"><span data-stu-id="b136c-315">To move existing resources to another resource group or subscription, use the `azure resource move` command.</span></span> <span data-ttu-id="b136c-316">Podaj identyfikatorów zasobów przenoszenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="b136c-316">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="b136c-317">Można pobrać identyfikatorów zasobów za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b136c-317">You can get resource IDs with the following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="b136c-318">Polecenie to zwraca następujący format:</span><span class="sxs-lookup"><span data-stu-id="b136c-318">Which returns the following format:</span></span>

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

<span data-ttu-id="b136c-319">Poniższy przykład przedstawia sposób przenoszenia konta magazynu do nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="b136c-319">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="b136c-320">W `-i` parametru zawierają rozdzielaną przecinkami listę identyfikatorów przenoszenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="b136c-320">In the `-i` parameter, provide a comma-separated list of the resource IDs to move.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="b136c-321">Zostanie wyświetlona prośba o potwierdzenie, że chcesz przenieść określonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="b136c-321">You are asked to confirm that you want to move the specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="b136c-322">Używanie interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="b136c-322">Use REST API</span></span>
<span data-ttu-id="b136c-323">Aby przenieść istniejące zasoby do innej grupy zasobów lub subskrypcji, uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="b136c-323">To move existing resources to another resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="b136c-324">W treści żądania Określ docelowa grupa zasobów i zasobów, aby przenieść.</span><span class="sxs-lookup"><span data-stu-id="b136c-324">In the request body, you specify the target resource group and the resources to move.</span></span> <span data-ttu-id="b136c-325">Aby uzyskać więcej informacji na temat operacji REST przenoszenia zobacz [przenoszenia zasobów](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="b136c-325">For more information about the move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b136c-326">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b136c-326">Next steps</span></span>
* <span data-ttu-id="b136c-327">Aby dowiedzieć się więcej na temat poleceń cmdlet programu PowerShell do zarządzania subskrypcją, zobacz [przy użyciu programu Azure PowerShell z usługą Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b136c-327">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="b136c-328">Informacje na temat polecenia wiersza polecenia platformy Azure do zarządzania subskrypcją, zobacz [przy użyciu wiersza polecenia platformy Azure z usługą Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b136c-328">To learn about Azure CLI commands for managing your subscription, see [Using the Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="b136c-329">Aby dowiedzieć się więcej o funkcjach portalu do zarządzania subskrypcją, zobacz [przy użyciu portalu Azure do zarządzania zasobami](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b136c-329">To learn about portal features for managing your subscription, see [Using the Azure portal to manage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="b136c-330">Informacje na temat stosowania logiczna organizacji do zasobów, zobacz [przy użyciu tagów do organizowania zasobów](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="b136c-330">To learn about applying a logical organization to your resources, see [Using tags to organize your resources](resource-group-using-tags.md).</span></span>
