---
title: "aaaProtect HLS zawartości z Microsoft PlayReady lub Apple FairPlay - Azure | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera omówienie i pokazuje, jak toodynamically usługi Azure Media Services toouse szyfrowania zawartości HTTP Live Streaming (HLS) przy użyciu FairPlay firmy Apple. Pokazuje też, jak hello toouse Media Services licencji toodeliver usługi dostarczania tooclients licencje FairPlay."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 91ca451e3e7bf0da1d74dac4c99180f08f39e4ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="725e3-104">Ochrona programu HLS zawartości z FairPlay firmy Apple lub Microsoft PlayReady</span><span class="sxs-lookup"><span data-stu-id="725e3-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="725e3-105">Azure Media Services umożliwia toodynamically można zaszyfrować zawartość HTTP Live Streaming (HLS) przy użyciu hello następujących formatów:</span><span class="sxs-lookup"><span data-stu-id="725e3-105">Azure Media Services enables you toodynamically encrypt your HTTP Live Streaming (HLS) content by using hello following formats:</span></span>  

* <span data-ttu-id="725e3-106">**Koperty AES-128, klucz niezaszyfrowany**</span><span class="sxs-lookup"><span data-stu-id="725e3-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="725e3-107">Hello całego fragmentów są szyfrowane przy użyciu hello **CBC AES-128** tryb.</span><span class="sxs-lookup"><span data-stu-id="725e3-107">hello entire chunk is encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="725e3-108">odszyfrowywanie Hello strumienia hello jest obsługiwany natywnie przez systemów iOS i OS X player.</span><span class="sxs-lookup"><span data-stu-id="725e3-108">hello decryption of hello stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="725e3-109">Aby uzyskać więcej informacji, zobacz [dynamicznego szyfrowania przy użyciu standardu AES-128 i usługi dostarczania klucza](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="725e3-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="725e3-110">**FairPlay firmy Apple**</span><span class="sxs-lookup"><span data-stu-id="725e3-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="725e3-111">Witaj poszczególnych wideo i audio próbki są szyfrowane przy użyciu hello **CBC AES-128** tryb.</span><span class="sxs-lookup"><span data-stu-id="725e3-111">hello individual video and audio samples are encrypted by using hello **AES-128 CBC** mode.</span></span> <span data-ttu-id="725e3-112">**Przesyłanie strumieniowe FairPlay** (kl. / s) jest zintegrowany z systemów operacyjnych urządzeń hello, macierzystą obsługę w systemach iOS i Apple TV.</span><span class="sxs-lookup"><span data-stu-id="725e3-112">**FairPlay Streaming** (FPS) is integrated into hello device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="725e3-113">Przeglądarka Safari w OS X umożliwia klatek na Sekundę przy użyciu Obsługa interfejsu hello szyfrowane nośnika rozszerzenia (EME).</span><span class="sxs-lookup"><span data-stu-id="725e3-113">Safari on OS X enables FPS by using hello Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="725e3-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="725e3-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="725e3-115">Witaj poniższy obraz przedstawia hello **HLS + FairPlay lub PlayReady szyfrowania dynamicznego** przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="725e3-115">hello following image shows hello **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![Diagram przepływu pracy szyfrowania dynamicznego](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="725e3-117">W tym temacie przedstawiono, jak toodynamically Media Services toouse zaszyfrować HLS zawartości przy użyciu FairPlay firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="725e3-117">This topic demonstrates how toouse Media Services toodynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="725e3-118">Pokazuje też, jak hello toouse Media Services licencji toodeliver usługi dostarczania tooclients licencje FairPlay.</span><span class="sxs-lookup"><span data-stu-id="725e3-118">It also shows how toouse hello Media Services license delivery service toodeliver FairPlay licenses tooclients.</span></span>

