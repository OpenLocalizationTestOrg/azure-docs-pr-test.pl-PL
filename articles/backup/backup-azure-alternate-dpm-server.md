---
title: aaaRecover danych z serwera z kopii zapasowej Azure | Dokumentacja firmy Microsoft
description: "Odzyskiwanie danych hello był chroniony magazyn usług odzyskiwania tooa z dowolnego magazynu toothat zarejestrowanego serwera usługi Kopia zapasowa Azure."
services: backup
documentationcenter: 
author: nkolli1
manager: shreeshd
editor: 
ms.assetid: a55f8c6b-3627-42e1-9d25-ed3e4ab17b1f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: adigan;giridham;trinadhk;markgal
ms.openlocfilehash: 74847880e646c3c4f198afe318f1db30363d137a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="recover-data-from-azure-backup-server"></a>Odzyskiwanie danych z usługi Azure Backup Server
Można użyć serwera kopii zapasowej Azure toorecover hello dane, które utworzono kopię zapasową tooa, które Magazyn usług odzyskiwania. Hello proces może więc jest zintegrowany z konsoli zarządzania serwerem kopia zapasowa Azure hello i podobne przepływu pracy odzyskiwania toohello dla innych składników usługi Kopia zapasowa Azure.

> [!NOTE]
> Ten artykuł dotyczy [System Center Data Protection Manager 2012 R2 z pakietem UR7 lub nowszej] (https://support.microsoft.com/en-us/kb/3065246), połączeniu z hello [najnowsza wersja agenta usługi Kopia zapasowa Azure](http://aka.ms/azurebackup_agent).
>
>

toorecover danych z serwera z kopii zapasowej Azure:

1. Z hello **odzyskiwania** kliknij kartę hello konsoli zarządzania serwerem kopia zapasowa Azure, **"Dodaj zewnętrzny program DPM"** (na powitania lewym górnym rogu ekranu hello).   
    ![Dodaj zewnętrzny program DPM](./media/backup-azure-alternate-dpm-server/add-external-dpm.png)
2. Pobierania nowych **magazynu poświadczeń** z magazynu hello skojarzone z hello **serwer kopii zapasowej Azure** w przypadku, gdy hello dane są odzyskiwane, wybierz hello Azure Utwórz kopię zapasową serwera z listy hello serwerów kopia zapasowa Azure zarejestrowany w magazynie usług odzyskiwania hello i podaj hello **hasło szyfrowania** skojarzone z serwerem hello, którego dane są odzyskiwane.

    ![Poświadczenia zewnętrznego programu DPM](./media/backup-azure-alternate-dpm-server/external-dpm-credentials.png)

   > [!NOTE]
   > Tylko serwerów kopia zapasowa Azure skojarzony z hello sam rejestracji magazynu można odzyskać dane innych osób.
   >
   >

    Po hello zewnętrznego serwera kopii zapasowej Azure pomyślnie dodany, można wybrać danych hello powitania serwera zewnętrznego i hello lokalny serwer kopii zapasowej Azure z hello **odzyskiwania** kartę.
3. Przeglądaj hello listę dostępnych serwerów produkcyjnych chronione przez hello zewnętrznego serwera kopii zapasowej Azure i wybierz hello odpowiednie źródło danych.

    ![Przeglądaj serwera zewnętrznego programu DPM](./media/backup-azure-alternate-dpm-server/browse-external-dpm.png)
4. Wybierz **hello miesiąc i rok** z hello **punktów odzyskiwania** listy rozwijanej wybierz hello wymagane **Data Recovery** dla po hello punkt odzyskiwania został utworzony i wybierz hello **Czasu odzyskiwania**.

    W okienku dolnej hello, który można przeglądać i odzyskać lokalizacji tooany zostanie wyświetlona lista plików i folderów.

    ![Punkty odzyskiwania serwera DPM zewnętrzne](./media/backup-azure-alternate-dpm-server/external-dpm-recoverypoint.png)
5. Kliknij prawym przyciskiem myszy odpowiedni element hello, a następnie kliknij przycisk **odzyskać**.

    ![Zewnętrzne odzyskiwania programu DPM](./media/backup-azure-alternate-dpm-server/recover.png)
6. Przejrzyj hello **odzyskać wybór**. Sprawdź hello danych i czasu hello kopia zapasowa ma zostać przeprowadzone odzyskiwanie, a także hello źródło, z którego została utworzona kopia zapasowa hello. Jeśli zaznaczenie hello jest nieprawidłowa, kliknij przycisk **anulować** toonavigate wstecz toorecovery kartę tooselect odzyskiwania odpowiedniego punktu. Wybór hello są poprawne, kliknij przycisk **dalej**.

    ![Podsumowanie zewnętrznych odzyskiwania programu DPM](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-summary.png)
7. Wybierz **odzyskać lokalizacji alternatywnej tooan**. **Przeglądaj** toohello poprawną lokalizację dla hello odzyskiwania.

    ![Zewnętrznej lokalizacji alternatywnej odzyskiwania programu DPM](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-alternate-location.png)
8. Wybierz opcję hello powiązane zbyt**utworzyć kopię**, **Pomiń**, lub **Zastąp**.

   * **Utwórz kopię** — tworzy kopię pliku hello, jeśli istnieje kolizję nazw.
   * **Pomiń** — Jeśli istnieje kolizję nazw nie odzyskać pliku hello, co pozostawia hello oryginalnego pliku.
   * **Zastąp** — Jeśli istnieje kolizję nazw zastępuje istniejącą kopię pliku hello hello.

     Wybierz odpowiednią opcję hello zbyt**Przywróć zabezpieczenia**. Można zastosować ustawień zabezpieczeń hello hello komputera docelowego, gdzie hello dane są odzyskiwane lub hello ustawienia zabezpieczeń, które były stosowane tooproduct w czasie hello hello punkt odzyskiwania został utworzony.

     Zidentyfikuj czy **powiadomień** jest wysyłana, po pomyślnym zakończeniu hello odzyskiwania.

     ![Powiadomienia odzyskiwania zewnętrznego programu DPM](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-notifications.png)
9. Witaj **Podsumowanie** ekranu wymieniono opcje hello wybrane do tej pory. Po kliknięciu **"Odzyskać"**, dane hello jest toohello odzyskane odpowiednie lokalnymi lokalizacji.

    ![Podsumowanie opcji odzyskiwania zewnętrznego programu DPM](./media/backup-azure-alternate-dpm-server/external-dpm-recovery-options-summary.png)

   > [!NOTE]
   > zadanie odzyskiwania Hello mogą być monitorowane w hello **monitorowanie** kartę hello serwer kopii zapasowej Azure.
   >
   >

    ![Monitorowanie odzyskiwania](./media/backup-azure-alternate-dpm-server/monitoring-recovery.png)
10. Możesz kliknąć **wyczyść zewnętrzny program DPM** na powitania **odzyskiwania** kartę hello widok hello tooremove serwera programu DPM hello zewnętrznego serwera programu DPM.

    ![Wyczyść zewnętrzny program DPM](./media/backup-azure-alternate-dpm-server/clear-external-dpm.png)

## <a name="troubleshooting-error-messages"></a>Rozwiązywanie problemów z komunikatów o błędach
| Nie. | Komunikat o błędzie | Kroki rozwiązywania problemów |
|:---:|:--- |:--- |
| 1. |Ten serwer nie jest zarejestrowany toohello magazynie określonym przez poświadczenie magazynu hello. |**Przyczyna:** ten błąd jest wyświetlany, gdy plik poświadczeń magazynu hello wybrane, nie należy toohello magazyn usług odzyskiwania skojarzonych z Azure Utwórz kopię zapasową serwera, na którym hello próby odzyskiwania. <br> **Rozwiązanie:** plik poświadczeń magazynu hello pobierania z usług odzyskiwania hello magazynu toowhich hello serwer kopii zapasowej Azure jest zarejestrowany. |
| 2. |Dane możliwe do odzyskania hello są niedostępne albo hello wybrany serwer nie jest serwerem DPM. |**Przyczyna:** nie ma żadnych innych serwerów kopia zapasowa Azure zarejestrowanych toohello magazyn usług odzyskiwania, hello serwerów nie ma jeszcze przekazane metadanych hello lub hello wybrany serwer nie jest serwerem kopia zapasowa Azure (alias systemu Windows Server lub klienta systemu Windows). <br> **Rozwiązanie:** w przypadku innych magazyn usług odzyskiwania toohello zarejestrowanych serwerów kopia zapasowa Azure, upewnij się, jest zainstalowana najnowsza wersja agenta usługi Kopia zapasowa Azure tego hello. <br>Jeśli istnieją inne magazyn usług odzyskiwania toohello zarejestrowanych serwerów kopia zapasowa Azure, poczekaj na dzień po zakończeniu instalacji toostart hello odzyskiwania. Witaj nocne zadanie przekaże hello metadane dla wszystkich toocloud kopii zapasowych hello chronione. Witaj danych będą dostępne do odzyskania. |
| 3. |Żaden inny serwer DPM jest zarejestrowany toothis magazynu. |**Przyczyna:** Brak innych Azure kopii zapasowej serwerów będące toohello zarejestrowanych magazynu, z których hello próby odzyskiwania.<br>**Rozwiązanie:** w przypadku innych magazyn usług odzyskiwania toohello zarejestrowanych serwerów kopia zapasowa Azure, upewnij się, jest zainstalowana najnowsza wersja agenta usługi Kopia zapasowa Azure tego hello.<br>Jeśli istnieją inne magazyn usług odzyskiwania toohello zarejestrowanych serwerów kopia zapasowa Azure, poczekaj na dzień po zakończeniu instalacji toostart hello odzyskiwania. Witaj nocne zadanie przekazuje hello metadane dla wszystkich toocloud kopie zapasowe chronionych. Witaj danych będą dostępne do odzyskania. |
| 4. |podane hasło szyfrowania Hello nie jest zgodna z hasłem skojarzonym z hello następującego serwera:**<server name>** |**Przyczyna:** hasło szyfrowania hello używane w procesie hello hello danych z serwera hello Azure kopii zapasowej danych są odzyskiwane szyfrowania jest niezgodny z podane hasło szyfrowania hello. Hello agent jest toodecrypt hello danych. Dlatego hello odzyskiwanie zakończy się niepowodzeniem.<br>**Rozwiązanie:** Podaj hello dokładnie tego samego szyfrowania hasło skojarzone z hello Azure Utwórz kopię zapasową serwera, którego dane są odzyskiwane. |

## <a name="frequently-asked-questions"></a>Często zadawane pytania

### <a name="why-cant-i-add-an-external-dpm-server-after-installing-ur7-and-latest-azure-backup-agent"></a>Dlaczego nie można dodać zewnętrznego serwera programu DPM po zainstalowaniu pakietu zbiorczego aktualizacji 7 i najnowsza wersja agenta usługi Kopia zapasowa Azure?

Dla hello serwerów programu DPM ze źródłami danych, które są chronione toohello chmury (za pomocą pakietu zbiorczego aktualizacji starsze niż pakiet zbiorczy aktualizacji 7), musisz poczekać co najmniej jeden dzień po zainstalowaniu pakietu zbiorczego aktualizacji 7 hello i najnowsza wersja agenta usługi Kopia zapasowa Azure, toostart **serwera dodawania zewnętrznego programu DPM** . Witaj jeden dzień okres czasu jest tooupload wymagane metadane hello tooAzure grup ochrony programu DPM hello. Przekazaniu metadanych grupy ochrony hello za pośrednictwem nocne zadanie po raz pierwszy.

### <a name="what-is-hello-minimum-version-of-hello-microsoft-azure-recovery-services-agent-needed"></a>Co to jest hello minimalnej wersji agenta usług odzyskiwania Microsoft Azure hello potrzebne?

Minimalna wersja agenta usług odzyskiwania Microsoft Azure hello lub agenta usługi Kopia zapasowa Azure, wymagane tooenable Hello ta funkcja jest 2.0.8719.0.  Wersja agenta hello tooview: Otwórz Panel sterowania  **>**  elementy Panelu sterowania wszystkie  **>**  programy i funkcje  **>**  Agent usług odzyskiwania Microsoft Azure. Jeśli wersja hello jest mniejsza niż 2.0.8719.0, Pobierz i zainstaluj hello [najnowsza wersja agenta usługi Kopia zapasowa Azure](https://go.microsoft.com/fwLink/?LinkID=288905).

![Wyczyść zewnętrzny program DPM](./media/backup-azure-alternate-dpm-server/external-dpm-azurebackupagentversion.png)

## <a name="next-steps"></a>Następne kroki:
• [Azure często zadawane pytania dotyczące tworzenia kopii zapasowej](backup-azure-backup-faq.md)
