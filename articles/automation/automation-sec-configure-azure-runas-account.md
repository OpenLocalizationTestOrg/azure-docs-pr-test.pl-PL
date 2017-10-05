---
title: Konfigurowanie konta Uruchom jako platformy Azure | Microsoft Docs
description: "Ten samouczek przeprowadza Cię przez proces tworzenia, testowania i przykładowego użycia uwierzytelniania podmiotu zabezpieczeń w usłudze Azure Automation."
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
redirect_document_id: TRUE
ms.openlocfilehash: f88c775eba19bb227d0e206d6420c08b57305b92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="0ac13-104">Uwierzytelnianie elementów runbook przy użyciu konta Uruchom jako platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0ac13-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="0ac13-105">W tym artykule przedstawiono sposób konfigurowania konta usługi Azure Automation w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0ac13-105">This article shows you how to configure an Azure Automation account in the Azure portal.</span></span> <span data-ttu-id="0ac13-106">W tym celu można użyć funkcji konta Uruchom jako do uwierzytelniania elementów runbook zarządzających zasobami w usłudze Azure Resource Manager lub Azure Service Management.</span><span class="sxs-lookup"><span data-stu-id="0ac13-106">To do so, you use the Run As account feature to authenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="0ac13-107">Po utworzeniu konta usługi Automation w witrynie Azure Portal automatycznie utworzysz dwa konta:</span><span class="sxs-lookup"><span data-stu-id="0ac13-107">When you create an Automation account in the Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="0ac13-108">Konto Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="0ac13-108">A Run As account.</span></span> <span data-ttu-id="0ac13-109">To konto służy do tworzenia nazwy głównej usługi w usłudze Azure Active Directory (Azure AD) oraz certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0ac13-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="0ac13-110">Umożliwia ono również przypisywanie kontroli dostępu opartej na rolach (RBAC) typu Współautor, która zarządza zasobami usługi Resource Manager przy użyciu elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="0ac13-110">It also assigns the Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="0ac13-111">Klasyczne konto Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="0ac13-111">A Classic Run As account.</span></span> <span data-ttu-id="0ac13-112">To konto służy do przekazywania certyfikatu zarządzania, który jest używany do zarządzania usługą Service Management lub klasycznymi zasobami przy użyciu elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="0ac13-112">This account uploads a management certificate, which is used to manage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="0ac13-113">Utworzenie konta usługi Automation upraszcza proces i pomaga szybko rozpocząć tworzenie i wdrażanie elementów runbook dla różnych potrzeb automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="0ac13-113">Creating an Automation account simplifies the process for you and helps you quickly start building and deploying runbooks to support your automation needs.</span></span>

<span data-ttu-id="0ac13-114">Używając konta Uruchom jako i klasycznego konta Uruchom jako, możesz:</span><span class="sxs-lookup"><span data-stu-id="0ac13-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="0ac13-115">Zapewnić standardowy sposób uwierzytelniania na platformie Azure podczas zarządzania zasobami usługi Resource Manager lub Service Management z poziomu elementów runbook w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0ac13-115">Provide a standardized way to authenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in the Azure portal.</span></span>
* <span data-ttu-id="0ac13-116">Zautomatyzować użycie globalnych elementów runbook skonfigurowanych w alertach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0ac13-116">Automate the use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="0ac13-117">[Funkcja integracji alertu platformy Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) z globalnymi elementami runbook usługi Automation wymaga konta usługi Automation ze skonfigurowanym kontem Uruchom jako i klasycznym kontem Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="0ac13-117">The [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="0ac13-118">Można wybrać konto usługi Automation, które ma już zdefiniowane konto Uruchom jako i klasyczne konto Uruchom jako, lub wybrać opcję utworzenia nowego konta usługi Automation.</span><span class="sxs-lookup"><span data-stu-id="0ac13-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose to create a new Automation account.</span></span>
>  

<span data-ttu-id="0ac13-119">W tym artykule pokazano, jak utworzyć konto usługi Automation z witryny Azure Portal, zaktualizować konto usługi Automation przy użyciu programu Azure PowerShell, zarządzać konfiguracją konta oraz uwierzytelnić się w elementach runbook.</span><span class="sxs-lookup"><span data-stu-id="0ac13-119">This article shows how to create an Automation account from the Azure portal, update an Automation account by using Azure PowerShell, manage the account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="0ac13-120">Przed rozpoczęciem tworzenia konta usługi Automation warto poznać i rozważyć następujące kwestie:</span><span class="sxs-lookup"><span data-stu-id="0ac13-120">Before you begin creating an Automation account, it's a good idea to understand and consider the following:</span></span>

