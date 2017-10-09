---
title: "Samouczek: Konfigurowanie Samanage dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konta tooSamanage tooconfigure usługi Azure Active Directory tooautomatically udostępniania i usuwanie użytkowników."
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
ms.openlocfilehash: 6cb36d2cc6ce33da4f8ebba65d138bfd4f2aca9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a><span data-ttu-id="4f496-103">Samouczek: Konfigurowanie Samanage dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="4f496-103">Tutorial: Configuring Samanage for Automatic User Provisioning</span></span>


<span data-ttu-id="4f496-104">Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w Samanage i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooSamanage.</span><span class="sxs-lookup"><span data-stu-id="4f496-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Samanage and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSamanage.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4f496-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4f496-105">Prerequisites</span></span>

<span data-ttu-id="4f496-106">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4f496-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="4f496-107">Dzierżawy usługi Azure Active directory</span><span class="sxs-lookup"><span data-stu-id="4f496-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="4f496-108">Dzierżawcy Samanage z hello [Professional planu](https://www.samanage.com/pricing/) lub lepiej jest włączone</span><span class="sxs-lookup"><span data-stu-id="4f496-108">A Samanage tenant with hello [Professional plan](https://www.samanage.com/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="4f496-109">Konto użytkownika z uprawnieniami administratora w Samanage</span><span class="sxs-lookup"><span data-stu-id="4f496-109">A user account in Samanage with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="4f496-110">Hello Azure AD inicjowania obsługi administracyjnej integracji opiera się na powitania [interfejsu API REST Samanage](https://www.samanage.com/api/), zespoły tooSamanage dostępne na powitania Professional planowanie lub większą.</span><span class="sxs-lookup"><span data-stu-id="4f496-110">hello Azure AD provisioning integration relies on hello [Samanage REST API](https://www.samanage.com/api/), which is available tooSamanage teams on hello Professional plan or better.</span></span>

## <a name="assigning-users-toosamanage"></a><span data-ttu-id="4f496-111">Przypisywanie użytkowników tooSamanage</span><span class="sxs-lookup"><span data-stu-id="4f496-111">Assigning users tooSamanage</span></span>

<span data-ttu-id="4f496-112">Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu.</span><span class="sxs-lookup"><span data-stu-id="4f496-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="4f496-113">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="4f496-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="4f496-114">Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji Samanage tooyour.</span><span class="sxs-lookup"><span data-stu-id="4f496-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Samanage app.</span></span> <span data-ttu-id="4f496-115">Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour Samanage aplikacji:</span><span class="sxs-lookup"><span data-stu-id="4f496-115">Once decided, you can assign these users tooyour Samanage app by following hello instructions here:</span></span>

