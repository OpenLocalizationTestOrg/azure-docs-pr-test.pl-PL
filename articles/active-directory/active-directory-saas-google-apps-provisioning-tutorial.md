---
title: "Samouczek: Konfigurowanie usługi Google Apps dla użytkownika automatycznego inicjowania obsługi administracyjnej na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD do usługi Google Apps."
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
ms.openlocfilehash: b061f0ddad70be4a5ca48d48d1a737d6af8afa8d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="b1f8b-103">Samouczek: Konfigurowanie usługi Google Apps dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="b1f8b-104">Celem tego samouczka jest opisano czynności, które należy wykonać w usługi Google Apps a usługą Azure AD, aby automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD do usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-104">The objective of this tutorial is to show you the steps you need to perform in Google Apps and Azure AD to automatically provision and de-provision user accounts from Azure AD to Google Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1f8b-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b1f8b-105">Prerequisites</span></span>

<span data-ttu-id="b1f8b-106">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b1f8b-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="b1f8b-107">Dzierżawy usługi Azure Active directory.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="b1f8b-108">Musi mieć prawidłową dzierżawy dla usługi Google Apps pracy lub usługi Google Apps dla instytucji edukacyjnych.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="b1f8b-109">Można użyć bezpłatnego konta wersji próbnej dla każdej usługi.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="b1f8b-110">Konto użytkownika w usłudze Google Apps z uprawnieniami administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-to-google-apps"></a><span data-ttu-id="b1f8b-111">Przypisywanie użytkowników do usługi Google Apps</span><span class="sxs-lookup"><span data-stu-id="b1f8b-111">Assigning users to Google Apps</span></span>

