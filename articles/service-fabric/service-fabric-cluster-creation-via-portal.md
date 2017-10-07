---
title: "aaaCreate sieci szkieletowej usług dla klastra w hello portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak hello tooset zapasowej bezpiecznego klastra sieci szkieletowej usług za pomocą usługi Azure w portalu Azure i usługi Azure Key Vault."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a>Tworzenie klastra sieci szkieletowej usług na platformie Azure przy użyciu hello portalu Azure
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Witryna Azure Portal](service-fabric-cluster-creation-via-portal.md)
> 
> 

Jest to przewodnik krok po kroku, który przeprowadzi Cię przez kolejne hello procedurę konfigurowania klastra sieci szkieletowej usług bezpiecznej platformie Azure przy użyciu hello portalu Azure. Ten przewodnik przeprowadzi Cię przez hello następujące kroki:

* Konfigurowanie usługi Key Vault toomanage klucze dla zabezpieczenia klastra.
* Tworzenie klastra zabezpieczonych na platformie Azure za pośrednictwem hello portalu Azure.
* Uwierzytelnianie za pomocą certyfikatów Administratorzy.

> [!NOTE]
> Dla bardziej zaawansowanych opcji zabezpieczeń, takich jak uwierzytelnianie użytkowników w usłudze Azure Active Directory oraz konfigurowania certyfikatów do zabezpieczenia aplikacji [tworzenia klastra przy użyciu usługi Azure Resource Manager][create-cluster-arm].
> 
> 

Bezpieczne klaster jest klastrem uniemożliwiający operacji toomanagement nieautoryzowanym dostępem, w tym wdrażanie, uaktualnianie i usuwanie aplikacji, usług i danych hello, które zawierają. Niezabezpieczone klaster jest klastrem informujący o tym, czy każdy połączyć tooat w dowolnym momencie i wykonywać operacje zarządzania. Chociaż jest to możliwe toocreate niezabezpieczone klastra, jest **zdecydowanie zalecane toocreate bezpiecznego klastra**. Niezabezpieczone klastra **nie można zabezpieczyć później** — należy utworzyć nowy klaster.

