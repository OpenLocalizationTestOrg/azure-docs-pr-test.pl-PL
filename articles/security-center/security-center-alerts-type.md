---
title: "aaaSecurity alerty według typu w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono hello różnych rodzajów alerty zabezpieczeń dostępnych w Centrum zabezpieczeń Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b3e7b4bc-5ee0-4280-ad78-f49998675af1
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: ee69cb9035c35f5bc2ed51f9b9d6f29486b4caf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-security-alerts-in-azure-security-center"></a>Informacje o alertach zabezpieczeń w usłudze Azure Security Center
W tym artykule opisano toounderstand hello różnych typów alertów zabezpieczeń i powiązane szczegółowe informacje, które są dostępne w Centrum zabezpieczeń Azure. Aby uzyskać więcej informacji na temat sposobu toomanage alertów i zdarzeń, zobacz [toosecurity zarządzanie i odpowiada alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> tooset się zaawansowane wykryć uaktualnienia tooAzure Security Center Standard. Dostępna jest bezpłatna 60-dniowa wersja próbna. tooupgrade, wybierz opcję **warstwy cenowej** w hello [zasady zabezpieczeń](security-center-policies.md). toolearn więcej, zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/security-center/).
>

## <a name="what-type-of-alerts-are-available"></a>Jakie typy alertów są dostępne?
Centrum zabezpieczeń Azure używa różnorodnych narzędzi [możliwości wykrywania](security-center-detection-capabilities.md) ataków toopotential klientów tooalert przeznaczonych dla swoich środowiskach. Te alerty zawiera cennych informacji na temat hello co wyzwalane hello alertu, hello zasobów docelowych i hello źródła atak powitania. Hello informacje zawarte w alertu w zależności od typu hello analytics używane toodetect hello zagrożenia. Zdarzenia mogą również zawierać dodatkowe informacje kontekstowe przydatne podczas badania zagrożenia.  Ten artykuł zawiera informacje o hello następujące typy alertów:

* Analiza zachowania maszyny wirtualnej (VMBA)
* Analiza sieci
* Analiza zasobów
* Informacje kontekstowe

## <a name="virtual-machine-behavioral-analysis"></a>Analiza zachowania maszyny wirtualnej
Centrum zabezpieczeń Azure można użyć analizy behawioralnej tooidentify naruszony zasoby oparte na analizie dzienników zdarzeń maszyny wirtualnej. na przykład zdarzeń tworzenia procesów i zdarzeń logowania. Ponadto jest korelacji z innych toocheck sygnałów do obsługi dowód powszechnie kampanii.

> [!NOTE]
> Aby uzyskać więcej informacji na temat sposobu działania funkcji wykrywania usługi Security Center, zobacz [Funkcje wykrywania usługi Azure Security Center](security-center-detection-capabilities.md).
>

### <a name="crash-analysis"></a>Analiza awarii
Analiza pamięci zrzutu awaryjnego jest toodetect metodę zaawansowane złośliwego oprogramowania, które jest w stanie tooevade tradycyjne zabezpieczenia rozwiązania. Różne rodzaje złośliwego oprogramowania spróbuj tooreduce hello prawdopodobieństwo wykrycia przez programy antywirusowe nigdy nie pisząc toodisk lub zapisywane toodisk składniki oprogramowania są szyfrowane. Dzięki temu toodetect trudne hello złośliwego oprogramowania za pomocą metod tradycyjnych ochrony przed złośliwym oprogramowaniem. Jednak tego rodzaju złośliwe oprogramowanie może zostać wykryte przy użyciu analizy pamięci, ponieważ złośliwe oprogramowanie musi pozostać dane śledzenia w pamięci w kolejności toofunction.

W przypadku awarii oprogramowania zrzutu awaryjnego przechwytuje część pamięci w czasie hello hello awarii (Crash). Hello awarii może być spowodowane przez złośliwe oprogramowanie, ogólnym lub problemów z systemu. Analizując hello pamięci hello zrzutu awaryjnego, Centrum zabezpieczeń może wykryć techniki stosowane tooexploit luk w zabezpieczeniach oprogramowania, dostęp do poufnych danych i ukryty sposób utrwalić na maszynie z naruszonymi zabezpieczeniami. Jest to realizowane z toohosts wpływ wydajności minimalnej jako analizy hello jest wykonywane przez hello kończyć ponownie Centrum zabezpieczeń.

