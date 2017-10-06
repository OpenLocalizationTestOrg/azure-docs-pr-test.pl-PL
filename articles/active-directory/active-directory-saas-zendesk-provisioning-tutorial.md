---
title: "Samouczek: Konfigurowanie usługi ZenDesk dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konta tooZenDesk tooconfigure usługi Azure Active Directory tooautomatically udostępniania i usuwanie użytkowników."
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
ms.openlocfilehash: 200e8790ec1755f5cf927274ceb38527dd993f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-zendesk-for-automatic-user-provisioning"></a><span data-ttu-id="8a070-103">Samouczek: Konfigurowanie usługi ZenDesk dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="8a070-103">Tutorial: Configuring ZenDesk for Automatic User Provisioning</span></span>


<span data-ttu-id="8a070-104">Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w ZenDesk i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooZenDesk.</span><span class="sxs-lookup"><span data-stu-id="8a070-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in ZenDesk and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooZenDesk.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8a070-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8a070-105">Prerequisites</span></span>

<span data-ttu-id="8a070-106">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8a070-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="8a070-107">Dzierżawy usługi Azure Active directory</span><span class="sxs-lookup"><span data-stu-id="8a070-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="8a070-108">Dzierżawcy ZenDesk z hello [Enterprise plan](https://www.zendesk.com/product/pricing/) lub lepiej jest włączone</span><span class="sxs-lookup"><span data-stu-id="8a070-108">A ZenDesk tenant with hello [Enterprise plan](https://www.zendesk.com/product/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="8a070-109">Konto użytkownika z uprawnieniami administratora w ZenDesk</span><span class="sxs-lookup"><span data-stu-id="8a070-109">A user account in ZenDesk with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="8a070-110">Witaj usługi Azure AD inicjowania obsługi administracyjnej integracji opiera się na powitania [interfejsu API REST usługi ZenDesk](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), co jest dostępne tooZenDesk zespoły w planie niezbędne hello lub większą.</span><span class="sxs-lookup"><span data-stu-id="8a070-110">hello Azure AD provisioning integration relies on hello [ZenDesk REST API](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), which is available tooZenDesk teams on hello Essential plan or better.</span></span>

## <a name="assigning-users-toozendesk"></a><span data-ttu-id="8a070-111">Przypisywanie użytkowników tooZenDesk</span><span class="sxs-lookup"><span data-stu-id="8a070-111">Assigning users tooZenDesk</span></span>

<span data-ttu-id="8a070-112">Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu.</span><span class="sxs-lookup"><span data-stu-id="8a070-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="8a070-113">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD są synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="8a070-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="8a070-114">Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji usługi ZenDesk tooyour.</span><span class="sxs-lookup"><span data-stu-id="8a070-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour ZenDesk app.</span></span> <span data-ttu-id="8a070-115">Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour ZenDesk aplikacji:</span><span class="sxs-lookup"><span data-stu-id="8a070-115">Once decided, you can assign these users tooyour ZenDesk app by following hello instructions here:</span></span>

