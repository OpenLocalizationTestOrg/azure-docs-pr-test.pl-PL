---
title: "Konfigurowanie diagnostyki dla usług w chmurze Azure i maszyn wirtualnych | Dokumentacja firmy Microsoft"
description: "Zawiera opis sposobu konfigurowania informacje diagnostyczne dla debugowania Azure cloude usług i maszyn wirtualnych (VM) w programie Visual Studio."
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
ms.openlocfilehash: 2516c0eb8ce470577731db9b844d5b9038465477
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-diagnostics-for-azure-cloud-services-and-virtual-machines"></a>Konfigurowanie diagnostyki dla usług w chmurze Azure i maszyny wirtualne
Jeśli potrzebne jest rozwiązywanie problemów z usługą w chmurze platformy Azure lub maszyny wirtualnej platformy Azure, Diagnostyka Azure można skonfigurować łatwiej przy użyciu programu Visual Studio. Diagnostyka Azure powoduje przechwycenie danych systemowych i rejestrowanie danych na maszynach wirtualnych i wystąpień maszyn wirtualnych, które są uruchamiane usługi w chmurze i przesyła dane do wybranego konta magazynu. Zobacz [Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md) Aby uzyskać więcej informacji o diagnostyce rejestrowania na platformie Azure.

W tym temacie przedstawiono sposób włączania i konfigurowania diagnostyki Azure w programie Visual Studio, przed i po wdrożeniu, a także na maszynach wirtualnych platformy Azure. On również przedstawiono sposób wybierz typy informacje diagnostyczne do zbierania i wyświetlić informacje po ich zebraniu.

Diagnostyka Azure można skonfigurować w następujący sposób:

* Możesz zmienić ustawienia konfiguracji diagnostyki za pomocą **konfiguracji diagnostyki** okno dialogowe w programie Visual Studio. Ustawienia są zapisywane w pliku o nazwie diagnostics.wadcfgx (diagnostics.wadcfg Azure SDK 2.4 lub wcześniej). Alternatywnie można bezpośrednio modyfikować pliku konfiguracji. Jeśli ręcznie zaktualizować plik, zmiany w konfiguracji zacznie obowiązywać następnego czas wdrażania chmury usługa Azure lub uruchomienia w emulatorze usługi.
* Użyj **Eksplorator chmury** lub **Eksploratora serwera** w programie Visual Studio, aby zmienić ustawienia diagnostyki dla maszyny wirtualnej lub uruchomiona usługa w chmurze.

## <a name="azure-26-diagnostics-changes"></a>Zmiany diagnostyki Azure 2.6
Azure SDK w wersji 2.6 projektów programu Visual Studio wprowadzono następujące zmiany. (Te zmiany również dotyczyć nowsze wersje zestawu SDK platformy Azure.)

* Lokalne emulatora obsługuje teraz diagnostyki. Oznacza to, można zbierać dane diagnostyczne i upewnij się, że aplikacja tworzy prawo śladów podczas tworzenia i testowania w programie Visual Studio. Parametry połączenia `UseDevelopmentStorage=true` umożliwia zbieranie danych diagnostycznych, gdy używasz projekt usługi w chmurze w programie Visual Studio przy użyciu emulatora magazynu Azure. Wszystkie dane diagnostyczne są zbierane w ramach konta magazynu (Programowanie magazynu).
* Parametry połączenia konta magazynu diagnostyki (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) znajduje się jeszcze raz w pliku konfiguracji (cscfg) usługi. W systemie Azure SDK 2.5 konto magazynu diagnostyki została określona w pliku diagnostics.wadcfgx.

Istnieją pewne ważne różnice między jak parametry połączenia działał w 2.4 zestawu SDK platformy Azure i starszych i jak działa w Azure SDK w wersji 2.6 lub nowszej.

* W 2.4 zestawu SDK platformy Azure i starszych parametry połączenia została użyta jako środowisko uruchomieniowe dodatek diagnostyki można pobrać informacji o koncie magazynu przesyłania dzienników diagnostycznych.
* W Azure SDK w wersji 2.6 lub nowszej ciąg połączenia diagnostyki jest używany przez program Visual Studio Aby skonfigurować rozszerzenie diagnostyki magazynu odpowiednie informacje o koncie podczas publikowania. Parametry połączenia umożliwia definiowanie różnych kont magazynu dla konfiguracji innej usługi, które Visual Studio będzie korzystać w przypadku publikowania. Jednak ponieważ wtyczki Diagnostyka nie jest już dostępny (po 2.5 zestawu SDK platformy Azure), plik .cscfg samodzielnie nie można włączyć rozszerzenia diagnostyki. Należy włączyć rozszerzenie z osobna za pomocą narzędzi, takich jak Visual Studio lub programu PowerShell.
* Aby uprościć proces konfigurowania rozszerzenia diagnostyki przy użyciu programu PowerShell, dane wyjściowe pakietu z programu Visual Studio zawiera publicznej konfiguracji XML dla rozszerzenia diagnostyki dla każdej roli. Visual Studio będzie korzystać diagnostyki parametry połączenia do wypełniania informacji o koncie magazynu, które są obecne w publicznej konfiguracji. Pliki konfiguracji publicznego są tworzone w folderze rozszerzenia i postępuj zgodnie ze wzorcem PaaSDiagnostics. &lt;RoleName >. PubConfig.xml. Wszystkie wdrożenia na podstawie programu PowerShell można użyć tego wzorca do mapowania każdej konfiguracji do roli.
* Parametry połączenia w pliku .cscfg jest już używana przez [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) dostępu do danych diagnostycznych, więc może występować w **monitorowanie** kartę. Ciąg połączenia jest potrzebne do skonfigurowania usługi, aby wyświetlić pełne dane monitorowania w portalu.

