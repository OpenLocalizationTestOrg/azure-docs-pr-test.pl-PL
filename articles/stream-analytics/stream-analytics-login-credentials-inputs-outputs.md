---
title: "Analiza strumienia: Obracanie poświadczenia logowania dla danych wejściowych i wyjściowych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooupdate hello poświadczeń dla usługi analiza strumienia danych wejściowych i wyjściowych."
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
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="68faa-104">Obróć poświadczenia logowania dla wejścia i wyjścia w zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="68faa-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="68faa-105">Abstrakcyjny</span><span class="sxs-lookup"><span data-stu-id="68faa-105">Abstract</span></span>
<span data-ttu-id="68faa-106">Usługa Azure Stream Analytics obecnie nie zezwala na zastępowanie hello poświadczeń na wejścia/wyjścia zadania hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="68faa-106">Azure Stream Analytics today doesn’t allow replacing hello credentials on an input/output while hello job is running.</span></span>

<span data-ttu-id="68faa-107">Gdy Azure Stream Analytics obsługuje wznawianie zadania z ostatnich danych wyjściowych, możemy tooshare hello całego procesu dla minimalizując hello zwłokę między hello zatrzymywanie i uruchamianie zadania hello i obracanie hello poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="68faa-107">While Azure Stream Analytics does support resuming a job from last output, we wanted tooshare hello entire process for minimizing hello lag between hello stopping and starting of hello job and rotating hello login credentials.</span></span>

## <a name="part-1---prepare-hello-new-set-of-credentials"></a><span data-ttu-id="68faa-108">Część 1 — Przygotowanie hello nowy zestaw poświadczeń:</span><span class="sxs-lookup"><span data-stu-id="68faa-108">Part 1 - Prepare hello new set of credentials:</span></span>
<span data-ttu-id="68faa-109">Ta część jest zastosowanie toohello po wejść/wyjść:</span><span class="sxs-lookup"><span data-stu-id="68faa-109">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="68faa-110">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="68faa-110">Blob Storage</span></span>
* <span data-ttu-id="68faa-111">Usługa Event Hubs</span><span class="sxs-lookup"><span data-stu-id="68faa-111">Event Hubs</span></span>
* <span data-ttu-id="68faa-112">SQL Database</span><span class="sxs-lookup"><span data-stu-id="68faa-112">SQL Database</span></span>
* <span data-ttu-id="68faa-113">Table Storage</span><span class="sxs-lookup"><span data-stu-id="68faa-113">Table Storage</span></span>

<span data-ttu-id="68faa-114">Dla innych wejść/wyjść przejdź do części 2.</span><span class="sxs-lookup"><span data-stu-id="68faa-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="68faa-115">Magazyn obiektów blob magazynu/tabeli.</span><span class="sxs-lookup"><span data-stu-id="68faa-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="68faa-116">Przejdź toohello rozszerzenie magazynu w portalu zarządzania Azure hello:</span><span class="sxs-lookup"><span data-stu-id="68faa-116">Go toohello Storage extention on hello Azure Management portal:</span></span>  
   ![graphic1][graphic1]
2. <span data-ttu-id="68faa-118">Zlokalizuj hello Magazyn używany przez zadanie, a następnie przejdź w niej:</span><span class="sxs-lookup"><span data-stu-id="68faa-118">Locate hello storage used by your job and go into it:</span></span>  
   ![graphic2][graphic2]
3. <span data-ttu-id="68faa-120">Kliknij polecenie Zarządzaj kluczami dostępu hello:</span><span class="sxs-lookup"><span data-stu-id="68faa-120">Click hello Manage Access Keys command:</span></span>  
   ![graphic3][graphic3]
4. <span data-ttu-id="68faa-122">Między hello podstawowy klucz dostępu i hello pomocniczy klucz dostępu **wybierz hello, co nie jest używany przez zadanie**.</span><span class="sxs-lookup"><span data-stu-id="68faa-122">Between hello Primary Access Key and hello Secondary Access Key, **pick hello one not used by your job**.</span></span>
5. <span data-ttu-id="68faa-123">Regenerate trafień:</span><span class="sxs-lookup"><span data-stu-id="68faa-123">Hit regenerate:</span></span>  
   ![graphic4][graphic4]
6. <span data-ttu-id="68faa-125">Skopiuj hello nowo wygenerować klucz:</span><span class="sxs-lookup"><span data-stu-id="68faa-125">Copy hello newly generated key:</span></span>  
   ![graphic5][graphic5]
