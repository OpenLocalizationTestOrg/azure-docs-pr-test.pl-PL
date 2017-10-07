---
title: aaaMachine dokumentacji interfejsu API uczenia zalecenia | Dokumentacja firmy Microsoft
description: "Dokumentacji platformy Azure Machine Learning API zalecenia dla aparatu zalecenia, dostępne w hello Microsoft Azure Marketplace."
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a><span data-ttu-id="a085e-103">Dokumentacja dotycząca interfejsu API zaleceń usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a085e-103">Azure Machine Learning Recommendations API Documentation</span></span>
> [!NOTE]
> <span data-ttu-id="a085e-104">Należy rozpocząć za pomocą hello usługi kognitywnych zalecenia dotyczące interfejsu API, zamiast tej wersji.</span><span class="sxs-lookup"><span data-stu-id="a085e-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="a085e-105">Hello kognitywnych usługę rekomendacji spowoduje zastąpienie tej usługi, a opracowane zostaną wszystkie hello nowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="a085e-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="a085e-106">Ma on nowe funkcje, takie jak przetwarzanie wsadowe pomocy technicznej, lepiej Explorer interfejsu API, czyszczący środowisko signup/rozliczeń powierzchni, bardziej spójny interfejs API,... itd.</span><span class="sxs-lookup"><span data-stu-id="a085e-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="a085e-107">Dowiedz się więcej o [toohello Migrowanie nową usługę kognitywnych](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="a085e-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="a085e-108">Ten dokument przedstawia interfejsów API firmy Microsoft usługi Azure Machine Learning zalecenia.</span><span class="sxs-lookup"><span data-stu-id="a085e-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="a085e-109">1. Ogólne omówienie</span><span class="sxs-lookup"><span data-stu-id="a085e-109">1. General overview</span></span>
<span data-ttu-id="a085e-110">Ten dokument jest odwołanie do interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a085e-110">This document is an API reference.</span></span> <span data-ttu-id="a085e-111">Należy rozpocząć hello "Azure Machine Learning zalecenie — Szybki Start" dokumentu.</span><span class="sxs-lookup"><span data-stu-id="a085e-111">You should start with hello “Azure Machine Learning Recommendation - Quick Start” document.</span></span>

<span data-ttu-id="a085e-112">Hello Azure Machine Learning zalecenia API można podzielić na następujące grupy logiczne hello:</span><span class="sxs-lookup"><span data-stu-id="a085e-112">hello Azure Machine Learning Recommendations API can be divided into hello following logical groups:</span></span>

* <span data-ttu-id="a085e-113"><ins>Ograniczenia</ins> — ograniczenia interfejsu API zalecenia.</span><span class="sxs-lookup"><span data-stu-id="a085e-113"><ins>Limitations</ins> - Recommendations API limitations.</span></span>
* <span data-ttu-id="a085e-114"><ins>Informacje ogólne</ins> -informacji dotyczących uwierzytelniania, z identyfikatora URI i przechowywania wersji.</span><span class="sxs-lookup"><span data-stu-id="a085e-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span></span>
* <span data-ttu-id="a085e-115"><ins>Model Basic</ins> -interfejsów API, które umożliwiają toodo hello podstawowe operacje na modelu (np. Tworzenie, aktualizowanie i usuwanie modelu).</span><span class="sxs-lookup"><span data-stu-id="a085e-115"><ins>Model Basic</ins> - APIs that enable you toodo hello basic operations on model (e.g. create, update and delete a model).</span></span>
* <span data-ttu-id="a085e-116"><ins>Model zaawansowane</ins> -interfejsów API, które umożliwiają tooget zaawansowane wgląd w danych na powitania modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-116"><ins>Model Advanced</ins> - APIs that enable you tooget advanced data insights on hello model.</span></span>
* <span data-ttu-id="a085e-117"><ins>Model reguły biznesowe</ins> -interfejsów API, które umożliwiają toomanage reguły biznesowe na powitania modelu zalecenie wyniki.</span><span class="sxs-lookup"><span data-stu-id="a085e-117"><ins>Model Business Rules</ins> - APIs that enable you toomanage business rules on hello model recommendation results.</span></span>
* <span data-ttu-id="a085e-118"><ins>Katalog</ins> -interfejsów API, które umożliwiają toodo podstawowe operacje w wykazie modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-118"><ins>Catalog</ins> - APIs that enable you toodo basic operations on a model catalog.</span></span> <span data-ttu-id="a085e-119">Katalog zawiera informacje o metadanych na elementach hello hello danych użycia.</span><span class="sxs-lookup"><span data-stu-id="a085e-119">A catalog contains metadata information on hello items of hello usage data.</span></span>
* <span data-ttu-id="a085e-120"><ins>Funkcja</ins> -interfejsy API umożliwiające tooget wgląd w elemencie do katalogu hello i w jaki sposób toouse zalecenia lepsze toobuild informacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-120"><ins>Feature</ins> - APIs that enable tooget insights on item into hello catalog and how toouse this information toobuild better recommendations.</span></span>
* <span data-ttu-id="a085e-121"><ins>Dane użycia</ins> -interfejsów API, które umożliwiają toodo podstawowe operacje na danych użycia hello modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-121"><ins>Usage Data</ins> - APIs that enable you toodo basic operations on hello model usage data.</span></span> <span data-ttu-id="a085e-122">Dane użycia w podstawowej postaci hello składa się z wierszy, które obejmują pary &#60; userId &#62; &#60; identyfikator elementu &#62;.</span><span class="sxs-lookup"><span data-stu-id="a085e-122">Usage data in hello basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span></span>
* <span data-ttu-id="a085e-123"><ins>Tworzenie</ins> — Tworzenie interfejsów API, które umożliwiają tootrigger modelu i czy podstawowe operacje, które są powiązane toothis kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-123"><ins>Build</ins> - APIs that enable you tootrigger a model build and do basic operations that are related toothis build.</span></span> <span data-ttu-id="a085e-124">Po utworzeniu użycia cennych danych, można wyzwolić kompilację modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-124">You can trigger a model build once you have valuable usage data.</span></span>
* <span data-ttu-id="a085e-125"><ins>Zalecenie</ins> -interfejsów API, które umożliwiają zalecenia tooconsume po zakończeniu kompilacji hello modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-125"><ins>Recommendation</ins> - APIs that enable you tooconsume recommendations once hello build of a model ends.</span></span>
* <span data-ttu-id="a085e-126"><ins>Dane użytkownika</ins> -interfejsów API, które umożliwiają toofetch informacji na temat danych użycia hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a085e-126"><ins>User Data</ins> - APIs that enable you toofetch information on hello user usage data.</span></span>
* <span data-ttu-id="a085e-127"><ins>Powiadomienia</ins> -tooyour interfejsu API operacji związanych z interfejsów API, które umożliwiają powiadomienia tooreceive problemów.</span><span class="sxs-lookup"><span data-stu-id="a085e-127"><ins>Notifications</ins> - APIs that enable you tooreceive notifications on problems related tooyour API operations.</span></span> <span data-ttu-id="a085e-128">(Na przykład możesz są raportowania danych użycia przez gromadzenia danych i większość zdarzeń hello przetwarzania kończą się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="a085e-128">(For example, you are reporting usage data via Data Acquisition and most of hello events processing are failing.</span></span> <span data-ttu-id="a085e-129">Powiadomienie o błędzie zostanie wygenerowany.)</span><span class="sxs-lookup"><span data-stu-id="a085e-129">An error notification will be raised.)</span></span>

## <a name="2-limitations"></a><span data-ttu-id="a085e-130">2. Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="a085e-130">2. Limitations</span></span>
* <span data-ttu-id="a085e-131">Maksymalna liczba modeli na subskrypcję Hello wynosi 10.</span><span class="sxs-lookup"><span data-stu-id="a085e-131">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="a085e-132">Maksymalna liczba kompilacji na model w Hello wynosi 20.</span><span class="sxs-lookup"><span data-stu-id="a085e-132">hello maximum number of builds per model is 20.</span></span>
* <span data-ttu-id="a085e-133">Hello maksymalną liczbę elementów, które mogą zawierać wykaz wynosi 100 000.</span><span class="sxs-lookup"><span data-stu-id="a085e-133">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="a085e-134">Maksymalna liczba punktów użycia, które są zachowane w Hello jest ~ 5,000,000.</span><span class="sxs-lookup"><span data-stu-id="a085e-134">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="a085e-135">Hello najstarsze zostanie usunięte, gdy nowe zostanie przekazany lub zgłaszane.</span><span class="sxs-lookup"><span data-stu-id="a085e-135">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="a085e-136">Maksymalny rozmiar danych, które mogą być wysyłane w POST (np. import wykazu danych, importowanie danych użycia) Hello jest 200MB.</span><span class="sxs-lookup"><span data-stu-id="a085e-136">hello maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="a085e-137">Maksymalna liczba elementów, które może zostać wyświetlony monit o podanie podczas pobierania zalecenia Hello wynosi 150.</span><span class="sxs-lookup"><span data-stu-id="a085e-137">hello maximum number of items that can be asked for when getting recommendations is 150.</span></span>

## <a name="3-apis---general-information"></a><span data-ttu-id="a085e-138">3. Interfejsy API — informacje ogólne</span><span class="sxs-lookup"><span data-stu-id="a085e-138">3. APIs - general information</span></span>
### <a name="31-authentication"></a><span data-ttu-id="a085e-139">3.1.</span><span class="sxs-lookup"><span data-stu-id="a085e-139">3.1.</span></span> <span data-ttu-id="a085e-140">Authentication</span><span class="sxs-lookup"><span data-stu-id="a085e-140">Authentication</span></span>
<span data-ttu-id="a085e-141">Wykonaj hello Microsoft Azure Marketplace wytyczne dotyczące uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a085e-141">Please follow hello Microsoft Azure Marketplace guidelines regarding authentication.</span></span> <span data-ttu-id="a085e-142">Hello marketplace obsługuje każdej hello Basic lub OAuth z metod uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a085e-142">hello marketplace supports either hello Basic or OAuth authentication method.</span></span>