## <a name="migrating-projects-to-azure-sdk-26-and-later"></a>Migrowanie projektów Azure SDK w wersji 2.6 lub nowszego
Podczas migracji z 2.5 zestawu SDK platformy Azure do usługi Azure SDK w wersji 2.6 lub nowszej, jeśli masz konto magazynu diagnostyki określone w pliku .wadcfgx, następnie pozostanie on istnieje. Aby móc korzystać z elastyczność przy użyciu różnych kont magazynu dla konfiguracji innego magazynu, musisz ręcznie dodać parametry połączenia do projektu. W przypadku migrowania projektu z Azure SDK 2.4 lub jego starszej wersji 2.6 zestawu SDK platformy Azure, Diagnostyka parametry połączenia zostaną zachowane. Pamiętaj jednak zmiany w sposób parametry połączenia są traktowane w Azure SDK w wersji 2.6 określone w poprzedniej sekcji.

### <a name="how-visual-studio-determines-the-diagnostics-storage-account"></a>Jak Visual Studio Określa konto magazynu diagnostyki
* Jeśli parametry połączenia diagnostyki jest określone w pliku .cscfg, Visual Studio używa go do konfigurowania rozszerzenia diagnostyki podczas publikowania i podczas generowania publicznej konfiguracji plików xml podczas pakowania.
* Jeśli ciąg połączenia diagnostyki nie została określona w pliku .cscfg, następnie Visual Studio powraca do przy użyciu konta magazynu określony w pliku .wadcfgx, aby skonfigurować rozszerzenie diagnostyki podczas publikowania i generowanie publicznej konfiguracji plików xml Podczas tworzenia pakietu.
* Diagnostyka parametry połączenia w pliku .cscfg mają pierwszeństwo przed konta magazynu w pliku .wadcfgx. Jeśli parametry połączenia diagnostyki jest określone w pliku .cscfg, Visual Studio użyty i ignoruje konta magazynu w .wadcfgx.

### <a name="what-does-the-update-development-storage-connection-strings-checkbox-do"></a>Co to jest "Aktualizacja programowanie magazynu ciągów połączenia..." czy pole wyboru?
Pole wyboru **zaktualizować parametry połączenia magazynu programowanie dla diagnostyki i buforowanie z poświadczeniami konta magazynu Microsoft Azure podczas publikowania do systemu Microsoft Azure** udostępnia wygodny sposób zaktualizować rozwojem Parametry połączenia konta magazynu z kontem magazynu systemu Azure podczas publikowania określono.

Załóżmy na przykład, zaznacz to pole wyboru i określa parametry połączenia diagnostyki `UseDevelopmentStorage=true`. Podczas publikowania projektu na platformie Azure, programu Visual Studio automatycznie zaktualizuje diagnostyki parametry połączenia z kontem magazynu określone w Kreatorze publikowania. Jednak jeśli konto magazynu rzeczywista określono jako parametry połączenia diagnostyki, następnie to konto jest używana zamiast tego.

## <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Diagnostyka funkcji różnice między 2.4 zestawu SDK platformy Azure i wcześniej i Azure SDK, 2.5 lub nowszej
Jeśli uaktualniasz projektu z 2.4 zestawu SDK platformy Azure, Azure SDK 2.5 lub nowszej, musisz należy pamiętać następujące różnice funkcji diagnostyki.

* **Konfiguracyjne interfejsy API są przestarzałe** — trybu diagnostyki jest dostępna w 2.4 zestawu SDK platformy Azure i jego wcześniejsze wersje, ale jest przestarzała w wersji 2.5 zestawu SDK platformy Azure i nowszych. Jeśli konfiguracji diagnostyki jest obecnie zdefiniowane w kodzie, należy ponownie skonfigurować te ustawienia od podstaw w projekcie migrowane w kolejności diagnostyki, aby kontynuować pracę. Plik konfiguracji diagnostyki Azure SDK 2.4 jest diagnostics.wadcfg i diagnostics.wadcfgx dla 2.5 zestawu SDK platformy Azure i nowszych.
* **Diagnostyki dla aplikacji usługi w chmurze można skonfigurować tylko na poziomie roli, nie na poziomie wystąpienia.**
* **Za każdym razem, gdy wdrażanie aplikacji, zaktualizowano konfigurację diagnostyki** — może to powodować problemy z parzystością, jeśli zmiana konfiguracji diagnostyki z Eksploratora serwera, a następnie ponowne wdrożenie aplikacji.
* **W wersji 2.5 zestawu SDK platformy Azure i nowszych, zrzuty awaryjne są konfigurowane w pliku konfiguracji diagnostyki nie w kodzie** — Jeśli masz zrzuty awaryjne skonfigurowane w kodzie, musisz ręcznie przenieść konfiguracji z kodu do pliku konfiguracji, ponieważ zrzuty awaryjne nie są przenoszone podczas migracji do 2.6 zestawu SDK platformy Azure.

