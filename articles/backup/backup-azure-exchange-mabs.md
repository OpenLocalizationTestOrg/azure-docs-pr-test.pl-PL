---
title: "aaaBack zapasową programu Exchange server tooAzure kopii zapasowej z serwera usługi Azure Backup | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooback zapasową programu Exchange server tooAzure kopii zapasowej za pomocą serwera usługi Kopia zapasowa Azure"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: e46557e8-2eaf-4ee0-99ea-00fbb8687dca
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: db874161151fc57c5b79c41531e18d577f567f66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a>Wykonaj kopię zapasową programu Exchange server tooAzure kopii zapasowej z serwera usługi Kopia zapasowa Azure
W tym artykule opisano sposób tooback Microsoft Azure kopii zapasowej serwera (MABS) tooconfigure się tooAzure serwera Microsoft Exchange.  

## <a name="prerequisites"></a>Wymagania wstępne
Przed kontynuowaniem upewnij się, że serwer kopii zapasowej Azure jest [zainstalowany i przygotowane](backup-azure-microsoft-azure-backup.md).

## <a name="mabs-protection-agent"></a>Agent ochrony MABS
agent ochrony MABS hello tooinstall na powitania serwera Exchange, wykonaj następujące kroki:

1. Upewnij się, czy zapory hello są poprawnie skonfigurowane. Zobacz [skonfigurowania wyjątków zapory dla agenta hello](https://technet.microsoft.com/library/Hh758204.aspx).
2. Zainstaluj agenta hello na powitania serwera Exchange, klikając **zarządzania > agentów > Zainstaluj** w konsoli administratora MABS. Zobacz [agenta ochrony MABS hello instalacji](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) szczegółowy opis kroków.

## <a name="create-a-protection-group-for-hello-exchange-server"></a>Utwórz grupę ochrony dla hello programu Exchange server
1. W konsoli administratora MABS hello, kliknij przycisk **ochrony**, a następnie kliknij przycisk **nowy** na powitania narzędzia wstążki tooopen hello **tworzenia nowej grupy ochrony** kreatora.
2. Na powitania **powitalnej** ekranie powitania kreatora kliknij **dalej**.
3. Na powitania **wybierz typ grupy ochrony** wybierz **serwerów** i kliknij przycisk **dalej**.
4. Wybierz hello bazy danych serwera Exchange mają tooprotect, a następnie kliknij przycisk **dalej**.

   > [!NOTE]
   > W przypadku ochrony programu Exchange 2013 Sprawdź hello [wymagania wstępne programu Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).
   >
   >

    W hello poniższy przykład bazy danych programu Exchange 2010 hello jest zaznaczone.

    ![Wybierz członków grupy](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. Wybierz metodę ochrony danych hello.

    Nazwa grupy ochrony hello, a następnie wybierz oba hello następujące opcje:

   * Chcę uzyskać krótkoterminową ochronę za pomocą dysku.
   * Chcę uzyskać ochronę online.
6. Kliknij przycisk **Dalej**.
7. Wybierz hello **integralność danych uruchom program Eseutil toocheck** opcję, jeśli chcesz, aby toocheck hello integralność bazy danych programu Exchange Server hello.

    Po wybraniu tej opcji sprawdzania spójności kopii zapasowej jest uruchamiane MABS tooavoid hello we/wy ruchu generowanego przez uruchomienie hello **eseutil** na powitania serwera Exchange.

   > [!NOTE]
   > toouse tę opcję, należy skopiować hello Ese.dll i Eseutil.exe katalogu C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin toohello plików na serwerze MAB hello. W przeciwnym razie zostanie wywołany hello następujący błąd:  
   > ![Błąd Eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)
   >
   >
8. Kliknij przycisk **Dalej**.
9. Bazy danych wybierz hello **kopii zapasowej**, a następnie kliknij przycisk **dalej**.

   > [!NOTE]
   > Jeśli nie zostanie wybrana opcja "Pełnej kopii zapasowej" dla co najmniej jednej grupy DAG kopii bazy danych, dzienniki nie zostaną obcięte.
   >
   >
10. Konfigurowanie celów powitania dla **krótkoterminowych kopii zapasowych**, a następnie kliknij przycisk **dalej**.
11. Przejrzyj hello dostępnego miejsca na dysku, a następnie kliknij przycisk **dalej**.
12. Wybierz czas hello, w których hello MAB serwera będzie utworzyć hello replikacji początkowej, a następnie kliknij **dalej**.
13. Wybierz opcje sprawdzania spójności hello, a następnie kliknij przycisk **dalej**.
14. Wybierz bazę danych hello, mają tooback się tooAzure, a następnie kliknij przycisk **dalej**. Na przykład:

    ![Określ dane chronione w trybie online](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. Zdefiniuj harmonogram hello **kopia zapasowa Azure**, a następnie kliknij przycisk **dalej**. Na przykład:

    ![Określ harmonogram tworzenia kopii zapasowej online](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > Należy pamiętać, punkty odzyskiwania Online są na podstawie ekspresowego pełnego punktów odzyskiwania. W związku z tym należy zaplanować punktu odzyskiwania online powitania po hello czasie określonym dla hello express punktu odzyskiwania pełnego.
    >
    >
16. Konfigurowanie zasad przechowywania hello **kopia zapasowa Azure**, a następnie kliknij przycisk **dalej**.
17. Wybierz opcję replikacji online, a następnie kliknij przycisk **dalej**.

    Jeśli masz dużą bazy danych, może upłynąć długo hello początkowej toobe kopii zapasowej utworzone za pośrednictwem sieci hello. tooavoid ten problem, można utworzyć kopię zapasową offline.  

    ![Określ zasady przechowywania danych online](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. Potwierdź ustawienia hello, a następnie kliknij przycisk **Utwórz grupę**.
19. Kliknij przycisk **Zamknij**.

## <a name="recover-hello-exchange-database"></a>Odzyskiwanie bazy danych programu Exchange hello
1. Kliknij przycisk toorecover bazy danych programu Exchange **odzyskiwania** w konsoli administratora MABS hello.
2. Zlokalizuj bazę danych programu Exchange hello, które mają toorecover.
3. Wybierz punkt odzyskiwania online z hello *czasu odzyskiwania* listy rozwijanej.
4. Kliknij przycisk **odzyskać** toostart hello **Kreatora odzyskiwania**.

Punkty odzyskiwania online są pięć typów odzyskiwania:

* **Odzyskiwanie lokalizacji serwera Exchange toooriginal:** hello dane zostaną odzyskane toohello oryginalny serwer programu Exchange.
* **Odzyskiwanie bazy danych tooanother na serwerze programu Exchange:** hello dane zostaną odzyskane tooanother bazy danych, na innym serwerze programu Exchange.
* **Odzyskiwanie bazy danych odzyskiwania tooa:** hello dane zostaną odzyskane tooan Exchange bazy danych odzyskiwania (RDB).
* **Folderu sieciowego tooa kopiowania:** hello dane zostaną odzyskane tooa folderu sieciowego.
* **Skopiuj tootape:** Jeśli biblioteka taśm lub autonomiczna stacja taśm MABS dołączona i skonfigurowane na powitania punkt odzyskiwania zostanie skopiowana tooa wolnej taśmy.

    ![Wybierz opcję replikacji online](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a>Następne kroki
* [Azure — często zadawane pytania kopii zapasowej](backup-azure-backup-faq.md)
