---
title: "Analiza strumienia: Obracanie poświadczenia logowania dla danych wejściowych i wyjściowych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zaktualizować poświadczenia dla usługi analiza strumienia danych wejściowych i wyjściowych."
keywords: "poświadczenia logowania"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 2cb995a3969a8cb025f371ed0ab160cd04b0454d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="db77f-104">Obróć poświadczenia logowania dla wejścia i wyjścia w zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="db77f-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="db77f-105">Abstrakcyjny</span><span class="sxs-lookup"><span data-stu-id="db77f-105">Abstract</span></span>
<span data-ttu-id="db77f-106">Usługa Azure Stream Analytics obecnie nie zezwala na zastępowanie poświadczeń na wejścia/wyjścia podczas uruchamiania zadania.</span><span class="sxs-lookup"><span data-stu-id="db77f-106">Azure Stream Analytics today doesn’t allow replacing the credentials on an input/output while the job is running.</span></span>

<span data-ttu-id="db77f-107">Gdy usługi Azure Stream Analytics obsługuje wznawianie zadania z ostatnich danych wyjściowych, możemy udostępniać cały proces minimalizując zwłokę między zatrzymywanie i uruchamianie zadania i obracanie poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="db77f-107">While Azure Stream Analytics does support resuming a job from last output, we wanted to share the entire process for minimizing the lag between the stopping and starting of the job and rotating the login credentials.</span></span>

## <a name="part-1---prepare-the-new-set-of-credentials"></a><span data-ttu-id="db77f-108">Część 1 — przygotowanie nowego zestawu poświadczeń:</span><span class="sxs-lookup"><span data-stu-id="db77f-108">Part 1 - Prepare the new set of credentials:</span></span>
<span data-ttu-id="db77f-109">Ta część dotyczy wejścia/wyjścia:</span><span class="sxs-lookup"><span data-stu-id="db77f-109">This part is applicable to the following inputs/outputs:</span></span>

* <span data-ttu-id="db77f-110">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="db77f-110">Blob Storage</span></span>
* <span data-ttu-id="db77f-111">Usługa Event Hubs</span><span class="sxs-lookup"><span data-stu-id="db77f-111">Event Hubs</span></span>
* <span data-ttu-id="db77f-112">SQL Database</span><span class="sxs-lookup"><span data-stu-id="db77f-112">SQL Database</span></span>
* <span data-ttu-id="db77f-113">Table Storage</span><span class="sxs-lookup"><span data-stu-id="db77f-113">Table Storage</span></span>

<span data-ttu-id="db77f-114">Dla innych wejść/wyjść przejdź do części 2.</span><span class="sxs-lookup"><span data-stu-id="db77f-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="db77f-115">Magazyn obiektów blob magazynu/tabeli.</span><span class="sxs-lookup"><span data-stu-id="db77f-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="db77f-116">Przejdź do rozszerzenie magazynu w portalu zarządzania Azure:</span><span class="sxs-lookup"><span data-stu-id="db77f-116">Go to the Storage extention on the Azure Management portal:</span></span>  
   ![graphic1][graphic1]
2. <span data-ttu-id="db77f-118">Zlokalizuj miejsca używanego przez zadanie, a następnie przejdź w niej:</span><span class="sxs-lookup"><span data-stu-id="db77f-118">Locate the storage used by your job and go into it:</span></span>  
   ![graphic2][graphic2]
3. <span data-ttu-id="db77f-120">Kliknij polecenie Zarządzaj kluczami dostępu:</span><span class="sxs-lookup"><span data-stu-id="db77f-120">Click the Manage Access Keys command:</span></span>  
   ![graphic3][graphic3]
4. <span data-ttu-id="db77f-122">Między podstawowy klucz dostępu i pomocniczy klucz dostępu **pobrania nie jest używany przez zadanie**.</span><span class="sxs-lookup"><span data-stu-id="db77f-122">Between the Primary Access Key and the Secondary Access Key, **pick the one not used by your job**.</span></span>
5. <span data-ttu-id="db77f-123">Regenerate trafień:</span><span class="sxs-lookup"><span data-stu-id="db77f-123">Hit regenerate:</span></span>  
   ![graphic4][graphic4]
6. <span data-ttu-id="db77f-125">Skopiuj nowo wygenerowany klucz:</span><span class="sxs-lookup"><span data-stu-id="db77f-125">Copy the newly generated key:</span></span>  
   ![graphic5][graphic5]
