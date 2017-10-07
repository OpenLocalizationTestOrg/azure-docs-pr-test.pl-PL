---
title: "aaaManage pierwszy interfejs API usługi Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dodać operacje toocreate interfejsów API i wprowadzenie do interfejsu API zarządzania."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="2be1e-103">Zarządzanie pierwszym interfejsem API w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="2be1e-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="2be1e-104"><a name="overview"> </a>Omówienie</span><span class="sxs-lookup"><span data-stu-id="2be1e-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="2be1e-105">W tym przewodniku pokazano, jak tooquickly Rozpoczynanie pracy za pomocą usługi Azure API Management i upewnij się Twoje pierwsze wywołanie interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2be1e-105">This guide shows you how tooquickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="2be1e-106"><a name="concepts"> </a>Co to jest usługa Azure API Management?</span><span class="sxs-lookup"><span data-stu-id="2be1e-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="2be1e-107">Można użyć dowolnego zaplecza Azure API Management tootake i uruchomić pełni funkcjonalnymi program interfejsu API na ich podstawie.</span><span class="sxs-lookup"><span data-stu-id="2be1e-107">You can use Azure API Management tootake any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="2be1e-108">Typowe scenariusze obejmują:</span><span class="sxs-lookup"><span data-stu-id="2be1e-108">Common scenarios include:</span></span>

* <span data-ttu-id="2be1e-109">**Zabezpieczanie infrastruktury mobilnej** przez uzyskanie dostępu bramowego z kluczami interfejsu API, zapobieganie atakom DOS przy użyciu ograniczania przepływności lub korzystanie z zaawansowanych zasad zabezpieczeń, takich jak sprawdzanie poprawności tokenu JWT.</span><span class="sxs-lookup"><span data-stu-id="2be1e-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="2be1e-110">**Włączanie ekosystemami partnerów niezależnego dostawcy oprogramowania** oferując dołączania szybkiego partnera przez dewelopera hello portalu i tworzenia toodecouple fasad interfejsu API z wewnętrznej implementacji, które nie są dojrzałe do użycia przez partnera.</span><span class="sxs-lookup"><span data-stu-id="2be1e-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through hello developer portal and building an API facade toodecouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="2be1e-111">**Uruchomiony program wewnętrznego interfejsu API** oferując scentralizowanej lokalizacji hello organizacji toocommunicate o dostępności hello i najnowszych zmian tooAPIs, uzyskania dostępu na podstawie organizacyjnego kont bramowego wszystkie oparte na bezpiecznego kanału między Brama Hello interfejsu API i hello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2be1e-111">**Running an internal API program** by offering a centralized location for hello organization toocommunicate about hello availability and latest changes tooAPIs, gating access based on organizational accounts, all based on a secured channel between hello API gateway and hello backend.</span></span>

<span data-ttu-id="2be1e-112">Hello system składa się z hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="2be1e-112">hello system is made up of hello following components:</span></span>

