---
title: "aaaFix błędem połączenia SQL błąd przejściowy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootroubleshoot, diagnozowanie i zapobieganie błąd połączenia SQL lub Błąd przejściowy w bazie danych SQL Azure. "
keywords: "Połączenie SQL, ciąg połączenia, problemy z łącznością, błąd przejściowy, błąd połączenia"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="6f118-104">Rozwiązywanie problemów, diagnozowanie i unikanie błędów połączenia SQL oraz błędów przejściowych w usłudze SQL Database</span><span class="sxs-lookup"><span data-stu-id="6f118-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="6f118-105">W tym artykule opisano, jak tooprevent, rozwiązywanie problemów, diagnozowanie i ograniczyć błędów połączenia i błędom przejściowym, których aplikacja kliencka napotka przy interakcji z bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6f118-105">This article describes how tooprevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="6f118-106">Dowiedz się, jak tooconfigure Logika ponawiania próby utworzenia parametrów połączenia hello i inne ustawienia połączenia.</span><span class="sxs-lookup"><span data-stu-id="6f118-106">Learn how tooconfigure retry logic, build hello connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="6f118-107">Przejściowe błędy (błędów przejściowych)</span><span class="sxs-lookup"><span data-stu-id="6f118-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="6f118-108">Błąd przejściowy — Ponadto błędu przejściowego - ma podstawową przyczyną, który wkrótce zostanie rozwiązany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="6f118-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="6f118-109">Okazjonalne przyczyną błędów przejściowych jest podczas hello systemu Azure szybko przewiduje sprzętu zasobów toobetter równoważenia obciążenia różnych obciążeń.</span><span class="sxs-lookup"><span data-stu-id="6f118-109">An occasional cause of transient errors is when hello Azure system quickly shifts hardware resources toobetter load-balance various workloads.</span></span> <span data-ttu-id="6f118-110">Większość tych zdarzeń ponowne konfigurowanie często Ukończono w mniej niż 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="6f118-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="6f118-111">Podczas tego zakresu czasu ponownej konfiguracji może mieć łączności wystawia tooAzure bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="6f118-111">During this reconfiguration time span, you may have connectivity issues tooAzure SQL Database.</span></span> <span data-ttu-id="6f118-112">Aplikacje łączenie tooAzure bazy danych SQL powinny być utworzone tooexpect tych błędów przejściowych dojścia ich zaimplementowanie ponów logikę w ich kodu zamiast udostępniając je toousers jako błędy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6f118-112">Applications connecting tooAzure SQL Database should be built tooexpect these transient errors, handle them by implementing retry logic in their code instead of surfacing them toousers as application errors.</span></span>

<span data-ttu-id="6f118-113">Jeśli program kliencki używa ADO.NET, program jest powiadamiany o błąd przejściowy hello przez throw hello z **SqlException**.</span><span class="sxs-lookup"><span data-stu-id="6f118-113">If your client program is using ADO.NET, your program is told about hello transient error by hello throw of an **SqlException**.</span></span> <span data-ttu-id="6f118-114">Witaj **numer** właściwości można porównać z hello listę błędów przejściowych u góry hello tematu hello: [kody błędów SQL dla aplikacji klienckich, baza danych SQL](sql-database-develop-error-messages.md).</span><span class="sxs-lookup"><span data-stu-id="6f118-114">hello **Number** property can be compared against hello list of transient errors near hello top of hello topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="6f118-115">Połączenie i polecenia</span><span class="sxs-lookup"><span data-stu-id="6f118-115">Connection versus command</span></span>
<span data-ttu-id="6f118-116">Będzie ponowić próbę nawiązania połączenia SQL hello lub ustanawiania go ponownie, w zależności od następujących hello:</span><span class="sxs-lookup"><span data-stu-id="6f118-116">You'll retry hello SQL connection or establish it again, depending on hello following:</span></span>

* <span data-ttu-id="6f118-117">**Błąd przejściowy występuje podczas próby połączenia**: hello połączenie powinno być ponowione po opóźnienia przez kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="6f118-117">**A transient error occurs during a connection try**: hello connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="6f118-118">**Błąd przejściowy występuje w ciągu polecenia zapytania SQL**: hello polecenia należy nie natychmiast wykonać ponownie.</span><span class="sxs-lookup"><span data-stu-id="6f118-118">**A transient error occurs during a SQL query command**: hello command should not be immediately retried.</span></span> <span data-ttu-id="6f118-119">Zamiast tego z opóźnieniem hello powinien świeżo ustanowić połączenia.</span><span class="sxs-lookup"><span data-stu-id="6f118-119">Instead, after a delay, hello connection should be freshly established.</span></span> <span data-ttu-id="6f118-120">Następnie można ponowić hello polecenia.</span><span class="sxs-lookup"><span data-stu-id="6f118-120">Then hello command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="6f118-121">Logika ponawiania próby dla błędów przejściowych</span><span class="sxs-lookup"><span data-stu-id="6f118-121">Retry logic for transient errors</span></span>
<span data-ttu-id="6f118-122">Programy klienckie, które od czasu do czasu wystąpienia błędu przejściowego są bardziej niezawodne, jeśli zawierają one logiki ponawiania próby.</span><span class="sxs-lookup"><span data-stu-id="6f118-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="6f118-123">Gdy program komunikuje się z bazą danych SQL Azure za pośrednictwem 3 oprogramowanie pośredniczące strony, zapytanie z dostawcą hello, czy oprogramowanie pośredniczące hello zawiera logiki ponawiania próby w przypadku błędów przejściowych.</span><span class="sxs-lookup"><span data-stu-id="6f118-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with hello vendor whether hello middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="6f118-124">Zasady ponawiania</span><span class="sxs-lookup"><span data-stu-id="6f118-124">Principles for retry</span></span>
* <span data-ttu-id="6f118-125">Jeśli błąd hello jest przejściowe, należy wykonać ponownie tooopen próba połączenia.</span><span class="sxs-lookup"><span data-stu-id="6f118-125">An attempt tooopen a connection should be retried if hello error is transient.</span></span>
* <span data-ttu-id="6f118-126">Instrukcję SQL SELECT, który zakończy się niepowodzeniem z powodu błędu przejściowego nie należy bezpośrednio wykonać ponownie.</span><span class="sxs-lookup"><span data-stu-id="6f118-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="6f118-127">Zamiast tego należy ustanowić nowego połączenia, a następnie ponów hello wybierz.</span><span class="sxs-lookup"><span data-stu-id="6f118-127">Instead, establish a fresh connection, and then retry hello SELECT.</span></span>
* <span data-ttu-id="6f118-128">Po instrukcji SQL UPDATE zakończy się niepowodzeniem z powodu błędu przejściowego, należy ustanowić połączenia świeże przed powitalne próba aktualizacji zostanie ponowiona.</span><span class="sxs-lookup"><span data-stu-id="6f118-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before hello UPDATE is retried.</span></span>
  
  * <span data-ttu-id="6f118-129">Logika ponawiania Hello musi zapewnić, że ukończyć transakcji całą bazę danych hello lub tym hello cała transakcja zostanie wycofana.</span><span class="sxs-lookup"><span data-stu-id="6f118-129">hello retry logic must ensure that either hello entire database transaction completed, or that hello entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="6f118-130">Inne uwagi dotyczące ponownych prób</span><span class="sxs-lookup"><span data-stu-id="6f118-130">Other considerations for retry</span></span>
