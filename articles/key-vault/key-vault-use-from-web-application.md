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
# <a name="use-azure-key-vault-from-a-web-application"></a>Użyj usługi Azure Key Vault z aplikacji sieci Web
## <a name="introduction"></a>Wprowadzenie
Użyj tego samouczka toohelp dowiesz się, jak toouse Azure klucza magazynu z aplikacji sieci web na platformie Azure. Przeprowadza użytkownika przez proces hello uzyskiwania dostępu do klucza tajnego z magazynu kluczy Azure, dzięki czemu mogą być używane w aplikacji sieci web.

**Szacowany czas toocomplete:** 15 minut

Aby uzyskać ogólne informacje na temat usługi Azure Key Vault, zobacz [Co to jest usługa Azure Key Vault?](key-vault-whatis.md)

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete tego samouczka, musi mieć następujące hello:

* Identyfikator URI tooa klucza tajnego w magazynie kluczy Azure
* Identyfikator klienta i klucz tajny klienta dla aplikacji sieci web w zarejestrowany w usłudze Azure Active Directory, zawierający tooyour dostępu do magazynu kluczy
* Aplikacja sieci web. Firma Microsoft będzie wyświetlane hello kroki dla aplikacji platformy ASP.NET MVC wdrożona na platformie Azure jako aplikacji sieci Web.

> [!NOTE]
> Jest to, że zostały wykonane kroki hello na liście [wprowadzenie do usługi Azure Key Vault](key-vault-get-started.md) w tym samouczku, aby mieć hello klucz tajny tooa identyfikatora URI i hello identyfikator klienta i klucz tajny klienta dla aplikacji sieci web.
> 
> 

Aplikacja sieci web Hello będą uzyskiwać dostęp do usługi Key Vault hello jest hello, co jest zarejestrowany w usłudze Azure Active Directory, która została podana tooyour dostępu do magazynu kluczy. Jeśli nie jest to hello, wróć tooRegister aplikację w Samouczek wprowadzający hello i powtórz kroki hello na liście.

Ten samouczek jest przeznaczony dla deweloperów sieci web, które rozumieją hello podstawy tworzenia aplikacji sieci web na platformie Azure. Aby uzyskać więcej informacji dotyczących aplikacji sieci Web platformy Azure, zobacz [Omówienie aplikacji sieci Web](../app-service-web/app-service-web-overview.md).

## <a id="packages"></a>Dodawanie pakietów Nuget
Istnieją dwa pakiety, które toohave zainstalowanych aplikacji sieci web.

* Biblioteki uwierzytelniania usługi Active Directory - zawiera metody interakcji z usługą Azure Active Directory i Zarządzanie tożsamościami użytkowników
* Biblioteka magazynu Azure klucza — zawiera metody interakcji z usługą Azure Key Vault

Oba te pakiety można zainstalować przy użyciu konsoli Menedżera pakietów za pomocą polecenia Install-Package hello hello.

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <a id="webconfig"></a>Modyfikowanie pliku Web.Config
Istnieją trzy ustawienia aplikacji, które należy pliku web.config dodano toohello toobe w następujący sposób.

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


Jeśli nie ma toohost aplikacji jako aplikacji sieci Web platformy Azure, należy dodać hello rzeczywiste ClientId, klucz tajny klienta i identyfikator URI klucza tajnego wartości toohello pliku web.config. W przeciwnym razie pozostaw te wartości fikcyjny ponieważ dodamy hello wartości rzeczywistych w hello Azure Portal dodatkowy poziom zabezpieczeń.

## <a id="gettoken"></a>Dodaj Token dostępu tooGet — metoda
W kolejności toouse hello klucz API magazynu należy tokenu dostępu. Witaj klucz magazynu klienta obsługuje wywołania toohello klucz API magazynu, ale konieczne toosupply go przy użyciu funkcji, który pobiera token dostępu hello.  

