---
title: "aaaCreate elastycznej zadania przy użyciu programu PowerShell i zarządzać nimi | Dokumentacja firmy Microsoft"
description: "PowerShell używane toomanage pule bazy danych SQL Azure"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="eb7b8-103">Tworzenie i zarządzanie nimi zadania elastycznej bazy danych SQL przy użyciu programu PowerShell (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="eb7b8-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="eb7b8-104">Witaj interfejsów API środowiska PowerShell dla **zadania elastycznej bazy danych** (w wersji zapoznawczej), umożliwiają definiowanie grupę baz danych, które wykona skryptów.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-104">hello PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="eb7b8-105">W tym artykule przedstawiono sposób toocreate i zarządzanie nimi **zadania elastycznej bazy danych** przy użyciu poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-105">This article shows how toocreate and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="eb7b8-106">Zobacz [omówienie zadania elastyczne](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eb7b8-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="eb7b8-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eb7b8-107">Prerequisites</span></span>
* <span data-ttu-id="eb7b8-108">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-108">An Azure subscription.</span></span> <span data-ttu-id="eb7b8-109">Bezpłatnej wersji próbnej, zobacz [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb7b8-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="eb7b8-110">Zestaw baz danych utworzonych z hello narzędzi elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-110">A set of databases created with hello Elastic Database tools.</span></span> <span data-ttu-id="eb7b8-111">Zobacz [wprowadzenie do narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eb7b8-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="eb7b8-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-112">Azure PowerShell.</span></span> <span data-ttu-id="eb7b8-113">Aby uzyskać szczegółowe informacje, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="eb7b8-113">For detailed information, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="eb7b8-114">**Zadania elastyczne bazy danych** pakietu programu PowerShell: zobacz [zadania instalowania elastycznej bazy danych](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="eb7b8-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="eb7b8-115">Wybierz subskrypcję platformy Azure</span><span class="sxs-lookup"><span data-stu-id="eb7b8-115">Select your Azure subscription</span></span>
<span data-ttu-id="eb7b8-116">tooselect hello subskrypcji należy identyfikator subskrypcji (**- SubscriptionId**) lub nazwę subskrypcji (**— Nazwa subskrypcji**).</span><span class="sxs-lookup"><span data-stu-id="eb7b8-116">tooselect hello subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="eb7b8-117">Jeśli masz wiele subskrypcji możesz uruchomić hello **Get-AzureRmSubscription** polecenia cmdlet i skopiuj hello potrzeby informacji o subskrypcji z hello zestawu wyników.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-117">If you have multiple subscriptions you can run hello **Get-AzureRmSubscription** cmdlet and copy hello desired subscription information from hello result set.</span></span> <span data-ttu-id="eb7b8-118">Po uzyskaniu informacji o subskrypcji, uruchom następujące polecenie commandlet tooset hello tej subskrypcji jako domyślny hello, a mianowicie hello cel dla tworzenia zadania i zarządzać nimi:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-118">Once you have your subscription information, run hello following commandlet tooset this subscription as hello default, namely hello target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="eb7b8-119">Witaj [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) jest zalecane w przypadku użycia toodevelop i wykonywanie skryptów programu PowerShell przed hello zadania elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-119">hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage toodevelop and execute PowerShell scripts against hello Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="eb7b8-120">Obiekty zadania elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="eb7b8-121">Witaj następujących tabela zawiera listę się wszystkie typy obiektów hello z **zadania elastycznej bazy danych** wraz z jego opis i odpowiednich interfejsów API programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-121">hello following table lists out all hello object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="eb7b8-122">Typ obiektu</span><span class="sxs-lookup"><span data-stu-id="eb7b8-122">Object Type</span></span></th>
    <th><span data-ttu-id="eb7b8-123">Opis</span><span class="sxs-lookup"><span data-stu-id="eb7b8-123">Description</span></span></th>
    <th><span data-ttu-id="eb7b8-124">Powiązanych interfejsów API programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="eb7b8-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="eb7b8-125">Poświadczenie</span><span class="sxs-lookup"><span data-stu-id="eb7b8-125">Credential</span></span></td>
    <td><span data-ttu-id="eb7b8-126">Toouse nazwy użytkownika i hasła podczas łączenia toodatabases dla wykonywania skryptów lub aplikacji DACPACs.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-126">Username and password toouse when connecting toodatabases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="eb7b8-127">Witaj hasło jest szyfrowane przed wysłaniem tooand przechowywania w hello zadania elastyczne bazy danych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-127">hello password is encrypted before sending tooand storing in hello Elastic Database Jobs database.</span></span>  <span data-ttu-id="eb7b8-128">hasło Hello jest odszyfrowywany przez hello zadania elastyczne bazy danych usługi za pomocą poświadczeń hello utworzone i załadowane z hello skrypt instalacji.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-128">hello password is decrypted by hello Elastic Database Jobs service via hello credential created and uploaded from hello installation script.</span></span></td>
    <td><p><span data-ttu-id="eb7b8-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="eb7b8-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="eb7b8-130">Nowe AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="eb7b8-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="eb7b8-131">Zestaw AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="eb7b8-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="eb7b8-132">Skrypt</span><span class="sxs-lookup"><span data-stu-id="eb7b8-132">Script</span></span></td>
    <td><span data-ttu-id="eb7b8-133">Toobe skryptu języka Transact-SQL używane do wykonywania różnych bazach danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-133">Transact-SQL script toobe used for execution across databases.</span></span>  <span data-ttu-id="eb7b8-134">skrypt Hello powinna być idempotentności toobe utworzone, ponieważ usługa hello ponowi wykonanie skryptu powitania po awarii.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-134">hello script should be authored toobe idempotent since hello service will retry execution of hello script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="eb7b8-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="eb7b8-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="eb7b8-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="eb7b8-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="eb7b8-137">Nowe AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="eb7b8-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="eb7b8-138">Zestaw AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="eb7b8-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="eb7b8-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="eb7b8-139">DACPAC</span></span></td>
    <td><span data-ttu-id="eb7b8-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Aplikacji warstwy danych </a> pakietu toobe zastosowany do wszystkich baz danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package toobe applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="eb7b8-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="eb7b8-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="eb7b8-142">Nowe AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="eb7b8-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="eb7b8-143">Zestaw AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="eb7b8-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="eb7b8-144">Docelowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-144">Database Target</span></span></td>
    <td><span data-ttu-id="eb7b8-145">Bazy danych i serwera nazw tooan wskazujące bazę danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-145">Database and server name pointing tooan Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="eb7b8-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="eb7b8-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="eb7b8-147">Nowe AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="eb7b8-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="eb7b8-148">Identyfikator niezależnego fragmentu mapy docelowego</span><span class="sxs-lookup"><span data-stu-id="eb7b8-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="eb7b8-149">Kombinacja docelowej bazy danych i toobe poświadczenia używane toodetermine informacje przechowywane w mapie niezależnego fragmentu elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-149">Combination of a database target and a credential toobe used toodetermine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="eb7b8-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="eb7b8-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="eb7b8-151">Nowe AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="eb7b8-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="eb7b8-152">Zestaw AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="eb7b8-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="eb7b8-153">Docelowy kolekcji niestandardowej</span><span class="sxs-lookup"><span data-stu-id="eb7b8-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="eb7b8-154">Zdefiniowaną grupę toocollectively baz danych użycia dla wykonania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-154">Defined group of databases toocollectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="eb7b8-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="eb7b8-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="eb7b8-156">Nowe AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="eb7b8-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="eb7b8-157">Docelowy podrzędnej kolekcji niestandardowej</span><span class="sxs-lookup"><span data-stu-id="eb7b8-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="eb7b8-158">Obiekt docelowy bazy danych, do którego odwołuje się z kolekcji niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="eb7b8-159">Dodaj AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="eb7b8-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="eb7b8-160">Usuń AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="eb7b8-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="eb7b8-161">Zadanie</span><span class="sxs-lookup"><span data-stu-id="eb7b8-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="eb7b8-162">Definicja parametrów dla zadania, które mogą być używane tootrigger wykonanie lub toofulfill harmonogram.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-162">Definition of parameters for a job that can be used tootrigger execution or toofulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="eb7b8-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="eb7b8-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="eb7b8-164">Nowe AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="eb7b8-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="eb7b8-165">Zestaw AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="eb7b8-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="eb7b8-166">Wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="eb7b8-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="eb7b8-167">Kontener toofulfill niezbędnych zadań wykonywania skryptu lub zastosowania docelowego tooa DACPAC, przy użyciu poświadczeń dla połączenia z bazą danych z błędami obsługiwane zasady wykonywania tooan zgodnie.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-167">Container of tasks necessary toofulfill either executing a script or applying a DACPAC tooa target using credentials for database connections with failures handled in accordance tooan execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="eb7b8-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="eb7b8-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="eb7b8-169">Start AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="eb7b8-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="eb7b8-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="eb7b8-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="eb7b8-171">AzureSqlJobExecution oczekiwania</span><span class="sxs-lookup"><span data-stu-id="eb7b8-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="eb7b8-172">Wykonywanie zadań zadania</span><span class="sxs-lookup"><span data-stu-id="eb7b8-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="eb7b8-173">Pojedynczą jednostkę pracy toofulfill zadania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-173">Single unit of work toofulfill a job.</span></span></p>
    <p><span data-ttu-id="eb7b8-174">Jeśli zadanie nie jest możliwe toosuccessfully wykonania, będą rejestrowane hello Wynikowy komunikat o wyjątku i nowe zadanie dopasowania zostanie utworzona i wykonywane w określonych toohello zgodnie zasad wykonywania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-174">If a job task is not able toosuccessfully execute, hello resulting exception message will be logged and a new matching job task will be created and executed in accordance toohello specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="eb7b8-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="eb7b8-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="eb7b8-176">Start AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="eb7b8-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="eb7b8-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="eb7b8-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="eb7b8-178">AzureSqlJobExecution oczekiwania</span><span class="sxs-lookup"><span data-stu-id="eb7b8-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="eb7b8-179">Zasady wykonywania zadania</span><span class="sxs-lookup"><span data-stu-id="eb7b8-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="eb7b8-180">Formanty zadań limitów czasu wykonywania, ponownych prób, ograniczenia i odstępach czasu między kolejnymi próbami.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="eb7b8-181">Zadania elastyczne bazy danych zawiera domyślne zasady wykonywania zadania, które zasadniczo nieskończone ponowne próby niepowodzeń zadań zadania z wykładniczego wycofywania odstępach czasu między kolejnymi próbami.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="eb7b8-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="eb7b8-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="eb7b8-183">Nowe AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="eb7b8-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="eb7b8-184">Zestaw AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="eb7b8-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="eb7b8-185">Harmonogram</span><span class="sxs-lookup"><span data-stu-id="eb7b8-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="eb7b8-186">Czas na podstawie specyfikacji wykonywania tootake miejsce reoccurring interwał lub na jeden raz.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-186">Time based specification for execution tootake place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="eb7b8-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="eb7b8-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="eb7b8-188">Nowe AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="eb7b8-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="eb7b8-189">Zestaw AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="eb7b8-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="eb7b8-190">Wyzwala zadanie</span><span class="sxs-lookup"><span data-stu-id="eb7b8-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="eb7b8-191">Mapowanie między zadania i harmonogram wykonywania zadania tootrigger zgodnie z harmonogramem toohello.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-191">A mapping between a job and a schedule tootrigger job execution according toohello schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="eb7b8-192">Nowe AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="eb7b8-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="eb7b8-193">Usuń AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="eb7b8-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="eb7b8-194">Obsługiwane zadania elastycznej bazy danych grupy typów</span><span class="sxs-lookup"><span data-stu-id="eb7b8-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="eb7b8-195">zadanie Hello wykonuje skrypty języka Transact-SQL (T-SQL) lub aplikacji DACPACs między grupą baz danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-195">hello job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="eb7b8-196">Gdy zadanie jest przesłanych toobe wykonywane przez grupę baz danych, zadania hello "rozwija" hello na zadań podrzędnych, gdzie pełniących hello zażądał miało zostać wykonane w pojedynczej bazy danych w grupie hello.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-196">When a job is submitted toobe executed across a group of databases, hello job “expands” hello into child jobs where each performs hello requested execution against a single database in hello group.</span></span> 

<span data-ttu-id="eb7b8-197">Istnieją dwa typy grup, które możesz utworzyć:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="eb7b8-198">[Mapa niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md) grupy: zadania po przesłanych tootarget mapy niezależnego fragmentu zadania hello odpytuje hello niezależnego fragmentu mapy toodetermine jej bieżącego zestawu odłamków, a następnie zadania dla każdego niezależnego fragmentu tworzy podrzędnych, hello niezależnego fragmentu mapy.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted tootarget a shard map, hello job queries hello shard map toodetermine its current set of shards, and then creates child jobs for each shard in hello shard map.</span></span>
* <span data-ttu-id="eb7b8-199">Niestandardowe grupy zbierania: niestandardowy zdefiniowany zestaw baz danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="eb7b8-200">Gdy zadanie jest przeznaczony dla kolekcji niestandardowych, tworzy podrzędnych zadania dla każdej bazy danych obecnie w kolekcji niestandardowej hello.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-200">When a job targets a custom collection, it creates child jobs for each database currently in hello custom collection.</span></span>

## <a name="tooset-hello-elastic-database-jobs-connection"></a><span data-ttu-id="eb7b8-201">Witaj tooset połączenia zadania elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-201">tooset hello Elastic Database jobs connection</span></span>
<span data-ttu-id="eb7b8-202">Połączenie musi toobe Konfigurowanie toohello zadań *bazy danych kontroli* hello toousing poprzedniego zadania interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-202">A connection needs toobe set toohello jobs *control database* prior toousing hello jobs APIs.</span></span> <span data-ttu-id="eb7b8-203">Uruchomienie tego polecenia cmdlet wyzwala toopop okna poświadczeń, się Żądanie hello nazwy użytkownika i hasła utworzonego podczas instalacji zadania elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-203">Running this cmdlet triggers a credential window toopop up requesting hello user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="eb7b8-204">Wszystkie przykłady w tym temacie założono, że pierwsza została już wykonana.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="eb7b8-205">Otwórz połączenie toohello elastycznej bazy danych zadań:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-205">Open a connection toohello Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a><span data-ttu-id="eb7b8-206">Zaszyfrowane poświadczenia w ramach hello zadania elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-206">Encrypted credentials within hello Elastic Database jobs</span></span>
<span data-ttu-id="eb7b8-207">Poświadczenia bazy danych można wstawiać do zadań hello *bazy danych kontroli* jego hasłem, szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-207">Database credentials can be inserted into hello jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="eb7b8-208">Jest toostore niezbędne poświadczenia tooenable zadania toobe wykonane w późniejszym czasie (przy użyciu harmonogramy zadań).</span><span class="sxs-lookup"><span data-stu-id="eb7b8-208">It is necessary toostore credentials tooenable jobs toobe executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="eb7b8-209">Szyfrowanie działa za pośrednictwem utworzone jako część hello skrypt instalacji certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-209">Encryption works through a certificate created as part of hello installation script.</span></span> <span data-ttu-id="eb7b8-210">Tworzy skrypt instalacji Hello i przekazywanie certyfikatu hello na powitania usługi w chmurze Azure do odszyfrowywania hello przechowywane hasła szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-210">hello installation script creates and uploads hello certificate into hello Azure Cloud Service for decryption of hello stored encrypted passwords.</span></span> <span data-ttu-id="eb7b8-211">Usługi w chmurze Azure Hello później przechowuje hello klucza publicznego w ramach zadania hello *bazy danych kontroli* co pozwala hello interfejsu API programu PowerShell lub klasycznego portalu Azure tooencrypt interfejsu podanego hasła bez konieczności hello certyfikatu toobe zainstalowane lokalnie.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-211">hello Azure Cloud Service later stores hello public key within hello jobs *control database* which enables hello PowerShell API or Azure Classic Portal interface tooencrypt a provided password without requiring hello certificate toobe locally installed.</span></span>

<span data-ttu-id="eb7b8-212">Witaj poświadczenie hasła są szyfrowane i bezpieczne od użytkowników z obiektami zadania bazy danych tooElastic dostęp tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-212">hello credential passwords are encrypted and secure from users with read-only access tooElastic Database jobs objects.</span></span> <span data-ttu-id="eb7b8-213">Ale istnieje możliwość przez złośliwego użytkownika mającego dostęp do odczytu zapisu tooElastic zadań baz danych obiektów tooextract hasła.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-213">But it is possible for a malicious user with read-write access tooElastic Database Jobs objects tooextract a password.</span></span> <span data-ttu-id="eb7b8-214">Poświadczenia są zaprojektowane toobe ponownie wykorzystać w odniesieniu do wykonania zadania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-214">Credentials are designed toobe reused across job executions.</span></span> <span data-ttu-id="eb7b8-215">Poświadczenia są przekazywane tootarget baz danych podczas ustanawiania połączenia.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-215">Credentials are passed tootarget databases when establishing connections.</span></span> <span data-ttu-id="eb7b8-216">Obecnie nie istnieją żadne ograniczenia dotyczące hello docelowymi bazami danych używane dla każdego poświadczenia, złośliwy użytkownik może dodać element docelowy bazy danych dla bazy danych pod kontrolą hello złośliwy użytkownik.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-216">There are currently no restrictions on hello target databases used for each credential, malicious user could add a database target for a database under hello malicious user's control.</span></span> <span data-ttu-id="eb7b8-217">Użytkownik Hello później można uruchomić zadania przeznaczonych dla tej bazy danych toogain hello poświadczeń hasła.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-217">hello user could subsequently start a job targeting this database toogain hello credential's password.</span></span>

<span data-ttu-id="eb7b8-218">Najlepsze rozwiązania dotyczące zadania elastycznej bazy danych obejmują:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="eb7b8-219">Ogranicz użycie hello interfejsów API tootrusted osób.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-219">Limit usage of hello APIs tootrusted individuals.</span></span>
* <span data-ttu-id="eb7b8-220">Poświadczenia powinny mieć hello co najmniej zadanie hello tooperform niezbędne uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-220">Credentials should have hello least privileges necessary tooperform hello job task.</span></span>  <span data-ttu-id="eb7b8-221">Więcej informacji, można wyświetlić w ramach tego [autoryzacji i uprawnienia](https://msdn.microsoft.com/library/bb669084.aspx) artykuł w witrynie MSDN programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="eb7b8-222">toocreate zaszyfrowane poświadczenia do wykonywania zadań dla baz danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-222">toocreate an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="eb7b8-223">toocreate nową szyfrowane poświadczeń, hello [ **polecenia cmdlet Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) monit o podanie nazwy użytkownika i hasło, które mogą zostać przekazane toohello [ **AzureSqlJobCredential nowy polecenia cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span><span class="sxs-lookup"><span data-stu-id="eb7b8-223">toocreate a new encrypted credential, hello [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed toohello [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a><span data-ttu-id="eb7b8-224">poświadczenia tooupdate</span><span class="sxs-lookup"><span data-stu-id="eb7b8-224">tooupdate credentials</span></span>
<span data-ttu-id="eb7b8-225">Po zmianie hasła, należy użyć hello [ **polecenia cmdlet Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) i zestaw hello **CredentialName** parametru.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-225">When passwords change, use hello [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set hello **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a><span data-ttu-id="eb7b8-226">toodefine obiektu docelowego mapy niezależnego fragmentu elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-226">toodefine an Elastic Database shard map target</span></span>
<span data-ttu-id="eb7b8-227">tooexecute zadania dla wszystkich baz danych w zestawie niezależnego fragmentu (utworzone za pomocą [biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md)), użyj mapy niezależnego fragmentu jako hello docelowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-227">tooexecute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as hello database target.</span></span> <span data-ttu-id="eb7b8-228">W tym przykładzie wymaga podzielonej aplikacji utworzony za pomocą biblioteki klienta elastycznej bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-228">This example requires a sharded application created using hello Elastic Database client library.</span></span> <span data-ttu-id="eb7b8-229">Zobacz [wprowadzenie próbki narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eb7b8-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="eb7b8-230">Hello niezależnego fragmentu Mapa menedżera z bazy danych musi być ustawiona jako docelowej bazy danych, a opcja hello mapy określonych niezależnego fragmentu musi być określona jako miejsce docelowe.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-230">hello shard map manager database must be set as a database target and then hello specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="eb7b8-231">Tworzenie skryptu T-SQL do wykonania dla baz danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="eb7b8-232">Podczas tworzenia skryptów T-SQL do wykonania, zdecydowanie zaleca się toobuild je toobe [idempotentności](https://en.wikipedia.org/wiki/Idempotence) i odporne na błędy.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-232">When creating T-SQL scripts for execution, it is highly recommended toobuild them toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="eb7b8-233">Zadania elastyczne bazy danych ponowi wykonanie skryptu zawsze, gdy wykonanie napotka błąd, niezależnie od klasyfikacji hello hello awarii.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of hello classification of hello failure.</span></span>

<span data-ttu-id="eb7b8-234">Użyj hello [ **polecenia cmdlet New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate i zapisać skrypt do wykonania i ustaw hello **- ContentName** i **- CommandText**parametrów.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-234">Use hello [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate and save a script for execution and set hello **-ContentName** and **-CommandText** parameters.</span></span>

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="eb7b8-235">Utwórz nowy skrypt z pliku</span><span class="sxs-lookup"><span data-stu-id="eb7b8-235">Create a new script from a file</span></span>
<span data-ttu-id="eb7b8-236">Jeśli hello skryptu T-SQL jest zdefiniowany w pliku, należy użyć tego skryptu hello tooimport:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-236">If hello T-SQL script is defined within a file, use this tooimport hello script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="eb7b8-237">skrypt tooupdate T-SQL do wykonania dla baz danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-237">tooupdate a T-SQL script for execution across databases</span></span>
<span data-ttu-id="eb7b8-238">Tej aktualizacji skrypt programu PowerShell hello tekst polecenia T-SQL dla istniejącego skryptu.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-238">This PowerShell script updates hello T-SQL command text for an existing script.</span></span>

<span data-ttu-id="eb7b8-239">Następujące zmienne tooreflect hello hello zestaw żądaną zestaw toobe definicji skryptu:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-239">Set hello following variables tooreflect hello desired script definition toobe set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a><span data-ttu-id="eb7b8-240">tooupdate hello definicji tooan istniejącego skryptu</span><span class="sxs-lookup"><span data-stu-id="eb7b8-240">tooupdate hello definition tooan existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a><span data-ttu-id="eb7b8-241">toocreate tooexecute zadania skryptu w mapie niezależnego fragmentu</span><span class="sxs-lookup"><span data-stu-id="eb7b8-241">toocreate a job tooexecute a script across a shard map</span></span>
<span data-ttu-id="eb7b8-242">Ten skrypt programu PowerShell uruchamia zadania do wykonania skryptu w każdej niezależnego fragmentu w mapie niezależnego fragmentu elastycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="eb7b8-243">Następujące zmienne tooreflect hello hello zestaw żądaną skryptu i obiekt docelowy:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-243">Set hello following variables tooreflect hello desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a><span data-ttu-id="eb7b8-244">tooexecute zadania</span><span class="sxs-lookup"><span data-stu-id="eb7b8-244">tooexecute a job</span></span>
<span data-ttu-id="eb7b8-245">Ten skrypt programu PowerShell jest wykonywany istniejącego zadania:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="eb7b8-246">Aktualizacja hello następującej zmiennej tooreflect hello żądanego zadania nazwa toohave wykonane:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-246">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="eb7b8-247">Stan hello tooretrieve wykonywania pojedyncze zadanie</span><span class="sxs-lookup"><span data-stu-id="eb7b8-247">tooretrieve hello state of a single job execution</span></span>
<span data-ttu-id="eb7b8-248">Użyj hello [ **polecenia cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) i zestaw hello **JobExecutionId** parametru tooview hello stan wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-248">Use hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set hello **JobExecutionId** parameter tooview hello state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="eb7b8-249">Użyj hello sam **Get-AzureSqlJobExecution** polecenia cmdlet z hello **właściwość IncludeChildren** parametru tooview hello stan wykonania zadania podrzędne, czyli hello określonym stanie dla każdego wykonywania zadania w odniesieniu do każdego celem zadania hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-249">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a><span data-ttu-id="eb7b8-250">Stan hello tooview między wieloma wykonania zadania</span><span class="sxs-lookup"><span data-stu-id="eb7b8-250">tooview hello state across multiple job executions</span></span>
<span data-ttu-id="eb7b8-251">Witaj [ **polecenia cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) ma wiele parametrów opcjonalnych, które mogą być używane toodisplay wielu wykonania zadania, filtrowane przez hello podane parametry.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-251">hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="eb7b8-252">Hello poniżej przedstawiono niektóre hello możliwości toouse Get-AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-252">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="eb7b8-253">Pobierz wszystkie aktywne najwyższego poziomu zadanie wykonaniami:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="eb7b8-254">Pobierz wszystkie wykonaniami najwyższego poziomu zadania, w tym wykonaniami nieaktywnego zadania:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="eb7b8-255">Pobierz wszystkie wykonania zadania podrzędne identyfikatora wykonywania podane zadanie wykonaniami nieaktywnego zadania w tym:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="eb7b8-256">Pobierz wszystkie wykonania zadania utworzone za pomocą harmonogramu / zadania kombinacji, w tym nieaktywnych zadań:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="eb7b8-257">Pobieranie wszystkich zadań przeznaczonych dla określonej niezależnych mapy, w tym nieaktywnych zadań:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="eb7b8-258">Pobieranie wszystkich zadań przeznaczonych dla określonej kolekcji niestandardowych, łącznie z nieaktywnych zadań:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="eb7b8-259">Pobrać listy hello zadanie wykonania zadania w ramach wykonania określonego zadania:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-259">Retrieve hello list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="eb7b8-260">Pobieranie szczegółów wykonywania zadań zadania:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="eb7b8-261">Witaj następującego skryptu programu PowerShell może być używane tooview hello szczegóły zadania wykonywania zadań, które jest szczególnie przydatne w przypadku debugowania awarii wykonywania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-261">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a><span data-ttu-id="eb7b8-262">wykonania zadań tooretrieve błędów w ramach zadania</span><span class="sxs-lookup"><span data-stu-id="eb7b8-262">tooretrieve failures within job task executions</span></span>
<span data-ttu-id="eb7b8-263">Witaj **obiektu JobTaskExecution** zawiera właściwość dla cyklu życia hello zadania hello wraz z właściwością wiadomości.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-263">hello **JobTaskExecution object** includes a property for hello lifecycle of hello task along with a message property.</span></span> <span data-ttu-id="eb7b8-264">Jeśli wykonanie zadania zadania nie powiodło się, będzie można ustawić właściwości cyklu życia hello zbyt** i zostanie ustawiona właściwość wiadomości powitania toohello Wynikowy komunikat o wyjątku i jego stosu.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-264">If a job task execution failed, hello lifecycle property will be set too*Failed* and hello message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="eb7b8-265">Jeśli zadanie nie powiodło się, jest ważne tooview hello szczegóły zadania, których nie powiodła się dla danego zadania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-265">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a><span data-ttu-id="eb7b8-266">toowait dla toocomplete wykonania zadania</span><span class="sxs-lookup"><span data-stu-id="eb7b8-266">toowait for a job execution toocomplete</span></span>
<span data-ttu-id="eb7b8-267">Hello następującego skryptu programu PowerShell może być używane toowait dla toocomplete zadań zadania:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-267">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="eb7b8-268">Tworzenie zasad wykonywania niestandardowych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-268">Create a custom execution policy</span></span>
<span data-ttu-id="eb7b8-269">Zadania elastyczne bazy danych obsługuje tworzenie zasad wykonywania niestandardowych, które mogą być stosowane podczas uruchamiania zadania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="eb7b8-270">Zasady wykonywania obecnie umożliwiają definiowanie:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="eb7b8-271">Name: Identyfikator hello zasad wykonywania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-271">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="eb7b8-272">Limit czasu zadania: Całkowity czas przed zadania zostaną anulowane przez zadania elastyczne bazy danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="eb7b8-273">Interwał ponawiania prób początkowej: Interwał toowait przed ponowną próbą wykonania pierwszej.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-273">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="eb7b8-274">Maksymalny interwał ponawiania: Limit toouse interwałów ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-274">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="eb7b8-275">Współczynnik wycofywania interwału ponawiania: Współczynnik używany toocalculate hello dalej interwał między ponownymi próbami.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-275">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="eb7b8-276">Witaj używana jest następująca formuła: (początkowej interwał ponawiania próby) * Math.Pow — ((interwał wycofywania współczynnik) (liczba prób) - 2).</span><span class="sxs-lookup"><span data-stu-id="eb7b8-276">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="eb7b8-277">Maksymalna liczba prób: hello maksymalna liczba ponawiania prób tooperform w ramach danego zadania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-277">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="eb7b8-278">domyślne zasady wykonywania Hello używa hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-278">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="eb7b8-279">Nazwa: Domyślne zasady wykonywania</span><span class="sxs-lookup"><span data-stu-id="eb7b8-279">Name: Default execution policy</span></span>
* <span data-ttu-id="eb7b8-280">Limit czasu zadania: 1 tydzień</span><span class="sxs-lookup"><span data-stu-id="eb7b8-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="eb7b8-281">Interwał ponawiania prób początkowej: 100 milisekund</span><span class="sxs-lookup"><span data-stu-id="eb7b8-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="eb7b8-282">Maksymalny interwał ponawiania: 30 minut</span><span class="sxs-lookup"><span data-stu-id="eb7b8-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="eb7b8-283">Spróbuj ponownie współczynnik interwał: 2</span><span class="sxs-lookup"><span data-stu-id="eb7b8-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="eb7b8-284">Maksymalna liczba prób: 2 147 483 647</span><span class="sxs-lookup"><span data-stu-id="eb7b8-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="eb7b8-285">Tworzenie zasad wykonywania hello potrzeby:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-285">Create hello desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="eb7b8-286">Aktualizacja zasad wykonywania niestandardowych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-286">Update a custom execution policy</span></span>
<span data-ttu-id="eb7b8-287">Aktualizacja hello potrzeby tooupdate zasad wykonywania:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-287">Update hello desired execution policy tooupdate:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="eb7b8-288">Anulowanie zadania</span><span class="sxs-lookup"><span data-stu-id="eb7b8-288">Cancel a job</span></span>
<span data-ttu-id="eb7b8-289">Zadania elastyczne bazy danych obsługuje żądania anulowania zadań.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="eb7b8-290">Jeśli zadania elastyczne bazy danych wykryje żądanie anulowania aktualnie wykonywanego zadania, podejmie toostop hello zadania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="eb7b8-291">Istnieją dwa różne sposoby, że zadania elastyczne bazy danych można wykonać anulowania:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="eb7b8-292">Anuluj aktualnie wykonywanych zadań: wykrycie anulowania aktualnie uruchomionej zadania anulowania będą podejmowane w hello aktualnie wykonywanych aspekt hello zadań.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="eb7b8-293">Na przykład: w przypadku długo działające kwerendy obecnie wykonywana jest próba anulowania, nastąpi próba toocancel hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="eb7b8-294">Anulowanie zadań ponownych prób: w przypadku anulowania wykrycia przez wątek kontroli hello przed uruchomieniu zadania do wykonania, wątek kontroli hello będzie uniknąć uruchamiania zadań hello i zadeklarować żądania hello jak anulowane.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-294">Canceling task retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="eb7b8-295">Jeśli żądanie anulowania zadań dla zadania nadrzędnego, żądanie anulowania hello będą honorowane dla zadania nadrzędnego hello i wszystkich jego zadań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-295">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="eb7b8-296">toosubmit żądanie anulowania, użyj hello [ **polecenie cmdlet Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) i zestaw hello **JobExecutionId** parametru.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-296">toosubmit a cancellation request, use hello [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set hello **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="eb7b8-297">toodelete zadania i Historia zadania asynchronicznego</span><span class="sxs-lookup"><span data-stu-id="eb7b8-297">toodelete a job and job history asynchronously</span></span>
<span data-ttu-id="eb7b8-298">Zadania elastyczne bazy danych obsługuje asynchroniczne usuwania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="eb7b8-299">Zadanie może być oznaczony do usunięcia, a hello system spowoduje usunięcie hello zadania i jego historii zadań po zakończeniu wszystkich zadań wykonaniami hello zadania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-299">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="eb7b8-300">Witaj systemu nie będzie automatycznie anulowania wykonaniami aktywnego zadania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-300">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="eb7b8-301">Wywołanie [ **Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel wykonaniami aktywnego zadania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel active job executions.</span></span>

<span data-ttu-id="eb7b8-302">Usuwanie zadania tootrigger, użyj hello [ **polecenia cmdlet Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) i zestaw hello **JobName** parametru.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-302">tootrigger job deletion, use hello [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set hello **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a><span data-ttu-id="eb7b8-303">toocreate obiektu docelowego w niestandardowej bazie danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-303">toocreate a custom database target</span></span>
<span data-ttu-id="eb7b8-304">Można określić cele w niestandardowej bazie danych bezpośrednie wykonywanie lub dołączania w ramach grupy niestandardowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="eb7b8-305">Na przykład ponieważ **pule elastyczne** są nie jest jeszcze bezpośrednio obsługiwane przy użyciu interfejsów API środowiska PowerShell, można utworzyć obiekt docelowy w niestandardowej bazie danych oraz miejsca docelowego do kolekcji niestandardowej bazy danych, które obejmuje wszystkie hello bazy danych w puli hello.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="eb7b8-306">Ustaw hello następujące zmienne tooreflect hello potrzeby bazy danych:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-306">Set hello following variables tooreflect hello desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a><span data-ttu-id="eb7b8-307">toocreate docelowej kolekcji niestandardowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-307">toocreate a custom database collection target</span></span>
<span data-ttu-id="eb7b8-308">Użyj hello [ **AzureSqlJobTarget nowy** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) toodefine polecenia cmdlet w niestandardowej bazie danych kolekcji docelowej tooenable wykonywania przez wiele obiektów docelowych określonych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-308">Use hello [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine a custom database collection target tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="eb7b8-309">Po utworzeniu grupy bazy danych może być skojarzony z docelowym kolekcji niestandardowej hello baz danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-309">After creating a database group, databases can be associated with hello custom collection target.</span></span>

<span data-ttu-id="eb7b8-310">Ustaw powitania po konfiguracji docelowej żądanej kolekcji niestandardowych zmiennych tooreflect hello:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-310">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="eb7b8-311">tooadd baz danych tooa w niestandardowej bazie danych kolekcji docelowej</span><span class="sxs-lookup"><span data-stu-id="eb7b8-311">tooadd databases tooa custom database collection target</span></span>
<span data-ttu-id="eb7b8-312">tooadd bazy danych tooa określonej kolekcji niestandardowych Użyj hello [ **AzureSqlJobChildTarget Dodaj** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-312">tooadd a database tooa specific custom collection use hello [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="eb7b8-313">Przejrzyj hello bazy danych, w docelowej kolekcji niestandardowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-313">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="eb7b8-314">Użyj hello [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) polecenia cmdlet tooretrieve hello podrzędnej bazy danych, w docelowej kolekcji niestandardowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-314">Use hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="eb7b8-315">Utwórz skrypt tooexecute zadania w docelowej kolekcji niestandardowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-315">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="eb7b8-316">Użyj hello [ **AzureSqlJob nowy** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) toocreate polecenia cmdlet zadania przed grupę baz danych, wynika z docelowej kolekcji niestandardowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-316">Use hello [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="eb7b8-317">Zadania elastyczne bazy danych będzie rozszerzać hello zadania do wielu zadań podrzędnych każdego odpowiednia baza danych tooa skojarzone z hello w niestandardowej bazie danych kolekcji docelowych i upewnij się, że hello skrypt zostanie wykonany w każdej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-317">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="eb7b8-318">Ponownie ważne jest, że skrypty są odporne tooretries toobe idempotentności.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-318">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="eb7b8-319">Zbieranie danych dla baz danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-319">Data collection across databases</span></span>
<span data-ttu-id="eb7b8-320">Można użyć zadania tooexecute kwerendy między grupą baz danych i wysyłania hello wyniki tooa określonej tabeli.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-320">You can use a job tooexecute a query across a group of databases and send hello results tooa specific table.</span></span> <span data-ttu-id="eb7b8-321">Witaj tabeli może być badana po hello fakt toosee hello wyniki zapytania w każdej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-321">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="eb7b8-322">Zapewnia metody asynchronicznej tooexecute kwerendy przez wiele baz danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-322">This provides an asynchronous method tooexecute a query across many databases.</span></span> <span data-ttu-id="eb7b8-323">Nieudanych prób są obsługiwane automatycznie za pomocą ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="eb7b8-324">Hello określonej lokalizacji docelowej tabeli zostaną utworzone automatycznie, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-324">hello specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="eb7b8-325">nową tabelę Hello zgodny schemat hello hello zwrócił zestaw wyników.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-325">hello new table matches hello schema of hello returned result set.</span></span> <span data-ttu-id="eb7b8-326">Jeśli skrypt zwraca wiele zestawów wyników, zadania elastycznej bazy danych wysyła hello pierwszy toohello tabeli docelowej.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-326">If a script returns multiple result sets, Elastic Database jobs will only send hello first toohello destination table.</span></span>

<span data-ttu-id="eb7b8-327">Witaj następujący skrypt programu PowerShell wykonuje skrypt i zbiera jej wyników do określonej tabeli.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-327">hello following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="eb7b8-328">Ten skrypt zakłada, że skryptu T-SQL została utworzona który wyprowadza pojedynczy zestaw wyników i utworzono element docelowy kolekcji niestandardowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="eb7b8-329">Ten skrypt używa hello [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-329">This script uses hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="eb7b8-330">Ustawianie parametrów hello skryptu, poświadczeń i wykonywanie obiekt docelowy:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-330">Set hello parameters for script, credentials, and execution target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="eb7b8-331">toocreate, a następnie Rozpocznij zadania dla scenariuszy zbierania danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-331">toocreate and start a job for data collection scenarios</span></span>
<span data-ttu-id="eb7b8-332">Ten skrypt używa hello [ **Start AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-332">This script uses hello [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a><span data-ttu-id="eb7b8-333">tooschedule wyzwalacz wykonania zadania</span><span class="sxs-lookup"><span data-stu-id="eb7b8-333">tooschedule a job execution trigger</span></span>
<span data-ttu-id="eb7b8-334">Witaj następującego skryptu programu PowerShell może być używane toocreate za pomocą harmonogramu cyklicznego.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-334">hello following PowerShell script can be used toocreate a recurring schedule.</span></span> <span data-ttu-id="eb7b8-335">Ten skrypt używa przedział minuty, ale [ **AzureSqlJobSchedule nowy** ](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) obsługuje również parametry - DayInterval, - HourInterval i - MonthInterval, - WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="eb7b8-336">Można utworzyć harmonogramy, które są wykonywane tylko raz przekazywanie przez - jednorazowe.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="eb7b8-337">Utwórz nowy harmonogram:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="eb7b8-338">tootrigger zadania wykonywane zgodnie z harmonogramem czasu</span><span class="sxs-lookup"><span data-stu-id="eb7b8-338">tootrigger a job executed on a time schedule</span></span>
<span data-ttu-id="eb7b8-339">Wyzwalacz zadania mogą być zdefiniowane toohave zgodnie z zadania wykonywane harmonogram tooa.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-339">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="eb7b8-340">Witaj następującego skryptu programu PowerShell może być używane toocreate wyzwalacza zadania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-340">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="eb7b8-341">Użyj [AzureSqlJobTrigger nowy](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) i zestaw hello następujące zmienne toocorrespond toohello żądanego zadania i harmonogramu:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set hello following variables toocorrespond toohello desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="eb7b8-342">tooremove skojarzenia zaplanowane zadanie toostop wykonywanie zgodnie z harmonogramem</span><span class="sxs-lookup"><span data-stu-id="eb7b8-342">tooremove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="eb7b8-343">można usunąć toodiscontinue pojawiał wykonywania zadań za pomocą wyzwalacza zadania hello wyzwalacza zadania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-343">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span> <span data-ttu-id="eb7b8-344">Usuwanie zadania toostop wyzwalacz zadania wykonywane zgodnie z harmonogramem tooa przy użyciu hello [ **polecenia cmdlet Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span><span class="sxs-lookup"><span data-stu-id="eb7b8-344">Remove a job trigger toostop a job from being executed according tooa schedule using hello [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a><span data-ttu-id="eb7b8-345">Pobieranie zadania wyzwalaczy tooa powiązania harmonogramu</span><span class="sxs-lookup"><span data-stu-id="eb7b8-345">Retrieve job triggers bound tooa time schedule</span></span>
<span data-ttu-id="eb7b8-346">Witaj następującego skryptu programu PowerShell można tooobtain używane i wyświetlić hello zadania wyzwalaczy zarejestrowanych tooa określonego harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-346">hello following PowerShell script can be used tooobtain and display hello job triggers registered tooa particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a><span data-ttu-id="eb7b8-347">powiązane tooa wyzwalaczy zadanie tooretrieve</span><span class="sxs-lookup"><span data-stu-id="eb7b8-347">tooretrieve job triggers bound tooa job</span></span>
<span data-ttu-id="eb7b8-348">Użyj [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain i wyświetlić harmonogramy zawierający zarejestrowanych zadania.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="eb7b8-349">toocreate aplikacji warstwy danych (DACPAC) do wykonania dla baz danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-349">toocreate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="eb7b8-350">Zobacz toocreate DACPAC [aplikacji warstwy danych](https://msdn.microsoft.com/library/ee210546.aspx).</span><span class="sxs-lookup"><span data-stu-id="eb7b8-350">toocreate a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="eb7b8-351">toodeploy DACPAC, użyj hello [polecenia cmdlet New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span><span class="sxs-lookup"><span data-stu-id="eb7b8-351">toodeploy a DACPAC, use hello [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="eb7b8-352">Witaj DACPAC musi być dostępny toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-352">hello DACPAC must be accessible toohello service.</span></span> <span data-ttu-id="eb7b8-353">Jest zalecana tooupload utworzony tooAzure DACPAC magazynu i Utwórz [sygnatura dostępu współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md) dla hello DACPAC.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-353">It is recommended tooupload a created DACPAC tooAzure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for hello DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="eb7b8-354">tooupdate aplikacji warstwy danych (DACPAC) do wykonania dla baz danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-354">tooupdate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="eb7b8-355">Istniejące DACPACs zarejestrowanych w ramach zadania elastyczne bazy danych może być toonew toopoint zaktualizowanych identyfikatorów URI.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-355">Existing DACPACs registered within Elastic Database Jobs can be updated toopoint toonew URIs.</span></span> <span data-ttu-id="eb7b8-356">Użyj hello [ **polecenia cmdlet Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI na istniejącym zarejestrowany DACPAC:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-356">Use hello [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="eb7b8-357">toocreate tooapply zadania aplikacji warstwy danych (DACPAC) dla baz danych</span><span class="sxs-lookup"><span data-stu-id="eb7b8-357">toocreate a job tooapply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="eb7b8-358">Po utworzeniu DACPAC w ramach zadania elastyczne bazy danych, zadania mogą być tworzone tooapply hello DACPAC między grupą baz danych.</span><span class="sxs-lookup"><span data-stu-id="eb7b8-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created tooapply hello DACPAC across a group of databases.</span></span> <span data-ttu-id="eb7b8-359">Hello następującego skryptu programu PowerShell może być używane toocreate zadania DACPAC przez niestandardowy zbiór baz danych:</span><span class="sxs-lookup"><span data-stu-id="eb7b8-359">hello following PowerShell script can be used toocreate a DACPAC job across a custom collection of databases:</span></span>

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