<span data-ttu-id="b1f8b-112">Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="b1f8b-113">W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="b1f8b-114">Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, należy zdecydować, jakie użytkownicy i/lub grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do aplikacji Google Apps.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Google Apps app.</span></span> <span data-ttu-id="b1f8b-115">Po decyzję, postępując zgodnie z instrukcjami w tym miejscu można przypisać tych użytkowników aplikacji Google Apps: [przypisać użytkownika lub grupy do aplikacji w przedsiębiorstwie](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="b1f8b-115">Once decided, you can assign these users to your Google Apps app by following the instructions here: [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="b1f8b-116">Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać do usługi Google Apps do testowania konfiguracji inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-116">It is recommended that a single Azure AD user be assigned to Google Apps to test the provisioning configuration.</span></span> <span data-ttu-id="b1f8b-117">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="b1f8b-118">Podczas przypisywania użytkowników do usługi Google Apps, należy wybrać w oknie dialogowym przydział roli użytkownika lub "Grupy".</span><span class="sxs-lookup"><span data-stu-id="b1f8b-118">When assigning a user to Google Apps, you must select the User or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="b1f8b-119">Rola "Domyślnego dostępu" nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-119">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="b1f8b-120">Włącz inicjowanie obsługi użytkowników automatycznych</span><span class="sxs-lookup"><span data-stu-id="b1f8b-120">Enable automated user provisioning</span></span>

<span data-ttu-id="b1f8b-121">Przewodniki dotyczące tej sekcji przez łączenie usługi Azure AD z interfejsu API inicjowania obsługi administracyjnej konta użytkownika usługi Google Apps i konfigurowanie usługi inicjowania obsługi administracyjnej do tworzenia, aktualizacji i wyłączania konta użytkowników przypisane w usłudze Google Apps na podstawie użytkownika i przypisanie do grupy w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-121">This section guides you through connecting your Azure AD to Google Apps's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="b1f8b-122">Można też włączone na języku SAML logowania jednokrotnego dla aplikacji Google, postępując zgodnie z instrukcjami zawarte w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b1f8b-122">You may also choose to enabled SAML-based Single Sign-On for Google Apps, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b1f8b-123">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="b1f8b-124">Skonfiguruj użytkownika automatyczne Inicjowanie obsługi konta</span><span class="sxs-lookup"><span data-stu-id="b1f8b-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="b1f8b-125">Inny wygodną opcją do automatyzacji Inicjowanie obsługi użytkowników do usługi Google Apps jest użycie [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) który inicjuje Twoich tożsamości: lokalnej usługi Active Directory do usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-125">Another viable option for automating user provisioning to Google Apps is to use [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities to Google Apps.</span></span> <span data-ttu-id="b1f8b-126">Natomiast rozwiązanie w tym samouczku inicjuje użytkowników usługi Azure Active Directory (w chmurze), a grupy obsługujące pocztę do usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-126">In contrast, the solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups to Google Apps.</span></span> 

1. <span data-ttu-id="b1f8b-127">Zaloguj się do [konsoli administracyjnej usługi Google Apps](http://admin.google.com/) przy użyciu konta administratora, a następnie kliknij przycisk **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-127">Sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="b1f8b-128">Jeśli nie widzisz łącza może być ukryty w obszarze **więcej formantów** menu u dołu ekranu.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-128">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![Kliknij pozycję Zabezpieczenia.][10]

2. <span data-ttu-id="b1f8b-130">Na **zabezpieczeń** kliknij przycisk **dokumentacja interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-130">On the **Security** page, click **API Reference**.</span></span>
   
    ![Kliknij przycisk dokumentacja interfejsu API.][15]

3. <span data-ttu-id="b1f8b-132">Wybierz **dostęp włączyć API**.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-132">Select **Enable API access**.</span></span>
   
    ![Kliknij przycisk dokumentacja interfejsu API.][16]

    > [!IMPORTANT]
    > <span data-ttu-id="b1f8b-134">Dla każdego użytkownika, który ma obsługiwać usługi Google Apps swoją nazwę użytkownika w usłudze Azure Active Directory *musi* ograniczeni do domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-134">For every user that you intend to provision to Google Apps, their username in Azure Active Directory *must* be tied to a custom domain.</span></span> <span data-ttu-id="b1f8b-135">Na przykład nazwy użytkowników, które przypominają bob@contoso.onmicrosoft.com nie jest akceptowane przez usługi Google Apps, podczas gdy bob@contoso.com została zaakceptowana.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="b1f8b-136">Istniejącego użytkownika domeny można zmienić, edytując właściwości ich w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="b1f8b-137">Instrukcje dotyczące sposobu ustawiania domeny niestandardowej dla usługi Azure Active Directory i usługi Google Apps znajdują się w następujących czynności.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-137">Instructions for how to set a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="b1f8b-138">Jeśli nie dodano jeszcze niestandardowej nazwy domeny do usługi Azure Active Directory, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b1f8b-138">If you haven't added a custom domain name to your Azure Active Directory yet, then follow the following steps:</span></span>
  
    <span data-ttu-id="b1f8b-139">a.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-139">a.</span></span> <span data-ttu-id="b1f8b-140">W [portalu Azure](https://portal.azure.com), w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-140">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="b1f8b-141">Na liście katalog wybierz swój katalog.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-141">In the directory list, select your directory.</span></span> 

    <span data-ttu-id="b1f8b-142">b.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-142">b.</span></span> <span data-ttu-id="b1f8b-143">Kliknij przycisk **nazwy domen** w lewym okienku nawigacji, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-143">Click **Domains name** on the left navigation pane, and then click **Add**.</span></span>
     
     ![Domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![Dodawanie domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="b1f8b-146">c.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-146">c.</span></span> <span data-ttu-id="b1f8b-147">Wpisz nazwę domeny do **nazwy domeny** pola.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-147">Type your domain name into the **Domain name** field.</span></span> <span data-ttu-id="b1f8b-148">Ta nazwa domeny powinien być tej samej nazwy domeny, która ma być używana dla konta Google Apps.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-148">This domain name should be the same domain name that you intend to use for Google Apps.</span></span> <span data-ttu-id="b1f8b-149">Po wykonaniu tych czynności kliknij przycisk **Dodawanie domeny** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-149">When ready, click the **Add Domain** button.</span></span>
     
     ![Nazwa domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="b1f8b-151">d.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-151">d.</span></span> <span data-ttu-id="b1f8b-152">Kliknij przycisk **dalej** aby przejść do strony weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-152">Click **Next** to go to the verification page.</span></span> <span data-ttu-id="b1f8b-153">Aby sprawdzić, czy jesteś właścicielem tej domeny, należy edytować rekordy DNS w domenie, zgodnie z wartościami dostępnych na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-153">To verify that you own this domain, you must edit the domain's DNS records according to the values provided on this page.</span></span> <span data-ttu-id="b1f8b-154">Można sprawdzić za pomocą **rekordów MX** lub **rekordów TXT**w oparciu o wybór dla **typu rekordu** opcji.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-154">You may choose to verify using either **MX records** or **TXT records**, depending on what you select for the **Record Type** option.</span></span> <span data-ttu-id="b1f8b-155">Bardziej szczegółowe instrukcje dotyczące sposobu weryfikowania nazwy domeny w usłudze Azure AD, zobacz [Dodaj własną nazwę domeny do usługi Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="b1f8b-155">For more comprehensive instructions on how to verify domain name with Azure AD, refer [Add your own domain name to Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![Domeny](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="b1f8b-157">e.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-157">e.</span></span> <span data-ttu-id="b1f8b-158">Powtórz poprzednie kroki dla wszystkich domen, które mają zostać dodane do katalogu.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-158">Repeat the preceding steps for all the domains that you intend to add to your directory.</span></span>

5. <span data-ttu-id="b1f8b-159">Po zweryfikowaniu wszystkich domen z usługą Azure AD, należy teraz sprawdzenie je ponownie z usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="b1f8b-160">Dla każdej domeny, która nie jest już zarejestrowany przy użyciu usługi Google Apps wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b1f8b-160">For each domain that isn't already registered with Google Apps, perform the following steps:</span></span>
   
    <span data-ttu-id="b1f8b-161">a.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-161">a.</span></span> <span data-ttu-id="b1f8b-162">W [konsoli administracyjnej usługi Google Apps](http://admin.google.com/), kliknij przycisk **domen**.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-162">In the [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![Kliknij w domenach][20]

    <span data-ttu-id="b1f8b-164">b.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-164">b.</span></span> <span data-ttu-id="b1f8b-165">Kliknij przycisk **Dodawanie domeny lub alias domeny**.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![Dodaj nową domenę][21]

    <span data-ttu-id="b1f8b-167">c.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-167">c.</span></span> <span data-ttu-id="b1f8b-168">Wybierz **Dodaj inną domenę**i wpisz nazwę domeny, który chcesz dodać.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-168">Select **Add another domain**, and type in the name of the domain that you would like to add.</span></span>
     
     ![Wpisz nazwę domeny][22]

    <span data-ttu-id="b1f8b-170">d.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-170">d.</span></span> <span data-ttu-id="b1f8b-171">Kliknij przycisk **Kontynuuj i Zweryfikuj prawo własności do domeny**.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="b1f8b-172">Następnie wykonaj kroki, aby sprawdzić, czy jesteś właścicielem nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-172">Then follow the steps to verify that you own the domain name.</span></span> <span data-ttu-id="b1f8b-173">Kompleksowe instrukcje na temat sposobu Sprawdź domenę z usługi Google Apps Zobacz.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-173">For comprehensive instructions on how to verify your domain with Google Apps, see.</span></span> <span data-ttu-id="b1f8b-174">[Zweryfikowanie prawa własności lokacji z usługi Google Apps](https://support.google.com/webmasters/answer/35179).</span><span class="sxs-lookup"><span data-stu-id="b1f8b-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="b1f8b-175">e.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-175">e.</span></span> <span data-ttu-id="b1f8b-176">Powtórz poprzednie kroki dla dodatkowe domeny, które mają zostać dodane do usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-176">Repeat the preceding steps for any additional domains that you intend to add to Google Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="b1f8b-177">Jeśli zmienisz domena podstawowa dla dzierżawy usługi Google Apps i jeśli masz już skonfigurowane logowanie jednokrotne z usługą Azure AD, a następnie trzeba powtórzyć krok #3 w obszarze [krok dwa: Włącz logowanie jednokrotne](#step-two-enable-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="b1f8b-177">If you change the primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have to repeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="b1f8b-178">W [konsoli administracyjnej usługi Google Apps](http://admin.google.com/), kliknij przycisk **ról administratora**.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-178">In the [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![Polecenie usługi Google Apps][26]

7. <span data-ttu-id="b1f8b-180">Określ konto administratora, które chcesz użyć do zarządzania, inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-180">Determine which admin account you would like to use to manage user provisioning.</span></span> <span data-ttu-id="b1f8b-181">Aby uzyskać **rolę administratora** tego konta, Edytuj **uprawnienia** dla tej roli.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-181">For the **admin role** of that account, edit the **Privileges** for that role.</span></span> <span data-ttu-id="b1f8b-182">Upewnij się, że zawiera wszystkie **uprawnień interfejsu API administratora** włączane tego konta można używać do inicjowania obsługi.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-182">Make sure it has all the **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![Polecenie usługi Google Apps][27]
   
    > [!NOTE]
    > <span data-ttu-id="b1f8b-184">W przypadku konfigurowania środowiska produkcyjnego, najlepszym rozwiązaniem jest tworzenie konta administratora w usłudze Google Apps specjalnie dla tego kroku.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-184">If you are configuring a production environment, the best practice is to create an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="b1f8b-185">Te konta musi mieć rolę administratora skojarzonego z nim, którą ma niezbędne uprawnienia interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-185">These accounts must have an admin role associated with it that has the necessary API privileges.</span></span>
     
8. <span data-ttu-id="b1f8b-186">W [portalu Azure](https://portal.azure.com), przejdź do **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-186">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="b1f8b-187">Jeśli został już skonfigurowany dla logowania jednokrotnego usługi Google Apps, wyszukaj dla swojego wystąpienia usługi Google Apps za pomocą pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using the search field.</span></span> <span data-ttu-id="b1f8b-188">W przeciwnym razie wybierz **Dodaj** i wyszukaj **usługi Google Apps** w galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-188">Otherwise, select **Add** and search for **Google Apps** in the application gallery.</span></span> <span data-ttu-id="b1f8b-189">Wybierz usługi Google Apps z wyników wyszukiwania, a następnie dodaj go do listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-189">Select Google Apps from the search results, and add it to your list of applications.</span></span>

10. <span data-ttu-id="b1f8b-190">Wybierz wystąpienie usługi Google Apps, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-190">Select your instance of Google Apps, then select the **Provisioning** tab.</span></span>

11. <span data-ttu-id="b1f8b-191">Ustaw **tryb obsługi administracyjnej** do **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-191">Set the **Provisioning Mode** to **Automatic**.</span></span> 

     ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="b1f8b-193">W obszarze **poświadczeń administratora** kliknij **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-193">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="b1f8b-194">Otwiera okno dialogowe autoryzacji usługi Google Apps w nowym oknie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="b1f8b-195">Upewnij się, że chcesz nadać uprawnienia usługi Azure Active Directory, aby wprowadzić zmiany w dzierżawie usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-195">Confirm that you would like to give Azure Active Directory permission to make changes to your Google Apps tenant.</span></span> <span data-ttu-id="b1f8b-196">Kliknij przycisk **zaakceptować**.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-196">Click **Accept**.</span></span>
    
     ![Upewnij się, uprawnienia.][28]

14. <span data-ttu-id="b1f8b-198">W portalu Azure kliknij **Testuj połączenie** zapewniające usługi Azure AD mogą łączyć się z aplikacji Google Apps.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-198">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Google Apps app.</span></span> <span data-ttu-id="b1f8b-199">Jeśli połączenie nie powiedzie się, upewnij się, Twoje konto usługi Google Apps ma uprawnienia administratora zespołu i spróbuj **"Autoryzuj"** krok ponownie.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-199">If the connection fails, ensure your Google Apps account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

15. <span data-ttu-id="b1f8b-200">Wprowadź adres e-mail osoby lub grupy, który powinien zostać wyświetlony inicjowania obsługi administracyjnej powiadomienia o błędach w **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-200">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

16. <span data-ttu-id="b1f8b-201">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="b1f8b-201">Click **Save.**</span></span>

17. <span data-ttu-id="b1f8b-202">W sekcji mapowania wybierz **synchronizacji Azure użytkownicy usługi Active Directory do usługi Google Apps.**</span><span class="sxs-lookup"><span data-stu-id="b1f8b-202">Under the Mappings section, select **Synchronize Azure Active Directory Users to Google Apps.**</span></span>

18. <span data-ttu-id="b1f8b-203">W **mapowań atrybutów** Przejrzyj atrybuty użytkowników, które są synchronizowane z usługi Azure AD do usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-203">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Google Apps.</span></span> <span data-ttu-id="b1f8b-204">Atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania kont użytkowników w usługi Google Apps dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-204">The attributes selected as **Matching** properties are used to match the user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="b1f8b-205">Wybierz przycisk Zapisz, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-205">Select the Save button to commit any changes.</span></span>

19. <span data-ttu-id="b1f8b-206">Aby włączyć usługi Azure AD, świadczenie usługi dla usługi Google Apps, zmień **stan inicjowania obsługi administracyjnej** do **na** w sekcji Ustawienia</span><span class="sxs-lookup"><span data-stu-id="b1f8b-206">To enable the Azure AD provisioning service for Google Apps, change the **Provisioning Status** to **On** in the Settings section</span></span>

20. <span data-ttu-id="b1f8b-207">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="b1f8b-207">Click **Save.**</span></span>

<span data-ttu-id="b1f8b-208">Rozpoczyna się wstępnej synchronizacji użytkowników i/lub grupy przypisane do usługi Google Apps w sekcji Użytkownicy i grupy.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-208">It starts the initial synchronization of any users and/or groups assigned to Google Apps in the Users and Groups section.</span></span> <span data-ttu-id="b1f8b-209">Synchronizacji początkowej zajmuje więcej czasu wykonywania niż kolejne synchronizacje, występujące co około 20 minut, tak długo, jak usługa jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-209">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="b1f8b-210">Można użyć **szczegóły synchronizacji** sekcji, aby monitorować postęp i skorzystaj z linków do inicjowania obsługi administracyjnej raporty działania, które opisują wszystkie akcje wykonywane przez usługę inicjowania obsługi administracyjnej na aplikację usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="b1f8b-210">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b1f8b-211">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b1f8b-211">Additional resources</span></span>

* [<span data-ttu-id="b1f8b-212">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="b1f8b-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b1f8b-213">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b1f8b-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="b1f8b-214">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b1f8b-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



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