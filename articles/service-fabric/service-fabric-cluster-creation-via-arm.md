---
title: "Sieć szkieletowa usług Azure aaaCreate klastra z szablonu | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooset się bezpiecznej sieci szkieletowej usług klastra na platformie Azure przy użyciu usługi Azure Resource Manager, magazyn kluczy Azure i usługi Azure Active Directory (Azure AD) do uwierzytelniania klientów."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a>Tworzenie klastra sieci szkieletowej usług za pomocą usługi Azure Resource Manager
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Witryna Azure Portal](service-fabric-cluster-creation-via-portal.md)
>
>

Ten przewodnik krok po kroku przeprowadzi Cię przez proces konfigurowania bezpiecznej klastra usługi sieć szkieletowa usług Azure na platformie Azure przy użyciu usługi Azure Resource Manager. Potwierdzam, że artykułu hello jest długa. Jeśli nie znasz już dokładnie hello zawartości, są toofollow się, że każdy krok uważnie.

Podręcznik Hello obejmuje hello następujące procedury:

* Konfigurowanie usługi Azure key vault tooupload certyfikaty zabezpieczeń klastra i aplikacji
* Tworzenie klastra zabezpieczonych na platformie Azure przy użyciu usługi Azure Resource Manager
* Uwierzytelnianie użytkowników przy użyciu usługi Azure Active Directory (Azure AD) do zarządzania klastrem

Bezpieczne klastra jest klastra, który uniemożliwia nieautoryzowanym dostępem toomanagement operacji. W tym wdrażanie, uaktualnianie i usuwania aplikacji, usług i hello nich danych. Niezabezpieczone klaster jest klastrem informujący o tym, czy każdy połączyć tooat w dowolnym momencie i wykonywać operacje zarządzania. Chociaż możliwe toocreate klastra niezabezpieczone, zdecydowanie zaleca się tworzenie bezpiecznej klastra z początku hello. Ponieważ niezabezpieczone klastra nie można zabezpieczyć później, należy utworzyć nowy klaster.