7. <span data-ttu-id="db77f-127">Nadal część 2.</span><span class="sxs-lookup"><span data-stu-id="db77f-127">Continue to Part 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="db77f-128">Centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="db77f-128">Event hubs</span></span>
1. <span data-ttu-id="db77f-129">Przejdź do rozszerzenia usługi Service Bus w portalu zarządzania Azure:</span><span class="sxs-lookup"><span data-stu-id="db77f-129">Go to the Service Bus extension on the Azure Management portal:</span></span>  
   ![graphic6][graphic6]
2. <span data-ttu-id="db77f-131">Zlokalizuj Namespace magistrali usług, które są używane przez zadanie, a następnie przejdź w niej:</span><span class="sxs-lookup"><span data-stu-id="db77f-131">Locate the Service Bus Namespace used by your job and go into it:</span></span>  
   ![graphic7][graphic7]
3. <span data-ttu-id="db77f-133">Jeśli zadanie używa zasady dostępu współużytkowanego na Namespace magistrali usługi, należy przejść do kroku 6</span><span class="sxs-lookup"><span data-stu-id="db77f-133">If your job uses a shared access policy on the Service Bus Namespace, jump to step 6</span></span>  
4. <span data-ttu-id="db77f-134">Przejdź do karty centra zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="db77f-134">Go to the Event Hubs tab:</span></span>  
   ![graphic8][graphic8]
5. <span data-ttu-id="db77f-136">Zlokalizuj Centrum zdarzeń, używane przez zadania, a następnie przejdź w niej:</span><span class="sxs-lookup"><span data-stu-id="db77f-136">Locate the Event Hub used by your job and go into it:</span></span>  
   ![graphic9][graphic9]
6. <span data-ttu-id="db77f-138">Przejdź na kartę Konfiguracja:</span><span class="sxs-lookup"><span data-stu-id="db77f-138">Go to the Configure Tab:</span></span>  
   ![graphic10][graphic10]
7. <span data-ttu-id="db77f-140">Na rozwijanej nazwę zasady Znajdź zasady dostępu współdzielonego, używane przez zadania:</span><span class="sxs-lookup"><span data-stu-id="db77f-140">On the Policy Name drop-down, locate the shared access policy used by your job:</span></span>  
   ![graphic11][graphic11]
8. <span data-ttu-id="db77f-142">Między klucz podstawowy i klucz pomocniczy **pobrania nie jest używany przez zadanie**.</span><span class="sxs-lookup"><span data-stu-id="db77f-142">Between the Primary Key and the Secondary Key, **pick the one not used by your job**.</span></span>  
9. <span data-ttu-id="db77f-143">Regenerate trafień:</span><span class="sxs-lookup"><span data-stu-id="db77f-143">Hit regenerate:</span></span>  
   ![graphic12][graphic12]
10. <span data-ttu-id="db77f-145">Skopiuj nowo wygenerowany klucz:</span><span class="sxs-lookup"><span data-stu-id="db77f-145">Copy the newly generated key:</span></span>  
   ![graphic13][graphic13]
11. <span data-ttu-id="db77f-147">Nadal część 2.</span><span class="sxs-lookup"><span data-stu-id="db77f-147">Continue to Part 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="db77f-148">SQL Database</span><span class="sxs-lookup"><span data-stu-id="db77f-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="db77f-149">Uwaga: należy połączyć się z usługą baza danych SQL.</span><span class="sxs-lookup"><span data-stu-id="db77f-149">Note: you will need to connect to the SQL Database Service.</span></span> <span data-ttu-id="db77f-150">Zamierzamy pokazują, jak to zrobić przy użyciu możliwości zarządzania w portalu zarządzania Azure, ale można używać niektórych po stronie klienta narzędzia, takiego jak SQL Server Management Studio również.</span><span class="sxs-lookup"><span data-stu-id="db77f-150">We are going to show how to do this using the management experience on the Azure Management portal but you may choose to use some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="db77f-151">Przejdź do rozszerzenia bazy danych SQL w portalu zarządzania Azure:</span><span class="sxs-lookup"><span data-stu-id="db77f-151">Go to the SQL Databases extension on the Azure Management portal:</span></span>  
   ![graphic14][graphic14]
