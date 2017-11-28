---
title: "aaaConfigure protokołu SSL dla usługi w chmurze (klasyczne) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toospecify punkt końcowy HTTPS dla roli sieci web i jak tooupload SSL certyfikatów toosecure aplikacji."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 4cbb7f38-7994-454d-b4f0-7259b558c766
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: a1ca031b98af49d371977a208ed24f6dc8ea2ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="d1233-103">Konfigurowanie protokołu SSL dla aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="d1233-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d1233-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d1233-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="d1233-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d1233-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="d1233-106">Metoda zabezpieczania danych przesyłanych między hello hello najczęściej używane jest szyfrowanie Secure Socket Layer (SSL) internet.</span><span class="sxs-lookup"><span data-stu-id="d1233-106">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="d1233-107">To zadanie typowe omówiono sposób toospecify punkt końcowy HTTPS dla roli sieci web i jak tooupload SSL certyfikatów toosecure aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1233-107">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="d1233-108">Usługi w chmurze tooAzure; Zastosuj Hello procedur w tym zadaniu dla usług aplikacji, zobacz [to](../app-service-web/web-sites-configure-ssl-certificate.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d1233-108">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="d1233-109">To zadanie używa wdrożenia produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d1233-109">This task uses a production deployment.</span></span> <span data-ttu-id="d1233-110">Informacji na temat używania tymczasowej wdrożenia znajduje się na powitania na końcu tego tematu.</span><span class="sxs-lookup"><span data-stu-id="d1233-110">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="d1233-111">Odczyt [to](cloud-services-how-to-create-deploy.md) najpierw artykułu, jeśli nie utworzono jeszcze usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d1233-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="d1233-112">Krok 1: Uzyskiwanie certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="d1233-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="d1233-113">tooconfigure protokołu SSL dla aplikacji, należy najpierw tooget certyfikat SSL, który został podpisany przez urząd certyfikacji, zaufanych innej firmy, który wystawia certyfikaty w tym celu.</span><span class="sxs-lookup"><span data-stu-id="d1233-113">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="d1233-114">Jeśli nie masz już jeden, należy tooobtain jedną z firmy, która sprzedaje certyfikatów SSL.</span><span class="sxs-lookup"><span data-stu-id="d1233-114">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="d1233-115">Hello certyfikatu musi spełniać następujące wymagania dotyczące certyfikatów SSL na platformie Azure hello:</span><span class="sxs-lookup"><span data-stu-id="d1233-115">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="d1233-116">Witaj, certyfikat musi zawierać klucz prywatny.</span><span class="sxs-lookup"><span data-stu-id="d1233-116">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="d1233-117">Witaj certyfikatu musi zostać utworzony dla wymiany kluczy, można eksportować tooa plik wymiany informacji osobistych (pfx).</span><span class="sxs-lookup"><span data-stu-id="d1233-117">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="d1233-118">Hello nazwa podmiotu certyfikatu musi odpowiadać usługi hello tooaccess hello domeny użytej w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d1233-118">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="d1233-119">Nie można uzyskać certyfikatu SSL z urzędu certyfikacji (CA) dla domeny cloudapp.net hello.</span><span class="sxs-lookup"><span data-stu-id="d1233-119">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="d1233-120">Należy uzyskać toouse nazwy domeny niestandardowej podczas dostępu usługi.</span><span class="sxs-lookup"><span data-stu-id="d1233-120">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="d1233-121">Podczas żądania certyfikatu z urzędu certyfikacji, nazwa podmiotu certyfikatu hello musi odpowiadać hello domenę niestandardową nazwę używaną tooaccess aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1233-121">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="d1233-122">Na przykład jeśli nazwą domeny niestandardowej jest **contoso.com** może zażądać certyfikatu od urzędu certyfikacji dla ***. contoso.com** lub **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="d1233-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="d1233-123">Witaj certyfikatu należy użyć co najmniej 2048-bitowego szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="d1233-123">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="d1233-124">Do celów testowych możesz [utworzyć](cloud-services-certs-create.md) i użycia certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="d1233-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="d1233-125">Certyfikatu z podpisem własnym nie jest uwierzytelniony za pośrednictwem urzędu certyfikacji i używać jako adres URL witryny sieci Web hello hello cloudapp.net domeny.</span><span class="sxs-lookup"><span data-stu-id="d1233-125">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="d1233-126">Na przykład hello następujące zadanie używa certyfikatu z podpisem własnym w których hello jest nazwa pospolita (CN) używane w certyfikacie hello **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="d1233-126">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="d1233-127">Następnie musi zawierać informacje o certyfikacie hello w definicji usługi oraz pliki konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="d1233-127">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="d1233-128">Krok 2: Modyfikowanie plików definicji i konfiguracji usługi hello</span><span class="sxs-lookup"><span data-stu-id="d1233-128">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="d1233-129">Aplikacja musi być skonfigurowany toouse hello certyfikatu, a punkt końcowy HTTPS muszą zostać dodane.</span><span class="sxs-lookup"><span data-stu-id="d1233-129">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="d1233-130">W związku z tym hello definicji usługi i pliki konfiguracji usługi wymagają toobe aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="d1233-130">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="d1233-131">W środowisku projektowania, otwórz plik definicji hello usługi (CSDEF), Dodaj **certyfikaty** sekcji w hello **sieć Web** sekcji, a obejmują hello następujących informacji certyfikat (i certyfikaty pośrednie):</span><span class="sxs-lookup"><span data-stu-id="d1233-131">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>
   
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
   
   <span data-ttu-id="d1233-132">Witaj **certyfikaty** sekcja definiuje nazwę hello naszych certyfikatu, jego lokalizację i nazwę hello magazynu hello, w którym znajduje się.</span><span class="sxs-lookup"><span data-stu-id="d1233-132">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>
   
   <span data-ttu-id="d1233-133">Uprawnienia (`permisionLevel` atrybutów) mogą być tooone zestawu z hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="d1233-133">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>
   
   | <span data-ttu-id="d1233-134">Wartość uprawnienia</span><span class="sxs-lookup"><span data-stu-id="d1233-134">Permission Value</span></span> | <span data-ttu-id="d1233-135">Opis</span><span class="sxs-lookup"><span data-stu-id="d1233-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="d1233-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="d1233-136">limitedOrElevated</span></span> |<span data-ttu-id="d1233-137">**(Ustawienie domyślne)**  Wszystkie procesy roli można uzyskać dostępu do klucza prywatnego hello.</span><span class="sxs-lookup"><span data-stu-id="d1233-137">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="d1233-138">z podwyższonym poziomem uprawnień</span><span class="sxs-lookup"><span data-stu-id="d1233-138">elevated</span></span> |<span data-ttu-id="d1233-139">Tylko procesów z podwyższonym poziomem uprawnień można uzyskać dostępu do klucza prywatnego hello.</span><span class="sxs-lookup"><span data-stu-id="d1233-139">Only elevated processes can access hello private key.</span></span> |
