---
title: "Instalowanie pakietów aplikacji w węzłach obliczeniowych - partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Użyj funkcji pakiety aplikacji partii zadań Azure ułatwia zarządzanie wiele aplikacji i wersji do instalacji na partii węzły obliczeniowe."
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
ms.openlocfilehash: afcc04c80ec15872a22de5d5969a7ef6a583562f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-applications-to-compute-nodes-with-batch-application-packages"></a><span data-ttu-id="130eb-103">Wdrażanie aplikacji do wyliczenia węzłów za pomocą pakietów aplikacji partii</span><span class="sxs-lookup"><span data-stu-id="130eb-103">Deploy applications to compute nodes with Batch application packages</span></span>

<span data-ttu-id="130eb-104">Funkcja pakiety aplikacji partii zadań Azure umożliwia łatwe zarządzanie aplikacjami zadań i ich wdrożenia węzłów obliczeniowych w puli.</span><span class="sxs-lookup"><span data-stu-id="130eb-104">The application packages feature of Azure Batch provides easy management of task applications and their deployment to the compute nodes in your pool.</span></span> <span data-ttu-id="130eb-105">Pakiety aplikacji możesz przekazać i zarządzanie wieloma wersjami aplikacji, których uruchamianie zadań, łącznie z ich pliki pomocnicze.</span><span class="sxs-lookup"><span data-stu-id="130eb-105">With application packages, you can upload and manage multiple versions of the applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="130eb-106">Można następnie automatycznie wdrożyć co najmniej jeden z tych aplikacji, do węzłów obliczeniowych w puli.</span><span class="sxs-lookup"><span data-stu-id="130eb-106">You can then automatically deploy one or more of these applications to the compute nodes in your pool.</span></span>

