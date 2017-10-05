---
title: 'Samouczek: Integracji Azure Active Directory z DocuSign | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 294cd6b8-74d7-44bc-92bc-020ccd13ff12
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 3b509ffa934949200277ae431761d2accd4a02d6
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-docusign-for-user-provisioning"></a><span data-ttu-id="f2fe8-103">Samouczek: Konfigurowanie DocuSign Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="f2fe8-103">Tutorial: Configuring DocuSign for User Provisioning</span></span>

<span data-ttu-id="f2fe8-104">Celem tego samouczka jest opisano czynności, które należy wykonać w DocuSign i Azure AD, aby automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD DocuSign.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-104">The objective of this tutorial is to show you the steps you need to perform in DocuSign and Azure AD to automatically provision and de-provision user accounts from Azure AD to DocuSign.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2fe8-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f2fe8-105">Prerequisites</span></span>

<span data-ttu-id="f2fe8-106">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f2fe8-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="f2fe8-107">Dzierżawy usługi Azure Active directory.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="f2fe8-108">DocuSign logowanie jednokrotne włączone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-108">A DocuSign single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="f2fe8-109">Konto użytkownika w DocuSign z uprawnieniami administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-109">A user account in DocuSign with Team Admin permissions.</span></span>

## <a name="assigning-users-to-docusign"></a><span data-ttu-id="f2fe8-110">Przypisywanie użytkowników do DocuSign</span><span class="sxs-lookup"><span data-stu-id="f2fe8-110">Assigning users to DocuSign</span></span>

<span data-ttu-id="f2fe8-111">Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="f2fe8-112">W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD są synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="f2fe8-113">Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, należy zdecydować, jakie użytkownicy i/lub grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do aplikacji DocuSign.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your DocuSign app.</span></span> <span data-ttu-id="f2fe8-114">Po decyzję, postępując zgodnie z instrukcjami w tym miejscu można przypisać tych użytkowników do aplikacji DocuSign:</span><span class="sxs-lookup"><span data-stu-id="f2fe8-114">Once decided, you can assign these users to your DocuSign app by following the instructions here:</span></span>

