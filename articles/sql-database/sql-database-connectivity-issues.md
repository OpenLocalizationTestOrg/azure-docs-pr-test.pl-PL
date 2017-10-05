---
title: "Napraw błąd połączenia SQL, błąd przejściowy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozwiązywanie problemów, diagnozowanie i zapobieganie błąd połączenia SQL lub Błąd przejściowy w bazie danych SQL Azure. "
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
ms.openlocfilehash: ae081fc0432e36bf9f4d4f06f289386ddce37990
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="02f98-104">Rozwiązywanie problemów, diagnozowanie i unikanie błędów połączenia SQL oraz błędów przejściowych w usłudze SQL Database</span><span class="sxs-lookup"><span data-stu-id="02f98-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="02f98-105">W tym artykule opisano sposób zapobiec, rozwiązywanie problemów z zdiagnozować i ograniczyć błędów połączenia i błędom przejściowym, których aplikacja kliencka napotka przy interakcji z bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="02f98-105">This article describes how to prevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="02f98-106">Dowiedz się, jak skonfigurować logiki ponawiania próby utworzenia parametrów połączenia i inne ustawienia połączenia.</span><span class="sxs-lookup"><span data-stu-id="02f98-106">Learn how to configure retry logic, build the connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="02f98-107">Przejściowe błędy (błędów przejściowych)</span><span class="sxs-lookup"><span data-stu-id="02f98-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="02f98-108">Błąd przejściowy — Ponadto błędu przejściowego - ma podstawową przyczyną, który wkrótce zostanie rozwiązany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="02f98-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="02f98-109">Okazjonalne przyczyną błędów przejściowych jest podczas systemu Azure szybko przenosi zasoby sprzętowe na lepsze równoważenie obciążenia różnych obciążeń.</span><span class="sxs-lookup"><span data-stu-id="02f98-109">An occasional cause of transient errors is when the Azure system quickly shifts hardware resources to better load-balance various workloads.</span></span> <span data-ttu-id="02f98-110">Większość tych zdarzeń ponowne konfigurowanie często Ukończono w mniej niż 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="02f98-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="02f98-111">Podczas tego zakresu czasu ponownej konfiguracji może mieć problemy z łącznością z bazą danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="02f98-111">During this reconfiguration time span, you may have connectivity issues to Azure SQL Database.</span></span> <span data-ttu-id="02f98-112">Nawiązywanie połączenia z bazą danych SQL Azure aplikacje powinny zostać skompilowane oczekiwane w przypadku błędów przejściowych, ich obsługę dzięki implementacji w kodzie ich zamiast udostępniając je do użytkowników jako błędy aplikacji logiki ponawiania próby.</span><span class="sxs-lookup"><span data-stu-id="02f98-112">Applications connecting to Azure SQL Database should be built to expect these transient errors, handle them by implementing retry logic in their code instead of surfacing them to users as application errors.</span></span>

<span data-ttu-id="02f98-113">Jeśli program kliencki używa ADO.NET, program jest powiadamiany o błąd przejściowy przez throw z **SqlException**.</span><span class="sxs-lookup"><span data-stu-id="02f98-113">If your client program is using ADO.NET, your program is told about the transient error by the throw of an **SqlException**.</span></span> <span data-ttu-id="02f98-114">**Numer** właściwości można porównać z listą błędów przejściowych u góry tego tematu: [kody błędów SQL dla aplikacji klienckich, baza danych SQL](sql-database-develop-error-messages.md).</span><span class="sxs-lookup"><span data-stu-id="02f98-114">The **Number** property can be compared against the list of transient errors near the top of the topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="02f98-115">Połączenie i polecenia</span><span class="sxs-lookup"><span data-stu-id="02f98-115">Connection versus command</span></span>
<span data-ttu-id="02f98-116">Będzie ponowić próbę nawiązania połączenia SQL lub ustanawiania go ponownie, w zależności od następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="02f98-116">You'll retry the SQL connection or establish it again, depending on the following:</span></span>