7. <span data-ttu-id="68faa-127">Nadal tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="68faa-127">Continue tooPart 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="68faa-128">Centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="68faa-128">Event hubs</span></span>
1. <span data-ttu-id="68faa-129">Przejdź toohello rozszerzenia usługi Service Bus w portalu zarządzania Azure hello:</span><span class="sxs-lookup"><span data-stu-id="68faa-129">Go toohello Service Bus extension on hello Azure Management portal:</span></span>  
   ![graphic6][graphic6]
2. <span data-ttu-id="68faa-131">Zlokalizuj hello Namespace magistrali usługi używane przez zadanie, a następnie przejdź w niej:</span><span class="sxs-lookup"><span data-stu-id="68faa-131">Locate hello Service Bus Namespace used by your job and go into it:</span></span>  
   ![graphic7][graphic7]
3. <span data-ttu-id="68faa-133">Jeśli zadanie używa zasady dostępu współużytkowanego na powitania Namespace magistrali usług, przejście toostep 6</span><span class="sxs-lookup"><span data-stu-id="68faa-133">If your job uses a shared access policy on hello Service Bus Namespace, jump toostep 6</span></span>  
4. <span data-ttu-id="68faa-134">Przejdź na kartę usługi Event Hubs toohello:</span><span class="sxs-lookup"><span data-stu-id="68faa-134">Go toohello Event Hubs tab:</span></span>  
   ![graphic8][graphic8]
5. <span data-ttu-id="68faa-136">Zlokalizuj hello używane przez zadanie Centrum zdarzeń i przejdź do niej:</span><span class="sxs-lookup"><span data-stu-id="68faa-136">Locate hello Event Hub used by your job and go into it:</span></span>  
   ![graphic9][graphic9]
6. <span data-ttu-id="68faa-138">Przejdź toohello kartę Konfiguracja:</span><span class="sxs-lookup"><span data-stu-id="68faa-138">Go toohello Configure Tab:</span></span>  
   ![graphic10][graphic10]
7. <span data-ttu-id="68faa-140">Na powitania listy rozwijanej nazwę zasady Znajdź zasad dostępu hello udostępnionych używanych przez zadania:</span><span class="sxs-lookup"><span data-stu-id="68faa-140">On hello Policy Name drop-down, locate hello shared access policy used by your job:</span></span>  
   ![graphic11][graphic11]
8. <span data-ttu-id="68faa-142">Między hello klucz podstawowy i klucz pomocniczy hello **wybierz hello, co nie jest używany przez zadanie**.</span><span class="sxs-lookup"><span data-stu-id="68faa-142">Between hello Primary Key and hello Secondary Key, **pick hello one not used by your job**.</span></span>  
9. <span data-ttu-id="68faa-143">Regenerate trafień:</span><span class="sxs-lookup"><span data-stu-id="68faa-143">Hit regenerate:</span></span>  
   ![graphic12][graphic12]
10. <span data-ttu-id="68faa-145">Skopiuj hello nowo wygenerować klucz:</span><span class="sxs-lookup"><span data-stu-id="68faa-145">Copy hello newly generated key:</span></span>  
   ![graphic13][graphic13]
11. <span data-ttu-id="68faa-147">Nadal tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="68faa-147">Continue tooPart 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="68faa-148">SQL Database</span><span class="sxs-lookup"><span data-stu-id="68faa-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="68faa-149">Uwaga: należy toohello tooconnect usługi baza danych SQL.</span><span class="sxs-lookup"><span data-stu-id="68faa-149">Note: you will need tooconnect toohello SQL Database Service.</span></span> <span data-ttu-id="68faa-150">Za chwilę tooshow jak toodo to przy użyciu hello możliwości zarządzania na hello portalu zarządzania Azure, ale można wybrać toouse niektórych po stronie klienta narzędzia, takiego jak SQL Server Management Studio również.</span><span class="sxs-lookup"><span data-stu-id="68faa-150">We are going tooshow how toodo this using hello management experience on hello Azure Management portal but you may choose toouse some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="68faa-151">Przejdź toohello rozszerzenia bazy danych SQL w portalu zarządzania Azure hello:</span><span class="sxs-lookup"><span data-stu-id="68faa-151">Go toohello SQL Databases extension on hello Azure Management portal:</span></span>  
   ![graphic14][graphic14]
