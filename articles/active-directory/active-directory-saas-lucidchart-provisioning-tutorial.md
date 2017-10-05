---
title: "Samouczek: Konfigurowanie LucidChart dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować usługi Azure Active Directory, aby automatycznie zapewnianie i usuwanie kont użytkowników do LucidChart."
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
ms.openlocfilehash: 1f9344a5e750360e21ed7dc8e3ed013c2c2e1a45
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="b667b-103">Samouczek: Konfigurowanie LucidChart dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="b667b-103">Tutorial: Configuring LucidChart for Automatic User Provisioning</span></span>


<span data-ttu-id="b667b-104">Celem tego samouczka jest opisano czynności, które należy wykonać w LucidChart i Azure AD, aby automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD LucidChart.</span><span class="sxs-lookup"><span data-stu-id="b667b-104">The objective of this tutorial is to show you the steps you need to perform in LucidChart and Azure AD to automatically provision and de-provision user accounts from Azure AD to LucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b667b-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b667b-105">Prerequisites</span></span>

<span data-ttu-id="b667b-106">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b667b-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="b667b-107">Dzierżawy usługi Azure Active directory</span><span class="sxs-lookup"><span data-stu-id="b667b-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="b667b-108">Dzierżawcy LucidChart z [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) lub lepiej jest włączone</span><span class="sxs-lookup"><span data-stu-id="b667b-108">A LucidChart tenant with the [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="b667b-109">Konto użytkownika z uprawnieniami administratora w LucidChart</span><span class="sxs-lookup"><span data-stu-id="b667b-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-to-lucidchart"></a><span data-ttu-id="b667b-110">Przypisywanie użytkowników do LucidChart</span><span class="sxs-lookup"><span data-stu-id="b667b-110">Assigning users to LucidChart</span></span>

<span data-ttu-id="b667b-111">Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b667b-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="b667b-112">W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="b667b-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="b667b-113">Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, należy zdecydować, jakie użytkownicy i/lub grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do aplikacji LucidChart.</span><span class="sxs-lookup"><span data-stu-id="b667b-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your LucidChart app.</span></span> <span data-ttu-id="b667b-114">Po decyzję, postępując zgodnie z instrukcjami w tym miejscu można przypisać tych użytkowników do aplikacji LucidChart:</span><span class="sxs-lookup"><span data-stu-id="b667b-114">Once decided, you can assign these users to your LucidChart app by following the instructions here:</span></span>