## <a name="enable-diagnostics-in-cloud-service-projects-before-deploying-them"></a>Włącz diagnostykę w projekty usługi w chmurze przed ich wdrożeniem
W programie Visual Studio można zbierać dane diagnostyczne dla ról, które działają na platformie Azure, podczas uruchamiania usługi w emulatorze przed jego wdrożeniem. Wszelkie zmiany wprowadzone w ustawieniach diagnostyki w programie Visual Studio są zapisywane w pliku konfiguracyjnym diagnostics.wadcfgx. Te ustawienia konfiguracji Określ konto magazynu, w której jest zapisywany dane diagnostyczne, podczas wdrażania usługi w chmurze.

[!INCLUDE [cloud-services-wad-warning](../includes/cloud-services-wad-warning.md)]

### <a name="to-enable-diagnostics-in-visual-studio-before-deployment"></a>Aby włączyć diagnostyki w programie Visual Studio przed wdrożeniem
1. Menu skrótów dla roli interesującego, wybierz **właściwości**, a następnie wybierz pozycję **konfiguracji** kartę do roli **właściwości** okna.
2. W **diagnostyki** sekcji, upewnij się, że **włączyć diagnostyki** pole wyboru jest zaznaczone.
   
    ![Dostęp do opcji Włącz diagnostyki](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796660.png)
3. Wybierz przycisk wielokropka (...), aby określić miejsce przechowywania danych diagnostycznych konta magazynu. Wybrane konto magazynu będzie miejsce przechowywania danych diagnostycznych.
   
    ![Określ konto magazynu do użycia](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796661.png)
4. W **utworzyć parametry połączenia magazynu** oknie dialogowym Określ, czy chcesz się połączyć przy użyciu emulatora usługi Azure Storage, subskrypcji platformy Azure, lub ręcznie wprowadzić poświadczenia.
   
    ![Okno dialogowe konta magazynu](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796662.png)
   
   * Jeśli wybierzesz Microsoft opcja emulatora magazynu Azure, ciąg połączenia jest ustawiona na UseDevelopmentStorage = true.
   * Jeśli wybierzesz opcję Twojej subskrypcji, można wybrać subskrypcji platformy Azure, którego chcesz użyć, a nazwa konta. Można wybrać przycisk Zarządzaj kontami, aby zarządzać subskrypcjami platformy Azure.
   * Jeśli zostanie wybrana opcja wprowadzone ręcznie poświadczenia, wyświetlany jest monit o wprowadzenie nazwy i klucza konta Azure, którego chcesz użyć.