2. <span data-ttu-id="68faa-153">Zlokalizuj hello bazy danych SQL używane przez zadania i **kliknij na powitania serwera** łącze hello sam wiersza:</span><span class="sxs-lookup"><span data-stu-id="68faa-153">Locate hello SQL Database used by your job and **click on hello server** link on hello same line:</span></span>  
   <span data-ttu-id="68faa-154">![graphic15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="68faa-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="68faa-155">Kliknij polecenie Zarządzaj hello:</span><span class="sxs-lookup"><span data-stu-id="68faa-155">Click hello Manage command:</span></span>  
   ![graphic16][graphic16]
4. <span data-ttu-id="68faa-157">Typ główny bazy danych:</span><span class="sxs-lookup"><span data-stu-id="68faa-157">Type Database Master:</span></span>  
   ![graphic17][graphic17]
5. <span data-ttu-id="68faa-159">Wpisz nazwę użytkownika, hasło i kliknij przycisk Zaloguj:</span><span class="sxs-lookup"><span data-stu-id="68faa-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![graphic18][graphic18]
6. <span data-ttu-id="68faa-161">Kliknij pozycję Nowa kwerenda:</span><span class="sxs-lookup"><span data-stu-id="68faa-161">Click New Query:</span></span>  
   ![graphic19][graphic19]
7. <span data-ttu-id="68faa-163">Typ w hello następującego zapytania, zastępując < login_name > z nazwą użytkownika i zastępowanie <enterStrongPasswordHere> przy użyciu nowego hasła:</span><span class="sxs-lookup"><span data-stu-id="68faa-163">Type in hello following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="68faa-164">Kliknij przycisk Uruchom:</span><span class="sxs-lookup"><span data-stu-id="68faa-164">Click Run:</span></span>  
   ![graphic20][graphic20]
9. <span data-ttu-id="68faa-166">Wróć toostep 2 i tym razem kliknij hello bazy danych:</span><span class="sxs-lookup"><span data-stu-id="68faa-166">Go back toostep 2 and this time click hello database:</span></span>  
   ![graphic21][graphic21]
10. <span data-ttu-id="68faa-168">Kliknij polecenie Zarządzaj hello:</span><span class="sxs-lookup"><span data-stu-id="68faa-168">Click hello Manage command:</span></span>  
   ![graphic22][graphic22]
11. <span data-ttu-id="68faa-170">Wpisz nazwę użytkownika, hasło i kliknij przycisk logowania:</span><span class="sxs-lookup"><span data-stu-id="68faa-170">type in your User Name, Password, and click Logon:</span></span>  
   ![graphic23][graphic23]
12. <span data-ttu-id="68faa-172">Kliknij pozycję Nowa kwerenda:</span><span class="sxs-lookup"><span data-stu-id="68faa-172">Click New Query:</span></span>  
   ![graphic24][graphic24]
13. <span data-ttu-id="68faa-174">Wpisz hello następującego zapytania, zastępując < nazwa_użytkownika > o nazwie, przez którą ma tooidentify tej nazwy logowania w kontekście hello tej bazy danych (możesz podać tę samą wartość nadana < login_name >, na przykład Witaj) i zastępowanie < login_name > Nowa nazwa użytkownika:</span><span class="sxs-lookup"><span data-stu-id="68faa-174">Type in hello following query replacing <user_name> with a name by which you want tooidentify this login in hello context of this database (you can provide hello same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="68faa-175">Kliknij przycisk Uruchom:</span><span class="sxs-lookup"><span data-stu-id="68faa-175">Click Run:</span></span>  
   ![graphic25][graphic25]
15. <span data-ttu-id="68faa-177">Teraz należy zapewnić nowego użytkownika z hello tego samego ról oraz uprawnień miał oryginalny użytkownika.</span><span class="sxs-lookup"><span data-stu-id="68faa-177">You should now provide your new user with hello same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="68faa-178">Nadal tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="68faa-178">Continue tooPart 2.</span></span>

## <a name="part-2-stopping-hello-stream-analytics-job"></a><span data-ttu-id="68faa-179">Część 2: Hello zatrzymywania zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="68faa-179">Part 2: Stopping hello Stream Analytics Job</span></span>
1. <span data-ttu-id="68faa-180">Przejdź toohello rozszerzenia usługi Stream Analytics w portalu zarządzania Azure hello:</span><span class="sxs-lookup"><span data-stu-id="68faa-180">Go toohello Stream Analytics extension on hello Azure Management portal:</span></span>  
   ![graphic26][graphic26]
2. <span data-ttu-id="68faa-182">Znajdź swoją pracę i przejdź do niej:</span><span class="sxs-lookup"><span data-stu-id="68faa-182">Locate your job and go into it:</span></span>  
   ![graphic27][graphic27]
3. <span data-ttu-id="68faa-184">Przejdź toohello danych wejściowych karty lub hello wyniki według tego, czy są obracanie hello poświadczeń na danych wejściowych lub wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="68faa-184">Go toohello Inputs tab or hello Outputs tab based on whether you are rotating hello credentials on an Input or on an Output.</span></span>  
   ![graphic28][graphic28]
4. <span data-ttu-id="68faa-186">Kliknij polecenie zatrzymania hello i upewnij się, że zadanie powitania przestał:</span><span class="sxs-lookup"><span data-stu-id="68faa-186">Click hello Stop command and confirm hello job has stopped:</span></span>  
   <span data-ttu-id="68faa-187">![graphic29][graphic29] poczekaj, aż hello toostop zadania.</span><span class="sxs-lookup"><span data-stu-id="68faa-187">![graphic29][graphic29] Wait for hello job toostop.</span></span>
5. <span data-ttu-id="68faa-188">Zlokalizuj hello wejścia/wyjścia ma poświadczenia toorotate na i przejdź do niej:</span><span class="sxs-lookup"><span data-stu-id="68faa-188">Locate hello input/output you want toorotate credentials on and go into it:</span></span>  
   ![graphic30][graphic30]
6. <span data-ttu-id="68faa-190">Kontynuować tooPart 3.</span><span class="sxs-lookup"><span data-stu-id="68faa-190">Proceed tooPart 3.</span></span>

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a><span data-ttu-id="68faa-191">Część 3: Edytowanie hello poświadczeń na powitania zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="68faa-191">Part 3: Editing hello credentials on hello Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="68faa-192">Magazyn obiektów blob magazynu/tabeli.</span><span class="sxs-lookup"><span data-stu-id="68faa-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="68faa-193">Znajdź pole klucz konta magazynu hello i wkleić klucz wygenerowanym:</span><span class="sxs-lookup"><span data-stu-id="68faa-193">Find hello Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![graphic31][graphic31]
2. <span data-ttu-id="68faa-195">Kliknij polecenie Zapisz hello i Potwierdź zapisywania zmian:</span><span class="sxs-lookup"><span data-stu-id="68faa-195">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic32][graphic32]
3. <span data-ttu-id="68faa-197">Test połączenia zostaną automatycznie uruchomione po zapisaniu zmian, upewnij się, to znaczy został pomyślnie przekazany.</span><span class="sxs-lookup"><span data-stu-id="68faa-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="68faa-198">Kontynuować tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="68faa-198">Proceed tooPart 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="68faa-199">Centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="68faa-199">Event hubs</span></span>
1. <span data-ttu-id="68faa-200">Znajdź pole klucza zasad Centrum zdarzeń hello i wkleić klucz wygenerowanym:</span><span class="sxs-lookup"><span data-stu-id="68faa-200">Find hello Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![graphic33][graphic33]
2. <span data-ttu-id="68faa-202">Kliknij polecenie Zapisz hello i Potwierdź zapisywania zmian:</span><span class="sxs-lookup"><span data-stu-id="68faa-202">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic34][graphic34]
3. <span data-ttu-id="68faa-204">Test połączenia zostaną automatycznie uruchomione po zapisaniu zmian, upewnij się, że został przekazany pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="68faa-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="68faa-205">Kontynuować tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="68faa-205">Proceed tooPart 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="68faa-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="68faa-206">Power BI</span></span>
1. <span data-ttu-id="68faa-207">Kliknij hello odnawiania autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="68faa-207">Click hello Renew authorization:</span></span>  

   ![graphic35][graphic35]
