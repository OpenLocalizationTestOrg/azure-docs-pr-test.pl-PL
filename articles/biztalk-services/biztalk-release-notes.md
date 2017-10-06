---
title: "aaaRelease uwagi dotyczące usług BizTalk Azure | Dokumentacja firmy Microsoft"
description: "Wyświetla listę hello znane problemy dotyczące usług Azure BizTalk"
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: f4906fdc-4cd9-4a57-a007-a88c2e51a18f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: ea53d6c40ed58badf4141453dc77d28dcfc6407f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-biztalk-services"></a>Informacje o wersji dla usługi Azure BizTalk Services

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Witaj informacje o wersji dla usługi BizTalk hello Microsoft Azure zawierają hello znane problemy występujące w tej wersji.

## <a name="whats-new-in-hello-november-update-of-biztalk-services"></a>Nowości w aktualizacji listopada hello usługi BizTalk Services
* Można włączyć szyfrowanie przechowywanych w hello Portal usługi BizTalk. Zobacz [włączyć szyfrowanie przechowywanych w portalu usługi BizTalk](https://msdn.microsoft.com/library/azure/dn874052.aspx).

## <a name="update-history"></a>Historia aktualizacji
### <a name="october-update"></a>Aktualizacja z października
* Konta organizacyjne są obsługiwane:  
  * **Scenariusz**: zarejestrowany wdrażania usługi BizTalk przy użyciu konta Microsoft (takich jak user@live.com). W tym scenariuszu tylko Account Microsoft użytkownicy mogą zarządzać hello przy użyciu portalu usługi BizTalk Services hello usługi BizTalk. Nie można użyć konta organizacyjnego.  
  * **Scenariusz**: zarejestrowanych w usłudze Azure Active Directory za pomocą konta organizacyjnego wdrożenia usługi BizTalk (takich jak user@fabrikam.com lub user@contoso.com). W tym scenariuszu tylko użytkownicy usługi Azure Active Directory w ramach tej samej organizacji można zarządzać powitalne hello przy użyciu portalu usługi BizTalk Services hello usługi BizTalk. Nie można użyć konta Microsoft.  
* Podczas tworzenia usługi BizTalk w hello klasycznego portalu Azure, są automatycznie rejestrowane w portalu usługi BizTalk hello.
  * **Scenariusz**: możesz zalogować się do klasycznego portalu Azure, hello Utwórz usługę BizTalk, a następnie wybierz **Zarządzaj** dla hello pierwszego. Po otwarciu portalu usługi BizTalk Services hello hello usługi BizTalk automatycznie rejestruje i jest gotowy do wdrożeń.  
    Zobacz [rejestrowanie i aktualizowanie wdrożenia usługi BizTalk w portalu usługi BizTalk hello](https://msdn.microsoft.com/library/azure/hh689837.aspx).  

### <a name="august-14-update"></a>Aktualizacja z sierpnia 14
* Umowy oraz Mostek oddzielenie — umów z partnerami i mostków teraz jest całkowicie niezależna hello Portal usługi BizTalk. Teraz Utwórz umowy i mostków oddzielnie, a w mostków środowiska uruchomieniowego rozpoznać na podstawie wartości hello w wiadomości powitania EDI umowy tooan. Zobacz [Tworzenie umów w usług Azure BizTalk](https://msdn.microsoft.com/library/azure/hh689908.aspx), [utworzyć mostek EDI przy użyciu portalu usługi BizTalk](https://msdn.microsoft.com/library/azure/dn793986.aspx), [utworzyć mostek AS2 przy użyciu portalu usługi BizTalk](https://msdn.microsoft.com/library/azure/dn793993.aspx)i [ Jak mostków usunąć umowy w czasie wykonywania](https://msdn.microsoft.com/library/azure/dn794001.aspx)  
* Hello opcja toocreate szablonów dla umowy jest przerywane.  
* Powitania po stronie wysyłania umowy można teraz określić ogranicznik różne zestawy dla każdego schematu. Ta konfiguracja jest wybranym w ustawieniach protokołu umowy po stronie wysyłania. Aby uzyskać więcej informacji, zobacz [Utwórz moduł X12 umowy w usłudze Azure BizTalk Services](https://msdn.microsoft.com/library/azure/hh689847.aspx) i [Tworzenie umów EDIFACT w usług Azure BizTalk](https://msdn.microsoft.com/library/azure/dn606267.aspx). Dwa nowe jednostki zostaną także dodane toohello API OM modułu TPM na powitania tych samych celów. Zobacz [X12DelimiterOverrides](https://msdn.microsoft.com/library/azure/dn798749.aspx) i [EDIFACTDelimiterOverride](https://msdn.microsoft.com/library/azure/dn798748.aspx).  
* Konstrukcje XSD, łącznie z typów pochodnych, są teraz obsługiwane. Zobacz [XSD standardowych użyj konstrukcji w map](https://msdn.microsoft.com/library/azure/dn793987.aspx) i [Użyj typów pochodnych w przykłady i scenariusze mapowania](https://msdn.microsoft.com/library/azure/dn793997.aspx).  
* AS2 obsługuje nowych algorytmów Mikrofon do podpisywania wiadomości i nowych algorytmów szyfrowania. Zobacz [Tworzenie umów AS2 w usługach Azure BizTalk](https://msdn.microsoft.com/library/azure/hh689890.aspx).  
  ## <a name="know-issues"></a>Znać problemów

### <a name="connectivity-issues-after-biztalk-services-portal-update"></a>Problemy z połączeniem po aktualizacji portalu usług BizTalk
  Jeśli masz hello otworzyć Portal usługi BizTalk, gdy trwa uaktualnianie usługi BizTalk Services tooroll w zmiany toohello usługi, może sprostać problemy z łącznością z hello Portal usługi BizTalk.  
  Jako obejście może ponownie uruchomić przeglądarkę hello, usunąć pamięci podręcznej przeglądarki hello lub start portalu hello w trybie prywatnym.  

### <a name="visual-studio-ide-cannot-locate-hello-artifact-if-you-click-an-error-or-warning-in-a-biztalk-services-project"></a>Środowiska IDE programu Visual Studio nie może zlokalizować artefaktu hello, jeśli klikniesz przycisk błąd lub ostrzeżenie w projekcie usługi BizTalk Services
Zainstaluj problem hello toofix hello Visual Studio 2012 Update 3 RC 1.  

### <a name="custom-binding-project-reference"></a>Odwołanie do niestandardowego powiązania projektu
Należy wziąć pod uwagę hello następujące sytuacje z usługi BizTalk Services projektu w rozwiązaniu Visual Studio:  

* W hello na tym samym rozwiązaniu Visual Studio, jest projektem usługi BizTalk Services i projektu niestandardowego powiązania. Witaj projektu usługi BizTalk istnieje plik projektu odwołanie toothis niestandardowego powiązania.
* Hello projektu usługi BizTalk ma odwołania tooa niestandardowego powiązania/zachowanie biblioteki DLL.

Rozwiązanie programu Visual Studio możesz "Kompilacji" hello pomyślnie. Następnie "Odbudować" lub "Czysta" hello rozwiązania. Po wykonaniu tej odbudować lub oczyszczania ponownie hello następującego błędu:  
  Plik toocopy <Path tooDLL> too"bin\Debug\FileName.dll". proces Hello nie może uzyskać dostępu pliku hello "bin\Debug\FileName.dll", ponieważ jest on używany przez inny proces.  

#### <a name="workaround"></a>Obejście problemu
* Jeśli [Visual Studio 2012 Update 3](https://www.microsoft.com/download/details.aspx?id=39305) jest zainstalowany, masz hello następujące dwie opcje:
  
  * Uruchom ponownie program Visual Studio lub
  * Uruchom ponownie rozwiązanie hello. Następnie należy wykonać tylko kompilacji na powitania rozwiązania.  
* Jeśli [Visual Studio 2012 Update 3](https://www.microsoft.com/download/details.aspx?id=39305) jest nie jest zainstalowany, otwórz Menedżera zadań, kliknij kartę procesów powitania kliknij hello MSBuild.exe procesu i kliknij przycisk Zakończ proces hello.  

### <a name="routing-toobasichttprelay-endpoints-is-not-supported-from-bridges-and-biztalk-services-portal-if-non-printable-characters-are-promoted-as-http-headers"></a>Routing tooBasicHttpRelay punktów końcowych nie jest obsługiwana w portalu usługi BizTalk i mostków czy znaki niedrukowalne są awansowane nagłówki HTTP
Jeśli używasz niedrukowalne znaki jako część awansowanej właściwości komunikatów o tych wiadomości nie może być routingiem toorelay miejsc docelowych, korzystające z hello BasicHttpRelay wiązania. Ponadto hello awansowane właściwości, które są dostępne jako część śledzenia są zakodowane w adresie URL dla obiektów blob i cofanie zakodowanego dla miejsc docelowych.  

### <a name="mdn-is-sent-asynchronously-even-if-hello-send-asynchronous-mdn-option-is-unchecked"></a>MDN są wysyłane asynchronicznie, nawet jeśli hello Wysyłanie asynchroniczne MDN opcja jest zaznaczona
Rozważmy scenariusz, w tym — w przypadku wybrania hello **Wysyłanie asynchroniczne MDN** wyboru i określ adres URL async hello toosend MDN i usuń zaznaczenie hello **Wysyłanie asynchroniczne MDN** wyboru ponownie, hello MDN jest nadal adres URL określony toohello wysłane, nawet jeśli nie wybrano hello opcja toosend async MDNs.  
Jako obejście, należy wyczyścić hello określony adres URL przed zaznaczenie pola wyboru hello **Wysyłanie asynchroniczne MDN** pole wyboru, a następnie wdrożyć hello AS2 umowy.  

### <a name="whitespace-characters-beyond-a-valid-interchange-cause-an-empty-message-toobe-sent-toohello-suspend-endpoint"></a>Odstęp poza przyczyny prawidłowy wymiany toohello toobe wysyłane wiadomości pusty zawiesić punktu końcowego
W przypadku białe znaki poza segment IEA dezasembler hello traktuje tego jako końca bieżącego wymiany i analizuje następny zestaw hello odstępy jako następny komunikat. Ponieważ to nie jest prawidłową wymiany, widoczny czy jeden pomyślne komunikat jest wysyłany toohello docelowy trasy i jeden pusty komunikat jest wysyłany hello zawiesić punktu końcowego.  

### <a name="tracking-in-biztalk-services-portal"></a>Śledzenie w portalu usługi BizTalk
Zdarzenia śledzenia są przechwytywane przetwarzania komunikatów EDI toohello i wszelkie korelacji. W przypadku niepowodzenia komunikat poza hello etap protokołu śledzenia zostaną wyświetlone pomyślnym przeprowadzeniu. W takiej sytuacji można znaleźć w sekcji dziennika toohello hello **szczegóły** kolumny w **śledzenia** szczegóły błędów.
Witaj X12 odbierania i wysyłania ustawień ([Utwórz moduł X12 umowy w usłudze Azure BizTalk Services](https://msdn.microsoft.com/library/azure/hh689847.aspx)) zawierają informacje na powitania etap protokołu.  

### <a name="update-agreement"></a>Aktualizowanie umowy
Hello Portal usługi BizTalk umożliwia hello toomodify kwalifikator tożsamości Umowa jest skonfigurowany. Może to spowodować właściwości jest niezgodna. Na przykład istnieje umowa przy użyciu ZZ:1234567 i ZZ:7654321 hello kwalifikatora. W ustawieniach profilu Portal usługi BizTalk hello możesz zmienić ZZ:1234567 toobe 01:ChangedValue. Otwórz umowę hello i 01:ChangedValue jest wyświetlany zamiast ZZ:1234567.
toomodify hello kwalifikator tożsamości, Usuń hello umowy, zaktualizuj **tożsamości** w hello profil partnera, a następnie utwórz ponownie hello umowy.  

> AZURE. Ostrzeżenie zachowanie tej wpływa na X12 i AS2.  
> 
> 

### <a name="as2-attachments"></a>Załączniki AS2
Załączniki wiadomości nie są obsługiwane w AS2 wysyłać ani odbierać. W szczególności załączników dyskretnie są ignorowane, a treść wiadomości powitania jest przetwarzany jako zwykłe wiadomości AS2.  

### <a name="resources-remembering-path"></a>Zasoby: Ścieżka zapamiętywanie
Podczas dodawania **zasobów**, okno dialogowe hello nie może pamiętać hello tooadd wcześniej użyta ścieżka zasobu. tooremember hello wcześniej używane ścieżki, spróbuj Dodawanie witryny sieci web portalu usługi BizTalk hello zbyt**Zaufane witryny** w programie Internet Explorer.  

### <a name="if-you-rename-hello-entity-name-of-a-bridge-and-close-hello-project-without-saving-changes-opening-hello-entity-again-results-in-an-error"></a>Jeśli zmienisz nazwę jednostki hello mostek i hello Zamknij projekt bez zapisywania zmian ponownie otworzyć jednostki hello powoduje wystąpienie błędu
Rozważmy scenariusz, w następującej kolejności hello:  

* Dodaj tooa Mostek (na przykład XML One-Way mostek) projektu usługi BizTalk  
* Zmień nazwę Mostek hello, określając wartość hello Właściwość Nazwa jednostki. To polecenie zmienia hello .bridgeconfig skojarzony plik o podanej nazwy hello.  
* Zamknij plik .bcs hello (zamykając kartę hello w programie Visual Studio) bez zapisywania zmian hello.  
* Ponownie otworzyć plik .bcs hello z hello Eksploratora rozwiązań.  
  Można zauważyć, że podczas hello .bridgeconfig skojarzony plik ma hello nowe określona nazwa, nazwa jednostki hello na powierzchni projektowej hello jest nadal hello starej nazwy. Jeśli spróbujesz hello tooopen konfiguracji mostu przez dwukrotne kliknięcie hello Mostek składnika można uzyskać hello następujący błąd:  
  `‘<old name>’ Entity’s associated file ‘<old name>.bridgeconfig’ does not exist`tooavoid uruchomione w tym scenariuszu należy upewnić się, czy zapisać zmiany po zmianie nazwy jednostek hello w projekcie usługi BizTalk.  
  
### <a name="biztalk-service-project-builds-successfully-even-if-an-artifact-has-been-excluded-from-a-visual-studio-project"></a>Projekt usługi BizTalk kompilacje pomyślnie, nawet jeśli artefakty został on wykluczony z projektu programu Visual Studio
Rozważmy scenariusz, w której dodać tooa artefaktu (na przykład plik XSD) projektu usługi BizTalk, dołączenie tego artefaktu hello konfigurację mostka (na przykład, określając go jako typ komunikatu żądania), a następnie Wyklucz go z projektu programu Visual Studio hello. W takim przypadku kompilowania projektu hello nie będzie przekazywać wszelkie błędy tak długo, jak artefaktu hello usunięte jest dostępna na dysku hello na powitania tej samej lokalizacji, z której została uwzględniona w hello projektu Visual Studio.
  
### <a name="hello-biztalk-service-project-does-not-check-for-schema-availability-while-configuring-hello-bridges"></a>Hello projektu usługi BizTalk nie sprawdza dostępność schematu podczas konfigurowania mostków hello
W projekcie usługi BizTalk Jeśli schemat, który zostanie dodany projekt toohello importuje inny schemat hello projektu usługi BizTalk nie sprawdza, czy hello zaimportowanego schematu dodaniu toohello projektu. Jeśli spróbujesz toobuild takiego projektu nie są błędy kompilacji.
  
### <a name="hello-response-message-for-a-xml-request-reply-bridge-is-always-of-charset-utf-8"></a>komunikat odpowiedzi Hello mostka "żądanie-odpowiedź" XML jest zawsze zestawu znaków UTF-8
W tym wydaniu zestaw znaków hello komunikat odpowiedzi z XML mostka "żądanie-odpowiedź" hello ma zawsze wartość tooUTF-8.
  
### <a name="user-defined-datatypes"></a>Zdefiniowane przez użytkownika typów danych
Hello BizTalk Adapter Pack kart w funkcji usługi Adapter BizTalk hello mogą wykorzystywać zdefiniowanych przez użytkownika typów danych w operacjach karty.
Używając zdefiniowanych przez użytkownika typów danych, skopiuj hello plików (.dll) toodrive:\Program Files\Microsoft Service\BAServiceRuntime\bin\ karty BizTalk lub toohello globalnej pamięci podręcznej zestawów (GAC) na serwerze hello hello usługi BizTalk karty usługi hosta. W przeciwnym razie hello następujący błąd może wystąpić na powitania klienta:  
```
<s:Fault xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
<faultcode>s:Client</faultcode>
<faultstring xml:lang="en-US">hello UDT with FullName "File, FileUDT, Version=Value, Culture=Value, PublicKeyToken=Value" could not be loaded. Try placing hello assembly containing hello UDT definition in hello Global Assembly Cache.</faultstring>
<detail>
  <AFConnectRuntimeFault xmlns="http://Microsoft.ApplicationServer.Integration.AFConnect/2011" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <ExceptionCode>ERROR_IN_SENDING_MESSAGE</ExceptionCode>
  </AFConnectRuntimeFault>
</detail>
</s:Fault>
```  
  
> [!IMPORTANT]
> Jest zalecana toouse GACUtil.exe tooinstall pliku do hello globalnej pamięci podręcznej zestawów. Dokumenty GACUtil.exe jak toouse to narzędzie i hello opcje wiersza polecenia programu Visual Studio.  
> 
> 

### <a name="restarting-hello-biztalk-adapter-service-web-site"></a>Ponowne uruchamianie hello witryny sieci Web usługi karty BizTalk
Instalowanie hello **środowiska uruchomieniowego usługi karty BizTalk*** tworzy hello **Usługa karty BizTalk** witryny sieci web w usługach IIS, która zawiera hello **BAService** aplikacji. **BAService** aplikacji wewnętrznie używa przekazywania powiązania tooextend hello zasięgu chmury toohello punktu końcowego usługi lokalnej. Do usługi hostowanej w sieci lokalnej punkt końcowy hello odpowiedniego przekazywania zostanie zarejestrowany na powitania usługi Service Bus, tylko wtedy, gdy hello lokalnego uruchamiania usługi.  

Jeśli zatrzymać i uruchomić aplikację, nie jest honorowana hello konfiguracji do automatycznego uruchamiania aplikacji. W takim przypadku **BAService** jest zatrzymana, należy zawsze należy ponownie uruchomić hello **Usługa karty BizTalk** witryny sieci web zamiast tego. Się nie uruchomić lub zatrzymać hello **BAService** aplikacji.

### <a name="special-characters-should-not-be-used-for-address-and-entity-names-of-lob-components"></a>Nie należy używać znaków specjalnych nazw adres i jednostek biznesowych składników
Dla nazwy adresu i jednostek biznesowych składników nie należy używać znaków specjalnych. Jeśli tak zrobisz, wystąpi błąd podczas wdrażania hello projektu usługi BizTalk. Dla niektórych znaków, takich jak '%', hello BizTalk karty usługi witryny sieci Web może Przejdź w stanie zatrzymania i trzeba będzie toomanually ją uruchomić.

### <a name="test-map-with-get-context-property"></a>Mapa testu z Get właściwości kontekstu
Jeśli zawiera transformacji **Get właściwości kontekstu** operacji mapy **mapy testu** zakończy się niepowodzeniem. Tymczasowo zastąpić hello **Get właściwości kontekstu** mapy operację, podając ciąg połączenia mapy operację fikcyjny danymi. To wypełnić schemat docelowej hello i zezwala na test innych funkcji przekształcenia.

### <a name="test-map-property-does-not-display"></a>Właściwość mapy testu nie jest wyświetlana
Witaj **mapy testu** właściwości nie są wyświetlane w programie Visual Studio. Taka sytuacja może wystąpić, jeśli hello **właściwości** okno i hello **Eksploratora rozwiązań** okno nie jest zadokowany jednocześnie. tooresolve tego hello dokowania **właściwości** i hello **Eksploratora rozwiązań** systemu windows.  

### <a name="datetime-reformat-drop-down-is-grayed-out"></a>Ponowne formatowanie daty/godziny listy rozwijanej jest wyszarzony.
Po dodaniu operację mapy ponowne formatowanie daty/godziny toohello zaprojektować powierzchni i skonfigurowaniu hello Format mogą być wyszarzone listy rozwijanej. Może się to zdarzyć, jeśli komputer hello wyświetlana jest ustawiony **średni — 125%** lub **większe – 150%**. tooresolve, ustawić wyświetlania hello także**mniejsze — 100% (ustawienie domyślne)** przy użyciu hello poniższe kroki:  

1. Otwórz hello **Panelu sterowania** i kliknij przycisk **wygląd i personalizacja**.
2. Kliknij przycisk **wyświetlania**.
3. Kliknij przycisk **mniejsze — 100% (ustawienie domyślne)** i kliknij przycisk **Zastosuj**.

Witaj **Format** listy rozwijanej teraz powinny działać zgodnie z oczekiwaniami.

### <a name="duplicate-agreements-in-hello-biztalk-services-portal"></a>Zduplikowane umów w hello Portal usługi BizTalk
Należy wziąć pod uwagę hello następujących scenariuszy:

1. Tworzenie umowy z przy użyciu hello handlowi Zarządzanie partnerami OM z interfejsu API.
2. Otwórz umowę hello w hello Portal usługi BizTalk na dwóch różnych kartach.
3. Wdróż hello umowy z obu kartach hello.
4. W związku z tym umowami hello wdrożony co zduplikowane wpisy w hello Portal usługi BizTalk

**Obejście**. Otwórz dowolną hello zduplikowane umów w hello Portal usługi BizTalk i wdrożyć.  

### <a name="bridges-do-not-use-updated-certificate-even-after-a-certificate-has-been-updated-in-hello-artifact-store"></a>Nawet po zaktualizowaniu certyfikatu w magazynie artefaktu hello mostków nie używaj zaktualizowany certyfikat
Należy wziąć pod uwagę hello następujące scenariusze:  

**Scenariusz 1: Przy użyciu na podstawie odcisku palca certyfikatów do zabezpieczenia transferu wiadomości z punktu końcowego usługi tooa Mostek**  
Rozważmy scenariusz, w których są używane certyfikaty oparte na odcisk palca w projekcie usługi BizTalk. Należy zaktualizować hello certyfikatu w portalu usługi BizTalk hello z hello takie same nazwy, ale inny odcisk palca, ale nie zaktualizować hello projektu usługi BizTalk, w związku z tym. W takiej sytuacji Mostek hello może kontynuować wiadomości powitania tooprocess, ponieważ hello starszych danych certyfikatu może nadal być w pamięci podręcznej hello kanału. Po wykonaniu tej przetwarzanie komunikatu kończy się niepowodzeniem.  

**Obejście**: aktualizowanie certyfikatów hello w hello projektu usługi BizTalk i wdrożenie projektu hello.  

**Scenariusz 2: Za pomocą certyfikatów tooidentify na podstawie nazwy zachowania do zabezpieczenia transferu wiadomości z punktu końcowego usługi tooa Mostek**

Rozważmy scenariusz, w których są używane certyfikaty tooidentify na podstawie nazwy zachowania w projekcie usługi BizTalk. Aktualizuj certyfikat hello w portalu usługi BizTalk hello, ale nie aktualizuj odpowiednio hello projektu usługi BizTalk. W takiej sytuacji Mostek hello może kontynuować wiadomości powitania tooprocess, ponieważ hello starszych danych certyfikatu może nadal być w pamięci podręcznej hello kanału. Po wykonaniu tej przetwarzanie komunikatu kończy się niepowodzeniem.  

**Obejście**: aktualizowanie certyfikatów hello w hello projektu usługi BizTalk i wdrożenie projektu hello.  

### <a name="bridges-continue-tooprocess-messages-even-when-hello-sql-database-is-offline"></a>Mostków kontynuować tooprocess wiadomości, nawet wtedy, gdy baza danych SQL hello jest w trybie offline
mostków usługi BizTalk Services Hello kontynuować tooprocess wiadomości przez pewien czas, nawet jeśli hello Microsoft Azure bazy danych SQL (służący do przechowywania hello systemem informacje, takie jak wdrożonej artefakty i potoki) jest w trybie offline. Jest to spowodowane usługi BizTalk Services używa artefakty hello w pamięci podręcznej i Mostek konfiguracji.
Jeśli nie mają tooprocess mostków hello komunikaty podczas hello bazy danych SQL jest w trybie offline, można użyć toostop poleceń cmdlet programu PowerShell usługi BizTalk hello lub zawiesić hello usługi BizTalk. Zobacz [przykład zarządzania usługi BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=329019) dla operacji toomanage poleceń cmdlet programu Windows PowerShell hello.  

### <a name="reading-hello-xml-message-within-a-bridges-custom-code-component-includes-an-extra-bom-character"></a>Odczytywanie hello XML komunikat w składniku kod niestandardowy Mostek zawiera dodatkowy znak BOM
Rozważmy scenariusz, w którym ma tooread komunikatu XML w Mostek niestandardowego kodu. Jeśli używasz hello System.Text.Encoding.UTF8.GetString(bytes) interfejsu API platformy .NET nadmiarowe znaki BOM jest uwzględnionych w danych wyjściowych hello na początku hello wiadomości powitania. Tak więc, jeśli nie chcesz hello dane wyjściowe tooinclude hello nadmiarowe znaki BOM, należy użyć ```System.IO.StreamReader().ReadToEnd()```.

### <a name="sending-messages-tooa-bridge-using-wcf-does-not-scale"></a>Nie obsługuje wysyłanie komunikatów Mostek tooa przy użyciu programu WCF
Komunikaty wysłane Mostek tooa przy użyciu usługi WCF nie działa. Zamiast tego należy używać HttpWebRequest, jeśli klient skalowalnych.

### <a name="upgrade-token-provider-error-after-upgrading-from-biztalk-services-preview-toogeneral-availability-ga"></a>UAKTUALNIANIE: Błąd dostawcy tokenu po uaktualnieniu z wersji zapoznawczej usługi BizTalk tooGeneral dostępności (GA)
Brak EDI lub umowy AS2 z active partie. Po uaktualnieniu z wersji zapoznawczej tooGA hello usługi BizTalk, mogą wystąpić następujące hello:

* Błąd: hello dostawcy tokenu to tooprovide tokenu zabezpieczającego. Dostawca tokenu zwrócił komunikat: nie można rozpoznać nazwy zdalnej hello.
* Zadania wsadowe zostały anulowane.

**Obejście**: hello usługi BizTalk po zaktualizowane tooGeneral dostępności (GA), należy ponownie wdrożyć hello umowy.  

### <a name="upgrade-toolbox-shows-hello-old-bridge-icons-after-upgrading-hello-biztalk-services-sdk"></a>UAKTUALNIANIE: Przybornika pokazuje hello starego Mostek ikony po uaktualnieniu hello zestawu SDK usługi BizTalk Services
Po uaktualnieniu wcześniejszej wersji hello zestaw SDK usługi BizTalk, który miał starego ikony reprezentujące mostków hello, przybornika hello nadal tooshow hello starego ikony hello mostków. Jednak jeśli dodasz powierzchni Mostek tooBizTalk usługi projektu Projektanta powierzchni hello pokazuje hello nową ikonę.  

**Obejście**. Można obejść ten problem, usuwając pliki .tbd hello w obszarze <system drive>: \Users\<użytkownika > \AppData\Local\Microsoft\VisualStudio\11.0.  

### <a name="upgrade-biztalk-portal-update-from-preview-tooga-might-show-an-error-indicating-that-hello-edi-capability-is-not-available"></a>UAKTUALNIENIE: BizTalk portalu aktualizacji z wersji zapoznawczej tooGA wyświetli komunikat o błędzie informujący, że hello EDI możliwości nie jest dostępny
Jeśli użytkownik jest zalogowany do portalu usługi BizTalk hello podczas usługi BizTalk hello jest uaktualniana tooGA podglądu, może uzyskać hello następujący błąd w portalu hello:  

Ta funkcja nie jest dostępna w ramach tej wersji usług Microsoft Azure BizTalk. toouse te możliwości przełącznika tooan odpowiedniej wersji.  

**Rozdzielczość**: wylogowania z portalu hello, zamknij i otwórz hello przeglądarki, a następnie zaloguj się do portalu hello.  

### <a name="upgrade-new-tracking-data-does-not-show-up-after-biztalk-services-is-upgraded-tooga"></a>UAKTUALNIANIE: Nowe dane śledzenia nie jest wyświetlany po uaktualnionego tooGA usługi BizTalk Services
Przykładowa scenariusz, w którym masz Mostek XML wdrożone w wersji zapoznawczej usługi BizTalk subskrypcji. Wysyłać wiadomości Mostek toohello i odpowiadające im dane śledzenia hello jest dostępna w hello Portal usługi BizTalk. Teraz, jeśli bitów środowiska uruchomieniowego BizTalk usługi portalu i usługi BizTalk Services hello jest uaktualniony tooGA i wysłać toohello wiadomości, tego samego punktu końcowego mostka wdrożonej wcześniej, hello dane śledzenia nie jest wyświetlany dla wiadomości wysyłanych po uaktualnieniu.  

### <a name="pipelines-versus-bridges"></a>Potoki i mostków
W tym dokumencie termin hello "potoki" i "mostków" są używane zamiennie. Zasadniczo oznacza zarówno hello sam element, który jest wdrożony na usługi BizTalk Services jednostki przetwarzania komunikatu.  

### <a name="concepts"></a>Pojęcia
[Usługi BizTalk Services](https://msdn.microsoft.com/library/azure/hh689864.aspx)   

