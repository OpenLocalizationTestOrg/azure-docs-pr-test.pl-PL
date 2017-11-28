---
title: "Samouczek: Konfigurowanie ThousandEyes dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować usługi Azure Active Directory, aby automatycznie zapewnianie i usuwanie kont użytkowników do ThousandEyes."
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
ms.openlocfilehash: e6bc2eab3cc1adcf26857ed98d920177a51455ea
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a><span data-ttu-id="a42d8-103">Samouczek: Konfigurowanie ThousandEyes dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="a42d8-103">Tutorial: Configuring ThousandEyes for Automatic User Provisioning</span></span>


<span data-ttu-id="a42d8-104">Celem tego samouczka jest opisano czynności, które należy wykonać w ThousandEyes i Azure AD, aby automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="a42d8-104">The objective of this tutorial is to show you the steps you need to perform in ThousandEyes and Azure AD to automatically provision and de-provision user accounts from Azure AD to ThousandEyes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a42d8-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a42d8-105">Prerequisites</span></span>

<span data-ttu-id="a42d8-106">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a42d8-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="a42d8-107">Dzierżawy usługi Azure Active directory</span><span class="sxs-lookup"><span data-stu-id="a42d8-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="a42d8-108">Dzierżawcy ThousandEyes z [planu Standard](https://www.thousandeyes.com/pricing) lub lepiej jest włączone</span><span class="sxs-lookup"><span data-stu-id="a42d8-108">A ThousandEyes tenant with the [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="a42d8-109">Konto użytkownika z uprawnieniami administratora w ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="a42d8-109">A user account in ThousandEyes with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="a42d8-110">Zależy od usługi Azure AD, inicjowania obsługi administracyjnej integracji [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), który jest dostępny dla zespołów ThousandEyes w planie Standard lub większą.</span><span class="sxs-lookup"><span data-stu-id="a42d8-110">The Azure AD provisioning integration relies on the [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available to ThousandEyes teams on the Standard plan or better.</span></span>

## <a name="assigning-users-to-thousandeyes"></a><span data-ttu-id="a42d8-111">Przypisywanie użytkowników do ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="a42d8-111">Assigning users to ThousandEyes</span></span>

<span data-ttu-id="a42d8-112">Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a42d8-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="a42d8-113">W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="a42d8-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="a42d8-114">Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, należy zdecydować, jakie użytkownicy i/lub grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do aplikacji ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="a42d8-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your ThousandEyes app.</span></span> <span data-ttu-id="a42d8-115">Po decyzję, postępując zgodnie z instrukcjami w tym miejscu można przypisać tych użytkowników do aplikacji ThousandEyes:</span><span class="sxs-lookup"><span data-stu-id="a42d8-115">Once decided, you can assign these users to your ThousandEyes app by following the instructions here:</span></span>

