---
title: "Przetwarzanie wsadowe wydajność aplikacji bazy danych SQL Azure tooimprove toouse aaaHow"
description: "Witaj temat zawiera dowód, że przetwarzanie wsadowe bazy danych operacji znacznie imroves hello szybkość i skalowalność aplikacji bazy danych SQL Azure. Mimo że te techniki przetwarzanie wsadowe działać dla dowolnej bazy danych programu SQL Server, hello hello artykuł koncentruje się na platformie Azure."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a><span data-ttu-id="92341-104">Jak toouse przetwarzanie wsadowe wydajność aplikacji tooimprove bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="92341-104">How toouse batching tooimprove SQL Database application performance</span></span>
<span data-ttu-id="92341-105">Przetwarzanie wsadowe operacji tooAzure bazy danych SQL znacznie poprawia hello wydajność i skalowalność aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92341-105">Batching operations tooAzure SQL Database significantly improves hello performance and scalability of your applications.</span></span> <span data-ttu-id="92341-106">W kolejności toounderstand hello korzyści hello pierwsza część w tym artykule omówiono niektóre przykładowe wyniki testów, pozwalające porównać tooa żądań wsadowych i sekwencyjny bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="92341-106">In order toounderstand hello benefits, hello first part of this article covers some sample test results that compare sequential and batched requests tooa SQL Database.</span></span> <span data-ttu-id="92341-107">Witaj dalszej części artykułu hello pokazuje hello technik, scenariusze i zagadnienia dotyczące toohelp toouse pomyślnie przetwarzanie wsadowe w aplikacjach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="92341-107">hello remainder of hello article shows hello techniques, scenarios, and considerations toohelp you toouse batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="92341-108">Dlaczego jest przetwarzanie wsadowe ważne dla bazy danych SQL?</span><span class="sxs-lookup"><span data-stu-id="92341-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="92341-109">Przetwarzanie wsadowe wywołania tooa zdalny jest dobrze znane strategię zwiększenie wydajności i skalowalności.</span><span class="sxs-lookup"><span data-stu-id="92341-109">Batching calls tooa remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="92341-110">Usunięto przetwarzania kosztów tooany interakcji z usługi zdalnej, takich jak serializacji, transferu sieciowego i deserializacji.</span><span class="sxs-lookup"><span data-stu-id="92341-110">There are fixed processing costs tooany interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="92341-111">Pakowanie wiele oddzielnych transakcji do pojedynczej partii minimalizuje tych kosztów.</span><span class="sxs-lookup"><span data-stu-id="92341-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="92341-112">W tym dokumencie chcemy tooexamine różne strategie przetwarzanie wsadowe bazy danych SQL i scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="92341-112">In this paper, we want tooexamine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="92341-113">Mimo że strategie również są ważne dla aplikacji lokalnych, które używają programu SQL Server, istnieje kilka przyczyn wyróżnianie hello stosowania przetwarzania wsadowego dla bazy danych SQL:</span><span class="sxs-lookup"><span data-stu-id="92341-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting hello use of batching for SQL Database:</span></span>

* <span data-ttu-id="92341-114">Brak potencjalnie większe opóźnienia sieci podczas uzyskiwania dostępu do bazy danych SQL, zwłaszcza, jeśli uzyskują dostęp do bazy danych SQL z hello poza tym samym centrum danych Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="92341-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside hello same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="92341-115">toohello odpowiada warstwy dostępu Hello wielodostępnym właściwości bazy danych SQL oznacza, że hello wydajności danych hello ogólnej skalowalności hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="92341-115">hello multitenant characteristics of SQL Database means that hello efficiency of hello data access layer correlates toohello overall scalability of hello database.</span></span> <span data-ttu-id="92341-116">Baza danych SQL musi uniemożliwić przejęcie kontroli nad bazy danych zasobów toohello szkody innych dzierżawców dowolnego pojedynczego dzierżawcy/użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92341-116">SQL Database must prevent any single tenant/user from monopolizing database resources toohello detriment of other tenants.</span></span> <span data-ttu-id="92341-117">W odpowiedzi toousage poza przydziały wstępnie zdefiniowane bazy danych SQL można zmniejszyć przepływności lub odpowiadać, podając ograniczania wyjątków.</span><span class="sxs-lookup"><span data-stu-id="92341-117">In response toousage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="92341-118">Korzyści, takich jak przetwarzanie wsadowe, Włącz toodo możesz więcej pracy w bazie danych SQL przed osiągnięciem tych ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="92341-118">Efficiencies, such as batching, enable you toodo more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="92341-119">Tworzenie plików wsadowych jest również dla architektury, które używają wielu baz danych (dzielenia na fragmenty).</span><span class="sxs-lookup"><span data-stu-id="92341-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="92341-120">wydajność Hello współpracy z każdej jednostki bazy danych nadal jest kluczowym czynnikiem Twojej ogólnej skalowalności.</span><span class="sxs-lookup"><span data-stu-id="92341-120">hello efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="92341-121">Jedną z zalet hello przy użyciu bazy danych SQL jest, że nie masz serwerów hello toomanage hello hosta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="92341-121">One of hello benefits of using SQL Database is that you don’t have toomanage hello servers that host hello database.</span></span> <span data-ttu-id="92341-122">Jednak ta infrastruktura zarządzanych również oznacza, że toothink inaczej o optymalizacji bazy danych.</span><span class="sxs-lookup"><span data-stu-id="92341-122">However, this managed infrastructure also means that you have toothink differently about database optimizations.</span></span> <span data-ttu-id="92341-123">Nie można sprawdzić tooimprove hello bazy danych sprzętu lub siecią infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="92341-123">You can no longer look tooimprove hello database hardware or network infrastructure.</span></span> <span data-ttu-id="92341-124">Microsoft Azure określa tych środowisk.</span><span class="sxs-lookup"><span data-stu-id="92341-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="92341-125">Hello obszaru głównego, który można kontrolować jest współdziałania aplikacji z bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="92341-125">hello main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="92341-126">Tworzenie plików wsadowych jest jednym z tych optymalizacji.</span><span class="sxs-lookup"><span data-stu-id="92341-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="92341-127">Pierwsza część papieru hello Hello sprawdza różnych technik przetwarzanie wsadowe aplikacji .NET, które używają bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="92341-127">hello first part of hello paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="92341-128">sekcje ostatnich dwóch Hello obejmują scenariusze i wskazówki dotyczące przetwarzanie wsadowe.</span><span class="sxs-lookup"><span data-stu-id="92341-128">hello last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="92341-129">Przetwarzanie wsadowe strategie</span><span class="sxs-lookup"><span data-stu-id="92341-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="92341-130">Należy pamiętać o wynikach czasu, w tym temacie</span><span class="sxs-lookup"><span data-stu-id="92341-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="92341-131">Wyniki nie są testów porównawczych, ale mają tooshow **względną wydajność**.</span><span class="sxs-lookup"><span data-stu-id="92341-131">Results are not benchmarks but are meant tooshow **relative performance**.</span></span> <span data-ttu-id="92341-132">Czasy są oparte na średnio co najmniej 10 uruchomień testów.</span><span class="sxs-lookup"><span data-stu-id="92341-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="92341-133">Operacje są wstawia do pustej tabeli.</span><span class="sxs-lookup"><span data-stu-id="92341-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="92341-134">Te testy zostały zmierzone pre-V12, a ich nie muszą odpowiadać toothroughput, które mogą pojawić się w bazie danych w wersji 12 przy użyciu nowego hello [warstw usług](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="92341-134">These tests were measured pre-V12, and they do not necessarily correspond toothroughput that you might experience in a V12 database using hello new [service tiers](sql-database-service-tiers.md).</span></span> <span data-ttu-id="92341-135">Hello względną zaletą hello przetwarzanie wsadowe technika powinny być podobne.</span><span class="sxs-lookup"><span data-stu-id="92341-135">hello relative benefit of hello batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="92341-136">Transakcje</span><span class="sxs-lookup"><span data-stu-id="92341-136">Transactions</span></span>
<span data-ttu-id="92341-137">Wydaje się dziwne toobegin Przegląd przetwarzania wsadowego przez dyskutować transakcji.</span><span class="sxs-lookup"><span data-stu-id="92341-137">It seems strange toobegin a review of batching by discussing transactions.</span></span> <span data-ttu-id="92341-138">Ale użyj hello transakcji po stronie klienta ma Delikatny efekt przetwarzanie wsadowe po stronie serwera, który zapewnia lepszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="92341-138">But hello use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="92341-139">I transakcji można dodać przy tylko kilku wierszy kodu, więc zapewniają szybki sposób wydajności tooimprove sekwencyjnych operacji.</span><span class="sxs-lookup"><span data-stu-id="92341-139">And transactions can be added with only a few lines of code, so they provide a fast way tooimprove performance of sequential operations.</span></span>

<span data-ttu-id="92341-140">Należy wziąć pod uwagę hello następującego kodu C#, który zawiera sekwencję INSERT i aktualizowanie operacji na prostej tabeli.</span><span class="sxs-lookup"><span data-stu-id="92341-140">Consider hello following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="92341-141">Hello następującego kodu ADO.NET sekwencyjnie wykonuje te operacje.</span><span class="sxs-lookup"><span data-stu-id="92341-141">hello following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="92341-142">Witaj najlepsze sposób toooptimize ten kod jest tooimplement jakiegoś typu po stronie klienta przetwarzanie wsadowe tych wywołań.</span><span class="sxs-lookup"><span data-stu-id="92341-142">hello best way toooptimize this code is tooimplement some form of client-side batching of these calls.</span></span> <span data-ttu-id="92341-143">Występuje wydajność hello tooincrease prosty sposób ten kod po prostu zawijania hello sekwencję wywołań w transakcji.</span><span class="sxs-lookup"><span data-stu-id="92341-143">But there is a simple way tooincrease hello performance of this code by simply wrapping hello sequence of calls in a transaction.</span></span> <span data-ttu-id="92341-144">Oto hello tego samego kodu, który używa transakcji.</span><span class="sxs-lookup"><span data-stu-id="92341-144">Here is hello same code that uses a transaction.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

<span data-ttu-id="92341-145">Transakcje są rzeczywiście używane w obu tych przykładów.</span><span class="sxs-lookup"><span data-stu-id="92341-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="92341-146">W pierwszym przykładzie hello każdego wywołania poszczególnych jest transakcji niejawnej.</span><span class="sxs-lookup"><span data-stu-id="92341-146">In hello first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="92341-147">W drugim przykładzie hello transakcji jawnej opakowuje wszystkich połączeń hello.</span><span class="sxs-lookup"><span data-stu-id="92341-147">In hello second example, an explicit transaction wraps all of hello calls.</span></span> <span data-ttu-id="92341-148">Na powitania dokumentacji hello [dziennika transakcji zapisu z wyprzedzeniem](https://msdn.microsoft.com/library/ms186259.aspx), rekordów dziennika są wyczyszczone toohello dysku po zatwierdzeniu hello transakcji.</span><span class="sxs-lookup"><span data-stu-id="92341-148">Per hello documentation for hello [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed toohello disk when hello transaction commits.</span></span> <span data-ttu-id="92341-149">Dlatego przy tym kolejnych wywołań w transakcji, hello dziennika transakcji toohello zapisu można opóźnienie do momentu hello transakcja została przekazana.</span><span class="sxs-lookup"><span data-stu-id="92341-149">So by including more calls in a transaction, hello write toohello transaction log can delay until hello transaction is committed.</span></span> <span data-ttu-id="92341-150">W efekcie włączasz, przetwarzanie wsadowe dla dziennika transakcji serwera hello zapisy toohello.</span><span class="sxs-lookup"><span data-stu-id="92341-150">In effect, you are enabling batching for hello writes toohello server’s transaction log.</span></span>

