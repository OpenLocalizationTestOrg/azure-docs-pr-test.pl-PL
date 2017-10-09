---
title: "aaaLearn funkcje w wersji usługi BizTalk Services | Dokumentacja firmy Microsoft"
description: "Porównano możliwości hello wersji usługi BizTalk Services hello: Zwolnij Developer, podstawowa, standardowa i Premium. MABS, WABS."
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c589629f-06b1-44bb-b8ca-1db71826ea59
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 81626fa743a7190e7c78a0fd90b3054a08982b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-editions-chart"></a>Usługa BizTalk Services: wykres wersji

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

W ramach usługi Azure BizTalk Services oferowane są różne wersje. Użyj toodetermine tego artykułu, która wersja jest odpowiednie dla Twojego scenariusza oraz o potrzebach biznesowych.

## <a name="compare-hello-editions"></a>Porównaj wersje hello
**Bezpłatna (wersja zapoznawcza)**

Można tworzyć połączenia hybrydowe i nimi zarządzać. Połączenie hybrydowe jest łatwy sposób tooconnect tooan witryny sieci Web Azure lokalnego systemu, takie jak SQL Server.

**Developer**

Obejmuje przetwarzanie komunikatów połączeń hybrydowych, EAI i EDI za pomocą prostego w obsłudze portalu zarządzania dla partnerów handlowych oraz obsługę typowych schematów EDI i dynamicznego przetwarzania EDI zgodnie z normami X12 i AS2. Można utworzyć typowe scenariusze EAI usług w chmurze hello łączności z dowolnym tooread protokołów HTTP/S, REST, FTP, usługi WCF i SFTP i pisanie wiadomości.  Korzystanie z systemów LOB lokalnych tooon łączność z kartami SAP, Oracle eBusiness bazy danych Oracle, Siebel i SQL Server gotowe do użycia. Użyj środowiska zorientowanego na dewelopera oraz narzędzi programu Visual Studio w celu łatwego programowania i wdrażania. Ograniczone toodevelopment testu celów i tylko z nie poziom Umowa dotycząca usług (SLA).

**Podstawowa**

Zawiera większość zwiększa możliwości Developer hello w połączeniach z połączeń hybrydowych było możliwe, EAI mostków umów EDI i BizTalk karty dodatkiem Service Pack. Oferuje wysoką dostępność i hello opcja tooscale z Umowa dotycząca poziomu usług (SLA).

**Standardowa**

Zawiera wszystkie funkcje podstawowe hello z zwiększa w połączeniach z połączeń hybrydowych było możliwe, EAI mostków umów EDI i BizTalk karty dodatkiem Service Pack. Oferuje wysoką dostępność i hello opcja tooscale z Umowa dotycząca poziomu usług (SLA).

**Premium**

Zawiera wszystkie funkcje standardowej hello z rośnie w połączeniach z połączeń hybrydowych było możliwe, EAI mostków umów EDI i BizTalk karty dodatkiem Service Pack. Zawiera także archiwizacji, wysokiej dostępności i hello opcja tooscale z Umowa dotycząca poziomu usług (SLA).

## <a name="editions-chart"></a>Wykres przedstawiający wersje
Witaj poniższej tabeli wymieniono różnice hello.

<table border="1">
<tr bgcolor="FAF9F9">
        <th></th>
        <th>Bezpłatna (wersja zapoznawcza)</th>
        <th>Dla deweloperów</th>
        <th>Podstawowa</th>
        <th>Standardowa</th>
        <th>Premium</th>
</tr>

