---
title: "Tworzenie klastra sieci szkieletowej usług na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć klaster systemu Windows lub Linux Service Fabric na platformie Azure przy użyciu programu PowerShell."
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
ms.openlocfilehash: f62249417552b9cf840bfac3b94c27f63bd7064e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a>Tworzenie bezpiecznej klastra na platformie Azure przy użyciu programu PowerShell
W tym samouczku przedstawiono sposób tworzenia klastra usługi sieć szkieletowa (Windows lub Linux) działają na platformie Azure. Po zakończeniu, masz działającą w chmurze, które można wdrożyć aplikacji do klastra.

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie bezpiecznej klastra sieci szkieletowej usług na platformie Azure przy użyciu programu PowerShell
> * Zabezpieczanie klastra za pomocą certyfikatu X.509
> * Nawiązywanie połączenia z klastrem przy użyciu programu PowerShell
> * Usuwanie klastra

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka:
- Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- Zainstaluj [modułu zestawu SDK usług sieci szkieletowej i programu PowerShell](service-fabric-get-started.md)
- Zainstaluj [programu Azure Powershell w wersji modułu 4.1 lub nowszej](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)

Poniższa procedura tworzy Podgląd (jednej maszyny wirtualnej) jednowęzłowy klaster sieci szkieletowej usług. Klaster jest chroniony przez certyfikatu z podpisem własnym, który pobiera utworzona wraz z klastra, a następnie są umieszczane w magazynie kluczy. Nie może zostać przeskalowana jednowęzłowych poza jedną maszynę wirtualną i Podgląd klastrów nie można uaktualnić do nowszej wersji.

