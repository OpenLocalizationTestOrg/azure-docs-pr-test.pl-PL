---
title: "informacje o wersji aaaArchived — składniki platformy Hadoop w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Archiwizowane informacje o wersji dla starszych wersji składników platformy Hadoop dla usługi Azure HDInsight."
services: hdinsight
documentationcenter: 
editor: cgronlun
manager: jhubbard
author: nitinme
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 7a99c77f4557ca8c1dabe924cc67b2e0a134f8c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-archive-for-hadoop-components-on-azure-hdinsight"></a>Informacje o wersji (archiwum) dla składników platformy Hadoop w usłudze Azure HDInsight

Ten artykuł zawiera informacje o hello **starsze** Azure HDInsight wersji aktualizacji. Aby uzyskać informacji o nowych wersjach, zobacz [informacje o wersji usługi HDInsight](hdinsight-release-notes.md).

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz [artykułu przechowywanie wersji usługi HDInsight](hdinsight-component-versioning.md).



## <a name="notes-for-08302016-release-of-hdinsight"></a>Informacje o wersji usługi HDInsight 2016-08-30
numery wersji pełnej Hello klastrów usługi HDInsight opartych na systemie Linux wdrożonych w tej wersji:

| HDI | Wersja klastra HDI | HDP | HDP kompilacji | Ambari kompilacji |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8268980 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8268980 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8269383 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

numery wersji pełnej Hello klastrów usługi HDInsight opartych na systemie Windows wdrożone w tej wersji:

| HDI | Wersja klastra HDI | HDP | HDP kompilacji |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1033.2559206 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1033.2559206 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1033.2559206 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1033.2559206 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1033.2559206 |2.3 |2.3.3.1-25 |


