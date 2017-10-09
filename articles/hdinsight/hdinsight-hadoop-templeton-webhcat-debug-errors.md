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
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="2f441-103">Zrozumienia i rozwiązania błędów, odbierane z usługi WebHCat w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f441-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="2f441-104">Więcej informacji na temat błędów przy użyciu usługi WebHCat w usłudze HDInsight i jak tooresolve je.</span><span class="sxs-lookup"><span data-stu-id="2f441-104">Learn about errors received when using WebHCat with HDInsight, and how tooresolve them.</span></span> <span data-ttu-id="2f441-105">WebHCat jest używana wewnętrznie przez narzędzia po stronie klienta, takich jak Azure PowerShell i hello narzędzi Data Lake Tools dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2f441-105">WebHCat is used internally by client-side tools such as Azure PowerShell and hello Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="2f441-106">Co to jest WebHCat</span><span class="sxs-lookup"><span data-stu-id="2f441-106">What is WebHCat</span></span>

<span data-ttu-id="2f441-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) to interfejs API REST dla [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), tabeli i magazynu warstwa zarządzania dla platformy Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2f441-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="2f441-108">WebHCat jest domyślnie włączone w klastrach HDInsight i jest używany przez różne zadania toosubmit narzędzia, Pobierz stan zadania, itp., bez konieczności logowania się w klastrze toohello.</span><span class="sxs-lookup"><span data-stu-id="2f441-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools toosubmit jobs, get job status, etc. without logging in toohello cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="2f441-109">Modyfikowanie konfiguracji</span><span class="sxs-lookup"><span data-stu-id="2f441-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f441-110">Występuje kilka błędów hello wymienione w niniejszym dokumencie, ponieważ została przekroczona maksymalna skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="2f441-110">Several of hello errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="2f441-111">Podczas kroku rozpoznawania hello uwagi, można zmienić wartości, należy użyć jednego hello tooperform hello zmiany:</span><span class="sxs-lookup"><span data-stu-id="2f441-111">When hello resolution step mentions that you can change a value, you must use one of hello following tooperform hello change:</span></span>

