---
title: "pakiety aplikacji aaaInstall w węzłach obliczeniowych - partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Użyj funkcji pakietów aplikacji hello z tooeasily partii zadań Azure zarządzać wieloma aplikacjami i węzły obliczeniowe w wersji do instalacji w partii."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a>Wdrażanie aplikacji toocompute węzłów za pomocą pakietów aplikacji partii

Funkcja pakiety aplikacji Hello partii zadań Azure umożliwia łatwe zarządzanie aplikacji zadań i ich toohello wdrożenia obliczeniowe węzłów w puli. Pakiety aplikacji możesz przekazać i zarządzanie wieloma wersjami aplikacji hello, których uruchamianie zadań, łącznie z ich pliki pomocnicze. Można następnie automatycznie wdrożyć jeden lub więcej z tych aplikacji toohello obliczeniowe węzłów w puli.

W tym artykule przedstawiono sposób tooupload pakiety aplikacji w hello portalu Azure i zarządzać nimi. Następnie dowiesz się jak tooinstall je w puli węzły obliczeniowe z hello [partiami platformy .NET] [ api_net] biblioteki.

> [!NOTE]
> 
> Pakiety aplikacji są obsługiwane we wszystkich pulach usługi Batch utworzonych po 5 lipca 2017 r. Są one obsługiwane w pulach partii utworzyć między 10 marca 2016 i 5 2017 lipca tylko wtedy, gdy pula hello został utworzony za pomocą konfiguracji usługi w chmurze. Pule partii utworzone przed too10 marca 2016 r nie obsługują pakietów aplikacji.
>
> Witaj interfejsy API umożliwiające tworzenie i zarządzanie pakiety aplikacji są częścią hello [zarządzania partiami platformy .NET] [[api_net_mgmt]] biblioteki. Witaj interfejsy API do instalowania pakietów aplikacji w węźle obliczeń są częścią hello [partiami platformy .NET] [ api_net] biblioteki.  
>
> Funkcja pakiety aplikacji Hello opisanych tutaj zastępuje funkcji partii aplikacji hello dostępne w poprzednich wersjach usługi hello.
> 
> 

