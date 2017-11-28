---
title: 'Samouczek: Integracji Azure Active Directory z Jive | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 957b152fdd40d08a867e788b0cb9f7d57ed481e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="a4330-103">Samouczek: Konfigurowanie Jive Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="a4330-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="a4330-104">Celem tego samouczka jest opisano czynności, które należy wykonać w Jive i Azure AD można automatycznie udostępnić i usuwanie kont użytkowników z usługi Azure AD do Jive.</span><span class="sxs-lookup"><span data-stu-id="a4330-104">The objective of this tutorial is to show you the steps you need to perform in Jive and Azure AD to automatically provision and de-provision user accounts from Azure AD to Jive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4330-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a4330-105">Prerequisites</span></span>

<span data-ttu-id="a4330-106">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a4330-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="a4330-107">Dzierżawy usługi Azure Active directory.</span><span class="sxs-lookup"><span data-stu-id="a4330-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="a4330-108">Jive jednokrotnego włączone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="a4330-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="a4330-109">Konto użytkownika w Jive z uprawnieniami administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="a4330-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-to-jive"></a><span data-ttu-id="a4330-110">Przypisywanie użytkowników do Jive</span><span class="sxs-lookup"><span data-stu-id="a4330-110">Assigning users to Jive</span></span>

<span data-ttu-id="a4330-111">Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4330-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="a4330-112">W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="a4330-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="a4330-113">Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, należy zdecydować, jakie użytkownicy i/lub grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do aplikacji Jive.</span><span class="sxs-lookup"><span data-stu-id="a4330-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Jive app.</span></span> <span data-ttu-id="a4330-114">Po decyzję, postępując zgodnie z instrukcjami w tym miejscu można przypisać tych użytkowników do aplikacji Jive:</span><span class="sxs-lookup"><span data-stu-id="a4330-114">Once decided, you can assign these users to your Jive app by following the instructions here:</span></span>

