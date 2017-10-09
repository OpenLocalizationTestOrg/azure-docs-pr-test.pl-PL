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
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a>Testowanie hello wydajność lokalnie usługi chmury w hello hello Azure obliczeniowe z emulatora programu Visual Studio profilera
Różnych narzędzi i technik są dostępne do testowania wydajności hello usług w chmurze.
Podczas publikowania tooAzure usługi chmury, program Visual Studio zbierania danych profilowania, a następnie analizować lokalnie, zgodnie z opisem w [profilowania aplikacji Azure][1].
Umożliwia także tootrack diagnostyki liczników różnych wydajności, zgodnie z opisem w [na platformie Azure za pomocą liczników wydajności][2].
Można także tooprofile aplikacji lokalnie w emulatorze obliczeń hello przed jego wdrożeniem toohello chmury.

W tym artykule omówiono hello próbkowania procesora CPU — metoda profilowania, która może odbywać się lokalnie w emulatorze hello. Próbkowanie Procesora jest metoda profilowania, która nie jest bardzo niepożądanych. Interwałem próbkowania wyznaczonych profilera hello tworzy migawkę hello stosu wywołań. Witaj dane są zbierane przez pewien czas i wyświetlane w raporcie. Ta metoda profilowania zwykle tooindicate, gdzie w praktyce znacznym aplikacji większość pracy hello Procesora jest wykonywana.  Dzięki temu hello toofocus możliwości na powitania "aktywnej ścieżki" gdzie aplikacji jest poświęcany hello większość czasu.

## <a name="1-configure-visual-studio-for-profiling"></a>1: Konfigurowanie programu Visual Studio do profilowania
Najpierw istnieje kilka opcji konfiguracji programu Visual Studio, które mogą być przydatne podczas profilowania. toomake rozumieniu hello raportów dotyczących profilowania, potrzebne będą symboli (.pdb, pliki) dla aplikacji i również symboli dla biblioteki systemu. Należy toomake się odwoływać się hello symbol dostępne serwery. toodo to na powitania **narzędzia** menu w programie Visual Studio, wybierz **opcje**, a następnie wybierz **debugowanie**, następnie **symbole**. Upewnij się, że serwerów symboli firmy Microsoft znajduje się w obszarze **symboli (.pdb) lokalizacje**.  Można także odwoływać http://referencesource.microsoft.com/symbols, które mogą mieć dodatkowe symboli plików.

![Opcje symbolu][4]

W razie potrzeby można uprościć hello zgłasza, że profiler hello generuje, ustawiając opcję tylko mój kod. Tylko mój kod włączone stosy wywołań funkcji są uproszczone tak, który odwołuje się całkowicie wewnętrzny toolibraries i hello .NET Framework są ukryte przed hello raportów. Na powitania **narzędzia** menu, wybierz **opcje**. Rozwiń węzeł hello **narzędzi wydajności** węzeł i wybierz polecenie **ogólne**. Zaznacz pole wyboru powitania dla **Włącz opcję tylko mój kod dla raportów profilera**.

![Tylko mój kod opcje][17]

Instrukcje te mogą posłużyć z istniejącego projektu lub z nowym projektem.  Jeśli tworzysz nowy hello tootry projektu techniki opisane poniżej, wybierz C# **usługi w chmurze Azure** projekt i wybierz **roli sieci Web** i **roli procesu roboczego**.

![Azure ról projektu usługi w chmurze][5]

Na przykład celów, dodać niektóre projektu tooyour kodu, który zajmuje dużo czasu i przedstawiono niektóre problem z wydajnością oczywiste. Na przykład dodać hello następującego projektu roli proces roboczy tooa kodu:

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

Wywołać ten kod w metodzie RunAsync w klasie pochodnej RoleEntryPoint roli procesu roboczego hello hello. (Ignoruj hello ostrzeżenie dotyczące metody hello uruchomiona synchronicznie).

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

Tworzenie i uruchamianie usługi w chmurze lokalnie bez debugowania (Ctrl + F5) z konfiguracją rozwiązania hello ustawić także**wersji**. Dzięki temu, że wszystkie pliki i foldery są tworzone dla uruchomionej aplikacji hello na komputerze lokalnym i zapewnia uruchomienia wszystkich emulatory hello. Uruchom hello interfejs użytkownika emulatora obliczeń z tooverify zadań hello, uruchomionym swojej roli procesu roboczego.

## <a name="2-attach-tooa-process"></a>2: dołączanie tooa procesu
Zamiast profilowanie aplikacji hello przez od hello programu Visual Studio 2010 IDE, możesz dołączyć tooa profilera hello uruchomiony proces. 

tooattach hello tooa procesem profilera, na powitania **Analizuj** menu, wybierz **profilera** i **Attach/Detach**.

![Dołącz profile — opcja][6]

Dla roli proces roboczy odnaleźć hello WaWorkerHost.exe procesu.

![Proces WaWorkerHost][7]

W przypadku folderu projektu na dysku sieciowym, profilera hello wyświetli monit tooprovide innej lokalizacji toosave hello raporty profilowania.

 Można również dołączyć tooa roli sieci web, dołączając tooWaIISHost.exe.
Jeśli istnieje wiele procesów roli procesu roboczego w aplikacji, należy toouse hello processID toodistinguish je. Hello processID można badać programowo, uzyskując dostęp do obiektu procesu hello. Na przykład jeśli dodasz to metoda Run toohello kod klas pochodnych RoleEntryPoint hello w roli należy można przeglądać w dzienniku tooknow interfejs użytkownika emulatora obliczeń hello jakie tooconnect procesu do.

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

