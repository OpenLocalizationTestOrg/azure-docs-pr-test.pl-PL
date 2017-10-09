---
title: "aaaGet pracę z obszarem roboczym usługi Analiza dzienników Azure | Dokumentacja firmy Microsoft"
description: "Pracę z obszarem roboczym usługi Log Analytics można rozpocząć w kilka minut."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 508716de-72d3-4c06-9218-1ede631f23a6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/08/2017
ms.author: magoedte
ms.openlocfilehash: 442a9258a37ee79e8f0b45759ef24b5e3dae0130
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-log-analytics-workspace"></a>Wprowadzenie do obszaru roboczego usługi Log Analytics
Możesz szybko rozpocząć pracę z usługą Azure Log Analytics, która pomaga oceniać analizę operacyjną zbieraną z infrastruktury IT. Dzięki informacjom zawartym w tym artykule można łatwo i *bezpłatnie* rozpocząć eksplorowanie i analizowanie zbieranych danych oraz wykonywanie na nich działań.

W tym artykule służy jako tooLog wprowadzenie Analytics przy użyciu krótki toowalk samouczka możesz przy użyciu minimalnego wdrożenia na platformie Azure tak, aby uruchomić przy użyciu usługi hello. Witaj kontenerem logicznym przechowywania danych zarządzania na platformie Azure nosi nazwę obszaru roboczego. Po przejrzeniu tych informacji i zakończenia własnych oceny, należy usunąć hello oceny roboczym. Ponieważ ten artykuł jest samouczkiem, nie zawiera on informacji dotyczących wymagań biznesowych i planowania ani wskazówek dotyczących architektury.

>[!NOTE]
>Jeśli używasz hello chmury programu Microsoft Azure dla instytucji rządowych, użyj [monitorowania Azure dla instytucji rządowych + dokumentacja dotycząca zarządzania](https://docs.microsoft.com/azure/azure-government/documentation-government-services-monitoringandmanagement#log-analytics) zamiast tego.

Poniżej przedstawiono krótki przegląd tooget proces wykorzystywany hello uruchomiona:

![diagram procesu](./media/log-analytics-get-started/onboard-oms.png)

## <a name="1-create-an-azure-account-and-sign-in"></a>1. Tworzenie konta platformy Azure i logowanie

Jeśli nie masz jeszcze konta platformy Azure, należy toouse jeden toocreate analizy dzienników. Możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free/), które jest ważne przez 30 dni i umożliwia dostęp do dowolnej usługi Azure.

