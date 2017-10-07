---
title: "aaaSet zapasowej klastra usługi sieć szkieletowa usług Azure | Dokumentacja firmy Microsoft"
description: "Szybki start — tworzenie klastra usługi Service Fabric z systemem Windows lub Linux na platformie Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a>Tworzenie pierwszego klastra usługi Service Fabric na platformie Azure
[Klaster usługi Service Fabric](service-fabric-deploy-anywhere.md) jest połączonym z siecią zestawem maszyn wirtualnych lub fizycznych, w którym wdraża się mikrousługi i nimi zarządza. Ta opcja szybkiego startu pomaga toocreate pięcioma węzłami klastra, systemem Windows lub Linux, za pośrednictwem hello [programu Azure PowerShell](https://msdn.microsoft.com/library/dn135248) lub [portalu Azure](http://portal.azure.com) za kilka minut.  

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).


## <a name="use-hello-azure-portal"></a>Użyj hello portalu Azure

Zaloguj się za toohello portalu Azure w [http://portal.azure.com](http://portal.azure.com).

### <a name="create-hello-cluster"></a>Tworzenie klastra hello

1. Kliknij przycisk hello **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.
2. Wybierz **obliczeniowe** z hello **nowy** bloku, a następnie wybierz **klastra sieci szkieletowej usług** z hello **obliczeniowe** bloku.
3. Wypełnianie hello sieci szkieletowej usług **podstawy** formularza. Dla **systemu operacyjnego**, wybierz pozycję hello wersji systemu Windows lub Linux ma hello toorun węzłów klastra. Hello nazwy użytkownika i hasła wprowadzonego w tym miejscu jest używane toolog toohello maszynie wirtualnej. W obszarze **Grupa zasobów** utwórz nową. Grupa zasobów to logiczny kontener, w którym są tworzone i zbiorczo zarządzane zasoby platformy Azure. Po zakończeniu kliknij przycisk **OK**.

    ![Dane wyjściowe instalacji klastra][cluster-setup-basics]

4. Wypełnianie hello **konfiguracji klastra** formularza.  Dla ustawienia **Liczba typów węzłów** wprowadź wartość „1”.

5. Wybierz **typu węzła 1 (podstawowe)** i wypełnianie hello **konfiguracji typu węzła** formularza.  Wprowadź nazwę typu węzła i ustaw hello [warstwa trwałości](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) zbyt "brązową."  Wybierz rozmiar maszyny wirtualnej.

    Typy węzłów zdefiniuj hello rozmiar maszyny Wirtualnej, liczbę maszyn wirtualnych, niestandardowe punkty końcowe, oraz inne ustawienia hello maszyny wirtualne tego typu. Każdy typ węzła zdefiniowany jest skonfigurowany jako zestaw skali oddzielnej maszynie wirtualnej, który jest zarządzanych maszyn wirtualnych i toodeploy używane jako zestaw. Każdy typ węzła może być niezależnie skalowany w górę lub w dół, może mieć różne zestawy otwartych portów i może mieć różne metryki pojemności.  Hello pierwszy lub podstawowego, typ węzła jest którym usługi sieć szkieletowa usług systemowych są obsługiwane i musi mieć co najmniej pięć maszyn wirtualnych.

    W przypadku wszystkich wdrożeń produkcyjnych [planowanie pojemności](service-fabric-cluster-capacity.md) jest ważnym krokiem.  Niemniej w ramach tego przewodnika Szybki start nie uruchamiasz aplikacji, więc wybierz rozmiar maszyny wirtualnej *Standardowa DS1_v2*.  Wybierz "Srebrna" hello [warstwa niezawodności](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) i pojemność wynoszącą 5 zestawu skalowania maszyny wirtualnej początkowej.  

    Niestandardowe punkty końcowe otwarcie portów w usłudze równoważenia obciążenia Azure hello, dzięki czemu można połączyć z aplikacji działających na powitania klastra.  Wprowadź "80, 8172" tooopen się porty 80 i 8172.

    Nie sprawdzaj hello **Skonfiguruj ustawienia zaawansowane** okno, który służy do dostosowywania końcowych zarządzania TCP/HTTP, zakresy portów aplikacji, [ograniczenia umieszczania](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), i [pojemności właściwości](service-fabric-cluster-resource-manager-metrics.md).    

    Kliknij przycisk **OK**.

6. W hello **konfiguracji klastra** formularza, ustaw **diagnostyki** za**na**.  Dla tego przewodnika Szybki Start, nie trzeba tooenter any [sieci szkieletowej ustawienie](service-fabric-cluster-fabric-settings.md) właściwości.  W **wersja platformy Fabric**, wybierz pozycję **automatyczne** tryb uaktualniania, tak aby firma Microsoft automatycznie aktualizuje hello wersja kodu sieci szkieletowej hello uruchomionego hello klastra.  Ustaw tryb hello zbyt**ręcznego** Jeśli zbyt[Wybierz obsługiwaną wersję](service-fabric-cluster-upgrade.md) tooupgrade do. 

    ![Konfiguracja typu węzła][node-type-config]

    Kliknij przycisk **OK**.

7. Wypełnianie hello **zabezpieczeń** formularza.  W ramach tego przewodnika Szybki start wybierz opcję **Niezabezpieczony**.  Jest zdecydowanie zalecane toocreate bezpiecznego klastra w przypadku obciążeń produkcyjnych, jednak ponieważ każdy anonimowo połączyć tooan niezabezpieczone klaster i wykonywać operacje zarządzania.  

    Certyfikaty są używane w sieci szkieletowej usług tooprovide uwierzytelnianie i szyfrowanie toosecure różnych aspektów klastra i jego zastosowań. Aby uzyskać więcej informacji o sposobie wykorzystania certyfikatów w usłudze Service Fabric, zobacz [Scenariusze zabezpieczeń klastra usługi Service Fabric](service-fabric-cluster-security.md).  Uwierzytelnianie użytkownika tooenable za pomocą usługi Azure Active Directory lub tooset zapasowych certyfikatów zabezpieczeń aplikacji [Tworzenie klastra z szablonem usługi Resource Manager](service-fabric-cluster-creation-via-arm.md).

    Kliknij przycisk **OK**.

8. Witaj Przejrzyj podsumowania.  Jeśli chcesz toodownload szablonem usługi Resource Manager zbudowane na podstawie ustawień hello wprowadzona, wybierz **Pobierz szablon i parametry**.  Wybierz **Utwórz** toocreate hello klastra.

    Postęp tworzenia hello w powiadomieniach hello jest widoczny. (Kliknij ikonę dzwonka"hello" w pobliżu pasek stanu hello na powitania górnym rogu ekranu). Jeśli kliknięto **tooStartboard numeru Pin** podczas tworzenia klastra hello, zobacz **wdrażanie klastra sieci szkieletowej usług** przypięty toohello **Start** tablicy.

### <a name="view-cluster-status"></a>Wyświetlanie stanu klastra
Po utworzeniu klastra można sprawdzić klastra w hello **omówienie** bloku w portalu hello. Możesz teraz przeglądać szczegóły hello klastra na pulpicie nawigacyjnym hello, w tym klastrze hello publiczny punkt końcowy i tooService łącze Eksploratora sieci szkieletowej.

![Stan klastra][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Wizualizowanie klastra hello za pomocą Eksploratora usługi sieć szkieletowa
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) to odpowiednie narzędzie do wizualizowania klastra i zarządzania aplikacjami.  Service Fabric Explorer to usługa, która działa w klastrze hello.  Dostęp za pomocą przeglądarki sieci web, klikając hello **Service Fabric Explorer** łącze klastra hello **omówienie** w portalu hello na stronie.  Można również wprowadzić adres hello bezpośrednio w przeglądarce hello: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)

