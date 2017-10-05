---
title: "Konfigurowanie zasad ochrony zawartości przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule pokazano, jak skonfigurować zasady ochrony zawartości przy użyciu portalu Azure. Artykuł opisuje również sposób włączania szyfrowania dynamicznego trwałych."
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
ms.openlocfilehash: 67b3fa9936daebeafb7e87fe3a7b0c7e0105b3b3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-content-protection-policies-using-the-azure-portal"></a><span data-ttu-id="247fe-104">Konfigurowanie zasad ochrony zawartości przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="247fe-104">Configuring content protection policies using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="247fe-105">Do ukończenia tego samouczka jest potrzebne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="247fe-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="247fe-106">Aby uzyskać szczegółowe informacje, zobacz temat [Bezpłatna wersja próbna systemu Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="247fe-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="247fe-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="247fe-107">Overview</span></span>
<span data-ttu-id="247fe-108">Microsoft Azure Media Services (AMS) umożliwia zabezpieczenie od momentu, gdy opuszczą komputera za pośrednictwem przechowywania, przetwarzania i dostarczania multimediów.</span><span class="sxs-lookup"><span data-stu-id="247fe-108">Microsoft Azure Media Services (AMS) enables you to secure your media from the time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="247fe-109">Usługa Media Services umożliwia dostarczanie zawartości szyfrowane dynamicznie z Standard AES (Advanced Encryption) (przy użyciu 128-bitowe klucze szyfrowania), szyfrowania common encryption (CENC) za pomocą PlayReady lub Widevine DRM i FairPlay firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="247fe-109">Media Services allows you to deliver your content encrypted dynamically with Advanced Encryption Standard (AES) (using 128-bit encryption keys), common encryption (CENC) using PlayReady and/or Widevine DRM, and Apple FairPlay.</span></span> 

<span data-ttu-id="247fe-110">AMS udostępnia usługę dostarczania licencji DRM i AES wyczyść klucze do autoryzowanych klientów.</span><span class="sxs-lookup"><span data-stu-id="247fe-110">AMS provides a service for delivering DRM licenses and AES clear keys to authorized clients.</span></span> <span data-ttu-id="247fe-111">Azure portal umożliwia utworzenie jednego **zasady autoryzacji klucza/licencji** dla wszystkich typów szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="247fe-111">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

<span data-ttu-id="247fe-112">W tym artykule pokazano, jak skonfigurować zasady ochrony zawartości przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="247fe-112">This article demonstrates how to configure content protection policies with the Azure portal.</span></span> <span data-ttu-id="247fe-113">Artykuł opisuje również sposób stosowania szyfrowania dynamicznego do zasobów.</span><span class="sxs-lookup"><span data-stu-id="247fe-113">The article also shows how to apply dynamic encryption to your assets.</span></span>


> [!NOTE]
> <span data-ttu-id="247fe-114">Jeśli używasz klasycznego portalu Azure do tworzenia zasad ochrony, zasady nie może występować w [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="247fe-114">If you used the Azure classic portal to create protection policies, the policies may not appear in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="247fe-115">Jednak wszystkie zasady stary nadal istnieją.</span><span class="sxs-lookup"><span data-stu-id="247fe-115">However, all the old polices still exist.</span></span> <span data-ttu-id="247fe-116">Można sprawdzić za pomocą zestawu SDK .NET usługi Azure Media Services lub [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) narzędzia (które zasady, kliknij prawym przyciskiem myszy na zasób -> Wyświetl informacje (F4) -> kliknij na karcie kluczy zawartości -> kliknij na klucz).</span><span class="sxs-lookup"><span data-stu-id="247fe-116">You can examine them using the Azure Media Services .NET SDK or the [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) tool (to see the policies, right-click on the asset -> Display information (F4)->click on Content keys tab-> click on the key).</span></span> 
> 
> <span data-ttu-id="247fe-117">Do szyfrowania zawartości przy użyciu nowych zasad je skonfigurować przy użyciu portalu Azure, kliknij przycisk Zapisz i ponownie zastosuj szyfrowania dynamicznego.</span><span class="sxs-lookup"><span data-stu-id="247fe-117">If you want to encrypt your asset using new policies, configure them with the Azure portal, click save, and reapply dynamic encryption.</span></span> 
> 
> 

## <a name="start-configuring-content-protection"></a><span data-ttu-id="247fe-118">Rozpocząć konfigurowanie ochrony zawartości</span><span class="sxs-lookup"><span data-stu-id="247fe-118">Start configuring content protection</span></span>
<span data-ttu-id="247fe-119">Aby korzystać z portalu, aby rozpocząć konfigurowanie ochrony zawartości, do konta usługi AMS, globalne wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="247fe-119">To use the portal to start configuring content protection, global to your AMS account, do the following:</span></span>

1. <span data-ttu-id="247fe-120">W witrynie [Azure Portal](https://portal.azure.com/) wybierz swoje konto usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="247fe-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="247fe-121">Wybierz **ustawienia** > **zawartości ochrony**.</span><span class="sxs-lookup"><span data-stu-id="247fe-121">Select **Settings** > **Content protection**.</span></span>

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a><span data-ttu-id="247fe-123">Zasady autoryzacji klucza/licencji</span><span class="sxs-lookup"><span data-stu-id="247fe-123">Key/license authorization policy</span></span>
<span data-ttu-id="247fe-124">AMS obsługuje wiele sposobów uwierzytelniania użytkowników, którzy tworzą żądania licencji lub klucza.</span><span class="sxs-lookup"><span data-stu-id="247fe-124">AMS supports multiple ways of authenticating users who make key or license requests.</span></span> <span data-ttu-id="247fe-125">Zasady autoryzacji klucza zawartości należy skonfigurowane przez użytkownika i spełnione przez klienta w kolejności klucz/licencję do można delived do klienta.</span><span class="sxs-lookup"><span data-stu-id="247fe-125">The content key authorization policy must be configured by you and met by your client in order for the key/license to be delived to the client.</span></span> <span data-ttu-id="247fe-126">Zasady autoryzacji klucza zawartości może mieć jeden lub więcej ograniczeń: **Otwórz** lub **tokenu** ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="247fe-126">The content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span>

<span data-ttu-id="247fe-127">Azure portal umożliwia utworzenie jednego **zasady autoryzacji klucza/licencji** dla wszystkich typów szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="247fe-127">The Azure portal enables you to create one **key/license authorization policy** for all types of encryptions.</span></span>

### <a name="open"></a><span data-ttu-id="247fe-128">Otwarty</span><span class="sxs-lookup"><span data-stu-id="247fe-128">Open</span></span>
<span data-ttu-id="247fe-129">Otwórz ograniczeń oznacza, że system będzie dostarczać klucza dla każdego, kto wysyła żądanie klucza.</span><span class="sxs-lookup"><span data-stu-id="247fe-129">Open restriction means that the system will deliver the key to anyone who makes a key request.</span></span> <span data-ttu-id="247fe-130">To ograniczenie mogą być przydatne do celów testowych.</span><span class="sxs-lookup"><span data-stu-id="247fe-130">This restriction might be useful for test purposes.</span></span> 

### <a name="token"></a><span data-ttu-id="247fe-131">Token</span><span class="sxs-lookup"><span data-stu-id="247fe-131">Token</span></span>
<span data-ttu-id="247fe-132">Zasadzie ograniczenia tokenu musi towarzyszyć token wystawiony przez usługę STS (Secure Token Service).</span><span class="sxs-lookup"><span data-stu-id="247fe-132">The token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="247fe-133">Usługa Media Services obsługuje tokenów w formacie proste tokenów sieci Web (SWT) i format tokenu Web JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="247fe-133">Media Services supports tokens in the Simple Web Tokens (SWT) format and JSON Web Token (JWT) format.</span></span> <span data-ttu-id="247fe-134">Usługi Media Services nie zapewnia bezpieczny tokenu usługi.</span><span class="sxs-lookup"><span data-stu-id="247fe-134">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="247fe-135">Można utworzyć niestandardowy STS lub korzystać z usługi Microsoft Azure ACS do wydawania tokenów.</span><span class="sxs-lookup"><span data-stu-id="247fe-135">You can create a custom STS or leverage Microsoft Azure ACS to issue tokens.</span></span> <span data-ttu-id="247fe-136">Usługa tokenu Zabezpieczającego musi być skonfigurowana do utworzenia tokenu podpisany z określonego klucza i problem oświadczenia określony w konfiguracji ograniczenia tokenu.</span><span class="sxs-lookup"><span data-stu-id="247fe-136">The STS must be configured to create a token signed with the specified key and issue claims that you specified in the token restriction configuration.</span></span> <span data-ttu-id="247fe-137">Usługa Media Services klucza dostawy zwróci żądanego (licencji lub klucza) do klienta, jeśli token jest prawidłowy i oświadczeń z tokenu dopasowania tych skonfigurowana dla klucza (lub licencji).</span><span class="sxs-lookup"><span data-stu-id="247fe-137">The Media Services key delivery service will return the requested key (or license) to the client if the token is valid and the claims in the token match those configured for the key (or license).</span></span>

<span data-ttu-id="247fe-138">Podczas konfigurowania token ograniczony zasad, należy określić klucz podstawowy weryfikacji, wystawcy i parametry odbiorców.</span><span class="sxs-lookup"><span data-stu-id="247fe-138">When configuring the token restricted policy, you must specify the primary verification key, issuer, and audience parameters.</span></span> <span data-ttu-id="247fe-139">Klucz podstawowy weryfikacji zawiera klucz, który został podpisany token, z, wystawca jest bezpieczne usługi tokenu, który wystawia token.</span><span class="sxs-lookup"><span data-stu-id="247fe-139">The primary verification key contains the key that the token was signed with, issuer is the secure token service that issues the token.</span></span> <span data-ttu-id="247fe-140">Odbiorców (nazywane również zakres) opisano celem tokenu lub zasobu tokenu zezwala na dostęp do.</span><span class="sxs-lookup"><span data-stu-id="247fe-140">The audience (sometimes called scope) describes the intent of the token or the resource the token authorizes access to.</span></span> <span data-ttu-id="247fe-141">Usługa Media Services klucza dostawy weryfikuje, czy te wartości w tokenie pasują do wartości w szablonie.</span><span class="sxs-lookup"><span data-stu-id="247fe-141">The Media Services key delivery service validates that these values in the token match the values in the template.</span></span>

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a><span data-ttu-id="247fe-143">Szablon praw PlayReady</span><span class="sxs-lookup"><span data-stu-id="247fe-143">PlayReady rights template</span></span>
<span data-ttu-id="247fe-144">Aby uzyskać szczegółowe informacje o szablonie prawa PlayReady, zobacz [nośnika — omówienie szablon licencji PlayReady usług](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="247fe-144">For detailed information about the PlayReady rights template, see [Media Services PlayReady License Template Overview](media-services-playready-license-template-overview.md).</span></span>

### <a name="non-persistent"></a><span data-ttu-id="247fe-145">Inne niż stałe</span><span class="sxs-lookup"><span data-stu-id="247fe-145">Non persistent</span></span>
<span data-ttu-id="247fe-146">Jeśli skonfigurujesz licencji jako trwałe go tylko przechowywana w pamięci podczas odtwarzacz używa licencji.</span><span class="sxs-lookup"><span data-stu-id="247fe-146">If you configure license as non-persistent, it is only held in memory while the player is using the license.</span></span>  

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a><span data-ttu-id="247fe-148">Stałe</span><span class="sxs-lookup"><span data-stu-id="247fe-148">Persistent</span></span>
<span data-ttu-id="247fe-149">Jeśli skonfigurujesz licencji jako trwałe jest zapisywany w magazynu trwałego na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="247fe-149">If you configure the license  as persistent, it is saved in persistent storage on the client.</span></span>

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a><span data-ttu-id="247fe-151">Szablon praw Widevine</span><span class="sxs-lookup"><span data-stu-id="247fe-151">Widevine rights template</span></span>
<span data-ttu-id="247fe-152">Aby uzyskać szczegółowe informacje o szablonie prawa Widevine, zobacz [omówienie szablonu licencji Widevine](media-services-widevine-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="247fe-152">For detailed information about the Widevine rights template, see [Widevine License Template Overview](media-services-widevine-license-template-overview.md).</span></span>

### <a name="basic"></a><span data-ttu-id="247fe-153">Podstawowa</span><span class="sxs-lookup"><span data-stu-id="247fe-153">Basic</span></span>
<span data-ttu-id="247fe-154">Po wybraniu **podstawowe**, zostanie utworzony szablon z wszystkie wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="247fe-154">When you select **Basic**, the template will be created with all defaults values.</span></span>

### <a name="advanced"></a><span data-ttu-id="247fe-155">Advanced</span><span class="sxs-lookup"><span data-stu-id="247fe-155">Advanced</span></span>
<span data-ttu-id="247fe-156">Aby uzyskać szczegółowe informacje na temat Opcja Zaawansowane konfiguracje Widevine, zobacz [to](media-services-widevine-license-template-overview.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="247fe-156">For detailed explanation about advance option of Widevine configurations, see [this](media-services-widevine-license-template-overview.md) topic.</span></span>

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a><span data-ttu-id="247fe-158">Konfiguracja FairPlay</span><span class="sxs-lookup"><span data-stu-id="247fe-158">FairPlay configuration</span></span>
<span data-ttu-id="247fe-159">Aby włączyć szyfrowanie FairPlay, musisz podać aplikacji certyfikat i klucz tajny aplikacji (poproś) za pomocą opcji konfiguracji FairPlay.</span><span class="sxs-lookup"><span data-stu-id="247fe-159">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option.</span></span> <span data-ttu-id="247fe-160">Aby uzyskać szczegółowe informacje o konfiguracji FairPlay i wymagania, zobacz [to](media-services-protect-hls-with-fairplay.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="247fe-160">For detailed information about FairPlay configuration and requirements, see [this](media-services-protect-hls-with-fairplay.md) article.</span></span>

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-to-your-asset"></a><span data-ttu-id="247fe-162">Zastosowanie szyfrowania dynamicznego do zawartości</span><span class="sxs-lookup"><span data-stu-id="247fe-162">Apply dynamic encryption to your asset</span></span>
<span data-ttu-id="247fe-163">Aby korzystać z szyfrowania dynamicznego, należy kodowanie pliku źródłowego do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="247fe-163">To take advantage of dynamic encryption, you need to encode your source file into a set of adaptive-bitrate MP4 files.</span></span>

### <a name="select-an-asset-that-you-want-to-encrypt"></a><span data-ttu-id="247fe-164">Wybierz zasób, który chcesz zaszyfrować</span><span class="sxs-lookup"><span data-stu-id="247fe-164">Select an asset that you want to encrypt</span></span>
<span data-ttu-id="247fe-165">Aby wyświetlić wszystkich zasobów, wybierz **ustawienia** > **zasoby**.</span><span class="sxs-lookup"><span data-stu-id="247fe-165">To see all your assets, select **Settings** > **Assets**.</span></span>

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a><span data-ttu-id="247fe-167">Szyfrowanie AES lub DRM</span><span class="sxs-lookup"><span data-stu-id="247fe-167">Encrypt with AES or DRM</span></span>
<span data-ttu-id="247fe-168">Po naciśnięciu **Szyfruj** na zasób, dostępne są dwie opcje: **AES** lub **DRM**.</span><span class="sxs-lookup"><span data-stu-id="247fe-168">Once you press **Encrypt** on an asset, you are presented wtih two choices: **AES** or **DRM**.</span></span> 

#### <a name="aes"></a><span data-ttu-id="247fe-169">AES</span><span class="sxs-lookup"><span data-stu-id="247fe-169">AES</span></span>
<span data-ttu-id="247fe-170">Wyczyść klucza szyfrowania zostanie włączona na wszystkich protokołów transmisji strumieniowej AES: Smooth Streaming, HLS i MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="247fe-170">AES clear key encryption will be enabled on all streaming protocols: Smooth Streaming, HLS, and MPEG-DASH.</span></span>

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a><span data-ttu-id="247fe-172">DRM</span><span class="sxs-lookup"><span data-stu-id="247fe-172">DRM</span></span>
<span data-ttu-id="247fe-173">Jeśli zostanie wybrany na karcie DRM, dostępne są różne opcje zasady ochrony zawartości (co należy skonfigurować już) + zestaw protokoły przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="247fe-173">When you select the DRM tab, you are presented with different choices of content protection policies (which you must have configured by now) + a set of streaming protocols.</span></span>

* <span data-ttu-id="247fe-174">**PlayReady i Widevine z MPEG-DASH** -będzie dynamicznego szyfrowania strumienia MPEG-DASH PlayReady i Widevine DRMs.</span><span class="sxs-lookup"><span data-stu-id="247fe-174">**PlayReady and Widevine with MPEG-DASH** - will dynamically encrypt your MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span>
* <span data-ttu-id="247fe-175">**PlayReady i Widevine z MPEG-DASH + FairPlay z HLS** -dynamicznie są szyfrowane możesz strumieni MPEG-DASH PlayReady i Widevine DRMs.</span><span class="sxs-lookup"><span data-stu-id="247fe-175">**PlayReady and Widevine with MPEG-DASH + FairPlay with HLS** - will dynamically encrypt you MPEG-DASH stream with PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="247fe-176">Również są szyfrowane strumienie HLS z FairPlay.</span><span class="sxs-lookup"><span data-stu-id="247fe-176">Will also encrypt your HLS streams with FairPlay.</span></span>
* <span data-ttu-id="247fe-177">**PlayReady tylko w przypadku funkcji Smooth Streaming, HLS i MPEG-DASH** -będzie dynamicznego szyfrowania Smooth Streaming, HLS, strumieni MPEG-DASH z PlayReady DRM.</span><span class="sxs-lookup"><span data-stu-id="247fe-177">**PlayReady only with Smooth Streaming, HLS and MPEG-DASH** - will dynamically encrypt Smooth Streaming, HLS, MPEG-DASH streams with PlayReady DRM.</span></span>
* <span data-ttu-id="247fe-178">**Widevine tylko z MPEG-DASH** -dynamicznego szyfrowania należy MPEG-DASH z Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="247fe-178">**Widevine only with MPEG-DASH** - will dynamically encrypt you MPEG-DASH with Widevine DRM.</span></span>
* <span data-ttu-id="247fe-179">**FairPlay tylko z HLS** -będzie dynamicznego szyfrowania strumienia HLS z FairPlay.</span><span class="sxs-lookup"><span data-stu-id="247fe-179">**FairPlay only with HLS** - will dynamically encrypt your HLS stream with FairPlay.</span></span>

<span data-ttu-id="247fe-180">Aby włączyć szyfrowanie FairPlay, musisz podać aplikacji certyfikat i klucz tajny aplikacji (poproś) za pomocą opcji konfiguracji FairPlay bloku ustawienia ochrony zawartości.</span><span class="sxs-lookup"><span data-stu-id="247fe-180">To enable FairPlay encryption, you need to provide the App Certificate and Application Secret Key (ASK) through the FairPlay Configuration option of the Content Protection settings blade.</span></span>

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection009.png)

<span data-ttu-id="247fe-182">Po dokonaniu wyboru szyfrowania, naciśnij klawisz **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="247fe-182">Once you make the encryption selection, press **Apply**.</span></span>

>[!NOTE] 
><span data-ttu-id="247fe-183">Jeśli planujesz odtwarzania AES szyfrowane HLS w programie Safari, zobacz [ten blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="247fe-183">If you are planning to play an AES encrypted HLS in Safari, see [this blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="247fe-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="247fe-184">Next steps</span></span>
<span data-ttu-id="247fe-185">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="247fe-185">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="247fe-186">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="247fe-186">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