2. <span data-ttu-id="d1233-140">W pliku definicji usługi, dodać **InputEndpoint** elementu w obrębie hello **punkty końcowe** sekcji tooenable HTTPS:</span><span class="sxs-lookup"><span data-stu-id="d1233-140">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>
   
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

3. <span data-ttu-id="d1233-141">W pliku definicji usługi, dodać **powiązanie** elementu w obrębie hello **witryny** sekcji.</span><span class="sxs-lookup"><span data-stu-id="d1233-141">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="d1233-142">W tej sekcji dodaje toomap powiązanie HTTPS lokacji tooyour punktu końcowego:</span><span class="sxs-lookup"><span data-stu-id="d1233-142">This section adds an HTTPS binding toomap the endpoint tooyour site:</span></span>
   
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
   
   <span data-ttu-id="d1233-143">Wszystkie pliku definicji usługi toohello hello wymagane zmiany zostały ukończone, ale nadal potrzebujesz informacji o certyfikacie hello tooadd do pliku konfiguracji usługi hello.</span><span class="sxs-lookup"><span data-stu-id="d1233-143">All hello required changes toohello service definition file have been completed, but you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="d1233-144">W pliku konfiguracji usługi (CSCFG), ServiceConfiguration.Cloud.cscfg, Dodaj **certyfikaty** sekcji w hello **roli** sekcji, zastępując hello wartość odcisku palca dla przykładowych pokazano poniżej z który certyfikatu:</span><span class="sxs-lookup"><span data-stu-id="d1233-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within hello **Role** section, replacing hello sample thumbprint value shown below with that of your certificate:</span></span>
   
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

