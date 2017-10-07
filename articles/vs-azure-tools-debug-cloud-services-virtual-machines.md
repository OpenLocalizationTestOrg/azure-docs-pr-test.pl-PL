---
title: "aaaDebugging platformy Azure w chmurze, usługi lub maszyny wirtualnej w programie Visual Studio | Dokumentacja firmy Microsoft"
description: "Debugowanie usługi w chmurze lub maszyny wirtualnej w programie Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 945e06e0-2100-41af-b218-72347367ddab
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 32a326430021ba2ea9317a6a71fa005d4b87c273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-an-azure-cloud-service-or-virtual-machine-in-visual-studio"></a>Debugowanie usługi w chmurze Azure lub maszyny wirtualnej w programie Visual Studio
Visual Studio zapewnia różne opcje do debugowania usług w chmurze Azure i maszyn wirtualnych.

## <a name="debug-your-cloud-service-on-your-local-computer"></a>Usługi w chmurze na komputerze lokalnym debugowania
Można zapisać czas i pieniądze za pomocą toodebug emulatora obliczeń platformy Azure hello usługi w chmurze na komputerze lokalnym. Przez lokalnie debugowania usługi przed wdrożeniem, można zwiększyć niezawodność i wydajność bez płatności dla czasu obliczeniowego. Jednak niektóre mogą wystąpić błędy tylko po uruchomieniu usługi w chmurze na platformie Azure samej siebie. Te błędy można debugować po włączeniu zdalnego debugowania podczas publikowania usługi, a następnie dołącz wystąpienia roli tooa debugera hello.