2. <span data-ttu-id="db77f-153">Zlokalizuj bazę danych SQL używane przez zadania i **kliknij serwer** łącza w tym samym wierszu:</span><span class="sxs-lookup"><span data-stu-id="db77f-153">Locate the SQL Database used by your job and **click on the server** link on the same line:</span></span>  
   <span data-ttu-id="db77f-154">![graphic15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="db77f-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="db77f-155">Kliknij polecenie Zarządzaj:</span><span class="sxs-lookup"><span data-stu-id="db77f-155">Click the Manage command:</span></span>  
   ![graphic16][graphic16]
4. <span data-ttu-id="db77f-157">Typ główny bazy danych:</span><span class="sxs-lookup"><span data-stu-id="db77f-157">Type Database Master:</span></span>  
   ![graphic17][graphic17]
5. <span data-ttu-id="db77f-159">Wpisz nazwę użytkownika, hasło i kliknij przycisk Zaloguj:</span><span class="sxs-lookup"><span data-stu-id="db77f-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![graphic18][graphic18]
6. <span data-ttu-id="db77f-161">Kliknij pozycję Nowa kwerenda:</span><span class="sxs-lookup"><span data-stu-id="db77f-161">Click New Query:</span></span>  
   ![graphic19][graphic19]
7. <span data-ttu-id="db77f-163">Typ w następującym zapytaniu zamianę < login_name > Twoja nazwa użytkownika i zastępowanie <enterStrongPasswordHere> przy użyciu nowego hasła:</span><span class="sxs-lookup"><span data-stu-id="db77f-163">Type in the following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="db77f-164">Kliknij przycisk Uruchom:</span><span class="sxs-lookup"><span data-stu-id="db77f-164">Click Run:</span></span>  
   ![graphic20][graphic20]
9. <span data-ttu-id="db77f-166">Wróć do kroku 2 do tego czasu, kliknij bazy danych:</span><span class="sxs-lookup"><span data-stu-id="db77f-166">Go back to step 2 and this time click the database:</span></span>  
   ![graphic21][graphic21]
10. <span data-ttu-id="db77f-168">Kliknij polecenie Zarządzaj:</span><span class="sxs-lookup"><span data-stu-id="db77f-168">Click the Manage command:</span></span>  
   ![graphic22][graphic22]
11. <span data-ttu-id="db77f-170">Wpisz nazwę użytkownika, hasło i kliknij przycisk logowania:</span><span class="sxs-lookup"><span data-stu-id="db77f-170">type in your User Name, Password, and click Logon:</span></span>  
   ![graphic23][graphic23]
12. <span data-ttu-id="db77f-172">Kliknij pozycję Nowa kwerenda:</span><span class="sxs-lookup"><span data-stu-id="db77f-172">Click New Query:</span></span>  
   ![graphic24][graphic24]
13. <span data-ttu-id="db77f-174">Wpisz poniższe zapytanie zamienianie < nazwa_użytkownika > o nazwie, przez którą ma tę nazwę logowania w kontekście tej bazy danych (taką samą wartość, nadana < login_name >, na przykład można podać) identyfikację i zastępowanie < login_name > Nowa nazwa użytkownika:</span><span class="sxs-lookup"><span data-stu-id="db77f-174">Type in the following query replacing <user_name> with a name by which you want to identify this login in the context of this database (you can provide the same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="db77f-175">Kliknij przycisk Uruchom:</span><span class="sxs-lookup"><span data-stu-id="db77f-175">Click Run:</span></span>  
   ![graphic25][graphic25]
15. <span data-ttu-id="db77f-177">Teraz należy podać nowy użytkownik o tej samej role i uprawnienia miał oryginalny użytkownika.</span><span class="sxs-lookup"><span data-stu-id="db77f-177">You should now provide your new user with the same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="db77f-178">Nadal część 2.</span><span class="sxs-lookup"><span data-stu-id="db77f-178">Continue to Part 2.</span></span>

## <a name="part-2-stopping-the-stream-analytics-job"></a><span data-ttu-id="db77f-179">Część 2: Zatrzymywanie zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="db77f-179">Part 2: Stopping the Stream Analytics Job</span></span>
1. <span data-ttu-id="db77f-180">Przejdź do rozszerzenia usługi Stream Analytics w portalu zarządzania Azure:</span><span class="sxs-lookup"><span data-stu-id="db77f-180">Go to the Stream Analytics extension on the Azure Management portal:</span></span>  
   ![graphic26][graphic26]
2. <span data-ttu-id="db77f-182">Znajdź swoją pracę i przejdź do niej:</span><span class="sxs-lookup"><span data-stu-id="db77f-182">Locate your job and go into it:</span></span>  
   ![graphic27][graphic27]
3. <span data-ttu-id="db77f-184">Przejdź na kartę danych wejściowych lub wyjściowych według tego, czy są obracanie poświadczeń na danych wejściowych lub wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="db77f-184">Go to the Inputs tab or the Outputs tab based on whether you are rotating the credentials on an Input or on an Output.</span></span>  
   ![graphic28][graphic28]
4. <span data-ttu-id="db77f-186">Kliknij polecenie zatrzymania i upewnij się, że zadanie zostało zatrzymane:</span><span class="sxs-lookup"><span data-stu-id="db77f-186">Click the Stop command and confirm the job has stopped:</span></span>  
   <span data-ttu-id="db77f-187">![graphic29][graphic29] Zaczekaj na zatrzymanie zadania.</span><span class="sxs-lookup"><span data-stu-id="db77f-187">![graphic29][graphic29] Wait for the job to stop.</span></span>
5. <span data-ttu-id="db77f-188">Znajdź wejścia/wyjścia, który chcesz obrócić poświadczeń i przejdź do niego:</span><span class="sxs-lookup"><span data-stu-id="db77f-188">Locate the input/output you want to rotate credentials on and go into it:</span></span>  
   ![graphic30][graphic30]
6. <span data-ttu-id="db77f-190">Przejdź do części 3.</span><span class="sxs-lookup"><span data-stu-id="db77f-190">Proceed to Part 3.</span></span>

## <a name="part-3-editing-the-credentials-on-the-stream-analytics-job"></a><span data-ttu-id="db77f-191">Część 3: Edytowanie poświadczeń na zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="db77f-191">Part 3: Editing the credentials on the Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="db77f-192">Magazyn obiektów blob magazynu/tabeli.</span><span class="sxs-lookup"><span data-stu-id="db77f-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="db77f-193">Znajdź pole klucz konta magazynu i wkleić klucz wygenerowanym:</span><span class="sxs-lookup"><span data-stu-id="db77f-193">Find the Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![graphic31][graphic31]
2. <span data-ttu-id="db77f-195">Kliknij polecenie Zapisz i sprawdź, zapisywania zmian:</span><span class="sxs-lookup"><span data-stu-id="db77f-195">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic32][graphic32]
3. <span data-ttu-id="db77f-197">Test połączenia zostaną automatycznie uruchomione po zapisaniu zmian, upewnij się, to znaczy został pomyślnie przekazany.</span><span class="sxs-lookup"><span data-stu-id="db77f-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="db77f-198">Przejdź do części 4.</span><span class="sxs-lookup"><span data-stu-id="db77f-198">Proceed to Part 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="db77f-199">Centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="db77f-199">Event hubs</span></span>
1. <span data-ttu-id="db77f-200">Znajdź pole klucza zasad Centrum zdarzeń i wkleić klucz wygenerowanym:</span><span class="sxs-lookup"><span data-stu-id="db77f-200">Find the Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![graphic33][graphic33]
2. <span data-ttu-id="db77f-202">Kliknij polecenie Zapisz i sprawdź, zapisywania zmian:</span><span class="sxs-lookup"><span data-stu-id="db77f-202">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic34][graphic34]
3. <span data-ttu-id="db77f-204">Test połączenia zostaną automatycznie uruchomione po zapisaniu zmian, upewnij się, że został przekazany pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="db77f-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="db77f-205">Przejdź do części 4.</span><span class="sxs-lookup"><span data-stu-id="db77f-205">Proceed to Part 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="db77f-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="db77f-206">Power BI</span></span>
1. <span data-ttu-id="db77f-207">Kliknij przycisk Odnów autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="db77f-207">Click the Renew authorization:</span></span>  

   ![graphic35][graphic35]
