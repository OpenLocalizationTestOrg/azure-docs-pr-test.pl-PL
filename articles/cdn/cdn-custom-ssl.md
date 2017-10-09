---
title: "AAA \"Włącz protokół HTTPS na domenę niestandardową Azure CDN | Dokumentacja firmy Microsoft\""
description: "Dowiedz się, jak tooenable HTTPS na punkt końcowy usługi Azure CDN z domeny niestandardowej."
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="da5ab-103">Włącz protokół HTTPS na domenę niestandardową Azure CDN</span><span class="sxs-lookup"><span data-stu-id="da5ab-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="da5ab-104">Obsługa protokołu HTTPS dla domen niestandardowych usługi Azure CDN umożliwia bezpieczne zawartości za pośrednictwem protokołu SSL przy użyciu własnego domeny nazwa tooimprove hello bezpieczeństwa danych przesyłanych za toodeliver.</span><span class="sxs-lookup"><span data-stu-id="da5ab-104">HTTPS support for Azure CDN custom domains enables you toodeliver secure content via SSL using your own domain name tooimprove hello security of data while in transit.</span></span> <span data-ttu-id="da5ab-105">Hello przepływu pracy na trasie tooenable HTTPS dla domeny niestandardowej jest uproszczone, za pomocą pełnego zarządzania certyfikatami, na jednym kliknięciem włączenie i wszystkie bez dodatkowych kosztów.</span><span class="sxs-lookup"><span data-stu-id="da5ab-105">hello end-to-end workflow tooenable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="da5ab-106">Jest krytyczne tooensure hello prywatność i integralność danych ze wszystkich aplikacji sieci web poufne dane przesyłane.</span><span class="sxs-lookup"><span data-stu-id="da5ab-106">It's critical tooensure hello privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="da5ab-107">Przy użyciu protokołu HTTPS gwarantuje, że poufne dane są szyfrowane, gdy są przesyłane przez hello hello internet.</span><span class="sxs-lookup"><span data-stu-id="da5ab-107">Using hello HTTPS protocol ensures that your sensitive data is encrypted when it is sent across hello internet.</span></span> <span data-ttu-id="da5ab-108">Zapewnia zaufania, uwierzytelniania i chroni przed atakami aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="da5ab-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="da5ab-109">Obecnie usługa Azure CDN obsługuje HTTPS na punktu końcowego usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="da5ab-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="da5ab-110">Na przykład w przypadku utworzenia punktu końcowego usługi CDN z usługi Azure CDN (np. https://contoso.azureedge.net), protokołu HTTPS jest włączona domyślnie.</span><span class="sxs-lookup"><span data-stu-id="da5ab-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="da5ab-111">Teraz z domeny niestandardowej HTTPS, można włączyć bezpieczne dostarczanie dla domeny niestandardowej (np. https://www.contoso.com) oraz.</span><span class="sxs-lookup"><span data-stu-id="da5ab-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="da5ab-112">Atrybuty klucza hello funkcji HTTPS, należą:</span><span class="sxs-lookup"><span data-stu-id="da5ab-112">Some of hello key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="da5ab-113">Bez dodatkowych kosztów: Brak nie koszty nabycia certyfikatu lub odnowienie i bez dodatkowych kosztów dla ruchu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="da5ab-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="da5ab-114">Płacisz tylko za wyjście GB z hello CDN.</span><span class="sxs-lookup"><span data-stu-id="da5ab-114">You just pay for GB egress from hello CDN.</span></span>

- <span data-ttu-id="da5ab-115">Włączanie prostego: jeden inicjowania obsługi kliknij jest dostępna z hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="da5ab-115">Simple enablement: One click provisioning is available from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="da5ab-116">Można również użyć interfejsu API REST lub innych funkcji hello tooenable narzędzia developer.</span><span class="sxs-lookup"><span data-stu-id="da5ab-116">You can also use REST API or other developer tools tooenable hello feature.</span></span>

- <span data-ttu-id="da5ab-117">Zakończenie zarządzania certyfikatami: wszystkie certyfikatów nabywania i zarządzania jest już obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="da5ab-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="da5ab-118">Certyfikaty są automatycznie konfigurowani i odnowione przed tooexpiration.</span><span class="sxs-lookup"><span data-stu-id="da5ab-118">Certificates are automatically provisioned and renewed prior tooexpiration.</span></span> <span data-ttu-id="da5ab-119">Usuwa to całkowicie hello ryzyko przerw w wyniku certyfikat wygasa.</span><span class="sxs-lookup"><span data-stu-id="da5ab-119">This completely removes hello risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="da5ab-120">Obsługa protokołu HTTPS wcześniejsze tooenabling, musi mieć już określone [domenę niestandardową Azure CDN](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="da5ab-120">Prior tooenabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-hello-feature"></a><span data-ttu-id="da5ab-121">Krok 1: Włączenie funkcji hello</span><span class="sxs-lookup"><span data-stu-id="da5ab-121">Step 1: Enabling hello feature</span></span> 

1. <span data-ttu-id="da5ab-122">W hello [portalu Azure](https://portal.azure.com), Przeglądaj tooyour Verizon standard lub premium profilu CDN.</span><span class="sxs-lookup"><span data-stu-id="da5ab-122">In hello [Azure portal](https://portal.azure.com), browse tooyour Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="da5ab-123">Kliknij punkt końcowy hello zawierający domenę niestandardową na liście hello punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="da5ab-123">In hello list of endpoints, click hello endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="da5ab-124">Kliknij domenę niestandardową hello, dla której ma zostać tooenable HTTPS.</span><span class="sxs-lookup"><span data-stu-id="da5ab-124">Click hello custom domain for which you want tooenable HTTPS.</span></span>

    ![Blok końcowy](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="da5ab-126">Kliknij przycisk **na** tooenable HTTPS i Zapisz zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="da5ab-126">Click **On** tooenable HTTPS and save hello change.</span></span>

    ![Niestandardowe okno protokołu HTTPS](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="da5ab-128">Krok 2: Weryfikacja domeny</span><span class="sxs-lookup"><span data-stu-id="da5ab-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="da5ab-129">Należy ukończyć weryfikacji domeny na domenę niestandardową HTTPS będzie aktywny.</span><span class="sxs-lookup"><span data-stu-id="da5ab-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="da5ab-130">Masz 6 firm dni tooapprove hello domeny.</span><span class="sxs-lookup"><span data-stu-id="da5ab-130">You have 6 business days tooapprove hello domain.</span></span> <span data-ttu-id="da5ab-131">Żądanie zostanie anulowane z zatwierdzaniem nie w ciągu 6 dni roboczych.</span><span class="sxs-lookup"><span data-stu-id="da5ab-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="da5ab-132">Po włączeniu HTTPS na domenę niestandardową, naszych HTTPS dostawcę certyfikatów firmy DigiCert sprawdzi poprawność prawo własności do domeny, kontaktując się z rejestratorem hello domeny, na podstawie informacji rejestratorem WHOIS, za pośrednictwem poczty e-mail (domyślnie) lub telefonu.</span><span class="sxs-lookup"><span data-stu-id="da5ab-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting hello registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="da5ab-133">DigiCert również będzie wysyłać hello weryfikacji e-mail toohello poniżej adresów.</span><span class="sxs-lookup"><span data-stu-id="da5ab-133">DigiCert will also send hello verification email toohello below addresses.</span></span> <span data-ttu-id="da5ab-134">Jeśli prywatne informacje rejestratorem WHOIS, upewnij się, że możesz zatwierdzić bezpośrednio z jednego z tych adresów.</span><span class="sxs-lookup"><span data-stu-id="da5ab-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="da5ab-135">Administrator @ administratora < name.com Twoja domena > @< name.com your domeny ></span><span class="sxs-lookup"><span data-stu-id="da5ab-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="da5ab-136">webmaster @< name.com your domeny ></span><span class="sxs-lookup"><span data-stu-id="da5ab-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="da5ab-137">hostmaster @< name.com your domeny ></span><span class="sxs-lookup"><span data-stu-id="da5ab-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="da5ab-138">Postmaster @< name.com your domeny ></span><span class="sxs-lookup"><span data-stu-id="da5ab-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="da5ab-139">Po odebraniu wiadomości e-mail hello, dostępne są dwie opcje weryfikacji:</span><span class="sxs-lookup"><span data-stu-id="da5ab-139">Upon receiving hello email, you have two verification options:</span></span>

1. <span data-ttu-id="da5ab-140">Możesz zatwierdzać wszystkie przyszłe zamówień za pośrednictwem hello tego samego konta dla hello tej samej domeny katalogu głównego, np. consoto.com. Jest to zalecane podejście, jeśli planujesz tooadd dodatkowe domeny niestandardowe w przyszłości dla hello hello tej samej domeny katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="da5ab-140">You can approve all future orders placed through hello same account for hello same root domain, e.g. consoto.com. This is a recommended approach if you are planning tooadd additional custom domains in hello future for hello same root domain.</span></span>
 
2. <span data-ttu-id="da5ab-141">Możesz po prostu zatwierdzić hello określoną nazwę hosta używane w tym żądaniu.</span><span class="sxs-lookup"><span data-stu-id="da5ab-141">You can just approve hello specific host name used in this request.</span></span> <span data-ttu-id="da5ab-142">Dodatkowe zatwierdzenie będzie wymagane dla kolejnych żądań.</span><span class="sxs-lookup"><span data-stu-id="da5ab-142">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="da5ab-143">Przykład poczty e-mail:</span><span class="sxs-lookup"><span data-stu-id="da5ab-143">Example email:</span></span>
    
    ![Niestandardowe okno protokołu HTTPS](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="da5ab-145">Po zatwierdzeniu żądania DigiCert doda certyfikat SAN toohello nazwy domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="da5ab-145">After approval, DigiCert will add your custom domain name toohello SAN certificate.</span></span> <span data-ttu-id="da5ab-146">certyfikat Hello będzie ważny przez jeden rok i będą automatycznie odnawiane przed wygasła.</span><span class="sxs-lookup"><span data-stu-id="da5ab-146">hello certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a><span data-ttu-id="da5ab-147">Krok 3: Hello propagacji poczekać i rozpocząć korzystanie z funkcji</span><span class="sxs-lookup"><span data-stu-id="da5ab-147">Step 3: Wait for hello propagation then start using your feature</span></span>

<span data-ttu-id="da5ab-148">Po zweryfikowaniu jest nazwa domeny hello zajmuje too6 8 godzin dla active toobe funkcji HTTPS domeny niestandardowej hello.</span><span class="sxs-lookup"><span data-stu-id="da5ab-148">After hello domain name is validated it will take up too6-8 hours for hello custom domain HTTPS feature toobe active.</span></span> <span data-ttu-id="da5ab-149">Po ukończeniu procesu hello stan "HTTPS niestandardowego" hello w portalu Azure hello zostanie ustawiona zbyt "Enabled".</span><span class="sxs-lookup"><span data-stu-id="da5ab-149">After hello process is complete, hello "custom HTTPS" status in hello Azure portal will be set too"Enabled".</span></span> <span data-ttu-id="da5ab-150">Protokół HTTPS z domeny niestandardowej jest teraz gotowy do użycia.</span><span class="sxs-lookup"><span data-stu-id="da5ab-150">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="da5ab-151">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="da5ab-151">Frequently asked questions</span></span>

1. <span data-ttu-id="da5ab-152">*Kto jest hello dostawcę certyfikatów i jakiego typu używanego certyfikatu?*</span><span class="sxs-lookup"><span data-stu-id="da5ab-152">*Who is hello certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="da5ab-153">Używamy nazwy alternatywnej podmiotu (SAN) certyfikatu dostarczonego przez DigiCert.</span><span class="sxs-lookup"><span data-stu-id="da5ab-153">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="da5ab-154">Certyfikat SAN można zabezpieczyć wiele nazw FQDN z jednym certyfikatem.</span><span class="sxs-lookup"><span data-stu-id="da5ab-154">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="da5ab-155">*Można użyć dedykowanego certyfikatu?*</span><span class="sxs-lookup"><span data-stu-id="da5ab-155">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="da5ab-156">Aktualnie nie, ale jego na powitania plan.</span><span class="sxs-lookup"><span data-stu-id="da5ab-156">Not currently, but it's on hello roadmap.</span></span>

3. <span data-ttu-id="da5ab-157">*Co zrobić, jeśli nie pojawia się hello domeny weryfikacji w wiadomości e-mail od firmy DigiCert?*</span><span class="sxs-lookup"><span data-stu-id="da5ab-157">*What if I don't receive hello domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="da5ab-158">Skontaktuj się z firmy Microsoft, jeśli użytkownik nie otrzyma wiadomość e-mail w ciągu 24 godzin.</span><span class="sxs-lookup"><span data-stu-id="da5ab-158">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="da5ab-159">*Używa mniej bezpieczna niż certyfikat dedykowanych certyfikat SAN?*</span><span class="sxs-lookup"><span data-stu-id="da5ab-159">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="da5ab-160">Certyfikat SAN się, że następujące hello standardach szyfrowania i zabezpieczeń jako dedykowane certyfikatu. Wszystkie wystawiane certyfikaty SSL są za pomocą algorytmu SHA-256 rozszerzonego serwera zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="da5ab-160">A SAN cert follows hello same encryption and security standards as a dedicated cert. All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="da5ab-161">*Można używać protokołu HTTPS domeny niestandardowej z usługą Azure CDN from Akamai?*</span><span class="sxs-lookup"><span data-stu-id="da5ab-161">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="da5ab-162">Obecnie ta funkcja jest dostępna tylko z usługą Azure CDN from Verizon.</span><span class="sxs-lookup"><span data-stu-id="da5ab-162">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="da5ab-163">Pracujemy nad Obsługa tej funkcji w programie Azure CDN from Akamai w najbliższych miesiącach hello.</span><span class="sxs-lookup"><span data-stu-id="da5ab-163">We are working on supporting this feature with Azure CDN from Akamai in hello coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="da5ab-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="da5ab-164">Next steps</span></span>

- <span data-ttu-id="da5ab-165">Dowiedz się, jak tooset się [niestandardową domenę na punkt końcowy usługi Azure CDN](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="da5ab-165">Learn how tooset up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


