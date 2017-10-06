---
title: "wprowadzenie do usługi Azure CDN aaaGetting | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooenable hello Azure sieci dostarczania zawartości (CDN). Hello samouczek przeprowadza przez tworzenie hello nowy profil CDN i punktu końcowego."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a><span data-ttu-id="8a9e3-104">Wprowadzenie do usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="8a9e3-104">Getting started with Azure CDN</span></span>
<span data-ttu-id="8a9e3-105">W tym temacie opisano włączanie usługi Azure CDN z tworzeniem nowego profilu i punktu końcowego usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8a9e3-106">Wprowadzenie toohow CDN działa, a także listę funkcji, zobacz hello [Omówienie usługi CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8a9e3-106">For an introduction toohow CDN works, as well as a list of features, see hello [CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="8a9e3-107">Tworzenie nowego profilu CDN</span><span class="sxs-lookup"><span data-stu-id="8a9e3-107">Create a new CDN profile</span></span>
<span data-ttu-id="8a9e3-108">Profil CDN jest kolekcją punktów końcowych usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-108">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="8a9e3-109">Każdy profil zawiera jeden lub więcej punktów końcowych usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-109">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="8a9e3-110">Możesz toouse wiele profilów tooorganize punktami końcowymi CDN według domeny internetowej, aplikacji sieci web lub innych kryteriów.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-110">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="8a9e3-111">Domyślnie jedna subskrypcja platformy Azure jest ograniczona tooeight profilów usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-111">By default, a single Azure subscription is limited tooeight CDN profiles.</span></span> <span data-ttu-id="8a9e3-112">Każdy profil CDN jest ograniczony tooten punktów końcowych usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-112">Each CDN profile is limited tooten CDN endpoints.</span></span>
> 
> <span data-ttu-id="8a9e3-113">Cennik usługi CDN jest stosowany na poziomie profilu CDN hello.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-113">CDN pricing is applied at hello CDN profile level.</span></span> <span data-ttu-id="8a9e3-114">Jeśli chcesz toouse kombinację Azure CDN warstw cenowych, konieczne będzie wiele profilów CDN.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-114">If you wish toouse a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="8a9e3-115">Tworzenie nowego punktu końcowego usługi CDN</span><span class="sxs-lookup"><span data-stu-id="8a9e3-115">Create a new CDN endpoint</span></span>
<span data-ttu-id="8a9e3-116">**toocreate nowy punkt końcowy CDN**</span><span class="sxs-lookup"><span data-stu-id="8a9e3-116">**toocreate a new CDN endpoint**</span></span>

1. <span data-ttu-id="8a9e3-117">W hello [Azure Portal](https://portal.azure.com), przejdź tooyour profilu CDN.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-117">In hello [Azure Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="8a9e3-118">Użytkownik może został on przypięty toohello pulpitu nawigacyjnego w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-118">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="8a9e3-119">Jeśli użytkownik nie, możesz go znaleźć, klikając **Przeglądaj**, następnie **profilów usługi CDN**, i klikając profil hello planujesz tooadd punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="8a9e3-120">zostanie wyświetlony blok profilu CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-120">hello CDN profile blade appears.</span></span>
   
    ![Profil CDN][cdn-profile-settings]
2. <span data-ttu-id="8a9e3-122">Kliknij przycisk hello **Dodawanie punktu końcowego** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-122">Click hello **Add Endpoint** button.</span></span>
   
    ![Przycisk dodawania punktu końcowego][cdn-new-endpoint-button]
   
    <span data-ttu-id="8a9e3-124">Witaj **Dodawanie punktu końcowego** zostanie wyświetlony blok.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-124">hello **Add an endpoint** blade appears.</span></span>
   
    ![Blok dodawania punktu końcowego][cdn-add-endpoint]
3. <span data-ttu-id="8a9e3-126">Wprowadź **nazwę** dla tego punktu końcowego usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-126">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="8a9e3-127">Ta nazwa będzie używana tooaccess buforowanych zasobów w domenie hello `<endpointname>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-127">This name will be used tooaccess your cached resources at hello domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="8a9e3-128">W hello **typ źródła** listy rozwijanej wybierz typ źródła.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-128">In hello **Origin type** dropdown, select your origin type.</span></span>  <span data-ttu-id="8a9e3-129">Wybierz typ **Storage** dla konta usługi Azure Storage, **Usługa w chmurze** dla usługi Azure Cloud Service, **Web App** dla usługi Azure Web App lub **Źródło niestandardowe** dla każdego innego publicznie dostępnego źródła serwera sieci Web (hostowanego na platformie Azure lub gdziekolwiek indziej).</span><span class="sxs-lookup"><span data-stu-id="8a9e3-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span></span>
   
    ![Typ źródła usługi CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. <span data-ttu-id="8a9e3-131">W hello **nazwę hosta źródła** listy rozwijanej wybierz lub wpisz domenę źródła.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-131">In hello **Origin hostname** dropdown, select or type your origin domain.</span></span>  <span data-ttu-id="8a9e3-132">Witaj liście rozwijanej będą wyświetlane wszystkie dostępne źródła typu hello określonego w kroku 4.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-132">hello dropdown will list all available origins of hello type you specified in step 4.</span></span>  <span data-ttu-id="8a9e3-133">W przypadku wybrania *Źródło niestandardowe* jako sieci **typ źródła**, zostanie tekst w domenie hello źródła niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-133">If you selected *Custom origin* as your **Origin type**, you will type in hello domain of your custom origin.</span></span>
6. <span data-ttu-id="8a9e3-134">W hello **ścieżki źródła** tekst Wprowadź hello ścieżki toohello zasoby, które chcesz toocache lub pozostaw puste tooallow w pamięci podręcznej dowolnego zasobu w domenie hello określonego w kroku 5.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-134">In hello **Origin path** text box, enter hello path toohello resources you want toocache, or leave blank tooallow cache any resource at hello domain you specified in step 5.</span></span>
7. <span data-ttu-id="8a9e3-135">W hello **nagłówka hosta źródła**, wprowadź nagłówek hosta hello ma hello toosend CDN z każdym żądaniem, lub pozostaw domyślną hello.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-135">In hello **Origin host header**, enter hello host header you want hello CDN toosend with each request, or leave hello default.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="8a9e3-136">Niektóre typy źródeł, takich jak usługi Azure Storage i Web Apps, wymagają hello hosta nagłówka toomatch hello domeny pochodzenia hello.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-136">Some types of origins, such as Azure Storage and Web Apps, require hello host header toomatch hello domain of hello origin.</span></span> <span data-ttu-id="8a9e3-137">Jeśli nie masz źródło, które wymaga nagłówka hosta innego niż jego domena, należy pozostawić hello wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-137">Unless you have an origin that requires a host header different from its domain, you should leave hello default value.</span></span>
   > 
   > 
8. <span data-ttu-id="8a9e3-138">Dla **protokołu** i **port źródła**, określ hello protokoły i porty używane tooaccess zasobów hello pochodzenia.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-138">For **Protocol** and **Origin port**, specify hello protocols and ports used tooaccess your resources at hello origin.</span></span>  <span data-ttu-id="8a9e3-139">Należy wybrać co najmniej jeden protokół (HTTP lub HTTPS).</span><span class="sxs-lookup"><span data-stu-id="8a9e3-139">At least one protocol (HTTP or HTTPS) must be selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8a9e3-140">Witaj **port źródła** wpływa tylko na jakie punktu końcowego hello portu informacje tooretrieve pochodzenia hello są używane.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-140">hello **Origin port** only affects what port hello endpoint uses tooretrieve information from hello origin.</span></span>  <span data-ttu-id="8a9e3-141">Witaj sam punkt końcowy będzie tylko klientów tooend dostępne na powitania domyślne portach HTTP i HTTPS (80 i 443), niezależnie od hello **port źródła**.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-141">hello endpoint itself will only be available tooend clients on hello default HTTP and HTTPS ports (80 and 443), regardless of hello **Origin port**.</span></span>  
   > 
   > <span data-ttu-id="8a9e3-142">**Azure CDN from Akamai** punktów końcowych nie zezwalaj na powitania pełny zakres portów TCP dla źródeł.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-142">**Azure CDN from Akamai** endpoints do not allow hello full TCP port range for origins.</span></span>  <span data-ttu-id="8a9e3-143">Lista niedozwolonych portów źródłowych znajduje się w artykule [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx) (Azure CDN from Akamai — dozwolone porty źródłowe).</span><span class="sxs-lookup"><span data-stu-id="8a9e3-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="8a9e3-144">Uzyskiwanie dostępu do sieci CDN zawartości przy użyciu protokołu HTTPS ma hello następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="8a9e3-144">Accessing CDN content using HTTPS has hello following constraints:</span></span>
   > 
   > * <span data-ttu-id="8a9e3-145">Należy użyć hello certyfikatu SSL dostarczonego przez hello CDN.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-145">You must use hello SSL certificate provided by hello CDN.</span></span> <span data-ttu-id="8a9e3-146">Certyfikaty innych firm nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-146">Third party certificates are not supported.</span></span>
   > * <span data-ttu-id="8a9e3-147">Należy użyć domeny udostępnionej do sieci CDN hello (`<endpointname>.azureedge.net`) tooaccess zawartości HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-147">You must use hello CDN-provided domain (`<endpointname>.azureedge.net`) tooaccess HTTPS content.</span></span> <span data-ttu-id="8a9e3-148">Obsługa protokołu HTTPS nie jest dostępny dla niestandardowych nazw domen (rekordy CNAME), ponieważ w tej chwili hello CDN nie obsługuje niestandardowych certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-148">HTTPS support is not available for custom domain names (CNAMEs) since hello CDN does not support custom certificates at this time.</span></span>
   > 
   > 
9. <span data-ttu-id="8a9e3-149">Kliknij przycisk hello **Dodaj** toocreate przycisk hello nowy punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-149">Click hello **Add** button toocreate hello new endpoint.</span></span>
10. <span data-ttu-id="8a9e3-150">Po utworzeniu punktu końcowego hello pojawia się na liście punktów końcowych dla profilu hello.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-150">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="8a9e3-151">Widok listy Hello pokazuje tooaccess toouse adres URL hello w pamięci podręcznej zawartości, a także domeny źródła hello.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-151">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
    
    ![Punkt końcowy usługi CDN][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > <span data-ttu-id="8a9e3-153">punkt końcowy Hello nie natychmiast będzie dostępny do użycia, jak zajmuje trochę czasu hello toopropagate rejestracji za pomocą hello CDN.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-153">hello endpoint will not immediately be available for use, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="8a9e3-154">W przypadku profilów usługi <b>Azure CDN from Akamai</b> propagacja zwykle zostanie ukończona w ciągu minuty.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="8a9e3-155">W przypadku profilów usługi <b>Azure CDN from Verizon</b> propagacja zwykle zostanie ukończona w ciągu 90 minut, ale niekiedy może to zająć więcej czasu.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
    > 
    > <span data-ttu-id="8a9e3-156">Użytkownicy, którzy podejmą nazwy domeny usługi CDN hello toouse przed konfiguracji punktu końcowego hello zakończeniem propagacji toohello POP otrzymają kody odpowiedzi HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="8a9e3-156">Users who try toouse hello CDN domain name before hello endpoint configuration has propagated toohello POPs will receive HTTP 404 response codes.</span></span>  <span data-ttu-id="8a9e3-157">Jeśli od czasu utworzenia punktu końcowego minęło kilka godzin, a nadal otrzymujesz odpowiedzi 404, zapoznaj się z artykułem [Rozwiązywanie problemów z punktami końcowymi usługi CDN zwracającymi stany 404](cdn-troubleshoot-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="8a9e3-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span></span>
    > 
    > 

## <a name="see-also"></a><span data-ttu-id="8a9e3-158">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="8a9e3-158">See Also</span></span>
* [<span data-ttu-id="8a9e3-159">Kontrolowanie zachowania buforowania żądań z ciągami zapytań</span><span class="sxs-lookup"><span data-stu-id="8a9e3-159">Controlling caching behavior of requests with query strings</span></span>](cdn-query-string.md)
* [<span data-ttu-id="8a9e3-160">Jak tooa CDN zawartości tooMap domeny niestandardowe</span><span class="sxs-lookup"><span data-stu-id="8a9e3-160">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="8a9e3-161">Wstępne ładowanie zasobów w punkcie końcowym usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="8a9e3-161">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="8a9e3-162">Przeczyszczanie punktu końcowego usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="8a9e3-162">Purge an Azure CDN Endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="8a9e3-163">Rozwiązywanie problemów z punktami końcowymi usługi CDN zwracającymi stany 404</span><span class="sxs-lookup"><span data-stu-id="8a9e3-163">Troubleshooting CDN endpoints returning 404 statuses</span></span>](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
