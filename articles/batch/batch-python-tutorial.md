---
title: "aaaTutorial - hello Użyj zestawu SDK usługi partia zadań Azure dla języka Python | Dokumentacja firmy Microsoft"
description: "Dowiedz się hello podstawowych pojęciach dotyczących partii zadań Azure i utworzenie rozwiązania do prostych przy użyciu języka Python."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: 42cae157-d43d-47f8-88f5-486ccfd334f4
ms.service: batch
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c4d5152aeef31848c50a7f2aae5e7a7e0e1e9535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-sdk-for-python"></a>Rozpoczynanie pracy z hello partii zestawu SDK dla języka Python

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Dowiedz się podstawy hello [partii zadań Azure] [ azure_batch] i hello [Python partii] [ py_azure_sdk] klienta jako omówimy małych aplikacji partii napisanych w języku Python. Opisano, jak dwie przykładowe skrypty Użyj hello partii usługi tooprocess równoległe obciążenie maszyn wirtualnych systemu Linux w chmurze hello i sposób ich interakcji z [usługi Azure Storage](../storage/common/storage-introduction.md) potrzeby przemieszczania plików i odzyskiwania. Będzie informacje wspólnego przepływu pracy aplikacji partii i Uzyskaj podstawową wiedzę na temat hello głównych składników usługi partia zadań takich jak zadania, zadania, pul i węzły obliczeniowe.

![Przepływ pracy rozwiązania w usłudze Batch (podstawowy)][11]<br/>

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule założono, że masz praktyczną wiedzę dotyczącą języka Python oraz znasz system Linux. Przyjęto założenie, że jesteś toosatisfy stanie hello tworzenie wymagania dotyczące konta określonych poniżej platformy Azure i hello partii i usługi magazynu.

### <a name="accounts"></a>Konta
* **Konto platformy Azure**: jeśli nie masz jeszcze subskrypcji platformy Azure, [utwórz bezpłatne konto platformy Azure][azure_free_account].
* **Konto usługi Batch**: po uzyskaniu subskrypcji platformy Azure [utwórz konto usługi Azure Batch](batch-account-create-portal.md).
* **Konto magazynu**: zobacz sekcję [Tworzenie konta magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) w temacie [Informacje o kontach magazynu Azure](../storage/common/storage-create-storage-account.md).

### <a name="code-sample"></a>Przykład kodu
Samouczek Python Hello [przykładowy kod] [ github_article_samples] jest jednym z hello wiele przykładów kodu partii znaleziony w hello [azure partii próbek] [ github_samples] repozytorium na GitHub. Wszystkie próbki hello można pobrać po kliknięciu **klonowania lub pobierania > Pobierz ZIP** na stronie głównej repozytorium hello lub przez kliknięcie przycisku hello [azure partii — przykłady master.zip] [ github_samples_zip]łącze bezpośrednie. Gdy już wyodrębniono zawartość pliku ZIP hello hello hello dwa skrypty w tym samouczku znajdują się w hello `article_samples` katalogu:

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a>Środowisko Python
Witaj toorun *python_tutorial_client.py* przykładowy skrypt na na lokalnej stacji roboczej, należy **interpreter języka Python** zgodny z wersją **2.7** lub **3.3 +**. skrypt Hello przetestowano na systemie Linux i Windows.

### <a name="cryptography-dependencies"></a>Zależności kryptograficzne
Należy zainstalować zależności hello hello [kryptografii] [ crypto] biblioteki wymagane przez hello `azure-batch` i `azure-storage` pakietów języka Python. Wykonaj jedną z hello następujące operacje odpowiednie dla danej platformy, lub można znaleźć toohello [instalacji kryptografii] [ crypto_install] szczegóły, aby uzyskać więcej informacji:

* Ubuntu

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* CentOS

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* SLES/OpenSUSE

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* Windows

    `pip install cryptography`

