---
title: 'Samouczek: Integracji Azure Active Directory z Concur | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: cd35b6e2dc3171e9cffdb820bbc5b0d45ff58e07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="51616-103">Samouczek: Konfigurowanie cząstkowe do inicjowania obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="51616-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="51616-104">Celem tego samouczka jest opisano czynności, które należy wykonać w Concur i Azure AD, aby automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD Concur.</span><span class="sxs-lookup"><span data-stu-id="51616-104">The objective of this tutorial is to show you the steps you need to perform in Concur and Azure AD to automatically provision and de-provision user accounts from Azure AD to Concur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51616-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="51616-105">Prerequisites</span></span>

<span data-ttu-id="51616-106">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="51616-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="51616-107">Dzierżawy usługi Azure Active directory.</span><span class="sxs-lookup"><span data-stu-id="51616-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="51616-108">Concur logowanie jednokrotne włączone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="51616-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="51616-109">Konto użytkownika w Concur z uprawnieniami administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="51616-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-to-concur"></a><span data-ttu-id="51616-110">Przypisywanie użytkowników do Concur</span><span class="sxs-lookup"><span data-stu-id="51616-110">Assigning users to Concur</span></span>

<span data-ttu-id="51616-111">Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="51616-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="51616-112">W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="51616-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="51616-113">Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, należy zdecydować, jakie użytkownicy i/lub grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do aplikacji Concur.</span><span class="sxs-lookup"><span data-stu-id="51616-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Concur app.</span></span> <span data-ttu-id="51616-114">Po decyzję, postępując zgodnie z instrukcjami w tym miejscu można przypisać tych użytkowników do aplikacji Concur:</span><span class="sxs-lookup"><span data-stu-id="51616-114">Once decided, you can assign these users to your Concur app by following the instructions here:</span></span>