Pojęcia dotyczące Hello są hello identyczne tworzenia bezpiecznych klastrów, czy klastry hello są klastry z systemem Linux lub klastry z systemem Windows. Aby uzyskać więcej informacji i pomocnika skryptów tworzenia bezpiecznych klastrów systemu Linux, zobacz [tworzenia bezpiecznych klastrów w systemie Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters). Hello uzyskany przez skrypt pomocnika hello podane parametry mogą wprowadzać bezpośrednio w portalu hello zgodnie z opisem w sekcji hello [tworzenia klastra w portalu Azure hello](#create-cluster-portal).

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure
Ten przewodnik po używa [programu Azure PowerShell][azure-powershell]. Przy uruchamianiu nowej sesji programu PowerShell, zaloguj się za tooyour konto platformy Azure i wyboru subskrypcji przed wykonaniem polecenia platformy Azure.

Zaloguj się na koncie tooyour azure:

```powershell
Login-AzureRmAccount
```

Wybierz subskrypcję:

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a>Konfigurowanie usługi Key Vault
Ta część przewodnika hello przeprowadzi Cię przez utworzenie klucza magazynu dla klastra sieci szkieletowej usług platformy Azure i dla aplikacji sieci szkieletowej usług. Aby uzyskać pełne informacje na Key Vault, zobacz hello [Key Vault Wprowadzenie — przewodnik][key-vault-get-started].

Platforma Service Fabric korzysta toosecure certyfikatów X.509 klastra. Usługa Azure Key Vault jest toomanage używane certyfikaty dla klastrów sieci szkieletowej usług platformy Azure. Po wdrożeniu klastra w systemie Azure hello dostawcy zasobów platformy Azure jest odpowiedzialny za tworzenie klastrów usługi sieć szkieletowa ściąga certyfikaty z magazynu kluczy i instaluje je w klastrze hello maszyn wirtualnych.

Witaj poniższym diagramie przedstawiono relację hello Key Vault, klaster sieci szkieletowej usług i hello dostawcy zasobów platformy Azure, który wykorzystuje certyfikaty przechowywane w magazynie kluczy, podczas tworzenia klastra:

![Instalacja certyfikatu][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów
pierwszym krokiem Hello jest toocreate nową grupę zasobów dla usługi Key Vault. Wprowadzenie klucza magazynu do własnego grupy zasobów jest zalecane, dzięki czemu można usunąć grup zasobów obliczeniowych i przestrzeni dyskowej — takich jak grupy zasobów hello ma klastra usługi sieć szkieletowa — bez utraty z kluczy i kluczy tajnych. Witaj grupę zasobów, która ma magazyn kluczy musi należeć do hello hello klastra, który go używa tego samego regionu.

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a>Utwórz magazyn kluczy
Utwórz magazyn kluczy w hello nową grupę zasobów. Witaj Key Vault **musi być włączona dla wdrożenia** tooallow hello certyfikaty tooget dostawcy zasobów sieci szkieletowej usług z niego i zainstalować na węzłach klastra:

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
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

Jeśli masz istniejący magazyn kluczy, możesz je włączyć, wdrożenie przy użyciu wiersza polecenia platformy Azure:

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a>Dodaj certyfikaty tooKey magazynu
Certyfikaty są używane w sieci szkieletowej usług tooprovide uwierzytelnianie i szyfrowanie toosecure różnych aspektów klastra i jego zastosowań. Aby uzyskać więcej informacji dotyczących używania certyfikatów w sieci szkieletowej usług, zobacz [scenariusze zabezpieczeń klastra sieci szkieletowej usług][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Klaster a serwera certyfikatów (wymagane)
Ten certyfikat jest wymagany toosecure klastra i zapobiec tooit nieautoryzowanego dostępu. Udostępnia ona zabezpieczeń klastra na kilka sposobów:

* **Uwierzytelnianie klastra:** uwierzytelnia komunikacji między węzłami w Federacji klastra. Tylko węzły, które można potwierdzić swoją tożsamość, z tym certyfikatem może dołączać hello klastra.
* **Uwierzytelnianie serwera:** uwierzytelnia hello klastra zarządzania punkty końcowe tooa zarządzania klienta, tak, aby hello klienta zarządzania zna jest mówić toohello rzeczywistych klastra. Ten certyfikat zapewnia również SSL hello interfejsu API zarządzania HTTPS oraz Service Fabric Explorer, za pośrednictwem protokołu HTTPS.

tooserve tych celów hello certyfikatu musi spełniać następujące wymagania hello:

* Witaj, certyfikat musi zawierać klucz prywatny.
* Witaj certyfikatu musi zostać utworzony dla wymiany kluczy, można eksportować tooa plik wymiany informacji osobistych (pfx).
* Hello nazwa podmiotu certyfikatu musi odpowiadać klastra hello tooaccess hello domeny używane w sieci szkieletowej usług. Jest to wymagane tooprovide protokołu SSL dla punktów końcowych HTTPS zarządzania i Service Fabric Explorer hello klastra. Nie można uzyskać certyfikatu SSL z urzędu certyfikacji (CA) w celu hello `.cloudapp.azure.com` domeny. Możliwość nabycia niestandardowej nazwy domeny dla klastra. W przypadku żądania certyfikatu na podstawie nazwy podmiotu certyfikatu hello urzędu certyfikacji musi odpowiadać nazwie domeny niestandardowej hello używane dla klastra.

### <a name="client-authentication-certificates"></a>Certyfikaty uwierzytelniania klienta
Certyfikaty klienta dodatkowe uwierzytelnianie Administratorzy dla zadań zarządzania w klastrze. Sieć szkieletowa usług ma dwa poziomy dostępu: **admin** i **użytkownika tylko do odczytu**. Co najmniej jeden certyfikat dla dostępu administracyjnego należy używać. Dodatkowe dostępu na poziomie użytkownika należy podać oddzielny certyfikat. Aby uzyskać więcej informacji na dostęp do ról, zobacz [kontroli dostępu opartej na rolach dla klientów usługi sieć szkieletowa][service-fabric-cluster-security-roles].

Nie trzeba tooupload klienta uwierzytelniania certyfikatów tooKey magazynu toowork z sieci szkieletowej usług. Te certyfikaty muszą tylko toobe podane toousers, którzy mają uprawnienia do zarządzania klastrem. 

> [!NOTE]
> Usługa Azure Active Directory jest hello zalecany sposób tooauthenticate klientów dla klastra operacji zarządzania. toouse usługi Azure Active Directory, należy najpierw [Tworzenie klastra przy użyciu usługi Azure Resource Manager][create-cluster-arm].
> 
> 

### <a name="application-certificates-optional"></a>Certyfikaty aplikacji (opcjonalnie)
Dowolna liczba dodatkowych certyfikatów można zainstalować w klastrze dla aplikacji ze względów bezpieczeństwa. Przed utworzeniem klastra, należy wziąć pod uwagę scenariusze zabezpieczeń aplikacji hello, które wymagają toobe certyfikat zainstalowany na węzłach hello, takich jak:

* Szyfrowanie i odszyfrowywanie wartości konfiguracji aplikacji
* Szyfrowanie danych w węzłach podczas replikacji 

Nie można skonfigurować certyfikaty aplikacji, podczas tworzenia klastra za pośrednictwem hello portalu Azure. Certyfikaty aplikacji tooconfigure podczas konfiguracji klastra, należy najpierw [Tworzenie klastra przy użyciu usługi Azure Resource Manager][create-cluster-arm]. Można również dodać klastra toohello certyfikatów aplikacji po jego utworzeniu.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Formatowanie certyfikatów do użytku dostawcy zasobów platformy Azure
Pliki klucza prywatnego (pfx) można dodany i używany bezpośrednio za pomocą usługi Key Vault. Dostawcy zasobów platformy Azure hello wymaga jednak toobe klucze przechowywane w formacie JSON specjalny, który zawiera PFX hello jako base-64 zakodowany ciąg i hello hasło klucza prywatnego. tooaccommodate tych wymagań, klucze musi być umieszczona w ciągu JSON i następnie przechowywane jako *kluczy tajnych* w magazynie kluczy.

toomake to łatwiej przetwarzania, moduł programu PowerShell jest [dostępne w witrynie GitHub][service-fabric-rp-helpers]. Wykonaj te kroki toouse hello modułu:

1. Pobierz całą zawartość repozytorium hello hello do katalogu lokalnego. 
2. Zaimportuj moduł hello w oknie programu PowerShell:

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

Witaj `Invoke-AddCertToKeyVault` polecenia w tym module środowiska PowerShell automatycznie formatuje klucz prywatny certyfikatu do ciągu JSON i przekazanie jej tooKey magazynu. Użyj go tooadd hello klastra certyfikat i wszelkie dodatkowe aplikacji certyfikaty tooKey magazynu. Powtórz ten krok dla wszystkich dodatkowych certyfikatów, które chcesz tooinstall w klastrze.

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

Są to wszystkie wymagania wstępne usługi Key Vault hello do konfigurowania szablonu usługi Resource Manager klastra sieci szkieletowej usług, który instaluje certyfikatów dla uwierzytelniania węzła, zarządzania punktu końcowego zabezpieczeń i uwierzytelniania oraz wszelkie dodatkowe zabezpieczenia aplikacji Funkcje, które korzystają z certyfikatów X.509. W tym momencie powinny mieć teraz powitania po zakończeniu instalacji na platformie Azure:

* Grupa zasobów magazynu kluczy
  * Usługa Key Vault
    * Certyfikat uwierzytelniania serwera klastra

< /a "Tworzenie klastra portal" ></a>

## <a name="create-cluster-in-hello-azure-portal"></a>Tworzenie klastra w hello portalu Azure
### <a name="search-for-hello-service-fabric-cluster-resource"></a>Wyszukaj hello zasobu klastra usługi sieć szkieletowa
![Wyszukiwanie szablonu klastra sieci szkieletowej usług na powitania portalu Azure.][SearchforServiceFabricClusterTemplate]

1. Zaloguj się toohello [portalu Azure][azure-portal].
2. Kliknij przycisk **nowy** tooadd nowego szablonu zasobów. Wyszukaj hello szablonu klastra sieci szkieletowej usług w hello **Marketplace** w obszarze **wszystko**.
3. Wybierz **klastra sieci szkieletowej usług** z listy hello.
4. Przejdź toohello **klastra sieci szkieletowej usług** bloku, kliknij przycisk **Utwórz**,
5. Witaj **klastra tworzenia sieci szkieletowej usług** bloku ma hello następujące cztery kroki.

#### <a name="1-basics"></a>1. Podstawy
![Zrzut ekranu przedstawiający tworzenie nowej grupy zasobów.][CreateRG]

W bloku podstawowe służące hello należy tooprovide hello podstawowe szczegóły dla klastra.

1. Wprowadź nazwę hello klastra.
2. Wprowadź **nazwy użytkownika** i **hasło** dla pulpitu zdalnego dla hello maszyn wirtualnych.
3. Upewnij się, że hello tooselect **subskrypcji** mają Twojej toobe klastra wdrożone, zwłaszcza, jeśli masz wiele subskrypcji.
4. Utwórz **nową grupę zasobów**. Jest najlepszym toogive go hello samą nazwę jak hello klastra, ponieważ pomaga w znajdowaniu je później, szczególnie w przypadku, gdy są w trakcie wdrażania tooyour zmiany toomake lub usunięciu klastra.
   
   > [!NOTE]
   > Chociaż użytkownik może określić toouse istniejącą grupę zasobów, jest dobrym rozwiązaniem toocreate nową grupę zasobów. Dzięki temu można łatwo toodelete klastrów, w których nie ma potrzeby.
   > 
   > 
5. Wybierz hello **regionu** w której ma zostać toocreate hello klastra. Witaj, znajduje się w tym samym regionie, który klucz magazynu, należy użyć.

#### <a name="2-cluster-configuration"></a>2. Konfiguracja klastra
![Tworzenie typu węzła][CreateNodeType]

Skonfiguruj węzły klastra. Typy węzłów zdefiniować rozmiary maszyn wirtualnych hello hello liczbę maszyn wirtualnych i ich właściwości. Klaster może zawierać więcej niż jeden typ węzła, ale typ węzła podstawowego hello (hello w pierwszej kolejności należy zdefiniować w portalu hello) musi mieć co najmniej pięć maszyn wirtualnych, jak jest to typ węzła hello rozmieszczenia usługi sieć szkieletowa usług systemowych. Nie należy konfigurować **właściwości umieszczania** ponieważ domyślna właściwość umieszczania "NodeTypeName" są dodawane automatycznie.

> [!NOTE]
> Typowy scenariusz dla wielu typów węzła jest aplikacja, która zawiera usługi frontonu i zaplecza. Usługa frontonu hello tooput na mniejsze maszyn wirtualnych (na przykład D2 rozmiarów maszyn wirtualnych) z toohello otwartych portów internetowych, ale ma usługi zaplecza hello tooput na większych maszyn wirtualnych (o rozmiarów maszyn wirtualnych, takie jak D4, D6 D15 i tak dalej) z nie ma otwartych portów połączonych z Internetem.
> 
> 

1. Wybierz nazwę dla danego typu węzła (1 znaków too12 zawierających tylko litery i cyfry).
2. Minimalna Hello **rozmiar** maszyn wirtualnych dla węzła podstawowego hello typu jest wymuszany przez hello **trwałości** warstwy wybierz hello klastra. Witaj domyślnym warstwa trwałości hello jest brązowa. Aby uzyskać więcej informacji o trwałości, zobacz [jak toochoose hello sieci szkieletowej usług klastra niezawodność i trwałość][service-fabric-cluster-capacity].
3. Wybierz rozmiar maszyny Wirtualnej hello i warstwę cenową. Maszyny wirtualne D-series mają dyski SSD i zaleca aplikacji stanowych. Użyj dowolnej jednostki SKU maszyny Wirtualnej z częściowa rdzeni lub nie mają mniej niż 7 GB pojemności dysku. 
4. Minimalna Hello **numer** maszyn wirtualnych dla węzła podstawowego hello typu jest wymuszany przez hello **niezawodności** warstwy wybierzesz. domyślnym Hello warstwa niezawodności hello jest Silver. Aby uzyskać więcej informacji o niezawodności, zobacz [jak toochoose hello sieci szkieletowej usług klastra niezawodność i trwałość][service-fabric-cluster-capacity].
5. Wybierz hello liczbę maszyn wirtualnych dla typu węzła hello. Możesz skalować w górę lub w dół hello liczbę maszyn wirtualnych w typ węzła później, ale dla typu węzła podstawowego hello, minimalna hello jest wymuszany przez hello poziomu niezawodności, który wybrano. Inne typy węzłów może mieć co najmniej 1 maszyny wirtualnej.
6. Skonfiguruj niestandardowe punkty końcowe. To pole umożliwia tooenter rozdzielana przecinkami lista portów, które mają tooexpose za pośrednictwem toohello modułu równoważenia obciążenia Azure hello publicznego Internetu dla aplikacji. Na przykład, jeśli planujesz toodeploy klastra tooyour aplikacji sieci web, wpisz "80" tutaj tooallow ruch na porcie 80 do klastra. Aby uzyskać więcej informacji dotyczących punktów końcowych, zobacz [komunikacji z aplikacjami][service-fabric-connect-and-communicate-with-services]
7. Konfigurowanie klastra **diagnostyki**. Domyślnie diagnostycznych są włączone na tooassist z klastra z rozwiązywania problemów. Jeśli chcesz diagnostyki toodisable zmienić hello **stan** Przełącz zbyt**poza**. Wyłączenie diagnostyki jest **nie** zalecane.
8. Wybierz hello uaktualnianie tryb ma ustawioną wartość klastra. Wybierz **automatyczne**, jeśli chcesz hello systemu tooautomatically odbioru hello najnowszej dostępnej wersji i spróbuj tooupgrade Twojego tooit klastra. Ustaw tryb hello zbyt**ręcznego**, jeśli chcesz, aby toochoose obsługiwanej wersji.

> [!NOTE]
> Firma Microsoft obsługuje tylko klastry, które są z obsługiwanymi wersjami usługi sieci szkieletowej. Po wybraniu hello **ręcznego** trybie są tworzone na powitania odpowiedzialność tooupgrade wersji tooa obsługiwane klastra. Witaj można znaleźć więcej szczegółów na tryb uaktualniania sieci szkieletowej hello [dokumentu usługi sieci szkieletowej klastra uaktualnienia.][service-fabric-cluster-upgrade]
> 
> 

#### <a name="3-security"></a>3. Bezpieczeństwo
![Zrzut ekranu przedstawiający konfiguracjach zabezpieczeń w portalu Azure.][SecurityConfigs]

Witaj ostatnim krokiem jest tooprovide certyfikatu informacji toosecure hello klastra przy użyciu hello magazyn kluczy i certyfikatów informacji utworzony wcześniej.

* Wypełniania pól podstawowego certyfikatu hello z danych wyjściowych hello uzyskane z przekazywania hello **certyfikatu klastra** tooKey magazynu przy użyciu hello `Invoke-AddCertToKeyVault` polecenia programu PowerShell.

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* Sprawdź hello **Skonfiguruj ustawienia zaawansowane** polu tooenter certyfikaty klientów dla **klienta administrator** i **klienta tylko do odczytu**. W tych polach wprowadź hello odcisk palca certyfikatu klienta administratora i hello odcisk palca certyfikatu klienta użytkownika tylko do odczytu, jeśli ma to zastosowanie. Gdy administratorzy prób tooconnect toohello klastra, otrzymali dostępu tylko wtedy, gdy mają certyfikat z odciskiem palca, odpowiadającą wartości odcisku palca hello wprowadzanym w tym miejscu.  

#### <a name="4-summary"></a>4. Podsumowanie
![Zrzut ekranu przedstawiający tablicy start hello wyświetlanie "Klastra sieci szkieletowej usług wdrażanie". ][Notifications]

Utworzenie klastra hello toocomplete, kliknij przycisk **Podsumowanie** toosee hello konfiguracje, które zostały podane lub pobrać hello klastra które używane toodeploy szablonu usługi Azure Resource Manager. Po dostarczeniu hello ustawienia obowiązkowe, hello **OK** przycisk staje się zielony i można uruchomić procesu tworzenia klastra hello, klikając go.

Postęp tworzenia hello w powiadomieniach hello jest widoczny. (Kliknij ikonę dzwonka"hello" w pobliżu pasek stanu hello na powitania górnym rogu ekranu). Jeśli kliknięto **tooStartboard numeru Pin** podczas tworzenia klastra hello, zobaczysz **wdrażanie klastra sieci szkieletowej usług** przypięty toohello **Start** tablicy.

### <a name="view-your-cluster-status"></a>Wyświetl stan sieci klastra
![Zrzut ekranu przedstawiający szczegółów klastra hello w pulpicie nawigacyjnym.][ClusterDashboard]

Po utworzeniu klastra można sprawdzić w portalu hello klastra:

1. Przejdź za**Przeglądaj** i kliknij przycisk **klastry usługi sieć szkieletowa**.
2. Znajdź klastra i kliknij ją.
3. Możesz teraz przeglądać szczegóły hello klastra na pulpicie nawigacyjnym hello, w tym klastrze hello publiczny punkt końcowy i tooService łącze Eksploratora sieci szkieletowej.

Witaj **Monitor węzła** sekcji w bloku pulpit nawigacyjny klastra hello wskazuje hello liczbę maszyn wirtualnych, które są w dobrej kondycji i nie działa prawidłowo. Można znaleźć więcej szczegółów na temat kondycji hello klastra na [wprowadzenie modelu kondycji sieci szkieletowej usług][service-fabric-health-introduction].

> [!NOTE]
> Klastrów sieci szkieletowej usług wymaga określonej liczby węzłów toobe zawsze toomaintain dostępności i Zachowaj stan — określonego tooas "utrzymywania kworum". Z tego, zwykle nie jest bezpieczne tooshut dół wszystkie komputery w klastrze hello, chyba że najpierw wykonali [pełnej kopii zapasowej według stanu][service-fabric-reliable-services-backup-restore].
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a>Połączenie zdalne tooa wystąpienia zestawu skalowania maszyn wirtualnych lub węzła klastra
Każdy z elementów NodeType hello należy określić w wynikach klastra w zestawu skalowania maszyn wirtualnych pobieranie konfiguracji. Zobacz [połączenie zdalne wystąpienia zestawu skalowania maszyn wirtualnych tooa] [ remote-connect-to-a-vm-scale-set] szczegółowe informacje.

## <a name="next-steps"></a>Następne kroki
W tym momencie masz bezpiecznego klastra przy użyciu certyfikatów dla uwierzytelniania zarządzania. Następnie [połączenia klastra tooyour](service-fabric-connect-to-secure-cluster.md) i Dowiedz się, jak za[Zarządzanie klucze tajne aplikacji](service-fabric-application-secret-management.md).  Zapoznaj się z [opcje pomocy technicznej usługi sieć szkieletowa](service-fabric-support.md).

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
