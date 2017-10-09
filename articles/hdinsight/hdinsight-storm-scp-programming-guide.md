---
title: "Podręcznik programowania aaaSCP.NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse SCP.NET toocreate. Na podstawie NET topologii Storm do za pomocą Storm w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: raviperi
manager: jhubbard
editor: cgronlun
ms.assetid: 34192ed0-b1d1-4cf7-a3d4-5466301cf307
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/16/2016
ms.author: raviperi
ms.openlocfilehash: a57f4217b07e0e82a3f36650308695fbb45d9128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="c22b8-103">Podręcznik programowania punkt połączenia usługi</span><span class="sxs-lookup"><span data-stu-id="c22b8-103">SCP programming guide</span></span>
<span data-ttu-id="c22b8-104">Punkt połączenia usługi jest czasu rzeczywistego toobuild platformy, niezawodnych, spójne i wysoką wydajność przetwarzania danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c22b8-104">SCP is a platform toobuild real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="c22b8-105">Jest ona wbudowana nad [Apache Storm](http://storm.incubator.apache.org/) — systemu projektowania Wspólnot hello OSS przetwarzania strumienia.</span><span class="sxs-lookup"><span data-stu-id="c22b8-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by hello OSS communities.</span></span> <span data-ttu-id="c22b8-106">STORM jest zaprojektowana przez Nathan Marz i otwórz kwerendą źródłową Twitter.</span><span class="sxs-lookup"><span data-stu-id="c22b8-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="c22b8-107">Jest przeprowadzana z zastosowaniem [Apache ZooKeeper](http://zookeeper.apache.org/), Apache innego projektu tooenable wysoce niezawodne koordynacji rozproszonego oraz zarządzanie stanem.</span><span class="sxs-lookup"><span data-stu-id="c22b8-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project tooenable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="c22b8-108">Nie tylko projektu hello SCP systemie Storm w systemie Windows, ale również projekt hello dodany rozszerzenia i dostosowania dla ekosystemu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="c22b8-108">Not only hello SCP project ported Storm on Windows but also hello project added extensions and customization for hello Windows ecosystem.</span></span> <span data-ttu-id="c22b8-109">rozszerzenia Hello to środowisko dewelopera .NET i bibliotek, hello modyfikacje obejmują wdrażania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c22b8-109">hello extensions include .NET developer experience, and libraries, hello customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="c22b8-110">Witaj rozszerzenie i dostosowanie odbywa się w taki sposób, że nie występują toofork hello OSS projektów i firma Microsoft może korzystać z ekosystemami pochodnej, rozszerzający Storm.</span><span class="sxs-lookup"><span data-stu-id="c22b8-110">hello extension and customization is done in such a way that we do not need toofork hello OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="c22b8-111">Przetwarzanie modelu</span><span class="sxs-lookup"><span data-stu-id="c22b8-111">Processing model</span></span>
<span data-ttu-id="c22b8-112">dane Hello w punkt połączenia usługi jest modelowana jako ciągłe strumienie spójnych kolekcji.</span><span class="sxs-lookup"><span data-stu-id="c22b8-112">hello data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="c22b8-113">Zwykle krotek hello przepływać do niektórych kolejki najpierw, a następnie pobrana i przekształcenia przez hostowaną wewnątrz topologii Storm logiki biznesowej, koniec hello danych wyjściowych może być przekazywane w potoku jako system tooanother SCP krotek lub być zatwierdzone toostores rozproszonego systemu plików, takich jak lub bazy danych, takich jak SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c22b8-113">Typically hello tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally hello output could be piped as tuples tooanother SCP system, or be committed toostores like distributed file system or databases like SQL Server.</span></span>

