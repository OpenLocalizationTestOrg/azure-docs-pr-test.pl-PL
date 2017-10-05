---
title: "Włączanie funkcji przechwytywania usługi Azure Event Hubs przy użyciu portalu | Microsoft Docs"
description: "Włącz funkcję przechwytywania usługi Event Hubs przy użyciu witryny Azure Portal."
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
ms.openlocfilehash: 0cbf45dce922647f2996f929d2c7cf885a2f4db4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="enable-event-hubs-capture-using-the-azure-portal"></a><span data-ttu-id="5edc4-103">Włączanie funkcji przechwytywania usługi Event Hubs przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5edc4-103">Enable Event Hubs Capture using the Azure portal</span></span>

<span data-ttu-id="5edc4-104">Przy użyciu witryny [Azure Portal](https://portal.azure.com) można skonfigurować funkcję przechwytywania podczas tworzenia centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="5edc4-104">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5edc4-105">Dane mogą być przechwytywane do kontenera usługi Azure [Blob Storage](https://azure.microsoft.com/services/storage/blobs/) lub na konto usługi [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="5edc4-105">You can either capture the data to an Azure [Blob storage](https://azure.microsoft.com/services/storage/blobs/) container, or to an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account.</span></span>

## <a name="capture-data-to-an-azure-storage-account"></a><span data-ttu-id="5edc4-106">Przechwytywanie danych na konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5edc4-106">Capture data to an Azure Storage account</span></span>  

<span data-ttu-id="5edc4-107">Podczas tworzenia Centrum zdarzeń można włączyć przechwytywania, klikając **na** przycisk **tworzenia Centrum zdarzeń** bloku portalu.</span><span class="sxs-lookup"><span data-stu-id="5edc4-107">When you create an event hub, you can enable Capture by clicking the **On** button in the **Create Event Hub** portal blade.</span></span> <span data-ttu-id="5edc4-108">Następnie można określić konto magazynu i kontener przez kliknięcie pozycji **Azure Storage** w polu **Dostawca przechwytywania**.</span><span class="sxs-lookup"><span data-stu-id="5edc4-108">You then specify a Storage Account and container by clicking **Azure Storage** in the **Capture Provider** box.</span></span> <span data-ttu-id="5edc4-109">Ponieważ do uwierzytelniania w magazynie funkcja przechwytywania usługi Event Hubs korzysta z uwierzytelniania między usługami, nie trzeba podawać parametrów połączenia z magazynem.</span><span class="sxs-lookup"><span data-stu-id="5edc4-109">Because Event Hubs Capture uses service-to-service authentication with storage, you do not need to specify a storage connection string.</span></span> <span data-ttu-id="5edc4-110">Selektor zasobów automatycznie wybiera identyfikator URI zasobu dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="5edc4-110">The resource picker selects the resource URI for your storage account automatically.</span></span> <span data-ttu-id="5edc4-111">Jeśli używasz usługi Azure Resource Manager, musisz jawnie podać ten identyfikator URI jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="5edc4-111">If you use Azure Resource Manager, you must supply this URI explicitly as a string.</span></span>

<span data-ttu-id="5edc4-112">Domyślny przedział czasu to 5 minut.</span><span class="sxs-lookup"><span data-stu-id="5edc4-112">The default time window is 5 minutes.</span></span> <span data-ttu-id="5edc4-113">Minimalna wartość to 1, a maksymalna — 15.</span><span class="sxs-lookup"><span data-stu-id="5edc4-113">The minimum value is 1, the maximum 15.</span></span> <span data-ttu-id="5edc4-114">Okno **Rozmiar** ma zakres 10–500 MB.</span><span class="sxs-lookup"><span data-stu-id="5edc4-114">The **Size** window has a range of 10-500 MB.</span></span>

![][1]

## <a name="capture-data-to-an-azure-data-lake-store-account"></a><span data-ttu-id="5edc4-115">Przechwytywanie danych na konto usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5edc4-115">Capture data to an Azure Data Lake Store account</span></span>

<span data-ttu-id="5edc4-116">Aby przechwycić dane do usługi Azure Data Lake Store, należy utworzyć konto usługi Data Lake Store i centrum zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="5edc4-116">To capture data to Azure Data Lake Store, you create a Data Lake Store account, and an event hub:</span></span>

### <a name="create-an-azure-data-lake-store-account-and-folders"></a><span data-ttu-id="5edc4-117">Tworzenie konta i folderów usługi Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5edc4-117">Create an Azure Data Lake Store account and folders</span></span>

1. <span data-ttu-id="5edc4-118">Utwórz konto usługi Data Lake Store, postępując zgodnie z instrukcjami w temacie [Rozpoczynanie pracy z usługą Azure Data Lake Store za pomocą witryny Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5edc4-118">Create a Data Lake Store account, following the instructions in [Get started with Azure Data Lake Store using the Azure portal](../data-lake-store/data-lake-store-get-started-portal.md).</span></span> 
2. <span data-ttu-id="5edc4-119">Utwórz folder na tym koncie, postępując zgodnie z instrukcjami w sekcji [Tworzenie folderów w ramach konta usługi Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md#createfolder).</span><span class="sxs-lookup"><span data-stu-id="5edc4-119">Create a folder under this account, following the instructions in the [Create folders in Azure Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.</span></span>
3. <span data-ttu-id="5edc4-120">W bloku konta usługi Data Lake Store, kliknij **Eksploratora danych**.</span><span class="sxs-lookup"><span data-stu-id="5edc4-120">In the Data Lake Store account blade, click **Data Explorer**.</span></span>
4. <span data-ttu-id="5edc4-121">Kliknij pozycję **Dostęp**.</span><span class="sxs-lookup"><span data-stu-id="5edc4-121">Click **Access**.</span></span>
5. <span data-ttu-id="5edc4-122">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="5edc4-122">Click **Add**.</span></span>
6. <span data-ttu-id="5edc4-123">W polu **Wyszukaj według nazwy lub adresu e-mail** wpisz **Microsoft.EventHubs**, a następnie wybierz tę opcję.</span><span class="sxs-lookup"><span data-stu-id="5edc4-123">In the **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span> 
7. <span data-ttu-id="5edc4-124">Zostanie wyświetlona karta **Uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="5edc4-124">The **Permissions** tab appears.</span></span> <span data-ttu-id="5edc4-125">Ustaw uprawnienia, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="5edc4-125">Set the permissions as shown in the following figure:</span></span>

    ![][6]

8. <span data-ttu-id="5edc4-126">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="5edc4-126">Click **OK**.</span></span>
9. <span data-ttu-id="5edc4-127">Następnie utwórz folder w folderze głównym przez przejście do folderu docelowego i kliknięcie nazwy folderu.</span><span class="sxs-lookup"><span data-stu-id="5edc4-127">Now, create a folder in the root folder by browsing to the target folder and clicking on the folder name.</span></span>
10. <span data-ttu-id="5edc4-128">Kliknij pozycję **Dostęp**.</span><span class="sxs-lookup"><span data-stu-id="5edc4-128">Click **Access**.</span></span>
11. <span data-ttu-id="5edc4-129">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="5edc4-129">Click **Add**.</span></span>
12. <span data-ttu-id="5edc4-130">W polu **Wyszukaj według nazwy lub adresu e-mail** wpisz **Microsoft.EventHubs**, a następnie wybierz tę opcję.</span><span class="sxs-lookup"><span data-stu-id="5edc4-130">In the **Search by name or email** box type **Microsoft.EventHubs** and then select this option.</span></span>
13. <span data-ttu-id="5edc4-131">Ponownie zostanie wyświetlona karta **Uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="5edc4-131">The **Permissions** tab appears again.</span></span> <span data-ttu-id="5edc4-132">Ustaw uprawnienia, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="5edc4-132">Set the permissions as shown in the following figure:</span></span>

    ![][5]

### <a name="create-an-event-hub"></a><span data-ttu-id="5edc4-133">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="5edc4-133">Create an event hub</span></span>

1. <span data-ttu-id="5edc4-134">Centrum zdarzeń musi należeć do tej samej subskrypcji platformy Azure co właśnie utworzone konto usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5edc4-134">Note that the event hub must be in the same Azure subscription as the Azure Data Lake Store you just created.</span></span> <span data-ttu-id="5edc4-135">Tworzenie Centrum zdarzeń, klikając pozycję **na** przycisku w obszarze **przechwytywania** w **tworzenia Centrum zdarzeń** bloku portalu.</span><span class="sxs-lookup"><span data-stu-id="5edc4-135">Create the event hub, clicking the **On** button under **Capture** in the **Create Event Hub** portal blade.</span></span> 
2. <span data-ttu-id="5edc4-136">W **tworzenia Centrum zdarzeń** bloku portalu, wybierz opcję **Azure Data Lake Store** z **przechwytywania dostawcy** pole.</span><span class="sxs-lookup"><span data-stu-id="5edc4-136">In the **Create Event Hub** portal blade, select **Azure Data Lake Store** from the **Capture Provider** box.</span></span>
3. <span data-ttu-id="5edc4-137">W polu **Wybierz usługę Data Lake Store** określ utworzone wcześniej konto usługi Data Lake Store, a w polu **Ścieżka w usłudze Data Lake** wprowadź ścieżkę do utworzonego folderu danych.</span><span class="sxs-lookup"><span data-stu-id="5edc4-137">In **Select Data Lake Store**, specify the Data Lake Store account you created previously, and in the **Data Lake Path** field, enter the path to the data folder you created.</span></span>

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a><span data-ttu-id="5edc4-138">Dodawanie lub konfigurowanie funkcji przechwytywania w istniejącym centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="5edc4-138">Add or configure Capture on an existing event hub</span></span>

<span data-ttu-id="5edc4-139">Przechwytywanie można skonfigurować w istniejących centrach zdarzeń, które znajdują się w przestrzeniach nazw usługi Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="5edc4-139">You can configure Capture on existing event hubs that are in Event Hubs namespaces.</span></span> <span data-ttu-id="5edc4-140">Aby włączyć funkcję przechwytywania w istniejącym centrum zdarzeń lub zmienić ustawienia przechwytywania, kliknij przestrzeń nazw w celu załadowania bloku **Podstawy**, a następnie kliknij centrum zdarzeń, w którym chcesz włączyć przechwytywanie lub zmienić jego ustawienia.</span><span class="sxs-lookup"><span data-stu-id="5edc4-140">To enable Capture on an existing event hub, or to change your Capture settings, click the namespace to load the **Essentials** blade, then click the event hub for which you want to enable or change the Capture setting.</span></span> <span data-ttu-id="5edc4-141">Na koniec kliknij **właściwości** Otwórz bloku, a następnie Edytuj ustawienia przechwytywania, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="5edc4-141">Finally, click the **Properties** section of the open blade and then edit the Capture settings, as shown in the following figures:</span></span>

### <a name="azure-blob-storage"></a><span data-ttu-id="5edc4-142">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="5edc4-142">Azure Blob Storage</span></span>

![][2]

### <a name="azure-data-lake-store"></a><span data-ttu-id="5edc4-143">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5edc4-143">Azure Data Lake Store</span></span>

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a><span data-ttu-id="5edc4-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5edc4-144">Next steps</span></span>

<span data-ttu-id="5edc4-145">Funkcję przechwytywania usługi Event Hubs możesz również skonfigurować za pomocą szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5edc4-145">You can also configure Event Hubs Capture using Azure Resource Manager templates.</span></span> <span data-ttu-id="5edc4-146">Aby uzyskać więcej informacji, zobacz [Enable Capture using an Azure Resource Manager template (Włączanie funkcji przechwytywania przy użyciu szablonu usługi Azure Resource Manager)](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span><span class="sxs-lookup"><span data-stu-id="5edc4-146">For more information, see [Enable Capture using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).</span></span>
