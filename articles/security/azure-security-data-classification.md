---
title: aaaData klasyfikacji dla platformy Azure | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera toohello wprowadzenie podstawowe informacje dotyczące klasyfikacji danych i zaznacza jego wartość, w szczególności w kontekście hello chmury obliczeniowych oraz przy użyciu programu Microsoft Azure"
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ROBOTS: NOINDEX
redirect_url: https://aka.ms/data-classification-cloud
ms.assetid: 91d4afed-b80f-4a26-b526-b52b9c858cfb
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/18/2017
ms.author: yurid
ms.openlocfilehash: 726da2482beab3bf7b0ac33510f2b523d5074df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-classification-for-azure"></a>Klasyfikacja danych na platformie Azure
Ten artykuł zawiera toohello wprowadzenie podstawowe informacje dotyczące klasyfikacji danych i zaznacza jego wartość, w szczególności w kontekście hello chmury obliczeniowych oraz przy użyciu programu Microsoft Azure. 

## <a name="data-classification-fundamentals"></a>Podstawowe informacje dotyczące klasyfikacji danych
Klasyfikacja danych powiodło się w organizacji wymaga szerokiego świadomości potrzeb organizacji i dokładne zrozumienie, w którym znajdują się zasobów danych.  

Istnieją dane w jednym z trzech stanów podstawowe: 

* Magazynowane 
* W procesie 
* W drodze 

Wszystkie trzy stany wymagają unikatowych rozwiązań technicznych do klasyfikacji danych, ale hello zastosowanych zasad klasyfikacji danych powinny być hello takie same dla każdego. Dane, które jest sklasyfikowany jako poufny musi toostay poufne podczas magazynowane, w procesie i podczas przesyłania. 

Dane można także strukturalnych lub bez struktury. Znaleziono w bazach danych strukturalnych procesów klasyfikacji typowe dla hello i arkusze kalkulacyjne są mniej złożony i czasochłonny toomanage niż danych niestrukturalnych, takich jak dokumenty, kod źródłowy i poczty e-mail. 

> [!TIP]
> Aby uzyskać więcej informacji na temat funkcji platformy Azure i najlepsze rozwiązania dotyczące szyfrowania danych przeczytaj [najlepsze rozwiązania szyfrowania danych Azure](azure-security-data-encryption-best-practices.md)
> 
> 

Ogólnie rzecz biorąc, organizacje będą mieć więcej danych niestrukturalnych niż dane strukturalne. Niezależnie od tego, czy danych strukturalnych lub bez struktury jest ważne w przypadku należy toomanage danych czułości. W przypadku prawidłowego wdrożenia klasyfikacji danych pomaga zapewnić, że poufne dane, które zasoby są zarządzane za pomocą nadzoru większa niż zasobów danych, które są uważane za publiczne lub wolnego toodistribute. 

### <a name="controlling-access-toodata"></a>Kontrolowanie dostępu toodata
Uwierzytelnianie i autoryzacja są często pomylić ze sobą i ich role błędnie interpretowane. W rzeczywistości są zupełnie różne, jak pokazano w powitania po rysunku.  

![Dostęp do danych i kontrola](./media/azure-security-data-classification/azure-security-data-classification-fig1.png)

### <a name="authentication"></a>Authentication
Uwierzytelnianie zazwyczaj składa się z co najmniej dwie części: nazwa użytkownika lub użytkownika identyfikator tooidentify użytkownika oraz token, takie jak hasła, tooconfirm, który hello poświadczenie nazwy użytkownika jest prawidłowy. proces Hello nie zapewnia hello uwierzytelnionego użytkownika, dostęp do elementów tooany lub usług. sprawdzi, czy ten użytkownik hello jest kto mówią, że są one.   

> [!TIP]
> [Usługa Azure Active Directory](../active-directory/active-directory-whatis.md) zapewnia usługi tożsamości opartej na chmurze, które pozwalają tooauthenticate i autoryzacji użytkowników. 
> 
> 