## <a name="08172016---release-of-r-server-on-hdinsight"></a>08/17/2016 — wersja R Server w usłudze HDInsight
* Serwer R 8.0.5 - głównie zlecenia poprawka błędu. Zobacz hello [R Server wersji](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes) Aby uzyskać więcej informacji.
* Pakiet uczenie maszynowe Azure w węźle krawędzi hello - [tego pakietu R](https://cran.r-project.org/web/packages/AzureML/vignettes/getting_started.html) toobe modeli umożliwia R publikowania i użycia jako usługi sieci web uczenie Maszynowe Azure.  Zobacz hello ["Operacjonalizacji modelu"](hdinsight-hadoop-r-server-overview.md#operationalize-a-model) sekcji naszych ["Przegląd z R Server w HDInsight"](hdinsight-hadoop-r-server-overview.md) artykułu, aby uzyskać więcej informacji.
* Linux zależności hello [pierwszych 100 najpopularniejszych pakiety języka R](https://github.com/metacran/cranlogs) -te zależności pakietów systemu Linux są teraz instalowane wstępnie.
* Opcja toouse hello sieci CRAN repozytorium Dodawanie R pakiety toohello węzły danych. Aby uzyskać więcej informacji, zobacz ["Rozpoczynanie pracy z platformą R Server w usłudze HDInsight"](hdinsight-hadoop-r-server-get-started.md).
* Ulepszone hello wiarygodność R Server inicjowania obsługi podczas tworzenia klastrów.

## <a name="notes-for-08012016-release-of-hdinsight"></a>Informacje o wersji usługi HDInsight 2016-08-01
numery wersji pełnej Hello klastrów usługi HDInsight opartych na systemie Linux wdrożonych w tej wersji:

| HDI | Wersja klastra HDI | HDP | HDP kompilacji | Ambari kompilacji |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.8028416 |2.2 |2.2.9.1-19 |2.2.1.12-4 |
| 3.3 |3.3.1000.0.8028416 |2.3 |2.3.3.1-25 |2.2.1.12-4 |
| 3.4 |3.4.1000.0.8053402 |2.4 |2.4.2.4-5 |2.2.1.12-4 |

numery wersji pełnej Hello klastrów usługi HDInsight opartych na systemie Windows wdrożone w tej wersji:

| HDI | Wersja klastra HDI | HDP | HDP kompilacji |
| --- | --- | --- | --- |
| 2.1 |2.1.10.1005.2488842 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.1005.2488842 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.1005.2488842 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.1005.2488842 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.1005.2488842 |2.3 |2.3.3.1-25 |

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ klastra (na przykład Spark, Hadoop, HBase lub Storm) | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| Zmiany tooHDInsight 3.4 klastrów |Hello wartości domyślne dla następujących konfiguracji gałęzi są zmieniane w celu poprawy wydajności <ul><li>`hive.vectorized.execution.reduce.enabled=true`</li><li>`hive.tez.min.partition.factor=1f`</li><li>`hive.tez.max.partition.factor=3f`</li><li>`tez.shuffle-vertex-manager.min-src-fraction=0.9`</li><li>`tez.shuffle-vertex-manager.max-src-fraction=0.95`</li><li>`tez.runtime.shuffle.connect.timeout= 30000`</li></ul> |Usługa |Wszystkie |Nie dotyczy |
| Następujące poprawki zostały uwzględnione w tej wersji |GAŁĄŹ 13632, HIVE-12897,HIVE-12907,HIVE-12908,HIVE-12988,HIVE-13510,HIVE-13572,HIVE-13716,HIVE-13726,HIVE-12505,HIVE-13632,HIVE-13661,HIVE-13705,HIVE-13743,HIVE-13810,HIVE-13857,HIVE-13902,HIVE-13911,HIVE-13933 |Usługa |Wszystkie |Nie dotyczy |

## <a name="notes-for-07142016-release-of-hdinsight"></a>Informacje o wersji usługi HDInsight 2016-07-14
numery wersji pełnej Hello klastrów usługi HDInsight opartych na systemie Linux wdrożonych w tej wersji:

| HDI | Wersja klastra HDI | HDP | HDP kompilacji | Ambari kompilacji |
| --- | --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7932505 |2.2 |2.2.9.1-11 |2.2.1.12-2 |
| 3.3 |3.3.1000.0.7932505 |2.3 |2.3.3.1-18 |2.2.1.12-2 |
| 3.4 |3.4.1000.0.7933003 |2.4 |2.4.2.0 |2.2.1.12-2 |

numery wersji pełnej Hello klastrów usługi HDInsight opartych na systemie Windows wdrożone w tej wersji:

| HDI | Wersja klastra HDI | HDP | HDP kompilacji |
| --- | --- | --- | --- |
| 2.1 |2.1.10.989.2441725 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.989.2441725 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.989.2441725 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.989.2441725 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.989.2441725 |2.3 |2.3.3.1-21 |

## <a name="notes-for-07072016-release-of-hdinsight"></a>Informacje o wersji 2016-07-07 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight opartych na systemie Linux wdrożonych w tej wersji:

| HDI | Wersja klastra HDI | HDP | HDP kompilacji |
| --- | --- | --- | --- |
| 3.2 |3.2.1000.0.7864996 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.1000.0.7864996 |2.3 |2.3.3.1-18 |
| 3.4 |3.4.1000.0.7861906 |2.4 |2.4.2.0 |

numery wersji pełnej Hello klastrów usługi HDInsight opartych na systemie Windows wdrożone w tej wersji:

| HDI | Wersja klastra HDI | HDP | HDP kompilacji |
| --- | --- | --- | --- |
| 2.1 |2.1.10.977.2413853 |1.3 |1.3.12.0-01795 |
| 3.0 |3.0.6.977.2413853 |2.0 |2.0.13.0-2117 |
| 3.1 |3.1.4.977.2413853 |2.1 |2.1.16.0-2374 |
| 3.2 |3.2.7.977.2413853 |2.2 |2.2.9.1-11 |
| 3.3 |3.3.0.977.2413853 |2.3 |2.3.3.1-21 |

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ klastra (na przykład Spark, Hadoop, HBase lub Storm) | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| [Narzędzia HDInsight Tools for IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md) |Wtyczkę IntelliJ IDEA klastrów HDInsight Spark jest teraz zintegrowana z zestawu narzędzi Azure for IntelliJ. Go obsługuje v2.9.1 zestawu Azure SDK, najnowsze Java SDK i zawiera wszystkie funkcje hello z autonomicznego hello dodatek HDInsight for IntelliJ. |Narzędzia |platforma Spark |Nie dotyczy |
| [Narzędzia HDInsight Tools dla programu Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md) |Azure zestawu narzędzi dla programu Eclipse obsługuje teraz klastry HDInsight Spark. Umożliwia ona hello następujące funkcje: <ul><li>Utwórz i łatwo tworzenia aplikacji Spark Scala i Java z klasą pierwszego tworzenia obsługę funkcji IntelliSense, automatycznego formatowania, sprawdzanie błędów itp.</li><li>Testowanie aplikacji Spark hello lokalnie.</li><li>Prześlij klastra Spark tooHDInsight zadania i pobrać hello wyniki.</li><li>Zaloguj się za tooAzure i dostęp do wszystkich klastry Spark hello skojarzone z subskrypcjami platformy Azure.</li><li>Przejdź wszystkich hello skojarzonych zasobów magazynu klastra Spark w usłudze HDInsight.</li></ul> |Narzędzia |platforma Spark |Nie dotyczy |

Począwszy od tej wersji, zmieniono zasady stosowania poprawek systemu operacyjnego gościa hello klastrów usługi HDInsight opartej na systemie Linux. Celem Hello hello nowych zasad jest toosignificantly zmniejszyć hello liczby ponownych uruchomień komputera toopatching ukończenia. Witaj nowych zasad poprawki maszyn wirtualnych (VM) w systemie Linux klastrów każdego poniedziałek i czwartek, zaczynając od 00: 00 czasu UTC, w sposób rozłożone w węzłach żadnego danego klastra. Jednak żadnej danej maszyny Wirtualnej uruchamia co najwyżej raz na 30 dni powodu poprawki tooguest systemu operacyjnego. Ponadto hello ponownym nowo utworzony klaster nie odbywa się wcześniej niż 30 dni od daty utworzenia hello klastra.

> [!NOTE]
> Te zmiany mają zastosowanie tylko toonewly utworzyć klastry równą lub większą niż ta wersja.
>
>

## <a name="notes-for-06062016-release-of-hdinsight"></a>Informacje o wersji 2016-06-06 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

| HDP | Wersja usługi HDI | Platforma Spark w wersji | Numer kompilacji Ambari | Numer kompilacji HDP |
| --- | --- | --- | --- | --- |
| 2.3 |3.3.1000.0.7702215 |1.5.2 |2.2.1.8-2 |2.3.3.1-18 |
| 2.4 |3.4.1000.0.7702224 |1.6.1 |2.2.1.8-2 |2.4.2.0 |

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ klastra (na przykład Spark, Hadoop, HBase lub Storm) | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| Platforma Spark w usłudze HDInsight jest ogólnie dostępna |Ta wersja łączy poprawę dostępności, skalowalności i wydajności tooopen źródła Apache Spark w usłudze HDInsight. <ul><li>Branży dostępność na poziomie 99,9%, dzięki czemu odpowiednie dla wymagających obciążeń przedsiębiorstwa.</li><li>Warstwa skalowalności magazynu przy użyciu usługi Azure Data Lake Store.</li><li>Narzędzia wydajności dla każdej fazy Eksploracja danych i rozwoju. Notesów Jupyter z dostosowanych jądra Spark włączyć interakcyjną eksplorację, ułatwia udostępnianie danych szybki i ciągłe raportowania jest integracja z pulpitami nawigacyjnymi analizy Biznesowej, takich jak usługi Power BI i Tableau Qlik, wtyczkę IntelliJ opcji niezawodnej rozwoju artefaktu kodu i debugowanie.</li></ul> |Usługa |platforma Spark |Nie dotyczy |
| Narzędzia HDInsight Tools for IntelliJ |Jest to wtyczka IntelliJ IDEA klastry HDInsight Spark. Umożliwia ona hello następujące funkcje:<ul><li>Utwórz i łatwo tworzenia aplikacji Spark Scala i Java z klasą pierwszego tworzenia obsługę funkcji IntelliSense, automatycznego formatowania, sprawdzanie błędów itp.</li><li>Testowanie aplikacji Spark hello lokalnie.</li><li>Prześlij klastra Spark tooHDInsight zadania i pobrać hello wyniki.</li><li>Zaloguj się za tooAzure i dostęp do wszystkich klastry Spark hello skojarzone z subskrypcjami platformy Azure.</li><li>Przejdź wszystkich hello skojarzonych zasobów magazynu klastra Spark w usłudze HDInsight.</li><li>Przejdź wszystkie hello zadania historii i zadania informacje dla klastra Spark w usłudze HDInsight.</li><li>Debugowanie zadań Spark zdalnie z komputera stacjonarnego.</li></ul> |Narzędzia |platforma Spark |Nie dotyczy |

## <a name="notes-for-05132016-release-of-hdinsight"></a>Informacje o wersji usługi HDInsight 2016-05-13
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.875.2159884 (HDP 1.3.12.0-01795 — bez zmian) (system Windows)
* HDInsight 3.0.6.875.2159884 (HDP 2.0.13.0-2117 — bez zmian) (system Windows)
* HDInsight 3.1.4.922.2266903 (HDP 2.1.15.0-2374 — bez zmian) (system Windows)
* HDInsight 3.2.7.922.2266903 (HDP 2.2.9.1-11) (system Windows)
* HDInsight 3.3.0.922.2266903 (HDP 2.3.3.1-18) (system Windows)
* HDInsight (Linux) 3.2.1000.0.7565644 (HDP 2.2.9.1-11)
* HDInsight (Linux) 3.3.1000.0.7565644 (HDP 2.3.3.1-18)
* HDInsight (Linux) 3.4.1000.0.7548380 (HDP 2.4.2.0)

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ klastra (na przykład Spark, Hadoop, HBase lub Storm) | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| Aktualizacja wersji Spark i inne poprawki błędów |Ta wersja aktualizacje wersji Spark hello w too1.6.1 klastra usługi HDInsight i poprawki inne usterki |Usługa |platforma Spark |Nie dotyczy |

## <a name="notes-for-04112016-release-of-hdinsight"></a>Informacje o wersji usługi HDInsight 2016-04-11
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.889.2191206 (HDP 1.3.12.0-01795 — bez zmian) (system Windows)
* HDInsight 3.0.6.889.2191206 (HDP 2.0.13.0-2117 — bez zmian) (system Windows)
* HDInsight 3.1.4.889.2191206 (HDP 2.1.15.0-2374 — bez zmian) (system Windows)
* HDInsight 3.2.7.889.2191206 (HDP 2.2.9.1-10) (system Windows)
* HDInsight (system Windows) 3.3.0.889.2191206 (HDP 2.3.3.1-16 — bez zmian)
* HDInsight (Linux) 3.2.1000.0.7339916 (HDP 2.2.9.1-10)
* HDInsight (Linux) 3.3.1000.0.7339916 (HDP 2.3.3.1-16)
* HDInsight (Linux) 3.4.1000.0.7338911 (HDP 2.4.1.1-3)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ (na przykład Hadoop, HBase lub Storm) klastra | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| Uaktualnianie niestandardowych potrzeby magazynu metadanych wystawia dla HDI 3.4 |Tworzenie klastra będą się kończyć niepowodzeniem, jeśli używasz niestandardowego potrzeby magazynu metadanych, który był wcześniej używany w starszej wersji innego klastra usługi HDInsight. To powodu tooan uaktualnienia o błędzie skryptu teraz został rozwiązany |Tworzenie klastra |Wszystkie |Nie dotyczy |
| Odzyskiwanie po awarii programu Livy |Zapewnia odporność stan zadania dla dowolnego zadania przesłane za pośrednictwem programu Livy |Niezawodność |Platforma Spark w systemie Linux |Nie dotyczy |
| Zawartość Jupyter wysokiej dostępności |Udostępnia hello możliwości toosave i obciążenia Jupyter notebook zawartość tooand z hello konta magazynu skojarzone z klastrem hello. Aby uzyskać więcej informacji, zobacz [jądra dostępne dla notesów Jupyter](hdinsight-apache-spark-jupyter-notebook-kernels.md). |Komputery przenośne |Platforma Spark w systemie Linux |Nie dotyczy |
| Usunięcie hiveContext w notesach Jupyter |Użyj `%%sql` magic zamiast `%%hive` magic. Element SqlContext jest równoważne toohiveContext. Aby uzyskać więcej informacji, zobacz [jądra dostępne dla notesów Jupyter](hdinsight-apache-spark-jupyter-notebook-kernels.md) |Komputery przenośne |Klastry Spark w systemie Linux |Nie dotyczy |
| Amortyzacja starsze wersje Spark |Starsza wersja Spark 1.3.1 został usunięty z usługi hello na 5-31 |Usługa |Klastry Spark w systemie Windows |Nie dotyczy |

## <a name="notes-for-03292016-release-of-hdinsight"></a>Informacje o wersji usługi HDInsight 2016-03-29
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.875.2159884 (HDP 1.3.12.0-01795 — bez zmian) (system Windows)
* HDInsight 3.0.6.875.2159884 (HDP 2.0.13.0-2117 — bez zmian) (system Windows)
* HDInsight 3.1.4.875.2159884 (HDP 2.1.15.0-2374 — bez zmian) (system Windows)
* HDInsight 3.2.7.875.2159884 (HDP 2.2.9.1-7 — bez zmian) (system Windows)
* HDInsight 3.3.0.875.2159884 (HDP 2.3.3.1-16) (system Windows)
* HDInsight (Linux) 3.2.1000.0.7193255 (HDP 2.2.9.1-8 — bez zmian)
* HDInsight (Linux) 3.3.1000.0.7193255 (HDP 2.3.3.1-7 — bez zmian)
* HDInsight (Linux) 3.4.1000.0.7195842 (HDP 2.4.1.0-327)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ (na przykład Hadoop, HBase lub Storm) klastra | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| Dodano wersji HDInsight 3.4 i zaktualizowane wersje HDP dla wszystkich klastrów usługi HDInsight |W tej wersji możemy dodano v3.4 HDInsight (oparte na HDP 2.4) i zaktualizowano również inne wersje HDP. Dostępne są informacje o wersji HDP 2.4 [tutaj](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.4.0/bk_HDP_RelNotes/content/ch_relnotes_v240.html) i można go znaleźć więcej informacji na temat wersji usługi HDInsight [tutaj](hdinsight-component-versioning.md). |Usługa |Wszystkie klastry z systemem Linux |Nie dotyczy |
| HDInsight Premium |HDInsight jest teraz dostępna w dwóch różnych kategoriach — standardowa i Premium. HDInsight Premium jest obecnie w wersji zapoznawczej i jest dostępny tylko dla platformy Hadoop oraz Spark klastrów w systemie Linux. Aby uzyskać więcej informacji, zobacz [tutaj](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium). |Usługa |Hadoop i Spark w systemie Linux |Nie dotyczy |
| Serwer R firmy Microsoft |HDInsight Premium zapewnia Microsoft R Server, które mogą być dołączone do klastrów platformy Hadoop i Spark w systemie Linux. Aby uzyskać więcej informacji, zobacz [omówienie R Server w usłudze HDInsight](hdinsight-hadoop-r-server-overview.md). |Usługa |Hadoop i Spark w systemie Linux |Nie dotyczy |
| Platforma Spark 1.6.0 |Klastry HDInsight 3.4 zawierają teraz Spark 1.6.0 |Usługa |Klastry Spark w systemie Linux |Nie dotyczy |
| Ulepszenia notesu Jupyter |Notesów Jupyter dostępne z klastrami Spark zapewniają dodatkowe Spark jądra. Obejmuje to też ulepszenia, takie jak użycie %% magic, automatycznie wizualizacji i integracji z programem Python wizualizacji bibliotek (takich jak matplotlib). Aby uzyskać więcej informacji, zobacz [jądra dostępne dla notesów Jupyter](hdinsight-apache-spark-jupyter-notebook-kernels.md). |Usługa |Klastry Spark w systemie Linux |Nie dotyczy |

## <a name="notes-for-03222016-release-of-hdinsight"></a>Informacje o wersji 2016-03-22 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.875.2159884 (HDP 1.3.12.0-01795 — bez zmian) (system Windows)
* HDInsight 3.0.6.875.2159884 (HDP 2.0.13.0-2117 — bez zmian) (system Windows)
* HDInsight 3.1.4.875.2159884 (HDP 2.1.15.0-2374 — bez zmian) (system Windows)
* HDInsight 3.2.7.875.2159884 (HDP 2.2.9.1-7 — bez zmian) (system Windows)
* HDInsight 3.3.0.875.2159884 (HDP 2.3.3.1-16) (system Windows)
* HDInsight (Linux) 3.2.1000.0.7193255 (HDP 2.2.9.1-8 — bez zmian)
* HDInsight (Linux) 3.3.1000.0.7193255 (HDP 2.3.3.1-7 — bez zmian)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ (na przykład Hadoop, HBase lub Storm) klastra | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| Zaktualizowane wersje HDInsight dla wszystkich klastrów usługi HDInsight |W tej wersji zostały zaktualizowane wersje HDInsight dla wszystkich klastrów usługi HDInsight |Usługa |Wszystkie |Nie dotyczy |

## <a name="notes-for-03102016-release-of-hdinsight"></a>Informacje o wersji usługi HDInsight 2016-03-10
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.859.2123216 (HDP 1.3.12.0-01795 — bez zmian) (system Windows)
* HDInsight 3.0.6.859.2123216 (HDP 2.0.13.0-2117 — bez zmian) (system Windows)
* HDInsight 3.1.4.859.2123216 (HDP 2.1.15.0-2374 — bez zmian) (system Windows)
* HDInsight 3.2.7.859.2123216 (HDP 2.2.9.1-7) (system Windows)
* HDInsight 3.3.0.859.2123216 (HDP 2.3.3.1-5 — bez zmian) (system Windows)
* HDInsight (Linux) 3.2.1000.7076817 (HDP 2.2.9.1-8)
* HDInsight (Linux) 3.3.1000.7076817 (HDP 2.3.3.1-7)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ (na przykład Hadoop, HBase lub Storm) klastra | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| Zaktualizowane wersje HDInsight dla wszystkich klastrów usługi HDInsight |W tej wersji zostały zaktualizowane wersje HDInsight dla wszystkich klastrów usługi HDInsight |Usługa |Wszystkie |Nie dotyczy |

## <a name="notes-for-01272016-release-of-hdinsight"></a>Informacje o wersji usługi HDInsight 2016-01-27
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.817.2028315 (HDP 1.3.12.0-01795 — bez zmian) (system Windows)
* HDInsight 3.0.6.817.2028315 (HDP 2.0.13.0-2117 — bez zmian) (system Windows)
* HDInsight 3.1.4.817.2028315 (HDP 2.1.15.0-2374 — bez zmian) (system Windows)
* HDInsight 3.2.7.817.2028315 (HDP 2.2.9.1-1) (system Windows)
* HDInsight 3.3.0.817.2028315 (HDP 2.3.3.1-5 — bez zmian) (system Windows)
* HDInsight (Linux) 3.2.1000.4072335 (HDP 2.2.9.1-1)
* HDInsight (Linux) 3.3.1000.4072335 (HDP 2.3.3.1-1)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ (na przykład Hadoop, HBase lub Storm) klastra | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| Zaktualizowane wersje HDInsight dla wszystkich klastrów usługi HDInsight |W tej wersji zostały zaktualizowane wersje HDInsight dla wszystkich klastrów usługi HDInsight |Usługa |Wszystkie |Nie dotyczy |

## <a name="notes-for-12022015-release-of-hdinsight"></a>Informacje o wersji 2015-12-02 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.763.1931434 (HDP 1.3.12.0-01795 — bez zmian) (system Windows)
* HDInsight 3.0.6.763.1931434 (HDP 2.0.13.0-2117 — bez zmian) (system Windows)
* HDInsight 3.1.4.763.1931434 (HDP 2.1.15.0-2374 — bez zmian) (system Windows)
* HDInsight 3.2.7.763.1931434 (HDP 2.2.7.1-34 — bez zmian) (system Windows)
* HDInsight 3.3.1000.0 (HDP 2.3.3.1-5) (system Windows)
* HDInsight (Linux) 3.2.1000.0.6392801 (HDP 2.2.7.1-34 — bez zmian)
* HDInsight (Linux) 3.3.1000.0 (HDP 2.3.3.0-3039)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ (na przykład Hadoop, HBase lub Storm) klastra | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| Dodano wersji HDInsight 3.3 i zaktualizowane wersje HDP dla wszystkich klastrów usługi HDInsight |W tej wersji możemy dodano v3.3 HDInsight (oparte na HDP 2.3) i zaktualizowano również inne wersje HDP. Dostępne są informacje o wersji HDP 2.3 [tutaj](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.3.0/bk_HDP_RelNotes/content/ch_relnotes_v230.html) i można go znaleźć więcej informacji na temat wersji usługi HDInsight [tutaj](hdinsight-component-versioning.md). |Usługa |Wszystkie |Nie dotyczy |

## <a name="notes-for-11302015-release-of-hdinsight"></a>Informacje o wersji 2015-11-30 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.757.1923908 (HDP 1.3.12.0-01795 — bez zmian) (system Windows)
* HDInsight 3.0.6.757.1923908 (HDP 2.0.13.0-2117 — bez zmian) (system Windows)
* HDInsight 3.1.4.757.1923908 (HDP 2.1.15.0-2374 — bez zmian) (system Windows)
* HDInsight 3.2.7.757.1923908 (HDP 2.2.7.1-34) (system Windows)
* HDInsight (Linux) 3.2.1000.0.6392801 (HDP 2.2.7.1-34)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ (na przykład Hadoop, HBase lub Storm) klastra | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| Zaktualizowane wersje HDInsight dla wszystkich klastrów usługi HDInsight i wersji HDP klastrów usługi HDInsight w wersji 3.2 (z systemem Windows i Linux) |W tej wersji zostały zaktualizowane wersje HDInsight i HDP |Usługa |Wszystkie |Nie dotyczy |

## <a name="notes-for-10272015-release-of-hdinsight"></a>Informacje o wersji 2015-10-27 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.726.1866228 (HDP 1.3.12.0-01795 — bez zmian) (system Windows)
* HDInsight 3.0.6.726.1866228 (HDP 2.0.13.0-2117 — bez zmian) (system Windows)
* HDInsight 3.1.4.726.1866228 (HDP 2.1.15.0-2374 — bez zmian) (system Windows)
* HDInsight 3.2.7.726.1866228 (HDP 2.2.7.1-33) (system Windows)
* HDInsight (Linux) 3.2.1000.0.6035701 (HDP 2.2.7.1-33)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ (na przykład Hadoop, HBase lub Storm) klastra | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| Zaktualizowane wersje HDInsight dla wszystkich klastrów usługi HDInsight (z systemem Windows i Linux) |W tej wersji zostały zaktualizowane wersje HDInsight i HDP |Usługa |Wszystkie |Nie dotyczy |
| Stałe klastrów Jupyter Spark dla systemu Windows z klastrami wielkie litery |Klastry, które miały nazwy DNS podane wielkimi literami ma problemy z notesów Jupyter powodu tooan pochodzenia żądania wyboru. poprawka Hello jest nazwa DNS hello toochange przypadku toolower Jupyter w konfiguracji. |Usługa |HDInsight Spark (system Windows) |Nie dotyczy |

## <a name="notes-for-10202015-release-of-hdinsight"></a>Informacje o wersji 2015-10-20 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.716.1846990 (HDP 1.3.12.0-01795 — bez zmian) (system Windows)
* HDInsight 3.0.6.716.1846990 (HDP 2.0.13.0-2117 — bez zmian) (system Windows)
* HDInsight 3.1.4.716.1846990 (HDP 2.1.16.0-2374) (system Windows)
* HDInsight 3.2.7.716.1846990 (HDP 2.2.7.1-0004) (system Windows)
* HDInsight 3.2.1000.0.5930166 (Linux) (HDP 2.2.7.1-0004)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ (na przykład Hadoop, HBase lub Storm) klastra | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| Domyślna HDP tooHDP zmienione w wersji 2.2 |Witaj wersja domyślna dla klastrów usługi HDInsight w systemie Windows jest zmienione tooHDP 2.2. Od lutego 2015 została ogólnie dostępna w HDInsight w wersji 3.2 (HDP 2.2). Ta zmiana tylko Przerzuca hello domyślnej wersji klastra, gdy jawne wyboru nie zostanie wykonana podczas inicjowania obsługi klastra hello przy użyciu hello portalu Azure, poleceń cmdlet programu PowerShell lub hello zestawu SDK. |Usługa |Wszystkie |Nie dotyczy |
| Zmiany w formacie nazwy maszyny Wirtualnej do wdrażania wielu HDInsight w systemie Linux klastrów w jednej sieci wirtualnej |Obsługa wdrażania wielu klastrów HDInsight Linux w jednej sieci wirtualnej jest dodawany w tej wersji. W ramach aktualizacji, hello format nazwy maszyny wirtualnej w klastrze hello zmienił się z headnode\*, workernode\* i zookeepernode\* toohn\*, dół\*i zk\* odpowiednio. Nie jest zalecana praktyka tootake zależności bezpośrednich hello format nazwy maszyny wirtualnej, ponieważ jest to toochange podmiotu. Przy użyciu "hostname -f" na komputerze lokalnym hello lub Ambari API toodetermine hello listy hostów i mapowanie hello toohosts składników. Można znaleźć więcej informacji na [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/hosts.md) i [https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/host-components.md). |Usługa |Klastry usługi HDInsight w systemie Linux |Nie dotyczy |
| Zmiany konfiguracji |W przypadku klastrów usługi HDInsight w wersji 3.1 dostępne są teraz hello następujące konfiguracje: <ul><li>tez.yarn.ATS.Enabled i yarn.log.server.url. Dzięki temu serwer oś czasu aplikacji hello i hello dziennika serwera toobe stanie tooserve limit dzienników.</li></ul>W przypadku klastrów usługi HDInsight w wersji 3.2 zostały zmodyfikowane hello następujące konfiguracje: <ul><li>ustawiono mapreduce.fileoutputcommitter.Algorithm.Version too2. Umożliwia to korzystanie z wersji V2 hello hello FileOutputCommitter.</li></ul> |Usługa |Wszystkie |Nie dotyczy |

## <a name="notes-for-09092015-release-of-hdinsight"></a>Informacje o wersji 2015-09-09 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.675.1768697 (HDP 1.3.12.0-01795 — bez zmian)
* HDInsight 3.0.6.675.1768697 (HDP 2.0.13.0-2117 — bez zmian)
* HDInsight 3.1.4.675.1768697 (HDP 2.1.15.0-2334 — bez zmian)
* HDInsight 3.2.6.675.1768697 (HDP 2.2.6.1-0012 — bez zmian)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ (na przykład Hadoop, HBase lub Storm) klastra | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| Zaktualizowane wersje HDInsight dla wszystkich klastrów usługi HDInsight |W tej wersji zostały zaktualizowane wersje usługi HDInsight |Usługa |Wszystkie |Nie dotyczy |

## <a name="notes-for-07312015-release-of-hdinsight"></a>Informacje o wersji 2015-07-31 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.640.1695824 (HDP 1.3.12.0-01795 — bez zmian)
* HDInsight 3.0.6.640.1695824 (HDP 2.0.13.0-2117 — bez zmian)
* HDInsight 3.1.4.640.1695824 (HDP 2.1.15.0-2334 — bez zmian)
* HDInsight 3.2.6.640.1695824 (HDP 2.2.6.1-0012 — bez zmian)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ (na przykład Hadoop, HBase lub Storm) klastra | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| Usuń Spark węzła klastra ponownej instalacji systemu przepływu pracy |Stałe usterkę, która była przyczyną Spark toonot odzyskiwanie po odtworzenia z obrazu węzłów klastra |Usługa |platforma Spark |Nie dotyczy |

## <a name="notes-for-07312015-release-of-hdinsight"></a>Informacje o wersji 2015-07-31 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.635.1684502 (HDP 1.3.12.0-01795 — bez zmian)
* HDInsight 3.0.6.635.1684502 (HDP 2.0.13.0-2117 — bez zmian)
* HDInsight 3.1.4.635.1684502 (HDP 2.1.15.0-2334 — bez zmian)
* HDInsight 3.2.6.635.1684502 (HDP 2.2.6.1-0012 — bez zmian)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ (na przykład Hadoop, HBase lub Storm) klastra | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| Zaktualizowane wersje HDInsight dla wszystkich klastrów usługi HDInsight |W tej wersji zostały zaktualizowane wersje usługi HDInsight |Usługa |Wszystkie |Nie dotyczy |

## <a name="notes-for-07072015-release-of-hdinsight"></a>Informacje o wersji 2015-07-07 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.610.1630216 (HDP 1.3.12.0-01795 — bez zmian)
* HDInsight 3.0.6.610.1630216 (HDP 2.0.13.0-2117 — bez zmian)
* HDInsight 3.1.4.610.1630216 (HDP 2.1.15.0-2334 — bez zmian)
* HDInsight 3.2.4.610.1630216 (HDP 2.2.6.1-0012)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

| Tytuł | Opis | Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK) | Typ (na przykład Hadoop, HBase lub Storm) klastra | JIRA (jeśli dotyczy) |
| --- | --- | --- | --- | --- |
| Zaktualizowane wersje HDP klastrów usługi HDInsight w wersji 3.2 |W tej wersji HDInsight 3.2 wdraża HDP 2.2.6.1-0012 |Usługa |Wszystkie |Nie dotyczy |

## <a name="notes-for-06262015-release-of-hdinsight"></a>Informacje o wersji 2015-06-26 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.601.1610731 (HDP 1.3.12.0-01795 — bez zmian)
* HDInsight 3.0.6.601.1610731 (HDP 2.0.13.0-2117 — bez zmian)
* HDInsight 3.1.4.601.1610731 (HDP 2.1.15.0-2334 — bez zmian)
* HDInsight 3.2.4.601.1610731 (HDP 2.2.6.1-0011)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

<table border="1">
<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK)</p></th>
<th>Typ (na przykład Hadoop, HBase lub Storm) klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td>Zaktualizowane wersje HDP klastrów usługi HDInsight w wersji 3.2</td>
<td>W tej wersji HDInsight 3.2 wdraża HDP punktach 2.2.6.1</td>
<td>Usługa</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-06182015-release-of-hdinsight"></a>Informacje o wersji 2015-06-18 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.596.1601657 (HDP 1.3.12.0-01795 — bez zmian)
* HDInsight 3.0.6.596.1601657 (HDP 2.0.13.0-2117 — bez zmian)
* HDInsight 3.1.4.596.1601657 (HDP 2.1.15.0-2334)
* HDInsight 3.2.4.596.1601657 (HDP 2.2.6.1-0002)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