Hello emulator symuluje hello rozwiązań usługi obliczenia Azure usługi i jest uruchamiany w środowisku lokalnym, aby umożliwić testowanie i debugowanie usługi w chmurze, przed przystąpieniem do wdrażania. uchwyty emulatora Hello hello cyklem życia wystąpienia roli i udostępnia toosimulated zasoby, takie jak magazyn lokalny. Podczas debugowania i uruchamiania usługi z programu Visual Studio emulatora hello jest automatycznie uruchamiana jako aplikacja w tle, a następnie wdraża z emulatorem toohello usługi. Używając tooview emulatora hello usługi po uruchomieniu w środowisku lokalnym hello. Można uruchomić pełną wersję hello lub hello ekspresowej wersji emulatora hello. (Począwszy od wersji 2.3 Azure hello ekspresowej wersji emulatora hello jest domyślne hello). Zobacz [tooRun przy użyciu emulatora Express i debugowania lokalnie usługi chmury](https://msdn.microsoft.com/library/dn339018.aspx).

### <a name="toodebug-your-cloud-service-on-your-local-computer"></a>toodebug chmury usługi na komputerze lokalnym
1. Na pasku menu hello, wybierz **debugowania**, **Rozpocznij debugowanie** toorun Twojego projektu usługi w chmurze Azure. Alternatywnie naciśnij klawisz F5. Pojawi się wiadomość hello obliczeniowe emulatora jest uruchomione. Po uruchomieniu emulatora hello ikony paska zadań hello potwierdza go.

    ![Emulator usługi Azure w hello na pasku zadań](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC783828.png)
2. Wyświetlanie interfejsu użytkownika powitania dla emulatora obliczeń hello przez otwarcie menu skrótów hello hello Azure ikonę w obszarze powiadomień hello, a następnie wybierz **Pokaż interfejs użytkownika emulatora obliczeń**.

    Witaj w lewym okienku programu hello interfejsu użytkownika pokazuje hello usług, które są obecnie wdrożona toohello emulatora i hello roli wystąpienia obliczeniowe uruchomione każdej usługi. W okienku po prawej stronie powitania można hello usługi lub role toodisplay cykl życia, rejestrowania i informacji diagnostycznych. Umieszczenie hello fokusu w górny margines hello dołączone okna, rozszerza toofill powitania po prawej.
3. Krok przy użyciu aplikacji hello, wybierając polecenia na powitania **debugowania** menu i ustawianie punktów przerwania w kodzie. Podczas wykonywania kroków przy użyciu aplikacji hello w debugerze hello okienka hello są aktualizowane przy użyciu bieżącego stanu aplikacji hello hello. Po zatrzymaniu debugowania, wdrażania aplikacji hello jest usuwana. Jeśli aplikacja zawiera rolę sieci web i ustawiono przeglądarki sieci web hello toostart właściwości hello uruchomienia akcji, Visual Studio uruchamia aplikację sieci web w przeglądarce hello. Jeśli zmienisz hello liczbę wystąpień roli w konfiguracji usługi hello, musisz zatrzymać usługi w chmurze i ponownie uruchom debugowanie, dzięki czemu można debugować tych nowych wystąpień roli hello.

    **Uwaga:** gdy przestanie działać lub debugowanie usługi hello emulatora obliczeń lokalnych i emulatora magazynu nie są zatrzymane. Należy zatrzymać ich jawnie z hello obszaru powiadomień.

## <a name="debug-a-cloud-service-in-azure"></a>Usługi w chmurze na platformie Azure debugowania
toodebug usługi w chmurze z komputera zdalnego, należy włączyć te funkcje jawnie podczas wdrażania usługi w chmurze tak, że wymagane usługi (na przykład msvsmon.exe) są zainstalowane na maszynach wirtualnych hello systemem wystąpienia roli. Jeśli nie zostanie włączone, zdalne debugowanie po opublikowaniu usługi hello, masz toorepublish hello usługi z włączonym debugowaniem zdalnym.

Włączenie debugowania zdalnego dla usługi w chmurze, on nie działać z mniejszą wydajnością lub spowodować naliczenie dodatkowych opłat. Nie można używać zdalnego debugowania na usługi produkcji, ponieważ klienci używający usługi hello może mieć niekorzystny wpływ na.

> [!NOTE]
> Po opublikowaniu usługi w chmurze w programie Visual Studio, aby umożliwić **IntelliTrace** dla wszystkich ról, że usługa tego hello docelowej platformy .NET Framework 4 lub hello .NET Framework 4.5. Za pomocą **IntelliTrace**, można zbadać zdarzenia, które wystąpiły w wystąpieniu roli w przeszłości hello i Odtwórz kontekstu powitania od tego momentu. Zobacz [debugowania usługi opublikowana chmura za pomocą funkcji IntelliTrace i Visual Studio](http://go.microsoft.com/fwlink/?LinkID=623016) i [przy użyciu funkcji IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx).
>
>

### <a name="tooenable-remote-debugging-for-a-cloud-service"></a>tooenable zdalnego debugowania dla usługi w chmurze
1. Otwórz menu skrótów hello hello Azure projektu, a następnie wybierz **publikowania**.
2. Wybierz hello **przemieszczania** środowiska i hello **debugowania** konfiguracji.

    Jest to tylko wytyczne. Aby zrezygnować toorun środowiska testowego w środowisku produkcyjnym. Jednak użytkownik może niekorzystnie wpłynąć na użytkowników po włączeniu zdalnego debugowania na powitania środowiska produkcyjnego. Można wybrać hello wersji konfiguracji, ale konfiguracja debugowania hello sprawia, że ułatwia debugowanie.

    ![Wybierz konfigurację debugowania hello](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746717.gif)
3. Wykonaj kroki zwykle hello, ale wybierz hello **Włącz zdalny debuger dla wszystkich ról** pole wyboru na powitania **Zaawansowane ustawienia** kartę.

    ![Konfiguracja debugowania](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746718.gif)

### <a name="tooattach-hello-debugger-tooa-cloud-service-in-azure"></a>tooattach hello debugera tooa usługi w chmurze na platformie Azure
1. W Eksploratorze serwera rozwiń węzeł powitania dla usługi w chmurze.
2. Menu skrótów Otwórz hello roli hello lub toowhich wystąpienia roli tooattach, a następnie wybrać **dołączyć debuger**.

    Jeśli debugowania roli debuger programu Visual Studio hello dołącza tooeach wystąpienie tej roli. Debuger Hello przerwie na punkt przerwania dla hello pierwszego wystąpienia roli uruchamia wiersza kodu, który spełnia wszystkie warunki tego punktu przerwania. Jeśli debugowania wystąpienie debugera hello dołącza tooonly, że wystąpienie i podziału na punkt przerwania tylko wtedy, gdy to wystąpienie określonego wiersza kodu spełnia hello warunków punktu przerwania.

    ![Dołączanie debugera](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746719.gif)
3. Po debugera hello dołącza wystąpienia tooan, debugowania w zwykły sposób. Debuger Hello dołącza automatycznie toohello procesu odpowiedniego hosta dla roli użytkownika. W zależności od tego, jakie hello jest rola toow3wp.exe dołącza debuger hello, WaWorkerHost.exe albo WaIISHost.exe. tooverify hello procesu toowhich hello debuger jest dołączony, rozwiń węzeł wystąpienia hello w Eksploratorze serwera. Zobacz [Azure roli architektura](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx) Aby uzyskać więcej informacji o procesach platformy Azure.

    ![Wybór typu kodu — okno dialogowe](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
4. procesy hello tooidentify, który jest dołączony debuger hello toowhich, otwórz hello procesów — okno dialogowe, menu hello, wybierając debugowania, Windows, procesów. (Klawiatury: Ctrl + Alt + Z) toodetach określonego procesu, otwórz menu skrótów, a następnie wybierz **odłączyć procesu**. Lub, zlokalizuj węzeł wystąpienia hello w Eksploratorze serwera, odnaleźć hello procesu, otwórz menu skrótów, a następnie wybierz **odłączyć procesu**.

    ![Debugowanie procesów](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC690787.gif)

> [!WARNING]
> Uniknąć długich zatrzymane na punktów przerwania podczas zdalnego debugowania. Azure traktuje procesu, który został zatrzymany przez czas dłuższy niż kilka minut odpowiada, a następnie zatrzymuje wysyłania ruchu toothat wystąpienia. Jeśli zatrzymasz zbyt długo, msvsmon.exe odłączenie od procesu hello.
>
>

Debuger hello toodetach od wszystkich procesów w wystąpienia lub hello Otwórz menu skrótów dla roli hello lub wystąpienia, debugowanie, a następnie wybierz, roli **odłączyć debugera**.

## <a name="limitations-of-remote-debugging-in-azure"></a>Ograniczenia debugowania zdalnego na platformie Azure
Z 2.3 zestawu SDK platformy Azure zdalnego debugowania ma następujące ograniczenia hello.

* Z funkcją debugowania zdalnego włączone, nie można opublikować w którym dowolnej roli ma więcej niż 25 wystąpień usługi w chmurze.
* Debuger Hello używa too30424 30400 portów, 31400 too31424 i 32400 too32424. Jeśli spróbujesz toouse żadnego z tych portów, nie będzie możliwe toopublish, usługi i jeden hello następujące komunikaty o błędach będzie widoczna w hello dziennik aktywności platformy Azure:

  * Błąd podczas sprawdzania poprawności hello pliku .cscfg względem pliku hello plik csdef.
    Witaj zarezerwowany zakres portów "range" dla punktu końcowego, który nakłada się już zdefiniowany port lub zakres na Microsoft.WindowsAzure.Plugins.RemoteDebugger.Connector roli "roli".
  * Alokacja nie powiodła się. Spróbuj ponownie później, spróbuj zmniejszyć hello rozmiar maszyny Wirtualnej lub liczbę wystąpień roli lub spróbuj przeprowadzić wdrożenie w innym regionie tooa.

## <a name="debugging-azure-virtual-machines"></a>Debugowanie maszyn wirtualnych platformy Azure
Można debugować programy uruchamiane na maszynach wirtualnych Azure za pomocą Eksploratora serwera w programie Visual Studio. Po włączeniu zdalnego debugowania na maszynie wirtualnej platformy Azure, Azure instaluje hello zdalnego debugowania rozszerzenia na maszynie wirtualnej hello. Następnie można dołączyć tooprocesses na maszynie wirtualnej hello i debugowania w zwykły sposób.

> [!NOTE]
> Maszyny wirtualne utworzone za pośrednictwem hello Azure resource manager stosu można zdalnie debugować przy użyciu Eksplorator chmury w programie Visual Studio 2015. Aby uzyskać więcej informacji, zobacz [zarządzania zasobami Azure za pomocą Eksploratora chmury](http://go.microsoft.com/fwlink/?LinkId=623031).
>
>

### <a name="toodebug-an-azure-virtual-machine"></a>toodebug maszyny wirtualnej platformy Azure
1. W Eksploratorze serwera rozwiń węzeł maszyn wirtualnych hello i hello wybierz węzeł hello maszyny wirtualnej, które mają toodebug.
2. Otwórz menu kontekstowe hello i wybierz **włączyć debugowanie**. Po otrzymaniu monitu, jeśli masz pewności, jeśli chcesz tooenable debugowania na maszynie wirtualnej hello, wybierz opcję **tak**.

    Azure instaluje rozszerzenia debugowania zdalnego hello na powitania maszyny wirtualnej tooenable debugowania.

    ![Maszyna wirtualna włączyć polecenie debugowania](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Dziennik aktywności platformy Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
3. Po zakończeniu instalowania rozszerzenia debugowania zdalnego hello Otwórz menu kontekstowe maszyny wirtualnej hello i wybierz **dołączyć debuger...**

    Azure pobiera listę procesów hello na maszynie wirtualnej hello i wyświetla je w oknie dialogowym tooProcess Attach hello.

    ![Dołącz debuger polecenia](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
4. W hello **dołączyć tooProcess** okno dialogowe, wybierz opcję **wybierz** wyniki hello toolimit listy tooshow tylko hello typów kodu mają toodebug. Można debugować kodu 32 - lub 64-bitowych zarządzanego i kodu natywnego.

    ![Wybór typu kodu — okno dialogowe](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
5. Wybierz hello procesy mają toodebug hello maszyny wirtualnej, a następnie wybierz **Attach**. Na przykład wybrać hello procesu w3wp.exe, jeśli potrzebujesz toodebug aplikacji sieci web na maszynie wirtualnej hello. Zobacz [debugowania jeden lub więcej procesów w programie Visual Studio](https://msdn.microsoft.com/library/jj919165.aspx) i [Azure roli architektura](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx) Aby uzyskać więcej informacji.

## <a name="create-a-web-project-and-a-virtual-machine-for-debugging"></a>Tworzenie projektu sieci web i maszyny wirtualnej do debugowania
Przed opublikowaniem projektu platformy Azure, może być bardzo przydatne tootest go w środowisku zawartych w niej obsługującej debugowania i testowania scenariuszy i której można zainstalować testowania i monitorowanie programów. Jest jednym ze sposobów toodo tooremotely debugowanie aplikacji na maszynie wirtualnej.

Projekty Visual Studio ASP.NET oferuje toocreate opcji przydatną maszyny wirtualnej, która służy do testowania aplikacji. Maszyna wirtualna Hello obejmuje najczęściej wymagane punkty końcowe, takie jak środowiska PowerShell, pulpitu zdalnego i WebDeploy.

### <a name="toocreate-a-web-project-and-a-virtual-machine-for-debugging"></a>toocreate projektu sieci web i maszyny wirtualnej do debugowania
1. W programie Visual Studio Utwórz nową aplikację sieci Web ASP.NET.
2. W oknie dialogowym Nowy projekt ASP.NET hello, w hello Azure sekcji wybierz **maszyny wirtualnej** w polu listy rozwijanej hello. Pozostaw hello **Utwórz zasoby zdalne** zaznaczone pole wyboru. Wybierz **OK** tooproceed.

    Witaj **Utwórz maszynę wirtualną na platformie Azure** zostanie wyświetlone okno dialogowe.

    ![Tworzenie projektu sieci web platformy ASP.NET — okno dialogowe](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746723.png)

    **Uwaga:** użytkownik zostanie zapytany toosign w tooyour konto platformy Azure, jeśli użytkownik nie jest jeszcze zarejestrowany.

1. Wybierz hello różne ustawienia dla hello maszyny wirtualnej, a następnie wybierz **OK**. Zobacz [maszyn wirtualnych](http://go.microsoft.com/fwlink/?LinkId=623033) Aby uzyskać więcej informacji.

    Wprowadzona nazwa DNS nazwa Hello będzie hello nazwa hello maszyny wirtualnej.

    ![Utwórz maszynę wirtualną na okno dialogowe Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746724.png)

    Azure tworzy hello maszyny wirtualnej, a następnie przepisów i konfiguruje hello punktów końcowych, takie jak pulpitu zdalnego i narzędzia Web Deploy
2. Wybierz węzeł maszyny wirtualnej hello w Eksploratorze serwera, po hello maszyny wirtualnej jest w pełni skonfigurowane.
3. Otwórz menu kontekstowe hello i wybierz **włączyć debugowanie**. Po otrzymaniu monitu, jeśli masz pewności, jeśli chcesz tooenable debugowania na maszynie wirtualnej hello, wybierz opcję **tak**.

    Azure instaluje hello debugowania rozszerzenia toohello maszyny wirtualnej tooenable debugowania zdalnego.

    ![Maszyna wirtualna włączyć polecenie debugowania](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Dziennik aktywności platformy Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
4. Opublikować projekt w sposób opisany w [porady: Wdrażanie publikowania projektu sieci Web za pomocą jednego kliknięcia w programie Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx). Ponieważ chcesz, aby toodebug hello w na maszynie wirtualnej, hello **ustawienia** strony hello **publikowanie w sieci Web** kreatora wybierz **debugowania** jako hello konfiguracji. Dzięki temu symbole kodu są dostępne podczas debugowania.

    ![Ustawienia publikowania](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718349.png)
5. W hello **opcji publikowania pliku**, wybierz pozycję **Usuń dodatkowe pliki w miejscu docelowym** Jeśli hello projektu zostało już wdrożone wcześniej.
6. Po publikuje hello projektu, w menu kontekstowym maszyny wirtualnej hello w Eksploratorze serwera wybierz **dołączyć debuger...**

    Azure pobiera listę procesów hello na maszynie wirtualnej hello i wyświetla je w oknie dialogowym tooProcess Attach hello.

    ![Dołącz debuger polecenia](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
7. W hello **dołączyć tooProcess** okno dialogowe, wybierz opcję **wybierz** wyniki hello toolimit listy tooshow tylko hello typów kodu mają toodebug. Można debugować kodu 32 - lub 64-bitowych zarządzanego i kodu natywnego.

    ![Wybór typu kodu — okno dialogowe](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
8. Wybierz hello procesy mają toodebug hello maszyny wirtualnej, a następnie wybierz **Attach**. Na przykład wybrać hello procesu w3wp.exe, jeśli potrzebujesz toodebug aplikacji sieci web na maszynie wirtualnej hello. Zobacz [debugowania jeden lub więcej procesów w programie Visual Studio](https://msdn.microsoft.com/library/jj919165.aspx) Aby uzyskać więcej informacji.

## <a name="next-steps"></a>Następne kroki
* Użyj **Intellitrace** toocollect dziennika wywołań i zdarzenia z wersji serwera. Zobacz [debugowania usługi opublikowana chmura za pomocą funkcji IntelliTrace i Visual Studio](http://go.microsoft.com/fwlink/?LinkID=623016).
* Użyj **diagnostyki Azure** toolog szczegółowe informacje o uruchamianiu kodu w ramach ról, czy role hello są uruchomione w środowisku projektowym hello lub na platformie Azure. Zobacz [zbierania danych rejestrowania za pomocą diagnostyki Azure](http://go.microsoft.com/fwlink/p/?LinkId=400450).