> [!NOTE]
> Jeśli instalacja Python 3.3 + w systemie Linux, użyj odpowiedniki python3 hello hello Python zależności. Na przykład na platformie Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`
>
>

### <a name="azure-packages"></a>Pakiety platformy Azure
Następnie zainstaluj hello **partii zadań Azure** i **usługi Azure Storage** pakietów języka Python. Oba pakiety można zainstalować za pomocą **pip** i hello *requirements.txt* znaleźć tutaj:

`/azure-batch-samples/Python/Batch/requirements.txt`

Następujące problem **pip** polecenia pakietów hello tooinstall wsadowego i magazynowania:

`pip install -r requirements.txt`

Można także zainstalować hello [partii zadań azure] [ pypi_batch] i [magazyn azure] [ pypi_storage] Python pakietów ręcznego:

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> Jeśli używasz konta nieuprzywilejowanego, może być konieczne tooprefix poleceń z `sudo`. Na przykład `sudo pip install -r requirements.txt`. Więcej informacji na temat instalowania pakietów dla środowiska Python znajduje się w temacie [Instalowanie pakietów][pypi_install] w witrynie python.org.
>
>

## <a name="batch-python-tutorial-code-sample"></a>Przykład kodu z samouczka dotyczącego usługi Batch dla środowiska Python
Przykładowy kod samouczek Python partii Hello składa się z dwóch skryptów języka Python i kilka plików danych.

* **python_tutorial_client.PY**: współdziała z hello partii i magazynu usług tooexecute równoległe obciążenie obliczeniowe węzłach (maszynach wirtualnych). Witaj *python_tutorial_client.py* skrypt jest uruchamiany na na lokalnej stacji roboczej.
* **python_tutorial_task.PY**: hello skrypt uruchamiany na węzłach w pracy rzeczywistej hello Azure tooperform obliczeniowych. W przykładowym hello *python_tutorial_task.py* analizuje hello tekst w pliku, który został pobrany z usługi Azure Storage (plik wejściowy hello). Następnie tworzy plik tekstowy (plik wyjściowy hello) zawierający listę hello trzy najważniejsze wyrazy, które pojawiają się w pliku wejściowym hello. Po utworzeniu pliku wyjściowego hello *python_tutorial_task.py* przekazywania hello tooAzure pliku magazynu. Udostępnia pobierania toohello skrypt po stronie klienta uruchomione na stacji roboczej. Witaj *python_tutorial_task.py* skrypt będzie uruchamiany równolegle na wielu węzłach w hello usługa partia zadań obliczeniowych.
* **./Data/taskdata\*.txt**: te pliki tekstowe trzy Podaj dane wejściowe hello zadania hello, które będą uruchamiane na powitania węzły obliczeniowe.

powitania po diagram ilustruje hello głównej operacje, które są wykonywane przez skrypty powitania klienta i zadań. Ten podstawowy przepływ pracy jest typowy dla wielu rozwiązań obliczeniowych utworzonych za pomocą usługi Batch. Gdy nie wykazują wszystkich funkcji dostępnych w hello usługa partia zadań, niemal każdego scenariusza partii zawiera części ten przepływ pracy.

![Przykładowy przepływ pracy w usłudze Batch][8]<br/>

[**Krok 1.**](#step-1-create-storage-containers) Utwórz **kontenery** w usłudze Azure Blob Storage.<br/>
[**Krok 2.**](#step-2-upload-task-script-and-data-files) Przekaż toocontainers plików skryptów i dane wejściowe zadania.<br/>
[**Krok 3.**](#step-3-create-batch-pool) Utwórz **pulę** w usłudze Batch.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Witaj puli **StartTask** pliki do pobrania hello toonodes skryptu (python_tutorial_task.py) zadań zgodnie z ich przyłączyć hello puli.<br/>
[**Krok 4.**](#step-4-create-batch-job) Utwórz **zadanie** w usłudze Batch.<br/>
[**Krok 5.**](#step-5-add-tasks-to-job) Dodaj **zadania** toohello zadania.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** zadania Hello są zaplanowane tooexecute na węzłach.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** Każde zadanie pobiera dane wejściowe z usługi Azure Storage, a następnie rozpoczyna się wykonywanie.<br/>
[**Krok 6.**](#step-6-monitor-tasks) Monitoruj podzadania.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Jak czynności zostały wykonane, ich przekazywanie ich tooAzure danych wyjściowych magazynu.<br/>
[**Krok 7.**](#step-7-download-task-output) Pobierz dane wyjściowe podzadań z usługi Storage.

Jak wspomniano wcześniej, nie wszystkie rozwiązania usługi Batch obejmują dokładnie te kroki i mogą obejmować wiele innych, natomiast w tym przykładzie przedstawiono typowe procesy w ramach rozwiązania usługi Batch.

## <a name="prepare-client-script"></a>Przygotowanie skryptu klienta
Przed uruchomieniem hello próbki dodać poświadczeń konta wsadowego i magazynowania za*python_tutorial_client.py*. Jeśli jeszcze tego nie zrobiono, otwórz plik hello w Twoje ulubione hello edytora i zaktualizuj następujące wiersze przy użyciu poświadczeń.

```python
# Update hello Batch and Storage account credential strings below with hello values
# unique tooyour accounts. These are used when constructing connection strings
# for hello Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