[<span data-ttu-id="51616-115">Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie</span><span class="sxs-lookup"><span data-stu-id="51616-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-concur"></a><span data-ttu-id="51616-116">Ważne porady dotyczące przypisywania użytkowników do Concur</span><span class="sxs-lookup"><span data-stu-id="51616-116">Important tips for assigning users to Concur</span></span>

*   <span data-ttu-id="51616-117">Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać do Concur do testowania konfiguracji inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="51616-117">It is recommended that a single Azure AD user be assigned to Concur to test the provisioning configuration.</span></span> <span data-ttu-id="51616-118">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="51616-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="51616-119">Przypisanie użytkownika do Concur, musisz wybrać poprawnej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="51616-119">When assigning a user to Concur, you must select a valid user role.</span></span> <span data-ttu-id="51616-120">Rola "Domyślnego dostępu" nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="51616-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="51616-121">Włącz inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="51616-121">Enable user provisioning</span></span>

<span data-ttu-id="51616-122">Ta sekcja przeprowadzi Cię przez łączenie usługi Azure AD z konta użytkownika w Concur inicjowania obsługi interfejsu API i konfigurowanie inicjowania obsługi usługi do tworzenia, aktualizacji i wyłączania konta użytkowników przypisane w Concur w oparciu o przypisania użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51616-122">This section guides you through connecting your Azure AD to Concur's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="51616-123">Można też włączyć na języku SAML logowania jednokrotnego dla Concur, wykonując instrukcje podane w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="51616-123">You may also choose to enabled SAML-based Single Sign-On for Concur, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="51616-124">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="51616-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="51616-125">Aby skonfigurować, inicjowanie obsługi konta użytkownika:</span><span class="sxs-lookup"><span data-stu-id="51616-125">To configure user account provisioning:</span></span>

<span data-ttu-id="51616-126">Celem tej sekcji jest przedstawiają sposób włączania obsługi administracyjnej kont użytkowników usługi Active Directory do Concur.</span><span class="sxs-lookup"><span data-stu-id="51616-126">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Concur.</span></span>

<span data-ttu-id="51616-127">Aby włączyć aplikacje w usłudze wydatków, musi być prawidłową konfigurację i korzystania z profilem administrator usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="51616-127">To enable apps in the Expense Service, there has to be proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="51616-128">Nie dodawaj rolę administratora WS istniejącego profilu administratora używanego do T & j funkcji administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="51616-128">Don't add the WS Admin role to your existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="51616-129">Cząstkowe konsultantów lub administrator klienta należy utworzyć różne profilu administratora usługi sieci Web i administrator klienta musi używać tego profilu funkcji administratora usług sieci Web (na przykład włączenie aplikacje).</span><span class="sxs-lookup"><span data-stu-id="51616-129">Concur Consultants or the client administrator must create a distinct Web Service Administrator profile and the Client administrator must use this profile for the Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="51616-130">Te profile muszą być przechowywane oddzielnie od administratora klient codzienne T & E admin profilu (T & E profilu administratora nie powinna mieć rolę WSAdmin przypisane).</span><span class="sxs-lookup"><span data-stu-id="51616-130">These profiles must be kept separate from the client administrator's daily T&E admin profile (the T&E admin profile should not have the WSAdmin role assigned).</span></span>

<span data-ttu-id="51616-131">Podczas tworzenia profilu służący do włączania aplikacji, wprowadź nazwę administratora klienta do pól profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="51616-131">When you create the profile to be used for enabling the app, enter the client administrator's name into the user profile fields.</span></span> <span data-ttu-id="51616-132">W ten sposób własności do tego profilu.</span><span class="sxs-lookup"><span data-stu-id="51616-132">This assigns ownership to the profile.</span></span> <span data-ttu-id="51616-133">Po utworzeniu co najmniej jeden profil, klient musi Zaloguj się za pomocą tego profilu, kliknij "*włączyć*" przycisk aplikacji partnera w menu usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="51616-133">Once one or more profiles is created, the client must log in with this profile to click the "*Enable*" button for a Partner App within the Web Services menu.</span></span>

<span data-ttu-id="51616-134">Z następujących powodów tej akcji nie można wykonać za pomocą profilu używanego do normalnej T & E administracji.</span><span class="sxs-lookup"><span data-stu-id="51616-134">For the following reasons, this action should not be done with the profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="51616-135">Klient musi być elementem kliknie "*tak*" w oknie dialogu, które jest wyświetlane, gdy aplikacja zostanie włączona.</span><span class="sxs-lookup"><span data-stu-id="51616-135">The client has to be the one that clicks "*Yes*" on the dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="51616-136">Kliknij ten przycisk uznaje się, że klient jest gotowa dla aplikacji partnera dostępu do danych, więc możesz lub partnera nie kliknij ten przycisk Tak.</span><span class="sxs-lookup"><span data-stu-id="51616-136">This click acknowledges the client is willing for the Partner application to access their data, so you or the Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="51616-137">Jeśli administrator klienta, która włączyła aplikację za pomocą administratora T & E profilu odchodzi z firmy (co w profilu jest dezaktywowane), włączyć za pomocą profilu nie działać do czasu włączenia aplikacji z innym profilem administratora WS aktywne dla wszystkich aplikacji.</span><span class="sxs-lookup"><span data-stu-id="51616-137">If a client administrator that has enabled an app using the T&E admin profile leaves the company (resulting in the profile being inactivated), any apps enabled using that profile does not function until the app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="51616-138">Jest to, dlaczego są powinien utworzyć różne Admin WS profile.</span><span class="sxs-lookup"><span data-stu-id="51616-138">This is why you are supposed to create distinct WS Admin profiles.</span></span>

* <span data-ttu-id="51616-139">Jeśli administrator odchodzi z firmy, można można zmienić nazwy skojarzone z profilem administratora WS administratorowi zastąpienia, w razie potrzeby bez wpływu na pewno włączonych aplikacji, ponieważ ten profil nie jest konieczne dezaktywowane.</span><span class="sxs-lookup"><span data-stu-id="51616-139">If an administrator leaves the company, the name associated to the WS Admin profile can be changed to the replacement administrator if desired without impacting the enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="51616-140">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="51616-140">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="51616-141">Zaloguj się do Twojego **Concur** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="51616-141">Log on to your **Concur** tenant.</span></span>

2. <span data-ttu-id="51616-142">Z **administracji** menu, wybierz opcję **usług sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="51616-142">From the **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="51616-143">![Dzierżawy Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur dzierżawy")</span><span class="sxs-lookup"><span data-stu-id="51616-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="51616-144">Po lewej stronie z **usług sieci Web** okienku wybierz **Włącz aplikacji partnera**.</span><span class="sxs-lookup"><span data-stu-id="51616-144">On the left side, from the **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="51616-145">![Włączanie aplikacji partnera](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "włączyć partnera aplikacji")</span><span class="sxs-lookup"><span data-stu-id="51616-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="51616-146">Z **Włącz aplikacji** listy, wybierz **usługi Azure Active Directory**, a następnie kliknij przycisk **włączyć**.</span><span class="sxs-lookup"><span data-stu-id="51616-146">From the **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="51616-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="51616-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="51616-148">Kliknij przycisk **tak** zamknąć **potwierdzenie akcji** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="51616-148">Click **Yes** to close the **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="51616-149">![Potwierdzenie akcji](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "potwierdzenie akcji")</span><span class="sxs-lookup"><span data-stu-id="51616-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="51616-150">W [portalu Azure](https://portal.azure.com), przejdź do **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="51616-150">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="51616-151">Jeśli Concur został już skonfigurowany dla logowania jednokrotnego, wyszukiwanie wystąpieniem Concur przy użyciu pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="51616-151">If you have already configured Concur for single sign-on, search for your instance of Concur using the search field.</span></span> <span data-ttu-id="51616-152">W przeciwnym razie wybierz **Dodaj** i wyszukaj **Concur** w galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="51616-152">Otherwise, select **Add** and search for **Concur** in the application gallery.</span></span> <span data-ttu-id="51616-153">Wybierz Concur w wynikach wyszukiwania, a następnie dodaj go do listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="51616-153">Select Concur from the search results, and add it to your list of applications.</span></span>

8. <span data-ttu-id="51616-154">Wybierz wystąpienia programu Concur, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="51616-154">Select your instance of Concur, then select the **Provisioning** tab.</span></span>

9. <span data-ttu-id="51616-155">Ustaw **tryb obsługi administracyjnej** do **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="51616-155">Set the **Provisioning Mode** to **Automatic**.</span></span> 
 
    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="51616-157">W obszarze **poświadczeń administratora** wprowadź **nazwy użytkownika** i **hasło** administratora Concur.</span><span class="sxs-lookup"><span data-stu-id="51616-157">Under the **Admin Credentials** section, enter the **user name** and the **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="51616-158">W portalu Azure kliknij **Testuj połączenie** zapewniające usługi Azure AD mogą łączyć się z aplikacji Concur.</span><span class="sxs-lookup"><span data-stu-id="51616-158">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Concur app.</span></span> <span data-ttu-id="51616-159">Jeśli połączenie nie powiedzie się, upewnij się, że Twoje konto Concur ma uprawnienia administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="51616-159">If the connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="51616-160">Wprowadź adres e-mail osoby lub grupy, który powinien zostać wyświetlony inicjowania obsługi administracyjnej powiadomienia o błędach w **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="51616-160">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

13. <span data-ttu-id="51616-161">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="51616-161">Click **Save.**</span></span>

14. <span data-ttu-id="51616-162">W sekcji mapowania wybierz **synchronizacji Azure Active Directory użytkownikom Concur.**</span><span class="sxs-lookup"><span data-stu-id="51616-162">Under the Mappings section, select **Synchronize Azure Active Directory Users to Concur.**</span></span>

15. <span data-ttu-id="51616-163">W **mapowań atrybutów** Przejrzyj atrybutów użytkowników, które są synchronizowane z usługi Azure AD Concur.</span><span class="sxs-lookup"><span data-stu-id="51616-163">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Concur.</span></span> <span data-ttu-id="51616-164">Atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania kont użytkowników w Concur dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="51616-164">The attributes selected as **Matching** properties are used to match the user accounts in Concur for update operations.</span></span> <span data-ttu-id="51616-165">Wybierz przycisk Zapisz, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="51616-165">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="51616-166">Aby włączyć usługi Azure AD usługi dla Concur inicjowania obsługi administracyjnej, zmień **stan inicjowania obsługi administracyjnej** do **na** w **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="51616-166">To enable the Azure AD provisioning service for Concur, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

17. <span data-ttu-id="51616-167">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="51616-167">Click **Save.**</span></span>

<span data-ttu-id="51616-168">Można teraz utworzyć konta testowego.</span><span class="sxs-lookup"><span data-stu-id="51616-168">You can now create a test account.</span></span> <span data-ttu-id="51616-169">Aby sprawdzić, czy konto zostało zsynchronizowane z Concur poczekaj maksymalnie 20 minut.</span><span class="sxs-lookup"><span data-stu-id="51616-169">Wait for up to 20 minutes to verify that the account has been synchronized to Concur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="51616-170">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="51616-170">Additional resources</span></span>

* [<span data-ttu-id="51616-171">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="51616-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="51616-172">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="51616-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="51616-173">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="51616-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

