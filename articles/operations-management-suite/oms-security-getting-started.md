---
title: "aaaGetting wprowadzenie Operations Management Suite zabezpieczeń i inspekcji rozwiązania | Dokumentacja firmy Microsoft"
description: "Ten dokument ułatwia tooget zostanie uruchomiony z Operations Management Suite zabezpieczeń i inspekcji toomonitor możliwości rozwiązania chmury hybrydowej."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 754796ef-a43e-468a-86c9-04a2eda55b5b
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: get-started-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 5cb3e5dbb3e60f9702a34c9413ddc1bf2b14b411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-operations-management-suite-security-and-audit-solution"></a>Wprowadzenie do korzystania z rozwiązania Zabezpieczenia i inspekcja w pakiecie Operations Management Suite
Ten dokument pomaga szybko rozpocząć korzystanie z rozwiązania Zabezpieczenia i inspekcja w pakiecie Operations Management Suite (OMS), objaśniając działanie poszczególnych opcji.

## <a name="what-is-oms"></a>Co to jest pakiet OMS?
Pakiet Microsoft Operations Management Suite (OMS) to oparte na chmurze rozwiązanie firmy Microsoft do zarządzania systemami IT, które ułatwia zarządzanie infrastrukturą lokalną i chmurową oraz jej ochronę. Aby uzyskać więcej informacji na temat pakietu OMS, przeczytaj artykuł hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="oms-security-and-audit-dashboard"></a>Pulpit nawigacyjny Zabezpieczenia i inspekcja w pakiecie OMS
Hello OMS zabezpieczeń i inspekcji rozwiązanie zapewnia kompleksowy wgląd w Twojej organizacji IT stan zabezpieczeń z wbudowaną zapytania dotyczące godne uwagi problemy wymagające uwagi. Witaj **zabezpieczeń i inspekcji** pulpit nawigacyjny jest hello ekranu głównego dla wszystkich powiązanych toosecurity w OMS. Zawiera ogólne wgląd w stan zabezpieczeń hello komputerów. Obejmuje on też hello możliwości tooview wszystkie zdarzenia z hello poza 24 godzin, 7 dni lub innych niestandardowych przedziale czasu. Witaj tooaccess **zabezpieczeń i inspekcji** pulpitu nawigacyjnego, wykonaj następujące kroki:

1. W hello **programu Microsoft Operations Management Suite** głównym pulpicie nawigacyjnym kliknij **ustawienia** kafelka w lewo hello.
2. W hello **ustawienia** bloku, w obszarze **rozwiązań** kliknij **zabezpieczeń i inspekcji** opcji.
3. Witaj **zabezpieczeń i inspekcji** zostanie wyświetlony pulpit nawigacyjny:
   
    ![Pulpit nawigacyjny Zabezpieczenia i inspekcja w pakiecie OMS](./media/oms-security-getting-started/oms-getting-started-fig1-ga.png)

