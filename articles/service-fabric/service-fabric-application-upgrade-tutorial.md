---
title: Samouczek uaktualniania aplikacji sieci szkieletowej aaaService | Dokumentacja firmy Microsoft
description: "W tym artykule przedstawiono hello środowisko wdrażania aplikacji usługi Service Fabric, zmiana kodu hello i wprowadza uaktualnienia w programie Visual Studio."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a3181a7a-9ab1-4216-b07a-05b79bd826a4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: d069ff0b291018dbac846e65cddff1e9d73d156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-tutorial-using-visual-studio"></a>Samouczek uaktualniania aplikacji sieci szkieletowej usług za pomocą programu Visual Studio
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Program Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

Sieć szkieletowa usług Azure upraszcza proces hello uaktualniania aplikacji w chmurze w celu zapewnienia uaktualnienia tylko zmienione usługi, i że kondycja aplikacji jest monitorowane w trakcie procesu uaktualniania hello. On również automatycznie przywraca poprzedniej wersji toohello aplikacji hello przypadku napotkania problemów. Uaktualnienia aplikacji sieci szkieletowej usług są *przestój Zero*, ponieważ aplikacja hello można uaktualnić bez przestojów. W tym samouczku przedstawiono sposób toocomplete uaktualnienia stopniowego z programu Visual Studio.

## <a name="step-1-build-and-publish-hello-visual-objects-sample"></a>Krok 1: Tworzenie i publikowanie przykład obiektów Visual hello
Najpierw pobierz hello [obiektów Visual](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Actors/VisualObjects) aplikacji z usługi GitHub. Następnie, tworzenie i publikowanie aplikacji hello, klikając prawym przyciskiem myszy projekt aplikacji hello, **VisualObjects**i wybierając hello **publikowania** w element menu hello sieci szkieletowej usług.

![Menu kontekstowe dla aplikacji sieci szkieletowej usług][image1]

Wybieranie **publikowania** powoduje wyświetlenie okna podręcznego, i można ustawić hello **docelowego profilu** za**PublishProfiles\Local.xml**. Hello okno powinno wyglądać podobnie do następującego hello przed kliknięciem przycisku **publikowania**.

![Publikowanie aplikacji sieci szkieletowej usług][image2]

