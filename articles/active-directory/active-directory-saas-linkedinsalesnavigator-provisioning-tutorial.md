---
title: "Samouczek: Konfigurowanie LinkedIn Nawigator sprzedaży dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konta tooLinkedIn Nawigator sprzedaży tooconfigure usługi Azure Active Directory tooautomatically udostępniania i usuwanie użytkowników."
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 322c5271535994c13a9fafadbf74f356cdfe865d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-sales-navigator-for-automatic-user-provisioning"></a><span data-ttu-id="52177-103">Samouczek: Konfigurowanie LinkedIn Navigator sprzedaży dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="52177-103">Tutorial: Configuring LinkedIn Sales Navigator for Automatic User Provisioning</span></span>


<span data-ttu-id="52177-104">Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w Navigator sprzedaży LinkedIn i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooLinkedIn Nawigator sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="52177-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LinkedIn Sales Navigator and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLinkedIn Sales Navigator.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="52177-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="52177-105">Prerequisites</span></span>

<span data-ttu-id="52177-106">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="52177-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="52177-107">Dzierżawy usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52177-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="52177-108">Nawigator sprzedaży LinkedIn dzierżawcy</span><span class="sxs-lookup"><span data-stu-id="52177-108">A LinkedIn Sales Navigator tenant</span></span> 
*   <span data-ttu-id="52177-109">Konto administratora w Nawigatorze sprzedaży LinkedIn z toohello dostępu LinkedIn Centrum konta</span><span class="sxs-lookup"><span data-stu-id="52177-109">An administrator account in LinkedIn Sales Navigator with access toohello LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="52177-110">Usługa Azure Active Directory integruje się z Nawigatora sprzedaży LinkedIn przy użyciu hello [SCIM](http://www.simplecloud.info/) protokołu.</span><span class="sxs-lookup"><span data-stu-id="52177-110">Azure Active Directory integrates with LinkedIn Sales Navigator using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toolinkedin-sales-navigator"></a><span data-ttu-id="52177-111">Przypisywanie użytkowników tooLinkedIn Nawigator sprzedaży</span><span class="sxs-lookup"><span data-stu-id="52177-111">Assigning users tooLinkedIn Sales Navigator</span></span>

<span data-ttu-id="52177-112">Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu.</span><span class="sxs-lookup"><span data-stu-id="52177-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="52177-113">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD będą synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="52177-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="52177-114">Przed Skonfiguruj i Włącz hello inicjowania obsługi usługi, konieczne będzie toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą korzystać tooLinkedIn Nawigator sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="52177-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooLinkedIn Sales Navigator.</span></span> <span data-ttu-id="52177-115">Po decyzję, można przypisać tooLinkedIn tych użytkowników Navigator sprzedaży, wykonując instrukcje hello tutaj:</span><span class="sxs-lookup"><span data-stu-id="52177-115">Once decided, you can assign these users tooLinkedIn Sales Navigator by following hello instructions here:</span></span>

[<span data-ttu-id="52177-116">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="52177-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-sales-navigator"></a><span data-ttu-id="52177-117">Ważne porady dotyczące przypisywania użytkowników tooLinkedIn Nawigator sprzedaży</span><span class="sxs-lookup"><span data-stu-id="52177-117">Important tips for assigning users tooLinkedIn Sales Navigator</span></span>

*   <span data-ttu-id="52177-118">Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać hello tootest Nawigator sprzedaży tooLinkedIn inicjowania obsługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="52177-118">It is recommended that a single Azure AD user be assigned tooLinkedIn Sales Navigator tootest hello provisioning configuration.</span></span> <span data-ttu-id="52177-119">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="52177-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="52177-120">Podczas przypisywania tooLinkedIn użytkownika Navigator sprzedaży, należy wybrać hello **użytkownika** roli w oknie dialogowym przydział hello.</span><span class="sxs-lookup"><span data-stu-id="52177-120">When assigning a user tooLinkedIn Sales Navigator, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="52177-121">Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="52177-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-toolinkedin-sales-navigator"></a><span data-ttu-id="52177-122">Konfigurowanie użytkownika inicjowania obsługi administracyjnej tooLinkedIn Nawigator sprzedaży</span><span class="sxs-lookup"><span data-stu-id="52177-122">Configuring user provisioning tooLinkedIn Sales Navigator</span></span>

<span data-ttu-id="52177-123">Ta sekcja przeprowadzi Cię przez łączenie konta użytkownika SCIM programu Azure AD tooLinkedIn sprzedaży programu Navigator inicjowania obsługi interfejsu API i konfigurowanie hello inicjowania obsługi administracyjnej toocreate usługi, zaktualizuj i wyłączenie konta użytkowników przypisane w LinkedIn Nawigatorze sprzedaży na podstawie użytkownika i przypisanie do grupy w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52177-123">This section guides you through connecting your Azure AD tooLinkedIn Sales Navigator's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in LinkedIn Sales Navigator based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="52177-124">Można też tooenabled na języku SAML logowania jednokrotnego dla Navigator sprzedaży LinkedIn, po hello instrukcje podane w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="52177-124">You may also choose tooenabled SAML-based Single Sign-On for LinkedIn Sales Navigator, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="52177-125">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, że te dwie funkcje uzupełniają.</span><span class="sxs-lookup"><span data-stu-id="52177-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-sales-navigator-in-azure-ad"></a><span data-ttu-id="52177-126">konto użytkownika automatyczne tooconfigure udostępniania tooLinkedIn Nawigator sprzedaży w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="52177-126">tooconfigure automatic user account provisioning tooLinkedIn Sales Navigator in Azure AD:</span></span>


<span data-ttu-id="52177-127">pierwszym krokiem Hello jest tooretrieve LinkedIn tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="52177-127">hello first step is tooretrieve your LinkedIn access token.</span></span> <span data-ttu-id="52177-128">Jeśli jesteś administratorem przedsiębiorstwa może samodzielnie inicjować tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="52177-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="52177-129">W Centrum konta, przejdź zbyt**ustawienia &gt; ustawienia globalne** i otwórz hello **Instalator SCIM** panelu.</span><span class="sxs-lookup"><span data-stu-id="52177-129">In your account center, go too**Settings &gt; Global Settings** and open hello **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="52177-130">Jeśli uzyskujesz dostęp do Centrum konta hello bezpośrednio, a nie za pośrednictwem łącza, można osiągnąć za pomocą hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="52177-130">If you are accessing hello account center directly rather than through a link, you can reach it using hello following steps.</span></span>

1)  <span data-ttu-id="52177-131">Zaloguj się w Centrum tooAccount.</span><span class="sxs-lookup"><span data-stu-id="52177-131">Sign in tooAccount Center.</span></span>

2)  <span data-ttu-id="52177-132">Wybierz **Admin &gt; ustawienia administratora** .</span><span class="sxs-lookup"><span data-stu-id="52177-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="52177-133">Kliknij przycisk **zaawansowane integracji** na lewym pasku bocznym hello.</span><span class="sxs-lookup"><span data-stu-id="52177-133">Click **Advanced Integrations** on hello left sidebar.</span></span> <span data-ttu-id="52177-134">Jesteś toohello ukierunkowanej Centrum konta.</span><span class="sxs-lookup"><span data-stu-id="52177-134">You are directed toohello account center.</span></span>

