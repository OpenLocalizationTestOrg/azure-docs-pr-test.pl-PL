---
title: "aaaAdd Azure automatyzacji elementów runbook toorecovery planów w portalu klasycznym hello | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak usługi Azure Site Recovery obecnie umożliwia tooextend planów odzyskiwania podczas odzyskiwania tooAzure przy użyciu złożone zadania toocomplete usługi Automatyzacja Azure"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a><span data-ttu-id="1b944-103">Dodaj w portalu klasycznym hello planów toorecovery elementów runbook usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="1b944-103">Add Azure automation runbooks toorecovery plans in hello classic portal</span></span>
<span data-ttu-id="1b944-104">W tym samouczku opisano, jak usługi Azure Site Recovery integruje się z planami toorecovery rozszerzalności tooprovide automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="1b944-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation tooprovide extensibility toorecovery plans.</span></span> <span data-ttu-id="1b944-105">Plany odzyskiwania można organizować odzyskiwania maszyn wirtualnych chronionych za pomocą usługi Azure Site Recovery dla chmury toosecondary replikacji i scenariusze tooAzure replikacji.</span><span class="sxs-lookup"><span data-stu-id="1b944-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication toosecondary cloud and replication tooAzure scenarios.</span></span> <span data-ttu-id="1b944-106">Ułatwiają również w podejmowaniu odzyskiwania hello **spójnie dokładne**, **powtarzalne**, i **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="1b944-106">They also help in making hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="1b944-107">Jeśli Twoje tooAzure maszyny wirtualne są awaryjne, integracja z usługi Automatyzacja Azure rozszerza planów odzyskiwania i daje możliwość tooexecute elementów runbook, dzięki czemu zaawansowanych automatyzacji zadań.</span><span class="sxs-lookup"><span data-stu-id="1b944-107">If you are failing over your virtual machines tooAzure, integration with Azure Automation extends the recovery plans and gives you capability tooexecute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="1b944-108">Jeśli ma nie wiesz o usługi Automatyzacja Azure jeszcze, zarejestruj się [tutaj](https://azure.microsoft.com/services/automation/) i pobierania ich przykładowe skrypty [tutaj](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="1b944-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="1b944-109">Przeczytaj więcej na temat [usługi Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) i jak plany tooorchestrate tooAzure odzyskiwania przy użyciu funkcji odzyskiwania [tutaj](https://azure.microsoft.com/blog/?p=166264).</span><span class="sxs-lookup"><span data-stu-id="1b944-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how tooorchestrate recovery tooAzure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="1b944-110">W tym samouczku krótkich przedstawiono sposób integrowania elementu runbook usługi Automatyzacja Azure do planów odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="1b944-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="1b944-111">Firma Microsoft będzie zautomatyzować prostych zadań, które wcześniej wymagana ręczna interwencja i zobacz, jak tooconvert multi krok odzyskiwania do akcji odzyskiwania jednym kliknięciem.</span><span class="sxs-lookup"><span data-stu-id="1b944-111">We will automate simple tasks that earlier required manual intervention and see how tooconvert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="1b944-112">Firma Microsoft będzie też przyjrzeć poznać sposoby rozwiązywania prostego skryptu, jeśli jego nieprawidłowość.</span><span class="sxs-lookup"><span data-stu-id="1b944-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-hello-application-tooazure"></a><span data-ttu-id="1b944-113">Ochrona powitalnych tooAzure aplikacji</span><span class="sxs-lookup"><span data-stu-id="1b944-113">Protect hello application tooAzure</span></span>
<span data-ttu-id="1b944-114">Daj nam rozpoczynać się od prostej aplikacji składający się z dwóch maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1b944-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="1b944-115">W tym miejscu zostały HRweb stosowania firmy Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="1b944-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="1b944-116">Firma Fabrikam-HRweb frontonu i zaplecza Hrweb-firma Fabrikam to Witaj dwie maszyny wirtualne chronione przy użyciu usługi Azure Site Recovery tooAzure.</span><span class="sxs-lookup"><span data-stu-id="1b944-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are hello two virtual machines protected tooAzure using Azure Site Recovery.</span></span> <span data-ttu-id="1b944-117">maszyn wirtualnych hello tooprotect za pomocą usługi Azure Site Recovery, wykonaj poniższe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="1b944-117">tooprotect hello virtual machines using Azure Site Recovery, follow hello steps below.</span></span>

1. <span data-ttu-id="1b944-118">Włącz ochronę maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1b944-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="1b944-119">Upewnij się, że hello maszyn wirtualnych zakończyły replikację początkową i jest replikowana.</span><span class="sxs-lookup"><span data-stu-id="1b944-119">Ensure that hello virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="1b944-120">Zaczekaj do ukończenia replikacji początkowej hello i chronione mówi hello stan replikacji.</span><span class="sxs-lookup"><span data-stu-id="1b944-120">Wait till hello initial replication completes and hello Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="1b944-121">W tym samouczku utworzymy plan odzyskiwania na powitania tooAzure hello toofailover Fabrikam HRweb aplikacji w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b944-121">In this tutorial, we will create a recovery plan for hello Fabrikam HRweb application toofailover hello application tooAzure.</span></span> <span data-ttu-id="1b944-122">Następnie firma Microsoft będzie zintegrować ją z elementu runbook, który spowoduje utworzenie punktu końcowego na powitania przejścia w tryb failover maszyny wirtualnej platformy Azure stron sieci web tooserve na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="1b944-122">Then we will integrate it with a runbook that will create an endpoint on hello failed over Azure virtual machine tooserve web pages at port 80.</span></span>

<span data-ttu-id="1b944-123">Najpierw utwórz plan odzyskiwania do naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b944-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-hello-recovery-plan"></a><span data-ttu-id="1b944-124">Tworzenie planu odzyskiwania hello</span><span class="sxs-lookup"><span data-stu-id="1b944-124">Create hello recovery plan</span></span>
<span data-ttu-id="1b944-125">tooAzure aplikacji hello toorecover, należy toocreate planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="1b944-125">toorecover hello application tooAzure, you need toocreate a recovery plan.</span></span>
<span data-ttu-id="1b944-126">Przy użyciu planu odzyskiwania, które można określić kolejność hello odzyskiwania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1b944-126">Using a recovery plan you can specify hello order of recovery of the virtual machines.</span></span> <span data-ttu-id="1b944-127">Maszyna wirtualna Hello umieszczona w grupie 1 będzie odzyskanie i uruchomić się jako pierwszy i postępuj hello maszyny wirtualnej z grupy 2.</span><span class="sxs-lookup"><span data-stu-id="1b944-127">hello virtual machine placed in group 1 will recover and start first, and then hello virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="1b944-128">Tworzenie planu odzyskiwania, który wygląda jak poniżej.</span><span class="sxs-lookup"><span data-stu-id="1b944-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="1b944-129">więcej informacji na temat planów odzyskiwania, przeczytaj dokumentację tooread [tutaj](https://msdn.microsoft.com/library/azure/dn788799.aspx "tutaj").</span><span class="sxs-lookup"><span data-stu-id="1b944-129">tooread more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="1b944-130">Następnie utwórz hello artefakty niezbędne w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="1b944-130">Next, let's create hello necessary artifacts in Azure Automation.</span></span>

## <a name="create-hello-automation-account-and-its-assets"></a><span data-ttu-id="1b944-131">Tworzenie konta automatyzacji hello i jej zasobów</span><span class="sxs-lookup"><span data-stu-id="1b944-131">Create hello automation account and its assets</span></span>
<span data-ttu-id="1b944-132">Należy runbook toocreate konto usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="1b944-132">You need an Azure Automation account toocreate runbooks.</span></span> <span data-ttu-id="1b944-133">Jeśli nie masz już konto, przejdź wskazywane przez kartę automatyzacji tooAzure ![](media/site-recovery-runbook-automation/02.png)i Utwórz nowe konto.</span><span class="sxs-lookup"><span data-stu-id="1b944-133">If you do not already have an account, navigate tooAzure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="1b944-134">Nadaj kontu hello tooidentify nazwy z.</span><span class="sxs-lookup"><span data-stu-id="1b944-134">Give hello account a name tooidentify with.</span></span>
2. <span data-ttu-id="1b944-135">Określ region geograficzny, w którym ma tooplace hello konta.</span><span class="sxs-lookup"><span data-stu-id="1b944-135">Specify a geographical region where you want tooplace hello account.</span></span>

<span data-ttu-id="1b944-136">Zalecane jest tooplace hello konta w hello tym samym regionie co magazyn hello funkcja automatycznego odzyskiwania systemu.</span><span class="sxs-lookup"><span data-stu-id="1b944-136">It is recommended tooplace hello account in hello same region as hello ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="1b944-137">Następnie należy utworzyć hello następujące zasoby w hello konta.</span><span class="sxs-lookup"><span data-stu-id="1b944-137">Next, create hello following assets in hello Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="1b944-138">Dodaj nazwę subskrypcji jako zasobów</span><span class="sxs-lookup"><span data-stu-id="1b944-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="1b944-139">Dodaj nowe ustawienie ![](media/site-recovery-runbook-automation/04.png) w hello zasobów usługi Automatyzacja Azure i wybierz zbyt![](media/site-recovery-runbook-automation/05.png)</span><span class="sxs-lookup"><span data-stu-id="1b944-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select too![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="1b944-140">Wybierz typ zmiennej hello jako **ciągu**</span><span class="sxs-lookup"><span data-stu-id="1b944-140">Select hello variable type as **String**</span></span>
3. <span data-ttu-id="1b944-141">Określ nazwę zmiennej jako **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="1b944-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="1b944-142">Określ nazwę rzeczywiste subskrypcji platformy Azure jako hello wartość zmiennej.</span><span class="sxs-lookup"><span data-stu-id="1b944-142">Specify your actual Azure Subscription name as hello variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="1b944-143">Można ustalić nazwy hello subskrypcji ze strony ustawień hello Twojego konta na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1b944-143">You can identify hello name of your subscription from hello settings page of your account on hello Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="1b944-144">Dodaj poświadczeń logowania do systemu Azure jako zasobów</span><span class="sxs-lookup"><span data-stu-id="1b944-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="1b944-145">Automatyzacja Azure korzysta z programu Azure PowerShell tooconnect toothe subskrypcji i działa na powitania artefakty istnieje.</span><span class="sxs-lookup"><span data-stu-id="1b944-145">Azure Automation uses Azure PowerShell tooconnect toothe subscription and operates on hello artifacts there.</span></span> <span data-ttu-id="1b944-146">W tym celu należy przeprowadzić uwierzytelniania za pomocą konta Microsoft lub konta służbowego.</span><span class="sxs-lookup"><span data-stu-id="1b944-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="1b944-147">Poświadczenia konta hello można przechowywać w toobe zasobów bezpiecznie używany przez element runbook hello.</span><span class="sxs-lookup"><span data-stu-id="1b944-147">You can store hello account credentials in an asset toobe used securely by hello runbook.</span></span>

1. <span data-ttu-id="1b944-148">Dodaj nowe ustawienie ![](media/site-recovery-runbook-automation/04.png) w hello zasobów usługi Automatyzacja Azure i wybierz pozycję![](media/site-recovery-runbook-automation/09.png)</span><span class="sxs-lookup"><span data-stu-id="1b944-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="1b944-149">Wybierz typ poświadczenia hello jako **poświadczenie programu PowerShell systemu Windows**</span><span class="sxs-lookup"><span data-stu-id="1b944-149">Select hello Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="1b944-150">Określ nazwę hello jako **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="1b944-150">Specify hello name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="1b944-151">Określ hello nazwy użytkownika i hasła toosign za pomocą.</span><span class="sxs-lookup"><span data-stu-id="1b944-151">Specify hello username and password toosign-in with.</span></span>

<span data-ttu-id="1b944-152">Teraz oba te ustawienia są dostępne w zasobów.</span><span class="sxs-lookup"><span data-stu-id="1b944-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="1b944-153">Więcej informacji na temat sposobu tooconnect tooyour subskrypcji za pomocą programu PowerShell znajduje [tutaj](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1b944-153">More information about how tooconnect tooyour subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="1b944-154">Następnie spowoduje utworzenie elementu runbook w automatyzacji Azure, które można dodać punktu końcowego dla maszyny wirtualnej frontonu powitania po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="1b944-154">Next, you will create a runbook in Azure Automation that can add an endpoint for hello front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="1b944-155">Kontekst usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="1b944-155">Azure automation context</span></span>
<span data-ttu-id="1b944-156">Funkcja automatycznego odzyskiwania systemu przekazuje kontekst zmiennej toohello runbook toohelp pisania skryptów deterministyczna.</span><span class="sxs-lookup"><span data-stu-id="1b944-156">ASR passes a context variable toohello runbook toohelp you write deterministic scripts.</span></span> <span data-ttu-id="1b944-157">Jeden można argumentowało nazwy hello hello usługi w chmurze i hello maszyny wirtualnej są przewidywalne, ale się stanie, że nie jest on zawsze hello przypadku z powodu toocertain scenariuszy, takich jak hello co gdzie hello nazwy hello maszyny wirtualnej mogła ulec zmianie ukończenia znaki toounsupported na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1b944-157">One could argue that hello names of hello Cloud Service and hello Virtual Machine are predictable, but happens that it is not always hello case owing toocertain scenarios such as hello one where hello name of hello virtual machine name might have changed due toounsupported characters in Azure.</span></span> <span data-ttu-id="1b944-158">Dlatego te informacje są przesyłane planu odzyskiwania toohello ASR jako część hello *kontekstu*.</span><span class="sxs-lookup"><span data-stu-id="1b944-158">Hence this information is passed toohello ASR recovery plan as part of hello *context*.</span></span>

<span data-ttu-id="1b944-159">Poniżej przedstawiono przykładowy wygląd hello zmiennej kontekstu.</span><span class="sxs-lookup"><span data-stu-id="1b944-159">Below is an example of how hello context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="1b944-160">w poniższej tabeli Hello zawiera nazwę i opis dla każdej zmiennej w kontekście hello.</span><span class="sxs-lookup"><span data-stu-id="1b944-160">hello table below contains name and description for each variable in hello context.</span></span>

| <span data-ttu-id="1b944-161">**Nazwa zmiennej**</span><span class="sxs-lookup"><span data-stu-id="1b944-161">**Variable name**</span></span> | <span data-ttu-id="1b944-162">**Opis**</span><span class="sxs-lookup"><span data-stu-id="1b944-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="1b944-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="1b944-163">RecoveryPlanName</span></span> |<span data-ttu-id="1b944-164">Nazwa planu uruchomione.</span><span class="sxs-lookup"><span data-stu-id="1b944-164">Name of plan being run.</span></span> <span data-ttu-id="1b944-165">Ułatwia wykonanie akcji ze względu na użycie nazwy hello sam skrypt</span><span class="sxs-lookup"><span data-stu-id="1b944-165">Helps you take action based on name using hello same script</span></span> |
| <span data-ttu-id="1b944-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="1b944-166">FailoverType</span></span> |<span data-ttu-id="1b944-167">Określa, czy tryb failover hello jest przetestować, planowane lub nieplanowane.</span><span class="sxs-lookup"><span data-stu-id="1b944-167">Specifies whether hello failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="1b944-168">Element FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="1b944-168">FailoverDirection</span></span> |<span data-ttu-id="1b944-169">Określ, czy odzyskiwania jest tooprimary lub pomocniczej</span><span class="sxs-lookup"><span data-stu-id="1b944-169">Specify whether recovery is tooprimary or secondary</span></span> |
| <span data-ttu-id="1b944-170">Identyfikator grupy</span><span class="sxs-lookup"><span data-stu-id="1b944-170">GroupID</span></span> |<span data-ttu-id="1b944-171">Zidentyfikować numer grupy hello w ramach planu odzyskiwania hello planu hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="1b944-171">Identify hello group number within hello recovery plan when hello plan is running</span></span> |
| <span data-ttu-id="1b944-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="1b944-172">VmMap</span></span> |<span data-ttu-id="1b944-173">Tablica wszystkich maszyn wirtualnych hello hello grupy</span><span class="sxs-lookup"><span data-stu-id="1b944-173">Array of all hello virtual machines in hello group</span></span> |
| <span data-ttu-id="1b944-174">Klucz VMMap</span><span class="sxs-lookup"><span data-stu-id="1b944-174">VMMap key</span></span> |<span data-ttu-id="1b944-175">Klucz unikatowy (identyfikator GUID) dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1b944-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="1b944-176">Ma hello taka sama, jak hello programu VMM o identyfikatorze hello maszyny wirtualnej, jeśli to możliwe.</span><span class="sxs-lookup"><span data-stu-id="1b944-176">It's hello same as hello VMM ID of hello virtual machine where applicable.</span></span> |
| <span data-ttu-id="1b944-177">RoleName</span><span class="sxs-lookup"><span data-stu-id="1b944-177">RoleName</span></span> |<span data-ttu-id="1b944-178">Nazwa maszyny Wirtualnej platformy Azure, która jest przywracana hello</span><span class="sxs-lookup"><span data-stu-id="1b944-178">Name of hello Azure VM that's being recovered</span></span> |
| <span data-ttu-id="1b944-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="1b944-179">CloudServiceName</span></span> |<span data-ttu-id="1b944-180">Nazwa usługi w chmurze platformy Azure pod które hello utworzeniu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1b944-180">Azure Cloud Service name under which hello virtual machine is created.</span></span> |

<span data-ttu-id="1b944-181">Witaj tooidentify VmMap klucza w kontekście hello można również przejść toohello strony właściwości maszyny Wirtualnej w usłudze ASR i przyjrzyj się hello właściwości GUID maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1b944-181">tooidentify hello VmMap Key in hello context you could also go toohello VM properties page in ASR and look at hello VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="1b944-182">Tworzenie elementu runbook automatyzacji</span><span class="sxs-lookup"><span data-stu-id="1b944-182">Author an Automation runbook</span></span>
<span data-ttu-id="1b944-183">Na maszynie wirtualnej frontonu hello tworzyć hello runbook tooopen portu 80.</span><span class="sxs-lookup"><span data-stu-id="1b944-183">Now create hello runbook tooopen port 80 on hello front-end virtual machine.</span></span>

1. <span data-ttu-id="1b944-184">Utwórz nowy element runbook w hello konto usługi Automatyzacja Azure o nazwie hello **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="1b944-184">Create a new runbook in hello Azure Automation account with hello name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="1b944-185">Przejdź toohello widoku autora elementu hello runbook, a następnie wprowadź hello trybie wersji roboczej.</span><span class="sxs-lookup"><span data-stu-id="1b944-185">Navigate toohello Author view of hello runbook and enter hello draft mode.</span></span>
3. <span data-ttu-id="1b944-186">Najpierw określ hello toouse zmiennej jako kontekstu planu odzyskiwania hello</span><span class="sxs-lookup"><span data-stu-id="1b944-186">First specify hello variable toouse as hello recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="1b944-187">Następnym połączeniu toohello subskrypcji przy użyciu nazwy hello poświadczeń i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1b944-187">Next connect toohello subscription using hello credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="1b944-188">Należy pamiętać, że używasz hello Azure zasoby — **AzureCredential** i **AzureSubscriptionName** tutaj.</span><span class="sxs-lookup"><span data-stu-id="1b944-188">Note that you use hello Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="1b944-189">Teraz Określ szczegóły punktu końcowego hello i hello GUID hello maszyny wirtualnej, dla której ma zostać tooexpose hello endpoint.</span><span class="sxs-lookup"><span data-stu-id="1b944-189">Now specify hello endpoint details and hello GUID of hello virtual machine for which you want tooexpose hello endpoint.</span></span> <span data-ttu-id="1b944-190">W przypadku hello frontonu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1b944-190">In this case hello front-end virtual machine.</span></span>

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="1b944-191">To ustawienie określa hello protokół punktu końcowego platformy Azure, port lokalny na powitania maszyny Wirtualnej i jej zamapowanych publicznego.</span><span class="sxs-lookup"><span data-stu-id="1b944-191">This specifies hello Azure endpoint protocol, local port on hello VM and its mapped public port.</span></span> <span data-ttu-id="1b944-192">Te zmienne są parametry wymagane przez hello Azure poleceń, które dodać tooVMs punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="1b944-192">These variables are parameters     required by hello Azure commands that add endpoints tooVMs.</span></span> <span data-ttu-id="1b944-193">Witaj VMGUID przechowuje hello hello maszyny wirtualnej, którą należy toooperate na identyfikator GUID.</span><span class="sxs-lookup"><span data-stu-id="1b944-193">hello VMGUID holds hello GUID of hello virtual machine you need toooperate on.</span></span>
6. <span data-ttu-id="1b944-194">skrypt Hello teraz wyodrębnić hello kontekst hello podany identyfikator GUID maszyny Wirtualnej i utworzyć punktu końcowego na maszynie wirtualnej hello odwołuje się on.</span><span class="sxs-lookup"><span data-stu-id="1b944-194">hello script will now extract hello context for hello given VM GUID and create an endpoint on hello virtual machine referenced by it.</span></span>

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="1b944-195">Po zakończeniu tej operacji, kliknij przycisk Publikuj ![](media/site-recovery-runbook-automation/20.png) tooallow Twojego skryptu toobe dostępna do wykonania.</span><span class="sxs-lookup"><span data-stu-id="1b944-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) tooallow your script toobe available for execution.</span></span>

<span data-ttu-id="1b944-196">Ukończ skrypt Hello jest podany poniżej użytkownikowi</span><span class="sxs-lookup"><span data-stu-id="1b944-196">hello complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a><span data-ttu-id="1b944-197">Dodaj planu odzyskiwania toohello skryptu hello</span><span class="sxs-lookup"><span data-stu-id="1b944-197">Add hello script toohello recovery plan</span></span>
<span data-ttu-id="1b944-198">Gdy skrypt hello jest gotowy, można dodać toohello planu odzyskiwania, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="1b944-198">Once hello script is ready, you can add it toohello recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="1b944-199">W planie odzyskiwania hello utworzone wybierz tooadd skrypt po grupie 2.</span><span class="sxs-lookup"><span data-stu-id="1b944-199">In hello recovery plan you created, choose tooadd a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="1b944-200">Określ nazwę skryptu.</span><span class="sxs-lookup"><span data-stu-id="1b944-200">Specify a script name.</span></span> <span data-ttu-id="1b944-201">Jest to po prostu przyjazną nazwę dla tego skryptu do projekcji w ramach planu odzyskiwania hello.</span><span class="sxs-lookup"><span data-stu-id="1b944-201">This is just a friendly name for this script for showing within hello Recovery plan.</span></span>
3. <span data-ttu-id="1b944-202">W skrypcie tooAzure pracy awaryjnej hello — wybierz nazwę konta usługi Automatyzacja Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1b944-202">In hello failover tooAzure script – Select hello Azure Automation Account name.</span></span>
4. <span data-ttu-id="1b944-203">W hello Azure elementów Runbook wybierz element runbook hello, Twojego autorstwa.</span><span class="sxs-lookup"><span data-stu-id="1b944-203">In hello Azure Runbooks, select hello runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="1b944-204">Skrypty po stronie podstawowej</span><span class="sxs-lookup"><span data-stu-id="1b944-204">Primary side scripts</span></span>
<span data-ttu-id="1b944-205">Podczas wykonywania tooAzure trybu failover, można tooexecute skrypty po stronie głównej.</span><span class="sxs-lookup"><span data-stu-id="1b944-205">When you are executing a failover tooAzure, you can also choose tooexecute primary side scripts.</span></span> <span data-ttu-id="1b944-206">Skrypty te zostanie uruchomiony na serwerze VMM hello podczas pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="1b944-206">These scripts will run on hello VMM server during failover.</span></span>
<span data-ttu-id="1b944-207">Skrypty po stronie podstawowej są dostępne tylko w przypadku zamknięcia wstępne tylko i post etapy zamknięcia.</span><span class="sxs-lookup"><span data-stu-id="1b944-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="1b944-208">Jest to spowodowane oczekujemy toobe lokacji głównej hello zwykle niedostępne momencie uderzenia awarii.</span><span class="sxs-lookup"><span data-stu-id="1b944-208">This is because we expect hello primary site toobe typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="1b944-209">Podczas nieplanowany tryb failover tylko w przypadku uczestnictwa w operacjach lokacji głównej, będzie podejmować toorun hello głównej stronie skryptów.</span><span class="sxs-lookup"><span data-stu-id="1b944-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt toorun hello primary side scripts.</span></span> <span data-ttu-id="1b944-210">Jeśli nie są dostępne lub limit czasu pracy awaryjnej hello będą nadal toorecover hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="1b944-210">If they are not reachable or timeout, hello failover will continue toorecover hello virtual machines.</span></span>
<span data-ttu-id="1b944-211">Skrypty po stronie głównej cofanie dostępnych dla lokacji VMware/fizyczna/funkcji Hyper-v bez tooAzure VMM chronione - podczas tooAzure trybu failover.</span><span class="sxs-lookup"><span data-stu-id="1b944-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected tooAzure - while you failover tooAzure.</span></span>
<span data-ttu-id="1b944-212">Jednak po awarii z platformy Azure tooon lokalnie skrypty po stronie głównej (elementów Runbook) może służyć do wszystkich miejsc docelowych oprócz VMware.</span><span class="sxs-lookup"><span data-stu-id="1b944-212">However, when you failback from Azure tooon-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-hello-recovery-plan"></a><span data-ttu-id="1b944-213">Plan odzyskiwania hello testu</span><span class="sxs-lookup"><span data-stu-id="1b944-213">Test hello recovery plan</span></span>
<span data-ttu-id="1b944-214">Po dodaniu hello runbook toohello planu można zainicjować test trybu failover i zobaczyć ją w akcji.</span><span class="sxs-lookup"><span data-stu-id="1b944-214">Once you have added hello runbook toohello plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="1b944-215">Zawsze zalecane toorun tootest pracy awaryjnej testu Twojej aplikacji i hello odzyskiwania planu tooensure czy nie ma żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="1b944-215">It is always recommended toorun a test failover tootest your application and hello recovery plan tooensure that there are no errors.</span></span>

1. <span data-ttu-id="1b944-216">Wybierz plan odzyskiwania hello i zainicjuj test trybu failover.</span><span class="sxs-lookup"><span data-stu-id="1b944-216">Select hello recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="1b944-217">Podczas wykonywania planu hello możesz wyświetlić czy hello runbook jest wykonywana za pomocą jego stan.</span><span class="sxs-lookup"><span data-stu-id="1b944-217">During hello plan execution, you can see whether hello runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="1b944-218">Możesz również sprawdzić hello szczegółowy stan wykonywania elementu runbook na stronie zadań usługi Automatyzacja Azure hello hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="1b944-218">You can also see hello detailed runbook execution status on hello Azure Automation jobs page for hello runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="1b944-219">Po zakończeniu pracy awaryjnej hello, oprócz hello wyniku wykonania elementu runbook, widoczny czy wykonanie hello zakończy się pomyślnie lub nie odwiedzać strony maszyny wirtualnej platformy Azure hello i patrzeć hello punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="1b944-219">After hello failover completes, apart from hello runbook execution result, you can see whether hello execution is successful or not by visiting hello Azure virtual machine page and looking at hello endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="1b944-220">Przykładowe skrypty</span><span class="sxs-lookup"><span data-stu-id="1b944-220">Sample scripts</span></span>
<span data-ttu-id="1b944-221">Podczas Rezygnacja za pomocą automatyzacji jedną powszechnie używane zadania dodawania tooan punktu końcowego maszyny wirtualnej platformy Azure w tym samouczku, może wykonać szereg inne zadania automatyzacji zaawansowanych przy użyciu automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="1b944-221">While we walked through automating one commonly used task of adding an endpoint tooan Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="1b944-222">Firma Microsoft i hello społeczności usługi Automatyzacja Azure znajdują się przykładowe elementy runbook, które mogą pomóc rozpocząć tworzenie własnych rozwiązań i narzędzie elementów runbook, którego można użyć jako bloków konstrukcyjnych dla większych automatyzacji zadań.</span><span class="sxs-lookup"><span data-stu-id="1b944-222">Microsoft and hello Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="1b944-223">Rozpocznij korzystanie z nich z galerii hello i tworzenie planów odzyskiwania jednym kliknięciem zaawansowanych aplikacji przy użyciu usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1b944-223">Start using them from hello gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1b944-224">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1b944-224">Additional Resources</span></span>
[<span data-ttu-id="1b944-225">Przegląd automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="1b944-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Omówienie usługi Automatyzacja Azure")

[<span data-ttu-id="1b944-226">Przykładowe skrypty usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="1b944-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "przykładowe skrypty usługi Automatyzacja Azure")