<table border="1">
<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK)</p></th>
<th>Typ (na przykład Hadoop, HBase lub Storm) klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td>Dodatkowe otwierane porty HTTPS</td>
<td>usługi w chmurze Hello teraz otwiera 5 too8005 8001 portów w klastrze hello np. w https://<clustername>.azurehdinsight.net:8001/. Żądania toothese adresy URL są uwierzytelniani za pomocą hello sam mechanizm hasło uwierzytelniania podstawowego jako port 443. Te porty powiązać toohello sam port na powitania active headnode. Akcje skryptu może być używana toomake klienta usług nasłuchiwania na tych portów na powitania headnode i tras toooutside hello klastra.</td>
<td>Usługi w chmurze</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Tymczasowy problem losowa MapReduce dla usługi HDInsight w wersji 3.2</td>
<td>Poprawka dla rzadkich, sporadyczne wyścigu w losowo zmniejszyć mapy w dużych klastrach powodujące błędy okazjonalne zadania. Zobacz <a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE 6361</a> Aby uzyskać więcej informacji.</td>
<td>Podstawowe usługi Hadoop</td>
<td>Wszystkie</td>
<td><a href="https://issues.apache.org/jira/browse/MAPREDUCE-6361" target="_blank">MAPREDUCE 6361</a></td>
</tr>
<tr>
<td>Przenoszenie tooLatest 2.2 zestawu SDK Java usługi Azure HDInsight w wersji 3.2</td>
<td>Przenieść toolatest wersji zestawu Azure SDK dla języka Java, używany przez sterownik WASB hello hello. Witaj najnowszej wersji zestawu SDK ma kilka poprawek i hello hello same są dostępne pod adresem https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt.</td>
<td>Podstawowe usługi Hadoop</td>
<td>Wszystkie</td>
<td><a href="https://issues.apache.org/jira/browse/HADOOP-11959" target="_blank">HADOOP 11959</a></td>
</tr>
<tr>
<td>Przenieś tooHDP 2.1.15 klastrów usługi HDInsight w wersji 3.1</td>
<td>Hortonworks informacje o wersji dla wersji hello są dostępne <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.15-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.15.html" target="_blank">tutaj</a>.</td>
<td>HDP</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-06042015-release-of-hdinsight"></a>Informacje o wersji 2015-06-04 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.583.1575584 (HDP 1.3.12.0-01795 — bez zmian)
* HDInsight 3.0.6.583.1575584 (HDP 2.0.13.0-2117 — bez zmian)
* HDInsight 3.1.3.583.1575584 (HDP 2.1.12.1-0003 — bez zmian)
* HDInsight 3.2.4.583.1575584 (HDP 2.2.6.1-1)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

<table border="1">
<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK)</p></th>
<th>Typ (na przykład Hadoop, HBase lub Storm) klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td>Usuń 502 błędu zły bramy w przypadku klastrów Storm</td>
<td>Ta wersja rozwiązuje usterki wpływających na powitania zadania przesyłania API powodujący hello toobe witryny sieci Web w dół po ponownym rozruchu.</td>
<td>Usługa</td>
<td>Storm</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-06012015-release-of-hdinsight"></a>Informacje o wersji 2015-06-01 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.577.1563827 (HDP 1.3.12.0-01795 — bez zmian)
* HDInsight 3.0.6.577.1563827 (HDP 2.0.13.0-2117 — bez zmian)
* HDInsight 3.1.3.577.1563827 (HDP 2.1.12.1-0003 — bez zmian))
* HDInsight 3.2.4.577.1563827 (HDP 2.2.6.0-2800 — bez zmian)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

<table border="1">
<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK)</p></th>
<th>Typ (na przykład Hadoop, HBase lub Storm) klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td>Różne poprawki błędów</td>
<td>Poprawek usterek powiązanych toocluster inicjowania obsługi administracyjnej.</td>
<td>Usługa</td>
<td>Wszystkie typy klastrów</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-05272015-release-of-hdinsight"></a>Informacje o wersji 2015-05-27 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 3.2.4.570.1554102 (HDP 2.2.6.0-2800)
* Inne wersje klastra i zestawu SDK nie są wdrażane w ramach tej wersji.