Witaj kolejnych pól przedstawiono typowe toohello awarii zrzutu alertu pojawiające się w dalszej części tego artykułu:

* Plik zrzutu: Nazwa pliku zrzutu awaryjnego hello.
* PROCESSNAME: Nazwa hello awarii procesu.
* PROCESSVERSION: Wersja hello awarii procesu.

### <a name="shellcode-discovered"></a>Wykryto kod powłoki
Shellcode jest ładunku hello, które zostaje uruchomione po złośliwego oprogramowania luki w zabezpieczeniach oprogramowania. Ten alert oznacza, że analiza zrzutu awaryjnego wykryła zachowanie kodu wykonywalnego typowe dla złośliwych ładunków. Wprawdzie niezłośliwe oprogramowanie może zachowywać się podobnie, jednak nie jest to typowe w przypadku zwykłych metod tworzenia oprogramowania.

Przykład alertu Shellcode Witaj zapewnia hello następujące pola dodatkowe:

* ADRES: hello lokalizacja w pamięci hello shellcode.

Oto przykład tego typu alertu:

![Alert kodu powłoki](./media/security-center-alerts-type/security-center-alerts-type-fig2.png)

### <a name="module-hijacking-discovered"></a>Wykryto przejęcie modułu
System Windows używa bibliotek dołączanych dynamicznie (dll) tooallow oprogramowania tooutilize typowe funkcje systemu Windows systemu. Przejmującą DLL występuje, gdy złośliwe oprogramowanie hello DLL obciążenia kolejności tooload złośliwe ładunków do pamięci, gdzie mogą być wykonywane dowolnego kodu. Ten alert wskazuje, że analiza zrzutu awaryjnego hello wykryto o podobnej nazwie moduł, który jest ładowany z dwóch różnych ścieżek. Jedna ze ścieżek hello załadować pochodzi z wspólną lokalizację binarnego systemu Windows.

Deweloperzy oprogramowania legalnego czasem zmienić kolejność ładowania biblioteki DLL hello-złośliwego ze względu na przykład Instrumentacja, rozszerzanie systemu operacyjnego Windows hello lub rozszerzanie aplikacji systemu Windows. toohelp odróżnienie toohello złośliwego i potencjalnie niegroźne zmienia kolejność ładowania biblioteki DLL, Centrum zabezpieczeń Azure sprawdza, czy załadować moduł zgodne tooa podejrzane profilu. Hello wyniku sprawdzania jest wskazywana przez pole "Podpisu" hello hello alertu i jest widoczny w hello ważność alertu hello, opis alertu i kroki korygujące alertu. tooresearch, czy moduł hello jest uzasadnione lub złośliwe, analizować hello na dysku kopię hello przejmującą modułu. Na przykład można zweryfikować podpisu cyfrowego hello pliku lub uruchomić skanowanie za pomocą oprogramowania antywirusowego.

Ponadto typowe pola toohello opisane w sekcji wcześniejszych "Shellcode odnalezione" hello, ten alert zapewnia hello następujące pola:

* Podpis: Wskazuje, czy hello przejmującą modułu zgodne tooa podejrzane zachowanie profilu.
* HIJACKEDMODULE: Nazwa hello hello przejęty modułu systemu Windows.
* HIJACKEDMODULEPATH: ścieżka hello hello przejęty modułu systemu Windows.
* HIJACKINGMODULEPATH: ścieżka hello hello przechwyceniu modułu.

Oto przykład tego typu alertu:

![Alert o przejęciu modułu](./media/security-center-alerts-type/security-center-alerts-type-fig3.png)