### <a name="authorization"></a>Autoryzacja
Autoryzacja jest hello proces udostępniania tooaccess możliwości hello uwierzytelnionego użytkownika aplikacji, zestaw danych, pliku danych lub innego obiektu. Przypisywanie toouse prawa hello uwierzytelnionych użytkowników, modyfikowanie lub usuwanie elementów, które mogą uzyskiwać dostęp do wymaga uwagi toodata klasyfikacji. 

Implementacja mechanizmu toovalidate poszczególnych użytkowników potrzebuje tooaccess pliki i informacje w zależności od kombinację roli, zasady zabezpieczeń i zagadnienia dotyczące zasad ryzyka wymaga pomyślnej autoryzacji. Na przykład dane z określonych aplikacji (LOB)-biznesowych może nie być konieczne toobe dostępne dla wszystkich pracowników, a tylko mały podzbiór pracownicy będą prawdopodobnie muszą uzyskiwać dostęp do plików zasobów (HR) toohuman. Jednak dla organizacji toocontrol kto ma dostęp do danych, jak również jako warunkami i sposobami, efektywną systemu do uwierzytelniania użytkowników należy spełnić. 

> [!TIP]
> platformie Microsoft Azure upewnij się, że tooleverage based kontroli dostępu (RBAC) toogrant tylko hello takiego dostępu czy użytkownicy muszą tooperform swoich zadań. Odczyt [Użyj roli przypisania toomanage dostępu tooyour usługi Azure Active Directory zasobów](../active-directory/role-based-access-control-configure.md) Aby uzyskać więcej informacji. 
> 
> 

### <a name="roles-and-responsibilities-in-cloud-computing"></a>Role i obowiązki w chmury obliczeniowej
Mimo że dostawców w chmurze może ułatwić zarządzanie ryzykiem, klienci muszą tooensure tego Zarządzanie klasyfikacją danych i wymuszania jest poprawnie zaimplementowana tooprovide hello odpowiedni poziom usług zarządzania danych.  

Klasyfikacji danych, które różnią się obowiązki w oparciu modelem usługi chmury, które jest już na miejscu, jak pokazano w powitania po rysunku. trzy modele usług chmury podstawowej Hello są infrastruktura jako usługa (IaaS), platformy jako usługa (PaaS), a oprogramowanie jako usługa (SaaS). Implementacja mechanizmów klasyfikacji danych również różni się zależnie od zależy od hello i oczekiwań hello dostawcy usług w chmurze. 

![Role](./media/azure-security-data-classification/azure-security-data-classification-fig2.png)

Chociaż jest odpowiedzialny za klasyfikowania danych, dostawców w chmurze powinny być napisane zobowiązań dotyczących sposobu będzie bezpieczny i zadbać o zachowanie poufności hello powitania klienta danych przechowywanych w chmurze.  

* **Dostawcy IaaS** wymagania są ograniczone tooensuring, który hello środowisko wirtualne mogą obsługiwać funkcje klasyfikacji danych i wymagań dotyczących zgodności klienta. Dostawcy IaaS ma mniejszy roli w klasyfikacji danych, ponieważ potrzebna jest tylko tooensure, że dane klienta adresów wymagań dotyczących zgodności. Jednak dostawców musi nadal upewnij się, że ich środowisk wirtualnych adresów wymagania dotyczące klasyfikacji danych w toosecuring dodanie centrów danych.
* **Dostawców PaaS** obowiązki mogą być mieszane, ponieważ platforma hello mogą być używane w zabezpieczeń tooprovide warstwowego podejścia narzędzia klasyfikacji. PaaS dostawcy mogą być odpowiedzialne za uwierzytelnianie i prawdopodobnie niektórych reguł autoryzacji i podać zabezpieczeń i warstwy aplikacji tootheir funkcji klasyfikacji danych. Znacznie jak dostawcy IaaS dostawcy PaaS muszą tooensure, która ich platforma jest zgodna z żadnych wymagań dotyczących klasyfikacji odpowiednie dane.
* **Dostawców w modelu SaaS** często są traktowane jako część łańcucha autoryzacji i będzie konieczne tooensure, który hello danych przechowywanych w aplikacji SaaS hello mogą być kontrolowane przez typ klasyfikacji. Aplikacji SaaS mogą służyć do aplikacji biznesowych, a z natury muszą tooprovide hello tooauthenticate oznacza i autoryzować dane, które są używane i przechowywane. 

