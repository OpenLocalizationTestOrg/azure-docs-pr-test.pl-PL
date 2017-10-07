---
title: "zrzuty stosu aaaEnable usługi Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Włącz zrzuty stosu dla usług Hadoop z klastrów usługi HDInsight opartych na systemie Linux debugowania i analizy."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8f151adb-f687-41e4-aca0-82b551953725
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 49e30f26e1a83f19e068e9da253b5548caec70d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a>Włącz zrzuty stosu dla usługi Hadoop w HDInsight opartych na systemie Linux

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Zrzuty stosu zawierającego migawkę pamięci aplikacji hello, w tym hello wartości zmiennych w czasie hello zrzutu hello został utworzony. Tak, aby były przydatne do diagnozowania problemów występujących w czasie wykonywania.

> [!IMPORTANT]
> Hello kroki opisane w tym dokumencie pracować tylko z klastrami usługi HDInsight, które używają systemu Linux. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a name="whichServices"></a>Usługi

Można włączyć zrzuty stosu dla hello następujące usługi:

* **hcatalog** -tempelton
* **gałąź** -serwera hiveserver2, potrzeby magazynu metadanych, derbyserver
* **mapreduce** -jobhistoryserver
* **yarn** -resourcemanager nodemanager, timelineserver
* **System plików hdfs** -datanode secondarynamenode, namenode

Można także włączyć zrzuty stosu mapę hello i zmniejszyć procesów uruchomionych przez usługi HDInsight.

## <a name="configuration"></a>Opis sterty zrzutu konfiguracji

Zrzuty stosu są włączane przez przeniesienie opcji (czasami znana jako zdecyduje, lub parametry) toohello JVM podczas uruchamiania usługi. Dla większości usług Hadoop można zmodyfikować hello powłoki skryptu używanego toostart hello usługi toopass tych opcji.

Każdy skrypt ma Eksport  **\* \_OPTS**, który zawiera opcje hello przekazany toohello maszyny JVM. Na przykład w hello **hadoop env.sh** skryptu hello wiersza, który rozpoczyna się od `export HADOOP_NAMENODE_OPTS=` zawiera opcje hello hello NameNode usługi.

Mapowanie i zmniejszenie procesy są nieco inne operacje te są Proces podrzędny programu hello usługi MapReduce. Każdy mapy lub Zmniejsz proces jest uruchomiony w kontenerze, a dwa wpisy zawierające hello JVM opcje. Zarówno zawarte w **mapred-site.xml**:

* **mapreduce.Admin.map.child.Java.opts**
* **mapreduce.Admin.Reduce.child.Java.opts**

