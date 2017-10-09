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
# <a name="managing-secrets-in-service-fabric-applications"></a>Zarządzanie kluczy tajnych w aplikacji sieci szkieletowej usług
Ten przewodnik przeprowadzi Cię przez kroki hello zarządzania kluczy tajnych w aplikacji sieci szkieletowej usług. Klucze tajne można poufne informacje, takie jak parametry połączenia magazynu, hasła lub inne wartości, które nie powinny być traktowane w postaci zwykłego tekstu.

W tym przewodniku używa usługi Azure Key Vault toomanage kluczy i kluczy tajnych. Jednak *przy użyciu* kluczy tajnych w aplikacji jest chmury tooallow niezależny od platformy aplikacji toobe tooa wdrożonej klastra hostowanej dowolnego miejsca. 

## <a name="overview"></a>Omówienie
Witaj ustawienia konfiguracji usługi toomanage zalecaną metodą jest użycie [usługi pakiety konfiguracji][config-package]. Pakiety konfiguracji są kontrolą wersji i nadaje się do aktualizacji za pomocą zarządzanego stopniowe z sprawdzania kondycji i automatycznego wycofywania. Jest to preferowany tooglobal konfiguracji zmniejsza ryzyko hello awarię usług globalnych. Zaszyfrowanych kluczy tajnych są żaden wyjątek. Sieć szkieletowa usług ma wbudowane funkcje szyfrowania i odszyfrowywania wartości w pliku Settings.xml pakietu konfiguracji przy użyciu certyfikatu szyfrowania.

Witaj poniższym diagramie przedstawiono podstawowy przepływ hello tajny zarządzania w sieci szkieletowej usług aplikacji:

![Zarządzanie tajne — omówienie][overview]

W tym przepływie istnieją cztery główne kroki:

1. Uzyskaj certyfikat Szyfrowanie danych.
2. Zainstaluj certyfikat hello w klastrze.
3. Szyfrowanie tajny wartości podczas wdrażania aplikacji przy użyciu certyfikatu hello i wstawić je do pliku konfiguracji Settings.xml usługi.
4. Odczyt zaszyfrowanych wartości poza Settings.xml w tym celu odszyfrowuje z hello tego samego certyfikatu szyfrowanie. 

[Usługa Azure Key Vault] [ key-vault-get-started] jest tu używany jako lokalizację bezpiecznego magazynu certyfikatów, a tooget sposób certyfikatów zainstalowanych na klastrów sieci szkieletowej usług platformy Azure. Jeśli nie są wdrażane tooAzure, nie trzeba toouse kluczy tajnych toomanage Key Vault w aplikacji sieci szkieletowej usług.

## <a name="data-encipherment-certificate"></a>Certyfikat Szyfrowanie danych
Certyfikat Szyfrowanie danych jest używane wyłącznie do szyfrowania i odszyfrowywania konfiguracji wartości w pliku Settings.xml usługi i nie jest używany do uwierzytelniania lub podpisywanie tekst zaszyfrowany. certyfikat Hello musi spełniać hello następujące wymagania:

* Witaj, certyfikat musi zawierać klucz prywatny.
* Witaj certyfikatu musi zostać utworzony dla wymiany kluczy, można eksportować tooa plik wymiany informacji osobistych (pfx).
* sposób użycia klucza certyfikatu Hello musi zawierać szyfrowanie danych (10) i nie powinna zawierać uwierzytelniania serwera lub uwierzytelniania klienta. 
  
  Na przykład podczas tworzenia certyfikatu z podpisem własnym za pomocą programu PowerShell, hello `KeyUsage` musi również ustawiona flaga`DataEncipherment`:
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a>Zainstaluj certyfikat hello w klastrze
Ten certyfikat należy zainstalować na każdym węźle klastra hello. Będzie on używany w wartości toodecrypt środowiska uruchomieniowego przechowywanych w pliku Settings.xml usługi. Zobacz [jak toocreate klastra przy użyciu usługi Azure Resource Manager] [ service-fabric-cluster-creation-via-arm] instrukcje instalacji. 

## <a name="encrypt-application-secrets"></a>Szyfrowanie hasła aplikacji
Hello zestawu SDK sieci szkieletowej usług ma wbudowane funkcje tajny szyfrowania i odszyfrowywania. Tajny wartości może być szyfrowane w czasie zbudowany odszyfrować i programowo odczytać w kodzie usługi. 

