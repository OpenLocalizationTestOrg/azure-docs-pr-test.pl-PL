---
title: 'Samouczek: Integracji Azure Active Directory z Dropbox dla firm | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i skrzynki dla firm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6f7616e47322242f01a13d763f71c93d4ac06a92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="55c7b-103">Samouczek: Konfigurowanie skrzynki dla firm użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="55c7b-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="55c7b-104">Celem tego samouczka jest opisano czynności, które należy wykonać w Dropbox dla firm i Azure AD automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD do usługi Dropbox dla firm.</span><span class="sxs-lookup"><span data-stu-id="55c7b-104">The objective of this tutorial is to show you the steps you need to perform in Dropbox for Business and Azure AD to automatically provision and de-provision user accounts from Azure AD to Dropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55c7b-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="55c7b-105">Prerequisites</span></span>

<span data-ttu-id="55c7b-106">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="55c7b-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="55c7b-107">Dzierżawy usługi Azure Active directory.</span><span class="sxs-lookup"><span data-stu-id="55c7b-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="55c7b-108">Dropbox dla firm jednokrotnego włączone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="55c7b-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="55c7b-109">Konto użytkownika w Dropbox dla firm z uprawnieniami administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="55c7b-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-to-dropbox-for-business"></a><span data-ttu-id="55c7b-110">Przypisywanie użytkowników do usługi Dropbox dla firm</span><span class="sxs-lookup"><span data-stu-id="55c7b-110">Assigning users to Dropbox for Business</span></span>

<span data-ttu-id="55c7b-111">Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="55c7b-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="55c7b-112">W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="55c7b-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="55c7b-113">Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, należy zdecydować, jakie użytkownicy i/lub grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do Twojej skrzynki dla aplikacji biznesowych.</span><span class="sxs-lookup"><span data-stu-id="55c7b-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Dropbox for Business app.</span></span> <span data-ttu-id="55c7b-114">Po decyzję, można przypisać tych użytkowników do Twojej skrzynki dla aplikacji biznesowych, postępując zgodnie z instrukcjami poniżej:</span><span class="sxs-lookup"><span data-stu-id="55c7b-114">Once decided, you can assign these users to your Dropbox for Business app by following the instructions here:</span></span>

