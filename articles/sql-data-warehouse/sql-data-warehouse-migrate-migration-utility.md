---
title: "Migracja: Narzędzie do migracji magazynu danych | Dokumentacja firmy Microsoft"
description: "Przeprowadź migrację tooSQL hurtowni danych."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 4d7ad981-ef31-4513-b337-50bdc4709c09
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: c89909883fb42b0b04dd87a9973e5ee3e30d8f0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-migration-utility-preview"></a>Narzędzie migracji magazynu danych (wersja zapoznawcza)
> [!div class="op_single_selector"]
> * [Pobierz narzędzie do migracji][Download Migration Utility]
> 
> 

Witaj narzędzie migracji magazynu danych jest narzędziem zaprojektowane toomigrate schemat i dane z tooAzure programu SQL Server i bazy danych SQL Azure SQL Data Warehouse. Podczas migracji schematu narzędzia hello mapuje automatycznie hello odpowiedniego schematu ze toodestination źródła. Po przeprowadzeniu migracji schematu hello hello narzędzia zawiera hello opcja toomove danych za pomocą automatycznie wygenerowanych skryptów.

Ponadto migracji danych i tooschema, to narzędzie umożliwia hello opcja toogenerate zgodności raporty, które zawierają podsumowanie niezgodności między wystąpieniami źródłowe i docelowe hello, które mogłyby uniemożliwiać Uproszczenie migracji.

## <a name="get-started"></a>Rozpoczęcie pracy
Jako warunek wstępny dla instalacji konieczne będzie skrypty migracji toorun narzędzia wiersza polecenia BCP hello i raport zgodności hello tooview pakietu Office. Po uruchomieniu hello pliku wykonywalnego, który jest pobierany można będzie tooaccept zostanie wyświetlony monit o standardowych umowy licencyjnej przed narzędzia hello zostanie zainstalowana.

Ponadto hello toorun Utiliy migracji można będzie konieczne hello jedną następujących uprawnień w bazie danych hello szukasz toomigrate: tworzenie bazy danych, ALTER DATABASE dowolnego lub wszystkich definicji WIDOKU.

### <a name="launching-hello-tool-and-connecting"></a>Uruchamianie narzędzia hello i łączenia
Uruchom narzędzie hello, klikając ikony pulpitu hello, która pojawia się po instalacji. Po otwarciu narzędzia hello, zostanie wyświetlony monit o strony początkowego połączenia, w którym można wybrać źródłowe i docelowe dla narzędzia migracji hello. W tej chwili obsługujemy programu SQL Server i bazy danych SQL Azure jako źródła i magazynu danych SQL jako miejsca docelowego. Po wybraniu to użytkownik zostanie poproszony serwera źródłowego tooyour tooconnect wypełnianie nazwy serwera i uwierzytelniania, a następnie klikając przycisk "Połącz".

Po uwierzytelnieniu narzędzia hello zostaną wyświetlone listy baz danych, które znajdują się w powitania serwera, które są połączone z. Można rozpocząć migrację hello, wybierając bazę danych, którą chcesz toomigrate i klikając wybrany migracji.

## <a name="migration-report"></a>Raport migracji
Wybieranie "Sprawdzanie zgodności bazy danych" w narzędziu hello spowoduje wygenerowanie raportu podsumowania wszystkich niezgodności obiektu w bazie danych hello żądanego toomigrate. Szerszych listę niektórych hello funkcji programu SQL Server, który nie znajduje się w magazynie danych programu SQL można znaleźć w naszych [dokumentacja dotycząca migracji][migration documentation]. Po wygenerowaniu raport hello będzie możliwe toosave i hello Otwórz raport w programie Excel.

Należy pamiętać, że podczas generowania schematu migracji hello, większość problemy zidentyfikowane jako "Object" zostanie dostosowana w kolejności tooallow natychmiastowej migracji danych. Zapoznaj się z tematem hello tooensure zmiany nie ma dodatkowych zmian toomake przed zastosowaniem hello schematu.

## <a name="migrate-schema"></a>Migrowanie schematu
Po nawiązaniu połączenia, wybierając "Schema migracji" wygeneruje skryptu migracji schematu dla hello wybrane tabele. Ta struktura skryptu porty hello tabeli hello mapuje danych niezgodne typy toomore zgodne formularzy i tworzy poświadczenia zabezpieczeń i schematu, jeśli jest to określane przez użytkownika hello hello migracji ustawień. Ten kod mogą być uruchamiane na powitania docelowe wystąpienie SQL Data Warehouse, zapisany plik tooa, skopiować do Schowka tooyour lub nawet edycji wiersza przed podjęciem dalszych działań.  

Jako powyżej, podczas migracji migracji hello Przegląd schematu zmiany tego hello zawartych w kolejności tooensure narzędzia, które należy uważnie zapoznać się je.  

## <a name="migrate-data"></a>Migrowanie danych
Klikając opcję "Dane migracji" hello mogą generować BCP skrypty, które zostanie przesunięty w pierwszym tooflat pliki danych na serwerze, a następnie bezpośrednio do magazynu danych SQL. Firma Microsoft zaleca tego procesu przenoszenia niewielkich ilości danych i jako ponownych prób nie są wbudowane i błędów mogą wystąpić w przypadku utraty połączenia sieciowego hello. W celu toorun to, konieczne będzie toohave hello BCP zainstalowane narzędzie wiersza polecenia i schematu hello hello danych musi już być utworzony.

Po wypełnieniu parametry hello powyżej możesz po prostu tooclick uruchomić migracji i zostanie utworzony zestaw dwa pakiety tooyour określonej lokalizacji. Uruchom plik eksportu hello w kolejności tooexport danych ze źródła migracji do plików prostych i uruchom plik importu hello w kolejności tooimport danych do usługi SQL Data Warehouse.

## <a name="next-steps"></a>Następne kroki
Teraz, po migracji niektórych danych, sprawdź, jak za[opracowanie][develop].

<!--Image references-->

<!--Article references-->
[migration documentation]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md

<!--Other Web references--> 
[Download Migration Utility]: https://migrhoststorage.blob.core.windows.net/sqldwsample/DataWarehouseMigrationUtility.zip
