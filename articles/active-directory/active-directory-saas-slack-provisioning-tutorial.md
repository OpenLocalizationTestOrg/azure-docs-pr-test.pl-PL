---
title: "Samouczek: Konfigurowanie zapas czasu dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konta tooSlack tooconfigure usługi Azure Active Directory tooautomatically udostępniania i usuwanie użytkowników."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="5705a-103">Samouczek: Konfigurowanie zapas czasu dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="5705a-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="5705a-104">Witaj celem tego samouczka jest tooshow hello czynności, które należy tooperform zapas czasu i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooSlack.</span><span class="sxs-lookup"><span data-stu-id="5705a-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Slack and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSlack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5705a-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5705a-105">Prerequisites</span></span>

<span data-ttu-id="5705a-106">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5705a-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="5705a-107">Dzierżawy usługi Azure Active Active directory</span><span class="sxs-lookup"><span data-stu-id="5705a-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="5705a-108">Zapas czasu dzierżawy z hello [Plus planu](https://aadsyncfabric.slack.com/pricing) lub lepiej jest włączone</span><span class="sxs-lookup"><span data-stu-id="5705a-108">A Slack tenant with hello [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="5705a-109">Konto użytkownika w zapas czasu z uprawnieniami administratora zespołu</span><span class="sxs-lookup"><span data-stu-id="5705a-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="5705a-110">Uwaga: hello Azure AD inicjowania obsługi administracyjnej integracji opiera się na powitania [API SCIM zapas czasu](https://api.slack.com/scim) czyli zespoły tooSlack dostępne na powitania Plus planu lub większą.</span><span class="sxs-lookup"><span data-stu-id="5705a-110">Note: hello Azure AD provisioning integration relies on hello [Slack SCIM API](https://api.slack.com/scim) which is available tooSlack teams on hello Plus plan or better.</span></span>

## <a name="assigning-users-tooslack"></a><span data-ttu-id="5705a-111">Przypisywanie użytkowników tooSlack</span><span class="sxs-lookup"><span data-stu-id="5705a-111">Assigning users tooSlack</span></span>

<span data-ttu-id="5705a-112">Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu.</span><span class="sxs-lookup"><span data-stu-id="5705a-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="5705a-113">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD będą synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="5705a-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="5705a-114">Przed Skonfiguruj i Włącz hello inicjowania obsługi usługi, konieczne będzie toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji Slack tooyour.</span><span class="sxs-lookup"><span data-stu-id="5705a-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Slack app.</span></span> <span data-ttu-id="5705a-115">Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour Slack aplikacji:</span><span class="sxs-lookup"><span data-stu-id="5705a-115">Once decided, you can assign these users tooyour Slack app by following hello instructions here:</span></span>

[<span data-ttu-id="5705a-116">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="5705a-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a><span data-ttu-id="5705a-117">Ważne porady dotyczące przypisywania tooSlack użytkowników</span><span class="sxs-lookup"><span data-stu-id="5705a-117">Important tips for assigning users tooSlack</span></span>

*   <span data-ttu-id="5705a-118">Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać hello tootest tooSlack inicjowania obsługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5705a-118">It is recommended that a single Azure AD user be assigned tooSlack tootest hello provisioning configuration.</span></span> <span data-ttu-id="5705a-119">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="5705a-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="5705a-120">Podczas przypisywania tooSlack użytkownika, należy wybrać hello **użytkownika** lub rola "Grupy" w oknie dialogowym przydział hello.</span><span class="sxs-lookup"><span data-stu-id="5705a-120">When assigning a user tooSlack, you must select hello **User** or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="5705a-121">Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="5705a-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-tooslack"></a><span data-ttu-id="5705a-122">Konfigurowanie inicjowania obsługi administracyjnej tooSlack użytkownika</span><span class="sxs-lookup"><span data-stu-id="5705a-122">Configuring user provisioning tooSlack</span></span> 

<span data-ttu-id="5705a-123">Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooSlack programu Azure AD i konfigurowanie hello inicjowania obsługi administracyjnej toocreate usługi, zaktualizuj i wyłączenie konta użytkowników przypisane w zapas czasu, w oparciu o przypisania użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5705a-123">This section guides you through connecting your Azure AD tooSlack's user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="5705a-124">**Porada:** można też tooenabled na języku SAML rejestracji jednokrotnej dla zapas czasu, zgodnie z instrukcjami hello (Azure portal) [https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="5705a-124">**Tip:** You may also choose tooenabled SAML-based Single Sign-On for Slack, following hello instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="5705a-125">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.</span><span class="sxs-lookup"><span data-stu-id="5705a-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a><span data-ttu-id="5705a-126">konto użytkownika automatyczne tooconfigure udostępniania tooSlack w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="5705a-126">tooconfigure automatic user account provisioning tooSlack in Azure AD:</span></span>


1)  <span data-ttu-id="5705a-127">W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="5705a-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="5705a-128">Zapas czasu został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpienie usługi przy użyciu pola wyszukiwania hello zapas czasu.</span><span class="sxs-lookup"><span data-stu-id="5705a-128">If you have already configured Slack for single sign-on, search for your instance of Slack using hello search field.</span></span> <span data-ttu-id="5705a-129">W przeciwnym razie wybierz **Dodaj** i wyszukaj **Slack** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5705a-129">Otherwise, select **Add** and search for **Slack** in hello application gallery.</span></span> <span data-ttu-id="5705a-130">Wybierz zapas czasu z wyników wyszukiwania hello i dodać go tooyour listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5705a-130">Select Slack from hello search results, and add it tooyour list of applications.</span></span>

3)  <span data-ttu-id="5705a-131">Wybierz wystąpienia programu zapas czasu, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="5705a-131">Select your instance of Slack, then select hello **Provisioning** tab.</span></span>