* <span data-ttu-id="2be1e-113">Witaj **bramy interfejsu API** jest punkt końcowy hello który:</span><span class="sxs-lookup"><span data-stu-id="2be1e-113">hello **API gateway** is hello endpoint that:</span></span>
  
  * <span data-ttu-id="2be1e-114">Akceptuje wywołuje interfejs API i kieruje je zapleczy tooyour.</span><span class="sxs-lookup"><span data-stu-id="2be1e-114">Accepts API calls and routes them tooyour backends.</span></span>
  * <span data-ttu-id="2be1e-115">Weryfikowanie kluczy interfejsu API, tokenów JWT, certyfikatów i innych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="2be1e-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="2be1e-116">Wymuszanie przydziałów użycia i ograniczeń liczby wywołań.</span><span class="sxs-lookup"><span data-stu-id="2be1e-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="2be1e-117">Przy użyciu interfejsu API na bieżąco hello bez modyfikacji kodu.</span><span class="sxs-lookup"><span data-stu-id="2be1e-117">Transforms your API on hello fly without code modifications.</span></span>
  * <span data-ttu-id="2be1e-118">Buforowanie odpowiedzi zaplecza w skonfigurowanym miejscu.</span><span class="sxs-lookup"><span data-stu-id="2be1e-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="2be1e-119">Rejestrowanie w dzienniku metadanych wywołań w celu analizy.</span><span class="sxs-lookup"><span data-stu-id="2be1e-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="2be1e-120">Witaj **portal wydawcy** jest hello interfejsu administracyjnego skonfigurowanie programu interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2be1e-120">hello **publisher portal** is hello administrative interface where you set up your API program.</span></span> <span data-ttu-id="2be1e-121">Jego zastosowania to:</span><span class="sxs-lookup"><span data-stu-id="2be1e-121">Use it to:</span></span>
  
  * <span data-ttu-id="2be1e-122">Definiowanie lub importowanie schematu interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2be1e-122">Define or import API schema.</span></span>
  * <span data-ttu-id="2be1e-123">Tworzenie pakietów interfejsów API do produktów.</span><span class="sxs-lookup"><span data-stu-id="2be1e-123">Package APIs into products.</span></span>
  * <span data-ttu-id="2be1e-124">Skonfiguruj zasady, takie jak przydziałów lub przekształcenia na powitania interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="2be1e-124">Set up policies like quotas or transformations on hello APIs.</span></span>
  * <span data-ttu-id="2be1e-125">Uzyskiwanie szczegółowych informacji analitycznych.</span><span class="sxs-lookup"><span data-stu-id="2be1e-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="2be1e-126">Zarządzanie użytkownikami.</span><span class="sxs-lookup"><span data-stu-id="2be1e-126">Manage users.</span></span>
* <span data-ttu-id="2be1e-127">Witaj **portalu dla deweloperów** służy jako hello głównego witrynę internetową dla deweloperów, gdzie można:</span><span class="sxs-lookup"><span data-stu-id="2be1e-127">hello **developer portal** serves as hello main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="2be1e-128">Czytanie dokumentacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2be1e-128">Read API documentation.</span></span>
  * <span data-ttu-id="2be1e-129">Wypróbuj interfejsu API za pomocą konsoli interakcyjne hello.</span><span class="sxs-lookup"><span data-stu-id="2be1e-129">Try out an API via hello interactive console.</span></span>
  * <span data-ttu-id="2be1e-130">Utworzyć konto i Subskrypcja klucze tooget interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2be1e-130">Create an account and subscribe tooget API keys.</span></span>
  * <span data-ttu-id="2be1e-131">Zyskanie dostępu do analiz własnego użycia.</span><span class="sxs-lookup"><span data-stu-id="2be1e-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="2be1e-132"><a name="create-service-instance"> </a>Tworzenie wystąpienia usługi API Management</span><span class="sxs-lookup"><span data-stu-id="2be1e-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="2be1e-133">toocomplete tego samouczka jest potrzebne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2be1e-133">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="2be1e-134">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="2be1e-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="2be1e-135">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][Azure Free Trial].</span><span class="sxs-lookup"><span data-stu-id="2be1e-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="2be1e-136">pierwszym krokiem Hello w pracy z interfejsu API zarządzania jest toocreate wystąpienie usługi.</span><span class="sxs-lookup"><span data-stu-id="2be1e-136">hello first step in working with API Management is toocreate a service instance.</span></span> <span data-ttu-id="2be1e-137">Zaloguj się toohello [Azure Portal] [ Azure Portal] i kliknij przycisk **nowy**, **sieci Web i mobilność**, **zarządzanie interfejsami API**.</span><span class="sxs-lookup"><span data-stu-id="2be1e-137">Sign in toohello [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![Nowe wystąpienie usługi API Management][api-management-create-instance-menu]

