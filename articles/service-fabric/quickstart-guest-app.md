---
title: "Szybkie wdrażanie istniejącej aplikacji do klastra usługi Azure Service Fabric"
description: "Użyj klastra usługi Azure Service Fabric do hostowania istniejącej aplikacji w technologii Node.js za pomocą programu Visual Studio."
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
ms.date: 12/06/2017
ms.author: adegeo
ms.openlocfilehash: 304d22c14f6877138213db14333773f1e293c57a
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a>Hostowanie aplikacji w technologii Node.js w usłudze Azure Service Fabric

Przewodnik Szybki start ułatwia wdrożenie istniejącej aplikacji (w tym przykładzie w technologii Node.js) do klastra usługi Service Fabric działającego na platformie Azure.

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz [skonfigurowane środowisko programowania](service-fabric-get-started.md). Obejmuje to zainstalowanie zestawu SDK usługi Service Fabric i programu Visual Studio 2017 lub 2015.

Niezbędna jest również aplikacja Node.js do wdrożenia. Przewodnik Szybki Start używa prostej witryny sieci Web w technologii Node.js, którą można pobrać [stąd][download-sample]. W następnym kroku po utworzeniu projektu wyodrębnij ten plik do swojego folderu `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\`.

Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto][create-account].

## <a name="create-the-service"></a>Tworzenie usługi

Uruchom program Visual Studio jako **administrator**.

Tworzenie projektu przy użyciu klawiszy `CTRL`+`SHIFT`+`N`

W oknie dialogowym **Nowy projekt** wybierz kolejno pozycje **Chmura > Aplikacja usługi Service Fabric**.

Nazwij aplikację **MyGuestApp** i naciśnij przycisk **OK**.

>[!IMPORTANT]
>W technologii Node.js można łatwo obejść limit systemu Windows 260 znaków dla ścieżek. Użyj krótkiej ścieżki dla samego projektu, takiej jak **c:\code\svc1**. Opcjonalnie możesz wykonać **[te instrukcje](https://stackoverflow.com/a/41687101/1664231)**, aby włączyć długie ścieżki plików w systemie Windows 10.
   
![Okno dialogowe nowego projektu w programie Visual Studio][new-project]

W następnym oknie dialogowym można utworzyć usługę Service Fabric dowolnego typu. Na potrzeby tego przewodnika Szybki start wybierz pozycję **Wykonywalna gościa**.

Nazwij usługę **MyGuestService** i ustaw opcje po prawej stronie na następujące wartości:

| Ustawienie                   | Wartość |
| ------------------------- | ------ |
| Folder pakietu kodu       | _&lt;folder z aplikacją w technologii Node.js&gt;_ |
| Zachowanie pakietu kodu     | Skopiuj zawartość folderu do projektu |
| Program                   | node.exe |
| Argumenty                 | server.js |
| Folder roboczy            | CodePackage |

Naciśnij przycisk **OK**.

![Okno dialogowe nowej usługi w programie Visual Studio][new-service]

Program Visual Studio utworzy projekt aplikacji i projekt usługi aktora, a następnie wyświetli je w Eksploratorze rozwiązań.

Projekt aplikacji (**MyGuestApp**) nie zawiera bezpośrednio żadnego kodu. Zamiast tego odwołuje się do zestawu projektów usług. Ponadto zawiera trzy inne typy zawartości:

* **Profile publikowania**  
Preferencje narzędzi dla różnych środowisk.

* **Skrypty**  
Skrypt programu PowerShell przeznaczony do wdrażania/uaktualniania aplikacji.

* **Definicja aplikacji**  
Zawiera manifest aplikacji w ramach elementu *ApplicationPackageRoot*. Skojarzone pliki parametrów aplikacji znajdują się w ramach elementu *ApplicationParameters*, które definiują aplikację i umożliwiają jej konfigurowanie dla konkretnego środowiska.
    
Aby zapoznać się z omówieniem zawartości projektu usługi, zobacz [Pierwsze kroki z usługami Reliable Services](service-fabric-reliable-services-quick-start.md).

## <a name="set-up-networking"></a>Konfigurowanie zasobów sieciowych

Wdrażana przykładowa aplikacja w technologii Node.js korzysta z portu **80** i dlatego trzeba poinformować usługę Service Fabric, że ten port musi być widoczny.

Otwórz plik **ServiceManifest.xml** w projekcie. W dolnej części manifestu znajduje się blok `<Resources> \ <Endpoints>` z już zdefiniowanym wpisem. Zmodyfikuj ten wpis, aby dodać parametry `Port`, `Protocol`, i `Type`. 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-to-azure"></a>Wdrażanie na platformie Azure

Po naciśnięciu klawisza **F5** i uruchomieniu projektu zostanie on wdrożony w lokalnym klastrze. Zamiast tego wdrożymy go jednak na platformie Azure.

Kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Publikuj...**. Zostanie otwarte okno dialogowe publikowania na platformie Azure.

![Okno dialogowe Publikuj na platformie Azure dla usługi Service Fabric][publish]

Wybierz docelowy profil **PublishProfiles\Cloud.xml**.

Jeśli nie zostało to wykonane wcześniej, wybierz konto platformy Azure, na którym ma się odbyć wdrożenie. Jeśli nie masz jeszcze konta, [utwórz je][create-account].

W obszarze **Punkt końcowy połączenia** wybierz klaster usługi Service Fabric do wdrożenia. Jeśli go nie masz, wybierz opcję **&lt;Utwórz nowy klaster...&gt;**. Spowoduje to otwarcie okna przeglądarki sieci Web z witryną Azure Portal. Aby uzyskać więcej informacji, zobacz artykuł dotyczący [tworzenia klastra w portalu](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal). 

Podczas tworzenia klastra usługi Service Fabric upewnij się, że ustawienie **Niestandardowe punkty końcowe** ma wartość **80**.

![Konfiguracja typu węzła usługi sieci szkieletowej z niestandardowym punktem końcowym][custom-endpoint]

Tworzenie nowego klastra usługi Service Fabric zajmuje trochę czasu. Po jego utworzeniu wróć do okna dialogowego publikowania i wybierz opcję **&lt;Odśwież&gt;**. Nowy klaster znajduje się w polu listy rozwijanej; wybierz go.

Naciśnij przycisk **Publikuj** i poczekaj na zakończenie wdrożenia.

Może to potrwać kilka minut. Po zakończeniu instalacji może minąć jeszcze kilka minut, zanim aplikacja stanie się w pełni dostępna.

## <a name="test-the-website"></a>Testowanie witryny sieci Web

Po opublikowaniu usługi przetestuj ją w przeglądarce sieci web. 

Najpierw otwórz witrynę Azure Portal i znajdź swoją usługę Service Fabric.

Sprawdź adres bloku omówienia usługi. Użyj nazwy domeny z właściwości _Punkt końcowy połączenia klienta_. Na przykład `http://mysvcfab1.westus2.cloudapp.azure.com`.

![Blok omówienia usługi sieci szkieletowej w witrynie Azure Portal][overview]

Przejdź do tego adresu, gdy pojawi się odpowiedź `HELLO WORLD`.

## <a name="delete-the-cluster"></a>Usuwanie klastra

Pamiętaj, aby usunąć wszystkie zasoby, które zostały utworzone dla tego przewodnika Szybki start, ponieważ naliczane są za nie opłaty.

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