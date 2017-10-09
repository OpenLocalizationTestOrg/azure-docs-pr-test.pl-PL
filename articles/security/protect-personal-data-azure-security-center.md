---
title: "dane osobowe aaaProtect z Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ochrona danych osobistych, przy użyciu Centrum zabezpieczeń Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a>Ochrona danych osobowych z atakami i naruszeń: Centrum zabezpieczeń Azure

Ten artykuł pomoże Ci zrozumieć, jak dane osobowe tooprotect Centrum zabezpieczeń Azure toouse z naruszeń i ataków.

## <a name="scenario"></a>Scenariusz 

Firma rejs dużych, siedzibą hello Stanów Zjednoczonych, rozwija trasy toooffer jego operacji w hello Śródziemnego i Bałtyckiego mórz oraz hello brytyjskich. toohelp w tych działań, uzyskała mniejszych rejs wiersze na podstawie we Włoszech, Niemczech, Dania i hello Zjednoczone Królestwo

Witaj firma korzysta z danych firmowych toostore Microsoft Azure w chmurze hello. Dotyczy to również dane osobowe, takich jak nazwy, adresy, numery telefonów i informacje o karcie kredytowej. Zawiera również zasoby ludzkie informacji takich jak:

- Adresy
- Numery telefonów
- Numery identyfikacyjne podatku
- Inne informacje

wiersz rejs Hello zachowuje również dużej bazy danych elementów członkowskich programu osób trzecich i lojalność. Pracownikom firmy dostępu hello sieci z biurach zdalnych i agentów podróży hello firmy znajdujących się wokół Witaj świecie mają dostęp do zasobów firmowych toosome.
Dane osobowe są przesyłane w sieci hello między tymi lokalizacjami i centrum danych firmy Microsoft hello.

## <a name="problem-statement"></a>Opis problemu

Witaj firmy zależy od zagrożeń hello ataków na ich zasobów platformy Azure. Chcą narażenia tooprevent osób toounauthorized danych osobowych pracowników i klientów. Chcą, aby uzyskać wskazówki dotyczące zarówno związanych z zapobieganiem i odpowiedzi/korygowania, a także efektywny sposób toomonitor hello trwającą bezpieczeństwa zasobów w chmurze.
Muszą one silne linię obrony przed atakami współczesnych zaawansowane i organizowane.

## <a name="company-goal"></a>Celem firmy

Jednym z celów firmy hello jest tooensure hello prywatności danych osobowych pracowników i klientów, aby chronić go przed zagrożeniami. Jest jednym z celów ich toorespond, natychmiast toosigns toomitigate naruszenia hello wpływ. Wymaga to sposób tooassess hello bieżący stan zabezpieczeń, identyfikację narażone konfiguracji i usuwać z nich.

## <a name="solutions"></a>Rozwiązania

Microsoft Azure Security Center (ASC) zapewnia zabezpieczenia zintegrowane monitorowanie i zasady rozwiązania do zarządzania. Zapewnia łatwy w użyciu i skuteczne zapobieganie, wykrywanie i odpowiedzi możliwości.

### <a name="prevention"></a>Zapobieganie

ASC pomaga zapobiec naruszeń włączając tooset zasady zabezpieczeń, dostęp w czasie i zaimplementować zalecenia dotyczące zabezpieczeń.

Zasady zabezpieczeń określają hello zestaw kontrolek zalecane dla zasobów w hello określonej subskrypcji. Tylko w czasie dostępu może być używane toolock tooyour ruch przychodzący maszynach wirtualnych platformy Azure, zmniejszenie zagrożeń tooattacks w dół. Zalecenia dotyczące zabezpieczeń są tworzone przez ASC po przeanalizowaniu hello stan zabezpieczeń zasobów platformy Azure.

#### <a name="how-do-i-set-security-policies-in-asc"></a>Jak ustawić zasady zabezpieczeń w ASC?

