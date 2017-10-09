---
title: aaaAzure bazy danych SQL Azure zastosowania - Snelstart | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat sposobu SnelStart używa bazy danych SQL toorapidly rozwinięty jego usługi biznesowe w wysokości 1000 nowych bazami danych SQL Azure na miesiąc"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: fab506b2-439d-4f1a-bdc5-d1d25c80d267
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 69572393f41a9baf44f41b4f5f4ebbef347de851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="with-azure-snelstart-has-rapidly-expanded-its-business-services-at-a-rate-of-1000-new-azure-sql-databases-per-month"></a>Azure SnelStart szybko rozwinął jego usługi biznesowe w wysokości 1000 nowych bazami danych SQL Azure na miesiąc
![SnelStartLogo](./media/sql-database-implementation-snelstart/snelstartlogo.png)

SnelStart sprawia, że popularnych finansowych - i business — oprogramowanie do zarządzania dla małych i średnich firm (SMB) hello (Holandia). 55,000 klientów są obsługiwane przez personel 110 pracowników, w tym personel działu informatycznego 35. Przenoszenie z oferty oprogramowania — jako — usługa (SaaS) tooa oprogramowanie komputerowe zbudowany na platformie Azure, SnelStart wprowadzone hello najbardziej usług wbudowanych automatyzacji zarządzania przy użyciu znanego środowiska w języku C# i optymalizacji wydajności i skalowalności przez ani - over lub w obszarze udostępniania firmy za pomocą elastycznych pul. Za pomocą usługi Azure zapewnia płynną hello SnelStart przenoszenia klientów między lokalnymi i hello chmury.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-SnelStart/player]
> 
> 

## <a name="why-snelstart-extended-services-from-hello-desktop-toohello-cloud"></a>Dlaczego SnelStart rozszerzony usług z hello pulpitu toohello chmury
> "Pracy z platformą Azure oznacza, że firma Microsoft może szybciej dostarczanie oprogramowania, szybko reagować toocustomer wymagań i skalować rozwiązania, gdy zapotrzebowanie."
> 
> — Henry został architekt oprogramowania
> 
> 

SnelStart została uruchomiona pomyślnie oprogramowania firmy lat, przy użyciu modelu tradycyjnych programowanie: kodu, pakiet wysyłki i powtórz. Wraz z upływem czasu hello tempo zmian rozwijały się szybciej i szybciej. Przepisy dotyczące często zmieniane, a klienci potrzebne łatwiejsze dokumentów finansowych tooprocess sposoby i współpracować z ich księgowym i dla instytucji rządowych tookeep się z tymi zmianami.

"Wysyłania toocustomers oprogramowania jest kosztowne i ograniczającej," zgodnie z tooHenry zostały architekt oprogramowania. "Produkcji, opakowywanie i kosztów wysyłki ograniczone częstotliwość można wydać oprogramowanie. Było toopackage aktualizacje okresowe wysyłek, ale który wprowadzone twardych toomeet klientów wymaga zmiany. Firma Microsoft może nigdy nie mieć pewność, że naszym klientom uaktualniony toohello najnowszej wersji produktu hello. W związku z tym było toosupport wiele wersji, co hello obsługuje również zadania toodo bardzo trudne."

Zostały dodaje, "możemy sposób tooprogram i wersji aktualizacji przyspieszonego tempie, dlatego firma Microsoft może innowacji szybciej i Utwórz nowe usługi dla klientów. Możemy również poszukiwane tooautomate sposób więcej procesów w kolejności toosimplify potrzeby biznesowe administracji klientów."

Dla SnelStart, hello rozwiązanie było tooextend jego usługi staje się dostawcę SaaS oparte na chmurze. Platforma Azure SQL Database Hello pomogła SnelStart tam bez ponoszenia hello głównych IT obciążenie, które wymagałyby rozwiązania infrastruktury jako — usługa (IaaS).

model chmury Hello również umożliwia SnelStart toofix usterek i udostępnia nowe funkcje szybko, bez konieczności toodownload i uaktualnienie oprogramowania klientów. Zgodnie z tooBeen, "Using usług w chmurze Azure pozwala nam act tooquickly po zmianie wymagań od osób trzecich. Zamiast tooship nowe toothousands wersji klientów, możemy dostosować informacje wysyłane z naszych formatów toonew aplikacji komputerowych wymagane przez osoby trzecie."

## <a name="a-modern-company-with-traditional-roots"></a>Nowoczesne firmy z tradycyjnego katalogów głównych
SnelStart jest to nowoczesny, elastyczne, zaawansowanych technologicznie firma mieszcząca skromny katalogów głównych uaktualniania too1964, rozpoczęcie założycieli hello firmy hello producent części instrumentów muzycznych. Puls Hello z hello SnelStart oprogramowanie firm uruchomiona naprawdę bicie w hello lat 1980, podczas hello mnożenie hello komputerów osobistych. firmy Hello potrzebne lepsze alternatywnych toohello oprogramowania dostępne w czasie hello, więc zajęło sprawach w jego własnej ręce. W 1982 firma hello utworzona podstawę hello co ostatecznie staje się SnelStart oprogramowania. Od początku hello oprogramowania hello został admired na prostotę i szybkość — tak duża, aby firmy powitania po pewnym czasie zmienić fokus i reinvented się do producenta oprogramowania.

