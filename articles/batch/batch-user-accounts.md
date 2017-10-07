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
# <a name="run-tasks-under-user-accounts-in-batch"></a>Uruchomienie zadania na kontach użytkowników w partii

Zadania w partii zadań Azure jest zawsze uruchamiany na koncie użytkownika. Domyślnie zadania są uruchamiane na kontach użytkowników standardowych, bez uprawnień administratora. Domyślne ustawienia konta użytkownika są zwykle wystarczające. W niektórych scenariuszach jednak jest przydatne toobe tooconfigure stanie hello konta użytkownika pod którym ma zostać toorun zadań. W tym artykule omówiono hello typy kont użytkowników i jak można je skonfigurować dla danego scenariusza.

## <a name="types-of-user-accounts"></a>Typy kont użytkowników

Partia zadań Azure oferuje dwa typy kont użytkowników do uruchamiania zadań:

- **Konta użytkowników automatycznie.** Konta użytkowników automatycznie są wbudowane konta użytkowników, które są tworzone automatycznie przez hello usługa partia zadań. Domyślnie zadania są uruchamiane na koncie użytkownika automatycznie. Można skonfigurować hello specyfikacji użytkownika automatycznie tooindicate zadania, w którym użytkownik automatycznie uruchamiać zadania konta. Specyfikacja użytkownika automatycznie Hello pozwala toospecify hello podniesienie poziomu i zakres hello automatycznie użytkownika konta, które zostanie uruchomione zadanie hello. 

- **Konto użytkownika o nazwie.** Podczas tworzenia puli hello można określić co najmniej jednego konta użytkownika o nazwie puli. Każde konto użytkownika jest tworzony w każdym węźle hello puli. Ponadto toohello nazwa konta, określ hasło konta użytkownika hello, podniesienie poziomu, a w przypadku pul systemu Linux, klucza prywatnego SSH hello. Podczas dodawania zadania można określić hello o nazwie konta użytkownika, w którym to zadanie powinno być ono uruchomione.

