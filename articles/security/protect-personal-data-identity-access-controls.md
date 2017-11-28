---
title: "dane osobowe aaaProtect z Azure formanty tożsamościami i dostępem | Dokumentacja firmy Microsoft"
description: "Przy użyciu Azure toohelp formanty tożsamościami i dostępem chronić dane osobowe użytkownika"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a><span data-ttu-id="371de-103">Azure Active Directory i uwierzytelniania wieloskładnikowego: ochrony danych osobowych z formantami tożsamościami i dostępem</span><span class="sxs-lookup"><span data-stu-id="371de-103">Azure Active Directory and Multi-Factor Authentication: Protect personal data with identity and access controls</span></span>

<span data-ttu-id="371de-104">Ten artykuł zawiera informacje i procedury, można użyć danych osobowych tooprotect przy użyciu usługi i funkcje zabezpieczeń uwierzytelniania usługi Azure Active Directory i usługi Multi-Factor.</span><span class="sxs-lookup"><span data-stu-id="371de-104">This article provides information and procedures you can use tooprotect personal data using Azure Active Directory and Multi-factor authentication security features and services.</span></span>

## <a name="scenario"></a><span data-ttu-id="371de-105">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="371de-105">Scenario</span></span>

<span data-ttu-id="371de-106">Firma rejs dużych, siedzibą w Stanach Zjednoczonych hello, rozwija trasy toooffer jego operacji w Śródziemnego hello, Adriatyku i Bałtyckiego mórz, jak również hello brytyjskich.</span><span class="sxs-lookup"><span data-stu-id="371de-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="371de-107">toosupport tych działań uzyskała mniejszych rejs wiersze na podstawie we Włoszech Niemczech, Dania i hello Zjednoczone Królestwo</span><span class="sxs-lookup"><span data-stu-id="371de-107">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="371de-108">Witaj firma korzysta z danych firmowych toostore Microsoft Azure w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="371de-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="371de-109">Dotyczy to również dane osobowe, takich jak nazwy, adresy, numery telefonów i informacje o karcie kredytowej z jej klientów globalnych.</span><span class="sxs-lookup"><span data-stu-id="371de-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="371de-110">Zawiera także tradycyjnych informacje kadr, takie jak adresy, numery telefonów, numery identyfikacyjne podatku i medyczne informacje dotyczące pracowników firmy we wszystkich lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="371de-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="371de-111">wiersz rejs Hello zachowuje również dużej bazy danych elementów członkowskich programu osób trzecich i lojalność zawierający dane osobowe tootrack relacje z bieżących i starszych klientów.</span><span class="sxs-lookup"><span data-stu-id="371de-111">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="371de-112">Pracownikom firmy dostępu hello sieci z biurach zdalnych i agentów podróży hello firmy znajdujących się wokół Witaj świecie mają dostęp do zasobów firmowych toosome.</span><span class="sxs-lookup"><span data-stu-id="371de-112">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="371de-113">Opis problemu</span><span class="sxs-lookup"><span data-stu-id="371de-113">Problem statement</span></span>

<span data-ttu-id="371de-114">Hello firmy muszą chronić prywatność hello danych osobowych pracowników i klientów przed atakami znalezienia dostępu toogain tożsamości toouse naruszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="371de-114">hello company must protect hello privacy of customers’ and employees’ personal data from attackers seeking toouse compromised identities toogain access.</span></span> <span data-ttu-id="371de-115">One także sprawdzić toopersonal tego dostępu, które dane przez autoryzowanych użytkowników jest ograniczony tylko do tych wymagających toodo swoich zadań.</span><span class="sxs-lookup"><span data-stu-id="371de-115">They also must ensure that access toopersonal data by legitimate users is restricted to only those who need it toodo their jobs.</span></span>

## <a name="company-goal"></a><span data-ttu-id="371de-116">Celem firmy</span><span class="sxs-lookup"><span data-stu-id="371de-116">Company goal</span></span>

