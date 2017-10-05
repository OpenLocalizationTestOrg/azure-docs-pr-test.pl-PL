---
title: "Włącz protokół HTTPS na domenę niestandardową Azure CDN | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak włączyć protokół HTTPS na punkt końcowy usługi Azure CDN z domeny niestandardowej."
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
ms.openlocfilehash: b334ba6bbec1d0a7e23a514174bffae01c7fff05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a><span data-ttu-id="62022-103">Włącz protokół HTTPS na domenę niestandardową Azure CDN</span><span class="sxs-lookup"><span data-stu-id="62022-103">Enable HTTPS on an Azure CDN custom domain</span></span>

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="62022-104">Obsługa protokołu HTTPS dla domen niestandardowych usługi Azure CDN umożliwia dostarczanie bezpieczne zawartości za pośrednictwem protokołu SSL w celu zwiększenia bezpieczeństwa danych podczas przesyłania przy użyciu nazwy domeny.</span><span class="sxs-lookup"><span data-stu-id="62022-104">HTTPS support for Azure CDN custom domains enables you to deliver secure content via SSL using your own domain name to improve the security of data while in transit.</span></span> <span data-ttu-id="62022-105">Przepływ pracy end-to-end, aby włączyć protokół HTTPS dla domeny niestandardowej jest uproszczone, za pomocą jednego kliknięcia aktywacji, pełnego zarządzania certyfikatami i wszystkie bez dodatkowych kosztów.</span><span class="sxs-lookup"><span data-stu-id="62022-105">The end-to-end workflow to enable HTTPS for your custom domain is simplified via one-click enablement, complete certificate management, and all with no additional cost.</span></span>

<span data-ttu-id="62022-106">Bardzo ważne dla zapewnienia prywatności i integralności danych z wszystkich aplikacji sieci web poufnych danych przesyłanych jest.</span><span class="sxs-lookup"><span data-stu-id="62022-106">It's critical to ensure the privacy and data integrity of all of your web applications sensitive data while in transit.</span></span> <span data-ttu-id="62022-107">Użycie protokołu HTTPS gwarantuje, że poufne dane są szyfrowane, gdy są wysyłane przez internet.</span><span class="sxs-lookup"><span data-stu-id="62022-107">Using the HTTPS protocol ensures that your sensitive data is encrypted when it is sent across the internet.</span></span> <span data-ttu-id="62022-108">Zapewnia zaufania, uwierzytelniania i chroni przed atakami aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="62022-108">It provides trust, authentication and protects your web applications from attacks.</span></span> <span data-ttu-id="62022-109">Obecnie usługa Azure CDN obsługuje HTTPS na punktu końcowego usługi CDN.</span><span class="sxs-lookup"><span data-stu-id="62022-109">Currently, Azure CDN supports HTTPS on a CDN endpoint.</span></span> <span data-ttu-id="62022-110">Na przykład w przypadku utworzenia punktu końcowego usługi CDN z usługi Azure CDN (np. https://contoso.azureedge.net), protokołu HTTPS jest włączona domyślnie.</span><span class="sxs-lookup"><span data-stu-id="62022-110">For example, if you create a CDN endpoint from Azure CDN (e.g. https://contoso.azureedge.net), HTTPS is enabled by default.</span></span> <span data-ttu-id="62022-111">Teraz z domeny niestandardowej HTTPS, można włączyć bezpieczne dostarczanie dla domeny niestandardowej (np. https://www.contoso.com) oraz.</span><span class="sxs-lookup"><span data-stu-id="62022-111">Now, with custom domain HTTPS, you can enable secure delivery for a custom domain (e.g. https://www.contoso.com) as well.</span></span> 

<span data-ttu-id="62022-112">Niektóre z kluczowych atrybutów funkcja HTTPS są:</span><span class="sxs-lookup"><span data-stu-id="62022-112">Some of the key attributes of HTTPS feature are:</span></span>

- <span data-ttu-id="62022-113">Bez dodatkowych kosztów: Brak nie koszty nabycia certyfikatu lub odnowienie i bez dodatkowych kosztów dla ruchu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="62022-113">No additional cost: There are no costs for certificate acquisition or renewal and no additional cost for HTTPS traffic.</span></span> <span data-ttu-id="62022-114">Po prostu płacisz za GB wyjście z sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="62022-114">You just pay for GB egress from the CDN.</span></span>

