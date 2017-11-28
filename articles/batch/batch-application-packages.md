---
title: "pakiety aplikacji aaaInstall w węzłach obliczeniowych - partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Użyj funkcji pakietów aplikacji hello z tooeasily partii zadań Azure zarządzać wieloma aplikacjami i węzły obliczeniowe w wersji do instalacji w partii."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a><span data-ttu-id="373e0-103">Wdrażanie aplikacji toocompute węzłów za pomocą pakietów aplikacji partii</span><span class="sxs-lookup"><span data-stu-id="373e0-103">Deploy applications toocompute nodes with Batch application packages</span></span>

<span data-ttu-id="373e0-104">Funkcja pakiety aplikacji Hello partii zadań Azure umożliwia łatwe zarządzanie aplikacji zadań i ich toohello wdrożenia obliczeniowe węzłów w puli.</span><span class="sxs-lookup"><span data-stu-id="373e0-104">hello application packages feature of Azure Batch provides easy management of task applications and their deployment toohello compute nodes in your pool.</span></span> <span data-ttu-id="373e0-105">Pakiety aplikacji możesz przekazać i zarządzanie wieloma wersjami aplikacji hello, których uruchamianie zadań, łącznie z ich pliki pomocnicze.</span><span class="sxs-lookup"><span data-stu-id="373e0-105">With application packages, you can upload and manage multiple versions of hello applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="373e0-106">Można następnie automatycznie wdrożyć jeden lub więcej z tych aplikacji toohello obliczeniowe węzłów w puli.</span><span class="sxs-lookup"><span data-stu-id="373e0-106">You can then automatically deploy one or more of these applications toohello compute nodes in your pool.</span></span>

