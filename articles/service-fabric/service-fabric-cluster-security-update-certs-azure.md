---
title: "Certyfikaty aaaManage klastra usługi sieć szkieletowa usług Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooadd nowych certyfikatów, certyfikat przerzucania i usuwanie certyfikatów tooor z klastra usługi sieć szkieletowa usług."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a>Dodaj lub Usuń certyfikaty dla klastra usługi sieć szkieletowa na platformie Azure
Zalecane jest, zapoznaj się z używaniu certyfikatów X.509 w sieci szkieletowej usług, a następnie należy zapoznać się z hello [klastra scenariusze zabezpieczeń](service-fabric-cluster-security.md). Trzeba zrozumieć, jakie certyfikat klastra jest i do czego służy, przed przejściem dalej.

Usługa sieci szkieletowej pozwala określić dwa klastra certyfikatów, podstawowego i pomocniczego, podczas konfigurowania certyfikatu zabezpieczeń podczas tworzenia klastra, dodanie tooclient certyfikatów. Odwołuje się zbyt[tworzenia klastra platformy azure za pośrednictwem portalu](service-fabric-cluster-creation-via-portal.md) lub [tworzenia klastra platformy azure za pomocą usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) dla informacji o konfiguracji na czas utworzenia. Jeśli określisz tylko jeden certyfikat klastra na czas utworzenia, następnie używany jako podstawowy certyfikat hello. Po utworzeniu klastra można dodać nowego certyfikatu jako dodatkowej.

> [!NOTE]
> Bezpieczne klastra należy zawsze certyfikatu co najmniej jeden prawidłowy (nie odwołane i niewygasły) klastra (podstawowe lub pomocnicze) wdrożony (Jeśli nie, hello klaster przestanie działać). 90 dni, zanim wszystkie prawidłowe certyfikaty osiągną wygaśnięcia, generuje hello systemu śledzenia ostrzeżenie, a także zdarzenie kondycji ostrzeżenia w węźle hello. Jest obecnie Brak poczty e-mail ani innych powiadomień, które wysyła sieci szkieletowej usług w tym temacie. 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a>Dodawanie certyfikatu dodatkowej klastra przy użyciu portalu hello

Nie można dodać certyfikatu dodatkowej klastra za pośrednictwem hello portalu Azure. Masz toouse Azure powershell do tego. proces Hello jest opisane w dalszej części tego dokumentu.

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a>Wymiana certyfikatów klastra hello przy użyciu portalu hello

Po pomyślnie wdrożeniu certyfikatu klastra pomocniczego, jeśli chcesz tooswap hello podstawowych i pomocniczych, następnie przejdź toohello blok zabezpieczeń i wybierz opcję "Zamiany z podstawowej" hello z hello kontekstu menu tooswap hello dodatkowej certyfikatu z Witaj podstawowego certyfikatu.

