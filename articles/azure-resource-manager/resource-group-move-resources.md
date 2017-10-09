---
title: "aaaMove zasobów Azure toonew subskrypcji lub grupy zasobów | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Resource Manager toomove zasobów tooa nową grupę zasobów lub subskrypcji."
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
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a><span data-ttu-id="f63d8-103">Przenieś grupę zasobów toonew zasobów lub subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f63d8-103">Move resources toonew resource group or subscription</span></span>
<span data-ttu-id="f63d8-104">W tym temacie pokazano, jak tooeither zasobów toomove nową subskrypcję lub nowy zasób grupy w hello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f63d8-104">This topic shows you how toomove resources tooeither a new subscription or a new resource group in hello same subscription.</span></span> <span data-ttu-id="f63d8-105">Można użyć portalu hello, programu PowerShell, interfejsu wiersza polecenia Azure lub hello zasobów toomove interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="f63d8-105">You can use hello portal, PowerShell, Azure CLI, or hello REST API toomove resource.</span></span> <span data-ttu-id="f63d8-106">Witaj operacji przenoszenia w tym temacie są dostępne tooyou bez żadnych pomoc techniczną platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f63d8-106">hello move operations in this topic are available tooyou without any assistance from Azure support.</span></span>

<span data-ttu-id="f63d8-107">Podczas przenoszenia zasobów, zarówno hello źródłowej grupy, jak i grupy docelowej hello są zablokowane podczas operacji hello.</span><span class="sxs-lookup"><span data-stu-id="f63d8-107">When moving resources, both hello source group and hello target group are locked during hello operation.</span></span> <span data-ttu-id="f63d8-108">Zapisu i usuwania działań są zablokowane na temat grup zasobów hello dopiero po zakończeniu przenoszenia hello.</span><span class="sxs-lookup"><span data-stu-id="f63d8-108">Write and delete operations are blocked on hello resource groups until hello move completes.</span></span> <span data-ttu-id="f63d8-109">Ta blokada oznacza, że nie można dodawać, aktualizować lub usuwać zasobów w grupach zasobów hello, ale nie oznacza to, że zasoby hello są zablokowane.</span><span class="sxs-lookup"><span data-stu-id="f63d8-109">This lock means you cannot add, update, or delete resources in hello resource groups, but it does not mean hello resources are frozen.</span></span> <span data-ttu-id="f63d8-110">Na przykład jeśli przenosisz programu SQL Server i jego nowej grupy zasobów bazy danych tooa aplikacji korzystającej z bazy danych hello napotyka bez przestojów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-110">For example, if you move a SQL Server and its database tooa new resource group, an application that uses hello database experiences no downtime.</span></span> <span data-ttu-id="f63d8-111">On nadal odczytu i zapisu toohello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f63d8-111">It can still read and write toohello database.</span></span>