> [!IMPORTANT] 
> Witaj partii usługi wersji 2017-01-01.4.0 wprowadzono istotne zmiany wymaga aktualizacji toocall Twojego kod tej wersji. W przypadku migrowania kodu ze starszej wersji partii należy pamiętać, że hello **runElevated** właściwość nie jest już obsługiwana w hello bibliotek klienta interfejsu API REST lub partii. Użyj hello nowe **tożsamości użytkownika** właściwości poziomu zadań toospecify podniesienia uprawnień. Zobacz hello sekcji [zaktualizuj kod toohello najnowszego wsadu klienta biblioteki](#update-your-code-to-the-latest-batch-client-library) szybkie wytyczne dotyczące aktualizowanie kodu partii, jeśli używasz powitania klienta biblioteki.
>
>

> [!NOTE] 
> konta użytkowników Hello omówione w tym artykule nie obsługują protokołu RDP (Remote Desktop) lub protokołu Secure Shell (SSH), ze względów bezpieczeństwa. 
>
> tooconnect tooa węzła uruchomionych hello Linux konfiguracji maszyny wirtualnej za pośrednictwem protokołu SSH, zobacz [tooa pulpitu zdalnego użyj maszyny Wirtualnej systemu Linux na platformie Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md). toonodes tooconnect z systemem Windows za pomocą protokołu RDP, zobacz [połączyć tooa maszyny Wirtualnej systemu Windows Server](../virtual-machines/windows/connect-logon.md).<br /><br />
> tooconnect tooa węzła uruchomionych hello usługi konfiguracji chmury za pomocą protokołu RDP, zobacz [włączyć Podłączanie pulpitu zdalnego dla roli w usług Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).
>
>

## <a name="user-account-access-toofiles-and-directories"></a>Toofiles dostępu do konta użytkownika i katalogów

Zarówno konto użytkownika automatycznie, jak i konto użytkownika o nazwie ma zadanie odczytu/zapisu dostępu toohello katalog roboczy, udostępniony katalog i katalog zadania wielu wystąpień. Oba typy kont mają dostęp do odczytu toohello uruchomienia zadania przygotowanie katalogów i.

Jeśli zadanie jest uruchamiane hello samo konto, które zostało użyte do uruchomienia zadania uruchamiania, hello zadanie ma dostęp do odczytu zapisu toohello rozpoczęcia zadań katalog. Podobnie, jeśli zadanie jest uruchamiane hello samo konto, które zostało użyte do uruchomienia zadania przygotowanie zadania, zadania hello ma dostęp do odczytu zapisu toohello zadanie przygotowanie zadania katalogu. Jeśli zadanie jest uruchamiane przy użyciu innego konta niż zadania uruchamiania hello lub zadanie przygotowanie zadania, zadania hello ma tylko dostęp do odczytu toohello odpowiednich katalogu.

Aby uzyskać więcej informacji dotyczących uzyskiwania dostępu do plików i katalogów z zadania, zobacz [Programowanie równoległe na dużą skalę obliczeniowe rozwiązań w partii](batch-api-basics.md#files-and-directories).

## <a name="elevated-access-for-tasks"></a>Z podwyższonym poziomem uprawnień dostępu do zadania 

konto użytkownika Hello podniesienie poziomu wskazuje, czy zadanie jest uruchamiane z podwyższonym poziomem uprawnień. Zarówno konto użytkownika automatycznie, jak i konto użytkownika o nazwie można uruchomić z podwyższonym poziomem uprawnień. dostępne są następujące dwie opcje Hello podniesienie poziomu:

- **NonAdmin:** hello zadanie jest uruchamiane jako użytkownik standardowy bez podwyższonego poziomu dostępu. Witaj domyślny poziom podniesienia uprawnień konta użytkownika usługi partia zadań jest zawsze **NonAdmin**.
- **Administrator:** hello zadań uruchamia jako użytkownik z podwyższonym poziomem uprawnień i działa z pełnymi uprawnieniami administratora. 

## <a name="auto-user-accounts"></a>Konta użytkowników automatycznie

Domyślnie zadania są uruchamiane w trybie wsadowym na koncie użytkownika automatycznie jako użytkownik standardowy bez podwyższonego poziomu dostępu i z zakresu zadań. Po skonfigurowaniu specyfikacji użytkownika automatycznie hello zakresie zadania usługa partia zadań hello tworzy konta użytkownika automatycznie tylko tego zadania.

zakres tootask alternatywnych Hello jest zakres puli. Po skonfigurowaniu specyfikacji użytkownika automatycznie hello zadania dla zakresu puli hello zadanie jest uruchamiane jest zadanie tooany dostępne w puli hello z konta użytkownika automatycznie. Aby uzyskać więcej informacji na temat zakresu puli, zobacz hello sekcji [uruchomienia zadania, jak hello auto użytkownika w zakresie puli](#run-a-task-as-the-autouser-with-pool-scope).   

zakres domyślny Hello różni się w węzłach systemu Windows i Linux:

- W węzłach Windows zadania są uruchamiane w zakresie zadania domyślnie.
- Węzły Linux są zawsze uruchamiane w zakresie puli.

Istnieją cztery konfiguracje możliwych do określenia użytkownika automatycznie hello, z których każdy odpowiada tooa unikatowe auto-konto użytkownika:

- Dostęp inni niż administratorzy z zakresem zadań (Specyfikacja hello domyślne użytkownika automatycznie)
- Uprawnienia administratora (podwyższonymi) z zakresem zadań
- Dostęp inni niż administratorzy z zakresem puli
- Uprawnienia administratora w zakresie puli

> [!IMPORTANT] 
> Zadania uruchomione w zakresie zadania nie ma faktycznego zadań tooother dostępu w węźle. Jednak złośliwy użytkownik z kontem toohello dostępu można obejść to ograniczenie poprzez przesłanie zadanie, które jest uruchamiany z uprawnieniami administratora i uzyskuje dostęp do katalogów innych zadań. Złośliwy użytkownik można użyć również węzeł tooa tooconnect RDP lub SSH. Jest ważne tooprotect dostępu tooyour partii konta klucze tooprevent takiej sytuacji. Jeśli podejrzewasz, że Twoje konto zostało naruszone, można tooregenerate się, że Twoje klucze.
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a>Uruchamianie zadania jako użytkownik automatycznie z podwyższonym poziomem uprawnień

Można skonfigurować hello specyfikacji automatycznie użytkownika uprawnień administratora, gdy potrzebujesz toorun zadania z podwyższonym poziomem uprawnień. Na przykład może być konieczne zadania uruchamiania podwyższonego poziomu dostępu tooinstall oprogramowania w węźle hello.

> [!NOTE] 
> Ogólnie rzecz biorąc, najlepiej jest toouse z podwyższonym poziomem uprawnień dostępu tylko wtedy, gdy jest to konieczne. Najlepszym rozwiązaniem jest przyznanie hello minimalne uprawnienia niezbędne tooachieve hello żądanego wyniku. Na przykład zadania uruchamiania instalacji oprogramowania hello bieżącego użytkownika, a nie dla wszystkich użytkowników, może być możliwe tooavoid udzielanie tootasks podwyższonego poziomu dostępu. Można skonfigurować specyfikacji użytkownika automatycznie hello puli zakresu i bez uprawnień administratora dostępu dla wszystkich zadań wymagających toorun w obszarze hello tego samego konta, w tym hello rozpoczęcia zadań. 
>
>

powitania po wstawki kodu pokazują, jak tooconfigure hello specyfikacji użytkownika automatycznie. Przykłady Hello ustawić hello podniesienie poziomu także`Admin` i hello zakresu zbyt`Task`. Zakres zadań jest ustawienie domyślne hello, ale są przeznaczone dla zapewnienia hello przykład.

#### <a name="batch-net"></a>Batch .NET

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a>Java partii

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a>Batch Python

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

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a>Uruchamianie zadania jako użytkownik automatycznie z zakresem puli

Po zainicjowaniu obsługi węzła, konta dwóch całej puli automatycznej użytkownika są tworzone na każdym węźle w puli hello, z podwyższonym poziomem uprawnień i bez podwyższonego poziomu dostępu. Ustawianie zakresu toopool zakresu hello automatycznie użytkownika dla danego zadania uruchamia zadanie hello spełniająca jeden z tych dwóch całej puli auto-konta. 

Podczas określania zakresu puli dla hello auto użytkownika, wszystkie zadania, które są uruchamiane z uprawnieniami administratora uruchamiana hello tego samego konta użytkowników automatycznie w całej puli. Podobnie zadań, które są uruchamiane bez uprawnień administratora również uruchamiana jednego całej puli auto-konta użytkownika. 

> [!NOTE] 
> Witaj dwie całej puli auto-konta są osobnych kont. Zadania uruchamiania konto administracyjne hello całej puli nie może udostępniać dane zadań uruchomionych w ramach konta standardowe hello i na odwrót. 
>
>

Witaj toorunning korzyści w ramach tego samego konta użytkownika automatycznie jest, że zadania są tooshare stanie danych z innych zadań uruchomionych na powitania hello tym samym węźle.

Udostępnianie kluczy tajnych między zadaniami jest jeden scenariusz, w którym uruchamianie zadań w ramach jednego z kont użytkowników automatycznie w całej puli hello dwa przydaje się. Na przykład załóżmy, że zadanie uruchamiania musi tooprovision klucz tajny na powitania węzła, który można użyć innych zadań. Można użyć hello interfejsu API ochrony danych systemu Windows (DPAPI), ale wymaga uprawnień administratora. Zamiast tego można chronić klucz tajny hello na poziomie użytkownika hello. Witaj, mogą uzyskiwać dostęp do tego samego konta użytkownika do uruchamiania zadań hello klucz tajny bez podwyższonego poziomu dostępu.

Udostępnij innym scenariuszu może miejscu toorun zadania przy użyciu konta użytkownika automatycznie z zakresu puli jest plikiem komunikat interfejsu (Passing Interface). MPI udziału plików jest przydatne, gdy hello węzłów hello MPI zadań należy toowork na hello tych samych danych pliku. Witaj węzła głównego tworzy udział pliku, który hello węzłów podrzędnych można uzyskać dostępu do działające w obszarze hello tego samego konta użytkownika automatycznie. 

Witaj następującego fragmentu kodu ustawia hello automatycznie użytkownika zakresu toopool zakresu dla tego zadania w partiami platformy .NET. Witaj podniesienie poziomu zostanie pominięty, więc hello zadanie jest uruchamiane hello całej puli auto-konta użytkownika standardowego.

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a>Konta użytkowników o nazwie

Podczas tworzenia puli, można określić konta użytkowników o nazwie. Konto użytkownika o nazwie ma nazwę i hasło, które można wprowadzić. Można określić hello podniesienie poziomu dla konta użytkownika o nazwie. Dla systemu Linux węzłów można też podać klucz prywatny SSH.

Konto użytkownika o nazwie istnieje na wszystkich węzłach w puli hello i działa tooall dostępne zadania na tych węzłach. Mogą określić dowolną liczbę użytkowników o nazwie puli. Podczas dodawania zadań lub kolekcji zadań, można określić tego hello zadanie jest uruchamiane jeden hello o nazwie zdefiniowane w puli hello konta użytkownika.

Przydaje się konto użytkownika o nazwie należy toorun wszystkich zadań w ramach zadania w obszarze hello tego samego konta użytkownika, przy jednoczesnym izolowaniu ich od zadań uruchomionych w innych zadań na powitania tym samym czasie. Na przykład można utworzyć nazwanego użytkownika dla każdego zadania i uruchamiać zadania każde zadanie w ramach tego konta użytkownika o nazwie. Każde zadanie mogło współużytkować klucz tajny z własną zadania, ale nie z zadań uruchomionych w innych zadań.

Umożliwia także toorun konta użytkownika o nazwie zadań, która ustawia uprawnienia dotyczące zasobów zewnętrznych, takich jak udziały plików. Przy użyciu konta użytkownika o nazwie kontrolować hello tożsamości użytkownika i używać tego uprawnienia tooset tożsamości użytkownika.  

Konta użytkowników o nazwie Włącz SSH bez hasła między węzłami systemu Linux. Można użyć konta użytkownika o nazwie z węzłami Linux, wymagające toorun wielu wystąpień zadania. Każdy węzeł w puli hello można uruchamiać zadania przy użyciu konta użytkownika, zdefiniowanych na powitania całej puli. Aby uzyskać więcej informacji o wielu wystąpieniach zadań, zobacz [używać wielu\-wystąpienia zadania aplikacji MPI toorun](batch-mpi.md).

### <a name="create-named-user-accounts"></a>Utwórz konta użytkowników o nazwie

toocreate o nazwie konta użytkownika w partii, Dodaj kolekcję puli toohello konta użytkownika. Hello poniższe fragmenty kodu przedstawiają sposób toocreate o nazwie kontach użytkownika w programie .NET, Java i Python. Te Pokaż wstawki kodu jak toocreate zarówno administratora, jak i bez uprawnień administratora o nazwie kont w puli. Przykłady Hello tworzenie puli przy użyciu konfiguracji usługi w chmurze hello, ale użyj hello sam podejścia podczas tworzenia puli za pomocą hello konfiguracji maszyny wirtualnej systemu Windows lub Linux.

#### <a name="batch-net-example-windows"></a>Przykład .NET partii (system Windows)

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

#### <a name="batch-net-example-linux"></a>Przykład .NET partii (Linux)

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


#### <a name="batch-java-example"></a>Przykład Java partii

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

#### <a name="batch-python-example"></a>Przykład Python partii

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

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a>Uruchamianie zadania przy użyciu konta użytkownika o nazwie z podwyższonym poziomem uprawnień

toorun zadanie jako z podwyższonym poziomem uprawnień użytkownika, zestaw zadań hello **tożsamości użytkownika** tooa właściwość o nazwie konta użytkownika, który został utworzony z jego **ElevationLevel** właściwość zbyt`Admin`.

Następujący fragment kodu Określa, że to zadanie hello należy uruchamiać przy użyciu konta użytkownika o nazwie. To konto użytkownika o nazwie został zdefiniowany w puli hello podczas tworzenia puli hello. W takim przypadku hello o nazwie konta użytkownika została utworzona z uprawnieniami administratora:

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a>Zaktualizuj kod toohello najnowszego wsadu klienta biblioteki

wersja usługi partii Hello 2017-01-01.4.0 wprowadzono istotne zmiany, zastępując hello **runElevated** właściwości dostępne w starszych wersjach z hello **tożsamości użytkownika** właściwości. następujące tabele Hello zapewniają prosty mapowania, które korzystanie z tooupdate kodu z wcześniejszych wersji powitania klienta biblioteki.

### <a name="batch-net"></a>Batch .NET

| Jeśli korzysta z kodu...                  | Aby zaktualizować...                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| `CloudTask.RunElevated`nie określono | Aktualizacja nie jest wymagana                                                                                               |

### <a name="batch-java"></a>Java partii

| Jeśli korzysta z kodu...                      | Aby zaktualizować...                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| `CloudTask.withRunElevated`nie określono | Aktualizacja nie jest wymagana                                                                                                                     |

### <a name="batch-python"></a>Batch Python

| Jeśli korzysta z kodu...                      | Aby zaktualizować...                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | `user_identity=user`, gdzie <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | `user_identity=user`, gdzie <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| `run_elevated`nie określono | Aktualizacja nie jest wymagana                                                                                                                                  |


## <a name="next-steps"></a>Następne kroki

### <a name="batch-forum"></a>Forum usługi partia zadań

Witaj [Forum usługi partia zadań Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) w witrynie MSDN jest doskonałym umieścić toodiscuss partii i zadać pytania dotyczące usługi hello. HEAD na za pośrednictwem przydatne Posty przypiętych i opublikuj swoje pytania powstałych podczas tworzenia własnych rozwiązań partii.
