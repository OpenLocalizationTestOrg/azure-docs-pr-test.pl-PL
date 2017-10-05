---
title: "Podręcznik programowania SCP.NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać SCP.NET do tworzenia. Na podstawie NET topologii Storm do za pomocą Storm w usłudze HDInsight."
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
ms.openlocfilehash: 3d76aebd2a1fd729c8e0639e6afcbde4c3fb752b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="c2824-103">Podręcznik programowania punkt połączenia usługi</span><span class="sxs-lookup"><span data-stu-id="c2824-103">SCP programming guide</span></span>
<span data-ttu-id="c2824-104">Punkt połączenia usługi jest platformę do tworzenia w czasie rzeczywistym, niezawodnych, spójne i wysoką wydajność przetwarzania danych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2824-104">SCP is a platform to build real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="c2824-105">Jest ona wbudowana nad [Apache Storm](http://storm.incubator.apache.org/) — systemu projektowania Wspólnot OSS przetwarzania strumienia.</span><span class="sxs-lookup"><span data-stu-id="c2824-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by the OSS communities.</span></span> <span data-ttu-id="c2824-106">STORM jest zaprojektowana przez Nathan Marz i otwórz kwerendą źródłową Twitter.</span><span class="sxs-lookup"><span data-stu-id="c2824-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="c2824-107">Jest przeprowadzana z zastosowaniem [Apache ZooKeeper](http://zookeeper.apache.org/), inny projekt Apache w celu włączenia wysoce niezawodne rozproszone Zarządzanie koordynacji i stanu.</span><span class="sxs-lookup"><span data-stu-id="c2824-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project to enable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="c2824-108">Nie tylko projektu SCP systemie Storm w systemie Windows, ale również projekt został dodany rozszerzenia i dostosowania dla ekosystemu systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c2824-108">Not only the SCP project ported Storm on Windows but also the project added extensions and customization for the Windows ecosystem.</span></span> <span data-ttu-id="c2824-109">Rozszerzenia .NET środowisko dewelopera i bibliotek, dostosowywania zawiera wdrażania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c2824-109">The extensions include .NET developer experience, and libraries, the customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="c2824-110">Rozszerzenie i dostosowanie odbywa się w taki sposób, że firma Microsoft nie ma potrzeby rozwidlania projektów OSS i firma Microsoft może korzystać z ekosystemami pochodnej, rozszerzający Storm.</span><span class="sxs-lookup"><span data-stu-id="c2824-110">The extension and customization is done in such a way that we do not need to fork the OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="c2824-111">Przetwarzanie modelu</span><span class="sxs-lookup"><span data-stu-id="c2824-111">Processing model</span></span>
<span data-ttu-id="c2824-112">Dane w punkt połączenia usługi jest modelowana jako ciągłe strumienie spójnych kolekcji.</span><span class="sxs-lookup"><span data-stu-id="c2824-112">The data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="c2824-113">Zwykle krotki przepływać do niektórych kolejki najpierw, a następnie pobrana i przekształcenia przez hostowaną wewnątrz topologii Storm logiki biznesowej, koniec dane wyjściowe może być przekazywane w potoku jako krotek do innego systemu SCP lub zostać zatwierdzone do magazynów, takich jak rozproszonego systemu plików lub baz danych Podobnie jak SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c2824-113">Typically the tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally the output could be piped as tuples to another SCP system, or be committed to stores like distributed file system or databases like SQL Server.</span></span>

