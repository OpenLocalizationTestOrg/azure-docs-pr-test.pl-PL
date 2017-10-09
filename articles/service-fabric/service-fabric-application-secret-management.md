---
title: klucze tajne aaaManaging w aplikacjach platformy Service Fabric | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak wartości klucza tajnego toosecure w aplikacji sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 94a67e45-7094-4fbd-9c88-51f4fc3c523a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: b8cafcb681d95aaa1b8e9a1afaac78ba5b7f58b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="dcdbe-103">Zarządzanie kluczy tajnych w aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="dcdbe-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="dcdbe-104">Ten przewodnik przeprowadzi Cię przez kroki hello zarządzania kluczy tajnych w aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-104">This guide walks you through hello steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="dcdbe-105">Klucze tajne można poufne informacje, takie jak parametry połączenia magazynu, hasła lub inne wartości, które nie powinny być traktowane w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="dcdbe-106">W tym przewodniku używa usługi Azure Key Vault toomanage kluczy i kluczy tajnych.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-106">This guide uses Azure Key Vault toomanage keys and secrets.</span></span> <span data-ttu-id="dcdbe-107">Jednak *przy użyciu* kluczy tajnych w aplikacji jest chmury tooallow niezależny od platformy aplikacji toobe tooa wdrożonej klastra hostowanej dowolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-107">However, *using* secrets in an application is cloud platform-agnostic tooallow applications toobe deployed tooa cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="dcdbe-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="dcdbe-108">Overview</span></span>
<span data-ttu-id="dcdbe-109">Witaj ustawienia konfiguracji usługi toomanage zalecaną metodą jest użycie [usługi pakiety konfiguracji][config-package].</span><span class="sxs-lookup"><span data-stu-id="dcdbe-109">hello recommended way toomanage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="dcdbe-110">Pakiety konfiguracji są kontrolą wersji i nadaje się do aktualizacji za pomocą zarządzanego stopniowe z sprawdzania kondycji i automatycznego wycofywania.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="dcdbe-111">Jest to preferowany tooglobal konfiguracji zmniejsza ryzyko hello awarię usług globalnych.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-111">This is preferred tooglobal configuration as it reduces hello chances of a global service outage.</span></span> <span data-ttu-id="dcdbe-112">Zaszyfrowanych kluczy tajnych są żaden wyjątek.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="dcdbe-113">Sieć szkieletowa usług ma wbudowane funkcje szyfrowania i odszyfrowywania wartości w pliku Settings.xml pakietu konfiguracji przy użyciu certyfikatu szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="dcdbe-114">Witaj poniższym diagramie przedstawiono podstawowy przepływ hello tajny zarządzania w sieci szkieletowej usług aplikacji:</span><span class="sxs-lookup"><span data-stu-id="dcdbe-114">hello following diagram illustrates hello basic flow for secret management in a Service Fabric application:</span></span>

![Zarządzanie tajne — omówienie][overview]

<span data-ttu-id="dcdbe-116">W tym przepływie istnieją cztery główne kroki:</span><span class="sxs-lookup"><span data-stu-id="dcdbe-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="dcdbe-117">Uzyskaj certyfikat Szyfrowanie danych.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="dcdbe-118">Zainstaluj certyfikat hello w klastrze.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-118">Install hello certificate in your cluster.</span></span>
3. <span data-ttu-id="dcdbe-119">Szyfrowanie tajny wartości podczas wdrażania aplikacji przy użyciu certyfikatu hello i wstawić je do pliku konfiguracji Settings.xml usługi.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-119">Encrypt secret values when deploying an application with hello certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="dcdbe-120">Odczyt zaszyfrowanych wartości poza Settings.xml w tym celu odszyfrowuje z hello tego samego certyfikatu szyfrowanie.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-120">Read encrypted values out of Settings.xml by decrypting with hello same encipherment certificate.</span></span> 

