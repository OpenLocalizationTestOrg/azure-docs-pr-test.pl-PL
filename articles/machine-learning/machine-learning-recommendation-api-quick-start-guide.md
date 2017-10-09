---
title: 'Szybki start: Azure Machine Learning zalecenia API (wersja 1) | Dokumentacja firmy Microsoft'
description: "Azure Machine Learning zalecenia — Przewodnik Szybki Start"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d8f98e85f723a1104cb169b26d797934140979f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="60532-104">Przewodnik szybkiego startu hello Machine Learning zalecenia API (wersja 1)</span><span class="sxs-lookup"><span data-stu-id="60532-104">Quick start guide for hello Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="60532-105">Należy zacząć korzystać hello [kognitywnych usługi interfejsu API zalecenia](https://www.microsoft.com/cognitive-services/recommendations-api) zamiast tej wersji.</span><span class="sxs-lookup"><span data-stu-id="60532-105">You should start using hello [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="60532-106">Hello kognitywnych usługę rekomendacji spowoduje zastąpienie tej usługi, a opracowane zostaną wszystkie hello nowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="60532-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="60532-107">Ma on nowe funkcje, takie jak przetwarzanie wsadowe pomocy technicznej, lepiej Explorer interfejsu API, czyszczący środowisko signup/rozliczeń powierzchni, bardziej spójny interfejs API,... itd.</span><span class="sxs-lookup"><span data-stu-id="60532-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="60532-108">Dowiedz się więcej o [toohello Migrowanie nową usługę kognitywnych](http://aka.ms/recomigrate).</span><span class="sxs-lookup"><span data-stu-id="60532-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="60532-109">W tym dokumencie opisano sposób tooonboard Twojego toouse aplikacji lub usługi Microsoft Azure Machine Learning zalecenia.</span><span class="sxs-lookup"><span data-stu-id="60532-109">This document describes how tooonboard your service or application toouse Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="60532-110">Więcej informacji można znaleźć na powitania zalecenia dotyczące interfejsu API w hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="60532-110">You can find more details on hello Recommendations API in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="60532-111">Ogólne omówienie</span><span class="sxs-lookup"><span data-stu-id="60532-111">General overview</span></span>
<span data-ttu-id="60532-112">toouse Azure Machine Learning zalecenia należy hello tootake następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="60532-112">toouse Azure Machine Learning Recommendations, you need tootake hello following steps:</span></span>

* <span data-ttu-id="60532-113">Tworzenie modelu — model jest kontenerem danych użycia, danych wykazu i hello zalecenie modelu.</span><span class="sxs-lookup"><span data-stu-id="60532-113">Create a model - A model is a container of your usage data, catalog data, and hello recommendation model.</span></span>
* <span data-ttu-id="60532-114">Importuj dane katalogu - katalogu zawiera informacje metadanych na powitania elementów.</span><span class="sxs-lookup"><span data-stu-id="60532-114">Import catalog data - A catalog contains metadata information on hello items.</span></span> 
* <span data-ttu-id="60532-115">Importowanie danych użycia - dane użycia mogą być przekazywane w jeden z dwóch sposobów (lub obie):</span><span class="sxs-lookup"><span data-stu-id="60532-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="60532-116">Przekazując plik zawierający dane użycia hello.</span><span class="sxs-lookup"><span data-stu-id="60532-116">By uploading a file that contains hello usage data.</span></span>
  * <span data-ttu-id="60532-117">Wysyła zdarzenia pozyskiwania danych.</span><span class="sxs-lookup"><span data-stu-id="60532-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="60532-118">Zazwyczaj Przekaż plik użycia w stanie toocreate toobe kolejność modelu zalecenie początkowego (bootstrap) i go używać, dopóki hello system zbiera wystarczającej ilości danych przy użyciu formatu pozyskiwania danych hello.</span><span class="sxs-lookup"><span data-stu-id="60532-118">Usually you upload a usage file in order toobe able toocreate an initial recommendation model (bootstrap) and use it until hello system gathers enough data by using hello data acquisition format.</span></span>
* <span data-ttu-id="60532-119">Tworzenie modelu zalecenie — jest to operacja asynchroniczna, w których hello systemu zalecenie pobiera wszystkie dane użycia hello i tworzy model zalecenia.</span><span class="sxs-lookup"><span data-stu-id="60532-119">Build a recommendation model - This is an asynchronous operation in which hello recommendation system takes all hello usage data and creates a recommendation model.</span></span> <span data-ttu-id="60532-120">Ta operacja może potrwać kilka minut lub kilka godzin w zależności od hello rozmiar danych hello i hello kompilacji parametry konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="60532-120">This operation can take several minutes or several hours depending on hello size of hello data and hello build configuration parameters.</span></span> <span data-ttu-id="60532-121">W przypadku wyzwalają hello kompilacji, otrzyma identyfikatora dla kompilacji.</span><span class="sxs-lookup"><span data-stu-id="60532-121">When triggering hello build, you will get a build ID.</span></span> <span data-ttu-id="60532-122">Służy on toocheck podczas procesu kompilacji hello zakończyła się przed rozpoczęciem tooconsume zalecenia.</span><span class="sxs-lookup"><span data-stu-id="60532-122">Use it toocheck when hello build process has ended before starting tooconsume recommendations.</span></span>
* <span data-ttu-id="60532-123">Używać zalecenia - Get zalecenia dotyczące określonego elementu lub listy elementów.</span><span class="sxs-lookup"><span data-stu-id="60532-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="60532-124">Wszystkie powyższe kroki hello są realizowane za pomocą hello Azure Machine Learning zalecenia API.</span><span class="sxs-lookup"><span data-stu-id="60532-124">All hello steps above are done through hello Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="60532-125">Możesz pobrać przykładowej aplikacji, która implementuje każdy z tych kroków z hello [również galerii.](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="60532-125">You can download a sample application that implements each of these steps from hello [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="60532-126">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="60532-126">Limitations</span></span>
* <span data-ttu-id="60532-127">Maksymalna liczba modeli na subskrypcję Hello wynosi 10.</span><span class="sxs-lookup"><span data-stu-id="60532-127">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="60532-128">Hello maksymalną liczbę elementów, które mogą zawierać wykaz wynosi 100 000.</span><span class="sxs-lookup"><span data-stu-id="60532-128">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="60532-129">Maksymalna liczba punktów użycia, które są zachowane w Hello jest ~ 5,000,000.</span><span class="sxs-lookup"><span data-stu-id="60532-129">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="60532-130">Hello najstarsze zostanie usunięte, gdy nowe zostanie przekazany lub zgłaszane.</span><span class="sxs-lookup"><span data-stu-id="60532-130">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="60532-131">Maksymalny rozmiar danych, które mogą być wysyłane w POST (na przykład importu wykazu danych, importowanie danych użycia) Hello jest 200MB.</span><span class="sxs-lookup"><span data-stu-id="60532-131">hello maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="60532-132">Witaj liczba transakcji na sekundę dla kompilacji modelu zalecenie, która nie jest aktywny jest ~ 2TPS.</span><span class="sxs-lookup"><span data-stu-id="60532-132">hello number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="60532-133">Zalecenie kompilacji modelu, który jest aktywny, przytrzymując się too20TPS.</span><span class="sxs-lookup"><span data-stu-id="60532-133">A recommendation model build that is active can hold up too20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="60532-134">Integracja</span><span class="sxs-lookup"><span data-stu-id="60532-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="60532-135">Authentication</span><span class="sxs-lookup"><span data-stu-id="60532-135">Authentication</span></span>
<span data-ttu-id="60532-136">Microsoft Azure Marketplace obsługuje albo hello metody uwierzytelniania podstawowego lub uwierzytelniania OAuth.</span><span class="sxs-lookup"><span data-stu-id="60532-136">Microsoft Azure Marketplace supports either hello Basic or OAuth authentication method.</span></span> <span data-ttu-id="60532-137">Klucze konta hello można łatwo znaleźć przechodząc toohello klucze w witrynie marketplace hello w obszarze [ustawienia konta](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="60532-137">You can easily find hello account keys by navigating toohello keys in hello marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="60532-138">Uwierzytelnianie podstawowe</span><span class="sxs-lookup"><span data-stu-id="60532-138">Basic Authentication</span></span>
<span data-ttu-id="60532-139">Dodaj nagłówek autoryzacji hello:</span><span class="sxs-lookup"><span data-stu-id="60532-139">Add hello Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="60532-140">Konwertuj tooBase64 (C#)</span><span class="sxs-lookup"><span data-stu-id="60532-140">Convert tooBase64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="60532-141">Konwertuj tooBase64 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="60532-141">Convert tooBase64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="60532-142">Identyfikator URI usługi</span><span class="sxs-lookup"><span data-stu-id="60532-142">Service URI</span></span>
<span data-ttu-id="60532-143">główny usługi Hello identyfikatora URI dla interfejsów API usługi Azure Machine Learning zalecenia hello jest [tutaj.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="60532-143">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="60532-144">Identyfikator URI usługi pełne Hello jest wyrażona za pomocą elementów hello specyfikację OData.</span><span class="sxs-lookup"><span data-stu-id="60532-144">hello full service URI is expressed using elements of hello OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="60532-145">Wersja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="60532-145">API version</span></span>
<span data-ttu-id="60532-146">Każde wywołanie interfejsu API ma na końcu hello parametr zapytania o nazwie apiVersion, która powinna być ustawiona zbyt "1.0".</span><span class="sxs-lookup"><span data-stu-id="60532-146">Each API call will have, at hello end, a query parameter called apiVersion that should be set too"1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="60532-147">Identyfikatory jest rozróżniana wielkość liter</span><span class="sxs-lookup"><span data-stu-id="60532-147">IDs are case-sensitive</span></span>
<span data-ttu-id="60532-148">Identyfikatory zwrócony przez żadnego z interfejsów API, hello jest rozróżniana wielkość liter i powinien być używany jako takie, gdy dane są przekazywane jako parametry w kolejnych wywołaniach interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="60532-148">IDs, returned by any of hello APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="60532-149">Na przykład identyfikatory modelu i identyfikatory katalogu jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="60532-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="60532-150">Tworzenie modelu</span><span class="sxs-lookup"><span data-stu-id="60532-150">Create a model</span></span>
<span data-ttu-id="60532-151">Tworzenie żądania "Tworzenie modelu":</span><span class="sxs-lookup"><span data-stu-id="60532-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="60532-152">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="60532-152">HTTP Method</span></span> | <span data-ttu-id="60532-153">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="60532-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="60532-154">POST</span><span class="sxs-lookup"><span data-stu-id="60532-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="60532-155">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60532-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="60532-156">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="60532-156">Parameter Name</span></span> | <span data-ttu-id="60532-157">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="60532-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="60532-158">modelName</span><span class="sxs-lookup"><span data-stu-id="60532-158">modelName</span></span> |<span data-ttu-id="60532-159">Tylko litery (A-Z, a – z), cyfry (0 – 9), łączniki (-) i znak podkreślenia (_) są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="60532-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="60532-160">Maksymalna długość: 20</span><span class="sxs-lookup"><span data-stu-id="60532-160">Max length: 20</span></span> |
| <span data-ttu-id="60532-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="60532-161">apiVersion</span></span> |<span data-ttu-id="60532-162">1.0</span><span class="sxs-lookup"><span data-stu-id="60532-162">1.0</span></span> |
|  | |
| <span data-ttu-id="60532-163">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="60532-163">Request Body</span></span> |<span data-ttu-id="60532-164">BRAK</span><span class="sxs-lookup"><span data-stu-id="60532-164">NONE</span></span> |

<span data-ttu-id="60532-165">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="60532-165">**Response**:</span></span>

<span data-ttu-id="60532-166">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="60532-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="60532-167">`feed/entry/content/properties/id`-Zawiera identyfikator hello modelu.</span><span class="sxs-lookup"><span data-stu-id="60532-167">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="60532-168">Należy pamiętać, że identyfikator modelu hello jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="60532-168">Note that hello model ID is case-sensitive.</span></span>

<span data-ttu-id="60532-169">OData XML</span><span class="sxs-lookup"><span data-stu-id="60532-169">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-catalog-data"></a><span data-ttu-id="60532-170">Importuj dane katalogu</span><span class="sxs-lookup"><span data-stu-id="60532-170">Import catalog data</span></span>
<span data-ttu-id="60532-171">Po wysłaniu kilka katalogu plików toohello sam model z kilka wywołań możemy zostanie wstawiona tylko hello nowych elementów katalogu.</span><span class="sxs-lookup"><span data-stu-id="60532-171">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="60532-172">Istniejące elementy pozostanie z hello oryginalnych wartości.</span><span class="sxs-lookup"><span data-stu-id="60532-172">Existing items will remain with hello original values.</span></span>

| <span data-ttu-id="60532-173">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="60532-173">HTTP Method</span></span> | <span data-ttu-id="60532-174">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="60532-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="60532-175">POST</span><span class="sxs-lookup"><span data-stu-id="60532-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="60532-176">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60532-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="60532-177">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="60532-177">Parameter Name</span></span> | <span data-ttu-id="60532-178">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="60532-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="60532-179">modelId</span><span class="sxs-lookup"><span data-stu-id="60532-179">modelId</span></span> |<span data-ttu-id="60532-180">Unikatowy identyfikator modelu hello (z uwzględnieniem wielkości liter)</span><span class="sxs-lookup"><span data-stu-id="60532-180">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="60532-181">Nazwa pliku</span><span class="sxs-lookup"><span data-stu-id="60532-181">filename</span></span> |<span data-ttu-id="60532-182">Identyfikator tekstową hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="60532-182">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="60532-183">Tylko litery (A-Z, a – z), cyfry (0 – 9), łączniki (-) i znak podkreślenia (_) są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="60532-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="60532-184">Długość maksymalna: 50</span><span class="sxs-lookup"><span data-stu-id="60532-184">Max length: 50</span></span> |
| <span data-ttu-id="60532-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="60532-185">apiVersion</span></span> |<span data-ttu-id="60532-186">1.0</span><span class="sxs-lookup"><span data-stu-id="60532-186">1.0</span></span> |
|  | |
| <span data-ttu-id="60532-187">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="60532-187">Request Body</span></span> |<span data-ttu-id="60532-188">Wykazu danych.</span><span class="sxs-lookup"><span data-stu-id="60532-188">Catalog data.</span></span> <span data-ttu-id="60532-189">Format:</span><span class="sxs-lookup"><span data-stu-id="60532-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="60532-190">Nazwa</span><span class="sxs-lookup"><span data-stu-id="60532-190">Name</span></span></th><th><span data-ttu-id="60532-191">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="60532-191">Mandatory</span></span></th><th><span data-ttu-id="60532-192">Typ</span><span class="sxs-lookup"><span data-stu-id="60532-192">Type</span></span></th><th><span data-ttu-id="60532-193">Opis</span><span class="sxs-lookup"><span data-stu-id="60532-193">Description</span></span></th></tr><tr><td><span data-ttu-id="60532-194">Identyfikator elementu</span><span class="sxs-lookup"><span data-stu-id="60532-194">Item Id</span></span></td><td><span data-ttu-id="60532-195">Tak</span><span class="sxs-lookup"><span data-stu-id="60532-195">Yes</span></span></td><td><span data-ttu-id="60532-196">Alfanumeryczne, maksymalna długość 50</span><span class="sxs-lookup"><span data-stu-id="60532-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="60532-197">Unikatowy identyfikator elementu</span><span class="sxs-lookup"><span data-stu-id="60532-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="60532-198">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="60532-198">Item Name</span></span></td><td><span data-ttu-id="60532-199">Tak</span><span class="sxs-lookup"><span data-stu-id="60532-199">Yes</span></span></td><td><span data-ttu-id="60532-200">Alfanumeryczne, maksymalną długość 255 znaków</span><span class="sxs-lookup"><span data-stu-id="60532-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="60532-201">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="60532-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="60532-202">Kategoria elementu</span><span class="sxs-lookup"><span data-stu-id="60532-202">Item Category</span></span></td><td><span data-ttu-id="60532-203">Tak</span><span class="sxs-lookup"><span data-stu-id="60532-203">Yes</span></span></td><td><span data-ttu-id="60532-204">Alfanumeryczne, maksymalną długość 255 znaków</span><span class="sxs-lookup"><span data-stu-id="60532-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="60532-205">Toowhich kategorii, której ten element należy (na przykład gotowania książek teatralne...)</span><span class="sxs-lookup"><span data-stu-id="60532-205">Category toowhich this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="60532-206">Opis</span><span class="sxs-lookup"><span data-stu-id="60532-206">Description</span></span></td><td><span data-ttu-id="60532-207">Nie</span><span class="sxs-lookup"><span data-stu-id="60532-207">No</span></span></td><td><span data-ttu-id="60532-208">Alfanumeryczne, maksymalna długość 4000</span><span class="sxs-lookup"><span data-stu-id="60532-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="60532-209">Opis tego elementu</span><span class="sxs-lookup"><span data-stu-id="60532-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="60532-210">Maksymalny rozmiar pliku to 200MB.</span><span class="sxs-lookup"><span data-stu-id="60532-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="60532-211">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60532-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="60532-212">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="60532-212">**Response**:</span></span>

<span data-ttu-id="60532-213">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="60532-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="60532-214">`Feed\entry\content\properties\LineCount`— Zaakceptowano liczba wierszy.</span><span class="sxs-lookup"><span data-stu-id="60532-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="60532-215">`Feed\entry\content\properties\ErrorCount`-Liczba wierszy, które nie zostały wstawione ze względu na błąd tooan.</span><span class="sxs-lookup"><span data-stu-id="60532-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="60532-216">OData XML</span><span class="sxs-lookup"><span data-stu-id="60532-216">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a><span data-ttu-id="60532-217">Importowanie danych użycia</span><span class="sxs-lookup"><span data-stu-id="60532-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="60532-218">Przekazywanie pliku</span><span class="sxs-lookup"><span data-stu-id="60532-218">Uploading a file</span></span>
<span data-ttu-id="60532-219">W tej sekcji przedstawiono sposób tooupload dane użycia przy użyciu pliku.</span><span class="sxs-lookup"><span data-stu-id="60532-219">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="60532-220">Można wywołać tego interfejsu API z danych użycia.</span><span class="sxs-lookup"><span data-stu-id="60532-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="60532-221">Wszystkie dane użycia są zapisywane dla wszystkich wywołań.</span><span class="sxs-lookup"><span data-stu-id="60532-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="60532-222">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="60532-222">HTTP Method</span></span> | <span data-ttu-id="60532-223">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="60532-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="60532-224">POST</span><span class="sxs-lookup"><span data-stu-id="60532-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="60532-225">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60532-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="60532-226">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="60532-226">Parameter Name</span></span> | <span data-ttu-id="60532-227">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="60532-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="60532-228">modelId</span><span class="sxs-lookup"><span data-stu-id="60532-228">modelId</span></span> |<span data-ttu-id="60532-229">Unikatowy identyfikator modelu hello (z uwzględnieniem wielkości liter)</span><span class="sxs-lookup"><span data-stu-id="60532-229">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="60532-230">Nazwa pliku</span><span class="sxs-lookup"><span data-stu-id="60532-230">filename</span></span> |<span data-ttu-id="60532-231">Identyfikator tekstową hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="60532-231">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="60532-232">Tylko litery (A-Z, a – z), cyfry (0 – 9), łączniki (-) i znak podkreślenia (_) są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="60532-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="60532-233">Długość maksymalna: 50</span><span class="sxs-lookup"><span data-stu-id="60532-233">Max length: 50</span></span> |
| <span data-ttu-id="60532-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="60532-234">apiVersion</span></span> |<span data-ttu-id="60532-235">1.0</span><span class="sxs-lookup"><span data-stu-id="60532-235">1.0</span></span> |
|  | |
| <span data-ttu-id="60532-236">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="60532-236">Request Body</span></span> |<span data-ttu-id="60532-237">Dane użycia.</span><span class="sxs-lookup"><span data-stu-id="60532-237">Usage data.</span></span> <span data-ttu-id="60532-238">Format:</span><span class="sxs-lookup"><span data-stu-id="60532-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="60532-239">Nazwa</span><span class="sxs-lookup"><span data-stu-id="60532-239">Name</span></span></th><th><span data-ttu-id="60532-240">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="60532-240">Mandatory</span></span></th><th><span data-ttu-id="60532-241">Typ</span><span class="sxs-lookup"><span data-stu-id="60532-241">Type</span></span></th><th><span data-ttu-id="60532-242">Opis</span><span class="sxs-lookup"><span data-stu-id="60532-242">Description</span></span></th></tr><tr><td><span data-ttu-id="60532-243">Identyfikator użytkownika</span><span class="sxs-lookup"><span data-stu-id="60532-243">User Id</span></span></td><td><span data-ttu-id="60532-244">Tak</span><span class="sxs-lookup"><span data-stu-id="60532-244">Yes</span></span></td><td><span data-ttu-id="60532-245">Alfanumeryczne</span><span class="sxs-lookup"><span data-stu-id="60532-245">Alphanumeric</span></span></td><td><span data-ttu-id="60532-246">Unikatowy identyfikator użytkownika</span><span class="sxs-lookup"><span data-stu-id="60532-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="60532-247">Identyfikator elementu</span><span class="sxs-lookup"><span data-stu-id="60532-247">Item Id</span></span></td><td><span data-ttu-id="60532-248">Tak</span><span class="sxs-lookup"><span data-stu-id="60532-248">Yes</span></span></td><td><span data-ttu-id="60532-249">Alfanumeryczne, maksymalna długość 50</span><span class="sxs-lookup"><span data-stu-id="60532-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="60532-250">Unikatowy identyfikator elementu</span><span class="sxs-lookup"><span data-stu-id="60532-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="60532-251">Time</span><span class="sxs-lookup"><span data-stu-id="60532-251">Time</span></span></td><td><span data-ttu-id="60532-252">Nie</span><span class="sxs-lookup"><span data-stu-id="60532-252">No</span></span></td><td><span data-ttu-id="60532-253">Data w formacie: RRRR/MM/ddtgg (na przykład 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="60532-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="60532-254">Czas danych</span><span class="sxs-lookup"><span data-stu-id="60532-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="60532-255">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="60532-255">Event</span></span></td><td><span data-ttu-id="60532-256">Nie, jeśli podane, również umieścić daty</span><span class="sxs-lookup"><span data-stu-id="60532-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="60532-257">Jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="60532-257">One of hello following:</span></span><br><span data-ttu-id="60532-258">• Kliknij przycisk</span><span class="sxs-lookup"><span data-stu-id="60532-258">• Click</span></span><br><span data-ttu-id="60532-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="60532-259">• RecommendationClick</span></span><br><span data-ttu-id="60532-260">• AddShopCart</span><span class="sxs-lookup"><span data-stu-id="60532-260">•    AddShopCart</span></span><br><span data-ttu-id="60532-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="60532-261">• RemoveShopCart</span></span><br><span data-ttu-id="60532-262">• Zakupu</span><span class="sxs-lookup"><span data-stu-id="60532-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="60532-263">Maksymalny rozmiar pliku to 200MB.</span><span class="sxs-lookup"><span data-stu-id="60532-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="60532-264">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60532-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="60532-265">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="60532-265">**Response**:</span></span>

<span data-ttu-id="60532-266">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="60532-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="60532-267">`Feed\entry\content\properties\LineCount`— Zaakceptowano liczba wierszy.</span><span class="sxs-lookup"><span data-stu-id="60532-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="60532-268">`Feed\entry\content\properties\ErrorCount`-Liczba wierszy, które nie zostały wstawione ze względu na błąd tooan.</span><span class="sxs-lookup"><span data-stu-id="60532-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="60532-269">`Feed\entry\content\properties\FileId`— Identyfikator pliku.</span><span class="sxs-lookup"><span data-stu-id="60532-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="60532-270">OData XML</span><span class="sxs-lookup"><span data-stu-id="60532-270">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a><span data-ttu-id="60532-271">Przy użyciu danych</span><span class="sxs-lookup"><span data-stu-id="60532-271">Using data acquisition</span></span>
<span data-ttu-id="60532-272">W tej sekcji przedstawiono, jak zdarzenia toosend w rzeczywistym czasu tooAzure Machine Learning zalecenia, zazwyczaj z witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="60532-272">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="60532-273">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="60532-273">HTTP Method</span></span> | <span data-ttu-id="60532-274">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="60532-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="60532-275">POST</span><span class="sxs-lookup"><span data-stu-id="60532-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="60532-276">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="60532-276">Parameter Name</span></span> | <span data-ttu-id="60532-277">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="60532-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="60532-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="60532-278">apiVersion</span></span> |<span data-ttu-id="60532-279">1.0</span><span class="sxs-lookup"><span data-stu-id="60532-279">1.0</span></span> |
|  | |
| <span data-ttu-id="60532-280">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="60532-280">Request body</span></span> |<span data-ttu-id="60532-281">Wprowadzanie danych zdarzeń dla każdego zdarzenia mają toosend.</span><span class="sxs-lookup"><span data-stu-id="60532-281">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="60532-282">Należy wysłać dla hello tej samej sesji użytkownika lub przeglądarki hello tym samym identyfikatorze hello SessionId pola.</span><span class="sxs-lookup"><span data-stu-id="60532-282">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="60532-283">(Zobacz przykład treści zdarzenia poniżej).</span><span class="sxs-lookup"><span data-stu-id="60532-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="60532-284">Przykład dla zdarzenia "Kliknij przycisk":</span><span class="sxs-lookup"><span data-stu-id="60532-284">Example for event 'Click':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="60532-285">Przykład dla zdarzenia "RecommendationClick":</span><span class="sxs-lookup"><span data-stu-id="60532-285">Example for event 'RecommendationClick':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="60532-286">Przykład dla zdarzenia "AddShopCart":</span><span class="sxs-lookup"><span data-stu-id="60532-286">Example for event 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="60532-287">Przykład dla zdarzenia "RemoveShopCart":</span><span class="sxs-lookup"><span data-stu-id="60532-287">Example for event 'RemoveShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RemoveShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="60532-288">Przykład dla zdarzenia "Zakupu":</span><span class="sxs-lookup"><span data-stu-id="60532-288">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="60532-289">Przykład wysyłania 2 zdarzenia "kliknij" a "AddShopCart":</span><span class="sxs-lookup"><span data-stu-id="60532-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

<span data-ttu-id="60532-290">**Odpowiedź**: kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="60532-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="60532-291">Tworzenie modelu zalecenia</span><span class="sxs-lookup"><span data-stu-id="60532-291">Build a recommendation model</span></span>
| <span data-ttu-id="60532-292">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="60532-292">HTTP Method</span></span> | <span data-ttu-id="60532-293">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="60532-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="60532-294">POST</span><span class="sxs-lookup"><span data-stu-id="60532-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="60532-295">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60532-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="60532-296">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="60532-296">Parameter Name</span></span> | <span data-ttu-id="60532-297">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="60532-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="60532-298">modelId</span><span class="sxs-lookup"><span data-stu-id="60532-298">modelId</span></span> |<span data-ttu-id="60532-299">Unikatowy identyfikator modelu hello (z uwzględnieniem wielkości liter)</span><span class="sxs-lookup"><span data-stu-id="60532-299">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="60532-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="60532-300">userDescription</span></span> |<span data-ttu-id="60532-301">Identyfikator tekstową hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="60532-301">Textual identifier of hello catalog.</span></span> <span data-ttu-id="60532-302">Należy zwrócić uwagę, jeśli używasz spacje musi kodowanie go % 20 zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="60532-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="60532-303">Zobacz przykład powyżej.</span><span class="sxs-lookup"><span data-stu-id="60532-303">See example above.</span></span><br><span data-ttu-id="60532-304">Długość maksymalna: 50</span><span class="sxs-lookup"><span data-stu-id="60532-304">Max length: 50</span></span> |
| <span data-ttu-id="60532-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="60532-305">apiVersion</span></span> |<span data-ttu-id="60532-306">1.0</span><span class="sxs-lookup"><span data-stu-id="60532-306">1.0</span></span> |
|  | |
| <span data-ttu-id="60532-307">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="60532-307">Request Body</span></span> |<span data-ttu-id="60532-308">BRAK</span><span class="sxs-lookup"><span data-stu-id="60532-308">NONE</span></span> |

<span data-ttu-id="60532-309">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="60532-309">**Response**:</span></span>

<span data-ttu-id="60532-310">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="60532-310">HTTP Status code: 200</span></span>

<span data-ttu-id="60532-311">Jest to interfejs API asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="60532-311">This is an asynchronous API.</span></span> <span data-ttu-id="60532-312">Otrzymasz identyfikator kompilacji w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="60532-312">You will get a build ID as a response.</span></span> <span data-ttu-id="60532-313">tooknow po zakończeniu kompilacji hello, należy wywołać interfejs API "Pobierz kompilacje stan modelu" hello i zlokalizuj identyfikator to kompilacji w hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="60532-313">tooknow when hello build has ended, you should call hello "Get Builds Status of a Model" API and locate this build ID in hello response.</span></span> <span data-ttu-id="60532-314">Należy pamiętać, że kompilacja może trwać od toohours minut w zależności od wielkości hello hello danych.</span><span class="sxs-lookup"><span data-stu-id="60532-314">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="60532-315">Nie można używać zalecenia, dopóki hello kompilacji kończy się.</span><span class="sxs-lookup"><span data-stu-id="60532-315">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="60532-316">Stan prawidłowy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="60532-316">Valid build status:</span></span>

* <span data-ttu-id="60532-317">Utwórz — Model został utworzony.</span><span class="sxs-lookup"><span data-stu-id="60532-317">Create – Model was created.</span></span>
* <span data-ttu-id="60532-318">W kolejce — zostało wyzwolone kompilacji modelu i jest w kolejce.</span><span class="sxs-lookup"><span data-stu-id="60532-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="60532-319">Kompilowanie — Model została skompilowana.</span><span class="sxs-lookup"><span data-stu-id="60532-319">Building – Model is being built.</span></span>
* <span data-ttu-id="60532-320">Powodzenie — kompilacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="60532-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="60532-321">Błąd — Kompilacja została zakończona z błędem.</span><span class="sxs-lookup"><span data-stu-id="60532-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="60532-322">Anulowane — Kompilacja została anulowana.</span><span class="sxs-lookup"><span data-stu-id="60532-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="60532-323">Anulowanie — Kompilacja została anulowana.</span><span class="sxs-lookup"><span data-stu-id="60532-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="60532-324">Należy zwrócić uwagę tej kompilacji hello identyfikator można znaleźć pod ścieżką hello:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="60532-324">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="60532-325">OData XML</span><span class="sxs-lookup"><span data-stu-id="60532-325">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="60532-326">Pobierz stan kompilacji modelu</span><span class="sxs-lookup"><span data-stu-id="60532-326">Get build status of a model</span></span>
| <span data-ttu-id="60532-327">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="60532-327">HTTP Method</span></span> | <span data-ttu-id="60532-328">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="60532-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="60532-329">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="60532-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="60532-330">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60532-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="60532-331">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="60532-331">Parameter Name</span></span> | <span data-ttu-id="60532-332">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="60532-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="60532-333">modelId</span><span class="sxs-lookup"><span data-stu-id="60532-333">modelId</span></span> |<span data-ttu-id="60532-334">Unikatowy identyfikator modelu hello (z uwzględnieniem wielkości liter)</span><span class="sxs-lookup"><span data-stu-id="60532-334">Unique identifier of hello model  (case-sensitive)</span></span> |
| <span data-ttu-id="60532-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="60532-335">onlyLastBuild</span></span> |<span data-ttu-id="60532-336">Wskazuje, czy wszystkie hello tooreturn kompilacji tylko stan hello hello ostatniej kompilacji lub historii hello modelu.</span><span class="sxs-lookup"><span data-stu-id="60532-336">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="60532-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="60532-337">apiVersion</span></span> |<span data-ttu-id="60532-338">1.0</span><span class="sxs-lookup"><span data-stu-id="60532-338">1.0</span></span> |

<span data-ttu-id="60532-339">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="60532-339">**Response**:</span></span>

<span data-ttu-id="60532-340">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="60532-340">HTTP Status code: 200</span></span>

<span data-ttu-id="60532-341">odpowiedź Hello zawiera jednego wpisu na kompilacji.</span><span class="sxs-lookup"><span data-stu-id="60532-341">hello response includes one entry per build.</span></span> <span data-ttu-id="60532-342">Każdy wpis ma hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="60532-342">Each entry has hello following data:</span></span>

* <span data-ttu-id="60532-343">`feed/entry/content/properties/UserName`— Nazwa użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="60532-343">`feed/entry/content/properties/UserName` – Name of hello user.</span></span>
* <span data-ttu-id="60532-344">`feed/entry/content/properties/ModelName`— Nazwa hello modelu.</span><span class="sxs-lookup"><span data-stu-id="60532-344">`feed/entry/content/properties/ModelName` – Name of hello model.</span></span>
* <span data-ttu-id="60532-345">`feed/entry/content/properties/ModelId`— Unikatowy identyfikator modelu.</span><span class="sxs-lookup"><span data-stu-id="60532-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="60532-346">`feed/entry/content/properties/IsDeployed`— Czy kompilacja hello jest wdrożona ()</span><span class="sxs-lookup"><span data-stu-id="60532-346">`feed/entry/content/properties/IsDeployed` – Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="60532-347">aktywne kompilacji).</span><span class="sxs-lookup"><span data-stu-id="60532-347">active build).</span></span>
* <span data-ttu-id="60532-348">`feed/entry/content/properties/BuildId`— Unikatowy identyfikator kompilacji.</span><span class="sxs-lookup"><span data-stu-id="60532-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="60532-349">`feed/entry/content/properties/BuildType`— Typ hello kompilacji.</span><span class="sxs-lookup"><span data-stu-id="60532-349">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="60532-350">`feed/entry/content/properties/Status`— Stan kompilacji.</span><span class="sxs-lookup"><span data-stu-id="60532-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="60532-351">Może być jedną z następujących hello: błąd, kompilowanie, w kolejce, Cancelling anulowane, Powodzenie</span><span class="sxs-lookup"><span data-stu-id="60532-351">Can be one of hello following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="60532-352">`feed/entry/content/properties/StatusMessage`— Komunikat o stanie szczegółowe (dotyczy tylko Stany toospecific).</span><span class="sxs-lookup"><span data-stu-id="60532-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="60532-353">`feed/entry/content/properties/Progress`— Utwórz postępu (%).</span><span class="sxs-lookup"><span data-stu-id="60532-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="60532-354">`feed/entry/content/properties/StartTime`— Godzina rozpoczęcia kompilacji.</span><span class="sxs-lookup"><span data-stu-id="60532-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="60532-355">`feed/entry/content/properties/EndTime`— Czas zakończenia kompilacji.</span><span class="sxs-lookup"><span data-stu-id="60532-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="60532-356">`feed/entry/content/properties/ExecutionTime`— Czas trwania kompilacji.</span><span class="sxs-lookup"><span data-stu-id="60532-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="60532-357">`feed/entry/content/properties/ProgressStep`— Szczegółowe informacje o hello bieżący etap należącego do kompilacji w toku.</span><span class="sxs-lookup"><span data-stu-id="60532-357">`feed/entry/content/properties/ProgressStep` – Details about hello current stage that a build in progress is in.</span></span>

<span data-ttu-id="60532-358">Stan prawidłowy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="60532-358">Valid build status:</span></span>

* <span data-ttu-id="60532-359">Utworzono — wpis żądanie kompilacji zostało utworzone.</span><span class="sxs-lookup"><span data-stu-id="60532-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="60532-360">W kolejce — żądanie kompilacji zostało wyzwolone i jest w kolejce.</span><span class="sxs-lookup"><span data-stu-id="60532-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="60532-361">Kompilowanie — kompilacji jest w toku.</span><span class="sxs-lookup"><span data-stu-id="60532-361">Building – Build is in process.</span></span>
* <span data-ttu-id="60532-362">Powodzenie — kompilacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="60532-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="60532-363">Błąd — Kompilacja została zakończona z błędem.</span><span class="sxs-lookup"><span data-stu-id="60532-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="60532-364">Anulowane — Kompilacja została anulowana.</span><span class="sxs-lookup"><span data-stu-id="60532-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="60532-365">Anulowanie — Kompilacja została anulowana.</span><span class="sxs-lookup"><span data-stu-id="60532-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="60532-366">Prawidłowe wartości dla typu kompilacji:</span><span class="sxs-lookup"><span data-stu-id="60532-366">Valid values for build type:</span></span>

* <span data-ttu-id="60532-367">Ranga - rangę kompilacji.</span><span class="sxs-lookup"><span data-stu-id="60532-367">Rank - Rank build.</span></span> <span data-ttu-id="60532-368">(Rank kompilacji szczegółowe informacje, można znaleźć w dokumencie "Machine Learning zalecenie interfejsu API dokumentacji" toohello).</span><span class="sxs-lookup"><span data-stu-id="60532-368">(For rank build details, please refer toohello "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="60532-369">Zalecenie - zalecenie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="60532-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="60532-370">Zmianie wysokości progów - zakupione razem często kompilacji.</span><span class="sxs-lookup"><span data-stu-id="60532-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="60532-371">OData XML</span><span class="sxs-lookup"><span data-stu-id="60532-371">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
        <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
        <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
        <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
        <d:BuildId m:type="Edm.String">1000272</d:BuildId>
        <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
        <d:Status m:type="Edm.String">Success</d:Status>
        <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
        <d:Progress m:type="Edm.String">0</d:Progress>
        <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
        <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
        <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
        <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
        <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
      </m:properties>
     </content>
    </entry>
    </feed>


### <a name="get-recommendations"></a><span data-ttu-id="60532-372">Uzyskaj zalecenia</span><span class="sxs-lookup"><span data-stu-id="60532-372">Get recommendations</span></span>
| <span data-ttu-id="60532-373">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="60532-373">HTTP Method</span></span> | <span data-ttu-id="60532-374">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="60532-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="60532-375">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="60532-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="60532-376">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60532-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="60532-377">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="60532-377">Parameter Name</span></span> | <span data-ttu-id="60532-378">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="60532-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="60532-379">modelId</span><span class="sxs-lookup"><span data-stu-id="60532-379">modelId</span></span> |<span data-ttu-id="60532-380">Unikatowy identyfikator modelu hello (z uwzględnieniem wielkości liter)</span><span class="sxs-lookup"><span data-stu-id="60532-380">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="60532-381">identyfikatory elementów</span><span class="sxs-lookup"><span data-stu-id="60532-381">itemIds</span></span> |<span data-ttu-id="60532-382">Rozdzielana przecinkami lista hello elementów toorecommend dla.</span><span class="sxs-lookup"><span data-stu-id="60532-382">Comma-separated list of hello items toorecommend for.</span></span><br><span data-ttu-id="60532-383">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="60532-383">Max length: 1024</span></span> |
| <span data-ttu-id="60532-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="60532-384">numberOfResults</span></span> |<span data-ttu-id="60532-385">Liczba wymaganych wyników</span><span class="sxs-lookup"><span data-stu-id="60532-385">Number of required results</span></span> |
| <span data-ttu-id="60532-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="60532-386">includeMetatadata</span></span> |<span data-ttu-id="60532-387">Użycia w przyszłości, zawsze false</span><span class="sxs-lookup"><span data-stu-id="60532-387">Future use, always false</span></span> |
| <span data-ttu-id="60532-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="60532-388">apiVersion</span></span> |<span data-ttu-id="60532-389">1.0</span><span class="sxs-lookup"><span data-stu-id="60532-389">1.0</span></span> |

<span data-ttu-id="60532-390">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="60532-390">**Response:**</span></span>

<span data-ttu-id="60532-391">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="60532-391">HTTP Status code: 200</span></span>

<span data-ttu-id="60532-392">odpowiedź Hello zawiera jeden wpis dla każdego elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="60532-392">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="60532-393">Każdy wpis ma hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="60532-393">Each entry has hello following data:</span></span>

* <span data-ttu-id="60532-394">`Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="60532-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="60532-395">`Feed\entry\content\properties\Name`-Nazwa elementu hello.</span><span class="sxs-lookup"><span data-stu-id="60532-395">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="60532-396">`Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.</span><span class="sxs-lookup"><span data-stu-id="60532-396">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="60532-397">`Feed\entry\content\properties\Reasoning`-Zalecenie rozsądkiem (na przykład zalecenie wyjaśnienia).</span><span class="sxs-lookup"><span data-stu-id="60532-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="60532-398">OData XML</span><span class="sxs-lookup"><span data-stu-id="60532-398">OData XML</span></span>

<span data-ttu-id="60532-399">przykład odpowiedzi Hello poniżej zawiera 10 elementów zalecane:</span><span class="sxs-lookup"><span data-stu-id="60532-399">hello example response below includes 10 recommended items:</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="update-model"></a><span data-ttu-id="60532-400">Aktualizuj model</span><span class="sxs-lookup"><span data-stu-id="60532-400">Update model</span></span>
<span data-ttu-id="60532-401">Możesz zaktualizować opis modelu hello lub hello identyfikator active kompilacji.</span><span class="sxs-lookup"><span data-stu-id="60532-401">You can update hello model description or hello active build ID.</span></span>
<span data-ttu-id="60532-402">*Identyfikator kompilacji Active* -każdej kompilacji dla każdego modelu ma identyfikator kompilacji.</span><span class="sxs-lookup"><span data-stu-id="60532-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="60532-403">Identyfikator kompilacji active Hello jest hello pierwszym pomyślnym kompilacji każdego nowego modelu.</span><span class="sxs-lookup"><span data-stu-id="60532-403">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="60532-404">Gdy masz identyfikator active kompilacji i wykonaj dodatkowe kompilacje dla hello samego modelu należy tooexplicitly ustaw go jako hello domyślne kompilacji identyfikator aby.</span><span class="sxs-lookup"><span data-stu-id="60532-404">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="60532-405">Jeśli zalecenia, korzystać w sytuacji, jeśli nie określono Identyfikatora kompilacji hello, który ma toouse, domyślne hello, co zostanie użyta automatycznie.</span><span class="sxs-lookup"><span data-stu-id="60532-405">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span>

<span data-ttu-id="60532-406">Mechanizm ten umożliwia — po modelu zalecenia w środowisku produkcyjnym — toobuild nowe modele i testowane przed podwyższeniem ich tooproduction.</span><span class="sxs-lookup"><span data-stu-id="60532-406">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="60532-407">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="60532-407">HTTP Method</span></span> | <span data-ttu-id="60532-408">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="60532-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="60532-409">UMIEŚĆ</span><span class="sxs-lookup"><span data-stu-id="60532-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="60532-410">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60532-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="60532-411">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="60532-411">Parameter Name</span></span> | <span data-ttu-id="60532-412">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="60532-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="60532-413">id</span><span class="sxs-lookup"><span data-stu-id="60532-413">id</span></span> |<span data-ttu-id="60532-414">Unikatowy identyfikator modelu hello (z uwzględnieniem wielkości liter)</span><span class="sxs-lookup"><span data-stu-id="60532-414">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="60532-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="60532-415">apiVersion</span></span> |<span data-ttu-id="60532-416">1.0</span><span class="sxs-lookup"><span data-stu-id="60532-416">1.0</span></span> |
|  | |
| <span data-ttu-id="60532-417">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="60532-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="60532-418">Należy pamiętać, że hello XML znaczniki opis i ActiveBuildId są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="60532-418">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="60532-419">Jeśli nie chcesz, aby tooset opis lub ActiveBuildId, usuń cały tag hello.</span><span class="sxs-lookup"><span data-stu-id="60532-419">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="60532-420">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="60532-420">**Response**:</span></span>

<span data-ttu-id="60532-421">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="60532-421">HTTP Status code: 200</span></span>

<span data-ttu-id="60532-422">OData XML</span><span class="sxs-lookup"><span data-stu-id="60532-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="60532-423">Informacje prawne</span><span class="sxs-lookup"><span data-stu-id="60532-423">Legal</span></span>
<span data-ttu-id="60532-424">Niniejszy dokument jest udostępniany "jako — jest".</span><span class="sxs-lookup"><span data-stu-id="60532-424">This document is provided "as-is".</span></span> <span data-ttu-id="60532-425">Informacje i poglądy wyrażone w tym dokumencie, w tym adresy URL i innymi odwołaniami do witryn internetowych, mogą ulec zmianie bez uprzedzenia.</span><span class="sxs-lookup"><span data-stu-id="60532-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="60532-426">Niektóre przedstawione przykłady są udostępniane tylko do celów ilustracyjnych i są fikcyjne.</span><span class="sxs-lookup"><span data-stu-id="60532-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="60532-427">Żadne rzeczywiste skojarzenia ani połączenia jest przeznaczony lub powinny być zakładane.</span><span class="sxs-lookup"><span data-stu-id="60532-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="60532-428">Ten dokument nie daje użytkownikowi żadnych praw tooany własności intelektualnej związanej z jakimkolwiek produktem firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="60532-428">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="60532-429">Można kopiować i używać tego dokumentu do wewnętrznych celów referencyjnych.</span><span class="sxs-lookup"><span data-stu-id="60532-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="60532-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="60532-430">© 2014 Microsoft.</span></span> <span data-ttu-id="60532-431">Wszelkie prawa zastrzeżone.</span><span class="sxs-lookup"><span data-stu-id="60532-431">All rights reserved.</span></span> 

