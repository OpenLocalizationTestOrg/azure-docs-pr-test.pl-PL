---
title: "Samouczek: Konfigurowanie centralnego Cerner dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować usługi Azure Active Directory, aby automatycznie udostępnić użytkownikom spisu w środkowej Cerner."
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: 84613b7f8d7bd031d492a62da0bc53be96ac45a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="d128e-103">Samouczek: Konfigurowanie centralnego Cerner dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="d128e-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="d128e-104">Celem tego samouczka jest opisano czynności, które należy wykonać w środkowej Cerner i usługi Azure AD, aby automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD do spisu użytkownika, Indie środkowe Cerner.</span><span class="sxs-lookup"><span data-stu-id="d128e-104">The objective of this tutorial is to show you the steps you need to perform in Cerner Central and Azure AD to automatically provision and de-provision user accounts from Azure AD to a user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="d128e-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d128e-105">Prerequisites</span></span>

<span data-ttu-id="d128e-106">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d128e-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="d128e-107">Dzierżawy usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d128e-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="d128e-108">Dzierżawy Cerner środkowe</span><span class="sxs-lookup"><span data-stu-id="d128e-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="d128e-109">Usługa Azure Active Directory integruje się z centralnego Cerner przy użyciu [SCIM](http://www.simplecloud.info/) protokołu.</span><span class="sxs-lookup"><span data-stu-id="d128e-109">Azure Active Directory integrates with Cerner Central using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-cerner-central"></a><span data-ttu-id="d128e-110">Przypisywanie użytkowników do centralnego Cerner</span><span class="sxs-lookup"><span data-stu-id="d128e-110">Assigning users to Cerner Central</span></span>

<span data-ttu-id="d128e-111">Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d128e-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="d128e-112">W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD są synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="d128e-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="d128e-113">Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, należy podjąć decyzję dotyczącą jakie użytkowników i/lub grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do centralnego Cerner.</span><span class="sxs-lookup"><span data-stu-id="d128e-113">Before configuring and enabling the provisioning service, you should decide what users and/or groups in Azure AD represent the users who need access to Cerner Central.</span></span> <span data-ttu-id="d128e-114">Po decyzję, można przypisać tych użytkowników do centralnego Cerner, postępując zgodnie z instrukcjami poniżej:</span><span class="sxs-lookup"><span data-stu-id="d128e-114">Once decided, you can assign these users to Cerner Central by following the instructions here:</span></span>

