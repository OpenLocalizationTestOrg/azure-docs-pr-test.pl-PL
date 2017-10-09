---
title: "aaaSilent instalacji serwera usługi Kopia zapasowa Azure w wersji 2 | Dokumentacja firmy Microsoft"
description: "Użycie toosilently skrypt programu PowerShell zainstalowanie serwer kopii zapasowej Azure w wersji 2. Ten rodzaj instalacji jest również nazywany instalacji nienadzorowanej."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/30/2017
ms.author: markgal;masaran
ms.openlocfilehash: 6b94b4a278bfcd5f8c5c363cb811bd8eec984243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="3af1e-104">Uruchamianie nienadzorowanej instalacji serwera usługi Kopia zapasowa Azure w wersji 2</span><span class="sxs-lookup"><span data-stu-id="3af1e-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="3af1e-105">Dowiedz się, jak toorun instalacji nienadzorowanej v2 serwer kopii zapasowej Azure.</span><span class="sxs-lookup"><span data-stu-id="3af1e-105">Learn how toorun an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="3af1e-106">Te kroki nie są stosowane, jeśli instalujesz serwer kopii zapasowej Azure w wersji 1.</span><span class="sxs-lookup"><span data-stu-id="3af1e-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="3af1e-107">Zainstaluj serwer zapasowy v2</span><span class="sxs-lookup"><span data-stu-id="3af1e-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="3af1e-108">Na serwerze hello, który jest hostem serwera usługi Kopia zapasowa Azure w wersji 2 Utwórz plik tekstowy.</span><span class="sxs-lookup"><span data-stu-id="3af1e-108">On hello server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="3af1e-109">(Można utworzyć pliku hello w Notatniku lub w innym tekście edytora.) Zapisz plik hello jako MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="3af1e-109">(You can create hello file in Notepad or in another text editor.) Save hello file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="3af1e-110">Wklej hello następującego kodu w pliku MABSSetup.ini hello.</span><span class="sxs-lookup"><span data-stu-id="3af1e-110">Paste hello following code in hello MABSSetup.ini file.</span></span> <span data-ttu-id="3af1e-111">Zastąp tekst hello w nawiasach hello (\< \>) z wartościami z używanego środowiska.</span><span class="sxs-lookup"><span data-stu-id="3af1e-111">Replace hello text inside hello brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="3af1e-112">Przykładem jest Hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="3af1e-112">hello following text is an example:</span></span>

  ```
  [OPTIONS]
  UserName=administrator
  CompanyName=<Microsoft Corporation>
  SQLMachineName=localhost
  SQLInstanceName=<SQL instance name>
  SQLMachineUserName=administrator
  SQLMachinePassword=<admin password>
  SQLMachineDomainName=<machine domain>
  ReportingMachineName=localhost
  ReportingInstanceName=<reporting instance name>
  SqlAccountPassword=<admin password>
  ReportingMachineUserName=<username>
  ReportingMachinePassword=<reporting admin password>
  ReportingMachineDomainName=<domain>
  VaultCredentialFilePath=<vault credential full path and complete name>
  SecurityPassphrase=<passphrase>
  PassphraseSaveLocation=<passphrase save location>
  UseExistingSQL=<1/0 use or do not use existing SQL>
  ```

3. <span data-ttu-id="3af1e-113">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="3af1e-113">Save hello file.</span></span> <span data-ttu-id="3af1e-114">Następnie w wierszu polecenia z podwyższonym poziomem uprawnień na serwerze instalacji hello, wprowadź polecenie:</span><span class="sxs-lookup"><span data-stu-id="3af1e-114">Then, at an elevated command prompt on hello installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="3af1e-115">Można użyć tych flag do instalacji hello:</span><span class="sxs-lookup"><span data-stu-id="3af1e-115">You can use these flags for hello installation:</span></span></br><span data-ttu-id="3af1e-116">
**/f**: ścieżka pliku ini</span><span class="sxs-lookup"><span data-stu-id="3af1e-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="3af1e-117">
**/l**: ścieżka dziennika</span><span class="sxs-lookup"><span data-stu-id="3af1e-117">
**/l**: Log path</span></span></br><span data-ttu-id="3af1e-118">
**/i**: ścieżka instalacji</span><span class="sxs-lookup"><span data-stu-id="3af1e-118">
**/i**: Installation path</span></span></br><span data-ttu-id="3af1e-119">
**/x**: Odinstaluj ścieżki</span><span class="sxs-lookup"><span data-stu-id="3af1e-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="3af1e-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3af1e-120">Next steps</span></span>
<span data-ttu-id="3af1e-121">Po zainstalowaniu serwera kopii zapasowej, Dowiedz się jak tooprepare serwera, lub Włącz ochronę obciążeń.</span><span class="sxs-lookup"><span data-stu-id="3af1e-121">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="3af1e-122">Przygotowanie serwera kopii zapasowej obciążeń</span><span class="sxs-lookup"><span data-stu-id="3af1e-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="3af1e-123">Użyj tooback serwera kopii zapasowej serwera VMware</span><span class="sxs-lookup"><span data-stu-id="3af1e-123">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="3af1e-124">Użyj tooback serwera kopii zapasowej serwera SQL</span><span class="sxs-lookup"><span data-stu-id="3af1e-124">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="3af1e-125">Dodaj tooBackup nowoczesnych magazynu kopii zapasowej serwera</span><span class="sxs-lookup"><span data-stu-id="3af1e-125">Add Modern Backup Storage tooBackup Server</span></span>](backup-mabs-add-storage.md)
