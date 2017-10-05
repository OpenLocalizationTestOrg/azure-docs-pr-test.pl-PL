---
title: "Konfigurowanie klastra usługi Azure Service Fabric | Microsoft Docs"
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
ms.openlocfilehash: ec59450052b377412a28f7eaf55d1f1512b55195
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a>Tworzenie pierwszego klastra usługi Service Fabric na platformie Azure
[Klaster usługi Service Fabric](service-fabric-deploy-anywhere.md) jest połączonym z siecią zestawem maszyn wirtualnych lub fizycznych, w którym wdraża się mikrousługi i nimi zarządza. Niniejszy przewodnik Szybki start pomaga w utworzeniu klastra o pięciu węzłach, z systemem Windows lub Linux, za pośrednictwem środowiska [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) lub witryny [Azure Portal](http://portal.azure.com) w ciągu kilku minut.  

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).


## <a name="use-the-azure-portal"></a>Korzystanie z witryny Azure Portal

Zaloguj się w witrynie Azure Portal pod adresem [http://portal.azure.com](http://portal.azure.com).

### <a name="create-the-cluster"></a>Tworzenie klastra

1. Kliknij przycisk **Nowy** znajdujący się w lewym górnym rogu witryny Azure Portal.
2. Wybierz pozycję **Compute** w bloku **Nowy**, a następnie wybierz opcję **Klaster usługi Service Fabric** w bloku **Compute**.
3. Uzupełnij formularz **Podstawy** usługi Service Fabric. W sekcji **System operacyjny** wybierz wersję systemu Windows lub Linux, którego chcesz używać w węzłach klastra. Nazwa użytkownika i hasło wprowadzone w tym miejscu są używane na potrzeby logowania się do maszyny wirtualnej. W obszarze **Grupa zasobów** utwórz nową. Grupa zasobów to logiczny kontener, w którym są tworzone i zbiorczo zarządzane zasoby platformy Azure. Po zakończeniu kliknij przycisk **OK**.

    ![Dane wyjściowe instalacji klastra][cluster-setup-basics]

4. Uzupełnij formularz **Konfiguracja klastra**.  Dla ustawienia **Liczba typów węzłów** wprowadź wartość „1”.

5. Wybierz pozycję **Typ węzła 1 (podstawowy)** i wypełnij formularz **Konfiguracja typu węzła**.  Wprowadź nazwę typu węzła i dla pozycji [Warstwa trwałości](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) ustaw wartość „Brązowa”.  Wybierz rozmiar maszyny wirtualnej.

    Typy węzłów definiują rozmiar maszyny wirtualnej, liczbę maszyn wirtualnych, niestandardowe punkty końcowe oraz inne ustawienia dla maszyn wirtualnych tego typu. Każdy zdefiniowany typ węzła jest konfigurowany jako oddzielny zestaw skalowania maszyn wirtualnych, który jest używany do wdrażania maszyn wirtualnych i zarządzania nimi jako zestawem. Każdy typ węzła może być niezależnie skalowany w górę lub w dół, może mieć różne zestawy otwartych portów i może mieć różne metryki pojemności.  Pierwszy lub główny typ węzła jest miejscem, w którym hostowane są usługi systemowe Service Fabric. Musi zawierać co najmniej pięć maszyn wirtualnych.

    W przypadku wszystkich wdrożeń produkcyjnych [planowanie pojemności](service-fabric-cluster-capacity.md) jest ważnym krokiem.  Niemniej w ramach tego przewodnika Szybki start nie uruchamiasz aplikacji, więc wybierz rozmiar maszyny wirtualnej *Standardowa DS1_v2*.  Wybierz wartość „Srebrna” dla [warstwy niezawodności](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) oraz ustaw początkową pojemność zestawu skalowania maszyn wirtualnych na 5.  

    Niestandardowe punkty końcowe otwierają porty w module równoważenia obciążenia platformy Azure, dzięki czemu możesz nawiązywać połączenie z aplikacjami uruchomionymi w klastrze.  Wprowadź „80, 8172”, aby otworzyć porty 80 i 8172.

    Nie zaznaczaj pola wyboru **Skonfiguruj ustawienia zaawansowane**. Opcji tej używa się do dostosowywania punktów końcowych zarządzania protokołem TCP/HTTP, zakresem portów aplikacji, [ograniczeniami dotyczącymi umieszczania](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints) oraz [właściwościami pojemności](service-fabric-cluster-resource-manager-metrics.md).    

    Kliknij przycisk **OK**.

6. W formularzu **Konfigurowanie klastra** ustaw opcję **Diagnostyka** na wartość **Wł**.  W ramach tego przewodnika Szybki start nie musisz wprowadzać żadnych właściwości [ustawień sieci szkieletowej](service-fabric-cluster-fabric-settings.md).  W pozycji **Wersja sieci szkieletowej** wybierz tryb uaktualniania **Automatyczny**, dzięki czemu firma Microsoft będzie automatycznie aktualizować wersję kodu sieci szkieletowej obsługującego klaster.  Ustaw tryb **Ręczny**, jeśli chcesz [wybrać obsługiwaną wersję](service-fabric-cluster-upgrade.md) do uaktualnienia. 

    ![Konfiguracja typu węzła][node-type-config]

    Kliknij przycisk **OK**.

7. Uzupełnij formularz **Zabezpieczenia**.  W ramach tego przewodnika Szybki start wybierz opcję **Niezabezpieczony**.  Niemniej zaleca się utworzenie zabezpieczonego klastra dla obciążeń produkcyjnych, ponieważ każda osoba może anonimowo połączyć się z niezabezpieczonym klastrem i przeprowadzić operacje związane z zarządzaniem.  

    W usłudze Service Fabric używa się certyfikatów, aby zapewniać uwierzytelnianie i szyfrowanie w celu zabezpieczania różnych aspektów klastra i jego aplikacji. Aby uzyskać więcej informacji o sposobie wykorzystania certyfikatów w usłudze Service Fabric, zobacz [Scenariusze zabezpieczeń klastra usługi Service Fabric](service-fabric-cluster-security.md).  Aby włączyć uwierzytelnianie użytkownika przy użyciu usługi Azure Active Directory lub skonfigurować certyfikaty dla zabezpieczeń aplikacji, [utwórz klaster z szablonu usługi Resource Manager](service-fabric-cluster-creation-via-arm.md).

    Kliknij przycisk **OK**.

8. Przejrzyj podsumowanie.  Jeśli chcesz pobrać szablon usługi Resource Manager utworzony na podstawie wprowadzonych ustawień, wybierz opcję **Pobierz szablon i parametry**.  Wybierz opcję **Utwórz**, aby utworzyć klaster.

    Możesz zobaczyć postępy tworzenia w powiadomieniach. (Kliknij ikonę „Dzwonka” w pobliżu paska stanu w prawym górnym rogu ekranu). Jeśli kliknięto opcję **Przypnij do tablicy startowej** podczas tworzenia klastra, zobaczysz pozycję **Wdrażanie klastra usługi Service Fabric** przypiętą do tablicy **Start**.

### <a name="view-cluster-status"></a>Wyświetlanie stanu klastra
Po utworzeniu klastra możesz sprawdzić klaster w bloku **Przegląd** w portalu. Możesz teraz wyświetlić szczegóły klastra na pulpicie nawigacyjnym, w tym publiczny punkt końcowy klastra oraz link do narzędzia Service Fabric Explorer.

![Stan klastra][cluster-status]

### <a name="visualize-the-cluster-using-service-fabric-explorer"></a>Wizualizowanie klastra za pomocą narzędzia Service Fabric Explorer
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) to odpowiednie narzędzie do wizualizowania klastra i zarządzania aplikacjami.  Service Fabric Explorer jest usługą uruchamianą w klastrze.  Dostęp do tej usługi uzyskasz poprzez kliknięcie linku **Service Fabric Explorer** na stronie **Przegląd** klastra w portalu.  Możesz również wprowadzić jej adres bezpośrednio do przeglądarki: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)