[<span data-ttu-id="4f496-116">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="4f496-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toosamanage"></a><span data-ttu-id="4f496-117">Ważne porady dotyczące przypisywania tooSamanage użytkowników</span><span class="sxs-lookup"><span data-stu-id="4f496-117">Important tips for assigning users tooSamanage</span></span>

*   <span data-ttu-id="4f496-118">Zalecane jest jeden użytkownik usługi Azure AD jest przypisany hello tootest tooSamanage inicjowania obsługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4f496-118">It is recommended that a single Azure AD user is assigned tooSamanage tootest hello provisioning configuration.</span></span> <span data-ttu-id="4f496-119">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="4f496-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="4f496-120">Podczas przypisywania tooSamanage użytkownika, należy wybrać albo hello **użytkownika** rola, lub inny prawidłowy specyficzne dla aplikacji (jeśli jest dostępny) w oknie dialogowym przydział hello.</span><span class="sxs-lookup"><span data-stu-id="4f496-120">When assigning a user tooSamanage, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="4f496-121">Witaj **domyślnego dostępu** roli nie działa w przypadku inicjowania obsługi administracyjnej, a użytkownicy są pomijane.</span><span class="sxs-lookup"><span data-stu-id="4f496-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="4f496-122">Dodano funkcję hello świadczenie usługi odczytuje wszystkie role niestandardowe zdefiniowane w Samanage i zaimportowanie ich do usługi Azure AD, w którym można je wybrać w oknie dialogowym Wybierz rolę hello.</span><span class="sxs-lookup"><span data-stu-id="4f496-122">As an added feature, hello provisioning service reads any custom roles defined in Samanage, and imports them into Azure AD where they can be selected in hello Select Role dialog.</span></span> <span data-ttu-id="4f496-123">Role te będą widoczne w hello portalu Azure po włączeniu hello usługi inicjowania obsługi administracyjnej i jednego cyklu synchronizacji zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="4f496-123">These roles will be visible in hello Azure portal after hello provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-toosamanage"></a><span data-ttu-id="4f496-124">Konfigurowanie inicjowania obsługi administracyjnej tooSamanage użytkownika</span><span class="sxs-lookup"><span data-stu-id="4f496-124">Configuring user provisioning tooSamanage</span></span> 

<span data-ttu-id="4f496-125">Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooSamanage programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w Samanage w oparciu o przypisania użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4f496-125">This section guides you through connecting your Azure AD tooSamanage's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Samanage based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="4f496-126">Można też tooenabled na języku SAML logowania jednokrotnego dla Samanage hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4f496-126">You may also choose tooenabled SAML-based Single Sign-On for Samanage, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4f496-127">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="4f496-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toosamanage-in-azure-ad"></a><span data-ttu-id="4f496-128">Skonfiguruj konto użytkownika automatycznego inicjowania obsługi administracyjnej tooSamanage w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="4f496-128">Configure automatic user account provisioning tooSamanage in Azure AD:</span></span>


1. <span data-ttu-id="4f496-129">W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="4f496-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="4f496-130">Samanage został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpieniem Samanage za pomocą hello pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="4f496-130">If you have already configured Samanage for single sign-on, search for your instance of Samanage using hello search field.</span></span> <span data-ttu-id="4f496-131">W przeciwnym razie wybierz **Dodaj** i wyszukaj **Samanage** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="4f496-131">Otherwise, select **Add** and search for **Samanage** in hello application gallery.</span></span> <span data-ttu-id="4f496-132">Wybierz Samanage z wyników wyszukiwania hello i dodać go tooyour listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4f496-132">Select Samanage from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="4f496-133">Wybierz wystąpienia programu Samanage, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="4f496-133">Select your instance of Samanage, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="4f496-134">Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="4f496-134">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Samanage inicjowania obsługi administracyjnej.](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. <span data-ttu-id="4f496-136">W obszarze hello **poświadczeń administratora** hello wejściowych, sekcji **nazwa użytkownika i hasło administratora** Twojego Samanage konta.</span><span class="sxs-lookup"><span data-stu-id="4f496-136">Under hello **Admin Credentials** section, input hello **Admin Username&Admin Password** of your Samanage's account.</span></span> 

6. <span data-ttu-id="4f496-137">W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć tooyour Samanage aplikację.</span><span class="sxs-lookup"><span data-stu-id="4f496-137">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Samanage app.</span></span> <span data-ttu-id="4f496-138">Jeśli hello połączenia nie powiedzie się, upewnij się, że Twoje konto Samanage ma uprawnienia administratora i spróbuj ponownie wykonać krok 5.</span><span class="sxs-lookup"><span data-stu-id="4f496-138">If hello connection fails, ensure your Samanage account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="4f496-139">Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola i wyboru hello wyboru "Wyślij wiadomość e-mail z powiadomieniem, gdy wystąpi błąd."</span><span class="sxs-lookup"><span data-stu-id="4f496-139">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="4f496-140">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4f496-140">Click **Save**.</span></span> 

9. <span data-ttu-id="4f496-141">W obszarze hello sekcji mapowania, wybierz **tooSamanage synchronizacji Azure Active Directory użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="4f496-141">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSamanage**.</span></span>

10. <span data-ttu-id="4f496-142">W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooSamanage.</span><span class="sxs-lookup"><span data-stu-id="4f496-142">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooSamanage.</span></span> <span data-ttu-id="4f496-143">Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom Samanage dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="4f496-143">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Samanage for update operations.</span></span> <span data-ttu-id="4f496-144">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="4f496-144">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="4f496-145">tooenable hello inicjowania obsługi usługi Azure AD dla Samanage, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="4f496-145">tooenable hello Azure AD provisioning service for Samanage, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="4f496-146">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4f496-146">Click **Save**.</span></span> 

<span data-ttu-id="4f496-147">Ta operacja spowoduje uruchomienie synchronizacji początkowej hello użytkowników i/lub grupy przypisane tooSamanage w hello użytkowników i grup sekcji.</span><span class="sxs-lookup"><span data-stu-id="4f496-147">This operation starts hello initial synchronization of any users and/or groups assigned tooSamanage in hello Users and Groups section.</span></span> <span data-ttu-id="4f496-148">Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello.</span><span class="sxs-lookup"><span data-stu-id="4f496-148">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="4f496-149">Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello inicjowania obsługi usługi.</span><span class="sxs-lookup"><span data-stu-id="4f496-149">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="4f496-150">Aby uzyskać więcej informacji dotyczących sposobu inicjowania obsługi usługi Azure AD hello tooread logowania, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="4f496-150">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4f496-151">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4f496-151">Additional resources</span></span>

* [<span data-ttu-id="4f496-152">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="4f496-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="4f496-153">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4f496-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="4f496-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4f496-154">Next steps</span></span>

* [<span data-ttu-id="4f496-155">Dowiedz się, jak dzienniki tooreview i Uzyskaj raporty dotyczące inicjowania obsługi administracyjnej działania</span><span class="sxs-lookup"><span data-stu-id="4f496-155">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