<span data-ttu-id="2be1e-139">Aby uzyskać **nazwa**, określ toouse nazwę domeny podrzędnej unikatowy adres URL usługi hello.</span><span class="sxs-lookup"><span data-stu-id="2be1e-139">For **Name**, specify a unique sub-domain name toouse for hello service URL.</span></span>

<span data-ttu-id="2be1e-140">Wybierz żądaną hello **subskrypcji**, **grupy zasobów** i **lokalizacji** wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="2be1e-140">Choose hello desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="2be1e-141">Wprowadź **firmy Contoso, Ltd.** dla hello **nazwa organizacji**i wprowadź swój adres e-mail w hello **E-Mail administratora** pola.</span><span class="sxs-lookup"><span data-stu-id="2be1e-141">Enter **Contoso Ltd.** for hello **Organization Name**, and enter your email address in hello **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="2be1e-142">Ten adres e-mail jest używany dla powiadomień z hello system zarządzania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2be1e-142">This email address is used for notifications from hello API Management system.</span></span> <span data-ttu-id="2be1e-143">Aby uzyskać więcej informacji, zobacz [jak tooconfigure powiadomienia i szablonów w usłudze Azure API Management wiadomości e-mail][How tooconfigure notifications and email templates in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2be1e-143">For more information, see [How tooconfigure notifications and email templates in Azure API Management][How tooconfigure notifications and email templates in Azure API Management].</span></span>
> 
> 

![Nowa usługa API Management][api-management-create-instance-step1]

<span data-ttu-id="2be1e-145">Wystąpienia usługi API Management są dostępne w trzech warstwach: Deweloper, Standardowej i Premium.</span><span class="sxs-lookup"><span data-stu-id="2be1e-145">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="2be1e-146">jest Hello warstwy deweloperów do tworzenia, testowania i programy pilotażowe interfejsu API, gdzie wysokiej dostępności nie ma znaczenia.</span><span class="sxs-lookup"><span data-stu-id="2be1e-146">hello Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="2be1e-147">W hello Standard i Premium warstw można skalować Twojej toohandle liczba zarezerwowanych jednostek większego ruchu.</span><span class="sxs-lookup"><span data-stu-id="2be1e-147">In hello Standard and Premium tiers, you can scale your reserved unit count toohandle more traffic.</span></span> <span data-ttu-id="2be1e-148">Witaj warstwy standardowa i Premium zapewniają usługi API Management z hello większość mocy obliczeniowej i wydajności.</span><span class="sxs-lookup"><span data-stu-id="2be1e-148">hello Standard and Premium tiers provide your API Management service with hello most processing power and performance.</span></span> <span data-ttu-id="2be1e-149">W tym samouczku można korzystać z dowolnej warstwy.</span><span class="sxs-lookup"><span data-stu-id="2be1e-149">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="2be1e-150">Aby uzyskać więcej informacji na temat warstw usługi API Management, zobacz [API Management — cennik][API Management pricing].</span><span class="sxs-lookup"><span data-stu-id="2be1e-150">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="2be1e-151">Kliknij przycisk **Utwórz** toostart inicjowania obsługi administracyjnej wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="2be1e-151">Click **Create** toostart provisioning your service instance.</span></span>

![Nowa usługa API Management][api-management-instance-created]

<span data-ttu-id="2be1e-153">Po utworzeniu wystąpienia usługi hello hello następnym krokiem jest toocreate lub zaimportować interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2be1e-153">Once hello service instance is created, hello next step is toocreate or import an API.</span></span>

## <span data-ttu-id="2be1e-154"><a name="create-api"> </a>Importowanie interfejsu API</span><span class="sxs-lookup"><span data-stu-id="2be1e-154"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="2be1e-155">Interfejs API składa się z zestawu operacji, które mogą być wywoływane z poziomu aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="2be1e-155">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="2be1e-156">Operacje interfejsu API są tooexisting serwerem proxy usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="2be1e-156">API operations are proxied tooexisting web services.</span></span>

