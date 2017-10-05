---
title: "Samouczek: Konfigurowanie wyszukiwania LinkedIn dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować usługi Azure Active Directory, aby automatycznie zapewnianie i usuwanie kont użytkowników do wyszukiwania LinkedIn."
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
ms.openlocfilehash: 085a68cfe8f9e08b8722e8613994ee300a015776
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-linkedin-lookup-for-automatic-user-provisioning"></a><span data-ttu-id="440b7-103">Samouczek: Konfigurowanie wyszukiwania LinkedIn dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="440b7-103">Tutorial: Configuring LinkedIn Lookup for Automatic User Provisioning</span></span>


<span data-ttu-id="440b7-104">Celem tego samouczka jest opisano czynności, które należy wykonać w wyszukiwania LinkedIn i Azure AD, aby automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD do wyszukiwania LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="440b7-104">The objective of this tutorial is to show you the steps you need to perform in LinkedIn Lookup and Azure AD to automatically provision and de-provision user accounts from Azure AD to LinkedIn Lookup.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="440b7-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="440b7-105">Prerequisites</span></span>

<span data-ttu-id="440b7-106">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="440b7-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="440b7-107">Dzierżawy usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="440b7-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="440b7-108">Dzierżawy LinkedIn wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="440b7-108">A LinkedIn Lookup tenant</span></span> 
*   <span data-ttu-id="440b7-109">Konto administratora wyszukiwania LinkedIn dostęp do Centrum konta LinkedIn</span><span class="sxs-lookup"><span data-stu-id="440b7-109">An administrator account in LinkedIn Lookup with access to the LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="440b7-110">Usługa Azure Active Directory integruje się z LinkedIn wyszukiwania przy użyciu [SCIM](http://www.simplecloud.info/) protokołu.</span><span class="sxs-lookup"><span data-stu-id="440b7-110">Azure Active Directory integrates with LinkedIn Lookup using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-linkedin-lookup"></a><span data-ttu-id="440b7-111">Przypisywanie użytkowników do wyszukiwania LinkedIn</span><span class="sxs-lookup"><span data-stu-id="440b7-111">Assigning users to LinkedIn Lookup</span></span>

<span data-ttu-id="440b7-112">Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="440b7-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="440b7-113">W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD będą synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="440b7-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="440b7-114">Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, należy zdecydować, jakie użytkownicy i/lub grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do wyszukiwania LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="440b7-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to LinkedIn Lookup.</span></span> <span data-ttu-id="440b7-115">Po decyzję, można przypisać tych użytkowników do wyszukiwania LinkedIn, postępując zgodnie z instrukcjami poniżej:</span><span class="sxs-lookup"><span data-stu-id="440b7-115">Once decided, you can assign these users to LinkedIn Lookup by following the instructions here:</span></span>

[<span data-ttu-id="440b7-116">Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie</span><span class="sxs-lookup"><span data-stu-id="440b7-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-lookup"></a><span data-ttu-id="440b7-117">Ważne porady dotyczące przypisywania użytkowników do wyszukiwania LinkedIn</span><span class="sxs-lookup"><span data-stu-id="440b7-117">Important tips for assigning users to LinkedIn Lookup</span></span>

*   <span data-ttu-id="440b7-118">Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać do wyszukiwania LinkedIn do testowania konfiguracji inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="440b7-118">It is recommended that a single Azure AD user be assigned to LinkedIn Lookup to test the provisioning configuration.</span></span> <span data-ttu-id="440b7-119">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="440b7-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="440b7-120">Przypisanie użytkownika do wyszukiwania LinkedIn, należy wybrać **użytkownika** roli w oknie dialogowym przypisania.</span><span class="sxs-lookup"><span data-stu-id="440b7-120">When assigning a user to LinkedIn Lookup, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="440b7-121">Rola "Domyślnego dostępu" nie działa w przypadku inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="440b7-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-linkedin-lookup"></a><span data-ttu-id="440b7-122">Konfigurowanie inicjowania obsługi administracyjnej wyszukiwania LinkedIn użytkownika</span><span class="sxs-lookup"><span data-stu-id="440b7-122">Configuring user provisioning to LinkedIn Lookup</span></span>

<span data-ttu-id="440b7-123">Ta sekcja przeprowadzi Cię przez usługę Azure AD nawiązywania połączenia z kontem użytkownika SCIM LinkedIn wyszukiwania inicjowania obsługi interfejsu API i konfigurowanie usługi inicjowania obsługi administracyjnej do tworzenia, aktualizacji i wyłączyć przypisany użytkownik, który kont w LinkedIn wyszukiwania na podstawie użytkownika i przypisanie do grupy w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="440b7-123">This section guides you through connecting your Azure AD to LinkedIn Lookup's SCIM user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in LinkedIn Lookup based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="440b7-124">Można też włączyć na języku SAML logowania jednokrotnego do wyszukiwania LinkedIn, wykonując instrukcje podane w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="440b7-124">You may also choose to enabled SAML-based Single Sign-On for LinkedIn Lookup, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="440b7-125">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, że te dwie funkcje uzupełniają.</span><span class="sxs-lookup"><span data-stu-id="440b7-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-lookup-in-azure-ad"></a><span data-ttu-id="440b7-126">Aby skonfigurować użytkownika automatyczne Inicjowanie obsługi konta do LinkedIn wyszukiwania w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="440b7-126">To configure automatic user account provisioning to LinkedIn Lookup in Azure AD:</span></span>


<span data-ttu-id="440b7-127">Pierwszym krokiem jest można pobrać tokenu dostępu LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="440b7-127">The first step is to retrieve your LinkedIn access token.</span></span> <span data-ttu-id="440b7-128">Jeśli jesteś administratorem przedsiębiorstwa może samodzielnie inicjować tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="440b7-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="440b7-129">W Centrum konta, przejdź do **ustawienia &gt; ustawienia globalne** , a następnie otwórz **Instalator SCIM** panelu.</span><span class="sxs-lookup"><span data-stu-id="440b7-129">In your account center, go to **Settings &gt; Global Settings** and open the **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="440b7-130">Jeśli uzyskujesz dostęp do Centrum konta bezpośrednio, a nie za pośrednictwem łącza, można osiągnąć go, wykonując następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="440b7-130">If you are accessing the account center directly rather than through a link, you can reach it using the following steps.</span></span>

1)  <span data-ttu-id="440b7-131">Zaloguj się do konta Center.</span><span class="sxs-lookup"><span data-stu-id="440b7-131">Sign in to Account Center.</span></span>

2)  <span data-ttu-id="440b7-132">Wybierz **Admin &gt; ustawienia administratora** .</span><span class="sxs-lookup"><span data-stu-id="440b7-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="440b7-133">Kliknij przycisk **zaawansowane integracji** na lewym pasku bocznym.</span><span class="sxs-lookup"><span data-stu-id="440b7-133">Click **Advanced Integrations** on the left sidebar.</span></span> <span data-ttu-id="440b7-134">Użytkownik jest kierowany do Centrum konta.</span><span class="sxs-lookup"><span data-stu-id="440b7-134">You are directed to the account center.</span></span>

