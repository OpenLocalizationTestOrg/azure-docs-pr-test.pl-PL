---
title: "Przekazywanie plików na konto usługi Azure Media Services za pomocą rozwiązania Aspera | Microsoft Docs"
description: "Ten samouczek przedstawia kroki przekazywania plików do konta magazynu, który jest skojarzony z kontem usługi Media Services przy użyciu ** Aspera serwera na żądanie ** usługi na platformie Azure."
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: e3090da9b2c5b8f99545a1f7f9601bfd8d5221f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-the-aspera-server-on-demand-service-on-azure"></a><span data-ttu-id="f60e4-103">Przekazywanie plików na konto usługi Media Services przy użyciu usługi Aspera Server On Demand na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f60e4-103">Upload files into a Media Services account using the Aspera Server On Demand service on Azure</span></span>

## <a name="overview"></a><span data-ttu-id="f60e4-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f60e4-104">Overview</span></span>

<span data-ttu-id="f60e4-105">**Aspera** to oprogramowanie do szybkiego transferowania plików.</span><span class="sxs-lookup"><span data-stu-id="f60e4-105">**Aspera** is a high-speed file transfer software.</span></span> <span data-ttu-id="f60e4-106">Usługa **Aspera Server On Demand** dla platformy Azure umożliwia szybkie przekazywanie i pobieranie dużych plików bezpośrednio do i z magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f60e4-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span></span> <span data-ttu-id="f60e4-107">Aby uzyskać informacje na temat usługi **Aspera On Demand**, zobacz witrynę [Aspera Cloud](http://cloud.asperasoft.com/).</span><span class="sxs-lookup"><span data-stu-id="f60e4-107">For information about **Aspera On Demand**, see the [Aspera Cloud](http://cloud.asperasoft.com/) site.</span></span> 
  
<span data-ttu-id="f60e4-108">Usługa **Aspera Server On Demand** dla platformy Azure jest dostępna do kupienia w witrynie [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/).</span><span class="sxs-lookup"><span data-stu-id="f60e4-108">**Aspera Server On Demand** for Azure is available for purchase from the [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span></span> <span data-ttu-id="f60e4-109">Aby ukończyć zakup usługi **Aspera Server On Demand** dla platformy Azure, zaloguj się do witryny Azure Marketplace przy użycia swojego identyfikatora usługi Windows Live.</span><span class="sxs-lookup"><span data-stu-id="f60e4-109">In order to complete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span></span>

<span data-ttu-id="f60e4-110">Ten samouczek przeprowadzi Cię przez kroki przekazywania plików na konto magazynu skojarzone z kontem usługi Media Services za pomocą usługi **Aspera Server On Demand** na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f60e4-110">This tutorial walks you through the steps of uploading files into a storage account that is associated with a Media Services account using the **Aspera Server On Demand** service on Azure.</span></span> 

<span data-ttu-id="f60e4-111">[W tym miejscu](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest) można znaleźć przykład sposobu używania funkcji platformy Azure z usługami Aspera i Media Services.</span><span class="sxs-lookup"><span data-stu-id="f60e4-111">You can find an example that shows how to use Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span></span>

>[!NOTE]
><span data-ttu-id="f60e4-112">Istnieje limit maksymalnego rozmiaru pliku przetwarzanego przez procesory multimediów usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="f60e4-112">There is a limit to the maximum file size supported for processing with Azure Media Services media processors (MPs).</span></span> <span data-ttu-id="f60e4-113">Zobacz [ten](media-services-quotas-and-limitations.md) temat, aby uzyskać szczegółowe informacje na temat ograniczeń rozmiarów plików.</span><span class="sxs-lookup"><span data-stu-id="f60e4-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="f60e4-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f60e4-114">Prerequisites</span></span> 

<span data-ttu-id="f60e4-115">Do ukończenia tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f60e4-115">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="f60e4-116">Identyfikator usługi Windows Live</span><span class="sxs-lookup"><span data-stu-id="f60e4-116">A Windows Live ID</span></span>
* <span data-ttu-id="f60e4-117">[Konto platformy Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f60e4-117">An [Azure account](https://azure.microsoft.com).</span></span> <span data-ttu-id="f60e4-118">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f60e4-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="f60e4-119">[Konto usługi Azure Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="f60e4-119">An [Azure Media Services account](media-services-portal-create-account.md).</span></span>

## <a name="purchase-aspera-on-demand-for-azure"></a><span data-ttu-id="f60e4-120">Kupowanie usługi Aspera On Demand dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f60e4-120">Purchase Aspera On Demand for Azure</span></span>

<span data-ttu-id="f60e4-121">Po zalogowaniu się do witryny Azure Marketplace wykonaj te proste kroki, aby przeprowadzić zakup usługi Aspera On Demand dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f60e4-121">Once you have logged into Azure Marketplace,  follow these basic steps to complete your purchase of Aspera On Demand for Azure.</span></span>

1. <span data-ttu-id="f60e4-122">Wyszukaj nazwę Aspera i wybierz pozycję „Server On Demand”.</span><span class="sxs-lookup"><span data-stu-id="f60e4-122">Search for Aspera and select 'Server On Demand'.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. <span data-ttu-id="f60e4-124">Przejrzyj plany subskrypcji i kliknij pozycję „Zarejestruj się”.</span><span class="sxs-lookup"><span data-stu-id="f60e4-124">Review the subscription plans and click on 'Sign Up'</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. <span data-ttu-id="f60e4-126">Wprowadź szczegółowe informacje o subskrypcji Server on Demand.</span><span class="sxs-lookup"><span data-stu-id="f60e4-126">Fill in the specifics for your Server on Demand subscription.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. <span data-ttu-id="f60e4-128">Kliknij pozycję **Warstwa cenowa** i wybierz żądany miesięczny wolumin w panelu podrzędnym.</span><span class="sxs-lookup"><span data-stu-id="f60e4-128">Click on the **Pricing Tier** and select your desired monthly volume in the sub panel.</span></span> <span data-ttu-id="f60e4-129">W panelu **Szczegóły planu** wybierz pozycję **OK**.</span><span class="sxs-lookup"><span data-stu-id="f60e4-129">In the **Plan details** panel, select **OK**.</span></span> <span data-ttu-id="f60e4-130">Następnie w panelu **Wybierz warstwę cenową** kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="f60e4-130">Then, in the **Choose your Pricing Tier** panel, click **Select**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. <span data-ttu-id="f60e4-132">W panelu podrzędnym kliknij pozycję **Warunki prawne**, aby je wyświetlić i zaakceptować.</span><span class="sxs-lookup"><span data-stu-id="f60e4-132">Click on **Legal terms** to view and accept the legal terms in the sub panel.</span></span> <span data-ttu-id="f60e4-133">Po przejrzeniu warunków prawnych kliknij pozycję **Kup**.</span><span class="sxs-lookup"><span data-stu-id="f60e4-133">Once you have reviewed the legal terms, click **Purchase**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. <span data-ttu-id="f60e4-135">Sfinalizuj zakup, klikając pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f60e4-135">Complete the purchase by clicking **Create**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. <span data-ttu-id="f60e4-137">Na pulpicie nawigacyjnym platformy Azure pojawi się informacja, że usługa jest aprowizowana.</span><span class="sxs-lookup"><span data-stu-id="f60e4-137">The Azure dashboard will announce that it is provisioning the service.</span></span>  <span data-ttu-id="f60e4-138">Po zakończeniu aprowizacji nową subskrypcję będzie można znaleźć, wyszukując nazwę usługi w swoich zasobach.</span><span class="sxs-lookup"><span data-stu-id="f60e4-138">Once it is completed with provisioning, you can find the new subscription by searching in your resources for the name of the service.</span></span> <span data-ttu-id="f60e4-139">Po znalezieniu usługi kliknij ją dwukrotnie, aby uruchomić portal zarządzania usługą.</span><span class="sxs-lookup"><span data-stu-id="f60e4-139">Once you have found the service, double click on it to launch the service management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. <span data-ttu-id="f60e4-141">Uruchom portal zarządzania usługi Aspera.</span><span class="sxs-lookup"><span data-stu-id="f60e4-141">Launch the Aspera management portal.</span></span> <span data-ttu-id="f60e4-142">Po znalezieniu nowej usługi Aspera można uzyskać dostęp do portalu zarządzania, klikając usługę.</span><span class="sxs-lookup"><span data-stu-id="f60e4-142">Once you have found your new Aspera service, you can gain access to the management portal, by clicking on the service.</span></span>  <span data-ttu-id="f60e4-143">Zostanie uruchomiony nowy panel.</span><span class="sxs-lookup"><span data-stu-id="f60e4-143">A new panel will be launched.</span></span> <span data-ttu-id="f60e4-144">Na tym nowym panelu kliknij **nazwę zasobu** nowej usługi.</span><span class="sxs-lookup"><span data-stu-id="f60e4-144">From within that new panel, you need to click on the **Resource Name** of your new service.</span></span>  <span data-ttu-id="f60e4-145">Na poniższym zrzucie ekranu nazwa zasobu to „AsperaTransferDemo”.</span><span class="sxs-lookup"><span data-stu-id="f60e4-145">In the following screenshot, the resource name is 'AsperaTransferDemo'.</span></span> <span data-ttu-id="f60e4-146">Po kliknięciu nazwy zasobu zostanie uruchomiony kolejny panel.</span><span class="sxs-lookup"><span data-stu-id="f60e4-146">Once you click on the resource name, another panel is launched.</span></span> <span data-ttu-id="f60e4-147">W tym nowo uruchomionym panelu zobaczysz link „Zarządzaj”.</span><span class="sxs-lookup"><span data-stu-id="f60e4-147">In that newly launched panel, you will see a 'Manage' link.</span></span> <span data-ttu-id="f60e4-148">Kliknij link „Zarządzaj”, aby uruchomić portal zarządzania usługi Aspera.</span><span class="sxs-lookup"><span data-stu-id="f60e4-148">Click on the 'Manage' link to launch the Aspera management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. <span data-ttu-id="f60e4-150">Po kliknięciu linku zarządzania zostanie otwarta strona rejestracji. Rejestracja jest wymagana, aby uzyskać dostęp do usługi.</span><span class="sxs-lookup"><span data-stu-id="f60e4-150">By clicking on the manage link, you will get to the registration page, which is required to access the service.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. <span data-ttu-id="f60e4-152">W tym momencie powinien już być możliwy dostęp do portalu zarządzania usługą Aspera, w którym można tworzyć klucze dostępu, pobierać klientów i licencje usługi Aspera, wyświetlać użycie i dowiedzieć się więcej na temat interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="f60e4-152">At this point, you should have access to the Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about the APIs.</span></span>

    <span data-ttu-id="f60e4-153">Następujący zrzut ekranu przedstawia tworzenie dostępu.</span><span class="sxs-lookup"><span data-stu-id="f60e4-153">The following screenshot shows the access creation.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    <span data-ttu-id="f60e4-155">Poniższy zrzut ekranu przedstawia interfejsy raportowania użycia w portalu.</span><span class="sxs-lookup"><span data-stu-id="f60e4-155">The following screenshot shows the usage reporting interfaces in the portal.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a><span data-ttu-id="f60e4-157">Przekazywanie plików za pomocą usługi Aspera</span><span class="sxs-lookup"><span data-stu-id="f60e4-157">Upload files with Aspera</span></span>

1. <span data-ttu-id="f60e4-158">Pobierz i zainstaluj oprogramowanie klienckie Aspera:</span><span class="sxs-lookup"><span data-stu-id="f60e4-158">Download and install the Aspera client software:</span></span>
    
    * [<span data-ttu-id="f60e4-159">Wtyczka przeglądarki</span><span class="sxs-lookup"><span data-stu-id="f60e4-159">Browser plugin</span></span>](http://downloads.asperasoft.com/connect2/)
    * [<span data-ttu-id="f60e4-160">Klient wzbogacony</span><span class="sxs-lookup"><span data-stu-id="f60e4-160">Rich client</span></span>](http://downloads.asperasoft.com/en/downloads/2)

2. <span data-ttu-id="f60e4-161">Przeprowadź pierwszy transfer.</span><span class="sxs-lookup"><span data-stu-id="f60e4-161">Make your first transfer.</span></span> <span data-ttu-id="f60e4-162">Aby móc używać klienta Aspera do transferowania danych za pomocą usługi transferowania Aspera, musisz ukończyć następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f60e4-162">In order to use the Aspera client to transfer with the Aspera transfer service, you need to complete the following:</span></span> 

    1. <span data-ttu-id="f60e4-163">Utwórz klucz dostępu za pomocą portalu usługi Aspera.</span><span class="sxs-lookup"><span data-stu-id="f60e4-163">Create an access key, using the Aspera portal.</span></span>  
    2. <span data-ttu-id="f60e4-164">Pobierz i zainstaluj klienta usługi Aspera (oprogramowanie można znaleźć w portalu usługi Aspera) oraz uzyskaj dla niego licencję.</span><span class="sxs-lookup"><span data-stu-id="f60e4-164">Download, install, and license the Aspera client (software can be found in the Aspera portal).</span></span>  

    >[!NOTE]
    ><span data-ttu-id="f60e4-165">Przeczytaj podręcznik klienta usługi Aspera w celu uzyskania informacji o konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f60e4-165">Please read the Aspera client guide for configuration information.</span></span>
    
    3. <span data-ttu-id="f60e4-166">Pobierz niektóre informacje o swoim koncie magazynu skojarzonym z kontem usługi Azure Media za pomocą witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f60e4-166">Retrieve some information of your storage account that is associated with your Azure Media Account using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="f60e4-167">Konkretnie potrzebne będą nazwa i klucz oraz nazwa kontenera obiektu blob magazynu, w którym chcesz umieścić swoją zawartość.</span><span class="sxs-lookup"><span data-stu-id="f60e4-167">Specifically, name and key, and the storage blob container name in to which you want to place your content.</span></span> 

        * <span data-ttu-id="f60e4-168">Aby uzyskać informacje o magazynie z portalu: znajdź swoje konto magazynu, kliknij pozycję Klucze dostępu i skopiuj nazwę oraz klucz konta.</span><span class="sxs-lookup"><span data-stu-id="f60e4-168">To get the storage info from the portal: find your storage account, click on the Access keys and copy the name and the key of your account.</span></span>
        * <span data-ttu-id="f60e4-169">Aby uzyskać nazwę kontenera: znajdź swoje konto magazynu, wybierz opcję **Obiekty blob** i wybierz nazwę kontenera, do którego chcesz przekazywać zawartość.</span><span class="sxs-lookup"><span data-stu-id="f60e4-169">To get the container name: find your storage account, select **Blobs**, select the name of the container you want to upload the content into.</span></span> 

    <span data-ttu-id="f60e4-170">Poniżej znajduje się zrzut ekranu **Menedżer połączeń** klienta usługi Aspera, w którym jako typ magazynu należy określić wartość „Azure”, a także podać poświadczenia i wskazać kontener obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="f60e4-170">Below is the screenshot of the Aspera client **Connection Manager** where you must specify the 'Azure' storage type and credentials as well as the blob container.</span></span>

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a><span data-ttu-id="f60e4-172">Zasoby</span><span class="sxs-lookup"><span data-stu-id="f60e4-172">Resources</span></span>

<span data-ttu-id="f60e4-173">W niniejszym artykule zostały wymienione poniższe zasoby.</span><span class="sxs-lookup"><span data-stu-id="f60e4-173">The following resources were mentioned in this article.</span></span> 

* [<span data-ttu-id="f60e4-174">Nawiązywanie połączenia z wtyczką przeglądarki</span><span class="sxs-lookup"><span data-stu-id="f60e4-174">Connect Browser Plugin</span></span>](http://downloads.asperasoft.com/connect2/)
* [<span data-ttu-id="f60e4-175">Przewodnik po nawiązywaniu połączeń</span><span class="sxs-lookup"><span data-stu-id="f60e4-175">Connect Guide</span></span>](http://downloads.asperasoft.com/en/documentation/8)
* [<span data-ttu-id="f60e4-176">Klient usługi Aspera</span><span class="sxs-lookup"><span data-stu-id="f60e4-176">Aspera Client</span></span>](http://downloads.asperasoft.com/en/downloads/2)
* [<span data-ttu-id="f60e4-177">Podręcznik klienta</span><span class="sxs-lookup"><span data-stu-id="f60e4-177">Client Guide</span></span>](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a><span data-ttu-id="f60e4-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f60e4-178">Next steps</span></span>

<span data-ttu-id="f60e4-179">Możesz teraz [kopiować obiekty blob z konta magazynu na konto usługi AMS](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span><span class="sxs-lookup"><span data-stu-id="f60e4-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f60e4-180">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="f60e4-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f60e4-181">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="f60e4-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