[<span data-ttu-id="b667b-115">Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie</span><span class="sxs-lookup"><span data-stu-id="b667b-115">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-lucidchart"></a><span data-ttu-id="b667b-116">Ważne porady dotyczące przypisywania użytkowników do LucidChart</span><span class="sxs-lookup"><span data-stu-id="b667b-116">Important tips for assigning users to LucidChart</span></span>

*   <span data-ttu-id="b667b-117">Zalecane jest jeden jest przypisany użytkownik usługi Azure AD LucidChart do testowania konfiguracji inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="b667b-117">It is recommended that a single Azure AD user is assigned to LucidChart to test the provisioning configuration.</span></span> <span data-ttu-id="b667b-118">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="b667b-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="b667b-119">Przypisanie użytkownika do LucidChart, należy wybrać opcję **użytkownika** rola, lub inny prawidłowy specyficzne dla aplikacji (jeśli jest dostępny) w oknie dialogowym przypisania.</span><span class="sxs-lookup"><span data-stu-id="b667b-119">When assigning a user to LucidChart, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="b667b-120">**Domyślnego dostępu** roli nie działa w przypadku inicjowania obsługi administracyjnej, a użytkownicy są pomijane.</span><span class="sxs-lookup"><span data-stu-id="b667b-120">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-lucidchart"></a><span data-ttu-id="b667b-121">Konfigurowanie inicjowania obsługi administracyjnej LucidChart użytkownika</span><span class="sxs-lookup"><span data-stu-id="b667b-121">Configuring user provisioning to LucidChart</span></span> 

<span data-ttu-id="b667b-122">Ta sekcja przeprowadzi Cię przez łączenie usługi Azure AD z konta użytkownika w LucidChart inicjowania obsługi interfejsu API i konfigurowanie inicjowania obsługi usługi do tworzenia, aktualizacji i wyłączania konta użytkowników przypisane w LucidChart w oparciu o przypisania użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b667b-122">This section guides you through connecting your Azure AD to LucidChart's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="b667b-123">Można też włączyć na języku SAML logowania jednokrotnego dla LucidChart, wykonując instrukcje podane w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b667b-123">You may also choose to enabled SAML-based Single Sign-On for LucidChart, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b667b-124">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="b667b-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-lucidchart-in-azure-ad"></a><span data-ttu-id="b667b-125">Skonfiguruj użytkownika automatyczne Inicjowanie obsługi konta do LucidChart w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="b667b-125">Configure automatic user account provisioning to LucidChart in Azure AD</span></span>


1. <span data-ttu-id="b667b-126">W [portalu Azure](https://portal.azure.com), przejdź do **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="b667b-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="b667b-127">Jeśli LucidChart został już skonfigurowany dla logowania jednokrotnego, wyszukiwanie wystąpieniem LucidChart przy użyciu pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="b667b-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using the search field.</span></span> <span data-ttu-id="b667b-128">W przeciwnym razie wybierz **Dodaj** i wyszukaj **LucidChart** w galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b667b-128">Otherwise, select **Add** and search for **LucidChart** in the application gallery.</span></span> <span data-ttu-id="b667b-129">Wybierz LucidChart w wynikach wyszukiwania, a następnie dodaj go do listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b667b-129">Select LucidChart from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="b667b-130">Wybierz wystąpienia programu LucidChart, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="b667b-130">Select your instance of LucidChart, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="b667b-131">Ustaw **tryb obsługi administracyjnej** do **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="b667b-131">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![LucidChart inicjowania obsługi administracyjnej.](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="b667b-133">W obszarze **poświadczeń administratora** sekcji wejściowych **klucz tajny tokenu** generowane przez konto użytkownika LucidChart (przy użyciu tego konta można znaleźć tokenu: **zespołu**  >  **Integracji aplikacji** > **SCIM**).</span><span class="sxs-lookup"><span data-stu-id="b667b-133">Under the **Admin Credentials** section, input the **Secret Token** generated by your LucidChart's account (you can find the token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![LucidChart inicjowania obsługi administracyjnej.](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="b667b-135">W portalu Azure kliknij **Testuj połączenie** zapewniające usługi Azure AD mogą łączyć się z aplikacji LucidChart.</span><span class="sxs-lookup"><span data-stu-id="b667b-135">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your LucidChart app.</span></span> <span data-ttu-id="b667b-136">Jeśli połączenie nie powiedzie się, upewnij się, że Twoje konto LucidChart ma uprawnienia administratora i spróbuj ponownie wykonać krok 5.</span><span class="sxs-lookup"><span data-stu-id="b667b-136">If the connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="b667b-137">Wprowadź adres e-mail osoby lub grupy, który powinien zostać wyświetlony inicjowania obsługi administracyjnej powiadomienia o błędach w **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru "Wyślij wiadomość e-mail z powiadomieniem, gdy wystąpi błąd".</span><span class="sxs-lookup"><span data-stu-id="b667b-137">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="b667b-138">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="b667b-138">Click **Save**.</span></span> 

9. <span data-ttu-id="b667b-139">W sekcji mapowania wybierz **synchronizacji Azure Active Directory użytkownikom LucidChart**.</span><span class="sxs-lookup"><span data-stu-id="b667b-139">Under the Mappings section, select **Synchronize Azure Active Directory Users to LucidChart**.</span></span>

10. <span data-ttu-id="b667b-140">W **mapowań atrybutów** Przejrzyj atrybutów użytkowników, które są synchronizowane z usługi Azure AD LucidChart.</span><span class="sxs-lookup"><span data-stu-id="b667b-140">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to LucidChart.</span></span> <span data-ttu-id="b667b-141">Atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania kont użytkowników w LucidChart dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="b667b-141">The attributes selected as **Matching** properties are used to match the user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="b667b-142">Wybierz przycisk Zapisz, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="b667b-142">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="b667b-143">Aby włączyć usługi Azure AD usługi dla LucidChart inicjowania obsługi administracyjnej, zmień **stan inicjowania obsługi administracyjnej** do **na** w **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="b667b-143">To enable the Azure AD provisioning service for LucidChart, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="b667b-144">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="b667b-144">Click **Save**.</span></span> 

<span data-ttu-id="b667b-145">Ta operacja uruchamia wstępnej synchronizacji użytkowników i/lub grupy przypisane do LucidChart w sekcji Użytkownicy i grupy.</span><span class="sxs-lookup"><span data-stu-id="b667b-145">This operation starts the initial synchronization of any users and/or groups assigned to LucidChart in the Users and Groups section.</span></span> <span data-ttu-id="b667b-146">Synchronizacji początkowej zajmuje więcej czasu wykonywania niż kolejne synchronizacje, występujące co około 20 minut, tak długo, jak usługa jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="b667b-146">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="b667b-147">Można użyć **szczegóły synchronizacji** sekcji, aby monitorować postęp i skorzystaj z linków do inicjowania obsługi administracyjnej raporty działania, które opisują wszystkie akcje wykonywane przez usługę inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="b667b-147">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="b667b-148">Aby uzyskać więcej informacji na temat usługi Azure AD, inicjowanie obsługi dzienników do odczytu, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="b667b-148">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b667b-149">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b667b-149">Additional resources</span></span>

* [<span data-ttu-id="b667b-150">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="b667b-150">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="b667b-151">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b667b-151">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="b667b-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b667b-152">Next steps</span></span>

* [<span data-ttu-id="b667b-153">Dowiedz się, jak należy przejrzeć dzienniki i Uzyskaj raporty dotyczące inicjowania obsługi administracyjnej działania</span><span class="sxs-lookup"><span data-stu-id="b667b-153">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
