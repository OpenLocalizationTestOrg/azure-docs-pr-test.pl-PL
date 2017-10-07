---
title: "aaaTroubleshoot aplikacji sieci web w usłudze Azure App Service przy użyciu programu Visual Studio"
description: "Dowiedz się, jak tootroubleshoot aplikacji sieci web platformy Azure przy użyciu zdalnego debugowania, śledzenie i rejestrowanie narzędzi wbudowanych w tooVisual Studio 2013."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: 
ms.assetid: def8e481-7803-4371-aa55-64025d116c97
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: 8e3a8a58293f2ebcdc131fbf2534f8ff99b26730
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-web-app-in-azure-app-service-using-visual-studio"></a>Rozwiązywanie problemów z aplikacji sieci web w usłudze Azure App Service przy użyciu programu Visual Studio
## <a name="overview"></a>Omówienie
Ten samouczek pokazuje, jak toouse narzędzia Visual Studio, które ułatwiają debugowanie aplikacji sieci web w [usługi aplikacji](http://go.microsoft.com/fwlink/?LinkId=529714), uruchamiając w [tryb debugowania](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) zdalnie lub poprzez wyświetlenie Dzienniki aplikacji i dzienniki serwera sieci web.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

Dowiesz się:

* Funkcji zarządzania aplikacjami sieci web platformy Azure są dostępne w programie Visual Studio.
* Jak toouse Visual Studio zdalne wyświetlanie toomake szybkich zmian w aplikacji sieci web do zdalnego.
* Jak tryb debugowania toorun zdalnie podczas projektu jest uruchomiona na platformie Azure, zarówno w przypadku aplikacji sieci web, jak i zadanie WebJob.
* Jak aplikacja toocreate dzienniki śledzenia i przeglądać podczas tworzenia aplikacji hello je.
* Jak tooview dzienniki serwera sieci web, w tym szczegółowe komunikaty o błędach i śledzenie nieudanych żądań.
* Jak Diagnostyka toosend dzienniki tooan konta magazynu Azure i wyświetlić je istnieje.

Jeśli masz program Visual Studio Ultimate, można również użyć [IntelliTrace](http://msdn.microsoft.com/library/vstudio/dd264915.aspx) do debugowania. W tym samouczku nie pasuje do funkcji IntelliTrace.

## <a name="prerequisites"></a>Wymagania wstępne
W tym samouczku współpracuje z hello Środowisko deweloperskie, projekt sieci web i aplikacji sieci web platformy Azure, który został skonfigurowany w [wprowadzenie do platformy Azure i ASP.NET][GetStarted]. Dla sekcji zadań Webjob hello, będziesz potrzebować aplikacji hello, które są tworzone w [wprowadzenie hello Azure WebJobs SDK][GetStartedWJ].

Kod Hello próbek, w tym samouczku są przeznaczone dla aplikacji sieci web MVC C#, ale hello procedur rozwiązywania problemów są hello tej samej aplikacji Visual Basic i formularzy sieci Web.

Witaj samouczka przyjęto założenie, że używasz programu Visual Studio 2015 lub 2013. Jeśli używasz programu Visual Studio 2013, funkcje zadań Webjob hello wymagają [Update 4](http://go.microsoft.com/fwlink/?LinkID=510314) lub nowszym.

Dzienniki przesyłania strumieniowego Hello funkcja działa tylko w przypadku aplikacji przeznaczonych dla platformy .NET Framework 4 lub nowszy.

## <a name="sitemanagement"></a>Konfiguracja aplikacji sieci Web i zarządzanie
Program Visual Studio udostępnia dostępu tooa podzbiór funkcji zarządzania aplikacjami sieci web hello i ustawienia konfiguracji dostępne w hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). W tej sekcji zobaczysz, co jest dostępne przy użyciu **Eksploratora serwera**. Wypróbuj toosee hello najnowsze Azure funkcje integracji, **Eksplorator chmury** również. Oba okna można otworzyć z hello **widoku** menu.

1. Jeśli nie jest już zalogowany tooAzure w programie Visual Studio, kliknij przycisk hello **połączyć tooAzure** przycisk **Eksploratora serwera**.

    Alternatywą jest tooinstall czy umożliwia dostęp do konta tooyour certyfikatu zarządzania. Tooinstall wybrać certyfikat, kliknij prawym przyciskiem myszy hello **Azure** w węźle **Eksploratora serwera**, a następnie kliknij przycisk **zarządzanie i subskrypcje filtru** w menu kontekstowym hello. W hello **Zarządzaj subskrypcjami Azure** okna dialogowego kliknij hello **certyfikaty** , a następnie kliknij pozycję **importu**. Wykonaj hello toodownload instrukcjami, a następnie zaimportować plik subskrypcji (nazywane również *.publishsettings* pliku) dla konta platformy Azure.

   > [!NOTE]
   > Jeśli pobierzesz plik subskrypcji, zapisz go w folderze tooa poza katalogów kodu źródłowego (na przykład w folderze pobrane hello), a następnie usuń go, po zakończeniu importowania hello. Złośliwy użytkownik uzyska dostęp toohello subskrypcji plik można edytować, tworzenia i usuwania usług Azure.
   >
   >

    Aby uzyskać więcej informacji o podłączaniu tooAzure zasobów w programie Visual Studio, zobacz [Zarządzanie kontami, subskrypcje i ról administracyjnych](http://go.microsoft.com/fwlink/?LinkId=324796#BKMK_AccountVCert).
2. W **Eksploratora serwera**, rozwiń węzeł **Azure** i rozwiń **usługi aplikacji**.
3. Rozwiń grupę zasobów hello, która obejmuje hello aplikacji sieci web, który został utworzony w [wprowadzenie do platformy Azure i ASP.NET][GetStarted], a następnie kliknij prawym przyciskiem myszy węzeł aplikacji sieci web hello i kliknij przycisk **ustawienia widoku**.

    ![Ustawienia widoku w Eksploratorze serwera](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewsettings.png)

    Witaj **aplikacji sieci Web Azure** zostanie wyświetlona karta i widać tam hello sieci web aplikacji zarządzania i konfiguracji zadań, które są dostępne w programie Visual Studio.

    ![Okno aplikacji sieci Web platformy Azure](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configtab.png)

    W tym samouczku należy używać hello rejestrowania i śledzenia, listach rozwijanych. Będzie również używany zdalnego debugowania, ale użyjesz tooenable inną metodę go.

    Uzyskać hello pola ustawienia aplikacji i parametry połączenia w tym oknie informacje, zobacz [Azure Web Apps: jak ciągi aplikacji i pracy ciągów połączenia](http://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).

    Tooperform zadanie zarządzania aplikacji sieci web, które nie może zostać wykonane w tym oknie, kliknij przycisk **Otwórz w portalu zarządzania** tooopen toohello okna przeglądarki portalu Azure.

## <a name="remoteview"></a>Dostęp do plików aplikacji sieci web w Eksploratorze serwera
Zwykle wdrażanie projektu sieci web z hello `customErrors` oflagowane w hello zestawu plików Web.config zbyt`On` lub `RemoteOnly`, co oznacza, że użytkownik nie pojawia się komunikat przydatne, gdy coś nieprawidłowość. Wiele błędów, możesz uzyskać będzie stronę podobną hello następujące grupy.

**Błąd serwera w "/" aplikacji:**

![Strona błędu która nie jest pomocna](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror.png)

**Wystąpił błąd:**

![Strona błędu która nie jest pomocna](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror1.png)

**Witaj witryny sieci Web nie można wyświetlić strony hello**

![Strona błędu która nie jest pomocna](./media/web-sites-dotnet-troubleshoot-visual-studio/genericerror2.png)

Często hello Najprostszym sposobem toofind hello hello błąd jest spowodowany tooenable szczegółowe komunikaty o błędach, które hello pierwszy hello zrzuty ekranu poprzedzającym wyjaśniono, jak toodo. Który wymaga zmiany hello wdrożonym pliku Web.config. Można edytować hello *Web.config* pliku w projekcie hello i wdróż go ponownie hello projektu lub Utwórz [przekształcenie pliku Web.config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) i wdrożyć kompilację debugowania, ale szybciej: w **rozwiązania Eksplorator** bezpośrednio możesz wyświetlić i edytować pliki w aplikacji sieci web do zdalnego hello przy użyciu hello *zdalnego widoku* funkcji.

1. W **Eksploratora serwera**, rozwiń węzeł **Azure**, rozwiń węzeł **usługi aplikacji**, rozwiń grupę zasobów hello, która aplikacja sieci web znajdują się w temacie, a następnie rozwiń węzeł powitania dla aplikacji sieci web.

    Możesz sprawdzić węzłów, które zapewniają pliki zawartości i pliki dziennika aplikacji dostępu toohello sieci web.
2. Rozwiń hello **pliki** węzeł, a następnie kliknij dwukrotnie hello *Web.config* pliku.

    ![Otwórz plik Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfig.png)

    Visual Studio otworzy plik Web.config hello z aplikacji sieci web do zdalnego hello i przedstawia [zdalnego] następnej nazwy pliku toohello na pasku tytułu hello.
3. Dodaj powitania po wierszu toohello `system.web` elementu:

    `<customErrors mode="Off"></customErrors>`

    ![Edytowanie pliku Web.config](./media/web-sites-dotnet-troubleshoot-visual-studio/webconfigedit.png)
4. Odśwież hello przeglądarki, który jest wyświetlany komunikat która nie jest pomocna hello, a teraz uzyskać szczegółowy komunikat o błędzie, takich jak hello poniższy przykład:

    ![Szczegółowy komunikat o błędzie](./media/web-sites-dotnet-troubleshoot-visual-studio/detailederror.png)

    (błąd hello pokazano został utworzony przez dodanie wiersza hello zaznaczone na czerwono zbyt*Views\Home\Index.cshtml*.)

Edycji pliku Web.config hello jest tylko jeden przykład scenariusze, w których możliwości hello tooread i edytuj pliki w aplikacji sieci web platformy Azure ułatwienia rozwiązania problemu.

## <a name="remotedebug"></a>Zdalne debugowanie aplikacji sieci web
Jeśli hello szczegółowy komunikat o błędzie nie zawiera informacji wystarczających i nie można ponownie utworzyć błąd hello lokalnie, inny sposób tootroubleshoot zdalnie jest toorun w trybie debugowania. Można ustawić punktów przerwania, manipulowanie nimi pamięci bezpośrednio, krokowo kodu oraz nawet zmienić ścieżkę kodu hello.

Debugowanie zdalne nie działa w wersji Express programu Visual Studio.

W tej sekcji przedstawiono, jak toodebug zdalnie przy użyciu hello projektu, należy utworzyć w [wprowadzenie do platformy Azure i ASP.NET][GetStarted].

1. Projekt sieci web Otwórz hello utworzony w [wprowadzenie do platformy Azure i ASP.NET][GetStarted].
2. Otwórz *Controllers\HomeController.cs*.
3. Usuń hello `About()` — metoda i Wstaw następujący hello kod w jego miejscu.

        public ActionResult About()
        {
            string currentTime = DateTime.Now.ToLongTimeString();
            ViewBag.Message = "hello current time is " + currentTime;
            return View();
        }
4. [Ustaw punkt przerwania](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) na powitania `ViewBag.Message` wiersza.
5. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i kliknij przycisk **publikowania**.
6. W hello **profilu** listy rozwijanej, wybierz hello sam profilu tego można użyć w [wprowadzenie do platformy Azure i ASP.NET][GetStarted].
7. Kliknij hello **ustawienia** , a następnie zmień **konfiguracji** za**debugowania**, a następnie kliknij przycisk **publikowania**.

    ![Publikowanie w trybie debugowania](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-publishdebug.png)
8. Po wdrożeniu zakończenie i przeglądarka otwiera toohello Azure adres URL aplikacji sieci web, zamknij hello przeglądarki.
9. W **Eksploratora serwera**, kliknij prawym przyciskiem myszy aplikację sieci web, a następnie kliknij przycisk **dołączyć debuger**.

    ![Dołączanie debugera](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-attachdebugger.png)

    Przeglądarka Hello automatycznie otwiera stronę główną tooyour działające na platformie Azure. Może mieć toowait 20 sekund lub połączenie, więc Azure konfiguruje serwer hello do debugowania. To opóźnienie odbywa się tylko powitania po raz pierwszy uruchomiony w trybie debugowania w aplikacji sieci web. Kolejne razy w ciągu hello ciągu 48 godzin po rozpoczęciu debugowania ponownie będzie wyświetlony z pewnym opóźnieniem.

    **Uwaga:** Jeśli masz problemy z uruchamianie debugera hello toodo spróbuj go za pomocą **Eksplorator chmury** zamiast **Eksploratora serwera**.
10. Kliknij przycisk **o** hello menu.

     Zatrzymuje programu Visual Studio na powitania punktu przerwania i hello kod działa na platformie Azure, nie na komputerze lokalnym.
11. Umieść kursor nad hello `currentTime` wartość czasu hello toosee zmiennej.

     ![Zmienna widoku w trybie debugowania, które działają na platformie Azure](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugviewinwa.png)

     Witaj razem, gdy zostanie wyświetlony jest powitania serwera Azure czas, który może znajdować się w innej strefie czasowej niż komputera lokalnego.
12. Wprowadź nową wartość dla hello `currentTime` zmiennych, takich jak "Teraz działają na platformie Azure".
13. Naciśnij klawisz F5 toocontinue uruchomiona.

     Witaj o stronie działające na platformie Azure Wyświetla hello nową wartość wprowadzona w zmiennej bieżącagodzina hello.

     ![Strona z nową wartością — informacje](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugchangeinwa.png)

## <a name="remotedebugwj"></a>Zdalne debugowanie zadań Webjob
W tej sekcji przedstawiono, jak toodebug zdalnie przy użyciu hello projektu i aplikacji sieci web należy utworzyć w [wprowadzenie hello Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).

Funkcje Hello przedstawionym w tej sekcji są dostępne tylko w programie Visual Studio 2013 z aktualizacją Update 4 lub nowszym.

Debugowanie zdalne działa tylko ciągłe zadania Webjob. Zaplanowanych, jak i na żądanie zadania Webjob nie obsługuje debugowania.

1. Projekt sieci web Otwórz hello utworzony w [wprowadzenie hello Azure WebJobs SDK][GetStartedWJ].
2. W projekcie ContosoAdsWebJob hello Otwórz *Functions.cs*.
3. [Ustaw punkt przerwania](http://www.visualstudio.com/get-started/debug-your-app-vs.aspx) na powitania pierwszą instrukcją w hello `GnerateThumbnail` metody.

    ![Ustaw punkt przerwania](./media/web-sites-dotnet-troubleshoot-visual-studio/wjbreakpoint.png)
4. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt sieci web hello (nie projekt zadania WebJob hello) i kliknij przycisk **publikowania**.
5. W hello **profilu** listy rozwijanej, wybierz hello sam profilu tego można użyć w [wprowadzenie hello Azure WebJobs SDK](websites-dotnet-webjobs-sdk.md).
6. Kliknij hello **ustawienia** , a następnie zmień **konfiguracji** za**debugowania**, a następnie kliknij przycisk **publikowania**.

    Program Visual Studio wdroży hello sieci web i zadania WebJob projektów, a w przeglądarce zostanie otwarta toohello Azure adres URL aplikacji sieci web.
7. W **Eksploratora serwera** rozwiń **Azure > usługi aplikacji > grupy zasobów > aplikacji sieci web > zadań Webjob > ciągłe**i kliknij prawym przyciskiem myszy **ContosoAdsWebJob**.
8. Kliknij przycisk **dołączyć debuger**.

    ![Dołączanie debugera](./media/web-sites-dotnet-troubleshoot-visual-studio/wjattach.png)

    Przeglądarka Hello automatycznie otwiera stronę główną tooyour działające na platformie Azure. Może mieć toowait 20 sekund lub połączenie, więc Azure konfiguruje serwer hello do debugowania. To opóźnienie odbywa się tylko powitania po raz pierwszy uruchomiony w trybie debugowania w aplikacji sieci web. Hello następnym dołączyć debuger hello będzie opóźnienia, jeśli chcesz w ciągu 48 godzin.
9. W przeglądarce sieci web hello jest strona główna aplikacji Contoso Ads toohello otwarty Utwórz nowe usługi ad.

    Tworzenie ad powoduje, że kolejka komunikatów toobe utworzone, którego będą pobierane przez hello zadania WebJob i przetwarzane. Gdy zestaw SDK zadań Webjob hello wywołuje wiadomość hello funkcja tooprocess powitania kolejki, kod hello nastąpi trafienie punkt przerwania.
10. Gdy debuger hello dzieli się na punkt przerwania, można zbadać i zmieniać wartości zmiennych w trakcie hello program hello chmury. W hello następujące debugera hello ilustracja pokazuje zawartość hello hello blobInfo obiektu, który został przekazany toohello GenerateThumbnail — metoda.

     ![Obiekt blobInfo w debugerze](./media/web-sites-dotnet-troubleshoot-visual-studio/blobinfo.png)
11. Naciśnij klawisz F5 toocontinue uruchomiona.

     Hello metody GenerateThumbnail zakończy, tworzenie miniatur hello.
12. W przeglądarce hello strony indeksu hello odświeżania i zostanie wyświetlony hello miniatur.
13. W programie Visual Studio naciśnij klawisz SHIFT + F5 toostop debugowania.
14. W **Eksploratora serwera**, kliknij prawym przyciskiem myszy węzeł ContosoAdsWebJob hello i kliknij przycisk **widoku pulpitu nawigacyjnego**.
15. Zaloguj się przy użyciu poświadczeń usługi Azure, a następnie kliknij przycisk hello — strona toohello toogo Nazwa zadania WebJob WebJob.

     ![Kliknij przycisk ContosoAdsWebJob](./media/web-sites-dotnet-troubleshoot-visual-studio/clickcaw.png)

     Hello pulpitu nawigacyjnego przedstawia tego hello funkcja GenerateThumbnail ostatnio wykonane.

     (hello następnym kliknięciu **widoku pulpitu nawigacyjnego**, nie masz toosign w i przeglądarki hello dotyczy bezpośrednio strony toohello WebJob.)
16. Kliknij przycisk Szczegóły toosee nazwy funkcji hello o wykonanie funkcji hello.

     ![Szczegóły funkcji](./media/web-sites-dotnet-troubleshoot-visual-studio/funcdetails.png)

Jeśli funkcja [zapisano dzienniki](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs), można kliknąć przycisk **ToggleOutput** toosee je.

## <a name="notes-about-remote-debugging"></a>Uwagi dotyczące zdalnego debugowania
* Nie zaleca się uruchamiania w trybie debugowania w środowisku produkcyjnym. Jeśli Twoja aplikacja sieci web w środowisku produkcyjnym nie jest skalowana w poziomie toomultiple wystąpienia serwera, debugowanie uniemożliwi powitania serwera sieci web z odpowiada tooother żądań. Jeśli chcesz wielu wystąpień serwera sieci web po dołączeniu debugera toohello otrzymasz losowe wystąpienia, a mieć nie tooensure sposób przeglądarka kolejnych żądań przejdzie toothat wystąpienia. Ponadto zwykle nie można wdrożyć tooproduction kompilacji debugowania i optymalizacje kompilatora dla wersji kompilacji może być niemożliwe tooshow, co dzieje się linii w kodzie źródłowym. Podczas rozwiązywania problemów w środowisku produkcyjnym, najlepiej zasobu to aplikacja sieci web i śledzenie dzienniki serwera.
* Uniknąć długich zatrzymane na punktów przerwania podczas zdalnego debugowania. Azure traktuje procesu, który zostało zatrzymane przez czas dłuższy niż kilka minut jako proces nie odpowiada, a następnie zamyka go.
* Podczas debugowania kodu, hello serwer wysyła dane tooVisual w Studio, które mogą mieć wpływ na koszty przepustowości. Informacje o szybkości przepustowości, zobacz [cennik usługi Azure](https://azure.microsoft.com/pricing/calculator/).
* Upewnij się, że hello `debug` atrybutu hello `compilation` element hello *Web.config* pliku ustawiono tootrue. Tootrue jest ustawiona domyślnie po opublikowaniu konfiguracji kompilacji debugowania.

        <system.web>
          <compilation debug="true" targetFramework="4.5" />
          <httpRuntime targetFramework="4.5" />
        </system.web>
* Jeśli okaże się, że ten debuger hello nie wykonywanie kodu, które mają toodebug, może być ustawienie tylko mój kod hello toochange.  Aby uzyskać więcej informacji, zobacz [ograniczyć wykonywania krokowego tooJust mój kod](http://msdn.microsoft.com/library/vstudio/y740d9d3.aspx#BKMK_Restrict_stepping_to_Just_My_Code).
* Czasomierz rozpoczyna się na serwerze powitania po włączeniu funkcji zdalnego debugowania hello, oraz po 48 godzin funkcja hello jest automatycznie wyłączana. Ze względów bezpieczeństwa i wydajności odbywa się to ograniczenie 48 godzin. Można łatwo włączyć funkcji hello ponownie dowolną liczbę razy. Zaleca się pozostawienie ją wyłączoną, gdy nie są aktywnie debugowania.
* Można ręcznie dołączyć hello debugera tooany procesu, nie tylko hello web procesu aplikacji (w3wp.exe). Aby uzyskać więcej informacji dotyczących sposobu toouse debugowania tryb w programie Visual Studio, zobacz [debugowania w programie Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx).

## <a name="logsoverview"></a>Przegląd dzienników diagnostycznych
Aplikację ASP.NET, która działa w aplikacji sieci web platformy Azure można utworzyć hello następujące rodzaje dzienników:

* **Dzienniki śledzenia aplikacji**<br/>
  Witaj aplikacja tworzy te dzienniki przez wywołanie metody hello [System.Diagnostics.Trace](http://msdn.microsoft.com/library/system.diagnostics.trace.aspx) klasy.
* **Dzienniki serwera sieci Web**<br/>
  serwer sieci web Hello tworzy wpisów dziennika dla każdej aplikacji sieci web toohello żądania HTTP.
* **Szczegółowe informacje o błędzie dzienników komunikatów**<br/>
  serwer sieci web Hello tworzy strony HTML z niektóre dodatkowe informacje dotyczące żądań zakończonych niepowodzeniem HTTP (te, które powoduje kod stanu 400 lub nowszej).
* **Nie powiodło się żądanie dzienniki śledzenia**<br/>
  powitania serwera sieci web tworzy plik XML z informacjami o szczegółowe śledzenie niepomyślnych żądań HTTP. serwer sieci web Hello także XSL pliku tooformat hello XML w przeglądarce.

Rejestrowanie ma wpływ na wydajność aplikacji sieci web, więc Azure umożliwia hello tooenable możliwości lub wyłącz każdego typu dziennika stosownie do potrzeb. Dla Dzienniki aplikacji można określić, że można zapisywać tylko dzienniki powyżej pewnego poziomu ważności. Podczas tworzenia nowej aplikacji sieci web, domyślnie całego rejestrowania jest wyłączona.

Dzienniki są zapisywane toofiles *LogFiles* folder w systemie plików hello aplikacji sieci web i są dostępne za pośrednictwem protokołu FTP. Dzienniki aplikacji i dzienniki serwera sieci Web można również zapisać tooan konta magazynu Azure. Można zachować większa ilość dzienniki na koncie magazynu nie jest możliwe w systemie plików hello. Jesteś tooa ograniczone maksymalnie 100 megabajtów dzienniki użycia hello systemu plików. (Dzienniki systemu plików są tylko do przechowywania krótkoterminowego. Azure usuwa stare miejsca toomake plików dziennika dla nowych, po osiągnięciu limitu hello.)  

## <a name="apptracelogs"></a>Tworzenie i sprawdź dzienniki śledzenia aplikacji
W tej sekcji należy wykonać hello następujących zadań:

* Dodaj projekt sieci web toohello instrukcje śledzenia, który został utworzony w [wprowadzenie do platformy Azure i ASP.NET][GetStarted].
* Wyświetl dzienniki powitania po uruchomieniu projektu hello lokalnie.
* Wyświetl dzienniki hello wygenerowane hello aplikacji działających na platformie Azure.

Aby uzyskać informacji na temat sposobu logowania aplikacji toocreate w zadań Webjob, zobacz [jak zestaw SDK zadań Webjob — Witaj toowork z magazynu kolejek Azure za pomocą sposobu toowrite logowania](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs). Witaj następujące instrukcje dotyczące wyświetlania dziennika i określania, jak są przechowywane na platformie Azure mają również zastosowanie dzienniki tooapplication utworzony przez zadania Webjob.

### <a name="add-tracing-statements-toohello-application"></a>Dodaj aplikację toohello instrukcje śledzenia
1. Otwórz *Controllers\HomeController.cs*i Zastąp hello `Index`, `About`, i `Contact` metod hello następującego kodu w kolejności tooadd `Trace` instrukcje i `using` — instrukcja dla `System.Diagnostics`:

        public ActionResult Index()
        {
            Trace.WriteLine("Entering Index method");
            ViewBag.Message = "Modify this template toojump-start your ASP.NET MVC application.";
            Trace.TraceInformation("Displaying hello Index page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Index method");
            return View();
        }

        public ActionResult About()
        {
            Trace.WriteLine("Entering About method");
            ViewBag.Message = "Your app description page.";
            Trace.TraceWarning("Transient error on hello About page at " + DateTime.Now.ToShortTimeString());
            Trace.WriteLine("Leaving About method");
            return View();
        }

        public ActionResult Contact()
        {
            Trace.WriteLine("Entering Contact method");
            ViewBag.Message = "Your contact page.";
            Trace.TraceError("Fatal error on hello Contact page at " + DateTime.Now.ToLongTimeString());
            Trace.WriteLine("Leaving Contact method");
            return View();
        }        
2. Dodaj `using System.Diagnostics;` toohello instrukcji na początku pliku hello.

### <a name="view-hello-tracing-output-locally"></a>Śledzenie hello widoku danych wyjściowych lokalnie
1. Naciśnij klawisz F5 toorun hello aplikacji w trybie debugowania.

    odbiornik śledzenia domyślnego Hello zapisuje wszystkie toohello dane wyjściowe śledzenia **dane wyjściowe** okna, oraz innych danych wyjściowych debugowania. Witaj poniższej ilustracji przedstawiono dane wyjściowe hello hello instrukcji śledzenia dodania toohello `Index` metody.

    ![Śledzenie w oknie debugowania](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-debugtracing.png)

    Witaj następujące kroki pokazują, jak tooview danych wyjściowych śledzenia na stronie sieci web bez kompilowania kodu w trybie debugowania.
2. Otwórz plik Web.config aplikacji hello (jeden znajduje się w folderze projektu hello hello) i Dodaj `<system.diagnostics>` element na końcu pliku hello tuż przed zamknięciem hello hello `</configuration>` elementu:

          <system.diagnostics>
            <trace>
              <listeners>
                <add name="WebPageTraceListener"
                    type="System.Web.WebPageTraceListener,
                    System.Web,
                    Version=4.0.0.0,
                    Culture=neutral,
                    PublicKeyToken=b03f5f7f11d50a3a" />
              </listeners>
            </trace>
          </system.diagnostics>

    Witaj `WebPageTraceListener` umożliwiają wyświetlanie dane wyjściowe śledzenia przechodząc zbyt`/trace.axd`.
3. Dodaj <a href="http://msdn.microsoft.com/library/vstudio/6915t83k(v=vs.100).aspx">element śledzenia</a> w obszarze `<system.web>` w pliku Web.config hello, takich jak hello poniższy przykład:

        <trace enabled="true" writeToDiagnosticsTrace="true" mostRecent="true" pageOutput="false" />
4. Naciśnij klawisze CTRL + F5 toorun hello aplikacji.
5. Na pasku adresu hello hello okna przeglądarki, należy dodać *trace.axd* toohello adres URL, a następnie naciśnij klawisz Enter (adres URL hello będzie podobne toohttp://localhost:53370/trace.axd).
6. Na powitania **śledzenia aplikacji** kliknij przycisk **Wyświetl szczegóły** na powitania pierwszego wiersza (nie hello BrowserLink wiersza).

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd1.png)

    Hello **szczegółów żądania** zostanie wyświetlona strona w hello **informacje o śledzeniu** sekcji Zobacz hello danych wyjściowych instrukcji śledzenia hello dodania toohello `Index` metody.

    ![trace.axd](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-traceaxd2.png)

    Domyślnie `trace.axd` jest dostępna tylko lokalnie. Jeśli potrzebujesz toomake ją z aplikacji sieci web do zdalnego, można dodać `localOnly="false"` toohello `trace` element hello *Web.config* plików, jak pokazano w hello poniższy przykład:

        <trace enabled="true" writeToDiagnosticsTrace="true" localOnly="false" mostRecent="true" pageOutput="false" />

    Jednak włączenie `trace.axd` w sieci produkcyjnej aplikacji sieci web zwykle nie jest zalecane ze względów bezpieczeństwa, a w hello następujące sekcje pojawi się łatwiejsze tooread sposób śledzenia dzienniki w aplikacji sieci web platformy Azure.

### <a name="view-hello-tracing-output-in-azure"></a>Wyświetl dane wyjściowe śledzenia hello na platformie Azure
1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt sieci web hello i kliknij przycisk **publikowania**.
2. W hello **publikowanie w sieci Web** okno dialogowe, kliknij przycisk **publikowania**.

    Po Visual Studio publikuje aktualizację, zostanie otwarte okno tooyour strona główna (zakładając, że nie można wyczyścić **docelowy adres URL** na powitania **połączenia** kartę).
3. W **Eksploratora serwera**, kliknij prawym przyciskiem myszy aplikację sieci web i wybierz **Wyświetl dzienniki przesyłania strumieniowego**.

    ![Wyświetl dzienniki przesyłania strumieniowego w menu kontekstowym](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-viewlogsmenu.png)

    Witaj **dane wyjściowe** Pokazuje okno, które są połączone toohello przesyłania strumieniowego dzienników usługi i dodaje wiersz powiadomienia co minutę, który jest przesyłany bez toodisplay dziennika.

    ![Wyświetl dzienniki przesyłania strumieniowego w menu kontekstowym](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-nologsyet.png)
4. W oknie przeglądarki hello zawiera strony głównej aplikacji, kliknij przycisk **skontaktuj się z**.

    W ciągu kilku sekund hello, dane wyjściowe z hello śledzenia poziom błędu dodane toohello `Contact` metoda pojawia się w hello **dane wyjściowe** okna.

    ![Błąd podczas śledzenia w oknie danych wyjściowych](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-errortrace.png)

    Visual Studio tylko jest pokazywany śladów poziom błędu, ponieważ jest to ustawienie domyślne powitania po włączeniu dziennika hello monitorowanie usługi. Podczas tworzenia nowej aplikacji sieci web platformy Azure, wszystkie rejestrowanie jest domyślnie wyłączona, jak przedstawiono po otwarciu strony ustawień hello wcześniej:

    ![Rejestrowanie aplikacji](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-apploggingoff.png)

    Jednakże, gdy wybrano **Wyświetl dzienniki przesyłania strumieniowego**, Visual Studio automatycznie zmieniane **Logging(File System) aplikacji** za**błąd**, co oznacza, że dzienniki poziom błędu przekazywane. W kolejności toosee wszystkich dzienników śledzenia, możesz zmienić to ustawienie zbyt**pełne**. Po wybraniu niższa niż błąd poziom ważności, również są zgłaszane wszystkie dzienniki dla wyższego poziomu ważności. Więc po wybraniu pełne, możesz również sprawdzić informacje, ostrzeżenie i dzienników błędów.  

1. W **Eksploratora serwera**, kliknij prawym przyciskiem myszy hello aplikacji sieci web, a następnie kliknij przycisk **ustawienia widoku** tak samo jak wcześniej.
2. Zmień **rejestrowania aplikacji (w systemie plików)** za**pełne**, a następnie kliknij przycisk **zapisać**.

    ![Ustawienie poziomu tooVerbose śledzenia](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-applogverbose.png)
3. W oknie przeglądarki hello, który jest teraz wyświetlany z **skontaktuj się z** kliknij przycisk **Home**, następnie kliknij przycisk **o**, a następnie kliknij przycisk **skontaktuj się z**.

    W ciągu kilku sekund hello **dane wyjściowe** okna są wyświetlane wszystkie dane wyjściowe śledzenia.

    ![Dane wyjściowe śledzenia Verbose](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-verbosetraces.png)

    W tej sekcji włączyć i wyłączyć rejestrowanie za pomocą ustawień aplikacji sieci web platformy Azure. Można także włączyć i wyłączyć obiekty nasłuchujące śledzenia przez zmodyfikowanie pliku Web.config hello. Jednak zmodyfikowanie pliku Web.config hello powoduje, że toorecycle domeny aplikacji hello, podczas włączania rejestrowania za pomocą konfiguracji aplikacji sieci web hello nie to zrobić. Jeśli hello problem przyjmuje tooreproduce długo lub jest przerywana, odtwarzania domen aplikacji hello może "Napraw" i wymusić toowait dopóki zdarza się ponownie. Włączanie diagnostyki na platformie Azure nie to zrobić, można już zacząć od razu przechwytywanie informacji o błędzie.

### <a name="output-window-features"></a>Funkcje okna danych wyjściowych
Witaj **dzienników Azure** kartę hello **dane wyjściowe** okno ma kilka przycisków i pola tekstowego:

![Dzienniki karcie przycisków](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-icons.png)

Wykonaj te hello następujące funkcje:

* Wyczyść hello **dane wyjściowe** okna.
* Włącz lub Wyłącz zawijanie wierszy.
* Aby uruchomić lub zatrzymać monitorowanie dzienników.
* Określ, które rejestruje toomonitor.
* Pobierz dzienniki.
* Przefiltruj dzienniki na podstawie wyszukiwany ciąg lub wyrażenie regularne.
* Zamknij hello **dane wyjściowe** okna.

Jeśli wprowadzisz ciąg wyszukiwania lub wyrażenie regularne, Visual Studio filtruje informacje o rejestrowaniu na powitania klienta. Oznacza to, że można wprowadzić kryteria powitania po hello dzienniki są wyświetlane w hello **dane wyjściowe** a następnie zmienić kryteria filtrowania bez konieczności tooregenerate hello dzienniki.

## <a name="webserverlogs"></a>Wyświetl dzienniki serwera sieci web
Dzienniki serwera sieci Web rejestrować wszystkie aktywności protokołu HTTP dla aplikacji sieci web hello. W kolejności toosee je hello **dane wyjściowe** okno ma tooenable je na powitania sieci web app i przekaż programowi Visual Studio, które mają toomonitor je.

1. W hello **konfiguracji aplikacji sieci Web Azure** kartę, który został otwarty z **Eksploratora serwera**, zmień rejestrowania serwera sieci Web za**na**, a następnie kliknij przycisk **zapisać**.

    ![Włącz rejestrowanie pracy serwera sieci web](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-webserverloggingon.png)
2. W hello **dane wyjściowe** okna, kliknij hello **określić, które toomonitor Azure dzienniki** przycisku.

    ![Określ, które toomonitor dzienników Azure](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-specifylogs.png)
3. W hello **opcje rejestrowania Azure** wybierz pozycję **sieci Web dzienniki serwera**, a następnie kliknij przycisk **OK**.

    ![Monitoruj dzienniki serwera sieci web](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorwslogson.png)
4. W oknie przeglądarki hello pokazuje hello aplikacji sieci web, kliknij przycisk **Home**, następnie kliknij przycisk **o**, a następnie kliknij przycisk **skontaktuj się z**.

    Dzienniki aplikacji Hello zazwyczaj występować jako pierwszy, a następnie dzienniki serwera sieci web hello. Może być toowait podczas hello rejestruje tooappear.

    ![Dzienniki serwera sieci Web w oknie danych wyjściowych](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-wslogs.png)

Domyślnie po pierwszym włączeniu dzienniki serwera sieci web przy użyciu programu Visual Studio, Azure zapisuje hello toohello dzienniki w systemie plików. Alternatywnie, można użyć hello Azure toospecify portalu, które dzienniki serwera w sieci web powinna być zapisana tooa kontenera obiektów blob na koncie magazynu.

W przypadku używania serwera sieci web portalu tooenable hello rejestrowania tooan kontem magazynu platformy Azure, a następnie wyłącz rejestrowanie w programie Visual Studio po ponownym włączeniu rejestrowania w programie Visual Studio zostaną przywrócone ustawienia konta magazynu.

## <a name="detailederrorlogs"></a>Wyświetlanie dzienników komunikatów szczegółowe informacje o błędzie
Szczegółowe dzienniki błędów podaj dodatkowe informacje o żądaniach HTTP, które powoduje błąd kody odpowiedzi (400 lub nowszy). W kolejności toosee je hello **dane wyjściowe** okna, masz tooenable je na powitania sieci web app i przekaż programowi Visual Studio, które mają toomonitor je.

1. W hello **konfiguracji aplikacji sieci Web Azure** kartę, który został otwarty z **Eksploratora serwera**, zmień **szczegółowe komunikaty o błędach** za**na**, i następnie kliknij przycisk **zapisać**.

    ![Włącz szczegółowe komunikaty o błędach](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailedlogson.png)
2. W hello **dane wyjściowe** okna, kliknij hello **określić, które toomonitor Azure dzienniki** przycisku.
3. W hello **opcje rejestrowania Azure** okno dialogowe, kliknij przycisk **wszystkie dzienniki**, a następnie kliknij przycisk **OK**.

    ![Monitorowanie wszystkich dzienników](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-monitorall.png)
4. Na pasku adresu hello hello okna przeglądarki, Dodaj toocause adres URL toohello nadmiarowe znaki błąd 404 (na przykład `http://localhost:53370/Home/Contactx`), i naciśnij klawisz Enter.

    Po kilku sekundach hello dziennik szczegółowe informacje o błędzie pojawia się w Visual Studio hello **dane wyjściowe** okna.

    ![Szczegółowy dziennik błędów w oknie danych wyjściowych](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorlog.png)

    Kontrolowanie + kliknięcie hello łącze toosee hello wpisu w dzienniku sformatowany w przeglądarce:

    ![Szczegółowy dziennik błędów w oknie przeglądarki](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-detailederrorloginbrowser.png)

## <a name="downloadlogs"></a>Pobierz dzienniki systemu plików
Żadnych dzienników, które można monitorować w hello **dane wyjściowe** okna można również pobrać jako *.zip* pliku.

1. W hello **dane wyjściowe** okna, kliknij przycisk **Pobierz dzienniki przesyłania strumieniowego**.

    ![Dzienniki karcie przycisków](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadicon.png)

    Eksploratora plików otwiera tooyour *pobiera* folder o hello pobrany plik zaznaczony.

    ![Pobrany plik](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-downloadedfile.png)
2. Wyodrębnij hello *.zip* pliku i zostanie wyświetlony hello następujące struktury folderów:

    ![Pobrany plik](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilefolders.png)

   * Dzienniki śledzenia aplikacji znajdują się w *.txt* pliki w hello *LogFiles\Application* folderu.
   * Dzienniki serwera sieci Web znajdują się w *log* pliki w hello *LogFiles\http\RawLogs* folderu. Można użyć narzędzia, takie jak [Log Parser](http://www.microsoft.com/download/details.aspx?displaylang=en&id=24659) tooview tych plików i manipulowania nimi.
   * Szczegółowe informacje o błędzie komunikat Dzienniki znajdują się w *.html* pliki w hello *LogFiles\DetailedErrors* folderu.

     (hello *wdrożeń* folder jest tworzonych przez publikowanie; kontroli źródła nie ma cokolwiek pokrewne tooVisual Studio publikowania. Witaj *Git* jest folder dla śladów toosource powiązane kontrolki publikowanie hello plik dziennika i przesyłania strumieniowego usługi.)  

## <a name="storagelogs"></a>Wyświetl dzienniki magazynu
Dzienniki śledzenia aplikacji mogą być również wysyłane tooan kontem magazynu platformy Azure i można je wyświetlić w programie Visual Studio. toodo, że będzie utworzyć konto magazynu, Włącz dzienniki magazynu w portalu klasycznym hello i wyświetlić je w hello **dzienniki** kartę hello **aplikacji sieci Web Azure** okna.

Możesz wysłać dzienniki tooany lub wszystkich trzech miejsc docelowych:

* Witaj system plików.
* Tabele konta magazynu.
* Obiekty BLOB z konta magazynu.

Można określić poziom ważności różnych dla każdej lokalizacji docelowej.

Tabele stał się szczegóły łatwe tooview dzienników w trybie online i obsługują przesyłanie strumieniowe; można zbadać dzienniki w tabelach i Zobacz nowe dzienniki, ponieważ są one tworzone. Obiekty BLOB był łatwy toodownload dzienników w plikach i tooanalyze je za pomocą usługi HDInsight, ponieważ HDInsight wie jak toowork z magazynem obiektów blob. Aby uzyskać więcej informacji, zobacz **Hadoop i MapReduce** w [opcje magazynu danych (kompilowanie praktyczne aplikacje w chmurze platformy Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options).

Obecnie masz poziom systemu plików dzienników zestawu tooverbose; Witaj kolejnych krokach objaśniono sposób przy konfigurowaniu informacji poziomu dzienniki toogo toostorage konta tabel. Poziom informacji oznacza wszystkie dzienniki utworzona przez wywołanie metody `Trace.TraceInformation`, `Trace.TraceWarning`, i `Trace.TraceError` będą wyświetlane, ale nie dzienniki utworzona przez wywołanie metody `Trace.WriteLine`.

Konta usługi Storage oferują więcej pamięci, jak i długotrwałe przechowywania dzienników porównaniu toohello systemu plików. Inną zaletą aplikacja wysyłająca toostorage dzienniki śledzenia jest, aby uzyskać dodatkowe informacje o każdym dzienniku, której nie można korzystać z dzienników systemu plików.

1. Kliknij prawym przyciskiem myszy **magazynu** w obszarze hello Azure węzeł, a następnie kliknij przycisk **Utwórz konto magazynu**.

![Tworzenie konta magazynu](./media/web-sites-dotnet-troubleshoot-visual-studio/createstor.png)

1. W hello **Utwórz konto magazynu** okna dialogowego, wprowadź nazwę konta magazynu hello.

    Nazwa Hello musi być muszą być unikatowe (inne konto magazynu platformy Azure może mieć hello tej samej nazwy). Jeśli wprowadzona nazwa hello jest już używana, zostanie wyświetlony toochange szansy go.

    Witaj tooaccess adres URL konta magazynu będzie *{nazwa}*. core.windows.net.
2. Zestaw hello **Region lub grupę koligacji** tooyou najbliższy region toohello listy rozwijanej.

    To ustawienie określa, w którym Centrum danych Azure będą obsługiwać Twoje konto magazynu. W tym samouczku wybór nie należy to znaczącej różnicy, ale dla aplikacji sieci web w środowisku produkcyjnym trzeba serwera sieci web i toobe konta magazynu, korzystając z hello tego samego regionu toominimize opóźnienia i danych wyjściowych opłat. Aplikacja sieci web Hello (co należy utworzyć później) należy uruchomić w regionie, jak przeglądarki toohello możliwości uzyskiwania dostępu do aplikacji sieci web w kolejności toominimize opóźnienia.
3. Zestaw hello **replikacji** listy rozwijanej liście zbyt**magazyn lokalnie nadmiarowy**.
   
    Jeśli replikacja geograficzna jest włączona dla konta magazynu, hello przechowywana zawartość jest lokalizacji tooenable dodatkowego centrum danych replikowanych tooa toothat trybu failover w przypadku poważnej awarii w lokalizacji głównej hello. Replikacja geograficzna może pociągnąć za sobą dodatkowe koszty. W przypadku kont testowych i programistycznych zwykle nie chcesz toopay za replikację geograficzną. Aby uzyskać więcej informacji, zobacz temat dotyczący [tworzenia i usuwania konta magazynu oraz zarządzania nim](../storage/common/storage-create-storage-account.md).
4. Kliknij przycisk **Utwórz**.

    ![Nowe konto usługi Storage](./media/web-sites-dotnet-troubleshoot-visual-studio/newstorage.png)    
5. W Visual Studio hello **aplikacji sieci Web Azure** okna, kliknij hello **dzienniki** , a następnie kliknij pozycję **Konfiguruj rejestrowanie w portalu zarządzania**.

    <!-- todo:screenshot of new portal if hello VS page link goes toonew portal -->
    ![Konfigurowanie rejestrowania](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-configlogging.png)

    Spowoduje to otwarcie hello **Konfiguruj** kartę w portalu klasycznym powitania dla aplikacji sieci web.
6. W portalu klasycznym hello **Konfiguruj** karcie, przewiń w dół do sekcji Diagnostyka aplikacji toohello, a następnie zmień **rejestrowania aplikacji (Table Storage)** za**na**.
7. Zmień **poziom rejestrowania** za**informacji**.
8. Kliknij przycisk **zarządzać magazynem tabel**.

    ![Kliknij przycisk Zarządzaj TableStorage](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-stgsettingsmgmtportal.png)

    W hello **zarządzania magazynem tabeli z programem application Diagnostics** pole, można wybrać konta magazynu Jeśli masz więcej niż jeden. Możesz utworzyć nową tabelę lub użyć istniejącego.

    ![Zarządzanie magazynem tabeli](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-choosestorageacct.png)
9. W hello **zarządzania magazynem tabeli z programem application Diagnostics** pole kliknij hello znacznik wyboru tooclose hello pole.
10. W portalu klasycznym hello **Konfiguruj** , kliknij pozycję **zapisać**.
11. W oknie przeglądarki hello Wyświetla hello aplikacji sieci web aplikacji, kliknij przycisk **Home**, następnie kliknij przycisk **o**, a następnie kliknij przycisk **skontaktuj się z**.

     informacje o rejestrowaniu Hello utworzonego przez przeglądanie te strony sieci web zostanie zapisany toohello konta magazynu.
12. W hello **dzienniki** kartę hello **aplikacji sieci Web Azure** okna w programie Visual Studio, kliknij przycisk **Odśwież** w obszarze **diagnostycznych Podsumowanie**.

     ![Kliknij przycisk Odśwież](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-refreshstorage.png)

     Witaj **diagnostycznych Podsumowanie** sekcji przedstawiono dzienniki hello ostatnich 15 minut domyślnie. Możesz zmienić toosee okresu hello więcej dzienników.

     (Jeśli zostanie wyświetlony błąd "nie można odnaleźć tabeli", sprawdź, czy przeglądanie stron toohello, które hello śledzenie po włączono **rejestrowania aplikacji (magazyn)** i po kliknięciu przycisku **zapisać**.)

     ![Dzienniki magazynu](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-storagelogs.png)

     Zobacz powiadomienie, że w tym widoku, który **identyfikator procesu** i **identyfikator wątku** dla każdego dziennika, który nie możesz uzyskać w dziennikach systemu plików hello. Dodatkowe pola można wyświetlić, korzystając bezpośrednio hello tabeli magazynu systemu Azure.
13. Kliknij przycisk **Wyświetl wszystkie dzienniki aplikacji**.

     Tabela dziennika śledzenia Hello pojawia się w podglądzie tabeli magazynu systemu Azure hello.

     (Jeśli zostanie wyświetlony komunikat o błędzie "Sekwencja nie zawiera elementów", otwórz **Eksploratora serwera**, rozwiń węzeł hello konta magazynu w obszarze hello **Azure** węzeł, a następnie kliknij prawym przyciskiem myszy **tabel**i kliknij przycisk **Odśwież**.)

     ![Dzienniki magazynu w widoku tabeli](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracelogtableview.png)

     Ten widok przedstawia dodatkowe pola nie jest widoczny w innych widokach. W tym widoku można również toofilter dzienniki przy użyciu specjalnego interfejsu użytkownika konstruktora zapytań dla konstruowanie zapytania. Aby uzyskać więcej informacji, zobacz temat pracy z zasobami tabeli — filtrowania jednostek w [przeglądanie zasobami magazynu za pomocą Eksploratora serwera](http://msdn.microsoft.com/library/ff683677.aspx).
14. toolook na powitania szczegółów w pojedynczym wierszu, kliknij dwukrotnie jeden hello wierszy.

     ![Tabela śledzenia w Eksploratorze serwera](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-tracetablerow.png)

## <a name="failedrequestlogs"></a>Wyświetl dzienniki śledzenia nieudanych żądań
Dzienniki śledzenia nieudanych żądań są przydatne, gdy będziesz potrzebować toounderstand hello szczegółowe informacje dotyczące sposobu obsługuje żądania HTTP, w scenariuszach, takich jak problemy uwierzytelniania lub ponowne zapisywanie adresów URL usług IIS.

Funkcja śledzenia, które było dostępne w usługach IIS 7.0 i nowszych żądań hello użyj aplikacji sieci web platformy Azure sam nie powiodło się. Nie masz jednak toohello dostępu, które ustawienia usług IIS, które błędy konfiguracji mają być rejestrowane. Po włączeniu śledzenia nieudanych żądań, wszystkie błędy są przechwytywane.

Śledzenie nieudanych żądań można włączyć za pomocą programu Visual Studio, ale nie można wyświetlić je w programie Visual Studio. Te dzienniki są plikami XML. pliki, które zostaną uznane za czytelnych w trybie zwykłego tekstu monitoruje Hello przesyłania strumieniowego tylko usługi rejestrowania w dzienniku: *.txt*, *.html*, i *log* plików.

Dzienniki śledzenia nieudanych żądań można wyświetlić w przeglądarce bezpośrednio za pośrednictwem protokołu FTP lub lokalnie, po użyciu toodownload narzędzie FTP ich tooyour komputera lokalnego. W tej sekcji można będzie je wyświetlić w przeglądarce bezpośrednio.

1. W hello **konfiguracji** kartę hello **aplikacji sieci Web Azure** okna, który został otwarty z **Eksploratora serwera**, zmień **śledzenia nieudanych żądań**za**na**, a następnie kliknij przycisk **zapisać**.

    ![Włącz śledzenie nieudanych żądań](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequeston.png)
2. Na pasku adresu hello hello okna przeglądarki, pokazujący hello aplikacji sieci web Dodaj adres URL toohello nadmiarowe znaki, a następnie kliknij przycisk Enter toocause błąd 404.

    Powoduje to toobe dziennik śledzenia nieudanych żądań, utworzony i hello poniższej procedurze pokazano, jak tooview lub pobierania hello dziennika.
3. W programie Visual Studio w hello **konfiguracji** kartę hello **aplikacji sieci Web Azure** okna, kliknij przycisk **Otwórz w portalu zarządzania**.
4. W hello [Azure Portal](https://portal.azure.com) **ustawienia** bloku aplikacji sieci web, kliknij przycisk **poświadczenia wdrażania**, a następnie wprowadź nową nazwę użytkownika i hasło.

    ![Nowa FTP nazwa użytkownika i hasło](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-enterftpcredentials.png)

    ** Podczas logowania, masz toouse hello pełnej nazwy z tooit prefiksem nazwy aplikacji sieci web hello. Na przykład jeśli witryna hello jest "mój_przykład" Wprowadź "myid" jako nazwy użytkownika, logujesz się jako "myexample\myid".
5. W nowym oknie przeglądarki, przejdź do pozycji toohello adres URL, który jest wyświetlany w obszarze **nazwa hosta FTP** lub **FTPS hostname** w hello **aplikacji sieci Web** bloku aplikacji sieci web.
6. Zaloguj się przy użyciu poświadczeń hello FTP, które zostały utworzone wcześniej (w tym hello sieci web aplikacji prefiks nazwy dla nazwy użytkownika hello).

    przeglądarki Hello zawiera folder główny hello hello aplikacji sieci web.
7. Otwórz hello *LogFiles* folderu.

    ![Otwórz LogFiles folder](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-logfilesfolder.png)
8. Otwórz folder hello, o nazwie W3SVC plus wartość liczbową.

    ![Otwórz W3SVC folder](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfolder.png)

    Witaj folder zawiera pliki XML błędów, które zostały zarejestrowane po włączeniu śledzenia nieudanych żądań i pliku XSL w przeglądarce za pomocą tooformat hello XML.

    ![W3SVC folder](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-w3svcfoldercontents.png)
9. Kliknij przycisk hello pliku XML dla hello nieudanych żądań, który ma toosee informacji śledzenia dla.

    Witaj poniższej ilustracji przedstawiono część hello informacji śledzenia dla błędu próbki.

    ![Śledzenie nieudanych żądań w przeglądarce](./media/web-sites-dotnet-troubleshoot-visual-studio/tws-failedrequestinbrowser.png)

## <a name="nextsteps"></a>Następne kroki
W tym samouczku jak Visual Studio umożliwia łatwe tooview dzienniki utworzone przez aplikację sieci web platformy Azure. Witaj poniższe sekcje zawierają łącza zasobów toomore Tematy pokrewne:

* Rozwiązywanie problemów aplikacji sieci web platformy Azure
* Debugowanie w programie Visual Studio
* Zdalne debugowanie na platformie Azure
* Śledzenie w aplikacjach ASP.NET
* Analizowanie dzienników serwera sieci web
* Analizowanie dzienników śledzenia nieudanych żądań
* Debugowanie usług w chmurze

### <a name="azure-web-app-troubleshooting"></a>Rozwiązywanie problemów aplikacji sieci web platformy Azure
Aby uzyskać więcej informacji na temat rozwiązywania problemów z aplikacjami sieci web w usłudze Azure App Service zobacz następujące zasoby hello:

* [Jak toomonitor sieci web aplikacji](/manage/services/web-sites/how-to-monitor-websites/)
* [Badanie przecieki pamięci w aplikacji sieci Web platformy Azure za pomocą programu Visual Studio 2013](http://blogs.msdn.com/b/visualstudioalm/archive/2013/12/20/investigating-memory-leaks-in-azure-web-sites-with-visual-studio-2013.aspx). Microsoft ALM wpis w blogu o funkcje programu Visual Studio do analizowania problemów pamięci zarządzanej.
* [Narzędzia online aplikacji sieci web platformy Azure należy wiedzieć o](https://azure.microsoft.com/blog/2014/03/28/windows-azure-websites-online-tools-you-should-know-about-2/). Wpis w blogu przez firmę Apple Amitowi.

Aby uzyskać pomoc dotyczącą konkretne pytanie dotyczące rozwiązywania problemów należy uruchomić wątku w jednym następującego fora hello:

* [Hello Azure forum w witrynie platformy ASP.NET hello](http://forums.asp.net/1247.aspx/1?Azure+and+ASP+NET).
* [Hello Azure forum w witrynie MSDN](http://social.msdn.microsoft.com/Forums/windowsazure/).
* [StackOverflow.com](http://www.stackoverflow.com).

### <a name="debugging-in-visual-studio"></a>Debugowanie w programie Visual Studio
Aby uzyskać więcej informacji dotyczących sposobu toouse debugowania tryb w programie Visual Studio, zobacz hello [debugowania w programie Visual Studio](http://msdn.microsoft.com/library/vstudio/sc65sadd.aspx) MSDN, tematu i [debugowania etykietki z programu Visual Studio 2010](http://weblogs.asp.net/scottgu/archive/2010/08/18/debugging-tips-with-visual-studio-2010.aspx).

### <a name="remote-debugging-in-azure"></a>Zdalne debugowanie na platformie Azure
Aby uzyskać więcej informacji na temat zdalnego debugowania dla aplikacji sieci web platformy Azure i zadań Webjob Zobacz hello następujące zasoby:

* [Wprowadzenie tooRemote debugowania aplikacji usługi aplikacje sieci Web Azure](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/).
* [Wprowadzenie tooRemote debugowanie aplikacji sieci Web usługi aplikacji Azure część 2 - wewnątrz debugowanie zdalne](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)
* [Wprowadzenie tooRemote debugowanie aplikacji sieci Web usługi aplikacji Azure część 3 - w środowisku wielu wystąpień i GIT](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)
* [Zadania Webjob debugowania (klip wideo)](https://www.youtube.com/watch?v=ncQm9q5ZFZs&list=UU_SjTh-ZltPmTYzAybypB-g&index=1)

Jeśli aplikacja sieci web używa interfejsu API sieci Web Azure lub usługi Mobile Services zaplecza należy toodebug, który zobacz [debugowania zaplecza .NET w programie Visual Studio](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx).

### <a name="tracing-in-aspnet-applications"></a>Śledzenie w aplikacjach ASP.NET
Nie ma żadnych tooASP.NET wprowadzeń szczegółowe i aktualne śledzenie na powitania Internet. Hello najlepsze możesz zrobić jest wprowadzenie starego materiałów wprowadzające napisane specjalnie dla formularzy sieci Web ponieważ MVC i nie zostały jeszcze istnieje, które uzupełniają z nowszej blogu ogłoszenia skupiających się na konkretnych problemów. Niektóre toostart dobre miejsca są hello następujące zasoby:

* [Monitorowanie i dane telemetryczne (tworzenia rzeczywistych aplikacji w chmurze platformy Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry).<br>
  Książka elektroniczna rozdział z zaleceniami dotyczącymi śledzenie w aplikacjach w chmurze Azure.
* [Śledzenie na platformie ASP.NET](http://msdn.microsoft.com/library/ms972204.aspx)<br/>
  Stary, ale nadal dobrej zasobów dla podmiotu toohello wstęp.
* [Obiekty nasłuchujące śledzenia](http://msdn.microsoft.com/library/4y5y10s7.aspx)<br/>
  Informacje o obiektów nasłuchujących śledzenia, ale nie wspomina hello [WebPageTraceListener](http://msdn.microsoft.com/library/system.web.webpagetracelistener.aspx).
* [Wskazówki: Integrowanie śledzenie na platformie ASP.NET z System.Diagnostics śledzenia](http://msdn.microsoft.com/library/b0ectfxd.aspx)<br/>
  To zbyt jest stara, ale zawiera dodatkowe informacje wprowadzające artykułu hello nie obejmuje.
* [Śledzenie w widoki ASP.NET MVC Razor](http://blogs.msdn.com/b/webdev/archive/2013/07/16/tracing-in-asp-net-mvc-razor-views.aspx)<br/>
  Oprócz śledzenia w widokach Razor, hello post wyjaśniono również, jak filtrować toocreate wystąpił błąd w w kolejności toolog wszystkie nieobsługiwanych wyjątków w aplikacji MVC. Aby dowiedzieć się jak nieobsługiwany toolog wszystkie wyjątków w aplikacji formularzy sieci Web, zobacz przykład Global.asax Witaj w [pełny przykład dla programów obsługi błędu](http://msdn.microsoft.com/library/bb397417.aspx) w witrynie MSDN. W MVC i formularzy sieci Web toolog pewne wyjątki, ale pozwól framework domyślne hello obsługi zaczęły obowiązywać, można przechwycić i rethrow jak hello poniższy przykład:

        try
        {
           // Your code that might cause an exception toobe thrown.
        }
        catch (Exception ex)
        {
            Trace.TraceError("Exception: " + ex.ToString());
            throw;
        }
* [Przesyłanie strumieniowe diagnostyki śledzenia logowania z hello wiersza polecenia platformy Azure (oraz Glimpse!)](http://www.hanselman.com/blog/StreamingDiagnosticsTraceLoggingFromTheAzureCommandLinePlusGlimpse.aspx)<br/>
  Jak toouse hello toodo wiersza polecenia jakie ten samouczek przedstawia sposób toodo w programie Visual Studio. [Glimpse](http://www.hanselman.com/blog/IfYoureNotUsingGlimpseWithASPNETForDebuggingAndProfilingYoureMissingOut.aspx) to narzędzie do debugowania aplikacji ASP.NET.
* [Przy użyciu aplikacji sieci Web, rejestrowania i diagnostyki — z Ebbo Dominik](/documentation/videos/azure-web-site-logging-and-diagnostics/) i [przesyłania strumieniowego dzienników z aplikacji sieci Web — za pomocą Ebbo Dominik](/documentation/videos/log-streaming-with-azure-web-sites/)<br>
  Filmy wideo Scott Hanselman i Ebbo Dominika.

Rejestrowanie błędów alternatywnych toowriting kod śledzenia jest struktury rejestrowania toouse open source, takie jak [ELMAH](http://nuget.org/packages/elmah/). Aby uzyskać więcej informacji, zobacz [wpisy blogu Scott Hanselman o ELMAH](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx).

Należy również zauważyć, że masz toouse ASP.NET lub dzienniki śledzenia System.Diagnostics, jeśli chcesz tooget przesyłania strumieniowego z platformy Azure. Witaj przesyłania strumieniowego usługi rejestrowania w dzienniku aplikacji sieci web platformy Azure będą przesyłane strumieniowo żadnego *.txt*, *.html*, lub *log* pliku znalezionego w hello *LogFiles* folderu. W związku z tym można utworzyć własne systemu rejestrowania, zapisującej toohello system plików hello aplikacji sieci web, a plik zostanie automatycznie przesyłane strumieniowo i pobrane. Masz toodo zapisu kodu aplikacji, która tworzy pliki w hello jest *d:\home\logfiles* folderu.

### <a name="analyzing-web-server-logs"></a>Analizowanie dzienników serwera sieci web
Aby uzyskać więcej informacji na temat analizowania dzienniki serwera sieci web zobacz następujące zasoby hello:

* [LogParser](http://www.microsoft.com/download/details.aspx?id=24659)<br/>
  Narzędzia do wyświetlania danych w dzienniki serwera sieci web (*log* plików).
* [Rozwiązywanie problemów z wydajnością usług IIS lub błędy aplikacji przy użyciu LogParser](http://www.iis.net/learn/troubleshoot/performance-issues/troubleshooting-iis-performance-issues-or-application-errors-using-logparser)<br/>
  Dzienniki narzędzia Log Parser toohello wprowadzenie służy tooanalyze serwera sieci web.
* [Blog ogłoszenia przy Roberta Mcmurraya przy użyciu LogParser](http://blogs.msdn.com/b/robert_mcmurray/archive/tags/logparser/)<br/>
* [Witaj kod stanu HTTP w usługach IIS 7.0, IIS 7.5 i IIS 8.0](http://support.microsoft.com/kb/943891)

### <a name="analyzing-failed-request-tracing-logs"></a>Analizowanie dzienników śledzenia nieudanych żądań
zawiera witrynę sieci Web Microsoft TechNet Hello [za pomocą śledzenia nieudanych żądań](http://www.iis.net/learn/troubleshoot/using-failed-request-tracing) sekcji, które mogą być przydatne do zrozumienia sposobu toouse te dzienniki. Jednak ta dokumentacja skupiono się głównie na temat konfigurowania śledzenia nieudanych żądań w usługach IIS, które nie są możliwe w aplikacjach sieci Web platformy Azure.

[GetStarted]: app-service-web-get-started-dotnet.md
[GetStartedWJ]: websites-dotnet-webjobs-sdk.md
