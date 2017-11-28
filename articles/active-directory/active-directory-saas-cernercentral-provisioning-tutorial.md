---
title: "Samouczek: Konfigurowanie centralnego Cerner dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooautomatically usługi Azure Active Directory tooconfigure obsługi administracyjnej użytkowników tooa spisu w środkowej Cerner."
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
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="0996e-103">Samouczek: Konfigurowanie centralnego Cerner dla użytkownika automatycznego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="0996e-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="0996e-104">Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w środkowej Cerner i usługi Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooa użytkownika spisu w środkowej Cerner.</span><span class="sxs-lookup"><span data-stu-id="0996e-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Cerner Central and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooa user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="0996e-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0996e-105">Prerequisites</span></span>

<span data-ttu-id="0996e-106">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0996e-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="0996e-107">Dzierżawy usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0996e-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="0996e-108">Dzierżawy Cerner środkowe</span><span class="sxs-lookup"><span data-stu-id="0996e-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="0996e-109">Usługa Azure Active Directory integruje się z centralnego Cerner przy użyciu hello [SCIM](http://www.simplecloud.info/) protokołu.</span><span class="sxs-lookup"><span data-stu-id="0996e-109">Azure Active Directory integrates with Cerner Central using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toocerner-central"></a><span data-ttu-id="0996e-110">Przypisywanie użytkowników tooCerner środkowe</span><span class="sxs-lookup"><span data-stu-id="0996e-110">Assigning users tooCerner Central</span></span>

<span data-ttu-id="0996e-111">Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu.</span><span class="sxs-lookup"><span data-stu-id="0996e-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="0996e-112">W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD są synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="0996e-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="0996e-113">Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy podjąć decyzję dotyczącą jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy wymagają dostępu tooCerner centralnego.</span><span class="sxs-lookup"><span data-stu-id="0996e-113">Before configuring and enabling hello provisioning service, you should decide what users and/or groups in Azure AD represent hello users who need access tooCerner Central.</span></span> <span data-ttu-id="0996e-114">Po decyzję, można przypisać tych użytkowników tooCerner centralnego, wykonując instrukcje hello tutaj:</span><span class="sxs-lookup"><span data-stu-id="0996e-114">Once decided, you can assign these users tooCerner Central by following hello instructions here:</span></span>