### <a name="toocreate-a-free-account-and-sign-in"></a>toocreate bezpłatne konto i zaloguj się
1. Postępuj zgodnie ze wskazówkami hello na [utworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/free/).
2. Przejdź toohello [portalu Azure](https://portal.azure.com) i zaloguj się.

## <a name="2-create-a-workspace"></a>2. Tworzenie obszaru roboczego

Witaj następnym krokiem jest toocreate obszaru roboczego.

1. W portalu Azure hello, listy hello usług w hello Marketplace wyszukiwania dla *analizy dzienników*, a następnie wybierz **analizy dzienników**.  
    ![Witryna Azure Portal](./media/log-analytics-get-started/log-analytics-portal.png)
2. Kliknij przycisk **Utwórz**, następnie wybierz opcje dla hello następujące elementy:
   * **Obszar roboczy pakietu OMS** — wpisz nazwę obszaru roboczego.
   * **Subskrypcja** — Jeśli masz wiele subskrypcji, wybierz hello z nich ma tooassociate z hello nowy obszar roboczy.
   * **Grupa zasobów**
   * **Lokalizacja**
   * **Warstwa cenowa**  
       ![szybkie tworzenie](./media/log-analytics-get-started/oms-onboard-quick-create.png)
3. Kliknij przycisk **OK** toosee listę obszarów roboczych.
4. Wybierz toosee obszaru roboczego jego szczegóły hello portalu Azure.       
    ![szczegóły obszaru roboczego](./media/log-analytics-get-started/oms-onboard-workspace-details.png)         

## <a name="3-upgrade-workspace-toonew-log-search"></a>Wyszukiwania dziennika toonew 3 uaktualnienia obszaru roboczego
Została wydana nowy język zapytań usługi Analiza dzienników i w kolejności tootake korzystania z nich, należy tooconvert obszaru roboczego.  Jeśli region hello obszaru roboczego znajduje się w został uaktualniony, powinny pojawić się purpurowa transparent hello górze obszaru roboczego zaprasza Cię tooconvert. uaktualnienie Hello jest dobrowolne całkowicie i nie ma wpływu na środowiska pracy z analizy dzienników i rozwiązań dodane.  

Dalsze informacje toounderstand hello korzyści, zagadnień i tooupgrade procesu, zobacz [wyszukiwania dziennika toonew uaktualniania Azure Log Analytics](log-analytics-log-search-upgrade.md).  

## <a name="4-add-solutions-and-solution-offerings"></a>4. Dodawanie rozwiązań i ofert rozwiązań

Następnie dodaj rozwiązania do zarządzania i ofert rozwiązań. Rozwiązania to zestawy reguł logiki, wizualizacji i gromadzenia danych zawierające metryki dotyczące określonego obszaru problemów. Oferta rozwiązań to pakiet rozwiązań do zarządzania.

Dodanie obszaru roboczego tooyour rozwiązania pozwala toocollect analizy dzienników różne rodzaje danych z komputerów, które są połączone tooyour obszaru roboczego przy użyciu agentów. Informacje dotyczące dodawania agentów zostaną przedstawione później.

### <a name="tooadd-solutions-and-solution-offerings"></a>tooadd rozwiązań i ofert rozwiązania

1. W portalu Azure kliknij **nowy** , a następnie w hello **marketplace hello wyszukiwania** wpisz **analizy dzienników działania** , a następnie naciśnij klawisz ENTER.
2. W hello wszystko bloku, wybierz opcję **analizy dzienników działania** , a następnie kliknij przycisk **Utwórz**.  
    ![Activity Log Analytics](./media/log-analytics-get-started/activity-log-analytics.png)  
3. W hello *Nazwa rozwiązania zarządzania* bloku, wybierz obszar roboczy, które mają tooassociate z rozwiązaniem do zarządzania hello.
4. Kliknij przycisk **Utwórz**.  
    ![obszar roboczy rozwiązania](./media/log-analytics-get-started/solution-workspace.png)  
5. Powtórz kroki od 1 do 4 tooadd:
    - Witaj **zabezpieczeń i zgodności** oferty z rozwiązaniami hello bezpieczeństwa i ochrony przed złośliwym kodem, oceny i inspekcji usługi.
    - Witaj **Automatyzacja i kontrola** oferty hello automatyzacji hybrydowy proces roboczy, śledzenia zmian i rozwiązań System oceny aktualizacji (nazywanych również zarządzania aktualizacjami) usługi. Po dodaniu hello rozwiązania oferty, należy utworzyć konto usługi Automatyzacja.  
        ![Konto usługi Automation](./media/log-analytics-get-started/automation-account.png)  
6. Możesz wyświetlić rozwiązania do zarządzania hello dodanych roboczym tooyour przechodząc zbyt**analizy dzienników** > **subskrypcje** > ***nazwa obszaru roboczego***  >  **Omówienie**. Kafelki na potrzeby rozwiązania do zarządzania hello dodane przez użytkownika są wyświetlane.  
    >[!NOTE]
    >Ponieważ firma Microsoft nie jeszcze łączyły dowolnym obszarze roboczym toohello agentów, nie ma żadnych danych hello rozwiązań, które zostały dodane.  

    ![kafelki rozwiązania bez danych](./media/log-analytics-get-started/solutions-no-data.png)

## <a name="4-create-a-vm-and-onboard-an-agent"></a>4. Tworzenie maszyny wirtualnej i dodawanie agenta

Następnie należy utworzyć prostą maszynę wirtualną na platformie Azure. Po utworzeniu maszyny Wirtualnej, dołączyć hello OMS agenta tooenable go. Włączanie agent hello uruchamia zbieranie danych z hello maszyny Wirtualnej i wysyła dane tooLog Analytics.

### <a name="toocreate-a-virtual-machine"></a>toocreate maszyny wirtualnej

- Postępuj zgodnie ze wskazówkami hello na [tworzenie pierwszej maszyny wirtualnej systemu Windows w portalu Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md) i uruchomić hello nowej maszyny wirtualnej.

### <a name="connect-hello-virtual-machine-toolog-analytics"></a>Połącz tooLog maszyny wirtualnej hello analityka

- Postępuj zgodnie ze wskazówkami hello na [tooLog maszyny wirtualne Azure połączyć Analytics](log-analytics-azure-vm-extension.md) tooconnect hello wirtualna tooLog Analytics przy użyciu hello portalu Azure.

## <a name="6-view-and-act-on-data"></a>6. Wyświetlanie danych i działanie na nich

Wcześniej włączony hello rozwiązania analizy dziennika aktywności i ofert usług zabezpieczeń i zgodności oraz Automatyzacja i kontrola hello. Następnie można rozpocząć analizę danych zebranych przez te rozwiązania oraz wyników w wyszukiwaniach w dziennikach.

toostart, znajduje się w danych wyświetlanych w ramach rozwiązania. Następnie należy zapoznać się z wyszukiwaniami w dziennikach. Dziennik wyszukiwania pozwalają toocombine i skorelowania danych dowolnego komputera z wielu źródeł w danym środowisku. Aby uzyskać więcej informacji, zobacz [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-searches.md) lub jeśli można przekonwertować obszaru roboczego toohello nowego zapytania języka, zobacz [opis dziennika przeszukuje analizy dzienników](log-analytics-log-search-new.md). 

### <a name="tooview-antimalware-data"></a>tooview danych ochrony przed złośliwym oprogramowaniem

1. W portalu Azure hello kolejno zbyt**analizy dzienników** > ***obszaru roboczego***.
2. W bloku hello obszaru roboczego w obszarze **ogólne**, kliknij przycisk **omówienie**.  
    ![Omówienie](./media/log-analytics-get-started/overview.png)
3. Kliknij przycisk hello **oceny ochrony przed złośliwym kodem** kafelka. W tym przykładzie można zobaczyć, że usługa Windows Defender została zainstalowana na jednym komputerze, ale jej sygnatura jest nieaktualna.  
    ![Oprogramowanie chroniące przed złośliwym kodem](./media/log-analytics-get-started/solution-antimalware.png)
4. Na przykład w obszarze **stanu ochrony**, kliknij przycisk **podpisu nieaktualny** tooopen wyszukiwania dziennika i wyświetlenia jej szczegółów hello komputerów, które mają podpisy nieaktualny. W tym przykładzie należy zwrócić uwagę nosi nazwę tego komputera hello *getstarted*. Jeśli więcej niż jeden komputer z nieaktualny podpisów, czy wszystkie pojawią się one w hello wyszukiwania dziennika wyników.  
    ![Oprogramowanie chroniące przed złośliwym kodem jest nieaktualne](./media/log-analytics-get-started/antimalware-search.png)

### <a name="tooview-security-and-audit-data"></a>tooview zabezpieczeń i kontroli danych

1. W bloku hello obszaru roboczego w obszarze **ogólne**, kliknij przycisk **omówienie**.  
2. Kliknij przycisk hello **zabezpieczeń i inspekcji** kafelka. W tym przykładzie można zobaczyć, że występują dwa istotne problemy: na jednym komputerze brak jest krytycznych aktualizacji, a inny komputer nie ma wystarczającej ochrony.  
    ![Zabezpieczenia i inspekcja](./media/log-analytics-get-started/security-audit.png)
3. Na przykład w obszarze **godne uwagi problemy**, kliknij przycisk **komputerów brakuje aktualizacji krytycznych** tooopen wyszukiwania dziennika i Wyświetl szczegółowe informacje o komputerach brakuje aktualizacji krytycznych. W tym przykładzie brak jest jednej aktualizacji krytycznej i 63 innych aktualizacji.  
    ![Wyszukiwanie w dzienniku zabezpieczeń i inspekcji](./media/log-analytics-get-started/security-audit-log-search.png)

### <a name="tooview-and-act-on-system-update-data"></a>tooview i ustawy o danych aktualizacji systemu

1. W bloku hello obszaru roboczego w obszarze **ogólne**, kliknij przycisk **omówienie**.  
2. Kliknij przycisk hello **oceny aktualizacji systemu** kafelka. W tym przykładzie można zobaczyć, że istnieje jeden komputer z systemem Windows o nazwie *getstarted* wymagający aktualizacji krytycznych i jeden komputer wymagający aktualizacji definicji.  
    ![Aktualizacje systemu](./media/log-analytics-get-started/system-updates.png)
3. Na przykład w obszarze **brakujące aktualizacje**, kliknij przycisk **aktualizacje krytyczne** tooopen wyszukiwania dziennika i Wyświetl szczegółowe informacje o komputerach brakuje aktualizacji krytycznych. W tym przykładzie brak jest jednej aktualizacji i istnieje jedna wymagana aktualizacja.  
    ![Wyszukiwanie w dzienniku aktualizacji systemu](./media/log-analytics-get-started/system-updates-log-search.png)
4. Przejdź toohello [Operations Management Suite](http://microsoft.com/oms) witryny sieci Web i zaloguj się przy użyciu konta platformy Azure. Po zalogowaniu należy zauważyć, że informacje o rozwiązaniu hello jest podobne toowhat widać w hello portalu Azure.  
    ![Portal pakietu OMS](./media/log-analytics-get-started/oms-portal.png)
5. Kliknij przycisk hello **zarządzania aktualizacjami** kafelka.
6. Na pulpicie nawigacyjnym zarządzania zaktualizować hello należy zauważyć, że informacje o aktualizacjach systemu hello jest podobne informacje toohello System aktualizowanie, które przedstawiono w hello portalu Azure. Jednak hello **Zarządzanie wdrożenia aktualizacji** kafelka jest nowa. Kliknij przycisk hello **Zarządzanie wdrożenia aktualizacji** kafelka.  
    ![Kafelek Zarządzanie aktualizacjami](./media/log-analytics-get-started/update-management.png)
7. Na powitania **wdrożeń aktualizacji** kliknij przycisk **Dodaj** toocreate *przebieg aktualizacji*.  
    ![Wdrożenia aktualizacji](./media/log-analytics-get-started/update-management-update-deployments.png)
8.  Na powitania **nowe wdrożenie aktualizacji** strony, wpisz nazwę dla wdrożenia aktualizacji hello, wybierz tooupdate komputery (w tym przykładzie *getstarted*), wybierz harmonogram, a następnie kliknij przycisk **zapisać**.  
    ![Nowe wdrożenie](./media/log-analytics-get-started/new-deployment.png)  
    Po zapisaniu hello wdrożenia aktualizacji, zobacz hello zaplanowanych aktualizacji.  
    ![zaplanowana aktualizacja](./media/log-analytics-get-started/scheduled-update.png)  
    Po ukończeniu przebiegu aktualizacji hello hello pokazuje stan **Zakończono**.
    ![zakończona aktualizacja](./media/log-analytics-get-started/completed-update.png)
9. Po zakończeniu przebiegu aktualizacji hello można wyświetlić czy hello Uruchom zakończyła się powodzeniem i możliwość wyświetlania szczegółów dotyczących aktualizacji co w przypadku.

## <a name="after-evaluation"></a>Po dokonaniu oceny

W tym samouczku pokazano, jak zainstalować agenta na maszynie wirtualnej i szybko rozpocząć pracę. wykonano kroki Hello były szybkie i proste. Jednak większość dużych organizacji i przedsiębiorstw ma złożone lokalne infrastruktury IT. Tak zbieranie danych z tych złożonych środowiskach ma dodatkowe planowanie i nakładu niż hello samouczka. Przejrzyj informacje hello w powitania po sekcji Następne kroki artykuły toohelpful łącza.

Opcjonalnie można usunąć obszaru roboczego hello, które zostały utworzone z tego samouczka.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o nawiązywaniu połączeń [agentów systemu Windows](log-analytics-windows-agents.md) tooLog Analytics.
* Dowiedz się więcej o nawiązywaniu połączeń [agenty programu Operations Manager](log-analytics-om-agents.md) tooLog Analytics.
* [Dodawanie rozwiązania analizy dzienników z galerii rozwiązań hello](log-analytics-add-solutions.md) tooadd funkcjonalność i zbieranie danych.
* Zapoznaj się z [dziennika wyszukiwania](log-analytics-log-searches.md) tooview szczegółowe informacje zebrane przez rozwiązania.
