---
title: "aaaDashboard, monitora, skalowania, konfigurowanie i połączeń hybrydowych w usługi BizTalk Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello formantów i monitorowanie wydajności na kartach portalu klasycznego hello usługi BizTalk Services: pulpitu nawigacyjnego, Monitor skali, konfigurowanie i połączeń hybrydowych było możliwe. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a>Przejrzyj hello karty Pulpit nawigacyjny, Monitor skali, konfigurowanie i połączenia hybrydowego

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Po utworzeniu usługi BizTalk i wdrażania aplikacji, można zmienić niektóre ustawienia usługi BizTalk hello i monitorowanie wydajności aplikacji hello. 

Po otwarciu hello klasycznego portalu Azure, można automatycznie umieszczane w hello **wszystkie elementy** tooview kartę usługi BizTalk, wybierz usługę BizTalk w hello **wszystkie elementy** tab lub wybierz hello **Usługi BIZTALK SERVICES** ; a następnie wybierz nazwę usługi BizTalk.

Spowoduje to otwarcie nowego okna z hello następujące karty. W tym temacie opisano te karty.

## <a name="quickstart-quickstartquickstart"></a>(Szybki Start![Szybki start][Quickstart])
W zależności od wersji usługi BizTalk hello wszystkie opcje wymienione mogą nie być dostępne. 

<table border="1">
    <tr>
        <td><strong>Pobierz narzędzia hello</strong></td>
        <td>Pobierz hello zestawu SDK usługi BizTalk Services tooinstall hello szablony projektu Visual Studio na komputerze deweloperskim lokalnymi. Te szablony tworzą hello <strong>usługi BizTalk Services</strong> (mostek) i hello <strong>artefaktów usługi BizTalk</strong> projektów programu Visual Studio (Transform), które są wdrożone tooyour usługi BizTalk.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Jak mogę uruchomić przy użyciu hello zestaw SDK usług BizTalk Azure </a> i <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">hello Instalowanie zestawu SDK usługi BizTalk Azure</a> list hello tooget kroki pracy.
        </td>
    </tr>
    <tr>
        <td><strong>Tworzenie partnerów, umów</strong></td>
        <td>Zostanie otwarta hello Portal usługi BizTalk Azure hostowanej na platformie Azure, gdzie Dodawanie partnerami i tworzenie X12, AS2 oraz umów EDIFACT EDI.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Konfigurowanie składników EDI obsługi wiadomości w portalu usługi BizTalk</a> list hello tooget kroki pracy.
        </td>
    </tr>

<tr>
        <td><strong>Dowiedz się więcej na temat usługi BizTalk Services</strong></td>
        <td>Przejdź toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">Centrum uczenia</a> toolearn więcej informacji na temat usług BizTalk Azure.</td>
</tr>
</table>


Na pasku zadań hello u dołu hello można:

<table border="1">

<tr>
<td><strong>Zarządzanie</strong> wdrażania aplikacji</td>
<td>Otwiera hello portalu Azure usługi BizTalk. Portal usługi BizTalk Hello jest hello wejściu tooEDI konfiguracji, w tym dodawanie partnerami i tworzenie X12, AS2 oraz umów EDIFACT.
<br/><br/>
To jest identyczny hello <strong>Tworzenie umów z partnerami</strong> na powitania <strong>Szybki Start</strong> kartę.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Konfigurowanie składników EDI obsługi wiadomości w portalu usługi BizTalk</a> zamieszczono więcej informacji dotyczących hello Portal usługi BizTalk.</td>
</tr>

<tr>
<td><strong>Informacje o połączeniu</strong> z hello Namespace kontroli dostępu</td>
<td>Po wybraniu informacje o połączeniu tekst hello Namespace kontroli dostępu, domyślne wystawcy i klucza domyślne są wyświetlane. Możesz skopiować te wartości.
<br/><br/>
Można również otworzyć hello portalu kontroli dostępu. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Utwórz kontroli dostępu Namespace</a> zamieszczono więcej informacji dotyczących hello portalu kontroli dostępu.</td>
</tr>

