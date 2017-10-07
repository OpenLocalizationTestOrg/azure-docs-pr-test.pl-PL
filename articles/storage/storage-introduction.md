---
title: tooAzure aaaIntroduction magazynu | Dokumentacja firmy Microsoft
description: "Omówienie usługi Azure Storage — magazynu danych w trybie online firmy Microsoft w chmurze hello. Dowiedz się, jak toouse hello najlepsze rozwiązanie magazynu w chmurze dostępnych w aplikacji."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/26/2017
ms.author: marsma
ms.openlocfilehash: dec8280c77f4b23df4c2a471e1d755e365c14e58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-storage"></a>Wprowadzenie tooMicrosoft usługi Azure Storage

## <a name="overview"></a>Omówienie
Magazyn Azure to rozwiązanie magazynu hello w chmurze dla nowoczesnych aplikacji, które polegają na trwałości, dostępności i skalowalności toomeet hello potrzeb klientów. Ten artykuł, przeznaczony dla deweloperów, specjalistów IT i osób podejmujących decyzje biznesowe, zawiera następujące informacje:

* Co to jest usługa Azure Storage i jak można ją wykorzystać w aplikacjach w chmurze, mobilnych, serwerowych i klasycznych
* Jakiego rodzaju dane można przechowywać z usług Azure Storage hello: obiektu blob danych (obiekt), dane tabel NoSQL, komunikaty w kolejkach i udziały plików.
* Sposób zarządzania dane tooyour dostępu w usłudze Azure Storage
* Jak jest zapewniana trwałość danych usługi Azure Storage za pomocą nadmiarowości i replikacji
* Gdzie toobuild dalej toogo swoją pierwszą aplikację usługi Azure Storage

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!-- tooget up and running with Azure Storage quickly, see [Get started with Azure Storage in five minutes](storage-getting-started-guide.md). -->