### <a name="32-service-uri"></a><span data-ttu-id="a085e-143">3.2.</span><span class="sxs-lookup"><span data-stu-id="a085e-143">3.2.</span></span> <span data-ttu-id="a085e-144">Identyfikator URI usługi</span><span class="sxs-lookup"><span data-stu-id="a085e-144">Service URI</span></span>
<span data-ttu-id="a085e-145">główny usługi Hello identyfikatora URI dla interfejsów API usługi Azure Machine Learning zalecenia hello jest [tutaj.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span><span class="sxs-lookup"><span data-stu-id="a085e-145">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span></span>

<span data-ttu-id="a085e-146">Identyfikator URI usługi pełne Hello jest wyrażona za pomocą elementów hello specyfikację OData.</span><span class="sxs-lookup"><span data-stu-id="a085e-146">hello full service URI is expressed using elements of hello OData specification.</span></span>  

### <a name="33-api-version"></a><span data-ttu-id="a085e-147">3.3.</span><span class="sxs-lookup"><span data-stu-id="a085e-147">3.3.</span></span> <span data-ttu-id="a085e-148">Wersja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a085e-148">API version</span></span>
<span data-ttu-id="a085e-149">Każde wywołanie interfejsu API na końcu hello ma parametr zapytania o nazwie apiVersion, który powinien być ustawiony too1.0.</span><span class="sxs-lookup"><span data-stu-id="a085e-149">Each API call will have, at hello end, a query parameter called apiVersion that should be set too1.0.</span></span>

### <a name="34-ids-are-case-sensitive"></a><span data-ttu-id="a085e-150">3.4.</span><span class="sxs-lookup"><span data-stu-id="a085e-150">3.4.</span></span> <span data-ttu-id="a085e-151">Identyfikatory jest uwzględniana wielkość liter</span><span class="sxs-lookup"><span data-stu-id="a085e-151">IDs are case sensitive</span></span>
<span data-ttu-id="a085e-152">Identyfikatory zwrócony przez żadnego z interfejsów API, hello jest uwzględniana wielkość liter i powinien być używany jako takie, gdy dane są przekazywane jako parametry w kolejnych wywołaniach interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a085e-152">IDs, returned by any of hello APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="a085e-153">Na przykład identyfikatory modelu i identyfikatory katalogu jest uwzględniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="a085e-153">For instance, model IDs and catalog IDs are case sensitive.</span></span>

## <a name="4-recommendations-quality-and-cold-items"></a><span data-ttu-id="a085e-154">4. Zalecenia dotyczące jakości i zimnych elementów</span><span class="sxs-lookup"><span data-stu-id="a085e-154">4. Recommendations Quality and Cold Items</span></span>
### <a name="41-recommendation-quality"></a><span data-ttu-id="a085e-155">4.1.</span><span class="sxs-lookup"><span data-stu-id="a085e-155">4.1.</span></span> <span data-ttu-id="a085e-156">Zalecenie jakości</span><span class="sxs-lookup"><span data-stu-id="a085e-156">Recommendation quality</span></span>
<span data-ttu-id="a085e-157">Tworzenie modelu zalecenie jest zwykle zalecenia tooprovide za mało tooallow hello systemu.</span><span class="sxs-lookup"><span data-stu-id="a085e-157">Creating a recommendation model is usually enough tooallow hello system tooprovide recommendations.</span></span> <span data-ttu-id="a085e-158">Niemniej jednak jakości zalecenia w zależności od użycia hello przetwarzane i hello pokrycia hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="a085e-158">Nevertheless, recommendation quality varies based on hello usage processed and hello coverage of hello catalog.</span></span> <span data-ttu-id="a085e-159">Na przykład jeśli masz wiele zimnych elementów (bez użycia znaczących) systemu hello będziesz mieć trudności udostępnia zalecenia dla takiego elementu lub przy użyciu takiego elementu jako zalecana.</span><span class="sxs-lookup"><span data-stu-id="a085e-159">For example if you have a lot of cold items (items without significant usage), hello system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span></span> <span data-ttu-id="a085e-160">W kolejności tooovercome hello zimnych elementu problem hello systemu umożliwia wykorzystanie hello metadanych hello elementów tooenhance hello zalecenia.</span><span class="sxs-lookup"><span data-stu-id="a085e-160">In order tooovercome hello cold item problem, hello system allows hello use of metadata of hello items tooenhance hello recommendations.</span></span> <span data-ttu-id="a085e-161">Te metadane stanowią tooas określonej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a085e-161">This metadata is referred tooas features.</span></span> <span data-ttu-id="a085e-162">Typowe funkcje są książki autora lub filmu aktora.</span><span class="sxs-lookup"><span data-stu-id="a085e-162">Typical features are a book's author or a movie's actor.</span></span> <span data-ttu-id="a085e-163">Funkcje są udostępniane za pośrednictwem katalogu hello w postaci hello klucza i wartości ciągów.</span><span class="sxs-lookup"><span data-stu-id="a085e-163">Features are provided via hello catalog in hello form of key/value strings.</span></span> <span data-ttu-id="a085e-164">Hello pełny format pliku wykazu hello, można znaleźć w artykule toohello [zaimportować sekcja katalogu](#81-import-catalog-data).</span><span class="sxs-lookup"><span data-stu-id="a085e-164">For hello full format of hello catalog file, please refer toohello [import catalog section](#81-import-catalog-data).</span></span> 

### <a name="42-rank-build"></a><span data-ttu-id="a085e-165">4.2.</span><span class="sxs-lookup"><span data-stu-id="a085e-165">4.2.</span></span> <span data-ttu-id="a085e-166">Rank kompilacji</span><span class="sxs-lookup"><span data-stu-id="a085e-166">Rank build</span></span>
<span data-ttu-id="a085e-167">Funkcji można zwiększyć hello zalecenie modelu, ale toodo wymaga hello użycie funkcji łatwy do rozpoznania.</span><span class="sxs-lookup"><span data-stu-id="a085e-167">Features can enhance hello recommendation model, but toodo so requires hello use of meaningful features.</span></span> <span data-ttu-id="a085e-168">W tym celu wprowadzono nową kompilację — rangi kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-168">For this purpose a new build was introduced - a rank build.</span></span> <span data-ttu-id="a085e-169">Ta kompilacja zostanie rank powitania użyteczność funkcji.</span><span class="sxs-lookup"><span data-stu-id="a085e-169">This build will rank hello usefulness of features.</span></span> <span data-ttu-id="a085e-170">Funkcja łatwy do rozpoznania to funkcja z rangę 2 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="a085e-170">A meaningful feature is a feature with a rank score of 2 and up.</span></span>
<span data-ttu-id="a085e-171">Po zrozumienia, które funkcji hello są przydatne, wyzwolić kompilację zalecenie z listy hello (lub podlisty) łatwy do rozpoznania funkcji.</span><span class="sxs-lookup"><span data-stu-id="a085e-171">After understanding which of hello features are meaningful, trigger a recommendation build with hello list (or sublist) of meaningful features.</span></span> <span data-ttu-id="a085e-172">Jest to możliwe toouse, tych funkcji do rozszerzenia hello elementów ciepłych i zimnych elementów.</span><span class="sxs-lookup"><span data-stu-id="a085e-172">It is possible toouse these feature for hello enhancement of both warm items and cold items.</span></span> <span data-ttu-id="a085e-173">W kolejności toouse ich elementów ciepłych hello `UseFeatureInModel` parametru kompilacji powinny zostać skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="a085e-173">In order toouse them for warm items, hello `UseFeatureInModel` build parameter should be set up.</span></span> <span data-ttu-id="a085e-174">W funkcji toouse kolejność elementów zimnych, hello `AllowColdItemPlacement` parametru kompilacji powinno być włączone.</span><span class="sxs-lookup"><span data-stu-id="a085e-174">In order toouse features for cold items, hello `AllowColdItemPlacement` build parameter should be enabled.</span></span>
<span data-ttu-id="a085e-175">Uwaga: Nie jest możliwe tooenable `AllowColdItemPlacement` bez włączania `UseFeatureInModel`.</span><span class="sxs-lookup"><span data-stu-id="a085e-175">Note: It is not possible tooenable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span></span>

### <a name="43-recommendation-reasoning"></a><span data-ttu-id="a085e-176">4.3.</span><span class="sxs-lookup"><span data-stu-id="a085e-176">4.3.</span></span> <span data-ttu-id="a085e-177">Zalecenie logikę</span><span class="sxs-lookup"><span data-stu-id="a085e-177">Recommendation reasoning</span></span>
<span data-ttu-id="a085e-178">Rozsądkiem zalecenie jest innym aspektem użycie funkcji.</span><span class="sxs-lookup"><span data-stu-id="a085e-178">Recommendation reasoning is another aspect of feature usage.</span></span> <span data-ttu-id="a085e-179">W rzeczywistości hello Azure Machine Learning zalecenia aparat można użyć funkcji tooprovide zalecenie wyjaśnienia ()</span><span class="sxs-lookup"><span data-stu-id="a085e-179">Indeed, hello Azure Machine Learning Recommendations engine can use features tooprovide recommendation explanations (a.k.a.</span></span> <span data-ttu-id="a085e-180">uzasadnienie), prowadzące toomore zaufania w hello zalecane elementu z hello zalecenie konsumenta.</span><span class="sxs-lookup"><span data-stu-id="a085e-180">reasoning), leading toomore confidence in hello recommended item from hello recommendation consumer.</span></span>
<span data-ttu-id="a085e-181">tooenable uzasadnienie, hello `AllowFeatureCorrelation` i `ReasoningFeatureList` parametry powinny mieć toorequesting poprzednie ustawienia kompilacji zalecenia.</span><span class="sxs-lookup"><span data-stu-id="a085e-181">tooenable reasoning, hello `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior toorequesting a recommendation build.</span></span>

## <a name="5-model-basic"></a><span data-ttu-id="a085e-182">5. Basic modelu</span><span class="sxs-lookup"><span data-stu-id="a085e-182">5. Model Basic</span></span>
### <a name="51-create-model"></a><span data-ttu-id="a085e-183">5.1.</span><span class="sxs-lookup"><span data-stu-id="a085e-183">5.1.</span></span> <span data-ttu-id="a085e-184">Tworzenie modelu</span><span class="sxs-lookup"><span data-stu-id="a085e-184">Create Model</span></span>
<span data-ttu-id="a085e-185">Tworzy żądanie "Tworzenie modelu".</span><span class="sxs-lookup"><span data-stu-id="a085e-185">Creates a “create model” request.</span></span>

| <span data-ttu-id="a085e-186">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-186">HTTP Method</span></span> | <span data-ttu-id="a085e-187">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-187">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-188">POST</span><span class="sxs-lookup"><span data-stu-id="a085e-188">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-189">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-189">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-190">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-190">Parameter Name</span></span> | <span data-ttu-id="a085e-191">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-191">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-192">modelName</span><span class="sxs-lookup"><span data-stu-id="a085e-192">modelName</span></span> |<span data-ttu-id="a085e-193">Tylko litery (A-Z, a – z), cyfry (0 – 9), łączniki (-) i znak podkreślenia (_) są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="a085e-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="a085e-194">Maksymalna długość: 20</span><span class="sxs-lookup"><span data-stu-id="a085e-194">Max length: 20</span></span> |
| <span data-ttu-id="a085e-195">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-195">apiVersion</span></span> |<span data-ttu-id="a085e-196">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-196">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-197">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-197">Request Body</span></span> |<span data-ttu-id="a085e-198">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-198">NONE</span></span> |

<span data-ttu-id="a085e-199">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-199">**Response**:</span></span>

<span data-ttu-id="a085e-200">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-200">HTTP Status code: 200</span></span>

* <span data-ttu-id="a085e-201">`feed/entry/content/properties/id`-Zawiera identyfikator hello modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-201">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="a085e-202">**Uwaga**: identyfikator modelu jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="a085e-202">**Note**: model ID is case sensitive.</span></span>

<span data-ttu-id="a085e-203">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-203">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="52-get-model"></a><span data-ttu-id="a085e-204">5.2.</span><span class="sxs-lookup"><span data-stu-id="a085e-204">5.2.</span></span> <span data-ttu-id="a085e-205">Pobierz modelu</span><span class="sxs-lookup"><span data-stu-id="a085e-205">Get Model</span></span>
<span data-ttu-id="a085e-206">Tworzy żądanie "get modelu".</span><span class="sxs-lookup"><span data-stu-id="a085e-206">Creates a “get model” request.</span></span>

| <span data-ttu-id="a085e-207">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-207">HTTP Method</span></span> | <span data-ttu-id="a085e-208">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-208">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-209">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-209">GET</span></span> |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a085e-210">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-210">Example:</span></span><br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-211">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-211">Parameter Name</span></span> | <span data-ttu-id="a085e-212">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-212">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-213">id</span><span class="sxs-lookup"><span data-stu-id="a085e-213">id</span></span> |<span data-ttu-id="a085e-214">Unikatowy identyfikator modelu hello (z uwzględnieniem wielkości liter)</span><span class="sxs-lookup"><span data-stu-id="a085e-214">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="a085e-215">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-215">apiVersion</span></span> |<span data-ttu-id="a085e-216">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-216">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-217">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-217">Request Body</span></span> |<span data-ttu-id="a085e-218">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-218">NONE</span></span> |

<span data-ttu-id="a085e-219">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-219">**Response**:</span></span>

<span data-ttu-id="a085e-220">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-220">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-221">Witaj modelu danych można znaleźć w hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a085e-221">hello model data can be found under hello following elements:</span></span>

* <span data-ttu-id="a085e-222">`feed/entry/content/properties/Id`-Model unikatowego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="a085e-222">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="a085e-223">`feed/entry/content/properties/Name`-Nazwa modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-223">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="a085e-224">`feed/entry/content/properties/Date`-Data utworzenia modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-224">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="a085e-225">`feed/entry/content/properties/Status`-Stan modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-225">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="a085e-226">Jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="a085e-226">One of hello following:</span></span>
  * <span data-ttu-id="a085e-227">Utworzone — Model jest tworzony i nie zawiera katalogu i użycia.</span><span class="sxs-lookup"><span data-stu-id="a085e-227">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="a085e-228">ReadyForBuild — Model jest tworzony i zawiera katalog i użycia.</span><span class="sxs-lookup"><span data-stu-id="a085e-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="a085e-229">`feed/entry/content/properties/HasActiveBuild`— Wskazuje, czy hello model został utworzony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a085e-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="a085e-230">`feed/entry/content/properties/BuildId`-Identyfikator modelu active kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="a085e-231">`feed/entry/content/properties/Mpr`-Model klasyfikacji średniej percentyl (MPR — Aby uzyskać więcej informacji, zobacz ModelInsight).</span><span class="sxs-lookup"><span data-stu-id="a085e-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span></span>
* <span data-ttu-id="a085e-232">`feed/entry/content/properties/UserName`-Nazwa użytkownika wewnętrznego modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-232">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>

<span data-ttu-id="a085e-233">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-233">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a><span data-ttu-id="a085e-234">5.3.</span><span class="sxs-lookup"><span data-stu-id="a085e-234">5.3.</span></span>    <span data-ttu-id="a085e-235">Pobierz wszystkie modele</span><span class="sxs-lookup"><span data-stu-id="a085e-235">Get All Models</span></span>
<span data-ttu-id="a085e-236">Pobiera wszystkie modele hello bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a085e-236">Retrieves all models of hello current user.</span></span>

| <span data-ttu-id="a085e-237">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-237">HTTP Method</span></span> | <span data-ttu-id="a085e-238">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-238">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-239">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-239">GET</span></span> |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br><span data-ttu-id="a085e-240">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-240">Example:</span></span><br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-241">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-241">Parameter Name</span></span> | <span data-ttu-id="a085e-242">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-242">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-243">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-243">apiVersion</span></span> |<span data-ttu-id="a085e-244">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-244">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-245">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-245">Request Body</span></span> |<span data-ttu-id="a085e-246">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-246">NONE</span></span> |

<span data-ttu-id="a085e-247">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-247">**Response**:</span></span>

<span data-ttu-id="a085e-248">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-248">HTTP Status code: 200</span></span>

* <span data-ttu-id="a085e-249">`feed/entry/content/properties/Id`-Model unikatowego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="a085e-249">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="a085e-250">`feed/entry/content/properties/Name`-Nazwa modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-250">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="a085e-251">`feed/entry/content/properties/Date`-Data utworzenia modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-251">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="a085e-252">`feed/entry/content/properties/Status`-Stan modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-252">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="a085e-253">Jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="a085e-253">One of hello following:</span></span>
  * <span data-ttu-id="a085e-254">Utworzone — Model jest tworzony i nie zawiera katalogu i użycia.</span><span class="sxs-lookup"><span data-stu-id="a085e-254">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="a085e-255">ReadyForBuild — Model jest tworzony i zawiera katalog i użycia.</span><span class="sxs-lookup"><span data-stu-id="a085e-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="a085e-256">`feed/entry/content/properties/HasActiveBuild`— Wskazuje, czy hello model został utworzony pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a085e-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="a085e-257">`feed/entry/content/properties/BuildId`-Identyfikator modelu active kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="a085e-258">`feed/entry/content/properties/Mpr`-Model MPR (więcej informacji zawiera ModelInsight).</span><span class="sxs-lookup"><span data-stu-id="a085e-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span></span>
* <span data-ttu-id="a085e-259">`feed/entry/content/properties/UserName`-Nazwa użytkownika wewnętrznego modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-259">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>
* <span data-ttu-id="a085e-260">`feed/entry/content/properties/UsageFileNames`— Lista plików użycia modelu rozdzielonych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="a085e-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span></span>
* <span data-ttu-id="a085e-261">`feed/entry/content/properties/CatalogId`-Identyfikator modelu katalogu.</span><span class="sxs-lookup"><span data-stu-id="a085e-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span></span>
* <span data-ttu-id="a085e-262">`feed/entry/content/properties/Description`-Opis modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-262">`feed/entry/content/properties/Description` - Model description.</span></span>
* <span data-ttu-id="a085e-263">`feed/entry/content/properties/CatalogFileName`-Nazwa pliku katalogu modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span></span>

<span data-ttu-id="a085e-264">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-264">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a><span data-ttu-id="a085e-265">5.4.</span><span class="sxs-lookup"><span data-stu-id="a085e-265">5.4.</span></span>    <span data-ttu-id="a085e-266">Aktualizuj Model</span><span class="sxs-lookup"><span data-stu-id="a085e-266">Update Model</span></span>
<span data-ttu-id="a085e-267">Możesz zaktualizować opis modelu hello lub hello identyfikator active kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-267">You can update hello model description or hello active build ID.</span></span><br><span data-ttu-id="a085e-268">
<ins>Identyfikator kompilacji Active</ins> -każdej kompilacji dla każdego modelu ma identyfikator kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-268">
<ins>Active build ID</ins> - Every build for every model has a build ID.</span></span> <span data-ttu-id="a085e-269">Identyfikator kompilacji active Hello jest hello pierwszym pomyślnym kompilacji każdego nowego modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-269">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="a085e-270">Gdy masz identyfikator active kompilacji i wykonaj dodatkowe kompilacje dla hello samego modelu należy tooexplicitly ustaw go jako hello domyślne kompilacji identyfikator aby.</span><span class="sxs-lookup"><span data-stu-id="a085e-270">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="a085e-271">Jeśli zalecenia, korzystać w sytuacji, jeśli nie określono Identyfikatora kompilacji hello, który ma toouse, domyślne hello, co zostanie użyta automatycznie.</span><span class="sxs-lookup"><span data-stu-id="a085e-271">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span><br>
<span data-ttu-id="a085e-272">Mechanizm ten umożliwia — po modelu zalecenia w środowisku produkcyjnym — toobuild nowe modele i testowane przed podwyższeniem ich tooproduction.</span><span class="sxs-lookup"><span data-stu-id="a085e-272">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="a085e-273">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-273">HTTP Method</span></span> | <span data-ttu-id="a085e-274">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-275">UMIEŚĆ</span><span class="sxs-lookup"><span data-stu-id="a085e-275">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a085e-276">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-276">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-277">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-277">Parameter Name</span></span> | <span data-ttu-id="a085e-278">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-278">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-279">id</span><span class="sxs-lookup"><span data-stu-id="a085e-279">id</span></span> |<span data-ttu-id="a085e-280">Unikatowy identyfikator modelu hello (z uwzględnieniem wielkości liter)</span><span class="sxs-lookup"><span data-stu-id="a085e-280">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="a085e-281">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-281">apiVersion</span></span> |<span data-ttu-id="a085e-282">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-282">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-283">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-283">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br><span data-ttu-id="a085e-284">Należy pamiętać, że hello XML znaczniki opis i ActiveBuildId są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="a085e-284">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="a085e-285">Jeśli nie chcesz, aby tooset opis lub ActiveBuildId, usuń cały tag hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-285">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="a085e-286">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-286">**Response**:</span></span>

<span data-ttu-id="a085e-287">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-287">HTTP Status code: 200</span></span>

### <a name="55----delete-model"></a><span data-ttu-id="a085e-288">5.5.</span><span class="sxs-lookup"><span data-stu-id="a085e-288">5.5.</span></span>    <span data-ttu-id="a085e-289">Usuń Model</span><span class="sxs-lookup"><span data-stu-id="a085e-289">Delete Model</span></span>
<span data-ttu-id="a085e-290">Usuwa istniejącego modelu według identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="a085e-290">Deletes an existing model by ID.</span></span>

| <span data-ttu-id="a085e-291">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-291">HTTP Method</span></span> | <span data-ttu-id="a085e-292">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-292">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-293">USUŃ</span><span class="sxs-lookup"><span data-stu-id="a085e-293">DELETE</span></span> |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a085e-294">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-294">Example:</span></span><br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-295">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-295">Parameter Name</span></span> | <span data-ttu-id="a085e-296">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-296">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-297">id</span><span class="sxs-lookup"><span data-stu-id="a085e-297">id</span></span> |<span data-ttu-id="a085e-298">Unikatowy identyfikator modelu hello (z uwzględnieniem wielkości liter)</span><span class="sxs-lookup"><span data-stu-id="a085e-298">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="a085e-299">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-299">apiVersion</span></span> |<span data-ttu-id="a085e-300">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-300">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-301">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-301">Request Body</span></span> |<span data-ttu-id="a085e-302">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-302">NONE</span></span> |

<span data-ttu-id="a085e-303">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-303">**Response**:</span></span>

<span data-ttu-id="a085e-304">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-304">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-305">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-305">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a><span data-ttu-id="a085e-306">6. Zaawansowane modelu</span><span class="sxs-lookup"><span data-stu-id="a085e-306">6. Model Advanced</span></span>
### <a name="61----model-data-insight"></a><span data-ttu-id="a085e-307">6.1.</span><span class="sxs-lookup"><span data-stu-id="a085e-307">6.1.</span></span>    <span data-ttu-id="a085e-308">Szczegółowe informacje o modelu danych</span><span class="sxs-lookup"><span data-stu-id="a085e-308">Model Data Insight</span></span>
<span data-ttu-id="a085e-309">Zwraca dane statystyczne hello użycia danych, których ten model został skompilowany.</span><span class="sxs-lookup"><span data-stu-id="a085e-309">Returns statistical data on hello usage data that this model was built with.</span></span>

<span data-ttu-id="a085e-310">Dostępna tylko w przypadku kompilacji zalecenia.</span><span class="sxs-lookup"><span data-stu-id="a085e-310">Available only for Recommendation build.</span></span>

| <span data-ttu-id="a085e-311">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-311">HTTP Method</span></span> | <span data-ttu-id="a085e-312">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-312">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-313">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-313">GET</span></span> |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a085e-314">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-314">Example:</span></span><br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-315">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-315">Parameter Name</span></span> | <span data-ttu-id="a085e-316">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-316">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-317">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-317">modelId</span></span> |<span data-ttu-id="a085e-318">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-318">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-319">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-319">apiVersion</span></span> |<span data-ttu-id="a085e-320">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-320">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-321">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-321">Request Body</span></span> |<span data-ttu-id="a085e-322">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-322">NONE</span></span> |

<span data-ttu-id="a085e-323">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-323">**Response**:</span></span>

<span data-ttu-id="a085e-324">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-324">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-325">Witaj, dane są zwracane jako zbiór właściwości.</span><span class="sxs-lookup"><span data-stu-id="a085e-325">hello data is returned as a collection of properties.</span></span>

* <span data-ttu-id="a085e-326">`feed/entry/id/content/properties/key`-Zawiera nazwę właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-326">`feed/entry/id/content/properties/key` - Holds hello property name.</span></span>
* <span data-ttu-id="a085e-327">`feed/entry/id/content/properties/value`-Zawiera wartość właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-327">`feed/entry/id/content/properties/value` - Holds hello property value.</span></span>

<span data-ttu-id="a085e-328">Witaj w poniższej tabeli przedstawiono hello wartość, która reprezentuje każdy klucz.</span><span class="sxs-lookup"><span data-stu-id="a085e-328">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="a085e-329">Klucz</span><span class="sxs-lookup"><span data-stu-id="a085e-329">Key</span></span> | <span data-ttu-id="a085e-330">Opis</span><span class="sxs-lookup"><span data-stu-id="a085e-330">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-331">AvgItemLength</span><span class="sxs-lookup"><span data-stu-id="a085e-331">AvgItemLength</span></span> |<span data-ttu-id="a085e-332">Średnia liczba unikatowych użytkowników, dla każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="a085e-332">Average number of distinct users per item.</span></span> |
| <span data-ttu-id="a085e-333">AvgUserLength</span><span class="sxs-lookup"><span data-stu-id="a085e-333">AvgUserLength</span></span> |<span data-ttu-id="a085e-334">Średnia liczba unikatowych elementów dla każdego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a085e-334">Average number of distinct items per user.</span></span> |
| <span data-ttu-id="a085e-335">DensificationNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="a085e-335">DensificationNumberOfItems</span></span> |<span data-ttu-id="a085e-336">Liczba elementów po elementach oczyszczania, które nie mogą być modelowane.</span><span class="sxs-lookup"><span data-stu-id="a085e-336">Number of items after pruning items that cannot be modelled.</span></span> |
| <span data-ttu-id="a085e-337">DensificationNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="a085e-337">DensificationNumberOfUsers</span></span> |<span data-ttu-id="a085e-338">Liczba punktów użycia po oczyszczania użytkowników i elementy, które nie mogą być modelowane.</span><span class="sxs-lookup"><span data-stu-id="a085e-338">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="a085e-339">DensificationNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="a085e-339">DensificationNumberOfRecords</span></span> |<span data-ttu-id="a085e-340">Liczba punktów użycia po oczyszczania użytkowników i elementy, które nie mogą być modelowane.</span><span class="sxs-lookup"><span data-stu-id="a085e-340">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="a085e-341">MaxItemLength</span><span class="sxs-lookup"><span data-stu-id="a085e-341">MaxItemLength</span></span> |<span data-ttu-id="a085e-342">Liczba unikatowych użytkowników dla elementu najpopularniejszych hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-342">Number of distinct users for hello most popular item.</span></span> |
| <span data-ttu-id="a085e-343">MaxUserLength</span><span class="sxs-lookup"><span data-stu-id="a085e-343">MaxUserLength</span></span> |<span data-ttu-id="a085e-344">Maksymalna liczba unikatowych elementów dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a085e-344">Maximal number of distinct items for a user.</span></span> |
| <span data-ttu-id="a085e-345">MinItemLength</span><span class="sxs-lookup"><span data-stu-id="a085e-345">MinItemLength</span></span> |<span data-ttu-id="a085e-346">Maksymalna liczba różnych użytkowników dla elementu.</span><span class="sxs-lookup"><span data-stu-id="a085e-346">Maximal number of distinct users for an item.</span></span> |
| <span data-ttu-id="a085e-347">MinUserLength</span><span class="sxs-lookup"><span data-stu-id="a085e-347">MinUserLength</span></span> |<span data-ttu-id="a085e-348">Minimalna liczba unikatowych elementów dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a085e-348">Minimal number of distinct items for a user.</span></span> |
| <span data-ttu-id="a085e-349">RawNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="a085e-349">RawNumberOfItems</span></span> |<span data-ttu-id="a085e-350">Liczba elementów w plikach użycia hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-350">Number of items in hello usage files.</span></span> |
| <span data-ttu-id="a085e-351">RawNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="a085e-351">RawNumberOfUsers</span></span> |<span data-ttu-id="a085e-352">Liczba punktów użycia przed żadnych oczyszczania.</span><span class="sxs-lookup"><span data-stu-id="a085e-352">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="a085e-353">RawNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="a085e-353">RawNumberOfRecords</span></span> |<span data-ttu-id="a085e-354">Liczba punktów użycia przed żadnych oczyszczania.</span><span class="sxs-lookup"><span data-stu-id="a085e-354">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="a085e-355">SamplingNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="a085e-355">SamplingNumberOfItems</span></span> |<span data-ttu-id="a085e-356">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="a085e-356">N/A</span></span> |
| <span data-ttu-id="a085e-357">SamplingNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="a085e-357">SamplingNumberOfRecords</span></span> |<span data-ttu-id="a085e-358">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="a085e-358">N/A</span></span> |
| <span data-ttu-id="a085e-359">SamplingNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="a085e-359">SamplingNumberOfUsers</span></span> |<span data-ttu-id="a085e-360">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="a085e-360">N/A</span></span> |

<span data-ttu-id="a085e-361">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-361">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a><span data-ttu-id="a085e-362">6.2.</span><span class="sxs-lookup"><span data-stu-id="a085e-362">6.2.</span></span>    <span data-ttu-id="a085e-363">Szczegółowe informacje o modelu</span><span class="sxs-lookup"><span data-stu-id="a085e-363">Model Insight</span></span>
<span data-ttu-id="a085e-364">Zwraca model szczegółowe informacje o kompilacji active hello lub (jeśli istnieje) w ramach określonej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-364">Returns model insight on hello active build or (if given) on a specific build.</span></span>

<span data-ttu-id="a085e-365">Dostępna tylko w przypadku kompilacji zalecenia.</span><span class="sxs-lookup"><span data-stu-id="a085e-365">Available only for Recommendation build.</span></span>

| <span data-ttu-id="a085e-366">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-366">HTTP Method</span></span> | <span data-ttu-id="a085e-367">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-367">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-368">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-368">GET</span></span> |<span data-ttu-id="a085e-369">O identyfikatorze active kompilacji:</span><span class="sxs-lookup"><span data-stu-id="a085e-369">With active build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-370">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-370">Example:</span></span><br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-371">O identyfikatorze określonej kompilacji:</span><span class="sxs-lookup"><span data-stu-id="a085e-371">With specific build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-372">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-372">Parameter Name</span></span> | <span data-ttu-id="a085e-373">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-373">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-374">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-374">modelId</span></span> |<span data-ttu-id="a085e-375">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-375">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-376">identyfikatora buildId</span><span class="sxs-lookup"><span data-stu-id="a085e-376">buildId</span></span> |<span data-ttu-id="a085e-377">Opcjonalne — liczba, która identyfikuje pomyślnego utworzenia kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-377">Optional - number that identifies a successful build.</span></span> |
| <span data-ttu-id="a085e-378">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-378">apiVersion</span></span> |<span data-ttu-id="a085e-379">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-379">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-380">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-380">Request Body</span></span> |<span data-ttu-id="a085e-381">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-381">NONE</span></span> |

<span data-ttu-id="a085e-382">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-382">**Response**:</span></span>

<span data-ttu-id="a085e-383">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-383">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-384">Witaj, dane są zwracane jako zbiór właściwości.</span><span class="sxs-lookup"><span data-stu-id="a085e-384">hello data is returned as a collection of properties.</span></span>

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

<span data-ttu-id="a085e-385">Witaj w poniższej tabeli przedstawiono hello wartość, która reprezentuje każdy klucz.</span><span class="sxs-lookup"><span data-stu-id="a085e-385">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="a085e-386">Klucz</span><span class="sxs-lookup"><span data-stu-id="a085e-386">Key</span></span> | <span data-ttu-id="a085e-387">Opis</span><span class="sxs-lookup"><span data-stu-id="a085e-387">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-388">CatalogCoverage</span><span class="sxs-lookup"><span data-stu-id="a085e-388">CatalogCoverage</span></span> |<span data-ttu-id="a085e-389">Jaka część hello katalogu może być modelowane z wzorców użycia.</span><span class="sxs-lookup"><span data-stu-id="a085e-389">What part of hello catalog can be modelled with usage patterns.</span></span> <span data-ttu-id="a085e-390">Witaj pozostałe elementy hello należy funkcje na podstawie zawartości.</span><span class="sxs-lookup"><span data-stu-id="a085e-390">hello rest of hello items will need content-based features.</span></span> |
| <span data-ttu-id="a085e-391">MPR</span><span class="sxs-lookup"><span data-stu-id="a085e-391">Mpr</span></span> |<span data-ttu-id="a085e-392">Oznacza klasyfikacji percentyl hello modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-392">Mean percentile ranking of hello model.</span></span> <span data-ttu-id="a085e-393">Dolna jest lepszym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="a085e-393">Lower is better.</span></span> |
| <span data-ttu-id="a085e-394">NumberOfDimensions</span><span class="sxs-lookup"><span data-stu-id="a085e-394">NumberOfDimensions</span></span> |<span data-ttu-id="a085e-395">Liczba wymiarów używanych przez algorytm factorization macierzy hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-395">Number of dimensions used by hello matrix factorization algorithm.</span></span> |

<span data-ttu-id="a085e-396">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-396">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a><span data-ttu-id="a085e-397">6.3.</span><span class="sxs-lookup"><span data-stu-id="a085e-397">6.3.</span></span>    <span data-ttu-id="a085e-398">Pobierz przykładowe modelu</span><span class="sxs-lookup"><span data-stu-id="a085e-398">Get Model Sample</span></span>
<span data-ttu-id="a085e-399">Pobiera próbkę hello zalecenie modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-399">Gets a sample of hello recommendation model.</span></span>

| <span data-ttu-id="a085e-400">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-400">HTTP Method</span></span> | <span data-ttu-id="a085e-401">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-401">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-402">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-402">GET</span></span> |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a085e-403">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-403">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-404">O identyfikatorze określonej kompilacji:</span><span class="sxs-lookup"><span data-stu-id="a085e-404">With specific build ID:</span></span><br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a085e-405">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-405">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-406">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-406">Parameter Name</span></span> | <span data-ttu-id="a085e-407">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-407">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-408">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-408">modelId</span></span> |<span data-ttu-id="a085e-409">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-409">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-410">apiVersion</span></span> |<span data-ttu-id="a085e-411">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-411">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-412">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-412">Request Body</span></span> |<span data-ttu-id="a085e-413">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-413">NONE</span></span> |

<span data-ttu-id="a085e-414">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-414">**Response**:</span></span>

<span data-ttu-id="a085e-415">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-415">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-416">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-416">OData XML</span></span>

<span data-ttu-id="a085e-417">Odpowiedź zostanie zwrócona w formacie tekstowym raw:</span><span class="sxs-lookup"><span data-stu-id="a085e-417">Response is returned in raw text format:</span></span>

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a><span data-ttu-id="a085e-418">7. Reguły biznesowe modelu</span><span class="sxs-lookup"><span data-stu-id="a085e-418">7. Model Business Rules</span></span>
<span data-ttu-id="a085e-419">Są to typy hello reguł obsługiwane:</span><span class="sxs-lookup"><span data-stu-id="a085e-419">These are hello types of rules supported:</span></span>

* <span data-ttu-id="a085e-420"><strong>BlockList</strong> -BlockList umożliwia tooprovide listę elementów, które chcesz tooreturn w wynikach zalecenie hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-420"><strong>BlockList</strong> - BlockList enables you tooprovide a list of items that you do not want tooreturn in hello recommendation results.</span></span> 
* <span data-ttu-id="a085e-421"><strong>FeatureBlockList</strong> — funkcja BlockList umożliwia możesz tooblock elementy na podstawie wartości hello jego funkcje.</span><span class="sxs-lookup"><span data-stu-id="a085e-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you tooblock items based on hello values of its features.</span></span>

<span data-ttu-id="a085e-422">*Nie wysyłaj więcej niż 1000 pozycji w regule pojedynczego blocklist lub wywołania mogą limitu czasu. Jeśli potrzebujesz tooblock więcej niż 1000 pozycji, można wprowadzić kilka wywołań blocklist.*</span><span class="sxs-lookup"><span data-stu-id="a085e-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need tooblock more than 1000 items, you can make several blocklist calls.*</span></span>

* <span data-ttu-id="a085e-423"><strong>Upsale</strong> -Upsale umożliwia tooenforce tooreturn elementów w wynikach zalecenie hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-423"><strong>Upsale</strong> - Upsale enables you tooenforce items tooreturn in hello recommendation results.</span></span>
* <span data-ttu-id="a085e-424"><strong>Lista dozwolonych adresów</strong> — umożliwia białą listę tooonly możesz Sugeruj zalecenia z listy elementów.</span><span class="sxs-lookup"><span data-stu-id="a085e-424"><strong>WhiteList</strong> - White List enables you tooonly suggest recommendations from a list of items.</span></span>
* <span data-ttu-id="a085e-425"><strong>FeatureWhiteList</strong> — funkcja białą listę umożliwia tooonly zaleca się elementy, które mają wartości określonych funkcji.</span><span class="sxs-lookup"><span data-stu-id="a085e-425"><strong>FeatureWhiteList</strong> - Feature White List enables you tooonly recommend items that have specific feature values.</span></span>
* <span data-ttu-id="a085e-426"><strong>PerSeedBlockList</strong> — na zablokowanych inicjatora umożliwia tooprovide na element listę elementów, które nie może być zwracany jako wyniki zalecenie.</span><span class="sxs-lookup"><span data-stu-id="a085e-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you tooprovide per item a list of items that cannot be returned as recommendation results.</span></span>

### <a name="71----get-model-rules"></a><span data-ttu-id="a085e-427">7.1.</span><span class="sxs-lookup"><span data-stu-id="a085e-427">7.1.</span></span>    <span data-ttu-id="a085e-428">Pobieranie reguł modelu</span><span class="sxs-lookup"><span data-stu-id="a085e-428">Get Model Rules</span></span>
| <span data-ttu-id="a085e-429">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-429">HTTP Method</span></span> | <span data-ttu-id="a085e-430">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-430">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-431">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-431">GET</span></span> |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="a085e-432">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-432">Example:</span></span><br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-433">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-433">Parameter Name</span></span> | <span data-ttu-id="a085e-434">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-434">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-435">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-435">modelId</span></span> |<span data-ttu-id="a085e-436">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-436">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-437">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-437">apiVersion</span></span> |<span data-ttu-id="a085e-438">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-438">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-439">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-439">Request Body</span></span> |<span data-ttu-id="a085e-440">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-440">NONE</span></span> |

<span data-ttu-id="a085e-441">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-441">**Response**:</span></span>

<span data-ttu-id="a085e-442">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-442">HTTP Status code: 200</span></span>

* <span data-ttu-id="a085e-443">`feed/entry/content/properties/Id`-Unikatowy identyfikator tej reguły.</span><span class="sxs-lookup"><span data-stu-id="a085e-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="a085e-444">`feed/entry/content/properties/Type`-Typ reguły hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-444">`feed/entry/content/properties/Type` - Type of hello rule.</span></span>
* <span data-ttu-id="a085e-445">`feed/entry/content/properties/Parameter`-Parametr reguły.</span><span class="sxs-lookup"><span data-stu-id="a085e-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="a085e-446">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-446">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a><span data-ttu-id="a085e-447">7.2.</span><span class="sxs-lookup"><span data-stu-id="a085e-447">7.2.</span></span>    <span data-ttu-id="a085e-448">Dodaj regułę</span><span class="sxs-lookup"><span data-stu-id="a085e-448">Add Rule</span></span>
| <span data-ttu-id="a085e-449">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-449">HTTP Method</span></span> | <span data-ttu-id="a085e-450">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-450">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-451">POST</span><span class="sxs-lookup"><span data-stu-id="a085e-451">POST</span></span> |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| <span data-ttu-id="a085e-452">NAGŁÓWEK</span><span class="sxs-lookup"><span data-stu-id="a085e-452">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="a085e-453">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-453">Parameter Name</span></span> | <span data-ttu-id="a085e-454">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-454">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-455">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-455">apiVersion</span></span> |<span data-ttu-id="a085e-456">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-456">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-457">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-457">Request Body</span></span> | |

<span data-ttu-id="a085e-458"><ins>Zawsze, gdy w przypadku reguł biznesowych, zapewniając identyfikatory elementów, upewnij się, że toouse hello zewnętrznych identyfikator elementu hello (hello na tym samym identyfikatorze używanego w pliku wykazu hello)</ins></span><span class="sxs-lookup"><span data-stu-id="a085e-458"><ins>Whenever providing Item Ids for business rules, make sure toouse hello External Id of hello item (hello same Id that you used in hello catalog file)</ins></span></span><br><span data-ttu-id="a085e-459">
<ins>Reguła BlockList tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="a085e-459">
<ins>tooadd a BlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="a085e-460"><ins>
<ins>Reguła FeatureBlockList tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="a085e-460"><ins>
<ins>tooadd a FeatureBlockList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><span data-ttu-id="a085e-461"><ins>Reguła Upsale tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="a085e-461"><ins> tooadd an Upsale rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br><span data-ttu-id="a085e-462">
<ins>tooadd regułę listy dozwolonych adresów IP:</ins></span><span class="sxs-lookup"><span data-stu-id="a085e-462">
<ins>tooadd a WhiteList rule:</ins></span></span><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="a085e-463"><ins>
<ins>Reguła FeatureWhiteList tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="a085e-463"><ins>
<ins>tooadd a FeatureWhiteList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><span data-ttu-id="a085e-464"><ins>Reguła PerSeedBlockList tooadd:</ins></span><span class="sxs-lookup"><span data-stu-id="a085e-464"><ins> tooadd a PerSeedBlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

<span data-ttu-id="a085e-465">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-465">**Response**:</span></span>

<span data-ttu-id="a085e-466">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-466">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-467">Witaj interfejsu API zwraca hello nowo utworzona reguła z jego szczegółami.</span><span class="sxs-lookup"><span data-stu-id="a085e-467">hello API returns hello newly created rule with its details.</span></span> <span data-ttu-id="a085e-468">Właściwości reguł Hello mogą być pobierane z hello następującej ścieżki:</span><span class="sxs-lookup"><span data-stu-id="a085e-468">hello rules property can be retrieved from hello following paths:</span></span>

* <span data-ttu-id="a085e-469">`feed/entry/content/properties/Id`-Unikatowy identyfikator tej reguły.</span><span class="sxs-lookup"><span data-stu-id="a085e-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="a085e-470">`feed/entry/content/properties/Type`-Typ reguły hello: BlockList lub Upsale.</span><span class="sxs-lookup"><span data-stu-id="a085e-470">`feed/entry/content/properties/Type` - Type of hello rule: BlockList or Upsale.</span></span>
* <span data-ttu-id="a085e-471">`feed/entry/content/properties/Parameter`-Parametr reguły.</span><span class="sxs-lookup"><span data-stu-id="a085e-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="a085e-472">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-472">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a><span data-ttu-id="a085e-473">7.3.</span><span class="sxs-lookup"><span data-stu-id="a085e-473">7.3.</span></span>    <span data-ttu-id="a085e-474">Usuń regułę</span><span class="sxs-lookup"><span data-stu-id="a085e-474">Delete Rule</span></span>
| <span data-ttu-id="a085e-475">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-475">HTTP Method</span></span> | <span data-ttu-id="a085e-476">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-476">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-477">USUŃ</span><span class="sxs-lookup"><span data-stu-id="a085e-477">DELETE</span></span> |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-478">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-478">Example:</span></span><br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-479">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-479">Parameter Name</span></span> | <span data-ttu-id="a085e-480">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-480">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-481">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-481">modelId</span></span> |<span data-ttu-id="a085e-482">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-482">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-483">wartości filterId</span><span class="sxs-lookup"><span data-stu-id="a085e-483">filterId</span></span> |<span data-ttu-id="a085e-484">Unikatowy identyfikator hello filtru</span><span class="sxs-lookup"><span data-stu-id="a085e-484">Unique identifier of hello filter</span></span> |
| <span data-ttu-id="a085e-485">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-485">apiVersion</span></span> |<span data-ttu-id="a085e-486">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-486">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-487">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-487">Request Body</span></span> |<span data-ttu-id="a085e-488">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-488">NONE</span></span> |

<span data-ttu-id="a085e-489">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-489">**Response**:</span></span>

<span data-ttu-id="a085e-490">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-490">HTTP Status code: 200</span></span>

### <a name="74----delete-all-rules"></a><span data-ttu-id="a085e-491">7.4.</span><span class="sxs-lookup"><span data-stu-id="a085e-491">7.4.</span></span>    <span data-ttu-id="a085e-492">Usuń wszystkie reguły</span><span class="sxs-lookup"><span data-stu-id="a085e-492">Delete All Rules</span></span>
| <span data-ttu-id="a085e-493">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-493">HTTP Method</span></span> | <span data-ttu-id="a085e-494">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-495">USUŃ</span><span class="sxs-lookup"><span data-stu-id="a085e-495">DELETE</span></span> |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-496">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-496">Example:</span></span><br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-497">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-497">Parameter Name</span></span> | <span data-ttu-id="a085e-498">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-499">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-499">modelId</span></span> |<span data-ttu-id="a085e-500">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-501">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-501">apiVersion</span></span> |<span data-ttu-id="a085e-502">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-502">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-503">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-503">Request Body</span></span> |<span data-ttu-id="a085e-504">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-504">NONE</span></span> |

<span data-ttu-id="a085e-505">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-505">**Response**:</span></span>

<span data-ttu-id="a085e-506">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-506">HTTP Status code: 200</span></span>

## <a name="8-catalog"></a><span data-ttu-id="a085e-507">8. Katalogu</span><span class="sxs-lookup"><span data-stu-id="a085e-507">8. Catalog</span></span>
### <a name="81----import-catalog-data"></a><span data-ttu-id="a085e-508">8.1.</span><span class="sxs-lookup"><span data-stu-id="a085e-508">8.1.</span></span>    <span data-ttu-id="a085e-509">Importuj dane katalogu</span><span class="sxs-lookup"><span data-stu-id="a085e-509">Import Catalog Data</span></span>
<span data-ttu-id="a085e-510">Po wysłaniu kilka katalogu plików toohello sam model z kilka wywołań możemy zostanie wstawiona tylko hello nowych elementów katalogu.</span><span class="sxs-lookup"><span data-stu-id="a085e-510">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="a085e-511">Istniejące elementy pozostanie z hello oryginalnych wartości.</span><span class="sxs-lookup"><span data-stu-id="a085e-511">Existing items will remain with hello original values.</span></span> <span data-ttu-id="a085e-512">Nie można zaktualizować katalogu danych za pomocą tej metody.</span><span class="sxs-lookup"><span data-stu-id="a085e-512">You cannot update catalog data by using this method.</span></span>

<span data-ttu-id="a085e-513">dane wykazu Hello należy stosować hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="a085e-513">hello catalog data should follow hello following format:</span></span>

* <span data-ttu-id="a085e-514">Bez funkcji-`<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span><span class="sxs-lookup"><span data-stu-id="a085e-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span></span>
* <span data-ttu-id="a085e-515">Dzięki funkcjom-`<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span><span class="sxs-lookup"><span data-stu-id="a085e-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span></span>

<span data-ttu-id="a085e-516">Uwaga: hello maksymalny rozmiar pliku to 200MB.</span><span class="sxs-lookup"><span data-stu-id="a085e-516">Note: hello maximum file size is 200MB.</span></span>

<span data-ttu-id="a085e-517">** Formatuj szczegóły **</span><span class="sxs-lookup"><span data-stu-id="a085e-517">** Format details **</span></span>

| <span data-ttu-id="a085e-518">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a085e-518">Name</span></span> | <span data-ttu-id="a085e-519">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="a085e-519">Mandatory</span></span> | <span data-ttu-id="a085e-520">Typ</span><span class="sxs-lookup"><span data-stu-id="a085e-520">Type</span></span> | <span data-ttu-id="a085e-521">Opis</span><span class="sxs-lookup"><span data-stu-id="a085e-521">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a085e-522">Identyfikator elementu</span><span class="sxs-lookup"><span data-stu-id="a085e-522">Item Id</span></span> |<span data-ttu-id="a085e-523">Tak</span><span class="sxs-lookup"><span data-stu-id="a085e-523">Yes</span></span> |<span data-ttu-id="a085e-524">[A-z], [a-z], [0-9] [_] &#40; Podkreślenie &#41; [-] &#40; Dash &#41;</span><span class="sxs-lookup"><span data-stu-id="a085e-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="a085e-525">Długość maksymalna: 50</span><span class="sxs-lookup"><span data-stu-id="a085e-525">Max length: 50</span></span> |<span data-ttu-id="a085e-526">Unikatowy identyfikator elementu.</span><span class="sxs-lookup"><span data-stu-id="a085e-526">Unique identifier of an item.</span></span> |
| <span data-ttu-id="a085e-527">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="a085e-527">Item Name</span></span> |<span data-ttu-id="a085e-528">Tak</span><span class="sxs-lookup"><span data-stu-id="a085e-528">Yes</span></span> |<span data-ttu-id="a085e-529">Dowolne znaki alfanumeryczne</span><span class="sxs-lookup"><span data-stu-id="a085e-529">Any alphanumeric characters</span></span><br> <span data-ttu-id="a085e-530">Maksymalna długość: 255</span><span class="sxs-lookup"><span data-stu-id="a085e-530">Max length: 255</span></span> |<span data-ttu-id="a085e-531">Nazwa elementu.</span><span class="sxs-lookup"><span data-stu-id="a085e-531">Item name.</span></span> |
| <span data-ttu-id="a085e-532">Kategoria elementu</span><span class="sxs-lookup"><span data-stu-id="a085e-532">Item Category</span></span> |<span data-ttu-id="a085e-533">Tak</span><span class="sxs-lookup"><span data-stu-id="a085e-533">Yes</span></span> |<span data-ttu-id="a085e-534">Dowolne znaki alfanumeryczne</span><span class="sxs-lookup"><span data-stu-id="a085e-534">Any alphanumeric characters</span></span> <br> <span data-ttu-id="a085e-535">Maksymalna długość: 255</span><span class="sxs-lookup"><span data-stu-id="a085e-535">Max length: 255</span></span> |<span data-ttu-id="a085e-536">Kategoria toowhich ten element należy (np. gotowania książki teatralne...); może być pusta.</span><span class="sxs-lookup"><span data-stu-id="a085e-536">Category toowhich this item belongs (e.g. Cooking Books, Drama…); can be empty.</span></span> |
| <span data-ttu-id="a085e-537">Opis</span><span class="sxs-lookup"><span data-stu-id="a085e-537">Description</span></span> |<span data-ttu-id="a085e-538">Nie, chyba, że funkcje są istnieje (ale nie może być puste)</span><span class="sxs-lookup"><span data-stu-id="a085e-538">No, unless features are present (but can be empty)</span></span> |<span data-ttu-id="a085e-539">Dowolne znaki alfanumeryczne</span><span class="sxs-lookup"><span data-stu-id="a085e-539">Any alphanumeric characters</span></span> <br> <span data-ttu-id="a085e-540">Maksymalna długość: 4000</span><span class="sxs-lookup"><span data-stu-id="a085e-540">Max length: 4000</span></span> |<span data-ttu-id="a085e-541">Opis tego elementu.</span><span class="sxs-lookup"><span data-stu-id="a085e-541">Description of this item.</span></span> |
| <span data-ttu-id="a085e-542">Lista funkcji</span><span class="sxs-lookup"><span data-stu-id="a085e-542">Features list</span></span> |<span data-ttu-id="a085e-543">Nie</span><span class="sxs-lookup"><span data-stu-id="a085e-543">No</span></span> |<span data-ttu-id="a085e-544">Dowolne znaki alfanumeryczne</span><span class="sxs-lookup"><span data-stu-id="a085e-544">Any alphanumeric characters</span></span> <br> <span data-ttu-id="a085e-545">Maksymalna długość: 4000; Maksymalna liczba funkcji: 20</span><span class="sxs-lookup"><span data-stu-id="a085e-545">Max length: 4000; Max number of features:20</span></span> |<span data-ttu-id="a085e-546">Rozdzielana przecinkami lista nazwy funkcji = wartość funkcji, które mogą być używane tooenhance modelu zalecenia; zobacz [Tematy zaawansowane](#2-advanced-topics) sekcji.</span><span class="sxs-lookup"><span data-stu-id="a085e-546">Comma-separated list of feature name=feature value that can be used tooenhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span></span> |

| <span data-ttu-id="a085e-547">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-547">HTTP Method</span></span> | <span data-ttu-id="a085e-548">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-548">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-549">POST</span><span class="sxs-lookup"><span data-stu-id="a085e-549">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-550">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-550">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| <span data-ttu-id="a085e-551">NAGŁÓWEK</span><span class="sxs-lookup"><span data-stu-id="a085e-551">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="a085e-552">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-552">Parameter Name</span></span> | <span data-ttu-id="a085e-553">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-553">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-554">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-554">modelId</span></span> |<span data-ttu-id="a085e-555">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-555">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-556">Nazwa pliku</span><span class="sxs-lookup"><span data-stu-id="a085e-556">filename</span></span> |<span data-ttu-id="a085e-557">Identyfikator tekstową hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="a085e-557">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="a085e-558">Tylko litery (A-Z, a – z), cyfry (0 – 9), łączniki (-) i znak podkreślenia (_) są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="a085e-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="a085e-559">Długość maksymalna: 50</span><span class="sxs-lookup"><span data-stu-id="a085e-559">Max length: 50</span></span> |
| <span data-ttu-id="a085e-560">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-560">apiVersion</span></span> |<span data-ttu-id="a085e-561">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-561">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-562">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-562">Request Body</span></span> |<span data-ttu-id="a085e-563">Przykład: (funkcje):</span><span class="sxs-lookup"><span data-stu-id="a085e-563">Example (with features):</span></span><br/><span data-ttu-id="a085e-564">Tworzenie Clara Callan książki, opis książki hello, 2406e770-769c-4189-89de-1c9283f93a96, = Richard Wright publisher = Kanady Flamingo Harper, roku = 2001</span><span class="sxs-lookup"><span data-stu-id="a085e-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,hello book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span></span><br><span data-ttu-id="a085e-565">hello 21bf8088-b6c0-4509-870c-e1c7ac78304a, miejsca Forgetting: A fikcja (książka Byzantium), książki,, autora = Nick Bantock wydawcy = Harpercollins, rok = 1997</span><span class="sxs-lookup"><span data-stu-id="a085e-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span></span><br><span data-ttu-id="a085e-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23, Spadework, książki,, autora = Findley Tymotka publisher = Kanada HarperFlamingo roku = 2001</span><span class="sxs-lookup"><span data-stu-id="a085e-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span></span><br><span data-ttu-id="a085e-567">552a1940-21e4-4399-82bb-594b46d7ed54, ograniczenia bestii, książki, opis książki hello, tworzyć = młynów Magnus publisher = publikowania gier roku = 1998</span><span class="sxs-lookup"><span data-stu-id="a085e-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,hello book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span></span></pre> |

<span data-ttu-id="a085e-568">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-568">**Response**:</span></span>

<span data-ttu-id="a085e-569">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-569">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-570">Witaj interfejsu API zwraca raportu hello importu.</span><span class="sxs-lookup"><span data-stu-id="a085e-570">hello API returns a report of hello import.</span></span>

* <span data-ttu-id="a085e-571">`feed\entry\content\properties\LineCount`— Zaakceptowano liczba wierszy.</span><span class="sxs-lookup"><span data-stu-id="a085e-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="a085e-572">`feed\entry\content\properties\ErrorCount`-Liczba wierszy, które nie zostały wstawione ze względu na błąd tooan.</span><span class="sxs-lookup"><span data-stu-id="a085e-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="a085e-573">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-573">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a><span data-ttu-id="a085e-574">8.2.</span><span class="sxs-lookup"><span data-stu-id="a085e-574">8.2.</span></span>    <span data-ttu-id="a085e-575">Pobierz katalogu</span><span class="sxs-lookup"><span data-stu-id="a085e-575">Get Catalog</span></span>
<span data-ttu-id="a085e-576">Pobiera wszystkie elementy katalogu.</span><span class="sxs-lookup"><span data-stu-id="a085e-576">Retrieves all catalog items.</span></span>
<span data-ttu-id="a085e-577">katalogu Hello będzie można pobrać jedną stronę w czasie.</span><span class="sxs-lookup"><span data-stu-id="a085e-577">hello catalog will be retrieved one page at a time.</span></span> <span data-ttu-id="a085e-578">Jeśli chcesz elementów tooget od określonego indeksu można użyć parametru odata hello $skip.</span><span class="sxs-lookup"><span data-stu-id="a085e-578">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="a085e-579">Na przykład elementów tooget, zaczynając od pozycji 100, należy dodać parametr hello $skip = 100 toohello żądania.</span><span class="sxs-lookup"><span data-stu-id="a085e-579">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="a085e-580">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-580">HTTP Method</span></span> | <span data-ttu-id="a085e-581">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-581">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-582">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-582">GET</span></span> |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-583">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-583">Example:</span></span><br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-584">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-584">Parameter Name</span></span> | <span data-ttu-id="a085e-585">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-585">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-586">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-586">modelId</span></span> |<span data-ttu-id="a085e-587">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-587">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-588">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-588">apiVersion</span></span> |<span data-ttu-id="a085e-589">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-589">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-590">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-590">Request Body</span></span> |<span data-ttu-id="a085e-591">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-591">NONE</span></span> |

<span data-ttu-id="a085e-592">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-592">**Response**:</span></span>

<span data-ttu-id="a085e-593">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-593">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-594">odpowiedź Hello zawiera jeden wpis dla każdego elementu katalogu.</span><span class="sxs-lookup"><span data-stu-id="a085e-594">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="a085e-595">Każdy wpis ma hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="a085e-595">Each entry has hello following data:</span></span>

* <span data-ttu-id="a085e-596">`feed/entry/content/properties/ExternalId`— Identyfikator zewnętrznego elementu katalogu, hello dostarczonego przez powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="a085e-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, hello one provided by hello customer.</span></span>
* <span data-ttu-id="a085e-597">`feed/entry/content/properties/InternalId`-Katalogu wewnętrzny identyfikator elementu hello generowany Azure Machine Learning zalecenia.</span><span class="sxs-lookup"><span data-stu-id="a085e-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="a085e-598">`feed/entry/content/properties/Name`-Nazwa elementu katalogu.</span><span class="sxs-lookup"><span data-stu-id="a085e-598">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="a085e-599">`feed/entry/content/properties/Category`-Kategoria elementu katalogu.</span><span class="sxs-lookup"><span data-stu-id="a085e-599">`feed/entry/content/properties/Category` - Catalog item category.</span></span>
* <span data-ttu-id="a085e-600">`feed/entry/content/properties/Description`-Opis elementu katalogu.</span><span class="sxs-lookup"><span data-stu-id="a085e-600">`feed/entry/content/properties/Description` - Catalog item description.</span></span>
* <span data-ttu-id="a085e-601">`feed/entry/content/properties/Metadata`-Katalogu metadanych elementu.</span><span class="sxs-lookup"><span data-stu-id="a085e-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span></span>

<span data-ttu-id="a085e-602">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-602">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a><span data-ttu-id="a085e-603">8.3.</span><span class="sxs-lookup"><span data-stu-id="a085e-603">8.3.</span></span>    <span data-ttu-id="a085e-604">Pobrać elementów wykazu przez Token</span><span class="sxs-lookup"><span data-stu-id="a085e-604">Get Catalog Items by Token</span></span>
| <span data-ttu-id="a085e-605">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-605">HTTP Method</span></span> | <span data-ttu-id="a085e-606">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-606">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-607">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-607">GET</span></span> |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-608">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-608">Example:</span></span><br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-609">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-609">Parameter Name</span></span> | <span data-ttu-id="a085e-610">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-610">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-611">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-611">modelId</span></span> |<span data-ttu-id="a085e-612">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-612">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-613">Token</span><span class="sxs-lookup"><span data-stu-id="a085e-613">token</span></span> |<span data-ttu-id="a085e-614">Token nazwy element hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="a085e-614">Token of hello catalog item’s name.</span></span> <span data-ttu-id="a085e-615">Powinien zawierać co najmniej 3 znaki.</span><span class="sxs-lookup"><span data-stu-id="a085e-615">Should contain at least 3 characters.</span></span> |
| <span data-ttu-id="a085e-616">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-616">apiVersion</span></span> |<span data-ttu-id="a085e-617">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-617">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-618">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-618">Request Body</span></span> |<span data-ttu-id="a085e-619">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-619">NONE</span></span> |

<span data-ttu-id="a085e-620">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-620">**Response**:</span></span>

<span data-ttu-id="a085e-621">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-621">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-622">odpowiedź Hello zawiera jeden wpis dla każdego elementu katalogu.</span><span class="sxs-lookup"><span data-stu-id="a085e-622">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="a085e-623">Każdy wpis ma hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="a085e-623">Each entry has hello following data:</span></span>

* <span data-ttu-id="a085e-624">`feed/entry/content/properties/InternalId`-Katalogu wewnętrzny identyfikator elementu hello generowany Azure Machine Learning zalecenia.</span><span class="sxs-lookup"><span data-stu-id="a085e-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="a085e-625">`feed/entry/content/properties/Name`-Nazwa elementu katalogu.</span><span class="sxs-lookup"><span data-stu-id="a085e-625">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="a085e-626">`feed/entry/content/properties/Rating`-(do użytku w przyszłości)</span><span class="sxs-lookup"><span data-stu-id="a085e-626">`feed/entry/content/properties/Rating` -  (for future use)</span></span>
* <span data-ttu-id="a085e-627">`feed/entry/content/properties/Reasoning`-(do użytku w przyszłości)</span><span class="sxs-lookup"><span data-stu-id="a085e-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span></span>
* <span data-ttu-id="a085e-628">`feed/entry/content/properties/Metadata`-(do użytku w przyszłości)</span><span class="sxs-lookup"><span data-stu-id="a085e-628">`feed/entry/content/properties/Metadata` -  (for future use)</span></span>
* <span data-ttu-id="a085e-629">`feed/entry/content/properties/FormattedRating`-(do użytku w przyszłości)</span><span class="sxs-lookup"><span data-stu-id="a085e-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span></span>

<span data-ttu-id="a085e-630">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-630">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a><span data-ttu-id="a085e-631">9. Dane użycia</span><span class="sxs-lookup"><span data-stu-id="a085e-631">9. Usage data</span></span>
### <a name="91----import-usage-data"></a><span data-ttu-id="a085e-632">9.1.</span><span class="sxs-lookup"><span data-stu-id="a085e-632">9.1.</span></span>    <span data-ttu-id="a085e-633">Importowanie danych użycia</span><span class="sxs-lookup"><span data-stu-id="a085e-633">Import Usage Data</span></span>
#### <a name="911-uploading-file"></a><span data-ttu-id="a085e-634">9.1.1.</span><span class="sxs-lookup"><span data-stu-id="a085e-634">9.1.1.</span></span> <span data-ttu-id="a085e-635">Przekazywanie plików</span><span class="sxs-lookup"><span data-stu-id="a085e-635">Uploading File</span></span>
<span data-ttu-id="a085e-636">W tej sekcji przedstawiono sposób tooupload dane użycia przy użyciu pliku.</span><span class="sxs-lookup"><span data-stu-id="a085e-636">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="a085e-637">Można wywołać tego interfejsu API z danych użycia.</span><span class="sxs-lookup"><span data-stu-id="a085e-637">You can call this API several times with usage data.</span></span> <span data-ttu-id="a085e-638">Wszystkie dane użycia są zapisywane dla wszystkich wywołań.</span><span class="sxs-lookup"><span data-stu-id="a085e-638">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="a085e-639">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-639">HTTP Method</span></span> | <span data-ttu-id="a085e-640">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-640">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-641">POST</span><span class="sxs-lookup"><span data-stu-id="a085e-641">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-642">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-642">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-643">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-643">Parameter Name</span></span> | <span data-ttu-id="a085e-644">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-644">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-645">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-645">modelId</span></span> |<span data-ttu-id="a085e-646">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-646">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-647">Nazwa pliku</span><span class="sxs-lookup"><span data-stu-id="a085e-647">filename</span></span> |<span data-ttu-id="a085e-648">Identyfikator tekstową hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="a085e-648">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="a085e-649">Tylko litery (A-Z, a – z), cyfry (0 – 9), łączniki (-) i znak podkreślenia (_) są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="a085e-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="a085e-650">Długość maksymalna: 50</span><span class="sxs-lookup"><span data-stu-id="a085e-650">Max length: 50</span></span> |
| <span data-ttu-id="a085e-651">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-651">apiVersion</span></span> |<span data-ttu-id="a085e-652">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-652">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-653">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-653">Request Body</span></span> |<span data-ttu-id="a085e-654">Dane użycia.</span><span class="sxs-lookup"><span data-stu-id="a085e-654">Usage data.</span></span> <span data-ttu-id="a085e-655">Format:</span><span class="sxs-lookup"><span data-stu-id="a085e-655">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="a085e-656">Nazwa</span><span class="sxs-lookup"><span data-stu-id="a085e-656">Name</span></span></th><th><span data-ttu-id="a085e-657">Obowiązkowy</span><span class="sxs-lookup"><span data-stu-id="a085e-657">Mandatory</span></span></th><th><span data-ttu-id="a085e-658">Typ</span><span class="sxs-lookup"><span data-stu-id="a085e-658">Type</span></span></th><th><span data-ttu-id="a085e-659">Opis</span><span class="sxs-lookup"><span data-stu-id="a085e-659">Description</span></span></th></tr><tr><td><span data-ttu-id="a085e-660">Identyfikator użytkownika</span><span class="sxs-lookup"><span data-stu-id="a085e-660">User Id</span></span></td><td><span data-ttu-id="a085e-661">Tak</span><span class="sxs-lookup"><span data-stu-id="a085e-661">Yes</span></span></td><td><span data-ttu-id="a085e-662">[A-z], [a-z], [0-9] [_] &#40; Podkreślenie &#41; [-] &#40; Dash &#41;</span><span class="sxs-lookup"><span data-stu-id="a085e-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="a085e-663">Maksymalna długość: 255</span><span class="sxs-lookup"><span data-stu-id="a085e-663">Max length: 255</span></span> </td><td><span data-ttu-id="a085e-664">Unikatowy identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a085e-664">Unique identifier of a user.</span></span></td></tr><tr><td><span data-ttu-id="a085e-665">Identyfikator elementu</span><span class="sxs-lookup"><span data-stu-id="a085e-665">Item Id</span></span></td><td><span data-ttu-id="a085e-666">Tak</span><span class="sxs-lookup"><span data-stu-id="a085e-666">Yes</span></span></td><td><span data-ttu-id="a085e-667">[A-z], [a-z], [0-9] [&#95;] &#40; Podkreślenie &#41; [-] &#40; Dash &#41;</span><span class="sxs-lookup"><span data-stu-id="a085e-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="a085e-668">Długość maksymalna: 50</span><span class="sxs-lookup"><span data-stu-id="a085e-668">Max length: 50</span></span></td><td><span data-ttu-id="a085e-669">Unikatowy identyfikator elementu.</span><span class="sxs-lookup"><span data-stu-id="a085e-669">Unique identifier of an item.</span></span></td></tr><tr><td><span data-ttu-id="a085e-670">Time</span><span class="sxs-lookup"><span data-stu-id="a085e-670">Time</span></span></td><td><span data-ttu-id="a085e-671">Nie</span><span class="sxs-lookup"><span data-stu-id="a085e-671">No</span></span></td><td><span data-ttu-id="a085e-672">Data w formacie: RRRR/MM/ddtgg (np. 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="a085e-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="a085e-673">Czas danych.</span><span class="sxs-lookup"><span data-stu-id="a085e-673">Time of data.</span></span></td></tr><tr><td><span data-ttu-id="a085e-674">Wydarzenie</span><span class="sxs-lookup"><span data-stu-id="a085e-674">Event</span></span></td><td><span data-ttu-id="a085e-675">Brak; Jeśli podany również umieścić daty</span><span class="sxs-lookup"><span data-stu-id="a085e-675">No; if supplied then must also put date</span></span></td><td><span data-ttu-id="a085e-676">Jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="a085e-676">One of hello following:</span></span><br><span data-ttu-id="a085e-677">• Kliknij przycisk</span><span class="sxs-lookup"><span data-stu-id="a085e-677">• Click</span></span><br><span data-ttu-id="a085e-678">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="a085e-678">• RecommendationClick</span></span><br><span data-ttu-id="a085e-679">• AddShopCart</span><span class="sxs-lookup"><span data-stu-id="a085e-679">•    AddShopCart</span></span><br><span data-ttu-id="a085e-680">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="a085e-680">• RemoveShopCart</span></span><br><span data-ttu-id="a085e-681">• Zakupu</span><span class="sxs-lookup"><span data-stu-id="a085e-681">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="a085e-682">Maksymalny rozmiar pliku: 200MB</span><span class="sxs-lookup"><span data-stu-id="a085e-682">Maximum file size: 200MB</span></span><br><br><span data-ttu-id="a085e-683">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-683">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="a085e-684">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-684">**Response**:</span></span>

<span data-ttu-id="a085e-685">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-685">HTTP Status code: 200</span></span>

* <span data-ttu-id="a085e-686">`Feed\entry\content\properties\LineCount`— Zaakceptowano liczba wierszy.</span><span class="sxs-lookup"><span data-stu-id="a085e-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="a085e-687">`Feed\entry\content\properties\ErrorCount`-Liczba wierszy, które nie zostały wstawione ze względu na błąd tooan.</span><span class="sxs-lookup"><span data-stu-id="a085e-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="a085e-688">`Feed\entry\content\properties\FileId`— Identyfikator pliku.</span><span class="sxs-lookup"><span data-stu-id="a085e-688">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="a085e-689">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-689">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a><span data-ttu-id="a085e-690">9.1.2.</span><span class="sxs-lookup"><span data-stu-id="a085e-690">9.1.2.</span></span> <span data-ttu-id="a085e-691">Przy użyciu danych</span><span class="sxs-lookup"><span data-stu-id="a085e-691">Using Data Acquisition</span></span>
<span data-ttu-id="a085e-692">W tej sekcji przedstawiono, jak zdarzenia toosend w rzeczywistym czasu tooAzure Machine Learning zalecenia, zazwyczaj z witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a085e-692">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="a085e-693">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-693">HTTP Method</span></span> | <span data-ttu-id="a085e-694">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-694">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-695">POST</span><span class="sxs-lookup"><span data-stu-id="a085e-695">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| <span data-ttu-id="a085e-696">NAGŁÓWEK</span><span class="sxs-lookup"><span data-stu-id="a085e-696">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="a085e-697">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-697">Parameter Name</span></span> | <span data-ttu-id="a085e-698">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-698">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-699">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-699">apiVersion</span></span> |<span data-ttu-id="a085e-700">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-700">1.0</span></span> |
| <span data-ttu-id="a085e-701">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-701">Request body</span></span> |<span data-ttu-id="a085e-702">Wprowadzanie danych zdarzeń dla każdego zdarzenia mają toosend.</span><span class="sxs-lookup"><span data-stu-id="a085e-702">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="a085e-703">Należy wysłać dla hello tej samej sesji użytkownika lub przeglądarki hello tym samym identyfikatorze hello SessionId pola.</span><span class="sxs-lookup"><span data-stu-id="a085e-703">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="a085e-704">(Zobacz przykład treści zdarzenia poniżej).</span><span class="sxs-lookup"><span data-stu-id="a085e-704">(See sample of event body below.)</span></span> |

* <span data-ttu-id="a085e-705">Przykład dla zdarzenia "Kliknij przycisk":</span><span class="sxs-lookup"><span data-stu-id="a085e-705">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="a085e-706">Przykład dla zdarzenia "RecommendationClick":</span><span class="sxs-lookup"><span data-stu-id="a085e-706">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="a085e-707">Przykład dla zdarzenia "AddShopCart":</span><span class="sxs-lookup"><span data-stu-id="a085e-707">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="a085e-708">Przykład dla zdarzenia "RemoveShopCart":</span><span class="sxs-lookup"><span data-stu-id="a085e-708">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="a085e-709">Przykład dla zdarzenia "Zakupu":</span><span class="sxs-lookup"><span data-stu-id="a085e-709">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
            <EventData>
                <Name>Purchase</Name>
                <PurchaseItems>
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
                </PurchaseItems>
            </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="a085e-710">Przykład wysyłania 2 zdarzenia "kliknij" a "AddShopCart":</span><span class="sxs-lookup"><span data-stu-id="a085e-710">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="a085e-711">**Odpowiedź**: kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-711">**Response**: HTTP Status code: 200</span></span>

### <a name="92----list-model-usage-files"></a><span data-ttu-id="a085e-712">9.2.</span><span class="sxs-lookup"><span data-stu-id="a085e-712">9.2.</span></span>    <span data-ttu-id="a085e-713">Pliki użycia modelu listy</span><span class="sxs-lookup"><span data-stu-id="a085e-713">List Model Usage Files</span></span>
<span data-ttu-id="a085e-714">Pobiera metadane wszystkie pliki użycia modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-714">Retrieves metadata of all model usage files.</span></span>
<span data-ttu-id="a085e-715">Witaj użycia, które pliki są pobierane jedną stronę w czasie.</span><span class="sxs-lookup"><span data-stu-id="a085e-715">hello usage files will be retrieved one page at a time.</span></span> <span data-ttu-id="a085e-716">Elementy kasowa 100 każdej strony.</span><span class="sxs-lookup"><span data-stu-id="a085e-716">Each page containes 100 items.</span></span> <span data-ttu-id="a085e-717">Jeśli chcesz elementów tooget od określonego indeksu można użyć parametru odata hello $skip.</span><span class="sxs-lookup"><span data-stu-id="a085e-717">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="a085e-718">Na przykład elementów tooget, zaczynając od pozycji 100, należy dodać parametr hello $skip = 100 toohello żądania.</span><span class="sxs-lookup"><span data-stu-id="a085e-718">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="a085e-719">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-719">HTTP Method</span></span> | <span data-ttu-id="a085e-720">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-720">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-721">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-721">GET</span></span> |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-722">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-722">Example:</span></span><br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-723">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-723">Parameter Name</span></span> | <span data-ttu-id="a085e-724">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-724">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-725">forModelId</span><span class="sxs-lookup"><span data-stu-id="a085e-725">forModelId</span></span> |<span data-ttu-id="a085e-726">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-726">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-727">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-727">apiVersion</span></span> |<span data-ttu-id="a085e-728">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-728">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-729">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-729">Request Body</span></span> |<span data-ttu-id="a085e-730">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-730">NONE</span></span> |

<span data-ttu-id="a085e-731">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-731">**Response**:</span></span>

<span data-ttu-id="a085e-732">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-732">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-733">odpowiedź Hello zawiera jednego wpisu na użycie pliku.</span><span class="sxs-lookup"><span data-stu-id="a085e-733">hello response includes one entry per usage file.</span></span> <span data-ttu-id="a085e-734">Każdy wpis ma hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="a085e-734">Each entry has hello following data:</span></span>

* <span data-ttu-id="a085e-735">`feed\entry\content\properties\Id`-Identyfikator użycia pliku.</span><span class="sxs-lookup"><span data-stu-id="a085e-735">`feed\entry\content\properties\Id` - Usage file ID.</span></span>
* <span data-ttu-id="a085e-736">`feed\entry\content\properties\Length`— Długość pliku użycie w MB.</span><span class="sxs-lookup"><span data-stu-id="a085e-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span></span>
* <span data-ttu-id="a085e-737">`feed\entry\content\properties\DateModified`-Data utworzenia pliku użycia hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-737">`feed\entry\content\properties\DateModified` - Date when hello usage file was created.</span></span>
* <span data-ttu-id="a085e-738">`feed\entry\content\properties\UseInModel`— Czy plik użycia hello jest używany w hello modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-738">`feed\entry\content\properties\UseInModel` - Whether hello usage file is used in hello model.</span></span>

<span data-ttu-id="a085e-739">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-739">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a><span data-ttu-id="a085e-740">9.3.</span><span class="sxs-lookup"><span data-stu-id="a085e-740">9.3.</span></span>    <span data-ttu-id="a085e-741">Uzyskać statystyki użycia</span><span class="sxs-lookup"><span data-stu-id="a085e-741">Get Usage Statistics</span></span>
<span data-ttu-id="a085e-742">Pobiera statystyki użycia.</span><span class="sxs-lookup"><span data-stu-id="a085e-742">Gets usage statistics.</span></span>

| <span data-ttu-id="a085e-743">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-743">HTTP Method</span></span> | <span data-ttu-id="a085e-744">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-744">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-745">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-745">GET</span></span> |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-746">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-746">Example:</span></span><br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-747">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-747">Parameter Name</span></span> | <span data-ttu-id="a085e-748">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-748">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-749">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-749">modelId</span></span> |<span data-ttu-id="a085e-750">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-750">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-751">datą rozpoczęcia</span><span class="sxs-lookup"><span data-stu-id="a085e-751">startDate</span></span> |<span data-ttu-id="a085e-752">Data rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="a085e-752">Start date.</span></span> <span data-ttu-id="a085e-753">Format: RRRR/MM/Ddtgg</span><span class="sxs-lookup"><span data-stu-id="a085e-753">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="a085e-754">datą zakończenia</span><span class="sxs-lookup"><span data-stu-id="a085e-754">endDate</span></span> |<span data-ttu-id="a085e-755">Data zakończenia.</span><span class="sxs-lookup"><span data-stu-id="a085e-755">End date.</span></span> <span data-ttu-id="a085e-756">Format: RRRR/MM/Ddtgg</span><span class="sxs-lookup"><span data-stu-id="a085e-756">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="a085e-757">eventTypes</span><span class="sxs-lookup"><span data-stu-id="a085e-757">eventTypes</span></span> |<span data-ttu-id="a085e-758">Ciąg rozdzielony przecinkami zdarzenia typów lub wartość null tooget wszystkie zdarzenia</span><span class="sxs-lookup"><span data-stu-id="a085e-758">Comma-separated string of event types or null tooget all events</span></span> |
| <span data-ttu-id="a085e-759">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-759">apiVersion</span></span> |<span data-ttu-id="a085e-760">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-760">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-761">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-761">Request Body</span></span> |<span data-ttu-id="a085e-762">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-762">NONE</span></span> |

<span data-ttu-id="a085e-763">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-763">**Response**:</span></span>

<span data-ttu-id="a085e-764">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-764">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-765">Kolekcja elementów klucza i wartości.</span><span class="sxs-lookup"><span data-stu-id="a085e-765">A collection of key/value elements.</span></span> <span data-ttu-id="a085e-766">Każda z nich zawiera sumę hello zdarzeń dla określonego typu zdarzenia pogrupowane wg godziny.</span><span class="sxs-lookup"><span data-stu-id="a085e-766">Each one contains hello sum of events for a specific event type grouped by hour.</span></span>

* <span data-ttu-id="a085e-767">`feed\entry[i]\content\properties\Key`-Zawiera czas hello (pogrupowane według godzin) i hello typ zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="a085e-767">`feed\entry[i]\content\properties\Key` - Contains hello time (grouped by hour) and hello event type.</span></span>
* <span data-ttu-id="a085e-768">`feed\entry[i]\content\properties\Value`— Licznik Całkowita liczba zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="a085e-768">`feed\entry[i]\content\properties\Value` - Total event count.</span></span>

<span data-ttu-id="a085e-769">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-769">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a><span data-ttu-id="a085e-770">9.4.</span><span class="sxs-lookup"><span data-stu-id="a085e-770">9.4.</span></span>    <span data-ttu-id="a085e-771">Pobierz przykładowy plik użycia</span><span class="sxs-lookup"><span data-stu-id="a085e-771">Get Usage File Sample</span></span>
<span data-ttu-id="a085e-772">Pobiera hello 2KB pierwszego użycia pliku zawartości.</span><span class="sxs-lookup"><span data-stu-id="a085e-772">Retrieves hello first 2KB of usage file content.</span></span>

| <span data-ttu-id="a085e-773">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-773">HTTP Method</span></span> | <span data-ttu-id="a085e-774">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-774">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-775">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-775">GET</span></span> |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-776">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-776">Example:</span></span><br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-777">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-777">Parameter Name</span></span> | <span data-ttu-id="a085e-778">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-778">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-779">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-779">modelId</span></span> |<span data-ttu-id="a085e-780">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-780">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-781">fileId</span><span class="sxs-lookup"><span data-stu-id="a085e-781">fileId</span></span> |<span data-ttu-id="a085e-782">Unikatowy identyfikator hello modelu użycia pliku</span><span class="sxs-lookup"><span data-stu-id="a085e-782">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="a085e-783">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-783">apiVersion</span></span> |<span data-ttu-id="a085e-784">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-784">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-785">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-785">Request Body</span></span> |<span data-ttu-id="a085e-786">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-786">NONE</span></span> |

<span data-ttu-id="a085e-787">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-787">**Response**:</span></span>

<span data-ttu-id="a085e-788">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-788">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-789">Odpowiedź zostanie zwrócona w formacie tekstowym raw:</span><span class="sxs-lookup"><span data-stu-id="a085e-789">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a><span data-ttu-id="a085e-790">9.5.</span><span class="sxs-lookup"><span data-stu-id="a085e-790">9.5.</span></span>    <span data-ttu-id="a085e-791">Pobierz plik użycia modelu</span><span class="sxs-lookup"><span data-stu-id="a085e-791">Get Model Usage File</span></span>
<span data-ttu-id="a085e-792">Pobiera hello pełnej zawartości hello użycia pliku.</span><span class="sxs-lookup"><span data-stu-id="a085e-792">Retrieves hello full content of hello usage file.</span></span>

| <span data-ttu-id="a085e-793">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-793">HTTP Method</span></span> | <span data-ttu-id="a085e-794">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-794">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-795">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-795">GET</span></span> |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-796">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-796">Example:</span></span><br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-797">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-797">Parameter Name</span></span> | <span data-ttu-id="a085e-798">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-798">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-799">MID</span><span class="sxs-lookup"><span data-stu-id="a085e-799">mid</span></span> |<span data-ttu-id="a085e-800">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-800">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-801">FID</span><span class="sxs-lookup"><span data-stu-id="a085e-801">fid</span></span> |<span data-ttu-id="a085e-802">Unikatowy identyfikator hello modelu użycia pliku</span><span class="sxs-lookup"><span data-stu-id="a085e-802">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="a085e-803">Pobierz</span><span class="sxs-lookup"><span data-stu-id="a085e-803">download</span></span> |<span data-ttu-id="a085e-804">1</span><span class="sxs-lookup"><span data-stu-id="a085e-804">1</span></span> |
| <span data-ttu-id="a085e-805">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-805">apiVersion</span></span> |<span data-ttu-id="a085e-806">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-806">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-807">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-807">Request Body</span></span> |<span data-ttu-id="a085e-808">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-808">NONE</span></span> |

<span data-ttu-id="a085e-809">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-809">**Response**:</span></span>

<span data-ttu-id="a085e-810">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-810">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-811">Odpowiedź zostanie zwrócona w formacie tekstowym raw:</span><span class="sxs-lookup"><span data-stu-id="a085e-811">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a><span data-ttu-id="a085e-812">9.6.</span><span class="sxs-lookup"><span data-stu-id="a085e-812">9.6.</span></span>    <span data-ttu-id="a085e-813">Usuń plik użycia</span><span class="sxs-lookup"><span data-stu-id="a085e-813">Delete Usage File</span></span>
<span data-ttu-id="a085e-814">Usuwa plik użycia określonego modelu hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-814">Deletes hello specified model usage file.</span></span>

| <span data-ttu-id="a085e-815">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-815">HTTP Method</span></span> | <span data-ttu-id="a085e-816">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-816">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-817">USUŃ</span><span class="sxs-lookup"><span data-stu-id="a085e-817">DELETE</span></span> |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-818">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-818">Example:</span></span><br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-819">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-819">Parameter Name</span></span> | <span data-ttu-id="a085e-820">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-820">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-821">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-821">modelId</span></span> |<span data-ttu-id="a085e-822">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-822">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-823">fileId</span><span class="sxs-lookup"><span data-stu-id="a085e-823">fileId</span></span> |<span data-ttu-id="a085e-824">Unikatowy identyfikator hello toobe plik usunięty</span><span class="sxs-lookup"><span data-stu-id="a085e-824">Unique identifier of hello file toobe deleted</span></span> |
| <span data-ttu-id="a085e-825">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-825">apiVersion</span></span> |<span data-ttu-id="a085e-826">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-826">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-827">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-827">Request Body</span></span> |<span data-ttu-id="a085e-828">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-828">NONE</span></span> |

<span data-ttu-id="a085e-829">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-829">**Response**:</span></span>

<span data-ttu-id="a085e-830">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-830">HTTP Status code: 200</span></span>

### <a name="97----delete-all-usage-files"></a><span data-ttu-id="a085e-831">9.7.</span><span class="sxs-lookup"><span data-stu-id="a085e-831">9.7.</span></span>    <span data-ttu-id="a085e-832">Usuń wszystkie pliki użycia</span><span class="sxs-lookup"><span data-stu-id="a085e-832">Delete All Usage Files</span></span>
<span data-ttu-id="a085e-833">Usuwa wszystkie pliki użycia modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-833">Deletes all model usage files.</span></span>

| <span data-ttu-id="a085e-834">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-834">HTTP Method</span></span> | <span data-ttu-id="a085e-835">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-835">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-836">USUŃ</span><span class="sxs-lookup"><span data-stu-id="a085e-836">DELETE</span></span> |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-837">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-837">Example:</span></span><br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-838">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-838">Parameter Name</span></span> | <span data-ttu-id="a085e-839">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-839">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-840">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-840">modelId</span></span> |<span data-ttu-id="a085e-841">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-841">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-842">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-842">apiVersion</span></span> |<span data-ttu-id="a085e-843">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-843">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-844">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-844">Request Body</span></span> |<span data-ttu-id="a085e-845">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-845">NONE</span></span> |

<span data-ttu-id="a085e-846">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-846">**Response**:</span></span>

<span data-ttu-id="a085e-847">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-847">HTTP Status code: 200</span></span>

## <a name="10-features"></a><span data-ttu-id="a085e-848">10. Funkcje</span><span class="sxs-lookup"><span data-stu-id="a085e-848">10. Features</span></span>
<span data-ttu-id="a085e-849">W tej sekcji przedstawiono sposób tooretrieve funkcji informacji, takich jak funkcje hello zaimportowane i ich wartości, ich stopień i gdy ta pozycja został przydzielony.</span><span class="sxs-lookup"><span data-stu-id="a085e-849">This section shows how tooretrieve feature information, such as hello imported features and their values, their rank, and when this rank was allocated.</span></span> <span data-ttu-id="a085e-850">Funkcje są importowane jako część hello wykazu danych, a następnie ich pozycja jest skojarzony, po zakończeniu kompilacji rangi.</span><span class="sxs-lookup"><span data-stu-id="a085e-850">Features are imported as part of hello catalog data, and then their rank is associated when a rank build is done.</span></span>
<span data-ttu-id="a085e-851">Funkcja rangę można zmienić zgodnie z toohello wzorca użycia danych i typ elementów.</span><span class="sxs-lookup"><span data-stu-id="a085e-851">Feature rank can change according toohello pattern of usage data and type of items.</span></span> <span data-ttu-id="a085e-852">Ale rangę hello powinny mieć tylko małe wahania spójne użycia/elementów.</span><span class="sxs-lookup"><span data-stu-id="a085e-852">But for consistent usage/items, hello rank should have only small fluctuations.</span></span>
<span data-ttu-id="a085e-853">Ranga Hello funkcji jest liczbą nieujemną.</span><span class="sxs-lookup"><span data-stu-id="a085e-853">hello rank of features is a non-negative number.</span></span> <span data-ttu-id="a085e-854">Witaj numer 0 oznacza, że nie zajęła tej funkcji hello (się stanie w przypadku wywołać tego interfejsu API zakończenia wcześniejszych toohello pierwszej kompilacji rank powitania).</span><span class="sxs-lookup"><span data-stu-id="a085e-854">hello  number 0 means that hello feature was not ranked (happens if you invoke this API prior toohello completion of hello first rank build).</span></span> <span data-ttu-id="a085e-855">Data Hello jaką została przypisana rangę hello jest nazywany hello wynik świeżości.</span><span class="sxs-lookup"><span data-stu-id="a085e-855">hello date at which hello rank was attributed is called hello score freshness.</span></span>

### <a name="101-get-features-info-for-last-rank-build"></a><span data-ttu-id="a085e-856">10.1.</span><span class="sxs-lookup"><span data-stu-id="a085e-856">10.1.</span></span> <span data-ttu-id="a085e-857">Uzyskać informacje o funkcji (Ostatnia kompilacja rangi)</span><span class="sxs-lookup"><span data-stu-id="a085e-857">Get Features Info (For Last Rank Build)</span></span>
<span data-ttu-id="a085e-858">Pobiera informacje funkcji hello, w tym klasyfikacji dla hello ostatniej kompilacji rangi powiodło się.</span><span class="sxs-lookup"><span data-stu-id="a085e-858">Retrieves hello feature information, including ranking, for hello last successful rank build.</span></span>

| <span data-ttu-id="a085e-859">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-859">HTTP Method</span></span> | <span data-ttu-id="a085e-860">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-860">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-861">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-861">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-862">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-862">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-863">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-863">Parameter Name</span></span> | <span data-ttu-id="a085e-864">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-864">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-865">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-865">modelId</span></span> |<span data-ttu-id="a085e-866">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-866">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-867">samplingSize</span><span class="sxs-lookup"><span data-stu-id="a085e-867">samplingSize</span></span> |<span data-ttu-id="a085e-868">Liczba wartości tooinclude dla każdej funkcji, zgodnie z toohello danych w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-868">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span> <br/><span data-ttu-id="a085e-869">Możliwe wartości:</span><span class="sxs-lookup"><span data-stu-id="a085e-869">Possible values are:</span></span><br> <span data-ttu-id="a085e-870">-1 - wszystkie próbki.</span><span class="sxs-lookup"><span data-stu-id="a085e-870">-1 - All samples.</span></span> <br><span data-ttu-id="a085e-871">0 — próbkowanie nie.</span><span class="sxs-lookup"><span data-stu-id="a085e-871">0 - No sampling.</span></span> <br><span data-ttu-id="a085e-872">N - Zwróć N przykłady dla każdej nazwy funkcji.</span><span class="sxs-lookup"><span data-stu-id="a085e-872">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="a085e-873">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-873">apiVersion</span></span> |<span data-ttu-id="a085e-874">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-874">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-875">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-875">Request Body</span></span> |<span data-ttu-id="a085e-876">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-876">NONE</span></span> |

<span data-ttu-id="a085e-877">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-877">**Response**:</span></span>

<span data-ttu-id="a085e-878">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-878">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-879">odpowiedź Hello zawiera listę wpisów informacji o funkcji.</span><span class="sxs-lookup"><span data-stu-id="a085e-879">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="a085e-880">Każdy wpis zawiera:</span><span class="sxs-lookup"><span data-stu-id="a085e-880">Each entry contains:</span></span>

* <span data-ttu-id="a085e-881">`feed/entry/content/m:properties/d:Name`-Funkcja nazwa.</span><span class="sxs-lookup"><span data-stu-id="a085e-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="a085e-882">`feed/entry/content/m:properties/d:RankUpdateDate`-Data na które hello rangę funkcji przydzielone toothis alias</span><span class="sxs-lookup"><span data-stu-id="a085e-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="a085e-883">wynik świeżości funkcji.</span><span class="sxs-lookup"><span data-stu-id="a085e-883">score freshness feature.</span></span> <span data-ttu-id="a085e-884">Historical Data ("0001-01-01T00:00:00") oznacza, że wykonano nie rangi kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="a085e-885">`feed/entry/content/m:properties/d:Rank`— Ranga funkcja (float).</span><span class="sxs-lookup"><span data-stu-id="a085e-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="a085e-886">Ranga 2.0 lub nowszej jest uznawane za funkcję dobra.</span><span class="sxs-lookup"><span data-stu-id="a085e-886">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="a085e-887">`feed/entry/content/m:properties/d:SampleValues`-Rozdzielana przecinkami lista wartości żądany rozmiar toohello próbkowania.</span><span class="sxs-lookup"><span data-stu-id="a085e-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="a085e-888">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-888">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a><span data-ttu-id="a085e-889">10.2.</span><span class="sxs-lookup"><span data-stu-id="a085e-889">10.2.</span></span> <span data-ttu-id="a085e-890">Pobierz informacje funkcji (dla określonej kompilacji rangi)</span><span class="sxs-lookup"><span data-stu-id="a085e-890">Get Features Info (For Specific Rank Build)</span></span>
<span data-ttu-id="a085e-891">Pobiera informacje o funkcji hello, w tym klasyfikacji w ramach określonej kompilacji rank powitania.</span><span class="sxs-lookup"><span data-stu-id="a085e-891">Retrieves hello feature information, including hello ranking for a specific rank build.</span></span>

| <span data-ttu-id="a085e-892">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-892">HTTP Method</span></span> | <span data-ttu-id="a085e-893">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-893">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-894">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-894">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-895">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-895">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-896">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-896">Parameter Name</span></span> | <span data-ttu-id="a085e-897">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-897">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-898">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-898">modelId</span></span> |<span data-ttu-id="a085e-899">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-899">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-900">samplingSize</span><span class="sxs-lookup"><span data-stu-id="a085e-900">samplingSize</span></span> |<span data-ttu-id="a085e-901">Liczba wartości tooinclude dla każdej funkcji, zgodnie z toohello danych w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-901">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span><br/> <span data-ttu-id="a085e-902">Możliwe wartości:</span><span class="sxs-lookup"><span data-stu-id="a085e-902">Possible values are:</span></span><br> <span data-ttu-id="a085e-903">-1 - wszystkie próbki.</span><span class="sxs-lookup"><span data-stu-id="a085e-903">-1 - All samples.</span></span> <br><span data-ttu-id="a085e-904">0 — próbkowanie nie.</span><span class="sxs-lookup"><span data-stu-id="a085e-904">0 - No sampling.</span></span> <br><span data-ttu-id="a085e-905">N - Zwróć N przykłady dla każdej nazwy funkcji.</span><span class="sxs-lookup"><span data-stu-id="a085e-905">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="a085e-906">rankBuildId</span><span class="sxs-lookup"><span data-stu-id="a085e-906">rankBuildId</span></span> |<span data-ttu-id="a085e-907">Unikatowy identyfikator kompilacji rank powitania lub -1 dla ostatniej kompilacji rank powitania</span><span class="sxs-lookup"><span data-stu-id="a085e-907">Unique identifier of hello rank build or -1 for hello last rank build</span></span> |
| <span data-ttu-id="a085e-908">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-908">apiVersion</span></span> |<span data-ttu-id="a085e-909">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-909">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-910">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-910">Request Body</span></span> |<span data-ttu-id="a085e-911">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-911">NONE</span></span> |

<span data-ttu-id="a085e-912">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-912">**Response**:</span></span>

<span data-ttu-id="a085e-913">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-913">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-914">odpowiedź Hello zawiera listę wpisów informacji o funkcji.</span><span class="sxs-lookup"><span data-stu-id="a085e-914">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="a085e-915">Każdy wpis zawiera:</span><span class="sxs-lookup"><span data-stu-id="a085e-915">Each entry contains:</span></span>

* <span data-ttu-id="a085e-916">`feed/entry/content/m:properties/d:Name`-Funkcja nazwa.</span><span class="sxs-lookup"><span data-stu-id="a085e-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="a085e-917">`feed/entry/content/m:properties/d:RankUpdateDate`-Data na które hello rangę funkcji przydzielone toothis alias</span><span class="sxs-lookup"><span data-stu-id="a085e-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="a085e-918">wynik świeżości funkcji.</span><span class="sxs-lookup"><span data-stu-id="a085e-918">score freshness feature.</span></span> <span data-ttu-id="a085e-919">Historical Data ("0001-01-01T00:00:00") oznacza, że wykonano nie rangi kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="a085e-920">`feed/entry/content/m:properties/d:Rank`— Ranga funkcja (float).</span><span class="sxs-lookup"><span data-stu-id="a085e-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="a085e-921">Ranga 2.0 lub nowszej jest uznawane za funkcję dobra.</span><span class="sxs-lookup"><span data-stu-id="a085e-921">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="a085e-922">`feed/entry/content/m:properties/d:SampleValues`-Rozdzielana przecinkami lista wartości żądany rozmiar toohello próbkowania.</span><span class="sxs-lookup"><span data-stu-id="a085e-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="a085e-923">OData</span><span class="sxs-lookup"><span data-stu-id="a085e-923">OData</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a><span data-ttu-id="a085e-924">11. Kompilacja</span><span class="sxs-lookup"><span data-stu-id="a085e-924">11. Build</span></span>
  <span data-ttu-id="a085e-925">W tej sekcji opisano hello toobuilds związane z różnych interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="a085e-925">This section explains hello different APIs related toobuilds.</span></span> <span data-ttu-id="a085e-926">Istnieją 3 typy kompilacji: kompilację zalecenie, rangi kompilacji i kompilacji zmianie wysokości progów (często zakupione razem).</span><span class="sxs-lookup"><span data-stu-id="a085e-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span></span>

<span data-ttu-id="a085e-927">Celem Hello zalecenie kompilacji jest toogenerate model zalecenie używany do przewidywania.</span><span class="sxs-lookup"><span data-stu-id="a085e-927">hello recommendation build's purpose is toogenerate a recommendation model used for predictions.</span></span> <span data-ttu-id="a085e-928">Prognoz (dla tego typu kompilacji) są dostępne w dwóch odmian:</span><span class="sxs-lookup"><span data-stu-id="a085e-928">Predictions (for this type of build) come in two flavors:</span></span>

* <span data-ttu-id="a085e-929">I2I - alias</span><span class="sxs-lookup"><span data-stu-id="a085e-929">I2I - a.k.a.</span></span> <span data-ttu-id="a085e-930">Element zalecenia tooItem - danego elementu lub listy elementów tej opcji spowoduje prognozowania listę elementów, które są prawdopodobnie toobe wysoki odsetek.</span><span class="sxs-lookup"><span data-stu-id="a085e-930">Item tooItem recommendations - given an item or a list of items this option will predict a list of items that are likely toobe of high interest.</span></span>
* <span data-ttu-id="a085e-931">U2I - alias</span><span class="sxs-lookup"><span data-stu-id="a085e-931">U2I - a.k.a.</span></span> <span data-ttu-id="a085e-932">Zalecenia dotyczące tooItem użytkownika - podany identyfikator użytkownika (i opcjonalnie listę elementów) ta opcja będzie prognozowania listę elementów, które są prawdopodobnie toobe z niepodłączonych do hello danego użytkownika (i jego dodatkowe wybrane elementy).</span><span class="sxs-lookup"><span data-stu-id="a085e-932">User tooItem recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely toobe of high interest for hello given user (and its additional choice of items).</span></span> <span data-ttu-id="a085e-933">zalecenia dotyczące U2I Hello są oparte na powitania historii elementów, które były istotnych dla użytkownika hello czasu toohello, konstruowania modelu hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-933">hello U2I recommendations are based on hello history of items that were of interest for hello user up toohello time hello model was built.</span></span>

<span data-ttu-id="a085e-934">Rank kompilacji jest techniczne kompilacji, która pozwala toolearn o użyteczności hello funkcje.</span><span class="sxs-lookup"><span data-stu-id="a085e-934">A rank build is a technical build that allows you toolearn about hello usefulness of your features.</span></span> <span data-ttu-id="a085e-935">Zazwyczaj w kolejności tooget hello najlepszych wyników dla modelu zalecenia dotyczące funkcji, należy podjąć hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a085e-935">Usually, in order tooget hello best result for a recommendation model involving features, you should take hello following steps:</span></span>

* <span data-ttu-id="a085e-936">Wyzwalanie rangi kompilacji (o ile wynik hello funkcje jest stabilna), a następnie zaczekaj do wyniku funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-936">Trigger a rank build (unless hello score of your features is stable) and wait till you get hello feature score.</span></span>
* <span data-ttu-id="a085e-937">Pobrać rangę hello funkcje przez wywołanie hello [Get Info funkcji](#101-get-features-info-for-last-rank-build) interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a085e-937">Retrieve hello rank of your features by calling hello [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span></span>
* <span data-ttu-id="a085e-938">Konfigurowanie kompilowania zalecenia za pomocą hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="a085e-938">Configure a recommendation build with hello following parameters:</span></span>
  * <span data-ttu-id="a085e-939">`useFeatureInModel`-Set tooTrue.</span><span class="sxs-lookup"><span data-stu-id="a085e-939">`useFeatureInModel` - Set tooTrue.</span></span>
  * <span data-ttu-id="a085e-940">`ModelingFeatureList`-Set tooa rozdzielana przecinkami lista funkcji z wynikiem 2.0 lub więcej (według rangi toohello, pobierane w poprzednim kroku hello).</span><span class="sxs-lookup"><span data-stu-id="a085e-940">`ModelingFeatureList` - Set tooa comma-separated list of features with a score of 2.0 or more (according toohello ranks you retrieved in hello previous step).</span></span>
  * <span data-ttu-id="a085e-941">`AllowColdItemPlacement`-Set tooTrue.</span><span class="sxs-lookup"><span data-stu-id="a085e-941">`AllowColdItemPlacement` - Set tooTrue.</span></span>
  * <span data-ttu-id="a085e-942">Opcjonalnie można ustawić `EnableFeatureCorrelation` tooTrue i `ReasoningFeatureList` toohello lista funkcji, które chcesz toouse wyjaśnień (zazwyczaj hello tę samą listę funkcje używane w modelowania lub podlisty).</span><span class="sxs-lookup"><span data-stu-id="a085e-942">Optionally you can set `EnableFeatureCorrelation` tooTrue and `ReasoningFeatureList` toohello list of features you want toouse for explanations (usually hello same list of features used in modelling or a sublist).</span></span>
* <span data-ttu-id="a085e-943">Wyzwalacz hello zalecenie kompilacji z hello skonfigurowane parametry.</span><span class="sxs-lookup"><span data-stu-id="a085e-943">Trigger hello recommendation build with hello configured parameters.</span></span>

<span data-ttu-id="a085e-944">Uwaga: Jeśli nie skonfigurujesz żadnych parametrów (np. wywołać budowania zalecenie hello bez parametrów) lub nie zostanie jawnie wyłączone hello użycia funkcji (np. `UseFeatureInModel` ustawić tooFalse), hello system skonfiguruje hello parametry dotyczące funkcji toohello wyjaśniono powyższych wartości w przypadku, gdy istnieje rangi kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-944">Note: If you do not configure any parameters (e.g. invoke hello recommendation build without parameters) or you do not explicitly disable hello usage of features (e.g. `UseFeatureInModel` set tooFalse), hello system will set up hello feature-related parameters toohello explained values above in case a rank build exists.</span></span>

<span data-ttu-id="a085e-945">Nie podlega ograniczeniom na uruchomioną kompilację rangi i zalecenia kompilacji jednocześnie dla hello sam model.</span><span class="sxs-lookup"><span data-stu-id="a085e-945">There is no restriction on running a rank build and a recommendation build concurrently for hello same model.</span></span> <span data-ttu-id="a085e-946">Niemniej jednak nie można uruchomić dwie kompilacje hello tego samego typu na powitania sam model równolegle.</span><span class="sxs-lookup"><span data-stu-id="a085e-946">Nevertheless, you cannot run two builds of hello same type on hello same model in parallel.</span></span>

<span data-ttu-id="a085e-947">Kompilacja zmianie wysokości progów (często zakupione razem) jest jeszcze inny algorytm zalecenia nazywane czasami "zachowawcze" polecania, co ułatwia katalogi, które nie są jednorodne charakteru (jednorodnych: książek, filmów, niektóre żywności sposób; niejednorodnego: komputerów i urządzeń, między domenami, wysoce zróżnicowany).</span><span class="sxs-lookup"><span data-stu-id="a085e-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span></span>

<span data-ttu-id="a085e-948">Uwaga: Jeśli hello plików do użycia, które zostało przez Ciebie przekazane zawiera pole opcjonalne hello "typ zdarzenia" następnie dla zmianie wysokości progów modelowania tylko zdarzenia "Zakupu" będzie można używać.</span><span class="sxs-lookup"><span data-stu-id="a085e-948">Note: if hello usage files that you uploaded contain hello optional field "event type" then for FBT modelling only "Purchase" events will be used.</span></span> <span data-ttu-id="a085e-949">Jeśli żaden typ zdarzenia jest pod warunkiem, że wszystkie zdarzenia są traktowane jako zakupu.</span><span class="sxs-lookup"><span data-stu-id="a085e-949">If no event type is provided all events will be considered as purchase.</span></span>

#### <a name="111-build-parameters"></a><span data-ttu-id="a085e-950">11.1 kompilacji parametrów</span><span class="sxs-lookup"><span data-stu-id="a085e-950">11.1 Build parameters</span></span>
<span data-ttu-id="a085e-951">Każdy typ kompilacji mogą być konfigurowane przez zestaw parametrów (przedstawione poniżej).</span><span class="sxs-lookup"><span data-stu-id="a085e-951">Each build type can be configured via a set of parameters (depicted below).</span></span> <span data-ttu-id="a085e-952">Jeśli nie skonfigurujesz parametry hello hello systemu zostanie automatycznie atrybutu wartości parametrów toohello zgodnie z toohello informacje obecnych w chwili hello wyzwolić kompilację.</span><span class="sxs-lookup"><span data-stu-id="a085e-952">If you don't configure hello parameters, hello system will automatically attribute values toohello parameters according toohello information present at hello time you trigger a build.</span></span>

##### <a name="1111-usage-condenser"></a><span data-ttu-id="a085e-953">11.1.1.</span><span class="sxs-lookup"><span data-stu-id="a085e-953">11.1.1.</span></span> <span data-ttu-id="a085e-954">Zwrotną użycia</span><span class="sxs-lookup"><span data-stu-id="a085e-954">Usage condenser</span></span>
<span data-ttu-id="a085e-955">Użytkowników lub elementy o kilka punktów użycia może zawierać więcej szumu niż informacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-955">Users or items with few usage points might contain more noise than information.</span></span> <span data-ttu-id="a085e-956">Witaj system spróbuje toopredict hello minimalna liczba punktów użycia na użytkownika/elementu toobe używane w modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-956">hello system attempts toopredict hello minimal number of usage points per user/item toobe used in a model.</span></span> <span data-ttu-id="a085e-957">Ta liczba będzie zakresu hello zdefiniowany przez hello ItemCutoffLowerBound i parametrów ItemCutoffUpperBound elementów i hello zakresu zdefiniowanego przez hello UserCutOffLowerBound i UserCutoffUpperBound parametry dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a085e-957">This number will be within hello range defined by hello ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and hello range defined by hello UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span></span> <span data-ttu-id="a085e-958">Hello zwrotną wpływu na elementy lub użytkowników, można zminimalizować przez ustawienie co najmniej jeden z odpowiedniego toozero granice hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-958">hello condenser effect on items or users can be minimized by setting at least one of hello corresponding bounds toozero.</span></span>

##### <a name="1112-rank-build-parameters"></a><span data-ttu-id="a085e-959">11.1.2.</span><span class="sxs-lookup"><span data-stu-id="a085e-959">11.1.2.</span></span> <span data-ttu-id="a085e-960">Ranga kompilacji parametrów</span><span class="sxs-lookup"><span data-stu-id="a085e-960">Rank build parameters</span></span>
<span data-ttu-id="a085e-961">Witaj w poniższej tabeli przedstawiono hello parametry kompilacji dla kompilacji rangi.</span><span class="sxs-lookup"><span data-stu-id="a085e-961">hello table below depicts hello build parameters for a rank build.</span></span>

| <span data-ttu-id="a085e-962">Klucz</span><span class="sxs-lookup"><span data-stu-id="a085e-962">Key</span></span> | <span data-ttu-id="a085e-963">Opis</span><span class="sxs-lookup"><span data-stu-id="a085e-963">Description</span></span> | <span data-ttu-id="a085e-964">Typ</span><span class="sxs-lookup"><span data-stu-id="a085e-964">Type</span></span> | <span data-ttu-id="a085e-965">Nieprawidłowa wartość</span><span class="sxs-lookup"><span data-stu-id="a085e-965">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a085e-966">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="a085e-966">NumberOfModelIterations</span></span> |<span data-ttu-id="a085e-967">Hello liczby iteracji modelu hello wykonuje, sprawdzając hello obliczeniowe całkowity czas i hello dokładności modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-967">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="a085e-968">większa liczba hello Hello, hello większej dokładności, zostanie wyświetlony, ale hello obliczeń czas będzie trwać dłużej.</span><span class="sxs-lookup"><span data-stu-id="a085e-968">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="a085e-969">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-969">Integer</span></span> |<span data-ttu-id="a085e-970">10-50</span><span class="sxs-lookup"><span data-stu-id="a085e-970">10-50</span></span> |
| <span data-ttu-id="a085e-971">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="a085e-971">NumberOfModelDimensions</span></span> |<span data-ttu-id="a085e-972">Hello liczby wymiarów wiąże się, że liczba toohello "funkcji" hello modelu spróbuje toofind w danych.</span><span class="sxs-lookup"><span data-stu-id="a085e-972">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="a085e-973">Zwiększenie liczby hello wymiarów pozwoli lepiej dostrajanie hello wyniki w mniejszych klastrów.</span><span class="sxs-lookup"><span data-stu-id="a085e-973">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="a085e-974">Jednak zbyt dużo wymiarów uniemożliwi modelu hello odnalezienie korelacji między elementami.</span><span class="sxs-lookup"><span data-stu-id="a085e-974">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="a085e-975">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-975">Integer</span></span> |<span data-ttu-id="a085e-976">10-40</span><span class="sxs-lookup"><span data-stu-id="a085e-976">10-40</span></span> |
| <span data-ttu-id="a085e-977">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a085e-977">ItemCutOffLowerBound</span></span> |<span data-ttu-id="a085e-978">Definiuje element hello dolna granica zwrotną hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-978">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="a085e-979">Zobacz użycie zwrotną powyżej.</span><span class="sxs-lookup"><span data-stu-id="a085e-979">See usage condenser above.</span></span> |<span data-ttu-id="a085e-980">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-980">Integer</span></span> |<span data-ttu-id="a085e-981">co najmniej 2 (zwrotną Wyłącz 0)</span><span class="sxs-lookup"><span data-stu-id="a085e-981">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a085e-982">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a085e-982">ItemCutOffUpperBound</span></span> |<span data-ttu-id="a085e-983">Definiuje element hello górna granica zwrotną hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-983">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="a085e-984">Zobacz użycie zwrotną powyżej.</span><span class="sxs-lookup"><span data-stu-id="a085e-984">See usage condenser above.</span></span> |<span data-ttu-id="a085e-985">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-985">Integer</span></span> |<span data-ttu-id="a085e-986">co najmniej 2 (zwrotną Wyłącz 0)</span><span class="sxs-lookup"><span data-stu-id="a085e-986">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a085e-987">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a085e-987">UserCutOffLowerBound</span></span> |<span data-ttu-id="a085e-988">Definiuje hello użytkownika dolna granica zwrotną hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-988">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="a085e-989">Zobacz użycie zwrotną powyżej.</span><span class="sxs-lookup"><span data-stu-id="a085e-989">See usage condenser above.</span></span> |<span data-ttu-id="a085e-990">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-990">Integer</span></span> |<span data-ttu-id="a085e-991">co najmniej 2 (zwrotną Wyłącz 0)</span><span class="sxs-lookup"><span data-stu-id="a085e-991">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a085e-992">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a085e-992">UserCutOffUpperBound</span></span> |<span data-ttu-id="a085e-993">Definiuje hello użytkownika górna granica zwrotną hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-993">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="a085e-994">Zobacz użycie zwrotną powyżej.</span><span class="sxs-lookup"><span data-stu-id="a085e-994">See usage condenser above.</span></span> |<span data-ttu-id="a085e-995">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-995">Integer</span></span> |<span data-ttu-id="a085e-996">co najmniej 2 (zwrotną Wyłącz 0)</span><span class="sxs-lookup"><span data-stu-id="a085e-996">2 or more (0 disable condenser)</span></span> |

##### <a name="1113-recommendation-build-parameters"></a><span data-ttu-id="a085e-997">11.1.3.</span><span class="sxs-lookup"><span data-stu-id="a085e-997">11.1.3.</span></span> <span data-ttu-id="a085e-998">Parametry kompilacji zalecenia</span><span class="sxs-lookup"><span data-stu-id="a085e-998">Recommendation build parameters</span></span>
<span data-ttu-id="a085e-999">Witaj w poniższej tabeli przedstawiono hello parametry kompilacji dla kompilacji zalecenie.</span><span class="sxs-lookup"><span data-stu-id="a085e-999">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="a085e-1000">Klucz</span><span class="sxs-lookup"><span data-stu-id="a085e-1000">Key</span></span> | <span data-ttu-id="a085e-1001">Opis</span><span class="sxs-lookup"><span data-stu-id="a085e-1001">Description</span></span> | <span data-ttu-id="a085e-1002">Typ</span><span class="sxs-lookup"><span data-stu-id="a085e-1002">Type</span></span> | <span data-ttu-id="a085e-1003">Nieprawidłowa wartość</span><span class="sxs-lookup"><span data-stu-id="a085e-1003">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a085e-1004">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="a085e-1004">NumberOfModelIterations</span></span> |<span data-ttu-id="a085e-1005">Hello liczby iteracji modelu hello wykonuje, sprawdzając hello obliczeniowe całkowity czas i hello dokładności modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1005">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="a085e-1006">większa liczba hello Hello, hello większej dokładności, zostanie wyświetlony, ale hello obliczeń czas będzie trwać dłużej.</span><span class="sxs-lookup"><span data-stu-id="a085e-1006">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="a085e-1007">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-1007">Integer</span></span> |<span data-ttu-id="a085e-1008">10-50</span><span class="sxs-lookup"><span data-stu-id="a085e-1008">10-50</span></span> |
| <span data-ttu-id="a085e-1009">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="a085e-1009">NumberOfModelDimensions</span></span> |<span data-ttu-id="a085e-1010">Hello liczby wymiarów wiąże się, że liczba toohello "funkcji" hello modelu spróbuje toofind w danych.</span><span class="sxs-lookup"><span data-stu-id="a085e-1010">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="a085e-1011">Zwiększenie liczby hello wymiarów pozwoli lepiej dostrajanie hello wyniki w mniejszych klastrów.</span><span class="sxs-lookup"><span data-stu-id="a085e-1011">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="a085e-1012">Jednak zbyt dużo wymiarów uniemożliwi modelu hello odnalezienie korelacji między elementami.</span><span class="sxs-lookup"><span data-stu-id="a085e-1012">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="a085e-1013">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-1013">Integer</span></span> |<span data-ttu-id="a085e-1014">10-40</span><span class="sxs-lookup"><span data-stu-id="a085e-1014">10-40</span></span> |
| <span data-ttu-id="a085e-1015">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a085e-1015">ItemCutOffLowerBound</span></span> |<span data-ttu-id="a085e-1016">Definiuje element hello dolna granica zwrotną hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1016">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="a085e-1017">Zobacz użycie zwrotną powyżej.</span><span class="sxs-lookup"><span data-stu-id="a085e-1017">See usage condenser above.</span></span> |<span data-ttu-id="a085e-1018">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-1018">Integer</span></span> |<span data-ttu-id="a085e-1019">co najmniej 2 (zwrotną Wyłącz 0)</span><span class="sxs-lookup"><span data-stu-id="a085e-1019">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a085e-1020">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a085e-1020">ItemCutOffUpperBound</span></span> |<span data-ttu-id="a085e-1021">Definiuje element hello górna granica zwrotną hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1021">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="a085e-1022">Zobacz użycie zwrotną powyżej.</span><span class="sxs-lookup"><span data-stu-id="a085e-1022">See usage condenser above.</span></span> |<span data-ttu-id="a085e-1023">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-1023">Integer</span></span> |<span data-ttu-id="a085e-1024">co najmniej 2 (zwrotną Wyłącz 0)</span><span class="sxs-lookup"><span data-stu-id="a085e-1024">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a085e-1025">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a085e-1025">UserCutOffLowerBound</span></span> |<span data-ttu-id="a085e-1026">Definiuje hello użytkownika dolna granica zwrotną hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1026">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="a085e-1027">Zobacz użycie zwrotną powyżej.</span><span class="sxs-lookup"><span data-stu-id="a085e-1027">See usage condenser above.</span></span> |<span data-ttu-id="a085e-1028">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-1028">Integer</span></span> |<span data-ttu-id="a085e-1029">co najmniej 2 (zwrotną Wyłącz 0)</span><span class="sxs-lookup"><span data-stu-id="a085e-1029">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a085e-1030">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a085e-1030">UserCutOffUpperBound</span></span> |<span data-ttu-id="a085e-1031">Definiuje hello użytkownika górna granica zwrotną hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1031">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="a085e-1032">Zobacz użycie zwrotną powyżej.</span><span class="sxs-lookup"><span data-stu-id="a085e-1032">See usage condenser above.</span></span> |<span data-ttu-id="a085e-1033">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-1033">Integer</span></span> |<span data-ttu-id="a085e-1034">co najmniej 2 (zwrotną Wyłącz 0)</span><span class="sxs-lookup"><span data-stu-id="a085e-1034">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a085e-1035">Opis</span><span class="sxs-lookup"><span data-stu-id="a085e-1035">Description</span></span> |<span data-ttu-id="a085e-1036">Tworzenie opisu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1036">Build description.</span></span> |<span data-ttu-id="a085e-1037">Ciąg</span><span class="sxs-lookup"><span data-stu-id="a085e-1037">String</span></span> |<span data-ttu-id="a085e-1038">Dowolny tekst maksymalne 512 znaków</span><span class="sxs-lookup"><span data-stu-id="a085e-1038">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="a085e-1039">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="a085e-1039">EnableModelingInsights</span></span> |<span data-ttu-id="a085e-1040">Umożliwia toocompute metryki na powitania zalecenie modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1040">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="a085e-1041">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a085e-1041">Boolean</span></span> |<span data-ttu-id="a085e-1042">PRAWDA/FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1042">True/False</span></span> |
| <span data-ttu-id="a085e-1043">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="a085e-1043">UseFeaturesInModel</span></span> |<span data-ttu-id="a085e-1044">Wskazuje, czy funkcje mogą być używane w kolejności tooenhance hello zalecenie modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1044">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="a085e-1045">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a085e-1045">Boolean</span></span> |<span data-ttu-id="a085e-1046">PRAWDA/FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1046">True/False</span></span> |
| <span data-ttu-id="a085e-1047">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="a085e-1047">ModelingFeatureList</span></span> |<span data-ttu-id="a085e-1048">Rozdzielana przecinkami lista toobe nazwy funkcji używane w hello zalecenie kompilacji, w kolejności tooenhance hello zalecenia.</span><span class="sxs-lookup"><span data-stu-id="a085e-1048">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="a085e-1049">Ciąg</span><span class="sxs-lookup"><span data-stu-id="a085e-1049">String</span></span> |<span data-ttu-id="a085e-1050">Nazwy funkcji się too512 znaków</span><span class="sxs-lookup"><span data-stu-id="a085e-1050">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="a085e-1051">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="a085e-1051">AllowColdItemPlacement</span></span> |<span data-ttu-id="a085e-1052">Wskazuje, czy zalecenie hello ma również wypychać zimnych elementów za pomocą funkcji podobieństwa.</span><span class="sxs-lookup"><span data-stu-id="a085e-1052">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="a085e-1053">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a085e-1053">Boolean</span></span> |<span data-ttu-id="a085e-1054">PRAWDA/FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1054">True/False</span></span> |
| <span data-ttu-id="a085e-1055">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="a085e-1055">EnableFeatureCorrelation</span></span> |<span data-ttu-id="a085e-1056">Wskazuje, czy funkcje mogą być używane w uzasadnienie.</span><span class="sxs-lookup"><span data-stu-id="a085e-1056">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="a085e-1057">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a085e-1057">Boolean</span></span> |<span data-ttu-id="a085e-1058">PRAWDA/FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1058">True/False</span></span> |
| <span data-ttu-id="a085e-1059">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="a085e-1059">ReasoningFeatureList</span></span> |<span data-ttu-id="a085e-1060">Rozdzielana przecinkami lista toobe nazwy funkcji używany do wnioskowania zdań (np. zalecenie wyjaśnienia).</span><span class="sxs-lookup"><span data-stu-id="a085e-1060">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="a085e-1061">Ciąg</span><span class="sxs-lookup"><span data-stu-id="a085e-1061">String</span></span> |<span data-ttu-id="a085e-1062">Nazwy funkcji się too512 znaków</span><span class="sxs-lookup"><span data-stu-id="a085e-1062">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="a085e-1063">EnableU2I</span><span class="sxs-lookup"><span data-stu-id="a085e-1063">EnableU2I</span></span> |<span data-ttu-id="a085e-1064">Zezwalaj na powitania spersonalizowanych zalecenie alias</span><span class="sxs-lookup"><span data-stu-id="a085e-1064">Allow hello personalized recommendation a.k.a.</span></span> <span data-ttu-id="a085e-1065">U2I (zalecenia tooitem użytkownika).</span><span class="sxs-lookup"><span data-stu-id="a085e-1065">U2I (user tooitem recommendations).</span></span> |<span data-ttu-id="a085e-1066">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a085e-1066">Boolean</span></span> |<span data-ttu-id="a085e-1067">PRAWDA/FAŁSZ (domyślna wartość true)</span><span class="sxs-lookup"><span data-stu-id="a085e-1067">True/False (default true)</span></span> |

##### <a name="1114-fbt-build-parameters"></a><span data-ttu-id="a085e-1068">11.1.4.</span><span class="sxs-lookup"><span data-stu-id="a085e-1068">11.1.4.</span></span> <span data-ttu-id="a085e-1069">Parametry kompilacji zmianie wysokości progów</span><span class="sxs-lookup"><span data-stu-id="a085e-1069">FBT build parameters</span></span>
<span data-ttu-id="a085e-1070">Witaj w poniższej tabeli przedstawiono hello parametry kompilacji dla kompilacji zalecenie.</span><span class="sxs-lookup"><span data-stu-id="a085e-1070">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="a085e-1071">Klucz</span><span class="sxs-lookup"><span data-stu-id="a085e-1071">Key</span></span> | <span data-ttu-id="a085e-1072">Opis</span><span class="sxs-lookup"><span data-stu-id="a085e-1072">Description</span></span> | <span data-ttu-id="a085e-1073">Typ</span><span class="sxs-lookup"><span data-stu-id="a085e-1073">Type</span></span> | <span data-ttu-id="a085e-1074">Nieprawidłowa wartość (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="a085e-1074">Valid Value (Default)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a085e-1075">FbtSupportThreshold</span><span class="sxs-lookup"><span data-stu-id="a085e-1075">FbtSupportThreshold</span></span> |<span data-ttu-id="a085e-1076">Jak model zachowawcze hello jest.</span><span class="sxs-lookup"><span data-stu-id="a085e-1076">How conservative hello model is.</span></span> <span data-ttu-id="a085e-1077">Liczba wystąpień wspólnej toobe elementów brany pod uwagę podczas modelowania.</span><span class="sxs-lookup"><span data-stu-id="a085e-1077">Number of co-occurrences of items toobe considered for modeling.</span></span> |<span data-ttu-id="a085e-1078">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-1078">Integer</span></span> |<span data-ttu-id="a085e-1079">3-50 (6)</span><span class="sxs-lookup"><span data-stu-id="a085e-1079">3-50 (6)</span></span> |
| <span data-ttu-id="a085e-1080">FbtMaxItemSetSize</span><span class="sxs-lookup"><span data-stu-id="a085e-1080">FbtMaxItemSetSize</span></span> |<span data-ttu-id="a085e-1081">Granice hello liczba elementów w zestawie częste.</span><span class="sxs-lookup"><span data-stu-id="a085e-1081">Bounds hello number of items in a frequent set.</span></span> |<span data-ttu-id="a085e-1082">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-1082">Integer</span></span> |<span data-ttu-id="a085e-1083">2-3 (2)</span><span class="sxs-lookup"><span data-stu-id="a085e-1083">2-3 (2)</span></span> |
| <span data-ttu-id="a085e-1084">FbtMinimalScore</span><span class="sxs-lookup"><span data-stu-id="a085e-1084">FbtMinimalScore</span></span> |<span data-ttu-id="a085e-1085">Wynik minimalnego częste zestaw powinny mieć w kolejności toobe objęte hello zwrócone wyniki.</span><span class="sxs-lookup"><span data-stu-id="a085e-1085">Minimal score that a frequent set should have in order toobe included in hello returned results.</span></span> <span data-ttu-id="a085e-1086">Witaj wyższej Witaj lepiej.</span><span class="sxs-lookup"><span data-stu-id="a085e-1086">hello higher hello better.</span></span> |<span data-ttu-id="a085e-1087">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="a085e-1087">Double</span></span> |<span data-ttu-id="a085e-1088">0 lub nowszym (0)</span><span class="sxs-lookup"><span data-stu-id="a085e-1088">0 and above (0)</span></span> |
| <span data-ttu-id="a085e-1089">FbtSimilarityFunction</span><span class="sxs-lookup"><span data-stu-id="a085e-1089">FbtSimilarityFunction</span></span> |<span data-ttu-id="a085e-1090">Definiuje toobe funkcja podobieństwa hello używane przez hello kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1090">Defines hello similarity function toobe used by hello build.</span></span> <span data-ttu-id="a085e-1091">Przyrostu objawach serendipity, wspólnej wystąpienie objawach przewidywalności i Jaccard stanowi dobry kompromis między hello dwa.</span><span class="sxs-lookup"><span data-stu-id="a085e-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between hello two.</span></span> |<span data-ttu-id="a085e-1092">Ciąg</span><span class="sxs-lookup"><span data-stu-id="a085e-1092">String</span></span> |<span data-ttu-id="a085e-1093">cooccurrence przyrostu, jaccard (przyrostu)</span><span class="sxs-lookup"><span data-stu-id="a085e-1093">cooccurrence, lift, jaccard (lift)</span></span> |

### <a name="112-trigger-a-recommendation-build"></a><span data-ttu-id="a085e-1094">11.2.</span><span class="sxs-lookup"><span data-stu-id="a085e-1094">11.2.</span></span> <span data-ttu-id="a085e-1095">Wyzwalacz kompilacji zalecenia</span><span class="sxs-lookup"><span data-stu-id="a085e-1095">Trigger a Recommendation Build</span></span>
  <span data-ttu-id="a085e-1096">Domyślnie ten interfejs API wyzwoli kompilacji modelu zalecenia.</span><span class="sxs-lookup"><span data-stu-id="a085e-1096">By default this API will trigger a recommendation model build.</span></span> <span data-ttu-id="a085e-1097">tootrigger rangę kompilacji (w kolejności tooscore funkcji), hello kompilacji interfejsu API wariant z parametrem typu kompilacji powinien być używany.</span><span class="sxs-lookup"><span data-stu-id="a085e-1097">tootrigger a rank build (in order tooscore  features), hello build API variant with build type parameter should be used.</span></span>

| <span data-ttu-id="a085e-1098">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1098">HTTP Method</span></span> | <span data-ttu-id="a085e-1099">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1099">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1100">POST</span><span class="sxs-lookup"><span data-stu-id="a085e-1100">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1101">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-1101">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| <span data-ttu-id="a085e-1102">NAGŁÓWEK</span><span class="sxs-lookup"><span data-stu-id="a085e-1102">HEADER</span></span> |<span data-ttu-id="a085e-1103">`"Content-Type", "text/xml"`(Jeśli wysyła treść żądania)</span><span class="sxs-lookup"><span data-stu-id="a085e-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="a085e-1104">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1104">Parameter Name</span></span> | <span data-ttu-id="a085e-1105">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1105">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1106">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-1106">modelId</span></span> |<span data-ttu-id="a085e-1107">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-1107">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-1108">userDescription</span><span class="sxs-lookup"><span data-stu-id="a085e-1108">userDescription</span></span> |<span data-ttu-id="a085e-1109">Identyfikator tekstową hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1109">Textual identifier of hello catalog.</span></span> <span data-ttu-id="a085e-1110">Należy zwrócić uwagę, jeśli używasz spacje musi kodowanie go % 20 zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="a085e-1110">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="a085e-1111">Zobacz przykład powyżej.</span><span class="sxs-lookup"><span data-stu-id="a085e-1111">See example above.</span></span><br><span data-ttu-id="a085e-1112">Długość maksymalna: 50</span><span class="sxs-lookup"><span data-stu-id="a085e-1112">Max length: 50</span></span> |
| <span data-ttu-id="a085e-1113">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1113">apiVersion</span></span> |<span data-ttu-id="a085e-1114">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1114">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-1115">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-1115">Request Body</span></span> |<span data-ttu-id="a085e-1116">Jeśli pole pozostanie puste hello kompilacji zostaną wykonane z hello domyślne parametry kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1116">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="a085e-1117">Parametry kompilacji hello tooset, wysłać hello parametrów jako XML na treść hello jak hello następujące przykładowe.</span><span class="sxs-lookup"><span data-stu-id="a085e-1117">If you want tooset hello build parameters, send hello parameters as XML into hello body as in hello following sample.</span></span> <span data-ttu-id="a085e-1118">(Zobacz sekcji hello "Parametry kompilacji" Aby uzyskać informacje o parametrach hello).`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="a085e-1118">(See hello "Build parameters" section for an explanation of hello parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span></span> |

<span data-ttu-id="a085e-1119">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-1119">**Response**:</span></span>

<span data-ttu-id="a085e-1120">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1120">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-1121">Jest to interfejs API asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="a085e-1121">This is an asynchronous API.</span></span> <span data-ttu-id="a085e-1122">Otrzymasz identyfikator kompilacji w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a085e-1122">You will get a build ID as a response.</span></span> <span data-ttu-id="a085e-1123">tooknow po zakończeniu kompilacji hello, należy wywołać interfejs API "Pobierz kompilacje stan modelu" hello i zlokalizuj identyfikator to kompilacji w hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a085e-1123">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="a085e-1124">Należy pamiętać, że kompilacja może trwać od toohours minut w zależności od wielkości hello hello danych.</span><span class="sxs-lookup"><span data-stu-id="a085e-1124">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="a085e-1125">Nie można używać zalecenia, dopóki hello kompilacji kończy się.</span><span class="sxs-lookup"><span data-stu-id="a085e-1125">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="a085e-1126">Stan prawidłowy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="a085e-1126">Valid build status:</span></span>

* <span data-ttu-id="a085e-1127">Utwórz — żądanie kompilacji zostało utworzone.</span><span class="sxs-lookup"><span data-stu-id="a085e-1127">Create - Build request was created.</span></span>
* <span data-ttu-id="a085e-1128">W kolejce - wysłano żądanie kompilacji i jest w kolejce.</span><span class="sxs-lookup"><span data-stu-id="a085e-1128">Queued - Build request was sent and it is queued.</span></span>
* <span data-ttu-id="a085e-1129">Trwa kompilowanie - kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1129">Building - Build is in progress.</span></span>
* <span data-ttu-id="a085e-1130">Sukces - kompilacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a085e-1130">Success - Build ended successfully.</span></span>
* <span data-ttu-id="a085e-1131">Błąd — Kompilacja została zakończona z błędem.</span><span class="sxs-lookup"><span data-stu-id="a085e-1131">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="a085e-1132">Anulowane — Kompilacja została anulowana.</span><span class="sxs-lookup"><span data-stu-id="a085e-1132">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="a085e-1133">Anulowanie — wysłano żądanie anulowania kompilacji hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1133">Cancelling - A cancel request for hello build was sent.</span></span>

<span data-ttu-id="a085e-1134">Należy zwrócić uwagę tej kompilacji hello identyfikator można znaleźć pod ścieżką hello:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="a085e-1134">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="a085e-1135">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-1135">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a><span data-ttu-id="a085e-1136">11.3.</span><span class="sxs-lookup"><span data-stu-id="a085e-1136">11.3.</span></span> <span data-ttu-id="a085e-1137">Wyzwalacz kompilacji (zalecenie, pozycja lub zmianie wysokości progów)</span><span class="sxs-lookup"><span data-stu-id="a085e-1137">Trigger Build (Recommendation, Rank or FBT)</span></span>
| <span data-ttu-id="a085e-1138">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1138">HTTP Method</span></span> | <span data-ttu-id="a085e-1139">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1139">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1140">POST</span><span class="sxs-lookup"><span data-stu-id="a085e-1140">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1141">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-1141">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| <span data-ttu-id="a085e-1142">NAGŁÓWEK</span><span class="sxs-lookup"><span data-stu-id="a085e-1142">HEADER</span></span> |<span data-ttu-id="a085e-1143">`"Content-Type", "text/xml"`(Jeśli wysyła treść żądania)</span><span class="sxs-lookup"><span data-stu-id="a085e-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="a085e-1144">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1144">Parameter Name</span></span> | <span data-ttu-id="a085e-1145">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1145">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1146">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-1146">modelId</span></span> |<span data-ttu-id="a085e-1147">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-1147">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-1148">userDescription</span><span class="sxs-lookup"><span data-stu-id="a085e-1148">userDescription</span></span> |<span data-ttu-id="a085e-1149">Identyfikator tekstową hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1149">Textual identifier of hello catalog.</span></span> <span data-ttu-id="a085e-1150">Należy zwrócić uwagę, jeśli używasz spacje musi kodowanie go % 20 zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="a085e-1150">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="a085e-1151">Zobacz przykład powyżej.</span><span class="sxs-lookup"><span data-stu-id="a085e-1151">See example above.</span></span><br><span data-ttu-id="a085e-1152">Długość maksymalna: 50</span><span class="sxs-lookup"><span data-stu-id="a085e-1152">Max length: 50</span></span> |
| <span data-ttu-id="a085e-1153">buildType</span><span class="sxs-lookup"><span data-stu-id="a085e-1153">buildType</span></span> |<span data-ttu-id="a085e-1154">Typ hello tooinvoke kompilacji:</span><span class="sxs-lookup"><span data-stu-id="a085e-1154">Type of hello build tooinvoke:</span></span> <br/> <span data-ttu-id="a085e-1155">-"Zalecenie" dla kompilacji zalecenia</span><span class="sxs-lookup"><span data-stu-id="a085e-1155">- 'Recommendation' for recommendation build</span></span> <br> <span data-ttu-id="a085e-1156">-Klasyfikacji dla rangi kompilacji</span><span class="sxs-lookup"><span data-stu-id="a085e-1156">- 'Ranking' for rank build</span></span> <br/> <span data-ttu-id="a085e-1157">-Zmianie wysokości "progów" dla kompilacji zmianie wysokości progów</span><span class="sxs-lookup"><span data-stu-id="a085e-1157">- 'Fbt' for FBT build</span></span> |
| <span data-ttu-id="a085e-1158">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1158">apiVersion</span></span> |<span data-ttu-id="a085e-1159">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1159">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-1160">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-1160">Request Body</span></span> |<span data-ttu-id="a085e-1161">Jeśli pole pozostanie puste hello kompilacji zostaną wykonane z hello domyślne parametry kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1161">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="a085e-1162">Jeśli chcesz, aby parametry kompilacji tooset, wysyłać je jako XML na treść hello podobnie jak w hello następujące przykładowe.</span><span class="sxs-lookup"><span data-stu-id="a085e-1162">If you want tooset build parameters, send them as XML into hello body like in hello following sample.</span></span> <span data-ttu-id="a085e-1163">(W sekcji hello "Parametry kompilacji" wyjaśnienie i Pełna lista parametrów hello.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="a085e-1163">(See hello "Build parameters" section for an explanation and full list of hello parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span></span> |

<span data-ttu-id="a085e-1164">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-1164">**Response**:</span></span>

<span data-ttu-id="a085e-1165">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1165">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-1166">Jest to interfejs API asynchronicznego.</span><span class="sxs-lookup"><span data-stu-id="a085e-1166">This is an asynchronous API.</span></span> <span data-ttu-id="a085e-1167">Otrzymasz identyfikator kompilacji w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a085e-1167">You will get a build ID as a response.</span></span> <span data-ttu-id="a085e-1168">tooknow po zakończeniu kompilacji hello, należy wywołać interfejs API "Pobierz kompilacje stan modelu" hello i zlokalizuj identyfikator to kompilacji w hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a085e-1168">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="a085e-1169">Należy pamiętać, że kompilacja może trwać od toohours minut w zależności od wielkości hello hello danych.</span><span class="sxs-lookup"><span data-stu-id="a085e-1169">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="a085e-1170">Nie można używać zalecenia, dopóki hello kompilacji kończy się.</span><span class="sxs-lookup"><span data-stu-id="a085e-1170">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="a085e-1171">Stan prawidłowy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="a085e-1171">Valid build status:</span></span>

* <span data-ttu-id="a085e-1172">Utwórz — Model został utworzony.</span><span class="sxs-lookup"><span data-stu-id="a085e-1172">Create - Model was created.</span></span>
* <span data-ttu-id="a085e-1173">W kolejce — zostało wyzwolone kompilacji modelu i jest w kolejce.</span><span class="sxs-lookup"><span data-stu-id="a085e-1173">Queued - Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="a085e-1174">Kompilowanie — Model została skompilowana.</span><span class="sxs-lookup"><span data-stu-id="a085e-1174">Building - Model is being built.</span></span>
* <span data-ttu-id="a085e-1175">Sukces - kompilacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a085e-1175">Success - Build ended successfully.</span></span>
* <span data-ttu-id="a085e-1176">Błąd — Kompilacja została zakończona z błędem.</span><span class="sxs-lookup"><span data-stu-id="a085e-1176">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="a085e-1177">Anulowane — Kompilacja została anulowana.</span><span class="sxs-lookup"><span data-stu-id="a085e-1177">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="a085e-1178">Anulowanie - Trwa anulowanie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1178">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="a085e-1179">Należy zwrócić uwagę tej kompilacji hello identyfikator można znaleźć pod ścieżką hello:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="a085e-1179">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="a085e-1180">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-1180">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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




### <a name="114-get-builds-status-of-a-model"></a><span data-ttu-id="a085e-1181">11.4.</span><span class="sxs-lookup"><span data-stu-id="a085e-1181">11.4.</span></span> <span data-ttu-id="a085e-1182">Pobierz stan kompilacji modelu</span><span class="sxs-lookup"><span data-stu-id="a085e-1182">Get Builds Status of a Model</span></span>
<span data-ttu-id="a085e-1183">Pobiera kompilacji i ich stanu dla określonego modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1183">Retrieves builds and their status for a specified model.</span></span>

| <span data-ttu-id="a085e-1184">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1184">HTTP Method</span></span> | <span data-ttu-id="a085e-1185">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1185">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1186">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1186">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1187">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-1187">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-1188">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1188">Parameter Name</span></span> | <span data-ttu-id="a085e-1189">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1189">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1190">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-1190">modelId</span></span> |<span data-ttu-id="a085e-1191">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-1191">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-1192">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="a085e-1192">onlyLastBuild</span></span> |<span data-ttu-id="a085e-1193">Wskazuje, czy wszystkie hello tooreturn kompilacji tylko stan hello hello ostatniej kompilacji lub historii hello modelu</span><span class="sxs-lookup"><span data-stu-id="a085e-1193">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build</span></span> |
| <span data-ttu-id="a085e-1194">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1194">apiVersion</span></span> |<span data-ttu-id="a085e-1195">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1195">1.0</span></span> |

<span data-ttu-id="a085e-1196">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-1196">**Response**:</span></span>

<span data-ttu-id="a085e-1197">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1197">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-1198">odpowiedź Hello zawiera jednego wpisu na kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1198">hello response includes one entry per build.</span></span> <span data-ttu-id="a085e-1199">Każdy wpis ma hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="a085e-1199">Each entry has hello following data:</span></span>

* <span data-ttu-id="a085e-1200">`feed/entry/content/properties/UserName`-Nazwa hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a085e-1200">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="a085e-1201">`feed/entry/content/properties/ModelName`-Nazwa hello modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1201">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="a085e-1202">`feed/entry/content/properties/ModelId`-Unikatowy identyfikator modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="a085e-1203">`feed/entry/content/properties/IsDeployed`— Czy kompilacja hello jest wdrożona ()</span><span class="sxs-lookup"><span data-stu-id="a085e-1203">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="a085e-1204">aktywne kompilacji).</span><span class="sxs-lookup"><span data-stu-id="a085e-1204">active build).</span></span>
* <span data-ttu-id="a085e-1205">`feed/entry/content/properties/BuildId`-Utwórz unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="a085e-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="a085e-1206">`feed/entry/content/properties/BuildType`— Typ hello kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1206">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="a085e-1207">`feed/entry/content/properties/Status`-Stan kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1207">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="a085e-1208">Może być jedną z następujących hello: błąd, kompilowanie, w kolejce, Cancelling odwołania, Powodzenie.</span><span class="sxs-lookup"><span data-stu-id="a085e-1208">Can be one of hello following: Error, Building, Queued, Cancelling, Cancelled, Success.</span></span>
* <span data-ttu-id="a085e-1209">`feed/entry/content/properties/StatusMessage`— Komunikat o stanie szczegółowe (dotyczy tylko Stany toospecific).</span><span class="sxs-lookup"><span data-stu-id="a085e-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="a085e-1210">`feed/entry/content/properties/Progress`-Kompilacji postępu (%).</span><span class="sxs-lookup"><span data-stu-id="a085e-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="a085e-1211">`feed/entry/content/properties/StartTime`-Godzina rozpoczęcia kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1211">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="a085e-1212">`feed/entry/content/properties/EndTime`-Czas zakończenia kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1212">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="a085e-1213">`feed/entry/content/properties/ExecutionTime`— Czas trwania kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="a085e-1214">`feed/entry/content/properties/ProgressStep`— Szczegółowe informacje o hello bieżący etap kompilacji w toku.</span><span class="sxs-lookup"><span data-stu-id="a085e-1214">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="a085e-1215">Stan prawidłowy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="a085e-1215">Valid build status:</span></span>

