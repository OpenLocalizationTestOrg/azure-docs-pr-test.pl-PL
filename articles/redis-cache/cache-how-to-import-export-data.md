---
title: "aaaImport i wyeksportuj dane w pamięci podręcznej Redis Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooimport i eksportowanie tooand danych z magazynu obiektów blob wystąpieniami usługi pamięć podręczna Redis Azure — warstwa premium"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 4a68ac38-87af-4075-adab-569d37d7cc9e
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: sdanie
ms.openlocfilehash: f17464b207f1c652952f4da63ca147473fee2759
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a>Importowanie i eksportowanie danych w pamięci podręcznej Redis Azure
Import/Eksport jest operacji zarządzania pamięcią podręczną Redis Azure danych, co pozwala tooimport danych w pamięci podręcznej Redis Azure lub eksportowania danych z pamięci podręcznej Redis Azure przez importowanie i Eksportowanie migawki Redis pamięci podręcznej bazy danych (RDB) z pamięci podręcznej blob tooa premium na platformie Azure Konto magazynu. 

- **Eksportuj** — można eksportować z tooa migawki RDB pamięci podręcznej Redis Azure stronicowych obiektów Blob.
- **Importuj** — z migawki RDB pamięci podręcznej Redis można importować z stronicowych obiektów Blob lub blokowych obiektów Blob.

Narzędzie importu/eksportu umożliwia toomigrate między różnymi wystąpieniami usługi pamięć podręczna Redis Azure lub wypełnienia pamięci podręcznej hello danych przed użyciem.

Ten artykuł zawiera przewodnik do importowania i eksportowania danych z pamięci podręcznej Redis Azure i zapewnia odpowiedzi hello toocommonly zadawane pytania.

> [!IMPORTANT]
> Import/Eksport jest w wersji zapoznawczej i jest dostępny tylko dla [warstwy premium](cache-premium-tier-intro.md) przechowuje w pamięci podręcznej.
>
>

## <a name="import"></a>Import
Import może być używane toobring Redis zgodne RDB plików z dowolnego serwera Redis uruchomiona w chmurze lub środowiska, w tym Redis w systemie Linux, Windows albo dowolnego dostawcy chmury, takich jak usług Amazon Web Services i innych użytkowników. Importowanie danych jest łatwe toocreate pamięci podręcznej z wstępnie wypełnione danych. Podczas procesu importowania hello pamięć podręczna Redis Azure ładuje hello RDB pliki z magazynu Azure do pamięci i wstawianie hello klucze do pamięci podręcznej hello.

