---
title: informacje o stanie aaaRetrieving dla zadania importu/eksportu Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooobtain podać informacje dotyczące zadań usługi Import/Eksport Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 22d7e5f0-94da-49b4-a1ac-dd4c14a423c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: muralikk
ms.openlocfilehash: cbc35660519573d92f641924ac0025c9e577d69b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="retrieving-state-information-for-an-importexport-job"></a>Trwa pobieranie informacji o stanie dla zadania importu/eksportu
Możesz wywołać program hello [pobrania zadania](/rest/api/storageimportexport/jobs#Jobs_Get) operacji tooretrieve informacji o importowanie i eksportowanie zadań. Witaj zwracane są następujące informacje:

-   bieżący stan Hello hello zadania.

-   Procent przybliżonej Hello czy każde zadanie zostało zakończone.

-   Witaj bieżący stan każdego dysku.

-   Identyfikatory URI obiektów blob zawierający dzienniki błędów i pełne rejestrowanie informacji (jeśli jest włączona).

Witaj poniższe sekcje zawierają opis hello informacje zwracane przez hello `Get Job` operacji.

## <a name="job-states"></a>Stany zadania
Tabela Hello i Poniższy diagram stanu hello opisują hello stanów, które zadania przechodzi przez podczas cyklu życia. bieżący stan zadania hello Hello można ustalić przez wywołanie hello `Get Job` operacji.

![JobStates](./media/storage-import-export-retrieving-state-info-for-a-job/JobStates.png "JobStates")

Witaj poniższej tabeli opisano każdy stan zadania mogą przechodzić przez.

|Stan zadania|Opis|
|---------------|-----------------|
|`Creating`|Po wywołaj operację Put zadania hello, tworzone jest zadanie i jego stan jest ustawiony za`Creating`. Podczas zadania hello w hello `Creating` stanu hello usługi Import/Eksport zakłada hello dyski nie zostały jeszcze wysłane toohello centrum danych. Zadania mogą pozostawać na powitania `Creating` stanu dla się tootwo tygodni, po których zostanie on automatycznie usunięty przez usługę hello.<br /><br /> Jeśli wywołanie operacji właściwości zadania aktualizacji hello podczas zadania hello w hello `Creating` stanu zadania hello pozostaje w hello `Creating` stanu i hello limitu czasu interwał jest resetowania tootwo tygodni.|
|`Shipping`|Po wysyłasz do pakietu, należy wywołać hello właściwości zadania aktualizacji operację aktualizacji hello stanu zadania hello zbyt`Shipping`. Hello stanu wysyłania można ustawić tylko wtedy, gdy hello `DeliveryPackage` (operator pocztowy i numer identyfikacyjny) i hello `ReturnAddress` skonfigurowane dla zadania hello właściwości.<br /><br /> zadania Hello pozostanie w hello stan wysyłki się tootwo tygodni. Jeśli dwa tygodnie zakończonych powodzeniem i hello dyski nie zostały odebrane, Operatorzy usługi Import/Eksport hello otrzymasz powiadomienie.|
|`Received`|Po wszystkie dyski zostały odebrane w centrum danych hello, stan zadania hello zostanie ustawiona toohello stanie Received.|
|`Transferring`|Po hello dyski zostały odebrane w centrum danych hello i co najmniej jeden dysk rozpoczął przetwarzanie, stan zadania hello zostanie ustawiona toohello `Transferring` stanu. Zobacz hello `Drive States` sekcji poniżej, aby uzyskać szczegółowe informacje.|
|`Packaging`|Po zakończeniu wszystkich dysków przetwarzania, hello zadania zostaną umieszczone w hello `Packaging` stan do momentu hello dyski są wysłane toohello wstecz klienta.|
|`Completed`|Po wszystkie dyski zostały wysłane toohello wstecz klienta, jeśli hello zadanie zostało ukończone bez błędów, następnie zadania hello zostanie ustawiona toohello `Completed` stanu. Witaj zadania zostaną automatycznie usunięte po 90 dniach w hello `Completed` stanu.|
|`Closed`|Po wszystkie dyski zostały wysłane toohello wstecz klienta, jeśli pojawiły się błędy podczas przetwarzania hello hello zadania, następnie zadania hello zostanie ustawiona toohello `Closed` stanu. Witaj zadania zostaną automatycznie usunięte po 90 dniach w hello `Closed` stanu.|

Można anulować zadania tylko w określonych stanach. Anulowano zadanie pomija krok kopiowania danych hello, ale w przeciwnym razie wynika hello sam stan przejścia jako zadanie nie zostało anulowane.

Witaj poniższej tabeli opisano błędy, które mogą wystąpić na każdy stan zadania, a także hello wpływ na zadania powitania po wystąpieniu błędu.

|Stan zadania|Wydarzenie|Rozdzielczość / następne kroki|
|---------------|-----------|------------------------------|
|`Creating or Undefined`|Odebrano jeden lub więcej dysków dla zadania, ale hello zadania nie jest hello `Shipping` stanu lub nie istnieje rekord hello zadania w usłudze hello.|zespół operacyjny usługi Import/Eksport Hello będzie podejmować toocontact powitania klienta toocreate lub zaktualizować zadania hello z zadaniem hello toomove informacje niezbędne do przodu.<br /><br /> Jeśli zespół operacyjny hello toocontact powitania klienta w ciągu dwóch tygodni, zespół operacyjny hello podejmie tooreturn hello dysków.<br /><br /> W hello zdarzenia, które nie może być zwracany hello dysków i powitania klienta nie można nawiązać połączenia dyski hello będą bezpiecznie zniszczone w ciągu 90 dni.<br /><br /> Należy pamiętać, że zadania nie można przetworzyć do momentu jego stan jest aktualizowany za`Shipping`.|
|`Shipping`|Nie odebrano pakiet Hello zadania przez ponad dwa tygodnie.|zespół operacyjny Hello powiadomi powitania klienta hello brakuje pakietu. Oparte na powitania klienta odpowiedzi, zespół operacyjny hello będzie Rozszerz hello interwał toowait dla tooarrive pakietu hello albo anulować zadanie hello.<br /><br /> W przypadku hello powitania klienta nie można skontaktować się z lub nie odpowie w ciągu 30 dni, zespół operacyjny hello zainicjuje zadanie hello toomove akcji z hello `Shipping` stanu bezpośrednio toohello `Closed` stanu.|
|`Completed/Closed`|dyski Hello nigdy nie osiągnięto adres zwrotny hello lub zostały uszkodzone wydania (dotyczy tylko tooan zadanie eksportu).|Jeśli hello nie osiągną adres zwrotny hello, powitania klienta powinien pierwsza operacja pobrania zadania hello wywołania lub sprawdzania stanu zadania hello w hello portalu tooensure tego hello, które zostały wydane dysków. Jeśli hello dyski zostały wysłane, powitania klienta powinien skontaktuj się z hello wysyłanie tootry dostawcy i Znajdź hello dysków.<br /><br /> Jeśli stacje hello są uszkodzone podczas transportu, powitania klienta może być toorequest inne zadanie eksportu lub brak obiekty BLOB hello pobierania.|
|`Transferring/Packaging`|Zadanie ma nieprawidłowe lub brakujące adres zwrotny.|zespół operacyjny Hello będzie dotrzeć toohello osoby kontaktowej dla hello zadania tooobtain hello poprawny adres.<br /><br /> W przypadku powitania klienta hello jest nieosiągalny, hello dysków będą bezpiecznie zniszczone w ciągu 90 dni.|
|`Creating / Shipping/ Transferring`|Dysk, który nie ma listy hello toobe dysków zaimportowane znajduje się w hello wysyłania pakietu.|Witaj dodatkowych dysków nie będą przetwarzane i zostanie zwrócony toohello klienta po zakończeniu zadania hello.|

## <a name="drive-states"></a>Stany stacji
Hello tabeli i diagramu hello poniżej opisano hello cyklu życia poszczególnych dyskach, jako jego przejścia za pomocą zadania importu lub eksportu. Możesz pobrać bieżący stan dysku hello hello wywoływania `Get Job` hello operacji i zapoznanie się `State` element hello `DriveList` właściwości.

![DriveStates](./media/storage-import-export-retrieving-state-info-for-a-job/DriveStates.png "DriveStates")

Witaj poniższej tabeli opisano każdy stan może przekazywać dysku.

|Stan stacji|Opis|
|-----------------|-----------------|
|`Specified`|Dla zadania importu po utworzeniu zadania hello z hello operacji Put zadania hello stan początkowy dla dysku jest hello `Specified` stanu. Dla zadania eksportu, ponieważ dysk nie zostanie wskazany po utworzeniu zadania hello hello dysk początkowy stan jest hello `Received` stanu.|
|`Received`|dysk Hello przejścia toohello `Received` stanu, gdy hello operatora usługi Import/eksport został przetworzony hello dysków, które zostały odebrane z hello wysyłania firmy dla zadania importu. Dla zadania eksportu hello dysk początkowy stan jest hello `Received` stanu.|
|`NeverReceived`|dysk Hello przeniesie toohello `NeverReceived` stanu podczas hello dociera do pakietu dla zadania, ale hello pakiet nie zawiera hello dysku. Dysk można również przenosić w tym stanie, jeśli został dwa tygodnie od momentu hello usługa odebrała hello wysyłanie informacji, ale pakiet hello ma nie dotarły jeszcze w centrum danych hello.|
|`Transferring`|Dysk zostanie przesunięty toohello `Transferring` stanu, gdy hello Usługa rozpoczyna tootransfer danych z tooWindows dysku hello Azure Storage.|
|`Completed`|Dysk zostanie przesunięty toohello `Completed` stan, kiedy usługa hello pomyślnie przekazywane dane hello bez błędów.|
|`CompletedMoreInfo`|Dysk zostanie przesunięty toohello `CompletedMoreInfo` stanu toohello dysków lub gdy hello napotkała problemy podczas kopiowania danych z. informacje Hello mogą zawierać błędy, ostrzeżenia lub komunikaty informacyjne o zastępowaniu obiektów blob.|
|`ShippedBack`|dysk Hello przeniesie toohello `ShippedBack` stan, gdy została wysłana z adres zwrotny toohello wstecz centrum danych hello.|

Witaj poniższej tabeli opisano stanów awarii dysku hello i hello akcje wykonywane dla każdego stanu.

|Stan stacji|Wydarzenie|Rozdzielczość / następny krok|
|-----------------|-----------|-----------------------------|
|`NeverReceived`|Dysk, który jest oznaczony jako `NeverReceived` (ponieważ nie została odebrana jako część zadania hello wydania) dociera do innego wydania.|zespół operacyjny Hello przeniesie hello dysku toohello `Received` stanu.|
|`N/A`|Dysk, który nie jest częścią wszystkie zadania dociera hello centrum danych w ramach innego zadania.|dysk Hello zostaną oznaczone jako dodatkowy dysk i zostanie zwrócony toohello klienta po zakończeniu zadania hello skojarzonego z pakietem oryginalnego hello.|

## <a name="faulted-states"></a>Stany błędnej
W przypadku awarii tooprogress normalnie za pośrednictwem oczekiwanego cyklu życia zadania lub dysk zadania hello lub dysku zostaną przeniesione do `Faulted` stanu. W tym momencie zespół operacyjny hello skontaktuje się z powitania klienta poczty e-mail lub telefonu. Po usunięciu problemu hello hello błędny zadania lub dysku zostaną wykonane poza hello `Faulted` stanu i przeniesiony do hello odpowiednie stanu.

## <a name="next-steps"></a>Następne kroki

* [Przy użyciu interfejsu API REST usługi Import/Eksport hello](storage-import-export-using-the-rest-api.md)
