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
# <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="88b3d-103">Połącz tooa bezpiecznego klastra</span><span class="sxs-lookup"><span data-stu-id="88b3d-103">Connect tooa secure cluster</span></span>

<span data-ttu-id="88b3d-104">Gdy klient nawiąże połączenie z węzłem klastra usługi sieć szkieletowa tooa, powitania klienta mogą być uwierzytelniane i bezpieczne komunikacji za pomocą certyfikatu zabezpieczeń lub Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="88b3d-104">When a client connects tooa Service Fabric cluster node, hello client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="88b3d-105">To uwierzytelnianie gwarantuje, że tylko autoryzowani użytkownicy mogą uzyskiwać dostęp do klastra hello i wdrożone aplikacje i wykonywanie zadań zarządzania.</span><span class="sxs-lookup"><span data-stu-id="88b3d-105">This authentication ensures that only authorized users can access hello cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="88b3d-106">Certyfikat lub zabezpieczeń usługi AAD musi być wcześniej włączone w klastrze hello podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="88b3d-106">Certificate or AAD security must have been previously enabled on hello cluster when hello cluster was created.</span></span>  <span data-ttu-id="88b3d-107">Aby uzyskać więcej informacji na temat scenariuszy zabezpieczeń klastra zobacz [klastra zabezpieczeń](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="88b3d-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="88b3d-108">W przypadku łączenia klastrów tooa zabezpieczone za pomocą certyfikatów, [skonfigurować certyfikat klienta na powitania](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) na powitania komputer, który łączy toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="88b3d-108">If you are connecting tooa cluster secured with certificates, [set up hello client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on hello computer that connects toohello cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="88b3d-109">Połącz tooa klastra bezpiecznego przy użyciu wiersza polecenia platformy Azure Usługa sieci szkieletowej (sfctl)</span><span class="sxs-lookup"><span data-stu-id="88b3d-109">Connect tooa secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="88b3d-110">Istnieje kilka różnych sposobów tooconnect tooa bezpiecznego klastra przy użyciu hello usługi sieci szkieletowej interfejsu wiersza polecenia (sfctl).</span><span class="sxs-lookup"><span data-stu-id="88b3d-110">There are a few different ways tooconnect tooa secure cluster using hello Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="88b3d-111">Podczas uwierzytelniania przy użyciu certyfikatu klienta, certyfikat hello szczegóły musi być taka sama certyfikat wdrożony toohello węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="88b3d-111">When using a client certificate for authentication, hello certificate details must match a certificate deployed toohello cluster nodes.</span></span> <span data-ttu-id="88b3d-112">Jeśli certyfikat ma urzędy certyfikacji (CA), należy tooadditionally Określ hello zaufanych urzędów certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="88b3d-112">If your certificate has Certificate Authorities (CAs), you need tooadditionally specify hello trusted CAs.</span></span>

<span data-ttu-id="88b3d-113">Możesz połączyć tooa klastra przy użyciu hello `sfctl cluster select` polecenia.</span><span class="sxs-lookup"><span data-stu-id="88b3d-113">You can connect tooa cluster using hello `sfctl cluster select` command.</span></span>

<span data-ttu-id="88b3d-114">Certyfikaty klienta można określić w dwóch różnych fashions, jako para certyfikatu i klucza, lub jako plik pem pojedynczego.</span><span class="sxs-lookup"><span data-stu-id="88b3d-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="88b3d-115">Dla chronionych hasłem `pem` pliki, można automatycznie monit tooenter hello hasła.</span><span class="sxs-lookup"><span data-stu-id="88b3d-115">For password protected `pem` files, you will be prompted automatically tooenter hello password.</span></span>

<span data-ttu-id="88b3d-116">toospecify powitania klienta certyfikat jako plik pem, określ ścieżkę do pliku hello w hello `--pem` argumentu.</span><span class="sxs-lookup"><span data-stu-id="88b3d-116">toospecify hello client certificate as a pem file, specify hello file path in hello `--pem` argument.</span></span> <span data-ttu-id="88b3d-117">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="88b3d-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="88b3d-118">Pliki pem chronione hasłem wyświetli monit o podanie toorunning poprzednich haseł w dowolnym poleceniu.</span><span class="sxs-lookup"><span data-stu-id="88b3d-118">Password protected pem files will prompt for password prior toorunning any command.</span></span>

<span data-ttu-id="88b3d-119">toospecify cert pary kluczy Użyj hello `--cert` i `--key` argumenty toospecify hello ścieżki tooeach odpowiedniego pliku.</span><span class="sxs-lookup"><span data-stu-id="88b3d-119">toospecify a cert, key pair use hello `--cert` and `--key` arguments toospecify hello file paths tooeach respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="88b3d-120">Czasami używane certyfikaty toosecure testu lub klastry deweloperów wystąpi niepowodzenie weryfikacji certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="88b3d-120">Sometimes certificates used toosecure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="88b3d-121">toobypass certyfikatu weryfikacji, określ hello `--no-verify` opcji.</span><span class="sxs-lookup"><span data-stu-id="88b3d-121">toobypass certificate verification, specify hello `--no-verify` option.</span></span> <span data-ttu-id="88b3d-122">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="88b3d-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="88b3d-123">Nie używaj hello `no-verify` podczas łączenia klastrów sieci szkieletowej usług tooproduction.</span><span class="sxs-lookup"><span data-stu-id="88b3d-123">Do not use hello `no-verify` option when connecting tooproduction Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="88b3d-124">Ponadto można określić ścieżki toodirectories zaufane certyfikaty urzędu certyfikacji lub poszczególne certyfikaty.</span><span class="sxs-lookup"><span data-stu-id="88b3d-124">In addition, you can specify paths toodirectories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="88b3d-125">toospecify tych ścieżek, użyj hello `--ca` argumentu.</span><span class="sxs-lookup"><span data-stu-id="88b3d-125">toospecify these paths, use hello `--ca` argument.</span></span> <span data-ttu-id="88b3d-126">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="88b3d-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="88b3d-127">Po nawiązaniu połączenia można zbyt[innych poleceń sfctl](service-fabric-cli.md) toointeract hello klastra.</span><span class="sxs-lookup"><span data-stu-id="88b3d-127">After you connect, you should be able too[run other sfctl commands](service-fabric-cli.md) toointeract with hello cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a><span data-ttu-id="88b3d-128">Połącz tooa klastra przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="88b3d-128">Connect tooa cluster using PowerShell</span></span>
<span data-ttu-id="88b3d-129">Przed wykonaniem operacji w klastrze za pomocą programu PowerShell nawiązania połączenia toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="88b3d-129">Before you perform operations on a cluster through PowerShell, first establish a connection toohello cluster.</span></span> <span data-ttu-id="88b3d-130">połączenia klastra Hello jest używany dla wszystkich kolejnych poleceń w hello podane sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="88b3d-130">hello cluster connection is used for all subsequent commands in hello given PowerShell session.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="88b3d-131">Połącz tooan niezabezpieczone klastra</span><span class="sxs-lookup"><span data-stu-id="88b3d-131">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="88b3d-132">tooan tooconnect niezabezpieczone klastra, podaj toohello adres punktu końcowego klastra hello **Connect-ServiceFabricCluster** polecenia:</span><span class="sxs-lookup"><span data-stu-id="88b3d-132">tooconnect tooan unsecure cluster, provide hello cluster endpoint address toohello **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="88b3d-133">Połącz tooa klastra bezpiecznego przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88b3d-133">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="88b3d-134">tooconnect tooa bezpiecznego klastra, który używa usługi Azure Active Directory dostępu administratora klastra tooauthorize, podaj odcisk palca certyfikatu klastra hello i użyj hello *usługi AzureActiveDirectory* flagi.</span><span class="sxs-lookup"><span data-stu-id="88b3d-134">tooconnect tooa secure cluster that uses Azure Active Directory tooauthorize cluster administrator access, provide hello cluster certificate thumbprint and use hello *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="88b3d-135">Połącz klaster bezpiecznego tooa przy użyciu certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="88b3d-135">Connect tooa secure cluster using a client certificate</span></span>
<span data-ttu-id="88b3d-136">Hello uruchom następujące polecenia programu PowerShell tooa tooconnect bezpiecznego klastra, który używa dostępu administratora tooauthorize certyfikaty klienta.</span><span class="sxs-lookup"><span data-stu-id="88b3d-136">Run hello following PowerShell command tooconnect tooa secure cluster that uses client certificates tooauthorize administrator access.</span></span> <span data-ttu-id="88b3d-137">Podaj odcisk palca certyfikatu klastra hello i hello odcisk palca certyfikatu klienta hello, któremu przyznano uprawnienia do zarządzania klastrem.</span><span class="sxs-lookup"><span data-stu-id="88b3d-137">Provide hello cluster certificate thumbprint and hello thumbprint of hello client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="88b3d-138">Szczegóły certyfikatu Hello zgodny z certyfikatem w węzłach klastra hello.</span><span class="sxs-lookup"><span data-stu-id="88b3d-138">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="88b3d-139">*ServerCertThumbprint* jest hello odcisk palca certyfikatu serwera hello zainstalowanych w węzłach klastra hello.</span><span class="sxs-lookup"><span data-stu-id="88b3d-139">*ServerCertThumbprint* is hello thumbprint of hello server certificate installed on hello cluster nodes.</span></span> <span data-ttu-id="88b3d-140">*FindValue* jest hello odcisk palca certyfikatu klienta hello administratora.</span><span class="sxs-lookup"><span data-stu-id="88b3d-140">*FindValue* is hello thumbprint of hello admin client certificate.</span></span>
<span data-ttu-id="88b3d-141">Po wypełnieniu hello parametrów polecenia hello wygląda hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="88b3d-141">When hello parameters are filled in, hello command looks like hello following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="88b3d-142">Połącz tooa klastra bezpiecznego przy użyciu usługi Active Directory systemu Windows</span><span class="sxs-lookup"><span data-stu-id="88b3d-142">Connect tooa secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="88b3d-143">Jeśli klaster autonomiczny jest wdrażana przy użyciu zabezpieczeń usługi AD, należy połączyć toohello klastra przez dodanie przełącznika hello "WindowsCredential".</span><span class="sxs-lookup"><span data-stu-id="88b3d-143">If your standalone cluster is deployed using AD security, connect toohello cluster by appending hello switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a><span data-ttu-id="88b3d-144">Połącz tooa klastra przy użyciu powitania klienta fabricclient z rolą interfejsów API</span><span class="sxs-lookup"><span data-stu-id="88b3d-144">Connect tooa cluster using hello FabricClient APIs</span></span>
<span data-ttu-id="88b3d-145">Witaj zestawu SDK usług sieci szkieletowej udostępnia hello [klienta fabricclient z rolą](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) klasy do zarządzania klastrem.</span><span class="sxs-lookup"><span data-stu-id="88b3d-145">hello Service Fabric SDK provides hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="88b3d-146">toouse powitania klienta fabricclient z rolą interfejsów API, Pobierz pakiet Microsoft.ServiceFabric NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="88b3d-146">toouse hello FabricClient APIs, get hello Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="88b3d-147">Połącz tooan niezabezpieczone klastra</span><span class="sxs-lookup"><span data-stu-id="88b3d-147">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="88b3d-148">tooconnect tooa niezabezpieczona klastra zdalnego, Utwórz wystąpienie klienta fabricclient z rolą i podaj adres klastra hello:</span><span class="sxs-lookup"><span data-stu-id="88b3d-148">tooconnect tooa remote unsecured cluster, create a FabricClient instance and provide hello cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="88b3d-149">Kod, który działa z w klastrze, na przykład w niezawodnej usługi, utworzyć klienta fabricclient z rolą *bez* określenie hello adres klastra.</span><span class="sxs-lookup"><span data-stu-id="88b3d-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying hello cluster address.</span></span> <span data-ttu-id="88b3d-150">Klienta fabricclient z rolą łączy toohello lokalnego zarządzania bramy na kod hello węzła hello jest obecnie uruchomiony w, unikając przeskoku dodatkowe sieci.</span><span class="sxs-lookup"><span data-stu-id="88b3d-150">FabricClient connects toohello local management gateway on hello node hello code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="88b3d-151">Połącz klaster bezpiecznego tooa przy użyciu certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="88b3d-151">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="88b3d-152">Hello węzłów w klastrze hello musi mieć prawidłowe certyfikaty, których nazwa pospolita lub nazwa DNS w sieci SAN jest wyświetlana w hello [właściwości RemoteCommonNames](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) ustawiać [klienta fabricclient z rolą](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="88b3d-152">hello nodes in hello cluster must have valid certificates whose common name or DNS name in SAN appears in hello [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="88b3d-153">Następujące ten proces umożliwia uwierzytelnianie wzajemne między powitania klienta i hello węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="88b3d-153">Following this process enables mutual authentication between hello client and hello cluster nodes.</span></span>

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

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="88b3d-154">Połącz tooa klastra bezpiecznego interaktywnego przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88b3d-154">Connect tooa secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="88b3d-155">powitania po przykład używa usługi Azure Active Directory dla tożsamości i serwer certyfikat klienta dla tożsamości serwera.</span><span class="sxs-lookup"><span data-stu-id="88b3d-155">hello following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="88b3d-156">Okno dialogowe automatycznie wyskakującej do interakcyjnego logowania po połączeniu toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="88b3d-156">A dialog window automatically pops up for interactive sign-in upon connecting toohello cluster.</span></span>

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

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="88b3d-157">Połącz tooa klastra bezpiecznego nieinteraktywnie przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88b3d-157">Connect tooa secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="88b3d-158">Witaj poniższy przykład zależy od Microsoft.IdentityModel.Clients.ActiveDirectory, wersja: 2.19.208020213.</span><span class="sxs-lookup"><span data-stu-id="88b3d-158">hello following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="88b3d-159">Aby uzyskać więcej informacji na przejęcie tokenu usługi AAD, zobacz [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span><span class="sxs-lookup"><span data-stu-id="88b3d-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

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

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="88b3d-160">Połącz tooa bezpiecznego klastra bez uprzedniego metadanych wiedzy przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88b3d-160">Connect tooa secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="88b3d-161">Witaj poniższy przykład korzysta z podejścia nieinterakcyjnego nabycia tokenu, ale hello same podejście może być toobuild używane środowisko niestandardowych interakcyjne nabycia tokenu.</span><span class="sxs-lookup"><span data-stu-id="88b3d-161">hello following example uses non-interactive token acquisition, but hello same approach can be used toobuild a custom interactive token acquisition experience.</span></span> <span data-ttu-id="88b3d-162">Metadane usługi Azure Active Directory Hello wymagane uzyskania tokenu są odczytywane z konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="88b3d-162">hello Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

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

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="88b3d-163">Połącz klaster bezpiecznego tooa za pomocą Eksploratora usługi sieć szkieletowa</span><span class="sxs-lookup"><span data-stu-id="88b3d-163">Connect tooa secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="88b3d-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) danego klastra można wskazać w przeglądarce do:</span><span class="sxs-lookup"><span data-stu-id="88b3d-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="88b3d-165">pełny adres URL Hello jest również dostępna w okienku essentials klastra hello hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="88b3d-165">hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="88b3d-166">Połącz tooa klastra bezpiecznego przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88b3d-166">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="88b3d-167">tooconnect tooa klastra, który jest zabezpieczony przy użyciu usługi AAD, pkt przeglądarkę, aby:</span><span class="sxs-lookup"><span data-stu-id="88b3d-167">tooconnect tooa cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="88b3d-168">Są automatycznie jest monitem toolog się przy użyciu usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="88b3d-168">You are automatically be prompted toolog in with AAD.</span></span>

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="88b3d-169">Połącz klaster bezpiecznego tooa przy użyciu certyfikatu klienta</span><span class="sxs-lookup"><span data-stu-id="88b3d-169">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="88b3d-170">tooconnect tooa klastra, który jest zabezpieczony za pomocą certyfikatów, punkt przeglądarkę, aby:</span><span class="sxs-lookup"><span data-stu-id="88b3d-170">tooconnect tooa cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="88b3d-171">Są automatycznie jest tooselect zostanie wyświetlony monit o certyfikat klienta.</span><span class="sxs-lookup"><span data-stu-id="88b3d-171">You are automatically be prompted tooselect a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a><span data-ttu-id="88b3d-172">Konfigurowanie certyfikatu klienta na komputerze zdalnym hello</span><span class="sxs-lookup"><span data-stu-id="88b3d-172">Set up a client certificate on hello remote computer</span></span>
<span data-ttu-id="88b3d-173">Co najmniej dwa certyfikaty powinny być używane do zabezpieczania hello klastra dla certyfikatu hello klastra i serwera i drugi dla dostępu klientów.</span><span class="sxs-lookup"><span data-stu-id="88b3d-173">At least two certificates should be used for securing hello cluster, one for hello cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="88b3d-174">Zalecamy również użycie dodatkowych dodatkowej certyfikatów i certyfikaty dostępu klienta.</span><span class="sxs-lookup"><span data-stu-id="88b3d-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="88b3d-175">toosecure hello komunikacji między klientem a węzeł klastra przy użyciu certyfikatu zabezpieczeń, należy najpierw tooobtain i zainstalować certyfikat klienta na powitania.</span><span class="sxs-lookup"><span data-stu-id="88b3d-175">toosecure hello communication between a client and a cluster node using certificate security, you first need tooobtain and install hello client certificate.</span></span> <span data-ttu-id="88b3d-176">Witaj certyfikat może być zainstalowany w hello (Mój) magazynie osobistym komputera lokalnego hello lub hello bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="88b3d-176">hello certificate can be installed into hello Personal (My) store of hello local computer or hello current user.</span></span>  <span data-ttu-id="88b3d-177">Należy również hello odcisk palca certyfikatu serwera hello tak, aby hello klienta można uwierzytelniać hello klastra.</span><span class="sxs-lookup"><span data-stu-id="88b3d-177">You also need hello thumbprint of hello server certificate so that hello client can authenticate hello cluster.</span></span>

<span data-ttu-id="88b3d-178">Uruchom powitania po tooset polecenia cmdlet programu PowerShell hello certyfikatu klienta na komputerze hello, z którego korzystasz hello klastra.</span><span class="sxs-lookup"><span data-stu-id="88b3d-178">Run hello following PowerShell cmdlet tooset up hello client certificate on hello computer from which you access hello cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="88b3d-179">Jeśli certyfikat z podpisem własnym, należy tooimport przechowywać go tooyour maszyny "zaufanych osób" zanim będzie możliwe użycie tego certyfikatu tooconnect tooa bezpiecznego klastra.</span><span class="sxs-lookup"><span data-stu-id="88b3d-179">If it is a self-signed certificate, you need tooimport it tooyour machine's "trusted people" store before you can use this certificate tooconnect tooa secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="88b3d-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="88b3d-180">Next steps</span></span>

* [<span data-ttu-id="88b3d-181">Proces uaktualniania klastra sieci szkieletowej usług oraz oczekiwań od użytkownika</span><span class="sxs-lookup"><span data-stu-id="88b3d-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="88b3d-182">Zarządzanie aplikacji usługi Service Fabric w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88b3d-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="88b3d-183">Wprowadzenie modelu kondycji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="88b3d-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="88b3d-184">Zabezpieczenia aplikacji i Uruchom jako</span><span class="sxs-lookup"><span data-stu-id="88b3d-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="88b3d-185">Getting started with Service Fabric CLI (Wprowadzenie do interfejsu wiersza polecenia usługi Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="88b3d-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
