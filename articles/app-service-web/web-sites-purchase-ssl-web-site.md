---
title: "aaaAdd SSL certyfikatów tooyour aplikacji usługi Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd SSL certyfikatów tooyour aplikacji usługi app Service."
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="efcda-103">Kup i skonfiguruj certyfikat SSL dla usługi Azure App Service</span><span class="sxs-lookup"><span data-stu-id="efcda-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="efcda-104">W tym samouczku zostanie zabezpieczenia aplikacji sieci web po zakupie certyfikatu SSL dla Twojej  **[usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, bezpieczne przechowywanie ich w [usługi Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)i kojarzenie go z domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="efcda-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-tooazure"></a><span data-ttu-id="efcda-105">Krok 1 — Logowanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="efcda-105">Step 1 - Log in tooAzure</span></span>

<span data-ttu-id="efcda-106">Zaloguj się za toohello portalu Azure w http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="efcda-106">Log in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="efcda-107">Krok 2 — złóż zamówienie certyfikat SSL</span><span class="sxs-lookup"><span data-stu-id="efcda-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="efcda-108">Kolejność certyfikat SSL można umieścić przez utworzenie nowej [certyfikatu usługi aplikacji](https://portal.azure.com/#create/Microsoft.SSL) w hello **portalu Azure**.</span><span class="sxs-lookup"><span data-stu-id="efcda-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In hello **Azure portal**.</span></span>

