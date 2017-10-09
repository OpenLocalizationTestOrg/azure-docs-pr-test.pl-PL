---
title: "punkty końcowe z portalu Azure hello przesyłania strumieniowego aaaManage | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób toomanage punktów końcowych przesyłania strumieniowego z hello portalu Azure."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="9670c-103">Zarządzanie punktów końcowych przesyłania strumieniowego z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9670c-103">Manage streaming endpoints with hello Azure portal</span></span>

<span data-ttu-id="9670c-104">W tym temacie przedstawiono sposób toouse hello punktów końcowych przesyłania strumieniowego toomanage portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9670c-104">This topic shows  how toouse hello Azure portal toomanage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="9670c-105">Upewnij się, że hello tooreview [omówienie](media-services-streaming-endpoints-overview.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="9670c-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="9670c-106">Aby uzyskać informacje o sposobie tooscale hello punktu końcowego przesyłania strumieniowego, zobacz [to](media-services-portal-scale-streaming-endpoints.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="9670c-106">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="9670c-107">Rozpocznij zarządzanie punktów końcowych przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="9670c-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="9670c-108">toostart Zarządzanie punktów końcowych przesyłania strumieniowego dla Twojego konta, hello następujące.</span><span class="sxs-lookup"><span data-stu-id="9670c-108">toostart managing streaming endpoints for your account, do hello following.</span></span>

1. <span data-ttu-id="9670c-109">W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="9670c-109">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="9670c-110">W hello **ustawienia** bloku, wybierz opcję **punkty końcowe przesyłania strumieniowego**.</span><span class="sxs-lookup"><span data-stu-id="9670c-110">In hello **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![Punkt końcowy przesyłania strumieniowego](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="9670c-112">Rozliczenie jest przeprowadzane tylko w przypadku przesyłania strumieniowego punktu końcowego jest w stanie uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="9670c-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="9670c-113">Dodawanie/Usuwanie punktu końcowego przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="9670c-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="9670c-114">Nie można usunąć domyślnej Hello punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="9670c-114">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="9670c-115">tooadd/usuwania przesyłania strumieniowego punktu końcowego za pomocą hello portalu Azure, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="9670c-115">tooadd/delete streaming endpoint using hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="9670c-116">tooadd punktu końcowego przesyłania strumieniowego, kliknij przycisk hello **+ punktu końcowego** u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="9670c-116">tooadd a streaming endpoint, click hello **+ Endpoint** at hello top of hello page.</span></span> 

    <span data-ttu-id="9670c-117">Jeśli planujesz toohave może ma wiele punktów końcowych przesyłania strumieniowego innego CDN lub CDN oraz bezpośredni dostęp do.</span><span class="sxs-lookup"><span data-stu-id="9670c-117">You might want multiple Streaming Endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="9670c-118">Naciśnij klawisz toodelete punktu końcowego przesyłania strumieniowego, **usunąć** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9670c-118">toodelete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="9670c-119">Kliknij przycisk hello **Start** hello toostart przycisk punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="9670c-119">Click hello **Start** button toostart hello streaming endpoint.</span></span>
   
    ![Punkt końcowy przesyłania strumieniowego](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="9670c-121"><a id="configure_streaming_endpoints"></a>Konfigurowanie hello punktu końcowego przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="9670c-121"><a id="configure_streaming_endpoints"></a>Configuring hello Streaming Endpoint</span></span>
<span data-ttu-id="9670c-122">Punktu końcowego przesyłania strumieniowego umożliwia hello tooconfigure następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="9670c-122">Streaming Endpoint enables you tooconfigure hello following properties:</span></span>

* <span data-ttu-id="9670c-123">Kontrola dostępu</span><span class="sxs-lookup"><span data-stu-id="9670c-123">Access control</span></span>
* <span data-ttu-id="9670c-124">Kontrola pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="9670c-124">Cache control</span></span>
* <span data-ttu-id="9670c-125">Granic lokacji zasad dostępu</span><span class="sxs-lookup"><span data-stu-id="9670c-125">Cross site access policies</span></span>

<span data-ttu-id="9670c-126">Aby uzyskać szczegółowe informacje na temat tych właściwości, zobacz [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="9670c-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="9670c-127">Można skonfigurować punktu końcowego przesyłania strumieniowego, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="9670c-127">You can configure streaming endpoint by doing hello following:</span></span>

1. <span data-ttu-id="9670c-128">Wybierz hello ma tooconfigure punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="9670c-128">Select hello streaming endpoint you want tooconfigure.</span></span>
2. <span data-ttu-id="9670c-129">Kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="9670c-129">Click **Settings**.</span></span>

<span data-ttu-id="9670c-130">Krótki opis pola hello się poniżej.</span><span class="sxs-lookup"><span data-stu-id="9670c-130">A brief description of hello fields follows.</span></span>

![Punkt końcowy przesyłania strumieniowego](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="9670c-132">Maksymalna pamięć podręczna zasad: okres istnienia pamięci podręcznej tooconfigure używane zasoby obsługiwane za pomocą tego punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="9670c-132">Maximum cache policy: used tooconfigure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="9670c-133">Jeśli wartość nie jest ustawiona, używana jest domyślna hello.</span><span class="sxs-lookup"><span data-stu-id="9670c-133">If no value is set, hello default is used.</span></span> <span data-ttu-id="9670c-134">wartości domyślne Hello można zdefiniować w taki sposób, bezpośrednio w magazynie Azure.</span><span class="sxs-lookup"><span data-stu-id="9670c-134">hello default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="9670c-135">Jeśli włączono Azure CDN hello punktu końcowego przesyłania strumieniowego, nie należy ustawiać hello pamięci podręcznej zasad wartość tooless niż 600 sekund.</span><span class="sxs-lookup"><span data-stu-id="9670c-135">If Azure CDN is enabled for hello streaming endpoint, you should not set hello cache policy value tooless than 600 seconds.</span></span>  
2. <span data-ttu-id="9670c-136">Dozwolone adresy IP: używane adresy IP toospecify, których mogliby tooconnect toohello opublikowane punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="9670c-136">Allowed IP addresses: used toospecify IP addresses that would be allowed tooconnect toohello published streaming endpoint.</span></span> <span data-ttu-id="9670c-137">Jeśli nie określono adresów IP, dowolnego adresu IP będą mogli tooconnect.</span><span class="sxs-lookup"><span data-stu-id="9670c-137">If no IP addresses specified, any IP address would be able tooconnect.</span></span> <span data-ttu-id="9670c-138">Adresy IP można określić jako pojedynczy adres IP (na przykład "10.0.0.1"), zakresu adresów IP przy użyciu adresu IP i maski podsieci CIDR (na przykład "10.0.0.1/22") lub zakres adresów IP przy użyciu adresu IP i maski podsieci dziesiętną kropkami (na przykład 10.0.0.1 () 255.255.255.0) ").</span><span class="sxs-lookup"><span data-stu-id="9670c-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="9670c-139">Konfiguracja Akamai podpis nagłówka uwierzytelniania: używane toospecify konfiguracji podpis nagłówka uwierzytelniania żądania z Akamai serwerów.</span><span class="sxs-lookup"><span data-stu-id="9670c-139">Configuration for Akamai signature header authentication: used toospecify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="9670c-140">Wygaśnięcia jest w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="9670c-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="9670c-141">Skalowanie programu Premium punktu końcowego przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="9670c-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="9670c-142">Aby uzyskać więcej informacji, zobacz [ten](media-services-portal-scale-streaming-endpoints.md) temat.</span><span class="sxs-lookup"><span data-stu-id="9670c-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="9670c-143"><a id="enable_cdn"></a>Włącz integrację usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="9670c-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="9670c-144">Podczas tworzenia nowego konta integracji przesyłania strumieniowego punktu końcowego usługi Azure CDN domyślny jest domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="9670c-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="9670c-145">Jeśli chcesz później hello toodisable/enable CDN, przesyłania strumieniowego punktu końcowego musi należeć do hello **zatrzymana** stanu.</span><span class="sxs-lookup"><span data-stu-id="9670c-145">If you later want toodisable/enable hello CDN, your streaming endpoint must be in hello **stopped** state.</span></span> <span data-ttu-id="9670c-146">Między hello wszystkich punktów POP w sieci CDN może potrwać godziny too2 tooget integracji usługi Azure CDN hello włączone i toobe zmiany hello active.</span><span class="sxs-lookup"><span data-stu-id="9670c-146">It could take up too2 hours for hello Azure CDN integration tooget enabled and for hello changes toobe active across all hello CDN POPs.</span></span> <span data-ttu-id="9670c-147">Jednak można uruchomić punktu końcowego oraz strumienia bez przerw w działaniu przesyłania z hello punktu końcowego przesyłania strumieniowego i po ukończeniu integracji hello strumienia hello są dostarczane z hello CDN.</span><span class="sxs-lookup"><span data-stu-id="9670c-147">However, your can start your streaming endpoint and stream without interruptions from hello streaming endpoint and once hello integration is complete, hello stream will be delivered from hello CDN.</span></span> <span data-ttu-id="9670c-148">Podczas inicjowania obsługi administracyjnej okres hello będzie punktu końcowego przesyłania strumieniowego w **uruchamianie** stanu i użytkownik może obserwować degredad wydajności.</span><span class="sxs-lookup"><span data-stu-id="9670c-148">During hello provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="9670c-149">Integracja usługi CDN jest włączona we wszystkich execpt centrach danych platformy Azure hello Chin i regiony rządu federalnego.</span><span class="sxs-lookup"><span data-stu-id="9670c-149">CDN integration is enabled in all hello Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="9670c-150">Po włączeniu hello **kontroli dostępu**, **niestandardowej nazwy hosta** i **uwierzytelnianie za pomocą sygnatury Akamai** konfiguracja zostanie wyłączona.</span><span class="sxs-lookup"><span data-stu-id="9670c-150">Once it is enabled, hello **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="9670c-151">Integracja usługi Azure Media Services z usługą Azure CDN jest wdrażana w **Azure CDN from Verizon** standardu punkty końcowe przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="9670c-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="9670c-152">Punkty końcowe przesyłania strumieniowego Premium można skonfigurować przy użyciu wszystkich **Azure CDN ceny warstw i dostawców**.</span><span class="sxs-lookup"><span data-stu-id="9670c-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="9670c-153">Aby uzyskać więcej informacji na temat funkcji usługi Azure CDN, zobacz hello [Omówienie usługi CDN](../cdn/cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9670c-153">For more information about Azure CDN features, see hello [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="9670c-154">Dodatkowe zagadnienia</span><span class="sxs-lookup"><span data-stu-id="9670c-154">Additional considerations</span></span>

* <span data-ttu-id="9670c-155">Po włączeniu przesyłania strumieniowego punktu końcowego CDN klientów nie można żądać zawartości bezpośrednio z hello źródła.</span><span class="sxs-lookup"><span data-stu-id="9670c-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from hello origin.</span></span> <span data-ttu-id="9670c-156">Należy tootest możliwości hello zawartości z lub bez sieci CDN w warstwie można utworzyć innego przesyłania strumieniowego punktu końcowego, który nie jest włączona w sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="9670c-156">If you need hello ability tootest your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="9670c-157">Twoje przesyłania strumieniowego pozostaje nazwę hosta punktu końcowego hello sam po włączeniu usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="9670c-157">Your streaming endpoint hostname remains hello same after enabling CDN.</span></span> <span data-ttu-id="9670c-158">Nie trzeba toomake każdy przepływ pracy usług, zmiany tooyour nośnika po włączeniu usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="9670c-158">You don’t need toomake any changes tooyour media services workflow after CDN is enabled.</span></span> <span data-ttu-id="9670c-159">Na przykład jeśli Twoje przesyłania strumieniowego hosta punktu końcowego jest strasbourg.streaming.mediaservices.windows.net, po włączeniu usługi CDN, dokładnie tej samej nazwy hosta hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="9670c-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, hello exact same hostname is used.</span></span>
* <span data-ttu-id="9670c-160">Dla nowych punktów końcowych przesyłania strumieniowego można włączyć CDN za tworzenie nowego punktu końcowego; istniejące punkty końcowe przesyłania strumieniowego wymaga punktu końcowego hello stop toofirst, a następnie Włącz/Wyłącz hello CDN.</span><span class="sxs-lookup"><span data-stu-id="9670c-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need toofirst stop hello endpoint and then enable/disable hello CDN.</span></span>
* <span data-ttu-id="9670c-161">Standardowego punktu końcowego przesyłania strumieniowego można skonfigurować tylko za pomocą **dostawcy sieci CDN w warstwie standardowa Verizon** za pomocą portalu zarządzania Azure.</span><span class="sxs-lookup"><span data-stu-id="9670c-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="9670c-162">Jednak można włączyć innych dostawców usługi Azure CDN przy użyciu interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="9670c-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="9670c-163">Skonfiguruj profil CDN</span><span class="sxs-lookup"><span data-stu-id="9670c-163">Configure CDN profile</span></span>

<span data-ttu-id="9670c-164">Można skonfigurować profil CDN hello, wybierając hello **Zarządzanie CDN** przycisk od góry hello.</span><span class="sxs-lookup"><span data-stu-id="9670c-164">You can configure hello CDN profile by selecting hello **Manage CDN** button from hello top.</span></span>

![Punkt końcowy przesyłania strumieniowego](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="9670c-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9670c-166">Next steps</span></span>
<span data-ttu-id="9670c-167">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="9670c-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9670c-168">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="9670c-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

