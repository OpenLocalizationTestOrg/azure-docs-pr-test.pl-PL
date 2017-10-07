---
title: "aaaQuickly wdrażanie istniejącego klastra usługi sieć szkieletowa usług Azure tooan aplikacji"
description: "Sieć szkieletowa usług Azure klastra toohost istniejącą aplikację Node.js za pomocą programu Visual Studio."
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a>Hostowanie aplikacji w technologii Node.js w usłudze Azure Service Fabric

Ta opcja szybkiego startu ułatwia wdrożenie klastra usługi sieć szkieletowa istniejących tooa (Node.js w tym przykładzie) aplikacji działających na platformie Azure.

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz [skonfigurowane środowisko programowania](service-fabric-get-started.md). W tym zainstalowanie hello zestawu SDK usług sieci szkieletowej i Visual Studio 2017 lub 2015.

Należy również toohave istniejącą aplikację Node.js do wdrożenia. Przewodnik Szybki Start używa prostej witryny sieci Web w technologii Node.js, którą można pobrać [stąd][download-sample]. Wyodrębnij tooyour tego pliku `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder po utworzeniu projektu hello w hello następnego kroku.

Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto][create-account].

## <a name="create-hello-service"></a>Tworzenie usługi hello

Uruchom program Visual Studio jako **administrator**.

Tworzenie projektu przy użyciu klawiszy `CTRL`+`SHIFT`+`N`

W hello **nowy projekt** okno dialogowe, wybierz **chmury > aplikacji sieci szkieletowej usług**.

Nadaj nazwę aplikacji hello **MyGuestApp** i naciśnij klawisz **OK**.

>[!IMPORTANT]
>Łatwo mogą być dzielone limit 260 znaków hello dla ścieżek zawierających system windows ma node.js. Użyj krótkiej ścieżki dla projektu hello, takiego jak **c:\code\svc1**.
   
![Okno dialogowe nowego projektu w programie Visual Studio][new-project]

Można utworzyć dowolnego typu usługi sieć szkieletowa usług z hello następnego okna dialogowego. Na potrzeby tego przewodnika Szybki start wybierz pozycję **Wykonywalna gościa**.

Nazwa usługi hello **MyGuestService** i ustawianie opcji hello na powitania prawo toohello następujące wartości:

| Ustawienie                   | Wartość |
| ------------------------- | ------ |
| Folder pakietu kodu       | _&lt;folder Hello z aplikacji Node.js&gt;_ |
| Zachowanie pakietu kodu     | Skopiuj folder zawartości tooproject |
| Program                   | node.exe |
| Argumenty                 | server.js |
| Folder roboczy            | CodePackage |

Naciśnij przycisk **OK**.

![Okno dialogowe nowej usługi w programie Visual Studio][new-service]

Visual Studio tworzy projekt aplikacji hello i projekt usługi aktora hello i wyświetla je w Eksploratorze rozwiązań.

Projekt aplikacji Hello (**MyGuestApp**) nie zawiera żadnego kodu bezpośrednio. Zamiast tego odwołuje się do zestawu projektów usług. Ponadto zawiera trzy inne typy zawartości:

* **Profile publikowania**  
Preferencje narzędzi dla różnych środowisk.

* **Skrypty**  
Skrypt programu PowerShell przeznaczony do wdrażania/uaktualniania aplikacji.

* **Definicja aplikacji**  
Zawiera manifest aplikacji hello w ramach *ApplicationPackageRoot*. Pliki parametru skojarzonej aplikacji znajdują się w obszarze *ApplicationParameters*, który Definiowanie aplikacji hello i pozwala tooconfigure specjalnie dla danego środowiska.
    
Omówienie hello zawartości projektu usługi hello, zobacz [Rozpoczynanie pracy z usługami Reliable Services](service-fabric-reliable-services-quick-start.md).

## <a name="set-up-networking"></a>Konfigurowanie zasobów sieciowych

przykład Witaj aplikacja Node.js jest wdrażany firma Microsoft korzysta z portu **80** i potrzebujemy tootell usługi Service Fabric, czego potrzebujemy portem udostępnianym.

Otwórz hello **ServiceManifest.xml** plik w projekcie hello. Dole hello manifestu hello jest `<Resources> \ <Endpoints>` z wpisu, który został już zdefiniowany. Zmodyfikuj ten wpis tooadd `Port`, `Protocol`, i `Type`. 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a>Wdrażanie tooAzure

Jeśli naciśniesz **F5** i uruchomić projekt hello, jest wdrożone toohello klastra lokalnego. Jednak wdróżmy tooAzure zamiast tego.

Kliknij prawym przyciskiem myszy na powitania projektu i wybierz polecenie **publikowania...**  otwierający tooAzure toopublish okna dialogowego.

![Publikowanie tooazure okno dialogowe Usługa sieci szkieletowej usług][publish]

Wybierz hello **PublishProfiles\Cloud.xml** docelowego profilu.

Jeśli jeszcze nie zostało to wcześniej, wybierz toodeploy konto platformy Azure do. Jeśli nie masz jeszcze konta, [utwórz je][create-account].

W obszarze **punktu końcowego połączenia**, wybierz hello toodeploy klastra sieci szkieletowej usług do. Jeśli nie masz, wybierz  **&lt;Utwórz nowy klaster... &gt;**  który otwiera toohello okna przeglądarki sieci web portalu Azure. Aby uzyskać więcej informacji, zobacz [utworzyć klaster w portalu hello](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal). 

Podczas tworzenia klastra usługi sieć szkieletowa hello, upewnij się, że hello tooset **niestandardowe punkty końcowe** ustawienie zbyt**80**.

![Konfiguracja typu węzła usługi sieci szkieletowej z niestandardowym punktem końcowym][custom-endpoint]

Tworzenie nowego klastra usługi sieć szkieletowa przyjmuje niektórych toocomplete czasu. Po został utworzony, przejdź wstecz toohello okna dialogowego publikowania i wybierz  **&lt;Odśwież&gt;**. Hello nowy klaster znajduje się w polu listy rozwijanej hello; Wybierz go.

Naciśnij klawisz **publikowania** i poczekaj, aż hello toofinish wdrożenia.

Może to potrwać kilka minut. Po jej zakończeniu, może upłynąć kilka minut dla toobe aplikacji hello pełni dostępna.

## <a name="test-hello-website"></a>Test hello witryny sieci Web

Po opublikowaniu usługi przetestuj ją w przeglądarce sieci web. 

Najpierw otwórz hello portalu Azure i Znajdź usługi sieć szkieletowa usług.

Przejdź do bloku omówienie hello hello adresu usługi. Użyj nazwy domeny hello z hello _punktu końcowego połączenia klienta_ właściwości. Na przykład `http://mysvcfab1.westus2.cloudapp.azure.com`.

![Usługa sieci szkieletowej omówienie bloku na powitania portalu Azure][overview]

Przejdź do adresu toothis gdzie zobaczysz hello `HELLO WORLD` odpowiedzi.

## <a name="delete-hello-cluster"></a>Usuń klaster hello

Nie zapomnij toodelete wszystkie zasoby hello, utworzone dla tego przewodnika Szybki Start, jak naliczane są opłaty za te zasoby.

## <a name="next-steps"></a>Następne kroki
Przeczytaj więcej na temat [plików wykonywalnych gościa](service-fabric-deploy-existing-app.md).

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F