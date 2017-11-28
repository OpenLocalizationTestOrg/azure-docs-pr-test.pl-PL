---
title: aaaConfigure Azure konto Uruchom jako dla | Dokumentacja firmy Microsoft
description: "Ten samouczek przedstawia hello tworzenie, testowanie i przykład uwierzytelnianie przy użyciu podmiotu zabezpieczeń w automatyzacji Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: "nazwa główna usługi, setspn, uwierzytelnianie azure"
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="60bbb-104">Uwierzytelnianie elementów runbook przy użyciu konta Uruchom jako platformy Azure</span><span class="sxs-lookup"><span data-stu-id="60bbb-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="60bbb-105">W tym artykule opisano, jak konto tooconfigure usługi Automatyzacja Azure hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="60bbb-105">This article shows you how tooconfigure an Azure Automation account in hello Azure portal.</span></span> <span data-ttu-id="60bbb-106">toodo tak, hello Uruchom jako konta funkcji tooauthenticate elementy runbook służą zarządzania zasobami Azure Resource Manager lub zarządzania usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="60bbb-106">toodo so, you use hello Run As account feature tooauthenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="60bbb-107">Podczas tworzenia konta automatyzacji w portalu Azure hello, można automatycznie utworzyć dwa konta:</span><span class="sxs-lookup"><span data-stu-id="60bbb-107">When you create an Automation account in hello Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="60bbb-108">Konto Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="60bbb-108">A Run As account.</span></span> <span data-ttu-id="60bbb-109">To konto służy do tworzenia nazwy głównej usługi w usłudze Azure Active Directory (Azure AD) oraz certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="60bbb-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="60bbb-110">Przypisuje hello współautora opartej na rolach kontroli dostępu (RBAC), która zarządza zasoby usługi Resource Manager za pomocą elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="60bbb-110">It also assigns hello Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="60bbb-111">Klasyczne konto Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="60bbb-111">A Classic Run As account.</span></span> <span data-ttu-id="60bbb-112">To konto przekazywanie certyfikatu zarządzania, który jest używany toomanage zarządzania usługami lub zasoby klasyczne za pomocą elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="60bbb-112">This account uploads a management certificate, which is used toomanage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="60bbb-113">Tworzenie konta upraszcza proces hello i pomaga szybko rozpocząć tworzenie i wdrażanie toosupport elementów runbook usługi Automatyzacja z automatyzacji musi.</span><span class="sxs-lookup"><span data-stu-id="60bbb-113">Creating an Automation account simplifies hello process for you and helps you quickly start building and deploying runbooks toosupport your automation needs.</span></span>

