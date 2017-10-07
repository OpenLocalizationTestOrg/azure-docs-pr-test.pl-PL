---
title: "problemy z połączeniem aaaTroubleshoot Azure punkt lokacja | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootroubleshoot problemów połączenie punkt lokacja."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="da743-103">Rozwiązywanie problemów: Problemów Azure połączenie punkt lokacja</span><span class="sxs-lookup"><span data-stu-id="da743-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="da743-104">W tym artykule wymieniono typowe problemy połączenie punkt lokacja, które mogą wystąpić.</span><span class="sxs-lookup"><span data-stu-id="da743-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="da743-105">Omówiono w nim również możliwe przyczyny i potencjalne rozwiązania tych problemów.</span><span class="sxs-lookup"><span data-stu-id="da743-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="da743-106">Błąd klienta sieci VPN: nie można odnaleźć certyfikatu</span><span class="sxs-lookup"><span data-stu-id="da743-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="da743-107">Objaw</span><span class="sxs-lookup"><span data-stu-id="da743-107">Symptom</span></span>

<span data-ttu-id="da743-108">Podczas tooan tooconnect sieci wirtualnej platformy Azure przy użyciu powitania klienta sieci VPN, pojawi się następujący komunikat o błędzie hello:</span><span class="sxs-lookup"><span data-stu-id="da743-108">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="da743-109">**Nie można odnaleźć certyfikatu, który może zostać użyty z protokołem uwierzytelniania rozszerzonego. (Błąd 798)**</span><span class="sxs-lookup"><span data-stu-id="da743-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="da743-110">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="da743-110">Cause</span></span>

<span data-ttu-id="da743-111">Ten problem występuje, jeśli brakuje certyfikat klienta na powitania **Certyfikaty — bieżący User\Personal\Certificates**.</span><span class="sxs-lookup"><span data-stu-id="da743-111">This problem occurs if hello client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="da743-112">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="da743-112">Solution</span></span>

<span data-ttu-id="da743-113">Upewnij się, że ten certyfikat klienta hello jest zainstalowane na powitania po lokalizację magazynu certyfikatów hello (Certmgr.msc):</span><span class="sxs-lookup"><span data-stu-id="da743-113">Make sure that hello client certificate is installed in hello following location of hello Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="da743-114">**Certyfikaty — bieżący User\Personal\Certificates**</span><span class="sxs-lookup"><span data-stu-id="da743-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="da743-115">Aby uzyskać więcej informacji o sposobie tooinstall hello certyfikatu klienta, zobacz [Generowanie i eksportowania certyfikatów połączeń punkt lokacja](vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="da743-115">For more information about how tooinstall hello client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="da743-116">Po zaimportowaniu certyfikatu klienta hello nie zaznaczaj hello **Włącz silną ochronę klucza prywatnego** opcji.</span><span class="sxs-lookup"><span data-stu-id="da743-116">When you import hello client certificate, do not select hello **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="da743-117">Błąd klienta sieci VPN: Odebrano wiadomość hello jest nieoczekiwany lub nieprawidłowo sformatowany</span><span class="sxs-lookup"><span data-stu-id="da743-117">VPN client error: hello message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="da743-118">Objaw</span><span class="sxs-lookup"><span data-stu-id="da743-118">Symptom</span></span>

<span data-ttu-id="da743-119">Podczas tooan tooconnect sieci wirtualnej platformy Azure przy użyciu powitania klienta sieci VPN, pojawi się następujący komunikat o błędzie hello:</span><span class="sxs-lookup"><span data-stu-id="da743-119">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="da743-120">**Odebrano wiadomość Hello jest nieoczekiwany lub nieprawidłowo sformatowany. (Błąd 0x80090326)**</span><span class="sxs-lookup"><span data-stu-id="da743-120">**hello message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="da743-121">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="da743-121">Cause</span></span>

<span data-ttu-id="da743-122">Ten problem występuje, gdy klucz publiczny certyfikatu głównego hello nie zostało załadowane do hello bramy sieci VPN platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="da743-122">This problem occurs if hello root certificate public key is not uploaded into hello Azure VPN gateway.</span></span> <span data-ttu-id="da743-123">Może również wystąpić, jeśli klucz hello jest uszkodzony lub wygasł.</span><span class="sxs-lookup"><span data-stu-id="da743-123">It can also occur if hello key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="da743-124">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="da743-124">Solution</span></span>

