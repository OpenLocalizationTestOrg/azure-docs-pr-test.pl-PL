---
title: "aaaConnect bezpiecznie klastra sieci szkieletowej usług Azure tooan | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooauthenticate klienta dostępu do klastra usługi sieć szkieletowa tooa i w jaki sposób toosecure komunikacji między klientami i klastra."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 759a539e-e5e6-4055-bff5-d38804656e10
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 1b6a87a1fefaddce2043c604ca53751157232170
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-cluster"></a>Połącz tooa bezpiecznego klastra

Gdy klient nawiąże połączenie z węzłem klastra usługi sieć szkieletowa tooa, powitania klienta mogą być uwierzytelniane i bezpieczne komunikacji za pomocą certyfikatu zabezpieczeń lub Azure Active Directory (AAD). To uwierzytelnianie gwarantuje, że tylko autoryzowani użytkownicy mogą uzyskiwać dostęp do klastra hello i wdrożone aplikacje i wykonywanie zadań zarządzania.  Certyfikat lub zabezpieczeń usługi AAD musi być wcześniej włączone w klastrze hello podczas tworzenia klastra hello.  Aby uzyskać więcej informacji na temat scenariuszy zabezpieczeń klastra zobacz [klastra zabezpieczeń](service-fabric-cluster-security.md). W przypadku łączenia klastrów tooa zabezpieczone za pomocą certyfikatów, [skonfigurować certyfikat klienta na powitania](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) na powitania komputer, który łączy toohello klastra. 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a>Połącz tooa klastra bezpiecznego przy użyciu wiersza polecenia platformy Azure Usługa sieci szkieletowej (sfctl)

Istnieje kilka różnych sposobów tooconnect tooa bezpiecznego klastra przy użyciu hello usługi sieci szkieletowej interfejsu wiersza polecenia (sfctl). Podczas uwierzytelniania przy użyciu certyfikatu klienta, certyfikat hello szczegóły musi być taka sama certyfikat wdrożony toohello węzłów klastra. Jeśli certyfikat ma urzędy certyfikacji (CA), należy tooadditionally Określ hello zaufanych urzędów certyfikacji.

Możesz połączyć tooa klastra przy użyciu hello `sfctl cluster select` polecenia.

Certyfikaty klienta można określić w dwóch różnych fashions, jako para certyfikatu i klucza, lub jako plik pem pojedynczego. Dla chronionych hasłem `pem` pliki, można automatycznie monit tooenter hello hasła.

toospecify powitania klienta certyfikat jako plik pem, określ ścieżkę do pliku hello w hello `--pem` argumentu. Na przykład:

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Pliki pem chronione hasłem wyświetli monit o podanie toorunning poprzednich haseł w dowolnym poleceniu.

toospecify cert pary kluczy Użyj hello `--cert` i `--key` argumenty toospecify hello ścieżki tooeach odpowiedniego pliku.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

Czasami używane certyfikaty toosecure testu lub klastry deweloperów wystąpi niepowodzenie weryfikacji certyfikatu. toobypass certyfikatu weryfikacji, określ hello `--no-verify` opcji. Na przykład:

> [!WARNING]
> Nie używaj hello `no-verify` podczas łączenia klastrów sieci szkieletowej usług tooproduction.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

Ponadto można określić ścieżki toodirectories zaufane certyfikaty urzędu certyfikacji lub poszczególne certyfikaty. toospecify tych ścieżek, użyj hello `--ca` argumentu. Na przykład:

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

Po nawiązaniu połączenia można zbyt[innych poleceń sfctl](service-fabric-cli.md) toointeract hello klastra.

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a>Połącz tooa klastra przy użyciu programu PowerShell
Przed wykonaniem operacji w klastrze za pomocą programu PowerShell nawiązania połączenia toohello klastra. połączenia klastra Hello jest używany dla wszystkich kolejnych poleceń w hello podane sesji programu PowerShell.

### <a name="connect-tooan-unsecure-cluster"></a>Połącz tooan niezabezpieczone klastra

tooan tooconnect niezabezpieczone klastra, podaj toohello adres punktu końcowego klastra hello **Connect-ServiceFabricCluster** polecenia:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>Połącz tooa klastra bezpiecznego przy użyciu usługi Azure Active Directory

