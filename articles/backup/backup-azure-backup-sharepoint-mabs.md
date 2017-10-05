---
title: "Użyj serwera usługi Kopia zapasowa Azure, aby utworzyć kopię zapasową farmy programu SharePoint do platformy Azure | Dokumentacja firmy Microsoft"
description: "Serwer kopii zapasowej Azure umożliwia tworzenie kopii zapasowej i przywracanie danych programu SharePoint. Ten artykuł zawiera informacje, aby skonfigurować farmę programu SharePoint, tak aby żądanych danych mogą być przechowywane na platformie Azure. Chronione dane SharePoint można przywrócić z dysku lub z platformy Azure."
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: 34ba87a4-91f1-4054-a4a1-272af1e15496
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 3ed000affd326eb1bd7c99773ec021ad6e03cc3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-a-sharepoint-farm-to-azure"></a><span data-ttu-id="afc7d-105">Tworzenie kopii zapasowych farmy programu SharePoint na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="afc7d-105">Back up a SharePoint farm to Azure</span></span>
<span data-ttu-id="afc7d-106">Możesz utworzyć kopię zapasową farmy programu SharePoint do systemu Microsoft Azure przy użyciu usługi Microsoft Azure kopii zapasowej serwera (MABS) w znacznie tak samo jak wykonanie kopii zapasowej innych źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="afc7d-106">You back up a SharePoint farm to Microsoft Azure by using Microsoft Azure Backup Server (MABS) in much the same way that you back up other data sources.</span></span> <span data-ttu-id="afc7d-107">Kopia zapasowa Azure zapewnia elastyczność w harmonogram tworzenia kopii zapasowych, aby utworzyć codziennie, co tydzień, miesięcznego lub rocznego kopii zapasowej wskazuje i udostępnia opcje zasad przechowywania dla różnych punktów kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="afc7d-107">Azure Backup provides flexibility in the backup schedule to create daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="afc7d-108">Zapewnia także możliwość przechowywania kopii dysku lokalnym dla szybka celami czasu odzyskiwania (RTO) i Zapisz kopie Azure ekonomiczny, długoterminowego przechowywania.</span><span class="sxs-lookup"><span data-stu-id="afc7d-108">It also provides the capability to store local disk copies for quick recovery-time objectives (RTO) and to store copies to Azure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="afc7d-109">Obsługiwane wersje programu SharePoint, a powiązane scenariusze ochrony</span><span class="sxs-lookup"><span data-stu-id="afc7d-109">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="afc7d-110">Kopia zapasowa Azure dla programu DPM obsługuje następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="afc7d-110">Azure Backup for DPM supports the following scenarios:</span></span>

| <span data-ttu-id="afc7d-111">Obciążenie</span><span class="sxs-lookup"><span data-stu-id="afc7d-111">Workload</span></span> | <span data-ttu-id="afc7d-112">Wersja</span><span class="sxs-lookup"><span data-stu-id="afc7d-112">Version</span></span> | <span data-ttu-id="afc7d-113">Wdrażanie SharePoint</span><span class="sxs-lookup"><span data-stu-id="afc7d-113">SharePoint deployment</span></span> | <span data-ttu-id="afc7d-114">Ochrona i odzyskiwanie</span><span class="sxs-lookup"><span data-stu-id="afc7d-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="afc7d-115">Sharepoint</span><span class="sxs-lookup"><span data-stu-id="afc7d-115">SharePoint</span></span> |<span data-ttu-id="afc7d-116">SharePoint 2013, SharePoint programu SharePoint 2010, SharePoint 2007 3.0</span><span class="sxs-lookup"><span data-stu-id="afc7d-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="afc7d-117">SharePoint wdrożony jako serwer fizyczny lub maszyny wirtualnej funkcji Hyper-V/VMware</span><span class="sxs-lookup"><span data-stu-id="afc7d-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="afc7d-118">Funkcji SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="afc7d-118">SQL AlwaysOn</span></span> | <span data-ttu-id="afc7d-119">Ochrona opcje odzyskiwania farmy programu SharePoint: farmy odzyskiwania bazy danych i plik lub element listy z punktów odzyskiwania dysku.</span><span class="sxs-lookup"><span data-stu-id="afc7d-119">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="afc7d-120">Odzyskiwania farmy i bazy danych z punktów odzyskiwania systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="afc7d-120">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="afc7d-121">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="afc7d-121">Before you start</span></span>
<span data-ttu-id="afc7d-122">Istnieje kilka rzeczy, które trzeba upewnić się, aby wykonać kopię zapasową farmy programu SharePoint do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="afc7d-122">There are a few things you need to confirm before you back up a SharePoint farm to Azure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="afc7d-123">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="afc7d-123">Prerequisites</span></span>
<span data-ttu-id="afc7d-124">Przed kontynuowaniem upewnij się, że masz [zainstalowane i przygotować serwer kopii zapasowej Azure](backup-azure-microsoft-azure-backup.md) ochrony obciążeń.</span><span class="sxs-lookup"><span data-stu-id="afc7d-124">Before you proceed, make sure that you have [installed and prepared the Azure Backup Server](backup-azure-microsoft-azure-backup.md) to protect workloads.</span></span>

