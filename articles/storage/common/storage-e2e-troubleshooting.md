---
title: "aaaTroubleshooting usługi Azure Storage z diagnostyki & Message Analyzer | Dokumentacja firmy Microsoft"
description: "Samouczek prezentacja end-to-end Rozwiązywanie problemów z funkcją analizy magazynu Azure, AzCopy i programu Microsoft Message Analyzer"
services: storage
documentationcenter: dotnet
author: robinsh
manager: timlt
ms.assetid: 643372a3-1c07-4e88-b4ef-042512a43086
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/15/2017
ms.author: robinsh
ms.openlocfilehash: 2d7a2a14b2e8da01b566ac3dec19996f0ef88cc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="end-to-end-troubleshooting-using-azure-storage-metrics-and-logging-azcopy-and-message-analyzer"></a>Rozwiązywanie problemów na trasie przy użyciu metryk usługi Azure Storage i rejestrowania, AzCopy i analizatora komunikatów
[!INCLUDE [storage-selector-portal-e2e-troubleshooting](../../../includes/storage-selector-portal-e2e-troubleshooting.md)]

Diagnozowanie i rozwiązywanie problemów z jest klucza umiejętności umożliwiające tworzenie i obsługa aplikacji klienta za pomocą usługi Magazyn Microsoft Azure. Powodu charakter toohello rozproszonych aplikacji Azure diagnozowanie i rozwiązywanie problemów z błędów i problemów z wydajnością może być bardziej skomplikowane niż w tradycyjnych środowisk.

W tym samouczku przedstawiony sposób tooidentify niektórych błędów, które mogą wpłynąć na wydajność i Rozwiąż te błędy z end-to-end za pomocą narzędzi dostarczanych przez firmę Microsoft i usługi Azure Storage w kolejności toooptimize powitania klienta aplikacji.