Zasady zabezpieczeń można skonfigurować dla każdej subskrypcji. toomodify zasady zabezpieczeń, musi być właścicielem lub współautorem subskrypcji. W portalu Azure hello hello następujące:

1. Wybierz **zasad** hello ASC w pulpicie nawigacyjnym.

2. Wybierz subskrypcję hello, na którym ma zostać tooenable hello zasad.

3. Wybierz **zasady zapobiegania** tooconfigure zasady dla subskrypcji. **Zbieranie danych z maszyn wirtualnych** powinna być ustawiona zbyt**na.**

4. W hello **zasady zapobiegania** opcji wybierz **na** tooenable hello zalecenia dotyczące zabezpieczeń związane hello subskrypcji.

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

Aby uzyskać szczegółowe instrukcje i informacje o wszystkich hello zaleceń dotyczących zasad, które mogą być włączone, zobacz [ustawić zasady zabezpieczeń w Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).

#### <a name="how-do-i-configure-just-in-time-access-jit"></a>Jak skonfigurować tylko w czasie dostępu (JIT)?

Po włączeniu JIT Centrum zabezpieczeń blokuje ruch przychodzący tooyour maszynach wirtualnych platformy Azure przez tworzenie reguły NSG. Wybierz porty hello na powitania toowhich maszyny Wirtualnej zostanie zablokowana ruchu przychodzącego. toouse JIT dostępu, hello następujące:

1. Wybierz hello **bezpośrednio w kafelku dostęp maszyny Wirtualnej czas** na powitania ASC bloku.

2. Wybierz hello **zalecane** kartę.

3. W obszarze **maszyn wirtualnych**, wybierz hello maszyn wirtualnych, które mają tooenable. Spowoduje to umieszczenie znacznikiem wyboru tooa dalej maszyny Wirtualnej. 
4. Wybierz **włączyć JIT** na maszynach wirtualnych.
5. Wybierz pozycję **Zapisz**.

Następnie można zobaczyć hello domyślnych portów, które ASC zaleca włączana na potrzeby JIT. Można również dodać i skonfigurować nowy port, na którym ma zostać hello tooenable tylko w rozwiązaniu czasu. Witaj **bezpośrednio w dostęp do maszyny Wirtualnej czasu** kafelka w Centrum zabezpieczeń hello pokazuje liczbę hello skonfigurowana dla dostępu JIT maszyn wirtualnych. Zawiera także hello liczba żądań zatwierdzonych dostępu wprowadzone w hello ostatniego tygodnia.

![](media/protect-personal-data-azure-security-center/jit-vm.png)

Aby uzyskać instrukcje dotyczące toodo, oraz dodatkowe informacje na temat tylko w czasie dostępu, zobacz [zarządzanie dostępem do maszyny wirtualnej przy użyciu tylko w czasie.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)

#### <a name="how-do-i-implement-asc-security-recommendations"></a>Jak wdrożyć ASC zalecenia dotyczące zabezpieczeń?

Po znalezieniu potencjalnych luk w zabezpieczeniach usługa Security Center tworzy odpowiednie zalecenia. zalecenia Hello pomocne hello proces konfigurowania kontrolek hello potrzebne. 
1. Wybierz hello **zalecenia** kafelka na pulpicie nawigacyjnym ASC hello.

2. Wyświetl zalecenia hello, które są wyświetlane w formacie tabeli, w której każdy wiersz zawiera jeden zalecenia.

3. Wybierz zalecenia toofilter **filtru** i wybierz hello ważność i stan wartości mają toosee.

4. toodismiss rekomendację, która nie ma zastosowania, można kliknij prawym przyciskiem myszy i wybierz **odrzucenia.**

5. Należy ocenić, które zalecenie powinny być stosowane najpierw.

6. Stosować zalecenia hello w kolejności priorytetów.

Listę możliwych zalecenia i przewodników dotyczących tooapply, zobacz [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)

### <a name="detection-and-response"></a>Wykrywanie i odpowiedzi