[<span data-ttu-id="f2fe8-115">Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie</span><span class="sxs-lookup"><span data-stu-id="f2fe8-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-docusign"></a><span data-ttu-id="f2fe8-116">Ważne porady dotyczące przypisywania użytkowników do DocuSign</span><span class="sxs-lookup"><span data-stu-id="f2fe8-116">Important tips for assigning users to DocuSign</span></span>

*   <span data-ttu-id="f2fe8-117">Zalecane jest jeden jest przypisany użytkownik usługi Azure AD DocuSign do testowania konfiguracji inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-117">It is recommended that a single Azure AD user is assigned to DocuSign to test the provisioning configuration.</span></span> <span data-ttu-id="f2fe8-118">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="f2fe8-119">Przypisanie użytkownika do DocuSign, musisz wybrać poprawnej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-119">When assigning a user to DocuSign, you must select a valid user role.</span></span> <span data-ttu-id="f2fe8-120">Rola "Domyślnego dostępu" nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="f2fe8-121">Włącz inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="f2fe8-121">Enable User Provisioning</span></span>

<span data-ttu-id="f2fe8-122">Ta sekcja przeprowadzi Cię przez łączenie usługi Azure AD z konta użytkownika w DocuSign inicjowania obsługi interfejsu API i konfigurowanie inicjowania obsługi usługi do tworzenia, aktualizacji i wyłączania konta użytkowników przypisane w DocuSign w oparciu o przypisania użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-122">This section guides you through connecting your Azure AD to DocuSign's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in DocuSign based on user and group assignment in Azure AD.</span></span>

> [!Tip]
> <span data-ttu-id="f2fe8-123">Można też włączyć na języku SAML logowania jednokrotnego dla DocuSign, wykonując instrukcje podane w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f2fe8-123">You may also choose to enabled SAML-based Single Sign-On for DocuSign, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f2fe8-124">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="f2fe8-125">Aby skonfigurować, inicjowanie obsługi konta użytkownika:</span><span class="sxs-lookup"><span data-stu-id="f2fe8-125">To configure user account provisioning:</span></span>

<span data-ttu-id="f2fe8-126">Celem tej sekcji jest przedstawiają sposób włączania kont użytkowników usługi Active Directory do DocuSign Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to DocuSign.</span></span>

1. <span data-ttu-id="f2fe8-127">W [portalu Azure](https://portal.azure.com), przejdź do **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="f2fe8-128">Jeśli DocuSign został już skonfigurowany dla logowania jednokrotnego, wyszukiwanie wystąpieniem DocuSign przy użyciu pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-128">If you have already configured DocuSign for single sign-on, search for your instance of DocuSign using the search field.</span></span> <span data-ttu-id="f2fe8-129">W przeciwnym razie wybierz **Dodaj** i wyszukaj **DocuSign** w galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-129">Otherwise, select **Add** and search for **DocuSign** in the application gallery.</span></span> <span data-ttu-id="f2fe8-130">Wybierz DocuSign w wynikach wyszukiwania, a następnie dodaj go do listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-130">Select DocuSign from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="f2fe8-131">Wybierz wystąpienia programu DocuSign, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-131">Select your instance of DocuSign, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="f2fe8-132">Ustaw **tryb obsługi administracyjnej** do **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-132">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-docusign-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="f2fe8-134">W obszarze **poświadczeń administratora** sekcji, skonfiguruj następujące ustawienia konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="f2fe8-134">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="f2fe8-135">a.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-135">a.</span></span> <span data-ttu-id="f2fe8-136">W **nazwa użytkownika administratora** pole tekstowe, typ, nazwa, która ma konta DocuSign **Administrator systemu** profil DocuSign.com przypisane.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-136">In the **Admin User Name** textbox, type a DocuSign account name that has the **System Administrator** profile in DocuSign.com assigned.</span></span>
   
    <span data-ttu-id="f2fe8-137">b.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-137">b.</span></span> <span data-ttu-id="f2fe8-138">W **hasło administratora** tekstowym, wpisz hasło dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-138">In the **Admin Password** textbox, type the password for this account.</span></span>

6. <span data-ttu-id="f2fe8-139">W portalu Azure kliknij **Testuj połączenie** zapewniające usługi Azure AD mogą łączyć się z aplikacji DocuSign.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-139">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your DocuSign app.</span></span>

7. <span data-ttu-id="f2fe8-140">W **wiadomość E-mail z powiadomieniem** wprowadź adres e-mail osoby lub grupy, który powinien otrzymywać powiadomienia błąd inicjowania obsługi administracyjnej i zaznacz pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-140">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

8. <span data-ttu-id="f2fe8-141">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="f2fe8-141">Click **Save.**</span></span>

9. <span data-ttu-id="f2fe8-142">W sekcji mapowania wybierz **synchronizacji Azure Active Directory użytkownikom DocuSign.**</span><span class="sxs-lookup"><span data-stu-id="f2fe8-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to DocuSign.**</span></span>

10. <span data-ttu-id="f2fe8-143">W **mapowań atrybutów** Przejrzyj atrybutów użytkowników, które są synchronizowane z usługi Azure AD DocuSign.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to DocuSign.</span></span> <span data-ttu-id="f2fe8-144">Atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania kont użytkowników w DocuSign dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-144">The attributes selected as **Matching** properties are used to match the user accounts in DocuSign for update operations.</span></span> <span data-ttu-id="f2fe8-145">Wybierz przycisk Zapisz, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="f2fe8-146">Aby włączyć usługi Azure AD usługi dla DocuSign inicjowania obsługi administracyjnej, zmień **stan inicjowania obsługi administracyjnej** do **na** w sekcji Ustawienia</span><span class="sxs-lookup"><span data-stu-id="f2fe8-146">To enable the Azure AD provisioning service for DocuSign, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="f2fe8-147">Kliknij przycisk **zapisać.**</span><span class="sxs-lookup"><span data-stu-id="f2fe8-147">Click **Save.**</span></span>

<span data-ttu-id="f2fe8-148">Rozpoczyna się wstępnej synchronizacji użytkowników i/lub grupy przypisane do DocuSign w sekcji Użytkownicy i grupy.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-148">It starts the initial synchronization of any users and/or groups assigned to DocuSign in the Users and Groups section.</span></span> <span data-ttu-id="f2fe8-149">Synchronizacji początkowej zajmuje więcej czasu wykonywania niż kolejne synchronizacje, występujące co około 20 minut, tak długo, jak usługa jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="f2fe8-150">Można użyć **szczegóły synchronizacji** sekcji, aby monitorować postęp i skorzystaj z linków do inicjowania obsługi administracyjnej raporty działania, które opisują wszystkie akcje wykonywane przez usługę inicjowania obsługi administracyjnej na DocuSign aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your DocuSign app.</span></span>

<span data-ttu-id="f2fe8-151">Można teraz utworzyć konta testowego.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-151">You can now create a test account.</span></span> <span data-ttu-id="f2fe8-152">Aby sprawdzić, czy konto zostało zsynchronizowane z DocuSign poczekaj maksymalnie 20 minut.</span><span class="sxs-lookup"><span data-stu-id="f2fe8-152">Wait for up to 20 minutes to verify that the account has been synchronized to DocuSign.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f2fe8-153">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f2fe8-153">Additional resources</span></span>

* [<span data-ttu-id="f2fe8-154">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="f2fe8-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f2fe8-155">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f2fe8-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="f2fe8-156">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f2fe8-156">Configure Single Sign-on</span></span>](active-directory-saas-docusign-tutorial.md)