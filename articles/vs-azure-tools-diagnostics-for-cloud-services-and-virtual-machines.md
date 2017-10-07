---
title: "aaaConfiguring diagnostyki dla usług Azure Cloud Services i maszyn wirtualnych | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooconfigure informacje diagnostyczne do debugowania usług Azure cloude i maszynach wirtualnych (VM) w programie Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: e70cd7b4-6298-43aa-adea-6fd618414c26
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 74cdf49413d6d89a84195070dd9d817da2463373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-diagnostics-for-azure-cloud-services-and-virtual-machines"></a>Konfigurowanie diagnostyki dla usług w chmurze Azure i maszyny wirtualne
Jeśli potrzebujesz tootroubleshoot usługi w chmurze Azure lub maszyny wirtualnej platformy Azure, Diagnostyka Azure można skonfigurować łatwiej przy użyciu programu Visual Studio. Diagnostyka Azure powoduje przechwycenie danych systemowych i danych rejestrowania na powitania maszyn wirtualnych i wystąpień maszyn wirtualnych, które są uruchamiane usługi w chmurze i przesyła dane do wybranego konta magazynu. Zobacz [Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md) Aby uzyskać więcej informacji o diagnostyce rejestrowania na platformie Azure.

W tym temacie opisano sposób tooenable i skonfigurować diagnostycznych platformy Azure w programie Visual Studio, przed i po wdrożeniu, a także na maszynach wirtualnych platformy Azure. Przedstawia on także jak typy hello tooselect toocollect informacji diagnostycznych i jak zbierane są informacje hello tooview po nim.

Diagnostyka Azure można skonfigurować w hello następujące sposoby:

* Możesz zmienić ustawienia konfiguracji diagnostyki za pośrednictwem hello **konfiguracji diagnostyki** okno dialogowe w programie Visual Studio. Ustawienia Hello są zapisywane w pliku o nazwie diagnostics.wadcfgx (diagnostics.wadcfg Azure SDK 2.4 lub wcześniej). Alternatywnie można bezpośrednio modyfikować hello pliku konfiguracji. Jeśli ręcznie zaktualizować plik hello, hello konfiguracji zmiany zaczną obowiązywać hello następnym wdrażania tooAzure usługi chmury hello lub usługi hello uruchomienia w emulatorze hello.
* Użyj **Eksplorator chmury** lub **Eksploratora serwera** w Visual Studio toochange hello ustawień diagnostycznych uruchomiona usługa w chmurze lub maszyny wirtualnej.

## <a name="azure-26-diagnostics-changes"></a>Zmiany diagnostyki Azure 2.6
Azure SDK w wersji 2.6 projektów programu Visual Studio hello następujące zmiany zostały wprowadzone. (Te zmiany mają zastosowanie również toolater wersji zestawu SDK platformy Azure.)

* emulator lokalne powitania obsługuje teraz diagnostyki. Oznacza to, można zbierać dane diagnostyczne i upewnij się, że aplikacja tworzy hello prawo śladów podczas tworzenia i testowania w programie Visual Studio. Witaj parametry połączenia `UseDevelopmentStorage=true` umożliwia zbieranie danych diagnostycznych, gdy używasz projekt usługi w chmurze w programie Visual Studio przy użyciu emulatora magazynu Azure hello. Wszystkie dane diagnostyczne są zbierane na koncie magazynu hello (Programowanie magazynu).
* Parametry połączenia konta magazynu diagnostyki Hello (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) znajduje się jeszcze raz w pliku konfiguracji (cscfg) hello usługi. W systemie Azure SDK 2.5 konto magazynu diagnostyki hello została określona w pliku diagnostics.wadcfgx hello.

Istnieją pewne ważne różnice między jak parametry połączenia hello działał w 2.4 zestawu SDK platformy Azure i starszych i jak działa w Azure SDK w wersji 2.6 lub nowszej.

* W 2.4 zestawu SDK platformy Azure i starszych parametry połączenia hello był używany jako środowisko uruchomieniowe w hello diagnostyki wtyczki tooget hello informacji o koncie magazynu przesyłania dzienników diagnostycznych.
* W Azure SDK w wersji 2.6 lub nowszej ciąg połączenia diagnostyki hello jest używany przez rozszerzenie Diagnostyka programu Visual Studio tooconfigure hello hello magazynu odpowiednie informacje o koncie podczas publikowania. Parametry połączenia Hello umożliwia definiowanie różnych kont magazynu dla konfiguracji innej usługi, które Visual Studio będzie korzystać w przypadku publikowania. Jednak ponieważ hello diagnostyki wtyczki nie jest już dostępny (po 2.5 zestawu SDK platformy Azure), plik .cscfg hello samodzielnie nie można włączyć hello rozszerzenia diagnostyki. Masz rozszerzenia hello tooenable z osobna za pomocą narzędzi, takich jak Visual Studio lub programu PowerShell.
* proces hello toosimplify konfigurowania rozszerzenia diagnostyki hello przy użyciu programu PowerShell, hello pakietu wyjście z programu Visual Studio zawiera także hello publicznej konfiguracji XML hello diagnostyki rozszerzenia dla poszczególnych ról. Visual Studio będzie korzystać hello diagnostyki połączenia ciąg toopopulate hello informacji o koncie magazynu w konfiguracji publicznego hello. pliki konfiguracji publicznego Hello są tworzone w folderze rozszerzenia hello i wykonaj wzorzec hello PaaSDiagnostics. &lt;RoleName >. PubConfig.xml. Wszystkie wdrożenia programu PowerShell na podstawie można użyć tego wzorca toomap każdego tooa konfiguracji roli.
* Witaj parametry połączenia w pliku .cscfg hello jest już używana przez hello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) tooaccess hello danych diagnostycznych, dlatego może być wyświetlany w hello **monitorowanie** wymagane parametry połączenia hello kartę tooconfigure hello usługi tooshow pełne dane w portalu hello monitorowania.