## <a name="classification-process"></a>Proces klasyfikacji
Organizacje, które rozumieją hello potrzebne do klasyfikacji danych i ma on dostęp podstawowego żądania tooimplement: gdzie toobegin?

Jednym ze sposobów skuteczne i proste klasyfikacji danych tooimplement jest toouse hello planu, należy wyboru, USTAWA modelu z [MOF](https://technet.microsoft.com/solutionaccelerators/dd320379.aspx). następujące Hello rysunek wykresy hello zadania, które są wymagane toosuccessfully klasyfikacji danych implementuje w tym modelu.  

1. **PLANOWANIE**. Identyfikowanie zasobów danych, program klasyfikacji danych niejawnego toodeploy hello i utworzyć profile ochrony. 
2. **CZY**. Po uzgodnionych zasad klasyfikacji danych wdrożyć hello program i implementować technologie wymuszania, zgodnie z potrzebami dla poufnych danych.  
3. **SPRAWDŹ**. Sprawdź i zweryfikować raporty tooensure, które skutecznie adresowania hello narzędzia i stosowane metody hello zasady klasyfikacji. 
4. **DZIAŁANIE**. Sprawdź stan hello dostępu do danych i przejrzyj pliki i dane, które wymagają poprawek za pomocą przeklasyfikowania i zmiany tooadopt metodologii poprawki i nowe zagrożenia tooaddress.  

![Planowanie,, sprawdź, działania](./media/azure-security-data-classification/azure-security-data-classification-fig3.png)

### <a name="select-a-terminology-model-that-addresses-your-needs"></a>Wybierz model terminologii, którego dotyczy potrzeb
Istnieje kilka typów procesów klasyfikacji danych, w tym procesów ręcznych, oparte na lokalizacji procesom klasyfikacji danych na podstawie lokalizacji użytkownika lub komputera, na podstawie aplikacji procesy, takie jak Klasyfikacja specyficzny dla bazy danych i automatyczne procesy używane przez różne technologie, niektóre z nich są opisane w sekcji "Zabezpieczania poufnych danych" hello w dalszej części tego artykułu.  

W tym artykule przedstawiono dwa modele uogólniony terminologii oparte na powszechnie używane i wzięty pod uwagę branży modeli. Te modele terminologii, które zapewnia trzy poziomy czułości klasyfikacji, są wyświetlane w hello w poniższej tabeli.  

> [!NOTE]
> Podczas klasyfikowania plik lub zasób, że łączy, które należy określić dane, które zwykle może być klasyfikowane na różnych poziomach, hello najwyższy poziom klasyfikacji występuje hello ogólnej klasyfikacji. Na przykład plik zawierający dane poufne i ograniczeniami powinny być klasyfikowane jako ograniczone.  
> 
> 

| **Czułość** | **Terminologia modelu 1** | **Terminologia modelu 2** |
| --- | --- | --- |
| Wysoka |Poufne |Ograniczone |
| Medium |Tylko do użytku wewnętrznego |Wielkość liter |
| Niska |Publiczne |Bez ograniczeń |

#### <a name="confidential-restricted"></a>Poufne (ograniczony)
Informacje, które zostanie sklasyfikowany jako poufny lub zastrzeżony zawiera dane, które mogą być tooone krytycznego więcej osób lub organizacji, jeśli naruszone lub utraty. Takie informacje często znajduje się na zasadzie "potrzeby tooknow" i mogą być następujące: 

* Dane osobowe, w tym dane osobowe Social Security lub numery identyfikacyjne national, numery passport, numery kart kredytowych, sterownika numerów licencji, medyczne rekordów i numery identyfikatorów zasad ubezpieczenia zdrowotnego.  
* Dokumentów finansowych, w tym finansowych lub numery kont takich jak sprawdzanie inwestycji konta. 
* Materiał biznesowych, takich jak dokumenty lub dane, które jest określonych własności intelektualnej.  
* Dane prawnych, w tym potencjalnych materiałów prawnikiem uprawnieniach. 
* Dane uwierzytelniania, w tym klucze prywatne kryptografii, pary hasło nazwy użytkownika lub innych sekwencji identyfikacji, takie jak biometryczne plików kluczy prywatnych. 

Dane, które jest sklasyfikowany jako poufny często ma przepisami i wymagań dotyczących zgodności dla obsługi danych. 

#### <a name="for-internal-use-only-sensitive"></a>Do użytku wewnętrznego tylko (liter)
Informacje, które jest klasyfikowany jako średnia czułości zawiera pliki i dane, które nie miałoby poważny wpływ na poszczególne i/lub organizacji, w przypadku utraty lub zniszczenia. Takie informacje mogą być następujące: 

* Wiadomości e-mail, z których większość można usunąć lub rozproszonych bez powodowania kryzysu (bez skrzynek pocztowych lub adres e-mail osoby, które są identyfikowane w klasyfikacji poufne hello).  
* Dokumenty i pliki, które nie zawierają dane poufne.

Ogólnie rzecz biorąc ta klasyfikacja obejmuje wszystkie elementy, które nie są poufne. Ta klasyfikacja może zawierać większości danych biznesowych, ponieważ większość plików, które są zarządzane lub są używane bieżące mogą być klasyfikowane jako poufne. Z wyjątkiem hello danych, który jest opublikowany lub poufne wszystkie dane w obrębie organizacji firm mogą być klasyfikowane jako poufne domyślnie. 

#### <a name="public-unrestricted"></a>Public (bez ograniczeń)
Informacje, które jest klasyfikowany jako publiczną, zawiera dane i pliki, które nie są krytyczne toobusiness musi lub operacji. Ta klasyfikacja może także zawierać dane, który został celowo wydanych toohello publicznej do użytku, takich jak marketingu anonsów materiałów lub naciśnij klawisz. Ponadto ta klasyfikacja może zawierać dane, takie jak wiadomości-śmieci e-mail przechowywane przez usługę poczty e-mail. 

### <a name="define-data-ownership"></a>Zdefiniuj własność danych
Jest ważne tooestablish wyczyść custodial łańcucha własności dla wszystkich zasobów danych. Hello Poniższa tabela zawiera dane różnych własność ról w wysiłków klasyfikacji danych oraz ich odpowiednich praw.  

| **Rola** | **Tworzenie** | **Zmodyfikuj lub usuń** | **Delegat** | **Odczyt** | **Archiwizacji i przywracania** |
| --- | --- | --- | --- | --- | --- |
| Właściciel |X |X |X |X |X |
| Niejawnego | | |X | | |
| Administrator | | | | |X |
| Użytkownika\* | |X | |X | |

**Użytkownicy mogą otrzymać dodatkowych praw, takich jak edytowanie i usuwanie przez niejawnego* 

> [!NOTE]
> Ta tabela nie ma to pełna lista ról i uprawnień, ale tylko reprezentatywnej próbki. 
> 
> 

Witaj **właściciel zasobu danych** jest hello oryginalnego twórca hello danych, który można delegować prawa własności i przypisać nadzorcą jest. Podczas tworzenia pliku właściciela hello powinny być możliwe tooassign klasyfikacji, co oznacza, że mają one toounderstand odpowiedzialność niezbędne toobe sklasyfikowanych jako poufne na podstawie używanych w organizacji zasad. Wszystkie dane właściciela zasobów danych mogą być klasyfikowane automatycznie podobnie jak w przypadku tylko użytku wewnętrznego (wielkość liter), chyba że są one odpowiedzialne za będący właścicielem lub tworzenie typów danych poufnych (ograniczony). Często rolę właściciela hello zmieni się po klasyfikowania danych hello. Na przykład właściciela hello może utworzyć bazę danych informacji niejawnych i zrzeka się ich niejawnego danych toohello praw.  

> [!NOTE]
> Właściciele zawartości danych często używają usług, urządzeń i nośników, niektóre z nich osobistych, a niektóre z nich należy toohello organizacji. Zasady wyczyść organizacji pozwala zagwarantować, że użycie urządzeń przenośnych i urządzeń inteligentnych jest zgodnie z wytycznymi klasyfikacji danych.  
> 
> 

Witaj **niejawnego zasobów danych** jest przypisywany przez właściciela zasobów hello (lub ich delegata) toomanage hello zasobów zgodnie z tooagreements hello właściciel zasobu lub zgodnie z wymaganiami odpowiednich zasad. W idealnym przypadku hello niejawnego roli może być wdrożonych w automatyczny system. Niejawnego zasobów temu kontroli dostępu konieczne jest dostępny i jest odpowiedzialny za zarządzanie i ochrony zasobów delegowane opieki tootheir. obowiązki Hello hello niejawnego zasobów mogą obejmować:  

* Ochrona zasobów hello zgodnie z kierunku właściciel zasobu hello lub porozumieniu hello właściciel zasobu 
* Zapewnienie, że spełnione są zasady klasyfikacji 
* Informowanie właścicieli zasobów wszelkich zmian tooagreed — od formantów i/lub wprowadzonych zmian toothose poprzednich procedur ochrony 
* Właściciel zasobu usługi raportowania toohello o usunięcie tooor zmiany hello zasobów niejawnego obowiązki 
* **Administratora** reprezentuje użytkownika, który jest odpowiedzialny za zapewnienie, że integralność została zachowana, ale nie są właściciela zasobów danych, niejawnego lub użytkownika. W rzeczywistości wiele ról administratora dostępne usługi zarządzania kontenera danych bez potrzeby dostępu do danych toohello. Rola administrator Hello obejmuje kopii zapasowej i przywracania danych hello, obsługa rekordy zasobów hello, i wybieranie, nabywania i używania hello urządzenia i magazynu tego DOM hello zasoby. 
* Witaj zasobów użytkownika obejmuje każdy, kto uzyskuje dostęp toodata lub pliku. Przypisywanie dostępu jest często delegowane przez hello właściciela toohello zasobów niejawnego.  

### <a name="implementation"></a>Wdrażanie
Zagadnienia dotyczące zarządzania zastosować tooall metodologii klasyfikacji. Powyższe zagadnienia, musisz szczegółów tooinclude o tym, kto, co, gdzie, kiedy i dlaczego zasobu danych będzie można używany, dostęp do, zmienić lub usunąć. Wszystkie zarządzanie zasobami musi odbywać się zrozumieniu jak organizacji widoków jego ryzyka, ale proste metodologii mogą być stosowane zgodnie z definicją w procesie klasyfikacji danych hello. Dodatkowe zagadnienia dotyczące klasyfikacji danych obejmują hello wprowadzenie nowych aplikacji oraz narzędzia i zarządzanie zmianami po metodzie klasyfikacji.  

### <a name="reclassification"></a>Podziału
Przeklasyfikowania lub zmiana hello klasyfikacji stanu trwałego danych musi toobe wykonane, gdy użytkownik lub system określa ważność tego zasobu danych hello lub zmieniono profilu ryzyka. Tej pracy są istotne dla zapewnienia, że stan klasyfikacji hello nadal bieżącego toobe i prawidłowe. Większość zawartości, która nie jest sklasyfikowany ręcznie można automatycznie klasyfikowane lub na podstawie użycia niejawnego danych lub właściciela danych. 

### <a name="manual-data-reclassification"></a>Podział danych ręczne
W idealnym przypadku tej pracy będzie zapewnia hello szczegóły są przechwycenie i inspekcji. najbardziej prawdopodobną przyczyną Hello ręcznego podziału jest powody czułości lub przechowywane w formacie papieru lub dane tooreview wymagania, które pierwotnie został nieprawidłowo klasyfikowana rekordów. Ponieważ w tym dokumencie uwzględnia klasyfikacji danych i toohello przenoszenie danych w chmurze, wymagają uwagi w przypadku przez działania ręcznego podziału, a przeglądu zarządzania ryzykiem będzie idealne tooaddress wymagań dotyczących klasyfikacji. Ogólnie rzecz biorąc nakładu pracy będzie należy wziąć pod uwagę zasady organizacji hello o niezbędne toobe sklasyfikowane, hello domyślny stan klasyfikacji (wszystkich danych i jest wielkość liter, ale nie do poufnych plików) i zająć wyjątki dla danych o wysokim ryzyku. 

### <a name="automatic-data-reclassification"></a>Podział danych
Podział danych używa hello sam ogólne reguły jako ręcznej klasyfikacji. wyjątek Hello jest, że automatycznego rozwiązania można zapewnić, a następnie i stosowane zgodnie z potrzebami reguły. Klasyfikacja danych może odbywać się w ramach zasady wymuszania klasyfikacji danych, które można wymusić, gdy dane są przechowywane w użyciu i podczas przesyłania przy użyciu technologii autoryzacji.

* Na podstawie aplikacji. Przy użyciu określonych aplikacji domyślnie ustawia poziomu klasyfikacji. Na przykład dane z oprogramowanie (CRM) zarządzania relacjami z klientami, HR i narzędzia zarządzania rekordami kondycji jest poufne domyślnie. 
* Na podstawie lokalizacji. Lokalizacja danych może ułatwić identyfikację wrażliwości danych. Na przykład dane przechowywane przez HR lub działu finansowego jest bardziej prawdopodobne toobe charakteru poufnego.  

### <a name="data-retention-recovery-and-disposal"></a>Przechowywanie danych, odzyskiwania i usuwania
Odzyskiwanie danych i usuwania, takie jak podział danych jest ważnym aspektem zarządzania zasobów danych. Witaj zasady odzyskiwania danych i usuwania byłoby zdefiniowane przez zasady przechowywania danych i wykonywane w hello sam sposób jak podziału danych; nakładu pracy może być wykonane przez hello niejawnego i administrator ról jako wspólne zadania.  

Błąd toohave zasady przechowywania danych może oznaczać utratę lub awarię toocomply danych z wymogami przepisów i prawnych odnajdywania. Większość organizacji, które nie mają zasady przechowywania danych jasno określone zwykle toouse domyślnych zasad przechowywania "Zachowaj wszystko". Jednak zasady przechowywania ma dodatkowe zagrożenia w scenariuszach usługi w chmurze. 

Na przykład zasady przechowywania danych dla dostawcy usług w chmurze jest uznawana za podobnie jak w przypadku "hello obowiązywania subskrypcji hello" (tak długo, jak usługa hello jest płatnej dla hello dane zostaną zachowane). Umowę płatności do przechowywania nie może kierować zasady firmowe i przepisami przechowywania. Definiowanie zasad dotyczących poufnych danych można upewnij się, że dane są przechowywane i usunięte w oparciu o najlepsze rozwiązania. Ponadto można tworzyć zasady archiwizacji tooformalize zrozumienia, jakie dane powinny zostać usunięte z i kiedy. 

Zasady przechowywania danych należy spełnić hello wymagane przepisami i wymagania dotyczące zgodności, a także wymagania dotyczące przechowywania prawne firmy. Niejawne danych może powodować pytania dotyczące czas przechowywania i wyjątków dla danych, które były przechowywane u dostawcy; takie pytania są bardziej prawdopodobne w przypadku danych, który nie został poprawnie sklasyfikowany. 

> [!TIP]
> więcej informacji na temat zasad przechowywania danych platformy Azure i inne odczytując hello [umowę subskrypcji Online firmy Microsoft](https://azure.microsoft.com/support/legal/subscription-agreement/)
> 
> 

## <a name="protecting-confidential-data"></a>Ochrona poufnych danych.
Po sklasyfikowaniu danych Znajdowanie i implementacja metody tooprotect poufnych danych staje się integralną częścią każdej strategii wdrażania ochrony danych. Ochrona poufnych danych wymaga uwagi dodatkowe toohow dane są przechowywane i przekazywane w konwencjonalnych architektury także jak hello chmury. 

Ta sekcja zawiera podstawowe informacje o niektóre technologie, które można zautomatyzować wysiłków wymuszania toohelp ochrony danych, które zostało sklasyfikowane jako poufne. 

Jako hello po rysunek pokazuje, można wdrożyć tych technologii jako lokalnymi lub rozwiązań w chmurze — lub w sposób hybrydowe z niektórych ich wdrożonych lokalnie, a niektóre w chmurze hello. (Niektóre technologii, takich jak szyfrowania i zarządzania prawami również rozszerzyć toouser urządzenia).  

![Technologie](./media/azure-security-data-classification/azure-security-data-classification-fig4.png)

### <a name="rights-management-software"></a>Oprogramowanie do zarządzania prawami
Jedno rozwiązanie w celu zapobieżenia utracie danych jest oprogramowanie do zarządzania prawami. W przeciwieństwie do metod próbujące toointerrupt hello przepływ informacji w punkty wyjścia w organizacji oprogramowanie do zarządzania prawami działa na poziomach głębokości w ramach technologii magazynowania danych. Dokumenty są szyfrowane i kontrolować, kto ich odszyfrować używa kontroli dostępu, które są zdefiniowane w rozwiązania kontrolki uwierzytelniania, takie jak usługi katalogowej.  

> [!TIP]
> można użyć usługi Azure Rights Management (Azure RMS) jako hello danych tooprotect rozwiązanie ochrony informacji w różnych scenariuszach. Odczyt [co to jest usługa Azure Rights Management?](https://docs.microsoft.com/rights-management/understand-explore/what-is-azure-rms) Aby uzyskać więcej informacji o tym rozwiązaniu platformy Azure.
> 
> 

Zalety hello oprogramowanie do zarządzania prawami między innymi: 

* Chronionym poufne informacje. Użytkownicy mogą chronić swoje dane bezpośrednio przy użyciu aplikacji z obsługą zarządzania prawami. Nie są wymagane żadne dodatkowe czynności — tworzenie dokumentów, wysyłania wiadomości e-mail oraz publikowania danych oferują środowisko ochrony spójności danych. 
* Ochrona porusza się z danymi hello. Klienci zachowuje kontrolę nad kto ma dostęp do danych tootheir, zarówno w chmurze hello, istniejącej infrastruktury IT, lub na pulpicie użytkownika hello. Organizacje mogą wybierz tooencrypt swoje dane i ograniczanie dostępu zgodnie z wymaganiami biznesowymi tootheir. 
* Domyślne zasady ochrony informacji. Administratorzy i użytkownicy mogą używać zasad standardowe przypadku wielu typowych scenariuszy biznesowych, takich jak "Firmy poufne — tylko do odczytu" i "Nie przekazuj." Bogaty zestaw praw użytkowania są obsługiwane, takich jak odczytu, kopiowania, drukowania, zapisywania, edytowania i do przodu tooallow elastyczność podczas definiowania niestandardowe prawa użytkowania. 

> [!TIP]
> chronić dane w usłudze Azure Storage za pomocą [szyfrowanie usługi Magazyn Azure](../storage/storage-service-encryption.md) dla przechowywanych danych. Można również użyć [szyfrowania dysków Azure](azure-security-disk-encryption.md) toohelp ochrony danych znajdujących się na dyski wirtualne użyte maszyn wirtualnych platformy Azure.
> 
> 

### <a name="encryption-gateways"></a>Bramy szyfrowania
Bramy szyfrowania działanie w swoich własnych usług szyfrowania tooprovide warstwy, przekierowanie wszystkich danych na podstawie toocloud dostępu. Ta metoda nie należy mylić z tym wirtualnej sieci prywatnej (VPN). Bramy szyfrowania są zaprojektowane tooprovide przezroczyste warstwy toocloud rozwiązań.   

Bramy szyfrowania zapewnić toomanage oznacza i zabezpieczonych danych, które zostało sklasyfikowane jako poufne hello przesyłanych danych, a także magazynowane dane są szyfrowane.  

Bramy szyfrowania są umieszczane w hello przepływ danych między urządzeniami użytkowników oraz usług szyfrowania i odszyfrowywania tooprovide w centrach danych aplikacji. Tych rozwiązań, takich jak sieci VPN, znajdują się głównie rozwiązań lokalnych. Są one zaprojektowane tooprovide innych firm kontrolę nad kluczami szyfrowania, który pomaga ograniczyć ryzyko związane z hello umieszczenia zarówno hello danych i zarządzania kluczami z jednego dostawcę. W przypadku takich rozwiązań są zaprojektowane, podobnie jak szyfrowanie, toowork bezproblemowo i w przezroczysty sposób między użytkownikami i hello usługi. 

> [!TIP]
> można użyć tooextend Azure ExpressRoute sieci lokalnych do chmury Microsoft hello przez dedykowane połączenie prywatne. Odczyt [opis techniczny ExpressRoute](../expressroute/expressroute-introduction.md) uzyskać więcej informacji dotyczących tej funkcji. Opcje dla innego między lokalnym łączność między siecią lokalną i [Azure to VPN lokacja lokacja](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).
> 
> 

### <a name="data-loss-prevention"></a>Zapobieganie utracie danych
Ważną kwestią jest utrata danych (czasami określonego tooas wycieku danych), a hello zapobiegania utracie danych zewnętrznych za pomocą wewnętrznych złośliwe i przypadkowe jest podstawowym w przypadku wielu organizacji.  

Technologie zapobiegania (DLP) utraty danych pozwala zagwarantować rozwiązania, takie jak usługi poczty e-mail nie wysyłaj danych, które zostało sklasyfikowane jako poufne. Organizacje mogą korzystać z funkcji DLP w istniejących produktów toohelp zapobiec utracie danych. Takie funkcje za pomocą zasad, które można łatwo utworzyć od podstaw lub za pomocą szablonu dostarczana przez dostawcę oprogramowania hello.  

Technologie DLP może wykonywać szczegółowa analiza zawartości poprzez dopasowanie słów kluczowych, dopasowanie słowników, ocenę wyrażeń regularnych i innej zawartości toodetect badanie zawartości, która narusza zasady organizacyjne DLP. Na przykład DLP może zapobiec utracie hello hello następujące typy danych: 

* Ubezpieczenia społecznego i numery identyfikacyjne national 
* Informacje dotyczące bankowości 
* Numer karty kredytowej  
* Adresy IP 

Niektóre technologie DLP udostępniają hello możliwości toooverride hello DLP konfigurację (na przykład, jeśli organizacja musi tootransmit numer ubezpieczenia społecznego informacji tooa Lista płac procesora). Ponadto jest możliwe tooconfigure DLP tak, aby użytkownicy są powiadamiani, przed próbą nawet toosend poufne informacje, które nie powinny być przekazywane. 

> [!TIP]
> można użyć dokumentów pakietu Office 365 DLP tooprotect możliwości. Odczyt [kontrole zgodności usługi Office 365: zapobieganie utracie danych](https://blogs.office.com/2013/10/28/office-365-compliance-controls-data-loss-prevention/) Aby uzyskać więcej informacji.
> 
> 

## <a name="see-also"></a>Zobacz też
* [Najlepsze rozwiązania szyfrowania danych Azure](azure-security-data-encryption-best-practices.md)
* [Azure Zarządzanie tożsamościami i dostępem kontrolować najlepszych rozwiązań dotyczących zabezpieczeń](azure-security-identity-management-best-practices.md)
* [Blog zespołu ds. zabezpieczeń platformy Azure](http://blogs.msdn.com/b/azuresecurity/)
* [Centrum zabezpieczeń firmy Microsoft](https://technet.microsoft.com/library/dn440717.aspx)