Aby obliczyć kosztów ponoszonych przez uruchomienie klastra sieci szkieletowej usług Azure używana [Kalkulator cen platformy Azure](https://azure.microsoft.com/pricing/calculator/).
Aby uzyskać więcej informacji na temat tworzenia klastrów sieci szkieletowej usług, zobacz [tworzenia klastra usługi sieć szkieletowa usług za pomocą usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).

## <a name="create-the-cluster-using-azure-powershell"></a>Tworzenie klastra przy użyciu programu Azure PowerShell
1. Pobierz kopię lokalną szablonu usługi Azure Resource Manager i pliku parametrów z [szablon Menedżera zasobów Azure dla platformy Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) repozytorium GitHub.  *azuredeploy.JSON* jest szablonu usługi Azure Resource Manager, który definiuje klastra sieci szkieletowej usług. *azuredeploy.parameters.JSON* jest plikiem parametry umożliwiające dostosowywanie wdrożenia klastra.

2. Następujące parametry w *azuredeploy.parameters.json* pliku parametrów:

   | Parametr       | Opis | Sugerowana wartość |
   | --------------- | ----------- | --------------- |
   | clusterLocation | Region platformy Azure, dla której chcesz wdrożyć w klastrze. | *na przykład westeurope, eastasia, eastus* |
   | clusterName     | Nazwa klastra, który chcesz utworzyć. | *na przykład komputer1 sfpreviewcluster* |
   | adminUserName   | Konto administratora lokalnego na maszynach wirtualnych w klastrze. | *Wszelkie prawidłowej nazwy użytkownika systemu Windows Server* |
   | adminPassword   | Hasło konta administratora lokalnego na maszynach wirtualnych w klastrze. | *Wszystkie prawidłowe hasło systemu Windows Server* |
   | clusterCodeVersion | Wersja usługi sieć szkieletowa usług do uruchomienia. (255.255.X.255 są wersji zapoznawczych). | **255.255.5718.255** |
   | vmInstanceCount | Liczba maszyn wirtualnych w klastrze (może być 1 lub 3-99). | **1** | *W przypadku klastra w wersji zapoznawczej określić tylko jednej maszyny wirtualnej* |

3. Otwórz konsolę programu PowerShell, logowanie do platformy Azure i wybierz subskrypcję, którą chcesz wdrożyć w klastrze:

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. Utwórz i szyfrowania hasło dla certyfikatu, który ma być używany przez sieć szkieletowa usług.

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. Tworzenie klastra i jego certyfikat, uruchamiając następujące polecenie:

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
   >`-CertificateSubjectName` Parametru powinno odpowiadać parametr clusterName określony w pliku parametrów, a także domeny powiązane region platformy Azure została wybrana opcja, takich jak: `clustername.eastus.cloudapp.azure.com`.

Po zakończeniu konfiguracji generuje informacje o klastrze utworzona na platformie Azure. Kopiuje również certyfikat klastra katalogu - CertificateOutputFolder na ścieżkę, którą określono dla tego parametru. Należy na dostęp do Eksploratora usługi sieć szkieletowa i wyświetlić informacje o kondycji klastra tego certyfikatu.

Zanotuj adres URL dla klastra, które mogą być podobne do następującego adresu URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*

## <a name="modify-the-certificate--access-service-fabric-explorer"></a>Dostęp do Eksploratora usługi sieć szkieletowa & zmienić certyfikat ##

1. Kliknij dwukrotnie certyfikat, aby otworzyć Kreatora importu certyfikatów.

2. Użyj ustawień domyślnych, ale pamiętaj sprawdzić **Oznacz ten klucz jako eksportowalny.** należy zaznaczyć pole wyboru, w **ochrony klucza prywatnego** kroku. Program Visual Studio musi wyeksportować certyfikat podczas konfigurowania rejestru kontenera Azure do uwierzytelniania klastra sieci szkieletowej usług w dalszej części tego samouczka.

3. Teraz możesz otworzyć Eksploratora usługi sieć szkieletowa w przeglądarce. Aby to zrobić, przejdź do **ManagementEndpoint** adres URL dla klastra przy użyciu przeglądarki sieci web i wybierz certyfikat, który został zapisany na komputerze.

>[!NOTE]
>Podczas otwierania Service Fabric Explorer, zobacz błąd certyfikatu, ponieważ używasz certyfikatu z podpisem własnym. W programie Edge, trzeba kliknąć *szczegóły* , a następnie *przejdź do strony sieci Web* łącza. W przeglądarce Chrome, trzeba kliknąć *zaawansowane* , a następnie *kontynuować* łącza.

>[!NOTE]
>W przypadku niepowodzenia tworzenia klastra należy zawsze uruchamiaj ponownie polecenie, które aktualizuje zasoby już wdrożone. Jeśli certyfikat został utworzony jako część wdrożenia nie powiodło się, zostanie wygenerowany nowy. Aby rozwiązać tworzenia klastra, zobacz [tworzenia klastra usługi sieć szkieletowa usług za pomocą usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).

## <a name="connect-to-the-secure-cluster"></a>Połącz się z klastrem bezpieczne
Połącz z klastrem przy użyciu modułu programu PowerShell usługi Service Fabric zainstalowany przy użyciu zestawu SDK sieci szkieletowej usług.  Najpierw zainstaluj certyfikat do magazynu osobistego (Mój) bieżącego użytkownika na komputerze.  Uruchom następujące polecenie programu PowerShell:

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

Teraz możesz przystąpić do nawiązywania połączenia z zabezpieczonym klastrem.

**Sieci szkieletowej usług** modułu programu PowerShell zawiera wiele poleceń cmdlet do zarządzania klastrami, aplikacji i usług sieci szkieletowej usług.  Użyj [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) polecenia cmdlet, aby połączyć się z klastrem bezpieczne. Szczegóły punktu końcowego połączenia i odcisk palca certyfikatu można znaleźć w danych wyjściowych z poprzedniego kroku.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Sprawdź, czy nawiązano połączenie i klastra jest w dobrej kondycji za pomocą [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) polecenia cmdlet.

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Klaster składa się z innych zasobów platformy Azure poza samym zasobem klastra. Najprostszym sposobem na usunięcie klastra i wszystkich wykorzystywanych przez niego zasobów jest usunięcie grupy zasobów.

Logowanie do platformy Azure i wybierz identyfikator subskrypcji, z którą chcesz usunąć klaster.  Identyfikator subskrypcji można znaleźć po zalogowaniu się do [portalu Azure](http://portal.azure.com). Usuń grupę zasobów i zasobów klastra przy użyciu [polecenia cmdlet Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).

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
> * Zabezpieczanie klastra za pomocą certyfikatu X.509
> * Nawiązywanie połączenia z klastrem przy użyciu programu PowerShell
> * Usuwanie klastra

Następnie przejdź do następujących samouczkiem, aby dowiedzieć się, jak wdrożyć istniejącą aplikację.
> [!div class="nextstepaction"]
> [Wdrażanie istniejącą aplikację .NET z rozwiązania Docker Compose](service-fabric-host-app-in-a-container.md)
