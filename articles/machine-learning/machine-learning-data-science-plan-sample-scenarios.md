---
title: "aaaIdentify zaawansowanych scenariuszy analizy dla usługi Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Wybierz odpowiednie scenariusze hello robić, zaawansowane analizy predykcyjnej z hello proces nauki danych Team."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a>Scenariusze zaawansowanej analizy w usłudze Azure Machine Learning
W tym artykule omówiono hello różnych źródeł danych przykładowych i scenariusze docelowe, które są obsługiwane przez hello [zespołu danych nauki procesu (TDSP)](data-science-process-overview.md). Witaj TDSP zapewnia systematyczne podejście toocollaborate zespołów na tworzeniu aplikacji inteligentnego. scenariusze Hello przedstawionych w tym miejscu przedstawiono opcje dostępne w hello przetwarzania danych w przepływie pracy, które są zależne od właściwości danych hello, lokalizacje źródłowe i repozytoriów docelowego na platformie Azure.

Witaj **drzewa decyzyjnego** dla wybranie hello przykładowe scenariusze, które jest odpowiednie dla danych i cel są prezentowane w ostatniej sekcji hello.

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

Przedstawia informacje o poszczególnych hello następujące sekcje przykładowy scenariusz. Dla każdego scenariusza nauki danych lub zaawansowana analityka przepływu i obsługi zasobów platformy Azure są wyświetlane.

> [!NOTE]
> **Wszystkie następujące scenariusze hello musisz:**
> <br/>
> 
> * [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md)
>   <br/>
> * [Utwórz obszar roboczy usługi Azure Machine Learning](machine-learning-create-workspace.md)
> 
> 

## <a name="smalllocal"></a>Scenariusz \#1: mały toomedium tabelarycznym zestawu danych w lokalnych plikach
![Toomedium małych plików lokalnych][1]

#### <a name="additional-azure-resources-none"></a>Dodatkowe zasoby platformy Azure: Brak
1. Zaloguj się toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
2. Przekaż zestawu danych.
3. Tworzenie przepływu eksperymentu uczenia maszynowego Azure począwszy przekazane zestawów danych.