pulpit nawigacyjny klastra Hello Omówienie klastra, w tym podsumowanie aplikacji i kondycji węzła. Widok węzła Hello przedstawia hello fizycznego układu hello klastra. Dla danego węzła można sprawdzić, które aplikacje mają kod wdrożony w tym węźle.

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a>Połącz toohello klastra przy użyciu programu PowerShell
Sprawdź, czy w tym klastrze hello jest uruchomiona, nawiązując połączenie za pomocą programu PowerShell.  Witaj modułu ServiceFabric programu PowerShell jest instalowany z hello [zestawu SDK usług sieci szkieletowej](service-fabric-get-started.md).  Witaj [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet ustanawia połączenie toohello klastra.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
Zobacz [klastra bezpiecznego połączenia tooa](service-fabric-connect-to-secure-cluster.md) inne przykłady łączącego tooa klastra. Po łączącego toohello klastra, użyj hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay polecenia cmdlet listy węzłów w hello klastra oraz informacje o stanie dla każdego węzła. Element **HealthState** powinien mieć wartość *OK* dla każdego węzła.

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a>Usuń hello klastra
Klastra usługi sieć szkieletowa składa się z innych zasobów platformy Azure oprócz zasobu klastra toohello samej siebie. Dlatego toocompletely Usuwanie klastra sieci szkieletowej usług należy również toodelete hello wszystkie zasoby, które składa się z. Hello najprostszy sposób toodelete hello klaster i wszystkie zużywanych zasobach hello jest grupa zasobów hello toodelete. Dla innych toodelete sposoby klaster lub toodelete zasobów hello niektóre (ale nie wszystkie) w grupie zasobów, zobacz [usunąć klaster](service-fabric-cluster-delete.md)

Usuń grupę zasobów w portalu Azure hello:
1. Przejdź toohello klastra sieci szkieletowej usług ma toodelete.
2. Kliknij przycisk hello **grupy zasobów** nazwa strony essentials hello klastra.
3. W hello **Essentials grupy zasobów** kliknij przycisk **Usuń grupę zasobów** i wykonać instrukcje hello usunięcie hello toocomplete strony tego hello grupy zasobów.
    ![Usuń grupę zasobów hello][cluster-delete]


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a>Użyj programu Azure Powershell toodeploy bezpiecznego klastra
1. Pobierz hello [programu Azure Powershell modułu w wersji 4.0 lub nowszej](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) na tym komputerze.

2. Otwórz okno programu Windows PowerShell, hello uruchom następujące polecenie. 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    Powinny zostać wyświetlone następujące dane wyjściowe podobne toohello.

    ![ps-list][ps-list]

3. TooAzure logowania i wybierz hello toowhich subskrypcji ma toocreate hello klastra

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. Hello uruchom następujące polecenie toonow tworzenia bezpiecznego klastra. Nie zapomnij toocustomize hello parametrów. 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    polecenie Hello może potrwać od 10 minut too30 minut toocomplete na końcu hello go, należy pobrać następujące dane wyjściowe podobne toohello. dane wyjściowe Hello zawiera informacje o certyfikacie hello, hello KeyVault, w którym został przekazany, i hello folder lokalny, w którym certyfikat hello jest kopiowany. 

    ![ps-out][ps-out]

5. Kopiuj dane wyjściowe całego hello i Zapisz plik tekstowy tooa jako potrzebujemy toorefer tooit. Zanotuj hello następujących informacji w danych wyjściowych hello. 

    - **CertificateSavedLocalPath** : c:\mojecertyfikaty\mojklaster20170504141137.pfx
    - **CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10
    - **ManagementEndpoint** : https://mojklaster.southcentralus.cloudapp.azure.com:19080
    - **ClientConnectionEndpointPort** : 19000

### <a name="install-hello-certificate-on-your-local-machine"></a>Zainstaluj certyfikat hello na komputerze lokalnym
  
tooconnect toohello klastra, potrzebujesz tooinstall hello certyfikatu do magazynu osobistego (Mój) hello hello bieżącego użytkownika. 

Uruchom hello następującego środowiska PowerShell

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

Wszystko jest teraz gotowy tooconnect tooyour bezpiecznego klastra.

### <a name="connect-tooa-secure-cluster"></a>Połącz tooa bezpiecznego klastra 

Uruchom powitania po klastra bezpiecznego tooa tooconnect polecenia programu PowerShell. Szczegóły certyfikatu Hello musi odpowiadać certyfikatu, który był używany tooset zapasowej hello klastra. 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


powitania po hello przedstawiono przykład ukończone parametry: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Uruchom hello następujące polecenia toocheck, że komputer jest połączony i hello klastra jest w dobrej kondycji.

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a>Publikowanie aplikacji tooyour klastra w programie Visual Studio

Teraz, gdy zdefiniowano klastra platformy Azure możesz opublikować tooit Twojej aplikacji w programie Visual Studio przez następujące hello [klastra tooan publikowania](service-fabric-publish-app-remote-cluster.md) dokumentu. 

### <a name="remove-hello-cluster"></a>Usuń hello klastra
Klaster składa się z innych zasobów platformy Azure oprócz zasobu klastra toohello samej siebie. Hello najprostszy sposób toodelete hello klaster i wszystkie zużywanych zasobach hello jest grupa zasobów hello toodelete. 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a>Następne kroki
Po skonfigurowaniu klastra projektowego wypróbować hello następujące czynności:
* [Tworzenie bezpiecznej klastra w portalu hello](service-fabric-cluster-creation-via-portal.md)
* [Tworzenie klastra na podstawie szablonu](service-fabric-cluster-creation-via-arm.md) 
* [Wdrażanie aplikacji przy użyciu programu PowerShell](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