Teraz możesz kliknąć **publikowania** w oknie dialogowym hello. Można użyć [Service Fabric Explorer tooview hello klastra i hello aplikacji](service-fabric-visualizing-your-cluster.md). Obiekty Visual aplikacji Hello ma usługi sieci web, czy można przejść, wpisując tooby [http://localhost:8081/visualobjects/](http://localhost:8081/visualobjects/) hello pasku adresu przeglądarki.  10 obiektów visual przestawnych przenoszenia na ekranie powitania powinna zostać wyświetlona.

**Uwaga:** wdrażania zbyt`Cloud.xml` profilu (sieć szkieletowa usług Azure,) aplikacji hello powinien być dostępny w **http://{ServiceFabricName}. { Region}.cloudapp.Azure.com:8081/visualobjects/**. Upewnij się, że masz `8081/TCP` skonfigurowane w hello modułu równoważenia obciążenia (Znajdź hello modułu równoważenia obciążenia w hello tej samej grupie zasobów co hello wystąpienia usługi sieć szkieletowa).

## <a name="step-2-update-hello-visual-objects-sample"></a>Krok 2: Aktualizacja hello obiektów Visual próbki
Można zauważyć, że z wersją hello, który został wdrożony w kroku 1, obiektów visual hello nie Obróć. Uaktualnij teraz tooone tej aplikacji, gdzie obiektów visual hello również Obróć.

Wybierz projekt VisualObjects.ActorService hello w hello VisualObjects rozwiązania, a następnie otwórz hello **VisualObjectActor.cs** pliku. W tym pliku Przejdź metody toohello `MoveObject`, komentarz `visualObject.Move(false)`i Usuń komentarz `visualObject.Move(true)`. Ta zmiana kodu obraca obiekty powitania po uaktualnieniu hello usługi.  **Teraz możesz utworzyć (nie kompilację) hello rozwiązanie**, które kompilacje hello zmodyfikowane projekty. W przypadku wybrania *odbudowanie wszystkiego*, masz wersji hello tooupdate hello wszystkich projektów.

Należy również tooversion naszej aplikacji. Wersja hello toomake zmienia się po kliknięciu prawym przyciskiem myszy na powitania **VisualObjects** projektu, można użyć hello Visual Studio **edytować wersji manifestu** opcji. Wybranie tej opcji wywołuje hello dialogowe dla wersji edition w następujący sposób:

![Okno dialogowe kontroli wersji][image3]

Wersje hello aktualizacji dla hello zmodyfikować projektów i ich pakiety kodu, wraz z tooversion aplikacji hello 2.0.0. Po dokonaniu zmiany hello hello manifest powinna wyglądać następujące hello (pogrubienie części Pokaż zmiany hello):

![Aktualizowanie wersji][image4]

narzędzia Visual Studio Hello można wykonać automatyczne pakiety zbiorcze wersji po wybraniu **automatycznie Aktualizuj wersje aplikacji i usługi**. Jeśli używasz [programu SemVer](http://www.semver.org), należy tooupdate hello kod i/lub konfiguracji pakietu wersji tylko, jeśli opcja jest zaznaczona.

Zapisz zmiany hello, a teraz sprawdzić hello **hello uaktualniania aplikacji** pole.

## <a name="step-3--upgrade-your-application"></a>Krok 3: Uaktualnienie aplikacji
Zapoznaj się z hello [parametry uaktualniania aplikacji](service-fabric-application-upgrade-parameters.md) i hello [procesu uaktualniania](service-fabric-application-upgrade.md) tooget dobrą znajomość hello uaktualniania różnych parametrów, limity czasu i kryterium kondycji, które można można zastosować. W ramach tego przewodnika kryterium oceny kondycji usługi hello ustawiono domyślne toohello (tryb niemonitorowane). Te ustawienia można skonfigurować, wybierając **skonfigurować ustawienia uaktualnienia** , a następnie modyfikując hello parametry zgodnie z potrzebami.

Teraz możemy wszystkie aplikacji hello toostart zestaw uaktualnienia, wybierając **publikowania**. Ta opcja uaktualnia Twojej aplikacji tooversion 2.0.0, w którym Obróć hello obiektów. Sieć szkieletowa usług uaktualnia jednej domeny aktualizacji w czasie (niektóre obiekty są aktualizowane w pierwszej kolejności, zostały wykonane przez innych użytkowników) i hello usługi, pozostanie dostępne podczas uaktualniania hello. Usługa toohello dostępu można sprawdzić za pomocą klienta (przeglądarka).  

Teraz, jak hello kontynuowane uaktualniania aplikacji, można go monitorować z Eksploratora usługi sieć szkieletowa, za pomocą hello **uaktualnień w toku** kartę w obszarze aplikacji hello.

W ciągu kilku minut można uaktualnić wszystkie domeny aktualizacji (ukończone), a okno danych wyjściowych programu Visual Studio hello powinny prezentować również, że tego uaktualnienia hello zostało zakończone. I który należy odnaleźć *wszystkie* hello obiekty widoczne w oknie przeglądarki są teraz obracanie!

Możesz mają tootry zmiana wersji hello i przenoszenie z wersji 2.0.0 tooversion 3.0.0 jako wykonywania, lub nawet z wersji 2.0.0 kopii tooversion 1.0.0. Odtwarzanie z limitów czasu i toomake zasady kondycji samodzielnie z nich korzystać. Podczas wdrażania klastra Azure jako tooan przeciwieństwie tooa klaster lokalny, hello parametry używane może być toodiffer. Firma Microsoft zaleca, Ustaw limity czasu hello konserwatywnie.

## <a name="next-steps"></a>Następne kroki
[Uaktualnianie aplikacji przy użyciu programu PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu PowerShell.

Kontrolowanie, jak aplikacja zostanie uaktualniony przy użyciu [parametry uaktualnienia](service-fabric-application-upgrade-parameters.md).

Uzyskania uaktualnień aplikacji zgodnych przez uczenia jak toouse [szeregowanie danych](service-fabric-application-upgrade-data-serialization.md).

Dowiedz się, jak toouse zaawansowanych funkcji podczas uaktualniania aplikacji, odnosząc się zbyt[Tematy zaawansowane](service-fabric-application-upgrade-advanced.md).

Rozwiązywania typowych problemów w aplikacji uaktualnień, odnosząc się kroki toohello [Rozwiązywanie problemów z uaktualnieniami aplikacji](service-fabric-application-upgrade-troubleshooting.md).

[image1]: media/service-fabric-application-upgrade-tutorial/upgrade7.png
[image2]: media/service-fabric-application-upgrade-tutorial/upgrade1.png
[image3]: media/service-fabric-application-upgrade-tutorial/upgrade5.png
[image4]: media/service-fabric-application-upgrade-tutorial/upgrade6.png
