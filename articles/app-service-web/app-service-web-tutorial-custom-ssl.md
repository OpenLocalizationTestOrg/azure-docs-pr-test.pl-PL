---
title: "aaaBind istniejących SSL niestandardowych certyfikatów aplikacji sieci Web tooAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się tootoobind niestandardowej aplikacji sieci web tooyour certyfikatu SSL, zaplecza aplikacji mobilnej lub aplikacji interfejsu API w usłudze Azure App Service."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a><span data-ttu-id="a972a-103">Powiąż istniejący niestandardowy SSL certyfikatu tooAzure aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="a972a-103">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>

<span data-ttu-id="a972a-104">Aplikacje sieci Web platformy Azure oferuje wysoce skalowalną, własnym poprawiania usługi hosta sieci web.</span><span class="sxs-lookup"><span data-stu-id="a972a-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="a972a-105">Ten samouczek pokazuje, jak toobind SSL niestandardowych certyfikatów, czemu zakupionego od zaufanego urzędu certyfikacji za[Azure Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a972a-105">This tutorial shows you how toobind a custom SSL certificate that you purchased from a trusted certificate authority too[Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="a972a-106">Po zakończeniu będziesz w stanie tooaccess aplikacji sieci web na punkt końcowy HTTPS hello DNS domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="a972a-106">When you're finished, you'll be able tooaccess your web app at hello HTTPS endpoint of your custom DNS domain.</span></span>

![Aplikacja sieci Web z niestandardowego certyfikatu SSL](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="a972a-108">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="a972a-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a972a-109">Uaktualnij warstwę cenową aplikacji</span><span class="sxs-lookup"><span data-stu-id="a972a-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="a972a-110">Powiąż z niestandardowych tooApp certyfikatu SSL usługi</span><span class="sxs-lookup"><span data-stu-id="a972a-110">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="a972a-111">Wymuszanie protokołu HTTPS dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="a972a-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="a972a-112">Powiązania certyfikatu SSL za pomocą skryptów automatyzacji</span><span class="sxs-lookup"><span data-stu-id="a972a-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="a972a-113">Tooget niestandardowego certyfikatu SSL, należy możesz pobrać go w portalu Azure hello bezpośrednio i powiązać ją tooyour aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a972a-113">If you need tooget a custom SSL certificate, you can get one in hello Azure portal directly and bind it tooyour web app.</span></span> <span data-ttu-id="a972a-114">Wykonaj hello [certyfikaty usługi aplikacji — samouczek](web-sites-purchase-ssl-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="a972a-114">Follow hello [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a972a-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a972a-115">Prerequisites</span></span>

<span data-ttu-id="a972a-116">toocomplete tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="a972a-116">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="a972a-117">Utwórz aplikację usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="a972a-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="a972a-118">Mapy niestandardowej aplikacji sieci web tooyour nazwy DNS</span><span class="sxs-lookup"><span data-stu-id="a972a-118">Map a custom DNS name tooyour web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="a972a-119">Uzyskanie certyfikatu SSL z zaufanego urzędu certyfikacji</span><span class="sxs-lookup"><span data-stu-id="a972a-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="a972a-120">Wymagania dotyczące certyfikatu SSL</span><span class="sxs-lookup"><span data-stu-id="a972a-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="a972a-121">toouse certyfikatów w usłudze App Service, hello certyfikatu musi spełniać wszystkie hello następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="a972a-121">toouse a certificate in App Service, hello certificate must meet all hello following requirements:</span></span>

* <span data-ttu-id="a972a-122">Podpisane przez zaufany urząd certyfikacji</span><span class="sxs-lookup"><span data-stu-id="a972a-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="a972a-123">Eksportowane jako chronionego hasłem pliku PFX</span><span class="sxs-lookup"><span data-stu-id="a972a-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="a972a-124">Zawiera klucz prywatny co najmniej 2048 bitów długo</span><span class="sxs-lookup"><span data-stu-id="a972a-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="a972a-125">Zawiera wszystkie certyfikaty pośrednie w łańcuchu certyfikatów hello</span><span class="sxs-lookup"><span data-stu-id="a972a-125">Contains all intermediate certificates in hello certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="a972a-126">**Certyfikaty krzywa Cryptography (ECC) eliptycznej** może współpracować z usługi aplikacji, ale nie są objęte w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="a972a-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="a972a-127">Współpraca z urzędu certyfikacji na powitania kolejnych kroków toocreate ECC certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="a972a-127">Work with your certificate authority on hello exact steps toocreate ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="a972a-128">Przygotowanie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="a972a-128">Prepare your web app</span></span>

<span data-ttu-id="a972a-129">toobind SSL niestandardowych certyfikatów tooyour aplikacji sieci web, z [planu usługi aplikacji](https://azure.microsoft.com/pricing/details/app-service/) musi być w hello **podstawowe**, **standardowe**, lub **Premium** warstwy.</span><span class="sxs-lookup"><span data-stu-id="a972a-129">toobind a custom SSL certificate tooyour web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in hello **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="a972a-130">W tym kroku możesz upewnij się, że aplikacja sieci web jest w hello obsługiwane warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="a972a-130">In this step, you make sure that your web app is in hello supported pricing tier.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="a972a-131">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="a972a-131">Log in tooAzure</span></span>

<span data-ttu-id="a972a-132">Otwórz hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a972a-132">Open hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-tooyour-web-app"></a><span data-ttu-id="a972a-133">Przejdź do aplikacji sieci web tooyour</span><span class="sxs-lookup"><span data-stu-id="a972a-133">Navigate tooyour web app</span></span>

<span data-ttu-id="a972a-134">W menu po lewej stronie powitania kliknij **usługi aplikacji**, a następnie kliknij nazwę hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a972a-134">From hello left menu, click **App Services**, and then click hello name of your web app.</span></span>

![Wybierz aplikację sieci web](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="a972a-136">Jest strony Zarządzanie hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a972a-136">You have landed in hello management page of your web app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="a972a-137">Sprawdź hello warstwy cenowej</span><span class="sxs-lookup"><span data-stu-id="a972a-137">Check hello pricing tier</span></span>

<span data-ttu-id="a972a-138">W nawigacji po lewej stronie powitania strony aplikacji sieci web, przewiń toohello **ustawienia** a następnie wybierz opcję **skalowanie w górę (plan usługi App Service)**.</span><span class="sxs-lookup"><span data-stu-id="a972a-138">In hello left-hand navigation of your web app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Skalowanie w pionie menu](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="a972a-140">Sprawdź toomake się, że aplikacja sieci web nie jest hello **wolne** lub **Shared** warstwy.</span><span class="sxs-lookup"><span data-stu-id="a972a-140">Check toomake sure that your web app is not in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="a972a-141">Warstwa bieżąca aplikacja sieci web jest wyróżniony ciemny niebieskie pole.</span><span class="sxs-lookup"><span data-stu-id="a972a-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![Sprawdź warstwę cenową](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="a972a-143">Niestandardowe SSL nie jest obsługiwany w hello **wolne** lub **Shared** warstwy.</span><span class="sxs-lookup"><span data-stu-id="a972a-143">Custom SSL is not supported in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="a972a-144">Jeśli potrzebujesz tooscale zapasowych, wykonaj kroki hello w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="a972a-144">If you need tooscale up, follow hello steps in hello next section.</span></span> <span data-ttu-id="a972a-145">W przeciwnym razie Zamknij hello **wybierz warstwę cenową** strony i pominąć zbyt[przekazywanie i powiązać certyfikatu SSL](#upload).</span><span class="sxs-lookup"><span data-stu-id="a972a-145">Otherwise, close hello **Choose your pricing tier** page and skip too[Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="a972a-146">Skalowanie w górę plan usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="a972a-146">Scale up your App Service plan</span></span>

<span data-ttu-id="a972a-147">Wybierz jedną z hello **podstawowe**, **standardowe**, lub **Premium** warstw.</span><span class="sxs-lookup"><span data-stu-id="a972a-147">Select one of hello **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="a972a-148">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="a972a-148">Click **Select**.</span></span>

![Wybierz warstwę cenową](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="a972a-150">Po wyświetleniu powiadomienia hello hello skali operacja została zakończona.</span><span class="sxs-lookup"><span data-stu-id="a972a-150">When you see hello following notification, hello scale operation is complete.</span></span>

![Skalowanie w górę powiadomień](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="a972a-152">Powiąż certyfikat protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="a972a-152">Bind your SSL certificate</span></span>

<span data-ttu-id="a972a-153">Możesz są gotowe tooupload aplikację sieci web uzyskiwania informacji na temat tooyour certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="a972a-153">You are ready tooupload your SSL certificate tooyour web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="a972a-154">Certyfikaty pośrednie scalenia</span><span class="sxs-lookup"><span data-stu-id="a972a-154">Merge intermediate certificates</span></span>

<span data-ttu-id="a972a-155">Urzędu certyfikacji zawiera wiele certyfikatów w łańcuchu certyfikatów hello, należy najpierw toomerge hello certyfikaty w kolejności.</span><span class="sxs-lookup"><span data-stu-id="a972a-155">If your certificate authority gives you multiple certificates in hello certificate chain, you need toomerge hello certificates in order.</span></span> 

<span data-ttu-id="a972a-156">toodo to open każdego certyfikatu otrzymane w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="a972a-156">toodo this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="a972a-157">Utwórz plik certyfikatu scalonych hello, nazywany _mergedcertificate.crt_.</span><span class="sxs-lookup"><span data-stu-id="a972a-157">Create a file for hello merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="a972a-158">W edytorze tekstów skopiuj zawartość hello każdy z certyfikatów do tego pliku.</span><span class="sxs-lookup"><span data-stu-id="a972a-158">In a text editor, copy hello content of each certificate into this file.</span></span> <span data-ttu-id="a972a-159">kolejność Hello certyfikaty powinna wyglądać hello następującego szablonu:</span><span class="sxs-lookup"><span data-stu-id="a972a-159">hello order of your certificates should look like hello following template:</span></span>

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-toopfx"></a><span data-ttu-id="a972a-160">Eksportuj certyfikat tooPFX</span><span class="sxs-lookup"><span data-stu-id="a972a-160">Export certificate tooPFX</span></span>

<span data-ttu-id="a972a-161">Eksportowanie scalonych certyfikatu SSL z kluczem prywatnym hello wygenerowania żądania certyfikatu z.</span><span class="sxs-lookup"><span data-stu-id="a972a-161">Export your merged SSL certificate with hello private key that your certificate request was generated with.</span></span>

<span data-ttu-id="a972a-162">Jeśli generowany jest żądanie certyfikatu przy użyciu biblioteki OpenSSL, został utworzony plik klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="a972a-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="a972a-163">tooexport Twojego tooPFX certyfikat, uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="a972a-163">tooexport your certificate tooPFX, run hello following command.</span></span> <span data-ttu-id="a972a-164">Zastąp symbole zastępcze hello  _&lt;plików kluczy prywatnych >_ i  _&lt;scalić — plik certyfikatu >_.</span><span class="sxs-lookup"><span data-stu-id="a972a-164">Replace hello placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="a972a-165">Po wyświetleniu monitu, należy określić hasło eksportu.</span><span class="sxs-lookup"><span data-stu-id="a972a-165">When prompted, define an export password.</span></span> <span data-ttu-id="a972a-166">To hasło będzie używany podczas przekazywania z protokołu SSL certyfikatu tooApp usługi później.</span><span class="sxs-lookup"><span data-stu-id="a972a-166">You'll use this password when uploading your SSL certificate tooApp Service later.</span></span>

<span data-ttu-id="a972a-167">Jeśli używasz usług IIS lub _Certreq.exe_ toogenerate Twojego żądania certyfikatu, zainstaluj hello certyfikatu tooyour komputera lokalnego, a następnie [wyeksportować hello certyfikatu tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="a972a-167">If you used IIS or _Certreq.exe_ toogenerate your certificate request, install hello certificate tooyour local machine, and then [export hello certificate tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="a972a-168">Przekaż certyfikat protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="a972a-168">Upload your SSL certificate</span></span>

<span data-ttu-id="a972a-169">tooupload certyfikatu SSL, kliknij przycisk **certyfikaty SSL** w hello lewy pasek nawigacyjny aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a972a-169">tooupload your SSL certificate, click **SSL certificates** in hello left navigation of your web app.</span></span>

<span data-ttu-id="a972a-170">Kliknij przycisk **Przekaż certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="a972a-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="a972a-171">W **plik certyfikatu PFX**, wybierz plik w formacie PFX.</span><span class="sxs-lookup"><span data-stu-id="a972a-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="a972a-172">W **hasło certyfikatu**, wpisz hasło hello, utworzonego podczas eksportowania pliku PFX hello.</span><span class="sxs-lookup"><span data-stu-id="a972a-172">In **Certificate password**, type hello password that you created when you exported hello PFX file.</span></span>

<span data-ttu-id="a972a-173">Kliknij pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="a972a-173">Click **Upload**.</span></span>

![Przekazywanie certyfikatu](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="a972a-175">Po zakończeniu przekazywania certyfikatu usługi aplikacji był w hello **certyfikaty SSL** strony.</span><span class="sxs-lookup"><span data-stu-id="a972a-175">When App Service finishes uploading your certificate, it appears in hello **SSL certificates** page.</span></span>

![Przekazany certyfikat](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="a972a-177">Powiąż certyfikat protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="a972a-177">Bind your SSL certificate</span></span>

<span data-ttu-id="a972a-178">W hello **powiązania SSL** kliknij **dodać powiązanie**.</span><span class="sxs-lookup"><span data-stu-id="a972a-178">In hello **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="a972a-179">W hello **Dodaj powiązanie SSL** Użyj hello listę rozwijaną tooselect hello domeny nazwa toosecure i hello toouse certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="a972a-179">In hello **Add SSL Binding** page, use hello dropdowns tooselect hello domain name toosecure, and hello certificate toouse.</span></span>

> [!NOTE]
> <span data-ttu-id="a972a-180">Jeśli zostały przekazane certyfikat, ale nie ma nazwy domeny hello w hello **Hostname** listy rozwijanej, spróbuj odświeżyć stronę przeglądarki hello.</span><span class="sxs-lookup"><span data-stu-id="a972a-180">If you have uploaded your certificate but don't see hello domain name(s) in hello **Hostname** dropdown, try refreshing hello browser page.</span></span>
>
>

<span data-ttu-id="a972a-181">W **typu SSL**, wybierz pozycję czy toouse  **[oznaczenia nazwy serwera (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  lub opartych na protokole SSL.</span><span class="sxs-lookup"><span data-stu-id="a972a-181">In **SSL Type**, select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="a972a-182">**SSL opartego na protokole SNI** -powiązania SSL opartego na wiele SNI mogą zostać dodane.</span><span class="sxs-lookup"><span data-stu-id="a972a-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="a972a-183">Ta opcja umożliwia wielu toosecure certyfikaty SSL wielu domen na powitania tego samego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="a972a-183">This option allows multiple SSL certificates toosecure multiple domains on hello same IP address.</span></span> <span data-ttu-id="a972a-184">Większość nowoczesnych przeglądarek (w tym programu Internet Explorer, Chrome, Firefox i Opera) obsługuje SNI (znaleźć bardziej szczegółowe informacje pomocy technicznej przeglądarki na [wskaźnika nazwy serwera](http://wikipedia.org/wiki/Server_Name_Indication)).</span><span class="sxs-lookup"><span data-stu-id="a972a-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="a972a-185">**Oparte na protokole SSL** — mogą być dodawane tylko jednego powiązania SSL opartego na protokole IP.</span><span class="sxs-lookup"><span data-stu-id="a972a-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="a972a-186">Ta opcja umożliwia tylko jeden toosecure certyfikatu SSL dedykowanych publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="a972a-186">This option allows only one SSL certificate toosecure a dedicated public IP address.</span></span> <span data-ttu-id="a972a-187">toosecure wiele domen, należy zabezpieczyć je przy użyciu wszystkich hello tego samego certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="a972a-187">toosecure multiple domains, you must secure them all using hello same SSL certificate.</span></span> <span data-ttu-id="a972a-188">To jest opcją tradycyjnych hello powiązania SSL.</span><span class="sxs-lookup"><span data-stu-id="a972a-188">This is hello traditional option for SSL binding.</span></span>

<span data-ttu-id="a972a-189">Kliknij przycisk **dodać powiązanie**.</span><span class="sxs-lookup"><span data-stu-id="a972a-189">Click **Add Binding**.</span></span>

![Powiąż certyfikat protokołu SSL](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="a972a-191">Po zakończeniu przekazywania certyfikatu usługi aplikacji był w hello **powiązania SSL** sekcje.</span><span class="sxs-lookup"><span data-stu-id="a972a-191">When App Service finishes uploading your certificate, it appears in hello **SSL bindings** sections.</span></span>

![Certyfikat powiązany tooweb aplikacji](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="a972a-193">Ponowne mapowanie rekord dla protokołu SSL z adresu IP</span><span class="sxs-lookup"><span data-stu-id="a972a-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="a972a-194">Jeśli nie używasz w aplikacji sieci web opartych na protokole SSL, Pomiń zbyt[HTTPS testu dla domeny niestandardowej](#test).</span><span class="sxs-lookup"><span data-stu-id="a972a-194">If you don't use IP-based SSL in your web app, skip too[Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="a972a-195">Domyślnie aplikacja sieci web używa udostępnionego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="a972a-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="a972a-196">Gdy Powiąż certyfikat z SSL opartego na protokole IP, usługi aplikacji — tworzy nowy, dedykowany adres IP dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a972a-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="a972a-197">Jeśli zamapowaniu aplikacji sieci web tooyour rekordów A, zaktualizować rejestr domeny ten nowy, dedykowany adres IP.</span><span class="sxs-lookup"><span data-stu-id="a972a-197">If you have mapped an A record tooyour web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="a972a-198">Aplikacja sieci web **domeny niestandardowe** strona zostanie zaktualizowana przy hello nowy, dedykowany adres IP.</span><span class="sxs-lookup"><span data-stu-id="a972a-198">Your web app's **Custom domain** page is updated with hello new, dedicated IP address.</span></span> <span data-ttu-id="a972a-199">[Skopiuj ten adres IP](app-service-web-tutorial-custom-domain.md#info), następnie [ponownego mapowania hello rekord](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis nowego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="a972a-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap hello A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="a972a-200">Test protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="a972a-200">Test HTTPS</span></span>

<span data-ttu-id="a972a-201">Teraz opuścił toodo jest toomake się upewnić, że HTTPS działa dla domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="a972a-201">All that's left toodo now is toomake sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="a972a-202">W różnych przeglądarkach, Przeglądaj zbyt`https://<your.custom.domain>` toosee pełniącą zapasowej swojej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a972a-202">In various browsers, browse too`https://<your.custom.domain>` toosee that it serves up your web app.</span></span>

![Aplikacja tooAzure nawigacji w portalu](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="a972a-204">Jeśli aplikacja sieci web udostępnia certyfikatu błędy sprawdzania poprawności, prawdopodobnie używasz certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="a972a-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="a972a-205">Jeśli nie jest to przypadek hello, mogą być przechowywane poza certyfikaty pośrednie podczas eksportowania pliku PFX toohello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="a972a-205">If that's not hello case, you may have left out intermediate certificates when you export your certificate toohello PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="a972a-206">Wymuszanie protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="a972a-206">Enforce HTTPS</span></span>

<span data-ttu-id="a972a-207">Usługa aplikacji ma *nie* Wymuszanie protokołu HTTPS, więc każdy może nadal uzyskiwać dostęp do aplikacji sieci web przy użyciu protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="a972a-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="a972a-208">tooenforce HTTPS dla aplikacji sieci web, zdefiniuj reguły ponownego zapisywania w hello _web.config_ plików dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a972a-208">tooenforce HTTPS for your web app, define a rewrite rule in hello _web.config_ file for your web app.</span></span> <span data-ttu-id="a972a-209">Ten plik, niezależnie od hello strukturę języka aplikacji sieci web korzysta z usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a972a-209">App Service uses this file, regardless of hello language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="a972a-210">Jest specyficzny dla języka Przekierowywanie żądań.</span><span class="sxs-lookup"><span data-stu-id="a972a-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="a972a-211">ASP.NET MVC można użyć hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtru zamiast reguły ponownego zapisywania hello w _web.config_.</span><span class="sxs-lookup"><span data-stu-id="a972a-211">ASP.NET MVC can use hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of hello rewrite rule in _web.config_.</span></span>

<span data-ttu-id="a972a-212">Jeśli jesteś deweloperem .NET stosunkowo zapoznaj się z tym plikiem.</span><span class="sxs-lookup"><span data-stu-id="a972a-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="a972a-213">Znajduje się w głównym hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="a972a-213">It is in hello root of your solution.</span></span>

<span data-ttu-id="a972a-214">Można również w przypadku tworzenia z PHP, Node.js, Python lub Java, jest stosowany ten plik w Twoim imieniu możemy generowane w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="a972a-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="a972a-215">Łączenie aplikacji sieci web tooyour końcowego FTP wykonując instrukcje hello [wdrażanie tooAzure Twojej aplikacji App Service przy użyciu FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="a972a-215">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="a972a-216">Ten plik powinien znajdować się w _/home/site/wwwroot_.</span><span class="sxs-lookup"><span data-stu-id="a972a-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="a972a-217">Jeśli nie, należy utworzyć _web.config_ plik w tym folderze z powitania po XML:</span><span class="sxs-lookup"><span data-stu-id="a972a-217">If not, create a _web.config_ file in this folder with hello following XML:</span></span>

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

<span data-ttu-id="a972a-218">Dla istniejącej _web.config_ plików, skopiować cały hello `<rule>` element do Twojej _web.config_w `configuration/system.webServer/rewrite/rules` elementu.</span><span class="sxs-lookup"><span data-stu-id="a972a-218">For an existing _web.config_ file, copy hello entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="a972a-219">Jeśli istnieją inne `<rule>` elementów w Twojej _web.config_, hello miejsce skopiowane `<rule>` element przed hello innych `<rule>` elementów.</span><span class="sxs-lookup"><span data-stu-id="a972a-219">If there are other `<rule>` elements in your _web.config_, place hello copied `<rule>` element before hello other `<rule>` elements.</span></span>

<span data-ttu-id="a972a-220">Ta reguła zwraca protokół HTTP 301 (Stałe przekierowanie) toohello HTTPS zawsze, gdy użytkownik hello sprawia, że aplikacja sieci web tooyour żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="a972a-220">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="a972a-221">Na przykład przekierowuje z `http://contoso.com` zbyt`https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="a972a-221">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

<span data-ttu-id="a972a-222">Aby uzyskać więcej informacji na powitania moduł ponowne zapisywanie adresów URL usług IIS, zobacz hello [ponowne zapisywanie adresów URL](http://www.iis.net/downloads/microsoft/url-rewrite) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="a972a-222">For more information on hello IIS URL Rewrite module, see hello [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="a972a-223">Wymuszanie protokołu HTTPS dla aplikacji sieci Web w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="a972a-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="a972a-224">Usługa aplikacji w systemie Linux ma *nie* Wymuszanie protokołu HTTPS, więc każdy może nadal uzyskiwać dostęp do aplikacji sieci web przy użyciu protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="a972a-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="a972a-225">tooenforce HTTPS dla aplikacji sieci web, zdefiniuj reguły ponownego zapisywania w hello _.htaccess_ plików dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="a972a-225">tooenforce HTTPS for your web app, define a rewrite rule in hello _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="a972a-226">Łączenie aplikacji sieci web tooyour końcowego FTP wykonując instrukcje hello [wdrażanie tooAzure Twojej aplikacji App Service przy użyciu FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="a972a-226">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="a972a-227">W _/home/site/wwwroot_, Utwórz _.htaccess_ pliku z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="a972a-227">In _/home/site/wwwroot_, create an _.htaccess_ file with hello following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="a972a-228">Ta reguła zwraca protokół HTTP 301 (Stałe przekierowanie) toohello HTTPS zawsze, gdy użytkownik hello sprawia, że aplikacja sieci web tooyour żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="a972a-228">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="a972a-229">Na przykład przekierowuje z `http://contoso.com` zbyt`https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="a972a-229">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="a972a-230">Zautomatyzować za pomocą skryptów</span><span class="sxs-lookup"><span data-stu-id="a972a-230">Automate with scripts</span></span>

<span data-ttu-id="a972a-231">Można zautomatyzować powiązań SSL dla aplikacji sieci web za pomocą skryptów przy użyciu hello [interfejsu wiersza polecenia Azure](/cli/azure/install-azure-cli) lub [programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a972a-231">You can automate SSL bindings for your web app with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="a972a-232">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a972a-232">Azure CLI</span></span>

<span data-ttu-id="a972a-233">Witaj następujące polecenia przekazuje wyeksportowanego pliku PFX i pobiera hello odcisk palca.</span><span class="sxs-lookup"><span data-stu-id="a972a-233">hello following command uploads an exported PFX file and gets hello thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="a972a-234">Witaj następujące polecenie dodaje powiązania SSL opartego na protokole SNI, za pomocą odcisku palca hello z hello poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="a972a-234">hello following command adds an SNI-based SSL binding, using hello thumbprint from hello previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="a972a-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a972a-235">Azure PowerShell</span></span>

<span data-ttu-id="a972a-236">Witaj następujące polecenie przekazuje wyeksportowanego pliku PFX i dodaje powiązania SSL opartego na SNI.</span><span class="sxs-lookup"><span data-stu-id="a972a-236">hello following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="a972a-237">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a972a-237">Next steps</span></span>

<span data-ttu-id="a972a-238">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="a972a-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a972a-239">Uaktualnij warstwę cenową aplikacji</span><span class="sxs-lookup"><span data-stu-id="a972a-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="a972a-240">Powiąż z niestandardowych tooApp certyfikatu SSL usługi</span><span class="sxs-lookup"><span data-stu-id="a972a-240">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="a972a-241">Wymuszanie protokołu HTTPS dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="a972a-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="a972a-242">Powiązania certyfikatu SSL za pomocą skryptów automatyzacji</span><span class="sxs-lookup"><span data-stu-id="a972a-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="a972a-243">Jak przejść dalej toolearn samouczka toohello toouse Azure Content Delivery Network.</span><span class="sxs-lookup"><span data-stu-id="a972a-243">Advance toohello next tutorial toolearn how toouse Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a972a-244">Dodaj tooan sieci dostarczania zawartości (CDN) usługi Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a972a-244">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