<tr>
<td><strong>Cena początkowa</strong></td>
<td colspan="5"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011">Azure BizTalk Services — cennik</a> <br/><br/> <a HREF="http://azure.microsoft.com/pricing/calculator/?scenario=full">Kalkulator cen platformy Azure</a></td>
</tr>
<tr>
<td><strong>Domyślna konfiguracja minimalna</strong></td>
<td>1 jednostka bezpłatna</td>
<td>1 jednostka dla dewelopera</td>
<td>1 jednostka podstawowa</td>
<td>1 jednostka standardowa</td>
<td>1 jednostka Premium</td>
</tr>
<tr>
<td><strong>Skalowanie</strong></td>
<td>Brak skalowania</td>
<td>Brak skalowania</td>
<td>Tak, w przyrostach co 1 jednostkę podstawową</td>
<td>Tak, w przyrostach co 1 jednostkę standardową</td>
<td>Tak, w przyrostach co 1 jednostkę Premium</td>
</tr>
<tr>
<td><strong>Maksymalne dozwolone skalowanie w poziomie</strong></td>
<td>Brak skalowania</td>
<td>Brak skalowania</td>
<td>Konfiguracja too8 jednostki</td>
<td>Konfiguracja too8 jednostki</td>
<td>Konfiguracja too8 jednostki</td>
</tr>
<tr>
<td><strong>Mostki EAI na jednostkę</strong></td>
<td>Nie dołączono</td>
<td>25</td>
<td>25</td>
<td>125</td>
<td>500</td>
</tr>
<tr>
<td><strong>EDI, AS2</strong>
<br/><br/>
Zawiera umowy modułu TPM</td>
<td>Nie dołączono</td>
<td>Dołączono. 10 umów na jednostkę.</td>
<td>Dołączono. 50 umów na jednostkę.</td>
<td>Dołączono. 250 umów na jednostkę.</td>
<td>Dołączono. 1000 umów na jednostkę.</td>
</tr>
<tr>
<td><strong>Połączenia hybrydowe na jednostkę</strong></td>
<td>5</td>
<td>5</td>
<td>10</td>
<td>50</td>
<td>100</td>
</tr>
<tr>
<td><strong>Transfer danych połączenia hybrydowego (GB) na jednostkę</strong></td>
<td>5</td>
<td>5</td>
<td>50</td>
<td>250</td>
<td>500</td>
</tr>
<tr>
<td><strong>Usługa karty BizTalk połączeń lokalnych tooon LOB systemów</strong></td>
<td>Nie dołączono</td>
<td>1 połączenie</td>
<td>2 połączenia</td>
<td>5 połączeń</td>
<td>25 połączeń</td>
</tr>
<tr>
<td align="left"><strong>Obsługiwane protokoły/systemy:</strong>
<ul>
<li>HTTP</li>
<li>HTTPS</li>
<li>FTP</li>
<li>SFTP</li>
<li>WCF</li>
<li>Magistrala usług (SB)</li>
<li>Obiekt bob Azure</li>
<li>Interfejsy API REST</li>
</ul>
</td>
<td>Nie dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
</tr>
<tr>
<td><strong>Wysoka dostępność</strong>
<br/><br/>
Umowa dotycząca poziomu usług (SLA) znajduje się w artykule <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011">Usługa BizTalk — cennik</a>.
</td>
<td>Nie dołączono</td>
<td>Nie dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
</tr>
<tr>
<td><strong>Tworzenie kopii zapasowej i przywracanie</strong></td>
<td>Nie dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
</tr>
<tr>
<td><strong>Śledzenie</strong></td>
<td>Nie dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
</tr>
<tr>
<td><strong>Archiwizacja</strong><br/><br/>
Obejmuje odrzucenie bez otrzymania (NRR) i pobieranie śledzonych wiadomości</td>
<td>Nie dołączono</td>
<td>Dołączono</td>
<td>Nie dołączono</td>
<td>Nie dołączono</td>
<td>Dołączono</td>
</tr>
<tr>
<td><strong>Użycie kodu niestandardowego</strong></td>
<td>Nie dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
</tr>
<tr>
<td><strong>Użycie przekształceń, w tym niestandardowych przekształceń XSLT</strong></td>
<td>Nie dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
<td>Dołączono</td>
</tr>
</table>

> [!NOTE]
> W celu zapewnienia odporności na awarie sprzętu wysoka dostępność zakłada posiadanie wielu maszyn wirtualnych w ramach jednej jednostki BizTalk.
> 
> 

