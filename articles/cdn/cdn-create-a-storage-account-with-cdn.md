---
title: "Konto magazynu platformy Azure z usługą Azure CDN aaaIntegrate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse zawartości hello Azure Content Delivery Network (CDN) toodeliver wysokiej przepustowości przez buforowanie obiektów blob z usługi Magazyn Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="0f9c7-103">Integracja z usługą Azure CDN konta magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0f9c7-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="0f9c7-104">Sieci CDN może być włączone toocache zawartości z magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-104">CDN can be enabled toocache content from your Azure storage.</span></span> <span data-ttu-id="0f9c7-105">Oferuje deweloperom globalne rozwiązanie umożliwiające dostarczanie zawartości wysokiej przepustowości przez buforowanie obiektów blob i zawartości statycznej wystąpień obliczeń w węzłach fizycznych hello USA, Europa, Azji, Australii i Ameryka Południowa.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in hello United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="0f9c7-106">Krok 1: Utwórz konto magazynu</span><span class="sxs-lookup"><span data-stu-id="0f9c7-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="0f9c7-107">Użyj hello następujące procedury toocreate nowe konto magazynu dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-107">Use hello following procedure toocreate a new storage account for a Azure subscription.</span></span> <span data-ttu-id="0f9c7-108">Konto magazynu zapewnia dostęp do usług magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="0f9c7-109">Konto magazynu Hello reprezentuje hello najwyższy poziom przestrzeń nazw hello dla uzyskiwania dostępu do poszczególnych składników usługi Magazyn Azure hello: obiektów Blob usługi, usługi kolejki i usługi tabeli.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-109">hello storage account represents hello highest level of hello namespace for accessing each of hello Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="0f9c7-110">Aby uzyskać więcej informacji, zobacz toohello [tooMicrosoft wprowadzenie usługi Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0f9c7-110">For more information, refer toohello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="0f9c7-111">toocreate konta magazynu musi być hello administrator usługi albo współadministratorem dla hello skojarzone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-111">toocreate a storage account, you must be either hello service administrator or a co-administrator for hello associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="0f9c7-112">Istnieje kilka metod, można użyć toocreate konto magazynu, w tym hello portalu Azure i programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-112">There are several methods you can use toocreate a storage account, including hello Azure Portal and Powershell.</span></span>  <span data-ttu-id="0f9c7-113">W tym samouczku będziemy używać hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-113">For this tutorial, we'll be using hello Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="0f9c7-114">**toocreate konto magazynu dla subskrypcji platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="0f9c7-114">**toocreate a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="0f9c7-115">Zaloguj się toohello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f9c7-115">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0f9c7-116">W górnym lewym rogu hello, wybierz **nowy**.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-116">In hello upper left corner, select **New**.</span></span> <span data-ttu-id="0f9c7-117">W hello **nowy** zaznacz pozycję **dane i magazyn**, następnie kliknij przycisk **konta magazynu**.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-117">In hello **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="0f9c7-118">Witaj **utworzyć konto magazynu** zostanie wyświetlony blok.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-118">hello **Create storage account** blade appears.</span></span>   

    ![Tworzenie konta magazynu][create-new-storage-account]  