### <a name="protection-agent"></a><span data-ttu-id="afc7d-125">Agent ochrony</span><span class="sxs-lookup"><span data-stu-id="afc7d-125">Protection agent</span></span>
<span data-ttu-id="afc7d-126">Musi być zainstalowany agent ochrony na serwerze, który jest uruchomiony, SharePoint, serwery z programem SQL Server i wszystkich serwerów, które należą do farmy programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="afc7d-126">The Protection agent must be installed on the server that's running SharePoint, the servers that are running SQL Server, and all other servers that are part of the SharePoint farm.</span></span> <span data-ttu-id="afc7d-127">Aby uzyskać więcej informacji na temat sposobu konfigurowania agenta ochrony, zobacz [instalacji agenta ochrony](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span><span class="sxs-lookup"><span data-stu-id="afc7d-127">For more information about how to set up the protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="afc7d-128">Jedynym wyjątkiem jest, zainstaluj agenta tylko na jednym serwerze sieci web frontonu (WFE).</span><span class="sxs-lookup"><span data-stu-id="afc7d-128">The one exception is that you install the agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="afc7d-129">Program DPM wymaga agenta na jednym serwerze WFE tylko służy jako punkt wejścia do ochrony.</span><span class="sxs-lookup"><span data-stu-id="afc7d-129">DPM needs the agent on one WFE server only to serve as the entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="afc7d-130">Farma programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="afc7d-130">SharePoint farm</span></span>
<span data-ttu-id="afc7d-131">Dla każdych 10 milionów elementów w farmie musi istnieć co najmniej 2 GB miejsca na woluminie, w którym znajduje się MABS folder.</span><span class="sxs-lookup"><span data-stu-id="afc7d-131">For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the MABS folder is located.</span></span> <span data-ttu-id="afc7d-132">Ta przestrzeń jest wymagany do generowania katalogu.</span><span class="sxs-lookup"><span data-stu-id="afc7d-132">This space is required for catalog generation.</span></span> <span data-ttu-id="afc7d-133">W przypadku MABS odzyskać określone elementy (zbiory witryn, witryn listy, biblioteki dokumentów, foldery, pojedyncze dokumenty i elementy listy) generowania katalogu tworzy listę adresów URL, które są zawarte w każdej bazie danych zawartości.</span><span class="sxs-lookup"><span data-stu-id="afc7d-133">For MABS to recover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of the URLs that are contained within each content database.</span></span> <span data-ttu-id="afc7d-134">Można wyświetlić listę adresów URL w okienku elementy możliwe do odzyskania w **odzyskiwania** obszarze Konsola administratora MABS zadań.</span><span class="sxs-lookup"><span data-stu-id="afc7d-134">You can view the list of URLs in the recoverable item pane in the **Recovery** task area of MABS Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="afc7d-135">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="afc7d-135">SQL Server</span></span>
<span data-ttu-id="afc7d-136">MABS działa jako konto systemu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="afc7d-136">MABS runs as a LocalSystem account.</span></span> <span data-ttu-id="afc7d-137">Aby utworzyć kopię zapasową bazy danych programu SQL Server, MABS wymaga uprawnień administratora na tym koncie dla serwera, na którym działa program SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afc7d-137">To back up SQL Server databases, MABS needs sysadmin privileges on that account for the server that's running SQL Server.</span></span> <span data-ttu-id="afc7d-138">Ustaw Zarządzanie NT\System *sysadmin* na serwerze, na którym działa program SQL Server przed jego kopię zapasową.</span><span class="sxs-lookup"><span data-stu-id="afc7d-138">Set NT AUTHORITY\SYSTEM to *sysadmin* on the server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="afc7d-139">Jeśli farma programu SharePoint zawiera bazy danych programu SQL Server, które skonfigurowano z aliasami programu SQL Server, należy zainstalować składniki klienta programu SQL Server na serwerze frontonu sieci Web, które będzie chronione MABS.</span><span class="sxs-lookup"><span data-stu-id="afc7d-139">If the SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front-end Web server that MABS will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="afc7d-140">Oprogramowanie SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="afc7d-140">SharePoint Server</span></span>
<span data-ttu-id="afc7d-141">Gdy wydajność zależy od wielu czynników, takich jak rozmiar farmy programu SharePoint, stanowią ogólne wskazówki MABS jeden może chronić farmy programu SharePoint 25 TB.</span><span class="sxs-lookup"><span data-stu-id="afc7d-141">While performance depends on many factors such as size of SharePoint farm, as general guidance one MABS can protect a 25 TB SharePoint farm.</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="afc7d-142">Jakie operacje nie są obsługiwane</span><span class="sxs-lookup"><span data-stu-id="afc7d-142">What's not supported</span></span>
* <span data-ttu-id="afc7d-143">MABS, który zapewnia ochronę farmy programu SharePoint nie chroni indeksy wyszukiwania lub bazy danych aplikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="afc7d-143">MABS that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="afc7d-144">Należy skonfigurować osobno ochrony tych baz danych.</span><span class="sxs-lookup"><span data-stu-id="afc7d-144">You will need to configure the protection of these databases separately.</span></span>
* <span data-ttu-id="afc7d-145">MABS nie ma kopii zapasowej baz danych serwera SQL programu SharePoint, które znajdują się w udziałach serwera (SOFS) plików skalowalnego w poziomie.</span><span class="sxs-lookup"><span data-stu-id="afc7d-145">MABS does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="afc7d-146">Konfigurowanie ochrony programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="afc7d-146">Configure SharePoint protection</span></span>
<span data-ttu-id="afc7d-147">Przed MABS można użyć do ochrony programu SharePoint, należy skonfigurować usługę składnika zapisywania usługi VSS programu SharePoint (usługa składnika zapisywania programu WSS) przy użyciu **ConfigureSharePoint.exe**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-147">Before you can use MABS to protect SharePoint, you must configure the SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="afc7d-148">Można znaleźć **ConfigureSharePoint.exe** w folderze \bin [ścieżka instalacji MABS] na serwerze frontonu sieci web.</span><span class="sxs-lookup"><span data-stu-id="afc7d-148">You can find **ConfigureSharePoint.exe** in the [MABS Installation Path]\bin folder on the front-end web server.</span></span> <span data-ttu-id="afc7d-149">To narzędzie udostępnia agentowi ochrony poświadczenia farmy programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="afc7d-149">This tool provides the protection agent with the credentials for the SharePoint farm.</span></span> <span data-ttu-id="afc7d-150">Możesz uruchomić na jednym serwerze WFE.</span><span class="sxs-lookup"><span data-stu-id="afc7d-150">You run it on a single WFE server.</span></span> <span data-ttu-id="afc7d-151">Jeśli masz wiele serwerów WFE, należy wybrać jeden z nich podczas konfigurowania grupy ochrony.</span><span class="sxs-lookup"><span data-stu-id="afc7d-151">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="to-configure-the-sharepoint-vss-writer-service"></a><span data-ttu-id="afc7d-152">Aby skonfigurować usługę składnika zapisywania usługi VSS programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="afc7d-152">To configure the SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="afc7d-153">Na serwerze WFE, w wierszu polecenia przejdź do \bin\ [Lokalizacja instalacji MABS]</span><span class="sxs-lookup"><span data-stu-id="afc7d-153">On the WFE server, at a command prompt, go to [MABS installation location]\bin\\</span></span>
2. <span data-ttu-id="afc7d-154">Wprowadź ConfigureSharePoint - EnableSharePointProtection.</span><span class="sxs-lookup"><span data-stu-id="afc7d-154">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="afc7d-155">Wprowadź poświadczenia administratora farmy.</span><span class="sxs-lookup"><span data-stu-id="afc7d-155">Enter the farm administrator credentials.</span></span> <span data-ttu-id="afc7d-156">To konto powinno być członkiem lokalnej grupy administratorów na serwerze WFE.</span><span class="sxs-lookup"><span data-stu-id="afc7d-156">This account should be a member of the local Administrator group on the WFE server.</span></span> <span data-ttu-id="afc7d-157">Jeśli administrator farmy nie jest lokalnym administratorem Przyznaj poniższe uprawnienia na serwerze WFE:</span><span class="sxs-lookup"><span data-stu-id="afc7d-157">If the farm administrator isn’t a local admin grant the following permissions on the WFE server:</span></span>
   * <span data-ttu-id="afc7d-158">Przyznaj grupie WSS_ADMIN_WPG uprawnienia Pełna kontrola do folderu programu DPM (% Program Files%\Microsoft Azure Backup\DPM).</span><span class="sxs-lookup"><span data-stu-id="afc7d-158">Grant the WSS_Admin_WPG group full control to the DPM folder (%Program Files%\Microsoft Azure Backup\DPM).</span></span>
   * <span data-ttu-id="afc7d-159">Przyznaj grupie WSS_ADMIN_WPG uprawnienia odczytu do klucza rejestru programu DPM (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span><span class="sxs-lookup"><span data-stu-id="afc7d-159">Grant the WSS_Admin_WPG group read access to the DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="afc7d-160">Musisz ponownie uruchomić ConfigureSharePoint.exe, gdy istnieje zmiana poświadczeń administratora farmy programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="afc7d-160">You’ll need to rerun ConfigureSharePoint.exe whenever there’s a change in the SharePoint farm administrator credentials.</span></span>
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a><span data-ttu-id="afc7d-161">Kopii zapasowej farmy programu SharePoint za pomocą MABS</span><span class="sxs-lookup"><span data-stu-id="afc7d-161">Back up a SharePoint farm by using MABS</span></span>
<span data-ttu-id="afc7d-162">Po skonfigurowaniu MABS i farmy programu SharePoint, jak opisano wcześniej, SharePoint mogą być chronione przez MABS.</span><span class="sxs-lookup"><span data-stu-id="afc7d-162">After you have configured MABS and the SharePoint farm as explained previously, SharePoint can be protected by MABS.</span></span>

### <a name="to-protect-a-sharepoint-farm"></a><span data-ttu-id="afc7d-163">Aby chronić farmy programu SharePoint</span><span class="sxs-lookup"><span data-stu-id="afc7d-163">To protect a SharePoint farm</span></span>
1. <span data-ttu-id="afc7d-164">Z **ochrony** kartę w konsoli administratora MABS, kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-164">From the **Protection** tab of the MABS Administrator Console, click **New**.</span></span>
    <span data-ttu-id="afc7d-165">![Nowa karta ochrony](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="afc7d-165">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="afc7d-166">Na **wybierz typ grupy ochrony** strony **tworzenia nowej grupy ochrony** kreatora, zaznacz **serwerów**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-166">On the **Select Protection Group Type** page of the **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>

    ![Wybierz grupę ochrony typu](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="afc7d-168">Na **Wybierz członków grupy** ekranu, zaznacz pole wyboru dla serwera programu SharePoint chcesz chronić, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-168">On the **Select Group Members** screen, select the check box for the SharePoint server you want to protect and click **Next**.</span></span>

    ![Wybierz członków grupy](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > <span data-ttu-id="afc7d-170">Z zainstalowanym agentem ochrony zobacz temat serwer w kreatorze.</span><span class="sxs-lookup"><span data-stu-id="afc7d-170">With the protection agent installed, you can see the server in the wizard.</span></span> <span data-ttu-id="afc7d-171">MABS zawiera także jego struktury.</span><span class="sxs-lookup"><span data-stu-id="afc7d-171">MABS also shows its structure.</span></span> <span data-ttu-id="afc7d-172">Ponieważ uruchomiono ConfigureSharePoint.exe MABS komunikuje się z usługą składnik zapisywania usługi VSS programu SharePoint i jego odpowiednie baz danych programu SQL Server i rozpoznaje struktury farmy programu SharePoint i skojarzonych baz danych zawartości oraz wszystkie odpowiednie elementy.</span><span class="sxs-lookup"><span data-stu-id="afc7d-172">Because you ran ConfigureSharePoint.exe, MABS communicates with the SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes the SharePoint farm structure, the associated content databases, and any corresponding items.</span></span>
   >
   >
4. <span data-ttu-id="afc7d-173">Na **wybierz metodę ochrony danych** strony, wprowadź nazwę **grupy ochrony**i wybierz preferowany *metody ochrony*.</span><span class="sxs-lookup"><span data-stu-id="afc7d-173">On the **Select Data Protection Method** page, enter the name of the **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="afc7d-174">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-174">Click **Next**.</span></span>

    ![Wybierz metodę ochrony danych](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > <span data-ttu-id="afc7d-176">Metoda ochrony dysku pozwala osiąganie celów czasu odzyskiwania krótki.</span><span class="sxs-lookup"><span data-stu-id="afc7d-176">The disk protection method helps to meet short recovery-time objectives.</span></span>
   >
   >
5. <span data-ttu-id="afc7d-177">Na **Określ cele krótkoterminowe** wybierz preferowany **zakres przechowywania** i ustalić, kiedy chcesz, aby tworzenie kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="afc7d-177">On the **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups to occur.</span></span>

    ![Określanie celów krótkoterminowych](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > <span data-ttu-id="afc7d-179">Ponieważ odzyskiwania najczęściej jest wymagana dla danych, która jest mniejsza niż pięć dni, możemy wybrany zakres przechowywania 5 dni na dysku i zapewnić, że tworzenie kopii zapasowej odbywa się podczas nieprodukcyjnych godzin, w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="afc7d-179">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that the backup happens during non-production hours, for this example.</span></span>
   >
   >
6. <span data-ttu-id="afc7d-180">Przejrzyj miejsce przydzielone do grupy ochrony na dysku puli magazynów, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-180">Review the storage pool disk space allocated for the protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="afc7d-181">Dla każdej grupy ochrony MABS przydziela miejsce na dysku do przechowywania replik.</span><span class="sxs-lookup"><span data-stu-id="afc7d-181">For every protection group, MABS allocates disk space to store and manage replicas.</span></span> <span data-ttu-id="afc7d-182">W tym momencie MABS należy utworzyć kopię wybranych danych.</span><span class="sxs-lookup"><span data-stu-id="afc7d-182">At this point, MABS must create a copy of the selected data.</span></span> <span data-ttu-id="afc7d-183">Wybierz, jak i kiedy chcesz utworzyć replikę, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-183">Select how and when you want the replica created, and then click **Next**.</span></span>

    ![Wybierz metodę tworzenia repliki](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > <span data-ttu-id="afc7d-185">Aby upewnić się, że ruch sieciowy nie jest wykonywane, wybierz godzinę poza godzinami produkcji.</span><span class="sxs-lookup"><span data-stu-id="afc7d-185">To make sure that network traffic is not effected, select a time outside production hours.</span></span>
   >
   >
8. <span data-ttu-id="afc7d-186">MABS zapewnia integralność danych poprzez przeprowadzenie sprawdzania spójności w replice.</span><span class="sxs-lookup"><span data-stu-id="afc7d-186">MABS ensures data integrity by performing consistency checks on the replica.</span></span> <span data-ttu-id="afc7d-187">Dostępne są dwie opcje dostępne.</span><span class="sxs-lookup"><span data-stu-id="afc7d-187">There are two available options.</span></span> <span data-ttu-id="afc7d-188">Można zdefiniować harmonogram wykonywania sprawdzania spójności lub programu DPM można uruchomić sprawdzania spójności automatycznie w replice zawsze, gdy stanie się niespójna.</span><span class="sxs-lookup"><span data-stu-id="afc7d-188">You can define a schedule to run consistency checks, or DPM can run consistency checks automatically on the replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="afc7d-189">Wybierz preferowaną opcję, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-189">Select your preferred option, and then click **Next**.</span></span>

    ![Sprawdzanie spójności](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="afc7d-191">Na **Określ dane chronione Online** farmy programu SharePoint, które chcesz chronić, a następnie kliknij przycisk Wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-191">On the **Specify Online Protection Data** page, select the SharePoint farm that you want to protect, and then click **Next**.</span></span>

    ![Program DPM Protection1 programu SharePoint](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="afc7d-193">Na **Określanie harmonogramu tworzenia kopii zapasowej Online** , wybierz preferowany harmonogram, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-193">On the **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="afc7d-195">MABS zawiera maksymalnie dwóch kopii zapasowych codziennie Azure z następnie dostępne najnowszego punktu kopii zapasowej dysku.</span><span class="sxs-lookup"><span data-stu-id="afc7d-195">MABS provides a maximum of two daily backups to Azure from the then available latest disk backup point.</span></span> <span data-ttu-id="afc7d-196">Kopia zapasowa Azure można również sterować ilość przepustowości sieci WAN, który może służyć do przechowywania kopii zapasowych w szczycie i poza godzinami pracy przy użyciu [ograniczania sieci kopia zapasowa Azure](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span><span class="sxs-lookup"><span data-stu-id="afc7d-196">Azure Backup can also control the amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    >
    >
11. <span data-ttu-id="afc7d-197">W zależności od harmonogram tworzenia kopii zapasowych, zostanie wybrany na **Określanie zasad przechowywania Online** wybierz zasady przechowywania dla punktów kopii zapasowej codziennie, co tydzień, miesięcznych i rocznych.</span><span class="sxs-lookup"><span data-stu-id="afc7d-197">Depending on the backup schedule that you selected, on the **Specify Online Retention Policy** page, select the retention policy for daily, weekly, monthly, and yearly backup points.</span></span>

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > <span data-ttu-id="afc7d-199">MABS wykorzystuje schemat przechowywania dziadek ojciec syn. w którym można wybrać zasady przechowywania różne dla różnych punktów kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="afc7d-199">MABS uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    >
    >
12. <span data-ttu-id="afc7d-200">Podobnie jak dysk, replika punktu początkowego odwołanie musi zostać utworzona na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="afc7d-200">Similar to disk, an initial reference point replica needs to be created in Azure.</span></span> <span data-ttu-id="afc7d-201">Wybierz preferowaną opcję tworzenia początkowej kopii zapasowej na platformie Azure, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-201">Select your preferred option to create an initial backup copy to Azure, and then click **Next**.</span></span>

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="afc7d-203">Przejrzyj wybrane ustawienia na **Podsumowanie** , a następnie kliknij przycisk **Utwórz grupę**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-203">Review your selected settings on the **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="afc7d-204">Po utworzeniu grupy ochrony, zobaczą komunikat z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="afc7d-204">You will see a success message after the protection group has been created.</span></span>

    ![Podsumowanie](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a><span data-ttu-id="afc7d-206">Przywróć element programu SharePoint z dysku przy użyciu MABS</span><span class="sxs-lookup"><span data-stu-id="afc7d-206">Restore a SharePoint item from disk by using MABS</span></span>
<span data-ttu-id="afc7d-207">W poniższym przykładzie *element odzyskiwanie programu SharePoint* został przypadkowo usunięty i mają zostać odzyskane.</span><span class="sxs-lookup"><span data-stu-id="afc7d-207">In the following example, the *Recovering SharePoint item* has been accidentally deleted and needs to be recovered.</span></span>
<span data-ttu-id="afc7d-208">![MABS Protection4 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="afc7d-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="afc7d-209">Otwórz **konsoli administratora programu DPM**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-209">Open the **DPM Administrator Console**.</span></span> <span data-ttu-id="afc7d-210">Wszystkie farmy programu SharePoint, które są chronione przez program DPM są wyświetlane w **ochrony** kartę.</span><span class="sxs-lookup"><span data-stu-id="afc7d-210">All SharePoint farms that are protected by DPM are shown in the **Protection** tab.</span></span>

    ![MABS Protection3 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="afc7d-212">Aby rozpocząć odzyskać element, wybierz **odzyskiwania** kartę.</span><span class="sxs-lookup"><span data-stu-id="afc7d-212">To begin to recover the item, select the **Recovery** tab.</span></span>

    ![MABS Protection5 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="afc7d-214">Umożliwia wyszukiwanie programu SharePoint dla *element odzyskiwanie programu SharePoint* przy użyciu symboli wieloznacznych na podstawie wyszukiwania w ramach odzyskiwania punktu zakresu.</span><span class="sxs-lookup"><span data-stu-id="afc7d-214">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>

    ![MABS Protection6 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="afc7d-216">Wybierz punkt odzyskiwania odpowiednie w wynikach wyszukiwania, kliknij element prawym przyciskiem myszy, a następnie wybierz **odzyskać**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-216">Select the appropriate recovery point from the search results, right-click the item, and then select **Recover**.</span></span>
5. <span data-ttu-id="afc7d-217">Można również przejrzeć różnych punktów odzyskiwania i wybierz bazę danych lub element, aby odzyskać.</span><span class="sxs-lookup"><span data-stu-id="afc7d-217">You can also browse through various recovery points and select a database or item to recover.</span></span> <span data-ttu-id="afc7d-218">Wybierz **Data > Godzina odzyskiwania**, a następnie wybierz poprawny **bazy danych > farmy programu SharePoint > punktu odzyskiwania > elementu**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-218">Select **Date > Recovery time**, and then select the correct **Database > SharePoint farm > Recovery point > Item**.</span></span>

    ![MABS Protection7 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="afc7d-220">Kliknij element prawym przyciskiem myszy, a następnie wybierz **odzyskać** otworzyć **Kreatora odzyskiwania**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-220">Right-click the item, and then select **Recover** to open the **Recovery Wizard**.</span></span> <span data-ttu-id="afc7d-221">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-221">Click **Next**.</span></span>

    ![Przegląd wybranego elementu odzyskiwania](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="afc7d-223">Wybierz typ odzyskiwania, które chcesz przeprowadzić, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-223">Select the type of recovery that you want to perform, and then click **Next**.</span></span>

    ![Typ odzyskiwania](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > <span data-ttu-id="afc7d-225">Wybór **Odzyskaj do oryginalnego** w przykładzie odzyskuje element do oryginalnej witryny programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="afc7d-225">The selection of **Recover to original** in the example recovers the item to the original SharePoint site.</span></span>
   >
   >
8. <span data-ttu-id="afc7d-226">Wybierz **proces odzyskiwania** którego chcesz używać.</span><span class="sxs-lookup"><span data-stu-id="afc7d-226">Select the **Recovery Process** that you want to use.</span></span>

   * <span data-ttu-id="afc7d-227">Wybierz **odzyskać bez używania farmy odzyskiwania** Jeśli farma programu SharePoint nie została zmieniona i jest taki sam jak punkt odzyskiwania, który jest przywracana.</span><span class="sxs-lookup"><span data-stu-id="afc7d-227">Select **Recover without using a recovery farm** if the SharePoint farm has not changed and is the same as the recovery point that is being restored.</span></span>
   * <span data-ttu-id="afc7d-228">Wybierz **odzyskać za pomocą farmy odzyskiwania** Jeśli farma SharePoint zmieniła się od czasu utworzenia punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="afc7d-228">Select **Recover using a recovery farm** if the SharePoint farm has changed since the recovery point was created.</span></span>

     ![Proces odzyskiwania](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="afc7d-230">Podaj tymczasowej lokalizacji wystąpienia programu SQL Server tymczasowo przywrócić bazę danych i podaj przemieszczania udziału plików na MABS oraz serwera z programem SharePoint, aby odzyskać elementu.</span><span class="sxs-lookup"><span data-stu-id="afc7d-230">Provide a staging SQL Server instance location to recover the database temporarily, and provide a staging file share on MABS and the server that's running SharePoint to recover the item.</span></span>

    ![Location1 przemieszczania](./media/backup-azure-backup-sharepoint/staging-location1.png)

    <span data-ttu-id="afc7d-232">MABS dołącza bazy danych zawartości, który jest hostem element programu SharePoint do tymczasowego wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afc7d-232">MABS attaches the content database that is hosting the SharePoint item to the temporary SQL Server instance.</span></span> <span data-ttu-id="afc7d-233">Z bazy danych zawartości odzyskuje elementu i umieszcza je na tymczasowej lokalizacji pliku na MABS.</span><span class="sxs-lookup"><span data-stu-id="afc7d-233">From the content database, it recovers the item and puts it on the staging file location on MABS.</span></span> <span data-ttu-id="afc7d-234">Odzyskiwanego elementu, który znajduje się w tymczasowej lokalizacji teraz musi zostać wyeksportowany do lokalizacji tymczasowej na farmie SharePoint.</span><span class="sxs-lookup"><span data-stu-id="afc7d-234">The recovered item that's on the staging location now needs to be exported to the staging location on the SharePoint farm.</span></span>

    ![Location2 przemieszczania](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="afc7d-236">Wybierz **Określ opcje odzyskiwania**i stosuje ustawienia zabezpieczeń do farmy programu SharePoint lub Zastosuj ustawienia zabezpieczeń dla punktu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="afc7d-236">Select **Specify recovery options**, and apply security settings to the SharePoint farm or apply the security settings of the recovery point.</span></span> <span data-ttu-id="afc7d-237">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-237">Click **Next**.</span></span>

    ![Opcje odzyskiwania](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > <span data-ttu-id="afc7d-239">Istnieje możliwość ograniczania użycia przepustowości sieci.</span><span class="sxs-lookup"><span data-stu-id="afc7d-239">You can choose to throttle the network bandwidth usage.</span></span> <span data-ttu-id="afc7d-240">Pozwala to zmniejszyć wpływ na serwerze produkcyjnym poza godzinami produkcji.</span><span class="sxs-lookup"><span data-stu-id="afc7d-240">This minimizes impact to the production server during production hours.</span></span>
    >
    >
11. <span data-ttu-id="afc7d-241">Sprawdź informacje, a następnie kliknij przycisk **odzyskać** aby rozpocząć odzyskiwanie pliku.</span><span class="sxs-lookup"><span data-stu-id="afc7d-241">Review the summary information, and then click **Recover** to begin recovery of the file.</span></span>

    ![Podsumowanie odzyskiwania](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="afc7d-243">Teraz wybierz **monitorowanie** karcie **konsoli administratora MABS** Aby wyświetlić **stan** odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="afc7d-243">Now select the **Monitoring** tab in the **MABS Administrator Console** to view the **Status** of the recovery.</span></span>

    ![Stan odzyskiwania](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > <span data-ttu-id="afc7d-245">Plik jest przywrócone.</span><span class="sxs-lookup"><span data-stu-id="afc7d-245">The file is now restored.</span></span> <span data-ttu-id="afc7d-246">Można odświeżać Sprawdź przywróconych plików witryny programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="afc7d-246">You can refresh the SharePoint site to check the restored file.</span></span>
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="afc7d-247">Przywróć bazę danych programu SharePoint z platformy Azure za pomocą programu DPM</span><span class="sxs-lookup"><span data-stu-id="afc7d-247">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="afc7d-248">Aby odzyskać bazę danych zawartości programu SharePoint, przejdź przez różne punkty odzyskiwania (jak pokazano wcześniej), a następnie wybierz punkt odzyskiwania, który chcesz przywrócić.</span><span class="sxs-lookup"><span data-stu-id="afc7d-248">To recover a SharePoint content database, browse through various recovery points (as shown previously), and select the recovery point that you want to restore.</span></span>

    ![MABS Protection8 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="afc7d-250">Kliknij dwukrotnie punkt odzyskiwania SharePoint, aby wyświetlić dostępne informacje o katalogu programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="afc7d-250">Double-click the SharePoint recovery point to show the available SharePoint catalog information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="afc7d-251">Ponieważ farmy programu SharePoint jest chroniony w celu przechowywania długoterminowego na platformie Azure, informacje katalogu (metadanych) są niedostępne na MABS.</span><span class="sxs-lookup"><span data-stu-id="afc7d-251">Because the SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on MABS.</span></span> <span data-ttu-id="afc7d-252">W związku z tym zawsze, gdy baza danych zawartości programu SharePoint w momencie mają zostać odzyskane, musisz ponownie w katalogu farmy programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="afc7d-252">As a result, whenever a point-in-time SharePoint content database needs to be recovered, you need to catalog the SharePoint farm again.</span></span>
   >
   >
3. <span data-ttu-id="afc7d-253">Kliknij przycisk **ponownego katalogowania**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-253">Click **Re-catalog**.</span></span>

    ![MABS Protection10 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    <span data-ttu-id="afc7d-255">**Ponownie skatalogować chmury** otwiera się okno stanu.</span><span class="sxs-lookup"><span data-stu-id="afc7d-255">The **Cloud Recatalog** status window opens.</span></span>

    ![MABS Protection11 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    <span data-ttu-id="afc7d-257">Po zakończeniu skatalogowania stan zmienia się na *Powodzenie*.</span><span class="sxs-lookup"><span data-stu-id="afc7d-257">After cataloging is finished, the status changes to *Success*.</span></span> <span data-ttu-id="afc7d-258">Kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-258">Click **Close**.</span></span>

    ![MABS Protection12 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="afc7d-260">Kliknij obiekt SharePoint pokazano MABS **odzyskiwania** kartę, aby pobrać struktury bazy danych zawartości.</span><span class="sxs-lookup"><span data-stu-id="afc7d-260">Click the SharePoint object shown in the MABS **Recovery** tab to get the content database structure.</span></span> <span data-ttu-id="afc7d-261">Kliknij element prawym przyciskiem myszy, a następnie kliknij przycisk **odzyskać**.</span><span class="sxs-lookup"><span data-stu-id="afc7d-261">Right-click the item, and then click **Recover**.</span></span>

    ![MABS Protection13 programu SharePoint](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="afc7d-263">W tym momencie wykonać [opisane w tym artykule](#restore-a-sharepoint-item-from-disk-using-dpm) odzyskać bazę danych zawartości programu SharePoint z dysku.</span><span class="sxs-lookup"><span data-stu-id="afc7d-263">At this point, follow the [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) to recover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="afc7d-264">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="afc7d-264">FAQs</span></span>
<span data-ttu-id="afc7d-265">Pytanie: czy element programu SharePoint do oryginalnej lokalizacji można odzyskać skonfigurowanie programu SharePoint przy użyciu funkcji SQL AlwaysOn (Ochrona na dysku)?</span><span class="sxs-lookup"><span data-stu-id="afc7d-265">Q: Can I recover a SharePoint item to the original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="afc7d-266">Odpowiedź: tak elementu można odzyskać do oryginalnej witryny programu SharePoint.</span><span class="sxs-lookup"><span data-stu-id="afc7d-266">A: Yes, the item can be recovered to the original SharePoint site.</span></span>

<span data-ttu-id="afc7d-267">Pytanie: czy bazy danych programu SharePoint do oryginalnej lokalizacji można odzyskać Jeśli programu SharePoint została skonfigurowana przy użyciu funkcji SQL AlwaysOn?</span><span class="sxs-lookup"><span data-stu-id="afc7d-267">Q: Can I recover a SharePoint database to the original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="afc7d-268">Odpowiedź: ponieważ baz danych programu SharePoint są konfigurowane w funkcji SQL AlwaysOn, nie można modyfikować, chyba że zostanie usunięta grupa dostępności.</span><span class="sxs-lookup"><span data-stu-id="afc7d-268">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless the availability group is removed.</span></span> <span data-ttu-id="afc7d-269">W związku z tym MABS nie można przywrócić bazę danych do oryginalnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="afc7d-269">As a result, MABS cannot restore a database to the original location.</span></span> <span data-ttu-id="afc7d-270">Można odzyskać bazy danych programu SQL Server do innego wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="afc7d-270">You can recover a SQL Server database to another SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afc7d-271">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="afc7d-271">Next steps</span></span>
* <span data-ttu-id="afc7d-272">Dowiedz się więcej o MABS ochrony programu SharePoint — zobacz [wideo serii — Program DPM ochronę programu SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span><span class="sxs-lookup"><span data-stu-id="afc7d-272">Learn more about MABS Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>