2. <span data-ttu-id="68faa-209">Otrzymasz powitania po potwierdzeniu:</span><span class="sxs-lookup"><span data-stu-id="68faa-209">You will get hello following confirmation:</span></span>  

   ![graphic36][graphic36]
3. <span data-ttu-id="68faa-211">Kliknij polecenie Zapisz hello i Potwierdź zapisywania zmian:</span><span class="sxs-lookup"><span data-stu-id="68faa-211">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic37][graphic37]
4. <span data-ttu-id="68faa-213">Test połączenia zostaną automatycznie uruchomione po zapisaniu zmian, upewnij się, że jej został pomyślnie przekazany.</span><span class="sxs-lookup"><span data-stu-id="68faa-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="68faa-214">Kontynuować tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="68faa-214">Proceed tooPart 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="68faa-215">SQL Database</span><span class="sxs-lookup"><span data-stu-id="68faa-215">SQL Database</span></span>
1. <span data-ttu-id="68faa-216">Znajdź hello pola Nazwa użytkownika i hasło i Wklej nowo utworzonego zestawu poświadczeń do nich:</span><span class="sxs-lookup"><span data-stu-id="68faa-216">Find hello User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![graphic38][graphic38]
2. <span data-ttu-id="68faa-218">Kliknij polecenie Zapisz hello i Potwierdź zapisywania zmian:</span><span class="sxs-lookup"><span data-stu-id="68faa-218">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic39][graphic39]
3. <span data-ttu-id="68faa-220">Test połączenia zostaną automatycznie uruchomione po zapisaniu zmian, upewnij się, że został przekazany pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="68faa-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="68faa-221">Kontynuować tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="68faa-221">Proceed tooPart 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="68faa-222">Część 4: Uruchamianie zadania od ostatniego zatrzymania</span><span class="sxs-lookup"><span data-stu-id="68faa-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="68faa-223">Opuścić hello wejścia/wyjścia:</span><span class="sxs-lookup"><span data-stu-id="68faa-223">Navigate away from hello Input/Output:</span></span>  
   ![graphic40][graphic40]
