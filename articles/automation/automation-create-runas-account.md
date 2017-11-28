---
title: konta automatyzacji Uruchom jako platformy Azure aaaCreate | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób tooupdate automatyzacji Twojego konta, a następnie utworzyć konta Uruchom jako, przy użyciu programu PowerShell lub portalu hello."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 94eb54fa0b518056a726d17146c63411e248273b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="86ad6-103">Aktualizowanie uwierzytelniania konta usługi Automation przy użyciu kont Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="86ad6-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="86ad6-104">Można aktualizować istniejącego konta automatyzacji z portalu hello lub jeśli za pomocą programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="86ad6-104">You can update your existing Automation account from hello portal or use PowerShell if:</span></span>

* <span data-ttu-id="86ad6-105">Utwórz konto usługi Automatyzacja, ale odrzucić konta Uruchom jako hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="86ad6-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="86ad6-106">Zasoby usługi Resource Manager toomanage konto automatyzacji jest już używana, i chcesz tooupdate hello konta tooinclude hello konta Uruchom jako dla uwierzytelniania elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="86ad6-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="86ad6-107">Używasz toomanage konta automatyzacji dla zasoby klasyczne i chcesz tooupdate go hello toouse konta w klasycznym Uruchom jako, zamiast tworzenia nowego konta i migrację z tooit elementy runbook i zasoby.</span><span class="sxs-lookup"><span data-stu-id="86ad6-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="86ad6-108">Ma toocreate Uruchom jako, a konto klasycznego Uruchom jako za pomocą certyfikatu wystawionego przez urząd certyfikacji (CA) przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="86ad6-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86ad6-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="86ad6-109">Prerequisites</span></span>

* <span data-ttu-id="86ad6-110">skrypt Hello może być uruchomiony tylko w systemie Windows 10 i Windows Server 2016 z usługi Azure Resource Manager modułów 3.0.0 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="86ad6-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="86ad6-111">Nie jest obsługiwany przez wcześniejsze wersje systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="86ad6-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="86ad6-112">Program Azure PowerShell 1.0 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="86ad6-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="86ad6-113">Aby uzyskać informacje o wersji hello PowerShell 1.0, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="86ad6-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="86ad6-114">Konto automatyzacji, który jest określany jako wartość hello hello *— AutomationAccountName* i *- ApplicationDisplayName* parametrów w hello następującego skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86ad6-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="86ad6-115">wartości tooget hello *SubscriptionID*, *ResourceGroup*, i *AutomationAccountName*, które są wymagane parametry skryptu hello, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="86ad6-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello script, do hello following:</span></span>