[<span data-ttu-id="a4330-115">Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie</span><span class="sxs-lookup"><span data-stu-id="a4330-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-jive"></a><span data-ttu-id="a4330-116">Ważne porady dotyczące przypisywania użytkowników do Jive</span><span class="sxs-lookup"><span data-stu-id="a4330-116">Important tips for assigning users to Jive</span></span>

*   <span data-ttu-id="a4330-117">Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać do Jive do testowania konfiguracji inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="a4330-117">It is recommended that a single Azure AD user be assigned to Jive to test the provisioning configuration.</span></span> <span data-ttu-id="a4330-118">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="a4330-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="a4330-119">Przypisanie użytkownika do Jive, musisz wybrać poprawnej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a4330-119">When assigning a user to Jive, you must select a valid user role.</span></span> <span data-ttu-id="a4330-120">Rola "Domyślnego dostępu" nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="a4330-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="a4330-121">Włącz inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="a4330-121">Enable User Provisioning</span></span>

<span data-ttu-id="a4330-122">Ta sekcja przeprowadzi Cię przez łączenie usługi Azure AD z konta użytkownika w Jive inicjowania obsługi interfejsu API i konfigurowanie inicjowania obsługi usługi do tworzenia, aktualizacji i wyłączania konta użytkowników przypisane w Jive w oparciu o przypisania użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4330-122">This section guides you through connecting your Azure AD to Jive's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="a4330-123">Można też włączyć na języku SAML rejestracji jednokrotnej dla Jive, wykonując instrukcje podane w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a4330-123">You may also choose to enabled SAML-based Single Sign-On for Jive, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a4330-124">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="a4330-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="a4330-125">Aby skonfigurować, inicjowanie obsługi konta użytkownika:</span><span class="sxs-lookup"><span data-stu-id="a4330-125">To configure user account provisioning:</span></span>

<span data-ttu-id="a4330-126">Celem tej sekcji jest przedstawiają sposób włączania kont użytkowników usługi Active Directory do Jive Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a4330-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Jive.</span></span>
<span data-ttu-id="a4330-127">W ramach tej procedury możesz są wymagane do potrzebnych do żądania od Jive.com token zabezpieczeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a4330-127">As part of this procedure, you are required to provide a user security token you need to request from Jive.com.</span></span>

1. <span data-ttu-id="a4330-128">W [portalu Azure](https://portal.azure.com), przejdź do **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a4330-128">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="a4330-129">Jeśli Jive został już skonfigurowany dla logowania jednokrotnego, wyszukiwanie wystąpieniem Jive przy użyciu pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="a4330-129">If you have already configured Jive for single sign-on, search for your instance of Jive using the search field.</span></span> <span data-ttu-id="a4330-130">W przeciwnym razie wybierz **Dodaj** i wyszukaj **Jive** w galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4330-130">Otherwise, select **Add** and search for **Jive** in the application gallery.</span></span> <span data-ttu-id="a4330-131">Wybierz Jive w wynikach wyszukiwania, a następnie dodaj go do listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4330-131">Select Jive from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="a4330-132">Wybierz wystąpienia programu Jive, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="a4330-132">Select your instance of Jive, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="a4330-133">Ustaw **tryb obsługi administracyjnej** do **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="a4330-133">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="a4330-135">W obszarze **poświadczeń administratora** sekcji, skonfiguruj następujące ustawienia konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="a4330-135">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="a4330-136">a.</span><span class="sxs-lookup"><span data-stu-id="a4330-136">a.</span></span> <span data-ttu-id="a4330-137">W **nazwa użytkownika administratora Jive** pole tekstowe, typ, nazwa, która ma konta Jive **Administrator systemu** profil Jive.com przypisane.</span><span class="sxs-lookup"><span data-stu-id="a4330-137">In the **Jive Admin User Name** textbox, type a Jive account name that has the **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="a4330-138">b.</span><span class="sxs-lookup"><span data-stu-id="a4330-138">b.</span></span> <span data-ttu-id="a4330-139">W **hasło administratora Jive** tekstowym, wpisz hasło dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="a4330-139">In the **Jive Admin Password** textbox, type the password for this account.</span></span>
   
    <span data-ttu-id="a4330-140">c.</span><span class="sxs-lookup"><span data-stu-id="a4330-140">c.</span></span> <span data-ttu-id="a4330-141">W **adres URL dzierżawy Jive** tekstowym, wpisz adres URL dzierżawy Jive.</span><span class="sxs-lookup"><span data-stu-id="a4330-141">In the **Jive Tenant URL** textbox, type the Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="a4330-142">Adres URL dzierżawy Jive jest adres URL, który jest używany przez organizację do logowania do Jive.</span><span class="sxs-lookup"><span data-stu-id="a4330-142">The Jive tenant URL is URL that is used by your organization to log in to Jive.</span></span>  
      > <span data-ttu-id="a4330-143">Zwykle adres URL ma następujący format: **www.\< Organizacja\>. jive.com**.</span><span class="sxs-lookup"><span data-stu-id="a4330-143">Typically, the URL has the following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="a4330-144">W portalu Azure kliknij **Testuj połączenie** zapewniające usługi Azure AD mogą łączyć się z aplikacji Jive.</span><span class="sxs-lookup"><span data-stu-id="a4330-144">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Jive app.</span></span>

7. <span data-ttu-id="a4330-145">Wprowadź adres e-mail osoby lub grupy, który powinien zostać wyświetlony inicjowania obsługi administracyjnej powiadomienia o błędach w **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru poniżej.</span><span class="sxs-lookup"><span data-stu-id="a4330-145">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

8. <span data-ttu-id="a4330-146">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="a4330-146">Click **Save.**</span></span>

9. <span data-ttu-id="a4330-147">W sekcji mapowania wybierz **synchronizacji Azure Active Directory użytkownikom Jive.**</span><span class="sxs-lookup"><span data-stu-id="a4330-147">Under the Mappings section, select **Synchronize Azure Active Directory Users to Jive.**</span></span>

10. <span data-ttu-id="a4330-148">W **mapowań atrybutów** Przejrzyj atrybutów użytkowników, które są synchronizowane z usługi Azure AD Jive.</span><span class="sxs-lookup"><span data-stu-id="a4330-148">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Jive.</span></span> <span data-ttu-id="a4330-149">Atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania kont użytkowników w Jive dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="a4330-149">The attributes selected as **Matching** properties are used to match the user accounts in Jive for update operations.</span></span> <span data-ttu-id="a4330-150">Wybierz przycisk Zapisz, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="a4330-150">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="a4330-151">Aby włączyć usługi Azure AD usługi dla Jive inicjowania obsługi administracyjnej, zmień **stan inicjowania obsługi administracyjnej** do **na** w sekcji Ustawienia</span><span class="sxs-lookup"><span data-stu-id="a4330-151">To enable the Azure AD provisioning service for Jive, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="a4330-152">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="a4330-152">Click **Save.**</span></span>

<span data-ttu-id="a4330-153">Rozpoczyna się wstępnej synchronizacji użytkowników i/lub grupy przypisane do Jive w sekcji Użytkownicy i grupy.</span><span class="sxs-lookup"><span data-stu-id="a4330-153">It starts the initial synchronization of any users and/or groups assigned to Jive in the Users and Groups section.</span></span> <span data-ttu-id="a4330-154">Synchronizacji początkowej zajmuje więcej czasu wykonywania niż kolejne synchronizacje, występujące co około 20 minut, tak długo, jak usługa jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="a4330-154">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="a4330-155">Można użyć **szczegóły synchronizacji** sekcji, aby monitorować postęp i skorzystaj z linków do inicjowania obsługi administracyjnej raporty działania, które opisują wszystkie akcje wykonywane przez usługę inicjowania obsługi administracyjnej na Jive aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4330-155">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Jive app.</span></span>

<span data-ttu-id="a4330-156">Można teraz utworzyć konta testowego.</span><span class="sxs-lookup"><span data-stu-id="a4330-156">You can now create a test account.</span></span> <span data-ttu-id="a4330-157">Aby sprawdzić, czy konto zostało zsynchronizowane z Jive poczekaj maksymalnie 20 minut.</span><span class="sxs-lookup"><span data-stu-id="a4330-157">Wait for up to 20 minutes to verify that the account has been synchronized to Jive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a4330-158">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a4330-158">Additional resources</span></span>

* [<span data-ttu-id="a4330-159">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="a4330-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a4330-160">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a4330-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a4330-161">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a4330-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)