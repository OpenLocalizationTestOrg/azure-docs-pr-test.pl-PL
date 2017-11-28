---
title: "zasady ochrony zawartości aaaConfiguring za pomocą hello portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono sposób toouse hello tooconfigure portalu Azure zasady ochrony zawartości. Witaj artykule jest także przedstawiono sposób dynamicznego szyfrowania tooenable trwałych."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a><span data-ttu-id="0e48b-104">Konfigurowanie zasad ochrony zawartości przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0e48b-104">Configuring content protection policies using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="0e48b-105">toocomplete tego samouczka jest potrzebne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0e48b-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="0e48b-106">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e48b-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="0e48b-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="0e48b-107">Overview</span></span>
<span data-ttu-id="0e48b-108">Microsoft Azure Media Services (AMS) umożliwia toosecure możesz z hello razem, gdy opuszczą komputera za pośrednictwem przechowywania, przetwarzania i dostarczania multimediów.</span><span class="sxs-lookup"><span data-stu-id="0e48b-108">Microsoft Azure Media Services (AMS) enables you toosecure your media from hello time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="0e48b-109">Usługa Media Services umożliwia toodeliver zawartości szyfrowane dynamicznie z Standard AES (Advanced Encryption) (przy użyciu 128-bitowe klucze szyfrowania), szyfrowania common encryption (CENC) za pomocą PlayReady lub Widevine DRM i FairPlay firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="0e48b-109">Media Services allows you toodeliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="0e48b-110">AMS udostępnia usługę dostarczania licencji DRM i AES wyczyść klucze tooauthorized klientów.</span><span class="sxs-lookup"><span data-stu-id="0e48b-110">AMS provides a service for delivering DRM licenses and AES clear keys tooauthorized clients.</span></span> <span data-ttu-id="0e48b-111">Witaj portalu Azure pozwala toocreate jedną **zasady autoryzacji klucza/licencji** dla wszystkich typów szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="0e48b-111">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="0e48b-112">W tym artykule przedstawiono sposób tooconfigure zawartości zasady ochrony z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0e48b-112">This article demonstrates how tooconfigure content protection policies with hello Azure portal.</span></span> <span data-ttu-id="0e48b-113">Witaj artykule jest także przedstawiono sposób tooapply szyfrowania dynamicznego tooyour zasoby.</span><span class="sxs-lookup"><span data-stu-id="0e48b-113">hello article also shows how tooapply dynamic encryption tooyour assets.</span></span>


> [!NOTE]
> <span data-ttu-id="0e48b-114">Jeśli używasz zasad ochrony hello Azure classic portal toocreate hello zasad nie może występować w hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0e48b-114">If you used hello Azure classic portal toocreate protection policies, hello policies may not appear in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="0e48b-115">Jednak wszystkie hello starego zasady nadal istnieje.</span><span class="sxs-lookup"><span data-stu-id="0e48b-115">However, all hello old polices still exist.</span></span> <span data-ttu-id="0e48b-116">Można sprawdzić za pomocą hello zestawu .NET SDK usługi Azure Media Services lub hello [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) narzędzia (toosee hello zasad, kliknij prawym przyciskiem myszy na powitania zasobów -> Wyświetl informacje (F4) -> -> kartę kluczy zawartości, kliknij polecenie Kliknij na powitania klucza).</span><span class="sxs-lookup"><span data-stu-id="0e48b-116">You can examine them using hello Azure Media Services .NET SDK or hello [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (toosee hello policies, right-click on hello asset -> Display information (F4)->click on Content keys tab-> click on hello key).</span></span> 
> 
> <span data-ttu-id="0e48b-117">Tooencrypt zawartości przy użyciu nowych zasad, należy skonfigurować je z hello portalu Azure, kliknij przycisk Zapisz i ponowne zastosowanie szyfrowania dynamicznego.</span><span class="sxs-lookup"><span data-stu-id="0e48b-117">If you want tooencrypt your asset using new policies, configure them with hello Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="0e48b-118">Rozpocząć konfigurowanie ochrony zawartości</span><span class="sxs-lookup"><span data-stu-id="0e48b-118">Start configuring content protection</span></span>
<span data-ttu-id="0e48b-119">toouse hello portalu toostart Konfigurowanie ochrony zawartości, konto globalne tooyour AMS hello następujące:</span><span class="sxs-lookup"><span data-stu-id="0e48b-119">toouse hello portal toostart configuring content protection, global tooyour AMS account, do hello following:</span></span>

