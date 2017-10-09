---
title: aaaPublish klastra zdalnego tooa aplikacji z programem Visual Studio | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toopublish sieci szkieletowej zdalny tooa aplikacji klastra za pomocą programu Visual Studio."
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: faecd892-eb54-4d9c-8023-c67442afb8e8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/29/2016
ms.author: cawa
ms.openlocfilehash: d0f06f120cc7e22f3f8e73ce0970e1da5823e647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-visual-studio"></a>Wdrażanie i usunąć aplikacje przy użyciu programu Visual Studio
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-deploy-remove-applications.md)
> * [Program Visual Studio](service-fabric-publish-app-remote-cluster.md)
> * [Interfejsy API FabricClient](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

Hello rozszerzenia sieć szkieletowa usług Azure dla programu Visual Studio udostępnia toopublish łatwe, powtarzalnych i skryptowe sposób klastra sieci szkieletowej usług tooa aplikacji.

## <a name="hello-artifacts-required-for-publishing"></a>Artefakty Hello wymagane do opublikowania
### <a name="deploy-fabricapplicationps1"></a>Wdrażanie FabricApplication.ps1
Jest to skrypt PowerShell, który używa ścieżkę profilu publikowania jako parametr do publikowania aplikacji sieci szkieletowej usług. Ponieważ ten skrypt jest częścią aplikacji, są toomodify powitalnej go odpowiednio do potrzeb aplikacji.

### <a name="publish-profiles"></a>Profilów publikowania
Folder w projekt aplikacji hello sieci szkieletowej usług o nazwie **PublishProfiles** zawiera pliki XML, które przechowują informacje niezbędne do publikowania aplikacji, takich jak:

* Parametry połączenia klastra sieci szkieletowej usług
* Plik parametrów aplikacji tooan ścieżki
* Ustawienia uaktualniania

Domyślnie aplikacja obejmuje trzy profilów publikowania: Local.1Node.xml, Local.5Node.xml i Cloud.xml. Możesz dodać więcej profilów kopiując i wklejając jedną hello domyślnych plików.

### <a name="application-parameter-files"></a>Pliki parametrów aplikacji
Folder w projekt aplikacji hello sieci szkieletowej usług o nazwie **ApplicationParameters** zawiera pliki XML dla wartości parametru manifestu aplikacji określone przez użytkownika. Pliki manifestu aplikacji mogą nadać parametry, dzięki czemu można użyć innych wartości dla ustawienia wdrażania. Zobacz toolearn więcej informacji na temat aplikacji, ustawianie [Zarządzanie wiele środowisk w sieci szkieletowej usług](service-fabric-manage-multiple-environment-app-configuration.md).

> [!NOTE]
> Dla usług aktora powinno utworzyć projekt hello najpierw przed podjęciem próby wykonania tooedit hello plik w edytorze lub za pośrednictwem hello opublikować okno dialogowe. Jest to spowodowane część pliki manifestu hello zostanie wygenerowana podczas kompilacji hello.

## <a name="toopublish-an-application-using-hello-publish-service-fabric-application-dialog-box"></a>toopublish aplikacji przy użyciu okno dialogowe hello publikowania aplikacji sieci szkieletowej usług
Witaj następująca procedura przedstawia sposób hello toopublish aplikacji przy użyciu **publikowania aplikacji sieci szkieletowej usług** okno dialogowe podał hello Visual Studio Service Fabric Tools.

1. W menu skrótów hello hello projektu aplikacji sieci szkieletowej usług, wybierz **publikowania...** Witaj tooview **publikowania aplikacji sieci szkieletowej usług** okno dialogowe.
   
    ![Witaj ** opublikować usługi sieci szkieletowej aplikacji ** — okno dialogowe][0]
   
    Hello pliku wybranego w hello **docelowego profilu** jest lista rozwijana, gdy wszystkie ustawienia hello, z wyjątkiem **manifestu wersji**, są zapisywane. Można ponownie użyć istniejącego profilu lub utworzyć nową, wybierając **<... zarządzania profilami >** w hello **docelowego profilu** pole listy rozwijanej. Po wybraniu profilu publikowania, jego zawartość jest wyświetlana w odpowiednie pola hello hello okna dialogowego. toosave zmiany w dowolnym momencie, wybierz hello **Zapisz profil** łącza.    
2. W hello **punktu końcowego połączenia** Określ punkt końcowy publikowania lokalnego lub zdalnego klastra sieci szkieletowej usług firmy. tooadd lub zmień hello punktu końcowego połączenia, kliknij na powitania **punktu końcowego połączenia** listy rozwijanej. Witaj przedstawiono hello dostępne sieci szkieletowej usług klastrowania połączenia punkty końcowe toowhich, który można opublikować oparte na subskrypcjach platformy Azure. Należy zauważyć, że jeśli tooVisual Studio nie jest już zalogowany, będzie zostanie wyświetlony monit o toodo tak.
   
    Użyj hello toochoose pole okna dialogowego wyboru klastra z zestawu hello dostępnych subskrypcji i klastrów.
   
    ![Witaj ** okno dialogowe Wybieranie usługi sieć szkieletowa klastra **][1]
   
   > [!NOTE]
   > Jeśli chcesz toopublish tooan dowolnego punktu końcowego (na przykład strona klastra), zobacz hello **publikowania punktu końcowego dowolnego klastra tooan** poniższej sekcji.
   > 
   > 
   
    Po wybraniu punktu końcowego programu Visual Studio weryfikuje klastra sieci szkieletowej usług toohello wybrane połączenia hello. Jeśli hello klastra nie jest bezpieczne, Visual Studio można połączyć z tooit natychmiast. Jednak jeśli klaster hello jest bezpieczne, konieczne będzie tooinstall certyfikatu na komputerze lokalnym przed kontynuowaniem. Zobacz [jak tooconfigure bezpiecznych połączeń](service-fabric-visualstudio-configure-secure-connections.md) Aby uzyskać więcej informacji. Gdy wszystko będzie gotowe, wybierz hello **OK** przycisku. Witaj wybranego klastra jest wyświetlana w hello **publikowania aplikacji sieci szkieletowej usług** okno dialogowe.
3. W hello **plik parametrów aplikacji** listy rozwijanej wybierz plik parametrów aplikacji tooan. Plik parametrów aplikacji zostały określone przez użytkownika wartości dla parametrów w pliku manifestu aplikacji hello. tooadd lub zmień parametr, wybierz hello **Edytuj** przycisku. Wprowadź lub zmień wartość parametru hello hello **parametrów** siatki. Gdy wszystko będzie gotowe, wybierz hello **zapisać** przycisku.
   
    ![Witaj ** okno dialogowe Edytowanie parametrów **][2]
4. Użyj hello **hello uaktualniania aplikacji** toospecify wyboru czy opublikować to działanie jest uaktualnienie. Uaktualnienie publikowania akcje różnią się od normalnego publikowania akcje. Zobacz [uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md) listę różnic. Ustawienia uaktualniania tooconfigure, wybierz hello **skonfigurować ustawienia uaktualnienia** łącza. zostanie wyświetlony Hello Edytor parametr uaktualnienia. Zobacz [skonfigurować hello uaktualnienie aplikacji usługi sieć szkieletowa](service-fabric-visualstudio-configure-upgrade.md) toolearn więcej informacji na temat uaktualniania parametrów.
5. Wybierz hello **wersji manifestu...** przycisk tooview hello **edytować wersji** okno dialogowe. Dla miejsca tootake uaktualnienia należy tooupdate aplikacji i wersji usługi. Zobacz [samouczek uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade-tutorial.md) toolearn jak aplikacji i wersji manifestu usługi wpływ procesu uaktualniania.
   
    ![Witaj ** okno dialogowe Edytowanie wersji **][3]
   
    Użycie aplikacji hello i wersji usługi wersjonowania semantycznego, takie jak 1.0.0 lub wartości liczbowe w formacie hello 1.0.0.0, wybierz hello **automatycznie Aktualizuj wersje aplikacji i usługi** opcji. Jeśli możesz wybrać tę opcję, usługa hello i numery wersji aplikacji są automatycznie aktualizowane przy każdym code, config lub wersja pakietu danych jest aktualizowany. Jeśli wolisz wersji hello tooedit ręcznie, wyczyść toodisable wyboru hello tej funkcji.
   
   > [!NOTE]
   > Na wszystkich tooappear wpisy pakiet w projekcie aktora najpierw utworzyć toogenerate projektu hello hello wpisów w plikach manifestu usługi hello.
   > 
   > 
6. Po zakończeniu określania wszystkie niezbędne ustawienia hello, wybierz hello **publikowania** przycisk toopublish Twojego toohello aplikacji wybrany klaster sieci szkieletowej usług. są stosowane ustawienia Hello toohello publikowania procesu.

## <a name="publish-tooan-arbitrary-cluster-endpoint-including-party-clusters"></a>Opublikuj punkt końcowy dowolnego klastra tooan (w tym klastrów firmy)
Witaj publikowania środowiska Visual Studio jest zoptymalizowana pod kątem publikowania klastry tooremote skojarzone z jednej z Twoich subskrypcji platformy Azure. Jednak jest możliwe toopublish tooarbitrary z punktów końcowych (takich jak klastry strona usługi Service Fabric) przez bezpośredniej edycji hello publikowania profilu XML. Zgodnie z powyższym opisem trzech profilów publikowania znajdują się domyślnie —**Local.1Node.xml**, **Local.5Node.xml**, i **Cloud.xml**—, ale są toocreate-Zapraszamy! dodatkowe profile dla różnych środowisk. Na przykład może być toocreate profil publikowania tooparty klastrów, być może o nazwie **Party.xml**.

Jeśli łączysz tooan niezabezpieczone klastra hello punktu końcowego połączenia klastra, wszystkie, która jest wymagana jest takie jak `partycluster1.eastus.cloudapp.azure.com:19000`. W tym przypadku hello punktu końcowego połączenia w hello publikowania profil powinien wyglądać mniej więcej tak:

```XML
<ClusterConnectionParameters ConnectionEndpoint="partycluster1.eastus.cloudapp.azure.com:19000" />
```

  Jeśli łączysz tooa zabezpieczonych klastra konieczne będzie również szczegóły hello tooprovide hello certyfikatu klienta z toobe magazynu lokalnego hello używany do uwierzytelniania. Aby uzyskać więcej informacji, zobacz [klastra sieci szkieletowej usług tooa bezpiecznych połączeń Konfigurowanie](service-fabric-visualstudio-configure-secure-connections.md).

  Po skonfigurowaniu swój profil publikowania, możesz odwoływać się do niej w hello okno dialogowe publikowanie, jak pokazano poniżej.

  ![Nowy profil publikowania w publikowania — okno dialogowe][4]

  Należy pamiętać, że w takim przypadku hello nowego profilu publikowania punktów tooone pliki parametrów aplikacji hello w domyślnej. Jest to odpowiednie, jeśli chcesz toopublish hello numer tooa konfiguracji aplikacji tego samego środowiska. Z kolei w przypadkach, w którym ma toohave różne konfiguracje dla poszczególnych środowisk, który ma toopublish do Czy rozsądne toocreate znaczeniu plik parametrów aplikacji.

## <a name="next-steps"></a>Następne kroki
proces publikowania hello tooautomate w środowisku ciągłej integracji, zobacz temat toolearn [Konfigurowanie ciągłej integracji usługi sieć szkieletowa](service-fabric-set-up-continuous-integration.md).

[0]: ./media/service-fabric-publish-app-remote-cluster/PublishDialog.png
[1]: ./media/service-fabric-publish-app-remote-cluster/SelectCluster.png
[2]: ./media/service-fabric-publish-app-remote-cluster/EditParams.png
[3]: ./media/service-fabric-publish-app-remote-cluster/EditVersions.png
[4]: ./media/service-fabric-publish-app-remote-cluster/publish-to-party-cluster.png