Poniżej znajduje się hello kodu tooget token dostępu z usługi Azure Active Directory. Ten kod może przejść w dowolne miejsce w aplikacji. Podoba tooadd witryny lub EncryptionHelper klasy.  

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
> Przy użyciu Identyfikatora klienta i klucz tajny klienta jest hello Najprostszym sposobem tooauthenticate aplikacji usługi Azure AD. I używania go w aplikacji sieci web umożliwia rozdzielenie obowiązków i większą kontrolę nad zarządzania infrastrukturą kluczy. Jednak zależne umieszczanie hello klucz tajny klienta w ustawieniach konfiguracji, które może być ryzykowne jako jako wprowadzanie hasła hello mają tooprotect w ustawieniach konfiguracji dla niektórych. Poniżej znajduje się omówione jak toouse identyfikator klienta i certyfikatu, a identyfikator klienta i klucz tajny klienta tooauthenticate hello aplikacji usługi Azure AD.
> 
> 

## <a id="appstart"></a>Pobierz klucz tajny hello Start aplikacji
Teraz możemy muszą kodu hello toocall interfejsu API magazynu kluczy i pobrać hello klucz tajny. Witaj następujący kod mogą być przełączane gdziekolwiek tak długo, jak jest ona wywoływana przed toouse go. Zostało umieszczone ten kod w przypadku uruchomienia aplikacji hello w pliku Global.asax hello, tak aby raz uruchamia się po uruchomieniu i klucz tajny dostępnych dla aplikacji hello hello sprawia, że.

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <a id="portalsettings"></a>Dodawanie ustawienia aplikacji w hello portalu Azure (opcjonalnie)
Jeśli masz aplikacji sieci Web platformy Azure można teraz dodawać hello rzeczywiste wartości hello AppSettings w hello portalu Azure. Dzięki temu wartości rzeczywistych hello nie będzie w pliku web.config hello, ale chronione za pomocą hello portalu, gdzie masz dostęp do osobnych możliwości kontroli. Te wartości zostaną zastąpione hello wartości, które zostały wprowadzone w pliku web.config. Upewnij się, nazwy hello są hello takie same.