* <span data-ttu-id="a085e-1216">Utworzone — wpis żądanie kompilacji zostało utworzone.</span><span class="sxs-lookup"><span data-stu-id="a085e-1216">Created - Build request entry was created.</span></span>
* <span data-ttu-id="a085e-1217">W kolejce — żądanie kompilacji zostało wyzwolone i jest w kolejce.</span><span class="sxs-lookup"><span data-stu-id="a085e-1217">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="a085e-1218">Kompilowanie - kompilacji jest przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1218">Building - Build is in process.</span></span>
* <span data-ttu-id="a085e-1219">Sukces - kompilacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a085e-1219">Success - Build ended successfully.</span></span>
* <span data-ttu-id="a085e-1220">Błąd — Kompilacja została zakończona z błędem.</span><span class="sxs-lookup"><span data-stu-id="a085e-1220">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="a085e-1221">Anulowane — Kompilacja została anulowana.</span><span class="sxs-lookup"><span data-stu-id="a085e-1221">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="a085e-1222">Anulowanie - Trwa anulowanie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1222">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="a085e-1223">Prawidłowe wartości dla typu kompilacji:</span><span class="sxs-lookup"><span data-stu-id="a085e-1223">Valid values for build type:</span></span>

* <span data-ttu-id="a085e-1224">Ranga - rangę kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1224">Rank - Rank build.</span></span>
* <span data-ttu-id="a085e-1225">Zalecenie - zalecenie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1225">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="a085e-1226">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-1226">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="115-get-builds-status"></a><span data-ttu-id="a085e-1227">11.5.</span><span class="sxs-lookup"><span data-stu-id="a085e-1227">11.5.</span></span> <span data-ttu-id="a085e-1228">Pobierz stan kompilacji</span><span class="sxs-lookup"><span data-stu-id="a085e-1228">Get Builds Status</span></span>
<span data-ttu-id="a085e-1229">Pobiera kompilacji statusy wszystkich modeli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a085e-1229">Retrieves build statuses of all models of a user.</span></span>