* <span data-ttu-id="02f98-117">**Błąd przejściowy występuje podczas próby połączenia**: połączenie powinno być ponowione po opóźnienia przez kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="02f98-117">**A transient error occurs during a connection try**: The connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="02f98-118">**Błąd przejściowy występuje w ciągu polecenia zapytania SQL**: polecenie należy nie natychmiast wykonać ponownie.</span><span class="sxs-lookup"><span data-stu-id="02f98-118">**A transient error occurs during a SQL query command**: The command should not be immediately retried.</span></span> <span data-ttu-id="02f98-119">Zamiast tego z opóźnieniem, powinny być świeżo nawiązać połączenia.</span><span class="sxs-lookup"><span data-stu-id="02f98-119">Instead, after a delay, the connection should be freshly established.</span></span> <span data-ttu-id="02f98-120">Następnie może zostać powtórzone polecenie.</span><span class="sxs-lookup"><span data-stu-id="02f98-120">Then the command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="02f98-121">Logika ponawiania próby dla błędów przejściowych</span><span class="sxs-lookup"><span data-stu-id="02f98-121">Retry logic for transient errors</span></span>
<span data-ttu-id="02f98-122">Programy klienckie, które od czasu do czasu wystąpienia błędu przejściowego są bardziej niezawodne, jeśli zawierają one logiki ponawiania próby.</span><span class="sxs-lookup"><span data-stu-id="02f98-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="02f98-123">Gdy program komunikuje się z bazą danych SQL Azure za pośrednictwem 3 oprogramowanie pośredniczące strony, zapytanie z dostawcą, czy oprogramowanie pośredniczące zawiera logiki ponawiania próby w przypadku błędów przejściowych.</span><span class="sxs-lookup"><span data-stu-id="02f98-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with the vendor whether the middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="02f98-124">Zasady ponawiania</span><span class="sxs-lookup"><span data-stu-id="02f98-124">Principles for retry</span></span>
* <span data-ttu-id="02f98-125">Próba otwarcia połączenia należy wykonać ponownie, jeśli jest przejściowy błąd.</span><span class="sxs-lookup"><span data-stu-id="02f98-125">An attempt to open a connection should be retried if the error is transient.</span></span>
* <span data-ttu-id="02f98-126">Instrukcję SQL SELECT, który zakończy się niepowodzeniem z powodu błędu przejściowego nie należy bezpośrednio wykonać ponownie.</span><span class="sxs-lookup"><span data-stu-id="02f98-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="02f98-127">Zamiast tego należy ustanowić nowego połączenia, a następnie ponów wyboru.</span><span class="sxs-lookup"><span data-stu-id="02f98-127">Instead, establish a fresh connection, and then retry the SELECT.</span></span>
* <span data-ttu-id="02f98-128">Po instrukcji SQL UPDATE zakończy się niepowodzeniem z powodu błędu przejściowego, powinny można nawiązać połączenia świeże, zanim próba aktualizacji zostanie ponowiona.</span><span class="sxs-lookup"><span data-stu-id="02f98-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before the UPDATE is retried.</span></span>
  
  * <span data-ttu-id="02f98-129">Logika ponawiania musi zapewnić, że ukończono transakcji całą bazę danych lub który cała transakcja zostanie wycofana.</span><span class="sxs-lookup"><span data-stu-id="02f98-129">The retry logic must ensure that either the entire database transaction completed, or that the entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="02f98-130">Inne uwagi dotyczące ponownych prób</span><span class="sxs-lookup"><span data-stu-id="02f98-130">Other considerations for retry</span></span>
* <span data-ttu-id="02f98-131">Pliku wsadowego zostanie automatycznie uruchomiony po godzinach pracy, a które zostanie zakończony przed rano, można przyznać pacjenta bardzo długo interwałów czasu między jego ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="02f98-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford to very patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="02f98-132">Program interfejsu użytkownika należy uwzględnić tendencje ludzi po zbyt długim czasie oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="02f98-132">A user interface program should account for the human tendency to give up after too long a wait.</span></span>
  
  * <span data-ttu-id="02f98-133">Jednak rozwiązania nie może być aby ponowić próbę co kilka sekund, ponieważ te zasady mogą wypełniania system z żądaniami.</span><span class="sxs-lookup"><span data-stu-id="02f98-133">However, the solution must not be to retry every few seconds, because that policy can flood the system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="02f98-134">Zwiększ interwał między ponownymi próbami</span><span class="sxs-lookup"><span data-stu-id="02f98-134">Interval increase between retries</span></span>
<span data-ttu-id="02f98-135">Firma Microsoft zaleca opóźnienie 5 sekund przed ponowną próbą wykonania Twojego pierwszego.</span><span class="sxs-lookup"><span data-stu-id="02f98-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="02f98-136">Ponawianie próby opóźnieniem krótszy niż 5 sekund ryzyka przeciążając uda się rozpoznać usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="02f98-136">Retrying after a delay shorter than 5 seconds risks overwhelming the cloud service.</span></span> <span data-ttu-id="02f98-137">Każda kolejne próby opóźnienie powinien być zwiększany wykładniczo maksymalnie 60 sekund.</span><span class="sxs-lookup"><span data-stu-id="02f98-137">For each subsequent retry the delay should grow exponentially, up to a maximum of 60 seconds.</span></span>