<span data-ttu-id="2be1e-157">Interfejsy API mogą być tworzone ręcznie (wraz z dodawaniem operacji) lub importowane.</span><span class="sxs-lookup"><span data-stu-id="2be1e-157">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="2be1e-158">W tym samouczku zaimportujemy hello interfejsu API dla przykładowych Kalkulator usługi sieci web obsługiwane przez firmę Microsoft i hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="2be1e-158">In this tutorial, we will import hello API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="2be1e-159">Aby uzyskać wskazówki na temat tworzenia interfejsu API i ręczne dodanie czynności, zobacz [jak toocreate interfejsów API](api-management-howto-create-apis.md) i [jak tooadd tooan operacje interfejsu API](api-management-howto-add-operations.md).</span><span class="sxs-lookup"><span data-stu-id="2be1e-159">For guidance on creating an API and manually adding operations, see [How toocreate APIs](api-management-howto-create-apis.md) and [How tooadd operations tooan API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="2be1e-160">Interfejsy API są skonfigurowane z hello wydawcy portalu.</span><span class="sxs-lookup"><span data-stu-id="2be1e-160">APIs are configured from hello publisher portal.</span></span> <span data-ttu-id="2be1e-161">tooreach, kliknij przycisk **wydawcy portalu** z paska narzędzi usługi hello.</span><span class="sxs-lookup"><span data-stu-id="2be1e-161">tooreach it, click **Publisher portal** from hello service toolbar.</span></span>

![Portal wydawcy][api-management-management-console]

<span data-ttu-id="2be1e-163">Kalkulator hello tooimport interfejsu API, kliknij przycisk **interfejsów API** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **Import API**.</span><span class="sxs-lookup"><span data-stu-id="2be1e-163">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![Przycisk do importowania interfejsu API][api-management-import-api]

<span data-ttu-id="2be1e-165">Wykonaj następujące kroki tooconfigure hello Kalkulator API hello:</span><span class="sxs-lookup"><span data-stu-id="2be1e-165">Perform hello following steps tooconfigure hello calculator API:</span></span>

1. <span data-ttu-id="2be1e-166">Kliknij przycisk **z adresu URL**, wprowadź **http://calcapi.cloudapp.net/calcapi.json** do hello **Specyfikacja adresu URL** tekst i kliknij hello **programu Swagger**  przycisk radiowy.</span><span class="sxs-lookup"><span data-stu-id="2be1e-166">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into hello **Specification document URL** text box, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="2be1e-167">Typ **obliczenia** do hello **sufiks adresu URL interfejsu API sieci Web** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="2be1e-167">Type **calc** into hello **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="2be1e-168">Kliknij hello **produktów (opcjonalnie)** polu i wybierz polecenie **Starter**.</span><span class="sxs-lookup"><span data-stu-id="2be1e-168">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="2be1e-169">Kliknij przycisk **zapisać** hello tooimport interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2be1e-169">Click **Save** tooimport hello API.</span></span>

![Dodawanie nowego interfejsu API][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="2be1e-171">Usługa **API Management** obecnie obsługuje importowanie obu wersji dokumentu Swagger (1.2 i 2.0).</span><span class="sxs-lookup"><span data-stu-id="2be1e-171">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="2be1e-172">Zwróć uwagę, że chociaż w [specyfikacji Swagger 2.0](http://swagger.io/specification) zadeklarowano, że właściwości `host`, `basePath`, i `schemes` są opcjonalne, dokument Swagger 2.0 **MUSI** zawierać te właściwości. W przeciwnym razie nie zostanie zaimportowany.</span><span class="sxs-lookup"><span data-stu-id="2be1e-172">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="2be1e-173">Po zaimportowaniu hello API hello strony podsumowania dla interfejsu API hello jest wyświetlana w hello wydawcy portalu.</span><span class="sxs-lookup"><span data-stu-id="2be1e-173">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![Podsumowanie interfejsu API][api-management-imported-api-summary]

<span data-ttu-id="2be1e-175">Witaj sekcji interfejsu API ma kilka kart.</span><span class="sxs-lookup"><span data-stu-id="2be1e-175">hello API section has several tabs.</span></span> <span data-ttu-id="2be1e-176">Witaj **Podsumowanie** karta zawiera podstawowe metryki i informacji na temat hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2be1e-176">hello **Summary** tab displays basic metrics and information about hello API.</span></span> <span data-ttu-id="2be1e-177">Witaj [ustawienia](api-management-howto-create-apis.md#configure-api-settings) karta jest używane tooview i edytowanie hello konfigurację interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2be1e-177">hello [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used tooview and edit hello configuration for an API.</span></span> <span data-ttu-id="2be1e-178">Witaj [operacji](api-management-howto-add-operations.md) karta jest używane toomanage hello interfejsu API operacji.</span><span class="sxs-lookup"><span data-stu-id="2be1e-178">hello [Operations](api-management-howto-add-operations.md) tab is used toomanage hello API's operations.</span></span> <span data-ttu-id="2be1e-179">Witaj **zabezpieczeń** karty mogą być używane tooconfigure bramy uwierzytelniania na powitania serwera wewnętrznej bazy danych przy użyciu uwierzytelniania podstawowego lub [uwierzytelnianie wzajemne certyfikatu](api-management-howto-mutual-certificates.md)i tooconfigure [ Autoryzacja użytkownika przy użyciu protokołu OAuth 2.0](api-management-howto-oauth2.md).</span><span class="sxs-lookup"><span data-stu-id="2be1e-179">hello **Security** tab can be used tooconfigure gateway authentication for hello backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and tooconfigure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="2be1e-180">Witaj **problemów** karta jest używane tooview problemy zgłoszone przez hello deweloperów, którzy korzystają z interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="2be1e-180">hello **Issues** tab is used tooview issues reported by hello developers who are using your APIs.</span></span> <span data-ttu-id="2be1e-181">Witaj **produktów** karta jest używane tooconfigure hello produktów, które zawierają ten interfejs API.</span><span class="sxs-lookup"><span data-stu-id="2be1e-181">hello **Products** tab is used tooconfigure hello products that contain this API.</span></span>

<span data-ttu-id="2be1e-182">Domyślnie każde wystąpienie usługi API Management zawiera dwa produkty przykładowe:</span><span class="sxs-lookup"><span data-stu-id="2be1e-182">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="2be1e-183">**Starter (początkowy)**</span><span class="sxs-lookup"><span data-stu-id="2be1e-183">**Starter**</span></span>
* <span data-ttu-id="2be1e-184">**Unlimited (nieograniczony)**</span><span class="sxs-lookup"><span data-stu-id="2be1e-184">**Unlimited**</span></span>

<span data-ttu-id="2be1e-185">W tym samouczku hello podstawowe Kalkulator interfejsu API dodano produktu Starter toohello importowane hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2be1e-185">In this tutorial, hello Basic Calculator API was added toohello Starter product when hello API was imported.</span></span>

<span data-ttu-id="2be1e-186">W kolejności toomake wywołania tooan interfejsu API deweloperzy najpierw uzyskać subskrypcję produktu tooa, co umożliwia im tooit dostępu.</span><span class="sxs-lookup"><span data-stu-id="2be1e-186">In order toomake calls tooan API, developers must first subscribe tooa product that gives them access tooit.</span></span> <span data-ttu-id="2be1e-187">Deweloperzy mogą subskrybować tooproducts w portalu dla deweloperów hello lub Administratorzy mogą subskrybować tooproducts deweloperów w portalu wydawcy hello.</span><span class="sxs-lookup"><span data-stu-id="2be1e-187">Developers can subscribe tooproducts in hello developer portal, or administrators can subscribe developers tooproducts in hello publisher portal.</span></span> <span data-ttu-id="2be1e-188">Od czasu utworzenia wystąpienia interfejsu API zarządzania hello w hello poprzednie kroki w samouczku hello tak, aby już subskrybowany tooevery produktu domyślnie są przeznaczone dla administratorów.</span><span class="sxs-lookup"><span data-stu-id="2be1e-188">You are an administrator since you created hello API Management instance in hello previous steps in hello tutorial, so you are already subscribed tooevery product by default.</span></span>

## <span data-ttu-id="2be1e-189"><a name="call-operation"></a>Wywołać operację z portalu dla deweloperów hello</span><span class="sxs-lookup"><span data-stu-id="2be1e-189"><a name="call-operation"> </a>Call an operation from hello developer portal</span></span>
<span data-ttu-id="2be1e-190">Operacje mogą być wywoływane bezpośrednio z portalu dla deweloperów hello, która zapewnia tooview wygodny sposób i przetestować hello operacje interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2be1e-190">Operations can be called directly from hello developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="2be1e-191">W tym kroku samouczka wywoła API Kalkulator podstawowe hello **Dodaj dwie liczb całkowitych** operacji.</span><span class="sxs-lookup"><span data-stu-id="2be1e-191">In this tutorial step, you will call hello Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="2be1e-192">Kliknij przycisk **portalu dla deweloperów** menu hello w hello górnego prawego hello wydawcy portalu.</span><span class="sxs-lookup"><span data-stu-id="2be1e-192">Click **Developer portal** from hello menu at hello top right of hello publisher portal.</span></span>

![Portal dla deweloperów][api-management-developer-portal-menu]

<span data-ttu-id="2be1e-194">Kliknij przycisk **interfejsów API** z hello menu u góry, a następnie kliknij przycisk **podstawowe Kalkulator** toosee hello dostępnych operacji.</span><span class="sxs-lookup"><span data-stu-id="2be1e-194">Click **APIs** from hello top menu, and then click **Basic Calculator** toosee hello available operations.</span></span>

![Portal dla deweloperów][api-management-developer-portal-calc-api]

<span data-ttu-id="2be1e-196">Należy pamiętać, hello próbki opisy i parametrów, które zostały zaimportowane wraz z hello interfejsu API i operacje, Udostępnianie dokumentacji dla deweloperów hello, które będą korzystać z tej operacji.</span><span class="sxs-lookup"><span data-stu-id="2be1e-196">Note hello sample descriptions and parameters that were imported along with hello API and operations, providing documentation for hello developers that will use this operation.</span></span> <span data-ttu-id="2be1e-197">Te opisy można również dodawać podczas ręcznego dodawania operacji.</span><span class="sxs-lookup"><span data-stu-id="2be1e-197">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="2be1e-198">Witaj toocall **Dodaj dwie liczb całkowitych** operacji, kliknij przycisk **wypróbuj**.</span><span class="sxs-lookup"><span data-stu-id="2be1e-198">toocall hello **Add two integers** operation, click **Try it**.</span></span>

![Wypróbuj][api-management-developer-portal-calc-api-console]

<span data-ttu-id="2be1e-200">Wpisz część wartości parametrów hello lub zachować ustawienia domyślne hello a następnie kliknij przycisk **wysyłania**.</span><span class="sxs-lookup"><span data-stu-id="2be1e-200">You can enter some values for hello parameters or keep hello defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="2be1e-202">Po wywołaniu operacji portalu dla deweloperów hello Wyświetla hello **stanu odpowiedzi**, hello **nagłówki odpowiedzi**, natomiast dla ustawienia **zawartości odpowiedzi**.</span><span class="sxs-lookup"><span data-stu-id="2be1e-202">After an operation is invoked, hello developer portal displays hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![Odpowiedź][api-management-invoke-get-response]

## <span data-ttu-id="2be1e-204"><a name="view-analytics"> </a>Wyświetlanie analiz</span><span class="sxs-lookup"><span data-stu-id="2be1e-204"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="2be1e-205">Analiza tooview podstawowe Kalkulator, przełącznik wstecz toohello wydawcy portalu, wybierając **Zarządzaj** menu hello w hello górnego prawego hello portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="2be1e-205">tooview analytics for Basic Calculator, switch back toohello publisher portal by selecting **Manage** from hello menu at hello top right of hello developer portal.</span></span>

![Zarządzanie][api-management-manage-menu]

<span data-ttu-id="2be1e-207">Witaj domyślny widok portalu wydawcy hello jest hello **pulpitu nawigacyjnego**, który zawiera omówienie wystąpienia interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="2be1e-207">hello default view for hello publisher portal is hello **Dashboard**, which provides an overview of your API Management instance.</span></span>

![Pulpit nawigacyjny][api-management-dashboard]

<span data-ttu-id="2be1e-209">Przesuwania myszy hello wykres hello **podstawowe Kalkulator** toosee hello określonych metryk hello użyciem hello interfejsu API dla danego okresu.</span><span class="sxs-lookup"><span data-stu-id="2be1e-209">Hover hello mouse over hello chart for **Basic Calculator** toosee hello specific metrics for hello usage of hello API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="2be1e-210">Na wykresie nie ma żadnych wierszy, Przełącz portalu dla deweloperów toohello Wstecz i wywołań do hello interfejsu API, poczekaj chwilę, a następnie powrotu toohello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="2be1e-210">If you don't see any lines on your chart, switch back toohello developer portal and make some calls into hello API, wait a few moments, and then come back toohello dashboard.</span></span>
> 
> 

<span data-ttu-id="2be1e-211">Kliknij przycisk **Wyświetl szczegóły** tooview hello stronę podsumowania hello interfejsu API, łącznie z większą wersję metryki hello wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="2be1e-211">Click **View Details** tooview hello summary page for hello API, including a larger version of hello displayed metrics.</span></span>

![Analiza][api-management-mouse-over]

![Podsumowanie][api-management-api-summary-metrics]

<span data-ttu-id="2be1e-214">Szczegółowe metryki i raportów, kliknij przycisk **Analytics** z hello **zarządzanie interfejsami API** menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="2be1e-214">For detailed metrics and reports, click **Analytics** from hello **API Management** menu on hello left.</span></span>

![Omówienie][api-management-analytics-overview]

<span data-ttu-id="2be1e-216">Witaj **Analytics** sekcja zawiera następujące cztery karty hello:</span><span class="sxs-lookup"><span data-stu-id="2be1e-216">hello **Analytics** section has hello following four tabs:</span></span>

* <span data-ttu-id="2be1e-217">**Jeden rzut oka** udostępnia ogólne użycie i metryki kondycji również hello top deweloperzy najlepszych produktów, top interfejsów API operacje i top.</span><span class="sxs-lookup"><span data-stu-id="2be1e-217">**At a glance** provides overall usage and health metrics, as well as hello top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="2be1e-218">**Użycie** zapewnia głębszy wgląd w wywołania interfejsu API i przepustowość, w tym reprezentację geograficzną.</span><span class="sxs-lookup"><span data-stu-id="2be1e-218">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="2be1e-219">**Kondycja** koncentruje się na kodach stanu, współczynnikach pomyślnego użycia pamięci podręcznej, czasach odpowiedzi oraz czasach odpowiedzi interfejsu API i usług.</span><span class="sxs-lookup"><span data-stu-id="2be1e-219">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="2be1e-220">**Działanie** udostępnia raporty, które przechodzenie na powitania określonego działania przez deweloperów, produktu, interfejsu API i operację.</span><span class="sxs-lookup"><span data-stu-id="2be1e-220">**Activity** provides reports that drill down on hello specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="2be1e-221"><a name="next-steps"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2be1e-221"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="2be1e-222">Dowiedz się, jak za[chronić interfejs API limity szybkości](api-management-howto-product-with-rules.md).</span><span class="sxs-lookup"><span data-stu-id="2be1e-222">Learn how too[Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