### <a name="masquerading-windows-module-detected"></a>Wykryto zamaskowany moduł systemu Windows
Złośliwe oprogramowanie może używać nazw pospolitych plików binarnych systemu Windows (na przykład SVCHOST. Wywołanie pliku EXE) lub modułów (na przykład NTDLL. Biblioteki DLL) zbyt*blend* i przesłaniać hello rodzaj hello złośliwego oprogramowania z administratorów systemu. Ten alert wskazuje, że analiza zrzutu awaryjnego hello wykrywa, że ten plik zrzutu awaryjnego hello zawiera moduły, użyj nazwy modułu systemu Windows, które nie spełniają innych kryteriów, które są typowe dla modułów systemu Windows. Analizowanie hello na dysku kopię hello zamaskowana moduł może zawierać dodatkowe informacje dotyczące hello rodzaj uzasadnionych lub złośliwymi tego modułu. Analiza może obejmować:

* Potwierdź, że w pliku hello jest dostarczana jako część pakietu oprogramowania uzasadnione.
* Sprawdź plik hello podpisu cyfrowego.
* Uruchom skanowanie za pomocą oprogramowania antywirusowego na powitania pliku.

Ponadto typowe pola toohello opisany w sekcji "Shellcode odnalezione" hello, ten alert zapewnia hello następujące dodatkowe pola:

* Szczegóły: Opis, czy metadane modułu hello jest prawidłowy i czy hello moduł został załadowany w ścieżce systemowej.
* NAME: hello nazwa zamaskowana modułu Windows hello.
* ŚCIEŻKA: hello ścieżki toohello zamaskowana modułu Windows.

Ten alert również wyodrębnia i zawiera określone pola z modułu hello nagłówek PE, takie jak "Sumy kontrolnej" i "TIMESTAMP". Te pola są wyświetlane tylko pola hello znajdują się w hello module. Zobacz hello [PE firmy Microsoft i specyfikacja COFF](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) szczegółowe informacje na temat tych pól.

Oto przykład tego typu alertu:

![Alert o zamaskowanym elemencie systemu Windows](./media/security-center-alerts-type/security-center-alerts-type-fig4.png)

### <a name="modified-system-binary-discovered"></a>Wykryto zmodyfikowany plik binarny systemu
Złośliwe oprogramowanie może zmodyfikować plików binarnych systemu core w kolejności toocovertly dostęp do danych lub ukryty sposób utrwalić w systemie, którego bezpieczeństwo zostało naruszone. Ten alert wskazuje, czy analiza zrzutu awaryjnego hello wykrył, że pliki binarne systemu operacyjnego Windows core zostały zmodyfikowane w pamięci lub na dysku.

Wiarygodni programiści czasami modyfikują moduły systemu w pamięci z niezłośliwych powodów, na przykład w celu obejścia lub uzyskania zgodności aplikacji. toohelp zróżnicować złośliwego i potencjalnie legalnych modułach, Centrum zabezpieczeń Azure sprawdza, czy moduł zmodyfikowane hello jest zgodny tooa podejrzane profilu. Wskazuje Hello wyniku sprawdzania hello ważność alertu hello, opis alertu i kroki korygujące alertu.

Ponadto typowe pola toohello opisany w sekcji "Shellcode odnalezione" hello, ten alert zapewnia hello następujące dodatkowe pola:

* Nazwa modułu: Nazwa hello zmodyfikować systemowym pliku binarnym.
* Wersja modułu: Wersja hello zmodyfikowana systemowym pliku binarnym.

Oto przykład tego typu alertu:

![Alert o zmodyfikowanym pliku binarnym systemu](./media/security-center-alerts-type/security-center-alerts-type-fig5.png)

### <a name="suspicious-process-executed"></a>Wykonanie podejrzanego procesu
Centrum zabezpieczeń zostanie zidentyfikowana podejrzane procesu, który jest uruchamiany na powitania docelowej maszyny wirtualnej, a następnie wyzwala alert. wykrywanie Hello wygląda dla określonej nazwy hello, ale poszukaj parametru hello pliku wykonywalnego. W związku z tym nawet jeśli osoba atakująca hello zmienia nazwę pliku wykonywalnego hello, Centrum zabezpieczeń może wykryć podejrzane procesu hello.

Oto przykład tego typu alertu:

![Alert o wykonaniu podejrzanego procesu](./media/security-center-alerts-type/security-center-alerts-type-fig6-new.png)