4)  <span data-ttu-id="5705a-132">Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="5705a-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Zapas czasu obsługi](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="5705a-134">W obszarze hello **poświadczeń administratora** kliknij **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="5705a-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="5705a-135">Spowoduje to otwarcie okna dialogowego Slack autoryzacji w nowym oknie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="5705a-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="5705a-136">W nowym oknie hello Zaloguj się do zapas czasu przy użyciu konta administratora zespołu.</span><span class="sxs-lookup"><span data-stu-id="5705a-136">In hello new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="5705a-137">w hello wynikowy autoryzacji oknie dialogowym Wybierz hello Slack zespół, który ma tooenable Inicjowanie obsługi, a następnie wybierz **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="5705a-137">in hello resulting authorization dialog, select hello Slack team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="5705a-138">Inicjowanie obsługi konfiguracji hello toocomplete portalu Azure po zakończeniu, zwróć toohello.</span><span class="sxs-lookup"><span data-stu-id="5705a-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

![Okno dialogowe autoryzacji](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="5705a-140">W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć aplikację Slack tooyour.</span><span class="sxs-lookup"><span data-stu-id="5705a-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Slack app.</span></span> <span data-ttu-id="5705a-141">Jeśli hello połączenia nie powiedzie się, upewnij się, że Slack konto ma uprawnienia administratora zespołu i spróbuj hello "Autoryzuj" krok ponownie.</span><span class="sxs-lookup"><span data-stu-id="5705a-141">If hello connection fails, ensure your Slack account has Team Admin permissions and try hello "Authorize" step again.</span></span>

8) <span data-ttu-id="5705a-142">Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola i zaznacz pole wyboru hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="5705a-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

9) <span data-ttu-id="5705a-143">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="5705a-143">Click **Save**.</span></span> 

10) <span data-ttu-id="5705a-144">W obszarze hello sekcji mapowania, wybierz **tooSlack synchronizacji Azure Active Directory użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="5705a-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSlack**.</span></span>

11) <span data-ttu-id="5705a-145">W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooSlack.</span><span class="sxs-lookup"><span data-stu-id="5705a-145">In hello **Attribute Mappings** section, review hello user attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="5705a-146">Należy pamiętać, że wybrany jako atrybuty hello **pasujące** właściwości będzie używane toomatch hello kontom zapas czasu dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="5705a-146">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts in Slack for update operations.</span></span> <span data-ttu-id="5705a-147">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="5705a-147">Select hello Save button toocommit any changes.</span></span>

12) <span data-ttu-id="5705a-148">tooenable hello inicjowania obsługi usługi Azure AD dla zapas czasu, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="5705a-148">tooenable hello Azure AD provisioning service for Slack, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13) <span data-ttu-id="5705a-149">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="5705a-149">Click **Save**.</span></span> 

