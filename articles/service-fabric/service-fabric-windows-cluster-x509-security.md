---
title: "Sieć szkieletowa usług Azure aaaSecure klastra w systemie Windows przy użyciu certyfikatów | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toosecure komunikacji w ramach autonomicznej hello lub prywatnej klastra oraz między klientami i hello klastra."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: fe0ed74c-9af5-44e9-8d62-faf1849af68c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dekapur
ms.openlocfilehash: f0d411963615349a84edfc8125dec4ee5908f146
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a>Zabezpieczanie klastra autonomicznego w systemie Windows za pomocą certyfikatów X.509
W tym artykule opisano, jak toosecure hello komunikacji między hello różnych węzłów w klastrze Windows autonomicznych, a także sposobu tooauthenticate klientów łączących się klastra toothis, za pomocą certyfikatów X.509. Dzięki temu, że tylko autoryzowani użytkownicy mogą uzyskiwać dostęp do klastra hello hello wdrożonych aplikacji i wykonywać zadania zarządzania.  Certyfikat zabezpieczeń powinien być włączony w klastrze hello podczas tworzenia klastra hello.  

Aby uzyskać więcej informacji dotyczących zabezpieczeń klastra, takie jak zabezpieczeń węzła do węzła, węzeł klient zabezpieczeń i kontroli dostępu opartej na rolach, zobacz [klastra scenariusze zabezpieczeń](service-fabric-cluster-security.md).

