---
title: "aaaAzure Data Catalog — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące usługi Azure Data Catalog, w tym funkcji Odnajdywanie źródła danych, adnotacja i zarządzania."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5c7e209a-458c-4bb4-96bb-7ed178f9528a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 03f9f4b801640b2e14232c62c8fc168e42e2c393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-frequently-asked-questions"></a>Wykaz danych Azure — często zadawane pytania
Ten artykuł zawiera odpowiedzi toofrequently zadawane pytania powiązane toohello usługi Azure Data Catalog.

## <a name="what-is-azure-data-catalog"></a>Co to jest usługa Azure Data Catalog?
Wykazu danych to w pełni zarządzana usługa, hostowanej na platformie Microsoft Azure, która służy jako system rejestracji i odnajdywania źródeł danych przedsiębiorstwa. Data Catalog każdy użytkownik z analityków toodata programistów i analityków, można zarejestrować, odnajdywanie zrozumieć i używania źródeł danych.

## <a name="what-customer-challenges-does-it-solve"></a>Jaką klient będzie wymagał robi to rozwiązuje?
Adresy wykazu danych hello wyzwania źródło danych odnajdywania i "ciemny dane", dzięki czemu użytkownicy mogą odnaleźć i zrozumieć źródeł danych przedsiębiorstwa.

## <a name="what-are-its-target-audiences"></a>Jakie są jej docelowi?
Data Catalog jest przeznaczona dla użytkowników Pomoc techniczna i nietechniczna, w tym:

* Dane deweloperów i specjalistów BI i analiza: osób odpowiedzialnych za tworzenie danych i ich analiza zawartości dla innych tooconsume.
* Dane stewards: osób, które mają hello wiedzą na temat hello danych, co oznacza i jak jest zamierzone toobe używane.
* Konsumenci danych: osoby, który należy tooeasily stanie toobe odnajdowanie, zrozumieć i łączenie danych toohello potrzebują toodo ich zadania za pomocą narzędzia hello wybranych przez nich.
* Centralna IT: użytkownicy, którzy potrzebują toomake setki źródeł danych wykrywalny przez użytkowników biznesowych i którzy potrzebują toomaintain nadzoru nad sposobu używania danych i przez kogo.

## <a name="what-is-its-availability-by-region"></a>Co to jest jego dostępność według regionu?
Usługi wykazu danych są obecnie dostępne w hello następujących centrach danych:

* Zachodnie stany USA
* Wschodnie stany USA
* Europa Zachodnia
* Europa Północna
* Australia Wschodnia
* Azja Południowo-Wschodnia

## <a name="what-are-its-limits-on-hello-number-of-data-assets"></a>Jakie są limity jego hello liczby zasobów danych?
Witaj bezpłatnej wersji wykazu danych jest ograniczone too5, 000 zarejestrowanych zasobów danych.

obsługuje Standard Edition usługi Data Catalog Hello się too100, 000 zarejestrowanych zasobów danych.

## <a name="what-are-its-supported-data-source-and-asset-types"></a>Co to są typy źródła i zasobów jego obsługiwane dane?
Aby uzyskać listę aktualnie obsługiwanych źródeł danych, zobacz [DSR wykazu danych](data-catalog-dsr.md).