## <a name="faqs"></a>Często zadawane pytania
#### <a name="what-is-a-biztalk-unit"></a>Czym jest jednostka BizTalk?
"Jednostki" jest hello atomic poziomu wdrożenia usług BizTalk Azure. Każda wersja zawiera jednostkę o określonej wydajności obliczeniowej i pamięci. Na przykład jednostka wersji podstawowej ma większą moc obliczeniową niż jednostka wersji dla deweloperów, a jednostka wersji standardowej ma większą moc obliczeniową niż jednostka wersji podstawowej itd. Jednostka jest również miarą skalowania usługi BizTalk.

#### <a name="what-is-hello-difference-between-biztalk-services-and-azure-biztalk-vm"></a>Co to jest hello różnica między usługi BizTalk i maszyny Wirtualnej Azure BizTalk?
Usługi BizTalk Services oferuje true architektura platformy jako — usługa (PaaS) umożliwiające tworzenie rozwiązań integracji w chmurze hello. Model PaaS hello, całkowicie skupić się na logiki aplikacji hello i pozostawić wszystkie hello infrastruktury zarządzania tooMicrosoft, w tym:

* Nie konieczności toomanage lub poprawki maszyn wirtualnych.
* Firma Microsoft zapewnia dostępność.
* Możesz kontrolować skalowanie na żądanie żądając po prostu bardziej lub mniej pojemności za pośrednictwem hello portalu Azure.

Usługa BizTalk Server na maszynach wirtualnych Azure zapewnia architekturę typu infrastruktura jako usługa (IaaS). Tworzenie maszyn wirtualnych i skonfigurować je tak samo jak w lokalnym środowisku, dzięki czemu łatwiej toorun istniejące aplikacje w chmurze hello bez zmian kodu. Z IaaS możesz nadal są odpowiedzialne podczas konfigurowania hello maszyn wirtualnych i zarządzania maszynami wirtualnymi hello (na przykład zainstalować oprogramowanie i poprawek systemu operacyjnego) oraz projektowania aplikacji hello wysokiej dostępności.

Jeśli chcesz tworzyć nowe rozwiązania integracji, które zminimalizują wysiłek związany z zarządzaniem infrastrukturą, użyj usługi BizTalk Services. Jeśli szukasz tooquickly migracji istniejących rozwiązań BizTalk lub wyszukiwanie toodevelop na żądanie środowiska i testowania BizTalk Server aplikacji, użyj BizTalk Server na maszynie wirtualnej platformy Azure.

#### <a name="what-is-hello-difference-between-biztalk-adapter-service-and-hybrid-connections"></a>Co to jest hello różnica między Usługa karty BizTalk i połączenia hybrydowe?
Hello Usługa karty BizTalk jest używany przez usługę Azure BizTalk. Hello Usługa karty BizTalk używa hello BizTalk Adapter Pack tooconnect tooan lokalnego Linia biznesowych (LOB) systemu. Połączenie hybrydowe zapewnia łatwe i wygodny sposób tooconnect aplikacji Azure, takich jak hello funkcja Web Apps w usłudze Azure App Service i usługi Azure Mobile Services tooan lokalnych zasobów.