2. <span data-ttu-id="db77f-209">Otrzymasz po potwierdzeniu:</span><span class="sxs-lookup"><span data-stu-id="db77f-209">You will get the following confirmation:</span></span>  

   ![graphic36][graphic36]
3. <span data-ttu-id="db77f-211">Kliknij polecenie Zapisz i sprawdź, zapisywania zmian:</span><span class="sxs-lookup"><span data-stu-id="db77f-211">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic37][graphic37]
4. <span data-ttu-id="db77f-213">Test połączenia zostaną automatycznie uruchomione po zapisaniu zmian, upewnij się, że jej został pomyślnie przekazany.</span><span class="sxs-lookup"><span data-stu-id="db77f-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="db77f-214">Przejdź do części 4.</span><span class="sxs-lookup"><span data-stu-id="db77f-214">Proceed to Part 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="db77f-215">SQL Database</span><span class="sxs-lookup"><span data-stu-id="db77f-215">SQL Database</span></span>
1. <span data-ttu-id="db77f-216">Znajdź pola Nazwa użytkownika i hasło i Wklej nowo utworzonego zestawu poświadczeń do nich:</span><span class="sxs-lookup"><span data-stu-id="db77f-216">Find the User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![graphic38][graphic38]
2. <span data-ttu-id="db77f-218">Kliknij polecenie Zapisz i sprawdź, zapisywania zmian:</span><span class="sxs-lookup"><span data-stu-id="db77f-218">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic39][graphic39]
3. <span data-ttu-id="db77f-220">Test połączenia zostaną automatycznie uruchomione po zapisaniu zmian, upewnij się, że został przekazany pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="db77f-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="db77f-221">Przejdź do części 4.</span><span class="sxs-lookup"><span data-stu-id="db77f-221">Proceed to Part 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="db77f-222">Część 4: Uruchamianie zadania od ostatniego zatrzymania</span><span class="sxs-lookup"><span data-stu-id="db77f-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="db77f-223">Opuścić wejścia/wyjścia:</span><span class="sxs-lookup"><span data-stu-id="db77f-223">Navigate away from the Input/Output:</span></span>  
   ![graphic40][graphic40]