### <a name="multiple-domain-accounts-queried"></a>Wiele zapytań do kont domeny
Centrum zabezpieczeń może wykryć wielu prób tooquery kont domeny usługi Active Directory, która coś jest zazwyczaj wykonywane przez osoby atakujące podczas Rekonesans sieci. Osoby atakujące mogą wykorzystać to technika tooquery hello domeny tooidentify hello użytkownicy, zidentyfikować konta administratora domeny hello, identyfikację hello komputerów, które są kontrolerami domeny, a także zidentyfikować hello potencjalnych domeny zaufania relacji z innymi domenami.

Oto przykład tego typu alertu:

![Alert o wielokrotnych zapytaniach do konta domeny](./media/security-center-alerts-type/security-center-alerts-type-fig7-new.png)

### <a name="local-administrators-group-members-were-enumerated"></a>Wyliczono członków grupy administratorów lokalnych

Centrum zabezpieczeń będzie tootrigger alert, gdy jest wyzwolić zdarzeń zabezpieczeń hello 4798, w systemie Windows Server 2016 i Windows 10. Dzieje się tak, kiedy zostają wyliczone grupy administratorów lokalnych, co jest zazwyczaj wykonywane przez osoby atakujące podczas czynności rozpoznawczych sieci. Osoby atakujące mogą korzystać z tej techniki tooquery hello tożsamości użytkowników z uprawnieniami administracyjnymi.

Oto przykład tego typu alertu:

![Administrator lokalny](./media/security-center-alerts-type/security-center-alerts-type-fig14-new.png)

### <a name="anomalous-mix-of-upper-and-lower-case-characters"></a>Nietypowa kombinacja wielkich i małych liter

Centrum zabezpieczeń wyzwolenia alertu po wykryciu hello użycie kombinacji wielkich i małych liter w wierszu polecenia hello. Niektóre osoby atakujące mogą wykorzystać toohide to technika, z uwzględnieniem wielkości liter lub skrótu na podstawie reguł maszyny.

Oto przykład tego typu alertu:

![Nietypowa kombinacja](./media/security-center-alerts-type/security-center-alerts-type-fig15-new.png)

### <a name="suspected-kerberos-golden-ticket-attack"></a>Podejrzenie ataku na złoty bilet protokołu Kerberos

Złamany [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) klucz może być używany przez osobę atakującą toocreate protokołu Kerberos "Złotego biletów", umożliwiając tooimpersonate atakująca hello każdy użytkownik ma. Centrum zabezpieczeń będzie tootrigger alert po wykryciu tego typu działania.

> [!NOTE] 
> Aby uzyskać więcej informacji o złotym bilecie protokołu Kerberos, przeczytaj przewodnik [Windows 10 credential theft mitigation guide](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx) (Przewodnik ograniczania przypadków kradzieży poświadczeń w systemie Windows 10).

Oto przykład tego typu alertu:

![Złoty bilet](./media/security-center-alerts-type/security-center-alerts-type-fig16-new.png)

### <a name="suspicious-account-created"></a>Utworzono podejrzane konto

Usługa Security Center wyzwoli alert, kiedy zostanie utworzone konto bardzo podobne do istniejącego wbudowanego konta z uprawnieniami administracyjnymi. Ta technika może służyć przez osoby atakujące toocreate nieautoryzowanego konta tooavoid jest wystąpieniem przez człowieka weryfikacji.
 
Oto przykład tego typu alertu:

![Podejrzane konto](./media/security-center-alerts-type/security-center-alerts-type-fig17-new.png)

### <a name="suspicious-firewall-rule-created"></a>Utworzono podejrzaną regułę zapory

Osoby atakujące mogą spróbuj zabezpieczeń hosta toocircumvent przez tworzenie toocommunicate złośliwe aplikacje tooallow reguły zapory niestandardowych za pomocą polecenia i kontroli lub toolaunch ataków za pośrednictwem sieci hello za pośrednictwem hello naruszenia zabezpieczeń hosta. Usługa Security Center wyzwoli alert, kiedy wykryje, że utworzono nową regułę zapory przy użyciu pliku wykonywalnego w podejrzanej lokalizacji.
 