![Tworzenie certyfikatu](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="efcda-110">Wprowadź przyjazną nazwę w polu **nazwa** certyfikatów dla ustawienia zabezpieczeń SSL, a następnie wprowadź hello **nazwy domeny**</span><span class="sxs-lookup"><span data-stu-id="efcda-110">Enter a friendly **Name** for your SSL certificate and enter hello **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="efcda-111">To jest jednym z najważniejszych części procesu zakupu hello hello.</span><span class="sxs-lookup"><span data-stu-id="efcda-111">This is one of hello most critical parts of hello purchase process.</span></span> <span data-ttu-id="efcda-112">Upewnij się, że tooenter Popraw nazwę hosta (domena niestandardowych), które mają tooprotect z tym certyfikatem.</span><span class="sxs-lookup"><span data-stu-id="efcda-112">Make sure tooenter correct host name (custom domain) that you want tooprotect with this certificate.</span></span> <span data-ttu-id="efcda-113">**NIE** Dołącz hello nazwy hosta z sieci Web.</span><span class="sxs-lookup"><span data-stu-id="efcda-113">**DO NOT** append hello Host name with WWW.</span></span> 
>

<span data-ttu-id="efcda-114">Wybierz użytkownika **subskrypcji**, **grupy zasobów**, i **certyfikatu jednostki SKU**</span><span class="sxs-lookup"><span data-stu-id="efcda-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="efcda-115">Certyfikaty usługi aplikacji można używać tylko przez inne usługi aplikacji w ramach hello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="efcda-115">App Service Certificates can only be used by other App Services within hello same subscription.</span></span>  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a><span data-ttu-id="efcda-116">Krok 3 — magazynu hello certyfikatu w magazynie kluczy Azure</span><span class="sxs-lookup"><span data-stu-id="efcda-116">Step 3 - Store hello certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="efcda-117">[Magazyn kluczy](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) jest usługą platformy Azure, która pomaga w zabezpieczaniu kluczy kryptograficznych i kluczy tajnych używanych przez usługi i aplikacje w chmurze.</span><span class="sxs-lookup"><span data-stu-id="efcda-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="efcda-118">Po zakończeniu hello zakupu certyfikatów SSL, należy tooopen [certyfikaty usługi aplikacji](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) bloku zasobów.</span><span class="sxs-lookup"><span data-stu-id="efcda-118">Once hello SSL Certificate purchase is complete, you need tooopen [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![Wstaw obraz gotowy toostore w KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="efcda-120">Można zauważyć, że stan certyfikatu jest **"Oczekujące wystawiania"** jako obejmuje kilka kroków więcej potrzebujesz toocomplete przed rozpoczęciem używania tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="efcda-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need toocomplete before you can start using this certificate.</span></span>

<span data-ttu-id="efcda-121">Kliknij przycisk **Konfiguracja certyfikatów** wewnątrz bloku właściwości certyfikatu, kliknij polecenie **krok 1: magazyn** toostore ten certyfikat w magazynie kluczy Azure.</span><span class="sxs-lookup"><span data-stu-id="efcda-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** toostore this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="efcda-122">Z **klucza magazynu stanu** bloku, kliknij przycisk **klucza magazynu repozytorium** toochoose istniejących toostore Key Vault tego certyfikatu **lub Utwórz nowy magazyn kluczy** toocreate nowy klucz magazynu w tej samej subskrypcji i grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="efcda-122">From **Key Vault Status** Blade, click **Key Vault Repository** toochoose an existing Key Vault toostore this certificate **OR Create New Key Vault** toocreate new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="efcda-123">Usługa Azure Key Vault ma minimalny opłat do przechowywania certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="efcda-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="efcda-124">Aby uzyskać więcej informacji, zobacz  **[szczegóły cennika usługi Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.</span><span class="sxs-lookup"><span data-stu-id="efcda-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="efcda-125">Po wybraniu hello toostore repozytorium magazynu klucza tego certyfikatu, hello **magazynu** opcji powinny być widoczne Powodzenie.</span><span class="sxs-lookup"><span data-stu-id="efcda-125">Once you have selected hello Key Vault Repository toostore this certificate in, hello **Store** option should show success.</span></span>

![Wstaw obraz sukcesu magazynu w KV](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a><span data-ttu-id="efcda-127">Krok 4. Sprawdź hello własność domeny</span><span class="sxs-lookup"><span data-stu-id="efcda-127">Step 4 - Verify hello Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="efcda-128">Istnieją trzy typy weryfikację domeny obsługiwane przez certyfikaty usługi aplikacji: domeny poczty, ręczne weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="efcda-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="efcda-129">Te omówiono bardziej szczegółowo w hello [zaawansowane sekcji](#advanced).</span><span class="sxs-lookup"><span data-stu-id="efcda-129">These are explained in more details in hello [Advanced section](#advanced).</span></span>

<span data-ttu-id="efcda-130">Z hello sam **Konfiguracja certyfikatów** bloku używane w kroku 3, kliknij przycisk **krok 2: Sprawdź**.</span><span class="sxs-lookup"><span data-stu-id="efcda-130">From hello same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="efcda-131">**Weryfikacja domeny** proces najodpowiedniejszym hello **tylko w przypadku** masz  **[zakupionych domeny niestandardowej z usługi aplikacji Azure.](custom-dns-web-site-buydomains-web-app.md)**</span><span class="sxs-lookup"><span data-stu-id="efcda-131">**Domain Verification** This is hello most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="efcda-132">Polecenie **Sprawdź** przycisk toocomplete ten krok.</span><span class="sxs-lookup"><span data-stu-id="efcda-132">Click on **Verify** button toocomplete this step.</span></span>

![Wstaw obraz weryfikację domeny](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="efcda-134">Po kliknięciu przycisku **Sprawdź**, użyj hello **Odśwież** przycisku do hello **Sprawdź** opcji powinny być widoczne Powodzenie.</span><span class="sxs-lookup"><span data-stu-id="efcda-134">After clicking **Verify**, use hello **Refresh** button until hello **Verify** option should show success.</span></span>

![Wstaw obraz sprawdzić, czy w KV](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a><span data-ttu-id="efcda-136">Krok 5 — przypisać tooApp certyfikatu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="efcda-136">Step 5 - Assign Certificate tooApp Service App</span></span>

> [!NOTE]
> <span data-ttu-id="efcda-137">Przed wykonaniem kroków hello w tej sekcji, muszą mieć skojarzone nazwy domeny niestandardowej z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="efcda-137">Before performing hello steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="efcda-138">Aby uzyskać więcej informacji, zobacz  **[Konfigurowanie niestandardowej nazwy domeny dla aplikacji sieci web.](app-service-web-tutorial-custom-domain.md)**</span><span class="sxs-lookup"><span data-stu-id="efcda-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="efcda-139">W hello  **[portalu Azure](https://portal.azure.com/)**, kliknij przycisk hello **usługi aplikacji** opcję na powitania po lewej stronie hello.</span><span class="sxs-lookup"><span data-stu-id="efcda-139">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="efcda-140">Kliknij nazwę hello toowhich Twojej aplikacji ma tooassign tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="efcda-140">Click hello name of your app toowhich you want tooassign this certificate.</span></span>

<span data-ttu-id="efcda-141">W hello **ustawienia**, kliknij przycisk **certyfikaty SSL**.</span><span class="sxs-lookup"><span data-stu-id="efcda-141">In hello **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="efcda-142">Kliknij przycisk **Importowanie certyfikatu usługi aplikacji** i hello wybierz certyfikat, które zostały zakupione.</span><span class="sxs-lookup"><span data-stu-id="efcda-142">Click **Import App Service Certificate** and select hello certificate that you just purchased.</span></span>

![Wstaw obraz Importowanie certyfikatu](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="efcda-144">W hello **powiązania ssl** sekcji kliknij na **dodać powiązania**, hello listę rozwijaną tooselect hello domeny nazwa toosecure za pomocą protokołu SSL i hello toouse certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="efcda-144">In hello **ssl bindings** section Click on **Add bindings**, and use hello dropdowns tooselect hello domain name toosecure with SSL, and hello certificate toouse.</span></span> <span data-ttu-id="efcda-145">Można również wybrać czy toouse  **[oznaczenia nazwy serwera (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  lub adresu IP na podstawie protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="efcda-145">You may also select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![Wstaw obraz z wiązaniami SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="efcda-147">Kliknij przycisk **Dodawanie powiązania** toosave hello zmian i Włącz protokół SSL.</span><span class="sxs-lookup"><span data-stu-id="efcda-147">Click **Add Binding** toosave hello changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="efcda-148">W przypadku wybrania **IP na podstawie SSL** i domeny niestandardowej jest konfigurowana przy użyciu rekordu A, musisz wykonać następujące dodatkowe kroki hello.</span><span class="sxs-lookup"><span data-stu-id="efcda-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps.</span></span> <span data-ttu-id="efcda-149">Te omówiono bardziej szczegółowo w hello [zaawansowane sekcji](#Advanced).</span><span class="sxs-lookup"><span data-stu-id="efcda-149">These are explained in more details in hello [Advanced section](#Advanced).</span></span>

<span data-ttu-id="efcda-150">W tym momencie możesz powinno być możliwe toovisit przy użyciu aplikacji `HTTPS://` zamiast `HTTP://` tooverify, który hello certyfikat został poprawnie skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="efcda-150">At this point, you should be able toovisit your app using `HTTPS://` instead of `HTTP://` tooverify that hello certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="efcda-151">Krok 6 — zadania związane z zarządzaniem</span><span class="sxs-lookup"><span data-stu-id="efcda-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="efcda-152">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="efcda-152">Azure CLI</span></span>

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a><span data-ttu-id="efcda-153">PowerShell</span><span class="sxs-lookup"><span data-stu-id="efcda-153">PowerShell</span></span>

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a><span data-ttu-id="efcda-154">Advanced</span><span class="sxs-lookup"><span data-stu-id="efcda-154">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="efcda-155">Weryfikowanie własność domeny</span><span class="sxs-lookup"><span data-stu-id="efcda-155">Verifying Domain Ownership</span></span>

<span data-ttu-id="efcda-156">Istnieją dwa typy więcej weryfikacji domeny obsługiwane przez certyfikaty usługi aplikacji: poczty i weryfikacja ręcznego.</span><span class="sxs-lookup"><span data-stu-id="efcda-156">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="efcda-157">Weryfikacja poczty</span><span class="sxs-lookup"><span data-stu-id="efcda-157">Mail Verification</span></span>

<span data-ttu-id="efcda-158">Weryfikacja e-mail została już wysłana toohello adresy E-mail skojarzony z tym domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="efcda-158">Verification email has already been sent toohello Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="efcda-159">Witaj toocomplete E-mail weryfikacji, otwórz hello poczty e-mail i kliknij łącze weryfikacji hello.</span><span class="sxs-lookup"><span data-stu-id="efcda-159">toocomplete hello Email verification step, open hello email and click hello verification link.</span></span>

![Wstaw obraz Weryfikacja adresu e-mail](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="efcda-161">Jeśli potrzebujesz tooresend hello weryfikacji w wiadomości e-mail, kliknij przycisk hello **ponowne wysyłanie wiadomości E-mail** przycisku.</span><span class="sxs-lookup"><span data-stu-id="efcda-161">If you need tooresend hello verification email, click hello **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="efcda-162">Weryfikacja ręczna</span><span class="sxs-lookup"><span data-stu-id="efcda-162">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efcda-163">HTML strony sieci Web weryfikacji (dotyczy tylko wersji Standard certyfikatu)</span><span class="sxs-lookup"><span data-stu-id="efcda-163">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="efcda-164">Utwórz plik HTML o nazwie **"starfield.html"**</span><span class="sxs-lookup"><span data-stu-id="efcda-164">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="efcda-165">Zawartość tego pliku powinna być hello dokładną nazwę hello domeny weryfikacji tokenu.</span><span class="sxs-lookup"><span data-stu-id="efcda-165">Content of this file should be hello exact name of hello Domain Verification Token.</span></span> <span data-ttu-id="efcda-166">(Możesz skopiować hello token z hello bloku stanu weryfikacji domeny)</span><span class="sxs-lookup"><span data-stu-id="efcda-166">(You can copy hello token from hello Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="efcda-167">Przekazywanie tego pliku w katalogu głównym powitania serwera sieci web hello hosting domeny`/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="efcda-167">Upload this file at hello root of hello web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="efcda-168">Kliknij przycisk **Odśwież** tooupdate stanu certyfikatu powitania po zakończeniu weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="efcda-168">Click **Refresh** tooupdate hello certificate status after verification is completed.</span></span> <span data-ttu-id="efcda-169">Może upłynąć kilka minut, aż toocomplete weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="efcda-169">It might take few minutes for verification toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="efcda-170">Sprawdź, czy w terminalu przy użyciu `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello odpowiedź powinna zawierać hello `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="efcda-170">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello response should contain hello `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="efcda-171">Weryfikacja rekordu DNS TXT</span><span class="sxs-lookup"><span data-stu-id="efcda-171">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="efcda-172">Korzystanie z Menedżera DNS utworzyć rekord TXT na powitania `@` poddomeny z domeny weryfikacji tokenu toohello takie same wartości.</span><span class="sxs-lookup"><span data-stu-id="efcda-172">Using your DNS manager, Create a TXT record on hello `@` subdomain with value equal toohello Domain Verification Token.</span></span>
1. <span data-ttu-id="efcda-173">Kliknij przycisk **"Odśwież"** tooupdate hello stanu certyfikatu po zakończeniu weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="efcda-173">Click **“Refresh”** tooupdate hello Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="efcda-174">Należy toocreate rekord TXT na `@.<domain>` o wartości `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="efcda-174">You need toocreate a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-tooapp-service-app"></a><span data-ttu-id="efcda-175">Przypisz tooApp certyfikatu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="efcda-175">Assign Certificate tooApp Service App</span></span>

<span data-ttu-id="efcda-176">W przypadku wybrania **IP na podstawie SSL** i domeny niestandardowej jest konfigurowana przy użyciu rekordu A, musisz wykonać następujące dodatkowe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="efcda-176">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps:</span></span>

<span data-ttu-id="efcda-177">Po skonfigurowaniu adresów IP na podstawie powiązania SSL, dedykowany adres IP jest przypisany tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="efcda-177">After you have configured an IP based SSL binding, a dedicated IP address is assigned tooyour app.</span></span> <span data-ttu-id="efcda-178">Ten adres IP można znaleźć na powitania **domeny niestandardowe** w obszarze Ustawienia aplikacji, nad hello **Hostnames** sekcji.</span><span class="sxs-lookup"><span data-stu-id="efcda-178">You can find this IP address on hello **Custom domain** page under settings of your app, right above hello **Hostnames** section.</span></span> <span data-ttu-id="efcda-179">Jest on wyświetlany jako **zewnętrzny adres IP**</span><span class="sxs-lookup"><span data-stu-id="efcda-179">It is listed as **External IP Address**</span></span>

![Wstaw obraz z protokołu SSL z adresu IP](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="efcda-181">Należy pamiętać, że ten adres IP jest inny niż hello wirtualnego adresu IP używane wcześniej rekord A hello tooconfigure dla danej domeny.</span><span class="sxs-lookup"><span data-stu-id="efcda-181">Note that this IP address is different than hello virtual IP address used previously tooconfigure hello A record for your domain.</span></span> <span data-ttu-id="efcda-182">Jeśli są skonfigurowane toouse SNI na podstawie protokołu SSL lub nie są skonfigurowane toouse SSL, żaden adres jest wymienionych dla tego wpisu.</span><span class="sxs-lookup"><span data-stu-id="efcda-182">If you are configured toouse SNI based SSL, or are not configured toouse SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="efcda-183">Za pomocą narzędzi hello dostarczonych przez rejestratora nazw domen, zmodyfikuj hello rekordu adresu IP toohello toopoint nazwy domeny niestandardowej hello w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="efcda-183">Using hello tools provided by your domain name registrar, modify hello A record for your custom domain name toopoint toohello IP address from hello previous step.</span></span>

## <a name="rekey-and-sync-hello-certificate"></a><span data-ttu-id="efcda-184">Ponowne tworzenie klucza i zsynchronizuj hello certyfikatu</span><span class="sxs-lookup"><span data-stu-id="efcda-184">Rekey and Sync hello Certificate</span></span>

<span data-ttu-id="efcda-185">Jeśli kiedykolwiek zajdzie tooRekey certyfikat, wybierz **ponowne tworzenie klucza i zsynchronizuj** opcję **właściwości certyfikatu** bloku.</span><span class="sxs-lookup"><span data-stu-id="efcda-185">If you ever need tooRekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="efcda-186">Kliknij przycisk **ponowne tworzenie klucza** przycisk tooinitiate hello procesu.</span><span class="sxs-lookup"><span data-stu-id="efcda-186">Click **Rekey** Button tooinitiate hello process.</span></span> <span data-ttu-id="efcda-187">Ten proces może potrwać toocomplete 1 – 10 minut.</span><span class="sxs-lookup"><span data-stu-id="efcda-187">This process can take 1-10 minutes toocomplete.</span></span>

![Wstaw obraz ponowne tworzenie klucza protokołu SSL](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="efcda-189">Ponowne tworzenie klucza certyfikatu przedstawia hello certyfikatu przy użyciu nowego certyfikatu wystawionego przez urząd certyfikacji hello.</span><span class="sxs-lookup"><span data-stu-id="efcda-189">Rekeying your certificate rolls hello certificate with a new certificate issued from hello certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efcda-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="efcda-190">Next Steps</span></span>

* [<span data-ttu-id="efcda-191">Dodawanie sieci dostarczania zawartości</span><span class="sxs-lookup"><span data-stu-id="efcda-191">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)