* <span data-ttu-id="0ac13-121">Utworzenie konta usługi Automation nie wpływa na istniejące konta usługi Automation, które zostały już utworzone w modelu klasycznym lub modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0ac13-121">Creating an Automation account does not affect Automation accounts you might have already created in either the classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="0ac13-122">Proces działa tylko w przypadku kont usługi Automation tworzonych w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0ac13-122">The process works only for Automation accounts that you create in the Azure portal.</span></span> <span data-ttu-id="0ac13-123">Próba utworzenia konta za pomocą klasycznej witryny Azure Portal nie powoduje replikacji konfiguracji konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="0ac13-123">Attempting to create an account from the Azure classic portal does not replicate the Run As account configuration.</span></span>
* <span data-ttu-id="0ac13-124">Jeśli masz już elementy runbook i zasoby (na przykład harmonogramy lub zmienne) przeznaczone do zarządzania zasobami klasycznymi i chcesz uwierzytelniać elementy runbook przy użyciu nowego klasycznego konta Uruchom jako, wykonaj jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="0ac13-124">If you already have runbooks and assets (such as schedules or variables) in place to manage classic resources, and you want runbooks to authenticate with the new Classic Run As account, do either of the following:</span></span>

  * <span data-ttu-id="0ac13-125">Aby utworzyć klasyczne konto Uruchom jako, postępuj zgodnie z instrukcjami w sekcji „Zarządzanie kontem Uruchom jako”.</span><span class="sxs-lookup"><span data-stu-id="0ac13-125">To create a Classic Run As account, follow the instructions in the "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="0ac13-126">Aby zaktualizować istniejące konto, użyj skryptu programu PowerShell z sekcji „Aktualizowanie konta usługi Automation przy użyciu programu PowerShell”.</span><span class="sxs-lookup"><span data-stu-id="0ac13-126">To update your existing account, use the PowerShell script in the "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="0ac13-127">Aby uwierzytelniać się przy użyciu nowego konta Uruchom jako i klasycznego konta Uruchom jako usługi Automation, musisz zmodyfikować istniejące elementy runbook za pomocą przykładowego kodu podanego w sekcji [Przykłady kodu uwierzytelniania](#authentication-code-examples).</span><span class="sxs-lookup"><span data-stu-id="0ac13-127">To authenticate by using the new Run As account and Classic Run As Automation account, you  need to modify your existing runbooks with the example code provided in the section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="0ac13-128">Konto Uruchom jako jest przeznaczone do uwierzytelniania względem zasobów usługi Resource Manager za pomocą nazwy głównej usługi opartej na certyfikacie.</span><span class="sxs-lookup"><span data-stu-id="0ac13-128">The Run As account is for authentication against Resource Manager resources using the certificate-based service principal.</span></span> <span data-ttu-id="0ac13-129">Klasyczne konto Uruchom jako jest przeznaczone do uwierzytelniania względem zasobów usługi Service Management przy użyciu certyfikatu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="0ac13-129">The Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-the-azure-portal"></a><span data-ttu-id="0ac13-130">Tworzenie konta usługi Automation w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0ac13-130">Create an Automation account from the Azure portal</span></span>
<span data-ttu-id="0ac13-131">W tej sekcji utworzysz konto usługi Azure Automation w witrynie Azure Portal, co z kolei spowoduje utworzenie konta Uruchom jako i klasycznego konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="0ac13-131">In this section, you create an Azure Automation account from the Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="0ac13-132">Aby utworzyć konto usługi Automation, musisz być członkiem roli Administratorzy usługi lub współadministratorem subskrypcji, która udziela praw dostępu do subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0ac13-132">To create an Automation account, you must be a member of the Service Admins role or co-administrator of the subscription that is granting access to the subscription.</span></span> <span data-ttu-id="0ac13-133">Musisz być również użytkownikiem dodanym do domyślnego wystąpienia usługi Active Directory tej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0ac13-133">You must also be added as a user to that subscription's default Active Directory instance.</span></span> <span data-ttu-id="0ac13-134">Konto nie musi mieć przypisanej roli uprzywilejowanej.</span><span class="sxs-lookup"><span data-stu-id="0ac13-134">The account does not need to be assigned a privileged role.</span></span>
>
><span data-ttu-id="0ac13-135">Jeśli nie jesteś członkiem wystąpienia usługi Active Directory subskrypcji przed dodaniem do roli współadministratora subskrypcji, dodamy Cię do usługi Active Directory jako gościa.</span><span class="sxs-lookup"><span data-stu-id="0ac13-135">If you are not a member of the subscription’s Active Directory instance before you are added to the co-administrator role of the subscription, you will be added to Active Directory as a guest.</span></span> <span data-ttu-id="0ac13-136">W tym wystąpieniu zobaczysz ostrzeżenie „Nie masz uprawnień do utworzenia...”</span><span class="sxs-lookup"><span data-stu-id="0ac13-136">In this instance, you will receive a “You do not have permissions to create…”</span></span> <span data-ttu-id="0ac13-137">w bloku **Dodawanie konta usługi Automation**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-137">warning on the **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="0ac13-138">Użytkownicy dodani do roli współadministratora najpierw mogą zostać usunięci z wystąpienia usługi Active Directory dla subskrypcji i ponownie dodani, aby zostali pełnymi użytkownikami w usłudze Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0ac13-138">Users who were added to the co-administrator role first can be removed from the subscription's Active Directory instance and re-added to make them a full User in Active Directory.</span></span> <span data-ttu-id="0ac13-139">Aby zweryfikować tę sytuację w okienku **Azure Active Directory** w witrynie Azure Portal wybierz kolejno pozycje **Użytkownicy i grupy** i **Wszyscy użytkownicy**, a po wybraniu określonego użytkownika wybierz pozycję **Profil**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-139">To verify this situation from the **Azure Active Directory** pane in the Azure portal by selecting **Users and groups**, selecting **All users** and, after you select the specific user, selecting **Profile**.</span></span> <span data-ttu-id="0ac13-140">Wartość atrybutu **Typ użytkownika** na liście profilów użytkowników nie powinna być równa **Gość**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-140">The value of the **User type** attribute under the users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="0ac13-141">Zaloguj się do witryny Azure Portal przy użyciu konta, które jest członkiem roli Administratorzy subskrypcji i współadministratorem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0ac13-141">Sign in to the Azure portal with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>

2. <span data-ttu-id="0ac13-142">Wybierz opcję **Konta automatyzacji**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="0ac13-143">W bloku **Konta usługi Automation** kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-143">On the **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="0ac13-144">Zostanie otwarty blok **Dodawanie konta usługi Automation**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-144">The **Add Automation Account** blade opens.</span></span>

 ![Blok „Dodawanie konta usługi Automation”](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="0ac13-146">Jeśli konto nie jest członkiem roli Administratorzy subskrypcji i współadministratorem subskrypcji, w bloku **Dodawanie konta usługi Automation** zobaczysz poniższe ostrzeżenie:</span><span class="sxs-lookup"><span data-stu-id="0ac13-146">If your account is not a member of the subscription administrators role and co-administrator of the subscription, the following warning is displayed on the **Add Automation Account** blade:</span></span>
   >
   >![Ostrzeżenie podczas dodawania konta usługi Automation](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="0ac13-148">W bloku **Dodawanie konta usługi Automation** w polu **Nazwa** wpisz nazwę nowego konta usługi Automation.</span><span class="sxs-lookup"><span data-stu-id="0ac13-148">On the **Add Automation Account** blade, in the **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="0ac13-149">Jeśli masz więcej niż jedną subskrypcję, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0ac13-149">If you have more than one subscription, do the following:</span></span>

    <span data-ttu-id="0ac13-150">a.</span><span class="sxs-lookup"><span data-stu-id="0ac13-150">a.</span></span> <span data-ttu-id="0ac13-151">W obszarze **Subskrypcja** określ subskrypcję dla nowego konta.</span><span class="sxs-lookup"><span data-stu-id="0ac13-151">Under **Subscription**, specify one for the new account.</span></span>

    <span data-ttu-id="0ac13-152">b.</span><span class="sxs-lookup"><span data-stu-id="0ac13-152">b.</span></span> <span data-ttu-id="0ac13-153">W obszarze **Grupa zasobów** kliknij pozycję **Utwórz nową** lub **Użyj istniejącej**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="0ac13-154">c.</span><span class="sxs-lookup"><span data-stu-id="0ac13-154">c.</span></span> <span data-ttu-id="0ac13-155">W obszarze **Lokalizacja** określ centrum danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0ac13-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="0ac13-156">W obszarze **Tworzenie konta Uruchom jako platformy Azure** wybierz pozycję **Tak**, a następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0ac13-157">Jeśli zrezygnujesz z tworzenia konta Uruchom jako, wybierając pozycję **Nie**, w bloku **Dodawanie konta usługi Automation** zostanie wyświetlony komunikat ostrzegawczy.</span><span class="sxs-lookup"><span data-stu-id="0ac13-157">If you choose not to create the Run As account by selecting **No**, a warning message is displayed the **Add Automation Account** blade.</span></span> <span data-ttu-id="0ac13-158">Mimo że konto zostanie utworzone w witrynie Azure Portal, nie będzie ono miało odpowiedniej tożsamości uwierzytelniania w usłudze katalogowej subskrypcji klasycznej lub subskrypcji usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0ac13-158">Although the account is created in the Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="0ac13-159">Dlatego konto nie będzie miało dostępu do zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0ac13-159">Consequently, the account has no access to resources in your subscription.</span></span> <span data-ttu-id="0ac13-160">Ten scenariusz zapobiega sytuacji, w której wszelkie elementy runbook odwołujące się do tego konta miałyby możliwość uwierzytelniania i wykonywania zadań w odniesieniu do zasobów w tych modelach wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0ac13-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > ![Komunikat ostrzegawczy w bloku „Dodawanie konta usługi Automation”](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="0ac13-162">Ponadto — ponieważ nie została utworzona nazwa główna usługi — nie można przypisać roli Współautor.</span><span class="sxs-lookup"><span data-stu-id="0ac13-162">Additionally, because the service principal is not created, the Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="0ac13-163">W trakcie tworzenia konta usługi Automation na platformie Azure postęp można śledzić po wybraniu z menu opcji **Powiadomienia**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-163">While Azure creates the Automation account, you can track the progress under **Notifications** from the menu.</span></span>

### <a name="resources"></a><span data-ttu-id="0ac13-164">Zasoby</span><span class="sxs-lookup"><span data-stu-id="0ac13-164">Resources</span></span>
<span data-ttu-id="0ac13-165">Po pomyślnym utworzeniu konta usługi Automation automatycznie zostanie utworzonych kilka zasobów.</span><span class="sxs-lookup"><span data-stu-id="0ac13-165">When the Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="0ac13-166">Zasoby są podsumowywane w dwóch następujących tabelach:</span><span class="sxs-lookup"><span data-stu-id="0ac13-166">The resources are summarized in the following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="0ac13-167">Zasoby konta Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="0ac13-167">Run As account resources</span></span>

| <span data-ttu-id="0ac13-168">Zasób</span><span class="sxs-lookup"><span data-stu-id="0ac13-168">Resource</span></span> | <span data-ttu-id="0ac13-169">Opis</span><span class="sxs-lookup"><span data-stu-id="0ac13-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0ac13-170">AzureAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="0ac13-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="0ac13-171">Przykładowy graficzny element runbook, który demonstruje sposób uwierzytelniania przy użyciu konta Uruchom jako i pobiera wszystkie zasoby usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0ac13-171">An example graphical runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span></span> |
| <span data-ttu-id="0ac13-172">AzureAutomationTutorialScript Runbook</span><span class="sxs-lookup"><span data-stu-id="0ac13-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="0ac13-173">Przykładowy element runbook programu PowerShell, który demonstruje sposób uwierzytelniania przy użyciu konta Uruchom jako i pobiera wszystkie zasoby usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0ac13-173">An example PowerShell runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span></span> |
| <span data-ttu-id="0ac13-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="0ac13-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="0ac13-175">Zasób certyfikatu tworzony automatycznie podczas tworzenia konta usługi Automation lub używania poniższego skryptu programu PowerShell dla istniejącego konta.</span><span class="sxs-lookup"><span data-stu-id="0ac13-175">The certificate asset that's automatically created when you create an Automation account or use the following PowerShell script for an existing account.</span></span> <span data-ttu-id="0ac13-176">Certyfikat umożliwia uwierzytelnianie za pomocą platformy Azure, aby można było zarządzać zasobami usługi Azure Resource Manager z poziomu elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="0ac13-176">The certificate allows you to authenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="0ac13-177">Certyfikat ma roczny okres obowiązywania.</span><span class="sxs-lookup"><span data-stu-id="0ac13-177">The certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="0ac13-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="0ac13-178">AzureRunAsConnection</span></span> | <span data-ttu-id="0ac13-179">Zasób połączenia tworzony automatycznie podczas tworzenia konta usługi Automation lub używania skryptu programu PowerShell dla istniejącego konta.</span><span class="sxs-lookup"><span data-stu-id="0ac13-179">The connection asset that's automatically created when you create an Automation account or use the PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="0ac13-180">Zasoby klasycznego konta Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="0ac13-180">Classic Run As account resources</span></span>

| <span data-ttu-id="0ac13-181">Zasób</span><span class="sxs-lookup"><span data-stu-id="0ac13-181">Resource</span></span> | <span data-ttu-id="0ac13-182">Opis</span><span class="sxs-lookup"><span data-stu-id="0ac13-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0ac13-183">AzureClassicAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="0ac13-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="0ac13-184">Przykładowy graficzny element runbook, który pobiera wszystkie maszyny wirtualne tworzone za pomocą klasycznego modelu wdrożenia w subskrypcji przy użyciu klasycznego konta Uruchom jako (certyfikatu), a następnie zapisuje nazwę i stan maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0ac13-184">An example graphical runbook that gets all the VMs that are created using the classic deployment model in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span></span> |
| <span data-ttu-id="0ac13-185">AzureClassicAutomationTutorial Script Runbook</span><span class="sxs-lookup"><span data-stu-id="0ac13-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="0ac13-186">Przykładowy element runbook programu PowerShell, który pobiera wszystkie klasyczne maszyny wirtualne w subskrypcji przy użyciu klasycznego konta Uruchom jako (certyfikatu), a następnie zapisuje nazwę i stan maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0ac13-186">An example PowerShell runbook that gets all the classic VMs in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span></span> |
| <span data-ttu-id="0ac13-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="0ac13-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="0ac13-188">Automatycznie utworzony zasób certyfikatu, który służy do uwierzytelniania za pomocą platformy Azure, aby można było zarządzać klasycznymi zasobami platformy Azure z poziomu elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="0ac13-188">The automatically created certificate asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="0ac13-189">Certyfikat ma roczny okres obowiązywania.</span><span class="sxs-lookup"><span data-stu-id="0ac13-189">The certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="0ac13-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="0ac13-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="0ac13-191">Automatycznie utworzony zasób połączenia, który służy do uwierzytelniania za pomocą platformy Azure, aby można było zarządzać klasycznymi zasobami platformy Azure z poziomu elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="0ac13-191">The automatically created connection asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="0ac13-192">Sprawdzanie uwierzytelniania Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="0ac13-192">Verify Run As authentication</span></span>
<span data-ttu-id="0ac13-193">Wykonaj mały test, aby potwierdzić, że możesz pomyślnie przeprowadzić uwierzytelnienie przy użyciu nowego konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="0ac13-193">Perform a small test to confirm that you can successfully authenticate by using the new Run As account.</span></span>

1. <span data-ttu-id="0ac13-194">Otwórz utworzone wcześniej konto usługi Automation w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0ac13-194">In the Azure portal, open the Automation account that you created earlier.</span></span>

2. <span data-ttu-id="0ac13-195">Kliknij kafelek **Elementy runbook**, aby otworzyć listę elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="0ac13-195">Click the **Runbooks** tile to open the list of runbooks.</span></span>

3. <span data-ttu-id="0ac13-196">Wybierz element runbook **AzureAutomationTutorialScript**, a następnie kliknij pozycję **Start**, aby go uruchomić.</span><span class="sxs-lookup"><span data-stu-id="0ac13-196">Select the **AzureAutomationTutorialScript** runbook, and then click **Start** to start the runbook.</span></span> <span data-ttu-id="0ac13-197">Wystąpią następujące zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="0ac13-197">The following events occur:</span></span>
 * <span data-ttu-id="0ac13-198">Nastąpi utworzenie [zadania elementu runbook](automation-runbook-execution.md), wyświetlenie bloku **Zadanie** oraz wyświetlenie stanu zadania w kafelku **Podsumowanie zadania**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-198">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span></span>
 * <span data-ttu-id="0ac13-199">Zadanie będzie miało początkowy stan **W kolejce** oznaczający, że trwa oczekiwanie na udostępnienie procesu roboczego elementu runbook w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0ac13-199">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span></span>
 * <span data-ttu-id="0ac13-200">Stan zmieni się na **Uruchamianie**, gdy proces roboczy pobierze zadanie.</span><span class="sxs-lookup"><span data-stu-id="0ac13-200">The status becomes **Starting** when a worker claims the job.</span></span>
 * <span data-ttu-id="0ac13-201">Stan zmieni się na **Uruchomiono**, gdy element runbook zacznie działać.</span><span class="sxs-lookup"><span data-stu-id="0ac13-201">The status becomes **Running** when the runbook starts running.</span></span>
 * <span data-ttu-id="0ac13-202">Gdy zadanie elementu runbook zakończy działanie, powinniśmy zobaczyć stan **Ukończono**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-202">When the runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="0ac13-203">Aby wyświetlić szczegółowe wyniki elementu runbook, kliknij kafelek **Dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-203">To see the detailed results of the runbook, click the **Output** tile.</span></span>  
<span data-ttu-id="0ac13-204">Zostanie wyświetlony blok **Dane wyjściowe** z informacją o tym, że element runbook został pomyślnie uwierzytelniony, oraz zostanie zwrócona lista wszystkich zasobów dostępnych w tej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="0ac13-204">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all resources available in the resource group.</span></span>

5. <span data-ttu-id="0ac13-205">Zamknij blok **Dane wyjściowe**, aby wrócić do bloku **Podsumowanie zadania**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-205">Close the **Output** blade to return to the **Job Summary** blade.</span></span>

6. <span data-ttu-id="0ac13-206">Zamknij blok **Podsumowanie zadania** i odpowiedni blok elementu runbook **AzureAutomationTutorialScript**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-206">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="0ac13-207">Sprawdzanie klasycznego uwierzytelniania Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="0ac13-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="0ac13-208">Wykonaj podobny mały test, aby potwierdzić, że możesz pomyślnie przeprowadzić uwierzytelnienie przy użyciu nowego klasycznego konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="0ac13-208">Perform a similar small test to confirm that you can successfully authenticate by using the new Classic Run As account.</span></span>

1. <span data-ttu-id="0ac13-209">Otwórz utworzone wcześniej konto usługi Automation w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0ac13-209">In the Azure portal, open the Automation account that you created earlier.</span></span>

2. <span data-ttu-id="0ac13-210">Kliknij kafelek **Elementy runbook**, aby otworzyć listę elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="0ac13-210">Click the **Runbooks** tile to open the list of runbooks.</span></span>

3. <span data-ttu-id="0ac13-211">Wybierz element runbook **AzureClassicAutomationTutorialScript**, a następnie kliknij pozycję **Start**, aby go uruchomić.</span><span class="sxs-lookup"><span data-stu-id="0ac13-211">Select the **AzureClassicAutomationTutorialScript** runbook, and then click **Start** to  start the runbook.</span></span> <span data-ttu-id="0ac13-212">Wystąpią następujące zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="0ac13-212">The following events occur:</span></span>

 * <span data-ttu-id="0ac13-213">Nastąpi utworzenie [zadania elementu runbook](automation-runbook-execution.md), wyświetlenie bloku **Zadanie** oraz wyświetlenie stanu zadania w kafelku **Podsumowanie zadania**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-213">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span></span>
 * <span data-ttu-id="0ac13-214">Zadanie będzie miało początkowy stan **W kolejce** oznaczający, że trwa oczekiwanie na udostępnienie procesu roboczego elementu runbook w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0ac13-214">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span></span>
 * <span data-ttu-id="0ac13-215">Stan zmieni się na **Uruchamianie**, gdy proces roboczy pobierze zadanie.</span><span class="sxs-lookup"><span data-stu-id="0ac13-215">The status becomes **Starting** when a worker claims the job.</span></span>
 * <span data-ttu-id="0ac13-216">Stan zmieni się na **Uruchomiono**, gdy element runbook zacznie działać.</span><span class="sxs-lookup"><span data-stu-id="0ac13-216">The status becomes **Running** when the runbook starts running.</span></span>
 * <span data-ttu-id="0ac13-217">Gdy zadanie elementu runbook zakończy działanie, powinniśmy zobaczyć stan **Ukończono**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-217">When the runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![Test elementu Runbook zabezpieczeń](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="0ac13-219">Aby wyświetlić szczegółowe wyniki elementu runbook, kliknij kafelek **Dane wyjściowe**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-219">To see the detailed results of the runbook, click the **Output** tile.</span></span>  
<span data-ttu-id="0ac13-220">Zostanie wyświetlony blok **Dane wyjściowe** z informacją o tym, że element został pomyślnie uwierzytelniony, oraz zostanie zwrócona lista wszystkich klasycznych maszyn wirtualnych w subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0ac13-220">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all classic VMs in the subscription.</span></span>

5. <span data-ttu-id="0ac13-221">Zamknij blok **Dane wyjściowe**, aby wrócić do bloku **Podsumowanie zadania**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-221">Close the **Output** blade to return to the **Job Summary** blade.</span></span>

6. <span data-ttu-id="0ac13-222">Zamknij blok **Podsumowanie zadania** i odpowiedni blok elementu runbook **AzureAutomationTutorialScript**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-222">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="0ac13-223">Zarządzanie kontem Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="0ac13-223">Managing your Run As account</span></span>
<span data-ttu-id="0ac13-224">W pewnym momencie przed wygaśnięciem ważności konta usługi Automation należy odnowić certyfikat.</span><span class="sxs-lookup"><span data-stu-id="0ac13-224">At some point before your Automation account expires, you will need to renew the certificate.</span></span> <span data-ttu-id="0ac13-225">Jeśli uważasz, że bezpieczeństwo konta Uruchom jako zostało naruszone, możesz je usunąć i utworzyć ponownie.</span><span class="sxs-lookup"><span data-stu-id="0ac13-225">If you believe that the Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="0ac13-226">W tej sekcji opisano kroki umożliwiające wykonanie tych operacji.</span><span class="sxs-lookup"><span data-stu-id="0ac13-226">This section discusses how to perform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="0ac13-227">Odnawianie certyfikatu z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="0ac13-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="0ac13-228">Certyfikat z podpisem własnym utworzony dla konta Uruchom jako wygasa rok od daty utworzenia.</span><span class="sxs-lookup"><span data-stu-id="0ac13-228">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span></span> <span data-ttu-id="0ac13-229">Można go odnowić w dowolnym momencie przed wygaśnięciem jego ważności.</span><span class="sxs-lookup"><span data-stu-id="0ac13-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="0ac13-230">Po odnowieniu bieżący ważny certyfikat zostanie zachowany w celu zapewnienia, że ta zmiana nie wpłynie negatywnie na żadne umieszczone w kolejce lub aktywnie działające elementy runbook, które uwierzytelniają się przy użyciu konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="0ac13-230">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span></span> <span data-ttu-id="0ac13-231">Certyfikat pozostanie ważny aż do daty wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="0ac13-231">The certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="0ac13-232">Jeśli konto Uruchom jako usługi Automation skonfigurowano do użycia certyfikatu wystawionego przez urząd certyfikacji przedsiębiorstwa, w przypadku użycia tej opcji certyfikat przedsiębiorstwa zostanie zastąpiony certyfikatem z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="0ac13-232">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="0ac13-233">Aby odnowić certyfikat, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0ac13-233">To renew the certificate, do the following:</span></span>

1. <span data-ttu-id="0ac13-234">W witrynie Azure Portal otwórz konto usługi Automation.</span><span class="sxs-lookup"><span data-stu-id="0ac13-234">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="0ac13-235">W bloku **Konto usługi Automation** w okienku **Właściwości konta** w obszarze **Ustawienia konta** wybierz pozycję **Konta Uruchom jako**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-235">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Okienko właściwości konta usługi Automation](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="0ac13-237">W bloku właściwości **Konta Uruchom jako** wybierz konto Uruchom jako albo klasyczne konto Uruchom jako, dla którego chcesz odnowić certyfikat.</span><span class="sxs-lookup"><span data-stu-id="0ac13-237">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span></span>

4. <span data-ttu-id="0ac13-238">W bloku **Właściwości** wybranego konta kliknij pozycję **Odnów certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-238">On the **Properties** blade for the selected account, click **Renew certificate**.</span></span>

    ![Odnawianie certyfikatu konta Uruchom jako](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="0ac13-240">W trakcie odnawiania certyfikatu postęp można śledzić po wybraniu z menu opcji **Powiadomienia**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-240">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="0ac13-241">Usuwanie konta Uruchom jako lub klasycznego konta Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="0ac13-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="0ac13-242">W tej sekcji opisano sposób usuwania i ponownego tworzenia konta Uruchom jako lub klasycznego konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="0ac13-242">This section describes how to delete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="0ac13-243">Konto usługi Automation jest zachowywane podczas wykonywania tej akcji.</span><span class="sxs-lookup"><span data-stu-id="0ac13-243">When you perform this action, the Automation account is retained.</span></span> <span data-ttu-id="0ac13-244">Po usunięciu konta Uruchom jako lub klasycznego konta Uruchom jako możesz je ponownie utworzyć w witrynie Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0ac13-244">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span></span>

1. <span data-ttu-id="0ac13-245">W witrynie Azure Portal otwórz konto usługi Automation.</span><span class="sxs-lookup"><span data-stu-id="0ac13-245">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="0ac13-246">W bloku **Konto usługi Automation** w okienku właściwości konta wybierz pozycję **Konta Uruchom jako**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-246">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="0ac13-247">W bloku właściwości **Konta Uruchom jako** wybierz konto Uruchom jako albo klasyczne konto Uruchom jako, które chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="0ac13-247">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span></span> <span data-ttu-id="0ac13-248">Następnie w bloku **Właściwości** wybranego konta kliknij pozycję **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-248">Then, on the **Properties** blade for the selected account, click **Delete**.</span></span>

 ![Usuwanie konta Uruchom jako](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="0ac13-250">W trakcie usuwania konta postęp można śledzić po wybraniu z menu opcji **Powiadomienia**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-250">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span></span>

5. <span data-ttu-id="0ac13-251">Po usunięciu konta możesz je ponownie utworzyć w bloku właściwości **Konta Uruchom jako**, wybierając opcję tworzenia **Konto Uruchom jako platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-251">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span></span>

 ![Ponowne tworzenie konta Uruchom jako usługi Automation](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="0ac13-253">Błąd konfiguracji</span><span class="sxs-lookup"><span data-stu-id="0ac13-253">Misconfiguration</span></span>
<span data-ttu-id="0ac13-254">Niektóre elementy konfiguracji niezbędne do poprawnego działania konta Uruchom jako lub klasycznego konta Uruchom jako zostały usunięte lub nie zostały utworzone prawidłowo podczas początkowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0ac13-254">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="0ac13-255">Te elementy to na przykład:</span><span class="sxs-lookup"><span data-stu-id="0ac13-255">The items include:</span></span>

* <span data-ttu-id="0ac13-256">Zasób certyfikatu</span><span class="sxs-lookup"><span data-stu-id="0ac13-256">Certificate asset</span></span>
* <span data-ttu-id="0ac13-257">Zasób połączenia</span><span class="sxs-lookup"><span data-stu-id="0ac13-257">Connection asset</span></span>
* <span data-ttu-id="0ac13-258">Konto Uruchom jako zostało usunięte z roli współautora</span><span class="sxs-lookup"><span data-stu-id="0ac13-258">Run As account has been removed from the contributor role</span></span>
* <span data-ttu-id="0ac13-259">Nazwa główna usługi lub aplikacji w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ac13-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="0ac13-260">W poprzednim i innych przypadkach błędnej konfiguracji konto usługi Automation wykrywa te zmiany i wyświetla stan *Niekompletne* w bloku właściwości **Konta Uruchom jako** dla konta.</span><span class="sxs-lookup"><span data-stu-id="0ac13-260">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span></span>

![Stan Niekompletne dla konfiguracji konta Uruchom jako](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="0ac13-262">Po wybraniu konta Uruchom jako w okienku **Właściwości** konta zostanie wyświetlony następujący komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="0ac13-262">When you select the Run As account, the account **Properties** pane displays the following error message:</span></span>

![Komunikat ostrzegawczy Niekompletne dla konfiguracji konta Uruchom jako](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="0ac13-264">.</span><span class="sxs-lookup"><span data-stu-id="0ac13-264">.</span></span>

<span data-ttu-id="0ac13-265">Te problemy związane z kontem Uruchom jako można szybko rozwiązać, usuwając konto i tworząc je ponownie.</span><span class="sxs-lookup"><span data-stu-id="0ac13-265">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="0ac13-266">Aktualizacja konta usługi Automation przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ac13-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="0ac13-267">Istniejące konto usługi Automation można zaktualizować przy użyciu programu PowerShell, gdy:</span><span class="sxs-lookup"><span data-stu-id="0ac13-267">You can use PowerShell to update your existing Automation account if:</span></span>

* <span data-ttu-id="0ac13-268">Użytkownik utworzył konto usługi Automation, ale zrezygnował z tworzenia konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="0ac13-268">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="0ac13-269">Użytkownik używa już konta usługi Automation do zarządzania zasobami usługi Resource Manager i chce je zaktualizować, aby umożliwiało uwierzytelnianie elementu runbook za pomocą konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="0ac13-269">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="0ac13-270">Użytkownik używa już konta usługi Automation do zarządzania zasobami klasycznymi i chce je zaktualizować, aby używać klasycznego konta Uruchom jako, zamiast tworzenia nowego konta i migrowania do niego elementów runbook i zasobów.</span><span class="sxs-lookup"><span data-stu-id="0ac13-270">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="0ac13-271">Użytkownik chce utworzyć konto Uruchom jako i klasyczne konto Uruchom jako przy użyciu certyfikatu wystawionego przez urząd certyfikacji przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="0ac13-271">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="0ac13-272">Skrypt ma następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="0ac13-272">The script has the following prerequisites:</span></span>

* <span data-ttu-id="0ac13-273">Skrypt jest obsługiwany tylko w systemach Windows 10 i Windows Server 2016 z modułami usługi Azure Resource Manager w wersji 2.01 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="0ac13-273">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="0ac13-274">Nie jest obsługiwany przez wcześniejsze wersje systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="0ac13-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="0ac13-275">Program Azure PowerShell 1.0 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="0ac13-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="0ac13-276">Informacje o wersji PowerShell 1.0 można znaleźć w temacie [How to install and configure Azure PowerShell](/powershell/azure/overview) (Jak zainstalować i skonfigurować program Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="0ac13-276">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="0ac13-277">Konto usługi Automation, które jest przywoływane jako wartość parametrów *–AutomationAccountName* i *-ApplicationDisplayName* w poniższym skrypcie programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ac13-277">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="0ac13-278">Aby uzyskać wartości parametrów *SubscriptionID*, *ResourceGroup* i *AutomationAccountName*, które są wymagane w przypadku skryptów, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0ac13-278">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the scripts, do the following:</span></span>
1. <span data-ttu-id="0ac13-279">W witrynie Azure Portal wybierz konto usługi Automation w bloku **Konto usługi Automation**, a następnie wybierz pozycję **Wszystkie ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-279">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="0ac13-280">W bloku **Wszystkie ustawienia** w obszarze **Ustawienia konta** wybierz pozycję **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-280">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="0ac13-281">Zwróć uwagę na wartości w bloku **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="0ac13-281">Note the values on the **Properties** blade.</span></span>

![Okienko „Właściwości” konta usługi Automation](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="0ac13-283">Tworzenie skryptu programu PowerShell konta Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="0ac13-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="0ac13-284">Ten skrypt programu PowerShell obsługuje następujące konfiguracje:</span><span class="sxs-lookup"><span data-stu-id="0ac13-284">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="0ac13-285">Tworzenie konta Uruchom jako przy użyciu certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="0ac13-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="0ac13-286">Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="0ac13-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="0ac13-287">Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="0ac13-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="0ac13-288">Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu z podpisem własnym w chmurze usługi Azure Government.</span><span class="sxs-lookup"><span data-stu-id="0ac13-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="0ac13-289">W zależności od wybranej opcji konfiguracji skrypt tworzy poniższe elementy.</span><span class="sxs-lookup"><span data-stu-id="0ac13-289">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="0ac13-290">**W przypadku kont Uruchom jako:**</span><span class="sxs-lookup"><span data-stu-id="0ac13-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="0ac13-291">Tworzy aplikację Azure AD, która będzie eksportowana przy użyciu klucza publicznego certyfikatu z podpisem własnym lub certyfikatu przedsiębiorstwa, tworzy konto dla nazwy głównej usługi dla aplikacji w usłudze Azure AD i przypisuje rolę Współautor dla konta w bieżącej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0ac13-291">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="0ac13-292">To ustawienie możesz zmienić na rolę Właściciel lub inną.</span><span class="sxs-lookup"><span data-stu-id="0ac13-292">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="0ac13-293">Aby uzyskać więcej informacji, zobacz [Kontrola dostępu oparta na rolach w usłudze Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="0ac13-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="0ac13-294">Tworzy zasób certyfikatu usługi Automation o nazwie *AzureRunAsCertificate* na określonym koncie usługi Automation.</span><span class="sxs-lookup"><span data-stu-id="0ac13-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="0ac13-295">Zasób certyfikatu zawiera klucz prywatny certyfikatu używany przez aplikację Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ac13-295">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="0ac13-296">Tworzy zasób połączenia usługi Automation o nazwie *AzureRunAsConnection* na określonym koncie usługi Automation.</span><span class="sxs-lookup"><span data-stu-id="0ac13-296">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="0ac13-297">Zasób połączenia zawiera identyfikator aplikacji, identyfikator dzierżawy, identyfikator subskrypcji i odcisk palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0ac13-297">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="0ac13-298">**W przypadku klasycznych kont Uruchom jako:**</span><span class="sxs-lookup"><span data-stu-id="0ac13-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="0ac13-299">Tworzy zasób certyfikatu usługi Automation o nazwie *AzureClassicRunAsCertificate* na określonym koncie usługi Automation.</span><span class="sxs-lookup"><span data-stu-id="0ac13-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="0ac13-300">Zasób certyfikatu zawiera klucz prywatny certyfikatu używany przez certyfikat zarządzania.</span><span class="sxs-lookup"><span data-stu-id="0ac13-300">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="0ac13-301">Tworzy zasób połączenia usługi Automation o nazwie *AzureClassicRunAsConnection* na określonym koncie usługi Automation.</span><span class="sxs-lookup"><span data-stu-id="0ac13-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="0ac13-302">Zasób połączenia zawiera nazwę subskrypcji, identyfikator subskrypcji i nazwę zasobu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0ac13-302">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="0ac13-303">Jeśli wybierzesz dowolną opcję tworzenia klasycznego konta Uruchom jako, po wykonaniu skryptu przekaż certyfikat publiczny (z rozszerzeniem nazwy pliku CER) do magazynu zarządzania dla subskrypcji, w ramach której zostało utworzone konto usługi Automation.</span><span class="sxs-lookup"><span data-stu-id="0ac13-303">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

<span data-ttu-id="0ac13-304">Aby wykonać skrypt i przekazać certyfikat, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0ac13-304">To execute the script and upload the certificate, do the following:</span></span>

1. <span data-ttu-id="0ac13-305">Zapisz na komputerze poniższy skrypt.</span><span class="sxs-lookup"><span data-stu-id="0ac13-305">Save the following script on your computer.</span></span> <span data-ttu-id="0ac13-306">W tym przykładzie zapisz plik pod nazwą *New-RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="0ac13-306">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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

        # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
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
           Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate the ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload the .cer format of #CERT# to the Management store by following the steps below." + [Environment]::NewLine +
                    "Log in to the Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload the .cer format of #CERT#"

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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate the ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="0ac13-307">Na komputerze kliknij przycisk **Start**, a następnie uruchom program **Windows PowerShell** z podwyższonym poziomem uprawnień użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0ac13-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="0ac13-308">Z powłoki wiersza polecenia programu PowerShell z podwyższonym poziomem uprawnień użytkownika przejdź do folderu zawierającego skrypt utworzony w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="0ac13-308">From the elevated PowerShell command-line shell, go to the folder that contains the script you created in step 1.</span></span>

4. <span data-ttu-id="0ac13-309">Wykonaj skrypt, używając wartości parametrów wymaganej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0ac13-309">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="0ac13-310">**Tworzenie konta Uruchom jako przy użyciu certyfikatu z podpisem własnym**</span><span class="sxs-lookup"><span data-stu-id="0ac13-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="0ac13-311">**Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu z podpisem własnym**</span><span class="sxs-lookup"><span data-stu-id="0ac13-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="0ac13-312">**Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu przedsiębiorstwa**</span><span class="sxs-lookup"><span data-stu-id="0ac13-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="0ac13-313">**Tworzenie konta Uruchom jako i klasycznego konta Uruchom jako przy użyciu certyfikatu z podpisem własnym w chmurze usługi Azure Government**</span><span class="sxs-lookup"><span data-stu-id="0ac13-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="0ac13-314">Po wykonaniu skryptu pojawi się monit o uwierzytelnienie na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0ac13-314">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="0ac13-315">Zaloguj się przy użyciu konta, które jest członkiem roli Administratorzy subskrypcji i współadministratorem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0ac13-315">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="0ac13-316">Po pomyślnym wykonaniu skryptu pamiętaj o następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="0ac13-316">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="0ac13-317">Jeśli zostało utworzone klasyczne konto Uruchom jako z certyfikatem publicznym z podpisem własnym (plik CER), skrypt tworzy i zapisuje je w folderze plików tymczasowych na komputerze w ramach profilu użytkownika *%USERPROFILE%\AppData\Local\Temp* użytego do uruchomienia sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ac13-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="0ac13-318">Jeśli zostało utworzone klasyczne konto Uruchom jako z publicznym certyfikatem przedsiębiorstwa (plik CER), użyj tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0ac13-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="0ac13-319">Postępuj zgodnie z instrukcjami [przekazywania certyfikatu interfejsu API zarządzania do klasycznej witryny Azure Portal](../azure-api-management-certs.md), a następnie zweryfikuj konfigurację poświadczeń za pomocą zasobów usługi Service Management, używając [przykładowego kodu do uwierzytelniania za pośrednictwem zasobów usługi Service Management](#sample-code-to-authenticate-with-service-management-resources).</span><span class="sxs-lookup"><span data-stu-id="0ac13-319">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with Service Management resources by using the [sample code to authenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="0ac13-320">Jeśli klasyczne konto Uruchom jako *nie* zostało utworzone, uwierzytelnij się za pomocą zasobów usługi Resource Manager i zweryfikuj konfigurację poświadczeń, używając [przykładowego kodu do uwierzytelniania za pośrednictwem zasobów usługi Service Management](#sample-code-to-authenticate-with-resource-manager-resources).</span><span class="sxs-lookup"><span data-stu-id="0ac13-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-to-authenticate-with-resource-manager-resources"></a><span data-ttu-id="0ac13-321">Przykładowy kod służący do uwierzytelniania przy użyciu Menedżera zasobów</span><span class="sxs-lookup"><span data-stu-id="0ac13-321">Sample code to authenticate with Resource Manager resources</span></span>
<span data-ttu-id="0ac13-322">Możesz korzystać z następującego zaktualizowanego przykładowego kodu, pobranego z przykładowego elementu runbook *AzureAutomationTutorialScript*, w celu uwierzytelniania za pomocą konta Uruchom jako do zarządzania zasobami usługi Resource Manager przy użyciu elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="0ac13-322">You can use the following updated sample code, taken from the *AzureAutomationTutorialScript* example runbook, to authenticate by using the Run As account to manage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get the connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in to Azure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context to a specific subscription"     
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

<span data-ttu-id="0ac13-323">Aby ułatwić pracę z wieloma subskrypcjami, skrypt zawiera dwa dodatkowe wiersze kodu odwołujące się do kontekstu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0ac13-323">To help you to easily work between multiple subscriptions, the script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="0ac13-324">Zasób zmiennej o nazwie *SubscriptionId* zawiera identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0ac13-324">A variable asset named *SubscriptionId* contains the ID of the subscription.</span></span> <span data-ttu-id="0ac13-325">Po instrukcji polecenia cmdlet `Add-AzureRmAccount` znajduje się polecenie cmdlet [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) z zestawem parametrów *-SubscriptionId*.</span><span class="sxs-lookup"><span data-stu-id="0ac13-325">After the `Add-AzureRmAccount` cmdlet statement, the [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet is stated with the parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="0ac13-326">Jeśli nazwa zmiennej jest zbyt ogólna, można ją skorygować tak, aby dołączyć prefiks lub zastosować inną konwencję nazewnictwa w celu ułatwienia identyfikacji.</span><span class="sxs-lookup"><span data-stu-id="0ac13-326">If the variable name is too generic, you can revise it to include a prefix or use another naming convention to make it easier to identify.</span></span> <span data-ttu-id="0ac13-327">Alternatywnie można zastosować zestaw parametrów *-SubscriptionName* zamiast -*-SubscriptionId* z odpowiednim zasobem zmiennej.</span><span class="sxs-lookup"><span data-stu-id="0ac13-327">Alternatively, you can use the parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="0ac13-328">Polecenie cmdlet służące do uwierzytelniania w elemencie runbook, `Add-AzureRmAccount`, używa zestawu parametrów *ServicePrincipalCertificate*.</span><span class="sxs-lookup"><span data-stu-id="0ac13-328">The cmdlet that you use for authenticating in the runbook, `Add-AzureRmAccount`, uses the *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="0ac13-329">Uwierzytelnia się ono za pomocą certyfikatu nazwy głównej usługi, a nie poświadczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0ac13-329">It authenticates by using the service principal certificate, not the user credentials.</span></span>

## <a name="sample-code-to-authenticate-with-service-management-resources"></a><span data-ttu-id="0ac13-330">Przykładowy kod służący do uwierzytelniania przy użyciu zasobów usługi Service Management</span><span class="sxs-lookup"><span data-stu-id="0ac13-330">Sample code to authenticate with Service Management resources</span></span>
<span data-ttu-id="0ac13-331">Możesz skorzystać z następującego zaktualizowanego przykładowego kodu, pobranego z przykładowego elementu runbook *AzureClassicAutomationTutorialScript*, w celu uwierzytelniania za pomocą klasycznego konta Uruchom jako do zarządzania klasycznymi zasobami przy użyciu elementów runbook.</span><span class="sxs-lookup"><span data-stu-id="0ac13-331">You can use the following updated sample code, which is taken from the *AzureClassicAutomationTutorialScript* example runbook, to authenticate by using the Classic Run As account to manage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get the connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate to Azure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in the Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting the certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in the Automation account."
    }

    Write-Verbose "Authenticating to Azure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="0ac13-332">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0ac13-332">Next steps</span></span>
* <span data-ttu-id="0ac13-333">[Application and service principal objects in Azure AD](../active-directory/active-directory-application-objects.md) (Obiekty aplikacji i nazwy głównej usługi w usłudze Azure AD)</span><span class="sxs-lookup"><span data-stu-id="0ac13-333">[Application and service principal objects in Azure AD](../active-directory/active-directory-application-objects.md)</span></span>
* [<span data-ttu-id="0ac13-334">Kontrola dostępu oparta na rolach w usłudze Azure Automation</span><span class="sxs-lookup"><span data-stu-id="0ac13-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* <span data-ttu-id="0ac13-335">[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md) (Omówienie certyfikatów usług Azure Cloud Services)</span><span class="sxs-lookup"><span data-stu-id="0ac13-335">[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md)</span></span>
