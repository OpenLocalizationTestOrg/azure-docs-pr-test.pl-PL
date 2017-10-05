---
title: "Przy użyciu systemu dla zarządzania tożsamościami między domenami automatycznej aprowizacji użytkowników i grup z usługi Azure Active Directory do aplikacji | Dokumentacja firmy Microsoft"
description: "Usługa Azure Active Directory mogą automatycznie obsługiwać użytkowników i grup do aplikacji lub tożsamości magazynu, który jest fronted przez usługę sieci web przy użyciu interfejsu zdefiniowane w specyfikacji protokołu SCIM"
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
ms.openlocfilehash: 91978cee88d55c99bcb63c63cdaf01581ae84668
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="using-system-for-cross-domain-identity-management-to-automatically-provision-users-and-groups-from-azure-active-directory-to-applications"></a><span data-ttu-id="cfb31-103">Przy użyciu systemu do innej domeny zarządzania tożsamościami do automatycznej aprowizacji użytkowników i grup z usługi Azure Active Directory do aplikacji</span><span class="sxs-lookup"><span data-stu-id="cfb31-103">Using System for Cross-Domain Identity Management to automatically provision users and groups from Azure Active Directory to applications</span></span>

## <a name="overview"></a><span data-ttu-id="cfb31-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="cfb31-104">Overview</span></span>
<span data-ttu-id="cfb31-105">Azure Active Directory (Azure AD), mogą automatycznie obsługiwać użytkowników i grup do aplikacji lub tożsamości magazynu, który jest fronted przez usługę sieci web przy użyciu interfejsu zdefiniowanych w [systemu dla protokołu zarządzania tożsamości między domenami (SCIM) 2.0 Specyfikacja](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="cfb31-105">Azure Active Directory (Azure AD) can automatically provision users and groups to any application or identity store that is fronted by a web service with the interface defined in the [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="cfb31-106">Usługa Azure Active Directory mogą wysyłać żądania do tworzenia, modyfikowania lub usuwania przypisane użytkowników i grup z usługą sieci web.</span><span class="sxs-lookup"><span data-stu-id="cfb31-106">Azure Active Directory can send requests to create, modify, or delete assigned users and groups to the web service.</span></span> <span data-ttu-id="cfb31-107">Usługa sieci web może dokonywać translacji te żądania do operacji w magazynie docelowym tożsamości.</span><span class="sxs-lookup"><span data-stu-id="cfb31-107">The web service can then translate those requests into operations on the target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="cfb31-108">Firma Microsoft zaleca zarządzanie usługą Azure AD przy użyciu [centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w witrynie Azure Portal zamiast korzystania z klasycznej witryny Azure Portal przywołanej w niniejszym artykule.</span><span class="sxs-lookup"><span data-stu-id="cfb31-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="cfb31-109">![][0]
*Rysunek 1: Inicjowanie obsługi administracyjnej z usługi Azure Active Directory, do magazynu tożsamości za pomocą usługi sieci web*</span><span class="sxs-lookup"><span data-stu-id="cfb31-109">![][0]
*Figure 1: Provisioning from Azure Active Directory to an identity store via a web service*</span></span>

<span data-ttu-id="cfb31-110">Ta możliwość może służyć w połączeniu z możliwością "Przynieś własne aplikacji" w usłudze Azure AD do włączenia logowania jednokrotnego i użytkownika automatyczne Inicjowanie obsługi administracyjnej dla aplikacji, które zapewniają lub są fronted przez usługę sieci web SCIM.</span><span class="sxs-lookup"><span data-stu-id="cfb31-110">This capability can be used in conjunction with the “bring your own app” capability in Azure AD to enable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="cfb31-111">Istnieją dwa przypadki użycia przy użyciu SCIM w usłudze Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="cfb31-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="cfb31-112">**Inicjowanie obsługi użytkowników i grup do aplikacji, które obsługują SCIM** aplikacji, które obsługują SCIM 2.0 i używają tokenów elementu nośnego OAuth dla działania uwierzytelniania w usłudze Azure AD bez konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="cfb31-112">**Provisioning users and groups to applications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="cfb31-113">**Skompiluj rozwiązanie inicjowania obsługi administracyjnej dla aplikacji, które obsługę innych oparty na interfejsach API** dla aplikacji z systemem innym niż SCIM, można utworzyć punktu końcowego SCIM translacji przez punkt końcowy usługi Azure AD SCIM i jakiegokolwiek interfejsu API aplikacja obsługuje dla użytkownika Inicjowanie obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="cfb31-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint to translate between the Azure AD SCIM endpoint and any API the application supports for user provisioning.</span></span> <span data-ttu-id="cfb31-114">Aby ułatwić tworzenie punktu końcowego SCIM, udostępniamy infrastruktury języka wspólnego (CLI) bibliotek oraz przykłady kodu, które pokazują, jak Podaj punkt końcowy SCIM i tłumaczenie SCIM wiadomości.</span><span class="sxs-lookup"><span data-stu-id="cfb31-114">To help you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how to do provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-to-applications-that-support-scim"></a><span data-ttu-id="cfb31-115">Inicjowanie obsługi użytkowników i grup do aplikacji, które obsługują SCIM</span><span class="sxs-lookup"><span data-stu-id="cfb31-115">Provisioning users and groups to applications that support SCIM</span></span>
<span data-ttu-id="cfb31-116">Usługi Azure AD można skonfigurować do automatycznego należy przypisać użytkowników i grup do aplikacji, które implementują [systemu do zarządzania tożsamościami międzydomenowego 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) usługi sieci web i zaakceptować tokenów elementu nośnego OAuth dla uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="cfb31-116">Azure AD can be configured to automatically provision assigned users and groups to applications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="cfb31-117">W specyfikacji SCIM 2.0 aplikacji musi spełniać następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="cfb31-117">Within the SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="cfb31-118">Obsługuje tworzenie użytkowników i grupy, zgodnie z sekcji 3.3 protokołu SCIM.</span><span class="sxs-lookup"><span data-stu-id="cfb31-118">Supports creating users and/or groups, as per section 3.3 of the SCIM protocol.</span></span>  
* <span data-ttu-id="cfb31-119">Obsługa modyfikowania użytkowników i/lub grup z żądaniami poprawki zgodnie z sekcji 3.5.2 protokołu SCIM.</span><span class="sxs-lookup"><span data-stu-id="cfb31-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="cfb31-120">Obsługuje pobieranie znanych zasobów zgodnie z sekcji 3.4.1 protokołu SCIM.</span><span class="sxs-lookup"><span data-stu-id="cfb31-120">Supports retrieving a known resource as per section 3.4.1 of the SCIM protocol.</span></span>  
* <span data-ttu-id="cfb31-121">Obsługa zapytań użytkowników i grupy, zgodnie z sekcji 3.4.2 protokołu SCIM.</span><span class="sxs-lookup"><span data-stu-id="cfb31-121">Supports querying users and/or groups, as per section 3.4.2 of the SCIM protocol.</span></span>  <span data-ttu-id="cfb31-122">Domyślnie użytkownicy są proszeni przez externalId i grup są żądanych przez Nazwa wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="cfb31-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="cfb31-123">Obsługa zapytań użytkownika według Identyfikatora i przez Menedżera zgodnie z sekcji 3.4.2 protokołu SCIM.</span><span class="sxs-lookup"><span data-stu-id="cfb31-123">Supports querying user by ID and by manager as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="cfb31-124">Obsługa zapytań grup według Identyfikatora i przez członka zgodnie z sekcji 3.4.2 protokołu SCIM.</span><span class="sxs-lookup"><span data-stu-id="cfb31-124">Supports querying groups by ID and by member as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="cfb31-125">Akceptuje tokenów elementu nośnego OAuth dla autoryzacji zgodnie z sekcji 2.1 protokołu SCIM.</span><span class="sxs-lookup"><span data-stu-id="cfb31-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of the SCIM protocol.</span></span>

<span data-ttu-id="cfb31-126">Skontaktuj się z dostawcą aplikacji lub dokumentacji dostawcy aplikacji dla instrukcji zgodność z tych wymagań.</span><span class="sxs-lookup"><span data-stu-id="cfb31-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="cfb31-127">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="cfb31-127">Getting started</span></span>
<span data-ttu-id="cfb31-128">Aplikacje, które obsługują profilu SCIM opisane w tym artykule można podłączyć do usługi Azure Active Directory za pomocą funkcji "z systemem innym niż galerii aplikacji" w galerii aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfb31-128">Applications that support the SCIM profile described in this article can be connected to Azure Active Directory using the "non-gallery application" feature in the Azure AD application gallery.</span></span> <span data-ttu-id="cfb31-129">Po nawiązaniu połączenia usługi Azure AD uruchamia proces synchronizacji co 20 minut, gdzie wysyła zapytanie do punktu końcowego SCIM aplikacji przypisanych użytkowników i grup i tworzy lub modyfikuje je zgodnie z szczegółów przypisania.</span><span class="sxs-lookup"><span data-stu-id="cfb31-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries the application's SCIM endpoint for assigned users and groups, and creates or modifies them according to the assignment details.</span></span>

<span data-ttu-id="cfb31-130">**Aby połączyć aplikację obsługującą SCIM:**</span><span class="sxs-lookup"><span data-stu-id="cfb31-130">**To connect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="cfb31-131">Zaloguj się do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cfb31-131">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="cfb31-132">Przejdź do ** usługi Azure Active Directory > aplikacje dla przedsiębiorstw, a następnie wybierz **nowej aplikacji > wszystkie > Non galerii aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="cfb31-132">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="cfb31-133">Wprowadź nazwę aplikacji, a następnie kliknij przycisk **Dodaj** ikonę, aby utworzyć obiekt aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cfb31-133">Enter a name for your application, and click **Add** icon to create an app object.</span></span>
    
  <span data-ttu-id="cfb31-134">![][1]
  *Rysunek 2: Galerii aplikacji usługi Azure AD*</span><span class="sxs-lookup"><span data-stu-id="cfb31-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="cfb31-135">Na ekranie wynikowy wybierz **inicjowania obsługi administracyjnej** kartę w lewej kolumnie.</span><span class="sxs-lookup"><span data-stu-id="cfb31-135">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="cfb31-136">W **inicjowania obsługi trybu** menu, wybierz opcję **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="cfb31-136">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="cfb31-137">![][2]
  *Rysunek 3: Konfigurowanie inicjowania obsługi w portalu Azure*</span><span class="sxs-lookup"><span data-stu-id="cfb31-137">![][2]
*Figure 3: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="cfb31-138">W **adres URL dzierżawy** wprowadź adres URL punktu końcowego SCIM aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cfb31-138">In the **Tenant URL** field, enter the URL of the application's SCIM endpoint.</span></span> <span data-ttu-id="cfb31-139">Przykład: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="cfb31-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="cfb31-140">Jeśli punkt końcowy SCIM wymaga tokenu elementu nośnego OAuth od wystawcy innego niż Azure AD, następnie skopiuj wymagany token elementu nośnego OAuth do opcjonalnego **klucz tajny tokenu** pola.</span><span class="sxs-lookup"><span data-stu-id="cfb31-140">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="cfb31-141">Jeśli to pole pozostanie puste, usługi Azure AD uwzględnione tokenu elementu nośnego OAuth wystawione przez usługi Azure AD z każdym żądaniem.</span><span class="sxs-lookup"><span data-stu-id="cfb31-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="cfb31-142">Aplikacje, które używają usługi Azure AD jako dostawca tożsamości może sprawdzić poprawność tej usługi Azure AD-wystawiony token.</span><span class="sxs-lookup"><span data-stu-id="cfb31-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="cfb31-143">Kliknij przycisk **Testuj połączenie** przycisk, aby podejmować próby nawiązania połączenia z punktem końcowym SCIM usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cfb31-143">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="cfb31-144">W przypadku awarii próby, wyświetlane informacje o błędzie.</span><span class="sxs-lookup"><span data-stu-id="cfb31-144">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="cfb31-145">Jeśli próby połączenia się pomyślnie aplikacji, należy kliknąć **zapisać** można zapisać poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="cfb31-145">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="cfb31-146">W **mapowania** sekcji, istnieją dwa zestawy wybieranych mapowań atrybutów: jeden dla obiektów użytkownika i jeden dla obiektów grupy.</span><span class="sxs-lookup"><span data-stu-id="cfb31-146">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="cfb31-147">Zaznacz każdą z nich Przejrzyj atrybuty, które są synchronizowane z usługą Azure Active Directory do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cfb31-147">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="cfb31-148">Atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania użytkowników i grup w aplikacji dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="cfb31-148">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="cfb31-149">Wybierz przycisk Zapisz, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="cfb31-149">Select the Save button to commit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="cfb31-150">Opcjonalnie możesz wyłączyć synchronizację obiektów grupy przez wyłączenie mapowania "grupy".</span><span class="sxs-lookup"><span data-stu-id="cfb31-150">You can optionally disable syncing of group objects by disabling the "groups" mapping.</span></span> 

11. <span data-ttu-id="cfb31-151">W obszarze **ustawienia**, **zakres** pola definiuje, które użytkownicy i grupy są synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="cfb31-151">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="cfb31-152">Wybranie "Synchronizacji tylko przypisane użytkowników i grup" (zalecane) będzie tylko synchronizować użytkownicy i grupy przypisane w **użytkowników i grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="cfb31-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="cfb31-153">Po zakończeniu konfiguracji zmienić **stan inicjowania obsługi administracyjnej** do **na**.</span><span class="sxs-lookup"><span data-stu-id="cfb31-153">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="cfb31-154">Kliknij przycisk **zapisać** można uruchomić usługi Azure AD, inicjowania obsługi usługi.</span><span class="sxs-lookup"><span data-stu-id="cfb31-154">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="cfb31-155">Jeśli synchronizacja przypisana tylko użytkownicy i grupy (zalecane), należy wybrać **użytkowników i grup** karcie i Przypisz użytkowników i/lub grup, które chcesz wykonać synchronizację.</span><span class="sxs-lookup"><span data-stu-id="cfb31-155">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="cfb31-156">Po rozpoczęciu synchronizacji początkowej, można użyć **dzienniki inspekcji** kartę do monitorowania postępu, który pokazuje wszystkie akcje wykonywane przez usługę inicjowania obsługi administracyjnej w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cfb31-156">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="cfb31-157">Aby uzyskać więcej informacji na temat usługi Azure AD, inicjowanie obsługi dzienników do odczytu, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="cfb31-157">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="cfb31-158">Synchronizacji początkowej zajmuje więcej czasu wykonywania niż kolejne synchronizacje, występujące co około 20 minut, tak długo, jak usługa jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="cfb31-158">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="cfb31-159">Tworzenie rozwiązania inicjowania obsługi administracyjnej dla dowolnej aplikacji</span><span class="sxs-lookup"><span data-stu-id="cfb31-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="cfb31-160">Tworząc interfejsy usługi sieci web SCIM z usługi Azure Active Directory, można włączyć pojedynczego użytkownika logowania jednokrotnego i automatyczne Inicjowanie obsługi praktycznie dowolnej aplikacji, która zawiera użytkownika inicjowania obsługi interfejsu API REST lub protokołu SOAP.</span><span class="sxs-lookup"><span data-stu-id="cfb31-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="cfb31-161">Oto jak to działa:</span><span class="sxs-lookup"><span data-stu-id="cfb31-161">Here’s how it works:</span></span>

1. <span data-ttu-id="cfb31-162">Usługa Azure AD zapewnia o nazwie biblioteki wspólnej infrastruktury języka [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="cfb31-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="cfb31-163">Deweloperów i integratorów systemów. platforma można użyć tej biblioteki, możesz utworzyć i wdrożyć punkt końcowy usługi sieci web opartych na SCIM może nawiązywać połączenia usługi Azure AD z magazynu tożsamości dowolnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cfb31-163">System integrators and developers can use this library to create and deploy a SCIM-based web service endpoint capable of connecting Azure AD to any application’s identity store.</span></span>
2. <span data-ttu-id="cfb31-164">Mapowania są implementowane w usłudze sieci web do mapowania schematu użytkowników standardowych użytkowników schematu i protokół wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="cfb31-164">Mappings are implemented in the web service to map the standardized user schema to the user schema and protocol required by the application.</span></span>
3. <span data-ttu-id="cfb31-165">Końcowy adres URL jest zarejestrowany w usłudze Azure AD w ramach niestandardowych aplikacji w galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cfb31-165">The endpoint URL is registered in Azure AD as part of a custom application in the application gallery.</span></span>
4. <span data-ttu-id="cfb31-166">Użytkownicy i grupy są przypisane do tej aplikacji w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfb31-166">Users and groups are assigned to this application in Azure AD.</span></span> <span data-ttu-id="cfb31-167">Po przypisania są umieszczane w kolejce do synchronizacji w aplikacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="cfb31-167">Upon assignment, they are put into a queue to be synchronized to the target application.</span></span> <span data-ttu-id="cfb31-168">Proces synchronizacji obsługi kolejki jest uruchamiana co 20 minut.</span><span class="sxs-lookup"><span data-stu-id="cfb31-168">The synchronization process handling the queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="cfb31-169">Przykłady kodu</span><span class="sxs-lookup"><span data-stu-id="cfb31-169">Code Samples</span></span>
<span data-ttu-id="cfb31-170">Tego łatwiejsze, procesu to zbiór [przykłady kodu](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) pod warunkiem że utworzyć SCIM punkt końcowy usługi sieci web i Wykaż, automatyczne udostępnianie.</span><span class="sxs-lookup"><span data-stu-id="cfb31-170">To make this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="cfb31-171">Przykład jest dostawcy, który przechowuje plik z wierszami z wartościami rozdzielonymi przecinkami reprezentująca użytkowników i grup.</span><span class="sxs-lookup"><span data-stu-id="cfb31-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="cfb31-172">Druga to dostawcy, który działa na usługi Amazon Web Services tożsamość i zarządzanie dostępem.</span><span class="sxs-lookup"><span data-stu-id="cfb31-172">The other is of a provider that operates on the Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="cfb31-173">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="cfb31-173">**Prerequisites**</span></span>

* <span data-ttu-id="cfb31-174">Visual Studio 2013 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="cfb31-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="cfb31-175">Zestaw Azure SDK dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="cfb31-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="cfb31-176">Windows urządzenia, które obsługuje struktury programu ASP.NET 4.5 do użycia jako punkt końcowy SCIM.</span><span class="sxs-lookup"><span data-stu-id="cfb31-176">Windows machine that supports the ASP.NET framework 4.5 to be used as the SCIM endpoint.</span></span> <span data-ttu-id="cfb31-177">Tego komputera muszą być dostępne z chmury</span><span class="sxs-lookup"><span data-stu-id="cfb31-177">This machine must be accessible from the cloud</span></span>
* [<span data-ttu-id="cfb31-178">Subskrypcja platformy Azure w wersji próbnej lub licencjonowanej wersji programu Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="cfb31-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="cfb31-179">Przykład Amazon AWS wymaga bibliotek [usług AWS narzędzi dla programu Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span><span class="sxs-lookup"><span data-stu-id="cfb31-179">The Amazon AWS sample requires libraries from the [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="cfb31-180">Aby uzyskać więcej informacji zobacz plik README, uwzględnionych w próbce.</span><span class="sxs-lookup"><span data-stu-id="cfb31-180">For more information, see the README file included with the sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="cfb31-181">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="cfb31-181">Getting Started</span></span>
<span data-ttu-id="cfb31-182">Najprostszym sposobem wykonania SCIM punktu końcowego, który może zaakceptować żądania alokacji z usługi Azure AD jest do tworzenia i wdrażania przykładowy kod, który wyprowadza elastycznie użytkowników do pliku wartości rozdzielanych przecinkami (CSV).</span><span class="sxs-lookup"><span data-stu-id="cfb31-182">The easiest way to implement a SCIM endpoint that can accept provisioning requests from Azure AD is to build and deploy the code sample that outputs the provisioned users to a comma-separated value (CSV) file.</span></span>

<span data-ttu-id="cfb31-183">**Aby utworzyć punkt końcowy SCIM próbki:**</span><span class="sxs-lookup"><span data-stu-id="cfb31-183">**To create a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="cfb31-184">Pobierz przykładowy kod w [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="cfb31-184">Download the code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="cfb31-185">Rozpakuj pakiet i umieść go na komputerze z systemem Windows w lokalizacji, takich jak C:\AzureAD-BYOA-Provisioning-Samples\.</span><span class="sxs-lookup"><span data-stu-id="cfb31-185">Unzip the package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="cfb31-186">W tym folderze uruchom rozwiązania FileProvisioningAgent w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cfb31-186">In this folder, launch the FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="cfb31-187">Wybierz **Narzędzia > Menedżer pakietów biblioteki > konsoli Menedżera pakietów**i wykonaj następujące polecenia dla projektu FileProvisioningAgent można rozpoznać odwołań do rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="cfb31-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute the following commands for the FileProvisioningAgent project to resolve the solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="cfb31-188">Skompiluj projekt FileProvisioningAgent.</span><span class="sxs-lookup"><span data-stu-id="cfb31-188">Build the FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="cfb31-189">Uruchamianie aplikacji wiersza polecenia w systemie Windows (jako Administrator), a następnie użyj **cd** polecenia Zmień katalog na Twojej **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span><span class="sxs-lookup"><span data-stu-id="cfb31-189">Launch the Command Prompt application in Windows (as an Administrator), and use the **cd** command to change the directory to your **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="cfb31-190">Uruchom następujące polecenie, zastępując < adres ip > IP adresu lub nazwy domeny komputera z systemem Windows:</span><span class="sxs-lookup"><span data-stu-id="cfb31-190">Run the following command, replacing <ip-address> with the IP address or domain name of the Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="cfb31-191">W systemie Windows w obszarze **ustawienia systemu Windows > Sieć i Internet ustawienia**, wybierz pozycję **zapory systemu Windows > Zaawansowane ustawienia**i Utwórz **reguły ruchu przychodzącego** który Umożliwia przychodzący dostęp do portu 9000.</span><span class="sxs-lookup"><span data-stu-id="cfb31-191">In Windows under **Windows Settings > Network & Internet Settings**, select the **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access to port 9000.</span></span>
9. <span data-ttu-id="cfb31-192">W przypadku komputera z systemem Windows za routerem, router musi być skonfigurowany do wykonywania tłumaczenia dostępu do sieci między portu 9000, który jest połączenie z Internetem i portu 9000 na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="cfb31-192">If the Windows machine is behind a router, the router needs to be configured to perform Network Access Translation between its port 9000 that is exposed to the internet, and port 9000 on the Windows machine.</span></span> <span data-ttu-id="cfb31-193">Jest to wymagane dla usługi Azure AD można było uzyskać dostępu do tego punktu końcowego w chmurze.</span><span class="sxs-lookup"><span data-stu-id="cfb31-193">This is required for Azure AD to be able to access this endpoint in the cloud.</span></span>

<span data-ttu-id="cfb31-194">**Aby zarejestrować punkt końcowy SCIM przykładowych w usłudze Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="cfb31-194">**To register the sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="cfb31-195">Zaloguj się do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cfb31-195">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="cfb31-196">Przejdź do ** usługi Azure Active Directory > aplikacje dla przedsiębiorstw, a następnie wybierz **nowej aplikacji > wszystkie > Non galerii aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="cfb31-196">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="cfb31-197">Wprowadź nazwę aplikacji, a następnie kliknij przycisk **Dodaj** ikonę, aby utworzyć obiekt aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cfb31-197">Enter a name for your application, and click **Add** icon to create an app object.</span></span> <span data-ttu-id="cfb31-198">Utworzony obiekt aplikacji jest przeznaczony do reprezentowania aplikacji docelowej może być inicjowania obsługi administracyjnej i implementowania rejestracji jednokrotnej dla, a nie tylko punkt końcowy SCIM.</span><span class="sxs-lookup"><span data-stu-id="cfb31-198">The application object created is intended to represent the target app you would be provisioning to and implementing single sign-on for, and not just the SCIM endpoint.</span></span>
4. <span data-ttu-id="cfb31-199">Na ekranie wynikowy wybierz **inicjowania obsługi administracyjnej** kartę w lewej kolumnie.</span><span class="sxs-lookup"><span data-stu-id="cfb31-199">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="cfb31-200">W **inicjowania obsługi trybu** menu, wybierz opcję **automatyczne**.</span><span class="sxs-lookup"><span data-stu-id="cfb31-200">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="cfb31-201">![][2]
  *Rysunek 4: Konfigurowanie inicjowania obsługi w portalu Azure*</span><span class="sxs-lookup"><span data-stu-id="cfb31-201">![][2]
*Figure 4: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="cfb31-202">W **adres URL dzierżawy** wprowadź adres URL i port punktu końcowego SCIM dostępne za pośrednictwem Internetu.</span><span class="sxs-lookup"><span data-stu-id="cfb31-202">In the **Tenant URL** field, enter the internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="cfb31-203">Będzie to coś jak http://testmachine.contoso.com:9000 lub http://<ip-address>:9000/, gdzie < adres ip > jest internet IP udostępniany adres.</span><span class="sxs-lookup"><span data-stu-id="cfb31-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is the internet exposed IP address.</span></span>  
7. <span data-ttu-id="cfb31-204">Jeśli punkt końcowy SCIM wymaga tokenu elementu nośnego OAuth od wystawcy innego niż Azure AD, następnie skopiuj wymagany token elementu nośnego OAuth do opcjonalnego **klucz tajny tokenu** pola.</span><span class="sxs-lookup"><span data-stu-id="cfb31-204">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="cfb31-205">Jeśli to pole pozostanie puste, usługi Azure AD będą zawierać tokenu elementu nośnego OAuth wystawione przez usługi Azure AD z każdym żądaniem.</span><span class="sxs-lookup"><span data-stu-id="cfb31-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="cfb31-206">Aplikacje, które używają usługi Azure AD jako dostawca tożsamości może sprawdzić poprawność tej usługi Azure AD-wystawiony token.</span><span class="sxs-lookup"><span data-stu-id="cfb31-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="cfb31-207">Kliknij przycisk **Testuj połączenie** przycisk, aby podejmować próby nawiązania połączenia z punktem końcowym SCIM usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cfb31-207">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="cfb31-208">W przypadku awarii próby, wyświetlane informacje o błędzie.</span><span class="sxs-lookup"><span data-stu-id="cfb31-208">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="cfb31-209">Jeśli próby połączenia się pomyślnie aplikacji, należy kliknąć **zapisać** można zapisać poświadczeń administratora.</span><span class="sxs-lookup"><span data-stu-id="cfb31-209">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="cfb31-210">W **mapowania** sekcji, istnieją dwa zestawy wybieranych mapowań atrybutów: jeden dla obiektów użytkownika i jeden dla obiektów grupy.</span><span class="sxs-lookup"><span data-stu-id="cfb31-210">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="cfb31-211">Zaznacz każdą z nich Przejrzyj atrybuty, które są synchronizowane z usługą Azure Active Directory do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cfb31-211">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="cfb31-212">Atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania użytkowników i grup w aplikacji dla operacji update.</span><span class="sxs-lookup"><span data-stu-id="cfb31-212">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="cfb31-213">Wybierz przycisk Zapisz, aby zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="cfb31-213">Select the Save button to commit any changes.</span></span>
11. <span data-ttu-id="cfb31-214">W obszarze **ustawienia**, **zakres** pola definiuje, które użytkownicy i grupy są synchronizowane.</span><span class="sxs-lookup"><span data-stu-id="cfb31-214">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="cfb31-215">Wybranie "Synchronizacji tylko przypisane użytkowników i grup" (zalecane) będzie tylko synchronizować użytkownicy i grupy przypisane w **użytkowników i grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="cfb31-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="cfb31-216">Po zakończeniu konfiguracji zmienić **stan inicjowania obsługi administracyjnej** do **na**.</span><span class="sxs-lookup"><span data-stu-id="cfb31-216">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="cfb31-217">Kliknij przycisk **zapisać** można uruchomić usługi Azure AD, inicjowania obsługi usługi.</span><span class="sxs-lookup"><span data-stu-id="cfb31-217">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="cfb31-218">Jeśli synchronizacja przypisana tylko użytkownicy i grupy (zalecane), należy wybrać **użytkowników i grup** karcie i Przypisz użytkowników i/lub grup, które chcesz wykonać synchronizację.</span><span class="sxs-lookup"><span data-stu-id="cfb31-218">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="cfb31-219">Po rozpoczęciu synchronizacji początkowej, można użyć **dzienniki inspekcji** kartę do monitorowania postępu, który pokazuje wszystkie akcje wykonywane przez usługę inicjowania obsługi administracyjnej w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cfb31-219">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="cfb31-220">Aby uzyskać więcej informacji na temat usługi Azure AD, inicjowanie obsługi dzienników do odczytu, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="cfb31-220">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="cfb31-221">Ostatnim krokiem podczas weryfikowania próbki jest można otworzyć pliku TargetFile.csv w folderze \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="cfb31-221">The final step in verifying the sample is to open the TargetFile.csv file in the \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="cfb31-222">Po uruchomieniu procesu zastrzegania, ten plik zawiera szczegółowe informacje o całości przypisane i udostępnione użytkowników i grup.</span><span class="sxs-lookup"><span data-stu-id="cfb31-222">Once the provisioning process is run, this file shows the details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="cfb31-223">Biblioteki programistyczne</span><span class="sxs-lookup"><span data-stu-id="cfb31-223">Development libraries</span></span>
<span data-ttu-id="cfb31-224">Aby opracować własnej usługi sieci web, który jest zgodny ze specyfikacją SCIM, najpierw zapoznać się z następujących bibliotek obsługiwane przez firmę Microsoft w celu przyspieszenia procesu tworzenia:</span><span class="sxs-lookup"><span data-stu-id="cfb31-224">To develop your own web service that conforms to the SCIM specification, first familiarize yourself with the following libraries provided by Microsoft to help accelerate the development process:</span></span> 

1. <span data-ttu-id="cfb31-225">Wspólne biblioteki języka infrastruktury (CLI) dostępnych do użycia z językami oparte na infrastruktury, takich jak C#.</span><span class="sxs-lookup"><span data-stu-id="cfb31-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="cfb31-226">Jeden z tych bibliotek [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), deklaruje interfejsu Microsoft.SystemForCrossDomainIdentityManagement.IProvider, pokazane na poniższej ilustracji: A Developer przy użyciu bibliotek czy implementuje ten interfejs z klasy, która może być określone, objęty dostawcę.</span><span class="sxs-lookup"><span data-stu-id="cfb31-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in the following illustration:  A developer using the libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="cfb31-227">Biblioteki umożliwiają deweloperom wdrażanie usługi sieci web, który jest zgodny ze specyfikacją SCIM.</span><span class="sxs-lookup"><span data-stu-id="cfb31-227">The libraries enable the developer to deploy a web service that conforms to the SCIM specification.</span></span> <span data-ttu-id="cfb31-228">Usługi sieci web może być obsługiwany albo w ramach Internetowe usługi informacyjne lub dowolnego pliku wykonywalnego zestawu wspólną infrastrukturę języka.</span><span class="sxs-lookup"><span data-stu-id="cfb31-228">The web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="cfb31-229">Żądanie jest przetłumaczony na wywołania metody dostawcy, które mogłyby programowane przez dewelopera do działania na niektórych magazynu tożsamości.</span><span class="sxs-lookup"><span data-stu-id="cfb31-229">Request is translated into calls to the provider’s methods, which would be programmed by the developer to operate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="cfb31-230">[Express obsługi trasy](http://expressjs.com/guide/routing.html) są dostępne na potrzeby analizowania node.js żądania obiekty reprezentujące wywołania (zgodnie z definicją w specyfikacji SCIM), wprowadzone do usługi sieci web node.js.</span><span class="sxs-lookup"><span data-stu-id="cfb31-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by the SCIM specification), made to a node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="cfb31-231">Tworzenie punktu końcowego niestandardowych SCIM</span><span class="sxs-lookup"><span data-stu-id="cfb31-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="cfb31-232">Przy użyciu biblioteki interfejsu wiersza polecenia, deweloperzy przy użyciu tych bibliotek mogą być hostowane swoich usług w dowolnym pliku wykonywalnego zestawu wspólną infrastrukturę języka lub do internetowych usług informacyjnych.</span><span class="sxs-lookup"><span data-stu-id="cfb31-232">Using the CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="cfb31-233">Poniżej przedstawiono przykładowy kod w celu hostowania usługi w zestawie pliku wykonywalnego, pod adresem http://localhost:9000:</span><span class="sxs-lookup"><span data-stu-id="cfb31-233">Here is sample code for hosting a service within an executable assembly, at the address http://localhost:9000:</span></span> 

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

<span data-ttu-id="cfb31-234">Ta usługa musi mieć HTTP adres i serwera uwierzytelniania certyfikat której główny urząd certyfikacji jest jednym z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="cfb31-234">This service must have an HTTP address and server authentication certificate of which the root certification authority is one of the following:</span></span> 

* <span data-ttu-id="cfb31-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="cfb31-235">CNNIC</span></span>
* <span data-ttu-id="cfb31-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="cfb31-236">Comodo</span></span>
* <span data-ttu-id="cfb31-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="cfb31-237">CyberTrust</span></span>
* <span data-ttu-id="cfb31-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="cfb31-238">DigiCert</span></span>
* <span data-ttu-id="cfb31-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="cfb31-239">GeoTrust</span></span>
* <span data-ttu-id="cfb31-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="cfb31-240">GlobalSign</span></span>
* <span data-ttu-id="cfb31-241">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="cfb31-241">Go Daddy</span></span>
* <span data-ttu-id="cfb31-242">VeriSign</span><span class="sxs-lookup"><span data-stu-id="cfb31-242">Verisign</span></span>
* <span data-ttu-id="cfb31-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="cfb31-243">WoSign</span></span>

<span data-ttu-id="cfb31-244">Certyfikat uwierzytelniania serwera może być powiązana z portu na hoście z systemem Windows przy użyciu narzędzia powłoki sieciowej:</span><span class="sxs-lookup"><span data-stu-id="cfb31-244">A server authentication certificate can be bound to a port on a Windows host using the network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="cfb31-245">W tym miejscu wartość podana dla argumentu skrót certyfikatu jest odcisk palca certyfikatu, gdy wartość podana dla argumentu identyfikator appid jest umownym identyfikatorem globalnie unikatowy.</span><span class="sxs-lookup"><span data-stu-id="cfb31-245">Here, the value provided for the certhash argument is the thumbprint of the certificate, while the value provided for the appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="cfb31-246">Do obsługi usługi w usługach IIS, deweloper może kompilacji w zestawie CLA kod biblioteki z klasy o nazwie uruchamiania dla domyślnej przestrzeni nazw zestawu.</span><span class="sxs-lookup"><span data-stu-id="cfb31-246">To host the service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in the default namespace of the assembly.</span></span>  <span data-ttu-id="cfb31-247">Oto przykład takiego klasy:</span><span class="sxs-lookup"><span data-stu-id="cfb31-247">Here is a sample of such a class:</span></span> 

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

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="cfb31-248">Obsługa punktu końcowego uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="cfb31-248">Handling endpoint authentication</span></span>
<span data-ttu-id="cfb31-249">Żądania z usługi Azure Active Directory zawierać tokenu elementu nośnego OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="cfb31-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="cfb31-250">Każda usługa żądania odbierania powinna uwierzytelniać wystawca jako imieniu oczekiwanego dzierżawy usługi Azure Active Directory, do uzyskiwania dostępu do usługi sieci web Azure Active Directory Graph usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cfb31-250">Any service receiving the request should authenticate the issuer as being Azure Active Directory on behalf of the expected Azure Active Directory tenant, for access to the Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="cfb31-251">W tokenie, wystawca jest identyfikowany przez oświadczenie iss, takich jak "iss": "https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span><span class="sxs-lookup"><span data-stu-id="cfb31-251">In the token, the issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="cfb31-252">W tym przykładzie adres podstawowy wartość oświadczenia https://sts.windows.net, identyfikuje usługi Azure Active Directory jako wystawcy, podczas gdy segment adres względny, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, jest unikatowym identyfikatorem usługi Azure Active Directory Dzierżawca imieniu którego token został wystawiony.</span><span class="sxs-lookup"><span data-stu-id="cfb31-252">In this example, the base address of the claim value, https://sts.windows.net, identifies Azure Active Directory as the issuer, while the relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of the Azure Active Directory tenant on behalf of which the token was issued.</span></span>  <span data-ttu-id="cfb31-253">Jeśli token został wystawiony na uzyskiwanie dostępu do usługi sieci web Azure Active Directory Graph, identyfikator tej usługi, 00000002-0000-0000-c000-000000000000, powinien być w wartości oświadczenia lub tokenu.</span><span class="sxs-lookup"><span data-stu-id="cfb31-253">If the token was issued for accessing the Azure Active Directory Graph web service, then the identifier of that service, 00000002-0000-0000-c000-000000000000, should be in the value of the token’s aud claim.</span></span>  

<span data-ttu-id="cfb31-254">Deweloperzy przy użyciu bibliotek CLA obsługiwane przez firmę Microsoft do tworzenia usługi SCIM może uwierzytelnić żądania z usługi Azure Active Directory przy użyciu pakietu Microsoft.Owin.Security.ActiveDirectory, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cfb31-254">Developers using the CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using the Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="cfb31-255">U dostawcy należy zaimplementować właściwości Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior przez go zwracać metoda do wywołania po każdym uruchomieniu usługi:</span><span class="sxs-lookup"><span data-stu-id="cfb31-255">In a provider, implement the Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method to be called whenever the service is started:</span></span> 

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

2. <span data-ttu-id="cfb31-256">Dodaj następujący kod do tej metody, aby wszystkie żądania dla każdego z punktów końcowych usługi uwierzytelniony jako mając token wystawiony przez usługę Azure Active Directory w imieniu określonego dzierżawcę, aby uzyskać dostęp do usługi sieci web programu Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="cfb31-256">Add the following code to that method to have any request to any of the service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access to the Azure AD Graph web service:</span></span> 

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
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute the appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="cfb31-257">Schemat użytkowników i grup</span><span class="sxs-lookup"><span data-stu-id="cfb31-257">User and group schema</span></span>
<span data-ttu-id="cfb31-258">Usługa Azure Active Directory można udostępnić dwa typy zasobów do SCIM usług sieci web.</span><span class="sxs-lookup"><span data-stu-id="cfb31-258">Azure Active Directory can provision two types of resources to SCIM web services.</span></span>  <span data-ttu-id="cfb31-259">Te typy zasobów są użytkowników i grup.</span><span class="sxs-lookup"><span data-stu-id="cfb31-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="cfb31-260">Zasoby użytkownika są identyfikowane za pomocą identyfikatora schematu, urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, który jest dostępny w tej specyfikacji protokołu: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="cfb31-260">User resources are identified by the schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="cfb31-261">Domyślne mapowanie atrybutów użytkowników w usłudze Azure Active Directory w atrybutach urn: ietf:params:scim:schemas:extension:enterprise:2.0:User zasobów znajduje się w tabeli 1, poniżej.</span><span class="sxs-lookup"><span data-stu-id="cfb31-261">The default mapping of the attributes of users in Azure Active Directory to the attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="cfb31-262">Grupy zasobów są identyfikowane za pomocą identyfikatora schematu http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="cfb31-262">Group resources are identified by the schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="cfb31-263">Tabela 2, poniżej przedstawiono domyślne mapowanie atrybutów grup w usłudze Azure Active Directory w atrybutach http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group zasobów.</span><span class="sxs-lookup"><span data-stu-id="cfb31-263">Table 2, below, shows the default mapping of the attributes of groups in Azure Active Directory to the attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="cfb31-264">Tabela 1: Domyślne mapowanie atrybutu użytkownika</span><span class="sxs-lookup"><span data-stu-id="cfb31-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="cfb31-265">Azure użytkownika usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfb31-265">Azure Active Directory user</span></span> | <span data-ttu-id="cfb31-266">urn: ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="cfb31-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="cfb31-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="cfb31-267">IsSoftDeleted</span></span> |<span data-ttu-id="cfb31-268">Aktywne</span><span class="sxs-lookup"><span data-stu-id="cfb31-268">active</span></span> |
| <span data-ttu-id="cfb31-269">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="cfb31-269">displayName</span></span> |<span data-ttu-id="cfb31-270">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="cfb31-270">displayName</span></span> |
| <span data-ttu-id="cfb31-271">TelephoneNumber faksu</span><span class="sxs-lookup"><span data-stu-id="cfb31-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="cfb31-272">.value phoneNumbers [eq typu "faks"]</span><span class="sxs-lookup"><span data-stu-id="cfb31-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="cfb31-273">Imię</span><span class="sxs-lookup"><span data-stu-id="cfb31-273">givenName</span></span> |<span data-ttu-id="cfb31-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="cfb31-274">name.givenName</span></span> |
| <span data-ttu-id="cfb31-275">Stanowisko</span><span class="sxs-lookup"><span data-stu-id="cfb31-275">jobTitle</span></span> |<span data-ttu-id="cfb31-276">Tytuł</span><span class="sxs-lookup"><span data-stu-id="cfb31-276">title</span></span> |
| <span data-ttu-id="cfb31-277">Poczty</span><span class="sxs-lookup"><span data-stu-id="cfb31-277">mail</span></span> |<span data-ttu-id="cfb31-278">.value wiadomości e-mail [eq typu "Praca"]</span><span class="sxs-lookup"><span data-stu-id="cfb31-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="cfb31-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="cfb31-279">mailNickname</span></span> |<span data-ttu-id="cfb31-280">externalId</span><span class="sxs-lookup"><span data-stu-id="cfb31-280">externalId</span></span> |
| <span data-ttu-id="cfb31-281">Menedżer</span><span class="sxs-lookup"><span data-stu-id="cfb31-281">manager</span></span> |<span data-ttu-id="cfb31-282">Menedżer</span><span class="sxs-lookup"><span data-stu-id="cfb31-282">manager</span></span> |
| <span data-ttu-id="cfb31-283">Telefon komórkowy</span><span class="sxs-lookup"><span data-stu-id="cfb31-283">mobile</span></span> |<span data-ttu-id="cfb31-284">.value phoneNumbers [eq typu "mobile"]</span><span class="sxs-lookup"><span data-stu-id="cfb31-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="cfb31-285">Identyfikator obiektu</span><span class="sxs-lookup"><span data-stu-id="cfb31-285">objectId</span></span> |<span data-ttu-id="cfb31-286">id</span><span class="sxs-lookup"><span data-stu-id="cfb31-286">id</span></span> |
| <span data-ttu-id="cfb31-287">KodPocztowy</span><span class="sxs-lookup"><span data-stu-id="cfb31-287">postalCode</span></span> |<span data-ttu-id="cfb31-288">.postalCode adresów [eq typu "Praca"]</span><span class="sxs-lookup"><span data-stu-id="cfb31-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="cfb31-289">Adresy serwerów proxy</span><span class="sxs-lookup"><span data-stu-id="cfb31-289">proxy-Addresses</span></span> |<span data-ttu-id="cfb31-290">wiadomości e-mail [Wpisz eq "other"]. Wartość</span><span class="sxs-lookup"><span data-stu-id="cfb31-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="cfb31-291">Physical dostarczania-OfficeName</span><span class="sxs-lookup"><span data-stu-id="cfb31-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="cfb31-292">adresy [Wpisz eq "other"]. Sformatowany</span><span class="sxs-lookup"><span data-stu-id="cfb31-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="cfb31-293">Adres</span><span class="sxs-lookup"><span data-stu-id="cfb31-293">streetAddress</span></span> |<span data-ttu-id="cfb31-294">.streetAddress adresów [eq typu "Praca"]</span><span class="sxs-lookup"><span data-stu-id="cfb31-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="cfb31-295">nazwisko</span><span class="sxs-lookup"><span data-stu-id="cfb31-295">surname</span></span> |<span data-ttu-id="cfb31-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="cfb31-296">name.familyName</span></span> |
| <span data-ttu-id="cfb31-297">Numer telefonu</span><span class="sxs-lookup"><span data-stu-id="cfb31-297">telephone-Number</span></span> |<span data-ttu-id="cfb31-298">.value phoneNumbers [eq typu "Praca"]</span><span class="sxs-lookup"><span data-stu-id="cfb31-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="cfb31-299">PrincipalName użytkownika</span><span class="sxs-lookup"><span data-stu-id="cfb31-299">user-PrincipalName</span></span> |<span data-ttu-id="cfb31-300">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="cfb31-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="cfb31-301">Tabela 2: Domyślne grupy atrybutów mapowanie</span><span class="sxs-lookup"><span data-stu-id="cfb31-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="cfb31-302">Grupa usługi Active Directory systemu Azure</span><span class="sxs-lookup"><span data-stu-id="cfb31-302">Azure Active Directory group</span></span> | <span data-ttu-id="cfb31-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="cfb31-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="cfb31-304">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="cfb31-304">displayName</span></span> |<span data-ttu-id="cfb31-305">externalId</span><span class="sxs-lookup"><span data-stu-id="cfb31-305">externalId</span></span> |
| <span data-ttu-id="cfb31-306">Poczty</span><span class="sxs-lookup"><span data-stu-id="cfb31-306">mail</span></span> |<span data-ttu-id="cfb31-307">.value wiadomości e-mail [eq typu "Praca"]</span><span class="sxs-lookup"><span data-stu-id="cfb31-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="cfb31-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="cfb31-308">mailNickname</span></span> |<span data-ttu-id="cfb31-309">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="cfb31-309">displayName</span></span> |
| <span data-ttu-id="cfb31-310">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="cfb31-310">members</span></span> |<span data-ttu-id="cfb31-311">Elementy członkowskie</span><span class="sxs-lookup"><span data-stu-id="cfb31-311">members</span></span> |
| <span data-ttu-id="cfb31-312">Identyfikator obiektu</span><span class="sxs-lookup"><span data-stu-id="cfb31-312">objectId</span></span> |<span data-ttu-id="cfb31-313">id</span><span class="sxs-lookup"><span data-stu-id="cfb31-313">id</span></span> |
| <span data-ttu-id="cfb31-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="cfb31-314">proxyAddresses</span></span> |<span data-ttu-id="cfb31-315">wiadomości e-mail [Wpisz eq "other"]. Wartość</span><span class="sxs-lookup"><span data-stu-id="cfb31-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="cfb31-316">Inicjowanie obsługi użytkowników i anulowanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="cfb31-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="cfb31-317">Na poniższej ilustracji pokazano komunikatów wysyła usługi Azure Active Directory z usługą SCIM do zarządzania cyklem życia w innym magazynie tożsamości użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cfb31-317">The following illustration shows the messages that Azure Active Directory sends to a SCIM service to manage the lifecycle of a user in another identity store.</span></span> <span data-ttu-id="cfb31-318">Na diagramie przedstawiono również sposób usługa SCIM implementowane przy użyciu biblioteki interfejsu wiersza polecenia obsługiwane przez firmę Microsoft do budowy, się, że takie usługi tłumaczenia te żądania na wywołania metod dostawcy.</span><span class="sxs-lookup"><span data-stu-id="cfb31-318">The diagram also shows how a SCIM service implemented using the CLI libraries provided by Microsoft for building such services translate those requests into calls to the methods of a provider.</span></span>  

<span data-ttu-id="cfb31-319">![][4]
*Rysunek 5: Użytkownik aprowizację i anulowanie obsługi sekwencji*</span><span class="sxs-lookup"><span data-stu-id="cfb31-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="cfb31-320">Usługa Azure Active Directory korzysta z usługi dla użytkownika z wartością atrybutu externalId dopasowywanie mailNickname wartość atrybutu użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cfb31-320">Azure Active Directory queries the service for a user with an externalId attribute value matching the mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="cfb31-321">Zapytanie jest wyrażony jako żądania protokołu HTTP (Hypertext Transfer), np. w tym przykładzie, w którym jyoung znajduje się przykład mailNickname użytkownika w usłudze Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="cfb31-321">The query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="cfb31-322">Jeśli usługa został zbudowany przy użyciu bibliotek wspólną infrastrukturę języka obsługiwane przez firmę Microsoft dla implementacji usługi SCIM, żądanie jest przetłumaczony na wywołanie do metody zapytania dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="cfb31-322">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span>  <span data-ttu-id="cfb31-323">Podpis metody jest następujący:</span><span class="sxs-lookup"><span data-stu-id="cfb31-323">Here is the signature of that method:</span></span> 
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
  <span data-ttu-id="cfb31-324">W tym miejscu znajduje się definicja interfejsu Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters:</span><span class="sxs-lookup"><span data-stu-id="cfb31-324">Here is the definition of the Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
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
  <span data-ttu-id="cfb31-325">W poniższym przykładzie zapytanie dla użytkownika z danej wartości dla atrybutu externalId wartości Argumenty przekazane do metody zapytania są:</span><span class="sxs-lookup"><span data-stu-id="cfb31-325">In the following sample of a query for a user with a given value for the externalId attribute, values of the arguments passed to the Query method are:</span></span> 
  * <span data-ttu-id="cfb31-326">Parametry. AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="cfb31-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="cfb31-327">Parametry. AlternateFilters.ElementAt(0). AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="cfb31-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="cfb31-328">Parametry. AlternateFilters.ElementAt(0). OperatorPorównania: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="cfb31-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="cfb31-329">Parametry. AlternateFilter.ElementAt(0). ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="cfb31-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="cfb31-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin. Identyfikator żądania"]</span><span class="sxs-lookup"><span data-stu-id="cfb31-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="cfb31-331">Jeśli odpowiedź na zapytanie do usługi sieci web dla użytkownika z wartością atrybutu externalId, która jest zgodna z wartością atrybutu mailNickname użytkownika nie zwraca żadnych użytkowników, następnie usługi Azure Active Directory żąda czy usługa udostępnić odpowiednie do tego użytkownika w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cfb31-331">If the response to a query to the web service for a user with an externalId attribute value that matches the mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that the service provision a user corresponding to the one in Azure Active Directory.</span></span>  <span data-ttu-id="cfb31-332">Oto przykład takiego żądania:</span><span class="sxs-lookup"><span data-stu-id="cfb31-332">Here is an example of such a request:</span></span> 
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
  <span data-ttu-id="cfb31-333">Biblioteki wspólną infrastrukturę języka obsługiwane przez firmę Microsoft dla implementacji usługi SCIM przekłada to żądanie do wywołania metody Create dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="cfb31-333">The Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call to the Create method of the service’s provider.</span></span>  <span data-ttu-id="cfb31-334">Metoda Create ma podpis:</span><span class="sxs-lookup"><span data-stu-id="cfb31-334">The Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="cfb31-335">W żądaniu skierowanym do obsługi administracyjnej użytkownika wartość argumentu zasobów jest wystąpieniem Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="cfb31-335">In a request to provision a user, the value of the resource argument is an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="cfb31-336">Klasa Core2EnterpriseUser zdefiniowany w bibliotece Microsoft.SystemForCrossDomainIdentityManagement.Schemas.</span><span class="sxs-lookup"><span data-stu-id="cfb31-336">Core2EnterpriseUser class, defined in the Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="cfb31-337">Jeśli żądanie do udostępnienia użytkownik zakończy się powodzeniem, następnie implementacji metody powinien zwrócić wystąpienia Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="cfb31-337">If the request to provision the user succeeds, then the implementation of the method is expected to return an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="cfb31-338">Klasa Core2EnterpriseUser o wartość właściwości identyfikator ustawioną Unikatowy identyfikator nowo aprowizowanej użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cfb31-338">Core2EnterpriseUser class, with the value of the Identifier property set to the unique identifier of the newly provisioned user.</span></span>  

3. <span data-ttu-id="cfb31-339">Do zaktualizowania użytkownika istnieje w magazynie tożsamości przez SCIM, Azure Active Directory przechodzi przez zażądanie bieżący stan tego użytkownika z usługi z żądaniem, takich jak:</span><span class="sxs-lookup"><span data-stu-id="cfb31-339">To update a user known to exist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting the current state of that user from the service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="cfb31-340">W usłudze utworzony przy użyciu bibliotek wspólną infrastrukturę języka obsługiwane przez firmę Microsoft dla implementacji usługi SCIM żądanie jest przetłumaczony na wywołanie do metody pobierania dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="cfb31-340">In a service built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, the request is translated into a call to the Retrieve method of the service’s provider.</span></span>  <span data-ttu-id="cfb31-341">Oto podpis metody pobierania:</span><span class="sxs-lookup"><span data-stu-id="cfb31-341">Here is the signature of the Retrieve method:</span></span> 
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
  <span data-ttu-id="cfb31-342">W tym przykładzie żądanie, aby pobrać bieżący stan użytkownika wartości właściwości obiektu dostarczonych jako wartość argumentu parametry są następujące:</span><span class="sxs-lookup"><span data-stu-id="cfb31-342">In the example of a request to retrieve the current state of a user, the values of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="cfb31-343">Identyfikator: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="cfb31-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="cfb31-344">SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="cfb31-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="cfb31-345">Jeśli atrybut odwołania ma zostać zaktualizowany, a następnie usługi Azure Active Directory wysyła zapytanie do usługi, aby określić, czy bieżąca wartość atrybutu odwołania magazynu tożsamości fronted przez usługę już jest zgodna z wartością tego atrybutu w usłudze Azure Active Katalog.</span><span class="sxs-lookup"><span data-stu-id="cfb31-345">If a reference attribute is to be updated, then Azure Active Directory queries the service to determine whether or not the current value of the reference attribute in the identity store fronted by the service already matches the value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="cfb31-346">W przypadku użytkowników jedyny atrybut, z których bieżąca wartość jest poddawany kwerendzie w ten sposób jest atrybutem menedżera.</span><span class="sxs-lookup"><span data-stu-id="cfb31-346">For users, the only attribute of which the current value is queried in this way is the manager attribute.</span></span> <span data-ttu-id="cfb31-347">Oto przykład żądanie, aby ustalić, czy atrybut menedżera obiektu określonego użytkownika aktualnie ma określoną wartość:</span><span class="sxs-lookup"><span data-stu-id="cfb31-347">Here is an example of a request to determine whether the manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="cfb31-348">Wartość parametru zapytania atrybuty, identyfikator, oznacza, że, jakby istniał obiektu użytkownika spełnia wyrażenie dostarczonych jako wartość parametru zapytania filtru, a następnie usługę powinien odpowiadać, podając urn: ietf:params:scim:schemas:core:2.0:User lub zasób urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, z uwzględnieniem tylko wartości atrybutu id tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="cfb31-348">The value of the attributes query parameter, id, signifies that if a user object exists that satisfies the expression provided as the value of the filter query parameter, then the service is expected to respond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only the value of that resource’s id attribute.</span></span>  <span data-ttu-id="cfb31-349">Wartość **identyfikator** atrybutu jest znany obiekt żądający.</span><span class="sxs-lookup"><span data-stu-id="cfb31-349">The value of the **id** attribute is known to the requestor.</span></span> <span data-ttu-id="cfb31-350">Znajduje się on w wartości parametru zapytania filtru; Celem pyta jest rzeczywiście żądanie minimalnego reprezentacja zasobu spełniające wyrażenie filtru jako ze wskazaniem, czy istnieje takiego obiektu.</span><span class="sxs-lookup"><span data-stu-id="cfb31-350">It is included in the value of the filter query parameter; the purpose of asking for it is actually to request a minimal representation of a resource that satisfying the filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="cfb31-351">Jeśli usługa został zbudowany przy użyciu bibliotek wspólną infrastrukturę języka obsługiwane przez firmę Microsoft dla implementacji usługi SCIM, żądanie jest przetłumaczony na wywołanie do metody zapytania dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="cfb31-351">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span> <span data-ttu-id="cfb31-352">Wartość właściwości obiektu dostarczonych jako wartość argumentu parametry są następujące:</span><span class="sxs-lookup"><span data-stu-id="cfb31-352">The value of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="cfb31-353">Parametry. AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="cfb31-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="cfb31-354">Parametry. AlternateFilters.ElementAt(x). AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="cfb31-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="cfb31-355">Parametry. AlternateFilters.ElementAt(x). OperatorPorównania: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="cfb31-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="cfb31-356">Parametry. AlternateFilter.ElementAt(x). ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="cfb31-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="cfb31-357">Parametry. AlternateFilters.ElementAt(y). AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="cfb31-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="cfb31-358">Parametry. AlternateFilters.ElementAt(y). OperatorPorównania: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="cfb31-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="cfb31-359">Parametry. AlternateFilter.ElementAt(y). ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="cfb31-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="cfb31-360">Parametry. RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="cfb31-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="cfb31-361">Parametry. SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="cfb31-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="cfb31-362">W tym miejscu wartość indeksu x może być równa 0 i wartość y indeksu może być równa 1, lub wartość x może być równa 1 i wartości y może mieć wartość 0, w zależności od kolejność wyrażenia parametru zapytania filtru.</span><span class="sxs-lookup"><span data-stu-id="cfb31-362">Here, the value of the index x may be 0 and the value of the index y may be 1, or the value of x may be 1 and the value of y may be 0, depending on the order of the expressions of the filter query parameter.</span></span>   

5. <span data-ttu-id="cfb31-363">Oto przykład żądania z usługi Azure Active Directory z usługą SCIM do zaktualizowania użytkownika:</span><span class="sxs-lookup"><span data-stu-id="cfb31-363">Here is an example of a request from Azure Active Directory to an SCIM service to update a user:</span></span> 
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
  <span data-ttu-id="cfb31-364">Implementowanie usług SCIM z bibliotekami wspólną infrastrukturę języka Microsoft przekłada żądania do wywołania metody aktualizacji dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="cfb31-364">The Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate the request into a call to the Update method of the service’s provider.</span></span> <span data-ttu-id="cfb31-365">Oto podpis metody aktualizacji:</span><span class="sxs-lookup"><span data-stu-id="cfb31-365">Here is the signature of the Update method:</span></span> 
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
    <span data-ttu-id="cfb31-366">W tym przykładzie żądania do zaktualizowania użytkownika dostarczony jako wartość argumentu poprawki obiekt ma wartości tych właściwości:</span><span class="sxs-lookup"><span data-stu-id="cfb31-366">In the example of a request to update a user, the object provided as the value of the patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="cfb31-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="cfb31-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="cfb31-368">ResourceIdentifier.SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="cfb31-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="cfb31-369">(PatchRequest jako PatchRequest2). Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="cfb31-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="cfb31-370">(PatchRequest jako PatchRequest2). Operations.ElementAt(0). OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="cfb31-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="cfb31-371">(PatchRequest jako PatchRequest2). Operations.ElementAt(0). Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="cfb31-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="cfb31-372">(PatchRequest jako PatchRequest2). Operations.ElementAt(0). Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="cfb31-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="cfb31-373">(PatchRequest jako PatchRequest2). Operations.ElementAt(0). Value.ElementAt(0). Odwołanie: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="cfb31-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="cfb31-374">(PatchRequest jako PatchRequest2). Operations.ElementAt(0). Value.ElementAt(0). Wartość: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="cfb31-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="cfb31-375">Aby anulować aprowizację użytkownika z tożsamości magazynu przez usługę SCIM, usługi Azure AD wysyła żądanie takie jak:</span><span class="sxs-lookup"><span data-stu-id="cfb31-375">To de-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="cfb31-376">Jeśli usługa został zbudowany przy użyciu bibliotek wspólną infrastrukturę języka obsługiwane przez firmę Microsoft dla implementacji usługi SCIM, żądanie jest przetłumaczony na wywołanie do metody Delete dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="cfb31-376">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Delete method of the service’s provider.</span></span>   <span data-ttu-id="cfb31-377">Ta metoda ma podpis:</span><span class="sxs-lookup"><span data-stu-id="cfb31-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="cfb31-378">Obiekt udostępniany jako wartość argumentu resourceIdentifier ma wartości tych właściwości w tym przykładzie żądanie, aby anulować aprowizację użytkownika:</span><span class="sxs-lookup"><span data-stu-id="cfb31-378">The object provided as the value of the resourceIdentifier argument has these property values in the example of a request to de-provision a user:</span></span> 
  
  * <span data-ttu-id="cfb31-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="cfb31-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="cfb31-380">ResourceIdentifier.SchemaIdentifier: "urn: ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="cfb31-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="cfb31-381">Grupy aprowizację i anulowanie obsługi</span><span class="sxs-lookup"><span data-stu-id="cfb31-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="cfb31-382">Na poniższej ilustracji pokazano komunikatów wysyła Azure AcD z usługą SCIM do zarządzania cyklem życia grupy w innym magazynie tożsamości.</span><span class="sxs-lookup"><span data-stu-id="cfb31-382">The following illustration shows the messages that Azure AcD sends to a SCIM service to manage the lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="cfb31-383">Te komunikaty różnią się od komunikaty dotyczące użytkowników na trzy sposoby:</span><span class="sxs-lookup"><span data-stu-id="cfb31-383">Those messages differ from the messages pertaining to users in three ways:</span></span> 

* <span data-ttu-id="cfb31-384">Schemat zasób grupy jest rozpoznawany jako http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="cfb31-384">The schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="cfb31-385">Żądania pobrania grup stanowić atrybut elementów członkowskich mają być wykluczone z dowolnego zasobu w odpowiedzi na żądanie.</span><span class="sxs-lookup"><span data-stu-id="cfb31-385">Requests to retrieve groups stipulate that the members attribute is to be excluded from any resource provided in response to the request.</span></span>  
* <span data-ttu-id="cfb31-386">Żądania, aby ustalić, czy jest atrybut odwołania ma określoną wartość są żądania dotyczące elementów członkowskich atrybutu.</span><span class="sxs-lookup"><span data-stu-id="cfb31-386">Requests to determine whether a reference attribute has a certain value are requests about the members attribute.</span></span>  

<span data-ttu-id="cfb31-387">![][5]
*Rysunek 6: Grupy aprowizację i anulowanie obsługi sekwencji*</span><span class="sxs-lookup"><span data-stu-id="cfb31-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="cfb31-388">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="cfb31-388">Related articles</span></span>
* [<span data-ttu-id="cfb31-389">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cfb31-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="cfb31-390">Automatyzowanie użytkownika udostępniania/anulowania obsługi do aplikacji SaaS</span><span class="sxs-lookup"><span data-stu-id="cfb31-390">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="cfb31-391">Dostosowywanie mapowań atrybutów do inicjowania obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="cfb31-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="cfb31-392">Tworzenie wyrażeń na potrzeby mapowań atrybutów</span><span class="sxs-lookup"><span data-stu-id="cfb31-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="cfb31-393">Filtry zakresu dla Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="cfb31-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="cfb31-394">Powiadomienia aprowizacji kont</span><span class="sxs-lookup"><span data-stu-id="cfb31-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="cfb31-395">Lista samouczków dotyczących sposobów integracji aplikacji SaaS</span><span class="sxs-lookup"><span data-stu-id="cfb31-395">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
