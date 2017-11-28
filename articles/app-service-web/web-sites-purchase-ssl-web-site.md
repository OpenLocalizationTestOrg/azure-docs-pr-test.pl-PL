---
title: "Dodawanie certyfikatu SSL do aplikacji usługi Azure App Service | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dodać certyfikat SSL do aplikację usługi aplikacji."
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
ms.openlocfilehash: 191dd7240ad15b4936a72bc27a2d0162350f3afb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="1b32a-103">Kup i skonfiguruj certyfikat SSL dla usługi Azure App Service</span><span class="sxs-lookup"><span data-stu-id="1b32a-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="1b32a-104">W tym samouczku zostanie zabezpieczenia aplikacji sieci web po zakupie certyfikatu SSL dla Twojej  **[usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, bezpieczne przechowywanie ich w [usługi Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)i kojarzenie go z domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="1b32a-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-to-azure"></a><span data-ttu-id="1b32a-105">Krok 1 — Logowanie do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1b32a-105">Step 1 - Log in to Azure</span></span>

<span data-ttu-id="1b32a-106">Zaloguj się do portalu Azure pod adresem http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="1b32a-106">Log in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="1b32a-107">Krok 2 — złóż zamówienie certyfikat SSL</span><span class="sxs-lookup"><span data-stu-id="1b32a-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="1b32a-108">Kolejność certyfikat SSL można umieścić przez utworzenie nowej [certyfikatu usługi aplikacji](https://portal.azure.com/#create/Microsoft.SSL) w **portalu Azure**.</span><span class="sxs-lookup"><span data-stu-id="1b32a-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In the **Azure portal**.</span></span>

