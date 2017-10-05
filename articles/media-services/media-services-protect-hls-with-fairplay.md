---
title: "Ochrona zawartości z Microsoft PlayReady lub Apple FairPlay - Azure HLS | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera omówienie i pokazuje, jak używać usługi Azure Media Services do dynamicznego szyfrowania zawartości HTTP Live Streaming (HLS) przy użyciu FairPlay firmy Apple. Ponadto sposobu korzystania z usługi dostarczania licencji Media Services dostarczać licencje FairPlay do klientów."
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
ms.openlocfilehash: 895d6307b1cef74e195cc2ffd8dbef4196e97b1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="protect-your-hls-content-with-apple-fairplay-or-microsoft-playready"></a><span data-ttu-id="0f947-104">Ochrona programu HLS zawartości z FairPlay firmy Apple lub Microsoft PlayReady</span><span class="sxs-lookup"><span data-stu-id="0f947-104">Protect your HLS content with Apple FairPlay or Microsoft PlayReady</span></span>
<span data-ttu-id="0f947-105">Usługa Azure Media Services umożliwia dynamicznego szyfrowania zawartości HTTP Live Streaming (HLS) przy użyciu następujących formatów:</span><span class="sxs-lookup"><span data-stu-id="0f947-105">Azure Media Services enables you to dynamically encrypt your HTTP Live Streaming (HLS) content by using the following formats:</span></span>  

* <span data-ttu-id="0f947-106">**Koperty AES-128, klucz niezaszyfrowany**</span><span class="sxs-lookup"><span data-stu-id="0f947-106">**AES-128 envelope clear key**</span></span>

    <span data-ttu-id="0f947-107">Cały fragmentów są szyfrowane przy użyciu **CBC AES-128** tryb.</span><span class="sxs-lookup"><span data-stu-id="0f947-107">The entire chunk is encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="0f947-108">Odszyfrowywanie strumień jest obsługiwany natywnie przez systemów iOS i OS X player.</span><span class="sxs-lookup"><span data-stu-id="0f947-108">The decryption of the stream is supported by iOS and OS X player natively.</span></span> <span data-ttu-id="0f947-109">Aby uzyskać więcej informacji, zobacz [dynamicznego szyfrowania przy użyciu standardu AES-128 i usługi dostarczania klucza](media-services-protect-with-aes128.md).</span><span class="sxs-lookup"><span data-stu-id="0f947-109">For more information, see [Using AES-128 dynamic encryption and key delivery service](media-services-protect-with-aes128.md).</span></span>
* <span data-ttu-id="0f947-110">**FairPlay firmy Apple**</span><span class="sxs-lookup"><span data-stu-id="0f947-110">**Apple FairPlay**</span></span>

    <span data-ttu-id="0f947-111">Poszczególne próbki audio i wideo są szyfrowane przy użyciu **CBC AES-128** tryb.</span><span class="sxs-lookup"><span data-stu-id="0f947-111">The individual video and audio samples are encrypted by using the **AES-128 CBC** mode.</span></span> <span data-ttu-id="0f947-112">**Przesyłanie strumieniowe FairPlay** (kl. / s) jest zintegrowany z systemów operacyjnych urządzeń macierzystą obsługę w systemach iOS i Apple TV.</span><span class="sxs-lookup"><span data-stu-id="0f947-112">**FairPlay Streaming** (FPS) is integrated into the device operating systems, with native support on iOS and Apple TV.</span></span> <span data-ttu-id="0f947-113">Przeglądarka Safari w OS X umożliwia klatek na Sekundę przy użyciu funkcji obsługi interfejsu szyfrowane nośnika rozszerzenia (EME).</span><span class="sxs-lookup"><span data-stu-id="0f947-113">Safari on OS X enables FPS by using the Encrypted Media Extensions (EME) interface support.</span></span>
* <span data-ttu-id="0f947-114">**Microsoft PlayReady**</span><span class="sxs-lookup"><span data-stu-id="0f947-114">**Microsoft PlayReady**</span></span>

<span data-ttu-id="0f947-115">Poniższy obraz przedstawia **HLS + FairPlay lub PlayReady szyfrowania dynamicznego** przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="0f947-115">The following image shows the **HLS + FairPlay or PlayReady dynamic encryption** workflow.</span></span>

