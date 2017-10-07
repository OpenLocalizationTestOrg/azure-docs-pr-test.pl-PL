---
title: "pliki aaaUpload do konta usługi Azure Media Services przy użyciu Aspera | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki hello przekazywania plików do konta magazynu, który jest skojarzony z kontem usługi Media Services przy użyciu hello ** Aspera serwera na żądanie ** usługi na platformie Azure."
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
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a><span data-ttu-id="35041-103">Przekazywanie plików do konta usługi Media Services przy użyciu hello Aspera serwera na żądanie usługi na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="35041-103">Upload files into a Media Services account using hello Aspera Server On Demand service on Azure</span></span>

## <a name="overview"></a><span data-ttu-id="35041-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="35041-104">Overview</span></span>

<span data-ttu-id="35041-105">**Aspera** to oprogramowanie do szybkiego transferowania plików.</span><span class="sxs-lookup"><span data-stu-id="35041-105">**Aspera** is a high-speed file transfer software.</span></span> <span data-ttu-id="35041-106">Usługa **Aspera Server On Demand** dla platformy Azure umożliwia szybkie przekazywanie i pobieranie dużych plików bezpośrednio do i z magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="35041-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span></span> <span data-ttu-id="35041-107">Aby uzyskać informacje o **Aspera na żądanie**, zobacz hello [chmury Aspera](http://cloud.asperasoft.com/) lokacji.</span><span class="sxs-lookup"><span data-stu-id="35041-107">For information about **Aspera On Demand**, see hello [Aspera Cloud](http://cloud.asperasoft.com/) site.</span></span> 
  
<span data-ttu-id="35041-108">**Serwer Aspera na żądanie** Azure jest dostępne do zakupu od hello [witrynę Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span><span class="sxs-lookup"><span data-stu-id="35041-108">**Aspera Server On Demand** for Azure is available for purchase from hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span></span> <span data-ttu-id="35041-109">W celu toocomplete zakupu **Aspera serwera na żądanie** dla platformy Azure, należy zalogować się do portalu Azure Marketplace z swojego identyfikatora Windows Live.</span><span class="sxs-lookup"><span data-stu-id="35041-109">In order toocomplete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span></span>

<span data-ttu-id="35041-110">Ten samouczek przedstawia kroki hello przekazywania plików do konta magazynu, który jest skojarzony z kontem usługi Media Services przy użyciu hello **Aspera serwera na żądanie** usługi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="35041-110">This tutorial walks you through hello steps of uploading files into a storage account that is associated with a Media Services account using hello **Aspera Server On Demand** service on Azure.</span></span> 

<span data-ttu-id="35041-111">Przykład działania toouse Azure z Aspera i usługi Media Services można znaleźć [tutaj](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span><span class="sxs-lookup"><span data-stu-id="35041-111">You can find an example that shows how toouse Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span></span>

>[!NOTE]
><span data-ttu-id="35041-112">Brak limitu toohello maksymalny obsługiwany rozmiar pliku do przetwarzania w usłudze Azure Media Services procesory multimediów (MP).</span><span class="sxs-lookup"><span data-stu-id="35041-112">There is a limit toohello maximum file size supported for processing with Azure Media Services media processors (MPs).</span></span> <span data-ttu-id="35041-113">Zobacz [to](media-services-quotas-and-limitations.md) tematu, aby uzyskać szczegółowe informacje dotyczące limitu rozmiaru pliku hello.</span><span class="sxs-lookup"><span data-stu-id="35041-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="35041-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="35041-114">Prerequisites</span></span> 

<span data-ttu-id="35041-115">toocomplete tego samouczka należy:</span><span class="sxs-lookup"><span data-stu-id="35041-115">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="35041-116">Identyfikator usługi Windows Live</span><span class="sxs-lookup"><span data-stu-id="35041-116">A Windows Live ID</span></span>
* <span data-ttu-id="35041-117">[Konto platformy Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="35041-117">An [Azure account](https://azure.microsoft.com).</span></span> <span data-ttu-id="35041-118">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35041-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="35041-119">[Konto usługi Azure Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="35041-119">An [Azure Media Services account](media-services-portal-create-account.md).</span></span>

## <a name="purchase-aspera-on-demand-for-azure"></a><span data-ttu-id="35041-120">Kupowanie usługi Aspera On Demand dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="35041-120">Purchase Aspera On Demand for Azure</span></span>

<span data-ttu-id="35041-121">Po użytkownik zalogował się do portalu Azure Marketplace, należy wykonać te podstawowe kroki toocomplete zakupie Aspera na żądanie dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="35041-121">Once you have logged into Azure Marketplace,  follow these basic steps toocomplete your purchase of Aspera On Demand for Azure.</span></span>

1. <span data-ttu-id="35041-122">Wyszukaj nazwę Aspera i wybierz pozycję „Server On Demand”.</span><span class="sxs-lookup"><span data-stu-id="35041-122">Search for Aspera and select 'Server On Demand'.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. <span data-ttu-id="35041-124">Przejrzyj hello plany subskrypcji i kliknij przycisk "Utwórz konto"</span><span class="sxs-lookup"><span data-stu-id="35041-124">Review hello subscription plans and click on 'Sign Up'</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. <span data-ttu-id="35041-126">Wprowadź szczegóły powitania serwera na żądanie subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="35041-126">Fill in hello specifics for your Server on Demand subscription.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. <span data-ttu-id="35041-128">Polecenie hello **warstwy cenowej** i wybierz odpowiednią woluminu miesięczne hello sub panelu.</span><span class="sxs-lookup"><span data-stu-id="35041-128">Click on hello **Pricing Tier** and select your desired monthly volume in hello sub panel.</span></span> <span data-ttu-id="35041-129">W hello **planowanie szczegóły** panelu, wybierz opcję **OK**.</span><span class="sxs-lookup"><span data-stu-id="35041-129">In hello **Plan details** panel, select **OK**.</span></span> <span data-ttu-id="35041-130">Następnie w hello **wybierz warstwę cenową** panelu, kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="35041-130">Then, in hello **Choose your Pricing Tier** panel, click **Select**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. <span data-ttu-id="35041-132">Polecenie **postanowienia prawne** tooview i zaakceptuj postanowienia prawne hello hello sub panelu.</span><span class="sxs-lookup"><span data-stu-id="35041-132">Click on **Legal terms** tooview and accept hello legal terms in hello sub panel.</span></span> <span data-ttu-id="35041-133">Po przejrzeniu hello postanowienia prawne, kliknij przycisk **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="35041-133">Once you have reviewed hello legal terms, click **Purchase**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. <span data-ttu-id="35041-135">Ukończ zakupu hello klikając **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="35041-135">Complete hello purchase by clicking **Create**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. <span data-ttu-id="35041-137">Hello Azure pulpitu nawigacyjnego ogłaszamy, że jest inicjowania obsługi usługi hello.</span><span class="sxs-lookup"><span data-stu-id="35041-137">hello Azure dashboard will announce that it is provisioning hello service.</span></span>  <span data-ttu-id="35041-138">Po zakończeniu z inicjowaniem obsługi administracyjnej przez wyszukiwanie w Twoich zasobów dla nazwy hello hello usługi można znaleźć hello nową subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="35041-138">Once it is completed with provisioning, you can find hello new subscription by searching in your resources for hello name of hello service.</span></span> <span data-ttu-id="35041-139">Po znalezieniu hello usługi, podwójne kliknięcie portalu zarządzania usługami hello toolaunch.</span><span class="sxs-lookup"><span data-stu-id="35041-139">Once you have found hello service, double click on it toolaunch hello service management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. <span data-ttu-id="35041-141">Uruchom program hello Aspera management portal.</span><span class="sxs-lookup"><span data-stu-id="35041-141">Launch hello Aspera management portal.</span></span> <span data-ttu-id="35041-142">Po znalezieniu nowej usługi Aspera mogą uzyskać dostęp do portalu zarządzania toohello, klikając hello usługi.</span><span class="sxs-lookup"><span data-stu-id="35041-142">Once you have found your new Aspera service, you can gain access toohello management portal, by clicking on hello service.</span></span>  <span data-ttu-id="35041-143">Zostanie uruchomiony nowy panel.</span><span class="sxs-lookup"><span data-stu-id="35041-143">A new panel will be launched.</span></span> <span data-ttu-id="35041-144">Od w tym nowym panelu należy tooclick na powitania **Nazwa zasobu** z nowej usługi.</span><span class="sxs-lookup"><span data-stu-id="35041-144">From within that new panel, you need tooclick on hello **Resource Name** of your new service.</span></span>  <span data-ttu-id="35041-145">W hello następującego zrzutu ekranu Nazwa zasobu hello jest "AsperaTransferDemo".</span><span class="sxs-lookup"><span data-stu-id="35041-145">In hello following screenshot, hello resource name is 'AsperaTransferDemo'.</span></span> <span data-ttu-id="35041-146">Po kliknięciu hello Nazwa zasobu jest uruchamiana innego panelu.</span><span class="sxs-lookup"><span data-stu-id="35041-146">Once you click on hello resource name, another panel is launched.</span></span> <span data-ttu-id="35041-147">W tym nowo uruchomionym panelu zobaczysz link „Zarządzaj”.</span><span class="sxs-lookup"><span data-stu-id="35041-147">In that newly launched panel, you will see a 'Manage' link.</span></span> <span data-ttu-id="35041-148">Polecenie hello portalu zarządzania Aspera hello toolaunch link "Zarządzaj".</span><span class="sxs-lookup"><span data-stu-id="35041-148">Click on hello 'Manage' link toolaunch hello Aspera management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. <span data-ttu-id="35041-150">Klikając hello zarządzać link, zostanie wyświetlona strona rejestracji toohello, co jest wymagane tooaccess hello usługi.</span><span class="sxs-lookup"><span data-stu-id="35041-150">By clicking on hello manage link, you will get toohello registration page, which is required tooaccess hello service.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. <span data-ttu-id="35041-152">W tym momencie powinien mieć dostęp toohello Aspera portalu zarządzania usługami, gdzie można utworzyć klucze dostępu, Pobierz Aspera klientów i licencji, Wyświetl użycie i Dowiedz się więcej o hello interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="35041-152">At this point, you should have access toohello Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about hello APIs.</span></span>

    <span data-ttu-id="35041-153">Witaj Poniższy zrzut ekranu przedstawia hello tworzenia dostępu.</span><span class="sxs-lookup"><span data-stu-id="35041-153">hello following screenshot shows hello access creation.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    <span data-ttu-id="35041-155">Witaj Poniższy zrzut ekranu przedstawia raportowanie interfejsów w portalu hello hello użycia.</span><span class="sxs-lookup"><span data-stu-id="35041-155">hello following screenshot shows hello usage reporting interfaces in hello portal.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a><span data-ttu-id="35041-157">Przekazywanie plików za pomocą usługi Aspera</span><span class="sxs-lookup"><span data-stu-id="35041-157">Upload files with Aspera</span></span>

1. <span data-ttu-id="35041-158">Pobierz i zainstaluj oprogramowanie klienckie Aspera hello:</span><span class="sxs-lookup"><span data-stu-id="35041-158">Download and install hello Aspera client software:</span></span>
    
    * [<span data-ttu-id="35041-159">Wtyczka przeglądarki</span><span class="sxs-lookup"><span data-stu-id="35041-159">Browser plugin</span></span>](http://downloads.asperasoft.com/connect2/)
    * [<span data-ttu-id="35041-160">Klient wzbogacony</span><span class="sxs-lookup"><span data-stu-id="35041-160">Rich client</span></span>](http://downloads.asperasoft.com/en/downloads/2)

2. <span data-ttu-id="35041-161">Przeprowadź pierwszy transfer.</span><span class="sxs-lookup"><span data-stu-id="35041-161">Make your first transfer.</span></span> <span data-ttu-id="35041-162">Kolejność toouse hello Aspera klienta tootransfer z hello Aspera transfer service niezbędne są następujące hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="35041-162">In order toouse hello Aspera client tootransfer with hello Aspera transfer service, you need toocomplete hello following:</span></span> 

    1. <span data-ttu-id="35041-163">Utwórz klucz dostępu za pomocą portalu Aspera hello.</span><span class="sxs-lookup"><span data-stu-id="35041-163">Create an access key, using hello Aspera portal.</span></span>  
    2. <span data-ttu-id="35041-164">Pobieranie, instalacji i licencji hello Aspera klienta (oprogramowania można znaleźć w portalu Aspera hello).</span><span class="sxs-lookup"><span data-stu-id="35041-164">Download, install, and license hello Aspera client (software can be found in hello Aspera portal).</span></span>  

    >[!NOTE]
    ><span data-ttu-id="35041-165">Przeczytaj przewodnik klienta Aspera hello informacji o konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="35041-165">Please read hello Aspera client guide for configuration information.</span></span>
    
    3. <span data-ttu-id="35041-166">Pobrać niektóre informacje o koncie magazynu, który jest skojarzony z Twoim kontem multimediów Azure przy użyciu hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="35041-166">Retrieve some information of your storage account that is associated with your Azure Media Account using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="35041-167">W szczególności nazwy i klucza, a nazwa kontenera obiektów blob magazynu hello w toowhich ma tooplace zawartości.</span><span class="sxs-lookup"><span data-stu-id="35041-167">Specifically, name and key, and hello storage blob container name in toowhich you want tooplace your content.</span></span> 

        * <span data-ttu-id="35041-168">informacje dotyczące tooget hello magazynu z portalu hello: znaleźć konta magazynu, kliknij hello klawisze dostępu, a kopia klucza nazwy i hello hello Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="35041-168">tooget hello storage info from hello portal: find your storage account, click on hello Access keys and copy hello name and hello key of your account.</span></span>
        * <span data-ttu-id="35041-169">Nazwa kontenera hello tooget: znaleźć konta magazynu, wybierz opcję **obiekty BLOB**, wybierz pozycję hello nazwa kontenera hello tooupload hello zawartość do.</span><span class="sxs-lookup"><span data-stu-id="35041-169">tooget hello container name: find your storage account, select **Blobs**, select hello name of hello container you want tooupload hello content into.</span></span> 

    <span data-ttu-id="35041-170">Poniżej przedstawiono zrzut ekranu powitania klienta Aspera hello **Menedżera połączeń** gdzie należy określić typ magazynu "Azure" hello i poświadczenia, a także hello kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="35041-170">Below is hello screenshot of hello Aspera client **Connection Manager** where you must specify hello 'Azure' storage type and credentials as well as hello blob container.</span></span>

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a><span data-ttu-id="35041-172">Zasoby</span><span class="sxs-lookup"><span data-stu-id="35041-172">Resources</span></span>

<span data-ttu-id="35041-173">Witaj następujące zasoby zostały wymienione w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="35041-173">hello following resources were mentioned in this article.</span></span> 

* [<span data-ttu-id="35041-174">Nawiązywanie połączenia z wtyczką przeglądarki</span><span class="sxs-lookup"><span data-stu-id="35041-174">Connect Browser Plugin</span></span>](http://downloads.asperasoft.com/connect2/)
* [<span data-ttu-id="35041-175">Przewodnik po nawiązywaniu połączeń</span><span class="sxs-lookup"><span data-stu-id="35041-175">Connect Guide</span></span>](http://downloads.asperasoft.com/en/documentation/8)
* [<span data-ttu-id="35041-176">Klient usługi Aspera</span><span class="sxs-lookup"><span data-stu-id="35041-176">Aspera Client</span></span>](http://downloads.asperasoft.com/en/downloads/2)
* [<span data-ttu-id="35041-177">Podręcznik klienta</span><span class="sxs-lookup"><span data-stu-id="35041-177">Client Guide</span></span>](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a><span data-ttu-id="35041-178">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="35041-178">Next steps</span></span>

<span data-ttu-id="35041-179">Możesz teraz [kopiować obiekty blob z konta magazynu na konto usługi AMS](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span><span class="sxs-lookup"><span data-stu-id="35041-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="35041-180">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="35041-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="35041-181">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="35041-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