<span data-ttu-id="130eb-107">W tym artykule dowiesz się, jak przekazywać oraz zarządzać nimi pakietów aplikacji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="130eb-107">In this article, you will learn how to upload and manage application packages in the Azure portal.</span></span> <span data-ttu-id="130eb-108">Następnie dowiesz się jak do zainstalowania go na węzłach obliczeń puli z [partiami platformy .NET] [ api_net] biblioteki.</span><span class="sxs-lookup"><span data-stu-id="130eb-108">You will then learn how to install them on a pool's compute nodes with the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="130eb-109">Pakiety aplikacji są obsługiwane we wszystkich pulach usługi Batch utworzonych po 5 lipca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="130eb-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="130eb-110">W pulach usługi Batch utworzonych między 10 marca 2016 r. a 5 lipca 2017 r. są one obsługiwane tylko w przypadku, gdy pula została utworzona za pomocą konfiguracji usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="130eb-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="130eb-111">Pule usługi Batch utworzone przed 10 marca 2016 r. nie obsługują pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-111">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="130eb-112">Interfejsy API umożliwiające tworzenie i zarządzanie pakietów aplikacji należą [zarządzania partiami platformy .NET] [[api_net_mgmt]] biblioteki.</span><span class="sxs-lookup"><span data-stu-id="130eb-112">The APIs for creating and managing application packages are part of the [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="130eb-113">Interfejsy API do instalowania pakietów aplikacji w węźle obliczeń są częścią [partiami platformy .NET] [ api_net] biblioteki.</span><span class="sxs-lookup"><span data-stu-id="130eb-113">The APIs for installing application packages on a compute node are part of the [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="130eb-114">Funkcja pakietów aplikacji, które są opisane w tym miejscu zastępuje funkcję partii aplikacje dostępne w poprzednich wersjach usługi.</span><span class="sxs-lookup"><span data-stu-id="130eb-114">The application packages feature described here supersedes the Batch Apps feature available in previous versions of the service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="130eb-115">Wymagania dotyczące pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="130eb-115">Application package requirements</span></span>
<span data-ttu-id="130eb-116">Aby użyć pakietów aplikacji, musisz [połączyć konto usługi Azure Storage](#link-a-storage-account) do konta partii zadań.</span><span class="sxs-lookup"><span data-stu-id="130eb-116">To use application packages, you need to [link an Azure Storage account](#link-a-storage-account) to your Batch account.</span></span>

<span data-ttu-id="130eb-117">Ta funkcja została wprowadzona w [interfejsu API REST partii] [ api_rest] wersji 2015-12-01.2.2 i odpowiadający mu [partiami platformy .NET] [ api_net] wersji biblioteki 3.1.0.</span><span class="sxs-lookup"><span data-stu-id="130eb-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and the corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="130eb-118">Firma Microsoft zaleca zawsze używać najnowszej wersji interfejsu API podczas pracy z partii.</span><span class="sxs-lookup"><span data-stu-id="130eb-118">We recommend that you always use the latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="130eb-119">Pakiety aplikacji są obsługiwane we wszystkich pulach usługi Batch utworzonych po 5 lipca 2017 r.</span><span class="sxs-lookup"><span data-stu-id="130eb-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="130eb-120">W pulach usługi Batch utworzonych między 10 marca 2016 r. a 5 lipca 2017 r. są one obsługiwane tylko w przypadku, gdy pula została utworzona za pomocą konfiguracji usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="130eb-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="130eb-121">Pule usługi Batch utworzone przed 10 marca 2016 r. nie obsługują pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-121">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="130eb-122">Aplikacje i pakiety aplikacji — informacje</span><span class="sxs-lookup"><span data-stu-id="130eb-122">About applications and application packages</span></span>
<span data-ttu-id="130eb-123">W partii zadań Azure *aplikacji* odwołuje się do zestawu określonej wersji plików binarnych, które mogą być automatycznie pobrane do węzłów obliczeniowych w puli.</span><span class="sxs-lookup"><span data-stu-id="130eb-123">Within Azure Batch, an *application* refers to a set of versioned binaries that can be automatically downloaded to the compute nodes in your pool.</span></span> <span data-ttu-id="130eb-124">*Pakiet aplikacji* odwołuje się do *określonego zestawu* tych danych binarnych i reprezentuje danego *wersji* aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-124">An *application package* refers to a *specific set* of those binaries and represents a given *version* of the application.</span></span>

<span data-ttu-id="130eb-125">![Diagramu wysokiego poziomu aplikacji i pakietów aplikacji][1]</span><span class="sxs-lookup"><span data-stu-id="130eb-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="130eb-126">Aplikacje</span><span class="sxs-lookup"><span data-stu-id="130eb-126">Applications</span></span>
<span data-ttu-id="130eb-127">Aplikacja w partii zawiera jeden lub więcej aplikacji, pakietów i opcje konfiguracji dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-127">An application in Batch contains one or more application packages and specifies configuration options for the application.</span></span> <span data-ttu-id="130eb-128">Na przykład aplikacji można określić domyślnej wersji pakietu aplikacji do zainstalowania na węzłów obliczeniowych oraz czy jej pakietów można zaktualizować lub usunąć.</span><span class="sxs-lookup"><span data-stu-id="130eb-128">For example, an application can specify the default application package version to install on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="130eb-129">Pakiety aplikacji</span><span class="sxs-lookup"><span data-stu-id="130eb-129">Application packages</span></span>
<span data-ttu-id="130eb-130">Pakiet aplikacji jest plik zip, który zawiera pliki binarne aplikacji i plików pomocniczych, które są wymagane dla zadań do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-130">An application package is a .zip file that contains the application binaries and supporting files that are required for your tasks to run the application.</span></span> <span data-ttu-id="130eb-131">Każdy pakiet aplikacji reprezentuje określoną wersję aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-131">Each application package represents a specific version of the application.</span></span>

<span data-ttu-id="130eb-132">Można określić pakietów aplikacji na poziomach puli i zadań.</span><span class="sxs-lookup"><span data-stu-id="130eb-132">You can specify application packages at the pool and task levels.</span></span> <span data-ttu-id="130eb-133">Podczas tworzenia puli lub zadania można określić co najmniej jeden z tych pakietów i (opcjonalnie) wersja.</span><span class="sxs-lookup"><span data-stu-id="130eb-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="130eb-134">**Pakiety aplikacji w puli** są wdrażane na *co* węzła w puli.</span><span class="sxs-lookup"><span data-stu-id="130eb-134">**Pool application packages** are deployed to *every* node in the pool.</span></span> <span data-ttu-id="130eb-135">Gdy węzeł dołącza pulę i gdy jest ponownego rozruchu lub odtworzenia z obrazu wdrożenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="130eb-136">Pakiety aplikacji w puli są odpowiednie, wszystkie węzły w puli wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="130eb-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="130eb-137">Podczas tworzenia puli, można dodać lub zaktualizować pakiety istniejącej puli, można określić co najmniej jednego pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="130eb-138">Aktualizuj istniejącą pulę aplikacji pakietów, należy ponownie uruchomić jego węzły do zainstalowania nowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="130eb-138">If you update an existing pool's application packages, you must restart its nodes to install the new package.</span></span>
* <span data-ttu-id="130eb-139">**Zadanie pakietów aplikacji** są wdrażane tylko w węźle obliczeń, zaplanowane zadanie, wystarczy, przed uruchomieniem zadania wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="130eb-139">**Task application packages** are deployed only to a compute node scheduled to run a task, just before running the task's command line.</span></span> <span data-ttu-id="130eb-140">Jeśli podany pakiet aplikacji i wersji jest już w węźle, nie jest wdrożone i jest używany istniejący pakiet.</span><span class="sxs-lookup"><span data-stu-id="130eb-140">If the specified application package and version is already on the node, it is not redeployed and the existing package is used.</span></span>
  
    <span data-ttu-id="130eb-141">Pakiety aplikacji zadań są przydatne w środowisku udostępnionych puli, której różne zadania są uruchamiane w jednej puli i puli nie zostanie usunięta po zakończeniu zadania.</span><span class="sxs-lookup"><span data-stu-id="130eb-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and the pool is not deleted when a job is completed.</span></span> <span data-ttu-id="130eb-142">Jeśli liczba zadań podrzędnych w zadaniu jest mniejsza niż liczba węzłów w puli, pakiety aplikacji zadania podrzędnego mogą minimalizować ilość transferowanych danych, ponieważ aplikacja jest wdrażana tylko dla węzłów, w których odbywa się uruchamianie zadań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="130eb-142">If your job has fewer tasks than nodes in the pool, task application packages can minimize data transfer since your application is deployed only to the nodes that run tasks.</span></span>
  
    <span data-ttu-id="130eb-143">Inne scenariusze, które mogą korzystać z zadań pakiety aplikacji są zadań uruchamianych dużej aplikacji, ale tylko kilka zadań.</span><span class="sxs-lookup"><span data-stu-id="130eb-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="130eb-144">Na przykład przetwarzania wstępnego etap lub zadanie scalania, gdzie aplikacja przetwarzanie wstępne lub merge jest ogromnych, może korzystać z zadań pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-144">For example, a pre-processing stage or a merge task, where the pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="130eb-145">Istnieją ograniczenia liczby aplikacji i pakietów aplikacji w ramach konta usługi partia zadań i aplikacji maksymalny rozmiar pakietu.</span><span class="sxs-lookup"><span data-stu-id="130eb-145">There are restrictions on the number of applications and application packages within a Batch account and on the maximum application package size.</span></span> <span data-ttu-id="130eb-146">Zobacz [przydziały i limity dla usługi partia zadań Azure](batch-quota-limit.md) szczegółowe informacje o tych ograniczeniach.</span><span class="sxs-lookup"><span data-stu-id="130eb-146">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="130eb-147">Korzyści wynikające z pakietów aplikacji</span><span class="sxs-lookup"><span data-stu-id="130eb-147">Benefits of application packages</span></span>
<span data-ttu-id="130eb-148">Pakiety aplikacji można uprościć kod w rozwiązaniu partii i zmniejszyć nakład pracy potrzebny do zarządzania aplikacjami, które uruchamiania zadań.</span><span class="sxs-lookup"><span data-stu-id="130eb-148">Application packages can simplify the code in your Batch solution and lower the overhead required to manage the applications that your tasks run.</span></span>

<span data-ttu-id="130eb-149">Z pakietów aplikacji zadanie uruchamiania przez pulę nie trzeba określać długą listę plików poszczególnych zasobów można zainstalować na węzłach.</span><span class="sxs-lookup"><span data-stu-id="130eb-149">With application packages, your pool's start task doesn't have to specify a long list of individual resource files to install on the nodes.</span></span> <span data-ttu-id="130eb-150">Nie trzeba ręcznie Zarządzanie wieloma wersjami plików aplikacji w usłudze Azure Storage lub na węzły.</span><span class="sxs-lookup"><span data-stu-id="130eb-150">You don't have to manually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="130eb-151">I nie trzeba martwić generowania [adresy URL SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) zapewniające dostęp do plików na Twoim koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="130eb-151">And, you don't need to worry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to provide access to the files in your Storage account.</span></span> <span data-ttu-id="130eb-152">Wsadowe działa w tle z usługą Azure Storage do przechowywania pakietów aplikacji i wdrożenia ich na węzłach obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="130eb-152">Batch works in the background with Azure Storage to store application packages and deploy them to compute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="130eb-153">Całkowity rozmiar zadania podrzędnego uruchamiania musi wynosić 32 768 znaków, w tym pliki zasobów lub zmienne środowiskowe, lub być mniejszy.</span><span class="sxs-lookup"><span data-stu-id="130eb-153">The total size of a start task must be less than or equal to 32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="130eb-154">Jeśli zadanie start przekracza ten limit, za pomocą pakietów aplikacji jest inną opcją.</span><span class="sxs-lookup"><span data-stu-id="130eb-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="130eb-155">Można również utworzyć archiwum zip zawierającym pliki zasobów, przekaż go jako obiekt blob do magazynu Azure i Rozpakuj go z poziomu wiersza polecenia zadania uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="130eb-155">You can also create a zipped archive containing your resource files, upload it as a blob to Azure Storage, and then unzip it from the command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="130eb-156">Przekazywanie aplikacji i zarządzanie nimi</span><span class="sxs-lookup"><span data-stu-id="130eb-156">Upload and manage applications</span></span>
<span data-ttu-id="130eb-157">Można użyć [portalu Azure] [ portal] lub [zarządzania partiami platformy .NET](batch-management-dotnet.md) biblioteki w zakresie zarządzania pakietami aplikacji w ramach konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="130eb-157">You can use the [Azure portal][portal] or the [Batch Management .NET](batch-management-dotnet.md) library to manage the application packages in your Batch account.</span></span> <span data-ttu-id="130eb-158">W kolejnych sekcjach kilka możemy najpierw pokazują, jak połączyć konto magazynu, a następnie omówiono Dodawanie aplikacji i pakietów i zarządzania nimi przy użyciu portalu.</span><span class="sxs-lookup"><span data-stu-id="130eb-158">In the next few sections, we first show how to link a Storage account, then discuss adding applications and packages and managing them with the portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="130eb-159">Połącz konto magazynu</span><span class="sxs-lookup"><span data-stu-id="130eb-159">Link a Storage account</span></span>
<span data-ttu-id="130eb-160">Aby użyć pakietów aplikacji, możesz połączyć konto magazynu Azure do konta partii zadań.</span><span class="sxs-lookup"><span data-stu-id="130eb-160">To use application packages, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="130eb-161">Jeśli nie skonfigurowano jeszcze konta magazynu, portalu Azure wyświetli ostrzeżenie, po raz pierwszy kliknij **aplikacji** kafelka w **konto wsadowe** bloku.</span><span class="sxs-lookup"><span data-stu-id="130eb-161">If you have not yet configured a Storage account, the Azure portal displays a warning the first time you click the **Applications** tile in the **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="130eb-162">Obecnie partii obsługuje *tylko* **ogólnego przeznaczenia** typu konta magazynu, zgodnie z opisem w kroku 5, [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account)w [o Azure konta magazynu](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="130eb-162">Batch currently supports *only* the **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="130eb-163">Łącząc konta usługi Azure Storage do konta partii zadań, należy połączyć *tylko* **ogólnego przeznaczenia** konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="130eb-163">When you link an Azure Storage account to your Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="130eb-164">![Ostrzeżenie "Nie skonfigurowano konta magazynu" w portalu Azure][9]</span><span class="sxs-lookup"><span data-stu-id="130eb-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="130eb-165">Usługa partia zadań używa skojarzone konto magazynu do przechowywania pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-165">The Batch service uses the associated Storage account to store your application packages.</span></span> <span data-ttu-id="130eb-166">Po połączeniu dwóch kont usługi partia zadań można automatycznie wdrażać pakietów przechowywanych w ramach połączonego konta magazynu do węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="130eb-166">After you've linked the two accounts, Batch can automatically deploy the packages stored in the linked Storage account to your compute nodes.</span></span> <span data-ttu-id="130eb-167">Aby połączyć konto magazynu do konta partii zadań, kliknij **ustawienia konta magazynu** na **ostrzeżenie** bloku, a następnie kliknij przycisk **konta magazynu** na  **Konto magazynu** bloku.</span><span class="sxs-lookup"><span data-stu-id="130eb-167">To link a Storage account to your Batch account, click **Storage account settings** on the **Warning** blade, and then click **Storage Account** on the **Storage Account** blade.</span></span>

<span data-ttu-id="130eb-168">![Wybierz bloku konto magazynu w portalu Azure][10]</span><span class="sxs-lookup"><span data-stu-id="130eb-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="130eb-169">Zaleca się utworzenie konta magazynu *w szczególności* do użytku z kontem usługi partia zadań i zaznacz je tutaj.</span><span class="sxs-lookup"><span data-stu-id="130eb-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="130eb-170">Aby uzyskać więcej informacji o sposobie tworzenia konta magazynu, zobacz "Tworzenie konta magazynu" w [konta usługi Azure Storage](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="130eb-170">For details about how to create a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="130eb-171">Po utworzeniu konta magazynu można następnie połączyć go do konta partii zadań za pomocą **konta magazynu** bloku.</span><span class="sxs-lookup"><span data-stu-id="130eb-171">After you've created a Storage account, you can then link it to your Batch account by using the **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="130eb-172">Usługa partia zadań używa usługi Azure Storage do przechowywania pakietów aplikacji jako blokowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="130eb-172">The Batch service uses Azure Storage to store your application packages as block blobs.</span></span> <span data-ttu-id="130eb-173">Jesteś [rozliczany jako normalne] [ storage_pricing] dla bloku danych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="130eb-173">You are [charged as normal][storage_pricing] for the block blob data.</span></span> <span data-ttu-id="130eb-174">Należy wziąć pod uwagę rozmiar i liczbę pakietów aplikacji, a okresowe usuwanie przestarzałych pakietów, aby zminimalizować koszty.</span><span class="sxs-lookup"><span data-stu-id="130eb-174">Be sure to consider the size and number of your application packages, and periodically remove deprecated packages to minimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="130eb-175">Wyświetl bieżące aplikacje</span><span class="sxs-lookup"><span data-stu-id="130eb-175">View current applications</span></span>
<span data-ttu-id="130eb-176">Aby wyświetlić aplikacje w ramach konta usługi partia zadań, kliknij przycisk **aplikacji** elementu menu w menu po lewej stronie podczas przeglądania **konto wsadowe** bloku.</span><span class="sxs-lookup"><span data-stu-id="130eb-176">To view the applications in your Batch account, click the **Applications** menu item in the left menu while viewing the **Batch account** blade.</span></span>

<span data-ttu-id="130eb-177">![Kafelek aplikacji][2]</span><span class="sxs-lookup"><span data-stu-id="130eb-177">![Applications tile][2]</span></span>

<span data-ttu-id="130eb-178">Wybranie tej opcji menu otwiera **aplikacji** bloku:</span><span class="sxs-lookup"><span data-stu-id="130eb-178">Selecting this menu option opens the **Applications** blade:</span></span>

<span data-ttu-id="130eb-179">![Lista aplikacji][3]</span><span class="sxs-lookup"><span data-stu-id="130eb-179">![List applications][3]</span></span>

<span data-ttu-id="130eb-180">**Aplikacji** bloku Wyświetla identyfikator każdej aplikacji w Twoje konto oraz następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="130eb-180">The **Applications** blade displays the ID of each application in your account and the following properties:</span></span>

* <span data-ttu-id="130eb-181">**Pakiety**: numer wersji skojarzonych z tą aplikacją.</span><span class="sxs-lookup"><span data-stu-id="130eb-181">**Packages**: The number of versions associated with this application.</span></span>
* <span data-ttu-id="130eb-182">**Wersja domyślna**: wersja aplikacji zainstalowane, jeśli nie wskazują wersji po określeniu dla puli aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-182">**Default version**: The application version installed if you do not indicate a version when you specify the application for a pool.</span></span> <span data-ttu-id="130eb-183">To ustawienie jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="130eb-183">This setting is optional.</span></span>
* <span data-ttu-id="130eb-184">**Zezwalaj na aktualizacje**: wartość, która określa, czy pakiet aktualizacji, usuwanie i dodatki są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="130eb-184">**Allow updates**: The value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="130eb-185">Jeśli ta wartość jest równa **nr**, pakiet aktualizacji i usunięć są wyłączone dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-185">If this is set to **No**, package updates and deletions are disabled for the application.</span></span> <span data-ttu-id="130eb-186">Można dodawać tylko nowe wersje pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-186">Only new application package versions can be added.</span></span> <span data-ttu-id="130eb-187">Wartość domyślna to **tak**.</span><span class="sxs-lookup"><span data-stu-id="130eb-187">The default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="130eb-188">Wyświetlanie szczegółów aplikacji</span><span class="sxs-lookup"><span data-stu-id="130eb-188">View application details</span></span>
<span data-ttu-id="130eb-189">Aby otworzyć blok, który zawiera szczegóły aplikacji, wybierz aplikację w **aplikacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="130eb-189">To open the blade that includes the details for an application, select the application in the **Applications** blade.</span></span>

<span data-ttu-id="130eb-190">![Szczegóły aplikacji][4]</span><span class="sxs-lookup"><span data-stu-id="130eb-190">![Application details][4]</span></span>

<span data-ttu-id="130eb-191">W bloku szczegóły aplikacji można skonfigurować następujące ustawienia dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-191">In the application details blade, you can configure the following settings for your application.</span></span>

* <span data-ttu-id="130eb-192">**Zezwalaj na aktualizacje**: Określ, czy można zaktualizować lub usunąć jego pakietów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="130eb-193">Zobacz "Aktualizowanie lub usuwanie pakietu aplikacji" w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="130eb-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="130eb-194">**Wersja domyślna**: Określ pakiet aplikacji domyślnej, aby wdrożyć węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="130eb-194">**Default version**: Specify a default application package to deploy to compute nodes.</span></span>
* <span data-ttu-id="130eb-195">**Nazwa wyświetlana**: Określ przyjazną nazwę, która rozwiązania partii można użyć, gdy jest on Wyświetla informacje o aplikacji, na przykład w Interfejsie użytkownika usługi, które zapewniają klientom za pośrednictwem usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="130eb-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about the application, for example, in the UI of a service that you provide to your customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="130eb-196">Dodaj nową aplikację</span><span class="sxs-lookup"><span data-stu-id="130eb-196">Add a new application</span></span>
<span data-ttu-id="130eb-197">Aby utworzyć nową aplikację, należy dodać pakiet aplikacji i określ aplikacji nowy, unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="130eb-197">To create a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="130eb-198">Pierwszy pakiet aplikacji, który możesz dodać nowy identyfikator aplikacji tworzy nową aplikację.</span><span class="sxs-lookup"><span data-stu-id="130eb-198">The first application package that you add with the new application ID also creates the new application.</span></span>

<span data-ttu-id="130eb-199">Kliknij przycisk **Dodaj** na **aplikacji** bloku, aby otworzyć **nowej aplikacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="130eb-199">Click **Add** on the **Applications** blade to open the **New application** blade.</span></span>

<span data-ttu-id="130eb-200">![Nowy blok aplikacji w portalu Azure][5]</span><span class="sxs-lookup"><span data-stu-id="130eb-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="130eb-201">**Nowej aplikacji** blok zawiera następujące pola, aby określić ustawienia nowej aplikacji i pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-201">The **New application** blade provides the following fields to specify the settings of your new application and application package.</span></span>

<span data-ttu-id="130eb-202">**Identyfikator aplikacji**</span><span class="sxs-lookup"><span data-stu-id="130eb-202">**Application id**</span></span>

<span data-ttu-id="130eb-203">To pole określa identyfikator nowej aplikacji, która podlega standardowych reguł sprawdzania poprawności identyfikator partii Azure.</span><span class="sxs-lookup"><span data-stu-id="130eb-203">This field specifies the ID of your new application, which is subject to the standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="130eb-204">Dostępne są następujące reguły zapewniające identyfikator aplikacji:</span><span class="sxs-lookup"><span data-stu-id="130eb-204">The rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="130eb-205">W węzłach Windows identyfikator może zawierać dowolną kombinację znaków alfanumerycznych, łączniki i podkreślenia.</span><span class="sxs-lookup"><span data-stu-id="130eb-205">On Windows nodes, the ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="130eb-206">W węzłach Linux są dozwolone tylko znaki alfanumeryczne oraz znaki podkreślenia.</span><span class="sxs-lookup"><span data-stu-id="130eb-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="130eb-207">Nie może zawierać więcej niż 64 znaki.</span><span class="sxs-lookup"><span data-stu-id="130eb-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="130eb-208">Musi być unikatowa w ramach konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="130eb-208">Must be unique within the Batch account.</span></span>
* <span data-ttu-id="130eb-209">Jest zachowywanie i bez uwzględniania wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="130eb-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="130eb-210">**Wersja**</span><span class="sxs-lookup"><span data-stu-id="130eb-210">**Version**</span></span>

<span data-ttu-id="130eb-211">To pole określa wersję pakietu aplikacji, które przekazujesz.</span><span class="sxs-lookup"><span data-stu-id="130eb-211">This field specifies the version of the application package you are uploading.</span></span> <span data-ttu-id="130eb-212">Ciągi wersji obowiązują następujące reguły sprawdzania poprawności:</span><span class="sxs-lookup"><span data-stu-id="130eb-212">Version strings are subject to the following validation rules:</span></span>

* <span data-ttu-id="130eb-213">W węzłach Windows ciąg wersji może zawierać dowolną kombinację znaków alfanumerycznych, łączniki, podkreślenia i kropki.</span><span class="sxs-lookup"><span data-stu-id="130eb-213">On Windows nodes, the version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="130eb-214">W węzłach Linux ciąg wersji może zawierać tylko znaki alfanumeryczne oraz znaki podkreślenia.</span><span class="sxs-lookup"><span data-stu-id="130eb-214">On Linux nodes, the version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="130eb-215">Nie może zawierać więcej niż 64 znaki.</span><span class="sxs-lookup"><span data-stu-id="130eb-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="130eb-216">Musi być unikatowa w ramach aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-216">Must be unique within the application.</span></span>
* <span data-ttu-id="130eb-217">To zachowanie w przypadku i bez uwzględniania wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="130eb-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="130eb-218">**Pakiet aplikacji**</span><span class="sxs-lookup"><span data-stu-id="130eb-218">**Application package**</span></span>

<span data-ttu-id="130eb-219">To pole określa plik zip, który zawiera pliki binarne aplikacji i plików pomocniczych, które są wymagane do wykonania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-219">This field specifies the .zip file that contains the application binaries and supporting files that are required to execute the application.</span></span> <span data-ttu-id="130eb-220">Kliknij przycisk **wybierz plik** pola lub ikonę folderu Wyszukaj i wybierz plik zip, który zawiera pliki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-220">Click the **Select a file** box or the folder icon to browse to and select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="130eb-221">Po wybraniu pliku, kliknij przycisk **OK** można rozpocząć przekazywania do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="130eb-221">After you've selected a file, click **OK** to begin the upload to Azure Storage.</span></span> <span data-ttu-id="130eb-222">Po zakończeniu operacji wysyłania portal wyświetla powiadomienie i zamyka bloku.</span><span class="sxs-lookup"><span data-stu-id="130eb-222">When the upload operation is complete, the portal displays a notification and closes the blade.</span></span> <span data-ttu-id="130eb-223">W zależności od rozmiaru pliku, czy przekazujesz i szybkość połączenia sieciowego ta operacja może potrwać pewien czas.</span><span class="sxs-lookup"><span data-stu-id="130eb-223">Depending on the size of the file that you are uploading and the speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="130eb-224">Nie zamykaj **nowej aplikacji** bloku przed zakończeniem operacji przesyłania.</span><span class="sxs-lookup"><span data-stu-id="130eb-224">Do not close the **New application** blade before the upload operation is complete.</span></span> <span data-ttu-id="130eb-225">W ten sposób zostanie zatrzymany procesu przekazywania.</span><span class="sxs-lookup"><span data-stu-id="130eb-225">Doing so will stop the upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="130eb-226">Dodaj nowy pakiet aplikacji</span><span class="sxs-lookup"><span data-stu-id="130eb-226">Add a new application package</span></span>
<span data-ttu-id="130eb-227">Aby dodać nową wersję pakietu aplikacji dla istniejącej aplikacji, wybierz aplikację w **aplikacji** bloku, kliknij przycisk **pakiety**, następnie kliknij przycisk **Dodaj** otworzyć **Dodaj pakiet** bloku.</span><span class="sxs-lookup"><span data-stu-id="130eb-227">To add a new application package version for an existing application, select an application in the **Applications** blade, click **Packages**, then click **Add** to open the **Add package** blade.</span></span>

<span data-ttu-id="130eb-228">![Dodawanie bloku pakietu aplikacji w portalu Azure][8]</span><span class="sxs-lookup"><span data-stu-id="130eb-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="130eb-229">Jak widać, pól zgodnie z regułami **nowej aplikacji** bloku, ale **identyfikator aplikacji** pole jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="130eb-229">As you can see, the fields match those of the **New application** blade, but the **Application id** box is disabled.</span></span> <span data-ttu-id="130eb-230">Tak samo jak dla nowej aplikacji, określ **wersji** nowego pakietu, przejdź do Twojej **pakiet aplikacji** zip pliku, a następnie kliknij przycisk **OK** do przekazania pakietu.</span><span class="sxs-lookup"><span data-stu-id="130eb-230">As you did for the new application, specify the **Version** for your new package, browse to your **Application package** .zip file, then click **OK** to upload the package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="130eb-231">Aktualizowanie lub usuwanie pakietu aplikacji</span><span class="sxs-lookup"><span data-stu-id="130eb-231">Update or delete an application package</span></span>
<span data-ttu-id="130eb-232">Aby zaktualizować lub usunąć istniejący pakiet aplikacji, Otwórz szczegóły blok dla aplikacji, kliknij przycisk **pakiety** otworzyć **pakiety** bloku, kliknij przycisk **wielokropka** w wiersz pakietu aplikacji, który chcesz zmodyfikować, a następnie wybierz akcję, którą chcesz wykonać.</span><span class="sxs-lookup"><span data-stu-id="130eb-232">To update or delete an existing application package, open the details blade for the application, click **Packages** to open the **Packages** blade, click the **ellipsis** in the row of the application package that you want to modify, and select the action that you want to perform.</span></span>

<span data-ttu-id="130eb-233">![Aktualizowanie lub usuwanie pakietu w portalu Azure][7]</span><span class="sxs-lookup"><span data-stu-id="130eb-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="130eb-234">**Aktualizacja**</span><span class="sxs-lookup"><span data-stu-id="130eb-234">**Update**</span></span>

<span data-ttu-id="130eb-235">Po kliknięciu **aktualizacji**, *pakiet aktualizacji* bloku jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="130eb-235">When you click **Update**, the *Update package* blade is displayed.</span></span> <span data-ttu-id="130eb-236">Ten blok jest podobny do *nowy pakiet aplikacji* bloku, jednak tylko pole wyboru pakietu jest włączona, co pozwoli określić nowy plik ZIP i przekazać.</span><span class="sxs-lookup"><span data-stu-id="130eb-236">This blade is similar to the *New application package* blade, however only the package selection field is enabled, allowing you to specify a new ZIP file to upload.</span></span>

<span data-ttu-id="130eb-237">![Blok pakietu aktualizacji w portalu Azure][11]</span><span class="sxs-lookup"><span data-stu-id="130eb-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="130eb-238">**Usuwanie**</span><span class="sxs-lookup"><span data-stu-id="130eb-238">**Delete**</span></span>

<span data-ttu-id="130eb-239">Po kliknięciu **usunąć**, zostanie wyświetlona prośba o potwierdzenie usunięcia wersji pakietu i partii usuwa pakiet z usługi Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="130eb-239">When you click **Delete**, you are asked to confirm the deletion of the package version, and Batch deletes the package from Azure Storage.</span></span> <span data-ttu-id="130eb-240">Jeśli usuniesz domyślnej wersji aplikacji, **wersja domyślna** ustawienie zostanie usunięte z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-240">If you delete the default version of an application, the **Default version** setting is removed for the application.</span></span>

<span data-ttu-id="130eb-241">![Usuwanie aplikacji][12]</span><span class="sxs-lookup"><span data-stu-id="130eb-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="130eb-242">Instalowanie aplikacji na węzły obliczeniowe</span><span class="sxs-lookup"><span data-stu-id="130eb-242">Install applications on compute nodes</span></span>
<span data-ttu-id="130eb-243">Teraz, kiedy znasz już jak zarządzać pakietami aplikacji z portalu Azure, można omówiono sposób wdrożenia ich na węzłach obliczeniowych i uruchom je z zadań wsadowych.</span><span class="sxs-lookup"><span data-stu-id="130eb-243">Now that you've learned how to manage application packages with the Azure portal, we can discuss how to deploy them to compute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="130eb-244">Zainstaluj pakiety aplikacji w puli</span><span class="sxs-lookup"><span data-stu-id="130eb-244">Install pool application packages</span></span>
<span data-ttu-id="130eb-245">Aby zainstalować pakiet aplikacji we wszystkich węzłach obliczeń w puli, należy określić co najmniej jeden pakiet aplikacji *odwołania* puli.</span><span class="sxs-lookup"><span data-stu-id="130eb-245">To install an application package on all compute nodes in a pool, specify one or more application package *references* for the pool.</span></span> <span data-ttu-id="130eb-246">Pakiety aplikacji, które określają dla puli są instalowane w każdym węźle obliczeń, w tym węźle sprzężenia puli oraz w przypadku węzła jest ponownego rozruchu lub odtworzenia z obrazu.</span><span class="sxs-lookup"><span data-stu-id="130eb-246">The application packages that you specify for a pool are installed on each compute node when that node joins the pool, and when the node is rebooted or reimaged.</span></span>

<span data-ttu-id="130eb-247">W partiami platformy .NET, należy określić jedną lub więcej [CloudPool][net_cloudpool].[ ApplicationPackageReferences] [ net_cloudpool_pkgref] podczas tworzenia nowej puli lub dla istniejącej puli.</span><span class="sxs-lookup"><span data-stu-id="130eb-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="130eb-248">[ApplicationPackageReference] [ net_pkgref] klasa określa węzły obliczeniowe identyfikator i wersję aplikacji do zainstalowania w puli.</span><span class="sxs-lookup"><span data-stu-id="130eb-248">The [ApplicationPackageReference][net_pkgref] class specifies an application ID and version to install on a pool's compute nodes.</span></span>

```csharp
// Create the unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify the application and version to install on the compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit the pool so that it's created in the Batch service. As the nodes join
// the pool, the specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="130eb-249">Jeśli wdrożenie pakietu aplikacji nie powiedzie się z jakiegokolwiek powodu, usługa partia zadań oznacza węzeł [bezużyteczne][net_nodestate], i zadania nie są zaplanowane do uruchomienia w tym węźle.</span><span class="sxs-lookup"><span data-stu-id="130eb-249">If an application package deployment fails for any reason, the Batch service marks the node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="130eb-250">W takim przypadku należy **ponowne uruchomienie** węzeł, aby ponownie zainicjować wdrożenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="130eb-250">In this case, you should **restart** the node to reinitiate the package deployment.</span></span> <span data-ttu-id="130eb-251">Ponowne uruchomienie węzła umożliwia również w węźle ponownie harmonogramy zadań.</span><span class="sxs-lookup"><span data-stu-id="130eb-251">Restarting the node also enables task scheduling again on the node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="130eb-252">Zainstaluj pakiety aplikacji zadań</span><span class="sxs-lookup"><span data-stu-id="130eb-252">Install task application packages</span></span>
<span data-ttu-id="130eb-253">Podobnie do puli, należy określić pakiet aplikacji *odwołania* zadania.</span><span class="sxs-lookup"><span data-stu-id="130eb-253">Similar to a pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="130eb-254">Gdy zadanie jest zaplanowane do uruchomienia w węźle, pakiet jest pobrane i wyodrębnione tuż przed wykonaniem zadania wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="130eb-254">When a task is scheduled to run on a node, the package is downloaded and extracted just before the task's command line is executed.</span></span> <span data-ttu-id="130eb-255">Jeśli określonego pakietu i wersja jest już zainstalowany w węźle, pakiet nie jest pobierana i jest używany istniejący pakiet.</span><span class="sxs-lookup"><span data-stu-id="130eb-255">If a specified package and version is already installed on the node, the package is not downloaded and the existing package is used.</span></span>

<span data-ttu-id="130eb-256">Aby zainstalować pakiet aplikacji zadań, należy skonfigurować zadania [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] właściwości:</span><span class="sxs-lookup"><span data-stu-id="130eb-256">To install a task application package, configure the task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

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

## <a name="execute-the-installed-applications"></a><span data-ttu-id="130eb-257">Wykonanie zainstalowanych aplikacji</span><span class="sxs-lookup"><span data-stu-id="130eb-257">Execute the installed applications</span></span>
<span data-ttu-id="130eb-258">Pakiety, które zostały określone dla puli lub zadania są pobrane i wyodrębnione do katalogu o nazwie w `AZ_BATCH_ROOT_DIR` węzła.</span><span class="sxs-lookup"><span data-stu-id="130eb-258">The packages that you've specified for a pool or task are downloaded and extracted to a named directory within the `AZ_BATCH_ROOT_DIR` of the node.</span></span> <span data-ttu-id="130eb-259">Partii tworzy również zmienną środowiskową, który zawiera ścieżkę do katalogu o nazwie.</span><span class="sxs-lookup"><span data-stu-id="130eb-259">Batch also creates an environment variable that contains the path to the named directory.</span></span> <span data-ttu-id="130eb-260">Wiersze poleceń z zadań Użyj tej zmiennej środowiskowej podczas odwoływania się do aplikacji w węźle.</span><span class="sxs-lookup"><span data-stu-id="130eb-260">Your task command lines use this environment variable when referencing the application on the node.</span></span> 

<span data-ttu-id="130eb-261">W węzłach Windows zmienna jest w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="130eb-261">On Windows nodes, the variable is in the following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="130eb-262">W węzłach Linux format różni się nieznacznie.</span><span class="sxs-lookup"><span data-stu-id="130eb-262">On Linux nodes, the format is slightly different.</span></span> <span data-ttu-id="130eb-263">Kropki (.), łączniki (-) i znaki numeru (#) są jako spłaszczone podkreślenia w zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="130eb-263">Periods (.), hypens (-) and number signs (#) are flattened to underscores in the environment variable.</span></span> <span data-ttu-id="130eb-264">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="130eb-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="130eb-265">`APPLICATIONID`i `version` to wartości, które odpowiadają wersji aplikacji i pakietów zostały określone dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="130eb-265">`APPLICATIONID` and `version` are values that correspond to the application and package version you've specified for deployment.</span></span> <span data-ttu-id="130eb-266">Na przykład, jeśli określono tej wersji 2.7 aplikacji *mieszarce* należy zainstalować na węzłach systemu Windows, Twoje wiersze polecenia zadań użyje tej zmiennej środowiskowej dostęp do swoich plików:</span><span class="sxs-lookup"><span data-stu-id="130eb-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable to access its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="130eb-267">W węzłach Linux Określ zmienną środowiskową w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="130eb-267">On Linux nodes, specify the environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="130eb-268">Podczas przekazywania pakietu aplikacji, można określić domyślnej wersji do wdrożenia węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="130eb-268">When you upload an application package, you can specify a default version to deploy to your compute nodes.</span></span> <span data-ttu-id="130eb-269">Jeśli określono domyślnej wersji aplikacji, sufiks wersji można pominąć w przypadku odwołania do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-269">If you have specified a default version for an application, you can omit the version suffix when you reference the application.</span></span> <span data-ttu-id="130eb-270">Można określić domyślnej wersji aplikacji w portalu Azure, w bloku aplikacji, jak pokazano w [przekazywanie aplikacji i zarządzanie nimi](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="130eb-270">You can specify the default application version in the Azure portal, on the Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="130eb-271">Na przykład jeśli ustawisz "2.7", jako wersja domyślna dla aplikacji *mieszarce*i zadania odwołują się następujące zmiennej środowiskowej, a następnie węzły Windows wykona wersji 2.7:</span><span class="sxs-lookup"><span data-stu-id="130eb-271">For example, if you set "2.7" as the default version for application *blender*, and your tasks reference the following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="130eb-272">Poniższy fragment kodu przedstawia przykład wiersz polecenia zadania, który uruchamia domyślnej wersji *mieszarce* aplikacji:</span><span class="sxs-lookup"><span data-stu-id="130eb-272">The following code snippet shows an example task command line that launches the default version of the *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="130eb-273">Zobacz [ustawienia środowiska dla zadań](batch-api-basics.md#environment-settings-for-tasks) w [Przegląd funkcji partii](batch-api-basics.md) Aby uzyskać więcej informacji na temat ustawień środowiska węzła obliczeń.</span><span class="sxs-lookup"><span data-stu-id="130eb-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in the [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="130eb-274">Aktualizowanie pakietów aplikacji puli</span><span class="sxs-lookup"><span data-stu-id="130eb-274">Update a pool's application packages</span></span>
<span data-ttu-id="130eb-275">Jeśli skonfigurowano już istniejącą pulę z pakietem aplikacji, można określić nowy pakiet dla tej puli.</span><span class="sxs-lookup"><span data-stu-id="130eb-275">If an existing pool has already been configured with an application package, you can specify a new package for the pool.</span></span> <span data-ttu-id="130eb-276">Jeśli określisz nowe odwołanie pakietu dla puli, następujących warunków:</span><span class="sxs-lookup"><span data-stu-id="130eb-276">If you specify a new package reference for a pool, the following apply:</span></span>

* <span data-ttu-id="130eb-277">Usługa partia zadań instaluje nowo określonego pakietu na wszystkie nowe węzły, które Dołącz do puli oraz na istniejący węzeł, który jest ponownego rozruchu lub odtworzenia z obrazu.</span><span class="sxs-lookup"><span data-stu-id="130eb-277">The Batch service installs the newly specified package on all new nodes that join the pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="130eb-278">Obliczeń węzłów, które są już w puli, gdy aktualizacja odwołania do pakietu nie są instalowane automatycznie nowy pakiet aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-278">Compute nodes that are already in the pool when you update the package references do not automatically install the new application package.</span></span> <span data-ttu-id="130eb-279">Obliczeniowe te węzły muszą być ponowny rozruch lub odtworzyć z obrazu do odbierania nowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="130eb-279">These compute nodes must be rebooted or reimaged to receive the new package.</span></span>
* <span data-ttu-id="130eb-280">Po wdrożeniu nowego pakietu, zmienne środowiskowe utworzony odzwierciedlają nowego odwołania do pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-280">When a new package is deployed, the created environment variables reflect the new application package references.</span></span>

<span data-ttu-id="130eb-281">W tym przykładzie istniejącej puli ma wersji 2.7 *mieszarce* aplikacji skonfigurowany jako jeden z jego [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref].</span><span class="sxs-lookup"><span data-stu-id="130eb-281">In this example, the existing pool has version 2.7 of the *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="130eb-282">Aby zaktualizować węzłów w puli z wersją 2.76b, określić nową [ApplicationPackageReference] [ net_pkgref] z nową wersję oraz zatwierdzić zmiany.</span><span class="sxs-lookup"><span data-stu-id="130eb-282">To update the pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with the new version, and commit the change.</span></span>

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

<span data-ttu-id="130eb-283">Teraz, nowa wersja została skonfigurowana, usługa partia zadań powoduje zainstalowanie wersji 2.76b do dowolnego *nowe* węzła, w której jest przyłączany puli.</span><span class="sxs-lookup"><span data-stu-id="130eb-283">Now that the new version has been configured, the Batch service installs version 2.76b to any *new* node that joins the pool.</span></span> <span data-ttu-id="130eb-284">Aby zainstalować 2.76b w węzłach, które są *już* w puli, ponownego uruchamiania lub je odtworzyć.</span><span class="sxs-lookup"><span data-stu-id="130eb-284">To install 2.76b on the nodes that are *already* in the pool, reboot or reimage them.</span></span> <span data-ttu-id="130eb-285">Należy zwrócić uwagę zachowanie pliki z poprzedniego wdrożenia pakietu po ponownym rozruchu węzłów.</span><span class="sxs-lookup"><span data-stu-id="130eb-285">Note that rebooted nodes retain the files from previous package deployments.</span></span>

## <a name="list-the-applications-in-a-batch-account"></a><span data-ttu-id="130eb-286">Wyświetl listę aplikacji w ramach konta usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="130eb-286">List the applications in a Batch account</span></span>
<span data-ttu-id="130eb-287">Można wyświetlić listę aplikacji i ich pakietów w ramach konta usługi partia zadań, za pomocą [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] metody.</span><span class="sxs-lookup"><span data-stu-id="130eb-287">You can list the applications and their packages in a Batch account by using the [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List the applications and their application packages in the Batch account.
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

## <a name="wrap-up"></a><span data-ttu-id="130eb-288">Dobiega końca</span><span class="sxs-lookup"><span data-stu-id="130eb-288">Wrap up</span></span>
<span data-ttu-id="130eb-289">Z pakietów aplikacji możesz pomóc klientom Wybierz aplikacje do ich zadań i określić dokładną wersję do użycia podczas przetwarzania zadania z usługą przetwarzania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="130eb-289">With application packages, you can help your customers select the applications for their jobs and specify the exact version to use when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="130eb-290">Można również określić przez klientów do przekazywania i śledzenie własnych aplikacji w usłudze.</span><span class="sxs-lookup"><span data-stu-id="130eb-290">You might also provide the ability for your customers to upload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="130eb-291">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="130eb-291">Next steps</span></span>
* <span data-ttu-id="130eb-292">[Interfejsu API REST partii] [ api_rest] obsługuje również do pracy z pakietami aplikacji.</span><span class="sxs-lookup"><span data-stu-id="130eb-292">The [Batch REST API][api_rest] also provides support to work with application packages.</span></span> <span data-ttu-id="130eb-293">Na przykład, zobacz [applicationPackageReferences] [ rest_add_pool_with_packages] element [Dodaj pulę, aby konto] [ rest_add_pool] informacji o sposobie określania pakiety do zainstalowania przy użyciu interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="130eb-293">For example, see the [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool to an account][rest_add_pool] for information about how to specify packages to install by using the REST API.</span></span> <span data-ttu-id="130eb-294">Zobacz [aplikacji] [ rest_applications] szczegółowe informacje na temat sposobu uzyskiwania informacji o aplikacji przy użyciu interfejsu API REST partii.</span><span class="sxs-lookup"><span data-stu-id="130eb-294">See [Applications][rest_applications] for details about how to obtain application information by using the Batch REST API.</span></span>
* <span data-ttu-id="130eb-295">Dowiedz się, jak programowo [Zarządzanie kontami partii zadań Azure i przydziały zarządzania partiami platformy .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="130eb-295">Learn how to programmatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="130eb-296">[Zarządzania partiami platformy .NET][api_net_mgmt] biblioteki można włączyć funkcji Tworzenie i usuwanie konta wsadowego aplikacji lub usługi.</span><span class="sxs-lookup"><span data-stu-id="130eb-296">The [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

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
