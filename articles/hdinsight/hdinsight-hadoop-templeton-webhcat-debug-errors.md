---
title: "Zrozumienia i rozwiązania błędów WebHCat w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak do około typowe błędy zwrócone przez WebHCat w usłudze HDInsight oraz sposobów ich rozwiązywania."
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
ms.openlocfilehash: 6d8162e0d64ec9fc42690392b7c822593c0c2767
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-resolve-errors-received-from-webhcat-on-hdinsight"></a><span data-ttu-id="d1a59-103">Zrozumienia i rozwiązania błędów, odbierane z usługi WebHCat w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="d1a59-103">Understand and resolve errors received from WebHCat on HDInsight</span></span>

<span data-ttu-id="d1a59-104">Więcej informacji na temat błędów podczas przy użyciu usługi WebHCat w usłudze HDInsight i sposobu ich rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d1a59-104">Learn about errors received when using WebHCat with HDInsight, and how to resolve them.</span></span> <span data-ttu-id="d1a59-105">WebHCat jest używana wewnętrznie przez klienta narzędzi, takich jak Azure PowerShell i narzędzi Data Lake Tools dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1a59-105">WebHCat is used internally by client-side tools such as Azure PowerShell and the Data Lake Tools for Visual Studio.</span></span>

## <a name="what-is-webhcat"></a><span data-ttu-id="d1a59-106">Co to jest WebHCat</span><span class="sxs-lookup"><span data-stu-id="d1a59-106">What is WebHCat</span></span>

<span data-ttu-id="d1a59-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) to interfejs API REST dla [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), tabeli i magazynu warstwa zarządzania dla platformy Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d1a59-107">[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) is a REST API for [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), a table, and storage management layer for Hadoop.</span></span> <span data-ttu-id="d1a59-108">WebHCat jest domyślnie włączone w klastrach HDInsight i jest używany przez różnych narzędzi do przesyłania zadań, Pobierz stan zadania, itp., bez potrzeby logowania do klastra.</span><span class="sxs-lookup"><span data-stu-id="d1a59-108">WebHCat is enabled by default on HDInsight clusters, and is used by various tools to submit jobs, get job status, etc. without logging in to the cluster.</span></span>

## <a name="modifying-configuration"></a><span data-ttu-id="d1a59-109">Modyfikowanie konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d1a59-109">Modifying configuration</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1a59-110">Występuje kilka błędów wymienione w niniejszym dokumencie, ponieważ została przekroczona maksymalna skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="d1a59-110">Several of the errors listed in this document occur because a configured maximum has been exceeded.</span></span> <span data-ttu-id="d1a59-111">Podczas kroku rozpoznawania uwagi, można zmienić wartości, należy użyć jednej z poniższych Aby dokonać zmiany:</span><span class="sxs-lookup"><span data-stu-id="d1a59-111">When the resolution step mentions that you can change a value, you must use one of the following to perform the change:</span></span>