![Wymiany certyfikatów][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a>Usuń certyfikat klastra za pomocą portalu hello

Bezpieczne klastra należy zawsze co najmniej jeden prawidłowy (nie odwołane i niewygasły) certyfikat (podstawowe lub pomocnicze) wdrożone w przeciwnym razie hello klaster przestanie działać.

tooremove dodatkowego certyfikatu z użycia zabezpieczeń klastra, Nawiguj toohello zabezpieczeń bloku i wybierz hello "Delete" opcji z menu kontekstowego hello na powitania dodatkowego certyfikatu.

Jeśli tooremove hello certyfikatu, który jest oznaczony jako podstawowy, a następnie konieczne będzie tooswap zamierzeniu go przy użyciu hello dodatkowej najpierw, a następnie usuń hello dodatkowej po ukończeniu uaktualniania hello.

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a>Dodania dodatkowego certyfikatu przy użyciu programu Powershell Menedżera zasobów

Tych krokach przyjęto założenie, zapoznali się z działania Menedżera zasobów i zostaną wdrożone co najmniej jeden klaster sieci szkieletowej usług za pomocą szablonu usługi Resource Manager i szablon hello użytą tooset zapasowej klastra hello pod ręką. Zakłada się również, że masz doświadczenia, za pomocą formatu JSON.

> [!NOTE]
> Jeśli szukasz przykładowy szablon i parametrów, których można używać toofollow wzdłuż lub jako punkt początkowy, następnie pobierz go z tego [repozytorium git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample). 
> 
> 

### <a name="edit-your-resource-manager-template"></a>Edytuj szablon Menedżera zasobów

W celu ułatwienia następujące wzdłuż próbki 5-VM-1-elementów NodeType-Secure_Step2.JSON zawiera wszystkie zmiany hello wprowadzamy. przykład Witaj jest dostępny w [repozytorium git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).

**Upewnij się, że toofollow wszystkie kroki hello**

**Krok 1:** Otwórz szablon usługi Resource Manager hello używane toodeploy należy umieścić w klastrze. (Jeśli przykładowe hello zostały pobrane z hello powyżej repozytorium, następnie użyć toodeploy 5-VM-1-elementów NodeType-Secure_Step1.JSON bezpiecznego klastra i następnie otwarcia tego szablonu).

**Krok 2:** Dodaj **dwa nowe parametry** "secCertificateThumbprint" i "secCertificateUrlValue" typu "string" toohello parametru części szablonu. Można skopiować hello następującego fragmentu kodu i dodaj go toohello szablonu. W zależności od źródła hello szablonu może już tych zdefiniowana, jeśli tak przenosić toohello następnego kroku. 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

**Krok 3:** wprowadzanie zmian toohello **Microsoft.ServiceFabric/clusters** zasobu, zlokalizować definicji zasobu "Microsoft.ServiceFabric/clusters" hello w szablonie. We właściwościach tej definicji, można znaleźć "Certyfikatu" JSON tagu, który powinien wyglądać jak powitania po fragment kodu JSON:

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Dodaj nowy znacznik "thumbprintSecondary" i nadaj mu wartość "[parameters('secCertificateThumbprint')]".  

Tak, teraz hello definicji zasobu powinna wyglądać hello następujące (w zależności od źródła hello szablonu, może nie być dokładnie takie same jak poniższy fragment hello). 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Jeśli chcesz zbyt**przerzucania hello cert**, następnie określ hello nowego certyfikatu jako podstawowego i przenoszenie hello podstawowy bieżącego pomocniczym. Powoduje to hello przerzucania bieżącego podstawowego certyfikatu toohello nowy certyfikat w jednym kroku wdrożenia.

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


**Krok 4:** wprowadzanie zmian zbyt**wszystkie** hello **Microsoft.Compute/virtualMachineScaleSets** definicji zasobów — zlokalizuj hello Microsoft.Compute/virtualMachineScaleSets zasobów Definicja. Przewiń toohello "publisher": "Microsoft.Azure.ServiceFabric", w obszarze "virtualMachineProfile".

W ustawieniach hello usługi sieć szkieletowa wydawcy powinna zostać wyświetlona podobny do następującego.

![Json_Pub_Setting1][Json_Pub_Setting1]

Dodaj hello nowego certyfikatu wpisów tooit

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

właściwości Hello powinna wyglądać tak jak to

![Json_Pub_Setting2][Json_Pub_Setting2]

Jeśli chcesz zbyt**przerzucania hello cert**, następnie określ hello nowego certyfikatu jako podstawowego i przenoszenie hello podstawowy bieżącego pomocniczym. Powoduje to hello przerzucania bieżącego certyfikatu toohello nowy certyfikat w jednym kroku wdrożenia. 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
właściwości Hello powinna wyglądać tak jak to

![Json_Pub_Setting3][Json_Pub_Setting3]


**Krok 5:** zmiany zbyt**wszystkie** hello **Microsoft.Compute/virtualMachineScaleSets** definicji zasobów — Znajdź hello Microsoft.Compute/virtualMachineScaleSets zasobów Definicja. Przewiń toohello "vaultCertificates":, w obszarze "OSProfile". powinien on wyglądać następująco.


![Json_Pub_Setting4][Json_Pub_Setting4]

Dodaj hello secCertificateUrlValue tooit. Użyj następującego fragmentu hello:

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
Teraz hello wynikowa Json powinien wyglądać następująco.
![Json_Pub_Setting5][Json_Pub_Setting5]


> [!NOTE]
> Upewnij się, że zostało wpisane kroki 4 i 5, dla wszystkich definicji zasobu Nodetypes/Microsoft.Compute/virtualMachineScaleSets hello szablonu. Jeśli pominiesz jeden z nich hello certyfikatu nie zostaną zainstalowane na tym VMSS i może spowodować nieprzewidywalne skutki w klastrze, w tym klastrze hello przechodzi w dół (Jeśli na końcu nie prawidłowe certyfikaty, można użyć w tym klastrze hello zabezpieczeń. Dlatego Sprawdź, przed kontynuacją.
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a>Edytuj szablon pliku tooreflect hello nowe parametry dodanych powyżej
Jeśli używasz hello próbki z hello [repozytorium git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow wraz, można uruchomić zmiany toomake w hello próbki 5-VM — 1-elementów NodeType — Secure.paramters_Step2.JSON 

Edytowanie parametru szablonu usługi Resource Manager pliku, dodaj dwa nowe parametry hello secCertificateThumbprint i secCertificateUrlValue. 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a>Wdrażanie hello tooAzure szablonu

- Użytkownik jest teraz gotowy toodeploy tooAzure Twojego szablonu. Otwórz wiersz polecenia w wersji 1 + Azure PS.
- Zaloguj się za tooyour konto platformy Azure i wybierz hello określonej subskrypcji platformy azure. Jest to ważny krok do pracowników, mających toomore dostępu niż jedną subskrypcją platformy azure.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

Test toodeploying poprzedniego szablonu hello go. Użyj hello klastra jest obecnie wdrożona do tej samej grupy zasobów.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

Wdrażanie grupy zasobów tooyour szablonu hello. Użyj hello klastra jest obecnie wdrożona do tej samej grupy zasobów. Uruchom polecenie New-AzureRmResourceGroupDeployment hello. Nie trzeba toospecify hello trybu, ponieważ hello wartość domyślna to **przyrostowe**.

> [!NOTE]
> Po ustawieniu trybu tooComplete przypadkowo można usunąć zasoby, które nie znajdują się w szablonie. Dlatego nie jest używana w tym scenariuszu.
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

W tym miejscu jest wypełniony się przykładem hello tego samego środowiska powershell.

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

Po zakończeniu wdrażania hello połączyć tooyour klastra przy użyciu hello nowego certyfikatu i wykonywania niektórych zapytań. Jeśli jesteś toodo stanie. Następnie można usunąć starego certyfikatu hello. 

Jeśli używasz certyfikatu z podpisem własnym, nie zapomnij tooimport ich do lokalnego magazynu certyfikatów TrustedPeople.

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
Dla wygody Oto hello polecenia tooconnect tooa bezpiecznego klastra 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
Dla wygody Oto hello polecenia tooget klastra kondycji

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a>Wdrażanie klastra toohello certyfikaty aplikacji.

Możesz użyć hello same kroki zgodnie z opisem w kroki 5 powyżej certyfikatów hello toohave wdrożone z toohello keyvault węzłów. Możesz po prostu należy zdefiniować i użyć innych parametrów.


## <a name="adding-or-removing-client-certificates"></a>Dodanie lub usunięcie certyfikatów klienta

W dodatku toohello klastra certyfikatów można dodać operacji zarządzania tooperform certyfikaty klienta w klastrze usługi sieć szkieletowa.

Możesz dodać dwa rodzaje certyfikatów klienta — administratora lub w trybie tylko do odczytu. Następnie mogą być używane toocontrol dostępu toohello administratora operacji i operacje kwerend w klastrze hello. Domyślnie certyfikaty klastra hello są dodawane toohello Admin certyfikaty listy dozwolonych.

można określić dowolną liczbę certyfikatów klienta. Każdy dodanie/usunięcie powoduje klastra sieci szkieletowej usług toohello aktualizacji konfiguracji


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a>Dodawanie certyfikatów klienta — administratora lub w trybie tylko do odczytu za pomocą portalu

1. Przejdź do bloku zabezpieczeń toohello, a następnie wybierz hello "+ uwierzytelniania" przycisk u góry bloku zabezpieczeń hello.
2. W bloku "Dodaj uwierzytelniania" hello wybierz hello "Typ uwierzytelniania" - "Tylko do odczytu" lub "Admin klienta"
3. Teraz wybierz metodę autoryzacji hello. Czy powinna wyszukiwać ten certyfikat za pomocą hello nazwa podmiotu lub odcisku palca hello wskazuje tooService sieci szkieletowej. Ogólnie rzecz biorąc go nie jest dobrym rozwiązaniem toouse hello autoryzacji metodą nazwy podmiotu. 

![Dodawanie certyfikatu klienta][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a>Usunięcie certyfikatów klienta — administratora lub tylko do odczytu za pomocą hello portalu

tooremove dodatkowego certyfikatu z użycia zabezpieczeń klastra, Nawiguj toohello zabezpieczeń bloku i wybierz hello "Delete" opcji z menu kontekstowego hello na powitania określonego certyfikatu.



## <a name="next-steps"></a>Następne kroki
Przeczytaj następujące artykuły, aby uzyskać więcej informacji na temat zarządzania klastrem:

* [Proces uaktualniania klastra sieci szkieletowej usług oraz oczekiwań od użytkownika](service-fabric-cluster-upgrade.md)
* [Ustawienia dostępu opartego na rolach dla klientów](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


