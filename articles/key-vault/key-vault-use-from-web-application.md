---
title: "aaaUse usługi Azure Key Vault z aplikacji sieci Web | Dokumentacja firmy Microsoft"
description: "Użyj tego samouczka toohelp dowiesz się, jak toouse Azure klucza magazynu z aplikacji sieci web."
services: key-vault
documentationcenter: 
author: adhurwit
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: adhurwit
ms.openlocfilehash: d5e2299e60b379c4e234d5cd6be03411c5a5c958
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="6bf15-103">Użyj usługi Azure Key Vault z aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="6bf15-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="6bf15-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="6bf15-104">Introduction</span></span>
<span data-ttu-id="6bf15-105">Użyj tego samouczka toohelp dowiesz się, jak toouse Azure klucza magazynu z aplikacji sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6bf15-105">Use this tutorial toohelp you learn how toouse Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="6bf15-106">Przeprowadza użytkownika przez proces hello uzyskiwania dostępu do klucza tajnego z magazynu kluczy Azure, dzięki czemu mogą być używane w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="6bf15-106">It walks you through hello process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="6bf15-107">**Szacowany czas toocomplete:** 15 minut</span><span class="sxs-lookup"><span data-stu-id="6bf15-107">**Estimated time toocomplete:** 15 minutes</span></span>