<span data-ttu-id="d1233-145">(hello poprzedzających przykładzie użyto **sha1** hello odcisku palca algorytmu.</span><span class="sxs-lookup"><span data-stu-id="d1233-145">(hello preceding example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="d1233-146">Określ hello odpowiednią wartość dla algorytmu odcisk palca certyfikatu).</span><span class="sxs-lookup"><span data-stu-id="d1233-146">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="d1233-147">Teraz, gdy hello definicji i usługa plików konfiguracyjnych usługi zostały zaktualizowane, pakiet wdrożenia do przekazywania tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d1233-147">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="d1233-148">Jeśli używasz **cspack**, nie używaj **/generateConfigurationFile** Flaga, jako który zastępuje wstawiono informacji o certyfikacie.</span><span class="sxs-lookup"><span data-stu-id="d1233-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="d1233-149">Krok 3: Przekaż certyfikat</span><span class="sxs-lookup"><span data-stu-id="d1233-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="d1233-150">Pakiet wdrażania zostało zaktualizowane toouse hello certyfikatu, i dodano punkt końcowy HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d1233-150">Your deployment package has been updated toouse hello certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="d1233-151">Możesz teraz przekazać tooAzure certyfikatów i pakietów hello z hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d1233-151">Now you can upload hello package and certificate tooAzure with hello Azure classic portal.</span></span>

1. <span data-ttu-id="d1233-152">Zaloguj się za toohello [klasycznego portalu Azure][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="d1233-152">Log in toohello [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="d1233-153">Kliknij przycisk **usługi w chmurze** w okienku nawigacji po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="d1233-153">Click **Cloud Services** on hello left-side navigation pane.</span></span>
3. <span data-ttu-id="d1233-154">Kliknij pozycję usługi w chmurze hello potrzebne.</span><span class="sxs-lookup"><span data-stu-id="d1233-154">Click hello desired cloud service.</span></span>
4. <span data-ttu-id="d1233-155">Kliknij przycisk hello **certyfikaty** kartę.</span><span class="sxs-lookup"><span data-stu-id="d1233-155">Click hello **Certificates** tab.</span></span>
   
    ![Kliknij kartę certyfikaty hello](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="d1233-157">Kliknij przycisk hello **przekazać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d1233-157">Click hello **Upload** button.</span></span>
   
    ![Upload](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="d1233-159">Podaj hello **pliku**, **hasło**, następnie kliknij przycisk **Complete** (hello znacznikiem wyboru).</span><span class="sxs-lookup"><span data-stu-id="d1233-159">Provide hello **File**, **Password**, then click **Complete** (hello checkmark).</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="d1233-160">Krok 4: Łączenie toohello wystąpienia roli przy użyciu protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="d1233-160">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="d1233-161">Teraz, wdrożenie jest uruchomiona na platformie Azure, możesz połączyć tooit przy użyciu protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d1233-161">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="d1233-162">W hello klasycznego portalu Azure, wybierz wdrożenie, a następnie kliknij łącze hello w obszarze **adres URL witryny**.</span><span class="sxs-lookup"><span data-stu-id="d1233-162">In hello Azure classic portal, select your deployment, then click hello link under **Site URL**.</span></span>
   
   ![Określić adres URL witryny][2]
2. <span data-ttu-id="d1233-164">W przeglądarce sieci web, należy zmodyfikować hello łącze toouse **https** zamiast **http**, a następnie odwiedź stronę hello.</span><span class="sxs-lookup"><span data-stu-id="d1233-164">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d1233-165">Jeśli używasz certyfikatu z podpisem własnym, podczas przeglądania tooan punkt końcowy HTTPS skojarzoną z certyfikatu z podpisem własnym hello mogą pojawić się w przeglądarce hello błąd certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="d1233-165">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="d1233-166">Przy użyciu certyfikatu podpisanego przez zaufany urząd certyfikacji eliminuje ten problem. w hello międzyczasie, możesz zignorować błąd hello.</span><span class="sxs-lookup"><span data-stu-id="d1233-166">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="d1233-167">(Inną możliwością jest tooadd hello certyfikatu z podpisem własnym toohello certyfikat zaufanego urzędu magazynu certyfikatów użytkownika).</span><span class="sxs-lookup"><span data-stu-id="d1233-167">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![Przykład witryny sieci web protokołu SSL][3]

<span data-ttu-id="d1233-169">Jeśli chcesz toouse SSL przemieszczania wdrożenia zamiast wdrożenia produkcyjnego, należy najpierw toodetermine hello adres URL dla hello przemieszczania wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d1233-169">If you want toouse SSL for a staging deployment instead of a production deployment, you first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="d1233-170">Wdrażanie usługi toohello przemieszczania środowiska chmury bez uwzględniania certyfikatu lub żadnych informacji o certyfikacie.</span><span class="sxs-lookup"><span data-stu-id="d1233-170">Deploy your cloud service toohello staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="d1233-171">Po wdrożeniu, można określić adresu hello URL na podstawie identyfikatora GUID, który znajduje się na powitania klasycznego portalu Azure **adres URL witryny** pola.</span><span class="sxs-lookup"><span data-stu-id="d1233-171">Once deployed, you can determine hello GUID-based URL, which is listed in hello Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="d1233-172">Utwórz certyfikat z hello typowych nazwa (CN) równy toohello oparta na identyfikatorze GUID adresem URL (na przykład **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="d1233-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="d1233-173">Użyj hello Azure classic portal tooadd hello certyfikatu tooyour przemieszczane usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d1233-173">Use hello Azure classic portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="d1233-174">Dodawaniu hello informacji tooyour CSDEF i CSCFG pliki certyfikatów, Spakuj ponownie aplikację i zaktualizować wdrożenia etapowego toouse hello nowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="d1233-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1233-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d1233-175">Next steps</span></span>
* <span data-ttu-id="d1233-176">[Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d1233-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="d1233-177">Dowiedz się, jak za[wdrażania usługi w chmurze](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d1233-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="d1233-178">Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="d1233-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="d1233-179">[Usługi w chmurze zarządzanie](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="d1233-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