| <span data-ttu-id="a085e-1230">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1230">HTTP Method</span></span> | <span data-ttu-id="a085e-1231">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1231">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1232">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1232">GET</span></span> |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1233">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-1233">Example:</span></span><br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-1234">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1234">Parameter Name</span></span> | <span data-ttu-id="a085e-1235">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1235">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1236">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="a085e-1236">onlyLastBuild</span></span> |<span data-ttu-id="a085e-1237">Wskazuje, czy wszystkie hello tooreturn kompilacji tylko stan hello hello ostatniej kompilacji lub historii hello modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1237">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="a085e-1238">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1238">apiVersion</span></span> |<span data-ttu-id="a085e-1239">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1239">1.0</span></span> |

<span data-ttu-id="a085e-1240">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-1240">**Response**:</span></span>

<span data-ttu-id="a085e-1241">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1241">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-1242">odpowiedź Hello zawiera jednego wpisu na kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1242">hello response includes one entry per build.</span></span> <span data-ttu-id="a085e-1243">Każdy wpis ma hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="a085e-1243">Each entry has hello following data:</span></span>

* <span data-ttu-id="a085e-1244">`feed/entry/content/properties/UserName`-Nazwa hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a085e-1244">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="a085e-1245">`feed/entry/content/properties/ModelName`-Nazwa hello modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1245">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="a085e-1246">`feed/entry/content/properties/ModelId`-Unikatowy identyfikator modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="a085e-1247">`feed/entry/content/properties/IsDeployed`— Czy hello kompilacja zostaje wdrożona.</span><span class="sxs-lookup"><span data-stu-id="a085e-1247">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed.</span></span>
* <span data-ttu-id="a085e-1248">`feed/entry/content/properties/BuildId`-Utwórz unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="a085e-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="a085e-1249">`feed/entry/content/properties/BuildType`— Typ hello kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1249">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="a085e-1250">`feed/entry/content/properties/Status`-Stan kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1250">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="a085e-1251">Może być jedną z następujących hello: błąd, kompilowanie, w kolejce, odwołania, Cancelling, Powodzenie.</span><span class="sxs-lookup"><span data-stu-id="a085e-1251">Can be one of hello following: Error, Building, Queued, Cancelled, Cancelling, Success.</span></span>
* <span data-ttu-id="a085e-1252">`feed/entry/content/properties/StatusMessage`— Komunikat o stanie szczegółowe (dotyczy tylko Stany toospecific).</span><span class="sxs-lookup"><span data-stu-id="a085e-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="a085e-1253">`feed/entry/content/properties/Progress`-Kompilacji postępu (%).</span><span class="sxs-lookup"><span data-stu-id="a085e-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="a085e-1254">`feed/entry/content/properties/StartTime`-Godzina rozpoczęcia kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1254">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="a085e-1255">`feed/entry/content/properties/EndTime`-Czas zakończenia kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1255">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="a085e-1256">`feed/entry/content/properties/ExecutionTime`— Czas trwania kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="a085e-1257">`feed/entry/content/properties/ProgressStep`— Szczegółowe informacje o hello bieżący etap kompilacji w toku.</span><span class="sxs-lookup"><span data-stu-id="a085e-1257">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="a085e-1258">Stan prawidłowy kompilacji:</span><span class="sxs-lookup"><span data-stu-id="a085e-1258">Valid build status:</span></span>

