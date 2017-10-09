---
title: "aaaOnline kopia zapasowa i przywracanie z bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooperform automatyczne kopie zapasowe i przywracanie bazy danych z bazy danych Azure rozwiązania Cosmos."
keywords: Kopia zapasowa i przywracanie, tworzenie kopii zapasowej online
services: cosmos-db
documentationcenter: 
author: RahulPrasad16
manager: jhubbard
editor: monicar
ms.assetid: 98eade4a-7ef4-4667-b167-6603ecd80b79
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/11/2017
ms.author: raprasa
ms.openlocfilehash: a0b464c95681dfc7b5462b02bf04c2c43d6bc16f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-online-backup-and-restore-with-azure-cosmos-db"></a>Automatyczne tworzenie kopii zapasowej online i przywracania bazy danych Azure rozwiązania Cosmos
Azure DB rozwiązania Cosmos automatycznie wykonuje kopie zapasowe wszystkich danych w regularnych odstępach czasu. Hello automatycznego tworzenia kopii zapasowych woluminów bez wpływu na wydajność hello lub dostępności operacji w bazie danych. Kopie zapasowe są przechowywane oddzielnie w innej usłudze magazynu, a te kopie zapasowe globalnie są replikowane w celu odporność regionalnej awarii. Hello automatycznego tworzenia kopii zapasowej są przeznaczone dla scenariuszy podczas przypadkowego usunięcia z kontenera Comos DB i później wymagają danych odzyskiwania lub rozwiązanie odzyskiwania po awarii.  

W tym artykule rozpoczyna się od szybkie drużyn hello danych nadmiarowości i dostępności w bazie danych rozwiązania Cosmos, a następnie omówiono tworzenie kopii zapasowych. 

## <a name="high-availability-with-cosmos-db---a-recap"></a>Wysoka dostępność rozwiązania Cosmos DB — podsumowanie
Rozwiązania cosmos bazy danych jest zaprojektowana toobe [globalnie rozproszone](distribute-data-globally.md) — umożliwia przepływności tooscale w różnych regionach platformy Azure oraz zasad zmiennych przezroczysty wielu interfejsów API i pracy awaryjnej. Jako ofertę bazy danych systemu [dostępności 99,99% SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db), wszystkie hello zapisy do bazy danych rozwiązania Cosmos są dyski toolocal trwale zatwierdzone przez kworum replik w obrębie centrum danych lokalnych przed potwierdzeniem toohello klienta. Należy pamiętać, że hello wysokiej dostępności rozwiązania Cosmos DB korzysta z lokalnej pamięci masowej i nie zależy od żadnych technologie magazynu zewnętrznego. Ponadto jeśli konta bazy danych jest skojarzony z więcej niż jeden region platformy Azure, programu zapisy są replikowane za pomocą innych regionów, a także. tooscale przepływności i dostępu do danych w małych opóźnień, może mieć wiele regionów skojarzonych z Twoim kontem bazy danych, według uznania w trybie odczytu. W każdym regionie odczytu dane hello (zreplikowana) trwale jest trwała dla zestawu replik.  

Jak pokazano na powitania po diagramu, jeden kontener DB rozwiązania Cosmos jest [poziomie partycjonowanej](partition-data.md). "Partycji" jest oznaczona okrąg powitania po diagramu, a każda partycja jest zyskuje dużą dostępność za pośrednictwem zestawu replik. Jest to dystrybucji lokalne powitania w pojedynczym regionie Azure (wskazywane przez hello osi X). Ponadto każda partycja (z jego odpowiedniego zestawu replik) jest globalnie dystrybuowane w różnych regionach skojarzonych z Twoim kontem bazy danych (na przykład, w tym ilustracji hello trzech regionach — wschodnie stany USA, zachodnie stany USA i Indie środkowe). "Ustaw partycji" Hello jest globalnie rozproszone jednostki składającej się z wielu kopii danych w każdym regionie (wskazywane przez osi hello Y). Można przypisać priorytet regionów toohello skojarzonych z Twoim kontem bazy danych i DB rozwiązania Cosmos będzie przezroczysty następny region toohello trybu failover w przypadku awarii. Można też ręcznie symulować trybu failover tootest hello end-to-end dostępności aplikacji.  

Witaj poniższym obrazie przedstawiono hello wysoki stopień nadmiarowość DB rozwiązania Cosmos.

![Wysoki stopień nadmiarowość DB rozwiązania Cosmos](./media/online-backup-and-restore/redundancy.png)

![Wysoki stopień nadmiarowość DB rozwiązania Cosmos](./media/online-backup-and-restore/global-distribution.png)