tooconnect tooa bezpiecznego klastra, który używa usługi Azure Active Directory dostępu administratora klastra tooauthorize, podaj odcisk palca certyfikatu klastra hello i użyj hello *usługi AzureActiveDirectory* flagi.  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Połącz klaster bezpiecznego tooa przy użyciu certyfikatu klienta
Hello uruchom następujące polecenia programu PowerShell tooa tooconnect bezpiecznego klastra, który używa dostępu administratora tooauthorize certyfikaty klienta. Podaj odcisk palca certyfikatu klastra hello i hello odcisk palca certyfikatu klienta hello, któremu przyznano uprawnienia do zarządzania klastrem. Szczegóły certyfikatu Hello zgodny z certyfikatem w węzłach klastra hello.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

*ServerCertThumbprint* jest hello odcisk palca certyfikatu serwera hello zainstalowanych w węzłach klastra hello. *FindValue* jest hello odcisk palca certyfikatu klienta hello administratora.
Po wypełnieniu hello parametrów polecenia hello wygląda hello poniższy przykład: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a>Połącz tooa klastra bezpiecznego przy użyciu usługi Active Directory systemu Windows
Jeśli klaster autonomiczny jest wdrażana przy użyciu zabezpieczeń usługi AD, należy połączyć toohello klastra przez dodanie przełącznika hello "WindowsCredential".

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a>Połącz tooa klastra przy użyciu powitania klienta fabricclient z rolą interfejsów API
Witaj zestawu SDK usług sieci szkieletowej udostępnia hello [klienta fabricclient z rolą](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) klasy do zarządzania klastrem. toouse powitania klienta fabricclient z rolą interfejsów API, Pobierz pakiet Microsoft.ServiceFabric NuGet hello.

### <a name="connect-tooan-unsecure-cluster"></a>Połącz tooan niezabezpieczone klastra

tooconnect tooa niezabezpieczona klastra zdalnego, Utwórz wystąpienie klienta fabricclient z rolą i podaj adres klastra hello:

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

Kod, który działa z w klastrze, na przykład w niezawodnej usługi, utworzyć klienta fabricclient z rolą *bez* określenie hello adres klastra. Klienta fabricclient z rolą łączy toohello lokalnego zarządzania bramy na kod hello węzła hello jest obecnie uruchomiony w, unikając przeskoku dodatkowe sieci.

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Połącz klaster bezpiecznego tooa przy użyciu certyfikatu klienta

Hello węzłów w klastrze hello musi mieć prawidłowe certyfikaty, których nazwa pospolita lub nazwa DNS w sieci SAN jest wyświetlana w hello [właściwości RemoteCommonNames](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) ustawiać [klienta fabricclient z rolą](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient). Następujące ten proces umożliwia uwierzytelnianie wzajemne między powitania klienta i hello węzłów klastra.

```csharp
using System.Fabric;
using System.Security.Cryptography.X509Certificates;

string clientCertThumb = "71DE04467C9ED0544D021098BCD44C71E183414E";
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string CommonName = "www.clustername.westus.azure.com";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var xc = GetCredentials(clientCertThumb, serverCertThumb, CommonName);
var fc = new FabricClient(xc, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

static X509Credentials GetCredentials(string clientCertThumb, string serverCertThumb, string name)
{
    X509Credentials xc = new X509Credentials();
    xc.StoreLocation = StoreLocation.CurrentUser;
    xc.StoreName = "My";
    xc.FindType = X509FindType.FindByThumbprint;
    xc.FindValue = clientCertThumb;
    xc.RemoteCommonNames.Add(name);
    xc.RemoteCertThumbprints.Add(serverCertThumb);
    xc.ProtectionLevel = ProtectionLevel.EncryptAndSign;
    return xc;
}
```

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a>Połącz tooa klastra bezpiecznego interaktywnego przy użyciu usługi Azure Active Directory

powitania po przykład używa usługi Azure Active Directory dla tożsamości i serwer certyfikat klienta dla tożsamości serwera.

Okno dialogowe automatycznie wyskakującej do interakcyjnego logowania po połączeniu toohello klastra.

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}
```

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a>Połącz tooa klastra bezpiecznego nieinteraktywnie przy użyciu usługi Azure Active Directory

Witaj poniższy przykład zależy od Microsoft.IdentityModel.Clients.ActiveDirectory, wersja: 2.19.208020213.

Aby uzyskać więcej informacji na przejęcie tokenu usługi AAD, zobacz [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).

```csharp
string tenantId = "C15CFCEA-02C1-40DC-8466-FBD0EE0B05D2";
string clientApplicationId = "118473C2-7619-46E3-A8E4-6DA8D5F56E12";
string webApplicationId = "53E6948C-0897-4DA6-B26A-EE2A38A690B4";