4)  <span data-ttu-id="440b7-135">Kliknij przycisk **+ Dodaj nową konfigurację SCIM** i postępuj zgodnie z procedurą, wypełniając każdego pola.</span><span class="sxs-lookup"><span data-stu-id="440b7-135">Click **+ Add new SCIM configuration** and follow the procedure by filling in each field.</span></span>

> <span data-ttu-id="440b7-136">Autoassign licencji nie jest włączona, oznacza, że tylko dane użytkownika jest synchronizowany.</span><span class="sxs-lookup"><span data-stu-id="440b7-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![Wyszukiwanie LinkedIn inicjowania obsługi administracyjnej](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="440b7-138">Po włączeniu autolicense przypisania musisz Zanotuj wystąpienia aplikacji i typu licencji.</span><span class="sxs-lookup"><span data-stu-id="440b7-138">When auto­license assignment is enabled, you need to note the application instance and license type.</span></span> <span data-ttu-id="440b7-139">Przypisano licencje na pierwszym dostarczanych, najpierw służyć podstawę, dopóki wszystkie licencje są pobierane.</span><span class="sxs-lookup"><span data-stu-id="440b7-139">Licenses are assigned on a first come, first serve basis until all the licenses are taken.</span></span>

![Wyszukiwanie LinkedIn inicjowania obsługi administracyjnej](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="440b7-141">Kliknij przycisk **Generuj token**.</span><span class="sxs-lookup"><span data-stu-id="440b7-141">Click **Generate token**.</span></span> <span data-ttu-id="440b7-142">Powinien zostać wyświetlony ekran tokenu dostępu w obszarze **token dostępu** pola.</span><span class="sxs-lookup"><span data-stu-id="440b7-142">You should see your access token display under the **Access token** field.</span></span>

6)  <span data-ttu-id="440b7-143">Zapisz tokenu dostępu do Schowka lub komputera przed opuszczeniem strony.</span><span class="sxs-lookup"><span data-stu-id="440b7-143">Save your access token to your clipboard or computer before leaving the page.</span></span>

