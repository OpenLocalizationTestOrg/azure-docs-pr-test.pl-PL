---
title: "Samouczek: Konfigurowanie usługi GitHub dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować usługi Azure Active Directory, aby automatycznie zapewnianie i usuwanie kont użytkowników do usługi GitHub."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: 3cc70273e95dbf4913e7bbcd8a37bd9a52987b60
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a><span data-ttu-id="a2559-103">Samouczek: Konfigurowanie usługi GitHub dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="a2559-103">Tutorial: Configuring GitHub for Automatic User Provisioning</span></span>


<span data-ttu-id="a2559-104">Celem tego samouczka jest opisano czynności, które należy wykonać w witrynie GitHub i usługi Azure AD, aby automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD do usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="a2559-104">The objective of this tutorial is to show you the steps you need to perform in GitHub and Azure AD to automatically provision and de-provision user accounts from Azure AD to GitHub.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a2559-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a2559-105">Prerequisites</span></span>

<span data-ttu-id="a2559-106">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a2559-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="a2559-107">Dzierżawy usługi Azure Active directory</span><span class="sxs-lookup"><span data-stu-id="a2559-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="a2559-108">Dzierżawcy Github z [planu firm](https://help.github.com/articles/organization-billing-plans/#business-plan) lub lepiej jest włączone</span><span class="sxs-lookup"><span data-stu-id="a2559-108">A Github tenant with the [Business plan](https://help.github.com/articles/organization-billing-plans/#business-plan) or better enabled</span></span> 
*   <span data-ttu-id="a2559-109">Konto użytkownika z uprawnieniami administratora w usłudze GitHub</span><span class="sxs-lookup"><span data-stu-id="a2559-109">A user account in GitHub with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="a2559-110">Zależy od usługi Azure AD, inicjowania obsługi administracyjnej integracji [GitHub SCIM API](https://developer.github.com/v3/scim/), który jest dostępny dla zespołów Github dla planu biznesowych lub większą.</span><span class="sxs-lookup"><span data-stu-id="a2559-110">The Azure AD provisioning integration relies on the [GitHub SCIM API](https://developer.github.com/v3/scim/), which is available to Github teams on the Business plan or better.</span></span>

## <a name="assigning-users-to-github"></a><span data-ttu-id="a2559-111">Przypisywanie użytkowników do usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="a2559-111">Assigning users to GitHub</span></span>

<span data-ttu-id="a2559-112">Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a2559-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="a2559-113">W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="a2559-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="a2559-114">Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, należy zdecydować, jakie użytkownicy i/lub grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do aplikacji GitHub.</span><span class="sxs-lookup"><span data-stu-id="a2559-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your GitHub app.</span></span> <span data-ttu-id="a2559-115">Po decyzję, postępując zgodnie z instrukcjami w tym miejscu można przypisać tych użytkowników do aplikacji GitHub:</span><span class="sxs-lookup"><span data-stu-id="a2559-115">Once decided, you can assign these users to your GitHub app by following the instructions here:</span></span>

[<span data-ttu-id="a2559-116">Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie</span><span class="sxs-lookup"><span data-stu-id="a2559-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-github"></a><span data-ttu-id="a2559-117">Ważne porady dotyczące przypisywania użytkowników do usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="a2559-117">Important tips for assigning users to GitHub</span></span>

*   <span data-ttu-id="a2559-118">Zalecane jest pojedynczego użytkownika usługi Azure AD jest przypisana do GitHub, aby przetestować konfigurację inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="a2559-118">It is recommended that a single Azure AD user is assigned to GitHub to test the provisioning configuration.</span></span> <span data-ttu-id="a2559-119">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="a2559-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="a2559-120">Przypisanie użytkownika do witryny GitHub, należy wybrać opcję **użytkownika** rola, lub inny prawidłowy specyficzne dla aplikacji (jeśli jest dostępny) w oknie dialogowym przypisania.</span><span class="sxs-lookup"><span data-stu-id="a2559-120">When assigning a user to GitHub, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="a2559-121">**Domyślnego dostępu** roli nie działa w przypadku inicjowania obsługi administracyjnej, a użytkownicy są pomijane.</span><span class="sxs-lookup"><span data-stu-id="a2559-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-github"></a><span data-ttu-id="a2559-122">Konfigurowanie Inicjowanie obsługi użytkowników do usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="a2559-122">Configuring user provisioning to GitHub</span></span> 

<span data-ttu-id="a2559-123">Ta sekcja przeprowadzi Cię przez łączenie usługi Azure AD z konta użytkownika GitHub inicjowania obsługi interfejsu API i konfigurowanie inicjowania obsługi usługi do tworzenia, aktualizacji i wyłączania konta użytkowników przypisane w usłudze GitHub, w oparciu o przypisania użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2559-123">This section guides you through connecting your Azure AD to GitHub's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in GitHub based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="a2559-124">Można też włączone na języku SAML logowania jednokrotnego dla GitHub, postępując zgodnie z instrukcjami zawarte w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a2559-124">You may also choose to enabled SAML-based Single Sign-On for GitHub, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a2559-125">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="a2559-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-github-in-azure-ad"></a><span data-ttu-id="a2559-126">Skonfiguruj automatyczne konta Inicjowanie obsługi użytkowników do usługi GitHub w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2559-126">Configure automatic user account provisioning to GitHub in Azure AD</span></span>


1. <span data-ttu-id="a2559-127">W [portalu Azure](https://portal.azure.com), przejdź do **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a2559-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="a2559-128">Jeśli skonfigurowano już program GitHub dla logowania jednokrotnego, wyszukaj dla swojego wystąpienia usługi GitHub, za pomocą pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="a2559-128">If you have already configured GitHub for single sign-on, search for your instance of GitHub using the search field.</span></span> <span data-ttu-id="a2559-129">W przeciwnym razie wybierz **Dodaj** i wyszukaj **GitHub** w galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a2559-129">Otherwise, select **Add** and search for **GitHub** in the application gallery.</span></span> <span data-ttu-id="a2559-130">Wybierz GitHub z wyników wyszukiwania, a następnie dodaj go do listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a2559-130">Select GitHub from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="a2559-131">Wybierz wystąpienie usługi GitHub, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="a2559-131">Select your instance of GitHub, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="a2559-132">Ustaw **tryb obsługi administracyjnej** do **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="a2559-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Inicjowanie obsługi usługi GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. <span data-ttu-id="a2559-134">W obszarze **poświadczeń administratora** kliknij **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="a2559-134">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="a2559-135">Ta operacja otwiera okno dialogowe autoryzacji GitHub w nowym oknie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="a2559-135">This operation opens a GitHub authorization dialog in a new browser window.</span></span> 

6. <span data-ttu-id="a2559-136">W nowym oknie Zaloguj się do usługi GitHub przy użyciu konta administratora.</span><span class="sxs-lookup"><span data-stu-id="a2559-136">In the new window, sign into GitHub using your Admin account.</span></span> <span data-ttu-id="a2559-137">W oknie dialogowym autoryzacji wynikowy, wybierz zespół GitHub, który chcesz włączyć udostępnianie, a następnie wybierz **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="a2559-137">In the resulting authorization dialog, select the GitHub team that you want to enable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="a2559-138">Po ukończeniu, wróć do portalu Azure, aby zakończyć konfigurację inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="a2559-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span></span>

    ![Okno dialogowe autoryzacji](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. <span data-ttu-id="a2559-140">W portalu Azure, wprowadź **adres URL dzierżawy** i kliknij przycisk **Testuj połączenie** zapewniające usługi Azure AD mogą łączyć się z aplikacji GitHub.</span><span class="sxs-lookup"><span data-stu-id="a2559-140">In the Azure portal, input **Tenant URL** and click **Test Connection** to ensure Azure AD can connect to your GitHub app.</span></span> <span data-ttu-id="a2559-141">Jeśli połączenie nie powiedzie się, upewnij się, Twoje konto GitHub ma uprawnienia administratora i **adres URl dzierżawy** jest wprowadzona poprawnie, a następnie ponownie spróbuj kroku "Autoryzuj" (może stanowić **adres URL dzierżawy** przez regułę: "https:// API.github.com/scim/v2/Organizations/ + < Organizations_name > ", można znaleźć Twojej organizacji na koncie usługi GitHub: **ustawienia** > **organizacji**).</span><span class="sxs-lookup"><span data-stu-id="a2559-141">If the connection fails, ensure your GitHub account has Admin permissions and **Tenant URl** is inputted correctly, then try the "Authorize" step again (you can constitute **Tenant URL** by rule: "https://api.github.com/scim/v2/organizations/ + <Organizations_name>", you can find your organizations under your GitHub account: **Settings** > **Organizations**).</span></span>

    ![Okno dialogowe autoryzacji](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. <span data-ttu-id="a2559-143">Wprowadź adres e-mail osoby lub grupy, który powinien zostać wyświetlony inicjowania obsługi administracyjnej powiadomienia o błędach w **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru "Wyślij wiadomość e-mail z powiadomieniem, gdy wystąpi błąd".</span><span class="sxs-lookup"><span data-stu-id="a2559-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

9. <span data-ttu-id="a2559-144">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a2559-144">Click **Save**.</span></span> 

10. <span data-ttu-id="a2559-145">W sekcji mapowania wybierz **synchronizacji Azure Active Directory użytkownikom GitHub**.</span><span class="sxs-lookup"><span data-stu-id="a2559-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to GitHub**.</span></span>

11. <span data-ttu-id="a2559-146">W **mapowań atrybutów** Przejrzyj atrybuty użytkowników, które są synchronizowane z usługi Azure AD do usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="a2559-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to GitHub.</span></span> <span data-ttu-id="a2559-147">Atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania kont użytkowników w usłudze GitHub dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="a2559-147">The attributes selected as **Matching** properties are used to match the user accounts in GitHub for update operations.</span></span> <span data-ttu-id="a2559-148">Wybierz przycisk Zapisz, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="a2559-148">Select the Save button to commit any changes.</span></span>

12. <span data-ttu-id="a2559-149">Aby włączyć usługi Azure AD, inicjowania obsługi usługi GitHub, zmień **stan inicjowania obsługi administracyjnej** do **na** w **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="a2559-149">To enable the Azure AD provisioning service for GitHub, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

13. <span data-ttu-id="a2559-150">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a2559-150">Click **Save**.</span></span> 

<span data-ttu-id="a2559-151">Ta operacja uruchamia wstępnej synchronizacji użytkowników i/lub grupy przypisane do usługi GitHub w sekcji Użytkownicy i grupy.</span><span class="sxs-lookup"><span data-stu-id="a2559-151">This operation starts the initial synchronization of any users and/or groups assigned to GitHub in the Users and Groups section.</span></span> <span data-ttu-id="a2559-152">Synchronizacji początkowej zajmuje więcej czasu wykonywania niż kolejne synchronizacje, występujące co około 20 minut, tak długo, jak usługa jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="a2559-152">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="a2559-153">Można użyć **szczegóły synchronizacji** sekcji, aby monitorować postęp i skorzystaj z linków do inicjowania obsługi administracyjnej raporty działania, które opisują wszystkie akcje wykonywane przez usługę inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="a2559-153">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="a2559-154">Aby uzyskać więcej informacji na temat usługi Azure AD, inicjowanie obsługi dzienników do odczytu, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="a2559-154">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a2559-155">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a2559-155">Additional resources</span></span>

* [<span data-ttu-id="a2559-156">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="a2559-156">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="a2559-157">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a2559-157">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="a2559-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a2559-158">Next steps</span></span>

* [<span data-ttu-id="a2559-159">Dowiedz się, jak należy przejrzeć dzienniki i Uzyskaj raporty dotyczące inicjowania obsługi administracyjnej działania</span><span class="sxs-lookup"><span data-stu-id="a2559-159">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
