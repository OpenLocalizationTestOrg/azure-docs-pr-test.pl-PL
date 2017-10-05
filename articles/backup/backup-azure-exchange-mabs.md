---
title: "Utwórz kopię zapasową serwera programu Exchange do usługi Kopia zapasowa Azure serwer kopii zapasowej Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wykonać kopię zapasową serwera Exchange, kopia zapasowa Azure za pomocą serwera usługi Kopia zapasowa Azure"
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
ms.openlocfilehash: 60b784fd00013c2b9504f8635c6b5c4c592563be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-azure-backup-server"></a><span data-ttu-id="c257e-103">Wykonywanie kopii zapasowej serwera Exchange kopia zapasowa Azure z serwerem kopia zapasowa Azure</span><span class="sxs-lookup"><span data-stu-id="c257e-103">Back up an Exchange server to Azure Backup with Azure Backup Server</span></span>
<span data-ttu-id="c257e-104">W tym artykule opisano sposób konfigurowania programu Microsoft Azure kopii zapasowej serwera (MABS) aby utworzyć kopię zapasową Microsoft Exchange server na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c257e-104">This article describes how to configure Microsoft Azure Backup Server (MABS) to back up a Microsoft Exchange server to Azure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="c257e-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c257e-105">Prerequisites</span></span>
<span data-ttu-id="c257e-106">Przed kontynuowaniem upewnij się, że serwer kopii zapasowej Azure jest [zainstalowany i przygotowane](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="c257e-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="c257e-107">Agent ochrony MABS</span><span class="sxs-lookup"><span data-stu-id="c257e-107">MABS protection agent</span></span>
<span data-ttu-id="c257e-108">Aby zainstalować agenta ochrony MABS na serwerze programu Exchange, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c257e-108">To install the MABS protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="c257e-109">Upewnij się, że zapory są poprawnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="c257e-109">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="c257e-110">Zobacz [skonfigurowania wyjątków zapory dla agenta](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="c257e-110">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="c257e-111">Zainstaluj agenta na serwerze programu Exchange, klikając **zarządzania > agentów > Zainstaluj** w konsoli administratora MABS.</span><span class="sxs-lookup"><span data-stu-id="c257e-111">Install the agent on the Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="c257e-112">Zobacz [zainstalować agenta ochrony MABS](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) szczegółowy opis kroków.</span><span class="sxs-lookup"><span data-stu-id="c257e-112">See [Install the MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="c257e-113">Utwórz grupę ochrony dla serwera Exchange</span><span class="sxs-lookup"><span data-stu-id="c257e-113">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="c257e-114">W konsoli administratora MABS kliknij **ochrony**, a następnie kliknij przycisk **nowy** na wstążce narzędzi, aby otworzyć **tworzenia nowej grupy ochrony** kreatora.</span><span class="sxs-lookup"><span data-stu-id="c257e-114">In the MABS Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="c257e-115">Na **powitalnej** ekranu kliknij kreatora **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c257e-115">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="c257e-116">Na **wybierz typ grupy ochrony** wybierz **serwerów** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c257e-116">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="c257e-117">Wybierz bazy danych serwera Exchange, który chcesz chronić, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c257e-117">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c257e-118">W przypadku ochrony programu Exchange 2013 Sprawdź [wymagania wstępne programu Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="c257e-118">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="c257e-119">W poniższym przykładzie wybrano bazy danych programu Exchange 2010.</span><span class="sxs-lookup"><span data-stu-id="c257e-119">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Wybierz członków grupy](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="c257e-121">Wybierz metodę ochrony danych.</span><span class="sxs-lookup"><span data-stu-id="c257e-121">Select the data protection method.</span></span>

    <span data-ttu-id="c257e-122">Określ nazwę grupy ochrony, a następnie wybierz oba z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="c257e-122">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="c257e-123">Chcę uzyskać krótkoterminową ochronę za pomocą dysku.</span><span class="sxs-lookup"><span data-stu-id="c257e-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="c257e-124">Chcę uzyskać ochronę online.</span><span class="sxs-lookup"><span data-stu-id="c257e-124">I want online protection.</span></span>
6. <span data-ttu-id="c257e-125">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="c257e-125">Click **Next**.</span></span>
7. <span data-ttu-id="c257e-126">Wybierz **Uruchom program Eseutil, aby sprawdzić spójność danych** opcję, jeśli chcesz sprawdzić spójność baz danych programu Exchange Server.</span><span class="sxs-lookup"><span data-stu-id="c257e-126">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="c257e-127">Po wybraniu tej opcji sprawdzania spójności kopii zapasowej jest uruchamiane MABS, aby uniknąć ruch we/wy, który jest generowany przez uruchomienie **eseutil** polecenia na serwerze Exchange.</span><span class="sxs-lookup"><span data-stu-id="c257e-127">After you select this option, backup consistency checking will be run on MABS to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c257e-128">Aby użyć tej opcji, należy skopiować pliki Ese.dll i Eseutil.exe do katalogu C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin na serwerze MAB.</span><span class="sxs-lookup"><span data-stu-id="c257e-128">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on the MAB server.</span></span> <span data-ttu-id="c257e-129">W przeciwnym razie zostanie wywołany następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="c257e-129">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="c257e-130">![Błąd Eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="c257e-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="c257e-131">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="c257e-131">Click **Next**.</span></span>
9. <span data-ttu-id="c257e-132">Wybierz bazę danych dla **kopii zapasowej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c257e-132">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c257e-133">Jeśli nie zostanie wybrana opcja "Pełnej kopii zapasowej" dla co najmniej jednej grupy DAG kopii bazy danych, dzienniki nie zostaną obcięte.</span><span class="sxs-lookup"><span data-stu-id="c257e-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="c257e-134">Konfigurowanie celów dla **krótkoterminowych kopii zapasowych**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c257e-134">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="c257e-135">Przejrzyj dostępne miejsce na dysku, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c257e-135">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="c257e-136">Określ czas, jaką serwera MAB będzie utworzyć replikacji początkowej, a następnie kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c257e-136">Select the time at which the MAB Server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="c257e-137">Wybierz opcje sprawdzania spójności, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c257e-137">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="c257e-138">Wybierz bazę danych, który chcesz utworzyć kopię zapasową na platformie Azure, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c257e-138">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="c257e-139">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c257e-139">For example:</span></span>

    ![Określ dane chronione w trybie online](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="c257e-141">Zdefiniuj harmonogram **kopia zapasowa Azure**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c257e-141">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="c257e-142">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c257e-142">For example:</span></span>

    ![Określ harmonogram tworzenia kopii zapasowej online](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="c257e-144">Należy pamiętać, punkty odzyskiwania Online są na podstawie ekspresowego pełnego punktów odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="c257e-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="c257e-145">W związku z tym musisz zaplanować punktu odzyskiwania online po punktu odzyskiwania w czasie określonym dla ekspresowej pełnej.</span><span class="sxs-lookup"><span data-stu-id="c257e-145">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="c257e-146">Konfigurowanie zasad przechowywania dla **kopia zapasowa Azure**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c257e-146">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="c257e-147">Wybierz opcję replikacji online, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c257e-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="c257e-148">Jeśli masz dużą bazy danych, może upłynąć długo początkowa kopia zapasowa ma zostać utworzony za pośrednictwem sieci.</span><span class="sxs-lookup"><span data-stu-id="c257e-148">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="c257e-149">Aby uniknąć tego problemu, można utworzyć kopię zapasową offline.</span><span class="sxs-lookup"><span data-stu-id="c257e-149">To avoid this issue, you can create an offline backup.</span></span>  

    ![Określ zasady przechowywania danych online](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="c257e-151">Potwierdź ustawienia, a następnie kliknij przycisk **Utwórz grupę**.</span><span class="sxs-lookup"><span data-stu-id="c257e-151">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="c257e-152">Kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="c257e-152">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="c257e-153">Odzyskiwanie bazy danych programu Exchange</span><span class="sxs-lookup"><span data-stu-id="c257e-153">Recover the Exchange database</span></span>
1. <span data-ttu-id="c257e-154">Aby odzyskać bazy danych programu Exchange, kliknij **odzyskiwania** w konsoli administratora MABS.</span><span class="sxs-lookup"><span data-stu-id="c257e-154">To recover an Exchange database, click **Recovery** in the MABS Administrator Console.</span></span>
2. <span data-ttu-id="c257e-155">Zlokalizuj bazy danych programu Exchange, który chcesz odzyskać.</span><span class="sxs-lookup"><span data-stu-id="c257e-155">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="c257e-156">Wybierz punkt odzyskiwania online z *czasu odzyskiwania* listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="c257e-156">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="c257e-157">Kliknij przycisk **odzyskać** uruchomić **Kreatora odzyskiwania**.</span><span class="sxs-lookup"><span data-stu-id="c257e-157">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="c257e-158">Punkty odzyskiwania online są pięć typów odzyskiwania:</span><span class="sxs-lookup"><span data-stu-id="c257e-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="c257e-159">**Odzyskaj do oryginalnej lokalizacji serwera Exchange:** dane zostaną odzyskane na oryginalnym serwerze Exchange.</span><span class="sxs-lookup"><span data-stu-id="c257e-159">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="c257e-160">**Odzyskaj do innej bazy danych serwera Exchange:** dane zostaną odzyskane do innej bazy danych na innym serwerze programu Exchange.</span><span class="sxs-lookup"><span data-stu-id="c257e-160">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="c257e-161">**Odzyskaj do bazy danych odzyskiwania:** dane zostaną odzyskane do bazy danych odzyskiwania programu Exchange (RDB).</span><span class="sxs-lookup"><span data-stu-id="c257e-161">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="c257e-162">**Kopiuj do folderu sieciowego:** dane zostaną odzyskane do folderu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="c257e-162">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="c257e-163">**Kopiuj na taśmę:** Jeśli biblioteka taśm lub autonomiczna stacja taśm dołączonych i skonfigurowane na MABS, punkt odzyskiwania zostanie skopiowana do wolnej taśmy.</span><span class="sxs-lookup"><span data-stu-id="c257e-163">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, the recovery point will be copied to a free tape.</span></span>

    ![Wybierz opcję replikacji online](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="c257e-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c257e-165">Next steps</span></span>
* [<span data-ttu-id="c257e-166">Azure — często zadawane pytania kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="c257e-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