<span data-ttu-id="371de-117">Celem firmy Hello jest tooensure, że dostęp do danych toopersonal ścisłą kontrolę.</span><span class="sxs-lookup"><span data-stu-id="371de-117">hello company’s goal is tooensure that access toopersonal data is strictly controlled.</span></span> <span data-ttu-id="371de-118">Istotne jest, że tożsamości użytkowników mających dostęp do danych toopersonal być chronione przez silnego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="371de-118">It is essential that identities of users with access toopersonal data be protected by strong authentication.</span></span> <span data-ttu-id="371de-119">Zasady [najniższych uprawnień] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) musi odbywać się tak, że istnieje tylko poziom hello potrzebują dostępu i nie więcej.</span><span class="sxs-lookup"><span data-stu-id="371de-119">A policy of [least privilege] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) must be enforced so that legitimate users have only hello level of  access they need, and no more.</span></span>

## <a name="solutions"></a><span data-ttu-id="371de-120">Rozwiązania</span><span class="sxs-lookup"><span data-stu-id="371de-120">Solutions</span></span>

<span data-ttu-id="371de-121">Microsoft Azure udostępnia narzędzia do zarządzania tożsamościami i dostępem toohelp firm kontrolować, kto może tooresources dostępu, które zawierają dane osobowe.</span><span class="sxs-lookup"><span data-stu-id="371de-121">Microsoft Azure provides identity and access management tools toohelp companies control who has access tooresources that contain personal data.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="371de-122">Usługa Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="371de-122">Azure Active Directory</span></span>

<span data-ttu-id="371de-123">[Usługa Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) zarządza tożsamości i kontroluje dostęp tooAzure, jak również innych lokalnych i innych zasobów w chmurze, danych i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="371de-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) manages identities and controls access tooAzure as well as other on-premises and other cloud resources, data, and applications.</span></span> <span data-ttu-id="371de-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) pomaga Azure Administratorzy toominimize hello liczbę użytkowników, którzy mają dostęp toocertain informacje, takie jak dane osobowe.</span><span class="sxs-lookup"><span data-stu-id="371de-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helps Azure administrators toominimize hello number of people who have access toocertain information such as personal data.</span></span> <span data-ttu-id="371de-125">Pozwala toodiscover, ograniczenia i monitorowanie tożsamości uprzywilejowanych i ich tooresources i tooassign tymczasowe, just in Time (JIT) prawa administracyjne tooeligible użytkowników dostępu.</span><span class="sxs-lookup"><span data-stu-id="371de-125">It enables them toodiscover, restrict, and monitor privileged identities and their access tooresources, and tooassign temporary, Just-In-Time (JIT) administrative rights tooeligible users.</span></span> <span data-ttu-id="371de-126">Zapewnia wgląd w tych, którzy mają uprawnienia administracyjne w usłudze AAD.</span><span class="sxs-lookup"><span data-stu-id="371de-126">It also provides insight into those who have AAD administrative privileges.</span></span>

<span data-ttu-id="371de-127">Witaj działania związane ze stosowaniem AAD PIM obejmują:</span><span class="sxs-lookup"><span data-stu-id="371de-127">hello activities involved in using AAD PIM include:</span></span>

- <span data-ttu-id="371de-128">Włączanie katalogu Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="371de-128">Enabling Privileged Identity Management for your directory</span></span>

- <span data-ttu-id="371de-129">Przy użyciu Privileged Identity Management admin pulpit nawigacyjny toosee ważne informacje w skrócie</span><span class="sxs-lookup"><span data-stu-id="371de-129">Using Privileged Identity Management admin dashboard toosee important information at a glance</span></span>

- <span data-ttu-id="371de-130">Zarządzanie tożsamościami hello uprzywilejowany (Administratorzy) przez dodanie lub usunięcie roli tooeach stałych lub kwalifikujących się Administratorzy</span><span class="sxs-lookup"><span data-stu-id="371de-130">Managing hello privileged identities (administrators) by adding or removing permanent or eligible administrators tooeach role</span></span>

