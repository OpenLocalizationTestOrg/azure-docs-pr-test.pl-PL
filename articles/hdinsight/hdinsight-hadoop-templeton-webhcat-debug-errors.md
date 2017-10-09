---
title: "aaaUnderstand i usuń błędy WebHCat w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooabout typowe błędy zwrócone przez WebHCat w usłudze HDInsight i jak tooresolve je."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1b3d94b1-207d-4550-aece-21dc45485549
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0071a1e9ed448ae146b93c8f4f518e31b95d27c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a>Zrozumienia i rozwiązania błędów, odbierane z usługi WebHCat w usłudze HDInsight

Więcej informacji na temat błędów przy użyciu usługi WebHCat w usłudze HDInsight i jak tooresolve je. WebHCat jest używana wewnętrznie przez narzędzia po stronie klienta, takich jak Azure PowerShell i hello narzędzi Data Lake Tools dla programu Visual Studio.

## <a name="what-is-webhcat"></a>Co to jest WebHCat

[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) to interfejs API REST dla [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), tabeli i magazynu warstwa zarządzania dla platformy Hadoop. WebHCat jest domyślnie włączone w klastrach HDInsight i jest używany przez różne zadania toosubmit narzędzia, Pobierz stan zadania, itp., bez konieczności logowania się w klastrze toohello.

## <a name="modifying-configuration"></a>Modyfikowanie konfiguracji

> [!IMPORTANT]
> Występuje kilka błędów hello wymienione w niniejszym dokumencie, ponieważ została przekroczona maksymalna skonfigurowana. Podczas kroku rozpoznawania hello uwagi, można zmienić wartości, należy użyć jednego hello tooperform hello zmiany:

* Dla **Windows** klastrów: Użyj wartości hello tooconfigure akcji skryptu podczas tworzenia klastra. Aby uzyskać więcej informacji, zobacz [tworzenie akcji skryptów](hdinsight-hadoop-script-actions.md).

* Aby uzyskać **Linux** klastrów: wartość hello toomodify Ambari Użyj (sieć web lub interfejsu API REST). Aby uzyskać więcej informacji, zobacz [Zarządzanie HDInsight przy użyciu narzędzia Ambari](hdinsight-hadoop-manage-ambari.md)

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

### <a name="default-configuration"></a>Domyślna konfiguracja

W przypadku przekroczenia hello następujące wartości domyślne, możesz obniżyć wydajność usługi WebHCat, lub powodować błędy:

| Ustawienie | Wyniki działania | Wartość domyślna |
| --- | --- | --- |
| [yarn.Scheduler.Capacity.Maximum — aplikacje][maximum-applications] |Maksymalna liczba zadań, które mogą być jednocześnie aktywne Hello (oczekiwanie lub uruchomiona) |10 000 |
| [templeton.EXEC.max procs][max-procs] |Maksymalna liczba żądań, które mogą być przekazywane jednocześnie Hello |20 |
| [mapreduce.jobhistory.max wieku ms][max-age-ms] |Witaj liczbę dni, które Historia zadania są zachowywane. |7 dni |

## <a name="too-many-requests"></a>Zbyt wiele żądań

**Kod stanu HTTP**: 429

| Przyczyna | Rozwiązanie |
| --- | --- |
| Przekroczono hello maksymalną równoczesnych żądań obsłużonych przez WebHCat na minutę (domyślnie 20) |Zmniejsz Twojej tooensure obciążenia, czy nie przesyłać więcej niż hello maksymalną liczbę jednoczesnych żądań lub zwiększ limit równoczesnych żądań hello przez zmodyfikowanie `templeton.exec.max-procs`. Aby uzyskać więcej informacji, zobacz [modyfikowanie konfiguracji](#modifying-configuration) |

## <a name="server-unavailable"></a>Serwer jest niedostępny

**Kod stanu HTTP**: 503

| Przyczyna | Rozwiązanie |
| --- | --- |
| Ten kod stanu zazwyczaj występuje w trybie failover między hello podstawowe i pomocnicze HeadNode hello klastra |Poczekaj 2 minuty, a następnie ponów próbę wykonania operacji hello |

## <a name="bad-request-content-could-not-find-job"></a>Nieprawidłowe żądanie zawartości: nie można odnaleźć zadania

**Kod stanu HTTP**: 400

| Przyczyna | Rozwiązanie |
| --- | --- |
| Szczegóły zadania zostały wyczyszczone w historii zadań hello czyszcząca |Witaj domyślnego okresu przechowywania historii zadań wynosi 7 dni. Witaj domyślnego okresu przechowywania można zmienić, modyfikując `mapreduce.jobhistory.max-age-ms`. Aby uzyskać więcej informacji, zobacz [modyfikowanie konfiguracji](#modifying-configuration) |
| Zadanie ukończenia pracy awaryjnej tooa został zatrzymany |Spróbuj ponownie przesyłanie zadań do zapasowej tootwo minut |
| Nieprawidłowy identyfikator zadania został użyty. |Sprawdź, czy identyfikator zadania hello jest prawidłowa |

## <a name="bad-gateway"></a>Zły bramy

**Kod stanu HTTP**: 502

| Przyczyna | Rozwiązanie |
| --- | --- |
| Wewnętrzny wyrzucanie elementów bezużytecznych ma miejsce w hello procesu usługi WebHCat |Poczekaj, aż odzyskiwanie kolekcji toofinish lub ponowne uruchomienie usługi WebHCat hello |
| Upłynął limit czasu oczekiwania na odpowiedź z hello ResourceManager usługi. Ten błąd może wystąpić, gdy hello liczba aktywnych aplikacji hello skonfigurowany maksymalny (domyślnie 10 000) |Poczekaj, aż aktualnie uruchomione zadania toocomplete lub zwiększ limit równoczesnych zadań hello modyfikując `yarn.scheduler.capacity.maximum-applications`. Aby uzyskać więcej informacji, zobacz hello [modyfikowanie konfiguracji](#modifying-configuration) sekcji. |
| Próba tooretrieve wszystkie zadania za pomocą hello [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) wywołania podczas `Fields` ustawiono zbyt`*` |Nie pobierają *wszystkie* szczegóły zadania. Zamiast tego użyj `jobid` tooretrieve szczegóły zadania tylko większe niektórych identyfikator zadania. Nie używaj`Fields` |
| Witaj usługi WebHCat nie działa w trybie failover HeadNode |Poczekaj dwóch minut i ponów próbę wykonania operacji hello |
| Istnieje więcej niż 500 oczekujące zadania przesłane za pośrednictwem usługi WebHCat |Poczekaj, aż obecnie oczekujące zadania zostały ukończone przed przesłaniem więcej zadań |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