![Diagram przepływu pracy szyfrowania dynamicznego](./media/media-services-content-protection-overview/media-services-content-protection-with-fairplay.png)

<span data-ttu-id="0f947-117">W tym temacie przedstawiono sposób korzystania z usługi Media Services do dynamicznego szyfrowania zawartości HLS przy użyciu FairPlay firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="0f947-117">This topic demonstrates how to use Media Services to dynamically encrypt your HLS content with Apple FairPlay.</span></span> <span data-ttu-id="0f947-118">Ponadto sposobu korzystania z usługi dostarczania licencji Media Services dostarczać licencje FairPlay do klientów.</span><span class="sxs-lookup"><span data-stu-id="0f947-118">It also shows how to use the Media Services license delivery service to deliver FairPlay licenses to clients.</span></span>

> [!NOTE]
> <span data-ttu-id="0f947-119">Jeśli chcesz także do szyfrowania treści HLS za pomocą PlayReady, należy utworzyć wspólny klucz zawartości i powiązać ją z zawartości.</span><span class="sxs-lookup"><span data-stu-id="0f947-119">If you also want to encrypt your HLS content with PlayReady, you need to create a common content key and associate it with your asset.</span></span> <span data-ttu-id="0f947-120">Należy również skonfigurować zasady autoryzacji klucza zawartości, zgodnie z opisem w [za pomocą PlayReady, dynamicznego szyfrowania common encryption](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="0f947-120">You also need to configure the content key’s authorization policy, as described in [Using PlayReady dynamic common encryption](media-services-protect-with-drm.md).</span></span>
>
>

## <a name="requirements-and-considerations"></a><span data-ttu-id="0f947-121">Wymagania i uwagi</span><span class="sxs-lookup"><span data-stu-id="0f947-121">Requirements and considerations</span></span>

<span data-ttu-id="0f947-122">Poniżej są wymagane w przypadku przy użyciu usługi Media Services, aby dostarczać HLS zaszyfrowanych z FairPlay i dostarczać licencje FairPlay:</span><span class="sxs-lookup"><span data-stu-id="0f947-122">The following are required when using Media Services to deliver HLS encrypted with FairPlay, and to deliver FairPlay licenses:</span></span>

  * <span data-ttu-id="0f947-123">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0f947-123">An Azure account.</span></span> <span data-ttu-id="0f947-124">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna systemu Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="0f947-124">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
  * <span data-ttu-id="0f947-125">Konto usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="0f947-125">A Media Services account.</span></span> <span data-ttu-id="0f947-126">Aby go utworzyć, zobacz [utworzyć konto usługi Azure Media Services przy użyciu portalu Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="0f947-126">To create one, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
  * <span data-ttu-id="0f947-127">Logowanie się przy [Program firmy Apple Development](https://developer.apple.com/).</span><span class="sxs-lookup"><span data-stu-id="0f947-127">Sign up with [Apple Development Program](https://developer.apple.com/).</span></span>
  * <span data-ttu-id="0f947-128">Firma Apple wymaga właściciela zawartości uzyskać [pakietu wdrożeniowego](https://developer.apple.com/contact/fps/).</span><span class="sxs-lookup"><span data-stu-id="0f947-128">Apple requires the content owner to obtain the [deployment package](https://developer.apple.com/contact/fps/).</span></span> <span data-ttu-id="0f947-129">Stan już zaimplementowany klucza modułu zabezpieczeń (KSM) z usługi Media Services, a następnie żądają końcowego pakietu kl. / s.</span><span class="sxs-lookup"><span data-stu-id="0f947-129">State that you already implemented Key Security Module (KSM) with Media Services, and that you are requesting the final FPS package.</span></span> <span data-ttu-id="0f947-130">Nie ma instrukcji w pakiecie końcowego kl. / s do generowania certyfikacji i uzyskać klucz tajny aplikacji (poproś).</span><span class="sxs-lookup"><span data-stu-id="0f947-130">There are instructions in the final FPS package to generate certification and obtain the Application Secret Key (ASK).</span></span> <span data-ttu-id="0f947-131">Poproś są używane do konfigurowania FairPlay.</span><span class="sxs-lookup"><span data-stu-id="0f947-131">You use ASK to configure FairPlay.</span></span>
  * <span data-ttu-id="0f947-132">Wersja Azure .NET SDK usługi Media Services **3.6.0** lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="0f947-132">Azure Media Services .NET SDK version **3.6.0** or later.</span></span>

<span data-ttu-id="0f947-133">Po stronie klucza dostawy Media Services musi być ustawione następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0f947-133">The following things must be set on Media Services key delivery side:</span></span>

  * <span data-ttu-id="0f947-134">**Aplikacja certyfikatu (AC)**: jest to plik PFX zawierający klucz prywatny.</span><span class="sxs-lookup"><span data-stu-id="0f947-134">**App Cert (AC)**: This is a .pfx file that contains the private key.</span></span> <span data-ttu-id="0f947-135">Utwórz ten plik i szyfrowania za pomocą hasła.</span><span class="sxs-lookup"><span data-stu-id="0f947-135">You create this file and encrypt it with a password.</span></span>

       <span data-ttu-id="0f947-136">Po skonfigurowaniu zasad klucza dostawy, musisz podać to hasło, a plik pfx w formacie Base64.</span><span class="sxs-lookup"><span data-stu-id="0f947-136">When you configure a key delivery policy, you must provide that password and the .pfx file in Base64 format.</span></span>

      <span data-ttu-id="0f947-137">W poniższych krokach opisano sposób generowania pliku certyfikatu PFX dla FairPlay:</span><span class="sxs-lookup"><span data-stu-id="0f947-137">The following steps describe how to generate a .pfx certificate file for FairPlay:</span></span>

    1. <span data-ttu-id="0f947-138">Zainstaluj biblioteki OpenSSL z https://slproweb.com/products/Win32OpenSSL.html.</span><span class="sxs-lookup"><span data-stu-id="0f947-138">Install OpenSSL from https://slproweb.com/products/Win32OpenSSL.html.</span></span>

        <span data-ttu-id="0f947-139">Przejdź do folderu, w których są certyfikatu FairPlay i inne pliki dostarczane przez firmę Apple.</span><span class="sxs-lookup"><span data-stu-id="0f947-139">Go to the folder where the FairPlay certificate and other files delivered by Apple are.</span></span>
    2. <span data-ttu-id="0f947-140">W wierszu polecenia uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="0f947-140">Run the following command from the command line.</span></span> <span data-ttu-id="0f947-141">Plik .cer to konwertuje plik PEM.</span><span class="sxs-lookup"><span data-stu-id="0f947-141">This converts the .cer file to a .pem file.</span></span>

        <span data-ttu-id="0f947-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509-informuje der — w fairplay.cer-out fairplay out.pem</span><span class="sxs-lookup"><span data-stu-id="0f947-142">"C:\OpenSSL-Win32\bin\openssl.exe" x509 -inform der -in fairplay.cer -out fairplay-out.pem</span></span>
    3. <span data-ttu-id="0f947-143">W wierszu polecenia uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="0f947-143">Run the following command from the command line.</span></span> <span data-ttu-id="0f947-144">Plik PEM to konwertuje do pliku .pfx z kluczem prywatnym.</span><span class="sxs-lookup"><span data-stu-id="0f947-144">This converts the .pem file to a .pfx file with the private key.</span></span> <span data-ttu-id="0f947-145">Biblioteki OpenSSL następnie o hasło pliku pfx.</span><span class="sxs-lookup"><span data-stu-id="0f947-145">The password for the .pfx file is then asked by OpenSSL.</span></span>

        <span data-ttu-id="0f947-146">Pkcs12 "C:\OpenSSL-Win32\bin\openssl.exe"-Eksportowanie — limit fairplay out.pfx-inkey privatekey.pem — w file:privatekey-pem-pass.txt - passin fairplay out.pem</span><span class="sxs-lookup"><span data-stu-id="0f947-146">"C:\OpenSSL-Win32\bin\openssl.exe" pkcs12 -export -out fairplay-out.pfx -inkey privatekey.pem -in fairplay-out.pem -passin file:privatekey-pem-pass.txt</span></span>
  * <span data-ttu-id="0f947-147">**Hasło certyfikatu aplikacji**: hasło do utworzenia pliku .pfx.</span><span class="sxs-lookup"><span data-stu-id="0f947-147">**App Cert password**: The password for creating the .pfx file.</span></span>
  * <span data-ttu-id="0f947-148">**Identyfikator hasła aplikacji Cert**: musisz przekazać hasła, podobnie jak ich przekazać kluczy usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="0f947-148">**App Cert password ID**: You must upload the password, similar to how they upload other Media Services keys.</span></span> <span data-ttu-id="0f947-149">Użyj **ContentKeyType.FairPlayPfxPassword** wartości wyliczenia, aby uzyskać nazwę usługi multimediów.</span><span class="sxs-lookup"><span data-stu-id="0f947-149">Use the **ContentKeyType.FairPlayPfxPassword** enum value to get the Media Services ID.</span></span> <span data-ttu-id="0f947-150">Jest to, muszą zostać użyty w opcji zasad klucza dostawy.</span><span class="sxs-lookup"><span data-stu-id="0f947-150">This is what they need to use inside the key delivery policy option.</span></span>
  * <span data-ttu-id="0f947-151">**IV**: jest to wartość losowe 16 bajtów.</span><span class="sxs-lookup"><span data-stu-id="0f947-151">**iv**: This is a random value of 16 bytes.</span></span> <span data-ttu-id="0f947-152">Musi on być zgodny z iv w zasad dostarczania elementów zawartości.</span><span class="sxs-lookup"><span data-stu-id="0f947-152">It must match the iv in the asset delivery policy.</span></span> <span data-ttu-id="0f947-153">Generowanie iv i umieszcza je w obu miejscach: zasady dostarczania elementu zawartości i opcji zasad klucza dostawy.</span><span class="sxs-lookup"><span data-stu-id="0f947-153">You generate the iv, and put it in both places: the asset delivery policy and the key delivery policy option.</span></span>
  * <span data-ttu-id="0f947-154">**Poproś**: ten klucz jest odebrane podczas generowania certyfikacji za pomocą portalu dla deweloperów firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="0f947-154">**ASK**: This key is received when you generate the certification by using the Apple Developer portal.</span></span> <span data-ttu-id="0f947-155">Każdy zespół deweloperów otrzyma unikatowy poproś.</span><span class="sxs-lookup"><span data-stu-id="0f947-155">Each development team will receive a unique ASK.</span></span> <span data-ttu-id="0f947-156">Zapisz kopię ZADAJ i przechowuj go w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="0f947-156">Save a copy of the ASK, and store it in a safe place.</span></span> <span data-ttu-id="0f947-157">Należy skonfigurować poproś jako FairPlayAsk usługą Media Services.</span><span class="sxs-lookup"><span data-stu-id="0f947-157">You will need to configure ASK as FairPlayAsk to Media Services later.</span></span>
  * <span data-ttu-id="0f947-158">**Poproś identyfikator**: ten identyfikator jest uzyskiwany podczas przekazywania poproś do usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="0f947-158">**ASK ID**: This ID is obtained when you upload ASK into Media Services.</span></span> <span data-ttu-id="0f947-159">Należy przekazać poproś przy użyciu **ContentKeyType.FairPlayAsk** wartości wyliczenia.</span><span class="sxs-lookup"><span data-stu-id="0f947-159">You must upload ASK by using the **ContentKeyType.FairPlayAsk** enum value.</span></span> <span data-ttu-id="0f947-160">W rezultacie identyfikator usług Media jest zwracane, a jest przeznaczenia, ustawiając opcję zasady dostarczania klucza.</span><span class="sxs-lookup"><span data-stu-id="0f947-160">As the result, the Media Services ID is returned, and this is what should be used when setting the key delivery policy option.</span></span>

<span data-ttu-id="0f947-161">Po stronie klienta kl. / s musi być ustawione następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0f947-161">The following things must be set by the FPS client side:</span></span>

  * <span data-ttu-id="0f947-162">**Aplikacja certyfikatu (AC)**: jest to plik.cer/.der, który zawiera klucz prywatny, który używa systemu operacyjnego do szyfrowania niektórych ładunku.</span><span class="sxs-lookup"><span data-stu-id="0f947-162">**App Cert (AC)**: This is a .cer/.der file that contains the public key, which the operating system uses to encrypt some payload.</span></span> <span data-ttu-id="0f947-163">Usługa Media Services musi wiedzieć o on, ponieważ jest to wymagane przez odtwarzacz.</span><span class="sxs-lookup"><span data-stu-id="0f947-163">Media Services needs to know about it because it is required by the player.</span></span> <span data-ttu-id="0f947-164">Usługi dostarczania klucza odszyfrowuje ją przy użyciu odpowiedniego klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="0f947-164">The key delivery service decrypts it using the corresponding private key.</span></span>

<span data-ttu-id="0f947-165">Aby odtworzyć strumienia zaszyfrowanych FairPlay uzyskać rzeczywiste Poproś pierwszy, a następnie wygeneruj rzeczywistych certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0f947-165">To play back a FairPlay encrypted stream, get a real ASK first, and then generate a real certificate.</span></span> <span data-ttu-id="0f947-166">Ten proces tworzy wszystkich trzech części:</span><span class="sxs-lookup"><span data-stu-id="0f947-166">That process creates all three parts:</span></span>

  * <span data-ttu-id="0f947-167">pliku der</span><span class="sxs-lookup"><span data-stu-id="0f947-167">.der file</span></span>
  * <span data-ttu-id="0f947-168">plik PFX</span><span class="sxs-lookup"><span data-stu-id="0f947-168">.pfx file</span></span>
  * <span data-ttu-id="0f947-169">hasło dla pliku pfx</span><span class="sxs-lookup"><span data-stu-id="0f947-169">password for the .pfx</span></span>

<span data-ttu-id="0f947-170">Następujący klienci obsługuje HLS z **CBC AES-128** szyfrowania: Safari w systemie iOS Apple TV, OS X.</span><span class="sxs-lookup"><span data-stu-id="0f947-170">The following clients support HLS with **AES-128 CBC** encryption: Safari on OS X, Apple TV, iOS.</span></span>

## <a name="configure-fairplay-dynamic-encryption-and-license-delivery-services"></a><span data-ttu-id="0f947-171">Konfigurowanie FairPlay dynamicznego szyfrowania i licencji dostarczania usług</span><span class="sxs-lookup"><span data-stu-id="0f947-171">Configure FairPlay dynamic encryption and license delivery services</span></span>
<span data-ttu-id="0f947-172">Poniżej przedstawiono ogólne kroki do ochrony zasobów z FairPlay przy użyciu usługi dostarczania licencji Media Services, a także za pomocą szyfrowania dynamicznego.</span><span class="sxs-lookup"><span data-stu-id="0f947-172">The following are general steps for protecting your assets with FairPlay by using the Media Services license delivery service, and also by using dynamic encryption.</span></span>

1. <span data-ttu-id="0f947-173">Utworzenie elementu zawartości i przekazywanie plików do zawartości.</span><span class="sxs-lookup"><span data-stu-id="0f947-173">Create an asset, and upload files into the asset.</span></span>
2. <span data-ttu-id="0f947-174">Kodowanie zawartości, który zawiera plik o adaptacyjnej szybkości bitowej MP4 ustawiona.</span><span class="sxs-lookup"><span data-stu-id="0f947-174">Encode the asset that contains the file to the adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="0f947-175">Utwórz klucz zawartości i skojarzyć go z zakodowanym elementem zawartości.</span><span class="sxs-lookup"><span data-stu-id="0f947-175">Create a content key, and associate it with the encoded asset.</span></span>  
4. <span data-ttu-id="0f947-176">Skonfiguruj zasady autoryzacji klucza zawartości.</span><span class="sxs-lookup"><span data-stu-id="0f947-176">Configure the content key’s authorization policy.</span></span> <span data-ttu-id="0f947-177">Określ następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="0f947-177">Specify the following:</span></span>

   * <span data-ttu-id="0f947-178">Metoda dostarczania (w tym przypadku FairPlay).</span><span class="sxs-lookup"><span data-stu-id="0f947-178">The delivery method (in this case, FairPlay).</span></span>
   * <span data-ttu-id="0f947-179">FairPlay konfiguracji opcje zasad.</span><span class="sxs-lookup"><span data-stu-id="0f947-179">FairPlay policy options configuration.</span></span> <span data-ttu-id="0f947-180">Aby uzyskać więcej informacji na temat konfigurowania FairPlay, zobacz **ConfigureFairPlayPolicyOptions()** metody w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="0f947-180">For details on how to configure FairPlay, see the **ConfigureFairPlayPolicyOptions()** method in the sample below.</span></span>

     > [!NOTE]
     > <span data-ttu-id="0f947-181">Zwykle czy chcesz skonfigurować opcje zasad FairPlay tylko raz, ponieważ będzie mieć tylko jeden zestaw certyfikacji i poproś.</span><span class="sxs-lookup"><span data-stu-id="0f947-181">Usually, you would want to configure FairPlay policy options only once, because you will only have one set of a certification and an ASK.</span></span>
     >
     >
   * <span data-ttu-id="0f947-182">Ograniczenia (otwarte lub tokenu).</span><span class="sxs-lookup"><span data-stu-id="0f947-182">Restrictions (open or token).</span></span>
   * <span data-ttu-id="0f947-183">Informacje specyficzne dla typu klucza dostawy, który definiuje sposób dostawy klucza do klienta.</span><span class="sxs-lookup"><span data-stu-id="0f947-183">Information specific to the key delivery type that defines how the key is delivered to the client.</span></span>
5. <span data-ttu-id="0f947-184">Skonfiguruj zasady dostarczania elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="0f947-184">Configure the asset delivery policy.</span></span> <span data-ttu-id="0f947-185">Konfiguracja zasady dostarczania obejmuje:</span><span class="sxs-lookup"><span data-stu-id="0f947-185">The delivery policy configuration includes:</span></span>

   * <span data-ttu-id="0f947-186">Protokół dostarczania (HLS).</span><span class="sxs-lookup"><span data-stu-id="0f947-186">The delivery protocol (HLS).</span></span>
   * <span data-ttu-id="0f947-187">Typ szyfrowania dynamicznego (typowe szyfrowanie CBC).</span><span class="sxs-lookup"><span data-stu-id="0f947-187">The type of dynamic encryption (common CBC encryption).</span></span>
   * <span data-ttu-id="0f947-188">Adres URL pozyskiwania licencji.</span><span class="sxs-lookup"><span data-stu-id="0f947-188">The license acquisition URL.</span></span>

     > [!NOTE]
     > <span data-ttu-id="0f947-189">Jeśli chcesz dostarczyć strumienia, który jest szyfrowana za FairPlay i innego systemu zarządzania prawami cyfrowymi (DRM), należy skonfigurować zasady dostarczania oddzielne:</span><span class="sxs-lookup"><span data-stu-id="0f947-189">If you want to deliver a stream that is encrypted with FairPlay and another Digital Rights Management (DRM) system, you have to configure separate delivery policies:</span></span>
     >
     > * <span data-ttu-id="0f947-190">Jeden IAssetDeliveryPolicy, aby skonfigurować dynamiczne adaptacyjne przesyłanie strumieniowe za pośrednictwem protokołu HTTP (DASH) z wspólnego szyfrowania (CENC) (PlayReady i Widevine) i Smooth za pomocą PlayReady</span><span class="sxs-lookup"><span data-stu-id="0f947-190">One IAssetDeliveryPolicy to configure Dynamic Adaptive Streaming over HTTP (DASH) with Common Encryption (CENC) (PlayReady + Widevine), and Smooth with PlayReady</span></span>
     > * <span data-ttu-id="0f947-191">Inny IAssetDeliveryPolicy, aby skonfigurować FairPlay dla protokołu HLS</span><span class="sxs-lookup"><span data-stu-id="0f947-191">Another IAssetDeliveryPolicy to configure FairPlay for HLS</span></span>
     >
     >
6. <span data-ttu-id="0f947-192">Utwórz Lokalizator OnDemand w celu uzyskania adresu URL przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="0f947-192">Create an OnDemand locator to get a streaming URL.</span></span>

## <a name="use-fairplay-key-delivery-by-player-apps"></a><span data-ttu-id="0f947-193">Aby użyć klucza dostawy FairPlay aplikacji odtwarzacza</span><span class="sxs-lookup"><span data-stu-id="0f947-193">Use FairPlay key delivery by player apps</span></span>
<span data-ttu-id="0f947-194">Można programować aplikacje player przy użyciu zestawu SDK dla systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="0f947-194">You can develop player apps by using the iOS SDK.</span></span> <span data-ttu-id="0f947-195">Możliwość odtwarzania zawartości FairPlay, należy zaimplementować protokół wymiany licencji.</span><span class="sxs-lookup"><span data-stu-id="0f947-195">To be able to play FairPlay content, you have to implement the license exchange protocol.</span></span> <span data-ttu-id="0f947-196">Ten protokół nie jest określony przez firmę Apple.</span><span class="sxs-lookup"><span data-stu-id="0f947-196">This protocol is not specified by Apple.</span></span> <span data-ttu-id="0f947-197">Jest każda aplikacja sposób wysyłania żądań klucza dostawy.</span><span class="sxs-lookup"><span data-stu-id="0f947-197">It is up to each app how to send key delivery requests.</span></span> <span data-ttu-id="0f947-198">Usługi Media Services FairPlay klucza dostawy oczekuje SPC znaleziona jako www-form-url post zakodowany komunikat w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="0f947-198">The Media Services FairPlay key delivery service expects the SPC to come as a www-form-url encoded post message, in the following form:</span></span>

    spc=<Base64 encoded SPC>

> [!NOTE]
> <span data-ttu-id="0f947-199">Azure Media Player nie obsługuje odtwarzania FairPlay poza pole.</span><span class="sxs-lookup"><span data-stu-id="0f947-199">Azure Media Player doesn’t support FairPlay playback out of the box.</span></span> <span data-ttu-id="0f947-200">Uzyskanie odtwarzania FairPlay w systemie MAC OS X, uzyskać player próbki z konta dewelopera firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="0f947-200">To get FairPlay playback on MAC OS X, obtain the sample player from the Apple developer account.</span></span>
>
>

## <a name="streaming-urls"></a><span data-ttu-id="0f947-201">Adresy URL przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="0f947-201">Streaming URLs</span></span>
<span data-ttu-id="0f947-202">Jeśli zawartości została zaszyfrowana z więcej niż jeden DRM, należy użyć tag szyfrowania w adresie URL przesyłania strumieniowego: (format = "m3u8-aapl, szyfrowanie = 'xxx').</span><span class="sxs-lookup"><span data-stu-id="0f947-202">If your asset was encrypted with more than one DRM, you should use an encryption tag in the streaming URL: (format='m3u8-aapl', encryption='xxx').</span></span>

<span data-ttu-id="0f947-203">Następujące kwestie:</span><span class="sxs-lookup"><span data-stu-id="0f947-203">The following considerations apply:</span></span>

* <span data-ttu-id="0f947-204">Można określić tylko zero lub jeden typ szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="0f947-204">Only zero or one encryption type can be specified.</span></span>
* <span data-ttu-id="0f947-205">Typ szyfrowania nie ma określonego w adresie URL, jeśli tylko jeden szyfrowania została zastosowana do zasobu.</span><span class="sxs-lookup"><span data-stu-id="0f947-205">The encryption type doesn't have to be specified in the URL if only one encryption was applied to the asset.</span></span>
* <span data-ttu-id="0f947-206">Typ szyfrowania jest uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="0f947-206">The encryption type is case insensitive.</span></span>
* <span data-ttu-id="0f947-207">Można określić następujące typy szyfrowania:</span><span class="sxs-lookup"><span data-stu-id="0f947-207">The following encryption types can be specified:</span></span>  
  * <span data-ttu-id="0f947-208">**cenc**: szyfrowania Common encryption (PlayReady lub Widevine)</span><span class="sxs-lookup"><span data-stu-id="0f947-208">**cenc**:  Common encryption (PlayReady or Widevine)</span></span>
  * <span data-ttu-id="0f947-209">**cbcs-aapl**: FairPlay</span><span class="sxs-lookup"><span data-stu-id="0f947-209">**cbcs-aapl**: FairPlay</span></span>
  * <span data-ttu-id="0f947-210">**CBC**: szyfrowanie AES envelope</span><span class="sxs-lookup"><span data-stu-id="0f947-210">**cbc**: AES envelope encryption</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="0f947-211">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0f947-211">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="0f947-212">Skonfiguruj środowisko projektowe i wypełnij plik app.config przy użyciu informacji dotyczących połączenia, zgodnie z opisem w sekcji [Projektowanie usługi Media Services na platformie .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="0f947-212">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="0f947-213">Dodaj następujące elementy do węzła **appSettings** zdefiniowanego w pliku app.config:</span><span class="sxs-lookup"><span data-stu-id="0f947-213">Add the following elements to **appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="0f947-214">Przykład</span><span class="sxs-lookup"><span data-stu-id="0f947-214">Example</span></span>

<span data-ttu-id="0f947-215">W poniższym przykładzie pokazano możliwość używania usługi Media Services do dostarczania zawartości zaszyfrowane za pomocą FairPlay.</span><span class="sxs-lookup"><span data-stu-id="0f947-215">The following sample demonstrates the ability to use Media Services to deliver your content encrypted with FairPlay.</span></span> <span data-ttu-id="0f947-216">Ta funkcja została wprowadzona w Azure Media Services SDK dla platformy .NET w wersji 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="0f947-216">This functionality was introduced in the Azure Media Services SDK for .NET version 3.6.0.</span></span> 

<span data-ttu-id="0f947-217">Zastąp kod w pliku Program.cs kodem przedstawionym w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="0f947-217">Overwrite the code in your Program.cs file with the code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="0f947-218">Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="0f947-218">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="0f947-219">Należy używać tego samego identyfikatora zasad, jeśli zawsze są używane uprawnienia dotyczące tych samych dni lub tego samego dostępu, na przykład dla lokalizatorów przeznaczonych do długotrwałego stosowania (nieprzekazywanych zasad).</span><span class="sxs-lookup"><span data-stu-id="0f947-219">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="0f947-220">Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.</span><span class="sxs-lookup"><span data-stu-id="0f947-220">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="0f947-221">Upewnij się, że zaktualizowano zmienne, tak aby wskazywały foldery, w których znajdują się pliki danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="0f947-221">Make sure to update variables to point to folders where your input files are located.</span></span>

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
        // Read values from the App.config file.
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
            Console.WriteLine("Created key {0} for the asset {1} ", key.Id, encodedAsset.Id);
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

            // Generate a test token based on the the data in the given TokenRestrictionTemplate.
            // Note, you need to pass the key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during the creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("The authorization token is:\nBearer {0}", testToken);
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

            // Associate the key with the asset.
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

            // Associate the content key authorization policy with the content key.
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

            // Associate the content key authorization policy with the content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        private static string ConfigureFairPlayPolicyOptions()
        {
            // For testing you can provide all zeroes for ASK bytes together with the cert from Apple FPS SDK.
            // However, for production you must use a real ASK from Apple bound to a real prod certificate.
            byte[] askBytes = Guid.NewGuid().ToByteArray();
            var askId = Guid.NewGuid();
            // Key delivery retrieves askKey by askId and uses this key to generate the response.
            IContentKey askKey = _context.ContentKeys.Create(
                        askId,
                        askBytes,
                        "askKey",
                        ContentKeyType.FairPlayASk);

            //Customer password for creating the .pfx file.
            string pfxPassword = "<customer password for creating the .pfx file>";
            // Key delivery retrieves pfxPasswordKey by pfxPasswordId and uses this key to generate the response.
            var pfxPasswordId = Guid.NewGuid();
            byte[] pfxPasswordBytes = System.Text.Encoding.UTF8.GetBytes(pfxPassword);
            IContentKey pfxPasswordKey = _context.ContentKeys.Create(
                        pfxPasswordId,
                        pfxPasswordBytes,
                        "pfxPasswordKey",
                        ContentKeyType.FairPlayPfxPassword);

            // iv - 16 bytes random value, must match the iv in the asset delivery policy.
            byte[] iv = Guid.NewGuid().ToByteArray();

            //Specify the .pfx file created by the customer.
            var appCert = new X509Certificate2("path to the .pfx file created by the customer", pfxPassword, X509KeyStorageFlags.Exportable);

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

            // Get the FairPlay license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.FairPlay);

            // The reason the below code replaces "https://" with "skd://" is because
            // in the IOS player sample code which you obtained in Apple developer account,
            // the player only recognizes a Key URL that starts with skd://.
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

            // Add AssetDelivery Policy to the asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }


        /// <summary>
        /// Gets the streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference to the streaming manifest file from the  
            // collection of files in the asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator to the streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL to the manifest file.
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


## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="0f947-222">Następne kroki: ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="0f947-222">Next steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0f947-223">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="0f947-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
