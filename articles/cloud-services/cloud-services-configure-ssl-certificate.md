---
title: "Konfigurowanie protokołu SSL dla usługi w chmurze (klasyczne) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak określić punkt końcowy HTTPS dla roli sieci web i jak można przekazać certyfikatu SSL do zabezpieczania aplikacji."
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
ms.openlocfilehash: edb9aaf6dae11c9b8a171b22bc8a17003f80d86b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="014b7-103">Konfigurowanie protokołu SSL dla aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="014b7-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="014b7-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="014b7-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="014b7-105">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="014b7-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="014b7-106">Szyfrowanie SSL (Secure Socket Layer) to najczęściej stosowana metoda zabezpieczania danych wysyłanych przez Internet.</span><span class="sxs-lookup"><span data-stu-id="014b7-106">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="014b7-107">W ramach tego często wykonywanego zadania omówiono sposób określania punktu końcowego HTTPS dla roli sieci Web oraz przekazywania certyfikatu SSL w celu zabezpieczenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="014b7-107">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="014b7-108">Procedury w tym zadaniu mają zastosowanie do usług Azure Cloud Services; dla usług aplikacji, zobacz [to](../app-service-web/web-sites-configure-ssl-certificate.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="014b7-108">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="014b7-109">To zadanie używa wdrożenia produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="014b7-109">This task uses a production deployment.</span></span> <span data-ttu-id="014b7-110">Informacji na temat używania tymczasowej wdrożenia znajduje się na końcu tego tematu.</span><span class="sxs-lookup"><span data-stu-id="014b7-110">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="014b7-111">Odczyt [to](cloud-services-how-to-create-deploy.md) najpierw artykułu, jeśli nie utworzono jeszcze usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="014b7-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="014b7-112">Krok 1: Uzyskiwanie certyfikatu SSL.</span><span class="sxs-lookup"><span data-stu-id="014b7-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="014b7-113">Aby skonfigurować protokół SSL dla aplikacji, należy najpierw uzyskać certyfikat SSL, który został podpisany przez urząd certyfikacji, zaufanych innej firmy, który wystawia certyfikaty w tym celu.</span><span class="sxs-lookup"><span data-stu-id="014b7-113">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="014b7-114">Jeśli nie masz już jeden, należy uzyskać go z firmą, która sprzedaje certyfikatów SSL.</span><span class="sxs-lookup"><span data-stu-id="014b7-114">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="014b7-115">Certyfikat musi spełniać następujące wymagania dotyczące certyfikatów SSL na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="014b7-115">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="014b7-116">Certyfikat musi zawierać klucz prywatny.</span><span class="sxs-lookup"><span data-stu-id="014b7-116">The certificate must contain a private key.</span></span>
* <span data-ttu-id="014b7-117">Certyfikat musi zostać utworzony dla wymiany kluczy, można eksportować do pliku wymiany informacji osobistych (pfx).</span><span class="sxs-lookup"><span data-stu-id="014b7-117">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="014b7-118">Nazwa podmiotu certyfikatu musi odpowiadać domeny używane do uzyskania dostępu do usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="014b7-118">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="014b7-119">Nie można uzyskać certyfikatu SSL z urzędu certyfikacji (CA) dla domeny cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="014b7-119">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="014b7-120">Należy uzyskać niestandardowej nazwy domeny do użycia podczas połączenia się z usługą.</span><span class="sxs-lookup"><span data-stu-id="014b7-120">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="014b7-121">Podczas żądania certyfikatu z urzędu certyfikacji, nazwa podmiotu certyfikatu musi odpowiadać nazwie domeny niestandardowej, umożliwiające dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="014b7-121">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="014b7-122">Na przykład jeśli nazwą domeny niestandardowej jest **contoso.com** może zażądać certyfikatu od urzędu certyfikacji dla ***. contoso.com** lub **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="014b7-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="014b7-123">Certyfikat należy użyć co najmniej 2048-bitowego szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="014b7-123">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="014b7-124">Do celów testowych możesz [utworzyć](cloud-services-certs-create.md) i użycia certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="014b7-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="014b7-125">Certyfikatu z podpisem własnym nie jest uwierzytelniony za pośrednictwem urzędu certyfikacji i może używać domeny cloudapp.net jako adres URL witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="014b7-125">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="014b7-126">Na przykład następujące zadanie używa certyfikatu z podpisem własnym jest nazwa pospolita (CN) użyta w certyfikacie **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="014b7-126">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="014b7-127">Następnie musi zawierać informacje o certyfikacie w definicji usługi oraz pliki konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="014b7-127">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="014b7-128">Krok 2: Modyfikowanie plików definicji i konfigurację usługi</span><span class="sxs-lookup"><span data-stu-id="014b7-128">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="014b7-129">Aplikacji musi być skonfigurowana do używania certyfikatu, a punkt końcowy HTTPS muszą zostać dodane.</span><span class="sxs-lookup"><span data-stu-id="014b7-129">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="014b7-130">W związku z tym definicji usługi i pliki konfiguracyjne usługi muszą zostać zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="014b7-130">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="014b7-131">W środowisku projektowania, otwórz plik definicji usługi (CSDEF), Dodaj **certyfikaty** sekcji w **sieć Web** sekcji i obejmują następujące informacje dotyczące certyfikatu (i certyfikaty pośrednie):</span><span class="sxs-lookup"><span data-stu-id="014b7-131">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>
   
    ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                        storeLocation="LocalMachine" 
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by the CA root, you
            must include all the intermediate certificates
            here. You must list them here, even if they are
            not bound to any endpoints. Failing to list any of
            the intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```
   
   <span data-ttu-id="014b7-132">**Certyfikaty** sekcja definiuje nazwę naszych certyfikatu, jego lokalizację i nazwę magazynu, w którym znajduje się.</span><span class="sxs-lookup"><span data-stu-id="014b7-132">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>
   
   <span data-ttu-id="014b7-133">Uprawnienia (`permisionLevel` atrybut) może być ustawione na jedną z następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="014b7-133">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>
   
   | <span data-ttu-id="014b7-134">Wartość uprawnienia</span><span class="sxs-lookup"><span data-stu-id="014b7-134">Permission Value</span></span> | <span data-ttu-id="014b7-135">Opis</span><span class="sxs-lookup"><span data-stu-id="014b7-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="014b7-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="014b7-136">limitedOrElevated</span></span> |<span data-ttu-id="014b7-137">**(Ustawienie domyślne)**  Wszystkie procesy roli można uzyskać dostępu do klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="014b7-137">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="014b7-138">z podwyższonym poziomem uprawnień</span><span class="sxs-lookup"><span data-stu-id="014b7-138">elevated</span></span> |<span data-ttu-id="014b7-139">Tylko procesów z podwyższonym poziomem uprawnień można uzyskać dostępu do klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="014b7-139">Only elevated processes can access the private key.</span></span> |
2. <span data-ttu-id="014b7-140">W pliku definicji usługi, dodać **InputEndpoint** w elemencie **punkty końcowe** sekcji, aby włączyć protokół HTTPS:</span><span class="sxs-lookup"><span data-stu-id="014b7-140">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>
   
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

3. <span data-ttu-id="014b7-141">W pliku definicji usługi, dodać **powiązanie** w elemencie **witryny** sekcji.</span><span class="sxs-lookup"><span data-stu-id="014b7-141">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="014b7-142">W tej sekcji dodaje powiązanie HTTPS do mapowania punktu końcowego do swojej witryny:</span><span class="sxs-lookup"><span data-stu-id="014b7-142">This section adds an HTTPS binding to map the endpoint to your site:</span></span>
   
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
   
   <span data-ttu-id="014b7-143">Wszystkie wymagane zmiany w pliku definicji usługi zostały ukończone, ale nadal konieczne jest dodanie informacji o certyfikacie w pliku konfiguracji usługi.</span><span class="sxs-lookup"><span data-stu-id="014b7-143">All the required changes to the service definition file have been completed, but you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="014b7-144">W pliku konfiguracji usługi (CSCFG), ServiceConfiguration.Cloud.cscfg, Dodaj **certyfikaty** sekcji w **roli** sekcji, zastępując wartość odcisku palca przykładowych pokazano poniżej, z którego certyfikatu:</span><span class="sxs-lookup"><span data-stu-id="014b7-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within the **Role** section, replacing the sample thumbprint value shown below with that of your certificate:</span></span>
   
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

<span data-ttu-id="014b7-145">(W poprzednim przykładzie użyto **sha1** dla algorytmu odcisk palca.</span><span class="sxs-lookup"><span data-stu-id="014b7-145">(The preceding example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="014b7-146">Określ wartość odpowiednią dla algorytmu odcisk palca certyfikatu).</span><span class="sxs-lookup"><span data-stu-id="014b7-146">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="014b7-147">Teraz, definicji usługi i pliki konfiguracji usługi zostały zaktualizowane, pakiet wdrożenia do przekazywania do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="014b7-147">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="014b7-148">Jeśli używasz **cspack**, nie używaj **/generateConfigurationFile** Flaga, jako który zastępuje wstawiono informacji o certyfikacie.</span><span class="sxs-lookup"><span data-stu-id="014b7-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="014b7-149">Krok 3: Przekaż certyfikat</span><span class="sxs-lookup"><span data-stu-id="014b7-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="014b7-150">Pakiet wdrażania została zaktualizowana do używania certyfikatu, a dodano punkt końcowy HTTPS.</span><span class="sxs-lookup"><span data-stu-id="014b7-150">Your deployment package has been updated to use the certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="014b7-151">Możesz teraz przekazać certyfikatów i pakietów do platformy Azure z klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="014b7-151">Now you can upload the package and certificate to Azure with the Azure classic portal.</span></span>

1. <span data-ttu-id="014b7-152">Zaloguj się do [klasycznego portalu Azure][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="014b7-152">Log in to the [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="014b7-153">Kliknij przycisk **usługi w chmurze** w okienku nawigacji po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="014b7-153">Click **Cloud Services** on the left-side navigation pane.</span></span>
3. <span data-ttu-id="014b7-154">Kliknij usługę w chmurze żądany.</span><span class="sxs-lookup"><span data-stu-id="014b7-154">Click the desired cloud service.</span></span>
4. <span data-ttu-id="014b7-155">Kliknij przycisk **certyfikaty** kartę.</span><span class="sxs-lookup"><span data-stu-id="014b7-155">Click the **Certificates** tab.</span></span>
   
    ![Kliknij kartę certyfikaty](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="014b7-157">Kliknij przycisk **Przekaż**.</span><span class="sxs-lookup"><span data-stu-id="014b7-157">Click the **Upload** button.</span></span>
   
    ![Upload](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="014b7-159">Podaj **pliku**, **hasło**, następnie kliknij przycisk **Complete** (znacznikiem wyboru).</span><span class="sxs-lookup"><span data-stu-id="014b7-159">Provide the **File**, **Password**, then click **Complete** (the checkmark).</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="014b7-160">Krok 4: Łączenie z wystąpienia roli przy użyciu protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="014b7-160">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="014b7-161">Teraz, że wdrożenie jest uruchomiona na platformie Azure, można połączyć się przy użyciu protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="014b7-161">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="014b7-162">W klasycznym portalu Azure, wybierz wdrożenie, a następnie kliknij łącze w obszarze **adres URL witryny**.</span><span class="sxs-lookup"><span data-stu-id="014b7-162">In the Azure classic portal, select your deployment, then click the link under **Site URL**.</span></span>
   
   ![Określić adres URL witryny][2]
2. <span data-ttu-id="014b7-164">W przeglądarce sieci web Zmień łącze do użycia **https** zamiast **http**, a następnie odwiedź stronę.</span><span class="sxs-lookup"><span data-stu-id="014b7-164">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="014b7-165">Jeśli używasz certyfikatu z podpisem własnym, po przejściu do punktu końcowego protokołu HTTPS, który został skojarzony z certyfikatu z podpisem własnym może zostać wyświetlony błąd certyfikatu w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="014b7-165">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="014b7-166">Przy użyciu certyfikatu podpisanego przez zaufany urząd certyfikacji eliminuje ten problem. w międzyczasie możesz zignorować błąd.</span><span class="sxs-lookup"><span data-stu-id="014b7-166">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="014b7-167">(Inną opcją jest można dodać certyfikatu z podpisem własnym do magazynu certyfikatów urzędu zaufanego certyfikatu użytkownika).</span><span class="sxs-lookup"><span data-stu-id="014b7-167">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![Przykład witryny sieci web protokołu SSL][3]

<span data-ttu-id="014b7-169">Jeśli chcesz używać protokołu SSL dla tymczasowej wdrożenia zamiast wdrożenia produkcyjnego, należy najpierw ustalić adresu URL używany do wdrażania przejściowego.</span><span class="sxs-lookup"><span data-stu-id="014b7-169">If you want to use SSL for a staging deployment instead of a production deployment, you first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="014b7-170">Wdrażanie usługi w chmurze do środowiska pomostowego, bez uwzględniania certyfikatu lub żadnych informacji o certyfikacie.</span><span class="sxs-lookup"><span data-stu-id="014b7-170">Deploy your cloud service to the staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="014b7-171">Po wdrożeniu, można określić adres URL na podstawie identyfikatora GUID, która jest wyświetlana w klasycznym portalu Azure w **adres URL witryny** pola.</span><span class="sxs-lookup"><span data-stu-id="014b7-171">Once deployed, you can determine the GUID-based URL, which is listed in the Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="014b7-172">Utwórz certyfikat z nazwa pospolita (CN) taki sam adres URL na podstawie identyfikatora GUID (na przykład **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="014b7-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="014b7-173">Użyj klasycznego portalu Azure można dodać certyfikatu do usługi w chmurze przemieszczane.</span><span class="sxs-lookup"><span data-stu-id="014b7-173">Use the Azure classic portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="014b7-174">Następnie dodaj informacje o certyfikacie do pliki CSDEF i CSCFG, ponownie utworzyć pakiet aplikacji i aktualizacji przemieszczanego wdrożenia do użycia nowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="014b7-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="014b7-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="014b7-175">Next steps</span></span>
* <span data-ttu-id="014b7-176">[Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="014b7-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="014b7-177">Dowiedz się, jak [wdrażania usługi w chmurze](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="014b7-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="014b7-178">Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="014b7-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="014b7-179">[Usługi w chmurze zarządzanie](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="014b7-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
