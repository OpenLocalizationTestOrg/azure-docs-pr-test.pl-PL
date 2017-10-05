---
title: Klasyfikacja danych na platformie Azure | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera wprowadzenie do podstawowe informacje dotyczące klasyfikacji danych i zaznacza jego wartość, w szczególności w kontekście chmury obliczeniowych oraz przy użyciu programu Microsoft Azure"
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
ms.openlocfilehash: e5d8841c47f91b27131fcf5066bfd3805b5670f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="data-classification-for-azure"></a>Klasyfikacja danych na platformie Azure
Ten artykuł zawiera wprowadzenie do podstawowe informacje dotyczące klasyfikacji danych i zaznacza jego wartość, w szczególności w kontekście chmury obliczeniowych oraz przy użyciu programu Microsoft Azure. 

## <a name="data-classification-fundamentals"></a>Podstawowe informacje dotyczące klasyfikacji danych
Klasyfikacja danych powiodło się w organizacji wymaga szerokiego świadomości potrzeb organizacji i dokładne zrozumienie, w którym znajdują się zasobów danych.  

Istnieją dane w jednym z trzech stanów podstawowe: 

* Magazynowane 
* W procesie 
* W drodze 

Wszystkie trzy stany wymagają unikatowych rozwiązań technicznych do klasyfikacji danych, ale zastosowanych zasad klasyfikacji danych powinna być taka sama dla każdego. Dane, które jest sklasyfikowany jako poufny musi pozostać poufne, gdy komputer znajduje się w stanie spoczynku, w procesie i podczas przesyłania. 

Dane można także strukturalnych lub bez struktury. Procesy typowe klasyfikacji danych strukturalnych w baz danych i arkuszy kalkulacyjnych są mniej złożony i czasochłonny do zarządzania niż danych niestrukturalnych, takich jak dokumenty, kod źródłowy i poczty e-mail. 

> [!TIP]
> Aby uzyskać więcej informacji na temat funkcji platformy Azure i najlepsze rozwiązania dotyczące szyfrowania danych przeczytaj [najlepsze rozwiązania szyfrowania danych Azure](azure-security-data-encryption-best-practices.md)
> 
> 

Ogólnie rzecz biorąc, organizacje będą mieć więcej danych niestrukturalnych niż dane strukturalne. Niezależnie od tego, czy danych strukturalnych lub bez struktury ważne jest zarządzanie wrażliwości danych. W przypadku prawidłowego wdrożenia pomaga klasyfikacji danych, upewnij się, że poufne dane, które zasoby są zarządzane za pomocą nadzoru większa niż zasobów danych, które są uważane za publiczne lub wolnego do dystrybucji. 

### <a name="controlling-access-to-data"></a>Kontrolowanie dostępu do danych
Uwierzytelnianie i autoryzacja są często pomylić ze sobą i ich role błędnie interpretowane. W rzeczywistości są zupełnie różne, jak pokazano na poniższej ilustracji.  

![Dostęp do danych i kontrola](./media/azure-security-data-classification/azure-security-data-classification-fig1.png)

### <a name="authentication"></a>Authentication
Uwierzytelnianie zazwyczaj składa się z co najmniej dwie części: nazwa użytkownika lub Identyfikatora użytkownika do identyfikacji użytkownika i token, takich jak hasło, aby upewnić się, że poświadczenie nazwy użytkownika jest prawidłowy. Proces nie zapewnia uwierzytelniony użytkownik z dostępem do dowolnego towarów lub usług. sprawdza, czy użytkownik jest kto mówią, że są one.   

> [!TIP]
> [Usługa Azure Active Directory](../active-directory/active-directory-whatis.md) zapewnia usługi tożsamości opartej na chmurze, które umożliwiają uwierzytelniania i autoryzacji użytkowników. 
> 
> 

### <a name="authorization"></a>Autoryzacja
Autoryzacja jest to proces udostępniania uwierzytelnionego użytkownika umożliwia dostęp do aplikacji, zestaw danych, pliku danych lub innego obiektu. Przypisywanie użytkowników uwierzytelnionych prawa do używania, modyfikowanie lub usuwanie elementów, które mogą uzyskiwać dostęp do wymaga uwagi do klasyfikacji danych. 

