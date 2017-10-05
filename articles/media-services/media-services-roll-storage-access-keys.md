---
title: "Aktualizacja usługi Media Services po wycofanie kluczy dostępu do magazynu | Dokumentacja firmy Microsoft"
description: "W tym artykule umożliwiają wskazówki na temat aktualizowania usługi Media Services po wycofanie kluczy dostępu do magazynu."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a892ebb0-0ea0-4fc8-b715-60347cc5c95b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: milanga;cenkdin;juliako
ms.openlocfilehash: 304e72e0d2d4a7e95df513e6d5481def9eae3f68
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a><span data-ttu-id="85c48-103">Aktualizacja usługi Media Services po wycofanie kluczy dostępu do magazynu</span><span class="sxs-lookup"><span data-stu-id="85c48-103">Update Media Services after rolling storage access keys</span></span>

<span data-ttu-id="85c48-104">Podczas tworzenia nowego konta usługi Azure Media Services (AMS) również należy wybrać konto magazynu Azure używanego do przechowywania zawartości nośnika.</span><span class="sxs-lookup"><span data-stu-id="85c48-104">When you create a new Azure Media Services (AMS) account, you are also asked to select an Azure Storage account that is used to store your media content.</span></span> <span data-ttu-id="85c48-105">Można dodać więcej niż jedno konto magazynu do konta usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="85c48-105">You can add more than one storage accounts to your Media Services account.</span></span> <span data-ttu-id="85c48-106">W tym temacie przedstawiono sposób Obróć magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="85c48-106">This topic shows how to rotate storage keys.</span></span> <span data-ttu-id="85c48-107">Zawiera on również sposób dodawania konta magazynu do konta usługi media.</span><span class="sxs-lookup"><span data-stu-id="85c48-107">It also shows how to add storage accounts to a media account.</span></span> 