7) <span data-ttu-id="440b7-144">Następnie zaloguj się do [portalu Azure](https://portal.azure.com), a następnie przejdź do **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="440b7-144">Next, sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="440b7-145">LinkedIn wyszukiwania został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpienia LinkedIn wyszukiwania przy użyciu pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="440b7-145">If you have already configured LinkedIn Lookup for single sign-on, search for your instance of LinkedIn Lookup using the search field.</span></span> <span data-ttu-id="440b7-146">W przeciwnym razie wybierz **Dodaj** i wyszukaj **wyszukiwania LinkedIn** w galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="440b7-146">Otherwise, select **Add** and search for **LinkedIn Lookup** in the application gallery.</span></span> <span data-ttu-id="440b7-147">Wybierz wyszukiwania LinkedIn z wyników wyszukiwania i dodaj go do listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="440b7-147">Select LinkedIn Lookup from the search results, and add it to your list of applications.</span></span>

9)  <span data-ttu-id="440b7-148">Wybierz wystąpienia programu LinkedIn wyszukiwania, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="440b7-148">Select your instance of LinkedIn Lookup, then select the **Provisioning** tab.</span></span>

10) <span data-ttu-id="440b7-149">Ustaw **tryb obsługi administracyjnej** do **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="440b7-149">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Wyszukiwanie LinkedIn inicjowania obsługi administracyjnej](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="440b7-151">Wypełnij następujące pola w obszarze **poświadczeń administratora** :</span><span class="sxs-lookup"><span data-stu-id="440b7-151">Fill in the following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="440b7-152">W **adres URL dzierżawy** wprowadź https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="440b7-152">In the **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="440b7-153">W **klucz tajny tokenu** wprowadź token dostępu wygenerowany w kroku 1 i kliknij przycisk **Testuj połączenie** .</span><span class="sxs-lookup"><span data-stu-id="440b7-153">In the **Secret Token** field, enter the access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="440b7-154">Powiadomienie o Powodzenie powinna zostać wyświetlona po stronie upperright portalu usługi.</span><span class="sxs-lookup"><span data-stu-id="440b7-154">You should see a success notification on the upper­right side of   your portal.</span></span>

12) <span data-ttu-id="440b7-155">Wprowadź adres e-mail osoby lub grupy, który powinien zostać wyświetlony inicjowania obsługi administracyjnej powiadomienia o błędach w **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru poniżej.</span><span class="sxs-lookup"><span data-stu-id="440b7-155">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

13) <span data-ttu-id="440b7-156">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="440b7-156">Click **Save**.</span></span> 

14) <span data-ttu-id="440b7-157">W **mapowań atrybutów** Przejrzyj atrybuty użytkowników i grup, które będą synchronizowane z usługi Azure AD można wyszukać LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="440b7-157">In the **Attribute Mappings** section, review the user and group attributes that will be synchronized from Azure AD to LinkedIn Lookup.</span></span> <span data-ttu-id="440b7-158">Należy pamiętać, że atrybuty wybrany jako **pasujące** właściwości, które będą używane do dopasowania kont użytkowników i grup w LinkedIn wyszukiwania dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="440b7-158">Note that the attributes selected as **Matching** properties will be used to match the user accounts and groups in LinkedIn Lookup for update operations.</span></span> <span data-ttu-id="440b7-159">Wybierz przycisk Zapisz, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="440b7-159">Select the Save button to commit any changes.</span></span>

![Wyszukiwanie LinkedIn inicjowania obsługi administracyjnej](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="440b7-161">Aby włączyć usługi Azure AD usługi wyszukiwanie LinkedIn inicjowania obsługi administracyjnej, zmień **stan inicjowania obsługi administracyjnej** do **na** w **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="440b7-161">To enable the Azure AD provisioning service for LinkedIn Lookup, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

16) <span data-ttu-id="440b7-162">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="440b7-162">Click **Save**.</span></span> 

<span data-ttu-id="440b7-163">Spowoduje to uruchomienie synchronizacji początkowej użytkowników i/lub grupy przypisane do wyszukiwania LinkedIn w sekcji Użytkownicy i grupy.</span><span class="sxs-lookup"><span data-stu-id="440b7-163">This will start the initial synchronization of any users and/or groups assigned to LinkedIn Lookup in the Users and Groups section.</span></span> <span data-ttu-id="440b7-164">Należy pamiętać, że synchronizacji początkowej będzie trwać dłużej wykonać niż kolejne synchronizacje, występujące co około 20 minut, tak długo, jak usługa jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="440b7-164">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="440b7-165">Można użyć **szczegóły synchronizacji** sekcji, aby monitorować postęp i skorzystaj z linków do inicjowania obsługi administracyjnej raporty działania, które opisują wszystkie akcje wykonywane przez usługę inicjowania obsługi administracyjnej w aplikacji wyszukiwania LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="440b7-165">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your LinkedIn Lookup app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="440b7-166">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="440b7-166">Additional Resources</span></span>

* [<span data-ttu-id="440b7-167">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="440b7-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="440b7-168">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="440b7-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