[<span data-ttu-id="d128e-115">Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie</span><span class="sxs-lookup"><span data-stu-id="d128e-115">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-cerner-central"></a><span data-ttu-id="d128e-116">Ważne porady dotyczące przypisywania użytkowników do centralnego Cerner</span><span class="sxs-lookup"><span data-stu-id="d128e-116">Important tips for assigning users to Cerner Central</span></span>

*   <span data-ttu-id="d128e-117">Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać do centralnego Cerner do testowania konfiguracji inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="d128e-117">It is recommended that a single Azure AD user be assigned to Cerner Central to test the provisioning configuration.</span></span> <span data-ttu-id="d128e-118">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="d128e-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="d128e-119">Po zakończeniu testowania początkowej dla pojedynczego użytkownika centralnego Cerner zaleca przypisywanie całą listę użytkownicy mają dostęp do wszelkich rozwiązań Cerner (nie tylko Cerner centralnego) być przygotowana do Cerner przez użytkownika spisu.</span><span class="sxs-lookup"><span data-stu-id="d128e-119">Once initial testing is complete for a single user, Cerner Central recommends assigning the entire list of users intended to access any Cerner solution (not just Cerner Central) to be provisioned to Cerner’s user roster.</span></span>  <span data-ttu-id="d128e-120">Inne rozwiązania Cerner korzystać z tej listy użytkowników w spisu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d128e-120">Other Cerner solutions leverage this list of users in the user roster.</span></span>

*   <span data-ttu-id="d128e-121">Przypisanie użytkownika do centralnego Cerner, należy wybrać **użytkownika** roli w oknie dialogowym przypisania.</span><span class="sxs-lookup"><span data-stu-id="d128e-121">When assigning a user to Cerner Central, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="d128e-122">Użytkownicy z rolą "Domyślnego dostępu" są wykluczone z inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="d128e-122">Users with the "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-to-cerner-central"></a><span data-ttu-id="d128e-123">Konfigurowanie do centralnego Cerner Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="d128e-123">Configuring user provisioning to Cerner Central</span></span>

<span data-ttu-id="d128e-124">Ta sekcja przeprowadzi użytkownika przez łączenie usługi Azure AD z centralnego Cerner spisu użytkownika przy użyciu konta użytkownika SCIM Cerner przez Inicjowanie obsługi interfejsu API i konfigurowanie inicjowania obsługi usługi do tworzenia, aktualizacji i wyłączania przypisany użytkownik, na podstawie kont w środkowej Cerner Przypisywanie użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d128e-124">This section guides you through connecting your Azure AD to Cerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="d128e-125">Można też włączyć na języku SAML logowania jednokrotnego dla siedziby Cerner, zgodnie z instrukcjami podanymi w [portalu Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d128e-125">You may also choose to enabled SAML-based Single Sign-On for Cerner Central, following the instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="d128e-126">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, że te dwie funkcje uzupełniają.</span><span class="sxs-lookup"><span data-stu-id="d128e-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="d128e-127">Aby uzyskać więcej informacji, zobacz [Cerner centralnego pojedynczego logowania jednokrotnego samouczek](active-directory-saas-cernercentral-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="d128e-127">For more information, see the [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-cerner-central-in-azure-ad"></a><span data-ttu-id="d128e-128">Aby skonfigurować użytkownika automatyczne Inicjowanie obsługi konta do centralnego Cerner w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="d128e-128">To configure automatic user account provisioning to Cerner Central in Azure AD:</span></span>


<span data-ttu-id="d128e-129">Aby udostępnić konta użytkowników do centralnego Cerner, należy poprosić konta systemu centralnego Cerner Cerner oraz do generowania tokenu elementu nośnego OAuth używanego przez usługi Azure AD do nawiązania połączenia przez Cerner SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="d128e-129">In order to provision user accounts to Cerner Central, you’ll need to request a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use to connect to Cerner's SCIM endpoint.</span></span> <span data-ttu-id="d128e-130">Zalecane jest również, że integracji można wykonać w środowisku piaskownicy Cerner przed wdrożeniem w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="d128e-130">It is also recommended that the integration be performed in a Cerner sandbox environment before deploying to production.</span></span>

1.  <span data-ttu-id="d128e-131">Pierwszym krokiem jest zapewnienie osobom Zarządzanie Cerner i integracji z usługą Azure AD ma konto CernerCare, co jest wymagane, aby uzyskać dostęp do dokumentacji, które należy wykonać instrukcje.</span><span class="sxs-lookup"><span data-stu-id="d128e-131">The first step is to ensure the people managing the Cerner and Azure AD integration have a CernerCare account, which is required to access the documentation necessary to complete the instructions.</span></span> <span data-ttu-id="d128e-132">Jeśli to konieczne, umożliwiają utworzenie kont CernerCare w każdym środowisku dotyczy poniżej adresy URL.</span><span class="sxs-lookup"><span data-stu-id="d128e-132">If necessary, use the URLs below to create CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="d128e-133">Piaskownicy: https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="d128e-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="d128e-134">Produkcji: https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="d128e-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="d128e-135">Następnie należy utworzyć konta systemu dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d128e-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="d128e-136">Poniższe instrukcje umożliwiają żądania konto systemowe dla środowiska izolowanego i produkcji.</span><span class="sxs-lookup"><span data-stu-id="d128e-136">Use the instructions below to request a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="d128e-137">Instrukcje: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="d128e-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="d128e-138">Piaskownicy: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="d128e-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="d128e-139">Produkcji: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="d128e-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="d128e-140">Następnie można wygenerować tokenu elementu nośnego OAuth dla każdego konta użytkownika systemu.</span><span class="sxs-lookup"><span data-stu-id="d128e-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="d128e-141">Aby to zrobić, postępuj zgodnie z poniższymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="d128e-141">To do this, follow the instructions below.</span></span>

   * <span data-ttu-id="d128e-142">Instrukcje: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="d128e-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="d128e-143">Piaskownicy: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="d128e-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="d128e-144">Produkcji: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="d128e-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="d128e-145">Na koniec należy uzyskać identyfikatory obszaru spisu użytkownika dla środowisk zarówno piaskownicy, jak i produkcji w Cerner, aby zakończyć konfigurację.</span><span class="sxs-lookup"><span data-stu-id="d128e-145">Finally, you need to acquire User Roster Realm IDs for both the sandbox and production environments in Cerner to complete the configuration.</span></span> <span data-ttu-id="d128e-146">Aby uzyskać informacje dotyczące sposobu uzyskania to, zobacz: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span><span class="sxs-lookup"><span data-stu-id="d128e-146">For information on how to acquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="d128e-147">Teraz można skonfigurować usługi Azure AD do kont użytkowników należy Cerner.</span><span class="sxs-lookup"><span data-stu-id="d128e-147">Now you can configure Azure AD to provision user accounts to Cerner.</span></span> <span data-ttu-id="d128e-148">Zaloguj się do [portalu Azure](https://portal.azure.com), a następnie przejdź do **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="d128e-148">Sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="d128e-149">Środkowe Cerner został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpienia środkowej Cerner przy użyciu pola wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="d128e-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using the search field.</span></span> <span data-ttu-id="d128e-150">W przeciwnym razie wybierz **Dodaj** i wyszukaj **centralnego Cerner** w galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d128e-150">Otherwise, select **Add** and search for **Cerner Central** in the application gallery.</span></span> <span data-ttu-id="d128e-151">Wybierz Cerner centralnego w wynikach wyszukiwania i dodaj ją do listy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d128e-151">Select Cerner Central from the search results, and add it to your list of applications.</span></span>

7.  <span data-ttu-id="d128e-152">Wybierz wystąpienie Cerner środkowej, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="d128e-152">Select your instance of Cerner Central, then select the **Provisioning** tab.</span></span>

8.  <span data-ttu-id="d128e-153">Ustaw **tryb obsługi administracyjnej** do **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="d128e-153">Set the **Provisioning Mode** to **Automatic**.</span></span>

   ![Środkowe Cerner inicjowania obsługi administracyjnej](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="d128e-155">Wypełnij następujące pola w obszarze **poświadczeń administratora**:</span><span class="sxs-lookup"><span data-stu-id="d128e-155">Fill in the following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="d128e-156">W **adres URL dzierżawy** wprowadź adres URL w formacie poniżej, zastępując "Użytkownik-spisu-obszaru-ID" z Identyfikatorem obszaru uzyskaną w kroku #4.</span><span class="sxs-lookup"><span data-stu-id="d128e-156">In the **Tenant URL** field, enter a URL in the format below, replacing "User-Roster-Realm-ID" with the realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="d128e-157">Piaskownicy: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="d128e-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="d128e-158">Produkcji: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="d128e-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="d128e-159">W **klucz tajny tokenu** wprowadź token elementu nośnego OAuth wygenerowany w kroku #3 i kliknij przycisk **Testuj połączenie**.</span><span class="sxs-lookup"><span data-stu-id="d128e-159">In the **Secret Token** field, enter the OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="d128e-160">Powiadomienie o Powodzenie powinna zostać wyświetlona po stronie upperright portalu usługi.</span><span class="sxs-lookup"><span data-stu-id="d128e-160">You should see a success notification on the upper­right side of your portal.</span></span>

10. <span data-ttu-id="d128e-161">Wprowadź adres e-mail osoby lub grupy, który powinien zostać wyświetlony inicjowania obsługi administracyjnej powiadomienia o błędach w **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru poniżej.</span><span class="sxs-lookup"><span data-stu-id="d128e-161">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

11. <span data-ttu-id="d128e-162">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d128e-162">Click **Save**.</span></span> 

12. <span data-ttu-id="d128e-163">W **mapowań atrybutów** Przejrzyj atrybuty użytkowników i grup, które mają być synchronizowane z usługi Azure AD do centralnego Cerner.</span><span class="sxs-lookup"><span data-stu-id="d128e-163">In the **Attribute Mappings** section, review the user and group attributes to be synchronized from Azure AD to Cerner Central.</span></span> <span data-ttu-id="d128e-164">Atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania kont użytkowników i grup w środkowej Cerner dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="d128e-164">The attributes selected as **Matching** properties are used to match the user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="d128e-165">Wybierz przycisk Zapisz, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="d128e-165">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="d128e-166">Aby włączyć usługi Azure AD usługi dla siedziby Cerner inicjowania obsługi administracyjnej, zmień **stan inicjowania obsługi administracyjnej** do **na** w **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="d128e-166">To enable the Azure AD provisioning service for Cerner Central, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

14. <span data-ttu-id="d128e-167">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d128e-167">Click **Save**.</span></span> 

<span data-ttu-id="d128e-168">Spowoduje to uruchomienie synchronizacji początkowej użytkowników i/lub grupy przypisane do centralnego Cerner w sekcji Użytkownicy i grupy.</span><span class="sxs-lookup"><span data-stu-id="d128e-168">This starts the initial synchronization of any users and/or groups assigned to Cerner Central in the Users and Groups section.</span></span> <span data-ttu-id="d128e-169">Synchronizacji początkowej zajmuje więcej czasu wykonywania niż kolejne synchronizacje, występujące co około 20 minut, jak długo działa usługi Azure AD, inicjowania obsługi usługi.</span><span class="sxs-lookup"><span data-stu-id="d128e-169">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="d128e-170">Można użyć **szczegóły synchronizacji** sekcji, aby monitorować postęp i skorzystaj z linków do inicjowania obsługi administracyjnej raporty działania, które opisują wszystkie akcje wykonywane przez usługę inicjowania obsługi administracyjnej w aplikacji Cerner centralnego.</span><span class="sxs-lookup"><span data-stu-id="d128e-170">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="d128e-171">Aby uzyskać więcej informacji na temat usługi Azure AD, inicjowanie obsługi dzienników do odczytu, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="d128e-171">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d128e-172">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d128e-172">Additional resources</span></span>

* [<span data-ttu-id="d128e-173">Środkowe Cerner: Publikowania danych tożsamości za pomocą usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d128e-173">Cerner Central: Publishing identity data using Azure AD</span></span>](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [<span data-ttu-id="d128e-174">Samouczek: Konfigurowanie centralnego Cerner na potrzeby rejestracji jednokrotnej z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d128e-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="d128e-175">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="d128e-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="d128e-176">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d128e-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="d128e-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d128e-177">Next steps</span></span>
* <span data-ttu-id="d128e-178">[Dowiedz się, jak należy przejrzeć dzienniki i Uzyskaj raporty dotyczące inicjowania obsługi administracyjnej działania](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="d128e-178">[Learn how to review logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