* <span data-ttu-id="6f118-131">Pliku wsadowego zostanie automatycznie uruchomiony po godzinach pracy, a które zostanie zakończony przed rano, akceptowalny toovery pacjenta długo interwałów czasu między jego ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="6f118-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford toovery patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="6f118-132">Program interfejsu użytkownika należy uwzględnić hello człowieka tendencję toogive się po zbyt długim czasie oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="6f118-132">A user interface program should account for hello human tendency toogive up after too long a wait.</span></span>
  
  * <span data-ttu-id="6f118-133">Jednak hello rozwiązania nie może być tooretry co kilka sekund, ponieważ te zasady mogą wypełniania hello system z żądaniami.</span><span class="sxs-lookup"><span data-stu-id="6f118-133">However, hello solution must not be tooretry every few seconds, because that policy can flood hello system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="6f118-134">Zwiększ interwał między ponownymi próbami</span><span class="sxs-lookup"><span data-stu-id="6f118-134">Interval increase between retries</span></span>
<span data-ttu-id="6f118-135">Firma Microsoft zaleca opóźnienie 5 sekund przed ponowną próbą wykonania Twojego pierwszego.</span><span class="sxs-lookup"><span data-stu-id="6f118-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="6f118-136">Ponawia próbę po krótszy niż 5 sekund opóźnienia ryzyko związane z usługą hello utrudnione w chmurze.</span><span class="sxs-lookup"><span data-stu-id="6f118-136">Retrying after a delay shorter than 5 seconds risks overwhelming hello cloud service.</span></span> <span data-ttu-id="6f118-137">Każda kolejne próby opóźnienie hello powinien być zwiększany wykładniczo, zapasowej tooa maksymalnie 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="6f118-137">For each subsequent retry hello delay should grow exponentially, up tooa maximum of 60 seconds.</span></span>