Oto przykład tego typu alertu:

![Reguła zapory](./media/security-center-alerts-type/security-center-alerts-type-fig18-new.png)

### <a name="suspicious-combination-of-hta-and-powershell"></a>Podejrzana kombinacja hosta HTA i programu PowerShell

Usługa Security Center wyzwoli alert, kiedy wykryje, że narzędzie Microsoft HTML Application Host (HTA) uruchamia polecenia programu PowerShell. Jest to metoda używane przez osoby atakujące toolaunch złośliwych skryptów środowiska PowerShell.
 
Oto przykład tego typu alertu:

![HTA i PS](./media/security-center-alerts-type/security-center-alerts-type-fig19-new.png)


## <a name="network-analysis"></a>Analiza sieci
Wykrywanie zagrożeń sieci za pomocą usługi Security Center polega na automatycznym zbieraniu informacji o zabezpieczeniach uzyskanych na podstawie ruchu protokołu IPFIX (Internet Protocol Flow Information Export) na platformie Azure. Te informacje, często korelowanie informacji z wielu źródeł, zagrożenia tooidentify analizę.

### <a name="suspicious-outgoing-traffic-detected"></a>Wykryto podejrzany ruch wychodzący
Urządzenia sieciowe podlega odnajdywaniu i profilowane w znacznie hello tak samo jak inne rodzaje systemów. Osoby atakujące zazwyczaj zaczynają od skanowania portów. W następnym przykładzie hello masz podejrzane ruchu protokołu Secure Shell (SSH) z maszyny Wirtualnej. W tym scenariuszu możliwy jest siłowy atak SSH lub atak polegający na sprawdzaniu, czy dany port jest otwarty w zasobie zewnętrznym.

![Alert o podejrzanym ruchu wychodzącym](./media/security-center-alerts-type/security-center-alerts-type-fig8.png)

Ten alert zapewnia informacje, których można używać tooidentify hello zasobu, który był używany tooinitiate takiego ataku. Ten alert zawiera również informacje tooidentify hello naruszenia zabezpieczeń komputera, czas wykrycia hello, oraz hello protokół i port, który był używany. Ten blok również zawiera listę kroków korygowania, które mogą być używane toomitigate ten problem.

### <a name="network-communication-with-a-malicious-machine"></a>Komunikacja sieciowa ze złośliwą maszyną
Wykorzystując źródła analizy zagrożeń firmy Microsoft, usługa Azure Security Center może wykryć zagrożone maszyny, które komunikują się ze złośliwym adresem IP W wielu przypadkach adres złośliwego hello jest centrum dowodzenia i kontroli. W takim przypadku Centrum zabezpieczeń wykrył, że komunikacja hello została wykonana za pomocą modułu ładującego kuce złośliwego oprogramowania (znanej także jako [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)).

![alert o komunikacji sieciowej](./media/security-center-alerts-type/security-center-alerts-type-fig9.png)

Ten alert zapewnia informacje, które pozwala tooidentify hello zasobu, który był używany tooinitiate takiego ataku, hello zaatakowany zasób, IP ofiara hello IP osoby atakującej hello i czas wykrycia hello.

> [!NOTE]
> W celu zachowania poufności informacji prawdziwe adresy IP zostały usunięte z tego zrzutu ekranu.
>
>

### <a name="possible-outgoing-denial-of-service-attack-detected"></a>Możliwy wychodzący atak typu „odmowa usługi”
Nietypowe ruchu sieciowego pochodzącego z jednej maszyny wirtualnej może spowodować potencjalne typem ataku typu "odmowa usługi" tootrigger Centrum zabezpieczeń.

Oto przykład tego typu alertu:

![Wychodzący atak typu „odmowa usługi”](./media/security-center-alerts-type/security-center-alerts-type-fig10-new.png)

## <a name="resource-analysis"></a>Analiza zasobów
Analiza zasobów w Centrum zabezpieczeń koncentruje się na platformy jako usługi usługa (PaaS), na przykład hello integracji z hello [wykrywanie zagrożeń bazy danych SQL Azure](../sql-database/sql-database-threat-detection.md) funkcji. Na podstawie analizy hello wyników z tych obszarów, Centrum zabezpieczeń wyzwala alert związane z zasobami.