<span data-ttu-id="60bbb-114">Używając konta Uruchom jako i klasycznego konta Uruchom jako, możesz:</span><span class="sxs-lookup"><span data-stu-id="60bbb-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="60bbb-115">Podaj tooauthenticate sposób Zestandaryzowany z usługi Azure Resource Manager lub usługi zarządzania zasobami w przypadku zarządzania z poziomu elementów runbook w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="60bbb-115">Provide a standardized way tooauthenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in hello Azure portal.</span></span>
* <span data-ttu-id="60bbb-116">Użyj hello globalne elementy runbook, które można skonfigurować w alertach Azure do automatyzacji procesu.</span><span class="sxs-lookup"><span data-stu-id="60bbb-116">Automate hello use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="60bbb-117">Witaj [Azure alertu funkcji integracji](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) automatyzacji elementów runbook globalnego wymaga konto automatyzacji, który skonfigurowano konto Uruchom jako i konto klasycznego Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="60bbb-117">hello [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="60bbb-118">Można wybrać konto automatyzacji, który został już zdefiniowany konta Uruchom jako i klasycznego Uruchom jako lub toocreate można wybrać nowe konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="60bbb-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose toocreate a new Automation account.</span></span>
>  

<span data-ttu-id="60bbb-119">W tym artykule przedstawiono sposób toocreate konto usługi Automatyzacja z hello portalu Azure, zaktualizuj konto automatyzacji za pomocą programu Azure PowerShell, zarządzanie konfiguracją konta hello i uwierzytelnić się w elementach runbook.</span><span class="sxs-lookup"><span data-stu-id="60bbb-119">This article shows how toocreate an Automation account from hello Azure portal, update an Automation account by using Azure PowerShell, manage hello account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="60bbb-120">Przed rozpoczęciem tworzenia konta automatyzacji jest toounderstand dobrze i należy wziąć pod uwagę następujące hello:</span><span class="sxs-lookup"><span data-stu-id="60bbb-120">Before you begin creating an Automation account, it's a good idea toounderstand and consider hello following:</span></span>

* <span data-ttu-id="60bbb-121">Tworzenie konta automatyzacji nie ma wpływu na kont automatyzacji, który może zostały już utworzone w klasycznym hello lub modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="60bbb-121">Creating an Automation account does not affect Automation accounts you might have already created in either hello classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="60bbb-122">proces Hello działa tylko w przypadku kont automatyzacji, tworzone w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="60bbb-122">hello process works only for Automation accounts that you create in hello Azure portal.</span></span> <span data-ttu-id="60bbb-123">Próba toocreate konta z hello klasycznego portalu Azure nie jest replikowany hello Konfiguracja Uruchom jako konta.</span><span class="sxs-lookup"><span data-stu-id="60bbb-123">Attempting toocreate an account from hello Azure classic portal does not replicate hello Run As account configuration.</span></span>
* <span data-ttu-id="60bbb-124">Jeśli masz już elementy runbook i zasoby (na przykład harmonogramy lub zmienne) w zasoby klasyczne toomanage miejsca, i chcesz tooauthenticate elementów runbook z hello nowego klasycznego konta Uruchom jako, wykonaj jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="60bbb-124">If you already have runbooks and assets (such as schedules or variables) in place toomanage classic resources, and you want runbooks tooauthenticate with hello new Classic Run As account, do either of hello following:</span></span>

  * <span data-ttu-id="60bbb-125">toocreate klasycznego konta Uruchom jako, wykonaj instrukcje hello w sekcji "Zarządzanie Twoje konto Uruchom jako" hello.</span><span class="sxs-lookup"><span data-stu-id="60bbb-125">toocreate a Classic Run As account, follow hello instructions in hello "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="60bbb-126">tooupdate istniejącego konta, użyj hello PowerShell skryptu w sekcji "Aktualizuj Twoje konto usługi Automatyzacja przy użyciu programu PowerShell" hello.</span><span class="sxs-lookup"><span data-stu-id="60bbb-126">tooupdate your existing account, use hello PowerShell script in hello "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="60bbb-127">tooauthenticate przy użyciu hello nowego konta Uruchom jako i konto klasycznego Uruchom jako automatyzacji, należy toomodify istniejące elementy runbook z hello przykładowy kod podany w sekcji hello [przykłady kodu uwierzytelniania](#authentication-code-examples).</span><span class="sxs-lookup"><span data-stu-id="60bbb-127">tooauthenticate by using hello new Run As account and Classic Run As Automation account, you  need toomodify your existing runbooks with hello example code provided in hello section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="60bbb-128">Hello konta Uruchom jako jest uwierzytelniania przy użyciu nazwy głównej usługi oparte na certyfikatach hello zasoby usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="60bbb-128">hello Run As account is for authentication against Resource Manager resources using hello certificate-based service principal.</span></span> <span data-ttu-id="60bbb-129">Witaj konto klasycznego Uruchom jako jest do uwierzytelniania względem zasobów usługi zarządzania z certyfikatem zarządzania.</span><span class="sxs-lookup"><span data-stu-id="60bbb-129">hello Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-hello-azure-portal"></a><span data-ttu-id="60bbb-130">Utwórz konto automatyzacji z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="60bbb-130">Create an Automation account from hello Azure portal</span></span>
<span data-ttu-id="60bbb-131">W tej sekcji utworzysz konto usługi Automatyzacja Azure z hello portalu Azure, który z kolei tworzy zarówno konto Uruchom jako, jak i konto klasycznego Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="60bbb-131">In this section, you create an Azure Automation account from hello Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="60bbb-132">toocreate konto usługi Automatyzacja, musi być członkiem roli Administratorzy usługi hello lub współadministratorem subskrypcji hello, która udziela dostępu toohello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="60bbb-132">toocreate an Automation account, you must be a member of hello Service Admins role or co-administrator of hello subscription that is granting access toohello subscription.</span></span> <span data-ttu-id="60bbb-133">Należy również dodać jako subskrypcji toothat użytkownika domyślnego wystąpienia usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="60bbb-133">You must also be added as a user toothat subscription's default Active Directory instance.</span></span> <span data-ttu-id="60bbb-134">konta Hello toobe przypisane do ról uprzywilejowanych nie jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="60bbb-134">hello account does not need toobe assigned a privileged role.</span></span>
>
><span data-ttu-id="60bbb-135">Jeśli nie jesteś członkiem wystąpienia usługi Active Directory hello subskrypcji przed dodaniem roli administratora współpracującego toohello hello subskrypcji, użytkownik zostanie dodany tooActive katalogu jako Gość.</span><span class="sxs-lookup"><span data-stu-id="60bbb-135">If you are not a member of hello subscription’s Active Directory instance before you are added toohello co-administrator role of hello subscription, you will be added tooActive Directory as a guest.</span></span> <span data-ttu-id="60bbb-136">W takim przypadku otrzymasz "nie ma uprawnień toocreate..."</span><span class="sxs-lookup"><span data-stu-id="60bbb-136">In this instance, you will receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="60bbb-137">Ostrzeżenie dotyczące hello **Dodaj konto automatyzacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="60bbb-137">warning on hello **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="60bbb-138">Użytkownicy, którzy dodano rolę administratora współpracującego toohello najpierw można usunąć z wystąpienia usługi Active Directory hello subskrypcji i ponownie dodany toomake ich pełną użytkownika w usłudze Active Directory.</span><span class="sxs-lookup"><span data-stu-id="60bbb-138">Users who were added toohello co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="60bbb-139">tooverify tej sytuacji z hello **usługi Azure Active Directory** okienku w portalu Azure, wybierając hello **użytkowników i grup**, wybierając żądane **wszyscy użytkownicy** i po wybraniu Witaj określonego użytkownika, wybierając **profilu**.</span><span class="sxs-lookup"><span data-stu-id="60bbb-139">tooverify this situation from hello **Azure Active Directory** pane in hello Azure portal by selecting **Users and groups**, selecting **All users** and, after you select hello specific user, selecting **Profile**.</span></span> <span data-ttu-id="60bbb-140">Witaj wartość hello **typ użytkownika** atrybutu na liście profilów użytkowników hello nie powinna być równa **gościa**.</span><span class="sxs-lookup"><span data-stu-id="60bbb-140">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="60bbb-141">Zaloguj się w portalu Azure przy użyciu konta, które jest członkiem grupy administratorów subskrypcji hello i współadministratorem subskrypcji hello toohello.</span><span class="sxs-lookup"><span data-stu-id="60bbb-141">Sign in toohello Azure portal with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>

2. <span data-ttu-id="60bbb-142">Wybierz opcję **Konta automatyzacji**.</span><span class="sxs-lookup"><span data-stu-id="60bbb-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="60bbb-143">Na powitania **kont automatyzacji** bloku, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="60bbb-143">On hello **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="60bbb-144">Witaj **Dodaj konto automatyzacji** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="60bbb-144">hello **Add Automation Account** blade opens.</span></span>

 ![Blok "Dodaj konto automatyzacji" Hello](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="60bbb-146">Jeśli Twoje konto nie jest członkiem roli Administratorzy subskrypcji hello i współadministratorem subskrypcji hello, hello następujące ostrzeżenie jest wyświetlane na powitania **Dodaj konto automatyzacji** bloku:</span><span class="sxs-lookup"><span data-stu-id="60bbb-146">If your account is not a member of hello subscription administrators role and co-administrator of hello subscription, hello following warning is displayed on hello **Add Automation Account** blade:</span></span>
   >
   >![Ostrzeżenie podczas dodawania konta usługi Automation](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="60bbb-148">Na powitania **Dodaj konto automatyzacji** bloku w hello **nazwa** wpisz nazwę nowego konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="60bbb-148">On hello **Add Automation Account** blade, in hello **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="60bbb-149">Jeśli masz więcej niż jedną subskrypcję, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="60bbb-149">If you have more than one subscription, do hello following:</span></span>

    <span data-ttu-id="60bbb-150">a.</span><span class="sxs-lookup"><span data-stu-id="60bbb-150">a.</span></span> <span data-ttu-id="60bbb-151">W obszarze **subskrypcji**, określ jedną hello nowego konta.</span><span class="sxs-lookup"><span data-stu-id="60bbb-151">Under **Subscription**, specify one for hello new account.</span></span>

    <span data-ttu-id="60bbb-152">b.</span><span class="sxs-lookup"><span data-stu-id="60bbb-152">b.</span></span> <span data-ttu-id="60bbb-153">W obszarze **Grupa zasobów** kliknij pozycję **Utwórz nową** lub **Użyj istniejącej**.</span><span class="sxs-lookup"><span data-stu-id="60bbb-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="60bbb-154">c.</span><span class="sxs-lookup"><span data-stu-id="60bbb-154">c.</span></span> <span data-ttu-id="60bbb-155">W obszarze **Lokalizacja** określ centrum danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="60bbb-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="60bbb-156">W obszarze **Tworzenie konta Uruchom jako platformy Azure** wybierz pozycję **Tak**, a następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="60bbb-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="60bbb-157">Jeśli wybierzesz nie toocreate hello konta Uruchom jako, wybierając **nr**, zostanie wyświetlony komunikat ostrzegawczy hello **Dodaj konto automatyzacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="60bbb-157">If you choose not toocreate hello Run As account by selecting **No**, a warning message is displayed hello **Add Automation Account** blade.</span></span> <span data-ttu-id="60bbb-158">Mimo że hello konto jest tworzone w portalu Azure hello, nie ma odpowiedniego tożsamość uwierzytelniania w ramach Twojej classic lub usługa katalogowa subskrypcji Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="60bbb-158">Although hello account is created in hello Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="60bbb-159">W rezultacie hello konto ma nie tooresources dostępu w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="60bbb-159">Consequently, hello account has no access tooresources in your subscription.</span></span> <span data-ttu-id="60bbb-160">Ten scenariusz zapobiega sytuacji, w której wszelkie elementy runbook odwołujące się do tego konta miałyby możliwość uwierzytelniania i wykonywania zadań w odniesieniu do zasobów w tych modelach wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="60bbb-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > ![Komunikat ostrzegawczy w bloku "Dodaj konto automatyzacji" hello](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="60bbb-162">Ponadto ponieważ hello nazwy głównej usługi nie jest tworzony, nie jest przypisana rola współautora hello.</span><span class="sxs-lookup"><span data-stu-id="60bbb-162">Additionally, because hello service principal is not created, hello Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="60bbb-163">Gdy Azure tworzy konto automatyzacji hello, możesz śledzić postępy hello w obszarze **powiadomienia** hello menu.</span><span class="sxs-lookup"><span data-stu-id="60bbb-163">While Azure creates hello Automation account, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="resources"></a><span data-ttu-id="60bbb-164">Zasoby</span><span class="sxs-lookup"><span data-stu-id="60bbb-164">Resources</span></span>
<span data-ttu-id="60bbb-165">Po pomyślnym utworzeniu konta automatyzacji hello kilka zasoby są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="60bbb-165">When hello Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="60bbb-166">zasoby Hello podsumowano w hello następujących tabel:</span><span class="sxs-lookup"><span data-stu-id="60bbb-166">hello resources are summarized in hello following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="60bbb-167">Zasoby konta Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="60bbb-167">Run As account resources</span></span>

| <span data-ttu-id="60bbb-168">Zasób</span><span class="sxs-lookup"><span data-stu-id="60bbb-168">Resource</span></span> | <span data-ttu-id="60bbb-169">Opis</span><span class="sxs-lookup"><span data-stu-id="60bbb-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="60bbb-170">AzureAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="60bbb-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="60bbb-171">Przykład graficzny element runbook, który demonstruje sposób tooauthenticate przy użyciu hello konta Uruchom jako i pobiera wszystkie zasoby usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="60bbb-171">An example graphical runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="60bbb-172">AzureAutomationTutorialScript Runbook</span><span class="sxs-lookup"><span data-stu-id="60bbb-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="60bbb-173">Runbook programu PowerShell przykładzie pokazano, jak tooauthenticate przy użyciu hello konta Uruchom jako, który pobiera wszystkie zasoby usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="60bbb-173">An example PowerShell runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="60bbb-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="60bbb-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="60bbb-175">zasób certyfikatu Hello jest tworzony automatycznie podczas tworzenia konta automatyzacji lub użyj następującego skryptu PowerShell do istniejącego konta hello.</span><span class="sxs-lookup"><span data-stu-id="60bbb-175">hello certificate asset that's automatically created when you create an Automation account or use hello following PowerShell script for an existing account.</span></span> <span data-ttu-id="60bbb-176">Hello certyfikatu umożliwia tooauthenticate z platformy Azure, dzięki czemu zasoby usługi Azure Resource Manager można zarządzać z poziomu elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="60bbb-176">hello certificate allows you tooauthenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="60bbb-177">Witaj certyfikat ma żywotność jednego roku.</span><span class="sxs-lookup"><span data-stu-id="60bbb-177">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="60bbb-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="60bbb-178">AzureRunAsConnection</span></span> | <span data-ttu-id="60bbb-179">zasób połączenia Hello jest tworzony automatycznie podczas tworzenia konta automatyzacji lub użyj skryptu programu PowerShell hello do istniejącego konta.</span><span class="sxs-lookup"><span data-stu-id="60bbb-179">hello connection asset that's automatically created when you create an Automation account or use hello PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="60bbb-180">Zasoby klasycznego konta Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="60bbb-180">Classic Run As account resources</span></span>

| <span data-ttu-id="60bbb-181">Zasób</span><span class="sxs-lookup"><span data-stu-id="60bbb-181">Resource</span></span> | <span data-ttu-id="60bbb-182">Opis</span><span class="sxs-lookup"><span data-stu-id="60bbb-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="60bbb-183">AzureClassicAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="60bbb-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="60bbb-184">Przykład graficzny element runbook, który pobiera wszystkich maszyn wirtualnych hello, które są tworzone przy użyciu hello klasycznego modelu wdrażania w ramach subskrypcji przy użyciu konta hello klasycznego Uruchom jako (certyfikatów), a następnie zapisuje hello nazwę maszyny Wirtualnej i stanu.</span><span class="sxs-lookup"><span data-stu-id="60bbb-184">An example graphical runbook that gets all hello VMs that are created using hello classic deployment model in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="60bbb-185">AzureClassicAutomationTutorial Script Runbook</span><span class="sxs-lookup"><span data-stu-id="60bbb-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="60bbb-186">Przykład runbook programu PowerShell, która pobiera wszystkie hello klasycznych maszyn wirtualnych w ramach subskrypcji przy użyciu konta hello klasycznego Uruchom jako (certyfikatów), a następnie zapisuje hello nazwę maszyny Wirtualnej i stanu.</span><span class="sxs-lookup"><span data-stu-id="60bbb-186">An example PowerShell runbook that gets all hello classic VMs in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="60bbb-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="60bbb-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="60bbb-188">Witaj, automatycznie tworzony zasób certyfikatu Użyj tooauthenticate z platformy Azure, dzięki czemu można zarządzać Azure zasoby klasyczne z elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="60bbb-188">hello automatically created certificate asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="60bbb-189">Witaj certyfikat ma żywotność jednego roku.</span><span class="sxs-lookup"><span data-stu-id="60bbb-189">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="60bbb-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="60bbb-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="60bbb-191">trwały Hello automatycznie utworzone połączenie, użyj tooauthenticate z platformy Azure, dzięki czemu można zarządzać Azure zasoby klasyczne z elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="60bbb-191">hello automatically created connection asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="60bbb-192">Sprawdzanie uwierzytelniania Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="60bbb-192">Verify Run As authentication</span></span>
<span data-ttu-id="60bbb-193">Wykonaj tooconfirm teście małych, który może pomyślnie wykonać uwierzytelnienia za pomocą hello nowego konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="60bbb-193">Perform a small test tooconfirm that you can successfully authenticate by using hello new Run As account.</span></span>

1. <span data-ttu-id="60bbb-194">Hello portalu Azure Otwórz konto automatyzacji hello, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="60bbb-194">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="60bbb-195">Kliknij przycisk hello **elementów Runbook** kafelka tooopen hello listy elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="60bbb-195">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="60bbb-196">Wybierz hello **AzureAutomationTutorialScript** runbook, a następnie kliknij przycisk **Start** toostart hello runbook.</span><span class="sxs-lookup"><span data-stu-id="60bbb-196">Select hello **AzureAutomationTutorialScript** runbook, and then click **Start** toostart hello runbook.</span></span> <span data-ttu-id="60bbb-197">wykonywane Hello następujące zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="60bbb-197">hello following events occur:</span></span>
 * <span data-ttu-id="60bbb-198">A [zadanie elementu runbook](automation-runbook-execution.md) utworzeniu hello **zadania** zostanie wyświetlony blok i stan zadania hello jest wyświetlany w hello **Podsumowanie zadania** kafelka.</span><span class="sxs-lookup"><span data-stu-id="60bbb-198">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="60bbb-199">Stan zadania Hello początkowo **w kolejce**, wskazujący, że oczekuje na proces roboczy elementu runbook, w toobecome chmury hello dostępne.</span><span class="sxs-lookup"><span data-stu-id="60bbb-199">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="60bbb-200">Stan Hello staje się **uruchamianie** gdy pracownik oświadczeń hello zadania.</span><span class="sxs-lookup"><span data-stu-id="60bbb-200">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="60bbb-201">Stan Hello staje się **systemem** , gdy element runbook hello zacznie działać.</span><span class="sxs-lookup"><span data-stu-id="60bbb-201">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="60bbb-202">Gdy zadanie elementu runbook hello zakończył działanie, powinien zostać wyświetlony stan **Ukończono**.</span><span class="sxs-lookup"><span data-stu-id="60bbb-202">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="60bbb-203">toosee hello szczegółowe wyniki hello elementu runbook, kliknij przycisk hello **dane wyjściowe** kafelka.</span><span class="sxs-lookup"><span data-stu-id="60bbb-203">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="60bbb-204">Witaj **dane wyjściowe** bloku zostanie wyświetlone hello elementu runbook pomyślnie uwierzytelniony i zwrócona lista wszystkich dostępnych w grupie zasobów hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="60bbb-204">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all resources available in hello resource group.</span></span>

5. <span data-ttu-id="60bbb-205">Zamknij hello **dane wyjściowe** toohello tooreturn bloku **Podsumowanie zadania** bloku.</span><span class="sxs-lookup"><span data-stu-id="60bbb-205">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="60bbb-206">Zamknij hello **Podsumowanie zadania** bloku i hello odpowiadającego **AzureAutomationTutorialScript** bloku elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="60bbb-206">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="60bbb-207">Sprawdzanie klasycznego uwierzytelniania Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="60bbb-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="60bbb-208">Wykonaj podobne małą test tooconfirm, który może pomyślnie wykonać uwierzytelnienia za pomocą hello nowego klasycznego konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="60bbb-208">Perform a similar small test tooconfirm that you can successfully authenticate by using hello new Classic Run As account.</span></span>

1. <span data-ttu-id="60bbb-209">Hello portalu Azure Otwórz konto automatyzacji hello, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="60bbb-209">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="60bbb-210">Kliknij przycisk hello **elementów Runbook** kafelka tooopen hello listy elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="60bbb-210">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="60bbb-211">Wybierz hello **AzureClassicAutomationTutorialScript** elementu runbook, a następnie kliknij przycisk **Start** zbyt uruchomić elementu runbook hello.</span><span class="sxs-lookup"><span data-stu-id="60bbb-211">Select hello **AzureClassicAutomationTutorialScript** runbook, and then click **Start** too start hello runbook.</span></span> <span data-ttu-id="60bbb-212">wykonywane Hello następujące zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="60bbb-212">hello following events occur:</span></span>

 * <span data-ttu-id="60bbb-213">A [zadanie elementu runbook](automation-runbook-execution.md) utworzeniu hello **zadania** zostanie wyświetlony blok i stan zadania hello jest wyświetlany w hello **Podsumowanie zadania** kafelka.</span><span class="sxs-lookup"><span data-stu-id="60bbb-213">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="60bbb-214">Stan zadania Hello początkowo **w kolejce**, wskazujący, że oczekuje na proces roboczy elementu runbook, w toobecome chmury hello dostępne.</span><span class="sxs-lookup"><span data-stu-id="60bbb-214">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="60bbb-215">Stan Hello staje się **uruchamianie** gdy pracownik oświadczeń hello zadania.</span><span class="sxs-lookup"><span data-stu-id="60bbb-215">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="60bbb-216">Stan Hello staje się **systemem** , gdy element runbook hello zacznie działać.</span><span class="sxs-lookup"><span data-stu-id="60bbb-216">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="60bbb-217">Gdy zadanie elementu runbook hello zakończył działanie, powinien zostać wyświetlony stan **Ukończono**.</span><span class="sxs-lookup"><span data-stu-id="60bbb-217">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![Test elementu Runbook zabezpieczeń](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="60bbb-219">toosee hello szczegółowe wyniki hello elementu runbook, kliknij przycisk hello **dane wyjściowe** kafelka.</span><span class="sxs-lookup"><span data-stu-id="60bbb-219">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="60bbb-220">Witaj **dane wyjściowe** bloku zostanie wyświetlone pomyślnie uwierzytelniony i zwracane listę wszystkich klasycznych maszyn wirtualnych w subskrypcji hello hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="60bbb-220">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all classic VMs in hello subscription.</span></span>

5. <span data-ttu-id="60bbb-221">Zamknij hello **dane wyjściowe** toohello tooreturn bloku **Podsumowanie zadania** bloku.</span><span class="sxs-lookup"><span data-stu-id="60bbb-221">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="60bbb-222">Zamknij hello **Podsumowanie zadania** bloku i hello odpowiadającego **AzureAutomationTutorialScript** bloku elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="60bbb-222">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="60bbb-223">Zarządzanie kontem Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="60bbb-223">Managing your Run As account</span></span>
<span data-ttu-id="60bbb-224">W pewnym momencie przed upływem Twoje konto usługi Automatyzacja, konieczne będzie toorenew hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="60bbb-224">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="60bbb-225">Jeśli uważasz, że naruszono tego hello konta Uruchom jako, można usunąć i ponownie go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="60bbb-225">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="60bbb-226">W tej sekcji omówiono sposób tooperform te operacje.</span><span class="sxs-lookup"><span data-stu-id="60bbb-226">This section discusses how tooperform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="60bbb-227">Odnawianie certyfikatu z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="60bbb-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="60bbb-228">Witaj podpisem utworzony certyfikat dla hello konta Uruchom jako wygasa rok z daty utworzenia hello.</span><span class="sxs-lookup"><span data-stu-id="60bbb-228">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="60bbb-229">Można go odnowić w dowolnym momencie przed wygaśnięciem jego ważności.</span><span class="sxs-lookup"><span data-stu-id="60bbb-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="60bbb-230">Podczas odnawiania go hello bieżącego prawidłowy certyfikat jest zachowanych tooensure, że wszystkie elementy runbook umieszczonych w kolejce maksymalnie lub aktywnie działa i że uwierzytelniania za pomocą hello konta Uruchom jako nie negatywnie zainfekowane.</span><span class="sxs-lookup"><span data-stu-id="60bbb-230">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="60bbb-231">certyfikat Hello pozostaje ważny aż do daty jego wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="60bbb-231">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="60bbb-232">Jeśli zostały skonfigurowane z automatyzacji Uruchom jako konta toouse certyfikat wystawiony przez urząd certyfikacji w Twojej organizacji, możesz użyć tej opcji hello firmowy certyfikat zostanie zastąpione przez certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="60bbb-232">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="60bbb-233">Witaj toorenew certyfikatów, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="60bbb-233">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="60bbb-234">Hello portalu Azure Otwórz hello konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="60bbb-234">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="60bbb-235">Na powitania **konto automatyzacji** bloku w hello **konta właściwości** okienku w obszarze **ustawienia konta**, wybierz pozycję **konta Uruchom jako**.</span><span class="sxs-lookup"><span data-stu-id="60bbb-235">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Okienko właściwości konta usługi Automation](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="60bbb-237">Na powitania **konta Uruchom jako** bloku właściwości, wybierz albo hello Uruchom jako konta lub hello klasycznego konto Uruchom jako ma toorenew hello certyfikat dla.</span><span class="sxs-lookup"><span data-stu-id="60bbb-237">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="60bbb-238">Na powitania **właściwości** bloku hello wybranego konta, kliknij przycisk **odnawiania certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="60bbb-238">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![Odnawianie certyfikatu konta Uruchom jako](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="60bbb-240">Gdy hello certyfikat zostanie odnowiony, możesz śledzić postępy hello w obszarze **powiadomienia** hello menu.</span><span class="sxs-lookup"><span data-stu-id="60bbb-240">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="60bbb-241">Usuwanie konta Uruchom jako lub klasycznego konta Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="60bbb-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="60bbb-242">W tej sekcji opisano sposób toodelete i ponownie utwórz konto Uruchom jako lub klasycznego Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="60bbb-242">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="60bbb-243">Podczas wykonywania tej akcji jest zachowywana hello konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="60bbb-243">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="60bbb-244">Po usunięciu konta Uruchom jako lub klasycznego Uruchom jako, można go utworzyć ponownie w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="60bbb-244">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="60bbb-245">Hello portalu Azure Otwórz hello konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="60bbb-245">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="60bbb-246">Na powitania **konto automatyzacji** bloku w hello konta w okienku właściwości, wybierz opcję **konta Uruchom jako**.</span><span class="sxs-lookup"><span data-stu-id="60bbb-246">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="60bbb-247">Na powitania **konta Uruchom jako** bloku właściwości, albo hello Uruchom jako konto klasycznego konto Uruchom jako lub wybierz konto, które mają toodelete.</span><span class="sxs-lookup"><span data-stu-id="60bbb-247">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="60bbb-248">Następnie na powitania **właściwości** bloku hello wybranego konta, kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="60bbb-248">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![Usuwanie konta Uruchom jako](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="60bbb-250">Gdy konto hello jest usuwany, możesz śledzić postępy hello w obszarze **powiadomienia** hello menu.</span><span class="sxs-lookup"><span data-stu-id="60bbb-250">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="60bbb-251">Po usunięciu konta hello, można go ponownie utworzyć na powitania **konta Uruchom jako** opcja tworzenia bloku właściwości, wybierając hello **Azure konta Uruchom jako**.</span><span class="sxs-lookup"><span data-stu-id="60bbb-251">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Ponownie utwórz konto Uruchom jako automatyzacji hello](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="60bbb-253">Błąd konfiguracji</span><span class="sxs-lookup"><span data-stu-id="60bbb-253">Misconfiguration</span></span>
<span data-ttu-id="60bbb-254">Niektóre elementy konfiguracji niezbędne do toofunction konta Uruchom jako klasycznego konto Uruchom jako lub hello prawidłowo może zostały usunięte lub nieprawidłowo utworzone podczas instalacji początkowej.</span><span class="sxs-lookup"><span data-stu-id="60bbb-254">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="60bbb-255">elementy Hello obejmują:</span><span class="sxs-lookup"><span data-stu-id="60bbb-255">hello items include:</span></span>

* <span data-ttu-id="60bbb-256">Zasób certyfikatu</span><span class="sxs-lookup"><span data-stu-id="60bbb-256">Certificate asset</span></span>
* <span data-ttu-id="60bbb-257">Zasób połączenia</span><span class="sxs-lookup"><span data-stu-id="60bbb-257">Connection asset</span></span>
* <span data-ttu-id="60bbb-258">Konto Uruchom jako zostało usunięte z hello roli współautora</span><span class="sxs-lookup"><span data-stu-id="60bbb-258">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="60bbb-259">Nazwa główna usługi lub aplikacji w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="60bbb-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="60bbb-260">W poprzednim hello i inne wystąpienia błędnej konfiguracji hello konta automatyzacji wykrywa hello zmiany i ma stan *niepełnym* na powitania **konta Uruchom jako** bloku właściwości hello konto.</span><span class="sxs-lookup"><span data-stu-id="60bbb-260">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![Stan Niekompletne dla konfiguracji konta Uruchom jako](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="60bbb-262">Po wybraniu konta Uruchom jako hello hello konta **właściwości** okienko zawierające hello następujący komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="60bbb-262">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![Komunikat ostrzegawczy Niekompletne dla konfiguracji konta Uruchom jako](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="60bbb-264">.</span><span class="sxs-lookup"><span data-stu-id="60bbb-264">.</span></span>

<span data-ttu-id="60bbb-265">Przez usunięcie i ponowne utworzenie konta hello można szybko rozwiązać te problemy Uruchom jako konta.</span><span class="sxs-lookup"><span data-stu-id="60bbb-265">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="60bbb-266">Aktualizacja konta usługi Automation przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="60bbb-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="60bbb-267">Możesz za pomocą programu PowerShell tooupdate istniejącego konta automatyzacji:</span><span class="sxs-lookup"><span data-stu-id="60bbb-267">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="60bbb-268">Utwórz konto usługi Automatyzacja, ale odrzucić konta Uruchom jako hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="60bbb-268">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="60bbb-269">Zasoby usługi Resource Manager toomanage konto automatyzacji jest już używana, i chcesz tooupdate hello konta tooinclude hello konta Uruchom jako dla uwierzytelniania elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="60bbb-269">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="60bbb-270">Używasz toomanage konta automatyzacji dla zasoby klasyczne i chcesz tooupdate go hello toouse konta w klasycznym Uruchom jako, zamiast tworzenia nowego konta i migrację z tooit elementy runbook i zasoby.</span><span class="sxs-lookup"><span data-stu-id="60bbb-270">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="60bbb-271">Ma toocreate Uruchom jako, a konto klasycznego Uruchom jako za pomocą certyfikatu wystawionego przez urząd certyfikacji (CA) przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="60bbb-271">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="60bbb-272">skrypt Hello ma hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="60bbb-272">hello script has hello following prerequisites:</span></span>

* <span data-ttu-id="60bbb-273">skrypt Hello można uruchomić tylko w systemie Windows 10 i Windows Server 2016 z modułami usługi Azure Resource Manager 2.01 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="60bbb-273">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="60bbb-274">Nie jest obsługiwany przez wcześniejsze wersje systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="60bbb-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="60bbb-275">Program Azure PowerShell 1.0 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="60bbb-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="60bbb-276">Aby uzyskać informacje o wersji hello PowerShell 1.0, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="60bbb-276">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="60bbb-277">Konto automatyzacji, który jest określany jako wartość hello hello *— AutomationAccountName* i *- ApplicationDisplayName* parametrów w hello następującego skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60bbb-277">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="60bbb-278">wartości tooget hello *SubscriptionID*, *ResourceGroup*, i *AutomationAccountName*, które są wymagane parametry hello skryptów, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="60bbb-278">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="60bbb-279">W hello portalu Azure, wybierz konto Automatyzacja na powitania **konto automatyzacji** bloku, a następnie wybierz **wszystkie ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="60bbb-279">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="60bbb-280">Na powitania **wszystkie ustawienia** bloku, w obszarze **ustawienia konta**, wybierz pozycję **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="60bbb-280">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="60bbb-281">Należy pamiętać, wartości hello na powitania **właściwości** bloku.</span><span class="sxs-lookup"><span data-stu-id="60bbb-281">Note hello values on hello **Properties** blade.</span></span>

![Blok "Właściwości" konto automatyzacji Hello](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="60bbb-283">Tworzenie skryptu programu PowerShell konta Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="60bbb-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="60bbb-284">Ten skrypt programu PowerShell obejmuje obsługę hello następujące konfiguracje:</span><span class="sxs-lookup"><span data-stu-id="60bbb-284">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="60bbb-285">Tworzenie konta Uruchom jako przy użyciu certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="60bbb-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="60bbb-286">Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="60bbb-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="60bbb-287">Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="60bbb-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="60bbb-288">Utwórz konto Uruchom jako i konto klasycznego Uruchom jako za pomocą certyfikatu z podpisem własnym w hello chmury Azure dla instytucji rządowych.</span><span class="sxs-lookup"><span data-stu-id="60bbb-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="60bbb-289">W zależności od opcji konfiguracji hello wybranej hello skrypt tworzy hello następujące elementy.</span><span class="sxs-lookup"><span data-stu-id="60bbb-289">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="60bbb-290">**W przypadku kont Uruchom jako:**</span><span class="sxs-lookup"><span data-stu-id="60bbb-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="60bbb-291">Tworzy Azure AD aplikacji toobe wyeksportowany z obu hello z podpisem własnym lub klucz publiczny certyfikatu przedsiębiorstwa, tworzy konto główne usługi dla aplikacji hello w usłudze Azure AD i przypisuje hello roli współautora dla konta hello w bieżącym Subskrypcja.</span><span class="sxs-lookup"><span data-stu-id="60bbb-291">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="60bbb-292">Możesz zmienić to ustawienie tooOwner ani żadnych innych ról.</span><span class="sxs-lookup"><span data-stu-id="60bbb-292">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="60bbb-293">Aby uzyskać więcej informacji, zobacz [Kontrola dostępu oparta na rolach w usłudze Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="60bbb-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="60bbb-294">Tworzy zasób certyfikatu usługi Automatyzacja o nazwie *AzureRunAsCertificate* hello określono konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="60bbb-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="60bbb-295">zasób certyfikatu Hello przechowuje hello certyfikatu klucza prywatnego, który jest używany przez aplikację hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60bbb-295">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="60bbb-296">Tworzy zasób połączenia usługi Automatyzacja o nazwie *AzureRunAsConnection* hello określono konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="60bbb-296">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="60bbb-297">zasób połączenia Hello przechowuje identyfikator aplikacji hello, identyfikatora dzierżawcy, identyfikator subskrypcji i odcisk palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="60bbb-297">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="60bbb-298">**W przypadku klasycznych kont Uruchom jako:**</span><span class="sxs-lookup"><span data-stu-id="60bbb-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="60bbb-299">Tworzy zasób certyfikatu usługi Automatyzacja o nazwie *AzureClassicRunAsCertificate* hello określono konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="60bbb-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="60bbb-300">zasób certyfikatu Hello zawiera klucz prywatny certyfikatu hello używane przez hello certyfikat zarządzania.</span><span class="sxs-lookup"><span data-stu-id="60bbb-300">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="60bbb-301">Tworzy zasób połączenia usługi Automatyzacja o nazwie *AzureClassicRunAsConnection* hello określono konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="60bbb-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="60bbb-302">zasób połączenia Hello przechowuje hello Nazwa subskrypcji, identyfikator subskrypcji i certyfikat nazwa zasobów.</span><span class="sxs-lookup"><span data-stu-id="60bbb-302">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="60bbb-303">Jeśli wybierzesz opcję tworzenia klasycznego konta Uruchom jako, po wykonaniu skryptu hello, przekazywanie hello publicznego zarządzania toohello (rozszerzenie nazwy pliku cer) magazynu certyfikatów dla subskrypcji hello tego konta automatyzacji hello został utworzony w.</span><span class="sxs-lookup"><span data-stu-id="60bbb-303">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

<span data-ttu-id="60bbb-304">tooexecute hello skryptu i przekaż certyfikat hello, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="60bbb-304">tooexecute hello script and upload hello certificate, do hello following:</span></span>

1. <span data-ttu-id="60bbb-305">Zapisz hello następującego skryptu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="60bbb-305">Save hello following script on your computer.</span></span> <span data-ttu-id="60bbb-306">W tym przykładzie, zapisać go z nazwą pliku hello *RunAsAccount.ps1 nowy*.</span><span class="sxs-lookup"><span data-stu-id="60bbb-306">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="60bbb-307">Na komputerze kliknij przycisk **Start**, a następnie uruchom program **Windows PowerShell** z podwyższonym poziomem uprawnień użytkownika.</span><span class="sxs-lookup"><span data-stu-id="60bbb-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="60bbb-308">Z hello z podwyższonym poziomem uprawnień, powłoka wiersza polecenia programu PowerShell, przejdź toohello folderu, który zawiera hello skryptu, który został utworzony w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="60bbb-308">From hello elevated PowerShell command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>

4. <span data-ttu-id="60bbb-309">Uruchom skrypt hello przy użyciu wartości parametrów hello hello konfiguracji, które są wymagane.</span><span class="sxs-lookup"><span data-stu-id="60bbb-309">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="60bbb-310">**Tworzenie konta Uruchom jako przy użyciu certyfikatu z podpisem własnym**</span><span class="sxs-lookup"><span data-stu-id="60bbb-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="60bbb-311">**Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu z podpisem własnym**</span><span class="sxs-lookup"><span data-stu-id="60bbb-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="60bbb-312">**Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu przedsiębiorstwa**</span><span class="sxs-lookup"><span data-stu-id="60bbb-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="60bbb-313">**Utwórz konto Uruchom jako i konto klasycznego Uruchom jako za pomocą certyfikatu z podpisem własnym w hello chmury Azure dla instytucji rządowych**</span><span class="sxs-lookup"><span data-stu-id="60bbb-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="60bbb-314">Po wykonaniu skryptu hello, będzie tooauthenticate zostanie wyświetlony monit o systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="60bbb-314">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="60bbb-315">Zaloguj się przy użyciu konta, które jest członkiem grupy administratorów subskrypcji hello i współadministratorem subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="60bbb-315">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="60bbb-316">Po pomyślnym wykonaniu hello script należy zwrócić uwagę na następujące hello:</span><span class="sxs-lookup"><span data-stu-id="60bbb-316">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="60bbb-317">Jeśli utworzono konto klasycznego Uruchom jako z publicznego certyfikatu z podpisem własnym (plik cer) hello skrypt tworzy i zapisuje go toohello folder plików tymczasowych na komputerze w obszarze profil użytkownika hello *%USERPROFILE%\AppData\Local\Temp*, używany sesji programu PowerShell hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="60bbb-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="60bbb-318">Jeśli zostało utworzone klasyczne konto Uruchom jako z publicznym certyfikatem przedsiębiorstwa (plik CER), użyj tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="60bbb-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="60bbb-319">Wykonaj instrukcje hello [przekazywania toohello certyfikat interfejsu API zarządzania klasycznego portalu Azure](../azure-api-management-certs.md), a następnie zweryfikować hello konfigurację poświadczeń z usługi zarządzania zasobami przy użyciu hello [przykładowy kod tooauthenticate z usługi zarządzania zasobami](#sample-code-to-authenticate-with-service-management-resources).</span><span class="sxs-lookup"><span data-stu-id="60bbb-319">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with Service Management resources by using hello [sample code tooauthenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="60bbb-320">Jeśli tak, *nie* Utwórz konto klasycznego Uruchom jako, uwierzytelniania za pomocą zasoby usługi Resource Manager i sprawdzić poprawność konfiguracji poświadczeń hello przy użyciu hello [przykładowy kod w celu uwierzytelniania z usługi zarządzania zasoby](#sample-code-to-authenticate-with-resource-manager-resources).</span><span class="sxs-lookup"><span data-stu-id="60bbb-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a><span data-ttu-id="60bbb-321">Przykładowy kod tooauthenticate z zasobami usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="60bbb-321">Sample code tooauthenticate with Resource Manager resources</span></span>
<span data-ttu-id="60bbb-322">Można użyć następujących hello zaktualizowany przykładowy kod z hello *AzureAutomationTutorialScript* Przykładowy element runbook, tooauthenticate za pomocą hello Uruchom jako konta toomanage zasoby usługi Resource Manager elementy runbook.</span><span class="sxs-lookup"><span data-stu-id="60bbb-322">You can use hello following updated sample code, taken from hello *AzureAutomationTutorialScript* example runbook, tooauthenticate by using hello Run As account toomanage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

<span data-ttu-id="60bbb-323">toohelp tooeasily możesz pracy między wiele subskrypcji, skrypt hello zawiera dwa wiersze kodu obsługujących odwołujące się do kontekstu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="60bbb-323">toohelp you tooeasily work between multiple subscriptions, hello script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="60bbb-324">Zasób zmiennej o nazwie *SubscriptionId* zawiera identyfikator hello hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="60bbb-324">A variable asset named *SubscriptionId* contains hello ID of hello subscription.</span></span> <span data-ttu-id="60bbb-325">Po hello `Add-AzureRmAccount` instrukcji polecenia cmdlet hello [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) polecenia cmdlet jest podany zestaw parametrów hello *- SubscriptionId*.</span><span class="sxs-lookup"><span data-stu-id="60bbb-325">After hello `Add-AzureRmAccount` cmdlet statement, hello [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet is stated with hello parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="60bbb-326">Jeśli nazwa zmiennej hello jest zbyt ogólne, można poprawić go tooinclude prefiksu lub użyj innego toomake konwencji nazewnictwa go tooidentify łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="60bbb-326">If hello variable name is too generic, you can revise it tooinclude a prefix or use another naming convention toomake it easier tooidentify.</span></span> <span data-ttu-id="60bbb-327">Alternatywnie można użyć zestaw parametrów hello *— Nazwa subskrypcji* zamiast *- SubscriptionId* z odpowiedniej zawartości zmiennej.</span><span class="sxs-lookup"><span data-stu-id="60bbb-327">Alternatively, you can use hello parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="60bbb-328">polecenia cmdlet służące do uwierzytelniania w hello runbook Hello `Add-AzureRmAccount`, używa hello *ServicePrincipalCertificate* zestaw parametrów.</span><span class="sxs-lookup"><span data-stu-id="60bbb-328">hello cmdlet that you use for authenticating in hello runbook, `Add-AzureRmAccount`, uses hello *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="60bbb-329">Jest uwierzytelniany przy użyciu hello certyfikat główny usługi, nie hello poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="60bbb-329">It authenticates by using hello service principal certificate, not hello user credentials.</span></span>

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a><span data-ttu-id="60bbb-330">Przykładowy kod tooauthenticate z zasobami usługi zarządzania</span><span class="sxs-lookup"><span data-stu-id="60bbb-330">Sample code tooauthenticate with Service Management resources</span></span>
<span data-ttu-id="60bbb-331">Można użyć powitania po przykładowy kod, który jest pobierana z hello *AzureClassicAutomationTutorialScript* Przykładowy element runbook, tooauthenticate przy użyciu hello klasycznego Uruchom jako konta toomanage zasoby klasyczne z sieci elementy runbook.</span><span class="sxs-lookup"><span data-stu-id="60bbb-331">You can use hello following updated sample code, which is taken from hello *AzureClassicAutomationTutorialScript* example runbook, tooauthenticate by using hello Classic Run As account toomanage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="60bbb-332">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="60bbb-332">Next steps</span></span>
* <span data-ttu-id="60bbb-333">[Application and service principal objects in Azure AD](../active-directory/active-directory-application-objects.md) (Obiekty aplikacji i nazwy głównej usługi w usłudze Azure AD)</span><span class="sxs-lookup"><span data-stu-id="60bbb-333">[Application and service principal objects in Azure AD](../active-directory/active-directory-application-objects.md)</span></span>
* [<span data-ttu-id="60bbb-334">Kontrola dostępu oparta na rolach w usłudze Azure Automation</span><span class="sxs-lookup"><span data-stu-id="60bbb-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* <span data-ttu-id="60bbb-335">[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md) (Omówienie certyfikatów usług Azure Cloud Services)</span><span class="sxs-lookup"><span data-stu-id="60bbb-335">[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md)</span></span>