[<span data-ttu-id="a42d8-116">Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie</span><span class="sxs-lookup"><span data-stu-id="a42d8-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-thousandeyes"></a><span data-ttu-id="a42d8-117">Ważne porady dotyczące przypisywania użytkowników do ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="a42d8-117">Important tips for assigning users to ThousandEyes</span></span>

*   <span data-ttu-id="a42d8-118">Zalecane jest jeden jest przypisany użytkownik usługi Azure AD ThousandEyes do testowania konfiguracji inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="a42d8-118">It is recommended that a single Azure AD user is assigned to ThousandEyes to test the provisioning configuration.</span></span> <span data-ttu-id="a42d8-119">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="a42d8-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="a42d8-120">Przypisanie użytkownika do ThousandEyes, należy wybrać opcję **użytkownika** rola, lub inny prawidłowy specyficzne dla aplikacji (jeśli jest dostępny) w oknie dialogowym przypisania.</span><span class="sxs-lookup"><span data-stu-id="a42d8-120">When assigning a user to ThousandEyes, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="a42d8-121">**Domyślnego dostępu** roli nie działa w przypadku inicjowania obsługi administracyjnej, a użytkownicy są pomijane.</span><span class="sxs-lookup"><span data-stu-id="a42d8-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-thousandeyes"></a><span data-ttu-id="a42d8-122">Konfigurowanie inicjowania obsługi administracyjnej ThousandEyes użytkownika</span><span class="sxs-lookup"><span data-stu-id="a42d8-122">Configuring user provisioning to ThousandEyes</span></span> 

<span data-ttu-id="a42d8-123">Ta sekcja przeprowadzi Cię przez łączenie usługi Azure AD z konta użytkownika w ThousandEyes inicjowania obsługi interfejsu API i konfigurowanie inicjowania obsługi usługi do tworzenia, aktualizacji i wyłączania konta użytkowników przypisane w ThousandEyes w oparciu o przypisania użytkowników i grup w usłudze Azure AD .</span><span class="sxs-lookup"><span data-stu-id="a42d8-123">This section guides you through connecting your Azure AD to ThousandEyes's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="a42d8-124">Można też włączyć na języku SAML logowania jednokrotnego dla ThousandEyes, wykonując instrukcje podane w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a42d8-124">You may also choose to enabled SAML-based Single Sign-On for ThousandEyes, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a42d8-125">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="a42d8-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-thousandeyes-in-azure-ad"></a><span data-ttu-id="a42d8-126">Skonfiguruj użytkownika automatyczne Inicjowanie obsługi konta do ThousandEyes w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="a42d8-126">Configure automatic user account provisioning to ThousandEyes in Azure AD</span></span>


1. <span data-ttu-id="a42d8-127">W [portalu Azure](https://portal.azure.com), przejdź do **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a42d8-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="a42d8-128">Jeśli ThousandEyes został już skonfigurowany dla logowania jednokrotnego, wyszukiwanie wystąpieniem ThousandEyes przy użyciu pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="a42d8-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using the search field.</span></span> <span data-ttu-id="a42d8-129">W przeciwnym razie wybierz **Dodaj** i wyszukaj **ThousandEyes** w galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a42d8-129">Otherwise, select **Add** and search for **ThousandEyes** in the application gallery.</span></span> <span data-ttu-id="a42d8-130">Wybierz ThousandEyes w wynikach wyszukiwania, a następnie dodaj go do listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a42d8-130">Select ThousandEyes from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="a42d8-131">Wybierz wystąpienia programu ThousandEyes, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="a42d8-131">Select your instance of ThousandEyes, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="a42d8-132">Ustaw **tryb obsługi administracyjnej** do **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="a42d8-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![ThousandEyes inicjowania obsługi administracyjnej](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. <span data-ttu-id="a42d8-134">W obszarze **poświadczeń administratora** sekcji wejściowych **klucz tajny tokenu** generowane przez konto użytkownika ThousandEyes (token znajduje się na koncie ThousandEyes: **zabezpieczeń & Uwierzytelnianie**).</span><span class="sxs-lookup"><span data-stu-id="a42d8-134">Under the **Admin Credentials** section, input the **Secret Token** generated by your ThousandEyes's account (you can find the token under your ThousandEyes account: **Security & Authentication**).</span></span> 

    ![ThousandEyes inicjowania obsługi administracyjnej](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. <span data-ttu-id="a42d8-136">W portalu Azure kliknij **Testuj połączenie** zapewniające usługi Azure AD mogą łączyć się z aplikacji ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="a42d8-136">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your ThousandEyes app.</span></span> <span data-ttu-id="a42d8-137">Jeśli połączenie nie powiedzie się, upewnij się, że Twoje konto ThousandEyes ma uprawnienia administratora i spróbuj ponownie wykonać krok 5.</span><span class="sxs-lookup"><span data-stu-id="a42d8-137">If the connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="a42d8-138">Wprowadź adres e-mail osoby lub grupy, który powinien zostać wyświetlony inicjowania obsługi administracyjnej powiadomienia o błędach w **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru "Wyślij wiadomość e-mail z powiadomieniem, gdy wystąpi błąd".</span><span class="sxs-lookup"><span data-stu-id="a42d8-138">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="a42d8-139">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a42d8-139">Click **Save**.</span></span> 

9. <span data-ttu-id="a42d8-140">W sekcji mapowania wybierz **synchronizacji Azure Active Directory użytkownikom ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="a42d8-140">Under the Mappings section, select **Synchronize Azure Active Directory Users to ThousandEyes**.</span></span>

10. <span data-ttu-id="a42d8-141">W **mapowań atrybutów** Przejrzyj atrybutów użytkowników, które są synchronizowane z usługi Azure AD ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="a42d8-141">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to ThousandEyes.</span></span> <span data-ttu-id="a42d8-142">Atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania kont użytkowników w ThousandEyes dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="a42d8-142">The attributes selected as **Matching** properties are used to match the user accounts in ThousandEyes for update operations.</span></span> <span data-ttu-id="a42d8-143">Wybierz przycisk Zapisz, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="a42d8-143">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="a42d8-144">Aby włączyć usługi Azure AD usługi dla ThousandEyes inicjowania obsługi administracyjnej, zmień **stan inicjowania obsługi administracyjnej** do **na** w **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="a42d8-144">To enable the Azure AD provisioning service for ThousandEyes, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="a42d8-145">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a42d8-145">Click **Save**.</span></span> 

<span data-ttu-id="a42d8-146">Ta operacja uruchamia wstępnej synchronizacji użytkowników i/lub grupy przypisane do ThousandEyes w sekcji Użytkownicy i grupy.</span><span class="sxs-lookup"><span data-stu-id="a42d8-146">This operation starts the initial synchronization of any users and/or groups assigned to ThousandEyes in the Users and Groups section.</span></span> <span data-ttu-id="a42d8-147">Synchronizacji początkowej zajmuje więcej czasu wykonywania niż kolejne synchronizacje, występujące co około 20 minut, tak długo, jak usługa jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="a42d8-147">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="a42d8-148">Można użyć **szczegóły synchronizacji** sekcji, aby monitorować postęp i skorzystaj z linków do inicjowania obsługi administracyjnej raporty działania, które opisują wszystkie akcje wykonywane przez usługę inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="a42d8-148">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="a42d8-149">Aby uzyskać więcej informacji na temat usługi Azure AD, inicjowanie obsługi dzienników do odczytu, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="a42d8-149">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="a42d8-150">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a42d8-150">Additional resources</span></span>

* [<span data-ttu-id="a42d8-151">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="a42d8-151">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="a42d8-152">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a42d8-152">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="a42d8-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a42d8-153">Next steps</span></span>

* [<span data-ttu-id="a42d8-154">Dowiedz się, jak należy przejrzeć dzienniki i Uzyskaj raporty dotyczące inicjowania obsługi administracyjnej działania</span><span class="sxs-lookup"><span data-stu-id="a42d8-154">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
