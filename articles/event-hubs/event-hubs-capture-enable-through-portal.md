---
title: "Włącz aaaAzure przechwytywania centra zdarzeń za pośrednictwem portalu | Dokumentacja firmy Microsoft"
description: "Włącz funkcję przechwytywania centra zdarzeń hello przy użyciu hello portalu Azure."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a><span data-ttu-id="ef9d2-103">Włącz przy użyciu portalu Azure hello przechwytywania centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ef9d2-103">Enable Event Hubs Capture using hello Azure portal</span></span>

<span data-ttu-id="ef9d2-104">Można skonfigurować przechwytywania hello zdarzenia koncentratora czas utworzenia przy użyciu hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ef9d2-104">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ef9d2-105">Można albo przechwytywania tooan danych hello Azure [magazynu obiektów Blob](https://azure.microsoft.com/services/storage/blobs/) kontener lub tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) konta.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-105">You can either capture hello data tooan Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-tooan-azure-storage-account"></a><span data-ttu-id="ef9d2-106">Konto magazynu Azure tooan danych przechwytywania</span><span class="sxs-lookup"><span data-stu-id="ef9d2-106">Capture data tooan Azure Storage account</span></span>  

<span data-ttu-id="ef9d2-107">Podczas tworzenia Centrum zdarzeń można włączyć przechwytywania, klikając hello **na** przycisku na powitania **tworzenia Centrum zdarzeń** bloku portalu.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-107">When you create an event hub, you can enable Capture by clicking hello **On** button in hello **Create Event Hub** portal blade.</span></span> <span data-ttu-id="ef9d2-108">Następnie możesz określić konto magazynu i kontener, klikając **usługi Azure Storage** w hello **przechwytywania dostawcy** pole.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-108">You then specify a Storage Account and container by clicking **Azure Storage** in hello **Capture Provider** box.</span></span> <span data-ttu-id="ef9d2-109">Ponieważ przechwytywania centra zdarzeń korzysta z uwierzytelniania do usługi z magazynem, nie trzeba toospecify parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need toospecify a storage connection string.</span></span> <span data-ttu-id="ef9d2-110">Selektor zasobów Hello automatycznie wybiera hello identyfikator URI zasobu dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-110">hello resource picker selects hello resource URI for your storage account automatically.</span></span> <span data-ttu-id="ef9d2-111">Jeśli używasz usługi Azure Resource Manager, musisz jawnie podać ten identyfikator URI jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="ef9d2-112">przedział czasu domyślne Hello jest 5 minut.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-112">hello default time window is 5 minutes.</span></span> <span data-ttu-id="ef9d2-113">Hello minimalna wartość to 1, hello maksymalną 15.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-113">hello minimum value is 1, hello maximum 15.</span></span> <span data-ttu-id="ef9d2-114">Witaj **rozmiar** okno ma zakres 10 500 MB.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-114">hello **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a><span data-ttu-id="ef9d2-115">Konto usługi Azure Data Lake Store tooan danych przechwytywania</span><span class="sxs-lookup"><span data-stu-id="ef9d2-115">Capture data tooan Azure Data Lake Store account</span></span>

<span data-ttu-id="ef9d2-116">toocapture tooAzure danych Data Lake Store, Utwórz konto usługi Data Lake Store i Centrum zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="ef9d2-116">toocapture data tooAzure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="ef9d2-117">Tworzenie konta i folderów usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ef9d2-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="ef9d2-118">Utwórz konto usługi Data Lake Store instrukcjami hello w [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure hello](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ef9d2-118">Create a Data Lake Store account, following hello instructions in [Get started with Azure Data Lake Store using hello Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="ef9d2-119">Utwórz folder na tym koncie instrukcjami hello w hello [tworzenie folderów w ramach konta usługi Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) sekcji.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-119">Create a folder under this account, following hello instructions in hello [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="ef9d2-120">W bloku konta usługi Data Lake Store powitania kliknij **Eksploratora danych**.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-120">In hello Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="ef9d2-121">Kliknij pozycję **Dostęp**.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-121">Click **Access**.</span></span>
5. <span data-ttu-id="ef9d2-122">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-122">Click **Add**.</span></span>
6. <span data-ttu-id="ef9d2-123">W hello **wyszukiwania według nazwy lub e-mail** wpisz **Microsoft.EventHubs** , a następnie wybierz tę opcję.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-123">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="ef9d2-124">Witaj **uprawnienia** zostanie wyświetlona karta.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-124">hello **Permissions** tab appears.</span></span> <span data-ttu-id="ef9d2-125">Ustaw uprawnienia hello, jak pokazano w następującej ilustracji hello:</span><span class="sxs-lookup"><span data-stu-id="ef9d2-125">Set hello permissions as shown in hello following figure:</span></span>

    ![][6]

8. <span data-ttu-id="ef9d2-126">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-126">Click **OK**.</span></span>
9. <span data-ttu-id="ef9d2-127">Teraz Utwórz folder w folderze głównym hello przeglądanie toohello folder docelowy i klikając nazwę folderu hello.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-127">Now, create a folder in hello root folder by browsing toohello target folder and clicking on hello folder name.</span></span>
10. <span data-ttu-id="ef9d2-128">Kliknij pozycję **Dostęp**.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-128">Click **Access**.</span></span>
11. <span data-ttu-id="ef9d2-129">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-129">Click **Add**.</span></span>
12. <span data-ttu-id="ef9d2-130">W hello **wyszukiwania według nazwy lub e-mail** wpisz **Microsoft.EventHubs** , a następnie wybierz tę opcję.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-130">In hello **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="ef9d2-131">Witaj **uprawnienia** kartę pojawi się ponownie.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-131">hello **Permissions** tab appears again.</span></span> <span data-ttu-id="ef9d2-132">Ustaw uprawnienia hello, jak pokazano w następującej ilustracji hello:</span><span class="sxs-lookup"><span data-stu-id="ef9d2-132">Set hello permissions as shown in hello following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="ef9d2-133">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ef9d2-133">Create an event hub</span></span>

1. <span data-ttu-id="ef9d2-134">Tego Centrum zdarzeń hello musi być w hello tej samej subskrypcji platformy Azure jako hello Azure Data Lake Store właśnie utworzony.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-134">Note that hello event hub must be in hello same Azure subscription as hello Azure Data Lake Store you just created.</span></span> <span data-ttu-id="ef9d2-135">Tworzenie Centrum zdarzeń hello, klikając hello **na** przycisku w obszarze **przechwytywania** w hello **tworzenia Centrum zdarzeń** bloku portalu.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-135">Create hello event hub, clicking hello **On** button under **Capture** in hello **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="ef9d2-136">W hello **tworzenia Centrum zdarzeń** bloku portalu, wybierz opcję **Azure Data Lake Store** z hello **przechwytywania dostawcy** pole.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-136">In hello **Create Event Hub** portal blade, select **Azure Data Lake Store** from hello **Capture Provider** box.</span></span>
3. <span data-ttu-id="ef9d2-137">W **wybierz Data Lake Store**, określ hello utworzonego wcześniej, a w hello konta usługi Data Lake Store **Data Lake ścieżki** wprowadź hello ścieżki toohello folderu danych został utworzony.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-137">In **Select Data Lake Store**, specify hello Data Lake Store account you created previously, and in hello **Data Lake Path** field, enter hello path toohello data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="ef9d2-138">Dodawanie lub konfigurowanie funkcji przechwytywania w istniejącym centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="ef9d2-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="ef9d2-139">Przechwytywanie można skonfigurować w istniejących centrach zdarzeń, które znajdują się w przestrzeniach nazw usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="ef9d2-140">tooenable przechwytywania na istniejącym Centrum zdarzeń, lub toochange ustawienia przechwytywania, kliknij przycisk hello przestrzeni nazw tooload hello **Essentials** bloku, kliknij przycisk hello Centrum zdarzeń, dla którego chcesz tooenable lub zmienić ustawienie przechwytywania hello.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-140">tooenable Capture on an existing event hub, or toochange your Capture settings, click hello namespace tooload hello **Essentials** blade, then click hello event hub for which you want tooenable or change hello Capture setting.</span></span> <span data-ttu-id="ef9d2-141">Na koniec kliknij hello **właściwości** sekcji hello otwarcie bloku, a następnie Edytuj ustawienia przechwytywania hello, jak pokazano w hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="ef9d2-141">Finally, click hello **Properties** section of hello open blade and then edit hello Capture settings, as shown in hello following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="ef9d2-142">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="ef9d2-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="ef9d2-143">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ef9d2-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="ef9d2-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ef9d2-144">Next steps</span></span>

<span data-ttu-id="ef9d2-145">Funkcję przechwytywania usługi Event Hubs możesz również skonfigurować za pomocą szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ef9d2-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="ef9d2-146">Aby uzyskać więcej informacji, zobacz [Enable Capture using an Azure Resource Manager template (Włączanie funkcji przechwytywania przy użyciu szablonu usługi Azure Resource Manager)](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span><span class="sxs-lookup"><span data-stu-id="ef9d2-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>