<span data-ttu-id="f63d8-112">Nie można zmienić lokalizacji hello hello zasobu.</span><span class="sxs-lookup"><span data-stu-id="f63d8-112">You cannot change hello location of hello resource.</span></span> <span data-ttu-id="f63d8-113">Przeniesienie zasobu tylko przenosi je tooa nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-113">Moving a resource only moves it tooa new resource group.</span></span> <span data-ttu-id="f63d8-114">Witaj nowej grupy zasobów może mieć inną lokalizację, ale nie zmienia lokalizację hello hello zasobu.</span><span class="sxs-lookup"><span data-stu-id="f63d8-114">hello new resource group may have a different location, but that does not change hello location of hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="f63d8-115">W tym artykule opisano sposób wysyłania ofert konta toomove zasoby w istniejącą Azure.</span><span class="sxs-lookup"><span data-stu-id="f63d8-115">This article describes how toomove resources within an existing Azure account offering.</span></span> <span data-ttu-id="f63d8-116">Jeśli konieczne toochange konta platformy Azure oferty (takich jak uaktualnianie z płatności obejmujące płatności toopre), pozostawiając toowork z istniejących zasobów, zobacz [przełącznika ofertę tooanother subskrypcji platformy Azure](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="f63d8-116">If you actually want toochange your Azure account offering (such as upgrading from pay-as-you-go toopre-pay) while continuing toowork with your existing resources, see [Switch your Azure subscription tooanother offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="f63d8-117">Lista kontrolna przed przeniesieniem zasobów</span><span class="sxs-lookup"><span data-stu-id="f63d8-117">Checklist before moving resources</span></span>
<span data-ttu-id="f63d8-118">Istnieją pewne ważne czynności tooperform przed przeniesieniem zasobu.</span><span class="sxs-lookup"><span data-stu-id="f63d8-118">There are some important steps tooperform before moving a resource.</span></span> <span data-ttu-id="f63d8-119">Dzięki sprawdzeniu tych warunków można uniknąć błędów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="f63d8-120">Witaj subskrypcji źródłowych i docelowych musi istnieć w ramach hello sam [dzierżawy usługi Azure Active Directory](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="f63d8-120">hello source and destination subscriptions must exist within hello same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="f63d8-121">obie subskrypcje mają hello sam toocheck Identyfikatorem dzierżawy, użyj programu Azure PowerShell lub interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f63d8-121">toocheck that both subscriptions have hello same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="f63d8-122">Dla programu Azure PowerShell użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="f63d8-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="f63d8-123">Azure CLI 2.0 należy użyć:</span><span class="sxs-lookup"><span data-stu-id="f63d8-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="f63d8-124">Jeśli hello dzierżawy identyfikatory hello źródłowego i docelowego subskrypcje są hello takie same, można spróbować katalogu hello toochange hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f63d8-124">If hello tenant IDs for hello source and destination subscriptions are not hello same, you can attempt toochange hello directory for hello subscription.</span></span> <span data-ttu-id="f63d8-125">Jednak ta opcja jest tylko dostępne tooService administratorów, którzy są podpisane za pomocą konta Microsoft (nie konta organizacyjnego).</span><span class="sxs-lookup"><span data-stu-id="f63d8-125">However, this option is only available tooService Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="f63d8-126">Zmienianie katalogu hello, logowanie toohello tooattempt [klasyczny portal](https://manage.windowsazure.com/)i wybierz **ustawienia**i wybierz subskrypcję hello.</span><span class="sxs-lookup"><span data-stu-id="f63d8-126">tooattempt changing hello directory, log in toohello [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select hello subscription.</span></span> <span data-ttu-id="f63d8-127">Jeśli hello **Edytuj katalog** ikona jest dostępna, zaznacz go toochange hello skojarzone usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f63d8-127">If hello **Edit Directory** icon is available, select it toochange hello associated Azure Active Directory.</span></span>

  ![Edytowanie katalogu](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="f63d8-129">Tę ikonę nie jest dostępny, musisz skontaktować się obsługa toomove hello zasobów tooa nowej dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="f63d8-129">If that icon is not available, you must contact support toomove hello resources tooa new tenant.</span></span>

2. <span data-ttu-id="f63d8-130">Usługa Hello należy włączyć hello możliwości toomove zasobów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-130">hello service must enable hello ability toomove resources.</span></span> <span data-ttu-id="f63d8-131">Ten temat zawiera listę usług, które umożliwiają przenoszenie zasobów i usług, które nie należy włączać przenoszenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="f63d8-132">Witaj, subskrypcji docelowej musi być zarejestrowana do dostawcy zasobów hello zasobu hello przenoszony.</span><span class="sxs-lookup"><span data-stu-id="f63d8-132">hello destination subscription must be registered for hello resource provider of hello resource being moved.</span></span> <span data-ttu-id="f63d8-133">Jeśli nie, zostanie wyświetlony komunikat o błędzie informujący, że hello **subskrypcja nie jest zarejestrowana dla typu zasobu**.</span><span class="sxs-lookup"><span data-stu-id="f63d8-133">If not, you receive an error stating that hello **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="f63d8-134">Ten problem może wystąpić, podczas przenoszenia zasobów tooa nową subskrypcję, ale tej subskrypcji nigdy nie został użyty z tym typem zasobu.</span><span class="sxs-lookup"><span data-stu-id="f63d8-134">You might encounter this problem when moving a resource tooa new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="f63d8-135">toolearn toocheck hello stanu rejestracji i zarejestrować dostawców zasobów, zobacz [dostawców zasobów i typów](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="f63d8-135">toolearn how toocheck hello registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-toocall-support"></a><span data-ttu-id="f63d8-136">Jeżeli obsługują toocall</span><span class="sxs-lookup"><span data-stu-id="f63d8-136">When toocall support</span></span>
<span data-ttu-id="f63d8-137">Można przenieść najwięcej zasobów za pomocą operacji samoobsługi hello wyświetlane w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="f63d8-137">You can move most resources through hello self-service operations shown in this topic.</span></span> <span data-ttu-id="f63d8-138">Użyj hello samoobsługi operacje:</span><span class="sxs-lookup"><span data-stu-id="f63d8-138">Use hello self-service operations to:</span></span>

* <span data-ttu-id="f63d8-139">Przenieś zasoby usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f63d8-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="f63d8-140">Przenoszenie zasobów klasycznych zgodnie z toohello [ograniczenia wdrażania klasycznego](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="f63d8-140">Move classic resources according toohello [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="f63d8-141">Jeśli trzeba z działem pomocy technicznej:</span><span class="sxs-lookup"><span data-stu-id="f63d8-141">Call support when you need to:</span></span>

* <span data-ttu-id="f63d8-142">Przenoszenie zasobów tooa nowe konto platformy Azure (i dzierżawy usługi Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f63d8-142">Move your resources tooa new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="f63d8-143">Przenoszenie zasobów klasycznych, ale występują problemy z ograniczeniami hello.</span><span class="sxs-lookup"><span data-stu-id="f63d8-143">Move classic resources but are having trouble with hello limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="f63d8-144">Usługi, które pozwalają przenoszenia</span><span class="sxs-lookup"><span data-stu-id="f63d8-144">Services that enable move</span></span>
<span data-ttu-id="f63d8-145">Obecnie dostępne są następujące usługi hello, umożliwiając przenoszenie tooboth nową grupę zasobów i subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="f63d8-145">For now, hello services that enable moving tooboth a new resource group and subscription are:</span></span>

* <span data-ttu-id="f63d8-146">API Management</span><span class="sxs-lookup"><span data-stu-id="f63d8-146">API Management</span></span>
* <span data-ttu-id="f63d8-147">Usługi aplikacji — aplikacje (aplikacje sieci web) — zobacz [ograniczenia usługi aplikacji](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="f63d8-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="f63d8-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="f63d8-148">Application Insights</span></span>
* <span data-ttu-id="f63d8-149">Automatyzacja</span><span class="sxs-lookup"><span data-stu-id="f63d8-149">Automation</span></span>
* <span data-ttu-id="f63d8-150">Batch</span><span class="sxs-lookup"><span data-stu-id="f63d8-150">Batch</span></span>
* <span data-ttu-id="f63d8-151">Mapy Bing</span><span class="sxs-lookup"><span data-stu-id="f63d8-151">Bing Maps</span></span>
* <span data-ttu-id="f63d8-152">CDN</span><span class="sxs-lookup"><span data-stu-id="f63d8-152">CDN</span></span>
* <span data-ttu-id="f63d8-153">Usługi w chmurze — zobacz [Classic deployment ograniczenia](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="f63d8-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="f63d8-154">Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="f63d8-154">Cognitive Services</span></span>
* <span data-ttu-id="f63d8-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="f63d8-155">Content Moderator</span></span>
* <span data-ttu-id="f63d8-156">Data Catalog</span><span class="sxs-lookup"><span data-stu-id="f63d8-156">Data Catalog</span></span>
* <span data-ttu-id="f63d8-157">Fabryka danych</span><span class="sxs-lookup"><span data-stu-id="f63d8-157">Data Factory</span></span>
* <span data-ttu-id="f63d8-158">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f63d8-158">Data Lake Analytics</span></span>
* <span data-ttu-id="f63d8-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f63d8-159">Data Lake Store</span></span>
* <span data-ttu-id="f63d8-160">DNS</span><span class="sxs-lookup"><span data-stu-id="f63d8-160">DNS</span></span>
* <span data-ttu-id="f63d8-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f63d8-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="f63d8-162">Usługa Event Hubs</span><span class="sxs-lookup"><span data-stu-id="f63d8-162">Event Hubs</span></span>
* <span data-ttu-id="f63d8-163">Klastry HDInsight — zobacz [ograniczenia usługi HDInsight](#hdinsight-limitations)</span><span class="sxs-lookup"><span data-stu-id="f63d8-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="f63d8-164">Centra IoT</span><span class="sxs-lookup"><span data-stu-id="f63d8-164">IoT Hubs</span></span>
* <span data-ttu-id="f63d8-165">Usługa Key Vault</span><span class="sxs-lookup"><span data-stu-id="f63d8-165">Key Vault</span></span>
* <span data-ttu-id="f63d8-166">Moduły równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="f63d8-166">Load Balancers</span></span>
* <span data-ttu-id="f63d8-167">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="f63d8-167">Logic Apps</span></span>
* <span data-ttu-id="f63d8-168">Usługa Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f63d8-168">Machine Learning</span></span>
* <span data-ttu-id="f63d8-169">Media Services</span><span class="sxs-lookup"><span data-stu-id="f63d8-169">Media Services</span></span>
* <span data-ttu-id="f63d8-170">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="f63d8-170">Mobile Engagement</span></span>
* <span data-ttu-id="f63d8-171">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="f63d8-171">Notification Hubs</span></span>
* <span data-ttu-id="f63d8-172">Operational Insights</span><span class="sxs-lookup"><span data-stu-id="f63d8-172">Operational Insights</span></span>
* <span data-ttu-id="f63d8-173">Operations Management</span><span class="sxs-lookup"><span data-stu-id="f63d8-173">Operations Management</span></span>
* <span data-ttu-id="f63d8-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="f63d8-174">Power BI</span></span>
* <span data-ttu-id="f63d8-175">Pamięć podręczna Redis</span><span class="sxs-lookup"><span data-stu-id="f63d8-175">Redis Cache</span></span>
* <span data-ttu-id="f63d8-176">Scheduler</span><span class="sxs-lookup"><span data-stu-id="f63d8-176">Scheduler</span></span>
* <span data-ttu-id="f63d8-177">Wyszukiwanie</span><span class="sxs-lookup"><span data-stu-id="f63d8-177">Search</span></span>
* <span data-ttu-id="f63d8-178">Zarządzanie serwerem</span><span class="sxs-lookup"><span data-stu-id="f63d8-178">Server Management</span></span>
* <span data-ttu-id="f63d8-179">Service Bus</span><span class="sxs-lookup"><span data-stu-id="f63d8-179">Service Bus</span></span>
* <span data-ttu-id="f63d8-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f63d8-180">Service Fabric</span></span>
* <span data-ttu-id="f63d8-181">Magazyn</span><span class="sxs-lookup"><span data-stu-id="f63d8-181">Storage</span></span>
* <span data-ttu-id="f63d8-182">Magazyn (klasyczne) — zobacz [Classic deployment ograniczenia](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="f63d8-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="f63d8-183">Stream Analytics — usługi analiza strumienia zadania nie można przenieść uruchomionej w stanie.</span><span class="sxs-lookup"><span data-stu-id="f63d8-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="f63d8-184">Serwer bazy danych SQL — Witaj bazy danych i serwera musi znajdować się w hello tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-184">SQL Database server - hello database and server must reside in hello same resource group.</span></span> <span data-ttu-id="f63d8-185">W przypadku przenoszenia programu SQL server, również są przenoszone jej baz danych.</span><span class="sxs-lookup"><span data-stu-id="f63d8-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="f63d8-186">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="f63d8-186">Traffic Manager</span></span>
* <span data-ttu-id="f63d8-187">Maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="f63d8-187">Virtual Machines</span></span>
* <span data-ttu-id="f63d8-188">Maszyny wirtualne z certyfikatem przechowywane w magazynie kluczy - toonew przeniesienie zasobów grupy w tej samej subskrypcji jest włączona, ale przenoszenia między subskrypcji nie jest włączona.</span><span class="sxs-lookup"><span data-stu-id="f63d8-188">Virtual Machines with certificate stored in Key Vault - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="f63d8-189">Maszyny wirtualne (klasyczne) — zobacz [Classic deployment ograniczenia](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="f63d8-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="f63d8-190">Zestawy skali maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="f63d8-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="f63d8-191">Sieci wirtualne — obecnie, peered sieci wirtualnej nie można przenieść do momentu równorzędna sieci wirtualnej zostały wyłączone.</span><span class="sxs-lookup"><span data-stu-id="f63d8-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="f63d8-192">Po wyłączeniu hello sieci wirtualnej mogą zostać przeniesione pomyślnie i hello sieci wirtualnej komunikacji równorzędnej można włączyć.</span><span class="sxs-lookup"><span data-stu-id="f63d8-192">Once disabled, hello Virtual Network can be moved successfully and hello VNet peering can be enabled.</span></span> <span data-ttu-id="f63d8-193">Ponadto sieci wirtualnej nie może być przeniesiony tooa innej subskrypcji Jeśli hello sieć wirtualna zawiera żadnej podsieci z zasobów łącza nawigacji.</span><span class="sxs-lookup"><span data-stu-id="f63d8-193">In addition, a Virtual Network cannot be moved tooa different subscription if hello Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="f63d8-194">Na przykład podsieć sieci wirtualnej ma łącza nawigacji zasobu, gdy zasób redis Microsoft.Cache zostaje wdrożona do tej podsieci.</span><span class="sxs-lookup"><span data-stu-id="f63d8-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="f63d8-195">VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="f63d8-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="f63d8-196">Usługi, które nie należy włączać przenoszenia</span><span class="sxs-lookup"><span data-stu-id="f63d8-196">Services that do not enable move</span></span>
<span data-ttu-id="f63d8-197">Witaj usług, które aktualnie nie należy włączać przenoszenie zasobu to:</span><span class="sxs-lookup"><span data-stu-id="f63d8-197">hello services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="f63d8-198">Usługi domenowe AD</span><span class="sxs-lookup"><span data-stu-id="f63d8-198">AD Domain Services</span></span>
* <span data-ttu-id="f63d8-199">Usługa kondycji hybrydowe AD</span><span class="sxs-lookup"><span data-stu-id="f63d8-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="f63d8-200">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="f63d8-200">Application Gateway</span></span>
* <span data-ttu-id="f63d8-201">Zestawy dostępności z maszynami wirtualnymi z dyskami zarządzane</span><span class="sxs-lookup"><span data-stu-id="f63d8-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="f63d8-202">BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="f63d8-202">BizTalk Services</span></span>
* <span data-ttu-id="f63d8-203">Container Service</span><span class="sxs-lookup"><span data-stu-id="f63d8-203">Container Service</span></span>
* <span data-ttu-id="f63d8-204">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f63d8-204">Express Route</span></span>
* <span data-ttu-id="f63d8-205">DevTest Labs — przeniesienie grupy zasobów toonew w tej samej subskrypcji jest włączona, ale między przeniesienia subskrypcji nie jest włączona.</span><span class="sxs-lookup"><span data-stu-id="f63d8-205">DevTest Labs - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="f63d8-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="f63d8-206">Dynamics LCS</span></span>
* <span data-ttu-id="f63d8-207">Obrazy utworzone na podstawie zarządzanych dysków</span><span class="sxs-lookup"><span data-stu-id="f63d8-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="f63d8-208">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="f63d8-208">Managed Disks</span></span>
* <span data-ttu-id="f63d8-209">Zarządzane aplikacje</span><span class="sxs-lookup"><span data-stu-id="f63d8-209">Managed Applications</span></span>
* <span data-ttu-id="f63d8-210">Magazyn usług odzyskiwania — również nie przenoszenia hello obliczeniowych, sieci i magazynu zasoby skojarzone z tekst hello usług odzyskiwania magazynu, zobacz [ograniczenia usług odzyskiwania](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="f63d8-210">Recovery Services vault - also do not move hello Compute, Network, and Storage resources associated with hello Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="f63d8-211">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="f63d8-211">Security</span></span>
* <span data-ttu-id="f63d8-212">Migawek utworzonych z dysków zarządzanych</span><span class="sxs-lookup"><span data-stu-id="f63d8-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="f63d8-213">Menedżer urządzeń StorSimple</span><span class="sxs-lookup"><span data-stu-id="f63d8-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="f63d8-214">Maszyny wirtualne z dyskami zarządzanych</span><span class="sxs-lookup"><span data-stu-id="f63d8-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="f63d8-215">Sieci wirtualne (klasyczne) — zobacz [Classic deployment ograniczenia](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="f63d8-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="f63d8-216">Nie można przenieść maszyny wirtualne utworzone na podstawie zasobów Marketplace - różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f63d8-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="f63d8-217">Zasób musi toobe anulowana w bieżącej subskrypcji hello i wdrożyć ponownie w nowej subskrypcji hello</span><span class="sxs-lookup"><span data-stu-id="f63d8-217">Resource needs toobe deprovisioned in hello current subscription and deployed again in hello new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="f63d8-218">Ograniczenia usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="f63d8-218">App Service limitations</span></span>
<span data-ttu-id="f63d8-219">Podczas pracy z aplikacjami usługi App Service, nie można przenieść plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f63d8-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="f63d8-220">toomove usługi aplikacji — aplikacje, są następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="f63d8-220">toomove App Service apps, your options are:</span></span>

* <span data-ttu-id="f63d8-221">Przenieś hello planu usługi aplikacji i innych zasobów usługi aplikacji w tym zasobów grupy tooa nową grupę zasobów, które jeszcze nie ma zasobów usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f63d8-221">Move hello App Service plan and all other App Service resources in that resource group tooa new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="f63d8-222">To wymaganie, że oznacza, że należy przenieść nawet hello zasobów usługi aplikacji — które nie są skojarzone z hello planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f63d8-222">This requirement means you must move even hello App Service resources that are not associated with hello App Service plan.</span></span>
* <span data-ttu-id="f63d8-223">Przenieś grupę zasobów różnych tooa aplikacji hello, ale zachować wszystkie plany usługi App Service w grupie zasobów z oryginalnego hello.</span><span class="sxs-lookup"><span data-stu-id="f63d8-223">Move hello apps tooa different resource group, but keep all App Service plans in hello original resource group.</span></span>

<span data-ttu-id="f63d8-224">Witaj plan nie jest konieczne tooreside w usługi aplikacji hello tej samej grupie zasobów co aplikacja hello dla toofunction aplikacji hello poprawnie.</span><span class="sxs-lookup"><span data-stu-id="f63d8-224">hello App Service plan does not need tooreside in hello same resource group as hello app for hello app toofunction correctly.</span></span>

<span data-ttu-id="f63d8-225">Na przykład, jeśli zawiera grupie zasobów:</span><span class="sxs-lookup"><span data-stu-id="f63d8-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="f63d8-226">**sieci Web a** skojarzony z **planu a**</span><span class="sxs-lookup"><span data-stu-id="f63d8-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="f63d8-227">**sieci Web-b** skojarzony z **plan-b**</span><span class="sxs-lookup"><span data-stu-id="f63d8-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="f63d8-228">Dostępne opcje to:</span><span class="sxs-lookup"><span data-stu-id="f63d8-228">Your options are:</span></span>

* <span data-ttu-id="f63d8-229">Przenieś **sieci web a**, **planu a**, **sieci web-b**, i **plan-b**</span><span class="sxs-lookup"><span data-stu-id="f63d8-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="f63d8-230">Przenieś **sieci web a** i **b sieci web**</span><span class="sxs-lookup"><span data-stu-id="f63d8-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="f63d8-231">Przenieś **w sieci web**</span><span class="sxs-lookup"><span data-stu-id="f63d8-231">Move **web-a**</span></span>
* <span data-ttu-id="f63d8-232">Przenieś **b sieci web**</span><span class="sxs-lookup"><span data-stu-id="f63d8-232">Move **web-b**</span></span>

<span data-ttu-id="f63d8-233">Wszystkie inne kombinacje obejmują, pozostawiając w niej typ zasobu, który nie może pozostać podczas przenoszenia planu usługi App Service (dowolny typ zasobu usługi App Service).</span><span class="sxs-lookup"><span data-stu-id="f63d8-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="f63d8-234">Jeśli aplikacja sieci web znajduje się w innej grupie zasobów niż swój plan usługi aplikacji, ale ma toomove zarówno tooa nową grupę zasobów, należy wykonać przenoszenia hello w dwóch krokach.</span><span class="sxs-lookup"><span data-stu-id="f63d8-234">If your web app resides in a different resource group than its App Service plan but you want toomove both tooa new resource group, you must perform hello move in two steps.</span></span> <span data-ttu-id="f63d8-235">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="f63d8-235">For example:</span></span>

* <span data-ttu-id="f63d8-236">**sieci Web a** znajduje się w **grupy sieci web**</span><span class="sxs-lookup"><span data-stu-id="f63d8-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="f63d8-237">**Plan a** znajduje się w **planu grupy**</span><span class="sxs-lookup"><span data-stu-id="f63d8-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="f63d8-238">Ma **sieci web a** i **planu a** tooreside w **połączeniu grupy**</span><span class="sxs-lookup"><span data-stu-id="f63d8-238">You want **web-a** and **plan-a** tooreside in **combined-group**</span></span>

<span data-ttu-id="f63d8-239">to przeniesienie, wykonaj dwa operacji przenoszenia oddzielne w powitania po sekwencji tooaccomplish:</span><span class="sxs-lookup"><span data-stu-id="f63d8-239">tooaccomplish this move, perform two separate move operations in hello following sequence:</span></span>

1. <span data-ttu-id="f63d8-240">Przenieś hello **sieci web a** zbyt**planu grupy**</span><span class="sxs-lookup"><span data-stu-id="f63d8-240">Move hello **web-a** too**plan-group**</span></span>
2. <span data-ttu-id="f63d8-241">Przenieś **sieci web a** i **planu a** za**łączyć grupy**.</span><span class="sxs-lookup"><span data-stu-id="f63d8-241">Move **web-a** and **plan-a** too**combined-group**.</span></span>

<span data-ttu-id="f63d8-242">Można przenieść certyfikatu usługi aplikacji tooa nową grupę zasobów lub subskrypcji, bez żadnych problemów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-242">You can move an App Service Certificate tooa new resource group or subscription without any issues.</span></span> <span data-ttu-id="f63d8-243">Jednak jeśli aplikacja sieci web zawiera certyfikat SSL zakupionych zewnętrznie, a następnie przekazać toohello aplikacji, należy usunąć hello certyfikatu przed aplikacji hello ruchu w sieci web.</span><span class="sxs-lookup"><span data-stu-id="f63d8-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded toohello app, you must delete hello certificate before moving hello web app.</span></span> <span data-ttu-id="f63d8-244">Na przykład można wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f63d8-244">For example, you can perform hello following steps:</span></span>

1. <span data-ttu-id="f63d8-245">Usuń certyfikat hello przekazany z hello aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="f63d8-245">Delete hello uploaded certificate from hello web app</span></span>
2. <span data-ttu-id="f63d8-246">Przenieś hello aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="f63d8-246">Move hello web app</span></span>
3. <span data-ttu-id="f63d8-247">Przekaż aplikację sieci web toohello certyfikatu hello</span><span class="sxs-lookup"><span data-stu-id="f63d8-247">Upload hello certificate toohello web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="f63d8-248">Ograniczenia usługi odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="f63d8-248">Recovery Services limitations</span></span>
<span data-ttu-id="f63d8-249">Przenieś nie jest włączona dla magazynu, sieci, lub zasoby obliczeniowe używane tooset zapasowej odzyskiwania po awarii z usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f63d8-249">Move is not enabled for Storage, Network, or Compute resources used tooset up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="f63d8-250">Na przykład załóżmy, że po skonfigurowaniu replikacji konta magazynu tooa maszyny lokalnej (Storage1) i ma hello chronione maszyny toocome się po tooAzure pracy awaryjnej jako maszynę wirtualną (VM1) dołączony tooa sieci wirtualnej (Network1).</span><span class="sxs-lookup"><span data-stu-id="f63d8-250">For example, suppose you have set up replication of your on-premises machines tooa storage account (Storage1) and want hello protected machine toocome up after failover tooAzure as a virtual machine (VM1) attached tooa virtual network (Network1).</span></span> <span data-ttu-id="f63d8-251">Nie można przenieść żadnego z tych zasobów Azure - Storage1, VM1, oraz Network1 — między zasobów grup w hello takie same subskrypcji lub różnych subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f63d8-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within hello same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="f63d8-252">Ograniczenia usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="f63d8-252">HDInsight limitations</span></span>

<span data-ttu-id="f63d8-253">Można przenieść klastrów HDInsight tooa nowej subskrypcji lub grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-253">You can move HDInsight clusters tooa new subscription or resource group.</span></span> <span data-ttu-id="f63d8-254">Jednak nie można przenieść między subskrypcjami hello sieci klastra usługi HDInsight toohello połączonych zasobów (na przykład hello sieci wirtualnej karty Sieciowej lub usługi równoważenia obciążenia).</span><span class="sxs-lookup"><span data-stu-id="f63d8-254">However, you cannot move across subscriptions hello networking resources linked toohello HDInsight cluster (such as hello virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="f63d8-255">Ponadto nie można przenieść tooa nową grupę zasobów kartę Sieciową, która jest dołączona tooa maszyny wirtualnej klastra hello.</span><span class="sxs-lookup"><span data-stu-id="f63d8-255">In addition, you cannot move tooa new resource group a NIC that is attached tooa virtual machine for hello cluster.</span></span>

<span data-ttu-id="f63d8-256">Podczas przenoszenia HDInsight klastra tooa nową subskrypcję, należy najpierw przenieść innych zasobów (takich jak hello konta magazynu).</span><span class="sxs-lookup"><span data-stu-id="f63d8-256">When moving an HDInsight cluster tooa new subscription, first move other resources (like hello storage account).</span></span> <span data-ttu-id="f63d8-257">Następnie przenieś klastra usługi HDInsight hello samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="f63d8-257">Then, move hello HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="f63d8-258">Wdrożenie klasyczne ograniczenia</span><span class="sxs-lookup"><span data-stu-id="f63d8-258">Classic deployment limitations</span></span>
<span data-ttu-id="f63d8-259">Witaj Opcje przenoszenia zasobów wdrażać przy użyciu modelu klasycznego hello różnią się zależności od tego, czy przenosisz hello zasobów w ramach subskrypcji lub tooa nową subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="f63d8-259">hello options for moving resources deployed through hello classic model differ based on whether you are moving hello resources within a subscription or tooa new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="f63d8-260">Tej samej subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f63d8-260">Same subscription</span></span>
<span data-ttu-id="f63d8-261">Podczas przenoszenia zasobów z jednej grupy tooanother zasobów grupy zasobów w ramach hello zastosowania tej samej subskrypcji, hello następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="f63d8-261">When moving resources from one resource group tooanother resource group within hello same subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="f63d8-262">Nie można przenieść sieci wirtualnych (klasyczny).</span><span class="sxs-lookup"><span data-stu-id="f63d8-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="f63d8-263">Maszyny wirtualne (klasyczne) muszą zostać przeniesione z usługą w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="f63d8-263">Virtual machines (classic) must be moved with hello cloud service.</span></span>
* <span data-ttu-id="f63d8-264">Usługi w chmurze tylko przeniesienia podczas przenoszenia hello obejmuje wszystkie maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="f63d8-264">Cloud service can only be moved when hello move includes all its virtual machines.</span></span>
* <span data-ttu-id="f63d8-265">Usługi w chmurze tylko jeden mogą zostać przeniesione w czasie.</span><span class="sxs-lookup"><span data-stu-id="f63d8-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="f63d8-266">Jednocześnie można przenosić tylko jedno konto magazynu (klasyczne).</span><span class="sxs-lookup"><span data-stu-id="f63d8-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="f63d8-267">Konto magazynu (klasyczne) nie może zostać przeniesiony w hello tej samej operacji z maszyny wirtualnej lub usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f63d8-267">Storage account (classic) cannot be moved in hello same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="f63d8-268">toomove zasoby klasyczne tooa nowej grupy zasobów w hello tej samej subskrypcji, użyj operacji przenoszenia standardowe hello za pośrednictwem hello [portal](#use-portal), [programu Azure PowerShell](#use-powershell), [interfejsu wiersza polecenia Azure](#use-azure-cli), lub [interfejsu API REST](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="f63d8-268">toomove classic resources tooa new resource group within hello same subscription, use hello standard move operations through hello [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="f63d8-269">Możesz użyć hello tych samych operacji, ponieważ używane do przenoszenia zasoby usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f63d8-269">You use hello same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="f63d8-270">Nowa subskrypcja</span><span class="sxs-lookup"><span data-stu-id="f63d8-270">New subscription</span></span>
<span data-ttu-id="f63d8-271">Podczas przenoszenia zasobów tooa nową subskrypcję, zastosuj hello następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="f63d8-271">When moving resources tooa new subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="f63d8-272">Wszystkie zasoby klasyczne w subskrypcji hello muszą zostać przeniesione w hello tej samej operacji.</span><span class="sxs-lookup"><span data-stu-id="f63d8-272">All classic resources in hello subscription must be moved in hello same operation.</span></span>
* <span data-ttu-id="f63d8-273">Witaj, subskrypcji docelowej nie może zawierać inne zasoby klasyczne.</span><span class="sxs-lookup"><span data-stu-id="f63d8-273">hello target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="f63d8-274">Przenieś Hello się żądać tylko wtedy za pomocą osobnych interfejsu API REST dla przenosi klasycznego.</span><span class="sxs-lookup"><span data-stu-id="f63d8-274">hello move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="f63d8-275">Witaj standardowe polecenia move Menedżera zasobów nie działają podczas przenoszenia zasobów klasycznych tooa nową subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="f63d8-275">hello standard Resource Manager move commands do not work when moving classic resources tooa new subscription.</span></span>

<span data-ttu-id="f63d8-276">toomove zasoby klasyczne tooa nowej subskrypcji, użyj operacji REST hello, które są tooclassic określonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-276">toomove classic resources tooa new subscription, use hello REST operations that are specific tooclassic resources.</span></span> <span data-ttu-id="f63d8-277">toouse REST, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="f63d8-277">toouse REST, perform hello following steps:</span></span>

1. <span data-ttu-id="f63d8-278">Wyboru, jeśli subskrypcja źródłowa hello mogą uczestniczyć w między subskrypcjami przenieść.</span><span class="sxs-lookup"><span data-stu-id="f63d8-278">Check if hello source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="f63d8-279">Użyj następującej operacji hello:</span><span class="sxs-lookup"><span data-stu-id="f63d8-279">Use hello following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="f63d8-280">W treści żądania hello obejmują:</span><span class="sxs-lookup"><span data-stu-id="f63d8-280">In hello request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="f63d8-281">Hello odpowiedzi dla operacji sprawdzania poprawności hello jest hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="f63d8-281">hello response for hello validation operation is in hello following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="f63d8-282">Wyboru subskrypcji docelowej hello mogą uczestniczyć w między subskrypcjami przenieść.</span><span class="sxs-lookup"><span data-stu-id="f63d8-282">Check if hello destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="f63d8-283">Użyj następującej operacji hello:</span><span class="sxs-lookup"><span data-stu-id="f63d8-283">Use hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="f63d8-284">W treści żądania hello obejmują:</span><span class="sxs-lookup"><span data-stu-id="f63d8-284">In hello request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="f63d8-285">odpowiedź Hello jest hello takiego samego formatu jak hello źródła subskrypcji weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="f63d8-285">hello response is in hello same format as hello source subscription validation.</span></span>
3. <span data-ttu-id="f63d8-286">Jeśli obie subskrypcje przeszedł sprawdzania poprawności, Przenieś wszystkie zasoby klasyczne z jedną subskrypcją tooanother subskrypcji z hello następującej operacji:</span><span class="sxs-lookup"><span data-stu-id="f63d8-286">If both subscriptions pass validation, move all classic resources from one subscription tooanother subscription with hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="f63d8-287">W treści żądania hello obejmują:</span><span class="sxs-lookup"><span data-stu-id="f63d8-287">In hello request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="f63d8-288">Operacja Hello może trwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="f63d8-288">hello operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="f63d8-289">Korzystanie z portalu</span><span class="sxs-lookup"><span data-stu-id="f63d8-289">Use portal</span></span>
<span data-ttu-id="f63d8-290">toomove zasobów, wybierz grupę zasobów hello zawierające te zasoby, a następnie wybierz hello **Przenieś** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f63d8-290">toomove resources, select hello resource group containing those resources, and then select hello **Move** button.</span></span>

![Przenoszenie zasobów](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="f63d8-292">Określ, czy przenosisz hello zasobów tooa nową grupę zasobów lub nową subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="f63d8-292">Select whether you are moving hello resources tooa new resource group or a new subscription.</span></span>

<span data-ttu-id="f63d8-293">Wybierz hello toomove zasobów i grupy zasobów hello docelowego.</span><span class="sxs-lookup"><span data-stu-id="f63d8-293">Select hello resources toomove and hello destination resource group.</span></span> <span data-ttu-id="f63d8-294">Potwierdzić wymagane skrypty tooupdate dla tych zasobów i wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="f63d8-294">Acknowledge that you need tooupdate scripts for these resources and select **OK**.</span></span> <span data-ttu-id="f63d8-295">Jeśli wybrano hello edycji subskrypcją ikonę w poprzednim kroku hello, musisz wybrać hello subskrypcji docelowej.</span><span class="sxs-lookup"><span data-stu-id="f63d8-295">If you selected hello edit subscription icon in hello previous step, you must also select hello destination subscription.</span></span>

![Wybierz miejsce docelowe](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="f63d8-297">W **powiadomienia**, zobacz ten hello Przenieś uruchomiona operacja.</span><span class="sxs-lookup"><span data-stu-id="f63d8-297">In **Notifications**, you see that hello move operation is running.</span></span>

![Pokaż stan przenoszenia](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="f63d8-299">Po ukończeniu, użytkownik jest powiadamiany o hello wynik.</span><span class="sxs-lookup"><span data-stu-id="f63d8-299">When it has completed, you are notified of hello result.</span></span>

![Pokaż Przenieś wyników](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="f63d8-301">Korzystanie z programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="f63d8-301">Use PowerShell</span></span>
<span data-ttu-id="f63d8-302">toomove istniejącej grupy zasobów tooanother zasobów lub subskrypcji, użyj hello `Move-AzureRmResource` polecenia.</span><span class="sxs-lookup"><span data-stu-id="f63d8-302">toomove existing resources tooanother resource group or subscription, use hello `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="f63d8-303">Witaj w pierwszym przykładzie pokazano sposób toomove jeden zasób tooa nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-303">hello first example shows how toomove one resource tooa new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="f63d8-304">Witaj w drugim przykładzie pokazano sposób toomove wiele zasobów tooa nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-304">hello second example shows how toomove multiple resources tooa new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="f63d8-305">Nowa subskrypcja tooa toomove zawierać wartość hello `DestinationSubscriptionId` parametru.</span><span class="sxs-lookup"><span data-stu-id="f63d8-305">toomove tooa new subscription, include a value for hello `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="f63d8-306">Pojawi się monit, które mają toomove hello tooconfirm określonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-306">You are asked tooconfirm that you want toomove hello specified resources.</span></span>

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="f63d8-307">Użyj interfejsu wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="f63d8-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="f63d8-308">toomove istniejącej grupy zasobów tooanother zasobów lub subskrypcji, użyj hello `az resource move` polecenia.</span><span class="sxs-lookup"><span data-stu-id="f63d8-308">toomove existing resources tooanother resource group or subscription, use hello `az resource move` command.</span></span> <span data-ttu-id="f63d8-309">Podaj zasobów hello identyfikatorów hello toomove zasobów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-309">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="f63d8-310">Identyfikatory zasobów można uzyskać z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f63d8-310">You can get resource IDs with hello following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="f63d8-311">Witaj poniższy przykład pokazuje, jak toomove magazynu konta tooa nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-311">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="f63d8-312">W hello `--ids` parametru, podaj rozdzieloną spacjami listę toomove identyfikatorów zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="f63d8-312">In hello `--ids` parameter, provide a space-separated list of hello resource IDs toomove.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="f63d8-313">toomove tooa nową subskrypcję, podaj hello `--destination-subscription-id` parametru.</span><span class="sxs-lookup"><span data-stu-id="f63d8-313">toomove tooa new subscription, provide hello `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="f63d8-314">Użyj interfejsu wiersza polecenia platformy Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="f63d8-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="f63d8-315">toomove istniejącej grupy zasobów tooanother zasobów lub subskrypcji, użyj hello `azure resource move` polecenia.</span><span class="sxs-lookup"><span data-stu-id="f63d8-315">toomove existing resources tooanother resource group or subscription, use hello `azure resource move` command.</span></span> <span data-ttu-id="f63d8-316">Podaj zasobów hello identyfikatorów hello toomove zasobów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-316">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="f63d8-317">Identyfikatory zasobów można uzyskać z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f63d8-317">You can get resource IDs with hello following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="f63d8-318">Polecenie to zwraca hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="f63d8-318">Which returns hello following format:</span></span>

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

<span data-ttu-id="f63d8-319">Witaj poniższy przykład pokazuje, jak toomove magazynu konta tooa nową grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-319">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="f63d8-320">W hello `-i` parametru zawierają toomove identyfikatorów zasobów hello listę rozdzielaną przecinkami.</span><span class="sxs-lookup"><span data-stu-id="f63d8-320">In hello `-i` parameter, provide a comma-separated list of hello resource IDs toomove.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="f63d8-321">Pojawi się monit, które mają toomove hello tooconfirm określony zasób.</span><span class="sxs-lookup"><span data-stu-id="f63d8-321">You are asked tooconfirm that you want toomove hello specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="f63d8-322">Używanie interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="f63d8-322">Use REST API</span></span>
<span data-ttu-id="f63d8-323">toomove istniejącą zasobów tooanother grupę zasobów lub subskrypcji, uruchom:</span><span class="sxs-lookup"><span data-stu-id="f63d8-323">toomove existing resources tooanother resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="f63d8-324">W treści żądania hello należy określić hello docelowa grupa zasobów i hello toomove zasobów.</span><span class="sxs-lookup"><span data-stu-id="f63d8-324">In hello request body, you specify hello target resource group and hello resources toomove.</span></span> <span data-ttu-id="f63d8-325">Aby uzyskać więcej informacji na temat operacji REST przenoszenia hello zobacz [przenoszenia zasobów](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="f63d8-325">For more information about hello move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f63d8-326">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f63d8-326">Next steps</span></span>
* <span data-ttu-id="f63d8-327">toolearn o poleceniach cmdlet programu PowerShell do zarządzania subskrypcją, zobacz [przy użyciu programu Azure PowerShell z usługą Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f63d8-327">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="f63d8-328">toolearn o polecenia wiersza polecenia platformy Azure do zarządzania subskrypcją, zobacz [hello Using Azure CLI za pomocą Menedżera zasobów](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f63d8-328">toolearn about Azure CLI commands for managing your subscription, see [Using hello Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="f63d8-329">Zobacz toolearn funkcje portalu do zarządzania subskrypcją, [korzystanie z zasobów platformy Azure toomanage portalu hello](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f63d8-329">toolearn about portal features for managing your subscription, see [Using hello Azure portal toomanage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="f63d8-330">toolearn o zastosowaniu logicznej tooyour zasobów organizacji, zobacz [używanie tagów tooorganize zasobami](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="f63d8-330">toolearn about applying a logical organization tooyour resources, see [Using tags tooorganize your resources](resource-group-using-tags.md).</span></span>
