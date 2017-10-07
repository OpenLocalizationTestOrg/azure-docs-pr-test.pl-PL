---
title: "aaaCreate usługi sieć szkieletowa klastra na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate systemu Windows lub Linux Service Fabric klastra na platformie Azure przy użyciu programu PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a>Tworzenie bezpiecznej klastra na platformie Azure przy użyciu programu PowerShell
Ten samouczek pokazuje, jak toocreate usługi sieć szkieletowa klastra (z systemem Windows lub Linux) w systemie Azure. Po zakończeniu, masz klastra z systemem w chmurze hello, którą można wdrożyć aplikacji.

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie bezpiecznej klastra sieci szkieletowej usług na platformie Azure przy użyciu programu PowerShell
> * Zabezpieczanie klastra hello za pomocą certyfikatu X.509
> * Połącz toohello klastra przy użyciu programu PowerShell
> * Usuwanie klastra

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka:
- Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- Zainstaluj hello [modułu zestawu SDK usług sieci szkieletowej i programu PowerShell](service-fabric-get-started.md)
- Zainstaluj hello [programu Azure Powershell w wersji modułu 4.1 lub nowszej](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)

Witaj procedury tworzy Podgląd (jednej maszyny wirtualnej) jednowęzłowy klaster sieci szkieletowej usług. klaster Hello jest zabezpieczony przez certyfikatu z podpisem własnym, który pobiera utworzony wraz hello klastra, a następnie są umieszczane w magazynie kluczy. Nie może zostać przeskalowana jednowęzłowych poza jedną maszynę wirtualną i klastrów w wersji zapoznawczej nie może być toonewer uaktualnionej wersji.