## <a name="migrating-projects-tooazure-sdk-26-and-later"></a>Migrowanie projektów tooAzure SDK 2.6 lub nowszej
Podczas migrowania z tooAzure Azure SDK 2.5 SDK w wersji 2.6 lub nowszej, jeśli masz konto magazynu diagnostyki określone w pliku .wadcfgx hello, następnie pozostanie on istnieje. Zaletą tootake hello elastyczność za pomocą innego magazynu kont do innego magazynu konfiguracji, należy dodać projekt tooyour ciąg połączenia hello toomanually. W przypadku migrowania projektu z Azure SDK 2.4 lub starszych tooAzure 2.6 zestawu SDK, następnie hello diagnostyki parametry połączenia zostaną zachowane. Pamiętaj jednak zmiany hello jak parametry połączenia są traktowane w Azure SDK w wersji 2.6 określone w poprzedniej sekcji hello.

### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Jak określa konto magazynu diagnostyki hello w Visual Studio
* Jeśli parametry połączenia diagnostyki jest określone w pliku .cscfg hello, Visual Studio używa on tooconfigure hello diagnostyki rozszerzenia podczas publikowania i podczas generowania pliki xml konfiguracji publicznego hello podczas pakowania.
* Jeśli ciąg połączenia diagnostyki nie została określona w pliku .cscfg hello, następnie Visual Studio w języku konta magazynu hello toousing określonego w hello .wadcfgx tooconfigure hello diagnostyki rozszerzenie pliku podczas publikowania i generowania hello publicznego pliki xml konfiguracji podczas pakowania.
* Parametry połączenia diagnostyki Hello w pliku .cscfg hello mają pierwszeństwo przed hello konta magazynu w pliku .wadcfgx hello. Jeśli parametry połączenia diagnostyki jest określona w pliku .cscfg hello, następnie Visual Studio użyty i ignoruje hello konta magazynu w .wadcfgx.

### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>Co to Witaj, "Aktualizuj parametry połączenia magazynu programowanie..." czy pole wyboru?
Witaj wyboru **zaktualizować parametry połączenia magazynu programowanie dla diagnostyki i buforowanie z poświadczeniami konta magazynu Microsoft Azure podczas publikowania tooMicrosoft Azure** daje żadnych tooupdate wygodny sposób Programowanie parametry połączenia konta magazynu z kontem magazynu platformy Azure hello określony podczas publikowania.

Załóżmy na przykład, zaznacz to pole wyboru i określa parametry połączenia diagnostyki hello `UseDevelopmentStorage=true`. Podczas publikowania hello tooAzure projektu programu Visual Studio będzie automatycznie zaktualizować parametry połączenia diagnostyki hello z kontem magazynu hello określone w Kreatorze publikowania hello. Jednak jeśli konto magazynu rzeczywista określono jako parametry połączenia diagnostyki hello, następnie to konto jest używana zamiast tego.

## <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Diagnostyka funkcji różnice między 2.4 zestawu SDK platformy Azure i wcześniej i Azure SDK, 2.5 lub nowszej
Jeśli uaktualniasz projektu z tooAzure Azure SDK 2.4 SDK, 2.5 lub nowszej, powinna zawierać się w hello uwadze następujące różnice funkcji diagnostyki.

* **Konfiguracyjne interfejsy API są przestarzałe** — trybu diagnostyki jest dostępna w 2.4 zestawu SDK platformy Azure i jego wcześniejsze wersje, ale jest przestarzała w wersji 2.5 zestawu SDK platformy Azure i nowszych. Jeśli aktualnie zdefiniowano konfigurację diagnostyki w kodzie, konieczne będzie tooreconfigure tych ustawień od podstaw w projekcie migrowanych hello aby pracy tookeep diagnostyki. plik konfiguracji diagnostyki Hello Azure SDK 2.4 jest diagnostics.wadcfg i diagnostics.wadcfgx dla 2.5 zestawu SDK platformy Azure i nowszych.
* **Można skonfigurować tylko na poziomie roli hello, nie na poziomie wystąpienia hello diagnostyki dla aplikacji usługi w chmurze.**
* **Za każdym razem, gdy wdrażanie aplikacji, zaktualizowano konfigurację diagnostyki hello** — może to powodować problemy z parzystością, jeśli zmiana konfiguracji diagnostyki z Eksploratora serwera, a następnie ponowne wdrożenie aplikacji.
* **W wersji 2.5 zestawu SDK platformy Azure i nowszych, zrzuty awaryjne są konfigurowane w pliku konfiguracji diagnostyki hello, nie w kodzie** — Jeśli masz zrzuty awaryjne skonfigurowane w kodzie, będziesz mieć toomanually transfer hello konfiguracji z pliku konfiguracji toohello kodu, Ponieważ zrzuty awaryjne hello nie są przenoszone podczas tooAzure migracji hello 2.6 zestawu SDK.

