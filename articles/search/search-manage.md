---
title: "Administrowanie aaaService dla usługi Azure Search w portalu Azure hello"
description: "Zarządzaj usługi Azure Search, Usługa wyszukiwania w hostowanej chmurze w systemie Microsoft Azure, przy użyciu hello portalu Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: c87d1fdd-b3b8-4702-a753-6d7e29dbe0a2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/18/2017
ms.author: heidist
ms.openlocfilehash: 9bb33660d93e068e0f35b856cba0a41c92623644
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-administration-for-azure-search-in-hello-azure-portal"></a>Administrowanie usługi dla usługi Azure Search w portalu Azure hello
> [!div class="op_single_selector"]
> * [Portal](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> * [Zestaw SDK platformy .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.search)
> * [Python](https://pypi.python.org/pypi/azure-mgmt-search/0.1.0)> 

Usługa wyszukiwanie Azure to usługa wyszukiwania w pełni zarządzana, oparte na chmurze używaną do tworzenia zaawansowanych wyszukiwanie w aplikacje niestandardowe. W tym artykule omówiono hello *usługi administracyjnej* zadań, które można wykonywać w hello [portalu Azure](https://portal.azure.com) usługi wyszukiwania, która została już przydzielona. *Usługi administracyjnej* jest lekki zgodnie z projektem, ograniczone toohello następujące zadania:

* Zarządzanie i zabezpieczanie dostępu toohello *klucze interfejsu api* używane przez usługę tooyour odczytu lub zapisu.
* Dostosuj wydajność usługi, zmieniając alokacji hello partycji i replik.
* Monitorowanie użycia zasobów, limitów względną toomaximum warstwę usług.

**Nie znajduje się w zakresie** 

*Zarządzanie zawartością* (lub indeksu zarządzania) odwołuje się toooperations takich jak analizowanie woluminu zapytania toounderstand ruchu wyszukiwania, odnajdywanie osób którego warunki wyszukiwania, a wyszukiwania jak pomyślne wyniki w przeprowadzi toospecific klientów dokumenty w indeksie. Aby uzyskać pomoc w tym obszarze, [analizy ruchu wyszukiwania dla usługi wyszukiwanie Azure](search-traffic-analytics.md).

*Wydajność zapytania* również wykracza poza zakres tego artykułu hello. Aby uzyskać więcej informacji, zobacz [monitorowanie metryk użycia i zapytania](search-monitor-usage.md) i [wydajności i optymalizacji](search-performance-optimization.md).

*Uaktualnij* nie jest zadania administracyjnego. Przenoszenie tooa inną warstwą, ponieważ zasoby są przydzielane po zainicjowaniu obsługi usługi hello, wymaga nowej usługi. Aby uzyskać więcej informacji, zobacz [Tworzenie usługi Azure Search](search-create-service-portal.md).

<a id="admin-rights"></a>

## <a name="administrator-rights"></a>Prawa administratora
Inicjowanie obsługi administracyjnej lub likwidowanie sama usługa hello jest możliwe przez administratora subskrypcji platformy Azure lub współadministratorem.

W ramach usługi każda osoba mająca dostęp toohello — adres URL usługi i klucz interfejsu api administratora ma dostęp do odczytu zapisu toohello usługi. Tooadd możliwości hello zapewnia dostęp do odczytu i zapisu, usuwanie lub modyfikowanie obiektów serwera, w tym klucze interfejsu api, indeksów, indeksatorów, źródła danych, harmonogramów i przypisania ról, ponieważ implementowane za pośrednictwem [zdefiniowane RBAC ról](#rbac).

Cała interakcja użytkownika z usługi Azure Search znajduje się w jeden z następujących trybów: Odczyt i zapis usługi toohello dostęp (prawa administratora) lub usługi toohello dostęp tylko do odczytu (zapytanie praw). Aby uzyskać więcej informacji, zobacz [Zarządzanie klucze interfejsu api hello](#manage-keys).

<a id="sys-info"></a>

## <a name="set-rbac-roles-for-administrative-access"></a>Ustaw role RBAC dla dostępu administracyjnego
Platforma Azure udostępnia [modelu autoryzacji opartej na rolach globalne](../active-directory/role-based-access-control-configure.md) dla wszystkich usług zarządzanych za pomocą portalu hello lub interfejsów API Menedżera zasobów. Role właściciela, współautora i czytnika określają poziom hello administracji usługi dla użytkowników usługi Active Directory, grup i roli tooeach przypisanych podmiotów zabezpieczeń. 

Dla usługi Azure Search uprawnienia RBAC określają hello następujące zadania administracyjne:

| Rola | Zadanie |
| --- | --- |
| Właściciel |Utwórz lub Usuń usługi hello lub dowolnego obiektu w usłudze hello, w tym klucze interfejsu api, indeksów, indeksatorów, indeksatora źródeł danych i harmonogramy indeksatora.<p>Wyświetl stan usługi, w tym liczby i rozmiaru magazynu.<p>Dodawanie lub usuwanie członkostwo roli (tylko właściciel może zarządzać członkostwem w roli).<p>Administratorzy subskrypcji i właścicieli usług mają automatyczne członkostwa w roli właścicieli hello. |
| Współautor |Sam poziom dostępu właściciel minus RBAC zarządzania rolami. Na przykład współautora można wyświetlić i ponownie wygenerować `api-key`, ale nie można zmodyfikować członkostwa w roli. |
| Czytelnik |Wyświetl klucze stanu i zapytania usługi. Członkowie tej roli nie można zmienić konfiguracji usługi i nie można wyświetlić kluczy administratora. |

Role nie przyznawaj końcowego usługi toohello praw dostępu. Wyszukiwania na nich operacji usługi, takie jak Zarządzanie indeksami, wypełniania indeksu i zapytań wyszukiwania danych, są kontrolowane przez klucze interfejsu api, nie ról. Aby uzyskać więcej informacji, zobacz "Autoryzacja zarządzania lub dane" w [co to jest kontrola dostępu oparta na rolach](../active-directory/role-based-access-control-what-is.md).

<a id="secure-keys"></a>
## <a name="logging-and-system-information"></a>Informacje o rejestracji i system
Usługa Azure Search nie ujawnia plików dziennika dla poszczególnych usług za pomocą portalu hello lub interfejsów programistycznych. W warstwie podstawowej hello lub nowszym Microsoft monitoruje wszystkie usługi Azure Search dostępności 99,9% na umów dotyczących poziomu usług (SLA). Jeśli usługa hello jest powolne, żądania przepływności spada poniżej progów SLA zespoły pomocy technicznej Przejrzyj toothem dostępne pliki dziennika hello i adres hello problem.

Pod względem ogólne informacje o usłudze można uzyskać informacji w hello następujące sposoby:

* W portalu hello na pulpicie nawigacyjnym usługi hello, za pomocą powiadomień, właściwości i komunikaty o stanie.
* Przy użyciu [PowerShell](search-manage-powershell.md) lub hello [interfejsu API REST zarządzania](https://docs.microsoft.com/rest/api/searchmanagement/) za[pobrać właściwości usługi](https://docs.microsoft.com/rest/api/searchmanagement/services), lub stan użycia zasobów indeksu.
* Za pomocą [analizy ruchu wyszukiwania](search-traffic-analytics.md), jak podano wcześniej.

<a id="manage-keys"></a>

## <a name="manage-api-keys"></a>Zarządzanie kluczami interfejsu api
Wszystkie żądania usługi wyszukiwania tooa muszą klucz interfejsu api wygenerowany specjalnie dla usługi. Ten klucz interfejsu api jest hello mechanizm wyłącznie w celu uwierzytelniania dostępu do punktu końcowego usługi wyszukiwania dla tooyour. 

Klucz interfejsu api to ciąg składający się z losowo generowany liter i cyfr. Za pomocą [uprawnienia RBAC](#rbac), możesz usunąć lub odczyt kluczy hello, ale nie można zastąpić klucz przy użyciu hasła użytkownika. 

Dwa typy klucze są używane tooaccess usługi wyszukiwania:

* Administrator (dotyczy żadnych operacji odczytu i zapisu w usłudze hello)
* Zapytania (nieprawidłowy dla operacji tylko do odczytu, takich jak zapytań względem indeksu)

Klucz interfejsu api administratora jest tworzona po zainicjowaniu obsługi usługi hello. Dostępne są dwa klucze administratora, wyznaczony jako *głównej* i *dodatkowej* tookeep je bezpośrednio, ale w rzeczywistości są wymienne. Każda usługa ma dwa klucze administratora, dzięki czemu można jedną przerzucane bez utraty dostępu do usługi tooyour. Można ponownie wygenerować klucza albo administratora, ale nie można dodać klucza liczby całkowitej admin toohello. Brak maksymalnie dwa klucze administratora dla usługi wyszukiwania.

Klucze zapytania są przeznaczone dla aplikacji klienckich, które bezpośrednio wywołać wyszukiwania. Możesz utworzyć zapasowej too50 zapytania kluczy. W kodzie aplikacji należy określić adres URL hello wyszukiwania i usługi toohello dostęp tylko do odczytu tooallow klucz api-key zapytania. Kod aplikacji określa również indeksu hello używanych przez aplikację. Razem hello punktu końcowego, klucz interfejsu api dla dostęp tylko do odczytu i indeksu docelowego zdefiniować poziom dostępu i zakres hello hello połączenia z aplikacji klienta.

tooget lub regenerate klucze api Key, hello Otwórz pulpit nawigacyjny usługi. Kliknij przycisk **KLUCZE** tooslide Otwórz stronę Zarządzanie kluczami hello. Polecenia ponownie wygenerować lub tworzenia kluczy są u góry hello hello strony. Domyślnie są tworzone tylko kluczy administratora. Klucze interfejsu api zapytania muszą być utworzone ręcznie.

 ![][9]

<a id="rbac"></a>

## <a name="secure-api-keys"></a>Klucze zabezpieczeń interfejsu api
Bezpieczeństwo kluczy jest zapewniana przez ograniczenie dostępu za pośrednictwem portalu hello lub interfejsy usługi Resource Manager (programu PowerShell lub interfejsu wiersza polecenia). Jak wspomniano, Administratorzy subskrypcji można wyświetlać i ponowne wygenerowanie wszystkich kluczy interfejsu api. Ze względów Przejrzyj toounderstand przypisania roli, kto ma dostęp do toohello admin kluczy.

1. Na pulpicie nawigacyjnym usługi hello kliknij przycisk blok użytkownicy hello Otwórz ikonę tooslide hello dostępu.
   ![][7]
2. Użytkownicy przejrzyj istniejące przypisania roli. Zgodnie z oczekiwaniami, Administratorzy subskrypcji już usługi toohello pełny dostęp za pośrednictwem hello właściciela roli.
3. Kliknij przycisk Dalej, toodrill **Administratorzy subskrypcji** , a następnie rozwiń węzeł toosee listy przypisania roli hello, który ma uprawnienia do administrowania wspólnej na usługi wyszukiwania.

Inny sposób tooview dostępu uprawnień jest tooclick **ról** na blok użytkownicy hello. W ten sposób Wyświetla dostępne role i hello liczby użytkowników lub grup tooeach przypisanej roli.

<a id="sub-5"></a>

## <a name="monitor-resource-usage"></a>Monitorowanie użycia zasobów
Na pulpicie nawigacyjnym hello monitorowania zasobów jest toohello ograniczone informacje wyświetlane na pulpicie nawigacyjnym usługi hello i kilka metryk, które można uzyskać przez zapytanie usługi hello. Na pulpicie nawigacyjnym usługi hello, w sekcji użycia hello może szybko określić, czy poziomy zasobów partycji są odpowiednie dla twojej aplikacji.

Witaj interfejsu API usługi wyszukiwania można uzyskać liczbę dokumentów oraz indeksów. Brak limitu skojarzone z tych liczników oparte na powitania warstwy cenowej. Aby uzyskać więcej informacji, zobacz [limity usługi wyszukiwania](search-limits-quotas-capacity.md). 

* [Uzyskać statystyki indeksu](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)
* [Liczba dokumentów](https://docs.microsoft.com/rest/api/searchservice/count-documents)

> [!NOTE]
> Buforowanie zachowania tymczasowo zawyżenie limit. Na przykład w przypadku używania usługi hello udostępnionych, można napotkać dokumentu liczba przekracza limit twardym powitania 10 000 dokumentów. zawyżania Hello jest tymczasowy i zostanie wykryty na powitania dalej sprawdzenia wymuszenia limitu. 
> 
> 

## <a name="disaster-recovery-and-service-outages"></a>Awarie awaryjnego odzyskiwania i usługi

Mimo że firma Microsoft może odzyskana danych, usługi Azure Search nie zapewnia błyskawiczne pracy awaryjnej usługi hello, w przypadku awarii na poziomie Centrum hello klastra lub danych. Jeśli klaster nie powiedzie się w centrum danych hello, zespół operacyjny hello wykryje i działają usługi toorestore. Podczas przywracania usługi wystąpi Przestój. Możesz poprosić o toocompensate środki na korzystanie z usługi w przypadku niedostępności usługi na powitania [Umowa dotycząca poziomu usług (SLA)](https://azure.microsoft.com/support/legal/sla/search/v1_0/). 

Jeśli usługa ciągłego jest wymagana w przypadku hello poważnej awarii poza kontrolą firmy Microsoft, można [obsługi administracyjnej dodatkowych usług](search-create-service-portal.md) w innym regionie i indeksów tooensure strategii wdrażania replikacja geograficzna są w pełni nadmiarowe we wszystkich usługach.

Klienci korzystający z [indeksatory](search-indexer-overview.md) toopopulate i Odśwież indeksów może obsłużyć odzyskiwania po awarii poprzez wykorzystanie hello indeksatory specyficzne dla magazynu geograficznie tego samego źródła danych. Dwie usługi w różnych regionach, systemem indeksatora, można indeksu z hello sam nadmiarowość geograficzna tooachieve źródła danych. Jeśli indeksujesz ze źródeł danych, które są również geograficznie nadmiarowego należy pamiętać, że usługi Azure Search indeksatory można wykonać tylko przyrostowe indeksowania z repliki podstawowej. W przypadku trybu failover należy się, że punkt toore hello indeksatora toohello nowej repliki podstawowej. 

Jeśli nie używasz indeksatorów, należy użyć aplikacji kod toopush obiekty i dane toodifferent wyszukiwania usług równolegle. Aby uzyskać więcej informacji, zobacz [wydajności i optymalizacji w usłudze Azure Search](search-performance-optimization.md).

## <a name="backup-and-restore"></a>Tworzenie kopii zapasowej i przywracanie

Ponieważ usługa Azure Search nie jest rozwiązanie magazynu danych podstawowych, nie udzielamy posiadanie mechanizmu samoobsługowego tworzenia kopii zapasowych i przywracania. Kod aplikacji używanych do tworzenia i wypełniania indeksu jest hello faktyczne opcja przywracania, jeśli przez pomyłkę usuwanie indeksu. 

toorebuild jako indeks, czy usunąć ją (zakładając, że istnieje), ponownie utwórz indeks hello w usłudze hello i załaduj ponownie przez pobranie danych z magazynu danych podstawowych. Alternatywnie możesz uzyskiwać dostęp za[techniczną]() toosalvage indeksy przypadku regionalnej awarii.


<a id="scale"></a>

## <a name="scale-up-or-down"></a>Skalowanie w górę lub w dół
Każda usługa wyszukiwania rozpoczyna się od co najmniej jedna replika i jedną partycję. Jeśli użytkownik utworzył konto na [warstwy, która zapewnia zasobów dedykowanych](search-limits-quotas-capacity.md), kliknij hello **skali** kafelka wykorzystania zasobów tooadjust hello usługi Pulpit nawigacyjny.

Po dodaniu pojemności za pośrednictwem albo zasób hello usługa używa je automatycznie. Nie są wymagane nie dalsze działania ze strony użytkownika, ale występuje niewielkie opóźnienie przed hello wpływ nowy zasób hello jest realizowana. Może zająć 15 minut lub więcej tooprovision dodatkowych zasobów.

 ![][10]

### <a name="add-replicas"></a>Dodawanie repliki
Zwiększenie zapytania na sekundę (QPS) lub osiągnięcia wysokiej dostępności polega na dodaniu repliki. Każdej repliki ma jedną kopię indeksu, więc Dodawanie jedna replika więcej tłumaczy tooone więcej indeks dostępne do obsługi żądań zapytań usługi. Co najmniej 3 repliki są wymagane w celu zapewnienia wysokiej dostępności (zobacz [planowania pojemności](search-capacity-planning.md) szczegółowe informacje).

Mając więcej repliki usługi wyszukiwania można równoważenia obciążenia zapytania żądań kierowanych przez większą liczbę indeksów. Biorąc pod uwagę na poziomie woluminu zapytania, przepływności zapytania będzie toobe szybciej w przypadku większej liczby kopii hello indeksu dostępne tooservice hello żądania. Jeśli występuje opóźnienie kwerendy, można oczekiwać pozytywny wpływ na wydajność, po hello dodatkowe repliki są w trybie online.

Przepływność zapytania rośnie w miarę dodawania replik, go nie dokładnie dwukrotnie lub potrójne podczas dodawania usługi tooyour repliki. Wszystkie aplikacje wyszukiwania są podmiotu tooexternal czynników, które można wpływają na wydajność kwerend. Złożonych kwerend i opóźnienie sieci są dwa składniki, które toovariations w czas odpowiedzi na zapytania.

### <a name="add-partitions"></a>Dodawanie partycji
Większość aplikacji usługi ma wbudowane potrzeba więcej repliki zamiast partycji. Dla tych przypadków, gdy wymagana jest liczba zwiększona dokumentu można dodać partycji, jeśli konta usługi — warstwa standardowa. Warstwa podstawowa nie zapewnia dodatkowych partycji.

W warstwie standardowa hello, partycje są dodawane w wielokrotności 12 (w szczególności 1, 2, 3, 4, 6 i 12). Jest to artefaktu dzielenia na fragmenty. Indeks jest tworzony w 12 fragmentów, których wszystkie można przechowywany na partycji 1 lub jednakowo podzielone na 2, 3, 4, 6 lub 12 partycji (jednego niezależnego fragmentu jednej partycji).

### <a name="remove-replicas"></a>Usuwanie repliki
Po okresach woluminów wysokiej kwerendy można zmniejszyć replik po ładowania zapytań wyszukiwania ma znormalizowany (na przykład po sprzedaży świąteczne za pośrednictwem).

toodo tego przeniesienia hello repliki suwaka wstecz tooa mniejsza ich liczba. Nie istnieją żadne dodatkowe czynności, wymagane ze strony użytkownika. Zmniejszenie liczby replik hello zwalnia maszyn wirtualnych w centrum danych hello. Wprowadzanie operacje zapytań i danych będzie uruchamiana na maszynach wirtualnych mniej niż przed. Witaj minimalny limit to jedna replika.

### <a name="remove-partitions"></a>Usuń partycje
W przeciwieństwie do usuwania repliki, który wymaga nie dodatkowych działań ze strony użytkownika, może być niektórych toodo pracy, jeśli używasz więcej licencji, niż można zmniejszyć. Na przykład jeśli rozwiązanie używa trzech partycji, tooone redukcję zatrudnienia lub dwie partycje wygeneruje błąd jeśli hello nowe miejsce do magazynowania jest mniejszy niż wymagane. Zgodnie z oczekiwaniami może wybrane opcje są indeksy toodelete lub dokumentów w ramach toofree skojarzonego indeksu miejsca, ani zatrzymywać hello bieżącej konfiguracji.

Nie istnieje metoda wykrywania informujący o tym, które odłamków indeksu są przechowywane na określonej partycji. Każda partycja zawiera około 25 GB w magazynie, konieczne będzie tooreduce rozmiar tooa magazynu, że są spełnione przez hello liczbę partycji, do których masz. Jeśli chcesz toorevert tooone partycji, wszystkie odłamków 12 należy toofit.

toohelp planowanie przyszłych, może być toocheck magazynu (przy użyciu [uzyskać statystyki indeksu](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)) toosee ile rzeczywiście używane. 

<a id="advanced-deployment"></a>

## <a name="best-practices-on-scale-and-deployment"></a>Najlepsze rozwiązania w skali i wdrażania
Ten 30-minutowy film wideo przegląda najlepsze rozwiązania dotyczące wdrażania zaawansowanych scenariuszy, w tym rozproszona geograficznie obciążeń. Możesz również sprawdzić [wydajności i optymalizacji w usłudze Azure Search](search-performance-optimization.md) dla pomocy strony tego hello obejmują takie same punkty.

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<a id="next-steps"></a>

## <a name="next-steps"></a>Następne kroki
Po zrozumieniu hello pojęć dotyczących administracji usługi, rozważ użycie [PowerShell](search-manage-powershell.md) tooautomate zadania.

Zalecamy również recenzowania hello [wydajności i optymalizacji artykułu](search-performance-optimization.md).

Inny zaleca hello toowatch wideo zanotowanym w poprzedniej sekcji hello. Zapewnia on lepszą pokrycia technik hello wymienionych w tej sekcji.

<!--Image references-->
[7]: ./media/search-manage/rbac-icon.png
[8]: ./media/search-manage/Azure-Search-Manage-1-URL.png
[9]: ./media/search-manage/Azure-Search-Manage-2-Keys.png
[10]: ./media/search-manage/Azure-Search-Manage-3-ScaleUp.png