toocalculate kosztów ponoszonych przez uruchomienie klastra sieci szkieletowej usług w hello Azure użyj [Kalkulator cen platformy Azure](https://azure.microsoft.com/pricing/calculator/).
Aby uzyskać więcej informacji na temat tworzenia klastrów sieci szkieletowej usług, zobacz [tworzenia klastra usługi sieć szkieletowa usług za pomocą usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).

## <a name="create-hello-cluster-using-azure-powershell"></a>Tworzenie klastra hello przy użyciu programu Azure PowerShell
1. Pobierz kopię lokalną hello szablonu usługi Azure Resource Manager i pliku parametrów hello z hello [szablon Menedżera zasobów Azure dla platformy Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) repozytorium GitHub.  *azuredeploy.JSON* jest hello szablonu usługi Azure Resource Manager, który definiuje klastra sieci szkieletowej usług. *azuredeploy.parameters.JSON* pliku parametrów dla użytkowników jest wdrożenie klastra hello toocustomize.

2. Dostosowywanie hello następujące parametry w hello *azuredeploy.parameters.json* pliku parametrów:

   | Parametr       | Opis | Sugerowana wartość |
   | --------------- | ----------- | --------------- |
   | clusterLocation | Witaj regionu Azure toowhich toodeploy hello klastra. | *na przykład westeurope, eastasia, eastus* |
   | clusterName     | Nazwa klastra hello ma toocreate. | *na przykład komputer1 sfpreviewcluster* |
   | adminUserName   | Hello konto administratora lokalnego na maszynach wirtualnych hello klastra. | *Wszelkie prawidłowej nazwy użytkownika systemu Windows Server* |
   | adminPassword   | Hasło konta administratora lokalnego hello na powitania klastrowanie maszyn wirtualnych. | *Wszystkie prawidłowe hasło systemu Windows Server* |
   | clusterCodeVersion | Witaj toorun wersji platformy Service Fabric. (255.255.X.255 są wersji zapoznawczych). | **255.255.5718.255** |
   | vmInstanceCount | Witaj liczbę maszyn wirtualnych w klastrze (może być 1 lub 3-99). | **1** | *W przypadku klastra w wersji zapoznawczej określić tylko jednej maszyny wirtualnej* |

3. Otwórz konsolę programu PowerShell, tooAzure logowania, a następnie wybierz subskrypcję hello, który ma toodeploy hello klastra w:

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. Utwórz i szyfrowania hasła dla hello toobe certyfikat używany przez sieć szkieletowa usług.

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. Tworzenie klastra hello i jego certyfikat, uruchamiając następujące polecenie hello:

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   >Witaj `-CertificateSubjectName` parametru powinno odpowiadać parametr NazwaKlastra hello określony w pliku parametrów hello, jak również jako hello toohello domeny powiązane region platformy Azure została wybrana opcja, takich jak: `clustername.eastus.cloudapp.azure.com`.

Po zakończeniu konfiguracji hello generuje informacje o klastrze hello utworzona na platformie Azure. Kopiuje hello klastra certyfikatu toohello - CertificateOutputFolder katalogu na powitania ścieżka określona dla tego parametru. Należy to tooaccess certyfikat kondycji hello Service Fabric Explorer i Widok klastra.

Zanotuj adres URL klastra, który może być podobne toohello hello następującego adresu URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a>Dostęp do Eksploratora usługi sieć szkieletowa & modyfikowanie hello certyfikatu ##

1. Kliknij dwukrotnie hello certyfikatu tooopen hello Kreatora importu certyfikatów.

2. Użyj ustawień domyślnych, ale upewnij się, że hello toocheck **Oznacz ten klucz jako eksportowalny.** pole wyboru w hello **ochrony klucza prywatnego** kroku. Program Visual Studio musi tooexport hello certyfikatu podczas konfigurowania uwierzytelniania klastra sieci szkieletowej tooService rejestru kontenera platformy Azure w dalszej części tego samouczka.

3. Teraz możesz otworzyć Eksploratora usługi sieć szkieletowa w przeglądarce. toodo tak, przejdź toohello **ManagementEndpoint** adres URL dla klastra przy użyciu przeglądarki sieci web i hello wybierz certyfikat, który został zapisany na komputerze.

>[!NOTE]
>Podczas otwierania Service Fabric Explorer, zobacz błąd certyfikatu, ponieważ używasz certyfikatu z podpisem własnym. W programie Edge, masz tooclick *szczegóły* , a następnie hello *przejdź na stronę sieci Web toohello* łącza. W przeglądarce Chrome, masz tooclick *zaawansowane* , a następnie hello *kontynuować* łącza.

>[!NOTE]
>W przypadku niepowodzenia tworzenia klastra hello zawsze można ponownie uruchomić polecenie hello aktualizacji zasobów hello już wdrożone. Jeśli certyfikat został utworzony jako część wdrożenia hello nie powiodło się, zostanie wygenerowany nowy. Tworzenie klastra tootroubleshoot, zobacz [tworzenia klastra usługi sieć szkieletowa usług za pomocą usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).

## <a name="connect-toohello-secure-cluster"></a>Połącz toohello bezpiecznego klastra
Połącz toohello klastra przy użyciu modułu PowerShell sieci szkieletowej usług hello z hello zestawu SDK usług sieci szkieletowej.  Najpierw zainstaluj hello certyfikatu do magazynu osobistego (Mój) hello hello bieżącego użytkownika na komputerze.  Uruchom następujące polecenia programu PowerShell hello:

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

Wszystko jest teraz gotowy tooconnect tooyour bezpiecznego klastra.

Witaj **sieci szkieletowej usług** modułu programu PowerShell zawiera wiele poleceń cmdlet do zarządzania klastrami, aplikacji i usług sieci szkieletowej usług.  Użyj hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) polecenia cmdlet tooconnect toohello bezpiecznego klastra. Witaj odcisk palca certyfikatu i szczegóły punktu końcowego połączenia można znaleźć w danych wyjściowych hello z poprzedniego kroku.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Sprawdź, czy nawiązano połączenie i hello klastra jest w dobrej kondycji, przy użyciu hello [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) polecenia cmdlet.

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Klaster składa się z innych zasobów platformy Azure oprócz zasobu klastra toohello samej siebie. Hello najprostszy sposób toodelete hello klaster i wszystkie zużywanych zasobach hello jest grupa zasobów hello toodelete.

Zaloguj się za tooAzure i wybierz hello identyfikator subskrypcji, z którym ma zostać tooremove hello klastra.  Identyfikator subskrypcji można znaleźć po zalogowaniu się toohello [portalu Azure](http://portal.azure.com). Usuń grupę zasobów hello i wszystkich zasobów klastra hello przy użyciu hello [polecenia cmdlet Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a>Następne kroki
W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie klastra sieci szkieletowej usług na platformie Azure
> * Zabezpieczanie klastra hello za pomocą certyfikatu X.509
> * Połącz toohello klastra przy użyciu programu PowerShell
> * Usuwanie klastra

Następnie poprawić toohello po toolearn samouczek jak toodeploy istniejącej aplikacji.
> [!div class="nextstepaction"]
> [Wdrażanie istniejącą aplikację .NET z rozwiązania Docker Compose](service-fabric-host-app-in-a-container.md)
