---
title: "Przykład MyDriving Azure IoT: skompiluj go | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji, która jest kompleksowe pokaz tooarchitect system IoT przy użyciu programu Microsoft Azure, w tym usługi Stream Analytics, Machine Learning i usługi Event Hubs."
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
ms.openlocfilehash: e78571225697f745fe011c722e57c8600704c392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-hello-mydriving-solution-tooyour-environment"></a>Tworzenie i wdrażanie hello MyDriving rozwiązania tooyour środowiska
MyDriving to rozwiązanie Internetu rzeczy (IoT), które zbiera dane z samochodu, przetwarza je za pomocą uczenia maszynowego, przedstawiając ją na telefonie komórkowym. wewnętrzna Hello składa się z różnych usług świadczonych przez Microsoft Azure. Witaj klienci mogą mieć telefony Android, iOS i Windows 10.

Utworzyliśmy hello MyDriving rozwiązania toogive możesz Rozpocznij pracę w tworzeniu systemu IoT. Z hello [MyDriving repozytorium w usłudze GitHub](https://github.com/Azure-Samples/MyDriving), możesz uzyskać skryptów usługi Azure Resource Manager toodeploy hello zaplecza architektury do konta platformy Azure. Od tego momentu można ponownie skonfigurować hello różnych usług, modyfikowania toosuit zapytania hello danych użytkownika i itd. Skrypty te — wraz z kodu dla aplikacji mobilnej hello, projekt interfejsu API usługi aplikacji Azure hello i inne — w repozytorium MyDriving hello można znaleźć.

Jeśli jeszcze nie nastąpiła aplikacji hello, obejrzyj hello [przewodnika Get](iot-solution-get-started.md).

Istnieje konto szczegółowe architektury hello w hello [MyDriving podręcznik](http://aka.ms/mydrivingdocs). Podsumowując, są klasyfikować czy skonfigurujemy toocreate podobnego projektu:

* A **aplikacji klienckiej** działa na telefonach z systemem Android, iOS i Windows 10. Używamy tooshare platformy Xamarin hello dużo hello kodu, który jest przechowywany w serwisie GitHub pod `src/MobileApp`. Aplikacja Hello faktycznie wykonuje dwie różne funkcje:
  * Przekazuje on dane telemetryczne z urządzenia lokalnego Diagnostyka hello i zaplecza w chmurze własnej lokalizacji usługi toohello systemu.
  * Jest interfejsu użytkownika, w którym użytkownicy mogą wyszukiwać o ich rund drogowej zarejestrowane.
* A **usługi w chmurze** wysyła strumień danych podróży drogowej hello w czasie rzeczywistym i przetwarza je. Hello głównego pracy tworzenia tej usługi jest toochoose parametryzacja i połączenie się z usługami Azure. Niektóre z części hello wymagają skryptów toofilter i przetwarzanie hello przychodzących danych. Używamy tooconfigure szablonu usługi Azure Resource Manager wszystkie części hello.
* A **aplikacji usługi mobilnej** to usługa sieci web hello za część interfejsu użytkownika hello hello aplikacji urządzenia. Swojego zadania głównego jest bazą danych hello tooquery przechowywanych, przetworzonych danych. Jego kod jest w witrynie GitHub pod `src/MobileAppService`.
* **Visual Studio z platformą Xamarin** jest naszych Środowisko deweloperskie. Program Xamarin, która istnieje zarówno jako część programu Visual Studio, jak i jako autonomiczny zintegrowane środowisko programistyczne (IDE), jest używany kod obsługujący wiele platform urządzenia hello toobuild. toobuild hello iOS kodu, jest konieczne toohave wystąpienia Xamarin uruchomiona na komputerze OS X. W razie potrzeby mogą być uruchamiane jako zarządzane przy użyciu agenta, z programu Visual Studio.
* **Testy jednostkowe** urządzenia hello aplikacji jest wykonywane w chmury testowej Xamarin.
* **GitHub** hello repozytorium, gdzie są przechowywane wszystkie hello kodu, skrypty i szablony.
* **Visual Studio Team Services** to usługa w chmurze, która została użyta kompilacji ciągłej hello toomanage i testu sieci web hello aplikacje usługi i urządzenia.
* **HockeyApp** jest toodistribute używane wersje hello kod urządzenia. Zbiera również awarii i użycia raporty i opinie użytkowników.
* **Visual Studio Application Insights** monitorów hello usługi sieci web urządzeń przenośnych.

Tak Zobacz, jak skonfigurowanie to wszystko. 

> [!NOTE] 
> Wiele hello następujące kroki są opcjonalne.
>
>

## <a name="sign-up-for-accounts"></a>Załóż kont
* [Podstawowe informacje dotyczące programu Visual Studio Dev](https://www.visualstudio.com/products/visual-studio-dev-essentials-vs.aspx). To bezpłatny program zapewnia łatwy dostęp toomany developer tools i usług, w tym programu Visual Studio, Visual Studio Team Services i platformy Azure. Udostępnia środki na 25 miesięcznie na platformie Azure przez 12 miesięcy. Zawiera także uniwersyteckich Xamarin i szkolenia tooPluralsight subskrypcji. Można również założyć oddzielnie dla warstwy bezpłatna [Azure](https://azure.com) i [Visual Studio Team Services](https://www.visualstudio.com/products/visual-studio-team-services-vs.aspx), ale nie zapewniają one kredytów systemu Azure.
* [HockeyApp](https://rink.hockeyapp.net/) (opcjonalnie), do zarządzania testu dystrybucję aplikacji mobilnych i zbieranie danych telemetrycznych.
* [Xamarin](https://xamarin.com/) (wymagane), do tworzenia aplikacji mobilnej hello i uruchomione przebiegi debugowania i testy [chmury testowej Xamarin](https://xamarin.com/test-cloud).
* [GitHub](https://github.com/Azure-Samples/MyDriving/) (opcjonalnie) toocreate wolnego publicznego repozytoria własnego kodu (płatnej są prywatne repozytoria). Alternatywnie można użyć podstawowy plan hello w Visual Studio Team Services dla repozytoriów prywatnych.
* [Power BI](https://powerbi.microsoft.com/) (opcjonalnie) toocreate sformatowanego wizualizacje danych na powitania całego systemu.

> [!NOTE]
> Nie ma potrzeby GitHub tooaccess konta hello MyDriving kodu w [hello repozytorium GitHub MyDriving](https://github.com/Azure-Samples/MyDriving).
> 
> 

## <a name="install-development-tools"></a>Zainstaluj narzędzia do programowania
Witaj następujące ustawienia jest związane z opracowywaniem hello pełnego rozwiązania: iOS, Android i Windows 10 Mobile zaplecza aplikacji i platform, za pomocą platformy Azure.

Alternatywnie można użyć Xamarin Studio Mac lub Windows toodevelop hello mobile apps w, jeśli nie działają na powitania kończyć Azure z powrotem.

Brak [dłuższy opis tej instalacji](https://msdn.microsoft.com/library/mt613162.aspx).

### <a name="windows-development-machine"></a>Komputer deweloperski systemu Windows
centralnej narzędzie Windows Hello jest Visual Studio do pracy z hello MyDriving aplikacji dla systemów Android i Windows, projekt interfejsu API usługi aplikacji hello i rozszerzenia mikrousługi.

Program Xamarin, Git emulatorów i inne składniki przydatne są zintegrowane z programem Visual Studio.

Instalacja:

* [Visual Studio z platformą Xamarin](https://www.visualstudio.com/products/visual-studio-community-vs) (dowolna wersja — społeczności jest bezpłatna).
* [SQLite dla platformy uniwersalnej systemu Windows](https://visualstudiogallery.msdn.microsoft.com/4913e7d5-96c9-4dde-a1a1-69820d615936). Wymagane toobuild hello systemu Windows 10 Mobile kodu.
* [Zestaw Azure SDK dla programu Visual Studio](https://www.visualstudio.com/vs/azure-tools/). Umożliwia także hello zestawu SDK do uruchamiania aplikacji na platformie Azure, wraz z wiersza polecenia narzędzia do zarządzania Azure.
* [Usługi Azure Service Fabric SDK](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric). Wymagane toobuild hello [mikrousługi](../service-fabric/service-fabric-get-started.md) rozszerzenia.

Upewnij się, że masz hello prawo rozszerzeń programu Visual Studio. Sprawdź, czy w obszarze **narzędzia**, zostanie wyświetlony **Android, iOS, Xamarin...** . Jeśli nie, Otwórz program Visual Studio, wyszukania Xamarin i wykonaj hello monity tooinstall go. Ponadto sprawdź, czy **Git dla systemu Windows** jest zainstalowany. Jeśli nie, w programie Visual Studio ją wyszukać i wykonaj hello monity tooinstall go. 

### <a name="mac-development-machine"></a>Mac komputerze deweloperskim
Witaj Mac (Yosemite lub nowszym) jest wymagany, jeśli chcesz toodevelop dla systemu iOS. Mimo że możemy użyć programu Visual Studio z platformą Xamarin na toodevelop systemu Windows i zarządzanie cały kod hello, Xamarin używa agent został zainstalowany na komputerze Mac, w kolejności toobuild i znak hello kodu dla systemu iOS.

![Tworzenie w systemie Windows i kompilacji dla komputerów Mac](./media/iot-solution-build-system/image1.png)

(Alternatywnym służy program Xamarin Studio bezpośrednio na powitania Mac toodevelop wieloplatformowych aplikacji.)

Jeśli nie chcesz tooinclude iOS jako platforma docelowa nie jest konieczne hello Mac.

Instalacja:

* [Program Xamarin Studio dla systemu iOS](https://developer.xamarin.com/guides/ios/getting_started/installation/mac/). Można również skonfigurować Visual Studio i Xamarin na komputerze Mac, działającej maszyny wirtualnej systemu Windows. Zobacz [Instalatora, instalacja i weryfikacja dla użytkowników komputerów Mac](https://msdn.microsoft.com/library/mt488770.aspx) w witrynie MSDN.
* [Narzędzia deweloperskie Azure](https://azure.microsoft.com/downloads/) (opcjonalnie).

Włączanie zdalnej nazwy logowania na powitania Mac. Otwórz **preferencjach systemowych** > **udostępniania**, a następnie wybierz **logowania zdalnego**.

Po otwarciu projektu systemu iOS w programie Visual Studio w systemie Windows hello Xamarin wtyczki wyświetli monit o hello identyfikator Mac. hello

## <a name="fetch-hello-github-repository"></a>Pobierz repozytorium GitHub hello
Pobierz kopię lokalną [hello repozytorium GitHub MyDriving](https://github.com/Azure-Samples/MyDriving) przy użyciu hello **Pobierz ZIP** przycisk w witrynie GitHub, Visual Studio lub innego klienta Git.

Rozpakuj folderze tooa hello o krótkiej nazwy ścieżki, takie jak C:\\kodu.

Alternatywnie tookeep się toodate z lub współtworzenia tooour kodu, Klonuj następujący hello repozytorium:

**https://github.com/Azure-Samples/MyDriving.git klonowania git**

## <a name="get-a-bing-maps-api-key"></a>Pobierz klucz interfejsu API map Bing
[Zarejestruj klucz interfejsu API map Bing](https://msdn.microsoft.com/library/ff428642.aspx).

Należy tooreplace to w wierszu 22 cale `src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs`.

## <a name="build-hello-demo-app"></a>Tworzenie aplikacji demonstracyjnej hello
Otwieranie tych rozwiązań w programie Visual Studio:

* src\MobileApps\MyDriving.sln
* src\MobileAppService\MyDrivingService.sln
* src\Extensions\ServiceFabric\VINLookUpApplication\VINLookUpApplication.sln

Zostanie wyświetlony monit o:

* Zaufania niektórych projektów potencjalnie niezaufanym. Wybierz tooopen je, jeśli chcesz toogo wyprzedzeniem.
* Jeśli pracujesz na komputerze z systemem Windows 10 świeże, należy ustawić tryb dewelopera.
* Wprowadź swoje poświadczenia Xamarin.
* Połącz toohello Xamarin Mac. Jeśli nie masz Mac, iOS powitania kliknij prawym przyciskiem myszy projekt w programie Visual Studio, a następnie wybierz **Zwolnij projekt**.

Odbuduj hello rozwiązania.

Jeśli masz problemy budynku, spróbuj hello tooquirks rozwiązania, które znaleźliśmy:

* *VINLookupApplication projektu nie jest ładowana*: Upewnij się, że zainstalowano hello [zestawu Azure SDK dla programu Visual Studio](https://www.visualstudio.com/vs/azure-tools/).
* *Projekt sieci szkieletowej usług nie kompilacji*: tworzenie pierwszej kompilacji projektów interfejsu hello i upewnij się, że zainstalowano hello zestawu SDK usług sieci szkieletowej.
* *Android — aplikacja nie kompilacji*:
  
  * Otwórz **narzędzia** > **Android** > **Android SDK Manager**i upewnij się, że 6 systemu Android (interfejs API 23) / zainstalowano zestaw SDK platformy.
  * Usuń ten katalog, a następnie ponownie:<br/>
    `%LocalAppData%\Xamarin\zips`

## <a name="get-tooknow-hello-code"></a>Pobierz kod hello tooknow
W rozwiązaniu hello znajdziesz:

* Rozszerzenia Azure: sieć szkieletowa usług.
* Usługa Azure HDInsight: Skrypty do przetwarzania danych podróży na platformie Azure.
* Aplikacje mobilne: hello aplikacji dla urządzeń.
* MobileAppsService/MyDrivingService: końcowy hello sieci web z powrotem.
* Usługa Power BI: hello definicji raportu.
* Skrypty:
  
  * Menedżer zasobów: szablony toobuild hello zasobów platformy Azure.
  * Środowiska PowerShell: Skrypty toorun hello Resource Manager szablonów.
  * Azure SQL Database: Debugowanie baz danych.
* Baza danych SQL: CreateTables: definicje schematów.
* Usługa Azure Stream Analytics: Wysyła zapytanie strumieniu przekształcenia hello przychodzących danych.

## <a name="run-hello-apps-in-development-mode"></a>Uruchamianie aplikacji hello w trybie projektowania
Wykonaj akcję toorun aplikacji hello, oparty na urządzeniu hello, którego używasz:

* Wewnętrzna: MyDrivingService Ustaw jako projekt startowy hello, a następnie naciśnij klawisz F5 toorun hello sieci web zaplecza usługi. Zostanie otwarty widok przeglądarki listę hello interfejsu API.
* Klientów mobilnych: hello [aplikacji mobilnych są tworzone w programie Xamarin](https://developer.xamarin.com/guides/cross-platform/deployment,_testing,_and_metrics/debugging_with_xamarin/).
  
  * System android: Aby uzyskać więcej informacji, zobacz [debugowania dla systemu Android w programie Xamarin](http://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/debugging_with_xamarin_android/).
  * iOS: Aby uzyskać więcej informacji, zobacz [debugowania w systemie iOS](http://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/).
  * Windows Phone: Aby uzyskać więcej informacji, zobacz [Xamarin i Windows Phone](https://developer.xamarin.com/guides/cross-platform/windows/phone/).

## <a name="upload-hello-mobile-app-toohockeyapp"></a>Przekaż hello tooHockeyApp aplikacji mobilnej
HockeyApp zarządza dystrybucji hello Android, iOS i Windows aplikacji tootest użytkowników, powiadamianie użytkowników o nowych wersji. Ponadto zbiera raporty awarii przydatne, opinii użytkowników z zrzuty ekranu i metryki użycia.

[Rozpocznij od przekazywania](http://support.hockeyapp.net/kb/app-management-2/how-to-create-a-new-app) aplikacji kompilacji. Następnie zaloguj się za[HockeyApp](https://rink.hockeyapp.net) z komputerze deweloperskim. Na powitania projektanta pulpitu nawigacyjnego, kliknij przycisk **nową aplikację**, a następnie przeciągnij hello skompilowane pliki na powitania okna. (Później, można zautomatyzować Twojej toodo usługi kompilacji to.)

Teraz możesz w pulpicie nawigacyjnym aplikacji.

![Karta Przegląd na pulpicie nawigacyjnym aplikacji hello](./media/iot-solution-build-system/image2.png)

Powtórz kroki hello dla każdej platformy, która aplikacja będzie działać na. Następnie należy hello następujące czynności:

* Użyj hello [identyfikator aplikacji](http://support.hockeyapp.net/kb/app-management-2/how-to-find-the-app-id) z hello pulpitu nawigacyjnego toosend awarii danych i informacji zwrotnych z aplikacji. W MyDriving należy zaktualizować identyfikatorów hello w src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs.
* [Zaprosić użytkowników testowych](http://support.hockeyapp.net/kb/app-management-2/how-to-invite-beta-testers). Pobierz toorecruit adres URL testerów użytkowników. One będzie być może toosign dla zespołu, Pobierz aplikacji hello i wysłać opinię.
* Jeśli chcesz bardziej otwarte wydania beta, należy ustawić hello toopublic dystrybucji. Kliknij przycisk **Zarządzanie aplikacją** > **dystrybucji** > **Pobierz = Public**. Każda osoba, która teraz pobrać aplikację i wysłać opinię i zostanie wyświetlone powiadomienie, gdy opublikujesz nowej wersji. Zbyt można uzyskać niektóre raporty awarii z nich.
  
   ![Zespoły na powitania pulpitu nawigacyjnego](./media/iot-solution-build-system/image3.png)
* [Awaria łącza raportów tooVisual Studio Team Services](http://support.hockeyapp.net/kb/third-party-bug-trackers-services-and-webhooks/how-to-use-hockeyapp-with-visual-studio-team-services-vsts-or-team-foundation-server-tfs). Kliknij przycisk **Zarządzanie aplikacją** > **Visual Studio Team Services**. Platforma HockeyApp może automatycznie tworzyć elementy robocze w Team Services, jeśli raporty awarii ani otrzymania opinii.

Odczytaj w hello [lokacji HockeyApp](https://hockeyapp.net).

## <a name="test-hello-mobile-app-on-xamarin-test-cloud"></a>Testowanie aplikacji mobilnej hello na chmury testowej Xamarin
[Chmury testowej Xamarin](https://developer.xamarin.com/guides/testcloud/introduction-to-test-cloud/) automatyzuje rzeczywistych urządzeń w chmurze hello testów UI. Przy użyciu hello NUnit framework, należy napisać testy, które Uruchom aplikację za pomocą interfejsu użytkownika hello.

toouse Xamarin, możesz dołączyć do nich hello [Xamarin.UITests](https://developer.xamarin.com/guides/testcloud/uitest/intro-to-uitest/) zestawu SDK w aplikacji, która jest dostępna jako pakietu NuGet. Znajdziesz w hello aplikacja demonstracyjna, a była dostępna, podczas tworzenia nowych projektów testów z hello szablony Xamarin.

![Gdzie toofind hello SDK i platform w interfejsie hello](./media/iot-solution-build-system/image4.png)

Przykładowy projekt testu jest dołączony do aplikacji hello w repozytorium hello. W [MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService), sprawdź w obszarze [src](https://github.com/Azure-Samples/MyDriving/tree/master/src)/MobileApps/[MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileApps/MyDriving)/MyDriving.UITests/.

Jeśli używasz kompilacji programu Visual Studio Team Services, jest łatwe toowrite jednostkę interfejsu użytkownika platformy Xamarin testów i uruchom je jako część kompilacji.

## <a name="deploy-azure-services"></a>Wdrażanie usług platformy Azure
tooperform automatyczne wdrożenie usług platformy Azure i usługi kompilacji Team Services, zobacz toohello szczegółowe instrukcje w **scripts/README.md**.

Microsoft Azure zawiera szereg różnych usług, których można używać aplikacji w chmurze toobuild. Mimo że wiele mogą być używane pojedynczo (takich jak aplikacje sieci Web i usługi aplikacji), są one w ich w najlepszym przypadku są połączone tooform zintegrowany system tak jak używamy w MyDriving.

Jest to możliwe toocreate i ręcznie łączyć usług Azure, ale jest znacznie szybsza i bardziej niezawodna szablonów usługi Azure Resource Manager toouse. [Menedżer zasobów](../azure-resource-manager/resource-group-overview.md) zautomatyzowanie hello wdrażania rozwiązania zasobów oraz wprowadzania hello połączeń między nimi.

Szablon hello systemu MyDriving hello znajdziesz w repozytorium GitHub hello w obszarze [skryptów/ARM](https://github.com/Azure-Samples/MyDriving/tree/master/scripts/ARM). Zapewnia kompleksowe i zwięzły widok jak hello różnych usług w naszym architektury są połączone ze sobą. Prezentujemy wszystkie powyższe szczegółowo w hello zasady [MyDriving podręcznik](http://aka.ms/mydrivingdocs), ale Dowiedz się wiele wystarczy odczytu za pomocą szablonu hello.

> [!NOTE]
> Najbardziej Azure usługi mają skojarzone koszt, w zależności od hello warstwy cenowej. Jeśli nowy tooAzure można [bezpłatnie wypróbowanie](https://azure.microsoft.com/free/). Jednak jeśli nie planujesz toouse pewne składniki w hello MyDriving systemu, należy się tooremove ich tooavoid zaciąganie kosztów. sekcja "Szacowania kosztów operacyjnych" Hello później w tym artykule zawiera podsumowanie kosztów typowe usługi.
> 
> 

### <a name="edit-hello-template"></a>Edytuj szablon hello
toocustomize wdrożenia, prawdopodobnie tooremove zbędne części lub tooadd innych użytkowników, najpierw utwórz kopie scenariusza\_complete.params.json oraz scenariusz\_complete.json, w których zmiany toomake.

Można użyć scenariusza hello\_toooverride pliku complete.params.json różne wartości domyślne, takie jak hello usługi SKU lub hello typ replikacji magazynu, zgodnie z opisem w poniższej tabeli hello. wartości domyślne Hello wybierz opcje najniższy koszt hello.

| **Parametr** | **Opis** | **Wartość domyślna** |
| --- | --- | --- |
| Centrum IoT jednostki SKU |Warstwy usługi Centrum IoT Azure |F1 |
| Typ konta magazynu |Typ replikacji magazynu |Standard-LRS |
| Cel usługi SQL |Użycie miejsca współbieżności |DW100 |
| Plan hostingu jednostki SKU |Plan usługi App Service |F1 |

W scenariuszu\_complete.json:

* Wyszukaj nazwę "bazową" i zmień jego nazwę tooa, preferowaną.
* Wyszukaj "Utwórz". Każda z tych sekcji tworzy zasób.
* Ustaw sqlServerAdminLogin i sqlServerAdminPassword toosuitable wartości.
* Przed usunięciem sekcja, która tworzy zasób, sprawdź, czy ma zależności, wyszukując swojej nazwy w innym miejscu w pliku hello. Należy pamiętać, że każda sekcja, która tworzy usługę obejmuje *dependsOn* sekcji, która zawiera jego zależności.

W tym konfiguruje którego hello szablonu. Szczegółowe informacje znajdują się w hello [podręcznik](http://aka.ms/mydrivingdocs).

| **Usługa** | **Opis i szczegóły** |
| --- | --- |
| Konta magazynu |Szablon Hello tworzy trzy konta: |
| -Bazy danych SQL odbiera zagregowane dane telemetryczne z usługi Stream Analytics, która służy jako magazynu zapasowego hello tabel Azure App Service, z użyciem tych danych za pośrednictwem punkty końcowe interfejsu API. | |
| — Magazyn obiekt blob, która gromadzi dane historyczne z innego zadania Stream Analytics, toobe przetwarzanych przez usługi HDInsight. | |
| -Bazy danych SQL służącą do odbierania wyników przetworzone przez HDInsight do użycia z usługą Power BI. | |
| Azure IoT Hub |Ustanawia połączenie dwukierunkowe tooeach podłączonego urządzenia. W hello MyDriving rozwiązania aplikacji mobilnej hello działa jako pole bramy toosend danych tooAzure Centrum IoT. Centrum IoT Azure następnie służy jako tooStream wejściowego analizy. |
| Azure Event Hubs |Dane wyjściowe zadania Stream Analytics, że kolejek hello tooextensions dane wyjściowe, które są tworzone za pomocą usługi Azure Service Fabric. |
| Azure SQL Data Warehouse | |
| Zadania usługi analiza strumienia |Uzyskuj dostęp do danych wejściowych i wyjściowych kwerendę, która jest używana tooaggregate zarówno w czasie rzeczywistym, jak i historyczne dane dotyczące hello interfejsów API usługi App Service, usługi Azure Machine Learning, rozszerzenia i usługi Power BI. |
| Obszaru roboczego uczenia maszyny |Obejmuje eksperymentów, kod języka R i usługi interfejsu API. |
| Azure Data Factory |Zaplanowanego ponownego trenowania uczenia maszynowego. |
| Plan hostingu w sieci szkieletowej usług |Dla rozszerzenia. |
| Usługi aplikacji ("aplikacji mobilnej") |Hosty hello projekt interfejsu API aplikacji mobilnej, który zapewnia punkty końcowe hello aplikacji mobilnej. Witaj kodu interfejsu API musi być tooApp wdrożonej usługi w programie Visual Studio. |
| Reguły alertów |Wysyła wiadomości e-mail, jeśli odpowiedzi aplikacji hello wskazują błędów. |
| Application Insights |Do monitorowania wydajności hello interfejsów API w usłudze App Service. Masz połączenie hello tooconfigure w programie Visual Studio. |
| W usłudze Azure Key Vault |Aby zapisać certyfikat klastra usługi sieci web hello. |

### <a name="run-hello-template"></a>Uruchom hello szablonu
W **scripts/README.md**, są szczegółowe instrukcje dotyczące szablonu hello uruchomione.

tooprovision tych usług w konta platformy Azure przy użyciu skryptu hello, wykonaj jedną z hello następujące:

* Za pomocą programu PowerShell:
  
  ```
  
  cd scripts/PowerShell;
  deploy.ps1 *location* *resourceGroupName*
  ```
  
  * *Lokalizacja* jest hello [lokalizacji platformy Azure](https://azure.microsoft.com/regions/), takich jak `North Europe` lub `West US`. Użyj `Get-AzureLocation` toofind listę dostępnych lokalizacji.
  * *resourceGroupName* jest nazwą hello, którą toogive toohello grupa, której należy wszystkie zasoby hello. Po zakończeniu hello zasobów można usunąć je wszystkie razem przez usunięcie tej grupy.
* Uruchom DeploymentScripts/Bash/deploy.sh z Bash.
* Otwórz i rozwiązania Visual Studio hello DeploymentScripts/VS/DeployARM.sln kompilacji.

Należy pamiętać, że jest uruchamiane każdego szablonu hello czasu tworzy nowy zestaw zasobów pod inną nazwą. zasoby hello toodelete, przejdź toohello portal i Usuń grupę zasobów hello.

Jeśli skrypt hello jakiegoś powodu nie powiedzie się, można ponownie uruchomić.

zapewnia skryptu Hello hello możliwość skonfigurowania ciągłej integracji w programie Visual Studio Team Services. Jeśli w projekcie usługi Team Services, będziesz mieć adres URL: https://yourAccountName.visualstudio.com. Wprowadź pełny adres URL hello w odpowiedzi na pytanie. Można nadać mu nazwę nowego lub istniejącego projektu Team Services.

## <a name="set-up-build-and-test-definitions-in-visual-studio-team-services"></a>Konfigurowanie kompilacji i testowania definicje w Visual Studio Team Services
Firma Microsoft korzystania z usług zespołu nad tym projektem przede wszystkim na jego kompilacji i przetestować funkcje. Ale również zapewnia doskonałą współpracy pomocy technicznej, takich jak zadania zarządzania za pomocą tablic Kanban, kompilacje przeglądu kodu zintegrowane z zadaniami i kontroli źródła i warunkowych. Integruje się również przy użyciu innych narzędzi, takich jak GitHub, Xamarin HockeyApp i oczywiście Visual Studio. Można do niego dostęp za pośrednictwem interfejsu sieci web hello lub Visual Studio, w zależności jest wygodniejsze w dowolnym momencie.

Hello kroki w kompilacji hello i definicji wersji użycia różnych usług wtyczki, które są dostępne w usługach zespołu hello [Marketplace](https://marketplace.visualstudio.com/VSTS). Wiersze poleceń toorun dodanie toobasic narzędzia lub kopiowania plików są usługi wywołania które kompilacje Xamarin, Android i innych dostawców, a które łączyć tooHockeyApp.

![Opcje w Team Services kompilacji](./media/iot-solution-build-system/image5.png)

### <a name="build-definitions"></a>Definicje kompilacji
Mamy definicje kompilacji dla każdej hello główne cele. Mamy także odchyleń dla funkcji i testowania regresji. Daje:

* MyDriving.Services (hello aplikacji sieci web zaplecza aplikacji mobilnej hello)
* MyDriving.Xamarin.Android
  
  * MyDriving.Xamarin.Android — funkcja
  * Regresja MyDriving.Xamarin.Android
* MyDriving.Xamarin.iOS
  
  * MyDriving.Xamarin.iOS — funkcja
  * Regresja MyDriving.Xamarin.iOS
* MyDriving.Xamarin.UWP
  
  * MyDriving.Xamarin.UWP — funkcja
  * Regresja MyDriving.Xamarin.UWP

Jeśli chcesz toosee hello pełne szczegóły naszych konfiguracji, zobacz sekcję 4.7 hello [MyDriving podręcznik](http://aka.ms/mydrivingdocs), "Kompilacji i konfiguracji wydania". Wykonaj one hello tego samego wzorca ogólne. skrypt Hello:

1. Przywraca hello pakietu NuGet. Firma Microsoft nie przechowuj skompilowany kod w repozytorium hello, więc hello pierwsze kroki z każdej kompilacji toorestore hello wymaganych pakietów NuGet.
2. Aktywuje hello licencji. Kompilacja Hello jest wykonywane w chmurze hello tak w przypadku, gdy potrzebna licencja — w szczególności hello usługi--kompilacji Xamarin zostały tooactivate naszych licencji na maszynie kompilacji bieżącego hello. Następnie możemy zdezaktywować natychmiast później tooallow on toobe używany na innym komputerze.
3. Tworzy się przy użyciu hello odpowiednią usługę. Używamy kompilacje platformy Xamarin dla aplikacji mobilnych hello i Visual Studio kompiluje hello usługi sieci web zaplecza.
4. Tworzy testy.
5. Uruchamia testy. Firma Microsoft Uruchom testy aplikacji mobilnej hello w chmury testowej Xamarin.
6. Publikuje lokalizacji docelowej toohello wynik kompilacji hello.

wyzwalacz Hello hello głównego kompilacji jest ustawiony toocontinuous integracji. Oznacza to kompilacji hello jest uruchamiane za każdym razem kodu zostanie zaznaczona w gałęzi głównej toohello.

![Interfejs, której wyzwalacz hello jest zestaw toocontinuous integracji](./media/iot-solution-build-system/image6.png)

### <a name="release-definitions"></a>Definicji wersji
Definicji wersji są konfigurowane w znacznie hello sam sposób.

Usługi sieci web hello skonfigurowanie wdrożenia jako aplikacja sieci web platformy Azure:

![Interfejs na potrzeby konfigurowania wdrażania aplikacji sieci web platformy Azure](./media/iot-solution-build-system/image7.png)

I umieszczania hello wersji wyzwalacza toocontinuous wdrożenia. Oznacza to, co zaewidencjonowania następuje polecenie wyników pomyślnego utworzenia kompilacji w aplikacji sieci web toohello aktualizacji.

![Interfejs do ustawiania hello wersji wyzwalacza toocontinuous wdrożenia](./media/iot-solution-build-system/image8.png)

Dla aplikacji mobilnych możemy wdrożyć tooHockeyApp:

![Interfejs do wdrażania tooHockeyApp aplikacji mobilnej](./media/iot-solution-build-system/image9.png)

## <a name="explore-telemetry-by-using-application-insights"></a>Eksploruj dane telemetryczne za pomocą usługi Application Insights
[Usługa Application Insights](../application-insights/app-insights-overview.md) zbiera dane telemetryczne dotyczące hello wydajności i użycia usług sieci web. Hello zestaw SDK usługi Application Insights wysyła dane telemetryczne z toohello usługi hello zasobu usługi Application Insights na platformie Azure.

Przeglądaj szablonu hello Konfigurowanie toohello zasobu usługi Application Insights. Istnieje, można eksplorować wykresy wydajności hello Twojej [projekt usługi mobilnej aplikacji](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService). Pokazują one żądań serwera i czasy odpowiedzi, błędów, i liczby wyjątków. Dostępne są także wykresy czasów odpowiedzi zależności — to, że baza danych toohello wywołania i tooREST interfejsów API, takich jak Machine Learning. Jeśli występują problemy z wydajnością, będziesz w stanie toosee powoduje jakie części systemu.

![Wykres wydajności przykład](./media/iot-solution-build-system/image11.png)

Jeśli masz usługi sieci web skonfigurowanej ręcznie tooget łatwe jego hello wykresów tego samego. W bloku usługi sieci web hello, kliknij polecenie **narzędzia** > **rozszerzenia** > **Dodaj**. Wybierz **usługi Application Insights**.

![Interfejs wybierania wykresy hello tooget usługi Application Insights](./media/iot-solution-build-system/image12.png)

Funkcja Hello działa przez instrumentacji aplikacji przy użyciu hello zestaw SDK usługi Application Insights.

Możesz dodać niestandardowe dane telemetryczne (lub Instrumentacji aplikacji, która jest uruchomiona w innym poza Azure) przez [Dodawanie hello zestaw SDK usługi Application Insights](../application-insights/app-insights-asp-net.md) w czasie opracowywania. Jest to przydatne toolog metryki, które są zależne od aplikacji hello, takie jak długość średni podróży użytkowników lub całkowita przebiegu. W programie Visual Studio, kliknij prawym przyciskiem myszy projekt hello, a następnie wybierz **Dodaj usługę Application Insights**.

![Interfejs wybierania telemetria niestandardowa tooadd Dodaj usługę Application Insights](./media/iot-solution-build-system/image10.png)

Usługi Application Insights będzie wysyłać wiadomości e-mail alertów, jeśli nietypowe liczby odpowiedzi. Można również skonfigurować alerty na różnych metryk, takich jak czas odpowiedzi.

Po prostu toobe się, że usługi sieci web jest zawsze aktualne i działa, możesz skonfigurować [testów dostępności](../application-insights/app-insights-monitor-web-app-availability.md). Te testy ping witryny z różnych lokalizacji na całym świecie hello co 15 minut. Ponownie otrzymasz wiadomość e-mail Jeśli prawdopodobnie toobe problem.

## <a name="estimate-operational-costs"></a>Szacowanie kosztów operacyjnych
Jest niezwykle niedrogich toorun aplikacji, takich jak ta na małą skalę. Wiele hello usług ma bezpłatnej warstwy klasy podstawowej, dzięki czemu projektowanie i operacji na małą skalę koszt niewielkie. I oczywiście własnych aplikacji nie ma wszystkich funkcji hello przedstawiona w MyDriving toouse.

Oto oszacowanie koszty z konfigurowaniem konfiguracji Programowanie hello MyDriving. Firma Microsoft należy również zauważyć pewne rozwiązań alternatywnych, które robiliśmy *nie* użycia. Te informacje mogą być przydatne Szacowanie własnych kosztów.

Przyjęto założenie:

* Zespół nie więcej niż pięć (oraz obserwowania uczestnicy projektu).
* Uruchomiony około miesiąca.
* 100 użytkowników z czterech rund na dzień.

> [!NOTE]
> W przypadku nowych tooAzure jest [bezpłatne konto](https://azure.microsoft.com/free/).
> 
> 

| **Składnik/usługi** | **Uwagi** | **Koszt miesięcznie** |
| --- | --- | --- |
| [Visual Studio 2015 Community](https://www.visualstudio.com/products/visual-studio-community-vs) z [Xamarin](https://visualstudiogallery.msdn.microsoft.com/dcd5b7bd-48f0-4245-80b6-002d22ea6eee) <br/>Środowiska deweloperskiego między platformami |Visual Studio Community. (Należy [Visual Studio Professional](https://www.visualstudio.com/vs-2015-product-editions) dla [platformy Xamarin.Forms](https://xamarin.com/forms), toodesign i platform ze ścieżki bazowej kodu pojedynczego.) |$0 |
| [Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/) <br/>Toodevices połączenia danych dwukierunkowe |8000 wiadomości + 0,5 KB/komunikat zwolnienia. |$0 |
| [Stream Analytics](https://azure.microsoft.com/pricing/details/stream-analytics/)  <br/>   Przetwarzanie danych dużych strumienia |Opłata 0,031 $ na przesyłanie strumieniowe jednostki na godzinę, podczas włączania. Wybierz hello liczbę jednostek przesyłania strumieniowego, które mają; więcej tooscale w górę. |$23 |
| [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)<br/> Adaptacyjną odpowiedzi |$10 stanowisko/miesięcznie. <br/>                                                                                                                                                                                 + 3-godzinnym eksperymentu \* $1 / eksperymentu godzinę. <br/>                                                                                                                                                           + Procesora interfejsu API 3.5-godzinnym \* $2 / godzina produkcji procesora CPU. <br/>                                                                                                                                                          Czas procesora CPU interfejsu API zakłada 5 min/dzień ponownego trenowania, chociaż może to spowodować dane wejściowe.                   <br/>                                                                                                                                                                     + 2 min/dzień oceniania tooprocess 400 rund/dzień. |$20 |
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
Ponieważ utworzyliśmy Rozpocznij pracę toohelp MyDriving systemów IoT chcemy pewnością toohear od użytkownika o tym, jak działa. Daj nam znać, jeśli:

* Wystąpiły problemy lub wyzwania.
* Brak punktu rozszerzenia, że będą bardziej odpowiedni scenariusz tooyour.
* Efektywniejsze tooaccomplish sposób znaleźć określonych potrzeb.
* Masz inne sugestie dotyczące poprawiania MyDriving lub niniejszej dokumentacji.

opinie toogive plików [problem w usłudze GitHub] lub zostaw komentarz poniżej (en-us edition).

Mamy nadzieję toohearing od Ciebie!

## <a name="next-steps"></a>Następne kroki
Firma Microsoft zaleca hello [MyDriving podręcznik](http://aka.ms/mydrivingdocs), która jest kompleksowy opis projektu hello hello systemu i jej składniki.