![Ustawienia aplikacji wyświetlane w portalu Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a>Uwierzytelnianie przy użyciu certyfikatu zamiast klucz tajny klienta
Inny sposób tooauthenticate aplikacji usługi Azure AD jest przy użyciu Identyfikatora klienta oraz certyfikatu zamiast z Identyfikatorem klienta i klucz tajny klienta. Poniżej są hello toouse kroki certyfikatu w aplikacji sieci Web platformy Azure:

1. Uzyskaj lub Utwórz certyfikat
2. Skojarz hello certyfikat przy użyciu aplikacji do usługi Azure AD
3. Dodaj kod tooyour aplikacji sieci Web toouse hello certyfikatu
4. Dodaj certyfikat tooyour aplikacji sieci Web

**Uzyskaj lub Utwórz certyfikat** dla naszych celów firma Microsoft będzie wprowadzać certyfikatu testowego. Oto kilka poleceń, w której można w toocreate wiersza polecenia dewelopera certyfikatu. Utworzone pliki certyfikatu hello toowhere katalogu zmiany.  Ponadto dla hello otwierające i zamykające Data certyfikatu hello, użyj hello bieżącą datę i 1 rok.

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

Zwróć uwagę na datę zakończenia hello i hello hasło PFX hello (w tym przykładzie: 2016-07-31 i test123). Należy je poniżej.

Aby uzyskać więcej informacji na temat tworzenia certyfikatu testowego, zobacz [porady: tworzenie swój własny testu certyfikatu](https://msdn.microsoft.com/library/ff699202.aspx)

**Skojarz hello certyfikat przy użyciu aplikacji do usługi Azure AD** teraz, certyfikatu, należy tooassociate go przy użyciu aplikacji do usługi Azure AD. Obecnie usługa hello Azure Portal nie obsługuje tego przepływu pracy; Można to wykonać za pomocą programu PowerShell. Uruchom hello następujące polecenia tooassoicate hello certyfikatu z aplikacji hello Azure AD:

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

Po uruchomieniu tych poleceń, widać aplikacji hello w usłudze Azure AD. Podczas wyszukiwania, upewnij się, że wybierz "Moja firma jest właścicielem aplikacji" zamiast "Korzysta z aplikacji firmy" w oknie dialogowym wyszukiwania hello.

Zobacz toolearn więcej informacji na temat obiektów aplikacji w usłudze Azure AD i obiekty ServicePrincipal [obiekty aplikacji i nazwy głównej usługi](../active-directory/active-directory-application-objects.md)

**Dodaj kod tooyour aplikacji sieci Web toouse hello certyfikatu** teraz dodamy kod tooyour aplikacji sieci Web tooaccess hello certyfikatu i użyć jej do uwierzytelniania.

Najpierw jest kod tooaccess hello certyfikatu.

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


Należy zauważyć, że ten hello StoreLocation jest CurrentUser zamiast LocalMachine. I czy są firma Microsoft udostępnia toohello 'false' znaleźć metody, ponieważ użyto certyfikatu testowego.

Następnie jest kod, który używa hello CertificateHelper i tworzy ClientAssertionCertificate, który jest wymagany do uwierzytelniania.

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


Oto hello nowy kod tooget hello token dostępu. Spowoduje to zastąpienie hello GetToken — metoda powyżej. Przyznanymi I on inną nazwę dla wygody.

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

I umieszczono wszystkie ten kod do klasy witryny projektu aplikacji sieci Web dla łatwość użycia.

Ostatnia zmiana kodu Hello jest hello metody Application_Start. Najpierw musimy hello toocall GetCert() metody tooload hello ClientAssertionCertificate. A następnie zmień firma Microsoft hello metody wywołania zwrotnego, która dostarczamy podczas tworzenia nowego KeyVaultClient. Należy pamiętać, że spowoduje to zastąpienie kod hello było powyżej.

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


**Dodaj certyfikat tooyour aplikacji sieci Web za pośrednictwem portalu Azure hello** Dodawanie certyfikatu tooyour aplikacji sieci Web jest procesem dwuetapowym proste. Najpierw należy przejść toohello portalu Azure i przejdź tooyour aplikacji sieci Web. W bloku ustawienia hello dla aplikacji sieci Web kliknij wpis hello "domen niestandardowych i SSL". Na powitania bloku, który zostanie otwarty, możesz być hello tooupload stanie certyfikatu utworzoną wcześniej KVWebApp.pfx, upewnij się, czy pamiętasz hello hasła dla profilu pfx hello.

![Dodawanie certyfikatu tooa aplikacji sieci Web w hello portalu Azure][2]

Witaj ostatnim zadaniem, które należy toodo jest tooadd tooyour ustawienie aplikacji sieci Web aplikacji, który ma hello nazwa witryny sieci Web\_obciążenia\_certyfikaty i wartość *. Daje to pewność, że wszystkie certyfikaty zostały załadowane. Jeśli chce się, że tooload hello tylko certyfikaty, które zostały przekazane, a następnie możesz wprowadzić rozdzielana przecinkami lista ich odciski palców.

toolearn więcej na temat dodawania tooa certyfikatów aplikacji sieci Web, zobacz [przy użyciu certyfikatów w aplikacjach witryn sieci Web Azure](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)

**Dodaj certyfikat tooKey magazynu jako klucz tajny** zamiast bezpośrednio przekazywania toohello Twojego certyfikatu usługi sieci Web aplikacji, należy go przechowywać w Key Vault jako klucz tajny i wdrożyć ją stamtąd. To jest procesem dwuetapowym, opisaną w powitania po wpis w blogu, [wdrażanie Azure certyfikatu aplikacji sieci Web za pomocą usługi Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)

## <a id="next"></a>Następne kroki
Odwołania dotyczące programowania, zobacz [Azure Key Vault klienta interfejsu API odwołanie w C#](https://msdn.microsoft.com/library/azure/dn903628.aspx).

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