<span data-ttu-id="5705a-150">Spowoduje to uruchomienie synchronizacji początkowej hello użytkowników i/lub grupy przypisane tooSlack w hello użytkowników i grup sekcji.</span><span class="sxs-lookup"><span data-stu-id="5705a-150">This will start hello initial synchronization of any users and/or groups assigned tooSlack in hello Users and Groups section.</span></span> <span data-ttu-id="5705a-151">Należy pamiętać, że synchronizacji początkowej hello potrwa tooperform dłużej niż kolejne synchronizacje, które występują co 10 minut, tak długo, jak działa usługa hello.</span><span class="sxs-lookup"><span data-stu-id="5705a-151">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 10 minutes as long as hello service is running.</span></span> <span data-ttu-id="5705a-152">Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie akcje wykonywane przez hello świadczenie usługi na Slack aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5705a-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-tooslack"></a><span data-ttu-id="5705a-153">[Opcjonalnie] Konfigurowanie inicjowania obsługi administracyjnej tooSlack obiektu grupy</span><span class="sxs-lookup"><span data-stu-id="5705a-153">[Optional] Configuring group object provisioning tooSlack</span></span> 

<span data-ttu-id="5705a-154">Opcjonalnie można włączyć hello udostępnianie obiektów grupy z tooSlack usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5705a-154">Optionally, you can enable hello provisioning of group objects from Azure AD tooSlack.</span></span> <span data-ttu-id="5705a-155">To jest inny niż "przypisanie grupy użytkowników", w tym obiekcie rzeczywiste grupy hello dodatkowo tooits elementy członkowskie będą replikowane z tooSlack usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5705a-155">This is different from "assigning groups of users", in that hello actual group object in addition tooits members will be replicated from Azure AD tooSlack.</span></span> <span data-ttu-id="5705a-156">Na przykład jeśli istnieje grupa o nazwie "My" w usłudze Azure AD, wewnątrz zapas czasu zostanie utworzona grupa identitical o nazwie "My".</span><span class="sxs-lookup"><span data-stu-id="5705a-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="tooenable-provisioning-of-group-objects"></a><span data-ttu-id="5705a-157">obiekty grupy tooenable inicjowania obsługi administracyjnej:</span><span class="sxs-lookup"><span data-stu-id="5705a-157">tooenable provisioning of group objects:</span></span>

1) <span data-ttu-id="5705a-158">W obszarze hello sekcji mapowania, wybierz **tooSlack synchronizacji Azure Active Directory grup**.</span><span class="sxs-lookup"><span data-stu-id="5705a-158">Under hello Mappings section, select **Synchronize Azure Active Directory Groups tooSlack**.</span></span>

2) <span data-ttu-id="5705a-159">W bloku atrybutu mapowania hello ustawić tooYes włączone.</span><span class="sxs-lookup"><span data-stu-id="5705a-159">In hello Attribute Mapping blade, set Enabled tooYes.</span></span>

3) <span data-ttu-id="5705a-160">W hello **mapowań atrybutów** Przejrzyj hello grupy atrybutów, które są synchronizowane z usługą Azure AD tooSlack.</span><span class="sxs-lookup"><span data-stu-id="5705a-160">In hello **Attribute Mappings** section, review hello group attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="5705a-161">Należy pamiętać, że wybrany jako atrybuty hello **pasujące** właściwości zostaną grup hello toomatch używanych w zapas czasu dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="5705a-161">Note that hello attributes selected as **Matching** properties will be used toomatch hello groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="5705a-162">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="5705a-162">Click **Save**.</span></span>

<span data-ttu-id="5705a-163">Ten wynik w dowolnej grupy tooSlack przypisane obiekty w hello **użytkowników i grup** sekcji pełni synchronizowane z usługą Azure AD tooSlack.</span><span class="sxs-lookup"><span data-stu-id="5705a-163">This result in any group objects assigned tooSlack in hello **Users and Groups** section being fully synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="5705a-164">Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie akcje wykonywane przez hello świadczenie usługi na Slack aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5705a-164">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="5705a-165">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5705a-165">Additional Resources</span></span>

* [<span data-ttu-id="5705a-166">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="5705a-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="5705a-167">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5705a-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
