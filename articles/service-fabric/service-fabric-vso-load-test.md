---
title: "aaaLoad przetestować aplikację za pomocą programu Visual Studio Team Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toostress test aplikacji sieci szkieletowej usług Azure przy użyciu programu Visual Studio Team Services."
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: fc743585-0d1b-483f-981d-493f4552ac07
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 663cf8db5e8f0a4d0d7f27b585645d7f776392f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-test-your-application-by-using-visual-studio-team-services"></a>Aplikacja testu obciążenia za pomocą programu Visual Studio Team Services
W tym artykule opisano, jak toostress testu obciążenia toouse programu Microsoft Visual Studio w funkcji testowania aplikacji. Używa usługi Azure Service Fabric usługi stanowej zaplecza i usługi bezstanowej frontonu sieci web. Witaj przykładowej aplikacji używane w tym miejscu jest samolotowy symulatora lokalizacji. Musisz podać identyfikator samolotowy, czas wyjścia i docelowej. Witaj zaplecza aplikacji przetwarza hello żądania, i wyświetla frontonu hello na samolotowy hello mapy, które spełniają kryteria hello.

Witaj poniższym diagramie przedstawiono hello sieci szkieletowej usług aplikacji, która będzie testowania.

![Diagram hello przykład samolotowy lokalizacja aplikacji][0]

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem pracy należy toodo hello poniżej:

* Uzyskaj konto usługi Visual Studio Team Services. Możesz ją uzyskać, za darmo w [Visual Studio Team Services](https://www.visualstudio.com).
* Pobierz i zainstaluj program Visual Studio 2013 lub Visual Studio 2015. W tym artykule korzysta z wersji programu Visual Studio Enterprise 2015, ale programu Visual Studio 2013 i inne wersje powinny działać podobnie.
* Wdrażanie sieci tooa aplikacji przemieszczania środowiska. Zobacz [jak tooa aplikacji toodeploy zdalnego klastra przy użyciu programu Visual Studio](service-fabric-publish-app-remote-cluster.md) informacje na temat.
* Zrozumienie wzorca użycia aplikacji. Te informacje są wzorca obciążenia hello toosimulate używane.
* Zrozumienie celem hello na potrzeby testów obciążenia. Dzięki temu można zinterpretować i analizowanie wyników testów obciążenia hello.

## <a name="create-and-run-hello-web-performance-and-load-test-project"></a>Tworzenie i uruchamianie projektu hello wydajności sieci Web i testów obciążenia
### <a name="create-a-web-performance-and-load-test-project"></a>Tworzenie projektu wydajności sieci Web i testów obciążenia
1. Otwórz program Visual Studio 2015. Wybierz **pliku** > **nowy** > **projektu** hello menu tooopen hello **nowy projekt** okno dialogowe.
2. Rozwiń węzeł hello **Visual C#** węzeł i wybierz polecenie **testu** > **wydajności sieci Web i testów obciążenia projektu**. Nadaj nazwę hello projektu, a następnie wybierz pozycję hello **OK** przycisku.

    ![Zrzut ekranu: okno dialogowe Nowy projekt hello][1]

    Powinien zostać wyświetlony nowy projekt wydajności sieci Web i testów obciążenia w Eksploratorze rozwiązań.

    ![Zrzut ekranu przedstawiający Eksploratora rozwiązań przedstawiający hello nowy projekt][2]

### <a name="record-a-web-performance-test"></a>Rekord testu wydajności sieci web
1. Otwórz hello .webtest projektu.
2. Wybierz hello **dodać rejestrowania** ikona toostart sesję rejestrowania w przeglądarce.

    ![Zrzut ekranu przedstawiający hello Dodaj nagranie ikony w przeglądarce][3]

    ![Zrzut ekranu przedstawiający przycisk rekordu hello w przeglądarce][4]
3. Przeglądaj toohello sieci szkieletowej usług aplikacji. panel rejestrowania Hello powinny być widoczne hello żądań sieci web.

    ![Zrzut ekranu przedstawiający żądań sieci web w hello rejestrowania panelu][5]
4. Wykonaj sekwencję akcji spodziewać się hello tooperform użytkowników. Te akcje są używane jako wzorzec obciążenia hello toogenerate.
5. Gdy wszystko będzie gotowe, wybierz hello **zatrzymać** przycisk toostop rejestrowania.

    ![Zrzut ekranu przedstawiający przycisk zatrzymywania hello][6]

    seria żądań powinien przechwycone Hello .webtest projektu programu Visual Studio. Parametry dynamiczne są zastępowane automatycznie. W tym momencie można usunąć wszelkie zależności dodatkowe, powtarzane żądania nie są częścią Twojego scenariusza testu.
6. Zapisz hello projektu, a następnie wybierz pozycję hello **Uruchom Test** wydajności sieci web hello toorun polecenia testowanie lokalnie i upewnij się, że wszystko działa prawidłowo.

    ![Zrzut ekranu przedstawiający hello polecenie uruchomienia testu][7]

### <a name="parameterize-hello-web-performance-test"></a>Parametryzacja testu wydajności sieci web hello
Parametryzacja z testów wydajności sieci web hello, konwersją testu wydajności sieci web tooa na stałe, a następnie edytując kod hello. Alternatywnie można powiązać lista danych tooa testu wydajności sieci web hello tak, aby hello testu iteruje hello danych. Zobacz [Generowanie i Uruchamianie testów wydajności sieci web kodowane](https://msdn.microsoft.com/library/ms182552.aspx) szczegółowe informacje o sposobie tooconvert hello web wydajności testu tooa kodowanego testu. Zobacz [Dodaj testu wydajności sieci web tooa źródła danych](https://msdn.microsoft.com/library/ms243142.aspx) dla informacji na temat sposobu wydajności sieci web tooa danych toobind testu.

Na przykład będzie przekonwertować testu tooa kodowanego testu wydajności sieci web hello, można zastąpić identyfikator samolotowy hello generowanym identyfikatorze GUID lub dodawać więcej żądań toosend lotach toodifferent lokalizacji.

### <a name="create-a-load-test-project"></a>Tworzenie projektu testu obciążenia
Projekt testowy obciążenia składa się z co najmniej jeden z opisanych testu wydajności sieci web hello i testu jednostkowego, wraz z ustawień testu obciążenia dodatkowych scenariuszy. Witaj następujące kroki pokazują, jak projekt testowy toocreate obciążenia:

1. W menu skrótów hello projektu wydajności sieci Web i testów obciążenia, wybierz **Dodaj** > **testu obciążenia**. W hello **testu obciążenia** kreatora wybierz hello **dalej** przycisk ustawień testu hello tooconfigure.
2. W hello **wzorzec obciążenia** sekcji, wybierz, czy chcesz obciążenia stałej użytkownika lub obciążenia krok, który rozpoczyna się od kilku użytkowników i zwiększa hello użytkowników w czasie.

    Jeśli korzystasz z dobrym oszacowanie hello ilość obciążenie użytkownikami i chcesz toosee sposób wykonywania hello bieżącego systemu, wybierz **załadować stałej**. Jeśli celem jest toolearn, czy hello system spójnie przeprowadza przy różnych obciążeniach, wybierz **obciążenia krok**.
3. W hello **testu mieszanego** wybierz hello **Dodaj** przycisk, a następnie wybierz opcję hello testów, które mają tooinclude w teście obciążenia hello. Można użyć hello **dystrybucji** kolumny toospecify hello procent całkowitej testów dla każdego z testów.
4. W hello **parametrów uruchomieniowych** Określ czas trwania testu obciążenia hello.

   > [!NOTE]
   > Witaj **iteracje testu** opcja jest dostępna tylko po uruchomieniu testu obciążenia lokalnie za pomocą programu Visual Studio.
   >
   >
5. W hello **lokalizacji** sekcji **parametrów uruchomieniowych**, określ lokalizację hello, w których są generowane żądań testu obciążenia. Kreator Hello może monitować toolog w tooyour konta usługi Team Services. Zaloguj się, a następnie wybierz lokalizację geograficzną. Gdy wszystko będzie gotowe, wybierz hello **Zakończ** przycisku.
6. Po utworzeniu testu obciążenia hello Otwórz hello .loadtest projektu i wybierz polecenie Uruchom ustawienia, takie jak bieżące hello **parametrów uruchomieniowych** > **Settings1 Uruchom [Active]**. Zostanie otwarta ustawienia hello Uruchom hello **właściwości** okna.
7. W hello **wyniki** sekcji hello **parametrów uruchomieniowych** okna właściwości, hello **magazynowania szczegółów chronometrażu** powinien mieć ustawienie **Brak** jako wartość domyślną. Zmień tę wartość za**wszystkie szczegóły poszczególnych** tooget więcej informacji na temat wyników testów obciążenia hello. Zobacz [testowania obciążenia](https://www.visualstudio.com/load-testing.aspx) uzyskać więcej informacji o jak przetestować tooVisual tooconnect Studio Team Services i uruchom obciążenia.

### <a name="run-hello-load-test-by-using-visual-studio-team-services"></a>Uruchamianie testu obciążenia hello przy użyciu programu Visual Studio Team Services
Wybierz hello **uruchomienia testu obciążenia** uruchomienia testu hello toostart polecenia.

![Zrzut ekranu przedstawiający hello polecenie uruchomienia testu obciążenia][8]

## <a name="view-and-analyze-hello-load-test-results"></a>Wyświetlanie i analizowanie wyników testów obciążenia hello
Jako hello załadować realizowany test, informacje o wydajności hello jest wyświetlone na wykresie. Powinny pojawić się coś podobnego toohello po wykresu.

![Zrzut ekranu przedstawiający wykres wydajności dla wyników testu obciążenia][9]

1. Wybierz hello **Pobierz raport** łącze górze hello hello strony. Po pobraniu raportu hello wybierz hello **wyświetlić raport** przycisku.

    Na powitania **wykres** są widoczne wykresy różnych liczników wydajności. Na powitania **Podsumowanie** karcie hello ogólne wyniki testu są wyświetlane. Witaj **tabel** karcie są wyświetlane hello całkowita liczba testów obciążenia przekazany i nie powiodło się.
2. Wybierz numer łącza hello na powitania **testu** > **** i hello **błędy** > **liczba** kolumn Szczegóły błędu toosee.

    Witaj **szczegółów** karcie są wyświetlane wirtualnego testu scenariusza informacji o użytkownikach i niepomyślnych żądań. Może to być przydatne, jeśli test obciążenia hello zawiera wiele scenariuszy.

Zobacz [analizowanie załadować wyników testu w widoku wykresu analizatora testu obciążenia hello hello](https://www.visualstudio.com/load-testing.aspx) Aby uzyskać więcej informacji o wyświetlaniu obciążenia wyniki testu.

## <a name="automate-your-load-test"></a>Automatyzowanie testów obciążenia
Visual Studio Team Services testu obciążenia udostępnia interfejsy API toohelp zarządzania testami obciążenia i analiza wyników w ramach konta usługi Team Services. Zobacz [API Rest testowania obciążenia chmury](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) Aby uzyskać więcej informacji.

## <a name="next-steps"></a>Następne kroki
* [Monitorowanie i diagnozowanie usług w Instalatorze programowanie komputera lokalnego](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[0]: ./media/service-fabric-vso-load-test/OverviewDiagram.png
[1]: ./media/service-fabric-vso-load-test/NewProjectDialog.png
[2]: ./media/service-fabric-vso-load-test/Project.png
[3]: ./media/service-fabric-vso-load-test/AddRecording.png
[4]: ./media/service-fabric-vso-load-test/AddRecording2.png
[5]: ./media/service-fabric-vso-load-test/ActionSequence.png
[6]: ./media/service-fabric-vso-load-test/StopRecording.png
[7]: ./media/service-fabric-vso-load-test/RunTest.png
[8]: ./media/service-fabric-vso-load-test/RunTest2.png
[9]: ./media/service-fabric-vso-load-test/Graph.png