* <span data-ttu-id="a085e-1259">Utworzone — wpis żądanie kompilacji zostało utworzone.</span><span class="sxs-lookup"><span data-stu-id="a085e-1259">Created - Build request entry was created.</span></span>
* <span data-ttu-id="a085e-1260">W kolejce — żądanie kompilacji zostało wyzwolone i jest w kolejce.</span><span class="sxs-lookup"><span data-stu-id="a085e-1260">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="a085e-1261">Kompilowanie - kompilacji jest przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1261">Building - Build is in process.</span></span>
* <span data-ttu-id="a085e-1262">Sukces - kompilacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a085e-1262">Success - Build ended successfully.</span></span>
* <span data-ttu-id="a085e-1263">Błąd — Kompilacja została zakończona z błędem.</span><span class="sxs-lookup"><span data-stu-id="a085e-1263">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="a085e-1264">Anulowane — Kompilacja została anulowana.</span><span class="sxs-lookup"><span data-stu-id="a085e-1264">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="a085e-1265">Anulowanie - Trwa anulowanie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1265">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="a085e-1266">Prawidłowe wartości dla typu kompilacji:</span><span class="sxs-lookup"><span data-stu-id="a085e-1266">Valid values for build type:</span></span>

* <span data-ttu-id="a085e-1267">Ranga - rangę kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1267">Rank - Rank build.</span></span>
* <span data-ttu-id="a085e-1268">Zalecenie - zalecenie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1268">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="a085e-1269">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-1269">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="116-delete-build"></a><span data-ttu-id="a085e-1270">11.6.</span><span class="sxs-lookup"><span data-stu-id="a085e-1270">11.6.</span></span> <span data-ttu-id="a085e-1271">Usuń kompilacji</span><span class="sxs-lookup"><span data-stu-id="a085e-1271">Delete Build</span></span>
<span data-ttu-id="a085e-1272">Usuwa kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1272">Deletes a build.</span></span>

