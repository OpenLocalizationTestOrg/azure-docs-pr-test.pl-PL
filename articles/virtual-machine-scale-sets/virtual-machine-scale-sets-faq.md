---
title: "często zadawane pytania dotyczące zestawach skali maszyn wirtualnych aaaAzure | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi toofrequently zadawane pytania dotyczące zestawy skalowania maszyny wirtualnej."
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a>Zestawach skali maszyny wirtualnej platformy Azure — często zadawane pytania

Odpowiedzi ustawia toofrequently zadawane pytania dotyczące skalowania maszyny wirtualnej na platformie Azure.

## <a name="autoscale"></a>Automatyczne skalowanie

### <a name="what-are-best-practices-for-azure-autoscale"></a>Jakie są najlepsze rozwiązania dotyczące skalowania automatycznego Azure?

Aby uzyskać najlepsze rozwiązania dotyczące skalowania automatycznego, zobacz [najlepsze rozwiązania w przypadku maszyn wirtualnych, skalowanie automatyczne](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a>Gdzie można znaleźć nazwy metryki Skalowanie automatyczne, który wykorzystuje metryki oparta na hoście

Metryki nazw dla Skalowanie automatyczne, który wykorzystuje metryki oparta na hoście, zobacz [obsługiwane metryki z monitorem Azure](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a>Czy istnieją przykładami Skalowanie automatyczne w oparciu o długości kolejek i tematów usługi Azure Service Bus?

Tak. Przykłady Skalowanie automatyczne w oparciu o długości kolejek i tematów usługi Azure Service Bus, zobacz [metryki wspólnej Skalowanie automatyczne Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).

Dla kolejki usługi Service Bus Użyj następującego formatu JSON hello:

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

Kolejki magazynu należy użyć powitania po JSON:

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

Zastąp wartości przykładowe zasobu Uniform Resource Identifier (URI).


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a>Czy należy skalowania automatycznego przy użyciu metryk oparta na hoście lub rozszerzenia diagnostyki?

Ustawienia skalowania automatycznego można tworzyć na metryki poziomu hosta toouse maszyny Wirtualnej lub metryki na podstawie systemu operacyjnego gościa.

Aby uzyskać listę obsługiwanych metryki, zobacz [metryki wspólnej Skalowanie automatyczne Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics). 

Aby uzyskać pełny przykład dla zestawy skalowania maszyny wirtualnej, zobacz [konfiguracji automatycznego skalowania zaawansowanych przy użyciu szablonów usługi Resource Manager dla zestawy skalowania maszyny wirtualnej](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets). 

Witaj w przykładzie użyto hello poziomie hosta Procesora metryk i metrykę liczba wiadomości.



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a>Jak ustawić reguły alertów na zestaw skali maszyny wirtualnej?

Alerty można tworzyć na metryki dla zestawy skalowania maszyny wirtualnej za pomocą programu PowerShell lub interfejsu wiersza polecenia platformy Azure. Aby uzyskać więcej informacji, zobacz [Azure PowerShell Monitor szybki start przykłady](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) i [Azure Monitor i platform interfejsu wiersza polecenia Szybki start przykłady](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).

Element TargetResourceId zestawu skali maszyny wirtualnej hello Hello wygląda następująco: 

/Subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/Providers/Microsoft.COMPUTE/virtualMachineScaleSets/yourvmssname

Można wybrać dowolnego licznika wydajności maszyny Wirtualnej jako tooset metryki hello alert dla. Aby uzyskać więcej informacji, zobacz [metryki systemu operacyjnego gościa dla maszyn wirtualnych Menedżera zasobów systemu Windows](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) i [metryki systemu operacyjnego gościa dla maszyn wirtualnych systemu Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) w hello [Azure Monitor Skalowanie automatyczne wspólnej metryki](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)artykułu.

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a>Jak skonfigurować automatycznego skalowania w skali maszyny wirtualnej ustawić przy użyciu programu PowerShell?

tooset się automatycznego skalowania w skali maszyny wirtualnej ustawić przy użyciu programu PowerShell, zobacz hello blogu [konfiguracji tooadd tooan skalowania automatycznego skalowania maszyny wirtualnej platformy Azure](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).




## <a name="certificates"></a>Certyfikaty

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a>Jak bezpiecznie wysłać toohello certyfikatów maszyny Wirtualnej? Jak udostępnić toorun zestaw skali maszyny wirtualnej witryny sieci Web, gdzie hello SSL dla witryny sieci Web hello jest dostarczany bezpiecznie z konfiguracji certyfikatu? (hello typowych operacji obrotu certyfikatu może być prawie hello jak w przypadku operacji aktualizacji konfiguracji.) Czy masz przykładem toodo to? 

toosecurely wysłać toohello certyfikatów maszyny Wirtualnej, należy zainstalować certyfikat klienta, bezpośrednio do magazynu certyfikatów systemu Windows z magazynu kluczy powitania klienta.

Użyj następującego formatu JSON hello:

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

Kod Hello obsługuje system Windows i Linux.

Aby uzyskać więcej informacji, zobacz [Tworzenie lub aktualizacja zestawu skalowania maszyn wirtualnych](https://msdn.microsoft.com/library/mt589035.aspx).


### <a name="example-of-self-signed-certificate"></a>Przykład certyfikatu z podpisem własnym

1.  Tworzenie certyfikatu z podpisem własnym w magazynie kluczy.

    Użyj następującego polecenia programu PowerShell hello:

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    To polecenie umożliwia hello dane wejściowe dla szablonu usługi Azure Resource Manager hello.

    Przykład toocreate certyfikatu z podpisem własnym w magazynie kluczy, zobacz temat [scenariusze zabezpieczeń klastra sieci szkieletowej usług](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).

2.  Zmień hello szablonu usługi Resource Manager.

    Dodaj tę właściwość za**virtualMachineProfile**, jako część hello zasobów zestawu skalowania maszyn wirtualnych:

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a>Czy mogę określić toouse pary kluczy SSH do uwierzytelniania SSH o skali maszyny wirtualnej systemu Linux ustawiony na podstawie szablonu usługi Resource Manager?  

Tak. Witaj interfejsu API REST dla **osProfile** jest podobne toohello standardowa maszyna wirtualna interfejsu API REST. 

Obejmują **osProfile** w szablonie:

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
Ten blok JSON jest używany w [hello 101-vm-sshkey GitHub szybki start szablonu](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).
 
Witaj profilu systemu operacyjnego jest również używana w [grelayhost.json hello GitHub szybki start szablonu](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).

Aby uzyskać więcej informacji, zobacz [Tworzenie lub aktualizacja zestawu skalowania maszyn wirtualnych](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).
  

### <a name="how-do-i-remove-deprecated-certificates"></a>Jak usunąć przestarzałe certyfikatów? 

tooremove przestarzałe certyfikaty i Usuń hello starego certyfikatu z listy certyfikatów magazynu hello. Pozostaw wszystkie certyfikaty hello mają tooremain na komputerze, na liście hello. Nie powoduje usunięcia certyfikatu hello z wszystkich maszyn wirtualnych. Ponadto nie dodaje hello certyfikatu toonew maszyn wirtualnych, które są tworzone w zestawie skalowania maszyn wirtualnych hello. 

tooremove hello certyfikatu z istniejących maszyn wirtualnych, zapis skryptu niestandardowego rozszerzenia toomanually Usuń hello certyfikaty z magazynu certyfikatów.
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a>Jak iniekcję istniejącego klucza publicznego SSH do warstwy zestawu skali hello maszyny wirtualnej w SSH podczas inicjowania obsługi Toostore hello SSH publicznego klucza wartości w usłudze Azure Key Vault, a następnie używać ich w szablonie usługi Resource Manager.

Jeśli hello maszyny wirtualne są udostępniane tylko za pomocą klucza publicznego SSH, nie potrzebujesz tooput hello kluczy publicznych w magazynie kluczy. Klucze publiczne nie są poufne.
 
Klucze publiczne SSH w postaci zwykłego tekstu można podać podczas tworzenia maszyny Wirtualnej systemu Linux:

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
Nazwa elementu linuxConfiguration | Wymagane | Typ | Opis
--- | --- | --- | --- |  ---
SSH | Nie | Collection | Określa hello konfiguracji kluczy SSH w systemie operacyjnym Linux
Ścieżka | Tak | Ciąg | Określa ścieżkę pliku Linux hello gdzie kluczy SSH hello lub certyfikat powinien być zlokalizowany
Kontenerem | Tak | Ciąg | Określa klucz publiczny SSH algorytmem Base64

Na przykład zobacz [hello 101-vm-sshkey GitHub szybki start szablonu](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a>Po uruchomieniu `Update-AzureRmVmss` po dodaniu więcej niż jeden certyfikat z hello klucza magazynu, są widoczne hello następujący komunikat:
 
>AzureRmVmss aktualizacji: Klucz tajny listy zawiera powtórzony wystąpienia /subscriptions/ < identyfikator Moje subskrypcji > / resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, który jest niedozwolone.
 
Może się to zdarzyć, Jeśli spróbujesz toore — Dodaj hello sam magazynu zamiast używania nowego certyfikatu w magazynie dla hello istniejący źródłowy magazyn. Witaj `Add-AzureRmVmssSecret` polecenie nie działa poprawnie, w przypadku dodawania dodatkowych kluczy tajnych.
 
tooadd więcej kluczy tajnych ze hello tego samego magazynu kluczy, lista $vmss.properties.osProfile.secrets[0].vaultCertificates hello aktualizacji.
 
Aby hello oczekiwano strukturze wejściowej, zobacz [Tworzenie lub aktualizacja maszyny wirtualnej ustawić](https://msdn.microsoft.com/library/azure/mt589035.aspx).
 
Znajdź klucz tajny hello w obiekcie zestawu skali maszyny wirtualnej hello, który znajduje się w magazynie kluczy hello. Następnie należy dodać skojarzony z magazynem hello listy toohello odwołania (adres URL hello i nazwa magazynu tajny hello) certyfikatu.

> [!NOTE] 
> Obecnie nie można usunąć certyfikaty z maszyn wirtualnych za pomocą API zestawu skali maszyny wirtualnej hello.
>

Nowe maszyny wirtualne nie będą miały hello stary certyfikat. Maszyny wirtualne w tym hello certyfikatów, które są już wdrożone będzie jednak hello stary certyfikat.
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a>Czy można push skalowania maszyny wirtualnej toohello certyfikaty ustawić bez konieczności podawania hasła hello, gdy hello certyfikat znajduje się w magazynie tajny hello?

Nie trzeba toohard kod hasła w skryptach. Dynamiczne mogą pobierać hasła z uprawnieniami hello użycie toorun hello wdrożenie skryptu. Jeśli masz skrypt, który przenosi certyfikat z magazynu kluczy tajnych magazynu hello hello tajny magazynu `get certificate` polecenie wyświetla również hello hasło pliku PFX hello.
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a>Jak właściwości kluczy tajnych hello virtualMachineProfile.osProfile skali maszyny wirtualnej ustawić pracy? Dlaczego należy hello sourceVault wartość, gdy toospecify hello bezwzględnym identyfikatorem URI certyfikatu za pomocą właściwości certificateUrl hello? 

Odwołanie certyfikatu Windows Remote Management (WinRM) musi być obecny w hello właściwości kluczy tajnych hello profilu systemu operacyjnego. 

Celem Hello wskazujący hello źródłowy magazyn jest zasady listę kontroli dostępu (ACL) kontroli dostępu tooenforce, które istnieją w modelu usługi w chmurze Azure użytkownika. Jeśli hello źródłowy magazyn nie zostanie określona, użytkowników, którzy nie mają uprawnień dostępu lub toodeploy kluczy tajnych tooa magazynu kluczy będą mogli toothrough obliczeniowe dostawcy zasobów (CRP). Listy ACL istnieje nawet w przypadku zasobów, które nie istnieją.

Jeśli podasz nieprawidłowe źródło identyfikator magazynu, ale adres URL magazynu kluczy prawidłowy podczas sondowania operacji hello jest zgłaszany błąd.
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a>Jeśli dodać tooan kluczy tajnych istniejący zestaw skali maszyny wirtualnej, są klucze tajne hello dodane do istniejących maszyn wirtualnych, lub tylko na nowe? 

Certyfikaty są dodawane tooall maszyn wirtualnych, nawet istniejący już przetworzone wcześniej. Jeśli właściwość upgradePolicy Twojego skalowania maszyny wirtualnej jest ustawiona zbyt**ręczne**, certyfikat hello jest dodawany toohello maszyny Wirtualnej, podczas przeprowadzania ręcznej aktualizacji hello maszyny Wirtualnej.
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a>Gdzie umieścić certyfikaty dla maszyn wirtualnych systemu Linux?

toolearn toodeploy certyfikatów dla maszyn wirtualnych systemu Linux, zobacz temat [wdrażanie tooVMs certyfikaty z magazynu zarządzanego przez klienta klucza](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a>Jak dodać nowy magazyn certyfikatów tooa nowego certyfikatu obiekt?

tooadd magazyn certyfikatów tooan istniejący klucz tajny, zobacz poniższy przykład PowerShell hello. Użyj tylko jeden obiekt tajny.
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a>Co się stanie toocertificates, jeśli można odtworzyć z obrazu maszyny Wirtualnej?

Czy można odtworzyć z obrazu maszyny Wirtualnej, certyfikaty zostaną usunięte. Ponownym hello usuwa cały dysk systemu operacyjnego. 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a>Co się stanie po usunięciu certyfikatu z magazynu kluczy hello?

Jeśli klucz tajny hello zostanie usunięty z magazynu kluczy hello, a następnie uruchom `stop deallocate` dla wszystkich maszyn wirtualnych, a następnie uruchom je ponownie, wystąpi błąd. Witaj błąd występuje, ponieważ hello CRP wymaga kluczy tajnych hello tooretrieve z magazynu kluczy hello, ale nie jest. W tym scenariuszu można usunąć certyfikatów hello z modelu zestawu skali maszyny wirtualnej hello. 

Witaj CRP składnika nie jest trwały kluczy tajnych klienta. Po uruchomieniu `stop deallocate` dla wszystkich maszyn wirtualnych w zestawie skalowania maszyn wirtualnych hello, pamięć podręczna hello zostanie usunięta. W tym scenariuszu kluczy tajnych są pobierane z hello magazynu kluczy.

Ten problem nie wystąpić w trakcie skalowania, ponieważ nie istnieje w pamięci podręcznej kopię klucza tajnego hello w sieci szkieletowej usług Azure (w modelu sieci szkieletowej pojedynczej dzierżawy hello).
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a>Dlaczego ma toospecify hello dokładnej lokalizacji dla adresu URL certyfikatu hello (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), jak określono w [scenariusze zabezpieczeń klastra sieci szkieletowej usług](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?
 
Witaj dokumentacji usługi Azure Key Vault stany tego Pobierz klucz tajny interfejsu API REST powinien zwrócić hello najnowszą wersję hello klucz tajny, jeśli nie określono wersji hello powitalne.
 
Metoda | ADRES URL
--- | ---
POBIERZ | https://mykeyvault.Vault.Azure.NET/secrets/ {klucz tajny name} / {klucz tajny version}? api-version = {wersja interfejsu api}

Zastąp {*nazwa klucza tajnego*} o nazwie hello i Zastąp {*wersja klucza tajnego*} z wersją hello SECRET hello ma tooretrieve. wersję klucza tajnego Hello może zostać wyłączone. W takim przypadku jest pobierana hello bieżącej wersji.
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a>Dlaczego ma toospecify hello certyfikatu wersji, podczas korzystania z usługi Key Vault?

Celem Hello hello Key Vault wymaganie toospecify hello certyfikatu wersji jest toomake go wyczyścić użytkownika toohello certyfikat, który jest wdrożony na swoich maszynach wirtualnych.

Jeśli tworzenie maszyny Wirtualnej, a następnie zaktualizuj klucz tajny w magazynie kluczy hello hello nowy certyfikat nie jest pobrany tooyour maszyn wirtualnych. Pojawiły się maszyny wirtualne i nowych maszyn wirtualnych Uzyskaj nowy klucz tajny hello tooreference. tooavoid, są wymagane tooreference wersję klucza tajnego.

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a>Mojego zespołu współpracuje z kilka certyfikatów, które są dystrybuowane toous jako .cer kluczy publicznych. Co to jest hello zalecane podejście do wdrażania tych zestaw skali maszyny wirtualnej tooa certyfikatów?

toodeploy cer kluczy publicznych tooa zestaw skali maszyny wirtualnej, można wygenerować pliku PFX, który zawiera tylko pliki cer. toodo, użyj `X509ContentType = Pfx`. Na przykład załadować plik cer hello jako obiekt x509Certificate2 w języku C# lub programu PowerShell, a następnie wywołaj metodę hello. 

Aby uzyskać więcej informacji, zobacz [metody X509Certificate.Export (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a>Nie ma opcji toopass użytkowników w certyfikatach jako ciąg base64. Większość dostawców zasobów ma tę opcję.

przekazywanie certyfikatu jako ciąg base64 tooemulate hello najnowszej wersji adresu URL w szablonie usługi Resource Manager może wyodrębnić. Obejmują następujące właściwości JSON w szablonie usługi Resource Manager hello:

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a>Certyfikaty toowrap są dostępne w obiektów JSON w magazynów kluczy?

Zestawy skalowania maszyn wirtualnych i maszyn wirtualnych certyfikaty muszą być ujęte w obiektów JSON. 

Obsługujemy również hello typu zawartości application/x-pkcs12. Aby uzyskać instrukcje na temat używania application/x-pkcs12, zobacz [certyfikatów PFX w usłudze Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).
 
Obecnie nie obsługujemy .cer plików. pliki .cer toouse, eksportowanie ich do kontenerów pfx.



## <a name="compliance"></a>Zgodność

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a>Czy na pewno zgodnych zestawach skali maszyn wirtualnych?

Zestawy skalowania maszyny wirtualnej są alokowania warstwę interfejsu API na powitania CRP. Oba te składniki są częścią platforma obliczeniowa hello w hello Azure drzewa usługi.

Z punktu widzenia zgodności zestawy skalowania maszyny wirtualnej są integralną częścią hello platformy obliczeń platformy Azure. One udostępniać zespołu, narzędzia procesów, metodę wdrażania, opcji zabezpieczeń, just in time (JIT) kompilacji, monitorowanie, alerty i itd., CRP hello, sama. Zestawy skalowania maszyny wirtualnej są Payment Card Industry (PCI)-zgodne, ponieważ hello CRP jest częścią hello bieżące poświadczenie PCI danych zabezpieczeń Standard (DSS).

Aby uzyskać więcej informacji, zobacz [hello Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).






## <a name="extensions"></a>Rozszerzenia

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a>Jak usunąć rozszerzenia zestawu skali maszyny wirtualnej?

toodelete skalowania maszyny wirtualnej ustawić rozszerzenia, użyj hello poniższy przykład środowiska PowerShell:

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
Można znaleźć wartości extensionName hello w `$vmss`.
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a>Istnieje już zestawu skalowania maszyny wirtualnej na przykład szablon, która integruje się z pakietem Operations Management Suite?

Na przykład szablon, która integruje się z pakietem Operations Management Suite zestawu skalowania maszyn wirtualnych, zobacz drugi przykład Witaj w [wdrażanie klastra usługi sieć szkieletowa usług Azure i Włącz monitorowanie przy użyciu analizy dzienników](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a>Rozszerzenia prawdopodobnie toorun równolegle na zestawy skalowania maszyny wirtualnej. Powoduje to, że moje toofail rozszerzenie skryptu niestandardowego. Co można zrobić toofix to?

toolearn o sekwencjonowania rozszerzenia w zestawy skalowania maszyny wirtualnej, zobacz [sekwencjonowania rozszerzenia w zestawy skalowania maszyny wirtualnej platformy Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a>Sposób resetowania hasła powitania dla maszyn wirtualnych w zestawu skali maszyny wirtualnej

tooreset hello hasła dla maszyn wirtualnych w skali sieci maszyny wirtualnej zestawu, użyj rozszerzenia dostępu do maszyny Wirtualnej. 

Użyj hello poniższy przykład środowiska PowerShell:

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a>Jak dodać rozszerzenie tooall maszyn wirtualnych w zestawu skali maszyny wirtualnej?

Jeśli zasady aktualizacji ustawiono zbyt**automatyczne**, ponowne wdrożenie szablonu hello z nowymi właściwościami rozszerzenia hello aktualizacji wszystkich maszyn wirtualnych.

Jeśli zasady aktualizacji ustawiono zbyt**ręczne**, najpierw zaktualizuj rozszerzenie hello, a następnie ręcznie zaktualizuj wszystkie wystąpienia w maszyn wirtualnych.

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a>Jeśli hello rozszerzenia skojarzone z istniejącego zestawu skalowania maszyny wirtualnej zostaną zaktualizowane, czy istniejące maszyny wirtualne, których dotyczy problem? (To znaczy będzie hello maszyn wirtualnych *nie* modelu zestawu skali maszyny wirtualnej hello dopasowania?) Czy są one zignorowane? Gdy istniejącej maszyny zabliźnione usługi lub odtworzyć z obrazu, są hello skrypty, które są aktualnie skonfigurowane na zestaw skali maszyny wirtualnej hello wykonywane, lub hello skrypty, które zostały skonfigurowane stosowania hello najpierw utworzenia maszyny Wirtualnej?

Jeśli ustawione definicji rozszerzenia hello w skali maszyny wirtualnej hello zaktualizować modelu oraz zbyt ustawiono właściwość upgradePolicy hello**automatyczne**, aktualizuje hello maszyn wirtualnych. Jeśli właściwość upgradePolicy hello ustawiono zbyt**ręczne**, rozszerzenia są oznaczone jako niezgodny hello modelu. 

W przypadku istniejącej maszyny Wirtualnej zabliźnione usługi, jest widoczny jako ponowne uruchomienie komputera, a hello rozszerzenia nie są ponownie. Jeśli go zostanie odtworzone z obrazu, to tak, zastępując dysk systemu operacyjnego hello hello obrazu źródłowego. Wszelkie specjalizacji z najnowszego modelu hello, takie jak rozszerzenia, są uruchamiane.
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a>Jak dołączyć do domeny tooan usługi Azure AD zestaw skali maszyny wirtualnej?

toojoin domeny usługi Azure Active Directory (Azure AD) tooan zestaw skali maszyny wirtualnej, można określić rozszerzenia. 

toodefine rozszerzenie, należy użyć właściwości JsonADDomainExtension hello:

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a>Moje rozszerzenia zestawu skali maszyny wirtualnej jest w trakcie tooinstall coś, co wymaga ponownego uruchomienia. Na przykład "commandToExecute": "powershell.exe - ExecutionPolicy Unrestricted Install-WindowsFeature — nazwa FS-Resource-Manager-IncludeManagementTools"

Jeśli rozszerzenia zestawu skali maszyny wirtualnej jest w trakcie tooinstall coś, co wymaga ponownego uruchomienia, można użyć hello Azure Automation konfiguracji żądanego stanu (DSC automatyzacji) rozszerzenia. Jeśli system operacyjny hello jest Windows Server 2012 R2, Azure ściąga w Instalatorze Windows Management Framework (WMF) 5.0 hello jest uruchamiany ponownie, a następnie kontynuuje hello konfiguracji. 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a>Jak włączyć ochrony przed złośliwym oprogramowaniem w zestawu skali maszyny wirtualnej

tooturn na ochrony przed złośliwym oprogramowaniem w skali sieci maszyny wirtualnej ustawić, użyj hello poniższy przykład środowiska PowerShell:

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a>Potrzebuję tooexecute niestandardowego skryptu, który znajduje się na koncie magazynu prywatnych. Witaj, skrypt zostanie uruchomiony pomyślnie, hello magazynu jest publiczny, ale podczas toouse dostępu sygnatury dostępu Współdzielonego, działanie nie powiodło się. Ten komunikat jest wyświetlany: "Brak parametrów obowiązkowych współużytkowanego podpisu dostępu". Łącze + SAS działa prawidłowo z przeglądarki sieci lokalnej.

tooexecute niestandardowego skryptu, który znajduje się na koncie magazynu prywatne, określić ustawienia chronionego klucz konta magazynu hello i nazwę. Aby uzyskać więcej informacji, zobacz [niestandardowe rozszerzenie skryptu systemu Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).







## <a name="networking"></a>Sieć
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a>Jest to tooassign można ustawić skali tooa grupy zabezpieczeń sieci (NSG), dzięki czemu będą stosować tooall hello kart sieciowych maszyny Wirtualnej w zestawie hello?

Tak. Grupa zabezpieczeń sieci można stosować bezpośrednio zestawu skalowania tooa, umieszczając odwołanie do sekcji Networkinterfaceconfiguration hello hello profilu sieciowego. Przykład:

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a>W jaki sposób wymiany wirtualnych adresów IP dla zestawach skali maszyn wirtualnych w hello sam subskrypcji i tego samego regionu?

Jeśli masz dwie wirtualne zestawach skali maszyn z przodu końców modułu równoważenia obciążenia Azure i są w hello tej samej subskrypcji i regionu, można cofnąć hello publicznych adresów IP z każdej z nich i przypisz toohello innych. Zobacz [wymiany wirtualnych adresów IP: zielony niebieski wdrożenia usługi Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) np. Opóźnienie to oznaczać, chociaż jako hello zasoby są alokację przydzielone na poziomie sieci hello. Opcja szybsza jest toouse bramy aplikacji Azure z dwóch pul zaplecza i reguły routingu. Alternatywnie można udostępniać aplikacji z [usługi aplikacji Azure](https://azure.microsoft.com/en-us/services/app-service/) który zapewnia obsługę szybkie przełączanie między miejscami tymczasową i produkcyjną.
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a>Jak określić zakres prywatny toouse adresy IP, statycznych alokacji prywatnego adresu IP?

Adresy IP są wybierane w podsieci, który określisz. 

Metoda alokacji Hello adresów IP zestawu skali maszyny wirtualnej jest zawsze "dynamiczny", ale nie oznacza to, że można zmienić tych adresów IP. W takim przypadku "dynamiczny" tylko oznacza nieokreślenia hello adresu IP w żądaniu PUT. Określ hello statycznych skonfigurowane przy użyciu hello podsieci. 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a>Jak wdrożyć maszynę wirtualną skali zestaw tooan istniejącej sieci wirtualnej platformy Azure? 

toodeploy skalowania maszyny wirtualnej tooan istniejącej sieci wirtualnej platformy Azure, zobacz [wdrażania maszyny wirtualnej skali zestaw tooan istniejącej sieci wirtualnej](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet). 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a>Jak dodać adres IP hello hello pierwsza maszyna wirtualna w skali maszyny wirtualnej ustawiony toohello wynik szablonu?

adres IP hello tooadd hello pierwszej maszyny Wirtualnej w maszynie wirtualnej skali zestaw toohello danych wyjściowych szablonu, zobacz [ARM: Pobierz VMSS prywatnych adresów IP](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a>Przyspieszony sieciowych można używać zestawów skalowania?

Tak. toouse przyspieszony sieci, ustawienia enableAcceleratedNetworking tootrue Twojego skali zestawu elementów Networkinterfaceconfiguration. Na przykład
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a>Jak można skonfigurować hello serwery DNS używane przez zestaw skali

toocreate zestawu skalowania maszyny Wirtualnej z niestandardowej konfiguracji DNS, dodać sekcji Networkinterfaceconfiguration zestawu skalowania toohello dnsSettings JSON pakietów. Przykład:
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a>Jak można skonfigurować skali tooassign zestaw publiczny tooeach adres IP maszyny Wirtualnej?

toocreate zestawu skalowania maszyny Wirtualnej, która przypisuje publicznego tooeach adres IP maszyny Wirtualnej, upewnij się, że wersja hello interfejsu API hello Microsoft.Compute/virtualMAchineScaleSets zasobów jest 2017-03-30 i Dodaj _publicipaddressconfiguration_ pakietów JSON elementy Ipconfiguration sekcji zestawu skalowania toohello. Przykład:

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a>Z wielu bram aplikacji można skonfigurować toowork zestaw skalowania?

Tak. Możesz dodać hello identyfikator zasobu w dla wielu toohello pule adresów zaplecza bramy aplikacji _applicationGatewayBackendAddressPools_ liście hello _Ipconfiguration_ sekcji zestawu skali profil sieci.

## <a name="scale"></a>Skalowanie

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a>W przypadku jakich może utworzyć skali maszyny wirtualnej ustawić z mniej niż dwóch maszyn wirtualnych?

Jedną z przyczyn toocreate zestawu skalowania maszyn wirtualnych z mniej niż dwóch maszyn wirtualnych zostałaby użyta właściwości elastycznej hello toouse skali maszyny wirtualnej. Na przykład można wdrożyć zestaw skali maszyny wirtualnej o zero toodefine maszyn wirtualnych infrastruktury bez płatności koszty maszyny Wirtualnej. Następnie gdy wszystko jest gotowe toodeploy maszyn wirtualnych, Zwiększ hello "pojemność" liczba wystąpień produkcji toohello zestaw hello maszyny wirtualnej skali.

Kolejny powód, które można tworzyć skali maszyny wirtualnej ustawić z mniej niż dwóch maszyn wirtualnych jest, jeśli jesteś danego mniej dostępności niż przy użyciu zestawu z maszynami wirtualnymi odrębny dostępności. Zestawy skalowania maszyny wirtualnej nadaj toowork sposób z jednostkami niesortowalne obliczeniowe, które są zamienne. Ta jednolitość jest główną różnicą dla zestawy skalowania maszyny wirtualnej i zestawów dostępności. Wiele obciążeń bezstanowych nie Śledź pojedyncze jednostki. Spadnie hello obciążenie, można dół Jednostka obliczeniowa tooone i następnie skalowanie w górę toomany podczas zwiększa obciążenie hello.

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a>Jak zmienić hello liczbę maszyn wirtualnych w zestawie skalowania maszyn wirtualnych?

toochange hello liczbę maszyn wirtualnych w zestawie skalowania maszyn wirtualnych, zobacz [zmienić hello liczba wystąpień zestawu skali maszyny wirtualnej](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a>Jak określić niestandardowe alerty po osiągnięciu progów niektórych?

Masz pewną swobodę określania w sposób obsługi alertów dla określonej wartości progowe. Na przykład można zdefiniować niestandardowych elementów webhook. Poniższy przykład elementu webhook Hello jest z szablonem usługi Resource Manager:

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

W tym przykładzie alert przechodzi tooPagerduty.com po osiągnięciu progu.



## <a name="patching-and-operations"></a>Operacje i stosowanie poprawek

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a>Jak utworzyć skali w istniejącej grupie zasobów?

Tworzenie zestawów skali w istniejący zasób grupy nie jest jeszcze możliwe z hello portalu Azure, ale można określić istniejącą grupę zasobów, podczas wdrażania skali ustawiony na podstawie szablonu usługi Azure Resource Manager. Można również określić istniejącą grupę zasobów podczas tworzenia skali ustawić za pomocą programu Azure PowerShell lub interfejsu wiersza polecenia.

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a>Grupa zasobów tooanother zestawu skali możemy przenieść?

Tak, można przenosić skalę zestawu zasobów tooa nowej subskrypcji lub grupy zasobów.

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a>Jak zaktualizować tooI tooa nowy obraz zestawu Moje skalowania maszyn wirtualnych? Jak zarządzać stosowanie poprawek

Zobacz tooupdate Twojego skalowania maszyny wirtualnej ustawić nowy obraz tooa i stosowanie poprawek toomanage, [Uaktualnij zestaw skali maszyny wirtualnej](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a>Tooreset operacja odtworzenia z obrazu hello Maszynę wirtualną można używać bez zmieniania hello obrazu? (Czyli chcę Resetowanie ustawień toofactory maszyny Wirtualnej zamiast tooa nowy obraz.)

Tak, można użyć tooreset operacja odtworzenia z obrazu hello maszyny Wirtualnej bez zmieniania hello obrazu. Jednak jeśli zestawu skalowania maszyn wirtualnych, sieci odwołuje się do obrazu platformy z `version = latest`, maszyny Wirtualnej można aktualizować tooa nowszego systemu operacyjnego obrazu podczas wywoływania `reimage`.

Aby uzyskać więcej informacji, zobacz [Zarządzanie wszystkich maszyn wirtualnych w zestawie skalowania maszyn wirtualnych](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).



## <a name="troubleshooting"></a>Rozwiązywanie problemów

### <a name="how-do-i-turn-on-boot-diagnostics"></a>Jak włączyć diagnostyki rozruchu

tooturn na diagnostyki rozruchu, najpierw utwórz konto magazynu. Następnie, umieść ten blok JSON do zestawu skalowania maszyny wirtualnej **virtualMachineProfile**i zaktualizuj zestaw skali maszyny wirtualnej hello:

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

Podczas tworzenia nowej maszyny Wirtualnej hello InstanceView właściwość hello wirtualna Wyświetla szczegóły hello hello zrzut ekranu i tak dalej. Oto przykład:
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a>Właściwości maszyny wirtualnej

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a>Jak uzyskać informacje dotyczące właściwości dla każdej maszyny Wirtualnej bez wykonywania wywołań wielu? Na przykład jak może uzyskać hello domeny błędów dla każdego hello 100 maszyn wirtualnych w zestawu skali maszyny wirtualnej?

informacje dotyczące właściwości tooget dla każdej maszyny Wirtualnej bez wykonywania wielu wywołań, należy wywołać `ListVMInstanceViews` za pomocą interfejsu API REST `GET` na powitania następującego identyfikatora URI zasobu:

/Subscriptions/ < IDENTYFIKATOR_SUBSKRYPCJI > /resourceGroups/ < resource_group_name > /providers/Microsoft.Compute/virtualMachineScaleSets/ < scaleset_name > / virtualMachines? $rozwiń = instanceView & $select = instanceView

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a>Można przekazywać argumenty inne rozszerzenie toodifferent maszyn wirtualnych w zestawie skalowania maszyn wirtualnych?

Nie, nie można przekazywać argumenty inne rozszerzenie toodifferent maszyn wirtualnych w zestawie skalowania maszyn wirtualnych. Jednak rozszerzenia może działać przy hello unikatowy właściwości hello są uruchamiane na przykład na powitania nazwa komputera maszyny Wirtualnej. Rozszerzenia również mogą wysyłać zapytania metadanych wystąpienia na http://169.254.169.254 tooget więcej informacji na temat hello maszyny Wirtualnej.

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a>Dlaczego są luki pomiędzy Moje nazw maszyn maszyny Wirtualnej zestawu skali maszyny wirtualnej i identyfikatory maszyny Wirtualnej Na przykład: 0, 1, 3...

Brak przerw między nazw maszyn maszyny Wirtualnej zestawu skali maszyny wirtualnej i identyfikatory maszyny Wirtualnej ponieważ zestawu skalowania maszyn wirtualnych, sieci **nadmiernej aprowizacji** właściwość jest ustawiona wartość domyślna toohello **true**. Jeśli nadmiarowe Inicjowanie obsługi administracyjnej jest ustawiona zbyt**true**, VMs więcej niż żądana są tworzone. Dodatkowe maszyny wirtualne są usuwane. W takim przypadku uzyskania wdrożenia większą niezawodność, ale na powitania koszt ciągłe nazewnictwa i ciągłe translatora adresów sieciowych (NAT) reguły. 

Tę właściwość można ustawić za**false**. Dla zestawów skalowania małych maszyny wirtualnej to nie znacząco wpłynąć na niezawodność wdrożenia.

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a>Jaka jest różnica hello usuwania maszyny Wirtualnej w zestawie skalowania maszyn wirtualnych i dealokowanie hello maszyny Wirtualnej? Po jednym za pośrednictwem hello innych wybrać?

Witaj podstawowa różnica między usuwania maszyny Wirtualnej w zestawie skalowania maszyn wirtualnych i dealokowanie hello maszyny Wirtualnej jest to, że `deallocate` nie powoduje usunięcia hello wirtualnych dysków twardych (VHD). Są skojarzone z uruchomioną kosztów magazynowania `stop deallocate`. Może używać co najmniej hello innych jednego hello z następujących powodów:

- Ma toostop płatności kosztów obliczeń, ale ma stan dysku hello tookeep hello maszyn wirtualnych.
- Szybciej, niż można skalować w poziomie zestaw skali maszyny wirtualnej ma toostart zestaw maszyn wirtualnych.
  - Scenariusz pokrewne toothis zostały utworzone własnego aparatu skalowania automatycznego i chcesz szybsze skali end-to-end.
- Masz zestaw skali maszyny wirtualnej, która nierównomiernie jest dystrybuowana do domen błędów lub domen aktualizacji. Może to być, ponieważ selektywnie usunąć maszyn wirtualnych lub maszyn wirtualnych zostały usunięte po nadmiarowe Inicjowanie obsługi administracyjnej. Uruchomiona `stop deallocate` następuje `start` na maszynie wirtualnej hello równomiernie zestaw skalowania rozdziela hello maszyn wirtualnych w domenach awarii lub domen aktualizacji.