2. <span data-ttu-id="68faa-225">Kliknij polecenie Start hello:</span><span class="sxs-lookup"><span data-stu-id="68faa-225">Click hello Start command:</span></span>  
   ![graphic41][graphic41]
3. <span data-ttu-id="68faa-227">Wybierz hello czas ostatniego zatrzymania, a następnie kliknij przycisk OK:</span><span class="sxs-lookup"><span data-stu-id="68faa-227">Pick hello Last Stopped Time and click OK:</span></span>  
   ![graphic42][graphic42]
4. <span data-ttu-id="68faa-229">Kontynuować tooPart 5.</span><span class="sxs-lookup"><span data-stu-id="68faa-229">Proceed tooPart 5.</span></span>  

## <a name="part-5-removing-hello-old-set-of-credentials"></a><span data-ttu-id="68faa-230">Część 5: Usuwanie hello stary zestaw poświadczeń</span><span class="sxs-lookup"><span data-stu-id="68faa-230">Part 5: Removing hello old set of credentials</span></span>
<span data-ttu-id="68faa-231">Ta część jest zastosowanie toohello po wejść/wyjść:</span><span class="sxs-lookup"><span data-stu-id="68faa-231">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="68faa-232">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="68faa-232">Blob Storage</span></span>
* <span data-ttu-id="68faa-233">Usługa Event Hubs</span><span class="sxs-lookup"><span data-stu-id="68faa-233">Event Hubs</span></span>
* <span data-ttu-id="68faa-234">SQL Database</span><span class="sxs-lookup"><span data-stu-id="68faa-234">SQL Database</span></span>
* <span data-ttu-id="68faa-235">Table Storage</span><span class="sxs-lookup"><span data-stu-id="68faa-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="68faa-236">Magazyn obiektów blob magazynu/tabeli.</span><span class="sxs-lookup"><span data-stu-id="68faa-236">Blob storage/Table storage</span></span>
<span data-ttu-id="68faa-237">Powtórz część 1 dla hello klucz dostępu, który był wcześniej używany przez zadanie toorenew hello teraz nieużywane klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="68faa-237">Repeat Part 1 for hello Access Key that was previously used by your job toorenew hello now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="68faa-238">Centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="68faa-238">Event hubs</span></span>
<span data-ttu-id="68faa-239">Powtórz część 1 dla hello klucz, który był wcześniej używany przez zadanie toorenew hello teraz nieużywane klucza.</span><span class="sxs-lookup"><span data-stu-id="68faa-239">Repeat Part 1 for hello Key that was previously used by your job toorenew hello now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="68faa-240">SQL Database</span><span class="sxs-lookup"><span data-stu-id="68faa-240">SQL Database</span></span>
1. <span data-ttu-id="68faa-241">Przejdź wstecz toohello oknie zapytania z część 1 krok 7 i wpisz hello następującego zapytania, zastępując < previous_login_name > hello nazwę użytkownika, który był wcześniej używany przez zadania:</span><span class="sxs-lookup"><span data-stu-id="68faa-241">Go back toohello query window from Part 1 Step 7 and type in hello following query, replacing <previous_login_name> with hello User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="68faa-242">Kliknij przycisk Uruchom:</span><span class="sxs-lookup"><span data-stu-id="68faa-242">Click Run:</span></span>  
   ![graphic43][graphic43]  

<span data-ttu-id="68faa-244">Należy pobrać powitania po potwierdzeniu:</span><span class="sxs-lookup"><span data-stu-id="68faa-244">You should get hello following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="68faa-245">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="68faa-245">Get help</span></span>
<span data-ttu-id="68faa-246">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="68faa-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="68faa-247">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="68faa-247">Next steps</span></span>
* [<span data-ttu-id="68faa-248">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="68faa-248">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="68faa-249">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="68faa-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="68faa-250">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="68faa-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="68faa-251">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="68faa-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="68faa-252">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="68faa-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