Pulpit nawigacyjny klastra zawiera omówienie klastra, w tym podsumowanie kondycji węzła i aplikacji. Widok węzła przedstawia fizyczny układ klastra. Dla danego węzła można sprawdzić, które aplikacje mają kod wdrożony w tym węźle.

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-to-the-cluster-using-powershell"></a>Nawiązywanie połączenia z klastrem przy użyciu programu PowerShell
Sprawdź, czy klaster działa, nawiązując połączenie przy użyciu programu PowerShell.  Moduł ServiceFabric programu PowerShell jest instalowany przy użyciu [Zestawu SDK usługi Service Fabric](service-fabric-get-started.md).  Polecenie cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) umożliwia ustanowienie połączenia z klastrem.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
Inne przykłady łączenia z klastrem można znaleźć w temacie [Nawiązywanie połączenia z zabezpieczonym klastrem](service-fabric-connect-to-secure-cluster.md). Po nawiązaniu połączenia z klastrem użyj polecenia cmdlet [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps), aby wyświetlić listę węzłów w klastrze oraz informacje o stanie każdego węzła. Element **HealthState** powinien mieć wartość *OK* dla każdego węzła.

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

### <a name="remove-the-cluster"></a>Usuwanie klastra
Klaster usługi Service Fabric składa się z innych zasobów platformy Azure poza samym zasobem klastra. Dlatego też, aby całkowicie usunąć klaster usługi Service Fabric, musisz również usunąć wszystkie zasoby, z których się składa. Najprostszym sposobem na usunięcie klastra i wszystkich wykorzystywanych przez niego zasobów jest usunięcie grupy zasobów. Aby uzyskać informacje o innych sposobach usunięcia klastra lub usunięcia części (nie wszystkich) zasobów w grupie zasobów, zobacz [Usuwanie klastra](service-fabric-cluster-delete.md).