2. <span data-ttu-id="db77f-225">Kliknij polecenie Start:</span><span class="sxs-lookup"><span data-stu-id="db77f-225">Click the Start command:</span></span>  
   ![graphic41][graphic41]
3. <span data-ttu-id="db77f-227">Wybierz czas ostatniego zatrzymania, a następnie kliknij przycisk OK:</span><span class="sxs-lookup"><span data-stu-id="db77f-227">Pick the Last Stopped Time and click OK:</span></span>  
   ![graphic42][graphic42]
4. <span data-ttu-id="db77f-229">Przejdź do części 5.</span><span class="sxs-lookup"><span data-stu-id="db77f-229">Proceed to Part 5.</span></span>  

## <a name="part-5-removing-the-old-set-of-credentials"></a><span data-ttu-id="db77f-230">Część 5: Usuwanie starego zestaw poświadczeń</span><span class="sxs-lookup"><span data-stu-id="db77f-230">Part 5: Removing the old set of credentials</span></span>
<span data-ttu-id="db77f-231">Ta część dotyczy wejścia/wyjścia:</span><span class="sxs-lookup"><span data-stu-id="db77f-231">This part is applicable to the following inputs/outputs:</span></span>

* <span data-ttu-id="db77f-232">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="db77f-232">Blob Storage</span></span>
* <span data-ttu-id="db77f-233">Usługa Event Hubs</span><span class="sxs-lookup"><span data-stu-id="db77f-233">Event Hubs</span></span>
* <span data-ttu-id="db77f-234">SQL Database</span><span class="sxs-lookup"><span data-stu-id="db77f-234">SQL Database</span></span>
* <span data-ttu-id="db77f-235">Table Storage</span><span class="sxs-lookup"><span data-stu-id="db77f-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="db77f-236">Magazyn obiektów blob magazynu/tabeli.</span><span class="sxs-lookup"><span data-stu-id="db77f-236">Blob storage/Table storage</span></span>
<span data-ttu-id="db77f-237">Powtórz część 1 dla klucza dostępu, który był wcześniej używany przez zadanie Aby odnowić teraz nieużywane klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="db77f-237">Repeat Part 1 for the Access Key that was previously used by your job to renew the now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="db77f-238">Centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="db77f-238">Event hubs</span></span>
<span data-ttu-id="db77f-239">Powtórz część 1 dla klucza, który był wcześniej używany przez zadanie Aby odnowić klucz teraz nieużywane.</span><span class="sxs-lookup"><span data-stu-id="db77f-239">Repeat Part 1 for the Key that was previously used by your job to renew the now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="db77f-240">SQL Database</span><span class="sxs-lookup"><span data-stu-id="db77f-240">SQL Database</span></span>
1. <span data-ttu-id="db77f-241">Wróć do okna zapytania z część 1 krok 7 i wpisz następujące zapytanie, zastępując < previous_login_name > Nazwa użytkownika, który był wcześniej używany przez zadania:</span><span class="sxs-lookup"><span data-stu-id="db77f-241">Go back to the query window from Part 1 Step 7 and type in the following query, replacing <previous_login_name> with the User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="db77f-242">Kliknij przycisk Uruchom:</span><span class="sxs-lookup"><span data-stu-id="db77f-242">Click Run:</span></span>  
   ![graphic43][graphic43]  

<span data-ttu-id="db77f-244">Należy pobrać następujące potwierdzenia:</span><span class="sxs-lookup"><span data-stu-id="db77f-244">You should get the following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="db77f-245">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="db77f-245">Get help</span></span>
<span data-ttu-id="db77f-246">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="db77f-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="db77f-247">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="db77f-247">Next steps</span></span>
* [<span data-ttu-id="db77f-248">Wprowadzenie do usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="db77f-248">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="db77f-249">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="db77f-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="db77f-250">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="db77f-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="db77f-251">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="db77f-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="db77f-252">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="db77f-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

