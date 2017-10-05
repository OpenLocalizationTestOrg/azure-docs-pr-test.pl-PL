---
title: "Usługi w chmurze lokalnie w emulatorze obliczeń profilowania | Dokumentacja firmy Microsoft"
services: cloud-services
description: "Zbadaj problemy z wydajnością usług w chmurze przy użyciu profilera Visual Studio"
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
tags: 
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 51c8192d8312dc5cf546b4c357aeecf6f19d56b8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="testing-the-performance-of-a-cloud-service-locally-in-the-azure-compute-emulator-using-the-visual-studio-profiler"></a><span data-ttu-id="b7a8e-103">Testowanie wydajności usługi w chmurze lokalnie w emulatorze obliczeń platformy Azure przy użyciu profilera Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b7a8e-103">Testing the Performance of a Cloud Service Locally in the Azure Compute Emulator Using the Visual Studio Profiler</span></span>
<span data-ttu-id="b7a8e-104">Różnych narzędzi i technik są dostępne do testowania wydajności usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-104">A variety of tools and techniques are available for testing the performance of cloud services.</span></span>
<span data-ttu-id="b7a8e-105">Po opublikowaniu usługi w chmurze na platformie Azure, program Visual Studio zbierania danych profilowania, a następnie analizować lokalnie, zgodnie z opisem w [profilowania aplikacji Azure][1].</span><span class="sxs-lookup"><span data-stu-id="b7a8e-105">When you publish a cloud service to Azure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="b7a8e-106">Umożliwia także diagnostyki do śledzenia różne liczniki wydajności, zgodnie z opisem w [na platformie Azure za pomocą liczników wydajności][2].</span><span class="sxs-lookup"><span data-stu-id="b7a8e-106">You can also use diagnostics to track a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="b7a8e-107">Można także profilu aplikacji lokalnie w emulatorze obliczeń przed jego wdrożeniem w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-107">You might also want to profile your application locally in the compute emulator before deploying it to the cloud.</span></span>

<span data-ttu-id="b7a8e-108">W tym artykule opisano profilowanie metodą próbkowania procesora, które można przeprowadzić lokalnie w emulatorze.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-108">This article covers the CPU Sampling method of profiling, which can be done locally in the emulator.</span></span> <span data-ttu-id="b7a8e-109">Próbkowanie Procesora jest metoda profilowania, która nie jest bardzo niepożądanych.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="b7a8e-110">Interwałem próbkowania wyznaczonych profilera wykonuje migawkę stosu wywołań.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-110">At a designated sampling interval, the profiler takes a snapshot of the call stack.</span></span> <span data-ttu-id="b7a8e-111">Dane są zbierane przez pewien czas i wyświetlane w raporcie.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-111">The data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="b7a8e-112">Ta metoda profilowania zwykle wskazuje, gdzie w praktyce znacznym aplikacji większość pracy Procesora jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-112">This method of profiling tends to indicate where in a computationally intensive application most of the CPU work is being done.</span></span>  <span data-ttu-id="b7a8e-113">Zapewnia możliwość skupić się na "ścieżce aktywnej" gdzie aplikacji jest poświęcany najwięcej czasu.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-113">This gives you the opportunity to focus on the "hot path" where your application is spending the most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="b7a8e-114">1: Konfigurowanie programu Visual Studio do profilowania</span><span class="sxs-lookup"><span data-stu-id="b7a8e-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="b7a8e-115">Najpierw istnieje kilka opcji konfiguracji programu Visual Studio, które mogą być przydatne podczas profilowania.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="b7a8e-116">Aby sensu raportów profilowania, musisz symboli (.pdb, pliki) dla aplikacji i również symboli dla biblioteki systemu.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-116">To make sense of the profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="b7a8e-117">Należy się upewnić, że odwoływania serwerów dostępna symbolu.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-117">You'll want to make sure that you reference the available symbol servers.</span></span> <span data-ttu-id="b7a8e-118">Aby to zrobić, na **narzędzia** menu w programie Visual Studio, wybierz **opcje**, a następnie wybierz **debugowanie**, następnie **symbole**.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-118">To do this, on the **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="b7a8e-119">Upewnij się, że serwerów symboli firmy Microsoft znajduje się w obszarze **symboli (.pdb) lokalizacje**.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="b7a8e-120">Można także odwoływać http://referencesource.microsoft.com/symbols, które mogą mieć dodatkowe symboli plików.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Opcje symbolu][4]

<span data-ttu-id="b7a8e-122">W razie potrzeby można uprościć raportów, które generuje profilera, ustawiając opcję tylko mój kod.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-122">If desired, you can simplify the reports that the profiler generates by setting Just My Code.</span></span> <span data-ttu-id="b7a8e-123">Z tylko mój kod włączone stosy wywołań funkcji są uproszczone, dzięki czemu wywołania całkowicie wewnętrznej biblioteki i .NET Framework są ukryte przed raporty.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal to libraries and the .NET Framework are hidden from the reports.</span></span> <span data-ttu-id="b7a8e-124">Na **narzędzia** menu, wybierz **opcje**.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-124">On the **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="b7a8e-125">Następnie rozwiń węzeł **narzędzi wydajności** węzeł i wybierz polecenie **ogólne**.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-125">Then expand the **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="b7a8e-126">Zaznacz pole wyboru **Włącz opcję tylko mój kod dla raportów profilera**.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-126">Select the checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Tylko mój kod opcje][17]

<span data-ttu-id="b7a8e-128">Instrukcje te mogą posłużyć z istniejącego projektu lub z nowym projektem.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="b7a8e-129">Jeśli tworzysz nowy projekt, aby spróbować techniki opisane poniżej, wybierz C# **usługi w chmurze Azure** projekt i wybierz **roli sieci Web** i **roli procesu roboczego**.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-129">If you create a new project to try the techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Azure ról projektu usługi w chmurze][5]

<span data-ttu-id="b7a8e-131">Na przykład celów, dodać kod do projektu, który zajmuje dużo czasu i przedstawiono niektóre problem z wydajnością oczywiste.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-131">For example purposes, add some code to your project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="b7a8e-132">Na przykład dodaj następujący kod do projektu roli proces roboczy:</span><span class="sxs-lookup"><span data-stu-id="b7a8e-132">For example, add the following code to a worker role project:</span></span>

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

<span data-ttu-id="b7a8e-133">Wywołaj ten kod w metodzie RunAsync w klasie pochodnej RoleEntryPoint roli procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-133">Call this code from the RunAsync method in the worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="b7a8e-134">(Zignorować ostrzeżenie dotyczące metody uruchomiona synchronicznie).</span><span class="sxs-lookup"><span data-stu-id="b7a8e-134">(Ignore the warning about the method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace the following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="b7a8e-135">Tworzenie i uruchamianie usługi w chmurze lokalnie bez debugowania (Ctrl + F5) z konfiguracją rozwiązania ustawioną **wersji**.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-135">Build and run your cloud service locally without debugging (Ctrl+F5), with the solution configuration set to **Release**.</span></span> <span data-ttu-id="b7a8e-136">Dzięki temu, że wszystkie pliki i foldery są tworzone dla aplikacji uruchomionej na komputerze lokalnym i zapewnia, że są uruchomione te emulatory.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-136">This ensures that all files and folders are created for running the application locally, and ensures that all the emulators are started.</span></span> <span data-ttu-id="b7a8e-137">Uruchom interfejs użytkownika emulatora obliczeń z poziomu paska zadań, aby sprawdzić, czy działa swojej roli procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-137">Start the Compute Emulator UI from the taskbar to verify that your worker role is running.</span></span>

## <a name="2-attach-to-a-process"></a><span data-ttu-id="b7a8e-138">2: dołączanie do procesu</span><span class="sxs-lookup"><span data-stu-id="b7a8e-138">2: Attach to a process</span></span>
<span data-ttu-id="b7a8e-139">Profilowanie aplikacji przez uruchomienie go z programu Visual Studio 2010 IDE, a nie musi dołączanie profilera do uruchomionego procesu.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-139">Instead of profiling the application by starting it from the Visual Studio 2010 IDE, you must attach the profiler to a running process.</span></span> 

<span data-ttu-id="b7a8e-140">Aby dołączanie profilera do procesu, na **Analizuj** menu, wybierz **profilera** i **Attach/Detach**.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-140">To attach the profiler to a process, on the **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Dołącz profile — opcja][6]

<span data-ttu-id="b7a8e-142">Dla roli proces roboczy Znajdź proces WaWorkerHost.exe.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-142">For a worker role, find the WaWorkerHost.exe process.</span></span>

![Proces WaWorkerHost][7]

<span data-ttu-id="b7a8e-144">W przypadku folderu projektu na dysku sieciowym, profilera zostanie wyświetlony monit o podanie inną lokalizację, aby zapisać raportów profilowania.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-144">If your project folder is on a network drive, the profiler will ask you to provide another location to save the profiling reports.</span></span>

 <span data-ttu-id="b7a8e-145">Możesz także dołączyć do roli sieci web przez dołączenie do WaIISHost.exe.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-145">You can also attach to a web role by attaching to WaIISHost.exe.</span></span>
<span data-ttu-id="b7a8e-146">Jeśli istnieje wiele procesów roli procesu roboczego w aplikacji, należy użyć processID, aby odróżnić je.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-146">If there are multiple worker role processes in your application, you need to use the processID to distinguish them.</span></span> <span data-ttu-id="b7a8e-147">ProcessID można badać programowo, uzyskując dostęp do obiektu procesu.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-147">You can query the processID programmatically by accessing the Process object.</span></span> <span data-ttu-id="b7a8e-148">Na przykład jeśli dodasz ten kod do metody Run klas pochodnych po RoleEntryPoint w roli można przyjrzeć się zaloguj interfejs użytkownika emulatora obliczeń wiedzieć, jakie procesy, aby nawiązać połączenie.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-148">For example, if you add this code to the Run method of the RoleEntryPoint-derived class in a role, you can look at the log in the Compute Emulator UI to know what process to connect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="b7a8e-149">Aby wyświetlić dziennik, uruchom interfejs użytkownika emulatora obliczeń.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-149">To view the log, start the Compute Emulator UI.</span></span>

![Uruchom Emulator obliczeń interfejsu użytkownika][8]

<span data-ttu-id="b7a8e-151">Otwórz okno konsoli dziennik roli procesu roboczego w interfejs użytkownika emulatora obliczeń, klikając na pasku tytułu okna konsoli.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-151">Open the worker role log console window in the Compute Emulator UI by clicking on the console window's title bar.</span></span> <span data-ttu-id="b7a8e-152">Identyfikator procesu w dzienniku jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-152">You can see the process ID in the log.</span></span>

![Identyfikator procesu widoku][9]

<span data-ttu-id="b7a8e-154">Jedna podłączona, wykonaj kroki w interfejsie użytkownika aplikacji (w razie potrzeby) do odtworzenia tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-154">One you've attached, perform the steps in your application's UI (if needed) to reproduce the scenario.</span></span>

<span data-ttu-id="b7a8e-155">Aby zatrzymać profilowanie, wybrać **Zatrzymaj profilowanie** łącza.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-155">When you want to stop profiling, choose the **Stop Profiling** link.</span></span>

![Zatrzymaj profilowanie opcji][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="b7a8e-157">3: Wyświetl raporty wydajności</span><span class="sxs-lookup"><span data-stu-id="b7a8e-157">3: View performance reports</span></span>
<span data-ttu-id="b7a8e-158">Zostanie wyświetlony raport wydajności aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-158">The performance report for your application is displayed.</span></span>

<span data-ttu-id="b7a8e-159">W tym momencie profilera zatrzymuje wykonywanie, zapisuje dane w pliku Vsp i wyświetla raport zawiera analizę danych.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-159">At this point, the profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Raport programu profilującego][11]

<span data-ttu-id="b7a8e-161">Jeśli widzisz String.wstrcpy w aktywnej ścieżki, kliknij tylko mój kod, aby zmienić widok, aby pokazać tylko kod użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-161">If you see String.wstrcpy in the Hot Path, click on Just My Code to change the view to show user code only.</span></span>  <span data-ttu-id="b7a8e-162">Jeśli widzisz String.concat — spróbuj nacisnąć przycisk Pokaż cały kod.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-162">If you see String.Concat, try pressing the Show All Code button.</span></span>

<span data-ttu-id="b7a8e-163">Powinna zostać wyświetlona ZŁĄCZ.teksty metoda i String.concat — zajmuje dużo czasu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-163">You should see the Concatenate method and String.Concat taking up a large portion of the execution time.</span></span>

![Raport analizy][12]

<span data-ttu-id="b7a8e-165">Jeśli dodano kod łączenia ciągu w tym artykule, w tym powinna zostać wyświetlona ostrzeżenie na liście zadań.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-165">If you added the string concatenation code in this article, you should see a warning in the Task List for this.</span></span> <span data-ttu-id="b7a8e-166">Może również zostać wyświetlony ostrzeżenie, że jest nadmierne ilości pamięci, czyli z powodu liczby ciągów, które są tworzone i usunięty.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-166">You may also see a warning that there is an excessive amount of garbage collection, which is due to the number of strings that are created and disposed.</span></span>

![Ostrzeżenia wydajności][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="b7a8e-168">4: wprowadź zmiany i porównanie wydajności</span><span class="sxs-lookup"><span data-stu-id="b7a8e-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="b7a8e-169">Można także porównać wydajności przed i po zmianie kodu.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-169">You can also compare the performance before and after a code change.</span></span>  <span data-ttu-id="b7a8e-170">Zatrzymaj uruchomionego procesu, a następnie Edytuj kod, aby zastąpić ciąg operacji łączenia z użyciem klasy StringBuilder:</span><span class="sxs-lookup"><span data-stu-id="b7a8e-170">Stop the running process, and edit the code to replace the string concatenation operation with the use of StringBuilder:</span></span>

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

<span data-ttu-id="b7a8e-171">Czy inne uruchomienie wydajności, a następnie porównaj wydajność.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-171">Do another performance run, and then compare the performance.</span></span> <span data-ttu-id="b7a8e-172">W Eksploratorze wydajności, jeśli działa znajdują się w tej samej sesji można po prostu wybraniu obu raportów, otwórz menu skrótów i **raporty porównanie wydajności**.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-172">In the Performance Explorer, if the runs are in the same session, you can just select both reports, open the shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="b7a8e-173">Do porównania z uruchomiony w innej sesji wydajności, należy otworzyć **Analizuj** menu i wybierz polecenie **raporty porównanie wydajności**.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-173">If you want to compare with a run in another performance session, open the **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="b7a8e-174">Określ oba pliki, w wyświetlonym oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-174">Specify both files in the dialog box that appears.</span></span>

![Porównanie opcji raporty wydajności][15]

<span data-ttu-id="b7a8e-176">Raporty zaznacz różnice między dwa przebiegi.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-176">The reports highlight differences between the two runs.</span></span>

![Raport porównawczy][16]

<span data-ttu-id="b7a8e-178">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="b7a8e-178">Congratulations!</span></span> <span data-ttu-id="b7a8e-179">Rozpoczęciu pracy przy użyciu profilera.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-179">You've gotten started with the profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b7a8e-180">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="b7a8e-180">Troubleshooting</span></span>
* <span data-ttu-id="b7a8e-181">Upewnij się, czy profilowania kompilacji wydania i uruchomić bez debugowania.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="b7a8e-182">Jeśli opcja Attach/Detach nie jest włączona w menu profilera, uruchom Kreatora wydajności.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-182">If the Attach/Detach option is not enabled on the Profiler menu, run the Performance Wizard.</span></span>
* <span data-ttu-id="b7a8e-183">Interfejs użytkownika emulatora obliczeń Umożliwia wyświetlenie stanu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-183">Use the Compute Emulator UI to view the status of your application.</span></span> 
* <span data-ttu-id="b7a8e-184">Jeśli masz problemy z uruchamianiem aplikacji w emulatorze lub dołączenie profilera, zamknij emulator obliczeń w dół i uruchom ją ponownie.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-184">If you have problems starting applications in the emulator, or attaching the profiler, shut down the compute emulator and restart it.</span></span> <span data-ttu-id="b7a8e-185">Jeśli to nie rozwiąże problemu, spróbuj wykonać ponowny rozruch.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-185">If that doesn't solve the problem, try rebooting.</span></span> <span data-ttu-id="b7a8e-186">Ten problem może wystąpić, jeśli używasz emulatora obliczeniowe do wstrzymania i usuwanie wdrożeń uruchomionych.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-186">This problem can occur if you use the Compute Emulator to suspend and remove running deployments.</span></span>
* <span data-ttu-id="b7a8e-187">Jeśli używasz dowolnego z profilowania poleceń w wierszu polecenia, szczególnie ustawienia globalne, upewnij się, VSPerfClrEnv /globaloff została wywołana i zamknąć VsPerfMon.exe.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-187">If you have used any of the profiling commands from the command line, especially the global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="b7a8e-188">Jeśli podczas pobierania próbek, zostanie wyświetlony komunikat "PRF0025: żadne dane nie zostały zebrane," Sprawdź, czy dołączyć do procesu ma aktywności Procesora.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-188">If when sampling, you see the message "PRF0025: No data was collected," check that the process you attached to has CPU activity.</span></span> <span data-ttu-id="b7a8e-189">Aplikacje, które są bezczynny obliczeniowy może nie dawać dane z próbkowania.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="b7a8e-190">Istnieje również możliwość, że proces został zakończony zanim wykonano żadnych próbkowania.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-190">It's also possible that the process exited before any sampling was done.</span></span> <span data-ttu-id="b7a8e-191">Sprawdź, czy metoda Run dla roli, do której są profilowania nie kończy.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-191">Check to see that the Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7a8e-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b7a8e-192">Next Steps</span></span>
<span data-ttu-id="b7a8e-193">Instrumentacja Azure pliki binarne w emulatorze nie jest obsługiwany w profilera Visual Studio, ale jeśli chcesz przetestować alokacji pamięci, możesz wybrać tę opcję podczas profilowania.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-193">Instrumenting Azure binaries in the emulator is not supported in the Visual Studio profiler, but if you want to test memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="b7a8e-194">Można również wybrać profilowania współbieżności, który pomaga ustalić, czy wątki są marnować czas rywalizuje blokady lub warstwy profilowanie interakcji, który pomaga wykrywać problemy z wydajnością, gdy interakcji między warstwami aplikacji, większość często między warstwą danych i rolę procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between the data tier and a worker role.</span></span>  <span data-ttu-id="b7a8e-195">Można wyświetlić kwerendy bazy danych, które generuje aplikacji i za pomocą danych profilowania zwiększyć korzystania z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b7a8e-195">You can view the database queries that your app generates and use the profiling data to improve your use of the database.</span></span> <span data-ttu-id="b7a8e-196">Informacji o profilowanie interakcji między warstwami znajduje się w temacie we wpisie blogu [wskazówki: w programie Visual Studio Team System 2010 przy użyciu profilera interakcji warstwy][3].</span><span class="sxs-lookup"><span data-stu-id="b7a8e-196">For information about tier interaction profiling, see the blog post [Walkthrough: Using the Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png