1. <span data-ttu-id="0e48b-120">W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="0e48b-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="0e48b-121">Wybierz **ustawienia** > **zawartości ochrony**.</span><span class="sxs-lookup"><span data-stu-id="0e48b-121">Select **Settings** > **Content protection**.</span></span>

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="0e48b-123">Zasady autoryzacji klucza/licencji</span><span class="sxs-lookup"><span data-stu-id="0e48b-123">Key/license authorization policy</span></span>
<span data-ttu-id="0e48b-124">AMS obsługuje wiele sposobów uwierzytelniania użytkowników, którzy tworzą żądania licencji lub klucza.</span><span class="sxs-lookup"><span data-stu-id="0e48b-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="0e48b-125">zasady autoryzacji klucza zawartości Hello musi być skonfigurowane przez użytkownika i spełnione przez klienta w kolejności hello klucz/licencji toobe delived toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="0e48b-125">hello content key authorization policy must be configured by you and met by your client in order for hello key/license toobe delived toohello client.</span></span> <span data-ttu-id="0e48b-126">Witaj zasady autoryzacji klucza zawartości może mieć jeden lub więcej ograniczeń: **Otwórz** lub **tokenu** ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="0e48b-126">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="0e48b-127">Witaj portalu Azure pozwala toocreate jedną **zasady autoryzacji klucza/licencji** dla wszystkich typów szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="0e48b-127">hello Azure portal enables you toocreate one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="0e48b-128">Otwarty</span><span class="sxs-lookup"><span data-stu-id="0e48b-128">Open</span></span>
<span data-ttu-id="0e48b-129">Otwórz ograniczeń oznacza, że hello system będzie dostarczać hello tooanyone klucza, który wysyła żądanie klucza.</span><span class="sxs-lookup"><span data-stu-id="0e48b-129">Open restriction means that hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="0e48b-130">To ograniczenie mogą być przydatne do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="0e48b-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="0e48b-131">Token</span><span class="sxs-lookup"><span data-stu-id="0e48b-131">Token</span></span>
<span data-ttu-id="0e48b-132">Witaj zasadzie ograniczenia tokenu musi towarzyszyć token wystawiony przez Secure Token Service (STS).</span><span class="sxs-lookup"><span data-stu-id="0e48b-132">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="0e48b-133">Usługa Media Services obsługuje tokenów w i hello proste tokenów sieci Web (SWT) format tokenu Web JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="0e48b-133">Media Services supports tokens in hello Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="0e48b-134">Usługi Media Services nie zapewnia bezpieczny tokenu usługi.</span><span class="sxs-lookup"><span data-stu-id="0e48b-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="0e48b-135">Można utworzyć niestandardowy STS lub korzystać z usługi Microsoft Azure ACS tooissue tokenów.</span><span class="sxs-lookup"><span data-stu-id="0e48b-135">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="0e48b-136">Witaj STS musi być skonfigurowany toocreate podpisany token hello określony klucz i wystawianie oświadczeń, określonych w konfiguracji ograniczenia tokenu hello.</span><span class="sxs-lookup"><span data-stu-id="0e48b-136">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration.</span></span> <span data-ttu-id="0e48b-137">Hello Media Services, który zwróci usługi dostarczania klucza żądanej powitania klienta toohello (licencji lub klucza) Jeśli hello token jest prawidłowy i hello oświadczenia w hello token dopasowania tych skonfigurowane dla hello (licencji lub klucza).</span><span class="sxs-lookup"><span data-stu-id="0e48b-137">hello Media Services key delivery service will return hello requested key (or license) toohello client if hello token is valid and hello claims in hello token match those configured for hello key (or license).</span></span>