<span data-ttu-id="373e0-107">W tym artykule przedstawiono sposób tooupload pakiety aplikacji w hello portalu Azure i zarządzać nimi.</span><span class="sxs-lookup"><span data-stu-id="373e0-107">In this article, you will learn how tooupload and manage application packages in hello Azure portal.</span></span> <span data-ttu-id="373e0-108">Następnie dowiesz się jak tooinstall je w puli węzły obliczeniowe z hello [partiami platformy .NET] [ api_net] biblioteki.</span><span class="sxs-lookup"><span data-stu-id="373e0-108">You will then learn how tooinstall them on a pool's compute nodes with hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="373e0-109">Pakiety aplikacji są obsługiwane we wszystkich pulach usługi Batch utworzonych po 5 lipca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="373e0-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="373e0-110">Są one obsługiwane w pulach partii utworzyć między 10 marca 2016 i 5 2017 lipca tylko wtedy, gdy pula hello został utworzony za pomocą konfiguracji usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="373e0-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="373e0-111">Pule partii utworzone przed too10 marca 2016 r nie obsługują pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="373e0-111">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="373e0-112">Witaj interfejsy API umożliwiające tworzenie i zarządzanie pakiety aplikacji są częścią hello [zarządzania partiami platformy .NET] [[api_net_mgmt]] biblioteki.</span><span class="sxs-lookup"><span data-stu-id="373e0-112">hello APIs for creating and managing application packages are part of hello [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="373e0-113">Witaj interfejsy API do instalowania pakietów aplikacji w węźle obliczeń są częścią hello [partiami platformy .NET] [ api_net] biblioteki.</span><span class="sxs-lookup"><span data-stu-id="373e0-113">hello APIs for installing application packages on a compute node are part of hello [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="373e0-114">Funkcja pakiety aplikacji Hello opisanych tutaj zastępuje funkcji partii aplikacji hello dostępne w poprzednich wersjach usługi hello.</span><span class="sxs-lookup"><span data-stu-id="373e0-114">hello application packages feature described here supersedes hello Batch Apps feature available in previous versions of hello service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="373e0-115">Wymagania dotyczące pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="373e0-115">Application package requirements</span></span>
<span data-ttu-id="373e0-116">toouse pakietów aplikacji, należy za[połączyć konto usługi Azure Storage](#link-a-storage-account) tooyour konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="373e0-116">toouse application packages, you need too[link an Azure Storage account](#link-a-storage-account) tooyour Batch account.</span></span>

<span data-ttu-id="373e0-117">Ta funkcja została wprowadzona w [interfejsu API REST partii] [ api_rest] wersji 2015-12-01.2.2 i hello odpowiadającego [partiami platformy .NET] [ api_net] wersji biblioteki 3.1.0.</span><span class="sxs-lookup"><span data-stu-id="373e0-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and hello corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="373e0-118">Firma Microsoft zaleca zawsze używać najnowszej wersji interfejsu API hello podczas pracy z partii.</span><span class="sxs-lookup"><span data-stu-id="373e0-118">We recommend that you always use hello latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="373e0-119">Pakiety aplikacji są obsługiwane we wszystkich pulach usługi Batch utworzonych po 5 lipca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="373e0-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="373e0-120">Są one obsługiwane w pulach partii utworzyć między 10 marca 2016 i 5 2017 lipca tylko wtedy, gdy pula hello został utworzony za pomocą konfiguracji usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="373e0-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="373e0-121">Pule partii utworzone przed too10 marca 2016 r nie obsługują pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="373e0-121">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="373e0-122">Aplikacje i pakiety aplikacji — informacje</span><span class="sxs-lookup"><span data-stu-id="373e0-122">About applications and application packages</span></span>
<span data-ttu-id="373e0-123">W partii zadań Azure *aplikacji* odwołuje się zestaw tooa numerów wersji plików binarnych, które mogą być automatycznie pobierane toohello węzłów obliczeniowych w puli.</span><span class="sxs-lookup"><span data-stu-id="373e0-123">Within Azure Batch, an *application* refers tooa set of versioned binaries that can be automatically downloaded toohello compute nodes in your pool.</span></span> <span data-ttu-id="373e0-124">*Pakiet aplikacji* odwołuje się tooa *określonego zestawu* tych danych binarnych i reprezentuje danego *wersji* aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="373e0-124">An *application package* refers tooa *specific set* of those binaries and represents a given *version* of hello application.</span></span>

<span data-ttu-id="373e0-125">![Diagramu wysokiego poziomu aplikacji i pakietów aplikacji][1]</span><span class="sxs-lookup"><span data-stu-id="373e0-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="373e0-126">Aplikacje</span><span class="sxs-lookup"><span data-stu-id="373e0-126">Applications</span></span>
<span data-ttu-id="373e0-127">Aplikacja w partii zawiera jeden lub więcej aplikacji, pakietów i opcje konfiguracji dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="373e0-127">An application in Batch contains one or more application packages and specifies configuration options for hello application.</span></span> <span data-ttu-id="373e0-128">Na przykład aplikacji można określić hello domyślna aplikacja pakietu wersji tooinstall węzłów obliczeniowych i czy jego pakietów można zaktualizować lub usunąć.</span><span class="sxs-lookup"><span data-stu-id="373e0-128">For example, an application can specify hello default application package version tooinstall on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="373e0-129">Pakiety aplikacji</span><span class="sxs-lookup"><span data-stu-id="373e0-129">Application packages</span></span>
<span data-ttu-id="373e0-130">Pakiet aplikacji jest plik zip, który zawiera pliki binarne aplikacji hello i pliki pomocnicze, które są wymagane dla aplikacji hello toorun zadania.</span><span class="sxs-lookup"><span data-stu-id="373e0-130">An application package is a .zip file that contains hello application binaries and supporting files that are required for your tasks toorun hello application.</span></span> <span data-ttu-id="373e0-131">Każdy pakiet aplikacji reprezentuje określoną wersję aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="373e0-131">Each application package represents a specific version of hello application.</span></span>

<span data-ttu-id="373e0-132">Można określić pakietów aplikacji na poziomie hello puli i zadań.</span><span class="sxs-lookup"><span data-stu-id="373e0-132">You can specify application packages at hello pool and task levels.</span></span> <span data-ttu-id="373e0-133">Podczas tworzenia puli lub zadania można określić co najmniej jeden z tych pakietów i (opcjonalnie) wersja.</span><span class="sxs-lookup"><span data-stu-id="373e0-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="373e0-134">**Pakiety aplikacji w puli** są wdrażane za*co* węzła w puli hello.</span><span class="sxs-lookup"><span data-stu-id="373e0-134">**Pool application packages** are deployed too*every* node in hello pool.</span></span> <span data-ttu-id="373e0-135">Gdy węzeł dołącza pulę i gdy jest ponownego rozruchu lub odtworzenia z obrazu wdrożenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="373e0-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="373e0-136">Pakiety aplikacji w puli są odpowiednie, wszystkie węzły w puli wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="373e0-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="373e0-137">Podczas tworzenia puli, można dodać lub zaktualizować pakiety istniejącej puli, można określić co najmniej jednego pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="373e0-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="373e0-138">Aktualizuj istniejącą pulę aplikacji pakietów, należy ponownie uruchomić jego węzły tooinstall hello nowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="373e0-138">If you update an existing pool's application packages, you must restart its nodes tooinstall hello new package.</span></span>
* <span data-ttu-id="373e0-139">**Zadanie pakietów aplikacji** są wdrażane tylko w węźle obliczeń tooa zaplanowane toorun zadania, po prostu, przed uruchomieniem zadania hello wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="373e0-139">**Task application packages** are deployed only tooa compute node scheduled toorun a task, just before running hello task's command line.</span></span> <span data-ttu-id="373e0-140">Jeśli hello określony pakiet aplikacji i wersji już znajduje się w węźle hello, nie jest wdrożone i istniejący pakiet hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="373e0-140">If hello specified application package and version is already on hello node, it is not redeployed and hello existing package is used.</span></span>
  
    <span data-ttu-id="373e0-141">Pakiety aplikacji zadań są przydatne w środowisku udostępnionych puli, której różne zadania są uruchamiane w jednej puli i hello puli nie zostanie usunięta po zakończeniu zadania.</span><span class="sxs-lookup"><span data-stu-id="373e0-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and hello pool is not deleted when a job is completed.</span></span> <span data-ttu-id="373e0-142">Jeśli zadanie ma mniejszą liczbę zadań niż węzłów w puli hello, pakiety aplikacji zadań można zminimalizować transfer danych, ponieważ aplikacja jest wdrożony toohello tylko węzły, które uruchamiania zadań.</span><span class="sxs-lookup"><span data-stu-id="373e0-142">If your job has fewer tasks than nodes in hello pool, task application packages can minimize data transfer since your application is deployed only toohello nodes that run tasks.</span></span>
  
    <span data-ttu-id="373e0-143">Inne scenariusze, które mogą korzystać z zadań pakiety aplikacji są zadań uruchamianych dużej aplikacji, ale tylko kilka zadań.</span><span class="sxs-lookup"><span data-stu-id="373e0-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="373e0-144">Na przykład przetwarzania wstępnego etap lub zadanie scalania, gdzie aplikacja hello przetwarzanie wstępne lub merge jest ogromnych, może korzystać z zadań pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="373e0-144">For example, a pre-processing stage or a merge task, where hello pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="373e0-145">Ma ograniczeń na powitania liczba aplikacji i pakietów aplikacji w ramach konta usługi partia zadań i rozmiar pakietu maksymalną aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="373e0-145">There are restrictions on hello number of applications and application packages within a Batch account and on hello maximum application package size.</span></span> <span data-ttu-id="373e0-146">Zobacz [przydziały i limity dla usługi partia zadań Azure hello](batch-quota-limit.md) szczegółowe informacje o tych ograniczeniach.</span><span class="sxs-lookup"><span data-stu-id="373e0-146">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="373e0-147">Korzyści wynikające z pakietów aplikacji</span><span class="sxs-lookup"><span data-stu-id="373e0-147">Benefits of application packages</span></span>
<span data-ttu-id="373e0-148">Pakiety aplikacji może uprościć kod hello rozwiązania partii i dolnym hello narzutów toomanage wymagane hello aplikacji uruchamianych zadań.</span><span class="sxs-lookup"><span data-stu-id="373e0-148">Application packages can simplify hello code in your Batch solution and lower hello overhead required toomanage hello applications that your tasks run.</span></span>

<span data-ttu-id="373e0-149">Z pakietami aplikacji zadania uruchamiania puli użytkownika nie ma toospecify długą listę tooinstall pliki pojedynczego zasobu w węzłach hello.</span><span class="sxs-lookup"><span data-stu-id="373e0-149">With application packages, your pool's start task doesn't have toospecify a long list of individual resource files tooinstall on hello nodes.</span></span> <span data-ttu-id="373e0-150">Nie masz toomanually Zarządzanie wieloma wersjami plików aplikacji w usłudze Azure Storage lub na węzły.</span><span class="sxs-lookup"><span data-stu-id="373e0-150">You don't have toomanually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="373e0-151">I nie ma potrzeby tooworry o generowaniu [adresy URL SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide dostępu toohello plików na Twoim koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="373e0-151">And, you don't need tooworry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide access toohello files in your Storage account.</span></span> <span data-ttu-id="373e0-152">Działa w tle hello z pakietów aplikacji usługi Azure Storage toostore partii i wdrażać je toocompute węzłów.</span><span class="sxs-lookup"><span data-stu-id="373e0-152">Batch works in hello background with Azure Storage toostore application packages and deploy them toocompute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="373e0-153">Witaj łączny rozmiar zadania uruchamiania musi być mniejsza lub równa znaków too32768, w tym plików zasobów i zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="373e0-153">hello total size of a start task must be less than or equal too32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="373e0-154">Jeśli zadanie start przekracza ten limit, za pomocą pakietów aplikacji jest inną opcją.</span><span class="sxs-lookup"><span data-stu-id="373e0-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="373e0-155">Można również utworzyć archiwum zip zawierającym pliki zasobów, przekaż go jako tooAzure obiektu blob magazynu i Rozpakuj go z wiersza polecenia hello rozpoczęcia zadania.</span><span class="sxs-lookup"><span data-stu-id="373e0-155">You can also create a zipped archive containing your resource files, upload it as a blob tooAzure Storage, and then unzip it from hello command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="373e0-156">Przekazywanie aplikacji i zarządzanie nimi</span><span class="sxs-lookup"><span data-stu-id="373e0-156">Upload and manage applications</span></span>
<span data-ttu-id="373e0-157">Można użyć hello [portalu Azure] [ portal] lub hello [zarządzania partiami platformy .NET](batch-management-dotnet.md) pakietów aplikacji hello toomanage biblioteki w ramach konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="373e0-157">You can use hello [Azure portal][portal] or hello [Batch Management .NET](batch-management-dotnet.md) library toomanage hello application packages in your Batch account.</span></span> <span data-ttu-id="373e0-158">W hello następne sekcje kilka, zostanie najpierw przedstawiony sposób toolink konta magazynu, następnie omówiono Dodawanie aplikacji i pakietów i zarządzania nimi z hello portalu.</span><span class="sxs-lookup"><span data-stu-id="373e0-158">In hello next few sections, we first show how toolink a Storage account, then discuss adding applications and packages and managing them with hello portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="373e0-159">Połącz konto magazynu</span><span class="sxs-lookup"><span data-stu-id="373e0-159">Link a Storage account</span></span>
<span data-ttu-id="373e0-160">toouse pakietów aplikacji, należy najpierw połączyć tooyour konta usługi Azure Storage konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="373e0-160">toouse application packages, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="373e0-161">Jeśli nie skonfigurowano jeszcze konta magazynu, hello portalu Azure Wyświetla hello ostrzeżenie po raz pierwszy kliknij hello **aplikacji** kafelka w hello **konto wsadowe** bloku.</span><span class="sxs-lookup"><span data-stu-id="373e0-161">If you have not yet configured a Storage account, hello Azure portal displays a warning hello first time you click hello **Applications** tile in hello **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="373e0-162">Obecnie partii obsługuje *tylko* hello **ogólnego przeznaczenia** typu konta magazynu, zgodnie z opisem w kroku 5, [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account)w [o Azure konta magazynu](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="373e0-162">Batch currently supports *only* hello **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="373e0-163">Po połączeniu tooyour konta usługi Azure Storage konta usługi partia zadań link *tylko* **ogólnego przeznaczenia** konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="373e0-163">When you link an Azure Storage account tooyour Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="373e0-164">![Ostrzeżenie "Nie skonfigurowano konta magazynu" w portalu Azure][9]</span><span class="sxs-lookup"><span data-stu-id="373e0-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="373e0-165">Witaj hello używa usługi partii skojarzone toostore konta magazynu pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="373e0-165">hello Batch service uses hello associated Storage account toostore your application packages.</span></span> <span data-ttu-id="373e0-166">Po połączeniu hello dwa konta partii można automatycznie wdrażać pakietów hello przechowywane w węzły obliczeniowe tooyour konta magazynu hello połączone.</span><span class="sxs-lookup"><span data-stu-id="373e0-166">After you've linked hello two accounts, Batch can automatically deploy hello packages stored in hello linked Storage account tooyour compute nodes.</span></span> <span data-ttu-id="373e0-167">toolink tooyour konta magazynu konta usługi partia zadań, kliknij przycisk **ustawienia konta magazynu** na powitania **ostrzeżenie** bloku, a następnie kliknij przycisk **konta magazynu** na powitania **Konta magazynu** bloku.</span><span class="sxs-lookup"><span data-stu-id="373e0-167">toolink a Storage account tooyour Batch account, click **Storage account settings** on hello **Warning** blade, and then click **Storage Account** on hello **Storage Account** blade.</span></span>

<span data-ttu-id="373e0-168">![Wybierz bloku konto magazynu w portalu Azure][10]</span><span class="sxs-lookup"><span data-stu-id="373e0-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="373e0-169">Zaleca się utworzenie konta magazynu *w szczególności* do użytku z kontem usługi partia zadań i zaznacz je tutaj.</span><span class="sxs-lookup"><span data-stu-id="373e0-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="373e0-170">Aby uzyskać szczegółowe informacje o tym, jak toocreate konta magazynu, zobacz "Tworzenie konta magazynu" w [konta usługi Azure Storage](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="373e0-170">For details about how toocreate a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="373e0-171">Po utworzeniu konta magazynu, można je następnie połączyć konto usługi partia zadań tooyour przy użyciu hello **konta magazynu** bloku.</span><span class="sxs-lookup"><span data-stu-id="373e0-171">After you've created a Storage account, you can then link it tooyour Batch account by using hello **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="373e0-172">Hello usługa partia zadań używa usługi Azure Storage toostore pakietów aplikacji jako blokowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="373e0-172">hello Batch service uses Azure Storage toostore your application packages as block blobs.</span></span> <span data-ttu-id="373e0-173">Jesteś [rozliczany jako normalne] [ storage_pricing] hello blokowych obiektów blob danych.</span><span class="sxs-lookup"><span data-stu-id="373e0-173">You are [charged as normal][storage_pricing] for hello block blob data.</span></span> <span data-ttu-id="373e0-174">Można się, że rozmiar hello tooconsider i liczbę pakietów aplikacji, a okresowe usuwanie pakietów przestarzałe toominimize kosztów.</span><span class="sxs-lookup"><span data-stu-id="373e0-174">Be sure tooconsider hello size and number of your application packages, and periodically remove deprecated packages toominimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="373e0-175">Wyświetl bieżące aplikacje</span><span class="sxs-lookup"><span data-stu-id="373e0-175">View current applications</span></span>
<span data-ttu-id="373e0-176">tooview aplikacji hello konta partii zadań kliknij hello **aplikacji** elementu menu w menu po lewej stronie powitania podczas wyświetlania hello **konto wsadowe** bloku.</span><span class="sxs-lookup"><span data-stu-id="373e0-176">tooview hello applications in your Batch account, click hello **Applications** menu item in hello left menu while viewing hello **Batch account** blade.</span></span>

<span data-ttu-id="373e0-177">![Kafelek aplikacji][2]</span><span class="sxs-lookup"><span data-stu-id="373e0-177">![Applications tile][2]</span></span>

<span data-ttu-id="373e0-178">Wybranie tej opcji menu otwiera hello **aplikacji** bloku:</span><span class="sxs-lookup"><span data-stu-id="373e0-178">Selecting this menu option opens hello **Applications** blade:</span></span>

<span data-ttu-id="373e0-179">![Lista aplikacji][3]</span><span class="sxs-lookup"><span data-stu-id="373e0-179">![List applications][3]</span></span>

<span data-ttu-id="373e0-180">Witaj **aplikacji** wyświetla bloku hello identyfikator każdej aplikacji w ramach Twojego konta i hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="373e0-180">hello **Applications** blade displays hello ID of each application in your account and hello following properties:</span></span>

* <span data-ttu-id="373e0-181">**Pakiety**: hello numer wersji skojarzonych z tą aplikacją.</span><span class="sxs-lookup"><span data-stu-id="373e0-181">**Packages**: hello number of versions associated with this application.</span></span>
* <span data-ttu-id="373e0-182">**Wersja domyślna**: wersja aplikacji hello zainstalowane, jeśli nie wskazują wersji po określeniu aplikacji hello puli.</span><span class="sxs-lookup"><span data-stu-id="373e0-182">**Default version**: hello application version installed if you do not indicate a version when you specify hello application for a pool.</span></span> <span data-ttu-id="373e0-183">To ustawienie jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="373e0-183">This setting is optional.</span></span>
* <span data-ttu-id="373e0-184">**Zezwalaj na aktualizacje**: hello wartość, która określa, czy pakiet aktualizacji, usuwanie i dodatki są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="373e0-184">**Allow updates**: hello value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="373e0-185">Jeśli ta opcja jest ustawiona zbyt**nr**, pakiet aktualizacji i usunięć są wyłączone dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="373e0-185">If this is set too**No**, package updates and deletions are disabled for hello application.</span></span> <span data-ttu-id="373e0-186">Można dodawać tylko nowe wersje pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="373e0-186">Only new application package versions can be added.</span></span> <span data-ttu-id="373e0-187">Domyślnie Hello **tak**.</span><span class="sxs-lookup"><span data-stu-id="373e0-187">hello default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="373e0-188">Wyświetlanie szczegółów aplikacji</span><span class="sxs-lookup"><span data-stu-id="373e0-188">View application details</span></span>
<span data-ttu-id="373e0-189">tooopen hello bloku, który zawiera szczegóły hello aplikacji hello aplikacji, wybierz pozycję w hello **aplikacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="373e0-189">tooopen hello blade that includes hello details for an application, select hello application in hello **Applications** blade.</span></span>

<span data-ttu-id="373e0-190">![Szczegóły aplikacji][4]</span><span class="sxs-lookup"><span data-stu-id="373e0-190">![Application details][4]</span></span>

<span data-ttu-id="373e0-191">W bloku szczegóły aplikacji hello można skonfigurować następujące ustawienia dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="373e0-191">In hello application details blade, you can configure hello following settings for your application.</span></span>

* <span data-ttu-id="373e0-192">**Zezwalaj na aktualizacje**: Określ, czy można zaktualizować lub usunąć jego pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="373e0-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="373e0-193">Zobacz "Aktualizowanie lub usuwanie pakietu aplikacji" w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="373e0-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="373e0-194">**Wersja domyślna**: Określ domyślną aplikację pakietu toodeploy toocompute węzłów.</span><span class="sxs-lookup"><span data-stu-id="373e0-194">**Default version**: Specify a default application package toodeploy toocompute nodes.</span></span>
* <span data-ttu-id="373e0-195">**Nazwa wyświetlana**: Określ przyjazną nazwę, która jest Twoje partii rozwiązania można użyć, gdy na przykład wyświetla informacje o aplikacji hello w hello interfejsu użytkownika usługi, która zapewniają tooyour klientów za pośrednictwem usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="373e0-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about hello application, for example, in hello UI of a service that you provide tooyour customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="373e0-196">Dodaj nową aplikację</span><span class="sxs-lookup"><span data-stu-id="373e0-196">Add a new application</span></span>
<span data-ttu-id="373e0-197">toocreate nowej aplikacji, Dodaj pakiet aplikacji i określ aplikacji nowy, unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="373e0-197">toocreate a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="373e0-198">Witaj pierwszy pakiet aplikacji, który możesz dodać nowy identyfikator aplikacji hello tworzy również hello nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="373e0-198">hello first application package that you add with hello new application ID also creates hello new application.</span></span>

<span data-ttu-id="373e0-199">Kliknij przycisk **Dodaj** na powitania **aplikacji** hello tooopen bloku **nowej aplikacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="373e0-199">Click **Add** on hello **Applications** blade tooopen hello **New application** blade.</span></span>

<span data-ttu-id="373e0-200">![Nowy blok aplikacji w portalu Azure][5]</span><span class="sxs-lookup"><span data-stu-id="373e0-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="373e0-201">Witaj **nowej aplikacji** bloku zapewnia hello poniższe pola toospecify hello ustawienia nowej aplikacji i pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="373e0-201">hello **New application** blade provides hello following fields toospecify hello settings of your new application and application package.</span></span>

<span data-ttu-id="373e0-202">**Identyfikator aplikacji**</span><span class="sxs-lookup"><span data-stu-id="373e0-202">**Application id**</span></span>

<span data-ttu-id="373e0-203">To pole określa identyfikator hello nowej aplikacji, czyli podmiotu toohello standardowych reguł sprawdzania poprawności identyfikator partii Azure.</span><span class="sxs-lookup"><span data-stu-id="373e0-203">This field specifies hello ID of your new application, which is subject toohello standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="373e0-204">dostępne są następujące reguły Hello zapewniające identyfikator aplikacji:</span><span class="sxs-lookup"><span data-stu-id="373e0-204">hello rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="373e0-205">W węzłach Windows hello identyfikator może zawierać dowolną kombinację znaków alfanumerycznych, łączniki i podkreślenia.</span><span class="sxs-lookup"><span data-stu-id="373e0-205">On Windows nodes, hello ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="373e0-206">W węzłach Linux są dozwolone tylko znaki alfanumeryczne oraz znaki podkreślenia.</span><span class="sxs-lookup"><span data-stu-id="373e0-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="373e0-207">Nie może zawierać więcej niż 64 znaki.</span><span class="sxs-lookup"><span data-stu-id="373e0-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="373e0-208">Musi być unikatowa w obrębie hello konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="373e0-208">Must be unique within hello Batch account.</span></span>
* <span data-ttu-id="373e0-209">Jest zachowywanie i bez uwzględniania wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="373e0-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="373e0-210">**Wersja**</span><span class="sxs-lookup"><span data-stu-id="373e0-210">**Version**</span></span>

<span data-ttu-id="373e0-211">To pole określa hello wersji pakietu aplikacji hello przekazywany.</span><span class="sxs-lookup"><span data-stu-id="373e0-211">This field specifies hello version of hello application package you are uploading.</span></span> <span data-ttu-id="373e0-212">Ciągi wersji są następujące reguły sprawdzania poprawności toohello podmiotu:</span><span class="sxs-lookup"><span data-stu-id="373e0-212">Version strings are subject toohello following validation rules:</span></span>

* <span data-ttu-id="373e0-213">W węzłach Windows hello ciąg wersji może zawierać dowolną kombinację znaków alfanumerycznych, łączniki, podkreślenia i kropki.</span><span class="sxs-lookup"><span data-stu-id="373e0-213">On Windows nodes, hello version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="373e0-214">W węzłach Linux hello ciąg wersji może zawierać tylko znaki alfanumeryczne oraz znaki podkreślenia.</span><span class="sxs-lookup"><span data-stu-id="373e0-214">On Linux nodes, hello version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="373e0-215">Nie może zawierać więcej niż 64 znaki.</span><span class="sxs-lookup"><span data-stu-id="373e0-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="373e0-216">Musi być unikatowa w obrębie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="373e0-216">Must be unique within hello application.</span></span>
* <span data-ttu-id="373e0-217">To zachowanie w przypadku i bez uwzględniania wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="373e0-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="373e0-218">**Pakiet aplikacji**</span><span class="sxs-lookup"><span data-stu-id="373e0-218">**Application package**</span></span>

<span data-ttu-id="373e0-219">To pole określa hello plik zip, który zawiera pliki binarne aplikacji hello i plików pomocniczych, które są wymagane tooexecute hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="373e0-219">This field specifies hello .zip file that contains hello application binaries and supporting files that are required tooexecute hello application.</span></span> <span data-ttu-id="373e0-220">Kliknij przycisk hello **wybierz plik** pola lub hello tooand toobrowse ikonę folderu, wybierz plik zip, który zawiera pliki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="373e0-220">Click hello **Select a file** box or hello folder icon toobrowse tooand select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="373e0-221">Po wybraniu pliku, kliknij przycisk **OK** toobegin hello przekazywania tooAzure magazynu.</span><span class="sxs-lookup"><span data-stu-id="373e0-221">After you've selected a file, click **OK** toobegin hello upload tooAzure Storage.</span></span> <span data-ttu-id="373e0-222">Po zakończeniu operacji wysyłania hello hello portal wyświetla powiadomienie i zamyka hello bloku.</span><span class="sxs-lookup"><span data-stu-id="373e0-222">When hello upload operation is complete, hello portal displays a notification and closes hello blade.</span></span> <span data-ttu-id="373e0-223">W zależności od wielkości hello pliku hello to przekazywanie i hello szybkość połączenia sieciowego ta operacja może potrwać pewien czas.</span><span class="sxs-lookup"><span data-stu-id="373e0-223">Depending on hello size of hello file that you are uploading and hello speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="373e0-224">Nie zamykaj hello **nowej aplikacji** bloku przed zakończeniem operacji wysyłania hello.</span><span class="sxs-lookup"><span data-stu-id="373e0-224">Do not close hello **New application** blade before hello upload operation is complete.</span></span> <span data-ttu-id="373e0-225">W ten sposób spowoduje zatrzymanie procesu przekazywania hello.</span><span class="sxs-lookup"><span data-stu-id="373e0-225">Doing so will stop hello upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="373e0-226">Dodaj nowy pakiet aplikacji</span><span class="sxs-lookup"><span data-stu-id="373e0-226">Add a new application package</span></span>
<span data-ttu-id="373e0-227">tooadd nowej wersji pakietu aplikacji dla istniejącej aplikacji, wybierz aplikację w hello **aplikacji** bloku, kliknij przycisk **pakiety**, następnie kliknij przycisk **Dodaj** tooopen Witaj **Dodaj pakiet** bloku.</span><span class="sxs-lookup"><span data-stu-id="373e0-227">tooadd a new application package version for an existing application, select an application in hello **Applications** blade, click **Packages**, then click **Add** tooopen hello **Add package** blade.</span></span>

<span data-ttu-id="373e0-228">![Dodawanie bloku pakietu aplikacji w portalu Azure][8]</span><span class="sxs-lookup"><span data-stu-id="373e0-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="373e0-229">Jak widać, pola hello pasują do właściwości hello **nowej aplikacji** bloku, ale hello **identyfikator aplikacji** pole jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="373e0-229">As you can see, hello fields match those of hello **New application** blade, but hello **Application id** box is disabled.</span></span> <span data-ttu-id="373e0-230">Tak samo jak dla nowej aplikacji hello, określ hello **wersji** nowego pakietu, Przeglądaj tooyour **pakiet aplikacji** zip pliku, a następnie kliknij przycisk **OK** tooupload hello pakiet.</span><span class="sxs-lookup"><span data-stu-id="373e0-230">As you did for hello new application, specify hello **Version** for your new package, browse tooyour **Application package** .zip file, then click **OK** tooupload hello package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="373e0-231">Aktualizowanie lub usuwanie pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="373e0-231">Update or delete an application package</span></span>
<span data-ttu-id="373e0-232">tooupdate lub usuń istniejący pakiet aplikacji, otwórz hello szczegóły blok dla aplikacji hello kliknij **pakiety** tooopen hello **pakiety** bloku, kliknij hello **wielokropka**w wierszu hello pakietu aplikacji hello mają toomodify i wybierz akcję hello, które mają tooperform.</span><span class="sxs-lookup"><span data-stu-id="373e0-232">tooupdate or delete an existing application package, open hello details blade for hello application, click **Packages** tooopen hello **Packages** blade, click hello **ellipsis** in hello row of hello application package that you want toomodify, and select hello action that you want tooperform.</span></span>

<span data-ttu-id="373e0-233">![Aktualizowanie lub usuwanie pakietu w portalu Azure][7]</span><span class="sxs-lookup"><span data-stu-id="373e0-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="373e0-234">**Aktualizacja**</span><span class="sxs-lookup"><span data-stu-id="373e0-234">**Update**</span></span>

<span data-ttu-id="373e0-235">Po kliknięciu **aktualizacji**, hello *pakiet aktualizacji* bloku jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="373e0-235">When you click **Update**, hello *Update package* blade is displayed.</span></span> <span data-ttu-id="373e0-236">Ten blok jest podobne toohello *nowy pakiet aplikacji* bloku, jednak tylko pola wyboru pakietów hello jest włączona, umożliwiając toospecify nowe tooupload pliku ZIP.</span><span class="sxs-lookup"><span data-stu-id="373e0-236">This blade is similar toohello *New application package* blade, however only hello package selection field is enabled, allowing you toospecify a new ZIP file tooupload.</span></span>

<span data-ttu-id="373e0-237">![Blok pakietu aktualizacji w portalu Azure][11]</span><span class="sxs-lookup"><span data-stu-id="373e0-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="373e0-238">**Usuwanie**</span><span class="sxs-lookup"><span data-stu-id="373e0-238">**Delete**</span></span>

<span data-ttu-id="373e0-239">Po kliknięciu **usunąć**, monit o usunięcie hello tooconfirm wersja pakietu hello i partii usuwa hello pakietu z magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="373e0-239">When you click **Delete**, you are asked tooconfirm hello deletion of hello package version, and Batch deletes hello package from Azure Storage.</span></span> <span data-ttu-id="373e0-240">Jeśli usuniesz hello domyślnej wersji aplikacji hello **wersja domyślna** ustawienie zostanie usunięte z aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="373e0-240">If you delete hello default version of an application, hello **Default version** setting is removed for hello application.</span></span>

<span data-ttu-id="373e0-241">![Usuwanie aplikacji][12]</span><span class="sxs-lookup"><span data-stu-id="373e0-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="373e0-242">Instalowanie aplikacji na węzły obliczeniowe</span><span class="sxs-lookup"><span data-stu-id="373e0-242">Install applications on compute nodes</span></span>
<span data-ttu-id="373e0-243">Teraz, kiedy znasz już jak aplikacji toomanage pakietów hello portalu Azure, można omówiono sposób toodeploy ich toocompute węzłów i uruchom je z zadań wsadowych.</span><span class="sxs-lookup"><span data-stu-id="373e0-243">Now that you've learned how toomanage application packages with hello Azure portal, we can discuss how toodeploy them toocompute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="373e0-244">Zainstaluj pakiety aplikacji w puli</span><span class="sxs-lookup"><span data-stu-id="373e0-244">Install pool application packages</span></span>
<span data-ttu-id="373e0-245">tooinstall pakietu aplikacji na wszystkich obliczeniowe węzłów w puli, należy określić co najmniej jeden pakiet aplikacji *odwołania* hello puli.</span><span class="sxs-lookup"><span data-stu-id="373e0-245">tooinstall an application package on all compute nodes in a pool, specify one or more application package *references* for hello pool.</span></span> <span data-ttu-id="373e0-246">pakiety aplikacji Hello określające dla puli są instalowane w każdym węźle obliczeń, w tym węźle dołącza hello puli oraz w przypadku węzła hello jest ponownego rozruchu lub odtworzenia z obrazu.</span><span class="sxs-lookup"><span data-stu-id="373e0-246">hello application packages that you specify for a pool are installed on each compute node when that node joins hello pool, and when hello node is rebooted or reimaged.</span></span>

<span data-ttu-id="373e0-247">W partiami platformy .NET, należy określić jedną lub więcej [CloudPool][net_cloudpool].[ ApplicationPackageReferences] [ net_cloudpool_pkgref] podczas tworzenia nowej puli lub dla istniejącej puli.</span><span class="sxs-lookup"><span data-stu-id="373e0-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="373e0-248">Witaj [ApplicationPackageReference] [ net_pkgref] klasa określa identyfikator aplikacji i wersji węzły obliczeniowe tooinstall w puli.</span><span class="sxs-lookup"><span data-stu-id="373e0-248">hello [ApplicationPackageReference][net_pkgref] class specifies an application ID and version tooinstall on a pool's compute nodes.</span></span>

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="373e0-249">Jeśli wdrożenie pakietu aplikacji nie powiedzie się z jakiegokolwiek powodu, znaczniki usługi partii hello hello węzła [bezużyteczne][net_nodestate], i zadania nie są zaplanowane do uruchomienia w tym węźle.</span><span class="sxs-lookup"><span data-stu-id="373e0-249">If an application package deployment fails for any reason, hello Batch service marks hello node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="373e0-250">W takim przypadku należy **ponowne uruchomienie** hello węzła tooreinitiate hello pakietu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="373e0-250">In this case, you should **restart** hello node tooreinitiate hello package deployment.</span></span> <span data-ttu-id="373e0-251">Ponownie uruchomić węzeł hello umożliwia również w węźle hello ponownie harmonogramy zadań.</span><span class="sxs-lookup"><span data-stu-id="373e0-251">Restarting hello node also enables task scheduling again on hello node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="373e0-252">Zainstaluj pakiety aplikacji zadań</span><span class="sxs-lookup"><span data-stu-id="373e0-252">Install task application packages</span></span>
<span data-ttu-id="373e0-253">Podobne tooa puli, określ pakiet aplikacji *odwołania* zadania.</span><span class="sxs-lookup"><span data-stu-id="373e0-253">Similar tooa pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="373e0-254">Gdy zadanie jest zaplanowane toorun w węźle, pakietów hello jest pobrane i wyodrębnione właśnie, przed wykonaniem zadań hello wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="373e0-254">When a task is scheduled toorun on a node, hello package is downloaded and extracted just before hello task's command line is executed.</span></span> <span data-ttu-id="373e0-255">Jeśli określonego pakietu i wersja jest już zainstalowany w węźle hello, hello pakietu nie jest pobierana, a istniejący pakiet hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="373e0-255">If a specified package and version is already installed on hello node, hello package is not downloaded and hello existing package is used.</span></span>

<span data-ttu-id="373e0-256">tooinstall pakiet aplikacji zadanie konfigurowania zadania hello [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] właściwości:</span><span class="sxs-lookup"><span data-stu-id="373e0-256">tooinstall a task application package, configure hello task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a><span data-ttu-id="373e0-257">Wykonywania aplikacji hello zainstalowany</span><span class="sxs-lookup"><span data-stu-id="373e0-257">Execute hello installed applications</span></span>
<span data-ttu-id="373e0-258">Hello pakietów określonych dla puli lub zadania zostaną pobrane i wyodrębnione tooa o nazwie katalogu w hello `AZ_BATCH_ROOT_DIR` hello węzła.</span><span class="sxs-lookup"><span data-stu-id="373e0-258">hello packages that you've specified for a pool or task are downloaded and extracted tooa named directory within hello `AZ_BATCH_ROOT_DIR` of hello node.</span></span> <span data-ttu-id="373e0-259">Partii tworzy również zmiennej środowiskowej, zawierający hello toohello ścieżki o nazwie katalogu.</span><span class="sxs-lookup"><span data-stu-id="373e0-259">Batch also creates an environment variable that contains hello path toohello named directory.</span></span> <span data-ttu-id="373e0-260">Podczas odwoływania się do aplikacji hello w węźle hello, wiersze poleceń z zadań używania tej zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="373e0-260">Your task command lines use this environment variable when referencing hello application on hello node.</span></span> 

<span data-ttu-id="373e0-261">W węzłach systemu Windows hello zmiennej znajduje się w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="373e0-261">On Windows nodes, hello variable is in hello following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="373e0-262">W węzłach Linux hello format jest nieco inne.</span><span class="sxs-lookup"><span data-stu-id="373e0-262">On Linux nodes, hello format is slightly different.</span></span> <span data-ttu-id="373e0-263">Kropki (.), łączniki (-) i znaki numeru (#) są spłaszczoną toounderscores w zmiennej środowiskowej hello.</span><span class="sxs-lookup"><span data-stu-id="373e0-263">Periods (.), hypens (-) and number signs (#) are flattened toounderscores in hello environment variable.</span></span> <span data-ttu-id="373e0-264">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="373e0-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="373e0-265">`APPLICATIONID`i `version` są wartości, które odpowiadają toohello aplikacji i wersję pakietu został określony dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="373e0-265">`APPLICATIONID` and `version` are values that correspond toohello application and package version you've specified for deployment.</span></span> <span data-ttu-id="373e0-266">Na przykład, jeśli określono tej wersji 2.7 aplikacji *mieszarce* należy zainstalować na węzłach systemu Windows, Twoje wierszy polecenia zadania użyje tego tooaccess zmiennej środowiskowej jej pliki:</span><span class="sxs-lookup"><span data-stu-id="373e0-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable tooaccess its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="373e0-267">W węzłach Linux Określ zmienną środowiskową hello w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="373e0-267">On Linux nodes, specify hello environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="373e0-268">Podczas przekazywania pakietu aplikacji, można określić węzły obliczeniowe tooyour toodeploy wersja domyślna.</span><span class="sxs-lookup"><span data-stu-id="373e0-268">When you upload an application package, you can specify a default version toodeploy tooyour compute nodes.</span></span> <span data-ttu-id="373e0-269">Jeśli wybrano domyślną wersję aplikacji hello wersji sufiks można pominąć w przypadku odwołania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="373e0-269">If you have specified a default version for an application, you can omit hello version suffix when you reference hello application.</span></span> <span data-ttu-id="373e0-270">Możesz określić hello domyślnej wersji aplikacji hello portalu Azure, w bloku aplikacji hello, jak pokazano w [przekazywanie aplikacji i zarządzanie nimi](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="373e0-270">You can specify hello default application version in hello Azure portal, on hello Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="373e0-271">Na przykład jeśli ustawisz "2.7" jako hello wersja domyślna dla aplikacji *mieszarce*i zadania odwołania hello następującej zmiennej środowiskowej, a następnie węzły Windows wykona wersji 2.7:</span><span class="sxs-lookup"><span data-stu-id="373e0-271">For example, if you set "2.7" as hello default version for application *blender*, and your tasks reference hello following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="373e0-272">Hello poniższy fragment kodu przedstawia przykład wiersza polecenia zadania uruchamiająca hello domyślnej wersji hello *mieszarce* aplikacji:</span><span class="sxs-lookup"><span data-stu-id="373e0-272">hello following code snippet shows an example task command line that launches hello default version of hello *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="373e0-273">Zobacz [ustawienia środowiska dla zadań](batch-api-basics.md#environment-settings-for-tasks) w hello [Przegląd funkcji partii](batch-api-basics.md) Aby uzyskać więcej informacji na temat ustawień środowiska węzła obliczeń.</span><span class="sxs-lookup"><span data-stu-id="373e0-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in hello [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="373e0-274">Aktualizowanie pakietów aplikacji puli</span><span class="sxs-lookup"><span data-stu-id="373e0-274">Update a pool's application packages</span></span>
<span data-ttu-id="373e0-275">Jeśli skonfigurowano już istniejącą pulę z pakietem aplikacji, można określić nowy pakiet dla hello puli.</span><span class="sxs-lookup"><span data-stu-id="373e0-275">If an existing pool has already been configured with an application package, you can specify a new package for hello pool.</span></span> <span data-ttu-id="373e0-276">Jeśli określisz nowe odwołanie pakietu dla puli, zastosuj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="373e0-276">If you specify a new package reference for a pool, hello following apply:</span></span>

* <span data-ttu-id="373e0-277">Witaj, usługa partia zadań instaluje hello nowo określonego pakietu na wszystkie nowe węzły, które Dołącz do puli hello i istniejący węzeł, który jest ponownego rozruchu lub odtworzenia z obrazu.</span><span class="sxs-lookup"><span data-stu-id="373e0-277">hello Batch service installs hello newly specified package on all new nodes that join hello pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="373e0-278">Węzły, które znajdują się już w puli hello podczas aktualizacji odwołania do pakietu hello nie są instalowane automatycznie nowy pakiet aplikacji hello obliczeń.</span><span class="sxs-lookup"><span data-stu-id="373e0-278">Compute nodes that are already in hello pool when you update hello package references do not automatically install hello new application package.</span></span> <span data-ttu-id="373e0-279">Obliczeniowe te węzły, należy ponownie uruchomić lub ponownie tooreceive hello nowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="373e0-279">These compute nodes must be rebooted or reimaged tooreceive hello new package.</span></span>
* <span data-ttu-id="373e0-280">Po wdrożeniu nowego pakietu hello utworzone zmiennych środowiskowych odzwierciedlają hello nowej aplikacji będzie odwoływał się pakiet.</span><span class="sxs-lookup"><span data-stu-id="373e0-280">When a new package is deployed, hello created environment variables reflect hello new application package references.</span></span>

<span data-ttu-id="373e0-281">W tym przykładzie hello istniejącej puli ma wersji 2.7 hello *mieszarce* aplikacji skonfigurowany jako jeden z jego [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref].</span><span class="sxs-lookup"><span data-stu-id="373e0-281">In this example, hello existing pool has version 2.7 of hello *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="373e0-282">węzły tooupdate hello puli z wersją 2.76b, określić nową [ApplicationPackageReference] [ net_pkgref] hello nowej wersji i zatwierdzania hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="373e0-282">tooupdate hello pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with hello new version, and commit hello change.</span></span>

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

<span data-ttu-id="373e0-283">Teraz, gdy hello nowa wersja została skonfigurowana, hello usługa partia zadań instaluje wersję 2.76b tooany *nowe* węzła, w której jest przyłączany hello puli.</span><span class="sxs-lookup"><span data-stu-id="373e0-283">Now that hello new version has been configured, hello Batch service installs version 2.76b tooany *new* node that joins hello pool.</span></span> <span data-ttu-id="373e0-284">tooinstall 2.76b na powitania węzłów, które są *już* w puli hello ponownego rozruchu lub je odtworzyć.</span><span class="sxs-lookup"><span data-stu-id="373e0-284">tooinstall 2.76b on hello nodes that are *already* in hello pool, reboot or reimage them.</span></span> <span data-ttu-id="373e0-285">Należy zwrócić uwagę zachowanie hello pliki z poprzedniego wdrożenia pakietu po ponownym rozruchu węzłów.</span><span class="sxs-lookup"><span data-stu-id="373e0-285">Note that rebooted nodes retain hello files from previous package deployments.</span></span>

## <a name="list-hello-applications-in-a-batch-account"></a><span data-ttu-id="373e0-286">Lista aplikacji hello w ramach konta usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="373e0-286">List hello applications in a Batch account</span></span>
<span data-ttu-id="373e0-287">Można wyświetlić listę aplikacji hello i ich pakietów w ramach konta usługi partia zadań, za pomocą hello [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] metody.</span><span class="sxs-lookup"><span data-stu-id="373e0-287">You can list hello applications and their packages in a Batch account by using hello [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a><span data-ttu-id="373e0-288">Dobiega końca</span><span class="sxs-lookup"><span data-stu-id="373e0-288">Wrap up</span></span>
<span data-ttu-id="373e0-289">Z pakietów aplikacji możesz pomóc klientom wybierz aplikacji hello dla swoich zadań i określ hello dokładnej wersji toouse podczas przetwarzania zadania z usługą przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="373e0-289">With application packages, you can help your customers select hello applications for their jobs and specify hello exact version toouse when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="373e0-290">Może także zapewnienia możliwości hello tooupload Twojego klientów i śledzenie własne aplikacje w usłudze.</span><span class="sxs-lookup"><span data-stu-id="373e0-290">You might also provide hello ability for your customers tooupload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="373e0-291">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="373e0-291">Next steps</span></span>
* <span data-ttu-id="373e0-292">Witaj [interfejsu API REST partii] [ api_rest] oferuje także funkcje obsługi toowork pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="373e0-292">hello [Batch REST API][api_rest] also provides support toowork with application packages.</span></span> <span data-ttu-id="373e0-293">Na przykład, zobacz hello [applicationPackageReferences] [ rest_add_pool_with_packages] element [Dodaj konto tooan puli] [ rest_add_pool] informacje na temat toospecify tooinstall pakietów przy użyciu hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="373e0-293">For example, see hello [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool tooan account][rest_add_pool] for information about how toospecify packages tooinstall by using hello REST API.</span></span> <span data-ttu-id="373e0-294">Zobacz [aplikacji] [ rest_applications] szczegółowe informacje o sposobie tooobtain informacje o aplikacji przy użyciu hello interfejsu API REST partii.</span><span class="sxs-lookup"><span data-stu-id="373e0-294">See [Applications][rest_applications] for details about how tooobtain application information by using hello Batch REST API.</span></span>
* <span data-ttu-id="373e0-295">Dowiedz się, jak tooprogrammatically [Zarządzanie kontami partii zadań Azure i przydziały zarządzania partiami platformy .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="373e0-295">Learn how tooprogrammatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="373e0-296">Witaj [zarządzania partiami platformy .NET][api_net_mgmt] biblioteki można włączyć funkcji Tworzenie i usuwanie konta wsadowego aplikacji lub usługi.</span><span class="sxs-lookup"><span data-stu-id="373e0-296">hello [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "Diagram ogólny pakietów aplikacji"
[2]: ./media/batch-application-packages/app_pkg_02.png "Kafelka aplikacji w portalu Azure"
[3]: ./media/batch-application-packages/app_pkg_03.png "Blok aplikacje w portalu Azure"
[4]: ./media/batch-application-packages/app_pkg_04.png "Blok szczegółów aplikacji w portalu Azure"
[5]: ./media/batch-application-packages/app_pkg_05.png "Nowy blok aplikacji w portalu Azure"
[7]: ./media/batch-application-packages/app_pkg_07.png "Aktualizowanie lub usuwanie pakietów listy rozwijanej w portalu Azure"
[8]: ./media/batch-application-packages/app_pkg_08.png "Nowy blok pakietu aplikacji w portalu Azure"
[9]: ./media/batch-application-packages/app_pkg_09.png "Alert nie połączonego konta magazynu"
[10]: ./media/batch-application-packages/app_pkg_10.png "Wybierz bloku konto magazynu w portalu Azure"
[11]: ./media/batch-application-packages/app_pkg_11.png "Blok pakietu aktualizacji w portalu Azure"
[12]: ./media/batch-application-packages/app_pkg_12.png "Usuń okno dialogowe potwierdzenia pakiet w portalu Azure"