tooview hello dziennika hello start interfejs użytkownika emulatora obliczeń.

![Uruchom hello interfejs użytkownika emulatora obliczeń][8]

Otwórz okno konsoli dziennik roli procesu roboczego hello w hello interfejs użytkownika emulatora obliczeń, klikając pasek tytułu okna konsoli hello. Identyfikator procesu hello w dzienniku hello jest widoczny.

![Identyfikator procesu widoku][9]

Jedna podłączona, wykonaj kroki hello w scenariuszu hello tooreproduce interfejsu użytkownika (w razie potrzeby) aplikacji.

Profilowanie toostop, wybrać hello **Zatrzymaj profilowanie** łącza.

![Zatrzymaj profilowanie opcji][10]

## <a name="3-view-performance-reports"></a>3: Wyświetl raporty wydajności
zostanie wyświetlony raport wydajności Hello aplikacji.

W tym momencie profilera hello zatrzymuje wykonywanie, zapisuje dane w pliku Vsp i wyświetla raport zawiera analizę danych.

![Raport programu profilującego][11]

Jeśli zostanie wyświetlony w hello String.wstrcpy aktywnej ścieżki, kliknij opcję tylko mój kod toochange hello wyświetlić tooshow tylko kod użytkownika.  Jeśli widzisz String.concat — spróbuj nacisnąć przycisk Pokaż cały kod hello.

Metoda ZŁĄCZ.teksty hello i zajmuje dużo czasu wykonywania hello String.concat — powinien być widoczny.

![Raport analizy][12]

Jeśli dodano kod łączenia ciąg hello w tym artykule, w tym powinna zostać wyświetlona ostrzeżenie w hello listy zadań. Może również zostać wyświetlony ostrzeżenie, że jest nadmierne ilości pamięci jest powodu toohello liczba ciągów, które są tworzone i usunięty.

![Ostrzeżenia wydajności][14]

## <a name="4-make-changes-and-compare-performance"></a>4: wprowadź zmiany i porównanie wydajności
Porównanie wydajności hello przed i po zmianie kodu.  Zatrzymaj hello uruchomienie procesu, a następnie edytuj hello kodu tooreplace hello łączenia operacja ciągów z użyciem hello elementu StringBuilder:

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

Czy inne uruchomienie wydajności, a następnie porównaj hello wydajności. W hello Eksplorator wydajności, jeśli hello uruchamia znajdują się w hello tej samej sesji, po prostu wybierz obu raportów, otwórz menu skrótów hello i wybierz polecenie **raporty porównanie wydajności**. Toocompare z uruchomiony w innej sesji wydajności, należy otworzyć hello **Analizuj** menu i wybierz polecenie **raporty porównanie wydajności**. Określ oba pliki, pojawi się okno dialogowe hello.

![Porównanie opcji raporty wydajności][15]

Raporty Hello zaznacz różnice między hello dwa przebiegi.

![Raport porównawczy][16]

Gratulacje! Rozpoczęciu pracy z hello profilera.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
* Upewnij się, czy profilowania kompilacji wydania i uruchomić bez debugowania.
* Jeśli nie włączono hello Attach/Detach opcji menu profilera hello, uruchom hello Kreator wydajności.
* Użyj hello interfejs użytkownika emulatora obliczeń tooview hello stanu aplikacji. 
* Jeśli masz problemy z uruchamianiem aplikacji w emulatorze hello lub dołączanie hello profilera, zamknij emulator obliczeń hello i uruchom go ponownie. Jeśli to nie rozwiąże problemu hello, spróbuj wykonać ponowny rozruch. Ten problem może wystąpić, jeśli używasz hello obliczeniowe emulatora toosuspend i Usuń uruchomionych wdrożeniach.
* Jeśli używasz dowolnej hello profilowania poleceń w wierszu polecenia szczególnie hello ustawienia globalne, upewnij się, że VSPerfClrEnv /globaloff została wywołana i zamknąć VsPerfMon.exe.
* Jeśli podczas pobierania próbek, zobacz wiadomości powitania "PRF0025: żadne dane nie zostały zebrane," Sprawdź, czy hello proces dołączony działania toohas procesora CPU. Aplikacje, które są bezczynny obliczeniowy może nie dawać dane z próbkowania.  Istnieje również możliwość, że hello proces został zakończony zanim wykonano żadnych próbkowania. Sprawdź toosee, która metoda Run powitania dla roli, do której są profilowania nie kończy.

## <a name="next-steps"></a>Następne kroki
Instrumentacja Azure pliki binarne w emulatorze hello nie jest obsługiwany w hello profilera Visual Studio, ale jeśli chcesz tootest alokacji pamięci, można wybrać opcję podczas profilowania. Można również wybrać profilowania współbieżności, który pomaga ustalić, czy wątki są marnować czas rywalizuje blokady lub warstwy profilowanie interakcji, który pomaga wykrywać problemy z wydajnością, gdy interakcji między warstwami aplikacji, większość często między hello warstwy danych i rolę procesu roboczego.  Można wyświetlić hello kwerendy bazy danych, które generuje aplikacji i używać hello profilowania korzystania z bazy danych hello tooimprove danych. Informacje profilowanie interakcji między warstwami, zobacz hello blogu [wskazówki: przy użyciu hello warstwy profilera interakcji w programie Visual Studio Team System 2010][3].

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