![Diagram kolejki podawania danych do przetwarzania, które źródeł danych magazynu danych](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="c2824-115">Topologia aplikacji Storm, definiuje Graf obliczeń.</span><span class="sxs-lookup"><span data-stu-id="c2824-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="c2824-116">Każdy węzeł w topologii zawiera logikę przetwarzania i łącza między węzłami Oznaczanie przepływu danych.</span><span class="sxs-lookup"><span data-stu-id="c2824-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="c2824-117">Węzły można wstawić danych wejściowych do topologii są nazywane elementach Spout, które mogą być używane do serii danych.</span><span class="sxs-lookup"><span data-stu-id="c2824-117">The nodes to inject input data into the topology are called Spouts, which can be used to sequence the data.</span></span> <span data-ttu-id="c2824-118">Dane wejściowe może znajdować się w plików dzienników, transakcyjne bazy danych licznika wydajności systemu itp. Węzły z obu przepływów danych wejściowych i wyjściowych są nazywane elementów Bolt, które filtrowanie rzeczywiste dane i wybór oraz agregacji.</span><span class="sxs-lookup"><span data-stu-id="c2824-118">The input data could reside in file logs, transactional database, system performance counter etc. The nodes with both input and output data flows are called Bolts, which do the actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="c2824-119">Punkt połączenia usługi obsługuje starań w najmniej jednokrotne, a dokładnie — raz przetwarzania danych.</span><span class="sxs-lookup"><span data-stu-id="c2824-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="c2824-120">W przypadku przesyłania strumieniowego przetwarzania aplikacji rozproszonej różne błędy może się tak zdarzyć podczas przetwarzania danych, takich jak awaria sieci, błąd maszyny lub błąd kodu użytkownika itd. Przetwarzanie w najmniej jednokrotne gwarantuje, że wszystkie dane będą przetwarzane przez odtwarzanie automatycznie tych samych danych, gdy błąd występuje co najmniej raz.</span><span class="sxs-lookup"><span data-stu-id="c2824-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically the same data when error happens.</span></span> <span data-ttu-id="c2824-121">Przetwarzanie w najmniej jednokrotne jest proste i niezawodne i odpowiada także w wielu aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="c2824-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="c2824-122">Jednak gdy aplikacja wymaga dokładnego zliczanie, na przykład przetwarzania na najmniej jednokrotne jest niewystarczająca, ponieważ te same dane potencjalnie może zostać odtworzone w topologii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2824-122">However, when the application requires exact counting, for example, at-least-once processing is insufficient since the same data could potentially be played in the application topology.</span></span> <span data-ttu-id="c2824-123">W takim przypadku, dokładnie-po przetwarzania zaprojektowano w celu upewnij się, że wynik jest poprawna, nawet jeśli dane mogą być odtwarzany i przetwarzane wiele razy.</span><span class="sxs-lookup"><span data-stu-id="c2824-123">In that case, exactly-once processing is designed to make sure the result is correct even when the data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="c2824-124">Punkt połączenia usługi umożliwia deweloperom platformy .NET opracowywania aplikacji procesu danych czasu rzeczywistego podczas wykorzystać maszyny wirtualnej Java (JVM) na podstawie Storm w obszarze pokrycia.</span><span class="sxs-lookup"><span data-stu-id="c2824-124">SCP enables .NET developers to develop real time data process applications while leverage the Java Virtual Machine (JVM) based Storm under the cover.</span></span> <span data-ttu-id="c2824-125">.NET i JVM komunikują się za pośrednictwem lokalnego gniazda TCP.</span><span class="sxs-lookup"><span data-stu-id="c2824-125">The .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="c2824-126">Zasadniczo każdego Spout/Bolt jest para procesu .net/Java, gdzie logikę użytkownika działa w procesie .net jako dodatek.</span><span class="sxs-lookup"><span data-stu-id="c2824-126">Basically each Spout/Bolt is a .Net/Java process pair, where the user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="c2824-127">Do tworzenia aplikacji programu przetwarzania danych na górze punkt połączenia usługi, potrzebne jest wykonanie kilku kroków:</span><span class="sxs-lookup"><span data-stu-id="c2824-127">To build a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="c2824-128">Projektowanie i implementowanie elementach Spout ściągania danych z kolejki.</span><span class="sxs-lookup"><span data-stu-id="c2824-128">Design and implement the Spouts to pull in data from queue.</span></span>
* <span data-ttu-id="c2824-129">Projektowanie i implementowanie elementów Bolt do przetwarzania danych wejściowych i Zapisz danych zewnętrzne magazyny, takie jak bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c2824-129">Design and implement Bolts to process the input data, and save data to external stores such as Database.</span></span>
* <span data-ttu-id="c2824-130">Projektowanie topologii, przesyłania, a następnie uruchom topologii.</span><span class="sxs-lookup"><span data-stu-id="c2824-130">Design the topology, then submit and run the topology.</span></span> <span data-ttu-id="c2824-131">Topologia definiuje wierzchołki i dane między wierzchołków.</span><span class="sxs-lookup"><span data-stu-id="c2824-131">The topology defines vertexes and the data flows between the vertexes.</span></span> <span data-ttu-id="c2824-132">Punkt połączenia usługi otrzymuje specyfikację topologii i wdrożyć ją na klaster Storm, w którym każdy wierzchołek jest uruchamiany w jednym węźle logiczne.</span><span class="sxs-lookup"><span data-stu-id="c2824-132">SCP will take the topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="c2824-133">Tryb failover i skalowanie będzie można wybrać ofertę z harmonogramu zadań systemu Storm.</span><span class="sxs-lookup"><span data-stu-id="c2824-133">The failover and scaling will be taken care of by the Storm task scheduler.</span></span>

<span data-ttu-id="c2824-134">Ten dokument użyje proste przykłady przechodzenia przez sposób tworzenia aplikacji przetwarzania danych z punktu połączenia usługi.</span><span class="sxs-lookup"><span data-stu-id="c2824-134">This document will use some simple examples to walk through how to build data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="c2824-135">Interfejs wtyczki punkt połączenia usługi</span><span class="sxs-lookup"><span data-stu-id="c2824-135">SCP Plugin Interface</span></span>
<span data-ttu-id="c2824-136">Wtyczki punkt połączenia usługi (lub aplikacji) są autonomiczne plików exe, można jednocześnie uruchomić w programie Visual Studio fazie projektowania, które można podłączyć do potoku Storm po wdrożeniu w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="c2824-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during the development phase, and be plugged into the Storm pipeline after deployment in production.</span></span> <span data-ttu-id="c2824-137">Pisanie wtyczki punkt połączenia usługi jest w taki sam jak zapisywania wszelkich innych standardowych aplikacji systemu Windows konsoli.</span><span class="sxs-lookup"><span data-stu-id="c2824-137">Writing the SCP plugin is just the same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="c2824-138">Platforma SCP.NET deklaruje niektórych interfejs dla spout/bolt i kod wtyczki użytkownika należy zaimplementować te interfejsy.</span><span class="sxs-lookup"><span data-stu-id="c2824-138">SCP.NET platform declares some interface for spout/bolt, and the user plugin code should implement these interfaces.</span></span> <span data-ttu-id="c2824-139">Głównym celem projektu tego jest to, czy użytkownik może skupić się na ich własnych warunki biznesowe logiczne i pozostawienie innymi mają być obsługiwane przez platformę SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="c2824-139">The main purpose of this design is that the user can focus on their own business logics, and leaving other things to be handled by SCP.NET platform.</span></span>

<span data-ttu-id="c2824-140">Kod użytkownika wtyczki powinny implementować jeden z następujących typów interfejsów, zależy od tego, czy topologia jest transakcyjna lub nietransakcyjna i określa, czy składnik jest spout lub bolt.</span><span class="sxs-lookup"><span data-stu-id="c2824-140">The user plugin code should implement one of the followings interfaces, depends on whether the topology is transactional or non-transactional, and whether the component is spout or bolt.</span></span>

* <span data-ttu-id="c2824-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="c2824-141">ISCPSpout</span></span>
* <span data-ttu-id="c2824-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="c2824-142">ISCPBolt</span></span>
* <span data-ttu-id="c2824-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="c2824-143">ISCPTxSpout</span></span>
* <span data-ttu-id="c2824-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="c2824-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="c2824-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="c2824-145">ISCPPlugin</span></span>
<span data-ttu-id="c2824-146">ISCPPlugin jest wspólny interfejs dla wszystkich rodzajów wtyczek.</span><span class="sxs-lookup"><span data-stu-id="c2824-146">ISCPPlugin is the common interface for all kinds of plugins.</span></span> <span data-ttu-id="c2824-147">Obecnie jest interfejsem zastępczego.</span><span class="sxs-lookup"><span data-stu-id="c2824-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="c2824-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="c2824-148">ISCPSpout</span></span>
<span data-ttu-id="c2824-149">ISCPSpout jest interfejsem spout nietransakcyjnej.</span><span class="sxs-lookup"><span data-stu-id="c2824-149">ISCPSpout is the interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="c2824-150">Gdy `NextTuple()` jest nazywany C\# jeden lub więcej krotek można emitowanie kodu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c2824-150">When `NextTuple()` is called, the C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="c2824-151">Jeśli nie ma nic do emisji, ta metoda powinna zwrócić bez emitowanie żadnych czynności.</span><span class="sxs-lookup"><span data-stu-id="c2824-151">If there is nothing to emit, this method should return without emitting anything.</span></span> <span data-ttu-id="c2824-152">Należy zauważyć, że `NextTuple()`, `Ack()`, i `Fail()` są wszystkie wywoływane w pętli ścisłej w jednym wątku w języku C\# procesu.</span><span class="sxs-lookup"><span data-stu-id="c2824-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="c2824-153">Nie ma żadnych krotek, aby emitować, jest uprzejmy uśpienia NextTuple o krótkim czasie (na przykład 10 ms) w celu są używane zbyt dużo Procesora.</span><span class="sxs-lookup"><span data-stu-id="c2824-153">When there are no tuples to emit, it is courteous to have NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="c2824-154">`Ack()`i `Fail()` można wywołać tylko wtedy, gdy mechanizmu potwierdzenia jest włączone w specyfikacji pliku.</span><span class="sxs-lookup"><span data-stu-id="c2824-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="c2824-155">`seqId` Służy do identyfikowania spójnej kolekcji, który jest prześledzone lub nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="c2824-155">The `seqId` is used to identify the tuple which is acked or failed.</span></span> <span data-ttu-id="c2824-156">Dlatego po włączeniu potwierdzenia w nietransakcyjnej topologii w Spout należy użyć następujących funkcji emitowanie:</span><span class="sxs-lookup"><span data-stu-id="c2824-156">So if ack is enabled in non-transactional topology, the following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="c2824-157">Jeśli potwierdzenie nie jest obsługiwany w topologii nietransakcyjnej `Ack()` i `Fail()` może pozostać puste funkcji.</span><span class="sxs-lookup"><span data-stu-id="c2824-157">If ack is not supported in non-transactional topology, the `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="c2824-158">`parms` Parametry wejściowe w te funkcje są po prostu pusty słownik, są one zarezerwowane do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="c2824-158">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="c2824-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="c2824-159">ISCPBolt</span></span>
<span data-ttu-id="c2824-160">ISCPBolt jest interfejsem bolt nietransakcyjnej.</span><span class="sxs-lookup"><span data-stu-id="c2824-160">ISCPBolt is the interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="c2824-161">Po udostępnieniu nowej krotki `Execute()` zostanie wywołana funkcja go przetworzyć.</span><span class="sxs-lookup"><span data-stu-id="c2824-161">When new tuple is available, the `Execute()` function will be called to process it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="c2824-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="c2824-162">ISCPTxSpout</span></span>
<span data-ttu-id="c2824-163">ISCPTxSpout jest interfejsem spout transakcyjnych.</span><span class="sxs-lookup"><span data-stu-id="c2824-163">ISCPTxSpout is the interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="c2824-164">Podobnie jak ich nietransakcyjnej zaradczych strony `NextTx()`, `Ack()`, i `Fail()` są wszystkie wywoływane w pętli ścisłej w jednym wątku w języku C\# procesu.</span><span class="sxs-lookup"><span data-stu-id="c2824-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="c2824-165">Jeśli nie ma żadnych danych do wysyłania, jest uprzejmy mają `NextTx` uśpienia przez krótki czas (10 ms) w celu są używane zbyt dużo Procesora.</span><span class="sxs-lookup"><span data-stu-id="c2824-165">When there are no data to emit, it is courteous to have `NextTx` sleep for a short amount of time (10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="c2824-166">`NextTx()`jest wywoływana, aby rozpocząć nowej transakcji, a parametr out `seqId` służy do identyfikowania transakcji, która jest również używana w `Ack()` i `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="c2824-166">`NextTx()` is called to start a new transaction, the out parameter `seqId` is used to identify the transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="c2824-167">W `NextTx()`, użytkownik może emitować danych do strony Java.</span><span class="sxs-lookup"><span data-stu-id="c2824-167">In `NextTx()`, user can emit data to Java side.</span></span> <span data-ttu-id="c2824-168">Dane będą przechowywane w dozorcy do obsługi powtarzania.</span><span class="sxs-lookup"><span data-stu-id="c2824-168">The data will be stored in ZooKeeper to support replay.</span></span> <span data-ttu-id="c2824-169">Ponieważ pojemność dozorcy jest bardzo ograniczona, użytkownik powinien Emituj tylko metadane, nie zbiorcze danych transakcyjnych spout.</span><span class="sxs-lookup"><span data-stu-id="c2824-169">Because the capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="c2824-170">STORM będzie odtwarzana w transakcji automatycznie w przypadku niepowodzenia to `Fail()` nie powinna być wywoływana w przypadku normalnych.</span><span class="sxs-lookup"><span data-stu-id="c2824-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="c2824-171">Ale jeśli punkt połączenia usługi można sprawdzić metadanych emitowane przez transakcyjne spout, może wywołać `Fail()` Jeśli metadanych jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="c2824-171">But if SCP can check the metadata emitted by transactional spout, it can call `Fail()` when the metadata is invalid.</span></span>

<span data-ttu-id="c2824-172">`parms` Parametry wejściowe w te funkcje są po prostu pusty słownik, są one zarezerwowane do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="c2824-172">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="c2824-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="c2824-173">ISCPBatchBolt</span></span>
<span data-ttu-id="c2824-174">ISCPBatchBolt jest interfejs dla transakcyjnego bolt.</span><span class="sxs-lookup"><span data-stu-id="c2824-174">ISCPBatchBolt is the interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="c2824-175">`Execute()`jest wywoływana po nowej krotki otrzymywanych elementy bolt.</span><span class="sxs-lookup"><span data-stu-id="c2824-175">`Execute()` is called when there is new tuple arriving at the bolt.</span></span> <span data-ttu-id="c2824-176">`FinishBatch()`jest wywoływana po zakończeniu tej transakcji.</span><span class="sxs-lookup"><span data-stu-id="c2824-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="c2824-177">`parms` Parametr wejściowy jest zarezerwowany do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="c2824-177">The `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="c2824-178">Topologia transakcyjne jest ważne pojęcia — `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="c2824-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="c2824-179">Składa się z dwóch pól `TxId` i `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="c2824-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="c2824-180">`TxId`Służy do identyfikowania określonej transakcji, a dla danej transakcji, może mieć wielu prób transakcji nie powiedzie się i jest odtwarzany.</span><span class="sxs-lookup"><span data-stu-id="c2824-180">`TxId` is used to identify a specific transaction, and for a given transaction, there may be multiple attempt if the transaction fails and is replayed.</span></span> <span data-ttu-id="c2824-181">SCP.NET nowych będzie inny obiekt ISCPBatchBolt przetwarzania każdego `StormTxAttempt`, po prostu jak czego Storm w języku Java po stronie.</span><span class="sxs-lookup"><span data-stu-id="c2824-181">SCP.NET will new a different ISCPBatchBolt object to process each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="c2824-182">Celem tego projektu jest obsługuje transakcji równoległych przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="c2824-182">The purpose of this design is to support parallel transactions processing.</span></span> <span data-ttu-id="c2824-183">Użytkownik należy go przechowywać w pamiętać, że jeśli próba transakcji jest zakończone, odpowiedni obiekt ISCPBatchBolt zostaną usunięte i bezużytecznych.</span><span class="sxs-lookup"><span data-stu-id="c2824-183">User should keep it in mind that if transaction attempt is finished, the corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="c2824-184">Model obiektu</span><span class="sxs-lookup"><span data-stu-id="c2824-184">Object Model</span></span>
<span data-ttu-id="c2824-185">SCP.NET udostępnia prosty zestaw obiektów kluczy dla deweloperów do programu z.</span><span class="sxs-lookup"><span data-stu-id="c2824-185">SCP.NET also provides a simple set of key objects for developers to program with.</span></span> <span data-ttu-id="c2824-186">Są one **kontekstu**, **stan klientów**, i **SCPRuntime**.</span><span class="sxs-lookup"><span data-stu-id="c2824-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="c2824-187">Będą one omówione w pozostałej części tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="c2824-187">They will be discussed in the rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="c2824-188">Kontekst</span><span class="sxs-lookup"><span data-stu-id="c2824-188">Context</span></span>
<span data-ttu-id="c2824-189">Kontekst udostępnia środowisko uruchomionej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2824-189">Context provides a running environment to the application.</span></span> <span data-ttu-id="c2824-190">Każde wystąpienie ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) ma odpowiednie wystąpienia kontekstu.</span><span class="sxs-lookup"><span data-stu-id="c2824-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="c2824-191">Funkcje zapewniane przez kontekst można podzielić na dwie części: (1 w statycznej części, które jest dostępne w całej C\# przetwarzać, (2 części dynamicznej, która jest dostępna tylko dla określonego wystąpienia kontekstu.</span><span class="sxs-lookup"><span data-stu-id="c2824-191">The functionality provided by Context can be divided into two parts: (1) the static part which is available in the whole C\# process, (2) the dynamic part which is only available for the specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="c2824-192">Statycznej części</span><span class="sxs-lookup"><span data-stu-id="c2824-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="c2824-193">`Logger`podano w celu dziennika.</span><span class="sxs-lookup"><span data-stu-id="c2824-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="c2824-194">`pluginType`Służy do wskazywania typu dodatek c\# procesu.</span><span class="sxs-lookup"><span data-stu-id="c2824-194">`pluginType` is used to indicate the plugin type of the C\# process.</span></span> <span data-ttu-id="c2824-195">Jeśli C\# proces jest uruchomiony w trybie lokalnym testu (bez Java), jest typu wtyczki `SCP_NET_LOCAL`.</span><span class="sxs-lookup"><span data-stu-id="c2824-195">If the C\# process is run in local test mode (without Java), the plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="c2824-196">`Config`podano można pobrać parametrów konfiguracji po stronie Java.</span><span class="sxs-lookup"><span data-stu-id="c2824-196">`Config` is provided to get configuration parameters from Java side.</span></span> <span data-ttu-id="c2824-197">Parametry są przekazywane z Java strony po C\# dodatek został zainicjowany.</span><span class="sxs-lookup"><span data-stu-id="c2824-197">The parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="c2824-198">`Config` Parametry są podzielone na dwie części: `stormConf` i `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="c2824-198">The `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="c2824-199">`stormConf`jest parametrów zdefiniowanych Storm i `pluginConf` jest parametrów zdefiniowanych przez punkt połączenia usługi.</span><span class="sxs-lookup"><span data-stu-id="c2824-199">`stormConf` is parameters defined by Storm and `pluginConf` is the parameters defined by SCP.</span></span> <span data-ttu-id="c2824-200">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c2824-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="c2824-201">`TopologyContext`podano pobrać kontekstu topologii, jest najbardziej przydatny w przypadku składników z wielu równoległości.</span><span class="sxs-lookup"><span data-stu-id="c2824-201">`TopologyContext` is provided to get the topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="c2824-202">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="c2824-202">Here is an example:</span></span>

    //demo how to get TopologyContext info
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

### <a name="dynamic-part"></a><span data-ttu-id="c2824-203">Części dynamicznej</span><span class="sxs-lookup"><span data-stu-id="c2824-203">Dynamic Part</span></span>
<span data-ttu-id="c2824-204">Następujące interfejsy są odpowiednie do wystąpienia kontekstu.</span><span class="sxs-lookup"><span data-stu-id="c2824-204">The following interfaces are pertinent to a certain Context instance.</span></span> <span data-ttu-id="c2824-205">Wystąpienie kontekstu jest tworzony przez platformę SCP.NET i przekazane do kodu użytkownika:</span><span class="sxs-lookup"><span data-stu-id="c2824-205">The Context instance is created by SCP.NET platform and passed to the user code:</span></span>

    // Declare the Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple to default stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple to the specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="c2824-206">Do obsługi potwierdzenia nietransakcyjnej spout podano następującą metodę:</span><span class="sxs-lookup"><span data-stu-id="c2824-206">For non-transactional spout supporting ack, the following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="c2824-207">Dla obsługi potwierdzenia nietransakcyjnej bolt, należy go jawnie `Ack()` lub `Fail()` odebrała spójnej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="c2824-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` the tuple it received.</span></span> <span data-ttu-id="c2824-208">I podczas emitowania nowe spójnej kolekcji, należy także określić kotwic nowe spójnej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="c2824-208">And when emitting new tuple, it must also specify the anchors of the new tuple.</span></span> <span data-ttu-id="c2824-209">Udostępniono następujące metody.</span><span class="sxs-lookup"><span data-stu-id="c2824-209">The following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="c2824-210">Stan klientów</span><span class="sxs-lookup"><span data-stu-id="c2824-210">StateStore</span></span>
<span data-ttu-id="c2824-211">`StateStore`udostępnia usługi metadanych, generowanie monotoniczna sekwencji i koordynacji bez oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="c2824-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="c2824-212">Abstrakcje wyższego poziomu współbieżności rozproszonej mogą być wbudowane w `StateStore`, w tym rozproszonej blokad, kolejek rozproszonych bariery i transakcji usługi.</span><span class="sxs-lookup"><span data-stu-id="c2824-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="c2824-213">Punkt połączenia usługi, aplikacje mogą używać `State` obiekt, aby zachować niektóre informacje w dozorcy, szczególnie w przypadku topologii transakcyjnych.</span><span class="sxs-lookup"><span data-stu-id="c2824-213">SCP applications may use the `State` object to persist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="c2824-214">Wykonywanie, dzięki czemu transakcyjne spout ulegnie awarii, uruchom ponownie może pobrać niezbędne informacje z dozorcy i ponownie uruchomić potoku.</span><span class="sxs-lookup"><span data-stu-id="c2824-214">Doing so, if transactional spout crashes and restart, it can retrieve the necessary information from ZooKeeper and restart the pipeline.</span></span>

<span data-ttu-id="c2824-215">`StateStore` Obiekt ma głównie tych metod:</span><span class="sxs-lookup"><span data-stu-id="c2824-215">The `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method to retrieve a state store of the given path and connStr 
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
    /// Get all the States in the StateStore
    /// </summary>
    /// <returns>All the States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all the committed states
    /// </summary>
    /// <returns>Registries contain the Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all the Aborted State in the StateStore
    /// </summary>
    /// <returns>Registries contain the Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of the State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="c2824-216">`State` Obiekt ma głównie tych metod:</span><span class="sxs-lookup"><span data-stu-id="c2824-216">The `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set the status of the state object to commit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set the status of the state object to abort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under the give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get the attribute value associated with the given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="c2824-217">Dla `Commit()` metody, gdy simpleMode ma ustawioną wartość true, po prostu usunie odpowiedniego ZNode w dozorcy.</span><span class="sxs-lookup"><span data-stu-id="c2824-217">For the `Commit()` method, when simpleMode is set to true, it will simply delete the corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="c2824-218">W przeciwnym razie spowoduje usunięcie bieżącego ZNode i dodanie nowego węzła w zatwierdzone\_ścieżki.</span><span class="sxs-lookup"><span data-stu-id="c2824-218">Otherwise, it will delete the current ZNode, and adding a new node in the COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="c2824-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="c2824-219">SCPRuntime</span></span>
<span data-ttu-id="c2824-220">SCPRuntime udostępnia dwie metody.</span><span class="sxs-lookup"><span data-stu-id="c2824-220">SCPRuntime provides the following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="c2824-221">`Initialize()`Służy do inicjowania środowiska uruchomieniowego punkt połączenia usługi.</span><span class="sxs-lookup"><span data-stu-id="c2824-221">`Initialize()` is used to initialize the SCP runtime environment.</span></span> <span data-ttu-id="c2824-222">W przypadku tej metody C\# procesu będą łączyć się po stronie Java i pobiera parametry konfiguracji i topologii kontekstu.</span><span class="sxs-lookup"><span data-stu-id="c2824-222">In this method, the C\# process will connect to the Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="c2824-223">`LaunchPlugin()`Służy do zaczną działać poza pętlą przetwarzania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="c2824-223">`LaunchPlugin()` is used to kick off the message processing loop.</span></span> <span data-ttu-id="c2824-224">W tym pętli C\# wtyczki będą otrzymywać wiadomości formularza po stronie Java (w tym sygnały krotek i sterowania), a następnie przetwarzanie komunikatów, być może podczas wywoływania metody interfejsu Podaj przez kod użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c2824-224">In this loop, the C\# plugin will receive messages form Java side (including tuples and control signals), and then process the messages, perhaps calling the interface method provide by the user code.</span></span> <span data-ttu-id="c2824-225">Parametr wejściowy dla metody `LaunchPlugin()` jest delegata, który może zwracać obiekt, który implementuje interfejs ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.</span><span class="sxs-lookup"><span data-stu-id="c2824-225">The input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="c2824-226">Dla ISCPBatchBolt, można pobrać `StormTxAttempt` z `parms`i przy jego użyciu ocenić, czy jest ono próbę powtórzony.</span><span class="sxs-lookup"><span data-stu-id="c2824-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it to judge whether it is a replayed attempt.</span></span> <span data-ttu-id="c2824-227">Jest to zazwyczaj wykonywane na bolt zatwierdzania i zostało to przedstawione w `HelloWorldTx` przykład.</span><span class="sxs-lookup"><span data-stu-id="c2824-227">This is usually done at the commit bolt, and it is demonstrated in the `HelloWorldTx` example.</span></span>

<span data-ttu-id="c2824-228">Ogólnie rzecz biorąc wtyczek SCP może działać w dwóch trybach tutaj:</span><span class="sxs-lookup"><span data-stu-id="c2824-228">Generally speaking, the SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="c2824-229">Tryb lokalnego testu: W tym trybie wtyczek punkt połączenia usługi (C\# kod użytkownika) uruchom w programie Visual Studio w fazie projektowania.</span><span class="sxs-lookup"><span data-stu-id="c2824-229">Local Test Mode: In this mode, the SCP plugins (the C\# user code) run inside Visual Studio during the development phase.</span></span> <span data-ttu-id="c2824-230">`LocalContext`można w tym trybie, który zapewnia metody do serializacji emitowany krotek do lokalnych plików i odczytania ich pamięci.</span><span class="sxs-lookup"><span data-stu-id="c2824-230">`LocalContext` can be used in this mode, which provides method to serialize the emitted tuples to local files, and read them back to memory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="c2824-231">Tryb regularnych: W tym trybie wtyczek punkt połączenia usługi będą uruchamiane przez proces java storm.</span><span class="sxs-lookup"><span data-stu-id="c2824-231">Regular Mode: In this mode, the SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="c2824-232">Oto przykład uruchamiania SCP wtyczki:</span><span class="sxs-lookup"><span data-stu-id="c2824-232">Here is an example of launching SCP plugin:</span></span>
   
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
            /* Setting the environment variable here can change the log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="c2824-233">Topologia specyfikacja języka</span><span class="sxs-lookup"><span data-stu-id="c2824-233">Topology Specification Language</span></span>
<span data-ttu-id="c2824-234">Specyfikacja topologii punkt połączenia usługi jest domeny określonego języka dla zawierająca opis i Konfigurowanie topologii punkt połączenia usługi.</span><span class="sxs-lookup"><span data-stu-id="c2824-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="c2824-235">Jest on oparty na jego Storm Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) i zostanie rozszerzony przez punkt połączenia usługi.</span><span class="sxs-lookup"><span data-stu-id="c2824-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="c2824-236">Specyfikacje topologii można przesyłać bezpośrednio do klastra storm do wykonywania za pośrednictwem ***runspec*** polecenia.</span><span class="sxs-lookup"><span data-stu-id="c2824-236">Topology specifications can be submitted directly to storm cluster for execution via the ***runspec*** command.</span></span>

<span data-ttu-id="c2824-237">SCP.NET ma Dodaj funkcje wykonaj do definiowania transakcyjne topologii:</span><span class="sxs-lookup"><span data-stu-id="c2824-237">SCP.NET has add follow functions to define the Transactional Topology:</span></span>

| <span data-ttu-id="c2824-238">**Nowe funkcje**</span><span class="sxs-lookup"><span data-stu-id="c2824-238">**New Functions**</span></span> | <span data-ttu-id="c2824-239">**Parametry**</span><span class="sxs-lookup"><span data-stu-id="c2824-239">**Parameters**</span></span> | <span data-ttu-id="c2824-240">**Opis**</span><span class="sxs-lookup"><span data-stu-id="c2824-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c2824-241">**TX topolopy**</span><span class="sxs-lookup"><span data-stu-id="c2824-241">**tx-topolopy**</span></span> |<span data-ttu-id="c2824-242">Nazwa topologii</span><span class="sxs-lookup"><span data-stu-id="c2824-242">topology-name</span></span><br /><span data-ttu-id="c2824-243">spout mapy</span><span class="sxs-lookup"><span data-stu-id="c2824-243">spout-map</span></span><br /><span data-ttu-id="c2824-244">bolt mapy</span><span class="sxs-lookup"><span data-stu-id="c2824-244">bolt-map</span></span> |<span data-ttu-id="c2824-245">Zdefiniuj transakcyjne topologii o nazwie topologii &nbsp;spouts mapy definicji, a następnie mapować definicji elementów bolt</span><span class="sxs-lookup"><span data-stu-id="c2824-245">Define a transactional topology with the topology name, &nbsp;spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="c2824-246">**spout-tx — punkt połączenia usługi**</span><span class="sxs-lookup"><span data-stu-id="c2824-246">**scp-tx-spout**</span></span> |<span data-ttu-id="c2824-247">exec — nazwa</span><span class="sxs-lookup"><span data-stu-id="c2824-247">exec-name</span></span><br /><span data-ttu-id="c2824-248">argumentów</span><span class="sxs-lookup"><span data-stu-id="c2824-248">args</span></span><br /><span data-ttu-id="c2824-249">Pola</span><span class="sxs-lookup"><span data-stu-id="c2824-249">fields</span></span> |<span data-ttu-id="c2824-250">Zdefiniuj spout transakcyjnych.</span><span class="sxs-lookup"><span data-stu-id="c2824-250">Define a transactional spout.</span></span> <span data-ttu-id="c2824-251">Zostanie uruchomiony aplikacji z ***nazwa exec*** przy użyciu ***argumentów***.</span><span class="sxs-lookup"><span data-stu-id="c2824-251">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="c2824-252">***Pola*** jest pól danych wyjściowych dla spout</span><span class="sxs-lookup"><span data-stu-id="c2824-252">The ***fields*** is the Output Fields for spout</span></span> |
| <span data-ttu-id="c2824-253">**punkt połączenia usługi tx partii bolt**</span><span class="sxs-lookup"><span data-stu-id="c2824-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="c2824-254">exec — nazwa</span><span class="sxs-lookup"><span data-stu-id="c2824-254">exec-name</span></span><br /><span data-ttu-id="c2824-255">argumentów</span><span class="sxs-lookup"><span data-stu-id="c2824-255">args</span></span><br /><span data-ttu-id="c2824-256">Pola</span><span class="sxs-lookup"><span data-stu-id="c2824-256">fields</span></span> |<span data-ttu-id="c2824-257">Zdefiniuj transakcyjne Bolt partii.</span><span class="sxs-lookup"><span data-stu-id="c2824-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="c2824-258">Zostanie uruchomiony aplikacji z ***nazwa exec*** przy użyciu ***argumentów.***</span><span class="sxs-lookup"><span data-stu-id="c2824-258">It will run the application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="c2824-259">Pola jest pól danych wyjściowych dla bolt.</span><span class="sxs-lookup"><span data-stu-id="c2824-259">The Fields is the Output Fields for bolt.</span></span> |
| <span data-ttu-id="c2824-260">**punkt połączenia usługi tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="c2824-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="c2824-261">exec — nazwa</span><span class="sxs-lookup"><span data-stu-id="c2824-261">exec-name</span></span><br /><span data-ttu-id="c2824-262">argumentów</span><span class="sxs-lookup"><span data-stu-id="c2824-262">args</span></span><br /><span data-ttu-id="c2824-263">Pola</span><span class="sxs-lookup"><span data-stu-id="c2824-263">fields</span></span> |<span data-ttu-id="c2824-264">Zdefiniuj transakcyjne Bolt zatwierdzający.</span><span class="sxs-lookup"><span data-stu-id="c2824-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="c2824-265">Zostanie uruchomiony aplikacji z ***nazwa exec*** przy użyciu ***argumentów***.</span><span class="sxs-lookup"><span data-stu-id="c2824-265">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="c2824-266">***Pola*** jest pól danych wyjściowych dla bolt</span><span class="sxs-lookup"><span data-stu-id="c2824-266">The ***fields*** is the Output Fields for bolt</span></span> |
| <span data-ttu-id="c2824-267">**nontx topolopy**</span><span class="sxs-lookup"><span data-stu-id="c2824-267">**nontx-topolopy**</span></span> |<span data-ttu-id="c2824-268">Nazwa topologii</span><span class="sxs-lookup"><span data-stu-id="c2824-268">topology-name</span></span><br /><span data-ttu-id="c2824-269">spout mapy</span><span class="sxs-lookup"><span data-stu-id="c2824-269">spout-map</span></span><br /><span data-ttu-id="c2824-270">bolt mapy</span><span class="sxs-lookup"><span data-stu-id="c2824-270">bolt-map</span></span> |<span data-ttu-id="c2824-271">Zdefiniuj topologię nietransakcyjne o nazwie topologii&nbsp; spouts mapy definicji, a następnie mapować definicji elementów bolt</span><span class="sxs-lookup"><span data-stu-id="c2824-271">Define a nontransactional topology with the topology name,&nbsp; spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="c2824-272">**spout punkt połączenia usługi**</span><span class="sxs-lookup"><span data-stu-id="c2824-272">**scp-spout**</span></span> |<span data-ttu-id="c2824-273">exec — nazwa</span><span class="sxs-lookup"><span data-stu-id="c2824-273">exec-name</span></span><br /><span data-ttu-id="c2824-274">argumentów</span><span class="sxs-lookup"><span data-stu-id="c2824-274">args</span></span><br /><span data-ttu-id="c2824-275">Pola</span><span class="sxs-lookup"><span data-stu-id="c2824-275">fields</span></span><br /><span data-ttu-id="c2824-276">Parametry</span><span class="sxs-lookup"><span data-stu-id="c2824-276">parameters</span></span> |<span data-ttu-id="c2824-277">Zdefiniuj spout nietransakcyjne.</span><span class="sxs-lookup"><span data-stu-id="c2824-277">Define a nontransactional spout.</span></span> <span data-ttu-id="c2824-278">Zostanie uruchomiony aplikacji z ***nazwa exec*** przy użyciu ***argumentów***.</span><span class="sxs-lookup"><span data-stu-id="c2824-278">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="c2824-279">***Pola*** jest pól danych wyjściowych dla spout</span><span class="sxs-lookup"><span data-stu-id="c2824-279">The ***fields*** is the Output Fields for spout</span></span><br /><br /><span data-ttu-id="c2824-280">***Parametry*** jest opcjonalny, używany do określenia niektórych parametrów, takich jak "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="c2824-280">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="c2824-281">**bolt punkt połączenia usługi**</span><span class="sxs-lookup"><span data-stu-id="c2824-281">**scp-bolt**</span></span> |<span data-ttu-id="c2824-282">exec — nazwa</span><span class="sxs-lookup"><span data-stu-id="c2824-282">exec-name</span></span><br /><span data-ttu-id="c2824-283">argumentów</span><span class="sxs-lookup"><span data-stu-id="c2824-283">args</span></span><br /><span data-ttu-id="c2824-284">Pola</span><span class="sxs-lookup"><span data-stu-id="c2824-284">fields</span></span><br /><span data-ttu-id="c2824-285">Parametry</span><span class="sxs-lookup"><span data-stu-id="c2824-285">parameters</span></span> |<span data-ttu-id="c2824-286">Zdefiniuj nietransakcyjne Bolt.</span><span class="sxs-lookup"><span data-stu-id="c2824-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="c2824-287">Zostanie uruchomiony aplikacji z ***nazwa exec*** przy użyciu ***argumentów***.</span><span class="sxs-lookup"><span data-stu-id="c2824-287">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="c2824-288">***Pola*** jest pól danych wyjściowych dla bolt</span><span class="sxs-lookup"><span data-stu-id="c2824-288">The ***fields*** is the Output Fields for bolt</span></span><br /><br /><span data-ttu-id="c2824-289">***Parametry*** jest opcjonalny, używany do określenia niektórych parametrów, takich jak "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="c2824-289">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="c2824-290">Wykonaj ma SCP.NET kluczy zdefiniowane słowa:</span><span class="sxs-lookup"><span data-stu-id="c2824-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="c2824-291">**Słowa kluczowe**</span><span class="sxs-lookup"><span data-stu-id="c2824-291">**Key Words**</span></span> | <span data-ttu-id="c2824-292">**Opis**</span><span class="sxs-lookup"><span data-stu-id="c2824-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="c2824-293">**: Nazwa**</span><span class="sxs-lookup"><span data-stu-id="c2824-293">**:name**</span></span> |<span data-ttu-id="c2824-294">Zdefiniuj nazwę topologii</span><span class="sxs-lookup"><span data-stu-id="c2824-294">Define the Topology Name</span></span> |
| <span data-ttu-id="c2824-295">**: topologii**</span><span class="sxs-lookup"><span data-stu-id="c2824-295">**:topology**</span></span> |<span data-ttu-id="c2824-296">Zdefiniuj topologię za pomocą funkcji powyżej i kompilacji w tych.</span><span class="sxs-lookup"><span data-stu-id="c2824-296">Define the Topology using the above functions and build in ones.</span></span> |
| <span data-ttu-id="c2824-297">**: p**</span><span class="sxs-lookup"><span data-stu-id="c2824-297">**:p**</span></span> |<span data-ttu-id="c2824-298">Zdefiniuj wskazówka równoległości dla każdego spout lub bolt.</span><span class="sxs-lookup"><span data-stu-id="c2824-298">Define the parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="c2824-299">**: config**</span><span class="sxs-lookup"><span data-stu-id="c2824-299">**:config**</span></span> |<span data-ttu-id="c2824-300">Zdefiniuj parametr skonfigurować lub zaktualizować istniejące</span><span class="sxs-lookup"><span data-stu-id="c2824-300">Define configure parameter or update the existing ones</span></span> |
| <span data-ttu-id="c2824-301">**: schematu**</span><span class="sxs-lookup"><span data-stu-id="c2824-301">**:schema**</span></span> |<span data-ttu-id="c2824-302">Zdefiniuj schemat strumienia.</span><span class="sxs-lookup"><span data-stu-id="c2824-302">Define the Schema of Stream.</span></span> |

<span data-ttu-id="c2824-303">I często używane parametry:</span><span class="sxs-lookup"><span data-stu-id="c2824-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="c2824-304">**Parametr**</span><span class="sxs-lookup"><span data-stu-id="c2824-304">**Parameter**</span></span> | <span data-ttu-id="c2824-305">**Opis**</span><span class="sxs-lookup"><span data-stu-id="c2824-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="c2824-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="c2824-306">**"plugin.name"**</span></span> |<span data-ttu-id="c2824-307">Nazwa pliku exe wtyczki C#</span><span class="sxs-lookup"><span data-stu-id="c2824-307">exe file name of the C# plugin</span></span> |
| <span data-ttu-id="c2824-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="c2824-308">**"plugin.args"**</span></span> |<span data-ttu-id="c2824-309">argumenty wtyczki</span><span class="sxs-lookup"><span data-stu-id="c2824-309">plugin args</span></span> |
| <span data-ttu-id="c2824-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="c2824-310">**"output.schema"**</span></span> |<span data-ttu-id="c2824-311">Schemat danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="c2824-311">Output schema</span></span> |
| <span data-ttu-id="c2824-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="c2824-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="c2824-313">Czy potwierdzenia jest włączone dla topologii nietransakcyjne</span><span class="sxs-lookup"><span data-stu-id="c2824-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="c2824-314">Polecenie runspec zostaną wdrożone razem z usługi bits, jest użycie, takich jak:</span><span class="sxs-lookup"><span data-stu-id="c2824-314">The runspec command will be deployed together with the bits, the usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="c2824-315">***Zasobów dir*** parametr jest opcjonalny, musisz podać go, jeśli chcesz dołączyć C\# aplikacji, a ten katalog będzie zawierać aplikację, zależności i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c2824-315">The ***resource-dir*** parameter is optional, you need to specify it when you want to plug a C\# application, and this directory will contain the application, the dependencies and configurations.</span></span>

<span data-ttu-id="c2824-316">***Ścieżki klasy*** parametr również jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="c2824-316">The ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="c2824-317">Służy do określenia klasy Java, jeśli plik specyfikacji zawiera Java Spout lub Bolt.</span><span class="sxs-lookup"><span data-stu-id="c2824-317">It is used to specify the Java classpath if the spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="c2824-318">Różne funkcje</span><span class="sxs-lookup"><span data-stu-id="c2824-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="c2824-319">Danych wejściowych i wyjściowych schematu deklaracji</span><span class="sxs-lookup"><span data-stu-id="c2824-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="c2824-320">Użytkownik może emitować spójnej kolekcji w języku C\# procesu platformy musi być serializuje spójna kolekcja znajdująca się na byte [], Przenieś stronę Java i Storm przekaże to tuple elementy docelowe.</span><span class="sxs-lookup"><span data-stu-id="c2824-320">The user can emit tuple in C\# process, the platform needs to serialize the tuple into byte[], transfer to Java side, and Storm will transfer this tuple to the targets.</span></span> <span data-ttu-id="c2824-321">W tym samym czasie w składniku podrzędne, C\# proces będzie otrzymywać krotki powrotem po stronie java i przekształcić ją do oryginalnego typów przez platformę, wszystkie czynności są ukryte przez platformę.</span><span class="sxs-lookup"><span data-stu-id="c2824-321">Meanwhile in downstream component, the C\# process will receive tuple back from java side, and convert it to the original types by platform, all these operations are hidden by the Platform.</span></span>

<span data-ttu-id="c2824-322">Do obsługi serializacji i deserializacji, kod użytkownika musi zadeklarować schemat danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c2824-322">To support the serialization and deserialization, user code needs to declare the schema of the inputs and outputs.</span></span>

<span data-ttu-id="c2824-323">Schemat wejścia/wyjścia strumień jest zdefiniowany jako słownik, klucz jest StreamId, a wartość to typy kolumn.</span><span class="sxs-lookup"><span data-stu-id="c2824-323">The input/output stream schema is defined as a dictionary, the key is the StreamId and the value is the Types of the columns.</span></span> <span data-ttu-id="c2824-324">Składnik może mieć wielu strumieni zadeklarowany.</span><span class="sxs-lookup"><span data-stu-id="c2824-324">The component can have multi-streams declared.</span></span>

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


<span data-ttu-id="c2824-325">Obiekt kontekstu mamy następujący interfejs API dodany:</span><span class="sxs-lookup"><span data-stu-id="c2824-325">In Context object, we have the following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="c2824-326">Kod użytkownika, należy się upewnić, krotek wysyłanego przestrzegać schematu zdefiniowane dla tego strumienia lub system zgłosi wyjątek czasu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="c2824-326">User code must make sure the tuples emitted obey the schema defined for that stream, or the system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="c2824-327">Obsługa wielu strumienia</span><span class="sxs-lookup"><span data-stu-id="c2824-327">Multi-Stream Support</span></span>
<span data-ttu-id="c2824-328">Punkt połączenia usługi obsługuje kod użytkownika Emituj lub odebrać z wielu różnych strumieni w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="c2824-328">SCP supports user code to emit or receive from multiple distinct streams at the same time.</span></span> <span data-ttu-id="c2824-329">Obsługa odzwierciedla w kontekście obiektu jako metoda emitowanie korzysta z parametru Identyfikatora strumienia opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="c2824-329">The support reflects in the Context object as the Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="c2824-330">Dodano dwie metody w obiekcie SCP.NET kontekstu.</span><span class="sxs-lookup"><span data-stu-id="c2824-330">Two methods in the SCP.NET Context object have been added.</span></span> <span data-ttu-id="c2824-331">Są one używane do wysyłania spójnej kolekcji lub krotek, aby określić StreamId.</span><span class="sxs-lookup"><span data-stu-id="c2824-331">They are used to emit Tuple or Tuples to specify StreamId.</span></span> <span data-ttu-id="c2824-332">StreamId jest ciągiem i musi być zgodne w obu C\# i użycie definicji topologii.</span><span class="sxs-lookup"><span data-stu-id="c2824-332">The StreamId is a string and it needs to be consistent in both C\# and the Topology Definition Spec.</span></span>

        /* Emit tuple to the specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="c2824-333">Emitowanie strumień nieistniejącego spowoduje wyjątki czasu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="c2824-333">The emitting to a non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="c2824-334">Grupowanie pól</span><span class="sxs-lookup"><span data-stu-id="c2824-334">Fields Grouping</span></span>
<span data-ttu-id="c2824-335">Kompilacji w polach grupowania Strom nie działa prawidłowo w SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="c2824-335">The build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="c2824-336">Po stronie serwera Proxy Java wszystkich typów danych pola są faktycznie byte [], a pola Grupowanie używa typu byte [] obiektu skrótu do wykonania grupowanie.</span><span class="sxs-lookup"><span data-stu-id="c2824-336">On the Java Proxy side, all the fields data types are actually byte[], and the fields grouping uses the byte[] object hash code to perform the grouping.</span></span> <span data-ttu-id="c2824-337">Byte [] obiektu skrótu jest adres tego obiektu w pamięci.</span><span class="sxs-lookup"><span data-stu-id="c2824-337">The byte[] object hash code is the address of this object in memory.</span></span> <span data-ttu-id="c2824-338">To grupowanie będą nieprawidłowe dla dwóch byte [] obiektów, które mają tę samą zawartość, ale nie sam adres.</span><span class="sxs-lookup"><span data-stu-id="c2824-338">So the grouping will be wrong for two byte[] objects that share the same content but not the same address.</span></span>

<span data-ttu-id="c2824-339">SCP.NET dodaje metodę grupowania dostosowany, a zawartość byte [] zostanie użyty do grupowania.</span><span class="sxs-lookup"><span data-stu-id="c2824-339">SCP.NET adds a customized grouping method, and it will use the content of the byte[] to do the grouping.</span></span> <span data-ttu-id="c2824-340">W **SPEC** pliku przypomina składnię:</span><span class="sxs-lookup"><span data-stu-id="c2824-340">In **SPEC** file, the syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="c2824-341">Tutaj</span><span class="sxs-lookup"><span data-stu-id="c2824-341">Here,</span></span>

1. <span data-ttu-id="c2824-342">"punkt połączenia usługi pola group" oznacza "Grupowania pola niestandardowe implementowane przez punkt połączenia usługi".</span><span class="sxs-lookup"><span data-stu-id="c2824-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="c2824-343">": tx"lub":-tx" oznacza, że jeśli jest transakcyjna topologii.</span><span class="sxs-lookup"><span data-stu-id="c2824-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="c2824-344">Potrzebujemy tych informacji, ponieważ indeks początkowy a topologie-tx różni się w tx.</span><span class="sxs-lookup"><span data-stu-id="c2824-344">We need this information since the starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="c2824-345">zestaw hashset identyfikatory pola, począwszy od 0 oznacza [0,1].</span><span class="sxs-lookup"><span data-stu-id="c2824-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="c2824-346">Topologia hybrydowego</span><span class="sxs-lookup"><span data-stu-id="c2824-346">Hybrid topology</span></span>
<span data-ttu-id="c2824-347">Natywny Storm napisano w języku Java.</span><span class="sxs-lookup"><span data-stu-id="c2824-347">The native Storm is written in Java.</span></span> <span data-ttu-id="c2824-348">I SCP.Net ma rozszerzone go w celu włączenia naszych celne zapisu C\# kod, aby obsłużyć ich logiki biznesowej.</span><span class="sxs-lookup"><span data-stu-id="c2824-348">And SCP.Net has enhanced it to enable our customs to write C\# code to handle their business logic.</span></span> <span data-ttu-id="c2824-349">Obsługujemy również hybrydowe topologie, która zawiera nie tylko C, ale\# elementów elementach spout/bolt, ale również elementów Java Spout/Bolt.</span><span class="sxs-lookup"><span data-stu-id="c2824-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="c2824-350">Określ Java Spout/Bolt w specyfikacji pliku</span><span class="sxs-lookup"><span data-stu-id="c2824-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="c2824-351">W specyfikacji pliku "punkt połączenia usługi spout" i "punkt połączenia usługi bolt" można również określić Java Spouts i elementów Bolt, Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="c2824-351">In spec file, "scp-spout" and "scp-bolt" can also be used to specify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="c2824-352">W tym miejscu `microsoft.scp.example.HybridTopology.Generator` jest nazwa klasy Java Spout.</span><span class="sxs-lookup"><span data-stu-id="c2824-352">Here `microsoft.scp.example.HybridTopology.Generator` is the name of the Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="c2824-353">Określ klasy Java w runSpec polecenia</span><span class="sxs-lookup"><span data-stu-id="c2824-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="c2824-354">Jeśli chcesz przesłać topologii zawierające Java Spouts lub elementów Bolt, należy najpierw skompilować Java Spouts lub elementów Bolt i Pobierz pliki Jar.</span><span class="sxs-lookup"><span data-stu-id="c2824-354">If you want to submit topology containing Java Spouts or Bolts, you need to first compile the Java Spouts or Bolts and get the Jar files.</span></span> <span data-ttu-id="c2824-355">Następnie należy określić klasy java, który zawiera pliki Jar podczas przesyłania topologii.</span><span class="sxs-lookup"><span data-stu-id="c2824-355">Then you should specify the java classpath that contains the Jar files when submitting topology.</span></span> <span data-ttu-id="c2824-356">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="c2824-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="c2824-357">W tym miejscu **przykłady\\HybridTopology\\java\\docelowej\\**  jest folder zawierający plik Jar Spout/Bolt Java.</span><span class="sxs-lookup"><span data-stu-id="c2824-357">Here **examples\\HybridTopology\\java\\target\\** is the folder containing the Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="c2824-358">Serializacja i deserializacja między Java i C\\</span><span class="sxs-lookup"><span data-stu-id="c2824-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="c2824-359">Nasze składnik SCP zawiera stronie Java i C\# po stronie.</span><span class="sxs-lookup"><span data-stu-id="c2824-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="c2824-360">Aby pracować interaktywnie z natywnego języka Java elementach Spout/elementów Bolt, serializacji/deserializacji przeprowadza się między stronie Java i C\# po stronie, jak przedstawiono na wykresie.</span><span class="sxs-lookup"><span data-stu-id="c2824-360">In order to interact with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in the following graph.</span></span>

![Diagram składnika java wysyłanie do wysyłania do składnika Java składnika punkt połączenia usługi](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="c2824-362">**Serializacja w stronie Java i deserializacji w języku C\# po stronie**</span><span class="sxs-lookup"><span data-stu-id="c2824-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="c2824-363">Najpierw firma Microsoft udostępnia domyślną implementację do serializacji w języku Java po stronie i deserializacji w języku C\# po stronie.</span><span class="sxs-lookup"><span data-stu-id="c2824-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="c2824-364">Metoda serializacji w języku Java po stronie można określić w specyfikacji pliku:</span><span class="sxs-lookup"><span data-stu-id="c2824-364">The serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="c2824-365">Metoda deserializacji w języku C\# po stronie powinny być określone w języku C\# kod użytkownika:</span><span class="sxs-lookup"><span data-stu-id="c2824-365">The deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="c2824-366">Ta domyślna implementacja powinna obsługiwać większości przypadków, jeśli typ danych nie jest zbyt złożony.</span><span class="sxs-lookup"><span data-stu-id="c2824-366">This default implementation should handle most cases if the data type is not too complex.</span></span> <span data-ttu-id="c2824-367">Dla niektórych przypadków, ponieważ typem danych użytkownika jest zbyt złożony lub funkcjonowania naszych Domyślna implementacja nie spełnia wymagań użytkownika, wtyczka użytkownika mogą ich implementacji.</span><span class="sxs-lookup"><span data-stu-id="c2824-367">For certain cases, either because the user data type is too complex, or because the performance of our default implementation does not meet the user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="c2824-368">Interfejs serializacja po stronie java jest zdefiniowany jako:</span><span class="sxs-lookup"><span data-stu-id="c2824-368">The serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="c2824-369">Interfejs deserialize w języku C\# po stronie jest zdefiniowany jako:</span><span class="sxs-lookup"><span data-stu-id="c2824-369">The deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="c2824-370">Interfejs publiczny ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="c2824-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="c2824-371">**Serializacji w języku C\# po stronie i deserializacji w języku Java obok siebie**</span><span class="sxs-lookup"><span data-stu-id="c2824-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="c2824-372">Metoda serializacji w języku C\# po stronie powinny być określone w języku C\# kod użytkownika:</span><span class="sxs-lookup"><span data-stu-id="c2824-372">The serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="c2824-373">W języku Java po stronie metody deserializacji powinny być określone w specyfikacji pliku:</span><span class="sxs-lookup"><span data-stu-id="c2824-373">The Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="c2824-374">(punkt połączenia usługi spout</span><span class="sxs-lookup"><span data-stu-id="c2824-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="c2824-375">Tutaj "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" jest nazwą Deserializator i "microsoft.scp.example.HybridTopology.Person" to klasa docelowa danych jest deserializacji do.</span><span class="sxs-lookup"><span data-stu-id="c2824-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is the name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is the target class the data is deserialized to.</span></span>
   
   <span data-ttu-id="c2824-376">Użytkownik może również wtyczki realizacji c\# serializator i Deserializator Java.</span><span class="sxs-lookup"><span data-stu-id="c2824-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="c2824-377">Jest to interfejs dla C\# serializator:</span><span class="sxs-lookup"><span data-stu-id="c2824-377">This is the interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="c2824-378">Jest to interfejs do deserializacji Java:</span><span class="sxs-lookup"><span data-stu-id="c2824-378">This is the interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="c2824-379">Tryb punktu połączenia usługi hosta</span><span class="sxs-lookup"><span data-stu-id="c2824-379">SCP Host Mode</span></span>
<span data-ttu-id="c2824-380">W tym trybie użytkownika można skompilować ich kody do biblioteki DLL i umożliwia SCPHost.exe dostarczonych przez punkt połączenia usługi przesyłania topologii.</span><span class="sxs-lookup"><span data-stu-id="c2824-380">In this mode, user can compile their codes to DLL, and use SCPHost.exe provided by SCP to submit topology.</span></span> <span data-ttu-id="c2824-381">Specyfikacji pliku wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="c2824-381">The spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="c2824-382">W tym miejscu `plugin.name` jest określony jako `SCPHost.exe` dostarczonych przez punkt połączenia usługi SDK.</span><span class="sxs-lookup"><span data-stu-id="c2824-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="c2824-383">SCPHost.exe akceptującego dokładnie trzy parametry:</span><span class="sxs-lookup"><span data-stu-id="c2824-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="c2824-384">Pierwsza z nich jest nazwa biblioteki DLL, która jest `"HelloWorld.dll"` w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c2824-384">The first one is the DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="c2824-385">Drugim jest nazwy klasy, która jest `"Scp.App.HelloWorld.Generator"` w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c2824-385">The second one is the Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="c2824-386">Trzeci jest nazwą publicznej metody statycznej, który może być wywoływany można pobrać wystąpienia ISCPPlugin.</span><span class="sxs-lookup"><span data-stu-id="c2824-386">The third one is the name of a public static method, which can be invoked to get an instance of ISCPPlugin.</span></span>

<span data-ttu-id="c2824-387">W trybie hosta kod użytkownika jest skompilowana jako biblioteki DLL i jest wywoływane przez platformę punkt połączenia usługi.</span><span class="sxs-lookup"><span data-stu-id="c2824-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="c2824-388">Dlatego platformy punkt połączenia usługi można uzyskać pełną kontrolę nad logika przetwarzania całego.</span><span class="sxs-lookup"><span data-stu-id="c2824-388">So SCP platform can get full control of the whole processing logic.</span></span> <span data-ttu-id="c2824-389">Dlatego zaleca się naszym klientom przesyłania topologii w trybie hosta punktu połączenia usługi, ponieważ może uprościć proces tworzenia i przełączyć nam większą elastyczność i lepszą zgodność z poprzednimi wersjami oraz nowszych wersji.</span><span class="sxs-lookup"><span data-stu-id="c2824-389">So we recommend our customers to submit topology in SCP host mode since it can simplify the development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="c2824-390">Przykłady programowania w języku punkt połączenia usługi</span><span class="sxs-lookup"><span data-stu-id="c2824-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="c2824-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="c2824-391">HelloWorld</span></span>
<span data-ttu-id="c2824-392">**HelloWorld** jest bardzo prosty przykład pokazanie smak SCP.Net.</span><span class="sxs-lookup"><span data-stu-id="c2824-392">**HelloWorld** is a very simple example to show a taste of SCP.Net.</span></span> <span data-ttu-id="c2824-393">Za pomocą topologii nietransakcyjnej i spout, nazywany **generator**i dwóch elementów bolt o nazwie **podziału** i **licznika**.</span><span class="sxs-lookup"><span data-stu-id="c2824-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="c2824-394">Spout **generator** będzie losowo wygenerować niektórych zdań i wyemitować tych zdań **podziału**.</span><span class="sxs-lookup"><span data-stu-id="c2824-394">The spout **generator** will randomly generate some sentences, and emit these sentences to **splitter**.</span></span> <span data-ttu-id="c2824-395">Elementy bolt **podziału** będzie podzielić zdań wyrazy i wysyłać te słowa do **licznika** bolt.</span><span class="sxs-lookup"><span data-stu-id="c2824-395">The bolt **splitter** will split the sentences to words and emit these words to **counter** bolt.</span></span> <span data-ttu-id="c2824-396">Bolt "licznika" używa słownika, aby zarejestrować numer wystąpienia każdego wyrazu.</span><span class="sxs-lookup"><span data-stu-id="c2824-396">The bolt "counter" uses a dictionary to record the occurrence number of each word.</span></span>

<span data-ttu-id="c2824-397">Istnieją dwa pliki specyfikacji, **HelloWorld.spec** i **HelloWorld\_EnableAck.spec** w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="c2824-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="c2824-398">W języku C\# kodu, jego można ustalić, czy potwierdzenia jest włączona, pobierając pluginConf z strony Java.</span><span class="sxs-lookup"><span data-stu-id="c2824-398">In the C\# code, it can find out whether ack is enabled by getting the pluginConf from Java side.</span></span>

    /* demo how to get pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="c2824-399">W spout po włączeniu potwierdzenia słownik jest używane do pamięci podręcznej krotek, które nie zostały jeszcze prześledzone.</span><span class="sxs-lookup"><span data-stu-id="c2824-399">In the spout, if ack is enabled, a dictionary is used to cache the tuples that have not been acked.</span></span> <span data-ttu-id="c2824-400">Jeśli Fail() zostanie wywołany, zostaną odtworzone krotki nie powiodło się:</span><span class="sxs-lookup"><span data-stu-id="c2824-400">If Fail() is called, the failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get the cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay the failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="c2824-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="c2824-401">HelloWorldTx</span></span>
<span data-ttu-id="c2824-402">**HelloWorldTx** przykładzie pokazano sposób wdrożenia transakcyjnego topologii.</span><span class="sxs-lookup"><span data-stu-id="c2824-402">The **HelloWorldTx** example demonstrates how to implement transactional topology.</span></span> <span data-ttu-id="c2824-403">Ma on jeden spout o nazwie **generator**, partii elementów bolt o nazwie **partial-count**, i wywołuje bolt zatwierdzania **Suma liczba**.</span><span class="sxs-lookup"><span data-stu-id="c2824-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="c2824-404">Istnieją również trzy pliki txt wstępnie utworzone: **DataSource0.txt**, **DataSource1.txt** i **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="c2824-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="c2824-405">W każdej transakcji spout **generator** będzie losowo wybierz dwa pliki z wstępnie utworzone trzy pliki i Emituj nazw dwóch plików do **partial-count** bolt.</span><span class="sxs-lookup"><span data-stu-id="c2824-405">In each transaction, the spout **generator** will randomly choose two files from the pre-created three files, and emit the two file names to the **partial-count** bolt.</span></span> <span data-ttu-id="c2824-406">Elementy bolt **partial-count** zostanie najpierw uzyskać nazwy pliku z odebrane spójnej kolekcji, a następnie otwórz plik i liczbę słów w tym pliku i na koniec Emituj numer programu word do **Suma liczba** bolt.</span><span class="sxs-lookup"><span data-stu-id="c2824-406">The bolt **partial-count** will first get the file name from the received tuple, then open the file and count the number of words in this file, and finally emit the word number to the **count-sum** bolt.</span></span> <span data-ttu-id="c2824-407">**Suma liczba** bolt podsumowanie liczby całkowitej.</span><span class="sxs-lookup"><span data-stu-id="c2824-407">The **count-sum** bolt will summarize the total count.</span></span>

<span data-ttu-id="c2824-408">Do osiągnięcia **dokładnie raz** semantyki, bolt zatwierdzania **Suma liczba** należy ocenić, czy jest powtórzonym transakcji.</span><span class="sxs-lookup"><span data-stu-id="c2824-408">To achieve **exactly once** semantics, the commit bolt **count-sum** need to judge whether it is a replayed transaction.</span></span> <span data-ttu-id="c2824-409">W tym przykładzie ma statycznym elementem członkowskim zmiennej:</span><span class="sxs-lookup"><span data-stu-id="c2824-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="c2824-410">Po utworzeniu wystąpienia ISCPBatchBolt pobierze `txAttempt` z parametrów wejściowych:</span><span class="sxs-lookup"><span data-stu-id="c2824-410">When an ISCPBatchBolt instance is created, it will get the `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from the input parms */
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

<span data-ttu-id="c2824-411">Gdy `FinishBatch()` jest nazywany `lastCommittedTxId` będzie aktualizacji, jeśli nie jest transakcją powtórzony.</span><span class="sxs-lookup"><span data-stu-id="c2824-411">When `FinishBatch()` is called, the `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update the toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="c2824-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="c2824-412">HybridTopology</span></span>
<span data-ttu-id="c2824-413">Ta topologia zawiera elementów Spout Java i C\# Bolt.</span><span class="sxs-lookup"><span data-stu-id="c2824-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="c2824-414">Domyślna implementacja serializacji i deserializacji dostarczane przez platformę punkt połączenia usługi jest używany.</span><span class="sxs-lookup"><span data-stu-id="c2824-414">It uses the default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="c2824-415">Skontaktuj się z ref **HybridTopology.spec** w **przykłady\\HybridTopology** folder szczegółów specyfikacji pliku i **SubmitTopology.bat** dla sposobu określania Klasy Java.</span><span class="sxs-lookup"><span data-stu-id="c2824-415">Please ref the **HybridTopology.spec** in **examples\\HybridTopology** folder for the spec file details, and **SubmitTopology.bat** for how to specify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="c2824-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="c2824-416">SCPHostDemo</span></span>
<span data-ttu-id="c2824-417">W tym przykładzie jest taka sama jak HelloWorld w zasadzie.</span><span class="sxs-lookup"><span data-stu-id="c2824-417">This example is the same as HelloWorld in essence.</span></span> <span data-ttu-id="c2824-418">Jedyna różnica polega na kompilowania kodu użytkownika jako biblioteki DLL, a topologia jest przesyłany za pomocą SCPHost.exe.</span><span class="sxs-lookup"><span data-stu-id="c2824-418">The only difference is that the user code is compiled as DLL and the topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="c2824-419">Skontaktuj się z odwołania w sekcji "Punkt połączenia usługi hosta tryb" bardziej szczegółowy opis.</span><span class="sxs-lookup"><span data-stu-id="c2824-419">Please ref the section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2824-420">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c2824-420">Next Steps</span></span>
<span data-ttu-id="c2824-421">Przykłady topologii Storm utworzone przy użyciu połączenia usługi zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="c2824-421">For examples of Storm topologies created using SCP, see the following:</span></span>

* [<span data-ttu-id="c2824-422">Tworzenie topologii C# dla Apache Storm w usłudze HDInsight przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c2824-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="c2824-423">Zdarzenia procesu z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2824-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="c2824-424">Tworzenie wielu strumieni danych w topologii Storm C#</span><span class="sxs-lookup"><span data-stu-id="c2824-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="c2824-425">Wizualizuj dane z topologii Storm przy użyciu usługi Power Bi</span><span class="sxs-lookup"><span data-stu-id="c2824-425">Use Power Bi to visualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="c2824-426">Przetwarzania danych czujnika vehicle z usługi Event Hubs za pomocą Storm w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2824-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="c2824-427">Wyodrębniania, transformacji i ładowania (ETL) z usługi Azure Event Hubs do bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="c2824-427">Extract, Transform, and Load (ETL) from Azure Event Hubs to HBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="c2824-428">Korelowanie zdarzeń za pomocą Storm i bazy danych HBase w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2824-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)

