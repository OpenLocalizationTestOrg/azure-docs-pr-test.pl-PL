---
title: "Samouczek: Konfigurowanie LucidChart dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konta tooLucidChart tooconfigure usługi Azure Active Directory tooautomatically udostępniania i usuwanie użytkowników."
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
ms.openlocfilehash: d3af45141731215f2edc8942ad21b016468c1e38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="4c1df-103">Samouczek: Konfigurowanie LucidChart dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="4c1df-103">Tutorial: Configuring LucidChart for Automatic User Provisioning</span></span>


<span data-ttu-id="4c1df-104">Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w LucidChart i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooLucidChart.</span><span class="sxs-lookup"><span data-stu-id="4c1df-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LucidChart and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4c1df-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4c1df-105">Prerequisites</span></span>

<span data-ttu-id="4c1df-106">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4c1df-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="4c1df-107">Dzierżawy usługi Azure Active directory</span><span class="sxs-lookup"><span data-stu-id="4c1df-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="4c1df-108">Dzierżawcy LucidChart z hello [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) lub lepiej jest włączone</span><span class="sxs-lookup"><span data-stu-id="4c1df-108">A LucidChart tenant with hello [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="4c1df-109">Konto użytkownika z uprawnieniami administratora w LucidChart</span><span class="sxs-lookup"><span data-stu-id="4c1df-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-toolucidchart"></a><span data-ttu-id="4c1df-110">Przypisywanie użytkowników tooLucidChart</span><span class="sxs-lookup"><span data-stu-id="4c1df-110">Assigning users tooLucidChart</span></span>

<span data-ttu-id="4c1df-111">Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu.</span><span class="sxs-lookup"><span data-stu-id="4c1df-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="4c1df-112">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="4c1df-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="4c1df-113">Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji LucidChart tooyour.</span><span class="sxs-lookup"><span data-stu-id="4c1df-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour LucidChart app.</span></span> <span data-ttu-id="4c1df-114">Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour LucidChart aplikacji:</span><span class="sxs-lookup"><span data-stu-id="4c1df-114">Once decided, you can assign these users tooyour LucidChart app by following hello instructions here:</span></span>

