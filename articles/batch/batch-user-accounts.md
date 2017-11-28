---
title: "zadania aaaRun na kontach użytkowników w partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Konfigurowanie kont użytkowników do uruchamiania zadań w partii zadań Azure"
services: batch
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.openlocfilehash: 13d7d76451d89a3cca090c4ef24ed0ed781bbf09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="2d69c-103">Uruchomienie zadania na kontach użytkowników w partii</span><span class="sxs-lookup"><span data-stu-id="2d69c-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="2d69c-104">Zadania w partii zadań Azure jest zawsze uruchamiany na koncie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2d69c-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="2d69c-105">Domyślnie zadania są uruchamiane na kontach użytkowników standardowych, bez uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="2d69c-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="2d69c-106">Domyślne ustawienia konta użytkownika są zwykle wystarczające.</span><span class="sxs-lookup"><span data-stu-id="2d69c-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="2d69c-107">W niektórych scenariuszach jednak jest przydatne toobe tooconfigure stanie hello konta użytkownika pod którym ma zostać toorun zadań.</span><span class="sxs-lookup"><span data-stu-id="2d69c-107">For certain scenarios, however, it's useful toobe able tooconfigure hello user account under which you want a task toorun.</span></span> <span data-ttu-id="2d69c-108">W tym artykule omówiono hello typy kont użytkowników i jak można je skonfigurować dla danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="2d69c-108">This article discusses hello types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="2d69c-109">Typy kont użytkowników</span><span class="sxs-lookup"><span data-stu-id="2d69c-109">Types of user accounts</span></span>

<span data-ttu-id="2d69c-110">Partia zadań Azure oferuje dwa typy kont użytkowników do uruchamiania zadań:</span><span class="sxs-lookup"><span data-stu-id="2d69c-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="2d69c-111">**Konta użytkowników automatycznie.**</span><span class="sxs-lookup"><span data-stu-id="2d69c-111">**Auto-user accounts.**</span></span> <span data-ttu-id="2d69c-112">Konta użytkowników automatycznie są wbudowane konta użytkowników, które są tworzone automatycznie przez hello usługa partia zadań.</span><span class="sxs-lookup"><span data-stu-id="2d69c-112">Auto-user accounts are built-in user accounts that are created automatically by hello Batch service.</span></span> <span data-ttu-id="2d69c-113">Domyślnie zadania są uruchamiane na koncie użytkownika automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2d69c-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="2d69c-114">Można skonfigurować hello specyfikacji użytkownika automatycznie tooindicate zadania, w którym użytkownik automatycznie uruchamiać zadania konta.</span><span class="sxs-lookup"><span data-stu-id="2d69c-114">You can configure hello auto-user specification for a task tooindicate under which auto-user account a task should run.</span></span> <span data-ttu-id="2d69c-115">Specyfikacja użytkownika automatycznie Hello pozwala toospecify hello podniesienie poziomu i zakres hello automatycznie użytkownika konta, które zostanie uruchomione zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="2d69c-115">hello auto-user specification allows you toospecify hello elevation level and scope of hello auto-user account that will run hello task.</span></span> 