> [!NOTE]
> Zaleca się przy użyciu Ambari toomodify zarówno hello skryptów i ustawienia mapred-site.xml jako Ambari obsługi replikacji zmian w węzłach w klastrze hello. Zobacz hello [przy użyciu Ambari](#using-ambari) sekcji, aby poznać konkretne kroki.

### <a name="enable-heap-dumps"></a>Włączanie zrzutów stosu

Witaj Poniższa opcja umożliwia zrzuty stosu po wystąpieniu OutOfMemoryError:

    -XX:+HeapDumpOnOutOfMemoryError

Witaj  **+**  wskazuje, że ta opcja jest włączona. Domyślnie Hello jest wyłączona.

> [!WARNING]
> Zrzuty stosu nie są włączone dla usługi Hadoop w usłudze HDInsight domyślnie jako pliki zrzutu hello mogą być duże. Włączenie ich do rozwiązywania problemów, należy pamiętać toodisable hello je po odtworzeniu problemu i hello zebranych plików zrzutu.

### <a name="dump-location"></a>Lokalizacja zrzutu

Domyślna lokalizacja pliku zrzutu hello Hello jest hello bieżący katalog roboczy. Można kontrolować, gdzie hello plik jest przechowywany przy użyciu hello następujących opcji:

    -XX:HeapDumpPath=/path

Na przykład za pomocą `-XX:HeapDumpPath=/tmp` powoduje, że toobe zrzuty hello przechowywane w TMP hello.

### <a name="scripts"></a>Skrypty

Można również uruchomić skrypt po **OutOfMemoryError** występuje. Na przykład wyzwalania powiadomienie, aby wiedzieć, że błąd hello wystąpił. Użyj następujących hello opcję tootrigger skrypt na __OutOfMemoryError__:

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> Ponieważ Hadoop to Rozproszony system, dowolny skrypt używany muszą znajdować się we wszystkich węzłach w klastrze hello hello usługa jest uruchomiona na.
> 
> skrypt Hello musi również być w lokalizacji, która jest dostępna przez program hello konta hello usługa działa jako i podać uprawnienia do wykonywania. Na przykład możesz toostore skryptów w `/usr/local/bin` i użyj `chmod go+rx /usr/local/bin/filename.sh` toogrant uprawnienia Odczyt i wykonywanie.

## <a name="using-ambari"></a>Za pomocą narzędzia Ambari

toomodify hello konfiguracji dla usługi, użyj hello następujące kroki:

1. Otwórz hello Ambari web UI dla klastra. adres URL Hello jest https://YOURCLUSTERNAME.azurehdinsight.net.

    Po wyświetleniu monitu uwierzytelniania przy użyciu nazwy konta hello HTTP witryny toohello (domyślne: admin) i hasło dla klastra.

   > [!NOTE]
   > Może pojawić się prośba po raz drugi przez Ambari hello nazwy użytkownika i hasła. Jeśli tak, wprowadź hello tę samą nazwę konta i hasło

2. Przy użyciu listy hello powitania po lewej stronie, wybierz obszar usługi hello ma toomodify. Na przykład **HDFS**. W obszarze center hello, wybierz hello **Configs** kartę.

    ![Obraz z wybraną kartą Configs systemu plików HDFS w sieci Web Ambari](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. Przy użyciu hello **filtru...**  wpisu, wprowadź **zdecyduje**. Tylko elementy zawierające ten tekst są wyświetlane.

    ![Filtrowana lista](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. Znajdź hello  **\* \_OPTS** wpisu dla usługi hello tooenable zrzuty stosu dla, a następnie dodaj hello opcje chcesz tooenable. W następujących obrazu hello, zostały dodane `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** wpis:

    ![HADOOP_NAMENODE_OPTS z - XX: + HeapDumpOnOutOfMemoryError - XX: HeapDumpPath = / tmp /](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > Podczas włączania zrzuty stosu dla hello mapy lub Zmniejsz procesu podrzędnego, wyszukaj hello pola o nazwie **mapreduce.admin.map.child.java.opts** i **mapreduce.admin.reduce.child.java.opts**.

    Użyj hello **zapisać** przycisk toosave hello zmiany. Można wprowadzić krótkiej uwagi opisujące hello zmiany.

5. Po zastosowaniu zmian hello hello **wymagane jest ponowne uruchomienie** pojawi się ikona obok co najmniej jedna usługa.

    ![ponowne uruchomienie ikonę wymagane i uruchom ponownie przycisku](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. Wybierz każda usługa, która wymaga ponownego uruchomienia i użyj hello **akcji usługi** przycisk zbyt**włączyć w trybie konserwacji**. Tryb konserwacji zapobiega alerty generowane z hello usługi po ponownym jej uruchomieniu.

    ![Włącz menu Tryb konserwacji](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. Po włączeniu trybu konserwacji, użyj hello **Uruchom ponownie** przycisk usługi hello zbyt**Uruchom ponownie wszystkie dokonane**

    ![Uruchom ponownie wszystkie dotyczy wpisu](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > Witaj wpisy dla hello **ponowne uruchomienie** przycisk mogą być różne dla innych usług.

8. Po uruchomieniu usługi hello Użyj hello **akcji usługi** przycisk zbyt**włączyć Wyłącz tryb konserwacji**. To monitorowanie dla alertów dla usługi hello tooresume Ambari.