## <a name="which-certificates-will-you-need"></a>Certyfikatów, które będą potrzebne?
toostart, [Pobierz hello wersjach klastra](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone hello węzłów w klastrze. W hello pobrano pakiet, można znaleźć **ClusterConfig.X509.MultiMachine.json** pliku. Otwórz plik hello i sekcji hello **zabezpieczeń** w obszarze hello **właściwości** sekcji:

```JSON
"security": {
    "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
    "ClusterCredentialType": "X509",
    "ServerCredentialType": "X509",
    "CertificateInformation": {
        "ClusterCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },        
        "ClusterCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ServerCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ServerCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ClientCertificateThumbprints": [
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": false
            },
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ClientCertificateCommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]",
                "CertificateIssuerThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ReverseProxyCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ReverseProxyCertificateCommonNames": {
            "CommonNames": [
                {
                "CertificateCommonName": "[CertificateCommonName]"
                }
            ],
            "X509StoreName": "My"
        }
    }
},
```

W tej sekcji opisano hello certyfikaty, które należy do zabezpieczania autonomiczny klastra systemu Windows. W przypadku określania certyfikatu klastra, należy ustawić wartość hello **ClusterCredentialType** too_**X509**_. W przypadku określania certyfikatu serwera dla połączeń zewnętrznych, ustaw hello **ServerCredentialType** za_**X509**_. Chociaż nie jest to konieczne, zaleca się toohave oba te certyfikaty zabezpieczenie klastra. Jeśli te wartości zostaną ustawione zbyt*X509* , a następnie należy również określić hello odpowiednie certyfikaty lub sieci szkieletowej usług spowoduje zgłoszenie wyjątku. W niektórych scenariuszach tylko możesz toospecify hello _ClientCertificateThumbprints_ lub _ReverseProxyCertificate_. W tych scenariuszach nie należy ustawić _ClusterCredentialType_ lub _ServerCredentialType_ too_X509_.


> [!NOTE]
> A [odcisk palca](https://en.wikipedia.org/wiki/Public_key_fingerprint) jest hello podstawowej tożsamości certyfikatu. Odczyt [jak tooretrieve odcisk palca certyfikatu](https://msdn.microsoft.com/library/ms734695.aspx) toofind limit odcisk palca hello hello certyfikatów, które możesz utworzyć.
> 
> 

Witaj poniższej tabeli wymieniono hello certyfikaty, które będą potrzebne w konfiguracji klastra:

| **Ustawienie CertificateInformation** | **Opis** |
| --- | --- |
| ClusterCertificate |Zalecana dla środowiska testowego. Ten certyfikat jest wymagany toosecure hello komunikacji między węzłami hello w klastrze. Dwa różne certyfikaty, podstawowego i pomocniczego służy do uaktualnienia. Ustaw hello odcisk palca certyfikatu podstawowego hello w hello **odcisk palca** sekcji i który hello pomocniczym w hello **ThumbprintSecondary** zmiennych. |
| ClusterCertificateCommonNames |Zalecana dla środowiska produkcyjnego. Ten certyfikat jest wymagany toosecure hello komunikacji między węzłami hello w klastrze. Można użyć jednego lub dwóch klastra wspólnej nazwy certyfikatów. |
| ServerCertificate |Zalecana dla środowiska testowego. Ten certyfikat jest widoczne toohello klienta po próbie tooconnect toothis klastra. Dla wygody można wybrać toouse hello sam certyfikat dla *ClusterCertificate* i *ServerCertificate*. Do uaktualnienia, można użyć dwóch różnych certyfikatów, podstawowego i pomocniczego. Ustaw hello odcisk palca certyfikatu podstawowego hello w hello **odcisk palca** sekcji i który hello pomocniczym w hello **ThumbprintSecondary** zmiennych. |
| ServerCertificateCommonNames |Zalecana dla środowiska produkcyjnego. Ten certyfikat jest widoczne toohello klienta po próbie tooconnect toothis klastra. Dla wygody można wybrać toouse hello sam certyfikat dla *ClusterCertificateCommonNames* i *ServerCertificateCommonNames*. Można użyć jednego lub dwóch certyfikatu wspólnej nazwy serwerów. |
| ClientCertificateThumbprints |Jest to zestaw certyfikatów, które mają tooinstall na klientach hello uwierzytelniony. Może mieć wiele różnych klientów certyfikatów zainstalowanych na powitania maszyny, które mają tooallow dostępu toohello klastra. Ustaw hello odcisk palca każdy z certyfikatów w hello **CertificateThumbprint** zmiennej. Jeśli ustawisz hello **IsAdmin** za*true*, a następnie powitania klienta przy użyciu tego certyfikatu na nim zainstalowany zrobić administrator działaniach zarządzania na powitania klastra. Jeśli hello **IsAdmin** jest *false*, powitania klienta przy użyciu tego certyfikatu można wykonać tylko akcje hello dozwolone praw dostępu użytkownika, zwykle tylko do odczytu. Aby uzyskać więcej informacji na temat ról przeczytaj [oparta na rolach kontrola dostępu (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac) |
| ClientCertificateCommonNames |Zestaw hello nazwa pospolita hello pierwszego certyfikatu klienta na powitania **CertificateCommonName**. Witaj **CertificateIssuerThumbprint** jest hello odcisk palca wystawcy hello tego certyfikatu. Odczyt [Praca z certyfikatami](https://msdn.microsoft.com/library/ms731899.aspx) tooknow więcej informacji na temat wspólnej nazwy i Witaj Wystawca. |
| ReverseProxyCertificate |Zalecana dla środowiska testowego. Jest opcjonalny certyfikat, który może być określony, jeśli chcesz, aby toosecure Twojego [wstecznego Proxy](service-fabric-reverseproxy.md). Upewnij się, że reverseProxyEndpointPort jest ustawiony w elementów NodeType, jeśli używasz tego certyfikatu. |
| ReverseProxyCertificateCommonNames |Zalecana dla środowiska produkcyjnego. Jest opcjonalny certyfikat, który może być określony, jeśli chcesz, aby toosecure Twojego [wstecznego Proxy](service-fabric-reverseproxy.md). Upewnij się, że reverseProxyEndpointPort jest ustawiony w elementów NodeType, jeśli używasz tego certyfikatu. |

Oto przykład konfiguracji klastra gdzie dostarczono hello certyfikatów klastra, klientów i serwerów. Należy pamiętać, że dla klastra / server / reverseProxy certyfikatów, odcisk palca i nazwa pospolita nie są dozwolone toobe skonfigurowanych dla hello sam typ certyfikatu.

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace hello localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
            "ClusterCredentialType": "X509",
            "ServerCredentialType": "X509",
            "CertificateInformation": {
                "ClusterCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myClusterCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ServerCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myServerCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ClientCertificateThumbprints": [{
                    "CertificateThumbprint": "c4 c18 8e aa a8 58 77 98 65 f8 61 4a 0d da 4c 13 c5 a1 37 6e",
                    "IsAdmin": false
                }, {
                    "CertificateThumbprint": "71 de 04 46 7c 9e d0 54 4d 02 10 98 bc d4 4c 71 e1 83 41 4e",
                    "IsAdmin": true
                }]
            }
        },
        "reliabilityLevel": "Bronze",
        "nodeTypes": [{
            "name": "NodeType0",
            "clientConnectionEndpointPort": "19000",
            "clusterConnectionEndpointPort": "19001",
            "leaseDriverEndpointPort": "19002",
            "serviceConnectionEndpointPort": "19003",
            "httpGatewayEndpointPort": "19080",
            "applicationPorts": {
                "startPort": "20001",
                "endPort": "20031"
            },
            "ephemeralPorts": {
                "startPort": "20032",
                "endPort": "20062"
            },
            "isPrimary": true
        }
         ],
        "fabricSettings": [{
            "name": "Setup",
            "parameters": [{
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
            }, {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
            }]
        }]
    }
}
 ```

## <a name="certificate-roll-over"></a>Przerzuć certyfikatu
Używając nazwa pospolita certyfikatu zamiast odcisku palca, wycofywanie certyfikatu za pośrednictwem nie wymaga uaktualnienia konfiguracji klastra.
Jeśli wycofywanie certyfikatu za pośrednictwem obejmuje wystawcy przerzucane, pamiętaj o hello starego wystawcy certyfikatu w magazynie certyfikatów hello co najmniej 2 godziny po zainstalowaniu hello nowego wystawcy certyfikatu.

## <a name="acquire-hello-x509-certificates"></a>Uzyskanie certyfikatów X.509 hello
toosecure komunikacji w ramach klastra hello, musisz najpierw certyfikatów X.509 tooobtain dla węzłów klastra. Ponadto toolimit toothis połączenia klastra tooauthorized maszyny/użytkownicy, będzie konieczne tooobtain i instalowania certyfikatów dla komputerów klienckich hello.

W przypadku klastrów z systemem obciążeń produkcyjnych należy używać [urzędu certyfikacji,](https://en.wikipedia.org/wiki/Certificate_authority) podpisany klastra hello toosecure certyfikatu X.509. Szczegółowe informacje dotyczące uzyskiwania tych certyfikatów, przejdź zbyt[porady: uzyskiwanie certyfikatu](http://msdn.microsoft.com/library/aa702761.aspx).

W przypadku klastrów korzystających do celów testowych można toouse certyfikatu z podpisem własnym.

## <a name="optional-create-a-self-signed-certificate"></a>Opcjonalnie: Utwórz certyfikat z podpisem własnym
Toouse hello jest jednym ze sposobów toocreate podpisanych certyfikatów, które mogą być chronione poprawnie *CertSetup.ps1* skryptu w folderze zestawu SDK usług sieci szkieletowej hello w katalogu hello *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*. Edytowanie tego pliku toochange hello domyślną nazwę certyfikatu hello (Wyszukaj wartość hello *CN = ServiceFabricDevClusterCert*). Uruchom ten skrypt jako `.\CertSetup.ps1 -Install`.

Obecnie można wyeksportować plik PFX tooa hello certyfikatu chronione hasłem. Najpierw pobierz hello odcisk palca certyfikatu hello. Z hello *Start* menu, uruchom hello *zarządzanie certyfikatami komputera*. Przejdź toohello **komputera lokalnego** folder i Znajdź hello certyfikatu należy po prostu utworzyć. Kliknij dwukrotnie tooopen certyfikatu hello go, wybierz opcję hello *szczegóły* i przewiń w dół toohello *odcisk palca* pola. Skopiuj wartość odcisku palca hello do polecenia programu PowerShell hello poniżej, po usunięciu hello spacji.  Zmień hello `String` wartość tooprotect odpowiedniego bezpieczne hasło tooa go i uruchom powitania po w programie PowerShell:

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

Szczegóły hello toosee zainstalowanego na powitania certyfikatu komputera należy uruchomić następujące polecenia programu PowerShell hello:

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

Alternatywnie, jeśli masz subskrypcję platformy Azure, wykonaj sekcji hello [Dodaj certyfikaty tooKey magazynu](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).

## <a name="install-hello-certificates"></a>Instalowanie certyfikatów hello
Po utworzeniu certyfikaty, można je zainstalować na węzłach klastra hello. Węzły muszą toohave hello najnowsze środowiska Windows PowerShell 3.x na nich zainstalowany. Konieczne będzie toorepeat następujące kroki na każdym węźle, zarówno w przypadku klastra, jak i serwera certyfikatów i wszystkie pomocnicze certyfikaty.

1. Skopiuj hello PFX pliki toohello węzła.
2. Otwórz okno programu PowerShell jako administrator, a następnie wprowadź hello następujące polecenia. Zastąp hello *$pswd* hasłem hello używane toocreate tego certyfikatu. Zastąp hello *$PfxFilePath* mającym pełną ścieżkę hello hello PFX skopiowanych toothis węzła.
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. Teraz ustawić hello kontrolę dostępu dla tego certyfikatu, aby proces sieci szkieletowej usług hello, który jest uruchamiana hello konto Usługa sieciowa, może być używany przez uruchomienie hello następującego skryptu. Podaj odcisk palca hello hello certyfikatu i 'Usługa sieciowa"hello konta usługi. Możesz sprawdzić hello tej listy ACL w certyfikacie hello są poprawne, otwierając hello certyfikatu w *Start* > *zarządzanie certyfikatami komputera* i patrzeć *wszystkie zadania*  >  *Zarządzaj kluczami prywatnymi*.
   
    ```powershell
    param
    (
    [Parameter(Position=1, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$pfxThumbPrint,
   
    [Parameter(Position=2, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$serviceAccount
    )
   
    $cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object -FilterScript { $PSItem.ThumbPrint -eq $pfxThumbPrint; }
   
    # Specify hello user, hello permissions and hello permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of hello machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get hello current acl of hello private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add hello new ace toohello acl of hello private key
    $acl.SetAccessRule($accessRule)
   
    # Write back hello new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe hello access rights currently assigned toothis certificate.
    get-acl $keyFullPath| fl
    ```
4. Powtórz powyższe kroki powitania dla każdego certyfikatu serwera. Umożliwia także te kroki tooinstall hello certyfikaty klienta na powitania maszynach, które mają tooallow dostępu toohello klastra.

## <a name="create-hello-secure-cluster"></a>Tworzenie klastra bezpiecznego hello
Po skonfigurowaniu hello **zabezpieczeń** sekcji hello **ClusterConfig.X509.MultiMachine.json** plików, można przejść za[tworzenia klastra](service-fabric-cluster-creation-for-windows-server.md#createcluster) tooconfigure sekcji Witaj węzłów i utworzenie klastra autonomiczny hello. Pamiętaj toouse hello **ClusterConfig.X509.MultiMachine.json** pliku podczas tworzenia klastra hello. Na przykład polecenie może wyglądać hello następujące czynności:

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

Po utworzeniu hello bezpiecznego autonomicznego Windows klastra pomyślnie uruchomione, a następnie Instalator tooit tooconnect uwierzytelnionym klientom Witaj, wykonaj sekcji hello [Connect tooa bezpiecznego klastra przy użyciu programu PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit. Na przykład:

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

Następnie możesz uruchomić inne toowork poleceń programu PowerShell z tym klastrem. Na przykład [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow listy węzłów w tym klastrze bezpieczne.


tooremove hello klastra, połączenia z toohello węzła w klastrze hello którego został pobrany pakiet sieci szkieletowej usług hello, otwórz wiersz polecenia i przejdź do folderu pakietu toohello. Teraz uruchom hello następujące polecenie:

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> Nieprawidłowy certyfikat konfiguracji może uniemożliwić powtarzający się podczas wdrażania klastra hello. tooself-diagnozowanie problemów z zabezpieczeniami, zapoznaj się w grupie podglądu zdarzeń *Dzienniki aplikacji i usług* > *sieci szkieletowej usług Microsoft*.
> 
> 