<tr>
<td><strong>Synchronizowanie kluczy</strong> w hello konta magazynu</td>
<td>Podczas tworzenia konta usługi Storage następuje automatyczne utworzenie klucza podstawowego i klucza pomocniczego. Te klucze szyfrowania kontroli dostępu tooyour konta magazynu. Usługi BizTalk automatycznie używa hello klucza podstawowego. <strong>Synchronizowanie kluczy</strong> włączyć tooswitch użytkowników między hello klucz podstawowy i klucz pomocniczy hello bez zakłócania hello usługi BizTalk.
<br/><br/>
Na przykład chcesz hello toouse usługi BizTalk nowy klucz podstawowy hello konta magazynu. toodo to:
<br/><br/>
<ol>
<li>Wybierz usługę BizTalk i wybierz <strong>klucze synchronizacji</strong>. Wybierz hello klucza pomocniczego. Po wykonaniu tej czynności hello usługi BizTalk zacznie korzystać hello klucza pomocniczego.</li>
<li>W hello klasycznego portalu Azure wybierz konto magazynu i ponownie wygenerować hello klucza podstawowego. Należy pamiętać, że usługi BizTalk używa hello klucza pomocniczego.</li>
<li>Wybierz usługę BizTalk i wybierz <strong>klucze synchronizacji</strong>. Teraz wybierz hello klucza podstawowego. Jest to nowy hello można ponownie wygenerować klucz podstawowy.</li>
<li>W hello klasycznego portalu Azure wybierz konto magazynu i ponownie wygenerować klucz pomocniczy hello.</li>
</ol>
<br/>
Ten proces jest nazywany "przerzucania kluczy". Celem Hello jest tooenable tooswitch użytkowników między hello klucz podstawowy i klucz pomocniczy hello bez zakłócania hello usługi BizTalk.</td>
</tr>

<tr>
<td><strong>Usuń</strong> aplikacji</td>
<td>Po wybraniu usunąć usługi BizTalk, a wszystkie tooit wdrożone elementy są usuwane.</td>
</tr>
</table>


## <a name="dashboard"></a>Pulpit nawigacyjny
W zależności od wersji usługi BizTalk hello wszystkie opcje wymienione mogą nie być dostępne. 

Po wybraniu nazwy usługi BizTalk, karta pulpitu nawigacyjnego hello jest wyświetlana. Na pulpicie nawigacyjnym można:

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a>Przegląd wykorzystania: Pokazuje hello liczbę używanych połączeń hybrydowych
Wykorzystanie danych hello są również wyświetlane w GB. 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a>Wykres metryki: Lista stałej metryki wydajności
Te metryki Podaj wartości w czasie rzeczywistym dotyczące kondycji hello hello usługi BizTalk. Możesz również hello **względną** lub **bezwzględną** wartości i hello zakres czasu **interwał** hello metryk, które są wyświetlane na wykresie hello. 