1. <span data-ttu-id="86ad6-116">W hello portalu Azure, wybierz konto Automatyzacja na powitania **konto automatyzacji** bloku, a następnie wybierz **wszystkie ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="86ad6-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="86ad6-117">Na powitania **wszystkie ustawienia** bloku, w obszarze **ustawienia konta**, wybierz pozycję **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="86ad6-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="86ad6-118">Należy pamiętać, wartości hello na powitania **właściwości** bloku.</span><span class="sxs-lookup"><span data-stu-id="86ad6-118">Note hello values on hello **Properties** blade.</span></span><br><br> <span data-ttu-id="86ad6-119">![Blok "Właściwości" konto automatyzacji Hello](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="86ad6-119">![hello Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-tooupdate-your-automation-account"></a><span data-ttu-id="86ad6-120">Wymagane uprawnienia tooupdate Twojego konta automatyzacji</span><span class="sxs-lookup"><span data-stu-id="86ad6-120">Required permissions tooupdate your Automation account</span></span>
<span data-ttu-id="86ad6-121">tooupdate konto usługi Automatyzacja, musi mieć powitania po określone uprawnienia i toocomplete wymagane uprawnienia, w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="86ad6-121">tooupdate an Automation account, you must have hello following specific privileges and permissions required toocomplete this topic.</span></span>   
 
* <span data-ttu-id="86ad6-122">Twoje konto użytkownika AD musi toobe tooa dodano rolę z roli współautora toohello równoważne uprawnienia dla zasobów Microsoft.Automation w sposób opisany w artykule [kontroli dostępu opartej na rolach w automatyzacji Azure](automation-role-based-access-control.md#contributor-role-permissions).</span><span class="sxs-lookup"><span data-stu-id="86ad6-122">Your AD user account needs toobe added tooa role with permissions equivalent toohello Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="86ad6-123">Użytkownicy inni niż administratorzy w Twojej dzierżawie usługi Azure AD mogą [rejestrowania aplikacji AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) Jeśli rejestracji aplikacji hello ustawienie ustawiono zbyt**tak**.</span><span class="sxs-lookup"><span data-stu-id="86ad6-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if hello App registrations setting is set too**Yes**.</span></span>  <span data-ttu-id="86ad6-124">Jeśli ustawienie rejestracji aplikacji hello ustawiono zbyt**nr**, wykonanie tej czynności użytkownika hello musi być administratorem globalnym w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86ad6-124">If hello app registrations setting is set too**No**, hello user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="86ad6-125">Jeśli nie jesteś członkiem wystąpienia usługi Active Directory hello subskrypcji przed dodaniem toohello globalnego administratora/drugi-administrator roli hello subskrypcji, zostaną dodane tooActive katalogu jako Gość.</span><span class="sxs-lookup"><span data-stu-id="86ad6-125">If you are not a member of hello subscription’s Active Directory instance before you are added toohello global administrator/co-administrator role of hello subscription, you are added tooActive Directory as a guest.</span></span> <span data-ttu-id="86ad6-126">W takiej sytuacji pojawi się "nie ma uprawnień toocreate..."</span><span class="sxs-lookup"><span data-stu-id="86ad6-126">In this situation, you receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="86ad6-127">Ostrzeżenie dotyczące hello **Dodaj konto automatyzacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="86ad6-127">warning on hello **Add Automation Account** blade.</span></span> <span data-ttu-id="86ad6-128">Użytkownicy, którzy zostały dodane toohello globalnego administratora/drugi-administrator roli najpierw można usunąć z wystąpienia usługi Active Directory hello subskrypcji i ponownie dodany toomake ich pełną użytkownika w usłudze Active Directory.</span><span class="sxs-lookup"><span data-stu-id="86ad6-128">Users who were added toohello global administrator/co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="86ad6-129">tooverify takiej sytuacji z hello **usługi Azure Active Directory** okienka w hello portalu Azure, wybierz opcję **użytkowników i grup**, wybierz pozycję **wszyscy użytkownicy** i po wybraniu hello określony użytkownik, wybierz opcję **profilu**.</span><span class="sxs-lookup"><span data-stu-id="86ad6-129">tooverify this situation, from hello **Azure Active Directory** pane in hello Azure portal, select **Users and groups**, select **All users** and, after you select hello specific user, select **Profile**.</span></span> <span data-ttu-id="86ad6-130">Witaj wartość hello **typ użytkownika** atrybutu na liście profilów użytkowników hello nie powinna być równa **gościa**.</span><span class="sxs-lookup"><span data-stu-id="86ad6-130">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-hello-portal"></a><span data-ttu-id="86ad6-131">Utwórz konto Uruchom jako z portalu hello</span><span class="sxs-lookup"><span data-stu-id="86ad6-131">Create Run As account from hello portal</span></span>
<span data-ttu-id="86ad6-132">W tej sekcji wykonaj następujące kroki tooupdate hello Twoje konto usługi Automatyzacja Azure z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="86ad6-132">In this section, perform hello following steps tooupdate your Azure Automation account from  hello Azure portal.</span></span>  <span data-ttu-id="86ad6-133">Tworzenia hello konta Uruchom jako i klasycznego Uruchom jako indywidualnie, a jeśli toomanage zasobów w klasycznym portalu Azure hello nie jest konieczne, można utworzyć konta Uruchom jako platformy Azure hello.</span><span class="sxs-lookup"><span data-stu-id="86ad6-133">You create hello Run As and Classic Run As accounts individually, and if you don't need toomanage resources in hello classic Azure portal, you can just create hello Azure Run As account.</span></span>  

<span data-ttu-id="86ad6-134">proces Hello tworzy hello następujące elementy na Twoim koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="86ad6-134">hello process creates hello following items in your Automation account.</span></span>

<span data-ttu-id="86ad6-135">**W przypadku kont Uruchom jako:**</span><span class="sxs-lookup"><span data-stu-id="86ad6-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="86ad6-136">Tworzy aplikację usługi Azure AD z certyfikatu z podpisem własnym, tworzy konto główne usługi dla aplikacji hello w usłudze Azure AD i przypisuje rolę współautora hello hello konta w Twojej bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="86ad6-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="86ad6-137">Możesz zmienić to ustawienie tooOwner ani żadnych innych ról.</span><span class="sxs-lookup"><span data-stu-id="86ad6-137">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="86ad6-138">Aby uzyskać więcej informacji, zobacz [Kontrola dostępu oparta na rolach w usłudze Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="86ad6-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="86ad6-139">Tworzy zasób certyfikatu usługi Automatyzacja o nazwie *AzureRunAsCertificate* hello określono konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="86ad6-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="86ad6-140">zasób certyfikatu Hello przechowuje hello certyfikatu klucza prywatnego, który jest używany przez aplikację hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86ad6-140">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="86ad6-141">Tworzy zasób połączenia usługi Automatyzacja o nazwie *AzureRunAsConnection* hello określono konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="86ad6-141">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="86ad6-142">zasób połączenia Hello przechowuje identyfikator aplikacji hello, identyfikatora dzierżawcy, identyfikator subskrypcji i odcisk palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="86ad6-142">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="86ad6-143">**W przypadku klasycznych kont Uruchom jako:**</span><span class="sxs-lookup"><span data-stu-id="86ad6-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="86ad6-144">Tworzy zasób certyfikatu usługi Automatyzacja o nazwie *AzureClassicRunAsCertificate* hello określono konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="86ad6-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="86ad6-145">zasób certyfikatu Hello zawiera klucz prywatny certyfikatu hello używane przez hello certyfikat zarządzania.</span><span class="sxs-lookup"><span data-stu-id="86ad6-145">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="86ad6-146">Tworzy zasób połączenia usługi Automatyzacja o nazwie *AzureClassicRunAsConnection* hello określono konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="86ad6-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="86ad6-147">zasób połączenia Hello przechowuje hello Nazwa subskrypcji, identyfikator subskrypcji i certyfikat nazwa zasobów.</span><span class="sxs-lookup"><span data-stu-id="86ad6-147">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="86ad6-148">Zaloguj się toohello portalu Azure przy użyciu konta, które jest członkiem roli Administratorzy subskrypcji hello i współadministratorem subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="86ad6-148">Sign in toohello Azure portal with an account that is a member of hello Subscription Admins role and co-administrator of hello subscription.</span></span>
2. <span data-ttu-id="86ad6-149">W bloku konta usługi Automatyzacja hello, wybierz **konta Uruchom jako** sekcji hello **ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="86ad6-149">From hello Automation account blade, select **Run As Accounts** under hello section **Account Settings**.</span></span>  
3. <span data-ttu-id="86ad6-150">W zależności od tego, które konto jest wymagane, wybierz pozycję **Konto Uruchom jako platformy Azure** lub **Klasyczne konto Uruchom jako platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="86ad6-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="86ad6-151">Po wybraniu albo hello **dodać Uruchom jako platformy Azure** lub **dodać Azure Classic konta Uruchom jako** bloku pojawia się i po przejrzeniu hello ogólne informacje, kliknij przycisk **Utwórz** tooproceed z Tworzenie konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="86ad6-151">After selecting either hello **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing hello overview information, click **Create** tooproceed with Run As account creation.</span></span>  
4. <span data-ttu-id="86ad6-152">Gdy Azure utworzy hello konta Uruchom jako, możesz śledzić postępy hello w obszarze **powiadomienia** z hello menu i transparent wyświetleniem informacją o trwającym tworzeniu konta hello.</span><span class="sxs-lookup"><span data-stu-id="86ad6-152">While Azure creates hello Run As account, you can track hello progress under **Notifications** from hello menu and a banner is displayed stating hello account is being created.</span></span>  <span data-ttu-id="86ad6-153">Ten proces może potrwać kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="86ad6-153">This process can take a few minutes toocomplete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="86ad6-154">Tworzenie konta Uruchom jako przy użyciu skryptu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="86ad6-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="86ad6-155">Ten skrypt programu PowerShell obejmuje obsługę hello następujące konfiguracje:</span><span class="sxs-lookup"><span data-stu-id="86ad6-155">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="86ad6-156">Tworzenie konta Uruchom jako przy użyciu certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="86ad6-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="86ad6-157">Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="86ad6-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="86ad6-158">Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="86ad6-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="86ad6-159">Utwórz konto Uruchom jako i konto klasycznego Uruchom jako za pomocą certyfikatu z podpisem własnym w hello chmury Azure dla instytucji rządowych.</span><span class="sxs-lookup"><span data-stu-id="86ad6-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="86ad6-160">W zależności od opcji konfiguracji hello wybranej hello skrypt tworzy hello następujące elementy.</span><span class="sxs-lookup"><span data-stu-id="86ad6-160">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="86ad6-161">**W przypadku kont Uruchom jako:**</span><span class="sxs-lookup"><span data-stu-id="86ad6-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="86ad6-162">Tworzy Azure AD aplikacji toobe wyeksportowany z obu hello z podpisem własnym lub klucz publiczny certyfikatu przedsiębiorstwa, tworzy konto główne usługi dla aplikacji hello w usłudze Azure AD i przypisuje hello roli współautora dla konta hello w bieżącym Subskrypcja.</span><span class="sxs-lookup"><span data-stu-id="86ad6-162">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="86ad6-163">Możesz zmienić to ustawienie tooOwner ani żadnych innych ról.</span><span class="sxs-lookup"><span data-stu-id="86ad6-163">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="86ad6-164">Aby uzyskać więcej informacji, zobacz [Kontrola dostępu oparta na rolach w usłudze Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="86ad6-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="86ad6-165">Tworzy zasób certyfikatu usługi Automatyzacja o nazwie *AzureRunAsCertificate* hello określono konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="86ad6-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="86ad6-166">zasób certyfikatu Hello przechowuje hello certyfikatu klucza prywatnego, który jest używany przez aplikację hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86ad6-166">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="86ad6-167">Tworzy zasób połączenia usługi Automatyzacja o nazwie *AzureRunAsConnection* hello określono konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="86ad6-167">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="86ad6-168">zasób połączenia Hello przechowuje identyfikator aplikacji hello, identyfikatora dzierżawcy, identyfikator subskrypcji i odcisk palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="86ad6-168">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="86ad6-169">**W przypadku klasycznych kont Uruchom jako:**</span><span class="sxs-lookup"><span data-stu-id="86ad6-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="86ad6-170">Tworzy zasób certyfikatu usługi Automatyzacja o nazwie *AzureClassicRunAsCertificate* hello określono konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="86ad6-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="86ad6-171">zasób certyfikatu Hello zawiera klucz prywatny certyfikatu hello używane przez hello certyfikat zarządzania.</span><span class="sxs-lookup"><span data-stu-id="86ad6-171">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="86ad6-172">Tworzy zasób połączenia usługi Automatyzacja o nazwie *AzureClassicRunAsConnection* hello określono konto automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="86ad6-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="86ad6-173">zasób połączenia Hello przechowuje hello Nazwa subskrypcji, identyfikator subskrypcji i certyfikat nazwa zasobów.</span><span class="sxs-lookup"><span data-stu-id="86ad6-173">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="86ad6-174">Jeśli wybierzesz opcję tworzenia klasycznego konta Uruchom jako, po wykonaniu skryptu hello, przekazywanie hello publicznego zarządzania toohello (rozszerzenie nazwy pliku cer) magazynu certyfikatów dla subskrypcji hello tego konta automatyzacji hello został utworzony w.</span><span class="sxs-lookup"><span data-stu-id="86ad6-174">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="86ad6-175">Zapisz hello następującego skryptu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="86ad6-175">Save hello following script on your computer.</span></span> <span data-ttu-id="86ad6-176">W tym przykładzie, zapisać go z nazwą pliku hello *RunAsAccount.ps1 nowy*.</span><span class="sxs-lookup"><span data-stu-id="86ad6-176">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

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
        $KeyCredential.EndDate = Get-Date $PfxCert.GetExpirationDateString()
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
        if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 0) -or ($AzureRMProfileVersion.Major -gt 3)))
        {
            Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
            return
        }

        Login-AzureRmAccount -Environment $EnvironmentName 
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
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="86ad6-177">Na komputerze, należy uruchomić **programu Windows PowerShell** z hello **Start** ekranu z podwyższonym poziomem uprawnień użytkownika.</span><span class="sxs-lookup"><span data-stu-id="86ad6-177">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="86ad6-178">Z hello z podwyższonym poziomem uprawnień, powłoka wiersza polecenia przejdź toohello folderu, który zawiera hello skryptu, który został utworzony w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="86ad6-178">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="86ad6-179">Uruchom skrypt hello przy użyciu wartości parametrów hello hello konfiguracji, które są wymagane.</span><span class="sxs-lookup"><span data-stu-id="86ad6-179">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="86ad6-180">**Tworzenie konta Uruchom jako przy użyciu certyfikatu z podpisem własnym**</span><span class="sxs-lookup"><span data-stu-id="86ad6-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="86ad6-181">**Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu z podpisem własnym**</span><span class="sxs-lookup"><span data-stu-id="86ad6-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="86ad6-182">**Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu przedsiębiorstwa**</span><span class="sxs-lookup"><span data-stu-id="86ad6-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="86ad6-183">**Utwórz konto Uruchom jako i konto klasycznego Uruchom jako za pomocą certyfikatu z podpisem własnym w hello chmury Azure dla instytucji rządowych**</span><span class="sxs-lookup"><span data-stu-id="86ad6-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="86ad6-184">Po wykonaniu skryptu hello, będzie tooauthenticate zostanie wyświetlony monit o systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="86ad6-184">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="86ad6-185">Zaloguj się przy użyciu konta, które jest członkiem grupy administratorów subskrypcji hello i współadministratorem subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="86ad6-185">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="86ad6-186">Po pomyślnym wykonaniu hello script należy zwrócić uwagę na następujące hello:</span><span class="sxs-lookup"><span data-stu-id="86ad6-186">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="86ad6-187">Jeśli utworzono konto klasycznego Uruchom jako z publicznego certyfikatu z podpisem własnym (plik cer) hello skrypt tworzy i zapisuje go toohello folder plików tymczasowych na komputerze w obszarze profil użytkownika hello *%USERPROFILE%\AppData\Local\Temp*, używany sesji programu PowerShell hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="86ad6-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="86ad6-188">Jeśli zostało utworzone klasyczne konto Uruchom jako z publicznym certyfikatem przedsiębiorstwa (plik CER), użyj tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="86ad6-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="86ad6-189">Wykonaj instrukcje hello [przekazywania toohello certyfikat interfejsu API zarządzania klasycznego portalu Azure](../azure-api-management-certs.md), a następnie sprawdź poprawność konfiguracji poświadczeń hello o zasoby klasyczne wdrożenia przy użyciu hello [przykładowy kod tooauthenticate z zasobów wdrożenia klasycznego Azure](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="86ad6-189">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="86ad6-190">Jeśli tak, *nie* Utwórz konto klasycznego Uruchom jako, uwierzytelniania za pomocą zasoby usługi Resource Manager i sprawdzić poprawność konfiguracji poświadczeń hello przy użyciu hello [przykładowy kod w celu uwierzytelniania z usługi zarządzania zasoby](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="86ad6-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86ad6-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86ad6-191">Next steps</span></span>
* <span data-ttu-id="86ad6-192">Aby uzyskać więcej informacji na temat nazwy główne usług można znaleźć zbyt[obiekty aplikacji i nazwy głównej usługi](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="86ad6-192">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="86ad6-193">Aby uzyskać więcej informacji na temat certyfikatów i usług Azure można znaleźć zbyt[Omówienie certyfikatów dla usług w chmurze Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="86ad6-193">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
