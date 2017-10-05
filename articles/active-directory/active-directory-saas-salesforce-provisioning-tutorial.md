---
title: "Samouczek: Integracji Azure Active Directory z usług Salesforce | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a573a7ef79e28c50ae0923849a88f88af40f21be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a><span data-ttu-id="13ee0-103">Samouczek: Konfigurowanie usług Salesforce użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="13ee0-103">Tutorial: Configuring Salesforce for Automatic User Provisioning</span></span>

<span data-ttu-id="13ee0-104">Celem tego samouczka jest Pokaż kroki wymagane do przeprowadzenia w Salesforce i Azure AD, aby automatycznie udostępniać i kont usuwanie użytkowników z usługi Azure AD do usługi Salesforce.</span><span class="sxs-lookup"><span data-stu-id="13ee0-104">The objective of this tutorial is to show the steps required to perform in Salesforce and Azure AD to automatically provision and de-provision user accounts from Azure AD to Salesforce.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13ee0-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="13ee0-105">Prerequisites</span></span>

<span data-ttu-id="13ee0-106">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="13ee0-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="13ee0-107">Dzierżawy usługi Azure Active directory.</span><span class="sxs-lookup"><span data-stu-id="13ee0-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="13ee0-108">Musi mieć prawidłową dzierżawy dla usługi Salesforce w pracy lub Salesforce dla instytucji edukacyjnych.</span><span class="sxs-lookup"><span data-stu-id="13ee0-108">You must have a valid tenant for Salesforce for Work or Salesforce for Education.</span></span> <span data-ttu-id="13ee0-109">Można użyć bezpłatnego konta wersji próbnej dla każdej usługi.</span><span class="sxs-lookup"><span data-stu-id="13ee0-109">You may use a free trial     account for either service.</span></span>
*   <span data-ttu-id="13ee0-110">Konto użytkownika w usłudze Salesforce z uprawnieniami administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="13ee0-110">A user account in Salesforce with Team Admin permissions.</span></span>

## <a name="assigning-users-to-salesforce"></a><span data-ttu-id="13ee0-111">Przypisywanie użytkowników do usługi Salesforce</span><span class="sxs-lookup"><span data-stu-id="13ee0-111">Assigning users to Salesforce</span></span>

<span data-ttu-id="13ee0-112">Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="13ee0-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="13ee0-113">W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="13ee0-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="13ee0-114">Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, należy zdecydować, jakie użytkownicy i/lub grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do aplikacji Salesforce.</span><span class="sxs-lookup"><span data-stu-id="13ee0-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Salesforce app.</span></span> <span data-ttu-id="13ee0-115">Po decyzję, można przypisać tych użytkowników do aplikacji Salesforce, postępując zgodnie z instrukcjami poniżej:</span><span class="sxs-lookup"><span data-stu-id="13ee0-115">Once decided, you can assign these users to your Salesforce app by following the instructions here:</span></span>