W 1995 r. SnelStart wydawane swoją pierwszą aplikację księgowości dla systemu Windows. Aplikacja Hello, oparty na baz danych programu Microsoft Visual Basic 1.0 i programu Microsoft Access, pomogła wzrostu powitania klienta podstawowej toomore niż 5000 użytkownikami.

Obecnie SnelStart jest głównych dostawcy — biznesowych (LOB) i aplikacji biznesowych administracji celem holenderski małych i średnich firmach i przedsiębiorcami samodzielnej. Jak Carlo Kuip, architektów IT, jest wyświetlany komunikat "naszym celem jest tooprovide 100 procent automatyzacji usług biznesowych administracji dla naszych klientów."

## <a name="optimizing-performance-and-cost-with-elastic-pools"></a>Optymalizacja wydajności i kosztów z pul elastycznych
SnelStart został na dużą skalę "wczesnego uczestnictwa" elastyczne pule. Pule elastyczne hello firmy limit koszty i bardziej wydajnie zarządzać wymagania dotyczące wydajności. Zgodnie z tooBeen "przy użyciu pul elastycznych, możemy wydajność można zoptymalizować w zależności od wymagań hello naszych klientów bez przerostu. Gdyby tooprovision oparte na obciążenia szczytowego, jest dość kosztowna. Zamiast tego hello opcja tooshare zasobów między wieloma bazami danych niskiego obciążenia umożliwia toocreate rozwiązanie, które wykonuje również i kosztach. "

## <a name="azure-sql-databases-help-containerize-data-for-isolation-and-security"></a>Bazy danych SQL Azure pomocy containerize danych izolacji i zabezpieczeń
Baza danych SQL Azure umożliwia SnelStart tooeasily i niezauważalnie przenosić tooAzure danych business administracyjnej lokalnych klientów. Hello bazy danych SQL Azure jest wygodne kontenerem, który zapewnia izolację, granicy do uwierzytelniania, autoryzacji i łatwe możliwości tworzenia kopii zapasowych i przywracania. Bazy danych podaj odpowiednie model koncepcyjny zarządzania. Zgodnie z tooCarlo Kuip, architektów IT "elementów w obrębie granicy ten kontener zawiera poufne dane tooa kluczowe znaczenie biznesowe i przechowywania tych elementów w przechowuje izolowanej bazy danych oraz ich ochronę. Firma Microsoft może zarządzać autoryzacji na poziomie bazy danych hello i nawet automatyzacji zarządzania hello i skalowalnego w poziomie z tych baz danych bez konieczności administratorów bazy danych (DBAs) na pracowników".

Usługa Azure SQL Data Warehouse także pełni rolę w wątku zabezpieczeń i zarządzania SnelStart hello przez firmy hello zebrać dane telemetryczne, np. wykrywania nieautoryzowanego dostępu, rejestrowanie aktywności użytkownika i łączności.

## <a name="azure-removes-overhead-so-that-developers-can-spend-more-time-delivering-value"></a>Azure usuwa nakładów pracy, dzięki czemu deweloperzy mogą poświęcić więcej czasu na dostarczanie wartości
model platformy Azure Hello usunięte koszty infrastruktury i włączone SnelStart tooautomate wdrożenia korzystające z biblioteki zarządzania C#. Jak Kuip stany, "możemy stanie toogrow opcje nasze bieżące operacje z bardzo małych personelu podczas jednocześnie zwiększa skalowalność, szybkości i odzyskiwanie po awarii dla klientów. Programowanie tooservices shift Hello zwalniane zasobów toofocus nowych usług i funkcji, a nie tylko Uaktualnianie istniejącego kodu tookeep się nowe kody przepisy lub podatku." Dodaje, "Automatyzacji zarządzania i używając hello SaaS oferty, możemy stanie toodeliver więcej wartości dla klientów bez konieczności toomake dużych inwestycji w operacyjnej personelu." Na przykład przy użyciu platformy Azure i elastyczne pule, SnelStart został tooadd stanie szereg nowych funkcji, tym bardziej niezawodne integracji danych klienta w bankach, rozliczeń nowych usług, kontrole małych firm i usługi poczty e-mail.

> "Hello tylko pierwszych kilku miesięcy 2016, możemy rozwinięty naszych wdrożeń baza danych SQL Azure z około 5500 toomore niż 12 000 i obecnie trwa dodawanie około 1000 baz danych miesięcznie."
> 
> — Henry został architekt oprogramowania
> 
> 