[<span data-ttu-id="8a070-116">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="8a070-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toozendesk"></a><span data-ttu-id="8a070-117">Ważne porady dotyczące przypisywania tooZenDesk użytkowników</span><span class="sxs-lookup"><span data-stu-id="8a070-117">Important tips for assigning users tooZenDesk</span></span>

*   <span data-ttu-id="8a070-118">Zalecane jest jeden użytkownik usługi Azure AD jest przypisany hello tootest tooZenDesk inicjowania obsługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8a070-118">It is recommended that a single Azure AD user is assigned tooZenDesk tootest hello provisioning configuration.</span></span> <span data-ttu-id="8a070-119">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="8a070-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="8a070-120">Podczas przypisywania tooZenDesk użytkownika, należy wybrać albo hello **użytkownika** rola, lub inny prawidłowy specyficzne dla aplikacji (jeśli jest dostępny) w oknie dialogowym przydział hello.</span><span class="sxs-lookup"><span data-stu-id="8a070-120">When assigning a user tooZenDesk, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="8a070-121">Witaj **domyślnego dostępu** roli nie działa w przypadku inicjowania obsługi administracyjnej, a użytkownicy są pomijane.</span><span class="sxs-lookup"><span data-stu-id="8a070-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="8a070-122">Dodano funkcję hello świadczenie usługi odczytuje wszystkie role niestandardowe zdefiniowane w Zendesk i zaimportowanie ich do usługi Azure AD, w którym można je wybrać w oknie dialogowym Wybierz rolę hello.</span><span class="sxs-lookup"><span data-stu-id="8a070-122">As an added feature, hello provisioning service reads any custom roles defined in Zendesk, and imports them into Azure AD where they can be selected in hello Select Role dialog.</span></span> <span data-ttu-id="8a070-123">Role te będą widoczne w hello portalu Azure po włączeniu hello usługi inicjowania obsługi administracyjnej i jednego cyklu synchronizacji zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="8a070-123">These roles will be visible in hello Azure portal after hello provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-toozendesk"></a><span data-ttu-id="8a070-124">Konfigurowanie inicjowania obsługi administracyjnej tooZenDesk użytkownika</span><span class="sxs-lookup"><span data-stu-id="8a070-124">Configuring user provisioning tooZenDesk</span></span> 

<span data-ttu-id="8a070-125">Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooZenDesk programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w ZenDesk w oparciu o przypisania użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a070-125">This section guides you through connecting your Azure AD tooZenDesk's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in ZenDesk based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="8a070-126">Można też tooenabled na języku SAML logowania jednokrotnego dla ZenDesk hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8a070-126">You may also choose tooenabled SAML-based Single Sign-On for ZenDesk, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8a070-127">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="8a070-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toozendesk-in-azure-ad"></a><span data-ttu-id="8a070-128">Skonfiguruj konto użytkownika automatycznego inicjowania obsługi administracyjnej tooZenDesk w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a070-128">Configure automatic user account provisioning tooZenDesk in Azure AD</span></span>


1. <span data-ttu-id="8a070-129">W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="8a070-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="8a070-130">Jeśli skonfigurowano już program ZenDesk dla logowania jednokrotnego, wyszukiwanie wystąpienia programu ZenDesk przy użyciu pola wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="8a070-130">If you have already configured ZenDesk for single sign-on, search for your instance of ZenDesk using hello search field.</span></span> <span data-ttu-id="8a070-131">W przeciwnym razie wybierz **Dodaj** i wyszukaj **ZenDesk** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8a070-131">Otherwise, select **Add** and search for **ZenDesk** in hello application gallery.</span></span> <span data-ttu-id="8a070-132">Wybierz ZenDesk z wyników wyszukiwania hello i dodać go tooyour listę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8a070-132">Select ZenDesk from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="8a070-133">Wybierz wystąpienia programu ZenDesk, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="8a070-133">Select your instance of ZenDesk, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="8a070-134">Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="8a070-134">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Inicjowanie obsługi usługi ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk1.png)

5. <span data-ttu-id="8a070-136">W obszarze hello **poświadczeń administratora** hello wejściowych, sekcji **administratora & tokenkey & domeny** generowane przez konto użytkownika usługi ZenDesk (przy użyciu tego konta można znaleźć tokenu hello: **administratora**   >  **Interfejsu API** > **ustawienia**).</span><span class="sxs-lookup"><span data-stu-id="8a070-136">Under hello **Admin Credentials** section, input hello **Admin Username&tokenkey&Domain** generated by your ZenDesk's account (you can find hello token under your account: **Admin** > **API** > **Settings**).</span></span> 

    ![Inicjowanie obsługi usługi ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk2.png)

6. <span data-ttu-id="8a070-138">W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć tooyour ZenDesk aplikację.</span><span class="sxs-lookup"><span data-stu-id="8a070-138">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour ZenDesk app.</span></span> <span data-ttu-id="8a070-139">Jeśli hello połączenia nie powiedzie się, upewnij się, że Twoje konto usługi ZenDesk ma uprawnienia administratora i spróbuj ponownie wykonać krok 5.</span><span class="sxs-lookup"><span data-stu-id="8a070-139">If hello connection fails, ensure your ZenDesk account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="8a070-140">Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola i wyboru hello wyboru "Wyślij wiadomość e-mail z powiadomieniem, gdy wystąpi błąd."</span><span class="sxs-lookup"><span data-stu-id="8a070-140">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="8a070-141">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8a070-141">Click **Save**.</span></span> 

9. <span data-ttu-id="8a070-142">W obszarze hello sekcji mapowania, wybierz **tooZenDesk synchronizacji Azure Active Directory użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="8a070-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooZenDesk**.</span></span>

10. <span data-ttu-id="8a070-143">W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooZenDesk.</span><span class="sxs-lookup"><span data-stu-id="8a070-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooZenDesk.</span></span> <span data-ttu-id="8a070-144">Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom ZenDesk dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="8a070-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in ZenDesk for update operations.</span></span> <span data-ttu-id="8a070-145">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="8a070-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="8a070-146">tooenable hello inicjowania obsługi usługi Azure AD dla usługi ZenDesk, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="8a070-146">tooenable hello Azure AD provisioning service for ZenDesk, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="8a070-147">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8a070-147">Click **Save**.</span></span> 

<span data-ttu-id="8a070-148">Ta operacja spowoduje uruchomienie synchronizacji początkowej hello użytkowników i/lub grupy przypisane tooZenDesk w hello użytkowników i grup sekcji.</span><span class="sxs-lookup"><span data-stu-id="8a070-148">This operation starts hello initial synchronization of any users and/or groups assigned tooZenDesk in hello Users and Groups section.</span></span> <span data-ttu-id="8a070-149">Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello.</span><span class="sxs-lookup"><span data-stu-id="8a070-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="8a070-150">Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello inicjowania obsługi usługi.</span><span class="sxs-lookup"><span data-stu-id="8a070-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="8a070-151">Aby uzyskać więcej informacji dotyczących sposobu inicjowania obsługi usługi Azure AD hello tooread logowania, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="8a070-151">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8a070-152">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8a070-152">Additional resources</span></span>

* [<span data-ttu-id="8a070-153">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="8a070-153">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="8a070-154">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8a070-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="8a070-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8a070-155">Next steps</span></span>

* [<span data-ttu-id="8a070-156">Dowiedz się, jak dzienniki tooreview i Uzyskaj raporty dotyczące inicjowania obsługi administracyjnej działania</span><span class="sxs-lookup"><span data-stu-id="8a070-156">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