[<span data-ttu-id="4c1df-115">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="4c1df-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolucidchart"></a><span data-ttu-id="4c1df-116">Ważne porady dotyczące przypisywania tooLucidChart użytkowników</span><span class="sxs-lookup"><span data-stu-id="4c1df-116">Important tips for assigning users tooLucidChart</span></span>

*   <span data-ttu-id="4c1df-117">Zalecane jest jeden użytkownik usługi Azure AD jest przypisany hello tootest tooLucidChart inicjowania obsługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4c1df-117">It is recommended that a single Azure AD user is assigned tooLucidChart tootest hello provisioning configuration.</span></span> <span data-ttu-id="4c1df-118">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="4c1df-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="4c1df-119">Podczas przypisywania tooLucidChart użytkownika, należy wybrać albo hello **użytkownika** rola, lub inny prawidłowy specyficzne dla aplikacji (jeśli jest dostępny) w oknie dialogowym przydział hello.</span><span class="sxs-lookup"><span data-stu-id="4c1df-119">When assigning a user tooLucidChart, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="4c1df-120">Witaj **domyślnego dostępu** roli nie działa w przypadku inicjowania obsługi administracyjnej, a użytkownicy są pomijane.</span><span class="sxs-lookup"><span data-stu-id="4c1df-120">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toolucidchart"></a><span data-ttu-id="4c1df-121">Konfigurowanie inicjowania obsługi administracyjnej tooLucidChart użytkownika</span><span class="sxs-lookup"><span data-stu-id="4c1df-121">Configuring user provisioning tooLucidChart</span></span> 

<span data-ttu-id="4c1df-122">Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooLucidChart programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w LucidChart w oparciu o przypisania użytkowników i grup w usłudze Azure AD .</span><span class="sxs-lookup"><span data-stu-id="4c1df-122">This section guides you through connecting your Azure AD tooLucidChart's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="4c1df-123">Można też tooenabled na języku SAML logowania jednokrotnego dla LucidChart hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4c1df-123">You may also choose tooenabled SAML-based Single Sign-On for LucidChart, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4c1df-124">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="4c1df-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toolucidchart-in-azure-ad"></a><span data-ttu-id="4c1df-125">Skonfiguruj konto użytkownika automatycznego inicjowania obsługi administracyjnej tooLucidChart w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c1df-125">Configure automatic user account provisioning tooLucidChart in Azure AD</span></span>


1. <span data-ttu-id="4c1df-126">W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="4c1df-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="4c1df-127">LucidChart został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpieniem LucidChart za pomocą hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="4c1df-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using hello search field.</span></span> <span data-ttu-id="4c1df-128">W przeciwnym razie wybierz **Dodaj** i wyszukaj **LucidChart** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="4c1df-128">Otherwise, select **Add** and search for **LucidChart** in hello application gallery.</span></span> <span data-ttu-id="4c1df-129">Wybierz LucidChart z wyników wyszukiwania hello i dodać go tooyour listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c1df-129">Select LucidChart from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="4c1df-130">Wybierz wystąpienia programu LucidChart, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="4c1df-130">Select your instance of LucidChart, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="4c1df-131">Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="4c1df-131">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![LucidChart inicjowania obsługi administracyjnej.](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="4c1df-133">W obszarze hello **poświadczeń administratora** hello wejściowych, sekcji **klucz tajny tokenu** generowane przez konto użytkownika LucidChart (przy użyciu tego konta można znaleźć tokenu hello: **zespołu**  >  **Integracji aplikacji** > **SCIM**).</span><span class="sxs-lookup"><span data-stu-id="4c1df-133">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your LucidChart's account (you can find hello token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![LucidChart inicjowania obsługi administracyjnej.](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="4c1df-135">W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć tooyour LucidChart aplikację.</span><span class="sxs-lookup"><span data-stu-id="4c1df-135">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour LucidChart app.</span></span> <span data-ttu-id="4c1df-136">Jeśli hello połączenia nie powiedzie się, upewnij się, że Twoje konto LucidChart ma uprawnienia administratora i spróbuj ponownie wykonać krok 5.</span><span class="sxs-lookup"><span data-stu-id="4c1df-136">If hello connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="4c1df-137">Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola i wyboru hello wyboru "Wyślij wiadomość e-mail z powiadomieniem, gdy wystąpi błąd."</span><span class="sxs-lookup"><span data-stu-id="4c1df-137">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="4c1df-138">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4c1df-138">Click **Save**.</span></span> 

9. <span data-ttu-id="4c1df-139">W obszarze hello sekcji mapowania, wybierz **tooLucidChart synchronizacji Azure Active Directory użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="4c1df-139">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooLucidChart**.</span></span>

10. <span data-ttu-id="4c1df-140">W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooLucidChart.</span><span class="sxs-lookup"><span data-stu-id="4c1df-140">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooLucidChart.</span></span> <span data-ttu-id="4c1df-141">Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom LucidChart dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="4c1df-141">hello attributes selected as **Matching** properties are used toomatch hello user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="4c1df-142">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="4c1df-142">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="4c1df-143">tooenable hello inicjowania obsługi usługi Azure AD dla LucidChart, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="4c1df-143">tooenable hello Azure AD provisioning service for LucidChart, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="4c1df-144">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4c1df-144">Click **Save**.</span></span> 

<span data-ttu-id="4c1df-145">Ta operacja spowoduje uruchomienie synchronizacji początkowej hello użytkowników i/lub grupy przypisane tooLucidChart w hello użytkowników i grup sekcji.</span><span class="sxs-lookup"><span data-stu-id="4c1df-145">This operation starts hello initial synchronization of any users and/or groups assigned tooLucidChart in hello Users and Groups section.</span></span> <span data-ttu-id="4c1df-146">Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello.</span><span class="sxs-lookup"><span data-stu-id="4c1df-146">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="4c1df-147">Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello inicjowania obsługi usługi.</span><span class="sxs-lookup"><span data-stu-id="4c1df-147">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="4c1df-148">Aby uzyskać więcej informacji dotyczących sposobu inicjowania obsługi usługi Azure AD hello tooread logowania, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="4c1df-148">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4c1df-149">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4c1df-149">Additional resources</span></span>

* [<span data-ttu-id="4c1df-150">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="4c1df-150">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="4c1df-151">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4c1df-151">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="4c1df-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4c1df-152">Next steps</span></span>

* [<span data-ttu-id="4c1df-153">Dowiedz się, jak dzienniki tooreview i Uzyskaj raporty dotyczące inicjowania obsługi administracyjnej działania</span><span class="sxs-lookup"><span data-stu-id="4c1df-153">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