<span data-ttu-id="92341-151">Hello w poniższej tabeli przedstawiono niektóre wyniki testowania ad hoc.</span><span class="sxs-lookup"><span data-stu-id="92341-151">hello following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="92341-152">Witaj testy wykonywane hello, które same sekwencyjnych wstawia z włączonymi i wyłączonymi transakcji.</span><span class="sxs-lookup"><span data-stu-id="92341-152">hello tests performed hello same sequential inserts with and without transactions.</span></span> <span data-ttu-id="92341-153">Więcej perspektywy hello pierwszy zestaw testów został uruchomiony zdalnie z komputera przenośnego toohello bazy danych w systemie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="92341-153">For more perspective, hello first set of tests ran remotely from a laptop toohello database in Microsoft Azure.</span></span> <span data-ttu-id="92341-154">Witaj drugi zestaw testów został uruchomiony z usługi w chmurze i że oba znajdowały się w obrębie hello sama baza danych Microsoft Azure datacenter (zachodnie stany USA).</span><span class="sxs-lookup"><span data-stu-id="92341-154">hello second set of tests ran from a cloud service and database that both resided within hello same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="92341-155">Witaj poniższej tabeli przedstawiono czas trwania hello w milisekundach sekwencyjnego wstawiania z włączonymi i wyłączonymi transakcji.</span><span class="sxs-lookup"><span data-stu-id="92341-155">hello following table shows hello duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="92341-156">**TooAzure lokalnymi**:</span><span class="sxs-lookup"><span data-stu-id="92341-156">**On-Premises tooAzure**:</span></span>

| <span data-ttu-id="92341-157">Operacje</span><span class="sxs-lookup"><span data-stu-id="92341-157">Operations</span></span> | <span data-ttu-id="92341-158">Brak transakcji (ms)</span><span class="sxs-lookup"><span data-stu-id="92341-158">No Transaction (ms)</span></span> | <span data-ttu-id="92341-159">W transakcji (ms)</span><span class="sxs-lookup"><span data-stu-id="92341-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92341-160">1</span><span class="sxs-lookup"><span data-stu-id="92341-160">1</span></span> |<span data-ttu-id="92341-161">130</span><span class="sxs-lookup"><span data-stu-id="92341-161">130</span></span> |<span data-ttu-id="92341-162">402</span><span class="sxs-lookup"><span data-stu-id="92341-162">402</span></span> |
| <span data-ttu-id="92341-163">10</span><span class="sxs-lookup"><span data-stu-id="92341-163">10</span></span> |<span data-ttu-id="92341-164">1208</span><span class="sxs-lookup"><span data-stu-id="92341-164">1208</span></span> |<span data-ttu-id="92341-165">1226</span><span class="sxs-lookup"><span data-stu-id="92341-165">1226</span></span> |
| <span data-ttu-id="92341-166">100</span><span class="sxs-lookup"><span data-stu-id="92341-166">100</span></span> |<span data-ttu-id="92341-167">12662</span><span class="sxs-lookup"><span data-stu-id="92341-167">12662</span></span> |<span data-ttu-id="92341-168">10395</span><span class="sxs-lookup"><span data-stu-id="92341-168">10395</span></span> |
| <span data-ttu-id="92341-169">1000</span><span class="sxs-lookup"><span data-stu-id="92341-169">1000</span></span> |<span data-ttu-id="92341-170">128852</span><span class="sxs-lookup"><span data-stu-id="92341-170">128852</span></span> |<span data-ttu-id="92341-171">102917</span><span class="sxs-lookup"><span data-stu-id="92341-171">102917</span></span> |

<span data-ttu-id="92341-172">**Azure tooAzure (tym samym centrum danych)**:</span><span class="sxs-lookup"><span data-stu-id="92341-172">**Azure tooAzure (same datacenter)**:</span></span>

| <span data-ttu-id="92341-173">Operacje</span><span class="sxs-lookup"><span data-stu-id="92341-173">Operations</span></span> | <span data-ttu-id="92341-174">Brak transakcji (ms)</span><span class="sxs-lookup"><span data-stu-id="92341-174">No Transaction (ms)</span></span> | <span data-ttu-id="92341-175">W transakcji (ms)</span><span class="sxs-lookup"><span data-stu-id="92341-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92341-176">1</span><span class="sxs-lookup"><span data-stu-id="92341-176">1</span></span> |<span data-ttu-id="92341-177">21</span><span class="sxs-lookup"><span data-stu-id="92341-177">21</span></span> |<span data-ttu-id="92341-178">26</span><span class="sxs-lookup"><span data-stu-id="92341-178">26</span></span> |
| <span data-ttu-id="92341-179">10</span><span class="sxs-lookup"><span data-stu-id="92341-179">10</span></span> |<span data-ttu-id="92341-180">220</span><span class="sxs-lookup"><span data-stu-id="92341-180">220</span></span> |<span data-ttu-id="92341-181">56</span><span class="sxs-lookup"><span data-stu-id="92341-181">56</span></span> |
| <span data-ttu-id="92341-182">100</span><span class="sxs-lookup"><span data-stu-id="92341-182">100</span></span> |<span data-ttu-id="92341-183">2145</span><span class="sxs-lookup"><span data-stu-id="92341-183">2145</span></span> |<span data-ttu-id="92341-184">341</span><span class="sxs-lookup"><span data-stu-id="92341-184">341</span></span> |
| <span data-ttu-id="92341-185">1000</span><span class="sxs-lookup"><span data-stu-id="92341-185">1000</span></span> |<span data-ttu-id="92341-186">21479</span><span class="sxs-lookup"><span data-stu-id="92341-186">21479</span></span> |<span data-ttu-id="92341-187">2756</span><span class="sxs-lookup"><span data-stu-id="92341-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="92341-188">Wyniki nie są testy.</span><span class="sxs-lookup"><span data-stu-id="92341-188">Results are not benchmarks.</span></span> <span data-ttu-id="92341-189">Zobacz hello [należy pamiętać o wynikach czasu, w tym temacie](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="92341-189">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="92341-190">Oparte na powitania poprzednie wyniki testu, zawijania jednej operacji w transakcji obniża wydajność.</span><span class="sxs-lookup"><span data-stu-id="92341-190">Based on hello previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="92341-191">Ale zwiększania hello liczba operacji w ramach jednej transakcji zwiększenie wydajności hello staje się bardziej oznaczone.</span><span class="sxs-lookup"><span data-stu-id="92341-191">But as you increase hello number of operations within a single transaction, hello performance improvement becomes more marked.</span></span> <span data-ttu-id="92341-192">poprawę wydajności Hello jest bardziej widoczne również w przypadku, gdy wszystkie operacje są wykonywane w ramach centrum danych Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="92341-192">hello performance difference is also more noticeable when all operations occur within hello Microsoft Azure datacenter.</span></span> <span data-ttu-id="92341-193">Witaj większe opóźnienia korzystania z bazy danych SQL z centrum danych Microsoft Azure poza hello overshadows hello przyrost wydajności przy użyciu transakcji.</span><span class="sxs-lookup"><span data-stu-id="92341-193">hello increased latency of using SQL Database from outside hello Microsoft Azure datacenter overshadows hello performance gain of using transactions.</span></span>

