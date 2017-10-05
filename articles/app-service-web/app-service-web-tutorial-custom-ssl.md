---
title: "Powiąż istniejący certyfikat SSL niestandardowych do aplikacji sieci Web platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się powiązać niestandardowego certyfikatu SSL do aplikacji sieci web, zaplecza aplikacji mobilnej lub aplikacji interfejsu API w usłudze Azure App Service."
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
ms.openlocfilehash: 15c31ae5451a31dff2df08047ee43e75edacc127
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-to-azure-web-apps"></a><span data-ttu-id="b51f4-103">Powiąż istniejący certyfikat SSL niestandardowych do aplikacji sieci Web Azure</span><span class="sxs-lookup"><span data-stu-id="b51f4-103">Bind an existing custom SSL certificate to Azure Web Apps</span></span>

<span data-ttu-id="b51f4-104">Aplikacje sieci Web platformy Azure oferuje wysoce skalowalną, własnym poprawiania usługi hosta sieci web.</span><span class="sxs-lookup"><span data-stu-id="b51f4-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="b51f4-105">Ten samouczek pokazuje, jak można powiązać certyfikat SSL niestandardowych zakupionego od zaufanego urzędu certyfikacji do [Azure Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b51f4-105">This tutorial shows you how to bind a custom SSL certificate that you purchased from a trusted certificate authority to [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="b51f4-106">Po zakończeniu, będzie można uzyskać dostępu do aplikacji sieci web w punkcie końcowym HTTPS z niestandardowej domeny DNS.</span><span class="sxs-lookup"><span data-stu-id="b51f4-106">When you're finished, you'll be able to access your web app at the HTTPS endpoint of your custom DNS domain.</span></span>

![Aplikacja sieci Web z niestandardowego certyfikatu SSL](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="b51f4-108">Ten samouczek zawiera informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="b51f4-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b51f4-109">Uaktualnij warstwę cenową aplikacji</span><span class="sxs-lookup"><span data-stu-id="b51f4-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="b51f4-110">Powiązać niestandardowego certyfikatu SSL z usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b51f4-110">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="b51f4-111">Wymuszanie protokołu HTTPS dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="b51f4-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="b51f4-112">Powiązania certyfikatu SSL za pomocą skryptów automatyzacji</span><span class="sxs-lookup"><span data-stu-id="b51f4-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="b51f4-113">Jeśli potrzebujesz niestandardowego certyfikatu SSL, możesz pobrać go w portalu Azure bezpośrednio i powiązać go z aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b51f4-113">If you need to get a custom SSL certificate, you can get one in the Azure portal directly and bind it to your web app.</span></span> <span data-ttu-id="b51f4-114">Postępuj zgodnie z [certyfikaty usługi aplikacji — samouczek](web-sites-purchase-ssl-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="b51f4-114">Follow the [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b51f4-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b51f4-115">Prerequisites</span></span>

<span data-ttu-id="b51f4-116">W celu ukończenia tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="b51f4-116">To complete this tutorial:</span></span>

- [<span data-ttu-id="b51f4-117">Utwórz aplikację usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b51f4-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="b51f4-118">Mapowanie niestandardową nazwę DNS do aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="b51f4-118">Map a custom DNS name to your web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="b51f4-119">Uzyskanie certyfikatu SSL z zaufanego urzędu certyfikacji</span><span class="sxs-lookup"><span data-stu-id="b51f4-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="b51f4-120">Wymagania dotyczące certyfikatu SSL</span><span class="sxs-lookup"><span data-stu-id="b51f4-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="b51f4-121">Aby użyć certyfikatu w usłudze App Service, certyfikat musi spełniać następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="b51f4-121">To use a certificate in App Service, the certificate must meet all the following requirements:</span></span>

* <span data-ttu-id="b51f4-122">Podpisane przez zaufany urząd certyfikacji</span><span class="sxs-lookup"><span data-stu-id="b51f4-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="b51f4-123">Eksportowane jako chronionego hasłem pliku PFX</span><span class="sxs-lookup"><span data-stu-id="b51f4-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="b51f4-124">Zawiera klucz prywatny co najmniej 2048 bitów długo</span><span class="sxs-lookup"><span data-stu-id="b51f4-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="b51f4-125">Zawiera wszystkie certyfikaty pośrednie w łańcuchu certyfikatów</span><span class="sxs-lookup"><span data-stu-id="b51f4-125">Contains all intermediate certificates in the certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="b51f4-126">**Certyfikaty krzywa Cryptography (ECC) eliptycznej** może współpracować z usługi aplikacji, ale nie są objęte w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="b51f4-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="b51f4-127">Współpraca z urzędu certyfikacji na kolejnych kroków w celu utworzenia certyfikatów ECC.</span><span class="sxs-lookup"><span data-stu-id="b51f4-127">Work with your certificate authority on the exact steps to create ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="b51f4-128">Przygotowanie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="b51f4-128">Prepare your web app</span></span>

<span data-ttu-id="b51f4-129">Do powiązania niestandardowego certyfikatu SSL do aplikacji sieci web z [planu usługi aplikacji](https://azure.microsoft.com/pricing/details/app-service/) musi znajdować się w **podstawowe**, **standardowe**, lub **Premium** warstwy.</span><span class="sxs-lookup"><span data-stu-id="b51f4-129">To bind a custom SSL certificate to your web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in the **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="b51f4-130">W tym kroku należy upewnić się, że aplikacja sieci web jest w obsługiwanym warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="b51f4-130">In this step, you make sure that your web app is in the supported pricing tier.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="b51f4-131">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b51f4-131">Log in to Azure</span></span>

<span data-ttu-id="b51f4-132">Otwórz [portal Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b51f4-132">Open the [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-to-your-web-app"></a><span data-ttu-id="b51f4-133">Przejdź do aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="b51f4-133">Navigate to your web app</span></span>

<span data-ttu-id="b51f4-134">Z menu po lewej stronie kliknij **usługi aplikacji**, a następnie kliknij nazwę aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b51f4-134">From the left menu, click **App Services**, and then click the name of your web app.</span></span>

![Wybierz aplikację sieci web](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="b51f4-136">Jest na stronie Zarządzanie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b51f4-136">You have landed in the management page of your web app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="b51f4-137">Sprawdź warstwę cenową</span><span class="sxs-lookup"><span data-stu-id="b51f4-137">Check the pricing tier</span></span>

<span data-ttu-id="b51f4-138">W obszarze nawigacji po lewej stronie strony aplikacji sieci web, przewiń do **ustawienia** a następnie wybierz opcję **skalowanie w górę (plan usługi App Service)**.</span><span class="sxs-lookup"><span data-stu-id="b51f4-138">In the left-hand navigation of your web app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Skalowanie w pionie menu](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="b51f4-140">Upewnij się, że aplikacja sieci web nie znajduje się w **wolne** lub **Shared** warstwy.</span><span class="sxs-lookup"><span data-stu-id="b51f4-140">Check to make sure that your web app is not in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="b51f4-141">Warstwa bieżąca aplikacja sieci web jest wyróżniony ciemny niebieskie pole.</span><span class="sxs-lookup"><span data-stu-id="b51f4-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![Sprawdź warstwę cenową](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="b51f4-143">Niestandardowe SSL nie jest obsługiwany w **wolne** lub **Shared** warstwy.</span><span class="sxs-lookup"><span data-stu-id="b51f4-143">Custom SSL is not supported in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="b51f4-144">Jeśli potrzebujesz skalowanie w górę, wykonaj kroki opisane w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="b51f4-144">If you need to scale up, follow the steps in the next section.</span></span> <span data-ttu-id="b51f4-145">W przeciwnym razie Zamknij **wybierz warstwę cenową** strony i przejść [przekazywanie i powiązać certyfikatu SSL](#upload).</span><span class="sxs-lookup"><span data-stu-id="b51f4-145">Otherwise, close the **Choose your pricing tier** page and skip to [Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="b51f4-146">Skalowanie w górę plan usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b51f4-146">Scale up your App Service plan</span></span>

<span data-ttu-id="b51f4-147">Wybierz jedną z **podstawowe**, **standardowe**, lub **Premium** warstw.</span><span class="sxs-lookup"><span data-stu-id="b51f4-147">Select one of the **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="b51f4-148">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="b51f4-148">Click **Select**.</span></span>

![Wybierz warstwę cenową](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="b51f4-150">Gdy zostanie wyświetlone następujące powiadomienie, zakończeniu operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="b51f4-150">When you see the following notification, the scale operation is complete.</span></span>

![Skalowanie w górę powiadomień](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="b51f4-152">Powiąż certyfikat protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="b51f4-152">Bind your SSL certificate</span></span>

<span data-ttu-id="b51f4-153">Wszystko jest gotowe do przekazania certyfikatu SSL do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b51f4-153">You are ready to upload your SSL certificate to your web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="b51f4-154">Certyfikaty pośrednie scalenia</span><span class="sxs-lookup"><span data-stu-id="b51f4-154">Merge intermediate certificates</span></span>

<span data-ttu-id="b51f4-155">Urzędu certyfikacji zawiera wiele certyfikatów w łańcuchu certyfikatów, należy scalić certyfikaty w kolejności.</span><span class="sxs-lookup"><span data-stu-id="b51f4-155">If your certificate authority gives you multiple certificates in the certificate chain, you need to merge the certificates in order.</span></span> 

<span data-ttu-id="b51f4-156">Aby to zrobić, Otwórz każdy z certyfikatów, zostanie wyświetlony w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="b51f4-156">To do this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="b51f4-157">Utwórz plik certyfikatu scalone, nazywany _mergedcertificate.crt_.</span><span class="sxs-lookup"><span data-stu-id="b51f4-157">Create a file for the merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="b51f4-158">W edytorze tekstów skopiuj zawartość każdy z certyfikatów do tego pliku.</span><span class="sxs-lookup"><span data-stu-id="b51f4-158">In a text editor, copy the content of each certificate into this file.</span></span> <span data-ttu-id="b51f4-159">Kolejność certyfikaty powinna wyglądać następującego szablonu:</span><span class="sxs-lookup"><span data-stu-id="b51f4-159">The order of your certificates should look like the following template:</span></span>

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

### <a name="export-certificate-to-pfx"></a><span data-ttu-id="b51f4-160">Wyeksportuj certyfikat PFX</span><span class="sxs-lookup"><span data-stu-id="b51f4-160">Export certificate to PFX</span></span>

<span data-ttu-id="b51f4-161">Eksportowanie scalonych certyfikatu SSL z kluczem prywatnym, który żądania certyfikatu został wygenerowany z.</span><span class="sxs-lookup"><span data-stu-id="b51f4-161">Export your merged SSL certificate with the private key that your certificate request was generated with.</span></span>

<span data-ttu-id="b51f4-162">Jeśli generowany jest żądanie certyfikatu przy użyciu biblioteki OpenSSL, został utworzony plik klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="b51f4-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="b51f4-163">Aby wyeksportować certyfikat do PFX, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="b51f4-163">To export your certificate to PFX, run the following command.</span></span> <span data-ttu-id="b51f4-164">Zastąp symbole zastępcze  _&lt;plików kluczy prywatnych >_ i  _&lt;scalić — plik certyfikatu >_.</span><span class="sxs-lookup"><span data-stu-id="b51f4-164">Replace the placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="b51f4-165">Po wyświetleniu monitu, należy określić hasło eksportu.</span><span class="sxs-lookup"><span data-stu-id="b51f4-165">When prompted, define an export password.</span></span> <span data-ttu-id="b51f4-166">To hasło będzie używany podczas przekazywania certyfikatu SSL w usłudze App Service później.</span><span class="sxs-lookup"><span data-stu-id="b51f4-166">You'll use this password when uploading your SSL certificate to App Service later.</span></span>

<span data-ttu-id="b51f4-167">Jeśli używasz usług IIS lub _Certreq.exe_ do wygenerowania żądania certyfikatu, zainstalować certyfikat na komputerze lokalnym, a następnie [wyeksportuj certyfikat PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="b51f4-167">If you used IIS or _Certreq.exe_ to generate your certificate request, install the certificate to your local machine, and then [export the certificate to PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="b51f4-168">Przekaż certyfikat protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="b51f4-168">Upload your SSL certificate</span></span>

<span data-ttu-id="b51f4-169">Aby przekazać certyfikat SSL, kliknij przycisk **certyfikaty SSL** na lewym pasku nawigacyjnym aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b51f4-169">To upload your SSL certificate, click **SSL certificates** in the left navigation of your web app.</span></span>

<span data-ttu-id="b51f4-170">Kliknij przycisk **Przekaż certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="b51f4-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="b51f4-171">W **plik certyfikatu PFX**, wybierz plik w formacie PFX.</span><span class="sxs-lookup"><span data-stu-id="b51f4-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="b51f4-172">W **hasło certyfikatu**, wpisz hasło, które utworzono podczas eksportowania pliku PFX.</span><span class="sxs-lookup"><span data-stu-id="b51f4-172">In **Certificate password**, type the password that you created when you exported the PFX file.</span></span>

<span data-ttu-id="b51f4-173">Kliknij pozycję **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="b51f4-173">Click **Upload**.</span></span>

![Przekazywanie certyfikatu](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="b51f4-175">Po zakończeniu przekazywania certyfikatu usługi aplikacji był w **certyfikaty SSL** strony.</span><span class="sxs-lookup"><span data-stu-id="b51f4-175">When App Service finishes uploading your certificate, it appears in the **SSL certificates** page.</span></span>

![Przekazany certyfikat](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="b51f4-177">Powiąż certyfikat protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="b51f4-177">Bind your SSL certificate</span></span>

<span data-ttu-id="b51f4-178">W **powiązania SSL** kliknij **dodać powiązanie**.</span><span class="sxs-lookup"><span data-stu-id="b51f4-178">In the **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="b51f4-179">W **Dodaj powiązanie SSL** Użyj listę rozwijaną, aby wybrać nazwę domeny do zabezpieczania i certyfikat do użycia.</span><span class="sxs-lookup"><span data-stu-id="b51f4-179">In the **Add SSL Binding** page, use the dropdowns to select the domain name to secure, and the certificate to use.</span></span>

> [!NOTE]
> <span data-ttu-id="b51f4-180">Jeśli zostały przekazane certyfikat, ale nie ma nazwy domeny w **Hostname** listy rozwijanej, spróbuj odświeżyć stronę przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="b51f4-180">If you have uploaded your certificate but don't see the domain name(s) in the **Hostname** dropdown, try refreshing the browser page.</span></span>
>
>

<span data-ttu-id="b51f4-181">W **typu SSL**, wybierz, czy ma być używany  **[oznaczenia nazwy serwera (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  lub opartych na protokole SSL.</span><span class="sxs-lookup"><span data-stu-id="b51f4-181">In **SSL Type**, select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="b51f4-182">**SSL opartego na protokole SNI** -powiązania SSL opartego na wiele SNI mogą zostać dodane.</span><span class="sxs-lookup"><span data-stu-id="b51f4-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="b51f4-183">Ta opcja umożliwia wielu certyfikatów protokołu SSL do zabezpieczania wielu domen na ten sam adres IP.</span><span class="sxs-lookup"><span data-stu-id="b51f4-183">This option allows multiple SSL certificates to secure multiple domains on the same IP address.</span></span> <span data-ttu-id="b51f4-184">Większość nowoczesnych przeglądarek (w tym programu Internet Explorer, Chrome, Firefox i Opera) obsługuje SNI (znaleźć bardziej szczegółowe informacje pomocy technicznej przeglądarki na [wskaźnika nazwy serwera](http://wikipedia.org/wiki/Server_Name_Indication)).</span><span class="sxs-lookup"><span data-stu-id="b51f4-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="b51f4-185">**Oparte na protokole SSL** — mogą być dodawane tylko jednego powiązania SSL opartego na protokole IP.</span><span class="sxs-lookup"><span data-stu-id="b51f4-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="b51f4-186">Ta opcja umożliwia tylko jeden certyfikat SSL do zabezpieczania dedykowanych publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="b51f4-186">This option allows only one SSL certificate to secure a dedicated public IP address.</span></span> <span data-ttu-id="b51f4-187">Aby zabezpieczyć wielu domen, należy zabezpieczyć je wszystkie przy użyciu tego samego certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="b51f4-187">To secure multiple domains, you must secure them all using the same SSL certificate.</span></span> <span data-ttu-id="b51f4-188">Jest to tradycyjne opcja dla powiązania SSL.</span><span class="sxs-lookup"><span data-stu-id="b51f4-188">This is the traditional option for SSL binding.</span></span>

<span data-ttu-id="b51f4-189">Kliknij przycisk **dodać powiązanie**.</span><span class="sxs-lookup"><span data-stu-id="b51f4-189">Click **Add Binding**.</span></span>

![Powiąż certyfikat protokołu SSL](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="b51f4-191">Po zakończeniu przekazywania certyfikatu usługi aplikacji był w **powiązania SSL** sekcje.</span><span class="sxs-lookup"><span data-stu-id="b51f4-191">When App Service finishes uploading your certificate, it appears in the **SSL bindings** sections.</span></span>

![Certyfikat powiązany z aplikacji sieci web](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="b51f4-193">Ponowne mapowanie rekord dla protokołu SSL z adresu IP</span><span class="sxs-lookup"><span data-stu-id="b51f4-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="b51f4-194">Jeśli nie używasz opartych na protokole SSL w aplikacji sieci web, przejdź do [HTTPS testu dla domeny niestandardowej](#test).</span><span class="sxs-lookup"><span data-stu-id="b51f4-194">If you don't use IP-based SSL in your web app, skip to [Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="b51f4-195">Domyślnie aplikacja sieci web używa udostępnionego publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="b51f4-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="b51f4-196">Gdy Powiąż certyfikat z SSL opartego na protokole IP, usługi aplikacji — tworzy nowy, dedykowany adres IP dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b51f4-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="b51f4-197">Jeśli rekord A zamapowaniu do aplikacji sieci web, należy zaktualizować rejestru domeny ten nowy, dedykowany adres IP.</span><span class="sxs-lookup"><span data-stu-id="b51f4-197">If you have mapped an A record to your web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="b51f4-198">Aplikacja sieci web **domeny niestandardowe** strona zostanie zaktualizowana nowy, dedykowany adres IP.</span><span class="sxs-lookup"><span data-stu-id="b51f4-198">Your web app's **Custom domain** page is updated with the new, dedicated IP address.</span></span> <span data-ttu-id="b51f4-199">[Skopiuj ten adres IP](app-service-web-tutorial-custom-domain.md#info), następnie [ponownie zamapować rekord A](app-service-web-tutorial-custom-domain.md#map-an-a-record) ten nowy adres IP.</span><span class="sxs-lookup"><span data-stu-id="b51f4-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap the A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) to this new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="b51f4-200">Test protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="b51f4-200">Test HTTPS</span></span>

<span data-ttu-id="b51f4-201">Teraz pozostało celu jest aby upewnić się, że HTTPS działa dla domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="b51f4-201">All that's left to do now is to make sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="b51f4-202">W różnych przeglądarkach, przejdź do `https://<your.custom.domain>` aby zobaczyć, służy ona zapasowej swojej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b51f4-202">In various browsers, browse to `https://<your.custom.domain>` to see that it serves up your web app.</span></span>

![Nawigacji w portalu do aplikacji Azure](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="b51f4-204">Jeśli aplikacja sieci web udostępnia certyfikatu błędy sprawdzania poprawności, prawdopodobnie używasz certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="b51f4-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="b51f4-205">Jeśli nie jest wielkość liter, mogą być przechowywane poza certyfikaty pośrednie podczas eksportowania certyfikatu do pliku PFX.</span><span class="sxs-lookup"><span data-stu-id="b51f4-205">If that's not the case, you may have left out intermediate certificates when you export your certificate to the PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="b51f4-206">Wymuszanie protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="b51f4-206">Enforce HTTPS</span></span>

<span data-ttu-id="b51f4-207">Usługa aplikacji ma *nie* Wymuszanie protokołu HTTPS, więc każdy może nadal uzyskiwać dostęp do aplikacji sieci web przy użyciu protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="b51f4-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="b51f4-208">Aby wymusić HTTPS dla aplikacji sieci web, należy zdefiniować reguły ponownego zapisywania w _web.config_ plików dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b51f4-208">To enforce HTTPS for your web app, define a rewrite rule in the _web.config_ file for your web app.</span></span> <span data-ttu-id="b51f4-209">Ten plik, niezależnie od struktury języka aplikacji sieci web korzysta z usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b51f4-209">App Service uses this file, regardless of the language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="b51f4-210">Jest specyficzny dla języka Przekierowywanie żądań.</span><span class="sxs-lookup"><span data-stu-id="b51f4-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="b51f4-211">ASP.NET MVC można użyć [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtru zamiast reguły ponownego zapisywania _web.config_.</span><span class="sxs-lookup"><span data-stu-id="b51f4-211">ASP.NET MVC can use the [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of the rewrite rule in _web.config_.</span></span>

<span data-ttu-id="b51f4-212">Jeśli jesteś deweloperem .NET stosunkowo zapoznaj się z tym plikiem.</span><span class="sxs-lookup"><span data-stu-id="b51f4-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="b51f4-213">Znajduje się w katalogu głównym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="b51f4-213">It is in the root of your solution.</span></span>

<span data-ttu-id="b51f4-214">Można również w przypadku tworzenia z PHP, Node.js, Python lub Java, jest stosowany ten plik w Twoim imieniu możemy generowane w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="b51f4-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="b51f4-215">Połącz do punktu końcowego FTP aplikacji sieci web zgodnie z instrukcjami w [wdrażanie aplikacji w usłudze Azure App Service przy użyciu FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="b51f4-215">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="b51f4-216">Ten plik powinien znajdować się w _/home/site/wwwroot_.</span><span class="sxs-lookup"><span data-stu-id="b51f4-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="b51f4-217">Jeśli nie, należy utworzyć _web.config_ plik w tym folderze z następującego kodu XML:</span><span class="sxs-lookup"><span data-stu-id="b51f4-217">If not, create a _web.config_ file in this folder with the following XML:</span></span>

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

<span data-ttu-id="b51f4-218">Dla istniejącej _web.config_ plików, skopiować całą `<rule>` element do Twojej _web.config_w `configuration/system.webServer/rewrite/rules` elementu.</span><span class="sxs-lookup"><span data-stu-id="b51f4-218">For an existing _web.config_ file, copy the entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="b51f4-219">Jeśli istnieją inne `<rule>` elementów w Twojej _web.config_, umieść skopiowanych `<rule>` element przed innych `<rule>` elementów.</span><span class="sxs-lookup"><span data-stu-id="b51f4-219">If there are other `<rule>` elements in your _web.config_, place the copied `<rule>` element before the other `<rule>` elements.</span></span>

<span data-ttu-id="b51f4-220">Ta reguła zwraca HTTP 301 (Stałe przekierowanie) protokołu HTTPS zawsze, gdy użytkownik wysyła żądanie HTTP do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b51f4-220">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="b51f4-221">Na przykład przekierowuje z `http://contoso.com` do `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="b51f4-221">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

<span data-ttu-id="b51f4-222">Aby uzyskać więcej informacji na moduł ponowne zapisywanie adresów URL usług IIS, zobacz [ponowne zapisywanie adresów URL](http://www.iis.net/downloads/microsoft/url-rewrite) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="b51f4-222">For more information on the IIS URL Rewrite module, see the [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="b51f4-223">Wymuszanie protokołu HTTPS dla aplikacji sieci Web w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="b51f4-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="b51f4-224">Usługa aplikacji w systemie Linux ma *nie* Wymuszanie protokołu HTTPS, więc każdy może nadal uzyskiwać dostęp do aplikacji sieci web przy użyciu protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="b51f4-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="b51f4-225">Aby wymusić HTTPS dla aplikacji sieci web, należy zdefiniować reguły ponownego zapisywania w _.htaccess_ plików dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b51f4-225">To enforce HTTPS for your web app, define a rewrite rule in the _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="b51f4-226">Połącz do punktu końcowego FTP aplikacji sieci web zgodnie z instrukcjami w [wdrażanie aplikacji w usłudze Azure App Service przy użyciu FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="b51f4-226">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="b51f4-227">W _/home/site/wwwroot_, Utwórz _.htaccess_ pliku następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="b51f4-227">In _/home/site/wwwroot_, create an _.htaccess_ file with the following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="b51f4-228">Ta reguła zwraca HTTP 301 (Stałe przekierowanie) protokołu HTTPS zawsze, gdy użytkownik wysyła żądanie HTTP do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b51f4-228">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="b51f4-229">Na przykład przekierowuje z `http://contoso.com` do `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="b51f4-229">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="b51f4-230">Zautomatyzować za pomocą skryptów</span><span class="sxs-lookup"><span data-stu-id="b51f4-230">Automate with scripts</span></span>

<span data-ttu-id="b51f4-231">Można zautomatyzować powiązań SSL dla aplikacji sieci web za pomocą skryptów przy użyciu [interfejsu wiersza polecenia Azure](/cli/azure/install-azure-cli) lub [programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b51f4-231">You can automate SSL bindings for your web app with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="b51f4-232">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b51f4-232">Azure CLI</span></span>

<span data-ttu-id="b51f4-233">Polecenie przekazuje wyeksportowanego pliku PFX i pobiera odcisk palca.</span><span class="sxs-lookup"><span data-stu-id="b51f4-233">The following command uploads an exported PFX file and gets the thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="b51f4-234">Polecenie dodaje powiązania SSL opartego na protokole SNI, za pomocą odcisku palca z poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="b51f4-234">The following command adds an SNI-based SSL binding, using the thumbprint from the previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="b51f4-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b51f4-235">Azure PowerShell</span></span>

<span data-ttu-id="b51f4-236">Polecenie przekazuje wyeksportowanego pliku PFX i dodaje powiązania SSL opartego na SNI.</span><span class="sxs-lookup"><span data-stu-id="b51f4-236">The following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="b51f4-237">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b51f4-237">Next steps</span></span>

<span data-ttu-id="b51f4-238">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="b51f4-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b51f4-239">Uaktualnij warstwę cenową aplikacji</span><span class="sxs-lookup"><span data-stu-id="b51f4-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="b51f4-240">Powiązać niestandardowego certyfikatu SSL z usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="b51f4-240">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="b51f4-241">Wymuszanie protokołu HTTPS dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="b51f4-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="b51f4-242">Powiązania certyfikatu SSL za pomocą skryptów automatyzacji</span><span class="sxs-lookup"><span data-stu-id="b51f4-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="b51f4-243">Przejdź do następnego samouczkiem, aby dowiedzieć się, jak używać usługi Azure Content Delivery Network.</span><span class="sxs-lookup"><span data-stu-id="b51f4-243">Advance to the next tutorial to learn how to use Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b51f4-244">Dodawanie sieci dostarczania zawartości (CDN) w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b51f4-244">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