> [!NOTE]
> <span data-ttu-id="725e3-119">Chcąc również tooencrypt Twojego HLS zawartości za pomocą PlayReady, należy toocreate wspólny klucz zawartości i skojarzyć go z zawartości.</span><span class="sxs-lookup"><span data-stu-id="725e3-119">If you also want tooencrypt your HLS content with PlayReady, you need toocreate a common content key and associate it with your asset.</span></span> <span data-ttu-id="725e3-120">Należy również tooconfigure hello zawartości zasady autoryzacji klucza, zgodnie z opisem w [za pomocą PlayReady, dynamicznego szyfrowania common encryption](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="725e3-120">You also need tooconfigure hello content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="725e3-121">Wymagania i uwagi</span><span class="sxs-lookup"><span data-stu-id="725e3-121">Requirements and considerations</span></span>

<span data-ttu-id="725e3-122">następujące Hello są wymagane, gdy przy użyciu toodeliver Media Services, który HLS zaszyfrowanych z FairPlay i licencje FairPlay toodeliver:</span><span class="sxs-lookup"><span data-stu-id="725e3-122">hello following are required when using Media Services toodeliver HLS encrypted with FairPlay, and toodeliver FairPlay licenses:</span></span>

  * <span data-ttu-id="725e3-123">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="725e3-123">An Azure account.</span></span> <span data-ttu-id="725e3-124">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna systemu Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="725e3-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="725e3-125">Konto usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="725e3-125">A Media Services account.</span></span> <span data-ttu-id="725e3-126">Zobacz toocreate, [Tworzenie konta usługi Azure Media Services przy użyciu portalu Azure hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="725e3-126">toocreate one, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="725e3-127">Logowanie się przy [Program firmy Apple Development](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="725e3-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="725e3-128">Firma Apple wymaga hello właściciela zawartości tooobtain hello [pakietu wdrożeniowego](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="725e3-128">Apple requires hello content owner tooobtain hello [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="725e3-129">Stan już zaimplementowany klucza modułu zabezpieczeń (KSM) z usługi Media Services, a następnie żądają hello pakiet klatek na Sekundę.</span><span class="sxs-lookup"><span data-stu-id="725e3-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting hello final FPS package.</span></span> <span data-ttu-id="725e3-130">Istnieją instrukcje hello końcowego kl. / s pakietu toogenerate certyfikacji i uzyskiwanie hello klucz tajny aplikacji (poproś).</span><span class="sxs-lookup"><span data-stu-id="725e3-130">There are instructions in hello final FPS package toogenerate certification and obtain hello Application Secret Key (ASK).</span></span> <span data-ttu-id="725e3-131">Możesz użyć poproś tooconfigure FairPlay.</span><span class="sxs-lookup"><span data-stu-id="725e3-131">You use ASK tooconfigure FairPlay.</span></span>
  * <span data-ttu-id="725e3-132">Wersja Azure .NET SDK usługi Media Services **3.6.0** lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="725e3-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="725e3-133">po stronie klucza dostawy Media Services musi być ustawione hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="725e3-133">hello following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="725e3-134">**Aplikacja certyfikatu (AC)**: jest to plik PFX zawierający klucz prywatny hello.</span><span class="sxs-lookup"><span data-stu-id="725e3-134">**App Cert (AC)**: This is a .pfx file that contains hello private key.</span></span> <span data-ttu-id="725e3-135">Utwórz ten plik i szyfrowania za pomocą hasła.</span><span class="sxs-lookup"><span data-stu-id="725e3-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="725e3-136">Po skonfigurowaniu zasad klucza dostawy, należy podać ten plik PFX hasło i hello w formacie Base64.</span><span class="sxs-lookup"><span data-stu-id="725e3-136">When you configure a key delivery policy, you must provide that password and hello .pfx file in Base64 format.</span></span>

      <span data-ttu-id="725e3-137">Witaj następujące kroki opisano, jak plik FairPlay toogenerate certyfikatu PFX:</span><span class="sxs-lookup"><span data-stu-id="725e3-137">hello following steps describe how toogenerate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="725e3-138">Zainstaluj biblioteki OpenSSL z https://slproweb.com/products/Win32OpenSSL.html.</span><span class="sxs-lookup"><span data-stu-id="725e3-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="725e3-139">Przejdź toohello folder zawierający certyfikat FairPlay hello i inne pliki dostarczane przez firmę Apple.</span><span class="sxs-lookup"><span data-stu-id="725e3-139">Go toohello folder where hello FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="725e3-140">Uruchom następujące polecenie z wiersza polecenia hello hello.</span><span class="sxs-lookup"><span data-stu-id="725e3-140">Run hello following command from hello command line.</span></span> <span data-ttu-id="725e3-141">Konwertuje to plik PEM tooa pliku .cer hello.</span><span class="sxs-lookup"><span data-stu-id="725e3-141">This converts hello .cer file tooa .pem file.</span></span>

        <span data-ttu-id="725e3-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509-informuje der — w fairplay.cer-out fairplay out.pem</span><span class="sxs-lookup"><span data-stu-id="725e3-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="725e3-143">Uruchom następujące polecenie z wiersza polecenia hello hello.</span><span class="sxs-lookup"><span data-stu-id="725e3-143">Run hello following command from hello command line.</span></span> <span data-ttu-id="725e3-144">Plik PFX tooa pliku PEM hello to konwertuje hello kluczem prywatnym.</span><span class="sxs-lookup"><span data-stu-id="725e3-144">This converts hello .pem file tooa .pfx file with hello private key.</span></span> <span data-ttu-id="725e3-145">następnie o Hello hasło pliku PFX hello biblioteki OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="725e3-145">hello password for hello .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="725e3-146">Pkcs12 "C:\OpenSSL-Win32\bin\openssl.exe"-Eksportowanie — limit fairplay out.pfx-inkey privatekey.pem — w file:privatekey-pem-pass.txt - passin fairplay out.pem</span><span class="sxs-lookup"><span data-stu-id="725e3-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="725e3-147">**Hasło certyfikatu aplikacji**: hello hasło do utworzenia pliku PFX hello.</span><span class="sxs-lookup"><span data-stu-id="725e3-147">**App Cert password**: hello password for creating hello .pfx file.</span></span>
  * <span data-ttu-id="725e3-148">**Identyfikator hasła aplikacji Cert**: musisz przekazać hello hasła, podobne toohow one przekazać kluczy usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="725e3-148">**App Cert password ID**: You must upload hello password, similar toohow they upload other Media Services keys.</span></span> <span data-ttu-id="725e3-149">Użyj hello **ContentKeyType.FairPlayPfxPassword** hello tooget wartość enum nośnika identyfikatora usługi.</span><span class="sxs-lookup"><span data-stu-id="725e3-149">Use hello **ContentKeyType.FairPlayPfxPassword** enum value tooget hello Media Services ID.</span></span> <span data-ttu-id="725e3-150">Jest to, co potrzebne toouse wewnątrz opcji zasad hello klucza dostawy.</span><span class="sxs-lookup"><span data-stu-id="725e3-150">This is what they need toouse inside hello key delivery policy option.</span></span>
  * <span data-ttu-id="725e3-151">**IV**: jest to wartość losowe 16 bajtów.</span><span class="sxs-lookup"><span data-stu-id="725e3-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="725e3-152">Musi on być zgodny hello iv w zasad dostarczania elementów zawartości hello.</span><span class="sxs-lookup"><span data-stu-id="725e3-152">It must match hello iv in hello asset delivery policy.</span></span> <span data-ttu-id="725e3-153">Możesz wygenerować hello iv i umieszcza je w obu miejscach: zasady dostarczania elementu zawartości hello i opcji zasad hello klucza dostawy.</span><span class="sxs-lookup"><span data-stu-id="725e3-153">You generate hello iv, and put it in both places: hello asset delivery policy and hello key delivery policy option.</span></span>
  * <span data-ttu-id="725e3-154">**Poproś**: podczas generowania hello certyfikacji za pomocą portalu dla deweloperów firmy Apple hello otrzymania tego klucza.</span><span class="sxs-lookup"><span data-stu-id="725e3-154">**ASK**: This key is received when you generate hello certification by using hello Apple Developer portal.</span></span> <span data-ttu-id="725e3-155">Każdy zespół deweloperów otrzyma unikatowy poproś.</span><span class="sxs-lookup"><span data-stu-id="725e3-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="725e3-156">Zapisz kopię hello poproś i przechowuj go w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="725e3-156">Save a copy of hello ASK, and store it in a safe place.</span></span> <span data-ttu-id="725e3-157">Konieczne będzie tooconfigure poproś jako FairPlayAsk tooMedia usługi później.</span><span class="sxs-lookup"><span data-stu-id="725e3-157">You will need tooconfigure ASK as FairPlayAsk tooMedia Services later.</span></span>
  * <span data-ttu-id="725e3-158">**Poproś identyfikator**: ten identyfikator jest uzyskiwany podczas przekazywania poproś do usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="725e3-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="725e3-159">Należy przekazać poproś przy użyciu hello **ContentKeyType.FairPlayAsk** wartości wyliczenia.</span><span class="sxs-lookup"><span data-stu-id="725e3-159">You must upload ASK by using hello **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="725e3-160">W wyniku hello hello Media Services ID jest zwracany, co jest przeznaczenia, ustawiając opcję zasad klucza dostawy hello.</span><span class="sxs-lookup"><span data-stu-id="725e3-160">As hello result, hello Media Services ID is returned, and this is what should be used when setting hello key delivery policy option.</span></span>

<span data-ttu-id="725e3-161">Witaj następujących czynności należy ustawić hello kl. / s po stronie klienta:</span><span class="sxs-lookup"><span data-stu-id="725e3-161">hello following things must be set by hello FPS client side:</span></span>

  * <span data-ttu-id="725e3-162">**Aplikacja certyfikatu (AC)**: jest to plik.cer/.der, który zawiera klucz publiczny hello, korzysta z systemu operacyjnego hello tooencrypt niektórych ładunku.</span><span class="sxs-lookup"><span data-stu-id="725e3-162">**App Cert (AC)**: This is a .cer/.der file that contains hello public key, which hello operating system uses tooencrypt some payload.</span></span> <span data-ttu-id="725e3-163">Usługi Media Services musi tooknow informacji na ten temat, ponieważ jest to wymagane przez odtwarzacz hello.</span><span class="sxs-lookup"><span data-stu-id="725e3-163">Media Services needs tooknow about it because it is required by hello player.</span></span> <span data-ttu-id="725e3-164">usługi dostarczania klucza Hello odszyfrowuje ją przy użyciu odpowiedniego klucza prywatnego hello.</span><span class="sxs-lookup"><span data-stu-id="725e3-164">hello key delivery service decrypts it using hello corresponding private key.</span></span>

<span data-ttu-id="725e3-165">tooplay kopii FairPlay strumienia zaszyfrowane, uzyskać pierwszy rzeczywistych poproś i następnie wygenerować rzeczywistych certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="725e3-165">tooplay back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="725e3-166">Ten proces tworzy wszystkich trzech części:</span><span class="sxs-lookup"><span data-stu-id="725e3-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="725e3-167">pliku der</span><span class="sxs-lookup"><span data-stu-id="725e3-167">.der file</span></span>
  * <span data-ttu-id="725e3-168">plik PFX</span><span class="sxs-lookup"><span data-stu-id="725e3-168">.pfx file</span></span>
  * <span data-ttu-id="725e3-169">hasło dla pliku PFX hello</span><span class="sxs-lookup"><span data-stu-id="725e3-169">password for hello .pfx</span></span>

<span data-ttu-id="725e3-170">Witaj następujący klienci obsługuje HLS z **CBC AES-128** szyfrowania: Safari w systemie iOS Apple TV, OS X.</span><span class="sxs-lookup"><span data-stu-id="725e3-170">hello following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="725e3-171">Konfigurowanie FairPlay dynamicznego szyfrowania i licencji dostarczania usług</span><span class="sxs-lookup"><span data-stu-id="725e3-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="725e3-172">Witaj poniżej przedstawiono ogólne kroki do ochrony zasobów z FairPlay przy użyciu usługi dostarczania licencji Media Services hello, a także za pomocą szyfrowania dynamicznego.</span><span class="sxs-lookup"><span data-stu-id="725e3-172">hello following are general steps for protecting your assets with FairPlay by using hello Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="725e3-173">Utworzenie elementu zawartości i przekazywanie plików do zawartości hello.</span><span class="sxs-lookup"><span data-stu-id="725e3-173">Create an asset, and upload files into hello asset.</span></span>
2. <span data-ttu-id="725e3-174">Kodowanie zawartości hello, który zawiera hello pliku toohello o adaptacyjnej szybkości bitowej MP4 ustawiona.</span><span class="sxs-lookup"><span data-stu-id="725e3-174">Encode hello asset that contains hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="725e3-175">Utwórz klucz zawartości i skojarzyć go z zasobów hello zakodowany.</span><span class="sxs-lookup"><span data-stu-id="725e3-175">Create a content key, and associate it with hello encoded asset.</span></span>  
4. <span data-ttu-id="725e3-176">Skonfiguruj zasady autoryzacji klucza zawartości hello.</span><span class="sxs-lookup"><span data-stu-id="725e3-176">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="725e3-177">Określ następujące hello:</span><span class="sxs-lookup"><span data-stu-id="725e3-177">Specify hello following:</span></span>

   * <span data-ttu-id="725e3-178">Metoda dostarczania Hello (w tym przypadku FairPlay).</span><span class="sxs-lookup"><span data-stu-id="725e3-178">hello delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="725e3-179">FairPlay konfiguracji opcje zasad.</span><span class="sxs-lookup"><span data-stu-id="725e3-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="725e3-180">Aby uzyskać więcej informacji na temat tooconfigure FairPlay, zobacz hello **ConfigureFairPlayPolicyOptions()** w poniższym przykładzie hello metody.</span><span class="sxs-lookup"><span data-stu-id="725e3-180">For details on how tooconfigure FairPlay, see hello **ConfigureFairPlayPolicyOptions()** method in hello sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="725e3-181">Zwykle czy chcesz tooconfigure zasad FairPlay opcje tylko raz, ponieważ będzie mieć tylko jeden zestaw certyfikacji i poproś.</span><span class="sxs-lookup"><span data-stu-id="725e3-181">Usually, you would want tooconfigure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="725e3-182">Ograniczenia (otwarte lub tokenu).</span><span class="sxs-lookup"><span data-stu-id="725e3-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="725e3-183">Informacje typu klucza dostawy określonych toohello, który definiuje sposób dostawy klucza powitania klienta toohello.</span><span class="sxs-lookup"><span data-stu-id="725e3-183">Information specific toohello key delivery type that defines how hello key is delivered toohello client.</span></span>
5. <span data-ttu-id="725e3-184">Skonfiguruj zasady dostarczania elementu zawartości hello.</span><span class="sxs-lookup"><span data-stu-id="725e3-184">Configure hello asset delivery policy.</span></span> <span data-ttu-id="725e3-185">Konfiguracja zasady dostarczania Hello obejmuje:</span><span class="sxs-lookup"><span data-stu-id="725e3-185">hello delivery policy configuration includes:</span></span>

   * <span data-ttu-id="725e3-186">Protokół dostarczania Hello (HLS).</span><span class="sxs-lookup"><span data-stu-id="725e3-186">hello delivery protocol (HLS).</span></span>
   * <span data-ttu-id="725e3-187">Witaj typ szyfrowania dynamicznego (typowe szyfrowanie CBC).</span><span class="sxs-lookup"><span data-stu-id="725e3-187">hello type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="725e3-188">adres URL pozyskiwania licencji Hello.</span><span class="sxs-lookup"><span data-stu-id="725e3-188">hello license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="725e3-189">Jeśli chcesz toodeliver strumienia, który jest szyfrowana za FairPlay i innego systemu zarządzania prawami cyfrowymi (DRM), masz zasady dostarczania oddzielnych tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="725e3-189">If you want toodeliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have tooconfigure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="725e3-190">Jeden tooconfigure IAssetDeliveryPolicy dynamiczne adaptacyjne przesyłanie strumieniowe za pośrednictwem protokołu HTTP (DASH) z wspólnego szyfrowania (CENC) (PlayReady i Widevine) i Smooth za pomocą PlayReady</span><span class="sxs-lookup"><span data-stu-id="725e3-190">One IAssetDeliveryPolicy tooconfigure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="725e3-191">Inny tooconfigure IAssetDeliveryPolicy FairPlay dla protokołu HLS</span><span class="sxs-lookup"><span data-stu-id="725e3-191">Another IAssetDeliveryPolicy tooconfigure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="725e3-192">Utwórz tooget lokalizatora OnDemand adresu URL przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="725e3-192">Create an OnDemand locator tooget a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="725e3-193">Aby użyć klucza dostawy FairPlay aplikacji odtwarzacza</span><span class="sxs-lookup"><span data-stu-id="725e3-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="725e3-194">Aplikacji odtwarzacza można programować za pomocą hello iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="725e3-194">You can develop player apps by using hello iOS SDK.</span></span> <span data-ttu-id="725e3-195">toobe stanie tooplay FairPlay zawartości, masz tooimplement hello licencji exchange protokołu.</span><span class="sxs-lookup"><span data-stu-id="725e3-195">toobe able tooplay FairPlay content, you have tooimplement hello license exchange protocol.</span></span> <span data-ttu-id="725e3-196">Ten protokół nie jest określony przez firmę Apple.</span><span class="sxs-lookup"><span data-stu-id="725e3-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="725e3-197">Jest zapasowej aplikacji tooeach sposób dostawy klucza toosend żądań.</span><span class="sxs-lookup"><span data-stu-id="725e3-197">It is up tooeach app how toosend key delivery requests.</span></span> <span data-ttu-id="725e3-198">Hello Media Services FairPlay klucza dostawy usług oczekuje hello SPC toocome jako www-form-url post zakodowany komunikat w hello następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="725e3-198">hello Media Services FairPlay key delivery service expects hello SPC toocome as a www-form-url encoded post message, in hello following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="725e3-199">Azure Media Player nie obsługuje odtwarzania FairPlay fabrycznej hello.</span><span class="sxs-lookup"><span data-stu-id="725e3-199">Azure Media Player doesn’t support FairPlay playback out of hello box.</span></span> <span data-ttu-id="725e3-200">odtwarzanie FairPlay tooget w systemie MAC OS X, uzyskać player próbki hello hello konta dewelopera firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="725e3-200">tooget FairPlay playback on MAC OS X, obtain hello sample player from hello Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="725e3-201">Adresy URL przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="725e3-201">Streaming URLs</span></span>
<span data-ttu-id="725e3-202">Jeśli zawartości została zaszyfrowana z więcej niż jeden DRM, należy użyć tag szyfrowania w hello URL przesyłania strumieniowego: (format = "m3u8-aapl, szyfrowanie = 'xxx').</span><span class="sxs-lookup"><span data-stu-id="725e3-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in hello streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="725e3-203">Zastosuj Hello następujące zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="725e3-203">hello following considerations apply:</span></span>

* <span data-ttu-id="725e3-204">Można określić tylko zero lub jeden typ szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="725e3-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="725e3-205">Typ szyfrowania Hello nie ma toobe określona w adresie URL hello, jeśli tylko jeden szyfrowania został zastosowany toohello zasobów.</span><span class="sxs-lookup"><span data-stu-id="725e3-205">hello encryption type doesn't have toobe specified in hello URL if only one encryption was applied toohello asset.</span></span>
* <span data-ttu-id="725e3-206">Typ szyfrowania Hello jest uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="725e3-206">hello encryption type is case insensitive.</span></span>
* <span data-ttu-id="725e3-207">można określić Hello następujące typy szyfrowania:</span><span class="sxs-lookup"><span data-stu-id="725e3-207">hello following encryption types can be specified:</span></span>  
  * <span data-ttu-id="725e3-208">**cenc**: szyfrowania Common encryption (PlayReady lub Widevine)</span><span class="sxs-lookup"><span data-stu-id="725e3-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="725e3-209">**cbcs-aapl**: FairPlay</span><span class="sxs-lookup"><span data-stu-id="725e3-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="725e3-210">**CBC**: szyfrowanie AES envelope</span><span class="sxs-lookup"><span data-stu-id="725e3-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="725e3-211">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="725e3-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="725e3-212">Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="725e3-212">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="725e3-213">Dodaj następujące elementy zbyt hello**appSettings** zdefiniowane w pliku app.config:</span><span class="sxs-lookup"><span data-stu-id="725e3-213">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="725e3-214">Przykład</span><span class="sxs-lookup"><span data-stu-id="725e3-214">Example</span></span>

<span data-ttu-id="725e3-215">Hello następujące przykładowe pokazuje hello możliwości toouse toodeliver Media Services zaszyfrowane za pomocą FairPlay zawartości.</span><span class="sxs-lookup"><span data-stu-id="725e3-215">hello following sample demonstrates hello ability toouse Media Services toodeliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="725e3-216">Ta funkcja została wprowadzona w hello Azure Media Services SDK dla platformy .NET w wersji 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="725e3-216">This functionality was introduced in hello Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="725e3-217">Zastąp hello kodu w pliku Program.cs kodem hello przedstawionym w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="725e3-217">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="725e3-218">Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="725e3-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="725e3-219">Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / dostęp uprawnień, na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (zasady — przekazywanie).</span><span class="sxs-lookup"><span data-stu-id="725e3-219">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="725e3-220">Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.</span><span class="sxs-lookup"><span data-stu-id="725e3-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="725e3-221">Upewnij się, że zmienne tooupdate toopoint toofolders gdzie znajdują się pliki danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="725e3-221">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.FairPlay;
    using Newtonsoft.Json;
    using System.Security.Cryptography.X509Certificates;

    namespace DynamicEncryptionWithFairPlay
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonCBCTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("FairPlay License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted HLS URL: {0}/manifest(format=m3u8-aapl)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding {0}", inputAsset.Name));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }

        static public IContentKey CreateCommonCBCTypeContentKey(IAsset asset)
        {
            // Create HLS SAMPLE AES encryption content key
            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryptionCbcs);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }


        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {
            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Open",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                        Requirements = null
                    }
                    };


            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();

            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
            ContentKeyDeliveryType.FairPlay,
            restrictions,
            FairPlayConfiguration);


            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with no restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                    {
                    new ContentKeyAuthorizationPolicyRestriction
                    {
                        Name = "Token Authorization Policy",
                        KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                        Requirements = tokenTemplateString,
                    }
                    };

            // Configure FairPlay policy option.
            string FairPlayConfiguration = ConfigureFairPlayPolicyOptions();


            IContentKeyAuthorizationPolicyOption FairPlayPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                   ContentKeyDeliveryType.FairPlay,
                   restrictions,
                   FairPlayConfiguration);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common CBC Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(FairPlayPolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with hello cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound tooa real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key toogenerate hello response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating hello .pfx file.
            string pfxPassword = "<customer password for creating hello .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key toogenerate hello response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match hello iv in hello asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify hello .pfx file created by hello customer.
            var appCert = new X509Certificate2("path toohello .pfx file created by hello customer", pfxPassword, X509KeyStorageFlags.Exportable);

            string FairPlayConfiguration =
            Microsoft.WindowsAzure.MediaServices.Client.FairPlay.FairPlayConfiguration.CreateSerializedFairPlayOptionConfiguration(
                appCert,
                pfxPassword,
                pfxPasswordId,
                askId,
                iv);

            return FairPlayConfiguration;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();
            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            var kdPolicy = _context.ContentKeyAuthorizationPolicies.Where(p => p.Id == key.AuthorizationPolicyId).Single();

            var kdOption = kdPolicy.Options.Single(o => o.KeyDeliveryType == ContentKeyDeliveryType.FairPlay);

            FairPlayConfiguration configFP = JsonConvert.DeserializeObject<FairPlayConfiguration>(kdOption.KeyDeliveryConfiguration);

            // Get hello FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // hello reason hello below code replaces "https://" with "skd://" is because
            // in hello IOS player sample code which you obtained in Apple developer account,
            // hello player only recognizes a Key URL that starts with skd://.
            // However, if you are using a customized player,
            // you can choose whatever protocol you want.
            // For example, "https".

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.FairPlayLicenseAcquisitionUrl, acquisitionUrl.ToString().Replace("https://", "skd://")},
                    {AssetDeliveryPolicyConfigurationKey.CommonEncryptionIVForCbcs, configFP.ContentEncryptionIV}
            };

            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryptionCbcs,
            AssetDeliveryProtocol.HLS,
            assetDeliveryPolicyConfiguration);

            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="725e3-222">Następne kroki: ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="725e3-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="725e3-223">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="725e3-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