![Diagram kolejki zasilania tooprocessing danych, które źródeł danych magazynu danych](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="c22b8-115">Topologia aplikacji Storm, definiuje Graf obliczeń.</span><span class="sxs-lookup"><span data-stu-id="c22b8-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="c22b8-116">Każdy węzeł w topologii zawiera logikę przetwarzania i łącza między węzłami Oznaczanie przepływu danych.</span><span class="sxs-lookup"><span data-stu-id="c22b8-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="c22b8-117">dane wejściowe tooinject węzłów Hello w topologii hello są nazywane elementach Spout, które mogą być używane toosequence hello danych.</span><span class="sxs-lookup"><span data-stu-id="c22b8-117">hello nodes tooinject input data into hello topology are called Spouts, which can be used toosequence hello data.</span></span> <span data-ttu-id="c22b8-118">Witaj danych wejściowych może znajdować się w plików dzienników, transakcyjne bazy danych licznika wydajności systemu itp. hello węzłów z obu przepływów danych wejściowych i wyjściowych są nazywane elementów Bolt, które hello filtrowania rzeczywiste dane i wybór oraz agregacji.</span><span class="sxs-lookup"><span data-stu-id="c22b8-118">hello input data could reside in file logs, transactional database, system performance counter etc. hello nodes with both input and output data flows are called Bolts, which do hello actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="c22b8-119">Punkt połączenia usługi obsługuje starań w najmniej jednokrotne, a dokładnie — raz przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="c22b8-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="c22b8-120">W przypadku przesyłania strumieniowego przetwarzania aplikacji rozproszonej różne błędy może się tak zdarzyć podczas przetwarzania danych, takich jak awaria sieci, błąd maszyny lub błąd kodu użytkownika itd. Przetwarzanie w najmniej jednokrotne zapewnia wszystkie dane będą przetwarzane co najmniej raz przez powtarzanie automatycznie hello tych samych danych w przypadku błędu.</span><span class="sxs-lookup"><span data-stu-id="c22b8-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically hello same data when error happens.</span></span> <span data-ttu-id="c22b8-121">Przetwarzanie w najmniej jednokrotne jest proste i niezawodne i odpowiada także w wielu aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="c22b8-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="c22b8-122">Jednak gdy aplikacji hello wymaga dokładnego zliczanie, na przykład w najmniej jednokrotne przetwarzania jest niewystarczająca ponieważ hello tych samych danych może potencjalnie być odtworzone w topologii aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="c22b8-122">However, when hello application requires exact counting, for example, at-least-once processing is insufficient since hello same data could potentially be played in hello application topology.</span></span> <span data-ttu-id="c22b8-123">W takim przypadku, dokładnie-po zaprojektowano przetwarzania toomake się, że wynik hello jest poprawna, nawet wtedy, gdy hello danych mogą być odtwarzany i przetwarzane wiele razy.</span><span class="sxs-lookup"><span data-stu-id="c22b8-123">In that case, exactly-once processing is designed toomake sure hello result is correct even when hello data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="c22b8-124">Punkt połączenia usługi umożliwia aplikacji procesu danych czasu rzeczywistego .NET deweloperzy toodevelop podczas hello wykorzystać maszyny wirtualnej Java (JVM) na podstawie Storm w obszarze okładce hello.</span><span class="sxs-lookup"><span data-stu-id="c22b8-124">SCP enables .NET developers toodevelop real time data process applications while leverage hello Java Virtual Machine (JVM) based Storm under hello cover.</span></span> <span data-ttu-id="c22b8-125">Witaj .NET i JVM komunikują się za pośrednictwem lokalnego gniazda TCP.</span><span class="sxs-lookup"><span data-stu-id="c22b8-125">hello .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="c22b8-126">Zasadniczo każdego Spout/Bolt jest para procesu .net/Java, gdzie hello logikę użytkownika działa w procesie .net jako dodatek.</span><span class="sxs-lookup"><span data-stu-id="c22b8-126">Basically each Spout/Bolt is a .Net/Java process pair, where hello user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="c22b8-127">toobuild danych przetwarzania aplikacji na punkt połączenia usługi, kilka czynności:</span><span class="sxs-lookup"><span data-stu-id="c22b8-127">toobuild a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="c22b8-128">Projektowania i implementacji hello elementach Spout toopull danych z kolejki.</span><span class="sxs-lookup"><span data-stu-id="c22b8-128">Design and implement hello Spouts toopull in data from queue.</span></span>
* <span data-ttu-id="c22b8-129">Projektowanie i implementowanie tooprocess elementów Bolt hello danych wejściowych i Zapisz dane są przechowywane tooexternal, takie jak bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c22b8-129">Design and implement Bolts tooprocess hello input data, and save data tooexternal stores such as Database.</span></span>
* <span data-ttu-id="c22b8-130">Projektowanie topologii hello, przesyłania, a następnie uruchom hello topologii.</span><span class="sxs-lookup"><span data-stu-id="c22b8-130">Design hello topology, then submit and run hello topology.</span></span> <span data-ttu-id="c22b8-131">Witaj topologii definiuje wierzchołki i hello dane między hello wierzchołków.</span><span class="sxs-lookup"><span data-stu-id="c22b8-131">hello topology defines vertexes and hello data flows between hello vertexes.</span></span> <span data-ttu-id="c22b8-132">Punkt połączenia usługi otrzymuje hello topologii specyfikacji i wdrożyć ją na klaster Storm, w którym każdy wierzchołek jest uruchamiany w jednym węźle logiczne.</span><span class="sxs-lookup"><span data-stu-id="c22b8-132">SCP will take hello topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="c22b8-133">Hello trybu failover i skalowanie będzie można wybrać ofertę z przez harmonogram zadań hello Storm.</span><span class="sxs-lookup"><span data-stu-id="c22b8-133">hello failover and scaling will be taken care of by hello Storm task scheduler.</span></span>

<span data-ttu-id="c22b8-134">Ten dokument będzie używać niektórych toowalk proste przykłady za pośrednictwem jak toobuild przetwarzania danych aplikacji przy użyciu połączenia usługi.</span><span class="sxs-lookup"><span data-stu-id="c22b8-134">This document will use some simple examples toowalk through how toobuild data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="c22b8-135">Interfejs wtyczki punkt połączenia usługi</span><span class="sxs-lookup"><span data-stu-id="c22b8-135">SCP Plugin Interface</span></span>
<span data-ttu-id="c22b8-136">Wtyczki punkt połączenia usługi (lub aplikacji) są autonomiczne plików exe, które można jednocześnie uruchomić w programie Visual Studio w fazie programowanie hello i być podłączane do potoku Storm powitania po wdrożeniu w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="c22b8-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during hello development phase, and be plugged into hello Storm pipeline after deployment in production.</span></span> <span data-ttu-id="c22b8-137">Pisanie wtyczki hello punkt połączenia usługi jest po prostu hello taki sam jak zapisywania wszelkich innych standardowych aplikacji systemu Windows konsoli.</span><span class="sxs-lookup"><span data-stu-id="c22b8-137">Writing hello SCP plugin is just hello same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="c22b8-138">Platforma SCP.NET deklaruje niektórych interfejs dla spout/bolt, i kod wtyczki użytkownika hello należy zaimplementować te interfejsy.</span><span class="sxs-lookup"><span data-stu-id="c22b8-138">SCP.NET platform declares some interface for spout/bolt, and hello user plugin code should implement these interfaces.</span></span> <span data-ttu-id="c22b8-139">głównym celem Hello ten projekt jest ten użytkownik hello można skupić się na ich własnych warunki biznesowe logiczne i pozostawienie toobe innych elementów, obsługiwane przez platformę SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="c22b8-139">hello main purpose of this design is that hello user can focus on their own business logics, and leaving other things toobe handled by SCP.NET platform.</span></span>

<span data-ttu-id="c22b8-140">Kod wtyczki użytkownika Hello powinny implementować jeden hello następujących typów interfejsów, zależy od tego, czy topologia hello jest transakcyjna lub nietransakcyjna i określa, czy składnik hello jest spout lub bolt.</span><span class="sxs-lookup"><span data-stu-id="c22b8-140">hello user plugin code should implement one of hello followings interfaces, depends on whether hello topology is transactional or non-transactional, and whether hello component is spout or bolt.</span></span>

* <span data-ttu-id="c22b8-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="c22b8-141">ISCPSpout</span></span>
* <span data-ttu-id="c22b8-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="c22b8-142">ISCPBolt</span></span>
* <span data-ttu-id="c22b8-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="c22b8-143">ISCPTxSpout</span></span>
* <span data-ttu-id="c22b8-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="c22b8-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="c22b8-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="c22b8-145">ISCPPlugin</span></span>
<span data-ttu-id="c22b8-146">ISCPPlugin jest hello wspólny interfejs dla wszystkich rodzajów wtyczek.</span><span class="sxs-lookup"><span data-stu-id="c22b8-146">ISCPPlugin is hello common interface for all kinds of plugins.</span></span> <span data-ttu-id="c22b8-147">Obecnie jest interfejsem zastępczego.</span><span class="sxs-lookup"><span data-stu-id="c22b8-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="c22b8-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="c22b8-148">ISCPSpout</span></span>
<span data-ttu-id="c22b8-149">ISCPSpout jest interfejs hello spout nietransakcyjnej.</span><span class="sxs-lookup"><span data-stu-id="c22b8-149">ISCPSpout is hello interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="c22b8-150">Gdy `NextTuple()` jest nazywany hello C\# jeden lub więcej krotek można emitowanie kodu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c22b8-150">When `NextTuple()` is called, hello C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="c22b8-151">Jeśli nie ma nic tooemit, ta metoda powinna zwrócić bez emitowanie żadnych czynności.</span><span class="sxs-lookup"><span data-stu-id="c22b8-151">If there is nothing tooemit, this method should return without emitting anything.</span></span> <span data-ttu-id="c22b8-152">Należy zauważyć, że `NextTuple()`, `Ack()`, i `Fail()` są wszystkie wywoływane w pętli ścisłej w jednym wątku w języku C\# procesu.</span><span class="sxs-lookup"><span data-stu-id="c22b8-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="c22b8-153">Jeśli nie ma żadnych tooemit krotek, jest uśpienia NextTuple uprzejmy toohave do krótkim czasie (na przykład 10 ms) tak, jak nie toowaste zbyt dużo Procesora.</span><span class="sxs-lookup"><span data-stu-id="c22b8-153">When there are no tuples tooemit, it is courteous toohave NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="c22b8-154">`Ack()`i `Fail()` można wywołać tylko wtedy, gdy mechanizmu potwierdzenia jest włączone w specyfikacji pliku.</span><span class="sxs-lookup"><span data-stu-id="c22b8-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="c22b8-155">Witaj `seqId` jest używane tooidentify spójnej kolekcji hello prześledzone lub nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="c22b8-155">hello `seqId` is used tooidentify hello tuple which is acked or failed.</span></span> <span data-ttu-id="c22b8-156">Dlatego po włączeniu potwierdzenia w topologii nietransakcyjnej powitania po emitowanie funkcji powinny być używane w Spout:</span><span class="sxs-lookup"><span data-stu-id="c22b8-156">So if ack is enabled in non-transactional topology, hello following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="c22b8-157">Jeśli potwierdzenie nie jest obsługiwany w topologii nietransakcyjnej, hello `Ack()` i `Fail()` może pozostać puste funkcji.</span><span class="sxs-lookup"><span data-stu-id="c22b8-157">If ack is not supported in non-transactional topology, hello `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="c22b8-158">Witaj `parms` parametry wejściowe w te funkcje są po prostu pusty słownik, są one zarezerwowane do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="c22b8-158">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="c22b8-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="c22b8-159">ISCPBolt</span></span>
<span data-ttu-id="c22b8-160">ISCPBolt jest interfejs hello bolt nietransakcyjnej.</span><span class="sxs-lookup"><span data-stu-id="c22b8-160">ISCPBolt is hello interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="c22b8-161">Po udostępnieniu nowej krotki hello `Execute()` funkcji zostanie wywołana tooprocess go.</span><span class="sxs-lookup"><span data-stu-id="c22b8-161">When new tuple is available, hello `Execute()` function will be called tooprocess it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="c22b8-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="c22b8-162">ISCPTxSpout</span></span>
<span data-ttu-id="c22b8-163">ISCPTxSpout jest interfejs hello spout transakcyjnych.</span><span class="sxs-lookup"><span data-stu-id="c22b8-163">ISCPTxSpout is hello interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="c22b8-164">Podobnie jak ich nietransakcyjnej zaradczych strony `NextTx()`, `Ack()`, i `Fail()` są wszystkie wywoływane w pętli ścisłej w jednym wątku w języku C\# procesu.</span><span class="sxs-lookup"><span data-stu-id="c22b8-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="c22b8-165">Jeśli nie ma żadnych tooemit danych, jest uprzejmy toohave `NextTx` uśpienia przez krótki czas (10 ms), nie toowaste zbyt dużo Procesora.</span><span class="sxs-lookup"><span data-stu-id="c22b8-165">When there are no data tooemit, it is courteous toohave `NextTx` sleep for a short amount of time (10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="c22b8-166">`NextTx()`jest nazywany toostart nowej transakcji, hello parametru out `seqId` jest używane tooidentify hello transakcję, która jest również używana w `Ack()` i `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="c22b8-166">`NextTx()` is called toostart a new transaction, hello out parameter `seqId` is used tooidentify hello transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="c22b8-167">W `NextTx()`, użytkownik może emitować po stronie tooJava danych.</span><span class="sxs-lookup"><span data-stu-id="c22b8-167">In `NextTx()`, user can emit data tooJava side.</span></span> <span data-ttu-id="c22b8-168">Witaj danych będą przechowywane w dozorcy toosupport powtarzania.</span><span class="sxs-lookup"><span data-stu-id="c22b8-168">hello data will be stored in ZooKeeper toosupport replay.</span></span> <span data-ttu-id="c22b8-169">Ponieważ hello pojemność dozorcy jest bardzo ograniczona, użytkownika powinien tylko Emituj metadane, nie zbiorczego danych w spout transakcyjnych.</span><span class="sxs-lookup"><span data-stu-id="c22b8-169">Because hello capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="c22b8-170">STORM będzie odtwarzana w transakcji automatycznie w przypadku niepowodzenia to `Fail()` nie powinna być wywoływana w przypadku normalnych.</span><span class="sxs-lookup"><span data-stu-id="c22b8-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="c22b8-171">Ale jeśli punkt połączenia usługi można sprawdzić metadanych hello emitowane przez transakcyjne spout, może wywołać `Fail()` Jeśli hello metadanych jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="c22b8-171">But if SCP can check hello metadata emitted by transactional spout, it can call `Fail()` when hello metadata is invalid.</span></span>

<span data-ttu-id="c22b8-172">Witaj `parms` parametry wejściowe w te funkcje są po prostu pusty słownik, są one zarezerwowane do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="c22b8-172">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="c22b8-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="c22b8-173">ISCPBatchBolt</span></span>
<span data-ttu-id="c22b8-174">ISCPBatchBolt jest interfejsem powitania dla transakcyjnego bolt.</span><span class="sxs-lookup"><span data-stu-id="c22b8-174">ISCPBatchBolt is hello interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="c22b8-175">`Execute()`jest wywoływana po nowej krotki otrzymywanych hello bolt.</span><span class="sxs-lookup"><span data-stu-id="c22b8-175">`Execute()` is called when there is new tuple arriving at hello bolt.</span></span> <span data-ttu-id="c22b8-176">`FinishBatch()`jest wywoływana po zakończeniu tej transakcji.</span><span class="sxs-lookup"><span data-stu-id="c22b8-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="c22b8-177">Witaj `parms` parametru wejściowego jest zarezerwowany do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="c22b8-177">hello `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="c22b8-178">Topologia transakcyjne jest ważne pojęcia — `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="c22b8-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="c22b8-179">Składa się z dwóch pól `TxId` i `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="c22b8-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="c22b8-180">`TxId`jest używana tooidentify określonej transakcji, a dla danej transakcji, może mieć wielu prób transakcji hello kończy się niepowodzeniem i jest odtwarzany.</span><span class="sxs-lookup"><span data-stu-id="c22b8-180">`TxId` is used tooidentify a specific transaction, and for a given transaction, there may be multiple attempt if hello transaction fails and is replayed.</span></span> <span data-ttu-id="c22b8-181">SCP.NET nowych będzie inny ISCPBatchBolt obiektu tooprocess każdego `StormTxAttempt`, po prostu jak czego Storm w języku Java po stronie.</span><span class="sxs-lookup"><span data-stu-id="c22b8-181">SCP.NET will new a different ISCPBatchBolt object tooprocess each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="c22b8-182">Celem Hello ten projekt jest toosupport przetwarzania transakcji równoległych.</span><span class="sxs-lookup"><span data-stu-id="c22b8-182">hello purpose of this design is toosupport parallel transactions processing.</span></span> <span data-ttu-id="c22b8-183">Użytkownika należy go przechowywać w uwadze który jeśli próba transakcji zostało zakończone, odpowiedni obiekt ISCPBatchBolt hello zostaną zniszczone i w ramach odzyskiwania pamięci.</span><span class="sxs-lookup"><span data-stu-id="c22b8-183">User should keep it in mind that if transaction attempt is finished, hello corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="c22b8-184">Model obiektu</span><span class="sxs-lookup"><span data-stu-id="c22b8-184">Object Model</span></span>
<span data-ttu-id="c22b8-185">SCP.NET udostępnia prosty zestaw obiektów kluczy dla deweloperów tooprogram z.</span><span class="sxs-lookup"><span data-stu-id="c22b8-185">SCP.NET also provides a simple set of key objects for developers tooprogram with.</span></span> <span data-ttu-id="c22b8-186">Są one **kontekstu**, **stan klientów**, i **SCPRuntime**.</span><span class="sxs-lookup"><span data-stu-id="c22b8-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="c22b8-187">Będą one omówione w hello pozostałej części tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="c22b8-187">They will be discussed in hello rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="c22b8-188">Kontekst</span><span class="sxs-lookup"><span data-stu-id="c22b8-188">Context</span></span>
<span data-ttu-id="c22b8-189">Kontekst udostępnia działającej aplikacji toohello środowiska.</span><span class="sxs-lookup"><span data-stu-id="c22b8-189">Context provides a running environment toohello application.</span></span> <span data-ttu-id="c22b8-190">Każde wystąpienie ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) ma odpowiednie wystąpienia kontekstu.</span><span class="sxs-lookup"><span data-stu-id="c22b8-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="c22b8-191">Hello funkcje udostępniane przez kontekst można podzielić na dwie części: statycznej części hello (1), który jest dostępny w hello całego C\# przetworzyć strony dynamicznej hello (2), który jest dostępny tylko dla określonego wystąpienia kontekstu hello.</span><span class="sxs-lookup"><span data-stu-id="c22b8-191">hello functionality provided by Context can be divided into two parts: (1) hello static part which is available in hello whole C\# process, (2) hello dynamic part which is only available for hello specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="c22b8-192">Statycznej części</span><span class="sxs-lookup"><span data-stu-id="c22b8-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="c22b8-193">`Logger`podano w celu dziennika.</span><span class="sxs-lookup"><span data-stu-id="c22b8-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="c22b8-194">`pluginType`jest używany typ wtyczki hello tooindicate hello C\# procesu.</span><span class="sxs-lookup"><span data-stu-id="c22b8-194">`pluginType` is used tooindicate hello plugin type of hello C\# process.</span></span> <span data-ttu-id="c22b8-195">Jeśli hello C\# proces jest uruchomiony w trybie lokalnym testu (bez Java), typ wtyczki hello jest `SCP_NET_LOCAL`.</span><span class="sxs-lookup"><span data-stu-id="c22b8-195">If hello C\# process is run in local test mode (without Java), hello plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="c22b8-196">`Config`podano tooget parametry konfiguracji po stronie Java.</span><span class="sxs-lookup"><span data-stu-id="c22b8-196">`Config` is provided tooget configuration parameters from Java side.</span></span> <span data-ttu-id="c22b8-197">Witaj parametry są przekazywane z Java strony po C\# dodatek został zainicjowany.</span><span class="sxs-lookup"><span data-stu-id="c22b8-197">hello parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="c22b8-198">Witaj `Config` parametry są podzielone na dwie części: `stormConf` i `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="c22b8-198">hello `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="c22b8-199">`stormConf`jest parametrów zdefiniowanych Storm i `pluginConf` jest hello parametrów zdefiniowanych przez punkt połączenia usługi.</span><span class="sxs-lookup"><span data-stu-id="c22b8-199">`stormConf` is parameters defined by Storm and `pluginConf` is hello parameters defined by SCP.</span></span> <span data-ttu-id="c22b8-200">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c22b8-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="c22b8-201">`TopologyContext`są podane w kontekście topologii tooget hello jest najbardziej przydatny w przypadku składników z wielu równoległości.</span><span class="sxs-lookup"><span data-stu-id="c22b8-201">`TopologyContext` is provided tooget hello topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="c22b8-202">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="c22b8-202">Here is an example:</span></span>

    //demo how tooget TopologyContext info
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)                      
    {
        Context.Logger.Info("TopologyContext info:");
        TopologyContext topologyContext = Context.TopologyContext;                    
        Context.Logger.Info("taskId: {0}", topologyContext.GetThisTaskId());          
        taskIndex = topologyContext.GetThisTaskIndex();
        Context.Logger.Info("taskIndex: {0}", taskIndex);
        string componentId = topologyContext.GetThisComponentId();                    
        Context.Logger.Info("componentId: {0}", componentId);
        List<int> componentTasks = topologyContext.GetComponentTasks(componentId);  
        Context.Logger.Info("taskNum: {0}", componentTasks.Count);                    
    }

### <a name="dynamic-part"></a><span data-ttu-id="c22b8-203">Części dynamicznej</span><span class="sxs-lookup"><span data-stu-id="c22b8-203">Dynamic Part</span></span>
<span data-ttu-id="c22b8-204">Witaj następujące interfejsy są istotne tooa niektórych wystąpienia kontekstu.</span><span class="sxs-lookup"><span data-stu-id="c22b8-204">hello following interfaces are pertinent tooa certain Context instance.</span></span> <span data-ttu-id="c22b8-205">wystąpienie kontekstu Hello jest tworzony przez platformę SCP.NET i przekazany kod użytkownika toohello:</span><span class="sxs-lookup"><span data-stu-id="c22b8-205">hello Context instance is created by SCP.NET platform and passed toohello user code:</span></span>

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="c22b8-206">Do obsługi potwierdzenia nietransakcyjnej spout podano hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="c22b8-206">For non-transactional spout supporting ack, hello following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="c22b8-207">Dla obsługi potwierdzenia nietransakcyjnej bolt, należy go jawnie `Ack()` lub `Fail()` hello odebrała spójnej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="c22b8-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` hello tuple it received.</span></span> <span data-ttu-id="c22b8-208">I podczas emitowania nowe spójnej kolekcji, należy także określić kotwice hello z hello nowej krotki.</span><span class="sxs-lookup"><span data-stu-id="c22b8-208">And when emitting new tuple, it must also specify hello anchors of hello new tuple.</span></span> <span data-ttu-id="c22b8-209">podano Hello następujące metody.</span><span class="sxs-lookup"><span data-stu-id="c22b8-209">hello following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="c22b8-210">Stan klientów</span><span class="sxs-lookup"><span data-stu-id="c22b8-210">StateStore</span></span>
<span data-ttu-id="c22b8-211">`StateStore`udostępnia usługi metadanych, generowanie monotoniczna sekwencji i koordynacji bez oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="c22b8-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="c22b8-212">Abstrakcje wyższego poziomu współbieżności rozproszonej mogą być wbudowane w `StateStore`, w tym rozproszonej blokad, kolejek rozproszonych bariery i transakcji usługi.</span><span class="sxs-lookup"><span data-stu-id="c22b8-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="c22b8-213">Punkt połączenia usługi, aplikacje mogą używać hello `State` obiekt toopersist niektóre informacje w dozorcy, szczególnie w przypadku topologii transakcyjnych.</span><span class="sxs-lookup"><span data-stu-id="c22b8-213">SCP applications may use hello `State` object toopersist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="c22b8-214">Wykonywanie, dzięki czemu transakcyjne spout ulegnie awarii, uruchom ponownie może pobrać hello niezbędne informacje z dozorcy i uruchom ponownie hello potoku.</span><span class="sxs-lookup"><span data-stu-id="c22b8-214">Doing so, if transactional spout crashes and restart, it can retrieve hello necessary information from ZooKeeper and restart hello pipeline.</span></span>

<span data-ttu-id="c22b8-215">Witaj `StateStore` obiekt ma głównie tych metod:</span><span class="sxs-lookup"><span data-stu-id="c22b8-215">hello `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method tooretrieve a state store of hello given path and connStr 
    /// </summary>
    /// <param name="storePath">StateStore Path</param>
    /// <param name="connStr">StateStore Address</param>
    /// <returns>Instance of StateStore</returns>
    public static StateStore Get(string storePath, string connStr);

    /// <summary>
    /// Create a new state object in this state store instance
    /// </summary>
    /// <returns>State from StateStore</returns>
    public State Create();

    /// <summary>
    /// Retrieve all states that were previously uncommitted, excluding all aborted states 
    /// </summary>
    /// <returns>Uncommited States</returns>
    public IEnumerable<State> GetUnCommitted();

    /// <summary>
    /// Get all hello States in hello StateStore
    /// </summary>
    /// <returns>All hello States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all hello committed states
    /// </summary>
    /// <returns>Registries contain hello Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all hello Aborted State in hello StateStore
    /// </summary>
    /// <returns>Registries contain hello Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of hello State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="c22b8-216">Witaj `State` obiekt ma głównie tych metod:</span><span class="sxs-lookup"><span data-stu-id="c22b8-216">hello `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set hello status of hello state object toocommit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set hello status of hello state object tooabort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under hello give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get hello attribute value associated with hello given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="c22b8-217">Dla hello `Commit()` metody, gdy simpleMode ustawiono tootrue, po prostu usunie hello odpowiadającego ZNode w dozorcy.</span><span class="sxs-lookup"><span data-stu-id="c22b8-217">For hello `Commit()` method, when simpleMode is set tootrue, it will simply delete hello corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="c22b8-218">W przeciwnym razie spowoduje usunięcie hello bieżącego ZNode i dodanie nowego węzła w hello zatwierdzone\_ścieżki.</span><span class="sxs-lookup"><span data-stu-id="c22b8-218">Otherwise, it will delete hello current ZNode, and adding a new node in hello COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="c22b8-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="c22b8-219">SCPRuntime</span></span>
<span data-ttu-id="c22b8-220">SCPRuntime zapewnia hello następujących dwóch metod.</span><span class="sxs-lookup"><span data-stu-id="c22b8-220">SCPRuntime provides hello following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="c22b8-221">`Initialize()`to środowisko uruchomieniowe hello SCP tooinitialize używane.</span><span class="sxs-lookup"><span data-stu-id="c22b8-221">`Initialize()` is used tooinitialize hello SCP runtime environment.</span></span> <span data-ttu-id="c22b8-222">W przypadku tej metody hello C\# procesu połączy toohello stronie Java i pobiera parametry konfiguracji i topologii kontekstu.</span><span class="sxs-lookup"><span data-stu-id="c22b8-222">In this method, hello C\# process will connect toohello Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="c22b8-223">`LaunchPlugin()`jest używana tookick poza wiadomość hello przetwarzanie pętli.</span><span class="sxs-lookup"><span data-stu-id="c22b8-223">`LaunchPlugin()` is used tookick off hello message processing loop.</span></span> <span data-ttu-id="c22b8-224">W tym pętli hello C\# wtyczki będą otrzymywać wiadomości formularza po stronie Java (w tym sygnały krotek i sterowania), a następnie podaj wiadomości powitania procesu, prawdopodobnie podczas wywoływania metody interfejsu hello przez kod użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="c22b8-224">In this loop, hello C\# plugin will receive messages form Java side (including tuples and control signals), and then process hello messages, perhaps calling hello interface method provide by hello user code.</span></span> <span data-ttu-id="c22b8-225">wejściowy parametr metody Hello `LaunchPlugin()` jest delegata, który może zwracać obiekt, który implementuje interfejs ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.</span><span class="sxs-lookup"><span data-stu-id="c22b8-225">hello input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="c22b8-226">Dla ISCPBatchBolt, można pobrać `StormTxAttempt` z `parms`i przy jego użyciu toojudge czy jest próba powtórzony.</span><span class="sxs-lookup"><span data-stu-id="c22b8-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it toojudge whether it is a replayed attempt.</span></span> <span data-ttu-id="c22b8-227">Zwykle odbywa się na powitania zatwierdzania bolt i zostało to przedstawione w hello `HelloWorldTx` przykład.</span><span class="sxs-lookup"><span data-stu-id="c22b8-227">This is usually done at hello commit bolt, and it is demonstrated in hello `HelloWorldTx` example.</span></span>

<span data-ttu-id="c22b8-228">Ogólnie rzecz biorąc hello wtyczek SCP może działać w dwóch trybach tutaj:</span><span class="sxs-lookup"><span data-stu-id="c22b8-228">Generally speaking, hello SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="c22b8-229">Tryb lokalnego testu: W tym trybie hello wtyczek punkt połączenia usługi (hello C\# kod użytkownika) uruchom w programie Visual Studio w fazie programowanie hello.</span><span class="sxs-lookup"><span data-stu-id="c22b8-229">Local Test Mode: In this mode, hello SCP plugins (hello C\# user code) run inside Visual Studio during hello development phase.</span></span> <span data-ttu-id="c22b8-230">`LocalContext`można w tym trybie, co zapewnia metody tooserialize hello wysyłanego krotek toolocal pliki i utworzyć ich kopię toomemory odczytu.</span><span class="sxs-lookup"><span data-stu-id="c22b8-230">`LocalContext` can be used in this mode, which provides method tooserialize hello emitted tuples toolocal files, and read them back toomemory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="c22b8-231">Tryb regularnych: W tym trybie wtyczek SCP hello będą uruchamiane przez proces java storm.</span><span class="sxs-lookup"><span data-stu-id="c22b8-231">Regular Mode: In this mode, hello SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="c22b8-232">Oto przykład uruchamiania SCP wtyczki:</span><span class="sxs-lookup"><span data-stu-id="c22b8-232">Here is an example of launching SCP plugin:</span></span>
   
        namespace Scp.App.HelloWorld
        {
        public class Generator : ISCPSpout
        {
            … …
            public static Generator Get(Context ctx, Dictionary<string, Object> parms)
            {
            return new Generator(ctx);
            }
        }
   
        class HelloWorld
        {
            static void Main(string[] args)
            {
            /* Setting hello environment variable here can change hello log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="c22b8-233">Topologia specyfikacja języka</span><span class="sxs-lookup"><span data-stu-id="c22b8-233">Topology Specification Language</span></span>
<span data-ttu-id="c22b8-234">Specyfikacja topologii punkt połączenia usługi jest domeny określonego języka dla zawierająca opis i Konfigurowanie topologii punkt połączenia usługi.</span><span class="sxs-lookup"><span data-stu-id="c22b8-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="c22b8-235">Jest on oparty na jego Storm Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) i zostanie rozszerzony przez punkt połączenia usługi.</span><span class="sxs-lookup"><span data-stu-id="c22b8-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="c22b8-236">Specyfikacje topologii można przesłać bezpośrednio toostorm klastra wykonywania za pośrednictwem hello ***runspec*** polecenia.</span><span class="sxs-lookup"><span data-stu-id="c22b8-236">Topology specifications can be submitted directly toostorm cluster for execution via hello ***runspec*** command.</span></span>

<span data-ttu-id="c22b8-237">SCP.NET ma Dodaj następujące funkcje toodefine hello transakcyjne topologii:</span><span class="sxs-lookup"><span data-stu-id="c22b8-237">SCP.NET has add follow functions toodefine hello Transactional Topology:</span></span>

| <span data-ttu-id="c22b8-238">**Nowe funkcje**</span><span class="sxs-lookup"><span data-stu-id="c22b8-238">**New Functions**</span></span> | <span data-ttu-id="c22b8-239">**Parametry**</span><span class="sxs-lookup"><span data-stu-id="c22b8-239">**Parameters**</span></span> | <span data-ttu-id="c22b8-240">**Opis**</span><span class="sxs-lookup"><span data-stu-id="c22b8-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c22b8-241">**TX topolopy**</span><span class="sxs-lookup"><span data-stu-id="c22b8-241">**tx-topolopy**</span></span> |<span data-ttu-id="c22b8-242">Nazwa topologii</span><span class="sxs-lookup"><span data-stu-id="c22b8-242">topology-name</span></span><br /><span data-ttu-id="c22b8-243">spout mapy</span><span class="sxs-lookup"><span data-stu-id="c22b8-243">spout-map</span></span><br /><span data-ttu-id="c22b8-244">bolt mapy</span><span class="sxs-lookup"><span data-stu-id="c22b8-244">bolt-map</span></span> |<span data-ttu-id="c22b8-245">Zdefiniuj transakcyjne topologii o nazwie topologii hello, &nbsp;spouts mapy definicji i hello elementów bolt definicji mapy</span><span class="sxs-lookup"><span data-stu-id="c22b8-245">Define a transactional topology with hello topology name, &nbsp;spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="c22b8-246">**spout-tx — punkt połączenia usługi**</span><span class="sxs-lookup"><span data-stu-id="c22b8-246">**scp-tx-spout**</span></span> |<span data-ttu-id="c22b8-247">exec — nazwa</span><span class="sxs-lookup"><span data-stu-id="c22b8-247">exec-name</span></span><br /><span data-ttu-id="c22b8-248">argumentów</span><span class="sxs-lookup"><span data-stu-id="c22b8-248">args</span></span><br /><span data-ttu-id="c22b8-249">Pola</span><span class="sxs-lookup"><span data-stu-id="c22b8-249">fields</span></span> |<span data-ttu-id="c22b8-250">Zdefiniuj spout transakcyjnych.</span><span class="sxs-lookup"><span data-stu-id="c22b8-250">Define a transactional spout.</span></span> <span data-ttu-id="c22b8-251">Zostanie uruchomiony aplikacji hello z ***nazwa exec*** przy użyciu ***argumentów***.</span><span class="sxs-lookup"><span data-stu-id="c22b8-251">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="c22b8-252">Witaj ***pola*** jest hello pól danych wyjściowych dla spout</span><span class="sxs-lookup"><span data-stu-id="c22b8-252">hello ***fields*** is hello Output Fields for spout</span></span> |
| <span data-ttu-id="c22b8-253">**punkt połączenia usługi tx partii bolt**</span><span class="sxs-lookup"><span data-stu-id="c22b8-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="c22b8-254">exec — nazwa</span><span class="sxs-lookup"><span data-stu-id="c22b8-254">exec-name</span></span><br /><span data-ttu-id="c22b8-255">argumentów</span><span class="sxs-lookup"><span data-stu-id="c22b8-255">args</span></span><br /><span data-ttu-id="c22b8-256">Pola</span><span class="sxs-lookup"><span data-stu-id="c22b8-256">fields</span></span> |<span data-ttu-id="c22b8-257">Zdefiniuj transakcyjne Bolt partii.</span><span class="sxs-lookup"><span data-stu-id="c22b8-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="c22b8-258">Zostanie uruchomiony aplikacji hello z ***nazwa exec*** przy użyciu ***argumentów.***</span><span class="sxs-lookup"><span data-stu-id="c22b8-258">It will run hello application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="c22b8-259">Witaj pola jest hello pól danych wyjściowych dla bolt.</span><span class="sxs-lookup"><span data-stu-id="c22b8-259">hello Fields is hello Output Fields for bolt.</span></span> |
| <span data-ttu-id="c22b8-260">**punkt połączenia usługi tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="c22b8-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="c22b8-261">exec — nazwa</span><span class="sxs-lookup"><span data-stu-id="c22b8-261">exec-name</span></span><br /><span data-ttu-id="c22b8-262">argumentów</span><span class="sxs-lookup"><span data-stu-id="c22b8-262">args</span></span><br /><span data-ttu-id="c22b8-263">Pola</span><span class="sxs-lookup"><span data-stu-id="c22b8-263">fields</span></span> |<span data-ttu-id="c22b8-264">Zdefiniuj transakcyjne Bolt zatwierdzający.</span><span class="sxs-lookup"><span data-stu-id="c22b8-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="c22b8-265">Zostanie uruchomiony aplikacji hello z ***nazwa exec*** przy użyciu ***argumentów***.</span><span class="sxs-lookup"><span data-stu-id="c22b8-265">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="c22b8-266">Witaj ***pola*** jest hello pól danych wyjściowych dla bolt</span><span class="sxs-lookup"><span data-stu-id="c22b8-266">hello ***fields*** is hello Output Fields for bolt</span></span> |
| <span data-ttu-id="c22b8-267">**nontx topolopy**</span><span class="sxs-lookup"><span data-stu-id="c22b8-267">**nontx-topolopy**</span></span> |<span data-ttu-id="c22b8-268">Nazwa topologii</span><span class="sxs-lookup"><span data-stu-id="c22b8-268">topology-name</span></span><br /><span data-ttu-id="c22b8-269">spout mapy</span><span class="sxs-lookup"><span data-stu-id="c22b8-269">spout-map</span></span><br /><span data-ttu-id="c22b8-270">bolt mapy</span><span class="sxs-lookup"><span data-stu-id="c22b8-270">bolt-map</span></span> |<span data-ttu-id="c22b8-271">Zdefiniuj topologię nietransakcyjne o nazwie topologii hello,&nbsp; spouts mapy definicji i hello elementów bolt definicji mapy</span><span class="sxs-lookup"><span data-stu-id="c22b8-271">Define a nontransactional topology with hello topology name,&nbsp; spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="c22b8-272">**spout punkt połączenia usługi**</span><span class="sxs-lookup"><span data-stu-id="c22b8-272">**scp-spout**</span></span> |<span data-ttu-id="c22b8-273">exec — nazwa</span><span class="sxs-lookup"><span data-stu-id="c22b8-273">exec-name</span></span><br /><span data-ttu-id="c22b8-274">argumentów</span><span class="sxs-lookup"><span data-stu-id="c22b8-274">args</span></span><br /><span data-ttu-id="c22b8-275">Pola</span><span class="sxs-lookup"><span data-stu-id="c22b8-275">fields</span></span><br /><span data-ttu-id="c22b8-276">parameters</span><span class="sxs-lookup"><span data-stu-id="c22b8-276">parameters</span></span> |<span data-ttu-id="c22b8-277">Zdefiniuj spout nietransakcyjne.</span><span class="sxs-lookup"><span data-stu-id="c22b8-277">Define a nontransactional spout.</span></span> <span data-ttu-id="c22b8-278">Zostanie uruchomiony aplikacji hello z ***nazwa exec*** przy użyciu ***argumentów***.</span><span class="sxs-lookup"><span data-stu-id="c22b8-278">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="c22b8-279">Witaj ***pola*** jest hello pól danych wyjściowych dla spout</span><span class="sxs-lookup"><span data-stu-id="c22b8-279">hello ***fields*** is hello Output Fields for spout</span></span><br /><br /><span data-ttu-id="c22b8-280">Witaj ***parametry*** jest opcjonalny, przy jej użyciu toospecify niektóre parametry, takie jak "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="c22b8-280">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="c22b8-281">**bolt punkt połączenia usługi**</span><span class="sxs-lookup"><span data-stu-id="c22b8-281">**scp-bolt**</span></span> |<span data-ttu-id="c22b8-282">exec — nazwa</span><span class="sxs-lookup"><span data-stu-id="c22b8-282">exec-name</span></span><br /><span data-ttu-id="c22b8-283">argumentów</span><span class="sxs-lookup"><span data-stu-id="c22b8-283">args</span></span><br /><span data-ttu-id="c22b8-284">Pola</span><span class="sxs-lookup"><span data-stu-id="c22b8-284">fields</span></span><br /><span data-ttu-id="c22b8-285">parameters</span><span class="sxs-lookup"><span data-stu-id="c22b8-285">parameters</span></span> |<span data-ttu-id="c22b8-286">Zdefiniuj nietransakcyjne Bolt.</span><span class="sxs-lookup"><span data-stu-id="c22b8-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="c22b8-287">Zostanie uruchomiony aplikacji hello z ***nazwa exec*** przy użyciu ***argumentów***.</span><span class="sxs-lookup"><span data-stu-id="c22b8-287">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="c22b8-288">Witaj ***pola*** jest hello pól danych wyjściowych dla bolt</span><span class="sxs-lookup"><span data-stu-id="c22b8-288">hello ***fields*** is hello Output Fields for bolt</span></span><br /><br /><span data-ttu-id="c22b8-289">Witaj ***parametry*** jest opcjonalny, przy jej użyciu toospecify niektóre parametry, takie jak "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="c22b8-289">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="c22b8-290">Wykonaj ma SCP.NET kluczy zdefiniowane słowa:</span><span class="sxs-lookup"><span data-stu-id="c22b8-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="c22b8-291">**Słowa kluczowe**</span><span class="sxs-lookup"><span data-stu-id="c22b8-291">**Key Words**</span></span> | <span data-ttu-id="c22b8-292">**Opis**</span><span class="sxs-lookup"><span data-stu-id="c22b8-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="c22b8-293">**: Nazwa**</span><span class="sxs-lookup"><span data-stu-id="c22b8-293">**:name**</span></span> |<span data-ttu-id="c22b8-294">Zdefiniuj hello nazwa topologii</span><span class="sxs-lookup"><span data-stu-id="c22b8-294">Define hello Topology Name</span></span> |
| <span data-ttu-id="c22b8-295">**: topologii**</span><span class="sxs-lookup"><span data-stu-id="c22b8-295">**:topology**</span></span> |<span data-ttu-id="c22b8-296">Zdefiniuj hello topologię za pomocą hello powyżej funkcje i kompilacji w tych.</span><span class="sxs-lookup"><span data-stu-id="c22b8-296">Define hello Topology using hello above functions and build in ones.</span></span> |
| <span data-ttu-id="c22b8-297">**: p**</span><span class="sxs-lookup"><span data-stu-id="c22b8-297">**:p**</span></span> |<span data-ttu-id="c22b8-298">Zdefiniuj hello równoległości wskazówkę dla każdego spout lub bolt.</span><span class="sxs-lookup"><span data-stu-id="c22b8-298">Define hello parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="c22b8-299">**: config**</span><span class="sxs-lookup"><span data-stu-id="c22b8-299">**:config**</span></span> |<span data-ttu-id="c22b8-300">Zdefiniuj skonfigurować parametru lub aktualizacji hello istniejących</span><span class="sxs-lookup"><span data-stu-id="c22b8-300">Define configure parameter or update hello existing ones</span></span> |
| <span data-ttu-id="c22b8-301">**: schematu**</span><span class="sxs-lookup"><span data-stu-id="c22b8-301">**:schema**</span></span> |<span data-ttu-id="c22b8-302">Zdefiniuj hello schematu strumienia.</span><span class="sxs-lookup"><span data-stu-id="c22b8-302">Define hello Schema of Stream.</span></span> |

<span data-ttu-id="c22b8-303">I często używane parametry:</span><span class="sxs-lookup"><span data-stu-id="c22b8-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="c22b8-304">**Parametr**</span><span class="sxs-lookup"><span data-stu-id="c22b8-304">**Parameter**</span></span> | <span data-ttu-id="c22b8-305">**Opis**</span><span class="sxs-lookup"><span data-stu-id="c22b8-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="c22b8-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="c22b8-306">**"plugin.name"**</span></span> |<span data-ttu-id="c22b8-307">Nazwa pliku exe wtyczki hello C#</span><span class="sxs-lookup"><span data-stu-id="c22b8-307">exe file name of hello C# plugin</span></span> |
| <span data-ttu-id="c22b8-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="c22b8-308">**"plugin.args"**</span></span> |<span data-ttu-id="c22b8-309">argumenty wtyczki</span><span class="sxs-lookup"><span data-stu-id="c22b8-309">plugin args</span></span> |
| <span data-ttu-id="c22b8-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="c22b8-310">**"output.schema"**</span></span> |<span data-ttu-id="c22b8-311">Schemat danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="c22b8-311">Output schema</span></span> |
| <span data-ttu-id="c22b8-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="c22b8-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="c22b8-313">Czy potwierdzenia jest włączone dla topologii nietransakcyjne</span><span class="sxs-lookup"><span data-stu-id="c22b8-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="c22b8-314">polecenie runspec Hello zostaną wdrożone razem z bitów hello, użycie hello jest podobne:</span><span class="sxs-lookup"><span data-stu-id="c22b8-314">hello runspec command will be deployed together with hello bits, hello usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="c22b8-315">Hello ***zasobów dir*** parametr jest opcjonalny, należy toospecify go, jeśli chcesz tooplug C\# aplikacji, a ten katalog będzie zawierać aplikacji hello hello zależności i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c22b8-315">hello ***resource-dir*** parameter is optional, you need toospecify it when you want tooplug a C\# application, and this directory will contain hello application, hello dependencies and configurations.</span></span>

<span data-ttu-id="c22b8-316">Witaj ***ścieżki klasy*** parametr również jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="c22b8-316">hello ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="c22b8-317">Jeśli plik specyfikacji hello zawiera Java Spout lub Bolt jest klasy Java hello toospecify używane.</span><span class="sxs-lookup"><span data-stu-id="c22b8-317">It is used toospecify hello Java classpath if hello spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="c22b8-318">Różne funkcje</span><span class="sxs-lookup"><span data-stu-id="c22b8-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="c22b8-319">Danych wejściowych i wyjściowych schematu deklaracji</span><span class="sxs-lookup"><span data-stu-id="c22b8-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="c22b8-320">Witaj użytkownika może emitować spójnej kolekcji w języku C\# przetwarzania, hello platformy potrzeb krotki hello tooserialize byte [] stronie tooJava transferu, i Storm będzie przenieść ten cele toohello spójnej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="c22b8-320">hello user can emit tuple in C\# process, hello platform needs tooserialize hello tuple into byte[], transfer tooJava side, and Storm will transfer this tuple toohello targets.</span></span> <span data-ttu-id="c22b8-321">W tym samym czasie w składniku podrzędne hello C\# proces będzie otrzymywać krotki powrotem po stronie java i przekształcić ją typów pierwotnego toohello przez platformę, wszystkie czynności są ukryte przez hello platformy.</span><span class="sxs-lookup"><span data-stu-id="c22b8-321">Meanwhile in downstream component, hello C\# process will receive tuple back from java side, and convert it toohello original types by platform, all these operations are hidden by hello Platform.</span></span>

<span data-ttu-id="c22b8-322">toosupport hello serializacji i deserializacji kodu użytkownika musi toodeclare hello schemat hello wejścia i wyjścia.</span><span class="sxs-lookup"><span data-stu-id="c22b8-322">toosupport hello serialization and deserialization, user code needs toodeclare hello schema of hello inputs and outputs.</span></span>

<span data-ttu-id="c22b8-323">Schemat wejścia/wyjścia strumienia Hello jest zdefiniowany jako słownik, klucz hello jest hello StreamId a hello hello typów kolumn hello.</span><span class="sxs-lookup"><span data-stu-id="c22b8-323">hello input/output stream schema is defined as a dictionary, hello key is hello StreamId and hello value is hello Types of hello columns.</span></span> <span data-ttu-id="c22b8-324">składnik Hello może mieć wielu strumieni zadeklarowany.</span><span class="sxs-lookup"><span data-stu-id="c22b8-324">hello component can have multi-streams declared.</span></span>

    public class ComponentStreamSchema
    {
        public Dictionary<string, List<Type>> InputStreamSchema { get; set; }
        public Dictionary<string, List<Type>> OutputStreamSchema { get; set; }
        public ComponentStreamSchema(Dictionary<string, List<Type>> input, Dictionary<string, List<Type>> output)
        {
            InputStreamSchema = input;
            OutputStreamSchema = output;
        }
    }


<span data-ttu-id="c22b8-325">Obiekt kontekstu mamy hello dodano następujący interfejs API:</span><span class="sxs-lookup"><span data-stu-id="c22b8-325">In Context object, we have hello following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="c22b8-326">Kod użytkownika, należy się upewnić, krotek hello wysyłanego przestrzegać schematu hello zdefiniowane dla tego strumienia lub hello system zgłosi wyjątek czasu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="c22b8-326">User code must make sure hello tuples emitted obey hello schema defined for that stream, or hello system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="c22b8-327">Obsługa wielu strumienia</span><span class="sxs-lookup"><span data-stu-id="c22b8-327">Multi-Stream Support</span></span>
<span data-ttu-id="c22b8-328">Użytkownika obsługuje SCP kodu tooemit lub odebrać z wielu różnych strumieni na powitania sam czas.</span><span class="sxs-lookup"><span data-stu-id="c22b8-328">SCP supports user code tooemit or receive from multiple distinct streams at hello same time.</span></span> <span data-ttu-id="c22b8-329">Obsługa Hello odzwierciedla w obiekt kontekstu hello jako hello emitowanie metoda przyjmuje parametr ID opcjonalne strumienia.</span><span class="sxs-lookup"><span data-stu-id="c22b8-329">hello support reflects in hello Context object as hello Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="c22b8-330">Dodano dwie metody w hello obiekt SCP.NET kontekstu.</span><span class="sxs-lookup"><span data-stu-id="c22b8-330">Two methods in hello SCP.NET Context object have been added.</span></span> <span data-ttu-id="c22b8-331">Są one używane tooemit spójnej kolekcji lub krotek toospecify StreamId.</span><span class="sxs-lookup"><span data-stu-id="c22b8-331">They are used tooemit Tuple or Tuples toospecify StreamId.</span></span> <span data-ttu-id="c22b8-332">Hello StreamId jest ciągiem i musi on toobe spójne w obu C\# i hello specyfikacji definicji topologii.</span><span class="sxs-lookup"><span data-stu-id="c22b8-332">hello StreamId is a string and it needs toobe consistent in both C\# and hello Topology Definition Spec.</span></span>

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="c22b8-333">wyjątki czasu wykonywania spowoduje, że Hello emisji tooa nieistniejącego strumienia.</span><span class="sxs-lookup"><span data-stu-id="c22b8-333">hello emitting tooa non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="c22b8-334">Grupowanie pól</span><span class="sxs-lookup"><span data-stu-id="c22b8-334">Fields Grouping</span></span>
<span data-ttu-id="c22b8-335">Witaj w kompilacji Grupowanie pól w Strom nie działa prawidłowo w SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="c22b8-335">hello build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="c22b8-336">Na powitania po stronie serwera Proxy Java wszystkie typy danych pola hello są faktycznie byte [], a pola hello grupowanie używa hello byte [] obiektu skrótu kodu tooperform hello grupowania.</span><span class="sxs-lookup"><span data-stu-id="c22b8-336">On hello Java Proxy side, all hello fields data types are actually byte[], and hello fields grouping uses hello byte[] object hash code tooperform hello grouping.</span></span> <span data-ttu-id="c22b8-337">Witaj byte [] obiektu skrótu jest adresem hello tego obiektu w pamięci.</span><span class="sxs-lookup"><span data-stu-id="c22b8-337">hello byte[] object hash code is hello address of this object in memory.</span></span> <span data-ttu-id="c22b8-338">Dzięki grupowania hello będą nieprawidłowe dla dwóch bajtów [] obiektów hello tego udziału, same zawartości, ale nie hello tego samego adresu.</span><span class="sxs-lookup"><span data-stu-id="c22b8-338">So hello grouping will be wrong for two byte[] objects that share hello same content but not hello same address.</span></span>

<span data-ttu-id="c22b8-339">SCP.NET dodaje metodę grupowania dostosowane, i użyje zawartości hello hello byte [] toodo hello grupowania.</span><span class="sxs-lookup"><span data-stu-id="c22b8-339">SCP.NET adds a customized grouping method, and it will use hello content of hello byte[] toodo hello grouping.</span></span> <span data-ttu-id="c22b8-340">W **SPEC** pliku przypomina hello składni:</span><span class="sxs-lookup"><span data-stu-id="c22b8-340">In **SPEC** file, hello syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="c22b8-341">Tutaj</span><span class="sxs-lookup"><span data-stu-id="c22b8-341">Here,</span></span>

1. <span data-ttu-id="c22b8-342">"punkt połączenia usługi pola group" oznacza "Grupowania pola niestandardowe implementowane przez punkt połączenia usługi".</span><span class="sxs-lookup"><span data-stu-id="c22b8-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="c22b8-343">": tx"lub":-tx" oznacza, że jeśli jest transakcyjna topologii.</span><span class="sxs-lookup"><span data-stu-id="c22b8-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="c22b8-344">Potrzebujemy tych informacji, ponieważ hello początkowy indeks jest inna w tx a topologie-tx.</span><span class="sxs-lookup"><span data-stu-id="c22b8-344">We need this information since hello starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="c22b8-345">zestaw hashset identyfikatory pola, począwszy od 0 oznacza [0,1].</span><span class="sxs-lookup"><span data-stu-id="c22b8-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="c22b8-346">Topologia hybrydowego</span><span class="sxs-lookup"><span data-stu-id="c22b8-346">Hybrid topology</span></span>
<span data-ttu-id="c22b8-347">natywny Hello Storm są zapisywane w języku Java.</span><span class="sxs-lookup"><span data-stu-id="c22b8-347">hello native Storm is written in Java.</span></span> <span data-ttu-id="c22b8-348">I SCP.Net rozszerzonego, jego tooenable naszych toowrite celne C\# kodu toohandle ich logiki biznesowej.</span><span class="sxs-lookup"><span data-stu-id="c22b8-348">And SCP.Net has enhanced it tooenable our customs toowrite C\# code toohandle their business logic.</span></span> <span data-ttu-id="c22b8-349">Obsługujemy również hybrydowe topologie, która zawiera nie tylko C, ale\# elementów elementach spout/bolt, ale również elementów Java Spout/Bolt.</span><span class="sxs-lookup"><span data-stu-id="c22b8-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="c22b8-350">Określ Java Spout/Bolt w specyfikacji pliku</span><span class="sxs-lookup"><span data-stu-id="c22b8-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="c22b8-351">W specyfikacji pliku "punkt połączenia usługi spout" i "punkt połączenia usługi bolt" można też Spouts Java toospecify używane i elementów Bolt, Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="c22b8-351">In spec file, "scp-spout" and "scp-bolt" can also be used toospecify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="c22b8-352">W tym miejscu `microsoft.scp.example.HybridTopology.Generator` jest nazwą hello hello Klasa Java Spout.</span><span class="sxs-lookup"><span data-stu-id="c22b8-352">Here `microsoft.scp.example.HybridTopology.Generator` is hello name of hello Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="c22b8-353">Określ klasy Java w runSpec polecenia</span><span class="sxs-lookup"><span data-stu-id="c22b8-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="c22b8-354">Chcąc topologii toosubmit zawierające Java Spouts lub elementów Bolt, wymaga hello kompilacji toofirst Java Spouts lub elementów Bolt i Pobierz pliki Jar hello.</span><span class="sxs-lookup"><span data-stu-id="c22b8-354">If you want toosubmit topology containing Java Spouts or Bolts, you need toofirst compile hello Java Spouts or Bolts and get hello Jar files.</span></span> <span data-ttu-id="c22b8-355">Następnie należy określić klasy java hello, który zawiera pliki Jar hello podczas przesyłania topologii.</span><span class="sxs-lookup"><span data-stu-id="c22b8-355">Then you should specify hello java classpath that contains hello Jar files when submitting topology.</span></span> <span data-ttu-id="c22b8-356">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="c22b8-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="c22b8-357">W tym miejscu **przykłady\\HybridTopology\\java\\docelowej\\**  jest hello folder zawierający plik Jar Spout/Bolt Java hello.</span><span class="sxs-lookup"><span data-stu-id="c22b8-357">Here **examples\\HybridTopology\\java\\target\\** is hello folder containing hello Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="c22b8-358">Serializacja i deserializacja między Java i C\\</span><span class="sxs-lookup"><span data-stu-id="c22b8-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="c22b8-359">Nasze składnik SCP zawiera stronie Java i C\# po stronie.</span><span class="sxs-lookup"><span data-stu-id="c22b8-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="c22b8-360">W kolejności toointeract z macierzystego Java elementach Spout/elementów Bolt, serializacji/deserializacji przeprowadza się między stronie Java i C\# po stronie, jak pokazano na powitania po wykresu.</span><span class="sxs-lookup"><span data-stu-id="c22b8-360">In order toointeract with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in hello following graph.</span></span>

![Diagram składnika java wysyłania składnika tooSCP wysyłania tooJava składnika](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="c22b8-362">**Serializacja w stronie Java i deserializacji w języku C\# po stronie**</span><span class="sxs-lookup"><span data-stu-id="c22b8-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="c22b8-363">Najpierw firma Microsoft udostępnia domyślną implementację do serializacji w języku Java po stronie i deserializacji w języku C\# po stronie.</span><span class="sxs-lookup"><span data-stu-id="c22b8-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="c22b8-364">Witaj metoda serializacji w języku Java po stronie można określić w specyfikacji pliku:</span><span class="sxs-lookup"><span data-stu-id="c22b8-364">hello serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="c22b8-365">Witaj metody deserializacji w języku C\# po stronie powinny być określone w języku C\# kod użytkownika:</span><span class="sxs-lookup"><span data-stu-id="c22b8-365">hello deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="c22b8-366">Ta domyślna implementacja powinna obsługiwać większości przypadków, jeśli hello — typ danych nie jest zbyt złożony.</span><span class="sxs-lookup"><span data-stu-id="c22b8-366">This default implementation should handle most cases if hello data type is not too complex.</span></span> <span data-ttu-id="c22b8-367">W niektórych przypadkach albo ponieważ hello typie danych użytkownika jest zbyt złożony lub hello wydajności naszych Domyślna implementacja nie spełnia hello wymaganie użytkownika, użytkownik może wtyczki realizacji.</span><span class="sxs-lookup"><span data-stu-id="c22b8-367">For certain cases, either because hello user data type is too complex, or because hello performance of our default implementation does not meet hello user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="c22b8-368">Witaj serializować interfejsu w języku java po stronie jest zdefiniowany jako:</span><span class="sxs-lookup"><span data-stu-id="c22b8-368">hello serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="c22b8-369">Witaj deserializacji interfejsu w języku C\# po stronie jest zdefiniowany jako:</span><span class="sxs-lookup"><span data-stu-id="c22b8-369">hello deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="c22b8-370">Interfejs publiczny ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="c22b8-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="c22b8-371">**Serializacji w języku C\# po stronie i deserializacji w języku Java obok siebie**</span><span class="sxs-lookup"><span data-stu-id="c22b8-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="c22b8-372">Witaj, metoda serializacji w języku C\# po stronie powinny być określone w języku C\# kod użytkownika:</span><span class="sxs-lookup"><span data-stu-id="c22b8-372">hello serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="c22b8-373">Witaj metody deserializacji po stronie Java powinny być określone w specyfikacji pliku:</span><span class="sxs-lookup"><span data-stu-id="c22b8-373">hello Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="c22b8-374">(punkt połączenia usługi spout</span><span class="sxs-lookup"><span data-stu-id="c22b8-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="c22b8-375">Tutaj "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" jest nazwą hello Deserializator i "microsoft.scp.example.HybridTopology.Person" oznacza dane hello klasy docelowej hello jest deserializacji do.</span><span class="sxs-lookup"><span data-stu-id="c22b8-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is hello name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is hello target class hello data is deserialized to.</span></span>
   
   <span data-ttu-id="c22b8-376">Użytkownik może również wtyczki realizacji c\# serializator i Deserializator Java.</span><span class="sxs-lookup"><span data-stu-id="c22b8-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="c22b8-377">Jest to interfejs hello C\# serializator:</span><span class="sxs-lookup"><span data-stu-id="c22b8-377">This is hello interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="c22b8-378">Jest to interfejs hello Deserializator Java:</span><span class="sxs-lookup"><span data-stu-id="c22b8-378">This is hello interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="c22b8-379">Tryb punktu połączenia usługi hosta</span><span class="sxs-lookup"><span data-stu-id="c22b8-379">SCP Host Mode</span></span>
<span data-ttu-id="c22b8-380">W tym trybie użytkownika można skompilować tooDLL ich kody i korzystać SCPHost.exe dostarczonych przez punkt połączenia usługi toosubmit topologii.</span><span class="sxs-lookup"><span data-stu-id="c22b8-380">In this mode, user can compile their codes tooDLL, and use SCPHost.exe provided by SCP toosubmit topology.</span></span> <span data-ttu-id="c22b8-381">Witaj specyfikacji pliku wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="c22b8-381">hello spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="c22b8-382">W tym miejscu `plugin.name` jest określony jako `SCPHost.exe` dostarczonych przez punkt połączenia usługi SDK.</span><span class="sxs-lookup"><span data-stu-id="c22b8-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="c22b8-383">SCPHost.exe akceptującego dokładnie trzy parametry:</span><span class="sxs-lookup"><span data-stu-id="c22b8-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="c22b8-384">Witaj najpierw jeden jest hello nazwy biblioteki DLL, która jest `"HelloWorld.dll"` w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c22b8-384">hello first one is hello DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="c22b8-385">Witaj drugim jest hello nazwy klasy, która jest `"Scp.App.HelloWorld.Generator"` w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c22b8-385">hello second one is hello Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="c22b8-386">Witaj innej jedną jest hello nazwa publicznej metody statycznej, który może być wywołana tooget wystąpienia ISCPPlugin.</span><span class="sxs-lookup"><span data-stu-id="c22b8-386">hello third one is hello name of a public static method, which can be invoked tooget an instance of ISCPPlugin.</span></span>

<span data-ttu-id="c22b8-387">W trybie hosta kod użytkownika jest skompilowana jako biblioteki DLL i jest wywoływane przez platformę punkt połączenia usługi.</span><span class="sxs-lookup"><span data-stu-id="c22b8-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="c22b8-388">Dlatego platformy punkt połączenia usługi można uzyskać pełną kontrolę nad hello całego przetwarzania logiki.</span><span class="sxs-lookup"><span data-stu-id="c22b8-388">So SCP platform can get full control of hello whole processing logic.</span></span> <span data-ttu-id="c22b8-389">Dlatego zalecamy naszych klientów toosubmit topologii w trybie hosta SCP ponieważ można uprościć środowisko programistyczne hello i przełączyć nam większą elastyczność i lepszą zgodność z poprzednimi wersjami oraz nowszych wersji.</span><span class="sxs-lookup"><span data-stu-id="c22b8-389">So we recommend our customers toosubmit topology in SCP host mode since it can simplify hello development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="c22b8-390">Przykłady programowania w języku punkt połączenia usługi</span><span class="sxs-lookup"><span data-stu-id="c22b8-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="c22b8-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="c22b8-391">HelloWorld</span></span>
<span data-ttu-id="c22b8-392">**HelloWorld** jest tooshow bardzo prosty przykład smak SCP.Net.</span><span class="sxs-lookup"><span data-stu-id="c22b8-392">**HelloWorld** is a very simple example tooshow a taste of SCP.Net.</span></span> <span data-ttu-id="c22b8-393">Za pomocą topologii nietransakcyjnej i spout, nazywany **generator**i dwóch elementów bolt o nazwie **podziału** i **licznika**.</span><span class="sxs-lookup"><span data-stu-id="c22b8-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="c22b8-394">Hello spout **generator** losowo spowoduje wygenerowanie zdań niektóre i wyemitować tych zdań zbyt**podziału**.</span><span class="sxs-lookup"><span data-stu-id="c22b8-394">hello spout **generator** will randomly generate some sentences, and emit these sentences too**splitter**.</span></span> <span data-ttu-id="c22b8-395">Hello bolt **podziału** będzie podzielić toowords zdań hello i zbyt Emituj te słowa**licznika** bolt.</span><span class="sxs-lookup"><span data-stu-id="c22b8-395">hello bolt **splitter** will split hello sentences toowords and emit these words too**counter** bolt.</span></span> <span data-ttu-id="c22b8-396">Witaj bolt "licznika" używa wielu wystąpienie słownika toorecord hello każdego wyrazu.</span><span class="sxs-lookup"><span data-stu-id="c22b8-396">hello bolt "counter" uses a dictionary toorecord hello occurrence number of each word.</span></span>

<span data-ttu-id="c22b8-397">Istnieją dwa pliki specyfikacji, **HelloWorld.spec** i **HelloWorld\_EnableAck.spec** w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c22b8-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="c22b8-398">W hello C\# kodu, go można ustalić, czy potwierdzenia jest włączona pobierając hello pluginConf z strony Java.</span><span class="sxs-lookup"><span data-stu-id="c22b8-398">In hello C\# code, it can find out whether ack is enabled by getting hello pluginConf from Java side.</span></span>

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="c22b8-399">Po włączeniu potwierdzenia w hello spout słownik jest używane toocache hello krotek, które nie zostały jeszcze prześledzone.</span><span class="sxs-lookup"><span data-stu-id="c22b8-399">In hello spout, if ack is enabled, a dictionary is used toocache hello tuples that have not been acked.</span></span> <span data-ttu-id="c22b8-400">Jeśli po wywołaniu Fail() hello krotki nie powiodło się zostaną odtworzone:</span><span class="sxs-lookup"><span data-stu-id="c22b8-400">If Fail() is called, hello failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get hello cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay hello failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="c22b8-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="c22b8-401">HelloWorldTx</span></span>
<span data-ttu-id="c22b8-402">Witaj **HelloWorldTx** przykładzie pokazano, jak tooimplement transakcyjnych topologii.</span><span class="sxs-lookup"><span data-stu-id="c22b8-402">hello **HelloWorldTx** example demonstrates how tooimplement transactional topology.</span></span> <span data-ttu-id="c22b8-403">Ma on jeden spout o nazwie **generator**, partii elementów bolt o nazwie **partial-count**, i wywołuje bolt zatwierdzania **Suma liczba**.</span><span class="sxs-lookup"><span data-stu-id="c22b8-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="c22b8-404">Istnieją również trzy pliki txt wstępnie utworzone: **DataSource0.txt**, **DataSource1.txt** i **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="c22b8-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="c22b8-405">W każdej transakcji hello spout **generator** będzie losowo wybierz dwa pliki z hello wstępnie utworzone trzy pliki i emisji toohello nazwy pliku hello dwa **partial-count** bolt.</span><span class="sxs-lookup"><span data-stu-id="c22b8-405">In each transaction, hello spout **generator** will randomly choose two files from hello pre-created three files, and emit hello two file names toohello **partial-count** bolt.</span></span> <span data-ttu-id="c22b8-406">Hello bolt **partial-count** najpierw pobrać nazwy pliku hello hello Odebrano spójnej kolekcji, a następnie otwórz hello plików i liczba hello liczbę słów w tym pliku, a ostatecznie Emituj toohello numer word hello **Suma liczba**bolt.</span><span class="sxs-lookup"><span data-stu-id="c22b8-406">hello bolt **partial-count** will first get hello file name from hello received tuple, then open hello file and count hello number of words in this file, and finally emit hello word number toohello **count-sum** bolt.</span></span> <span data-ttu-id="c22b8-407">Witaj **Suma liczba** bolt podsumowanie hello łączna liczba.</span><span class="sxs-lookup"><span data-stu-id="c22b8-407">hello **count-sum** bolt will summarize hello total count.</span></span>

<span data-ttu-id="c22b8-408">tooachieve **dokładnie raz** semantyki, hello zatwierdzania bolt **Suma liczba** muszą toojudge, czy jest powtórzonym transakcji.</span><span class="sxs-lookup"><span data-stu-id="c22b8-408">tooachieve **exactly once** semantics, hello commit bolt **count-sum** need toojudge whether it is a replayed transaction.</span></span> <span data-ttu-id="c22b8-409">W tym przykładzie ma statycznym elementem członkowskim zmiennej:</span><span class="sxs-lookup"><span data-stu-id="c22b8-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="c22b8-410">Po utworzeniu wystąpienia ISCPBatchBolt pobierze hello `txAttempt` z parametrów wejściowych:</span><span class="sxs-lookup"><span data-stu-id="c22b8-410">When an ISCPBatchBolt instance is created, it will get hello `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from hello input parms */
        if (parms.ContainsKey(Constants.STORM_TX_ATTEMPT))
        {
            StormTxAttempt txAttempt = (StormTxAttempt)parms[Constants.STORM_TX_ATTEMPT];
            return new CountSum(ctx, txAttempt);
        }
        else
        {
            throw new Exception("null txAttempt");
        }
    }

<span data-ttu-id="c22b8-411">Gdy `FinishBatch()` po wywołaniu hello `lastCommittedTxId` będzie aktualizacji, jeśli nie jest transakcją powtórzony.</span><span class="sxs-lookup"><span data-stu-id="c22b8-411">When `FinishBatch()` is called, hello `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update hello toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="c22b8-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="c22b8-412">HybridTopology</span></span>
<span data-ttu-id="c22b8-413">Ta topologia zawiera elementów Spout Java i C\# Bolt.</span><span class="sxs-lookup"><span data-stu-id="c22b8-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="c22b8-414">Używa ona hello domyślnej serializacji i deserializacji implementacji dostarczonych przez punkt połączenia usługi platformy.</span><span class="sxs-lookup"><span data-stu-id="c22b8-414">It uses hello default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="c22b8-415">Użyj ref hello **HybridTopology.spec** w **przykłady\\HybridTopology** folder szczegółów specyfikacji pliku hello, i **SubmitTopology.bat** jak klasy Java toospecify.</span><span class="sxs-lookup"><span data-stu-id="c22b8-415">Please ref hello **HybridTopology.spec** in **examples\\HybridTopology** folder for hello spec file details, and **SubmitTopology.bat** for how toospecify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="c22b8-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="c22b8-416">SCPHostDemo</span></span>
<span data-ttu-id="c22b8-417">W tym przykładzie jest hello taki sam jak HelloWorld w zasadzie.</span><span class="sxs-lookup"><span data-stu-id="c22b8-417">This example is hello same as HelloWorld in essence.</span></span> <span data-ttu-id="c22b8-418">Witaj tylko różnica polega na kod użytkownika hello jest skompilowana jako biblioteki DLL, a topologia hello jest przesyłany za pomocą SCPHost.exe.</span><span class="sxs-lookup"><span data-stu-id="c22b8-418">hello only difference is that hello user code is compiled as DLL and hello topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="c22b8-419">Aby uzyskać dokładniejsze objaśnienie, zapoznaj się z sekcji hello ref "Punkt połączenia usługi hosta tryb".</span><span class="sxs-lookup"><span data-stu-id="c22b8-419">Please ref hello section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c22b8-420">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c22b8-420">Next Steps</span></span>
<span data-ttu-id="c22b8-421">Przykłady topologii Storm utworzone przy użyciu połączenia usługi zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c22b8-421">For examples of Storm topologies created using SCP, see hello following:</span></span>

* [<span data-ttu-id="c22b8-422">Tworzenie topologii C# dla Apache Storm w usłudze HDInsight przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c22b8-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="c22b8-423">Zdarzenia procesu z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="c22b8-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="c22b8-424">Tworzenie wielu strumieni danych w topologii Storm C#</span><span class="sxs-lookup"><span data-stu-id="c22b8-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="c22b8-425">Użyj usługi Power Bi toovisualize danych od topologii Storm</span><span class="sxs-lookup"><span data-stu-id="c22b8-425">Use Power Bi toovisualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="c22b8-426">Przetwarzania danych czujnika vehicle z usługi Event Hubs za pomocą Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="c22b8-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="c22b8-427">Wyodrębniania, przekształcania i ładowania (ETL) z usługi Azure Event Hubs tooHBase</span><span class="sxs-lookup"><span data-stu-id="c22b8-427">Extract, Transform, and Load (ETL) from Azure Event Hubs tooHBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="c22b8-428">Korelowanie zdarzeń za pomocą Storm i bazy danych HBase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="c22b8-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)