3. <span data-ttu-id="0f9c7-120">W hello **nazwa** wpisz nazwę domeny podrzędnej.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-120">In hello **Name** field, type a subdomain name.</span></span> <span data-ttu-id="0f9c7-121">Ten wpis może zawierać 3 do 24 małych liter i cyfr.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="0f9c7-122">Ta wartość staje się nazwa hosta hello w hello identyfikator URI, który jest wykorzystywana do adresowania obiektów Blob, kolejki lub tabeli zasobów hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-122">This value becomes hello host name within hello URI that is used to address Blob, Queue, or Table resources for hello subscription.</span></span> <span data-ttu-id="0f9c7-123">Aby rozwiązać zasobu kontenera w hello usługa Blob, czy korzystania z identyfikatora URI hello zgodny z formatem, gdzie  *&lt;StorageAccountLabel&gt;*  odwołuje się wartość toohello wpisane w **wprowadź adres URL**:</span><span class="sxs-lookup"><span data-stu-id="0f9c7-123">To address a container resource in hello Blob service, you would use a URI in hello following format, where *&lt;StorageAccountLabel&gt;* refers toohello value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="0f9c7-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mojkontener&gt;*</span><span class="sxs-lookup"><span data-stu-id="0f9c7-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="0f9c7-125">**Ważne:** hello adresu URL etykiety formularze hello poddomeny konta magazynu hello identyfikatora URI i musi być unikatowa wśród wszystkich usług hostowanych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-125">**Important:** hello URL label forms hello subdomain of hello storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="0f9c7-126">Ta wartość jest również używana jako nazwa hello tego konta magazynu w portalu hello lub podczas uzyskiwania dostępu do tego konta programowo.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-126">This value is also used as hello name of this storage account in hello portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="0f9c7-127">Pozostaw ustawienia domyślne hello **modelu wdrażania**, **konta rodzaju**, **wydajności**, i **replikacji**.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-127">Leave hello defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="0f9c7-128">Wybierz hello **subskrypcji** czy konto magazynu hello będą używane z.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-128">Select hello **Subscription** that hello storage account will be used with.</span></span>
6. <span data-ttu-id="0f9c7-129">Wybierz lub utwórz **grupę zasobów**.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="0f9c7-130">Więcej informacji na temat grup zasobów znajduje się w temacie [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="0f9c7-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="0f9c7-131">Wybierz lokalizację dla konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="0f9c7-132">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-132">Click **Create**.</span></span> <span data-ttu-id="0f9c7-133">proces tworzenia konta magazynu hello Hello może potrwać kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-133">hello process of creating hello storage account might take several minutes toocomplete.</span></span>

## <a name="step-2-enable-cdn-for-hello-storage-account"></a><span data-ttu-id="0f9c7-134">Krok 2: Włączanie CDN dla konta magazynu hello</span><span class="sxs-lookup"><span data-stu-id="0f9c7-134">Step 2: Enable CDN for hello storage account</span></span>

<span data-ttu-id="0f9c7-135">Dzięki integracji najnowsze hello można teraz włączyć CDN dla konta magazynu bez opuszczania rozszerzenia portalu magazynu.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-135">With hello newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="0f9c7-136">Wybierz konto magazynu hello, wyszukiwanie "CDN" lub przewiń w dół menu nawigacji po lewej stronie powitania, a następnie kliknij przycisk "Azure CDN".</span><span class="sxs-lookup"><span data-stu-id="0f9c7-136">Select hello storage account, search "CDN" or scroll down from hello left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="0f9c7-137">Witaj **Azure CDN** zostanie wyświetlony blok.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-137">hello **Azure CDN** blade appears.</span></span>

    ![CDN Włącz nawigacji][cdn-enable-navigation]
    
2. <span data-ttu-id="0f9c7-139">Utwórz nowy punkt końcowy wprowadzając hello wymagane informacje</span><span class="sxs-lookup"><span data-stu-id="0f9c7-139">Create a new endpoint by entering hello required information</span></span>
    - <span data-ttu-id="0f9c7-140">**Profil CDN**: można utworzyć nowy lub użyć istniejącego profilu.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="0f9c7-141">**Warstwa cenowa**: wystarczy tooselect warstwy cenowej w przypadku utworzenia nowego profilu CDN.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-141">**Pricing tier**: You only need tooselect a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="0f9c7-142">**Nazwa punktu końcowego CDN**: Wprowadź nazwę punktu końcowego na wybór.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="0f9c7-143">punkt końcowy CDN Hello utworzona domyślnie używa hello nazwa hosta konta magazynu jako źródła.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-143">hello created CDN endpoint uses hello hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="0f9c7-144">! [tworzenie punktu końcowego cdn nowego] [cdn — nowy — utworzenie punktu końcowego]</span><span class="sxs-lookup"><span data-stu-id="0f9c7-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="0f9c7-145">Po utworzeniu nowy punkt końcowy hello będą widoczne w powyższej listy punktów końcowych hello.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-145">After creation, hello new endpoint will show up in hello endpoint list above.</span></span>

    ![nowy punkt końcowy sieci CDN w warstwie magazynu][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="0f9c7-147">Można także przejść tooAzure CDN rozszerzenia tooenable CDN. [Samouczek](#Tutorial-cdn-create-profile).</span><span class="sxs-lookup"><span data-stu-id="0f9c7-147">You can also go tooAzure CDN extension tooenable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="0f9c7-148">Krok 3: Włącz dodatkowe funkcje CDN</span><span class="sxs-lookup"><span data-stu-id="0f9c7-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="0f9c7-149">Z bloku "Azure CDN" konto magazynu kliknij punkt końcowy CDN hello z hello listy tooopen CDN konfiguracji bloku.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-149">From storage account "Azure CDN" blade, click hello CDN endpoint from hello list tooopen CDN configuration blade.</span></span> <span data-ttu-id="0f9c7-150">Można włączyć dodatkowe funkcje sieci CDN w celu dostarczania, na przykład kompresji, ciąg zapytania geograficznie filtrowania.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="0f9c7-151">Można również dodać niestandardową domenę mapowania tooyour — punkt końcowy CDN i włączyć domeny niestandardowej HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-151">You can also add custom domain mapping tooyour CDN endpoint and enable custom domain HTTPS.</span></span>
    
![Konfiguracja sieci CDN w warstwie magazynu CDN][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="0f9c7-153">Krok 4: Dostęp do zawartości w sieci CDN</span><span class="sxs-lookup"><span data-stu-id="0f9c7-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="0f9c7-154">tooaccess pamięci podręcznej zawartości na powitania CDN, użyj hello adresu CDN zawarte w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-154">tooaccess cached content on hello CDN, use hello CDN URL provided in hello portal.</span></span> <span data-ttu-id="0f9c7-155">Hello adres pamięci podręcznej blob będzie podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0f9c7-155">hello address for a cached blob will be similar toohello following:</span></span>

<span data-ttu-id="0f9c7-156">http://<*EndpointName*\>.azureedge.net/ <*myPublicContainer*\>/<*element BlobName*\></span><span class="sxs-lookup"><span data-stu-id="0f9c7-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="0f9c7-157">Po włączeniu konta magazynu tooa dostępu do sieci CDN wszystkich publicznie dostępnych obiektów kwalifikują się do buforowania krawędzi CDN.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-157">Once you enable CDN access tooa storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="0f9c7-158">Po zmodyfikowaniu obiektu, który jest aktualnie w pamięci podręcznej hello CDN hello nową zawartość nie będzie dostępne za pośrednictwem hello CDN dopóki hello CDN odświeża jego zawartości, gdy hello buforowane okres czasu wygaśnięcia zawartości.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-158">If you modify an object that is currently cached in hello CDN, hello new content will not be available via hello CDN until hello CDN refreshes its content when hello cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a><span data-ttu-id="0f9c7-159">Krok 5: Usuń zawartość z hello CDN</span><span class="sxs-lookup"><span data-stu-id="0f9c7-159">Step 5: Remove content from hello CDN</span></span>
<span data-ttu-id="0f9c7-160">Jeśli nie chcesz już toocache obiektu w hello Azure sieci dostarczania zawartości (CDN), można wykonać jedną z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0f9c7-160">If you no longer wish toocache an object in hello Azure Content Delivery Network (CDN), you can take one of hello following steps:</span></span>

* <span data-ttu-id="0f9c7-161">Możesz wprowadzić hello prywatnego kontenera zamiast publicznego.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-161">You can make hello container private instead of public.</span></span> <span data-ttu-id="0f9c7-162">Zobacz [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiekty BLOB](../storage/blobs/storage-manage-access-to-resources.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-162">See [Manage anonymous read access toocontainers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="0f9c7-163">Można wyłączyć lub usunąć punkt końcowy CDN hello przy użyciu hello portalu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-163">You can disable or delete hello CDN endpoint using hello Management Portal.</span></span>
* <span data-ttu-id="0f9c7-164">Można zmodyfikować Twojej usługi hostowanej toono dłużej odpowiedź toorequests dla obiekt hello.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-164">You can modify your hosted service toono longer respond toorequests for hello object.</span></span>

<span data-ttu-id="0f9c7-165">Obiekt w sieci CDN hello już pamięci podręcznej pozostaje w pamięci podręcznej aż do okresu hello time-to-live dla obiekt hello lub punktu końcowego hello jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-165">An object already cached in hello CDN will remain cached until hello time-to-live period for hello object expires or until hello endpoint is purged.</span></span> <span data-ttu-id="0f9c7-166">Po wygaśnięciu okresu time-to-live hello hello CDN sprawdzi toosee, czy punkt końcowy CDN hello jest nadal ważny i nadal anonimowo dostępny obiekt hello.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-166">When hello time-to-live period expires, hello CDN will check toosee whether hello CDN endpoint is still valid and hello object still anonymously accessible.</span></span> <span data-ttu-id="0f9c7-167">Jeśli nie, obiekt hello już być buforowane.</span><span class="sxs-lookup"><span data-stu-id="0f9c7-167">If it is not, then hello object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0f9c7-168">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0f9c7-168">Additional resources</span></span>
* [<span data-ttu-id="0f9c7-169">Jak tooa CDN zawartości tooMap domeny niestandardowe</span><span class="sxs-lookup"><span data-stu-id="0f9c7-169">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="0f9c7-170">Włącz protokół HTTPS dla domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="0f9c7-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