<span data-ttu-id="92341-194">Mimo że hello użycie transakcji można zwiększyć wydajność, nadal zbyt[obserwować najlepsze rozwiązania dotyczące połączenia i transakcje](https://msdn.microsoft.com/library/ms187484.aspx).</span><span class="sxs-lookup"><span data-stu-id="92341-194">Although hello use of transactions can increase performance, continue too[observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="92341-195">Zachowanie transakcji hello tak krótka jak to możliwe i zamknij hello połączenia z bazą danych, po zakończeniu pracy hello.</span><span class="sxs-lookup"><span data-stu-id="92341-195">Keep hello transaction as short as possible, and close hello database connection after hello work completes.</span></span> <span data-ttu-id="92341-196">przy użyciu instrukcji w poprzednim przykładzie hello Hello gwarantuje, że połączenie hello jest zamknięte po zakończeniu blok kodu kolejnych hello.</span><span class="sxs-lookup"><span data-stu-id="92341-196">hello using statement in hello previous example assures that hello connection is closed when hello subsequent code block completes.</span></span>

<span data-ttu-id="92341-197">Hello w poprzednim przykładzie pokazano, dodać kod ADO.NET tooany transakcji lokalnej z dwóch wierszy.</span><span class="sxs-lookup"><span data-stu-id="92341-197">hello previous example demonstrates that you can add a local transaction tooany ADO.NET code with two lines.</span></span> <span data-ttu-id="92341-198">Transakcje oferują szybki sposób tooimprove hello wydajności kodu, który sprawia, że kolejne wstawiania, aktualizowania i usuwania operacji.</span><span class="sxs-lookup"><span data-stu-id="92341-198">Transactions offer a quick way tooimprove hello performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="92341-199">Jednak dla hello największą wydajność, należy rozważyć zmianę hello kodu dalsze tootake zaletą po stronie klienta przetwarzanie wsadowe, takie jak parametry przechowywanymi w tabeli.</span><span class="sxs-lookup"><span data-stu-id="92341-199">However, for hello fastest performance, consider changing hello code further tootake advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="92341-200">Aby uzyskać więcej informacji o transakcji w ADO.NET, zobacz [lokalne transakcje w ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span><span class="sxs-lookup"><span data-stu-id="92341-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="92341-201">Parametry przechowywanymi w tabeli</span><span class="sxs-lookup"><span data-stu-id="92341-201">Table-valued parameters</span></span>
<span data-ttu-id="92341-202">Parametry przechowywanymi w tabeli obsługuje typach tabel zdefiniowanych przez użytkownika jako parametry w instrukcji języka Transact-SQL, procedury składowane i funkcje.</span><span class="sxs-lookup"><span data-stu-id="92341-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="92341-203">Ta technika przetwarzanie wsadowe po stronie klienta umożliwia toosend wiele wierszy danych w ramach hello parametru przechowywanymi w tabeli.</span><span class="sxs-lookup"><span data-stu-id="92341-203">This client-side batching technique allows you toosend multiple rows of data within hello table-valued parameter.</span></span> <span data-ttu-id="92341-204">Parametry toouse przechowywanymi w tabeli, najpierw zdefiniować typu tabeli.</span><span class="sxs-lookup"><span data-stu-id="92341-204">toouse table-valued parameters, first define a table type.</span></span> <span data-ttu-id="92341-205">Witaj następującej instrukcji języka Transact-SQL tworzy typ tabeli o nazwie **MyTableType**.</span><span class="sxs-lookup"><span data-stu-id="92341-205">hello following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="92341-206">W kodzie, możesz utworzyć **DataTable** z hello dokładnie tej samej nazwy i typy hello typ tabeli.</span><span class="sxs-lookup"><span data-stu-id="92341-206">In code, you create a **DataTable** with hello exact same names and types of hello table type.</span></span> <span data-ttu-id="92341-207">Przekazany **DataTable** w parametrze tekstu zapytania lub procedury składowanej wywołania.</span><span class="sxs-lookup"><span data-stu-id="92341-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="92341-208">Witaj poniższy przykład przedstawia tej techniki:</span><span class="sxs-lookup"><span data-stu-id="92341-208">hello following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

<span data-ttu-id="92341-209">W poprzednim przykładzie hello hello **SqlCommand** obiektu wstawia wiersze z parametrem przechowywanymi w tabeli  **@TestTvp** .</span><span class="sxs-lookup"><span data-stu-id="92341-209">In hello previous example, hello **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="92341-210">Hello wcześniej utworzony **DataTable** obiektu przypisano parametru toothis o hello **SqlCommand.Parameters.Add** metody.</span><span class="sxs-lookup"><span data-stu-id="92341-210">hello previously created **DataTable** object is assigned toothis parameter with hello **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="92341-211">Przetwarzanie wsadowe wstawia hello w jednym wywołać znacznie zwiększa wydajność hello za pośrednictwem sekwencyjnego wstawiania.</span><span class="sxs-lookup"><span data-stu-id="92341-211">Batching hello inserts in one call significantly increases hello performance over sequential inserts.</span></span>

<span data-ttu-id="92341-212">tooimprove hello poprzedni przykład, użyj procedury składowanej zamiast polecenia opartego na tekście.</span><span class="sxs-lookup"><span data-stu-id="92341-212">tooimprove hello previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="92341-213">następujące polecenie języka Transact-SQL Hello tworzy procedury przechowywanej, która przyjmuje hello **SimpleTestTableType** parametru przechowywanymi w tabeli.</span><span class="sxs-lookup"><span data-stu-id="92341-213">hello following Transact-SQL command creates a stored procedure that takes hello **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="92341-214">Następnie zmienić hello **SqlCommand** obiekt deklaracji w poniższych toohello przykładów kodu hello poprzedniej.</span><span class="sxs-lookup"><span data-stu-id="92341-214">Then change hello **SqlCommand** object declaration in hello previous code example toohello following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="92341-215">W większości przypadków przechowywanymi w tabeli Parametry mają równoważną lub lepszą wydajność niż innych technik, przetwarzanie wsadowe.</span><span class="sxs-lookup"><span data-stu-id="92341-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="92341-216">Parametry przechowywanymi w tabeli są często zalecane, ponieważ są one bardziej elastyczne niż inne opcje.</span><span class="sxs-lookup"><span data-stu-id="92341-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="92341-217">Na przykład innych technik, takich jak kopiowania zbiorczego SQL, tylko umożliwienia hello wstawiania nowych wierszy.</span><span class="sxs-lookup"><span data-stu-id="92341-217">For example, other techniques, such as SQL bulk copy, only permit hello insertion of new rows.</span></span> <span data-ttu-id="92341-218">Ale z parametrami przechowywanymi w tabeli, możesz użyć logikę w hello przechowywane procedury toodetermine wiersze, które są aktualizacje i które są wstawia.</span><span class="sxs-lookup"><span data-stu-id="92341-218">But with table-valued parameters, you can use logic in hello stored procedure toodetermine which rows are updates and which are inserts.</span></span> <span data-ttu-id="92341-219">Typ tabeli Hello można także toocontain zmodyfikował kolumnę "Operacji", która wskazuje, czy hello określony wiersz powinien można wstawiać, zaktualizować lub usunąć.</span><span class="sxs-lookup"><span data-stu-id="92341-219">hello table type can also be modified toocontain an “Operation” column that indicates whether hello specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="92341-220">Witaj w poniższej tabeli przedstawiono ad hoc wyników testu do użytku hello parametrów przechowywanymi w tabeli w milisekundach.</span><span class="sxs-lookup"><span data-stu-id="92341-220">hello following table shows ad-hoc test results for hello use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="92341-221">Operacje</span><span class="sxs-lookup"><span data-stu-id="92341-221">Operations</span></span> | <span data-ttu-id="92341-222">TooAzure lokalnymi (ms)</span><span class="sxs-lookup"><span data-stu-id="92341-222">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="92341-223">Tym samym centrum danych Azure (ms)</span><span class="sxs-lookup"><span data-stu-id="92341-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92341-224">1</span><span class="sxs-lookup"><span data-stu-id="92341-224">1</span></span> |<span data-ttu-id="92341-225">124</span><span class="sxs-lookup"><span data-stu-id="92341-225">124</span></span> |<span data-ttu-id="92341-226">32</span><span class="sxs-lookup"><span data-stu-id="92341-226">32</span></span> |
| <span data-ttu-id="92341-227">10</span><span class="sxs-lookup"><span data-stu-id="92341-227">10</span></span> |<span data-ttu-id="92341-228">131</span><span class="sxs-lookup"><span data-stu-id="92341-228">131</span></span> |<span data-ttu-id="92341-229">25</span><span class="sxs-lookup"><span data-stu-id="92341-229">25</span></span> |
| <span data-ttu-id="92341-230">100</span><span class="sxs-lookup"><span data-stu-id="92341-230">100</span></span> |<span data-ttu-id="92341-231">338</span><span class="sxs-lookup"><span data-stu-id="92341-231">338</span></span> |<span data-ttu-id="92341-232">51</span><span class="sxs-lookup"><span data-stu-id="92341-232">51</span></span> |
| <span data-ttu-id="92341-233">1000</span><span class="sxs-lookup"><span data-stu-id="92341-233">1000</span></span> |<span data-ttu-id="92341-234">2615</span><span class="sxs-lookup"><span data-stu-id="92341-234">2615</span></span> |<span data-ttu-id="92341-235">382</span><span class="sxs-lookup"><span data-stu-id="92341-235">382</span></span> |
| <span data-ttu-id="92341-236">10 000</span><span class="sxs-lookup"><span data-stu-id="92341-236">10000</span></span> |<span data-ttu-id="92341-237">23830</span><span class="sxs-lookup"><span data-stu-id="92341-237">23830</span></span> |<span data-ttu-id="92341-238">3586</span><span class="sxs-lookup"><span data-stu-id="92341-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="92341-239">Wyniki nie są testy.</span><span class="sxs-lookup"><span data-stu-id="92341-239">Results are not benchmarks.</span></span> <span data-ttu-id="92341-240">Zobacz hello [należy pamiętać o wynikach czasu, w tym temacie](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="92341-240">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="92341-241">Hello są bardziej wydajne z tworzenie plików wsadowych jest oczywista.</span><span class="sxs-lookup"><span data-stu-id="92341-241">hello performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="92341-242">Poprzedni test sekwencyjnych hello 1000 operacji trwało 129 sekund hello poza centrum danych i 21 sekund od w ramach hello centrum danych.</span><span class="sxs-lookup"><span data-stu-id="92341-242">In hello previous sequential test, 1000 operations took 129 seconds outside hello datacenter and 21 seconds from within hello datacenter.</span></span> <span data-ttu-id="92341-243">Jednak z parametrami przechowywanymi w tabeli, operacje 1000 wykorzystania tylko 2.6 sekund poza centrum danych hello i 0,4 sekund w obrębie centrum danych hello.</span><span class="sxs-lookup"><span data-stu-id="92341-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside hello datacenter and 0.4 seconds within hello datacenter.</span></span>

<span data-ttu-id="92341-244">Aby uzyskać więcej informacji o parametrach przechowywanymi w tabeli, zobacz [zwracającej tabelę parametrów](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="92341-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="92341-245">Kopiowania zbiorczego SQL</span><span class="sxs-lookup"><span data-stu-id="92341-245">SQL bulk copy</span></span>
<span data-ttu-id="92341-246">Kopiowania zbiorczego SQL jest w inny sposób tooinsert dużych ilości danych do docelowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="92341-246">SQL bulk copy is another way tooinsert large amounts of data into a target database.</span></span> <span data-ttu-id="92341-247">Aplikacje .NET mogą używać hello **SqlBulkCopy** klasy tooperform zbiorczego wstawiania operacji.</span><span class="sxs-lookup"><span data-stu-id="92341-247">.NET applications can use hello **SqlBulkCopy** class tooperform bulk insert operations.</span></span> <span data-ttu-id="92341-248">**SqlBulkCopy** przypomina w funkcji toohello narzędzie wiersza polecenia, **Bcp.exe**, lub hello instrukcji języka Transact-SQL **BULK INSERT**.</span><span class="sxs-lookup"><span data-stu-id="92341-248">**SqlBulkCopy** is similar in function toohello command-line tool, **Bcp.exe**, or hello Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="92341-249">Witaj Poniższy przykładowy kod przedstawia sposób hello kopiowania toobulk wierszy w źródle hello **DataTable**, tabeli, w tabeli docelowej toohello w programie SQL Server, MyTable.</span><span class="sxs-lookup"><span data-stu-id="92341-249">hello following code example shows how toobulk copy hello rows in hello source **DataTable**, table, toohello destination table in SQL Server, MyTable.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

<span data-ttu-id="92341-250">Istnieją przypadki, gdzie kopiowania zbiorczego jest preferowana przez parametry przechowywanymi w tabeli.</span><span class="sxs-lookup"><span data-stu-id="92341-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="92341-251">Zobacz Tabela porównawcza hello przechowywanymi w tabeli parametrów lub w temacie hello BULK INSERT [zwracającej tabelę parametrów](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="92341-251">See hello comparison table of Table-Valued parameters versus BULK INSERT operations in hello topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="92341-252">Witaj następujące wyniki testu ad hoc Pokaż hello wydajność przetwarzania wsadowego z **SqlBulkCopy** w milisekundach.</span><span class="sxs-lookup"><span data-stu-id="92341-252">hello following ad-hoc test results show hello performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="92341-253">Operacje</span><span class="sxs-lookup"><span data-stu-id="92341-253">Operations</span></span> | <span data-ttu-id="92341-254">TooAzure lokalnymi (ms)</span><span class="sxs-lookup"><span data-stu-id="92341-254">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="92341-255">Tym samym centrum danych Azure (ms)</span><span class="sxs-lookup"><span data-stu-id="92341-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92341-256">1</span><span class="sxs-lookup"><span data-stu-id="92341-256">1</span></span> |<span data-ttu-id="92341-257">433</span><span class="sxs-lookup"><span data-stu-id="92341-257">433</span></span> |<span data-ttu-id="92341-258">57</span><span class="sxs-lookup"><span data-stu-id="92341-258">57</span></span> |
| <span data-ttu-id="92341-259">10</span><span class="sxs-lookup"><span data-stu-id="92341-259">10</span></span> |<span data-ttu-id="92341-260">441</span><span class="sxs-lookup"><span data-stu-id="92341-260">441</span></span> |<span data-ttu-id="92341-261">32</span><span class="sxs-lookup"><span data-stu-id="92341-261">32</span></span> |
| <span data-ttu-id="92341-262">100</span><span class="sxs-lookup"><span data-stu-id="92341-262">100</span></span> |<span data-ttu-id="92341-263">636</span><span class="sxs-lookup"><span data-stu-id="92341-263">636</span></span> |<span data-ttu-id="92341-264">53</span><span class="sxs-lookup"><span data-stu-id="92341-264">53</span></span> |
| <span data-ttu-id="92341-265">1000</span><span class="sxs-lookup"><span data-stu-id="92341-265">1000</span></span> |<span data-ttu-id="92341-266">2535</span><span class="sxs-lookup"><span data-stu-id="92341-266">2535</span></span> |<span data-ttu-id="92341-267">341</span><span class="sxs-lookup"><span data-stu-id="92341-267">341</span></span> |
| <span data-ttu-id="92341-268">10 000</span><span class="sxs-lookup"><span data-stu-id="92341-268">10000</span></span> |<span data-ttu-id="92341-269">21605</span><span class="sxs-lookup"><span data-stu-id="92341-269">21605</span></span> |<span data-ttu-id="92341-270">2737</span><span class="sxs-lookup"><span data-stu-id="92341-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="92341-271">Wyniki nie są testy.</span><span class="sxs-lookup"><span data-stu-id="92341-271">Results are not benchmarks.</span></span> <span data-ttu-id="92341-272">Zobacz hello [należy pamiętać o wynikach czasu, w tym temacie](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="92341-272">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="92341-273">W mniejszych partii hello korzystanie z przechowywanymi w tabeli parametrów outperformed hello **SqlBulkCopy** klasy.</span><span class="sxs-lookup"><span data-stu-id="92341-273">In smaller batch sizes, hello use table-valued parameters outperformed hello **SqlBulkCopy** class.</span></span> <span data-ttu-id="92341-274">Jednak **SqlBulkCopy** wykonano % 12-31 szybciej niż przechowywanymi w tabeli parametrów dla testów hello 1000 i 10 000 wierszy.</span><span class="sxs-lookup"><span data-stu-id="92341-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for hello tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="92341-275">Przechowywanymi w tabeli parametrów, takich jak **SqlBulkCopy** jest dobra opcja w przypadku operacji wsadowej operacji wstawienia, szczególnie w porównaniu toohello wydajność operacji niewsadowego.</span><span class="sxs-lookup"><span data-stu-id="92341-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared toohello performance of non-batched operations.</span></span>

<span data-ttu-id="92341-276">Aby uzyskać więcej informacji dotyczących kopiowania zbiorczego w ADO.NET, zobacz [operacje kopiowania masowego w programie SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span><span class="sxs-lookup"><span data-stu-id="92341-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="92341-277">Instrukcje sparametryzowana WSTAWIĆ wiele wierszy</span><span class="sxs-lookup"><span data-stu-id="92341-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="92341-278">Jeden alternatywą dla małych partii jest tooconstruct dużej sparametryzowanych instrukcji INSERT, która wstawia wiele wierszy.</span><span class="sxs-lookup"><span data-stu-id="92341-278">One alternative for small batches is tooconstruct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="92341-279">Witaj poniższy przykład kodu pokazuje tej metody.</span><span class="sxs-lookup"><span data-stu-id="92341-279">hello following code example demonstrates this technique.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


<span data-ttu-id="92341-280">W tym przykładzie oznacza tooshow hello podstawowe pojęcia.</span><span class="sxs-lookup"><span data-stu-id="92341-280">This example is meant tooshow hello basic concept.</span></span> <span data-ttu-id="92341-281">Scenariusz bardziej realistyczne czy pętli ciąg hello wymagane jednostek tooconstruct hello zapytania i parametry polecenia hello jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="92341-281">A more realistic scenario would loop through hello required entities tooconstruct hello query string and hello command parameters simultaneously.</span></span> <span data-ttu-id="92341-282">Istnieje ograniczenie tooa całkowitej liczby parametrów zapytania 2100, co ogranicza hello całkowitą liczbę wierszy, które mogą być przetwarzane w ten sposób.</span><span class="sxs-lookup"><span data-stu-id="92341-282">You are limited tooa total of 2100 query parameters, so this limits hello total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="92341-283">powitania po ad hoc wydajności hello Pokaż wyniki testu tego typu instrukcji insert w milisekundach.</span><span class="sxs-lookup"><span data-stu-id="92341-283">hello following ad-hoc test results show hello performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="92341-284">Operacje</span><span class="sxs-lookup"><span data-stu-id="92341-284">Operations</span></span> | <span data-ttu-id="92341-285">Parametry z wartościami przechowywanymi w tabeli (ms)</span><span class="sxs-lookup"><span data-stu-id="92341-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="92341-286">Wstaw jednej instrukcji (ms)</span><span class="sxs-lookup"><span data-stu-id="92341-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92341-287">1</span><span class="sxs-lookup"><span data-stu-id="92341-287">1</span></span> |<span data-ttu-id="92341-288">32</span><span class="sxs-lookup"><span data-stu-id="92341-288">32</span></span> |<span data-ttu-id="92341-289">20</span><span class="sxs-lookup"><span data-stu-id="92341-289">20</span></span> |
| <span data-ttu-id="92341-290">10</span><span class="sxs-lookup"><span data-stu-id="92341-290">10</span></span> |<span data-ttu-id="92341-291">30</span><span class="sxs-lookup"><span data-stu-id="92341-291">30</span></span> |<span data-ttu-id="92341-292">25</span><span class="sxs-lookup"><span data-stu-id="92341-292">25</span></span> |
| <span data-ttu-id="92341-293">100</span><span class="sxs-lookup"><span data-stu-id="92341-293">100</span></span> |<span data-ttu-id="92341-294">33</span><span class="sxs-lookup"><span data-stu-id="92341-294">33</span></span> |<span data-ttu-id="92341-295">51</span><span class="sxs-lookup"><span data-stu-id="92341-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="92341-296">Wyniki nie są testy.</span><span class="sxs-lookup"><span data-stu-id="92341-296">Results are not benchmarks.</span></span> <span data-ttu-id="92341-297">Zobacz hello [należy pamiętać o wynikach czasu, w tym temacie](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="92341-297">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="92341-298">Ta metoda może być nieco większą partii, które są mniej niż 100 wierszy.</span><span class="sxs-lookup"><span data-stu-id="92341-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="92341-299">Mimo że ulepszenie hello jest mały, ta metoda jest inną opcją, która może działać również w danym scenariuszu określonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92341-299">Although hello improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="92341-300">Element DataAdapter</span><span class="sxs-lookup"><span data-stu-id="92341-300">DataAdapter</span></span>
<span data-ttu-id="92341-301">Witaj **element DataAdapter** klasa umożliwia toomodify **DataSet** obiekt i spróbuj przesłać zmiany hello operacji INSERT, UPDATE i DELETE.</span><span class="sxs-lookup"><span data-stu-id="92341-301">hello **DataAdapter** class allows you toomodify a **DataSet** object and then submit hello changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="92341-302">Jeśli używasz hello **element DataAdapter** w ten sposób jest ważne, toonote, który upłynąć wywołania są wykonywane dla każdej operacji distinct.</span><span class="sxs-lookup"><span data-stu-id="92341-302">If you are using hello **DataAdapter** in this manner, it is important toonote that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="92341-303">wydajność tooimprove, użyj hello **UpdateBatchSize** właściwości toohello liczba operacji, które należy umieścić w zadaniu wsadowym, w czasie.</span><span class="sxs-lookup"><span data-stu-id="92341-303">tooimprove performance, use hello **UpdateBatchSize** property toohello number of operations that should be batched at a time.</span></span> <span data-ttu-id="92341-304">Aby uzyskać więcej informacji, zobacz [wykonywania wsadowego operacje przy użyciu obiektów DataAdapter](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span><span class="sxs-lookup"><span data-stu-id="92341-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="92341-305">Programu Entity framework</span><span class="sxs-lookup"><span data-stu-id="92341-305">Entity framework</span></span>
<span data-ttu-id="92341-306">Entity Framework nie obsługuje obecnie przetwarzanie wsadowe.</span><span class="sxs-lookup"><span data-stu-id="92341-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="92341-307">Deweloperzy różne społeczności hello podjęto toodemonstrate rozwiązania, takie jak zastąpienie hello **SaveChanges** metody.</span><span class="sxs-lookup"><span data-stu-id="92341-307">Different developers in hello community have attempted toodemonstrate workarounds, such as override hello **SaveChanges** method.</span></span> <span data-ttu-id="92341-308">Ale zazwyczaj są rozwiązania hello aplikacji złożonych i dostosowane toohello i modelu danych.</span><span class="sxs-lookup"><span data-stu-id="92341-308">But hello solutions are typically complex and customized toohello application and data model.</span></span> <span data-ttu-id="92341-309">Hello Entity Framework w witrynie codeplex projektu jest obecnie strona dyskusji na żądanie tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="92341-309">hello Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="92341-310">tooview te informacje, zobacz [spotkania uwagami - 2 sierpień 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span><span class="sxs-lookup"><span data-stu-id="92341-310">tooview this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="92341-311">XML</span><span class="sxs-lookup"><span data-stu-id="92341-311">XML</span></span>
<span data-ttu-id="92341-312">Aby informacje były kompletne uważamy, jest ważne tootalk o XML jako strategii przetwarzanie wsadowe.</span><span class="sxs-lookup"><span data-stu-id="92341-312">For completeness, we feel that it is important tootalk about XML as a batching strategy.</span></span> <span data-ttu-id="92341-313">Jednak użycie hello XML ma nie zalet w porównaniu z innych metod i kilka wady.</span><span class="sxs-lookup"><span data-stu-id="92341-313">However, hello use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="92341-314">podejście Hello jest podobnych tootable o wartościach parametrów, ale plik XML lub ciąg jest przekazywany tooa przechowywane procedury zamiast tabeli zdefiniowane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92341-314">hello approach is similar tootable-valued parameters, but an XML file or string is passed tooa stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="92341-315">procedury przechowywane Hello analizuje polecenia hello hello przechowywane procedury.</span><span class="sxs-lookup"><span data-stu-id="92341-315">hello stored procedure parses hello commands in hello stored procedure.</span></span>

<span data-ttu-id="92341-316">Istnieje kilka wady toothis podejścia:</span><span class="sxs-lookup"><span data-stu-id="92341-316">There are several disadvantages toothis approach:</span></span>

* <span data-ttu-id="92341-317">Praca z danymi XML może być skomplikowane i błąd podatnych na błędy.</span><span class="sxs-lookup"><span data-stu-id="92341-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="92341-318">Podczas analizowania hello XML na powitania bazy danych może być użycie Procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="92341-318">Parsing hello XML on hello database can be CPU-intensive.</span></span>
* <span data-ttu-id="92341-319">W większości przypadków ta metoda jest mniejsza niż parametry przechowywanymi w tabeli.</span><span class="sxs-lookup"><span data-stu-id="92341-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="92341-320">Z tego względu nie jest zalecane użycie hello XML dla partii zapytań.</span><span class="sxs-lookup"><span data-stu-id="92341-320">For these reasons, hello use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="92341-321">Przetwarzanie wsadowe uwagi</span><span class="sxs-lookup"><span data-stu-id="92341-321">Batching considerations</span></span>
<span data-ttu-id="92341-322">Witaj następujące sekcje zawierają więcej wskazówki dotyczące stosowania hello przetwarzanie wsadowe w aplikacjach baz danych SQL.</span><span class="sxs-lookup"><span data-stu-id="92341-322">hello following sections provide more guidance for hello use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="92341-323">Wady i zalety</span><span class="sxs-lookup"><span data-stu-id="92341-323">Tradeoffs</span></span>
<span data-ttu-id="92341-324">W zależności od architektury przetwarzanie wsadowe może obejmować zależności między wydajność i odporność.</span><span class="sxs-lookup"><span data-stu-id="92341-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="92341-325">Na przykład Rozważmy scenariusz hello, których rola użytkownika nieoczekiwanie ulegnie awarii.</span><span class="sxs-lookup"><span data-stu-id="92341-325">For example, consider hello scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="92341-326">W przypadku utraty jednego wiersza danych, wpływ hello jest mniejszy niż wpływ hello utraty duży wsadu nieprzesłane wierszy.</span><span class="sxs-lookup"><span data-stu-id="92341-326">If you lose one row of data, hello impact is smaller than hello impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="92341-327">Istnieje większe ryzyko, gdy bufor wierszy przed ich wysłaniem toohello bazy danych w oknie określonego czasu.</span><span class="sxs-lookup"><span data-stu-id="92341-327">There is a greater risk when you buffer rows before sending them toohello database in a specified time window.</span></span>

<span data-ttu-id="92341-328">Ze względu na to zależnościami ocenić hello typ operacji tego wsadowej.</span><span class="sxs-lookup"><span data-stu-id="92341-328">Because of this tradeoff, evaluate hello type of operations that you batch.</span></span> <span data-ttu-id="92341-329">Bardziej agresywnie partii (większe partie i dłuższy czas systemu windows) przy użyciu danych jest mniej istotny.</span><span class="sxs-lookup"><span data-stu-id="92341-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="92341-330">Rozmiar partii</span><span class="sxs-lookup"><span data-stu-id="92341-330">Batch size</span></span>
<span data-ttu-id="92341-331">Nasze testy nie było zwykle nie partie dużych toobreaking korzystać na mniejsze fragmenty.</span><span class="sxs-lookup"><span data-stu-id="92341-331">In our tests, there was typically no advantage toobreaking large batches into smaller chunks.</span></span> <span data-ttu-id="92341-332">W rzeczywistości często tej części pola spowodowała wolniej niż przesyłanie dużych pojedyncza partia.</span><span class="sxs-lookup"><span data-stu-id="92341-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="92341-333">Na przykład Rozważmy scenariusz, w którym ma być tooinsert 1000 wierszy.</span><span class="sxs-lookup"><span data-stu-id="92341-333">For example, consider a scenario where you want tooinsert 1000 rows.</span></span> <span data-ttu-id="92341-334">Witaj poniższej tabeli przedstawiono czas potrzebny toouse przechowywanymi w tabeli parametrów tooinsert 1000 wierszy, gdy podzielona na mniejsze partie.</span><span class="sxs-lookup"><span data-stu-id="92341-334">hello following table shows how long it takes toouse table-valued parameters tooinsert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="92341-335">Rozmiar partii</span><span class="sxs-lookup"><span data-stu-id="92341-335">Batch size</span></span> | <span data-ttu-id="92341-336">Liczba iteracji</span><span class="sxs-lookup"><span data-stu-id="92341-336">Iterations</span></span> | <span data-ttu-id="92341-337">Parametry z wartościami przechowywanymi w tabeli (ms)</span><span class="sxs-lookup"><span data-stu-id="92341-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92341-338">1000</span><span class="sxs-lookup"><span data-stu-id="92341-338">1000</span></span> |<span data-ttu-id="92341-339">1</span><span class="sxs-lookup"><span data-stu-id="92341-339">1</span></span> |<span data-ttu-id="92341-340">347</span><span class="sxs-lookup"><span data-stu-id="92341-340">347</span></span> |
| <span data-ttu-id="92341-341">500</span><span class="sxs-lookup"><span data-stu-id="92341-341">500</span></span> |<span data-ttu-id="92341-342">2</span><span class="sxs-lookup"><span data-stu-id="92341-342">2</span></span> |<span data-ttu-id="92341-343">355</span><span class="sxs-lookup"><span data-stu-id="92341-343">355</span></span> |
| <span data-ttu-id="92341-344">100</span><span class="sxs-lookup"><span data-stu-id="92341-344">100</span></span> |<span data-ttu-id="92341-345">10</span><span class="sxs-lookup"><span data-stu-id="92341-345">10</span></span> |<span data-ttu-id="92341-346">465</span><span class="sxs-lookup"><span data-stu-id="92341-346">465</span></span> |
| <span data-ttu-id="92341-347">50</span><span class="sxs-lookup"><span data-stu-id="92341-347">50</span></span> |<span data-ttu-id="92341-348">20</span><span class="sxs-lookup"><span data-stu-id="92341-348">20</span></span> |<span data-ttu-id="92341-349">630</span><span class="sxs-lookup"><span data-stu-id="92341-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="92341-350">Wyniki nie są testy.</span><span class="sxs-lookup"><span data-stu-id="92341-350">Results are not benchmarks.</span></span> <span data-ttu-id="92341-351">Zobacz hello [należy pamiętać o wynikach czasu, w tym temacie](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="92341-351">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="92341-352">Widać, że hello najlepszą wydajność 1000 wierszy jest toosubmit ich wszystkich naraz.</span><span class="sxs-lookup"><span data-stu-id="92341-352">You can see that hello best performance for 1000 rows is toosubmit them all at once.</span></span> <span data-ttu-id="92341-353">W innych testach (nie jest tutaj widoczny) wystąpił toobreak przyrost wydajności małych partii 10000 wiersza w dwóch partie 5000.</span><span class="sxs-lookup"><span data-stu-id="92341-353">In other tests (not shown here) there was a small performance gain toobreak a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="92341-354">Ale schemat tabeli hello tych testów jest stosunkowo proste, należy wykonać testy na określonych danych i tooverify rozmiary partii tych wyników.</span><span class="sxs-lookup"><span data-stu-id="92341-354">But hello table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes tooverify these findings.</span></span>

<span data-ttu-id="92341-355">Innym czynnikiem tooconsider jest Jeśli całkowita liczba partii hello stanie się zbyt duży, bazy danych SQL może ograniczenie przepustowości i odmówić toocommit hello partii.</span><span class="sxs-lookup"><span data-stu-id="92341-355">Another factor tooconsider is that if hello total batch becomes too large, SQL Database might throttle and refuse toocommit hello batch.</span></span> <span data-ttu-id="92341-356">Dla uzyskania najlepszych wyników hello testu toodetermine Twojego danego scenariusza Jeśli rozmiar partii idealne.</span><span class="sxs-lookup"><span data-stu-id="92341-356">For hello best results, test your specific scenario toodetermine if there is an ideal batch size.</span></span> <span data-ttu-id="92341-357">Rozmiar partii hello można skonfigurować w wprowadzanie korekt szybkie tooenable środowiska uruchomieniowego na podstawie wydajności lub błędy.</span><span class="sxs-lookup"><span data-stu-id="92341-357">Make hello batch size configurable at runtime tooenable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="92341-358">Ponadto równoważenie hello rozmiar wsadu hello ryzyka hello skojarzone z przetwarzanie wsadowe.</span><span class="sxs-lookup"><span data-stu-id="92341-358">Finally, balance hello size of hello batch with hello risks associated with batching.</span></span> <span data-ttu-id="92341-359">Jeśli ma błędów przejściowych lub roli hello nie powiedzie się, należy wziąć pod uwagę konsekwencje hello ponowną próbą wykonania operacji hello lub utraty danych hello w partii hello.</span><span class="sxs-lookup"><span data-stu-id="92341-359">If there are transient errors or hello role fails, consider hello consequences of retrying hello operation or of losing hello data in hello batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="92341-360">Przetwarzanie równoległe</span><span class="sxs-lookup"><span data-stu-id="92341-360">Parallel processing</span></span>
<span data-ttu-id="92341-361">Co zrobić, jeśli trwało podejście hello zmniejsza rozmiar partii hello, ale używana wiele wątków tooexecute hello pracy?</span><span class="sxs-lookup"><span data-stu-id="92341-361">What if you took hello approach of reducing hello batch size but used multiple threads tooexecute hello work?</span></span> <span data-ttu-id="92341-362">Ponownie Nasze testy wykazały, czy partie mniejszych wielowątkowe najczęściej wykonywane gorsza niż pojedyncza partia większy.</span><span class="sxs-lookup"><span data-stu-id="92341-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="92341-363">Witaj następującego testu prób tooinsert 1000 wierszy w partii równoległych co najmniej jeden.</span><span class="sxs-lookup"><span data-stu-id="92341-363">hello following test attempts tooinsert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="92341-364">Ten test pokazuje, jak więcej jednoczesnych partie faktycznie obniżenie wydajności.</span><span class="sxs-lookup"><span data-stu-id="92341-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="92341-365">Rozmiar partii [iteracji]</span><span class="sxs-lookup"><span data-stu-id="92341-365">Batch size [Iterations]</span></span> | <span data-ttu-id="92341-366">Dwoma wątkami (ms)</span><span class="sxs-lookup"><span data-stu-id="92341-366">Two threads (ms)</span></span> | <span data-ttu-id="92341-367">Cztery wątków (ms)</span><span class="sxs-lookup"><span data-stu-id="92341-367">Four threads (ms)</span></span> | <span data-ttu-id="92341-368">Sześć wątków (ms)</span><span class="sxs-lookup"><span data-stu-id="92341-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="92341-369">1000 [1]</span><span class="sxs-lookup"><span data-stu-id="92341-369">1000 [1]</span></span> |<span data-ttu-id="92341-370">277</span><span class="sxs-lookup"><span data-stu-id="92341-370">277</span></span> |<span data-ttu-id="92341-371">315</span><span class="sxs-lookup"><span data-stu-id="92341-371">315</span></span> |<span data-ttu-id="92341-372">266</span><span class="sxs-lookup"><span data-stu-id="92341-372">266</span></span> |
| <span data-ttu-id="92341-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="92341-373">500 [2]</span></span> |<span data-ttu-id="92341-374">548</span><span class="sxs-lookup"><span data-stu-id="92341-374">548</span></span> |<span data-ttu-id="92341-375">278</span><span class="sxs-lookup"><span data-stu-id="92341-375">278</span></span> |<span data-ttu-id="92341-376">256</span><span class="sxs-lookup"><span data-stu-id="92341-376">256</span></span> |
| <span data-ttu-id="92341-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="92341-377">250 [4]</span></span> |<span data-ttu-id="92341-378">405</span><span class="sxs-lookup"><span data-stu-id="92341-378">405</span></span> |<span data-ttu-id="92341-379">329</span><span class="sxs-lookup"><span data-stu-id="92341-379">329</span></span> |<span data-ttu-id="92341-380">265</span><span class="sxs-lookup"><span data-stu-id="92341-380">265</span></span> |
| <span data-ttu-id="92341-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="92341-381">100 [10]</span></span> |<span data-ttu-id="92341-382">488</span><span class="sxs-lookup"><span data-stu-id="92341-382">488</span></span> |<span data-ttu-id="92341-383">439</span><span class="sxs-lookup"><span data-stu-id="92341-383">439</span></span> |<span data-ttu-id="92341-384">391</span><span class="sxs-lookup"><span data-stu-id="92341-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="92341-385">Wyniki nie są testy.</span><span class="sxs-lookup"><span data-stu-id="92341-385">Results are not benchmarks.</span></span> <span data-ttu-id="92341-386">Zobacz hello [należy pamiętać o wynikach czasu, w tym temacie](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="92341-386">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="92341-387">Istnieje kilka potencjalnych przyczyn hello spadek wydajności z powodu tooparallelism:</span><span class="sxs-lookup"><span data-stu-id="92341-387">There are several potential reasons for hello degradation in performance due tooparallelism:</span></span>

* <span data-ttu-id="92341-388">Istnieje wiele wywołań awarią sieci, zamiast jednego.</span><span class="sxs-lookup"><span data-stu-id="92341-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="92341-389">Wiele operacji na jednej tabeli może spowodować rywalizację i blokowania.</span><span class="sxs-lookup"><span data-stu-id="92341-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="92341-390">Występują ogólne koszty związane z wielowątkowości.</span><span class="sxs-lookup"><span data-stu-id="92341-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="92341-391">wydatków Hello otwarcia wielu połączeń przeważa nad hello zaletą przetwarzania równoległego.</span><span class="sxs-lookup"><span data-stu-id="92341-391">hello expense of opening multiple connections outweighs hello benefit of parallel processing.</span></span>

<span data-ttu-id="92341-392">W przypadku skierowania różnych tabelach lub baz danych, jest możliwe toosee wydajności uzyskania z tej strategii.</span><span class="sxs-lookup"><span data-stu-id="92341-392">If you target different tables or databases, it is possible toosee some performance gain with this strategy.</span></span> <span data-ttu-id="92341-393">Dzielenia na fragmenty bazy danych lub federacje byłoby scenariusz dla tej metody.</span><span class="sxs-lookup"><span data-stu-id="92341-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="92341-394">Dzielenia na fragmenty używa wielu baz danych i bazy danych tooeach różnych danych trasy.</span><span class="sxs-lookup"><span data-stu-id="92341-394">Sharding uses multiple databases and routes different data tooeach database.</span></span> <span data-ttu-id="92341-395">Jeżeli każdej partii małych będzie tooa innej bazy danych, może być skuteczniejsza następnie operacji hello równolegle.</span><span class="sxs-lookup"><span data-stu-id="92341-395">If each small batch is going tooa different database, then performing hello operations in parallel can be more efficient.</span></span> <span data-ttu-id="92341-396">Jednak hello są bardziej wydajne nie jest wystarczająco znaczące toouse jako podstawy hello decyzji toouse bazy danych dzielenia na fragmenty w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="92341-396">However, hello performance gain is not significant enough toouse as hello basis for a decision toouse database sharding in your solution.</span></span>

<span data-ttu-id="92341-397">W niektórych projektach wykonywanie równoległe partii mniejszych może spowodować lepszą przepustowość żądań w systemie pod obciążeniem.</span><span class="sxs-lookup"><span data-stu-id="92341-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="92341-398">W takim przypadku mimo że jest to szybsza tooprocess pojedyncza partia większy, wiele instancji równoległego przetwarzania może być bardziej wydajne.</span><span class="sxs-lookup"><span data-stu-id="92341-398">In this case, even though it is quicker tooprocess a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="92341-399">Jeśli używasz wykonywanie równoległe, należy wziąć pod uwagę kontrolowanie hello maksymalną liczbę wątków roboczych.</span><span class="sxs-lookup"><span data-stu-id="92341-399">If you do use parallel execution, consider controlling hello maximum number of worker threads.</span></span> <span data-ttu-id="92341-400">Mniejsza liczba może spowodować mniej rywalizacji i skrócić czas wykonywania.</span><span class="sxs-lookup"><span data-stu-id="92341-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="92341-401">Należy również rozważyć hello dodatkowego obciążenia, które ten zostaje umieszczony na powitania docelowa baza danych połączenia i transakcji.</span><span class="sxs-lookup"><span data-stu-id="92341-401">Also, consider hello additional load that this places on hello target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="92341-402">Czynniki wydajności związanych z</span><span class="sxs-lookup"><span data-stu-id="92341-402">Related performance factors</span></span>
<span data-ttu-id="92341-403">Typowe wskazówki dotyczące wydajności bazy danych ma wpływ również na przetwarzanie wsadowe.</span><span class="sxs-lookup"><span data-stu-id="92341-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="92341-404">Na przykład, Wstaw wydajność jest ograniczona do tabel, które mają duże kluczem podstawowym lub wiele nieklastrowanych indeksów.</span><span class="sxs-lookup"><span data-stu-id="92341-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="92341-405">Jeśli parametry przechowywanymi w tabeli, użyj procedury składowanej, możesz użyć polecenia hello **SET NOCOUNT ON** na początku hello hello procedury.</span><span class="sxs-lookup"><span data-stu-id="92341-405">If table-valued parameters use a stored procedure, you can use hello command **SET NOCOUNT ON** at hello beginning of hello procedure.</span></span> <span data-ttu-id="92341-406">Ta instrukcja pomija hello powrotu hello liczbę wierszy hello wpływ hello procedury.</span><span class="sxs-lookup"><span data-stu-id="92341-406">This statement suppresses hello return of hello count of hello affected rows in hello procedure.</span></span> <span data-ttu-id="92341-407">Jednak w naszym testy hello użycie **SET NOCOUNT ON** nie miała wpływu albo obniżenie wydajności.</span><span class="sxs-lookup"><span data-stu-id="92341-407">However, in our tests, hello use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="92341-408">Witaj procedury przechowywane testu został proste za pomocą jednej **Wstaw** polecenie hello parametru przechowywanymi w tabeli.</span><span class="sxs-lookup"><span data-stu-id="92341-408">hello test stored procedure was simple with a single **INSERT** command from hello table-valued parameter.</span></span> <span data-ttu-id="92341-409">Istnieje możliwość, że bardziej złożonych procedur składowanych będzie korzystać z tej instrukcji.</span><span class="sxs-lookup"><span data-stu-id="92341-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="92341-410">Ale nie zakłada się, że dodawanie **SET NOCOUNT ON** tooyour przechowywane procedury automatycznie poprawia wydajność.</span><span class="sxs-lookup"><span data-stu-id="92341-410">But don’t assume that adding **SET NOCOUNT ON** tooyour stored procedure automatically improves performance.</span></span> <span data-ttu-id="92341-411">toounderstand hello efekt, przetestować procedurę składowaną z włączonymi i wyłączonymi hello **SET NOCOUNT ON** instrukcji.</span><span class="sxs-lookup"><span data-stu-id="92341-411">toounderstand hello effect, test your stored procedure with and without hello **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="92341-412">Przetwarzanie wsadowe scenariuszy</span><span class="sxs-lookup"><span data-stu-id="92341-412">Batching scenarios</span></span>
<span data-ttu-id="92341-413">Witaj poniższych sekcjach opisano sposób toouse przechowywanymi w tabeli parametrów w trzech scenariuszy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="92341-413">hello following sections describe how toouse table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="92341-414">pierwszy scenariusz Hello pokazuje, jak buforowanie i przetwarzanie wsadowe mogą współdziałać ze sobą.</span><span class="sxs-lookup"><span data-stu-id="92341-414">hello first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="92341-415">drugi scenariusz Hello zwiększa wydajność, wykonując operacje główny szczegółowy w wywołaniu jednej procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="92341-415">hello second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="92341-416">Witaj końcowego scenariuszu przedstawiono sposób toouse przechowywanymi w tabeli parametrów w operacji "UPSERT".</span><span class="sxs-lookup"><span data-stu-id="92341-416">hello final scenario shows how toouse table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="92341-417">Buforowanie</span><span class="sxs-lookup"><span data-stu-id="92341-417">Buffering</span></span>
<span data-ttu-id="92341-418">Istnieje kilka scenariuszy, które są oczywiste candidate dla przetwarzania wsadowego, istnieje wiele scenariuszy, które można wykorzystać przetwarzania wsadowego przez przetwarzanie opóźnione.</span><span class="sxs-lookup"><span data-stu-id="92341-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="92341-419">Jednak również opóźnione przetwarzanie niesie większe ryzyko, że hello dane zostaną utracone w przypadku hello wystąpił nieoczekiwany błąd.</span><span class="sxs-lookup"><span data-stu-id="92341-419">However, delayed processing also carries a greater risk that hello data is lost in hello event of an unexpected failure.</span></span> <span data-ttu-id="92341-420">Jest to zagrożenie toounderstand ważne i należy wziąć pod uwagę konsekwencje hello.</span><span class="sxs-lookup"><span data-stu-id="92341-420">It is important toounderstand this risk and consider hello consequences.</span></span>

<span data-ttu-id="92341-421">Rozważmy na przykład aplikacji sieci web służący do śledzenia historii nawigacji hello każdego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="92341-421">For example, consider a web application that tracks hello navigation history of each user.</span></span> <span data-ttu-id="92341-422">Na każdym żądaniu strony aplikacji hello można utworzyć widok strony użytkownika hello toorecord wywołania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="92341-422">On each page request, hello application could make a database call toorecord hello user’s page view.</span></span> <span data-ttu-id="92341-423">Jednak buforowanie użytkowników hello nawigacji działania, a następnie wysyła tę bazę danych toohello danych w partiach można osiągnąć wyższą wydajność i skalowalność.</span><span class="sxs-lookup"><span data-stu-id="92341-423">But higher performance and scalability can be achieved by buffering hello users’ navigation activities and then sending this data toohello database in batches.</span></span> <span data-ttu-id="92341-424">Możesz wyzwolić hello aktualizacji bazy danych przez czas, który upłynął i/lub rozmiaru buforu.</span><span class="sxs-lookup"><span data-stu-id="92341-424">You can trigger hello database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="92341-425">Na przykład reguła można określić tej partii hello powinna zostać przetworzona po 20 sekund lub gdy bufor hello osiągnie 1000 elementów.</span><span class="sxs-lookup"><span data-stu-id="92341-425">For example, a rule could specify that hello batch should be processed after 20 seconds or when hello buffer reaches 1000 items.</span></span>

<span data-ttu-id="92341-426">następujące Hello przykład kodu wykorzystuje [rozszerzenia reaktywne - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess buforowane zdarzenia wywoływane przez klasę monitorowania.</span><span class="sxs-lookup"><span data-stu-id="92341-426">hello following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess buffered events raised by a monitoring class.</span></span> <span data-ttu-id="92341-427">Gdy hello wypełnienia buforu lub osiągnięto limit czasu, hello partii danych użytkownika jest wysyłana bazy danych toohello z parametrem przechowywanymi w tabeli.</span><span class="sxs-lookup"><span data-stu-id="92341-427">When hello buffer fills or a timeout is reached, hello batch of user data is sent toohello database with a table-valued parameter.</span></span>

<span data-ttu-id="92341-428">Witaj poniższe NavHistoryData klasy modeli hello użytkownika nawigacji informacje.</span><span class="sxs-lookup"><span data-stu-id="92341-428">hello following NavHistoryData class models hello user navigation details.</span></span> <span data-ttu-id="92341-429">Zawiera podstawowe informacje, takie jak identyfikator użytkownika hello, adres URL hello dostęp i hello czas dostępu.</span><span class="sxs-lookup"><span data-stu-id="92341-429">It contains basic information such as hello user identifier, hello URL accessed, and hello access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="92341-430">Witaj NavHistoryDataMonitor klasy jest odpowiedzialny za buforowanie bazy danych toohello danych hello użytkownika nawigacji.</span><span class="sxs-lookup"><span data-stu-id="92341-430">hello NavHistoryDataMonitor class is responsible for buffering hello user navigation data toohello database.</span></span> <span data-ttu-id="92341-431">Zawiera metodę RecordUserNavigationEntry, która odpowiada za wywoływanie **OnAdded** zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="92341-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="92341-432">Witaj poniższy kod przedstawia hello logikę konstruktora, który używa Rx toocreate zauważalne kolekcji na podstawie hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="92341-432">hello following code shows hello constructor logic that uses Rx toocreate an observable collection based on hello event.</span></span> <span data-ttu-id="92341-433">Subskrybuje następnie toothis zauważalne kolekcji z metodą buforu hello.</span><span class="sxs-lookup"><span data-stu-id="92341-433">It then subscribes toothis observable collection with hello Buffer method.</span></span> <span data-ttu-id="92341-434">przeciążenie Hello Określa, że ten bufor hello mają być wysyłane co 20 sekund lub 1000 wpisów.</span><span class="sxs-lookup"><span data-stu-id="92341-434">hello overload specifies that hello buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="92341-435">obsługi Hello konwertuje wszystkie elementy hello buforowane na typ przechowywanymi w tabeli i następnie przekazuje tej procedury przechowywane tooa typu tej partii hello procesów.</span><span class="sxs-lookup"><span data-stu-id="92341-435">hello handler converts all of hello buffered items into a table-valued type and then passes this type tooa stored procedure that processes hello batch.</span></span> <span data-ttu-id="92341-436">Witaj poniższy kod przedstawia hello pełnej definicji hello NavHistoryDataEventArgs i hello NavHistoryDataMonitor klasy.</span><span class="sxs-lookup"><span data-stu-id="92341-436">hello following code shows hello complete definition for both hello NavHistoryDataEventArgs and hello NavHistoryDataMonitor classes.</span></span>

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

<span data-ttu-id="92341-437">toouse tej klasy buforowania aplikacji hello tworzy obiektu NavHistoryDataMonitor statycznego.</span><span class="sxs-lookup"><span data-stu-id="92341-437">toouse this buffering class, hello application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="92341-438">Każdym razem, użytkownik uzyskuje dostęp do strony, aplikacji hello wywołuje metodę NavHistoryDataMonitor.RecordUserNavigationEntry hello.</span><span class="sxs-lookup"><span data-stu-id="92341-438">Each time a user accesses a page, hello application calls hello NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="92341-439">Hello buforowanie logiki przebieg tootake nad wysyła te bazy danych toohello wpisów w partiach.</span><span class="sxs-lookup"><span data-stu-id="92341-439">hello buffering logic proceeds tootake care of sending these entries toohello database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="92341-440">Wzorzec szczegół</span><span class="sxs-lookup"><span data-stu-id="92341-440">Master detail</span></span>
<span data-ttu-id="92341-441">Parametry przechowywanymi w tabeli są przydatne w scenariuszach INSERT proste.</span><span class="sxs-lookup"><span data-stu-id="92341-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="92341-442">Jednak może być trudniejsza wstawia toobatch obejmujące więcej niż jedna tabela.</span><span class="sxs-lookup"><span data-stu-id="92341-442">However, it can be more challenging toobatch inserts that involve more than one table.</span></span> <span data-ttu-id="92341-443">scenariusz "wzorzec/szczegół" Hello jest dobrym przykładem.</span><span class="sxs-lookup"><span data-stu-id="92341-443">hello “master/detail” scenario is a good example.</span></span> <span data-ttu-id="92341-444">główny tabeli Hello identyfikuje hello podstawowej jednostki.</span><span class="sxs-lookup"><span data-stu-id="92341-444">hello master table identifies hello primary entity.</span></span> <span data-ttu-id="92341-445">Co najmniej jedna tabela szczegółów przechowywać więcej danych dotyczących hello jednostki.</span><span class="sxs-lookup"><span data-stu-id="92341-445">One or more detail tables store more data about hello entity.</span></span> <span data-ttu-id="92341-446">W tym scenariuszu relacje klucza obcego wymusić relacji hello szczegóły tooa unikatowe jednostki wzorca.</span><span class="sxs-lookup"><span data-stu-id="92341-446">In this scenario, foreign key relationships enforce hello relationship of details tooa unique master entity.</span></span> <span data-ttu-id="92341-447">Należy wziąć pod uwagę uproszczonej wersji tabeli PurchaseOrder i jego skojarzonej tabeli OrderDetail.</span><span class="sxs-lookup"><span data-stu-id="92341-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="92341-448">Hello następującego języka Transact-SQL tworzy hello PurchaseOrder tabeli z czterech kolumn: OrderID, OrderDate CustomerID i stanu.</span><span class="sxs-lookup"><span data-stu-id="92341-448">hello following Transact-SQL creates hello PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="92341-449">Każdej kolejności zawiera co najmniej jeden produkt.</span><span class="sxs-lookup"><span data-stu-id="92341-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="92341-450">Te informacje są przechwytywane hello PurchaseOrderDetail tabeli.</span><span class="sxs-lookup"><span data-stu-id="92341-450">This information is captured in hello PurchaseOrderDetail table.</span></span> <span data-ttu-id="92341-451">Hello następującego języka Transact-SQL tworzy hello PurchaseOrderDetail tabeli z kolumnami pięć: OrderID, OrderDetailID ProductID, UnitPrice i OrderQty.</span><span class="sxs-lookup"><span data-stu-id="92341-451">hello following Transact-SQL creates hello PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="92341-452">z tabeli PurchaseOrder hello Hello OrderID kolumny w tabeli PurchaseOrderDetail hello musi odwoływać się zamówienia.</span><span class="sxs-lookup"><span data-stu-id="92341-452">hello OrderID column in hello PurchaseOrderDetail table must reference an order from hello PurchaseOrder table.</span></span> <span data-ttu-id="92341-453">po definicji klucza obcego Hello wymusza to ograniczenie.</span><span class="sxs-lookup"><span data-stu-id="92341-453">hello following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="92341-454">W parametrach przechowywanymi w tabeli toouse kolejności musi mieć jeden typ tabeli zdefiniowany przez użytkownika dla każdej tabeli docelowej.</span><span class="sxs-lookup"><span data-stu-id="92341-454">In order toouse table-valued parameters, you must have one user-defined table type for each target table.</span></span>

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

<span data-ttu-id="92341-455">Następnie zdefiniuj procedury przechowywanej, która akceptuje tabele tych typów.</span><span class="sxs-lookup"><span data-stu-id="92341-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="92341-456">Ta procedura umożliwia partii toolocally aplikacji zestaw zleceń i szczegółów zamówienia w pojedynczym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="92341-456">This procedure allows an application toolocally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="92341-457">Witaj następującego języka Transact-SQL zawiera hello deklaracji całą procedurę składowaną w ramach tego przykładu zamówienia zakupu.</span><span class="sxs-lookup"><span data-stu-id="92341-457">hello following Transact-SQL provides hello complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="92341-458">W tym przykładzie hello zdefiniowany lokalnie @IdentityLink w tabeli są przechowywane wartości rzeczywistych OrderID hello hello nowo wstawić wierszy.</span><span class="sxs-lookup"><span data-stu-id="92341-458">In this example, hello locally defined @IdentityLink table stores hello actual OrderID values from hello newly inserted rows.</span></span> <span data-ttu-id="92341-459">Te identyfikatory kolejności różnią się od wartości tymczasowe OrderID hello w hello @orders i @details parametry przechowywanymi w tabeli.</span><span class="sxs-lookup"><span data-stu-id="92341-459">These order identifiers are different from hello temporary OrderID values in hello @orders and @details table-valued parameters.</span></span> <span data-ttu-id="92341-460">Z tego powodu hello @IdentityLink tabeli następnie łączy w wartości OrderID hello hello @orders toohello rzeczywistych OrderID wartości parametrów dla hello nowych wierszy w tabeli PurchaseOrder hello.</span><span class="sxs-lookup"><span data-stu-id="92341-460">For this reason, hello @IdentityLink table then connects hello OrderID values from hello @orders parameter toohello real OrderID values for hello new rows in hello PurchaseOrder table.</span></span> <span data-ttu-id="92341-461">Po wykonaniu tego kroku hello @IdentityLink tabela ułatwia wstawianie szczegółów zamówienia hello z hello rzeczywiste OrderID, spełniająca hello ograniczenie klucza obcego.</span><span class="sxs-lookup"><span data-stu-id="92341-461">After this step, hello @IdentityLink table can facilitate inserting hello order details with hello actual OrderID that satisfies hello foreign key constraint.</span></span>

<span data-ttu-id="92341-462">Tę procedurę składowaną można z kodu lub inne wywołania języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="92341-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="92341-463">W sekcji hello przechowywanymi w tabeli parametrów tego dokumentu, na przykład kodu.</span><span class="sxs-lookup"><span data-stu-id="92341-463">See hello table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="92341-464">Witaj następującego języka Transact-SQL pokazuje, jak toocall hello sp_InsertOrdersBatch.</span><span class="sxs-lookup"><span data-stu-id="92341-464">hello following Transact-SQL shows how toocall hello sp_InsertOrdersBatch.</span></span>

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

<span data-ttu-id="92341-465">To rozwiązanie umożliwia toouse każdej partii zestaw wartości OrderID, które rozpoczynają się do 1.</span><span class="sxs-lookup"><span data-stu-id="92341-465">This solution allows each batch toouse a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="92341-466">Te wartości tymczasowe OrderID opisano relacje hello w partii hello, ale hello rzeczywiste OrderID wartości są określane w czasie hello hello operacji insert.</span><span class="sxs-lookup"><span data-stu-id="92341-466">These temporary OrderID values describe hello relationships in hello batch, but hello actual OrderID values are determined at hello time of hello insert operation.</span></span> <span data-ttu-id="92341-467">Można uruchomić hello tych samych instrukcji w poprzednim przykładzie hello wielokrotnie i wygenerować unikatowy zamówienia hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="92341-467">You can run hello same statements in hello previous example repeatedly and generate unique orders in hello database.</span></span> <span data-ttu-id="92341-468">Z tego powodu należy rozważyć dodanie więcej logiki kodu lub bazy danych, która zapobiega zduplikowane zleceń za pomocą tej techniki partie.</span><span class="sxs-lookup"><span data-stu-id="92341-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="92341-469">W tym przykładzie pokazano, że można zebrać bardziej złożone operacje bazy danych, takimi jak operacje wzorzec szczegół za pomocą parametrów przechowywanymi w tabeli.</span><span class="sxs-lookup"><span data-stu-id="92341-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="92341-470">UPSERT</span><span class="sxs-lookup"><span data-stu-id="92341-470">UPSERT</span></span>
<span data-ttu-id="92341-471">Inny przetwarzanie wsadowe scenariusz obejmuje jednoczesne aktualizowanie istniejących wierszy i wstawianie nowych wierszy.</span><span class="sxs-lookup"><span data-stu-id="92341-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="92341-472">Ta operacja jest czasami tooas określonej operacji "UPSERT" (aktualizacja + insert).</span><span class="sxs-lookup"><span data-stu-id="92341-472">This operation is sometimes referred tooas an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="92341-473">Zamiast wprowadzania tooINSERT wywołań i aktualizacji, instrukcji MERGE hello jest najlepiej nadaje się toothis zadań.</span><span class="sxs-lookup"><span data-stu-id="92341-473">Rather than making separate calls tooINSERT and UPDATE, hello MERGE statement is best suited toothis task.</span></span> <span data-ttu-id="92341-474">Hello instrukcji MERGE można wykonywać zarówno wstawiania i aktualizowania operacji w pojedynczym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="92341-474">hello MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="92341-475">Parametry przechowywanymi w tabeli mogą być używane z aktualizacji tooperform instrukcji MERGE hello i wstawia.</span><span class="sxs-lookup"><span data-stu-id="92341-475">Table-valued parameters can be used with hello MERGE statement tooperform updates and inserts.</span></span> <span data-ttu-id="92341-476">Rozważmy na przykład uproszczony tabeli pracowników, która zawiera następujące kolumny hello: identyfikator pracownika, FirstName, LastName, SocialSecurityNumber:</span><span class="sxs-lookup"><span data-stu-id="92341-476">For example, consider a simplified Employee table that contains hello following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="92341-477">W tym przykładzie można użyć hello fakt, że ten hello SocialSecurityNumber jest unikatowy tooperform scalania wielu pracowników.</span><span class="sxs-lookup"><span data-stu-id="92341-477">In this example, you can use hello fact that hello SocialSecurityNumber is unique tooperform a MERGE of multiple employees.</span></span> <span data-ttu-id="92341-478">Najpierw utwórz hello typu tabeli zdefiniowanego przez użytkownika:</span><span class="sxs-lookup"><span data-stu-id="92341-478">First, create hello user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="92341-479">Następnie utwórz procedurę składowaną lub napisać kod, że używa hello aktualizacji hello tooperform instrukcji MERGE i wstawiania.</span><span class="sxs-lookup"><span data-stu-id="92341-479">Next, create a stored procedure or write code that uses hello MERGE statement tooperform hello update and insert.</span></span> <span data-ttu-id="92341-480">Witaj poniższym przykładzie użyto hello instrukcji MERGE dla parametru przechowywanymi w tabeli, @employees, typu EmployeeTableType.</span><span class="sxs-lookup"><span data-stu-id="92341-480">hello following example uses hello MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="92341-481">Witaj zawartość hello @employees tabeli nie są wyświetlane tutaj.</span><span class="sxs-lookup"><span data-stu-id="92341-481">hello contents of hello @employees table are not shown here.</span></span>

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

<span data-ttu-id="92341-482">Aby uzyskać więcej informacji zobacz hello dokumentacja i przykłady dotyczące hello instrukcji MERGE.</span><span class="sxs-lookup"><span data-stu-id="92341-482">For more information, see hello documentation and examples for hello MERGE statement.</span></span> <span data-ttu-id="92341-483">Mimo że powitalne służbowe może być wykonana w kroku wielu przechowywane wywołania procedury z oddzielnych operacji INSERT i UPDATE, hello instrukcji MERGE jest bardziej wydajny.</span><span class="sxs-lookup"><span data-stu-id="92341-483">Although hello same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, hello MERGE statement is more efficient.</span></span> <span data-ttu-id="92341-484">Kod bazy danych można także konstruować wywołania języka Transact-SQL, które użyj instrukcji MERGE hello bezpośrednio, bez konieczności dwóch wywołania bazy danych dla INSERT i UPDATE.</span><span class="sxs-lookup"><span data-stu-id="92341-484">Database code can also construct Transact-SQL calls that use hello MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="92341-485">Zalecenie podsumowania</span><span class="sxs-lookup"><span data-stu-id="92341-485">Recommendation summary</span></span>
<span data-ttu-id="92341-486">Witaj Poniższa lista zawiera podsumowanie hello przetwarzanie wsadowe zalecenia omówione w tym temacie:</span><span class="sxs-lookup"><span data-stu-id="92341-486">hello following list provides a summary of hello batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="92341-487">Użycie buforowania i przetwarzanie wsadowe tooincrease hello wydajność i skalowalność aplikacji bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="92341-487">Use buffering and batching tooincrease hello performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="92341-488">Zrozumienie wady i zalety hello między przetwarzanie wsadowe buforowania i odporność.</span><span class="sxs-lookup"><span data-stu-id="92341-488">Understand hello tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="92341-489">Podczas awarii roli hello ryzyko utraty nieprzetworzone partii strategicznych danych biznesowych mogą przeważają korzyści hello wydajności przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="92341-489">During a role failure, hello risk of losing an unprocessed batch of business-critical data might outweigh hello performance benefit of batching.</span></span>
* <span data-ttu-id="92341-490">Próba tookeep wszystkie bazy danych toohello wywołań w opóźnienia tooreduce jednego centrum danych.</span><span class="sxs-lookup"><span data-stu-id="92341-490">Attempt tookeep all calls toohello database within a single datacenter tooreduce latency.</span></span>
* <span data-ttu-id="92341-491">Jeśli wybierzesz pojedyncza technika przetwarzanie wsadowe parametry przechowywanymi w tabeli oferują hello najlepszą wydajność i elastyczność.</span><span class="sxs-lookup"><span data-stu-id="92341-491">If you choose a single batching technique, table-valued parameters offer hello best performance and flexibility.</span></span>
* <span data-ttu-id="92341-492">Dla hello najszybszym Wstaw wydajności, wykonaj następujące ogólne wytyczne, ale test danego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="92341-492">For hello fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="92341-493">< 100 wierszy użyj jednego sparametryzowane polecenia INSERT.</span><span class="sxs-lookup"><span data-stu-id="92341-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="92341-494">< 1000 wierszy użyj parametrów przechowywanymi w tabeli.</span><span class="sxs-lookup"><span data-stu-id="92341-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="92341-495">Aby uzyskać > = 1000 wierszy, użyj SqlBulkCopy.</span><span class="sxs-lookup"><span data-stu-id="92341-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="92341-496">Dla aktualizacji i operacji usunięcia, parametry przechowywanymi w tabeli za pomocą procedury składowanej logikę, która określa hello poprawne działanie w każdym wierszu w parametrze tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="92341-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines hello correct operation on each row in hello table parameter.</span></span>
* <span data-ttu-id="92341-497">Informacje dotyczące rozmiaru partii:</span><span class="sxs-lookup"><span data-stu-id="92341-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="92341-498">Użyj hello największy rozmiarów partii odpowiednich dla aplikacji i wymaganiami biznesowymi.</span><span class="sxs-lookup"><span data-stu-id="92341-498">Use hello largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="92341-499">Wydajności hello równoważenia uzyskać dużych partii z ryzykiem hello tymczasowe lub poważnej awarii.</span><span class="sxs-lookup"><span data-stu-id="92341-499">Balance hello performance gain of large batches with hello risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="92341-500">Co to jest konsekwencją hello ponownych prób i utraty danych hello w partii hello?</span><span class="sxs-lookup"><span data-stu-id="92341-500">What is hello consequence of retries or loss of hello data in hello batch?</span></span> 
  * <span data-ttu-id="92341-501">Przetestuj hello największy partii rozmiar tooverify bazy danych SQL go nie odrzucić.</span><span class="sxs-lookup"><span data-stu-id="92341-501">Test hello largest batch size tooverify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="92341-502">Utwórz ustawienia konfiguracji tej partii kontroli, takich jak rozmiar partii hello lub hello buforowania przedział czasu.</span><span class="sxs-lookup"><span data-stu-id="92341-502">Create configuration settings that control batching, such as hello batch size or hello buffering time window.</span></span> <span data-ttu-id="92341-503">Te ustawienia zapewniają elastyczność.</span><span class="sxs-lookup"><span data-stu-id="92341-503">These settings provide flexibility.</span></span> <span data-ttu-id="92341-504">Przetwarzanie wsadowe zachowanie w środowisku produkcyjnym bez ponownego wdrożenia usługi w chmurze hello hello, można zmienić.</span><span class="sxs-lookup"><span data-stu-id="92341-504">You can change hello batching behavior in production without redeploying hello cloud service.</span></span>
* <span data-ttu-id="92341-505">Unikaj wykonywanie równoległe w partii, które pracują na pojedynczej tabeli w jednej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="92341-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="92341-506">Jeśli wybierzesz toodivide pojedyncza partia przez wiele wątków roboczych, uruchom testy toodetermine hello idealne liczba wątków.</span><span class="sxs-lookup"><span data-stu-id="92341-506">If you do choose toodivide a single batch across multiple worker threads, run tests toodetermine hello ideal number of threads.</span></span> <span data-ttu-id="92341-507">Po nieokreślone wartości progowej więcej wątków będzie obniżyć wydajność, a nie powinna ona być.</span><span class="sxs-lookup"><span data-stu-id="92341-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="92341-508">Należy wziąć pod uwagę buforowanie włączone rozmiaru i czasu sposób stosowania przetwarzania wsadowego dla scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="92341-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92341-509">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="92341-509">Next steps</span></span>
<span data-ttu-id="92341-510">Ten artykuł skupia się na sposób projektowania baz danych i techniki tworzenia kodu powiązane toobatching może zwiększyć Twojej aplikacji wydajności i skalowalności.</span><span class="sxs-lookup"><span data-stu-id="92341-510">This article focused on how database design and coding techniques related toobatching can improve your application performance and scalability.</span></span> <span data-ttu-id="92341-511">Ale tylko jeden składnik w ogólnej strategii.</span><span class="sxs-lookup"><span data-stu-id="92341-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="92341-512">Więcej sposobów tooimprove wydajności i skalowalności, zobacz [wytyczne dotyczące wydajności bazy danych SQL Azure dla pojedynczej bazy danych](sql-database-performance-guidance.md) i [zagadnienia dotyczące cen i wydajności dla elastycznej puli](sql-database-elastic-pool-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="92341-512">For more ways tooimprove performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool-guidance.md).</span></span>