[<span data-ttu-id="0996e-115">Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan</span><span class="sxs-lookup"><span data-stu-id="0996e-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a><span data-ttu-id="0996e-116">Ważne porady dotyczące przypisywania użytkowników tooCerner środkowe</span><span class="sxs-lookup"><span data-stu-id="0996e-116">Important tips for assigning users tooCerner Central</span></span>

*   <span data-ttu-id="0996e-117">Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać hello centralnej tootest tooCerner inicjowania obsługi konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0996e-117">It is recommended that a single Azure AD user be assigned tooCerner Central tootest hello provisioning configuration.</span></span> <span data-ttu-id="0996e-118">Później można przypisać dodatkowych użytkowników i/lub grup.</span><span class="sxs-lookup"><span data-stu-id="0996e-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="0996e-119">Po zakończeniu testowania początkowej dla pojedynczego użytkownika centralnego Cerner zaleca przypisywanie hello całą listę użytkowników przeznaczonych tooaccess żadnych Cerner rozwiązanie (nie tylko Cerner centralnego) toobe elastycznie tooCerner przez użytkownika spisu.</span><span class="sxs-lookup"><span data-stu-id="0996e-119">Once initial testing is complete for a single user, Cerner Central recommends assigning hello entire list of users intended tooaccess any Cerner solution (not just Cerner Central) toobe provisioned tooCerner’s user roster.</span></span>  <span data-ttu-id="0996e-120">Inne rozwiązania Cerner korzystać z tej listy użytkowników w hello użytkownika spisu.</span><span class="sxs-lookup"><span data-stu-id="0996e-120">Other Cerner solutions leverage this list of users in hello user roster.</span></span>

*   <span data-ttu-id="0996e-121">Podczas przypisywania tooCerner użytkownika środkowe, musisz wybrać hello **użytkownika** roli w oknie dialogowym przydział hello.</span><span class="sxs-lookup"><span data-stu-id="0996e-121">When assigning a user tooCerner Central, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="0996e-122">Użytkownicy z rolą "Domyślnego dostępu" hello są wykluczone z inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="0996e-122">Users with hello "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-toocerner-central"></a><span data-ttu-id="0996e-123">Konfigurowanie inicjowania obsługi administracyjnej tooCerner centralnego użytkownika</span><span class="sxs-lookup"><span data-stu-id="0996e-123">Configuring user provisioning tooCerner Central</span></span>

<span data-ttu-id="0996e-124">Ta sekcja przeprowadzi Cię przez łączenie spisu użytkownika centralnego tooCerner usługi Azure AD przy użyciu konta użytkownika SCIM Cerner przez Inicjowanie obsługi interfejsu API i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz przypisany użytkownik kont w środkowej Cerner oparte na przydziału użytkowników i grup w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0996e-124">This section guides you through connecting your Azure AD tooCerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="0996e-125">Można też tooenabled na języku SAML logowania jednokrotnego dla siedziby Cerner, zgodnie z instrukcjami hello [portalu Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0996e-125">You may also choose tooenabled SAML-based Single Sign-On for Cerner Central, following hello instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="0996e-126">Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, że te dwie funkcje uzupełniają.</span><span class="sxs-lookup"><span data-stu-id="0996e-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="0996e-127">Aby uzyskać więcej informacji, zobacz hello [Cerner centralnego pojedynczego logowania jednokrotnego samouczek](active-directory-saas-cernercentral-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="0996e-127">For more information, see hello [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a><span data-ttu-id="0996e-128">konto użytkownika automatyczne tooconfigure udostępniania tooCerner centralnego w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="0996e-128">tooconfigure automatic user account provisioning tooCerner Central in Azure AD:</span></span>


<span data-ttu-id="0996e-129">W kolejności tooprovision użytkownika konta tooCerner środkowa będzie muszą toorequest konto systemowe centralnego Cerner z Cerner, a Generowanie usługi Azure AD za pomocą punktu końcowego SCIM tooconnect tooCerner tokenu elementu nośnego OAuth.</span><span class="sxs-lookup"><span data-stu-id="0996e-129">In order tooprovision user accounts tooCerner Central, you’ll need toorequest a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use tooconnect tooCerner's SCIM endpoint.</span></span> <span data-ttu-id="0996e-130">Zalecane jest również, że hello integracji można wykonać w środowisku piaskownicy Cerner przed wdrożeniem tooproduction.</span><span class="sxs-lookup"><span data-stu-id="0996e-130">It is also recommended that hello integration be performed in a Cerner sandbox environment before deploying tooproduction.</span></span>

1.  <span data-ttu-id="0996e-131">pierwszym krokiem Hello jest osób hello tooensure Zarządzanie hello Cerner i integracji z usługą Azure AD ma konto CernerCare, która jest wymagana tooaccess hello dokumentacji niezbędne toocomplete hello instrukcje.</span><span class="sxs-lookup"><span data-stu-id="0996e-131">hello first step is tooensure hello people managing hello Cerner and Azure AD integration have a CernerCare account, which is required tooaccess hello documentation necessary toocomplete hello instructions.</span></span> <span data-ttu-id="0996e-132">W razie potrzeby użyj adresów URL hello poniżej toocreate CernerCare kont w każdym środowisku zastosowania.</span><span class="sxs-lookup"><span data-stu-id="0996e-132">If necessary, use hello URLs below toocreate CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="0996e-133">Piaskownicy: https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="0996e-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="0996e-134">Produkcji: https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="0996e-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="0996e-135">Następnie należy utworzyć konta systemu dla usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0996e-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="0996e-136">Skorzystaj z instrukcji hello poniżej toorequest konto systemowe środowiska izolowanego i produkcji.</span><span class="sxs-lookup"><span data-stu-id="0996e-136">Use hello instructions below toorequest a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="0996e-137">Instrukcje: https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="0996e-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="0996e-138">Piaskownicy: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="0996e-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="0996e-139">Produkcji: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="0996e-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="0996e-140">Następnie można wygenerować tokenu elementu nośnego OAuth dla każdego konta użytkownika systemu.</span><span class="sxs-lookup"><span data-stu-id="0996e-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="0996e-141">toodo tego hello wykonaj instrukcje poniżej.</span><span class="sxs-lookup"><span data-stu-id="0996e-141">toodo this, follow hello instructions below.</span></span>

   * <span data-ttu-id="0996e-142">Instrukcje: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="0996e-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="0996e-143">Piaskownicy: https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="0996e-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="0996e-144">Produkcji: https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="0996e-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="0996e-145">Na koniec należy tooacquire identyfikatory obszaru spisu dla obu hello piaskownicy i środowiska produkcyjne w Cerner toocomplete hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0996e-145">Finally, you need tooacquire User Roster Realm IDs for both hello sandbox and production environments in Cerner toocomplete hello configuration.</span></span> <span data-ttu-id="0996e-146">Aby uzyskać informacje na temat tooacquire tego, zobacz: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span><span class="sxs-lookup"><span data-stu-id="0996e-146">For information on how tooacquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="0996e-147">Teraz można skonfigurować tooCerner konta użytkownika tooprovision usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0996e-147">Now you can configure Azure AD tooprovision user accounts tooCerner.</span></span> <span data-ttu-id="0996e-148">Zaloguj się toohello [portalu Azure](https://portal.azure.com)i Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="0996e-148">Sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="0996e-149">Środkowe Cerner został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpienia przy użyciu pola wyszukiwania hello środkowej Cerner.</span><span class="sxs-lookup"><span data-stu-id="0996e-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using hello search field.</span></span> <span data-ttu-id="0996e-150">W przeciwnym razie wybierz **Dodaj** i wyszukaj **centralnego Cerner** w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="0996e-150">Otherwise, select **Add** and search for **Cerner Central** in hello application gallery.</span></span> <span data-ttu-id="0996e-151">Wybierz Cerner centralnego z wyników wyszukiwania hello i dodać tooyour listę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0996e-151">Select Cerner Central from hello search results, and add it tooyour list of applications.</span></span>

7.  <span data-ttu-id="0996e-152">Wybierz wystąpienie Cerner środkowej, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="0996e-152">Select your instance of Cerner Central, then select hello **Provisioning** tab.</span></span>

8.  <span data-ttu-id="0996e-153">Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="0996e-153">Set hello **Provisioning Mode** too**Automatic**.</span></span>

   ![Środkowe Cerner inicjowania obsługi administracyjnej](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="0996e-155">Wypełnij następujące pola w obszarze hello **poświadczeń administratora**:</span><span class="sxs-lookup"><span data-stu-id="0996e-155">Fill in hello following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="0996e-156">W hello **adres URL dzierżawy** wprowadź adres URL w formacie hello poniżej, zastępując "Użytkownik-spisu-obszaru-ID" z Identyfikatorem obszaru hello uzyskaną w kroku #4.</span><span class="sxs-lookup"><span data-stu-id="0996e-156">In hello **Tenant URL** field, enter a URL in hello format below, replacing "User-Roster-Realm-ID" with hello realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="0996e-157">Piaskownicy: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="0996e-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="0996e-158">Produkcji: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="0996e-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="0996e-159">W hello **klucz tajny tokenu** wprowadź token elementu nośnego OAuth hello wygenerowany w kroku #3 i kliknij przycisk **Testuj połączenie**.</span><span class="sxs-lookup"><span data-stu-id="0996e-159">In hello **Secret Token** field, enter hello OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="0996e-160">Powiadomienie Powodzenie powinna zostać wyświetlona po stronie upperright hello portalu usługi.</span><span class="sxs-lookup"><span data-stu-id="0996e-160">You should see a success notification on hello upper­right side of your portal.</span></span>

10. <span data-ttu-id="0996e-161">Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola i zaznacz pole wyboru hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="0996e-161">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

11. <span data-ttu-id="0996e-162">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="0996e-162">Click **Save**.</span></span> 

12. <span data-ttu-id="0996e-163">W hello **mapowań atrybutów** Przejrzyj hello użytkowników i grupy atrybutów toobe synchronizowane z usługi Azure AD tooCerner centralnego.</span><span class="sxs-lookup"><span data-stu-id="0996e-163">In hello **Attribute Mappings** section, review hello user and group attributes toobe synchronized from Azure AD tooCerner Central.</span></span> <span data-ttu-id="0996e-164">Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kont i grup użytkowników w centralnych Cerner dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="0996e-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="0996e-165">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="0996e-165">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="0996e-166">tooenable hello inicjowania obsługi usługi Azure AD dla siedziby Cerner, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji</span><span class="sxs-lookup"><span data-stu-id="0996e-166">tooenable hello Azure AD provisioning service for Cerner Central, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

14. <span data-ttu-id="0996e-167">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="0996e-167">Click **Save**.</span></span> 

<span data-ttu-id="0996e-168">Spowoduje to uruchomienie synchronizacji początkowej hello żadnych użytkowników i/lub grupy przypisane tooCerner centralnego w sekcji hello użytkowników i grup.</span><span class="sxs-lookup"><span data-stu-id="0996e-168">This starts hello initial synchronization of any users and/or groups assigned tooCerner Central in hello Users and Groups section.</span></span> <span data-ttu-id="0996e-169">Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, jak długo działa hello inicjowania obsługi usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0996e-169">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello Azure AD provisioning service is running.</span></span> <span data-ttu-id="0996e-170">Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie akcje wykonywane przez hello świadczenie usługi w aplikacji Cerner centralnego.</span><span class="sxs-lookup"><span data-stu-id="0996e-170">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="0996e-171">Aby uzyskać więcej informacji dotyczących sposobu inicjowania obsługi usługi Azure AD hello tooread logowania, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="0996e-171">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0996e-172">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0996e-172">Additional resources</span></span>

* [<span data-ttu-id="0996e-173">Środkowe Cerner: Publikowania danych tożsamości za pomocą usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0996e-173">Cerner Central: Publishing identity data using Azure AD</span></span>](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [<span data-ttu-id="0996e-174">Samouczek: Konfigurowanie centralnego Cerner na potrzeby rejestracji jednokrotnej z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0996e-174">Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory</span></span>](active-directory-saas-cernercentral-tutorial.md)
* [<span data-ttu-id="0996e-175">Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="0996e-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="0996e-176">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0996e-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="0996e-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0996e-177">Next steps</span></span>
* <span data-ttu-id="0996e-178">[Dowiedz się, jak dzienniki tooreview i get raport dotyczący inicjowania obsługi administracyjnej działania](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="0996e-178">[Learn how tooreview logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