- <span data-ttu-id="371de-131">Konfigurowanie ustawień aktywacji roli hello</span><span class="sxs-lookup"><span data-stu-id="371de-131">Configuring hello role activation settings</span></span>

- <span data-ttu-id="371de-132">Aktywacja ról</span><span class="sxs-lookup"><span data-stu-id="371de-132">Activating roles</span></span>

- <span data-ttu-id="371de-133">Przeglądanie roli działania</span><span class="sxs-lookup"><span data-stu-id="371de-133">Reviewing role activity</span></span>

#### <a name="how-do-i-enable-aad-pim"></a><span data-ttu-id="371de-134">Jak włączyć AAD PIM?</span><span class="sxs-lookup"><span data-stu-id="371de-134">How do I enable AAD PIM?</span></span>

<span data-ttu-id="371de-135">przy użyciu usługi PIM dla katalogu, toostart hello następujące:</span><span class="sxs-lookup"><span data-stu-id="371de-135">toostart using PIM for your directory, do hello following:</span></span>

1. <span data-ttu-id="371de-136">Zaloguj się toohello portalu Azure jako administrator globalny katalogu.</span><span class="sxs-lookup"><span data-stu-id="371de-136">Sign in toohello Azure portal as a global administrator of your directory.</span></span>

2. <span data-ttu-id="371de-137">Jeśli Twoja organizacja ma więcej niż jeden katalog, w hello prawym górnym rogu hello portalu Azure wybierz nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="371de-137">If your organization has more than one directory, select your username in hello upper right-hand corner of hello Azure portal.</span></span> <span data-ttu-id="371de-138">Wybierz katalog hello, w którym będziesz używać usługi Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="371de-138">Select hello directory where you will use Azure AD Privileged Identity Management.</span></span>

3. <span data-ttu-id="371de-139">Wybierz **więcej usług** i użyj hello **filtru** toosearch pole tekstowe dla usługi Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="371de-139">Select **More services** and use hello **Filter** textbox toosearch for Azure AD Privileged Identity Management.</span></span>

4. <span data-ttu-id="371de-140">Sprawdź **toodashboard numeru Pin** , a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="371de-140">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="371de-141">Otwiera Hello aplikacji Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="371de-141">hello Privileged Identity Management application opens.</span></span>

<span data-ttu-id="371de-142">Po skonfigurowaniu usługi Azure AD Privileged Identity Management, zobacz blok nawigacji hello przy każdym otwarciu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="371de-142">Once Azure AD Privileged Identity Management is set up, you see hello navigation blade whenever you open hello application.</span></span>

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

