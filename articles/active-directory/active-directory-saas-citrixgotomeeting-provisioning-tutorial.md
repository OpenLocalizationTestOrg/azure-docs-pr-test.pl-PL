---
title: 'Samouczek: Integracji Azure Active Directory z Citrix GoToMeeting | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1ddfcd991431a11e5c3e306bd5905003d094ac18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="89b62-103">Samouczek: Konfigurowanie Citrix GoToMeeting dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="89b62-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="89b62-104">Celem tego samouczka jest opisano czynności, które należy wykonać w Citrix GoToMeeting i Azure AD, aby automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="89b62-104">The objective of this tutorial is to show you the steps you need to perform in Citrix GoToMeeting and Azure AD to automatically provision and de-provision user accounts from Azure AD to Citrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89b62-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="89b62-105">Prerequisites</span></span>

<span data-ttu-id="89b62-106">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="89b62-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="89b62-107">Dzierżawy usługi Azure Active directory.</span><span class="sxs-lookup"><span data-stu-id="89b62-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="89b62-108">Citrix GoToMeeting jednokrotnego włączone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="89b62-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="89b62-109">Konto użytkownika w Citrix GoToMeeting z uprawnieniami administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="89b62-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="89b62-110">Przypisywanie użytkowników do Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="89b62-110">Assigning users to Citrix GoToMeeting</span></span>

<span data-ttu-id="89b62-111">Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="89b62-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="89b62-112">W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="89b62-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="89b62-113">Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, należy zdecydować, jakie użytkownicy i/lub grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do aplikacji Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="89b62-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="89b62-114">Po decyzję, można przypisać tych użytkowników do aplikacji Citrix GoToMeeting, postępując zgodnie z instrukcjami poniżej:</span><span class="sxs-lookup"><span data-stu-id="89b62-114">Once decided, you can assign these users to your Citrix GoToMeeting app by following the instructions here:</span></span>