Zarządzanie bazą danych jest dalsze zautomatyzowanej przy użyciu funkcji zadania elastyczne hello. Jak Kuip stany, "wysokiej Cenimy hello automatycznego wykrywania baz danych w wystąpieniu bazy danych SQL (server)." Dzięki temu SnelStart tooexecute operacji zarządzania przez klienta dynamicznie rosnącym podstawowej bez dodatkowych kosztów związanych.

SnelStart jest również tworzenie interfejsu API, który działa jako broker między danych klienta i aplikacje przez partnerów oprogramowania innych firm. Jak Państwa Kuip "tego interfejsu API umożliwi innych dostawców tooadd funkcji tooour oprogramowania, takiego jak wyeliminowanie wprowadzenie danych faktury i inne dokumenty." Klienci nie będą już zawierały toomanually typu faktury do ich małych firm oprogramowania; Witaj oprogramowania SnelStart wymieniają hello niezbędne informacje bezpośrednio. Dzięki temu klienci toojoin ich business-zadania z ekosystemem hello jest wychodzące z transformacji cyfrowych w branży hello informacji.  

## <a name="how-azure-services-enable-saas-for-snelstart"></a>W jaki sposób usługi Azure umożliwiają SaaS dla SnelStart
Za pomocą usługi Azure, SnelStart może obsługiwać klientów i ich księgowym więcej bezproblemowo w chmurze hello. Na przykład klientów i księgowym udostępniać informacje innym uzyskując bezpośrednio dostęp do interfejsu API klienta dla SnelStart, hostowanej na platformie Azure. Kuip Stany "aplikacje sieci web skierowane do klienta tooour dostępne są te usługi wielokrotnego użytku, oraz zapewniają wspólnej infrastruktury i funkcje tooallow dostępu toobusiness administracji dla klientów i toothird firm używane przez klientów. Przykładami zapewnia możliwości konfiguracji produktów, zarządzanie reguły zapory i zarządzanie procesy długotrwałe, takich jak tworzenie kopii zapasowych."

> Naszym celem jest tooprovide 100 procent automatyzacji usług biznesowych administracji dla naszych klientów." 
> 
> — Carlo Kuip, architektów IT
> 
> 

Ponadto usługi sieci web SnelStart pozwalają zarówno klientów i księgowym tooeasily uzyskiwanie dostępu do danych w puli elastycznej bazy danych SQL Azure. Ten model SaaS, w połączeniu z bazy danych, elastyczność i usługi Azure Resource Manager zapewnia SnelStart funkcje skalowalności, które uzupełniają każdego wdrożenia usługi Azure. Implementacja Hello jest pełni zautomatyzowany przy użyciu biblioteki zarządzania C#.

![Architektura SnelStart](./media/sql-database-implementation-snelstart/figure1.png)

Rysunek 1. Począwszy od czerwca 2016 SnelStart ma więcej niż 11 000 baz danych i pul elastycznych więcej niż 50

## <a name="simplicity-from-hello-cloud"></a>Prostota z hello chmury
Od przenoszenie tooan rozwiązania w chmurze platformy Azure, SnelStart została wzrostu szybkie klienta stanie toosupport podczas oferty usługi i innowacyjnych funkcji. Zgodnie z tooBeen, "z platformy Azure, udostępnienia niemalże ciągłe aktualizacje dla naszych klientów bez rozwijania pracownikami operacji. I uzyskujemy hello wszystkie inne doskonałe funkcje platformy Azure — takie jak skalowalność i odzyskiwanie po awarii — powiązane w. "

> "Kiedy możemy faktycznie za pośrednictwem w Redmond... Zwrócona wywołanie dewelopera w Holandia hello chciałaby mnie dotyczące konkretnego problemu. Firma Microsoft zostały toodeliver Microsoft tooget możliwe zmiany w środowisku produkcyjnym w ciągu 48 godzin toosolve naszych problem. "
> 
> — Henry został architekt oprogramowania
> 
> 

SnelStart ocenia również hello silne powiązanie, które zostały one opracowany z zespołem bazy danych SQL Azure Microsoft hello. Jak Państwa Kuip "mamy dyskusjach na temat funkcji i jak zwiększyć toouse technologii, która jest coś po obu stronach."
Hello bezpośrednim celem dla SnelStart jest tookeep rośnie podstawowego spełnia klienta. Jak zostało Stany "Bez hello technicznych i ograniczenia zasobów, które było jako niezależnego dostawcy oprogramowania, brak nie toohow limit do tej pory firma Microsoft mogła się rozrastać."

## <a name="more-information"></a>Więcej informacji
* toolearn więcej informacji na temat usługi Azure pule elastyczne, zobacz [pule elastyczne](sql-database-elastic-pool.md).
* Zobacz toolearn więcej informacji na temat ról sieć Web i roli proces roboczy [roli proces roboczy](../fundamentals-introduction-to-azure.md#compute).    
* toolearn więcej informacji na temat usługi Azure SQL Data Warehouse, zobacz [SQL Data Warehouse](https://azure.microsoft.com/documentation/services/sql-data-warehouse/)
* toolearn więcej informacji na temat SnelStart, zobacz [SnelStart](http://www.snelstart.nl).