<span data-ttu-id="dcdbe-121">[Usługa Azure Key Vault] [ key-vault-get-started] jest tu używany jako lokalizację bezpiecznego magazynu certyfikatów, a tooget sposób certyfikatów zainstalowanych na klastrów sieci szkieletowej usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way tooget certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="dcdbe-122">Jeśli nie są wdrażane tooAzure, nie trzeba toouse kluczy tajnych toomanage Key Vault w aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-122">If you are not deploying tooAzure, you do not need toouse Key Vault toomanage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="dcdbe-123">Certyfikat Szyfrowanie danych</span><span class="sxs-lookup"><span data-stu-id="dcdbe-123">Data encipherment certificate</span></span>
<span data-ttu-id="dcdbe-124">Certyfikat Szyfrowanie danych jest używane wyłącznie do szyfrowania i odszyfrowywania konfiguracji wartości w pliku Settings.xml usługi i nie jest używany do uwierzytelniania lub podpisywanie tekst zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="dcdbe-125">certyfikat Hello musi spełniać hello następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="dcdbe-125">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="dcdbe-126">Witaj, certyfikat musi zawierać klucz prywatny.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-126">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="dcdbe-127">Witaj certyfikatu musi zostać utworzony dla wymiany kluczy, można eksportować tooa plik wymiany informacji osobistych (pfx).</span><span class="sxs-lookup"><span data-stu-id="dcdbe-127">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="dcdbe-128">sposób użycia klucza certyfikatu Hello musi zawierać szyfrowanie danych (10) i nie powinna zawierać uwierzytelniania serwera lub uwierzytelniania klienta.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-128">hello certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="dcdbe-129">Na przykład podczas tworzenia certyfikatu z podpisem własnym za pomocą programu PowerShell, hello `KeyUsage` musi również ustawiona flaga`DataEncipherment`:</span><span class="sxs-lookup"><span data-stu-id="dcdbe-129">For example, when creating a self-signed certificate using PowerShell, hello `KeyUsage` flag must be set too`DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a><span data-ttu-id="dcdbe-130">Zainstaluj certyfikat hello w klastrze</span><span class="sxs-lookup"><span data-stu-id="dcdbe-130">Install hello certificate in your cluster</span></span>
<span data-ttu-id="dcdbe-131">Ten certyfikat należy zainstalować na każdym węźle klastra hello.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-131">This certificate must be installed on each node in hello cluster.</span></span> <span data-ttu-id="dcdbe-132">Będzie on używany w wartości toodecrypt środowiska uruchomieniowego przechowywanych w pliku Settings.xml usługi.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-132">It will be used at runtime toodecrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="dcdbe-133">Zobacz [jak toocreate klastra przy użyciu usługi Azure Resource Manager] [ service-fabric-cluster-creation-via-arm] instrukcje instalacji.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-133">See [how toocreate a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="dcdbe-134">Szyfrowanie hasła aplikacji</span><span class="sxs-lookup"><span data-stu-id="dcdbe-134">Encrypt application secrets</span></span>
<span data-ttu-id="dcdbe-135">Hello zestawu SDK sieci szkieletowej usług ma wbudowane funkcje tajny szyfrowania i odszyfrowywania.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-135">hello Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="dcdbe-136">Tajny wartości może być szyfrowane w czasie zbudowany odszyfrować i programowo odczytać w kodzie usługi.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="dcdbe-137">Witaj następującego polecenia programu PowerShell jest używane tooencrypt klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-137">hello following PowerShell command is used tooencrypt a secret.</span></span> <span data-ttu-id="dcdbe-138">To polecenie szyfruje wartości hello; robi **nie** zarejestrować hello tekst zaszyfrowany.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-138">This command only encrypts hello value; it does **not** sign hello cipher text.</span></span> <span data-ttu-id="dcdbe-139">Należy użyć hello tego samego certyfikatu szyfrowanie zainstalowanej w Twojej tekstu szyfrowanego tooproduce klastra tajny wartości:</span><span class="sxs-lookup"><span data-stu-id="dcdbe-139">You must use hello same encipherment certificate that is installed in your cluster tooproduce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="dcdbe-140">Witaj wynikowy ciąg base-64 zawiera zarówno tajny tekstu szyfrowanego hello, jak również informacje o certyfikacie hello, który był używany tooencrypt go.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-140">hello resulting base-64 string contains both hello secret ciphertext as well as information about hello certificate that was used tooencrypt it.</span></span>  <span data-ttu-id="dcdbe-141">Witaj zakodowanym ciągiem base-64 można wstawiać do parametru w pliku konfiguracji usługi Settings.xml hello `IsEncrypted` zbyt ustawiony atrybut`true`:</span><span class="sxs-lookup"><span data-stu-id="dcdbe-141">hello base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with hello `IsEncrypted` attribute set too`true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="dcdbe-142">Wstaw klucze tajne aplikacji do wystąpienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="dcdbe-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="dcdbe-143">W idealnym przypadku środowisk toodifferent wdrażania należy jak zautomatyzowane, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-143">Ideally, deployment toodifferent environments should be as automated as possible.</span></span> <span data-ttu-id="dcdbe-144">Można to zrobić wykonywania tajny szyfrowania w środowisku kompilacji i podając hello zaszyfrowanych kluczy tajnych jako parametry podczas tworzenia wystąpień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-144">This can be accomplished by performing secret encryption in a build environment and providing hello encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="dcdbe-145">Korzystanie z możliwym do zastąpienia parametrów w pliku Settings.xml</span><span class="sxs-lookup"><span data-stu-id="dcdbe-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="dcdbe-146">plik konfiguracji w pliku Settings.xml Hello umożliwia możliwością zastępowania parametrów, które można podać podczas tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-146">hello Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="dcdbe-147">Użyj hello `MustOverride` zamiast podawania wartości dla parametru atrybutu:</span><span class="sxs-lookup"><span data-stu-id="dcdbe-147">Use hello `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="dcdbe-148">toooverride wartości w pliku Settings.xml, Zadeklaruj parametr zastąpienia dla usługi hello w pliku ApplicationManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="dcdbe-148">toooverride values in Settings.xml, declare an override parameter for hello service in ApplicationManifest.xml:</span></span>