### <a name="potential-sql-injection"></a>Potencjalna iniekcja SQL
Iniekcja kodu SQL jest atak, gdzie złośliwego kodu zostaną wstawione do ciągów, które później zostaną przekazane tooan wystąpienia programu SQL Server dla analizy i wykonywanie. Każda procedura tworząca instrukcje SQL powinna zostać przejrzana pod kątem zagrożenia iniekcją, ponieważ oprogramowanie SQL Server wykonuje wszystkie otrzymane zapytania, które mają poprawną składnię. Wykrywanie zagrożeń SQL używa uczenia maszynowego, analizy behawioralnej i anomalii wykrywania toodetermine podejrzane zdarzenia, które może być przeprowadzana w bazach danych Azure SQL. Na przykład:

* Próba dostępu do bazy danych przez byłego pracownika
* Ataki polegające na iniekcji SQL
* Nietypowe zachowanie podczas dostępu do bazy danych produkcyjnych tooa w domu przez użytkownika

![Alert o potencjalnej iniekcji SQL](./media/security-center-alerts-type/security-center-alerts-type-fig11.png)

Hello informacje w tym alercie mogą być używane tooidentify atak powitania zasobów, czas wykrycia hello i stan hello atak powitania. Zapewnia również połączenie toofurther dochodzenia kroki.

### <a name="vulnerability-toosql-injection"></a>Luki w zabezpieczeniach tooSQL iniekcji
Ten alert jest wyzwalany, gdy w bazie danych zostanie wykryty błąd aplikacji, Ten alert może oznaczać, że ataków iniekcji tooSQL możliwe luki w zabezpieczeniach.

![Alert o potencjalnej iniekcji SQL](./media/security-center-alerts-type/security-center-alerts-type-fig12-new.png)

### <a name="unusual-access-from-unfamiliar-location"></a>Nietypowy dostęp z nieznanej lokalizacji
Ten alert jest wyzwalany, gdy na powitania serwera, który nie była widoczna w hello ostatnim okresie wykryto zdarzenie dostępu z adresu IP doświadczenia w pracy.

![Alert o nietypowym dostępie](./media/security-center-alerts-type/security-center-alerts-type-fig13-new.png)

## <a name="contextual-information"></a>Informacje kontekstowe
Podczas badania analityków muszą tooreach dodatkowy kontekst verdict o hello rodzaj hello zagrożeń i w jaki sposób toomitigate go.  Na przykład wykryto anomalii sieci, ale bez zrozumienia co dzieje się w sieci hello lub z uwzględnieniem toohello docelowe zasobem on jest każdy twardych toounderstand obok tootake jakie akcje. tooaid ze specyfikacją, zdarzenia zabezpieczeń mogą zawierać artefaktów, zdarzenia powiązane i informacje, które mogą pomóc badający hello. Witaj dostępności dodatkowe informacje będą się różnić w zależności na hello typu wykrytych hello konfiguracji środowiska i nie będą dostępne dla wszystkich zdarzeń zabezpieczeń.

Jeśli dostępne są dodatkowe informacje, zostanie wyświetlona w hello naruszające poniżej hello Lista alertów. Może ono zawierać informacje, takie jak:

- Zdarzenia czyszczenia dziennika
- Urządzenie PNP podłączone z nieznanego urządzenia
- Alerty, względem których nie można wykonać żadnych działań 

![Alert o nietypowym dostępie](./media/security-center-alerts-type/security-center-alerts-type-fig20.png) 


## <a name="see-also"></a>Zobacz też
W tym artykule przedstawiono o różnych typach hello alerty zabezpieczeń w Centrum zabezpieczeń. toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Obsługa zdarzeń naruszenia zabezpieczeń w usłudze Azure Security Center](security-center-incident.md)
* [Funkcje wykrywania usługi Azure Security Center](security-center-detection-capabilities.md)
* [Przewodnik planowania i obsługi usługi Azure Security Center](security-center-planning-and-operations-guide.md)
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md): często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.
