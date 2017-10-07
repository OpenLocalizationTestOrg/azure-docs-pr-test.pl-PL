---
title: "aaaConfigure protokołu SSL dla usługi w chmurze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toospecify punkt końcowy HTTPS dla roli sieci web i jak tooupload SSL certyfikatów toosecure aplikacji. Poniższe przykłady użycia hello portalu Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: b19283bb7b0e95374f2ae9c3532eb1effc7d6a9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="67147-104">Konfigurowanie protokołu SSL dla aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="67147-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="67147-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="67147-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="67147-106">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="67147-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="67147-107">Metoda zabezpieczania danych przesyłanych między hello hello najczęściej używane jest szyfrowanie Secure Socket Layer (SSL) internet.</span><span class="sxs-lookup"><span data-stu-id="67147-107">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="67147-108">To zadanie typowe omówiono sposób toospecify punkt końcowy HTTPS dla roli sieci web i jak tooupload SSL certyfikatów toosecure aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67147-108">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="67147-109">Usługi w chmurze tooAzure; Zastosuj Hello procedur w tym zadaniu dla usług aplikacji, zobacz [to](../app-service-web/web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="67147-109">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="67147-110">To zadanie używa wdrożenia produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="67147-110">This task uses a production deployment.</span></span> <span data-ttu-id="67147-111">Informacji na temat używania tymczasowej wdrożenia znajduje się na powitania na końcu tego tematu.</span><span class="sxs-lookup"><span data-stu-id="67147-111">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="67147-112">Odczyt [to](cloud-services-how-to-create-deploy-portal.md) pierwszy, jeśli nie utworzono jeszcze usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="67147-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="67147-113">Krok 1: Uzyskiwanie certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="67147-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="67147-114">tooconfigure protokołu SSL dla aplikacji, należy najpierw tooget certyfikat SSL, który został podpisany przez urząd certyfikacji, zaufanych innej firmy, który wystawia certyfikaty w tym celu.</span><span class="sxs-lookup"><span data-stu-id="67147-114">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="67147-115">Jeśli nie masz już jeden, należy tooobtain jedną z firmy, która sprzedaje certyfikatów SSL.</span><span class="sxs-lookup"><span data-stu-id="67147-115">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="67147-116">Hello certyfikatu musi spełniać następujące wymagania dotyczące certyfikatów SSL na platformie Azure hello:</span><span class="sxs-lookup"><span data-stu-id="67147-116">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="67147-117">Witaj, certyfikat musi zawierać klucz prywatny.</span><span class="sxs-lookup"><span data-stu-id="67147-117">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="67147-118">Witaj certyfikatu musi zostać utworzony dla wymiany kluczy, można eksportować tooa plik wymiany informacji osobistych (pfx).</span><span class="sxs-lookup"><span data-stu-id="67147-118">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="67147-119">Hello nazwa podmiotu certyfikatu musi odpowiadać usługi hello tooaccess hello domeny użytej w chmurze.</span><span class="sxs-lookup"><span data-stu-id="67147-119">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="67147-120">Nie można uzyskać certyfikatu SSL z urzędu certyfikacji (CA) dla domeny cloudapp.net hello.</span><span class="sxs-lookup"><span data-stu-id="67147-120">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="67147-121">Należy uzyskać toouse nazwy domeny niestandardowej podczas dostępu usługi.</span><span class="sxs-lookup"><span data-stu-id="67147-121">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="67147-122">Podczas żądania certyfikatu z urzędu certyfikacji, nazwa podmiotu certyfikatu hello musi odpowiadać hello domenę niestandardową nazwę używaną tooaccess aplikacji.</span><span class="sxs-lookup"><span data-stu-id="67147-122">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="67147-123">Na przykład jeśli nazwą domeny niestandardowej jest **contoso.com** może zażądać certyfikatu od urzędu certyfikacji dla ***. contoso.com** lub **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="67147-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="67147-124">Witaj certyfikatu należy użyć co najmniej 2048-bitowego szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="67147-124">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="67147-125">Do celów testowych możesz [utworzyć](cloud-services-certs-create.md) i użycia certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="67147-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="67147-126">Certyfikatu z podpisem własnym nie jest uwierzytelniony za pośrednictwem urzędu certyfikacji i używać jako adres URL witryny sieci Web hello hello cloudapp.net domeny.</span><span class="sxs-lookup"><span data-stu-id="67147-126">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="67147-127">Na przykład hello następujące zadanie używa certyfikatu z podpisem własnym w których hello jest nazwa pospolita (CN) używane w certyfikacie hello **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="67147-127">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="67147-128">Następnie musi zawierać informacje o certyfikacie hello w definicji usługi oraz pliki konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="67147-128">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="67147-129"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="67147-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="67147-130">Krok 2: Modyfikowanie plików definicji i konfiguracji usługi hello</span><span class="sxs-lookup"><span data-stu-id="67147-130">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="67147-131">Aplikacja musi być skonfigurowany toouse hello certyfikatu, a punkt końcowy HTTPS muszą zostać dodane.</span><span class="sxs-lookup"><span data-stu-id="67147-131">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="67147-132">W związku z tym hello definicji usługi i pliki konfiguracji usługi wymagają toobe aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="67147-132">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="67147-133">W środowisku projektowania, otwórz plik definicji hello usługi (CSDEF), Dodaj **certyfikaty** sekcji w hello **sieć Web** sekcji, a obejmują hello następujących informacji certyfikat (i certyfikaty pośrednie):</span><span class="sxs-lookup"><span data-stu-id="67147-133">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   <span data-ttu-id="67147-134">Witaj **certyfikaty** sekcja definiuje nazwę hello naszych certyfikatu, jego lokalizację i nazwę hello magazynu hello, w którym znajduje się.</span><span class="sxs-lookup"><span data-stu-id="67147-134">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>

   <span data-ttu-id="67147-135">Uprawnienia (`permisionLevel` atrybutów) mogą być tooone zestawu z hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="67147-135">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>

   | <span data-ttu-id="67147-136">Wartość uprawnienia</span><span class="sxs-lookup"><span data-stu-id="67147-136">Permission Value</span></span> | <span data-ttu-id="67147-137">Opis</span><span class="sxs-lookup"><span data-stu-id="67147-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="67147-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="67147-138">limitedOrElevated</span></span> |<span data-ttu-id="67147-139">**(Ustawienie domyślne)**  Wszystkie procesy roli można uzyskać dostępu do klucza prywatnego hello.</span><span class="sxs-lookup"><span data-stu-id="67147-139">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="67147-140">z podwyższonym poziomem uprawnień</span><span class="sxs-lookup"><span data-stu-id="67147-140">elevated</span></span> |<span data-ttu-id="67147-141">Tylko procesów z podwyższonym poziomem uprawnień można uzyskać dostępu do klucza prywatnego hello.</span><span class="sxs-lookup"><span data-stu-id="67147-141">Only elevated processes can access hello private key.</span></span> |

2. <span data-ttu-id="67147-142">W pliku definicji usługi, dodać **InputEndpoint** elementu w obrębie hello **punkty końcowe** sekcji tooenable HTTPS:</span><span class="sxs-lookup"><span data-stu-id="67147-142">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443"
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. <span data-ttu-id="67147-143">W pliku definicji usługi, dodać **powiązanie** elementu w obrębie hello **witryny** sekcji.</span><span class="sxs-lookup"><span data-stu-id="67147-143">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="67147-144">Ten element dodaje toomap powiązanie HTTPS lokacji tooyour punktu końcowego:</span><span class="sxs-lookup"><span data-stu-id="67147-144">This element adds an HTTPS binding toomap the endpoint tooyour site:</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```

   <span data-ttu-id="67147-145">Zostały ukończone wszystkie pliku definicji usługi toohello hello wymagane zmiany; jednak nadal potrzebujesz informacji o certyfikacie hello tooadd do pliku konfiguracji usługi hello.</span><span class="sxs-lookup"><span data-stu-id="67147-145">All hello required changes toohello service definition file have been completed; but, you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="67147-146">W pliku konfiguracji usługi (CSCFG), ServiceConfiguration.Cloud.cscfg, Dodaj **certyfikaty** wartości z tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="67147-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="67147-147">Witaj Poniższy przykładowy kod zawiera szczegółowe informacje o hello **certyfikaty** części, z wyjątkiem hello wartość odcisku palca.</span><span class="sxs-lookup"><span data-stu-id="67147-147">hello following code sample provides details of hello **Certificates** section, except for hello thumbprint value.</span></span>

   ```xml
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff"
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc"
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

<span data-ttu-id="67147-148">(W tym przykładzie użyto **sha1** hello odcisku palca algorytmu.</span><span class="sxs-lookup"><span data-stu-id="67147-148">(This example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="67147-149">Określ hello odpowiednią wartość dla algorytmu odcisk palca certyfikatu).</span><span class="sxs-lookup"><span data-stu-id="67147-149">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="67147-150">Teraz, gdy hello definicji i usługa plików konfiguracyjnych usługi zostały zaktualizowane, pakiet wdrożenia do przekazywania tooAzure.</span><span class="sxs-lookup"><span data-stu-id="67147-150">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="67147-151">Jeśli używasz **cspack**, nie używaj **/generateConfigurationFile** Flaga, jako który zastąpi wstawione informacje o certyfikacie.</span><span class="sxs-lookup"><span data-stu-id="67147-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="67147-152">Krok 3: Przekaż certyfikat</span><span class="sxs-lookup"><span data-stu-id="67147-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="67147-153">Połącz toohello portalu Azure i...</span><span class="sxs-lookup"><span data-stu-id="67147-153">Connect toohello Azure portal and...</span></span>

1. <span data-ttu-id="67147-154">W hello **wszystkie zasoby** sekcji hello portalu, wybierz usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="67147-154">In hello **All resources** section of hello Portal, select your cloud service.</span></span>

    ![Publikowanie usługi w chmurze](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="67147-156">Kliknij przycisk **certyfikaty**.</span><span class="sxs-lookup"><span data-stu-id="67147-156">Click **Certificates**.</span></span>

    ![Kliknij ikonę certyfikaty hello](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="67147-158">Kliknij przycisk **przekazać** u góry hello obszaru certyfikaty hello.</span><span class="sxs-lookup"><span data-stu-id="67147-158">Click **Upload** at hello top of hello certificates area.</span></span>

    ![Kliknij element menu hello przekazywania](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="67147-160">Podaj hello **pliku**, **hasło**, następnie kliknij przycisk **przekazać** u dołu hello obszar wprowadzania danych hello.</span><span class="sxs-lookup"><span data-stu-id="67147-160">Provide hello **File**, **Password**, then click **Upload** at hello bottom of hello data entry area.</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="67147-161">Krok 4: Łączenie toohello wystąpienia roli przy użyciu protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="67147-161">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="67147-162">Teraz, wdrożenie jest uruchomiona na platformie Azure, możesz połączyć tooit przy użyciu protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="67147-162">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="67147-163">Kliknij przycisk hello **adres URL witryny** tooopen hello przeglądarkę sieci web.</span><span class="sxs-lookup"><span data-stu-id="67147-163">Click hello **Site URL** tooopen up hello web browser.</span></span>

   ![Kliknij przycisk hello adres URL witryny](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="67147-165">W przeglądarce sieci web, należy zmodyfikować hello łącze toouse **https** zamiast **http**, a następnie odwiedź stronę hello.</span><span class="sxs-lookup"><span data-stu-id="67147-165">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="67147-166">Jeśli używasz certyfikatu z podpisem własnym, podczas przeglądania tooan punkt końcowy HTTPS skojarzoną z certyfikatu z podpisem własnym hello mogą pojawić się w przeglądarce hello błąd certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="67147-166">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="67147-167">Przy użyciu certyfikatu podpisanego przez zaufany urząd certyfikacji eliminuje ten problem. w hello międzyczasie, możesz zignorować błąd hello.</span><span class="sxs-lookup"><span data-stu-id="67147-167">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="67147-168">(Inną możliwością jest tooadd hello certyfikatu z podpisem własnym toohello certyfikat zaufanego urzędu magazynu certyfikatów użytkownika).</span><span class="sxs-lookup"><span data-stu-id="67147-168">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![Wersja zapoznawcza witryny](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="67147-170">Jeśli chcesz toouse SSL przemieszczania wdrożenia zamiast wdrożenia produkcyjnego, najpierw należy toodetermine hello adres URL dla hello przemieszczania wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="67147-170">If you want toouse SSL for a staging deployment instead of a production deployment, you'll first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="67147-171">Po wdrożeniu usługi w chmurze toohello adres URL hello środowiska przemieszczania jest określany przez hello **identyfikator wdrożenia** identyfikator GUID w następującym formacie:`https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="67147-171">Once your cloud service has been deployed, hello URL toohello staging environment is determined by hello **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="67147-172">Utwórz certyfikat z hello typowych nazwa (CN) równy toohello oparta na identyfikatorze GUID adresem URL (na przykład **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="67147-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="67147-173">Użyj hello portalu tooadd hello certyfikatu tooyour przemieszczane usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="67147-173">Use hello portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="67147-174">Dodawaniu hello informacji tooyour CSDEF i CSCFG pliki certyfikatów, Spakuj ponownie aplikację i zaktualizować wdrożenia etapowego toouse hello nowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="67147-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="67147-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="67147-175">Next steps</span></span>
* <span data-ttu-id="67147-176">[Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="67147-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="67147-177">Dowiedz się, jak za[wdrażania usługi w chmurze](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="67147-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="67147-178">Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="67147-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="67147-179">[Usługi w chmurze zarządzanie](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="67147-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