![Tworzenie certyfikatu](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="1b32a-110">Wprowadź przyjazną nazwę w polu **nazwa** certyfikatów dla ustawienia zabezpieczeń SSL, a następnie wprowadź **nazwy domeny**</span><span class="sxs-lookup"><span data-stu-id="1b32a-110">Enter a friendly **Name** for your SSL certificate and enter the **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="1b32a-111">To jest jednym z najważniejszych części procesu zakupu.</span><span class="sxs-lookup"><span data-stu-id="1b32a-111">This is one of the most critical parts of the purchase process.</span></span> <span data-ttu-id="1b32a-112">Upewnij się wprowadzić poprawną nazwę hosta (domena niestandardowych), który chcesz chronić za pomocą tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1b32a-112">Make sure to enter correct host name (custom domain) that you want to protect with this certificate.</span></span> <span data-ttu-id="1b32a-113">**NIE** Dołącz nazwy hosta z sieci Web.</span><span class="sxs-lookup"><span data-stu-id="1b32a-113">**DO NOT** append the Host name with WWW.</span></span> 
>

<span data-ttu-id="1b32a-114">Wybierz użytkownika **subskrypcji**, **grupy zasobów**, i **certyfikatu jednostki SKU**</span><span class="sxs-lookup"><span data-stu-id="1b32a-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="1b32a-115">Certyfikaty usługi aplikacji można używać tylko w innych usługach aplikacji w ramach tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1b32a-115">App Service Certificates can only be used by other App Services within the same subscription.</span></span>  
>

## <a name="step-3---store-the-certificate-in-azure-key-vault"></a><span data-ttu-id="1b32a-116">Krok 3 — magazyn certyfikatów w usłudze Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="1b32a-116">Step 3 - Store the certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="1b32a-117">[Magazyn kluczy](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) jest usługą platformy Azure, która pomaga w zabezpieczaniu kluczy kryptograficznych i kluczy tajnych używanych przez usługi i aplikacje w chmurze.</span><span class="sxs-lookup"><span data-stu-id="1b32a-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="1b32a-118">Po zakończeniu zakupu certyfikatów SSL, należy otworzyć [certyfikaty usługi aplikacji](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) bloku zasobów.</span><span class="sxs-lookup"><span data-stu-id="1b32a-118">Once the SSL Certificate purchase is complete, you need to open [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![Wstaw obraz gotowy do przechowywania w KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="1b32a-120">Można zauważyć, że stan certyfikatu jest **"Oczekujące wystawiania"** są kilka więcej czynności należy wykonać przed rozpoczęciem używania tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1b32a-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need to complete before you can start using this certificate.</span></span>

<span data-ttu-id="1b32a-121">Kliknij przycisk **Konfiguracja certyfikatów** wewnątrz bloku właściwości certyfikatu, kliknij polecenie **krok 1: przechowywanie** do przechowywania ten certyfikat w magazynie kluczy Azure.</span><span class="sxs-lookup"><span data-stu-id="1b32a-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** to store this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="1b32a-122">Z **klucza magazynu stanu** bloku, kliknij przycisk **klucza magazynu repozytorium** wybrać istniejącego magazynu kluczy w tym certyfikatem **lub Utwórz nowy magazyn kluczy** Aby utworzyć nowy magazyn kluczy w tej samej subskrypcji i grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="1b32a-122">From **Key Vault Status** Blade, click **Key Vault Repository** to choose an existing Key Vault to store this certificate **OR Create New Key Vault** to create new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="1b32a-123">Usługa Azure Key Vault ma minimalny opłat do przechowywania certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1b32a-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="1b32a-124">Aby uzyskać więcej informacji, zobacz  **[szczegóły cennika usługi Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.</span><span class="sxs-lookup"><span data-stu-id="1b32a-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="1b32a-125">Po wybraniu klucza repozytorium magazynu do przechowywania tego certyfikatu, **przechowywania** opcji powinny być widoczne Powodzenie.</span><span class="sxs-lookup"><span data-stu-id="1b32a-125">Once you have selected the Key Vault Repository to store this certificate in, the **Store** option should show success.</span></span>

![Wstaw obraz sukcesu magazynu w KV](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-the-domain-ownership"></a><span data-ttu-id="1b32a-127">Krok 4. Zweryfikuj prawo własności do domeny</span><span class="sxs-lookup"><span data-stu-id="1b32a-127">Step 4 - Verify the Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="1b32a-128">Istnieją trzy typy weryfikację domeny obsługiwane przez certyfikaty usługi aplikacji: domeny poczty, ręczne weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="1b32a-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="1b32a-129">Te omówiono bardziej szczegółowo w [zaawansowane sekcji](#advanced).</span><span class="sxs-lookup"><span data-stu-id="1b32a-129">These are explained in more details in the [Advanced section](#advanced).</span></span>

<span data-ttu-id="1b32a-130">Z tej samej **Konfiguracja certyfikatów** bloku używane w kroku 3, kliknij przycisk **krok 2: Sprawdź**.</span><span class="sxs-lookup"><span data-stu-id="1b32a-130">From the same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="1b32a-131">**Weryfikacja domeny** to polega na najbardziej odpowiednim **tylko jeśli** masz  **[zostały zakupione domeny niestandardowej w usłudze Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span><span class="sxs-lookup"><span data-stu-id="1b32a-131">**Domain Verification** This is the most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="1b32a-132">Polecenie **Sprawdź** przycisk, aby ukończyć ten krok.</span><span class="sxs-lookup"><span data-stu-id="1b32a-132">Click on **Verify** button to complete this step.</span></span>

![Wstaw obraz weryfikację domeny](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="1b32a-134">Po kliknięciu przycisku **Sprawdź**, użyj **Odśwież** przycisku do **Sprawdź** opcji powinny być widoczne Powodzenie.</span><span class="sxs-lookup"><span data-stu-id="1b32a-134">After clicking **Verify**, use the **Refresh** button until the **Verify** option should show success.</span></span>

![Wstaw obraz sprawdzić, czy w KV](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-to-app-service-app"></a><span data-ttu-id="1b32a-136">Krok 5. certyfikat Przypisz do aplikacji usługi App Service</span><span class="sxs-lookup"><span data-stu-id="1b32a-136">Step 5 - Assign Certificate to App Service App</span></span>

> [!NOTE]
> <span data-ttu-id="1b32a-137">Przed wykonaniem kroków w tej sekcji, muszą mieć skojarzone nazwy domeny niestandardowej z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="1b32a-137">Before performing the steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="1b32a-138">Aby uzyskać więcej informacji, zobacz  **[Konfigurowanie niestandardowej nazwy domeny dla aplikacji sieci web.](app-service-web-tutorial-custom-domain.md)**</span><span class="sxs-lookup"><span data-stu-id="1b32a-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="1b32a-139">W  **[portalu Azure](https://portal.azure.com/)**, kliknij przycisk **usługi aplikacji** opcję z lewej strony.</span><span class="sxs-lookup"><span data-stu-id="1b32a-139">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="1b32a-140">Kliknij nazwę aplikacji, do której chcesz przypisać ten certyfikat.</span><span class="sxs-lookup"><span data-stu-id="1b32a-140">Click the name of your app to which you want to assign this certificate.</span></span>

<span data-ttu-id="1b32a-141">W **ustawienia**, kliknij przycisk **certyfikaty SSL**.</span><span class="sxs-lookup"><span data-stu-id="1b32a-141">In the **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="1b32a-142">Kliknij przycisk **Importowanie certyfikatu usługi aplikacji** i wybierz certyfikat, który można zakupić.</span><span class="sxs-lookup"><span data-stu-id="1b32a-142">Click **Import App Service Certificate** and select the certificate that you just purchased.</span></span>

![Wstaw obraz Importowanie certyfikatu](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="1b32a-144">W **powiązania ssl** sekcji kliknij na **dodać powiązania**i wybierz nazwę domeny, aby zabezpieczyć za pomocą protokołu SSL i certyfikatu do użycia przy użyciu list rozwijanych.</span><span class="sxs-lookup"><span data-stu-id="1b32a-144">In the **ssl bindings** section Click on **Add bindings**, and use the dropdowns to select the domain name to secure with SSL, and the certificate to use.</span></span> <span data-ttu-id="1b32a-145">Można również wybrać opcję korzystania  **[oznaczenia nazwy serwera (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  lub adresu IP na podstawie protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="1b32a-145">You may also select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![Wstaw obraz z wiązaniami SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="1b32a-147">Kliknij przycisk **Dodawanie powiązania** Aby zapisać zmiany i Włącz protokół SSL.</span><span class="sxs-lookup"><span data-stu-id="1b32a-147">Click **Add Binding** to save the changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="1b32a-148">W przypadku wybrania **IP na podstawie SSL** i domeny niestandardowej jest konfigurowana przy użyciu rekordu A, musisz wykonać następujące dodatkowe czynności.</span><span class="sxs-lookup"><span data-stu-id="1b32a-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps.</span></span> <span data-ttu-id="1b32a-149">Te omówiono bardziej szczegółowo w [zaawansowane sekcji](#Advanced).</span><span class="sxs-lookup"><span data-stu-id="1b32a-149">These are explained in more details in the [Advanced section](#Advanced).</span></span>

<span data-ttu-id="1b32a-150">W tym momencie powinno być możliwe do odwiedzenia przy użyciu aplikacji `HTTPS://` zamiast `HTTP://` Aby sprawdzić, czy certyfikat został poprawnie skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="1b32a-150">At this point, you should be able to visit your app using `HTTPS://` instead of `HTTP://` to verify that the certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="1b32a-151">Krok 6 — zadania związane z zarządzaniem</span><span class="sxs-lookup"><span data-stu-id="1b32a-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="1b32a-152">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1b32a-152">Azure CLI</span></span>

<span data-ttu-id="1b32a-153">[!code-azurecli[główne](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "wiązania niestandardowego certyfikatu SSL w aplikacji sieci web")]</span><span class="sxs-lookup"><span data-stu-id="1b32a-153">[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span> 

### <a name="powershell"></a><span data-ttu-id="1b32a-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b32a-154">PowerShell</span></span>

<span data-ttu-id="1b32a-155">[!code-powershell[główne](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "wiązania niestandardowego certyfikatu SSL w aplikacji sieci web")]</span><span class="sxs-lookup"><span data-stu-id="1b32a-155">[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]</span></span>

## <a name="advanced"></a><span data-ttu-id="1b32a-156">Advanced</span><span class="sxs-lookup"><span data-stu-id="1b32a-156">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="1b32a-157">Weryfikowanie własność domeny</span><span class="sxs-lookup"><span data-stu-id="1b32a-157">Verifying Domain Ownership</span></span>

<span data-ttu-id="1b32a-158">Istnieją dwa typy więcej weryfikacji domeny obsługiwane przez certyfikaty usługi aplikacji: poczty i weryfikacja ręcznego.</span><span class="sxs-lookup"><span data-stu-id="1b32a-158">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="1b32a-159">Weryfikacja poczty</span><span class="sxs-lookup"><span data-stu-id="1b32a-159">Mail Verification</span></span>

<span data-ttu-id="1b32a-160">Weryfikacja e-mail została już wysłana na adresy E-mail skojarzony z tym domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="1b32a-160">Verification email has already been sent to the Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="1b32a-161">Aby ukończyć proces weryfikacji wiadomości E-mail, otwórz wiadomości e-mail i kliknij łącze weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="1b32a-161">To complete the Email verification step, open the email and click the verification link.</span></span>

![Wstaw obraz Weryfikacja adresu e-mail](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="1b32a-163">Jeśli konieczne jest ponowne wysłanie wiadomości e-mail weryfikacji, kliknij przycisk **ponowne wysłanie wiadomości E-mail** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1b32a-163">If you need to resend the verification email, click the **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="1b32a-164">Weryfikacja ręczna</span><span class="sxs-lookup"><span data-stu-id="1b32a-164">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b32a-165">HTML strony sieci Web weryfikacji (dotyczy tylko wersji Standard certyfikatu)</span><span class="sxs-lookup"><span data-stu-id="1b32a-165">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="1b32a-166">Utwórz plik HTML o nazwie **"starfield.html"**</span><span class="sxs-lookup"><span data-stu-id="1b32a-166">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="1b32a-167">Zawartość tego pliku powinna być dokładną nazwę domeny weryfikacji tokenu.</span><span class="sxs-lookup"><span data-stu-id="1b32a-167">Content of this file should be the exact name of the Domain Verification Token.</span></span> <span data-ttu-id="1b32a-168">(Możesz skopiować token z bloku stanu weryfikacji domeny)</span><span class="sxs-lookup"><span data-stu-id="1b32a-168">(You can copy the token from the Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="1b32a-169">Przekazywanie tego pliku w katalogu głównym serwera sieci web hosting domeny`/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="1b32a-169">Upload this file at the root of the web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="1b32a-170">Kliknij przycisk **Odśwież** można zaktualizować stanu certyfikatu po zakończeniu weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="1b32a-170">Click **Refresh** to update the certificate status after verification is completed.</span></span> <span data-ttu-id="1b32a-171">Może upłynąć kilka minut, aż weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="1b32a-171">It might take few minutes for verification to complete.</span></span>

> [!TIP]
> <span data-ttu-id="1b32a-172">Sprawdź, czy w terminalu przy użyciu `curl -G http://<domain>/.well-known/pki-validation/starfield.html` odpowiedź powinna zawierać `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="1b32a-172">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` the response should contain the `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="1b32a-173">Weryfikacja rekordu DNS TXT</span><span class="sxs-lookup"><span data-stu-id="1b32a-173">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="1b32a-174">Korzystanie z Menedżera DNS utworzyć rekord TXT na `@` poddomeny o wartości równej tokenu weryfikacji domeny.</span><span class="sxs-lookup"><span data-stu-id="1b32a-174">Using your DNS manager, Create a TXT record on the `@` subdomain with value equal to the Domain Verification Token.</span></span>
1. <span data-ttu-id="1b32a-175">Kliknij przycisk **"Odśwież"** można zaktualizować stanu certyfikatu po zakończeniu weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="1b32a-175">Click **“Refresh”** to update the Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="1b32a-176">Należy utworzyć rekord TXT na `@.<domain>` o wartości `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="1b32a-176">You need to create a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-to-app-service-app"></a><span data-ttu-id="1b32a-177">Przypisania certyfikatu do aplikacji usługi App Service</span><span class="sxs-lookup"><span data-stu-id="1b32a-177">Assign Certificate to App Service App</span></span>

<span data-ttu-id="1b32a-178">W przypadku wybrania **IP na podstawie SSL** i domeny niestandardowej jest konfigurowana przy użyciu rekordu A, musisz wykonać następujące dodatkowe czynności:</span><span class="sxs-lookup"><span data-stu-id="1b32a-178">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps:</span></span>

<span data-ttu-id="1b32a-179">Po skonfigurowaniu adresów IP na podstawie powiązania SSL, dedykowany adres IP jest przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b32a-179">After you have configured an IP based SSL binding, a dedicated IP address is assigned to your app.</span></span> <span data-ttu-id="1b32a-180">Ten adres IP można znaleźć w **domeny niestandardowe** strony w obszarze Ustawienia aplikacji, nad **Hostnames** sekcji.</span><span class="sxs-lookup"><span data-stu-id="1b32a-180">You can find this IP address on the **Custom domain** page under settings of your app, right above the **Hostnames** section.</span></span> <span data-ttu-id="1b32a-181">Jest on wyświetlany jako **zewnętrzny adres IP**</span><span class="sxs-lookup"><span data-stu-id="1b32a-181">It is listed as **External IP Address**</span></span>

![Wstaw obraz z protokołu SSL z adresu IP](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="1b32a-183">Należy pamiętać, że ten adres IP jest inny niż wirtualny adres IP wcześniej użyty do skonfigurowania rekordu A dla domeny.</span><span class="sxs-lookup"><span data-stu-id="1b32a-183">Note that this IP address is different than the virtual IP address used previously to configure the A record for your domain.</span></span> <span data-ttu-id="1b32a-184">Jeśli są skonfigurowane do używania SNI na podstawie protokołu SSL lub nie są skonfigurowane do używania protokołu SSL, żaden adres jest wymienionych dla tego wpisu.</span><span class="sxs-lookup"><span data-stu-id="1b32a-184">If you are configured to use SNI based SSL, or are not configured to use SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="1b32a-185">Korzystając z narzędzi dostarczanych przez rejestratora nazw domen, zmodyfikuj rekordu A dla nazwy domeny niestandardowe wskazywał adres IP z poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="1b32a-185">Using the tools provided by your domain name registrar, modify the A record for your custom domain name to point to the IP address from the previous step.</span></span>

## <a name="rekey-and-sync-the-certificate"></a><span data-ttu-id="1b32a-186">Ponowne tworzenie klucza i zsynchronizować certyfikatu</span><span class="sxs-lookup"><span data-stu-id="1b32a-186">Rekey and Sync the Certificate</span></span>

<span data-ttu-id="1b32a-187">Jeśli trzeba będzie ponowne tworzenie klucza certyfikatu, zaznacz **ponowne tworzenie klucza i zsynchronizuj** opcję **właściwości certyfikatu** bloku.</span><span class="sxs-lookup"><span data-stu-id="1b32a-187">If you ever need to Rekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="1b32a-188">Kliknij przycisk **ponowne tworzenie klucza** przycisk, aby zainicjować proces.</span><span class="sxs-lookup"><span data-stu-id="1b32a-188">Click **Rekey** Button to initiate the process.</span></span> <span data-ttu-id="1b32a-189">Może to potrwać 1 – 10 minut.</span><span class="sxs-lookup"><span data-stu-id="1b32a-189">This process can take 1-10 minutes to complete.</span></span>

![Wstaw obraz ponowne tworzenie klucza protokołu SSL](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="1b32a-191">Ponowne tworzenie klucza certyfikatu przedstawia certyfikat przy użyciu nowego certyfikatu wystawionego przez urząd certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="1b32a-191">Rekeying your certificate rolls the certificate with a new certificate issued from the certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b32a-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1b32a-192">Next Steps</span></span>

* [<span data-ttu-id="1b32a-193">Dodawanie sieci dostarczania zawartości</span><span class="sxs-lookup"><span data-stu-id="1b32a-193">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)