Aby uzyskać opis tych metryk wydajności Przejdź zbyt[dostępne metryki](#Metrics) w tym temacie.

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a>Szybkiego dostępu: Wyświetla listę właściwości usługi BizTalk
<table border="1">

<tr>
<td><strong>Zaktualizuj poświadczenia śledzenia bazy danych</strong></td>
<td>Zmiany hello nazwę użytkownika i hasło używane toolog do hello śledzenia bazy danych.</td>
</tr>
<tr>
<td><strong>Aktualizuj certyfikat protokołu SSL</strong></td>
<td>Można aktualizować hello toouse usługi BizTalk innego certyfikatu SSL. Certyfikatu SSL z podpisem własnym jest tworzony automatycznie, gdy użytkownik <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">utworzyć hello usługi BizTalk</a>.</td>
</tr>
<tr>
<td><strong>Pobierz certyfikat</strong></td>
<td>Możesz pobrać hello certyfikat SSL używany przez komputer lokalny tooa usługi BizTalk.</td>
</tr>
<tr>
<td><strong>Stan</strong></td>
<td>Wyświetla bieżący stan hello usługi BizTalk. Zobacz <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">usługi BizTalk Services: Usługa stanu wykresu</a>. </td>
</tr>
<tr>
<td><strong>Adres URL usługi</strong></td>
<td>adres URL Hello usługi BizTalk. Jest to samo hello jako hello <strong>adresu URL domeny</strong> wprowadzane podczas tworzenia usługi BizTalk.</td>
</tr>
<tr>
<td><strong>Adres publiczny wirtualnego adresu IP (VIP)</strong></td>
<td>adres IP Hello przypisany tooyour usługi BizTalk. Jest on używany dla wszystkich wejściowych punktów końcowych i jest hello adresu źródłowego dla ruchu wychodzącego. Ten adres IP należy tooyour usługi BizTalk, pod warunkiem jego tworzenia. Jeśli usuniesz hello usługi BizTalk, adres IP hello jest przypisany tooanother usługi BizTalk.</td>
</tr>
<tr>
<td><strong>Namespace ACS</strong></td>
<td>Jest uwierzytelniany w usłudze hello usługi BizTalk.</td>
</tr>
<tr>
<td><strong>Wersja</strong></td>
<td>Wyświetla listę hello wprowadzona w wersji po utworzeniu hello usługi BizTalk.</td>
</tr>
<tr>
<td><strong>Lokalizacja</strong></td>
<td>Wyświetla hello region geograficzny, który jest hostem usługi BizTalk.</td>
</tr>
<tr>
<td><strong>Utworzone</strong></td>
<td>Hello hello Wyświetla datę i godzinę utworzenia usługi BizTalk.</td>
</tr>
<tr>
<td><strong>Śledzenie bazy danych</strong></td>
<td>Nazwa bazy danych SQL Azure Hello przechowuje hello śledzenia tabelami używanymi przez usługę BizTalk. 
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Wymagania dotyczące poradnik</a> zawiera szczegółowe informacje na powitania śledzenia bazy danych.</td>
</tr>
<tr>
<td><strong>Monitorowanie archiwizacji magazynu</strong></td>
<td>Hello nazwę konta magazynu Azure, która przechowuje hello monitorowania danych wyjściowych usługi BizTalk.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Wymagania dotyczące poradnik</a> zawiera szczegółowe informacje na powitania konta magazynu.</td>
</tr>
<tr>
<td><strong>Nazwa subskrypcji</strong></td>
<td>Wyświetla listę subskrypcji hello, który jest hostem usługi BizTalk. Subskrypcja Hello reguluje toohello dostępu do klasycznego portalu Azure.</td>
</tr>
<tr>
<td><strong>Identyfikator subskrypcji</strong></td>
<td>Identyfikator subskrypcji jest generowany automatycznie podczas tworzenia subskrypcji. Podczas korzystania z interfejsów API REST, może być konieczne hello tooenter identyfikator subskrypcji.</td>
</tr>
</table>

[Usługi BizTalk Services: Inicjowanie obsługi administracyjnej klasycznego portalu Azure za pomocą](http://go.microsoft.com/fwlink/p/?LinkID=302280) list hello toocreate kroki usługi BizTalk.

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a>Zarządzanie, informacje o połączeniu, klucze synchronizacji i Usuń na pasku zadań hello:
<table border="1">

<tr>
<td><strong>Zarządzanie</strong> wdrażania aplikacji</td>
<td>Otwiera hello Azure Portal usługi BizTalk. Portal usługi BizTalk Hello jest hello wejściu tooEDI konfiguracji, w tym dodawanie partnerami i tworzenie X12, AS2 oraz umów EDIFACT.
<br/><br/>
To jest identyczny hello <strong>Tworzenie umów z partnerami</strong> na powitania <strong>Szybki Start</strong> kartę.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Konfigurowanie składników EDI obsługi wiadomości w portalu usługi BizTalk</a> zamieszczono więcej informacji dotyczących hello Portal usługi BizTalk.</td>
</tr>
<tr>
<td><strong>Informacje o połączeniu</strong> z hello Namespace kontroli dostępu</td>
<td>Wyświetla hello Namespace kontroli dostępu, domyślne wystawcy i klucza domyślne wartości. które mogą zostać skopiowane.
<br/><br/>
Można również otworzyć hello portalu kontroli dostępu. Ten Portal kontroli dostępu jest hello taki sam jak przy użyciu opcji usługi Active Directory hello w okienku nawigacji po lewej stronie powitania.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Zarządzanie Your Namespace ACS</a> zamieszczono więcej informacji dotyczących hello portalu kontroli dostępu.</td>
</tr>
<tr>
<td><strong>Synchronizowanie kluczy</strong> w hello konta magazynu</td>
<td>Podczas tworzenia konta usługi Storage następuje automatyczne utworzenie klucza podstawowego i klucza pomocniczego. Te klucze szyfrowania kontroli dostępu tooyour konta magazynu. Usługi BizTalk automatycznie używa hello klucza podstawowego. <strong>Synchronizowanie kluczy</strong> włączyć tooswitch użytkowników między hello klucz podstawowy i klucz pomocniczy hello bez zakłócania hello usługi BizTalk.
<br/><br/>
Na przykład chcesz hello toouse usługi BizTalk nowy klucz podstawowy hello konta magazynu. toodo to:
<br/><br/>
<ol>
<li>Wybierz usługę BizTalk i wybierz <strong>klucze synchronizacji</strong>. Wybierz hello klucza pomocniczego. Po wykonaniu tej czynności hello usługi BizTalk zacznie korzystać hello klucza pomocniczego.</li>
<li>W hello klasycznego portalu Azure wybierz konto magazynu i ponownie wygenerować hello klucza podstawowego. Należy pamiętać, że usługi BizTalk używa hello klucza pomocniczego.</li>
<li>Wybierz usługę BizTalk i wybierz <strong>klucze synchronizacji</strong>. Teraz wybierz hello klucza podstawowego. Jest to nowy hello można ponownie wygenerować klucz podstawowy.</li>
<li>W hello klasycznego portalu Azure wybierz konto magazynu i ponownie wygenerować klucz pomocniczy hello.</li>
</ol>
<br/>
Ten proces jest nazywany "przerzucania kluczy". Celem Hello jest tooenable tooswitch użytkowników między hello klucz podstawowy i klucz pomocniczy hello bez zakłócania hello usługi BizTalk.</td>
</tr>

<tr>
<td><strong>Usuń</strong> aplikacji</td>
<td>Usługi BizTalk i wszystkie tooit wdrożone elementy zostaną usunięte.</td>
</tr>
</table>


## <a name="monitor"></a>Monitorowanie
Nie ma zastosowania toohello bezpłatna wersja.

Po wybraniu nazwy usługi BizTalk kartę Monitor hello jest dostępny i wyświetla następujące hello:

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a>Wykres metryki: Hello Wyświetla wybrany metryki wydajności
Te metryki Podaj wartości w czasie rzeczywistym dotyczące kondycji hello hello usługi BizTalk. Możesz wybrać metryki wydajności, które są wyświetlane. Maksymalnie sześć metryki wydajności mogą być jednocześnie wyświetlane. 

Możesz również hello **względną** lub **bezwzględną** wartości i hello zakres czasu **interwał** hello metryk, które są wyświetlane. 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a>metryki tooremove lub wyświetlany na wykresie hello:
1. Wybierz hello **Monitor** kartę.
2. Wybierz **dodać metryki** na pasku zadań hello:  
   ![Wybierz opcję Dodaj metryk][AddMetrics]
3. Sprawdź metryki wydajności hello ma toodisplay.
4. Wybierz hello znacznikiem wyboru tooreturn toohello **Monitor** kartę.
5. Wybierz hello koło dalej toohello metryki toodisplay wartość tej metryki hello wykresie.  
   
    Na przykład Witaj **użycie procesora CPU** metryka jest wyszarzona; dane wyjściowe nie jest wyświetlany na wykresie hello:  
   ![Metryki użycia procesora CPU jest szary.][GrayedMetric]  
   
    Wybierz hello wygaszone hello tooenable koło **użycie procesora CPU** metryki toodisplay dane wyjściowe w grafie hello:  
   ![Metryki użycia procesora CPU jest włączona.][EnabledMetric]
6. Wybierz tooremove Metryka z hello wyświetlania wykresu i listy hello **usunąć Metryka** na pasku zadań hello. tooadd hello metryki toohello wstecz listy, wybierz **dodać metryki** na pasku zadań hello, sprawdź hello metryki i wybierz hello znacznikiem wyboru tooreturn toohello **Monitor** kartę. Wybierz hello wygaszone koło tooenable hello metryki.

## <a name="Metrics"></a>Dostępne metryki
Witaj następujące metryki liczniki wydajności są dostępne:

<table border="1">

<tr>
<td><strong>Opóźnienie RountdTrip</strong></td>
<td>Wyświetla hello Średni czas w milisekundach (ms) tooprocess, otrzymany komunikat z wiadomość hello czasu powitania dopóki wiadomość hello pełni jest przetwarzany przez hello usługi BizTalk we wszystkich mostków. Zliczane są tylko pomyślnie przetworzonych komunikatów.<br/><br/>
Gdy występują następujące zdarzenia hello, tworzona jest sygnatura czasowa:
<ul>
<li>Komunikat wprowadza hello bramy</li>
<li>Komunikat jest miejscem docelowym toohello routingiem</li>
<li>Miejsce docelowe odpowiedzi</li>
<li>Docelowy potwierdzenia odpowiedzi wysłanych toohello bramy</li>
</ul>
<br/>
Ta metryka przedstawia wynik hello hello następujące obliczenie:
<br/><br/>
[Docelowy potwierdzenia odpowiedzi wysłanych toohello brama] - [hello brama wprowadza wiadomości]</td>
</tr>
<tr>
<td><strong>Błędy w źródle</strong></td>
<td>Wyświetla hello całkowita liczba komunikatów, których nie powiodła się przez hello usługi BizTalk, gdy ściąganie wiadomości z punktów końcowych źródła hello.</td>
</tr>
<tr>
<td><strong>Użycie procesora CPU</strong></td>
<td>Wyświetla listę hello średni procent czasu procesora wszystkich wystąpień ról.</td>
</tr>
<tr>
<td><strong>Opóźnienie przetwarzania</strong></td>
<td>Wyświetla średni czas hello w milisekundach (ms) tooprocess wiadomości przez hello usługi BizTalk we wszystkich mostków, z wyłączeniem czasu hello spędzony w miejsc docelowych. Zliczane są tylko pomyślnie przetworzonych komunikatów.<br/><br/>
Po każdym hello następujące zdarzenia, tworzona jest sygnatura czasowa:

<ul>
<li>Komunikat wprowadza hello bramy</li>
<li>Komunikat jest miejscem docelowym toohello routingiem</li>
<li>Miejsce docelowe odpowiedzi</li>
<li>Docelowy potwierdzenia odpowiedzi wysłanych toohello bramy</li>
</ul>
<br/>Ta metryka przedstawia wynik hello hello następujące obliczenie:<br/><br/>
[Docelowy potwierdzenia odpowiedzi wysłanych toohello brama] - [komunikat wprowadza bramy hello] - [docelowy odpowiedzi] + [wiadomość jest miejscem docelowym routingiem toohello]</td>
</tr>
<tr>
<td><strong>Błędy w procesie</strong></td>
<td>Wyświetla hello całkowita liczba komunikatów, których nie powiodła się podczas przetwarzania przez hello usługi BizTalk we wszystkich mostków hello w interwale czasu.</td>
</tr>
<tr>
<td><strong>Komunikaty wysyłane</strong></td>
<td>Wyświetla hello całkowitą liczbę komunikatów wysłanych przez hello usługi BizTalk we wszystkich mostków w interwale czasu. Ta metryka jest zwiększany, gdy komunikat wysłany z potokiem osiągnie hello docelowy trasy. Ta metryka nie wskazuje, że wiadomość jest pomyślnie przetwarzane.<br/><br/>
W scenariuszu "żądanie-odpowiedź" hello metryka jest zwiększany po docelowy trasy hello wysyła potoku wstecz toohello potwierdzenia otrzymania.</td>
</tr>
<tr>
<td><strong>Odebrane wiadomości</strong></td>
<td>Wyświetla hello całkowitą liczbę komunikatów odebranych przez hello usługi BizTalk we wszystkich mostków w interwale czasu. Ta metryka jest zwiększany, gdy nowy komunikat jest odbierany przez hello potoku.</td>
</tr>
<tr>
<td><strong>Komunikaty w procesie</strong></td>
<td>Wyświetla hello całkowita liczba aktualnie przetwarzanych przez usługę BizTalk hello w interwale czasu.</td>
</tr>
<tr>
<td><strong>Liczba przetworzonych komunikatów</strong></td>
<td>Wyświetla hello całkowita liczba komunikatów pomyślnie przetworzone przez hello usługi BizTalk we wszystkich mostków w interwale czasu. Ta metryka jest zwiększany, gdy wiadomość została odebrana pomyślnie hello potok i docelowym toohello pomyślnie routingiem.</td>
</tr>
</table>


## <a name="scale"></a>Skalowanie
Na karcie skali hello można dodać lub odjąć hello liczbę jednostek używanych przez usługę BizTalk. Domyślnie istnieje skonfigurowane jednostki. Dodatkowe jednostki można dodać tooscale usługi BizTalk. Zwiększenie skali hello są zwiększyć przepustowość. Witaj ilość zasobów zwiększa także, tym mostków wdrożone, umowy, LOB połączeń i mocy obliczeniowej. Na przykład można zwiększyć hello skali od 1 jednostki too2 jednostki. W takiej sytuacji można wdrożyć hello dwa razy liczba mostków, double umów hello double hello LOB połączeń i mocy obliczeniowej hello dwa razy.

Niektóre wersje BizTalk nie oferują opcji skalowania. W takim przypadku jednostki jest dozwolone. toodetermine liczbę jednostek, które mogą być skalowane posiadanej wersji, zobacz zbyt[usługi BizTalk Services: wersje wykresu](biztalk-editions-feature-chart.md).

Zwiększenie liczby hello jednostek może mieć wpływ cennik. Jeśli zwiększysz hello jednostki, wybierając **zapisać** zostanie wyświetlony komunikat informujący o tym, jeśli jest wpływ na rozliczenia. Następnie wybierz toocontinue. Wraz ze zwiększeniem hello liczbę jednostek hello stan usługi BizTalk zmienia Active tooUpdating. W hello aktualizacji stanu usługi BizTalk nadal toorun.

[Usługi BizTalk Services: Wersje wykresu](biztalk-editions-feature-chart.md) definiuje "Jednostki".

## <a name="configure"></a>Konfigurowanie
Nie dotyczy połączeń tooHybrid.

Ustawia hello tooNone stanu kopii zapasowej lub automatyczne. Po ustawieniu tooNone, nie ma kopii zapasowych są tworzone automatycznie. Po ustawieniu tooAutomatic, skonfiguruj hello lokalizacji kopii zapasowej, częstotliwość hello hello kopii zapasowej i jak długo pliki kopii zapasowej hello tookeep. 

[Usługi BizTalk Services: Kopia zapasowa i przywracanie](biztalk-backup-restore.md) hello szczegółowe informacje. 

## <a name="HybridConnections"></a>Połączenia hybrydowe
Połączenia hybrydowe umożliwiają łączenie aplikacji Azure, takich jak aplikacje sieci Web lub aplikacji mobilnych w usłudze Azure App Service, zasób lokalną tooan, który używa portu TCP statycznego, takich jak SQL Server, MySQL, interfejsów API sieci Web HTTP i najbardziej niestandardowych usług sieci Web. Usługi BizTalk Services zarządzania połączeń hybrydowych w hello klasycznego portalu Azure.

toocreate połączeń hybrydowych w usłudze Azure App Service, zobacz [dostępu do zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).

toocreate lub zarządzać połączeń hybrydowych w usłudze Azure BizTalk Services, zobacz [połączeń hybrydowych](integration-hybrid-connection-overview.md).

## <a name="next"></a>Następne kroki
Teraz, kiedy znasz różnych kartach zawierających hello, możesz dowiedzieć się więcej funkcji usług BizTalk Azure hello:

* [BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)](biztalk-throttling-thresholds.md)  
* [BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)](biztalk-issuer-name-issuer-key.md)  
* [BizTalk Services: Backup and Restore (Usługa BizTalk Services: tworzenie kopii zapasowej i przywracanie)](biztalk-backup-restore.md)

## <a name="see-also"></a>Zobacz też
* [Połączenia hybrydowe](integration-hybrid-connection-overview.md)  
* [Usługi BizTalk Services: Developer, podstawowa, standardowa i Premium Edition wykresu](biztalk-editions-feature-chart.md)  
* [Usługi BizTalk Services: Klasyczny portal Azure przy użyciu inicjowania obsługi](biztalk-provision-services.md)  
* [Usługi BizTalk Services: Stan usługi BizTalk wykresu](biztalk-service-state-chart.md)  
* [Jak mogę uruchomić przy użyciu hello Azure zestawu SDK usługi BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