<span data-ttu-id="02f98-138">Omówienie *okresu blokowania* dla klientów używających ADO.NET jest dostępna w [programu SQL Server połączenia buforowanie (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span><span class="sxs-lookup"><span data-stu-id="02f98-138">A discussion of the *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="02f98-139">Można również ustawić maksymalnej liczby ponownych prób zanim program własnym zakończy.</span><span class="sxs-lookup"><span data-stu-id="02f98-139">You might also want to set a maximum number of retries before the program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="02f98-140">Przykłady kodu z logiki ponawiania próby</span><span class="sxs-lookup"><span data-stu-id="02f98-140">Code samples with retry logic</span></span>
<span data-ttu-id="02f98-141">Przykłady kodu z logiki ponawiania próby w różnych językach programowania, są dostępne pod adresem:</span><span class="sxs-lookup"><span data-stu-id="02f98-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="02f98-142">Biblioteki połączeń dla bazy danych SQL i programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="02f98-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="02f98-143">Logika ponawiania testu</span><span class="sxs-lookup"><span data-stu-id="02f98-143">Test your retry logic</span></span>
<span data-ttu-id="02f98-144">Aby przetestować Logika ponawiania, musi symulować lub spowodować błąd, nie można usunąć, gdy program jest nadal uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="02f98-144">To test your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-the-network"></a><span data-ttu-id="02f98-145">Testowanie przez odłączenie od sieci</span><span class="sxs-lookup"><span data-stu-id="02f98-145">Test by disconnecting from the network</span></span>
<span data-ttu-id="02f98-146">Jednym ze sposobów można przetestować Logika ponawiania jest odłączyć od sieci na komputerze klienckim, gdy program jest uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="02f98-146">One way you can test your retry logic is to disconnect your client computer from the network while the program is running.</span></span> <span data-ttu-id="02f98-147">Błąd będą:</span><span class="sxs-lookup"><span data-stu-id="02f98-147">The error will be:</span></span>

* <span data-ttu-id="02f98-148">**SqlException.Number** = 11001</span><span class="sxs-lookup"><span data-stu-id="02f98-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="02f98-149">Komunikat o błędzie: "nie Nieznany host"</span><span class="sxs-lookup"><span data-stu-id="02f98-149">Message: "No such host is known"</span></span>

<span data-ttu-id="02f98-150">W ramach pierwszej ponowienia próby program może Popraw błąd i spróbuj nawiązać.</span><span class="sxs-lookup"><span data-stu-id="02f98-150">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span></span>

<span data-ttu-id="02f98-151">Aby to praktyczne, odłączeniu komputera od sieci przed rozpoczęciem pracy z programem.</span><span class="sxs-lookup"><span data-stu-id="02f98-151">To make this practical, you unplug your computer from the network before you start your program.</span></span> <span data-ttu-id="02f98-152">Następnie program rozpoznaje parametr czas, który powoduje, że program:</span><span class="sxs-lookup"><span data-stu-id="02f98-152">Then your program recognizes a run time parameter that causes the program to:</span></span>

1. <span data-ttu-id="02f98-153">Dodaj tymczasowo 11001 do swojej listy błędów można rozważyć jako przejściowy.</span><span class="sxs-lookup"><span data-stu-id="02f98-153">Temporarily add 11001 to its list of errors to consider as transient.</span></span>
2. <span data-ttu-id="02f98-154">Próba jego pierwszego połączenia w zwykły sposób.</span><span class="sxs-lookup"><span data-stu-id="02f98-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="02f98-155">Po zostanie przechwycony błąd, należy usunąć 11001 z listy.</span><span class="sxs-lookup"><span data-stu-id="02f98-155">After the error is caught, remove 11001 from the list.</span></span>
4. <span data-ttu-id="02f98-156">Wyświetla komunikat informujący użytkownika o podłączenie komputera do sieci.</span><span class="sxs-lookup"><span data-stu-id="02f98-156">Display a message telling the user to plug the computer into the network.</span></span>
   * <span data-ttu-id="02f98-157">Zatrzymać dalsze wykonywanie za pomocą **Console.ReadLine** metody lub okna dialogowego z przycisku OK.</span><span class="sxs-lookup"><span data-stu-id="02f98-157">Pause further execution by using either the **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="02f98-158">Użytkownik naciska klawisz Enter po komputera podłączony do sieci.</span><span class="sxs-lookup"><span data-stu-id="02f98-158">The user presses the Enter key after the computer plugged into the network.</span></span>
5. <span data-ttu-id="02f98-159">Spróbuj ponownie połączyć, oczekiwano Powodzenie.</span><span class="sxs-lookup"><span data-stu-id="02f98-159">Attempt again to connect, expecting success.</span></span>

##### <a name="test-by-misspelling-the-database-name-when-connecting"></a><span data-ttu-id="02f98-160">Testowanie przez nazwę bazy danych. błędy podczas nawiązywania połączenia</span><span class="sxs-lookup"><span data-stu-id="02f98-160">Test by misspelling the database name when connecting</span></span>
<span data-ttu-id="02f98-161">Program można celowo błędnie nazwy użytkownika przed pierwszą próbę połączenia.</span><span class="sxs-lookup"><span data-stu-id="02f98-161">Your program can purposely misspell the user name before the first connection attempt.</span></span> <span data-ttu-id="02f98-162">Błąd będą:</span><span class="sxs-lookup"><span data-stu-id="02f98-162">The error will be:</span></span>

* <span data-ttu-id="02f98-163">**SqlException.Number** = 18456</span><span class="sxs-lookup"><span data-stu-id="02f98-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="02f98-164">Komunikat o błędzie: "Logowanie użytkownika"WRONG_MyUserName"nie powiodło się."</span><span class="sxs-lookup"><span data-stu-id="02f98-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="02f98-165">W ramach pierwszej ponowienia próby program może Popraw błąd i spróbuj nawiązać.</span><span class="sxs-lookup"><span data-stu-id="02f98-165">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span></span>

<span data-ttu-id="02f98-166">Aby to praktyczne, program może rozpoznać parametru czas, który powoduje, że program:</span><span class="sxs-lookup"><span data-stu-id="02f98-166">To make this practical, your program could recognize a run time parameter that causes the program to:</span></span>

1. <span data-ttu-id="02f98-167">Dodaj tymczasowo 18456 do swojej listy błędów można rozważyć jako przejściowy.</span><span class="sxs-lookup"><span data-stu-id="02f98-167">Temporarily add 18456 to its list of errors to consider as transient.</span></span>
2. <span data-ttu-id="02f98-168">Celowo Dodaj "WRONG_" do nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="02f98-168">Purposely add 'WRONG_' to the user name.</span></span>
3. <span data-ttu-id="02f98-169">Po zostanie przechwycony błąd, należy usunąć 18456 z listy.</span><span class="sxs-lookup"><span data-stu-id="02f98-169">After the error is caught, remove 18456 from the list.</span></span>
4. <span data-ttu-id="02f98-170">Usuń "WRONG_" z nazwą użytkownika.</span><span class="sxs-lookup"><span data-stu-id="02f98-170">Remove 'WRONG_' from the user name.</span></span>
5. <span data-ttu-id="02f98-171">Spróbuj ponownie połączyć, oczekiwano Powodzenie.</span><span class="sxs-lookup"><span data-stu-id="02f98-171">Attempt again to connect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="02f98-172">Parametry .NET SqlConnection ponownych prób połączenia</span><span class="sxs-lookup"><span data-stu-id="02f98-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="02f98-173">Jeśli program kliencki łączy się z bazą danych SQL Azure za pomocą klasy .NET Framework **System.Data.SqlClient.SqlConnection**, należy użyć .NET 4.6.1 lub nowszej (lub .NET Core), można wykorzystać jej funkcji ponów próbę połączenia.</span><span class="sxs-lookup"><span data-stu-id="02f98-173">If your client program connects to to Azure SQL Database by using the .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="02f98-174">Szczegóły funkcji są [tutaj](http://go.microsoft.com/fwlink/?linkid=393996).</span><span class="sxs-lookup"><span data-stu-id="02f98-174">Details of the feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points to dn632678.aspx, which links to a downloadable .docx related to SqlClient and SQL Server 2014.
-->


<span data-ttu-id="02f98-175">Podczas budowania [ciąg połączenia](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) dla Twojego **SqlConnection** obiektu, powinny koordynować wartości między następującymi parametrami:</span><span class="sxs-lookup"><span data-stu-id="02f98-175">When you build the [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate the values among the following parameters:</span></span>

* <span data-ttu-id="02f98-176">ConnectRetryCount &nbsp; &nbsp; *(wartość domyślna to 1. Zakres to od 0 do 255).*</span><span class="sxs-lookup"><span data-stu-id="02f98-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="02f98-177">ConnectRetryInterval &nbsp; &nbsp; *(wartość domyślna to 1 sekundę. Zakres to od 1 do 60).*</span><span class="sxs-lookup"><span data-stu-id="02f98-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="02f98-178">Limit czasu połączenia &nbsp; &nbsp; *(wartość domyślna to 15 sekund. Zakres to od 0 do 2147483647)*</span><span class="sxs-lookup"><span data-stu-id="02f98-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="02f98-179">W szczególności wybranej wartości upewnić następujące true równości:</span><span class="sxs-lookup"><span data-stu-id="02f98-179">Specifically, your chosen values should make the following equality true:</span></span>

* <span data-ttu-id="02f98-180">Limit czasu połączenia = ConnectRetryCount * ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="02f98-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="02f98-181">Na przykład jeśli liczba = 3, interwał = 10 sekund, limit czasu równy tylko 29 sekund może nie dość przekazywać system wystarczająco dużo czasu, przez jego ponów 3 i końcowych na łączenie: 29 < 3 * 10.</span><span class="sxs-lookup"><span data-stu-id="02f98-181">For example, if the count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give the system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="02f98-182">Połączenie i polecenia</span><span class="sxs-lookup"><span data-stu-id="02f98-182">Connection versus command</span></span>
<span data-ttu-id="02f98-183">**ConnectRetryCount** i **ConnectRetryInterval** let parametrów z **SqlConnection** obiektu spróbuj ponownie wykonać operację połączenia bez informuje lub bothering programu, takie jak zwracanie formantu do programu.</span><span class="sxs-lookup"><span data-stu-id="02f98-183">The **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry the connect operation without telling or bothering your program, such as returning control to your program.</span></span> <span data-ttu-id="02f98-184">Ponowne próby mogą wystąpić w następujących sytuacjach:</span><span class="sxs-lookup"><span data-stu-id="02f98-184">The retries can occur in the following situations:</span></span>

* <span data-ttu-id="02f98-185">Wywołanie metody mySqlConnection.Open</span><span class="sxs-lookup"><span data-stu-id="02f98-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="02f98-186">Wywołanie metody mySqlConnection.Execute</span><span class="sxs-lookup"><span data-stu-id="02f98-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="02f98-187">Brak subtlety.</span><span class="sxs-lookup"><span data-stu-id="02f98-187">There is a subtlety.</span></span> <span data-ttu-id="02f98-188">Jeśli wystąpi błąd przejściowy podczas Twojej *zapytania* jest wykonywana, Twoje **SqlConnection** obiektu nie connect spróbuj wykonać operację ponownie, a go na pewno nie ponów próbę wykonania zapytania.</span><span class="sxs-lookup"><span data-stu-id="02f98-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry the connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="02f98-189">Jednak **SqlConnection** bardzo szybko sprawdzić połączenie przed wysłaniem kwerendy do wykonania.</span><span class="sxs-lookup"><span data-stu-id="02f98-189">However, **SqlConnection** very quickly checks the connection before sending your query for execution.</span></span> <span data-ttu-id="02f98-190">Jeśli szybkie sprawdzenie wykryje problem z połączeniem **SqlConnection** ponawia operację połączenia.</span><span class="sxs-lookup"><span data-stu-id="02f98-190">If the quick check detects a connection problem, **SqlConnection** retries the connect operation.</span></span> <span data-ttu-id="02f98-191">Jeśli próba powiedzie się, możesz zapytanie jest wysyłane do wykonania.</span><span class="sxs-lookup"><span data-stu-id="02f98-191">If the retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="02f98-192">Czy ConnectRetryCount powinny być połączone z aplikacji logiki ponawiania próby?</span><span class="sxs-lookup"><span data-stu-id="02f98-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="02f98-193">Załóżmy, że aplikacja ma Logika ponawiania niestandardowych niezawodny.</span><span class="sxs-lookup"><span data-stu-id="02f98-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="02f98-194">Może on ponów operację connect 4 godziny.</span><span class="sxs-lookup"><span data-stu-id="02f98-194">It might retry the connect operation 4 times.</span></span> <span data-ttu-id="02f98-195">Jeśli dodasz **ConnectRetryInterval** i **ConnectRetryCount** = 3 do parametrów połączenia, spowoduje zwiększenie liczby ponownych prób do 4 * 3 = 12 ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="02f98-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 to your connection string, you will increase the retry count to 4 * 3 = 12 retries.</span></span> <span data-ttu-id="02f98-196">Może nie ma takich dużą liczbę ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="02f98-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-to-azure-sql-database"></a><span data-ttu-id="02f98-197">Połączenia z bazą danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="02f98-197">Connections to Azure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="02f98-198">Połączenia: Parametry</span><span class="sxs-lookup"><span data-stu-id="02f98-198">Connection: Connection string</span></span>
<span data-ttu-id="02f98-199">Parametry połączenia wymagane do połączenia z bazą danych SQL Azure są nieco inne niż ciąg w celu nawiązania z programu Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="02f98-199">The connection string necessary for connecting to Azure SQL Database is slightly different from the string for connecting to Microsoft SQL Server.</span></span> <span data-ttu-id="02f98-200">Możesz skopiować parametry połączenia bazy danych z [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="02f98-200">You can copy the connection string for your database from the [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="02f98-201">Połączenia: Adres IP</span><span class="sxs-lookup"><span data-stu-id="02f98-201">Connection: IP address</span></span>
<span data-ttu-id="02f98-202">Należy skonfigurować serwer bazy danych SQL, aby akceptował komunikację z adresu IP komputera, który obsługuje program kliencki.</span><span class="sxs-lookup"><span data-stu-id="02f98-202">You must configure the SQL Database server to accept communication from the IP address of the computer that hosts your client program.</span></span> <span data-ttu-id="02f98-203">Można to zrobić, edytując ustawienia zapory za pośrednictwem [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="02f98-203">You do this by editing the firewall settings through the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="02f98-204">Jeśli zapomnisz skonfigurować adres IP, program zakończy się niepowodzeniem, przydatną komunikat o błędzie stwierdzający niezbędne adresu IP.</span><span class="sxs-lookup"><span data-stu-id="02f98-204">If you forget to configure the IP address, your program will fail with a handy error message that states the necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="02f98-205">Aby uzyskać więcej informacji, zobacz: [porady: Konfigurowanie ustawień zapory w bazie danych SQL](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="02f98-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="02f98-206">Połączenia: porty</span><span class="sxs-lookup"><span data-stu-id="02f98-206">Connection: Ports</span></span>
<span data-ttu-id="02f98-207">Zwykle wystarczy upewnij się, że jest otwarty dla komunikacji wychodzącej, na komputerze hostującym program kliencki port 1433.</span><span class="sxs-lookup"><span data-stu-id="02f98-207">Typically you only need to ensure that port 1433 is open for outbound communication, on the computer that hosts you client program.</span></span>

<span data-ttu-id="02f98-208">Na przykład kiedy program kliencki znajduje się na komputerze z systemem Windows, zapory systemu Windows na hoście można otworzyć port 1433:</span><span class="sxs-lookup"><span data-stu-id="02f98-208">For example, when your client program is hosted on a Windows computer, the Windows Firewall on the host enables you to open port 1433:</span></span>

1. <span data-ttu-id="02f98-209">Otwórz Panel sterowania</span><span class="sxs-lookup"><span data-stu-id="02f98-209">Open the Control Panel</span></span>
2. <span data-ttu-id="02f98-210">&gt;Wszystkie elementy Panelu sterowania</span><span class="sxs-lookup"><span data-stu-id="02f98-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="02f98-211">&gt;Zapora systemu Windows</span><span class="sxs-lookup"><span data-stu-id="02f98-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="02f98-212">&gt;Ustawienia zaawansowane</span><span class="sxs-lookup"><span data-stu-id="02f98-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="02f98-213">&gt;Reguły ruchu wychodzącego</span><span class="sxs-lookup"><span data-stu-id="02f98-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="02f98-214">&gt;Akcje</span><span class="sxs-lookup"><span data-stu-id="02f98-214">&gt; Actions</span></span>
7. <span data-ttu-id="02f98-215">&gt;Nowa reguła</span><span class="sxs-lookup"><span data-stu-id="02f98-215">&gt; New Rule</span></span>

<span data-ttu-id="02f98-216">Jeśli program kliencki znajduje się na maszynie wirtualnej platformy Azure (VM), należy przeczytać:</span><span class="sxs-lookup"><span data-stu-id="02f98-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="02f98-217">[Porty inne niż 1433 ADO.NET 4.5 i bazy danych SQL](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="02f98-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="02f98-218">Aby uzyskać informacje dotyczące cofiguration portów i adresów IP, zobacz: [zapory bazy danych SQL Azure](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="02f98-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="02f98-219">Połączenie: ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="02f98-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="02f98-220">Jeśli program korzysta z klas ADO.NET, takich jak **System.Data.SqlClient.SqlConnection** nawiązywania połączenia z bazą danych SQL Azure, zalecane jest użycie .NET Framework w wersji 4.6.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="02f98-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** to connect to Azure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="02f98-221">ADO.NET 4.6.1:</span><span class="sxs-lookup"><span data-stu-id="02f98-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="02f98-222">Bazy danych SQL Azure jest większą niezawodność po otwarciu połączenia przy użyciu **SqlConnection.Open** metody.</span><span class="sxs-lookup"><span data-stu-id="02f98-222">For Azure SQL Database, there is improved reliability when you open a connection by using the **SqlConnection.Open** method.</span></span> <span data-ttu-id="02f98-223">**Otwórz** metoda zawiera teraz najlepsze mechanizmów ponownych prób nakładu pracy w odpowiedzi na błędów przejściowych dla niektórych błędów w określonym przedziale czasu połączenia.</span><span class="sxs-lookup"><span data-stu-id="02f98-223">The **Open** method now incorporates best effort retry mechanisms in response to transient faults, for certain errors within the Connection Timeout period.</span></span>
* <span data-ttu-id="02f98-224">Obsługuje tworzenie puli połączeń.</span><span class="sxs-lookup"><span data-stu-id="02f98-224">Supports connection pooling.</span></span> <span data-ttu-id="02f98-225">W tym skutecznej weryfikacji, który obiekt połączenia udostępnia program działa.</span><span class="sxs-lookup"><span data-stu-id="02f98-225">This includes an efficient verification that the connection object it gives your program is functioning.</span></span>

<span data-ttu-id="02f98-226">Podczas korzystania z obiektu połączenia z puli połączeń, zaleca się, że program tymczasowo zamknąć połączenie, gdy nie jest od razu przy użyciu.</span><span class="sxs-lookup"><span data-stu-id="02f98-226">When you use a connection object from a connection pool, we recommend that your program temporarily close the connection when not immediately using it.</span></span> <span data-ttu-id="02f98-227">Ponowne otwarcie połączenia nie jest kosztowna, sposób tworzenia nowego połączenia.</span><span class="sxs-lookup"><span data-stu-id="02f98-227">Re-opening a connection is not expensive the way creating a new connection is.</span></span>

<span data-ttu-id="02f98-228">Jeśli używasz ADO.NET 4.0 lub wcześniejszym, zaleca się uaktualnienie do najnowszej ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="02f98-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade to the latest ADO.NET.</span></span>

* <span data-ttu-id="02f98-229">Począwszy od listopada 2015 r, możesz [Pobierz ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span><span class="sxs-lookup"><span data-stu-id="02f98-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="02f98-230">Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="02f98-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="02f98-231">Diagnostyka: Test sprawdzający, czy można połączyć z narzędzia</span><span class="sxs-lookup"><span data-stu-id="02f98-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="02f98-232">Jeśli program nie może nawiązać połączenia z bazą danych SQL Azure, jedną opcję diagnostyczne jest próby nawiązania połączenia z programem narzędzia.</span><span class="sxs-lookup"><span data-stu-id="02f98-232">If your program is failing to connect to Azure SQL Database, one diagnostic option is to try to connect with a utility program.</span></span> <span data-ttu-id="02f98-233">W idealnym przypadku narzędzie czy połączenia przy użyciu tej samej bibliotece, używany przez program.</span><span class="sxs-lookup"><span data-stu-id="02f98-233">Ideally the utility would connect by using the same library that your program uses.</span></span>

<span data-ttu-id="02f98-234">Na dowolnym komputerze z systemem Windows możesz spróbować tych narzędzi:</span><span class="sxs-lookup"><span data-stu-id="02f98-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="02f98-235">SQL Server Management Studio (ssms.exe), który jest połączony za pomocą ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="02f98-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="02f98-236">sqlcmd.exe, który jest połączony za pomocą [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span><span class="sxs-lookup"><span data-stu-id="02f98-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="02f98-237">Po nawiązaniu połączenia, należy sprawdzić, czy działa krótkich zapytanie SQL SELECT.</span><span class="sxs-lookup"><span data-stu-id="02f98-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-the-open-ports"></a><span data-ttu-id="02f98-238">Diagnostyka: Sprawdź otwartych portów</span><span class="sxs-lookup"><span data-stu-id="02f98-238">Diagnostics: Check the open ports</span></span>
<span data-ttu-id="02f98-239">Załóżmy, że podejrzewasz, że próby nawiązania połączenia kończy się niepowodzeniem z powodu problemów z portu.</span><span class="sxs-lookup"><span data-stu-id="02f98-239">Suppose you suspect that connection attempts are failing due to port issues.</span></span> <span data-ttu-id="02f98-240">Na komputerze można uruchomić narzędzie, które raportów dotyczących konfiguracji portów.</span><span class="sxs-lookup"><span data-stu-id="02f98-240">On your computer you can run a utility that reports on the port configurations.</span></span>

<span data-ttu-id="02f98-241">W systemie Linux mogą być przydatne następujące narzędzia:</span><span class="sxs-lookup"><span data-stu-id="02f98-241">On Linux the following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="02f98-242">(Zmień wartość przykład na adres IP).</span><span class="sxs-lookup"><span data-stu-id="02f98-242">(Change the example value to be your IP address.)</span></span>

<span data-ttu-id="02f98-243">W systemie Windows [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) narzędzia mogą być pomocne.</span><span class="sxs-lookup"><span data-stu-id="02f98-243">On Windows the [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="02f98-244">Oto przykład wykonywania, który zbadać sytuację portu na serwerze bazy danych SQL Azure i której zostało uruchomione na komputerze przenośnym:</span><span class="sxs-lookup"><span data-stu-id="02f98-244">Here is an example execution that queried the port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting to resolve name to IP address...
Name resolved to 23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="02f98-245">Diagnostycznego: Błędy dziennika</span><span class="sxs-lookup"><span data-stu-id="02f98-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="02f98-246">Problem tymczasowy jest czasami najlepiej zdiagnozowany przez wykrywanie ogólne wzorca przez dni lub tygodnie.</span><span class="sxs-lookup"><span data-stu-id="02f98-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="02f98-247">Klient może pomóc w diagnozy przez funkcję rejestrowania wszystkich błędów napotkaniu.</span><span class="sxs-lookup"><span data-stu-id="02f98-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="02f98-248">Dzięki temu można skorelować wpisy dziennika z danymi błąd, który loguje się wewnętrznie bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="02f98-248">You might be able to correlate the log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="02f98-249">6 biblioteki przedsiębiorstwa (EntLib60) oferuje klas zarządzanych .NET z rejestrowania:</span><span class="sxs-lookup"><span data-stu-id="02f98-249">Enterprise Library 6 (EntLib60) offers .NET managed classes to assist with logging:</span></span>

* [<span data-ttu-id="02f98-250">5 — tak proste, jak objętych poza dziennika: za pomocą bloku rejestrowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="02f98-250">5 - As Easy As Falling Off a Log: Using the Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="02f98-251">Diagnostyka: Sprawdź dzienniki systemu pod kątem błędów</span><span class="sxs-lookup"><span data-stu-id="02f98-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="02f98-252">Poniżej przedstawiono niektóre instrukcji języka Transact-SQL SELECT tego zapytania dzienników błędów oraz innych informacji.</span><span class="sxs-lookup"><span data-stu-id="02f98-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="02f98-253">Zapytanie dziennika</span><span class="sxs-lookup"><span data-stu-id="02f98-253">Query of log</span></span> | <span data-ttu-id="02f98-254">Opis</span><span class="sxs-lookup"><span data-stu-id="02f98-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="02f98-255">[Sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) widok zawiera informacje na temat poszczególnych zdarzeniami, w tym te, które mogą powodować przejściowe błędy lub awarie połączenia.</span><span class="sxs-lookup"><span data-stu-id="02f98-255">The [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="02f98-256">W idealnym przypadku można skorelować **godzina_rozpoczęcia** lub **end_time** wartości informująca, gdy program kliencki wystąpienia problemów.</span><span class="sxs-lookup"><span data-stu-id="02f98-256">Ideally you can correlate the **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="02f98-257">**Porada:** należy połączyć **wzorca** bazy danych, aby uruchomić to.</span><span class="sxs-lookup"><span data-stu-id="02f98-257">**TIP:** You must connect to the **master** database to run this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="02f98-258">[Sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) widoku oferuje zagregowanej liczby typów zdarzeń dla dodatkowych diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="02f98-258">The [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="02f98-259">**Porada:** należy połączyć **wzorca** bazy danych, aby uruchomić to.</span><span class="sxs-lookup"><span data-stu-id="02f98-259">**TIP:** You must connect to the **master** database to run this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-the-sql-database-log"></a><span data-ttu-id="02f98-260">Diagnostyka: Wyszukaj problem zdarzenia w dzienniku bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="02f98-260">Diagnostics: Search for problem events in the SQL Database log</span></span>
<span data-ttu-id="02f98-261">Możesz wyszukać wpisy dotyczące problemu zdarzeń w dzienniku bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="02f98-261">You can search for entries about problem events in the log of Azure SQL Database.</span></span> <span data-ttu-id="02f98-262">Spróbuj następujących instrukcji języka Transact-SQL SELECT **wzorca** bazy danych:</span><span class="sxs-lookup"><span data-stu-id="02f98-262">Try the following Transact-SQL SELECT statement in the **master** database:</span></span>

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


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="02f98-263">Kilka wierszy zwrócony z sys.fn_xe_telemetry_blob_target_read_file</span><span class="sxs-lookup"><span data-stu-id="02f98-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="02f98-264">Następnie jest jak może wyglądać zwróconego wiersza.</span><span class="sxs-lookup"><span data-stu-id="02f98-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="02f98-265">Wartości null, często nie są wartości null w innych wierszy.</span><span class="sxs-lookup"><span data-stu-id="02f98-265">The null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="02f98-266">Biblioteka Enterprise 6</span><span class="sxs-lookup"><span data-stu-id="02f98-266">Enterprise Library 6</span></span>
<span data-ttu-id="02f98-267">6 biblioteki przedsiębiorstwa (EntLib60) to platforma klas .NET ułatwiająca implementację niezawodne klientów usługi w chmurze, z których jeden jest usługą bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="02f98-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is the Azure SQL Database service.</span></span> <span data-ttu-id="02f98-268">Możesz znaleźć przeznaczona do każdego obszaru, w którym można pomóc EntLib60 odwiedzając pierwszy tematy:</span><span class="sxs-lookup"><span data-stu-id="02f98-268">You can locate topics dedicated to each area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="02f98-269">Biblioteka Enterprise 6 kwietnia 2013 r.</span><span class="sxs-lookup"><span data-stu-id="02f98-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="02f98-270">Logika ponawiania do obsługi błędów przejściowych jest jeden obszar, w którym można pomóc EntLib60:</span><span class="sxs-lookup"><span data-stu-id="02f98-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="02f98-271">4 - perseverance, klucz tajny wszystkie sukcesy: za pomocą bloku aplikacji obsługi błędu przejściowego</span><span class="sxs-lookup"><span data-stu-id="02f98-271">4 - Perseverance, Secret of All Triumphs: Using the Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="02f98-272">Kod źródłowy EntLib60 jest dostępna dla publicznego [Pobierz](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span><span class="sxs-lookup"><span data-stu-id="02f98-272">The source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="02f98-273">Microsoft nie planuje wprowadzić dodatkowe aktualizacje funkcji lub aktualizacje konserwacji EntLib.</span><span class="sxs-lookup"><span data-stu-id="02f98-273">Microsoft has no plans to make further feature updates or maintenance updates to EntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="02f98-274">Klasy EntLib60 dla błędów przejściowych i spróbuj ponownie</span><span class="sxs-lookup"><span data-stu-id="02f98-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="02f98-275">Następujące klasy EntLib60 są szczególnie użyteczne w przypadku logiki ponawiania próby.</span><span class="sxs-lookup"><span data-stu-id="02f98-275">The following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="02f98-276">Wszystkie te znajdują się w lub wchodzi w przestrzeni nazw **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span><span class="sxs-lookup"><span data-stu-id="02f98-276">All these  are in, or are further under, the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="02f98-277">*W obszarze nazw **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span><span class="sxs-lookup"><span data-stu-id="02f98-277">*In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="02f98-278">**RetryPolicy** — klasa</span><span class="sxs-lookup"><span data-stu-id="02f98-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="02f98-279">**ExecuteAction** — metoda</span><span class="sxs-lookup"><span data-stu-id="02f98-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="02f98-280">**ExponentialBackoff** — klasa</span><span class="sxs-lookup"><span data-stu-id="02f98-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="02f98-281">**SqlDatabaseTransientErrorDetectionStrategy** — klasa</span><span class="sxs-lookup"><span data-stu-id="02f98-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="02f98-282">**ReliableSqlConnection** — klasa</span><span class="sxs-lookup"><span data-stu-id="02f98-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="02f98-283">**Parametr ExecuteCommand** — metoda</span><span class="sxs-lookup"><span data-stu-id="02f98-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="02f98-284">W obszarze nazw **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="02f98-284">In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="02f98-285">**AlwaysTransientErrorDetectionStrategy** — klasa</span><span class="sxs-lookup"><span data-stu-id="02f98-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="02f98-286">**NeverTransientErrorDetectionStrategy** — klasa</span><span class="sxs-lookup"><span data-stu-id="02f98-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="02f98-287">Poniżej podano linki do informacji na temat EntLib60:</span><span class="sxs-lookup"><span data-stu-id="02f98-287">Here are links to information about EntLib60:</span></span>

* <span data-ttu-id="02f98-288">Bezpłatne [książki pobierania: przewodnik dewelopera do biblioteki Microsoft Enterprise, wydanie 2](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="02f98-288">Free [Book Download: Developer's Guide to Microsoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="02f98-289">Najlepsze rozwiązania: [ponów ogólne wskazówki](../best-practices-retry-general.md) ma znakomity szczegółowym omówieniem logiki ponawiania próby.</span><span class="sxs-lookup"><span data-stu-id="02f98-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="02f98-290">Pobieranie NuGet [Biblioteka Enterprise — Obsługa błędów przejściowych bloku aplikacji w wersji 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="02f98-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-the-logging-block"></a><span data-ttu-id="02f98-291">EntLib60: Rejestrowanie bloku</span><span class="sxs-lookup"><span data-stu-id="02f98-291">EntLib60: The logging block</span></span>
* <span data-ttu-id="02f98-292">Blok rejestrowania jest bardzo elastyczne i można skonfigurować rozwiązanie umożliwiający:</span><span class="sxs-lookup"><span data-stu-id="02f98-292">The Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="02f98-293">Utwórz i wiadomości dziennika są przechowywane w różnych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="02f98-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="02f98-294">Przeprowadzania kategoryzacji i filtrowania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="02f98-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="02f98-295">Zbierz informacje kontekstowe, które jest rejestrowanie przydatne do debugowania i śledzenia, a także do przeprowadzania inspekcji i ogólnych wymagań.</span><span class="sxs-lookup"><span data-stu-id="02f98-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="02f98-296">Blok rejestrowania abstracts funkcji rejestrowania miejsce docelowe dziennika, aby kod aplikacji jest zgodny, niezależnie od lokalizacji i typ magazynu docelowego rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="02f98-296">The Logging block abstracts the logging functionality from the log destination so that the application code is consistent, irrespective of the location and type of the target logging store.</span></span>

<span data-ttu-id="02f98-297">Aby uzyskać więcej informacji, zobacz: [5 - jako łatwe jako objęte poza dziennika: za pomocą bloku rejestrowania aplikacji](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="02f98-297">For details see: [5 - As Easy As Falling Off a Log: Using the Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="02f98-298">Kod źródłowy EntLib60 IsTransient — metoda</span><span class="sxs-lookup"><span data-stu-id="02f98-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="02f98-299">Dalej z **SqlDatabaseTransientErrorDetectionStrategy** klasy, kodu źródłowego C# dla **IsTransient** metody.</span><span class="sxs-lookup"><span data-stu-id="02f98-299">Next, from the **SqlDatabaseTransientErrorDetectionStrategy** class, is the C# source code for the **IsTransient** method.</span></span> <span data-ttu-id="02f98-300">Kod źródłowy wyjaśnia, błędów, które zostały uznane za przejściowych i ponów próbę, począwszy od kwietnia 2013 warta.</span><span class="sxs-lookup"><span data-stu-id="02f98-300">The source code clarifies which errors were considered to be transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="02f98-301">Wiele **//comment** wiersze zostały usunięte z tej kopii, aby wyróżnić czytelności.</span><span class="sxs-lookup"><span data-stu-id="02f98-301">Numerous **//comment** lines have been removed from this copy to emphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in the exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // The service is currently busy. Retry the request after 10 seconds.
            // Code: (reason code to be decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode the reason code from the error message to
            // determine the grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach the decoded values as additional attributes to
            // the original SQL exception.
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
            // The instance of SQL Server you attempted to connect to
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


## <a name="next-steps"></a><span data-ttu-id="02f98-302">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02f98-302">Next steps</span></span>
* <span data-ttu-id="02f98-303">Do rozwiązywania problemów inne typowe problemy z połączeniami bazy danych SQL Azure, odwiedź stronę [Rozwiązywanie problemów z połączeniem z bazą danych SQL Azure](sql-database-troubleshoot-common-connection-issues.md).</span><span class="sxs-lookup"><span data-stu-id="02f98-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues to Azure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="02f98-304">Połączenie z serwerem SQL buforowanie (ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="02f98-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="02f98-305">*Ponawianie próby* jest Apache 2.0 licencjonowane ogólnego przeznaczenia, ponawianie próby biblioteki napisany w **Python**, aby uprościć zadanie dodawania zachowanie ponownych prób do wszystko, co.</span><span class="sxs-lookup"><span data-stu-id="02f98-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, to simplify the task of adding retry behavior to just about anything.</span></span>](https://pypi.python.org/pypi/retrying)