Witaj następującego polecenia programu PowerShell jest używane tooencrypt klucz tajny. To polecenie szyfruje wartości hello; robi **nie** zarejestrować hello tekst zaszyfrowany. Należy użyć hello tego samego certyfikatu szyfrowanie zainstalowanej w Twojej tekstu szyfrowanego tooproduce klastra tajny wartości:

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

Witaj wynikowy ciąg base-64 zawiera zarówno tajny tekstu szyfrowanego hello, jak również informacje o certyfikacie hello, który był używany tooencrypt go.  Witaj zakodowanym ciągiem base-64 można wstawiać do parametru w pliku konfiguracji usługi Settings.xml hello `IsEncrypted` zbyt ustawiony atrybut`true`:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a>Wstaw klucze tajne aplikacji do wystąpienia aplikacji
W idealnym przypadku środowisk toodifferent wdrażania należy jak zautomatyzowane, jak to możliwe. Można to zrobić wykonywania tajny szyfrowania w środowisku kompilacji i podając hello zaszyfrowanych kluczy tajnych jako parametry podczas tworzenia wystąpień aplikacji.

#### <a name="use-overridable-parameters-in-settingsxml"></a>Korzystanie z możliwym do zastąpienia parametrów w pliku Settings.xml
plik konfiguracji w pliku Settings.xml Hello umożliwia możliwością zastępowania parametrów, które można podać podczas tworzenia aplikacji. Użyj hello `MustOverride` zamiast podawania wartości dla parametru atrybutu:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

toooverride wartości w pliku Settings.xml, Zadeklaruj parametr zastąpienia dla usługi hello w pliku ApplicationManifest.xml:

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

Teraz można określić wartość hello jako *parametru aplikacji* podczas tworzenia wystąpienia aplikacji hello. Tworzenie wystąpienia aplikacji mogą być przetwarzane przez skrypty przy użyciu programu PowerShell, lub napisane w języku C# dla Łatwa integracja w procesie kompilacji.

Przy użyciu programu PowerShell, parametr hello jest podany toohello `New-ServiceFabricApplication` polecenie jako [tablicy skrótów](https://technet.microsoft.com/library/ee692803.aspx):

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

Przy użyciu języka C#, parametry aplikacji są określone w `ApplicationDescription` jako `NameValueCollection`:

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

## <a name="decrypt-secrets-from-service-code"></a>Odszyfrowywanie hasła z kodem usługi
Usługi w sieci szkieletowej usług w ramach usługi SIECIOWE są domyślnie uruchamiane w systemie Windows i nie są toocertificates dostępu zainstalowane w węźle hello bez dodatkowej konfiguracji.

Korzystając z certyfikatu szyfrowanie danych, należy toomake się, że Usługa sieciowa lub uruchamiania niezależnie od usługi hello konto użytkownika ma klucz prywatny certyfikatu toohello dostępu. Sieć szkieletowa usług będzie obsługiwać udzielania dostępu dla usługi automatycznie należy skonfigurować je toodo tak. Ta konfiguracja może odbywać się w pliku ApplicationManifest.xml przez zdefiniowanie zasad zabezpieczeń dla certyfikatów i użytkowników. Podany przez hello poniższy przykład, hello konto Usługa sieciowa jest zdefiniowany przez jego odcisk palca certyfikatu tooa dostęp do odczytu:

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
> Podczas kopiowania odcisku palca certyfikatu z certyfikatu hello magazynu przystawki w systemie Windows, znaku niewidoczne znajduje się na początku hello hello odcisk palca ciągu. Ten znak niewidoczne może spowodować błąd podczas próby toolocate certyfikatu przez odcisk palca, więc należy toodelete się, że ten dodatkowy znak.
> 
> 

### <a name="use-application-secrets-in-service-code"></a>Użyj hasła aplikacji w kodzie usługi
Witaj interfejsu API do uzyskiwania dostępu do wartości konfiguracji z pliku Settings.xml w pakiecie konfiguracji umożliwia łatwe odszyfrowywania wartości, które mają hello `IsEncrypted` zbyt ustawiony atrybut`true`. Ponieważ hello zaszyfrowany tekst zawiera informacje o hello certyfikat używany do szyfrowania, nie trzeba toomanually Znajdź hello certyfikatu. certyfikat Hello wystarczy toobe zainstalowany w węźle hello, że usługa hello jest uruchomiona na. Po prostu Wywołaj hello `DecryptValue()` oryginalna wartość tajna metody tooretrieve hello:

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [uruchamiania aplikacji za pomocą uprawnień zabezpieczeń](service-fabric-application-runas-security.md)

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