* <span data-ttu-id="2f441-112">Dla **Windows** klastrów: Użyj wartości hello tooconfigure akcji skryptu podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="2f441-112">For **Windows** clusters: Use a script action tooconfigure hello value during cluster creation.</span></span> <span data-ttu-id="2f441-113">Aby uzyskać więcej informacji, zobacz [tworzenie akcji skryptów](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="2f441-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="2f441-114">Aby uzyskać **Linux** klastrów: wartość hello toomodify Ambari Użyj (sieć web lub interfejsu API REST).</span><span class="sxs-lookup"><span data-stu-id="2f441-114">For **Linux** clusters: Use Ambari (web or REST API) toomodify hello value.</span></span> <span data-ttu-id="2f441-115">Aby uzyskać więcej informacji, zobacz [Zarządzanie HDInsight przy użyciu narzędzia Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="2f441-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f441-116">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="2f441-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2f441-117">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="2f441-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="2f441-118">Domyślna konfiguracja</span><span class="sxs-lookup"><span data-stu-id="2f441-118">Default configuration</span></span>

<span data-ttu-id="2f441-119">W przypadku przekroczenia hello następujące wartości domyślne, możesz obniżyć wydajność usługi WebHCat, lub powodować błędy:</span><span class="sxs-lookup"><span data-stu-id="2f441-119">If hello following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="2f441-120">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="2f441-120">Setting</span></span> | <span data-ttu-id="2f441-121">Wyniki działania</span><span class="sxs-lookup"><span data-stu-id="2f441-121">What it does</span></span> | <span data-ttu-id="2f441-122">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="2f441-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f441-123">[yarn.Scheduler.Capacity.Maximum — aplikacje][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="2f441-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="2f441-124">Maksymalna liczba zadań, które mogą być jednocześnie aktywne Hello (oczekiwanie lub uruchomiona)</span><span class="sxs-lookup"><span data-stu-id="2f441-124">hello maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="2f441-125">10 000</span><span class="sxs-lookup"><span data-stu-id="2f441-125">10,000</span></span> |
| <span data-ttu-id="2f441-126">[templeton.EXEC.max procs][max-procs]</span><span class="sxs-lookup"><span data-stu-id="2f441-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="2f441-127">Maksymalna liczba żądań, które mogą być przekazywane jednocześnie Hello</span><span class="sxs-lookup"><span data-stu-id="2f441-127">hello maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="2f441-128">20</span><span class="sxs-lookup"><span data-stu-id="2f441-128">20</span></span> |
| <span data-ttu-id="2f441-129">[mapreduce.jobhistory.max wieku ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="2f441-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="2f441-130">Witaj liczbę dni, które Historia zadania są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="2f441-130">hello number of days that job history are retained</span></span> |<span data-ttu-id="2f441-131">7 dni</span><span class="sxs-lookup"><span data-stu-id="2f441-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="2f441-132">Zbyt wiele żądań</span><span class="sxs-lookup"><span data-stu-id="2f441-132">Too many requests</span></span>

<span data-ttu-id="2f441-133">**Kod stanu HTTP**: 429</span><span class="sxs-lookup"><span data-stu-id="2f441-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="2f441-134">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="2f441-134">Cause</span></span> | <span data-ttu-id="2f441-135">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="2f441-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="2f441-136">Przekroczono hello maksymalną równoczesnych żądań obsłużonych przez WebHCat na minutę (domyślnie 20)</span><span class="sxs-lookup"><span data-stu-id="2f441-136">You have exceeded hello maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="2f441-137">Zmniejsz Twojej tooensure obciążenia, czy nie przesyłać więcej niż hello maksymalną liczbę jednoczesnych żądań lub zwiększ limit równoczesnych żądań hello przez zmodyfikowanie `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="2f441-137">Reduce your workload tooensure that you do not submit more than hello maximum number of concurrent requests or increase hello concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="2f441-138">Aby uzyskać więcej informacji, zobacz [modyfikowanie konfiguracji](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="2f441-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="2f441-139">Serwer jest niedostępny</span><span class="sxs-lookup"><span data-stu-id="2f441-139">Server unavailable</span></span>

<span data-ttu-id="2f441-140">**Kod stanu HTTP**: 503</span><span class="sxs-lookup"><span data-stu-id="2f441-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="2f441-141">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="2f441-141">Cause</span></span> | <span data-ttu-id="2f441-142">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="2f441-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="2f441-143">Ten kod stanu zazwyczaj występuje w trybie failover między hello podstawowe i pomocnicze HeadNode hello klastra</span><span class="sxs-lookup"><span data-stu-id="2f441-143">This status code usually occurs during failover between hello primary and secondary HeadNode for hello cluster</span></span> |<span data-ttu-id="2f441-144">Poczekaj 2 minuty, a następnie ponów próbę wykonania operacji hello</span><span class="sxs-lookup"><span data-stu-id="2f441-144">Wait two minutes, then retry hello operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="2f441-145">Nieprawidłowe żądanie zawartości: nie można odnaleźć zadania</span><span class="sxs-lookup"><span data-stu-id="2f441-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="2f441-146">**Kod stanu HTTP**: 400</span><span class="sxs-lookup"><span data-stu-id="2f441-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="2f441-147">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="2f441-147">Cause</span></span> | <span data-ttu-id="2f441-148">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="2f441-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="2f441-149">Szczegóły zadania zostały wyczyszczone w historii zadań hello czyszcząca</span><span class="sxs-lookup"><span data-stu-id="2f441-149">Job details have been cleaned up by hello job history cleaner</span></span> |<span data-ttu-id="2f441-150">Witaj domyślnego okresu przechowywania historii zadań wynosi 7 dni.</span><span class="sxs-lookup"><span data-stu-id="2f441-150">hello default retention period for job history is 7 days.</span></span> <span data-ttu-id="2f441-151">Witaj domyślnego okresu przechowywania można zmienić, modyfikując `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="2f441-151">hello default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="2f441-152">Aby uzyskać więcej informacji, zobacz [modyfikowanie konfiguracji](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="2f441-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="2f441-153">Zadanie ukończenia pracy awaryjnej tooa został zatrzymany</span><span class="sxs-lookup"><span data-stu-id="2f441-153">Job has been killed due tooa failover</span></span> |<span data-ttu-id="2f441-154">Spróbuj ponownie przesyłanie zadań do zapasowej tootwo minut</span><span class="sxs-lookup"><span data-stu-id="2f441-154">Retry job submission for up tootwo minutes</span></span> |
| <span data-ttu-id="2f441-155">Nieprawidłowy identyfikator zadania został użyty.</span><span class="sxs-lookup"><span data-stu-id="2f441-155">An Invalid job id was used</span></span> |<span data-ttu-id="2f441-156">Sprawdź, czy identyfikator zadania hello jest prawidłowa</span><span class="sxs-lookup"><span data-stu-id="2f441-156">Check if hello job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="2f441-157">Zły bramy</span><span class="sxs-lookup"><span data-stu-id="2f441-157">Bad gateway</span></span>

<span data-ttu-id="2f441-158">**Kod stanu HTTP**: 502</span><span class="sxs-lookup"><span data-stu-id="2f441-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="2f441-159">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="2f441-159">Cause</span></span> | <span data-ttu-id="2f441-160">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="2f441-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="2f441-161">Wewnętrzny wyrzucanie elementów bezużytecznych ma miejsce w hello procesu usługi WebHCat</span><span class="sxs-lookup"><span data-stu-id="2f441-161">Internal garbage collection is occurring within hello WebHCat process</span></span> |<span data-ttu-id="2f441-162">Poczekaj, aż odzyskiwanie kolekcji toofinish lub ponowne uruchomienie usługi WebHCat hello</span><span class="sxs-lookup"><span data-stu-id="2f441-162">Wait for garbage collection toofinish or restart hello WebHCat service</span></span> |
| <span data-ttu-id="2f441-163">Upłynął limit czasu oczekiwania na odpowiedź z hello ResourceManager usługi.</span><span class="sxs-lookup"><span data-stu-id="2f441-163">Time out waiting on a response from hello ResourceManager service.</span></span> <span data-ttu-id="2f441-164">Ten błąd może wystąpić, gdy hello liczba aktywnych aplikacji hello skonfigurowany maksymalny (domyślnie 10 000)</span><span class="sxs-lookup"><span data-stu-id="2f441-164">This error can occur when hello number of active applications goes hello configured maximum (default 10,000)</span></span> |<span data-ttu-id="2f441-165">Poczekaj, aż aktualnie uruchomione zadania toocomplete lub zwiększ limit równoczesnych zadań hello modyfikując `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="2f441-165">Wait for currently running jobs toocomplete or increase hello concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="2f441-166">Aby uzyskać więcej informacji, zobacz hello [modyfikowanie konfiguracji](#modifying-configuration) sekcji.</span><span class="sxs-lookup"><span data-stu-id="2f441-166">For more information, see hello [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="2f441-167">Próba tooretrieve wszystkie zadania za pomocą hello [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) wywołania podczas `Fields` ustawiono zbyt`*`</span><span class="sxs-lookup"><span data-stu-id="2f441-167">Attempting tooretrieve all jobs through hello [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set too`*`</span></span> |<span data-ttu-id="2f441-168">Nie pobierają *wszystkie* szczegóły zadania.</span><span class="sxs-lookup"><span data-stu-id="2f441-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="2f441-169">Zamiast tego użyj `jobid` tooretrieve szczegóły zadania tylko większe niektórych identyfikator zadania. Nie używaj`Fields`</span><span class="sxs-lookup"><span data-stu-id="2f441-169">Instead use `jobid` tooretrieve details for jobs only greater than certain job id. Or, do not use `Fields`</span></span> |
| <span data-ttu-id="2f441-170">Witaj usługi WebHCat nie działa w trybie failover HeadNode</span><span class="sxs-lookup"><span data-stu-id="2f441-170">hello WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="2f441-171">Poczekaj dwóch minut i ponów próbę wykonania operacji hello</span><span class="sxs-lookup"><span data-stu-id="2f441-171">Wait for two minutes and retry hello operation</span></span> |
| <span data-ttu-id="2f441-172">Istnieje więcej niż 500 oczekujące zadania przesłane za pośrednictwem usługi WebHCat</span><span class="sxs-lookup"><span data-stu-id="2f441-172">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="2f441-173">Poczekaj, aż obecnie oczekujące zadania zostały ukończone przed przesłaniem więcej zadań</span><span class="sxs-lookup"><span data-stu-id="2f441-173">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