<span data-ttu-id="a085e-1273">UWAGA:</span><span class="sxs-lookup"><span data-stu-id="a085e-1273">NOTE:</span></span> <br><span data-ttu-id="a085e-1274">Nie można usunąć aktywnej kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1274">You cannot delete an active build.</span></span> <span data-ttu-id="a085e-1275">Witaj model powinien być zaktualizowany inną kompilację active tooa przed jego usunięciem.</span><span class="sxs-lookup"><span data-stu-id="a085e-1275">hello model should be updated tooa different active build before you delete it.</span></span><br><span data-ttu-id="a085e-1276">Nie można usunąć kompilacji w toku.</span><span class="sxs-lookup"><span data-stu-id="a085e-1276">You cannot delete an in-progress build.</span></span> <span data-ttu-id="a085e-1277">Należy anulować kompilacji hello najpierw przez wywołanie metody <strong>anulowania kompilacji</strong>.</span><span class="sxs-lookup"><span data-stu-id="a085e-1277">You should cancel hello build first by calling <strong>Cancel Build</strong>.</span></span>

| <span data-ttu-id="a085e-1278">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1278">HTTP Method</span></span> | <span data-ttu-id="a085e-1279">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1279">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1280">USUŃ</span><span class="sxs-lookup"><span data-stu-id="a085e-1280">DELETE</span></span> |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1281">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-1281">Example:</span></span><br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-1282">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1282">Parameter Name</span></span> | <span data-ttu-id="a085e-1283">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1283">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1284">identyfikatora buildId</span><span class="sxs-lookup"><span data-stu-id="a085e-1284">buildId</span></span> |<span data-ttu-id="a085e-1285">Unikatowy identyfikator hello kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1285">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="a085e-1286">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1286">apiVersion</span></span> |<span data-ttu-id="a085e-1287">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1287">1.0</span></span> |

<span data-ttu-id="a085e-1288">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="a085e-1288">**Response:**</span></span>

<span data-ttu-id="a085e-1289">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1289">HTTP Status code: 200</span></span>

### <a name="117-cancel-build"></a><span data-ttu-id="a085e-1290">11.7.</span><span class="sxs-lookup"><span data-stu-id="a085e-1290">11.7.</span></span> <span data-ttu-id="a085e-1291">Anulowanie kompilacji</span><span class="sxs-lookup"><span data-stu-id="a085e-1291">Cancel Build</span></span>
<span data-ttu-id="a085e-1292">Anuluje kompilacji, która w budynku stanu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1292">Cancels a build that is in building status.</span></span>

| <span data-ttu-id="a085e-1293">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1293">HTTP Method</span></span> | <span data-ttu-id="a085e-1294">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1294">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1295">UMIEŚĆ</span><span class="sxs-lookup"><span data-stu-id="a085e-1295">PUT</span></span> |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1296">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-1296">Example:</span></span><br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-1297">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1297">Parameter Name</span></span> | <span data-ttu-id="a085e-1298">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1298">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1299">identyfikatora buildId</span><span class="sxs-lookup"><span data-stu-id="a085e-1299">buildId</span></span> |<span data-ttu-id="a085e-1300">Unikatowy identyfikator hello kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1300">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="a085e-1301">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1301">apiVersion</span></span> |<span data-ttu-id="a085e-1302">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1302">1.0</span></span> |

<span data-ttu-id="a085e-1303">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="a085e-1303">**Response:**</span></span>

<span data-ttu-id="a085e-1304">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1304">HTTP Status code: 200</span></span>

### <a name="118-get-build-parameters"></a><span data-ttu-id="a085e-1305">11.8.</span><span class="sxs-lookup"><span data-stu-id="a085e-1305">11.8.</span></span> <span data-ttu-id="a085e-1306">Pobranie parametrów kompilacji</span><span class="sxs-lookup"><span data-stu-id="a085e-1306">Get Build Parameters</span></span>
<span data-ttu-id="a085e-1307">Pobiera kompilacji parametrów.</span><span class="sxs-lookup"><span data-stu-id="a085e-1307">Retrieves build parameters.</span></span>

| <span data-ttu-id="a085e-1308">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1308">HTTP Method</span></span> | <span data-ttu-id="a085e-1309">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1309">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1310">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1310">GET</span></span> |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1311">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-1311">Example:</span></span><br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-1312">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1312">Parameter Name</span></span> | <span data-ttu-id="a085e-1313">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1313">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1314">identyfikatora buildId</span><span class="sxs-lookup"><span data-stu-id="a085e-1314">buildId</span></span> |<span data-ttu-id="a085e-1315">Unikatowy identyfikator hello kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1315">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="a085e-1316">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1316">apiVersion</span></span> |<span data-ttu-id="a085e-1317">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1317">1.0</span></span> |

<span data-ttu-id="a085e-1318">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="a085e-1318">**Response:**</span></span>

<span data-ttu-id="a085e-1319">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1319">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-1320">Ten interfejs API zwraca kolekcję elementów klucza i wartości.</span><span class="sxs-lookup"><span data-stu-id="a085e-1320">This API returns a collection of key/value elements.</span></span> <span data-ttu-id="a085e-1321">Każdy element reprezentuje parametr i wartość:</span><span class="sxs-lookup"><span data-stu-id="a085e-1321">Each element represents a parameter and its value:</span></span>