## <a name="smalllocalprocess"></a>Scenariusz \#2: małe toomedium zestawu danych lokalnych plików, które wymagają przetworzenia
![Mała toomedium lokalnych plików z przetwarzaniem][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (notesu IPython server)
1. Utwórz maszynę wirtualną platformy Azure, systemem IPython notesu.
2. Przekaż kontenera magazynu Azure tooan danych.
3. Wstępnie przetworzyć i czyszczenia danych w notesie IPython, uzyskiwanie dostępu do danych z kontenera magazynu systemu Azure.
4. Przekształcanie danych, toocleaned w formie tabelarycznej.
5. Zapisz przekształcone dane w obiektach blob Azure.
6. Zaloguj się toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
7. Odczytywanie danych hello z obiekty BLOB platformy Azure przy użyciu hello [i zaimportuj dane] [ import-data] modułu.
8. Tworzenie przepływu eksperymentu uczenia maszynowego Azure począwszy pozyskiwane zestawów danych.

## <a name="largelocal"></a>Scenariusz \#3: dużego zestawu danych lokalnych plików przeznaczonych dla obiektów blob Azure
![Dużych plików lokalnych][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (notesu IPython server)
1. Utwórz maszynę wirtualną platformy Azure, systemem IPython notesu.
2. Przekaż kontenera magazynu Azure tooan danych.
3. Wstępnie przetworzyć i czyszczenia danych w notesie IPython, dostęp do danych z obiektów blob Azure.
4. Przekształcanie danych, toocleaned w formie tabelarycznej, w razie potrzeby.
5. Eksplorowanie danych i tworzenie funkcji zgodnie z potrzebami.
6. Wyodrębnij przykładowych danych w małych i średnich.
7. Zapisz hello próbce danych w obiektach blob Azure.
8. Zaloguj się toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
9. Odczytywanie danych hello z obiekty BLOB platformy Azure przy użyciu hello [i zaimportuj dane] [ import-data] modułu.
10. Tworzenie przepływu eksperymentu uczenia maszynowego Azure począwszy pozyskiwane zestawów danych.

## <a name="smalllocaltodb"></a>Scenariusz \#4: mały toomedium zestawu danych lokalnych plików przeznaczonych dla programu SQL Server w maszynie wirtualnej platformy Azure
![Mała toomedium tooSQL lokalne pliki bazy danych na platformie Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (SQL Server / Notes IPython serwera)
1. Utwórz maszynę wirtualną platformy Azure z programu SQL Server + IPython notesu.
2. Przekaż kontenera magazynu Azure tooan danych.
3. Wstępnie przetworzyć i czyszczenia danych w kontenerze magazynu platformy Azure przy użyciu IPython notesu.
4. Przekształcanie danych, toocleaned w formie tabelarycznej, w razie potrzeby.
5. Zapisywanie plików danych lokalnych tooVM (notesu IPython działa na maszynie Wirtualnej, dysków lokalnych można znaleźć dysków tooVM).
6. Dane tooSQL serwera bazy danych obciążenia uruchomione na maszynie Wirtualnej platformy Azure.
   
   Opcja \#1: użycie programu SQL Server Management Studio.
   
   * TooSQL logowania maszyny Wirtualnej serwera
   * Uruchom program SQL Server Management Studio.
   * Tworzenie tabel bazy danych i obiekt docelowy.
   * Użyj jednej z zbiorczego hello importowanie metody tooload hello danych z plików lokalnej maszyny Wirtualnej.
   
   Opcja \#2: przy użyciu IPython notesu — nie zaleca się dla średnich i większych zestawów danych
   
   <!-- -->    
   * Używanie tooaccess ciąg połączenia ODBC programu SQL Server na maszynie Wirtualnej.
   * Tworzenie tabel bazy danych i obiekt docelowy.
   * Użyj jednej z zbiorczego hello importowanie metody tooload hello danych z plików lokalnej maszyny Wirtualnej.
7. Eksploruj dane, należy utworzyć funkcje zgodnie z potrzebami. Należy zauważyć, że funkcje hello nie toobe zmaterializowany w tabelach bazy danych hello. Tylko Pamiętaj toocreate niezbędne zapytania hello je.
8. Podejmowanie decyzji o rozmiarze przykładowych danych, jeśli wymagane lub pożądane.
9. Zaloguj się toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
10. Witaj odczytu danych bezpośrednio z hello SQL Server przy użyciu hello [i zaimportuj dane] [ import-data] modułu. Wklej hello niezbędne kwerendę, która umożliwia wyodrębnianie pól, tworzy funkcje i przykłady danych, w razie potrzeby bezpośrednio w hello [i zaimportuj dane] [ import-data] zapytania.
11. Tworzenie przepływu eksperymentu uczenia maszynowego Azure począwszy pozyskiwane zestawów danych.

## <a name="largelocaltodb"></a>Scenariusz \#5: dużego zestawu danych w lokalnych plikach, docelowa programu SQL Server w maszynie Wirtualnej platformy Azure
![TooSQL dużych plików lokalnej bazy danych na platformie Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (SQL Server / Notes IPython serwera)
1. Utwórz maszynę wirtualną platformy Azure z programu SQL Server oraz serwer IPython notesu.
2. Przekaż kontenera magazynu Azure tooan danych.
3. (Opcjonalnie) Wstępnie przetworzyć i czyszczenia danych.
   
   a.  Wstępnie przetworzyć i czyszczenia danych w notesie IPython, uzyskiwanie dostępu do danych z platformy Azure
   
       blobs.
   
   b.  Przekształcanie danych, toocleaned w formie tabelarycznej, w razie potrzeby.
   
   c.  Zapisywanie plików danych lokalnych tooVM (notesu IPython działa na maszynie Wirtualnej, dysków lokalnych można znaleźć dysków tooVM).
4. Dane tooSQL serwera bazy danych obciążenia uruchomione na maszynie Wirtualnej platformy Azure.
   
   a.  TooSQL logowania maszyny Wirtualnej serwera.
   
   b.  Jeśli nie już zapisany na danych, pobieranie plików danych z platformy Azure
   
       storage container toolocal-VM folder.
   
   c.  Uruchom program SQL Server Management Studio.
   
   d.  Tworzenie tabel bazy danych i obiekt docelowy.
   
   e.  Użyj jednej z zbiorczego hello Importuj metody tooload hello dane.
   
   f.  Jeśli sprzężeń tabel są wymagane, tworzyć sprzężenia tooexpedite indeksów.
   
   > [!NOTE]
   > Szybkość wczytywania rozmiary dużej ilości danych, zalecane jest utworzenie partycjonowane tabele i zbiorczego importowania danych hello równolegle. Aby uzyskać więcej informacji, zobacz [tabel na partycje tooSQL równoległych importu danych](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
   > 
   > 
5. Eksploruj dane, należy utworzyć funkcje zgodnie z potrzebami. Należy zauważyć, że funkcje hello nie toobe zmaterializowany w tabelach bazy danych hello. Tylko Pamiętaj toocreate niezbędne zapytania hello je.
6. Podejmowanie decyzji o rozmiarze przykładowych danych, jeśli wymagane lub pożądane.
7. Zaloguj się toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
8. Witaj odczytu danych bezpośrednio z hello SQL Server przy użyciu hello [i zaimportuj dane] [ import-data] modułu. Wklej hello niezbędne kwerendę, która umożliwia wyodrębnianie pól, tworzy funkcje i przykłady danych, w razie potrzeby bezpośrednio w hello [i zaimportuj dane] [ import-data] zapytania.
9. Proste przepływu eksperymentu uczenia maszynowego Azure, począwszy od dataset przekazany

## <a name="largedbtodb"></a>Scenariusz \#6: dużego zestawu danych w programie SQL Server bazy danych lokalnych, przeznaczonych dla programu SQL Server w maszynie wirtualnej platformy Azure
![Duże bazy danych SQL tooSQL lokalnej bazy danych na platformie Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (SQL Server / Notes IPython serwera)
1. Utwórz maszynę wirtualną platformy Azure z programu SQL Server oraz serwer IPython notesu.
2. Użyj jednej z danych hello wyeksportować metody tooexport hello danych z pliki toodump programu SQL Server.
   
   > [!NOTE]
   > Jeśli zdecydujesz toomove wszystkie dane z bazy danych z lokalnego hello, alternatywne (szybsze) metoda toomove hello pełnej bazy danych toothe wystąpienie programu SQL Server na platformie Azure. Pomiń hello kroki tooexport danych, Utwórz bazę danych i obciążenia/import danych toohello docelowej z bazy danych i wykonaj hello alternatywna metoda.
   > 
   > 
3. Przekaż kontenera magazynu tooAzure plików zrzutu.
4. Obciążenia hello danych tooa bazy danych SQL Server uruchomiony na maszynie wirtualnej platformy Azure.
   
   a.  Toohello logowania maszyny Wirtualnej programu SQL Server.
   
   b.  Pobieranie plików danych z folderu lokalnego wirtualna toohello kontenera magazynu Azure.
   
   c.  Uruchom program SQL Server Management Studio.
   
   d.  Tworzenie tabel bazy danych i obiekt docelowy.
   
   e.  Użyj jednej z zbiorczego hello Importuj metody tooload hello dane.
   
   f.  Jeśli sprzężeń tabel są wymagane, tworzyć sprzężenia tooexpedite indeksów.
   
   > [!NOTE]
   > Szybkość wczytywania rozmiary dużej ilości danych, należy utworzyć toobulk importu hello danych i tabele partycjonowane równolegle. Aby uzyskać więcej informacji, zobacz [tabel na partycje tooSQL równoległych importu danych](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
   > 
   > 
5. Eksploruj dane, należy utworzyć funkcje zgodnie z potrzebami. Należy zauważyć, że funkcje hello nie toobe zmaterializowany w tabelach bazy danych hello. Tylko Pamiętaj toocreate niezbędne zapytania hello je.
6. Podejmowanie decyzji o rozmiarze przykładowych danych, jeśli wymagane lub pożądane.
7. Zaloguj się toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
8. Witaj odczytu danych bezpośrednio z hello SQL Server przy użyciu hello [i zaimportuj dane] [ import-data] modułu. Wklej hello niezbędne kwerendę, która umożliwia wyodrębnianie pól, tworzy funkcje i przykłady danych, w razie potrzeby bezpośrednio w hello [i zaimportuj dane] [ import-data] zapytania.
9. Począwszy od dataset przekazany prosty przepływ eksperymentu uczenia maszynowego Azure.

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a>Alternatywna metoda toocopy pełnej bazy danych z lokalnego programu SQL Server tooAzure bazy danych SQL
![Odłączanie lokalnej bazy danych i Dołącz tooSQL bazy danych na platformie Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Dodatkowe zasoby platformy Azure: maszyny wirtualnej platformy Azure (SQL Server / Notes IPython serwera)
tooreplicate hello całej bazy danych SQL Server w maszyną Wirtualną programu SQL Server, należy skopiować bazę danych z jednego serwera/lokalizacji tooanother, przy założeniu, że hello bazy danych można wykonać tymczasowo w trybie offline. Możesz to zrobić w hello Eksplorator obiektów SQL Server Management Studio lub za pomocą hello równoważnych poleceń języka Transact-SQL.

1. Odłączanie bazy danych hello w lokalizacji źródłowej hello. Aby uzyskać więcej informacji, zobacz [odłączyć bazy danych](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).
2. W oknie Eksploratora Windows lub wiersza polecenia systemu Windows hello kopiowania odłączyć plik bazy danych lub pliki i pliku dziennika lub lokalizacji docelowej toohello pliki na powitania maszyna wirtualna na platformie Azure SQL Server.
3. Dołącz wystąpienia programu SQL Server hello kopiowane pliki toohello docelowej. Aby uzyskać więcej informacji, zobacz [dołączyć bazę danych](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).

[Przenoszenie bazy danych przy użyciu odłączyć i dołączyć (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)

## <a name="largedbtohive"></a>Scenariusz \#7: danych Big data w lokalnych plikach docelowa baza danych gałęzi w klastrach usługi Azure HDInsight Hadoop
![Dane big data w celu lokalnego gałęzi][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a>Dodatkowe zasoby platformy Azure: klastra usługi Hadoop w usłudze Azure HDInsight i maszyny wirtualnej platformy Azure (notesu IPython server)
1. Utwórz maszynę wirtualną platformy Azure, usługami IPython notesu.
2. Tworzenie klastra usługi Azure HDInsight Hadoop.
3. (Opcjonalnie) Wstępnie przetworzyć i czyszczenia danych.
   
   a.  Wstępnie przetworzyć i czyszczenia danych w notesie IPython, uzyskiwanie dostępu do danych z platformy Azure
   
       blobs.
   
   b.  Przekształcanie danych, toocleaned w formie tabelarycznej, w razie potrzeby.
   
   c.  Zapisywanie plików danych lokalnych tooVM (notesu IPython działa na maszynie Wirtualnej, dysków lokalnych można znaleźć dysków tooVM).
4. Przekazywanie danych toohello domyślny kontener klastra Hadoop hello wybrany w hello krok 2.
5. Dane tooHive bazy danych obciążenia w klastrze usługi Azure HDInsight Hadoop.
   
   a.  Zaloguj się za toohello węzła głównego klastra usługi Hadoop hello
   
   b.  Otwórz hello wiersza polecenia usługi Hadoop.
   
   c.  Wprowadź katalog główny hello Hive za pomocą polecenia `cd %hive_home%\bin` w wierszu polecenia Hadoop.
   
   d.  Uruchom hello Hive zapytania toocreate w bazie danych i tabele i ładowanie danych z tabel tooHive magazynu obiektów blob.
   
   > [!NOTE]
   > Jeśli dane hello jest duży, użytkownicy mogą tworzyć hello tabelę programu Hive z partycjami. Następnie użytkownicy mogą używać `for` pętli w hello wiersza polecenia usługi Hadoop na powitania węzła głównego tooload danych do tabeli Hive hello partycjonowanego partycji.
   > 
   > 
6. Eksplorowanie danych i tworzenie funkcji zgodnie z potrzebami w wierszu polecenia Hadoop. Należy zauważyć, że funkcje hello nie toobe zmaterializowany w tabelach bazy danych hello. Tylko Pamiętaj toocreate niezbędne zapytania hello je.
   
   a.  Zaloguj się za toohello węzła głównego klastra usługi Hadoop hello
   
   b.  Otwórz hello wiersza polecenia usługi Hadoop.
   
   c.  Wprowadź katalog główny hello Hive za pomocą polecenia `cd %hive_home%\bin` w wierszu polecenia Hadoop.
   
   d.  Uruchamianie zapytań Hive hello w wierszu polecenia Hadoop na powitania węzła głównego hello Hadoop klastra tooexplore hello danych i tworzenie funkcji zgodnie z potrzebami.
7. Jeśli wymagane lub pożądane, przykładowe hello toofit danych w usłudze Azure Machine Learning Studio.
8. Zaloguj się toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
9. Odczytywanie danych hello bezpośrednio z hello `Hive Queries` przy użyciu hello [i zaimportuj dane] [ import-data] modułu. Wklej hello niezbędne kwerendę, która umożliwia wyodrębnianie pól, tworzy funkcje i przykłady danych, w razie potrzeby bezpośrednio w hello [i zaimportuj dane] [ import-data] zapytania.
10. Począwszy od dataset przekazany prosty przepływ eksperymentu uczenia maszynowego Azure.

## <a name="decisiontree"></a>Drzewo decyzyjne dotyczące wyboru scenariusza
- - -
Hello poniższym diagramie przedstawiono opisanych powyżej scenariuszy hello i hello zaawansowane procesu analizy i technologii wyborów dokonanych przyjmujących tooeach hello wyszczególnione scenariuszy. Uwaga: przetwarzanie danych, eksploracji engineering funkcji i próbkowanie może być umieścić w jedną lub więcej metody/środowiska — w źródle hello, pośrednie, i/lub środowiska docelowego — i można kontynuować wielokrotnie powtarzane, zgodnie z potrzebami. Hello diagram tylko służy jako ilustrację niektóre możliwe przepływów i nie zapewnia kompleksowe wyliczenia.

![Przykładowe DS procesu wskazówki scenariusze][8]

### <a name="advanced-analytics-in-action-examples"></a>Zaawansowane analizy w akcji przykłady
Aby uzyskać wskazówki dotyczące usługi Azure Machine Learning na trasie, które wykorzystują hello zaawansowane procesu analizy i technologii przy użyciu publicznego zestawów danych, zobacz:

* [Zespół proces analizy danych w działaniu: przy użyciu programu SQL Server](machine-learning-data-science-process-sql-walkthrough.md).
* [Zespół proces analizy danych w działaniu: z użyciem klastrów usługi HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md).

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