4)  <span data-ttu-id="52177-135">Kliknij przycisk **+ Dodaj nową konfigurację SCIM** i wykonaj procedurę hello wypełniając każdego pola.</span><span class="sxs-lookup"><span data-stu-id="52177-135">Click **+ Add new SCIM configuration** and follow hello procedure by filling in each field.</span></span>

> <span data-ttu-id="52177-136">Autoassign licencji nie jest włączona, oznacza, że tylko dane użytkownika jest synchronizowany.</span><span class="sxs-lookup"><span data-stu-id="52177-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![Nawigator sprzedaży LinkedIn inicjowania obsługi administracyjnej](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="52177-138">Po włączeniu przypisania autolicense należy toonote wystąpienia aplikacji i typu licencji.</span><span class="sxs-lookup"><span data-stu-id="52177-138">When auto­license assignment is enabled, you need toonote the application instance and license type.</span></span> <span data-ttu-id="52177-139">Przypisano licencje na pierwszym dostarczanych, najpierw służyć podstawę, dopóki wszystkie licencje hello są pobierane.</span><span class="sxs-lookup"><span data-stu-id="52177-139">Licenses are assigned on a first come, first serve basis until all hello licenses are taken.</span></span>

![Nawigator sprzedaży LinkedIn inicjowania obsługi administracyjnej](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="52177-141">Kliknij przycisk **Generuj token**.</span><span class="sxs-lookup"><span data-stu-id="52177-141">Click **Generate token**.</span></span> <span data-ttu-id="52177-142">Powinien zostać wyświetlony ekran tokenu dostępu w obszarze hello **token dostępu** pola.</span><span class="sxs-lookup"><span data-stu-id="52177-142">You should see your access token display under hello **Access token** field.</span></span>

6)  <span data-ttu-id="52177-143">Zapisz Schowka tooyour tokenu dostępu lub komputerze z przed opuszczeniem hello strony.</span><span class="sxs-lookup"><span data-stu-id="52177-143">Save your access token tooyour clipboard or computer before leaving hello page.</span></span>

