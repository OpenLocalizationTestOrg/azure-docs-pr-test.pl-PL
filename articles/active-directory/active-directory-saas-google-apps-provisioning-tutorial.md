---
title: "Samouczek: Konfigurowanie usługi Google Apps dla użytkownika automatycznego inicjowania obsługi administracyjnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konta tooautomatically udostępniania i usuwanie użytkowników z usługi Azure AD tooGoogle aplikacji."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="4b179-103">Samouczek: Konfigurowanie usługi Google Apps dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="4b179-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="4b179-104">Celem Hello tego samouczka jest tooshow hello kroki potrzebne tooperform rezerw tooautomatically usługi Google Apps a usługą Azure AD i anulować aprowizację kont użytkowników z usługi Azure AD tooGoogle aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4b179-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Google Apps and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGoogle Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b179-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4b179-105">Prerequisites</span></span>

<span data-ttu-id="4b179-106">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4b179-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="4b179-107">Dzierżawy usługi Azure Active directory.</span><span class="sxs-lookup"><span data-stu-id="4b179-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="4b179-108">Musi mieć prawidłową dzierżawy dla usługi Google Apps pracy lub usługi Google Apps dla instytucji edukacyjnych.</span><span class="sxs-lookup"><span data-stu-id="4b179-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="4b179-109">Można użyć bezpłatnego konta wersji próbnej dla każdej usługi.</span><span class="sxs-lookup"><span data-stu-id="4b179-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="4b179-110">Konto użytkownika w usłudze Google Apps z uprawnieniami administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="4b179-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-toogoogle-apps"></a><span data-ttu-id="4b179-111">Przypisywanie użytkowników tooGoogle aplikacji</span><span class="sxs-lookup"><span data-stu-id="4b179-111">Assigning users tooGoogle Apps</span></span>

<span data-ttu-id="4b179-112">Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu.</span><span class="sxs-lookup"><span data-stu-id="4b179-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="4b179-113">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="4b179-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="4b179-114">Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentowania hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji Google Apps tooyour.</span><span class="sxs-lookup"><span data-stu-id="4b179-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Google Apps app.</span></span> <span data-ttu-id="4b179-115">Po decyzję, wykonując następujące instrukcje hello tutaj można przypisać aplikacji Google Apps tooyour tych użytkowników: [przypisanie użytkownika lub grupy aplikacji przedsiębiorstwa tooan](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="4b179-115">Once decided, you can assign these users tooyour Google Apps app by following hello instructions here: [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="4b179-116">Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać hello tootest aplikacji tooGoogle inicjowania obsługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4b179-116">It is recommended that a single Azure AD user be assigned tooGoogle Apps tootest hello provisioning configuration.</span></span> <span data-ttu-id="4b179-117">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="4b179-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="4b179-118">Podczas przypisywania tooGoogle użytkownika aplikacji, należy wybrać w oknie dialogowym przydział hello hello użytkownika lub roli "Grupy".</span><span class="sxs-lookup"><span data-stu-id="4b179-118">When assigning a user tooGoogle Apps, you must select hello User or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="4b179-119">Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="4b179-119">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="4b179-120">Włącz inicjowanie obsługi użytkowników automatycznych</span><span class="sxs-lookup"><span data-stu-id="4b179-120">Enable automated user provisioning</span></span>

<span data-ttu-id="4b179-121">Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika aplikacji tooGoogle Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w usługi Google Apps na podstawie przypisań użytkowników i grup w usłudze Azure AD .</span><span class="sxs-lookup"><span data-stu-id="4b179-121">This section guides you through connecting your Azure AD tooGoogle Apps's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="4b179-122">Można też tooenabled na języku SAML logowania jednokrotnego dla aplikacji Google, hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4b179-122">You may also choose tooenabled SAML-based Single Sign-On for Google Apps, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4b179-123">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="4b179-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="4b179-124">Skonfiguruj użytkownika automatyczne Inicjowanie obsługi konta</span><span class="sxs-lookup"><span data-stu-id="4b179-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="4b179-125">Inną opcją działało do automatyzacji aprowizacji aplikacji tooGoogle użytkowników jest toouse [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) który inicjuje tooGoogle tożsamości aplikacji z lokalnej usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4b179-125">Another viable option for automating user provisioning tooGoogle Apps is toouse [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities tooGoogle Apps.</span></span> <span data-ttu-id="4b179-126">Z kolei hello rozwiązanie w tym samouczku udostępnia usługi Azure Active Directory (w chmurze), użytkowników i grup z włączoną obsługą poczty tooGoogle aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4b179-126">In contrast, hello solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups tooGoogle Apps.</span></span> 