## <a name="application-package-requirements"></a>Wymagania dotyczące pakietu aplikacji
toouse pakietów aplikacji, należy za[połączyć konto usługi Azure Storage](#link-a-storage-account) tooyour konta usługi partia zadań.

Ta funkcja została wprowadzona w [interfejsu API REST partii] [ api_rest] wersji 2015-12-01.2.2 i hello odpowiadającego [partiami platformy .NET] [ api_net] wersji biblioteki 3.1.0. Firma Microsoft zaleca zawsze używać najnowszej wersji interfejsu API hello podczas pracy z partii.

> [!NOTE]
> Pakiety aplikacji są obsługiwane we wszystkich pulach usługi Batch utworzonych po 5 lipca 2017 r. Są one obsługiwane w pulach partii utworzyć między 10 marca 2016 i 5 2017 lipca tylko wtedy, gdy pula hello został utworzony za pomocą konfiguracji usługi w chmurze. Pule partii utworzone przed too10 marca 2016 r nie obsługują pakietów aplikacji.
>
>

## <a name="about-applications-and-application-packages"></a>Aplikacje i pakiety aplikacji — informacje
W partii zadań Azure *aplikacji* odwołuje się zestaw tooa numerów wersji plików binarnych, które mogą być automatycznie pobierane toohello węzłów obliczeniowych w puli. *Pakiet aplikacji* odwołuje się tooa *określonego zestawu* tych danych binarnych i reprezentuje danego *wersji* aplikacji hello.

![Diagramu wysokiego poziomu aplikacji i pakietów aplikacji][1]

### <a name="applications"></a>Aplikacje
Aplikacja w partii zawiera jeden lub więcej aplikacji, pakietów i opcje konfiguracji dla aplikacji hello. Na przykład aplikacji można określić hello domyślna aplikacja pakietu wersji tooinstall węzłów obliczeniowych i czy jego pakietów można zaktualizować lub usunąć.

### <a name="application-packages"></a>Pakiety aplikacji
Pakiet aplikacji jest plik zip, który zawiera pliki binarne aplikacji hello i pliki pomocnicze, które są wymagane dla aplikacji hello toorun zadania. Każdy pakiet aplikacji reprezentuje określoną wersję aplikacji hello.

Można określić pakietów aplikacji na poziomie hello puli i zadań. Podczas tworzenia puli lub zadania można określić co najmniej jeden z tych pakietów i (opcjonalnie) wersja.

* **Pakiety aplikacji w puli** są wdrażane za*co* węzła w puli hello. Gdy węzeł dołącza pulę i gdy jest ponownego rozruchu lub odtworzenia z obrazu wdrożenia aplikacji.
  
    Pakiety aplikacji w puli są odpowiednie, wszystkie węzły w puli wykonywania zadania. Podczas tworzenia puli, można dodać lub zaktualizować pakiety istniejącej puli, można określić co najmniej jednego pakietu aplikacji. Aktualizuj istniejącą pulę aplikacji pakietów, należy ponownie uruchomić jego węzły tooinstall hello nowego pakietu.
* **Zadanie pakietów aplikacji** są wdrażane tylko w węźle obliczeń tooa zaplanowane toorun zadania, po prostu, przed uruchomieniem zadania hello wiersza polecenia. Jeśli hello określony pakiet aplikacji i wersji już znajduje się w węźle hello, nie jest wdrożone i istniejący pakiet hello jest używany.
  
    Pakiety aplikacji zadań są przydatne w środowisku udostępnionych puli, której różne zadania są uruchamiane w jednej puli i hello puli nie zostanie usunięta po zakończeniu zadania. Jeśli zadanie ma mniejszą liczbę zadań niż węzłów w puli hello, pakiety aplikacji zadań można zminimalizować transfer danych, ponieważ aplikacja jest wdrożony toohello tylko węzły, które uruchamiania zadań.
  
    Inne scenariusze, które mogą korzystać z zadań pakiety aplikacji są zadań uruchamianych dużej aplikacji, ale tylko kilka zadań. Na przykład przetwarzania wstępnego etap lub zadanie scalania, gdzie aplikacja hello przetwarzanie wstępne lub merge jest ogromnych, może korzystać z zadań pakietów aplikacji.

> [!IMPORTANT]
> Ma ograniczeń na powitania liczba aplikacji i pakietów aplikacji w ramach konta usługi partia zadań i rozmiar pakietu maksymalną aplikacji hello. Zobacz [przydziały i limity dla usługi partia zadań Azure hello](batch-quota-limit.md) szczegółowe informacje o tych ograniczeniach.
> 
> 

### <a name="benefits-of-application-packages"></a>Korzyści wynikające z pakietów aplikacji
Pakiety aplikacji może uprościć kod hello rozwiązania partii i dolnym hello narzutów toomanage wymagane hello aplikacji uruchamianych zadań.

Z pakietami aplikacji zadania uruchamiania puli użytkownika nie ma toospecify długą listę tooinstall pliki pojedynczego zasobu w węzłach hello. Nie masz toomanually Zarządzanie wieloma wersjami plików aplikacji w usłudze Azure Storage lub na węzły. I nie ma potrzeby tooworry o generowaniu [adresy URL SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide dostępu toohello plików na Twoim koncie magazynu. Działa w tle hello z pakietów aplikacji usługi Azure Storage toostore partii i wdrażać je toocompute węzłów.

> [!NOTE] 
> Witaj łączny rozmiar zadania uruchamiania musi być mniejsza lub równa znaków too32768, w tym plików zasobów i zmiennych środowiskowych. Jeśli zadanie start przekracza ten limit, za pomocą pakietów aplikacji jest inną opcją. Można również utworzyć archiwum zip zawierającym pliki zasobów, przekaż go jako tooAzure obiektu blob magazynu i Rozpakuj go z wiersza polecenia hello rozpoczęcia zadania. 
>
>

## <a name="upload-and-manage-applications"></a>Przekazywanie aplikacji i zarządzanie nimi
Można użyć hello [portalu Azure] [ portal] lub hello [zarządzania partiami platformy .NET](batch-management-dotnet.md) pakietów aplikacji hello toomanage biblioteki w ramach konta usługi partia zadań. W hello następne sekcje kilka, zostanie najpierw przedstawiony sposób toolink konta magazynu, następnie omówiono Dodawanie aplikacji i pakietów i zarządzania nimi z hello portalu.

### <a name="link-a-storage-account"></a>Połącz konto magazynu
toouse pakietów aplikacji, należy najpierw połączyć tooyour konta usługi Azure Storage konta usługi partia zadań. Jeśli nie skonfigurowano jeszcze konta magazynu, hello portalu Azure Wyświetla hello ostrzeżenie po raz pierwszy kliknij hello **aplikacji** kafelka w hello **konto wsadowe** bloku.

> [!IMPORTANT]
> Obecnie partii obsługuje *tylko* hello **ogólnego przeznaczenia** typu konta magazynu, zgodnie z opisem w kroku 5, [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account)w [o Azure konta magazynu](../storage/common/storage-create-storage-account.md). Po połączeniu tooyour konta usługi Azure Storage konta usługi partia zadań link *tylko* **ogólnego przeznaczenia** konta magazynu.
> 
> 

![Ostrzeżenie "Nie skonfigurowano konta magazynu" w portalu Azure][9]

Witaj hello używa usługi partii skojarzone toostore konta magazynu pakietów aplikacji. Po połączeniu hello dwa konta partii można automatycznie wdrażać pakietów hello przechowywane w węzły obliczeniowe tooyour konta magazynu hello połączone. toolink tooyour konta magazynu konta usługi partia zadań, kliknij przycisk **ustawienia konta magazynu** na powitania **ostrzeżenie** bloku, a następnie kliknij przycisk **konta magazynu** na powitania **Konta magazynu** bloku.

![Wybierz bloku konto magazynu w portalu Azure][10]

Zaleca się utworzenie konta magazynu *w szczególności* do użytku z kontem usługi partia zadań i zaznacz je tutaj. Aby uzyskać szczegółowe informacje o tym, jak toocreate konta magazynu, zobacz "Tworzenie konta magazynu" w [konta usługi Azure Storage](../storage/common/storage-create-storage-account.md). Po utworzeniu konta magazynu, można je następnie połączyć konto usługi partia zadań tooyour przy użyciu hello **konta magazynu** bloku.

> [!WARNING]
> Hello usługa partia zadań używa usługi Azure Storage toostore pakietów aplikacji jako blokowych obiektów blob. Jesteś [rozliczany jako normalne] [ storage_pricing] hello blokowych obiektów blob danych. Można się, że rozmiar hello tooconsider i liczbę pakietów aplikacji, a okresowe usuwanie pakietów przestarzałe toominimize kosztów.
> 
> 

### <a name="view-current-applications"></a>Wyświetl bieżące aplikacje
tooview aplikacji hello konta partii zadań kliknij hello **aplikacji** elementu menu w menu po lewej stronie powitania podczas wyświetlania hello **konto wsadowe** bloku.

![Kafelek aplikacji][2]

Wybranie tej opcji menu otwiera hello **aplikacji** bloku:

![Lista aplikacji][3]

Witaj **aplikacji** wyświetla bloku hello identyfikator każdej aplikacji w ramach Twojego konta i hello następujące właściwości:

* **Pakiety**: hello numer wersji skojarzonych z tą aplikacją.
* **Wersja domyślna**: wersja aplikacji hello zainstalowane, jeśli nie wskazują wersji po określeniu aplikacji hello puli. To ustawienie jest opcjonalne.
* **Zezwalaj na aktualizacje**: hello wartość, która określa, czy pakiet aktualizacji, usuwanie i dodatki są dozwolone. Jeśli ta opcja jest ustawiona zbyt**nr**, pakiet aktualizacji i usunięć są wyłączone dla aplikacji hello. Można dodawać tylko nowe wersje pakietu aplikacji. Domyślnie Hello **tak**.

### <a name="view-application-details"></a>Wyświetlanie szczegółów aplikacji
tooopen hello bloku, który zawiera szczegóły hello aplikacji hello aplikacji, wybierz pozycję w hello **aplikacji** bloku.

![Szczegóły aplikacji][4]

W bloku szczegóły aplikacji hello można skonfigurować następujące ustawienia dla aplikacji hello.

* **Zezwalaj na aktualizacje**: Określ, czy można zaktualizować lub usunąć jego pakietów aplikacji. Zobacz "Aktualizowanie lub usuwanie pakietu aplikacji" w dalszej części tego artykułu.
* **Wersja domyślna**: Określ domyślną aplikację pakietu toodeploy toocompute węzłów.
* **Nazwa wyświetlana**: Określ przyjazną nazwę, która jest Twoje partii rozwiązania można użyć, gdy na przykład wyświetla informacje o aplikacji hello w hello interfejsu użytkownika usługi, która zapewniają tooyour klientów za pośrednictwem usługi partia zadań.

### <a name="add-a-new-application"></a>Dodaj nową aplikację
toocreate nowej aplikacji, Dodaj pakiet aplikacji i określ aplikacji nowy, unikatowy identyfikator. Witaj pierwszy pakiet aplikacji, który możesz dodać nowy identyfikator aplikacji hello tworzy również hello nowej aplikacji.

Kliknij przycisk **Dodaj** na powitania **aplikacji** hello tooopen bloku **nowej aplikacji** bloku.

![Nowy blok aplikacji w portalu Azure][5]

Witaj **nowej aplikacji** bloku zapewnia hello poniższe pola toospecify hello ustawienia nowej aplikacji i pakietu aplikacji.

**Identyfikator aplikacji**

To pole określa identyfikator hello nowej aplikacji, czyli podmiotu toohello standardowych reguł sprawdzania poprawności identyfikator partii Azure. dostępne są następujące reguły Hello zapewniające identyfikator aplikacji:

* W węzłach Windows hello identyfikator może zawierać dowolną kombinację znaków alfanumerycznych, łączniki i podkreślenia. W węzłach Linux są dozwolone tylko znaki alfanumeryczne oraz znaki podkreślenia.
* Nie może zawierać więcej niż 64 znaki.
* Musi być unikatowa w obrębie hello konta usługi partia zadań.
* Jest zachowywanie i bez uwzględniania wielkości liter.

**Wersja**

To pole określa hello wersji pakietu aplikacji hello przekazywany. Ciągi wersji są następujące reguły sprawdzania poprawności toohello podmiotu:

* W węzłach Windows hello ciąg wersji może zawierać dowolną kombinację znaków alfanumerycznych, łączniki, podkreślenia i kropki. W węzłach Linux hello ciąg wersji może zawierać tylko znaki alfanumeryczne oraz znaki podkreślenia.
* Nie może zawierać więcej niż 64 znaki.
* Musi być unikatowa w obrębie aplikacji hello.
* To zachowanie w przypadku i bez uwzględniania wielkości liter.

**Pakiet aplikacji**

To pole określa hello plik zip, który zawiera pliki binarne aplikacji hello i plików pomocniczych, które są wymagane tooexecute hello aplikacji. Kliknij przycisk hello **wybierz plik** pola lub hello tooand toobrowse ikonę folderu, wybierz plik zip, który zawiera pliki aplikacji.

Po wybraniu pliku, kliknij przycisk **OK** toobegin hello przekazywania tooAzure magazynu. Po zakończeniu operacji wysyłania hello hello portal wyświetla powiadomienie i zamyka hello bloku. W zależności od wielkości hello pliku hello to przekazywanie i hello szybkość połączenia sieciowego ta operacja może potrwać pewien czas.

> [!WARNING]
> Nie zamykaj hello **nowej aplikacji** bloku przed zakończeniem operacji wysyłania hello. W ten sposób spowoduje zatrzymanie procesu przekazywania hello.
> 
> 

### <a name="add-a-new-application-package"></a>Dodaj nowy pakiet aplikacji
tooadd nowej wersji pakietu aplikacji dla istniejącej aplikacji, wybierz aplikację w hello **aplikacji** bloku, kliknij przycisk **pakiety**, następnie kliknij przycisk **Dodaj** tooopen Witaj **Dodaj pakiet** bloku.

![Dodawanie bloku pakietu aplikacji w portalu Azure][8]

Jak widać, pola hello pasują do właściwości hello **nowej aplikacji** bloku, ale hello **identyfikator aplikacji** pole jest wyłączone. Tak samo jak dla nowej aplikacji hello, określ hello **wersji** nowego pakietu, Przeglądaj tooyour **pakiet aplikacji** zip pliku, a następnie kliknij przycisk **OK** tooupload hello pakiet.

### <a name="update-or-delete-an-application-package"></a>Aktualizowanie lub usuwanie pakietu aplikacji
tooupdate lub usuń istniejący pakiet aplikacji, otwórz hello szczegóły blok dla aplikacji hello kliknij **pakiety** tooopen hello **pakiety** bloku, kliknij hello **wielokropka**w wierszu hello pakietu aplikacji hello mają toomodify i wybierz akcję hello, które mają tooperform.

![Aktualizowanie lub usuwanie pakietu w portalu Azure][7]

**Aktualizacja**

Po kliknięciu **aktualizacji**, hello *pakiet aktualizacji* bloku jest wyświetlany. Ten blok jest podobne toohello *nowy pakiet aplikacji* bloku, jednak tylko pola wyboru pakietów hello jest włączona, umożliwiając toospecify nowe tooupload pliku ZIP.

![Blok pakietu aktualizacji w portalu Azure][11]

**Usuwanie**

Po kliknięciu **usunąć**, monit o usunięcie hello tooconfirm wersja pakietu hello i partii usuwa hello pakietu z magazynu Azure. Jeśli usuniesz hello domyślnej wersji aplikacji hello **wersja domyślna** ustawienie zostanie usunięte z aplikacji hello.

![Usuwanie aplikacji][12]

## <a name="install-applications-on-compute-nodes"></a>Instalowanie aplikacji na węzły obliczeniowe
Teraz, kiedy znasz już jak aplikacji toomanage pakietów hello portalu Azure, można omówiono sposób toodeploy ich toocompute węzłów i uruchom je z zadań wsadowych.

### <a name="install-pool-application-packages"></a>Zainstaluj pakiety aplikacji w puli
tooinstall pakietu aplikacji na wszystkich obliczeniowe węzłów w puli, należy określić co najmniej jeden pakiet aplikacji *odwołania* hello puli. pakiety aplikacji Hello określające dla puli są instalowane w każdym węźle obliczeń, w tym węźle dołącza hello puli oraz w przypadku węzła hello jest ponownego rozruchu lub odtworzenia z obrazu.

W partiami platformy .NET, należy określić jedną lub więcej [CloudPool][net_cloudpool].[ ApplicationPackageReferences] [ net_cloudpool_pkgref] podczas tworzenia nowej puli lub dla istniejącej puli. Witaj [ApplicationPackageReference] [ net_pkgref] klasa określa identyfikator aplikacji i wersji węzły obliczeniowe tooinstall w puli.

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> Jeśli wdrożenie pakietu aplikacji nie powiedzie się z jakiegokolwiek powodu, znaczniki usługi partii hello hello węzła [bezużyteczne][net_nodestate], i zadania nie są zaplanowane do uruchomienia w tym węźle. W takim przypadku należy **ponowne uruchomienie** hello węzła tooreinitiate hello pakietu wdrożenia. Ponownie uruchomić węzeł hello umożliwia również w węźle hello ponownie harmonogramy zadań.
> 
> 

### <a name="install-task-application-packages"></a>Zainstaluj pakiety aplikacji zadań
Podobne tooa puli, określ pakiet aplikacji *odwołania* zadania. Gdy zadanie jest zaplanowane toorun w węźle, pakietów hello jest pobrane i wyodrębnione właśnie, przed wykonaniem zadań hello wiersza polecenia. Jeśli określonego pakietu i wersja jest już zainstalowany w węźle hello, hello pakietu nie jest pobierana, a istniejący pakiet hello jest używany.

tooinstall pakiet aplikacji zadanie konfigurowania zadania hello [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] właściwości:

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a>Wykonywania aplikacji hello zainstalowany
Hello pakietów określonych dla puli lub zadania zostaną pobrane i wyodrębnione tooa o nazwie katalogu w hello `AZ_BATCH_ROOT_DIR` hello węzła. Partii tworzy również zmiennej środowiskowej, zawierający hello toohello ścieżki o nazwie katalogu. Podczas odwoływania się do aplikacji hello w węźle hello, wiersze poleceń z zadań używania tej zmiennej środowiskowej. 

W węzłach systemu Windows hello zmiennej znajduje się w hello następującego formatu:

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

W węzłach Linux hello format jest nieco inne. Kropki (.), łączniki (-) i znaki numeru (#) są spłaszczoną toounderscores w zmiennej środowiskowej hello. Na przykład:

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

`APPLICATIONID`i `version` są wartości, które odpowiadają toohello aplikacji i wersję pakietu został określony dla wdrożenia. Na przykład, jeśli określono tej wersji 2.7 aplikacji *mieszarce* należy zainstalować na węzłach systemu Windows, Twoje wierszy polecenia zadania użyje tego tooaccess zmiennej środowiskowej jej pliki:

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

W węzłach Linux Określ zmienną środowiskową hello w następującym formacie:

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

Podczas przekazywania pakietu aplikacji, można określić węzły obliczeniowe tooyour toodeploy wersja domyślna. Jeśli wybrano domyślną wersję aplikacji hello wersji sufiks można pominąć w przypadku odwołania aplikacji hello. Możesz określić hello domyślnej wersji aplikacji hello portalu Azure, w bloku aplikacji hello, jak pokazano w [przekazywanie aplikacji i zarządzanie nimi](#upload-and-manage-applications).

Na przykład jeśli ustawisz "2.7" jako hello wersja domyślna dla aplikacji *mieszarce*i zadania odwołania hello następującej zmiennej środowiskowej, a następnie węzły Windows wykona wersji 2.7:

`AZ_BATCH_APP_PACKAGE_BLENDER`

Hello poniższy fragment kodu przedstawia przykład wiersza polecenia zadania uruchamiająca hello domyślnej wersji hello *mieszarce* aplikacji:

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> Zobacz [ustawienia środowiska dla zadań](batch-api-basics.md#environment-settings-for-tasks) w hello [Przegląd funkcji partii](batch-api-basics.md) Aby uzyskać więcej informacji na temat ustawień środowiska węzła obliczeń.
> 
> 

## <a name="update-a-pools-application-packages"></a>Aktualizowanie pakietów aplikacji puli
Jeśli skonfigurowano już istniejącą pulę z pakietem aplikacji, można określić nowy pakiet dla hello puli. Jeśli określisz nowe odwołanie pakietu dla puli, zastosuj następujące hello:

* Witaj, usługa partia zadań instaluje hello nowo określonego pakietu na wszystkie nowe węzły, które Dołącz do puli hello i istniejący węzeł, który jest ponownego rozruchu lub odtworzenia z obrazu.
* Węzły, które znajdują się już w puli hello podczas aktualizacji odwołania do pakietu hello nie są instalowane automatycznie nowy pakiet aplikacji hello obliczeń. Obliczeniowe te węzły, należy ponownie uruchomić lub ponownie tooreceive hello nowego pakietu.
* Po wdrożeniu nowego pakietu hello utworzone zmiennych środowiskowych odzwierciedlają hello nowej aplikacji będzie odwoływał się pakiet.

W tym przykładzie hello istniejącej puli ma wersji 2.7 hello *mieszarce* aplikacji skonfigurowany jako jeden z jego [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref]. węzły tooupdate hello puli z wersją 2.76b, określić nową [ApplicationPackageReference] [ net_pkgref] hello nowej wersji i zatwierdzania hello zmiany.

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

Teraz, gdy hello nowa wersja została skonfigurowana, hello usługa partia zadań instaluje wersję 2.76b tooany *nowe* węzła, w której jest przyłączany hello puli. tooinstall 2.76b na powitania węzłów, które są *już* w puli hello ponownego rozruchu lub je odtworzyć. Należy zwrócić uwagę zachowanie hello pliki z poprzedniego wdrożenia pakietu po ponownym rozruchu węzłów.

## <a name="list-hello-applications-in-a-batch-account"></a>Lista aplikacji hello w ramach konta usługi partia zadań
Można wyświetlić listę aplikacji hello i ich pakietów w ramach konta usługi partia zadań, za pomocą hello [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] metody.

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a>Dobiega końca
Z pakietów aplikacji możesz pomóc klientom wybierz aplikacji hello dla swoich zadań i określ hello dokładnej wersji toouse podczas przetwarzania zadania z usługą przetwarzania wsadowego. Może także zapewnienia możliwości hello tooupload Twojego klientów i śledzenie własne aplikacje w usłudze.

## <a name="next-steps"></a>Następne kroki
* Witaj [interfejsu API REST partii] [ api_rest] oferuje także funkcje obsługi toowork pakietów aplikacji. Na przykład, zobacz hello [applicationPackageReferences] [ rest_add_pool_with_packages] element [Dodaj konto tooan puli] [ rest_add_pool] informacje na temat toospecify tooinstall pakietów przy użyciu hello interfejsu API REST. Zobacz [aplikacji] [ rest_applications] szczegółowe informacje o sposobie tooobtain informacje o aplikacji przy użyciu hello interfejsu API REST partii.
* Dowiedz się, jak tooprogrammatically [Zarządzanie kontami partii zadań Azure i przydziały zarządzania partiami platformy .NET](batch-management-dotnet.md). Witaj [zarządzania partiami platformy .NET][api_net_mgmt] biblioteki można włączyć funkcji Tworzenie i usuwanie konta wsadowego aplikacji lub usługi.

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "Diagram ogólny pakietów aplikacji"
[2]: ./media/batch-application-packages/app_pkg_02.png "Kafelka aplikacji w portalu Azure"
[3]: ./media/batch-application-packages/app_pkg_03.png "Blok aplikacje w portalu Azure"
[4]: ./media/batch-application-packages/app_pkg_04.png "Blok szczegółów aplikacji w portalu Azure"
[5]: ./media/batch-application-packages/app_pkg_05.png "Nowy blok aplikacji w portalu Azure"
[7]: ./media/batch-application-packages/app_pkg_07.png "Aktualizowanie lub usuwanie pakietów listy rozwijanej w portalu Azure"
[8]: ./media/batch-application-packages/app_pkg_08.png "Nowy blok pakietu aplikacji w portalu Azure"
[9]: ./media/batch-application-packages/app_pkg_09.png "Alert nie połączonego konta magazynu"
[10]: ./media/batch-application-packages/app_pkg_10.png "Wybierz bloku konto magazynu w portalu Azure"
[11]: ./media/batch-application-packages/app_pkg_11.png "Blok pakietu aktualizacji w portalu Azure"
[12]: ./media/batch-application-packages/app_pkg_12.png "Usuń okno dialogowe potwierdzenia pakiet w portalu Azure"