- <span data-ttu-id="62022-115">Włączanie prostego: jeden inicjowania obsługi kliknij przycisk jest dostępny z [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="62022-115">Simple enablement: One click provisioning is available from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="62022-116">Aby włączyć tę funkcję, można użyć interfejsu API REST lub innych narzędzi dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="62022-116">You can also use REST API or other developer tools to enable the feature.</span></span>

- <span data-ttu-id="62022-117">Zakończenie zarządzania certyfikatami: wszystkie certyfikatów nabywania i zarządzania jest już obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="62022-117">Complete certificate management: All certificate procurement and management is handled for you.</span></span> <span data-ttu-id="62022-118">Certyfikaty są automatycznie udostępniane i odnowione przed jego wygaśnięciem.</span><span class="sxs-lookup"><span data-stu-id="62022-118">Certificates are automatically provisioned and renewed prior to expiration.</span></span> <span data-ttu-id="62022-119">Usuwa to całkowicie ryzyka przerw w wyniku certyfikat wygasa.</span><span class="sxs-lookup"><span data-stu-id="62022-119">This completely removes the risks of service interruption as a result of a certificate expiring.</span></span>

>[!NOTE] 
><span data-ttu-id="62022-120">Przed włączeniem obsługi protokołu HTTPS, musi mieć już określone [domenę niestandardową Azure CDN](./cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="62022-120">Prior to enabling HTTPS support, you must have already established an [Azure CDN custom domain](./cdn-map-content-to-custom-domain.md).</span></span>

## <a name="step-1-enabling-the-feature"></a><span data-ttu-id="62022-121">Krok 1: Włączenie funkcji</span><span class="sxs-lookup"><span data-stu-id="62022-121">Step 1: Enabling the feature</span></span> 

1. <span data-ttu-id="62022-122">W [portalu Azure](https://portal.azure.com), przejdź do profilu sieci CDN w warstwie standardowa lub premium Verizon.</span><span class="sxs-lookup"><span data-stu-id="62022-122">In the [Azure portal](https://portal.azure.com), browse to your Verizon standard or premium CDN profile.</span></span>

2. <span data-ttu-id="62022-123">Na liście punktów końcowych kliknij punkt końcowy zawierający domenę niestandardową.</span><span class="sxs-lookup"><span data-stu-id="62022-123">In the list of endpoints, click the endpoint containing your custom domain.</span></span>

3. <span data-ttu-id="62022-124">Kliknij przycisk domeny niestandardowej, dla którego chcesz włączyć protokół HTTPS.</span><span class="sxs-lookup"><span data-stu-id="62022-124">Click the custom domain for which you want to enable HTTPS.</span></span>

    ![Blok końcowy](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. <span data-ttu-id="62022-126">Kliknij przycisk **na** Aby włączyć protokół HTTPS i zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="62022-126">Click **On** to enable HTTPS and save the change.</span></span>

    ![Niestandardowe okno protokołu HTTPS](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a><span data-ttu-id="62022-128">Krok 2: Weryfikacja domeny</span><span class="sxs-lookup"><span data-stu-id="62022-128">Step 2: Domain validation</span></span>

>[!IMPORTANT] 
><span data-ttu-id="62022-129">Należy ukończyć weryfikacji domeny na domenę niestandardową HTTPS będzie aktywny.</span><span class="sxs-lookup"><span data-stu-id="62022-129">You must complete domain validation before HTTPS will be active on your custom domain.</span></span> <span data-ttu-id="62022-130">Masz 6 dni roboczych, aby zatwierdzić domeny.</span><span class="sxs-lookup"><span data-stu-id="62022-130">You have 6 business days to approve the domain.</span></span> <span data-ttu-id="62022-131">Żądanie zostanie anulowane z zatwierdzaniem nie w ciągu 6 dni roboczych.</span><span class="sxs-lookup"><span data-stu-id="62022-131">Request will be canceled with no approval within 6 business days.</span></span>  

<span data-ttu-id="62022-132">Po włączeniu HTTPS na domenę niestandardową, naszych HTTPS dostawcę certyfikatów firmy DigiCert sprawdzi poprawność prawo własności do domeny, kontaktując się z rejestratorem domeny, na podstawie informacji rejestratorem WHOIS, za pośrednictwem poczty e-mail (domyślnie) lub telefonu.</span><span class="sxs-lookup"><span data-stu-id="62022-132">After enabling HTTPS on your custom domain, our HTTPS certificate provider DigiCert will validate ownership of your domain by contacting the registrant for your domain, based on WHOIS registrant information, via email (by default) or phone.</span></span> <span data-ttu-id="62022-133">DigiCert również będzie wysyłać wiadomości e-mail weryfikacji do poniżej adresów.</span><span class="sxs-lookup"><span data-stu-id="62022-133">DigiCert will also send the verification email to the below addresses.</span></span> <span data-ttu-id="62022-134">Jeśli prywatne informacje rejestratorem WHOIS, upewnij się, że możesz zatwierdzić bezpośrednio z jednego z tych adresów.</span><span class="sxs-lookup"><span data-stu-id="62022-134">If WHOIS registrant information is private, make sure you can approve directly from one of these addresses.</span></span>

><span data-ttu-id="62022-135">Administrator @ administratora < name.com Twoja domena > @< name.com your domeny ></span><span class="sxs-lookup"><span data-stu-id="62022-135">admin@<your-domain-name.com> administrator@<your-domain-name.com></span></span>  
><span data-ttu-id="62022-136">webmaster @< name.com your domeny ></span><span class="sxs-lookup"><span data-stu-id="62022-136">webmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="62022-137">hostmaster @< name.com your domeny ></span><span class="sxs-lookup"><span data-stu-id="62022-137">hostmaster@<your-domain-name.com></span></span>  
><span data-ttu-id="62022-138">Postmaster @< name.com your domeny ></span><span class="sxs-lookup"><span data-stu-id="62022-138">postmaster@<your-domain-name.com></span></span>


<span data-ttu-id="62022-139">Po odebraniu wiadomości e-mail, dostępne są dwie opcje weryfikacji:</span><span class="sxs-lookup"><span data-stu-id="62022-139">Upon receiving the email, you have two verification options:</span></span>

1. <span data-ttu-id="62022-140">Możesz zatwierdzać wszystkie przyszłe zamówień za pomocą tego samego konta dla tej samej domeny katalogu głównego, np. consoto.com.</span><span class="sxs-lookup"><span data-stu-id="62022-140">You can approve all future orders placed through the same account for the same root domain, e.g. consoto.com.</span></span> <span data-ttu-id="62022-141">Jest to zalecane podejście, jeśli zamierzasz dodać dodatkowe domeny niestandardowe w przyszłości dla tej samej domeny głównej.</span><span class="sxs-lookup"><span data-stu-id="62022-141">This is a recommended approach if you are planning to add additional custom domains in the future for the same root domain.</span></span>
 
2. <span data-ttu-id="62022-142">Możesz po prostu zatwierdzić nazwę określonego hosta używaną w tym żądaniu.</span><span class="sxs-lookup"><span data-stu-id="62022-142">You can just approve the specific host name used in this request.</span></span> <span data-ttu-id="62022-143">Dodatkowe zatwierdzenie będzie wymagane dla kolejnych żądań.</span><span class="sxs-lookup"><span data-stu-id="62022-143">Additional approval will be required for subsequent requests.</span></span>

    <span data-ttu-id="62022-144">Przykład poczty e-mail:</span><span class="sxs-lookup"><span data-stu-id="62022-144">Example email:</span></span>
    
    ![Niestandardowe okno protokołu HTTPS](./media/cdn-custom-ssl/domain-validation-email-example.png)

<span data-ttu-id="62022-146">Po zatwierdzeniu żądania DigiCert doda niestandardową nazwę domeny certyfikat SAN.</span><span class="sxs-lookup"><span data-stu-id="62022-146">After approval, DigiCert will add your custom domain name to the SAN certificate.</span></span> <span data-ttu-id="62022-147">Certyfikat będzie ważny przez jeden rok i będą automatycznie odnawiane przed wygasła.</span><span class="sxs-lookup"><span data-stu-id="62022-147">The certificate will be valid for one year and will be auto renewed before it's expired.</span></span>

## <a name="step-3-wait-for-the-propagation-then-start-using-your-feature"></a><span data-ttu-id="62022-148">Krok 3: Poczekaj, aż propagacji, a następnie rozpocząć korzystanie z funkcji</span><span class="sxs-lookup"><span data-stu-id="62022-148">Step 3: Wait for the propagation then start using your feature</span></span>

<span data-ttu-id="62022-149">Po zweryfikowaniu jest nazwą domeny upłynąć do 6-8 godzin dla domeny niestandardowej funkcji HTTPS jest aktywne.</span><span class="sxs-lookup"><span data-stu-id="62022-149">After the domain name is validated it will take up to 6-8 hours for the custom domain HTTPS feature to be active.</span></span> <span data-ttu-id="62022-150">Po zakończeniu procesu stan "HTTPS niestandardowych" w portalu Azure będzie ustawiony na "Enabled".</span><span class="sxs-lookup"><span data-stu-id="62022-150">After the process is complete, the "custom HTTPS" status in the Azure portal will be set to "Enabled".</span></span> <span data-ttu-id="62022-151">Protokół HTTPS z domeny niestandardowej jest teraz gotowy do użycia.</span><span class="sxs-lookup"><span data-stu-id="62022-151">HTTPS with your custom domain is now ready for your use.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="62022-152">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="62022-152">Frequently asked questions</span></span>

1. <span data-ttu-id="62022-153">*Kto jest dostawcę certyfikatów i jakiego typu używanego certyfikatu?*</span><span class="sxs-lookup"><span data-stu-id="62022-153">*Who is the certificate provider and what type of certificate is used?*</span></span>

    <span data-ttu-id="62022-154">Używamy nazwy alternatywnej podmiotu (SAN) certyfikatu dostarczonego przez DigiCert.</span><span class="sxs-lookup"><span data-stu-id="62022-154">We use Subject Alternative Names (SAN) certificate provided by DigiCert.</span></span> <span data-ttu-id="62022-155">Certyfikat SAN można zabezpieczyć wiele nazw FQDN z jednym certyfikatem.</span><span class="sxs-lookup"><span data-stu-id="62022-155">A SAN certificate can secure multiple fully qualifIed domain names with one certificate.</span></span>

2. <span data-ttu-id="62022-156">*Można użyć dedykowanego certyfikatu?*</span><span class="sxs-lookup"><span data-stu-id="62022-156">*Can I use my dedicated certificate?*</span></span>
    
    <span data-ttu-id="62022-157">Aktualnie nie ale nie znajduje się na plan.</span><span class="sxs-lookup"><span data-stu-id="62022-157">Not currently, but it's on the roadmap.</span></span>

3. <span data-ttu-id="62022-158">*Co zrobić, jeśli I nie otrzymywać wiadomości e-mail weryfikacji domeny firmy DigiCert?*</span><span class="sxs-lookup"><span data-stu-id="62022-158">*What if I don't receive the domain verification email from DigiCert?*</span></span>

    <span data-ttu-id="62022-159">Skontaktuj się z firmy Microsoft, jeśli użytkownik nie otrzyma wiadomość e-mail w ciągu 24 godzin.</span><span class="sxs-lookup"><span data-stu-id="62022-159">Please contact Microsoft if you don't receive an email within 24 hours.</span></span>

4. <span data-ttu-id="62022-160">*Używa mniej bezpieczna niż certyfikat dedykowanych certyfikat SAN?*</span><span class="sxs-lookup"><span data-stu-id="62022-160">*Is using a SAN certificate less secure than a dedicated certificate?*</span></span>
    
    <span data-ttu-id="62022-161">Certyfikat SAN wykonuje szyfrowanie i zabezpieczenia standardach jako dedykowane certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="62022-161">A SAN cert follows the same encryption and security standards as a dedicated cert.</span></span> <span data-ttu-id="62022-162">Wszystkie wystawiane certyfikaty SSL są za pomocą algorytmu SHA-256 rozszerzonego serwera zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="62022-162">All issued SSL certificates are using SHA-256 for enhanced server security.</span></span>

5. <span data-ttu-id="62022-163">*Można używać protokołu HTTPS domeny niestandardowej z usługą Azure CDN from Akamai?*</span><span class="sxs-lookup"><span data-stu-id="62022-163">*Can I use custom domain HTTPS with Azure CDN from Akamai?*</span></span>

    <span data-ttu-id="62022-164">Obecnie ta funkcja jest dostępna tylko z usługą Azure CDN from Verizon.</span><span class="sxs-lookup"><span data-stu-id="62022-164">Currently, this feature is only available with Azure CDN from Verizon.</span></span> <span data-ttu-id="62022-165">Pracujemy nad Obsługa tej funkcji w programie Azure CDN from Akamai w najbliższych miesiącach.</span><span class="sxs-lookup"><span data-stu-id="62022-165">We are working on supporting this feature with Azure CDN from Akamai in the coming months.</span></span>


## <a name="next-steps"></a><span data-ttu-id="62022-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="62022-166">Next steps</span></span>

- <span data-ttu-id="62022-167">Dowiedz się, jak skonfigurować [niestandardową domenę na punkt końcowy usługi Azure CDN](./cdn-map-content-to-custom-domain.md)</span><span class="sxs-lookup"><span data-stu-id="62022-167">Learn how to set up a [custom domain on your Azure CDN endpoint](./cdn-map-content-to-custom-domain.md)</span></span>