[<span data-ttu-id="55c7b-115">Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie</span><span class="sxs-lookup"><span data-stu-id="55c7b-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-dropbox-for-business"></a><span data-ttu-id="55c7b-116">Ważne porady dotyczące przypisywania użytkowników do usługi Dropbox dla firm</span><span class="sxs-lookup"><span data-stu-id="55c7b-116">Important tips for assigning users to Dropbox for Business</span></span>

*   <span data-ttu-id="55c7b-117">Zalecane jest jeden użytkownik usługi Azure AD jest przypisany do skrzynki dla firm, aby przetestować konfigurację inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="55c7b-117">It is recommended that a single Azure AD user is assigned to Dropbox for Business to test the provisioning configuration.</span></span> <span data-ttu-id="55c7b-118">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="55c7b-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="55c7b-119">Przypisanie użytkownika do skrzynki dla firm, należy wybrać poprawnej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="55c7b-119">When assigning a user to Dropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="55c7b-120">Rola "Domyślnego dostępu" nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="55c7b-120">The "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="55c7b-121">Włącz automatyczne Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="55c7b-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="55c7b-122">Ta sekcja przeprowadzi użytkownika przez nawiązywania połączenia z usługi Azure AD Dropbox dla konta użytkownika firmy inicjowania obsługi interfejsu API i konfigurowanie usługi inicjowania obsługi administracyjnej do tworzenia, aktualizacji i wyłączania konta użytkowników przypisane w Dropbox dla firm, w oparciu o użytkowników i grup przypisania w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55c7b-122">This section guides you through connecting your Azure AD to Dropbox for Business's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="55c7b-123">Można też włączyć na języku SAML logowania jednokrotnego dla skrzynki dla firm, wykonując instrukcje podane w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="55c7b-123">You may also choose to enabled SAML-based Single Sign-On for Dropbox for Business, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="55c7b-124">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="55c7b-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="55c7b-125">Aby skonfigurować konto użytkownika automatycznego inicjowania obsługi administracyjnej:</span><span class="sxs-lookup"><span data-stu-id="55c7b-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="55c7b-126">W [portalu Azure](https://portal.azure.com), przejdź do **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="55c7b-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="55c7b-127">Jeśli skonfigurowano już program Dropbox dla firm dla logowania jednokrotnego, wyszukaj dla swojego wystąpienia usługi Dropbox dla firm przy użyciu pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="55c7b-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using the search field.</span></span> <span data-ttu-id="55c7b-128">W przeciwnym razie wybierz **Dodaj** i wyszukaj **Dropbox dla firm** w galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="55c7b-128">Otherwise, select **Add** and search for **Dropbox for Business** in the application gallery.</span></span> <span data-ttu-id="55c7b-129">Wybierz Dropbox dla firm z wyników wyszukiwania, a następnie dodaj go do listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="55c7b-129">Select Dropbox for Business from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="55c7b-130">Wybierz wystąpienie usługi Dropbox dla firm, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="55c7b-130">Select your instance of Dropbox for Business, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="55c7b-131">Ustaw **tryb obsługi administracyjnej** do **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="55c7b-131">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="55c7b-133">W obszarze **poświadczeń administratora** kliknij **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="55c7b-133">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="55c7b-134">Dropbox dla okna dialogowego logowania biznesowych zostanie otwarty w nowym oknie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="55c7b-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="55c7b-135">Na **logowania do usługi Dropbox, aby połączyć się z usługą Azure AD** okna dialogowego, zalogować się w usłudze Dropbox dla dzierżawy biznesowych.</span><span class="sxs-lookup"><span data-stu-id="55c7b-135">On the **Sign-in to Dropbox to link with Azure AD** dialog, sign in to your Dropbox for Business tenant.</span></span>

     <span data-ttu-id="55c7b-136">![Inicjowanie obsługi użytkowników](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Inicjowanie obsługi użytkowników")</span><span class="sxs-lookup"><span data-stu-id="55c7b-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="55c7b-137">Upewnij się, czy chcesz zezwolić usłudze Azure Active Directory Aby wprowadzić zmiany w usłudze Dropbox dla dzierżawy biznesowych.</span><span class="sxs-lookup"><span data-stu-id="55c7b-137">Confirm that you would like to give Azure Active Directory permission to make changes to your Dropbox for Business tenant.</span></span> <span data-ttu-id="55c7b-138">Kliknij przycisk **Zezwalaj**.</span><span class="sxs-lookup"><span data-stu-id="55c7b-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="55c7b-139">![Inicjowanie obsługi użytkowników](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Inicjowanie obsługi użytkowników")</span><span class="sxs-lookup"><span data-stu-id="55c7b-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="55c7b-140">W portalu Azure kliknij **Testuj połączenie** zapewniające usługi Azure AD mogą łączyć się z Twojej skrzynki dla aplikacji biznesowych.</span><span class="sxs-lookup"><span data-stu-id="55c7b-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Dropbox for Business app.</span></span> <span data-ttu-id="55c7b-141">Jeśli połączenie nie powiedzie się, zapewnić usłudze Dropbox konto firmowe, ma uprawnienia administratora zespołu i spróbuj **"Autoryzuj"** krok ponownie.</span><span class="sxs-lookup"><span data-stu-id="55c7b-141">If the connection fails, ensure your Dropbox for Business account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

9. <span data-ttu-id="55c7b-142">Wprowadź adres e-mail osoby lub grupy, który powinien zostać wyświetlony inicjowania obsługi administracyjnej powiadomienia o błędach w **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="55c7b-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

10. <span data-ttu-id="55c7b-143">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="55c7b-143">Click **Save.**</span></span>

11. <span data-ttu-id="55c7b-144">W sekcji mapowania wybierz **synchronizacji Azure użytkownicy usługi Active Directory do usługi Dropbox dla firm.**</span><span class="sxs-lookup"><span data-stu-id="55c7b-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Dropbox for Business.**</span></span>

12. <span data-ttu-id="55c7b-145">W **mapowań atrybutów** Przejrzyj atrybutów użytkowników, które są synchronizowane z usługi Azure AD Dropbox dla firm.</span><span class="sxs-lookup"><span data-stu-id="55c7b-145">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Dropbox for Business.</span></span> <span data-ttu-id="55c7b-146">Atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania kont użytkowników w Dropbox dla firm dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="55c7b-146">The attributes selected as **Matching** properties are used to match the user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="55c7b-147">Wybierz przycisk Zapisz, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="55c7b-147">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="55c7b-148">Aby włączyć usługi Azure AD, inicjowania obsługi usługi Dropbox dla firm, zmień **stan inicjowania obsługi administracyjnej** do **na** w sekcji Ustawienia</span><span class="sxs-lookup"><span data-stu-id="55c7b-148">To enable the Azure AD provisioning service for Dropbox for Business, change the **Provisioning Status** to **On** in the Settings section</span></span>

14. <span data-ttu-id="55c7b-149">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="55c7b-149">Click **Save.**</span></span>

<span data-ttu-id="55c7b-150">Rozpoczyna się wstępnej synchronizacji użytkowników i/lub grupy przypisane do skrzynki dla firm w sekcji Użytkownicy i grupy.</span><span class="sxs-lookup"><span data-stu-id="55c7b-150">It starts the initial synchronization of any users and/or groups assigned to Dropbox for Business in the Users and Groups section.</span></span> <span data-ttu-id="55c7b-151">Synchronizacji początkowej zajmuje więcej czasu wykonywania niż kolejne synchronizacje, występujące co około 20 minut, tak długo, jak usługa jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="55c7b-151">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="55c7b-152">Można użyć **szczegóły synchronizacji** sekcji, aby monitorować postęp i skorzystaj z linków do inicjowania obsługi administracyjnej raporty działania, które opisują wszystkie akcje wykonywane przez usługę inicjowania obsługi administracyjnej w usłudze Dropbox dla aplikacji biznesowych.</span><span class="sxs-lookup"><span data-stu-id="55c7b-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="55c7b-153">Można teraz utworzyć konta testowego.</span><span class="sxs-lookup"><span data-stu-id="55c7b-153">You can now create a test account.</span></span> <span data-ttu-id="55c7b-154">Poczekaj maksymalnie 20 minut, aby sprawdzić, czy konto zostało zsynchronizowane z Dropbox dla firm.</span><span class="sxs-lookup"><span data-stu-id="55c7b-154">Wait for up to 20 minutes to verify that the account has been synchronized to Dropbox for Business.</span></span>

<span data-ttu-id="55c7b-155">Użytkownik pomyślnie zakończono inicjowanie obsługi cyklu wskazuje stan powiązane.</span><span class="sxs-lookup"><span data-stu-id="55c7b-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="55c7b-156">![Przypisywanie użytkowników](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="55c7b-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="55c7b-157">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="55c7b-157">Additional resources</span></span>

* [<span data-ttu-id="55c7b-158">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="55c7b-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="55c7b-159">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="55c7b-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="55c7b-160">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="55c7b-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)