## <a name="full-automatic-online-backups"></a>Kopie zapasowe pełne, automatyczne, online
Niestety po usunięciu Moje kontener lub bazy danych! Rozwiązania Cosmos DB nie tylko z danych, ale hello kopie zapasowe danych są również awarii tooregional wysokiej nadmiarowe i odporność. Te automatyczne kopie zapasowe są obecnie wykonane co cztery godziny, a najnowszy 2 kopie zapasowe są przechowywane przez cały czas. Jeśli hello danych jest przypadkowo usunięty lub uszkodzony, skontaktuj [skontaktuj się z pomocą techniczną platformy Azure](https://azure.microsoft.com/support/options/) w 8 godzin. 

Hello kopii zapasowych woluminów bez wpływu na wydajność hello lub dostępności operacji w bazie danych. Rozwiązania cosmos bazy danych trwa hello kopii zapasowej w tle hello bez korzystanie z RUs elastycznie i wpływu na wydajność hello i bez wpływu na dostępność hello bazy danych. 

W przeciwieństwie do danych, która znajduje się wewnątrz rozwiązania Cosmos DB hello automatycznego tworzenia kopii zapasowych są przechowywane w usłudze magazyn obiektów Blob Azure. tooguarantee hello Niskie opóźnienie/wydajne przekazywania hello migawki kopii zapasowej jest tooan przekazane wystąpienie magazynu obiektów Blob platformy Azure, w tym samym regionie co hello bieżący obszar zapisu konta bazy danych DB rozwiązania Cosmos hello. Dla odporność regionalnej awarii każdej migawki kopii zapasowej danych w magazynie obiektów Blob Azure ponownie są replikowane za pomocą region tooanother magazynu geograficznie nadmiarowego (GRS). Witaj Poniższy diagram przedstawia hello całego kontenera DB rozwiązania Cosmos (ze wszystkich trzech partycje podstawowe w zachodnie stany USA, w tym przykładzie) kopia zapasowa jest tworzona w zdalnym konta magazynu obiektów Blob Azure w zachodnie stany USA, a następnie GRS replikowane tooEast NAS. 

Witaj poniższym obrazie przedstawiono okresowe pełne kopie zapasowe wszystkich jednostek rozwiązania Cosmos bazy danych grs w warstwie usługi Azure Storage.

![Okresowe pełne kopie zapasowe wszystkich jednostek rozwiązania Cosmos bazy danych grs w warstwie usługi Azure Storage](./media/online-backup-and-restore/automatic-backup.png)

## <a name="backup-retention-period"></a>Okres przechowywania kopii zapasowych
Zgodnie z powyższym opisem bazy danych Azure rozwiązania Cosmos przyjmuje migawki danych co cztery godziny i zachowa ostatnie dwa migawki hello każdej partycji przez 30 dni. Na naszym przepisy dotyczące zgodności migawki zostaną usunięte po 90 dniach.

Jeśli chcesz toomaintain własne migawek, można opcji tooJSON eksportu hello w hello Azure DB rozwiązania Cosmos [narzędzia migracji danych](import-data.md#export-to-json-file) tooschedule dodatkowych kopii zapasowych. 

## <a name="restoring-a-database-from-an-online-backup"></a>Przywracanie bazy danych z kopii zapasowej online
Jeśli został przypadkowo usunięty z bazy danych lub kolekcji, możesz [pliku biletu pomocy technicznej](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) lub [z działem pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) toorestore hello dane z ostatnich automatyczne kopie zapasowe hello. Jeśli potrzebujesz toorestore bazy danych z powodu problemu z uszkodzenie danych, zobacz [obsługi uszkodzenie danych](#handling-data-corruption) zgodnie z potrzebami tootake dodatkowe kroki tooprevent hello uszkodzone dane z penetrującymi hello kopii zapasowych. Określoną migawkę z kopii zapasowej toobe przywrócić DB rozwiązania Cosmos wymaga hello danych był dostępny na czas trwania hello hello cyklu tworzenia kopii zapasowych dla tej migawki.

## <a name="handling-data-corruption"></a>Obsługa uszkodzenie danych
Azure DB rozwiązania Cosmos zachowuje hello ostatnich dwóch kopii zapasowych wykonanych dla każdej partycji w systemie hello. Ten model dobrze działa przy kontenerze (kolekcję dokumentów, wykres, tabelę) lub bazy danych zostaną przypadkowo usunięte od czasu ostatniej wersji hello mogą zostać przywrócone. Jednak w hello case, podczas gdy użytkownicy mogą wprowadzać problem uszkodzenie danych, bazy danych Azure rozwiązania Cosmos może mieć świadomości hello uszkodzenie danych i możliwe, że hello uszkodzenie może mieć przejścia hello kopii zapasowych. Jak uszkodzenie zostanie wykryte, należy usunąć hello uszkodzony kontenera (kolekcji wykres/tabeli), aby tworzenie kopii zapasowych są chronione przed zastąpieniem z uszkodzone dane. Ponieważ hello ostatniej kopii zapasowej może być czterech godzin, hello użytkownika można wdrożyć [zmienić źródła](change-feed.md) toocapture i zapisać hello ostatnich czterech godzin warto danych przed usunięciem hello kontenera.

## <a name="next-steps"></a>Następne kroki

tooreplicate bazy danych w wielu centrach danych, zobacz [dystrybucji danych globalnie DB rozwiązania Cosmos](distribute-data-globally.md). 

toofile skontaktuj się z pomocą techniczną platformy Azure, [założyć zgłoszenie z portalu Azure hello](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