* <span data-ttu-id="a085e-1322">`feed/entry/content/properties/Key`-Nazwa parametru kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1322">`feed/entry/content/properties/Key` - Build parameter name.</span></span>
* <span data-ttu-id="a085e-1323">`feed/entry/content/properties/Value`— Wartość parametru kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1323">`feed/entry/content/properties/Value` - Build parameter value.</span></span>

<span data-ttu-id="a085e-1324">Witaj w poniższej tabeli przedstawiono hello wartość, która reprezentuje każdy klucz.</span><span class="sxs-lookup"><span data-stu-id="a085e-1324">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="a085e-1325">Klucz</span><span class="sxs-lookup"><span data-stu-id="a085e-1325">Key</span></span> | <span data-ttu-id="a085e-1326">Opis</span><span class="sxs-lookup"><span data-stu-id="a085e-1326">Description</span></span> | <span data-ttu-id="a085e-1327">Typ</span><span class="sxs-lookup"><span data-stu-id="a085e-1327">Type</span></span> | <span data-ttu-id="a085e-1328">Nieprawidłowa wartość</span><span class="sxs-lookup"><span data-stu-id="a085e-1328">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="a085e-1329">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="a085e-1329">NumberOfModelIterations</span></span> |<span data-ttu-id="a085e-1330">Hello liczby iteracji modelu hello wykonuje, sprawdzając hello obliczeniowe całkowity czas i hello dokładności modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1330">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="a085e-1331">większa liczba hello Hello, hello większej dokładności, zostanie wyświetlony, ale hello obliczeń czas będzie trwać dłużej.</span><span class="sxs-lookup"><span data-stu-id="a085e-1331">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="a085e-1332">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-1332">Integer</span></span> |<span data-ttu-id="a085e-1333">10-50</span><span class="sxs-lookup"><span data-stu-id="a085e-1333">10-50</span></span> |
| <span data-ttu-id="a085e-1334">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="a085e-1334">NumberOfModelDimensions</span></span> |<span data-ttu-id="a085e-1335">Hello liczby wymiarów wiąże się, że liczba toohello "funkcji" hello modelu spróbuje toofind w danych.</span><span class="sxs-lookup"><span data-stu-id="a085e-1335">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="a085e-1336">Zwiększenie liczby hello wymiarów pozwoli lepiej dostrajanie hello wyniki w mniejszych klastrów.</span><span class="sxs-lookup"><span data-stu-id="a085e-1336">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="a085e-1337">Jednak zbyt dużo wymiarów uniemożliwi modelu hello odnalezienie korelacji między elementami.</span><span class="sxs-lookup"><span data-stu-id="a085e-1337">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="a085e-1338">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-1338">Integer</span></span> |<span data-ttu-id="a085e-1339">10-40</span><span class="sxs-lookup"><span data-stu-id="a085e-1339">10-40</span></span> |
| <span data-ttu-id="a085e-1340">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a085e-1340">ItemCutOffLowerBound</span></span> |<span data-ttu-id="a085e-1341">Definiuje element hello dolna granica zwrotną hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1341">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="a085e-1342">Zobacz użycie zwrotną powyżej.</span><span class="sxs-lookup"><span data-stu-id="a085e-1342">See usage condenser above.</span></span> |<span data-ttu-id="a085e-1343">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-1343">Integer</span></span> |<span data-ttu-id="a085e-1344">co najmniej 2 (zwrotną Wyłącz 0)</span><span class="sxs-lookup"><span data-stu-id="a085e-1344">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a085e-1345">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a085e-1345">ItemCutOffUpperBound</span></span> |<span data-ttu-id="a085e-1346">Definiuje element hello górna granica zwrotną hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1346">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="a085e-1347">Zobacz użycie zwrotną powyżej.</span><span class="sxs-lookup"><span data-stu-id="a085e-1347">See usage condenser above.</span></span> |<span data-ttu-id="a085e-1348">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-1348">Integer</span></span> |<span data-ttu-id="a085e-1349">co najmniej 2 (zwrotną Wyłącz 0)</span><span class="sxs-lookup"><span data-stu-id="a085e-1349">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a085e-1350">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="a085e-1350">UserCutOffLowerBound</span></span> |<span data-ttu-id="a085e-1351">Definiuje hello użytkownika dolna granica zwrotną hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1351">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="a085e-1352">Zobacz użycie zwrotną powyżej.</span><span class="sxs-lookup"><span data-stu-id="a085e-1352">See usage condenser above.</span></span> |<span data-ttu-id="a085e-1353">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-1353">Integer</span></span> |<span data-ttu-id="a085e-1354">co najmniej 2 (zwrotną Wyłącz 0)</span><span class="sxs-lookup"><span data-stu-id="a085e-1354">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a085e-1355">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="a085e-1355">UserCutOffUpperBound</span></span> |<span data-ttu-id="a085e-1356">Definiuje hello użytkownika górna granica zwrotną hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1356">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="a085e-1357">Zobacz użycie zwrotną powyżej.</span><span class="sxs-lookup"><span data-stu-id="a085e-1357">See usage condenser above.</span></span> |<span data-ttu-id="a085e-1358">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a085e-1358">Integer</span></span> |<span data-ttu-id="a085e-1359">co najmniej 2 (zwrotną Wyłącz 0)</span><span class="sxs-lookup"><span data-stu-id="a085e-1359">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="a085e-1360">Opis</span><span class="sxs-lookup"><span data-stu-id="a085e-1360">Description</span></span> |<span data-ttu-id="a085e-1361">Tworzenie opisu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1361">Build description.</span></span> |<span data-ttu-id="a085e-1362">Ciąg</span><span class="sxs-lookup"><span data-stu-id="a085e-1362">String</span></span> |<span data-ttu-id="a085e-1363">Dowolny tekst maksymalne 512 znaków</span><span class="sxs-lookup"><span data-stu-id="a085e-1363">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="a085e-1364">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="a085e-1364">EnableModelingInsights</span></span> |<span data-ttu-id="a085e-1365">Umożliwia toocompute metryki na powitania zalecenie modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1365">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="a085e-1366">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a085e-1366">Boolean</span></span> |<span data-ttu-id="a085e-1367">PRAWDA/FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1367">True/False</span></span> |
| <span data-ttu-id="a085e-1368">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="a085e-1368">UseFeaturesInModel</span></span> |<span data-ttu-id="a085e-1369">Wskazuje, czy funkcje mogą być używane w kolejności tooenhance hello zalecenie modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1369">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="a085e-1370">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a085e-1370">Boolean</span></span> |<span data-ttu-id="a085e-1371">PRAWDA/FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1371">True/False</span></span> |
| <span data-ttu-id="a085e-1372">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="a085e-1372">ModelingFeatureList</span></span> |<span data-ttu-id="a085e-1373">Rozdzielana przecinkami lista toobe nazwy funkcji używane w hello zalecenie kompilacji, w kolejności tooenhance hello zalecenia.</span><span class="sxs-lookup"><span data-stu-id="a085e-1373">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="a085e-1374">Ciąg</span><span class="sxs-lookup"><span data-stu-id="a085e-1374">String</span></span> |<span data-ttu-id="a085e-1375">Nazwy funkcji się too512 znaków</span><span class="sxs-lookup"><span data-stu-id="a085e-1375">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="a085e-1376">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="a085e-1376">AllowColdItemPlacement</span></span> |<span data-ttu-id="a085e-1377">Wskazuje, czy zalecenie hello ma również wypychać zimnych elementów za pomocą funkcji podobieństwa.</span><span class="sxs-lookup"><span data-stu-id="a085e-1377">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="a085e-1378">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a085e-1378">Boolean</span></span> |<span data-ttu-id="a085e-1379">PRAWDA/FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1379">True/False</span></span> |
| <span data-ttu-id="a085e-1380">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="a085e-1380">EnableFeatureCorrelation</span></span> |<span data-ttu-id="a085e-1381">Wskazuje, czy funkcje mogą być używane w uzasadnienie.</span><span class="sxs-lookup"><span data-stu-id="a085e-1381">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="a085e-1382">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a085e-1382">Boolean</span></span> |<span data-ttu-id="a085e-1383">PRAWDA/FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1383">True/False</span></span> |
| <span data-ttu-id="a085e-1384">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="a085e-1384">ReasoningFeatureList</span></span> |<span data-ttu-id="a085e-1385">Rozdzielana przecinkami lista toobe nazwy funkcji używany do wnioskowania zdań (np. zalecenie wyjaśnienia).</span><span class="sxs-lookup"><span data-stu-id="a085e-1385">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="a085e-1386">Ciąg</span><span class="sxs-lookup"><span data-stu-id="a085e-1386">String</span></span> |<span data-ttu-id="a085e-1387">Nazwy funkcji się too512 znaków</span><span class="sxs-lookup"><span data-stu-id="a085e-1387">Feature names, up too512 chars</span></span> |

<span data-ttu-id="a085e-1388">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-1388">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a><span data-ttu-id="a085e-1389">12. Zalecenie</span><span class="sxs-lookup"><span data-stu-id="a085e-1389">12. Recommendation</span></span>
### <a name="121-get-item-recommendations-for-active-build"></a><span data-ttu-id="a085e-1390">12.1.</span><span class="sxs-lookup"><span data-stu-id="a085e-1390">12.1.</span></span> <span data-ttu-id="a085e-1391">Uzyskaj element zalecenia (dla active kompilacji)</span><span class="sxs-lookup"><span data-stu-id="a085e-1391">Get Item Recommendations (for active build)</span></span>
<span data-ttu-id="a085e-1392">Pobierz zalecenia hello active kompilacji typu "Zalecenie" lub "Zmianie wysokości progów" na podstawie listy elementów ziarna (dane wejściowe).</span><span class="sxs-lookup"><span data-stu-id="a085e-1392">Get recommendations of hello active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span></span>

| <span data-ttu-id="a085e-1393">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1393">HTTP Method</span></span> | <span data-ttu-id="a085e-1394">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1394">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1395">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1395">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1396">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-1396">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-1397">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1397">Parameter Name</span></span> | <span data-ttu-id="a085e-1398">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1398">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1399">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-1399">modelId</span></span> |<span data-ttu-id="a085e-1400">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-1400">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-1401">identyfikatory elementów</span><span class="sxs-lookup"><span data-stu-id="a085e-1401">itemIds</span></span> |<span data-ttu-id="a085e-1402">Rozdzielana przecinkami lista hello elementów toorecommend dla.</span><span class="sxs-lookup"><span data-stu-id="a085e-1402">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="a085e-1403">Jeśli kompilacja active hello jest wpisz zmianie wysokości progów, a następnie wysłać tylko jeden element.</span><span class="sxs-lookup"><span data-stu-id="a085e-1403">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="a085e-1404">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="a085e-1404">Max length: 1024</span></span> |
| <span data-ttu-id="a085e-1405">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a085e-1405">numberOfResults</span></span> |<span data-ttu-id="a085e-1406">Liczba wymaganych wyników</span><span class="sxs-lookup"><span data-stu-id="a085e-1406">Number of required results</span></span> <br> <span data-ttu-id="a085e-1407">Maksymalna liczba: 150</span><span class="sxs-lookup"><span data-stu-id="a085e-1407">Max: 150</span></span> |
| <span data-ttu-id="a085e-1408">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a085e-1408">includeMetatadata</span></span> |<span data-ttu-id="a085e-1409">Użycia w przyszłości, zawsze false</span><span class="sxs-lookup"><span data-stu-id="a085e-1409">Future use, always false</span></span> |
| <span data-ttu-id="a085e-1410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1410">apiVersion</span></span> |<span data-ttu-id="a085e-1411">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1411">1.0</span></span> |

<span data-ttu-id="a085e-1412">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="a085e-1412">**Response:**</span></span>

<span data-ttu-id="a085e-1413">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1413">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-1414">odpowiedź Hello zawiera jeden wpis dla każdego elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1414">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="a085e-1415">Każdy wpis ma hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="a085e-1415">Each entry has hello following data:</span></span>

* <span data-ttu-id="a085e-1416">`Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a085e-1417">`Feed\entry\content\properties\Name`-Nazwa elementu hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1417">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="a085e-1418">`Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.</span><span class="sxs-lookup"><span data-stu-id="a085e-1418">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a085e-1419">`Feed\entry\content\properties\Reasoning`-Zalecenie wnioskowania (np. zalecenie wyjaśnienia).</span><span class="sxs-lookup"><span data-stu-id="a085e-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a085e-1420">odpowiedź przykład Hello poniżej zawiera 10 elementów zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1420">hello example response below includes 10 recommended items.</span></span>

<span data-ttu-id="a085e-1421">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-1421">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
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

### <a name="122-get-item-recommendations-of-a-specific-build"></a><span data-ttu-id="a085e-1422">12.2.</span><span class="sxs-lookup"><span data-stu-id="a085e-1422">12.2.</span></span> <span data-ttu-id="a085e-1423">Pobierz element zalecenia (określonej kompilacji)</span><span class="sxs-lookup"><span data-stu-id="a085e-1423">Get Item Recommendations (of a specific build)</span></span>
<span data-ttu-id="a085e-1424">Pobierz zalecenia określonej kompilacji typu "Zalecenie" lub "Zmianie wysokości progów".</span><span class="sxs-lookup"><span data-stu-id="a085e-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span></span>

| <span data-ttu-id="a085e-1425">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1425">HTTP Method</span></span> | <span data-ttu-id="a085e-1426">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1426">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1427">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1427">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1428">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-1428">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-1429">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1429">Parameter Name</span></span> | <span data-ttu-id="a085e-1430">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1430">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1431">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-1431">modelId</span></span> |<span data-ttu-id="a085e-1432">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-1432">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-1433">identyfikatory elementów</span><span class="sxs-lookup"><span data-stu-id="a085e-1433">itemIds</span></span> |<span data-ttu-id="a085e-1434">Rozdzielana przecinkami lista hello elementów toorecommend dla.</span><span class="sxs-lookup"><span data-stu-id="a085e-1434">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="a085e-1435">Jeśli kompilacja active hello jest wpisz zmianie wysokości progów, a następnie wysłać tylko jeden element.</span><span class="sxs-lookup"><span data-stu-id="a085e-1435">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="a085e-1436">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="a085e-1436">Max length: 1024</span></span> |
| <span data-ttu-id="a085e-1437">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a085e-1437">numberOfResults</span></span> |<span data-ttu-id="a085e-1438">Liczba wymaganych wyników</span><span class="sxs-lookup"><span data-stu-id="a085e-1438">Number of required results</span></span> <br> <span data-ttu-id="a085e-1439">Maksymalna liczba: 150</span><span class="sxs-lookup"><span data-stu-id="a085e-1439">Max: 150</span></span> |
| <span data-ttu-id="a085e-1440">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a085e-1440">includeMetatadata</span></span> |<span data-ttu-id="a085e-1441">Użycia w przyszłości, zawsze false</span><span class="sxs-lookup"><span data-stu-id="a085e-1441">Future use, always false</span></span> |
| <span data-ttu-id="a085e-1442">identyfikatora buildId</span><span class="sxs-lookup"><span data-stu-id="a085e-1442">buildId</span></span> |<span data-ttu-id="a085e-1443">Witaj kompilacji toouse identyfikator dla tego żądania zalecenia</span><span class="sxs-lookup"><span data-stu-id="a085e-1443">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="a085e-1444">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1444">apiVersion</span></span> |<span data-ttu-id="a085e-1445">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1445">1.0</span></span> |

<span data-ttu-id="a085e-1446">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="a085e-1446">**Response:**</span></span>

<span data-ttu-id="a085e-1447">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1447">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-1448">odpowiedź Hello zawiera jeden wpis dla każdego elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1448">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="a085e-1449">Każdy wpis ma hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="a085e-1449">Each entry has hello following data:</span></span>

* <span data-ttu-id="a085e-1450">`Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a085e-1451">`Feed\entry\content\properties\Name`-Nazwa elementu hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1451">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="a085e-1452">`Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.</span><span class="sxs-lookup"><span data-stu-id="a085e-1452">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a085e-1453">`Feed\entry\content\properties\Reasoning`-Zalecenie wnioskowania (np. zalecenie wyjaśnienia).</span><span class="sxs-lookup"><span data-stu-id="a085e-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a085e-1454">Zobacz przykład odpowiedzi, 12.1</span><span class="sxs-lookup"><span data-stu-id="a085e-1454">See a response example in 12.1</span></span>

### <a name="123-get-fbt-recommendations-for-active-build"></a><span data-ttu-id="a085e-1455">12.3.</span><span class="sxs-lookup"><span data-stu-id="a085e-1455">12.3.</span></span> <span data-ttu-id="a085e-1456">Pobierz zalecenia zmianie wysokości progów (dla active kompilacji)</span><span class="sxs-lookup"><span data-stu-id="a085e-1456">Get FBT Recommendations (for active build)</span></span>
<span data-ttu-id="a085e-1457">Pobierz zalecenia hello active kompilacji typu "Zmianie wysokości progów" oparta na elemencie inicjatora (dane wejściowe).</span><span class="sxs-lookup"><span data-stu-id="a085e-1457">Get recommendations of hello active build of type "Fbt" based on a seed (input) item.</span></span>

| <span data-ttu-id="a085e-1458">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1458">HTTP Method</span></span> | <span data-ttu-id="a085e-1459">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1459">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1460">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1460">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1461">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-1461">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-1462">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1462">Parameter Name</span></span> | <span data-ttu-id="a085e-1463">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1463">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1464">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-1464">modelId</span></span> |<span data-ttu-id="a085e-1465">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-1465">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-1466">Identyfikator elementu</span><span class="sxs-lookup"><span data-stu-id="a085e-1466">itemId</span></span> |<span data-ttu-id="a085e-1467">Element toorecommend dla.</span><span class="sxs-lookup"><span data-stu-id="a085e-1467">Item toorecommend for.</span></span> <br><span data-ttu-id="a085e-1468">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="a085e-1468">Max length: 1024</span></span> |
| <span data-ttu-id="a085e-1469">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a085e-1469">numberOfResults</span></span> |<span data-ttu-id="a085e-1470">Liczba wymaganych wyników</span><span class="sxs-lookup"><span data-stu-id="a085e-1470">Number of required results</span></span> <br><span data-ttu-id="a085e-1471">Maksymalna liczba: 150</span><span class="sxs-lookup"><span data-stu-id="a085e-1471">Max: 150</span></span> |
| <span data-ttu-id="a085e-1472">minimalScore</span><span class="sxs-lookup"><span data-stu-id="a085e-1472">minimalScore</span></span> |<span data-ttu-id="a085e-1473">Wynik minimalnego częste zestaw powinny mieć w kolejności toobe objęte hello zwrócone wyniki</span><span class="sxs-lookup"><span data-stu-id="a085e-1473">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="a085e-1474">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a085e-1474">includeMetatadata</span></span> |<span data-ttu-id="a085e-1475">Użycia w przyszłości, zawsze false</span><span class="sxs-lookup"><span data-stu-id="a085e-1475">Future use, always false</span></span> |
| <span data-ttu-id="a085e-1476">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1476">apiVersion</span></span> |<span data-ttu-id="a085e-1477">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1477">1.0</span></span> |

<span data-ttu-id="a085e-1478">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="a085e-1478">**Response:**</span></span>

<span data-ttu-id="a085e-1479">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1479">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-1480">odpowiedź Hello zawiera jeden wpis dla danego zestawu elementu zalecane (zestaw elementów, które zwykle są kupowane wraz z elementu seed/input hello).</span><span class="sxs-lookup"><span data-stu-id="a085e-1480">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="a085e-1481">Każdy wpis ma hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="a085e-1481">Each entry has hello following data:</span></span>