1. <span data-ttu-id="4b179-127">Zaloguj się na powitania [konsoli administracyjnej usługi Google Apps](http://admin.google.com/) przy użyciu konta administratora, a następnie kliknij przycisk **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="4b179-127">Sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="4b179-128">Jeśli nie widzisz hello łącza może być ukryty w obszarze hello **więcej formantów** menu u dołu hello hello ekranu.</span><span class="sxs-lookup"><span data-stu-id="4b179-128">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Kliknij pozycję Zabezpieczenia.][10]

2. <span data-ttu-id="4b179-130">Na powitania **zabezpieczeń** kliknij przycisk **dokumentacja interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="4b179-130">On hello **Security** page, click **API Reference**.</span></span>
   
    ![Kliknij przycisk dokumentacja interfejsu API.][15]

3. <span data-ttu-id="4b179-132">Wybierz **dostęp włączyć API**.</span><span class="sxs-lookup"><span data-stu-id="4b179-132">Select **Enable API access**.</span></span>
   
    ![Kliknij przycisk dokumentacja interfejsu API.][16]

    > [!IMPORTANT]
    > <span data-ttu-id="4b179-134">Dla każdego użytkownika, który ma tooGoogle tooprovision aplikacji, swoją nazwę użytkownika w usłudze Azure Active Directory *musi* można wiązanej tooa domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="4b179-134">For every user that you intend tooprovision tooGoogle Apps, their username in Azure Active Directory *must* be tied tooa custom domain.</span></span> <span data-ttu-id="4b179-135">Na przykład nazwy użytkowników, które przypominają bob@contoso.onmicrosoft.com nie jest akceptowane przez usługi Google Apps, podczas gdy bob@contoso.com została zaakceptowana.</span><span class="sxs-lookup"><span data-stu-id="4b179-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="4b179-136">Istniejącego użytkownika domeny można zmienić, edytując właściwości ich w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b179-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="4b179-137">Instrukcje dla jak tooset domeny niestandardowej dla usługi Azure Active Directory i usługi Google Apps znajdują się w następujących krokach.</span><span class="sxs-lookup"><span data-stu-id="4b179-137">Instructions for how tooset a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="4b179-138">Nie dodano jeszcze tooyour nazwy domeny niestandardowej usługi Azure Active Directory, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="4b179-138">If you haven't added a custom domain name tooyour Azure Active Directory yet, then follow hello following steps:</span></span>
  
    <span data-ttu-id="4b179-139">a.</span><span class="sxs-lookup"><span data-stu-id="4b179-139">a.</span></span> <span data-ttu-id="4b179-140">W hello [portalu Azure](https://portal.azure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b179-140">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="4b179-141">Na liście hello katalogu wybierz swój katalog.</span><span class="sxs-lookup"><span data-stu-id="4b179-141">In hello directory list, select your directory.</span></span> 

    <span data-ttu-id="4b179-142">b.</span><span class="sxs-lookup"><span data-stu-id="4b179-142">b.</span></span> <span data-ttu-id="4b179-143">Kliknij przycisk **nazwy domen** na hello w lewym okienku nawigacji, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="4b179-143">Click **Domains name** on hello left navigation pane, and then click **Add**.</span></span>
     
     ![Domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![Dodawanie domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="4b179-146">c.</span><span class="sxs-lookup"><span data-stu-id="4b179-146">c.</span></span> <span data-ttu-id="4b179-147">Wpisz nazwę domeny do hello **nazwy domeny** pola.</span><span class="sxs-lookup"><span data-stu-id="4b179-147">Type your domain name into hello **Domain name** field.</span></span> <span data-ttu-id="4b179-148">Ta nazwa domeny musi być hello tej samej nazwy domeny czy zamierzasz toouse usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="4b179-148">This domain name should be hello same domain name that you intend toouse for Google Apps.</span></span> <span data-ttu-id="4b179-149">Po wykonaniu tych czynności kliknij przycisk hello **Dodawanie domeny** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4b179-149">When ready, click hello **Add Domain** button.</span></span>
     
     ![Nazwa domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="4b179-151">d.</span><span class="sxs-lookup"><span data-stu-id="4b179-151">d.</span></span> <span data-ttu-id="4b179-152">Kliknij przycisk **dalej** toogo toohello weryfikacji strony.</span><span class="sxs-lookup"><span data-stu-id="4b179-152">Click **Next** toogo toohello verification page.</span></span> <span data-ttu-id="4b179-153">tooverify, że jesteś właścicielem tej domeny, należy edytować rekordy DNS domeny hello zgodnie z wartościami toohello na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="4b179-153">tooverify that you own this domain, you must edit hello domain's DNS records according toohello values provided on this page.</span></span> <span data-ttu-id="4b179-154">Możesz wybrać tooverify za pomocą **rekordów MX** lub **rekordów TXT**w oparciu o wybór dla hello **typu rekordu** opcji.</span><span class="sxs-lookup"><span data-stu-id="4b179-154">You may choose tooverify using either **MX records** or **TXT records**, depending on what you select for hello **Record Type** option.</span></span> <span data-ttu-id="4b179-155">Bardziej szczegółowe instrukcje dotyczące sposobu nazwa domeny tooverify z usługą Azure AD, zobacz [dodać własne tooAzure nazwy domeny AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="4b179-155">For more comprehensive instructions on how tooverify domain name with Azure AD, refer [Add your own domain name tooAzure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![Domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="4b179-157">e.</span><span class="sxs-lookup"><span data-stu-id="4b179-157">e.</span></span> <span data-ttu-id="4b179-158">Powtórz hello w poprzednich krokach dla wszystkich domen hello, który ma tooadd tooyour katalogu.</span><span class="sxs-lookup"><span data-stu-id="4b179-158">Repeat hello preceding steps for all hello domains that you intend tooadd tooyour directory.</span></span>

5. <span data-ttu-id="4b179-159">Po zweryfikowaniu wszystkich domen z usługą Azure AD, należy teraz sprawdzenie je ponownie z usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="4b179-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="4b179-160">Dla każdej domeny, która nie jest już zarejestrowany przy użyciu usługi Google Apps wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="4b179-160">For each domain that isn't already registered with Google Apps, perform hello following steps:</span></span>
   
    <span data-ttu-id="4b179-161">a.</span><span class="sxs-lookup"><span data-stu-id="4b179-161">a.</span></span> <span data-ttu-id="4b179-162">W hello [konsoli administracyjnej usługi Google Apps](http://admin.google.com/), kliknij przycisk **domen**.</span><span class="sxs-lookup"><span data-stu-id="4b179-162">In hello [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![Kliknij w domenach][20]

    <span data-ttu-id="4b179-164">b.</span><span class="sxs-lookup"><span data-stu-id="4b179-164">b.</span></span> <span data-ttu-id="4b179-165">Kliknij przycisk **Dodawanie domeny lub alias domeny**.</span><span class="sxs-lookup"><span data-stu-id="4b179-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![Dodaj nową domenę][21]

    <span data-ttu-id="4b179-167">c.</span><span class="sxs-lookup"><span data-stu-id="4b179-167">c.</span></span> <span data-ttu-id="4b179-168">Wybierz **Dodaj inną domenę**i wpisz nazwę hello hello domeny, które chcesz tooadd.</span><span class="sxs-lookup"><span data-stu-id="4b179-168">Select **Add another domain**, and type in hello name of hello domain that you would like tooadd.</span></span>
     
     ![Wpisz nazwę domeny][22]

    <span data-ttu-id="4b179-170">d.</span><span class="sxs-lookup"><span data-stu-id="4b179-170">d.</span></span> <span data-ttu-id="4b179-171">Kliknij przycisk **Kontynuuj i Zweryfikuj prawo własności do domeny**.</span><span class="sxs-lookup"><span data-stu-id="4b179-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="4b179-172">Następnie wykonaj tooverify kroki hello czy własnej nazwy domeny hello.</span><span class="sxs-lookup"><span data-stu-id="4b179-172">Then follow hello steps tooverify that you own hello domain name.</span></span> <span data-ttu-id="4b179-173">Kompleksowe instrukcje na tooverify domeny usługi Google Apps, zobacz temat.</span><span class="sxs-lookup"><span data-stu-id="4b179-173">For comprehensive instructions on how tooverify your domain with Google Apps, see.</span></span> <span data-ttu-id="4b179-174">[Zweryfikowanie prawa własności lokacji z usługi Google Apps](https://support.google.com/webmasters/answer/35179).</span><span class="sxs-lookup"><span data-stu-id="4b179-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="4b179-175">e.</span><span class="sxs-lookup"><span data-stu-id="4b179-175">e.</span></span> <span data-ttu-id="4b179-176">Powtórz hello w poprzednich krokach dla dodatkowe domeny, który ma tooGoogle tooadd aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4b179-176">Repeat hello preceding steps for any additional domains that you intend tooadd tooGoogle Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="4b179-177">Jeśli zmienisz hello domena podstawowa dla dzierżawy usługi Google Apps i jeśli masz już skonfigurowane logowanie jednokrotne z usługą Azure AD, a następnie masz toorepeat krok #3 w obszarze [krok dwa: Włącz logowanie jednokrotne](#step-two-enable-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="4b179-177">If you change hello primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have toorepeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="4b179-178">W hello [konsoli administracyjnej usługi Google Apps](http://admin.google.com/), kliknij przycisk **ról administratora**.</span><span class="sxs-lookup"><span data-stu-id="4b179-178">In hello [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![Polecenie usługi Google Apps][26]

7. <span data-ttu-id="4b179-180">Określić, które administrator konta ma Inicjowanie obsługi użytkowników toomanage toouse.</span><span class="sxs-lookup"><span data-stu-id="4b179-180">Determine which admin account you would like toouse toomanage user provisioning.</span></span> <span data-ttu-id="4b179-181">Dla hello **rolę administratora** tego konta, Edytuj hello **uprawnienia** dla tej roli.</span><span class="sxs-lookup"><span data-stu-id="4b179-181">For hello **admin role** of that account, edit hello **Privileges** for that role.</span></span> <span data-ttu-id="4b179-182">Upewnij się, że ma ona wszystkie hello **uprawnień interfejsu API administratora** włączane tego konta można używać do inicjowania obsługi.</span><span class="sxs-lookup"><span data-stu-id="4b179-182">Make sure it has all hello **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![Polecenie usługi Google Apps][27]
   
    > [!NOTE]
    > <span data-ttu-id="4b179-184">W przypadku konfigurowania środowiska produkcyjnego, hello najlepszym rozwiązaniem jest toocreate konto administratora usługi Google Apps specjalnie dla tego kroku.</span><span class="sxs-lookup"><span data-stu-id="4b179-184">If you are configuring a production environment, hello best practice is toocreate an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="4b179-185">Te konta musi mieć rolę administratora skojarzonego z nim, którą ma niezbędne uprawnienia interfejsu API hello.</span><span class="sxs-lookup"><span data-stu-id="4b179-185">These accounts must have an admin role associated with it that has hello necessary API privileges.</span></span>
     
8. <span data-ttu-id="4b179-186">W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="4b179-186">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="4b179-187">Jeśli został już skonfigurowany dla logowania jednokrotnego usługi Google Apps, wyszukaj dla swojego wystąpienia usługi Google Apps za pomocą pola wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="4b179-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using hello search field.</span></span> <span data-ttu-id="4b179-188">W przeciwnym razie wybierz **Dodaj** i wyszukaj **usługi Google Apps** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="4b179-188">Otherwise, select **Add** and search for **Google Apps** in hello application gallery.</span></span> <span data-ttu-id="4b179-189">Wybierz usługi Google Apps z wyników wyszukiwania hello i dodać tooyour listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4b179-189">Select Google Apps from hello search results, and add it tooyour list of applications.</span></span>

10. <span data-ttu-id="4b179-190">Wybierz wystąpienie usługi Google Apps, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="4b179-190">Select your instance of Google Apps, then select hello **Provisioning** tab.</span></span>

11. <span data-ttu-id="4b179-191">Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="4b179-191">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

     ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="4b179-193">W obszarze hello **poświadczeń administratora** kliknij **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="4b179-193">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="4b179-194">Otwiera okno dialogowe autoryzacji usługi Google Apps w nowym oknie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="4b179-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="4b179-195">Upewnij się, chcieliby toogive usługi Azure Active Directory uprawnienia toomake zmiany dzierżawy tooyour usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="4b179-195">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Google Apps tenant.</span></span> <span data-ttu-id="4b179-196">Kliknij przycisk **zaakceptować**.</span><span class="sxs-lookup"><span data-stu-id="4b179-196">Click **Accept**.</span></span>
    
     ![Upewnij się, uprawnienia.][28]

14. <span data-ttu-id="4b179-198">W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć aplikację usługi Google Apps tooyour.</span><span class="sxs-lookup"><span data-stu-id="4b179-198">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Google Apps app.</span></span> <span data-ttu-id="4b179-199">Jeśli hello połączenia nie powiedzie się, upewnij się, Twoje konto usługi Google Apps ma uprawnienia administratora zespołu i spróbuj hello **"Autoryzuj"** krok ponownie.</span><span class="sxs-lookup"><span data-stu-id="4b179-199">If hello connection fails, ensure your Google Apps account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

15. <span data-ttu-id="4b179-200">Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="4b179-200">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

16. <span data-ttu-id="4b179-201">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="4b179-201">Click **Save.**</span></span>

17. <span data-ttu-id="4b179-202">W obszarze hello sekcji mapowania, wybierz **tooGoogle synchronizacji Azure Active Directory użytkowników aplikacji.**</span><span class="sxs-lookup"><span data-stu-id="4b179-202">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGoogle Apps.**</span></span>

18. <span data-ttu-id="4b179-203">W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługi Azure AD tooGoogle aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4b179-203">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGoogle Apps.</span></span> <span data-ttu-id="4b179-204">Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom usługi Google Apps dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="4b179-204">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="4b179-205">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="4b179-205">Select hello Save button toocommit any changes.</span></span>

19. <span data-ttu-id="4b179-206">tooenable hello inicjowania obsługi usługi Azure AD dla usługi Google Apps hello zmiany **stan inicjowania obsługi administracyjnej** za**na** w sekcji Ustawienia hello</span><span class="sxs-lookup"><span data-stu-id="4b179-206">tooenable hello Azure AD provisioning service for Google Apps, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

20. <span data-ttu-id="4b179-207">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="4b179-207">Click **Save.**</span></span>

<span data-ttu-id="4b179-208">Rozpoczyna hello wstępnej synchronizacji użytkowników i/lub grupy przypisane aplikacje tooGoogle w sekcji hello użytkowników i grup.</span><span class="sxs-lookup"><span data-stu-id="4b179-208">It starts hello initial synchronization of any users and/or groups assigned tooGoogle Apps in hello Users and Groups section.</span></span> <span data-ttu-id="4b179-209">Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello.</span><span class="sxs-lookup"><span data-stu-id="4b179-209">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="4b179-210">Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello świadczenie usługi w aplikacji usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="4b179-210">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4b179-211">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4b179-211">Additional resources</span></span>

* [<span data-ttu-id="4b179-212">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="4b179-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b179-213">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4b179-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="4b179-214">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4b179-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png