```xml
<ApplicationManifest ... >
  <Parameters>
    <Parameter Name="MySecret" DefaultValue="" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides>
      <ConfigOverride Name="Config">
        <Settings>
          <Section Name="MySettings">
            <Parameter Name="MySecret" Value="[MySecret]" IsEncrypted="true" />
          </Section>
        </Settings>
      </ConfigOverride>
    </ConfigOverrides>
  </ServiceManifestImport>
 ```

<span data-ttu-id="dcdbe-149">Teraz można określić wartość hello jako *parametru aplikacji* podczas tworzenia wystąpienia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-149">Now hello value can be specified as an *application parameter* when creating an instance of hello application.</span></span> <span data-ttu-id="dcdbe-150">Tworzenie wystąpienia aplikacji mogą być przetwarzane przez skrypty przy użyciu programu PowerShell, lub napisane w języku C# dla Łatwa integracja w procesie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="dcdbe-151">Przy użyciu programu PowerShell, parametr hello jest podany toohello `New-ServiceFabricApplication` polecenie jako [tablicy skrótów](https://technet.microsoft.com/library/ee692803.aspx):</span><span class="sxs-lookup"><span data-stu-id="dcdbe-151">Using PowerShell, hello parameter is supplied toohello `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="dcdbe-152">Przy użyciu języka C#, parametry aplikacji są określone w `ApplicationDescription` jako `NameValueCollection`:</span><span class="sxs-lookup"><span data-stu-id="dcdbe-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

```csharp
FabricClient fabricClient = new FabricClient();

NameValueCollection applicationParameters = new NameValueCollection();
applicationParameters["MySecret"] = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=";

ApplicationDescription applicationDescription = new ApplicationDescription(
    applicationName: new Uri("fabric:/MyApp"),
    applicationTypeName: "MyAppType",
    applicationTypeVersion: "1.0.0",
    applicationParameters: applicationParameters)
);

await fabricClient.ApplicationManager.CreateApplicationAsync(applicationDescription);
```

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="dcdbe-153">Odszyfrowywanie hasła z kodem usługi</span><span class="sxs-lookup"><span data-stu-id="dcdbe-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="dcdbe-154">Usługi w sieci szkieletowej usług w ramach usługi SIECIOWE są domyślnie uruchamiane w systemie Windows i nie są toocertificates dostępu zainstalowane w węźle hello bez dodatkowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access toocertificates installed on hello node without some extra setup.</span></span>

