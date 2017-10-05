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
redirect_document_id: TRUE
ms.openlocfilehash: 0a9d0b6aa1ef734a857ecc16777ba6250909b38d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="quick-start-guide-for-the-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="f8bc8-104">Przewodnik szybkiego startu Machine Learning API zalecenia (wersja 1)</span><span class="sxs-lookup"><span data-stu-id="f8bc8-104">Quick start guide for the Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="f8bc8-105">Należy zacząć korzystać [kognitywnych usługi interfejsu API zalecenia](https://www.microsoft.com/cognitive-services/recommendations-api) zamiast tej wersji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-105">You should start using the [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="f8bc8-106">Kognitywnych usługę rekomendacji spowoduje zastąpienie tej usługi, a opracowane zostaną nowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-106">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="f8bc8-107">Ma on nowe funkcje, takie jak przetwarzanie wsadowe pomocy technicznej, lepiej Explorer interfejsu API, czyszczący środowisko signup/rozliczeń powierzchni, bardziej spójny interfejs API,... itd.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="f8bc8-108">Dowiedz się więcej o [migracji do nowej usługi kognitywnych](http://aka.ms/recomigrate).</span><span class="sxs-lookup"><span data-stu-id="f8bc8-108">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="f8bc8-109">W tym dokumencie opisano sposób dołączyć daną usługą lub aplikacją do użycia Microsoft Azure Machine Learning zalecenia.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-109">This document describes how to onboard your service or application to use Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="f8bc8-110">Więcej szczegółów można znaleźć w interfejsie API zalecenia w [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="f8bc8-110">You can find more details on the Recommendations API in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="f8bc8-111">Ogólne omówienie</span><span class="sxs-lookup"><span data-stu-id="f8bc8-111">General overview</span></span>
<span data-ttu-id="f8bc8-112">Aby korzystać z usługi Azure Machine Learning zalecenia, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-112">To use Azure Machine Learning Recommendations, you need to take the following steps:</span></span>

* <span data-ttu-id="f8bc8-113">Tworzenie modelu — model jest kontenerem danych użycia, wykaz danych oraz model zalecenia.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-113">Create a model - A model is a container of your usage data, catalog data, and the recommendation model.</span></span>
* <span data-ttu-id="f8bc8-114">Importuj dane katalogu - katalogu zawiera informacje o metadanych dla elementów.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-114">Import catalog data - A catalog contains metadata information on the items.</span></span> 
* <span data-ttu-id="f8bc8-115">Importowanie danych użycia - dane użycia mogą być przekazywane w jeden z dwóch sposobów (lub obie):</span><span class="sxs-lookup"><span data-stu-id="f8bc8-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="f8bc8-116">Przekazując plik zawierający dane użycia.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-116">By uploading a file that contains the usage data.</span></span>
  * <span data-ttu-id="f8bc8-117">Wysyła zdarzenia pozyskiwania danych.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="f8bc8-118">Zwykle możesz przekazać plik użycia, aby można było utworzyć model zalecenie początkowego (bootstrap) i używać go, dopóki system zbiera wystarczającej ilości danych przy użyciu formatu pozyskiwania danych.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-118">Usually you upload a usage file in order to be able to create an initial recommendation model (bootstrap) and use it until the system gathers enough data by using the data acquisition format.</span></span>
* <span data-ttu-id="f8bc8-119">Tworzenie modelu zalecenie — jest to operacja asynchroniczna, w którym system zalecenie pobierze dane użycia i tworzy model zalecenie.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-119">Build a recommendation model - This is an asynchronous operation in which the recommendation system takes all the usage data and creates a recommendation model.</span></span> <span data-ttu-id="f8bc8-120">Ta operacja może zająć kilka minut lub kilka godzin w zależności od rozmiaru danych i parametry konfiguracji kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-120">This operation can take several minutes or several hours depending on the size of the data and the build configuration parameters.</span></span> <span data-ttu-id="f8bc8-121">W przypadku wyzwalają kompilacji, otrzyma identyfikatora dla kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-121">When triggering the build, you will get a build ID.</span></span> <span data-ttu-id="f8bc8-122">Użyj, aby sprawdzić podczas procesu kompilacji zostało zakończone przed rozpoczęciem korzystania zalecenia.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-122">Use it to check when the build process has ended before starting to consume recommendations.</span></span>
* <span data-ttu-id="f8bc8-123">Używać zalecenia - Get zalecenia dotyczące określonego elementu lub listy elementów.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="f8bc8-124">Powyższe kroki są wykonywane za pomocą interfejsu API usługi Azure Machine Learning zalecenia.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-124">All the steps above are done through the Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="f8bc8-125">Możesz pobrać przykładowej aplikacji, która implementuje każdy z tych kroków z [również galerii.](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="f8bc8-125">You can download a sample application that implements each of these steps from the [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="f8bc8-126">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="f8bc8-126">Limitations</span></span>
* <span data-ttu-id="f8bc8-127">Maksymalna liczba modeli dla subskrypcji wynosi 10.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-127">The maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="f8bc8-128">Maksymalna liczba elementów, które mogą zawierać wykaz wynosi 100 000.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-128">The maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="f8bc8-129">Maksymalna liczba punktów użycia, które są zachowane jest ~ 5,000,000.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-129">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="f8bc8-130">Najstarszych zostanie usunięte, gdy nowe zostanie przekazany lub zgłaszane.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-130">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="f8bc8-131">Maksymalny rozmiar danych, które mogą być wysyłane w POST (na przykład importu wykazu danych, importowanie danych użycia) to 200MB.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-131">The maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="f8bc8-132">Liczba transakcji na sekundę dla kompilacji modelu zalecenie, która nie jest aktywny jest ~ 2TPS.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-132">The number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="f8bc8-133">Zalecenie kompilacji modelu, który jest aktywny można przechowywać w do 20TPS.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-133">A recommendation model build that is active can hold up to 20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="f8bc8-134">Integracja</span><span class="sxs-lookup"><span data-stu-id="f8bc8-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="f8bc8-135">Authentication</span><span class="sxs-lookup"><span data-stu-id="f8bc8-135">Authentication</span></span>
<span data-ttu-id="f8bc8-136">Microsoft Azure Marketplace obsługuje podstawowe lub OAuth metodę uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-136">Microsoft Azure Marketplace supports either the Basic or OAuth authentication method.</span></span> <span data-ttu-id="f8bc8-137">Klucze konta można łatwo znaleźć przechodząc do kluczy w witrynie marketplace w obszarze [ustawienia konta](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="f8bc8-137">You can easily find the account keys by navigating to the keys in the marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="f8bc8-138">Uwierzytelnianie podstawowe</span><span class="sxs-lookup"><span data-stu-id="f8bc8-138">Basic Authentication</span></span>
<span data-ttu-id="f8bc8-139">Dodaj nagłówek autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-139">Add the Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="f8bc8-140">Konwertuj do formatu Base64 (C#)</span><span class="sxs-lookup"><span data-stu-id="f8bc8-140">Convert to Base64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="f8bc8-141">Konwertuj do formatu Base64 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="f8bc8-141">Convert to Base64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="f8bc8-142">Identyfikator URI usługi</span><span class="sxs-lookup"><span data-stu-id="f8bc8-142">Service URI</span></span>
<span data-ttu-id="f8bc8-143">Identyfikator URI dla interfejsów API usługi Azure Machine Learning zalecenia katalogu głównego usługi jest [tutaj.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="f8bc8-143">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="f8bc8-144">Pełny identyfikator URI usługi jest wyrażona za pomocą elementów ze specyfikacją OData.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-144">The full service URI is expressed using elements of the OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="f8bc8-145">Wersja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="f8bc8-145">API version</span></span>
<span data-ttu-id="f8bc8-146">Każde wywołanie interfejsu API będzie mieć na końcu, parametr zapytania o nazwie apiVersion, który powinien być ustawiony na "1.0".</span><span class="sxs-lookup"><span data-stu-id="f8bc8-146">Each API call will have, at the end, a query parameter called apiVersion that should be set to "1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="f8bc8-147">Identyfikatory jest rozróżniana wielkość liter</span><span class="sxs-lookup"><span data-stu-id="f8bc8-147">IDs are case-sensitive</span></span>
<span data-ttu-id="f8bc8-148">Identyfikatory zwrócony przez żadnego z interfejsów API, jest rozróżniana wielkość liter i powinien być używany jako takie, gdy dane są przekazywane jako parametry w kolejnych wywołaniach interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-148">IDs, returned by any of the APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="f8bc8-149">Na przykład identyfikatory modelu i identyfikatory katalogu jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="f8bc8-150">Tworzenie modelu</span><span class="sxs-lookup"><span data-stu-id="f8bc8-150">Create a model</span></span>
<span data-ttu-id="f8bc8-151">Tworzenie żądania "Tworzenie modelu":</span><span class="sxs-lookup"><span data-stu-id="f8bc8-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="f8bc8-152">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="f8bc8-152">HTTP Method</span></span> | <span data-ttu-id="f8bc8-153">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="f8bc8-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8bc8-154">POST</span><span class="sxs-lookup"><span data-stu-id="f8bc8-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f8bc8-155">Przykład:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f8bc8-156">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="f8bc8-156">Parameter Name</span></span> | <span data-ttu-id="f8bc8-157">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="f8bc8-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8bc8-158">modelName</span><span class="sxs-lookup"><span data-stu-id="f8bc8-158">modelName</span></span> |<span data-ttu-id="f8bc8-159">Tylko litery (A-Z, a – z), cyfry (0 – 9), łączniki (-) i znak podkreślenia (_) są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="f8bc8-160">Maksymalna długość: 20</span><span class="sxs-lookup"><span data-stu-id="f8bc8-160">Max length: 20</span></span> |
| <span data-ttu-id="f8bc8-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f8bc8-161">apiVersion</span></span> |<span data-ttu-id="f8bc8-162">1.0</span><span class="sxs-lookup"><span data-stu-id="f8bc8-162">1.0</span></span> |
|  | |
| <span data-ttu-id="f8bc8-163">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f8bc8-163">Request Body</span></span> |<span data-ttu-id="f8bc8-164">BRAK</span><span class="sxs-lookup"><span data-stu-id="f8bc8-164">NONE</span></span> |

<span data-ttu-id="f8bc8-165">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-165">**Response**:</span></span>

<span data-ttu-id="f8bc8-166">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f8bc8-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="f8bc8-167">`feed/entry/content/properties/id`-Zawiera identyfikator modelu.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-167">`feed/entry/content/properties/id` - Contains the model ID.</span></span>
  <span data-ttu-id="f8bc8-168">Należy pamiętać, że identyfikator modelu jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-168">Note that the model ID is case-sensitive.</span></span>

<span data-ttu-id="f8bc8-169">OData XML</span><span class="sxs-lookup"><span data-stu-id="f8bc8-169">OData XML</span></span>

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


### <a name="import-catalog-data"></a><span data-ttu-id="f8bc8-170">Importuj dane katalogu</span><span class="sxs-lookup"><span data-stu-id="f8bc8-170">Import catalog data</span></span>
<span data-ttu-id="f8bc8-171">Kilka plików wykazu podczas przesyłania do tego samego modelu z kilka wywołań, firma Microsoft będzie wstawić tylko nowych elementów katalogu.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-171">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span></span> <span data-ttu-id="f8bc8-172">Istniejące elementy pozostanie z oryginalnych wartości.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-172">Existing items will remain with the original values.</span></span>

| <span data-ttu-id="f8bc8-173">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="f8bc8-173">HTTP Method</span></span> | <span data-ttu-id="f8bc8-174">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="f8bc8-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8bc8-175">POST</span><span class="sxs-lookup"><span data-stu-id="f8bc8-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f8bc8-176">Przykład:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f8bc8-177">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="f8bc8-177">Parameter Name</span></span> | <span data-ttu-id="f8bc8-178">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="f8bc8-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8bc8-179">modelId</span><span class="sxs-lookup"><span data-stu-id="f8bc8-179">modelId</span></span> |<span data-ttu-id="f8bc8-180">Unikatowy identyfikator modelu (z uwzględnieniem wielkości liter)</span><span class="sxs-lookup"><span data-stu-id="f8bc8-180">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="f8bc8-181">Nazwa pliku</span><span class="sxs-lookup"><span data-stu-id="f8bc8-181">filename</span></span> |<span data-ttu-id="f8bc8-182">Tekstowy identyfikator katalogu.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-182">Textual identifier of the catalog.</span></span><br><span data-ttu-id="f8bc8-183">Tylko litery (A-Z, a – z), cyfry (0 – 9), łączniki (-) i znak podkreślenia (_) są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="f8bc8-184">Długość maksymalna: 50</span><span class="sxs-lookup"><span data-stu-id="f8bc8-184">Max length: 50</span></span> |
| <span data-ttu-id="f8bc8-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f8bc8-185">apiVersion</span></span> |<span data-ttu-id="f8bc8-186">1.0</span><span class="sxs-lookup"><span data-stu-id="f8bc8-186">1.0</span></span> |
|  | |
| <span data-ttu-id="f8bc8-187">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f8bc8-187">Request Body</span></span> |<span data-ttu-id="f8bc8-188">Wykazu danych.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-188">Catalog data.</span></span> <span data-ttu-id="f8bc8-189">Format:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="f8bc8-190">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f8bc8-190">Name</span></span></th><th><span data-ttu-id="f8bc8-191">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="f8bc8-191">Mandatory</span></span></th><th><span data-ttu-id="f8bc8-192">Typ</span><span class="sxs-lookup"><span data-stu-id="f8bc8-192">Type</span></span></th><th><span data-ttu-id="f8bc8-193">Opis</span><span class="sxs-lookup"><span data-stu-id="f8bc8-193">Description</span></span></th></tr><tr><td><span data-ttu-id="f8bc8-194">Identyfikator elementu</span><span class="sxs-lookup"><span data-stu-id="f8bc8-194">Item Id</span></span></td><td><span data-ttu-id="f8bc8-195">Tak</span><span class="sxs-lookup"><span data-stu-id="f8bc8-195">Yes</span></span></td><td><span data-ttu-id="f8bc8-196">Alfanumeryczne, maksymalna długość 50</span><span class="sxs-lookup"><span data-stu-id="f8bc8-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="f8bc8-197">Unikatowy identyfikator elementu</span><span class="sxs-lookup"><span data-stu-id="f8bc8-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="f8bc8-198">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="f8bc8-198">Item Name</span></span></td><td><span data-ttu-id="f8bc8-199">Tak</span><span class="sxs-lookup"><span data-stu-id="f8bc8-199">Yes</span></span></td><td><span data-ttu-id="f8bc8-200">Alfanumeryczne, maksymalną długość 255 znaków</span><span class="sxs-lookup"><span data-stu-id="f8bc8-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="f8bc8-201">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="f8bc8-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="f8bc8-202">Kategoria elementu</span><span class="sxs-lookup"><span data-stu-id="f8bc8-202">Item Category</span></span></td><td><span data-ttu-id="f8bc8-203">Tak</span><span class="sxs-lookup"><span data-stu-id="f8bc8-203">Yes</span></span></td><td><span data-ttu-id="f8bc8-204">Alfanumeryczne, maksymalną długość 255 znaków</span><span class="sxs-lookup"><span data-stu-id="f8bc8-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="f8bc8-205">Kategoria, do którego ten element należy (na przykład gotowania książek teatralne...)</span><span class="sxs-lookup"><span data-stu-id="f8bc8-205">Category to which this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="f8bc8-206">Opis</span><span class="sxs-lookup"><span data-stu-id="f8bc8-206">Description</span></span></td><td><span data-ttu-id="f8bc8-207">Nie</span><span class="sxs-lookup"><span data-stu-id="f8bc8-207">No</span></span></td><td><span data-ttu-id="f8bc8-208">Alfanumeryczne, maksymalna długość 4000</span><span class="sxs-lookup"><span data-stu-id="f8bc8-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="f8bc8-209">Opis tego elementu</span><span class="sxs-lookup"><span data-stu-id="f8bc8-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="f8bc8-210">Maksymalny rozmiar pliku to 200MB.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="f8bc8-211">Przykład:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="f8bc8-212">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-212">**Response**:</span></span>

<span data-ttu-id="f8bc8-213">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f8bc8-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="f8bc8-214">`Feed\entry\content\properties\LineCount`— Zaakceptowano liczba wierszy.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="f8bc8-215">`Feed\entry\content\properties\ErrorCount`-Liczba wierszy, które nie zostały wstawione z powodu błędu.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>

<span data-ttu-id="f8bc8-216">OData XML</span><span class="sxs-lookup"><span data-stu-id="f8bc8-216">OData XML</span></span>

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


### <a name="import-usage-data"></a><span data-ttu-id="f8bc8-217">Importowanie danych użycia</span><span class="sxs-lookup"><span data-stu-id="f8bc8-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="f8bc8-218">Przekazywanie pliku</span><span class="sxs-lookup"><span data-stu-id="f8bc8-218">Uploading a file</span></span>
<span data-ttu-id="f8bc8-219">W tej sekcji pokazano, jak przekazywać dane użycia przy użyciu pliku.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-219">This section shows how to upload usage data by using a file.</span></span> <span data-ttu-id="f8bc8-220">Można wywołać tego interfejsu API z danych użycia.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="f8bc8-221">Wszystkie dane użycia są zapisywane dla wszystkich wywołań.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="f8bc8-222">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="f8bc8-222">HTTP Method</span></span> | <span data-ttu-id="f8bc8-223">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="f8bc8-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8bc8-224">POST</span><span class="sxs-lookup"><span data-stu-id="f8bc8-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f8bc8-225">Przykład:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f8bc8-226">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="f8bc8-226">Parameter Name</span></span> | <span data-ttu-id="f8bc8-227">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="f8bc8-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8bc8-228">modelId</span><span class="sxs-lookup"><span data-stu-id="f8bc8-228">modelId</span></span> |<span data-ttu-id="f8bc8-229">Unikatowy identyfikator modelu (z uwzględnieniem wielkości liter)</span><span class="sxs-lookup"><span data-stu-id="f8bc8-229">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="f8bc8-230">Nazwa pliku</span><span class="sxs-lookup"><span data-stu-id="f8bc8-230">filename</span></span> |<span data-ttu-id="f8bc8-231">Tekstowy identyfikator katalogu.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-231">Textual identifier of the catalog.</span></span><br><span data-ttu-id="f8bc8-232">Tylko litery (A-Z, a – z), cyfry (0 – 9), łączniki (-) i znak podkreślenia (_) są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="f8bc8-233">Długość maksymalna: 50</span><span class="sxs-lookup"><span data-stu-id="f8bc8-233">Max length: 50</span></span> |
| <span data-ttu-id="f8bc8-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f8bc8-234">apiVersion</span></span> |<span data-ttu-id="f8bc8-235">1.0</span><span class="sxs-lookup"><span data-stu-id="f8bc8-235">1.0</span></span> |
|  | |
| <span data-ttu-id="f8bc8-236">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f8bc8-236">Request Body</span></span> |<span data-ttu-id="f8bc8-237">Dane użycia.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-237">Usage data.</span></span> <span data-ttu-id="f8bc8-238">Format:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="f8bc8-239">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f8bc8-239">Name</span></span></th><th><span data-ttu-id="f8bc8-240">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="f8bc8-240">Mandatory</span></span></th><th><span data-ttu-id="f8bc8-241">Typ</span><span class="sxs-lookup"><span data-stu-id="f8bc8-241">Type</span></span></th><th><span data-ttu-id="f8bc8-242">Opis</span><span class="sxs-lookup"><span data-stu-id="f8bc8-242">Description</span></span></th></tr><tr><td><span data-ttu-id="f8bc8-243">Identyfikator użytkownika</span><span class="sxs-lookup"><span data-stu-id="f8bc8-243">User Id</span></span></td><td><span data-ttu-id="f8bc8-244">Tak</span><span class="sxs-lookup"><span data-stu-id="f8bc8-244">Yes</span></span></td><td><span data-ttu-id="f8bc8-245">Alfanumeryczne</span><span class="sxs-lookup"><span data-stu-id="f8bc8-245">Alphanumeric</span></span></td><td><span data-ttu-id="f8bc8-246">Unikatowy identyfikator użytkownika</span><span class="sxs-lookup"><span data-stu-id="f8bc8-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="f8bc8-247">Identyfikator elementu</span><span class="sxs-lookup"><span data-stu-id="f8bc8-247">Item Id</span></span></td><td><span data-ttu-id="f8bc8-248">Tak</span><span class="sxs-lookup"><span data-stu-id="f8bc8-248">Yes</span></span></td><td><span data-ttu-id="f8bc8-249">Alfanumeryczne, maksymalna długość 50</span><span class="sxs-lookup"><span data-stu-id="f8bc8-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="f8bc8-250">Unikatowy identyfikator elementu</span><span class="sxs-lookup"><span data-stu-id="f8bc8-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="f8bc8-251">Time</span><span class="sxs-lookup"><span data-stu-id="f8bc8-251">Time</span></span></td><td><span data-ttu-id="f8bc8-252">Nie</span><span class="sxs-lookup"><span data-stu-id="f8bc8-252">No</span></span></td><td><span data-ttu-id="f8bc8-253">Data w formacie: RRRR/MM/ddtgg (na przykład 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="f8bc8-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="f8bc8-254">Czas danych</span><span class="sxs-lookup"><span data-stu-id="f8bc8-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="f8bc8-255">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="f8bc8-255">Event</span></span></td><td><span data-ttu-id="f8bc8-256">Nie, jeśli podane, również umieścić daty</span><span class="sxs-lookup"><span data-stu-id="f8bc8-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="f8bc8-257">Jeden z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-257">One of the following:</span></span><br><span data-ttu-id="f8bc8-258">• Kliknij przycisk</span><span class="sxs-lookup"><span data-stu-id="f8bc8-258">• Click</span></span><br><span data-ttu-id="f8bc8-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="f8bc8-259">• RecommendationClick</span></span><br><span data-ttu-id="f8bc8-260">• AddShopCart</span><span class="sxs-lookup"><span data-stu-id="f8bc8-260">•    AddShopCart</span></span><br><span data-ttu-id="f8bc8-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="f8bc8-261">• RemoveShopCart</span></span><br><span data-ttu-id="f8bc8-262">• Zakupu</span><span class="sxs-lookup"><span data-stu-id="f8bc8-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="f8bc8-263">Maksymalny rozmiar pliku to 200MB.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="f8bc8-264">Przykład:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="f8bc8-265">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-265">**Response**:</span></span>

<span data-ttu-id="f8bc8-266">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f8bc8-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="f8bc8-267">`Feed\entry\content\properties\LineCount`— Zaakceptowano liczba wierszy.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="f8bc8-268">`Feed\entry\content\properties\ErrorCount`-Liczba wierszy, które nie zostały wstawione z powodu błędu.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>
* <span data-ttu-id="f8bc8-269">`Feed\entry\content\properties\FileId`— Identyfikator pliku.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="f8bc8-270">OData XML</span><span class="sxs-lookup"><span data-stu-id="f8bc8-270">OData XML</span></span>

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


#### <a name="using-data-acquisition"></a><span data-ttu-id="f8bc8-271">Przy użyciu danych</span><span class="sxs-lookup"><span data-stu-id="f8bc8-271">Using data acquisition</span></span>
<span data-ttu-id="f8bc8-272">W tej sekcji przedstawiono sposób wysyłania zdarzeń w czasie rzeczywistym do Azure Machine Learning zalecenia, zazwyczaj z witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-272">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="f8bc8-273">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="f8bc8-273">HTTP Method</span></span> | <span data-ttu-id="f8bc8-274">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="f8bc8-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8bc8-275">POST</span><span class="sxs-lookup"><span data-stu-id="f8bc8-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f8bc8-276">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="f8bc8-276">Parameter Name</span></span> | <span data-ttu-id="f8bc8-277">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="f8bc8-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8bc8-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f8bc8-278">apiVersion</span></span> |<span data-ttu-id="f8bc8-279">1.0</span><span class="sxs-lookup"><span data-stu-id="f8bc8-279">1.0</span></span> |
|  | |
| <span data-ttu-id="f8bc8-280">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f8bc8-280">Request body</span></span> |<span data-ttu-id="f8bc8-281">Wpis danych zdarzeń dla każdego zdarzenia, które chcesz wysyłać.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-281">Event data entry for each event you want to send.</span></span> <span data-ttu-id="f8bc8-282">Należy wysłać do tej samej sesji użytkownika lub przeglądarki ten sam identyfikator w polu identyfikatora sesji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-282">You should send for the same user or browser session the same ID in the SessionId field.</span></span> <span data-ttu-id="f8bc8-283">(Zobacz przykład treści zdarzenia poniżej).</span><span class="sxs-lookup"><span data-stu-id="f8bc8-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="f8bc8-284">Przykład dla zdarzenia "Kliknij przycisk":</span><span class="sxs-lookup"><span data-stu-id="f8bc8-284">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="f8bc8-285">Przykład dla zdarzenia "RecommendationClick":</span><span class="sxs-lookup"><span data-stu-id="f8bc8-285">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="f8bc8-286">Przykład dla zdarzenia "AddShopCart":</span><span class="sxs-lookup"><span data-stu-id="f8bc8-286">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="f8bc8-287">Przykład dla zdarzenia "RemoveShopCart":</span><span class="sxs-lookup"><span data-stu-id="f8bc8-287">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="f8bc8-288">Przykład dla zdarzenia "Zakupu":</span><span class="sxs-lookup"><span data-stu-id="f8bc8-288">Example for event 'Purchase':</span></span>
  
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
* <span data-ttu-id="f8bc8-289">Przykład wysyłania 2 zdarzenia "kliknij" a "AddShopCart":</span><span class="sxs-lookup"><span data-stu-id="f8bc8-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="f8bc8-290">**Odpowiedź**: kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f8bc8-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="f8bc8-291">Tworzenie modelu zalecenia</span><span class="sxs-lookup"><span data-stu-id="f8bc8-291">Build a recommendation model</span></span>
| <span data-ttu-id="f8bc8-292">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="f8bc8-292">HTTP Method</span></span> | <span data-ttu-id="f8bc8-293">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="f8bc8-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8bc8-294">POST</span><span class="sxs-lookup"><span data-stu-id="f8bc8-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f8bc8-295">Przykład:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f8bc8-296">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="f8bc8-296">Parameter Name</span></span> | <span data-ttu-id="f8bc8-297">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="f8bc8-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8bc8-298">modelId</span><span class="sxs-lookup"><span data-stu-id="f8bc8-298">modelId</span></span> |<span data-ttu-id="f8bc8-299">Unikatowy identyfikator modelu (z uwzględnieniem wielkości liter)</span><span class="sxs-lookup"><span data-stu-id="f8bc8-299">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="f8bc8-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="f8bc8-300">userDescription</span></span> |<span data-ttu-id="f8bc8-301">Tekstowy identyfikator katalogu.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-301">Textual identifier of the catalog.</span></span> <span data-ttu-id="f8bc8-302">Należy zwrócić uwagę, jeśli używasz spacje musi kodowanie go % 20 zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="f8bc8-303">Zobacz przykład powyżej.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-303">See example above.</span></span><br><span data-ttu-id="f8bc8-304">Długość maksymalna: 50</span><span class="sxs-lookup"><span data-stu-id="f8bc8-304">Max length: 50</span></span> |
| <span data-ttu-id="f8bc8-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f8bc8-305">apiVersion</span></span> |<span data-ttu-id="f8bc8-306">1.0</span><span class="sxs-lookup"><span data-stu-id="f8bc8-306">1.0</span></span> |
|  | |
| <span data-ttu-id="f8bc8-307">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f8bc8-307">Request Body</span></span> |<span data-ttu-id="f8bc8-308">BRAK</span><span class="sxs-lookup"><span data-stu-id="f8bc8-308">NONE</span></span> |

<span data-ttu-id="f8bc8-309">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-309">**Response**:</span></span>

<span data-ttu-id="f8bc8-310">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f8bc8-310">HTTP Status code: 200</span></span>

<span data-ttu-id="f8bc8-311">Jest to interfejs API asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-311">This is an asynchronous API.</span></span> <span data-ttu-id="f8bc8-312">Otrzymasz identyfikator kompilacji w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-312">You will get a build ID as a response.</span></span> <span data-ttu-id="f8bc8-313">Aby wiedzieć, kiedy Kompilacja została zakończona, należy wywołać interfejs API "Pobierz kompilacje stan modelu" i zlokalizuj identyfikator tej kompilacji w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-313">To know when the build has ended, you should call the "Get Builds Status of a Model" API and locate this build ID in the response.</span></span> <span data-ttu-id="f8bc8-314">Należy pamiętać, że kompilacji może potrwać od minut godzin w zależności od rozmiaru danych.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-314">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="f8bc8-315">Nie można używać zalecenia do kompilacji kończy się.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-315">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="f8bc8-316">Stan prawidłowy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-316">Valid build status:</span></span>

* <span data-ttu-id="f8bc8-317">Utwórz — Model został utworzony.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-317">Create – Model was created.</span></span>
* <span data-ttu-id="f8bc8-318">W kolejce — zostało wyzwolone kompilacji modelu i jest w kolejce.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="f8bc8-319">Kompilowanie — Model została skompilowana.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-319">Building – Model is being built.</span></span>
* <span data-ttu-id="f8bc8-320">Powodzenie — kompilacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="f8bc8-321">Błąd — Kompilacja została zakończona z błędem.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="f8bc8-322">Anulowane — Kompilacja została anulowana.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="f8bc8-323">Anulowanie — Kompilacja została anulowana.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="f8bc8-324">Należy pamiętać, że identyfikator kompilacji można znaleźć w następującej ścieżce:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="f8bc8-324">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="f8bc8-325">OData XML</span><span class="sxs-lookup"><span data-stu-id="f8bc8-325">OData XML</span></span>

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

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="f8bc8-326">Pobierz stan kompilacji modelu</span><span class="sxs-lookup"><span data-stu-id="f8bc8-326">Get build status of a model</span></span>
| <span data-ttu-id="f8bc8-327">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="f8bc8-327">HTTP Method</span></span> | <span data-ttu-id="f8bc8-328">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="f8bc8-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8bc8-329">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="f8bc8-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="f8bc8-330">Przykład:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="f8bc8-331">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="f8bc8-331">Parameter Name</span></span> | <span data-ttu-id="f8bc8-332">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="f8bc8-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8bc8-333">modelId</span><span class="sxs-lookup"><span data-stu-id="f8bc8-333">modelId</span></span> |<span data-ttu-id="f8bc8-334">Unikatowy identyfikator modelu (z uwzględnieniem wielkości liter)</span><span class="sxs-lookup"><span data-stu-id="f8bc8-334">Unique identifier of the model  (case-sensitive)</span></span> |
| <span data-ttu-id="f8bc8-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="f8bc8-335">onlyLastBuild</span></span> |<span data-ttu-id="f8bc8-336">Wskazuje, czy mają być zwracane całą historię kompilacji modelu lub tylko stan ostatniej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-336">Indicates whether to return all the build history of the model or only the status of the most recent build.</span></span> |
| <span data-ttu-id="f8bc8-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f8bc8-337">apiVersion</span></span> |<span data-ttu-id="f8bc8-338">1.0</span><span class="sxs-lookup"><span data-stu-id="f8bc8-338">1.0</span></span> |

<span data-ttu-id="f8bc8-339">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-339">**Response**:</span></span>

<span data-ttu-id="f8bc8-340">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f8bc8-340">HTTP Status code: 200</span></span>

<span data-ttu-id="f8bc8-341">Odpowiedź zawiera jednego wpisu na kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-341">The response includes one entry per build.</span></span> <span data-ttu-id="f8bc8-342">Każdy wpis ma następujące dane:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-342">Each entry has the following data:</span></span>

* <span data-ttu-id="f8bc8-343">`feed/entry/content/properties/UserName`— Nazwa użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-343">`feed/entry/content/properties/UserName` – Name of the user.</span></span>
* <span data-ttu-id="f8bc8-344">`feed/entry/content/properties/ModelName`— Nazwa modelu.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-344">`feed/entry/content/properties/ModelName` – Name of the model.</span></span>
* <span data-ttu-id="f8bc8-345">`feed/entry/content/properties/ModelId`— Unikatowy identyfikator modelu.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="f8bc8-346">`feed/entry/content/properties/IsDeployed`— Czy kompilacja zostaje wdrożona ()</span><span class="sxs-lookup"><span data-stu-id="f8bc8-346">`feed/entry/content/properties/IsDeployed` – Whether the build is deployed (a.k.a.</span></span> <span data-ttu-id="f8bc8-347">aktywne kompilacji).</span><span class="sxs-lookup"><span data-stu-id="f8bc8-347">active build).</span></span>
* <span data-ttu-id="f8bc8-348">`feed/entry/content/properties/BuildId`— Unikatowy identyfikator kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="f8bc8-349">`feed/entry/content/properties/BuildType`— Typ kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-349">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="f8bc8-350">`feed/entry/content/properties/Status`— Stan kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="f8bc8-351">Może być jedną z następujących czynności: błąd, kompilowanie, w kolejce, Cancelling anulowane, Powodzenie</span><span class="sxs-lookup"><span data-stu-id="f8bc8-351">Can be one of the following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="f8bc8-352">`feed/entry/content/properties/StatusMessage`— Komunikat szczegółowy stan (dotyczy tylko określone stany).</span><span class="sxs-lookup"><span data-stu-id="f8bc8-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="f8bc8-353">`feed/entry/content/properties/Progress`— Utwórz postępu (%).</span><span class="sxs-lookup"><span data-stu-id="f8bc8-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="f8bc8-354">`feed/entry/content/properties/StartTime`— Godzina rozpoczęcia kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="f8bc8-355">`feed/entry/content/properties/EndTime`— Czas zakończenia kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="f8bc8-356">`feed/entry/content/properties/ExecutionTime`— Czas trwania kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="f8bc8-357">`feed/entry/content/properties/ProgressStep`— Szczegóły dotyczące bieżącego etapu należącego do kompilacji w toku.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-357">`feed/entry/content/properties/ProgressStep` – Details about the current stage that a build in progress is in.</span></span>

<span data-ttu-id="f8bc8-358">Stan prawidłowy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-358">Valid build status:</span></span>

* <span data-ttu-id="f8bc8-359">Utworzono — wpis żądanie kompilacji zostało utworzone.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="f8bc8-360">W kolejce — żądanie kompilacji zostało wyzwolone i jest w kolejce.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="f8bc8-361">Kompilowanie — kompilacji jest w toku.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-361">Building – Build is in process.</span></span>
* <span data-ttu-id="f8bc8-362">Powodzenie — kompilacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="f8bc8-363">Błąd — Kompilacja została zakończona z błędem.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="f8bc8-364">Anulowane — Kompilacja została anulowana.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="f8bc8-365">Anulowanie — Kompilacja została anulowana.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="f8bc8-366">Prawidłowe wartości dla typu kompilacji:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-366">Valid values for build type:</span></span>

* <span data-ttu-id="f8bc8-367">Ranga - rangę kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-367">Rank - Rank build.</span></span> <span data-ttu-id="f8bc8-368">(Rank kompilacji szczegółowe informacje, można znaleźć w dokumencie "Machine Learning zalecenie interfejsu API dokumentacji").</span><span class="sxs-lookup"><span data-stu-id="f8bc8-368">(For rank build details, please refer to the "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="f8bc8-369">Zalecenie - zalecenie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="f8bc8-370">Zmianie wysokości progów - zakupione razem często kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="f8bc8-371">OData XML</span><span class="sxs-lookup"><span data-stu-id="f8bc8-371">OData XML</span></span>

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


### <a name="get-recommendations"></a><span data-ttu-id="f8bc8-372">Uzyskaj zalecenia</span><span class="sxs-lookup"><span data-stu-id="f8bc8-372">Get recommendations</span></span>
| <span data-ttu-id="f8bc8-373">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="f8bc8-373">HTTP Method</span></span> | <span data-ttu-id="f8bc8-374">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="f8bc8-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8bc8-375">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="f8bc8-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="f8bc8-376">Przykład:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="f8bc8-377">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="f8bc8-377">Parameter Name</span></span> | <span data-ttu-id="f8bc8-378">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="f8bc8-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8bc8-379">modelId</span><span class="sxs-lookup"><span data-stu-id="f8bc8-379">modelId</span></span> |<span data-ttu-id="f8bc8-380">Unikatowy identyfikator modelu (z uwzględnieniem wielkości liter)</span><span class="sxs-lookup"><span data-stu-id="f8bc8-380">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="f8bc8-381">identyfikatory elementów</span><span class="sxs-lookup"><span data-stu-id="f8bc8-381">itemIds</span></span> |<span data-ttu-id="f8bc8-382">Rozdzielana przecinkami lista elementów zalecanie dla.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-382">Comma-separated list of the items to recommend for.</span></span><br><span data-ttu-id="f8bc8-383">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="f8bc8-383">Max length: 1024</span></span> |
| <span data-ttu-id="f8bc8-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="f8bc8-384">numberOfResults</span></span> |<span data-ttu-id="f8bc8-385">Liczba wymaganych wyników</span><span class="sxs-lookup"><span data-stu-id="f8bc8-385">Number of required results</span></span> |
| <span data-ttu-id="f8bc8-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="f8bc8-386">includeMetatadata</span></span> |<span data-ttu-id="f8bc8-387">Użycia w przyszłości, zawsze false</span><span class="sxs-lookup"><span data-stu-id="f8bc8-387">Future use, always false</span></span> |
| <span data-ttu-id="f8bc8-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f8bc8-388">apiVersion</span></span> |<span data-ttu-id="f8bc8-389">1.0</span><span class="sxs-lookup"><span data-stu-id="f8bc8-389">1.0</span></span> |

<span data-ttu-id="f8bc8-390">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="f8bc8-390">**Response:**</span></span>

<span data-ttu-id="f8bc8-391">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f8bc8-391">HTTP Status code: 200</span></span>

<span data-ttu-id="f8bc8-392">Odpowiedź zawiera jeden wpis dla każdego elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-392">The response includes one entry per recommended item.</span></span> <span data-ttu-id="f8bc8-393">Każdy wpis ma następujące dane:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-393">Each entry has the following data:</span></span>

* <span data-ttu-id="f8bc8-394">`Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="f8bc8-395">`Feed\entry\content\properties\Name`-Nazwa elementu.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-395">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="f8bc8-396">`Feed\entry\content\properties\Rating`— Ocena zalecenia; większa liczba oznacza większą wiarą.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-396">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="f8bc8-397">`Feed\entry\content\properties\Reasoning`-Zalecenie rozsądkiem (na przykład zalecenie wyjaśnienia).</span><span class="sxs-lookup"><span data-stu-id="f8bc8-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="f8bc8-398">OData XML</span><span class="sxs-lookup"><span data-stu-id="f8bc8-398">OData XML</span></span>

<span data-ttu-id="f8bc8-399">Przykład odpowiedzi poniżej zawiera 10 elementów zalecane:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-399">The example response below includes 10 recommended items:</span></span>

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

### <a name="update-model"></a><span data-ttu-id="f8bc8-400">Aktualizuj model</span><span class="sxs-lookup"><span data-stu-id="f8bc8-400">Update model</span></span>
<span data-ttu-id="f8bc8-401">Możesz zaktualizować opis modelu lub identyfikator active kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-401">You can update the model description or the active build ID.</span></span>
<span data-ttu-id="f8bc8-402">*Identyfikator kompilacji Active* -każdej kompilacji dla każdego modelu ma identyfikator kompilacji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="f8bc8-403">Identyfikator active kompilacji jest pomyślnego tworzenia pierwszej kompilacji każdego nowego modelu.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-403">The active build ID is the first successful build of every new model.</span></span> <span data-ttu-id="f8bc8-404">Gdy masz identyfikator kompilacji active i wykonaniu dodatkowych kompilacji w ramach tego samego modelu, musisz jawnie ustaw go jako domyślny identyfikator kompilacji Jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-404">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span></span> <span data-ttu-id="f8bc8-405">Gdy zalecenia, można korzystać, jeśli nie określisz identyfikator kompilacji, który ma być używany, domyślny zostanie użyty automatycznie.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-405">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span></span>

<span data-ttu-id="f8bc8-406">Mechanizm ten umożliwia — po utworzeniu modelu zalecenia w środowisku produkcyjnym — do tworzenia nowych modeli i testowane przed Przenieś do produkcji.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-406">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span></span>

| <span data-ttu-id="f8bc8-407">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="f8bc8-407">HTTP Method</span></span> | <span data-ttu-id="f8bc8-408">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="f8bc8-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8bc8-409">UMIEŚĆ</span><span class="sxs-lookup"><span data-stu-id="f8bc8-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="f8bc8-410">Przykład:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="f8bc8-411">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="f8bc8-411">Parameter Name</span></span> | <span data-ttu-id="f8bc8-412">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="f8bc8-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="f8bc8-413">id</span><span class="sxs-lookup"><span data-stu-id="f8bc8-413">id</span></span> |<span data-ttu-id="f8bc8-414">Unikatowy identyfikator modelu (z uwzględnieniem wielkości liter)</span><span class="sxs-lookup"><span data-stu-id="f8bc8-414">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="f8bc8-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f8bc8-415">apiVersion</span></span> |<span data-ttu-id="f8bc8-416">1.0</span><span class="sxs-lookup"><span data-stu-id="f8bc8-416">1.0</span></span> |
|  | |
| <span data-ttu-id="f8bc8-417">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="f8bc8-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="f8bc8-418">Należy pamiętać, że tagi XML, opis i ActiveBuildId są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-418">Note that the XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="f8bc8-419">Jeśli nie chcesz ustawić opis lub ActiveBuildId, usuń cały tag.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-419">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span></span> |

<span data-ttu-id="f8bc8-420">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="f8bc8-420">**Response**:</span></span>

<span data-ttu-id="f8bc8-421">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="f8bc8-421">HTTP Status code: 200</span></span>

<span data-ttu-id="f8bc8-422">OData XML</span><span class="sxs-lookup"><span data-stu-id="f8bc8-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="f8bc8-423">Informacje prawne</span><span class="sxs-lookup"><span data-stu-id="f8bc8-423">Legal</span></span>
<span data-ttu-id="f8bc8-424">Niniejszy dokument jest udostępniany "jako — jest".</span><span class="sxs-lookup"><span data-stu-id="f8bc8-424">This document is provided "as-is".</span></span> <span data-ttu-id="f8bc8-425">Informacje i poglądy wyrażone w tym dokumencie, w tym adresy URL i innymi odwołaniami do witryn internetowych, mogą ulec zmianie bez uprzedzenia.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="f8bc8-426">Niektóre przedstawione przykłady są udostępniane tylko do celów ilustracyjnych i są fikcyjne.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="f8bc8-427">Żadne rzeczywiste skojarzenia ani połączenia jest przeznaczony lub powinny być zakładane.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="f8bc8-428">Ten dokument nie daje użytkownikowi żadnych praw do jakiejkolwiek własności intelektualnej związanej z jakimkolwiek produktem firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-428">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="f8bc8-429">Można kopiować i używać tego dokumentu do wewnętrznych celów referencyjnych.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="f8bc8-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-430">© 2014 Microsoft.</span></span> <span data-ttu-id="f8bc8-431">Wszelkie prawa zastrzeżone.</span><span class="sxs-lookup"><span data-stu-id="f8bc8-431">All rights reserved.</span></span> 

