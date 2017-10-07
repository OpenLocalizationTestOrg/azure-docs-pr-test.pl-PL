---
title: "wprowadzenie do usługi Azure Data Lake Store aaaUse tooget programu PowerShell | Dokumentacja firmy Microsoft"
description: "Użyj programu Azure PowerShell toocreate konto usługi Data Lake Store i wykonywać podstawowe operacje"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a>Rozpoczynanie pracy z usługą Azure Data Lake Store przy użyciu programu Azure PowerShell
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Zestaw SDK platformy .NET](data-lake-store-get-started-net-sdk.md)
> * [Zestaw SDK Java](data-lake-store-get-started-java-sdk.md)
> * [Interfejs API REST](data-lake-store-get-started-rest-api.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Dowiedz się, jak toouse toocreate programu Azure PowerShell usługi Azure Data Lake przechowywać konto i wykonywać podstawowe operacje, takie jak tworzenie folderów, przekazywanie i pobieranie plików danych, usuwanie konta itp. Aby uzyskać więcej informacji o usłudze Data Lake Store, zobacz [Omówienie usługi Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka wymagane są następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Program Azure PowerShell 1.0 lub nowszy**. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

## <a name="authentication"></a>Authentication
W tym artykule używa prostsze uwierzytelniania z Data Lake Store, na którym są tooenter zostanie wyświetlony monit o poświadczenia konta Azure. następnie podlega Hello dostępu poziomu tooData Lake Store konta i system plików poziom dostępu hello hello zalogowanego użytkownika. Istnieją inne podejścia jako dobrze tooauthenticate z usługi Data Lake Store, które są **uwierzytelniania użytkowników końcowych** lub **do usługi uwierzytelniania**. Aby uzyskać instrukcje i więcej informacji na temat tooauthenticate, zobacz [uwierzytelniania użytkowników końcowych](data-lake-store-end-user-authenticate-using-active-directory.md) lub [do usługi uwierzytelniania](data-lake-store-authenticate-using-active-directory.md).

## <a name="create-an-azure-data-lake-store-account"></a>Tworzenie konta usługi Azure Data Lake Store
1. Na pulpicie otwórz nowe okno programu Windows PowerShell, wprowadź powitania po toolog fragment w tooyour konto platformy Azure, ustawione hello subskrypcję i zarejestruj dostawcę usługi Data Lake Store hello. Gdy zostanie wyświetlony monit o toolog, upewnij się, że logujesz się jako jeden hello/właścicieli subskrypcji:

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. Konto usługi Azure Data Lake Store jest skojarzone z grupą zasobów platformy Azure. Rozpocznij od utworzenia grupy zasobów platformy Azure.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    ![Tworzenie grupy zasobów platformy Azure](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Tworzenie grupy zasobów platformy Azure")
3. Utwórz konto usługi Azure Data Lake Store. Nazwa Hello musi zawierać tylko małe litery i cyfry.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    ![Tworzenie konta usługi Azure Data Lake Store](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Tworzenie konta usługi Azure Data Lake Store")
4. Sprawdź, czy hello konto zostało utworzone pomyślnie.

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    Witaj output powinna to być **True**.

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a>Tworzenie struktur katalogów w usłudze Azure Data Lake Store
Można tworzyć katalogi w obszarze toomanage konta użytkownika usługi Azure Data Lake Store i przechowywania danych.

1. Określ katalog główny.

        $myrootdir = "/"
2. Utwórz nowy katalog o nazwie **mynewdirectory** w katalogu głównym określonej hello.

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. Sprawdź, czy ten hello nowy katalog został utworzony pomyślnie.

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    Go powinny być widoczne dane wyjściowe podobne hello następujące czynności:

    ![Weryfikowanie katalogu](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Weryfikowanie katalogu")

## <a name="upload-data-tooyour-azure-data-lake-store"></a>Przekazywanie danych tooyour Azure Data Lake Store
Możesz przekazać sklepu Lake tooData danych bezpośrednio na powitania tooa lub na poziomie katalogu utworzonego w ramach konta hello. Witaj poniższe fragmenty kodu przedstawiają sposób tooupload niektóre przykładowe dane toohello katalogu (**mynewdirectory**) utworzonego w poprzedniej sekcji hello.

Jeśli szukasz niektórych tooupload dane przykładowe, możesz pobrać hello **Ambulance Data** folderu z hello [repozytorium Git programu Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Pobierz plik hello i zapisz go w katalogu lokalnym na komputerze, na przykład C:\sampledata\.

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a>Zmienianie nazwy, pobieranie i usuwanie danych z usługi Data Lake Store
toorename pliku hello Użyj następującego polecenia:

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

toodownload pliku hello Użyj następującego polecenia:

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

toodelete pliku hello Użyj następującego polecenia:

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

Po wyświetleniu monitu wprowadź **Y** toodelete hello elementu. Jeśli masz więcej niż jeden plik toodelete, musisz podać wszystkie ścieżki hello rozdzielonych przecinkami.

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a>Usuwanie konta usługi Azure Data Lake Store
Użyj następującego polecenia toodelete hello Twoje konto usługi Data Lake Store.

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

Po wyświetleniu monitu wprowadź **Y** toodelete hello konta.

## <a name="performance-guidance-while-using-powershell"></a>Wskazówki dotyczące wydajności podczas korzystania z programu PowerShell

Poniżej przedstawiono hello najważniejszych ustawień, które mogą być tooget Zaczekaj hello najlepszą wydajność podczas korzystania z usługi Data Lake Store toowork środowiska PowerShell:

| Właściwość            | Domyślne | Opis |
|---------------------|---------|-------------|
| PerFileThreadCount  | 10      | Ten parametr umożliwia toochoose hello liczbę równoległych wątków przekazanie lub pobranie każdego pliku. Liczba ta reprezentuje hello max wątków, które mogą być przydzielone dla każdego pliku, ale może zostać mniej wątków w zależności od danego scenariusza (np. podczas przekazywania pliku o rozmiarze 1 KB, otrzymasz jeden wątek, nawet jeśli poprosić o 20 wątków).  |
| ConcurrentFileCount | 10      | Ten parametr jest przeznaczony konkretnie na potrzeby przekazywania lub pobierania folderów. Ten parametr określa liczbę hello równoczesnych plików, które można przekazać lub pobrać. Liczba ta reprezentuje hello maksymalną liczbę równoczesnych plików, które można przekazać lub pobrana w tym samym czasie, ale może zostać mniej współbieżności, w zależności od danego scenariusza (np. można przekazać dwóch plików, otrzymasz dwa przekazywania plików jednoczesnych, nawet wtedy, gdy na żądanie użytkownika 15). |

**Przykład**

To polecenie pobiera pliki z dysku lokalnego użytkownika toohello Azure Data Lake Store za pomocą 20 wątków na plik i 100 równoczesnych pliki.

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a>Jak ustalić hello tooset wartości dla parametrów?

Oto kilka użytecznych wskazówek.

* **Krok 1: Określanie liczby całkowitej wątku hello** — należy zacząć od obliczania hello wątku łączna liczba toouse. Zasadniczo powinno się używać 6 wątków na każdy rdzeń fizyczny.

        Total thread count = total physical cores * 6

    **Przykład**

    Przy założeniu, że używasz hello PowerShell poleceń z D14 maszyny Wirtualnej, która ma 16 rdzeni

        Total thread count = 16 cores * 6 = 96 threads


* **Krok 2: Oblicz PerFileThreadCount** -możemy obliczyć naszych PerFileThreadCount na podstawie rozmiaru hello hello plików. Pliki mniejsze niż 2,5 GB jest toochange nie konieczności tego parametru, ponieważ domyślny hello 10 jest wystarczająca. W przypadku plików większych niż 2,5 GB należy użyć 10 wątków jako podstawa hello hello pierwszy 2,5 GB i Dodaj 1 wątków dla każdego dodatkowego zwiększenia 256 MB rozmiaru pliku. Podczas kopiowania folderu zawierającego pliki o szerokim zakresie rozmiarów warto podzielić je na grupy złożone z plików o podobnym rozmiarze. Różne rozmiary plików mogą spowodować utratę optymalnej wydajności. Jeśli nie jest możliwe toogroup podobne rozmiary plików, należy ustawić PerFileThreadCount oparte na powitania największy rozmiar pliku.

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    **Przykład**

    Zakładając, że masz 100 plików od too10GB 1 GB, używamy hello 10 GB, jak hello największy rozmiar dla równanie, które będzie odczytywać podobnie następującej hello pliku.

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* **Krok 3: Oblicz ConcurrentFilecount** — liczba całkowita liczba wątków hello użycia i PerFileThreadCount toocalculate ConcurrentFileCount oparte na powitania po równości.

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    **Przykład**

    Na podstawie wartości przykład hello, który był używany firma Microsoft

        96 = 40 * ConcurrentFileCount

    Tak **ConcurrentFileCount** jest **2.4**, które firma Microsoft może zaokrąglania zbyt**2**.

### <a name="further-tuning"></a>Dalsze dostosowywanie

Mogą być wymagane dodatkowe dostrajania, ponieważ istnieje szereg toowork rozmiary plików z. Witaj powyżej obliczania sprawdza się, gdy wszystkie lub większość plików hello są większe i bliżej toohello zakresu 10GB. Jeśli natomiast istnieje wiele różnych rozmiarów plików, z czego wiele plików jest mniejszych, można zmniejszyć wartość parametru PerFileThreadCount. Dzięki zmniejszeniu hello PerFileThreadCount, firma Microsoft może zwiększyć ConcurrentFileCount. Tak Jeśli przyjęto założenie, że większość naszego plików są mniejsze hello 5GB zakresu, możemy ponownie wykonaj naszych obliczenia:

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

Tak **ConcurrentFileCount** będzie teraz 96/20, czyli 4.8 zaokrąglana zbyt**4**.

Można kontynuować tootune te ustawienia, zmieniając hello **PerFileThreadCount** górę i w dół w zależności od hello dystrybucji Twojej rozmiary plików.

### <a name="limitation"></a>Ograniczenia

* **Liczba plików jest mniejsza niż ConcurrentFileCount**: Jeśli hello liczby plików podczas przekazywania jest mniejszy niż hello **ConcurrentFileCount** obliczane, a następnie należy zmniejszyć  **ConcurrentFileCount** toobe toohello równy liczby plików. Można użyć dowolnego pozostałych tooincrease wątków **PerFileThreadCount**.

* **Zbyt wiele wątków**: Jeśli zwiększysz wątku liczba zbyt dużo bez zwiększania rozmiar klastra, należy uruchomić hello ryzyko pogorszenie wydajności. Może być rywalizacji problemy podczas przełączania kontekstu na powitania procesora CPU.

* **Za mało współbieżności**: Jeśli nie wystarcza hello współbieżności, a następnie klastra jest za mały. Można zwiększyć hello liczby węzłów w klastrze, który będzie zawierać więcej współbieżności.

* **Błędy ograniczania przepływności**: błędy ograniczania przepływności mogą wystąpić wówczas, gdy współbieżność jest zbyt wysoka. Jeśli widzisz ograniczania błędy, możesz zmniejszają hello lub skontaktuj się z nami.

## <a name="next-steps"></a>Następne kroki
* [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md)
* [Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Korzystanie z usługi Azure HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