Aby uzyskać szczegółowe informacje dotyczące narzędzi, bibliotek i innych zasobów dotyczących pracy z usługą Azure Storage, zobacz [Następne kroki](#next-steps) poniżej.

## <a name="what-is-azure-storage"></a>Co to jest Azure Storage?
Obliczenia w chmurze umożliwiają użycie nowych scenariuszy w aplikacjach wymagających skalowalnego i trwałego magazynu o wysokiej dostępności dla danych — dlatego firma Microsoft opracowała usługę Azure Storage. W toomaking dodanie go możliwe dla deweloperów toobuild aplikacji na dużą skalę toosupport nowych scenariuszy, Azure Storage stanowi również podstawowy magazyn hello maszyn wirtualnych platformy Azure, dalsze niezawodności tooits dowód.

Usługa Azure Storage jest skalowalna na ogromną skalę, więc można przechowywać i przetwarzać setki terabajtów danych toosupport hello danych big data scenariusze analizy naukowych, finansowych i aplikacji. Możesz także przechowywać hello niewielkich ilości danych wymagane dla małych firm witryny sieci Web. Gdy Twoje potrzeby zmniejszą, płacisz tylko za hello dane, które są przechowywane. Obecnie Magazyn Azure przechowuje dziesiątki bilionów unikatowych obiektów klienckich i obsługuje średnio miliony żądań na sekundę.

Magazyn Azure to elastyczna, dzięki czemu projektowanie aplikacji dla dużych odbiorców globalnych i skalować je w miarę potrzeb — zarówno hello ilości przechowywanych danych i hello liczby żądań ich dotyczących. Płacisz tylko za to, czego używasz, i tylko wtedy, gdy tego używasz.

Usługa Azure Storage korzysta z systemu automatycznego partycjonowania, który automatycznie równoważy obciążenie danymi na podstawie ruchu. Oznacza to, że wymaga hello na wzrostu potrzeb aplikacji, Magazyn Azure automatycznie przydzieli toomeet odpowiednie zasoby hello je.

Usługa Azure Storage jest dostępna z dowolnego miejsca Witaj świecie, z dowolnego typu aplikacji, czy jest uruchomiona w chmurze hello, na pulpicie hello, na serwerze lokalnym lub telefonu komórkowego lub tabletu urządzenia. Można użyć usługi Azure Storage w scenariuszach mobilnych, gdzie aplikacja hello przechowuje podzbiór danych na urządzeniu hello i synchronizuje je z pełnym zbiorem danych przechowywanych w chmurze hello.

Usługa Azure Storage obsługuje klientów używających różnorodnych systemów operacyjnych (w tym Windows i Linux) i różnych języków programowania (w tym .NET, Java, Node.js, Python, Ruby, PHP, C++ i języki programowania zastosowań mobilnych), co umożliwia wygodne opracowywanie. Usługa Azure Storage uwidacznia również zasoby danych za pośrednictwem prostych interfejsów API REST, które są dostępne tooany klient może wysyłać i odbierać dane za pośrednictwem protokołu HTTP/HTTPS.

Usługa Azure Premium Storage oferuje obsługę dysków o wysokiej wydajności i małych opóźnieniach na potrzeby obciążeń intensywnie korzystających z operacji we/wy, które są uruchomione w usłudze Azure Virtual Machines. Usługa Azure Premium Storage, można dołączyć wielu trwałych danych dysków tooa maszyny wirtualnej i skonfigurować je toomeet wymagań dotyczących wydajności. Każdy dysk danych jest wspierany przez dysk SSD w usłudze Azure Premium Storage w celu zapewnienia maksymalnej wydajności operacji we/wy. Zobacz [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md) (Premium Storage: usługa Storage o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure), aby uzyskać szczegółowe informacje.

## <a name="introducing-hello-azure-storage-services"></a>Wprowadzenie do usługi Azure Storage hello
Usługa Azure storage udostępnia następujące cztery usługi hello: obiektu Blob magazynu, Magazyn tabel, magazyn kolejek i magazyn plików.

* Usługa Blob Storage przechowuje dane obiektów bez struktury. Obiekt blob może być dowolnymi danymi tekstowymi lub binarnymi, takimi jak dokument, plik multimedialny lub instalator aplikacji. Magazyn obiektów blob jest również tooas określonego obiektu magazynu.
* Usługa Table Storage przechowuje zestawy danych ze strukturą. Magazyn tabel jest magazynem danych pary klucz atrybut NoSQL, co umożliwia szybkie opracowywanie i szybki dostęp toolarge ilości danych.
* Usługa Queue Storage umożliwia niezawodną obsługę komunikatów na potrzeby przetwarzania przepływu pracy i komunikacji między składnikami usług w chmurze.
* Magazyn plików oferuje współużytkowany magazyn dla starszych aplikacji używających standardowego protokołu SMB hello. Maszyny wirtualne platformy Azure i usługi w chmurze mogą udostępniać dane między składnikami aplikacji za pośrednictwem zainstalowanych udziałów i lokalnych aplikacji można uzyskać dostępu do danych plików w udziale za pomocą hello interfejsu API REST usługi plików.

Konto usługi Azure storage to bezpieczne konto, które umożliwia dostęp do tooservices w usłudze Azure Storage. Konto magazynu zapewnia unikatową przestrzeń nazw powitania dla zasobów magazynu. Obraz powitania poniżej przedstawia hello relacje między zasobami magazynu platformy Azure hello na koncie magazynu:

![Zasoby usługi Azure Storage](./media/storage-introduction/storage-concepts.png)

[!INCLUDE [storage-account-types-include](../../includes/storage-account-types-include.md)]

[!INCLUDE [storage-versions-include](../../includes/storage-versions-include.md)]

## <a name="blob-storage"></a>Blob Storage
Użytkownicy z dużą ilością toostore danych obiektów niestrukturalnych w chmurze hello magazynu obiektów Blob oferuje ekonomiczne i skalowalne rozwiązanie. Można użyć obiektu Blob magazynu toostore zawartości, takich jak:

* Dokumenty
* Dane społecznościowe takie jak zdjęcia, wideo, muzyka i blogi
* Kopie zapasowe plików, komputerów, baz danych i urządzeń
* Obrazy i tekst dla aplikacji sieci Web
* Dane konfiguracji dla aplikacji w chmurze
* Dane big data takie jak dzienniki i inne duże zestawy danych

Każdy obiekt blob znajduje się w kontenerze. Kontenery również zapewnić wygodny sposób tooassign zabezpieczeń zasad toogroups obiektów. Konto magazynu może zawierać dowolną liczbę kontenerów, a kontener może zawierać dowolną liczbę obiektów blob w górę toohello 500 TB limitu pojemności konta magazynu hello.

Magazyn obiektów blob udostępnia trzy typy obiektów blob: blokowe obiekty blob, uzupełnialne obiekty blob i stronicowe obiekty blob (dyski).

* Blokowe obiekty blob są zoptymalizowane pod kątem przesyłania strumieniowego i przechowywania obiektów w chmurze i dobrze nadają się do przechowywania dokumentów, plików multimedialnych, kopii zapasowych itd.
* Dołącz obiekty BLOB są podobne tooblock obiektów blob, lecz są zoptymalizowane pod kątem operacji dołączania. Uzupełnialny obiekt blob można zaktualizować tylko przez dodanie nowego celu toohello bloku. Dołącz obiekty BLOB są dobrym rozwiązaniem w przypadku scenariuszy, takich jak rejestrowanie, gdy nowe dane musi toobe zapisywane tylko toohello koniec hello obiektu blob.
* Stronicowe obiekty BLOB są zoptymalizowane pod kątem reprezentowania dysków IaaS i obsługi losowych zapisuje i może być aktywne TB too1 rozmiar. Dysk IaaS dołączony do sieci maszyny wirtualnej platformy Azure to plik VHD przechowywany jako stronicowy obiekt blob.

Dla bardzo dużych zestawów danych, gdy ograniczenia sieci uniemożliwić przekazanie lub pobranie tooBlob pamięci masowej w wypadku przewodowy hello możesz wysłać tooimport tooMicrosoft dysk twardy lub wyeksportować dane bezpośrednio z centrum danych hello. Zobacz [Użyj hello usługi Import/Eksport Microsoft Azure tooTransfer danych tooBlob magazynu](storage-import-export-service.md).

## <a name="table-storage"></a>Magazyn tabel

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Nowoczesne aplikacje często wymagają magazynu, który jest bardziej skalowalny i elastyczny, niż określają to wymagania poprzedniej generacji oprogramowania. Magazyn tabel oferuje magazynu wysokiej dostępności, skalowalna na ogromną skalę, dzięki czemu aplikacja może automatycznie skalować toomeet żądanie użytkownika. Usługa Table Storage to magazyn typu NoSQL (par klucz-atrybut) firmy Microsoft — nie korzysta ze schematów, czym różni się od tradycyjnych relacyjnych baz danych. Z magazynem danych schematu jest łatwe tooadapt dane jako hello wymagają aplikacji. Magazyn tabel jest łatwy toouse, więc deweloperzy mogą szybko tworzyć aplikacje. Toodata dostępu jest szybki i ekonomiczny dla wszystkich rodzajów aplikacji.  Magazyn tabel jest zwykle znacznie tańszy niż tradycyjne bazy SQL dla podobnych ilości danych.

Magazyn tabel to magazyn zawierający pary klucz-atrybut, co oznacza, że każda wartość w tabeli jest przechowywana razem z nazwą właściwości z określonym typem. Nazwa właściwości Hello może służyć do filtrowania i określania kryteriów wyboru. Kolekcja właściwości i ich wartości stanowi jednostkę. Ponieważ Magazyn tabel nie korzysta ze schematów, dwie jednostki w hello sama tabela może zawierać różne kolekcje właściwości i te właściwości mogą być różnych typów.

Korzystając z tabeli magazynu toostore elastycznych zestawów danych, takich jak dane użytkownika dla aplikacji sieci web, książki adresowe, informacje o urządzeniach i inne rodzaje metadanych, których wymaga Twoja usługa.  W tabeli można przechowywać dowolną liczbę jednostek, a konto magazynu może zawierać dowolną liczbę tabel w górę toohello limitu pojemności konta magazynu hello.

Podobnie jak obiekty BLOB i kolejek deweloperzy można zarządzać, a dostęp do magazynu tabel za pomocą standardowych protokołów REST, jednak tabeli magazynu również obsługuje podzbiór protokołu OData hello, co upraszcza zaawansowanych możliwości zapytań i JSON i AtomPub (oparte na języku XML) formaty.

Dla współczesnych aplikacji internetowych bazy danych NoSQL, takie jak magazyn tabel oferują popularnych tootraditional alternatywnych relacyjnych baz danych.

## <a name="queue-storage"></a>Queue Storage
W przypadku projektowania aplikacji pod kątem skalowania składniki aplikacji są często rozłączane, dzięki czemu mogą być skalowane niezależnie. Magazyn kolejek zapewnia niezawodne rozwiązanie do obsługi komunikatów dla komunikacji asynchronicznej między składnikami aplikacji, czy działają w chmurze hello, hello pulpitu, na serwerze lokalnym lub na urządzeniu przenośnym. Magazyn kolejek obsługuje również zarządzanie asynchronicznymi zadaniami oraz przepływy pracy procesu kompilacji.

Konto magazynu może zawierać dowolną liczbę kolejek. Kolejka może zawierać dowolną liczbę komunikatów w górę toohello limitu pojemności konta magazynu hello. Poszczególne wiadomości mogą mieć się o rozmiarze too64 KB.

## <a name="file-storage"></a>File Storage
Witaj usługi pliki Azure umożliwia tooset zapasowej udziałów plików sieciowych wysokiej dostępności, które są dostępne przy użyciu standardowego protokołu bloku komunikatów serwera (SMB) hello. Oznacza, że wiele maszyn wirtualnych można udostępniać hello same pliki z odczytu i zapisu. Możesz przeczytać hello plików przy użyciu interfejsu REST hello lub bibliotek klienckich magazynu hello.

Rzecz, która odróżnia magazyn plików Azure z plików w udziale plików firmowych jest, że masz dostęp hello plików z dowolnego miejsca w Witaj świecie przy użyciu adresu URL, który wskazuje plik toohello i zawiera token sygnatury dostępu Współdzielonego dostępu współdzielonego. Można generować tokeny sygnatury dostępu Współdzielonego; umożliwiają one zasobów prywatnej tooa określonym dostępu dla określonego przedziału czasu.

Udziałów plików można używać w wielu typowych scenariuszach:

* Wiele aplikacji lokalnych korzysta z udziałów plików. Ta funkcja umożliwia łatwiejsze toomigrate tych aplikacji, które mają tooAzure danych. W przypadku instalowania hello sama litera który hello toohello udziału pliku lokalnego aplikacja używa, hello część aplikacji, który uzyskuje dostęp do udziału plików hello powinien współpracować z minimalne ewentualne zmiany.

* Pliki konfiguracji można przechowywać w udziale plików i uzyskiwać do nich dostęp z wielu maszyn wirtualnych. Narzędzi używanych przez wielu deweloperów w grupie mogą być przechowywane w udziale plików, zapewniając, że każdy można je znaleźć, i że używają one hello tej samej wersji.

* Dzienniki diagnostyczne, metryki i zrzuty awaryjne są tylko trzy przykłady, danych, które jest zapisywane tooa udziału plików i przetwarzany lub przeanalizowane później.

W tym czasie, uwierzytelnianie oparte na usłudze Active Directory i dostępu formantu listy (kontroli dostępu ACL) nie są obsługiwane, ale będzie na pewien czas w przyszłości hello. poświadczenia konta magazynu Hello są używane tooprovide uwierzytelniania dla udziału plików toohello dostępu. Oznacza to, każdy z udziałem hello zainstalowane będzie miał pełne odczytu/zapisu dostępu toohello udziału.

## <a name="access-tooblob-table-queue-and-file-resources"></a>TooBlob dostępu, tabeli, kolejki i plików zasobów
Domyślnie tylko hello właściciel konta magazynu można uzyskiwać dostęp do zasobów na koncie magazynu hello. Dla bezpieczeństwa hello danych musi zostać uwierzytelniony każde żądanie dotyczące zasobów na koncie. Uwierzytelnianie jest oparte na modelu klucza wspólnego. Obiekty BLOB może być również skonfigurowany toosupport uwierzytelnianie anonimowe.

Do Twojego konta magazynu podczas jego tworzenia są przypisywane dwa prywatne klucze dostępu, które są używane do uwierzytelniania. Dwa klucze gwarantuje, aplikacja pozostaje dostępna, gdy regularnie ponownego generowania kluczy hello jako popularną praktyką zarządzania kluczami zabezpieczeń.

Jeśli potrzebujesz zasobów magazynu tooyour tooallow użytkowników pod kontrolą dostępu, można utworzyć sygnatury dostępu współdzielonego. Sygnatury dostępu współdzielonego (SAS) to token, który może być dołączany tooa adres URL czy umożliwia delegowane zasobów magazynu tooa dostępu. Każdy, kto posiada hello token dostęp do zasobów hello wskazuje toowith hello uprawnienia, które on określa, hello okres czasu, że jest prawidłowy. Począwszy od wersji 2015-04-05, usługa Azure Storage obsługuje dwa rodzaje sygnatur dostępu współdzielonego: usługi i konta.

Obiekty delegowane sygnatury dostępu Współdzielonego usługi Hello dostępu tooa zasobu tylko w jednej z usług magazynu hello: hello usługi obiektów Blob, kolejki, tabeli lub pliku.

Sygnatura dostępu Współdzielonego konta deleguje dostęp tooresources w co najmniej jednej usługi magazynu hello. Możesz delegować operacji tooservice poziom dostępu, które nie są dostępne z sygnatury dostępu Współdzielonego usługi. Możesz również delegować dostęp tooread, zapisu i operacji usuwania kontenerów obiektów blob, tabel, kolejek i udziałów plików, które nie są dozwolone z sygnatury dostępu Współdzielonego usługi.

Istnieje także możliwość określenia kontenera i jego obiektów blob lub konkretnego obiektu blob jako dostępnego publicznie. Po wskazaniu, że kontener lub obiekt blob jest publiczny, dowolny użytkownik może go anonimowo odczytać — uwierzytelnianie nie jest wymagane.  Publiczne kontenery i obiekty blob są przydatne w wypadku ujawniania zasobów takich jak multimedia i dokumenty hostowane w witrynach sieci Web.  toodecrease opóźnienia sieciowe dla odbiorców globalnych, można buforować dane obiektów blob używane przez witryny sieci Web z hello Azure CDN.

Zobacz [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) (Używanie sygnatur dostępu współdzielonego), aby uzyskać więcej informacji o sygnaturach dostępu współdzielonego. Zobacz [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiekty BLOB](storage-manage-access-to-resources.md) i [uwierzytelniania dla usług magazynu Azure hello](https://msdn.microsoft.com/library/azure/dd179428.aspx) Aby uzyskać więcej informacji na koncie magazynu tooyour bezpiecznego dostępu.

## <a name="replication-for-durability-and-high-availability"></a>Replikacja na potrzeby trwałości i wysokiej dostępności
Witaj danych platformy Microsoft Azure konto magazynu jest zawsze replikowane tooensure trwałości i wysokiej dostępności. Witaj danych, w tym samym centrum danych lub tooa drugi centrum danych, w zależności od opcji replikacji wybierz kopie replikacji. Replikacja chroni dane i zachowuje Twojej aplikacji czasu w przypadku hello przejściowych awarii sprzętu. Jeśli dane są replikowane tooa drugi centrum danych, również chroni dane przed poważnej awarii w lokalizacji głównej hello.

Replikacja zapewnia, że Twoje konto magazynu ma spełnia hello [Umowa dotycząca poziomu usług (SLA) dla magazynu](https://azure.microsoft.com/support/legal/sla/storage/) nawet w fazie hello błędów. Zobacz hello umowy dotyczącej poziomu usług, aby uzyskać informacje na temat usługi Azure Storage zapewnia trwałość i dostępność.

Podczas tworzenia konta magazynu, możesz wybrać następujące opcje replikacji hello:

* **Magazyn lokalnie nadmiarowy (LRS).** Magazyn lokalnie nadmiarowy przechowuje trzy kopie danych. Magazyn LRS jest replikowany trzy razy w jednym centrum danych w pojedynczym regionie. Magazyn LRS chroni dane przed zwykłymi awariami sprzętu, ale nie z hello awarii jednego centrum danych.

    Magazyn LRS jest oferowany z rabatem. Aby uzyskać maksymalną trwałość, zalecamy użycie magazynu geograficznie nadmiarowego opisanego poniżej.
* **Magazyn strefowo nadmiarowy (ZRS).** Magazyn strefowo nadmiarowy przechowuje trzy kopie danych. Magazyn ZRS jest replikowany trzykrotnie w ramach dwóch toothree urządzeń, w jednym lub dwóch regionach, zapewniając większą trwałość niż magazyn LRS. Magazyn ZRS zapewnia, że dane są trwałe w pojedynczym regionie.

    Magazyn ZRS zapewnia wyższy poziom trwałości niż magazyn LRS, jednak w celu osiągnięcia maksymalnej trwałości zalecamy użycie magazynu geograficznie nadmiarowego opisanego poniżej.

  > [!NOTE]
  > Magazyn ZRS jest obecnie dostępny tylko dla blokowych obiektów blob i tylko dla wersji 2014-02-14 i nowszych.
  >
  > Po utworzeniu konta magazynu i wybraniu magazynu ZRS nie można przekonwertować go toouse tooany innego typu replikacji lub na odwrót.
  >
  >
* **Magazyn geograficznie nadmiarowy (GRS)**. Magazyn GRS przechowuje sześć kopii danych. W wypadku magazynu GRS dane są replikowane trzy razy w regionie podstawowym hello i są replikowane trzy razy w regionie pomocniczym setki odległości od regionu podstawowego hello, zapewniając hello najwyższy poziom trwałości. W przypadku hello awaria w regionie podstawowym hello usługa Azure Storage przejdzie region pomocniczy toohello trybu failover. Magazyn GRS zapewnia, że dane są trwałe w dwóch oddzielnych regionach.

    Informacje o parach podstawowych i dodatkowych według regionów można znaleźć w temacie [Regiony platformy Azure](https://azure.microsoft.com/regions/).
* **Magazyn geograficznie nadmiarowy dostępny do odczytu (RA-GRS)**. Dostęp do odczytu magazynu geograficznie nadmiarowego replikuje Twoje dane tooa dodatkowej lokalizacji geograficznej, a także zapewnia dostęp do odczytu tooyour danych w dodatkowej lokalizacji hello. Dostęp do odczytu magazynu geograficznie nadmiarowego umożliwia tooaccess danych z hello podstawowej lub dodatkowej lokalizacji hello w zdarzeniu hello niedostępny jednej lokalizacji. Dostęp do odczytu magazynu geograficznie nadmiarowego jest domyślną opcją hello konta magazynu, domyślnie podczas jego tworzenia.

  > [!IMPORTANT]
  > Możesz zmienić sposób replikacji danych po utworzeniu konta magazynu, o ile nie określono ZRS, podczas tworzenia konta hello. Jednak należy pamiętać, że może pociągnąć za sobą dodatkowe jednorazowo koszty transferu danych po przełączeniu z LRS tooGRS lub RA-GRS.
  >
  >

Aby uzyskać szczegółowe informacje na temat opcji replikacji magazynu, zobacz [Replikacja usługi Azure Storage](storage-redundancy.md).

Aby uzyskać informacje o cenniku replikacji konta magazynu, zobacz [Cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/). Aby uzyskać więcej informacji na temat dostępności usług w poszczególnych regionach, zobacz temat [Regiony świadczenia usługi Azure](https://azure.microsoft.com/regions/#services).

Aby uzyskać szczegółowe informacje o trwałości w usłudze Azure Storage, zobacz [SOSP Paper - Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx) (Dokument SOSP — Azure Storage: usługa magazynu w chmurze o wysokiej dostępności z dużą trwałością).

## <a name="transferring-data-tooand-from-azure-storage"></a>Transfer danych tooand z usługi Azure Storage
W ramach konta magazynu lub wielu kont magazynu, można użyć blob toocopy narzędzia wiersza polecenia AzCopy hello, plików i danych z tabeli. Zobacz [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md) Aby uzyskać więcej informacji.

Narzędzie AzCopy jest oparty na powitania [Biblioteka przenoszenia danych Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), która jest aktualnie dostępna w wersji zapoznawczej.

Hello usługi Import/Eksport Azure udostępnia sposób tooimport obiektu blob danych do lub wyeksportowanie danych obiektów blob z konta magazynu za pomocą dysku twardego przesłanego pocztą toohello centrum danych Azure. Aby uzyskać więcej informacji na temat hello usługi Import/eksport, zobacz [Użyj hello usługi Import/Eksport Microsoft Azure tooTransfer danych tooBlob magazynu](storage-import-export-service.md).

## <a name="pricing"></a>Cennik
[!INCLUDE [storage-account-billing-include](../../includes/storage-account-billing-include.md)]

## <a name="storage-apis-libraries-and-tools"></a>Narzędzia, biblioteki oraz interfejsy API usługi Storage
Zasoby usługi Azure Storage są dostępne za pomocą dowolnego języka, który obsługuje żądania HTTP/HTTPS. Dodatkowo Magazyn Azure oferuje biblioteki programistyczne dla kilku popularnych języków. Te biblioteki upraszczają wiele aspektów pracy z Magazynem Azure, obsługując szczegóły takie jak wywołania synchroniczne i asynchroniczne, przetwarzanie wsadowe operacji, zarządzanie wyjątkami, automatyczne ponawianie, zachowania podczas działania itd. Biblioteki są obecnie dostępne dla następujących języków hello i platform, a kolejne hello potoku:

### <a name="azure-storage-data-services"></a>Usługi danych usługi Azure Storage
* [Interfejs API REST usług Storage](http://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Biblioteka klienta usługi Storage dla platformy .NET, systemu Windows Phone i środowiska uruchomieniowego systemu Windows](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Biblioteka klienta usługi Storage dla języka C++](https://github.com/Azure/azure-storage-cpp)
* [Biblioteka klienta usługi Storage dla języka Java w systemie Android](https://azure.microsoft.com/develop/java/)
* [Biblioteka klienta usługi Storage dla oprogramowania Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Biblioteka klienta usługi Storage dla języka PHP](https://azure.microsoft.com/develop/php/)
* [Biblioteka klienta usługi Storage dla języka Ruby](https://azure.microsoft.com/develop/ruby/)
* [Biblioteka klienta usługi Storage dla języka Python](https://azure.microsoft.com/develop/python/)
* [Polecenia cmdlet usługi Storage dla programu PowerShell 1.0](/powershell/module/azurerm.storage/#storage)

### <a name="azure-storage-management-services"></a>Usługi zarządzania usługi Azure Storage
* [Dokumentacja interfejsu API REST dostawcy zasobów usługi Storage](/rest/api/storagerp/)
* [Biblioteka klienta dostawcy zasobów usługi Storage dla platformy .NET](/dotnet/api/microsoft.azure.management.storage)
* [Polecenia cmdlet dostawcy zasobów usługi Storage dla programu PowerShell 1.0](/powershell/module/azure.storage)
* [Interfejs API REST zarządzania usługą Storage (klasyczny)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### <a name="azure-storage-data-movement-services"></a>Usługi przenoszenia danych usługi Azure Storage
* [Interfejs API REST usługi Import/Eksport usługi Storage](storage-import-export-service.md)
* [Biblioteka klienta przenoszenia danych usługi Storage dla platformy .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### <a name="tools-and-utilities"></a>Narzędzia i programy narzędziowe
* [Eksplorator magazynu Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) jest bezpłatna, aplikacja autonomiczny firmy Microsoft, który umożliwia toowork wizualnie z danymi usługi Azure Storage w systemie Windows, macOS i Linux.
* [Azure Storage Client Tools](storage-explorers.md)
* [Zestawy SDK i narzędzia platformy Azure](https://azure.microsoft.com/tools/)
* [Azure Storage Emulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [Narzędzie wiersza polecenia AzCopy](http://aka.ms/downloadazcopy)

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat usługi Azure Storage, zapoznaj się z tymi zasobami:

### <a name="documentation"></a>Dokumentacja
* [Dokumentacja usługi Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Tworzenie konta magazynu](storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>Dla administratorów
* [Używanie programu Azure PowerShell z usługą Azure Storage](storage-powershell-guide-full.md)
* [Używanie interfejsu wiersza polecenia platformy Azure z usługą Azure Storage](storage-azure-cli.md)

### <a name="for-net-developers"></a>Dla deweloperów .NET
* [Rozpoczynanie pracy z usługą Azure Blob Storage przy użyciu platformy .NET](storage-dotnet-how-to-use-blobs.md)
* [Rozpoczynanie pracy z usługą Azure Table Storage przy użyciu platformy .NET](storage-dotnet-how-to-use-tables.md)
* [Rozpoczynanie pracy z usługą Azure Queue Storage przy użyciu platformy .NET](storage-dotnet-how-to-use-queues.md)
* [Rozpoczynanie pracy z usługą Azure File Storage w systemie Windows](storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Dla deweloperów języka Java w systemie Android
* [Jak toouse magazynu obiektów Blob w języku Java](storage-java-how-to-use-blob-storage.md)
* [Jak toouse magazynu tabel w języku Java](storage-java-how-to-use-table-storage.md)
* [Jak toouse magazynu kolejek w języku Java](storage-java-how-to-use-queue-storage.md)
* [Jak toouse magazyn plików za pomocą języka Java](storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Dla deweloperów oprogramowania Node.js
* [Jak toouse magazynu obiektów Blob w oprogramowaniu Node.js](storage-nodejs-how-to-use-blob-storage.md)
* [Jak toouse magazynu tabel w oprogramowaniu Node.js](storage-nodejs-how-to-use-table-storage.md)
* [Jak toouse magazynu kolejek w oprogramowaniu Node.js](storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>Dla deweloperów języka PHP
* [Jak toouse magazynu obiektów Blob w języku PHP](storage-php-how-to-use-blobs.md)
* [Jak toouse magazynu tabel w języku PHP](storage-php-how-to-use-table-storage.md)
* [Jak toouse magazynu kolejek w języku PHP](storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Dla deweloperów języka Ruby
* [Jak toouse magazynu obiektów Blob w języku Ruby](storage-ruby-how-to-use-blob-storage.md)
* [Jak toouse magazynu tabel w języku Ruby](storage-ruby-how-to-use-table-storage.md)
* [Jak toouse magazynu kolejek w języku Ruby](storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Dla deweloperów języka Python
* [Jak toouse magazynu obiektów Blob w języku Python](storage-python-how-to-use-blob-storage.md)
* [Jak toouse magazynu tabel w języku Python](storage-python-how-to-use-table-storage.md)
* [Jak toouse magazynu kolejek w języku Python](storage-python-how-to-use-queue-storage.md)
* [Jak toouse magazynu plików w języku Python](storage-python-how-to-use-file-storage.md)