## <a name="enable-diagnostics-in-cloud-service-projects-before-deploying-them"></a>Włącz diagnostykę w projekty usługi w chmurze przed ich wdrożeniem
W programie Visual Studio możesz toocollect danych diagnostycznych dotyczących ról, które działają na platformie Azure po uruchomieniu usługi hello w emulatorze hello przed jego wdrożeniem. Wszystkie ustawienia toodiagnostics zmiany w programie Visual Studio są zapisywane w pliku konfiguracyjnym diagnostics.wadcfgx hello. Te ustawienia konfiguracji Określ konto magazynu hello lokalizacji zapisywania danych diagnostycznych podczas wdrażania usługi w chmurze.

[!INCLUDE [cloud-services-wad-warning](../includes/cloud-services-wad-warning.md)]

### <a name="tooenable-diagnostics-in-visual-studio-before-deployment"></a>Diagnostyka tooenable w programie Visual Studio przed wdrożeniem
1. W menu skrótów hello roli hello, interesującego, wybierz **właściwości**, a następnie wybierz pozycję hello **konfiguracji** kartę w roli hello **właściwości** okna.
2. W hello **diagnostyki** sekcji, upewnij się, że hello **włączyć diagnostyki** pole wyboru jest zaznaczone.
   
    ![Dostęp do opcji Włącz diagnostyki hello](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796660.png)
3. Wybrać hello wielokropek (...) przycisk toospecify hello konta magazynu, w którym ma toobe danych diagnostycznych hello przechowywane. Konto magazynu Hello wybrane będzie hello miejsce przechowywania danych diagnostycznych.
   
    ![Określ toouse konta magazynu hello](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796661.png)
4. W hello **utworzyć parametry połączenia magazynu** oknie dialogowym Określ, czy mają tooconnect przy użyciu hello emulatora magazynu Azure, subskrypcji platformy Azure, lub ręcznie wprowadzić poświadczenia.
   
    ![Okno dialogowe konta magazynu](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796662.png)
   
   * Jeśli zostanie wybrana opcja emulatora magazynu Azure Microsoft hello, tooUseDevelopmentStorage ustawiono parametrów połączenia hello = true.
   * Jeśli opcja hello Twojej subskrypcji, możesz hello toouse i hello nazwa konta subskrypcji platformy Azure. Możesz wybrać hello Zarządzanie kontami przycisk toomanage subskrypcji platformy Azure.
   * Jeśli zostanie wybrana opcja poświadczenia hello wpisywane ręcznie, możesz tooenter zostanie wyświetlony monit o hello nazwy i klucza konta Azure, które chcesz toouse hello.
