---
title: "Analytics Platform: tooStream porównania Apache Storm Analytics | Dokumentacja firmy Microsoft"
description: "Pobierz wskazówki Wybieranie platformy analityka w chmurze przy użyciu systemu Apache Storm porównanie tooStream Analytics. Zrozumieć funkcje i różnice."
keywords: "Platforma do analiz, analytics platform, platforma do analiz chmury, porównanie storm"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: b9aac017-9866-4d0a-b98f-6f03881e9339
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/27/2017
ms.author: samacha
ms.openlocfilehash: 5a0ec5b2439596f0da962f04b776472031660062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a><span data-ttu-id="15b50-105">Wybieranie przesyłania strumieniowego platforma do analiz: porównanie systemu Apache Storm i usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="15b50-105">Choosing a streaming analytics platform: comparing Apache Storm and Azure Stream Analytics</span></span>
<span data-ttu-id="15b50-106">Platforma Azure oferuje wiele rozwiązań do analizowania danych przesyłania strumieniowego: [analiza strumienia Azure](https://docs.microsoft.com/azure/stream-analytics/) i [Apache Storm w usłudze Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span><span class="sxs-lookup"><span data-stu-id="15b50-106">Azure provides multiple solutions for analyzing streaming data: [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) and [Apache Storm on Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span></span> <span data-ttu-id="15b50-107">Obu platform analytics zapewnia korzyści hello rozwiązania typu PaaS.</span><span class="sxs-lookup"><span data-stu-id="15b50-107">Both analytics platforms provide hello benefits of a PaaS solution.</span></span> <span data-ttu-id="15b50-108">Ale platform hello niektóre istotne różnice w ich możliwości, jak również w sposób konfigurowania i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="15b50-108">But hello platforms have some significant differences in their capabilities as well as in how you configure and manage them.</span></span> 

<span data-ttu-id="15b50-109">W tym artykule przedstawiono porównanie side-by-side toohelp funkcje, wybrać między Apache Storm i analiza strumienia Azure jako platforma do analiz chmury.</span><span class="sxs-lookup"><span data-stu-id="15b50-109">This article provides a side-by-side comparison of features toohelp you choose between Apache Storm and Azure Stream Analytics as a cloud analytics platform.</span></span> 

## <a name="general-features"></a><span data-ttu-id="15b50-110">Funkcje ogólne</span><span class="sxs-lookup"><span data-stu-id="15b50-110">General features</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-111">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-111">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="15b50-112">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-112">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="15b50-113">
                    <strong>Apache Storm w usłudze HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-113">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-114">
                    <strong>Typu open source?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-114">
                    <strong>Open source?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-115">Nie.</span><span class="sxs-lookup"><span data-stu-id="15b50-115">No.</span></span> <span data-ttu-id="15b50-116">Usługa Azure Stream Analytics jest zastrzeżonych Microsoft oferty.</span><span class="sxs-lookup"><span data-stu-id="15b50-116">Azure Stream Analytics is a Microsoft proprietary offering.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-117">Tak.</span><span class="sxs-lookup"><span data-stu-id="15b50-117">Yes.</span></span> <span data-ttu-id="15b50-118">Apache Storm to technologia Apache licencji.</span><span class="sxs-lookup"><span data-stu-id="15b50-118">Apache Storm is an Apache licensed technology.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-119">
                    <strong>Pomoc techniczna firmy Microsoft?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-119">
                    <strong>Microsoft support?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-120">Tak</span><span class="sxs-lookup"><span data-stu-id="15b50-120">Yes</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-121">Tak</span><span class="sxs-lookup"><span data-stu-id="15b50-121">Yes</span></span> </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-122">
                    <strong>Wymagania sprzętowe</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-122">
                    <strong>Hardware requirements</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-123">Brak.</span><span class="sxs-lookup"><span data-stu-id="15b50-123">None.</span></span> <span data-ttu-id="15b50-124">Usługa Azure Stream Analytics jest usługą platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="15b50-124">Azure Stream Analytics is an Azure Service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-125">Brak.</span><span class="sxs-lookup"><span data-stu-id="15b50-125">None.</span></span> <span data-ttu-id="15b50-126">Apache Storm jest usługą platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="15b50-126">Apache Storm is an Azure Service.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-127">
                    <strong>Jednostki najwyższego poziomu</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-127">
                    <strong>Top-level unit</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-128">Użytkownicy, wdrażanie i monitorowanie zadań przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="15b50-128">Users deploy and monitor streaming jobs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-129">Użytkownicy, wdrażanie i monitorowanie całego klastra, który może obsługiwać wiele zadań Storm, a także innych obciążeń (w tym partii).</span><span class="sxs-lookup"><span data-stu-id="15b50-129">Users deploy and monitor a whole cluster, which can host multiple Storm jobs as well as other workloads (including batch).</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-130">
                    <strong>Cennik</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-130">
                    <strong>Pricing</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-131">Cena za wolumen danych przetwarzanych i działa hello liczbę jednostek przesyłania strumieniowego wymagane na godzinę, które hello zadania.</span><span class="sxs-lookup"><span data-stu-id="15b50-131">Priced by volume of data processed and hello number of streaming units required per hour that hello job is running.</span></span> 
                </p>
                    <p><span data-ttu-id="15b50-132">Aby uzyskać więcej informacji, zobacz <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">cennik usługi analiza strumienia</a>.</span><span class="sxs-lookup"><span data-stu-id="15b50-132">For more information, see <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics Pricing</a>.</span></span></p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-133">Jednostka Hello zakupu jest oparty na klastrze i jest rozliczana na podstawie na czas hello hello klaster działa, niezależnie od zadania wdrożone.</span><span class="sxs-lookup"><span data-stu-id="15b50-133">hello unit of purchase is cluster-based, and is charged based on hello time hello cluster is running, independent of jobs deployed.</span></span>
                </p>
                <p>
<span data-ttu-id="15b50-134">Aby uzyskać więcej informacji, zobacz <a href="http://azure.microsoft.com/pricing/details/hdinsight/">cennik usługi HDInsight</a>.</span><span class="sxs-lookup"><span data-stu-id="15b50-134">For more information, see <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight pricing</a>.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a><span data-ttu-id="15b50-135">Tworzenie</span><span class="sxs-lookup"><span data-stu-id="15b50-135">Authoring</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-136">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-136">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="15b50-137">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-137">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="15b50-138">
                    <strong>Apache Storm w usłudze HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-138">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-139">
                    <strong>Możliwości: DSL SQL?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-139">
                    <strong>Capabilities: SQL DSL?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-140">Tak.</span><span class="sxs-lookup"><span data-stu-id="15b50-140">Yes.</span></span> <span data-ttu-id="15b50-141">Stream Analytics zapewnia języka przypominającego SQL do tworzenia przekształcenia.</span><span class="sxs-lookup"><span data-stu-id="15b50-141">Stream Analytics provides a SQL-like language for creating transformations.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-142">Nie.</span><span class="sxs-lookup"><span data-stu-id="15b50-142">No.</span></span> <span data-ttu-id="15b50-143">Użytkownicy pisania kodu w języku Java lub C# lub przy użyciu interfejsów API języka Trident.</span><span class="sxs-lookup"><span data-stu-id="15b50-143">Users write code in Java or C#, or use Trident APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-144">
                    <strong>Możliwości: Operatory czasowe?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-144">
                    <strong>Capabilities: Temporal operators?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-145">Agregacjami i sprzężenia danych czasowych są obsługiwane domyślnie.</span><span class="sxs-lookup"><span data-stu-id="15b50-145">Windowed aggregates and temporal joins are supported by default.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-146">Operatory czasowe musi być implementowana przez użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="15b50-146">Temporal operators must be implemented by hello user.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-147">
                    <strong>Środowisko programistyczne</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-147">
                    <strong>Development experience</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-148">Użytkownicy mogą utworzyć, debugowania i monitorowania zadań za pośrednictwem hello portalu Azure, przy użyciu przykładowych danych pochodzących z strumień na żywo.</span><span class="sxs-lookup"><span data-stu-id="15b50-148">Users can create, debug, and monitor jobs through hello Azure portal, using sample data derived from a live stream.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-149">Użytkownicy przy użyciu platformy .NET można rozwijać, debugowania i monitorować za pomocą programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15b50-149">Users using .NET can develop, debug, and monitor through Visual Studio.</span></span> <span data-ttu-id="15b50-150">Za pomocą języka Java lub innych języków umożliwia hello IDE siebie.</span><span class="sxs-lookup"><span data-stu-id="15b50-150">Users using Java or other languages can use hello IDE of their choice.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-151">
                    <strong>Obsługa debugowania</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-151">
                    <strong>Debugging support</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-152">Podstawowe zadania stanu oraz operacji dzienniki są dostępne toohelp debugowania.</span><span class="sxs-lookup"><span data-stu-id="15b50-152">Basic job status and operations logs are available toohelp debug.</span></span> <span data-ttu-id="15b50-153">Analiza strumienia obecnie nie zezwala użytkownikom na określanie zawartości lub ilości zawartości znajduje się w dziennikach hello (tj. tryb informacji pełnej).</span><span class="sxs-lookup"><span data-stu-id="15b50-153">Stream Analytics currently does not let users specify what content or how much content is included in hello logs (i.e., verbose mode).</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-154">Szczegółowe dzienniki są dostępne.</span><span class="sxs-lookup"><span data-stu-id="15b50-154">Detailed logs are available.</span></span> <span data-ttu-id="15b50-155">Użytkownicy mają dostęp do dzienników w Visual Studio lub rejestrowania w klastrze toohello i bezpośrednie uzyskiwanie dostępu do dzienników hello.</span><span class="sxs-lookup"><span data-stu-id="15b50-155">Users can access logs in Visual Studio or by logging in toohello cluster and accessing hello logs directly.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-156">
                    <strong>Rozszerzalność przy użyciu kodu niestandardowego?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-156">
                    <strong>Extensibility using custom code?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-157">Częściowo obsługiwać funkcje UDF języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="15b50-157">Partially support with JavaScript UDFs.</span></span> <span data-ttu-id="15b50-158">Aby uzyskać więcej informacji, zobacz <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">integracji UDF języka JavaScript</a>.</span><span class="sxs-lookup"><span data-stu-id="15b50-158">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">JavaScript UDF integration</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-159">Tak.</span><span class="sxs-lookup"><span data-stu-id="15b50-159">Yes.</span></span> <span data-ttu-id="15b50-160">Użytkownicy mogą pisanie kodu niestandardowego w C#, Java lub dowolnego innego języka, obsługiwane na Storm.</span><span class="sxs-lookup"><span data-stu-id="15b50-160">Users can write custom code in C#, Java, or any other language supported on Storm.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a><span data-ttu-id="15b50-161">Źródła danych (dane wejściowe) i dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="15b50-161">Data sources (inputs) and outputs</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-162">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-162">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="15b50-163">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-163">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="15b50-164">
                    <strong>Apache Storm w usłudze HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-164">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-165">
                 <strong>Źródła danych wejściowych</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-165">
                 <strong>Input data sources</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="15b50-166">Magazyn Azure Event Hubs i obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="15b50-166">Azure Event Hubs and Azure Blob storage.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-167">Łączniki są dostępne dla usługi Azure Event Hubs, usługi Azure Service Bus, Kafka i inne.</span><span class="sxs-lookup"><span data-stu-id="15b50-167">Connectors are available for Azure Event Hubs, Azure Service Bus, Kafka, and more.</span></span> <span data-ttu-id="15b50-168">Użytkownicy mogą tworzyć dodatkowe łączniki przy użyciu kodu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="15b50-168">Users can create additional connectors using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-169">
                    <strong>Formaty danych wejściowych</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-169">
                    <strong>Input data formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-170">Avro JSON, CSV</span><span class="sxs-lookup"><span data-stu-id="15b50-170">Avro, JSON, CSV</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-171">Użytkownicy mogą zaimplementować dowolnym formacie przy użyciu kodu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="15b50-171">Users can implement any format using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-172">
                    <strong>Dane wyjściowe</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-172">
                    <strong>Outputs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-173">Zadanie przesyłania strumieniowego może mieć wielu wyjść.</span><span class="sxs-lookup"><span data-stu-id="15b50-173">A streaming job can have multiple outputs.</span></span> <span data-ttu-id="15b50-174">Obsługiwane dane wyjściowe są usługi Azure Event Hubs, obiektów Blob platformy Azure magazynu tabel Azure magazynu, bazy danych SQL Azure i usługi Power BI.</span><span class="sxs-lookup"><span data-stu-id="15b50-174">Supported outputs are Azure Event Hubs, Azure Blob storage, Azure Table storage, Azure SQL DB, and Power BI.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-175">STORM obsługuje wiele dane wyjściowe w topologii, a każdy dane wyjściowe mogą mieć niestandardową logikę na potrzeby przetwarzania podrzędnego.</span><span class="sxs-lookup"><span data-stu-id="15b50-175">Storm supports many outputs in a topology, and each output can have custom logic for downstream processing.</span></span> <span data-ttu-id="15b50-176">STORM zawiera łączniki dla usługi Power BI, Azure Event Hubs, obiektów Blob platformy Azure magazynu, bazy danych Azure rozwiązania Cosmos, SQL i bazy danych HBase.</span><span class="sxs-lookup"><span data-stu-id="15b50-176">Storm includes connectors for Power BI, Azure Event Hubs, Azure Blob storage, Azure Cosmos DB, SQL, and HBase.</span></span> <span data-ttu-id="15b50-177">Użytkownicy mogą tworzyć dodatkowe łączniki przy użyciu kodu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="15b50-177">Users can create additional connectors using custom code.</span></span>    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-178">
                    <strong>Formaty kodowania danych</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-178">
                    <strong>Data-encoding formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-179">Dane muszą być sformatowane w formacie UTF-8.</span><span class="sxs-lookup"><span data-stu-id="15b50-179">Data must be formatted using UTF-8.</span></span>
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-180">Użytkownicy mogą zaimplementować żadnych format kodowania danych przy użyciu kodu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="15b50-180">Users can implement any data encoding format using custom code.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a><span data-ttu-id="15b50-181">Zarządzanie i operacje</span><span class="sxs-lookup"><span data-stu-id="15b50-181">Management and operations</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-182">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-182">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="15b50-183">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-183">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="15b50-184">
                    <strong>Apache Storm w usłudze HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-184">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-185">
                    <strong>Model wdrażania zadania</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-185">
                    <strong>Job deployment model</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-186">Portalu Azure, programu PowerShell i interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="15b50-186">Azure portal, PowerShell, and REST APIs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-187">Portalu Azure, programu PowerShell programu Visual Studio i interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="15b50-187">Azure portal, PowerShell, Visual Studio, and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-188">
                    <strong>Monitorowanie (Statystyka, liczniki itp.)</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-188">
                    <strong>Monitoring (stats, counters, etc.)</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-189">Monitorowanie jest implementowane przy użyciu portalu Azure i interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="15b50-189">Monitoring is implemented using Azure portal and REST APIs.</span></span> <span data-ttu-id="15b50-190">Użytkownicy, można również skonfigurować alerty platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="15b50-190">Users can also configure Azure alerts.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-191">Monitorowanie jest implementowane przy użyciu interfejsu użytkownika platformy Storm hello i interfejsów API REST.</span><span class="sxs-lookup"><span data-stu-id="15b50-191">Monitoring is implemented using hello Storm UI and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-192">
                    <strong>Skalowalność</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-192">
                    <strong>Scalability</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-193">Skalowalność jest określana przez hello liczbę jednostek przesyłania strumieniowego (SUs) dla każdego zadania.</span><span class="sxs-lookup"><span data-stu-id="15b50-193">Scalability is determined by hello number of Streaming Units (SUs) for each job.</span></span> <span data-ttu-id="15b50-194">Każdej jednostki przesyłania strumieniowego przetwarza się too1 MB na sekundę, z maksymalną liczbę jednostek 50.</span><span class="sxs-lookup"><span data-stu-id="15b50-194">Each Streaming Unit processes up too1 MB/second, with a maximum 50 units.</span></span> <span data-ttu-id="15b50-195">Aby uzyskać więcej informacji, zobacz <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">przepływności tooincrease skali</a>.</span><span class="sxs-lookup"><span data-stu-id="15b50-195">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Scale tooincrease throughput</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-196">Skalowalność jest określana przez hello liczby węzłów w hello klaster Storm w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="15b50-196">Scalability is determined by hello number of nodes in hello HDInsight Storm cluster.</span></span> <span data-ttu-id="15b50-197">Górny limit hello liczby węzłów Hello jest zdefiniowana przez użytkownika hello Azure przydziału.</span><span class="sxs-lookup"><span data-stu-id="15b50-197">hello top limit on hello number of nodes is defined by hello user's Azure quota.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-198">
                    <strong>Limity przetwarzania danych</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-198">
                    <strong>Data processing limits</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-199">Użytkownicy, można zwiększyć przetwarzanie danych lub optymalizować koszty, zwiększ lub Zmniejsz hello liczbę jednostek przesyłania strumieniowego, z górnym limitem 1 GB na sekundę.</span><span class="sxs-lookup"><span data-stu-id="15b50-199">Users can increase data processing or optimize costs by increasing or decreasing hello number of Streaming Units, with an upper limit of 1 GB/second.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-200">Użytkownicy mogą być skalowane rozmiar klastra w górę lub w dół.</span><span class="sxs-lookup"><span data-stu-id="15b50-200">Users can scale cluster size up or down.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-201">
                    <strong>Zatrzymaj/wznowień</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-201">
                    <strong>Stop/Resume</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-202">Zatrzymaj i wznowić z ostatniego miejsca zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="15b50-202">Stop and resume from last place stopped.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-203">Zatrzymaj i wznowić z ostatniego umieść zatrzymania oparte na znak wodny.</span><span class="sxs-lookup"><span data-stu-id="15b50-203">Stop and resume from last place stopped based on a watermark.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-204">
                    <strong>Aktualizacja usługi i framework</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-204">
                    <strong>Service and framework update</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-205">Automatyczne stosowanie poprawek bez przestojów.</span><span class="sxs-lookup"><span data-stu-id="15b50-205">Automatic patching with no downtime.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-206">Automatyczne stosowanie poprawek bez przestojów.</span><span class="sxs-lookup"><span data-stu-id="15b50-206">Automatic patching with no downtime.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-207">
                    <strong>Ciągłość prowadzenia działalności biznesowej poprzez wysokiej dostępności usługi za pomocą gwarantowane umowy SLA</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-207">
                    <strong>Business continuity through a Highly Available Service with guaranteed SLAs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li><span data-ttu-id="15b50-208">Umowa SLA z wartością 99,9% czasu pracy</span><span class="sxs-lookup"><span data-stu-id="15b50-208">SLA of 99.9% uptime</span></span></li>
                <li><span data-ttu-id="15b50-209">Automatycznego odzyskiwania z błędami</span><span class="sxs-lookup"><span data-stu-id="15b50-209">Auto-recovery from failures</span></span></li>
                <li><span data-ttu-id="15b50-210">Wbudowane odzyskiwanie stanowe operatory czasowe</span><span class="sxs-lookup"><span data-stu-id="15b50-210">Built-in recovery of stateful temporal operators</span></span></li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-211">SLA 99,9% czasu pracy hello klaster Storm.</span><span class="sxs-lookup"><span data-stu-id="15b50-211">SLA of 99.9% uptime of hello Storm cluster.</span></span> 
                </p>
                <p>
<span data-ttu-id="15b50-212">Apache Storm to odpornej na uszkodzenia platformy przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="15b50-212">Apache Storm is a fault-tolerant streaming platform.</span></span> <span data-ttu-id="15b50-213">Jest jednak czy przesyłanie strumieniowe zadania wykonywania nieprzerwaną tooensure odpowiedzialność hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="15b50-213">However, it is hello user's responsibility tooensure that streaming jobs run uninterrupted.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a><span data-ttu-id="15b50-214">Funkcje zaawansowane</span><span class="sxs-lookup"><span data-stu-id="15b50-214">Advanced features</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-215">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-215">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="15b50-216">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-216">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="15b50-217">
                    <strong>Apache Storm w usłudze HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-217">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-218">
                    <strong>Obsługa zdarzeń późne przyjęcia i poza kolejnością.</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-218">
                    <strong>Late arrival and out-of-order event handling</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-219">Wbudowane zasady można skonfigurować można zmienić kolejność zdarzeń, upuszczania lub Dostosuj czas trwania zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="15b50-219">Built-in configurable policies can reorder events, drop events, or adjust event time.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-220">Użytkownicy muszą implementować toohandle logiki tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="15b50-220">Users must implement logic toohandle this scenario.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-221">
                    <strong>Dane referencyjne</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-221">
                    <strong>Reference data</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-222">Dane referencyjne jest dostępna z magazynu obiektów Blob platformy Azure z maksymalnie 100 MB pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="15b50-222">Reference data is available from Azure Blob storage with a maximum of 100 MB of in-memory cache.</span></span> <span data-ttu-id="15b50-223">Dane referencyjne są odświeżane przez usługę hello.</span><span class="sxs-lookup"><span data-stu-id="15b50-223">Reference data is refreshed by hello service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-224">Brak ograniczeń na rozmiar danych.</span><span class="sxs-lookup"><span data-stu-id="15b50-224">No limits on data size.</span></span> <span data-ttu-id="15b50-225">Łączniki są dostępne dla bazy danych HBase, bazy danych rozwiązania Cosmos platformy Azure, programu SQL Server i Azure.</span><span class="sxs-lookup"><span data-stu-id="15b50-225">Connectors are available for HBase, Azure Cosmos DB, SQL Server, and Azure.</span></span> <span data-ttu-id="15b50-226">Użytkownicy mogą tworzyć dodatkowe łączniki przy użyciu kodu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="15b50-226">Users can create additional connectors using custom code.</span></span> <span data-ttu-id="15b50-227">Dane referencyjne musi zostać odświeżona przy użyciu kodu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="15b50-227">Reference data must be refreshed using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="15b50-228">
                    <strong>Integracja z uczenia maszynowego</strong>
                </span><span class="sxs-lookup"><span data-stu-id="15b50-228">
                    <strong>Integration with Machine Learning</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="15b50-229">Opublikowane podczas tworzenia zadania można skonfigurować jako funkcje modeli uczenia maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="15b50-229">Published Azure Machine Learning models can be configured as functions during job creation.</span></span> <span data-ttu-id="15b50-230">Aby uzyskać więcej informacji, zobacz <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">skali dla funkcji Machine Learning</a>.</span><span class="sxs-lookup"><span data-stu-id="15b50-230">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Scale for Machine Learning functions</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="15b50-231">Dostępne za pośrednictwem Storm elementów Bolt.</span><span class="sxs-lookup"><span data-stu-id="15b50-231">Available through Storm Bolts.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>
