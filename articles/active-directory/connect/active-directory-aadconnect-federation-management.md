---
title: "Dostosowywanie z programem Azure AD Connect i zarządzania w usłudze Active Directory Federation Services | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 14f03542a6553c5bb697192828368ffe6b96441c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="cbcee-104">Zarządzanie i dostosowania usług federacyjnych Active Directory przy użyciu usługi Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="cbcee-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="cbcee-105">W tym artykule opisano sposób zarządzania i dostosowywania Active Directory Federation Services (AD FS) przy użyciu połączenia usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cbcee-105">This article describes how to manage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="cbcee-106">Zawiera również innych typowych zadań usług AD FS, które może być konieczne przeprowadzenie pełnej konfiguracji farmy usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="cbcee-106">It also includes other common AD FS tasks that you might need to do for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="cbcee-107">Temat</span><span class="sxs-lookup"><span data-stu-id="cbcee-107">Topic</span></span> | <span data-ttu-id="cbcee-108">Co obejmuje</span><span class="sxs-lookup"><span data-stu-id="cbcee-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="cbcee-109">**Zarządzanie usługami AD FS**</span><span class="sxs-lookup"><span data-stu-id="cbcee-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="cbcee-110">Napraw zaufania</span><span class="sxs-lookup"><span data-stu-id="cbcee-110">Repair the trust</span></span>](#repairthetrust) |<span data-ttu-id="cbcee-111">Jak naprawić relacja zaufania federacji z usługą Office 365.</span><span class="sxs-lookup"><span data-stu-id="cbcee-111">How to repair the federation trust with Office 365.</span></span> |
| [<span data-ttu-id="cbcee-112">Utworzenie federacji z usługą Azure AD przy użyciu alternatywnego Identyfikatora logowania</span><span class="sxs-lookup"><span data-stu-id="cbcee-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="cbcee-113">Konfigurowanie Federacji przy użyciu alternatywnego Identyfikatora logowania</span><span class="sxs-lookup"><span data-stu-id="cbcee-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="cbcee-114">Dodawanie serwera usług AD FS</span><span class="sxs-lookup"><span data-stu-id="cbcee-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="cbcee-115">Jak rozszerzyć farmy usług AD FS jest dodatkowy serwer usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="cbcee-115">How to expand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="cbcee-116">Dodaj serwer Proxy aplikacji sieci Web usług AD FS</span><span class="sxs-lookup"><span data-stu-id="cbcee-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="cbcee-117">Jak rozszerzyć farmy usług AD FS jest dodatkowy serwer Proxy aplikacji sieci Web (WAP).</span><span class="sxs-lookup"><span data-stu-id="cbcee-117">How to expand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="cbcee-118">Dodawanie domeny federacyjnej</span><span class="sxs-lookup"><span data-stu-id="cbcee-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="cbcee-119">Jak dodać domeny federacyjnej.</span><span class="sxs-lookup"><span data-stu-id="cbcee-119">How to add a federated domain.</span></span> |
| [<span data-ttu-id="cbcee-120">Aktualizuj certyfikat protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="cbcee-120">Update the SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="cbcee-121">Jak zaktualizować certyfikat SSL do farmy usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="cbcee-121">How to update the SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="cbcee-122">**Dostosowywanie usług AD FS**</span><span class="sxs-lookup"><span data-stu-id="cbcee-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="cbcee-123">Dodać logo firmy lub ilustracji</span><span class="sxs-lookup"><span data-stu-id="cbcee-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="cbcee-124">Sposób dostosowania strony w logowania usług AD FS, z firmowego logo i ilustracja.</span><span class="sxs-lookup"><span data-stu-id="cbcee-124">How to customize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="cbcee-125">Dodaj opis logowania</span><span class="sxs-lookup"><span data-stu-id="cbcee-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="cbcee-126">Jak dodać opis do strony logowania.</span><span class="sxs-lookup"><span data-stu-id="cbcee-126">How to add a sign-in page description.</span></span> |
| [<span data-ttu-id="cbcee-127">Modyfikowanie reguł oświadczeń usług AD FS</span><span class="sxs-lookup"><span data-stu-id="cbcee-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="cbcee-128">Jak zmodyfikować oświadczenia usług AD FS dla różnych scenariuszach federacji.</span><span class="sxs-lookup"><span data-stu-id="cbcee-128">How to modify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="cbcee-129">Zarządzanie usługami AD FS</span><span class="sxs-lookup"><span data-stu-id="cbcee-129">Manage AD FS</span></span>
<span data-ttu-id="cbcee-130">Różne zadania związane z FS AD można wykonać w programie Azure AD Connect z użytkownika minimalnej interwencji przy użyciu Kreatora programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="cbcee-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using the Azure AD Connect wizard.</span></span> <span data-ttu-id="cbcee-131">Po zakończeniu instalowania Azure AD Connect za pomocą kreatora można uruchomić kreatora ponownie w celu wykonywania dodatkowych zadań.</span><span class="sxs-lookup"><span data-stu-id="cbcee-131">After you've finished installing Azure AD Connect by running the wizard, you can run the wizard again to perform additional tasks.</span></span>

## <span data-ttu-id="cbcee-132">Napraw zaufania<a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="cbcee-132">Repair the trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="cbcee-133">Azure AD Connect umożliwia Sprawdź bieżącą kondycję usług AD FS i usługi Azure AD ufa i podjąć odpowiednie działania naprawić relacji zaufania.</span><span class="sxs-lookup"><span data-stu-id="cbcee-133">You can use Azure AD Connect to check the current health of the AD FS and Azure AD trust and take appropriate actions to repair the trust.</span></span> <span data-ttu-id="cbcee-134">Wykonaj następujące kroki, aby naprawić usługi Azure AD i zaufania usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="cbcee-134">Follow these steps to repair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="cbcee-135">Wybierz **AAD naprawy i zaufania usług AD FS** z listy dodatkowe zadania.</span><span class="sxs-lookup"><span data-stu-id="cbcee-135">Select **Repair AAD and ADFS Trust** from the list of additional tasks.</span></span>
   <span data-ttu-id="cbcee-136">![Napraw AAD i usług AD FS zaufania](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="cbcee-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="cbcee-137">Na **nawiązywanie połączenia z usługą Azure AD** , podaj poświadczenia administratora globalnego dla usługi Azure AD i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cbcee-137">On the **Connect to Azure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="cbcee-138">![Łączenie z usługą Azure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="cbcee-138">![Connect to Azure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="cbcee-139">Na **poświadczeń dostępu zdalnego** strony, wprowadź poświadczenia administratora domeny.</span><span class="sxs-lookup"><span data-stu-id="cbcee-139">On the **Remote access credentials** page, enter the credentials for the domain administrator.</span></span>

   ![Poświadczenia dostępu zdalnego](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="cbcee-141">Po kliknięciu **dalej**, Azure AD Connect sprawdza, czy certyfikat kondycji i zawiera wszystkie problemy.</span><span class="sxs-lookup"><span data-stu-id="cbcee-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![Stan certyfikatów](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="cbcee-143">**Wszystko gotowe do skonfigurowania** znajduje się lista akcji, które zostanie wykonane do naprawy relacji zaufania.</span><span class="sxs-lookup"><span data-stu-id="cbcee-143">The **Ready to configure** page shows the list of actions that will be performed to repair the trust.</span></span>

    ![Wszystko gotowe do skonfigurowania](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="cbcee-145">Kliknij przycisk **zainstalować** naprawić relacji zaufania.</span><span class="sxs-lookup"><span data-stu-id="cbcee-145">Click **Install** to repair the trust.</span></span>

> [!NOTE]
> <span data-ttu-id="cbcee-146">Azure AD Connect może tylko naprawy lub ustawy o certyfikaty z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="cbcee-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="cbcee-147">Azure AD Connect nie może naprawić certyfikatów innych firm.</span><span class="sxs-lookup"><span data-stu-id="cbcee-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="cbcee-148">Utworzenie federacji z usługą Azure AD przy użyciu AlternateID<a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="cbcee-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="cbcee-149">Zaleca się, że Name(UPN) podmiot zabezpieczeń użytkownika lokalnie i w chmurze główna nazwa użytkownika pozostają na takie same.</span><span class="sxs-lookup"><span data-stu-id="cbcee-149">It is recommended that the on-premises User Principal Name(UPN) and the cloud User Principal Name are kept the same.</span></span> <span data-ttu-id="cbcee-150">Jeśli korzysta z lokalną nazwą UPN domeny bez obsługi routingu (np.</span><span class="sxs-lookup"><span data-stu-id="cbcee-150">If the on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="cbcee-151">Contoso.local) lub nie można zmienić z powodu zależności aplikacji lokalnych, zaleca się konfigurowanie alternatywnego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="cbcee-151">Contoso.local) or cannot be changed due to local application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="cbcee-152">Alternatywnego Identyfikatora logowania umożliwia skonfigurowanie środowiska logowania z której użytkownicy mogą logować się przy użyciu atrybutu innego niż ich nazwy UPN, taki jak adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="cbcee-152">Alternate login ID allows you to configure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="cbcee-153">Wybór dla główna nazwa użytkownika usługi Azure AD Connect Domyślnie atrybut userPrincipalName w usłudze Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cbcee-153">The choice for User Principal Name in Azure AD Connect defaults to the userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="cbcee-154">Jeśli możesz wybrać inny atrybut główna nazwa użytkownika i Federacji przy użyciu usług AD FS, następnie Azure AD Connect konfiguracji usług AD FS dla alternatywny identyfikator.</span><span class="sxs-lookup"><span data-stu-id="cbcee-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="cbcee-155">Poniżej przedstawiono przykład wybranie innego atrybutu główna nazwa użytkownika:</span><span class="sxs-lookup"><span data-stu-id="cbcee-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![Alternatywny identyfikator atrybutu zaznaczenia](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="cbcee-157">Konfigurowanie alternatywnego Identyfikatora logowania dla usług AD FS składa się z dwóch głównych czynności:</span><span class="sxs-lookup"><span data-stu-id="cbcee-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="cbcee-158">**Konfigurowanie odpowiedniego zestawu wystawiania oświadczeń**: reguły wystawiania oświadczeń w usłudze Azure AD uzależnionej zaufania są modyfikacji w celu użycia wybranego atrybutu UserPrincipalName jako alternatywnego Identyfikatora użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cbcee-158">**Configure the right set of issuance claims**: The issuance claim rules in the Azure AD relying party trust are modified to use the selected UserPrincipalName attribute as the alternate ID of the user.</span></span>
2. <span data-ttu-id="cbcee-159">**Włącz alternatywnego Identyfikatora logowania w konfiguracji usług AD FS**: Zaktualizowano konfigurację usług AD FS, aby usługi AD FS można wyszukiwać użytkowników w lasach odpowiednie przy użyciu alternatywnego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="cbcee-159">**Enable alternate login ID in the AD FS configuration**: The AD FS configuration is updated so that AD FS can look up users in the appropriate forests using the alternate ID.</span></span> <span data-ttu-id="cbcee-160">Ta konfiguracja jest obsługiwana dla usług AD FS w systemie Windows Server 2012 R2 (z KB2919355) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="cbcee-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="cbcee-161">Jeśli serwery usług AD FS 2012 R2, Azure AD Connect sprawdza obecność wymagane KB.</span><span class="sxs-lookup"><span data-stu-id="cbcee-161">If the AD FS servers are 2012 R2, Azure AD Connect checks for the presence of the required KB.</span></span> <span data-ttu-id="cbcee-162">Jeśli nie wykryto KB, będzie wyświetlane ostrzeżenie po zakończeniu konfiguracji, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="cbcee-162">If the KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![Ostrzeżenie dotyczące Brak KB na 2012 R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="cbcee-164">Aby rozwiązać konfiguracji w przypadku brakujących KB, należy zainstalować wymagane [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) , a następnie napraw za pomocą zaufania [napraw AAD i AD FS zaufania](#repairthetrust).</span><span class="sxs-lookup"><span data-stu-id="cbcee-164">To rectify the configuration in case of missing KB, install the required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair the trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="cbcee-165">Aby uzyskać więcej informacji na alternateID i kroki, aby ręcznie skonfigurować odczytu [Konfigurowanie alternatywnego Identyfikatora logowania](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span><span class="sxs-lookup"><span data-stu-id="cbcee-165">For more information on alternateID and steps to manually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="cbcee-166">Dodawanie serwera usług AD FS<a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="cbcee-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="cbcee-167">Aby dodać serwer usług AD FS, Azure AD Connect wymaga certyfikatu PFX.</span><span class="sxs-lookup"><span data-stu-id="cbcee-167">To add an AD FS server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="cbcee-168">W związku z tym tę operację mogą wykonać tylko w przypadku skonfigurowania farmy usług AD FS przy użyciu usługi Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="cbcee-168">Therefore, you can perform this operation only if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="cbcee-169">Wybierz **wdrażanie dodatkowego serwera federacyjnego**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cbcee-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![Serwer federacyjny dodatkowe](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="cbcee-171">Na **nawiązywanie połączenia z usługą Azure AD** strony, wprowadź swoje poświadczenia administratora globalnego dla usługi Azure AD, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cbcee-171">On the **Connect to Azure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![Łączenie z usługą Azure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="cbcee-173">Podaj poświadczenia administratora domeny.</span><span class="sxs-lookup"><span data-stu-id="cbcee-173">Provide the domain administrator credentials.</span></span>

   ![Podane poświadczenia administratora domeny](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="cbcee-175">Azure AD Connect pytanie o hasło pliku PFX podany podczas konfigurowania nowej farmie serwerów usług AD FS z programem Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="cbcee-175">Azure AD Connect asks for the password of the PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="cbcee-176">Kliknij przycisk **wprowadź hasło** o podanie hasła dla pliku PFX.</span><span class="sxs-lookup"><span data-stu-id="cbcee-176">Click **Enter Password** to provide the password for the PFX file.</span></span>

   ![Hasło certyfikatu](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Określ certyfikat SSL](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="cbcee-179">Na **serwery usług AD FS** strony, wprowadź nazwę serwera lub adres IP ma zostać dodany do farmy usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="cbcee-179">On the **AD FS Servers** page, enter the server name or IP address to be added to the AD FS farm.</span></span>

   ![Serwery usług AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="cbcee-181">Kliknij przycisk **dalej**i przejść ostatecznych **Konfiguruj** strony.</span><span class="sxs-lookup"><span data-stu-id="cbcee-181">Click **Next**, and go through the final **Configure** page.</span></span> <span data-ttu-id="cbcee-182">Po zakończeniu Azure AD Connect Dodawanie serwerów do farmy usług AD FS, użytkownik otrzyma opcję, aby sprawdzić łączność.</span><span class="sxs-lookup"><span data-stu-id="cbcee-182">After Azure AD Connect has finished adding the servers to the AD FS farm, you will be given the option to verify the connectivity.</span></span>

   ![Wszystko gotowe do skonfigurowania](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Zakończenie instalacji](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="cbcee-185">Dodaj serwer AD FS WAP<a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="cbcee-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="cbcee-186">Aby dodać serwer proxy, Azure AD Connect wymaga certyfikatu PFX.</span><span class="sxs-lookup"><span data-stu-id="cbcee-186">To add a WAP server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="cbcee-187">W związku z tym można wykonać tylko tej operacji po skonfigurowaniu farmy usług AD FS przy użyciu usługi Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="cbcee-187">Therefore, you can only perform this operation if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="cbcee-188">Wybierz **wdrażanie Proxy aplikacji sieci Web** z listy dostępnych zadań.</span><span class="sxs-lookup"><span data-stu-id="cbcee-188">Select **Deploy Web Application Proxy** from the list of available tasks.</span></span>

   ![Wdrożenie serwera Proxy aplikacji sieci Web](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="cbcee-190">Podaj poświadczenia administratora globalnego usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="cbcee-190">Provide the Azure global administrator credentials.</span></span>

   ![Łączenie z usługą Azure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="cbcee-192">Na **certyfikat SSL określ** Podaj hasło dla pliku PFX podany podczas konfigurowania farmy usług AD FS z programem Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="cbcee-192">On the **Specify SSL certificate** page, provide the password for the PFX file that you provided when you configured the AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="cbcee-193">![Hasło certyfikatu](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="cbcee-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![Określ certyfikat SSL](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="cbcee-195">Dodaj serwer, który ma zostać dodany jako serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="cbcee-195">Add the server to be added as a WAP server.</span></span> <span data-ttu-id="cbcee-196">Ponieważ serwerowi proxy aplikacji nie może być przyłączony do domeny, Kreator zapyta o podanie poświadczeń administracyjnych dodawany serwer.</span><span class="sxs-lookup"><span data-stu-id="cbcee-196">Because the WAP server might not be joined to the domain, the wizard asks for administrative credentials to the server being added.</span></span>

   ![Poświadczenia administracyjne serwera](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="cbcee-198">Na **poświadczeń zaufania serwera Proxy** Podaj poświadczenia administracyjne, aby skonfigurować serwer proxy zaufania i uzyskać dostęp serwer główny w farmie usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="cbcee-198">On the **Proxy trust credentials** page, provide administrative credentials to configure the proxy trust and access the primary server in the AD FS farm.</span></span>

   ![Poświadczenia zaufania serwera proxy](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="cbcee-200">Na **wszystko gotowe do skonfigurowania** strony, Kreator z listą akcje, które będą wykonywane.</span><span class="sxs-lookup"><span data-stu-id="cbcee-200">On the **Ready to configure** page, the wizard shows the list of actions that will be performed.</span></span>

   ![Wszystko gotowe do skonfigurowania](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="cbcee-202">Kliknij przycisk **zainstalować** aby zakończyć konfigurację.</span><span class="sxs-lookup"><span data-stu-id="cbcee-202">Click **Install** to finish the configuration.</span></span> <span data-ttu-id="cbcee-203">Po zakończeniu konfiguracji kreatora udostępnia opcję, aby sprawdzić łączność z serwerami.</span><span class="sxs-lookup"><span data-stu-id="cbcee-203">After the configuration is complete, the wizard gives you the option to verify the connectivity to the servers.</span></span> <span data-ttu-id="cbcee-204">Kliknij przycisk **Sprawdź** Aby sprawdzić łączność.</span><span class="sxs-lookup"><span data-stu-id="cbcee-204">Click **Verify** to check connectivity.</span></span>

   ![Zakończenie instalacji](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="cbcee-206">Dodawanie domeny federacyjnej<a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="cbcee-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="cbcee-207">To proste dodać domenę federacyjną z usługą Azure AD za pomocą usługi Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="cbcee-207">It's easy to add a domain to be federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="cbcee-208">Azure AD Connect dodaje domeny na potrzeby federowania i modyfikuje reguł oświadczeń w celu odzwierciedlenia wystawca poprawnie, jeśli masz wiele domen federacyjnych z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cbcee-208">Azure AD Connect adds the domain for federation and modifies the claim rules to correctly reflect the issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="cbcee-209">Aby dodać domenę federacyjną, wybierz zadanie **Dodawanie kolejnej domeny usługi Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="cbcee-209">To add a federated domain, select the task **Add an additional Azure AD domain**.</span></span>

   ![Dodatkowe domeny usługi Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="cbcee-211">Na następnej stronie kreatora należy podać poświadczenia administratora globalnego dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cbcee-211">On the next page of the wizard, provide the global administrator credentials for Azure AD.</span></span>

   ![Łączenie z usługą Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="cbcee-213">Na **poświadczeń dostępu zdalnego** Podaj poświadczenia administratora domeny.</span><span class="sxs-lookup"><span data-stu-id="cbcee-213">On the **Remote access credentials** page, provide the domain administrator credentials.</span></span>

   ![Poświadczenia dostępu zdalnego](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="cbcee-215">Na następnej stronie kreatora zawiera listę domen usługi Azure AD, które można było wykonać Federację z katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="cbcee-215">On the next page, the wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="cbcee-216">Wybierz domenę z listy.</span><span class="sxs-lookup"><span data-stu-id="cbcee-216">Choose the domain from the list.</span></span>

   ![Domenowych Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="cbcee-218">Po wybraniu domeny Kreator udostępnia odpowiednie informacje o dalsze akcje, które podejmie kreatora i ich wpływ na konfigurację.</span><span class="sxs-lookup"><span data-stu-id="cbcee-218">After you choose the domain, the wizard provides you with appropriate information about further actions that the wizard will take and the impact of the configuration.</span></span> <span data-ttu-id="cbcee-219">W niektórych przypadkach w przypadku wybrania domeny, która nie jest jeszcze zweryfikowana w usłudze Azure AD, Kreator dostarcza informacje ułatwiające zweryfikować domenę.</span><span class="sxs-lookup"><span data-stu-id="cbcee-219">In some cases, if you select a domain that isn't yet verified in Azure AD, the wizard provides you with information to help you verify the domain.</span></span> <span data-ttu-id="cbcee-220">Zobacz [Dodawanie niestandardowej nazwy domeny do usługi Azure Active Directory](../active-directory-add-domain.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="cbcee-220">See [Add your custom domain name to Azure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="cbcee-221">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="cbcee-221">Click **Next**.</span></span> <span data-ttu-id="cbcee-222">**Wszystko gotowe do skonfigurowania** strona zawiera listę działań, które wykona Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="cbcee-222">The **Ready to configure** page shows the list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="cbcee-223">Kliknij przycisk **zainstalować** aby zakończyć konfigurację.</span><span class="sxs-lookup"><span data-stu-id="cbcee-223">Click **Install** to finish the configuration.</span></span>

   ![Wszystko gotowe do skonfigurowania](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="cbcee-225">Musi być synchronizowany użytkowników dodanych domeny federacyjnej, zanim będą mogli logować się do usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cbcee-225">Users from the added federated domain must be synchronized before they will be able to login to Azure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="cbcee-226">Dostosowania usług AD FS</span><span class="sxs-lookup"><span data-stu-id="cbcee-226">AD FS customization</span></span>
<span data-ttu-id="cbcee-227">Poniższe sekcje zawierają szczegółowe informacje o niektórych typowych zadań, które należy wykonać podczas dostosowywania strony logowania usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="cbcee-227">The following sections provide details about some of the common tasks that you might have to perform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="cbcee-228">Dodać logo firmy lub ilustracji<a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="cbcee-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="cbcee-229">Aby zmienić logo firmy, który jest wyświetlany na **logowania** strony, należy użyć następującego polecenia cmdlet programu Windows PowerShell i składni.</span><span class="sxs-lookup"><span data-stu-id="cbcee-229">To change the logo of the company that's displayed on the **Sign-in** page, use the following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="cbcee-230">Zalecane wymiary logo to 260 x 35 przy rozdzielczości 96 dpi w pliku o rozmiarze nie większym niż 10 KB.</span><span class="sxs-lookup"><span data-stu-id="cbcee-230">The recommended dimensions for the logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="cbcee-231">*TargetName* parametr jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="cbcee-231">The *TargetName* parameter is required.</span></span> <span data-ttu-id="cbcee-232">Motyw domyślny publikowany z usługami AD FS nosi nazwę domyślny.</span><span class="sxs-lookup"><span data-stu-id="cbcee-232">The default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="cbcee-233">Dodaj opis logowania<a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="cbcee-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="cbcee-234">Aby dodać opis do strony logowania **strony logowania**, użyj następującego polecenia cmdlet programu Windows PowerShell i składni.</span><span class="sxs-lookup"><span data-stu-id="cbcee-234">To add a sign-in page description to the **Sign-in page**, use the following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="cbcee-235">Modyfikowanie reguł oświadczeń usług AD FS<a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="cbcee-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="cbcee-236">Usługi AD FS obsługuje język sformatowanego oświadczenia, którego można używać do tworzenia niestandardowych reguł oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="cbcee-236">AD FS supports a rich claim language that you can use to create custom claim rules.</span></span> <span data-ttu-id="cbcee-237">Aby uzyskać więcej informacji, zobacz [rola języka reguł oświadczeń](https://technet.microsoft.com/library/dd807118.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbcee-237">For more information, see [The Role of the Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="cbcee-238">W poniższych sekcjach opisano, jak można zapisać reguły niestandardowe dla niektórych scenariuszy, które odnoszą się do usługi Azure AD i federacji usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="cbcee-238">The following sections describe how you can write custom rules for some scenarios that relate to Azure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-the-attribute"></a><span data-ttu-id="cbcee-239">Warunkowe na wartość jest obecny w atrybucie niezmienialnego Identyfikatora</span><span class="sxs-lookup"><span data-stu-id="cbcee-239">Immutable ID conditional on a value being present in the attribute</span></span>
<span data-ttu-id="cbcee-240">Azure AD Connect umożliwia określenie atrybutu ma być używany jako zakotwiczenie źródła, gdy obiekty są synchronizowane z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cbcee-240">Azure AD Connect lets you specify an attribute to be used as a source anchor when objects are synced to Azure AD.</span></span> <span data-ttu-id="cbcee-241">Jeśli wartość atrybutu niestandardowego nie jest pusta, można wystawić oświadczenie niezmienne identyfikator.</span><span class="sxs-lookup"><span data-stu-id="cbcee-241">If the value in the custom attribute is not empty, you might want to issue an immutable ID claim.</span></span>

<span data-ttu-id="cbcee-242">Na przykład możesz wybrać pozycję **ms-ds-consistencyguid** jako atrybut zakotwiczenia źródła i problem **nazwę ImmutableID** jako **consistencyguid-ms-ds** w przypadku, gdy atrybut ma wartość na nim.</span><span class="sxs-lookup"><span data-stu-id="cbcee-242">For example, you might select **ms-ds-consistencyguid** as the attribute for the source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case the attribute has a value against it.</span></span> <span data-ttu-id="cbcee-243">Jeśli nie ma żadnej wartości tego atrybutu, **objectGuid** jako niezmienialny identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="cbcee-243">If there's no value against the attribute, issue **objectGuid** as the immutable ID.</span></span> <span data-ttu-id="cbcee-244">Można utworzyć zestaw reguł oświadczeń, zgodnie z opisem w poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="cbcee-244">You can construct the set of custom claim rules as described in the following section.</span></span>

<span data-ttu-id="cbcee-245">**Reguła 1: Atrybuty zapytania**</span><span class="sxs-lookup"><span data-stu-id="cbcee-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="cbcee-246">W tej regule, w przypadku badania wartości **ms-ds-consistencyguid** i **objectGuid** dla użytkownika z usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cbcee-246">In this rule, you're querying the values of **ms-ds-consistencyguid** and **objectGuid** for the user from Active Directory.</span></span> <span data-ttu-id="cbcee-247">Zmień nazwę magazynu do magazynu odpowiednie nazwy we wdrożeniu usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="cbcee-247">Change the store name to an appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="cbcee-248">Zmień typ oświadczenia do odpowiedniego oświadczeń również typ federacyjnym, zgodnie z definicją **objectGuid** i **consistencyguid-ms-ds**.</span><span class="sxs-lookup"><span data-stu-id="cbcee-248">Also change the claims type to a proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="cbcee-249">Ponadto za pomocą **dodać** i nie **problem**, unikać dodawania problemu wychodzących dla obiektu, a można użyć wartości jako wartości pośrednich.</span><span class="sxs-lookup"><span data-stu-id="cbcee-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for the entity, and can use the values as intermediate values.</span></span> <span data-ttu-id="cbcee-250">Po ustaleniu wartość, która ma być używana jako niezmienialny identyfikatora wystawia oświadczenia w regule nowsze</span><span class="sxs-lookup"><span data-stu-id="cbcee-250">You will issue the claim in a later rule after you establish which value to use as the immutable ID.</span></span>

<span data-ttu-id="cbcee-251">**Reguła 2: Sprawdź, czy consistencyguid-ms-ds istnieje dla użytkownika**</span><span class="sxs-lookup"><span data-stu-id="cbcee-251">**Rule 2: Check if ms-ds-consistencyguid exists for the user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="cbcee-252">Ta zasada definiuje tymczasowe flagę o nazwie **idflag** który ustawiono **useguid** w przypadku nie **consistencyguid-ms-ds** wypełnione dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cbcee-252">This rule defines a temporary flag called **idflag** that is set to **useguid** if there's no **ms-ds-consistencyguid** populated for the user.</span></span> <span data-ttu-id="cbcee-253">Logiki tego jest fakt, że usługi AD FS nie zezwala na puste oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="cbcee-253">The logic behind this is the fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="cbcee-254">Dlatego po dodaniu http://contoso.com/ws/2016/02/identity/claims/objectguid oświadczeń i http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid w reguła 1 na końcu **msdsconsistencyguid** oświadczeń tylko, jeśli wartość jest wypełniana dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cbcee-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if the value is populated for the user.</span></span> <span data-ttu-id="cbcee-255">Jeśli go nie jest wypełnione, będzie mieć wartość pustą i odrzuca pochodzące od razu będzie widział usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="cbcee-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="cbcee-256">Wszystkie obiekty będą mieć **objectGuid**, więc roszczenie zawsze będą dostępne po wykonaniu reguła 1.</span><span class="sxs-lookup"><span data-stu-id="cbcee-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="cbcee-257">**Reguła 3: Wystawiać ms-ds-consistencyguid jako niezmienialnego Identyfikatora, jeśli jest obecny**</span><span class="sxs-lookup"><span data-stu-id="cbcee-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="cbcee-258">To jest niejawnie **Exist** Sprawdź.</span><span class="sxs-lookup"><span data-stu-id="cbcee-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="cbcee-259">Jeśli istnieje wartość oświadczenia, następnie wystawia, które jako niezmienialny identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="cbcee-259">If the value for the claim exists, then issue that as the immutable ID.</span></span> <span data-ttu-id="cbcee-260">W poprzednim przykładzie użyto **nameidentifier** oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="cbcee-260">The previous example uses the **nameidentifier** claim.</span></span> <span data-ttu-id="cbcee-261">Należy zmienić to typ oświadczenia właściwe dla niezmienialnego Identyfikatora w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="cbcee-261">You'll have to change this to the appropriate claim type for the immutable ID in your environment.</span></span>

<span data-ttu-id="cbcee-262">**Reguła 4: Jeśli consistencyGuid-ms-ds nie jest obecny Wystaw objectGuid jako niezmienialnego Identyfikatora**</span><span class="sxs-lookup"><span data-stu-id="cbcee-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="cbcee-263">W tej regule, sprawdzamy po prostu flagę tymczasowego **idflag**.</span><span class="sxs-lookup"><span data-stu-id="cbcee-263">In this rule, you're simply checking the temporary flag **idflag**.</span></span> <span data-ttu-id="cbcee-264">Określenie, czy wystawiać oświadczenia na podstawie jego wartości.</span><span class="sxs-lookup"><span data-stu-id="cbcee-264">You decide whether to issue the claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="cbcee-265">Ważne jest sekwencji tych zasad.</span><span class="sxs-lookup"><span data-stu-id="cbcee-265">The sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="cbcee-266">Usługa rejestracji Jednokrotnej z poddomeny nazwy UPN</span><span class="sxs-lookup"><span data-stu-id="cbcee-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="cbcee-267">Można dodać więcej niż jedną domenę federacyjną za pomocą usługi Azure AD Connect, zgodnie z opisem w [Dodaj nową domenę federacyjną](active-directory-aadconnect-federation-management.md#addfeddomain).</span><span class="sxs-lookup"><span data-stu-id="cbcee-267">You can add more than one domain to be federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="cbcee-268">Należy zmodyfikować oświadczenia użytkownika (UPN) Nazwa główna tak, aby identyfikator wystawcy odnosi się do domeny głównej, a nie domeny podrzędnej, ponieważ domeny głównej federacyjnych obejmuje również podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="cbcee-268">You must modify the user principal name (UPN) claim so that the issuer ID corresponds to the root domain and not the subdomain, because the federated root domain also covers the child.</span></span>

<span data-ttu-id="cbcee-269">Domyślnie reguły oświadczenia dla Identyfikatora wystawcy jest ustawiony jako:</span><span class="sxs-lookup"><span data-stu-id="cbcee-269">By default, the claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Oświadczenie Identyfikatora wystawcy domyślne](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="cbcee-271">Domyślna reguła po prostu przyjmuje sufiks głównej nazwy użytkownika i używa go w oświadczenie Identyfikatora wystawcy.</span><span class="sxs-lookup"><span data-stu-id="cbcee-271">The default rule simply takes the UPN suffix and uses it in the issuer ID claim.</span></span> <span data-ttu-id="cbcee-272">Na przykład Jan jest użytkownikiem w sub.contoso.com i contoso.com jest Sfederowane przy użyciu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cbcee-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="cbcee-273">Jan wprowadza john@sub.contoso.com jako nazwy użytkownika podczas logowania do usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cbcee-273">John enters john@sub.contoso.com as the username while signing in to Azure AD.</span></span> <span data-ttu-id="cbcee-274">Domyślna reguła oświadczeń identyfikator wystawcy w usługach AD FS obsługuje go w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="cbcee-274">The default issuer ID claim rule in AD FS handles it in the following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="cbcee-275">**Wartość oświadczenia:** http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="cbcee-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="cbcee-276">Aby w wartości oświadczenia wystawcy tylko domeny głównej, zmień reguły oświadczenia zgodne z następującymi:</span><span class="sxs-lookup"><span data-stu-id="cbcee-276">To have only the root domain in the issuer claim value, change the claim rule to match the following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="cbcee-277">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cbcee-277">Next steps</span></span>
<span data-ttu-id="cbcee-278">Dowiedz się więcej o [opcje logowania użytkowników](active-directory-aadconnect-user-signin.md).</span><span class="sxs-lookup"><span data-stu-id="cbcee-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>
