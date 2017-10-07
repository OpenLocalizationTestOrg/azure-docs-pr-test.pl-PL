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
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a><span data-ttu-id="3db1c-103">Wykonaj kopię zapasową programu Exchange server tooAzure kopii zapasowej z serwera usługi Kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="3db1c-103">Back up an Exchange server tooAzure Backup with Azure Backup Server</span></span>
<span data-ttu-id="3db1c-104">W tym artykule opisano sposób tooback Microsoft Azure kopii zapasowej serwera (MABS) tooconfigure się tooAzure serwera Microsoft Exchange.</span><span class="sxs-lookup"><span data-stu-id="3db1c-104">This article describes how tooconfigure Microsoft Azure Backup Server (MABS) tooback up a Microsoft Exchange server tooAzure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="3db1c-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3db1c-105">Prerequisites</span></span>
<span data-ttu-id="3db1c-106">Przed kontynuowaniem upewnij się, że serwer kopii zapasowej Azure jest [zainstalowany i przygotowane](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="3db1c-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="3db1c-107">Agent ochrony MABS</span><span class="sxs-lookup"><span data-stu-id="3db1c-107">MABS protection agent</span></span>
<span data-ttu-id="3db1c-108">agent ochrony MABS hello tooinstall na powitania serwera Exchange, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="3db1c-108">tooinstall hello MABS protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="3db1c-109">Upewnij się, czy zapory hello są poprawnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="3db1c-109">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="3db1c-110">Zobacz [skonfigurowania wyjątków zapory dla agenta hello](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="3db1c-110">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="3db1c-111">Zainstaluj agenta hello na powitania serwera Exchange, klikając **zarządzania > agentów > Zainstaluj** w konsoli administratora MABS.</span><span class="sxs-lookup"><span data-stu-id="3db1c-111">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="3db1c-112">Zobacz [agenta ochrony MABS hello instalacji](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) szczegółowy opis kroków.</span><span class="sxs-lookup"><span data-stu-id="3db1c-112">See [Install hello MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="3db1c-113">Utwórz grupę ochrony dla hello programu Exchange server</span><span class="sxs-lookup"><span data-stu-id="3db1c-113">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="3db1c-114">W konsoli administratora MABS hello, kliknij przycisk **ochrony**, a następnie kliknij przycisk **nowy** na powitania narzędzia wstążki tooopen hello **tworzenia nowej grupy ochrony** kreatora.</span><span class="sxs-lookup"><span data-stu-id="3db1c-114">In hello MABS Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="3db1c-115">Na powitania **powitalnej** ekranie powitania kreatora kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-115">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="3db1c-116">Na powitania **wybierz typ grupy ochrony** wybierz **serwerów** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-116">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="3db1c-117">Wybierz hello bazy danych serwera Exchange mają tooprotect, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-117">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3db1c-118">W przypadku ochrony programu Exchange 2013 Sprawdź hello [wymagania wstępne programu Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="3db1c-118">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="3db1c-119">W hello poniższy przykład bazy danych programu Exchange 2010 hello jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="3db1c-119">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![Wybierz członków grupy](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="3db1c-121">Wybierz metodę ochrony danych hello.</span><span class="sxs-lookup"><span data-stu-id="3db1c-121">Select hello data protection method.</span></span>

    <span data-ttu-id="3db1c-122">Nazwa grupy ochrony hello, a następnie wybierz oba hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="3db1c-122">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="3db1c-123">Chcę uzyskać krótkoterminową ochronę za pomocą dysku.</span><span class="sxs-lookup"><span data-stu-id="3db1c-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="3db1c-124">Chcę uzyskać ochronę online.</span><span class="sxs-lookup"><span data-stu-id="3db1c-124">I want online protection.</span></span>
6. <span data-ttu-id="3db1c-125">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-125">Click **Next**.</span></span>
7. <span data-ttu-id="3db1c-126">Wybierz hello **integralność danych uruchom program Eseutil toocheck** opcję, jeśli chcesz, aby toocheck hello integralność bazy danych programu Exchange Server hello.</span><span class="sxs-lookup"><span data-stu-id="3db1c-126">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="3db1c-127">Po wybraniu tej opcji sprawdzania spójności kopii zapasowej jest uruchamiane MABS tooavoid hello we/wy ruchu generowanego przez uruchomienie hello **eseutil** na powitania serwera Exchange.</span><span class="sxs-lookup"><span data-stu-id="3db1c-127">After you select this option, backup consistency checking will be run on MABS tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3db1c-128">toouse tę opcję, należy skopiować hello Ese.dll i Eseutil.exe katalogu C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin toohello plików na serwerze MAB hello.</span><span class="sxs-lookup"><span data-stu-id="3db1c-128">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on hello MAB server.</span></span> <span data-ttu-id="3db1c-129">W przeciwnym razie zostanie wywołany hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="3db1c-129">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="3db1c-130">![Błąd Eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="3db1c-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="3db1c-131">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-131">Click **Next**.</span></span>
9. <span data-ttu-id="3db1c-132">Bazy danych wybierz hello **kopii zapasowej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-132">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3db1c-133">Jeśli nie zostanie wybrana opcja "Pełnej kopii zapasowej" dla co najmniej jednej grupy DAG kopii bazy danych, dzienniki nie zostaną obcięte.</span><span class="sxs-lookup"><span data-stu-id="3db1c-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="3db1c-134">Konfigurowanie celów powitania dla **krótkoterminowych kopii zapasowych**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-134">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="3db1c-135">Przejrzyj hello dostępnego miejsca na dysku, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-135">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="3db1c-136">Wybierz czas hello, w których hello MAB serwera będzie utworzyć hello replikacji początkowej, a następnie kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-136">Select hello time at which hello MAB Server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="3db1c-137">Wybierz opcje sprawdzania spójności hello, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-137">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="3db1c-138">Wybierz bazę danych hello, mają tooback się tooAzure, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-138">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="3db1c-139">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="3db1c-139">For example:</span></span>

    ![Określ dane chronione w trybie online](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="3db1c-141">Zdefiniuj harmonogram hello **kopia zapasowa Azure**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-141">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="3db1c-142">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="3db1c-142">For example:</span></span>

    ![Określ harmonogram tworzenia kopii zapasowej online](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="3db1c-144">Należy pamiętać, punkty odzyskiwania Online są na podstawie ekspresowego pełnego punktów odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="3db1c-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="3db1c-145">W związku z tym należy zaplanować punktu odzyskiwania online powitania po hello czasie określonym dla hello express punktu odzyskiwania pełnego.</span><span class="sxs-lookup"><span data-stu-id="3db1c-145">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="3db1c-146">Konfigurowanie zasad przechowywania hello **kopia zapasowa Azure**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-146">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="3db1c-147">Wybierz opcję replikacji online, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="3db1c-148">Jeśli masz dużą bazy danych, może upłynąć długo hello początkowej toobe kopii zapasowej utworzone za pośrednictwem sieci hello.</span><span class="sxs-lookup"><span data-stu-id="3db1c-148">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="3db1c-149">tooavoid ten problem, można utworzyć kopię zapasową offline.</span><span class="sxs-lookup"><span data-stu-id="3db1c-149">tooavoid this issue, you can create an offline backup.</span></span>  

    ![Określ zasady przechowywania danych online](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="3db1c-151">Potwierdź ustawienia hello, a następnie kliknij przycisk **Utwórz grupę**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-151">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="3db1c-152">Kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-152">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="3db1c-153">Odzyskiwanie bazy danych programu Exchange hello</span><span class="sxs-lookup"><span data-stu-id="3db1c-153">Recover hello Exchange database</span></span>
1. <span data-ttu-id="3db1c-154">Kliknij przycisk toorecover bazy danych programu Exchange **odzyskiwania** w konsoli administratora MABS hello.</span><span class="sxs-lookup"><span data-stu-id="3db1c-154">toorecover an Exchange database, click **Recovery** in hello MABS Administrator Console.</span></span>
2. <span data-ttu-id="3db1c-155">Zlokalizuj bazę danych programu Exchange hello, które mają toorecover.</span><span class="sxs-lookup"><span data-stu-id="3db1c-155">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="3db1c-156">Wybierz punkt odzyskiwania online z hello *czasu odzyskiwania* listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="3db1c-156">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="3db1c-157">Kliknij przycisk **odzyskać** toostart hello **Kreatora odzyskiwania**.</span><span class="sxs-lookup"><span data-stu-id="3db1c-157">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="3db1c-158">Punkty odzyskiwania online są pięć typów odzyskiwania:</span><span class="sxs-lookup"><span data-stu-id="3db1c-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="3db1c-159">**Odzyskiwanie lokalizacji serwera Exchange toooriginal:** hello dane zostaną odzyskane toohello oryginalny serwer programu Exchange.</span><span class="sxs-lookup"><span data-stu-id="3db1c-159">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="3db1c-160">**Odzyskiwanie bazy danych tooanother na serwerze programu Exchange:** hello dane zostaną odzyskane tooanother bazy danych, na innym serwerze programu Exchange.</span><span class="sxs-lookup"><span data-stu-id="3db1c-160">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="3db1c-161">**Odzyskiwanie bazy danych odzyskiwania tooa:** hello dane zostaną odzyskane tooan Exchange bazy danych odzyskiwania (RDB).</span><span class="sxs-lookup"><span data-stu-id="3db1c-161">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="3db1c-162">**Folderu sieciowego tooa kopiowania:** hello dane zostaną odzyskane tooa folderu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="3db1c-162">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="3db1c-163">**Skopiuj tootape:** Jeśli biblioteka taśm lub autonomiczna stacja taśm MABS dołączona i skonfigurowane na powitania punkt odzyskiwania zostanie skopiowana tooa wolnej taśmy.</span><span class="sxs-lookup"><span data-stu-id="3db1c-163">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, hello recovery point will be copied tooa free tape.</span></span>

    ![Wybierz opcję replikacji online](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="3db1c-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3db1c-165">Next steps</span></span>
* [<span data-ttu-id="3db1c-166">Azure — często zadawane pytania kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="3db1c-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