## <a name="how-do-i-request-support-for-another-data-source"></a>Jak zażądać pomocy technicznej przez inne źródło danych?
toosubmit funkcji żądania i inne opinie na temat Przejdź toohello [forum usługi Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="how-do-i-get-started-with-data-catalog"></a>Jak rozpocząć pracę z wykazu danych?
Najlepszym sposobem tooget Hello jest uruchomiona, przechodząc zbyt[wprowadzenie do korzystania z usługi Data Catalog](data-catalog-get-started.md). W tym artykule przedstawiono end-to-end możliwości hello hello usługi.

## <a name="how-do-i-register-my-data"></a>Jak zarejestrować dane?
tooregister danych w katalogu danych:
1. W portalu Azure Data Catalog hello w hello **publikowania** obszaru, narzędzie do rozpoczęcia hello Azure Data Catalog rejestracji. 
2. W hello Data Catalog publikowanie aplikacji, zaloguj się przy użyciu hello sam poświadczeń, że używasz tooaccess hello portalu wykazu danych.
3. Wybierz źródło danych hello i hello określonych zasobów, które mają tooregister.

## <a name="what-properties-does-it-extract-for-data-assets-that-are-registered"></a>Właściwości, które powoduje ona rozpakowania zasobów danych, które są zarejestrowane w?
właściwości specyficzne dla Hello różnią się od źródła toodata źródła danych, ale ogólnie rzecz biorąc, Usługa publikowania w wykazie danych hello wyodrębnia hello następujących informacji:

* Nazwa zasobu
* Typ zasobu
* Opis elementu zasobów
* Nazwy atrybutu/kolumny
* Typy danych atrybutu/kolumny
* Opis atrybutu/kolumny

> [!IMPORTANT]
> Rejestrowanie zasobów danych z usługi Data Catalog nie przenosić ani kopiować chmury toohello danych. Rejestrowanie zasobów ze źródła danych kopii hello tooAzure metadanych zasoby, ale hello dane pozostają w istniejącej lokalizacji źródła danych hello. reguły toothis wyjątku Hello jest, jeśli wybierzesz rekordy Podgląd tooupload lub profilu danych podczas rejestrowania hello zasoby. Po dołączeniu Podgląd się too20 rekordy zostały skopiowane z poszczególnych zasobów i przechowywane jako migawka w wykazie danych. Po dołączeniu profilu danych agregują informacje jest obliczana i zawarte w metadanych hello, które są przechowywane w katalogu hello. Agregują informacje można zawiera rozmiaru hello tabel, hello procent wartości null dla kolumny lub hello minimalne, maksymalne i średnie wartości kolumny. 
>
>

> [!NOTE]
> Dla źródeł danych, takich jak SQL Server Analysis Services ma najwyższej jakości **opis** właściwość hello Data Catalog publikowania aplikacji wyodrębnia wartości tej właściwości. Relacyjnych baz danych programu SQL Server, w której brakuje najwyższej jakości **opis** właściwość, usługi Data Catalog publikowania aplikacji hello wyodrębnianie wartości hello z hello **ms_description** rozszerzone właściwości dla obiektów i kolumn. Aby uzyskać więcej informacji, zobacz [przy użyciu właściwości rozszerzone w obiektach bazy danych](https://technet.microsoft.com/library/ms190243%28v=sql.105%29.aspx).
>
>

## <a name="how-long-should-it-take-for-newly-registered-assets-tooappear-in-hello-catalog"></a>Jak długo powinien upłynąć do nowo zarejestrowanych zasobów tooappear w katalogu hello?
Po zarejestrowaniu zasoby z wykazu danych może być okres 5 sekund too10 przed wyświetleniem hello portalu wykazu danych.

## <a name="how-do-i-annotate-and-enrich-hello-metadata-for-my-registered-data-assets"></a>Jak dodawać adnotacje i wzbogacić hello metadanych dla moich zarejestrowanych zasobów danych?
Hello najprostszy sposób tooprovide metadanych dla zarejestrowanych zasobów jest tooselect hello zasobów w portalu wykazu danych hello, a następnie wprowadź wartości hello w okienku właściwości hello lub okienku schematu dla wybranego obiektu hello.

Można też podać niektóre metadane, takie jak ekspertów i tagi, podczas procesu rejestracji hello. wartości Hello w hello Usługa publikowania w wykazie danych zastosować zasoby tooall jest zarejestrowany w tym czasie. tooview hello ostatnio zarejestrowane obiekty w portalu hello dodatkowych adnotacji, wybierz hello **Wyświetl Portal** przycisk w ostatnim ekranie powitania hello Data Catalog publikowania aplikacji.

## <a name="how-do-i-delete-my-registered-data-objects"></a>Jak usunąć dane zarejestrowane obiekty?
Wybieranie obiektu hello w portalu hello, a następnie klikając polecenie hello można usunąć obiektu z wykazu danych **usunąć** przycisku. Usuwanie obiektu hello usuwa metadanych z wykazu danych, ale nie ma wpływu na powitania źródła danych.

## <a name="what-is-an-expert"></a>Co to jest eksperta?
Ekspert jest osoba, która ma perspektywy informacji dotyczących obiektu danych. Każdy obiekt może mieć wielu ekspertów. Ekspert nie jest konieczne hello toobe "właściciela" dla obiektu, ale to po prostu osoba, która wie, w jaki sposób dane hello i powinna być używana.

## <a name="how-do-i-share-information-with-hello-data-catalog-team-if-i-encounter-problems"></a>Jak udostępnić informacje z zespołem usługi Data Catalog hello I wystąpienia problemów?
problemy tooreport udostępniania informacji i zadać pytania, przejdź toohello [forum usługi Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="does-hello-catalog-work-with-another-data-source-that-im-interested-in"></a>Ma hello katalogu roboczego z innego źródła danych, które interesuje mnie?
Aktywnie pracujemy nad dodanie więcej tooData źródeł danych katalogu. Jeśli chcesz toosee określonego źródła danych obsługiwane Sugeruj go (lub głosowych działem pomocy technicznej, jeśli została już sugerowane) przez przejście toohello [forum usługi Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="how-is-azure-data-catalog-related-toohello-data-catalog-in-power-bi-for-office-365"></a>W jaki sposób usługa Azure Data Catalog związane z toohello wykazu danych w usłudze Power BI dla Office 365?
Azure Data Catalog można traktować jako ewolucji hello wykazu danych w usłudze Power BI. Począwszy od spring 2017 Azure Data Catalog jest hello tooenable używane do udostępniania i wykrywania zapytań w programie Excel 2016 i dodatku Power Query dla programu Excel. Możliwości usługi Data Catalog w programie Excel są dostępne toousers z licencjami usługi Power BI Pro.

## <a name="what-permissions-do-i-need-tooregister-assets-with-data-catalog"></a>Czy uprawnienia wymagane zasoby tooregister Data Catalog?
Narzędzie rejestracji usługi Data Catalog hello toorun, musisz mieć uprawnienia na powitania źródła danych, które pozwala tooread hello metadanych ze źródła hello. tooalso Dołącz Podgląd, musisz mieć uprawnienia, które pozwalają tooread hello danych z obiektów hello jest zarejestrowany.

## <a name="will-data-catalog-be-made-available-for-on-premises-deployment-as-well"></a>Wykaz danych będą dostępne dla lokalnego wdrożenia?
Data Catalog to usługi chmury, która może współpracować z toodeliver źródeł danych zarówno w chmurze, jak i dla lokalnego źródła danych odnajdywania hybrydowego. Obecnie nie ma żadnych planów dla wersji hello usługi Data Catalog w lokalnej.

## <a name="can-i-extract-more-or-richer-metadata-from-hello-data-sources-i-register"></a>Czy można wyodrębnić metadanych więcej lub bardziej rozbudowane, z hello źródeł danych, które można zarejestrować?
Aktywnie pracujemy tooexpand hello możliwości usługi Data Catalog. Jeśli chcesz, dodatkowe metadane toohave wyodrębnione ze źródła danych hello podczas rejestracji, sugerować go (lub głos go, jeśli została już sugerowane) w hello [forum usługi Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409). W przyszłości hello możemy umożliwi stron trzecich tooadd nowe źródło typy danych za pomocą rozszerzeń interfejsu API.

## <a name="how-do-i-restrict-hello-visibility-of-registered-data-assets-so-that-only-certain-people-can-discover-them"></a>Jak ograniczyć widoczność hello zarejestrowanych zasobów danych, tak, aby tylko wybrani użytkownicy może wykrywać je?
Wybierz zasoby danych hello hello wykazu danych, a następnie kliknij przycisk hello **Przejmij na własność** przycisku. Właściciele zasobów danych w katalogu danych można zmienić widoczność hello tooeither ustawienia Zezwalaj na wszystkie hello toodiscover użytkowników należące do zasobów lub ograniczyć widoczność toospecific użytkowników.

## <a name="how-do-i-update-hello-registration-for-a-data-asset-so-that-changes-in-hello-data-source-are-reflected-in-hello-catalog"></a>Jak zaktualizować hello rejestracji dla zasobów danych, tak aby zmiany w źródle danych hello są uwzględniane w katalogu hello?
metadane hello tooupdate dla zasobów danych, które są już zarejestrowane w wykazie hello, po prostu ponownie zarejestrować hello źródła danych, które zawiera zasoby hello. Wszelkie zmiany w źródle danych hello, takie jak kolumny są dodane lub usunięte z tabel lub widoków, są aktualizowane w katalogu hello, ale zostaną zachowane wszystkie adnotacje dostarczone przez użytkowników.

## <a name="my-question-isnt-answered-here-where-can-i-go-for-answers"></a>Mojego pytania nie jest tutaj odpowiedzi. Gdzie można przejść do odpowiedzi?
Przejdź toohello [forum usługi Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409). Monitów zostanie ustalone, sposób ich tutaj.