<span data-ttu-id="85c48-108">Aby wykonać czynności opisane w tym temacie, należy używać [ARM interfejsów API](https://docs.microsoft.com/rest/api/media/mediaservice) i [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span><span class="sxs-lookup"><span data-stu-id="85c48-108">To perform the actions described in this topic, you should be using [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span></span>  <span data-ttu-id="85c48-109">Aby uzyskać więcej informacji, zobacz [sposobu zarządzania zasobami Azure za pomocą programu PowerShell i Menedżera zasobów](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="85c48-109">For more information, see [How to manage Azure resources with PowerShell and Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

## <a name="overview"></a><span data-ttu-id="85c48-110">Omówienie</span><span class="sxs-lookup"><span data-stu-id="85c48-110">Overview</span></span>

<span data-ttu-id="85c48-111">Po utworzeniu nowego konta magazynu Azure generuje dwa klucze dostępu do magazynu 512-bitowe, które są używane do uwierzytelniania dostępu do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="85c48-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used to authenticate access to your storage account.</span></span> <span data-ttu-id="85c48-112">Do zabezpieczania połączenia z magazynem, zalecane jest okresowe ponowne wygenerowanie i obracania klucz dostępu do magazynu.</span><span class="sxs-lookup"><span data-stu-id="85c48-112">To keep your storage connections more secure, it is recommended to periodically regenerate and rotate your storage access key.</span></span> <span data-ttu-id="85c48-113">Dwa klucze dostępu (podstawowych i pomocniczych) znajdują się w celu umożliwienia można obsługiwać połączenia z kontem magazynu za pomocą jednego klucza dostępu, jednocześnie ponownie generując drugi klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="85c48-113">Two access keys (primary and secondary) are provided in order to enable you to maintain connections to the storage account using one access key while you regenerate the other access key.</span></span> <span data-ttu-id="85c48-114">Ta procedura jest również nazywany "stopniowego klucze dostępu".</span><span class="sxs-lookup"><span data-stu-id="85c48-114">This procedure is also called "rolling access keys".</span></span>

<span data-ttu-id="85c48-115">Podany klucz magazynu zależy od usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="85c48-115">Media Services depends on a storage key provided to it.</span></span> <span data-ttu-id="85c48-116">W szczególności lokalizatorów, które są używane do przesyłania strumieniowego lub pobierania zasobów są zależne od klucz dostępu do określonego magazynu.</span><span class="sxs-lookup"><span data-stu-id="85c48-116">Specifically, the locators that are used to stream or download your assets depend on the specified storage access key.</span></span> <span data-ttu-id="85c48-117">Po utworzeniu konta usługi AMS ma zależność na klucz dostępu do magazynu głównej domyślnie, ale jako użytkownik może zaktualizować klucza magazynu, który ma AMS.</span><span class="sxs-lookup"><span data-stu-id="85c48-117">When an AMS account is created it takes a dependency on the primary storage access key by default but as a user you can update the storage key that AMS has.</span></span> <span data-ttu-id="85c48-118">Należy się upewnić umożliwić Media Services wiedzieć, który klucz do użycia, wykonując kroki opisane w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="85c48-118">You must make sure to let Media Services know which key to use by following steps described in this topic.</span></span>  

>[!NOTE]
> <span data-ttu-id="85c48-119">Jeśli masz wiele kont magazynu, można zastosować tę procedurę za pomocą każdego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="85c48-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span></span> <span data-ttu-id="85c48-120">Kolejność, w którym obracania magazynu kluczy nie jest stały.</span><span class="sxs-lookup"><span data-stu-id="85c48-120">The order in which you rotate storage keys is not fixed.</span></span> <span data-ttu-id="85c48-121">Można obracać dodatkowej pierwszy klucza, a następnie podstawowy klucz lub na odwrót.</span><span class="sxs-lookup"><span data-stu-id="85c48-121">You can rotate the secondary key first and then the primary key or vice versa.</span></span>
>
> <span data-ttu-id="85c48-122">Przed wykonaniem kroków opisanych w tym temacie na koncie produkcji, upewnij się, że testowane na koncie produkcji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="85c48-122">Before executing steps described in this topic on a production account, make sure to test them on a pre-production account.</span></span>
>

## <a name="steps-to-rotate-storage-keys"></a><span data-ttu-id="85c48-123">Kroki w celu obracania magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="85c48-123">Steps to rotate storage keys</span></span> 
 
 1. <span data-ttu-id="85c48-124">Należy zmienić wartość klucza podstawowego konta magazynu za pomocą polecenia cmdlet programu powershell lub [Azure](https://portal.azure.com/) portalu.</span><span class="sxs-lookup"><span data-stu-id="85c48-124">Change the storage account Primary key through the powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span></span>
 2. <span data-ttu-id="85c48-125">Wywołaj polecenie cmdlet AzureRmMediaServiceStorageKeys synchronizacji z odpowiednie parametry, aby wymusić wykrycie klucze konta magazynu konta usługi media</span><span class="sxs-lookup"><span data-stu-id="85c48-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params to force media account to pick up storage account keys</span></span>
 
    <span data-ttu-id="85c48-126">Poniższy przykład pokazuje, jak można zsynchronizować klucze kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="85c48-126">The following example shows how to sync keys to storage accounts.</span></span>
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. <span data-ttu-id="85c48-127">Zaczekaj godzinę.</span><span class="sxs-lookup"><span data-stu-id="85c48-127">Wait an hour or so.</span></span> <span data-ttu-id="85c48-128">Sprawdź, czy działają scenariusze przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="85c48-128">Verify the streaming scenarios are working.</span></span>
 4. <span data-ttu-id="85c48-129">Zmiana klucza pomocniczego konta magazynu za pomocą polecenia cmdlet programu powershell lub portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="85c48-129">Change storage account secondary key through the powershell cmdlet or Azure portal.</span></span>
 5. <span data-ttu-id="85c48-130">Wywołanie synchronizacji AzureRmMediaServiceStorageKeys powershell za pomocą odpowiednie parametry, aby wymusić konta usługi media do odebrania nowych kluczy kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="85c48-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params to force media account to pick up new storage account keys.</span></span> 
 6. <span data-ttu-id="85c48-131">Zaczekaj godzinę.</span><span class="sxs-lookup"><span data-stu-id="85c48-131">Wait an hour or so.</span></span> <span data-ttu-id="85c48-132">Sprawdź, czy działają scenariusze przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="85c48-132">Verify the streaming scenarios are working.</span></span>
 
### <a name="a-powershell-cmdlet-example"></a><span data-ttu-id="85c48-133">Przykład polecenia cmdlet programu powershell</span><span class="sxs-lookup"><span data-stu-id="85c48-133">A powershell cmdlet example</span></span> 

<span data-ttu-id="85c48-134">W poniższym przykładzie pokazano, jak pobrać konta magazynu i synchronizacji z konta usługi AMS.</span><span class="sxs-lookup"><span data-stu-id="85c48-134">The following example demonstrates how to get the storage account and sync it with the AMS account.</span></span>

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-to-add-storage-accounts-to-your-ams-account"></a><span data-ttu-id="85c48-135">Kroki, aby dodać konta magazynu do konta usługi AMS</span><span class="sxs-lookup"><span data-stu-id="85c48-135">Steps to add storage accounts to your AMS account</span></span>

<span data-ttu-id="85c48-136">Poniższy temat opisuje sposób dodawania konta magazynu do konta usługi AMS: [dołączyć wiele kont magazynu do konta usługi Media Services](meda-services-managing-multiple-storage-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="85c48-136">The following topic shows how to add storage accounts to your AMS account: [Attach multiple storage accounts to a Media Services account](meda-services-managing-multiple-storage-accounts.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="85c48-137">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="85c48-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="85c48-138">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="85c48-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="85c48-139">Potwierdzenia</span><span class="sxs-lookup"><span data-stu-id="85c48-139">Acknowledgments</span></span>
<span data-ttu-id="85c48-140">Chcemy potwierdzić następujących osób, które przyczyniły się do tworzenia tego dokumentu: Seva Titov Cenk Dingiloglu, Gada Mediolan.</span><span class="sxs-lookup"><span data-stu-id="85c48-140">We would like to acknowledge the following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span></span>