[<span data-ttu-id="89b62-115">Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie</span><span class="sxs-lookup"><span data-stu-id="89b62-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="89b62-116">Ważne porady dotyczące przypisywania użytkowników do Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="89b62-116">Important tips for assigning users to Citrix GoToMeeting</span></span>

*   <span data-ttu-id="89b62-117">Zalecane jest pojedynczego użytkownika usługi Azure AD jest przypisana do Citrix GoToMeeting, aby przetestować konfigurację inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="89b62-117">It is recommended that a single Azure AD user is assigned to Citrix GoToMeeting to test the provisioning configuration.</span></span> <span data-ttu-id="89b62-118">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="89b62-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="89b62-119">Przypisanie użytkownika do Citrix GoToMeeting, należy wybrać poprawnej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="89b62-119">When assigning a user to Citrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="89b62-120">Rola "Domyślnego dostępu" nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="89b62-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="89b62-121">Włącz automatyczne Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="89b62-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="89b62-122">Ta sekcja przeprowadzi Cię przez łączenie usługi Azure AD z konta użytkownika Citrix GoToMeeting inicjowania obsługi interfejsu API i konfigurowanie inicjowania obsługi usługi do tworzenia, aktualizacji i wyłączania przypisany użytkownik kont w Citrix GoToMeeting opartych na przypisanie użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89b62-122">This section guides you through connecting your Azure AD to Citrix GoToMeeting's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="89b62-123">Można też włączyć na języku SAML logowania jednokrotnego dla Citrix GoToMeeting, wykonując instrukcje podane w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="89b62-123">You may also choose to enabled SAML-based Single Sign-On for Citrix GoToMeeting, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="89b62-124">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="89b62-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="89b62-125">Aby skonfigurować konto użytkownika automatycznego inicjowania obsługi administracyjnej:</span><span class="sxs-lookup"><span data-stu-id="89b62-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="89b62-126">W [portalu Azure](https://portal.azure.com), przejdź do **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="89b62-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="89b62-127">Jeśli Citrix GoToMeeting został już skonfigurowany dla logowania jednokrotnego, wyszukiwanie wystąpieniem Citrix GoToMeeting, korzystając z pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="89b62-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using the search field.</span></span> <span data-ttu-id="89b62-128">W przeciwnym razie wybierz **Dodaj** i wyszukaj **Citrix GoToMeeting** w galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="89b62-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in the application gallery.</span></span> <span data-ttu-id="89b62-129">Wybierz Citrix GoToMeeting w wynikach wyszukiwania i dodaj ją do listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="89b62-129">Select Citrix GoToMeeting from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="89b62-130">Wybierz wystąpienia programu Citrix GoToMeeting, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="89b62-130">Select your instance of Citrix GoToMeeting, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="89b62-131">Ustaw **inicjowania obsługi administracyjnej** tryb **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="89b62-131">Set the **Provisioning** Mode to **Automatic**.</span></span> 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="89b62-133">W sekcji poświadczenia administratora wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="89b62-133">Under the Admin Credentials section, perform the following steps:</span></span>
   
    <span data-ttu-id="89b62-134">a.</span><span class="sxs-lookup"><span data-stu-id="89b62-134">a.</span></span> <span data-ttu-id="89b62-135">W **nazwa użytkownika administratora GoToMeeting Citrix** tekstowym, wpisz nazwę użytkownika administratora.</span><span class="sxs-lookup"><span data-stu-id="89b62-135">In the **Citrix GoToMeeting Admin User Name** textbox, type the user name of an administrator.</span></span>

    <span data-ttu-id="89b62-136">b.</span><span class="sxs-lookup"><span data-stu-id="89b62-136">b.</span></span> <span data-ttu-id="89b62-137">W **hasło administratora GoToMeeting Citrix** pole tekstowe, hasło administratora.</span><span class="sxs-lookup"><span data-stu-id="89b62-137">In the **Citrix GoToMeeting Admin Password** textbox, the administrator's password.</span></span>

6. <span data-ttu-id="89b62-138">W portalu Azure kliknij **Testuj połączenie** zapewniające usługi Azure AD mogą łączyć się z aplikacji Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="89b62-138">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="89b62-139">Jeśli połączenie nie powiedzie się, upewnij się, Twoje konto Citrix GoToMeeting ma uprawnienia administratora zespołu i spróbuj **"Poświadczeń administratora"** krok ponownie.</span><span class="sxs-lookup"><span data-stu-id="89b62-139">If the connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try the **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="89b62-140">Wprowadź adres e-mail osoby lub grupy, który powinien zostać wyświetlony inicjowania obsługi administracyjnej powiadomienia o błędach w **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="89b62-140">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="89b62-141">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="89b62-141">Click **Save.**</span></span>

9. <span data-ttu-id="89b62-142">W sekcji mapowania wybierz **synchronizacji Azure Active Directory użytkownikom Citrix GoToMeeting.**</span><span class="sxs-lookup"><span data-stu-id="89b62-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Citrix GoToMeeting.**</span></span>

10. <span data-ttu-id="89b62-143">W **mapowań atrybutów** Przejrzyj atrybutów użytkowników, które są synchronizowane z usługi Azure AD Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="89b62-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Citrix GoToMeeting.</span></span> <span data-ttu-id="89b62-144">Atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania kont użytkowników w Citrix GoToMeeting dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="89b62-144">The attributes selected as **Matching** properties are used to match the user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="89b62-145">Wybierz przycisk Zapisz, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="89b62-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="89b62-146">Aby włączyć usługi Azure AD, świadczenie usługi dla Citrix GoToMeeting, zmień **stan inicjowania obsługi administracyjnej** do **na** w sekcji Ustawienia</span><span class="sxs-lookup"><span data-stu-id="89b62-146">To enable the Azure AD provisioning service for Citrix GoToMeeting, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="89b62-147">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="89b62-147">Click **Save.**</span></span>

<span data-ttu-id="89b62-148">Rozpoczyna się wstępnej synchronizacji użytkowników i/lub grupy przypisane do Citrix GoToMeeting w sekcji Użytkownicy i grupy.</span><span class="sxs-lookup"><span data-stu-id="89b62-148">It starts the initial synchronization of any users and/or groups assigned to Citrix GoToMeeting in the Users and Groups section.</span></span> <span data-ttu-id="89b62-149">Synchronizacji początkowej zajmuje więcej czasu wykonywania niż kolejne synchronizacje, występujące co około 20 minut, tak długo, jak usługa jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="89b62-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="89b62-150">Można użyć **szczegóły synchronizacji** sekcji, aby monitorować postęp i skorzystaj z linków do inicjowania obsługi administracyjnej raporty działania, które opisują wszystkie akcje wykonywane przez usługę inicjowania obsługi administracyjnej w aplikacji Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="89b62-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="89b62-151">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="89b62-151">Additional resources</span></span>

* [<span data-ttu-id="89b62-152">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="89b62-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89b62-153">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="89b62-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="89b62-154">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="89b62-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