<span data-ttu-id="371de-143">Aby uzyskać więcej informacji oraz instrukcje dotyczące wprowadzenie do korzystania z usługi PIM w usłudze AAD, zobacz [uruchomić przy użyciu usługi Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span><span class="sxs-lookup"><span data-stu-id="371de-143">For more information and instructions on getting started with AAD PIM, see [Start Using Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span></span>

### <a name="azure-role-based-access-control"></a><span data-ttu-id="371de-144">Kontrola dostępu oparta na rolach na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="371de-144">Azure Role-based Access Control</span></span>

<span data-ttu-id="371de-145">[Kontrola dostępu oparta na rolach Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) ułatwia administratorom Azure, zarządzanie zasobami tooAzure dostępu przez włączenie hello przyznawania dostępu na podstawie użytkownika hello przypisanej roli.</span><span class="sxs-lookup"><span data-stu-id="371de-145">[Azure Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helps Azure administrators manage access tooAzure resources by enabling hello granting of access based on hello user’s assigned role.</span></span> <span data-ttu-id="371de-146">Możesz rozdzielenie obowiązków w zespole i udzielić tylko hello ilość toousers dostępu, grup i aplikacji, że powinni tooperform swoich zadań.</span><span class="sxs-lookup"><span data-stu-id="371de-146">You can segregate duties within a team and grant only hello amount of access toousers, groups and applications that they need tooperform their jobs.</span></span>

<span data-ttu-id="371de-147">Dostępu na podstawie roli może zostać przydzielony toousers przy użyciu hello portalu Azure, narzędzi wiersza polecenia platformy Azure lub interfejsów API zarządzania platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="371de-147">Role-based access can be granted toousers using hello Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

<span data-ttu-id="371de-148">Aby uzyskać więcej informacji dotyczących podstaw Azure RBAC, zobacz [wprowadzenie opartej na rolach kontrola dostępu w hello portalu Azure.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span><span class="sxs-lookup"><span data-stu-id="371de-148">For more information about Azure RBAC basics, see [Get started with Role-Based Access Control in hello Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span></span>

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a><span data-ttu-id="371de-149">Jak zarządzać Azure RBAC przy użyciu programu PowerShell?</span><span class="sxs-lookup"><span data-stu-id="371de-149">How do I manage Azure RBAC with PowerShell?</span></span>

<span data-ttu-id="371de-150">Możesz użyć toomanage poleceń cmdlet programu PowerShell Azure RBAC, w tym hello następujące zadania związane z zarządzaniem:</span><span class="sxs-lookup"><span data-stu-id="371de-150">You can use PowerShell cmdlets toomanage Azure RBAC, including hello following management tasks:</span></span>

- <span data-ttu-id="371de-151">Lista ról</span><span class="sxs-lookup"><span data-stu-id="371de-151">List roles</span></span>

- <span data-ttu-id="371de-152">Zobacz, kto ma dostęp</span><span class="sxs-lookup"><span data-stu-id="371de-152">See who has access</span></span>

- <span data-ttu-id="371de-153">Udzielanie dostępu</span><span class="sxs-lookup"><span data-stu-id="371de-153">Grant access</span></span>

- <span data-ttu-id="371de-154">Usuń dostęp</span><span class="sxs-lookup"><span data-stu-id="371de-154">Remove access</span></span>

- <span data-ttu-id="371de-155">Tworzenie niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="371de-155">Create a custom role</span></span>

- <span data-ttu-id="371de-156">Pobierz akcji dla dostawcy zasobów</span><span class="sxs-lookup"><span data-stu-id="371de-156">Get Actions for a Resource Provider</span></span>

- <span data-ttu-id="371de-157">Modyfikowanie niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="371de-157">Modify a custom role</span></span>

- <span data-ttu-id="371de-158">Usunięcia niestandardowej roli zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="371de-158">Delete a custom role</span></span>

- <span data-ttu-id="371de-159">Lista ról niestandardowych</span><span class="sxs-lookup"><span data-stu-id="371de-159">List custom roles</span></span>

<span data-ttu-id="371de-160">Aby uzyskać instrukcje dotyczące toomanage Azure RBAC przy użyciu programu PowerShell, zobacz temat [opartej na rolach Zarządzanie dostępu przy użyciu programu Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span><span class="sxs-lookup"><span data-stu-id="371de-160">For instructions on how toomanage Azure RBAC with PowerShell, see [Manage Role-based Access with Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span></span>

### <a name="azure-multi-factor-authentication"></a><span data-ttu-id="371de-161">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="371de-161">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="371de-162">[Usługa Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) jest rozwiązaniem weryfikacji dwuetapowej, która ułatwia zabezpieczenie dostępu toodata i aplikacje, jednocześnie spełniając zapotrzebowanie na prosty proces logowania.</span><span class="sxs-lookup"><span data-stu-id="371de-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is a two-step verification solution that helps safeguard access toodata and applications, while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="371de-163">Oferuje ona silne uwierzytelnianie za pośrednictwem różnych metod weryfikacji, w tym weryfikacji w trakcie rozmowy telefonicznej albo przy użyciu wiadomości SMS lub aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="371de-163">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

<span data-ttu-id="371de-164">toodeploy MFA w hello chmury Azure należy toofirst ją włączyć, a następnie Włącz weryfikację dwuetapową dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="371de-164">toodeploy MFA in hello Azure cloud, you need toofirst enable it and then turn on two-step verification for users.</span></span>

#### <a name="how-do-i-enable-azure-toouse-mfa"></a><span data-ttu-id="371de-165">Jak włączyć Azure toouse MFA?</span><span class="sxs-lookup"><span data-stu-id="371de-165">How do I enable Azure toouse MFA?</span></span>

<span data-ttu-id="371de-166">Jeśli użytkownicy mają licencje, które obejmują usługi Azure Multi-Factor Authentication, nie ma nic konieczność tooturn toodo na usługę Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="371de-166">If your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="371de-167">W przeciwnym razie należy toocreate dostawcy uwierzytelniania wieloskładnikowego w katalogu.</span><span class="sxs-lookup"><span data-stu-id="371de-167">If not, you need toocreate a Multi-Factor Auth provider in your directory.</span></span> <span data-ttu-id="371de-168">toodo, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="371de-168">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="371de-169">Wybierz **usługi Active Directory** w hello klasycznego portalu Azure (zalogowany jako administrator).</span><span class="sxs-lookup"><span data-stu-id="371de-169">Select **Active Directory** in hello Azure classic portal (logged on as an administrator).</span></span>

2. <span data-ttu-id="371de-170">Wybierz **dostawców uwierzytelniania wieloskładnikowego.**</span><span class="sxs-lookup"><span data-stu-id="371de-170">Select **Multi-Factor Authentication Providers.**</span></span>

3. <span data-ttu-id="371de-171">Wybierz **nowy** , a następnie w obszarze **usługi aplikacji** wybierz **dostawcy uwierzytelniania wieloskładnikowego.**</span><span class="sxs-lookup"><span data-stu-id="371de-171">Select **New,** and then under **App Services,** select **Multi-Factor Auth Provider.**</span></span>

4. <span data-ttu-id="371de-172">Wybierz **szybkie tworzenie.**</span><span class="sxs-lookup"><span data-stu-id="371de-172">Select **Quick Create.**</span></span>

5. <span data-ttu-id="371de-173">Wypełnij pole Nazwa hello i wybierz model użycia (dla uwierzytelniania lub każdego włączonego użytkownika).</span><span class="sxs-lookup"><span data-stu-id="371de-173">Fill in hello name field and select a usage model (per authentication or per enabled user).</span></span>

6. <span data-ttu-id="371de-174">Wybierz katalog, z którego hello jest skojarzony dostawca usługi MFA.</span><span class="sxs-lookup"><span data-stu-id="371de-174">Designate a directory with which hello MFA Provider is associated.</span></span>

7. <span data-ttu-id="371de-175">Kliknij przycisk hello **Utwórz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="371de-175">Click hello **Create** button.</span></span>

![](media/protect-personal-data-identity-access-controls/quick-create.png)

<span data-ttu-id="371de-176">Aby uzyskać dodatkowe instrukcje na temat toomanage dostawcy uwierzytelniania wieloskładnikowego, zobacz [wprowadzenie do korzystania z dostawcy usługi Azure Multi-Factor Authentication.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span><span class="sxs-lookup"><span data-stu-id="371de-176">For more instructions on how toomanage your Multi-Factor Auth Provider, see [Getting Started with an Azure Multi-Factor Auth Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span></span>

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a><span data-ttu-id="371de-177">Jak włączyć weryfikację dwuetapową dla użytkowników?</span><span class="sxs-lookup"><span data-stu-id="371de-177">How do I turn on two-step verification for users?</span></span>

<span data-ttu-id="371de-178">Można wymusić weryfikacji dwuetapowej dla wszystkich logowania lub weryfikacji dwuetapowej toorequire zasady dostępu warunkowego można utworzyć tylko wtedy, gdy określone warunki są spełnione.</span><span class="sxs-lookup"><span data-stu-id="371de-178">You can enforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when specific conditions apply.</span></span>

<span data-ttu-id="371de-179">Włączanie usługi Azure MFA, zmieniając stanów użytkownika jest hello tradycyjne podejście, wymagająca weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="371de-179">Enabling Azure MFA by changing user states is hello traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="371de-180">Wszyscy użytkownicy hello, które można włączyć będą mieć hello tooperform sam wymóg włączono weryfikację dwuetapową, za każdym razem zalogują się w.</span><span class="sxs-lookup"><span data-stu-id="371de-180">All hello users that you enable will have hello same requirement tooperform two-step verification every time they sign in.</span></span> <span data-ttu-id="371de-181">Włączenie użytkownik zastępuje wszystkie zasady dostępu warunkowego, które mogą mieć wpływ na tego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="371de-181">Enabling a user overrides any conditional access policies that may affect that user.</span></span>

<span data-ttu-id="371de-182">Włączanie usługi Azure MFA z zasad dostępu warunkowego jest bardziej elastyczne podejście wymagająca weryfikacji dwuetapowej.</span><span class="sxs-lookup"><span data-stu-id="371de-182">Enabling Azure MFA with a conditional access policy is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="371de-183">Można utworzyć zasady dostępu warunkowego, które dotyczą toogroups, a także poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="371de-183">You can create conditional access policies that apply toogroups as well as individual users.</span></span> <span data-ttu-id="371de-184">O wysokim ryzyku grup można przydzielić więcej ograniczeń, niż niskiego ryzyka grup lub weryfikacji dwuetapowej mogą być wymagane tylko dla aplikacji w chmurze o wysokim ryzyku i pomijana dla nich niskiego ryzyka.</span><span class="sxs-lookup"><span data-stu-id="371de-184">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> <span data-ttu-id="371de-185">Dostęp warunkowy jest jednak płatnych funkcji usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="371de-185">However, conditional access is a paid feature of Azure Active Directory.</span></span>

<span data-ttu-id="371de-186">tooenable MFA przez zmianę stanu użytkownika hello następujące:</span><span class="sxs-lookup"><span data-stu-id="371de-186">tooenable MFA by changing user state, do hello following:</span></span>

1. <span data-ttu-id="371de-187">Zaloguj się toohello portalu Azure jako administrator.</span><span class="sxs-lookup"><span data-stu-id="371de-187">Sign in toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="371de-188">Przejdź za**usługi Azure Active Directory \> użytkowników i grup \> wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="371de-188">Go too**Azure Active Directory \> Users and groups \> All users**.</span></span>
3. <span data-ttu-id="371de-189">Wybierz **uwierzytelnianie wieloskładnikowe**.</span><span class="sxs-lookup"><span data-stu-id="371de-189">Select **Multi-Factor Authentication**.</span></span>
4. <span data-ttu-id="371de-190">Znajdź użytkownika hello mają tooenable dla usługi Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="371de-190">Find hello user that you want tooenable for Azure MFA.</span></span> <span data-ttu-id="371de-191">Może być konieczne toochange hello widoku u góry hello.</span><span class="sxs-lookup"><span data-stu-id="371de-191">You may need toochange hello view at hello top.</span></span>
5. <span data-ttu-id="371de-192">Sprawdź nazwę hello pole dalej toohello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="371de-192">Check hello box next toohello user’s name.</span></span>
6. <span data-ttu-id="371de-193">W prawo, w obszarze Szybkie kroki hello, wybierz polecenie **włączyć**.</span><span class="sxs-lookup"><span data-stu-id="371de-193">On hello right, under quick steps, choose **Enable**.</span></span>

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. <span data-ttu-id="371de-194">Potwierdź wybór w oknie podręcznym hello, który zostanie otwarty.</span><span class="sxs-lookup"><span data-stu-id="371de-194">Confirm your selection in hello pop-up window that opens.</span></span>  <span data-ttu-id="371de-195">Użytkownicy, dla których włączono uwierzytelnianie wieloskładnikowe zostanie wyświetlony monit tooregister hello następnym razem zalogują się w.</span><span class="sxs-lookup"><span data-stu-id="371de-195">Users for whom MFA has been enabled will be asked tooregister hello next time they sign in.</span></span>

<span data-ttu-id="371de-196">tooenable usługi Azure MFA za pomocą zasad dostępu warunkowego hello następujące:</span><span class="sxs-lookup"><span data-stu-id="371de-196">tooenable Azure MFA with a conditional access policy, do hello following:</span></span>

1. <span data-ttu-id="371de-197">Zaloguj się toohello portalu Azure jako administrator.</span><span class="sxs-lookup"><span data-stu-id="371de-197">Sign in toohello Azure portal as an administrator.</span></span>

2. <span data-ttu-id="371de-198">Przejdź za**usługi Azure Active Directory \> dostępu warunkowego**.</span><span class="sxs-lookup"><span data-stu-id="371de-198">Go too**Azure Active Directory \> Conditional access**.</span></span>

3. <span data-ttu-id="371de-199">Wybierz **nowe zasady**.</span><span class="sxs-lookup"><span data-stu-id="371de-199">Select **New policy**.</span></span>

4. <span data-ttu-id="371de-200">W obszarze **przypisania**, wybierz pozycję **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="371de-200">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="371de-201">Użyj hello **Include** i **wykluczyć** toospecify, którzy użytkownicy i grupy będą zarządzane przez zasady hello karty.</span><span class="sxs-lookup"><span data-stu-id="371de-201">Use hello **Include** and     **Exclude** tabs toospecify which users and groups will be managed by hello policy.</span></span>

5. <span data-ttu-id="371de-202">W obszarze **przypisania**, wybierz pozycję **aplikacji w chmurze.**</span><span class="sxs-lookup"><span data-stu-id="371de-202">Under **Assignments**, select **Cloud apps.**</span></span> <span data-ttu-id="371de-203">Wybierz zbyt**obejmują wszystkie aplikacje w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="371de-203">Choose too**include All cloud apps**.</span></span>
6.  <span data-ttu-id="371de-204">W obszarze **dostęp do formantów**, wybierz pozycję **Grant**.</span><span class="sxs-lookup"><span data-stu-id="371de-204">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="371de-205">Wybierz **wymusić uwierzytelnianie wieloskładnikowe**.</span><span class="sxs-lookup"><span data-stu-id="371de-205">Choose **Require multi-factor authentication**.</span></span>
7.  <span data-ttu-id="371de-206">Włącz **Włącz zasady** za**na** , a następnie wybierz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="371de-206">Turn **Enable policy** too**On** and then select **Save**.</span></span>

<span data-ttu-id="371de-207">Aby uzyskać informacje dotyczące sposobu tooset ustawienia usługi Azure MFA tooconfigure zapasowej alertów oszustwa, utworzyć jednorazowe obejście, użycia niestandardowe wiadomości głosowe, skonfiguruj buforowania, określ listę zaufanych adresów IP, tworzenie haseł aplikacji, Włącz zapamiętywanie MFA dla urządzeń, które ufają użytkowników, a następnie wybierz metody weryfikacji, zobacz [Konfigurowanie ustawień uwierzytelnianie wieloskładnikowe Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span><span class="sxs-lookup"><span data-stu-id="371de-207">For information on how tooconfigure Azure MFA settings tooset up fraud alerts, create a one-time bypass, use custom voice messages, configure caching, specify trusted IPs, create app passwords, enable remembering MFA for devices that users trust, and select verification methods, see [Configure Azure Multi-Factor Authentication Settings.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span></span>

## <a name="next-steps"></a><span data-ttu-id="371de-208">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="371de-208">Next steps</span></span>

- [<span data-ttu-id="371de-209">Zabezpieczanie uprzywilejowanego dostępu w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="371de-209">Securing privileged access in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [<span data-ttu-id="371de-210">Często zadawane pytania dotyczące usługi Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="371de-210">Frequently asked questions about Azure Multi-Factor Authentication</span></span>](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [<span data-ttu-id="371de-211">Oparta na rolach kontrola dostępu do rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="371de-211">Role-based Access Control troubleshooting</span></span>](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [<span data-ttu-id="371de-212">Ochronę tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="371de-212">Azure Active Directory Identity Protection</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
