---
title: "aaaUpgrade autonomiczny sieć szkieletowa usług Azure klastra w systemie Windows Server | Dokumentacja firmy Microsoft"
description: "Uaktualnij hello sieć szkieletowa usług Azure kod i/lub konfigurację, która uruchamia autonomicznej klastra sieci szkieletowej usług, w tym ustawieniu trybu aktualizacji klastra hello."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a>Uaktualnienie z autonomicznej usługi sieć szkieletowa usług Azure w klastrze systemu Windows Server
> [!div class="op_single_selector"]
> * [Klastrze platformy Azure](service-fabric-cluster-upgrade.md)
> * [Autonomiczny klastra](service-fabric-cluster-upgrade-windows-server.md)
>
>

Systemu nowoczesnych tooupgrade możliwości hello został pomyślnie długoterminowej toohello klucza produktu. Klastra usługi sieć szkieletowa usług Azure jest zasobem, którego jesteś właścicielem. W tym artykule opisano, jak można upewnij się, że klastra hello jest zawsze uruchamiane w obsługiwanych wersjach programu kodu sieci szkieletowej usług i konfiguracji.

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a>Formant hello sieci szkieletowej usług wersji, która działa w klastrze
tooset aktualizuje toodownload Twojego klastra usługi sieć szkieletowa, gdy firma Microsoft publikuje nową wersję zestawu hello **fabricClusterAutoupgradeEnabled** tootrue konfiguracji klastra. obsługiwana wersja usługi sieć szkieletowa usług, które mają toobe Twojego klastra na powitania zestaw tooselect **fabricClusterAutoupgradeEnabled** toofalse konfiguracji klastra.