Wykrywanie i odpowiedzi go razem można dowolnie toorespond możliwie jak najszybciej po wykryciu zagrożenia.
Wykrywanie zagrożeń ASC polega na automatyczne zbieranie informacji o zabezpieczeniach z zasobów platformy Azure, hello sieci i rozwiązań partnerskich połączonych. ASC szybko może aktualizować algorytmy wykrywania, jak osoby atakujące wersji nowy, coraz bardziej zaawansowany luki w zabezpieczeniach. Aby uzyskać szczegółowe informacje dotyczące sposobu działania wykrywanie zagrożeń ASC firmy, zobacz [funkcji wykrywania Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a>Jak zarządzać i odpowiadanie na alerty toosecurity?

Lista alertów zabezpieczeń uporządkowanych według priorytetu jest wyświetlany w Centrum zabezpieczeń oraz hello informacje potrzebne tooquickly Zbadaj hello problem. Centrum zabezpieczeń zawiera także zalecenia dotyczące tooremediate atak. alerty zabezpieczeń, wykonaj następujące hello toomanage:

1. Wybierz hello **alerty zabezpieczeń** kafelka na pulpicie nawigacyjnym ASC hello. To przedstawia szczegółowe informacje o każdym alercie.

2. Wybierz alerty toofilter na podstawie daty, stanu i ważności, **filtru** a następnie wybierz wartości hello ma toosee.

3. toorespond tooan alert, zaznacz go i przejrzyj informacje hello, a następnie wybierz hello zaatakowany zasób.

4. W hello **opis** pola, zobaczysz szczegółowe informacje, łącznie z zalecanych czynności naprawczych.

![](media/protect-personal-data-azure-security-center/security-alerts.png)

Aby uzyskać szczegółowe instrukcje dotyczące odpowiada alerty toosecurity, zobacz [toosecurity zarządzanie i odpowiada alertów w Centrum zabezpieczeń Azure.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)

Aby uzyskać dalszą pomoc w badania alertów zabezpieczeń firmy hello można zintegrować ASC alerty z własnego rozwiązania SIEM, za pomocą [integracji dziennika Azure](https://aka.ms/AzLog).

#### <a name="how-do-i-manage-security-incidents"></a>Jak zarządzać przypadki naruszenia zabezpieczeń?

Zdarzenia zabezpieczeń ASC, to agregacji wszystkich alertów dla zasobu, które są wyrównane z wzorców łańcucha kill. Zdarzenie będzie ujawnić hello listę powiązanych alertów, dzięki czemu możesz tooobtain więcej informacji na temat każdego wystąpienia. Zdarzenia są wyświetlane w powitalne Kafelek alerty zabezpieczeń i bloku.

tooreview i zarządzania incydentami zabezpieczeń, hello następujące:

1. Wybierz hello **alerty zabezpieczeń** kafelka. w przypadku wykrycia zdarzenia zabezpieczeń będą wyświetlane w obszarze wykresu alerty zabezpieczeń hello. Jej ikonę, która różni się od innych alertów.

2. Wybierz zdarzenia toosee hello więcej szczegółów dotyczących tego zdarzenia zabezpieczeń. Dodatkowe szczegóły obejmują jego pełny opis, jego ważność, jego bieżący stan, atak powitania zasobów, procedura korygowania hello hello zdarzenia i hello alertów, które wchodzą w skład tego zdarzenia.

Można filtrować toosee **tylko zdarzenia**, **alerty tylko**, lub **zarówno**.

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a>Jak uzyskać dostęp hello raportu analizy zagrożeń

ASC analizuje informacje z wielu źródeł tooidentify zagrożeń. zespoły odpowiedzi na zdarzenia tooassist zbadać i eliminowanie zagrożeń, Centrum zabezpieczeń zawiera raport analizy zagrożeń, który zawiera informacje o hello zagrożenia, które zostało wykryte.

Centrum zabezpieczeń zawiera trzy raporty zagrożenia, które mogą się różnić na atak.
dostępne raporty Hello są:

- Raport grupy działań: zawiera głębokie dives do osoby atakujące, ich cele i taktyk.

- Raport kampanii: koncentruje się na szczegóły ataku określonej kampanii.

- Raport podsumowania zagrożeń: obejmuje wszystkie elementy w hello poprzednich dwóch raportów.

Informacje tego typu jest bardzo przydatny podczas procesu odpowiedzi na zdarzenia hello, w przypadku badania trwającą hello źródło toounderstand atak powitania hello motywacji osoby atakującej i jakie toomitigate toodo wystawiać przenoszenie do przodu.

1. tooaccess hello analizy zagrożeń raportu, hello następujące:

2. Wybierz hello **alerty zabezpieczeń** kafelka na pulpicie nawigacyjnym ASC hello.

3. Wybierz alert zabezpieczeń hello, dla której ma zostać tooobtain więcej informacji.

4. W hello **raporty** kliknij raport analizy zagrożeń toohello łącze hello.

5. Spowoduje to otwarcie pliku PDF hello, który można pobrać.

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

Aby uzyskać dodatkowe informacje na temat hello raportu analizy zagrożeń ASC, zobacz [raport analizy zagrożeń z Centrum zabezpieczeń Azure.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

### <a name="assessment"></a>Ocena

toohelp do testowania, oceny i oceny strukturę bezpieczeństwa, ASC zapewnia oceny luk w zabezpieczeniach zintegrowane z Qualys agentów chmurze jako część jej składników zalecenia dotyczące maszyny wirtualnej.

Witaj Qualys agenci będą raportować luki w zabezpieczeniach danych toohello Qualys platformy zarządzania, który z kolei odsyła luki w zabezpieczeniach i danych monitorowania kondycji powrotem tooASC. Witaj tooadd zalecenie rozwiązanie do oceny luk w zabezpieczeniach jest wyświetlany w hello **zalecenia** bloku na pulpicie nawigacyjnym ASC hello.

Po zainstalowaniu rozwiązanie do oceny luk w zabezpieczeniach hello w celu hello wirtualna hello toodetect maszyny Wirtualnej i zidentyfikować luki w zabezpieczeniach systemu i aplikacji skanowania Centrum zabezpieczeń. Wykryto problemy są wyświetlane w obszarze hello **zalecenia dotyczące maszyny wirtualnej** opcji.

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a>Jak wdrożyć rozwiązanie do oceny luk w zabezpieczeniach? 

Jeśli maszyna wirtualna nie ma już wdrożone rozwiązanie do oceny luk w zabezpieczeniach zintegrowanego, Centrum zabezpieczeń zaleca się ona zainstalowana.

1. Na pulpicie nawigacyjnym ASC hello, na powitania **zalecenia** bloku, wybierz opcję **Dodaj rozwiązanie do oceny luk w zabezpieczeniach.**

2. Wybierz maszyny wirtualne hello miejscu rozwiązanie do oceny luk w zabezpieczeniach hello tooinstall.

3. Polecenie **zainstalowania na maszynach wirtualnych [numer].**

4. Wybierz rozwiązanie partnerskie w hello Azure Marketplace, lub na podstawie **użyć istniejącego rozwiązania,** wybierz **Qualys.**

5. Ustawienia aktualizacji automatycznego hello lub wyłącz można włączyć w hello **rozwiązań partnerskich** bloku.

Aby uzyskać dalsze instrukcje dotyczące tooimplement rozwiązania oceny luk w zabezpieczeniach, zobacz [oceny luk w zabezpieczeniach w Centrum zabezpieczeń Azure.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)

## <a name="next-steps"></a>Następne kroki

- [Przewodnik Szybki start dotyczący Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [Wprowadzenie tooAzure Centrum zabezpieczeń](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [Integrowanie z integracją dzienników Azure alerty Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [Zwiększenie wydajności Centrum zabezpieczeń Azure z oceny luk w zabezpieczeniach zintegrowane](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
