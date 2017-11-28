---
title: "aaaRun partii zadań Azure zadania end-to-end bez pisania kodu (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Utwórz pliki szablonów hello Azure CLI toocreate partii pule, zadań i zadań."
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="d5a5f-103">Korzystanie z szablonów interfejsu wiersza polecenia usługi Azure Batch i transferu plików (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="d5a5f-103">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="d5a5f-104">Przy użyciu interfejsu wiersza polecenia Azure hello jest możliwe toorun zadań wsadowych bez pisania kodu.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-104">Using hello Azure CLI it is possible toorun Batch jobs without writing code.</span></span>

<span data-ttu-id="d5a5f-105">Pliki szablonów można tworzyć i używać z hello interfejsu wiersza polecenia Azure, umożliwiające pule, zadań i zadań toobe utworzone partii.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-105">Template files can be created and used with hello Azure CLI that allow Batch pools, jobs, and tasks toobe created.</span></span> <span data-ttu-id="d5a5f-106">Pliki wejściowe zadania mogą być łatwo przekazywane hello konta magazynu skojarzone z hello konta i zadania dane wyjściowe pliki wsadowe pobrane.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-106">Job input files can be easily uploaded to hello storage account associated with hello Batch account and job output files downloaded.</span></span>

## <a name="overview"></a><span data-ttu-id="d5a5f-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d5a5f-107">Overview</span></span>

<span data-ttu-id="d5a5f-108">Toohello rozszerzenie interfejsu wiersza polecenia Azure umożliwia partii toobe używane na całej trasie przez użytkowników, którzy nie są deweloperów.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-108">An extension toohello Azure CLI enables Batch toobe used end-to-end by users who are not developers.</span></span> <span data-ttu-id="d5a5f-109">Można utworzyć puli, przekazać dane wejściowe, zadań i skojarzonych zadań tworzenia i hello wynikowe dane wyjściowe pobrane — kod nie jest wymagany, hello interfejsu wiersza polecenia używane bezpośrednio lub zintegrowania skryptów.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-109">A pool can be created, input data uploaded, jobs and associated tasks created, and hello resulting output data downloaded – no code required, hello CLI being used directly or being integrated into scripts.</span></span>

<span data-ttu-id="d5a5f-110">Tworzenie szablonów partii na powitania [istniejących obsługę partii w hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) umożliwiająca pliki w formacie JSON wartości właściwości toospecify hello tworzenia pul, zadania, zadania i inne elementy.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-110">Batch templates build on hello [existing Batch support in hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) that allows JSON files toospecify property values for hello creation of pools, jobs, tasks, and other items.</span></span> <span data-ttu-id="d5a5f-111">Z szablonami partii hello następujące funkcje są dodawane przez co to jest możliwe z plikami JSON hello:</span><span class="sxs-lookup"><span data-stu-id="d5a5f-111">With Batch templates, hello following capabilities are added over what is possible with hello JSON files:</span></span>

-   <span data-ttu-id="d5a5f-112">Można zdefiniować parametrów.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-112">Parameters can be defined.</span></span> <span data-ttu-id="d5a5f-113">Jeśli szablon hello jest używany, tylko wartości parametrów hello są toocreate określony element hello, o wartości innych właściwości elementu określany w treści szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-113">When hello template is used, only hello parameter values are specified toocreate hello item, with other item property values being specified in hello template body.</span></span> <span data-ttu-id="d5a5f-114">Użytkownik, który rozumie, iż partii i toobe aplikacje uruchamiane przez partię można utworzyć szablony, określając puli, zadania i wartości właściwości zadania.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-114">A user who understands Batch and the applications toobe run by Batch can create templates, specifying pool, job, and task property values.</span></span> <span data-ttu-id="d5a5f-115">Użytkownik mniej znanych z partii i/lub aplikacje potrzebuje tylko wartości hello toospecify hello zdefiniowanych parametrów.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-115">A user less familiar with Batch and/or the applications only needs toospecify hello values for hello defined parameters.</span></span>

-   <span data-ttu-id="d5a5f-116">Utworzenie zadania fabryki zadań lub więcej zadań skojarzonych z zadaniem, unikając hello konieczność dla wielu toobe definicji zadania utworzone i znacznie uproszczenie przesyłanie zadań.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-116">Job task factories create one or more tasks associated with a job, avoiding hello need for many task definitions toobe created and significantly simplifying job submission.</span></span>


<span data-ttu-id="d5a5f-117">Pliki danych wejściowych muszą toobe podany dla zadań i plików danych wyjściowych często są tworzone.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-117">Input data files need toobe supplied for jobs and output data files are often produced.</span></span> <span data-ttu-id="d5a5f-118">Konto magazynu jest skojarzony domyślnie, z każdej z partii konta i pliki mogą być łatwo przekazanych tooand z tego konta magazynu przy użyciu interfejsu wiersza polecenia, z nie kodowania i wymagane nie poświadczenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-118">A storage account is associated, by default, with each Batch account and files can be easily transferred tooand from this storage account using the CLI, with no coding and no storage credentials required.</span></span>

<span data-ttu-id="d5a5f-119">Na przykład [ffmpeg](http://ffmpeg.org/) jest popularnych aplikacji, która przetwarza plików audio i wideo.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-119">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span></span> <span data-ttu-id="d5a5f-120">Hello Azure partii interfejsu wiersza polecenia mogą być używane tooinvoke ffmpeg tootranscode źródła plików wideo toodifferent rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-120">hello Azure Batch CLI can be used tooinvoke ffmpeg tootranscode source video files toodifferent resolutions.</span></span>

-   <span data-ttu-id="d5a5f-121">Utworzono szablon puli.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-121">A pool template is created.</span></span> <span data-ttu-id="d5a5f-122">Użytkownik Hello tworzenia szablonu hello zna, jak toocall hello ffmpeg aplikacji i jej wymagań; określają one hello odpowiedni system operacyjny, maszyna wirtualna rozmiar, jak ffmpeg jest zainstalowana (od pakietu aplikacji lub za pomocą Menedżera pakietów, na przykład) i innych wartości właściwości w puli.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-122">hello user creating hello template knows how toocall hello ffmpeg application and its requirements; they specify hello appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span></span> <span data-ttu-id="d5a5f-123">Parametry są tworzone, więc jeśli szablon hello jest używany, toobe określony wymaga tylko identyfikator puli hello i liczbę maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-123">Parameters are created so when hello template is used, only hello pool id and number of VMs need toobe specified.</span></span>

-   <span data-ttu-id="d5a5f-124">Utworzono szablon zadania.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-124">A job template is created.</span></span> <span data-ttu-id="d5a5f-125">Tworzenie szablonu hello Hello użytkownika wie jak ffmpeg toobe musi wywołać tootranscode źródła wideo tooa inną rozdzielczość i określa wiersz polecenia zadania hello; które znają, że istnieje folder zawierający pliki wideo źródłowe hello, z zadaniem wymagane dla pliku wejściowego.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-125">hello user creating hello template knows how ffmpeg needs toobe invoked tootranscode source video tooa different resolution and specifies hello task command line; they also know that there is a folder containing hello source video files, with a task required per input file.</span></span>

-   <span data-ttu-id="d5a5f-126">Użytkownik końcowy zestaw plików wideo tootranscode najpierw tworzy puli przy użyciu szablonu puli hello, określając tylko identyfikator puli hello i liczbę maszyn wirtualnych wymagana.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-126">An end user with a set of video files tootranscode first creates a pool using hello pool template, specifying only hello pool id and number of VMs required.</span></span> <span data-ttu-id="d5a5f-127">Następnie przekazywać hello źródła plików tootranscode.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-127">They can then upload hello source files tootranscode.</span></span> <span data-ttu-id="d5a5f-128">Następnie można przesłać zadania przy użyciu szablonu zadania hello tylko identyfikator puli hello i lokalizację plików źródłowych hello przekazany.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-128">A job can then be submitted using hello job template, specifying only hello pool id and location of hello source files uploaded.</span></span> <span data-ttu-id="d5a5f-129">zadania wsadowego Hello jest tworzony z jedno zadanie na Trwa generowanie pliku wejściowego.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-129">hello Batch job is created, with one task per input file being generated.</span></span> <span data-ttu-id="d5a5f-130">Ponadto pliki wyjściowe przekodowane hello można pobierania.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-130">Finally, hello transcoded output files can be download.</span></span>

## <a name="installation"></a><span data-ttu-id="d5a5f-131">Instalacja</span><span class="sxs-lookup"><span data-stu-id="d5a5f-131">Installation</span></span>

<span data-ttu-id="d5a5f-132">możliwości transferu szablonu i pliku Hello wymagają toobe rozszerzenie zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-132">hello template and file transfer capabilities require an extension toobe installed.</span></span>

<span data-ttu-id="d5a5f-133">Aby uzyskać instrukcje dotyczące sposobu hello tooinstall wiersza polecenia platformy Azure, zobacz [zainstalować Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d5a5f-133">For instructions on how tooinstall hello Azure CLI see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="d5a5f-134">Raz hello wiersza polecenia platformy Azure został zainstalowany, hello partii rozszerzenia można zainstalować przy użyciu interfejsu wiersza polecenia następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d5a5f-134">Once hello Azure CLI has been installed, hello Batch extension can be installed using the following CLI command:</span></span>

```azurecli
az component update --add batch-extensions --allow-third-party
```

<span data-ttu-id="d5a5f-135">Aby uzyskać więcej informacji na temat hello partii rozszerzenia, zobacz [Microsoft Azure partii CLI rozszerzeń dla systemu Windows, Mac i Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span><span class="sxs-lookup"><span data-stu-id="d5a5f-135">For more information about hello Batch extension, see [Microsoft Azure Batch CLI Extensions for Windows, Mac and Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span></span>

## <a name="templates"></a><span data-ttu-id="d5a5f-136">Szablony</span><span class="sxs-lookup"><span data-stu-id="d5a5f-136">Templates</span></span>

<span data-ttu-id="d5a5f-137">Witaj interfejsu wiersza polecenia usługi partia zadań Azure umożliwia elementów, takich jak pule, zadania i toobe zadania utworzone przez określenie plik JSON zawierający nazwy i wartości właściwości.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-137">hello Azure Batch CLI allows items such as pools, jobs, and tasks toobe created by specifying a JSON file containing property names and values.</span></span> <span data-ttu-id="d5a5f-138">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d5a5f-138">For example:</span></span>

```azurecli
az batch pool create –-json-file AppPool.json
```

<span data-ttu-id="d5a5f-139">Szablony usługi partia zadań Azure to podobne szablony Menedżera zasobów tooAzure, funkcje i składni.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-139">Azure Batch templates are similar tooAzure Resource Manager templates, in functionality and syntax.</span></span> <span data-ttu-id="d5a5f-140">Są to pliki w formacie JSON, które zawiera element nazwy i wartości właściwości, Dodaj następujące główne pojęcia hello:</span><span class="sxs-lookup"><span data-stu-id="d5a5f-140">They are JSON files that contain item property names and values, but add hello following main concepts:</span></span>

-   <span data-ttu-id="d5a5f-141">**Parametry**</span><span class="sxs-lookup"><span data-stu-id="d5a5f-141">**Parameters**</span></span>

    -   <span data-ttu-id="d5a5f-142">Zezwalaj na toobe wartości właściwości o tylko wartości parametrów konieczności toobe dostarczana, gdy używany jest szablon hello określone w sekcji body.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-142">Allow property values toobe specified in a body section, with only parameter values needing toobe supplied when hello template is used.</span></span> <span data-ttu-id="d5a5f-143">Na przykład hello pełnej definicji dla puli można można umieścić w treści hello i tylko jeden parametr zdefiniowane dla Identyfikator puli; tylko ciąg identyfikatora puli w związku z tym musi toocreate toobe dostarczony puli.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-143">For example, hello complete definition for a pool could be placed in hello body and only one parameter defined for pool id; only a pool id string therefore needs toobe supplied toocreate a pool.</span></span>
        
    -   <span data-ttu-id="d5a5f-144">treści szablonu Hello można tworzyć przez osobę mającą wiedzę na temat partii i toobe aplikacji hello uruchamiany w partii; Jeśli szablon hello jest używany, należy podać tylko wartości parametrów zdefiniowanych przez autora hello.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-144">hello template body can be authored by someone with knowledge of Batch and hello applications toobe run by Batch; only values for hello author-defined parameters must be supplied when hello template is used.</span></span> <span data-ttu-id="d5a5f-145">Użytkownik bez hello szczegółowe partii i/lub bazy wiedzy w związku z tym można używać szablonów.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-145">A user without hello in-depth Batch and/or application knowledge can therefore use the templates.</span></span>

-   <span data-ttu-id="d5a5f-146">**Zmienne**</span><span class="sxs-lookup"><span data-stu-id="d5a5f-146">**Variables**</span></span>

    -   <span data-ttu-id="d5a5f-147">Zezwalaj na toobe wartości parametru prostymi lub złożonymi określony w jednym miejscu i używany w co najmniej jednego miejsca w treści szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-147">Allow simple or complex parameter values toobe specified in one place and used in one or more places in hello template body.</span></span> <span data-ttu-id="d5a5f-148">Zmienne można uprościć i zredukować rozmiar hello hello szablonu, a także była bardziej utrzymaniu przez jedną właściwości toochange lokalizacji, którego wartość może zmienić.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-148">Variables can simplify and reduce hello size of hello template, as well as make it more maintainable by having one location toochange properties whose value may change.</span></span>

-   <span data-ttu-id="d5a5f-149">**Konstrukcji wyższego poziomu**</span><span class="sxs-lookup"><span data-stu-id="d5a5f-149">**Higher-level constructs**</span></span>

    -   <span data-ttu-id="d5a5f-150">Niektóre konstrukcji wyższego poziomu dostępnych w szablonie hello, które nie są jeszcze dostępne w hello interfejsów API partii.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-150">Some higher-level constructs are available in hello template that are not yet available in hello Batch APIs.</span></span> <span data-ttu-id="d5a5f-151">Na przykład można zdefiniować fabryki zadań w szablonie zadania, który tworzy wiele zadań dla zadania hello przy użyciu wspólnej definicji zadania.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-151">For example, a task factory can be defined in a job template that creates multiple tasks for hello job using a common task definition.</span></span> <span data-ttu-id="d5a5f-152">Te konstrukcje uniknąć toocode potrzeby hello dynamicznie utworzyć wiele plików JSON, takich jak jeden plik poszczególnych zadań, a także utworzyć skrypt aplikacji tooinstall plików za pomocą Menedżera pakietów, na przykład.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-152">These constructs avoid hello need toocode to dynamically create multiple JSON files, such as one file per task, as well as create script files tooinstall applications via a package manager, for example.</span></span>

    -   <span data-ttu-id="d5a5f-153">W niektórych punktu, w przypadku, gdy ma to zastosowanie, tych konstrukcji mogą być dodane toothe partii usługi i jest dostępny w hello interfejsów API partii, UI itp.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-153">At some point, where applicable, these constructs may be added toothe Batch service and available in hello Batch APIs, UIs, etc.</span></span>

### <a name="pool-templates"></a><span data-ttu-id="d5a5f-154">Szablony puli</span><span class="sxs-lookup"><span data-stu-id="d5a5f-154">Pool templates</span></span>

<span data-ttu-id="d5a5f-155">Oprócz możliwości standardowego szablonu toohello parametry i zmienne, powitania po konstrukcji wyższego poziomu są obsługiwane przez szablon puli hello:</span><span class="sxs-lookup"><span data-stu-id="d5a5f-155">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello pool template:</span></span>

-   <span data-ttu-id="d5a5f-156">**Odwołania do pakietu**</span><span class="sxs-lookup"><span data-stu-id="d5a5f-156">**Package references**</span></span>

    -   <span data-ttu-id="d5a5f-157">Opcjonalnie umożliwia węzłów toopool toobe skopiowane oprogramowania przy użyciu pakietu menedżerów.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-157">Optionally allows software toobe copied toopool nodes by using package managers.</span></span> <span data-ttu-id="d5a5f-158">określono Menedżera pakietów Hello i identyfikator pakietu.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-158">hello package manager and package id are specified.</span></span> <span data-ttu-id="d5a5f-159">Trwa stanie toodeclare pozwala uniknąć jeden lub więcej pakietów hello potrzeby toocreate skrypt, który pobiera hello wymagane pakiety hello skrypt instalacji i uruchom skrypt hello w każdym węźle puli.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-159">Being able toodeclare one or more packages avoids hello need toocreate a script that gets hello required packages, install hello script, and run hello script on each pool node.</span></span>

<span data-ttu-id="d5a5f-160">Hello poniżej przedstawiono przykładowy szablon, który tworzy puli maszyn wirtualnych systemu Linux z ffmpeg zainstalowana i tylko wymaga puli ciągów i hello identyfikator toouse toobe dostarczony maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="d5a5f-160">hello following is an example of a template that creates a pool of Linux VMs with ffmpeg installed and only requires a pool id string and hello number of VMs toobe supplied toouse:</span></span>

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

<span data-ttu-id="d5a5f-161">Jeśli plik szablonu hello miał nazwę _ffmpeg.json puli_, a następnie hello szablon będzie można wywołać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d5a5f-161">If hello template file was named _pool-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a><span data-ttu-id="d5a5f-162">Szablony zadań</span><span class="sxs-lookup"><span data-stu-id="d5a5f-162">Job templates</span></span>

<span data-ttu-id="d5a5f-163">Oprócz możliwości standardowego szablonu toohello parametry i zmienne, powitania po konstrukcji wyższego poziomu są obsługiwane przez szablon zadania hello:</span><span class="sxs-lookup"><span data-stu-id="d5a5f-163">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello job template:</span></span>

-   <span data-ttu-id="d5a5f-164">**Fabryki zadań**</span><span class="sxs-lookup"><span data-stu-id="d5a5f-164">**Task factory**</span></span>

    -   <span data-ttu-id="d5a5f-165">Tworzy wiele zadań dla zadania na podstawie definicji zadania.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-165">Creates multiple tasks for a job from one task definition.</span></span> <span data-ttu-id="d5a5f-166">Trzy typy fabryki zadań są obsługiwane — parametrycznych odchylenia zadań dla każdego pliku i zadań w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-166">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span></span>

<span data-ttu-id="d5a5f-167">Hello poniżej przedstawiono przykładowy szablon, który tworzy zadanie, które używa ffmpeg do tooone plików wideo MP4 transkodowanie dwa niższe rozdzielczości, z jednego zadania utworzone na źródłowy plik wideo:</span><span class="sxs-lookup"><span data-stu-id="d5a5f-167">hello following is an example of a template that creates a job that uses ffmpeg to transcode MP4 video files tooone of two lower resolutions, with one task created per source video file:</span></span>

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

<span data-ttu-id="d5a5f-168">Jeśli plik szablonu hello miał nazwę _ffmpeg.json zadania_, a następnie hello szablon będzie można wywołać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d5a5f-168">If hello template file was named _job-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a><span data-ttu-id="d5a5f-169">Grup plików i transferu plików</span><span class="sxs-lookup"><span data-stu-id="d5a5f-169">File groups and file transfer</span></span>

<span data-ttu-id="d5a5f-170">Większość zadań i zadań wymagane pliki wejściowe i utworzyć pliki danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-170">Most jobs and tasks require input files and produce output files.</span></span> <span data-ttu-id="d5a5f-171">Oba pliki wejściowe i pliki wyjściowe zwykle wymagają toobe przeniesione z powitania klienta toohello węzła lub z hello węzła toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-171">Both input files and output files typically need toobe transferred, either from hello client toohello node, or from hello node toohello client.</span></span> <span data-ttu-id="d5a5f-172">Hello rozszerzenie interfejsu wiersza polecenia Azure partii abstracts transfer plików zadań i korzysta z konta magazynu hello utworzony domyślnie dla każdego konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-172">hello Azure Batch CLI extension abstracts away file transfer and utilizes hello storage account that is created by default for each Batch account.</span></span>

<span data-ttu-id="d5a5f-173">Grupa plików oznacza tooa kontener, który jest tworzony w hello kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-173">A file group equates tooa container that is created in hello Azure storage account.</span></span> <span data-ttu-id="d5a5f-174">grupy plików Hello może mieć podfoldery.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-174">hello file group may have subfolders.</span></span>

<span data-ttu-id="d5a5f-175">Hello rozszerzenia partii interfejsu wiersza polecenia zawiera polecenia służące do przekazywania plików z grupy określony plik tooa klientów i pobieranie plików z hello określonego pliku grupy tooa klienta.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-175">hello Batch CLI extension provides commands for uploading files from client tooa specified file group and downloading files from hello specified file group tooa client.</span></span>

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

<span data-ttu-id="d5a5f-176">Zezwalaj na pliki przechowywane w pliku grup toobe określony dla kopiowania na węzłach puli szablonów puli i zadania lub Wyłącz pulę węzłów wykonaj kopię tooa grupy plików.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-176">Pool and job templates allow files stored in file groups toobe specified for copy onto pool nodes or off pool nodes back tooa file group.</span></span> <span data-ttu-id="d5a5f-177">Na przykład w szablonie zadania poprzednio określono, hello grupy "ffmpeg — wejście" jest określony dla fabryki zadań hello jako hello lokalizację plików źródłowych hello wideo kopiowane na węzeł hello transkodowanie; Witaj grupy "ffmpeg-danych wyjściowych w pliku" jest używany jako hello lokalizacji, w którym pliki wyjściowe przekodowane hello są kopiowane węzeł hello toofrom działa każdego zadania.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-177">For example, in the job template specified previously, hello file group “ffmpeg-input” is specified for hello task factory as hello location of hello source video files copied down onto hello node for transcoding; hello file group “ffmpeg-output” is used as hello location where hello transcoded output files are copied toofrom hello node running each task.</span></span>

## <a name="summary"></a><span data-ttu-id="d5a5f-178">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="d5a5f-178">Summary</span></span>

<span data-ttu-id="d5a5f-179">Obsługa transferu szablon i plik obecnie zostały dodane toohello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-179">Template and file transfer support have currently been added only toohello Azure CLI.</span></span> <span data-ttu-id="d5a5f-180">Celem Hello jest tooexpand hello odbiorców, którzy mogą używać toousers wsadowego, który nie ma potrzeby toodevelop kodu za pomocą hello interfejsów API usługi partia zadań, takich jak pracowników naukowo-badawczych, udziałem użytkowników IT i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-180">hello goal is tooexpand hello audience that can use Batch toousers who do not need toodevelop code using hello Batch APIs, such as researchers, IT users, and so on.</span></span> <span data-ttu-id="d5a5f-181">Bez kodowania, użytkownicy mający wiedzę na temat platformy Azure, partii i toobe aplikacji hello Uruchom przez partię można utworzyć szablony do tworzenia puli i zadania.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-181">Without coding, users with knowledge of Azure, Batch, and hello applications toobe run by Batch can create templates for pool and job creation.</span></span> <span data-ttu-id="d5a5f-182">Parametry szablonu użytkowników bez szczegółowej znajomości partii i hello aplikacji można za pomocą szablonów hello.</span><span class="sxs-lookup"><span data-stu-id="d5a5f-182">With template parameters, users without detailed knowledge of Batch and hello applications can use hello templates.</span></span>

<span data-ttu-id="d5a5f-183">Wypróbowanie hello partii rozszerzenie hello wiersza polecenia platformy Azure i uzyskaliśmy wszelkie opinie i sugestie, albo w hello komentarzy tego artykułu lub za pośrednictwem hello [forum usługi partia zadań Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span><span class="sxs-lookup"><span data-stu-id="d5a5f-183">Try out hello Batch extension for hello Azure CLI and provide us with any feedback or suggestions, either in hello comments for this article or via hello [Azure Batch forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5a5f-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d5a5f-184">Next steps</span></span>

- <span data-ttu-id="d5a5f-185">Zobacz hello partii szablony wpisie w blogu: [za pomocą zadania uruchamiania partii zadań Azure hello Azure CLI — kod nie jest wymagany](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span><span class="sxs-lookup"><span data-stu-id="d5a5f-185">See hello Batch templates blog post: [Running Azure Batch jobs using hello Azure CLI – no code required](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span></span>
- <span data-ttu-id="d5a5f-186">Szczegółowa dokumentacja instalacji i użycia, przykłady i kodu źródłowego są dostępne w hello [repozytorium Azure GitHub](https://github.com/Azure/azure-batch-cli-extensions).</span><span class="sxs-lookup"><span data-stu-id="d5a5f-186">Detailed installation and usage documentation, samples, and source code are available in hello [Azure GitHub repository](https://github.com/Azure/azure-batch-cli-extensions).</span></span>
