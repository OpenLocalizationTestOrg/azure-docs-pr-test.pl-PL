---
title: "Samouczek: Konfigurowanie usługi GitHub dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konta tooGitHub tooconfigure usługi Azure Active Directory tooautomatically udostępniania i usuwanie użytkowników."
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
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a><span data-ttu-id="91931-103">Samouczek: Konfigurowanie usługi GitHub dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="91931-103">Tutorial: Configuring GitHub for Automatic User Provisioning</span></span>


<span data-ttu-id="91931-104">Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w GitHub i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooGitHub.</span><span class="sxs-lookup"><span data-stu-id="91931-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in GitHub and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGitHub.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="91931-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="91931-105">Prerequisites</span></span>

<span data-ttu-id="91931-106">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="91931-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="91931-107">Dzierżawy usługi Azure Active directory</span><span class="sxs-lookup"><span data-stu-id="91931-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="91931-108">Dzierżawcy Github z hello [planu firm](https://help.github.com/articles/organization-billing-plans/#business-plan) lub lepiej jest włączone</span><span class="sxs-lookup"><span data-stu-id="91931-108">A Github tenant with hello [Business plan](https://help.github.com/articles/organization-billing-plans/#business-plan) or better enabled</span></span> 
*   <span data-ttu-id="91931-109">Konto użytkownika z uprawnieniami administratora w usłudze GitHub</span><span class="sxs-lookup"><span data-stu-id="91931-109">A user account in GitHub with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="91931-110">Hello Azure AD inicjowania obsługi administracyjnej integracji opiera się na powitania [GitHub SCIM API](https://developer.github.com/v3/scim/), które jest dostępne tooGithub zespoły w planie firm hello lub większą.</span><span class="sxs-lookup"><span data-stu-id="91931-110">hello Azure AD provisioning integration relies on hello [GitHub SCIM API](https://developer.github.com/v3/scim/), which is available tooGithub teams on hello Business plan or better.</span></span>

## <a name="assigning-users-toogithub"></a><span data-ttu-id="91931-111">Przypisywanie użytkowników tooGitHub</span><span class="sxs-lookup"><span data-stu-id="91931-111">Assigning users tooGitHub</span></span>

<span data-ttu-id="91931-112">Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu.</span><span class="sxs-lookup"><span data-stu-id="91931-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="91931-113">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="91931-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="91931-114">Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji GitHub tooyour.</span><span class="sxs-lookup"><span data-stu-id="91931-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour GitHub app.</span></span> <span data-ttu-id="91931-115">Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour GitHub aplikacji:</span><span class="sxs-lookup"><span data-stu-id="91931-115">Once decided, you can assign these users tooyour GitHub app by following hello instructions here:</span></span>

[<span data-ttu-id="91931-116">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="91931-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a><span data-ttu-id="91931-117">Ważne porady dotyczące przypisywania tooGitHub użytkowników</span><span class="sxs-lookup"><span data-stu-id="91931-117">Important tips for assigning users tooGitHub</span></span>

*   <span data-ttu-id="91931-118">Zalecane jest jeden użytkownik usługi Azure AD jest przypisany hello tootest tooGitHub inicjowania obsługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="91931-118">It is recommended that a single Azure AD user is assigned tooGitHub tootest hello provisioning configuration.</span></span> <span data-ttu-id="91931-119">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="91931-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="91931-120">Podczas przypisywania tooGitHub użytkownika, należy wybrać albo hello **użytkownika** rola, lub inny prawidłowy specyficzne dla aplikacji (jeśli jest dostępny) w oknie dialogowym przydział hello.</span><span class="sxs-lookup"><span data-stu-id="91931-120">When assigning a user tooGitHub, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="91931-121">Witaj **domyślnego dostępu** roli nie działa w przypadku inicjowania obsługi administracyjnej, a użytkownicy są pomijane.</span><span class="sxs-lookup"><span data-stu-id="91931-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toogithub"></a><span data-ttu-id="91931-122">Konfigurowanie inicjowania obsługi administracyjnej tooGitHub użytkownika</span><span class="sxs-lookup"><span data-stu-id="91931-122">Configuring user provisioning tooGitHub</span></span> 

<span data-ttu-id="91931-123">Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooGitHub programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w usłudze GitHub, w oparciu o przypisania użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91931-123">This section guides you through connecting your Azure AD tooGitHub's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in GitHub based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="91931-124">Można też tooenabled na języku SAML logowania jednokrotnego dla GitHub hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="91931-124">You may also choose tooenabled SAML-based Single Sign-On for GitHub, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="91931-125">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="91931-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a><span data-ttu-id="91931-126">Skonfiguruj konto użytkownika automatycznego inicjowania obsługi administracyjnej tooGitHub w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="91931-126">Configure automatic user account provisioning tooGitHub in Azure AD</span></span>


1. <span data-ttu-id="91931-127">W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="91931-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="91931-128">Jeśli skonfigurowano już program GitHub dla logowania jednokrotnego, wyszukaj dla swojego wystąpienia usługi GitHub, za pomocą pola wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="91931-128">If you have already configured GitHub for single sign-on, search for your instance of GitHub using hello search field.</span></span> <span data-ttu-id="91931-129">W przeciwnym razie wybierz **Dodaj** i wyszukaj **GitHub** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="91931-129">Otherwise, select **Add** and search for **GitHub** in hello application gallery.</span></span> <span data-ttu-id="91931-130">Wybierz GitHub z wyników wyszukiwania hello i dodać go tooyour listę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="91931-130">Select GitHub from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="91931-131">Wybierz wystąpienie usługi GitHub, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="91931-131">Select your instance of GitHub, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="91931-132">Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="91931-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Inicjowanie obsługi usługi GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. <span data-ttu-id="91931-134">W obszarze hello **poświadczeń administratora** kliknij **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="91931-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="91931-135">Ta operacja otwiera okno dialogowe autoryzacji GitHub w nowym oknie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="91931-135">This operation opens a GitHub authorization dialog in a new browser window.</span></span> 

6. <span data-ttu-id="91931-136">W nowym oknie hello Zaloguj się do usługi GitHub przy użyciu konta administratora.</span><span class="sxs-lookup"><span data-stu-id="91931-136">In hello new window, sign into GitHub using your Admin account.</span></span> <span data-ttu-id="91931-137">W hello wynikowy okna dialogowego autoryzacji, wybierz zespół GitHub hello, inicjowanie obsługi tooenable, a następnie wybierz **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="91931-137">In hello resulting authorization dialog, select hello GitHub team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="91931-138">Inicjowanie obsługi konfiguracji hello toocomplete portalu Azure po zakończeniu, zwróć toohello.</span><span class="sxs-lookup"><span data-stu-id="91931-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

    ![Okno dialogowe autoryzacji](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. <span data-ttu-id="91931-140">W portalu Azure hello, wprowadź **adres URL dzierżawy** i kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć tooyour GitHub aplikację.</span><span class="sxs-lookup"><span data-stu-id="91931-140">In hello Azure portal, input **Tenant URL** and click **Test Connection** tooensure Azure AD can connect tooyour GitHub app.</span></span> <span data-ttu-id="91931-141">Jeśli hello połączenia nie powiedzie się, upewnij się, Twoje konto GitHub ma uprawnienia administratora i **adres URl dzierżawy** jest wprowadzona poprawnie, a następnie spróbuj hello "Autoryzuj" krok ponownie (może stanowić **adres URL dzierżawy** przez regułę: "https : //api.github.com/scim/v2/organizations/ + < Organizations_name > ", można znaleźć Twojej organizacji na koncie usługi GitHub: **ustawienia** > **organizacji**).</span><span class="sxs-lookup"><span data-stu-id="91931-141">If hello connection fails, ensure your GitHub account has Admin permissions and **Tenant URl** is inputted correctly, then try hello "Authorize" step again (you can constitute **Tenant URL** by rule: "https://api.github.com/scim/v2/organizations/ + <Organizations_name>", you can find your organizations under your GitHub account: **Settings** > **Organizations**).</span></span>

    ![Okno dialogowe autoryzacji](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. <span data-ttu-id="91931-143">Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola i wyboru hello wyboru "Wyślij wiadomość e-mail z powiadomieniem, gdy wystąpi błąd."</span><span class="sxs-lookup"><span data-stu-id="91931-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

9. <span data-ttu-id="91931-144">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="91931-144">Click **Save**.</span></span> 

10. <span data-ttu-id="91931-145">W obszarze hello sekcji mapowania, wybierz **tooGitHub synchronizacji Azure Active Directory użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="91931-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGitHub**.</span></span>

11. <span data-ttu-id="91931-146">W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooGitHub.</span><span class="sxs-lookup"><span data-stu-id="91931-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGitHub.</span></span> <span data-ttu-id="91931-147">Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello konta w serwisie GitHub operacje aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="91931-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in GitHub for update operations.</span></span> <span data-ttu-id="91931-148">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="91931-148">Select hello Save button toocommit any changes.</span></span>

12. <span data-ttu-id="91931-149">tooenable hello inicjowania obsługi usługi Azure AD dla usługi GitHub, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="91931-149">tooenable hello Azure AD provisioning service for GitHub, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13. <span data-ttu-id="91931-150">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="91931-150">Click **Save**.</span></span> 

<span data-ttu-id="91931-151">Ta operacja spowoduje uruchomienie synchronizacji początkowej hello użytkowników i/lub grupy przypisane tooGitHub w hello użytkowników i grup sekcji.</span><span class="sxs-lookup"><span data-stu-id="91931-151">This operation starts hello initial synchronization of any users and/or groups assigned tooGitHub in hello Users and Groups section.</span></span> <span data-ttu-id="91931-152">Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello.</span><span class="sxs-lookup"><span data-stu-id="91931-152">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="91931-153">Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello inicjowania obsługi usługi.</span><span class="sxs-lookup"><span data-stu-id="91931-153">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="91931-154">Aby uzyskać więcej informacji dotyczących sposobu inicjowania obsługi usługi Azure AD hello tooread logowania, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="91931-154">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="91931-155">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="91931-155">Additional resources</span></span>

* [<span data-ttu-id="91931-156">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="91931-156">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="91931-157">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="91931-157">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="91931-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="91931-158">Next steps</span></span>

* [<span data-ttu-id="91931-159">Dowiedz się, jak dzienniki tooreview i Uzyskaj raporty dotyczące inicjowania obsługi administracyjnej działania</span><span class="sxs-lookup"><span data-stu-id="91931-159">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