Poświadczenia konta wsadowego i magazynowania w bloku konta hello każdej usługi można znaleźć w hello [portalu Azure][azure_portal]:

![Partii poświadczeń w portalu hello][9]
![magazynu poświadczeń w portalu hello][10]<br/>

W hello następujące sekcje, możemy analizowanie hello krokami przez hello skrypty tooprocess obciążenia w hello usługa partia zadań. Firma Microsoft zachęca toorefer regularnie toohello skryptów w edytorze podczas przechodzić przez rest hello hello artykułu.

Przejdź toohello po wierszu **python_tutorial_client.py** toostart z kroku 1:

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a>Krok 1: tworzenie kontenerów w usłudze Storage
![Tworzenie kontenerów w usłudze Azure Storage][1]
<br/>

Usługa Batch ma wbudowaną funkcję obsługi interakcji z usługą Azure Storage. Kontenery na koncie magazynu będzie udostępniać hello pliki wymagane przez hello zadania, które są uruchamiane na koncie usługi partia zadań. kontenery Hello udostępniają danych wyjściowych hello toostore miejsce, który tworzy hello zadania. Po pierwsze Hello hello *python_tutorial_client.py* skrypt wykonuje tworzą trzy kontenery w [magazyn obiektów Blob Azure](../storage/common/storage-introduction.md#blob-storage):

* **Aplikacja**: ten kontener zapisze skrypt w języku Python hello uruchamiania zadań hello *python_tutorial_task.py*.
* **wejściowy**: zadań pobierze tooprocess pliki danych hello z hello *wejściowych* kontenera.
* **dane wyjściowe**: gdy zadania ukończyć przetwarzania pliku wejściowego, przekaże one hello wyniki toohello *dane wyjściowe* kontenera.

W kolejności toointeract z magazynu kont i Utwórz kontenerów, używamy hello [magazyn azure] [ pypi_storage] pakietu toocreate [BlockBlobService] [ py_blockblobservice] obiekt — Witaj "client obiektu blob". Następnie utworzymy trzy kontenery hello konto magazynu przy użyciu powitania klienta obiektu blob.

```python
import azure.storage.blob as azureblob

# Create hello blob client, for use in obtaining references to
# blob storage containers and uploading files toocontainers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use hello blob client toocreate hello containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

Po utworzeniu hello kontenery aplikacji hello teraz przekazać hello pliki, które będą używane przez zadania hello.

> [!TIP]
> [Jak toouse magazynu obiektów Blob platformy Azure w języku Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) zawiera omówienie pracy z usługą Azure Storage kontenerów i obiektów blob. Po rozpoczęciu pracy z instancją powinno być hello górze listy odczytu.
>
>

## <a name="step-2-upload-task-script-and-data-files"></a>Krok 2: przekazywanie skryptu podzadań i plików danych
![Zadanie przekazywania aplikacji i wejściowych (dane) pliki toocontainers][2]
<br/>

W pliku hello Przekaż operacji *python_tutorial_client.py* najpierw definiuje kolekcji **aplikacji** i **wejściowych** pliku ścieżki istniejących na komputerze lokalnym hello. Następnie przekazanie tych kontenerach toohello pliki, które zostały utworzone w poprzednim kroku hello.

```python
# Paths toohello task script. This script will be executed by hello tasks that
# run on hello compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# hello collection of data files that are toobe processed by hello tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload hello application script tooAzure Storage. This is hello script that
# will process hello data files, and is executed by each of hello tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload hello data files. This is hello data that will be processed by each of
# hello tasks executed on hello compute nodes in hello pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

Przy użyciu listy zrozumienia, hello `upload_file_to_container` funkcja jest wywoływana dla każdego pliku w kolekcjach hello i dwa [ResourceFile] [ py_resource_file] kolekcje są wypełnione. Witaj `upload_file_to_container` funkcja pojawia się poniżej:

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file tooan Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: hello name of hello Azure Blob storage container.
    :param str file_path: hello local path toohello file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} toocontainer [{}]...'.format(path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a>ResourceFiles