* <span data-ttu-id="a085e-1482">`Feed\entry\content\properties\Id1`— Identyfikator elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="a085e-1483">`Feed\entry\content\properties\Name1`-Nazwa elementu hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1483">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="a085e-1484">`Feed\entry\content\properties\Id2`Identyfikator elementu zalecane - 2 (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="a085e-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="a085e-1485">`Feed\entry\content\properties\Name2`-Nazwa elementu hello 2 (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="a085e-1485">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="a085e-1486">`Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.</span><span class="sxs-lookup"><span data-stu-id="a085e-1486">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a085e-1487">`Feed\entry\content\properties\Reasoning`-Zalecenie wnioskowania (np. zalecenie wyjaśnienia).</span><span class="sxs-lookup"><span data-stu-id="a085e-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a085e-1488">przykład odpowiedzi Hello poniżej zawiera 3 zestawy zalecane elementu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1488">hello example response below includes 3 recommended item sets.</span></span>

<span data-ttu-id="a085e-1489">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-1489">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a><span data-ttu-id="a085e-1490">12.4.</span><span class="sxs-lookup"><span data-stu-id="a085e-1490">12.4.</span></span> <span data-ttu-id="a085e-1491">Pobierz zmianie wysokości progów zalecenia (określonej kompilacji)</span><span class="sxs-lookup"><span data-stu-id="a085e-1491">Get FBT Recommendations (of a specific build)</span></span>
<span data-ttu-id="a085e-1492">Pobierz zalecenia określonej kompilacji typu "Zmianie wysokości progów".</span><span class="sxs-lookup"><span data-stu-id="a085e-1492">Get recommendations of a specific build of type "Fbt".</span></span>

| <span data-ttu-id="a085e-1493">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1493">HTTP Method</span></span> | <span data-ttu-id="a085e-1494">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1495">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1495">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1496">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-1496">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-1497">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1497">Parameter Name</span></span> | <span data-ttu-id="a085e-1498">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1499">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-1499">modelId</span></span> |<span data-ttu-id="a085e-1500">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-1500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-1501">Identyfikator elementu</span><span class="sxs-lookup"><span data-stu-id="a085e-1501">itemId</span></span> |<span data-ttu-id="a085e-1502">Element toorecommend dla.</span><span class="sxs-lookup"><span data-stu-id="a085e-1502">Item toorecommend for.</span></span> <br><span data-ttu-id="a085e-1503">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="a085e-1503">Max length: 1024</span></span> |
| <span data-ttu-id="a085e-1504">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a085e-1504">numberOfResults</span></span> |<span data-ttu-id="a085e-1505">Liczba wymaganych wyników</span><span class="sxs-lookup"><span data-stu-id="a085e-1505">Number of required results</span></span> <br><span data-ttu-id="a085e-1506">Maksymalna liczba: 150</span><span class="sxs-lookup"><span data-stu-id="a085e-1506">Max: 150</span></span> |
| <span data-ttu-id="a085e-1507">minimalScore</span><span class="sxs-lookup"><span data-stu-id="a085e-1507">minimalScore</span></span> |<span data-ttu-id="a085e-1508">Wynik minimalnego częste zestaw powinny mieć w kolejności toobe objęte hello zwrócone wyniki</span><span class="sxs-lookup"><span data-stu-id="a085e-1508">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="a085e-1509">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a085e-1509">includeMetatadata</span></span> |<span data-ttu-id="a085e-1510">Użycia w przyszłości, zawsze false</span><span class="sxs-lookup"><span data-stu-id="a085e-1510">Future use, always false</span></span> |
| <span data-ttu-id="a085e-1511">identyfikatora buildId</span><span class="sxs-lookup"><span data-stu-id="a085e-1511">buildId</span></span> |<span data-ttu-id="a085e-1512">Witaj kompilacji toouse identyfikator dla tego żądania zalecenia</span><span class="sxs-lookup"><span data-stu-id="a085e-1512">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="a085e-1513">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1513">apiVersion</span></span> |<span data-ttu-id="a085e-1514">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1514">1.0</span></span> |

<span data-ttu-id="a085e-1515">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="a085e-1515">**Response:**</span></span>

<span data-ttu-id="a085e-1516">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1516">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-1517">odpowiedź Hello zawiera jeden wpis dla danego zestawu elementu zalecane (zestaw elementów, które zwykle są kupowane wraz z elementu seed/input hello).</span><span class="sxs-lookup"><span data-stu-id="a085e-1517">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="a085e-1518">Każdy wpis ma hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="a085e-1518">Each entry has hello following data:</span></span>

* <span data-ttu-id="a085e-1519">`Feed\entry\content\properties\Id1`— Identyfikator elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="a085e-1520">`Feed\entry\content\properties\Name1`-Nazwa elementu hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1520">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="a085e-1521">`Feed\entry\content\properties\Id2`Identyfikator elementu zalecane - 2 (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="a085e-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="a085e-1522">`Feed\entry\content\properties\Name2`-Nazwa elementu hello 2 (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="a085e-1522">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="a085e-1523">`Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.</span><span class="sxs-lookup"><span data-stu-id="a085e-1523">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a085e-1524">`Feed\entry\content\properties\Reasoning`-Zalecenie wnioskowania (np. zalecenie wyjaśnienia).</span><span class="sxs-lookup"><span data-stu-id="a085e-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a085e-1525">Zobacz przykład odpowiedzi, w 12.3</span><span class="sxs-lookup"><span data-stu-id="a085e-1525">See a response example in 12.3</span></span>

### <a name="125-get-user-recommendations-for-active-build"></a><span data-ttu-id="a085e-1526">12.5.</span><span class="sxs-lookup"><span data-stu-id="a085e-1526">12.5.</span></span> <span data-ttu-id="a085e-1527">Pobierz zalecenia użytkownika (dla active kompilacji)</span><span class="sxs-lookup"><span data-stu-id="a085e-1527">Get User Recommendations (for active build)</span></span>
<span data-ttu-id="a085e-1528">Pobierz zalecenia użytkownika kompilacji typu "Recommendation" oznaczona jako aktywny kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span></span>

<span data-ttu-id="a085e-1529">Witaj interfejsu API zwróci listę przewidywane elementu zgodnie z historii użycia toohello hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a085e-1529">hello API will return a list of predicted item according toohello usage history of hello user.</span></span>

<span data-ttu-id="a085e-1530">Uwagi:</span><span class="sxs-lookup"><span data-stu-id="a085e-1530">Notes:</span></span> 

1. <span data-ttu-id="a085e-1531">Nie ma żadnych zalecenie użytkownika dla kompilacji zmianie wysokości progów.</span><span class="sxs-lookup"><span data-stu-id="a085e-1531">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="a085e-1532">Jeśli hello active kompilacji jest zmianie wysokości progów będą ta metoda zwraca błąd.</span><span class="sxs-lookup"><span data-stu-id="a085e-1532">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="a085e-1533">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1533">HTTP Method</span></span> | <span data-ttu-id="a085e-1534">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1534">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1535">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1535">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1536">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-1536">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-1537">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1537">Parameter Name</span></span> | <span data-ttu-id="a085e-1538">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1538">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1539">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-1539">modelId</span></span> |<span data-ttu-id="a085e-1540">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-1540">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-1541">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="a085e-1541">userId</span></span> |<span data-ttu-id="a085e-1542">Unikatowy identyfikator użytkownika hello</span><span class="sxs-lookup"><span data-stu-id="a085e-1542">Unique identifier of hello user</span></span> |
| <span data-ttu-id="a085e-1543">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a085e-1543">numberOfResults</span></span> |<span data-ttu-id="a085e-1544">Liczba wymaganych wyników</span><span class="sxs-lookup"><span data-stu-id="a085e-1544">Number of required results</span></span> |
| <span data-ttu-id="a085e-1545">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a085e-1545">includeMetatadata</span></span> |<span data-ttu-id="a085e-1546">Użycia w przyszłości, zawsze false</span><span class="sxs-lookup"><span data-stu-id="a085e-1546">Future use, always false</span></span> |
| <span data-ttu-id="a085e-1547">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1547">apiVersion</span></span> |<span data-ttu-id="a085e-1548">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1548">1.0</span></span> |

<span data-ttu-id="a085e-1549">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="a085e-1549">**Response:**</span></span>

<span data-ttu-id="a085e-1550">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1550">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-1551">odpowiedź Hello zawiera jeden wpis dla każdego elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1551">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="a085e-1552">Każdy wpis ma hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="a085e-1552">Each entry has hello following data:</span></span>

* <span data-ttu-id="a085e-1553">`Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a085e-1554">`Feed\entry\content\properties\Name`-Nazwa elementu hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1554">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="a085e-1555">`Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.</span><span class="sxs-lookup"><span data-stu-id="a085e-1555">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a085e-1556">`Feed\entry\content\properties\Reasoning`-Zalecenie wnioskowania (np. zalecenie wyjaśnienia).</span><span class="sxs-lookup"><span data-stu-id="a085e-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a085e-1557">Zobacz przykład odpowiedzi, 12.1</span><span class="sxs-lookup"><span data-stu-id="a085e-1557">See a response example in 12.1</span></span>

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a><span data-ttu-id="a085e-1558">12.6.</span><span class="sxs-lookup"><span data-stu-id="a085e-1558">12.6.</span></span> <span data-ttu-id="a085e-1559">Pobierz zalecenia dotyczące użytkownika z listy elementów (dla active kompilacji)</span><span class="sxs-lookup"><span data-stu-id="a085e-1559">Get User Recommendations with item list (for active build)</span></span>
<span data-ttu-id="a085e-1560">Uzyskaj zalecenia użytkownika kompilacji typu "Recommendation" oznaczona jako aktywny kompilacji z dodatkowych listy elementów</span><span class="sxs-lookup"><span data-stu-id="a085e-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span></span>

<span data-ttu-id="a085e-1561">Hello interfejsu API zwróci listę przewidywane elementu zgodnie z historii użycia toohello hello użytkownika i hello dodatkowe podane elementy.</span><span class="sxs-lookup"><span data-stu-id="a085e-1561">hello API will return a list of predicted item according toohello usage history of hello user and hello additional provided items.</span></span>

<span data-ttu-id="a085e-1562">Uwagi:</span><span class="sxs-lookup"><span data-stu-id="a085e-1562">Notes:</span></span> 

1. <span data-ttu-id="a085e-1563">Nie ma żadnych zalecenie użytkownika dla kompilacji zmianie wysokości progów.</span><span class="sxs-lookup"><span data-stu-id="a085e-1563">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="a085e-1564">Jeśli hello active kompilacji jest zmianie wysokości progów będą ta metoda zwraca błąd.</span><span class="sxs-lookup"><span data-stu-id="a085e-1564">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="a085e-1565">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1565">HTTP Method</span></span> | <span data-ttu-id="a085e-1566">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1566">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1567">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1567">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1568">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-1568">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-1569">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1569">Parameter Name</span></span> | <span data-ttu-id="a085e-1570">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1570">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1571">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-1571">modelId</span></span> |<span data-ttu-id="a085e-1572">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-1572">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-1573">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="a085e-1573">userId</span></span> |<span data-ttu-id="a085e-1574">Unikatowy identyfikator użytkownika hello</span><span class="sxs-lookup"><span data-stu-id="a085e-1574">Unique identifier of hello user</span></span> |
| <span data-ttu-id="a085e-1575">itemsIds</span><span class="sxs-lookup"><span data-stu-id="a085e-1575">itemsIds</span></span> |<span data-ttu-id="a085e-1576">Rozdzielana przecinkami lista hello elementów toorecommend dla.</span><span class="sxs-lookup"><span data-stu-id="a085e-1576">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="a085e-1577">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="a085e-1577">Max length: 1024</span></span> |
| <span data-ttu-id="a085e-1578">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a085e-1578">numberOfResults</span></span> |<span data-ttu-id="a085e-1579">Liczba wymaganych wyników</span><span class="sxs-lookup"><span data-stu-id="a085e-1579">Number of required results</span></span> |
| <span data-ttu-id="a085e-1580">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a085e-1580">includeMetatadata</span></span> |<span data-ttu-id="a085e-1581">Użycia w przyszłości, zawsze false</span><span class="sxs-lookup"><span data-stu-id="a085e-1581">Future use, always false</span></span> |
| <span data-ttu-id="a085e-1582">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1582">apiVersion</span></span> |<span data-ttu-id="a085e-1583">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1583">1.0</span></span> |

<span data-ttu-id="a085e-1584">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="a085e-1584">**Response:**</span></span>

<span data-ttu-id="a085e-1585">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1585">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-1586">odpowiedź Hello zawiera jeden wpis dla każdego elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1586">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="a085e-1587">Każdy wpis ma hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="a085e-1587">Each entry has hello following data:</span></span>

* <span data-ttu-id="a085e-1588">`Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a085e-1589">`Feed\entry\content\properties\Name`-Nazwa elementu hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1589">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="a085e-1590">`Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.</span><span class="sxs-lookup"><span data-stu-id="a085e-1590">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a085e-1591">`Feed\entry\content\properties\Reasoning`-Zalecenie wnioskowania (np. zalecenie wyjaśnienia).</span><span class="sxs-lookup"><span data-stu-id="a085e-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a085e-1592">Zobacz przykład odpowiedzi, 12.1</span><span class="sxs-lookup"><span data-stu-id="a085e-1592">See a response example in 12.1</span></span>

### <a name="127-get-user-recommendations--of-a-specific-build"></a><span data-ttu-id="a085e-1593">12.7.</span><span class="sxs-lookup"><span data-stu-id="a085e-1593">12.7.</span></span> <span data-ttu-id="a085e-1594">Uzyskaj zalecenia użytkownika (od określonej kompilacji)</span><span class="sxs-lookup"><span data-stu-id="a085e-1594">Get User Recommendations  (of a specific build)</span></span>
<span data-ttu-id="a085e-1595">Pobierz zalecenia użytkownika określonej kompilacji typu "Recommendation".</span><span class="sxs-lookup"><span data-stu-id="a085e-1595">Get user recommendations of a specific build of type "Recommendation".</span></span>

<span data-ttu-id="a085e-1596">Witaj interfejsu API zwróci listę przewidywane elementu zgodnie z historii użycia toohello hello użytkownika (używane w określonej kompilacji hello).</span><span class="sxs-lookup"><span data-stu-id="a085e-1596">hello API will return a list of predicted item according toohello usage history of hello user (used in hello specific build).</span></span>

<span data-ttu-id="a085e-1597">Uwaga: Jest Brak rekomendacji użytkownika dla kompilacji zmianie wysokości progów.</span><span class="sxs-lookup"><span data-stu-id="a085e-1597">Note: There is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="a085e-1598">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1598">HTTP Method</span></span> | <span data-ttu-id="a085e-1599">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1599">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1600">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1600">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1601">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-1601">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-1602">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1602">Parameter Name</span></span> | <span data-ttu-id="a085e-1603">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1603">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1604">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-1604">modelId</span></span> |<span data-ttu-id="a085e-1605">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-1605">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-1606">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="a085e-1606">userId</span></span> |<span data-ttu-id="a085e-1607">Unikatowy identyfikator użytkownika hello</span><span class="sxs-lookup"><span data-stu-id="a085e-1607">Unique identifier of hello user</span></span> |
| <span data-ttu-id="a085e-1608">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a085e-1608">numberOfResults</span></span> |<span data-ttu-id="a085e-1609">Liczba wymaganych wyników</span><span class="sxs-lookup"><span data-stu-id="a085e-1609">Number of required results</span></span> |
| <span data-ttu-id="a085e-1610">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a085e-1610">includeMetatadata</span></span> |<span data-ttu-id="a085e-1611">Użycia w przyszłości, zawsze false</span><span class="sxs-lookup"><span data-stu-id="a085e-1611">Future use, always false</span></span> |
| <span data-ttu-id="a085e-1612">identyfikatora buildId</span><span class="sxs-lookup"><span data-stu-id="a085e-1612">buildId</span></span> |<span data-ttu-id="a085e-1613">Witaj kompilacji toouse identyfikator dla tego żądania zalecenia</span><span class="sxs-lookup"><span data-stu-id="a085e-1613">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="a085e-1614">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1614">apiVersion</span></span> |<span data-ttu-id="a085e-1615">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1615">1.0</span></span> |

<span data-ttu-id="a085e-1616">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="a085e-1616">**Response:**</span></span>

<span data-ttu-id="a085e-1617">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1617">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-1618">odpowiedź Hello zawiera jeden wpis dla każdego elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1618">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="a085e-1619">Każdy wpis ma hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="a085e-1619">Each entry has hello following data:</span></span>

* <span data-ttu-id="a085e-1620">`Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a085e-1621">`Feed\entry\content\properties\Name`-Nazwa elementu hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1621">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="a085e-1622">`Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.</span><span class="sxs-lookup"><span data-stu-id="a085e-1622">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a085e-1623">`Feed\entry\content\properties\Reasoning`-Zalecenie wnioskowania (np. zalecenie wyjaśnienia).</span><span class="sxs-lookup"><span data-stu-id="a085e-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a085e-1624">Zobacz przykład odpowiedzi, 12.1</span><span class="sxs-lookup"><span data-stu-id="a085e-1624">See a response example in 12.1</span></span>

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a><span data-ttu-id="a085e-1625">12.8.</span><span class="sxs-lookup"><span data-stu-id="a085e-1625">12.8.</span></span> <span data-ttu-id="a085e-1626">Uzyskaj zalecenia użytkownika z listy elementów (o określonej kompilacji)</span><span class="sxs-lookup"><span data-stu-id="a085e-1626">Get User Recommendations with item list (of a specific build)</span></span>
<span data-ttu-id="a085e-1627">Pobierz zalecenia użytkownika określonej kompilacji typu "Recommendation" i hello listę dodatkowych elementów.</span><span class="sxs-lookup"><span data-stu-id="a085e-1627">Get user recommendations of a specific build of type "Recommendation" and hello list of additional items.</span></span>

<span data-ttu-id="a085e-1628">Hello interfejsu API zwróci listę przewidywane elementu zgodnie z historii użycia toohello hello użytkownika i hello dodatkowe listy elementów.</span><span class="sxs-lookup"><span data-stu-id="a085e-1628">hello API will return a list of predicted item according toohello usage history of hello user and hello additional list of items.</span></span>

<span data-ttu-id="a085e-1629">Uwaga: Tthere jest Brak rekomendacji użytkownika dla kompilacji zmianie wysokości progów.</span><span class="sxs-lookup"><span data-stu-id="a085e-1629">Note: Tthere is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="a085e-1630">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1630">HTTP Method</span></span> | <span data-ttu-id="a085e-1631">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1631">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1632">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1632">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1633">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-1633">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-1634">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1634">Parameter Name</span></span> | <span data-ttu-id="a085e-1635">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1635">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1636">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-1636">modelId</span></span> |<span data-ttu-id="a085e-1637">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-1637">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-1638">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="a085e-1638">userId</span></span> |<span data-ttu-id="a085e-1639">Unikatowy identyfikator użytkownika hello</span><span class="sxs-lookup"><span data-stu-id="a085e-1639">Unique identifier of hello user</span></span> |
| <span data-ttu-id="a085e-1640">identyfikatory elementów</span><span class="sxs-lookup"><span data-stu-id="a085e-1640">itemIds</span></span> |<span data-ttu-id="a085e-1641">Rozdzielana przecinkami lista hello elementów toorecommend dla.</span><span class="sxs-lookup"><span data-stu-id="a085e-1641">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="a085e-1642">Maksymalna długość: 1024</span><span class="sxs-lookup"><span data-stu-id="a085e-1642">Max length: 1024</span></span> |
| <span data-ttu-id="a085e-1643">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="a085e-1643">numberOfResults</span></span> |<span data-ttu-id="a085e-1644">Liczba wymaganych wyników</span><span class="sxs-lookup"><span data-stu-id="a085e-1644">Number of required results</span></span> |
| <span data-ttu-id="a085e-1645">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="a085e-1645">includeMetatadata</span></span> |<span data-ttu-id="a085e-1646">Użycia w przyszłości, zawsze false</span><span class="sxs-lookup"><span data-stu-id="a085e-1646">Future use, always false</span></span> |
| <span data-ttu-id="a085e-1647">identyfikatora buildId</span><span class="sxs-lookup"><span data-stu-id="a085e-1647">buildId</span></span> |<span data-ttu-id="a085e-1648">Witaj kompilacji toouse identyfikator dla tego żądania zalecenia</span><span class="sxs-lookup"><span data-stu-id="a085e-1648">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="a085e-1649">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1649">apiVersion</span></span> |<span data-ttu-id="a085e-1650">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1650">1.0</span></span> |

<span data-ttu-id="a085e-1651">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="a085e-1651">**Response:**</span></span>

<span data-ttu-id="a085e-1652">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1652">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-1653">odpowiedź Hello zawiera jeden wpis dla każdego elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1653">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="a085e-1654">Każdy wpis ma hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="a085e-1654">Each entry has hello following data:</span></span>

* <span data-ttu-id="a085e-1655">`Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a085e-1656">`Feed\entry\content\properties\Name`-Nazwa elementu hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1656">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="a085e-1657">`Feed\entry\content\properties\Rating`— Ocena zalecenia hello; większa liczba oznacza większą wiarą.</span><span class="sxs-lookup"><span data-stu-id="a085e-1657">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="a085e-1658">`Feed\entry\content\properties\Reasoning`-Zalecenie wnioskowania (np. zalecenie wyjaśnienia).</span><span class="sxs-lookup"><span data-stu-id="a085e-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="a085e-1659">Zobacz przykład odpowiedzi, 12.1</span><span class="sxs-lookup"><span data-stu-id="a085e-1659">See a response example in 12.1</span></span>

## <a name="13-user-usage-history"></a><span data-ttu-id="a085e-1660">13. Historia użycia użytkownika</span><span class="sxs-lookup"><span data-stu-id="a085e-1660">13. User Usage History</span></span>
<span data-ttu-id="a085e-1661">Po modelu zalecenie został utworzony hello system zezwoli używany dla kompilacji hello tooretrieve hello historię użytkownika (elementy skojarzone tooa określonego użytkownika).</span><span class="sxs-lookup"><span data-stu-id="a085e-1661">Once a recommendation model was built hello system will allow tooretrieve hello user history (items associated tooa specific user) used for hello build.</span></span>
<span data-ttu-id="a085e-1662">Ten interfejs API umożliwia tooretrieve hello użytkownika historii</span><span class="sxs-lookup"><span data-stu-id="a085e-1662">This API allow tooretrieve hello user history</span></span>

<span data-ttu-id="a085e-1663">Uwaga: hello historię użytkownika jest obecnie dostępny tylko dla kompilacji zalecenia.</span><span class="sxs-lookup"><span data-stu-id="a085e-1663">Note: hello user history is currently available only for recommendation builds.</span></span>

### <a name="131-retrieve-user-history"></a><span data-ttu-id="a085e-1664">13.1 pobrać historii użytkownika</span><span class="sxs-lookup"><span data-stu-id="a085e-1664">13.1 Retrieve user history</span></span>
<span data-ttu-id="a085e-1665">Pobieranie listy hello element używany w hello active kompilacji lub w hello określonej kompilacji dla hello podany identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a085e-1665">Retrieve hello list of item used in hello active build or in hello specified build for hello given user id.</span></span>

| <span data-ttu-id="a085e-1666">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1666">HTTP Method</span></span> | <span data-ttu-id="a085e-1667">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1667">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1668">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1668">GET</span></span> |<span data-ttu-id="a085e-1669">Pobierz historię użytkownika hello hello active kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1669">Get hello user history for hello active build.</span></span><br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/><span data-ttu-id="a085e-1670">Pobierz historię użytkownika hello dla hello podane kompilacji`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span><span class="sxs-lookup"><span data-stu-id="a085e-1670">Get hello user history for hello given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span></span><br/><br/><span data-ttu-id="a085e-1671">Przykład:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span><span class="sxs-lookup"><span data-stu-id="a085e-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span></span> |

| <span data-ttu-id="a085e-1672">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1672">Parameter Name</span></span> | <span data-ttu-id="a085e-1673">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1673">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1674">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-1674">modelId</span></span> |<span data-ttu-id="a085e-1675">Unikatowy identyfikator Hello hello modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1675">hello unique identifier of hello model.</span></span> |
| <span data-ttu-id="a085e-1676">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="a085e-1676">userId</span></span> |<span data-ttu-id="a085e-1677">Unikatowy identyfikator Hello hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a085e-1677">hello unique identifier of hello user.</span></span> |
| <span data-ttu-id="a085e-1678">identyfikatora buildId</span><span class="sxs-lookup"><span data-stu-id="a085e-1678">buildId</span></span> |<span data-ttu-id="a085e-1679">opcjonalny parametr Zezwalaj tooindicate, z których kompilacji hello historię użytkownika powinno być pobierania</span><span class="sxs-lookup"><span data-stu-id="a085e-1679">optional parameter, allow tooindicate from which build hello user history should be fetch</span></span> |
| <span data-ttu-id="a085e-1680">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1680">apiVersion</span></span> |<span data-ttu-id="a085e-1681">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1681">1.0</span></span> |

<span data-ttu-id="a085e-1682">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="a085e-1682">**Response:**</span></span>

<span data-ttu-id="a085e-1683">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1683">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-1684">odpowiedź Hello zawiera jeden wpis dla każdego elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1684">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="a085e-1685">Każdy wpis ma hello następujące dane:</span><span class="sxs-lookup"><span data-stu-id="a085e-1685">Each entry has hello following data:</span></span>

* <span data-ttu-id="a085e-1686">`Feed\entry\content\properties\Id`— Identyfikator elementu zalecane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="a085e-1687">`Feed\entry\content\properties\Name`-Nazwa elementu hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1687">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="a085e-1688">`Feed\entry\content\properties\Rating`-NIE DOTYCZY.</span><span class="sxs-lookup"><span data-stu-id="a085e-1688">`Feed\entry\content\properties\Rating` - N/A.</span></span>
* <span data-ttu-id="a085e-1689">`Feed\entry\content\properties\Reasoning`-NIE DOTYCZY.</span><span class="sxs-lookup"><span data-stu-id="a085e-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span></span>

<span data-ttu-id="a085e-1690">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-1690">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a><span data-ttu-id="a085e-1691">14. Powiadomienia</span><span class="sxs-lookup"><span data-stu-id="a085e-1691">14. Notifications</span></span>
<span data-ttu-id="a085e-1692">Azure Machine Learning zalecenia tworzy powiadomienia, gdy wystąpi trwałe błędów w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="a085e-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in hello system.</span></span> <span data-ttu-id="a085e-1693">Istnieją 3 typy powiadomień:</span><span class="sxs-lookup"><span data-stu-id="a085e-1693">There are 3 types of notifications:</span></span>

1. <span data-ttu-id="a085e-1694">Niepowodzenie kompilacji — to powiadomienie jest wyzwalany dla każdego błędu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a085e-1694">Build failure - This notification is triggered for every build failure.</span></span>
2. <span data-ttu-id="a085e-1695">Uzyskiwanie danych przetwarzania niepowodzenie — to powiadomienie jest wyzwalane, gdy będziemy mieć więcej niż 100 błędów w hello ostatnich 5 minut hello przetwarzania zdarzeń użycia dla modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of usage events per model.</span></span>
3. <span data-ttu-id="a085e-1696">Niepowodzenie zużycie zalecenie — to powiadomienie jest wyzwalane, gdy będziemy mieć więcej niż 100 błędów w hello ostatnich 5 minut hello przetwarzania żądań zalecenie na modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of recommendation requests per model.</span></span>

### <a name="141-get-notifications"></a><span data-ttu-id="a085e-1697">14.1.</span><span class="sxs-lookup"><span data-stu-id="a085e-1697">14.1.</span></span> <span data-ttu-id="a085e-1698">Otrzymywać powiadomień</span><span class="sxs-lookup"><span data-stu-id="a085e-1698">Get Notifications</span></span>
<span data-ttu-id="a085e-1699">Pobiera wszystkie hello powiadomienia dla wszystkich modeli lub dla pojedynczego modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1699">Retrieves all hello notifications for all models or for a single model.</span></span>

| <span data-ttu-id="a085e-1700">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1700">HTTP Method</span></span> | <span data-ttu-id="a085e-1701">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1701">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1702">POBIERZ</span><span class="sxs-lookup"><span data-stu-id="a085e-1702">GET</span></span> |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1703">Pobieranie wszystkich powiadomień dla wszystkich modeli:</span><span class="sxs-lookup"><span data-stu-id="a085e-1703">Getting all notifications for all models:</span></span><br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1704">Przykład uzyskiwanie powiadomień dla określonego modelu:</span><span class="sxs-lookup"><span data-stu-id="a085e-1704">Example for getting notifications for a specific model:</span></span><br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| <span data-ttu-id="a085e-1705">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1705">Parameter Name</span></span> | <span data-ttu-id="a085e-1706">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1706">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1707">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-1707">modelId</span></span> |<span data-ttu-id="a085e-1708">Parametr opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="a085e-1708">Optional parameter.</span></span> <span data-ttu-id="a085e-1709">Gdy pominięty, będą wyświetlane wszystkie powiadomienia dla wszystkich modeli.</span><span class="sxs-lookup"><span data-stu-id="a085e-1709">When omitted, you will get all notifications for all models.</span></span> <br><span data-ttu-id="a085e-1710">Prawidłowe wartości: Unikatowy identyfikator hello modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1710">Valid value: unique identifier of hello model.</span></span> |
| <span data-ttu-id="a085e-1711">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1711">apiVersion</span></span> |<span data-ttu-id="a085e-1712">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1712">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-1713">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-1713">Request Body</span></span> |<span data-ttu-id="a085e-1714">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-1714">NONE</span></span> |

<span data-ttu-id="a085e-1715">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="a085e-1715">**Response:**</span></span>

<span data-ttu-id="a085e-1716">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1716">HTTP Status code: 200</span></span>

<span data-ttu-id="a085e-1717">OData XML</span><span class="sxs-lookup"><span data-stu-id="a085e-1717">OData XML</span></span>

    hello response includes one entry per notification. Each entry has hello following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a><span data-ttu-id="a085e-1718">14.2.</span><span class="sxs-lookup"><span data-stu-id="a085e-1718">14.2.</span></span> <span data-ttu-id="a085e-1719">Usuwanie modelu powiadomień</span><span class="sxs-lookup"><span data-stu-id="a085e-1719">Delete Model Notifications</span></span>
<span data-ttu-id="a085e-1720">Usuwa wszystkie odczytu powiadomienia dla modelu.</span><span class="sxs-lookup"><span data-stu-id="a085e-1720">Deletes all read notifications for a model.</span></span>

| <span data-ttu-id="a085e-1721">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1721">HTTP Method</span></span> | <span data-ttu-id="a085e-1722">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1722">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1723">USUŃ</span><span class="sxs-lookup"><span data-stu-id="a085e-1723">DELETE</span></span> |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="a085e-1724">Przykład:</span><span class="sxs-lookup"><span data-stu-id="a085e-1724">Example:</span></span><br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-1725">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1725">Parameter Name</span></span> | <span data-ttu-id="a085e-1726">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1726">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1727">modelId</span><span class="sxs-lookup"><span data-stu-id="a085e-1727">modelId</span></span> |<span data-ttu-id="a085e-1728">Unikatowy identyfikator modelu hello</span><span class="sxs-lookup"><span data-stu-id="a085e-1728">Unique identifier of hello model</span></span> |
| <span data-ttu-id="a085e-1729">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1729">apiVersion</span></span> |<span data-ttu-id="a085e-1730">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1730">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-1731">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-1731">Request Body</span></span> |<span data-ttu-id="a085e-1732">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-1732">NONE</span></span> |

<span data-ttu-id="a085e-1733">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-1733">**Response**:</span></span>

<span data-ttu-id="a085e-1734">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1734">HTTP Status code: 200</span></span>

### <a name="143-delete-user-notifications"></a><span data-ttu-id="a085e-1735">14.3.</span><span class="sxs-lookup"><span data-stu-id="a085e-1735">14.3.</span></span> <span data-ttu-id="a085e-1736">Usunięcie powiadomienia użytkownika</span><span class="sxs-lookup"><span data-stu-id="a085e-1736">Delete User Notifications</span></span>
<span data-ttu-id="a085e-1737">Usuwa wszystkie powiadomienia dla wszystkich modeli.</span><span class="sxs-lookup"><span data-stu-id="a085e-1737">Deletes all notifications for all models.</span></span>

| <span data-ttu-id="a085e-1738">Metoda HTTP</span><span class="sxs-lookup"><span data-stu-id="a085e-1738">HTTP Method</span></span> | <span data-ttu-id="a085e-1739">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="a085e-1739">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1740">USUŃ</span><span class="sxs-lookup"><span data-stu-id="a085e-1740">DELETE</span></span> |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| <span data-ttu-id="a085e-1741">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="a085e-1741">Parameter Name</span></span> | <span data-ttu-id="a085e-1742">Prawidłowe wartości</span><span class="sxs-lookup"><span data-stu-id="a085e-1742">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="a085e-1743">apiVersion</span><span class="sxs-lookup"><span data-stu-id="a085e-1743">apiVersion</span></span> |<span data-ttu-id="a085e-1744">1.0</span><span class="sxs-lookup"><span data-stu-id="a085e-1744">1.0</span></span> |
|  | |
| <span data-ttu-id="a085e-1745">Treść żądania</span><span class="sxs-lookup"><span data-stu-id="a085e-1745">Request Body</span></span> |<span data-ttu-id="a085e-1746">BRAK</span><span class="sxs-lookup"><span data-stu-id="a085e-1746">NONE</span></span> |

<span data-ttu-id="a085e-1747">**Odpowiedź**:</span><span class="sxs-lookup"><span data-stu-id="a085e-1747">**Response**:</span></span>

<span data-ttu-id="a085e-1748">Kod stanu HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="a085e-1748">HTTP Status code: 200</span></span>

## <a name="15-legal"></a><span data-ttu-id="a085e-1749">15. Informacje prawne</span><span class="sxs-lookup"><span data-stu-id="a085e-1749">15. Legal</span></span>
<span data-ttu-id="a085e-1750">Niniejszy dokument jest udostępniany "jako — jest".</span><span class="sxs-lookup"><span data-stu-id="a085e-1750">This document is provided “as-is”.</span></span> <span data-ttu-id="a085e-1751">Informacje i poglądy wyrażone w tym dokumencie, w tym adresy URL i inne odsyłacze do witryn internetowych, mogą ulec zmianie bez uprzedzenia.</span><span class="sxs-lookup"><span data-stu-id="a085e-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span><br><br>
<span data-ttu-id="a085e-1752">Niektóre przedstawione przykłady są udostępniane tylko do celów ilustracyjnych i są fikcyjne.</span><span class="sxs-lookup"><span data-stu-id="a085e-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="a085e-1753">Żadne rzeczywiste skojarzenia ani połączenia jest przeznaczony lub powinny być zakładane.</span><span class="sxs-lookup"><span data-stu-id="a085e-1753">No real association or connection is intended or should be inferred.</span></span><br><br>
<span data-ttu-id="a085e-1754">Ten dokument nie daje użytkownikowi żadnych praw tooany własności intelektualnej związanej z jakimkolwiek produktem firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a085e-1754">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="a085e-1755">Można kopiować i używać tego dokumentu do wewnętrznych celów referencyjnych.</span><span class="sxs-lookup"><span data-stu-id="a085e-1755">You may copy and use this document for your internal, reference purposes.</span></span><br><br>
<span data-ttu-id="a085e-1756">© 2015 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a085e-1756">© 2015 Microsoft.</span></span> <span data-ttu-id="a085e-1757">Wszelkie prawa zastrzeżone.</span><span class="sxs-lookup"><span data-stu-id="a085e-1757">All rights reserved.</span></span>