5. Wybierz **Konfiguruj** przycisk, aby wyświetlić **konfiguracji diagnostyki** okno dialogowe. Każda karta (z wyjątkiem **ogólne** i **katalogów dziennika**) reprezentuje źródło danych diagnostycznych, które można zebrać. Karta domyślne **ogólne**, udostępnia następujące opcje zbierania danych diagnostycznych: **tylko błędy**, **wszystkie informacje**, i **plan niestandardowy**. Opcja domyślna **tylko błędy**, ma co najmniej ilość miejsca w magazynie, ponieważ nie transferu, ostrzeżenia lub komunikaty śledzenia. Opcji wszystkie informacje przesyła większość informacji i dlatego, jest opcją najdroższych pod względem pamięci masowej.
   
    ![Włącz diagnostyki Azure i konfiguracji](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
6. Na przykład wybierz **plan niestandardowy** opcja tak dostosować dane zbierane.
7. **Przydział dysku w MB** pole określa ilość miejsca, które mają zostać przydzielone na koncie magazynu dla danych diagnostycznych. Można zmienić wartość domyślną, jeśli chcesz.
8. Na każdej karcie mają być zbierane dane diagnostyczne, wybierz jej **włączyć Transfer <log type>**  pole wyboru. Na przykład, jeśli chcesz zbierać Dzienniki aplikacji, wybierz opcję **włączyć transferu Dzienniki aplikacji** pole wyboru na **Dzienniki aplikacji** kartę. Ponadto określ wszelkie inne informacje wymagane przez każdego typu danych diagnostycznych. Zobacz sekcję **Konfigurowanie źródeł danych diagnostycznych** dalszej części tego tematu, aby uzyskać informacje o konfiguracji na poszczególnych kartach.
9. Po włączeniu zbierania danych diagnostycznych chcesz wybrać **OK** przycisku.
10. Uruchom projekt usługi chmury Azure w programie Visual Studio w zwykły sposób. Jak za pomocą aplikacji informacje dziennika, które są włączone jest zapisywany do wskazanego konta magazynu Azure.

## <a name="enable-diagnostics-in-azure-virtual-machines"></a>Włącz diagnostykę w maszynach wirtualnych platformy Azure
W programie Visual Studio można zbierać dane diagnostyczne maszyn wirtualnych platformy Azure.

### <a name="to-enable-diagnostics-in-azure-virtual-machines"></a>Aby włączyć diagnostyki w maszynach wirtualnych platformy Azure
1. W **Eksploratora serwera**, wybierz węzeł Azure i Połącz z subskrypcją platformy Azure, jeśli jeszcze nie zostało nawiązane.
2. Rozwiń węzeł **maszyn wirtualnych** węzła. Utwórz nową maszynę wirtualną lub wybierz jedną, która jest już istnieje.
3. W menu skrótów dla maszyny wirtualnej, interesującego wybierz **Konfiguruj**. Pokazuje to okno dialogowe konfiguracji maszyny wirtualnej.
   
    ![Konfigurowanie maszyny wirtualnej platformy Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796663.png)
4. Jeśli to nie jest jeszcze zainstalowana, Dodaj rozszerzenie Diagnostyka agenta monitorowania firmy Microsoft. To rozszerzenie umożliwia zbieranie danych diagnostycznych dla maszyny wirtualnej platformy Azure. Na liście zainstalowanych rozszerzeń wybierz wybierz z menu rozwijanego dostępne rozszerzenia, a następnie wybierz pozycję Diagnostyka agenta monitorowania firmy Microsoft.
   
    ![Instalowanie rozszerzenia maszyny wirtualnej platformy Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766024.png)
   
   > [!NOTE]
   > Inne rozszerzenia diagnostyki są dostępne dla maszyn wirtualnych. Aby uzyskać więcej informacji zobacz funkcje i rozszerzenia maszyny Wirtualnej Azure.
   > 
   > 
5. Wybierz **Dodaj** przycisk, aby dodać rozszerzenie i wyświetl jego **konfiguracji diagnostyki** okno dialogowe.
6. Wybierz **Konfiguruj** przycisk, aby określić konto magazynu, a następnie wybierz pozycję **OK** przycisku.
   
    Każda karta (z wyjątkiem **ogólne** i **katalogów dziennika**) reprezentuje źródło danych diagnostycznych, które można zebrać.
   
    ![Włącz diagnostyki Azure i konfiguracji](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
   
    Karta domyślne **ogólne**, udostępnia następujące opcje zbierania danych diagnostycznych: **tylko błędy**, **wszystkie informacje**, i **plan niestandardowy**. Opcja domyślna **tylko błędy**, ma co najmniej ilość miejsca w magazynie, ponieważ nie transferu, ostrzeżenia lub komunikaty śledzenia. **Wszystkie informacje** opcja przekazuje informacje najbardziej i w związku z tym jest opcją najdroższych pod względem pamięci masowej.
7. Na przykład wybierz **plan niestandardowy** opcja tak dostosować dane zbierane.
8. **Przydział dysku w MB** pole określa ilość miejsca, które mają zostać przydzielone na koncie magazynu dla danych diagnostycznych. Można zmienić wartość domyślną, jeśli chcesz.
9. Na każdej karcie mają być zbierane dane diagnostyczne, wybierz jej **włączyć Transfer <log type>**  pole wyboru.
   
    Na przykład, jeśli chcesz zbierać Dzienniki aplikacji, wybierz opcję **włączyć transferu Dzienniki aplikacji** pole wyboru na **Dzienniki aplikacji** kartę. Ponadto określ wszelkie inne informacje wymagane przez każdego typu danych diagnostycznych. Zobacz sekcję **Konfigurowanie źródeł danych diagnostycznych** dalszej części tego tematu, aby uzyskać informacje o konfiguracji na poszczególnych kartach.
10. Po włączeniu zbierania danych diagnostycznych chcesz wybrać **OK** przycisku.
11. Zapisz zaktualizowany projekt.
    
     Zostanie wyświetlony komunikat w **dziennik aktywności programu Microsoft Azure** okna o zaktualizowaniu maszyny wirtualnej.

## <a name="configure-diagnostics-data-sources"></a>Konfigurowanie źródeł danych diagnostycznych
Po włączeniu funkcji zbierania danych diagnostycznych, można wybrać dokładnie źródeł danych, które chcesz zebrać i jakie informacje są zbierane. Poniżej znajduje się lista kart w **konfiguracji diagnostyki** okno dialogowe i oznacza każdej opcji konfiguracji.

### <a name="application-logs"></a>Dzienniki aplikacji
**Dzienniki aplikacji** zawierają informacje diagnostyczne produkowane przez aplikację sieci web. Jeśli chcesz przechwycić Dzienniki aplikacji, wybierz **włączyć transferu Dzienniki aplikacji** pole wyboru. Można zwiększyć lub zmniejszyć liczbę minut, jeśli dzienniki aplikacji są przenoszone do konta magazynu, zmieniając **transferu okres (min)** wartość. Można również zmienić ilość informacji przechwycone w dzienniku, ustawiając wartość poziomu dziennika. Na przykład można wybrać **pełne** Aby uzyskać więcej informacji, lub wybierz **krytyczny** do przechwytywania tylko błędy krytyczne. Jeśli masz diagnostyczne zależne od dostawcy, który emituje Dzienniki aplikacji, można przechwycić je przez dodanie identyfikator GUID dostawcy, aby **GUID dostawcy** pole.

  ![Dzienniki aplikacji](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758145.png)

  Zobacz [Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md) Aby uzyskać więcej informacji o dziennikach aplikacji.

### <a name="windows-event-logs"></a>Dzienniki zdarzeń systemu Windows
Aby przechwycić dzienniki zdarzeń systemu Windows, zaznacz **włączyć transferu dzienniki zdarzeń systemu Windows** pole wyboru. Można zwiększyć lub zmniejszyć liczbę minut, jeśli dzienniki zdarzeń są przenoszone do konta magazynu, zmieniając **transferu okres (min)** wartość. Zaznacz pola wyboru dla typów zdarzeń, które mają być śledzone.

  ![Dzienniki zdarzeń](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796664.png)

Jeśli używasz Azure SDK Version 2.6 lub nowszej, a aby określić niestandardowe źródło danych, wprowadź go w  **<Data source name>**  tekst pola, a następnie wybierz pozycję **Dodaj** przycisk obok niej. Źródło danych jest dodawane do pliku diagnostics.cfcfg.

Jeśli używasz 2.5 zestawu SDK platformy Azure i chcesz określić niestandardowe źródło danych, należy dodać go do `WindowsEventLog` sekcji diagnostics.wadcfgx plików, takie jak w poniższym przykładzie.

```
<WindowsEventLog scheduledTransferPeriod="PT1M">
   <DataSource name="Application!*" />
   <DataSource name="CustomDataSource!*" />
</WindowsEventLog>
```
### <a name="performance-counters"></a>Liczniki wydajności
Informacje o liczniku wydajności może pomóc w Znajdź wąskich gardeł systemu i poprawienia wydajności systemu i aplikacji. Zobacz [tworzenie i Użyj liczników wydajności w aplikacji Azure](https://msdn.microsoft.com/library/azure/hh411542.aspx) Aby uzyskać więcej informacji. Aby przechwycić liczniki wydajności, zaznacz **włączyć transferu liczniki wydajności** pole wyboru. Można zwiększyć lub zmniejszyć liczbę minut, jeśli dzienniki zdarzeń są przenoszone do konta magazynu, zmieniając **transferu okres (min)** wartość. Zaznacz pola wyboru dla liczników wydajności, które mają być śledzone.

  ![Liczniki wydajności](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758147.png)

Aby śledzić licznika wydajności, które nie ma na liście, wprowadź go przy użyciu składni sugerowane, a następnie wybierz pozycję **Dodaj** przycisku. System operacyjny na maszynie wirtualnej Określa, które liczniki wydajności można śledzić. Aby uzyskać więcej informacji na temat składni, zobacz [określania ścieżki licznika](https://msdn.microsoft.com/library/windows/desktop/aa373193.aspx).

### <a name="infrastructure-logs"></a>Dzienniki infrastruktury
Jeśli chcesz przechwycić dzienniki infrastruktury, które zawierają informacje dotyczące infrastruktury diagnostycznych platformy Azure, wybierz moduł RemoteAccess i RemoteForwarder moduł, **włączyć transferu dzienniki infrastruktury** Sprawdź pole. Można zwiększyć lub zmniejszyć liczbę minut, gdy są przekazywane dzienniki na koncie magazynu, zmieniając wartość okresu Transfer (min).

  ![Dzienniki infrastruktury diagnostyki](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758148.png)

  Zobacz [zbierania danych rejestrowania za pomocą diagnostyki Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx) Aby uzyskać więcej informacji.

### <a name="log-directories"></a>Katalogi dziennika
Aby przechwycić katalogi dziennika, które zawierają dane zbierane z katalogów dziennika dla żądań usług Internet Information Services (IIS), wybierz żądań zakończonych niepowodzeniem lub foldery, które można wybrać **włączyć transferu katalogów dziennika** pole wyboru. Można zwiększyć lub zmniejszyć liczbę minut, gdy są przekazywane dzienniki na koncie magazynu, zmieniając **transferu okres (min)** wartość.

Można wybrać pola dzienników, które chcesz zebrać, takich jak **dzienniki programu IIS** i **nie powiodło się żądanie** dzienniki. Domyślne nazwy kontenera magazynu jest dostępny, ale można zmienić nazwy, jeśli chcesz.

Ponadto można przechwycić dzienniki z dowolnego folderu. Po prostu określić ścieżkę w **dziennika z katalogu bezwzględną** sekcji, a następnie wybierz pozycję **Dodaj katalog** przycisku. Dzienniki będą przechwytywane do określonego kontenerów.

  ![Katalogi dziennika](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796665.png)

### <a name="etw-logs"></a>Dzienniki zdarzeń systemu Windows
Jeśli używasz [śledzenia zdarzeń dla systemu Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx) (ETW) i aby przechwytywać dzienniki zdarzeń systemu Windows, zaznacz **włączyć transferu dzienniki zdarzeń systemu Windows** pole wyboru. Można zwiększyć lub zmniejszyć liczbę minut, gdy są przekazywane dzienniki na koncie magazynu, zmieniając **transferu okres (min)** wartość.

Zdarzenia są przechwytywane ze źródła zdarzeń i manifesty zdarzeń, które określisz. Aby określić źródło zdarzenia, wprowadź nazwę w **źródła zdarzeń** sekcji, a następnie wybierz pozycję **Dodaj źródło zdarzeń** przycisku. Analogicznie, można określić manifest zdarzeń w **manifesty zdarzeń** sekcji, a następnie wybierz pozycję **Dodaj Manifest zdarzeń** przycisku.

  ![Dzienniki zdarzeń systemu Windows](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766025.png)

  ETW framework jest obsługiwana w programie ASP.NET za pośrednictwem klas w [System.Diagnostics.aspx] (przestrzeń nazw https://msdn.microsoft.com/library/system.diagnostics (v=vs.110). Przestrzeń nazw Microsoft.WindowsAzure.Diagnostics, która dziedziczy i rozszerza standard [System.Diagnostics.aspx] (https://msdn.microsoft.com/library/system.diagnostics (v=vs.110) klas, umożliwia użycie protokołu https ([System.Diagnostics.aspx] : //msdn.microsoft.com/library/system.diagnostics(v=vs.110) jako struktury rejestrowania, w środowisku platformy Azure. Aby uzyskać więcej informacji, zobacz [zająć kontroli z rejestrowania i śledzenia w systemie Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) i [Włączanie diagnostyki w usług Azure Cloud Services i maszyn wirtualnych](cloud-services/cloud-services-dotnet-diagnostics.md).

### <a name="crash-dumps"></a>Zrzuty awaryjne
Jeśli chcesz przechwycić informacje o po wystąpienia roli ulegnie awarii, wybierz **włączyć przesyłanie awarii zrzuty** pole wyboru. (Ponieważ ASP.NET obsługuje większość wyjątki, jest zazwyczaj przydatne tylko w przypadku roli proces roboczy). Można zwiększyć lub zmniejszyć wartości procentowej miejsca do magazynowania poświęcone zrzuty awaryjne, zmieniając **przydziału katalogu (%)** wartość. Można zmienić kontener magazynu, w którym zrzuty awaryjne są przechowywane i można wybrać, czy mają być przechwytywane **pełne** lub **Mini** zrzutu.

Procesy aktualnie śledzone są wyświetlane. Zaznacz pola wyboru dla procesów, które mają być przechwytywane. Aby dodać inny proces na liście, wprowadź nazwę procesu, a następnie wybierz pozycję **proces dodawania** przycisku.

  ![Zrzuty awaryjne](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766026.png)

  Zobacz [zająć kontroli z rejestrowania i śledzenia w systemie Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) i [Microsoft Azure Diagnostics część 4: składniki Rejestrowanie niestandardowe i zmiany 1.3 diagnostyki Azure](http://justazure.com/microsoft-azure-diagnostics-part-4-custom-logging-components-azure-diagnostics-1-3-changes/) Aby uzyskać więcej informacji.

## <a name="view-the-diagnostics-data"></a>Widok danych diagnostycznych
Po zostały zebrane dane diagnostyczne do usługi w chmurze lub maszynę wirtualną, możesz je wyświetlić.

### <a name="to-view-cloud-service-diagnostics-data"></a>Aby wyświetlić dane diagnostyczne usługi w chmurze
1. Wdrażanie usługi w chmurze w zwykły sposób, a następnie uruchom go.
2. Dane diagnostyczne można wyświetlić raportu, który generuje Visual Studio lub tabel na koncie magazynu. Aby wyświetlić dane w raporcie, otwórz **Eksplorator chmury** lub **Eksploratora serwera**, otwórz menu skrótów węzła interesującego roli, a następnie wybierz **widoku danych diagnostycznych**.
   
    ![Widok danych diagnostycznych](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748912.png)
   
    Zostanie wyświetlony raport pokazujący dostępne dane.
   
    ![Raport diagnostyczny platformy Microsoft Azure w programie Visual Studio](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796666.png)
   
    Jeśli nie ma najnowszych danych, może być konieczne poczekaj, aż okres transfer może upłynąć.
   
    Wybierz **Odśwież** łącze, aby natychmiast zaktualizować dane lub wybierz interwał w **automatycznego odświeżania** lista rozwijana dane aktualizowane automatycznie. Aby wyeksportować błąd danych, wybierz **Eksportuj do pliku CSV** przycisk, aby utworzyć plik wartości rozdzielanych przecinkami, można otworzyć w arkuszu kalkulacyjnym.
   
    W **Eksplorator chmury** lub **Eksploratora serwera**, otwórz konta magazynu, który został skojarzony z wdrożenia.
3. Otwórz w tabelach diagnostyki w podglądzie tabeli, a następnie przejrzyj zebranych danych. Dzienniki programu IIS i dzienników niestandardowych można otworzyć kontenera obiektów blob. Zostały podane w poniższej tabeli, można znaleźć tabeli lub obiektu blob kontenera, który zawiera interesujący Cię dane. Oprócz danych dla tego pliku dziennika, wpisy tabeli zawierają EventTickCount, DeploymentId roli i RoleInstance do określania, jakie maszyny wirtualnej i roli wygenerowanych danych i kiedy. 
   
   | Dane diagnostyczne | Opis | Lokalizacja |
   | --- | --- | --- |
   | Dzienniki aplikacji |Dzienniki generowane przez wywołanie metody klasy System.Diagnostics.Trace kodu. |WADLogsTable |
   | Dzienniki zdarzeń |Te dane są z dzienników zdarzeń systemu Windows na maszynach wirtualnych. System Windows przechowuje informacje w tych dziennikach, ale aplikacje i usługi również umożliwia raportowanie błędów lub rejestrowania informacji. |WADWindowsEventLogsTable |
   | Liczniki wydajności |Można zbierać dane w dowolnym licznika wydajności, które jest dostępne na maszynie wirtualnej. System operacyjny udostępnia liczników wydajności, które zawierają wiele statystyk, takich jak pamięć użycia i czasu procesora. |WADPerformanceCountersTable |
   | Dzienniki infrastruktury |Te dzienniki są generowane na podstawie samej infrastruktury diagnostyki. |WADDiagnosticInfrastructureLogsTable |
   | Dzienniki programu IIS |Te dzienniki rejestrowania żądań sieci web. Jeśli usługi w chmurze pobiera znaczną ilość ruchu, dzienniki te mogą być bardzo długie, dlatego należy zebrać i zapisane dane tej tylko wtedy, gdy zajdzie taka potrzeba. |Można znaleźć dzienniki żądanie nie powiodło się w kontenerze obiektów blob w obszarze wad iis failedreqlogs w ścieżce dla tego wdrożenia, roli i wystąpienia. Można znaleźć pełną dzienniki w obszarze logfiles-wad — usługi iis. Dla każdego pliku wpisów w tabeli WADDirectories. |
   | Zrzuty awaryjne |Informacje te stanowią binarny obraz procesu usługi chmury (zazwyczaj roli proces roboczy). |kontener obiektów blob wad zgniatania zrzutów |
   | Pliki dziennika niestandardowego |Dzienniki danych, który zostanie wstępnie zdefiniowane. |Można określić w kodzie lokalizację plików dziennika niestandardowe na koncie magazynu. Na przykład można określić kontenera niestandardowych obiektów blob. |
4. Jeśli zostały obcięte danych dowolnego typu, możesz zwiększyć bufor dla danych typu lub skrócić interwał między transferów danych z maszyny wirtualnej do konta magazynu.
5. (opcjonalnie) Przeczyść dane z konta magazynu od czasu do czasu na obniżenie ogólnych kosztów magazynowania.
6. Po wykonaniu pełne wdrożenie plik diagnostics.cscfg (.wadcfgx dla 2.5 zestawu SDK platformy Azure) został zaktualizowany na platformie Azure i usługi w chmurze przejmuje wszystkie zmiany w konfiguracji diagnostyki. Jeśli, należy zaktualizować istniejące wdrożenie, pliku nie zostały zaktualizowane na platformie Azure. Ustawienia diagnostyki, można zmienić, wykonując kroki opisane w następnej sekcji. Aby uzyskać więcej informacji na temat wykonywania pełne wdrożenie i aktualizowania istniejącego wdrożenia, zobacz [Kreator publikowania aplikacji Azure](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="to-view-virtual-machine-diagnostics-data"></a>Aby wyświetlić dane diagnostyczne maszyny wirtualnej
1. Menu skrótów dla maszyny wirtualnej, wybierz **dane diagnostyczne widoku**.
   
    ![Widok danych diagnostycznych w maszynie wirtualnej platformy Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766027.png)
   
    Spowoduje to otwarcie **podsumowanie diagnostyki** okna.
   
    ![Podsumowanie diagnostyki maszyny wirtualnej platformy Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796667.png)  
   
    Jeśli nie ma najnowszych danych, może być konieczne poczekaj, aż okres transfer może upłynąć.
   
    Wybierz **Odśwież** łącze, aby natychmiast zaktualizować dane lub wybierz interwał w **automatycznego odświeżania** lista rozwijana dane aktualizowane automatycznie. Aby wyeksportować błąd danych, wybierz **Eksportuj do pliku CSV** przycisk, aby utworzyć plik wartości rozdzielanych przecinkami, można otworzyć w arkuszu kalkulacyjnym.

## <a name="configure-cloud-service-diagnostics-after-deployment"></a>Skonfigurować diagnostykę usługi w chmurze po wdrożeniu
Jeśli w przypadku badania problemu z chmurą usługa tego już uruchomiona, należy zbierać dane, których nie podano zanim pierwotnie wdrożyć rolę. W takim przypadku można zacząć zbierać dane przy użyciu ustawień w Eksploratorze serwera. Możesz skonfigurować diagnostykę dla jednego wystąpienia lub wszystkich wystąpień w roli, w zależności od tego, czy otworzyć okno dialogowe konfiguracji diagnostyki w menu skrótów, czy wystąpienie roli. Jeśli konfigurujesz węzła roli, wszelkie zmiany dotyczą wszystkich wystąpień. Jeśli skonfigurujesz węzła wystąpienia zmiany dotyczą tylko tego wystąpienia.

### <a name="to-configure-diagnostics-for-a-running-cloud-service"></a>Aby skonfigurować diagnostykę dla uruchomionej usługi w chmurze
1. W Eksploratorze serwera rozwiń **usługi w chmurze** węzeł, a następnie rozwiń węzły można zlokalizować roli lub wystąpienie, które chcesz zbadać lub oba.
   
    ![Konfigurowanie diagnostyki](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748913.png)
2. W menu skrótów węzła wystąpienia lub węzłem roli wybierz **ustawień diagnostycznych aktualizacji**, a następnie wybierz pozycję Ustawienia diagnostyki, które mają być zbierane.
   
    Aby uzyskać informacje o ustawieniach konfiguracji, zobacz **Konfigurowanie źródeł danych diagnostycznych** w tym temacie. Aby uzyskać informacje o sposobie wyświetlania danych diagnostycznych, zobacz **wyświetlić dane diagnostyczne** w tym temacie.
   
    Jeśli zmienisz zbierania danych w **Eksploratora serwera**, te zmiany pozostaną aktywne do czasu ponownego wdrażania pełni usługi w chmurze. Jeśli użytkownik korzysta z domyślnych ustawień publikowania, zmiany nie zostaną zastąpione, ponieważ publikowania domyślne ustawienie służy do istniejącego wdrożenia aktualizacji, a nie czy pełnego ponownego wdrażania. Aby wyczyścić ustawienia w czasie wdrażania, przejdź do **Zaawansowane ustawienia** w Kreatorze publikowania i usuń zaznaczenie **aktualizację wdrożenia** wyboru. Podczas ponownego wdrażania z wyczyszczone pole wyboru, przywrócić ustawienia określone w pliku .wadcfgx (lub .wadcfg) zestawu za pomocą edytora właściwości roli. Po zaktualizowaniu wdrożenia usługi Azure śledzi stare ustawienia.

## <a name="troubleshoot-azure-cloud-service-issues"></a>Rozwiązywanie problemów dotyczących usługi w chmurze Azure
Jeśli wystąpią problemy z projektami usługi chmury, takich jak rolę, która pobiera zablokowane w stanie "zajęty" wielokrotnie odtwarzana lub zgłasza wyjątek, to wewnętrzny błąd serwera, istnieją narzędzia i techniki, których można użyć, aby zdiagnozować i rozwiązać te problemy. Przykładem typowe problemy i rozwiązania, a także omówienie pojęć i narzędzi służących do zdiagnozowania i rozwiązania takie błędy, zobacz [dane diagnostyczne obliczeniowe PaaS Azure](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

## <a name="q--a"></a>Pytania i odpowiedzi
**Co to jest rozmiar buforu, a rozmiar, jaki ma być?**

W każdym wystąpieniu maszyny wirtualnej przydziały ograniczyć ilość danych diagnostycznych może być przechowywany w lokalnym systemie plików. Ponadto można określić rozmiar buforu dla każdego typu danych diagnostycznych, która jest dostępna. Ten rozmiar buforu działa jak poszczególnych przydziału dla tego typu danych. Sprawdzając dolnej części okna dialogowego, można określić całkowitej ilości i ilość pamięci, które pozostają zachowane. Jeśli określisz buforów większy lub więcej typów danych będzie osiągają całkowitej ilości. Ogólny limit przydziału można zmienić, modyfikując plik konfiguracji diagnostics.wadcfg/.wadcfgx. Dane diagnostyczne są przechowywane w tym samym systemie plików jako dane aplikacji, więc jeśli aplikacja używa dużej ilości miejsca na dysku, nie należy zwiększyć ogólną przydział diagnostyki.

**Co to jest okres transfer i jak długo ma być?**

Okres transfer to czas, który przechwytuje upłynie między danymi. Po zaakceptowaniu transferu danych jest przenoszona z lokalnego systemu plików na maszynę wirtualną do tabel na koncie magazynu. Jeśli ilość zbieranych danych przekroczy limit przydziału przed upływem okresu transferu, starsze dane zostaną odrzucone. Można zmniejszyć okres transferu, jeśli w przypadku utraty danych, ponieważ danych przekracza rozmiar buforu lub całkowitej ilości.

**Strefy czasowej są sygnatury czasowe w?**

Sygnatury czasowe znajdują się w lokalnej strefie czasowej centrum danych, który jest hostem usługi w chmurze. Są używane następujące trzy kolumny znaczników czasu w tabelach dziennika.

* **PreciseTimeStamp** jest to sygnatura czasowa ETW zdarzenia. Oznacza to, że czas zdarzenie jest rejestrowane przez klienta.
* **Sygnatura CZASOWA** jest PreciseTimeStamp zostać zaokrąglona w dół do granicy częstotliwości wysyłania. Więc jeśli częstotliwość przekazywania jest 5 minut i zdarzenia, czas 00:17:12, sygnatura CZASOWA będzie 00:15:00.
* **Sygnatura czasowa** jest to sygnatura czasowa, w którym została utworzona jednostka w tabeli platformy Azure.

**Jak zarządzać kosztami, podczas zbierania informacji diagnostycznych?**

Ustawienia domyślne (**poziom dziennika** ustawioną **błąd** i **okres transferu** ustawioną **1 minuta**) zostały zaprojektowane do minimum kosztów. Razie zbieranie większej ilości danych lub Zmniejsz okres transfer zwiększy koszty obliczeń. Nie należy zbierać więcej danych niż wymagane i nie zapomnij Wyłącz funkcję zbierania danych, gdy nie są już potrzebne. Należy zawsze włączyć ją ponownie, nawet w czasie wykonywania, jak pokazano w poprzedniej sekcji.

**Jak zebrać dzienniki nie powiodło się żądanie za pomocą programu IIS?**

Domyślnie usługi IIS nie zbierania dzienników żądanie nie powiodło się. Można skonfigurować usługi IIS do zbierania ich edycji pliku web.config dla roli sieci web.

**Nie są zwracane informacje o śledzeniu z metody RoleEntryPoint, takie jak OnStart. Co jest nie tak?**

Metody RoleEntryPoint są nazywane w kontekście WAIISHost.exe, nie usług IIS. W związku z tym informacje o konfiguracji w pliku web.config, które normalnie nie mają zastosowanie umożliwia śledzenie. Aby rozwiązać ten problem, Dodaj plik .config do projektu roli sieci web i nazwa pliku do dopasowania zestawu wyjściowego, który zawiera kod RoleEntryPoint. W domyślnej projektu roli sieć web nazwa pliku .config byłoby WAIISHost.exe.config. Następnie dodaj następujące wiersze do tego pliku:

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

Teraz, w **właściwości** ustaw **Kopiuj do katalogu wyjściowego** właściwości **skopiuj zawsze**.

## <a name="next-steps"></a>Następne kroki
Aby dowiedzieć się więcej o diagnostyce rejestrowania na platformie Azure, zobacz [Włączanie diagnostyki w usług Azure Cloud Services i maszyn wirtualnych](cloud-services/cloud-services-dotnet-diagnostics.md) i [Włączanie rejestrowania diagnostyki dla aplikacji sieci web w usłudze Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md).

