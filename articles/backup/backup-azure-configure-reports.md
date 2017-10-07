---
title: "Raporty aaaConfigure dla usługi Kopia zapasowa Azure"
description: "Ten artykuł zawiera informacje o konfigurowaniu raportów usługi Power BI dla usługi Kopia zapasowa Azure przy użyciu magazynu usług odzyskiwania."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 86e465f1-8996-4a40-b582-ccf75c58ab87
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 503a240b36ea999e0fea434b6a50d26ddf7677bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-backup-reports"></a>Konfigurowanie raportów usługi Azure Backup
Ten artykuł zawiera informacje o raporty tooconfigure kroki dla usługi Kopia zapasowa Azure przy użyciu magazynu usług odzyskiwania i tooaccess tych raportów za pomocą usługi Power BI. Po wykonaniu tych kroków, możesz bezpośrednio przejść tooview tooPower BI wszystkich raportów hello, dostosowywanie i tworzenia raportów. 

## <a name="supported-scenarios"></a>Obsługiwane scenariusze
1. Raporty kopia zapasowa Azure są obsługiwane dla maszyny wirtualnej platformy Azure tworzenia kopii zapasowej i plik lub folder kopii zapasowej toocloud za pomocą agenta usług odzyskiwania Azure.
2. Raporty dotyczące Azure SQL, program DPM i serwer kopii zapasowej Azure nie są obsługiwane w tej chwili.
3. Raporty można wyświetlić różnych magazynów i różnych subskrypcji, skonfigurowanie tego samego konta magazynu dla każdej hello magazynów. Należy wybrać konto magazynu w hello magazyn usług odzyskiwania tego samego regionu.
4. częstotliwość Hello zaplanowanego odświeżania raportów hello wynosi 24 godziny w usłudze Power BI. Można również przeprowadzić odświeżanie ad hoc hello raportów w usłudze Power BI, w których wielkość najnowsze dane na koncie magazynu klienta jest używany do renderowania raportów. 