> [!NOTE]
> Upewnij się, że klaster zawsze działa obsługiwana wersja usługi Service Fabric. Microsoft ogłasza hello wydaniu nowej wersji platformy Service Fabric, poprzedniej wersji hello jest oznaczony w celu obsługi po co najmniej 60 dni od daty hello hello anonsu. Nowe wersje są ogłaszane [na blogu zespołu usługi sieć szkieletowa hello](https://blogs.msdn.microsoft.com/azureservicefabric/). nową wersję Hello jest toochoose dostępne w tym momencie.
>
>

Klaster toohello nowej wersji można uaktualnić tylko wtedy, gdy używane są konfiguracji węzła stylu produkcji, gdzie każdy węzeł sieci szkieletowej usług jest przydzielane w oddzielnych maszyny fizycznej lub wirtualnej. Jeśli masz klaster programowanie, gdzie więcej niż jeden węzeł sieci szkieletowej usług znajduje się na jednej maszynie fizycznej lub wirtualnej, należy ponownie utworzyć klaster hello hello nowej wersji.

Dwa różne przepływów pracy można uaktualnić najnowszej wersji toohello klastra lub obsługiwana wersja usługi Service Fabric. Jeden przepływ pracy jest przeznaczony dla klastrów, które mają automatycznie łączności toodownload hello najnowszej wersji. Witaj inny przepływ pracy jest klastrów, które nie mają łączność toodownload hello sieci szkieletowej usług najnowszą.

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a>Uaktualnij klastrów, które mają łączność toodownload hello najnowsze kod i Konfiguracja
Użyć wersji tooa obsługiwane klastra tooupgrade te kroki, jeśli węzły klastra jest połączony z Internetem za[http://download.microsoft.com](http://download.microsoft.com).

W przypadku klastrów połączeniem zbyt[http://download.microsoft.com](http://download.microsoft.com), Microsoft okresowo sprawdza dostępność nowych wersji platformy Service Fabric hello.

Dostępna jest nowa wersja usługi Service Fabric, pakietów hello jest pobierana lokalnie toohello klastra i udostępnione do uaktualnienia. Ponadto tooinform powitania klienta z tej nowej wersji, hello system zawiera ostrzeżenia kondycji jawne klastra, która jest podobne toohello następujące:

"hello Obsługa bieżącej wersji wersja # klastra kończy [Date]".

Po uruchomieniu klastra hello hello najnowszej wersji ostrzeżenie hello zniknie.

#### <a name="cluster-upgrade-workflow"></a>Przepływ pracy uaktualniania klastra
Po zostanie wyświetlone ostrzeżenie dotyczące kondycji klastra hello, hello następujące:

1. Połącz toohello klastra z dowolnym komputerze, że administrator dostępu tooall hello maszyny, które są wyświetlane jako węzły w klastrze hello. Ten skrypt jest uruchamiany na maszynie Hello nie ma toobe częścią klastra hello.

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. Pobierz listę hello można uaktualnić do wersji usługi sieć szkieletowa usług.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    Należy pobrać toothis podobne dane wyjściowe:

    ![Pobieranie wersji sieci szkieletowej][getfabversions]
3. Uruchom wersji dostępnych tooan uaktualnienia klastra przy użyciu [Start ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) polecenia programu PowerShell

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   postęp hello toomonitor hello uaktualnienia, można użyć Eksploratora usługi sieć szkieletowa lub hello uruchom następujące polecenia programu Windows PowerShell.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Jeśli zasady dotyczące kondycji hello klastra nie są spełnione, uaktualnienie hello zostanie wycofana. zasady dotyczące kondycji niestandardowych toospecify dla hello **Start ServiceFabricClusterUpgrade** polecenia, zobacz dokumentację dla [Start ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).

Po rozwiązaniu problemów hello, które spowodowało wycofanie hello zainicjować ponownie uaktualnienie hello przez następujące hello opisanej wcześniej te same czynności.

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a>Uaktualnij klastrów, które mają <U>bez łączności</u> toodownload hello najnowsze kodem i konfiguracją
Użyć wersji tooa obsługiwane klastra tooupgrade te kroki, jeśli węzły klastra nie ma łączności z Internetem za[http://download.microsoft.com](http://download.microsoft.com).

> [!NOTE]
> Jeśli korzystasz z klastra, który nie jest połączony toohello Internet, trzeba będzie toomonitor hello sieci szkieletowej usług team blog toolearn o nowej wersji. Witaj systemu nie są wyświetlane tooalert ostrzeżenie kondycji klastra z nową wersją.  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a>Automatycznego inicjowania obsługi administracyjnej vs ręcznego inicjowania obsługi administracyjnej.
automatyczne pobieranie tooenable i rejestracji hello najnowszą wersję kodu, należy skonfigurować usługi aktualizacji sieci szkieletowej. Zobacz toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt wewnątrz hello [pakiet autonomiczny](service-fabric-cluster-standalone-package-contents.md) instrukcje.
W przypadku ręczny proces wykonaj poniższe instrukcje hello.

Modyfikowanie użytkownika hello tooset konfiguracji klastra po toofalse właściwości przed rozpoczęciem uaktualniania programu configuration.

        "fabricClusterAutoupgradeEnabled": false,

Odwołuje się zbyt[cmd PS Start ServiceFabricClusterConfigurationUpgrade ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) szczegóły użycia. Przed rozpoczęciem uaktualniania konfiguracji hello, upewnij się, że tooupdate "clusterConfigurationVersion" w Twojej JSON.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a>Przepływ pracy uaktualniania klastra

1. Uruchom Get ServiceFabricClusterUpgrade w jednym z węzłów hello hello klastra i zanotuj hello TargetCodeVersion.
2. Witaj uruchom następujące polecenie w toolist maszyny połączenia internetowego uaktualnić wszystkie wersje zgodne z bieżącą wersją hello i Pobierz hello odpowiadającego pakietu z hello łączy do pobierania.

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. Połącz toohello klastra z dowolnym komputerze, że administrator dostępu tooall hello maszyny, które są wyświetlane jako węzły w klastrze hello. Ten skrypt jest uruchamiany na maszynie Hello nie ma toobe częścią klastra hello

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. Skopiuj pakiet hello pobrane do magazynu obrazu klastra hello.

5. Zarejestruj hello skopiować pakiet.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. Uruchom tooan uaktualnienia klastra dostępnej wersji.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   Możesz monitorować postęp hello hello uaktualnienia w narzędziu Service Fabric Explorer, lub uruchomić hello następującego polecenia programu PowerShell.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Jeśli zasady dotyczące kondycji hello klastra nie są spełnione, uaktualnienie hello zostanie wycofana. zasady dotyczące kondycji niestandardowych toospecify dla hello **Start ServiceFabricClusterUpgrade** polecenia, zobacz dokumentację hello [Start ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).

Po rozwiązaniu problemów hello, które spowodowało wycofanie hello zainicjować ponownie uaktualnienie hello przez następujące hello opisanej wcześniej te same czynności.


## <a name="upgrade-hello-cluster-configuration"></a>Uaktualnij konfigurację klastra hello
Przed rozpoczęciem uaktualniania konfiguracji hello można sprawdzić czy nowy kod json konfiguracji klastra za pomocą skryptu powershell hello hello autonomicznych pakietu.

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
lub

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

Niektóre konfiguracje nie może zostać uaktualniony, takich jak punkty końcowe, nazwa klastra IP węzła itd. Spowoduje to test hello nowego klastra konfiguracji json przed hello stary i zgłoszenia błędów w oknie programu Powershell hello, jeśli istnieje jakikolwiek problem.

Uaktualnianie konfiguracji klastra hello tooupgrade, uruchom **Start ServiceFabricClusterConfigurationUpgrade**. Uaktualnianie konfiguracji Hello jest przetworzonych domeny uaktualnień w domenie uaktualnienia.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a>Uaktualnianie konfiguracji certyfikatu klastra  
Certyfikat klastra jest używany do uwierzytelniania między węzłami klastra, więc przerzucane hello certyfikatu należy wykonać z wyjątkową ostrożność ponieważ niepowodzenia zablokuje hello komunikacji między węzłami klastra.  
Z technicznego punktu widzenia obsługiwane są trzy opcje:  

1. Uaktualnienie jeden certyfikat: ścieżka uaktualnienia hello jest "certyfikat (podstawowy) -> B certyfikatu (podstawowy) -> C certyfikatu (podstawowy) ->...".   
2. Double certyfikatu uaktualnienia: ścieżka uaktualnienia hello jest "B (pomocniczy) -> B certyfikatu (podstawowy) i certyfikatów (podstawowy) -> certyfikatów (podstawowy) -> B certyfikatu (podstawowy) i C (pomocniczy) -> C certyfikatu (podstawowy) ->...".
3. Uaktualnianie typu certyfikatu: Konfiguracja certyfikatów na podstawie CommonName configuration <> — na podstawie odcisku palca certyfikatu. Na przykład odcisk palca certyfikatu (podstawowy) i certyfikatów CommonName C. -> B odcisk palca (pomocniczy)


## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak toocustomize niektórych [ustawienia klastra usługi sieć szkieletowa](service-fabric-cluster-fabric-settings.md).
* Dowiedz się, jak za[skalowanie klastra i wylogowywanie](service-fabric-cluster-scale-up-down.md).
* Dowiedz się więcej o [uaktualnień aplikacji](service-fabric-application-upgrade.md).

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