<span data-ttu-id="6f118-138">Omówienie hello *okresu blokowania* dla klientów używających ADO.NET jest dostępna w [programu SQL Server połączenia buforowanie (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f118-138">A discussion of hello *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="6f118-139">Można także tooset maksymalnej liczby ponownych prób zanim hello program własnym zakończy.</span><span class="sxs-lookup"><span data-stu-id="6f118-139">You might also want tooset a maximum number of retries before hello program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="6f118-140">Przykłady kodu z logiki ponawiania próby</span><span class="sxs-lookup"><span data-stu-id="6f118-140">Code samples with retry logic</span></span>
<span data-ttu-id="6f118-141">Przykłady kodu z logiki ponawiania próby w różnych językach programowania, są dostępne pod adresem:</span><span class="sxs-lookup"><span data-stu-id="6f118-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="6f118-142">Biblioteki połączeń dla bazy danych SQL i programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="6f118-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="6f118-143">Logika ponawiania testu</span><span class="sxs-lookup"><span data-stu-id="6f118-143">Test your retry logic</span></span>
<span data-ttu-id="6f118-144">tootest Logika ponawiania należy symulować lub spowodować błąd, nie można usunąć, gdy program jest nadal uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="6f118-144">tootest your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-hello-network"></a><span data-ttu-id="6f118-145">Testowanie przez odłączenie od sieci hello</span><span class="sxs-lookup"><span data-stu-id="6f118-145">Test by disconnecting from hello network</span></span>
<span data-ttu-id="6f118-146">Jednym ze sposobów można przetestować Logika ponawiania jest toodisconnect sieciowej komputera klienckiego z hello hello program jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="6f118-146">One way you can test your retry logic is toodisconnect your client computer from hello network while hello program is running.</span></span> <span data-ttu-id="6f118-147">Błąd Hello będą:</span><span class="sxs-lookup"><span data-stu-id="6f118-147">hello error will be:</span></span>

* <span data-ttu-id="6f118-148">**SqlException.Number** = 11001</span><span class="sxs-lookup"><span data-stu-id="6f118-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="6f118-149">Komunikat o błędzie: "nie Nieznany host"</span><span class="sxs-lookup"><span data-stu-id="6f118-149">Message: "No such host is known"</span></span>

<span data-ttu-id="6f118-150">Jako część hello najpierw ponów próbę, program może poprawić błąd pisowni hello, a następnie spróbuj tooconnect.</span><span class="sxs-lookup"><span data-stu-id="6f118-150">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="6f118-151">toomake tym praktycznych, odłączeniu komputera od sieci hello przed rozpoczęciem pracy z programem.</span><span class="sxs-lookup"><span data-stu-id="6f118-151">toomake this practical, you unplug your computer from hello network before you start your program.</span></span> <span data-ttu-id="6f118-152">Następnie program rozpoznaje parametr czas, który powoduje, że hello program:</span><span class="sxs-lookup"><span data-stu-id="6f118-152">Then your program recognizes a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="6f118-153">Dodaj tymczasowo 11001 tooits listę błędów tooconsider jako przejściowy.</span><span class="sxs-lookup"><span data-stu-id="6f118-153">Temporarily add 11001 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="6f118-154">Próba jego pierwszego połączenia w zwykły sposób.</span><span class="sxs-lookup"><span data-stu-id="6f118-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="6f118-155">Po hello jest zgłoszony błąd, Usuń z listy hello 11001.</span><span class="sxs-lookup"><span data-stu-id="6f118-155">After hello error is caught, remove 11001 from hello list.</span></span>
4. <span data-ttu-id="6f118-156">Wyświetlony komunikat informujący hello użytkownika tooplug hello komputera do sieci hello.</span><span class="sxs-lookup"><span data-stu-id="6f118-156">Display a message telling hello user tooplug hello computer into hello network.</span></span>
   * <span data-ttu-id="6f118-157">Zatrzymać dalsze wykonywanie przy użyciu albo hello **Console.ReadLine** metody lub okna dialogowego z przycisku OK.</span><span class="sxs-lookup"><span data-stu-id="6f118-157">Pause further execution by using either hello **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="6f118-158">Witaj naciśnięciu klawisza Enter hello po hello komputer jest podłączony do sieci hello.</span><span class="sxs-lookup"><span data-stu-id="6f118-158">hello user presses hello Enter key after hello computer plugged into hello network.</span></span>
5. <span data-ttu-id="6f118-159">Spróbuj ponownie wykonać tooconnect, oczekiwano Powodzenie.</span><span class="sxs-lookup"><span data-stu-id="6f118-159">Attempt again tooconnect, expecting success.</span></span>

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a><span data-ttu-id="6f118-160">Testowanie według nazwy bazy danych hello błąd podczas nawiązywania połączenia</span><span class="sxs-lookup"><span data-stu-id="6f118-160">Test by misspelling hello database name when connecting</span></span>
<span data-ttu-id="6f118-161">Program można celowo błędnie hello nazwy użytkownika przed hello pierwszą próbę połączenia.</span><span class="sxs-lookup"><span data-stu-id="6f118-161">Your program can purposely misspell hello user name before hello first connection attempt.</span></span> <span data-ttu-id="6f118-162">Błąd Hello będą:</span><span class="sxs-lookup"><span data-stu-id="6f118-162">hello error will be:</span></span>

* <span data-ttu-id="6f118-163">**SqlException.Number** = 18456</span><span class="sxs-lookup"><span data-stu-id="6f118-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="6f118-164">Komunikat o błędzie: "Logowanie użytkownika"WRONG_MyUserName"nie powiodło się."</span><span class="sxs-lookup"><span data-stu-id="6f118-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="6f118-165">Jako część hello najpierw ponów próbę, program może poprawić błąd pisowni hello, a następnie spróbuj tooconnect.</span><span class="sxs-lookup"><span data-stu-id="6f118-165">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="6f118-166">toomake tym praktycznych, program może rozpoznać parametru czas, który powoduje, że hello program:</span><span class="sxs-lookup"><span data-stu-id="6f118-166">toomake this practical, your program could recognize a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="6f118-167">Dodaj tymczasowo 18456 tooits listę błędów tooconsider jako przejściowy.</span><span class="sxs-lookup"><span data-stu-id="6f118-167">Temporarily add 18456 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="6f118-168">Celowo Dodaj nazwę użytkownika toohello "WRONG_".</span><span class="sxs-lookup"><span data-stu-id="6f118-168">Purposely add 'WRONG_' toohello user name.</span></span>
3. <span data-ttu-id="6f118-169">Po hello jest zgłoszony błąd, Usuń z listy hello 18456.</span><span class="sxs-lookup"><span data-stu-id="6f118-169">After hello error is caught, remove 18456 from hello list.</span></span>
4. <span data-ttu-id="6f118-170">Usuń "WRONG_" z hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6f118-170">Remove 'WRONG_' from hello user name.</span></span>
5. <span data-ttu-id="6f118-171">Spróbuj ponownie wykonać tooconnect, oczekiwano Powodzenie.</span><span class="sxs-lookup"><span data-stu-id="6f118-171">Attempt again tooconnect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="6f118-172">Parametry .NET SqlConnection ponownych prób połączenia</span><span class="sxs-lookup"><span data-stu-id="6f118-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="6f118-173">Jeśli program kliencki łączy tootooAzure bazy danych SQL przy użyciu klasy .NET Framework hello **System.Data.SqlClient.SqlConnection**, należy użyć .NET 4.6.1 lub nowszej (lub .NET Core), można wykorzystać jej funkcji ponów próbę połączenia.</span><span class="sxs-lookup"><span data-stu-id="6f118-173">If your client program connects tootooAzure SQL Database by using hello .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="6f118-174">Szczegóły funkcji hello są [tutaj](http://go.microsoft.com/fwlink/?linkid=393996).</span><span class="sxs-lookup"><span data-stu-id="6f118-174">Details of hello feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


<span data-ttu-id="6f118-175">Podczas budowania hello [ciąg połączenia](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) dla Twojego **SqlConnection** obiektu, powinny koordynować wartości hello wśród hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="6f118-175">When you build hello [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate hello values among hello following parameters:</span></span>

* <span data-ttu-id="6f118-176">ConnectRetryCount &nbsp; &nbsp; *(wartość domyślna to 1. Zakres to od 0 do 255).*</span><span class="sxs-lookup"><span data-stu-id="6f118-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="6f118-177">ConnectRetryInterval &nbsp; &nbsp; *(wartość domyślna to 1 sekundę. Zakres to od 1 do 60).*</span><span class="sxs-lookup"><span data-stu-id="6f118-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="6f118-178">Limit czasu połączenia &nbsp; &nbsp; *(wartość domyślna to 15 sekund. Zakres to od 0 do 2147483647)*</span><span class="sxs-lookup"><span data-stu-id="6f118-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="6f118-179">W szczególności wybranej wartości upewnić powitania po true równości:</span><span class="sxs-lookup"><span data-stu-id="6f118-179">Specifically, your chosen values should make hello following equality true:</span></span>

* <span data-ttu-id="6f118-180">Limit czasu połączenia = ConnectRetryCount * ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="6f118-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="6f118-181">Na przykład, jeśli hello count = 3, interwał = 10 sekund, limit czasu równy tylko 29 sekund może nie dość przekazywać systemu hello wystarczająco dużo czasu, przez jego ponów 3 i końcowych na łączenie: 29 < 3 * 10.</span><span class="sxs-lookup"><span data-stu-id="6f118-181">For example, if hello count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give hello system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="6f118-182">Połączenie i polecenia</span><span class="sxs-lookup"><span data-stu-id="6f118-182">Connection versus command</span></span>
<span data-ttu-id="6f118-183">Hello **ConnectRetryCount** i **ConnectRetryInterval** let parametrów z **SqlConnection** operację łączenia obiektu ponawiania hello bez informuje lub bothering Twojego Program, takich jak zwracanie program tooyour sterowania.</span><span class="sxs-lookup"><span data-stu-id="6f118-183">hello **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry hello connect operation without telling or bothering your program, such as returning control tooyour program.</span></span> <span data-ttu-id="6f118-184">ponowne próby Hello może wystąpić w hello następujące sytuacje:</span><span class="sxs-lookup"><span data-stu-id="6f118-184">hello retries can occur in hello following situations:</span></span>

* <span data-ttu-id="6f118-185">Wywołanie metody mySqlConnection.Open</span><span class="sxs-lookup"><span data-stu-id="6f118-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="6f118-186">Wywołanie metody mySqlConnection.Execute</span><span class="sxs-lookup"><span data-stu-id="6f118-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="6f118-187">Brak subtlety.</span><span class="sxs-lookup"><span data-stu-id="6f118-187">There is a subtlety.</span></span> <span data-ttu-id="6f118-188">Jeśli wystąpi błąd przejściowy podczas Twojej *zapytania* jest wykonywana, Twoje **SqlConnection** obiekt łączy z nie hello ponów próbę wykonania operacji, a następnie go na pewno nie ponów próbę wykonania kwerendy.</span><span class="sxs-lookup"><span data-stu-id="6f118-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry hello connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="6f118-189">Jednak **SqlConnection** bardzo szybko kontroli hello połączenie przed wysłaniem kwerendy do wykonania.</span><span class="sxs-lookup"><span data-stu-id="6f118-189">However, **SqlConnection** very quickly checks hello connection before sending your query for execution.</span></span> <span data-ttu-id="6f118-190">Jeśli szybkie sprawdzenie hello wykryje problem z połączeniem **SqlConnection** operację łączenia hello ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="6f118-190">If hello quick check detects a connection problem, **SqlConnection** retries hello connect operation.</span></span> <span data-ttu-id="6f118-191">Jeśli ponawiania hello zakończy się powodzeniem, możesz zapytanie jest wysyłane do wykonania.</span><span class="sxs-lookup"><span data-stu-id="6f118-191">If hello retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="6f118-192">Czy ConnectRetryCount powinny być połączone z aplikacji logiki ponawiania próby?</span><span class="sxs-lookup"><span data-stu-id="6f118-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="6f118-193">Załóżmy, że aplikacja ma Logika ponawiania niestandardowych niezawodny.</span><span class="sxs-lookup"><span data-stu-id="6f118-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="6f118-194">Może być ponów hello operację łączenia 4 godziny.</span><span class="sxs-lookup"><span data-stu-id="6f118-194">It might retry hello connect operation 4 times.</span></span> <span data-ttu-id="6f118-195">Jeśli dodasz **ConnectRetryInterval** i **ConnectRetryCount** = 3 tooyour parametrów połączenia, zwiększy too4 liczby ponownych prób hello * 3 = 12 ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="6f118-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 tooyour connection string, you will increase hello retry count too4 * 3 = 12 retries.</span></span> <span data-ttu-id="6f118-196">Może nie ma takich dużą liczbę ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="6f118-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a><span data-ttu-id="6f118-197">TooAzure połączenia bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="6f118-197">Connections tooAzure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="6f118-198">Połączenia: Parametry</span><span class="sxs-lookup"><span data-stu-id="6f118-198">Connection: Connection string</span></span>
<span data-ttu-id="6f118-199">Parametry połączenia Hello niezbędną do połączenia tooAzure bazy danych SQL są nieco inne niż ciąg hello podłączania tooMicrosoft programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6f118-199">hello connection string necessary for connecting tooAzure SQL Database is slightly different from hello string for connecting tooMicrosoft SQL Server.</span></span> <span data-ttu-id="6f118-200">Możesz skopiować hello parametry połączenia bazy danych z hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6f118-200">You can copy hello connection string for your database from hello [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="6f118-201">Połączenia: Adres IP</span><span class="sxs-lookup"><span data-stu-id="6f118-201">Connection: IP address</span></span>
<span data-ttu-id="6f118-202">Należy skonfigurować hello bazy danych SQL tooaccept komunikacji z serwerem z adresu IP hello hello komputera, który hostuje program kliencki.</span><span class="sxs-lookup"><span data-stu-id="6f118-202">You must configure hello SQL Database server tooaccept communication from hello IP address of hello computer that hosts your client program.</span></span> <span data-ttu-id="6f118-203">Można to zrobić, edytując ustawienia zapory hello za pośrednictwem hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6f118-203">You do this by editing hello firewall settings through hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="6f118-204">Jeśli zapomnisz adres IP hello tooconfigure programu zakończy się niepowodzeniem, przydatną komunikat o błędzie stwierdzający hello niezbędne adresu IP.</span><span class="sxs-lookup"><span data-stu-id="6f118-204">If you forget tooconfigure hello IP address, your program will fail with a handy error message that states hello necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="6f118-205">Aby uzyskać więcej informacji, zobacz: [porady: Konfigurowanie ustawień zapory w bazie danych SQL](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="6f118-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="6f118-206">Połączenia: porty</span><span class="sxs-lookup"><span data-stu-id="6f118-206">Connection: Ports</span></span>
<span data-ttu-id="6f118-207">Zazwyczaj konieczne tooensure, czy port 1433 jest otwarty dla komunikacji wychodzącej, na komputerze hello, hostującym program kliencki.</span><span class="sxs-lookup"><span data-stu-id="6f118-207">Typically you only need tooensure that port 1433 is open for outbound communication, on hello computer that hosts you client program.</span></span>

<span data-ttu-id="6f118-208">Na przykład gdy program kliencki znajduje się na komputerze z systemem Windows, hello zapory systemu Windows na hoście hello pozwala tooopen portu 1433:</span><span class="sxs-lookup"><span data-stu-id="6f118-208">For example, when your client program is hosted on a Windows computer, hello Windows Firewall on hello host enables you tooopen port 1433:</span></span>

1. <span data-ttu-id="6f118-209">Otwórz Panel sterowania hello</span><span class="sxs-lookup"><span data-stu-id="6f118-209">Open hello Control Panel</span></span>
2. <span data-ttu-id="6f118-210">&gt;Wszystkie elementy Panelu sterowania</span><span class="sxs-lookup"><span data-stu-id="6f118-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="6f118-211">&gt;Zapora systemu Windows</span><span class="sxs-lookup"><span data-stu-id="6f118-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="6f118-212">&gt;Ustawienia zaawansowane</span><span class="sxs-lookup"><span data-stu-id="6f118-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="6f118-213">&gt;Reguły ruchu wychodzącego</span><span class="sxs-lookup"><span data-stu-id="6f118-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="6f118-214">&gt;Akcje</span><span class="sxs-lookup"><span data-stu-id="6f118-214">&gt; Actions</span></span>
7. <span data-ttu-id="6f118-215">&gt;Nowa reguła</span><span class="sxs-lookup"><span data-stu-id="6f118-215">&gt; New Rule</span></span>

<span data-ttu-id="6f118-216">Jeśli program kliencki znajduje się na maszynie wirtualnej platformy Azure (VM), należy przeczytać:</span><span class="sxs-lookup"><span data-stu-id="6f118-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="6f118-217">[Porty inne niż 1433 ADO.NET 4.5 i bazy danych SQL](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="6f118-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="6f118-218">Aby uzyskać informacje dotyczące cofiguration portów i adresów IP, zobacz: [zapory bazy danych SQL Azure](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="6f118-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="6f118-219">Połączenie: ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="6f118-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="6f118-220">Jeśli program korzysta z klas ADO.NET, takich jak **System.Data.SqlClient.SqlConnection** tooAzure tooconnect bazy danych SQL, firma Microsoft zaleca użycie .NET Framework w wersji 4.6.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="6f118-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="6f118-221">ADO.NET 4.6.1:</span><span class="sxs-lookup"><span data-stu-id="6f118-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="6f118-222">Bazy danych SQL Azure jest większą niezawodność po otwarciu połączenia przy użyciu hello **SqlConnection.Open** metody.</span><span class="sxs-lookup"><span data-stu-id="6f118-222">For Azure SQL Database, there is improved reliability when you open a connection by using hello **SqlConnection.Open** method.</span></span> <span data-ttu-id="6f118-223">Witaj **Otwórz** metoda zawiera teraz najlepsze nakładu ponawiania mechanizmy błędy tootransient odpowiedzi, niektóre błędy w określonym przedziale czasu połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="6f118-223">hello **Open** method now incorporates best effort retry mechanisms in response tootransient faults, for certain errors within hello Connection Timeout period.</span></span>
* <span data-ttu-id="6f118-224">Obsługuje tworzenie puli połączeń.</span><span class="sxs-lookup"><span data-stu-id="6f118-224">Supports connection pooling.</span></span> <span data-ttu-id="6f118-225">Obejmuje to efektywne weryfikacji, który hello połączenia obiektu udostępnia program działa.</span><span class="sxs-lookup"><span data-stu-id="6f118-225">This includes an efficient verification that hello connection object it gives your program is functioning.</span></span>

<span data-ttu-id="6f118-226">Podczas korzystania z obiektu połączenia z puli połączeń, zaleca się, czy program tymczasowo zamknąć połączenie hello podczas nie bezpośrednio za pomocą.</span><span class="sxs-lookup"><span data-stu-id="6f118-226">When you use a connection object from a connection pool, we recommend that your program temporarily close hello connection when not immediately using it.</span></span> <span data-ttu-id="6f118-227">Ponowne otwarcie połączenia nie jest kosztowna hello sposób tworzenia nowego połączenia.</span><span class="sxs-lookup"><span data-stu-id="6f118-227">Re-opening a connection is not expensive hello way creating a new connection is.</span></span>

<span data-ttu-id="6f118-228">Jeśli używasz ADO.NET 4.0 lub wcześniejszym, zaleca się uaktualnienie toohello najnowsze ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="6f118-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade toohello latest ADO.NET.</span></span>

* <span data-ttu-id="6f118-229">Począwszy od listopada 2015 r, możesz [Pobierz ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f118-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="6f118-230">Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="6f118-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="6f118-231">Diagnostyka: Test sprawdzający, czy można połączyć z narzędzia</span><span class="sxs-lookup"><span data-stu-id="6f118-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="6f118-232">Jeśli program nie działa prawidłowo tooAzure tooconnect bazy danych SQL, jedną opcję diagnostyczne jest tooconnect tootry za pomocą narzędzia programu.</span><span class="sxs-lookup"><span data-stu-id="6f118-232">If your program is failing tooconnect tooAzure SQL Database, one diagnostic option is tootry tooconnect with a utility program.</span></span> <span data-ttu-id="6f118-233">W idealnym przypadku narzędzie hello będzie łączyć się przy użyciu hello samej bibliotece, używany przez program.</span><span class="sxs-lookup"><span data-stu-id="6f118-233">Ideally hello utility would connect by using hello same library that your program uses.</span></span>

<span data-ttu-id="6f118-234">Na dowolnym komputerze z systemem Windows możesz spróbować tych narzędzi:</span><span class="sxs-lookup"><span data-stu-id="6f118-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="6f118-235">SQL Server Management Studio (ssms.exe), który jest połączony za pomocą ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="6f118-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="6f118-236">sqlcmd.exe, który jest połączony za pomocą [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f118-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="6f118-237">Po nawiązaniu połączenia, należy sprawdzić, czy działa krótkich zapytanie SQL SELECT.</span><span class="sxs-lookup"><span data-stu-id="6f118-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a><span data-ttu-id="6f118-238">Diagnostyka: Sprawdź hello otwartych portów</span><span class="sxs-lookup"><span data-stu-id="6f118-238">Diagnostics: Check hello open ports</span></span>
<span data-ttu-id="6f118-239">Załóżmy, że podejrzewasz, że kończy się niepowodzeniem prób nawiązania połączenia z powodu tooport problemy.</span><span class="sxs-lookup"><span data-stu-id="6f118-239">Suppose you suspect that connection attempts are failing due tooport issues.</span></span> <span data-ttu-id="6f118-240">Na komputerze można uruchomić narzędzie, które raportów dotyczących konfiguracji portów hello.</span><span class="sxs-lookup"><span data-stu-id="6f118-240">On your computer you can run a utility that reports on hello port configurations.</span></span>

<span data-ttu-id="6f118-241">Na powitania Linux mogą być przydatne następujące narzędzia:</span><span class="sxs-lookup"><span data-stu-id="6f118-241">On Linux hello following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="6f118-242">(Zmienić hello przykładzie wartość toobe adresu IP).</span><span class="sxs-lookup"><span data-stu-id="6f118-242">(Change hello example value toobe your IP address.)</span></span>

<span data-ttu-id="6f118-243">W systemie Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) narzędzia mogą być pomocne.</span><span class="sxs-lookup"><span data-stu-id="6f118-243">On Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="6f118-244">Oto wykonywania przykładzie, który proszeni hello sytuacji portu na serwerze bazy danych SQL Azure i której zostało uruchomione na komputerze przenośnym:</span><span class="sxs-lookup"><span data-stu-id="6f118-244">Here is an example execution that queried hello port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="6f118-245">Diagnostycznego: Błędy dziennika</span><span class="sxs-lookup"><span data-stu-id="6f118-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="6f118-246">Problem tymczasowy jest czasami najlepiej zdiagnozowany przez wykrywanie ogólne wzorca przez dni lub tygodnie.</span><span class="sxs-lookup"><span data-stu-id="6f118-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="6f118-247">Klient może pomóc w diagnozy przez funkcję rejestrowania wszystkich błędów napotkaniu.</span><span class="sxs-lookup"><span data-stu-id="6f118-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="6f118-248">Może być możliwe toocorrelate wpisy dziennika hello z danymi błąd, który loguje się wewnętrznie bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6f118-248">You might be able toocorrelate hello log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="6f118-249">6 biblioteki przedsiębiorstwa (EntLib60) oferuje tooassist klas zarządzanych .NET z rejestrowaniem:</span><span class="sxs-lookup"><span data-stu-id="6f118-249">Enterprise Library 6 (EntLib60) offers .NET managed classes tooassist with logging:</span></span>

* [<span data-ttu-id="6f118-250">5 — jako łatwe jako objęte poza dziennika: przy użyciu hello bloku rejestrowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="6f118-250">5 - As Easy As Falling Off a Log: Using hello Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="6f118-251">Diagnostyka: Sprawdź dzienniki systemu pod kątem błędów</span><span class="sxs-lookup"><span data-stu-id="6f118-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="6f118-252">Poniżej przedstawiono niektóre instrukcji języka Transact-SQL SELECT tego zapytania dzienników błędów oraz innych informacji.</span><span class="sxs-lookup"><span data-stu-id="6f118-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="6f118-253">Zapytanie dziennika</span><span class="sxs-lookup"><span data-stu-id="6f118-253">Query of log</span></span> | <span data-ttu-id="6f118-254">Opis</span><span class="sxs-lookup"><span data-stu-id="6f118-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="6f118-255">Witaj [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) widok zawiera informacje na temat poszczególnych zdarzeniami, w tym te, które mogą powodować przejściowe błędy lub awarie połączenia.</span><span class="sxs-lookup"><span data-stu-id="6f118-255">hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="6f118-256">W idealnym przypadku można skorelować hello **godzina_rozpoczęcia** lub **end_time** wartości informująca, gdy program kliencki wystąpienia problemów.</span><span class="sxs-lookup"><span data-stu-id="6f118-256">Ideally you can correlate hello **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="6f118-257">**Porada:** należy połączyć toohello **wzorca** toorun bazy danych to.</span><span class="sxs-lookup"><span data-stu-id="6f118-257">**TIP:** You must connect toohello **master** database toorun this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="6f118-258">Witaj [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) widoku oferuje zagregowanej liczby typów zdarzeń dla dodatkowych diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="6f118-258">hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="6f118-259">**Porada:** należy połączyć toohello **wzorca** toorun bazy danych to.</span><span class="sxs-lookup"><span data-stu-id="6f118-259">**TIP:** You must connect toohello **master** database toorun this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a><span data-ttu-id="6f118-260">Diagnostyka: Wyszukaj problem zdarzeń w dzienniku bazy danych SQL hello</span><span class="sxs-lookup"><span data-stu-id="6f118-260">Diagnostics: Search for problem events in hello SQL Database log</span></span>
<span data-ttu-id="6f118-261">Możesz wyszukać wpisy dotyczące problemu zdarzenia w dzienniku hello bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6f118-261">You can search for entries about problem events in hello log of Azure SQL Database.</span></span> <span data-ttu-id="6f118-262">Spróbuj hello następującej instrukcji języka Transact-SQL SELECT w hello **wzorca** bazy danych:</span><span class="sxs-lookup"><span data-stu-id="6f118-262">Try hello following Transact-SQL SELECT statement in hello **master** database:</span></span>

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="6f118-263">Kilka wierszy zwrócony z sys.fn_xe_telemetry_blob_target_read_file</span><span class="sxs-lookup"><span data-stu-id="6f118-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="6f118-264">Następnie jest jak może wyglądać zwróconego wiersza.</span><span class="sxs-lookup"><span data-stu-id="6f118-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="6f118-265">wartości zerowe Hello pokazano często nie mają wartości null w innych wierszy.</span><span class="sxs-lookup"><span data-stu-id="6f118-265">hello null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="6f118-266">Biblioteka Enterprise 6</span><span class="sxs-lookup"><span data-stu-id="6f118-266">Enterprise Library 6</span></span>
<span data-ttu-id="6f118-267">6 biblioteki przedsiębiorstwa (EntLib60) to platforma klas .NET ułatwiająca implementację niezawodne klientów usługi w chmurze, z których jeden jest usługą bazy danych SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6f118-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is hello Azure SQL Database service.</span></span> <span data-ttu-id="6f118-268">Możesz znaleźć, obszar dedykowanych tooeach tematy, w którym EntLib60 może pomóc odwiedzając pierwszy:</span><span class="sxs-lookup"><span data-stu-id="6f118-268">You can locate topics dedicated tooeach area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="6f118-269">Biblioteka Enterprise 6 kwietnia 2013 r.</span><span class="sxs-lookup"><span data-stu-id="6f118-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="6f118-270">Logika ponawiania do obsługi błędów przejściowych jest jeden obszar, w którym można pomóc EntLib60:</span><span class="sxs-lookup"><span data-stu-id="6f118-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="6f118-271">4 - perseverance, klucz tajny wszystkie sukcesy: przy użyciu hello bloku aplikacji obsługi błędów przejściowych</span><span class="sxs-lookup"><span data-stu-id="6f118-271">4 - Perseverance, Secret of All Triumphs: Using hello Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="6f118-272">Witaj EntLib60 kod źródłowy jest dostępny dla publicznego [Pobierz](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span><span class="sxs-lookup"><span data-stu-id="6f118-272">hello source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="6f118-273">Firma Microsoft nie ma funkcji dalsze toomake planów aktualizacji lub konserwacji tooEntLib aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="6f118-273">Microsoft has no plans toomake further feature updates or maintenance updates tooEntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="6f118-274">Klasy EntLib60 dla błędów przejściowych i spróbuj ponownie</span><span class="sxs-lookup"><span data-stu-id="6f118-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="6f118-275">następujące klasy EntLib60 Hello są szczególnie użyteczne w przypadku logiki ponawiania próby.</span><span class="sxs-lookup"><span data-stu-id="6f118-275">hello following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="6f118-276">Wszystkie te znajdują się w lub wchodzi w, hello przestrzeni nazw **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span><span class="sxs-lookup"><span data-stu-id="6f118-276">All these  are in, or are further under, hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="6f118-277">*W obszarze nazw hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span><span class="sxs-lookup"><span data-stu-id="6f118-277">*In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="6f118-278">**RetryPolicy** — klasa</span><span class="sxs-lookup"><span data-stu-id="6f118-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="6f118-279">**ExecuteAction** — metoda</span><span class="sxs-lookup"><span data-stu-id="6f118-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="6f118-280">**ExponentialBackoff** — klasa</span><span class="sxs-lookup"><span data-stu-id="6f118-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="6f118-281">**SqlDatabaseTransientErrorDetectionStrategy** — klasa</span><span class="sxs-lookup"><span data-stu-id="6f118-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="6f118-282">**ReliableSqlConnection** — klasa</span><span class="sxs-lookup"><span data-stu-id="6f118-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="6f118-283">**Parametr ExecuteCommand** — metoda</span><span class="sxs-lookup"><span data-stu-id="6f118-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="6f118-284">W obszarze nazw hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="6f118-284">In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="6f118-285">**AlwaysTransientErrorDetectionStrategy** — klasa</span><span class="sxs-lookup"><span data-stu-id="6f118-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="6f118-286">**NeverTransientErrorDetectionStrategy** — klasa</span><span class="sxs-lookup"><span data-stu-id="6f118-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="6f118-287">Oto łącza tooinformation o EntLib60:</span><span class="sxs-lookup"><span data-stu-id="6f118-287">Here are links tooinformation about EntLib60:</span></span>

* <span data-ttu-id="6f118-288">Bezpłatne [Pobierz książkę: tooMicrosoft przewodnik dewelopera biblioteki Enterprise wydanie 2](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="6f118-288">Free [Book Download: Developer's Guide tooMicrosoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="6f118-289">Najlepsze rozwiązania: [ponów ogólne wskazówki](../best-practices-retry-general.md) ma znakomity szczegółowym omówieniem logiki ponawiania próby.</span><span class="sxs-lookup"><span data-stu-id="6f118-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="6f118-290">Pobieranie NuGet [Biblioteka Enterprise — Obsługa błędów przejściowych bloku aplikacji w wersji 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="6f118-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a><span data-ttu-id="6f118-291">EntLib60: blok rejestrowania hello</span><span class="sxs-lookup"><span data-stu-id="6f118-291">EntLib60: hello logging block</span></span>
* <span data-ttu-id="6f118-292">Blok rejestrowania Hello jest bardzo elastyczne i można skonfigurować rozwiązanie umożliwiający:</span><span class="sxs-lookup"><span data-stu-id="6f118-292">hello Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="6f118-293">Utwórz i wiadomości dziennika są przechowywane w różnych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="6f118-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="6f118-294">Przeprowadzania kategoryzacji i filtrowania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="6f118-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="6f118-295">Zbierz informacje kontekstowe, które jest rejestrowanie przydatne do debugowania i śledzenia, a także do przeprowadzania inspekcji i ogólnych wymagań.</span><span class="sxs-lookup"><span data-stu-id="6f118-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="6f118-296">Witaj rejestrowania bloku streszczenia Witaj logowania funkcji z hello miejsce docelowe dziennika, aby kod aplikacji hello jest spójne, niezależnie od hello lokalizację i typ magazynu rejestrowania docelowego hello.</span><span class="sxs-lookup"><span data-stu-id="6f118-296">hello Logging block abstracts hello logging functionality from hello log destination so that hello application code is consistent, irrespective of hello location and type of hello target logging store.</span></span>

<span data-ttu-id="6f118-297">Aby uzyskać więcej informacji, zobacz: [5 - jako łatwe jako objęte poza dziennika: przy użyciu rejestrowania bloku aplikacji hello](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="6f118-297">For details see: [5 - As Easy As Falling Off a Log: Using hello Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="6f118-298">Kod źródłowy EntLib60 IsTransient — metoda</span><span class="sxs-lookup"><span data-stu-id="6f118-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="6f118-299">Dalej z hello **SqlDatabaseTransientErrorDetectionStrategy** klasa, jest kod źródłowy hello C# hello **IsTransient** metody.</span><span class="sxs-lookup"><span data-stu-id="6f118-299">Next, from hello **SqlDatabaseTransientErrorDetectionStrategy** class, is hello C# source code for hello **IsTransient** method.</span></span> <span data-ttu-id="6f118-300">Kod źródłowy Hello wyjaśnia, błędów, które zostały uznane za przejściowy toobe i ponów próbę, począwszy od kwietnia 2013 warta.</span><span class="sxs-lookup"><span data-stu-id="6f118-300">hello source code clarifies which errors were considered toobe transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="6f118-301">Wiele **//comment** wiersze zostały usunięte z tej kopii tooemphasize czytelności.</span><span class="sxs-lookup"><span data-stu-id="6f118-301">Numerous **//comment** lines have been removed from this copy tooemphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // hello instance of SQL Server you attempted tooconnect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a><span data-ttu-id="6f118-302">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6f118-302">Next steps</span></span>
* <span data-ttu-id="6f118-303">Do rozwiązywania problemów inne typowe problemy z połączeniami bazy danych SQL Azure, odwiedź stronę [połączenia Rozwiązywanie problemów tooAzure bazy danych SQL](sql-database-troubleshoot-common-connection-issues.md).</span><span class="sxs-lookup"><span data-stu-id="6f118-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues tooAzure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="6f118-304">Połączenie z serwerem SQL buforowanie (ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="6f118-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="6f118-305">*Ponawianie próby* jest Apache 2.0 licencjonowane ogólnego przeznaczenia, ponawianie próby biblioteki napisany w **Python**, toosimplify hello zadania dodawania ponawiania toojust zachowanie dotyczące wszystkich elementów.</span><span class="sxs-lookup"><span data-stu-id="6f118-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, toosimplify hello task of adding retry behavior toojust about anything.</span></span>](https://pypi.python.org/pypi/retrying)