#### <a name="what-does-hybrid-connection-data-transfer-gb-per-unit-mean-is-this-per-minutehourdayweekmonth-what-happens-when-hello-limit-is-reached"></a>Co oznacza „Transfer danych połączenia hybrydowego (GB) na jednostkę”? Czy jednostka jest liczona co minutę/godzinę/dzień/tydzień/miesiąc? Co się stanie po osiągnięciu limitu hello?
Witaj połączenia hybrydowego koszt jednostkowy zależy od hello usługi BizTalk Services edition. Krótko mówiąc, koszty zależą od ilości przesyłanych danych. Na przykład transfer 10 GB danych dziennie kosztuje mniej niż transfer 100 GB danych dziennie. Użyj hello [Kalkulator cen](https://azure.microsoft.com/pricing/calculator/?scenario=full) dla usługi BizTalk Services toodetermine określonych kosztów. Zazwyczaj limity hello są wymuszane codziennie. Jeśli przekroczysz hello limit żadnych nadwyżkowe jest pobierana szybkością hello $1 na GB.

#### <a name="when-i-create-an-agreement-in-biztalk-services-why-does-hello-number-of-bridges-go-up-by-two-instead-of-just-one"></a>Podczas tworzenia umowy w usługi BizTalk, dlaczego numer hello mostków do góry przez dwa zamiast co najmniej jeden?
Każda umowa składa się z dwóch różnych mostków: mostka komunikacji po stronie wysyłania i mostka komunikacji po stronie odbierania.

#### <a name="what-happens-when-i-hit-hello-quota-limit-on-hello-number-of-bridges-or-agreements"></a>Co się stanie, gdy I osiągnęła limit przydziału hello liczby hello mostków lub umowy?
Są nie jest w stanie toodeploy żadnych nowych mostków lub utworzyć żadnych nowych umów. toodeploy więcej, należy tooscale jednostek toomore usługi BizTalk hello lub wyższą wersję tooa uaktualnienia.

#### <a name="how-do-i-migrate-from-one-tier-of-biztalk-services-tooanother"></a>Jak przeprowadzić migrację z jedną warstwę tooanother usługi BizTalk Services?
Hello bezpłatna wersja nie może być warstwy tooanother migrowanych lub "skalowalnych" i nie można utworzyć kopii i przywrócić tooanother warstwy. Inną warstwa, należy utworzyć nową usługę BizTalk przy użyciu hello nową warstwę. Wszystkie artefakty utworzone za pomocą bezpłatna wersja hello, łącznie z połączeń hybrydowych było możliwe, należy toobe odtworzone w hello nową usługę BizTalk. 

W przypadku pozostałych wersji hello należy używać hello kopii zapasowej i przywracania migracji z artefaktów z jednego tooanother warstwy. Na przykład kopię zapasową z artefaktami w hello warstwy standardowa, a następnie przywrócić je toohello warstwy Premium. [Usługi BizTalk Services: Kopia zapasowa i przywracanie](biztalk-backup-restore.md) opisano hello obsługiwane ścieżki migracji i list, jakie artefakty kopie zapasowe są tworzone. Pamiętaj, że nie tworzy się kopii zapasowej połączeń hybrydowych. Po kopii zapasowych i przywracania tooa nową warstwę, następnie odtworzyć hello połączeń hybrydowych było możliwe.  

#### <a name="is-hello-biztalk-adapter-service-included-in-hello-service-how-do-i-receive-hello-software"></a>Hello Usługa karty BizTalk znajduje się w usłudze hello? Sposób otrzymywania hello oprogramowania?
Tak, hello usługę BizTalk karty z hello BizTalk Adapter Pack są dołączone hello zestaw SDK usług BizTalk Azure [Pobierz](http://www.microsoft.com/download/details.aspx?id=39087).

## <a name="next-steps"></a>Następne kroki
usługi BizTalk Services Azure toocreate w hello Azure przejdź do portalu, zbyt[usługi BizTalk Services: Inicjowanie obsługi przy użyciu hello portalu Azure](biztalk-provision-services.md). toostart tworzenia aplikacji, przejdź do zbyt[usług BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Usługi BizTalk Services: Inicjowanie obsługi przy użyciu hello portalu Azure](biztalk-provision-services.md)<br/>
* [BizTalk Services: Provisioning Status Chart (Usługa BizTalk Services: aprowizowanie wykresu stanu)](biztalk-service-state-chart.md)<br/>
* [BizTalk Services: Dashboard, Monitor and Scale tabs (Usługa BizTalk Services: karty Pulpit nawigacyjny, Monitor i Skalowanie)](biztalk-dashboard-monitor-scale-tabs.md)<br/>
* [BizTalk Services: Backup and Restore (Usługa BizTalk Services: tworzenie kopii zapasowej i przywracanie)](biztalk-backup-restore.md)<br/>
* [BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)](biztalk-throttling-thresholds.md)<br/>
* [BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)](biztalk-issuer-name-issuer-key.md)<br/>
* [Jak mogę uruchomić przy użyciu hello Azure zestawu SDK usługi BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>