<span data-ttu-id="dcdbe-155">Korzystając z certyfikatu szyfrowanie danych, należy toomake się, że Usługa sieciowa lub uruchamiania niezależnie od usługi hello konto użytkownika ma klucz prywatny certyfikatu toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-155">When using a data encipherment certificate, you need toomake sure NETWORK SERVICE or whatever user account hello service is running under has access toohello certificate's private key.</span></span> <span data-ttu-id="dcdbe-156">Sieć szkieletowa usług będzie obsługiwać udzielania dostępu dla usługi automatycznie należy skonfigurować je toodo tak.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-156">Service Fabric will handle granting access for your service automatically if you configure it toodo so.</span></span> <span data-ttu-id="dcdbe-157">Ta konfiguracja może odbywać się w pliku ApplicationManifest.xml przez zdefiniowanie zasad zabezpieczeń dla certyfikatów i użytkowników.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="dcdbe-158">Podany przez hello poniższy przykład, hello konto Usługa sieciowa jest zdefiniowany przez jego odcisk palca certyfikatu tooa dostęp do odczytu:</span><span class="sxs-lookup"><span data-stu-id="dcdbe-158">In hello following example, hello NETWORK SERVICE account is given read access tooa certificate defined by its thumbprint:</span></span>

```xml
<ApplicationManifest … >
    <Principals>
        <Users>
            <User Name="Service1" AccountType="NetworkService" />
        </Users>
    </Principals>
  <Policies>
    <SecurityAccessPolicies>
      <SecurityAccessPolicy GrantRights=”Read” PrincipalRef="Service1" ResourceRef="MyCert" ResourceType="Certificate"/>
    </SecurityAccessPolicies>
  </Policies>
  <Certificates>
    <SecretsCertificate Name="MyCert" X509FindType="FindByThumbprint" X509FindValue="[YourCertThumbrint]"/>
  </Certificates>
</ApplicationManifest>
```

> [!NOTE]
> <span data-ttu-id="dcdbe-159">Podczas kopiowania odcisku palca certyfikatu z certyfikatu hello magazynu przystawki w systemie Windows, znaku niewidoczne znajduje się na początku hello hello odcisk palca ciągu.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-159">When copying a certificate thumbprint from hello certificate store snap-in on Windows, an invisible character is placed at hello beginning of hello thumbprint string.</span></span> <span data-ttu-id="dcdbe-160">Ten znak niewidoczne może spowodować błąd podczas próby toolocate certyfikatu przez odcisk palca, więc należy toodelete się, że ten dodatkowy znak.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-160">This invisible character can cause an error when trying toolocate a certificate by thumbprint, so be sure toodelete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="dcdbe-161">Użyj hasła aplikacji w kodzie usługi</span><span class="sxs-lookup"><span data-stu-id="dcdbe-161">Use application secrets in service code</span></span>
<span data-ttu-id="dcdbe-162">Witaj interfejsu API do uzyskiwania dostępu do wartości konfiguracji z pliku Settings.xml w pakiecie konfiguracji umożliwia łatwe odszyfrowywania wartości, które mają hello `IsEncrypted` zbyt ustawiony atrybut`true`.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-162">hello API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have hello `IsEncrypted` attribute set too`true`.</span></span> <span data-ttu-id="dcdbe-163">Ponieważ hello zaszyfrowany tekst zawiera informacje o hello certyfikat używany do szyfrowania, nie trzeba toomanually Znajdź hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-163">Since hello encrypted text contains information about hello certificate used for encryption, you do not need toomanually find hello certificate.</span></span> <span data-ttu-id="dcdbe-164">certyfikat Hello wystarczy toobe zainstalowany w węźle hello, że usługa hello jest uruchomiona na.</span><span class="sxs-lookup"><span data-stu-id="dcdbe-164">hello certificate just needs toobe installed on hello node that hello service is running on.</span></span> <span data-ttu-id="dcdbe-165">Po prostu Wywołaj hello `DecryptValue()` oryginalna wartość tajna metody tooretrieve hello:</span><span class="sxs-lookup"><span data-stu-id="dcdbe-165">Simply call hello `DecryptValue()` method tooretrieve hello original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="dcdbe-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dcdbe-166">Next Steps</span></span>
<span data-ttu-id="dcdbe-167">Dowiedz się więcej o [uruchamiania aplikacji za pomocą uprawnień zabezpieczeń](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="dcdbe-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