<span data-ttu-id="da743-125">tooresolve ten problem, sprawdź status hello hello głównego certyfikatu w hello toosee portalu Azure, czy został on odwołany.</span><span class="sxs-lookup"><span data-stu-id="da743-125">tooresolve this problem, check hello status of hello root certificate in hello Azure portal toosee whether it was revoked.</span></span> <span data-ttu-id="da743-126">Jeśli nie został odwołany, spróbuj certyfikatu głównego hello toodelete i reupload.</span><span class="sxs-lookup"><span data-stu-id="da743-126">If it is not revoked, try toodelete hello root certificate and reupload.</span></span> <span data-ttu-id="da743-127">Aby uzyskać więcej informacji, zobacz [tworzenia certyfikatów](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span><span class="sxs-lookup"><span data-stu-id="da743-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="da743-128">Błąd klienta sieci VPN: łańcuch certyfikatów przetworzona, ale została przerwana</span><span class="sxs-lookup"><span data-stu-id="da743-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="da743-129">Objaw</span><span class="sxs-lookup"><span data-stu-id="da743-129">Symptom</span></span> 

<span data-ttu-id="da743-130">Podczas tooan tooconnect sieci wirtualnej platformy Azure przy użyciu powitania klienta sieci VPN, pojawi się następujący komunikat o błędzie hello:</span><span class="sxs-lookup"><span data-stu-id="da743-130">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="da743-131">**Łańcuch certyfikatów przetworzona, ale została przerwana w certyfikacie głównym, który nie jest zaufany przez dostawcę zaufania hello.**</span><span class="sxs-lookup"><span data-stu-id="da743-131">**A certificate chain processed but terminated in a root certificate which is not trusted by hello trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="da743-132">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="da743-132">Solution</span></span>

1. <span data-ttu-id="da743-133">Upewnij się, że hello następujące certyfikaty są w poprawnej lokalizacji hello:</span><span class="sxs-lookup"><span data-stu-id="da743-133">Make sure that hello following certificates are in hello correct location:</span></span>

    | <span data-ttu-id="da743-134">Certyfikat</span><span class="sxs-lookup"><span data-stu-id="da743-134">Certificate</span></span> | <span data-ttu-id="da743-135">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="da743-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="da743-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="da743-136">AzureClient.pfx</span></span>  | <span data-ttu-id="da743-137">Bieżący User\Personal\Certificates</span><span class="sxs-lookup"><span data-stu-id="da743-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="da743-138">Azuregateway -*GUID*. cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="da743-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="da743-139">Bieżący User\Trusted główne urzędy certyfikacji</span><span class="sxs-lookup"><span data-stu-id="da743-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="da743-140">AzureGateway -*GUID*. cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="da743-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="da743-141">Lokalny komputer lokalny\Zaufane główne urzędy certyfikacji</span><span class="sxs-lookup"><span data-stu-id="da743-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="da743-142">Jeśli certyfikaty hello znajdują się już w lokalizacji hello, spróbuj toodelete hello certyfikatów, a następnie zainstaluj je ponownie.</span><span class="sxs-lookup"><span data-stu-id="da743-142">If hello certificates are already in hello location, try toodelete hello certificates and reinstall them.</span></span> <span data-ttu-id="da743-143">Witaj  **azuregateway -*GUID*. cloudapp.net** certyfikat znajduje się w pakietu konfiguracji klienta VPN hello, który został pobrany z portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="da743-143">hello **azuregateway-*GUID*.cloudapp.net** certificate is in hello VPN client configuration package that you downloaded from hello Azure portal.</span></span> <span data-ttu-id="da743-144">Można użyć pliku archivers tooextract hello pliki z pakietu hello.</span><span class="sxs-lookup"><span data-stu-id="da743-144">You can use file archivers tooextract hello files from hello package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="da743-145">Błąd pobierania pliku: nie określono docelowego identyfikatora URI</span><span class="sxs-lookup"><span data-stu-id="da743-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="da743-146">Objaw</span><span class="sxs-lookup"><span data-stu-id="da743-146">Symptom</span></span>

<span data-ttu-id="da743-147">Pojawi się następujący komunikat o błędzie hello:</span><span class="sxs-lookup"><span data-stu-id="da743-147">You receive hello following error message:</span></span>

<span data-ttu-id="da743-148">**Wystąpił błąd podczas pobierania pliku. Nie określono docelowego identyfikatora URI.**</span><span class="sxs-lookup"><span data-stu-id="da743-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="da743-149">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="da743-149">Cause</span></span> 

<span data-ttu-id="da743-150">Ten problem występuje z powodu typu niepoprawne bramy.</span><span class="sxs-lookup"><span data-stu-id="da743-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="da743-151">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="da743-151">Solution</span></span>

<span data-ttu-id="da743-152">Witaj typu bramy sieci VPN musi być **VPN**, i hello typ sieci VPN musi być **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="da743-152">hello VPN gateway type must be **VPN**, and hello VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="da743-153">Błąd klienta sieci VPN: sieci VPN platformy Azure niestandardowego skryptu nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="da743-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="da743-154">Objaw</span><span class="sxs-lookup"><span data-stu-id="da743-154">Symptom</span></span>

<span data-ttu-id="da743-155">Podczas tooan tooconnect sieci wirtualnej platformy Azure przy użyciu powitania klienta sieci VPN, pojawi się następujący komunikat o błędzie hello:</span><span class="sxs-lookup"><span data-stu-id="da743-155">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="da743-156">**Skryptu niestandardowego (tooupdate Twojego routingu tabeli) nie powiodło się. (Błąd 8007026f)**</span><span class="sxs-lookup"><span data-stu-id="da743-156">**Custom script (tooupdate your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="da743-157">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="da743-157">Cause</span></span>

<span data-ttu-id="da743-158">Ten problem może wystąpić, jeśli próbujesz połączenia sieci VPN punktu lokacji hello tooopen przy użyciu skrótu.</span><span class="sxs-lookup"><span data-stu-id="da743-158">This problem might occur if you are trying tooopen hello site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="da743-159">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="da743-159">Solution</span></span> 

<span data-ttu-id="da743-160">Otwórz hello pakietu sieci VPN bezpośrednio, zamiast z hello skrótów.</span><span class="sxs-lookup"><span data-stu-id="da743-160">Open hello VPN package directly instead of opening it from hello shortcut.</span></span>

## <a name="cannot-install-hello-vpn-client"></a><span data-ttu-id="da743-161">Nie można zainstalować powitania klienta sieci VPN</span><span class="sxs-lookup"><span data-stu-id="da743-161">Cannot install hello VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="da743-162">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="da743-162">Cause</span></span> 

<span data-ttu-id="da743-163">Dodatkowy certyfikat jest brama sieci VPN hello tootrust wymagane dla sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="da743-163">An additional certificate is required tootrust hello VPN gateway for your virtual network.</span></span> <span data-ttu-id="da743-164">certyfikat Hello jest uwzględniany w pakietu konfiguracji klienta VPN hello, które są generowane na podstawie hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="da743-164">hello certificate is included in hello VPN client configuration package that is generated from hello Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="da743-165">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="da743-165">Solution</span></span>

<span data-ttu-id="da743-166">Wyodrębnienie pakietu konfiguracji klienta VPN hello i Znajdź plik cer hello.</span><span class="sxs-lookup"><span data-stu-id="da743-166">Extract hello VPN client configuration package, and find hello .cer file.</span></span> <span data-ttu-id="da743-167">Witaj tooinstall certyfikatów, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="da743-167">tooinstall hello certificate, follow these steps:</span></span>

1. <span data-ttu-id="da743-168">Otwórz mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="da743-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="da743-169">Dodaj hello **certyfikaty** przystawki.</span><span class="sxs-lookup"><span data-stu-id="da743-169">Add hello **Certificates** snap-in.</span></span>
3. <span data-ttu-id="da743-170">Wybierz hello **komputera** konta na komputerze lokalnym hello.</span><span class="sxs-lookup"><span data-stu-id="da743-170">Select hello **Computer** account for hello local computer.</span></span>
4. <span data-ttu-id="da743-171">Kliknij prawym przyciskiem myszy hello **zaufane główne urzędy certyfikacji** węzła.</span><span class="sxs-lookup"><span data-stu-id="da743-171">Right-click hello **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="da743-172">Kliknij przycisk **wszystkie zadania** > **importu**, a plik .cer toohello przeglądania wyodrębniony z pakietu konfiguracji klienta VPN hello.</span><span class="sxs-lookup"><span data-stu-id="da743-172">Click **All-Task** > **Import**, and browse toohello .cer file you extracted from hello VPN client configuration package.</span></span>
5. <span data-ttu-id="da743-173">Uruchom ponownie komputer hello.</span><span class="sxs-lookup"><span data-stu-id="da743-173">Restart hello computer.</span></span> 
6. <span data-ttu-id="da743-174">Spróbuj tooinstall hello obsługi klienta VPN.</span><span class="sxs-lookup"><span data-stu-id="da743-174">Try tooinstall hello VPN client.</span></span>

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a><span data-ttu-id="da743-175">Błąd portalu Azure: nie powiodło się bramy sieci VPN hello toosave i hello dane są nieprawidłowe</span><span class="sxs-lookup"><span data-stu-id="da743-175">Azure portal error: Failed toosave hello VPN gateway, and hello data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="da743-176">Objaw</span><span class="sxs-lookup"><span data-stu-id="da743-176">Symptom</span></span>

<span data-ttu-id="da743-177">Podczas próby zmiany hello toosave dla bramy sieci VPN hello w portalu Azure hello pojawi się następujący komunikat o błędzie hello:</span><span class="sxs-lookup"><span data-stu-id="da743-177">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span>

<span data-ttu-id="da743-178">**Brama sieci wirtualnej nie powiodło się toosave &lt;* nazwa bramy*&gt;.</span><span class="sxs-lookup"><span data-stu-id="da743-178">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="da743-179">Dane certyfikatu &lt; *certyfikatu identyfikator* &gt; jest invalid.* *</span><span class="sxs-lookup"><span data-stu-id="da743-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="da743-180">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="da743-180">Cause</span></span> 

<span data-ttu-id="da743-181">Ten problem może wystąpić, jeśli hello główny klucz publiczny certyfikatu, który został przekazany zawiera nieprawidłowy znak, takich jak miejsce.</span><span class="sxs-lookup"><span data-stu-id="da743-181">This problem might occur if hello root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="da743-182">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="da743-182">Solution</span></span>

<span data-ttu-id="da743-183">Upewnij się, że hello dane w certyfikacie hello nie zawiera nieprawidłowe znaki, takie jak podziały wiersza (znaki powrotu karetki).</span><span class="sxs-lookup"><span data-stu-id="da743-183">Make sure that hello data in hello certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="da743-184">Witaj całą wartość powinna być jeden długi wiersz.</span><span class="sxs-lookup"><span data-stu-id="da743-184">hello entire value should be one long line.</span></span> <span data-ttu-id="da743-185">powitania po tekst jest przykładem hello certyfikatu:</span><span class="sxs-lookup"><span data-stu-id="da743-185">hello following text is a sample of hello certificate:</span></span>

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a><span data-ttu-id="da743-186">Błąd portalu Azure: nie powiodło się bramy sieci VPN hello toosave i hello Nazwa zasobu jest nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="da743-186">Azure portal error: Failed toosave hello VPN gateway, and hello resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="da743-187">Objaw</span><span class="sxs-lookup"><span data-stu-id="da743-187">Symptom</span></span>

<span data-ttu-id="da743-188">Podczas próby zmiany hello toosave dla bramy sieci VPN hello w portalu Azure hello pojawi się następujący komunikat o błędzie hello:</span><span class="sxs-lookup"><span data-stu-id="da743-188">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span> 

<span data-ttu-id="da743-189">**Brama sieci wirtualnej nie powiodło się toosave &lt;* nazwa bramy*&gt;.</span><span class="sxs-lookup"><span data-stu-id="da743-189">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="da743-190">Nazwa zasobu &lt; *nazwę certyfikatu, spróbuj tooupload* &gt; jest nieprawidłowa **.</span><span class="sxs-lookup"><span data-stu-id="da743-190">Resource name &lt;*certificate name you try tooupload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="da743-191">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="da743-191">Cause</span></span>

<span data-ttu-id="da743-192">Ten problem występuje, ponieważ nazwa hello hello certyfikatu zawiera nieprawidłowy znak, takich jak miejsce.</span><span class="sxs-lookup"><span data-stu-id="da743-192">This problem occurs because hello name of hello certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="da743-193">Błąd portalu Azure: 503 błąd pobierania pliku pakietu sieci VPN</span><span class="sxs-lookup"><span data-stu-id="da743-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="da743-194">Objaw</span><span class="sxs-lookup"><span data-stu-id="da743-194">Symptom</span></span>

<span data-ttu-id="da743-195">Podczas próby pakietu klienta VPN toodownload hello w konfiguracji pojawi się następujący komunikat o błędzie hello:</span><span class="sxs-lookup"><span data-stu-id="da743-195">When you try toodownload hello VPN client configuration package, you receive hello following error message:</span></span>

<span data-ttu-id="da743-196">**Toodownload hello pliku nie powiodło się. Szczegóły błędu: błąd 503. Witaj serwer jest zajęty.**</span><span class="sxs-lookup"><span data-stu-id="da743-196">**Failed toodownload hello file. Error details: error 503. hello server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="da743-197">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="da743-197">Solution</span></span>

<span data-ttu-id="da743-198">Przyczyną tego błędu może być tymczasowy problem z siecią.</span><span class="sxs-lookup"><span data-stu-id="da743-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="da743-199">Spróbuj pakietu VPN hello toodownload ponownie za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="da743-199">Try toodownload hello VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a><span data-ttu-id="da743-200">Uaktualnianie programu Azure bramy sieci VPN: tooconnect są P2S wszystkich klientów</span><span class="sxs-lookup"><span data-stu-id="da743-200">Azure VPN Gateway upgrade: All P2S clients are unable tooconnect</span></span>

### <a name="cause"></a><span data-ttu-id="da743-201">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="da743-201">Cause</span></span>

<span data-ttu-id="da743-202">Jeśli certyfikat hello jest więcej niż 50% przez jego okres istnienia certyfikatu hello jest przerzuceniem.</span><span class="sxs-lookup"><span data-stu-id="da743-202">If hello certificate is more than 50 percent through its lifetime, hello certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="da743-203">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="da743-203">Solution</span></span>

<span data-ttu-id="da743-204">tooresolve ten problem, Utwórz i ponowne rozdzielanie nowych klientów sieci VPN toohello certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="da743-204">tooresolve this problem, create and redistribute new certificates toohello VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="da743-205">Zbyt wielu klientów sieci VPN na raz podłączone</span><span class="sxs-lookup"><span data-stu-id="da743-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="da743-206">Dla każdej bramy sieci VPN hello maksymalną liczbę dozwolonych połączeń to 128.</span><span class="sxs-lookup"><span data-stu-id="da743-206">For each VPN gateway, hello maximum number of allowable connections is 128.</span></span> <span data-ttu-id="da743-207">Całkowita liczba podłączonych klientów w portalu Azure hello hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="da743-207">You can see hello total number of connected clients in hello Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a><span data-ttu-id="da743-208">Sieć VPN punkt lokacja niepoprawnie dodaje trasę dla tabeli tras toohello 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="da743-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 toohello route table</span></span>

### <a name="symptom"></a><span data-ttu-id="da743-209">Objaw</span><span class="sxs-lookup"><span data-stu-id="da743-209">Symptom</span></span>

<span data-ttu-id="da743-210">Podczas wybierania hello połączenia sieci VPN na powitania klienta punkt lokacja powitania klienta sieci VPN należy dodać trasę kierunku hello sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="da743-210">When you dial hello VPN connection on hello point-to-site client, hello VPN client should add a route toward hello Azure virtual network.</span></span> <span data-ttu-id="da743-211">Usługa Pomocnika IP Hello należy dodać trasę dla podsieci hello hello klientów sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="da743-211">hello IP helper service should add a route for hello subnet of hello VPN clients.</span></span> 

<span data-ttu-id="da743-212">Hello zakresu klienta sieci VPN należy tooa mniejsze podsieci 10.0.0.0/8, takich jak 10.0.12.0/24.</span><span class="sxs-lookup"><span data-stu-id="da743-212">hello VPN client range belongs tooa smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="da743-213">Zamiast trasę 10.0.12.0/24 trasę dla 10.0.0.0/8 dodaniu, która ma wyższy priorytet.</span><span class="sxs-lookup"><span data-stu-id="da743-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="da743-214">Ta trasa niepoprawne dzieli łączności z pozostałych lokalnej sieci, które mogą należeć do podsieci tooanother w zakresie 10.0.0.0/8 hello, takich jak 10.50.0.0/24, które nie mają określoną trasę zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="da743-214">This incorrect route breaks connectivity with other on-premises networks that might belong tooanother subnet within hello 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="da743-215">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="da743-215">Cause</span></span>

<span data-ttu-id="da743-216">To zachowanie jest celowe w przypadku klientów z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="da743-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="da743-217">Gdy klient hello używa protokołu PPP IPCP hello, uzyskuje hello adres IP dla interfejsu tunelu hello z powitania serwera (hello bramy sieci VPN w tym przypadku).</span><span class="sxs-lookup"><span data-stu-id="da743-217">When hello client uses hello PPP IPCP protocol, it obtains hello IP address for hello tunnel interface from hello server (hello VPN gateway in this case).</span></span> <span data-ttu-id="da743-218">Jednak ze względu na ograniczenia w protokole hello powitania klienta nie ma hello maski podsieci.</span><span class="sxs-lookup"><span data-stu-id="da743-218">However, because of a limitation in hello protocol, hello client does not have hello subnet mask.</span></span> <span data-ttu-id="da743-219">Ponieważ nie istnieje żadne tooget sposób, powitania klienta próbuje maski podsieci hello tooguess oparte na powitania klasy adres IP interfejsu tunelu hello.</span><span class="sxs-lookup"><span data-stu-id="da743-219">Because there is no other way tooget it, hello client tries tooguess hello subnet mask based on hello class of hello tunnel interface IP address.</span></span> 

<span data-ttu-id="da743-220">W związku z tym trasę dodaje oparte na powitania po mapowania statyczne</span><span class="sxs-lookup"><span data-stu-id="da743-220">Therefore, a route is added based on hello following static mapping:</span></span> 

<span data-ttu-id="da743-221">Jeśli adres należy tooclass A--> Zastosuj /8</span><span class="sxs-lookup"><span data-stu-id="da743-221">If address belongs tooclass A --> apply /8</span></span>

<span data-ttu-id="da743-222">Jeśli adres należy tooclass--> B Zastosuj/16 do /</span><span class="sxs-lookup"><span data-stu-id="da743-222">If address belongs tooclass B --> apply /16</span></span>

<span data-ttu-id="da743-223">Jeśli adres należy tooclass C--> Zastosuj prefiksie/24</span><span class="sxs-lookup"><span data-stu-id="da743-223">If address belongs tooclass C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="da743-224">Klient sieci VPN nie może uzyskać dostępu udziałów plików sieciowych</span><span class="sxs-lookup"><span data-stu-id="da743-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="da743-225">Objaw</span><span class="sxs-lookup"><span data-stu-id="da743-225">Symptom</span></span>

<span data-ttu-id="da743-226">Klient sieci VPN Hello został podłączony toohello sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="da743-226">hello VPN client has connected toohello Azure virtual network.</span></span> <span data-ttu-id="da743-227">Jednak powitania klienta nie może uzyskać dostępu do udziałów sieciowych.</span><span class="sxs-lookup"><span data-stu-id="da743-227">However, hello client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="da743-228">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="da743-228">Cause</span></span>

<span data-ttu-id="da743-229">Witaj protokołu SMB służy do dostępu do udziału plików.</span><span class="sxs-lookup"><span data-stu-id="da743-229">hello SMB protocol is used for file share access.</span></span> <span data-ttu-id="da743-230">Po zainicjowaniu połączenia hello poświadczenia sesji hello dodaje powitania klienta sieci VPN i hello awarii.</span><span class="sxs-lookup"><span data-stu-id="da743-230">When hello connection is initiated, hello VPN client adds hello session credentials and hello failure occurs.</span></span> <span data-ttu-id="da743-231">Po nawiązaniu połączenia hello powitania klienta jest wymuszone toouse hello pamięci podręcznej poświadczeń dla uwierzytelniania Kerberos.</span><span class="sxs-lookup"><span data-stu-id="da743-231">After hello connection is established, hello client is forced toouse hello cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="da743-232">Ten proces jest inicjowany zapytania toohello Centrum dystrybucji kluczy (kontroler domeny) tooget tokenu.</span><span class="sxs-lookup"><span data-stu-id="da743-232">This process initiates queries toohello Key Distribution Center (a domain controller) tooget a token.</span></span> <span data-ttu-id="da743-233">Ponieważ hello klient nawiąże połączenie z hello Internet, może nie być kontrolera domeny hello tooreach stanie.</span><span class="sxs-lookup"><span data-stu-id="da743-233">Because hello client connects from hello Internet, it might not be able tooreach hello domain controller.</span></span> <span data-ttu-id="da743-234">W związku z tym powitania klienta nie może przełączyć się z tooNTLM protokołu Kerberos.</span><span class="sxs-lookup"><span data-stu-id="da743-234">Therefore, hello client cannot fail over from Kerberos tooNTLM.</span></span> 

<span data-ttu-id="da743-235">Hello tylko czasu klienta hello jest monitowany o poświadczenia jest, gdy ma prawidłowy certyfikat (z siecią SAN = nazwy UPN) wydanego przez toowhich domeny hello jest on dołączony.</span><span class="sxs-lookup"><span data-stu-id="da743-235">hello only time that hello client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by hello domain toowhich it is joined.</span></span> <span data-ttu-id="da743-236">również powitania klienta musi być fizycznie podłączone toohello sieci z domeną.</span><span class="sxs-lookup"><span data-stu-id="da743-236">hello client also must be physically connected toohello domain network.</span></span> <span data-ttu-id="da743-237">W takim przypadku hello klient próbuje toouse hello certyfikatów i przez nią miejsce osiągnie limit toohello kontrolera domeny.</span><span class="sxs-lookup"><span data-stu-id="da743-237">In this case, hello client tries toouse hello certificate and reaches out toohello domain controller.</span></span> <span data-ttu-id="da743-238">Następnie hello Centrum dystrybucji kluczy zwraca błąd "KDC_ERR_C_PRINCIPAL_UNKNOWN".</span><span class="sxs-lookup"><span data-stu-id="da743-238">Then hello Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="da743-239">powitania klienta jest wymuszone toofail tooNTLM.</span><span class="sxs-lookup"><span data-stu-id="da743-239">hello client is forced toofail over tooNTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="da743-240">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="da743-240">Solution</span></span>

<span data-ttu-id="da743-241">toowork wokół hello problem, wyłącz hello buforowanie poświadczeń domeny z powitania po podklucz rejestru:</span><span class="sxs-lookup"><span data-stu-id="da743-241">toowork around hello problem, disable hello caching of domain credentials from hello following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a><span data-ttu-id="da743-242">Nie można odnaleźć połączenia VPN punkt lokacja hello w systemie Windows przed ponowną instalację powitania klienta sieci VPN</span><span class="sxs-lookup"><span data-stu-id="da743-242">Cannot find hello point-to-site VPN connection in Windows after reinstalling hello VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="da743-243">Objaw</span><span class="sxs-lookup"><span data-stu-id="da743-243">Symptom</span></span>

<span data-ttu-id="da743-244">Usuń połączenie VPN punkt lokacja hello i ponownie zainstalować powitania klienta sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="da743-244">You remove hello point-to-site VPN connection and then reinstall hello VPN client.</span></span> <span data-ttu-id="da743-245">W takiej sytuacji nie skonfigurowano pomyślnie hello połączenia sieci VPN.</span><span class="sxs-lookup"><span data-stu-id="da743-245">In this situation, hello VPN connection is not configured successfully.</span></span> <span data-ttu-id="da743-246">Nie ma połączenie VPN hello hello **połączenia sieciowe** ustawienia systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="da743-246">You do not see hello VPN connection in hello **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="da743-247">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="da743-247">Solution</span></span>

<span data-ttu-id="da743-248">tooresolve hello problem, Usuń hello starego VPN plików konfiguracji klienta z **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, a następnie ponownie uruchom Instalatora klienta VPN hello.</span><span class="sxs-lookup"><span data-stu-id="da743-248">tooresolve hello problem, delete hello old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run hello VPN client installer again.</span></span>
