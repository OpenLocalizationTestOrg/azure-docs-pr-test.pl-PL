---
title: "Tworzenie i zarządzanie nimi przy użyciu programu PowerShell zadania elastyczne | Dokumentacja firmy Microsoft"
description: "Umożliwia Zarządzanie pulami bazy danych SQL Azure PowerShell"
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
ms.openlocfilehash: b4c97e8f51581f9a3f7c5a8d8e82562255fe7b48
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="bb9cb-103">Tworzenie i zarządzanie nimi zadania elastycznej bazy danych SQL przy użyciu programu PowerShell (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="bb9cb-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="bb9cb-104">Interfejsy API środowiska PowerShell dla **zadania elastycznej bazy danych** (w wersji zapoznawczej), umożliwiają definiowanie grupę baz danych, które wykona skryptów.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-104">The PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="bb9cb-105">W tym artykule przedstawiono sposób tworzenia i zarządzania nimi **zadania elastycznej bazy danych** przy użyciu poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-105">This article shows how to create and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="bb9cb-106">Zobacz [omówienie zadania elastyczne](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bb9cb-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bb9cb-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bb9cb-107">Prerequisites</span></span>
* <span data-ttu-id="bb9cb-108">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-108">An Azure subscription.</span></span> <span data-ttu-id="bb9cb-109">Bezpłatnej wersji próbnej, zobacz [bezpłatna miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bb9cb-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="bb9cb-110">Zestaw baz danych utworzonych przy użyciu narzędzi elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-110">A set of databases created with the Elastic Database tools.</span></span> <span data-ttu-id="bb9cb-111">Zobacz [wprowadzenie do narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bb9cb-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="bb9cb-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-112">Azure PowerShell.</span></span> <span data-ttu-id="bb9cb-113">Aby uzyskać szczegółowe informacje, zobacz artykuł [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview) (Instalowanie i konfigurowanie programu Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="bb9cb-113">For detailed information, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="bb9cb-114">**Zadania elastyczne bazy danych** pakietu programu PowerShell: zobacz [zadania instalowania elastycznej bazy danych](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="bb9cb-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="bb9cb-115">Wybierz subskrypcję platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bb9cb-115">Select your Azure subscription</span></span>
<span data-ttu-id="bb9cb-116">Aby wybrać subskrypcję należy identyfikator subskrypcji (**- SubscriptionId**) lub nazwę subskrypcji (**— Nazwa subskrypcji**).</span><span class="sxs-lookup"><span data-stu-id="bb9cb-116">To select the subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="bb9cb-117">Jeśli masz wiele subskrypcji możesz uruchomić **Get-AzureRmSubscription** polecenia cmdlet i skopiuj ustawić informacji o subskrypcji żądanego wyniku.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-117">If you have multiple subscriptions you can run the **Get-AzureRmSubscription** cmdlet and copy the desired subscription information from the result set.</span></span> <span data-ttu-id="bb9cb-118">Po uzyskaniu informacji o subskrypcji, uruchom następujące polecenia można ustawić jako domyślny, a mianowicie docelowych do tworzenia i zarządzania zadaniami tej subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-118">Once you have your subscription information, run the following commandlet to set this subscription as the default, namely the target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="bb9cb-119">[PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) jest zalecane w przypadku użycia w celu opracowywania i wykonywanie skryptów programu PowerShell dla zadania elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-119">The [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage to develop and execute PowerShell scripts against the Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="bb9cb-120">Obiekty zadania elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="bb9cb-121">W poniższej tabeli wymieniono się wszystkie typy obiektów z **zadania elastycznej bazy danych** wraz z jego opis i odpowiednich interfejsów API programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-121">The following table lists out all the object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="bb9cb-122">Typ obiektu</span><span class="sxs-lookup"><span data-stu-id="bb9cb-122">Object Type</span></span></th>
    <th><span data-ttu-id="bb9cb-123">Opis</span><span class="sxs-lookup"><span data-stu-id="bb9cb-123">Description</span></span></th>
    <th><span data-ttu-id="bb9cb-124">Powiązanych interfejsów API programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb9cb-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="bb9cb-125">Poświadczenie</span><span class="sxs-lookup"><span data-stu-id="bb9cb-125">Credential</span></span></td>
    <td><span data-ttu-id="bb9cb-126">Nazwa użytkownika i hasło do użycia podczas nawiązywania połączenia bazy danych dla wykonywania skryptów lub aplikacji DACPACs.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-126">Username and password to use when connecting to databases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="bb9cb-127">Hasło jest szyfrowane przed wysłaniem do i przechowywania w bazie danych zadania elastyczne bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-127">The password is encrypted before sending to and storing in the Elastic Database Jobs database.</span></span>  <span data-ttu-id="bb9cb-128">Hasło jest odszyfrowywany przez usługę zadania elastyczne bazy danych za pomocą poświadczeń utworzone i załadowane w skrypcie instalacji.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-128">The password is decrypted by the Elastic Database Jobs service via the credential created and uploaded from the installation script.</span></span></td>
    <td><p><span data-ttu-id="bb9cb-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="bb9cb-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="bb9cb-130">Nowe AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="bb9cb-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="bb9cb-131">Zestaw AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="bb9cb-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="bb9cb-132">Skrypt</span><span class="sxs-lookup"><span data-stu-id="bb9cb-132">Script</span></span></td>
    <td><span data-ttu-id="bb9cb-133">Skrypt języka Transact-SQL do użycia dla wykonania dla baz danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-133">Transact-SQL script to be used for execution across databases.</span></span>  <span data-ttu-id="bb9cb-134">Skrypt należy utworzone za idempotentności, ponieważ usługa ponowi wykonanie skryptu po awarii.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-134">The script should be authored to be idempotent since the service will retry execution of the script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="bb9cb-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="bb9cb-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="bb9cb-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="bb9cb-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="bb9cb-137">Nowe AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="bb9cb-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="bb9cb-138">Zestaw AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="bb9cb-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="bb9cb-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="bb9cb-139">DACPAC</span></span></td>
    <td><span data-ttu-id="bb9cb-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Aplikacji warstwy danych </a> pakietu, które mają być stosowane dla baz danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package to be applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="bb9cb-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="bb9cb-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="bb9cb-142">Nowe AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="bb9cb-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="bb9cb-143">Zestaw AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="bb9cb-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="bb9cb-144">Docelowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-144">Database Target</span></span></td>
    <td><span data-ttu-id="bb9cb-145">Nazwa bazy danych i serwera wskazujące bazę danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-145">Database and server name pointing to an Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="bb9cb-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="bb9cb-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="bb9cb-147">Nowe AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="bb9cb-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="bb9cb-148">Identyfikator niezależnego fragmentu mapy docelowego</span><span class="sxs-lookup"><span data-stu-id="bb9cb-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="bb9cb-149">Kombinacja docelowej bazy danych i poświadczeń ma być używany do określenia informacji przechowywanych w mapie niezależnego fragmentu elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-149">Combination of a database target and a credential to be used to determine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="bb9cb-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="bb9cb-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="bb9cb-151">Nowe AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="bb9cb-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="bb9cb-152">Zestaw AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="bb9cb-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="bb9cb-153">Docelowy kolekcji niestandardowej</span><span class="sxs-lookup"><span data-stu-id="bb9cb-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="bb9cb-154">Zdefiniowane grupy baz danych do zbiorczo użycia dla wykonania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-154">Defined group of databases to collectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="bb9cb-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="bb9cb-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="bb9cb-156">Nowe AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="bb9cb-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="bb9cb-157">Docelowy podrzędnej kolekcji niestandardowej</span><span class="sxs-lookup"><span data-stu-id="bb9cb-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="bb9cb-158">Obiekt docelowy bazy danych, do którego odwołuje się z kolekcji niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="bb9cb-159">Dodaj AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="bb9cb-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="bb9cb-160">Usuń AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="bb9cb-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="bb9cb-161">Zadanie</span><span class="sxs-lookup"><span data-stu-id="bb9cb-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="bb9cb-162">Definicja parametrów zadania, które mogą być używane do wyzwolenia wykonywania lub do zrealizowania planu.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-162">Definition of parameters for a job that can be used to trigger execution or to fulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="bb9cb-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="bb9cb-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="bb9cb-164">Nowe AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="bb9cb-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="bb9cb-165">Zestaw AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="bb9cb-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="bb9cb-166">Wykonanie zadania</span><span class="sxs-lookup"><span data-stu-id="bb9cb-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="bb9cb-167">Kontener zadania niezbędne do spełnienia wykonywania skryptu albo stosowania DACPAC do obiektu docelowego przy użyciu poświadczeń dla połączenia z bazą danych z błędami obsługiwane zgodnie z zasadami wykonywania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-167">Container of tasks necessary to fulfill either executing a script or applying a DACPAC to a target using credentials for database connections with failures handled in accordance to an execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="bb9cb-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="bb9cb-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="bb9cb-169">Start AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="bb9cb-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="bb9cb-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="bb9cb-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="bb9cb-171">AzureSqlJobExecution oczekiwania</span><span class="sxs-lookup"><span data-stu-id="bb9cb-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="bb9cb-172">Wykonywanie zadań zadania</span><span class="sxs-lookup"><span data-stu-id="bb9cb-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="bb9cb-173">Pojedynczą jednostkę pracy do wykonania zadania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-173">Single unit of work to fulfill a job.</span></span></p>
    <p><span data-ttu-id="bb9cb-174">Jeśli zadanie nie będzie mógł pomyślnie wykonać, będą rejestrowane Wynikowy komunikat o wyjątku i nowe zadanie zgodne, zostanie utworzona i wykonywane zgodnie z zasadami wykonywania określonej.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-174">If a job task is not able to successfully execute, the resulting exception message will be logged and a new matching job task will be created and executed in accordance to the specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="bb9cb-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="bb9cb-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="bb9cb-176">Start AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="bb9cb-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="bb9cb-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="bb9cb-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="bb9cb-178">AzureSqlJobExecution oczekiwania</span><span class="sxs-lookup"><span data-stu-id="bb9cb-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="bb9cb-179">Zasady wykonywania zadania</span><span class="sxs-lookup"><span data-stu-id="bb9cb-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="bb9cb-180">Formanty zadań limitów czasu wykonywania, ponownych prób, ograniczenia i odstępach czasu między kolejnymi próbami.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="bb9cb-181">Zadania elastyczne bazy danych zawiera domyślne zasady wykonywania zadania, które zasadniczo nieskończone ponowne próby niepowodzeń zadań zadania z wykładniczego wycofywania odstępach czasu między kolejnymi próbami.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="bb9cb-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="bb9cb-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="bb9cb-183">Nowe AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="bb9cb-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="bb9cb-184">Zestaw AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="bb9cb-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="bb9cb-185">Harmonogram</span><span class="sxs-lookup"><span data-stu-id="bb9cb-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="bb9cb-186">Czas na podstawie specyfikacji wykonywania odbywać się w przedziale reoccurring lub w danym momencie.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-186">Time based specification for execution to take place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="bb9cb-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="bb9cb-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="bb9cb-188">Nowe AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="bb9cb-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="bb9cb-189">Zestaw AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="bb9cb-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="bb9cb-190">Wyzwala zadanie</span><span class="sxs-lookup"><span data-stu-id="bb9cb-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="bb9cb-191">Mapowanie między zadania i harmonogramu wykonywania wyzwalacza zadania zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-191">A mapping between a job and a schedule to trigger job execution according to the schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="bb9cb-192">Nowe AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="bb9cb-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="bb9cb-193">Usuń AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="bb9cb-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="bb9cb-194">Obsługiwane zadania elastycznej bazy danych grupy typów</span><span class="sxs-lookup"><span data-stu-id="bb9cb-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="bb9cb-195">To zadanie wykonuje skrypty języka Transact-SQL (T-SQL) lub aplikacji DACPACs między grupą baz danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-195">The job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="bb9cb-196">Po przesłaniu zadania do wykonania między grupą baz danych przez zadanie "rozszerza" do zadania podrzędne gdzie pełniących żądanego wykonanie jednej bazy danych w grupie.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-196">When a job is submitted to be executed across a group of databases, the job “expands” the into child jobs where each performs the requested execution against a single database in the group.</span></span> 

<span data-ttu-id="bb9cb-197">Istnieją dwa typy grup, które możesz utworzyć:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="bb9cb-198">[Mapa niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md) grupy: przesyłanej zadania docelową mapę niezależnego fragmentu zadanie odpytuje mapy niezależnego fragmentu określenie jego bieżącego zestawu odłamków, a następnie zadania dla każdego niezależnego fragmentu tworzy podrzędnego, na mapie niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted to target a shard map, the job queries the shard map to determine its current set of shards, and then creates child jobs for each shard in the shard map.</span></span>
* <span data-ttu-id="bb9cb-199">Niestandardowe grupy zbierania: niestandardowy zdefiniowany zestaw baz danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="bb9cb-200">Gdy zadanie jest przeznaczony dla kolekcji niestandardowych, tworzy podrzędnych zadania dla każdej bazy danych obecnie w kolekcji niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-200">When a job targets a custom collection, it creates child jobs for each database currently in the custom collection.</span></span>

## <a name="to-set-the-elastic-database-jobs-connection"></a><span data-ttu-id="bb9cb-201">Aby ustawić elastycznej bazy danych zadania połączeń</span><span class="sxs-lookup"><span data-stu-id="bb9cb-201">To set the Elastic Database jobs connection</span></span>
<span data-ttu-id="bb9cb-202">Połączenie musi być ustawiona na zadania *bazy danych kontroli* przed użyciem zadania interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-202">A connection needs to be set to the jobs *control database* prior to using the jobs APIs.</span></span> <span data-ttu-id="bb9cb-203">Uruchomienie tego polecenia cmdlet wyzwala okno poświadczeń przeskoczyć do góry żądania nazwy użytkownika i hasła utworzonego podczas instalacji zadania elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-203">Running this cmdlet triggers a credential window to pop up requesting the user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="bb9cb-204">Wszystkie przykłady w tym temacie założono, że pierwsza została już wykonana.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="bb9cb-205">Otwórz połączenie zadania elastycznej bazy danych:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-205">Open a connection to the Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-the-elastic-database-jobs"></a><span data-ttu-id="bb9cb-206">Zaszyfrowane poświadczenia w ramach zadania elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-206">Encrypted credentials within the Elastic Database jobs</span></span>
<span data-ttu-id="bb9cb-207">Poświadczenia bazy danych można wstawiać do zadania *bazy danych kontroli* jego hasłem, szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-207">Database credentials can be inserted into the jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="bb9cb-208">Należy zapisać poświadczenia na potrzeby uruchomienia zadania do wykonania w późniejszym czasie (przy użyciu harmonogramy zadań).</span><span class="sxs-lookup"><span data-stu-id="bb9cb-208">It is necessary to store credentials to enable jobs to be executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="bb9cb-209">Szyfrowanie działa za pośrednictwem utworzone jako część skrypt instalacji certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-209">Encryption works through a certificate created as part of the installation script.</span></span> <span data-ttu-id="bb9cb-210">Skrypt instalacji tworzy i wysyła certyfikat do usługi w chmurze Azure do odszyfrowywania przechowywane hasła szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-210">The installation script creates and uploads the certificate into the Azure Cloud Service for decryption of the stored encrypted passwords.</span></span> <span data-ttu-id="bb9cb-211">Usługi w chmurze Azure później przechowuje klucz publiczny w ramach zadania *bazy danych kontroli* co pozwala interfejsu API programu PowerShell lub klasycznego portalu Azure do zaszyfrowania podanego hasła bez konieczności certyfikatu lokalnie zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-211">The Azure Cloud Service later stores the public key within the jobs *control database* which enables the PowerShell API or Azure Classic Portal interface to encrypt a provided password without requiring the certificate to be locally installed.</span></span>

<span data-ttu-id="bb9cb-212">Hasła poświadczenia są szyfrowane i bezpieczne od użytkowników z dostępem tylko do odczytu do obiektów zadania elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-212">The credential passwords are encrypted and secure from users with read-only access to Elastic Database jobs objects.</span></span> <span data-ttu-id="bb9cb-213">Ale istnieje możliwość, że złośliwy użytkownik z dostępem do odczytu i zapisu do obiektów zadania elastyczne bazy danych można wyodrębnić hasła.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-213">But it is possible for a malicious user with read-write access to Elastic Database Jobs objects to extract a password.</span></span> <span data-ttu-id="bb9cb-214">Poświadczenia są przeznaczone do ponownie wykorzystać w odniesieniu do wykonania zadania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-214">Credentials are designed to be reused across job executions.</span></span> <span data-ttu-id="bb9cb-215">Poświadczenia są przekazywane do docelowej bazy danych podczas ustanawiania połączenia.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-215">Credentials are passed to target databases when establishing connections.</span></span> <span data-ttu-id="bb9cb-216">Obecnie nie istnieją żadne ograniczenia dotyczące z docelowymi bazami danych używane dla każdego poświadczenia, złośliwy użytkownik może dodać element docelowy bazy danych dla bazy danych pod kontrolą złośliwy użytkownik.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-216">There are currently no restrictions on the target databases used for each credential, malicious user could add a database target for a database under the malicious user's control.</span></span> <span data-ttu-id="bb9cb-217">Użytkownik może następnie uruchomić zadanie przeznaczonych dla tej bazy danych, aby uzyskać poświadczenia: hasło.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-217">The user could subsequently start a job targeting this database to gain the credential's password.</span></span>

<span data-ttu-id="bb9cb-218">Najlepsze rozwiązania dotyczące zadania elastycznej bazy danych obejmują:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="bb9cb-219">Ogranicz użycie interfejsów API do zaufanych osób.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-219">Limit usage of the APIs to trusted individuals.</span></span>
* <span data-ttu-id="bb9cb-220">Poświadczenia ma co najmniej uprawnienia niezbędne do wykonania zadanie.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-220">Credentials should have the least privileges necessary to perform the job task.</span></span>  <span data-ttu-id="bb9cb-221">Więcej informacji, można wyświetlić w ramach tego [autoryzacji i uprawnienia](https://msdn.microsoft.com/library/bb669084.aspx) artykuł w witrynie MSDN programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="to-create-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="bb9cb-222">Aby utworzyć zaszyfrowany poświadczeń do wykonywania zadań dla baz danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-222">To create an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="bb9cb-223">Aby utworzyć nowe poświadczenie zaszyfrowane, [ **polecenia cmdlet Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) monit o podanie nazwy użytkownika i hasło, które mogą zostać przekazane do [ **polecenia cmdlet New-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span><span class="sxs-lookup"><span data-stu-id="bb9cb-223">To create a new encrypted credential, the [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed to the [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="to-update-credentials"></a><span data-ttu-id="bb9cb-224">Aby zaktualizować poświadczenia</span><span class="sxs-lookup"><span data-stu-id="bb9cb-224">To update credentials</span></span>
<span data-ttu-id="bb9cb-225">Po zmianie hasła, użyj [ **polecenia cmdlet Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) i ustaw **CredentialName** parametru.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-225">When passwords change, use the [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set the **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="to-define-an-elastic-database-shard-map-target"></a><span data-ttu-id="bb9cb-226">Aby określić obiekt docelowy mapy niezależnego fragmentu elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-226">To define an Elastic Database shard map target</span></span>
<span data-ttu-id="bb9cb-227">Do wykonania zadania wszystkich baz danych w zestawie niezależnego fragmentu (utworzone za pomocą [biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md)), użyć mapy niezależnego fragmentu jako element docelowy bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-227">To execute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as the database target.</span></span> <span data-ttu-id="bb9cb-228">W tym przykładzie wymaga podzielonej aplikacji utworzony za pomocą biblioteki klienta elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-228">This example requires a sharded application created using the Elastic Database client library.</span></span> <span data-ttu-id="bb9cb-229">Zobacz [wprowadzenie próbki narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bb9cb-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="bb9cb-230">Bazy danych Menedżera mapy niezależnego fragmentu musi być ustawiona jako docelowej bazy danych, a opcja mapy określonych niezależnego fragmentu musi być określona jako miejsce docelowe.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-230">The shard map manager database must be set as a database target and then the specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="bb9cb-231">Tworzenie skryptu T-SQL do wykonania dla baz danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="bb9cb-232">Podczas tworzenia skryptów T-SQL do wykonania, zdecydowanie zaleca się tworzenie [idempotentności](https://en.wikipedia.org/wiki/Idempotence) i odporne na błędy.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-232">When creating T-SQL scripts for execution, it is highly recommended to build them to be [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="bb9cb-233">Zadania elastyczne bazy danych ponowi wykonanie skryptu zawsze, gdy wykonanie napotka błąd, niezależnie od klasyfikacji błędu.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of the classification of the failure.</span></span>

<span data-ttu-id="bb9cb-234">Użyj [ **polecenia cmdlet New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) Aby utworzyć i zapisać skrypt do wykonania i zestaw **- ContentName** i **- CommandText** Parametry.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-234">Use the [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) to create and save a script for execution and set the **-ContentName** and **-CommandText** parameters.</span></span>

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

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="bb9cb-235">Utwórz nowy skrypt z pliku</span><span class="sxs-lookup"><span data-stu-id="bb9cb-235">Create a new script from a file</span></span>
<span data-ttu-id="bb9cb-236">Jeśli skryptu T-SQL jest zdefiniowany w pliku, służy do importowania skrypt:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-236">If the T-SQL script is defined within a file, use this to import the script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path to SQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="to-update-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="bb9cb-237">Aby zaktualizować skryptu T-SQL do wykonania dla baz danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-237">To update a T-SQL script for execution across databases</span></span>
<span data-ttu-id="bb9cb-238">Ten skrypt programu PowerShell aktualizuje tekst polecenia T-SQL dla istniejącego skryptu.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-238">This PowerShell script updates the T-SQL command text for an existing script.</span></span>

<span data-ttu-id="bb9cb-239">Ustaw następujące zmienne, aby odzwierciedlić definicji żądaną skryptu należy ustawić wartość:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-239">Set the following variables to reflect the desired script definition to be set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column to TestTable"
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

### <a name="to-update-the-definition-to-an-existing-script"></a><span data-ttu-id="bb9cb-240">Aby zaktualizować definicję do istniejącego skryptu</span><span class="sxs-lookup"><span data-stu-id="bb9cb-240">To update the definition to an existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="to-create-a-job-to-execute-a-script-across-a-shard-map"></a><span data-ttu-id="bb9cb-241">Aby utworzyć zadanie do wykonania skryptu w mapie niezależnego fragmentu</span><span class="sxs-lookup"><span data-stu-id="bb9cb-241">To create a job to execute a script across a shard map</span></span>
<span data-ttu-id="bb9cb-242">Ten skrypt programu PowerShell uruchamia zadania do wykonania skryptu w każdej niezależnego fragmentu w mapie niezależnego fragmentu elastycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="bb9cb-243">Ustaw następujące zmienne, aby odzwierciedlić żądaną skryptu i obiekt docelowy:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-243">Set the following variables to reflect the desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="to-execute-a-job"></a><span data-ttu-id="bb9cb-244">Do wykonania zadania</span><span class="sxs-lookup"><span data-stu-id="bb9cb-244">To execute a job</span></span>
<span data-ttu-id="bb9cb-245">Ten skrypt programu PowerShell jest wykonywany istniejącego zadania:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="bb9cb-246">Aktualizacja następującej zmiennej w celu odzwierciedlenia nazwa żądanego zadania zostały wykonane:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-246">Update the following variable to reflect the desired job name to have executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="to-retrieve-the-state-of-a-single-job-execution"></a><span data-ttu-id="bb9cb-247">Aby pobrać stan realizacji pojedyncze zadanie</span><span class="sxs-lookup"><span data-stu-id="bb9cb-247">To retrieve the state of a single job execution</span></span>
<span data-ttu-id="bb9cb-248">Użyj [ **polecenia cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) i ustaw **JobExecutionId** parametr, aby wyświetlić stan wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-248">Use the [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set the **JobExecutionId** parameter to view the state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="bb9cb-249">Używać tego samego **Get-AzureSqlJobExecution** polecenia cmdlet z **właściwość IncludeChildren** parametr, aby wyświetlić stan wykonania zadania podrzędne, czyli określonym stanie dla każdego wykonywania zadania dla każdej bazy danych Celem tego zadania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-249">Use the same **Get-AzureSqlJobExecution** cmdlet with the **IncludeChildren** parameter to view the state of child job executions, namely the specific state for each job execution against each database targeted by the job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="to-view-the-state-across-multiple-job-executions"></a><span data-ttu-id="bb9cb-250">Aby wyświetlić stan między wieloma wykonania zadania</span><span class="sxs-lookup"><span data-stu-id="bb9cb-250">To view the state across multiple job executions</span></span>
<span data-ttu-id="bb9cb-251">[ **Polecenia cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) ma wiele parametry opcjonalne, które mogą służyć do wyświetlania wielu wykonania zadania, filtrować za pomocą podanych parametrów.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-251">The [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used to display multiple job executions, filtered through the provided parameters.</span></span> <span data-ttu-id="bb9cb-252">Poniżej przedstawiono niektóre możliwe sposoby używania Get-AzureSqlJobExecution:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-252">The following demonstrates some of the possible ways to use Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="bb9cb-253">Pobierz wszystkie aktywne najwyższego poziomu zadanie wykonaniami:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="bb9cb-254">Pobierz wszystkie wykonaniami najwyższego poziomu zadania, w tym wykonaniami nieaktywnego zadania:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="bb9cb-255">Pobierz wszystkie wykonania zadania podrzędne identyfikatora wykonywania podane zadanie wykonaniami nieaktywnego zadania w tym:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="bb9cb-256">Pobierz wszystkie wykonania zadania utworzone za pomocą harmonogramu / zadania kombinacji, w tym nieaktywnych zadań:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="bb9cb-257">Pobieranie wszystkich zadań przeznaczonych dla określonej niezależnych mapy, w tym nieaktywnych zadań:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="bb9cb-258">Pobieranie wszystkich zadań przeznaczonych dla określonej kolekcji niestandardowych, łącznie z nieaktywnych zadań:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="bb9cb-259">Pobieranie listy zadanie wykonania zadania w ramach wykonania określonego zadania:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-259">Retrieve the list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="bb9cb-260">Pobieranie szczegółów wykonywania zadań zadania:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="bb9cb-261">Poniższy skrypt programu PowerShell może służyć do wyświetlania szczegółów zadania wykonywania zadania, które jest szczególnie przydatne w przypadku debugowania awarii wykonywania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-261">The following PowerShell script can be used to view the details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="to-retrieve-failures-within-job-task-executions"></a><span data-ttu-id="bb9cb-262">Można pobrać błędów w ramach zadania wykonania zadania</span><span class="sxs-lookup"><span data-stu-id="bb9cb-262">To retrieve failures within job task executions</span></span>
<span data-ttu-id="bb9cb-263">**Obiektu JobTaskExecution** zawiera właściwość dla cyklu życia zadania wraz z właściwością wiadomości.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-263">The **JobTaskExecution object** includes a property for the lifecycle of the task along with a message property.</span></span> <span data-ttu-id="bb9cb-264">Jeżeli wykonanie zadania zadania nie powiodło się, zostanie ustawiona właściwość cyklu życia do ** i będzie można ustawić właściwości wiadomości Wynikowy komunikat o wyjątku i jego stosu.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-264">If a job task execution failed, the lifecycle property will be set to *Failed* and the message property will be set to the resulting exception message and its stack.</span></span> <span data-ttu-id="bb9cb-265">Jeśli zadanie nie powiodło się, jest ważne wyświetlić szczegóły zadania, których nie powiodła się dla danego zadania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-265">If a job did not succeed, it is important to view the details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="to-wait-for-a-job-execution-to-complete"></a><span data-ttu-id="bb9cb-266">Oczekiwanie na ukończenie wykonywania zadania</span><span class="sxs-lookup"><span data-stu-id="bb9cb-266">To wait for a job execution to complete</span></span>
<span data-ttu-id="bb9cb-267">Poniższy skrypt programu PowerShell można czekać na ukończenie zadania zadania:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-267">The following PowerShell script can be used to wait for a job task to complete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="bb9cb-268">Tworzenie zasad wykonywania niestandardowych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-268">Create a custom execution policy</span></span>
<span data-ttu-id="bb9cb-269">Zadania elastyczne bazy danych obsługuje tworzenie zasad wykonywania niestandardowych, które mogą być stosowane podczas uruchamiania zadania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="bb9cb-270">Zasady wykonywania obecnie umożliwiają definiowanie:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="bb9cb-271">Nazwa: Identyfikator zasad wykonywania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-271">Name: Identifier for the execution policy.</span></span>
* <span data-ttu-id="bb9cb-272">Limit czasu zadania: Całkowity czas przed zadania zostaną anulowane przez zadania elastyczne bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="bb9cb-273">Początkowa interwału ponawiania prób: Interwał oczekiwania przed pierwszym ponów próbę.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-273">Initial Retry Interval: Interval to wait before first retry.</span></span>
* <span data-ttu-id="bb9cb-274">Maksymalny interwał ponawiania: Zakończenia interwałów ponawiania do użycia.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-274">Maximum Retry Interval: Cap of retry intervals to use.</span></span>
* <span data-ttu-id="bb9cb-275">Ponów próbę współczynnik wycofywania interwał: Współczynnik używane do obliczania następnego interwał między ponownymi próbami.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-275">Retry Interval Backoff Coefficient: Coefficient used to calculate the next interval between retries.</span></span>  <span data-ttu-id="bb9cb-276">Używana jest następująca formuła: (początkowej interwał ponawiania próby) * Math.Pow — ((interwał wycofywania współczynnik) (liczba prób) - 2).</span><span class="sxs-lookup"><span data-stu-id="bb9cb-276">The following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="bb9cb-277">Maksymalna liczba prób: Maksymalną liczbę ponownych prób do wykonania w ramach danego zadania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-277">Maximum Attempts: The maximum number of retry attempts to perform within a job.</span></span>

<span data-ttu-id="bb9cb-278">Domyślne zasady wykonywania korzysta z następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-278">The default execution policy uses the following values:</span></span>

* <span data-ttu-id="bb9cb-279">Nazwa: Domyślne zasady wykonywania</span><span class="sxs-lookup"><span data-stu-id="bb9cb-279">Name: Default execution policy</span></span>
* <span data-ttu-id="bb9cb-280">Limit czasu zadania: 1 tydzień</span><span class="sxs-lookup"><span data-stu-id="bb9cb-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="bb9cb-281">Interwał ponawiania prób początkowej: 100 milisekund</span><span class="sxs-lookup"><span data-stu-id="bb9cb-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="bb9cb-282">Maksymalny interwał ponawiania: 30 minut</span><span class="sxs-lookup"><span data-stu-id="bb9cb-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="bb9cb-283">Spróbuj ponownie współczynnik interwał: 2</span><span class="sxs-lookup"><span data-stu-id="bb9cb-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="bb9cb-284">Maksymalna liczba prób: 2 147 483 647</span><span class="sxs-lookup"><span data-stu-id="bb9cb-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="bb9cb-285">Tworzenie zasad wykonywania żądanego:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-285">Create the desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="bb9cb-286">Aktualizacja zasad wykonywania niestandardowych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-286">Update a custom execution policy</span></span>
<span data-ttu-id="bb9cb-287">Aktualizacja zasad wykonywania żądanej aktualizacji:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-287">Update the desired execution policy to update:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="bb9cb-288">Anulowanie zadania</span><span class="sxs-lookup"><span data-stu-id="bb9cb-288">Cancel a job</span></span>
<span data-ttu-id="bb9cb-289">Zadania elastyczne bazy danych obsługuje żądania anulowania zadań.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="bb9cb-290">Jeśli zadania elastyczne bazy danych wykryje żądanie anulowania aktualnie wykonywanego zadania, spróbuje zatrzymać zadanie.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt to stop the job.</span></span>

<span data-ttu-id="bb9cb-291">Istnieją dwa różne sposoby, że zadania elastyczne bazy danych można wykonać anulowania:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="bb9cb-292">Anuluj aktualnie wykonywanych zadań: wykrycie anulowania aktualnie uruchomionej zadania anulowania będą podejmowane w aspekcie aktualnie wykonywanego zadania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within the currently executing aspect of the task.</span></span>  <span data-ttu-id="bb9cb-293">Na przykład: w przypadku długo działające kwerendy obecnie wykonywana jest próba anulowania, nastąpi próba anulować wykonywanie zapytania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt to cancel the query.</span></span>
2. <span data-ttu-id="bb9cb-294">Anulowanie zadań ponownych prób: w przypadku anulowania wykrycia przez wątek kontroli przed uruchomieniu zadania do wykonania, wątku formant będzie uniknąć uruchamiania zadania i zadeklarować żądania jako anulowane.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-294">Canceling task retries: If a cancellation is detected by the control thread before a task is launched for execution, the control thread will avoid launching the task and declare the request as canceled.</span></span>

<span data-ttu-id="bb9cb-295">Jeśli żądanie anulowania zadań dla zadania nadrzędnego, żądanie anulowania będą honorowane dla zadania nadrzędnego i wszystkich jego zadań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-295">If a job cancellation is requested for a parent job, the cancellation request will be honored for the parent job and for all of its child jobs.</span></span>

<span data-ttu-id="bb9cb-296">Aby przesłać żądanie anulowania, użyj [ **polecenie cmdlet Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) i ustaw **JobExecutionId** parametru.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-296">To submit a cancellation request, use the [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set the **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="to-delete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="bb9cb-297">Aby usunąć zadania i Historia zadania asynchronicznego</span><span class="sxs-lookup"><span data-stu-id="bb9cb-297">To delete a job and job history asynchronously</span></span>
<span data-ttu-id="bb9cb-298">Zadania elastyczne bazy danych obsługuje asynchroniczne usuwania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="bb9cb-299">Zadanie może być oznaczony do usunięcia, a system spowoduje usunięcie zadania i jego historii zadań po zakończeniu wszystkich wykonania zadań dla zadania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-299">A job can be marked for deletion and the system will delete the job and all its job history after all job executions have completed for the job.</span></span> <span data-ttu-id="bb9cb-300">System nie zostanie automatycznie anulowania wykonaniami aktywnego zadania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-300">The system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="bb9cb-301">Wywołanie [ **Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) anulować wykonaniami aktywnego zadania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) to cancel active job executions.</span></span>

<span data-ttu-id="bb9cb-302">Aby wyzwolić usunięcia zadania, należy użyć [ **polecenia cmdlet Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) i ustaw **JobName** parametru.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-302">To trigger job deletion, use the [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set the **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="to-create-a-custom-database-target"></a><span data-ttu-id="bb9cb-303">Aby utworzyć cel w niestandardowej bazie danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-303">To create a custom database target</span></span>
<span data-ttu-id="bb9cb-304">Można określić cele w niestandardowej bazie danych bezpośrednie wykonywanie lub dołączania w ramach grupy niestandardowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="bb9cb-305">Na przykład ponieważ **pule elastyczne** są nie jest jeszcze bezpośrednio obsługiwane przy użyciu interfejsów API środowiska PowerShell, można utworzyć obiekt docelowy w niestandardowej bazie danych oraz miejsca docelowego do kolekcji niestandardowej bazy danych, które obejmuje wszystkie bazy danych w puli.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all the databases in the pool.</span></span>

<span data-ttu-id="bb9cb-306">Ustaw następujące zmienne, aby odzwierciedlić informacje o żądanej bazy danych:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-306">Set the following variables to reflect the desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="to-create-a-custom-database-collection-target"></a><span data-ttu-id="bb9cb-307">Aby utworzyć cel kolekcji niestandardowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-307">To create a custom database collection target</span></span>
<span data-ttu-id="bb9cb-308">Użyj [ **AzureSqlJobTarget nowy** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) polecenia cmdlet, aby zdefiniować cel kolekcji niestandardowej bazy danych, aby umożliwiają wykonanie między wiele elementów docelowych określonych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-308">Use the [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet to define a custom database collection target to enable execution across multiple defined database targets.</span></span> <span data-ttu-id="bb9cb-309">Po utworzeniu grupy bazy danych może być skojarzony z elementem docelowym kolekcji niestandardowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-309">After creating a database group, databases can be associated with the custom collection target.</span></span>

<span data-ttu-id="bb9cb-310">Ustaw następujące zmienne w celu uwzględnienia konfiguracji docelowej żądanej kolekcji niestandardowych:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-310">Set the following variables to reflect the desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="to-add-databases-to-a-custom-database-collection-target"></a><span data-ttu-id="bb9cb-311">Aby dodać bazy danych do docelowej kolekcji niestandardowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-311">To add databases to a custom database collection target</span></span>
<span data-ttu-id="bb9cb-312">Aby dodać bazy danych do użycia określonej kolekcji niestandardowych [ **AzureSqlJobChildTarget Dodaj** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-312">To add a database to a specific custom collection use the [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-the-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="bb9cb-313">Przejrzyj baz danych w docelowej kolekcji niestandardowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-313">Review the databases within a custom database collection target</span></span>
<span data-ttu-id="bb9cb-314">Użyj [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) polecenia cmdlet, aby pobrać podrzędnej bazy danych w docelowej kolekcji niestandardowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-314">Use the [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet to retrieve the child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-to-execute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="bb9cb-315">Utwórz zadanie do wykonania skryptu w docelowej kolekcji niestandardowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-315">Create a job to execute a script across a custom database collection target</span></span>
<span data-ttu-id="bb9cb-316">Użyj [ **AzureSqlJob nowy** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) polecenia cmdlet można utworzyć zadania w odniesieniu do grupy baz danych, wynika z docelowej kolekcji niestandardowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-316">Use the [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet to create a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="bb9cb-317">Zadania elastyczne bazy danych będzie rozszerzyć zadanie do wielu zadań podrzędnych, odpowiadający każdej bazy danych skojarzony z elementem docelowym kolekcji niestandardowej bazy danych i upewnij się, że skrypt zostanie wykonany w każdej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-317">Elastic Database jobs will expand the job into multiple child jobs each corresponding to a database associated with the custom database collection target and ensure that the script is executed against each database.</span></span> <span data-ttu-id="bb9cb-318">Ponownie ważne jest, że skrypty są idempotentności pozwala uzyskać odporność na ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-318">Again, it is important that scripts are idempotent to be resilient to retries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="bb9cb-319">Zbieranie danych dla baz danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-319">Data collection across databases</span></span>
<span data-ttu-id="bb9cb-320">Zadania umożliwia wykonywanie zapytań przez grupę baz danych i wysyłać wyniki do określonej tabeli.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-320">You can use a job to execute a query across a group of databases and send the results to a specific table.</span></span> <span data-ttu-id="bb9cb-321">Tabela może być badana po fakcie, aby zobaczyć wyniki zapytania w każdej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-321">The table can be queried after the fact to see the query’s results from each database.</span></span> <span data-ttu-id="bb9cb-322">Zapewnia to metodę asynchroniczną, można wykonać kwerendy przez wiele baz danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-322">This provides an asynchronous method to execute a query across many databases.</span></span> <span data-ttu-id="bb9cb-323">Nieudanych prób są obsługiwane automatycznie za pomocą ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="bb9cb-324">Jeśli jeszcze nie istnieje w określonej lokalizacji docelowej tabeli zostanie automatycznie utworzona.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-324">The specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="bb9cb-325">Nowa tabela zgodny schemat zestaw wyników zwrócony.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-325">The new table matches the schema of the returned result set.</span></span> <span data-ttu-id="bb9cb-326">Jeśli skrypt zwraca wiele zestawów wyników, zadania elastycznej bazy danych wysyła pierwszy do tabeli docelowej.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-326">If a script returns multiple result sets, Elastic Database jobs will only send the first to the destination table.</span></span>

<span data-ttu-id="bb9cb-327">Poniższy skrypt programu PowerShell wykonuje skrypt i zbiera jej wyników do określonej tabeli.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-327">The following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="bb9cb-328">Ten skrypt zakłada, że skryptu T-SQL została utworzona który wyprowadza pojedynczy zestaw wyników i utworzono element docelowy kolekcji niestandardowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="bb9cb-329">Ten skrypt używa [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-329">This script uses the [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="bb9cb-330">Ustaw parametry skryptu, poświadczeń i wykonywanie obiekt docelowy:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-330">Set the parameters for script, credentials, and execution target:</span></span>

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

### <a name="to-create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="bb9cb-331">Aby utworzyć i uruchomić zadanie scenariusze zbierania danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-331">To create and start a job for data collection scenarios</span></span>
<span data-ttu-id="bb9cb-332">Ten skrypt używa [ **Start AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-332">This script uses the [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

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

## <a name="to-schedule-a-job-execution-trigger"></a><span data-ttu-id="bb9cb-333">Aby zaplanować zadanie wykonywania wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="bb9cb-333">To schedule a job execution trigger</span></span>
<span data-ttu-id="bb9cb-334">Poniższy skrypt programu PowerShell, można utworzyć za pomocą harmonogramu cyklicznego.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-334">The following PowerShell script can be used to create a recurring schedule.</span></span> <span data-ttu-id="bb9cb-335">Ten skrypt używa przedział minuty, ale [ **AzureSqlJobSchedule nowy** ](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) obsługuje również parametry - DayInterval, - HourInterval i - MonthInterval, - WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="bb9cb-336">Można utworzyć harmonogramy, które są wykonywane tylko raz przekazywanie przez - jednorazowe.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="bb9cb-337">Utwórz nowy harmonogram:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="to-trigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="bb9cb-338">Do wyzwalania zadania wykonywane zgodnie z harmonogramem czasu</span><span class="sxs-lookup"><span data-stu-id="bb9cb-338">To trigger a job executed on a time schedule</span></span>
<span data-ttu-id="bb9cb-339">Wyzwalacz zadania można definiować zadania wykonywane zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-339">A job trigger can be defined to have a job executed according to a time schedule.</span></span> <span data-ttu-id="bb9cb-340">Poniższy skrypt programu PowerShell, można utworzyć wyzwalacza zadania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-340">The following PowerShell script can be used to create a job trigger.</span></span>

<span data-ttu-id="bb9cb-341">Użyj [AzureSqlJobTrigger nowy](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) i ustaw następujące zmienne odpowiadają żądanego zadania i harmonogramu:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set the following variables to correspond to the desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="to-remove-a-scheduled-association-to-stop-job-from-executing-on-schedule"></a><span data-ttu-id="bb9cb-342">Aby usunąć skojarzenie zaplanowane zatrzymania zadania wykonywanie zgodnie z harmonogramem</span><span class="sxs-lookup"><span data-stu-id="bb9cb-342">To remove a scheduled association to stop job from executing on schedule</span></span>
<span data-ttu-id="bb9cb-343">Aby przerwać pojawiał wykonywania zadań za pomocą wyzwalacza zadania, można usunąć wyzwalacza zadania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-343">To discontinue reoccurring job execution through a job trigger, the job trigger can be removed.</span></span> <span data-ttu-id="bb9cb-344">Usuń wyzwalacz zadania zatrzymania zadania z wykonywana zgodnie z harmonogramem przy użyciu [ **polecenia cmdlet Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span><span class="sxs-lookup"><span data-stu-id="bb9cb-344">Remove a job trigger to stop a job from being executed according to a schedule using the [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-to-a-time-schedule"></a><span data-ttu-id="bb9cb-345">Pobrać wyzwalaczy zadania powiązane z harmonogramu</span><span class="sxs-lookup"><span data-stu-id="bb9cb-345">Retrieve job triggers bound to a time schedule</span></span>
<span data-ttu-id="bb9cb-346">Poniższy skrypt programu PowerShell mogą być używane do wyświetlić wyzwalacze zadania zarejestrowany z harmonogramem określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-346">The following PowerShell script can be used to obtain and display the job triggers registered to a particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="to-retrieve-job-triggers-bound-to-a-job"></a><span data-ttu-id="bb9cb-347">Można pobrać zadania wyzwalaczy powiązany z zadaniem</span><span class="sxs-lookup"><span data-stu-id="bb9cb-347">To retrieve job triggers bound to a job</span></span>
<span data-ttu-id="bb9cb-348">Użyj [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) do wyświetlenia harmonogramy zawierający zarejestrowane zadania.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) to obtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="to-create-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="bb9cb-349">Aby utworzyć aplikację warstwy danych (DACPAC) do wykonania dla baz danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-349">To create a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="bb9cb-350">Aby utworzyć DACPAC, zobacz [aplikacji warstwy danych](https://msdn.microsoft.com/library/ee210546.aspx).</span><span class="sxs-lookup"><span data-stu-id="bb9cb-350">To create a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="bb9cb-351">Aby wdrożyć DACPAC, należy użyć [polecenia cmdlet New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span><span class="sxs-lookup"><span data-stu-id="bb9cb-351">To deploy a DACPAC, use the [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="bb9cb-352">DACPAC muszą być dostępne dla usługi.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-352">The DACPAC must be accessible to the service.</span></span> <span data-ttu-id="bb9cb-353">Zaleca się wysłanie utworzony DACPAC do magazynu Azure i utworzyć [sygnatura dostępu współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md) dla DACPAC.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-353">It is recommended to upload a created DACPAC to Azure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for the DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="to-update-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="bb9cb-354">Do aktualizacji aplikacji warstwy danych (DACPAC) do wykonania dla baz danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-354">To update a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="bb9cb-355">Istniejących DACPACs zarejestrowanych w ramach zadania elastyczne bazy danych może zostać zaktualizowana, aby wskazywały nowy identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-355">Existing DACPACs registered within Elastic Database Jobs can be updated to point to new URIs.</span></span> <span data-ttu-id="bb9cb-356">Użyj [ **polecenia cmdlet Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) można zaktualizować identyfikatora URI DACPAC na istniejącym zarejestrowany DACPAC:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-356">Use the [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) to update the DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="to-create-a-job-to-apply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="bb9cb-357">Aby utworzyć zadanie, aby zastosować aplikacji warstwy danych (DACPAC) dla baz danych</span><span class="sxs-lookup"><span data-stu-id="bb9cb-357">To create a job to apply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="bb9cb-358">Po utworzeniu DACPAC w ramach zadania elastyczne bazy danych można utworzyć zadania do stosowania DACPAC na grupę baz danych.</span><span class="sxs-lookup"><span data-stu-id="bb9cb-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created to apply the DACPAC across a group of databases.</span></span> <span data-ttu-id="bb9cb-359">Poniższy skrypt programu PowerShell można utworzyć zadania DACPAC przez niestandardowy zbiór baz danych:</span><span class="sxs-lookup"><span data-stu-id="bb9cb-359">The following PowerShell script can be used to create a DACPAC job across a custom collection of databases:</span></span>

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