A [ResourceFile] [ py_resource_file] zawiera zadania w partii hello adresu URL tooa plik z magazynu Azure, który jest pobrany tooa węźle obliczeń przed uruchomieniem tego zadania. Witaj [ResourceFile][py_resource_file]. **blob_source** właściwość określa hello pełny adres URL pliku hello, ponieważ znajduje się ona w magazynie Azure. adres URL Hello mogą również obejmować sygnatury dostępu współdzielonego (SAS) zawiera plik toohello bezpiecznego dostępu. Większość typów podzadań w ramach usługi Batch obejmuje właściwość *ResourceFiles*, m.in.:

* [CloudTask][py_task]
* [StartTask][py_starttask]
* [JobPreparationTask][py_jobpreptask]
* [JobReleaseTask][py_jobreltask]

W tym przykładzie używają hello JobPreparationTask lub JobReleaseTask typy zadań, lecz więcej o nich w [węzły obliczeniowe uruchamianie działań przygotowania i kończenia zadania w partii zadań Azure](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Sygnatura dostępu współdzielonego (SAS)
Sygnatury dostępu współdzielonego są ciągów, które zapewniają toocontainers bezpiecznego dostępu i obiekty BLOB w usłudze Azure Storage. Witaj *python_tutorial_client.py* skrypt używa zarówno obiektów blob i kontener sygnatury dostępu współdzielonego i pokazuje, jak tooobtain te udostępniane dostęp ciągi podpisu z hello usługi magazynu.

* **Obiekt blob sygnatur dostępu współdzielonego**: hello puli StartTask używa obiektu blob sygnatur dostępu współdzielonego po pobraniu hello zadania skryptu i dane wejściowe pliki danych z magazynu (zobacz [kroku nr 3](#step-3-create-batch-pool) poniżej). Witaj `upload_file_to_container` działać w *python_tutorial_client.py* zawiera hello kod, który uzyskuje sygnatury dostępu współdzielonego każdy obiekt blob. Robi to poprzez wywołanie [BlockBlobService.make_blob_url] [ py_make_blob_url] hello modułu magazynu.
* **Sygnatury dostępu współdzielonego kontenera**: zgodnie z każdego zadania zakończy pracę w węźle obliczeń hello, zostanie przesłany jego dane wyjściowe pliku toohello *dane wyjściowe* kontenera w magazynie Azure. toodo, *python_tutorial_task.py* używa kontenera sygnatury dostępu współdzielonego, która zapewnia dostęp do zapisu toohello kontenera. Witaj `get_container_sas_token` działać w *python_tutorial_client.py* uzyskuje sygnatury dostępu współdzielonego hello kontenera, który następnie jest przekazywany jako zadania toohello argumentu wiersza polecenia. Krok #5 [Dodaj zadania tooa zadania](#step-5-add-tasks-to-job), w tym artykule omówiono użycie hello kontenera hello sygnatury dostępu Współdzielonego.

> [!TIP]
> Wyewidencjonowanie hello dwuczęściową serii na sygnatur dostępu współdzielonego [część 1: modelu sygnatur dostępu Współdzielonego hello opis](../storage/common/storage-dotnet-shared-access-signature-part-1.md) i [część 2: tworzenie i używanie sygnatury dostępu Współdzielonego z hello usługa Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn więcej informacji na temat bezpieczny dostęp toodata na koncie magazynu.
>
>

## <a name="step-3-create-batch-pool"></a>Krok 3: tworzenie puli usługi Batch
![Tworzenie puli usługi Batch][3]
<br/>

**Pula** usługi Batch jest kolekcją węzłów obliczeniowych (maszyn wirtualnych), w których usługa Batch wykonuje podzadania danego zadania.

Po jego przekazuje hello zadania skryptu i danych plików toohello konta magazynu, *python_tutorial_client.py* jego interakcji z usługi partia zadań hello jest uruchamiany przy użyciu modułu Python partii hello. toodo, [BatchServiceClient] [ py_batchserviceclient] utworzeniu:

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

Następnie puli węzłów obliczeniowych jest tworzony w hello konta usługi partia zadań przy użyciu wywołania zbyt`create_pool`.

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with hello specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for hello new pool.
    :param list resource_files: A collection of resource files for hello pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify hello commands for hello pool's start task. hello start task is run
    # on each node as it joins hello pool, and when it's rebooted or re-imaged.
    # We use hello start task tooprep hello node for running our task script.
    task_commands = [
        # Copy hello python_tutorial_task.py script toohello "shared" directory
        # that all tasks that run on hello node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and hello dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install hello azure-storage module so that hello task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get hello node agent SKU and image reference for hello virtual machine
    # configuration.
    # For more information about hello virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

Podczas tworzenia puli, należy zdefiniować [PoolAddParameter] [ py_pooladdparam] , który określa kilka właściwości puli hello:

* **Identyfikator** hello puli (*identyfikator* — jest to wymagane)<p/>Podobnie jak w przypadku większości obiektów w usłudze Batch nowa pula musi mieć unikatowy identyfikator w ramach konta usługi Batch. Kod odwołuje się toothis puli za pomocą jego Identyfikatora, a jest to, jak rozpoznać puli hello w hello Azure [portal][azure_portal].
* **Liczba węzłów obliczeniowych** (element *target_dedicated* — wymagany)<p/>Ta właściwość określa, jak wiele maszyn wirtualnych powinny zostać wdrożone w puli hello. Jest ważne toonote, że wszystkie konta usługi partia zadań mają domyślnie **przydziału** czy limity hello liczba **rdzeni** (i w związku z tym węzły obliczeniowe) w ramach konta usługi partia zadań. Można znaleźć hello przydziałów domyślnych i instrukcje na temat zbyt[Zwiększ limit przydziału](batch-quota-limit.md#increase-a-quota) (na przykład hello maksymalna liczba rdzeni w ramach konta usługi partia zadań) w [przydziały i limity dla usługi partia zadań Azure hello](batch-quota-limit.md). Jeśli zaczniesz zastanawiać się: „Dlaczego moja pula nie może przekroczyć X rdzeni?”, Ten limit przydziału rdzeni może spowodować hello.
* **System operacyjny** dla węzłów (element *virtual_machine_configuration* **lub** *cloud_service_configuration* — wymagany)<p/>W skrypcie *python_tutorial_client.py* zostanie utworzona pula węzłów systemu Linux przy użyciu polecenia [VirtualMachineConfiguration][py_vm_config]. Witaj `select_latest_verified_vm_image_with_node_agent_sku` działać w `common.helpers` upraszcza pracy z [Marketplace maszyny wirtualne Azure] [ vm_marketplace] obrazów. Więcej informacji o używaniu obrazów z rynku znajduje się w artykule [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) (Inicjowanie obsługi węzłów obliczeniowych systemu Linux w pulach usługi Azure Batch).
* **Rozmiar węzłów obliczeniowych** (element *vm_size* — wymagany)<p/>Ponieważ należy określać węzły obliczeniowe systemu Linux dla parametru [VirtualMachineConfiguration][py_vm_config], określamy rozmiar maszyny wirtualnej (`STANDARD_A1` w tym przykładzie) na podstawie artykułu [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Rozmiary maszyn wirtualnych na platformie Azure). Więcej informacji znajduje się w artykule [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) (Inicjowanie obsługi węzłów obliczeniowych systemu Linux w pulach usługi Azure Batch).
* **Podzadanie uruchamiania** (element *start_task* — niewymagany)<p/>Wraz z hello powyżej właściwości węzła fizycznego, można również określić [StartTask] [ py_starttask] puli hello (nie jest wymagane). Hello StartTask wykonywane na każdym węźle, ponieważ ten węzeł dołącza hello puli i każdym uruchomieniu węzła. Hello StartTask jest szczególnie przydatna w przypadku przygotowywania węzły obliczeniowe hello wykonywania zadań, takich jak instalowanie aplikacji hello, które uruchamiane zadań.<p/>W tej przykładowej aplikacji hello StartTask kopiuje hello pliki, które pobiera z magazynu (które są określane przy użyciu hello StartTask **resource_files** właściwości) z hello StartTask *katalog roboczy* toohello *udostępnionego* katalogu, w którym wszystkie zadania uruchomione w węźle hello może uzyskać dostęp. Zasadniczo spowoduje to skopiowanie `python_tutorial_task.py` toohello udostępniony katalog w każdym węźle jako węzeł hello dołącza hello puli, tak aby wszystkie zadania, które będą uruchamiane w węźle hello do niego dostęp.

Można zauważyć hello wywołania toohello `wrap_commands_in_shell` funkcji pomocnika. Funkcja ta z kolekcji oddzielnych poleceń tworzy jeden wiersz polecenia odpowiedni dla właściwości wiersza polecenia podzadania.

Godny uwagi we fragmencie kodu hello powyżej jest również użycie Witaj dwie zmienne środowiskowe w hello **wiersz polecenia** właściwości hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` i `AZ_BATCH_NODE_SHARED_DIR`. Każdy węzeł obliczeniowy w puli partii jest automatycznie konfigurowany z kilku zmiennych środowiskowych, które są określone tooBatch. Żaden proces, która jest wykonywana przez zadanie ma zmienne środowiskowe toothese dostępu.

> [!TIP]
> toofind więcej informacji na temat hello zmiennych środowiskowych, które są dostępne w węzłach obliczeń w puli partii, jak również informacje o katalogach roboczych zadań, zobacz **ustawienia środowiska dla zadań** i **plików i katalogów**  w hello [Przegląd funkcji partii zadań Azure](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a>Krok 4: tworzenie zadania w usłudze Batch
![Tworzenie zadania w usłudze Batch][4]<br/>

**Zadanie** usługi Batch jest kolekcją podzadań i jest skojarzone z pulą węzłów obliczeniowych. wykonanie Hello zadań w ramach zadania w węzłach obliczeń puli hello skojarzone.

Można użyć zadania nie tylko do organizowaniu i śledzenia zadań w powiązanych obciążeń pracą, ale dla narzucania niektórych ograniczeń — takie jak hello maksymalną czasu wykonywania zadania hello (i przez rozszerzenie, jego zadań podrzędnych) i priorytet zadania w zadaniach tooother relacji hello konta usługi partia zadań. W tym przykładzie jednak hello zadanie jest skojarzone tylko z pulą hello, który został utworzony w kroku #3. Żadne dodatkowe właściwości nie są konfigurowane.

Wszystkie zadania usługi Batch są skojarzone z określoną pulą. To skojarzenie wskazuje węzły, które hello zadania wykonania na. Określ pulę hello przy użyciu hello [PoolInformation] [ py_poolinfo] właściwości, jak pokazano w hello poniższy fragment kodu.

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with hello specified ID, associated with hello specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID for hello job.
    :param str pool_id: hello ID for hello pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

Teraz, kiedy zadania został utworzony, zadania są dodawane tooperform hello pracy.

## <a name="step-5-add-tasks-toojob"></a>Krok 5: Dodawanie toojob zadań
![Dodaj toojob zadań][5]<br/>
*(1) zadania są dodawane toohello zadania, zadania (2) hello są zaplanowane toorun w węzłach i (3) hello zadania Pobierz tooprocess pliki danych hello*

Wsadowe **zadania** są hello poszczególnych jednostek pracy wykonywanych na powitania węzły obliczeniowe. Zadanie ma wiersza polecenia i uruchamia hello skrypty lub pliki wykonywalne, w tym wierszu polecenia.

tooactually wykonywania pracy, zadań, należy dodać tooa zadania. Każdy [CloudTask] [ py_task] jest skonfigurowana właściwość wiersza polecenia i [ResourceFiles] [ py_resource_file] (tak jak StartTask hello puli) tego hello zadanie pobiera węzła toohello przed jego wiersza polecenia jest wykonywane automatycznie. W przykładowym hello każde zadanie przetwarza tylko jeden plik. W związku z tym jego kolekcja ResourceFiles zawiera jeden element.

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in hello collection toohello specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID of hello job toowhich tooadd hello tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: hello ID of an Azure Blob storage container to
    which hello tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    hello specified Azure Blob storage container.
    """

    print('Adding {} tasks toojob [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [!IMPORTANT]
> Podczas uzyskiwania dostępu do zmiennych środowiskowych takich jak `$AZ_BATCH_NODE_SHARED_DIR` lub wykonywanie aplikacji nie można odnaleźć w węźle hello `PATH`, wiersze poleceń zadań należy wywołać hello skorupach jawnie, takich jak z `/bin/sh -c MyTaskApplication $MY_ENV_VAR`. To wymaganie nie jest konieczne, jeśli zadania wykonywania aplikacji w węźle hello `PATH` i nie odwołuje się do zmiennych środowiskowych.
>
>

W ramach hello `for` pętli we fragmencie kodu hello powyżej, zobaczysz, że hello wiersz polecenia dla zadania hello składa się z pięciu argumentów wiersza polecenia, które są przekazywane za*python_tutorial_task.py*:

1. **FilePath**: to jest plik toohello ścieżka lokalna hello, ponieważ znajduje się w węźle hello. Gdy hello obiektu ResourceFile w `upload_file_to_container` został utworzony w kroku 2 powyżej, nazwa pliku hello była używana dla tej właściwości (hello `file_path` parametru w Konstruktorze ResourceFile hello). Wskazuje, czy plik hello znajdują się w hello takie same katalogu w węźle hello jako *python_tutorial_task.py*.
2. **NUMWORDS**: hello górnej *N* wyrazy mają być zapisywane toohello pliku wyjściowego.
3. **Konto magazynu**: hello nazwę konta magazynu, który jest właścicielem danych wyjściowych zadania hello hello kontenera toowhich hello należy przekazać.
4. **storagecontainer**: Nazwa hello hello toowhich kontenera magazynu hello output można przekazywać pliki.
5. **sastoken**: sygnatury dostępu współdzielonego hello (SAS), która zapewnia dostęp do zapisu toohello **dane wyjściowe** kontenera w magazynie Azure. Hello *python_tutorial_task.py* skrypt używa tego sygnatury dostępu współdzielonego po utworzeniu jego odwołania BlockBlobService. Zapewnia dostęp do zapisu toohello kontenera bez konieczności klucz dostępu dla konta magazynu hello.

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a>Krok 6: monitorowanie podzadań
![Monitorowanie podzadań][6]<br/>
*Witaj zadania hello monitorów (1) dla stanu ukończenia i (2) hello zadania przekazać wynik tooAzure danych magazynu*

Jeśli zadania zostaną dodane zadania tooa, są automatycznie w kolejce i zaplanowane do uruchomienia w węzłach obliczeń w puli hello skojarzone z zadaniem hello. Na podstawie hello ustawień przez użytkownika, partii obsługuje wszystkich zadań usługi kolejkowania, planowania, ponawianie próby i obowiązków administracyjnych innych zadań za Ciebie.

Istnieje wiele metod toomonitoring wykonywania zadania. Witaj `wait_for_tasks_to_complete` działać w *python_tutorial_client.py* udostępnia prosty przykład monitorowania zadań dla niektórych stanu, w tym przypadku hello [ukończone] [ py_taskstate] Stan.

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in hello specified job reach hello Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello id of hello job whose tasks should be toomonitored.
    :param timedelta timeout: hello duration toowait for task completion. If all
    tasks in hello specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a>Krok 7: pobranie danych wyjściowych podzadań
![Pobieranie danych wyjściowych zadań podrzędnych z usługi Storage][7]<br/>

Teraz, hello ukończenia zadania, dane wyjściowe zadania hello hello można pobrać z magazynu Azure. Odbywa się przy użyciu wywołania zbyt`download_blobs_from_container` w *python_tutorial_client.py*:

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from hello specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: hello Azure Blob storage container from which to
     download files.
    :param directory_path: hello local directory toowhich toodownload hello files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] too{}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> Witaj wywołanie za`download_blobs_from_container` w *python_tutorial_client.py* Określa, czy pliki hello powinny być pobrany tooyour katalogu macierzystego. Możesz wolnego toomodify to lokalizacji wyjściowej.
>
>

## <a name="step-8-delete-containers"></a>Krok 8: usuwanie kontenerów
Naliczane są opłaty za dane przechowywane w usłudze Azure Storage, dlatego jest zawsze tooremove dobrym rozwiązaniem, wszystkie obiekty BLOB, które są już potrzebne dla zadań wsadowych. W *python_tutorial_client.py*, odbywa się z trzech wywołań zbyt[BlockBlobService.delete_container][py_delete_container]:

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>Krok 9: Usuwanie hello zadania i hello puli
W ostatnim kroku hello są zostanie wyświetlony monit o toodelete hello zadania i hello puli utworzone przez hello *python_tutorial_client.py* skryptu. Mimo że nie są naliczane opłaty za same zadania i podzadania, *są* naliczane opłaty za węzły obliczeniowe. W związku z tym zaleca się przydzielanie węzłów tylko zależnie do potrzeb. Usuwanie nieużywanych pul może odbywać się podczas konserwacji.

Witaj BatchServiceClient [JobOperations] [ py_job] i [PoolOperations] [ py_pool] mają odpowiednie metody usunięcia, które są wywołuje się, jeśli potwierdzenie usunięcia:

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> Należy pamiętać, że opłaty są naliczane za zasoby obliczeniowe — usunięcie nieużywanych pul zminimalizuje koszty. Ponadto należy pamiętać, że usunięcie puli spowoduje usunięcie wszystkich węzłów obliczeniowych w tej puli, a wszystkie dane na powitania węzły będą nieodwracalny po usunięciu hello puli.
>
>

## <a name="run-hello-sample-script"></a>Uruchom skrypt przykładowy hello
Po uruchomieniu hello *python_tutorial_client.py* skryptu z samouczka hello [przykładowy kod][github_article_samples], dane wyjściowe konsoli hello jest podobne toohello poniżej. Jest wstrzymany w `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` podczas puli hello węzły obliczeniowe są tworzone uruchomiona, a polecenia hello w puli hello rozpoczęcia zadania są wykonywane. Użyj hello [portalu Azure] [ azure_portal] toomonitor puli, węzły obliczeniowe, zadań i zadań podczas i po zakończeniu wykonywania. Użyj hello [portalu Azure] [ azure_portal] lub hello [Eksploratora usługi Microsoft Azure Storage] [ storage_explorer] tooview hello zasobów magazynu (kontenerów i obiektów blob) które są tworzone przez aplikację hello.

> [!TIP]
> Uruchom hello *python_tutorial_client.py* skrypt z wewnątrz hello `azure-batch-samples/Python/Batch/article_samples` katalogu. Ścieżka względna używa hello `common.helpers` importowania modułu, więc można napotkać `ImportError: No module named 'common'` Jeżeli nie uruchomisz hello skrypt w tym katalogu.
>
>

Typowy czas wykonywania jest **około 5-7 minut** po uruchomieniu próbki hello w konfiguracji domyślnej.

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py toocontainer [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt toocontainer [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks toojob [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached hello 'Completed' state within hello specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] too/home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] too/home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] too/home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER tooexit...
```

## <a name="next-steps"></a>Następne kroki
Uznać za zmiany wolnego toomake*python_tutorial_client.py* i *python_tutorial_task.py* tooexperiment innej obliczania scenariuszy. Na przykład, spróbuj opóźnienie wykonywania zbyt*python_tutorial_task.py* toosimulate długotrwałych zadań i monitorować je na powitania portalu. Spróbuj dodać więcej zadań lub dostosowanie hello liczba węzłów obliczeniowych. Dodaj logikę toocheck dla i Zezwalaj na użycie hello istniejących czas wykonywania toospeed puli.

Teraz, kiedy znasz hello podstawowy przepływ pracy rozwiązania partii, jest toodig czasu w toohello dodatkowe funkcje hello usługa partia zadań.

* Przejrzyj hello [funkcji partii omówienie Azure](batch-api-basics.md) artykułu, w którym firma Microsoft zaleca, jeśli masz nową usługę toohello.
* Uruchomienie hello inne artykuły programowanie partii w obszarze **programowanie szczegółowe** w hello [ścieżka szkoleniowa dotycząca partii][batch_learning_path].
* Zapoznaj się z inną implementację przetwarzania obciążenie hello "pierwszych N wyrazy" z partii w hello [TopNWords] [ github_topnwords] próbki.

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage
[pypi_install]: https://packaging.python.org/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-python-tutorial/batch_workflow_01_sm.png "Tworzenie kontenerów w usłudze Azure Storage"
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Zadanie przekazywania aplikacji i wejściowych (dane) pliki toocontainers"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Tworzenie puli usługi Batch"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Tworzenie zadania w usłudze Batch"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Dodaj toojob zadań"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Monitorowanie podzadań"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Pobieranie danych wyjściowych podzadań z usługi Storage"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Przepływ pracy w rozwiązaniu usługi Batch (pełny diagram)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Poświadczenia usługi Batch w portalu"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Poświadczenia usługi Storage w portalu"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Przepływ pracy rozwiązania w usłudze Batch (diagram minimalny)"
