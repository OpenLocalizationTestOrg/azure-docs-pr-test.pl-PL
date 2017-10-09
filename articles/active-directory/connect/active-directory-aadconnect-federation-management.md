---
title: "aaaActive Directory Federation Services zarządzania i dostosowywania z programem Azure AD Connect | Dokumentacja firmy Microsoft"
description: "Zarządzanie usługami AD FS z usługi Azure AD Connect i dostosowywania AD FS logowania użytkowników z usługi Azure AD Connect i programu PowerShell."
keywords: "Usługi AD FS, usługi AD FS, usługi AD FS zarządzania AAD Connect, Connect, logowania, usługi AD FS dostosowanie, napraw federacyjnej relacji zaufania, usługi O365, jednostki uzależnionej"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="6d863-104">Zarządzanie i dostosowania usług federacyjnych Active Directory przy użyciu usługi Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="6d863-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="6d863-105">W tym artykule opisano sposób toomanage i dostosować Active Directory Federation Services (AD FS) przy użyciu połączenia usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6d863-105">This article describes how toomanage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="6d863-106">Zawiera również innych typowych zadań usług AD FS, że może być konieczne toodo do ukończenia konfiguracji farmy usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="6d863-106">It also includes other common AD FS tasks that you might need toodo for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="6d863-107">Temat</span><span class="sxs-lookup"><span data-stu-id="6d863-107">Topic</span></span> | <span data-ttu-id="6d863-108">Co obejmuje</span><span class="sxs-lookup"><span data-stu-id="6d863-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="6d863-109">**Zarządzanie usługami AD FS**</span><span class="sxs-lookup"><span data-stu-id="6d863-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="6d863-110">Napraw hello zaufania</span><span class="sxs-lookup"><span data-stu-id="6d863-110">Repair hello trust</span></span>](#repairthetrust) |<span data-ttu-id="6d863-111">Jak toorepair hello federacyjnego zaufania z usługą Office 365.</span><span class="sxs-lookup"><span data-stu-id="6d863-111">How toorepair hello federation trust with Office 365.</span></span> |
| [<span data-ttu-id="6d863-112">Utworzenie federacji z usługą Azure AD przy użyciu alternatywnego Identyfikatora logowania</span><span class="sxs-lookup"><span data-stu-id="6d863-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="6d863-113">Konfigurowanie Federacji przy użyciu alternatywnego Identyfikatora logowania</span><span class="sxs-lookup"><span data-stu-id="6d863-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="6d863-114">Dodawanie serwera usług AD FS</span><span class="sxs-lookup"><span data-stu-id="6d863-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="6d863-115">Jak tooexpand usług AD FS farmy dodatkowy serwer usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="6d863-115">How tooexpand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="6d863-116">Dodaj serwer Proxy aplikacji sieci Web usług AD FS</span><span class="sxs-lookup"><span data-stu-id="6d863-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="6d863-117">Jak tooexpand usług AD FS farmy dodatkowy serwer Proxy aplikacji sieci Web (WAP).</span><span class="sxs-lookup"><span data-stu-id="6d863-117">How tooexpand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="6d863-118">Dodawanie domeny federacyjnej</span><span class="sxs-lookup"><span data-stu-id="6d863-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="6d863-119">Jak tooadd domeny federacyjnej.</span><span class="sxs-lookup"><span data-stu-id="6d863-119">How tooadd a federated domain.</span></span> |
| [<span data-ttu-id="6d863-120">Certyfikat SSL hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="6d863-120">Update hello SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="6d863-121">Jak tooupdate hello SSL certyfikatów dla farmy usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="6d863-121">How tooupdate hello SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="6d863-122">**Dostosowywanie usług AD FS**</span><span class="sxs-lookup"><span data-stu-id="6d863-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="6d863-123">Dodać logo firmy lub ilustracji</span><span class="sxs-lookup"><span data-stu-id="6d863-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="6d863-124">Sposób logowania usług AD FS toocustomize strony z firmowego logo i ilustracja.</span><span class="sxs-lookup"><span data-stu-id="6d863-124">How toocustomize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="6d863-125">Dodaj opis logowania</span><span class="sxs-lookup"><span data-stu-id="6d863-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="6d863-126">Jak opis strony tooadd logowania.</span><span class="sxs-lookup"><span data-stu-id="6d863-126">How tooadd a sign-in page description.</span></span> |
| [<span data-ttu-id="6d863-127">Modyfikowanie reguł oświadczeń usług AD FS</span><span class="sxs-lookup"><span data-stu-id="6d863-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="6d863-128">Jak toomodify usług AD FS oświadczeń dla różnych scenariuszy federacji.</span><span class="sxs-lookup"><span data-stu-id="6d863-128">How toomodify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="6d863-129">Zarządzanie usługami AD FS</span><span class="sxs-lookup"><span data-stu-id="6d863-129">Manage AD FS</span></span>
<span data-ttu-id="6d863-130">Za pomocą kreatora Połącz hello Azure AD, można wykonywać różne AD FS dotyczące zadania w programie Azure AD Connect z użytkownika minimalnej interwencji.</span><span class="sxs-lookup"><span data-stu-id="6d863-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using hello Azure AD Connect wizard.</span></span> <span data-ttu-id="6d863-131">Po zakończeniu instalowania usługi Azure AD Connect uruchomiony Kreator hello hello kreatora można uruchomić ponownie tooperform dodatkowe zadania.</span><span class="sxs-lookup"><span data-stu-id="6d863-131">After you've finished installing Azure AD Connect by running hello wizard, you can run hello wizard again tooperform additional tasks.</span></span>

## <span data-ttu-id="6d863-132">Napraw hello zaufania<a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="6d863-132">Repair hello trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="6d863-133">Można użyć usługi Azure AD Connect toocheck hello bieżącą kondycję hello usług AD FS i zaufania usługi Azure AD i podjąć odpowiednie działania toorepair hello zaufania.</span><span class="sxs-lookup"><span data-stu-id="6d863-133">You can use Azure AD Connect toocheck hello current health of hello AD FS and Azure AD trust and take appropriate actions toorepair hello trust.</span></span> <span data-ttu-id="6d863-134">Wykonaj te kroki toorepair Azure AD i usług AD FS zaufania.</span><span class="sxs-lookup"><span data-stu-id="6d863-134">Follow these steps toorepair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="6d863-135">Wybierz **AAD naprawy i zaufania usług AD FS** z listy hello dodatkowe zadania.</span><span class="sxs-lookup"><span data-stu-id="6d863-135">Select **Repair AAD and ADFS Trust** from hello list of additional tasks.</span></span>
   <span data-ttu-id="6d863-136">![Napraw AAD i usług AD FS zaufania](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="6d863-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="6d863-137">Na powitania **połączyć tooAzure AD** , podaj poświadczenia administratora globalnego dla usługi Azure AD i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6d863-137">On hello **Connect tooAzure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="6d863-138">![Połącz tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="6d863-138">![Connect tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="6d863-139">Na powitania **poświadczeń dostępu zdalnego** wprowadź poświadczenia hello hello administratora domeny.</span><span class="sxs-lookup"><span data-stu-id="6d863-139">On hello **Remote access credentials** page, enter hello credentials for hello domain administrator.</span></span>

   ![Poświadczenia dostępu zdalnego](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="6d863-141">Po kliknięciu **dalej**, Azure AD Connect sprawdza, czy certyfikat kondycji i zawiera wszystkie problemy.</span><span class="sxs-lookup"><span data-stu-id="6d863-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![Stan certyfikatów](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="6d863-143">Witaj **tooconfigure gotowe** strony pokazuje hello listę działań, które będą wykonywane toorepair hello zaufania.</span><span class="sxs-lookup"><span data-stu-id="6d863-143">hello **Ready tooconfigure** page shows hello list of actions that will be performed toorepair hello trust.</span></span>

    ![Gotowe tooconfigure](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="6d863-145">Kliknij przycisk **zainstalować** toorepair hello zaufania.</span><span class="sxs-lookup"><span data-stu-id="6d863-145">Click **Install** toorepair hello trust.</span></span>

> [!NOTE]
> <span data-ttu-id="6d863-146">Azure AD Connect może tylko naprawy lub ustawy o certyfikaty z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="6d863-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="6d863-147">Azure AD Connect nie może naprawić certyfikatów innych firm.</span><span class="sxs-lookup"><span data-stu-id="6d863-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="6d863-148">Utworzenie federacji z usługą Azure AD przy użyciu AlternateID<a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="6d863-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="6d863-149">Zaleca się, że hello lokalnego Name(UPN) głównej nazwy użytkownika i chmury hello główna nazwa użytkownika są przechowywane hello takie same.</span><span class="sxs-lookup"><span data-stu-id="6d863-149">It is recommended that hello on-premises User Principal Name(UPN) and hello cloud User Principal Name are kept hello same.</span></span> <span data-ttu-id="6d863-150">Jeśli hello UPN lokalnymi używa nierutowalny domeny (np.</span><span class="sxs-lookup"><span data-stu-id="6d863-150">If hello on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="6d863-151">Contoso.local) lub nie można zmienić powodu toolocal zależności aplikacji, zaleca się konfigurowanie alternatywnego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="6d863-151">Contoso.local) or cannot be changed due toolocal application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="6d863-152">Alternatywnego Identyfikatora logowania umożliwia tooconfigure Obsługa logowania w którym użytkownicy mogą logować się przy użyciu atrybutu innego niż ich nazwy UPN, taki jak adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="6d863-152">Alternate login ID allows you tooconfigure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="6d863-153">Wybór Hello do głównej nazwy użytkownika w atrybut userPrincipalName toohello domyślne Azure AD Connect w usłudze Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6d863-153">hello choice for User Principal Name in Azure AD Connect defaults toohello userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="6d863-154">Jeśli możesz wybrać inny atrybut główna nazwa użytkownika i Federacji przy użyciu usług AD FS, następnie Azure AD Connect konfiguracji usług AD FS dla alternatywny identyfikator.</span><span class="sxs-lookup"><span data-stu-id="6d863-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="6d863-155">Poniżej przedstawiono przykład wybranie innego atrybutu główna nazwa użytkownika:</span><span class="sxs-lookup"><span data-stu-id="6d863-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![Alternatywny identyfikator atrybutu zaznaczenia](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="6d863-157">Konfigurowanie alternatywnego Identyfikatora logowania dla usług AD FS składa się z dwóch głównych czynności:</span><span class="sxs-lookup"><span data-stu-id="6d863-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="6d863-158">**Skonfiguruj hello prawidłowego zestawu wystawiania oświadczeń**: hello wystawiania oświadczeń reguły w jednostce uzależnionej hello Azure AD zaufania, są atrybutu UserPrincipalName hello wybrane toouse zmodyfikowane, jak hello alternatywny identyfikator użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="6d863-158">**Configure hello right set of issuance claims**: hello issuance claim rules in hello Azure AD relying party trust are modified toouse hello selected UserPrincipalName attribute as hello alternate ID of hello user.</span></span>
2. <span data-ttu-id="6d863-159">**Włącz alternatywnego Identyfikatora logowania w konfiguracji usług AD FS hello**: hello AD FS konfiguracji zostaną zmienione tak, aby usługi AD FS można wyszukiwać użytkowników w lasach odpowiednie hello przy użyciu hello alternatywnego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="6d863-159">**Enable alternate login ID in hello AD FS configuration**: hello AD FS configuration is updated so that AD FS can look up users in hello appropriate forests using hello alternate ID.</span></span> <span data-ttu-id="6d863-160">Ta konfiguracja jest obsługiwana dla usług AD FS w systemie Windows Server 2012 R2 (z KB2919355) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="6d863-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="6d863-161">Jeśli serwery usług hello AD FS 2012 R2, Azure AD Connect sprawdza obecność hello hello wymagane KB.</span><span class="sxs-lookup"><span data-stu-id="6d863-161">If hello AD FS servers are 2012 R2, Azure AD Connect checks for hello presence of hello required KB.</span></span> <span data-ttu-id="6d863-162">Jeśli hello KB nie zostanie wykryta, ostrzeżenie będzie wyświetlana po zakończeniu konfiguracji, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="6d863-162">If hello KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![Ostrzeżenie dotyczące Brak KB na 2012 R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="6d863-164">toorectify hello konfiguracji w przypadku brakujących KB, zainstaluj hello wymagane [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) , a następnie napraw hello zaufania przy użyciu [napraw AAD i AD FS zaufania](#repairthetrust).</span><span class="sxs-lookup"><span data-stu-id="6d863-164">toorectify hello configuration in case of missing KB, install hello required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair hello trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="6d863-165">Aby uzyskać więcej informacji na toomanually alternateID i kroki konfigurowania, odczytać [Konfigurowanie alternatywnego Identyfikatora logowania](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span><span class="sxs-lookup"><span data-stu-id="6d863-165">For more information on alternateID and steps toomanually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="6d863-166">Dodawanie serwera usług AD FS<a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="6d863-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="6d863-167">Serwer tooadd usług AD FS, Azure AD Connect wymaga hello certyfikat PFX.</span><span class="sxs-lookup"><span data-stu-id="6d863-167">tooadd an AD FS server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="6d863-168">W związku z tym tę operację mogą wykonać tylko wtedy, gdy hello AD FS farmy jest konfigurowana przy użyciu usługi Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6d863-168">Therefore, you can perform this operation only if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="6d863-169">Wybierz **wdrażanie dodatkowego serwera federacyjnego**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6d863-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![Serwer federacyjny dodatkowe](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="6d863-171">Na powitania **połączyć tooAzure AD** strony, wprowadź swoje poświadczenia administratora globalnego dla usługi Azure AD, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6d863-171">On hello **Connect tooAzure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![Połącz tooAzure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="6d863-173">Podaj poświadczenia administratora domeny hello.</span><span class="sxs-lookup"><span data-stu-id="6d863-173">Provide hello domain administrator credentials.</span></span>

   ![Podane poświadczenia administratora domeny](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="6d863-175">Azure AD Connect pytanie o hasło hello hello pliku PFX, podane podczas konfigurowania nowej farmie serwerów usług AD FS z programem Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6d863-175">Azure AD Connect asks for hello password of hello PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="6d863-176">Kliknij przycisk **wprowadź hasło** tooprovide hello hasło dla pliku PFX hello.</span><span class="sxs-lookup"><span data-stu-id="6d863-176">Click **Enter Password** tooprovide hello password for hello PFX file.</span></span>

   ![Hasło certyfikatu](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Określ certyfikat SSL](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="6d863-179">Na powitania **serwery usług AD FS** wpisz nazwę serwera hello lub dodać toobe adres IP toohello AD FS farmy.</span><span class="sxs-lookup"><span data-stu-id="6d863-179">On hello **AD FS Servers** page, enter hello server name or IP address toobe added toohello AD FS farm.</span></span>

   ![Serwery usług AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="6d863-181">Kliknij przycisk **dalej**i wykonaj hello końcowego **Konfiguruj** strony.</span><span class="sxs-lookup"><span data-stu-id="6d863-181">Click **Next**, and go through hello final **Configure** page.</span></span> <span data-ttu-id="6d863-182">Po zakończeniu Azure AD Connect Dodawanie hello serwerów toohello AD FS farmy, będziesz mieć możliwość hello opcja tooverify hello łączności.</span><span class="sxs-lookup"><span data-stu-id="6d863-182">After Azure AD Connect has finished adding hello servers toohello AD FS farm, you will be given hello option tooverify hello connectivity.</span></span>

   ![Gotowe tooconfigure](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Zakończenie instalacji](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="6d863-185">Dodaj serwer AD FS WAP<a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="6d863-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="6d863-186">tooadd serwerowi proxy aplikacji Azure AD Connect wymaga hello certyfikat PFX.</span><span class="sxs-lookup"><span data-stu-id="6d863-186">tooadd a WAP server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="6d863-187">W związku z tym można wykonać tylko tej operacji po skonfigurowaniu hello AD FS farmy przy użyciu usługi Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6d863-187">Therefore, you can only perform this operation if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="6d863-188">Wybierz **wdrażanie Proxy aplikacji sieci Web** z hello listę dostępnych zadań.</span><span class="sxs-lookup"><span data-stu-id="6d863-188">Select **Deploy Web Application Proxy** from hello list of available tasks.</span></span>

   ![Wdrożenie serwera Proxy aplikacji sieci Web](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="6d863-190">Podaj poświadczenia administratora globalnego usługi Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6d863-190">Provide hello Azure global administrator credentials.</span></span>

   ![Połącz tooAzure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="6d863-192">Na powitania **certyfikat SSL określ** Podaj hello hasło dla pliku PFX hello podane podczas konfigurowania farmy usług hello AD FS z programem Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6d863-192">On hello **Specify SSL certificate** page, provide hello password for hello PFX file that you provided when you configured hello AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="6d863-193">![Hasło certyfikatu](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="6d863-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![Określ certyfikat SSL](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="6d863-195">Dodaj powitania serwera toobe dodany jako serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="6d863-195">Add hello server toobe added as a WAP server.</span></span> <span data-ttu-id="6d863-196">Ponieważ hello serwerowi proxy mogą nie być toohello przyłączone do domeny, Kreator hello poprosi o dodawany serwer toohello poświadczenia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="6d863-196">Because hello WAP server might not be joined toohello domain, hello wizard asks for administrative credentials toohello server being added.</span></span>

   ![Poświadczenia administracyjne serwera](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="6d863-198">Na powitania **poświadczeń zaufania serwera Proxy** Podaj poświadczenia administracyjne tooconfigure hello proxy zaufania i dostępu do serwera podstawowego hello w farmie hello usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="6d863-198">On hello **Proxy trust credentials** page, provide administrative credentials tooconfigure hello proxy trust and access hello primary server in hello AD FS farm.</span></span>

   ![Poświadczenia zaufania serwera proxy](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="6d863-200">Na powitania **tooconfigure gotowe** strony, Kreator hello listą hello akcje, które będą wykonywane.</span><span class="sxs-lookup"><span data-stu-id="6d863-200">On hello **Ready tooconfigure** page, hello wizard shows hello list of actions that will be performed.</span></span>

   ![Gotowe tooconfigure](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="6d863-202">Kliknij przycisk **zainstalować** toofinish hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6d863-202">Click **Install** toofinish hello configuration.</span></span> <span data-ttu-id="6d863-203">Po ukończeniu konfiguracji hello hello kreatora daje hello tooverify opcji hello łączności toohello serwerów.</span><span class="sxs-lookup"><span data-stu-id="6d863-203">After hello configuration is complete, hello wizard gives you hello option tooverify hello connectivity toohello servers.</span></span> <span data-ttu-id="6d863-204">Kliknij przycisk **Sprawdź** toocheck łączności.</span><span class="sxs-lookup"><span data-stu-id="6d863-204">Click **Verify** toocheck connectivity.</span></span>

   ![Zakończenie instalacji](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="6d863-206">Dodawanie domeny federacyjnej<a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="6d863-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="6d863-207">Jest łatwy tooadd toobe domeny Sfederowanych z usługą Azure AD za pomocą usługi Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6d863-207">It's easy tooadd a domain toobe federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="6d863-208">Azure AD Connect dodaje hello domeny dla Federacji i modyfikuje oświadczenia hello toocorrectly reguły odzwierciedlają hello wystawcy, jeśli masz wiele domen federacyjnych z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d863-208">Azure AD Connect adds hello domain for federation and modifies hello claim rules toocorrectly reflect hello issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="6d863-209">tooadd domeny federacyjnej, wybierz hello zadań **Dodawanie kolejnej domeny usługi Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="6d863-209">tooadd a federated domain, select hello task **Add an additional Azure AD domain**.</span></span>

   ![Dodatkowe domeny usługi Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="6d863-211">Na następnej stronie powitania hello kreatora należy podać poświadczenia administratora globalnego powitania dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d863-211">On hello next page of hello wizard, provide hello global administrator credentials for Azure AD.</span></span>

   ![Połącz tooAzure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="6d863-213">Na powitania **poświadczeń dostępu zdalnego** Podaj poświadczenia administratora domeny hello.</span><span class="sxs-lookup"><span data-stu-id="6d863-213">On hello **Remote access credentials** page, provide hello domain administrator credentials.</span></span>

   ![Poświadczenia dostępu zdalnego](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="6d863-215">Na następnej stronie powitania Kreatora hello zawiera listę domen usługi Azure AD, które można było wykonać Federację lokalnego katalogu z.</span><span class="sxs-lookup"><span data-stu-id="6d863-215">On hello next page, hello wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="6d863-216">Wybierz domenę hello z listy hello.</span><span class="sxs-lookup"><span data-stu-id="6d863-216">Choose hello domain from hello list.</span></span>

   ![Domenowych Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="6d863-218">Po wybraniu domeny hello kreatora hello zawiera odpowiednie informacje o dalsze akcje, które hello Kreator będzie trwać i hello wpływ hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6d863-218">After you choose hello domain, hello wizard provides you with appropriate information about further actions that hello wizard will take and hello impact of hello configuration.</span></span> <span data-ttu-id="6d863-219">W niektórych przypadkach w przypadku wybrania domeny, która jeszcze nie jest zweryfikowana w usłudze Azure AD, Kreator hello zapewnia informacje toohelp sprawdzisz hello domeny.</span><span class="sxs-lookup"><span data-stu-id="6d863-219">In some cases, if you select a domain that isn't yet verified in Azure AD, hello wizard provides you with information toohelp you verify hello domain.</span></span> <span data-ttu-id="6d863-220">Zobacz [tooAzure nazwa Twojej niestandardową domenę usługi Active Directory dodać](../active-directory-add-domain.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="6d863-220">See [Add your custom domain name tooAzure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="6d863-221">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="6d863-221">Click **Next**.</span></span> <span data-ttu-id="6d863-222">Witaj **tooconfigure gotowe** strony hello Lista akcji, które wykona Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6d863-222">hello **Ready tooconfigure** page shows hello list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="6d863-223">Kliknij przycisk **zainstalować** toofinish hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6d863-223">Click **Install** toofinish hello configuration.</span></span>

   ![Gotowe tooconfigure](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="6d863-225">Użytkownicy z hello dodać musi być synchronizowany domeny federacyjnej, zanim będą oni mogli toologin tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="6d863-225">Users from hello added federated domain must be synchronized before they will be able toologin tooAzure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="6d863-226">Dostosowania usług AD FS</span><span class="sxs-lookup"><span data-stu-id="6d863-226">AD FS customization</span></span>
<span data-ttu-id="6d863-227">Witaj poniższe sekcje zawierają szczegółowe informacje o niektórych typowych zadań hello może mieć tooperform podczas dostosowywania strony logowania usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="6d863-227">hello following sections provide details about some of hello common tasks that you might have tooperform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="6d863-228">Dodać logo firmy lub ilustracji<a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="6d863-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="6d863-229">toochange hello logo firmy hello, który jest wyświetlany na powitania **logowania** strony, należy użyć następującego polecenia cmdlet programu Windows PowerShell i składni hello.</span><span class="sxs-lookup"><span data-stu-id="6d863-229">toochange hello logo of hello company that's displayed on hello **Sign-in** page, use hello following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="6d863-230">Witaj zalecane wymiary hello logo to 260 x 35 przy rozdzielczości 96 dpi w pliku o rozmiarze nie większym niż 10 KB.</span><span class="sxs-lookup"><span data-stu-id="6d863-230">hello recommended dimensions for hello logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="6d863-231">Witaj *TargetName* parametr jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="6d863-231">hello *TargetName* parameter is required.</span></span> <span data-ttu-id="6d863-232">Witaj motyw domyślny publikowany z usługami AD FS nosi nazwę domyślny.</span><span class="sxs-lookup"><span data-stu-id="6d863-232">hello default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="6d863-233">Dodaj opis logowania<a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="6d863-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="6d863-234">tooadd toohello opisu strony logowania **strony logowania**, użyj następującego polecenia cmdlet programu Windows PowerShell i składni hello.</span><span class="sxs-lookup"><span data-stu-id="6d863-234">tooadd a sign-in page description toohello **Sign-in page**, use hello following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="6d863-235">Modyfikowanie reguł oświadczeń usług AD FS<a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="6d863-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="6d863-236">Usługi AD FS obsługują język sformatowanego oświadczeń można użyć toocreate niestandardowych reguł oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="6d863-236">AD FS supports a rich claim language that you can use toocreate custom claim rules.</span></span> <span data-ttu-id="6d863-237">Aby uzyskać więcej informacji, zobacz [hello roli hello języka reguł oświadczeń](https://technet.microsoft.com/library/dd807118.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d863-237">For more information, see [hello Role of hello Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="6d863-238">Witaj poniższych sekcjach opisano sposób można zapisać reguły niestandardowe dla niektórych scenariuszy, które są powiązane tooAzure AD i federacji usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="6d863-238">hello following sections describe how you can write custom rules for some scenarios that relate tooAzure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a><span data-ttu-id="6d863-239">Warunkowe na wartość jest obecny w atrybucie hello niezmienialnego Identyfikatora</span><span class="sxs-lookup"><span data-stu-id="6d863-239">Immutable ID conditional on a value being present in hello attribute</span></span>
<span data-ttu-id="6d863-240">Azure AD Connect umożliwia określenie toobe atrybutu używany jako zakotwiczenie źródła, gdy obiekty są synchronizowane tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="6d863-240">Azure AD Connect lets you specify an attribute toobe used as a source anchor when objects are synced tooAzure AD.</span></span> <span data-ttu-id="6d863-241">Jeśli wartość hello w atrybucie niestandardowym hello nie jest pusta, można tooissue niezmienne oświadczenie Identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="6d863-241">If hello value in hello custom attribute is not empty, you might want tooissue an immutable ID claim.</span></span>

<span data-ttu-id="6d863-242">Na przykład możesz wybrać pozycję **ms-ds-consistencyguid** jako atrybut hello zakotwiczenie źródła hello oraz wydawania **nazwę ImmutableID** jako **consistencyguid-ms-ds** w przypadku hello atrybut ma wartość na nim.</span><span class="sxs-lookup"><span data-stu-id="6d863-242">For example, you might select **ms-ds-consistencyguid** as hello attribute for hello source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case hello attribute has a value against it.</span></span> <span data-ttu-id="6d863-243">Jeśli nie ma żadnej wartości dla atrybutu hello, **objectGuid** jako hello niezmienne identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="6d863-243">If there's no value against hello attribute, issue **objectGuid** as hello immutable ID.</span></span> <span data-ttu-id="6d863-244">Zgodnie z opisem w następujących sekcji hello można konstruować hello zestaw niestandardowych reguł oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="6d863-244">You can construct hello set of custom claim rules as described in hello following section.</span></span>

<span data-ttu-id="6d863-245">**Reguła 1: Atrybuty zapytania**</span><span class="sxs-lookup"><span data-stu-id="6d863-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="6d863-246">W tej regule, w przypadku badania wartości hello **ms-ds-consistencyguid** i **objectGuid** hello użytkownika z usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6d863-246">In this rule, you're querying hello values of **ms-ds-consistencyguid** and **objectGuid** for hello user from Active Directory.</span></span> <span data-ttu-id="6d863-247">Zmień nazwę odpowiedniego sklepu hello magazynu Nazwa tooan we wdrożeniu usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="6d863-247">Change hello store name tooan appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="6d863-248">Również zmienić hello oświadczeń tooa oświadczeń prawidłowego typu dla federacyjnym, zgodnie z definicją **objectGuid** i **consistencyguid-ms-ds**.</span><span class="sxs-lookup"><span data-stu-id="6d863-248">Also change hello claims type tooa proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="6d863-249">Ponadto za pomocą **dodać** i nie **problem**, unikać dodawania wychodzących problemem w przypadku jednostki hello i użyć hello wartości jako wartości pośrednich.</span><span class="sxs-lookup"><span data-stu-id="6d863-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for hello entity, and can use hello values as intermediate values.</span></span> <span data-ttu-id="6d863-250">Będzie wystawiać oświadczenia hello w regule nowsze po ustaleniu które toouse wartość jako hello niezmienne identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="6d863-250">You will issue hello claim in a later rule after you establish which value toouse as hello immutable ID.</span></span>

<span data-ttu-id="6d863-251">**Reguła 2: Sprawdź, czy consistencyguid-ms-ds istnieje hello użytkownika**</span><span class="sxs-lookup"><span data-stu-id="6d863-251">**Rule 2: Check if ms-ds-consistencyguid exists for hello user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="6d863-252">Ta zasada definiuje tymczasowe flagę o nazwie **idflag** który ustawiono zbyt**useguid** w przypadku nie **consistencyguid-ms-ds** wypełnione hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6d863-252">This rule defines a temporary flag called **idflag** that is set too**useguid** if there's no **ms-ds-consistencyguid** populated for hello user.</span></span> <span data-ttu-id="6d863-253">Witaj logiki to jest hello fakt, że usługi AD FS nie zezwala na puste oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="6d863-253">hello logic behind this is hello fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="6d863-254">Dlatego po dodaniu http://contoso.com/ws/2016/02/identity/claims/objectguid oświadczeń i http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid w reguła 1 na końcu **msdsconsistencyguid** oświadczenia tylko wtedy, gdy wartość Hello jest wypełniana hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6d863-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if hello value is populated for hello user.</span></span> <span data-ttu-id="6d863-255">Jeśli go nie jest wypełnione, będzie mieć wartość pustą i odrzuca pochodzące od razu będzie widział usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="6d863-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="6d863-256">Wszystkie obiekty będą mieć **objectGuid**, więc roszczenie zawsze będą dostępne po wykonaniu reguła 1.</span><span class="sxs-lookup"><span data-stu-id="6d863-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="6d863-257">**Reguła 3: Wystawiać ms-ds-consistencyguid jako niezmienialnego Identyfikatora, jeśli jest obecny**</span><span class="sxs-lookup"><span data-stu-id="6d863-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="6d863-258">To jest niejawnie **Exist** Sprawdź.</span><span class="sxs-lookup"><span data-stu-id="6d863-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="6d863-259">Jeśli istnieje wartość hello hello oświadczenia, następnie wystawiania, która jako niezmienialny hello identyfikator.</span><span class="sxs-lookup"><span data-stu-id="6d863-259">If hello value for hello claim exists, then issue that as hello immutable ID.</span></span> <span data-ttu-id="6d863-260">Witaj poprzednim przykładzie użyto hello **nameidentifier** oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="6d863-260">hello previous example uses hello **nameidentifier** claim.</span></span> <span data-ttu-id="6d863-261">Będziesz mieć toochange tego typu oświadczenia właściwe toohello dla Identyfikatora niezmienne hello w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="6d863-261">You'll have toochange this toohello appropriate claim type for hello immutable ID in your environment.</span></span>

<span data-ttu-id="6d863-262">**Reguła 4: Jeśli consistencyGuid-ms-ds nie jest obecny Wystaw objectGuid jako niezmienialnego Identyfikatora**</span><span class="sxs-lookup"><span data-stu-id="6d863-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="6d863-263">W tej regule, sprawdzamy po prostu flagę tymczasowego hello **idflag**.</span><span class="sxs-lookup"><span data-stu-id="6d863-263">In this rule, you're simply checking hello temporary flag **idflag**.</span></span> <span data-ttu-id="6d863-264">Zdecyduj, czy oparta na oświadczeniach hello tooissue na jego wartość.</span><span class="sxs-lookup"><span data-stu-id="6d863-264">You decide whether tooissue hello claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="6d863-265">ważne jest sekwencji Hello tych zasad.</span><span class="sxs-lookup"><span data-stu-id="6d863-265">hello sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="6d863-266">Usługa rejestracji Jednokrotnej z poddomeny nazwy UPN</span><span class="sxs-lookup"><span data-stu-id="6d863-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="6d863-267">Możesz dodać więcej niż jeden toobe domeny federacyjnej przy użyciu usługi Azure AD Connect, zgodnie z opisem w [Dodaj nową domenę federacyjną](active-directory-aadconnect-federation-management.md#addfeddomain).</span><span class="sxs-lookup"><span data-stu-id="6d863-267">You can add more than one domain toobe federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="6d863-268">Należy zmodyfikować oświadczenia głównej nazwy (UPN) użytkownika hello tak, aby hello identyfikator wystawcy odpowiada domeny głównej toohello i nie hello poddomen, ponieważ hello federacyjnych główny domeny obejmuje również hello podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="6d863-268">You must modify hello user principal name (UPN) claim so that hello issuer ID corresponds toohello root domain and not hello subdomain, because hello federated root domain also covers hello child.</span></span>

<span data-ttu-id="6d863-269">Domyślnie reguł oświadczeń hello wystawcy Identyfikatora jest ustawiony jako:</span><span class="sxs-lookup"><span data-stu-id="6d863-269">By default, hello claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Oświadczenie Identyfikatora wystawcy domyślne](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="6d863-271">Hello domyślną regułę po prostu przyjmuje hello sufiks głównej nazwy użytkownika i używa go w Witaj wystawca identyfikator oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="6d863-271">hello default rule simply takes hello UPN suffix and uses it in hello issuer ID claim.</span></span> <span data-ttu-id="6d863-272">Na przykład Jan jest użytkownikiem w sub.contoso.com i contoso.com jest Sfederowane przy użyciu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d863-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="6d863-273">Jan wprowadza john@sub.contoso.com jako hello nazwy użytkownika podczas logowania tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="6d863-273">John enters john@sub.contoso.com as hello username while signing in tooAzure AD.</span></span> <span data-ttu-id="6d863-274">Hello domyślne wystawcy identyfikator reguły oświadczeń w usługach AD FS obsługuje on powitania po sposób:</span><span class="sxs-lookup"><span data-stu-id="6d863-274">hello default issuer ID claim rule in AD FS handles it in hello following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="6d863-275">**Wartość oświadczenia:** http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="6d863-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="6d863-276">toohave tylko hello domenie głównej Witaj wystawca wartości oświadczenia, hello oświadczeń reguła toomatch hello następujące zmiany:</span><span class="sxs-lookup"><span data-stu-id="6d863-276">toohave only hello root domain in hello issuer claim value, change hello claim rule toomatch hello following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="6d863-277">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d863-277">Next steps</span></span>
<span data-ttu-id="6d863-278">Dowiedz się więcej o [opcje logowania użytkowników](active-directory-aadconnect-user-signin.md).</span><span class="sxs-lookup"><span data-stu-id="6d863-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>