5. Wybierz hello **Konfiguruj** hello tooview przycisk **konfiguracji diagnostyki** okno dialogowe. Każda karta (z wyjątkiem **ogólne** i **katalogów dziennika**) reprezentuje źródło danych diagnostycznych, które można zebrać. Karta domyślne Hello, **ogólne**, oferuje hello następujących opcji zbierania danych diagnostycznych: **tylko błędy**, **wszystkie informacje**, i **plan niestandardowy** . Witaj opcji domyślnej **tylko błędy**, przyjmuje hello minimalnej liczbie magazynu, ponieważ nie transferu, ostrzeżenia lub komunikaty śledzenia. Hello wszystkich informacji opcję transferów hello większość informacji i, w związku z tym hello najdroższych opcji pod względem pamięci masowej.
   
    ![Włącz diagnostyki Azure i konfiguracji](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
6. Na przykład wybierz hello **plan niestandardowy** opcji, możesz dostosować hello dane zbierane.
7. Witaj **przydział dysku w MB** pole określa, ile miejsca chcesz tooallocate w magazynie konta dla danych diagnostycznych. Wartość domyślna hello można zmienić, jeśli chcesz.
8. Na każdej karcie dane diagnostyczne mają toocollect, wybierz jej **włączyć Transfer <log type>**  pole wyboru. Na przykład, jeśli chcesz toocollect Dzienniki aplikacji wybierz opcję hello **włączyć transferu Dzienniki aplikacji** pole wyboru na powitania **Dzienniki aplikacji** kartę. Ponadto określ wszelkie inne informacje wymagane przez każdego typu danych diagnostycznych. Zobacz sekcję hello **Konfigurowanie źródeł danych diagnostycznych** dalszej części tego tematu, aby uzyskać informacje o konfiguracji na poszczególnych kartach.
9. Po włączeniu kolekcji wszystkie dane diagnostyczne hello chcesz wybrać hello **OK** przycisku.
10. Uruchom projekt usługi chmury Azure w programie Visual Studio w zwykły sposób. Jak za pomocą aplikacji hello dziennika informacje, które są włączone jest zapisywany wskazane konto magazynu Azure toohello.

## <a name="enable-diagnostics-in-azure-virtual-machines"></a>Włącz diagnostykę w maszynach wirtualnych platformy Azure
W programie Visual Studio można wybrać dane diagnostyczne toocollect maszyn wirtualnych platformy Azure.

### <a name="tooenable-diagnostics-in-azure-virtual-machines"></a>Diagnostyka tooenable w maszynach wirtualnych platformy Azure
1. W **Eksploratora serwera**, wybierz hello Azure węzeł, a następnie połącz tooyour subskrypcji platformy Azure, jeśli jeszcze nie zostało nawiązane.
2. Rozwiń węzeł hello **maszyn wirtualnych** węzła. Utwórz nową maszynę wirtualną lub wybierz jedną, która jest już istnieje.
3. W menu skrótów hello maszyny wirtualnej hello interesującego wybierz **Konfiguruj**. Pokazuje to okno dialogowe konfiguracji maszyny wirtualnej hello.
   
    ![Konfigurowanie maszyny wirtualnej platformy Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796663.png)
4. Jeśli to nie jest jeszcze zainstalowana, Dodaj hello rozszerzenia Diagnostyka agenta monitorowania firmy Microsoft. To rozszerzenie umożliwia zbieranie danych diagnostycznych dotyczących hello maszyny wirtualnej platformy Azure. Z listy zainstalowanych rozszerzeń hello hello dostępne rozszerzenia listy rozwijanej wybierz menu wybierz opcję, a następnie wybierz pozycję Diagnostyka agenta monitorowania firmy Microsoft.
   
    ![Instalowanie rozszerzenia maszyny wirtualnej platformy Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766024.png)
   
   > [!NOTE]
   > Inne rozszerzenia diagnostyki są dostępne dla maszyn wirtualnych. Aby uzyskać więcej informacji zobacz funkcje i rozszerzenia maszyny Wirtualnej Azure.
   > 
   > 
5. Wybierz hello **Dodaj** przycisk tooadd hello rozszerzenie i wyświetl jego **konfiguracji diagnostyki** okno dialogowe.
6. Wybierz hello **Konfiguruj** przycisk toospecify konta magazynu, a następnie wybierz pozycję hello **OK** przycisku.
   
    Każda karta (z wyjątkiem **ogólne** i **katalogów dziennika**) reprezentuje źródło danych diagnostycznych, które można zebrać.
   
    ![Włącz diagnostyki Azure i konfiguracji](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
   
    Karta domyślne Hello, **ogólne**, oferuje hello następujących opcji zbierania danych diagnostycznych: **tylko błędy**, **wszystkie informacje**, i **plan niestandardowy** . Witaj opcji domyślnej **tylko błędy**, przyjmuje hello minimalnej liczbie magazynu, ponieważ nie transferu, ostrzeżenia lub komunikaty śledzenia. Witaj **wszystkie informacje** opcję transferów hello większość informacji i dlatego, jest opcja najdroższych hello pod względem pamięci masowej.
7. Na przykład wybierz hello **plan niestandardowy** opcji, możesz dostosować hello dane zbierane.
8. Witaj **przydział dysku w MB** pole określa, ile miejsca chcesz tooallocate w magazynie konta dla danych diagnostycznych. Wartość domyślna hello można zmienić, jeśli chcesz.
9. Na każdej karcie dane diagnostyczne mają toocollect, wybierz jej **włączyć Transfer <log type>**  pole wyboru.
   
    Na przykład, jeśli chcesz toocollect Dzienniki aplikacji wybierz opcję hello **włączyć transferu Dzienniki aplikacji** pole wyboru na powitania **Dzienniki aplikacji** kartę. Ponadto określ wszelkie inne informacje wymagane przez każdego typu danych diagnostycznych. Zobacz sekcję hello **Konfigurowanie źródeł danych diagnostycznych** dalszej części tego tematu, aby uzyskać informacje o konfiguracji na poszczególnych kartach.
10. Po włączeniu kolekcji wszystkie dane diagnostyczne hello chcesz wybrać hello **OK** przycisku.
11. Zapisz hello zaktualizowany projekt.
    
     Zostanie wyświetlony komunikat w hello **dziennik aktywności programu Microsoft Azure** okno hello maszyny wirtualnej zostały zaktualizowane.

## <a name="configure-diagnostics-data-sources"></a>Konfigurowanie źródeł danych diagnostycznych
Po włączeniu funkcji zbierania danych diagnostycznych, można wybrać dokładnie źródeł danych ma toocollect i jakie informacje są zbierane. Witaj poniżej znajduje się lista kart w hello **konfiguracji diagnostyki** okno dialogowe i oznacza każdej opcji konfiguracji.

### <a name="application-logs"></a>Dzienniki aplikacji
**Dzienniki aplikacji** zawierają informacje diagnostyczne produkowane przez aplikację sieci web. Dzienniki aplikacji toocapture, wybierz opcję hello **włączyć transferu Dzienniki aplikacji** pole wyboru. Można zwiększyć lub zmniejszyć hello liczbę minut, gdy są przekazywane Dzienniki aplikacji hello tooyour konta magazynu, zmieniając hello **transferu okres (min)** wartość. Można również zmienić hello ilość informacji przechwycone w dzienniku hello, ustawiając wartość poziomu dziennika hello. Na przykład można wybrać **pełne** tooget więcej informacji lub wybierz **krytyczny** toocapture tylko krytyczne błędy. Jeśli masz diagnostyczne zależne od dostawcy, który emituje Dzienniki aplikacji, można przechwycić je przez dodanie toohello GUID dostawcy hello **GUID dostawcy** pole.

  ![Dzienniki aplikacji](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758145.png)

  Zobacz [Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md) Aby uzyskać więcej informacji o dziennikach aplikacji.

### <a name="windows-event-logs"></a>Dzienniki zdarzeń systemu Windows
Dzienniki zdarzeń systemu Windows toocapture, wybierz opcję hello **włączyć transferu dzienniki zdarzeń systemu Windows** pole wyboru. Można zwiększyć lub zmniejszyć hello liczbę minut, gdy są przekazywane dzienniki zdarzeń hello tooyour konta magazynu, zmieniając hello **transferu okres (min)** wartość. Zaznacz pola wyboru hello hello typy zdarzeń, które mają tootrack.

  ![Dzienniki zdarzeń](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796664.png)

Jeśli używasz programu Azure SDK Version 2.6 lub nowszej i chcesz toospecify niestandardowe źródło danych, wprowadź go w hello  **<Data source name>**  tekst pola, a następnie wybierz pozycję hello **Dodaj** przycisku Dalej tooit. Witaj zostało dodane źródło danych pliku diagnostics.cfcfg toohello.

Jeśli używasz 2.5 zestawu SDK platformy Azure i mają toospecify niestandardowe źródło danych, możesz dodać ją toohello `WindowsEventLog` pliku sekcji hello diagnostics.wadcfgx, taki jak hello poniższy przykład.

```
<WindowsEventLog scheduledTransferPeriod="PT1M">
   <DataSource name="Application!*" />
   <DataSource name="CustomDataSource!*" />
</WindowsEventLog>
```
### <a name="performance-counters"></a>Liczniki wydajności
Informacje o liczniku wydajności może pomóc w Znajdź wąskich gardeł systemu i poprawienia wydajności systemu i aplikacji. Zobacz [tworzenie i Użyj liczników wydajności w aplikacji Azure](https://msdn.microsoft.com/library/azure/hh411542.aspx) Aby uzyskać więcej informacji. Liczniki wydajności toocapture, wybierz opcję hello **włączyć transferu liczniki wydajności** pole wyboru. Można zwiększyć lub zmniejszyć hello liczbę minut, gdy są przekazywane dzienniki zdarzeń hello tooyour konta magazynu, zmieniając hello **transferu okres (min)** wartość. Wybierz pola wyboru hello hello liczniki wydajności, które mają tootrack.

  ![Liczniki wydajności](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758147.png)

tootrack licznika wydajności, które nie ma na liście, wprowadź go za pomocą hello sugerowane składni, a następnie wybierz pozycję hello **Dodaj** przycisku. Witaj systemu operacyjnego na maszynie wirtualnej hello Określa, które liczniki wydajności można śledzić. Aby uzyskać więcej informacji na temat składni, zobacz [określania ścieżki licznika](https://msdn.microsoft.com/library/windows/desktop/aa373193.aspx).

### <a name="infrastructure-logs"></a>Dzienniki infrastruktury
Dzienniki infrastruktury toocapture zawierających informacje o hello infrastruktury diagnostycznych platformy Azure, moduł RemoteAccess hello i moduł RemoteForwarder hello zaznacz hello **włączyć transferu dzienniki infrastruktury**pole wyboru. Można zwiększyć lub zmniejszyć hello liczbę minut, gdy są przekazywane dzienniki hello tooyour konta magazynu, zmieniając wartość okresu Transfer (min) hello.

  ![Dzienniki infrastruktury diagnostyki](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758148.png)

  Zobacz [zbierania danych rejestrowania za pomocą diagnostyki Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx) Aby uzyskać więcej informacji.

### <a name="log-directories"></a>Katalogi dziennika
Toocapture dziennika katalogi, które zawierają dane zbierane z katalogów dziennika dla żądań usług Internet Information Services (IIS), żądań zakończonych niepowodzeniem lub foldery, które zostanie wybrana, wybierz opcję hello **włączyć transferu katalogów dziennika**pole wyboru. Można zwiększyć lub zmniejszyć hello liczbę minut, gdy są przekazywane dzienniki hello tooyour konta magazynu, zmieniając hello **transferu okres (min)** wartość.

Można wybrać pola hello ma toocollect, takich jak dzienniki hello **dzienniki programu IIS** i **nie powiodło się żądanie** dzienniki. Domyślne nazwy kontenera magazynu jest dostępny, ale można zmienić nazwy hello, jeśli chcesz.

Ponadto można przechwycić dzienniki z dowolnego folderu. Po prostu wprowadź ścieżkę hello hello **dziennika z katalogu bezwzględną** sekcji, a następnie wybierz pozycję hello **Dodaj katalog** przycisku. Witaj dzienniki będzie można przechwycić toohello określony kontenerów.

  ![Katalogi dziennika](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796665.png)

### <a name="etw-logs"></a>Dzienniki zdarzeń systemu Windows
Jeśli używasz [śledzenia zdarzeń dla systemu Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx) (ETW) i chcesz toocapture ETW dzienników, wybierz hello **włączyć transferu dzienniki zdarzeń systemu Windows** pole wyboru. Można zwiększyć lub zmniejszyć hello liczbę minut, gdy są przekazywane dzienniki hello tooyour konta magazynu, zmieniając hello **transferu okres (min)** wartość.

zdarzenia Hello są przechwytywane ze źródeł zdarzeń i manifesty zdarzeń, które określisz. toospecify źródło zdarzenia, wprowadź nazwę w hello **źródła zdarzeń** sekcji, a następnie wybierz pozycję hello **Dodaj źródło zdarzeń** przycisku. Analogicznie, można określić manifest zdarzeń w hello **manifesty zdarzeń** sekcji, a następnie wybierz pozycję hello **Dodaj Manifest zdarzeń** przycisku.

  ![Dzienniki zdarzeń systemu Windows](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766025.png)

  Hello ETW framework jest obsługiwana w programie ASP.NET za pośrednictwem klas w hello [System.Diagnostics.aspx] (przestrzeń nazw https://msdn.microsoft.com/library/system.diagnostics (v=vs.110). przestrzeń nazw Microsoft.WindowsAzure.Diagnostics Hello, która dziedziczy i rozszerza standard [System.Diagnostics.aspx] (klasy https://msdn.microsoft.com/library/system.diagnostics (v=vs.110), umożliwia użycie hello () [System.Diagnostics.aspx] https://msdn.microsoft.com/library/system.Diagnostics (v=vs.110) jako struktury rejestrowania, w hello środowiska platformy Azure. Aby uzyskać więcej informacji, zobacz [zająć kontroli z rejestrowania i śledzenia w systemie Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) i [Włączanie diagnostyki w usług Azure Cloud Services i maszyn wirtualnych](cloud-services/cloud-services-dotnet-diagnostics.md).

### <a name="crash-dumps"></a>Zrzuty awaryjne
Informacje toocapture po awarii wystąpienia roli, zaznacz hello **włączyć przesyłanie awarii zrzuty** pole wyboru. (Ponieważ ASP.NET obsługuje większość wyjątki, jest zazwyczaj przydatne tylko w przypadku roli proces roboczy). Można zwiększyć lub zmniejszyć hello odsetek magazynu miejsca przeznaczone toohello zrzuty awaryjne, zmieniając hello **przydziału katalogu (%)** wartość. Możesz zmienić hello kontenera magazynu, gdzie są przechowywane zrzuty awaryjne hello i można wybrać, czy ma toocapture **pełne** lub **Mini** zrzutu.

procesy Hello aktualnie śledzone są wyświetlane. Zaznacz pola wyboru hello hello procesów, które mają toocapture. tooadd lista toohello innego procesu, wprowadź nazwę procesu hello, a następnie wybierz pozycję hello **proces dodawania** przycisku.

  ![Zrzuty awaryjne](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766026.png)

  Zobacz [zająć kontroli z rejestrowania i śledzenia w systemie Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) i [Microsoft Azure Diagnostics część 4: składniki Rejestrowanie niestandardowe i zmiany 1.3 diagnostyki Azure](http://justazure.com/microsoft-azure-diagnostics-part-4-custom-logging-components-azure-diagnostics-1-3-changes/) Aby uzyskać więcej informacji.

## <a name="view-hello-diagnostics-data"></a>Dane diagnostyczne hello widoku
Po zostały zebrane dane diagnostyczne hello usługi w chmurze lub maszynę wirtualną, możesz je wyświetlić.

### <a name="tooview-cloud-service-diagnostics-data"></a>dane diagnostyczne usługi tooview w chmurze
1. Wdrażanie usługi w chmurze w zwykły sposób, a następnie uruchom go.
2. Dane diagnostyczne hello można wyświetlić raportu, który generuje Visual Studio lub tabele na koncie magazynu. Otwórz tooview hello danych w raporcie, **Eksplorator chmury** lub **Eksploratora serwera**, otwórz menu skrótów hello hello węzła dla roli hello, interesującego, a następnie wybierz **widoku danych diagnostycznych** .
   
    ![Widok danych diagnostycznych](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748912.png)
   
    Zostanie wyświetlony raport pokazujący hello dostępnych danych.
   
    ![Raport diagnostyczny platformy Microsoft Azure w programie Visual Studio](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796666.png)
   
    Jeśli nie zostanie wyświetlone powitalne najnowszych danych, może być toowait dla okresu tooelapse transfer hello.
   
    Wybierz hello **Odśwież** łączenie danych hello aktualizacji tooimmediately lub interwał hello **automatycznego odświeżania** listy rozwijanej liście pole toohave hello danych aktualizowane automatycznie. tooexport hello błąd danych, wybierz hello **wyeksportować tooCSV** toocreate przycisk pliku wartości rozdzielanych przecinkami, można otworzyć w arkuszu kalkulacyjnym.
   
    W **Eksplorator chmury** lub **Eksploratora serwera**, otwórz konta magazynu hello skojarzoną z hello wdrożenia.
3. Otwórz hello diagnostyki tabel w podglądzie tabeli hello, a następnie przejrzyj hello zebranych danych. Dzienniki programu IIS i dzienników niestandardowych można otworzyć kontenera obiektów blob. Przeglądając hello w poniższej tabeli, można znaleźć kontener tabeli lub obiektu blob hello, który zawiera dane hello, interesujący Cię. Ponadto toohello danych w tym pliku dziennika, wpisy tabeli hello zawierać EventTickCount, DeploymentId, roli, a toohelp RoleInstance określeniu, jakie maszyny wirtualnej i roli generowane hello danych i kiedy. 
   
   | Dane diagnostyczne | Opis | Lokalizacja |
   | --- | --- | --- |
   | Dzienniki aplikacji |Dzienniki generowane przez wywołanie metody hello System.Diagnostics.Trace — klasa kodu. |WADLogsTable |
   | Dzienniki zdarzeń |Te dane są z dzienników zdarzeń systemu Windows hello na maszynach wirtualnych hello. System Windows przechowuje informacje w tych dziennikach, ale aplikacje i usługi także korzystania z nich błędy tooreport lub rejestrowania informacji. |WADWindowsEventLogsTable |
   | Liczniki wydajności |Na dowolnym licznika wydajności, które jest dostępne na maszynie wirtualnej hello może zbierać dane. system operacyjny Hello zapewnia liczniki wydajności, które zawierają wiele statystyk, takich jak pamięć użycia i czasu procesora. |WADPerformanceCountersTable |
   | Dzienniki infrastruktury |Te dzienniki są generowane na podstawie infrastruktury diagnostyki hello, sama. |WADDiagnosticInfrastructureLogsTable |
   | Dzienniki programu IIS |Te dzienniki rejestrowania żądań sieci web. Jeśli usługi w chmurze pobiera znaczną ilość ruchu, dzienniki te mogą być bardzo długie, dlatego należy zebrać i zapisane dane tej tylko wtedy, gdy zajdzie taka potrzeba. |Można znaleźć dzienniki żądanie nie powiodło się w kontenerze obiektów blob hello w obszarze wad iis failedreqlogs w ścieżce dla tego wdrożenia, roli i wystąpienia. Można znaleźć pełną dzienniki w obszarze logfiles-wad — usługi iis. Dla każdego pliku wpisów w tabeli WADDirectories hello. |
   | Zrzuty awaryjne |Informacje te stanowią binarny obraz procesu usługi chmury (zazwyczaj roli proces roboczy). |kontener obiektów blob wad zgniatania zrzutów |
   | Pliki dziennika niestandardowego |Dzienniki danych, który zostanie wstępnie zdefiniowane. |Na koncie magazynu, można określić lokalizacji hello kodu niestandardowego plików dziennika. Na przykład można określić kontenera niestandardowych obiektów blob. |
4. Jeśli zostały obcięte danych dowolnego typu, możesz spróbować zwiększa hello buforu dla tego typu danych lub skrócić interwał powitania między transferów danych z konta magazynu tooyour maszyny wirtualnej hello.
5. (opcjonalnie) Czyszczenie danych z magazynu hello konta od czasu do czasu tooreduce ogólnych kosztów magazynowania.
6. Po wykonaniu pełne wdrożenie hello diagnostics.cscfg pliku (.wadcfgx dla 2.5 zestawu SDK platformy Azure) są aktualizowane na platformie Azure i usługi w chmurze przejmuje konfiguracji diagnostyki tooyour żadnych zmian. Jeśli, należy zaktualizować istniejące wdrożenie, hello pliku .cscfg nie zostały zaktualizowane na platformie Azure. Ustawienia diagnostyki, można zmienić, wykonując kroki hello w następnej sekcji hello. Aby uzyskać więcej informacji na temat wykonywania pełne wdrożenie i aktualizowania istniejącego wdrożenia, zobacz [Kreator publikowania aplikacji Azure](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="tooview-virtual-machine-diagnostics-data"></a>dane diagnostyczne tooview maszyny wirtualnej
1. W menu skrótów hello hello maszyny wirtualnej, wybierz **dane diagnostyczne widoku**.
   
    ![Widok danych diagnostycznych w maszynie wirtualnej platformy Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766027.png)
   
    Spowoduje to otwarcie hello **podsumowanie diagnostyki** okna.
   
    ![Podsumowanie diagnostyki maszyny wirtualnej platformy Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796667.png)  
   
    Jeśli nie zostanie wyświetlone powitalne najnowszych danych, może być toowait dla okresu tooelapse transfer hello.
   
    Wybierz hello **Odśwież** łączenie danych hello aktualizacji tooimmediately lub interwał hello **automatycznego odświeżania** listy rozwijanej liście pole toohave hello danych aktualizowane automatycznie. tooexport hello błąd danych, wybierz hello **wyeksportować tooCSV** toocreate przycisk pliku wartości rozdzielanych przecinkami, można otworzyć w arkuszu kalkulacyjnym.

## <a name="configure-cloud-service-diagnostics-after-deployment"></a>Skonfigurować diagnostykę usługi w chmurze po wdrożeniu
Problem z usługą w chmurze jest badanie tego już uruchomiona, można toocollect dane, które nie określono przed roli hello pierwotnie wdrożone. W takim przypadku można uruchomić toocollect danych przy użyciu ustawień hello w Eksploratorze serwera. Możesz skonfigurować diagnostykę dla jednego wystąpienia lub wszystkich wystąpień hello w roli, w zależności od tego, czy otworzyć okno dialogowe konfiguracji diagnostyki hello menu skrótów hello wystąpienia hello lub hello roli. Jeśli skonfigurujesz hello roli węzła zmiany zastosować tooall wystąpień. Jeśli skonfigurujesz węzła wystąpienia hello zmiany mają zastosowanie tylko wystąpienia toothat.

### <a name="tooconfigure-diagnostics-for-a-running-cloud-service"></a>Diagnostyka tooconfigure dla uruchomionej usługi w chmurze
1. W Eksploratorze serwera rozwiń hello **usługi w chmurze** węzeł, a następnie rozwiń węzły toolocate hello roli lub wystąpienie ma tooinvestigate lub oba.
   
    ![Konfigurowanie diagnostyki](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748913.png)
2. Na powitania menu skrótów węzła wystąpienia lub węzeł ról, wybierz **ustawień diagnostycznych aktualizacji**, a następnie wybierz pozycję hello ustawień diagnostycznych, które mają toocollect.
   
    Informacje o ustawieniach konfiguracji hello, zobacz **Konfigurowanie źródeł danych diagnostycznych** w tym temacie. Aby dowiedzieć się jak tooview hello danych diagnostycznych, zobacz **wyświetlić dane diagnostyczne hello** w tym temacie.
   
    Jeśli zmienisz zbierania danych w **Eksploratora serwera**, te zmiany pozostaną aktywne do czasu ponownego wdrażania pełni usługi w chmurze. Jeśli używasz hello domyślne ustawienia publikowania, hello zmiany nie są zastępowane, ponieważ publikowania hello domyślne ustawienie jest tooupdate hello istniejące wdrożenie, a nie pełnego ponownego wdrażania. Wyczyść toomake się, że ustawienia hello w czasie wdrażania, przejdź toohello **Zaawansowane ustawienia** kartę w Kreatorze publikowania hello i wyczyść hello **aktualizację wdrożenia** wyboru. Podczas ponownego wdrażania z wyczyszczone pole wyboru ustawień hello przywrócić toothose w pliku hello .wadcfgx (lub .wadcfg) zgodnie z ustaleniami za pomocą edytora właściwości hello hello roli. Po zaktualizowaniu wdrożenia usługi Azure śledzi hello stare ustawienia.

## <a name="troubleshoot-azure-cloud-service-issues"></a>Rozwiązywanie problemów dotyczących usługi w chmurze Azure
Jeśli wystąpią problemy z projektami usługi chmury, takich jak rolę, która pobiera zablokowane w stanie "zajęty" wielokrotnie odtwarzana lub zgłasza wyjątek, to wewnętrzny błąd serwera, narzędzi i technik, można użyć toodiagnose i rozwiązać te problemy. Przykładem typowe problemy i rozwiązania, a także omówienie pojęć hello i narzędzia używane toodiagnose i takie błędy, zobacz [dane diagnostyczne obliczeniowe PaaS Azure](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

## <a name="q--a"></a>Pytania i odpowiedzi
**Co to jest rozmiar buforu hello i rozmiar, jaki ma być?**

W każdym wystąpieniu maszyny wirtualnej przydziały ograniczyć ilość danych diagnostycznych mogą być przechowywane na powitania lokalnego systemu plików. Ponadto można określić rozmiar buforu dla każdego typu danych diagnostycznych, która jest dostępna. Ten rozmiar buforu działa jak poszczególnych przydziału dla tego typu danych. Sprawdzając hello dołu okna dialogowego hello, można określić hello całkowitej ilości i hello ilość pamięci, które pozostają zachowane. Jeśli określisz buforów większy lub więcej typów danych będzie podejścia hello całkowitej ilości. Możesz zmienić hello całkowitej ilości, modyfikując plik konfiguracji diagnostics.wadcfg/.wadcfgx hello. Diagnostyka Hello dane są przechowywane na hello tego samego systemu plików jako dane aplikacji, więc jeśli aplikacja używa dużej ilości miejsca na dysku, nie należy zwiększyć hello całkowitej ilości diagnostyki.

**Co to jest okres transfer hello i jak długo ma być?**

okres transfer Hello jest hello ilość czasu, który przechwytuje upłynie między danymi. Po zaakceptowaniu transfer przeniesienia danych z lokalnego systemu plików hello na tootables maszyny wirtualnej, na Twoim koncie magazynu. Jeśli hello ilość zbieranych danych przekracza przydział hello przed hello koniec okresu transferu, starsze dane zostaną odrzucone. Jeśli w przypadku utraty danych, ponieważ danych przekracza rozmiar buforu hello lub hello całkowitej ilości można toodecrease hello transfer okresu.

**Strefy czasowej są hello sygnatury czasowe w?**

sygnatury czasowe Hello są hello lokalnej strefy czasowej hello centrum danych, który jest hostem usługi w chmurze. Witaj następujące trzy kolumny znaczników czasu w tabelach dziennika hello są używane.

* **PreciseTimeStamp** jest sygnatura czasowa ETW hello hello zdarzenia. Oznacza to hello czasu hello zdarzenie jest rejestrowane z powitania klienta.
* **Sygnatura CZASOWA** jest PreciseTimeStamp zaokrąglana toohello przekazywania częstotliwość granic. Tak Jeśli częstotliwość przekazywania jest 5 minut i zdarzenia hello czas 00:17:12, sygnatura CZASOWA będzie 00:15:00.
* **Sygnatura czasowa** jest sygnatura czasowa hello, w których hello w hello tabeli platformy Azure została utworzona jednostka.

**Jak zarządzać kosztami, podczas zbierania informacji diagnostycznych?**

Hello ustawienia domyślne (**poziom dziennika** ustawić także**błąd** i **okres transferu** ustawić także**1 minutę**) są zaprojektowane toominimize kosztów. Razie zbieranie większej ilości danych lub Zmniejsz okres transfer hello zwiększy koszty obliczeń. Nie należy zbierać więcej danych niż wymagane i nie zapomnij toodisable zbierania danych, gdy nie są już potrzebne. Należy zawsze włączyć ją ponownie, nawet w czasie wykonywania, jak pokazano w poprzedniej sekcji hello.

**Jak zebrać dzienniki nie powiodło się żądanie za pomocą programu IIS?**

Domyślnie usługi IIS nie zbierania dzienników żądanie nie powiodło się. Można skonfigurować usługi IIS toocollect hello je po zmodyfikowaniu pliku web.config dla roli sieci web.

**Nie są zwracane informacje o śledzeniu z metody RoleEntryPoint, takie jak OnStart. Co jest nie tak?**

metody Hello RoleEntryPoint są nazywane w kontekście hello WAIISHost.exe, nie usług IIS. W związku z tym hello informacje o konfiguracji w pliku web.config, które normalnie nie mają zastosowanie umożliwia śledzenie. tooresolve ten problem, Dodaj projekt roli sieci web tooyour pliku .config, a nazwa hello pliku toomatch hello zestawu wyjściowego zawierający kod RoleEntryPoint hello. W projektu roli sieć web domyślne hello hello nazwę pliku .config hello jest WAIISHost.exe.config. Następnie dodaj poniższe wiersze toothis plik hello:

```
<system.diagnostics>
  <trace>
      <listeners>
          <add name “AzureDiagnostics” type=”Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener”>
              <filter type=”” />
          </add>
      </listeners>
  </trace>
</system.diagnostics>
```

Teraz, w hello **właściwości** okna, hello zestaw **skopiować tooOutput katalogu** właściwości zbyt**zawsze Kopiuj**.

## <a name="next-steps"></a>Następne kroki
Zobacz toolearn więcej informacji na temat rejestrowania na platformie Azure diagnostics [Włączanie diagnostyki w usług Azure Cloud Services i maszyn wirtualnych](cloud-services/cloud-services-dotnet-diagnostics.md) i [Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md).