string token = GetAccessToken(
    tenantId,
    webApplicationId,
    clientApplicationId,
    "urn:ietf:wg:oauth:2.0:oob");

string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);
claimsCredentials.LocalClaims = token;

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(
    string tenantId,
    string resource,
    string clientId,
    string redirectUri)
{
    string authorityFormat = @"https://login.microsoftonline.com/{0}";
    string authority = string.Format(CultureInfo.InvariantCulture, authorityFormat, tenantId);
    var authContext = new AuthenticationContext(authority);

    var authResult = authContext.AcquireToken(
        resource,
        clientId,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a>Połącz tooa bezpiecznego klastra bez uprzedniego metadanych wiedzy przy użyciu usługi Azure Active Directory

Witaj poniższy przykład korzysta z podejścia nieinterakcyjnego nabycia tokenu, ale hello same podejście może być toobuild używane środowisko niestandardowych interakcyjne nabycia tokenu. Metadane usługi Azure Active Directory Hello wymagane uzyskania tokenu są odczytywane z konfiguracji klastra.

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

fc.ClaimsRetrieval += (o, e) =>
{
    return GetAccessToken(e.AzureActiveDirectoryMetadata);
};

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(AzureActiveDirectoryMetadata aad)
{
    var authContext = new AuthenticationContext(aad.Authority);

    var authResult = authContext.AcquireToken(
        aad.ClusterApplication,
        aad.ClientApplication,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

<a id="connectsecureclustersfx"></a>

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a>Połącz klaster bezpiecznego tooa za pomocą Eksploratora usługi sieć szkieletowa
tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) danego klastra można wskazać w przeglądarce do:

`http://<your-cluster-endpoint>:19080/Explorer`

pełny adres URL Hello jest również dostępna w okienku essentials klastra hello hello portalu Azure.

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>Połącz tooa klastra bezpiecznego przy użyciu usługi Azure Active Directory

tooconnect tooa klastra, który jest zabezpieczony przy użyciu usługi AAD, pkt przeglądarkę, aby:

`https://<your-cluster-endpoint>:19080/Explorer`

Są automatycznie jest monitem toolog się przy użyciu usługi AAD.

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Połącz klaster bezpiecznego tooa przy użyciu certyfikatu klienta

tooconnect tooa klastra, który jest zabezpieczony za pomocą certyfikatów, punkt przeglądarkę, aby:

`https://<your-cluster-endpoint>:19080/Explorer`

Są automatycznie jest tooselect zostanie wyświetlony monit o certyfikat klienta.

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a>Konfigurowanie certyfikatu klienta na komputerze zdalnym hello
Co najmniej dwa certyfikaty powinny być używane do zabezpieczania hello klastra dla certyfikatu hello klastra i serwera i drugi dla dostępu klientów.  Zalecamy również użycie dodatkowych dodatkowej certyfikatów i certyfikaty dostępu klienta.  toosecure hello komunikacji między klientem a węzeł klastra przy użyciu certyfikatu zabezpieczeń, należy najpierw tooobtain i zainstalować certyfikat klienta na powitania. Witaj certyfikat może być zainstalowany w hello (Mój) magazynie osobistym komputera lokalnego hello lub hello bieżącego użytkownika.  Należy również hello odcisk palca certyfikatu serwera hello tak, aby hello klienta można uwierzytelniać hello klastra.

Uruchom powitania po tooset polecenia cmdlet programu PowerShell hello certyfikatu klienta na komputerze hello, z którego korzystasz hello klastra.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

Jeśli certyfikat z podpisem własnym, należy tooimport przechowywać go tooyour maszyny "zaufanych osób" zanim będzie możliwe użycie tego certyfikatu tooconnect tooa bezpiecznego klastra.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a>Następne kroki

* [Proces uaktualniania klastra sieci szkieletowej usług oraz oczekiwań od użytkownika](service-fabric-cluster-upgrade.md)
* [Zarządzanie aplikacji usługi Service Fabric w programie Visual Studio](service-fabric-manage-application-in-visual-studio.md)
* [Wprowadzenie modelu kondycji sieci szkieletowej usług](service-fabric-health-introduction.md)
* [Zabezpieczenia aplikacji i Uruchom jako](service-fabric-application-runas-security.md)
* [Getting started with Service Fabric CLI (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)](service-fabric-cli.md)
