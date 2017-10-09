---
title: "aaaOverview partii zadań Azure dla deweloperów | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej funkcji hello hello usługa partia zadań i jej interfejsów API z punktu widzenia rozwoju."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 416b95f8-2d7b-4111-8012-679b0f60d204
ms.service: batch
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3da9d82572b28d05d1923166bd08c26725ca3316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-large-scale-parallel-compute-solutions-with-batch"></a>Tworzenie rozbudowanych rozwiązań przetwarzania równoległego przy użyciu usługi Batch

W tym omówieniu hello podstawowe składniki usługi partia zadań Azure hello omówiono funkcje podstawowa usługa hello i że partii deweloperzy mogą używać równolegle na dużą skalę toobuild zasoby obliczeniowe rozwiązania.

Czy tworzony jest aplikacja rozproszona obliczeniową lub usługi, która wystawia bezpośredniego [interfejsu API REST] [ batch_rest_api] wywołania lub korzystania z jednego z hello [wsadowego zestawów SDK](batch-apis-tools.md#azure-accounts-for-batch-development), użyjesz wiele zasobów hello i funkcje omówione w tym artykule.

> [!TIP]
> Dla wyższego poziomu wprowadzenie toohello usługa partia zadań, zobacz [podstawy Azure partii](batch-technical-overview.md).
>
>

## <a name="batch-service-workflow"></a>Przepływ pracy usługi Batch
Witaj poniższy ogólny przepływ pracy jest typowe dla prawie wszystkich aplikacji i usług korzystających z usługi partia zadań hello przetwarzania równoległego obciążeń:

1. Przekaż hello **pliki danych** , które mają tooprocess tooan [usługi Azure Storage] [ azure_storage] konta. Wsadowe ma wbudowaną funkcję obsługi do uzyskiwania dostępu do magazynu obiektów Blob platformy Azure i zadań można takie pliki należy pobierać za[węzły obliczeniowe](#compute-node) uruchamiania zadań hello.
2. Przekaż hello **pliki aplikacji** uruchomienia zadania. Te pliki mogą być pliki binarne lub skryptów oraz ich zależności i są wykonywane przez zadania hello w zadaniach. Zadania mogą pobrać pliki z konta magazynu lub skorzystać z hello [pakietów aplikacji](#application-packages) funkcji partii Zarządzanie aplikacjami i wdrażania.
3. Utwórz [pulę](#pool) węzłów obliczeniowych. Po utworzeniu puli można określić numer hello węzłów obliczeniowych w puli hello, rozmiar i hello systemu operacyjnego. Po uruchomieniu każdego zadania, w którym zadanie jest przypisany tooexecute w jednym z węzłów hello w puli.
4. Utwórz [zadanie](#job). Zadanie umożliwia zarządzanie kolekcją zadań podrzędnych. Możesz skojarzyć poszczególnych zadania tooa określonych pul którym to zadanie zadania będą uruchamiane.
5. Dodaj [zadania](#task) toohello zadania. Każde zadanie uruchamia aplikacji hello lub skrypt, który został przekazany tooprocess hello danych plików, które pobiera z konta magazynu. Jak każdego zadania zakończeniu go przekazać tooAzure jego dane wyjściowe magazynu.
6. Monitorowanie postępu zadania i pobrać dane wyjściowe zadania hello z usługi Magazyn Azure.

Witaj poniższe sekcje omówienia i hello inne zasoby partii, umożliwiających rozproszonej scenariusz obliczeniową.

> [!NOTE]
> Należy [konto wsadowe](#account) hello toouse usługa partia zadań. W wielu rozwiązaniach do przechowywania i pobierania plików jest używane konto usługi [Azure Storage][azure_storage]. Wsadowe aktualnie obsługuje tylko hello **ogólnego przeznaczenia** typu konta magazynu, zgodnie z opisem w kroku 5 [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) w [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).
>
>

## <a name="batch-service-resources"></a>Zasoby usługi Batch
Niektóre hello następujących zasobów — kont, obliczeń węzłów, pule, zadań i zadań — są wymagane przez wszystkie rozwiązania korzystające hello usługa partia zadań. Inne, takie jak harmonogramy zadań i pakiety aplikacji, to funkcje przydatne, ale opcjonalne.

* [Konto](#account)
* [Węzeł obliczeniowy](#compute-node)
* [Pula](#pool)
* [Zadanie](#job)

  * [Harmonogramy zadań](#scheduled-jobs)
* [Zadanie podrzędne](#task)

  * [Zadanie podrzędne uruchamiania](#start-task)
  * [Zadanie podrzędne Menedżera zadań](#job-manager-task)
  * [Zadania podrzędne przygotowania i zwolnienia zadań](#job-preparation-and-release-tasks)
  * [Zadanie podrzędne obejmujące wiele wystąpień (MPI)](#multi-instance-tasks)
  * [Zależności zadań podrzędnych](#task-dependencies)
* [Pakiety aplikacji](#application-packages)

## <a name="account"></a>Konto
Konto usługi partia zadań jest jednostką jednoznacznie zdefiniowane w ramach hello usługa partia zadań. Całe przetwarzanie jest skojarzone z kontem usługi Batch.

Możesz utworzyć konto partii zadań Azure za pomocą hello [portalu Azure](batch-account-create-portal.md) lub programowo, takich jak z hello [biblioteki zarządzania partiami platformy .NET](batch-management-dotnet.md). Podczas tworzenia konta hello, można skojarzyć konto magazynu platformy Azure.

### <a name="pool-allocation-mode"></a>Tryb alokacji puli

Podczas tworzenia konta usługi Batch można określić sposób przydzielania [pul](#pool) węzłów obliczeniowych. Można wybrać pule tooallocate węzłów obliczeniowych w ramach subskrypcji, zarządza partii zadań Azure lub można je było przydzielić w ramach własnej subskrypcji. Witaj *Tryb alokacji puli* właściwość dla konta hello Określa, której pule są przydzielone. 

toodecide, który puli toouse Tryb alokacji, weź pod uwagę, która najlepiej pasuje do danego scenariusza:

* **Usługa partii**: Usługa partia zadań jest hello domyślnej puli alokacji tryb, przydzielania pule tle hello w subskrypcjach zarządzane Azure. Należy pamiętać, te najważniejsze informacje o trybie alokacji puli usługi partia zadań hello:

    - Tryb alokacji puli usługi partia zadań Hello obsługuje pule maszyn wirtualnych i usługi w chmurze.
    - Witaj Tryb alokacji puli usługi partia zadań obsługuje zarówno uwierzytelniania klucza współużytkowanego lub [uwierzytelniania usługi Azure Active Directory](batch-aad-auth.md) (Azure AD). 
    - Można użyć obu węzłów obliczeniowych dedykowanej lub niskim priorytecie w pulach przydzielone z trybem przydziału puli usługi partia zadań hello.
    - Tryb alokacji puli usługi partia zadań hello nie należy używać, jeśli planujesz toocreate pule maszyny wirtualnej platformy Azure z niestandardowych obrazów maszyn wirtualnych lub jeśli planujesz toouse sieci wirtualnej. Zamiast tego utworzyć konta z trybem przydziału puli subskrypcji użytkownika hello.
    - Zainicjowano obsługę administracyjną konta tworzone z trybem przydziału puli usługi partia zadań hello pule maszyny wirtualnej musi zostać utworzony z [Marketplace maszyny wirtualne Azure] [ vm_marketplace] obrazów.

* **Subskrypcji użytkownika**: Z trybem przydziału puli subskrypcji użytkownika hello, partii pule są przydzielane w hello subskrypcji platformy Azure, w którym hello konto jest tworzone. Należy pamiętać, te najważniejsze informacje o trybie alokacji puli subskrypcji użytkownika hello:
     
    - Tryb alokacji puli subskrypcji użytkownika Hello obsługuje tylko pule maszyny wirtualnej. Nie obsługuje ona pul usług w chmurze.
    - toocreate maszyny wirtualnej pulę z niestandardowych obrazów maszyn wirtualnych lub toouse sieć wirtualną przy użyciu pul maszyny wirtualnej, należy użyć trybu alokacji puli subskrypcji użytkownika hello.  
    - Należy użyć [uwierzytelniania usługi Azure Active Directory](batch-aad-auth.md) przy użyciu pul przydzielonych w subskrypcji użytkownika hello. 
    - Należy skonfigurować usługi Azure key vault dla Twojego konta usługi partia zadań, jeśli ustawiono tryb alokacji puli hello tooUser subskrypcji. 
    - Węzły obliczeniowe tylko dedykowanych można użyć w pulach w konto utworzone w trybie alokacji puli subskrypcji użytkownika hello. Węzły o niskim priorytecie nie są obsługiwane.
    - Zainicjowano obsługę administracyjną konta z trybem przydziału puli subskrypcji użytkownika hello pule maszyny wirtualnej można tworzyć z [Marketplace maszyny wirtualne Azure] [ vm_marketplace] obrazy lub z niestandardowych obrazów, które Podaj.

Witaj w poniższej tabeli porównano hello usługa partia zadań i subskrypcji użytkownika puli alokacji tryby.

| **Tryb alokacji puli**                 | **Usługa Batch**                                                                                       | **Subskrypcja użytkownika**                                                              |
|-------------------------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **Lokalizacja przydzielania puli**               | Subskrypcja zarządzana przez platformę Azure                                                                           | Hello użytkownika subskrypcji, w których hello partii konto jest tworzone                        |
| **Obsługiwane konfiguracje**             | <ul><li>Konfiguracja usługi w chmurze</li><li>Konfiguracja maszyny wirtualnej (Linux i Windows)</li></ul> | <ul><li>Konfiguracja maszyny wirtualnej (Linux i Windows)</li></ul>                |
| **Obsługiwane obrazy maszyn wirtualnych**                  | <ul><li>Obrazy z witryny Azure Marketplace</li></ul>                                                              | <ul><li>Obrazy z witryny Azure Marketplace</li><li>Obrazy niestandardowe</li></ul>                   |
| **Obsługiwane typy węzłów obliczeniowych**         | <ul><li>Węzły dedykowane</li><li>Węzły o niskim priorytecie</li></ul>                                            | <ul><li>Węzły dedykowane</li></ul>                                                  |
| **Obsługiwane uwierzytelnianie**             | <ul><li>Klucz wspólny</li><li>Azure AD</li></ul>                                                           | <ul><li>Azure AD</li></ul>                                                         |
| **Magazyn Azure Key Vault jest wymagany**             | Nie                                                                                                      | Tak                                                                                |
| **Limit przydziału rdzeni**                           | Ustalany zgodnie z limitem przydziału rdzeni usługi Batch                                                                          | Ustalany zgodnie z limitem przydziału rdzeni subskrypcji                                              |
| **Obsługa sieci Azure Virtual Network (VNet)** | Pule utworzone za pomocą hello konfiguracji usługi w chmurze                                                      | Pule utworzone za pomocą hello konfiguracji maszyny wirtualnej                               |
| **Obsługiwany model wdrożenia sieci wirtualnej**      | Sieci wirtualne utworzone przy użyciu klasycznego modelu wdrażania                                                             | Sieci wirtualne utworzone za pomocą hello klasycznego modelu wdrażania lub usługi Azure Resource Manager |

## <a name="azure-storage-account"></a>Konto usługi Azure Storage

Większość rozwiązań partii usługi Batch używa usługi Azure Storage do przechowywania plików zasobów i plików wyjściowych.  

Wsadowe aktualnie obsługuje tylko typ konta magazynu ogólnego przeznaczenia hello, zgodnie z opisem w kroku 5 [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) w [kont magazynu Azure o](../storage/common/storage-create-storage-account.md). Zadania podrzędne usługi Batch (w tym standardowe, uruchamiania oraz przygotowania i zwolnienia zadań) muszą określać pliki zasobów, które znajdują się na kontach magazynu ogólnego przeznaczenia.


## <a name="compute-node"></a>Węzeł obliczeniowy
Węzeł obliczeniowy to Azure maszyny wirtualnej (VM) lub usługi w chmurze maszyny Wirtualnej, który jest dedykowany tooprocessing część obciążenia aplikacji. rozmiar Hello węzła określa hello liczba rdzeni Procesora, pamięci i rozmiar systemu lokalnego pliku przydzielonej toohello węzła. Pule węzłów z systemem Windows lub Linux można tworzyć przy użyciu usług Azure Cloud Services, obrazów z hello [Marketplace maszyny wirtualne Azure][vm_marketplace], lub niestandardowych obrazów, które należy przygotować. Zobacz następujące hello [puli](#pool) sekcji, aby uzyskać więcej informacji na temat tych opcji.

Węzły można uruchomić wszystkie plik wykonywalny lub skrypt, który jest obsługiwany przez środowisko systemu operacyjnego hello hello węzła. Dotyczy to plików \*EXE, \*CMD, \*BAT i skryptów programu PowerShell dla systemu Windows — oraz plików binarnych, powłoki i skryptów języka Python dla systemu Linux.

Wszystkie węzły obliczeniowe usługi Batch obejmują również:

* Standardową [strukturę folderów](#files-and-directories) i skojarzone [zmienne środowiskowe](#environment-settings-for-tasks) dostępne do użycia jako odwołania w zadaniach podrzędnych.
* **Zapora** ustawienia, które są skonfigurowane toocontrol dostępu.
* [Dostęp zdalny](#connecting-to-compute-nodes) tooboth (protokołu RDP (Remote Desktop)) systemu Windows i Linux (Secure Shell (SSH)) węzły.

## <a name="pool"></a>Pula
Pula to kolekcja węzłów, w których jest uruchamiana aplikacja. Hello puli można tworzyć ręcznie przez użytkownika lub automatycznie przez hello usługa partia zadań po określeniu toobe pracy hello gotowe. Można utworzyć i zarządzać nimi puli, która spełnia wymagania dotyczące zasobów hello aplikacji. Pula może służyć tylko przez hello konta usługi partia zadań, w której został utworzony. Konto usługi Batch może zawierać więcej niż jedną pulę.

Azure pule partii bazując na powitania podstawowej platformy obliczeń platformy Azure. Udostępniają one alokacji na dużą skalę, instalacja aplikacji, danych dystrybucji, monitorowanie kondycji i hello liczba węzłów obliczeniowych w puli elastycznej ([skalowanie](#scaling-compute-resources)).

Każdy węzeł, który zostanie dodany do puli tooa przypisano unikatową nazwę i adres IP. Gdy węzeł zostanie usunięty z puli, wszelkie zmiany wprowadzone w systemie operacyjnym toohello lub pliki zostaną utracone, a jego nazwa i adres IP, które są wydawane do użytku w przyszłości. Gdy węzeł opuści pulę, oznacza to, że zakończył się jego okres istnienia.

Podczas tworzenia puli, można określić hello następujące atrybuty. Niektóre ustawienia są różne, w zależności od trybu alokacji puli hello hello partii [konta](#account):

- Wersja i system operacyjny węzła obliczeniowego
- Typ węzła obliczeniowego i docelowa liczba węzłów
- Rozmiar hello węzły obliczeniowe
- Zasady skalowania
- Zasady planowania zadań podrzędnych
- Stan komunikacji węzłów obliczeniowych
- Zadanie podrzędne uruchamiania dla węzłów obliczeniowych
- Pakiety aplikacji
- Konfiguracja sieci

Każde z tych ustawień jest opisane bardziej szczegółowo w hello następujące sekcje.

> [!IMPORTANT]
> Konta usługi partia zadań utworzone przy użyciu Tryb alokacji puli usługi partia zadań hello mieć domyślnego przydziału, która ogranicza hello liczba rdzeni w ramach konta usługi partia zadań. Witaj liczba rdzeni odpowiada toohello liczba węzłów obliczeniowych. Można znaleźć hello przydziałów domyślnych i instrukcje na temat zbyt[Zwiększ limit przydziału](batch-quota-limit.md#increase-a-quota) w [przydziały i limity dla usługi partia zadań Azure hello](batch-quota-limit.md). Jeśli pulę nie osiągnęła jego docelowy liczba węzłów, hello przyczyny mogą być hello limit przydziału rdzeni.
>
>Konta usługi partia zadań utworzone przy użyciu Tryb alokacji puli subskrypcji użytkownika hello nie Obserwuj przydziały usługi hello partii. Zamiast tego udziału w hello limit przydziału rdzeni dla hello określonej subskrypcji. Aby uzyskać więcej informacji, zobacz sekcję [Virtual Machines limits (Limity maszyn wirtualnych)](../azure-subscription-service-limits.md#virtual-machines-limits) w artykule [Azure subscription and service limits, quotas, and constraints (Ograniczenia, przydziały i limity usług i subskrypcji platformy Azure)](../azure-subscription-service-limits.md).
>
>

### <a name="compute-node-operating-system-and-version"></a>Wersja i system operacyjny węzła obliczeniowego

Podczas tworzenia puli partii, można określić hello konfiguracji maszyny wirtualnej platformy Azure i typ hello ma toorun w każdym węźle obliczeń w puli hello systemu operacyjnego. Istnieją dwa typy Hello konfiguracji dostępne w partii:

- Witaj **konfiguracji maszyny wirtualnej**, który określa tej puli hello składa się z maszyn wirtualnych platformy Azure. Te maszyny wirtualne można tworzyć na podstawie obrazów systemu Windows albo Linux. 

    Podczas tworzenia puli hello konfiguracji maszyny wirtualnej, należy określić nie tylko hello rozmiaru hello węzłów i hello źródła toocreate obrazy używane hello je, ale również hello **odwołanie do obrazu maszyny wirtualnej** i hello Wsadowe **agenta węzła jednostki SKU** toobe zainstalowane na powitania węzłów. Więcej informacji na temat określania powyższych właściwości puli znajduje się w artykule [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) (Aprowizowanie węzłów obliczeniowych systemu Linux w pulach usługi Azure Batch).

- Witaj **konfiguracji usługi w chmurze**, który określa tej puli hello składa się z węzłów usługi w chmurze Azure. Usługi Cloud Services oferują *tylko* węzły obliczeniowe systemu Windows.

    Dostępnych systemów operacyjnych dla pul konfiguracji usługi w chmurze są wymienione w hello [wersji systemu operacyjnego gościa Azure i zgodność pakietu SDK](../cloud-services/cloud-services-guestos-update-matrix.md). Podczas tworzenia puli, która zawiera węzły usługi w chmurze, wymagają rozmiaru węzła hello toospecify i jego *rodziny systemów operacyjnych*. Usługi w chmurze są wdrożone tooAzure szybciej niż maszyn wirtualnych z systemem Windows. Jeśli potrzebujesz pul systemu Windows, może się okazać, że usługi Cloud Services oferują korzystną wydajność związaną z czasem wdrażania.

    * Witaj *rodziny systemów operacyjnych* decyduje również o wersjach programu .NET są instalowane z hello systemu operacyjnego.
    * Zgodnie z rolami proces roboczy w ramach usługi w chmurze, można określić *wersji systemu operacyjnego* (Aby uzyskać więcej informacji o roli proces roboczy, zobacz hello [informacji o usługach w chmurze](../cloud-services/cloud-services-choose-me.md#tell-me-about-cloud-services) części hello [usługi w chmurze Omówienie](../cloud-services/cloud-services-choose-me.md)).
    * Zgodnie z roli proces roboczy, zaleca się określenie `*` dla hello *wersji systemu operacyjnego* tak, aby węzły hello są uaktualniane automatycznie i nie nie toocater pracy wymaganej wersji toonewly wydane. Witaj pierwotnym zastosowaniem wybranie określonych wersji systemu operacyjnego jest tooensure zgodności aplikacji, dzięki czemu zgodności z poprzednimi wersjami testowania toobe wykonywane przed zezwoleniem na powitania toobe wersji aktualizacji. Po sprawdzeniu poprawności, hello *wersji systemu operacyjnego* hello puli może być aktualizowana i może zostać zainstalowany nowy obraz systemu operacyjnego hello — wszelkie uruchomione zadania są przerwane i umieszczony w kolejce.

Podczas tworzenia puli należy tooselect hello odpowiednie **nodeAgentSkuId**w zależności od hello systemu operacyjnego hello obraz podstawowy dysk VHD. Można uzyskać mapowanie tootheir identyfikator jednostki SKU agenta węzła dostępne odwołań do obrazu systemu operacyjnego przez wywołanie hello [jednostki SKU agenta węzła listy obsługiwanych](https://docs.microsoft.com/rest/api/batchservice/list-supported-node-agent-skus) operacji.

Zobacz hello [konta](#account) sekcji informacji na temat ustawiania trybu alokacji puli hello podczas tworzenia konta usługi partia zadań.

#### <a name="custom-images-for-virtual-machine-pools"></a>Niestandardowe obrazy dla pul usługi Virtual Machines

toouse pule maszyny wirtualnej tooprovision niestandardowego obrazu, tworzenie konta partii zadań z trybem przydziału puli subskrypcji użytkownika hello. W tym trybie partii pule są przydzielone do subskrypcji hello, w którym znajduje się konto hello. Zobacz hello [konta](#account) sekcji informacji na temat ustawiania trybu alokacji puli hello podczas tworzenia konta usługi partia zadań.

toouse niestandardowego obrazu, będziesz potrzebować obraz powitania tooprepare uogólniania go. Aby uzyskać informacje dotyczące przygotowania niestandardowych obrazów systemu Linux z maszyn wirtualnych platformy Azure, zobacz [przechwytywania toouse Azure maszyny Wirtualnej systemu Linux jako szablon](../virtual-machines/linux/capture-image-nodejs.md). Aby uzyskać informacje na temat przygotowywania niestandardowych obrazów systemu Windows na podstawie maszyn wirtualnych Azure Virtual Machines, zobacz [Create custom VM images with Azure PowerShell (Tworzenie niestandardowych obrazów maszyn wirtualnych przy użyciu programu Azure PowerShell)](../virtual-machines/windows/tutorial-custom-images.md). 

> [!IMPORTANT]
> Podczas przygotowywania obraz niestandardowy, należy uwzględnić następujące hello:
> - Upewnij się, obraz systemu operacyjnego podstawowej tego hello Użyj tooprovision Twojego pule partii jest nie ma wstępnie zainstalowanych rozszerzeń Azure, takich jak hello rozszerzenia niestandardowego skryptu. Jeśli obraz powitania zawiera wstępnie zainstalowane rozszerzenia, Azure mogą wystąpić problemy, wdrażanie hello maszyny Wirtualnej.
> - Upewnij się, tego hello podstawowy obraz systemu operacyjnego zapewniają się, że używa hello domyślnym tymczasowego dysku, jak hello agenta węzła partii aktualnie oczekuje hello domyślnym tymczasowego dysku.
>
>

toocreate puli konfiguracji maszyny wirtualnej przy użyciu niestandardowego obrazu, trzeba będzie je utworzyć lub więcej standardowy magazyn Azure kont toostore niestandardowych obrazów dysku VHD. Obrazy niestandardowe są przechowywane jako obiekty blob. tooreference niestandardowe obrazy podczas tworzenia puli, określ hello URI hello obiekty BLOB dysków VHD niestandardowego obrazu dla hello [osDisk](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_osdisk) właściwości hello [virtualMachineConfiguration](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_vmconf) właściwości.

Upewnij się, że kont magazynu spełniają hello następujące kryteria:   

- Hello kont magazynu obiektów blob zawierający hello niestandardowego obrazu wirtualnego dysku twardego konieczne toobe w hello tej samej subskrypcji, jak hello konta usługi partia zadań (hello subskrypcji użytkownika).
- określony Hello kont magazynu muszą toobe w hello tego samego regionu hello konta usługi partia zadań.
- Obecnie są obsługiwane tylko standardowe konta magazynu ogólnego przeznaczenia. Usługa Azure Premium storage będzie obsługiwany w przyszłości hello.
- Możesz określić jedno konto magazynu z wieloma niestandardowymi obiektami blob dysku VHD lub wiele kont magazynu, każde z pojedynczym obiektem blob. Zalecamy toouse kont magazynu wielu tooget lepszą wydajność.
- Jeden unikatowy obrazu niestandardowego obiektu blob dysku VHD może obsługiwać too40, którego wystąpienia maszyny Wirtualnej systemu Linux lub 20 wystąpień maszyny Wirtualnej systemu Windows. Konieczne będzie toocreate kopie hello wirtualnego dysku twardego blob toocreate pule więcej maszyn wirtualnych. Na przykład pulą o 200 maszyn wirtualnych systemu Windows wymaga 10 unikatowy obiekty BLOB dysków VHD określony dla hello **osDisk** właściwości.

toocreate puli z niestandardowego obrazu przy użyciu hello portalu Azure:

1. Przejdź tooyour konta usługi partia zadań w hello portalu Azure.
2. Na powitania **ustawienia** bloku, wybierz hello **pule** elementu menu.
3. Na powitania **pule** bloku, wybierz hello **Dodaj** polecenie; hello **Dodawanie puli** zostanie wyświetlony blok.
4. Wybierz **niestandardowego obrazu (Linux/system Windows)** z hello **typ obrazu** listy rozwijanej. Hello portal Wyświetla hello **obraz niestandardowy** selektora. Wybierz jeden lub więcej dysków VHD z hello tego samego kontenera i kliknij przycisk hello **wybierz** przycisku. 
    Obsługa wielu wirtualnych dysków twardych z różnych kont magazynu i różnych kontenerów zostaną dodane w przyszłości hello.
5. Wybierz poprawną hello **wydawcy lub oferta/jednostki Sku** dla niestandardowych dyski VHD, wybierz wymaganą hello **buforowanie** trybie, a następnie wypełnij wszystkie inne parametry puli hello hello.
6. toocheck, jeśli pula jest oparta na niestandardowego obrazu, zobacz hello **systemu operacyjnego** właściwości hello zasobów podsumowania część hello **puli** bloku. Hello wartość tej właściwości musi być **obrazu maszyny Wirtualnej niestandardowe**.
7. Wszystkie dyski VHD niestandardowe skojarzone z pulą są wyświetlane w puli hello **właściwości** bloku.

### <a name="compute-node-type-and-target-number-of-nodes"></a>Typ węzła obliczeniowego i docelowa liczba węzłów

Po utworzeniu puli można określić typy węzłów obliczeniowych mają i hello numer docelowej dla każdego. typy Hello dwa węzły obliczeniowe są:

- **Dedykowane węzły obliczeniowe.** Dedykowane węzły obliczeniowe są zarezerwowane dla konkretnych obciążeń. Są droższe niż węzły niskiego priorytetu, ale są one zagwarantować toonever zostać przeniesiona.

- **Węzły obliczeniowe o niskim priorytecie.** Węzły o niskim priorytecie wykorzystać nadwyżki zdolności produkcyjnych w Azure toorun obciążeń partii. Węzły o niskim priorytecie są tańsze (niższe stawki za godzinę) niż węzły dedykowane i umożliwiają obsługiwanie obciążeń wymagających dużej mocy obliczeniowej. Aby uzyskać więcej informacji, zobacz [Use low-priority VMs with Batch](batch-low-pri-vms.md) (Korzystanie z maszyn wirtualnych o niskim priorytecie z usługą Batch).

    Węzły obliczeniowe o niskim priorytecie mogą być przerywane, jeśli na platformie Azure nie będzie wystarczającej nadwyżki wydajności. Jeśli węzeł jest zastępowane podczas uruchamiania zadania, zadania hello są umieszczony w kolejce i uruchom ponownie, gdy węzeł obliczeniowy znowu dostępne. Węzły niskiego priorytetu to dobra opcja w przypadku obciążeń, których czas ukończenia zadania hello jest elastyczny i hello pracy będzie rozmieszczona na wielu węzłach. Przed podjęciem decyzji o toouse niskiego priorytetu węzłów dla danego scenariusza, upewnij się, że pracę, utracone powodu toopreemption będzie toorecreate minimalnego i łatwe.

    Węzły obliczeniowe o niskim priorytecie są dostępne tylko dla konta wsadowego utworzone przy użyciu trybu alokacji puli hello ustawić także**usługa partia zadań**.

Może mieć obu węzłów obliczeniowych niskiego priorytetu i dedykowanych w hello tej samej puli. Każdy typ węzła &mdash; niskiego priorytetu i dedykowanych &mdash; ma własną ustawienie docelowe, dla którego można określić hello żądaną liczbę węzłów. 
    
Hello liczba węzłów obliczeniowych jest określony tooas *docelowej* ponieważ w niektórych sytuacjach puli użytkownika nie może nawiązać połączenia hello żądaną liczbę węzłów. Na przykład puli nie może osiągnąć hello docelowych, jeśli osiągnie hello [limit przydziału rdzeni](batch-quota-limit.md) Twojego partii najpierw kont. Lub puli hello wydajność nie będzie hello docelowy w przypadku zastosowania automatyczne skalowanie puli toohello formuły, która ogranicza hello maksymalną liczbę węzłów.

Aby uzyskać informacje dotyczące cen węzłów obliczeniowych o niskim priorytecie i dedykowanych węzłów obliczeniowych, zobacz [Batch — cennik](https://azure.microsoft.com/pricing/details/batch/).

### <a name="size-of-hello-compute-nodes"></a>Rozmiar hello węzły obliczeniowe

Lista rozmiarów węzłów obliczeniowych **konfiguracji usług Cloud Serivces** znajduje się w temacie [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Rozmiary dla usługi Cloud Services). Usługa Batch obsługuje wszystkie rozmiary usług Cloud Services oprócz `ExtraSmall`, `STANDARD_A1_V2` i `STANDARD_A2_V2`.

Listę rozmiarów obliczeniowych **konfiguracji usługi Virtual Machines** można znaleźć w tematach [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md) (Linux) (Rozmiary maszyn wirtualnych na platformie Azure) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md) (Windows) (Rozmiary maszyn wirtualnych na platformie Azure) (Windows). Usługa Batch obsługuje wszystkie rozmiary maszyn wirtualnych platformy Azure oprócz `STANDARD_A0` i maszyn z usługi Premium Storage (seria `STANDARD_GS`, `STANDARD_DS` i `STANDARD_DSV2`).

Podczas wybierania rozmiaru węzła obliczeń, należy wziąć pod uwagę hello charakterystyki i wymagania aplikacji hello, których będzie uruchamiany na powitania węzłów. Aspekty, takich jak określa, czy aplikacja hello jest wielowątkowe i ilość pamięci zużywa może pomóc określić rozmiaru węzła najbardziej odpowiedniego i ekonomiczne hello. To typowy tooselect, rozmiaru węzła, zakładając, że jedno zadanie zostanie uruchomiona w węźle naraz. Jest jednak możliwe toohave wielu zadań (i w związku z tym wiele wystąpień aplikacji) [równolegle](batch-parallel-node-tasks.md) na węzłach obliczeniowych podczas wykonywania zadania. W takim przypadku jest typowe toochoose na większych węzła rozmiar tooaccommodate hello zwiększyć żądanie wykonania zadań równoległych. Aby uzyskać więcej informacji, zobacz [Zasady planowania zadań podrzędnych](#task-scheduling-policy).

Wszystkie węzły hello w puli są hello sam rozmiar. Jeśli możesz mają aplikacje toorun różne wymagania systemowe i/lub obciążenia poziomy, zalecane jest użycie oddzielnych pule.

### <a name="scaling-policy"></a>Zasady skalowania

Dynamiczne obciążeń można zapisać i stosować [automatyczne skalowanie formuła](#scaling-compute-resources) tooa puli. Witaj usługa partia zadań okresowo ocenia formuły i koryguje hello liczbę węzłów w ramach puli hello na podstawie różnych puli, zadania i parametry zadania, które można określić.

### <a name="task-scheduling-policy"></a>Zasady planowania zadań podrzędnych

Witaj [maksymalnej liczby zadań na węzeł](batch-parallel-node-tasks.md) opcji konfiguracji określa maksymalną liczbę zadań, które mogą być uruchamiane równolegle na każdym węźle obliczeń w puli hello hello.

Hello domyślna konfiguracja Określa, że działa jedno zadanie naraz w węźle, ale w przypadku scenariuszy, w których jest korzystne toohave co najmniej dwa zadania wykonywane w węźle jednocześnie. Zobacz hello [przykładowy scenariusz](batch-parallel-node-tasks.md#example-scenario) w hello [węzła równoczesnych zadań](batch-parallel-node-tasks.md) toosee artykułu, jak można korzystać z wielu zadań na węzeł.

Można również określić *typ wypełnienia* który określa, czy partii rozprzestrzenia zadania hello równomiernie we wszystkich węzłach w puli, czy pakiety każdego węzła za hello maksymalna liczba zadań przed przypisaniem węzeł tooanother zadania.

### <a name="communication-status-for-compute-nodes"></a>Stan komunikacji węzłów obliczeniowych

W większości przypadków zadania działać niezależnie i nie ma potrzeby toocommunicate ze sobą. Jednak w niektórych aplikacjach będzie wymagana komunikacja między zadaniami podrzędnymi (np. w [scenariuszach MPI](batch-mpi.md)).

Można skonfigurować tooallow puli **komunikacji między węzłami**, dzięki czemu węzłów w puli może komunikować się w czasie wykonywania. Po włączeniu komunikacji międzywęzłowej węzły w pulach konfiguracji usług Cloud Services mogą komunikować się ze sobą na portach większych niż 1100, a w przypadku pul konfiguracji usługi Virtual Machines ruch nie jest ograniczony do żadnego portu.

Warto zauważyć, że włączenie komunikacji między węzłami również wpływa na rozmieszczenie hello hello węzłów w ramach klastrów może ograniczyć hello maksymalną liczbę węzłów w puli z powodu ograniczeń wdrożenia. Jeśli aplikacja nie wymaga komunikacji między węzłami, hello usługa partia zadań można przydzielić potencjalnie dużej liczby węzłów puli toohello z wielu różnych klastrów i centrów danych tooenable zwiększyć możliwości przetwarzania równoległego.

### <a name="start-tasks-for-compute-nodes"></a>Zadanie podrzędne uruchamiania dla węzłów obliczeniowych

opcjonalne Hello *Uruchom zadanie* wykonywane na każdym węźle, ponieważ ten węzeł dołącza hello puli i każdym razem, kiedy węzeł zostanie ponownie uruchomiony lub odtworzyć z obrazu. zadania uruchamiania Hello jest szczególnie przydatna w przypadku przygotowywania węzły obliczeniowe hello wykonywania zadań, takich jak instalowanie aplikacji hello, które zadania uruchamiane na powitania węzłów obliczeniowych.

### <a name="application-packages"></a>Pakiety aplikacji

Można określić [pakietów aplikacji](#application-packages) toodeploy toohello obliczeniowe węzłów w puli hello. Pakiety aplikacji zapewniają uproszczone wdrażanie i wersji aplikacji hello, których uruchamianie zadań. Pakiety aplikacji wybrane dla puli są instalowane w każdym węźle dołączanym do puli oraz za każdym razem, gdy węzeł jest ponownie uruchamiany lub odtwarzany z obrazu.

> [!NOTE]
> Pakiety aplikacji są obsługiwane we wszystkich pulach usługi Batch utworzonych po 5 lipca 2017 r. Są one obsługiwane w pulach partii utworzyć między 10 marca 2016 i 5 2017 lipca tylko wtedy, gdy pula hello został utworzony za pomocą konfiguracji usługi w chmurze. Pule partii utworzone przed too10 marca 2016 r nie obsługują pakietów aplikacji. Aby uzyskać więcej informacji dotyczących używania aplikacji pakiety toodeploy węzły partii tooyour aplikacji, zobacz [wdrożyć aplikacje toocompute węzły z pakietami aplikacji partii](batch-application-packages.md).
>
>

### <a name="network-configuration"></a>Konfiguracja sieci

Można określić podsieci hello Azure [sieć wirtualną (VNet)](../virtual-network/virtual-networks-overview.md) w puli które hello obliczeń należy utworzyć węzłów. Zobacz hello [konfiguracji sieci puli](#pool-network-configuration) sekcji, aby uzyskać więcej informacji.


## <a name="job"></a>Zadanie
Zadanie to kolekcja zadań podrzędnych. Zarządza realizację jego zadań podrzędnych na powitania węzłów obliczeniowych w puli obliczeń.

* zadanie Hello określa hello **puli** w których hello pracy jest toobe Uruchom. Możesz utworzyć nową pulę dla każdego zadania lub używać jednej puli dla wielu zadań. Możesz utworzyć pulę dla każdego zadania skojarzonego z harmonogramem zadań lub dla wszystkich zadań skojarzonych z harmonogramem zadań.
* Możesz określić opcjonalny **priorytet zadania**. Po przesłaniu zadania mające wyższy priorytet niż zadania, które są obecnie w toku hello zadań dla zadania o wyższym priorytecie hello są wstawiane do kolejki hello wcześniejsze zadań dla zadania o niższym priorytecie hello. Zadania podrzędne w zadaniach o niższym priorytecie, które zostały już uruchomione, nie są przerywane.
* Należy użyć zadania **ograniczenia** toospecify pewnych ograniczeń dla zadań:

    Można ustawić **wallclock maksymalny czas**, dzięki czemu, gdy zadanie działa przez czas dłuższy niż hello wallclock maksymalny czas, kończą hello zadania i wszystkie jego zadań podrzędnych.

    Usługa Batch może wykrywać zadania podrzędne zakończone niepowodzeniem, a następnie ponownie próbować je uruchomić. Można określić hello **maksymalnej liczby ponownych prób zadań** jako ograniczenie, w tym zadania *zawsze* lub *nigdy nie* ponowione. Ponawianie próby zadania oznacza, że to zadanie hello toobe umieszczony w kolejce, uruchom ponownie.
* Aplikacja kliencka można dodać zadania tooa zadania lub określić [zadanie Menedżer zadania](#job-manager-task). Zadanie Menedżer zadania zawiera hello informacje, które są niezbędne toocreate hello wymaganych zadań dla zadania, zadania Menedżer zadania hello uruchomione na jednym z hello węzły w puli hello obliczeniowe. Witaj zadanie Menedżer zadania jest obsługiwane w szczególności przez partię — jest Zakolejkowane natychmiast hello zadania jest tworzony i zostanie ponownie uruchomiony, jeśli jej nie powiedzie się. Zadanie Menedżer zadania jest *wymagane* dla zadań, które są tworzone przez [harmonogram zadań](#scheduled-jobs) ponieważ przed utworzeniem wystąpienia jest zadanie hello jest hello tylko sposób toodefine hello zadania.
* Domyślnie zadania pozostają w stanie aktywnym hello po zakończeniu wszystkich zadań w ramach zadania hello. Aby zmienić to zachowanie, dzięki czemu hello zadań kończy się automatycznie po zakończeniu wszystkich zadań w zadaniu hello. Zestaw hello zadania **onAllTasksComplete** właściwości ([OnAllTasksComplete] [ net_onalltaskscomplete] w partiami platformy .NET) zbyt*terminatejob* tooautomatically z chwilą zadania hello wszystkich swoich zadań znajdują się w stanie hello ukończone.

    Należy pamiętać, że usługa partia zadań hello uwzględnia zadania o *nie* toohave zadania wszystkie zadania zakończone. W związku z tym ta opcja jest najczęściej używana w przypadku [zadania podrzędnego Menedżera zadań](#job-manager-task). Jeśli chcesz toouse zadanie automatycznego zakończenia bez Menedżer zadań należy ustawić początkowo nowe zadanie **onAllTasksComplete** właściwości zbyt*noaction*, ustawić także*terminatejob* dopiero po zakończeniu dodawania zadań toohello zadania.

### <a name="job-priority"></a>Priorytet zadań
Można przypisać toojobs priorytetu, które są tworzone w partii. wartość priorytetu hello hello zadania toodetermine hello kolejność planowania zadań w ramach konta używa Hello usługa partia zadań (nie jest to toobe mylić z [zaplanowane zadanie](#scheduled-jobs)). wartości priorytetu Hello należeć do zakresu od -1000 too1000, przy czym -1000 jest hello najniższy priorytet, a 1000 hello najwyższy. priorytet hello tooupdate zadania hello wywołania [hello właściwości zadania aktualizacji] [ rest_update_job] operacji (REST partii), lub zmodyfikuj hello [CloudJob.Priority] [ net_cloudjob_priority] właściwości (partiami platformy .NET).

W ramach hello tego samego konta, wyższy priorytet zadania mają planowania pierwszeństwo nad zadania o niższym priorytecie. Zadanie o wyższym priorytecie na jednym koncie nie ma pierwszeństwa planowania nad innym zadaniem o niższym priorytecie na innym koncie.

Planowanie zadań między pulami odbywa się niezależnie. Między różnymi pulami nie ma żadnej gwarancji, że zadanie o wyższym priorytecie zostanie zaplanowane jako pierwsze, jeśli w skojarzonej z nim puli brakuje bezczynnych węzłów. W hello tej samej puli, zadania z hello sam priorytet mają taki sam sposób przez cały czas zaplanowane.

### <a name="scheduled-jobs"></a>Zaplanowane zadania
[Harmonogramy zadań] [ rest_job_schedules] pozwalają toocreate zadań cyklicznych, w ramach hello usługa partia zadań. Harmonogram zadania określa po toorun zadania i zawiera specyfikacje hello hello toobe zadania uruchamiania. Można określić czas trwania hello harmonogramu hello —, jak długo po hello harmonogram obowiązuje — i jak często zadania są tworzone podczas hello zaplanowany okres.

## <a name="task"></a>Zadanie
Zadanie podrzędne to jednostka obliczeniowa skojarzona z zadaniem. Jest ono uruchamiane w węźle. Zadania są przypisane tooa węzła w celu wykonywania lub są umieszczane w kolejce, dopóki zwolnieniu węzła. Po prostu umieść, zadanie działa programów lub skryptów na obliczeń węzła tooperform hello pracy potrzebne.

Podczas tworzenia zadania podrzędnego można określić:

* Witaj **wiersza polecenia** hello zadania. Jest to hello wiersz polecenia, który działa w węźle obliczeń hello aplikacji lub skryptu.

    Jest ważne toonote, który hello wiersza polecenia nie jest rzeczywiście uruchamiany w powłoce. W związku z tym natywnie nie może przyjąć korzystać z funkcji powłoki, takie jak [zmiennej środowiskowej](#environment-settings-for-tasks) rozszerzenia (dotyczy to również hello `PATH`). tootake korzystać z takich funkcji, należy wywołać hello powłoki w wierszu polecenia hello — na przykład uruchamiając `cmd.exe` w węzłach systemu Windows lub `/bin/sh` w systemie Linux:

    `cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

    `/bin/sh -c MyTaskApplication $MY_ENV_VAR`

    W przypadku zadania konieczne toorun aplikacji lub skrypt, który nie znajduje się w hello węzła `PATH` lub odwołać zmiennych środowiskowych, wywołaj powłoki hello jawnie w wierszu polecenia zadania hello.
* **Pliki zasobów** zawierających toobe danych hello przetworzone. Te pliki są automatycznie skopiowane toohello węzła z magazynu obiektów Blob na koncie magazynu Azure ogólnego przeznaczenia, przed wykonaniem zadań hello wiersza polecenia. Aby uzyskać więcej informacji, zobacz sekcje hello [zadania uruchamiania](#start-task) i [plików i katalogów](#files-and-directories).
* Witaj **zmiennych środowiskowych** wymagane przez aplikację. Aby uzyskać więcej informacji, zobacz hello [ustawienia środowiska dla zadań](#environment-settings-for-tasks) sekcji.
* Witaj **ograniczenia** pod które hello mają być wykonywane zadania. Na przykład ograniczenia obejmują hello maksymalny czas zadania hello jest dozwolona toorun, hello maksymalną liczbę razy, należy wykonać ponownie zadania zakończone niepowodzeniem, i hello maksymalny czas, który pliki w katalogu roboczym hello zadania są zachowywane.
* **Pakiety aplikacji** toodeploy toohello obliczeniowe węzeł, na którym hello zadanie jest zaplanowane toorun. [Pakiety aplikacji](#application-packages) uproszczone wdrażanie i wersji aplikacji hello, których uruchamianie zadań. Pakiety aplikacji na poziomie zadania są szczególnie przydatne w środowiskach udostępnionych puli, której różne zadania są uruchamiane w jednej puli i hello puli nie zostanie usunięta po zakończeniu zadania. Jeśli zadanie ma mniejszą liczbę zadań niż węzłów w puli hello, pakiety aplikacji zadań można zminimalizować transfer danych, ponieważ aplikacja jest wdrożony toohello tylko węzły, które uruchamiania zadań.

Ponadto należy zdefiniować w węźle obliczeń tooperform tootasks, powitania po specjalnych zadań podawane są również przez usługi partia zadań hello:

* [Zadanie podrzędne uruchamiania](#start-task)
* [Zadanie podrzędne Menedżera zadań](#job-manager-task)
* [Zadania podrzędne przygotowania i zwolnienia zadań](#job-preparation-and-release-tasks)
* [Zadania podrzędne obejmujące wiele wystąpień (MPI)](#multi-instance-tasks)
* [Zależności zadań podrzędnych](#task-dependencies)

### <a name="start-task"></a>Zadanie uruchamiania
Kojarząc **Uruchom zadanie** z puli, można przygotować hello działających w środowisku z jego węzłów. Na przykład można wykonać akcji, takich jak instalowanie aplikacji hello, których uruchamianie zadań lub uruchamianie procesów w tle. zadania uruchamiania Hello jest uruchamiany za każdym razem, gdy rozpoczyna się węzeł, dla tak długo, jak pozostaje w puli hello — tym, gdy węzeł hello jest najpierw dodać puli toohello i kiedy zostanie ponownie uruchomiony lub odtworzyć z obrazu.

Główną zaletą zadania uruchamiania hello jest można ją zawiera wszystkie informacje hello jest konieczne tooconfigure węźle obliczeń i instalację aplikacji hello, które są wymagane do wykonania zadania. W związku z tym zwiększenie hello liczby węzłów w puli jest tak proste, jak określanie liczby węzeł docelowy nowych hello. zadania uruchamiania Hello zawiera hello partii usługi hello informacje, które jest wymagane tooconfigure hello nowe węzły i przygotowanie ich do akceptowania zadań.

Zgodnie z dowolnego zadania partii zadań Azure można określić listę **pliki zasobów** w [usługi Azure Storage][azure_storage], oprócz tooa **wiersza polecenia** toobe wykonywane. Usługa partia zadań Hello najpierw kopiuje hello zasobów plików toohello węzeł z usługi Azure Storage, a następnie wykonuje hello wiersza polecenia. Zadania uruchamiania puli listy plików hello zazwyczaj zawiera hello zadań aplikacji i jej zależności.

Jednak hello rozpoczęcia zadań można także używane przez wszystkie zadania, które są uruchomione w węźle obliczeń hello toobe danych odwołania. Na przykład można wykonać zadania uruchamiania wiersza polecenia `robocopy` operacji toocopy pliki aplikacji (które zostały określone w postaci plików zasobów i pobrać toohello węzła) z hello uruchomić zadania [katalog roboczy](#files-and-directories) toohello [folderu udostępnionego](#files-and-directories), a następnie uruchom Instalatora MSI lub `setup.exe`.

Zwykle pożądane jest na powitania partii usługi toowait dla hello rozpoczęcia zadań toocomplete przed uwzględnieniu hello węzła gotowe toobe przypisane zadania, ale można go skonfigurować.

Jeśli zadanie uruchamiania nie powiedzie się w węźle obliczeń, następnie hello węzła hello jest w stanie niepowodzenia hello tooreflect zaktualizowane i hello węzeł nie ma przydzielonych żadnych zadań. Zadania uruchamiania może zakończyć się niepowodzeniem, jeśli wystąpi problem kopiowanie jego pliki zasobów z magazynu, czy Proces hello wykonywane przez jego wiersza polecenia zwraca kod zakończenia różną od zera.

Jeśli musisz dodać lub zaktualizować hello zadania uruchamiania dla istniejącej puli, musisz ponownie uruchomić jego węzły obliczeniowe hello rozpoczęcia zadań toobe stosowane toohello węzłów.

>[!NOTE]
> Witaj łączny rozmiar zadania uruchamiania musi być mniejsza lub równa znaków too32768, w tym plików zasobów i zmiennych środowiskowych. tooensure czy zadania rozpoczęcia spełnia tego wymagania, można użyć jednej z dwóch metod:
>
> 1. Umożliwia aplikacji toodistribute pakiety aplikacji i danych w każdym węźle w puli partii. Aby uzyskać więcej informacji na temat pakietów aplikacji, zobacz [wdrożyć aplikacje toocompute węzły z pakietami aplikacji partii](batch-application-packages.md).
> 2. Możesz ręcznie utworzyć skompresowane archiwum zawierające pliki aplikacji. Przekazywanie z archiwum zip tooAzure magazynu jako obiektu blob. Określ archiwum zip hello pliku zasobów w celu rozpoczęcia zadania. Przed uruchomieniem wiersza polecenia hello rozpoczęcia zadania, Rozpakuj archiwum hello z wiersza polecenia hello. 
>
>    archiwum hello toounzip, możesz użyć hello archiwizacji dowolnego narzędzia. Należy użyć archiwum hello toounzip jako plik zasobów na powitania zadanie uruchamiania narzędzia hello tooinclude.
>
>

### <a name="job-manager-task"></a>Zadanie Menedżera zadań
Zazwyczaj używają **zadanie Menedżer zadania** toocontrol i/lub monitor zadania wykonywania — na przykład toocreate i przesłać hello zadań dla zadania, określić dodatkowe zadania toorun i ustalić, po zakończeniu pracy. Zadanie Menedżer zadania nie jest jednak ograniczony toothese działań. Jest całkowicie użytecznym zadanie, które mogą wykonywać wszystkie akcje, które są wymagane dla zadania hello. Na przykład zadanie Menedżer zadania może pobrać plik, który jest określony jako parametr, analizowanie hello zawartość tego pliku i przesłać dodatkowych zadań na podstawie tych zawartości.

Zadanie podrzędne Menedżera zadań jest uruchamiane przed innymi zadaniami podrzędnymi. Udostępnia ona hello następujące funkcje:

* Jest automatycznie przesyłany jako zadanie przez hello usługa partia zadań po utworzeniu zadania hello.
* Jego jest zaplanowane tooexecute przed hello innych zadań w ramach zadania.
* Jego skojarzony węzeł jest hello toobe ostatniego usunąć z puli, gdy jest on downsized hello puli.
* Kończenie jego działania może być wiązanej toohello zakończenie wszystkich zadań w zadaniu hello.
* Zadanie Menedżer zadania otrzymuje hello najwyższy priorytet podczas musi toobe ponownego uruchomienia. Jeśli węzeł bezczynności nie jest dostępny, hello usługa partia zadań może zakończyć jedną hello inne uruchomione zadania w pomieszczeniu toomake puli hello na powitania zadania Menedżera zadań toorun.
* Zadanie Menedżer zadania jedno zadanie nie mają pierwszeństwo przed zadania hello innych zadań. W zadaniach przestrzegane są tylko priorytety na poziomie zadań.

### <a name="job-preparation-and-release-tasks"></a>Zadania przygotowania i zwolnienia zadań
Usługa Batch oferuje zadania podrzędne przygotowywania zadania na potrzeby konfiguracji przed wykonaniem zadania. Zadania podrzędne zwolnienia zadania to zadania konserwacji lub czyszczenia po wykonaniu zadania.

* **Zadanie przygotowanie zadania**: uruchamia zadanie przygotowanie zadania na wszystkie węzły obliczeniowe, które są toorun zaplanowanego zadania, przed każdą hello są wykonywane inne zadania. Można użyć danych toocopy zadania przygotowanie zadania, który jest współużytkowana przez wszystkie zadania, ale jest unikatowy toohello zadania, na przykład.
* **Zadanie zwolnienie zadania**: po ukończeniu zadania zadania Zwolnienie zadania działa na każdym węźle puli hello wykonywane co najmniej jedno zadanie. Na przykład można użyć zadania zlecenia zadań toodelete kopiowane dane to przez zadanie przygotowanie zadania hello lub toocompress i przekazywanie dzienników danych diagnostycznych.

Oba zadania przygotowanie i zadania wersji pozwalają toospecify toorun wiersza polecenia po wywołaniu hello zadań. Oferują one takie funkcje jak pobieranie plików, wykonywanie z podwyższonym poziomem uprawnień, niestandardowe zmienne środowiskowe, maksymalny czas trwania wykonywania, liczba ponownych prób i czas przechowywania pliku.

Więcej informacji na temat zadań przygotowania i zwolnienia zadań znajduje się w temacie [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md) (Uruchamianie zadań przygotowania i ukończenia zadań w węzłach obliczeniowych w usłudze Azure Batch).

### <a name="multi-instance-task"></a>Zadanie podrzędne obejmujące wiele wystąpień
A [zadań wielu wystąpieniach](batch-mpi.md) to zadanie, które jest skonfigurowany toorun na więcej niż jeden węzeł obliczeń jednocześnie. Korzystając z wielu wystąpień zadania, można włączyć wysokiej wydajności scenariuszach obliczeniowych, które wymagają określenia grupy węzły obliczeniowe, które są przydzielone razem tooprocess pojedyncze obciążenie (takie jak wiadomości interfejsu (Passing Interface)).

Szczegółowe omówienie na uruchomionych zadań MPI w partii przy użyciu biblioteki partiami platformy .NET hello, zapoznaj się z [użycie wielu wystąpień zadań toorun komunikat interfejsu (Passing Interface) aplikacji w partii zadań Azure](batch-mpi.md).

### <a name="task-dependencies"></a>Zależności zadań
[Zależności zadań](batch-task-dependencies.md), jako hello oznacza nazwę, pozwalają toospecify zadania zależne od ukończenia hello innych zadań przed jej wykonanie. Ta funkcja zapewnia obsługę sytuacje, w których zadanie "podrzędne" zużywa hello wyjściowych zadania "nadrzędnego"--lub gdy niektóre inicjowania wymaganych przez podrzędne zadania wykonuje zadania nadrzędnego. toouse tej funkcji, należy najpierw pierwszy zależności zadań Włącz na zadania wsadowego. Następnie dla każdego zadania, który jest zależny od innego (lub inne), określ hello zadania, które zależy od tego zadania.

Zależności zadań można skonfigurować scenariuszy, takich jak hello poniżej:

* *zadanie_podrzędne_B* zależy od *zadania_podrzędnego_A* (wykonywanie *zadania_podrzędnego_B* nie rozpocznie się, dopóki nie zostanie ukończone *zadanie_podrzędne_A*).
* *zadanie_podrzędne_C* zależy od *zadania_podrzędnego_A* i *zadania_podrzędnego_B*.
* *zadanie_podrzędne_D* zależy od wcześniejszego wykonania zakresu zadań podrzędnych, np. zadań od *1* do *10*.

Zapoznaj się z [zadań zależności w partii zadań Azure](batch-task-dependencies.md) i hello [TaskDependencies] [ github_sample_taskdeps] przykładowy kod w hello [azure partii próbek] [ github_samples] Repozytorium GitHub, aby uzyskać więcej informacji szczegółowych o tej funkcji.

## <a name="environment-settings-for-tasks"></a>Ustawienia środowiska dla zadań
Poszczególne zadania wykonywane przez hello usługa partia zadań ma dostęp tooenvironment zmiennych, które ustawia w węzłach obliczeniowych. Obejmuje to zdefiniowane przez hello usługa partia zadań zmienne środowiskowe ([usługa zdefiniowana][msdn_env_vars]) i zmiennych środowiskowych niestandardowych, które można zdefiniować dla zadań. Hello aplikacje i skrypty, których wykonanie zadań mają zmiennych środowiskowych toothese dostępu podczas wykonywania.

Można ustawić zmienne środowiskowe niestandardowe na poziomie hello zadań, definiując hello *ustawienia środowiska* właściwości dla tych obiektów. Na przykład, zobacz hello [dodać zadania tooa zadań] [ rest_add_task] operacji (interfejsu API REST partii) lub hello [CloudTask.EnvironmentSettings] [ net_cloudtask_env] i [ CloudJob.CommonEnvironmentSettings] [ net_job_env] właściwości w partiami platformy .NET.

Klient aplikacji lub usługi, można uzyskać zmiennych środowiskowych zadania, zarówno usługa zdefiniowana i niestandardowych, za pomocą hello [uzyskać informacje o zadaniu] [ rest_get_task_info] operacji (REST partii) lub uzyskując dostęp do Witaj [CloudTask.EnvironmentSettings] [ net_cloudtask_env] właściwości (partiami platformy .NET). Procesy wykonywane w węźle obliczeń mogą uzyskiwać dostęp do tych i innych zmiennych środowiskowych w węźle hello, na przykład za pomocą hello znanych `%VARIABLE_NAME%` (system Windows) lub `$VARIABLE_NAME` składni (Linux).

Pełna lista wszystkich zmiennych środowiskowych zdefiniowanych przez usługę jest dostępna w artykule dotyczącym [zmiennych środowiskowych węzłów obliczeniowych][msdn_env_vars].

## <a name="files-and-directories"></a>Pliki i katalogi
Każde zadanie podrzędne ma *katalog roboczy*, w którym tworzy pliki i katalogi (ich liczba może również wynosić zero). Ten katalog roboczy może służyć do przechowywania program hello uruchamiany przez zadanie hello, dane hello przetwarza, i hello wyjściowych przetwarzania hello, którą wykonuje. Wszystkie pliki i katalogi zadania są własnością hello zadań użytkownika.

Witaj usługa partia zadań udostępnia część hello system plików na węzeł jako hello *katalog główny*. Zadania można uzyskać dostępu do katalogu głównego hello odwołując hello `AZ_BATCH_NODE_ROOT_DIR` zmiennej środowiskowej. Więcej informacji na temat korzystania ze zmiennych środowiskowych znajduje się w temacie[Environment settings for tasks](#environment-settings-for-tasks) (Ustawienia środowiska dla zadań).

katalog główny Hello zawiera powitania po strukturę katalogów:

![Struktura katalogu węzła obliczeniowego][1]

* **udostępniony**: ten katalog zapewnia dostęp do odczytu/zapisu zbyt*wszystkie* zadań, które są uruchomione w węźle. Wszystkie zadania w węźle hello można tworzenia, odczytu, aktualizacji i usuwania plików w tym katalogu. Zadania można uzyskać dostępu do tego katalogu odwołując hello `AZ_BATCH_NODE_SHARED_DIR` zmiennej środowiskowej.
* **startup**: ten katalog jest używany jako katalog roboczy przez zadanie podrzędne uruchamiania. Wszystkie pliki hello węzła toohello pobrane przez zadanie uruchamiania hello są przechowywane w tym miejscu. zadania uruchamiania Hello można tworzenia, odczytu, aktualizacji i usuwania plików w tym katalogu. Zadania można uzyskać dostępu do tego katalogu odwołując hello `AZ_BATCH_NODE_STARTUP_DIR` zmiennej środowiskowej.
* **Zadania**: katalog jest tworzony dla każdego zadania w węźle hello. Jest on dostępny za pomocą odwołań do hello `AZ_BATCH_TASK_DIR` zmiennej środowiskowej.

    W każdym katalogu zadania usługa partia zadań hello tworzy katalog roboczy (`wd`) którego unikatowej ścieżki jest określona przez hello `AZ_BATCH_TASK_WORKING_DIR` zmiennej środowiskowej. Ten katalog zawiera zadania toohello dostęp do odczytu/zapisu. zadanie Hello można tworzenia, odczytu, aktualizacji i usuwania plików w tym katalogu. Ten katalog jest zachowane, oparte na powitania *RetentionTime* ograniczenie, które jest określone dla zadania hello.

    `stdout.txt`i `stderr.txt`: te pliki są zapisywane toohello folderu zadań podczas wykonywania hello hello zadania.

> [!IMPORTANT]
> Gdy węzeł zostanie usunięty z puli hello *wszystkie* z hello plików przechowywanych w węźle hello są usuwane.
>
>

## <a name="application-packages"></a>Pakiety aplikacji
Witaj [pakietów aplikacji](batch-application-packages.md) funkcja zapewnia łatwe zarządzanie i wdrażanie aplikacji toohello węzłów obliczeniowych w Twojej puli. Możesz przekazać i zarządzanie wieloma wersjami programu hello, które aplikacje są uruchamiane przez zadania, w tym ich pliki binarne i pliki obsługi. Następnie można automatycznie wdrażać lub jeden z tych aplikacji toohello obliczeniowe węzłów w puli.

Można określić pakietów aplikacji na poziomie hello puli i zadań. Po określeniu pakietów aplikacji w puli aplikacji hello jest węzeł tooevery wdrożonej w puli hello. Po określeniu pakietów aplikacji zadań aplikacja hello wdrożone tylko toonodes, które są zaplanowane co najmniej jeden toorun zadań hello zadania, bezpośrednio przed hello jest uruchamiany wiersz polecenia zadania.

Uchwyty partii hello szczegółowe informacje o pracy z usługi Azure Storage toostore pakiety aplikacji i wdrażać je węzłów toocompute, można uprościć kod i zarządzania koszty.

toofind więcej informacji na temat funkcji pakietu aplikacji hello, zapoznaj się z [wdrożyć aplikacje toocompute węzły z pakietami aplikacji partii](batch-application-packages.md).

> [!NOTE]
> Jeśli dodasz puli aplikacji pakietów tooan *istniejących* puli, musisz ponownie uruchomić jego węzły obliczeniowe dla węzłów toohello toobe wdrożone pakiety aplikacji hello.
>
>

## <a name="pool-and-compute-node-lifetime"></a>Okres istnienia puli i węzła obliczeniowego
Podczas projektowania rozwiązania partii zadań Azure, masz toomake decyzja o tym, jak i gdy pule są tworzone i jak długo wyliczenia węzłów w ramach tych pule są przechowywane.

W jednym zakończeniu spektrum hello można utworzyć puli dla każdego zadania, które można przesłać i usunąć pulę hello, jak jego zadań zakończenia wykonywania. Maksymalizację wykorzystania, ponieważ węzły hello są alokowane tylko, gdy potrzebne i zamknąć, jak są one bezczynności. Gdy to oznacza, że zadanie hello musi czekać, aż toobe węzłów hello przydzielone, jest ważne toonote, które zadania zaplanowane do uruchomienia, jak tylko węzły są dostępne oddzielnie, przydzielona i hello zadanie uruchamiania zostało zakończone. Partii jest *nie* poczekaj, aż wszystkie węzły w puli są dostępne przed przypisaniem zadania toohello węzłów. Dzięki temu zapewnia maksymalne wykorzystanie wszystkich dostępnych węzłów.

Na powitania drugiej spektrum hello, jeśli jest posiadanie zadania natychmiast rozpocząć hello najwyższy priorytet można można utworzyć pulę wcześniejsze i udostępnić jego węzłów przed przesłaniem zadania. W tym scenariuszu zadań można uruchomić natychmiast, ale węzłów może sit bezczynności podczas oczekiwania na ich toobe przypisane.

W przypadku zmiennego, ale ciągłego obciążenia zwykle jest stosowane rozwiązanie mieszane. Masz puli są przesyłane do wielu zadań, ale można skalować hello liczby węzłów w górę lub w dół zgodnie z toohello zadania obciążenia (zobacz [zasoby obliczeniowe skalowanie](#scaling-compute-resources) w powitania po sekcji). Można to zrobić w sposób reaktywny, w oparciu o bieżące obciążenie, lub aktywny, jeśli obciążenie można przewidzieć.

## <a name="virtual-network-vnet-and-firewall-configuration"></a>Konfiguracja sieci wirtualnej i zapory 

Podczas obsługi administracyjnej puli węzłów obliczeniowych w partii zadań Azure hello puli można skojarzyć z podsiecią Azure [sieć wirtualną (VNet)](../virtual-network/virtual-networks-overview.md). toolearn więcej informacji na temat tworzenia sieci wirtualnej z podsieciami, zobacz [Utwórz sieć wirtualną platformy Azure z podsieciami](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). 

 * Witaj sieci wirtualnej skojarzone z pulą musi być:

   * W hello Azure tego samego **region** jako hello konto partii zadań Azure.
   * W hello sam **subskrypcji** jako hello konto partii zadań Azure.

* Typ Hello obsługiwane sieci wirtualnej, zależy od tego, pule są przydzielaniem dla hello konta usługi partia zadań:

    - Jeśli hello puli alokacji dla konta wsadowego jest tryb tooBatch usługi, a następnie można przypisać toopools tylko sieci wirtualnej, utworzone za pomocą hello **konfiguracji usługi w chmurze**. Ponadto hello określona sieć wirtualna musi zostać utworzona z hello klasycznego modelu wdrażania. Sieci wirtualne utworzone za pomocą modelu wdrażania usługi Azure Resource Manager hello nie są obsługiwane.
 
    - Jeśli hello puli alokacji dla konta wsadowego jest tryb tooUser subskrypcji, a następnie można przypisać toopools tylko sieci wirtualnej, utworzone za pomocą hello **konfiguracji maszyny wirtualnej**. Pule utworzone za pomocą hello **konfiguracji usługi w chmurze** nie są obsługiwane. Witaj, skojarzone sieci wirtualnej mogą zostać utworzone przy użyciu modelu wdrażania usługi Azure Resource Manager hello lub hello klasycznego modelu wdrażania.

    Dla tabeli podsumowania obsługi sieci wirtualnej zgodnie z toopool Tryb alokacji, zobacz hello [Tryb alokacji puli](#pool-allocation-mode) sekcji.

* Jeśli tryb alokacji puli hello konta usługi partia zadań jest ustawiona tooBatch usługi, należy podać się, że uprawnienia dla hello tooaccess główna usługi partii hello sieci wirtualnej. Witaj sieci wirtualnej, należy przypisać hello [Classic Virtual Machine Contributor Role-Based kontroli dostępu (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/#classic-virtual-machine-contributor) roli toohello partii service principal. Jeśli hello określona rola RBAC nie został podany, usługa partia zadań hello zwraca 400 (nieprawidłowe żądanie). Rola hello tooadd w hello portalu Azure:

    1. Wybierz hello **sieci wirtualnej**, następnie **(IAM) kontroli dostępu** > **ról** > **Współautor·maszyny·wirtualnej**  >  **Dodać**.
    2. Na powitania **dodać uprawnienia** bloku, wybierz hello **Współautor·maszyny·wirtualnej** roli.
    3. Na powitania **dodać uprawnienia** bloku, wyszukiwanie hello interfejsu API partii. Wyszukaj każdy z tych ciągów z kolei do momentu znalezienia hello interfejsu API:
        1. **MicrosoftAzureBatch**.
        2. **Microsoft Azure Batch**. W przypadku nowszych dzierżaw usługi Azure AD może być używana ta nazwa.
        3. **ddbf3205-c6bd-46ae-8127-60eb93363864** jest identyfikator hello hello interfejsu API partii. 
    3. Wybierz hello nazwy głównej usługi interfejsu API partii. 
    4. Kliknij pozycję **Zapisz**.

        ![Przypisz jednostki usługi tooBatch roli współautora maszyny Wirtualnej](./media/batch-api-basics/iam-add-role.png)


* Hello Określona podsieć powinna mieć wystarczającej ilości wolnego **adresów IP** tooaccommodate hello łączna liczba węzłów docelowy; hello to znaczy sumę hello `targetDedicatedNodes` i `targetLowPriorityNodes` właściwości hello puli. Jeśli hello podsieci nie ma za mało dostępnych adresów IP, hello usługa partia zadań częściowo przydziela hello węzłów obliczeniowych w puli hello i zwraca błąd zmiany rozmiaru.

* Witaj określono podsieci musi Zezwalaj na komunikację z hello partii usługi toobe tooschedule stanie zadania na powitania węzłów obliczeniowych. Jeśli węzły obliczeniowe toohello komunikacji jest odrzucany przez **grupy zabezpieczeń sieci (NSG)** skojarzone z hello sieci wirtualnej, a następnie hello usługa partia zadań ustawia stan hello węzłów obliczeniowych hello zbyt**bezużyteczne**.

* Jeśli hello określona sieć wirtualna ma skojarzone **grup zabezpieczeń sieci (NSG)** i/lub **zapory**, a następnie kilka portów zarezerwowaną przez system, należy włączyć komunikacji przychodzącej:

- W przypadku pul utworzonych za pomocą konfiguracji maszyny wirtualnej włącz porty 29876 i 29877 oraz port 22 dla systemu Linux i port 3389 dla systemu Windows. 
- W przypadku pul utworzonych za pomocą konfiguracji usługi w chmurze włącz porty 10100, 20100 i 30100. 
- Włącz połączenia wychodzące tooAzure magazynu na porcie 443. Upewnij się również, że punkt końcowy usługi Azure Storage może zostać rozpoznany przez dowolne niestandardowe serwery DNS, które obsługują sieć wirtualną. W szczególności adresu URL formularza hello `<account>.table.core.windows.net` powinna być rozpoznawana.

    Witaj poniższej tabeli opisano hello ruchu przychodzącego portów, które muszą tooenable dla pul, które zostały utworzone z konfiguracją maszyny wirtualnej hello:

    |    Porty docelowe    |    Źródłowy adres IP      |    Czy usługa Batch dodaje sieciowe grupy zabezpieczeń?    |    Wymagane dla toobe maszyny Wirtualnej można używać?    |    Akcja użytkownika   |
    |---------------------------|---------------------------|----------------------------|-------------------------------------|-----------------------|
    |    <ul><li>Dla pul utworzone za pomocą konfiguracji maszyny wirtualnej hello: 29876, 29877</li><li>Dla pul utworzone z konfiguracją usługi w chmurze hello: 10100, 20100, 30100</li></ul>         |    Tylko adresy IP roli usługi Batch |    Tak. Wsadowe dodaje grupy NSG na poziomie hello tooVMs interfejsów (NIC), dołączony w sieci. Te sieciowe grupy zabezpieczeń zezwalają tylko na ruch z adresów IP roli usługi Batch. Nawet jeśli możesz otworzyć te porty dla całej sieci web hello, hello ruchu zostaną zablokowane na powitania karty sieciowej. |    Tak  |  Nie ma potrzeby toospecify NSG, ponieważ tylko adresy IP partii umożliwia wsadowe. <br /><br /> Jeśli jednak określisz sieciową grupę zabezpieczeń, upewnij się, że te porty zostały otwarte na potrzeby ruchu przychodzącego. <br /><br /> Jeśli określisz * jako hello źródłowy adres IP w sieci grupy NSG, partii doda grupy NSG na poziomie hello tooVMs kartę Sieciową podłączoną. |
    |    3389, 22               |    Użytkownik maszyny używane na potrzeby debugowania, tak aby zdalny dostęp do hello maszyny Wirtualnej.    |    Nie                                    |    Nie                     |    Dodaj grupy NSG, jeśli chcesz toopermit dostępu zdalnego (RDP/SSH) toohello maszyny Wirtualnej.   |                 

    Witaj w poniższej tabeli opisano hello port wychodzący konieczność tooenable toopermit dostępu tooAzure magazynu:

    |    Porty ruchu wychodzącego    |    Element docelowy    |    Czy usługa Batch dodaje sieciowe grupy zabezpieczeń?    |    Wymagane dla toobe maszyny Wirtualnej można używać?    |    Akcja użytkownika    |
    |------------------------|-------------------|----------------------------|-------------------------------------|------------------------|
    |    443    |    Azure Storage    |    Nie    |    Tak    |    Jeśli dodać żadnych grup NSG, upewnij się, że ten port jest otwarty toooutbound ruchu.    |


## <a name="scaling-compute-resources"></a>Skalowanie zasobów obliczeniowych
Z [automatyczne skalowanie](batch-automatic-scaling.md), usługa partia zadań hello dynamicznie zmieniać hello liczba węzłów obliczeniowych w puli, zgodnie z toohello bieżącego obciążenia i użycie zasobów obliczeniowych scenariusz może mieć. Dzięki temu można toolower hello całkowity koszt uruchamiania aplikacji przy użyciu tylko hello zasoby potrzebne i udostępnia te nie wymagają.

Automatyczne skalowanie można włączyć, pisząc [formułę automatycznego skalowania](batch-automatic-scaling.md#automatic-scaling-formulas) i kojarząc ją z pulą. Hello usługa partia zadań używa hello formuły toodetermine hello docelowej liczby węzłów w puli hello hello następnym interwale skalowania (interwał, z którym można skonfigurować). Można określić hello Ustawienia skalowania automatycznego dla puli, podczas jego tworzenia lub włączyć skalowanie później w puli. Można także zaktualizować hello skalowanie ustawienia w puli obsługą skalowania.

Na przykład możliwe, że zadanie wymaga czy przesłać bardzo dużej liczby toobe zadania wykonywane. Można przypisać skalowania puli toohello formuły, które można dostosować hello liczby węzłów w puli hello na podstawie hello bieżąca liczba zadań w kolejce i szybkość ukończenia hello hello zadań w zadaniu hello. Witaj usługa partia zadań okresowo ocenia formuła hello i zmienia rozmiar puli hello, na podstawie obciążenia i inne ustawienia formuły. Usługa Hello dodaje węzłów w chwili, gdy ma dużą liczbę zadań umieszczonych w kolejce i usuwa węzłów, gdy nie ma żadnych zadań w kolejce lub nie działają.

Formuła skalowania mogą być oparte na powitania następujące metryki:

* **Metryki czasu** są oparte na statystyki zbierane co pięć minut w hello określona liczba godzin.
* **Metryki zasobów** — na podstawie użycia procesora, wykorzystania przepustowości, użycia pamięci i liczby węzłów.
* **Metryki zadań podrzędnych** — na podstawie stanu zadania podrzędnego, takiego jak *Aktywne* (w kolejce), *Uruchomione* lub *Ukończone*.

Podczas automatycznego skalowania zmniejsza hello liczba węzłów obliczeniowych w puli, należy rozważyć sposób toohandle zadań, które są uruchomione w momencie hello hello zmniejszyć operacji. tooaccommodate tej, partii zapewnia *opcję dezalokacji węzła* obejmujących w formułach. Na przykład można określić, że uruchomione zadania są natychmiast zatrzymać, natychmiast zatrzymać i następnie umieszczony w kolejce do wykonania w innym węźle lub dozwolone toofinish przed hello węzeł zostanie usunięty z puli hello.

Więcej informacji na temat automatycznego skalowania aplikacji znajduje się w temacie [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) (Automatyczne skalowanie węzłów obliczeniowych w puli usługi Azure Batch).

> [!TIP]
> toomaximize obliczeniowe wykorzystania zasobów, ustaw hello docelowy liczbę węzłów toozero na końcu hello zadania, ale zezwalaj uruchomionych zadań toofinish.
>
>

## <a name="security-with-certificates"></a>Zabezpieczenia oparte na certyfikatach
Zazwyczaj potrzebne certyfikaty toouse zaszyfrować lub odszyfrować poufnych informacji dla zadania, takie jak klucz hello [konta magazynu Azure][azure_storage]. toosupport, możesz zainstalować certyfikaty na węzłach. Zaszyfrowanych kluczy tajnych są przekazywane tootasks przez parametry wiersza polecenia lub osadzone w jeden z zasobów zadań hello i hello zainstalowane certyfikaty mogą być używane toodecrypt je.

Użyj hello [Dodaj certyfikat] [ rest_add_cert] operacji (REST partii) lub [CertificateOperations.CreateCertificate] [ net_create_cert] — metoda (partiami platformy .NET) tooadd tooa certyfikatu konta usługi partia zadań. Następnie można skojarzyć hello certyfikatu przy użyciu nowej lub istniejącej puli. Gdy certyfikat jest skojarzony z pulą, usługa partia zadań hello instaluje certyfikat hello w każdym węźle hello puli. Hello usługa partia zadań instaluje odpowiednie certyfikaty hello podczas uruchamiania hello węzła, przed uruchomieniem żadnych zadań (w tym hello uruchamiania zadań i zadania Menedżer zadania).

Jeśli dodasz tooan certyfikaty *istniejących* puli, musisz ponownie uruchomić jego węzły obliczeniowe hello certyfikatów toobe stosowane toohello węzłów.

## <a name="error-handling"></a>Obsługa błędów
Może być konieczne toohandle błędów zarówno zadań i aplikacji w ramach rozwiązania partii.

### <a name="task-failure-handling"></a>Obsługa błędów zadań
Błędy zadań można podzielić na następujące kategorie:

* **Błędy przetwarzania wstępnego**

    Jeśli zadanie nie powiedzie się toostart, błąd przetwarzania wstępnego ustawiono hello zadania.  

    Błędy przetwarzania wstępnego może wystąpić, jeśli zadanie hello pliki zasobów zostały przeniesione, hello konta magazynu nie jest już dostępny lub wystąpił inny problem czy hello uniemożliwił pomyślne kopiowanie plików toohello węzła.

* **Błędy przekazywania plików**

    Jeśli przekazywania plików, które są określone dla zadania nie powiedzie się z jakiegokolwiek powodu, błąd przekazywania pliku wynosi hello zadania.

    Przekazywanie, mogą wystąpić błędy, jeśli hello SAS dostarczone dla uzyskiwania dostępu do magazynu Azure jest nieprawidłowy lub nie ma uprawnienia do zapisu, jeśli konto magazynu hello nie jest już dostępny lub inny problem uniemożliwiający hello pomyślne kopiowanie plików z pliku węzeł Hello.    

* **Błędy aplikacji**

    proces Hello, który jest określony za pomocą wiersza polecenia zadania hello również może zakończyć się niepowodzeniem. Witaj proces jest traktowany toohave nie powiodło się podczas przez proces hello, która jest wykonywana przez zadanie hello zostanie zwrócony kod zakończenia różną od zera (zobacz *kody zakończenia zadania* w następnej sekcji hello).

    Błędy aplikacji, można skonfigurować partii tooautomatically ponawiania hello zadanie w górę tooa określona liczba razy.

* **Błędy ograniczenia**

    Można ustawić ograniczenia, które określa hello wykonywania maksymalny czas trwania zadania lub zadania, hello *maxWallClockTime*. Może to być przydatne w przypadku zakończenia zadania, które nie są tooprogress.

    Przekroczenia hello maksymalną ilość czasu zadań hello jest oznaczony jako *ukończone*, ale kod zakończenia hello jest zbyt`0xC000013A` i hello *schedulingError* pole jest oznaczone jako `{ category:"ServerError", code="TaskEnded"}`.

### <a name="debugging-application-failures"></a>Błędy debugowania aplikacji
* `stderr` i `stdout`

    Podczas wykonywania aplikacja może powodować generowanie wyjście diagnostyczne służy tootroubleshoot problemów. Jak wspomniano w hello wcześniej sekcji [plików i katalogów](#files-and-directories), hello usługa partia zadań zapisuje wyjście standardowe i błąd standardowy output zbyt`stdout.txt` i `stderr.txt` plików w katalogu zadania hello na powitania węzła obliczeniowego. Używając hello portalu Azure lub jednego z toodownload wsadowego zestawów SDK hello tych plików. Na przykład można pobrać tych i innych plików na potrzeby rozwiązywania problemów przy użyciu [ComputeNode.GetNodeFile] [ net_getfile_node] i [CloudTask.GetNodeFile] [ net_getfile_task] hello biblioteki partiami platformy .NET.

* **Kody zakończenia zadania podrzędnego**

    Jak wspomniano wcześniej, zadanie zostanie oznaczone jako jako nieudane przez usługi partia zadań hello, jeśli proces hello, która jest wykonywana przez zadanie hello zwraca kod zakończenia różną od zera. Podczas procesu zadania, partii wypełnienie właściwości kodu zakończenia zadania hello z hello *zwracają kod procesu hello*. Jest ważne toonote, który jest kodem zakończenia zadania **nie** ustaleniami hello usługa partia zadań. Kod zakończenia zadania jest określana przez sam proces hello lub hello systemu operacyjnego, na których proces hello wykonywane.

### <a name="accounting-for-task-failures-or-interruptions"></a>Uwzględnianie błędów zadań lub przerw w zadaniach 
Od czasu do czasu zadania podrzędne mogą zakończyć się niepowodzeniem lub zostać przerwane. Witaj samą aplikację zadań może się nie powieść, może zostać przeprowadzony ponowny rozruch węzła hello, na które hello zadanie jest uruchomione lub węzła hello może zostać usunięta z puli hello podczas operacji zmiany rozmiaru w przypadku hello zasady dezalokacji puli zestaw węzłów tooremove natychmiast bez oczekiwania na toofinish zadania. We wszystkich przypadkach hello zadań mogą być automatycznie umieszczony w kolejce przez partię do wykonania w innym węźle.

Jest również możliwe toocause tymczasowy problem toohang zadań lub tooexecute zbyt długo potrwać. Można ustawić interwał powitania maksymalną wykonywania zadania. Po przekroczeniu hello wykonywania maksymalny interwał hello usługa partia zadań przerwań hello zadań aplikacji.

### <a name="connecting-toocompute-nodes"></a>Łączenie węzłów toocompute
Można wykonywać dodatkowe debugowania i rozwiązywania problemów, logując się w węźle obliczeń tooa zdalnie. Można użyć hello Azure toodownload portalu plików protokołu RDP (Remote Desktop) dla systemu Windows węzłów i uzyskać informacje o połączeniu Secure Shell (SSH) dla systemu Linux węzłów. Również można to zrobić za pomocą hello interfejsów API partii — na przykład [partiami platformy .NET] [ net_rdpfile] lub [Python partii](batch-linux-nodes.md#connect-to-linux-nodes-using-ssh).

> [!IMPORTANT]
> tooconnect tooa węzła za pośrednictwem protokołu RDP lub SSH, użytkownik musi najpierw utworzyć w węźle hello. toodo, można użyć hello portalu Azure, [Dodaj węzeł tooa konta użytkownika] [ rest_create_user] przy użyciu interfejsu API REST partii hello, wywołaj hello [ComputeNode.CreateComputeNodeUser] [ net_create_user] w partiami platformy .NET lub hello wywołania metody [add_user] [ py_add_user] metody w module języka Python partii hello.
>
>

### <a name="troubleshooting-problematic-compute-nodes"></a>Rozwiązywanie problemów z węzłami obliczeniowymi
W sytuacjach, w której niektóre z zadań kończy się niepowodzeniem partii klienta aplikacji lub usługi można zbadać metadane hello hello nie powiodło się zadania tooidentify błędna węzła. Każdy węzeł w puli otrzymuje unikatowy identyfikator, a hello węzeł, na którym uruchamiane jest zadanie jest uwzględniona w hello zadań metadanych. Po zidentyfikowaniu problemu dotyczącego węzła można wykonać kilka powiązanych czynności:

* **Ponowny rozruch węzła hello** ([REST][rest_reboot] | [.NET][net_reboot])

    Ponownie uruchomić węzeł hello można czasami wyczyszczone ukryty problemów, takich jak zablokowane lub awaria procesów. Należy pamiętać, że jeśli pulę używa zadanie uruchamiania lub zadanie używa zadanie przygotowanie zadania, są wykonywane po ponownym uruchomieniu węzła hello.
* **Odtworzyć z obrazu węzła hello** ([REST][rest_reimage] | [.NET][net_reimage])

    W węźle hello ponownie instaluje system operacyjny hello. Podobnie jak w przypadku ponowny rozruch węzła, uruchamiania zadań i zadania przygotowanie zadania są wykonywane ponownie, po hello węzeł ma zostać odtworzyć z obrazu.
* **Usuń węzeł hello z puli hello** ([REST][rest_remove] | [.NET][net_remove])

    Czasami jest konieczne toocompletely Usuń hello węzła z hello puli.
* **Wyłącz Planowanie zadań w węźle hello** ([REST][rest_offline] | [.NET][net_offline])

    Efektywnie trwa to hello węzła w trybie offline, aby kolejne zadania są przypisane tooit, ale umożliwia uruchamianie tooremain węzła hello i hello puli. Dzięki temu możesz tooperform dalsze badania hello Przyczyna awarii hello bez utraty danych hello zadania nie powiodło się i bez węzła hello przyczyną błędów dodatkowe zadania. Na przykład można wyłączyć harmonogramy w węźle hello następnie zadań [Zaloguj się w](#connecting-to-compute-nodes) tooexamine hello węzła Dzienniki zdarzeń i rozwiązywania problemów z innymi. Po zakończeniu badania, następnie przełączeniem węzła hello ponownie do trybu online, należy włączyć harmonogramy zadań ([REST][rest_online] | [.NET] [ net_online]), lub wykonaj jedną z hello inne akcje wymienione powyżej.

> [!IMPORTANT]
> Z każdego działania opisane w tej sekcji--ponowny rozruch, odtworzenia z obrazu, Usuń i Wyłącz Planowanie zadań — są możliwe toospecify obsługi zadania uruchomione w węźle hello podczas wykonywania akcji hello. Na przykład po wyłączeniu Planowanie zadań w węźle, za pomocą biblioteki klienta .NET partii hello, można określić [DisableComputeNodeSchedulingOption] [ net_offline_option] wyliczenia wartości toospecify czy zbyt**Przerwania** uruchamianie zadań, **Requeue** ich do planowania na innych węzłach lub zezwolić toocomplete zadań uruchomiona przed wykonaniem akcji hello (**TaskCompletion**).
>
>

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o hello [narzędzia i interfejsy API partii](batch-apis-tools.md) dostępne do tworzenia rozwiązań partii.
* Zapoznaj się z artykułem krok po kroku w przykładowej aplikacji partii [wprowadzenie hello biblioteki partii zadań Azure dla platformy .NET](batch-dotnet-get-started.md). Istnieje również [wersji języka Python](batch-python-tutorial.md) węzły obliczeniowe samouczek hello, który uruchamia obciążenia w systemie Linux.
* Pobieranie i tworzenie hello [Explorer partii] [ github_batchexplorer] przykładowy projekt do użycia podczas opracowywania rozwiązań partii. Przy użyciu hello Explorer partii, można wykonywać następujące hello i inne:

  * Monitorowanie pul i zadań w ramach konta usługi Batch i manipulowanie nimi
  * Pobieranie `stdout.txt`, `stderr.txt` i innych plików z węzłów
  * Tworzenie użytkowników w węzłach i pobieranie plików RDP do logowania zdalnego
* Dowiedz się, jak za[tworzenia pul węzły obliczeniowe Linux](batch-linux-nodes.md).
* Odwiedź hello [forum usługi partia zadań Azure] [ batch_forum] w witrynie MSDN. Hello forum jest bardzo umieścić tooask pytania, czy po prostu uczą się lub są eksperta w partii, używając.

[1]: ./media/batch-api-basics/node-folder-structure.png

[azure_storage]: https://azure.microsoft.com/services/storage/
[batch_forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch
[cloud_service_sizes]: ../cloud-services/cloud-services-sizes-specs.md
[msmpi]: https://msdn.microsoft.com/library/bb524831.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_sample_taskdeps]:  https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch_net_api]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[msdn_env_vars]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[net_cloudjob_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobmanagertask.aspx
[net_cloudjob_priority]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.priority.aspx
[net_cloudpool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_cloudtask_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.environmentsettings.aspx
[net_create_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.createcertificate.aspx
[net_create_user]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.createcomputenodeuser.aspx
[net_getfile_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getnodefile.aspx
[net_getfile_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.getnodefile.aspx
[net_job_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.commonenvironmentsettings.aspx
[net_multiinstancesettings]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_onalltaskscomplete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.onalltaskscomplete.aspx
[net_rdp]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getrdpfile.aspx
[net_reboot]: https://msdn.microsoft.com/library/azure/mt631495.aspx
[net_reimage]: https://msdn.microsoft.com/library/azure/mt631496.aspx
[net_remove]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.removefrompoolasync.aspx
[net_offline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.disableschedulingasync.aspx
[net_online]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.enableschedulingasync.aspx
[net_offline_option]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.disablecomputenodeschedulingoption.aspx
[net_rdpfile]: https://msdn.microsoft.com/library/azure/Mt272127.aspx
[vnet]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_netconf

[py_add_user]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.ComputeNodeOperations.add_user

[batch_rest_api]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[rest_add_job]: https://msdn.microsoft.com/library/azure/mt282178.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_cert]: https://msdn.microsoft.com/library/azure/dn820169.aspx
[rest_add_task]: https://msdn.microsoft.com/library/azure/dn820105.aspx
[rest_create_user]: https://msdn.microsoft.com/library/azure/dn820137.aspx
[rest_get_task_info]: https://msdn.microsoft.com/library/azure/dn820133.aspx
[rest_job_schedules]: https://msdn.microsoft.com/library/azure/mt282179.aspx
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx
[rest_multiinstancesettings]: https://msdn.microsoft.com/library/azure/dn820105.aspx#multiInstanceSettings
[rest_update_job]: https://msdn.microsoft.com/library/azure/dn820162.aspx
[rest_rdp]: https://msdn.microsoft.com/library/azure/dn820120.aspx
[rest_reboot]: https://msdn.microsoft.com/library/azure/dn820171.aspx
[rest_reimage]: https://msdn.microsoft.com/library/azure/dn820157.aspx
[rest_remove]: https://msdn.microsoft.com/library/azure/dn820194.aspx
[rest_offline]: https://msdn.microsoft.com/library/azure/mt637904.aspx
[rest_online]: https://msdn.microsoft.com/library/azure/mt637907.aspx

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