> [!NOTE]
> Przed rozpoczęciem powitalne operacji importowania, upewnij się, że pliku bazy danych Redis (RDB) lub pliki są przekazywane do strony lub blokowych obiektów blob w magazynie Azure, w hello takie same regionu i subskrypcji jako wystąpienie pamięci podręcznej Redis Azure. Aby uzyskać więcej informacji, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Jeśli wyeksportowany plik RDB przy użyciu hello [Azure Redis pamięci podręcznej wyeksportować](#export) funkcja, plik RDB jest już zapisana w stronicowych obiektów blob i jest gotowy do zaimportowania.
>
>

1. tooimport co najmniej jeden wyeksportowane obiektów blob w pamięci podręcznej [Przeglądaj pamięci podręcznej tooyour](cache-configure.md#configure-redis-cache-settings) w hello portalu Azure i kliknij przycisk **importowania danych** z hello **zasobów menu**.

    ![Importowanie danych][cache-import-data]
2. Kliknij przycisk **wybierz Blob(s)** i wybierz konto magazynu hello zawierający hello tooimport danych.

    ![Wybierz konto magazynu][cache-import-choose-storage-account]
3. Kliknij przycisk hello kontener, który zawiera hello tooimport danych.

    ![Wybierz kontener][cache-import-choose-container]
4. Wybierz co najmniej jeden tooimport obiektów blob, klikając hello obszaru toohello po lewej stronie powitania blob nazwy, a następnie kliknij przycisk **wybierz**.

    ![Wybierz obiekty BLOB][cache-import-choose-blobs]
5. Kliknij przycisk **zaimportować** procesu importowania hello toobegin.

   > [!IMPORTANT]
   > Witaj w pamięci podręcznej nie jest dostępny dla klientów pamięci podręcznej podczas procesu importowania hello, a wszystkie istniejące dane w pamięci podręcznej hello jest usunięte.
   >
   >

    ![Import][cache-import-blobs]

    Możesz monitorować postęp hello operacji importu hello przez następujące powiadomienia hello z hello portalu Azure lub przez wyświetlanie zdarzeń hello w hello [dziennik inspekcji](../azure-resource-manager/resource-group-audit.md).

    ![Postęp importowania][cache-import-data-import-complete]

## <a name="export"></a>Eksportowanie
Eksport umożliwia tooexport hello danych przechowywanych w pamięci podręcznej Redis Azure tooRedis zgodne pliki RDB. Można użyć tych danych toomove funkcji z jednego tooanother wystąpienia pamięci podręcznej Redis Azure lub tooanother serwera Redis. W procesie eksportu hello plik tymczasowy zostanie utworzony na powitania wirtualna hostów hello wystąpienie serwera pamięci podręcznej Redis Azure, czy plik hello jest przekazany toohello wyznaczony konta magazynu. Po ukończeniu operacji eksportowania hello ze stanem powodzenie lub niepowodzenie hello plik tymczasowy zostanie usunięty.

1. tooexport hello bieżącą zawartość hello toostorage pamięci podręcznej, [Przeglądaj pamięci podręcznej tooyour](cache-configure.md#configure-redis-cache-settings) w hello portalu Azure i kliknij przycisk **eksportować dane** z hello **zasobów menu**.

    ![Wybierz kontener magazynu][cache-export-data-choose-storage-container]
2. Kliknij przycisk **Wybierz kontener magazynu** i wybierz konto magazynu hello potrzebne. Konto magazynu Hello musi znajdować się w hello tej samej subskrypcji i regionu co pamięć podręczną.

   > [!IMPORTANT]
   > Eksportuj współpracuje z stronicowe obiekty BLOB, które są obsługiwane zarówno klasycznego i Menedżera zasobów konta magazynu, ale nie są obsługiwane przez [konta usługi Blob storage](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) w tej chwili.
   >
   >

    ![Konto magazynu][cache-export-data-choose-account]
3. Wybierz hello żądanego kontenera obiektów blob i kliknij przycisk **wybierz**. toouse nowy kontener, kliknij przycisk **dodać kontener** tooadd go pierwszy, a następnie wybierz z listy hello.

    ![Wybierz kontener magazynu][cache-export-data-container]
4. Wpisz **prefiks nazwy obiektu Blob** i kliknij przycisk **wyeksportować** toostart hello Eksport. Prefiks nazwy obiektu blob Hello jest nazwy hello tooprefix używane pliki generowane przez tę operację eksportu.

    ![Eksportowanie][cache-export-data]

    Możesz monitorować postęp hello hello operacji eksportowania, przez następujące powiadomienia hello z hello portalu Azure lub przez wyświetlanie zdarzeń hello w hello [dziennik inspekcji](../azure-resource-manager/resource-group-audit.md).

    ![Eksportowanie danych jest pełny][cache-export-data-export-complete]

    Pamięci podręczne pozostają dostępne do użycia podczas procesu eksportowania hello.

## <a name="importexport-faq"></a>Import/Eksport — często zadawane pytania
Ta sekcja zawiera często zadawane pytania dotyczące hello funkcji importowania/eksportowania.

* [Warstw cenowych, jakie można użyć importu/eksportu?](#what-pricing-tiers-can-use-importexport)
* [Można importować dane z dowolnego serwera Redis?](#can-i-import-data-from-any-redis-server)
* [Które wersje RDB można importować?](#what-rdb-versions-can-i-import)
* [Moje pamięci podręcznej jest dostępna podczas operacji importu/eksportu?](#is-my-cache-available-during-an-importexport-operation)
* [Import/Eksport można używać z klastrem Redis?](#can-i-use-importexport-with-redis-cluster)
* [Jak działa importu/eksportu z niestandardowych baz danych, ustawienia](#how-does-importexport-work-with-a-custom-databases-setting)
* [Sposób importu/eksportu jest inny niż trwałość Redis](#how-is-importexport-different-from-redis-persistence)
* [Czy można zautomatyzować przy użyciu programu PowerShell, interfejsu wiersza polecenia lub innych klientów zarządzania importu/eksportu?](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [Otrzymuję błąd upływu limitu czasu podczas mojej operacji importu i eksportu. Co to znaczy?](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [Otrzymano wystąpił błąd podczas eksportowania tooAzure Moje dane magazynu obiektów Blob. Co się stało?](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a>Warstw cenowych, jakie można użyć importu/eksportu?
Narzędzie importu/eksportu jest dostępna tylko w warstwie cenowej premium hello.

### <a name="can-i-import-data-from-any-redis-server"></a>Można importować dane z dowolnego serwera Redis?
Tak, oprócz danych tooimporting wyeksportowanych z wystąpienia pamięci podręcznej Redis Azure, można importować RDB plików z dowolnego serwera Redis uruchomiona w chmurze lub środowiska, takich jak Linux, Windows lub dostawców chmury, takich jak usług Amazon Web Services. toodo to przekazywanie hello RDB plików z serwera Redis hello potrzebne do obiektu blob strony lub blok w konta magazynu Azure, a następnie zaimportuj go do wystąpienia pamięci podręcznej Redis Azure premium. Może na przykład chcesz tooexport hello danych z pamięci podręcznej produkcji i zaimportuj go do pamięci podręcznej używany jako część środowiska przemieszczania do testowania lub migracji.

> [!IMPORTANT]
> Importuj dane toosuccessfully wyeksportowane z pamięci podręcznej Redis serwerów innych niż pamięć podręczna Redis Azure przy użyciu stronicowych obiektów blob, rozmiar obiektu blob strony hello musi być wyrównany na granicy 512-bajtowe. Dla przykładowy kod tooperform wszelkie niezbędne uzupełnienie bajt, zobacz [przykładowe strony blogu przekazywania](https://github.com/JimRoberts-MS/SamplePageBlobUpload).
> 
> 

### <a name="what-rdb-versions-can-i-import"></a>Które wersje RDB można importować?

Pamięć podręczna Redis Azure obsługuje importu RDB za pośrednictwem RDB w wersji 7.

### <a name="is-my-cache-available-during-an-importexport-operation"></a>Moje pamięci podręcznej jest dostępna podczas operacji importu/eksportu?
* **Eksportuj** — pamięci podręcznych pozostają dostępne i można kontynuować toouse pamięci podręcznej podczas operacji eksportowania.
* **Importuj** — pamięci podręcznych staną się niedostępne po uruchomieniu operacji importowania i stają się dostępne po zakończeniu operacji importowania hello.

### <a name="can-i-use-importexport-with-redis-cluster"></a>Import/Eksport można używać z klastrem Redis?
Tak, a użytkownik może importu/eksportu między klastrowanym pamięci podręcznej i nieklastrowanych pamięci podręcznej. Ponieważ klaster Redis [tylko obsługuje bazy danych 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), nie jest importowane żadnych danych w bazach danych innych niż 0. Podczas importowania danych z pamięci podręcznej klastrowanych hello klucze są rozdzielane odłamków hello hello klastra.

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a>Jak działa importu/eksportu z niestandardowych baz danych, ustawienia
Niektóre warstw cenowych mają różne [baz danych limity](cache-configure.md#databases), więc istnieją pewne kwestie podczas importu, jeśli skonfigurowano niestandardowej wartości dla hello `databases` ustawienie podczas tworzenia pamięci podręcznej.

* Podczas importowania tooa cenowym o niższej `databases` limit niż warstwy hello, z którego zostały wyeksportowane:
  * Jeśli używasz hello domyślną liczbę `databases`, która jest 16 dla wszystkich warstw cenowych, nie zostały utracone żadne dane.
  * Jeśli używasz niestandardowego liczba `databases` czy wypada w granicach hello na powitania warstwy toowhich importowany, zostały utracone żadne dane.
  * Jeśli wyeksportowane dane zawarte w danych w bazie danych, która przekracza limitów hello hello nową warstwę, hello danych z tych wyższej baz danych nie został zaimportowany.

### <a name="how-is-importexport-different-from-redis-persistence"></a>Sposób importu/eksportu jest inny niż trwałość Redis
Trwałość pamięci podręcznej Redis Azure umożliwia toopersist danych przechowywanych w pamięci podręcznej Redis tooAzure magazynu. Po skonfigurowaniu trwałości, pamięć podręczna Redis Azure będzie się powtarzać migawki pamięci podręcznej Redis hello w pamięci podręcznej Redis toodisk format binarny, na podstawie można skonfigurować częstotliwości tworzenia kopii zapasowej. W przypadku poważnej zdarzeń wyłączająca zarówno hello podstawowy i repliki w pamięci podręcznej, dane pamięci podręcznej hello został przywrócony automatycznie przy użyciu najnowszych migawki hello. Aby uzyskać więcej informacji, zobacz [jak trwałości danych tooconfigure dla podręczna Redis Azure Premium](cache-how-to-premium-persistence.md).

Importu / eksportu umożliwia dane toobring lub do eksportowania z pamięci podręcznej Redis Azure. Nie skonfigurowanie kopii zapasowej i przywracania przy użyciu trwałość Redis.

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a>Czy można zautomatyzować przy użyciu programu PowerShell, interfejsu wiersza polecenia lub innych klientów zarządzania importu/eksportu?
Tak, dla środowiska PowerShell instrukcje można znaleźć [tooimport pamięci podręcznej Redis](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) i [tooexport pamięci podręcznej Redis](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a>Otrzymuję błąd upływu limitu czasu podczas mojej operacji importu i eksportu. Co to znaczy?
Jeśli pozostają na powitania **importowania danych** lub **eksportować dane** bloku przez czas dłuższy niż 15 minut przed zainicjowaniem operacji hello komunikat o błędzie z błąd komunikat podobny toohello poniższy przykład:

    hello request tooimport data into cache 'contoso55' failed with status 'error' and error 'One of hello SAS URIs provided could not be used for hello following reason: hello SAS token end time (se) must be at least 1 hour from now and hello start time (st), if given, must be at least 15 minutes in hello past.

tooresolve, zainicjować hello importu lub eksportu przed upływem 15 minut.

### <a name="i-got-an-error-when-exporting-my-data-tooazure-blob-storage-what-happened"></a>Otrzymano wystąpił błąd podczas eksportowania tooAzure Moje dane magazynu obiektów Blob. Co się stało?
Eksport działa tylko w przypadku plików RDB przechowywane jako stronicowych obiektów blob. Inne typy obiektów blob nie są obecnie obsługiwane, łącznie z konta magazynu obiektów blob z warstwami gorącego i chłodnego. Aby uzyskać więcej informacji, zobacz [konta usługi Blob storage](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).

## <a name="next-steps"></a>Następne kroki
Dowiedz się, jak toouse premium więcej pamięci podręcznej funkcji.

* [Wprowadzenie toohello pamięci podręcznej Redis Azure Premium warstwy](cache-premium-tier-intro.md)    

<!-- IMAGES -->
[cache-settings-import-export-menu]: ./media/cache-how-to-import-export-data/cache-settings-import-export-menu.png
[cache-export-data-choose-account]: ./media/cache-how-to-import-export-data/cache-export-data-choose-account.png
[cache-export-data-choose-storage-container]: ./media/cache-how-to-import-export-data/cache-export-data-choose-storage-container.png
[cache-export-data-container]: ./media/cache-how-to-import-export-data/cache-export-data-container.png
[cache-export-data-export-complete]: ./media/cache-how-to-import-export-data/cache-export-data-export-complete.png
[cache-export-data]: ./media/cache-how-to-import-export-data/cache-export-data.png
[cache-import-data]: ./media/cache-how-to-import-export-data/cache-import-data.png
[cache-import-choose-storage-account]: ./media/cache-how-to-import-export-data/cache-import-choose-storage-account.png
[cache-import-choose-container]: ./media/cache-how-to-import-export-data/cache-import-choose-container.png
[cache-import-choose-blobs]: ./media/cache-how-to-import-export-data/cache-import-choose-blobs.png
[cache-import-blobs]: ./media/cache-how-to-import-export-data/cache-import-blobs.png
[cache-import-data-import-complete]: ./media/cache-how-to-import-export-data/cache-import-data-import-complete.png