<span data-ttu-id="0e48b-138">Podczas konfigurowania hello zasadzie ograniczenia tokenu, należy określić klucz podstawowy weryfikacji hello, wystawcy i parametry odbiorców.</span><span class="sxs-lookup"><span data-stu-id="0e48b-138">When configuring hello token restricted policy, you must specify hello primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="0e48b-139">klucz podstawowy weryfikacji Hello zawiera hello klucza, że hello token została podpisana z, wystawcy hello bezpiecznego tokenu usługi, która wystawia hello token.</span><span class="sxs-lookup"><span data-stu-id="0e48b-139">hello primary verification key contains hello key that hello token was signed with, issuer is hello secure token service that issues hello token.</span></span> <span data-ttu-id="0e48b-140">odbiorców Hello (nazywane również zakres) opisano hello celem hello token lub hello zasobów hello tokenu zezwala na dostęp do.</span><span class="sxs-lookup"><span data-stu-id="0e48b-140">hello audience (sometimes called scope) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="0e48b-141">Hello usługa Media Services klucza dostawy weryfikuje, czy te wartości w tokenie hello są takie same wartości hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="0e48b-141">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span>

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="0e48b-143">Szablon praw PlayReady</span><span class="sxs-lookup"><span data-stu-id="0e48b-143">PlayReady rights template</span></span>
<span data-ttu-id="0e48b-144">Aby uzyskać szczegółowe informacje o szablonie prawa PlayReady hello, zobacz [nośnika — omówienie szablon licencji PlayReady usług](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0e48b-144">For detailed information about hello PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="0e48b-145">Inne niż stałe</span><span class="sxs-lookup"><span data-stu-id="0e48b-145">Non persistent</span></span>
<span data-ttu-id="0e48b-146">Jeśli skonfigurujesz licencji jako trwałe go tylko przechowywana w pamięci podczas hello player używa hello licencji.</span><span class="sxs-lookup"><span data-stu-id="0e48b-146">If you configure license as non-persistent, it is only held in memory while hello player is using hello license.</span></span>  

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="0e48b-148">Stałe</span><span class="sxs-lookup"><span data-stu-id="0e48b-148">Persistent</span></span>
<span data-ttu-id="0e48b-149">Jeśli skonfigurujesz licencji hello jako trwałe jest zapisywany w magazynu trwałego na powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="0e48b-149">If you configure hello license  as persistent, it is saved in persistent storage on hello client.</span></span>

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="0e48b-151">Szablon praw Widevine</span><span class="sxs-lookup"><span data-stu-id="0e48b-151">Widevine rights template</span></span>
<span data-ttu-id="0e48b-152">Aby uzyskać szczegółowe informacje o szablonie prawa Widevine hello, zobacz [omówienie szablonu licencji Widevine](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0e48b-152">For detailed information about hello Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="0e48b-153">Podstawowa</span><span class="sxs-lookup"><span data-stu-id="0e48b-153">Basic</span></span>
<span data-ttu-id="0e48b-154">Po wybraniu **podstawowe**, zostanie utworzony szablon hello z wszystkie wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="0e48b-154">When you select **Basic**, hello template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="0e48b-155">Advanced</span><span class="sxs-lookup"><span data-stu-id="0e48b-155">Advanced</span></span>
<span data-ttu-id="0e48b-156">Aby uzyskać szczegółowe informacje na temat Opcja Zaawansowane konfiguracje Widevine, zobacz [to](media-services-widevine-license-template-overview.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="0e48b-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="0e48b-158">Konfiguracja FairPlay</span><span class="sxs-lookup"><span data-stu-id="0e48b-158">FairPlay configuration</span></span>
<span data-ttu-id="0e48b-159">tooenable FairPlay szyfrowania, należy tooprovide hello aplikacji certyfikat i klucz tajny aplikacji (poproś) za pomocą opcji konfiguracji FairPlay hello.</span><span class="sxs-lookup"><span data-stu-id="0e48b-159">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option.</span></span> <span data-ttu-id="0e48b-160">Aby uzyskać szczegółowe informacje o konfiguracji FairPlay i wymagania, zobacz [to](media-services-protect-hls-with-fairplay.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0e48b-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a><span data-ttu-id="0e48b-162">Zastosowanie szyfrowania dynamicznego tooyour zasobów</span><span class="sxs-lookup"><span data-stu-id="0e48b-162">Apply dynamic encryption tooyour asset</span></span>
<span data-ttu-id="0e48b-163">tootake korzystać z szyfrowania dynamicznego, należy tooencode pliku źródłowego do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="0e48b-163">tootake advantage of dynamic encryption, you need tooencode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-tooencrypt"></a><span data-ttu-id="0e48b-164">Wybierz zasób, które mają tooencrypt</span><span class="sxs-lookup"><span data-stu-id="0e48b-164">Select an asset that you want tooencrypt</span></span>
<span data-ttu-id="0e48b-165">Wybierz wszystkie zasoby, toosee **ustawienia** > **zasoby**.</span><span class="sxs-lookup"><span data-stu-id="0e48b-165">toosee all your assets, select **Settings** > **Assets**.</span></span>

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="0e48b-167">Szyfrowanie AES lub DRM</span><span class="sxs-lookup"><span data-stu-id="0e48b-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="0e48b-168">Po naciśnięciu **Szyfruj** na zasób, dostępne są dwie opcje: **AES** lub **DRM**.</span><span class="sxs-lookup"><span data-stu-id="0e48b-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="0e48b-169">AES</span><span class="sxs-lookup"><span data-stu-id="0e48b-169">AES</span></span>
<span data-ttu-id="0e48b-170">Wyczyść klucza szyfrowania zostanie włączona na wszystkich protokołów transmisji strumieniowej AES: Smooth Streaming, HLS i MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="0e48b-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="0e48b-172">DRM</span><span class="sxs-lookup"><span data-stu-id="0e48b-172">DRM</span></span>
<span data-ttu-id="0e48b-173">Po wybraniu karty DRM hello dostępne są różne opcje zasady ochrony zawartości (co należy skonfigurować już) + zestaw protokoły przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="0e48b-173">When you select hello DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="0e48b-174">**PlayReady i Widevine z MPEG-DASH** -będzie dynamicznego szyfrowania strumienia MPEG-DASH PlayReady i Widevine DRMs.</span><span class="sxs-lookup"><span data-stu-id="0e48b-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="0e48b-175">**PlayReady i Widevine z MPEG-DASH + FairPlay z HLS** -dynamicznie są szyfrowane możesz strumieni MPEG-DASH PlayReady i Widevine DRMs.</span><span class="sxs-lookup"><span data-stu-id="0e48b-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="0e48b-176">Również są szyfrowane strumienie HLS z FairPlay.</span><span class="sxs-lookup"><span data-stu-id="0e48b-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="0e48b-177">**PlayReady tylko w przypadku funkcji Smooth Streaming, HLS i MPEG-DASH** -będzie dynamicznego szyfrowania Smooth Streaming, HLS, strumieni MPEG-DASH z PlayReady DRM.</span><span class="sxs-lookup"><span data-stu-id="0e48b-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="0e48b-178">**Widevine tylko z MPEG-DASH** -dynamicznego szyfrowania należy MPEG-DASH z Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="0e48b-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="0e48b-179">**FairPlay tylko z HLS** -będzie dynamicznego szyfrowania strumienia HLS z FairPlay.</span><span class="sxs-lookup"><span data-stu-id="0e48b-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="0e48b-180">tooenable FairPlay szyfrowania, należy tooprovide hello aplikacji certyfikat i klucz tajny aplikacji (poproś) za pomocą opcji konfiguracji FairPlay bloku ustawienia ochrony zawartości hello hello.</span><span class="sxs-lookup"><span data-stu-id="0e48b-180">tooenable FairPlay encryption, you need tooprovide hello App Certificate and Application Secret Key (ASK) through hello FairPlay Configuration option of hello Content Protection settings blade.</span></span>

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="0e48b-182">Po wprowadzeniu wybór szyfrowania hello naciśnij **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="0e48b-182">Once you make hello encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="0e48b-183">Jeśli planujesz tooplay AES szyfrowane HLS w programie Safari, zobacz [ten blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="0e48b-183">If you are planning tooplay an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e48b-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0e48b-184">Next steps</span></span>
<span data-ttu-id="0e48b-185">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="0e48b-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0e48b-186">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="0e48b-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

