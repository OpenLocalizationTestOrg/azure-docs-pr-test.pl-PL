---
title: zadania elastycznej bazy danych aaaInstalling | Dokumentacja firmy Microsoft
description: Przeprowadzenie instalacji hello elastycznej zadanie funkcji.
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="7e3ce-103">Instalowanie omówienie zadania elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="7e3ce-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="7e3ce-104">[**Zadania elastyczne bazy danych** ](sql-database-elastic-jobs-overview.md) można zainstalować za pomocą programu PowerShell lub za pośrednictwem hello Portal.You klasycznego Azure mogą uzyskać dostęp do toocreate zadania i zarządzać nimi przy użyciu interfejsu API środowiska PowerShell hello tylko w przypadku instalowania pakietu programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through hello Azure Classic Portal.You can gain access toocreate and manage jobs using hello PowerShell API only if you install hello PowerShell package.</span></span> <span data-ttu-id="7e3ce-105">Ponadto hello interfejsów API środowiska PowerShell Podaj znacznie więcej funkcji niż hello portal w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-105">Additionally, hello PowerShell APIs provide significantly more functionality than hello portal at this point in time.</span></span>

<span data-ttu-id="7e3ce-106">Jeśli użytkownik zainstalował już **zadania elastycznej bazy danych** za pośrednictwem hello portalu z istniejącego **puli elastycznej**, hello najnowsze programu Powershell w wersji zapoznawczej obejmuje skrypty tooupgrade istniejącej instalacji.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-106">If you have already installed **Elastic Database jobs** through hello Portal from an existing **elastic pool**, hello latest Powershell preview includes scripts tooupgrade your existing installation.</span></span> <span data-ttu-id="7e3ce-107">Jest zdecydowanie zalecane tooupgrade Twojego toohello instalacji najnowszych **zadania elastycznej bazy danych** składników w kolejności tootake korzystać z nowych funkcji udostępnianych za pośrednictwem hello interfejsów API środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-107">It is highly recommended tooupgrade your installation toohello latest **Elastic Database jobs** components in order tootake advantage of new functionality exposed via hello PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e3ce-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7e3ce-108">Prerequisites</span></span>
* <span data-ttu-id="7e3ce-109">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-109">An Azure subscription.</span></span> <span data-ttu-id="7e3ce-110">Bezpłatnej wersji próbnej, zobacz [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e3ce-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7e3ce-111">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-111">Azure PowerShell.</span></span> <span data-ttu-id="7e3ce-112">Zainstaluj najnowszą wersję hello przy użyciu hello [Instalatora platformy sieci Web](http://go.microsoft.com/fwlink/p/?linkid=320376).</span><span class="sxs-lookup"><span data-stu-id="7e3ce-112">Install hello latest version using hello [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="7e3ce-113">Aby uzyskać szczegółowe informacje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7e3ce-113">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="7e3ce-114">[Narzędzie wiersza polecenia NuGet](https://nuget.org/nuget.exe) jest pakietem zadania elastycznej bazy danych hello tooinstall używane.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used tooinstall hello Elastic Database jobs package.</span></span> <span data-ttu-id="7e3ce-115">Aby uzyskać więcej informacji zobacz http://docs.nuget.org/docs/start-here/installing-nuget.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a><span data-ttu-id="7e3ce-116">Pobieranie i importowanie hello elastycznej bazy danych zadania programu PowerShell pakietu</span><span class="sxs-lookup"><span data-stu-id="7e3ce-116">Download and import hello Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="7e3ce-117">Uruchom okno poleceń programu PowerShell usługi Microsoft Azure i przejdź do katalogu toohello, którego pobrano narzędzie wiersza polecenia NuGet (nuget.exe).</span><span class="sxs-lookup"><span data-stu-id="7e3ce-117">Launch Microsoft Azure PowerShell command window and navigate toohello directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="7e3ce-118">Pobieranie i importowanie **zadania elastycznej bazy danych** pakietu do bieżącego katalogu hello z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="7e3ce-118">Download and import **Elastic Database jobs** package into hello current directory with hello following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="7e3ce-119">Witaj **zadania elastycznej bazy danych** pliki są umieszczane w katalogu lokalnego hello w folderze o nazwie **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** gdzie *x.x.xxxx.x* odzwierciedla hello numer wersji.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-119">hello **Elastic Database jobs** files are placed in hello local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects hello version number.</span></span> <span data-ttu-id="7e3ce-120">polecenia cmdlet programu PowerShell Hello (w tym wymagany klient biblioteki) znajdują się w hello **tools\ElasticDatabaseJobs** podkatalogu i hello tooinstall skrypty programu PowerShell, uaktualniania i odinstalowywania również znajdują się w hello  **narzędzia** podkatalogu.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-120">hello PowerShell cmdlets (including required client .dlls) are located in hello **tools\ElasticDatabaseJobs** sub-directory and hello PowerShell scripts tooinstall, upgrade and uninstall also reside in hello **tools** sub-directory.</span></span>
3. <span data-ttu-id="7e3ce-121">Przejdź toohello narzędzia podkatalogu w folderze Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x hello wpisując narzędzia dysku cd, na przykład:</span><span class="sxs-lookup"><span data-stu-id="7e3ce-121">Navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="7e3ce-122">Wykonanie hello.\InstallElasticDatabaseJobsCmdlets.ps1 skryptu toocopy hello ElasticDatabaseJobs katalogu do $home\Documents\WindowsPowerShell\Modules.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-122">Execute hello .\InstallElasticDatabaseJobsCmdlets.ps1 script toocopy hello ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="7e3ce-123">Spowoduje to również automatycznie zaimportowanie modułu hello do użycia, na przykład:</span><span class="sxs-lookup"><span data-stu-id="7e3ce-123">This will also automatically import hello module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="7e3ce-124">Zainstaluj składniki zadania elastycznej bazy danych hello przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e3ce-124">Install hello Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="7e3ce-125">Uruchom okno poleceń programu PowerShell usługi Microsoft Azure i przejdź toohello \tools podkatalogu w folderze Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x hello: wpisz \tools dysku cd</span><span class="sxs-lookup"><span data-stu-id="7e3ce-125">Launch a Microsoft Azure PowerShell command window and navigate toohello \tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="7e3ce-126">Uruchom skrypt programu PowerShell.\InstallElasticDatabaseJobs.ps1 hello i dostarczać wartości żądanej zmienne.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-126">Execute hello .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="7e3ce-127">Ten skrypt utworzy hello składników zawartych w [zadania elastycznej bazy danych, składników i cenach](sql-database-elastic-jobs-overview.md#components-and-pricing) oraz konfigurowanie hello usługi w chmurze Azure tooappropriately Użyj hello składników zależnych.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-127">This script will create hello components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring hello Azure Cloud Service tooappropriately use hello dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="7e3ce-128">Po uruchomieniu tego polecenia okna otwiera pytania o **nazwy użytkownika** i **hasło**.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="7e3ce-129">Nie jest to Twoje poświadczenia platformy Azure, wprowadź hello nazwę użytkownika i hasło, które będą poświadczeniami administratora hello ma toocreate hello nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-129">This is not your Azure credentials, enter hello user name and password that will be hello administrator credentials you want toocreate for hello new server.</span></span>

<span data-ttu-id="7e3ce-130">można zmodyfikować parametry Hello na to wywołanie próbki dla żądane ustawienia.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-130">hello parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="7e3ce-131">Hello poniżej zamieszczono więcej informacji dotyczących zachowania hello każdego parametru:</span><span class="sxs-lookup"><span data-stu-id="7e3ce-131">hello following provides more information on hello behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="7e3ce-132">Parametr</span><span class="sxs-lookup"><span data-stu-id="7e3ce-132">Parameter</span></span></th>
    <th><span data-ttu-id="7e3ce-133">Opis</span><span class="sxs-lookup"><span data-stu-id="7e3ce-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="7e3ce-134">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="7e3ce-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="7e3ce-135">Zawiera nazwę grupy zasobów platformy Azure hello utworzoną hello toocontain nowo utworzone składniki platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-135">Provides hello Azure resource group name created toocontain hello newly created Azure components.</span></span> <span data-ttu-id="7e3ce-136">Tego parametru, domyślnie przyjmowana jest zbyt "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="7e3ce-136">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="7e3ce-137">Nie jest zalecane toochange tej wartości.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-137">It is not recommended toochange this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="7e3ce-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="7e3ce-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="7e3ce-139">Udostępnia hello toobe lokalizacji platformy Azure używana dla hello nowo utworzone składniki platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-139">Provides hello Azure location toobe used for hello newly created Azure components.</span></span> <span data-ttu-id="7e3ce-140">Ten parametr domyślnie toohello USA centralnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-140">This parameter defaults toohello Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="7e3ce-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="7e3ce-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="7e3ce-142">Zawiera liczbę hello tooinstall pracowników usługi.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-142">Provides hello number of service workers tooinstall.</span></span> <span data-ttu-id="7e3ce-143">Ten parametr domyślnie too1.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-143">This parameter defaults too1.</span></span> <span data-ttu-id="7e3ce-144">Większa liczba procesów roboczych może być używane tooscale limit hello usługi i tooprovide wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-144">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span> <span data-ttu-id="7e3ce-145">Zalecane jest toouse "2" dla wdrożenia, które wymagają wysokiej dostępności usługi hello.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-145">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="7e3ce-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="7e3ce-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="7e3ce-147">Udostępnia hello rozmiar maszyny Wirtualnej do użycia w ramach hello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-147">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="7e3ce-148">Ten parametr domyślnie tooA0.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-148">This parameter defaults tooA0.</span></span> <span data-ttu-id="7e3ce-149">Wartości parametrów A0/A1/A2/a3 są akceptowane powodujących hello worker roli toouse rozmiar ExtraSmall/małych/średnich/duży odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-149">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="7e3ce-150">Zobacz więcej informacji na temat rozmiarów roli procesu roboczego, FO [zadania elastycznej bazy danych, składników i cenach](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="7e3ce-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="7e3ce-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="7e3ce-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="7e3ce-152">Zapewnia cel poziomu usługi hello Standard edition.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-152">Provides hello service level objective for a Standard edition.</span></span> <span data-ttu-id="7e3ce-153">Ten parametr domyślnie tooS0.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-153">This parameter defaults tooS0.</span></span> <span data-ttu-id="7e3ce-154">Wartości parametrów S0/S1/S2/S3 są akceptowane, które powodują hello bazy danych SQL Azure toouse hello odpowiednich SLO.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-154">Parameter values of S0/S1/S2/S3 are accepted which cause hello Azure SQL Database toouse hello respective SLO.</span></span> <span data-ttu-id="7e3ce-155">Aby uzyskać więcej informacji na cele slo bazy danych SQL, zobacz [zadania elastycznej bazy danych, składników i cenach](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="7e3ce-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="7e3ce-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="7e3ce-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="7e3ce-157">Zawiera nazwę użytkownika administratora hello hello nowo utworzonego serwera bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-157">Provides hello admin user name for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="7e3ce-158">Gdy nie jest określony, okno poświadczenia programu PowerShell zostanie otwarty tooprompt o poświadczenia hello.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-158">When not specified, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="7e3ce-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="7e3ce-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="7e3ce-160">Zapewnia hasło administratora hello hello nowo utworzonego serwera bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-160">Provides hello admin password for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="7e3ce-161">Po nie podano okno poświadczenia programu PowerShell zostanie otwarty tooprompt hello poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-161">When not provided, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="7e3ce-162">Dla systemów przeznaczonych o dużej liczby zadań uruchamianych jednocześnie na dużej liczbie baz danych, zaleca się parametry toospecify takich jak: - ServiceWorkerCount 2 - ServiceVmSize A2 - SqlServerDatabaseSlo S2.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended toospecify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="7e3ce-163">Aktualizowanie instalacji składników istniejącego zadania elastycznej bazy danych przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e3ce-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="7e3ce-164">**Zadania elastyczne bazy danych** może zostać zaktualizowana w ramach istniejącej instalacji zapewnienia skalowalności i wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="7e3ce-165">Ten proces umożliwia w ramach przyszłych uaktualnień kodu usługi bez konieczności toodrop i ponowne utworzenie bazy danych kontroli hello.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-165">This process allows for future upgrades of service code without having toodrop and recreate hello control database.</span></span> <span data-ttu-id="7e3ce-166">Ten proces można również w hello tej samej wersji toomodify hello usługi liczba maszyn wirtualnych rozmiaru lub powitania serwera worker.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-166">This process can also be used within hello same version toomodify hello service VM size or hello server worker count.</span></span>

<span data-ttu-id="7e3ce-167">rozmiar maszyny Wirtualnej hello tooupdate instalacji, hello wykonywania następującego skryptu z parametrami zaktualizować wartości toohello wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-167">tooupdate hello VM size of an installation, run hello following script with parameters updated toohello values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="7e3ce-168">Parametr</span><span class="sxs-lookup"><span data-stu-id="7e3ce-168">Parameter</span></span></th>
  <th><span data-ttu-id="7e3ce-169">Opis</span><span class="sxs-lookup"><span data-stu-id="7e3ce-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="7e3ce-170">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="7e3ce-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="7e3ce-171">Określa nazwę grupy zasobów platformy Azure hello składników zadania elastycznej bazy danych hello początkowo zostały zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-171">Identifies hello Azure resource group name used when hello Elastic Database job components were initially installed.</span></span> <span data-ttu-id="7e3ce-172">Tego parametru, domyślnie przyjmowana jest zbyt "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="7e3ce-172">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="7e3ce-173">Ponieważ nie jest zalecane toochange ta wartość nie powinna mieć toospecify tego parametru.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-173">Since it is not recommended toochange this value, you shouldn't have toospecify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="7e3ce-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="7e3ce-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="7e3ce-175">Zawiera liczbę hello tooinstall pracowników usługi.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-175">Provides hello number of service workers tooinstall.</span></span>  <span data-ttu-id="7e3ce-176">Ten parametr domyślnie too1.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-176">This parameter defaults too1.</span></span>  <span data-ttu-id="7e3ce-177">Większa liczba procesów roboczych może być używane tooscale limit hello usługi i tooprovide wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-177">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span>  <span data-ttu-id="7e3ce-178">Zalecane jest toouse "2" dla wdrożenia, które wymagają wysokiej dostępności usługi hello.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-178">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="7e3ce-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="7e3ce-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="7e3ce-180">Udostępnia hello rozmiar maszyny Wirtualnej do użycia w ramach hello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-180">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="7e3ce-181">Ten parametr domyślnie tooA0.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-181">This parameter defaults tooA0.</span></span> <span data-ttu-id="7e3ce-182">Wartości parametrów A0/A1/A2/a3 są akceptowane powodujących hello worker roli toouse rozmiar ExtraSmall/małych/średnich/duży odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-182">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="7e3ce-183">Zobacz więcej informacji na temat rozmiarów roli procesu roboczego, FO [zadania elastycznej bazy danych, składników i cenach](sql-database-elastic-jobs-overview.md#components-and-pricing).</span><span class="sxs-lookup"><span data-stu-id="7e3ce-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a><span data-ttu-id="7e3ce-184">Zainstaluj składniki zadania elastycznej bazy danych hello przy użyciu hello portalu</span><span class="sxs-lookup"><span data-stu-id="7e3ce-184">Install hello Elastic Database jobs components using hello Portal</span></span>
<span data-ttu-id="7e3ce-185">Po utworzeniu [utworzyć puli elastycznej](sql-database-elastic-pool-manage-portal.md), można zainstalować **zadania elastycznej bazy danych** składniki tooenable wykonywania zadań administracyjnych dla każdej bazy danych w puli elastycznej hello.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components tooenable execution of administrative tasks against each database in hello elastic pool.</span></span> <span data-ttu-id="7e3ce-186">Inaczej niż w przypadku, gdy przy użyciu hello **zadania elastycznej bazy danych** interfejsów API środowiska PowerShell, interfejsu portalu hello jest obecnie ograniczone tooonly wykonywane istniejącej puli.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-186">Unlike when using hello **Elastic Database jobs** PowerShell APIs, hello portal interface is currently restricted tooonly executing against an existing pool.</span></span>

<span data-ttu-id="7e3ce-187">**Szacowany czas toocomplete:** 10 minut.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-187">**Estimated time toocomplete:** 10 minutes.</span></span>

1. <span data-ttu-id="7e3ce-188">W widoku pulpitu nawigacyjnego hello hello puli elastycznej za pośrednictwem hello [Azure Portal](https://portal.azure.com/#) , kliknij przycisk **Utwórz zadanie**.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-188">From hello dashboard view of hello elastic pool via hello [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="7e3ce-189">W przypadku tworzenia zadania dla powitania po raz pierwszy, musisz zainstalować **zadania elastycznej bazy danych** klikając **warunki dotyczące**.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-189">If you are creating a job for hello first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="7e3ce-190">Zaakceptować warunki hello klikając hello wyboru.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-190">Accept hello terms by clicking hello checkbox.</span></span>
4. <span data-ttu-id="7e3ce-191">W widoku hello "instalacji usług" kliknij **POŚWIADCZENIA zadania**.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-191">In hello "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![Instalowanie usług hello][1]
5. <span data-ttu-id="7e3ce-193">Wpisz nazwę użytkownika i hasło administratora bazy danych. W ramach instalacji hello jest tworzony nowy serwer bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-193">Type a user name and password for a database admin. As part of hello installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="7e3ce-194">W ramach tego nowego serwera nowej bazy danych, znany jako bazy danych kontroli hello jest tworzony i używany toocontain hello meta danych dla zadania elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-194">Within this new server, a new database, known as hello control database, is created and used toocontain hello meta data for Elastic Database jobs.</span></span> <span data-ttu-id="7e3ce-195">Witaj, nazwę użytkownika i hasło utworzone w tym miejscu są używane hello w celu rejestrowania w bazie danych kontroli toohello.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-195">hello user name and password created here are used for hello purpose of logging in toohello control database.</span></span> <span data-ttu-id="7e3ce-196">Oddzielne poświadczeń jest używany do wykonania skryptu hello w przypadku baz danych w puli hello.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-196">A separate credential is used for script execution against hello databases within hello pool.</span></span>
   
    ![Utwórz nazwę użytkownika i hasło][2]
6. <span data-ttu-id="7e3ce-198">Kliknij przycisk OK hello.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-198">Click hello OK button.</span></span> <span data-ttu-id="7e3ce-199">składniki Hello są tworzone automatycznie w ciągu kilku minut w nowym [grupy zasobów](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7e3ce-199">hello components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="7e3ce-200">nową grupę zasobów Hello jest przypięty toohello start tablicy, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-200">hello new resource group is pinned toohello start board, as shown below.</span></span> <span data-ttu-id="7e3ce-201">Zadania po utworzeniu elastycznej bazy danych (usługi w chmurze, bazę danych SQL, magistrali usług i magazyn) są tworzone w grupie hello.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-201">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in hello group.</span></span>
   
    ![grupy zasobów w tablicy start][3]
7. <span data-ttu-id="7e3ce-203">Jeśli próba toocreate lub zarządzać zadania podczas instalowania zadania elastycznej bazy danych podczas dostarczania **poświadczenia** zobaczą następującą wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-203">If you attempt toocreate or manage a job while elastic database jobs is installing, when providing **Credentials** you will see hello following message.</span></span>
   
    ![Wdrożenie w toku][4]

<span data-ttu-id="7e3ce-205">Jeśli wymagana jest dezinstalację, należy usunąć hello grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-205">If uninstallation is required, delete hello resource group.</span></span> <span data-ttu-id="7e3ce-206">Zobacz [jak toouninstall hello elastycznej bazy danych zadania składniki](sql-database-elastic-jobs-uninstall.md).</span><span class="sxs-lookup"><span data-stu-id="7e3ce-206">See [How toouninstall hello Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e3ce-207">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7e3ce-207">Next steps</span></span>
<span data-ttu-id="7e3ce-208">Upewnij się, poświadczenie o hello odpowiednie prawa do wykonania skryptu jest utworzony w każdej bazie danych w grupie hello, aby uzyskać więcej informacji, zobacz [Zabezpieczanie bazy danych SQL](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="7e3ce-208">Ensure a credential with hello appropriate rights for script execution is created on each database in hello group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="7e3ce-209">Zobacz [Tworzenie zadania i zarządzać nimi elastycznej bazy danych](sql-database-elastic-jobs-create-and-manage.md) tooget uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="7e3ce-209">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) tooget started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