Jeśli nie masz urządzenia monitorowane przez OMS uzyskujesz dostęp do tego pulpitu nawigacyjnego dla powitania po raz pierwszy, hello Kafelki nie zostaną wypełnione z danych uzyskanych od hello agenta. Po zainstalowaniu agenta hello, może upłynąć kilka toopopulate czas, w związku z tym początkowo Zobacz może brakować części danych, ponieważ są one nadal przekazywania toohello chmury.  W takim przypadku jest normalne toosee niektóre Kafelki bez wymierne informacji. Odczytu [połączyć komputery bezpośrednio tooOMS](https://technet.microsoft.com/library/mt484108.aspx) Aby uzyskać więcej informacji na temat agent pakietu OMS tooinstall w systemie Windows i [Linux połączyć komputery tooOMS](https://technet.microsoft.com/library/mt622052.aspx) Aby uzyskać więcej informacji na temat tooperform tego zadania w systemie Linux.

> [!NOTE]
> Hello agent zbiera informacje hello oparte na powitania bieżącego zdarzeń, które są włączone, na przykład nazwa komputera, adresu IP i użytkownika nazwy. Nie są jednak gromadzone żadne dokumenty bądź pliki, nazwy baz danych ani dane prywatne.   
> 
> 

Rozwiązania to zestawy reguł logiki, wizualizacji i gromadzenia danych opracowane w celu pokonywania kluczowych wyzwań klienta. Zabezpieczenia i inspekcja to jedno z takich rozwiązań — inne można dodać oddzielnie. Przeczytaj artykuł hello [dodać rozwiązania](https://technet.microsoft.com/library/mt674635.aspx) Aby uzyskać więcej informacji na temat tooadd nowego rozwiązania.

pulpit nawigacyjny OMS zabezpieczeń i inspekcji Hello jest podzielone na cztery główne kategorie:

* **Domen zabezpieczeń**: w tym obszarze będą mogli toofurther Eksploruj rekordy zabezpieczeń w czasie, dostęp do oceny złośliwego oprogramowania, aktualizacji oceny, zabezpieczenia sieci, informacje o tożsamości i dostępu, komputery ze zdarzeniami zabezpieczeń oraz szybko pulpit nawigacyjny Centrum zabezpieczeń tooAzure dostępu.
* **Godne uwagi problemy**: Ta opcja umożliwi tooquickly określenie hello liczby aktywnych problemów i hello ważności tych problemów.
* **Wykryć (wersja zapoznawcza)**: włącza wzorców ataków tooidentify przez wizualizacja alerty zabezpieczeń, zgodnie z ich odbywać się z zasobami.
* **Analizy zagrożeń**: włącza wzorców ataków tooidentify przez wizualizacja hello całkowita liczba serwery z wychodzącym ruchem złośliwego oprogramowania IP, typ złośliwe oprogramowanie hello i mapy, pokazujący, gdzie pochodzą z tych adresów IP. 
* **Typowe zapytania zabezpieczeń**: Ta opcja zapewnia możesz listę najczęściej zabezpieczeń hello wysyła zapytanie do używania toomonitor środowiska. Po kliknięciu w jednym z tych zapytań zostanie otwarty hello **wyszukiwania** blok hello wyników dla tego zapytania.

> [!NOTE]
> Aby uzyskać więcej informacji o sposobach zapewniania bezpieczeństwa danych przez pakiet OMS, przeczytaj artykuł How OMS secures your data (W jaki sposób pakiet OMS chroni dane?).
> 
> 

## <a name="security-domains"></a>Domeny zabezpieczeń
Monitorowanie zasobów, jest ważne toobe tooquickly stanie dostępu hello bieżący stan środowiska. Jednak również jest ważne toobe tootrack stanie wstecz zdarzenia, które wystąpiły w ostatnich hello, który może prowadzić do lepszego zrozumienia tooa co dzieje się w danym środowisku, w niektórych punktu w czasie. 

> [!NOTE]
> przechowywanie danych jest według planu cenowego toohello OMS. Aby uzyskać więcej informacji można znaleźć hello [programu Microsoft Operations Management Suite](https://www.microsoft.com/server-cloud/operations-management-suite/pricing.aspx) cennik.
> 
> 

Zdarzenia scenariusze postępowania odpowiedzi i dowodowe bezpośrednio będą korzystać z dostępnych w hello wyników hello **rekordy zabezpieczeń w czasie** kafelka.

![Rekordy zabezpieczeń w czasie](./media/oms-security-getting-started/oms-getting-started-fig2.JPG)

Po kliknięciu tego kafelka hello **wyszukiwania** zostanie otwarty blok przedstawiający wyniku zapytania dla **zdarzenia zabezpieczeń** (typ = SecurityEvents) z danymi na podstawie hello ostatnich siedmiu dni, jak pokazano poniżej:

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Rekordy zabezpieczeń w czasie](./media/oms-security-getting-started/oms-getting-started-fig3.JPG)

wynik wyszukiwania Hello jest podzielony na dwa okienka: hello w okienku po lewej stronie umożliwia podział hello liczba zdarzeń zabezpieczeń, które zostały odnalezione komputery hello, w których znaleziono się tych zdarzeń, liczbę hello kont, które zostały odnalezione w tych komputerów i typy hello działania. Witaj w prawym okienku zapewnia hello całkowita liczba wyników i chronologicznej widoku zdarzeń zabezpieczeń hello aktywnością komputera hello nazwy i zdarzeń. Możesz również kliknąć **Pokaż więcej** tooview bardziej szczegółowe informacje dotyczące tego zdarzenia, takie jak dane zdarzeń hello, hello identyfikator zdarzenia i źródło zdarzenia hello.

> [!NOTE]
> Więcej informacji na temat zapytania wyszukiwania pakietu OMS zawiera artykuł [OMS search reference](https://technet.microsoft.com/library/mt450427.aspx) (Wprowadzenie do wyszukiwania w pakiecie OMS).
> 
> 

### <a name="antimalware-assessment"></a>Ocena oprogramowania chroniącego przed złośliwym kodem
Ta opcja umożliwia tooquickly można zidentyfikować komputery z niewystarczającą ochroną i komputerów, które są szkodzi wystąpieniem złośliwego oprogramowania. Oceny złośliwego oprogramowania, stanu i wykrytych zagrożeń na serwerach hello monitorowane są odczytywane, a następnie hello danych są wysyłane toohello usługę w chmurze hello do przetwarzania. Serwery z wykrytymi zagrożeniami i serwery z niewystarczającą ochroną są wyświetlane na powitania złośliwego oprogramowania oceny nawigacyjnym, która jest dostępna po kliknięciu hello **oceny ochrony przed złośliwym kodem** kafelka. 

![Ocena oprogramowania chroniącego przed złośliwym kodem](./media/oms-security-getting-started/oms-getting-started-fig4-ga.png)

Podobnie jak wszystkie inne dostępne na pulpicie nawigacyjnym OMS, na żywo kafelka po kliknięciu go hello **wyszukiwania** zostanie otwarty blok zawierający hello wyniku zapytania. Dla tej opcji, po kliknięciu hello **Niezgłaszających** opcję w obszarze **stanu ochrony**, będzie miał hello wynik kwerendy, który zawiera ten pojedynczy wpis zawierający nazwę komputera hello i jego ranking jako pokazano poniżej:

![Wynik wyszukiwania](./media/oms-security-getting-started/oms-getting-started-fig5.png)

> [!NOTE]
> *Ranga* jest klasa, podając stan hello tooreflect ochrona powitalnych (, off, zaktualizować, itp.) i zagrożenia, które zostały znalezione. Jako numer agregacji toomake pomaga, o które.
> 
> 

Kliknięcie w polu Nazwa komputera hello, konieczne będzie hello chronologicznej widok hello stanu ochrony dla tego komputera. Jest to przydatne w scenariuszach, w których należy toounderstand Jeśli wcześniej zainstalowano hello ochrony przed złośliwym oprogramowaniem i w pewnym momencie został usunięty.   

### <a name="update-assessment"></a>Ocena aktualizacji
Ta umożliwia opcja tooquickly możesz określić hello problemów z bezpieczeństwem toopotential ogólną zagrożeń i czy lub jak bardzo krytyczne te aktualizacje są w danym środowisku. OMS zabezpieczeń i inspekcji rozwiązania zapewniają tylko hello wizualizacji tych aktualizacji, hello rzeczywiste dane pochodzą z [rozwiązań do zarządzania aktualizacji](oms-solution-update-management.md), który jest inny moduł w OMS. Przykład Witaj aktualizacji w tym miejscu:

![Aktualizacje systemu](./media/oms-security-getting-started/oms-getting-started-fig6-new.png)

> [!NOTE]
> Aby uzyskać więcej informacji na temat rozwiązania Zarządzanie aktualizacjami, przeczytaj temat [Rozwiązanie do zarządzania aktualizacjami w usłudze OMS](oms-solution-update-management.md).
> 
> 

### <a name="identity-and-access"></a>Tożsamość i dostęp
Tożsamość powinna być kontroli hello płaszczyzny w przedsiębiorstwie, ochrona tożsamości powinna być sieci o najwyższym priorytecie. W przeszłości hello zostały strefy wokół organizacji i tych granicach zostały jednego podstawowego granice obrony hello, obecnie większej ilości danych i więcej aplikacji, przenoszenie chmury toohello tożsamości hello staje się hello obwodowej nowe. 

> [!NOTE]
> obecnie dane hello jest oparty tylko na dane logowania zdarzeń zabezpieczeń (zdarzenie ID 4624) w przyszłości logowania usługi Office 365 hello i danych usługi Azure AD będą również uwzględnione.
> 
> 

Monitorowanie działań tożsamości będzie aktywne działania w stanie tootake przed zdarzenie ma miejsce lub akcje reaktywne toostop próba ataku. Witaj **tożsamościami i dostępem** pulpit nawigacyjny zawiera omówienie stanu Twojej tożsamości, w tym hello liczby nieudanych prób toolog na konto użytkownika hello, które były używane podczas prób nawiązania, te konta, które zostały zablokowane, konta ze zmienionymi lub zresetować hasło, a obecnie liczby kont, które są rejestrowane w. 

Po kliknięciu hello **tożsamościami i dostępem** kafelka zobaczysz powitania po pulpitu nawigacyjnego:

![Tożsamość i dostęp](./media/oms-security-getting-started/oms-getting-started-fig7-ga.png)

Witaj informacje są dostępne na tym pulpicie nawigacyjnym natychmiast może pomóc tooidentify potencjalnych podejrzanych działań. Na przykład istnieją 338 toolog prób na jako **administratora** i 100% tych prób nie powiodła się. Może to być spowodowane atakiem siłowym na to konto. Po kliknięciu tego konta spowoduje uzyskać więcej informacji, które mogą pomóc zasobu docelowego hello toodetermine takiego ataku potencjalnych:

![Wyniki wyszukiwania](./media/oms-security-getting-started/oms-getting-started-fig8.JPG)

Witaj szczegółowy raport zawiera ważne informacje dotyczące tego zdarzenia, w tym: hello komputera docelowego, typ hello logowania (w tym przypadku logowania sieci), hello działania (w tym przypadku zdarzeniu 4625) i wszechstronne osi czasu każdej próby. 

### <a name="computers"></a>Komputery
Ten Kafelek mogą być używane tooaccess wszystkie komputery, których aktywnie zdarzeń zabezpieczeń. Kliknięcie tego kafelka zostanie wyświetlona lista hello komputerów za pomocą zdarzeń zabezpieczeń i hello liczba zdarzeń znajdujących się na każdym komputerze:

![Komputery](./media/oms-security-getting-started/oms-getting-started-fig9.JPG)

Można kontynuować badania klikając na każdym komputerze i przejrzyj hello zdarzenia zabezpieczeń, które zostały oznaczone.

### <a name="threat-intelligence"></a>Analiza zagrożeń

Przy użyciu opcji analizy zagrożeń hello dostępne w OMS zabezpieczeń i inspekcji, Administratorzy IT może zidentyfikować zagrożenia bezpieczeństwa hello środowisku, na przykład, ustalić, czy na określonym komputerze jest częścią botnet. Komputery mogą stać się węzły w sieć botnet wykorzystywana osobom atakującym instalowania nielegalnemu złośliwego oprogramowania, które potajemnie łączy z tego polecenia toohello komputera i kontroli. Może także identyfikować potencjalne zagrożenia pochodzące z tajnych kanałów komunikacji, takich jak darknet. Dowiedz się więcej o analizy zagrożeń, odczytując [toosecurity monitorowania i odpowiada alerty w programie Operations Management Suite zabezpieczeń i rozwiązanie inspekcji](oms-security-responding-alerts.md) artykułu.

W niektórych scenariuszach możesz zauważyć potencjalnie złośliwy adres IP, do którego uzyskano dostęp z jednego z monitorowanych komputerów:

![Mapa analizy zagrożeń](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

Ten alert i innych użytkowników w tej samej kategorii Witaj, są generowane przez OMS zabezpieczeń dzięki wykorzystaniu [analizy zagrożeń Microsoft](https://youtu.be/O4WtxgUrDc8). Hello danych analizy zagrożeń jest zbieranych przez firmę Microsoft a także zakupione z wiodącymi dostawcami analizy zagrożeń. Te dane jest często aktualizowana i dostosowywane przenoszenie toofast zagrożeń. Powodu charakter tooits powinny być połączone z innych źródeł informacji o zabezpieczeniach podczas [badanie](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) alert zabezpieczeń. 

### <a name="baseline-assessment"></a>Ocena linii bazowej

Firma Microsoft, wraz z instytucjami branżowymi i rządowymi na całym świecie, zdefiniowała konfigurację systemu Windows, która reprezentuje wdrożenia serwera o wysokim poziomie zabezpieczeń. Konfiguracja ta stanowi zestaw kluczy rejestru, ustawień zasad inspekcji i ustawień zasad zabezpieczeń wraz z zalecanymi przez firmę Microsoft wartościami tych ustawień. Ten zestaw reguł jest określany jako linia bazowa zabezpieczeń. Przeczytaj temat [Ocena linii bazowej w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite](oms-security-baseline.md), aby uzyskać więcej informacji na temat tej opcji.

### <a name="azure-security-center"></a>Azure Security Center
Ten Kafelek jest zasadniczo pulpit nawigacyjny Centrum zabezpieczeń Azure tooaccess skrótów. Więcej informacji na temat tego rozwiązania zawiera artykuł [Przewodnik Szybki start dotyczący Centrum zabezpieczeń Azure](../security-center/security-center-get-started.md).

## <a name="notable-issues"></a>Problemy godne uwagi
głównym celem tej grupy Opcje Hello jest tooprovide szybki przegląd hello występujące problemy w danym środowisku Kategoryzacja krytyczny, ostrzeżenie i do celów informacyjnych. Witaj aktywne problemy typu kafelka jest wizualizacji tych problemów, ale go nie zezwala tooexplore więcej szczegółowych informacji o nich, które mają być toouse hello dolnej części tego kafelka, nazwie hello hello wydania (nazwa), ile obiekty mają tak się stało (licznik) i jak bardzo krytyczne jest (waga).

![Problemy godne uwagi](./media/oms-security-getting-started/oms-getting-started-fig10.JPG)

Widać, że te problemy zostały opisane w różnych obszarach hello **domen zabezpieczeń** grupy, która umacnia hello celem tego widoku: wizualizacji hello najważniejszych zagadnień w środowisku z jednego miejsca.

## <a name="detections-preview"></a>Wykrycia (podgląd)
Witaj głównym celem tej opcji jest tooallow IT tooquickly zidentyfikować potencjalne zagrożenia środowiska tootheir przez i hello ważność tego zagrożenia.

![Analiza zagrożeń](./media/oms-security-getting-started/oms-getting-started-fig12.png)

Ta opcja umożliwia również podczas [dochodzenia odpowiedzi na zdarzenia](https://blogs.msdn.microsoft.com/azuresecurity/2016/11/30/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) tooperform hello oceny i Uzyskaj więcej informacji na temat atak powitania.

> [!NOTE]
> Aby uzyskać więcej informacji na temat toouse OMS do reagowania na zdarzenia, obejrzyj ten film: [jak tooLeverage hello Centrum zabezpieczeń Azure i programu Microsoft Operations Management Suite dla reagowania na zdarzenia](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703).
> 
> 

## <a name="threat-intelligence"></a>Analiza zagrożeń
Witaj nowych zagrożeń sekcja analizy rozwiązania zabezpieczeń i inspekcji hello wizualizuje wzorce możliwy atak powitania na kilka sposobów: hello łącznej liczby serwerów z wychodzącym ruchem złośliwego oprogramowania IP, hello typu złośliwe oprogramowanie i mapy, który wskazuje, gdzie tych adresów IP pochodzą z. Mogą współpracować z mapy hello i kliknij na powitania adresów IP, aby uzyskać więcej informacji.

Żółty pinezki — na mapie hello wskazują ruch przychodzący z złośliwymi adresami IP. Nie jest rzadko dla serwerów, które są udostępniane toohello internet toosee złośliwy ruch przychodzący, ale firma Microsoft zaleca przejrzenie tych prób toomake się, że żaden z nich zakończyło się pomyślnie. Wskaźniki te są oparte na dziennikach usług IIS i zapory systemu Windows oraz danych WireData.  

![Analiza zagrożeń](./media/oms-security-getting-started/oms-getting-started-fig11-ga.png)

## <a name="common-security-queries"></a>Typowe zapytania dotyczące zabezpieczeń
Hello listę typowych kwerend zabezpieczeń może okazać się przydatne podczas możesz toorapidly dostępu do informacji o zasobie i dostosować go na podstawie potrzeb w danym środowisku. Typowe zapytania obejmują:

* Wszystkie działania dotyczące zabezpieczeń
* Działania dotyczące zabezpieczeń na powitania komputera "computer01.contoso.com" (Zastąp własną nazwą komputera)
* Działania dotyczące zabezpieczeń na powitania komputera "computer01.contoso.com" dla konta "Administrator" (Zastąp własnymi nazwami komputera i konta)
* Działania logowania według komputera
* Konta, przy użyciu których przerwano pracę oprogramowania firmy Microsoft chroniącego przed złośliwym kodem na dowolnym komputerze
* Komputery, na których został przerwany hello proces ochrony przed złośliwym oprogramowaniem firmy Microsoft
* Komputery, na których wykonano plik „hash.exe” (zastąp inną nazwą procesu)
* Nazwy wszystkich wykonanych procesów
* Działania logowania według konta
* Konta, z których zdalne logowanie na powitania komputera "computer01.contoso.com" (Zastąp własną nazwą komputera)

## <a name="see-also"></a>Zobacz też
W tym dokumencie możesz zostały wprowadzone tooOMS rozwiązania zabezpieczeń i inspekcji. toolearn więcej informacji na temat zabezpieczeń OMS, zobacz następujące artykuły hello:

* [Omówienie pakietu Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Monitorowanie i alerty tooSecurity odpowiada Operations Management Suite zabezpieczeń i rozwiązanie inspekcji](oms-security-responding-alerts.md)
* [Monitorowanie zasobów w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite](oms-security-monitoring-resources.md)