Ten samouczek zawiera praktyczne eksploracji end-to-end scenariusza rozwiązywania problemów. Dla aplikacji usługi Azure storage szczegółowy przewodnik koncepcyjny tootroubleshooting [monitorowanie, diagnozowanie i rozwiązywanie problemów z usługi Magazyn Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="tools-for-troubleshooting-azure-storage-applications"></a>Narzędzia do rozwiązywania problemów z aplikacjami usługi Azure Storage
aplikacje klienckie tootroubleshoot przy użyciu usługi Magazyn Microsoft Azure, można użyć kombinacji toodetermine narzędzia, gdy wystąpił problem, i jakie hello przyczyną problemu hello może być. Do tych narzędzi należą:

* **Usługa Azure Storage Analytics**. [Analizy usługi Azure Storage](/rest/api/storageservices/Storage-Analytics) zawiera metryki i rejestrowania usługi Azure Storage.
  
  * **Metryki magazynu** śledzi transakcji metryki i metryki pojemności konta magazynu. Korzystając z metryki, można określić, jak aplikacja działa zgodnie z różnych tooa różnych działań. Zobacz [schemat tabeli metryki analityka magazynu](/rest/api/storageservices/Storage-Analytics-Metrics-Table-Schema) Aby uzyskać więcej informacji o typach hello metryki śledzone przez analityka magazynu.
  * **Rejestrowanie magazynu** dzienniki każdego żądania dziennika toohello usługi Azure Storage services tooa po stronie serwera. szczegółowe dane ścieżki Hello dziennika dla każdego żądania, w tym operacji hello wykonać hello stanu operacji hello i informacji opóźnienia. Zobacz [Format dziennika analityka magazynu](/rest/api/storageservices/Storage-Analytics-Log-Format) Aby uzyskać więcej informacji na temat hello żądań i odpowiedzi dane zapisane dzienniki toohello przez analityka magazynu.

> [!NOTE]
> Konta magazynu typu replikacji z magazynu Strefowo nadmiarowy (ZRS) nie mają metryki hello lub funkcja rejestrowania teraz włączone. 
> 
> 

* **Azure portal**. Można skonfigurować rejestrowanie i metryki dla konta magazynu w hello [portalu Azure](https://portal.azure.com). Można także wyświetlić schematy i wykresy, które pokazują, jak aplikacja działa w czasie i skonfigurować toonotify alerty, jeśli aplikacja przeprowadza się inaczej niż oczekiwany dla określonej metryki.
  
    Zobacz [monitorować konta magazynu w portalu Azure hello](storage-monitor-storage-account.md) informacji o konfigurowaniu monitorowania w hello portalu Azure.
* **Narzędzie AzCopy**. Dzienniki serwera usługi Azure Storage są przechowywane jako obiekty BLOB, dzięki czemu można użyć narzędzia AzCopy toocopy hello dziennika obiekty BLOB tooa katalogu lokalnego do analizy przy użyciu programu Microsoft Message Analyzer. Zobacz [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md) Aby uzyskać więcej informacji na temat narzędzia AzCopy.
* **Microsoft Message Analyzer**. Message Analyzer jest narzędziem, które korzysta z plików dziennika i dane dziennika są wyświetlane w formacie visual, który umożliwia łatwe toofilter, wyszukiwanie i grupy rejestrowanie danych do przydatne zestawów służącego tooanalyze błędów i problemów z wydajnością. Zobacz [Microsoft komunikatów analizatora operacyjnego przewodnik](http://technet.microsoft.com/library/jj649776.aspx) Aby uzyskać więcej informacji na temat analizatora komunikatów.

## <a name="about-hello-sample-scenario"></a>O hello przykładowy scenariusz
W tym samouczku zostaną omówione scenariusz, w którym metryk usługi Azure Storage wskazuje tempo niski procent powodzenia dla aplikacji, która wywołuje magazynu Azure. Witaj pomiar szybkości niski procent powodzenia (wyświetlane jako **PercentSuccess** w hello [portalu Azure](https://portal.azure.com) i w tabelach metryki hello) śledzi operacji, który powiedzie się, ale który zwrócił kod stanu HTTP, która jest większa niż 299. W plikach dziennika magazynu po stronie serwera hello, operacje te są rejestrowane ze stanem transakcji **ClientOtherErrors**. Aby uzyskać więcej informacji na temat Metryka niski procent powodzenia hello zobacz [metryki pokazują PercentSuccess niskim lub wpisy dziennika analytics ma operacji ze stanem transakcji ClientOtherErrors](storage-monitoring-diagnosing-troubleshooting.md#metrics-show-low-percent-success).

Azure operacje magazynu mogą zwracać kody stanu HTTP większa niż 299 jako część ich normalną funkcjonalność. Jednak te błędy w niektórych przypadkach wskazują, że może być możliwe toooptimize aplikację kliencką dla wyższą wydajność.

W tym scenariuszu teraz przyjrzymy się toobe szybkość niski procent powodzenia niczego poniżej 100%. Można wybrać różne metryki poziomu, jednak zgodnie z potrzebami tooyour. Firma Microsoft zaleca, że podczas testowania aplikacji, zostanie nawiązana tolerancji linii bazowej dla Twojego kluczowe metryki wydajności. Na przykład można określić na podstawie testowanie, czy aplikacja ma Częstotliwość powodzeń procent spójne 90% lub 85%. Jeśli dane metryk pokazuje, że aplikacja hello jest różniących się od tego numeru, a następnie można zbadać, co może powodować wzrost hello.

W naszym scenariuszu próbki po ustaleniu firma Microsoft hello procent powodzenia szybkość Metryka wynosi poniżej 100%, firma Microsoft będzie zbadać hello dzienniki toofind hello błędów, które skorelowania toohello metryki i używać ich toofigure się, co powoduje hello mniejszej szybkości procent powodzenia. Wyjaśniono, w szczególności błędy hello 400 zakresu. Następnie firma Microsoft będzie dokładniejsze badanie błędów 404 (nie znaleziono).

### <a name="some-causes-of-400-range-errors"></a>Niektóre przyczyny błędów 400 zakresu
Przykłady Hello poniżej przedstawiono przykładowy zakres 400 błędy żądań dotyczących magazynu obiektów Blob Azure i ich możliwe przyczyny. Żadnego z tych błędów, jak również błędy w zakresie 300 hello i hello 500 zakresu, może przyczynić się tooa niski procent współczynnika.

Należy zauważyć, że poniższe listy hello daleko od ukończenia. Zobacz [stanu i kodów błędów](http://msdn.microsoft.com/library/azure/dd179382.aspx) w witrynie MSDN, aby uzyskać szczegółowe informacje dotyczące ogólne błędy usługi Azure Storage i tooeach określonych błędów hello usług magazynu.

**Przykłady kodu 404 (nie znaleziono) stanu**

Występuje, gdy operacja odczytu względem kontener lub obiekt blob nie powiedzie się, ponieważ nie znaleziono obiektu blob hello lub kontenera.

* Występuje, gdy kontener lub obiekt blob został usunięty przez innego klienta przed tego żądania.
* Występuje, gdy używasz wywołanie interfejsu API, które tworzy hello kontener lub obiekt blob po sprawdzeniu, czy istnieje. Witaj CreateIfNotExists interfejsów API upewnij HEAD wymagają pierwszy toocheck istnienie hello hello kontener lub obiekt blob; Jeśli nie istnieje, zwracany jest błąd 404, a drugie wywołanie PUT jest przeprowadzane toowrite hello kontener lub obiekt blob.

**Kod stanu 409 przykłady (konflikt)**

* Występuje, gdy używasz toocreate API utworzyć nowy kontener lub obiekt blob, bez uprzedniego sprawdzania pod kątem istnienia i kontener lub obiekt blob o tej nazwie już istnieje.
* Występuje, gdy kontener jest usuwany, a następnie spróbuj toocreate nowy kontener z hello takie same nazwy, przed wykonaniem operacji usuwania hello.
* Występuje, gdy Określ dzierżawę na kontener lub obiekt blob, a jest już obecny dzierżawy.

**Kod stanu 412 (warunek wstępny nie powiodła się) przykłady**

* Występuje, gdy nie został spełniony warunek hello określony przez nagłówek warunkowy.
* Występuje, gdy określono Identyfikatora dzierżawy hello jest niezgodny z Identyfikatorem dzierżawy hello na powitania kontener lub obiekt blob.

## <a name="generate-log-files-for-analysis"></a>Generuj pliki dziennika do analizy
W tym samouczku użyjemy toowork analizatora komunikatów z trzech różnych typów plików dziennika, mimo że można wybrać toowork przy użyciu dowolnej z tych:

* Witaj **dziennik serwera**, który jest tworzony po włączeniu rejestrowania usługi Azure Storage. Dziennik serwera Hello zawiera dane dotyczące każdej operacji o nazwie względem jednej z usług Azure Storage hello — obiekt blob, kolejki, tabel i plików. Dziennik serwera Hello wskazuje operacja, która została wywołana i jakie kod stanu został zwrócony, a także inne szczegóły hello żądań i odpowiedzi.
* Witaj **dziennika klienta .NET**, który jest tworzony po włączeniu rejestrowania po stronie klienta z wewnątrz aplikacji .NET. powitania klienta dziennika zawiera szczegółowe informacje dotyczące sposobu powitania klienta przygotowuje hello żądania i odbiera i przetwarza hello odpowiedzi.
* Witaj **dziennika śledzenia sieci HTTP**, która zbiera dane na dane żądanie i odpowiedź HTTP/HTTPS, tym dla operacji w usłudze Azure Storage. W tym samouczku będziemy zostanie wygenerowany hello śledzenia sieci za pomocą analizatora komunikatów.

### <a name="configure-server-side-logging-and-metrics"></a>Konfigurowanie rejestrowania po stronie serwera i metryki
Najpierw potrzebujemy tooconfigure rejestrowania usługi Azure Storage i metryki, dzięki czemu będziemy mieć dane z powitania klienta aplikacji tooanalyze. Można skonfigurować rejestrowania i metryki na różne sposoby — za pośrednictwem hello [portalu Azure](https://portal.azure.com), za pomocą programu PowerShell, lub programowo. Zobacz [włączenie metryki magazynu i wyświetlanie danych metryk](http://msdn.microsoft.com/library/azure/dn782843.aspx) i [Włączanie rejestrowania magazynu i uzyskiwanie dostępu do danych dziennika](http://msdn.microsoft.com/library/azure/dn782840.aspx) w witrynie MSDN, aby uzyskać więcej informacji o konfigurowaniu rejestrowania i metryki.

**Za pomocą hello portalu Azure**

Rejestrowanie tooconfigure i metryk do konta magazynu przy użyciu hello [portalu Azure](https://portal.azure.com), postępuj zgodnie z instrukcjami hello w [monitorować konta magazynu w portalu Azure hello](storage-monitor-storage-account.md).

> [!NOTE]
> Nie jest możliwe tooset metryki minuty przy użyciu hello portalu Azure. Jednak zaleca się, że te elementy zostały skonfigurowane dla hello do celów tego samouczka i badania problemów dotyczących wydajności z aplikacją. Można ustawić minuty metryki przy użyciu programu PowerShell, jak pokazano poniżej, albo programowo z użyciem biblioteki klienta usługi storage hello.
> 
> Należy pamiętać, że w tym hello portalu Azure nie może wyświetlić metryki minuty, tylko metryki co godzinę.
> 
> 

**Za pomocą programu PowerShell**

tooget wprowadzenie do programu PowerShell dla usługi Azure, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

1. Użyj hello [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0) tooadd polecenia cmdlet okno programu PowerShell toohello konta użytkownika platformy Azure:
   
    ```powershell
    Add-AzureAccount
    ```

2. W hello **Zaloguj tooMicrosoft Azure** okna, wpisz adresy e-mail hello i hasło skojarzone z Twoim kontem. Azure służy do uwierzytelniania i zapisuje informacji o poświadczeniach hello, a następnie zamyka okno hello.
3. Ustaw hello domyślne konto usługi storage konta toohello magazynu używanego w samouczku hello, wykonując następujące polecenia w oknie programu PowerShell hello:
   
    ```powershell
    $SubscriptionName = 'Your subscription name'
    $StorageAccountName = 'yourstorageaccount'
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

4. Włącz rejestrowanie dla hello usługa Blob magazynu:
   
    ```powershell
    Set-AzureStorageServiceLoggingProperty -ServiceType Blob -LoggingOperations Read,Write,Delete -PassThru -RetentionDays 7 -Version 1.0
    ```

5. Włączyć metryki magazynu dla hello usługa Blob, dzięki czy tooset **- MetricsType** zbyt`Minute`:
   
    ```powershell
    Set-AzureStorageServiceMetricsProperty -ServiceType Blob -MetricsType Minute -MetricsLevel ServiceAndApi -PassThru -RetentionDays 7 -Version 1.0
    ```

### <a name="configure-net-client-side-logging"></a>Konfigurowanie rejestrowania klienta .NET
tooconfigure klienta rejestrowanie dla aplikacji .NET, Włącz diagnostykę .NET w pliku konfiguracyjnym aplikacji hello (plik web.config lub app.config). Zobacz [klienta rejestrowania z hello biblioteki klienta usługi Storage .NET](http://msdn.microsoft.com/library/azure/dn782839.aspx) i [klienta rejestrowania z hello Microsoft Azure Storage SDK for Java](http://msdn.microsoft.com/library/azure/dn782844.aspx) w witrynie MSDN, aby uzyskać szczegółowe informacje.

powitania klienta dziennika zawiera szczegółowe informacje dotyczące sposobu powitania klienta przygotowuje hello żądania i odbiera i przetwarza hello odpowiedzi.

Witaj biblioteki klienta usługi Storage przechowuje dane dziennika klienta w hello lokalizacji określonej w pliku konfiguracyjnym aplikacji hello (plik web.config lub app.config).

### <a name="collect-a-network-trace"></a>Zbieraj śledzenia ścieżek połączeń sieciowych
Aplikacja kliencka jest uruchomiona, można użyć toocollect analizatora komunikatów śledzenia sieci HTTP/HTTPS. Używa analizatora komunikatów [Fiddler](http://www.telerik.com/fiddler) na powitania zaplecza. Aby zebrać śledzenia sieci hello, zaleca się skonfigurowanie ruch HTTPS bez szyfrowania toorecord Fiddler:

1. Zainstaluj [Fiddler](http://www.telerik.com/download/fiddler).
2. Uruchom program Fiddler.
3. Wybierz **narzędzia | Opcje narzędzia fiddler**.
4. W oknie dialogowym Opcje hello, upewnij się, że **przechwytywania połączenie HTTPS** i **odszyfrowania ruchu HTTPS** są zaznaczone, jak pokazano poniżej.

![Skonfiguruj opcje Fiddler](./media/storage-e2e-troubleshooting/fiddler-options-1.png)

Samouczek hello zbierania i najpierw zapisać w analizatora komunikatów śledzenia sieci, a następnie utwórz analizy sesji tooanalyze hello śledzenia i hello dzienniki. toocollect śledzenia sieci w analizatora komunikatów:

1. Message Analyzer, wybierz **pliku | Szybkie śledzenia | Niezaszyfrowana HTTPS**.
2. śledzenia Hello rozpocznie się natychmiast. Wybierz **zatrzymać** toostop hello śledzenia tak, aby można go skonfigurować tootrace tylko ruch magazynu.
3. Wybierz **Edytuj** tooedit hello śledzenia sesji.
4. Wybierz hello **Konfiguruj** link toohello rogu hello **Microsoft-Pef-WebProxy** dostawcy ETW.
5. W hello **Zaawansowane ustawienia** okna dialogowego, kliknij przycisk hello **dostawcy** kartę.
6. W hello **filtru Hostname** Określ magazynu punktów końcowych, rozdzielając je spacjami. Na przykład można określić punktów końcowych Zmień `storagesample` toohello nazwę konta magazynu:

    ```   
    storagesample.blob.core.windows.net storagesample.queue.core.windows.net storagesample.table.core.windows.net
    ```

7. Zamknij okno dialogowe hello, a następnie kliknij przycisk **Uruchom ponownie** toobegin zbieranie hello śledzenia z filtrem hostname hello w miejscu, aby do śledzenia hello jest włączone tylko ruchu sieciowego magazynu Azure.

> [!NOTE]
> Po zakończeniu zbierania śledzenia sieci, zdecydowanie zaleca się aby przywrócić ustawienia hello, które zostały zmienione w ruchu HTTPS toodecrypt Fiddler. W oknie dialogowym Opcje Fiddler hello, odznacz opcję hello **przechwytywania połączenie HTTPS** i **odszyfrowania ruchu HTTPS** pola wyboru.
> 
> 

Zobacz [korzystanie z funkcji śledzenia sieci hello](http://technet.microsoft.com/library/jj674819.aspx) w witrynie Technet, aby uzyskać więcej informacji.

## <a name="review-metrics-data-in-hello-azure-portal"></a>Przejrzyj dane metryk w hello portalu Azure
Gdy aplikacja została uruchomiona w danym okresie czasu, można przejrzeć hello metryki wykresy, które są widoczne w hello [portalu Azure](https://portal.azure.com) tooobserve, jak usługa została wykonywania.

Przejdź najpierw tooyour konta magazynu w hello portalu Azure. Domyślnie monitorowanie wykres z hello **procent powodzenia** metryka jest wyświetlany w bloku konta hello. Jeśli wcześniej zmodyfikowano hello wykresu toodisplay różnych metryk, Dodaj hello **procent powodzenia** metryki.

Będą teraz widoczne **procent powodzenia** w hello monitorowania wykresu, wraz z innych metryk zostały dodane. W scenariuszu hello, które firma Microsoft będzie zbadać obok analizując dzienniki hello w Message Analyzer Częstotliwość powodzeń procent hello jest nieco poniżej 100%.

Więcej szczegółów na dodawanie i dostosowywanie metryki wykresy, zobacz [dostosowanie metryk wykresy](storage-monitor-storage-account.md#customize-metrics-charts).

> [!NOTE]
> Może upłynąć trochę czasu, zanim Twoje metryki tooappear danych w portalu Azure powitania po włączeniu metryki magazynu. Jest to spowodowane co godzinę metryki hello poprzedniej godziny nie są wyświetlane w hello portalu Azure, przed upływem hello bieżącej godziny. Ponadto metryki minutowe nie są aktualnie wyświetlane w portalu Azure hello. Dlatego w zależności od tego, po włączeniu metryki, może potrwać tootwo godziny toosee metryki danych.
> 
> 

## <a name="use-azcopy-toocopy-server-logs-tooa-local-directory"></a>Użyj narzędzia AzCopy toocopy serwera tooa lokalnego katalogu dzienników
Usługa Azure Storage zapisuje tooblobs danych dziennika serwera, gdy metryki są zapisywane tootables. Dziennik obiekty BLOB są dostępne w dobrze znanego hello `$logs` kontener dla konta magazynu. Obiekty BLOB dziennika są nazywane hierarchicznie przez rok, miesiąc, dzień i godzinę, dzięki czemu można łatwo zlokalizować hello zakres czasu, którego chcesz tooinvestigate. Na przykład w hello `storagesample` konto, hello kontenera obiektów blob dziennika hello for 01/02/2015 z 8-9 am, jest `https://storagesample.blob.core.windows.net/$logs/blob/2015/01/08/0800`. Witaj poszczególne obiekty BLOB w tym kontenerze są nazywane sekwencyjnie, począwszy od `000000.log`.

Toodownload narzędzia wiersza polecenia AzCopy hello można użyć wybranej tych lokalizacji tooa pliki dziennika po stronie serwera na komputerze lokalnym. Na przykład można użyć następujących plików dziennika hello toodownload polecenia dla operacji obiektu blob, które miały umieść na powitania folderu toohello 2 stycznia 2015 `C:\Temp\Logs\Server`; zastąpić `<storageaccountname>` hello nazwą konta magazynu i `<storageaccountkey>` z sieci klucz dostępu do konta:

```azcopy
AzCopy.exe /Source:http://<storageaccountname>.blob.core.windows.net/$logs /Dest:C:\Temp\Logs\Server /Pattern:"blob/2015/01/02" /SourceKey:<storageaccountkey> /S /V
```
Narzędzie AzCopy jest dostępny do pobrania na powitania [Azure pobiera](https://azure.microsoft.com/downloads/) strony. Aby uzyskać więcej informacji o używaniu narzędzia AzCopy, zobacz [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md).

Aby uzyskać dodatkowe informacje na temat pobierania dzienników po stronie serwera, zobacz [Pobierz rejestrowania magazynu danych dziennika](http://msdn.microsoft.com/library/azure/dn782840.aspx#DownloadingStorageLogginglogdata).

## <a name="use-microsoft-message-analyzer-tooanalyze-log-data"></a>Używanie programu Microsoft Message Analyzer tooanalyze dziennika danych
Programu Microsoft Message Analyzer jest narzędziem do przechwytywania, wyświetlania i analizowania ruchu, zdarzeń i inne komunikaty w scenariuszach rozwiązywania problemów i diagnozowania systemu lub aplikacji do obsługi komunikatów protokołu. Analizator komunikatów również umożliwia tooload agregacji i analizowania danych z dziennika i zapisane pliki śledzenia. Aby uzyskać więcej informacji na temat Message Analyzer, zobacz [Microsoft komunikatów analizatora operacyjnego przewodnik](http://technet.microsoft.com/library/jj649776.aspx).

Analizator komunikatów obejmuje zasoby usługi Azure Storage, które pomagają tooanalyze serwera i klienta oraz dzienniki sieci. W tej sekcji omówiono sposób toouse tooaddress tych narzędzi hello problem niskiej procent powodzenia w hello dzienniki magazynu.

### <a name="download-and-install-message-analyzer-and-hello-azure-storage-assets"></a>Pobierz i zainstaluj Message Analyzer i hello zasoby magazynu Azure
1. Pobierz [Message Analyzer](http://www.microsoft.com/download/details.aspx?id=44226) z hello Microsoft Download Center, a następnie uruchom Instalator hello.
2. Uruchom analizator komunikatów.
3. Z hello **narzędzia** menu, wybierz opcję **Menedżera zasobów**. W hello **Menedżera zasobów** okno dialogowe, wybierz opcję **pobiera**, następnie odfiltrować **usługi Azure Storage**. Zobaczysz hello zasobów magazynu Azure, pokazane na poniższej ilustracji hello.
4. Kliknij przycisk **wszystkie elementy wyświetlane synchronizacji** hello tooinstall zasoby magazynu Azure. Witaj dostępne zasoby obejmują:
   * **Reguły koloru magazynu Azure:** reguły koloru magazynu platformy Azure umożliwiają toodefine specjalne filtry używających kolor tekstu, i style toohighlight komunikaty, które zawierają określone informacje w śledzenia.
   * **Wykresy magazynu Azure:** wykresy magazynu Azure są wstępnie zdefiniowane wykresy, które dane dziennika dla serwera programu graph. Należy pamiętać, że toouse usługi Azure Storage wykresy w tej chwili może tylko obciążenia powitania serwera dziennika do hello analizy siatki.
   * **Azure magazynu analizatory składni:** hello Azure Storage analizatory składni analizy hello Azure Storage klienta, serwera i HTTP loguje w kolejności toodisplay ich hello analizy siatki.
   * **Filtry magazynu Azure:** filtry magazynu Azure są wstępnie zdefiniowane kryteria służącego tooquery danych w hello analizy siatki.
   * **Układy widoku magazynu Azure:** układów widoku magazynu Azure są układów wstępnie zdefiniowanych kolumn i grupowania w hello analizy siatki.
5. Po zainstalowaniu hello zasobów, należy ponownie uruchomić analizator komunikatów.

![Menedżera zasobów analizator komunikatów](./media/storage-e2e-troubleshooting/mma-start-page-1.png)

> [!NOTE]
> Zainstaluj wszystkie zasoby usługi Azure Storage hello pokazano hello celów tego samouczka.
> 
> 

### <a name="import-your-log-files-into-message-analyzer"></a>Importowanie plików dzienników do analizatora komunikatów
Można importować wszystkie zapisane pliki dziennika (po stronie serwera, po stronie klienta i sieci) w jednej sesji w programu Microsoft Message Analyzer do analizy.

1. Na powitania **pliku** kliknij menu programu Microsoft Message Analyzer **nowej sesji**, a następnie kliknij przycisk **puste sesji**. W hello **nowej sesji** okna dialogowego, wprowadź nazwę dla sesji analizy. W hello **szczegółowych informacji o sesji** panelu, kliknij na powitania **pliki** przycisku.
2. polecenie tooload hello śledzenia danych sieci generowane przez analizator komunikatów **Dodaj pliki**, przeglądanie toohello lokalizacji pliku .matp z sesji śledzenia sieci web, wybierz hello .matp pliku, i kliknij przycisk **Otwórz**.
3. dane dziennika po stronie serwera hello tooload, wybierz polecenie **Dodaj pliki**, Przeglądaj toohello której pobrano dzienników po stronie serwera, wybierz hello plików dziennika dla zakresu czasu hello tooanalyze i kliknij **Otwórz**. Następnie w hello **szczegółowych informacji o sesji** panelu, zestaw hello **konfiguracji dziennika tekstowego** listy rozwijanej dla każdego pliku dziennika po stronie serwera za**AzureStorageLog** tooensure używanej przez firmę Microsoft Analizator komunikatów można poprawnie przeanalizować pliku dziennika hello.
4. dane dziennika klienta hello tooload, wybierz polecenie **Dodaj pliki**, Przeglądaj toohello lokalizacji dzienników po stronie klienta, wybierz pliki dziennika hello tooanalyze i kliknij **Otwórz**. Następnie w hello **szczegółowych informacji o sesji** panelu, zestaw hello **konfiguracji dziennika tekstowego** listy rozwijanej dla każdego pliku dziennika po stronie klienta za**AzureStorageClientDotNetV4** tooensure który Programu Microsoft Message Analyzer można poprawnie przeanalizować pliku dziennika hello.
5. Kliknij przycisk **Start** w hello **nowej sesji** tooload i analizy hello dziennika danych w oknie dialogowym. dane dziennika Hello Wyświetla hello siatka analizy analizator komunikatów.

Obraz powitania poniżej przedstawia sesji przykład skonfigurowane z serwera, klienta i pliki dziennika śledzenia sieci.

![Konfigurowanie sesji analizator komunikatów](./media/storage-e2e-troubleshooting/configure-mma-session-1.png)

Należy pamiętać, że analizator komunikatów ładuje pliki dziennika do pamięci. Jeśli masz dużych zestawów danych dziennika można toofilter w kolejności tooget hello najlepszą wydajność z analizatora komunikatów.

Najpierw należy określić przedział czasu hello będące zrecenzować i ramce czasu możliwie jak najmniejszy. W wielu przypadkach można tooreview okres minut lub godziny Max. Importuj hello najmniejszy zestaw dzienników, które mogą zaspokoić potrzeb.

Jeśli masz dużą ilość danych dziennika można toospecify toofilter filtru sesji danych dziennika przed rozpoczęciem ładowania. W hello **filtru sesji** okno, wybierz hello **biblioteki** przycisk toochoose wstępnie zdefiniowany filtr; na przykład wybrać **globalne czasu filtru I** z hello filtrów usługi Azure Storage toofilter w przedziale czasu. Następnie można edytować hello filtru kryteria toospecify hello uruchamianie i kończenie sygnatury czasowej dla interwału powitania ma toosee. Można również filtrować według określony kod stanu; na przykład można wybrać tylko wpisy dziennika tooload, gdy kod stanie hello jest 404.

Aby uzyskać więcej informacji na temat importowania danych dziennika do programu Microsoft Message Analyzer, zobacz [pobierania danych komunikat](http://technet.microsoft.com/library/dn772437.aspx) w witrynie TechNet.

### <a name="use-hello-client-request-id-toocorrelate-log-file-data"></a>Użyj danych pliku dziennika toocorrelate identyfikator powitania klienta żądania
Witaj biblioteki klienta magazynu Azure automatycznie generuje identyfikator żądania klienta unikatowy dla każdego żądania. Ta wartość jest zapisywany toohello dziennika klienta, powitania serwera dziennika i śledzenia sieci hello, aby można było ich użyć toocorrelate danych we wszystkich trzech dzienników w analizatora komunikatów. Zobacz [Identyfikatora żądania klienta](storage-monitoring-diagnosing-troubleshooting.md#client-request-id) Aby uzyskać dodatkowe informacje o kliencie hello żądania identyfikatora.

w poniższych rozdziałach Hello opisano, jak toouse wstępnie skonfigurowanej z widokami niestandardowego układu danych toocorrelate i grupy na podstawie powitania klienta żądania identyfikatora.

### <a name="select-a-view-layout-toodisplay-in-hello-analysis-grid"></a>Wybierz toodisplay układ widoku hello analizy siatki
Witaj zasobów pamięci masowej dla analizatora komunikatów obejmują układów widoku magazynu Azure, które są wstępnie skonfigurowane widoki, której można toodisplay danych kolumn i grupowania przydatne dla różnych scenariuszy. Można również utworzyć widok niestandardowy układy i zapisywać je do ponownego użycia.

Obraz powitania poniżej przedstawia hello **układ widoku** menu dostępne po wybraniu **układ widoku** hello na wstążce narzędzi programu. Witaj układów widoku dla usługi Azure Storage są zgrupowane w hello **usługi Azure Storage** węzła w hello menu. Możesz wyszukać `Azure Storage` toofilter pole wyszukiwania hello w magazynie Azure przeglądać tylko układów. Możesz też wybrać hello gwiazdy dalej tooa widoku układu toomake it a elementu ulubionego i wyświetl ją u góry hello hello menu.

![Menu Widok układu](./media/storage-e2e-troubleshooting/view-layout-menu.png)

toobegin z wybierz **pogrupowane według ClientRequestID i modułu**. Ten widok Układ grup dziennika najpierw danych ze wszystkich trzech dzienników, identyfikator żądania klienta, a następnie plik dziennika źródła (lub **modułu** w analizator komunikatów). Z tym widokiem można przejść do Identyfikatora żądania klienta określonego i wyświetlać dane ze wszystkich trzech plików dziennika dla tego żądania klienta identyfikatora.

Hello obraz poniżej przedstawia tego układu widoku stosowane toohello przykładowych danych dziennika, z podzbiorem wyświetlane kolumny. Widać, że dla określonego Identyfikatora żądania klienta, hello siatki analizy są wyświetlane dane z hello dziennika klienta, serwera dziennika i śledzenia ścieżek połączeń sieciowych.

![Układ widoku magazynu Azure](./media/storage-e2e-troubleshooting/view-layout-client-request-id-module.png)

> [!NOTE]
> Różnych plikach dziennika mają różne kolumny, gdy dane z wielu plików dziennika są wyświetlane w hello analizy siatki, niektóre kolumny nie może zawierać żadnych danych dla danego wiersza. Na przykład hello ilustracji powyżej wierszy dziennika klienta są wyświetlane wszystkie dane dotyczące hello **sygnatury czasowej**, **TimeElapsed**, **źródła**, i **docelowego** kolumn, ponieważ te kolumny nie istnieją w hello dziennika klienta, ale istnieje w hello śledzenia sieci. Podobnie, hello **sygnatury czasowej** kolumna zawiera dane sygnatury czasowej powitania serwera dziennika, ale żadne dane nie są wyświetlone dla hello **TimeElapsed**, **źródła**, i  **Docelowy** kolumn, które nie są częścią hello dziennik serwera.
> 
> 

Ponadto toousing hello Azure Storage układów widoku, można również zdefiniować i zapisać układów widoku. Można wybrać inne wymagane pola do grupowania danych i zapisać grupowania hello jako część programu niestandardowego układu.

### <a name="apply-color-rules-toohello-analysis-grid"></a>Zastosuj toohello reguły kolor siatki analizy
Zasoby magazynu Hello także reguły koloru, które oferują element wizualny oznacza tooidentify różnych typów błędów w hello analizy siatki. Hello kolor wstępnie zdefiniowane reguły stosowane tooHTTP błędów, aby były wyświetlane tylko w przypadku śledzenia serwera hello dziennika i sieci.

Wybierz reguły koloru tooapply, **reguły koloru** hello wstążce narzędzi. Zobaczysz reguły koloru usługi Azure Storage hello hello menu. Samouczek hello wybierz **klientów z błędami (StatusCode w przedziale od 400 do 499)**, jak pokazano na rysunku hello poniżej.

![Układ widoku magazynu Azure](./media/storage-e2e-troubleshooting/color-rules-menu.png)

Ponadto toousing hello Azure Storage kolor reguł, można również zdefiniować i zapisać reguły koloru.

### <a name="group-and-filter-log-data-toofind-400-range-errors"></a>Grupy i filtrowanie danych toofind 400-range błędy dziennika
Następnie firma Microsoft będzie grupy i filtrować toofind danych dziennika hello wszystkie błędy w zakresie hello 400.

1. Zlokalizuj hello **StatusCode** kolumny w hello analizy siatki, kolumny powitania kliknij prawym przyciskiem myszy nagłówek i wybierz **grupy**.
2. Następnie grupy na powitania **ClientRequestId** kolumny. Zobaczysz czy dane hello powitalne siatki analizy teraz jest zorganizowana według stanu kodu i na żądanie klienta identyfikatora.
3. Wyświetlanie okna narzędzia hello filtr widoku, jeśli nie jest już wyświetlany. Na wstążce narzędzi hello, wybierz **okna narzędzi**, następnie **filtr widoku**.
4. toofilter hello danych toodisplay tylko zakres 400 błędy dziennika, Dodaj powitania po toohello kryteria filtru **filtr widoku** okna, a następnie kliknij przycisk **Zastosuj**:

    ```   
    (AzureStorageLog.StatusCode >= 400 && AzureStorageLog.StatusCode <=499) || (HTTP.StatusCode >= 400 && HTTP.StatusCode <= 499)
    ```

Obraz powitania poniżej przedstawia wyniki hello to grupowanie i filtrowanie. Powiększające hello **ClientRequestID** pole poniżej hello grupowanie dla kodu stanu 409, na przykład przedstawia operację, która spowodowała ten kod stanu.

![Układ widoku magazynu Azure](./media/storage-e2e-troubleshooting/400-range-errors1.png)

Po zastosowaniu tego filtru, zobaczysz, że wiersze z dziennika klienta hello są wyłączone, jako hello dziennika klienta nie zawiera **StatusCode** kolumny. toobegin z, firma Microsoft może przejrzeć serwera hello i błędów 404 toolocate dzienniki śledzenia sieci, a następnie zostanie zwrócona toohello klienta dziennika tooexamine powitania klienta operacje, które doprowadziły toothem.

> [!NOTE]
> Można filtrować według hello **StatusCode** kolumny i Wyświetl dane ze wszystkich trzech dzienników, w tym hello dziennika klienta, jeśli dodasz filtru toohello wyrażeń, która zawiera wpisy dziennika, gdy kod stanu hello jest null. tooconstruct to wyrażenie filtru, użyj:
> 
> <code>&#42;StatusCode >= 400 or !&#42;StatusCode</code>
> 
> Ten filtr zwraca wszystkie wiersze z powitania klienta dziennika i tylko wiersze z powitania serwera dziennika i dzienników HTTP których hello kod stanu jest większa niż 400. W przypadku zastosowania go układ widoku toohello pogrupowane według Identyfikatora żądania klienta i modułów, umożliwia wyszukiwanie lub przewiń hello dziennika toofind wpisy tych, których wszystkie trzy dzienniki są reprezentowane.   
> 
> 

### <a name="filter-log-data-toofind-404-errors"></a>Filtrowanie błędów 404 toofind dane dziennika
Zasoby magazynu Hello zawierają wstępnie zdefiniowane filtry, które można użyć toonarrow dziennika danych toofind hello błędy lub trendy, którego szukasz. Następnie będzie zastosować dwa filtry wstępnie zdefiniowane: jeden filtrujące powitania serwera i błędów 404 dzienniki śledzenia sieci i który filtry hello dane dotyczące określonego przedziału czasu.

1. Wyświetlanie okna narzędzia hello filtr widoku, jeśli nie jest już wyświetlany. Na wstążce narzędzi hello, wybierz **okna narzędzi**, następnie **filtr widoku**.
2. W oknie filtru widoku hello wybierz **biblioteki**i wyszukiwania na `Azure Storage` hello toofind filtrów usługi Azure Storage. Filtr wybierz hello **404 (nie znaleziono) wiadomości we wszystkich dziennikach**.
3. Wyświetl hello **biblioteki** menu ponownie i Znajdź i zaznacz hello **globalny filtr czasu**.
4. Edytuj sygnatury czasowe hello pokazane w zakresie toohello filtru hello mają tooview. Pomoże to zakres hello toonarrow tooanalyze danych.
5. Filtr powinien zostać wyświetlony podobny przykład toohello poniżej. Kliknij przycisk **Zastosuj** tooapply hello filtru toohello analizy siatki.

    ```   
    ((AzureStorageLog.StatusCode == 404 || HTTP.StatusCode == 404)) And
    (#Timestamp >= 2014-10-20T16:36:38 and #Timestamp <= 2014-10-20T16:36:39)
    ```

    ![Układ widoku magazynu Azure](./media/storage-e2e-troubleshooting/404-filtered-errors1.png)

### <a name="analyze-your-log-data"></a>Analizowanie danych dziennika
Teraz, grupowane i filtrować dane należy zbadać szczegóły hello poszczególnych żądań, które wygenerowały błędy 404. W hello bieżący układ widoku dane hello są grupowane według Identyfikatora żądania klienta, następnie według źródła dziennika. Firma Microsoft filtrowania żądań hello StatusCode polu, w którym znajduje się 404, firma Microsoft będzie wyświetlanych tylko powitania serwera i danych śledzenia sieci, nie hello dane dziennika klienta.

Obraz powitania poniżej zawiera określone żądanie gdzie operacji pobrania obiektu Blob zwróciło 404, ponieważ hello obiektu blob nie istnieje. Należy pamiętać, że niektóre kolumny zostały usunięte z widoku standardowym hello w kolejności toodisplay hello odpowiednie dane.

![Filtrowane Server i dzienniki śledzenia sieci](./media/storage-e2e-troubleshooting/server-filtered-404-error.png)

Następnie firma Microsoft będzie mieć związek tego Identyfikatora żądania klienta z powitania klienta dziennika danych toosee miał jakie akcje powitania klienta, gdy wystąpił błąd hello. Można wyświetlić nowy widok siatki analizy dla tej sesji tooview powitania klienta dziennika danych, który zostanie otwarty w drugiej karty:

1. Najpierw skopiuj wartość hello hello **ClientRequestId** pola toohello Schowka. Można to zrobić, wybierając albo wiersza lokalizowanie hello **ClientRequestId** pola wartości danych hello prawym przyciskiem myszy i wybierając pozycję **kopii "ClientRequestId"**.
2. Na wstążce narzędzi hello, wybierz **nowy podgląd**, a następnie wybierz pozycję **siatki analizy** tooopen na nowej karcie nowe hello kartę przedstawia wszystkie dane w plikach dziennika bez grupowania, filtrowania lub reguły koloru.
3. Na wstążce narzędzi hello, wybierz **układ widoku**, a następnie wybierz pozycję **wszystkie kolumny klienta .NET** w obszarze hello **usługi Azure Storage** sekcji. Ten układ widok zawiera dane ze hello dziennika klienta, a także hello dzienniki śledzenia serwera i sieci. Domyślnie jest sortowana na powitania **MessageNumber** kolumny.
4. Następnie wyszukaj powitania klienta dziennika identyfikator powitania klienta żądania. Na wstążce narzędzi hello, wybierz **znaleźć wiadomości**, następnie określenia niestandardowego filtru na powitania Identyfikatora żądania klienta w hello **znaleźć** pola. Dla filtru hello, określając własnego Identyfikatora żądania klienta, należy użyć następującej składni:

    ```
    *ClientRequestId == "398bac41-7725-484b-8a69-2a9e48fc669a"
    ```

Analizator komunikatów lokalizuje i wybiera pierwszy wpis dziennika hello, jeśli kryteria wyszukiwania hello odpowiada identyfikator powitania klienta żądania. W hello dziennika klienta, istnieje kilka wpisów dla każdego Identyfikatora żądania klienta, dlatego może być toogroup ich na powitania **ClientRequestId** toomake pola go toosee łatwiej je wszystkie. Obraz powitania poniżej przedstawia wszystkie wiadomości powitania klienta hello dziennika dla hello określony identyfikator żądania klienta.

![Wyświetlanie dziennika klienta błędów 404](./media/storage-e2e-troubleshooting/client-log-analysis-grid1.png)

Przy użyciu hello dane wyświetlane w hello układów widoku w tych dwóch kart, można przeanalizować hello żądania danych toodetermine co spowodowało błąd hello. Można również przyjrzeć się żądań, które poprzedzone to jeden toosee, jeśli poprzednie zdarzenie może spowodowały toohello błąd 404. Na przykład możesz przejrzeć wpisy dziennika klienta hello poprzedzających tego toodetermine identyfikator żądania klienta, czy hello blob mogła zostać usunięta, czy błąd hello powodu aplikacji klienckiej toohello wywołanie CreateIfNotExists API w kontenerze lub obiektu blob. W dzienniku powitania klienta można znaleźć adres hello obiektu blob w hello **opis** pola; w hello server i dzienniki śledzenia sieci, informacje te pojawiają się w hello **Podsumowanie** pola.

Gdy znasz adres hello hello obiektu blob, które zwróciło błąd hello 404, można zbadać dalej. Wyszukiwania hello wpisy dziennika dla innych komunikatów skojarzonych z operacji na powitania sam obiektu blob, można sprawdzić, czy powitania klienta wcześniej usunięty hello jednostki.

## <a name="analyze-other-types-of-storage-errors"></a>Analizowanie inne typy błędów magazynu
Teraz, po zapoznaniu się z przy użyciu analizatora komunikatów tooanalyze danych dziennika, można przeanalizować inne typy błędów przy użyciu widoku układów, reguły koloru i wyszukiwanie filtrowania. Witaj tabele poniżej listy problemy mogą wystąpić i hello kryteria filtrowania, można użyć toolocate je. Aby uzyskać więcej informacji na temat tworzenia filtrów i hello Message Analyzer filtrowania języka, zobacz [filtrowania danych komunikat](http://technet.microsoft.com/library/jj819365.aspx).

| tooInvestigate... | Użycie wyrażenia filtru... | Wyrażenie stosuje tooLog (klienta, serwera, sieci, wszystkie) |
| --- | --- | --- |
| Nieoczekiwane opóźnienia dotyczące dostarczania wiadomości w kolejce |Zawiera AzureStorageClientDotNetV4.Description "Ponawianie nie można wykonać operacji." |Klient |
| HTTP wzrost PercentThrottlingError |PROTOKÓŁ HTTP. Response.StatusCode == 500 &#124; &#124; PROTOKÓŁ HTTP. Response.StatusCode == 503 |Sieć |
| Wzrost PercentTimeoutError |PROTOKÓŁ HTTP. Response.StatusCode == 500 |Sieć |
| Wzrost PercentTimeoutError (wszystkie wersje) |* StatusCode == 500 |Wszystkie |
| Wzrost PercentNetworkError |AzureStorageClientDotNetV4.EventLogEntry.Level < 2 |Klient |
| Komunikaty HTTP 403 (zabroniony) |PROTOKÓŁ HTTP. Response.StatusCode == 403 |Sieć |
| HTTP 404 (nie znaleziono) wiadomości |PROTOKÓŁ HTTP. Response.StatusCode == 404 |Sieć |
| 404 (wszystkie wersje) |* StatusCode == 404 |Wszystkie |
| Udostępnione problem autoryzacji podpis dostępu (SAS) |AzureStorageLog.RequestStatus == "SASAuthorizationError" |Sieć |
| HTTP 409 (konflikt) wiadomości |PROTOKÓŁ HTTP. Response.StatusCode == 409 |Sieć |
| 409 (wszystkie wersje) |* StatusCode == 409 |Wszystkie |
| Działania o stanie transakcji ClientOtherErrors ma PercentSuccess małej lub analityka wpisy dziennika |AzureStorageLog.RequestStatus == "ClientOtherError" |Serwer |
| Ostrzeżenie Nagle'a |((AzureStorageLog.EndToEndLatencyMS-AzureStorageLog.ServerLatencyMS) > (AzureStorageLog.ServerLatencyMS * 1.5)) i (AzureStorageLog.RequestPacketSize < 1460) i (AzureStorageLog.EndToEndLatencyMS - AzureStorageLog.ServerLatencyMS > = 200) |Serwer |
| Zakres czasu w dziennikach serwera i sieci |#Timestamp > = 2014-10-20T16:36:38 i #Timestamp < = 2014-10-20T16:36:39 |Serwer, sieci |
| Zakres czasu w dziennikach serwera |AzureStorageLog.Timestamp > = 2014-10-20T16:36:38 i AzureStorageLog.Timestamp < = 2014-10-20T16:36:39 |Serwer |

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat rozwiązywania problemów scenariuszy end-to-end w usłudze Azure Storage zobacz następujące zasoby:

* [Monitorowanie, diagnozowanie i rozwiązywanie problemów z usługi Magazyn Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md)
* [Analityka magazynu](http://msdn.microsoft.com/library/azure/hh343270.aspx)
* [Monitor konta magazynu w hello portalu Azure](storage-monitor-storage-account.md)
* [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md)
* [Przewodnik operacyjny analizatora wiadomości firmy Microsoft](http://technet.microsoft.com/library/jj649776.aspx)