Implementacja mechanizmu sprawdzania poprawności potrzeb poszczególnym użytkownikom dostęp do plików i informacji oparty na kombinacji roli, zasady zabezpieczeń i zasad ryzyka zagadnienia wymaga pomyślnej autoryzacji. Na przykład dane z określonych aplikacji (LOB)-biznesowych nie może być konieczne dostęp do wszystkich pracowników, a tylko mały podzbiór pracowników prawdopodobnie będzie potrzebny dostęp do plików zasobów ludzkich (HR). Ale organizacjom kontroli kto ma dostęp do danych, jak również jako warunkami i sposobami, efektywną systemu do uwierzytelniania użytkowników należy spełnić. 

> [!TIP]
> w systemie Microsoft Azure upewnij się, że wykorzystanie based kontroli dostępu (RBAC) można udzielić tylko takiego dostępu, użytkownicy muszą wykonać swoje zadania. Odczyt [zarządzanie dostępem do zasobów usługi Azure Active Directory za pomocą przypisań ról](../active-directory/role-based-access-control-configure.md) Aby uzyskać więcej informacji. 
> 
> 

### <a name="roles-and-responsibilities-in-cloud-computing"></a>Role i obowiązki w chmury obliczeniowej
Mimo że dostawców w chmurze może ułatwić zarządzanie ryzykiem, klienci muszą upewnij się, że zarządzanie klasyfikacją danych i wymuszania jest poprawnie zaimplementowana aby zapewnić odpowiedni poziom usług zarządzania danych.  

Obowiązki klasyfikacji danych różni się zależnie od modelem usługi chmury, które jest już na miejscu, jak pokazano na poniższej ilustracji. Trzy modele usług chmury podstawowej są infrastruktura jako usługa (IaaS), platformy jako usługa (PaaS), a oprogramowanie jako usługa (SaaS). Implementacja mechanizmów klasyfikacji danych również różni się zależnie od zależność od oraz oczekiwań dostawcy chmury. 

![Role](./media/azure-security-data-classification/azure-security-data-classification-fig2.png)

Chociaż jest odpowiedzialny za klasyfikowania danych, dostawców w chmurze powinny być napisane zobowiązań dotyczących sposobu będzie bezpieczny i zadbać o zachowanie poufności danych klienta przechowywanych w chmurze.  

* **Dostawcy IaaS** wymagania są ograniczone do zapewnienia, że środowisko wirtualne mogą obsługiwać funkcje klasyfikacji danych i wymagań dotyczących zgodności klienta. Dostawcy IaaS ma mniejszy roli w klasyfikacji danych, ponieważ tylko wymagają upewnić się, że dane klienta adresów wymagań dotyczących zgodności. Jednak dostawców musi nadal upewnij się, że ich środowisk wirtualnych adresów wymagania dotyczące klasyfikacji danych oprócz zabezpieczanie centrów danych.
* **Dostawców PaaS** obowiązki mogą być mieszane, ponieważ platforma mogą być używane w warstwowego podejścia do zapewnienia bezpieczeństwa dla narzędzia klasyfikacji. PaaS dostawcy mogą być odpowiedzialne za uwierzytelnianie i prawdopodobnie niektórych reguł autoryzacji i podać zabezpieczeń oraz funkcje klasyfikacji danych do ich warstwy aplikacji. Znacznie jak dostawcy IaaS dostawcy PaaS konieczne upewnij się, że jego platforma jest zgodna z żadnych wymagań dotyczących klasyfikacji odpowiednie dane.
* **Dostawców w modelu SaaS** często są traktowane jako część łańcucha autoryzacji i trzeba będzie upewnij się, że danych przechowywanych w aplikacji SaaS mogą być kontrolowane przez typ klasyfikacji. Aplikacji SaaS można aplikacji biznesowych, a ich potrzeb charakter służyć do uwierzytelniania i autoryzacji dane, które są używane i przechowywane. 

## <a name="classification-process"></a>Proces klasyfikacji
Organizacje, które zrozumieć potrzeby klasyfikacji danych i chcesz ją wdrożyć stają przed podstawowe żądanie: czego zacząć?

