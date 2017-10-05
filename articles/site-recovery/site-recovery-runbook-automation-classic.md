---
title: "Dodaj elementy runbook automatyzacji Azure do planów odzyskiwania w klasycznym portalu | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak usługi Azure Site Recovery umożliwia teraz rozszerzyć planów odzyskiwania wykonać złożone zadania podczas odzyskiwania na platformie Azure przy użyciu automatyzacji Azure"
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
ms.openlocfilehash: 0a248e7c3f39a35ac10dc6ac64e5cef7d152e033
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans-in-the-classic-portal"></a><span data-ttu-id="af4bd-103">Dodaj elementy runbook automatyzacji Azure do planów odzyskiwania w klasycznym portalu</span><span class="sxs-lookup"><span data-stu-id="af4bd-103">Add Azure automation runbooks to recovery plans in the classic portal</span></span>
<span data-ttu-id="af4bd-104">W tym samouczku opisano, jak usługi Azure Site Recovery integruje się z automatyzacji Azure, który zapewni możliwość rozszerzenia do planów odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="af4bd-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation to provide extensibility to recovery plans.</span></span> <span data-ttu-id="af4bd-105">Plany odzyskiwania można organizować odzyskiwania maszyn wirtualnych chronionych za pomocą usługi Azure Site Recovery dla replikacji do chmury dodatkowej i replikacji do platformy Azure scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="af4bd-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication to secondary cloud and replication to Azure scenarios.</span></span> <span data-ttu-id="af4bd-106">Ułatwiają również w podejmowaniu odzyskiwania **spójnie dokładne**, **powtarzalne**, i **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="af4bd-106">They also help in making the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="af4bd-107">Jeśli kończą się niepowodzeniem na maszynach wirtualnych Azure, integracja z usługi Automatyzacja Azure rozszerza planów odzyskiwania i daje możliwość wykonywania elementów runbook, dzięki czemu zaawansowanych automatyzacji zadań.</span><span class="sxs-lookup"><span data-stu-id="af4bd-107">If you are failing over your virtual machines to Azure, integration with Azure Automation extends the recovery plans and gives you capability to execute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="af4bd-108">Jeśli ma nie wiesz o usługi Automatyzacja Azure jeszcze, zarejestruj się [tutaj](https://azure.microsoft.com/services/automation/) i pobierania ich przykładowe skrypty [tutaj](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="af4bd-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="af4bd-109">Przeczytaj więcej na temat [usługi Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) i organizowania odzyskiwania na platformie Azure przy użyciu planów odzyskiwania [tutaj](https://azure.microsoft.com/blog/?p=166264).</span><span class="sxs-lookup"><span data-stu-id="af4bd-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how to orchestrate recovery to Azure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="af4bd-110">W tym samouczku krótkich przedstawiono sposób integrowania elementu runbook usługi Automatyzacja Azure do planów odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="af4bd-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="af4bd-111">Firma Microsoft będzie zautomatyzować prostych zadań, które wcześniej wymagana ręczna interwencja i zobacz, jak przekonwertować odzyskiwania krok multi na akcję odzyskiwania jednym kliknięciem.</span><span class="sxs-lookup"><span data-stu-id="af4bd-111">We will automate simple tasks that earlier required manual intervention and see how to convert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="af4bd-112">Firma Microsoft będzie też przyjrzeć poznać sposoby rozwiązywania prostego skryptu, jeśli jego nieprawidłowość.</span><span class="sxs-lookup"><span data-stu-id="af4bd-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-the-application-to-azure"></a><span data-ttu-id="af4bd-113">Ochrona aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="af4bd-113">Protect the application to Azure</span></span>
<span data-ttu-id="af4bd-114">Daj nam rozpoczynać się od prostej aplikacji składający się z dwóch maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="af4bd-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="af4bd-115">W tym miejscu zostały HRweb stosowania firmy Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="af4bd-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="af4bd-116">Firma Fabrikam-HRweb frontonu i zaplecza Hrweb-Fabrikam są dwie maszyny wirtualne chronione na platformie Azure przy użyciu usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="af4bd-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are the two virtual machines protected to Azure using Azure Site Recovery.</span></span> <span data-ttu-id="af4bd-117">Aby włączyć ochronę maszyn wirtualnych przy użyciu usługi Azure Site Recovery, wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="af4bd-117">To protect the virtual machines using Azure Site Recovery, follow the steps below.</span></span>

1. <span data-ttu-id="af4bd-118">Włącz ochronę maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="af4bd-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="af4bd-119">Upewnij się, że maszyny wirtualne zakończyły replikację początkową i jest replikowana.</span><span class="sxs-lookup"><span data-stu-id="af4bd-119">Ensure that the virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="af4bd-120">Zaczekaj do ukończenia replikacji początkowej, a stan replikacji mówi chronione.</span><span class="sxs-lookup"><span data-stu-id="af4bd-120">Wait till the initial replication completes and the Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="af4bd-121">W tym samouczku utworzymy planu odzyskiwania do trybu failover aplikacji na platformie Azure aplikacji HRweb firmy Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="af4bd-121">In this tutorial, we will create a recovery plan for the Fabrikam HRweb application to failover the application to Azure.</span></span> <span data-ttu-id="af4bd-122">Następnie firma Microsoft będzie zintegrować ją z elementu runbook, który spowoduje utworzenie punktu końcowego na nieudane za pośrednictwem maszyny wirtualnej platformy Azure do obsługi stron sieci web na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="af4bd-122">Then we will integrate it with a runbook that will create an endpoint on the failed over Azure virtual machine to serve web pages at port 80.</span></span>

<span data-ttu-id="af4bd-123">Najpierw utwórz plan odzyskiwania do naszej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="af4bd-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-the-recovery-plan"></a><span data-ttu-id="af4bd-124">Tworzenie planu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="af4bd-124">Create the recovery plan</span></span>
<span data-ttu-id="af4bd-125">Aby odzyskać aplikacji na platformie Azure, należy utworzyć plan odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="af4bd-125">To recover the application to Azure, you need to create a recovery plan.</span></span>
<span data-ttu-id="af4bd-126">Przy użyciu planu odzyskiwania, które można określić kolejność odzyskiwania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="af4bd-126">Using a recovery plan you can specify the order of recovery of the virtual machines.</span></span> <span data-ttu-id="af4bd-127">Maszyna wirtualna umieszczona w grupie 1 będzie odzyskać i uruchomić się jako pierwszy, i postępuj maszyny wirtualnej z grupy 2.</span><span class="sxs-lookup"><span data-stu-id="af4bd-127">The virtual machine placed in group 1 will recover and start first, and then the virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="af4bd-128">Tworzenie planu odzyskiwania, który wygląda jak poniżej.</span><span class="sxs-lookup"><span data-stu-id="af4bd-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="af4bd-129">Aby dowiedzieć się więcej o planach odzyskiwania, przeczytaj dokumentację [tutaj](https://msdn.microsoft.com/library/azure/dn788799.aspx "tutaj").</span><span class="sxs-lookup"><span data-stu-id="af4bd-129">To read more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="af4bd-130">Następnie utwórz artefakty niezbędne w automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="af4bd-130">Next, let's create the necessary artifacts in Azure Automation.</span></span>

## <a name="create-the-automation-account-and-its-assets"></a><span data-ttu-id="af4bd-131">Tworzenie konta automatyzacji i jego zasoby.</span><span class="sxs-lookup"><span data-stu-id="af4bd-131">Create the automation account and its assets</span></span>
<span data-ttu-id="af4bd-132">Musisz mieć konto usługi Automatyzacja Azure do tworzenia elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="af4bd-132">You need an Azure Automation account to create runbooks.</span></span> <span data-ttu-id="af4bd-133">Jeśli nie masz już konto, przejdź do karty usługi Automatyzacja Azure wskazywane przez ![](media/site-recovery-runbook-automation/02.png)i Utwórz nowe konto.</span><span class="sxs-lookup"><span data-stu-id="af4bd-133">If you do not already have an account, navigate to Azure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="af4bd-134">Nadaj nazwę identyfikującą z konta.</span><span class="sxs-lookup"><span data-stu-id="af4bd-134">Give the account a name to identify with.</span></span>
2. <span data-ttu-id="af4bd-135">Określ region geograficzny, w której chcesz umieścić konta.</span><span class="sxs-lookup"><span data-stu-id="af4bd-135">Specify a geographical region where you want to place the account.</span></span>

<span data-ttu-id="af4bd-136">Zalecane jest umieszczenie konta w tym samym regionie co magazyn usługi ASR.</span><span class="sxs-lookup"><span data-stu-id="af4bd-136">It is recommended to place the account in the same region as the ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="af4bd-137">Następnie należy utworzyć następujące zasoby w ramach konta.</span><span class="sxs-lookup"><span data-stu-id="af4bd-137">Next, create the following assets in the Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="af4bd-138">Dodaj nazwę subskrypcji jako zasobów</span><span class="sxs-lookup"><span data-stu-id="af4bd-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="af4bd-139">Dodaj nowe ustawienie ![](media/site-recovery-runbook-automation/04.png) w zasoby automatyzacji Azure i wybrać opcję![](media/site-recovery-runbook-automation/05.png)</span><span class="sxs-lookup"><span data-stu-id="af4bd-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select to ![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="af4bd-140">Wybierz typ zmiennej jako **ciągu**</span><span class="sxs-lookup"><span data-stu-id="af4bd-140">Select the variable type as **String**</span></span>
3. <span data-ttu-id="af4bd-141">Określ nazwę zmiennej jako **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="af4bd-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="af4bd-142">Określ nazwę rzeczywiste subskrypcji platformy Azure jako wartość zmiennej.</span><span class="sxs-lookup"><span data-stu-id="af4bd-142">Specify your actual Azure Subscription name as the variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="af4bd-143">Można określić nazwę subskrypcji ze strony ustawień konta w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="af4bd-143">You can identify the name of your subscription from the settings page of your account on the Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="af4bd-144">Dodaj poświadczeń logowania do systemu Azure jako zasobów</span><span class="sxs-lookup"><span data-stu-id="af4bd-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="af4bd-145">Automatyzacja Azure korzysta z programu Azure PowerShell do nawiązania połączenia z subskrypcją i działa na artefakty istnieje.</span><span class="sxs-lookup"><span data-stu-id="af4bd-145">Azure Automation uses Azure PowerShell to connect to the subscription and operates on the artifacts there.</span></span> <span data-ttu-id="af4bd-146">W tym celu należy przeprowadzić uwierzytelniania za pomocą konta Microsoft lub konta służbowego.</span><span class="sxs-lookup"><span data-stu-id="af4bd-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="af4bd-147">Poświadczenia konta można przechowywać w zasób ma być bezpiecznie używany przez element runbook.</span><span class="sxs-lookup"><span data-stu-id="af4bd-147">You can store the account credentials in an asset to be used securely by the runbook.</span></span>

1. <span data-ttu-id="af4bd-148">Dodaj nowe ustawienie ![](media/site-recovery-runbook-automation/04.png) w zasoby automatyzacji Azure i wybierz pozycję![](media/site-recovery-runbook-automation/09.png)</span><span class="sxs-lookup"><span data-stu-id="af4bd-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="af4bd-149">Wybierz typ poświadczenia jako **poświadczenie programu PowerShell systemu Windows**</span><span class="sxs-lookup"><span data-stu-id="af4bd-149">Select the Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="af4bd-150">Określ nazwę jako **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="af4bd-150">Specify the name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="af4bd-151">Określ nazwę użytkownika i hasło do logowania z.</span><span class="sxs-lookup"><span data-stu-id="af4bd-151">Specify the username and password to sign-in with.</span></span>

<span data-ttu-id="af4bd-152">Teraz oba te ustawienia są dostępne w zasobów.</span><span class="sxs-lookup"><span data-stu-id="af4bd-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="af4bd-153">Więcej informacji na temat nawiązywania połączenia z subskrypcją za pomocą programu PowerShell znajduje się [tutaj](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="af4bd-153">More information about how to connect to your subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="af4bd-154">Następnie spowoduje utworzenie elementu runbook w automatyzacji Azure, które można dodać punktu końcowego dla frontonu maszyny wirtualnej po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="af4bd-154">Next, you will create a runbook in Azure Automation that can add an endpoint for the front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="af4bd-155">Kontekst usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="af4bd-155">Azure automation context</span></span>
<span data-ttu-id="af4bd-156">Funkcja automatycznego odzyskiwania systemu przekazuje zmiennej kontekstu do elementu runbook, który ułatwia pisanie skryptów deterministyczna.</span><span class="sxs-lookup"><span data-stu-id="af4bd-156">ASR passes a context variable to the runbook to help you write deterministic scripts.</span></span> <span data-ttu-id="af4bd-157">Co można argumentowało nazwy usługi w chmurze i maszyny wirtualnej są przewidywalne, ale się stanie, że nie jest zawsze przypadku z powodu niektórych scenariuszy, takich jak, której nazwę maszyny wirtualnej mogła ulec zmianie z powodu nieobsługiwanych znaków na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="af4bd-157">One could argue that the names of the Cloud Service and the Virtual Machine are predictable, but happens that it is not always the case owing to certain scenarios such as the one where the name of the virtual machine name might have changed due to unsupported characters in Azure.</span></span> <span data-ttu-id="af4bd-158">Dlatego te informacje są przesyłane do planu odzyskiwania ASR jako część *kontekstu*.</span><span class="sxs-lookup"><span data-stu-id="af4bd-158">Hence this information is passed to the ASR recovery plan as part of the *context*.</span></span>

<span data-ttu-id="af4bd-159">Poniżej przedstawiono przykładowy wygląd zmiennej kontekstu.</span><span class="sxs-lookup"><span data-stu-id="af4bd-159">Below is an example of how the context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="af4bd-160">Poniższa tabela zawiera nazwę i opis dla każdej zmiennej w kontekście.</span><span class="sxs-lookup"><span data-stu-id="af4bd-160">The table below contains name and description for each variable in the context.</span></span>

| <span data-ttu-id="af4bd-161">**Nazwa zmiennej**</span><span class="sxs-lookup"><span data-stu-id="af4bd-161">**Variable name**</span></span> | <span data-ttu-id="af4bd-162">**Opis**</span><span class="sxs-lookup"><span data-stu-id="af4bd-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="af4bd-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="af4bd-163">RecoveryPlanName</span></span> |<span data-ttu-id="af4bd-164">Nazwa planu uruchomione.</span><span class="sxs-lookup"><span data-stu-id="af4bd-164">Name of plan being run.</span></span> <span data-ttu-id="af4bd-165">Pomaga podjąć działania na podstawie nazwy przy użyciu tego samego skryptu</span><span class="sxs-lookup"><span data-stu-id="af4bd-165">Helps you take action based on name using the same script</span></span> |
| <span data-ttu-id="af4bd-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="af4bd-166">FailoverType</span></span> |<span data-ttu-id="af4bd-167">Określa, czy tryb failover jest przetestować, planowane lub nieplanowane.</span><span class="sxs-lookup"><span data-stu-id="af4bd-167">Specifies whether the failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="af4bd-168">Element FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="af4bd-168">FailoverDirection</span></span> |<span data-ttu-id="af4bd-169">Określ, czy odzyskiwania jest podstawowym lub pomocniczym</span><span class="sxs-lookup"><span data-stu-id="af4bd-169">Specify whether recovery is to primary or secondary</span></span> |
| <span data-ttu-id="af4bd-170">Identyfikator grupy</span><span class="sxs-lookup"><span data-stu-id="af4bd-170">GroupID</span></span> |<span data-ttu-id="af4bd-171">Określ liczbę grupy w ramach planu odzyskiwania, po uruchomieniu planu</span><span class="sxs-lookup"><span data-stu-id="af4bd-171">Identify the group number within the recovery plan when the plan is running</span></span> |
| <span data-ttu-id="af4bd-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="af4bd-172">VmMap</span></span> |<span data-ttu-id="af4bd-173">Tablica wszystkich maszyn wirtualnych w grupie</span><span class="sxs-lookup"><span data-stu-id="af4bd-173">Array of all the virtual machines in the group</span></span> |
| <span data-ttu-id="af4bd-174">Klucz VMMap</span><span class="sxs-lookup"><span data-stu-id="af4bd-174">VMMap key</span></span> |<span data-ttu-id="af4bd-175">Klucz unikatowy (identyfikator GUID) dla każdej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="af4bd-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="af4bd-176">Jest taki sam jak identyfikator maszyny wirtualnej VMM stosownych.</span><span class="sxs-lookup"><span data-stu-id="af4bd-176">It's the same as the VMM ID of the virtual machine where applicable.</span></span> |
| <span data-ttu-id="af4bd-177">RoleName</span><span class="sxs-lookup"><span data-stu-id="af4bd-177">RoleName</span></span> |<span data-ttu-id="af4bd-178">Nazwa maszyny Wirtualnej platformy Azure, która jest przywracana</span><span class="sxs-lookup"><span data-stu-id="af4bd-178">Name of the Azure VM that's being recovered</span></span> |
| <span data-ttu-id="af4bd-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="af4bd-179">CloudServiceName</span></span> |<span data-ttu-id="af4bd-180">Nazwa usługi w chmurze platformy Azure w której jest tworzony maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="af4bd-180">Azure Cloud Service name under which the virtual machine is created.</span></span> |

<span data-ttu-id="af4bd-181">Aby zidentyfikować klucza VmMap w kontekście można również przejść do strony właściwości maszyny Wirtualnej w usłudze ASR i przyjrzyj się właściwości GUID maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="af4bd-181">To identify the VmMap Key in the context you could also go to the VM properties page in ASR and look at the VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="af4bd-182">Tworzenie elementu runbook automatyzacji</span><span class="sxs-lookup"><span data-stu-id="af4bd-182">Author an Automation runbook</span></span>
<span data-ttu-id="af4bd-183">Teraz utworzyć element runbook, aby otworzyć port 80 na maszynie wirtualnej frontonu.</span><span class="sxs-lookup"><span data-stu-id="af4bd-183">Now create the runbook to open port 80 on the front-end virtual machine.</span></span>

1. <span data-ttu-id="af4bd-184">Utwórz nowy element runbook w ramach konta usługi Automatyzacja Azure o nazwie **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="af4bd-184">Create a new runbook in the Azure Automation account with the name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="af4bd-185">Przejdź do widoku autora elementu runbook, a następnie wprowadź trybie wersji roboczej.</span><span class="sxs-lookup"><span data-stu-id="af4bd-185">Navigate to the Author view of the runbook and enter the draft mode.</span></span>
3. <span data-ttu-id="af4bd-186">Najpierw określ zmienną, która ma być używana jako kontekst planu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="af4bd-186">First specify the variable to use as the recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="af4bd-187">Następnym połączeniu z subskrypcji przy użyciu nazwy poświadczeń i subskrypcji</span><span class="sxs-lookup"><span data-stu-id="af4bd-187">Next connect to the subscription using the credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect to Azure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="af4bd-188">Należy pamiętać, że używasz zasobów platformy Azure — **AzureCredential** i **AzureSubscriptionName** tutaj.</span><span class="sxs-lookup"><span data-stu-id="af4bd-188">Note that you use the Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="af4bd-189">Teraz określić szczegóły punktu końcowego i identyfikator GUID maszyny wirtualnej, dla którego chcesz udostępnić punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="af4bd-189">Now specify the endpoint details and the GUID of the virtual machine for which you want to expose the endpoint.</span></span> <span data-ttu-id="af4bd-190">W takim przypadku frontonu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="af4bd-190">In this case the front-end virtual machine.</span></span>

   ```
       # Specify the parameters to be used by the script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="af4bd-191">Określa protokół punktu końcowego platformy Azure, portów lokalnych na maszynie Wirtualnej i jej zamapowanych port publiczny.</span><span class="sxs-lookup"><span data-stu-id="af4bd-191">This specifies the Azure endpoint protocol, local port on the VM and its mapped public port.</span></span> <span data-ttu-id="af4bd-192">Te zmienne są parametry wymagane przez polecenia Azure, które dodania punktów końcowych do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="af4bd-192">These variables are parameters     required by the Azure commands that add endpoints to VMs.</span></span> <span data-ttu-id="af4bd-193">VMGUID przechowuje maszynę wirtualną, którą muszą działać na identyfikator GUID.</span><span class="sxs-lookup"><span data-stu-id="af4bd-193">The VMGUID holds the GUID of the virtual machine you need to operate on.</span></span>
6. <span data-ttu-id="af4bd-194">Skrypt teraz wyodrębnić kontekst dla podanego identyfikatora GUID maszyny Wirtualnej i utworzyć punktu końcowego na maszynie wirtualnej odwołuje się on.</span><span class="sxs-lookup"><span data-stu-id="af4bd-194">The script will now extract the context for the given VM GUID and create an endpoint on the virtual machine referenced by it.</span></span>

   ```
       #Read the VM GUID from the context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke the necessary pipeline commands to add a Azure Endpoint to a specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="af4bd-195">Po zakończeniu tej operacji, kliknij przycisk Publikuj ![](media/site-recovery-runbook-automation/20.png) umożliwia skrypt, aby był dostępny do wykonania.</span><span class="sxs-lookup"><span data-stu-id="af4bd-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) to allow your script to be available for execution.</span></span>

<span data-ttu-id="af4bd-196">Ukończ skrypt poniżej podano użytkownikowi</span><span class="sxs-lookup"><span data-stu-id="af4bd-196">The complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect to Azure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify the parameters to be used by the script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read the VM GUID from the context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke the necessary pipeline commands to add an Azure Endpoint to a specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-the-script-to-the-recovery-plan"></a><span data-ttu-id="af4bd-197">Dodaj skrypt do planu odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="af4bd-197">Add the script to the recovery plan</span></span>
<span data-ttu-id="af4bd-198">Gdy skrypt jest gotowy, można dodać go do planu odzyskiwania, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="af4bd-198">Once the script is ready, you can add it to the recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="af4bd-199">W planie odzyskiwania, który został utworzony wybierz dodać skrypt po grupie 2.</span><span class="sxs-lookup"><span data-stu-id="af4bd-199">In the recovery plan you created, choose to add a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="af4bd-200">Określ nazwę skryptu.</span><span class="sxs-lookup"><span data-stu-id="af4bd-200">Specify a script name.</span></span> <span data-ttu-id="af4bd-201">Jest to po prostu przyjazną nazwę dla tego skryptu do projekcji w ramach planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="af4bd-201">This is just a friendly name for this script for showing within the Recovery plan.</span></span>
3. <span data-ttu-id="af4bd-202">W tryb failover do platformy Azure skryptu — wybierz nazwę konta usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="af4bd-202">In the failover to Azure script – Select the Azure Automation Account name.</span></span>
4. <span data-ttu-id="af4bd-203">W elementach Runbook Azure wybierz element runbook Twojego autorstwa.</span><span class="sxs-lookup"><span data-stu-id="af4bd-203">In the Azure Runbooks, select the runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="af4bd-204">Skrypty po stronie podstawowej</span><span class="sxs-lookup"><span data-stu-id="af4bd-204">Primary side scripts</span></span>
<span data-ttu-id="af4bd-205">Po przejściu w tryb failover na platformie Azure są wykonywane, można również wykonać skrypty po stronie głównej.</span><span class="sxs-lookup"><span data-stu-id="af4bd-205">When you are executing a failover to Azure, you can also choose to execute primary side scripts.</span></span> <span data-ttu-id="af4bd-206">Skrypty te zostanie uruchomiony na serwerze programu VMM w trybie failover.</span><span class="sxs-lookup"><span data-stu-id="af4bd-206">These scripts will run on the VMM server during failover.</span></span>
<span data-ttu-id="af4bd-207">Skrypty po stronie podstawowej są dostępne tylko w przypadku zamknięcia wstępne tylko i post etapy zamknięcia.</span><span class="sxs-lookup"><span data-stu-id="af4bd-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="af4bd-208">Jest tak, ponieważ w lokacji głównej jest zwykle niedostępne, gdy uderzenia awarii.</span><span class="sxs-lookup"><span data-stu-id="af4bd-208">This is because we expect the primary site to be typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="af4bd-209">Podczas nieplanowanego trybu failover tylko wtedy, gdy uczestnictwa w operacjach lokacji głównej, spróbuje uruchomić skrypty po stronie głównej.</span><span class="sxs-lookup"><span data-stu-id="af4bd-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt to run the primary side scripts.</span></span> <span data-ttu-id="af4bd-210">Jeśli nie są dostępne lub limit czasu, przejście w tryb failover będzie odzyskiwanie maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="af4bd-210">If they are not reachable or timeout, the failover will continue to recover the virtual machines.</span></span>
<span data-ttu-id="af4bd-211">Skrypty po stronie głównej dostępnych cofanie witryn VMware/fizyczna/funkcji Hyper-v bez programu VMM chronione na platformie Azure — podczas failover do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="af4bd-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected to Azure - while you failover to Azure.</span></span>
<span data-ttu-id="af4bd-212">Jednak gdy możesz powrotu po awarii z platformy Azure do środowiska lokalnego, skrypty po stronie głównej (elementów Runbook) może służyć do wszystkich miejsc docelowych oprócz VMware.</span><span class="sxs-lookup"><span data-stu-id="af4bd-212">However, when you failback from Azure to on-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-the-recovery-plan"></a><span data-ttu-id="af4bd-213">Testuj plan odzyskiwania</span><span class="sxs-lookup"><span data-stu-id="af4bd-213">Test the recovery plan</span></span>
<span data-ttu-id="af4bd-214">Po dodaniu elementu runbook do planu można zainicjować test trybu failover i zobaczyć ją w akcji.</span><span class="sxs-lookup"><span data-stu-id="af4bd-214">Once you have added the runbook to the plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="af4bd-215">Zalecane jest zawsze uruchomić testowy tryb failover do testowania aplikacji i planu odzyskiwania, aby upewnić się, że nie ma żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="af4bd-215">It is always recommended to run a test failover to test your application and the recovery plan to ensure that there are no errors.</span></span>

1. <span data-ttu-id="af4bd-216">Wybierz plan odzyskiwania i zainicjuj test trybu failover.</span><span class="sxs-lookup"><span data-stu-id="af4bd-216">Select the recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="af4bd-217">Podczas wykonywania planu widać, czy element runbook jest wykonywana za pomocą jego stan.</span><span class="sxs-lookup"><span data-stu-id="af4bd-217">During the plan execution, you can see whether the runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="af4bd-218">Stan wykonania szczegółowe elementu runbook można również sprawdzić na stronie zadań usługi Automatyzacja Azure dla elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="af4bd-218">You can also see the detailed runbook execution status on the Azure Automation jobs page for the runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="af4bd-219">Po zakończeniu trybu failover, w wyniku wykonania elementu runbook, z wyjątkiem widoczny czy wykonywanie zakończy się pomyślnie lub nie, odwiedzając stronę maszyny wirtualnej platformy Azure i patrzeć punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="af4bd-219">After the failover completes, apart from the runbook execution result, you can see whether the execution is successful or not by visiting the Azure virtual machine page and looking at the endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="af4bd-220">Przykładowe skrypty</span><span class="sxs-lookup"><span data-stu-id="af4bd-220">Sample scripts</span></span>
<span data-ttu-id="af4bd-221">Podczas Rezygnacja za pomocą automatyzacji jedną powszechnie używane zadania dodawania punktu końcowego na maszynie wirtualnej platformy Azure, w tym samouczku, może wykonać szereg inne zadania automatyzacji zaawansowanych przy użyciu automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="af4bd-221">While we walked through automating one commonly used task of adding an endpoint to an Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="af4bd-222">Firma Microsoft i społecznością usługi Automatyzacja Azure znajdują się przykładowe elementy runbook, które mogą pomóc rozpocząć tworzenie własnych rozwiązań i narzędzie elementów runbook, którego można użyć jako bloków konstrukcyjnych dla większych automatyzacji zadań.</span><span class="sxs-lookup"><span data-stu-id="af4bd-222">Microsoft and the Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="af4bd-223">Rozpocznij korzystanie z nich z galerii i tworzenie planów odzyskiwania jednym kliknięciem zaawansowanych aplikacji przy użyciu usługi Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="af4bd-223">Start using them from the gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="af4bd-224">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="af4bd-224">Additional Resources</span></span>
[<span data-ttu-id="af4bd-225">Przegląd automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="af4bd-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Omówienie usługi Automatyzacja Azure")

[<span data-ttu-id="af4bd-226">Przykładowe skrypty usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="af4bd-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "przykładowe skrypty usługi Automatyzacja Azure")