7) <span data-ttu-id="52177-144">Następnie zaloguj się toohello [portalu Azure](https://portal.azure.com)i Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="52177-144">Next, sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="52177-145">Nawigator sprzedaży LinkedIn został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpienia przy użyciu pola wyszukiwania hello Navigator sprzedaży LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="52177-145">If you have already configured LinkedIn Sales Navigator for single sign-on, search for your instance of LinkedIn Sales Navigator using hello search field.</span></span> <span data-ttu-id="52177-146">W przeciwnym razie wybierz **Dodaj** i wyszukaj **LinkedIn sprzedaży Navigator** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="52177-146">Otherwise, select **Add** and search for **LinkedIn Sales Navigator** in hello application gallery.</span></span> <span data-ttu-id="52177-147">Wybierz Navigator sprzedaży LinkedIn z wyników wyszukiwania hello i dodać tooyour listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="52177-147">Select LinkedIn Sales Navigator from hello search results, and add it tooyour list of applications.</span></span>

9)  <span data-ttu-id="52177-148">Wybierz wystąpienia programu Navigator sprzedaży LinkedIn, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="52177-148">Select your instance of LinkedIn Sales Navigator, then select hello **Provisioning** tab.</span></span>

10) <span data-ttu-id="52177-149">Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="52177-149">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Nawigator sprzedaży LinkedIn inicjowania obsługi administracyjnej](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="52177-151">Wypełnij następujące pola w obszarze hello **poświadczeń administratora** :</span><span class="sxs-lookup"><span data-stu-id="52177-151">Fill in hello following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="52177-152">W hello **adres URL dzierżawy** wprowadź https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="52177-152">In hello **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="52177-153">W hello **klucz tajny tokenu** wprowadź token dostępu hello wygenerowany w kroku 1 i kliknij przycisk **Testuj połączenie** .</span><span class="sxs-lookup"><span data-stu-id="52177-153">In hello **Secret Token** field, enter hello access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="52177-154">Powiadomienie Powodzenie powinna zostać wyświetlona po stronie upperright hello portalu usługi.</span><span class="sxs-lookup"><span data-stu-id="52177-154">You should see a success notification on hello upper­right side of   your portal.</span></span>

12) <span data-ttu-id="52177-155">Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola i zaznacz pole wyboru hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="52177-155">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

13) <span data-ttu-id="52177-156">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="52177-156">Click **Save**.</span></span> 

14) <span data-ttu-id="52177-157">W hello **mapowań atrybutów** Przejrzyj atrybuty użytkowników i grup hello, które są synchronizowane z usługi Azure AD tooLinkedIn Nawigator sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="52177-157">In hello **Attribute Mappings** section, review hello user and group attributes that will be synchronized from Azure AD tooLinkedIn Sales Navigator.</span></span> <span data-ttu-id="52177-158">Należy pamiętać, że wybrany jako atrybuty hello **pasujące** właściwości będzie używana toomatch hello kont i grup użytkowników w Nawigatorze sprzedaży LinkedIn dla operacji aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="52177-158">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts and groups in LinkedIn Sales Navigator for update operations.</span></span> <span data-ttu-id="52177-159">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="52177-159">Select hello Save button toocommit any changes.</span></span>

![Nawigator sprzedaży LinkedIn inicjowania obsługi administracyjnej](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="52177-161">tooenable hello inicjowania obsługi usługi Azure AD dla LinkedIn Navigator sprzedaży, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="52177-161">tooenable hello Azure AD provisioning service for LinkedIn Sales Navigator, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

16) <span data-ttu-id="52177-162">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="52177-162">Click **Save**.</span></span> 

<span data-ttu-id="52177-163">Spowoduje to uruchomienie synchronizacji początkowej hello użytkowników i/lub grupy przypisane tooLinkedIn Nawigator sprzedaży w sekcji hello użytkowników i grup.</span><span class="sxs-lookup"><span data-stu-id="52177-163">This will start hello initial synchronization of any users and/or groups assigned tooLinkedIn Sales Navigator in hello Users and Groups section.</span></span> <span data-ttu-id="52177-164">Należy pamiętać, że synchronizacji początkowej hello potrwa tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello.</span><span class="sxs-lookup"><span data-stu-id="52177-164">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="52177-165">Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie akcje wykonywane przez hello świadczenie usługi w aplikacji LinkedIn sprzedaży nawigatora.</span><span class="sxs-lookup"><span data-stu-id="52177-165">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your LinkedIn Sales Navigator app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="52177-166">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="52177-166">Additional Resources</span></span>

* [<span data-ttu-id="52177-167">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="52177-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="52177-168">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="52177-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