Ta wersja zawiera hello następujące aktualizacje:

<table border="1">
<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK)</p></th>
<th>Typ (na przykład Hadoop, HBase lub Storm) klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td>HDP 2.2 aktualizacji</td>
<td>Ta wersja HDInsight 3.2 zawiera HDP 2.2.6 i oferuje kilka ważnych poprawek tooHDInsight. Witaj pełne informacje o wersji są dostępne pod adresem <a href="http://dev.hortonworks.com.s3.amazonaws.com/HDPDocuments/HDP2/HDP-2.2.6/HDP_RelNotes_v226/index.html">HDP 2.2.6 informacje o wersji</a>.</td>
<td>HDP</td>
<td>Wszystkie typy klastrów</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>TooDefault zmiany konfiguracji pamięci Yarn kontenera</td>
<td>W ramach tej aktualizacji hello domyślna ilość dostępnej pamięci tooYARN kontenery (yarn.nodemanager.resource.memory mb i yarn.scheduler.maximum alokacji mb), uruchamiana przez Menedżera węzła, zwiększona too5632MB. Wcześniej to zmniejszenie too4608MB, ale w oparciu o różne uruchomionych zadań, hello nową wartość musi oferować lepszą niezawodność i wydajność toomost zadania, dlatego jest lepsze domyślną. W zwykły sposób Jeśli w tej konfiguracji pamięci krytyczne zależności, ustaw go jawnie podczas tworzenia klastra hello.</td>
<td>HDP</td>
<td>Wszystkie typy klastrów</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Domyślna konfiguracja parzystości dla klastrów HBase i Storm</td>
<td>Ta aktualizacja przywraca Hbase i klastrów Storm toouse hello tej samej wartości YARN configs jako klastrów platformy Hadoop. Jest to realizowane parzystości wszystkich typów klastra.</td>
<td>HDP</td>
<td>Baza danych HBase, Storm</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-05202015-release-of-hdinsight"></a>Informacje o wersji 2015-05-20 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.564.1542093 (HDP 1.3.12.0-01795 — bez zmian)
* HDInsight 3.0.6.564.1542093 (HDP 2.0.13.0-2117 — bez zmian)
* HDInsight 3.1.3.564.1542093 (HDP 2.1.12.1-0003)
* HDInsight 3.2.4.564.1542093 (HDP 2.2.4.6-2)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

<table border="1">
<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK)</p></th>
<th>Typ (na przykład Hadoop, HBase lub Storm) klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td>Obsługa EventHub SCP.NET</td>
<td>Hello zaktualizowane pakiety klastra HDInsight Storm Przełącz nowy tooSCP.NET funkcji. Masz teraz dostęp toonew interfejsów API w topologii konstruktora, który ułatwia toouse EventHubSpout lub Java Spouts. Należy zaktualizować Twojego toowork zestawu SDK klienta SCP.NET z nowych klastrów jako kontrakty hello zostały zaktualizowane. Szczegółowe informacje na temat hello nowej notatki interfejsów API użycia i wersji (w tym poprawki błędów) można znaleźć toohello Readme objęte hello pakietu SCP.NET NuGet.</td>
<td>Narzędzi programu VS</td>
<td>Klastry HDInsight 3.2 STORM</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Aktualizacja sterownik JDBC</td>
<td>Zaktualizowano hello toohello sterownik programu SQL Server jest obsługiwana wersja sqljdbc_4.1.5605.100.</td>
<td>Potrzeby magazynu metadanych</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-04272015-release-of-hdinsight"></a>Informacje o wersji 2015-04-27 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.537.1486660 (HDP 1.3.12.0-01795 — bez zmian)
* HDInsight 3.0.6.537.1486660 (HDP 2.0.13.0-2117 — bez zmian)
* HDInsight 3.1.3.537.1486660 (HDP 2.1.12.0-2329 — bez zmian)
* HDInsight 3.2.3.537.1486660 (HDP 2.2.2.2-4)
* ZESTAW SDK 1.5.8

Ta wersja zawiera hello następujące aktualizacje:

<table border="1">
<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK)</p></th>
<th>Typ (na przykład Hadoop, HBase lub Storm) klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td>Usuń zależności biblioteki DLL</td>
<td>Usuwa zależność HDInsight Frameworka testów jednostkowych.</td>
<td>SDK</td>
<td>Usługa Hadoop</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Poprawka błędu dla sytuacji wyścigu</td>
<td>Klaster Utwórz żądanie teraz czeka na PUT żądania toobe zaakceptowana przed sondowania stanu hello</td>
<td>SDK</td>
<td>Usługa Hadoop</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-04142015-release-of-hdinsight"></a>Informacje o wersji 2015-04-14 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.521.1453250 (HDP 1.3.12.0-01795 — bez zmian)
* HDInsight 3.0.6.521.1453250 (HDP 2.0.13.0-2117 — bez zmian)
* HDInsight 3.1.3.521.1453250 (HDP 2.1.12.0-2329 — bez zmian)
* HDInsight 3.2.3.525.1459730 (HDP 2.2.2.2-2)
* ZESTAW SDK 1.5.6

Ta wersja zawiera hello następujące aktualizacje:

<table border="1">
<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK)</p></th>
<th>Typ (na przykład Hadoop, HBase lub Storm) klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td>Poprawki błędów aplikacji tez</td>
<td>Poprawki dla Apache TEZ 2214 i TEZ 1923 znajdują się w tej wersji HDI 3.2. Nie są potrzebne w niektórych zapytań Hive w aplikacji Tez, które wymagają tooshuffle znaczną ilość danych.
</td>
<td>HDP</td>
<td>Usługa Hadoop</td>
<td><a href="https://issues.apache.org/jira/browse/TEZ-2214">2214 APLIKACJI TEZ</a></br><a href="https://issues.apache.org/jira/browse/TEZ-1923">TEZ 1923</a></td>
</tr>
</table>

## <a name="notes-for-04062015-release-of-hdinsight"></a>Informacje o wersji 2015-04-06 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.521.1453250 (HDP 1.3.12.0-01795 — bez zmian)
* HDInsight 3.0.6.521.1453250 (HDP 2.0.13.0-2117 — bez zmian)
* HDInsight 3.1.3.521.1453250 (HDP 2.1.12.0-2329 — bez zmian)
* HDInsight 3.2.3.521.1453250 (HDP 2.2.2.2-1)
* ZESTAW SDK 1.5.6

Ta wersja zawiera hello następujące aktualizacje:

<table border="1">
<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK)</p></th>
<th>Typ (na przykład Hadoop, HBase lub Storm) klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td>Zestaw SDK .NET usługi HDInsight 1.5.6</td>
<td>Aktualizuje tooremove niektóre klasy wewnętrzne dla usługi HDInsight w systemie Linux.</td>
<td>SDK</td>
<td>Usługa Hadoop</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Biblioteka Avro 1.5.6</td>
<td>Dodaje <b>KnownTypeAttribute</b> dla metody <b>GetAllKnownTypes</b>. Stałe NullReferenceException typu ma wartość null dla metody GetAllKnownTypes.</td>
<td>SDK</td>
<td>Usługa Hadoop</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Poprawki błędów</td>
<td>Różne usługi toohello poprawki błędów</td>
<td>Usługa</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-04012015-release-of-hdinsight"></a>Informacje o wersji 2015-04-01 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.513.1431705 (HDP 1.3.12.0-01795)
* HDInsight 3.0.6.513.1431705 (HDP 2.0.13.0-2117)
* HDInsight 3.1.3.513.1431705 (HDP 2.1.12.0-2329)
* HDInsight 3.2.3.513.1431705 (HDP 2.2.2.1-2600)
* ZESTAW SDK 1.5.5

Ta wersja zawiera hello następujące aktualizacje:

<table border="1">
<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK)</p></th>
<th>Typ (na przykład Hadoop, HBase lub Storm) klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td>Zdolność tooenable/wyłączanie zdalnego pulpitu poświadczeń w klastrach z systemem Windows przy użyciu zestawu .NET SDK</td>
<td>Obsługa programowego włączenia lub wyłączenia protokołu RDP poświadczeń w klastrach z systemem Windows.</td>
<td>SDK</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Możliwość tooenable zdalnego pulpitu poświadczeń w klastrach podczas ich obsługi administracyjnej</td>
<td>Wsparcia programowego umożliwiających poświadczenia pulpitu zdalnego tworzenia hello klastra. Spowoduje to usunięcie hello dwuetapowy proces pierwszy klaster hello inicjowania obsługi administracyjnej, a następnie włączenie pulpitu zdalnego.</td>
<td>SDK</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Too2.7.8 uaktualnionego Python</td>
<td>Uaktualniony Python w klastrach HDInsight tooPython 2.7.8, który zawiera pewne ważne zabezpieczenia poprawki dla usługi HDInsight w wersji 2.1, 3.0, 3.1 i 3.2</td>
<td>Usługa</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Zmiana konfiguracji YARN</td>
<td>Zmienione YARN konfiguracji yarn.resourcemanager.max — ukończone — aplikacje too1000 dla wszystkich typów klastra usługi HDInsight w wersji 3.1 i 3.2. Ta wartość określa tylko hello listę ukończonych aplikacji w interfejsie użytkownika YARN hello. tooget informacji o aplikacji, które zostały przesłane wcześniejsze toohello listę aplikacji, pokazane na powitania interfejsu użytkownika, możesz bezpośrednio przejść toohello historii serwera.</td>
<td>YARN</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Zmienianie rozmiaru w węzłach klastra HBase</td>
<td>Klastrów HBase teraz zezwolić na zmianę rozmiaru węzłów (górę i w dół) dla usługi HDInsight w wersji 3.1 i 3.2</td>
<td>Usługa</td>
<td>HBase</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Uaktualnienie JDBC</td>
<td>Sterownik SQL JDBC jest uaktualniony tooversion sqljdbc_4.0.2206.100 dla usługi HDInsight w wersji 3.2. Ta wersja zawiera ulepszenia zabezpieczeń ważne.</td>
<td>HDP</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Aktualizacja konfiguracji maszyny wirtualnej Java</td>
<td>Zaktualizowane JVM konfiguracji networkaddress.cache.ttl too300 sekund z wartości domyślnej hello-1 dla usługi HDInsight w wersji 3.1 i 3.2. Ta wartość konfiguracji określa hello zasad dla wyszukiwania nazw powiodło się z usługi nazw hello buforowania. To rozwiązuje usterki powiązane toogrowing oraz zmniejszanie klastrów HBase.</td>
<td>Usługa</td>
<td>HBase</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Uaktualnij tooAzure Storage SDK for Java 2.0</td>
<td>HDInsight w wersji 3.2 jest uaktualniony toouse hello najnowsza wersja hello Azure Storage SDK for Java. Zawiera kilka ważnych poprawek na powitania 0.6.0 bieżącej wersji.</td>
<td>HDP</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Kod źródłowy WASB tooApache uaktualniony</td>
<td>HDInsight w wersji 3.2 teraz używa hello najnowsze kodu hello WASB system plików sterownika ze struktury Apache Hadoop. Dzięki tej zmianie sterownika WASB hello teraz jest dostarczana w oddzielnych jar. To jest wyłącznie zmiany opakowania i nie zawiera żadnych zmian toobehavior hello WASB sterownika. Nazwa tego pliku JAR Hello jest hadoop-azure-2.6.0.jar.</td>
<td>HDP</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Nazwa pliku aktualizacji w usłudze HDInsight w wersji 3.2 JAR</td>
<td>Ta aktualizacja tooHDInsight w wersji 3.2 zawiera kilka poprawek i kilka słoików wewnętrzny opakowane w ramach HDP zostały uaktualnione. Te JAR filesare wewnętrzny toohello HDP pakietu, a nie do bezpośredniego używania przez aplikacje klienta. Aplikacje powinny pakietu własną wersję słoików hello tak, aby toohello uaktualnienia, który JARs HDP wewnętrznej nie dzielone aplikacji klienta.</td>
<td>HDP</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-03032015-release-of-hdinsight"></a>Informacje o wersji 2015-03-03 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.488.1375841 (HDP 1.3.9.0-01351 — bez zmian)
* HDInsight 3.0.6.488.1375841 (HDP 2.0.9.0-2097 — bez zmian)
* HDInsight 3.1.3.488.1375841 (HDP 2.1.10.0-2290 — bez zmian)
* HDInsight 3.2.3.488.1375841 (HDP-2.2.10.0-2340 — bez zmian)
* Zestaw SDK 1.5.0 (bez zmian)

Ta wersja zawiera hello następujących aktualizacji:

<table border="1">
<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK)</p></th>
<th>Typ (na przykład Hadoop, HBase lub Storm) klastra</th>
<th>JIRA</th>
</tr>
<tr>
<td>Ulepszenia niezawodności</td>
<td>Wprowadziliśmy poprawki, które umożliwia lepsze z hello zwiększone obciążenie z tworzenia toocluster względem hello tooscale usługi.</td>
<td>Usługa</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-02182015-release-of-hdinsight"></a>Informacje o wersji 2015-02-18 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.471.1342507 (HDP 1.3.9.0-01351 — bez zmian)
* HDInsight 3.0.6.471.1342507 (HDP 2.0.9.0-2097 — bez zmian)
* HDInsight 3.1.3.471.1342507 (HDP 2.1.10.0-2290 — bez zmian)
* HDInsight 3.2.3.471.1342507 (HDP-2.2.10.0 2340)
* ZESTAW SDK 1.5.0

Ta wersja zawiera hello następujące aktualizacje:

<table border="1">
<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK)</p></th>
<th>Typ (na przykład Hadoop, HBase lub Storm) klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td>Klastry HDInsight w wersji 3.2</td>
<td>Hadoop 2.6/HDP2.2 jest dostępna z klastrami HDInsight 3.2. Zawiera on tooall wprowadzono znaczące aktualizacje składników hello open source. Aby uzyskać więcej informacji, zobacz Co nowego w usłudze HDInsight i <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.2.0/HDP_2.2.0_Release_Notes_20141202_version/index.html" target="_blank">informacje o wersji HDP 2.2.0.0</a>.</td>
<td>Oprogramowanie typu open source</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>HDInsight w systemie Linux (wersja zapoznawcza)</td>
<td>Można wdrożyć klastry systemem Ubuntu Linux. Aby uzyskać więcej informacji Zobacz Rozpoczynanie pracy z usługą HDInsight w systemie Linux.</td>
<td>Usługa</td>
<td>Usługa Hadoop</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Dostępność STORM ogólne</td>
<td>Klastry platformy Apache Storm jest ogólnie dostępna. Aby uzyskać więcej informacji zobacz rozpocząć korzystanie z systemu Storm w usłudze HDInsight.</td>
<td>Usługa</td>
<td>Storm</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Rozmiary maszyn wirtualnych</td>
<td>Usługa Azure HDInsight jest dostępna na więcej typów maszyny wirtualnej i rozmiary. HDInsight mogą wykorzystywać rozmiary tooA7 A2 przeznaczone do celów ogólnych; Węzły D-Series, które funkcji dysków półprzewodnikowych (SSD) oraz procesory szybsze 60 procent; rozmiary A8 i A9, które mają InfiniBand obsługę szybkiej transmisji w sieci oraz.</td>
<td>Usługa</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Skalowanie klastra</td>
<td>Możesz zmienić hello liczba węzłów danych uruchomionych klastra usługi HDInsight bez konieczności toodelete lub utwórz go ponownie. Obecnie tylko typy klastrów platformy Hadoop zapytań i Apache Storm mają tę możliwość, ale obsługuje typ klastra Apache HBase jest wkrótce toofollow. Aby uzyskać więcej informacji zobacz Zarządzanie w usłudze hdinsight.</td>
<td>Usługa</td>
<td>Hadoop, Storm</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Narzędzia usługi Visual Studio</td>
<td>Ponadto toocomplete narzędzia Apache STORM hello narzędzi dla Apache Hive w programie Visual Studio została zaktualizowany tooinclude uzupełniania, lokalna Weryfikacja i lepszą obsługę debugowania. Aby uzyskać więcej informacji zobacz wprowadzenie do narzędzi Hadoop w HDInsight dla programu Visual Studio.</td>
<td>Narzędzia</td>
<td>Usługa Hadoop</td>
<td>Nie dotyczy</td>
</tr>
<td>Łącznik usługi Hadoop dla usługi Azure rozwiązania Cosmos bazy danych</td>
<td>Łącznik usługi Hadoop dla bazy danych Azure rozwiązania Cosmos może wykonywać złożonych agregacji, analizy i manipulacje za pośrednictwem przechowywane bazy danych Azure rozwiązania Cosmos kolekcji lub konta bazy danych dokumentów JSON bez schematu. Aby uzyskać więcej informacji i zapoznać się z samouczkiem Zobacz uruchamianie zadań usługi Hadoop przy użyciu bazy danych rozwiązania Cosmos Azure i usługi HDInsight.</td>
<td>Usługa</td>
<td>Usługa Hadoop</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Poprawki błędów</td>
<td>Wprowadzono różnych niewielkie poprawki błędów dla usługi HDInsight. Nie oczekiwano żadnych zmian zachowania skierowane do klienta.</td>
<td>Usługa</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-02062015-release-of-hdinsight"></a>Informacje o wersji 2015-02-06 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.463.1325367 (HDP 1.3.9.0-01351 — bez zmian)
* HDInsight 3.0.6.463.1325367 (HDP 2.0.9.0-2097 — bez zmian)
* HDInsight 3.1.2.463.1325367 (HDP 2.1.10.0-2290)
* BRAK ZESTAWU SDK

Ta wersja zawiera hello następujące aktualizacje:

<table border="1">
<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK)</p></th>
<th>Typ (na przykład Hadoop, HBase lub Storm) klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td>Poprawki błędów</td>
<td>Wprowadzono różnych niewielkie poprawki błędów dla usługi HDInsight. Nie oczekiwano żadnych zmian zachowania skierowane do klienta.</td>
<td>Usługa</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>HDP 2.1 obsługi aktualizacji</td>
<td>HDInsight 3.1 jest zaktualizowane toodeploy HDP 2.1.10.0. Aby uzyskać więcej informacji, zobacz <a href ="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.10/bk_releasenotes_hdp_2.1/content/ch_relnotes-HDP-2.1.10.html" target="_blank">wersji HDP-2.1.10</a>. </td>
<td>Oprogramowanie typu open source</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>HDP binarne aktualizacji</td>
<td>Istnieje kilka plików JAR w bazie danych HBase dla plików, których nazwy zostały zaktualizowane. Te pliki JAR jest używana wewnętrznie przez HBase, więc nie oczekuje się, że klienci mają zależności na powitania nazwy tych plików JAR. Należą do nich:
<ul>
<li>./lib/jetty-6.1.26.hwx.JAR</li>
<li>./lib/jetty-sslengine-6.1.26.hwx.JAR</li>
<li>./lib/jetty-Util-6.1.26.hwx.JAR</li>
</ul>
</td>
<td>Oprogramowanie typu open source</td>
<td>HBase</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-1292015-release-of-hdinsight"></a>Informacje o wersji 2015-1-29 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.455.1309616 (HDP 1.3.9.0-01351 — bez zmian)
* HDInsight 3.0.6.455.1309616 (HDP 2.0.9.0-2097 — bez zmian)
* HDInsight 3.1.2.455.1309616 (HDP 2.1.9.0-2196 — bez zmian)
* BRAK ZESTAWU SDK

Ta wersja zawiera hello następujących aktualizacji:

<table border="1">

<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Wpływ na obszar (na przykład usługi, składnika lub zestawu SDK)</p></th>
<th>Typ (na przykład Hadoop, HBase lub Storm) klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td>Poprawki błędów</td>
<td>Wprowadzono kilka ważnych poprawek zwiększających hello niezawodność hello klastrów usługi HDInsight podczas uaktualniania systemu Azure.</td>
<td>Usługa</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-152015-release-of-hdinsight"></a>Informacje o wersji 2015-1-5 usługi HDInsight
numery wersji pełnej Hello klastrów usługi HDInsight wdrożonych w tej wersji:

* HDInsight 2.1.10.420.1246118 (HDP 1.3.9.0-01351 — bez zmian)
* HDInsight 3.0.6.420.1246118 (HDP 2.0.9.0-2097 — bez zmian)
* HDInsight 3.1.2.420.1246118 (HDP 2.1.9.0-2196 — bez zmian)

Ta wersja zawiera hello następujące aktualizacje:

<table border="1">

<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Składnik</th>
<th>Typ klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td>Przykłady dotyczące analizy trendów w serwisie Twitter i zalecenia na podstawie Mahout film</td>
<td><p>W tej wersji hello konsoli HDInsight zapytania ma dwie dodatkowe przykłady:</p>

<p><b>Analiza trendu w usłudze Twitter</b><br>
Publiczny interfejsów API dostarczonych przez witryn, takie jak Twitter są użyteczne źródło danych do analizowania i zrozumienie trendów popularnych. W tym samouczku Dowiedz się, jak toouse Hive tooget listę użytkowników usługi Twitter, wysłanych hello większości tweetów zawierający określonego wyrazu. </p>

<p><b>Zalecenie mahout film</b><br>
Apache Mahout jest maszyny platformy Apache Hadoop uczenia biblioteki. Mahout zawiera algorytmy przetwarzania danych (na przykład filtrowanie, klasyfikacji i klaster). W tym samouczku Użyj zalecenie aparat toogenerate filmu zalecenia oparte na filmów, które miały Twoich znajomych.</p></td>
<td>Zapytanie konsoli</td>
<td>Usługa Hadoop</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Zmień wartość toodefault konfiguracji Hive: hive.auto.convert.join.noconditionaltask.size</td>
<td><p>Ta konfiguracja rozmiar stosuje tooautomatically przekonwertować mapy sprzężenia. wartość Hello reprezentuje sumę hello rozmiary hello tabel, które mogą być przekonwertowana toohash map, które mieszczą się w pamięci. W poprzednich wersjach wartość ta zwiększona z wartości domyślnej powitania od 10 MB too128 MB. Jednak hello nową wartość 128 MB powodował toofail zadania z powodu toolack pamięci. Ta wersja zostanie przywrócona wartość domyślna hello kopii too10 MB. Klienci mogą nadal wybrać toooverride tę wartość podczas tworzenia klastra, biorąc pod uwagę ich zapytania i rozmiary tabeli. Aby uzyskać więcej informacji na temat tego ustawienia i w jaki sposób toooverride, zobacz <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.0.2/ds_Hive/optimize-joins.html#JoinOptimization-OptimizeAutoJoinConversion" target="_blank">zoptymalizować automatycznego dołączenia konwersji</a> w dokumentacji Hortonworks. </p></td>
<td>Hive</td>
<td>Hadoop, Hbase</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-12232014-release-of-hdinsight"></a>Informacje o wersji 2014-12-23 usługi hdinsight
Hello pełną wersję liczby klastrów HDInsight wdrożonych w tej wersji są:

* HDInsight 2.1.10.420.1246783 (HDP wersja bez zmian)
* HDInsight 3.0.6.420.1246783 (HDP wersja bez zmian)
* HDInsight 3.1.1.420.1246783 (HDP wersja bez zmian)

Ta wersja zawiera hello następujących aktualizacji:

<table border="1">
<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Składnik</th>
<th>Typ klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td>Błędy tworzenia klastra sporadyczne powodu tooexcessive obciążenia</td>
<td><p>Ulepszone algorytm pobierania pakietów HDP podczas tworzenia klastra umożliwia bardziej niezawodna obsługa błędów powodu tooexcessive obciążenia.</p></td>
<td>Usługa</td>
<td>Hadoop, Hbase, Storm</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-12182014-release-of-hdinsight"></a>Informacje o wersji 2014-12-18 usługi hdinsight
Ta wersja zawiera powitania po aktualizacji składników:

<table border="1">
<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Składnik</th>
<th>Typ klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td><a href = "hdinsight-hadoop-customize-cluster.md" target="_blank">Dostosowywanie ogólnej dostępności klastra</a></td>
<td><p>Dostosowania zapewnia możliwość hello można toocustomize Twojej usłudze Azure HDInsight clusters z projektów, które są dostępne w ekosystemie Apache Hadoop hello. Dzięki tej nowej funkcji można wypróbować i wdrażać Hadoop projekty tooAzure HDInsight. Ta opcja jest włączona za pośrednictwem hello **akcji skryptu** funkcji, która może zmodyfikować klastrów platformy Hadoop w dowolny sposób za pomocą skryptów niestandardowych. Takie dostosowanie jest dostępna dla wszystkich typów w tym Hadoop, HBase i Storm w usłudze hdinsight. power hello toodemonstrate tej możliwości, możemy udokumentowane hello procesu tooinstall hello popularnych <a href = "hdinsight-hadoop-spark-install.md" target="_blank">Spark</a>, <a href = "hdinsight-hadoop-r-scripts.md" target="_blank">R</a>, <a href = "hdinsight-hadoop-solr-install.md" target="_blank">Solr</a>, i <a href = "hdinsight-hadoop-giraph-install.md" target="_blank">Giraph</a> modułów. Ta wersja również dodaje możliwość hello toospecify klientów swoje działania niestandardowego skryptu, za pośrednictwem portalu Azure hello, zawiera wskazówki i najlepsze rozwiązania dotyczące sposobu toobuild niestandardowego skryptu akcji przy użyciu metody pomocnicze i zawiera wskazówki dotyczące tootest Witaj akcji skryptu. </p></td>
<td>Dostępność funkcji ogólne</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-12052014-release-of-hdinsight"></a>Informacje o wersji 2014-12-05 usługi hdinsight
Hello pełną wersję liczby klastrów HDInsight wdrożonych w tej wersji są:

* HDInsight 2.1.9.406.1221105 (HDP 1.3.9.0-01351)
* HDInsight 3.0.5.406.1221105 (HDP 2.0.9.0-2097)
* HDInsight 3.1.1.406.1221105 (HDP 2.1.9.0-2196)
* Zestaw SDK HDInsight n/d

Ta wersja zawiera następujące aktualizacje składników hello:

<table border="1">
<tr>
<th>Tytuł</th>
<th>Opis</th>
<th>Składnik</th>
<th>Typ klastra</th>
<th>JIRA (jeśli dotyczy)</th>
</tr>
<tr>
<td>Poprawka usterki: tymczasowy błąd podczas dodawania dużej liczby partycji tabeli tooa w pliku DDL Hive </td>
<td><p>Jeśli występuje błąd sporadyczne połączenia z bazą danych potrzeby magazynu metadanych Hive hello podczas dodawania wielu tabeli Hive tooa partycji, hello Hive DDL może zakończyć się niepowodzeniem. Ten błąd występuje po isseen instrukcji w dzienniku błędów Hive hello Hello: </p><p>"Błąd [main]: ql. Sterownik (SessionState.java:printError(547)) - nie powiodło się: błąd podczas wykonywania, kod powrotny 1 z org.apache.hadoop.hive.ql.exec.DDLTask. MetaException (message:java.lang.RuntimeException: commitTransaction została wywołana, ale openTransactionCalls = 0. To prawdopodobnie wskazuje, że są niezrównoważone wywołania tooopenTransaction/commitTransaction)"</p></td>
<td>Hive</td>
<td>Hadoop, Hbase</td>
<td>GAŁĄŹ-482 (jest to wewnętrzny JIRA, dlatego nie może być podane zewnętrznie. Zauważyć odwołania.)</td>
</tr>
<tr>
<td>Poprawka usterki: okazjonalne zawieszenie w hello HDInsight zapytania konsoli</td>
<td>W takim przypadku hello następująca instrukcja są widoczne w dzienniku WebHCat hello hello WebHCat uruchamiania zadania: <p>"org.apache.hive.hcatalog.templeton.CatchallExceptionMapper | org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.yarn.exceptions.YarnRuntimeException): nie można załadować pliku historii {pliku historii toohello adres url wasb} "</p></td>
<td>Usługi WebHCat</td>
<td>Usługa Hadoop</td>
<td>GAŁĄŹ-482 (jest to wewnętrzny JIRA, dlatego nie może być podane zewnętrznie. Zauważyć odwołania.)</td>
</tr>
<tr>
<td>Poprawka usterki: okazjonalne kolekcji opóźnienia kwerend bazy danych Hbase</td>
<td>W takim przypadku użytkownicy zauważyć okazjonalne kolekcji 3 sekundy opóźnienia hello kwerend bazy danych Hbase. </td>
<td>Brama klastra usługi HDInsight</td>
<td>HBase</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>HDP JAR zmiany nazwy pliku</td>
<td>W przypadku HDI klastra w wersji 3.0, istnieje kilka zmian toohello wewnętrzny JAR plików instalowanych przez HDP. jetty 6.1.26.jar zostało zastąpione jetty 6.1.26.hwx.jar. jetty-util-6.1.26.jar jetty-util-6.1.26.hwx.jar został zastąpiony. Te zmiany mają zastosowanie tooHadoop, Mahout, WebHCat i Oozie projektów.</td>
<td>Hadoop, Mahout, WebHCat, Oozie</td>
<td>Hadoop, HBase</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-11212014-release-of-hdinsight"></a>Informacje o wersji 2014-11-21 usługi hdinsight
Hello pełną wersję liczby klastrów HDInsight wdrożonych w tej wersji są:

* HDInsight 2.1.9.382.1169709 (bez zmian od 11/14/2014)
* HDInsight 3.0.5.382.1169709 (bez zmian od 11/14/2014)
* HDInsight 3.1.1.382.1169709 (bez zmian od 11/14/2014)
* Zestaw SDK HDInsight 1.4.0

Ta wersja zawiera następujące aktualizacje składników hello:

<table border="1">
<tr><th>Tytuł</th><th>Opis</th><th>Składnik</th><th>Typ klastra</th><th>JIRA (jeśli dotyczy)</th></tr>
<tr>
<td>Podczas uzyskiwania dostępu do dzienników aplikacji</td>
<td>Możliwość tooprogrammatically Wyliczanie aplikacji działających w klastrach i toodownload odpowiednich Dzienniki aplikacji lub kontener toohelp debugowania problematyczne aplikacje.</td>
<td>SDK</td>
<td>Usługa Hadoop</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Nazwa regionu toospecify możliwości IHdInsightClient.DeleteCluster </td>
<td>Hello zestawu SDK usługi Azure HDInsight udostępnia hello możliwości toospecify nazwę regionu przy użyciu **DeleteCluster**. Dzięki temu klienci, którzy ma dwa zasoby o tej samej nazwie w różnych regionach i był toodelete nie można odblokować każdej z nich.</td>
<td>SDK</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>ClusterDetails.DeploymentId</td>
<td>Witaj **ClusterDetails** zwraca obiekt **DeploymentID** pole reprezentuje unikatowy identyfikator dla hello klastra. Gwarantowane toobe unikatowy przez utworzenie klastra prób z hello takie same nazwy.</td>
<td>SDK</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
</table>

## <a name="notes-for-11142014-release-of-hdinsight"></a>Informacje o wersji 2014-11-14 usługi hdinsight

Hello pełną wersję liczby klastrów HDInsight wdrożonych w tej wersji są:

* HDInsight 2.1.9.382.1169709
* HDInsight 3.0.5.382.1169709
* HDInsight 3.1.1.382.1169709

Ta wersja zawiera hello następujące nowe funkcje, aktualizacje składników i poprawki błędów.

<table border="1">
<tr><th>Tytuł</th><th>Opis</th><th>Składnik</th><th>Typ klastra</th><th>JIRA (jeśli dotyczy)</th></tr>
<tr>
<td>Akcja skryptu (wersja zapoznawcza)</td>
<td>Podgląd hello klastra dostosowania funkcja, która umożliwia modyfikowanie Hadoop clusters w dowolny sposób za pomocą skryptów niestandardowych. Dzięki tej funkcji Użytkownicy mogą eksperymentować i wdrażania projektów, które są dostępne w hello tooAzure ekosystemu platformy Apache Hadoop, które klastrów usługi HDInsight. Ta funkcja dostosowywania jest dostępne na wszystkich typach klastrów HDInsight Hadoop, HBase i Storm.</td>
<td>Nowa funkcja</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Zadania wbudowane Azure analizy dzienników witryn sieci Web i magazynu</td>
<td>Witaj HDInsight zapytania konsoli ma wprowadzenie galerii, obsługującą rozwiązania, które działają na podstawie danych na przykładowych danych.
<p>**Rozwiązania, które działają na podstawie danych**:<br>
Utworzona zadania dla niektórych hello najbardziej typowych danych analizy scenariuszy tooprovide punkt początkowy do tworzenia własnych rozwiązań. Dane można użyć z hello toosee zadania, jak to działa. Następnie, gdy wszystko będzie gotowe, użyj informacjach uzyskanych toocreate rozwiązania, które jest modelowane hello wbudowane zadania.</p>
<p>**Rozwiązania, które działają na przykładowych danych**:<br>
Dowiedz się, jak toowork z usługą HDInsight przez Instruktaż niektóre podstawowe scenariusze (na przykład analizowanie danych czujnika i dzienniki sieci web). Dowiesz się, jak tooanalyze HDInsight toouse takich danych i jak można łączyć inne dane toothis aplikacji i usług. Wizualizacja danych łącząc tooMicrosoft programu Excel zawiera przykład power hello tego podejścia.</p></td>
<td>Zapytanie konsoli</td>
<td>Usługa Hadoop</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Poprawka przeciek pamięci w Templeton</td>
<td>Przeciek pamięci w Templeton, która dotyczy klientów, którzy były długotrwałe klastrów lub zostały przesyłania 100s zadania żądania drugiej został rozwiązany. Witaj problem dyskowe widoczne jako Templeton 5xx błędów i rozwiązania hello został toorestart hello usługi. Obejście Hello jest już potrzebne.</td>
<td>Templeton</td>
<td>Wszystkie</td>
<td>https://issues.apache.org/jira/Browse/HADOOP-11248</td>
</tr>
</table>

> [!NOTE]
> ma zostały udokumentowane toodemonstrate hello nowe funkcje udostępniane przez dostosowanie klastra, procedur hello przy użyciu akcji skryptu tooinstall Spark i modułów R w klastrze. Aby uzyskać więcej informacji, zobacz:

* [Zainstalować i używać Spark 1.0 w klastrach HDInsight](hdinsight-hadoop-spark-install.md)
* [Zainstaluj i użyj języka R w klastrach HDInsight Hadoop](hdinsight-hadoop-r-scripts.md)

## <a name="notes-for-11072014-release-of-hdinsight"></a>Informacje o wersji 2014-11-07 usługi hdinsight

Hello numery wersji pełnej dla klastrów usługi HDInsight, które są wdrożone w tej wersji są:

* HDInsight 2.1 2.1.9.374.1153876
* HDInsight 3.0 3.0.5.374.1153876
* HDInsight 3.1 3.1.1.374.1153876

Ta wersja zawiera następujące aktualizacje składników hello:

<table border="1">
<tr><th>Tytuł</th><th>Opis</th><th>Składnik</th><th>Typ klastra</th><th>JIRA (jeśli dotyczy)</th></tr>
<tr>
<td>HDP 2.1.7</td>
<td>Ta wersja jest oparty na Hortonworks Data Platform (HDP) 2.1.7. Aby uzyskać więcej informacji, zobacz <a href="http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html" target="_blank">informacje o wersji dla HDP 2.1.7</a>.</td>
<td>HDP</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>YARN osi czasu serwera</td>
<td>Witaj YARN osi czasu serwera (nazywanego także hello ogólny serwera historii aplikacji) została włączona domyślnie. Hello osi czasu serwera zawiera ogólne informacje o ukończone aplikacje (na przykład identyfikator aplikacji, nazwy aplikacji, stan aplikacji, czas przesyłania aplikacji i czas ukończenia aplikacji).

Informacje o tej aplikacji można pobrać z węzłem głównym powitania po zalogowaniu się do identyfikatora URI http://headnodehost:8188 hello lub uruchomione polecenie YARN hello: yarn aplikacja — lista appStates — wszystkie.

Informacje te można również pobrać zdalnie chociaż interfejsu API REST na https://{ClusterDnsName}. azurehdinsight.NET/ws/V1/applicationhistory/.

Aby uzyskać szczegółowe informacje, zobacz <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN osi czasu serwera</a>.</td>
<td>Usługi, YARN</td>
<td>Hadoop, HBase</td>
<td>Nie dotyczy</td>
</tr>
<tr>
<td>Identyfikator wdrożenia klastra</td>
<td>Począwszy od zestawu SDK w wersji 1.3.3.1.5426.29232, użytkownicy mogą uzyskać dostęp Unikatowy identyfikator dla każdego klastra, które wydaje HDInsight. To umożliwia toofigure klientów limit unikatowy wystąpienia klastrów, gdy nazwa DNS jest ponownie używany przez tworzenie lub porzucić scenariuszy.</td>
<td>SDK</td>
<td>Wszystkie</td>
<td>Nie dotyczy</td>
</tr>
</table>

> [!NOTE]
> usterki Hello, który uniemożliwił numer wersji pełnej hello wyświetlane w portalu hello lub zwracanych przez hello zestawu SDK lub środowiska Windows PowerShell został rozwiązany w tej wersji.

## <a name="notes-for-10152014-release"></a>Informacje o wersji 2014-10-15

Ta wersja poprawki stała Templeton, na które wpływ hello użytkownicy z Templeton przeciek pamięci. W niektórych przypadkach użytkownicy, którzy silnie wykonywane Templeton zobaczy błędy dyskowe widoczne jako 500 kody błędów, ponieważ żądania hello nie miałoby toorun za mało pamięci. Witaj obejście tego problemu jest toorestart hello Templeton usługi. Ten problem został rozwiązany.

## <a name="notes-for-1072014-release"></a>Informacje o wersji 2014-10-7

* Korzystając z narzędzia Ambari punktu końcowego, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", hello *host_name* pola zwraca Witaj w pełni kwalifikowana nazwa domeny (FQDN) węzła hello zamiast hello tylko nazwę hosta. Na przykład zamiast zwracać "**headnode0**", Pobierz hello FQDN"**headnode0. { .Net gt;. azurehdinsight.NET ClusterDNS}**". Ta zmiana została scenariusze wymagane toofacilitate wdrożonym wiele typów klastra (na przykład HBase i Hadoop) w jedną sieć wirtualną. Dzieje się tak, na przykład w przypadku używania bazy danych HBase jako platforma wewnętrzna dla platformy Hadoop.

