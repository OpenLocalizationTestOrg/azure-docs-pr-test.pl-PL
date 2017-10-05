---
title: "Przykład MyDriving Azure IoT: skompiluj go | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji, która jest kompleksowe pokaz zaprojektować IoT system przy użyciu programu Microsoft Azure, w tym usługi Stream Analytics, Machine Learning i usługi Event Hubs."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: c2fcd6ee-3bbe-43d1-a066-dce52cc3a53d
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 06/30/2017
ms.author: harikm
ms.openlocfilehash: c4b19cc76ca11f606ca8af6b0f3277b5aa46ac5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="build-and-deploy-the-mydriving-solution-to-your-environment"></a>Skompiluj i wdróż rozwiązanie MyDriving do środowiska
MyDriving to rozwiązanie Internetu rzeczy (IoT), które zbiera dane z samochodu, przetwarza je za pomocą uczenia maszynowego, przedstawiając ją na telefonie komórkowym. Wewnętrzny składa się z różnych usług świadczonych przez Microsoft Azure. Klienci mogą mieć telefony Android, iOS i Windows 10.

Utworzyliśmy rozwiązania MyDriving, aby zapewnić możliwość tworzenia systemu IoT Rozpocznij pracę. Z [MyDriving repozytorium w usłudze GitHub](https://github.com/Azure-Samples/MyDriving), można pobrać usługi Azure Resource Manager skryptów do wdrożenia architektury zaplecza do konta platformy Azure. Od tego momentu można ponownie skonfigurować różnych usług, modyfikowania zapytań własnych danych użytkownika i tak dalej. Skrypty te — wraz z kodu dla aplikacji mobilnej, projekt interfejsu API usługi aplikacji Azure i inne — w repozytorium MyDriving można znaleźć.

Jeśli jeszcze nie nastąpiła aplikacji, obejrzyj [przewodnika Get](iot-solution-get-started.md).

Istnieje konto szczegółowe architektury w [MyDriving podręcznik](http://aka.ms/mydrivingdocs). Podsumowując istnieją kilka elementów, które skonfigurujemy do tworzenia podobnych projektu:

* A **aplikacji klienckiej** działa na telefonach z systemem Android, iOS i Windows 10. Używamy platformy Xamarin udostępnianie taki kod, który jest przechowywany w serwisie GitHub pod `src/MobileApp`. Aplikacja faktycznie wykonuje dwie różne funkcje:
  * Przekazuje on dane telemetryczne z urządzenia lokalnego Diagnostyka i własnej lokalizacji usługi zaplecza w chmurze systemu.
  * Jest interfejsu użytkownika, w którym użytkownicy mogą wyszukiwać o ich rund drogowej zarejestrowane.
* A **usługi w chmurze** wysyła strumień danych podróży drogowej w czasie rzeczywistym i przetwarza je. Główne pracy tworzenia tej usługi jest wybierz parametryzacja i połączenie się z usługami Azure. Niektóre części wymagają skryptów służących do filtrowania i przetwarzania przychodzących danych. Używamy szablonu usługi Azure Resource Manager, aby skonfigurować wszystkie części.
* A **aplikacji usługi mobilnej** to usługa sieci web za część interfejsu użytkownika aplikacji urządzenia. Swojego zadania głównego jest przetworzonych danych przechowywanych w bazie danych. Jego kod jest w witrynie GitHub pod `src/MobileAppService`.
* **Visual Studio z platformą Xamarin** jest naszych Środowisko deweloperskie. Program Xamarin, która istnieje zarówno jako część programu Visual Studio, jak i jako autonomiczny zintegrowane środowisko programistyczne (IDE), jest używany do tworzenia kodu i platform urządzeń. Aby skompilować kod z systemem iOS, należy dla wystąpienia Xamarin uruchomiona na komputerze OS X. W razie potrzeby mogą być uruchamiane jako zarządzane przy użyciu agenta, z programu Visual Studio.
* **Testy jednostkowe** urządzenia aplikacji jest wykonywane w chmury testowej Xamarin.
* **GitHub** repozytorium, w którym są przechowywane wszystkie kodu, skrypty i szablony.
* **Visual Studio Team Services** to usługa w chmurze, która jest używana do zarządzania kompilacji ciągłej i testowania aplikacji sieci web usługi i urządzenia.
* **HockeyApp** jest używana do rozpowszechniania wersjach kod urządzenia. Zbiera również awarii i użycia raporty i opinie użytkowników.
* **Visual Studio Application Insights** monitoruje usługę sieci web urządzeń przenośnych.

Tak Zobacz, jak skonfigurowanie to wszystko. 

> [!NOTE] 
> Wiele z następujących czynności są opcjonalne.
>
>

## <a name="sign-up-for-accounts"></a>Załóż kont
* [Podstawowe informacje dotyczące programu Visual Studio Dev](https://www.visualstudio.com/products/visual-studio-dev-essentials-vs.aspx). To bezpłatny program zapewnia łatwy dostęp do wielu narzędzi dla deweloperów i usług, w tym programu Visual Studio, Visual Studio Team Services i platformy Azure. Udostępnia środki na 25 miesięcznie na platformie Azure przez 12 miesięcy. Obejmuje on też subskrypcje szkolenia Pluralsight i Xamarin University. Można również założyć oddzielnie dla warstwy bezpłatna [Azure](https://azure.com) i [Visual Studio Team Services](https://www.visualstudio.com/products/visual-studio-team-services-vs.aspx), ale nie zapewniają one kredytów systemu Azure.
* [HockeyApp](https://rink.hockeyapp.net/) (opcjonalnie), do zarządzania testu dystrybucję aplikacji mobilnych i zbieranie danych telemetrycznych.
* [Xamarin](https://xamarin.com/) (wymagane), umożliwiające tworzenie aplikacji mobilnej i uruchamianie przebiegów debugowania i testy na [chmury testowej Xamarin](https://xamarin.com/test-cloud).
* [GitHub](https://github.com/Azure-Samples/MyDriving/) (opcjonalnie) utworzyć bezpłatne repozytoria publicznego własnego kodu (płatnej są prywatne repozytoria). Alternatywnie można użyć podstawowy plan w Visual Studio Team Services dla repozytoriów prywatnych.
* [Power BI](https://powerbi.microsoft.com/) (opcjonalnie) utworzyć zaawansowane wizualizacje danych w całym systemie.

> [!NOTE]
> Nie jest potrzebne konto GitHub, dostęp do kodu MyDriving w [repozytorium GitHub MyDriving](https://github.com/Azure-Samples/MyDriving).
> 
> 

## <a name="install-development-tools"></a>Zainstaluj narzędzia do programowania
Następujące ustawienia są związane z opracowywaniem pełnego rozwiązania: iOS, Android i Windows 10 Mobile zaplecza aplikacji i platform, za pomocą platformy Azure.

Alternatywnie, można Xamarin Studio na Mac lub Windows do opracowywania aplikacji mobilnych, jeśli nie działają na platformie Azure zaplecza.

Brak [dłuższy opis tej instalacji](https://msdn.microsoft.com/library/mt613162.aspx).

### <a name="windows-development-machine"></a>Komputer deweloperski systemu Windows
Narzędzie centralnej w systemie Windows jest Visual Studio do pracy z aplikacjami MyDriving dla systemów Android i Windows, projekt interfejsu API usługi aplikacji i rozszerzenia mikrousługi.

Program Xamarin, Git emulatorów i inne składniki przydatne są zintegrowane z programem Visual Studio.

Instalacja:

* [Visual Studio z platformą Xamarin](https://www.visualstudio.com/products/visual-studio-community-vs) (dowolna wersja — społeczności jest bezpłatna).
* [SQLite dla platformy uniwersalnej systemu Windows](https://visualstudiogallery.msdn.microsoft.com/4913e7d5-96c9-4dde-a1a1-69820d615936). Wymagane, aby skompilować kod systemu Windows 10 Mobile.
* [Zestaw Azure SDK dla programu Visual Studio](https://www.visualstudio.com/vs/azure-tools/). Umożliwia zestawu SDK do uruchamiania aplikacji na platformie Azure, wraz z wiersza polecenia narzędzia do zarządzania Azure.
* [Usługi Azure Service Fabric SDK](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric). Wymagane do utworzenia [mikrousługi](../service-fabric/service-fabric-get-started.md) rozszerzenia.

Upewnij się, że masz prawa rozszerzeń programu Visual Studio. Sprawdź, czy w obszarze **narzędzia**, zostanie wyświetlony **Android, iOS, Xamarin...** . Jeśli nie, Otwórz program Visual Studio, wyszukania Xamarin i postępuj zgodnie z monitami, aby go zainstalować. Ponadto sprawdź, czy **Git dla systemu Windows** jest zainstalowany. Jeśli nie, w programie Visual Studio, wyszukaj go i postępuj zgodnie z monitami, aby go zainstalować. 

### <a name="mac-development-machine"></a>Mac komputerze deweloperskim
Mac (Yosemite lub nowszym) jest wymagany, jeśli chcesz utworzyć dla systemu iOS. Chociaż korzystamy opracowanie ich i zarządzania całego kodu programu Visual Studio za pomocą platformy Xamarin w systemie Windows, Xamarin używa agent został zainstalowany na komputerze Mac, aby można było utworzyć i podpisać kod z systemem iOS.

![Tworzenie w systemie Windows i kompilacji dla komputerów Mac](./media/iot-solution-build-system/image1.png)

(Alternatywnym służy program Xamarin Studio bezpośrednio na Mac do opracowywania i platform aplikacji.)

Jeśli nie chcesz uwzględnić iOS jako platforma docelowa nie jest konieczne Mac.

Instalacja:

* [Program Xamarin Studio dla systemu iOS](https://developer.xamarin.com/guides/ios/getting_started/installation/mac/). Można również skonfigurować Visual Studio i Xamarin na komputerze Mac, działającej maszyny wirtualnej systemu Windows. Zobacz [Instalatora, instalacja i weryfikacja dla użytkowników komputerów Mac](https://msdn.microsoft.com/library/mt488770.aspx) w witrynie MSDN.
* [Narzędzia deweloperskie Azure](https://azure.microsoft.com/downloads/) (opcjonalnie).

Włączanie zdalnej nazwy logowania na komputerach Mac. Otwórz **preferencjach systemowych** > **udostępniania**, a następnie wybierz **logowania zdalnego**.

Po otwarciu projektu systemu iOS w programie Visual Studio w systemie Windows, Xamarin wtyczki wyświetli monit o identyfikator Mac.

## <a name="fetch-the-github-repository"></a>Pobierz repozytorium GitHub
Pobierz kopię lokalną [repozytorium GitHub MyDriving](https://github.com/Azure-Samples/MyDriving) za pomocą **Pobierz ZIP** przycisk w witrynie GitHub, Visual Studio lub innego klienta Git.

Rozpakuj plik do folderu o krótkiej nazwy ścieżki, takie jak C:\\kodu.

Alternatywnie Jeśli chcesz zachować na bieżąco dzięki lub przyczyniają się do naszego kodu klonowania następujący repozytorium:

**https://github.com/Azure-Samples/MyDriving.git klonowania git**

## <a name="get-a-bing-maps-api-key"></a>Pobierz klucz interfejsu API map Bing
[Zarejestruj klucz interfejsu API map Bing](https://msdn.microsoft.com/library/ff428642.aspx).

Aby zastąpić to w wierszu 22 `src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs`.

## <a name="build-the-demo-app"></a>Tworzenie aplikacji demonstracyjnej
Otwieranie tych rozwiązań w programie Visual Studio:

* src\MobileApps\MyDriving.sln
* src\MobileAppService\MyDrivingService.sln
* src\Extensions\ServiceFabric\VINLookUpApplication\VINLookUpApplication.sln

Zostanie wyświetlony monit o:

* Zaufania niektórych projektów potencjalnie niezaufanym. Wybierz, aby je otworzyć, jeśli chcesz teraz.
* Jeśli pracujesz na komputerze z systemem Windows 10 świeże, należy ustawić tryb dewelopera.
* Wprowadź swoje poświadczenia Xamarin.
* Nawiązać Xamarin komputerów Mac. Jeśli nie masz Mac, kliknij prawym przyciskiem myszy projekt iOS w programie Visual Studio, a następnie wybierz **Zwolnij projekt**.

Ponownie skompiluj rozwiązanie.

Jeśli masz problemy z tworzenia możliwe rozwiązania do Osobliwości, które znaleźliśmy:

* *VINLookupApplication projektu nie jest ładowana*: Upewnij się, że zainstalowano [zestawu Azure SDK dla programu Visual Studio](https://www.visualstudio.com/vs/azure-tools/).
* *Projekt sieci szkieletowej usług nie kompilacji*: tworzenie pierwszej kompilacji projektów interfejsu i upewnij się, że zainstalowano zestaw SDK sieci szkieletowej usług.
* *Android — aplikacja nie kompilacji*:
  
  * Otwórz **narzędzia** > **Android** > **Android SDK Manager**i upewnij się, że 6 systemu Android (interfejs API 23) / zainstalowano zestaw SDK platformy.
  * Usuń ten katalog, a następnie ponownie:<br/>
    `%LocalAppData%\Xamarin\zips`

## <a name="get-to-know-the-code"></a>Poznawanie kodu
W rozwiązaniu można znaleźć:

* Rozszerzenia Azure: sieć szkieletowa usług.
* Usługa Azure HDInsight: Skrypty do przetwarzania danych podróży na platformie Azure.
* Aplikacje mobilne: Aplikacji dla urządzeń.
* MobileAppsService/MyDrivingService: Końcowy wstecz sieci web.
* Usługa Power BI: Definicja raportu.
* Skrypty:
  
  * Menedżer zasobów: szablony do tworzenia zasobów platformy Azure.
  * Programu PowerShell: Skrypty Aby uruchomić szablony Menedżera zasobów.
  * Azure SQL Database: Debugowanie baz danych.
* Baza danych SQL: CreateTables: definicje schematów.
* Usługa Azure Stream Analytics: Zapytań, które przekształcenie przychodzącego strumienia danych.

## <a name="run-the-apps-in-development-mode"></a>Uruchamianie aplikacji w trybie projektowania
Wykonaj akcję, aby uruchomić aplikacje oparte na urządzeniu, którego używasz:

* Wewnętrzna: MyDrivingService Ustaw jako projekt startowy, a następnie naciśnij klawisz F5, aby uruchomić usługę sieci web zaplecza. Zostanie otwarty widok przeglądarki na liście interfejsu API.
* Klientów mobilnych: [aplikacji mobilnych są tworzone w programie Xamarin](https://developer.xamarin.com/guides/cross-platform/deployment,_testing,_and_metrics/debugging_with_xamarin/).
  
  * System android: Aby uzyskać więcej informacji, zobacz [debugowania dla systemu Android w programie Xamarin](http://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/debugging_with_xamarin_android/).
  * iOS: Aby uzyskać więcej informacji, zobacz [debugowania w systemie iOS](http://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/).
  * Windows Phone: Aby uzyskać więcej informacji, zobacz [Xamarin i Windows Phone](https://developer.xamarin.com/guides/cross-platform/windows/phone/).

## <a name="upload-the-mobile-app-to-hockeyapp"></a>Przekaż aplikację mobilną na platformę HockeyApp
HockeyApp zarządza dystrybucji do testowania użytkowników aplikacji systemu Android, iOS lub Windows powiadamianie użytkowników o nowych wersji. Ponadto zbiera raporty awarii przydatne, opinii użytkowników z zrzuty ekranu i metryki użycia.

[Rozpocznij od przekazywania](http://support.hockeyapp.net/kb/app-management-2/how-to-create-a-new-app) aplikacji kompilacji. Następnie zaloguj się do [HockeyApp](https://rink.hockeyapp.net) z komputerze deweloperskim. Na pulpicie nawigacyjnym developer, kliknij przycisk **nową aplikację**, a następnie przeciągnij tworzone pliki na okna. (Później, można zautomatyzować, usługi kompilacji w tym celu).

Teraz możesz w pulpicie nawigacyjnym aplikacji.

![Karta Przegląd na pulpicie nawigacyjnym aplikacji](./media/iot-solution-build-system/image2.png)

Należy powtórzyć dla każdej platformy, która aplikacja będzie działać na. Następnie można wykonać następujące czynności:

* Użyj [identyfikator aplikacji](http://support.hockeyapp.net/kb/app-management-2/how-to-find-the-app-id) na pulpicie nawigacyjnym, aby wysłać dane awarii i przesyłania opinii z aplikacji. W MyDriving należy zaktualizować identyfikatorów w src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs.
* [Zaprosić użytkowników testowych](http://support.hockeyapp.net/kb/app-management-2/how-to-invite-beta-testers). Należy uzyskać adres URL rekrutacji testerów użytkowników. One będzie można utworzyć dla zespołu, Pobierz aplikację i wysłać opinię.
* Jeśli chcesz bardziej otwarte wydania beta ustawioną publicznego dystrybucji. Kliknij przycisk **Zarządzanie aplikacją** > **dystrybucji** > **Pobierz = Public**. Każda osoba, która teraz pobrać aplikację i wysłać opinię i zostanie wyświetlone powiadomienie, gdy opublikujesz nowej wersji. Zbyt można uzyskać niektóre raporty awarii z nich.
  
   ![Zespoły na pulpicie nawigacyjnym](./media/iot-solution-build-system/image3.png)
* [Połącz raporty awarii programu Visual Studio Team Services](http://support.hockeyapp.net/kb/third-party-bug-trackers-services-and-webhooks/how-to-use-hockeyapp-with-visual-studio-team-services-vsts-or-team-foundation-server-tfs). Kliknij przycisk **Zarządzanie aplikacją** > **Visual Studio Team Services**. Platforma HockeyApp może automatycznie tworzyć elementy robocze w Team Services, jeśli raporty awarii ani otrzymania opinii.

Dowiedz się więcej o [lokacji HockeyApp](https://hockeyapp.net).

## <a name="test-the-mobile-app-on-xamarin-test-cloud"></a>Testowanie aplikacji mobilnej na chmury testowej Xamarin
[Chmury testowej Xamarin](https://developer.xamarin.com/guides/testcloud/introduction-to-test-cloud/) automatyzuje testów interfejsu użytkownika na urządzeniach rzeczywistych w chmurze. Przy użyciu NUnit framework, należy napisać testy, które Uruchom aplikację za pomocą interfejsu użytkownika.

Aby program Xamarin, możesz dołączyć do nich [Xamarin.UITests](https://developer.xamarin.com/guides/testcloud/uitest/intro-to-uitest/) zestawu SDK w aplikacji, która jest dostępna jako pakietu NuGet. Znajdziesz w aplikacja demonstracyjna, a była dostępna, tworząc nowe projekty testowe z szablonami platformy Xamarin.

![Gdzie można znaleźć zestawu SDK i platform w interfejsie](./media/iot-solution-build-system/image4.png)

Przykładowy projekt testu jest dołączony do aplikacji w repozytorium. W [MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService), sprawdź w obszarze [src](https://github.com/Azure-Samples/MyDriving/tree/master/src)/MobileApps/[MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileApps/MyDriving)/MyDriving.UITests/.

Jeśli używasz kompilacji programu Visual Studio Team Services jest ułatwia pisanie testów jednostkowych Xamarin interfejsu użytkownika i uruchom je jako część kompilacji.

## <a name="deploy-azure-services"></a>Wdrażanie usług platformy Azure
Do wykonania automatyczne wdrożenie usług kompilacji Team Services i usług Azure, można znaleźć szczegółowe instrukcje w **scripts/README.md**.

Microsoft Azure udostępnia wiele różnych usług, które służą do tworzenia aplikacji w chmurze. Mimo że wiele mogą być używane pojedynczo (takich jak aplikacje sieci Web i usługi aplikacji), są one w ich przypadku są połączone ze sobą do formularza zintegrowany system, takich jak używanym w MyDriving.

Istnieje możliwość tworzenia i ręcznie łączyć usług platformy Azure, ale jest znacznie szybsza i bardziej niezawodna do użycia usługi Azure Resource Manager szablonów. [Menedżer zasobów](../azure-resource-manager/resource-group-overview.md) automatyzuje wdrażania rozwiązania zasobów oraz tworzenie połączenia między nimi.

Szablon dla systemu MyDriving znajdziesz w repozytorium serwisu GitHub, w obszarze [skryptów/ARM](https://github.com/Azure-Samples/MyDriving/tree/master/scripts/ARM). Zapewnia kompleksowe i zwięzły widok jak są połączone ze sobą różnych usług w naszym architektury. Prezentujemy zasady tych szczegółowo w [MyDriving podręcznik](http://aka.ms/mydrivingdocs), ale Dowiedz się wiele wystarczy odczytu za pomocą szablonu.

> [!NOTE]
> Najbardziej Azure usługi mają skojarzone koszt, w zależności od warstwy cenowej. Jeśli jesteś nowym użytkownikiem usługi Azure, możesz [bezpłatnie wypróbowanie](https://azure.microsoft.com/free/). Jednak jeśli nie zamierzasz korzystać z niektórych składników w systemie MyDriving, należy usunąć je, aby uniknąć ponoszenia kosztów. W sekcji "Oszacowanie kosztów operacyjnych" w dalszej części tego artykułu zawiera podsumowanie typowych usługi kosztów.
> 
> 

### <a name="edit-the-template"></a>Edytowanie szablonu
Aby dostosować wdrożenia, być może usunąć niepotrzebne składniki lub dodać inne, najpierw kopie scenariusza\_complete.params.json oraz scenariusz\_complete.json, w którym można wprowadzić zmiany.

Można użyć tego scenariusza\_complete.params.json pliku do przesłonięcia różnych wartości domyślnych, takich jak usługa SKU lub typ replikacji magazynu, zgodnie z opisem w poniższej tabeli. Wartości domyślne opcje najniższy koszt.

| **Parametr** | **Opis** | **Wartość domyślna** |
| --- | --- | --- |
| Centrum IoT jednostki SKU |Warstwy usługi Centrum IoT Azure |F1 |
| Typ konta magazynu |Typ replikacji magazynu |Standard-LRS |
| Cel usługi SQL |Użycie miejsca współbieżności |DW100 |
| Plan hostingu jednostki SKU |Plan usługi App Service |F1 |

W scenariuszu\_complete.json:

* Wyszukaj nazwę "bazową" i zmień jego nazwę preferowanego.
* Wyszukaj "Utwórz". Każda z tych sekcji tworzy zasób.
* Ustaw sqlServerAdminLogin i sqlServerAdminPassword odpowiednie wartości.
* Przed usunięciem sekcja, która tworzy zasób, sprawdź, czy ma zależności, wyszukując swojej nazwy w innym miejscu w pliku. Należy pamiętać, że każda sekcja, która tworzy usługę obejmuje *dependsOn* sekcji, która zawiera jego zależności.

Oto konfiguruje szablon. Szczegółowe informacje znajdują się w [podręcznik](http://aka.ms/mydrivingdocs).

| **Usługa** | **Opis i szczegóły** |
| --- | --- |
| Konta magazynu |Szablon tworzy trzy konta: |
| -Bazy danych SQL odbiera zagregowane dane telemetryczne z usługi Stream Analytics, która służy jako magazynu zapasowego dla tabel Azure App Service, z użyciem tych danych za pośrednictwem punkty końcowe interfejsu API. | |
| — Magazyn obiekt blob, która gromadzi dane historyczne z innego zadania Stream Analytics, do przetworzenia przez usługi HDInsight. | |
| -Bazy danych SQL służącą do odbierania wyników przetworzone przez HDInsight do użycia z usługą Power BI. | |
| Azure IoT Hub |Ustanawia połączenie dwukierunkowe każdego podłączonego urządzenia. W rozwiązaniu MyDriving aplikacji mobilnej działa jak brama pola do wysyłania danych do Centrum IoT Azure. Centrum IoT Azure następnie służy jako dane wejściowe do usługi Stream Analytics. |
| Azure Event Hubs |Dane wyjściowe do zadania usługi analiza strumienia kolejki danych wyjściowych do rozszerzeń, które zostały utworzone z sieci szkieletowej usług Azure. |
| Azure SQL Data Warehouse | |
| Zadania usługi analiza strumienia |Uzyskuj dostęp do danych wejściowych i wyjściowych kwerendę, która służy do agregacji zarówno w czasie rzeczywistym i historycznych danych dla aplikacji interfejsów API usługi Service, usługi Azure Machine Learning, rozszerzenia i usługi Power BI. |
| Obszaru roboczego uczenia maszyny |Obejmuje eksperymentów, kod języka R i usługi interfejsu API. |
| Azure Data Factory |Zaplanowanego ponownego trenowania uczenia maszynowego. |
| Plan hostingu w sieci szkieletowej usług |Dla rozszerzenia. |
| Usługi aplikacji ("aplikacji mobilnej") |Obsługuje projekt interfejsu API aplikacji mobilnej, który udostępnia punktów końcowych dla aplikacji mobilnej. W kodzie interfejsu API należy wdrożyć w aplikacji usługi z programu Visual Studio. |
| Reguły alertów |Wysyła wiadomości e-mail, jeśli błędy wskazują odpowiedzi aplikacji. |
| Application Insights |Do monitorowania wydajności interfejsów API w usłudze App Service. Należy skonfigurować połączenie w programie Visual Studio. |
| W usłudze Azure Key Vault |Aby zapisać certyfikat klastra usługi sieci web. |

### <a name="run-the-template"></a>Uruchom szablon
W **scripts/README.md**, są szczegółowe instrukcje dotyczące uruchamiania szablonu.

Aby udostępnić te usługi w konta Azure za pomocą skryptu, wykonaj jedną z następujących czynności:

* Za pomocą programu PowerShell:
  
  ```
  
  cd scripts/PowerShell;
  deploy.ps1 *location* *resourceGroupName*
  ```
  
  * *Lokalizacja* jest [lokalizacji platformy Azure](https://azure.microsoft.com/regions/), takich jak `North Europe` lub `West US`. Użyj `Get-AzureLocation` można znaleźć listę dostępnych lokalizacji.
  * *resourceGroupName* to nazwa, która ma zostać nadana do wszystkich zasobów będą należeć do grupy. Po zakończeniu z zasobami, usunąć je wszystkie razem przez usunięcie tej grupy.
* Uruchom DeploymentScripts/Bash/deploy.sh z Bash.
* Otwórz i rozwiązania Visual Studio DeploymentScripts/VS/DeployARM.sln kompilacji.

Należy pamiętać, że każdym uruchomieniu szablon tworzy nowy zestaw zasobów pod inną nazwą. Aby usunąć zasoby, przejdź do portalu i Usuń grupę zasobów.

Jeśli skrypt nie powiedzie się z jakiegokolwiek powodu, można ponownie uruchomić.

Skrypt udostępnia opcję konfigurowania integracji ciągłej w Visual Studio Team Services. Jeśli w projekcie usługi Team Services, będziesz mieć adres URL: https://yourAccountName.visualstudio.com. Gdy pojawi się monit, wprowadź pełny adres URL. Można nadać mu nazwę nowego lub istniejącego projektu Team Services.

## <a name="set-up-build-and-test-definitions-in-visual-studio-team-services"></a>Konfigurowanie kompilacji i testowania definicje w Visual Studio Team Services
Firma Microsoft korzystania z usług zespołu nad tym projektem przede wszystkim na jego kompilacji i przetestować funkcje. Ale również zapewnia doskonałą współpracy pomocy technicznej, takich jak zadania zarządzania za pomocą tablic Kanban, kompilacje przeglądu kodu zintegrowane z zadaniami i kontroli źródła i warunkowych. Integruje się również przy użyciu innych narzędzi, takich jak GitHub, Xamarin HockeyApp i oczywiście Visual Studio. Można do niego dostęp za pośrednictwem interfejsu sieci web lub za pomocą programu Visual Studio, w zależności jest wygodniejsze w dowolnym momencie.

Kroki opisane w definicji kompilacji i wydania użycia różnych usług wtyczki, które są dostępne w programie Team Services [Marketplace](https://marketplace.visualstudio.com/VSTS). Oprócz podstawowych funkcji uruchamiających wiersze polecenia lub kopiować pliki istnieją usług, który wywołania kompilacje Xamarin, Android i innych dostawców, a które łączyć na platformę HockeyApp.

![Opcje w Team Services kompilacji](./media/iot-solution-build-system/image5.png)

### <a name="build-definitions"></a>Definicje kompilacji
Mamy definicje kompilacji dla poszczególnych głównych celów. Mamy także odchyleń dla funkcji i testowania regresji. Daje:

* MyDriving.Services (aplikacja sieci web zaplecza aplikacji mobilnej)
* MyDriving.Xamarin.Android
  
  * MyDriving.Xamarin.Android — funkcja
  * Regresja MyDriving.Xamarin.Android
* MyDriving.Xamarin.iOS
  
  * MyDriving.Xamarin.iOS — funkcja
  * Regresja MyDriving.Xamarin.iOS
* MyDriving.Xamarin.UWP
  
  * MyDriving.Xamarin.UWP — funkcja
  * Regresja MyDriving.Xamarin.UWP

Jeśli chcesz wyświetlić szczegółowe informacje dotyczące naszych konfiguracji, zobacz sekcję 4.7 [MyDriving podręcznik](http://aka.ms/mydrivingdocs), "Kompilacji i konfiguracji wydania". One wykonują te same czynności ogólne. Skrypt:

1. Przywraca pakietu NuGet. Nie możemy przechowuj skompilowanego kodu repozytorium, aby przywrócić wymagane pakiety NuGet co pierwsze kroki każdej kompilacji.
2. Aktywuje licencję. Kompilacja jest wykonywane w chmurze, więc w przypadku, gdy potrzebna licencja — w szczególności kompilacji usługi Xamarin — mamy aktywować naszych licencji na bieżącym komputerze kompilacji. Następnie możemy zdezaktywować natychmiast później, aby umożliwić jego ma zostać użyty na innym komputerze.
3. Tworzy się przy użyciu odpowiedniej usługi. Używamy kompilacje platformy Xamarin dla aplikacji mobilnych, i Visual Studio tworzy dla usługi sieci web zaplecza.
4. Tworzy testy.
5. Uruchamia testy. Firma Microsoft Uruchom testy aplikacji mobilnej z chmury testowej Xamarin.
6. Publikuje wyniki kompilacji do lokalizacji docelowej.

Wyzwalacz dla głównego kompilacji jest ustawiony na ciągłą integrację. Oznacza to kompilacja jest uruchamiane za każdym razem, gdy kod jest zaewidencjonowane do gałęzi głównej.

![Interfejs którego wyzwalacz ustawiono ciągłej integracji](./media/iot-solution-build-system/image6.png)

### <a name="release-definitions"></a>Definicji wersji
Definicji wersji są ustawiane w taki sam sposób.

Usługi sieci web skonfigurowanie wdrożenia jako aplikacja sieci web platformy Azure:

![Interfejs na potrzeby konfigurowania wdrażania aplikacji sieci web platformy Azure](./media/iot-solution-build-system/image7.png)

I możemy ustawić wyzwalacz wersji do ciągłego wdrażania. Oznacza to, co zaewidencjonowania następuje pomyślnego utworzenia kompilacji spowoduje aktualizację do aplikacji sieci web.

![Interfejs do ustawiania wyzwalacza wersji ciągłe wdrażanie](./media/iot-solution-build-system/image8.png)

Dla aplikacji mobilnych możemy wdrożyć na platformę HockeyApp:

![Interfejs do wdrażania aplikacji mobilnej do aplikacji HockeyApp](./media/iot-solution-build-system/image9.png)

## <a name="explore-telemetry-by-using-application-insights"></a>Eksploruj dane telemetryczne za pomocą usługi Application Insights
[Usługa Application Insights](../application-insights/app-insights-overview.md) zbiera dane telemetryczne dotyczące wydajności i użycia usług sieci web. Zestaw SDK usługi Application Insights wysyła dane telemetryczne z usługi do zasobu usługi Application Insights na platformie Azure.

Przejdź do zasobu usługi Application Insights, skonfigurowanego szablonu. Istnieje, można eksplorować wykresy wydajności z [projekt usługi mobilnej aplikacji](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService). Pokazują one żądań serwera i czasy odpowiedzi, błędów, i liczby wyjątków. Dostępne są także wykresy zależności czasy odpowiedzi — to znaczy wywołania do bazy danych i interfejsów API REST, takich jak Machine Learning. Jeśli występują problemy z wydajnością, będzie można zobaczyć, jakie części systemu powoduje ich.

![Wykres wydajności przykład](./media/iot-solution-build-system/image11.png)

Jeśli masz usługi sieci web skonfigurowanej ręcznie jest łatwo uzyskać tego samego wykresy. W bloku usługi sieci web, kliknij polecenie **narzędzia** > **rozszerzenia** > **Dodaj**. Wybierz **usługi Application Insights**.

![Interfejs wybierania Application Insights, aby pobrać wykresy](./media/iot-solution-build-system/image12.png)

Ta funkcja działa przez instrumentacji aplikacji przy użyciu zestawu SDK usługi Application Insights.

Możesz dodać niestandardowe dane telemetryczne (lub Instrumentacji aplikacji, która jest uruchomiona w innym poza Azure) przez [Dodawanie zestawu SDK usługi Application Insights](../application-insights/app-insights-asp-net.md) w czasie opracowywania. Jest to przydatne do dziennika metryki, które są zależne od aplikacji, takie jak długość średni podróży użytkowników lub całkowita przebiegu. W programie Visual Studio, kliknij prawym przyciskiem myszy projekt, a następnie wybierz **Dodaj usługę Application Insights**.

![Interfejs wybierania Dodaj usługę Application Insights można dodać telemetria niestandardowa](./media/iot-solution-build-system/image10.png)

Usługi Application Insights będzie wysyłać wiadomości e-mail alertów, jeśli nietypowe liczby odpowiedzi. Można również skonfigurować alerty na różnych metryk, takich jak czas odpowiedzi.

Tylko w celu upewnij się, że usługi sieci web jest zawsze aktualne i działa, możesz skonfigurować [testów dostępności](../application-insights/app-insights-monitor-web-app-availability.md). Te testy ping witryny z różnych lokalizacji na całym świecie, co 15 minut. Ponownie otrzymasz wiadomość e-mail, jeśli wystąpił problem.

## <a name="estimate-operational-costs"></a>Szacowanie kosztów operacyjnych
Jest to niezwykle niedrogich do uruchomienia aplikacji, takich jak ta na małą skalę. Wiele usług mają bezpłatnej warstwy klasy podstawowej, więc rozwoju i operacji na małą skalę koszt niewielkie. I oczywiście własnych aplikacji nie ma możliwości korzystania z funkcji zostało to pokazane w MyDriving.

Oto oszacowanie koszty w procesie konfigurowania konfiguracji Programowanie MyDriving. Firma Microsoft należy również zauważyć pewne rozwiązań alternatywnych, które robiliśmy *nie* użycia. Te informacje mogą być przydatne Szacowanie własnych kosztów.

Przyjęto założenie:

* Zespół nie więcej niż pięć (oraz obserwowania uczestnicy projektu).
* Uruchomiony około miesiąca.
* 100 użytkowników z czterech rund na dzień.

> [!NOTE]
> Jeśli jesteś nowym użytkownikiem usługi Azure, Brak [bezpłatne konto](https://azure.microsoft.com/free/).
> 
> 

| **Składnik/usługi** | **Uwagi** | **Koszt miesięcznie** |
| --- | --- | --- |
| [Visual Studio 2015 Community](https://www.visualstudio.com/products/visual-studio-community-vs) z [Xamarin](https://visualstudiogallery.msdn.microsoft.com/dcd5b7bd-48f0-4245-80b6-002d22ea6eee) <br/>Środowiska deweloperskiego między platformami |Visual Studio Community. (Należy [Visual Studio Professional](https://www.visualstudio.com/vs-2015-product-editions) dla [platformy Xamarin.Forms](https://xamarin.com/forms), projektowanie i platform ze ścieżki bazowej kodu pojedynczego.) |$0 |
| [Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/) <br/>Połączenie danych dwukierunkowe na urządzeniach |8000 wiadomości + 0,5 KB/komunikat zwolnienia. |$0 |
| [Stream Analytics](https://azure.microsoft.com/pricing/details/stream-analytics/)  <br/>   Przetwarzanie danych dużych strumienia |Opłata 0,031 $ na przesyłanie strumieniowe jednostki na godzinę, podczas włączania. Wybierz liczbę jednostek przesyłania strumieniowego, które mają; więcej informacji na temat skalowanie w górę. |$23 |
| [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)<br/> Adaptacyjną odpowiedzi |$10 stanowisko/miesięcznie. <br/>                                                                                                                                                                                 + 3-godzinnym eksperymentu \* $1 / eksperymentu godzinę. <br/>                                                                                                                                                           + Procesora interfejsu API 3.5-godzinnym \* $2 / godzina produkcji procesora CPU. <br/>                                                                                                                                                          Czas procesora CPU interfejsu API zakłada 5 min/dzień ponownego trenowania, chociaż może to spowodować dane wejściowe.                   <br/>                                                                                                                                                                     + 2 min/dzień oceniania przetworzyć 400 rund/dzień. |$20 |
| [App Service](https://azure.microsoft.com/pricing/details/app-service/)  <br/> Host dla przenośnych zaplecza |Warstwy B1 — aplikacji sieci web w środowisku produkcyjnym. |$56 |
| [Visual Studio Team Services](https://azure.microsoft.com/pricing/details/visual-studio-team-services/)  <br/> Tworzenie testu jednostkowego i zarządzania zleceniami; Zarządzanie zadaniami |Prywatne agentów pięciu użytkowników. |$0 |
| [Usługa Application Insights](https://azure.microsoft.com/pricing/details/application-insights/) <br/>Monitorowanie wydajności i użycia usług sieci web i witryn |Warstwa bezpłatna. |$0 |
| [Platforma HockeyApp](http://hockeyapp.net/pricing/) <br/> Dystrybucji aplikacji w wersji beta i zbierania opinii, użycia i dane awarii |Dwa bezpłatne aplikacje dla nowych użytkowników.<br/> $30/ miesiąc później. |$0 |
| [Xamarin](https://store.xamarin.com/)<br/> Kod na platformie uniform dla wielu urządzeń |Bezpłatna wersja próbna. <br/>25 miesięcznie później. |$0 |
| [Baza danych SQL](https://azure.microsoft.com/pricing/details/sql-database/) dla usługi aplikacji Azure |Warstwa podstawowa; model pojedynczej bazy danych. |$5 |
| [Sieć szkieletowa usług](https://azure.microsoft.com/pricing/details/service-fabric/) (opcjonalnie) |Uruchom klaster lokalny. |$0 |
| [Power BI](https://powerbi.microsoft.com/pricing/)<br/> Wyświetla elastyczne i badanie danych strumienia i statyczne |Warstwa bezpłatna: 1 GB, 10 000 wierszy na godzinę, codziennie odświeżania. <br/> $10 użytkownika/miesięcznie dla [wyższe limity](https://powerbi.microsoft.com/documentation/powerbi-power-bi-pro-content-what-is-it/), więcej opcji połączenia, współpracy. |$0 |
| [Storage](https://azure.microsoft.com/pricing/details/storage/) |L (magazyn lokalnie nadmiarowy) &lt; 100 G 0.024 $/ GB. |$3 |
| [Fabryka danych](https://azure.microsoft.com/pricing/details/data-factory/) |$: 0,60 na działanie \* (FOC 8-5). |$2 |
| [HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/) <br/>  Codzienne ponownego trenowania klastra na żądanie |Trzy węzły A3 na godzinę 0.32 $ 1 godziny dziennie * 31 dni. |$30 |
| [Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/) |Podstawowy z jednostki przepływności miesięcznie 11 $ + $0,028 transfer danych przychodzących. |$11 |
| Klucz diagnostycznego | |$12 |
| **Całkowita liczba** | |**$157** |

Aby uzyskać więcej informacji, zobacz:

* Podsumowanie [usługi Azure przydziały i limity](../azure-subscription-service-limits.md#iot-hub-limits)
* Azure [Kalkulator cen](https://azure.microsoft.com/pricing/calculator/)

## <a name="send-us-your-feedback"></a>Wysyłanie opinii
Ponieważ systemy IoT utworzyliśmy MyDriving ułatwiające Rozpocznij pracę chcemy pewnością poznać Twoją opinię o tym, jak działa. Daj nam znać, jeśli:

* Wystąpiły problemy lub wyzwania.
* Brak punktu rozszerzenia, że będą bardziej odpowiednie do realizowanego scenariusza.
* Możesz znaleźć bardziej wydajny sposób wykonywania określonych potrzeb.
* Masz inne sugestie dotyczące poprawiania MyDriving lub niniejszej dokumentacji.

Aby przekazać opinię, plików [problem w usłudze GitHub] lub zostaw komentarz poniżej (en-us edition).

Czekamy na przesłuchanie od Ciebie!

## <a name="next-steps"></a>Następne kroki
Firma Microsoft zaleca [MyDriving podręcznik](http://aka.ms/mydrivingdocs), która jest kompleksowy opis projektu systemu i jej składniki.