<span data-ttu-id="6bf15-108">Aby uzyskać ogólne informacje na temat usługi Azure Key Vault, zobacz [Co to jest usługa Azure Key Vault?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="6bf15-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bf15-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6bf15-109">Prerequisites</span></span>
<span data-ttu-id="6bf15-110">toocomplete tego samouczka, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="6bf15-110">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="6bf15-111">Identyfikator URI tooa klucza tajnego w magazynie kluczy Azure</span><span class="sxs-lookup"><span data-stu-id="6bf15-111">A URI tooa secret in an Azure Key Vault</span></span>
* <span data-ttu-id="6bf15-112">Identyfikator klienta i klucz tajny klienta dla aplikacji sieci web w zarejestrowany w usłudze Azure Active Directory, zawierający tooyour dostępu do magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="6bf15-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access tooyour Key Vault</span></span>
* <span data-ttu-id="6bf15-113">Aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="6bf15-113">A web application.</span></span> <span data-ttu-id="6bf15-114">Firma Microsoft będzie wyświetlane hello kroki dla aplikacji platformy ASP.NET MVC wdrożona na platformie Azure jako aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6bf15-114">We will be showing hello steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="6bf15-115">Jest to, że zostały wykonane kroki hello na liście [wprowadzenie do usługi Azure Key Vault](key-vault-get-started.md) w tym samouczku, aby mieć hello klucz tajny tooa identyfikatora URI i hello identyfikator klienta i klucz tajny klienta dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="6bf15-115">It is essential that you have completed hello steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have hello URI tooa secret and hello Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="6bf15-116">Aplikacja sieci web Hello będą uzyskiwać dostęp do usługi Key Vault hello jest hello, co jest zarejestrowany w usłudze Azure Active Directory, która została podana tooyour dostępu do magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="6bf15-116">hello web application that will be accessing hello Key Vault is hello one that is registered in Azure Active Directory and has been given access tooyour Key Vault.</span></span> <span data-ttu-id="6bf15-117">Jeśli nie jest to hello, wróć tooRegister aplikację w Samouczek wprowadzający hello i powtórz kroki hello na liście.</span><span class="sxs-lookup"><span data-stu-id="6bf15-117">If this is not hello case, go back tooRegister an Application in hello Get Started tutorial and repeat hello steps listed.</span></span>

<span data-ttu-id="6bf15-118">Ten samouczek jest przeznaczony dla deweloperów sieci web, które rozumieją hello podstawy tworzenia aplikacji sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6bf15-118">This tutorial is designed for web developers that understand hello basics of creating web applications on Azure.</span></span> <span data-ttu-id="6bf15-119">Aby uzyskać więcej informacji dotyczących aplikacji sieci Web platformy Azure, zobacz [Omówienie aplikacji sieci Web](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6bf15-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="6bf15-120"><a id="packages"></a>Dodawanie pakietów Nuget</span><span class="sxs-lookup"><span data-stu-id="6bf15-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="6bf15-121">Istnieją dwa pakiety, które toohave zainstalowanych aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="6bf15-121">There are two packages that your web application needs toohave installed.</span></span>

* <span data-ttu-id="6bf15-122">Biblioteki uwierzytelniania usługi Active Directory - zawiera metody interakcji z usługą Azure Active Directory i Zarządzanie tożsamościami użytkowników</span><span class="sxs-lookup"><span data-stu-id="6bf15-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="6bf15-123">Biblioteka magazynu Azure klucza — zawiera metody interakcji z usługą Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="6bf15-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="6bf15-124">Oba te pakiety można zainstalować przy użyciu konsoli Menedżera pakietów za pomocą polecenia Install-Package hello hello.</span><span class="sxs-lookup"><span data-stu-id="6bf15-124">Both of these packages can be installed using hello Package Manager Console using hello Install-Package command.</span></span>

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="6bf15-125"><a id="webconfig"></a>Modyfikowanie pliku Web.Config</span><span class="sxs-lookup"><span data-stu-id="6bf15-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="6bf15-126">Istnieją trzy ustawienia aplikacji, które należy pliku web.config dodano toohello toobe w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="6bf15-126">There are three application settings that need toobe added toohello web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="6bf15-127">Jeśli nie ma toohost aplikacji jako aplikacji sieci Web platformy Azure, należy dodać hello rzeczywiste ClientId, klucz tajny klienta i identyfikator URI klucza tajnego wartości toohello pliku web.config. W przeciwnym razie pozostaw te wartości fikcyjny ponieważ dodamy hello wartości rzeczywistych w hello Azure Portal dodatkowy poziom zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="6bf15-127">If you are not going toohost your application as an Azure Web App, then you should add hello actual ClientId, Client Secret, and Secret URI values toohello web.config. Otherwise leave these dummy values because we will be adding hello actual values in hello Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="6bf15-128"><a id="gettoken"></a>Dodaj Token dostępu tooGet — metoda</span><span class="sxs-lookup"><span data-stu-id="6bf15-128"><a id="gettoken"></a>Add Method tooGet an Access Token</span></span>
<span data-ttu-id="6bf15-129">W kolejności toouse hello klucz API magazynu należy tokenu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6bf15-129">In order toouse hello Key Vault API you need an access token.</span></span> <span data-ttu-id="6bf15-130">Witaj klucz magazynu klienta obsługuje wywołania toohello klucz API magazynu, ale konieczne toosupply go przy użyciu funkcji, który pobiera token dostępu hello.</span><span class="sxs-lookup"><span data-stu-id="6bf15-130">hello Key Vault Client handles calls toohello Key Vault API but you need toosupply it with a function that gets hello access token.</span></span>  

<span data-ttu-id="6bf15-131">Poniżej znajduje się hello kodu tooget token dostępu z usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6bf15-131">Following is hello code tooget an access token from Azure Active Directory.</span></span> <span data-ttu-id="6bf15-132">Ten kod może przejść w dowolne miejsce w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6bf15-132">This code can go anywhere in your application.</span></span> <span data-ttu-id="6bf15-133">Podoba tooadd witryny lub EncryptionHelper klasy.</span><span class="sxs-lookup"><span data-stu-id="6bf15-133">I like tooadd a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property toohold hello secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //hello method that will be provided toohello KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed tooobtain hello JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="6bf15-134">Przy użyciu Identyfikatora klienta i klucz tajny klienta jest hello Najprostszym sposobem tooauthenticate aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bf15-134">Using a Client ID and Client Secret is hello easiest way tooauthenticate an Azure AD application.</span></span> <span data-ttu-id="6bf15-135">I używania go w aplikacji sieci web umożliwia rozdzielenie obowiązków i większą kontrolę nad zarządzania infrastrukturą kluczy.</span><span class="sxs-lookup"><span data-stu-id="6bf15-135">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="6bf15-136">Jednak zależne umieszczanie hello klucz tajny klienta w ustawieniach konfiguracji, które może być ryzykowne jako jako wprowadzanie hasła hello mają tooprotect w ustawieniach konfiguracji dla niektórych.</span><span class="sxs-lookup"><span data-stu-id="6bf15-136">But it does rely on putting hello Client Secret in your configuration settings which for some can be as risky as putting hello secret that you want tooprotect in your configuration settings.</span></span> <span data-ttu-id="6bf15-137">Poniżej znajduje się omówione jak toouse identyfikator klienta i certyfikatu, a identyfikator klienta i klucz tajny klienta tooauthenticate hello aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bf15-137">See below for a discussion on how toouse a Client ID and Certificate instead of Client ID and Client Secret tooauthenticate hello Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="6bf15-138"><a id="appstart"></a>Pobierz klucz tajny hello Start aplikacji</span><span class="sxs-lookup"><span data-stu-id="6bf15-138"><a id="appstart"></a>Retrieve hello secret on Application Start</span></span>
<span data-ttu-id="6bf15-139">Teraz możemy muszą kodu hello toocall interfejsu API magazynu kluczy i pobrać hello klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="6bf15-139">Now we need code toocall hello Key Vault API and retrieve hello secret.</span></span> <span data-ttu-id="6bf15-140">Witaj następujący kod mogą być przełączane gdziekolwiek tak długo, jak jest ona wywoływana przed toouse go.</span><span class="sxs-lookup"><span data-stu-id="6bf15-140">hello following code can be put anywhere as long as it is called before you need toouse it.</span></span> <span data-ttu-id="6bf15-141">Zostało umieszczone ten kod w przypadku uruchomienia aplikacji hello w pliku Global.asax hello, tak aby raz uruchamia się po uruchomieniu i klucz tajny dostępnych dla aplikacji hello hello sprawia, że.</span><span class="sxs-lookup"><span data-stu-id="6bf15-141">I have put this code in hello Application Start event in hello Global.asax so that it runs once on start and makes hello secret available for hello application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="6bf15-142"><a id="portalsettings"></a>Dodawanie ustawienia aplikacji w hello portalu Azure (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="6bf15-142"><a id="portalsettings"></a>Add App Settings in hello Azure Portal (optional)</span></span>
<span data-ttu-id="6bf15-143">Jeśli masz aplikacji sieci Web platformy Azure można teraz dodawać hello rzeczywiste wartości hello AppSettings w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6bf15-143">If you have an Azure Web App you can now add hello actual values for hello AppSettings in hello Azure Portal.</span></span> <span data-ttu-id="6bf15-144">Dzięki temu wartości rzeczywistych hello nie będzie w pliku web.config hello, ale chronione za pomocą hello portalu, gdzie masz dostęp do osobnych możliwości kontroli.</span><span class="sxs-lookup"><span data-stu-id="6bf15-144">By doing this, hello actual values will not be in hello web.config but protected via hello Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="6bf15-145">Te wartości zostaną zastąpione hello wartości, które zostały wprowadzone w pliku web.config. Upewnij się, nazwy hello są hello takie same.</span><span class="sxs-lookup"><span data-stu-id="6bf15-145">These values will be substituted for hello values that you entered in your web.config. Make sure that hello names are hello same.</span></span>

![Ustawienia aplikacji wyświetlane w portalu Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="6bf15-147">Uwierzytelnianie przy użyciu certyfikatu zamiast klucz tajny klienta</span><span class="sxs-lookup"><span data-stu-id="6bf15-147">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="6bf15-148">Inny sposób tooauthenticate aplikacji usługi Azure AD jest przy użyciu Identyfikatora klienta oraz certyfikatu zamiast z Identyfikatorem klienta i klucz tajny klienta.</span><span class="sxs-lookup"><span data-stu-id="6bf15-148">Another way tooauthenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="6bf15-149">Poniżej są hello toouse kroki certyfikatu w aplikacji sieci Web platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="6bf15-149">Following are hello steps toouse a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="6bf15-150">Uzyskaj lub Utwórz certyfikat</span><span class="sxs-lookup"><span data-stu-id="6bf15-150">Get or Create a Certificate</span></span>
2. <span data-ttu-id="6bf15-151">Skojarz hello certyfikat przy użyciu aplikacji do usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6bf15-151">Associate hello Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="6bf15-152">Dodaj kod tooyour aplikacji sieci Web toouse hello certyfikatu</span><span class="sxs-lookup"><span data-stu-id="6bf15-152">Add code tooyour Web App toouse hello Certificate</span></span>
4. <span data-ttu-id="6bf15-153">Dodaj certyfikat tooyour aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="6bf15-153">Add a Certificate tooyour Web App</span></span>

<span data-ttu-id="6bf15-154">**Uzyskaj lub Utwórz certyfikat** dla naszych celów firma Microsoft będzie wprowadzać certyfikatu testowego.</span><span class="sxs-lookup"><span data-stu-id="6bf15-154">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="6bf15-155">Oto kilka poleceń, w której można w toocreate wiersza polecenia dewelopera certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="6bf15-155">Here are a couple of commands that you can use in a Developer Command Prompt toocreate a certificate.</span></span> <span data-ttu-id="6bf15-156">Utworzone pliki certyfikatu hello toowhere katalogu zmiany.</span><span class="sxs-lookup"><span data-stu-id="6bf15-156">Change directory toowhere you want hello cert files created.</span></span>  <span data-ttu-id="6bf15-157">Ponadto dla hello otwierające i zamykające Data certyfikatu hello, użyj hello bieżącą datę i 1 rok.</span><span class="sxs-lookup"><span data-stu-id="6bf15-157">Also, for hello beginning and ending date of hello certificate, use hello current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="6bf15-158">Zwróć uwagę na datę zakończenia hello i hello hasło PFX hello (w tym przykładzie: 2016-07-31 i test123).</span><span class="sxs-lookup"><span data-stu-id="6bf15-158">Make note of hello end date and hello password for hello .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="6bf15-159">Należy je poniżej.</span><span class="sxs-lookup"><span data-stu-id="6bf15-159">You will need them below.</span></span>

<span data-ttu-id="6bf15-160">Aby uzyskać więcej informacji na temat tworzenia certyfikatu testowego, zobacz [porady: tworzenie swój własny testu certyfikatu](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="6bf15-160">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="6bf15-161">**Skojarz hello certyfikat przy użyciu aplikacji do usługi Azure AD** teraz, certyfikatu, należy tooassociate go przy użyciu aplikacji do usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bf15-161">**Associate hello Certificate with an Azure AD application** Now that you have a certificate, you need tooassociate it with an Azure AD application.</span></span> <span data-ttu-id="6bf15-162">Obecnie usługa hello Azure Portal nie obsługuje tego przepływu pracy; Można to wykonać za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6bf15-162">Presently, hello Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="6bf15-163">Uruchom hello następujące polecenia tooassoicate hello certyfikatu z aplikacji hello Azure AD:</span><span class="sxs-lookup"><span data-stu-id="6bf15-163">Run hello following commands tooassoicate hello certificate with hello Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get hello thumbprint toouse in your app settings
    $x509.Thumbprint

<span data-ttu-id="6bf15-164">Po uruchomieniu tych poleceń, widać aplikacji hello w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6bf15-164">After you have run these commands, you can see hello application in Azure AD.</span></span> <span data-ttu-id="6bf15-165">Podczas wyszukiwania, upewnij się, że wybierz "Moja firma jest właścicielem aplikacji" zamiast "Korzysta z aplikacji firmy" w oknie dialogowym wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="6bf15-165">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in hello search dialog.</span></span>

<span data-ttu-id="6bf15-166">Zobacz toolearn więcej informacji na temat obiektów aplikacji w usłudze Azure AD i obiekty ServicePrincipal [obiekty aplikacji i nazwy głównej usługi](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="6bf15-166">toolearn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="6bf15-167">**Dodaj kod tooyour aplikacji sieci Web toouse hello certyfikatu** teraz dodamy kod tooyour aplikacji sieci Web tooaccess hello certyfikatu i użyć jej do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="6bf15-167">**Add code tooyour Web App toouse hello Certificate** Now we will add code tooyour Web App tooaccess hello cert and use it for authentication.</span></span>

<span data-ttu-id="6bf15-168">Najpierw jest kod tooaccess hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="6bf15-168">First there is code tooaccess hello cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since hello test root isn't installed.
                if (col == null || col.Count == 0)
                    return null;
                return col[0];
            }
            finally
            {
                store.Close();
            }
        }
    }


<span data-ttu-id="6bf15-169">Należy zauważyć, że ten hello StoreLocation jest CurrentUser zamiast LocalMachine.</span><span class="sxs-lookup"><span data-stu-id="6bf15-169">Note that hello StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="6bf15-170">I czy są firma Microsoft udostępnia toohello 'false' znaleźć metody, ponieważ użyto certyfikatu testowego.</span><span class="sxs-lookup"><span data-stu-id="6bf15-170">And that we are supplying 'false' toohello Find method because we are using a test cert.</span></span>

<span data-ttu-id="6bf15-171">Następnie jest kod, który używa hello CertificateHelper i tworzy ClientAssertionCertificate, który jest wymagany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="6bf15-171">Next is code that uses hello CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="6bf15-172">Oto hello nowy kod tooget hello token dostępu.</span><span class="sxs-lookup"><span data-stu-id="6bf15-172">Here is hello new code tooget hello access token.</span></span> <span data-ttu-id="6bf15-173">Spowoduje to zastąpienie hello GetToken — metoda powyżej.</span><span class="sxs-lookup"><span data-stu-id="6bf15-173">This replaces hello GetToken method above.</span></span> <span data-ttu-id="6bf15-174">Przyznanymi I on inną nazwę dla wygody.</span><span class="sxs-lookup"><span data-stu-id="6bf15-174">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="6bf15-175">I umieszczono wszystkie ten kod do klasy witryny projektu aplikacji sieci Web dla łatwość użycia.</span><span class="sxs-lookup"><span data-stu-id="6bf15-175">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="6bf15-176">Ostatnia zmiana kodu Hello jest hello metody Application_Start.</span><span class="sxs-lookup"><span data-stu-id="6bf15-176">hello last code change is in hello Application_Start method.</span></span> <span data-ttu-id="6bf15-177">Najpierw musimy hello toocall GetCert() metody tooload hello ClientAssertionCertificate.</span><span class="sxs-lookup"><span data-stu-id="6bf15-177">First we need toocall hello GetCert() method tooload hello ClientAssertionCertificate.</span></span> <span data-ttu-id="6bf15-178">A następnie zmień firma Microsoft hello metody wywołania zwrotnego, która dostarczamy podczas tworzenia nowego KeyVaultClient.</span><span class="sxs-lookup"><span data-stu-id="6bf15-178">And then we change hello callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="6bf15-179">Należy pamiętać, że spowoduje to zastąpienie kod hello było powyżej.</span><span class="sxs-lookup"><span data-stu-id="6bf15-179">Note that this replaces hello code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="6bf15-180">**Dodaj certyfikat tooyour aplikacji sieci Web za pośrednictwem portalu Azure hello** Dodawanie certyfikatu tooyour aplikacji sieci Web jest procesem dwuetapowym proste.</span><span class="sxs-lookup"><span data-stu-id="6bf15-180">**Add a Certificate tooyour Web App through hello Azure Portal** Adding a Certificate tooyour Web App is a simple two-step process.</span></span> <span data-ttu-id="6bf15-181">Najpierw należy przejść toohello portalu Azure i przejdź tooyour aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6bf15-181">First, go toohello Azure Portal and navigate tooyour Web App.</span></span> <span data-ttu-id="6bf15-182">W bloku ustawienia hello dla aplikacji sieci Web kliknij wpis hello "domen niestandardowych i SSL".</span><span class="sxs-lookup"><span data-stu-id="6bf15-182">On hello Settings blade for your Web App, click on hello entry for "Custom domains and SSL".</span></span> <span data-ttu-id="6bf15-183">Na powitania bloku, który zostanie otwarty, możesz być hello tooupload stanie certyfikatu utworzoną wcześniej KVWebApp.pfx, upewnij się, czy pamiętasz hello hasła dla profilu pfx hello.</span><span class="sxs-lookup"><span data-stu-id="6bf15-183">On hello blade that opens you will be able tooupload hello Certificate that you created above, KVWebApp.pfx, make sure that you remember hello password for hello pfx.</span></span>

![Dodawanie certyfikatu tooa aplikacji sieci Web w hello portalu Azure][2]

<span data-ttu-id="6bf15-185">Witaj ostatnim zadaniem, które należy toodo jest tooadd tooyour ustawienie aplikacji sieci Web aplikacji, który ma hello nazwa witryny sieci Web\_obciążenia\_certyfikaty i wartość *.</span><span class="sxs-lookup"><span data-stu-id="6bf15-185">hello last thing that you need toodo is tooadd an Application Setting tooyour Web App that has hello name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="6bf15-186">Daje to pewność, że wszystkie certyfikaty zostały załadowane.</span><span class="sxs-lookup"><span data-stu-id="6bf15-186">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="6bf15-187">Jeśli chce się, że tooload hello tylko certyfikaty, które zostały przekazane, a następnie możesz wprowadzić rozdzielana przecinkami lista ich odciski palców.</span><span class="sxs-lookup"><span data-stu-id="6bf15-187">If you wanted tooload only hello Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="6bf15-188">toolearn więcej na temat dodawania tooa certyfikatów aplikacji sieci Web, zobacz [przy użyciu certyfikatów w aplikacjach witryn sieci Web Azure](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="6bf15-188">toolearn more about adding a Certificate tooa Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="6bf15-189">**Dodaj certyfikat tooKey magazynu jako klucz tajny** zamiast bezpośrednio przekazywania toohello Twojego certyfikatu usługi sieci Web aplikacji, należy go przechowywać w Key Vault jako klucz tajny i wdrożyć ją stamtąd.</span><span class="sxs-lookup"><span data-stu-id="6bf15-189">**Add a Certificate tooKey Vault as a secret** Instead of uploading your certificate toohello Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="6bf15-190">To jest procesem dwuetapowym, opisaną w powitania po wpis w blogu, [wdrażanie Azure certyfikatu aplikacji sieci Web za pomocą usługi Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="6bf15-190">This is a two-step process that is outlined in hello following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="6bf15-191"><a id="next"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6bf15-191"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="6bf15-192">Odwołania dotyczące programowania, zobacz [Azure Key Vault klienta interfejsu API odwołanie w C#](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span><span class="sxs-lookup"><span data-stu-id="6bf15-192">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