* Utworzono nowe ustawienia pamięci dla hello domyślnym wdrożeniu programu hello klastra usługi HDInsight. Poprzednie ustawienia pamięci domyślny nie został uwzględniony odpowiednio hello wskazówki hello liczba rdzeni Procesora wdrażany. Te nowe ustawienia pamięci powinien zapewnić lepszą wartości domyślnych (zgodnie z zaleceniami Hortonworks). toochange, zapoznaj się z dokumentacją odwołanie do zestawu SDK toohello o zmianie konfiguracji klastra. Hello nowych pamięci ustawień, które są używane przez klaster usługi HDInsight hello domyślne 4 Procesora core (kontener 8) są wymienione w poniższej tabeli hello. (hello wartości używane toothis wcześniejszych wersji podawane są również parenthetically.)

<table border="1">
<tr><th>Składnik</th><th>Alokacja pamięci</th></tr>
<tr><td> yarn.Scheduler.minimum alokacji</td><td>768 MB (wcześniej 512 MB)</td></tr>
<tr><td> yarn.Scheduler.Maximum alokacji</td><td>6144 MB (bez zmian)</td></tr>
<tr><td>yarn.nodemanager.Resource.Memory</td><td>6144 MB (bez zmian)</td></tr>
<tr><td>mapreduce.map.Memory</td><td>768 MB (wcześniej 512 MB)</td></tr>
<tr><td>mapreduce.map.Java.opts</td><td>Wyłącza funkcję Xmx512m = (wcześniej - Xmx410m)</td></tr>
<tr><td>mapreduce.Reduce.Memory</td><td>1536 MB (wcześniej 1024 MB)</td></tr>
<tr><td>mapreduce.Reduce.Java.opts</td><td>Wyłącza funkcję Xmx1024m = (wcześniej - Xmx819m)</td></tr>
<tr><td>yarn.App.mapreduce.AM.Resource</td><td>768 MB (wcześniej 1024 MB)</td></tr>
<tr><td>yarn.App.mapreduce.AM.Command</td><td>Wyłącza funkcję Xmx512m = (wcześniej - Xmx819m)</td></tr>
<tr><td>mapreduce.Task.IO.sort</td><td>256 MB (wcześniej 200 MB)</td></tr>
<tr><td>tez.AM.Resource.Memory</td><td>1536 MB (bez zmian)</td></tr>
</table>

Aby uzyskać więcej informacji o ustawieniach konfiguracji pamięci hello używany przez YARN i MapReduce na powitania platformie Hortonworks Data Platform, który jest używany przez usługi HDInsight, zobacz [określić ustawienia konfiguracji pamięci HDP](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1-latest/bk_installing_manually_book/content/rpm-chap1-11.html). Hortonworks w nim również podane narzędzie toocalculate pamięci odpowiednie ustawienia.

Dotyczące hello Azure PowerShell i hello zestawu SDK HDInsight komunikat: "*klastra nie jest skonfigurowany do dostępu do usług HTTP*":