[<span data-ttu-id="13ee0-116">Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie</span><span class="sxs-lookup"><span data-stu-id="13ee0-116">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-salesforce"></a><span data-ttu-id="13ee0-117">Ważne porady dotyczące przypisywania użytkowników do usługi Salesforce</span><span class="sxs-lookup"><span data-stu-id="13ee0-117">Important tips for assigning users to Salesforce</span></span>

*   <span data-ttu-id="13ee0-118">Zalecane jest pojedynczego użytkownika usługi Azure AD jest przypisana do usług Salesforce, aby przetestować konfigurację inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="13ee0-118">It is recommended that a single Azure AD user is assigned to Salesforce to test the provisioning configuration.</span></span> <span data-ttu-id="13ee0-119">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="13ee0-119">Additional users and/or groups may be assigned later.</span></span>

*  <span data-ttu-id="13ee0-120">Przypisanie użytkownika do usług Salesforce, musisz wybrać poprawnej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="13ee0-120">When assigning a user to Salesforce, you must select a valid user role.</span></span> <span data-ttu-id="13ee0-121">Rola "Domyślnego dostępu" nie działa w przypadku inicjowania obsługi administracyjnej</span><span class="sxs-lookup"><span data-stu-id="13ee0-121">The "Default Access" role does not work for provisioning</span></span>

    > [!NOTE]
    > <span data-ttu-id="13ee0-122">Ta aplikacja importuje role niestandardowe z Salesforce jako część procesu inicjowania obsługi administracyjnej klienta może chcesz wybrać podczas przypisywania użytkowników</span><span class="sxs-lookup"><span data-stu-id="13ee0-122">This app imports custom roles from Salesforce as part of the provisioning process, which the customer may want to select when assigning users</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="13ee0-123">Włącz automatyczne Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="13ee0-123">Enable Automated User Provisioning</span></span>

<span data-ttu-id="13ee0-124">Ta sekcja przeprowadzi Cię przez łączenie usługi Azure AD z konta użytkownika w Salesforce inicjowania obsługi interfejsu API i konfigurowanie inicjowania obsługi usługi do tworzenia, aktualizacji i wyłączania konta użytkowników przypisane w usłudze Salesforce w oparciu o przypisania użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13ee0-124">This section guides you through connecting your Azure AD to Salesforce's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Salesforce based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="13ee0-125">Można też włączone na języku SAML logowania jednokrotnego dla usług Salesforce, postępując zgodnie z instrukcjami zawarte w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="13ee0-125">You may also choose to enabled SAML-based Single Sign-On for Salesforce, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="13ee0-126">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="13ee0-126">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="13ee0-127">Aby skonfigurować konto użytkownika automatycznego inicjowania obsługi administracyjnej:</span><span class="sxs-lookup"><span data-stu-id="13ee0-127">To configure automatic user account provisioning:</span></span>

<span data-ttu-id="13ee0-128">Celem tej sekcji jest przedstawiają sposób włączania Inicjowanie obsługi użytkowników, kont użytkowników usługi Active Directory do usługi Salesforce.</span><span class="sxs-lookup"><span data-stu-id="13ee0-128">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Salesforce.</span></span>

1. <span data-ttu-id="13ee0-129">W [portalu Azure](https://portal.azure.com), przejdź do **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="13ee0-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="13ee0-130">Usługa Salesforce została już skonfigurowana dla logowania jednokrotnego, wyszukaj wystąpienie usługi Salesforce za pomocą pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="13ee0-130">If you have already configured Salesforce for single sign-on, search for your instance of Salesforce using the search field.</span></span> <span data-ttu-id="13ee0-131">W przeciwnym razie wybierz **Dodaj** i wyszukaj **Salesforce** w galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="13ee0-131">Otherwise, select **Add** and search for **Salesforce** in the application gallery.</span></span> <span data-ttu-id="13ee0-132">Wybierz usługi Salesforce z wyników wyszukiwania i dodaj go do listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="13ee0-132">Select Salesforce from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="13ee0-133">Wybierz wystąpienie usługi Salesforce, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="13ee0-133">Select your instance of Salesforce, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="13ee0-134">Ustaw **tryb obsługi administracyjnej** do **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="13ee0-134">Set the **Provisioning Mode** to **Automatic**.</span></span> 
<span data-ttu-id="13ee0-135">![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span><span class="sxs-lookup"><span data-stu-id="13ee0-135">![provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)</span></span>

5. <span data-ttu-id="13ee0-136">W obszarze **poświadczeń administratora** sekcji, skonfiguruj następujące ustawienia konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="13ee0-136">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="13ee0-137">a.</span><span class="sxs-lookup"><span data-stu-id="13ee0-137">a.</span></span> <span data-ttu-id="13ee0-138">W **nazwa użytkownika administratora** tekstowym, wpisz nazwę, która zawiera konta usług Salesforce **administratorem** profilu w witrynie Salesforce.com przypisane.</span><span class="sxs-lookup"><span data-stu-id="13ee0-138">In the **Admin User Name** textbox, type a Salesforce account name that has the **System Administrator** profile in Salesforce.com assigned.</span></span>
   
    <span data-ttu-id="13ee0-139">b.</span><span class="sxs-lookup"><span data-stu-id="13ee0-139">b.</span></span> <span data-ttu-id="13ee0-140">W **hasło administratora** tekstowym, wpisz hasło dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="13ee0-140">In the **Admin Password** textbox, type the password for this account.</span></span>

6. <span data-ttu-id="13ee0-141">Aby uzyskać token zabezpieczeń usług Salesforce, otwórz nową kartę i zaloguj do tego samego konta administratora usługi Salesforce.</span><span class="sxs-lookup"><span data-stu-id="13ee0-141">To get your Salesforce security token, open a new tab and sign into the same Salesforce admin account.</span></span> <span data-ttu-id="13ee0-142">W prawym górnym rogu strony, kliknij swoją nazwę, a następnie kliknij **Moje ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="13ee0-142">On the top right corner of the page, click your name, and then click **My Settings**.</span></span>

     <span data-ttu-id="13ee0-143">![Włącz inicjowanie obsługi użytkowników](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Włącz inicjowanie obsługi użytkowników")</span><span class="sxs-lookup"><span data-stu-id="13ee0-143">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Enable automatic user provisioning")</span></span>
7. <span data-ttu-id="13ee0-144">W lewym okienku nawigacji, kliknij polecenie **osobistych** rozwiń sekcję powiązane, a następnie kliknij przycisk **zresetować moje tokenu zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="13ee0-144">On the left navigation pane, click **Personal** to expand the related section, and then click **Reset My Security Token**.</span></span>
  
    <span data-ttu-id="13ee0-145">![Włącz inicjowanie obsługi użytkowników](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Włącz inicjowanie obsługi użytkowników")</span><span class="sxs-lookup"><span data-stu-id="13ee0-145">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Enable automatic user provisioning")</span></span>
8. <span data-ttu-id="13ee0-146">Na **zresetować moje tokenu zabezpieczeń** kliknij przycisk **zresetować tokenu zabezpieczeń** przycisku.</span><span class="sxs-lookup"><span data-stu-id="13ee0-146">On the **Reset My Security Token** page, click **Reset Security Token** button.</span></span>

    <span data-ttu-id="13ee0-147">![Włącz inicjowanie obsługi użytkowników](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Włącz inicjowanie obsługi użytkowników")</span><span class="sxs-lookup"><span data-stu-id="13ee0-147">![Enable automatic user provisioning](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Enable automatic user provisioning")</span></span>
9. <span data-ttu-id="13ee0-148">Sprawdź skrzynki odbiorczej poczty e-mail, skojarzone z tym kontem administratora.</span><span class="sxs-lookup"><span data-stu-id="13ee0-148">Check the email inbox associated with this admin account.</span></span> <span data-ttu-id="13ee0-149">Poszukaj wiadomości e-mail z witryny Salesforce.com, który zawiera nowy token zabezpieczający.</span><span class="sxs-lookup"><span data-stu-id="13ee0-149">Look for an email from Salesforce.com that contains the new security token.</span></span>
10. <span data-ttu-id="13ee0-150">Skopiuj token, przejdź do okna usługi Azure AD i wklej ją do **gniazda tokenu** pola.</span><span class="sxs-lookup"><span data-stu-id="13ee0-150">Copy the token, go to your Azure AD window, and paste it into the **Socket Token** field.</span></span>

11. <span data-ttu-id="13ee0-151">W portalu Azure kliknij **Testuj połączenie** zapewniające usługi Azure AD mogą łączyć się z aplikacji Salesforce.</span><span class="sxs-lookup"><span data-stu-id="13ee0-151">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Salesforce app.</span></span>

12. <span data-ttu-id="13ee0-152">W **wiadomość E-mail z powiadomieniem** wprowadź adres e-mail osoby lub grupy, który powinien otrzymywać powiadomienia błąd inicjowania obsługi administracyjnej i zaznacz pole wyboru poniżej.</span><span class="sxs-lookup"><span data-stu-id="13ee0-152">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox below.</span></span>

13. <span data-ttu-id="13ee0-153">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="13ee0-153">Click **Save.**</span></span>  
    
14.  <span data-ttu-id="13ee0-154">W sekcji mapowania wybierz **synchronizacji Azure Active Directory użytkownikom Salesforce.**</span><span class="sxs-lookup"><span data-stu-id="13ee0-154">Under the Mappings section, select **Synchronize Azure Active Directory Users to Salesforce.**</span></span>

15. <span data-ttu-id="13ee0-155">W **mapowań atrybutów** Przejrzyj atrybuty użytkowników, które są synchronizowane z usługi Azure AD do usługi Salesforce.</span><span class="sxs-lookup"><span data-stu-id="13ee0-155">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Salesforce.</span></span> <span data-ttu-id="13ee0-156">Należy pamiętać, że atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania kont użytkowników w usłudze Salesforce dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="13ee0-156">Note that the attributes selected as **Matching** properties are used to match the user accounts in Salesforce for update operations.</span></span> <span data-ttu-id="13ee0-157">Wybierz przycisk Zapisz, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="13ee0-157">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="13ee0-158">Aby włączyć usługi Azure AD, świadczenie usługi dla usług Salesforce, zmień **stan inicjowania obsługi administracyjnej** do **na** w sekcji Ustawienia</span><span class="sxs-lookup"><span data-stu-id="13ee0-158">To enable the Azure AD provisioning service for Salesforce, change the **Provisioning Status** to **On** in the Settings section</span></span>

17. <span data-ttu-id="13ee0-159">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="13ee0-159">Click **Save.**</span></span>

<span data-ttu-id="13ee0-160">Spowoduje to uruchomienie synchronizacji początkowej użytkowników i/lub grupy przypisane do usługi Salesforce w sekcji Użytkownicy i grupy.</span><span class="sxs-lookup"><span data-stu-id="13ee0-160">This starts the initial synchronization of any users and/or groups assigned to Salesforce in the Users and Groups section.</span></span> <span data-ttu-id="13ee0-161">Należy pamiętać, że synchronizacji początkowej dłużej, aby wykonać niż kolejne synchronizacje, występujące co około 20 minut, tak długo, jak usługa jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="13ee0-161">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="13ee0-162">Można użyć **szczegóły synchronizacji** sekcji, aby monitorować postęp i skorzystaj z linków do inicjowania obsługi administracyjnej raporty działania, które opisują wszystkie akcje wykonywane przez usługę inicjowania obsługi administracyjnej w aplikacji Salesforce.</span><span class="sxs-lookup"><span data-stu-id="13ee0-162">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Salesforce app.</span></span>

<span data-ttu-id="13ee0-163">Można teraz utworzyć konta testowego.</span><span class="sxs-lookup"><span data-stu-id="13ee0-163">You can now create a test account.</span></span> <span data-ttu-id="13ee0-164">Poczekaj maksymalnie 20 minut, aby sprawdzić, czy konto zostało zsynchronizowane z usług Salesforce.</span><span class="sxs-lookup"><span data-stu-id="13ee0-164">Wait for up to 20 minutes to verify that the account has been synchronized to Salesforce.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="13ee0-165">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="13ee0-165">Additional resources</span></span>

* [<span data-ttu-id="13ee0-166">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="13ee0-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="13ee0-167">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="13ee0-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="13ee0-168">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="13ee0-168">Configure Single Sign-on</span></span>](active-directory-saas-salesforce-tutorial.md)