## <a name="prerequisites"></a>Wymagania wstępne
1. Utwórz [konto magazynu Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) tooconfigure dla raportów. To konto magazynu jest używany do przechowywania danych powiązanych raportów.
2. [Utwórz konto usługi Power BI](https://powerbi.microsoft.com/landing/signin/) tooview, dostosowywanie i tworzenie własnych raportów za pomocą portalu usługi Power BI.
3. Rejestrowanie dostawcy zasobów hello **elemencie Microsoft.insights** Jeśli nie zarejestrowano już, z subskrypcją hello konta magazynu, a także z subskrypcji usługi odzyskiwania hello magazynu tooenable toohello tooflow danych raportowania Konto magazynu. toodo hello takie same, należy przejść do portalu tooAzure > subskrypcji > dostawców zasobów i sprawdź, czy ten dostawca tooregister go. 

## <a name="configure-storage-account-for-reports"></a>Konfigurowanie konta magazynu dla raportów
Witaj Użyj następującego konta magazynu hello tooconfigure kroki dla magazynu usług odzyskiwania przy użyciu portalu Azure. Jest to jednorazowej konfiguracji i po skonfigurowaniu konta magazynu, można przejść tooPower BI bezpośrednio tooview pakiet zawartości i wykorzystać raportów.
1. Jeśli masz już magazyn usług odzyskiwania, Otwórz, przejdź toonext kroku. Jeśli nie masz otwarte magazyn usług odzyskiwania, ale znajdują się w portalu Azure, w menu centralnym hello hello kliknij **Przeglądaj**.

   * Na liście hello zasobów, wpisz **usług odzyskiwania**.
   * Po rozpoczęciu wpisywania, hello listy filtry oparte na dane wejściowe. Po wyświetleniu pozycji **Magazyny Usług odzyskiwania** kliknij ją.

      ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     zostanie wyświetlona lista Hello Magazyny usług odzyskiwania. Z listy hello Magazyny usług odzyskiwania wybierz magazyn.

     Otwiera Hello wybranego magazynu z pulpitu nawigacyjnego.
2. Z listy hello elementów, który pojawia się w magazynie, kliknij przycisk **raporty kopii zapasowej** w obszarze monitorowanie i raporty w sekcji tooconfigure hello konta magazynu dla raportów.

      ![Wybierz raporty kopii zapasowej menu elementu krok 2](./media/backup-azure-configure-reports/backup-reports-settings.PNG)
3. W bloku kopia zapasowa raporty hello, kliknij **Konfiguruj** przycisku. Spowoduje to otwarcie bloku Azure Application Insights hello, który jest używany do wypychania konta magazynu toocustomer danych.

      ![Skonfiguruj konto magazynu — krok 3](./media/backup-azure-configure-reports/configure-storage-account.PNG)
4. Ustaw przycisk przełącznika stan hello zbyt**na** i wybierz **archiwum tooa konta magazynu** pole wyboru, aby raportowania danych można uruchomić przepływu toohello koncie magazynu.

      ![Włącz diagnostykę krok 4.](./media/backup-azure-configure-reports/set-status-on.png)
5. Kliknij przycisk wyboru konta magazynu i konto magazynu hello wybierz z listy hello do przechowywania raportowania danych i kliknij przycisk **OK**.

      ![Wybierz konto magazynu — krok 5](./media/backup-azure-configure-reports/select-storage-account.png)
6. Wybierz **AzureBackupReport** pole wyboru i również przenieść hello suwaka tooselect okres przechowywania to dane raportowania. Raportowanie danych na koncie magazynu hello jest przechowywana na okres hello wybranych za pomocą tego suwaka.

      ![Wybierz konto magazynu — krok 6](./media/backup-azure-configure-reports/save-configuration.png)
7. Przejrzyj wszystkie zmiany hello i kliknij przycisk **zapisać** znajdującego się na górze, jak pokazano na powyższym rysunku hello. Ta akcja gwarantuje, że wszystkie zmiany są zapisywane i konto magazynu jest teraz skonfigurowane do przechowywania danych raportowania.

> [!NOTE]
> Po skonfigurowaniu raportów przez zapisanie konta magazynu należy **Poczekaj 24 godziny** dla toocomplete wypychania danych początkowych. Pakiet zawartości usługi Kopia zapasowa Azure w usłudze Power BI należy importować tylko po tym czasie. Zobacz [sekcji często zadawanych PYTAŃ](#frequently-asked-questions) jeszcze bardziej szczegółowe informacje. 
>
>

## <a name="view-reports-in-power-bi"></a>Wyświetlanie raportów w usłudze Power BI 
Po Konfigurowanie konta magazynu dla raportów, za pomocą magazynu usług odzyskiwania, trwa około 24 godziny dla raportowania danych toostart przepływu w. Po 24 godzinach konfigurowania konta magazynu Użyj następujących hello kroki tooview raporty w usłudze Power BI:
1. [Zaloguj się](https://powerbi.microsoft.com/landing/signin/) tooPower BI.
2. Kliknij przycisk **Pobierz dane** i kliknij przycisk Pobierz w obszarze **usług** w bibliotece zawartości pakietu. Wykonaj kroki wymienione w [pakiet zawartości usługi Power BI dokumentacji tooaccess](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/).

     ![Importowanie pakietu zawartości](./media/backup-azure-configure-reports/content-pack-import.png)
3. Typ **kopia zapasowa Azure** na pasku wyszukiwania i kliknij przycisk **Pobierz teraz**.

      ![Pobierz pakiet zawartości](./media/backup-azure-configure-reports/content-pack-get.png)
4. Wprowadź nazwę konta magazynu hello skonfigurowane w kroku 5 powyżej, a następnie kliknij przycisk **dalej** przycisku.

    ![Wprowadź nazwę konta magazynu](./media/backup-azure-configure-reports/content-pack-storage-account-name.png)    
5. Wprowadź klucz konta magazynu hello do tego konta magazynu. Możesz [wyświetlanie i kopiowanie kluczy dostępu do magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-account) przechodząc tooyour konta magazynu w portalu Azure. 

     ![Wprowadź konto magazynu](./media/backup-azure-configure-reports/content-pack-storage-account-key.png) <br/>
     
6. Kliknij przycisk **Zaloguj** przycisku. Zaloguj się ponownie, możesz otrzymywać **importowania danych** powiadomień.

    ![Importowanie pakietu zawartości](./media/backup-azure-configure-reports/content-pack-importing-data.png) <br/>
    
    Po pewnym czasie **Powodzenie** powiadomienie po zakończeniu importowania hello. W przypadku dużych ilości danych na koncie magazynu hello małego dłużej tooimport hello pakietu zawartości, może potrwać.
    
    ![Importowanie pakietu zawartości Powodzenie](./media/backup-azure-configure-reports/content-pack-import-success.png) <br/>
    
7. Gdy dane są importowane pomyślnie, **kopia zapasowa Azure** pakiet zawartości jest widoczny w **aplikacji** w okienku nawigacji hello. Lista Hello zawiera teraz pulpitu nawigacyjnego usługi Kopia zapasowa Azure, raporty i zestawu danych z żółtą gwiazdką wskazującą nowo zaimportowany raportów. 

     ![Pakiet zawartości z kopii zapasowej platformy Azure](./media/backup-azure-configure-reports/content-pack-azure-backup.png) <br/>
     
8. Kliknij przycisk **kopia zapasowa Azure** w obszarze pulpity nawigacyjne, który wskazuje zestaw przypiętych raportów klucza.

      ![Pulpitu nawigacyjnego kopia zapasowa Azure](./media/backup-azure-configure-reports/azure-backup-dashboard.png) <br/>
9. tooview hello pełny zestaw raportów, kliknij przycisk żadnych raportów na pulpicie nawigacyjnym hello.

      ![Azure kondycji zadania tworzenia kopii zapasowej](./media/backup-azure-configure-reports/azure-backup-job-health.png) <br/>
10. Kliknij każdą kartę w raportach tooview raporty hello w tym obszarze.

      ![Karty raporty kopia zapasowa Azure](./media/backup-azure-configure-reports/reports-tab-view.png)


## <a name="frequently-asked-questions"></a>Często zadawane pytania
1. **Jak Sprawdź, czy dane raportowania została uruchomiona przepływu toostorage konta?**
    
    Można przejść magazynu toohello konta skonfigurowane i wybierz kontenery. Kontener hello ma wpis dotyczący insights — dzienniki azurebackupreport, wskazuje, że dane raportowania rozpoczęła przepływu.

2. **Co to jest częstotliwość hello konto toostorage wypychania danych i pakiet zawartości usługi Kopia zapasowa Azure w usłudze Power BI?**

   Dla użytkowników od dnia 0 zajmie około 24 godziny toopush danych toostorage konta. Po tym początkowej wypychania compelete, dane są odświeżane z powitania po częstotliwość hello rysunku poniżej. 
      * Dane powiązane zbyt**zadań, alerty, elementy kopii zapasowej, magazynów, chronionych serwerów i zasady** spoczywa toocustomer konto magazynu, jak i przy rejestrowaniu.
      * Dane powiązane zbyt**magazynu** spoczywa konta magazynu toocustomer co 24 godziny.
   
    ![Częstotliwość wypychania danych raportów kopia zapasowa Azure](./media/backup-azure-configure-reports/reports-data-refresh-cycle.png)

  Usługa Power BI ma [zaplanowanego odświeżania raz dziennie](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed). Ręczne odświeżanie danych hello można wykonywać w usłudze Power BI hello zawartości pakietu.

3. **Jak długo można zachować hello raportów** 

   Podczas konfigurowania konta magazynu, można wybrać okres przechowywania danych raportowania na koncie magazynu hello (przy użyciu kroku 6 na koncie magazynu konfiguracji dla sekcji raportów powyżej). Oprócz tego możesz [raportów analizy w programie excel](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/) i zapisać je na dłuższy okres przechowywania, zgodnie z potrzebami. 

4. **Po skonfigurowaniu konta magazynu hello będą widoczne wszystkie dane w raportach?**

   Witaj wszystkie dane generowane po **"Konfigurowanie konta magazynu"** wypychanie zostanie wykonane dla konta magazynu toohello i będą dostępne w raportach. Jednak **rozpoczętych zadań nie są usuwane,** do raportowania. Gdy zadanie hello lub niepomyślnym zakończeniem, wysyłana tooreports.

5. **Jeśli I zostały już skonfigurowane raporty tooview konta magazynu hello, można zmienić toouse konfiguracji hello innego konta magazynu?** 

   Tak, można zmienić hello konfiguracji toopoint tooa innego konta magazynu. Hello nowo skonfigurowane konto magazynu należy używać podczas łączenia pakietu zawartości tooAzure kopii zapasowej. Ponadto po skonfigurowaniu innego konta magazynu będzie przepływu nowe dane tego konta magazynu. Ale starszych danych (przed zmianą konfiguracji hello) nadal pozostanie w hello starsze konta magazynu.

6. **Raporty można wyświetlić różnych magazynów i różnych subskrypcji?** 

   Tak, można skonfigurować hello tego samego konta magazynu między różnymi magazyny tooview między magazynem raportów. Ponadto można skonfigurować hello tego samego konta magazynu dla magazynów w subskrypcjach. Można następnie użyć tego konta magazynu podczas łączenia tooAzure kopii zapasowej pakietu zawartości usługi Power BI tooview hello raportów. Wybrane konto magazynu hello należy jednak w hello magazyn usług odzyskiwania tego samego regionu.
   
## <a name="next-steps"></a>Następne kroki
Teraz, gdy skonfigurowano hello konta magazynu i zaimportowany pakiet zawartości usługi Kopia zapasowa Azure, następnym krokiem hello jest toocustomize te raporty i użyj raportowania raporty toocreate modelu danych. Można znaleźć hello następujące artykuły, aby uzyskać więcej informacji.

* [Przy użyciu modelu danych raportowania usługi Kopia zapasowa Azure](backup-azure-reports-data-model.md)
* [Filtrowanie raportów w usłudze Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
* [Tworzenie raportów w usłudze Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)

