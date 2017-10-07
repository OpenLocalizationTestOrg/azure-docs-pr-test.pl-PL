---
title: "strumień aaaLive za pomocą koderów lokalnych przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki tworzenia kanału, który jest skonfigurowany do dostarczania w formie przekazywania hello."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a><span data-ttu-id="9e99e-103">Jak tooperform transmisja strumieniowa na żywo z lokalnymi koderów przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9e99e-103">How tooperform live streaming with on-premises encoders using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9e99e-104">Portal</span><span class="sxs-lookup"><span data-stu-id="9e99e-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="9e99e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9e99e-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="9e99e-106">REST</span><span class="sxs-lookup"><span data-stu-id="9e99e-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="9e99e-107">Ten samouczek przedstawia kroki hello przy użyciu hello Azure portalu toocreate **kanału** skonfigurowanego do dostarczania w formie przekazywania.</span><span class="sxs-lookup"><span data-stu-id="9e99e-107">This tutorial walks you through hello steps of using hello Azure portal toocreate a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9e99e-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9e99e-108">Prerequisites</span></span>
<span data-ttu-id="9e99e-109">Samouczek hello toocomplete wymagane są następujące Hello:</span><span class="sxs-lookup"><span data-stu-id="9e99e-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="9e99e-110">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9e99e-110">An Azure account.</span></span> <span data-ttu-id="9e99e-111">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e99e-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="9e99e-112">Konto usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="9e99e-112">A Media Services account.</span></span> <span data-ttu-id="9e99e-113">Zobacz toocreate konto usługi Media Services [jak tooCreate konta usługi Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="9e99e-113">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="9e99e-114">Kamera internetowa.</span><span class="sxs-lookup"><span data-stu-id="9e99e-114">A webcam.</span></span> <span data-ttu-id="9e99e-115">Na przykład [koder Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="9e99e-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="9e99e-116">Zdecydowanie zaleca się hello tooreview następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="9e99e-116">It is highly recommended tooreview hello following articles:</span></span>

* [<span data-ttu-id="9e99e-117">Obsługa protokołu RTMP i kodery na żywo w usłudze Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="9e99e-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="9e99e-118">Omówienie transmisji strumieniowej na żywo przy użyciu usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="9e99e-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="9e99e-119">Transmisja strumieniowa na żywo za pomocą koderów lokalnych tworzących strumienie o różnej szybkości transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="9e99e-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="9e99e-120"><a id="scenario"></a>Typowy scenariusz transmisji strumieniowej na żywo</span><span class="sxs-lookup"><span data-stu-id="9e99e-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="9e99e-121">Witaj poniższych krokach opisano zadania związane z tworzeniem typowych aplikacji transmisji strumieniowej na żywo używających kanałów skonfigurowanych do dostarczania przekazywania.</span><span class="sxs-lookup"><span data-stu-id="9e99e-121">hello following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="9e99e-122">Ten samouczek pokazuje, jak toocreate kanał w formie przekazywania i wydarzeń na żywo oraz zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="9e99e-122">This tutorial shows how toocreate and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="9e99e-123">Upewnij się, że jest hello, z którego mają zostać toostream zawartości punktu końcowego przesyłania strumieniowego w hello **systemem** stanu.</span><span class="sxs-lookup"><span data-stu-id="9e99e-123">Make sure hello streaming endpoint from which you want toostream content is in hello **Running** state.</span></span> 
    
1. <span data-ttu-id="9e99e-124">Połącz komputer tooa kamerę wideo.</span><span class="sxs-lookup"><span data-stu-id="9e99e-124">Connect a video camera tooa computer.</span></span> <span data-ttu-id="9e99e-125">Uruchom i skonfiguruj lokalny koder na żywo, który wyprowadza strumień protokołu RTMP o różnej szybkości transmisji bitów lub pofragmentowany strumień MP4.</span><span class="sxs-lookup"><span data-stu-id="9e99e-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="9e99e-126">Aby uzyskać więcej informacji, zobacz temat [Obsługa protokołu RTMP i kodery na żywo w usłudze Azure Media Services](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="9e99e-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="9e99e-127">Ten krok można również wykonać po utworzeniu kanału.</span><span class="sxs-lookup"><span data-stu-id="9e99e-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="9e99e-128">Utwórz i uruchom kanał w formie przekazywania.</span><span class="sxs-lookup"><span data-stu-id="9e99e-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="9e99e-129">Adres URL pozyskiwania, Pobierz hello kanału.</span><span class="sxs-lookup"><span data-stu-id="9e99e-129">Retrieve hello Channel ingest URL.</span></span> 
   
    <span data-ttu-id="9e99e-130">adres URL pozyskiwania Hello jest używany przez hello kodera na żywo toosend hello strumienia toohello kanału.</span><span class="sxs-lookup"><span data-stu-id="9e99e-130">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>
4. <span data-ttu-id="9e99e-131">Pobiera adres URL podglądu kanału hello.</span><span class="sxs-lookup"><span data-stu-id="9e99e-131">Retrieve hello Channel preview URL.</span></span> 
   
    <span data-ttu-id="9e99e-132">Użyj tego adresu URL tooverify, czy kanał prawidłowo odbiera strumień na żywo hello.</span><span class="sxs-lookup"><span data-stu-id="9e99e-132">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>
5. <span data-ttu-id="9e99e-133">Utwórz program lub wydarzenie na żywo.</span><span class="sxs-lookup"><span data-stu-id="9e99e-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="9e99e-134">Przy użyciu hello portalu Azure, również utworzenie wydarzenia na żywo tworzy zasób.</span><span class="sxs-lookup"><span data-stu-id="9e99e-134">When using hello Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="9e99e-135">Uruchom wydarzenie/program hello, gdy są toostart gotowe, przesyłania strumieniowego i archiwizacji.</span><span class="sxs-lookup"><span data-stu-id="9e99e-135">Start hello event/program when you are ready toostart streaming and archiving.</span></span>
7. <span data-ttu-id="9e99e-136">Opcjonalnie hello kodera na żywo może być sygnałowego toostart anonsu.</span><span class="sxs-lookup"><span data-stu-id="9e99e-136">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="9e99e-137">Witaj reklama jest wstawiana hello strumienia wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="9e99e-137">hello advertisement is inserted in hello output stream.</span></span>
8. <span data-ttu-id="9e99e-138">Zatrzymaj wydarzenie/program hello zawsze, gdy chcesz toostop przesyłanie strumieniowe i archiwizowanie wydarzenia hello.</span><span class="sxs-lookup"><span data-stu-id="9e99e-138">Stop hello event/program whenever you want toostop streaming and archiving hello event.</span></span>
9. <span data-ttu-id="9e99e-139">Usuń wydarzenie/program hello (i opcjonalnie można również usunąć hello zasobów).</span><span class="sxs-lookup"><span data-stu-id="9e99e-139">Delete hello event/program (and optionally delete hello asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="9e99e-140">Zapoznaj się z tematem [transmisję strumieniową na żywo za pomocą koderów lokalnych, które tworzą strumienie o różnych szybkościach transmisji bitów](media-services-live-streaming-with-onprem-encoders.md) toolearn założenia i zagadnienia związane z toolive przesyłania strumieniowego z koderów lokalnych i kanałów w formie przekazywania.</span><span class="sxs-lookup"><span data-stu-id="9e99e-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) toolearn about concepts and considerations related toolive streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="tooview-notifications-and-errors"></a><span data-ttu-id="9e99e-141">tooview powiadomień i błędów</span><span class="sxs-lookup"><span data-stu-id="9e99e-141">tooview notifications and errors</span></span>
<span data-ttu-id="9e99e-142">Jeśli chcesz tooview powiadomienia i błędy generowane przez hello portalu Azure, kliknij ikonę powiadomienia hello.</span><span class="sxs-lookup"><span data-stu-id="9e99e-142">If you want tooview notifications and errors produced by hello Azure portal, click on hello Notification icon.</span></span>

![Powiadomienia](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="9e99e-144">Tworzenie i uruchamianie kanałów i wydarzeń w formie przekazywania</span><span class="sxs-lookup"><span data-stu-id="9e99e-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="9e99e-145">Kanał jest skojarzony z wydarzeniami/programami, umożliwiających toocontrol hello publikowania i przechowywania segmentów strumienia na żywo.</span><span class="sxs-lookup"><span data-stu-id="9e99e-145">A channel is associated with events/programs that enable you toocontrol hello publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="9e99e-146">Kanały zarządzają wydarzeniami.</span><span class="sxs-lookup"><span data-stu-id="9e99e-146">Channels manage events.</span></span> 

<span data-ttu-id="9e99e-147">Można określić hello liczbę godzin zawartości hello rejestrowane tooretain hello programu przez ustawienie hello **okno archiwum** długości.</span><span class="sxs-lookup"><span data-stu-id="9e99e-147">You can specify hello number of hours you want tooretain hello recorded content for hello program by setting hello **Archive Window** length.</span></span> <span data-ttu-id="9e99e-148">Tę wartość można ustawić z co najmniej 5 minut tooa maksymalnie 25 godzin.</span><span class="sxs-lookup"><span data-stu-id="9e99e-148">This value can be set from a minimum of 5 minutes tooa maximum of 25 hours.</span></span> <span data-ttu-id="9e99e-149">Długość okna archiwum określa również dostępny hello maksymalną ilość czasu, klienci mogą zwrócić wstecz od bieżącego położenia na żywo hello.</span><span class="sxs-lookup"><span data-stu-id="9e99e-149">Archive window length also dictates hello maximum amount of time clients can seek back in time from hello current live position.</span></span> <span data-ttu-id="9e99e-150">Zdarzenia mogą być uruchamiane hello określoną ilość czasu, ale zawartość, która wykracza poza długość okna hello jest stale odrzucana.</span><span class="sxs-lookup"><span data-stu-id="9e99e-150">Events can run over hello specified amount of time, but content that falls behind hello window length is continuously discarded.</span></span> <span data-ttu-id="9e99e-151">Ta wartość tej właściwości określa również, jak długo klient hello mogą być manifesty.</span><span class="sxs-lookup"><span data-stu-id="9e99e-151">This value of this property also determines how long hello client manifests can grow.</span></span>

<span data-ttu-id="9e99e-152">Każde wydarzenie jest skojarzone z elementem zawartości.</span><span class="sxs-lookup"><span data-stu-id="9e99e-152">Each event is associated with an asset.</span></span> <span data-ttu-id="9e99e-153">toopublish hello zdarzenia, należy utworzyć Lokalizator OnDemand dla hello skojarzonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9e99e-153">toopublish hello event, you must create an OnDemand locator for hello associated asset.</span></span> <span data-ttu-id="9e99e-154">Lokalizator umożliwia toobuild adresu URL przesyłania strumieniowego, która może zapewnić tooyour klientów.</span><span class="sxs-lookup"><span data-stu-id="9e99e-154">Having this locator enables you toobuild a streaming URL that you can provide tooyour clients.</span></span>

<span data-ttu-id="9e99e-155">Kanał obsługuje toothree współbieżnie uruchomionych zdarzeń, dzięki czemu można tworzyć wiele archiwów hello samego strumienia przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="9e99e-155">A channel supports up toothree concurrently running events so you can create multiple archives of hello same incoming stream.</span></span> <span data-ttu-id="9e99e-156">Dzięki temu toopublish i archiwum różnych części wydarzenia zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="9e99e-156">This allows you toopublish and archive different parts of an event as needed.</span></span> <span data-ttu-id="9e99e-157">Na przykład konkretnym wymaganiom biznesowym jest tooarchive sześciu godzin programu, ale toobroadcast ostatnich 10 minut.</span><span class="sxs-lookup"><span data-stu-id="9e99e-157">For example, your business requirement is tooarchive 6 hours of a program, but toobroadcast only last 10 minutes.</span></span> <span data-ttu-id="9e99e-158">tooaccomplish, należy toocreate dwa jednocześnie uruchomione programy.</span><span class="sxs-lookup"><span data-stu-id="9e99e-158">tooaccomplish this, you need toocreate two concurrently running programs.</span></span> <span data-ttu-id="9e99e-159">Jeden program ustawiono tooarchive sześciu godzin zdarzenia hello, ale hello program nie został opublikowany.</span><span class="sxs-lookup"><span data-stu-id="9e99e-159">One program is set tooarchive 6 hours of hello event but hello program is not published.</span></span> <span data-ttu-id="9e99e-160">Hello inny program jest zestaw tooarchive przez 10 minut i ten program zostanie opublikowany.</span><span class="sxs-lookup"><span data-stu-id="9e99e-160">hello other program is set tooarchive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="9e99e-161">Istniejących wydarzeń na żywo nie należy używać ponownie.</span><span class="sxs-lookup"><span data-stu-id="9e99e-161">You should not reuse existing live events.</span></span> <span data-ttu-id="9e99e-162">Zamiast tego należy utworzyć i uruchomić nowe wydarzenie dla każdego wydarzenia.</span><span class="sxs-lookup"><span data-stu-id="9e99e-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="9e99e-163">Uruchomić zdarzenie hello, gdy są toostart gotowe, przesyłania strumieniowego i archiwizacji.</span><span class="sxs-lookup"><span data-stu-id="9e99e-163">Start hello event when you are ready toostart streaming and archiving.</span></span> <span data-ttu-id="9e99e-164">Zatrzymaj hello program zawsze, gdy chcesz toostop przesyłanie strumieniowe i archiwizowanie wydarzenia hello.</span><span class="sxs-lookup"><span data-stu-id="9e99e-164">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span> 

<span data-ttu-id="9e99e-165">toodelete zarchiwizowane zawartość, Zatrzymaj i Usuń hello zdarzeń, a następnie usuń hello skojarzonego elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="9e99e-165">toodelete archived content, stop and delete hello event and then delete hello associated asset.</span></span> <span data-ttu-id="9e99e-166">Nie można usunąć elementu zawartości, jeśli jest on używany przez zdarzenie; Najpierw należy usunąć Hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9e99e-166">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="9e99e-167">Nawet po zatrzymaniu i usunięciu hello zdarzeń, hello użytkownicy będą mogli toostream zarchiwizowaną zawartość wideo na żądanie, dla tak długo, jak hello zasobów nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="9e99e-167">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span>

<span data-ttu-id="9e99e-168">Jeśli chcesz zarchiwizować hello tooretain zawartości, ale nie jest dostępny do przesyłania strumieniowego, Usuń hello przesyłania strumieniowego lokalizatora.</span><span class="sxs-lookup"><span data-stu-id="9e99e-168">If you do want tooretain hello archived content, but not have it available for streaming, delete hello streaming locator.</span></span>

### <a name="toouse-hello-portal-toocreate-a-channel"></a><span data-ttu-id="9e99e-169">toouse hello portalu toocreate kanału</span><span class="sxs-lookup"><span data-stu-id="9e99e-169">toouse hello portal toocreate a channel</span></span>
<span data-ttu-id="9e99e-170">W tej sekcji przedstawiono sposób toouse hello **szybkie tworzenie** toocreate opcja kanał w formie przekazywania.</span><span class="sxs-lookup"><span data-stu-id="9e99e-170">This section shows how toouse hello **Quick Create** option toocreate a pass-through channel.</span></span>

<span data-ttu-id="9e99e-171">Więcej szczegółowych informacji dotyczących kanałów przekazujących można znaleźć w temacie [Transmisja strumieniowa na żywo za pomocą koderów lokalnych tworzących strumienie o różnej szybkości transmisji bitów](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="9e99e-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="9e99e-172">W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="9e99e-172">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="9e99e-173">W hello **ustawienia** okna, kliknij przycisk **transmisja strumieniowa na żywo**.</span><span class="sxs-lookup"><span data-stu-id="9e99e-173">In hello **Settings** window, click **Live streaming**.</span></span> 
   
    ![Wprowadzenie](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="9e99e-175">Witaj **transmisja strumieniowa na żywo** zostanie wyświetlone okno.</span><span class="sxs-lookup"><span data-stu-id="9e99e-175">hello **Live streaming** window appears.</span></span>
3. <span data-ttu-id="9e99e-176">Kliknij przycisk **szybkie tworzenie** protokołu pozyskiwania toocreate kanał w formie przekazywania z hello RTMP.</span><span class="sxs-lookup"><span data-stu-id="9e99e-176">Click **Quick Create** toocreate a pass-through channel with hello RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="9e99e-177">Witaj **Utwórz nowy kanał** zostanie wyświetlone okno.</span><span class="sxs-lookup"><span data-stu-id="9e99e-177">hello **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="9e99e-178">Nadaj nazwę hello nowy kanał, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9e99e-178">Give hello new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="9e99e-179">Kanał w formie przekazywania to tworzy z hello protokołu pozyskiwania RTMP.</span><span class="sxs-lookup"><span data-stu-id="9e99e-179">This creates a pass-through channel with hello RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="9e99e-180">Tworzenie wydarzeń</span><span class="sxs-lookup"><span data-stu-id="9e99e-180">Create events</span></span>
1. <span data-ttu-id="9e99e-181">Wybierz toowhich kanału, ma tooadd zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="9e99e-181">Select a channel toowhich you want tooadd an event.</span></span>
2. <span data-ttu-id="9e99e-182">Naciśnij przycisk **Wydarzenie na żywo**.</span><span class="sxs-lookup"><span data-stu-id="9e99e-182">Press **Live Event** button.</span></span>

![Wydarzenie](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="9e99e-184">Pobieranie adresów URL pozyskiwania</span><span class="sxs-lookup"><span data-stu-id="9e99e-184">Get ingest URLs</span></span>
<span data-ttu-id="9e99e-185">Po utworzeniu kanału hello można uzyskać pozyskiwania adresów URL, które zapewnią toohello kodera na żywo.</span><span class="sxs-lookup"><span data-stu-id="9e99e-185">Once hello channel is created, you can get ingest URLs that you will provide toohello live encoder.</span></span> <span data-ttu-id="9e99e-186">Witaj koder używa tych adresów URL tooinput strumień na żywo.</span><span class="sxs-lookup"><span data-stu-id="9e99e-186">hello encoder uses these URLs tooinput a live stream.</span></span>

![Utworzone](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a><span data-ttu-id="9e99e-188">Obejrzyj hello zdarzeń</span><span class="sxs-lookup"><span data-stu-id="9e99e-188">Watch hello event</span></span>
<span data-ttu-id="9e99e-189">toowatch hello zdarzenia, kliknij przycisk **czujki** w hello Azure hello portalu lub kopiowania URL przesyłania strumieniowego i Użyj wybranego odtwarzacza.</span><span class="sxs-lookup"><span data-stu-id="9e99e-189">toowatch hello event, click **Watch** in hello Azure portal or copy hello streaming URL and use a player of your choice.</span></span> 

![Utworzone](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="9e99e-191">Wydarzenia na żywo automatycznie Pobierz zawartość przekonwertowanego żądanie tooon po zatrzymaniu.</span><span class="sxs-lookup"><span data-stu-id="9e99e-191">Live event automatically get converted tooon-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="9e99e-192">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="9e99e-192">Clean up</span></span>
<span data-ttu-id="9e99e-193">Więcej szczegółowych informacji dotyczących kanałów przekazujących można znaleźć w temacie [Transmisja strumieniowa na żywo za pomocą koderów lokalnych tworzących strumienie o różnej szybkości transmisji bitów](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="9e99e-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="9e99e-194">Kanał można zatrzymać tylko wtedy, gdy wszystkie wydarzenia/programy na kanale hello zostały zatrzymane.</span><span class="sxs-lookup"><span data-stu-id="9e99e-194">A channel can be stopped only when all events/programs on hello channel have been stopped.</span></span>  <span data-ttu-id="9e99e-195">Po zatrzymaniu kanału hello nie nie poniesiesz żadnych dodatkowych opłat.</span><span class="sxs-lookup"><span data-stu-id="9e99e-195">Once hello Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="9e99e-196">Jeśli wymagane jest toostart go ponownie, będzie mieć hello sam adres URL pozyskiwania, więc nie trzeba tooreconfigure kodera.</span><span class="sxs-lookup"><span data-stu-id="9e99e-196">When you need toostart it again, it will have hello same ingest URL so you won't need tooreconfigure your encoder.</span></span>
* <span data-ttu-id="9e99e-197">Kanał można usunąć tylko wtedy, gdy wszystkie wydarzenia na żywo w kanale hello zostały usunięte.</span><span class="sxs-lookup"><span data-stu-id="9e99e-197">A channel can be deleted only when all live events on hello channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="9e99e-198">Wyświetlanie zarchiwizowanej zawartości</span><span class="sxs-lookup"><span data-stu-id="9e99e-198">View archived content</span></span>
<span data-ttu-id="9e99e-199">Nawet po zatrzymaniu i usunięciu hello zdarzeń, hello użytkownicy będą mogli toostream zarchiwizowaną zawartość wideo na żądanie, dla tak długo, jak hello zasobów nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="9e99e-199">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span> <span data-ttu-id="9e99e-200">Nie można usunąć elementu zawartości, jeśli jest on używany przez zdarzenie; Najpierw należy usunąć Hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9e99e-200">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="9e99e-201">Wybierz zasobów, toomanage **ustawienie** i kliknij przycisk **zasoby**.</span><span class="sxs-lookup"><span data-stu-id="9e99e-201">toomanage your assets, select **Setting** and click **Assets**.</span></span>

![Elementy zawartości](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="9e99e-203">Następny krok</span><span class="sxs-lookup"><span data-stu-id="9e99e-203">Next step</span></span>
<span data-ttu-id="9e99e-204">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="9e99e-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9e99e-205">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="9e99e-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