Skuteczne i proste sposobem zaimplementować klasyfikacji danych jest używania wyboru planu wykonania, działania modelu z [MOF](https://technet.microsoft.com/solutionaccelerators/dd320379.aspx). Poniższa ilustracja wykresy zadań, które są wymagane, aby pomyślnie wdrożyć klasyfikacji danych, w tym modelu.  

1. **PLANOWANIE**. Zidentyfikuj niejawnego danych, aby wdrożyć program klasyfikacji i utworzyć profile ochrony zasobów danych. 
2. **CZY**. Po uzgodnionych zasad klasyfikacji danych wdrożyć program i implementować technologie wymuszania, zgodnie z potrzebami dla poufnych danych.  
3. **SPRAWDŹ**. Sprawdź i zweryfikować raporty, aby upewnić się, że narzędzia i metody używane są skutecznie adresowania zasady klasyfikacji. 
4. **DZIAŁANIE**. Sprawdź stan dostępu do danych i przejrzyj pliki i dane, które wymagają zmiany przy użyciu metodologii podziału i poprawką przyjęcie zmiany oraz do adresu nowych zagrożeń.  

![Planowanie,, sprawdź, działania](./media/azure-security-data-classification/azure-security-data-classification-fig3.png)

### <a name="select-a-terminology-model-that-addresses-your-needs"></a>Wybierz model terminologii, którego dotyczy potrzeb
Istnieje kilka typów procesów klasyfikacji danych, w tym procesów ręcznych, oparte na lokalizacji procesom klasyfikacji danych na podstawie lokalizacji użytkownika lub komputera, na podstawie aplikacji procesy, takie jak Klasyfikacja specyficzny dla bazy danych i automatyczne procesy używane przez różne technologie, niektóre z nich są opisane w sekcji "Zabezpieczania poufnych danych" w dalszej części tego artykułu.  

W tym artykule przedstawiono dwa modele uogólniony terminologii oparte na powszechnie używane i wzięty pod uwagę branży modeli. Te modele terminologii, które zapewnia trzy poziomy czułości klasyfikacji, przedstawiono w poniższej tabeli.  

> [!NOTE]
> Podczas klasyfikowania plik lub zasób, który łączy dane, które zwykle może być klasyfikowane na różnych poziomach, najwyższy poziom klasyfikacji obecny należy określić ogólną klasyfikacji. Na przykład plik zawierający dane poufne i ograniczeniami powinny być klasyfikowane jako ograniczone.  
> 
> 

| **Czułość** | **Terminologia modelu 1** | **Terminologia modelu 2** |
| --- | --- | --- |
| Wysoka |Poufne |Ograniczone |
| Medium |Tylko do użytku wewnętrznego |Wielkość liter |
| Niska |Publiczne |Bez ograniczeń |

#### <a name="confidential-restricted"></a>Poufne (ograniczony)
Informacje, które zostanie sklasyfikowany jako poufny lub zastrzeżony zawiera dane, które może być krytycznego do osób lub organizacji, jeśli utracone lub mają naruszone zabezpieczenia. Takie informacje często znajduje się na zasadzie "trzeba znać" i mogą być następujące: 

* Dane osobowe, w tym dane osobowe Social Security lub numery identyfikacyjne national, numery passport, numery kart kredytowych, sterownika numerów licencji, medyczne rekordów i numery identyfikatorów zasad ubezpieczenia zdrowotnego.  
* Dokumentów finansowych, w tym finansowych lub numery kont takich jak sprawdzanie inwestycji konta. 
* Materiał biznesowych, takich jak dokumenty lub dane, które jest określonych własności intelektualnej.  
* Dane prawnych, w tym potencjalnych materiałów prawnikiem uprawnieniach. 
* Dane uwierzytelniania, w tym klucze prywatne kryptografii, pary hasło nazwy użytkownika lub innych sekwencji identyfikacji, takie jak biometryczne plików kluczy prywatnych. 

Dane, które jest sklasyfikowany jako poufny często ma przepisami i wymagań dotyczących zgodności dla obsługi danych. 

#### <a name="for-internal-use-only-sensitive"></a>Do użytku wewnętrznego tylko (liter)
Informacje, które jest klasyfikowany jako średnia czułości zawiera pliki i dane, które nie miałoby poważny wpływ na poszczególne i/lub organizacji, w przypadku utraty lub zniszczenia. Takie informacje mogą być następujące: 

* Wiadomości e-mail, z których większość można usunąć lub rozproszonych bez powodowania kryzysu (bez skrzynek pocztowych lub adres e-mail osoby, które są identyfikowane w klasyfikacji poufne).  
* Dokumenty i pliki, które nie zawierają dane poufne.

Ogólnie rzecz biorąc ta klasyfikacja obejmuje wszystkie elementy, które nie są poufne. Ta klasyfikacja może zawierać większości danych biznesowych, ponieważ większość plików, które są zarządzane lub są używane bieżące mogą być klasyfikowane jako poufne. Z wyjątkiem danych jest upubliczniona lub poufne wszystkie dane w obrębie organizacji firm mogą być klasyfikowane jako poufne domyślnie. 

#### <a name="public-unrestricted"></a>Public (bez ograniczeń)
Informacje, które jest klasyfikowany jako publiczną, zawiera dane i pliki, które nie są krytyczne dla operacji lub potrzeb biznesowych. Ta klasyfikacja może również zawierać dane, które celowo został zwolniony publicznego ich wykorzystania, takich jak materiały marketingowe lub naciśnij klawisz anonsów. Ponadto ta klasyfikacja może zawierać dane, takie jak wiadomości-śmieci e-mail przechowywane przez usługę poczty e-mail. 

### <a name="define-data-ownership"></a>Zdefiniuj własność danych
Należy ustanowić wyczyść custodial łańcucha własności dla wszystkich zasobów danych. Poniższa tabela zawiera dane różnych własność ról w zakresie klasyfikacji danych i ich odpowiednich praw.  

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

**Właściciel zasobu danych** jest oryginalne twórca danych, który można delegować prawa własności i przypisać nadzorcą jest. Po utworzeniu pliku właściciel powinno być możliwe do przypisywania klasyfikacji, co oznacza, że mają one odpowiedzialność, aby zrozumieć, co powinna być sklasyfikowany jako poufny na podstawie zasad organizacji. Wszystkie dane właściciela zasobów danych mogą być klasyfikowane automatycznie podobnie jak w przypadku tylko użytku wewnętrznego (wielkość liter), chyba że są one odpowiedzialne za będący właścicielem lub tworzenie typów danych poufnych (ograniczony). Często właściciela roli ulegnie zmianie po klasyfikowania danych. Na przykład właściciel może utworzyć bazę danych informacji niejawnych i zrzeka się praw do niejawnego danych.  

> [!NOTE]
> Właściciele zawartości danych często używają usług, urządzeń i nośników, niektóre z nich osobiste i niektóre z nich należy do organizacji. Zasady wyczyść organizacji pozwala zagwarantować, że użycie urządzeń przenośnych i urządzeń inteligentnych jest zgodnie z wytycznymi klasyfikacji danych.  
> 
> 

**Niejawnego zasobów danych** jest przypisywany przez właściciela zasobów (lub ich delegata) do zarządzania zasobów zgodnie z umowy z właściciel zasobu lub zgodnie z wymaganiami odpowiednich zasad. W idealnym przypadku roli niejawnego można zaimplementować w systemie automatycznych. Niejawnego zasobów gwarantuje, że kontroli dostępu konieczne jest dostępny i jest odpowiedzialny za zarządzanie i ochrony zasobów, aby ich szczególną uwagę. Obowiązki niejawnego zasobów mogą obejmować:  

* Ochrona zasobów zgodnie z kierunku właściciel zasobu lub porozumieniu właściciel zasobu 
* Zapewnienie, że spełnione są zasady klasyfikacji 
* Informuje o dostępności właścicieli zasobów o wszelkich zmianach w ustalonym formantów i/lub procedur ochrony przed tych wprowadzonych zmian 
* Raportowanie do właściciela zasobów o zmiany lub usuwania obowiązki niejawnego zasobów 
* **Administratora** reprezentuje użytkownika, który jest odpowiedzialny za zapewnienie, że integralność została zachowana, ale nie są właściciela zasobów danych, niejawnego lub użytkownika. W rzeczywistości wiele ról administratora dostępne usługi zarządzania kontenera danych bez uzyskiwania dostępu do danych. Rola administratora obejmuje kopii zapasowej i przywracanie danych, Obsługa rekordów zasobów i wybieranie, pobieranie i obsługę urządzenia i magazynu domu zasoby. 
* Użytkownik zasobów zawiera każdego, kto uzyskuje dostęp do danych lub pliku. Przypisywanie dostępu jest często delegowane przez właściciela do niejawnego zasobów.  

### <a name="implementation"></a>Wdrażanie
Zagadnienia dotyczące zarządzania dotyczą wszystkich metod klasyfikacji. Te zagadnienia konieczne zawierają szczegółowe informacje o tym, kto, co, gdzie, kiedy i dlaczego zasobu danych będzie można używany, dostęp do, zmienić lub usunąć. Wszystkie zarządzanie zasobami musi odbywać się zrozumieniu jak organizacji widoków jego ryzyka, ale proste metodologii mogą być stosowane zgodnie z definicją w procesie klasyfikacji danych. Dodatkowe zagadnienia dotyczące klasyfikacji danych obejmują wprowadzenie nowych aplikacji oraz narzędzia i zarządzanie zmianami po metodzie klasyfikacji.  

### <a name="reclassification"></a>Podziału
Przeklasyfikowania lub zmiana klasyfikacji stanu trwałego danych należy wykonać, gdy użytkownik lub system Określa zmienił profilu znaczenie lub powoduje ryzyko zasobów danych. Tej pracy jest ważne w celu zapewnienia, że stan klasyfikacji jest nadal aktualne i prawidłowe. Większość zawartości, która nie jest sklasyfikowany ręcznie można automatycznie klasyfikowane lub na podstawie użycia niejawnego danych lub właściciela danych. 

### <a name="manual-data-reclassification"></a>Podział danych ręczne
Najlepiej tej pracy będzie upewnij się, aby uzyskać szczegółowe informacje o zmianie przechwycenie i inspekcji. Najbardziej prawdopodobnym powodem dla ręcznego podziału jest powody czułości lub przechowywane w formacie papieru lub wymaganie, aby przejrzeć dane, które pierwotnie został nieprawidłowo klasyfikowana rekordów. Ponieważ w tym dokumencie uwzględnia klasyfikacji danych i przenoszenie danych do chmury, działania ręcznego podziału wymagają uwagi na podstawie przypadku i przeglądu zarządzania ryzykiem będzie idealne do wymagań dotyczących klasyfikacji adres. Ogólnie rzecz biorąc, nakładu pracy będzie należy wziąć pod uwagę zasad organizacji dotyczących co musi być klasyfikowane, domyślnym stanem klasyfikacji (wszystkie dane i jest wielkość liter, ale nie do poufnych plików) i podejmij wyjątki dla danych o wysokim ryzyku. 

### <a name="automatic-data-reclassification"></a>Podział danych
Podział danych używa tej samej zasady jako ręczna klasyfikacja. Wyjątkiem jest to, że automatycznego rozwiązania można zapewnić, a następnie i stosowane zgodnie z potrzebami reguły. Klasyfikacja danych może odbywać się w ramach zasady wymuszania klasyfikacji danych, które można wymusić, gdy dane są przechowywane w użyciu i podczas przesyłania przy użyciu technologii autoryzacji.

* Na podstawie aplikacji. Przy użyciu określonych aplikacji domyślnie ustawia poziomu klasyfikacji. Na przykład dane z oprogramowanie (CRM) zarządzania relacjami z klientami, HR i narzędzia zarządzania rekordami kondycji jest poufne domyślnie. 
* Na podstawie lokalizacji. Lokalizacja danych może ułatwić identyfikację wrażliwości danych. Na przykład dane przechowywane przez HR lub działu finansowego jest bardziej prawdopodobną charakteru poufnego.  

### <a name="data-retention-recovery-and-disposal"></a>Przechowywanie danych, odzyskiwania i usuwania
Odzyskiwanie danych i usuwania, takie jak podział danych jest ważnym aspektem zarządzania zasobów danych. Zasady odzyskiwania danych i usuwania czy określone przez zasady przechowywania danych i wymuszane w taki sam sposób jak podziału danych; nakładu pracy może być wykonane przez role niejawnego i administratora jako wspólne zadania.  

Brak zasad przechowywania danych może oznaczać utrata danych lub niedopełnienie wymagania prawne i prawnych. Większość organizacji, które nie mają zasady przechowywania danych jasno określone zazwyczaj są używane domyślne zasady przechowywania "Zachowaj wszystko". Jednak zasady przechowywania ma dodatkowe zagrożenia w scenariuszach usługi w chmurze. 

Na przykład zasady przechowywania danych dla dostawcy usług w chmurze jest uznawana za podobnie jak w przypadku "czas trwania subskrypcji" (tak długo, jak usługa ma być stosowany do przechowywania danych). Umowę płatności do przechowywania nie może kierować zasady firmowe i przepisami przechowywania. Definiowanie zasad dotyczących poufnych danych można upewnij się, że dane są przechowywane i usunięte w oparciu o najlepsze rozwiązania. Ponadto można tworzyć zasady archiwizacji do formalnego zrozumienia, jakie dane powinny zostać usunięte z i kiedy. 

Zasady przechowywania danych należy spełnić wymaganych przepisami i wymagania dotyczące zgodności, a także wymagania dotyczące przechowywania prawne firmy. Niejawne danych może powodować pytania dotyczące czas przechowywania i wyjątków dla danych, które były przechowywane u dostawcy; takie pytania są bardziej prawdopodobne w przypadku danych, który nie został poprawnie sklasyfikowany. 

> [!TIP]
> więcej informacji na temat zasad przechowywania danych platformy Azure i inne odczytując [umowę subskrypcji Online firmy Microsoft](https://azure.microsoft.com/support/legal/subscription-agreement/)
> 
> 

## <a name="protecting-confidential-data"></a>Ochrona poufnych danych.
Po sklasyfikowaniu danych Znajdowanie i wdrażanie sposoby ochrony danych poufnych staje się integralną częścią każdej strategii wdrażania ochrony danych. Ochrona poufnych danych wymaga dodatkowych uwagę na sposób przechowywania danych i przekazywane w konwencjonalnej architektury, jak również w chmurze. 

Ta sekcja zawiera podstawowe informacje dotyczące niektórych technologii, których można zautomatyzować wymuszania starań, aby chronić dane, które zostało sklasyfikowane jako poufne. 

Jak pokazano na poniższej ilustracji, można wdrożyć tych technologii jako lokalnymi lub rozwiązań w chmurze — lub w sposób hybrydowe z niektórych ich wdrożonych lokalnie, a niektóre w chmurze. (Niektóre technologii, takich jak szyfrowania i zarządzania prawami rozszerzać urządzeniach użytkownika.)  

![Technologie](./media/azure-security-data-classification/azure-security-data-classification-fig4.png)

### <a name="rights-management-software"></a>Oprogramowanie do zarządzania prawami
Jedno rozwiązanie w celu zapobieżenia utracie danych jest oprogramowanie do zarządzania prawami. W przeciwieństwie do metod, które próbują przerwać przepływu informacji w punkcie wyjścia w organizacji oprogramowanie do zarządzania prawami działa na poziomach głębokości w ramach technologii magazynowania danych. Dokumenty są szyfrowane i kontrolować, kto ich odszyfrować używa kontroli dostępu, które są zdefiniowane w rozwiązania kontrolki uwierzytelniania, takie jak usługi katalogowej.  

> [!TIP]
> usługi Azure Rights Management (Azure RMS) można użyć jako rozwiązanie do ochrony informacji do ochrony danych w różnych scenariuszach. Odczyt [co to jest usługa Azure Rights Management?](https://docs.microsoft.com/rights-management/understand-explore/what-is-azure-rms) Aby uzyskać więcej informacji o tym rozwiązaniu platformy Azure.
> 
> 

Oto niektóre zalety oprogramowania do zarządzania prawami: 

* Chronionym poufne informacje. Użytkownicy mogą chronić swoje dane bezpośrednio przy użyciu aplikacji z obsługą zarządzania prawami. Nie są wymagane żadne dodatkowe czynności — tworzenie dokumentów, wysyłania wiadomości e-mail oraz publikowania danych oferują środowisko ochrony spójności danych. 
* Ochrona porusza się z danymi. Klienci zachowuje kontrolę nad kto ma dostęp do swoich danych w chmurze, istniejącej infrastruktury IT, lub na pulpicie użytkownika. Organizacje mogą wybrać szyfrować dane i ograniczenie dostępu zgodnie z ich wymaganiami biznesowymi. 
* Domyślne zasady ochrony informacji. Administratorzy i użytkownicy mogą używać zasad standardowe przypadku wielu typowych scenariuszy biznesowych, takich jak "Firmy poufne — tylko do odczytu" i "Nie przekazuj." Bogaty zestaw użycia prawa są obsługiwane, takich jak odczytu, kopiowania, drukowania, zapisywania, edytowania i do przodu, aby umożliwić elastyczność podczas definiowania niestandardowe prawa użytkowania. 

> [!TIP]
> chronić dane w usłudze Azure Storage za pomocą [szyfrowanie usługi Magazyn Azure](../storage/storage-service-encryption.md) dla przechowywanych danych. Można również użyć [szyfrowania dysków Azure](azure-security-disk-encryption.md) w celu ochrony danych znajdujących się na dyski wirtualne użyte maszyn wirtualnych platformy Azure.
> 
> 

### <a name="encryption-gateways"></a>Bramy szyfrowania
Bramy szyfrowania działają w ich własnych warstwy do świadczenia usług szyfrowania przez przekierowanie dostęp do danych opartych na chmurze. Ta metoda nie należy mylić z tym wirtualnej sieci prywatnej (VPN). Celem bramy szyfrowania jest przezroczyste warstwy do rozwiązań w chmurze.   

Bramy szyfrowania zapewniają sposób zarządzania i zabezpieczonych danych, które zostało sklasyfikowane jako poufne przez szyfrowanie danych podczas przesyłania, a także dane przechowywane.  

Bramy szyfrowania są umieszczane w przepływ danych między urządzeniami użytkownika i danych aplikacji Centrum w celu świadczenia usług szyfrowania i odszyfrowywania. Tych rozwiązań, takich jak sieci VPN, znajdują się głównie rozwiązań lokalnych. Są one przeznaczone do zapewnić kontrolę nad kluczami szyfrowania, który pomaga zmniejszyć ryzyko wprowadzania danych i klucz Zarządzanie za pomocą jednego dostawcę innych firm. Takich rozwiązań są zaprojektowane, podobnie jak szyfrowanie, aby zapewnić bezproblemowe działanie i w przezroczysty sposób między użytkownikami i usługi. 

> [!TIP]
> Usługa Azure ExpressRoute umożliwia rozszerzanie sieci lokalnej w chmurze firmy Microsoft za pośrednictwem dedykowanego połączenia prywatne. Odczyt [opis techniczny ExpressRoute](../expressroute/expressroute-introduction.md) uzyskać więcej informacji dotyczących tej funkcji. Opcje dla innego między lokalnym łączność między siecią lokalną i [Azure to VPN lokacja lokacja](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).
> 
> 

### <a name="data-loss-prevention"></a>Zapobieganie utracie danych
Ważną kwestią jest utrata danych (nazywane czasami wycieku danych) i zapobiegania utracie danych zewnętrznych za pomocą wewnętrznych złośliwe i przypadkowe jest podstawowym w przypadku wielu organizacji.  

Technologie zapobiegania (DLP) utraty danych pozwala zagwarantować rozwiązania, takie jak usługi poczty e-mail nie wysyłaj danych, które zostało sklasyfikowane jako poufne. Organizacje mogą korzystać z funkcji DLP w istniejących produktów w celu zapobieżenia utracie danych. Takie funkcje za pomocą zasad, które można łatwo utworzyć od podstaw lub za pomocą szablonu dostarczana przez dostawcę oprogramowania.  

Technologie DLP może wykonywać szczegółowa analiza zawartości poprzez dopasowanie słów kluczowych, dopasowanie słowników, ocenę wyrażeń regularnych i ocena innej zawartości, aby wykryć zawartość, która narusza zasady DLP organizacyjne. Na przykład DLP może zapobiec utracie następujące typy danych: 

* Ubezpieczenia społecznego i numery identyfikacyjne national 
* Informacje dotyczące bankowości 
* Numer karty kredytowej  
* Adresy IP 

Niektóre technologie DLP zapewniają również możliwość zastępowania konfiguracji DLP (na przykład, jeśli organizacja musi się do przesyłania informacji numer ubezpieczenia społecznego procesor Lista płac). Ponadto istnieje możliwość skonfiguruj DLP, dzięki czemu użytkownicy będą powiadamiani, zanim one nawet próbę wysłania poufne informacje, które nie powinny być przekazywane. 

> [!TIP]
> Aby chronić dokumenty skorzystać z możliwości Office 365 DLP. Odczyt [kontrole zgodności usługi Office 365: zapobieganie utracie danych](https://blogs.office.com/2013/10/28/office-365-compliance-controls-data-loss-prevention/) Aby uzyskać więcej informacji.
> 
> 

## <a name="see-also"></a>Zobacz też
* [Najlepsze rozwiązania szyfrowania danych Azure](azure-security-data-encryption-best-practices.md)
* [Azure Zarządzanie tożsamościami i dostępem kontrolować najlepszych rozwiązań dotyczących zabezpieczeń](azure-security-identity-management-best-practices.md)
* [Blog zespołu ds. zabezpieczeń platformy Azure](http://blogs.msdn.com/b/azuresecurity/)
* [Centrum zabezpieczeń firmy Microsoft](https://technet.microsoft.com/library/dn440717.aspx)