* <span data-ttu-id="d1a59-112">Dla **Windows** klastrów: Aby skonfigurować wartość podczas tworzenia klastra, użyj akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="d1a59-112">For **Windows** clusters: Use a script action to configure the value during cluster creation.</span></span> <span data-ttu-id="d1a59-113">Aby uzyskać więcej informacji, zobacz [tworzenie akcji skryptów](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="d1a59-113">For more information, see [Develop script actions](hdinsight-hadoop-script-actions.md).</span></span>

* <span data-ttu-id="d1a59-114">Dla **Linux** klastrów: Użyj Ambari (sieć web lub interfejsu API REST), aby zmodyfikować wartość.</span><span class="sxs-lookup"><span data-stu-id="d1a59-114">For **Linux** clusters: Use Ambari (web or REST API) to modify the value.</span></span> <span data-ttu-id="d1a59-115">Aby uzyskać więcej informacji, zobacz [Zarządzanie HDInsight przy użyciu narzędzia Ambari](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="d1a59-115">For more information, see [Manage HDInsight using Ambari](hdinsight-hadoop-manage-ambari.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1a59-116">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="d1a59-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d1a59-117">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="d1a59-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="default-configuration"></a><span data-ttu-id="d1a59-118">Domyślna konfiguracja</span><span class="sxs-lookup"><span data-stu-id="d1a59-118">Default configuration</span></span>

<span data-ttu-id="d1a59-119">W przypadku przekroczenia następujące wartości domyślne, możesz obniżyć wydajność usługi WebHCat lub powodować błędy:</span><span class="sxs-lookup"><span data-stu-id="d1a59-119">If the following default values are exceeded, it can degrade WebHCat performance or cause errors:</span></span>

| <span data-ttu-id="d1a59-120">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="d1a59-120">Setting</span></span> | <span data-ttu-id="d1a59-121">Wyniki działania</span><span class="sxs-lookup"><span data-stu-id="d1a59-121">What it does</span></span> | <span data-ttu-id="d1a59-122">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="d1a59-122">Default value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d1a59-123">[yarn.Scheduler.Capacity.Maximum — aplikacje][maximum-applications]</span><span class="sxs-lookup"><span data-stu-id="d1a59-123">[yarn.scheduler.capacity.maximum-applications][maximum-applications]</span></span> |<span data-ttu-id="d1a59-124">Maksymalna liczba zadań, które mogą być jednocześnie aktywne (oczekiwanie lub uruchomiona)</span><span class="sxs-lookup"><span data-stu-id="d1a59-124">The maximum number of jobs that can be active concurrently (pending or running)</span></span> |<span data-ttu-id="d1a59-125">10 000</span><span class="sxs-lookup"><span data-stu-id="d1a59-125">10,000</span></span> |
| <span data-ttu-id="d1a59-126">[templeton.EXEC.max procs][max-procs]</span><span class="sxs-lookup"><span data-stu-id="d1a59-126">[templeton.exec.max-procs][max-procs]</span></span> |<span data-ttu-id="d1a59-127">Maksymalna liczba żądań, które mogą być przekazywane jednocześnie</span><span class="sxs-lookup"><span data-stu-id="d1a59-127">The maximum number of requests that can be served concurrently</span></span> |<span data-ttu-id="d1a59-128">20</span><span class="sxs-lookup"><span data-stu-id="d1a59-128">20</span></span> |
| <span data-ttu-id="d1a59-129">[mapreduce.jobhistory.max wieku ms][max-age-ms]</span><span class="sxs-lookup"><span data-stu-id="d1a59-129">[mapreduce.jobhistory.max-age-ms][max-age-ms]</span></span> |<span data-ttu-id="d1a59-130">Liczba dni, które Historia zadania są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="d1a59-130">The number of days that job history are retained</span></span> |<span data-ttu-id="d1a59-131">7 dni</span><span class="sxs-lookup"><span data-stu-id="d1a59-131">7 days</span></span> |

## <a name="too-many-requests"></a><span data-ttu-id="d1a59-132">Zbyt wiele żądań</span><span class="sxs-lookup"><span data-stu-id="d1a59-132">Too many requests</span></span>

<span data-ttu-id="d1a59-133">**Kod stanu HTTP**: 429</span><span class="sxs-lookup"><span data-stu-id="d1a59-133">**HTTP Status code**: 429</span></span>

| <span data-ttu-id="d1a59-134">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="d1a59-134">Cause</span></span> | <span data-ttu-id="d1a59-135">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="d1a59-135">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="d1a59-136">Przekroczono maksymalną równoczesnych żądań obsłużonych przez WebHCat na minutę (domyślnie 20)</span><span class="sxs-lookup"><span data-stu-id="d1a59-136">You have exceeded the maximum concurrent requests served by WebHCat per minute (default 20)</span></span> |<span data-ttu-id="d1a59-137">Zmniejsz obciążenie w taki sposób, aby upewnić się, że nie przesłać więcej niż maksymalna liczba jednoczesnych żądań lub zwiększ limit równoczesnych żądań przez zmodyfikowanie `templeton.exec.max-procs`.</span><span class="sxs-lookup"><span data-stu-id="d1a59-137">Reduce your workload to ensure that you do not submit more than the maximum number of concurrent requests or increase the concurrent request limit by modifying `templeton.exec.max-procs`.</span></span> <span data-ttu-id="d1a59-138">Aby uzyskać więcej informacji, zobacz [modyfikowanie konfiguracji](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="d1a59-138">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |

## <a name="server-unavailable"></a><span data-ttu-id="d1a59-139">Serwer jest niedostępny</span><span class="sxs-lookup"><span data-stu-id="d1a59-139">Server unavailable</span></span>

<span data-ttu-id="d1a59-140">**Kod stanu HTTP**: 503</span><span class="sxs-lookup"><span data-stu-id="d1a59-140">**HTTP Status code**: 503</span></span>

| <span data-ttu-id="d1a59-141">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="d1a59-141">Cause</span></span> | <span data-ttu-id="d1a59-142">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="d1a59-142">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="d1a59-143">Ten kod stanu zazwyczaj występuje w trybie failover między HeadNode podstawowe i pomocnicze dla klastra</span><span class="sxs-lookup"><span data-stu-id="d1a59-143">This status code usually occurs during failover between the primary and secondary HeadNode for the cluster</span></span> |<span data-ttu-id="d1a59-144">Poczekaj 2 minuty, a następnie spróbuj ponownie wykonać operację</span><span class="sxs-lookup"><span data-stu-id="d1a59-144">Wait two minutes, then retry the operation</span></span> |

## <a name="bad-request-content-could-not-find-job"></a><span data-ttu-id="d1a59-145">Nieprawidłowe żądanie zawartości: nie można odnaleźć zadania</span><span class="sxs-lookup"><span data-stu-id="d1a59-145">Bad request Content: Could not find job</span></span>

<span data-ttu-id="d1a59-146">**Kod stanu HTTP**: 400</span><span class="sxs-lookup"><span data-stu-id="d1a59-146">**HTTP Status code**: 400</span></span>

| <span data-ttu-id="d1a59-147">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="d1a59-147">Cause</span></span> | <span data-ttu-id="d1a59-148">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="d1a59-148">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="d1a59-149">Szczegóły zadania zostały wyczyszczone w historii zadań czyszcząca</span><span class="sxs-lookup"><span data-stu-id="d1a59-149">Job details have been cleaned up by the job history cleaner</span></span> |<span data-ttu-id="d1a59-150">Domyślny okres przechowywania historii zadań wynosi 7 dni.</span><span class="sxs-lookup"><span data-stu-id="d1a59-150">The default retention period for job history is 7 days.</span></span> <span data-ttu-id="d1a59-151">Domyślny okres przechowywania można zmienić, modyfikując `mapreduce.jobhistory.max-age-ms`.</span><span class="sxs-lookup"><span data-stu-id="d1a59-151">The default retention period can be changed by modifying `mapreduce.jobhistory.max-age-ms`.</span></span> <span data-ttu-id="d1a59-152">Aby uzyskać więcej informacji, zobacz [modyfikowanie konfiguracji](#modifying-configuration)</span><span class="sxs-lookup"><span data-stu-id="d1a59-152">For more information, see [Modifying configuration](#modifying-configuration)</span></span> |
| <span data-ttu-id="d1a59-153">Zadania został zamknięty z powodu pracy awaryjnej</span><span class="sxs-lookup"><span data-stu-id="d1a59-153">Job has been killed due to a failover</span></span> |<span data-ttu-id="d1a59-154">Spróbuj ponownie przesyłanie zadań do dwóch minut</span><span class="sxs-lookup"><span data-stu-id="d1a59-154">Retry job submission for up to two minutes</span></span> |
| <span data-ttu-id="d1a59-155">Nieprawidłowy identyfikator zadania został użyty.</span><span class="sxs-lookup"><span data-stu-id="d1a59-155">An Invalid job id was used</span></span> |<span data-ttu-id="d1a59-156">Sprawdź, czy identyfikator zadania jest prawidłowa</span><span class="sxs-lookup"><span data-stu-id="d1a59-156">Check if the job id is correct</span></span> |

## <a name="bad-gateway"></a><span data-ttu-id="d1a59-157">Zły bramy</span><span class="sxs-lookup"><span data-stu-id="d1a59-157">Bad gateway</span></span>

<span data-ttu-id="d1a59-158">**Kod stanu HTTP**: 502</span><span class="sxs-lookup"><span data-stu-id="d1a59-158">**HTTP Status code**: 502</span></span>

| <span data-ttu-id="d1a59-159">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="d1a59-159">Cause</span></span> | <span data-ttu-id="d1a59-160">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="d1a59-160">Resolution</span></span> |
| --- | --- |
| <span data-ttu-id="d1a59-161">Wewnętrzny wyrzucanie elementów bezużytecznych jest wykonywana w ramach procesu usługi WebHCat</span><span class="sxs-lookup"><span data-stu-id="d1a59-161">Internal garbage collection is occurring within the WebHCat process</span></span> |<span data-ttu-id="d1a59-162">Poczekaj na wyrzucanie elementów bezużytecznych Zakończ lub ponownego uruchomienia usługi WebHCat</span><span class="sxs-lookup"><span data-stu-id="d1a59-162">Wait for garbage collection to finish or restart the WebHCat service</span></span> |
| <span data-ttu-id="d1a59-163">Upłynął limit czasu oczekiwania na odpowiedź z usługi ResourceManager.</span><span class="sxs-lookup"><span data-stu-id="d1a59-163">Time out waiting on a response from the ResourceManager service.</span></span> <span data-ttu-id="d1a59-164">Ten błąd może wystąpić, gdy liczba aktywnych aplikacji skonfigurowane maksimum (domyślnie 10 000)</span><span class="sxs-lookup"><span data-stu-id="d1a59-164">This error can occur when the number of active applications goes the configured maximum (default 10,000)</span></span> |<span data-ttu-id="d1a59-165">Poczekaj, aż aktualnie uruchomionych zadań do wykonania lub zwiększ limit równoczesnych zadań, modyfikując `yarn.scheduler.capacity.maximum-applications`.</span><span class="sxs-lookup"><span data-stu-id="d1a59-165">Wait for currently running jobs to complete or increase the concurrent job limit by modifying `yarn.scheduler.capacity.maximum-applications`.</span></span> <span data-ttu-id="d1a59-166">Aby uzyskać więcej informacji, zobacz [modyfikowanie konfiguracji](#modifying-configuration) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d1a59-166">For more information, see the [Modifying configuration](#modifying-configuration) section.</span></span> |
| <span data-ttu-id="d1a59-167">Podjęto próbę pobrania wszystkich zadań za pomocą [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) wywołania podczas `Fields` ma ustawioną wartość`*`</span><span class="sxs-lookup"><span data-stu-id="d1a59-167">Attempting to retrieve all jobs through the [GET /jobs](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference+Jobs) call while `Fields` is set to `*`</span></span> |<span data-ttu-id="d1a59-168">Nie pobierają *wszystkie* szczegóły zadania.</span><span class="sxs-lookup"><span data-stu-id="d1a59-168">Do not retrieve *all* job details.</span></span> <span data-ttu-id="d1a59-169">Zamiast tego użyj `jobid` można pobrać szczegółów zadań większe tylko niektórych identyfikator zadania.</span><span class="sxs-lookup"><span data-stu-id="d1a59-169">Instead use `jobid` to retrieve details for jobs only greater than certain job id.</span></span> <span data-ttu-id="d1a59-170">Nie używaj`Fields`</span><span class="sxs-lookup"><span data-stu-id="d1a59-170">Or, do not use `Fields`</span></span> |
| <span data-ttu-id="d1a59-171">Usługi WebHCat nie działa w trybie failover HeadNode</span><span class="sxs-lookup"><span data-stu-id="d1a59-171">The WebHCat service is down during HeadNode failover</span></span> |<span data-ttu-id="d1a59-172">Poczekaj 2 minuty, a następnie spróbuj ponownie wykonać operację</span><span class="sxs-lookup"><span data-stu-id="d1a59-172">Wait for two minutes and retry the operation</span></span> |
| <span data-ttu-id="d1a59-173">Istnieje więcej niż 500 oczekujące zadania przesłane za pośrednictwem usługi WebHCat</span><span class="sxs-lookup"><span data-stu-id="d1a59-173">There are more than 500 pending jobs submitted through WebHCat</span></span> |<span data-ttu-id="d1a59-174">Poczekaj, aż obecnie oczekujące zadania zostały ukończone przed przesłaniem więcej zadań</span><span class="sxs-lookup"><span data-stu-id="d1a59-174">Wait until currently pending jobs have completed before submitting more jobs</span></span> |

[maximum-applications]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.1.3/bk_system-admin-guide/content/setting_application_limits.html
[max-procs]: https://hive.apache.org/javadocs/hcat-r0.5.0/configuration.html
[max-age-ms]: http://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.0.6.0/ds_Hadoop/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml
