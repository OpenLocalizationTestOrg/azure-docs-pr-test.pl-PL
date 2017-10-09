---
title: "Chmury usługę lokalnie w hello obliczeniowe emulatora aaaProfiling | Dokumentacja firmy Microsoft"
services: cloud-services
description: "Zbadaj problemy z wydajnością usług w chmurze z hello profilera Visual Studio"
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
ms.openlocfilehash: fc37c85dad4db4cc0310f73afad56fc0fe5f3963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a><span data-ttu-id="49826-103">Testowanie hello wydajność lokalnie usługi chmury w hello hello Azure obliczeniowe z emulatora programu Visual Studio profilera</span><span class="sxs-lookup"><span data-stu-id="49826-103">Testing hello Performance of a Cloud Service Locally in hello Azure Compute Emulator Using hello Visual Studio Profiler</span></span>
<span data-ttu-id="49826-104">Różnych narzędzi i technik są dostępne do testowania wydajności hello usług w chmurze.</span><span class="sxs-lookup"><span data-stu-id="49826-104">A variety of tools and techniques are available for testing hello performance of cloud services.</span></span>
<span data-ttu-id="49826-105">Podczas publikowania tooAzure usługi chmury, program Visual Studio zbierania danych profilowania, a następnie analizować lokalnie, zgodnie z opisem w [profilowania aplikacji Azure][1].</span><span class="sxs-lookup"><span data-stu-id="49826-105">When you publish a cloud service tooAzure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="49826-106">Umożliwia także tootrack diagnostyki liczników różnych wydajności, zgodnie z opisem w [na platformie Azure za pomocą liczników wydajności][2].</span><span class="sxs-lookup"><span data-stu-id="49826-106">You can also use diagnostics tootrack a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="49826-107">Można także tooprofile aplikacji lokalnie w emulatorze obliczeń hello przed jego wdrożeniem toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="49826-107">You might also want tooprofile your application locally in hello compute emulator before deploying it toohello cloud.</span></span>

<span data-ttu-id="49826-108">W tym artykule omówiono hello próbkowania procesora CPU — metoda profilowania, która może odbywać się lokalnie w emulatorze hello.</span><span class="sxs-lookup"><span data-stu-id="49826-108">This article covers hello CPU Sampling method of profiling, which can be done locally in hello emulator.</span></span> <span data-ttu-id="49826-109">Próbkowanie Procesora jest metoda profilowania, która nie jest bardzo niepożądanych.</span><span class="sxs-lookup"><span data-stu-id="49826-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="49826-110">Interwałem próbkowania wyznaczonych profilera hello tworzy migawkę hello stosu wywołań.</span><span class="sxs-lookup"><span data-stu-id="49826-110">At a designated sampling interval, hello profiler takes a snapshot of hello call stack.</span></span> <span data-ttu-id="49826-111">Witaj dane są zbierane przez pewien czas i wyświetlane w raporcie.</span><span class="sxs-lookup"><span data-stu-id="49826-111">hello data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="49826-112">Ta metoda profilowania zwykle tooindicate, gdzie w praktyce znacznym aplikacji większość pracy hello Procesora jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="49826-112">This method of profiling tends tooindicate where in a computationally intensive application most of hello CPU work is being done.</span></span>  <span data-ttu-id="49826-113">Dzięki temu hello toofocus możliwości na powitania "aktywnej ścieżki" gdzie aplikacji jest poświęcany hello większość czasu.</span><span class="sxs-lookup"><span data-stu-id="49826-113">This gives you hello opportunity toofocus on hello "hot path" where your application is spending hello most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="49826-114">1: Konfigurowanie programu Visual Studio do profilowania</span><span class="sxs-lookup"><span data-stu-id="49826-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="49826-115">Najpierw istnieje kilka opcji konfiguracji programu Visual Studio, które mogą być przydatne podczas profilowania.</span><span class="sxs-lookup"><span data-stu-id="49826-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="49826-116">toomake rozumieniu hello raportów dotyczących profilowania, potrzebne będą symboli (.pdb, pliki) dla aplikacji i również symboli dla biblioteki systemu.</span><span class="sxs-lookup"><span data-stu-id="49826-116">toomake sense of hello profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="49826-117">Należy toomake się odwoływać się hello symbol dostępne serwery.</span><span class="sxs-lookup"><span data-stu-id="49826-117">You'll want toomake sure that you reference hello available symbol servers.</span></span> <span data-ttu-id="49826-118">toodo to na powitania **narzędzia** menu w programie Visual Studio, wybierz **opcje**, a następnie wybierz **debugowanie**, następnie **symbole**.</span><span class="sxs-lookup"><span data-stu-id="49826-118">toodo this, on hello **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="49826-119">Upewnij się, że serwerów symboli firmy Microsoft znajduje się w obszarze **symboli (.pdb) lokalizacje**.</span><span class="sxs-lookup"><span data-stu-id="49826-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="49826-120">Można także odwoływać http://referencesource.microsoft.com/symbols, które mogą mieć dodatkowe symboli plików.</span><span class="sxs-lookup"><span data-stu-id="49826-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Opcje symbolu][4]

<span data-ttu-id="49826-122">W razie potrzeby można uprościć hello zgłasza, że profiler hello generuje, ustawiając opcję tylko mój kod.</span><span class="sxs-lookup"><span data-stu-id="49826-122">If desired, you can simplify hello reports that hello profiler generates by setting Just My Code.</span></span> <span data-ttu-id="49826-123">Tylko mój kod włączone stosy wywołań funkcji są uproszczone tak, który odwołuje się całkowicie wewnętrzny toolibraries i hello .NET Framework są ukryte przed hello raportów.</span><span class="sxs-lookup"><span data-stu-id="49826-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal toolibraries and hello .NET Framework are hidden from hello reports.</span></span> <span data-ttu-id="49826-124">Na powitania **narzędzia** menu, wybierz **opcje**.</span><span class="sxs-lookup"><span data-stu-id="49826-124">On hello **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="49826-125">Rozwiń węzeł hello **narzędzi wydajności** węzeł i wybierz polecenie **ogólne**.</span><span class="sxs-lookup"><span data-stu-id="49826-125">Then expand hello **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="49826-126">Zaznacz pole wyboru powitania dla **Włącz opcję tylko mój kod dla raportów profilera**.</span><span class="sxs-lookup"><span data-stu-id="49826-126">Select hello checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Tylko mój kod opcje][17]

<span data-ttu-id="49826-128">Instrukcje te mogą posłużyć z istniejącego projektu lub z nowym projektem.</span><span class="sxs-lookup"><span data-stu-id="49826-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="49826-129">Jeśli tworzysz nowy hello tootry projektu techniki opisane poniżej, wybierz C# **usługi w chmurze Azure** projekt i wybierz **roli sieci Web** i **roli procesu roboczego**.</span><span class="sxs-lookup"><span data-stu-id="49826-129">If you create a new project tootry hello techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Azure ról projektu usługi w chmurze][5]

<span data-ttu-id="49826-131">Na przykład celów, dodać niektóre projektu tooyour kodu, który zajmuje dużo czasu i przedstawiono niektóre problem z wydajnością oczywiste.</span><span class="sxs-lookup"><span data-stu-id="49826-131">For example purposes, add some code tooyour project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="49826-132">Na przykład dodać hello następującego projektu roli proces roboczy tooa kodu:</span><span class="sxs-lookup"><span data-stu-id="49826-132">For example, add hello following code tooa worker role project:</span></span>

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

<span data-ttu-id="49826-133">Wywołać ten kod w metodzie RunAsync w klasie pochodnej RoleEntryPoint roli procesu roboczego hello hello.</span><span class="sxs-lookup"><span data-stu-id="49826-133">Call this code from hello RunAsync method in hello worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="49826-134">(Ignoruj hello ostrzeżenie dotyczące metody hello uruchomiona synchronicznie).</span><span class="sxs-lookup"><span data-stu-id="49826-134">(Ignore hello warning about hello method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="49826-135">Tworzenie i uruchamianie usługi w chmurze lokalnie bez debugowania (Ctrl + F5) z konfiguracją rozwiązania hello ustawić także**wersji**.</span><span class="sxs-lookup"><span data-stu-id="49826-135">Build and run your cloud service locally without debugging (Ctrl+F5), with hello solution configuration set too**Release**.</span></span> <span data-ttu-id="49826-136">Dzięki temu, że wszystkie pliki i foldery są tworzone dla uruchomionej aplikacji hello na komputerze lokalnym i zapewnia uruchomienia wszystkich emulatory hello.</span><span class="sxs-lookup"><span data-stu-id="49826-136">This ensures that all files and folders are created for running hello application locally, and ensures that all hello emulators are started.</span></span> <span data-ttu-id="49826-137">Uruchom hello interfejs użytkownika emulatora obliczeń z tooverify zadań hello, uruchomionym swojej roli procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="49826-137">Start hello Compute Emulator UI from hello taskbar tooverify that your worker role is running.</span></span>

## <a name="2-attach-tooa-process"></a><span data-ttu-id="49826-138">2: dołączanie tooa procesu</span><span class="sxs-lookup"><span data-stu-id="49826-138">2: Attach tooa process</span></span>
<span data-ttu-id="49826-139">Zamiast profilowanie aplikacji hello przez od hello programu Visual Studio 2010 IDE, możesz dołączyć tooa profilera hello uruchomiony proces.</span><span class="sxs-lookup"><span data-stu-id="49826-139">Instead of profiling hello application by starting it from hello Visual Studio 2010 IDE, you must attach hello profiler tooa running process.</span></span> 

<span data-ttu-id="49826-140">tooattach hello tooa procesem profilera, na powitania **Analizuj** menu, wybierz **profilera** i **Attach/Detach**.</span><span class="sxs-lookup"><span data-stu-id="49826-140">tooattach hello profiler tooa process, on hello **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Dołącz profile — opcja][6]

<span data-ttu-id="49826-142">Dla roli proces roboczy odnaleźć hello WaWorkerHost.exe procesu.</span><span class="sxs-lookup"><span data-stu-id="49826-142">For a worker role, find hello WaWorkerHost.exe process.</span></span>

![Proces WaWorkerHost][7]

<span data-ttu-id="49826-144">W przypadku folderu projektu na dysku sieciowym, profilera hello wyświetli monit tooprovide innej lokalizacji toosave hello raporty profilowania.</span><span class="sxs-lookup"><span data-stu-id="49826-144">If your project folder is on a network drive, hello profiler will ask you tooprovide another location toosave hello profiling reports.</span></span>

 <span data-ttu-id="49826-145">Można również dołączyć tooa roli sieci web, dołączając tooWaIISHost.exe.</span><span class="sxs-lookup"><span data-stu-id="49826-145">You can also attach tooa web role by attaching tooWaIISHost.exe.</span></span>
<span data-ttu-id="49826-146">Jeśli istnieje wiele procesów roli procesu roboczego w aplikacji, należy toouse hello processID toodistinguish je.</span><span class="sxs-lookup"><span data-stu-id="49826-146">If there are multiple worker role processes in your application, you need toouse hello processID toodistinguish them.</span></span> <span data-ttu-id="49826-147">Hello processID można badać programowo, uzyskując dostęp do obiektu procesu hello.</span><span class="sxs-lookup"><span data-stu-id="49826-147">You can query hello processID programmatically by accessing hello Process object.</span></span> <span data-ttu-id="49826-148">Na przykład jeśli dodasz to metoda Run toohello kod klas pochodnych RoleEntryPoint hello w roli należy można przeglądać w dzienniku tooknow interfejs użytkownika emulatora obliczeń hello jakie tooconnect procesu do.</span><span class="sxs-lookup"><span data-stu-id="49826-148">For example, if you add this code toohello Run method of hello RoleEntryPoint-derived class in a role, you can look at the log in hello Compute Emulator UI tooknow what process tooconnect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="49826-149">tooview hello dziennika hello start interfejs użytkownika emulatora obliczeń.</span><span class="sxs-lookup"><span data-stu-id="49826-149">tooview hello log, start hello Compute Emulator UI.</span></span>

![Uruchom hello interfejs użytkownika emulatora obliczeń][8]

<span data-ttu-id="49826-151">Otwórz okno konsoli dziennik roli procesu roboczego hello w hello interfejs użytkownika emulatora obliczeń, klikając pasek tytułu okna konsoli hello.</span><span class="sxs-lookup"><span data-stu-id="49826-151">Open hello worker role log console window in hello Compute Emulator UI by clicking on hello console window's title bar.</span></span> <span data-ttu-id="49826-152">Identyfikator procesu hello w dzienniku hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="49826-152">You can see hello process ID in hello log.</span></span>

![Identyfikator procesu widoku][9]

<span data-ttu-id="49826-154">Jedna podłączona, wykonaj kroki hello w scenariuszu hello tooreproduce interfejsu użytkownika (w razie potrzeby) aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49826-154">One you've attached, perform hello steps in your application's UI (if needed) tooreproduce hello scenario.</span></span>

<span data-ttu-id="49826-155">Profilowanie toostop, wybrać hello **Zatrzymaj profilowanie** łącza.</span><span class="sxs-lookup"><span data-stu-id="49826-155">When you want toostop profiling, choose hello **Stop Profiling** link.</span></span>

![Zatrzymaj profilowanie opcji][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="49826-157">3: Wyświetl raporty wydajności</span><span class="sxs-lookup"><span data-stu-id="49826-157">3: View performance reports</span></span>
<span data-ttu-id="49826-158">zostanie wyświetlony raport wydajności Hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49826-158">hello performance report for your application is displayed.</span></span>

<span data-ttu-id="49826-159">W tym momencie profilera hello zatrzymuje wykonywanie, zapisuje dane w pliku Vsp i wyświetla raport zawiera analizę danych.</span><span class="sxs-lookup"><span data-stu-id="49826-159">At this point, hello profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Raport programu profilującego][11]

<span data-ttu-id="49826-161">Jeśli zostanie wyświetlony w hello String.wstrcpy aktywnej ścieżki, kliknij opcję tylko mój kod toochange hello wyświetlić tooshow tylko kod użytkownika.</span><span class="sxs-lookup"><span data-stu-id="49826-161">If you see String.wstrcpy in hello Hot Path, click on Just My Code toochange hello view tooshow user code only.</span></span>  <span data-ttu-id="49826-162">Jeśli widzisz String.concat — spróbuj nacisnąć przycisk Pokaż cały kod hello.</span><span class="sxs-lookup"><span data-stu-id="49826-162">If you see String.Concat, try pressing hello Show All Code button.</span></span>

<span data-ttu-id="49826-163">Metoda ZŁĄCZ.teksty hello i zajmuje dużo czasu wykonywania hello String.concat — powinien być widoczny.</span><span class="sxs-lookup"><span data-stu-id="49826-163">You should see hello Concatenate method and String.Concat taking up a large portion of hello execution time.</span></span>

![Raport analizy][12]

<span data-ttu-id="49826-165">Jeśli dodano kod łączenia ciąg hello w tym artykule, w tym powinna zostać wyświetlona ostrzeżenie w hello listy zadań.</span><span class="sxs-lookup"><span data-stu-id="49826-165">If you added hello string concatenation code in this article, you should see a warning in hello Task List for this.</span></span> <span data-ttu-id="49826-166">Może również zostać wyświetlony ostrzeżenie, że jest nadmierne ilości pamięci jest powodu toohello liczba ciągów, które są tworzone i usunięty.</span><span class="sxs-lookup"><span data-stu-id="49826-166">You may also see a warning that there is an excessive amount of garbage collection, which is due toohello number of strings that are created and disposed.</span></span>

![Ostrzeżenia wydajności][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="49826-168">4: wprowadź zmiany i porównanie wydajności</span><span class="sxs-lookup"><span data-stu-id="49826-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="49826-169">Porównanie wydajności hello przed i po zmianie kodu.</span><span class="sxs-lookup"><span data-stu-id="49826-169">You can also compare hello performance before and after a code change.</span></span>  <span data-ttu-id="49826-170">Zatrzymaj hello uruchomienie procesu, a następnie edytuj hello kodu tooreplace hello łączenia operacja ciągów z użyciem hello elementu StringBuilder:</span><span class="sxs-lookup"><span data-stu-id="49826-170">Stop hello running process, and edit hello code tooreplace hello string concatenation operation with hello use of StringBuilder:</span></span>

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

<span data-ttu-id="49826-171">Czy inne uruchomienie wydajności, a następnie porównaj hello wydajności.</span><span class="sxs-lookup"><span data-stu-id="49826-171">Do another performance run, and then compare hello performance.</span></span> <span data-ttu-id="49826-172">W hello Eksplorator wydajności, jeśli hello uruchamia znajdują się w hello tej samej sesji, po prostu wybierz obu raportów, otwórz menu skrótów hello i wybierz polecenie **raporty porównanie wydajności**.</span><span class="sxs-lookup"><span data-stu-id="49826-172">In hello Performance Explorer, if hello runs are in hello same session, you can just select both reports, open hello shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="49826-173">Toocompare z uruchomiony w innej sesji wydajności, należy otworzyć hello **Analizuj** menu i wybierz polecenie **raporty porównanie wydajności**.</span><span class="sxs-lookup"><span data-stu-id="49826-173">If you want toocompare with a run in another performance session, open hello **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="49826-174">Określ oba pliki, pojawi się okno dialogowe hello.</span><span class="sxs-lookup"><span data-stu-id="49826-174">Specify both files in hello dialog box that appears.</span></span>

![Porównanie opcji raporty wydajności][15]

<span data-ttu-id="49826-176">Raporty Hello zaznacz różnice między hello dwa przebiegi.</span><span class="sxs-lookup"><span data-stu-id="49826-176">hello reports highlight differences between hello two runs.</span></span>

![Raport porównawczy][16]

<span data-ttu-id="49826-178">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="49826-178">Congratulations!</span></span> <span data-ttu-id="49826-179">Rozpoczęciu pracy z hello profilera.</span><span class="sxs-lookup"><span data-stu-id="49826-179">You've gotten started with hello profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="49826-180">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="49826-180">Troubleshooting</span></span>
* <span data-ttu-id="49826-181">Upewnij się, czy profilowania kompilacji wydania i uruchomić bez debugowania.</span><span class="sxs-lookup"><span data-stu-id="49826-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="49826-182">Jeśli nie włączono hello Attach/Detach opcji menu profilera hello, uruchom hello Kreator wydajności.</span><span class="sxs-lookup"><span data-stu-id="49826-182">If hello Attach/Detach option is not enabled on hello Profiler menu, run hello Performance Wizard.</span></span>
* <span data-ttu-id="49826-183">Użyj hello interfejs użytkownika emulatora obliczeń tooview hello stanu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49826-183">Use hello Compute Emulator UI tooview hello status of your application.</span></span> 
* <span data-ttu-id="49826-184">Jeśli masz problemy z uruchamianiem aplikacji w emulatorze hello lub dołączanie hello profilera, zamknij emulator obliczeń hello i uruchom go ponownie.</span><span class="sxs-lookup"><span data-stu-id="49826-184">If you have problems starting applications in hello emulator, or attaching hello profiler, shut down hello compute emulator and restart it.</span></span> <span data-ttu-id="49826-185">Jeśli to nie rozwiąże problemu hello, spróbuj wykonać ponowny rozruch.</span><span class="sxs-lookup"><span data-stu-id="49826-185">If that doesn't solve hello problem, try rebooting.</span></span> <span data-ttu-id="49826-186">Ten problem może wystąpić, jeśli używasz hello obliczeniowe emulatora toosuspend i Usuń uruchomionych wdrożeniach.</span><span class="sxs-lookup"><span data-stu-id="49826-186">This problem can occur if you use hello Compute Emulator toosuspend and remove running deployments.</span></span>
* <span data-ttu-id="49826-187">Jeśli używasz dowolnej hello profilowania poleceń w wierszu polecenia szczególnie hello ustawienia globalne, upewnij się, że VSPerfClrEnv /globaloff została wywołana i zamknąć VsPerfMon.exe.</span><span class="sxs-lookup"><span data-stu-id="49826-187">If you have used any of hello profiling commands from the command line, especially hello global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="49826-188">Jeśli podczas pobierania próbek, zobacz wiadomości powitania "PRF0025: żadne dane nie zostały zebrane," Sprawdź, czy hello proces dołączony działania toohas procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="49826-188">If when sampling, you see hello message "PRF0025: No data was collected," check that hello process you attached toohas CPU activity.</span></span> <span data-ttu-id="49826-189">Aplikacje, które są bezczynny obliczeniowy może nie dawać dane z próbkowania.</span><span class="sxs-lookup"><span data-stu-id="49826-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="49826-190">Istnieje również możliwość, że hello proces został zakończony zanim wykonano żadnych próbkowania.</span><span class="sxs-lookup"><span data-stu-id="49826-190">It's also possible that hello process exited before any sampling was done.</span></span> <span data-ttu-id="49826-191">Sprawdź toosee, która metoda Run powitania dla roli, do której są profilowania nie kończy.</span><span class="sxs-lookup"><span data-stu-id="49826-191">Check toosee that hello Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49826-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="49826-192">Next Steps</span></span>
<span data-ttu-id="49826-193">Instrumentacja Azure pliki binarne w emulatorze hello nie jest obsługiwany w hello profilera Visual Studio, ale jeśli chcesz tootest alokacji pamięci, można wybrać opcję podczas profilowania.</span><span class="sxs-lookup"><span data-stu-id="49826-193">Instrumenting Azure binaries in hello emulator is not supported in hello Visual Studio profiler, but if you want tootest memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="49826-194">Można również wybrać profilowania współbieżności, który pomaga ustalić, czy wątki są marnować czas rywalizuje blokady lub warstwy profilowanie interakcji, który pomaga wykrywać problemy z wydajnością, gdy interakcji między warstwami aplikacji, większość często między hello warstwy danych i rolę procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="49826-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between hello data tier and a worker role.</span></span>  <span data-ttu-id="49826-195">Można wyświetlić hello kwerendy bazy danych, które generuje aplikacji i używać hello profilowania korzystania z bazy danych hello tooimprove danych.</span><span class="sxs-lookup"><span data-stu-id="49826-195">You can view hello database queries that your app generates and use hello profiling data tooimprove your use of hello database.</span></span> <span data-ttu-id="49826-196">Informacje profilowanie interakcji między warstwami, zobacz hello blogu [wskazówki: przy użyciu hello warstwy profilera interakcji w programie Visual Studio Team System 2010][3].</span><span class="sxs-lookup"><span data-stu-id="49826-196">For information about tier interaction profiling, see hello blog post [Walkthrough: Using hello Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

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