* Ten błąd jest znanego [problem ze zgodnością](https://social.msdn.microsoft.com/Forums/azure/a7de016d-8de1-4385-b89e-d2e7a1a9d927/hdinsight-powershellsdk-error-cluster-is-not-configured-for-http-services-access?forum=hdinsight) , które mogą występować powodu różnicy tooa hello wersji z zestawu SDK HDInsight hello lub Azure PowerShell i hello hello klastra. Klastrów utworzonych na 8/15 lub nowszej obsługują nowe możliwości inicjowania obsługi administracyjnej do sieci wirtualnych. Jednak ta funkcja nie jest poprawnie interpretowany przez starsze wersje zestawu SDK HDInsight hello lub Azure PowerShell. wynik Hello jest błąd w niektórych operacji przesyłania zadania. Jeśli używasz interfejsów API zestawu SDK HDInsight lub Azure PowerShell polecenia cmdlet (**AzureRmHDInsightCluster użyj** lub **Invoke AzureRmHDInsightHiveJob**) zadania toosubmit te operacje może zakończyć się niepowodzeniem z komunikatem o błędzie hello " *Klastra <clustername> nie jest skonfigurowany do dostępu do usług HTTP*. " Lub (w zależności od operacji hello), mogą wystąpić inne komunikaty o błędach, takich jak "*nie można połączyć z toocluster*".
* Te problemy ze zgodnością są rozpoznawane w hello najnowsze wersje hello HDInsight SDK i programu Azure PowerShell. Zalecamy zaktualizowanie hello zestawu SDK HDInsight tooversion 1.3.1.6 lub nowszym i Azure PowerShell narzędzia tooversion 0.8.8 lub nowszym. Możesz uzyskać dostępu do toohello najnowsze SDK HDInsight [NugGet](http://nuget.codeplex.com/wikipage?title=Getting%20Started) i hello Azure PowerShell narzędzia [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

## <a name="notes-for-9122014-release-of-hdinsight-31"></a>Informacje o wersji 2014-12/9 HDInsight w wersji 3.1
* Ta wersja jest oparty na Hortonworks Data Platform (HDP) 2.1.5. Lista błędów hello stałym w tej wersji, zobacz hello [stałym w tej wersji](http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.5/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.5-fixed.html) w witrynie Hortonworks hello.
* W folderze biblioteki Pig Witaj, "avro-mapred-1.7.4.jar" hello plik został zmieniony zbyt "avro-mapred-1.7.4-hadoop2.jar." Witaj zawartość tego pliku zawiera pomocnicza Poprawka usterki nierozdzielające. Zaleca się, klienci nie wprowadzaj zależności bezpośrednich hello nazwę hello JAR podziały tooavoid pliku po zmianie nazw plików.

## <a name="notes-for-8212014-release"></a>Informacje o wersji 2014-8-21
* Dodajemy powitania po konfiguracji WebHCat (gałąź-7155), która ustawia domyślny limit pamięci dla kontrolera Templeton hello zadania too1 GB. (hello poprzednią wartość domyślna została 512 MB).

     templeton.mapper.Memory.MB (= 1024)

  * Zmiana ta dotyczy hello następujący błąd z powodu ograniczeń pamięci toolower niektórych zapytań programu Hive: "Kontenera jest uruchomiona poza limity pamięci fizycznej."
  * toorevert toohello stare ustawienia domyślne, można ustawić too512 wartość tej konfiguracji za pomocą programu Azure PowerShell w czasie tworzenia klastra przy użyciu hello następujące polecenie:

      Dodaj AzureRmHDInsightConfigValues-Core @{"templeton.mapper.memory.mb"="512";}
* Nazwa hosta Hello hello dozorcy roli została zmieniona zbyt*dozorcy*. Ma to wpływ na rozpoznawanie nazw w ramach klastra hello, ale nie ma wpływu na zewnętrznych interfejsów API REST. Jeśli masz składniki w tym hello użyj *zookeepernode* nazwy hosta należy tooupdate ich toouse nową nazwę. nowe nazwy hello trzy węzły dozorcy Hello są:

  * zookeeper0
  * zookeeper1
  * zookeeper2
* Macierzy obsługi wersji bazy danych HBase jest aktualizowana. HDInsight w wersji 3.1 (HBase wersji 0,98) jest obsługiwana w środowisku produkcyjnym dla obciążeń HBase. Wersja 3.0 (która jest dostępna dla wersji zapoznawczej) nie jest obsługiwana przenoszenie do przodu.

## <a name="notes-about-clusters-created-prior-too8152014"></a>Uwagi dotyczące klastrów utworzone przed too8 15 2014-
Komunikat o błędzie programu Azure PowerShell lub zestawu SDK HDInsight "klastra <clustername> nie jest skonfigurowany do dostępu do usług HTTP" (lub w zależności od operacji hello, inne komunikaty o błędach takich jak: "Nie można połączyć z toocluster") można napotkać powodu różnice wersji tooa między programu Azure PowerShell lub zestawu SDK HDInsight hello klastrem. Klastrów utworzonych na 8/15 lub nowszej obsługują nowe możliwości inicjowania obsługi administracyjnej do sieci wirtualnych. Ta funkcja nie jest prawidłowo interpretowane przez starsze wersje hello Azure PowerShell lub hello SDK HDInsight, co prowadzi do niepowodzenia operacji przesyłania zadań. Jeśli używasz programu Azure PowerShell polecenia cmdlet (np. Użyj AzureRmHDInsightCluster lub Invoke-AzureRmHDInsightHiveJob) toosubmit zadania lub interfejsów API zestawu SDK HDInsight te operacje może zakończyć się niepowodzeniem z opisem komunikaty o błędach hello.

Te problemy ze zgodnością są rozpoznawane w hello najnowsze wersje hello HDInsight SDK i programu Azure PowerShell. Zalecamy zaktualizowanie hello zestawu SDK HDInsight tooversion 1.3.1.6 lub nowszym i Azure PowerShell narzędzia tooversion 0.8.8 lub nowszym. Możesz uzyskać dostępu do toohello najnowsze SDK HDInsight [NuGet][nuget-link]. Hello Azure PowerShell narzędzia mogą korzystać za pomocą [Instalatora platformy sieci Web firmy Microsoft][webpi-link].

## <a name="notes-for-7282014-release"></a>Informacje o wersji 2014-7-28
* **HDInsight, które są dostępne w nowych regionów**: rozszerzona firma Microsoft HDInsight geograficzne obecności toothree regionów. HDInsight klienci mogą tworzyć klastry w tych obszarach:
  * Azja Wschodnia
  * Środkowo-północne stany USA
  * Środkowo-południowe stany USA
* HDInsight w wersji 1.6 (HDP 1.1 i Hadoop 1.0.3) oraz usługi HDInsight w wersji 2.1 (HDP1.3 i Hadoop 1.2) są usuwane z hello portalu Azure. Dla tych wersji przy użyciu hello polecenia cmdlet programu Azure PowerShell, można kontynuować klastrów platformy Hadoop toocreate [AzureRmHDInsightCluster nowy](http://msdn.microsoft.com/library/dn593744.aspx) lub za pomocą hello [zestawu SDK HDInsight](http://msdn.microsoft.com/library/azure/dn469975.aspx). Aby uzyskać więcej informacji, zobacz [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md).
* Hortonworks Data Platform (HDP) zmiany w tej wersji:

<table border="1">
<tr><th>HDP</th><th>Zmiany</th></tr>
<tr><td>HDP 1.3 / HDI 2.1</td><td>Brak zmian</td></tr>
<tr><td>HDP 2.0 / HDI 3.0</td><td>Brak zmian</td></tr>
<tr><td>HDP 2.1 / HDI 3.1</td><td>dozorcy: [3.4.5.2.1.3.0-1948] -> [3.4.5.2.1.3.2-0002]</td></tr>
</table>

## <a name="notes-for-6242014-release"></a>Informacje o wersji 2014-6-24
Ta wersja zawiera usługi HDInsight toohello ulepszenia:

* **Dostępność HDP 2.1**: 3.1 HDInsight, (zawierający HDP 2.1) jest ogólnie dostępna i hello wersja domyślna dla nowych klastrów.
* **HBase - ulepszenia portalu Azure**: udostępniamy klastrów HBase w wersji zapoznawczej. Można utworzyć klastry z bazy danych HBase z portalu hello za pomocą kilku kliknięć.

Z bazy danych HBase można utworzyć różnych obciążeń w czasie rzeczywistym w usłudze HDInsight, interaktywne witryny sieci Web pracować z dużymi zestawami danych tooservices przechowywania danych czujników i danych telemetrycznych z milionów punktów końcowych. Witaj następnym krokiem powinno być tooanalyze hello dane w tych obciążeń przy użyciu zadań platformy Hadoop, a jest to możliwe w usłudze HDInsight przy użyciu programu Azure PowerShell i pulpit nawigacyjny klastra Hive hello.

### <a name="apache-mahout-preinstalled-on-hdinsight-31"></a>Apache Mahout preinstalowany w usłudze HDInsight w wersji 3.1
 [Mahout](http://hortonworks.com/hadoop/mahout/) jest wstępnie zainstalowane w klastrach HDInsight 3.1 Hadoop, dlatego można uruchamiać zadania Mahout bez potrzeby hello konfiguracji dodatkowych klastra. Na przykład można zdalnego do klastra usługi Hadoop za pomocą protokołu RDP (Remote Desktop) i bez dodatkowych kroków, możesz uruchomić następujące polecenie Hello World Mahout hello:

        mahout org.apache.mahout.classifier.df.tools.Describe -p /user/hdp/glass.data -f /user/hdp/glass.info -d I 9 N L

        mahout org.apache.mahout.classifier.df.BreimanExample -d /user/hdp/glass.data -ds /user/hdp/glass.info -i 10 -t 100

Bardziej szczegółowy opis tej procedury, zobacz dokumentację hello hello [przykład Breiman](https://mahout.apache.org/users/classification/breiman-example.html) na powitania Apache Mahout witryny sieci Web.

### <a name="hive-queries-can-use-tez-in-hdinsight-31"></a>Zapytań programu hive można użyć aplikacji Tez w usłudze HDInsight w wersji 3.1
Gałąź 0,13 cala jest dostępna w usłudze HDInsight w wersji 3.1 i jest w stanie uruchamiania zapytań przy użyciu aplikacji Tez, którego można użyć do znacznej wydajności.
Tez nie jest włączone domyślnie dla zapytań programu Hive. toouse, należy wybrać w. Tez można włączyć, uruchamiając hello następującego fragmentu kodu:

        set hive.execution.engine=tez;
        select sc_status, count(*), histogram_numeric(sc_bytes,5) from website_logs_orc_local group by sc_status;

Hortonworks został opublikowany szczegółowy podział usprawnień wydajności zapytań Hive z Tez dostarczonych w standardowych danych wyjściowych. Aby uzyskać więcej informacji, zobacz [przeprowadzenia testów porównawczych Apache Hive 13 dla platformy Hadoop Enterprise](http://hortonworks.com/blog/benchmarking-apache-hive-13-enterprise-hadoop/).

Aby uzyskać więcej informacji, zobacz [Hive w aplikacji Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez).

### <a name="global-availability"></a>Dostępnością globalną
Witaj wersji z usługi HDInsight w wersji 2.2 Hadoop, firma Microsoft udostępniła HDInsight w wszystkich głównych regionów geograficznych, gdy platforma Azure jest dostępna. W szczególności hello zachodnie Europie i Azji Południowo-Wschodnia centrów danych ma został przełączony w tryb online. Dzięki temu klienci toolocate klastrów w centrum danych, które jest bliskie i potencjalnie w strefie podobne wymagania zgodności.

### <a name="dos--donts-between-cluster-versions"></a>DOS & zakazy między wersjami klastra
**Magazyny Oozie używane z klastra usługi HDInsight w wersji 3.1 nie są zgodne z klastrami HDInsight 2.1 i nie można ich używać z tą wersją poprzedniej**.

Niestandardowe Oozie potrzeby magazynu metadanych bazy danych z klastra usługi HDInsight w wersji 3.1 nie można użyć ponownie z klastrem usługi HDInsight 2.1. Dotyczy to hello nawet hello potrzeby magazynu metadanych pochodzi z klastrem usługi HDInsight 2.1. W tym scenariuszu nie jest obsługiwana, ponieważ schemat potrzeby magazynu metadanych hello pobiera uaktualniony, w przypadku użycia z klastra usługi HDInsight w wersji 3.1, więc nie jest już zgodny z hello wymagane przez klastry HDInsight 2.1 hello potrzeby magazynu metadanych. Wszelkie próby tooreuse potrzeby magazynu metadanych Oozie, który został użyty z klastrem usługi HDInsight w wersji 3.1 renderowania klastra usługi HDInsight 2.1 hello bezużyteczny.

**Nie można współużytkować magazyny Oozie w klastrach.**

Magazyny Oozie są dołączone toospecific klastrów, a nie może być współużytkowana przez klastry.

### <a name="breaking-changes"></a>Fundamentalne zmiany
**Prefiks składni**: tylko Witaj "wasb: / /" składnia jest obsługiwana w klastrach 3.0 i HDInsight w wersji 3.1. Witaj starsze "asv: / /" składnia jest obsługiwana w HDInsight 2.1 i 1.6 klastrów, ale nie jest obsługiwana w usłudze HDInsight w wersji 3.1 lub 3.0 klastrów. Oznacza to, że wszystkie zadania przesłane tooan HDInsight w wersji 3.1 lub 3.0 klastra, która jawnie używa powitania "asv: / /" składni zakończy się niepowodzeniem. Witaj "wasb: / /" zamiast tego należy użyć składni. Ponadto zadania przesłane tooany HDInsight w wersji 3.1 lub 3.0 klastrów, które zostały utworzone z istniejących potrzeby magazynu metadanych zawierającego jawne odwołuje się do tooresources przy użyciu hello "asv: / /" składni zakończy się niepowodzeniem. Te magazyny metadanych muszą toobe ponownie utworzone przy użyciu hello "wasb: / /" składni tooaddress zasobów.

**Porty**: hello porty używane przez usługi HDInsight hello zostały zmienione. zostały Hello numery portów, które były używane w ramach zakresu portów efemerycznych hello systemu operacyjnego Windows hello. Porty są przydzielane automatycznie z wstępnie zdefiniowanego zakresu tymczasowych w krótkim okresie internetowych opartych na protokole komunikacji. Nowy zestaw dozwolonych numerów portów usługi Hortonworks Data Platform (HDP) Hello są poza tym tooavoid zakresu występują konflikty, które mogą wystąpić z hello porty używane przez usługi działające na powitania węzła głównego. Witaj nowych numerów portów nie powinno powodować zmiany podziału. numery Hello używane są następujące:

 **HDInsight w wersji 1.6 (HDP 1.1)**

<table border="1">
<tr><th>Nazwa</th><th>Wartość</th></tr>
<tr><td>DFS.http.address</td><td>namenodehost:30070</td></tr>
<tr><td>DFS.datanode.address</td><td>0.0.0.0:30010</td></tr>
<tr><td>DFS.datanode.http.address</td><td>0.0.0.0:30075</td></tr>
<tr><td>DFS.datanode.IPC.address</td><td>0.0.0.0:30020</td></tr>
<tr><td>DFS.Secondary.http.address</td><td>0.0.0.0:30090</td></tr>
<tr><td>mapred.job.Tracker.http.address</td><td>jobtrackerhost:30030</td></tr>
<tr><td>mapred.Task.Tracker.http.address</td><td>0.0.0.0:30060</td></tr>
<tr><td>mapreduce.history.Server.http.address</td><td>0.0.0.0:31111</td></tr>
<tr><td>templeton.port</td><td>30111</td></tr>
</table>

 **HDInsight 3.1 i 3.0 (HDP 2.1 i 2.0)**

<table border="1">
<tr><th>Nazwa</th><th>Wartość</th></tr>
<tr><td>adres DFS.namenode.http</td><td>namenodehost:30070</td></tr>
<tr><td>adres DFS.namenode.HTTPS</td><td>headnodehost:30470</td></tr>
<tr><td>DFS.datanode.address</td><td>0.0.0.0:30010</td></tr>
<tr><td>DFS.datanode.http.address</td><td>0.0.0.0:30075</td></tr>
<tr><td>DFS.datanode.IPC.address</td><td>0.0.0.0:30020</td></tr>
<tr><td>adres DFS.namenode.Secondary.http</td><td>0.0.0.0:30090</td></tr>
<tr><td>yarn.nodemanager.webapp.address</td><td>0.0.0.0:30060</td></tr>
<tr><td>templeton.port</td><td>30111</td></tr>
</table>

### <a name="dependencies"></a>Zależności
Witaj następujących zależności zostały dodane w usłudze HDInsight 3.x (HDP2.x):

* serwlet guice
* podstawowe optiq
* javax.inject
* aktywacji
* jsr305
* geronimo-jaspic_1.0_spec
* lip slf4j
* Java xmlbuilder
* narzędzia ANT
* Commons kompilatora
* Interfejs api jdo
* math3 Commons:
* paranamer
* jaxb impl
* stringtemplate
* eigenbase xom
* serwlet Jersey
* exec Commons:
* Interfejs api jaxb
* Serwer jetty wszystkich serwerów
* janino
* xercesImpl
* optiq avatica
* jta
* właściwości eigenbase
* groovy-all
* podstawowe hamcrest
* Poczty
* linq4j
* jpam
* Jersey klienta
* aopalliance
* geronimo-annotation_1.0_spec
* Uruchamianie narzędzia ANT
* Jersey guice
* interfejsy API XML
* Interfejs api stax
* ASM commons
* drzewo Asm
* wadl
* geronimo-jta_1.1_spec
* guice
* leveldbjni-all
* szybkość pracy
* zrzucenia
* szałowe java
* wszystkie jetty
* dbcp Commons:

Witaj następujących zależności już nie istnieje w usłudze HDInsight 3.x (HDP2.x):

* jdeb
* kfs
* sqlline
* Bluszcz
* aspectjrt
* JSON
* rdzeń
* Interfejs api jdo2
* avro mapred
* Wzmacniacz datanucleus
* JSP
* Commons rejestrowania api
* Commons matematyczne
* JavaEWAH
* aspectjtools
* javolution
* hdfsproxy
* Baza danych hbase
* szałowe

### <a name="version-changes"></a>Zmiany wersji
wprowadzono następujące zmiany w wersji Hello między HDInsight 2.x (HDP1.x) i HDInsight 3.x (HDP2.x):

* Podstawowe metryki: [2.1.2] -> [3.0.0]
* derbynet: [10.4.2.0] -> [10.10.1.1]
* datanucleus: ['rdbms-3.0.8'] -> ["rdbms-3.2.9']
* Kompilator jasper: [5.5.12] -> [5.5.23]
* log4j: ["1.2.15", "1.2.16"] -> ["1.2.16", "1.2.17"]
* derbyclient: [10.4.2.0] -> [10.10.1.1]
* httpcore: [4.2.4] -> [4.2.5]
* hsqldb: [1.8.0.10] -> [2.0.0]
* jets3t: [0.6.1] -> [0.9.0]
* protobuf java: [2.4.1] -> [2.5.0]
* DOM: [10.4.2.0] -> [10.10.1.1]
* jasper: [' środowiska uruchomieniowego-5.5.12'] -> ["środowiska wykonawczego — 5.5.23']
* demon Commons: [1.0.1] -> [1.0.13]
* podstawowe datanucleus: [3.0.9] -> [3.2.10]
* datanucleus-api-jdo: [3.0.7] -> [3.2.6]
* dozorcy: [3.4.5.1.3.9.0-01320] -> [3.4.5.2.1.3.0-1948]
* bonecp: [0.7.1.RELEASE] -> ["
* 0.8.0.RELEASE "]

### <a name="drivers"></a>Sterowniki
Hello sterownik Java połączenia bazy danych (JDBC) dla programu SQL Server jest używana wewnętrznie przez usługi HDInsight i nie jest używane dla operacji zewnętrznych. Jeśli chcesz tooconnect tooHDInsight przy użyciu otwarte połączenie bazy danych (ODBC), użyj hello sterownik Microsoft Hive ODBC. Aby uzyskać więcej informacji, zobacz [tooHDInsight łączenie programu Excel z hello sterownik Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md).

### <a name="bug-fixes"></a>Poprawki błędów
W tej wersji możemy odświeżeniu powitania po wersji usługi HDInsight kilka poprawki błędów:

* HDInsight 2.1 (HDP 1.3)
* HDInsight 3.0 (HDP 2.0)
* HDInsight 3.1 (HDP 2.1)

## <a name="hortonworks-release-notes"></a>Informacje o wersji Hortonworks
Informacje o wersji dla hello Hortonworks Data Platform (HDPs) używanych przez klastry HDInsight są dostępne pod adresem hello następujących lokalizacji:

* HDInsight w wersji 3.1 używa dystrybucji Hadoop, która jest oparta na powitania [platformie Hortonworks Data Platform 2.1.7][hdp-2-1-7]. Jest to klastra Hadoop domyślnego hello utworzenia przy użyciu portalu Azure powitania po 2014-11-7. Klastry HDInsight 3.1 utworzone przed 2014-11-7 znajdowały się na powitania [platformie Hortonworks Data Platform 2.1.1][hdp-2-1-1]
* HDInsight w wersji 3.0 używa dystrybucji Hadoop, która jest oparta na powitania [Hortonworks Data Platform 2.0][hdp-2-0-8].
* HDInsight w wersji 2.1 używa dystrybucji Hadoop, która jest oparta na powitania [Hortonworks Data Platform 1.3][hdp-1-3-0].
* HDInsight w wersji 1.6 używa dystrybucji Hadoop, która jest oparta na powitania [Hortonworks Data Platform 1.1][hdp-1-1-0].

[hdp-2-1-7]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.7-Win/bk_releasenotes_HDP-Win/content/ch_relnotes-HDP-2.1.7.html

[hdp-2-1-1]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.1/bk_releasenotes_hdp_2.1/content/ch_relnotes-hdp-2.1.1.html

[hdp-2-0-8]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.8.0/bk_releasenotes_hdp_2.0/content/ch_relnotes-hdp2.0.8.0.html

[hdp-1-3-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-1.3.0/bk_releasenotes_hdp_1.x/content/ch_relnotes-hdp1.3.0_1.html

[hdp-1-1-0]: http://docs.hortonworks.com/HDPDocuments/HDP1/HDP-Win-1.1/bk_releasenotes_HDP-Win/content/ch_relnotes-hdp-win-1.1.0_1.html

[nuget-link]: https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.HDInsight/

[webpi-link]: http://go.microsoft.com/?linkid=9811175&clcid=0x409

[hdinsight-install-spark]: ../hdinsight-hadoop-spark-install/
[hdinsight-r-scripts]: ../hdinsight-hadoop-r-scripts/