- <span data-ttu-id="2d69c-116">**Konto użytkownika o nazwie.**</span><span class="sxs-lookup"><span data-stu-id="2d69c-116">**A named user account.**</span></span> <span data-ttu-id="2d69c-117">Podczas tworzenia puli hello można określić co najmniej jednego konta użytkownika o nazwie puli.</span><span class="sxs-lookup"><span data-stu-id="2d69c-117">You can specify one or more named user accounts for a pool when you create hello pool.</span></span> <span data-ttu-id="2d69c-118">Każde konto użytkownika jest tworzony w każdym węźle hello puli.</span><span class="sxs-lookup"><span data-stu-id="2d69c-118">Each user account is created on each node of hello pool.</span></span> <span data-ttu-id="2d69c-119">Ponadto toohello nazwa konta, określ hasło konta użytkownika hello, podniesienie poziomu, a w przypadku pul systemu Linux, klucza prywatnego SSH hello.</span><span class="sxs-lookup"><span data-stu-id="2d69c-119">In addition toohello account name, you specify hello user account password, elevation level, and, for Linux pools, hello SSH private key.</span></span> <span data-ttu-id="2d69c-120">Podczas dodawania zadania można określić hello o nazwie konta użytkownika, w którym to zadanie powinno być ono uruchomione.</span><span class="sxs-lookup"><span data-stu-id="2d69c-120">When you add a task, you can specify hello named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="2d69c-121">Witaj partii usługi wersji 2017-01-01.4.0 wprowadzono istotne zmiany wymaga aktualizacji toocall Twojego kod tej wersji.</span><span class="sxs-lookup"><span data-stu-id="2d69c-121">hello Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code toocall that version.</span></span> <span data-ttu-id="2d69c-122">W przypadku migrowania kodu ze starszej wersji partii należy pamiętać, że hello **runElevated** właściwość nie jest już obsługiwana w hello bibliotek klienta interfejsu API REST lub partii.</span><span class="sxs-lookup"><span data-stu-id="2d69c-122">If you are migrating code from an older version of Batch, note that hello **runElevated** property is no longer supported in hello REST API or Batch client libraries.</span></span> <span data-ttu-id="2d69c-123">Użyj hello nowe **tożsamości użytkownika** właściwości poziomu zadań toospecify podniesienia uprawnień.</span><span class="sxs-lookup"><span data-stu-id="2d69c-123">Use hello new **userIdentity** property of a task toospecify elevation level.</span></span> <span data-ttu-id="2d69c-124">Zobacz hello sekcji [zaktualizuj kod toohello najnowszego wsadu klienta biblioteki](#update-your-code-to-the-latest-batch-client-library) szybkie wytyczne dotyczące aktualizowanie kodu partii, jeśli używasz powitania klienta biblioteki.</span><span class="sxs-lookup"><span data-stu-id="2d69c-124">See hello section titled [Update your code toohello latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of hello client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="2d69c-125">konta użytkowników Hello omówione w tym artykule nie obsługują protokołu RDP (Remote Desktop) lub protokołu Secure Shell (SSH), ze względów bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="2d69c-125">hello user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="2d69c-126">tooconnect tooa węzła uruchomionych hello Linux konfiguracji maszyny wirtualnej za pośrednictwem protokołu SSH, zobacz [tooa pulpitu zdalnego użyj maszyny Wirtualnej systemu Linux na platformie Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="2d69c-126">tooconnect tooa node running hello Linux virtual machine configuration via SSH, see [Use Remote Desktop tooa Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="2d69c-127">toonodes tooconnect z systemem Windows za pomocą protokołu RDP, zobacz [połączyć tooa maszyny Wirtualnej systemu Windows Server](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="2d69c-127">tooconnect toonodes running Windows via RDP, see [Connect tooa Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="2d69c-128">tooconnect tooa węzła uruchomionych hello usługi konfiguracji chmury za pomocą protokołu RDP, zobacz [włączyć Podłączanie pulpitu zdalnego dla roli w usług Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2d69c-128">tooconnect tooa node running hello cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-toofiles-and-directories"></a><span data-ttu-id="2d69c-129">Toofiles dostępu do konta użytkownika i katalogów</span><span class="sxs-lookup"><span data-stu-id="2d69c-129">User account access toofiles and directories</span></span>

<span data-ttu-id="2d69c-130">Zarówno konto użytkownika automatycznie, jak i konto użytkownika o nazwie ma zadanie odczytu/zapisu dostępu toohello katalog roboczy, udostępniony katalog i katalog zadania wielu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="2d69c-130">Both an auto-user account and a named user account have read/write access toohello task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="2d69c-131">Oba typy kont mają dostęp do odczytu toohello uruchomienia zadania przygotowanie katalogów i.</span><span class="sxs-lookup"><span data-stu-id="2d69c-131">Both types of accounts have read access toohello startup and job preparation directories.</span></span>

<span data-ttu-id="2d69c-132">Jeśli zadanie jest uruchamiane hello samo konto, które zostało użyte do uruchomienia zadania uruchamiania, hello zadanie ma dostęp do odczytu zapisu toohello rozpoczęcia zadań katalog.</span><span class="sxs-lookup"><span data-stu-id="2d69c-132">If a task runs under hello same account that was used for running a start task, hello task has read-write access toohello start task directory.</span></span> <span data-ttu-id="2d69c-133">Podobnie, jeśli zadanie jest uruchamiane hello samo konto, które zostało użyte do uruchomienia zadania przygotowanie zadania, zadania hello ma dostęp do odczytu zapisu toohello zadanie przygotowanie zadania katalogu.</span><span class="sxs-lookup"><span data-stu-id="2d69c-133">Similarly, if a task runs under hello same account that was used for running a job preparation task, hello task has read-write access toohello job preparation task directory.</span></span> <span data-ttu-id="2d69c-134">Jeśli zadanie jest uruchamiane przy użyciu innego konta niż zadania uruchamiania hello lub zadanie przygotowanie zadania, zadania hello ma tylko dostęp do odczytu toohello odpowiednich katalogu.</span><span class="sxs-lookup"><span data-stu-id="2d69c-134">If a task runs under a different account than hello start task or job preparation task, then hello task has only read access toohello respective directory.</span></span>

<span data-ttu-id="2d69c-135">Aby uzyskać więcej informacji dotyczących uzyskiwania dostępu do plików i katalogów z zadania, zobacz [Programowanie równoległe na dużą skalę obliczeniowe rozwiązań w partii](batch-api-basics.md#files-and-directories).</span><span class="sxs-lookup"><span data-stu-id="2d69c-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="2d69c-136">Z podwyższonym poziomem uprawnień dostępu do zadania</span><span class="sxs-lookup"><span data-stu-id="2d69c-136">Elevated access for tasks</span></span> 

<span data-ttu-id="2d69c-137">konto użytkownika Hello podniesienie poziomu wskazuje, czy zadanie jest uruchamiane z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="2d69c-137">hello user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="2d69c-138">Zarówno konto użytkownika automatycznie, jak i konto użytkownika o nazwie można uruchomić z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="2d69c-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="2d69c-139">dostępne są następujące dwie opcje Hello podniesienie poziomu:</span><span class="sxs-lookup"><span data-stu-id="2d69c-139">hello two options for elevation level are:</span></span>

- <span data-ttu-id="2d69c-140">**NonAdmin:** hello zadanie jest uruchamiane jako użytkownik standardowy bez podwyższonego poziomu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2d69c-140">**NonAdmin:** hello task runs as a standard user without elevated access.</span></span> <span data-ttu-id="2d69c-141">Witaj domyślny poziom podniesienia uprawnień konta użytkownika usługi partia zadań jest zawsze **NonAdmin**.</span><span class="sxs-lookup"><span data-stu-id="2d69c-141">hello default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="2d69c-142">**Administrator:** hello zadań uruchamia jako użytkownik z podwyższonym poziomem uprawnień i działa z pełnymi uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="2d69c-142">**Admin:** hello task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="2d69c-143">Konta użytkowników automatycznie</span><span class="sxs-lookup"><span data-stu-id="2d69c-143">Auto-user accounts</span></span>

<span data-ttu-id="2d69c-144">Domyślnie zadania są uruchamiane w trybie wsadowym na koncie użytkownika automatycznie jako użytkownik standardowy bez podwyższonego poziomu dostępu i z zakresu zadań.</span><span class="sxs-lookup"><span data-stu-id="2d69c-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="2d69c-145">Po skonfigurowaniu specyfikacji użytkownika automatycznie hello zakresie zadania usługa partia zadań hello tworzy konta użytkownika automatycznie tylko tego zadania.</span><span class="sxs-lookup"><span data-stu-id="2d69c-145">When hello auto-user specification is configured for task scope, hello Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="2d69c-146">zakres tootask alternatywnych Hello jest zakres puli.</span><span class="sxs-lookup"><span data-stu-id="2d69c-146">hello alternative tootask scope is pool scope.</span></span> <span data-ttu-id="2d69c-147">Po skonfigurowaniu specyfikacji użytkownika automatycznie hello zadania dla zakresu puli hello zadanie jest uruchamiane jest zadanie tooany dostępne w puli hello z konta użytkownika automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2d69c-147">When hello auto-user specification for a task is configured for pool scope, hello task runs under an auto-user account that is available tooany task in hello pool.</span></span> <span data-ttu-id="2d69c-148">Aby uzyskać więcej informacji na temat zakresu puli, zobacz hello sekcji [uruchomienia zadania, jak hello auto użytkownika w zakresie puli](#run-a-task-as-the-autouser-with-pool-scope).</span><span class="sxs-lookup"><span data-stu-id="2d69c-148">For more information about pool scope, see hello section titled [Run a task as hello auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="2d69c-149">zakres domyślny Hello różni się w węzłach systemu Windows i Linux:</span><span class="sxs-lookup"><span data-stu-id="2d69c-149">hello default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="2d69c-150">W węzłach Windows zadania są uruchamiane w zakresie zadania domyślnie.</span><span class="sxs-lookup"><span data-stu-id="2d69c-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="2d69c-151">Węzły Linux są zawsze uruchamiane w zakresie puli.</span><span class="sxs-lookup"><span data-stu-id="2d69c-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="2d69c-152">Istnieją cztery konfiguracje możliwych do określenia użytkownika automatycznie hello, z których każdy odpowiada tooa unikatowe auto-konto użytkownika:</span><span class="sxs-lookup"><span data-stu-id="2d69c-152">There are four possible configurations for hello auto-user specification, each of which corresponds tooa unique auto-user account:</span></span>

- <span data-ttu-id="2d69c-153">Dostęp inni niż administratorzy z zakresem zadań (Specyfikacja hello domyślne użytkownika automatycznie)</span><span class="sxs-lookup"><span data-stu-id="2d69c-153">Non-admin access with task scope (hello default auto-user specification)</span></span>
- <span data-ttu-id="2d69c-154">Uprawnienia administratora (podwyższonymi) z zakresem zadań</span><span class="sxs-lookup"><span data-stu-id="2d69c-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="2d69c-155">Dostęp inni niż administratorzy z zakresem puli</span><span class="sxs-lookup"><span data-stu-id="2d69c-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="2d69c-156">Uprawnienia administratora w zakresie puli</span><span class="sxs-lookup"><span data-stu-id="2d69c-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="2d69c-157">Zadania uruchomione w zakresie zadania nie ma faktycznego zadań tooother dostępu w węźle.</span><span class="sxs-lookup"><span data-stu-id="2d69c-157">Tasks running under task scope do not have de facto access tooother tasks on a node.</span></span> <span data-ttu-id="2d69c-158">Jednak złośliwy użytkownik z kontem toohello dostępu można obejść to ograniczenie poprzez przesłanie zadanie, które jest uruchamiany z uprawnieniami administratora i uzyskuje dostęp do katalogów innych zadań.</span><span class="sxs-lookup"><span data-stu-id="2d69c-158">However, a malicious user with access toohello account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="2d69c-159">Złośliwy użytkownik można użyć również węzeł tooa tooconnect RDP lub SSH.</span><span class="sxs-lookup"><span data-stu-id="2d69c-159">A malicious user could also use RDP or SSH tooconnect tooa node.</span></span> <span data-ttu-id="2d69c-160">Jest ważne tooprotect dostępu tooyour partii konta klucze tooprevent takiej sytuacji.</span><span class="sxs-lookup"><span data-stu-id="2d69c-160">It's important tooprotect access tooyour Batch account keys tooprevent such a scenario.</span></span> <span data-ttu-id="2d69c-161">Jeśli podejrzewasz, że Twoje konto zostało naruszone, można tooregenerate się, że Twoje klucze.</span><span class="sxs-lookup"><span data-stu-id="2d69c-161">If you suspect your account may have been compromised, be sure tooregenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="2d69c-162">Uruchamianie zadania jako użytkownik automatycznie z podwyższonym poziomem uprawnień</span><span class="sxs-lookup"><span data-stu-id="2d69c-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="2d69c-163">Można skonfigurować hello specyfikacji automatycznie użytkownika uprawnień administratora, gdy potrzebujesz toorun zadania z podwyższonym poziomem uprawnień.</span><span class="sxs-lookup"><span data-stu-id="2d69c-163">You can configure hello auto-user specification for administrator privileges when you need toorun a task with elevated access.</span></span> <span data-ttu-id="2d69c-164">Na przykład może być konieczne zadania uruchamiania podwyższonego poziomu dostępu tooinstall oprogramowania w węźle hello.</span><span class="sxs-lookup"><span data-stu-id="2d69c-164">For example, a start task may need elevated access tooinstall software on hello node.</span></span>

> [!NOTE] 
> <span data-ttu-id="2d69c-165">Ogólnie rzecz biorąc, najlepiej jest toouse z podwyższonym poziomem uprawnień dostępu tylko wtedy, gdy jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2d69c-165">In general, it's best toouse elevated access only when necessary.</span></span> <span data-ttu-id="2d69c-166">Najlepszym rozwiązaniem jest przyznanie hello minimalne uprawnienia niezbędne tooachieve hello żądanego wyniku.</span><span class="sxs-lookup"><span data-stu-id="2d69c-166">Best practices recommend granting hello minimum privilege necessary tooachieve hello desired outcome.</span></span> <span data-ttu-id="2d69c-167">Na przykład zadania uruchamiania instalacji oprogramowania hello bieżącego użytkownika, a nie dla wszystkich użytkowników, może być możliwe tooavoid udzielanie tootasks podwyższonego poziomu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2d69c-167">For example, if a start task installs software for hello current user, instead of for all users, you may be able tooavoid granting elevated access tootasks.</span></span> <span data-ttu-id="2d69c-168">Można skonfigurować specyfikacji użytkownika automatycznie hello puli zakresu i bez uprawnień administratora dostępu dla wszystkich zadań wymagających toorun w obszarze hello tego samego konta, w tym hello rozpoczęcia zadań.</span><span class="sxs-lookup"><span data-stu-id="2d69c-168">You can configure hello auto-user specification for pool scope and non-admin access for all tasks that need toorun under hello same account, including hello start task.</span></span> 
>
>

<span data-ttu-id="2d69c-169">powitania po wstawki kodu pokazują, jak tooconfigure hello specyfikacji użytkownika automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2d69c-169">hello following code snippets show how tooconfigure hello auto-user specification.</span></span> <span data-ttu-id="2d69c-170">Przykłady Hello ustawić hello podniesienie poziomu także`Admin` i hello zakresu zbyt`Task`.</span><span class="sxs-lookup"><span data-stu-id="2d69c-170">hello examples set hello elevation level too`Admin` and hello scope too`Task`.</span></span> <span data-ttu-id="2d69c-171">Zakres zadań jest ustawienie domyślne hello, ale są przeznaczone dla zapewnienia hello przykład.</span><span class="sxs-lookup"><span data-stu-id="2d69c-171">Task scope is hello default setting, but is included here for hello sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="2d69c-172">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="2d69c-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="2d69c-173">Java partii</span><span class="sxs-lookup"><span data-stu-id="2d69c-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="2d69c-174">Batch Python</span><span class="sxs-lookup"><span data-stu-id="2d69c-174">Batch Python</span></span>

```python
user = batchmodels.UserIdentity(
    auto_user=batchmodels.AutoUserSpecification(
        elevation_level=batchmodels.ElevationLevel.admin,
        scope=batchmodels.AutoUserScope.task))
task = batchmodels.TaskAddParameter(
    id='task_1',
    command_line='cmd /c "echo hello world"',
    user_identity=user)
batch_client.task.add(job_id=jobid, task=task)
```

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="2d69c-175">Uruchamianie zadania jako użytkownik automatycznie z zakresem puli</span><span class="sxs-lookup"><span data-stu-id="2d69c-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="2d69c-176">Po zainicjowaniu obsługi węzła, konta dwóch całej puli automatycznej użytkownika są tworzone na każdym węźle w puli hello, z podwyższonym poziomem uprawnień i bez podwyższonego poziomu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2d69c-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in hello pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="2d69c-177">Ustawianie zakresu toopool zakresu hello automatycznie użytkownika dla danego zadania uruchamia zadanie hello spełniająca jeden z tych dwóch całej puli auto-konta.</span><span class="sxs-lookup"><span data-stu-id="2d69c-177">Setting hello auto-user's scope toopool scope for a given task runs hello task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="2d69c-178">Podczas określania zakresu puli dla hello auto użytkownika, wszystkie zadania, które są uruchamiane z uprawnieniami administratora uruchamiana hello tego samego konta użytkowników automatycznie w całej puli.</span><span class="sxs-lookup"><span data-stu-id="2d69c-178">When you specify pool scope for hello auto-user, all tasks that run with administrator access run under hello same pool-wide auto-user account.</span></span> <span data-ttu-id="2d69c-179">Podobnie zadań, które są uruchamiane bez uprawnień administratora również uruchamiana jednego całej puli auto-konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2d69c-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="2d69c-180">Witaj dwie całej puli auto-konta są osobnych kont.</span><span class="sxs-lookup"><span data-stu-id="2d69c-180">hello two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="2d69c-181">Zadania uruchamiania konto administracyjne hello całej puli nie może udostępniać dane zadań uruchomionych w ramach konta standardowe hello i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="2d69c-181">Tasks running under hello pool-wide administrative account cannot share data with tasks running under hello standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="2d69c-182">Witaj toorunning korzyści w ramach tego samego konta użytkownika automatycznie jest, że zadania są tooshare stanie danych z innych zadań uruchomionych na powitania hello tym samym węźle.</span><span class="sxs-lookup"><span data-stu-id="2d69c-182">hello advantage toorunning under hello same auto-user account is that tasks are able tooshare data with other tasks running on hello same node.</span></span>

<span data-ttu-id="2d69c-183">Udostępnianie kluczy tajnych między zadaniami jest jeden scenariusz, w którym uruchamianie zadań w ramach jednego z kont użytkowników automatycznie w całej puli hello dwa przydaje się.</span><span class="sxs-lookup"><span data-stu-id="2d69c-183">Sharing secrets between tasks is one scenario where running tasks under one of hello two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="2d69c-184">Na przykład załóżmy, że zadanie uruchamiania musi tooprovision klucz tajny na powitania węzła, który można użyć innych zadań.</span><span class="sxs-lookup"><span data-stu-id="2d69c-184">For example, suppose a start task needs tooprovision a secret onto hello node that other tasks can use.</span></span> <span data-ttu-id="2d69c-185">Można użyć hello interfejsu API ochrony danych systemu Windows (DPAPI), ale wymaga uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="2d69c-185">You could use hello Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="2d69c-186">Zamiast tego można chronić klucz tajny hello na poziomie użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="2d69c-186">Instead, you can protect hello secret at hello user level.</span></span> <span data-ttu-id="2d69c-187">Witaj, mogą uzyskiwać dostęp do tego samego konta użytkownika do uruchamiania zadań hello klucz tajny bez podwyższonego poziomu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2d69c-187">Tasks running under hello same user account can access hello secret without elevated access.</span></span>

<span data-ttu-id="2d69c-188">Udostępnij innym scenariuszu może miejscu toorun zadania przy użyciu konta użytkownika automatycznie z zakresu puli jest plikiem komunikat interfejsu (Passing Interface).</span><span class="sxs-lookup"><span data-stu-id="2d69c-188">Another scenario where you may want toorun tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="2d69c-189">MPI udziału plików jest przydatne, gdy hello węzłów hello MPI zadań należy toowork na hello tych samych danych pliku.</span><span class="sxs-lookup"><span data-stu-id="2d69c-189">An MPI file share is useful when hello nodes in hello MPI task need toowork on hello same file data.</span></span> <span data-ttu-id="2d69c-190">Witaj węzła głównego tworzy udział pliku, który hello węzłów podrzędnych można uzyskać dostępu do działające w obszarze hello tego samego konta użytkownika automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2d69c-190">hello head node creates a file share that hello child nodes can access if they are running under hello same auto-user account.</span></span> 

<span data-ttu-id="2d69c-191">Witaj następującego fragmentu kodu ustawia hello automatycznie użytkownika zakresu toopool zakresu dla tego zadania w partiami platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="2d69c-191">hello following code snippet sets hello auto-user's scope toopool scope for a task in Batch .NET.</span></span> <span data-ttu-id="2d69c-192">Witaj podniesienie poziomu zostanie pominięty, więc hello zadanie jest uruchamiane hello całej puli auto-konta użytkownika standardowego.</span><span class="sxs-lookup"><span data-stu-id="2d69c-192">hello elevation level is omitted, so hello task runs under hello standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="2d69c-193">Konta użytkowników o nazwie</span><span class="sxs-lookup"><span data-stu-id="2d69c-193">Named user accounts</span></span>

<span data-ttu-id="2d69c-194">Podczas tworzenia puli, można określić konta użytkowników o nazwie.</span><span class="sxs-lookup"><span data-stu-id="2d69c-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="2d69c-195">Konto użytkownika o nazwie ma nazwę i hasło, które można wprowadzić.</span><span class="sxs-lookup"><span data-stu-id="2d69c-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="2d69c-196">Można określić hello podniesienie poziomu dla konta użytkownika o nazwie.</span><span class="sxs-lookup"><span data-stu-id="2d69c-196">You can specify hello elevation level for a named user account.</span></span> <span data-ttu-id="2d69c-197">Dla systemu Linux węzłów można też podać klucz prywatny SSH.</span><span class="sxs-lookup"><span data-stu-id="2d69c-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="2d69c-198">Konto użytkownika o nazwie istnieje na wszystkich węzłach w puli hello i działa tooall dostępne zadania na tych węzłach.</span><span class="sxs-lookup"><span data-stu-id="2d69c-198">A named user account exists on all nodes in hello pool and is available tooall tasks running on those nodes.</span></span> <span data-ttu-id="2d69c-199">Mogą określić dowolną liczbę użytkowników o nazwie puli.</span><span class="sxs-lookup"><span data-stu-id="2d69c-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="2d69c-200">Podczas dodawania zadań lub kolekcji zadań, można określić tego hello zadanie jest uruchamiane jeden hello o nazwie zdefiniowane w puli hello konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2d69c-200">When you add a task or task collection, you can specify that hello task runs under one of hello named user accounts defined on hello pool.</span></span>

<span data-ttu-id="2d69c-201">Przydaje się konto użytkownika o nazwie należy toorun wszystkich zadań w ramach zadania w obszarze hello tego samego konta użytkownika, przy jednoczesnym izolowaniu ich od zadań uruchomionych w innych zadań na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="2d69c-201">A named user account is useful when you want toorun all tasks in a job under hello same user account, but isolate them from tasks running in other jobs at hello same time.</span></span> <span data-ttu-id="2d69c-202">Na przykład można utworzyć nazwanego użytkownika dla każdego zadania i uruchamiać zadania każde zadanie w ramach tego konta użytkownika o nazwie.</span><span class="sxs-lookup"><span data-stu-id="2d69c-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="2d69c-203">Każde zadanie mogło współużytkować klucz tajny z własną zadania, ale nie z zadań uruchomionych w innych zadań.</span><span class="sxs-lookup"><span data-stu-id="2d69c-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="2d69c-204">Umożliwia także toorun konta użytkownika o nazwie zadań, która ustawia uprawnienia dotyczące zasobów zewnętrznych, takich jak udziały plików.</span><span class="sxs-lookup"><span data-stu-id="2d69c-204">You can also use a named user account toorun a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="2d69c-205">Przy użyciu konta użytkownika o nazwie kontrolować hello tożsamości użytkownika i używać tego uprawnienia tooset tożsamości użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2d69c-205">With a named user account, you control hello user identity and can use that user identity tooset permissions.</span></span>  

<span data-ttu-id="2d69c-206">Konta użytkowników o nazwie Włącz SSH bez hasła między węzłami systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="2d69c-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="2d69c-207">Można użyć konta użytkownika o nazwie z węzłami Linux, wymagające toorun wielu wystąpień zadania.</span><span class="sxs-lookup"><span data-stu-id="2d69c-207">You can use a named user account with Linux nodes that need toorun multi-instance tasks.</span></span> <span data-ttu-id="2d69c-208">Każdy węzeł w puli hello można uruchamiać zadania przy użyciu konta użytkownika, zdefiniowanych na powitania całej puli.</span><span class="sxs-lookup"><span data-stu-id="2d69c-208">Each node in hello pool can run tasks under a user account defined on hello whole pool.</span></span> <span data-ttu-id="2d69c-209">Aby uzyskać więcej informacji o wielu wystąpieniach zadań, zobacz [używać wielu\-wystąpienia zadania aplikacji MPI toorun](batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="2d69c-209">For more information about multi-instance tasks, see [Use multi\-instance tasks toorun MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="2d69c-210">Utwórz konta użytkowników o nazwie</span><span class="sxs-lookup"><span data-stu-id="2d69c-210">Create named user accounts</span></span>

<span data-ttu-id="2d69c-211">toocreate o nazwie konta użytkownika w partii, Dodaj kolekcję puli toohello konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2d69c-211">toocreate named user accounts in Batch, add a collection of user accounts toohello pool.</span></span> <span data-ttu-id="2d69c-212">Hello poniższe fragmenty kodu przedstawiają sposób toocreate o nazwie kontach użytkownika w programie .NET, Java i Python.</span><span class="sxs-lookup"><span data-stu-id="2d69c-212">hello following code snippets show how toocreate named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="2d69c-213">Te Pokaż wstawki kodu jak toocreate zarówno administratora, jak i bez uprawnień administratora o nazwie kont w puli.</span><span class="sxs-lookup"><span data-stu-id="2d69c-213">These code snippets show how toocreate both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="2d69c-214">Przykłady Hello tworzenie puli przy użyciu konfiguracji usługi w chmurze hello, ale użyj hello sam podejścia podczas tworzenia puli za pomocą hello konfiguracji maszyny wirtualnej systemu Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="2d69c-214">hello examples create pools using hello cloud service configuration, but you use hello same approach when creating a Windows or Linux pool using hello virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="2d69c-215">Przykład .NET partii (system Windows)</span><span class="sxs-lookup"><span data-stu-id="2d69c-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using hello cloud service configuration.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                                         
    virtualMachineSize: "small",                                                
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));   

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount("adminUser", "xyz123", ElevationLevel.Admin),
    new UserAccount("nonAdminUser", "123xyz", ElevationLevel.NonAdmin),
};

