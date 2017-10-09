---
title: "Azure CosmosDB: Jednostek na minutę (RU/m) żądania | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak koszt tooreduce przy użyciu żądania jednostki na minutę."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="eea52-103">Jednostki żądania na minutę w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="eea52-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="eea52-104">Azure DB rozwiązania Cosmos jest zaprojektowana toohelp osiągnięcia szybkie, przewidywalną wydajność i skalę bezproblemowo wraz z wzrostu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eea52-104">Azure Cosmos DB is designed toohelp you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="eea52-105">Można udostępnić przepływności w kontenerze DB rozwiązania Cosmos zarówno, na sekundę i szczegółowości na minutę (RU/m).</span><span class="sxs-lookup"><span data-stu-id="eea52-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="eea52-106">Hello udostępnionej przepływności na minutę szczegółowości jest używane toomanage nieoczekiwany największego obciążenia hello występujących w szczegółowości na sekundę.</span><span class="sxs-lookup"><span data-stu-id="eea52-106">hello provisioned throughput at per-minute granularity is used toomanage unexpected spikes in hello workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="eea52-107">Ten artykuł zawiera omówienie działania hello inicjowania obsługi administracyjnej jednostki żądań na minutę (RU/m).</span><span class="sxs-lookup"><span data-stu-id="eea52-107">This article provides an overview of how hello provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="eea52-108">Celem Hello pamiętać z inicjowaniem obsługi administracyjnej RU/m jest tooprovide przewidywalną wydajność wokół nieprzewidywalne potrzeb (zwłaszcza, jeśli potrzebujesz toorun analytics na dane operacyjne) i spiky obciążeń.</span><span class="sxs-lookup"><span data-stu-id="eea52-108">hello goal in mind with provisioning of RU/m is tooprovide a predictable performance around unpredictable needs (especially if you need toorun analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="eea52-109">Chcemy toohave naszym klientom korzystać więcej przepustowości hello, który udostępnia, można szybko skalować z bez obaw.</span><span class="sxs-lookup"><span data-stu-id="eea52-109">We want toohave our customers consume more hello throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="eea52-110">Po przeczytaniu tego artykułu, będą mogli tooanswer hello następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="eea52-110">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="eea52-111">Jak działa jednostkę żądań na minutę</span><span class="sxs-lookup"><span data-stu-id="eea52-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="eea52-112">Jaka jest różnica hello jednostki żądania na minutę i jednostki żądania na sekundę?</span><span class="sxs-lookup"><span data-stu-id="eea52-112">What is hello difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="eea52-113">Jak tooprovision RU/m?</span><span class="sxs-lookup"><span data-stu-id="eea52-113">How tooprovision RU/m?</span></span>
* <span data-ttu-id="eea52-114">W obszarze scenariusza są wziąć pod uwagę inicjowania obsługi administracyjnej jednostki żądania na minutę?</span><span class="sxs-lookup"><span data-stu-id="eea52-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="eea52-115">Jak toouse hello toooptimize metryki portalu Moje kosztów i wydajności?</span><span class="sxs-lookup"><span data-stu-id="eea52-115">How toouse hello portal metrics toooptimize my cost and performance?</span></span>
* <span data-ttu-id="eea52-116">Zdefiniuj typy żądań, jaką może wykorzystać budżet RU/m?</span><span class="sxs-lookup"><span data-stu-id="eea52-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="eea52-117">Inicjowanie obsługi administracyjnej jednostki żądania na minutę (RU/m)</span><span class="sxs-lookup"><span data-stu-id="eea52-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="eea52-118">Podczas obsługi administracyjnej bazy danych Azure rozwiązania Cosmos w drugiego stopnia szczegółowości hello (RU/s), możesz uzyskać hello gwarancji, że przy niskim opóźnieniem powiedzie się żądanie przepustowość sieci nie przekroczył pojemności hello udostępniane w ramach tego drugiego.</span><span class="sxs-lookup"><span data-stu-id="eea52-118">When you provision Azure Cosmos DB at hello second granularity (RU/s), you get hello guarantee that your request succeeds at a low latency if your throughput has not exceeded hello capacity provisioned within that second.</span></span> <span data-ttu-id="eea52-119">Z RU/m szczegółowości hello jest na minutę hello z hello gwarancji, że Twoje żądanie zakończy się pomyślnie w ciągu tej minuty.</span><span class="sxs-lookup"><span data-stu-id="eea52-119">With RU/m, hello granularity is at hello minute with hello guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="eea52-120">Porównaniu systemów toobursting możemy upewnij się, że otrzymasz wydajności hello jest atrybutem wartości prognozowanych i można zaplanować na nim.</span><span class="sxs-lookup"><span data-stu-id="eea52-120">Compared toobursting systems, we make sure that hello performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="eea52-121">sposób Hello na minutę inicjowania obsługi administracyjnej działania jest prosty:</span><span class="sxs-lookup"><span data-stu-id="eea52-121">hello way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="eea52-122">RU/m są rozliczane co godzinę i w dodatku tooRU/s.</span><span class="sxs-lookup"><span data-stu-id="eea52-122">RU/m is billed hourly and in addition tooRU/s.</span></span> <span data-ttu-id="eea52-123">Aby uzyskać więcej informacji, odwiedź stronę bazy danych Azure rozwiązania Cosmos [cennikiem](https://aka.ms/acdbpricing).</span><span class="sxs-lookup"><span data-stu-id="eea52-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="eea52-124">RU/m może być włączone na poziomie kolekcji.</span><span class="sxs-lookup"><span data-stu-id="eea52-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="eea52-125">Który może odbywać się za pośrednictwem hello zestawów SDK (Node.js, Java lub .net) lub za pośrednictwem portalu hello (również obejmować obciążeń bazy danych MongoDB interfejsu API)</span><span class="sxs-lookup"><span data-stu-id="eea52-125">That can be done through hello SDKs (Node.js, Java, or .Net) or through hello portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="eea52-126">Po włączeniu RU/m, dla każdego 100 RU/s alokacji również uzyskać 1 000 RU/m udostępniane (stosunek hello jest 10 x)</span><span class="sxs-lookup"><span data-stu-id="eea52-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (hello ratio is 10x)</span></span>
* <span data-ttu-id="eea52-127">W drugiej danej, jednostka żądania zużywa Twojej RU/m udostępniania tylko wtedy, gdy został przekroczony z na drugi udostępniania w ramach tego drugiego</span><span class="sxs-lookup"><span data-stu-id="eea52-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="eea52-128">Raz hello 60 sekund czasu (UTC) zakończenia, hello na minutę inicjowania obsługi administracyjnej jest uzupełniania</span><span class="sxs-lookup"><span data-stu-id="eea52-128">Once hello 60-second period (UTC) ends, hello per minute provisioning is refilled</span></span>
* <span data-ttu-id="eea52-129">RU/m można włączyć tylko w przypadku kolekcji z maksymalną inicjowania obsługi 5000 RU/s dla każdej partycji.</span><span class="sxs-lookup"><span data-stu-id="eea52-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="eea52-130">Jeśli skalować potrzeb przepływności i wysoki poziom obsługi na partycję, otrzyma komunikat ostrzegawczy</span><span class="sxs-lookup"><span data-stu-id="eea52-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="eea52-131">Poniżej jest konkretnym przykładzie, w którym klient może udostępnić 10kRU/s z 100kRU/m, zapisywanie 73% w koszt Inicjowanie obsługi szczytowego (w 50kRU na sekundę) za pośrednictwem okres 90 sekund na kolekcję, która ma 10 000 RU/s do 100 000 RU/m udostępniane:</span><span class="sxs-lookup"><span data-stu-id="eea52-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="eea52-132">1 sekundę: hello RU/m budżetu jest ustawiona na 100 000</span><span class="sxs-lookup"><span data-stu-id="eea52-132">1st second: hello RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="eea52-133">3 sekundy: podczas tej drugiej hello zużycie jednostki żądania zostało 11,010 RUs 1,010 RUs powyżej hello RU/s inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="eea52-133">3rd second: During that second hello consumption of Request Unit was 11,010 RUs, 1,010 RUs above hello RU/s provisioning.</span></span> <span data-ttu-id="eea52-134">W związku z tym 1,010 RUs odejmuje się z hello RU/m budżetu.</span><span class="sxs-lookup"><span data-stu-id="eea52-134">Therefore, 1,010 RUs are deducted from hello RU/m budget.</span></span> <span data-ttu-id="eea52-135">98,990 RUs są dostępne dla hello dalej sekund 57 hello budżetu RU/m</span><span class="sxs-lookup"><span data-stu-id="eea52-135">98,990 RUs are available for hello next 57 seconds in hello RU/m budget</span></span>
* <span data-ttu-id="eea52-136">29 sekundę: podczas tego drugiego wystąpiły duże kolekcji (> 4 x wyższe niż inicjowania obsługi na sekundę) i 46,920 RUs hello zużycia jednostki żądania.</span><span class="sxs-lookup"><span data-stu-id="eea52-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and hello consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="eea52-137">36,920 RUs odejmuje się od budżetu RU/m hello z 92,323 too55 RUs (28 sekunda), RUs 403 (29 sekundy)</span><span class="sxs-lookup"><span data-stu-id="eea52-137">36,920 RUs are deducted from hello RU/m budget that dropped from 92,323 RUs (28th second) too55,403 RUs (29th second)</span></span>
* <span data-ttu-id="eea52-138">drugie 61st: budżetu RU/m jest ustawiana too100, 000 RUs.</span><span class="sxs-lookup"><span data-stu-id="eea52-138">61st second: RU/m budget is set back too100,000 RUs.</span></span>
 
![Wykres przedstawiający zużycie hello i inicjowania obsługi bazy danych Azure rozwiązania Cosmos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="eea52-140">Określanie pojemność jednostki żądania przy użyciu RU/m</span><span class="sxs-lookup"><span data-stu-id="eea52-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="eea52-141">Podczas tworzenia kolekcji usługi Azure DB rozwiązania Cosmos, określ numer hello jednostek żądań na sekundę (RU na sekundę) mają zastrzeżone dla hello kolekcji.</span><span class="sxs-lookup"><span data-stu-id="eea52-141">When creating an Azure Cosmos DB collection, you specify hello number of request units per second (RU per second) you want reserved for hello collection.</span></span> <span data-ttu-id="eea52-142">Można również określić, czy RU tooadd na minutę.</span><span class="sxs-lookup"><span data-stu-id="eea52-142">You can also decide if you want tooadd RU per minute.</span></span> <span data-ttu-id="eea52-143">Można to zrobić za pośrednictwem portalu hello lub hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="eea52-143">This can be done through hello Portal or hello SDK.</span></span> 

### <a name="through-hello-portal"></a><span data-ttu-id="eea52-144">Za pomocą hello portalu</span><span class="sxs-lookup"><span data-stu-id="eea52-144">Through hello Portal</span></span>

<span data-ttu-id="eea52-145">Włączanie lub wyłączanie RU na minutę po prostu wymaga kliknięcia podczas inicjowania obsługi administracyjnej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="eea52-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![Zrzut ekranu przedstawiający sposób tooset RU/m w hello portalu Azure](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a><span data-ttu-id="eea52-147">Za pomocą hello zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="eea52-147">Through hello SDK</span></span>
<span data-ttu-id="eea52-148">Po pierwsze jest ważne toonote czy RU/m jest dostępna tylko dla następujących zestawów SDK hello:</span><span class="sxs-lookup"><span data-stu-id="eea52-148">First, this is important toonote that RU/m is only available for hello following SDKs:</span></span>

* <span data-ttu-id="eea52-149">.NET 1.14.0</span><span class="sxs-lookup"><span data-stu-id="eea52-149">.Net 1.14.0</span></span>
* <span data-ttu-id="eea52-150">Java 1.11.0</span><span class="sxs-lookup"><span data-stu-id="eea52-150">Java 1.11.0</span></span>
* <span data-ttu-id="eea52-151">Node.js 1.12.0</span><span class="sxs-lookup"><span data-stu-id="eea52-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="eea52-152">Python 2.2.0</span><span class="sxs-lookup"><span data-stu-id="eea52-152">Python 2.2.0</span></span>

<span data-ttu-id="eea52-153">Oto fragment kodu dotyczący tworzenia kolekcji z 3000 jednostki żądania na żądanie drugi i 30 000 jednostek na minutę przy użyciu zestawu .NET SDK hello:</span><span class="sxs-lookup"><span data-stu-id="eea52-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using hello .NET SDK:</span></span>

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

<span data-ttu-id="eea52-154">Oto fragment kodu do zmiany hello przepływność too5 kolekcji, 000 jednostek żądań na sekundę bez udostępniania RU na użyciu minuty hello zestawu .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="eea52-154">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second without provisioning RU per minute using hello .NET SDK:</span></span>

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a><span data-ttu-id="eea52-155">Dobra obejmował scenariusze</span><span class="sxs-lookup"><span data-stu-id="eea52-155">Good fit scenarios</span></span>

<span data-ttu-id="eea52-156">W tej sekcji firma Microsoft udostępnia przegląd scenariuszy, które są dobrze umożliwiających jednostek żądań na minutę.</span><span class="sxs-lookup"><span data-stu-id="eea52-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="eea52-157">**Tworzenie/testowanie środowiska:** dobrze.</span><span class="sxs-lookup"><span data-stu-id="eea52-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="eea52-158">Na etapie programowania hello w przypadku testowania aplikacji z różnych obciążeń RU/m zapewniają elastyczność hello na tym etapie.</span><span class="sxs-lookup"><span data-stu-id="eea52-158">During hello development stage, if you are testing your application with different workloads, RU/m can provide hello flexibility at this stage.</span></span> <span data-ttu-id="eea52-159">Podczas hello [emulatora](local-emulator.md) to doskonałe narzędzie wolnego tootest bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="eea52-159">While hello [emulator](local-emulator.md) is a great free tool tootest Azure Cosmos DB.</span></span> <span data-ttu-id="eea52-160">Jednak jeśli chcesz toostart w środowisku chmury, konieczne będzie dużą elastyczność przy RU/m do potrzeb wydajności ad hoc.</span><span class="sxs-lookup"><span data-stu-id="eea52-160">However if you want toostart in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="eea52-161">Zostanie poświęcić więcej czasu na tworzenie mniej niepokojącego o potrzebach wydajności na początku.</span><span class="sxs-lookup"><span data-stu-id="eea52-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="eea52-162">Zaleca się, począwszy od hello minimalna inicjowania obsługi RU/s i włączyć RU/m.</span><span class="sxs-lookup"><span data-stu-id="eea52-162">We recommend starting with hello minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="eea52-163">**Wymaga szczegółowości nieprzewidywalne, spiky, minuty:** dobrej dopasowania — oszczędności: 25 75%.</span><span class="sxs-lookup"><span data-stu-id="eea52-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="eea52-164">Zaobserwowano są duże korzyści z większości środowisk produkcyjnych i RU/m do tej grupy.</span><span class="sxs-lookup"><span data-stu-id="eea52-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="eea52-165">Jeśli masz obciążenie IoT, które ma kilka razy w ciągu jednej minuty, kolekcji, jeśli masz zapytań wykonywanych po systemu sprawia, że masa wstawić na powitania sama godzina, konieczne będzie dodatkowej pojemności dla potrzeb handeling spiky.</span><span class="sxs-lookup"><span data-stu-id="eea52-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at hello same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="eea52-166">Firma Microsoft zaleca optymalizacji zapotrzebowanie na zasoby, stosując nasze podejście krok po kroku poniżej.</span><span class="sxs-lookup"><span data-stu-id="eea52-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![Wykres przedstawiający zużycie żądania w szczegółowości 5 minut](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="eea52-168">*Rysunek - RU zużycie testu*</span><span class="sxs-lookup"><span data-stu-id="eea52-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="eea52-169">**Spokój umysłu:** dobrej dopasowania — oszczędności: 10-20%.</span><span class="sxs-lookup"><span data-stu-id="eea52-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="eea52-170">Czasami po prostu chcesz spokój toohave i nie martw się o potencjalnych pików i ograniczania przepustowości.</span><span class="sxs-lookup"><span data-stu-id="eea52-170">Sometimes, you just want toohave peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="eea52-171">Ta funkcja jest hello odpowiedniej jeden dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="eea52-171">This feature is hello right one for you.</span></span> <span data-ttu-id="eea52-172">W takim przypadku zaleca się włączenie RU/m i nieco niższy użytkownika na drugim inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="eea52-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="eea52-173">Przypadek różni się od hello powyżej, ponieważ użytkownik nie będzie podejmował toooptimize agresywnie programu obsługi.</span><span class="sxs-lookup"><span data-stu-id="eea52-173">This case is different from hello above as you will not try toooptimize aggressively your provisioning.</span></span> <span data-ttu-id="eea52-174">Jest to jeden mindset "Zero ograniczania", które znajdują się w.</span><span class="sxs-lookup"><span data-stu-id="eea52-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="eea52-175">Ważne operacje o potrzebach ad hoc: Firma Microsoft zaleca czasami tooonly let ważne operacje dostępu RU/m budżetu, dlatego nie pobrać budżetu hello korzystanie przez ad hoc lub mniej ważne operacje.</span><span class="sxs-lookup"><span data-stu-id="eea52-175">Critical operations with adhoc needs: We sometimes recommend tooonly let critical operations access RU/m budget so hello budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="eea52-176">Który można łatwo zdefiniować w sekcji hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="eea52-176">That can be easily defined in hello section below.</span></span>

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a><span data-ttu-id="eea52-177">Przy użyciu hello portalu metryki toooptimize kosztów i wydajności</span><span class="sxs-lookup"><span data-stu-id="eea52-177">Using hello portal metrics toooptimize cost and performance</span></span>

<span data-ttu-id="eea52-178">**W najbliższych tygodniach hello firma Microsoft będzie kontynuować rozwijanie hello zawartością wokół monitorowania toooptimize minuty zużycie RUs, przepustowość sieci musi.**</span><span class="sxs-lookup"><span data-stu-id="eea52-178">**In hello coming weeks, we will further develop hello content around monitoring RUs minute consumption toooptimize your throughput needs.**</span></span>

<span data-ttu-id="eea52-179">Za pomocą portalu metryki hello widać, jaka część regularne sekund RU zużywają i RU minut.</span><span class="sxs-lookup"><span data-stu-id="eea52-179">Through hello portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="eea52-180">Monitorowanie tych metryk powinny pomóc w optymalizacji programu obsługi.</span><span class="sxs-lookup"><span data-stu-id="eea52-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="eea52-181">Zalecane podejście krok po kroku na temat toouse RU/m tooyour korzyści.</span><span class="sxs-lookup"><span data-stu-id="eea52-181">We recommend a step by step approach on how toouse RU/m tooyour advantage.</span></span> <span data-ttu-id="eea52-182">Dla każdego kroku powinny mieć omówienie zużycia hello RU reprezentujący pełnego cyklu obciążenie (możliwe, godziny, dni lub nawet tygodnie) i uzyskiwanie szczegółowych informacji na powitania wykorzystania można udostępnić.</span><span class="sxs-lookup"><span data-stu-id="eea52-182">For each step, you should have an overview of hello RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on hello utilization of what you provision.</span></span>

<span data-ttu-id="eea52-183">zasada Hello za takie podejście jest toomake udostępniania przepływności jako zamknąć jako możliwych tooa inicjowania obsługi administracyjnej punktu, który jest zgodna z kryteriami wydajności poniżej.</span><span class="sxs-lookup"><span data-stu-id="eea52-183">hello principle behind this approach is toomake your throughput provisioning as close as possible tooa provisioning point that matches your performance criteria below.</span></span> 

![Wykres przedstawiający zużycie żądania w 5-minutowy szczegółowości](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="eea52-185">toounderstand hello optymalne inicjowania obsługi administracyjnej punktu dla obciążenia, należy toounderstand:</span><span class="sxs-lookup"><span data-stu-id="eea52-185">toounderstand hello optimal provisioning point for your workload, you need toounderstand:</span></span>

* <span data-ttu-id="eea52-186">Wzorce użycia: Brak, rzadko lub utrzymujących nagłego?</span><span class="sxs-lookup"><span data-stu-id="eea52-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="eea52-187">Mała liczba godzin (średnia x 2), średnich i dużych (> 10 x średniej) nagłego?</span><span class="sxs-lookup"><span data-stu-id="eea52-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="eea52-188">Procent żądań ograniczeniem przepustowości: czy można bezpiecznie mając z bitowego ograniczania przepustowości?</span><span class="sxs-lookup"><span data-stu-id="eea52-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="eea52-189">Jeśli tak, jak duże?</span><span class="sxs-lookup"><span data-stu-id="eea52-189">If so, by how much?</span></span> 

<span data-ttu-id="eea52-190">Po zidentyfikowaniu, jakie są cele, będzie tooget stanie bliżej toohello optymalną inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="eea52-190">Once you have identified what your goals are, you will be able tooget closer toohello optimal provisioning.</span></span>

<span data-ttu-id="eea52-191">tooassist, chcemy tooprovide ogólne wskazówki dotyczące sposobu toooptimize Twojego inicjowania obsługi na podstawie RU/m użycia.</span><span class="sxs-lookup"><span data-stu-id="eea52-191">tooassist you, we want tooprovide an overall guidance on how toooptimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="eea52-192">W tych wskazówkach nie ma zastosowania tooall rodzaju obciążenia, ale jest oparta na powitania wiedzy prywatnej wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="eea52-192">This guidance doesn’t apply tooall kind of workloads but is based on hello private preview knowledge.</span></span> <span data-ttu-id="eea52-193">Firma Microsoft może zmienić takie linii bazowych jak możemy Dowiedz się więcej:</span><span class="sxs-lookup"><span data-stu-id="eea52-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="eea52-194">RU/m % wykorzystania</span><span class="sxs-lookup"><span data-stu-id="eea52-194">RU/m % utilization</span></span>|<span data-ttu-id="eea52-195">Stopień wykorzystania RU/m</span><span class="sxs-lookup"><span data-stu-id="eea52-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="eea52-196">Zalecane akcje dotyczące inicjowania obsługi administracyjnej</span><span class="sxs-lookup"><span data-stu-id="eea52-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="eea52-197">0-1%</span><span class="sxs-lookup"><span data-stu-id="eea52-197">0-1%</span></span>|<span data-ttu-id="eea52-198">W obszarze wykorzystania</span><span class="sxs-lookup"><span data-stu-id="eea52-198">Under utilization</span></span>|<span data-ttu-id="eea52-199">Dolny więcej RU/m tooconsume RU/s</span><span class="sxs-lookup"><span data-stu-id="eea52-199">Lower RU/s tooconsume more RU/m</span></span>|
|<span data-ttu-id="eea52-200">1-10%</span><span class="sxs-lookup"><span data-stu-id="eea52-200">1-10%</span></span>|<span data-ttu-id="eea52-201">Użyj dobrej kondycji</span><span class="sxs-lookup"><span data-stu-id="eea52-201">Healthy use</span></span>|<span data-ttu-id="eea52-202">Zachowaj hello sam inicjowania obsługi administracyjnej poziom</span><span class="sxs-lookup"><span data-stu-id="eea52-202">Keep hello same provisioning level</span></span>|
|<span data-ttu-id="eea52-203">Powyżej 10%</span><span class="sxs-lookup"><span data-stu-id="eea52-203">Above 10%</span></span>|<span data-ttu-id="eea52-204">Przez użycie</span><span class="sxs-lookup"><span data-stu-id="eea52-204">Over utilization</span></span>|<span data-ttu-id="eea52-205">Zwiększ RU/s toorely mniej na RU/m</span><span class="sxs-lookup"><span data-stu-id="eea52-205">Increase RU/s toorely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a><span data-ttu-id="eea52-206">Wybierz, jakie operacje, jaką może wykorzystać hello budżetu RU/m</span><span class="sxs-lookup"><span data-stu-id="eea52-206">Select which operations can consume hello RU/m budget</span></span>

<span data-ttu-id="eea52-207">Na poziomie żądania użytkownik może także włączanie/wyłączanie RU/m budżetu tooserve hello żądania niezależnie od typu operacji.</span><span class="sxs-lookup"><span data-stu-id="eea52-207">At request level, you can also enable/disable RU/m budget tooserve hello request irrespective of operation type.</span></span> <span data-ttu-id="eea52-208">Regularne elastycznie budżetu RUs na sekundę jest zużywany hello żądania nie mogą korzystać z hello RU/m budżetu, zostanie ograniczony tego żądania.</span><span class="sxs-lookup"><span data-stu-id="eea52-208">If regular provisioned RUs/sec budget is consumed and hello request cannot consume hello RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="eea52-209">Domyślnie wszystkie żądania jest obsługiwana przez budżetu RU/m, jeśli RU/m przepływności budżetu jest aktywna.</span><span class="sxs-lookup"><span data-stu-id="eea52-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="eea52-210">Oto fragment kodu dotyczący wyłączenie budżetu RU/m przy użyciu hello interfejsu API usługi DocumentDB dla operacji CRUD i zapytań.</span><span class="sxs-lookup"><span data-stu-id="eea52-210">Here is a code snippet for disabling RU/m budget using hello DocumentDB API for CRUD and query operations.</span></span>

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a><span data-ttu-id="eea52-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eea52-211">Next steps</span></span>

<span data-ttu-id="eea52-212">W tym artykule możemy zostały opisane działa jak partycjonowania w usłudze Azure DB rozwiązania Cosmos, tworzenia kolekcji partycjonowanych i jak można wybrać stanowi dobry klucz partycji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eea52-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="eea52-213">Należy przeprowadzić testowanie z bazy danych Azure rozwiązania Cosmos wydajności i skalowania.</span><span class="sxs-lookup"><span data-stu-id="eea52-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="eea52-214">Zobacz [wydajności i skalowania testowania z bazy danych Azure rozwiązania Cosmos](performance-testing.md) przykładowe.</span><span class="sxs-lookup"><span data-stu-id="eea52-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="eea52-215">Rozpoczynanie pracy kodowania z hello [zestawów SDK](documentdb-sdk-dotnet.md) lub hello [interfejsu API REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="eea52-215">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="eea52-216">Dowiedz się więcej o [udostępnionej przepływności](request-units.md) w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="eea52-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

