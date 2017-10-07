---
title: "aaaGet wprowadzenie do integracji dzienników Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall hello Azure Usługa integracji dziennika i integrowanie dzienników z magazynu Azure, dzienników inspekcji platformy Azure i alerty Centrum zabezpieczeń Azure."
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 53f67a7c-7e17-4c19-ac5c-a43fabff70e1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 07/26/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 26c19070d76ff73b1bdbd32ba77fb04978af387e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-with-azure-diagnostics-logging-and-windows-event-forwarding"></a>Integracja dzienników Azure z rejestrowania diagnostyki Azure i funkcji przekazywania zdarzeń systemu Windows
Integracja dziennika Azure (AzLog) umożliwia toointegrate nowych dzienników z zasobów platformy Azure do lokalnych systemów Security Information and Event Management (SIEM). Integracja ta ułatwia możliwe toohave pulpit nawigacyjny ujednoliconego zabezpieczeń dla wszystkich zasobów, lokalnymi lub w chmurze hello, dzięki czemu można zagregować skorelowania, analizowanie i alertów zdarzeń zabezpieczeń skojarzonych z aplikacjami.
>[!NOTE]
Aby uzyskać więcej informacji o integracji dziennika Azure, możesz przejrzeć hello [Omówienie integracji dziennika Azure](https://docs.microsoft.com/azure/security/security-azure-log-integration-overview).

Ten artykuł pomoże Ci rozpoczęcie pracy z integracji dziennika Azure koncentrujących się na instalację hello hello Azlog usługi i Integrowanie usługi hello Diagnostyka Azure. Hello Azure dziennika integracji usługi będą mogli toocollect informacji dziennika zdarzeń systemu Windows z hello kanału zdarzeń zabezpieczeń systemu Windows z maszyn wirtualnych wdrożonych w IaaS platformy Azure. To jest bardzo podobny zbyt "Funkcji przekazywania zdarzeń" który użyto lokalnymi.

>[!NOTE]
>dane wyjściowe hello toobring możliwości Hello integracji dzienników Azure w toohello SIEM są dostarczane przez hello SIEM się. Zobacz artykuł hello [integracji Azure dziennika integracji z lokalnymi system SIEM](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) Aby uzyskać więcej informacji.

toobe oczywiste - hello Usługa integracji dziennika Azure działa na komputerze fizycznym lub wirtualnym używa hello systemu Windows Server 2008 R2 lub nowszym systemu operacyjnego (Windows Server 2012 R2 lub Windows Server 2016 są preferowane).

komputer fizyczny Hello można uruchomić lokalnie (lub w witrynie dostawcy usług hostingowych). Jeśli usługa Azure dziennika integracji hello toorun na maszynie wirtualnej, że maszyna wirtualna może być znajdujących się lokalnie lub w chmurze publicznej, takich jak Microsoft Azure.

Hello fizycznego lub maszynę wirtualną działającą usługę Azure dziennika integracji hello wymaga toohello łączności sieciowej chmurze publicznej systemu Azure. Kroki opisane w tym artykule szczegółowo hello konfiguracji.

## <a name="prerequisites"></a>Wymagania wstępne
Co najmniej hello instalacja AzLog wymaga hello następujące elementy:
* **Subskrypcji platformy Azure**. Jeśli jej nie masz, możesz zarejestrować się w celu [utworzenia bezpłatnego konta](https://azure.microsoft.com/free/).
* A **konta magazynu** które mogą być używane do rejestrowania diagnostyki Windows Azure (możesz użyć konta magazynu wstępnie skonfigurowane lub Utwórz nową — zostanie przedstawiony sposób tooconfigure hello konta magazynu w dalszej części tego artykułu)
  >[!NOTE]
  W zależności od danego scenariusza konta magazynu nie może być wymagane. Dla hello Azure diagnostics scenariusz omówione w tym artykule, co jest potrzebne.
* **Dwa systemy**: komputerze, na którym działa usługa Azure dziennika integracji hello i na komputerze, który będzie monitorowany i jego informacje rejestrowania wysyłane toohello Azlog usługi maszyny.
   * Maszyny, którą chcesz toomonitor — jest to maszyny Wirtualnej z systemem jako [maszyny wirtualnej platformy Azure](../virtual-machines/virtual-machines-windows-overview.md)
   * Komputerze, na którym działa usługa integracji dzienników Azure hello; Ten komputer będzie zbierać wszystkie informacje dziennika hello później zostaną zaimportowane do rozwiązania SIEM.
    * Ten system może być lokalnie lub na platformie Microsoft Azure.  
    * Musi on uruchomiony x64 toobe wersji systemu Windows server 2008 R2 z dodatkiem SP1 lub nowszej i mają .NET 4.5.1 zainstalowane. Można określić wersji .NET hello instalowane przez następujący artykuł hello [porady: ustalić, które .NET Framework są zainstalowane wersje](https://msdn.microsoft.com/library/hh925568)  
    Musi mieć konto magazynu Azure toohello łączności używane na potrzeby rejestrowania diagnostyki Azure. Firma Microsoft udostępni instrukcje w dalszej części tego artykułu w sposób możesz potwierdzić połączeń

Do szybkiego pokaz hello procesu tworzenia maszyny wirtualnej przy użyciu portalu Azure hello Spójrz na powitania wideo poniżej.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Create-a-Virtual-Machine/player]



## <a name="deployment-considerations"></a>Zagadnienia dotyczące wdrażania
Podczas testowania integracji dziennika Azure, można użyć dowolnego systemu, który spełnia wymagania minimalne systemu operacyjnego hello. Jednak w przypadku hello środowiska produkcyjnego obciążenia może wymagać tooplan skalowania w górę lub w poziomie.

Można uruchomić wiele wystąpień usługi integracji dziennika Azure hello (jedno wystąpienie na maszynie fizycznej lub wirtualnej), jeśli wolumin zdarzeń jest duża. Ponadto użytkownik może równoważyć obciążenie konta magazynu diagnostyki Azure dla systemu Windows (WAD) i hello liczby wystąpień toohello tooprovide subskrypcji powinna być oparta na wydajność.
>[!NOTE]
W tej chwili nie mamy szczegółowe zalecenia dotyczące gdy tooscale limit wystąpień Azure dziennik maszyny integracji (tj. maszyny, które są uruchomione hello Azure dziennika integracji usługi) lub konta magazynu lub subskrypcji. Skalowanie decyzje powinny być oparte na Twojej uwagi wydajności w każdym z tych obszarów.

Masz również hello opcja tooscale się hello Azure dziennika integracji usługi toohelp zwiększenia wydajności. Hello następujące metryki wydajności mogą pomóc w części ustalanie rozmiarów maszyny hello, wybierz opcję Usługa integracji dzienników Azure hello toorun:
* Na maszynie procesor 8 (podstawowe) jedno wystąpienie Azlog Integrator może przetworzyć około 24 miliony zdarzeń na dzień (~1M/hour).

* Na komputerze 4-procesora (podstawowe) jedno wystąpienie Azlog Integrator może przetworzyć około 1,5 miliona zdarzeń na dzień (~62.5K/hour).

## <a name="install-azure-log-integration"></a>Zainstaluj integracji dzienników Azure
tooinstall integracji dziennika Azure należy toodownload hello [integracji dzienników Azure](https://www.microsoft.com/download/details.aspx?id=53324) pliku instalacyjnego. Wykonaj czynności procedury instalacji hello i określenie, czy tooMicrosoft informacje telemetryczne tooprovide.  

![Ekran instalacji z zaznaczonym polem telemetrii](./media/security-azure-log-integration-get-started/telemetry.png)

*
> [!NOTE]
> Firma Microsoft zaleca, Zezwalaj na dane telemetryczne toocollect firmy Microsoft. Zbieranie danych telemetrycznych można wyłączyć, usuwając zaznaczenie pola wyboru tej opcji.
>


Witaj Usługa integracji dziennika Azure zbiera dane telemetryczne z hello maszyny, na którym jest zainstalowany.  

Zbierane dane z telemetrii jest:

* Wyjątków występujących podczas wykonywania integracji dzienników Azure
* Metryki o liczbie hello zapytań i przetwarzania zdarzeń
* Statystyki, o które Azlog.exe są używane opcje wiersza polecenia

proces instalacji Hello jest objęte hello wideo poniżej.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Install-Azure-Log-Integration/player]



## <a name="post-installation-and-validation-steps"></a>Opublikuj kroków instalacji i sprawdzania poprawności
Po zakończeniu procedury podstawowa konfiguracja hello, gotowe krok tooperform post instalacja i weryfikacja kroki dzielą Cię:
1. Otwórz okno programu PowerShell z podwyższonym poziomem uprawnień i przejdź zbyt**c:\Program Files\Microsoft Azure dziennika integracji**
2. pierwszym krokiem Hello należy tootake jest hello tooget, poleceń cmdlet AzLog zaimportowane. Możesz to zrobić, uruchamiając skrypt hello **LoadAzlogModule.ps1** (powiadomienie hello ". \" w hello następujące polecenia). Typ **.\LoadAzlogModule.ps1** i naciśnij klawisz **ENTER**.  
Powinny zostać wyświetlone informacje takie jak na poniższej ilustracji hello wyświetlaną. </br></br>
![Ekran instalacji z zaznaczonym polem telemetrii](./media/security-azure-log-integration-get-started/loaded-modules.png) </br></br>
3. Teraz należy tooconfigure AzLog toouse określonego środowiska platformy Azure. "Środowiska platformy Azure" jest hello "type" w centrum danych chmury Azure, który ma toowork z. Gdy istnieje wiele środowisk Azure w tym momencie, obecnie odpowiednie opcje hello są **AzureCloud** lub **AzureUSGovernment**.   W środowisku PowerShell z podwyższonym poziomem uprawnień, upewnij się, że jesteś w **c:\program files\Microsoft Azure dziennika integracji\** </br></br>
    Gdy istnieje, uruchom polecenie hello: </br>
    ``Set-AzlogAzureEnvironment -Name AzureCloud``(w przypadku komercyjnej Azure)

      >[!NOTE]
      Gdy polecenie hello zakończy się powodzeniem, nie będą otrzymywać opinię.  Jeśli chcesz toouse hello Azure dla instytucji rządowych nam chmury, należy użyć **AzureUSGovernment** (dla hello — nazwa zmiennej) dla hello chmury dla instytucji rządowych USA. Inne chmury Azure nie są obsługiwane w tej chwili.  
4. Zanim będzie możliwe monitorowanie systemu należy hello nazwę konta magazynu hello używany diagnostyki Azure.  W hello portalu Azure Przejdź zbyt**maszyn wirtualnych** i poszukaj hello maszyny wirtualnej, która będzie monitorował. W hello **właściwości** wybierz **ustawień diagnostycznych**.  Polecenie **agenta** i zanotuj nazwę konta magazynu hello określony. Konieczne będzie nazwa tego konta w późniejszym kroku.
![Ustawienia diagnostyki Azure](./media/security-azure-log-integration-get-started/storage-account-large.png) </br></br>

      ![Ustawienia diagnostyki Azure](./media/security-azure-log-integration-get-started/azure-monitoring-not-enabled-large.png)
      >[!NOTE]
      Jeśli podczas tworzenia maszyny wirtualnej nie włączono monitorowania będziesz mieć możliwość tooenable opcji hello go jak pokazano powyżej.
5. Teraz możemy przełączać naszych toohello wstecz uwagi maszyny integracji dzienników Azure. Potrzebujemy tooverify mają łączność toohello konta magazynu z systemu hello, zainstalowanym integracji dziennika Azure. Hello komputera fizycznego lub maszynę wirtualną działającą hello Azure dziennika integracji usługi wymaga dostępu toohello tooretrieve informacji o koncie magazynu zarejestrowane przez diagnostyki Azure, zgodnie z konfiguracją na każdym hello monitorowane systemów.  
  1. Możesz pobrać Eksploratora usługi Storage Azure [tutaj](http://storageexplorer.com/).
  2. Wykonaj czynności procedury instalacji hello
  3. Po zakończeniu instalacji powitania kliknij **dalej** i pozostawić pole wyboru hello **Uruchom Eksploratora usługi Microsoft Azure Storage** zaznaczone.  
  4. Zaloguj się za tooAzure.
  5. Upewnij się, można wyświetlić hello konta magazynu, które skonfigurowano diagnostyki Azure.  
![Konta magazynu](./media/security-azure-log-integration-get-started/storage-account.jpg) </br></br>
   6. Zwróć uwagę, że istnieje kilka opcji w obszarze kont magazynu. Jeden z nich jest **tabel**. W obszarze **tabel** powinny pojawić się jeden o nazwie **WADWindowsEventLogsTable**. </br></br>
   ![Konta magazynu](./media/security-azure-log-integration-get-started/storage-explorer.png) </br>

## <a name="integrate-azure-diagnostic-logging"></a>Integracja rejestrowania diagnostycznego Azure
W tym kroku skonfigurujesz hello maszyny z systemem hello Azure dziennika integracji usługi tooconnect toohello konta magazynu zawierającego pliki dziennika hello.
toocomplete w tym kroku są wymagane na początku kilka rzeczy.  
* **FriendlyNameForSource:** jest przyjazna nazwa, które można zastosować konta magazynu toohello skonfigurowano hello toostore informacji o maszynie wirtualnej diagnostyki Azure
* **StorageAccountName:** jest hello nazwa konta magazynu hello określone podczas konfigurowania diagnotics platformy Azure.  
* **Atrybutu StorageKey:** jest hello klucz magazynu dla konta magazynu hello przechowywania hello Azure Diagnostics informacje dla tej maszyny wirtualnej.  

Wykonaj powitania po klucz magazynu hello tooobtain kroki:
 1. Przeglądaj toohello [portalu Azure](http://portal.azure.com).
 2. W okienku nawigacji hello hello Azure konsoli, przewiń w dół toohello i kliknij przycisk **więcej usług.**

 ![Więcej usług](./media/security-azure-log-integration-get-started/more-services.png)
 3. Wprowadź **magazynu** w hello **filtru** pola tekstowego. Kliknij przycisk **kont magazynu** (Ta wartość będzie wyświetlana po wprowadzeniu **magazynu**)

   ![pole filtru](./media/security-azure-log-integration-get-started/filter.png)
 4. Zostanie wyświetlona lista kont magazynu, kliknij dwukrotnie konta hello przypisania tooLog magazynu.

   ![Lista kont magazynu](./media/security-azure-log-integration-get-started/storage-accounts.png)
 5. Polecenie **klucze dostępu** w hello **ustawienia** sekcji.

  ![Klawisze dostępu](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 6. Kopiuj **klucz1** i umieszczenie go w bezpiecznej lokalizacji, do której będziesz mieć dostęp do następnego kroku hello.

   ![dwa klucze dostępu](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 7. Na serwerze hello zainstalowania integracji dziennika Azure Otwórz wiersz polecenia z podwyższonym poziomem uprawnień (należy pamiętać, że firma Microsoft korzysta z podwyższonym poziomem uprawnień okno wiersza polecenia w tym miejscu, nie z podwyższonym poziomem uprawnień konsoli programu PowerShell).
 8. Przejdź do zbyt**c:\Program Files\Microsoft Azure dziennika integracji**
 9. Uruchom polecenie ``Azlog source add <FriendlyNameForTheSource> WAD <StorageAccountName> <StorageKey> `` </br> Na przykład ``Azlog source add Azlogtest WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==`` Jeśli chcesz tooshow identyfikator subskrypcji hello się w przypadku hello XML, Dołącz hello subskrypcji identyfikator toohello przyjazną nazwę: ``Azlog source add <FriendlyNameForTheSource>.<SubscriptionID> WAD <StorageAccountName> <StorageKey>`` lub na przykład``Azlog source add Azlogtest.YourSubscriptionID WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==``

>[!NOTE]  
Poczekać too60 minut, a następnie wyświetlić hello zdarzenia, które są pobierane z hello konta magazynu. tooview Otwórz **Podgląd zdarzeń > Dzienniki systemu Windows > zdarzenia przekazane** na powitania Azlog Integrator.

W tym miejscu można zauważyć, że wideo przez kroki hello wymienionego powyżej.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Enable-Diagnostics-and-Storage/player]


## <a name="what-if-data-is-not-showing-up-in-hello-forwarded-events-folder"></a>Co zrobić, jeśli dane nie pojawia się w folderze zdarzenia przekazane hello?
Jeśli po upływie godziny danych nie pojawia się w hello **zdarzenia przekazane** folder, a następnie:

1. Sprawdź hello maszyny uruchomionej hello Azure dziennika integracji usługi i upewnij się, że można uzyskać dostępu do platformy Azure. tootest łączności, spróbuj tooopen hello [portalu Azure](http://portal.azure.com) z hello przeglądarki.
2. Upewnij się, że konto użytkownika hello **Azlog** ma uprawnienia do zapisu w folderze hello **users\Azlog**.
  <ol type="a">
   <li>Otwórz **Eksploratora Windows** </li>
  <li> Przejdź do zbyt**c:\users** </li>
  <li> Kliknij prawym przyciskiem myszy **c:\users\Azlog** </li>
  <li> Polecenie **zabezpieczeń**  </li>
  <li> Polecenie **NT Service\Azlog** i sprawdź uprawnienia hello hello konta. Jeśli hello konto nie ma na tej karcie lub hello odpowiednich uprawnień, nie są obecnie pokazujące, można przyznać praw konta hello na tej karcie.</li>
  </ol>
3.Upewnij się, że konto magazynu hello dodane w poleceniu hello **dodać źródła Azlog** znajduje się po uruchomieniu polecenia hello **listy źródeł Azlog**.
4. Przejdź za**Podgląd zdarzeń > Dzienniki systemu Windows > Aplikacja** toosee, jeśli wystąpią jakieś błędy zgłoszone hello Azure dziennika integracji.


Jeśli wystąpiły problemy podczas hello instalacji i konfiguracji, otwórz [żądania obsługi](../azure-supportability/how-to-create-azure-support-request.md), wybierz pozycję **integracji dziennika** jako usługa hello żądania pomocy technicznej.

Inną opcją pomocy technicznej jest hello [Forum MSDN integracji dziennika Azure](https://social.msdn.microsoft.com/Forums/home?forum=AzureLogIntegration). W tym miejscu społeczności hello może obsługiwać wzajemnie pytania, odpowiedzi, porady i wskazówki na jak tooget najbardziej hello poza integracji dziennika Azure. Ponadto hello Azure dziennika integracji zespołu monitoruje tym forum i zawierają informacje pomocne przy każdym możemy.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat integracji Azure dziennika Zobacz hello w następujących dokumentach:

* [Microsoft Azure dziennika integracji Azure dzienników](https://www.microsoft.com/download/details.aspx?id=53324) — Centrum pobierania, aby uzyskać szczegółowe informacje, wymagania systemowe i zainstalować instrukcje dotyczące integracji dzienników Azure.
* [Wprowadzenie tooAzure dziennika integracji](security-azure-log-integration-overview.md) — tym dokumencie przedstawiono tooAzure dziennika integracji, jego kluczowych możliwości i jak działa.
* [Czynności konfiguracyjnych partnera](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) — ten wpis w blogu pokazuje, jak tooconfigure Azure dziennika toowork integracji z rozwiązań partnerskich Splunk HP ArcSight i IBM QRadar. Jest to naszych bieżącego wskazówki dotyczące sposobu tooconfigure hello składniki SIEM. Skontaktuj się z dostawcą SIEM najpierw uzyskać dodatkowe szczegóły.
* [Dzienników Azure — często zadawane pytania (FAQ) integracji](security-azure-log-integration-faq.md) — to często zadawane pytania dotyczące odpowiedzi na pytania dotyczące integracji dzienników Azure.
* [Integrowanie Centrum zabezpieczeń alertów z usługi Azure dziennika integracji](../security-center/security-center-integrating-alerts-with-log-integration.md) — tym dokumencie przedstawiono, jak alerty Centrum zabezpieczeń toosync, wraz z zebrane przez diagnostyki Azure i Dzienniki aktywności platformy Azure, z Twojego analizy dzienników zdarzeń zabezpieczeń maszyny wirtualnej lub rozwiązania SIEM.
* [Nowe funkcje diagnostyki Azure i dzienników inspekcji platformy Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) — ten wpis w blogu wprowadza tooAzure dzienniki inspekcji i inne funkcje, które ułatwiają uzyskać wgląd w działania hello zasobów platformy Azure.