// Commit hello pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="2d69c-216">Przykład .NET partii (Linux)</span><span class="sxs-lookup"><span data-stu-id="2d69c-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello virtual machine configuration toouse toocreate hello pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create hello unbound pool.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                             
    virtualMachineSize: "Standard_A1",                                      
    virtualMachineConfiguration: virtualMachineConfiguration);                  

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount(
        name: "adminUser",
        password: "xyz123",
        elevationLevel: ElevationLevel.Admin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 12345,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
    new UserAccount(
        name: "nonAdminUser",
        password: "123xyz",
        elevationLevel: ElevationLevel.NonAdmin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 45678,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
};

// Commit hello pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="2d69c-217">Przykład Java partii</span><span class="sxs-lookup"><span data-stu-id="2d69c-217">Batch Java example</span></span>

```java
List<UserAccount> userList = new ArrayList<>();
userList.add(new UserAccount().withName(adminUserAccountName).withPassword(adminPassword).withElevationLevel(ElevationLevel.ADMIN));
userList.add(new UserAccount().withName(nonAdminUserAccountName).withPassword(nonAdminPassword).withElevationLevel(ElevationLevel.NONADMIN));
PoolAddParameter addParameter = new PoolAddParameter()
        .withId(poolId)
        .withTargetDedicatedNodes(POOL_VM_COUNT)
        .withVmSize(POOL_VM_SIZE)
        .withCloudServiceConfiguration(configuration)
        .withUserAccounts(userList);
batchClient.poolOperations().createPool(addParameter);
```

#### <a name="batch-python-example"></a><span data-ttu-id="2d69c-218">Przykład Python partii</span><span class="sxs-lookup"><span data-stu-id="2d69c-218">Batch Python example</span></span>

```python
users = [
    batchmodels.UserAccount(
        name='pool-admin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.admin)
    batchmodels.UserAccount(
        name='pool-nonadmin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.nonadmin)
]
pool = batchmodels.PoolAddParameter(
    id=pool_id,
    user_accounts=users,
    virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
        image_reference=image_ref_to_use,
        node_agent_sku_id=sku_to_use),
    vm_size=vm_size,
    target_dedicated=vm_count)
batch_client.pool.add(pool)
```

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="2d69c-219">Uruchamianie zadania przy użyciu konta użytkownika o nazwie z podwyższonym poziomem uprawnień</span><span class="sxs-lookup"><span data-stu-id="2d69c-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="2d69c-220">toorun zadanie jako z podwyższonym poziomem uprawnień użytkownika, zestaw zadań hello **tożsamości użytkownika** tooa właściwość o nazwie konta użytkownika, który został utworzony z jego **ElevationLevel** właściwość zbyt`Admin`.</span><span class="sxs-lookup"><span data-stu-id="2d69c-220">toorun a task as an elevated user, set hello task's **UserIdentity** property tooa named user account that was created with its **ElevationLevel** property set too`Admin`.</span></span>

<span data-ttu-id="2d69c-221">Następujący fragment kodu Określa, że to zadanie hello należy uruchamiać przy użyciu konta użytkownika o nazwie.</span><span class="sxs-lookup"><span data-stu-id="2d69c-221">This code snippet specifies that hello task should run under a named user account.</span></span> <span data-ttu-id="2d69c-222">To konto użytkownika o nazwie został zdefiniowany w puli hello podczas tworzenia puli hello.</span><span class="sxs-lookup"><span data-stu-id="2d69c-222">This named user account was defined on hello pool when hello pool was created.</span></span> <span data-ttu-id="2d69c-223">W takim przypadku hello o nazwie konta użytkownika została utworzona z uprawnieniami administratora:</span><span class="sxs-lookup"><span data-stu-id="2d69c-223">In this case, hello named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a><span data-ttu-id="2d69c-224">Zaktualizuj kod toohello najnowszego wsadu klienta biblioteki</span><span class="sxs-lookup"><span data-stu-id="2d69c-224">Update your code toohello latest Batch client library</span></span>

<span data-ttu-id="2d69c-225">wersja usługi partii Hello 2017-01-01.4.0 wprowadzono istotne zmiany, zastępując hello **runElevated** właściwości dostępne w starszych wersjach z hello **tożsamości użytkownika** właściwości.</span><span class="sxs-lookup"><span data-stu-id="2d69c-225">hello Batch service version 2017-01-01.4.0 introduces a breaking change, replacing hello **runElevated** property available in earlier versions with hello **userIdentity** property.</span></span> <span data-ttu-id="2d69c-226">następujące tabele Hello zapewniają prosty mapowania, które korzystanie z tooupdate kodu z wcześniejszych wersji powitania klienta biblioteki.</span><span class="sxs-lookup"><span data-stu-id="2d69c-226">hello following tables provide a simple mapping that you can use tooupdate your code from earlier versions of hello client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="2d69c-227">Batch .NET</span><span class="sxs-lookup"><span data-stu-id="2d69c-227">Batch .NET</span></span>

| <span data-ttu-id="2d69c-228">Jeśli korzysta z kodu...</span><span class="sxs-lookup"><span data-stu-id="2d69c-228">If your code uses...</span></span>                  | <span data-ttu-id="2d69c-229">Aby zaktualizować...</span><span class="sxs-lookup"><span data-stu-id="2d69c-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="2d69c-230">`CloudTask.RunElevated`nie określono</span><span class="sxs-lookup"><span data-stu-id="2d69c-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="2d69c-231">Aktualizacja nie jest wymagana</span><span class="sxs-lookup"><span data-stu-id="2d69c-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="2d69c-232">Java partii</span><span class="sxs-lookup"><span data-stu-id="2d69c-232">Batch Java</span></span>

| <span data-ttu-id="2d69c-233">Jeśli korzysta z kodu...</span><span class="sxs-lookup"><span data-stu-id="2d69c-233">If your code uses...</span></span>                      | <span data-ttu-id="2d69c-234">Aby zaktualizować...</span><span class="sxs-lookup"><span data-stu-id="2d69c-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="2d69c-235">`CloudTask.withRunElevated`nie określono</span><span class="sxs-lookup"><span data-stu-id="2d69c-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="2d69c-236">Aktualizacja nie jest wymagana</span><span class="sxs-lookup"><span data-stu-id="2d69c-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="2d69c-237">Batch Python</span><span class="sxs-lookup"><span data-stu-id="2d69c-237">Batch Python</span></span>

| <span data-ttu-id="2d69c-238">Jeśli korzysta z kodu...</span><span class="sxs-lookup"><span data-stu-id="2d69c-238">If your code uses...</span></span>                      | <span data-ttu-id="2d69c-239">Aby zaktualizować...</span><span class="sxs-lookup"><span data-stu-id="2d69c-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="2d69c-240">`user_identity=user`, gdzie</span><span class="sxs-lookup"><span data-stu-id="2d69c-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="2d69c-241">`user_identity=user`, gdzie</span><span class="sxs-lookup"><span data-stu-id="2d69c-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="2d69c-242">`run_elevated`nie określono</span><span class="sxs-lookup"><span data-stu-id="2d69c-242">`run_elevated` not specified</span></span> | <span data-ttu-id="2d69c-243">Aktualizacja nie jest wymagana</span><span class="sxs-lookup"><span data-stu-id="2d69c-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="2d69c-244">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2d69c-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="2d69c-245">Forum usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="2d69c-245">Batch Forum</span></span>

<span data-ttu-id="2d69c-246">Witaj [Forum usługi partia zadań Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) w witrynie MSDN jest doskonałym umieścić toodiscuss partii i zadać pytania dotyczące usługi hello.</span><span class="sxs-lookup"><span data-stu-id="2d69c-246">hello [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="2d69c-247">HEAD na za pośrednictwem przydatne Posty przypiętych i opublikuj swoje pytania powstałych podczas tworzenia własnych rozwiązań partii.</span><span class="sxs-lookup"><span data-stu-id="2d69c-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>