pojęcie Hello tworzenia bezpiecznych klastrów hello jest takie same, czy są one klastrów systemu Linux lub Windows. Aby uzyskać więcej informacji i pomocnika skryptów tworzenia bezpiecznych klastrów systemu Linux, zobacz [tworzenia bezpiecznych klastrów w systemie Linux](#secure-linux-clusters).

## <a name="sign-in-tooyour-azure-account"></a>Zaloguj się tooyour konto platformy Azure
Ten przewodnik po używa [programu Azure PowerShell][azure-powershell]. Po ponownym uruchomieniu nowej sesji programu PowerShell, zaloguj się tooyour konto platformy Azure i wybierz subskrypcję, przed wykonaniem polecenia platformy Azure.

Zaloguj się tooyour konto platformy Azure:

```powershell
Login-AzureRmAccount
```

Wybierz subskrypcję:

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a>Konfigurowanie magazynu kluczy
W tej sekcji omówiono tworzenie magazynu kluczy dla klastra sieci szkieletowej usług platformy Azure i dla aplikacji sieci szkieletowej usług. TooAzure kompletny przewodnik po klucz magazynu, można znaleźć w temacie toohello [Key Vault Wprowadzenie — przewodnik][key-vault-get-started].

Sieć szkieletowa usług używa toosecure certyfikatów X.509 klastra i zapewnia funkcje zabezpieczeń aplikacji. Używane certyfikaty toomanage Key Vault dla klastrów sieci szkieletowej usług platformy Azure. Po wdrożeniu klastra w systemie Azure hello dostawcy zasobów platformy Azure, który jest odpowiedzialny za tworzenie klastrów usługi sieć szkieletowa ściąga certyfikaty z magazynu kluczy i instaluje je w klastrze hello maszyn wirtualnych.

Witaj poniższym diagramie przedstawiono relację hello Azure Key Vault, klaster sieci szkieletowej usług i hello dostawcy zasobów platformy Azure, który wykorzystuje certyfikaty przechowywane w magazynie kluczy, podczas tworzenia klastra:

![Diagram instalacji certyfikatu][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów
pierwszym krokiem Hello jest toocreate grupę zasobów, w szczególności dla magazynu kluczy. Firma Microsoft zaleca umieścić hello magazynu kluczy w jego własnej grupy zasobów. Ta akcja umożliwia usunięcie hello obliczeniowej i pamięci masowej grup zasobów, tym hello grupy zasobów, zawierającą klaster sieci szkieletowej usług bez utraty z kluczy i kluczy tajnych. Hello grupę zasobów, która zawiera magazynu kluczy _musi być w hello tego samego regionu_ jako hello klastra, który jest używany.

Jeśli planujesz toodeploy klastry w wielu regionach, zalecamy nadanie nazwy grupy zasobów hello i hello magazynu kluczy w sposób, który wskazuje regionu, do którego należy.  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
dane wyjściowe Hello powinien wyglądać następująco:

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a>Tworzenie magazynu kluczy w hello nową grupę zasobów
magazyn kluczy Hello _musi być włączona dla wdrożenia_ tooallow hello certyfikaty tooget dostawcy zasobów obliczeniowych od niego i zainstalować ją na wystąpieniu maszyny wirtualnej:

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

dane wyjściowe Hello powinien wyglądać następująco:

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a>Użyj istniejącego magazynu kluczy

toouse istniejący magazyn kluczy, możesz _należy włączyć dla wdrożenia_ tooallow hello certyfikaty tooget dostawcy zasobów obliczeniowych od niego i zainstaluj go na węzłach klastra:

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a>Dodaj magazyn kluczy tooyour certyfikatów

Certyfikaty są używane w sieci szkieletowej usług tooprovide uwierzytelnianie i szyfrowanie toosecure różnych aspektów klastra i jego zastosowań. Aby uzyskać więcej informacji dotyczących używania certyfikatów w sieci szkieletowej usług, zobacz [scenariusze zabezpieczeń klastra sieci szkieletowej usług][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Klaster a serwera certyfikatów (wymagane)
Ten certyfikat jest wymagany toosecure klastra i zapobiec tooit nieautoryzowanego dostępu. Udostępnia ona zabezpieczeń klastra na dwa sposoby:

* Uwierzytelnianie klastra: uwierzytelnia komunikacji między węzłami w Federacji klastra. Tylko węzły, które można potwierdzić swoją tożsamość, z tym certyfikatem może dołączać hello klastra.
* Uwierzytelnianie serwera: uwierzytelnia hello klastra zarządzania punkty końcowe tooa zarządzania klienta, tak, aby hello klienta zarządzania zna jest mówić toohello rzeczywistych klastra. Ten certyfikat zapewnia również SSL hello interfejsu API zarządzania HTTPS oraz Service Fabric Explorer, za pośrednictwem protokołu HTTPS.

tooserve tych celów hello certyfikatu musi spełniać następujące wymagania hello:

* Witaj, certyfikat musi zawierać klucz prywatny.
* Witaj certyfikatu musi zostać utworzony dla wymiany kluczy, który jest możliwy do wyeksportowania tooa plik wymiany informacji osobistych (pfx).
* Nazwa podmiotu certyfikatu Hello musi odpowiadać domeny hello używanie klastra usługi sieć szkieletowa hello tooaccess. To dopasowanie jest wymagana tooprovide SSL dla punktów końcowych zarządzania HTTPS hello klastra i Service Fabric Explorer. Nie można uzyskać certyfikatu SSL z urzędu certyfikacji (CA) w celu hello. cloudapp.azure.com domeny. Należy uzyskać niestandardowej nazwy domeny dla klastra. Podczas żądania certyfikatu z urzędu certyfikacji, hello nazwa podmiotu certyfikatu musi odpowiadać hello niestandardowej nazwy domeny używanej dla klastra.

### <a name="application-certificates-optional"></a>Certyfikaty aplikacji (opcjonalnie)
Dowolna liczba dodatkowych certyfikatów można zainstalować w klastrze dla aplikacji ze względów bezpieczeństwa. Przed utworzeniem klastra, należy wziąć pod uwagę scenariusze zabezpieczeń aplikacji hello, które wymagają toobe certyfikat zainstalowany na węzłach hello, takich jak:

* Szyfrowanie i odszyfrowywanie wartości konfiguracji aplikacji.
* Szyfrowanie danych w węzłach podczas replikacji.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Formatowanie certyfikatów do użytku dostawcy zasobów platformy Azure
Można dodać i używać plików kluczy prywatnych (pfx) bezpośrednio za pomocą magazynu kluczy. Dostawcy zasobów obliczeniowych Azure hello wymaga jednak toobe klucze przechowywane w formacie JavaScript Object Notation (JSON) specjalnych. Hello format zawiera plik PFX hello jako ciąg zakodowany w formacie 64 bazy i hello hasło klucza prywatnego. tooaccommodate tych wymagań, hello kluczy musi być umieszczona w ciągu JSON i następnie przechowywane jako "hasła" hello klucza magazynu.

toomake to przetworzyć łatwiej, [moduł programu PowerShell jest dostępny w witrynie GitHub][service-fabric-rp-helpers]. Moduł hello toouse, hello następujące:

1. Pobierz całą zawartość repozytorium hello hello do katalogu lokalnego.
2. Przejdź toohello katalogu lokalnego.
2. Zaimportuj moduł ServiceFabricRPHelpers hello w oknie programu PowerShell:

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

Witaj `Invoke-AddCertToKeyVault` polecenia w tym module środowiska PowerShell automatycznie formatuje klucz prywatny certyfikatu do ciągu JSON i przekazanie jej toohello magazynu kluczy. Użyj hello polecenia tooadd hello klastra certyfikat i wszelkie dodatkowe aplikacji certyfikaty toohello magazynu kluczy. Powtórz ten krok dla wszystkich dodatkowych certyfikatów, które chcesz tooinstall w klastrze.

#### <a name="uploading-an-existing-certificate"></a>Przekazywanie istniejącego certyfikatu

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

Jeśli wystąpi błąd, takich jak hello przedstawionego poniżej, zwykle oznacza to, że występuje konflikt adresu URL zasobu. tooresolve hello konflikt, Zmień nazwę magazynu kluczy hello.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Po hello konflikt został rozwiązany, dane wyjściowe hello powinien wyglądać następująco:

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
>Należy hello trzech poprzednich ciągów, CertificateThumbprint, SourceVault i CertificateURL, tooset bezpiecznego klastra sieci szkieletowej usług i tooobtain wszelkich certyfikatów aplikacji, które mogą używać zabezpieczeń aplikacji. Jeśli zapiszesz hello ciągów, może być tooretrieve trudno ich badając klucza hello później magazynu.

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a>Tworzenie certyfikatu z podpisem własnym i przekazać go toohello magazyn kluczy

Jeśli zostały już przekazane magazynu kluczy toohello certyfikaty, Pomiń ten krok. Ten krok jest generowania nowego certyfikatu z podpisem własnym i przekazać go tooyour magazynu kluczy. Po Zmień parametry hello w hello następującego skryptu, a następnie uruchom go, należy się monit o hasło certyfikatu.  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

Jeśli wystąpi błąd, takich jak hello przedstawionego poniżej, zwykle oznacza to, że występuje konflikt adresu URL zasobu. konflikt hello tooresolve, Zmień nazwę magazynu kluczy hello, nazwa grupy zasobów i tak dalej.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Po hello konflikt został rozwiązany, dane wyjściowe hello powinien wyglądać następująco:

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
>Należy hello trzech poprzednich ciągów, CertificateThumbprint, SourceVault i CertificateURL, tooset bezpiecznego klastra sieci szkieletowej usług i tooobtain wszelkich certyfikatów aplikacji, które mogą używać zabezpieczeń aplikacji. Jeśli zapiszesz hello ciągów, może być tooretrieve trudno ich badając klucza hello później magazynu.

 W tym momencie powinny mieć następujące elementy w miejscu hello:

* Witaj grupy zasobów magazynu kluczy.
* Witaj magazyn kluczy i adresu URL (o nazwie SourceVault hello poprzedzający dane wyjściowe programu PowerShell).
* certyfikat uwierzytelniania serwera klastra Hello i jego adres URL w magazynie kluczy hello.
* Certyfikaty aplikacji Hello i ich adresy URL w magazynie kluczy hello.


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a>Konfigurowanie usługi Azure Active Directory do uwierzytelniania klientów

Usługi Azure AD umożliwia tooapplications dostępu użytkownika toomanage organizacji (nazywane dzierżawców). Aplikacje są podzielone na tych z opartą na sieci web interfejsu użytkownika logowania i te przy użyciu środowiska macierzystego klienta. W tym artykule przyjęto założenie, że utworzono już dzierżawcy. Jeśli nie masz, Rozpocznij od przeczytania [jak dzierżawy usługi Azure Active Directory tooget][active-directory-howto-tenant].

Klaster sieci szkieletowej usług oferuje kilka tooits punkty wejścia funkcje zarządzania, w tym hello opartych na sieci web [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] i [programu Visual Studio] [service-fabric-manage-application-in-visual-studio]. W związku z tym możesz utworzyć dwie usługi Azure AD aplikacji toocontrol dostępu toohello klastra, jednej aplikacji sieci web i jednej aplikacji natywnej.

Niektóre kroki hello zaangażowane w konfigurowaniu usługi Azure AD z klastrem usługi sieć szkieletowa toosimplify, został utworzony zestaw skryptów programu Windows PowerShell.

> [!NOTE]
> Należy wykonać następujące kroki, przed utworzeniem klastra hello hello. Ponieważ skrypty hello oczekuje nazwy klastra i punkty końcowe, hello wartości powinny być planowane i nie wartości, które zostało już utworzone.

1. [Pobierz skrypty hello] [ sf-aad-ps-script-download] tooyour komputera.
2. Kliknij prawym przyciskiem myszy hello pliku zip, wybierz opcję **właściwości**, wybierz pozycję hello **Odblokuj** pole wyboru, a następnie kliknij przycisk **Zastosuj**.
3. Wyodrębnij plik zip hello.
4. Uruchom `SetupApplications.ps1`i podaj hello TenantId, ClusterName i WebApplicationReplyUrl jako parametry. Na przykład:

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    Można znaleźć identyfikatora sieci dzierżawcy, wykonując polecenie programu PowerShell hello `Get-AzureSubscription`. Wykonywanie to polecenie wyświetla hello TenantId dla każdej subskrypcji.

    ClusterName jest tooprefix używanych aplikacji hello Azure AD, które są tworzone przez skrypt hello. Nie musi dokładnie toomatch hello rzeczywista nazwa klastra. Jest przeznaczone tylko toomake go łatwiejsze toomap usługi Azure AD artefakty toohello sieci szkieletowej usług klastra, który jest używany z.

    WebApplicationReplyUrl jest domyślny punkt końcowy hello, zwracające usługi Azure AD użytkownicy tooyour po kończyły się zalogować. Ustaw ten punkt końcowy jako punkt końcowy Service Fabric Explorer powitania dla klastra, która domyślnie jest:

    https://&lt;cluster_domain&gt;: 19080/Explorer

    Jesteś zostanie wyświetlony monit o toosign tooan konta, które ma uprawnienia administracyjne dla dzierżawy usługi Azure AD hello. Po zalogowaniu w hello skrypt tworzy hello sieci web i toorepresent natywnych aplikacji klastra sieci szkieletowej usług. Jeśli przyjrzymy się aplikacji hello dzierżawy w hello [klasycznego portalu Azure][azure-classic-portal], powinny pojawić się dwa nowe wpisy:

   * *ClusterName*\_klastra
   * *ClusterName*\_klienta

   skrypt Hello drukuje hello Otwórz wymagane przez szablon usługi Azure Resource Manager hello podczas tworzenia klastra hello w następnej sekcji hello, dzięki czemu okno programu PowerShell dobrze tookeep hello JSON.

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a>Utwórz szablon Menedżera zasobów klastra sieci szkieletowej usług
W tej sekcji hello produktów wyjściowych hello powyższych poleceń programu PowerShell są używane w szablonie usługi Resource Manager klastra sieci szkieletowej usług.

Szablony Menedżera zasobów próbki są dostępne w hello [galerii szablonów szybki start Azure w serwisie GitHub][azure-quickstart-templates]. Te szablony może służyć jako punkt początkowy dla szablonu klastra.

### <a name="create-hello-resource-manager-template"></a>Tworzenie szablonu usługi Resource Manager hello
W tym przewodniku używa hello [5 węzłów klastra bezpiecznego] [ service-fabric-secure-cluster-5-node-1-nodetype] przykładowy szablon i parametrów szablonu. Pobierz `azuredeploy.json` i `azuredeploy.parameters.json` tooyour komputera, a następnie otwórz oba pliki w edytorze tekstu.

### <a name="add-certificates"></a>Dodaj certyfikaty
Możesz dodać szablonu usługi Resource Manager klastra tooa certyfikatów za pomocą odwołań do magazynu kluczy hello, która zawiera klucze certyfikatów hello. Zaleca się umieszczenie hello usługi key vault wartości w pliku parametrów szablonu usługi Resource Manager. W ten sposób pozwala hello Menedżera zasobów pliku szablonu wielokrotnego użytku i wolnego wdrożenia tooa określonej wartości.

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a>Dodaj wszystkie certyfikaty toohello maszyny wirtualnej zestawu skalowania maszyny wirtualnej osProfile
Każdy certyfikat, który jest zainstalowany w klastrze hello muszą być skonfigurowane w sekcji osProfile hello zasób zestawu skali hello (Microsoft.Compute/virtualMachineScaleSets). Ta akcja powoduje, że certyfikat dostawcy zasobów hello hello tooinstall na powitania maszyn wirtualnych. Ta instalacja obejmuje zarówno hello klastra certyfikat, jak i wszelkich certyfikatów zabezpieczeń aplikacji planowanie toouse aplikacji:

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a>Konfigurowanie certyfikatu klastra usługi sieć szkieletowa hello
certyfikat uwierzytelniania Hello klastra muszą być skonfigurowane w obu zasobu klastra usługi sieć szkieletowa hello (Microsoft.ServiceFabric/clusters) i hello rozszerzenia sieci szkieletowej usług na potrzeby skalowania maszyny wirtualnej zestawy w zasób zestawu skali maszyny wirtualnej hello. To rozmieszczenie umożliwia tooconfigure dostawcy zasobów usługi Service Fabric hello go dla uwierzytelniania klastra i uwierzytelniania serwera dla punktów końcowych zarządzania.

##### <a name="virtual-machine-scale-set-resource"></a>Zasób zestawu skalowania maszyn wirtualnych:
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a>Zasobów sieci szkieletowej usług:
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a>Wstaw konfiguracji usługi Azure AD
mogą być wstawiane konfiguracji Hello Azure AD, który został utworzony wcześniej bezpośrednio do szablonu usługi Resource Manager. Jednak zaleca się najpierw Wyodrębnij wartości hello do parametrów pliku tookeep hello Menedżera zasobów szablonu do ponownego użycia i zwolnij wdrożenia tooa określonej wartości.

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### < "Konfigurowanie ramię" ></a>parametry szablonu Konfigurowanie Menedżera zasobów
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
Na koniec użyj hello wartości danych wyjściowych z magazynu kluczy hello i pliku parametrów hello toopopulate poleceń programu PowerShell usługi Azure AD:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
W tym momencie powinny mieć następujące elementy w miejscu hello:

* Grupa zasobów magazynu kluczy
  * Magazyn kluczy
  * Certyfikat uwierzytelniania serwera klastra
  * Certyfikat Szyfrowanie danych
* Dzierżawy usługi Azure Active Directory
  * Aplikacji usługi Azure AD dla zarządzania opartego na sieci web i Service Fabric Explorer
  * Aplikacji do zarządzania klientami z usługi Azure AD
  * Użytkownicy i przypisane im role
* Szablon usługi Resource Manager klastra sieci szkieletowej usług
  * Skonfigurowanych za pomocą magazynu kluczy certyfikatów
  * Usługa Azure Active Directory skonfigurowane

powitania po diagram ilustruje, gdy magazyn kluczy i konfiguracji usługi Azure AD mieści się w szablonie usługi Resource Manager.

![Menedżer zasobów zależności mapy][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a>Tworzenie klastra hello
Wszystko jest teraz gotowy toocreate hello klastra przy użyciu [wdrażania szablonu zasobów platformy Azure][resource-group-template-deploy].

#### <a name="test-it"></a>należy przeprowadzić test
Należy użyć szablonu usługi Resource Manager powitania po tootest polecenia programu PowerShell z pliku parametrów:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a>Wdróż go
Przeszedł test szablonu usługi Resource Manager hello, należy użyć powitania po toodeploy polecenia programu PowerShell do szablonu usługi Resource Manager z pliku parametrów:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a>Przypisywanie użytkowników tooroles
Po utworzeniu toorepresent aplikacji hello klastra, przypisywanie użytkownikom ról toohello obsługiwane przez usługi Service Fabric: tylko do odczytu i administratora. Można przypisać role hello za pomocą hello [klasycznego portalu Azure][azure-classic-portal].

1. W hello portalu Azure, przejdź do pozycji tooyour dzierżawy, a następnie wybierz **aplikacji**.
2. Wybierz aplikację sieci web hello mający nazwę jak `myTestCluster_Cluster`.
3. Kliknij przycisk hello **użytkowników** kartę.
4. Wybierz tooassign użytkownika, a następnie kliknij przycisk hello **przypisać** przycisk u dołu hello hello ekranu.

    ![Przypisywanie użytkowników tooroles przycisku][assign-users-to-roles-button]
5. Wybierz hello roli tooassign toohello użytkownika.

    ![Okno dialogowe "Przypisywanie użytkowników"][assign-users-to-roles-dialog]

> [!NOTE]
> Aby uzyskać więcej informacji na temat ról w sieci szkieletowej usług, zobacz [kontroli dostępu opartej na rolach dla klientów usługi sieć szkieletowa](service-fabric-cluster-security-roles.md).
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a>Tworzenie bezpiecznych klastrów w systemie Linux
proces hello toomake jest łatwiejsze, firma Microsoft umieściła [skryptu Pomocnika](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux). Przed użyciem tego skryptu pomocnika, upewnij się, że masz już Azure interfejsu wiersza polecenia (CLI) zainstalowany i znajduje się w ścieżce. Upewnij się, że skrypt hello ma tooexecute uprawnienia, uruchamiając `chmod +x cert_helper.py` po ją pobrać. pierwszym krokiem Hello jest toosign w tooyour konto platformy Azure przy użyciu interfejsu wiersza polecenia z hello `azure login` polecenia. Po zalogowaniu się tooyour konto platformy Azure, użyj hello pomocnika skryptu z urzędu certyfikacji certyfikatu z podpisem, jako powitania po pokazuje polecenia:

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

Parametr - ifile Hello może zająć plik pfx lub plik PEM jako dane wejściowe z hello typ certyfikatu (pfx lub pem lub ss, jeśli certyfikat z podpisem własnym).
Witaj parametr -h drukowania hello tekst pomocy.


To polecenie zwraca następujące trzy ciągi jako dane wyjściowe hello hello:

* SourceVaultID, który jest identyfikator hello hello nowe KeyVault ResourceGroup on utworzony
* CertificateUrl do uzyskiwania dostępu do certyfikatu hello
* CertificateThumbprint, który jest używany do uwierzytelniania

Witaj poniższy przykład pokazuje, jak toouse hello polecenia:

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
Wykonywanie hello poprzedzających daje polecenie hello trzy ciągi w następujący sposób:

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

Nazwa podmiotu certyfikatu Hello musi odpowiadać domeny hello używanie klastra usługi sieć szkieletowa hello tooaccess. To dopasowanie jest wymagana tooprovide SSL dla punktów końcowych zarządzania HTTPS hello klastra i Service Fabric Explorer. Nie można uzyskać certyfikatu SSL z urzędu certyfikacji dla hello `.cloudapp.azure.com` domeny. Należy uzyskać niestandardowej nazwy domeny dla klastra. Podczas żądania certyfikatu z urzędu certyfikacji, hello nazwa podmiotu certyfikatu musi odpowiadać hello niestandardowej nazwy domeny używanej dla klastra.

Te nazwy podmiotu są hello wpisy toocreate bezpiecznego klastra sieci szkieletowej usług (bez usługi Azure AD), zgodnie z opisem w [parametrów szablonu usługi Resource Manager skonfigurować](#configure-arm). Możesz połączyć toohello bezpiecznego klastra, wykonując instrukcje hello [uwierzytelniania klientów dostępu tooa klastra](service-fabric-connect-to-secure-cluster.md). Klastry z systemem Linux w wersji zapoznawczej nie obsługują uwierzytelniania usługi Azure AD. Można przypisać role administratora, jak i klienta, zgodnie z opisem w hello [przypisać role toousers](#assign-roles) sekcji. Po określeniu ról administratora, jak i klienta dla systemu Linux klastra w wersji zapoznawczej, masz tooprovide odciski palców certyfikatów do uwierzytelniania. (Nie zostanie określona nazwa podmiotu hello, ponieważ nie weryfikacji łańcucha lub odwołania jest wykonywane w tej wersji zapoznawczej.)

Jeśli chcesz toouse certyfikatu z podpisem własnym do testowania, możesz użyć hello tego samego toogenerate skryptu jeden. Można następnie przekaż magazynu kluczy tooyour certyfikatu hello zapewniając flagi hello `ss` zamiast podanie certyfikatu hello nazwy ścieżki i certyfikatów. Na przykład zobacz hello następujące polecenia umożliwiające tworzenie i przekazywanie certyfikatu z podpisem własnym:

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
To polecenie zwraca hello tego samego trzy ciągi: SourceVault, CertificateUrl i CertificateThumbprint. Następnie można toocreate ciągów hello bezpiecznego klastra systemu Linux i z lokalizacji, gdzie jest umieszczony certyfikat z podpisem własnym hello. Należy hello certyfikatu z podpisem własnym tooconnect toohello klastra. Możesz połączyć toohello bezpiecznego klastra, wykonując instrukcje hello [uwierzytelniania klientów dostępu tooa klastra](service-fabric-connect-to-secure-cluster.md).

Nazwa podmiotu certyfikatu Hello musi odpowiadać domeny hello używanie klastra usługi sieć szkieletowa hello tooaccess. To dopasowanie jest wymagana tooprovide SSL dla punktów końcowych zarządzania HTTPS hello klastra i Service Fabric Explorer. Nie można uzyskać certyfikatu SSL z urzędu certyfikacji dla hello `.cloudapp.azure.com` domeny. Należy uzyskać niestandardowej nazwy domeny dla klastra. Podczas żądania certyfikatu z urzędu certyfikacji, hello nazwa podmiotu certyfikatu musi odpowiadać hello niestandardowej nazwy domeny używanej dla klastra.

Możesz wpisać parametry hello ze skryptu pomocnika hello w hello portalu Azure, zgodnie z opisem w hello [tworzenia klastra w portalu Azure hello](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) sekcji.

## <a name="next-steps"></a>Następne kroki
W tym momencie masz bezpiecznego klaster o udostępnienie uwierzytelniania zarządzania usługą Azure Active Directory. Następnie [połączenia klastra tooyour](service-fabric-connect-to-secure-cluster.md) i Dowiedz się, jak za[Zarządzanie klucze tajne aplikacji](service-fabric-application-secret-management.md).

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a>Rozwiązywanie problemów z Konfigurowanie usługi Azure Active Directory do uwierzytelniania klientów
Jeśli napotkasz problem podczas podczas konfigurowania usługi Azure AD do uwierzytelniania klientów, przejrzyj hello potencjalne rozwiązania w tej sekcji.

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a>Service Fabric Explorer monituje tooselect certyfikatu
#### <a name="problem"></a>Problem
Po zalogowaniu pomyślnie tooAzure AD w narzędziu Service Fabric Explorer przeglądarki hello zwraca toohello strony głównej, ale komunikat monituje tooselect certyfikatu.

![Wybierz certyfikat SFX w oknie dialogowym][sfx-select-certificate-dialog]

#### <a name="reason"></a>Przyczyna
Hello użytkownika nie jest przypisana rola hello aplikacji klastra usługi Azure AD. W związku z tym niepowodzenia uwierzytelniania usługi Azure AD w klastrze usługi sieć szkieletowa usług. Service Fabric Explorer powraca toocertificate uwierzytelniania.

#### <a name="solution"></a>Rozwiązanie
Wykonaj hello instrukcje dotyczące konfigurowania usługi Azure AD i przypisz role użytkownika. Ponadto zalecamy włączenie "Użytkownika przypisania tooaccess wymagana aplikacja" jako `SetupApplications.ps1` jest.

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a>Połączenie przy użyciu programu PowerShell zakończy się niepowodzeniem z powodu błędu: "hello określone poświadczenia są nieprawidłowe"
#### <a name="problem"></a>Problem
Gdy używasz programu PowerShell tooconnect toohello klastra przy użyciu trybu zabezpieczeń "Usługi AzureActiveDirectory", po zalogowaniu się pomyślnie tooAzure AD hello połączenia zakończy się niepowodzeniem z powodu błędu: "hello określone poświadczenia są nieprawidłowe."

#### <a name="solution"></a>Rozwiązanie
To rozwiązanie jest powitalne identyczny hello poprzedzających jeden.

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a>Service Fabric Explorer zwróci błąd podczas logowania: "AADSTS50011"
#### <a name="problem"></a>Problem
Podczas próby toosign w tooAzure AD w narzędziu Service Fabric Explorer strony hello zwraca błąd: "AADSTS50011: hello adres zwrotny &lt;adres url&gt; jest niezgodny z adresów odpowiedzi hello skonfigurowanych dla aplikacji hello: &lt;guid&gt;."

![Adres zwrotny SFX jest niezgodny.][sfx-reply-address-not-match]

#### <a name="reason"></a>Przyczyna
Witaj aplikacji klastra (sieć web), która reprezentuje Eksploratora usługi sieć szkieletowa podejmuje tooauthenticate w usłudze Azure AD, a jako część żądania hello zapewnia zwrotny adres URL przekierowania hello. Ale hello adres URL nie jest wymieniony w aplikacji hello Azure AD **adres URL odpowiedzi** listy.

#### <a name="solution"></a>Rozwiązanie
Na powitania **Konfiguruj** kartę hello klastra aplikacji (aplikacji sieci web), należy dodać hello adresu URL Service Fabric Explorer toohello **adres URL odpowiedzi** listy lub Zastąp hello elementów na liście hello. Po zakończeniu zapisz zmianę.

![Adres url odpowiedzi aplikacji sieci Web][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a>Połącz hello klastra przy użyciu uwierzytelniania usługi Azure AD za pomocą programu PowerShell
Witaj tooconnect klastra sieci szkieletowej usług Użyj hello poniższy przykład polecenia programu PowerShell:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

toolearn temat hello Connect-ServiceFabricCluster polecenia cmdlet, zobacz [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a>Czy można ponownie użyć dzierżawy hello tej samej usługi Azure AD w wielu klastrach?
Tak. Należy jednak pamiętać tooadd hello adresu URL Service Fabric Explorer tooyour klastra (sieć web) aplikacji. W przeciwnym razie Eksploratora usługi sieć szkieletowa nie działa.

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a>Dlaczego nadal należy certyfikat serwera po włączeniu usługi Azure AD?
Klienta fabricclient z rolą i FabricGateway wykonać uwierzytelnianie wzajemne. Podczas uwierzytelniania usługi Azure AD integracji z usługą Azure AD zapewnia klienta serwera toohello tożsamości i tożsamości serwera hello tooverify używany jest certyfikat serwera hello. Aby uzyskać więcej informacji na temat sieci szkieletowej usług certyfikatów, zobacz [certyfikatów X.509 i sieci szkieletowej usług][x509-certificates-and-service-fabric].

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

