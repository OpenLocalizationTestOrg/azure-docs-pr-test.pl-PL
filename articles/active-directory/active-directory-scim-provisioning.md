---
title: "aaaUsing systemu do zarządzania tożsamościami międzydomenowego automatycznej aprowizacji użytkowników i grup z usługi Azure Active Directory tooapplications | Dokumentacja firmy Microsoft"
description: "Usługa Azure Active Directory mogą automatycznie obsługiwać użytkowników i grup tooany aplikacji lub tożsamości sklepu, która jest fronted przez usługę sieci web z interfejsem hello zdefiniowane w hello Specyfikacja protokołu SCIM"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a><span data-ttu-id="6b328-103">Zarządzanie tożsamościami międzydomenowego tooautomatically udostępniania użytkowników i grup z usługi Azure Active Directory tooapplications przy użyciu systemu</span><span class="sxs-lookup"><span data-stu-id="6b328-103">Using System for Cross-Domain Identity Management tooautomatically provision users and groups from Azure Active Directory tooapplications</span></span>

## <a name="overview"></a><span data-ttu-id="6b328-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6b328-104">Overview</span></span>
<span data-ttu-id="6b328-105">Azure Active Directory (Azure AD), mogą automatycznie obsługiwać użytkowników i grup tooany aplikacji lub tożsamości sklepu, która jest fronted przez usługę sieci web z interfejsem hello zdefiniowane w hello [systemu do innej domeny zarządzania tożsamości (SCIM) 2.0 Specyfikacja protokołu](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="6b328-105">Azure Active Directory (Azure AD) can automatically provision users and groups tooany application or identity store that is fronted by a web service with hello interface defined in hello [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="6b328-106">Usługa Azure Active Directory można wysłać żądania toocreate, zmodyfikować lub usunąć przypisanych użytkowników i grup usługi toohello w sieci web.</span><span class="sxs-lookup"><span data-stu-id="6b328-106">Azure Active Directory can send requests toocreate, modify, or delete assigned users and groups toohello web service.</span></span> <span data-ttu-id="6b328-107">usługi sieci web Hello może dokonywać translacji te żądania na operacje na magazynu tożsamości hello docelowego.</span><span class="sxs-lookup"><span data-stu-id="6b328-107">hello web service can then translate those requests into operations on hello target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6b328-108">Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="6b328-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="6b328-109">![][0]
*Rysunek 1: Inicjowanie obsługi administracyjnej z magazynu tożsamości tooan usługi Azure Active Directory za pośrednictwem usługi sieci web*</span><span class="sxs-lookup"><span data-stu-id="6b328-109">![][0]
*Figure 1: Provisioning from Azure Active Directory tooan identity store via a web service*</span></span>

<span data-ttu-id="6b328-110">Ta możliwość może służyć w połączeniu z możliwością "bring własną aplikację" hello, w usłudze Azure AD tooenable rejestracji jednokrotnej i użytkownika automatyczne Inicjowanie obsługi administracyjnej dla aplikacji, które zapewniają lub są fronted przez usługę sieci web SCIM.</span><span class="sxs-lookup"><span data-stu-id="6b328-110">This capability can be used in conjunction with hello “bring your own app” capability in Azure AD tooenable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="6b328-111">Istnieją dwa przypadki użycia przy użyciu SCIM w usłudze Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="6b328-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="6b328-112">**Inicjowanie obsługi użytkowników i grup tooapplications, która obsługuje SCIM** aplikacji, które obsługują SCIM 2.0 i używają tokenów elementu nośnego OAuth dla działania uwierzytelniania w usłudze Azure AD bez konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6b328-112">**Provisioning users and groups tooapplications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="6b328-113">**Skompiluj rozwiązanie inicjowania obsługi administracyjnej dla aplikacji, które obsługę innych oparty na interfejsach API** dla aplikacji z systemem innym niż SCIM, można utworzyć tootranslate punktu końcowego SCIM między punktu końcowego usługi Azure AD SCIM hello i wszelkie obsługuje aplikacji hello interfejsu API do inicjowania obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6b328-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint tootranslate between hello Azure AD SCIM endpoint and any API hello application supports for user provisioning.</span></span> <span data-ttu-id="6b328-114">Tworzenie punktu końcowego SCIM toohelp, udostępniamy infrastruktury języka wspólnego (CLI) bibliotek oraz przykłady kodu, przedstawiających sposób toodo Podaj punkt końcowy SCIM i tłumaczenie SCIM wiadomości.</span><span class="sxs-lookup"><span data-stu-id="6b328-114">toohelp you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how toodo provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a><span data-ttu-id="6b328-115">Inicjowanie obsługi administracyjnej użytkowników i grup tooapplications, która obsługuje SCIM</span><span class="sxs-lookup"><span data-stu-id="6b328-115">Provisioning users and groups tooapplications that support SCIM</span></span>
<span data-ttu-id="6b328-116">Usługi Azure AD może być skonfigurowany tooautomatically należy przypisać użytkowników i grup tooapplications który implementuje [systemu do zarządzania tożsamościami międzydomenowego 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) usługi sieci web i zaakceptować tokenów elementu nośnego OAuth dla uwierzytelniania .</span><span class="sxs-lookup"><span data-stu-id="6b328-116">Azure AD can be configured tooautomatically provision assigned users and groups tooapplications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="6b328-117">W specyfikacji hello SCIM 2.0 aplikacji musi spełniać następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="6b328-117">Within hello SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="6b328-118">Obsługuje tworzenie użytkowników i grupy, zgodnie z sekcji 3.3 hello SCIM protokołu.</span><span class="sxs-lookup"><span data-stu-id="6b328-118">Supports creating users and/or groups, as per section 3.3 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="6b328-119">Obsługa modyfikowania użytkowników i/lub grup z żądaniami poprawki zgodnie z sekcji 3.5.2 hello SCIM protokołu.</span><span class="sxs-lookup"><span data-stu-id="6b328-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="6b328-120">Obsługuje pobieranie znanych zasobów zgodnie z sekcji 3.4.1 hello SCIM protokołu.</span><span class="sxs-lookup"><span data-stu-id="6b328-120">Supports retrieving a known resource as per section 3.4.1 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="6b328-121">Obsługa zapytań użytkowników i grupy, zgodnie z sekcji 3.4.2 hello SCIM protokołu.</span><span class="sxs-lookup"><span data-stu-id="6b328-121">Supports querying users and/or groups, as per section 3.4.2 of hello SCIM protocol.</span></span>  <span data-ttu-id="6b328-122">Domyślnie użytkownicy są proszeni przez externalId i grup są żądanych przez Nazwa wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="6b328-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="6b328-123">Obsługa zapytań użytkownika według Identyfikatora i przez Menedżera zgodnie z sekcji 3.4.2 hello SCIM protokołu.</span><span class="sxs-lookup"><span data-stu-id="6b328-123">Supports querying user by ID and by manager as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="6b328-124">Obsługa zapytań grup według Identyfikatora i przez członka zgodnie z sekcji 3.4.2 hello SCIM protokołu.</span><span class="sxs-lookup"><span data-stu-id="6b328-124">Supports querying groups by ID and by member as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="6b328-125">Akceptuje tokenów elementu nośnego OAuth dla autoryzacji zgodnie z sekcji 2.1 hello SCIM protokołu.</span><span class="sxs-lookup"><span data-stu-id="6b328-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of hello SCIM protocol.</span></span>

<span data-ttu-id="6b328-126">Skontaktuj się z dostawcą aplikacji lub dokumentacji dostawcy aplikacji dla instrukcji zgodność z tych wymagań.</span><span class="sxs-lookup"><span data-stu-id="6b328-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="6b328-127">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="6b328-127">Getting started</span></span>
<span data-ttu-id="6b328-128">Aplikacje, które obsługują profilu SCIM hello opisane w tym artykule może być tooAzure podłączonej usługi Active Directory za pomocą funkcji hello "z systemem innym niż galerii aplikacji" w galerii aplikacji hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b328-128">Applications that support hello SCIM profile described in this article can be connected tooAzure Active Directory using hello "non-gallery application" feature in hello Azure AD application gallery.</span></span> <span data-ttu-id="6b328-129">Po uruchomieniu połączone, Azure AD proces synchronizacji co 20 minut, gdy wysyła zapytanie punktu końcowego SCIM aplikacji hello przypisanych użytkowników i grup i tworzy lub modyfikuje je zgodnie z toohello Szczegóły przypisania.</span><span class="sxs-lookup"><span data-stu-id="6b328-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries hello application's SCIM endpoint for assigned users and groups, and creates or modifies them according toohello assignment details.</span></span>

<span data-ttu-id="6b328-130">**tooconnect aplikacji, która obsługuje SCIM:**</span><span class="sxs-lookup"><span data-stu-id="6b328-130">**tooconnect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="6b328-131">Zaloguj się za[hello portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6b328-131">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="6b328-132">Przeglądaj zbyt ** usługi Azure Active Directory > aplikacje dla przedsiębiorstw, a następnie wybierz **nowej aplikacji > wszystkie > Non galerii aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="6b328-132">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="6b328-133">Wprowadź nazwę aplikacji, a następnie kliknij przycisk **Dodaj** toocreate ikona obiektu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6b328-133">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span>
    
  <span data-ttu-id="6b328-134">![][1]
  *Rysunek 2: Galerii aplikacji usługi Azure AD*</span><span class="sxs-lookup"><span data-stu-id="6b328-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="6b328-135">Na ekranie wynikowy hello wybierz hello **inicjowania obsługi administracyjnej** kartę w lewej kolumnie hello.</span><span class="sxs-lookup"><span data-stu-id="6b328-135">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="6b328-136">W hello **inicjowania obsługi trybu** menu, wybierz opcję **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="6b328-136">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="6b328-137">![][2]
  *Rysunek 3: Konfigurowanie inicjowania obsługi w hello portalu Azure*</span><span class="sxs-lookup"><span data-stu-id="6b328-137">![][2]
*Figure 3: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="6b328-138">W hello **adres URL dzierżawy** wprowadź adres URL punktu końcowego SCIM aplikacji hello hello.</span><span class="sxs-lookup"><span data-stu-id="6b328-138">In hello **Tenant URL** field, enter hello URL of hello application's SCIM endpoint.</span></span> <span data-ttu-id="6b328-139">Przykład: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="6b328-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="6b328-140">Jeśli punkt końcowy SCIM hello wymaga tokenu elementu nośnego OAuth od wystawcy innego niż Azure AD, a następnie hello kopiowania wymagany token elementu nośnego OAuth do hello opcjonalne **klucz tajny tokenu** pola.</span><span class="sxs-lookup"><span data-stu-id="6b328-140">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="6b328-141">Jeśli to pole pozostanie puste, usługi Azure AD uwzględnione tokenu elementu nośnego OAuth wystawione przez usługi Azure AD z każdym żądaniem.</span><span class="sxs-lookup"><span data-stu-id="6b328-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="6b328-142">Aplikacje, które używają usługi Azure AD jako dostawca tożsamości może sprawdzić poprawność tej usługi Azure AD-wystawiony token.</span><span class="sxs-lookup"><span data-stu-id="6b328-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="6b328-143">Kliknij przycisk hello **Testuj połączenie** przycisk toohave usługi Azure Active Directory próba tooconnect toohello SCIM punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="6b328-143">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="6b328-144">W przypadku awarii próby hello, wyświetlane informacje o błędzie.</span><span class="sxs-lookup"><span data-stu-id="6b328-144">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="6b328-145">W przypadku powodzenia hello prób tooconnect toohello aplikacji, następnie kliknij przycisk **zapisać** poświadczeń administratora hello toosave.</span><span class="sxs-lookup"><span data-stu-id="6b328-145">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="6b328-146">W hello **mapowania** sekcji, istnieją dwa zestawy wybieranych mapowań atrybutów: jeden dla obiektów użytkownika i jeden dla obiektów grupy.</span><span class="sxs-lookup"><span data-stu-id="6b328-146">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="6b328-147">Wybierz każdego jeden atrybuty hello tooreview, które są synchronizowane z usługą Azure Active Directory tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6b328-147">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="6b328-148">Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello użytkowników i grup w aplikacji dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="6b328-148">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="6b328-149">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="6b328-149">Select hello Save button toocommit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="6b328-150">Opcjonalnie możesz wyłączyć synchronizację obiektów grupy przez wyłączenie hello "grupy" mapowania.</span><span class="sxs-lookup"><span data-stu-id="6b328-150">You can optionally disable syncing of group objects by disabling hello "groups" mapping.</span></span> 

11. <span data-ttu-id="6b328-151">W obszarze **ustawienia**, hello **zakres** pola definiuje, które użytkownicy i grupy są synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="6b328-151">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="6b328-152">Wybieranie "Synchronizacji tylko przypisane użytkowników i grup" (zalecane) zsynchronizuje tylko użytkownicy i grupy przypisane w hello **użytkowników i grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="6b328-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="6b328-153">Po zakończeniu konfiguracji zmienić hello **stan inicjowania obsługi administracyjnej** za**na**.</span><span class="sxs-lookup"><span data-stu-id="6b328-153">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="6b328-154">Kliknij przycisk **zapisać** toostart hello inicjowania obsługi usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b328-154">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="6b328-155">Przydzielenia synchronizowanie tylko użytkownicy i grupy (zalecane), należy się hello tooselect **użytkowników i grup** karcie i przypisz hello użytkowników i/lub grup, które chcesz toosync.</span><span class="sxs-lookup"><span data-stu-id="6b328-155">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="6b328-156">Po rozpoczęciu hello wstępnej synchronizacji, można użyć hello **dzienniki inspekcji** karcie postępu toomonitor, który zawiera wszystkie akcje wykonywane przez hello świadczenie usługi w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6b328-156">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="6b328-157">Aby uzyskać więcej informacji dotyczących sposobu inicjowania obsługi usługi Azure AD hello tooread logowania, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="6b328-157">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="6b328-158">Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello.</span><span class="sxs-lookup"><span data-stu-id="6b328-158">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="6b328-159">Tworzenie rozwiązania inicjowania obsługi administracyjnej dla dowolnej aplikacji</span><span class="sxs-lookup"><span data-stu-id="6b328-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="6b328-160">Tworząc interfejsy usługi sieci web SCIM z usługi Azure Active Directory, można włączyć pojedynczego użytkownika logowania jednokrotnego i automatyczne Inicjowanie obsługi praktycznie dowolnej aplikacji, która zawiera użytkownika inicjowania obsługi interfejsu API REST lub protokołu SOAP.</span><span class="sxs-lookup"><span data-stu-id="6b328-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="6b328-161">Oto jak to działa:</span><span class="sxs-lookup"><span data-stu-id="6b328-161">Here’s how it works:</span></span>

1. <span data-ttu-id="6b328-162">Usługa Azure AD zapewnia o nazwie biblioteki wspólnej infrastruktury języka [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="6b328-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="6b328-163">Deweloperów i integratorów systemów. platforma można użyć tej biblioteki toocreate i wdrożyć punkt końcowy usługi sieci web opartych na SCIM może nawiązywać połączenia magazynu tożsamości aplikacji tooany usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b328-163">System integrators and developers can use this library toocreate and deploy a SCIM-based web service endpoint capable of connecting Azure AD tooany application’s identity store.</span></span>
2. <span data-ttu-id="6b328-164">Mapowania są implementowane w hello sieci web usługi toomap hello standardowych użytkowników schematu toohello użytkowników schematu i wymagane przez aplikację hello protokołu.</span><span class="sxs-lookup"><span data-stu-id="6b328-164">Mappings are implemented in hello web service toomap hello standardized user schema toohello user schema and protocol required by hello application.</span></span>
3. <span data-ttu-id="6b328-165">adres URL punktu końcowego Hello jest zarejestrowany w usłudze Azure AD w ramach niestandardowych aplikacji w galerii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6b328-165">hello endpoint URL is registered in Azure AD as part of a custom application in hello application gallery.</span></span>
4. <span data-ttu-id="6b328-166">Użytkownicy i grupy są przypisywane toothis aplikacji w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b328-166">Users and groups are assigned toothis application in Azure AD.</span></span> <span data-ttu-id="6b328-167">Po przypisania są umieszczane w aplikacji docelowej toohello toobe synchronizowane kolejki.</span><span class="sxs-lookup"><span data-stu-id="6b328-167">Upon assignment, they are put into a queue toobe synchronized toohello target application.</span></span> <span data-ttu-id="6b328-168">proces synchronizacji Hello obsługi kolejki hello jest uruchamiana co 20 minut.</span><span class="sxs-lookup"><span data-stu-id="6b328-168">hello synchronization process handling hello queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="6b328-169">Przykłady kodu</span><span class="sxs-lookup"><span data-stu-id="6b328-169">Code Samples</span></span>
<span data-ttu-id="6b328-170">toomake to przetwarzanie łatwiej, grupy [przykłady kodu](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) pod warunkiem że utworzyć SCIM punkt końcowy usługi sieci web i Wykaż, automatyczne udostępnianie.</span><span class="sxs-lookup"><span data-stu-id="6b328-170">toomake this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="6b328-171">Przykład jest dostawcy, który przechowuje plik z wierszami z wartościami rozdzielonymi przecinkami reprezentująca użytkowników i grup.</span><span class="sxs-lookup"><span data-stu-id="6b328-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="6b328-172">jest Hello innego dostawcy, który działa na powitania usługi Amazon Web Services tożsamość i zarządzanie dostępem.</span><span class="sxs-lookup"><span data-stu-id="6b328-172">hello other is of a provider that operates on hello Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="6b328-173">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="6b328-173">**Prerequisites**</span></span>

* <span data-ttu-id="6b328-174">Visual Studio 2013 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="6b328-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="6b328-175">Zestaw Azure SDK dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="6b328-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="6b328-176">Urządzenia z systemem Windows, które obsługuje hello ASP.NET framework 4.5 toobe używane jako hello SCIM punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="6b328-176">Windows machine that supports hello ASP.NET framework 4.5 toobe used as hello SCIM endpoint.</span></span> <span data-ttu-id="6b328-177">Tego komputera muszą być dostępne z chmury hello</span><span class="sxs-lookup"><span data-stu-id="6b328-177">This machine must be accessible from hello cloud</span></span>
* [<span data-ttu-id="6b328-178">Subskrypcja platformy Azure w wersji próbnej lub licencjonowanej wersji programu Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="6b328-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="6b328-179">przykład Amazon AWS Hello wymaga bibliotek hello [usług AWS narzędzi dla programu Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span><span class="sxs-lookup"><span data-stu-id="6b328-179">hello Amazon AWS sample requires libraries from hello [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="6b328-180">Aby uzyskać więcej informacji, zobacz plik README hello pliku dołączonego hello próbki.</span><span class="sxs-lookup"><span data-stu-id="6b328-180">For more information, see hello README file included with hello sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="6b328-181">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="6b328-181">Getting Started</span></span>
<span data-ttu-id="6b328-182">Witaj Najprostszym sposobem tooimplement SCIM punktu końcowego, który może zaakceptować inicjowania obsługi żądań z usługi Azure AD jest toobuild i wdrażanie hello przykładowy kod, który plik wartości rozdzielanych przecinkami (CSV) tooa użytkowników elastycznie hello.</span><span class="sxs-lookup"><span data-stu-id="6b328-182">hello easiest way tooimplement a SCIM endpoint that can accept provisioning requests from Azure AD is toobuild and deploy hello code sample that outputs hello provisioned users tooa comma-separated value (CSV) file.</span></span>

<span data-ttu-id="6b328-183">**toocreate punktu końcowego SCIM próbki:**</span><span class="sxs-lookup"><span data-stu-id="6b328-183">**toocreate a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="6b328-184">Pobierz przykładowy kod hello na [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="6b328-184">Download hello code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="6b328-185">Rozpakuj pakiet hello i umieść go na komputerze z systemem Windows w lokalizacji, takich jak C:\AzureAD-BYOA-Provisioning-Samples\.</span><span class="sxs-lookup"><span data-stu-id="6b328-185">Unzip hello package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="6b328-186">W tym folderze uruchom program hello FileProvisioningAgent rozwiązania w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b328-186">In this folder, launch hello FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="6b328-187">Wybierz **Narzędzia > Menedżer pakietów biblioteki > konsoli Menedżera pakietów**i wykonaj następujące polecenia dotyczące hello FileProvisioningAgent tooresolve hello rozwiązania odwołania hello:</span><span class="sxs-lookup"><span data-stu-id="6b328-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute hello following commands for hello FileProvisioningAgent project tooresolve hello solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="6b328-188">Tworzenie projektu FileProvisioningAgent hello.</span><span class="sxs-lookup"><span data-stu-id="6b328-188">Build hello FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="6b328-189">Uruchamianie hello wiersza polecenia aplikacji w systemie Windows (jako Administrator), a następnie użyj hello **cd** polecenia toochange hello katalogu tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folderu.</span><span class="sxs-lookup"><span data-stu-id="6b328-189">Launch hello Command Prompt application in Windows (as an Administrator), and use hello **cd** command toochange hello directory tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="6b328-190">Witaj uruchom następujące polecenie, zastępując < adres ip > hello IP adresu lub nazwy domeny komputera z systemem Windows hello:</span><span class="sxs-lookup"><span data-stu-id="6b328-190">Run hello following command, replacing <ip-address> with hello IP address or domain name of hello Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="6b328-191">W systemie Windows w obszarze **ustawienia systemu Windows > Sieć i Internet ustawienia**, wybierz pozycję hello **zapory systemu Windows > Zaawansowane ustawienia**i Utwórz **reguły ruchu przychodzącego** który Umożliwia dostęp przychodzący tooport 9000.</span><span class="sxs-lookup"><span data-stu-id="6b328-191">In Windows under **Windows Settings > Network & Internet Settings**, select hello **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access tooport 9000.</span></span>
9. <span data-ttu-id="6b328-192">W przypadku komputera z systemem Windows hello za routerem, hello router potrzeb toobe skonfigurowane tooperform tłumaczenia dostępu do sieci między portu 9000 będący narażonych toohello internet i port 9000 na komputerze z systemem Windows hello.</span><span class="sxs-lookup"><span data-stu-id="6b328-192">If hello Windows machine is behind a router, hello router needs toobe configured tooperform Network Access Translation between its port 9000 that is exposed toohello internet, and port 9000 on hello Windows machine.</span></span> <span data-ttu-id="6b328-193">Jest to wymagane dla usługi Azure AD toobe stanie tooaccess tego punktu końcowego w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="6b328-193">This is required for Azure AD toobe able tooaccess this endpoint in hello cloud.</span></span>

<span data-ttu-id="6b328-194">**tooregister hello próbki SCIM punktu końcowego w usłudze Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="6b328-194">**tooregister hello sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="6b328-195">Zaloguj się za[hello portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6b328-195">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="6b328-196">Przeglądaj zbyt ** usługi Azure Active Directory > aplikacje dla przedsiębiorstw, a następnie wybierz **nowej aplikacji > wszystkie > Non galerii aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="6b328-196">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="6b328-197">Wprowadź nazwę aplikacji, a następnie kliknij przycisk **Dodaj** toocreate ikona obiektu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6b328-197">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span> <span data-ttu-id="6b328-198">utworzony obiekt aplikacji Hello jest aplikacji docelowej hello zamierzonego toorepresent czy udostępniania tooand implementacja punktu końcowego SCIM pojedynczego hello jednokrotne, a nie tylko.</span><span class="sxs-lookup"><span data-stu-id="6b328-198">hello application object created is intended toorepresent hello target app you would be provisioning tooand implementing single sign-on for, and not just hello SCIM endpoint.</span></span>
4. <span data-ttu-id="6b328-199">Na ekranie wynikowy hello wybierz hello **inicjowania obsługi administracyjnej** kartę w lewej kolumnie hello.</span><span class="sxs-lookup"><span data-stu-id="6b328-199">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="6b328-200">W hello **inicjowania obsługi trybu** menu, wybierz opcję **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="6b328-200">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="6b328-201">![][2]
  *Rysunek 4: Konfigurowanie inicjowania obsługi w hello portalu Azure*</span><span class="sxs-lookup"><span data-stu-id="6b328-201">![][2]
*Figure 4: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="6b328-202">W hello **adres URL dzierżawy** wprowadź adres URL hello udostępniane przez internet i port punktu końcowego SCIM.</span><span class="sxs-lookup"><span data-stu-id="6b328-202">In hello **Tenant URL** field, enter hello internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="6b328-203">Będzie to coś jak http://testmachine.contoso.com:9000 lub http://<ip-address>:9000/, gdzie < adres ip > jest hello internet widoczne IP adres.</span><span class="sxs-lookup"><span data-stu-id="6b328-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is hello internet exposed IP address.</span></span>  
7. <span data-ttu-id="6b328-204">Jeśli punkt końcowy SCIM hello wymaga tokenu elementu nośnego OAuth od wystawcy innego niż Azure AD, a następnie hello kopiowania wymagany token elementu nośnego OAuth do hello opcjonalne **klucz tajny tokenu** pola.</span><span class="sxs-lookup"><span data-stu-id="6b328-204">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="6b328-205">Jeśli to pole pozostanie puste, usługi Azure AD będą zawierać tokenu elementu nośnego OAuth wystawione przez usługi Azure AD z każdym żądaniem.</span><span class="sxs-lookup"><span data-stu-id="6b328-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="6b328-206">Aplikacje, które używają usługi Azure AD jako dostawca tożsamości może sprawdzić poprawność tej usługi Azure AD-wystawiony token.</span><span class="sxs-lookup"><span data-stu-id="6b328-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="6b328-207">Kliknij przycisk hello **Testuj połączenie** przycisk toohave usługi Azure Active Directory próba tooconnect toohello SCIM punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="6b328-207">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="6b328-208">W przypadku awarii próby hello, wyświetlane informacje o błędzie.</span><span class="sxs-lookup"><span data-stu-id="6b328-208">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="6b328-209">W przypadku powodzenia hello prób tooconnect toohello aplikacji, następnie kliknij przycisk **zapisać** poświadczeń administratora hello toosave.</span><span class="sxs-lookup"><span data-stu-id="6b328-209">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="6b328-210">W hello **mapowania** sekcji, istnieją dwa zestawy wybieranych mapowań atrybutów: jeden dla obiektów użytkownika i jeden dla obiektów grupy.</span><span class="sxs-lookup"><span data-stu-id="6b328-210">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="6b328-211">Wybierz każdego jeden atrybuty hello tooreview, które są synchronizowane z usługą Azure Active Directory tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6b328-211">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="6b328-212">Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello użytkowników i grup w aplikacji dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="6b328-212">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="6b328-213">Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.</span><span class="sxs-lookup"><span data-stu-id="6b328-213">Select hello Save button toocommit any changes.</span></span>
11. <span data-ttu-id="6b328-214">W obszarze **ustawienia**, hello **zakres** pola definiuje, które użytkownicy i grupy są synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="6b328-214">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="6b328-215">Wybieranie "Synchronizacji tylko przypisane użytkowników i grup" (zalecane) zsynchronizuje tylko użytkownicy i grupy przypisane w hello **użytkowników i grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="6b328-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="6b328-216">Po zakończeniu konfiguracji zmienić hello **stan inicjowania obsługi administracyjnej** za**na**.</span><span class="sxs-lookup"><span data-stu-id="6b328-216">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="6b328-217">Kliknij przycisk **zapisać** toostart hello inicjowania obsługi usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b328-217">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="6b328-218">Przydzielenia synchronizowanie tylko użytkownicy i grupy (zalecane), należy się hello tooselect **użytkowników i grup** karcie i przypisz hello użytkowników i/lub grup, które chcesz toosync.</span><span class="sxs-lookup"><span data-stu-id="6b328-218">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="6b328-219">Po rozpoczęciu hello wstępnej synchronizacji, można użyć hello **dzienniki inspekcji** karcie postępu toomonitor, który zawiera wszystkie akcje wykonywane przez hello świadczenie usługi w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6b328-219">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="6b328-220">Aby uzyskać więcej informacji dotyczących sposobu inicjowania obsługi usługi Azure AD hello tooread logowania, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="6b328-220">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="6b328-221">Ostatnim krokiem Hello podczas weryfikowania próbki hello jest hello tooopen TargetFile.csv plików w folderze \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug hello na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="6b328-221">hello final step in verifying hello sample is tooopen hello TargetFile.csv file in hello \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="6b328-222">Po uruchomieniu procesu udostępniania hello ten plik zawiera szczegóły hello wszystkich przypisane i udostępnione użytkowników i grup.</span><span class="sxs-lookup"><span data-stu-id="6b328-222">Once hello provisioning process is run, this file shows hello details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="6b328-223">Biblioteki programistyczne</span><span class="sxs-lookup"><span data-stu-id="6b328-223">Development libraries</span></span>
<span data-ttu-id="6b328-224">toodevelop własnej usługi sieci web, zgodne ze specyfikacją SCIM toohello, najpierw zapoznać się z następującej biblioteki dostarczony przez firmę Microsoft toohelp przyspieszyć proces tworzenia hello hello:</span><span class="sxs-lookup"><span data-stu-id="6b328-224">toodevelop your own web service that conforms toohello SCIM specification, first familiarize yourself with hello following libraries provided by Microsoft toohelp accelerate hello development process:</span></span> 

1. <span data-ttu-id="6b328-225">Wspólne biblioteki języka infrastruktury (CLI) dostępnych do użycia z językami oparte na infrastruktury, takich jak C#.</span><span class="sxs-lookup"><span data-stu-id="6b328-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="6b328-226">Jeden z tych bibliotek [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), deklaruje interfejsu Microsoft.SystemForCrossDomainIdentityManagement.IProvider, pokazano na następującej ilustracji hello: A Developer przy użyciu bibliotek hello czy implementuje ten interfejs z klasy, która może być określone, objęty dostawcę.</span><span class="sxs-lookup"><span data-stu-id="6b328-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in hello following illustration:  A developer using hello libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="6b328-227">biblioteki Hello umożliwiają toodeploy developer hello odpowiada specyfikacji SCIM toohello usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="6b328-227">hello libraries enable hello developer toodeploy a web service that conforms toohello SCIM specification.</span></span> <span data-ttu-id="6b328-228">usługi sieci web Hello może być obsługiwany albo w ramach Internetowe usługi informacyjne lub dowolnego pliku wykonywalnego zestawu wspólną infrastrukturę języka.</span><span class="sxs-lookup"><span data-stu-id="6b328-228">hello web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="6b328-229">Żądanie jest przetłumaczyć dostawcy toohello wywołania metody, które może być programowane za toooperate developer hello na niektórych magazynu tożsamości.</span><span class="sxs-lookup"><span data-stu-id="6b328-229">Request is translated into calls toohello provider’s methods, which would be programmed by hello developer toooperate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="6b328-230">[Express obsługi trasy](http://expressjs.com/guide/routing.html) są dostępne na potrzeby analizowania reprezentujący wywołań (jak określono w specyfikacji SCIM hello), usługa sieci web node.js tooa obiektów żądania node.js.</span><span class="sxs-lookup"><span data-stu-id="6b328-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by hello SCIM specification), made tooa node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="6b328-231">Tworzenie punktu końcowego niestandardowych SCIM</span><span class="sxs-lookup"><span data-stu-id="6b328-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="6b328-232">Przy użyciu biblioteki interfejsu wiersza polecenia hello, deweloperzy przy użyciu tych bibliotek mogą być hostowane swoich usług w dowolnym pliku wykonywalnego zestawu wspólną infrastrukturę języka lub do internetowych usług informacyjnych.</span><span class="sxs-lookup"><span data-stu-id="6b328-232">Using hello CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="6b328-233">Poniżej przedstawiono przykładowy kod w celu hostowania usługi w zestawie pliku wykonywalnego, pod adresem hello http://localhost:9000:</span><span class="sxs-lookup"><span data-stu-id="6b328-233">Here is sample code for hosting a service within an executable assembly, at hello address http://localhost:9000:</span></span> 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

<span data-ttu-id="6b328-234">Ta usługa musi mieć HTTP adres i serwera uwierzytelniania certyfikat które hello główny urząd certyfikacji jest jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="6b328-234">This service must have an HTTP address and server authentication certificate of which hello root certification authority is one of hello following:</span></span> 

* <span data-ttu-id="6b328-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="6b328-235">CNNIC</span></span>
* <span data-ttu-id="6b328-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="6b328-236">Comodo</span></span>
* <span data-ttu-id="6b328-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="6b328-237">CyberTrust</span></span>
* <span data-ttu-id="6b328-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="6b328-238">DigiCert</span></span>
* <span data-ttu-id="6b328-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="6b328-239">GeoTrust</span></span>
* <span data-ttu-id="6b328-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="6b328-240">GlobalSign</span></span>
* <span data-ttu-id="6b328-241">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="6b328-241">Go Daddy</span></span>
* <span data-ttu-id="6b328-242">VeriSign</span><span class="sxs-lookup"><span data-stu-id="6b328-242">Verisign</span></span>
* <span data-ttu-id="6b328-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="6b328-243">WoSign</span></span>

<span data-ttu-id="6b328-244">Certyfikat uwierzytelniania serwera może być powiązane tooa portu na hoście z systemem Windows przy użyciu narzędzia powłoki sieciowej hello:</span><span class="sxs-lookup"><span data-stu-id="6b328-244">A server authentication certificate can be bound tooa port on a Windows host using hello network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="6b328-245">W tym miejscu wartość hello argumentu parametrów certhash hello jest hello odcisk palca certyfikatu hello, podczas hello wartość podana dla argumentu appid hello jest umownym identyfikatorem globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="6b328-245">Here, hello value provided for hello certhash argument is hello thumbprint of hello certificate, while hello value provided for hello appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="6b328-246">usługi hello toohost w usługach IIS, deweloper może kompilacji zestawem CLA kod biblioteki z klasy o nazwie uruchamiania w domyślnej przestrzeni nazw hello hello zestawu.</span><span class="sxs-lookup"><span data-stu-id="6b328-246">toohost hello service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in hello default namespace of hello assembly.</span></span>  <span data-ttu-id="6b328-247">Oto przykład takiego klasy:</span><span class="sxs-lookup"><span data-stu-id="6b328-247">Here is a sample of such a class:</span></span> 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="6b328-248">Obsługa punktu końcowego uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="6b328-248">Handling endpoint authentication</span></span>
<span data-ttu-id="6b328-249">Żądania z usługi Azure Active Directory zawierać tokenu elementu nośnego OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="6b328-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="6b328-250">Wszystkie żądania obsługi odbierania hello powinna uwierzytelniać Witaj wystawca jako imieniu hello oczekiwano dzierżawy usługi Azure Active Directory, dla toohello dostępu do usługi sieci web Azure Active Directory Graph usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6b328-250">Any service receiving hello request should authenticate hello issuer as being Azure Active Directory on behalf of hello expected Azure Active Directory tenant, for access toohello Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="6b328-251">W tokenie hello wystawcy hello jest identyfikowany przez oświadczenie iss, takich jak "iss": "https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span><span class="sxs-lookup"><span data-stu-id="6b328-251">In hello token, hello issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="6b328-252">W tym przykładzie adres podstawowy hello hello wartości oświadczenia, https://sts.windows.net, identyfikuje usługi Azure Active Directory, jak Witaj wystawca, gdy hello adres względny segmentu, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, jest unikatowy identyfikator hello Azure Active Katalog dzierżawy, w imieniu którego hello token został wystawiony.</span><span class="sxs-lookup"><span data-stu-id="6b328-252">In this example, hello base address of hello claim value, https://sts.windows.net, identifies Azure Active Directory as hello issuer, while hello relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of hello Azure Active Directory tenant on behalf of which hello token was issued.</span></span>  <span data-ttu-id="6b328-253">Jeśli hello token został wystawiony dla uzyskiwania dostępu do usługi sieci web Azure Active Directory Graph hello, następnie identyfikator hello tej usługi 00000002-0000-0000-c000-000000000000, powinny być hello wartość tokenu hello lub oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="6b328-253">If hello token was issued for accessing hello Azure Active Directory Graph web service, then hello identifier of that service, 00000002-0000-0000-c000-000000000000, should be in hello value of hello token’s aud claim.</span></span>  

<span data-ttu-id="6b328-254">Deweloperzy przy użyciu bibliotek CLA hello obsługiwane przez firmę Microsoft do tworzenia usługi SCIM może uwierzytelnić żądania z usługi Azure Active Directory przy użyciu pakietu Microsoft.Owin.Security.ActiveDirectory hello, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6b328-254">Developers using hello CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using hello Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="6b328-255">U dostawcy należy zaimplementować właściwości Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior hello przez właśnie zwrócić toobe — metoda, wywoływana, gdy jest uruchomiona usługa hello:</span><span class="sxs-lookup"><span data-stu-id="6b328-255">In a provider, implement hello Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method toobe called whenever hello service is started:</span></span> 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. <span data-ttu-id="6b328-256">Dodaj wszystkie żądania tooany punktów końcowych usługi hello uwierzytelniony jako mając token wystawiony przez usługę Azure Active Directory w imieniu określonego dzierżawcę, dla toohello dostępu do usługi sieci web Azure AD Graph hello następującego kodu toothat metody toohave:</span><span class="sxs-lookup"><span data-stu-id="6b328-256">Add hello following code toothat method toohave any request tooany of hello service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access toohello Azure AD Graph web service:</span></span> 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="6b328-257">Schemat użytkowników i grup</span><span class="sxs-lookup"><span data-stu-id="6b328-257">User and group schema</span></span>
<span data-ttu-id="6b328-258">Usługa Azure Active Directory można udostępnić dwa typy usług sieci web tooSCIM zasobów.</span><span class="sxs-lookup"><span data-stu-id="6b328-258">Azure Active Directory can provision two types of resources tooSCIM web services.</span></span>  <span data-ttu-id="6b328-259">Te typy zasobów są użytkowników i grup.</span><span class="sxs-lookup"><span data-stu-id="6b328-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="6b328-260">Zasoby użytkownika są identyfikowane za pomocą identyfikatora schematu hello, urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, który jest dostępny w tej specyfikacji protokołu: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="6b328-260">User resources are identified by hello schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="6b328-261">Witaj domyślne mapowanie atrybutów hello użytkowników w usłudze Azure Active Directory toohello atrybutów zasobów urn: ietf:params:scim:schemas:extension:enterprise:2.0:User znajduje się w tabeli 1, poniżej.</span><span class="sxs-lookup"><span data-stu-id="6b328-261">hello default mapping of hello attributes of users in Azure Active Directory toohello attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="6b328-262">Grupy zasobów są identyfikowane za pomocą identyfikatora schematu hello, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="6b328-262">Group resources are identified by hello schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="6b328-263">Tabela 2, poniżej przedstawiono hello domyślne mapowanie atrybutów hello grup w usłudze Azure Active Directory toohello atrybuty http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group zasobów.</span><span class="sxs-lookup"><span data-stu-id="6b328-263">Table 2, below, shows hello default mapping of hello attributes of groups in Azure Active Directory toohello attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="6b328-264">Tabela 1: Domyślne mapowanie atrybutu użytkownika</span><span class="sxs-lookup"><span data-stu-id="6b328-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="6b328-265">Azure użytkownika usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b328-265">Azure Active Directory user</span></span> | <span data-ttu-id="6b328-266">urn: ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="6b328-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="6b328-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="6b328-267">IsSoftDeleted</span></span> |<span data-ttu-id="6b328-268">Aktywne</span><span class="sxs-lookup"><span data-stu-id="6b328-268">active</span></span> |
| <span data-ttu-id="6b328-269">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="6b328-269">displayName</span></span> |<span data-ttu-id="6b328-270">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="6b328-270">displayName</span></span> |
| <span data-ttu-id="6b328-271">TelephoneNumber faksu</span><span class="sxs-lookup"><span data-stu-id="6b328-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="6b328-272">.value phoneNumbers [eq typu "faks"]</span><span class="sxs-lookup"><span data-stu-id="6b328-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="6b328-273">Imię</span><span class="sxs-lookup"><span data-stu-id="6b328-273">givenName</span></span> |<span data-ttu-id="6b328-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="6b328-274">name.givenName</span></span> |
| <span data-ttu-id="6b328-275">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="6b328-275">jobTitle</span></span> |<span data-ttu-id="6b328-276">Tytuł</span><span class="sxs-lookup"><span data-stu-id="6b328-276">title</span></span> |
| <span data-ttu-id="6b328-277">Poczty</span><span class="sxs-lookup"><span data-stu-id="6b328-277">mail</span></span> |<span data-ttu-id="6b328-278">.value wiadomości e-mail [eq typu "Praca"]</span><span class="sxs-lookup"><span data-stu-id="6b328-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="6b328-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="6b328-279">mailNickname</span></span> |<span data-ttu-id="6b328-280">externalId</span><span class="sxs-lookup"><span data-stu-id="6b328-280">externalId</span></span> |
| <span data-ttu-id="6b328-281">Menedżer</span><span class="sxs-lookup"><span data-stu-id="6b328-281">manager</span></span> |<span data-ttu-id="6b328-282">Menedżer</span><span class="sxs-lookup"><span data-stu-id="6b328-282">manager</span></span> |
| <span data-ttu-id="6b328-283">Telefon komórkowy</span><span class="sxs-lookup"><span data-stu-id="6b328-283">mobile</span></span> |<span data-ttu-id="6b328-284">.value phoneNumbers [eq typu "mobile"]</span><span class="sxs-lookup"><span data-stu-id="6b328-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="6b328-285">Identyfikator obiektu</span><span class="sxs-lookup"><span data-stu-id="6b328-285">objectId</span></span> |<span data-ttu-id="6b328-286">id</span><span class="sxs-lookup"><span data-stu-id="6b328-286">id</span></span> |
| <span data-ttu-id="6b328-287">KodPocztowy</span><span class="sxs-lookup"><span data-stu-id="6b328-287">postalCode</span></span> |<span data-ttu-id="6b328-288">.postalCode adresów [eq typu "Praca"]</span><span class="sxs-lookup"><span data-stu-id="6b328-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="6b328-289">Adresy serwerów proxy</span><span class="sxs-lookup"><span data-stu-id="6b328-289">proxy-Addresses</span></span> |<span data-ttu-id="6b328-290">wiadomości e-mail [Wpisz eq "other"]. Wartość</span><span class="sxs-lookup"><span data-stu-id="6b328-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="6b328-291">Physical dostarczania-OfficeName</span><span class="sxs-lookup"><span data-stu-id="6b328-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="6b328-292">adresy [Wpisz eq "other"]. Sformatowany</span><span class="sxs-lookup"><span data-stu-id="6b328-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="6b328-293">Adres</span><span class="sxs-lookup"><span data-stu-id="6b328-293">streetAddress</span></span> |<span data-ttu-id="6b328-294">.streetAddress adresów [eq typu "Praca"]</span><span class="sxs-lookup"><span data-stu-id="6b328-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="6b328-295">nazwisko</span><span class="sxs-lookup"><span data-stu-id="6b328-295">surname</span></span> |<span data-ttu-id="6b328-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="6b328-296">name.familyName</span></span> |
| <span data-ttu-id="6b328-297">Numer telefonu</span><span class="sxs-lookup"><span data-stu-id="6b328-297">telephone-Number</span></span> |<span data-ttu-id="6b328-298">.value phoneNumbers [eq typu "Praca"]</span><span class="sxs-lookup"><span data-stu-id="6b328-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="6b328-299">PrincipalName użytkownika</span><span class="sxs-lookup"><span data-stu-id="6b328-299">user-PrincipalName</span></span> |<span data-ttu-id="6b328-300">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="6b328-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="6b328-301">Tabela 2: Domyślne grupy atrybutów mapowanie</span><span class="sxs-lookup"><span data-stu-id="6b328-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="6b328-302">Grupa usługi Active Directory systemu Azure</span><span class="sxs-lookup"><span data-stu-id="6b328-302">Azure Active Directory group</span></span> | <span data-ttu-id="6b328-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="6b328-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="6b328-304">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="6b328-304">displayName</span></span> |<span data-ttu-id="6b328-305">externalId</span><span class="sxs-lookup"><span data-stu-id="6b328-305">externalId</span></span> |
| <span data-ttu-id="6b328-306">Poczty</span><span class="sxs-lookup"><span data-stu-id="6b328-306">mail</span></span> |<span data-ttu-id="6b328-307">.value wiadomości e-mail [eq typu "Praca"]</span><span class="sxs-lookup"><span data-stu-id="6b328-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="6b328-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="6b328-308">mailNickname</span></span> |<span data-ttu-id="6b328-309">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="6b328-309">displayName</span></span> |
| <span data-ttu-id="6b328-310">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="6b328-310">members</span></span> |<span data-ttu-id="6b328-311">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="6b328-311">members</span></span> |
| <span data-ttu-id="6b328-312">Identyfikator obiektu</span><span class="sxs-lookup"><span data-stu-id="6b328-312">objectId</span></span> |<span data-ttu-id="6b328-313">id</span><span class="sxs-lookup"><span data-stu-id="6b328-313">id</span></span> |
| <span data-ttu-id="6b328-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="6b328-314">proxyAddresses</span></span> |<span data-ttu-id="6b328-315">wiadomości e-mail [Wpisz eq "other"]. Wartość</span><span class="sxs-lookup"><span data-stu-id="6b328-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="6b328-316">Inicjowanie obsługi użytkowników i anulowanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="6b328-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="6b328-317">Witaj następujące wiadomości powitania ilustracji przedstawiono z usługi Azure Active Directory i wysyła tooa SCIM toomanage hello cyklu życia usług użytkownika w innym magazynie tożsamości.</span><span class="sxs-lookup"><span data-stu-id="6b328-317">hello following illustration shows hello messages that Azure Active Directory sends tooa SCIM service toomanage hello lifecycle of a user in another identity store.</span></span> <span data-ttu-id="6b328-318">Hello diagram pokazuje też, jak usługa SCIM implementowane przy użyciu biblioteki interfejsu wiersza polecenia hello obsługiwane przez firmę Microsoft do tworzenia, się, że takie usługi tłumaczenia te żądania na wywołania metody toohello dostawcy.</span><span class="sxs-lookup"><span data-stu-id="6b328-318">hello diagram also shows how a SCIM service implemented using hello CLI libraries provided by Microsoft for building such services translate those requests into calls toohello methods of a provider.</span></span>  

<span data-ttu-id="6b328-319">![][4]
*Rysunek 5: Użytkownik aprowizację i anulowanie obsługi sekwencji*</span><span class="sxs-lookup"><span data-stu-id="6b328-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="6b328-320">Azure zapytań usługi Active Directory hello usługi dla użytkownika z wartością atrybutu externalId dopasowania wartości atrybutu mailNickname hello użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b328-320">Azure Active Directory queries hello service for a user with an externalId attribute value matching hello mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="6b328-321">Zapytanie Hello jest wyrażony jako żądania protokołu HTTP (Hypertext Transfer), np. w tym przykładzie, w którym jyoung znajduje się przykład mailNickname użytkownika w usłudze Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="6b328-321">hello query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="6b328-322">Jeśli usługa hello został zbudowany przy użyciu bibliotek wspólną infrastrukturę języka hello obsługiwane przez firmę Microsoft dla implementacji usługi SCIM, Żądanie hello jest przetłumaczony na toohello wywołanie metody zapytania hello usługodawcy.</span><span class="sxs-lookup"><span data-stu-id="6b328-322">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span>  <span data-ttu-id="6b328-323">Oto podpisu hello tej metody:</span><span class="sxs-lookup"><span data-stu-id="6b328-323">Here is hello signature of that method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="6b328-324">Oto hello definicji interfejsu Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters hello:</span><span class="sxs-lookup"><span data-stu-id="6b328-324">Here is hello definition of hello Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  <span data-ttu-id="6b328-325">W następujące przykładowe zapytania dla użytkownika z danej wartości dla atrybutu externalId hello hello wartości hello Argumenty przekazane toohello metoda zapytania są:</span><span class="sxs-lookup"><span data-stu-id="6b328-325">In hello following sample of a query for a user with a given value for hello externalId attribute, values of hello arguments passed toohello Query method are:</span></span> 
  * <span data-ttu-id="6b328-326">Parametry. AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="6b328-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="6b328-327">Parametry. AlternateFilters.ElementAt(0). AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="6b328-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="6b328-328">Parametry. AlternateFilters.ElementAt(0). OperatorPorównania: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="6b328-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="6b328-329">Parametry. AlternateFilter.ElementAt(0). ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="6b328-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="6b328-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin. Identyfikator żądania"]</span><span class="sxs-lookup"><span data-stu-id="6b328-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="6b328-331">Jeśli hello odpowiedzi tooa zapytania toohello usługi sieci web dla użytkownika z wartością atrybutu externalId odpowiadającą wartości atrybutu mailNickname hello użytkownika nie zwraca żadnych użytkowników, następnie usługi Azure Active Directory żąda tego hello usług świadczonych przez użytkownika odpowiednie toohello co w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6b328-331">If hello response tooa query toohello web service for a user with an externalId attribute value that matches hello mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that hello service provision a user corresponding toohello one in Azure Active Directory.</span></span>  <span data-ttu-id="6b328-332">Oto przykład takiego żądania:</span><span class="sxs-lookup"><span data-stu-id="6b328-332">Here is an example of such a request:</span></span> 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  <span data-ttu-id="6b328-333">obsługiwane przez firmę Microsoft dla implementacji usługi SCIM bibliotek wspólną infrastrukturę języka Hello przekłada to żądanie do toohello wywołanie metody Create hello usługodawcy.</span><span class="sxs-lookup"><span data-stu-id="6b328-333">hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call toohello Create method of hello service’s provider.</span></span>  <span data-ttu-id="6b328-334">Witaj metody Create ma podpis:</span><span class="sxs-lookup"><span data-stu-id="6b328-334">hello Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="6b328-335">W tooprovision żądania użytkownika hello wartość argumentu zasobów hello jest wystąpieniem hello Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="6b328-335">In a request tooprovision a user, hello value of hello resource argument is an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="6b328-336">Klasa Core2EnterpriseUser zdefiniowany w bibliotece Microsoft.SystemForCrossDomainIdentityManagement.Schemas hello.</span><span class="sxs-lookup"><span data-stu-id="6b328-336">Core2EnterpriseUser class, defined in hello Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="6b328-337">Jeśli hello żądania tooprovision hello użytkownika zakończy się powodzeniem, następnie hello implementacja metody hello jest oczekiwany tooreturn wystąpienia hello Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="6b328-337">If hello request tooprovision hello user succeeds, then hello implementation of hello method is expected tooreturn an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="6b328-338">Klasa Core2EnterpriseUser, z hello wartość właściwości identyfikator hello ustawić toohello Unikatowy identyfikator użytkownika nowo aprowizowanej hello.</span><span class="sxs-lookup"><span data-stu-id="6b328-338">Core2EnterpriseUser class, with hello value of hello Identifier property set toohello unique identifier of hello newly provisioned user.</span></span>  

3. <span data-ttu-id="6b328-339">tooupdate użytkownika znane tooexist w magazynie tożsamości przez SCIM usługi Azure Active Directory będzie kontynuowane, żądając hello bieżący stan tego użytkownika z usługi hello z żądaniem, takich jak:</span><span class="sxs-lookup"><span data-stu-id="6b328-339">tooupdate a user known tooexist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting hello current state of that user from hello service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="6b328-340">W usłudze utworzony przy użyciu bibliotek wspólną infrastrukturę języka hello obsługiwane przez firmę Microsoft dla implementacji usługi SCIM Żądanie hello jest przetłumaczyć toohello wywołanie metody pobierania hello usługodawcy.</span><span class="sxs-lookup"><span data-stu-id="6b328-340">In a service built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, hello request is translated into a call toohello Retrieve method of hello service’s provider.</span></span>  <span data-ttu-id="6b328-341">Oto hello podpis metody pobierania hello:</span><span class="sxs-lookup"><span data-stu-id="6b328-341">Here is hello signature of hello Retrieve method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  <span data-ttu-id="6b328-342">W przykładzie hello żądania tooretrieve hello bieżącego stanu użytkownika hello wartości właściwości hello obiektu hello dostarczonych jako wartość hello argumentu parametrów hello są następujące:</span><span class="sxs-lookup"><span data-stu-id="6b328-342">In hello example of a request tooretrieve hello current state of a user, hello values of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="6b328-343">Identyfikator: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="6b328-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="6b328-344">SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="6b328-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="6b328-345">Jeśli atrybut odwołania jest toobe zaktualizowane, następnie usługi Azure Active Directory zapytania hello usługi toodetermine czy hello bieżącą wartość atrybutu odwołania hello w magazynie tożsamości hello fronted przez usługę hello pasuje już hello wartość tego atrybutu w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6b328-345">If a reference attribute is toobe updated, then Azure Active Directory queries hello service toodetermine whether or not hello current value of hello reference attribute in hello identity store fronted by hello service already matches hello value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="6b328-346">W przypadku użytkowników hello tylko z których hello bieżąca wartość jest poddawany kwerendzie w ten sposób jest hello Menedżera atrybutem.</span><span class="sxs-lookup"><span data-stu-id="6b328-346">For users, hello only attribute of which hello current value is queried in this way is hello manager attribute.</span></span> <span data-ttu-id="6b328-347">Oto przykład toodetermine żądania czy hello Menedżera atrybut obiektu określonego użytkownika aktualnie ma określoną wartość:</span><span class="sxs-lookup"><span data-stu-id="6b328-347">Here is an example of a request toodetermine whether hello manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="6b328-348">Witaj wartość parametru zapytania atrybuty hello, identyfikator, oznacza, że jeśli obiekt użytkownika istnieje odpowiadającej dostarczonego jako wartość parametru zapytania filtru hello hello wyrażenia hello, a następnie usługa hello jest oczekiwany toorespond z urn: ietf:params:scim:schemas: podstawowe: 2.0:User lub urn: ietf:params:scim:schemas:extension:enterprise:2.0:User zasobów łącznie tylko hello wartość atrybutu id tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="6b328-348">hello value of hello attributes query parameter, id, signifies that if a user object exists that satisfies hello expression provided as hello value of hello filter query parameter, then hello service is expected toorespond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only hello value of that resource’s id attribute.</span></span>  <span data-ttu-id="6b328-349">Witaj wartość hello **identyfikator** atrybut nosi toohello obiektu żądającego.</span><span class="sxs-lookup"><span data-stu-id="6b328-349">hello value of hello **id** attribute is known toohello requestor.</span></span> <span data-ttu-id="6b328-350">Znajduje się on w hello wartość parametru zapytania filtru hello; pyta celem Hello jest rzeczywiście toorequest minimalnego reprezentację z zasobem, który spełnia wyrażenie filtru hello jako ze wskazaniem, czy jakikolwiek obiekt istnieje.</span><span class="sxs-lookup"><span data-stu-id="6b328-350">It is included in hello value of hello filter query parameter; hello purpose of asking for it is actually toorequest a minimal representation of a resource that satisfying hello filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="6b328-351">Jeśli usługa hello został zbudowany przy użyciu bibliotek wspólną infrastrukturę języka hello obsługiwane przez firmę Microsoft dla implementacji usługi SCIM, Żądanie hello jest przetłumaczony na toohello wywołanie metody zapytania hello usługodawcy.</span><span class="sxs-lookup"><span data-stu-id="6b328-351">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span> <span data-ttu-id="6b328-352">wartość Hello hello właściwości obiektu hello dostarczonych jako wartość hello argumentu parametrów hello są następujące:</span><span class="sxs-lookup"><span data-stu-id="6b328-352">hello value of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="6b328-353">Parametry. AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="6b328-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="6b328-354">Parametry. AlternateFilters.ElementAt(x). AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="6b328-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="6b328-355">Parametry. AlternateFilters.ElementAt(x). OperatorPorównania: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="6b328-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="6b328-356">Parametry. AlternateFilter.ElementAt(x). ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="6b328-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="6b328-357">Parametry. AlternateFilters.ElementAt(y). AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="6b328-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="6b328-358">Parametry. AlternateFilters.ElementAt(y). OperatorPorównania: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="6b328-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="6b328-359">Parametry. AlternateFilter.ElementAt(y). ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="6b328-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="6b328-360">Parametry. RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="6b328-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="6b328-361">Parametry. SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="6b328-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="6b328-362">W tym miejscu hello wartość indeksu hello x może być 0 i hello wartość y o indeksie hello może być 1, lub hello wartość x może być równa 1 i hello wartość y może mieć wartość 0, w zależności od kolejności hello wyrażeń hello parametru zapytania filtru hello.</span><span class="sxs-lookup"><span data-stu-id="6b328-362">Here, hello value of hello index x may be 0 and hello value of hello index y may be 1, or hello value of x may be 1 and hello value of y may be 0, depending on hello order of hello expressions of hello filter query parameter.</span></span>   

5. <span data-ttu-id="6b328-363">Oto przykład żądania z usługi Azure Active Directory tooan SCIM usługi tooupdate użytkownika:</span><span class="sxs-lookup"><span data-stu-id="6b328-363">Here is an example of a request from Azure Active Directory tooan SCIM service tooupdate a user:</span></span> 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  <span data-ttu-id="6b328-364">Implementowanie usług SCIM biblioteki wspólną infrastrukturę języka Microsoft Hello przekłada hello żądania do toohello wywołanie metody aktualizacji hello usługodawcy.</span><span class="sxs-lookup"><span data-stu-id="6b328-364">hello Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate hello request into a call toohello Update method of hello service’s provider.</span></span> <span data-ttu-id="6b328-365">Oto hello podpis hello metody aktualizacji:</span><span class="sxs-lookup"><span data-stu-id="6b328-365">Here is hello signature of hello Update method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    <span data-ttu-id="6b328-366">W przykładzie hello tooupdate żądania użytkownika dostarczony jako wartość argumentu poprawki hello hello obiekt hello ma wartości tych właściwości:</span><span class="sxs-lookup"><span data-stu-id="6b328-366">In hello example of a request tooupdate a user, hello object provided as hello value of hello patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="6b328-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="6b328-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="6b328-368">ResourceIdentifier.SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="6b328-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="6b328-369">(PatchRequest jako PatchRequest2). Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="6b328-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="6b328-370">(PatchRequest jako PatchRequest2). Operations.ElementAt(0). OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="6b328-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="6b328-371">(PatchRequest jako PatchRequest2). Operations.ElementAt(0). Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="6b328-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="6b328-372">(PatchRequest jako PatchRequest2). Operations.ElementAt(0). Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="6b328-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="6b328-373">(PatchRequest jako PatchRequest2). Operations.ElementAt(0). Value.ElementAt(0). Odwołanie: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="6b328-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="6b328-374">(PatchRequest jako PatchRequest2). Operations.ElementAt(0). Value.ElementAt(0). Wartość: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="6b328-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="6b328-375">toode-provision użytkownika z magazynu tożsamości fronted przez usługę SCIM, takich jak wysyła żądanie usługi Azure AD:</span><span class="sxs-lookup"><span data-stu-id="6b328-375">toode-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="6b328-376">Jeśli usługa hello został zbudowany przy użyciu bibliotek wspólną infrastrukturę języka hello obsługiwane przez firmę Microsoft dla implementacji usługi SCIM, Żądanie hello jest przetłumaczony na toohello wywołanie metody Delete hello usługodawcy.</span><span class="sxs-lookup"><span data-stu-id="6b328-376">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Delete method of hello service’s provider.</span></span>   <span data-ttu-id="6b328-377">Ta metoda ma podpis:</span><span class="sxs-lookup"><span data-stu-id="6b328-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="6b328-378">dostarczony jako wartość argumentu resourceIdentifier hello hello obiekt Hello ma wartości tych właściwości w przykładzie hello żądania toode-przepisu użytkownika:</span><span class="sxs-lookup"><span data-stu-id="6b328-378">hello object provided as hello value of hello resourceIdentifier argument has these property values in hello example of a request toode-provision a user:</span></span> 
  
  * <span data-ttu-id="6b328-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="6b328-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="6b328-380">ResourceIdentifier.SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="6b328-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="6b328-381">Grupy aprowizację i anulowanie obsługi</span><span class="sxs-lookup"><span data-stu-id="6b328-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="6b328-382">Witaj następujące wiadomości powitania przedstawiono na ilustracji Azure AcD i wysyła tooa SCIM toomanage hello cyklu życia usług grupy w innym magazynie tożsamości.</span><span class="sxs-lookup"><span data-stu-id="6b328-382">hello following illustration shows hello messages that Azure AcD sends tooa SCIM service toomanage hello lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="6b328-383">Te komunikaty różnią się od wiadomości powitania dotyczące toousers na trzy sposoby:</span><span class="sxs-lookup"><span data-stu-id="6b328-383">Those messages differ from hello messages pertaining toousers in three ways:</span></span> 

* <span data-ttu-id="6b328-384">Schemat Hello zasób grupy jest rozpoznawany jako http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="6b328-384">hello schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="6b328-385">Żądania wysyłane grup tooretrieve określać atrybutu członków hello jest toobe wykluczone z dowolnego zasobu podany w żądaniu toohello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6b328-385">Requests tooretrieve groups stipulate that hello members attribute is toobe excluded from any resource provided in response toohello request.</span></span>  
* <span data-ttu-id="6b328-386">Określa, czy jest atrybut odwołania ma określoną wartość są żądania dotyczące hello elementy członkowskie atrybutu toodetermine żądań.</span><span class="sxs-lookup"><span data-stu-id="6b328-386">Requests toodetermine whether a reference attribute has a certain value are requests about hello members attribute.</span></span>  

<span data-ttu-id="6b328-387">![][5]
*Rysunek 6: Grupy aprowizację i anulowanie obsługi sekwencji*</span><span class="sxs-lookup"><span data-stu-id="6b328-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="6b328-388">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="6b328-388">Related articles</span></span>
* [<span data-ttu-id="6b328-389">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b328-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="6b328-390">Automatyzowanie inicjowania obsługi administracyjnej użytkowników/anulowania zastrzeżenia tooSaaS aplikacji</span><span class="sxs-lookup"><span data-stu-id="6b328-390">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="6b328-391">Dostosowywanie mapowań atrybutów do inicjowania obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="6b328-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="6b328-392">Tworzenie wyrażeń na potrzeby mapowań atrybutów</span><span class="sxs-lookup"><span data-stu-id="6b328-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="6b328-393">Filtry zakresu dla Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="6b328-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="6b328-394">Powiadomienia aprowizacji kont</span><span class="sxs-lookup"><span data-stu-id="6b328-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="6b328-395">Lista samouczków dotyczących tooIntegrate aplikacji SaaS</span><span class="sxs-lookup"><span data-stu-id="6b328-395">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