Usuń grupę zasobów w witrynie Azure Portal:
1. Przejdź do klastra usługi Service Fabric, który chcesz usunąć.
2. Kliknij nazwę **Grupy zasobów** na stronie podstawowych elementów klastra.
3. Na stronie **Podstawowe elementy grupy zasobów** kliknij pozycję **Usuń grupę zasobów** i wykonaj instrukcje na tej stronie, aby zakończyć usuwanie grupy zasobów.
    ![Usuwanie grupy zasobów][cluster-delete]


## <a name="use-azure-powershell-to-deploy-a-secure-cluster"></a>Wdrażanie zabezpieczonego klastra przy użyciu modułu Azure Powershell
1. Pobierz na komputer [moduł Azure Powershell w wersji 4.0 lub nowszej](https://docs.microsoft.com/powershell/azure/install-azurerm-ps).

2. Otwórz okno programu Windows PowerShell i uruchom następujące polecenie. 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    Powinny pojawić się dane wyjściowe podobne do następujących.

    ![ps-list][ps-list]

3. Zaloguj się do platformy Azure i wybierz subskrypcję, dla której chcesz utworzyć klaster.

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. Uruchom następujące polecenie, aby utworzyć teraz zabezpieczony klaster. Pamiętaj o dostosowaniu parametrów. 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also the name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    Wykonanie tego polecenia może potrwać od 10 do 30 minut. Na koniec powinny zostać wyświetlone dane wyjściowe podobne do następujących. Dane wyjściowe zawierają informacje dotyczące certyfikatu, usługi KeyVault, do której został przekazany certyfikat, i folderu lokalnego, do którego został skopiowany. 

    ![ps-out][ps-out]

5. Skopiuj wszystkie dane wyjściowe i zapisz je w pliku tekstowym do przyszłego użycia. Zanotuj następujące informacje z danych wyjściowych. 

    - **CertificateSavedLocalPath** : c:\mojecertyfikaty\mojklaster20170504141137.pfx
    - **CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10
    - **ManagementEndpoint** : https://mojklaster.southcentralus.cloudapp.azure.com:19080
    - **ClientConnectionEndpointPort** : 19000

### <a name="install-the-certificate-on-your-local-machine"></a>Instalowanie certyfikatu na komputerze lokalnym
  
Aby połączyć się z klastrem, należy zainstalować certyfikat w magazynie osobistym bieżącego użytkownika. 

Uruchom następujące polecenie programu PowerShell.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\the name of the cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

Teraz możesz przystąpić do nawiązywania połączenia z zabezpieczonym klastrem.

### <a name="connect-to-a-secure-cluster"></a>Nawiązywanie połączenia z zabezpieczonym klastrem 

Uruchom następujące polecenie programu PowerShell w celu nawiązania połączenia z zabezpieczonym klastrem. Szczegóły certyfikatu muszą być zgodne z certyfikatem, który został użyty do skonfigurowania klastra. 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


W poniższym przykładzie pokazano uzupełnione parametry: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Uruchom następujące polecenie, aby sprawdzić poprawność połączenia i upewnić się, że klaster jest w dobrej kondycji.

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-to-your-cluster-from-visual-studio"></a>Publikowanie aplikacji w klastrze z poziomu programu Visual Studio

Teraz po skonfigurowaniu klastra platformy Azure możesz opublikować w nim swoje aplikacje z poziomu programu Visual Studio. W tym celu wykonaj instrukcje zawarte w dokumencie [Publish to an cluster](service-fabric-publish-app-remote-cluster.md) (Publikowanie w klastrze). 

### <a name="remove-the-cluster"></a>Usuwanie klastra
Klaster składa się z innych zasobów platformy Azure poza samym zasobem klastra. Najprostszym sposobem na usunięcie klastra i wszystkich wykorzystywanych przez niego zasobów jest usunięcie grupy zasobów. 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a>Następne kroki
Teraz po skonfigurowaniu klastra programowania możesz spróbować wykonać następujące czynności:
* [Tworzenie zabezpieczonego klastra w portalu](service-fabric-cluster-creation-via-portal.md)
* [Tworzenie klastra na podstawie szablonu](service-fabric-cluster-creation-via-arm.md) 
* [Wdrażanie aplikacji przy użyciu programu PowerShell](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
