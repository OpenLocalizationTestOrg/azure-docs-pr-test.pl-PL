---
title: "Transmisja strumieniowa na żywo za pomocą koderów lokalnych przy użyciu witryny Azure Portal | Microsoft Docs"
description: "W tym samouczku opisano kolejne kroki w procesie tworzenia kanału konfigurowanego do dostarczania w formie przekazywania."
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
ms.openlocfilehash: 6939e3b31c3c1b514df4c559c2d9408fce122a4e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-perform-live-streaming-with-on-premises-encoders-using-the-azure-portal"></a><span data-ttu-id="8a943-103">Przeprowadzanie transmisji strumieniowej na żywo za pomocą koderów lokalnych przy użyciu witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8a943-103">How to perform live streaming with on-premises encoders using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8a943-104">Portal</span><span class="sxs-lookup"><span data-stu-id="8a943-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="8a943-105">.NET</span><span class="sxs-lookup"><span data-stu-id="8a943-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="8a943-106">REST</span><span class="sxs-lookup"><span data-stu-id="8a943-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="8a943-107">W tym samouczku opisano kolejne kroki w procesie tworzenia **kanału** skonfigurowanego do dostarczania zawartości w formie przekazywania przy użyciu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8a943-107">This tutorial walks you through the steps of using the Azure portal to create a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8a943-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8a943-108">Prerequisites</span></span>
<span data-ttu-id="8a943-109">Do wykonania czynności przedstawionych w tym samouczku są niezbędne następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8a943-109">The following are required to complete the tutorial:</span></span>

* <span data-ttu-id="8a943-110">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8a943-110">An Azure account.</span></span> <span data-ttu-id="8a943-111">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a943-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="8a943-112">Konto usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="8a943-112">A Media Services account.</span></span> <span data-ttu-id="8a943-113">Aby utworzyć konto usługi Media Services, zobacz temat [Jak utworzyć konto usługi Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="8a943-113">To create a Media Services account, see [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="8a943-114">Kamera internetowa.</span><span class="sxs-lookup"><span data-stu-id="8a943-114">A webcam.</span></span> <span data-ttu-id="8a943-115">Na przykład [koder Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm).</span><span class="sxs-lookup"><span data-stu-id="8a943-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="8a943-116">Zdecydowanie zaleca się następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="8a943-116">It is highly recommended to review the following articles:</span></span>

* [<span data-ttu-id="8a943-117">Obsługa protokołu RTMP i kodery na żywo w usłudze Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="8a943-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="8a943-118">Omówienie transmisji strumieniowej na żywo przy użyciu usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="8a943-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="8a943-119">Transmisja strumieniowa na żywo za pomocą koderów lokalnych tworzących strumienie o różnej szybkości transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="8a943-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="8a943-120"><a id="scenario"></a>Typowy scenariusz transmisji strumieniowej na żywo</span><span class="sxs-lookup"><span data-stu-id="8a943-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="8a943-121">W poniższych krokach opisano zadania związane z tworzeniem typowych aplikacji do transmisji strumieniowej na żywo używających kanałów skonfigurowanych do dostarczania zawartości w formie przekazywania.</span><span class="sxs-lookup"><span data-stu-id="8a943-121">The following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="8a943-122">W tym samouczku przedstawiono sposób tworzenia kanału do przekazywania zawartości i transmitowania wydarzeń na żywo oraz zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="8a943-122">This tutorial shows how to create and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="8a943-123">Upewnij się, że punkt końcowy przesyłania strumieniowego, z którego chcesz strumieniowo przesyłać zawartość, ma stan **Uruchomiony**.</span><span class="sxs-lookup"><span data-stu-id="8a943-123">Make sure the streaming endpoint from which you want to stream content is in the **Running** state.</span></span> 
    
1. <span data-ttu-id="8a943-124">Podłącz kamerę wideo do komputera.</span><span class="sxs-lookup"><span data-stu-id="8a943-124">Connect a video camera to a computer.</span></span> <span data-ttu-id="8a943-125">Uruchom i skonfiguruj lokalny koder na żywo, który wyprowadza strumień protokołu RTMP o różnej szybkości transmisji bitów lub pofragmentowany strumień MP4.</span><span class="sxs-lookup"><span data-stu-id="8a943-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="8a943-126">Aby uzyskać więcej informacji, zobacz temat [Obsługa protokołu RTMP i kodery na żywo w usłudze Azure Media Services](http://go.microsoft.com/fwlink/?LinkId=532824).</span><span class="sxs-lookup"><span data-stu-id="8a943-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="8a943-127">Ten krok można również wykonać po utworzeniu kanału.</span><span class="sxs-lookup"><span data-stu-id="8a943-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="8a943-128">Utwórz i uruchom kanał w formie przekazywania.</span><span class="sxs-lookup"><span data-stu-id="8a943-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="8a943-129">Pobierz adres URL pozyskiwania kanału.</span><span class="sxs-lookup"><span data-stu-id="8a943-129">Retrieve the Channel ingest URL.</span></span> 
   
    <span data-ttu-id="8a943-130">Koder na żywo używa adresu URL pozyskiwania do wysyłania strumienia do kanału.</span><span class="sxs-lookup"><span data-stu-id="8a943-130">The ingest URL is used by the live encoder to send the stream to the Channel.</span></span>
4. <span data-ttu-id="8a943-131">Pobierz adres URL podglądu kanału.</span><span class="sxs-lookup"><span data-stu-id="8a943-131">Retrieve the Channel preview URL.</span></span> 
   
    <span data-ttu-id="8a943-132">Użyj tego adresu URL, aby sprawdzić, czy kanał prawidłowo odbiera strumień na żywo.</span><span class="sxs-lookup"><span data-stu-id="8a943-132">Use this URL to verify that your channel is properly receiving the live stream.</span></span>
5. <span data-ttu-id="8a943-133">Utwórz program lub wydarzenie na żywo.</span><span class="sxs-lookup"><span data-stu-id="8a943-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="8a943-134">W przypadku korzystania z portalu Azure utworzenie wydarzenia na żywo spowoduje również utworzenie elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="8a943-134">When using the Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="8a943-135">Uruchom wydarzenie/program, gdy wszystko będzie gotowe do rozpoczęcia przesyłania strumieniowego i archiwizacji.</span><span class="sxs-lookup"><span data-stu-id="8a943-135">Start the event/program when you are ready to start streaming and archiving.</span></span>
7. <span data-ttu-id="8a943-136">Opcjonalnie można przesłać do kodera na żywo sygnał o rozpoczęciu reklamy.</span><span class="sxs-lookup"><span data-stu-id="8a943-136">Optionally, the live encoder can be signaled to start an advertisement.</span></span> <span data-ttu-id="8a943-137">Reklama jest wstawiana do strumienia wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="8a943-137">The advertisement is inserted in the output stream.</span></span>
8. <span data-ttu-id="8a943-138">Zatrzymaj wydarzenie/program w dowolnym momencie, w którym chcesz zatrzymać przesyłanie strumieniowe i archiwizowanie wydarzenia.</span><span class="sxs-lookup"><span data-stu-id="8a943-138">Stop the event/program whenever you want to stop streaming and archiving the event.</span></span>
9. <span data-ttu-id="8a943-139">Usuń wydarzenie/program (opcjonalnie można również usunąć element zawartości).</span><span class="sxs-lookup"><span data-stu-id="8a943-139">Delete the event/program (and optionally delete the asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="8a943-140">W temacie [Transmisja strumieniowa na żywo za pomocą koderów lokalnych tworzących strumienie o różnej szybkości transmisji bitów](media-services-live-streaming-with-onprem-encoders.md) opisano założenia i zagadnienia dotyczące transmisji strumieniowej na żywo za pomocą koderów lokalnych i kanałów przekazujących.</span><span class="sxs-lookup"><span data-stu-id="8a943-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) to learn about concepts and considerations related to live streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="to-view-notifications-and-errors"></a><span data-ttu-id="8a943-141">Wyświetlanie powiadomień i błędów</span><span class="sxs-lookup"><span data-stu-id="8a943-141">To view notifications and errors</span></span>
<span data-ttu-id="8a943-142">Jeśli chcesz wyświetlić powiadomienia i błędy wygenerowane w portalu Azure, kliknij ikonę Powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="8a943-142">If you want to view notifications and errors produced by the Azure portal, click on the Notification icon.</span></span>

![Powiadomienia](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="8a943-144">Tworzenie i uruchamianie kanałów i wydarzeń w formie przekazywania</span><span class="sxs-lookup"><span data-stu-id="8a943-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="8a943-145">Kanał jest skojarzony z wydarzeniami/programami, które umożliwiają kontrolowanie publikowania i przechowywania segmentów strumienia na żywo.</span><span class="sxs-lookup"><span data-stu-id="8a943-145">A channel is associated with events/programs that enable you to control the publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="8a943-146">Kanały zarządzają wydarzeniami.</span><span class="sxs-lookup"><span data-stu-id="8a943-146">Channels manage events.</span></span> 

<span data-ttu-id="8a943-147">Można określić liczbę godzin, aby zachować zarejestrowaną zawartość na potrzeby programu przez ustawienie długości **Okna archiwum**.</span><span class="sxs-lookup"><span data-stu-id="8a943-147">You can specify the number of hours you want to retain the recorded content for the program by setting the **Archive Window** length.</span></span> <span data-ttu-id="8a943-148">Ta wartość musi mieścić się w zakresie od 5 minut do maksymalnie 25 godzin.</span><span class="sxs-lookup"><span data-stu-id="8a943-148">This value can be set from a minimum of 5 minutes to a maximum of 25 hours.</span></span> <span data-ttu-id="8a943-149">Długość okna archiwum określa również dostępny dla klientów zakres cofania odtwarzania pliku od bieżącego momentu transmisji na żywo.</span><span class="sxs-lookup"><span data-stu-id="8a943-149">Archive window length also dictates the maximum amount of time clients can seek back in time from the current live position.</span></span> <span data-ttu-id="8a943-150">Wydarzenia mogą być uruchamiane w określonym czasie, ale zawartość, która wykracza poza długość okna jest stale odrzucana.</span><span class="sxs-lookup"><span data-stu-id="8a943-150">Events can run over the specified amount of time, but content that falls behind the window length is continuously discarded.</span></span> <span data-ttu-id="8a943-151">Wartość tej właściwości określa również, jak długie mogą być manifesty na kliencie.</span><span class="sxs-lookup"><span data-stu-id="8a943-151">This value of this property also determines how long the client manifests can grow.</span></span>

<span data-ttu-id="8a943-152">Każde wydarzenie jest skojarzone z elementem zawartości.</span><span class="sxs-lookup"><span data-stu-id="8a943-152">Each event is associated with an asset.</span></span> <span data-ttu-id="8a943-153">Aby opublikować wydarzenie, należy utworzyć lokalizator OnDemand dla skojarzonego elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="8a943-153">To publish the event, you must create an OnDemand locator for the associated asset.</span></span> <span data-ttu-id="8a943-154">Lokalizator umożliwia utworzenie adresu URL przesyłania strumieniowego, który można udostępnić klientom.</span><span class="sxs-lookup"><span data-stu-id="8a943-154">Having this locator enables you to build a streaming URL that you can provide to your clients.</span></span>

<span data-ttu-id="8a943-155">Kanał obsługuje maksymalnie trzy jednocześnie uruchomione wydarzenia, dzięki czemu można tworzyć wiele archiwów tego samego strumienia przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="8a943-155">A channel supports up to three concurrently running events so you can create multiple archives of the same incoming stream.</span></span> <span data-ttu-id="8a943-156">Umożliwia to w razie potrzeby publikowanie i archiwizację różnych części wydarzenia.</span><span class="sxs-lookup"><span data-stu-id="8a943-156">This allows you to publish and archive different parts of an event as needed.</span></span> <span data-ttu-id="8a943-157">Na przykład zgodnie z wymaganiami biznesowymi potrzebna jest archiwizacja sześciu godzin programu, ale do emisji przeznaczonych jest tylko ostatnich 10 minut.</span><span class="sxs-lookup"><span data-stu-id="8a943-157">For example, your business requirement is to archive 6 hours of a program, but to broadcast only last 10 minutes.</span></span> <span data-ttu-id="8a943-158">W tym celu należy utworzyć dwa jednocześnie uruchomione programy.</span><span class="sxs-lookup"><span data-stu-id="8a943-158">To accomplish this, you need to create two concurrently running programs.</span></span> <span data-ttu-id="8a943-159">Jeden z programów jest skonfigurowany na potrzeby archiwizacji sześciu godzin zdarzenia, ale ten program nie jest publikowany.</span><span class="sxs-lookup"><span data-stu-id="8a943-159">One program is set to archive 6 hours of the event but the program is not published.</span></span> <span data-ttu-id="8a943-160">Drugi z programów jest skonfigurowany w celu archiwizacji 10 minut wydarzenia i ten program zostanie opublikowany.</span><span class="sxs-lookup"><span data-stu-id="8a943-160">The other program is set to archive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="8a943-161">Istniejących wydarzeń na żywo nie należy używać ponownie.</span><span class="sxs-lookup"><span data-stu-id="8a943-161">You should not reuse existing live events.</span></span> <span data-ttu-id="8a943-162">Zamiast tego należy utworzyć i uruchomić nowe wydarzenie dla każdego wydarzenia.</span><span class="sxs-lookup"><span data-stu-id="8a943-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="8a943-163">Uruchom wydarzenie, gdy wszystko będzie gotowe do rozpoczęcia przesyłania strumieniowego i archiwizacji.</span><span class="sxs-lookup"><span data-stu-id="8a943-163">Start the event when you are ready to start streaming and archiving.</span></span> <span data-ttu-id="8a943-164">Zatrzymaj program w dowolnym momencie, w którym chcesz zatrzymać przesyłanie strumieniowe i archiwizowanie wydarzenia.</span><span class="sxs-lookup"><span data-stu-id="8a943-164">Stop the program whenever you want to stop streaming and archiving the event.</span></span> 

<span data-ttu-id="8a943-165">Aby usunąć zarchiwizowaną zawartość, zatrzymaj i usuń wydarzenie, a następnie usuń skojarzony element zawartości.</span><span class="sxs-lookup"><span data-stu-id="8a943-165">To delete archived content, stop and delete the event and then delete the associated asset.</span></span> <span data-ttu-id="8a943-166">Nie można usunąć elementu zawartości, jeśli jest on używany przez wydarzenie. Najpierw należy usunąć wydarzenie.</span><span class="sxs-lookup"><span data-stu-id="8a943-166">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="8a943-167">Nawet po zatrzymaniu i usunięciu wydarzenia użytkownicy będą mogli przesyłać strumieniowo zarchiwizowaną zawartość wideo na żądanie tak długo, jak zasoby nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="8a943-167">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span>

<span data-ttu-id="8a943-168">Jeśli chcesz zachować zarchiwizowaną zawartość, ale bez udostępniania jej do przesyłania strumieniowego, usuń lokalizator przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="8a943-168">If you do want to retain the archived content, but not have it available for streaming, delete the streaming locator.</span></span>

### <a name="to-use-the-portal-to-create-a-channel"></a><span data-ttu-id="8a943-169">Aby utworzyć kanał za pomocą portalu</span><span class="sxs-lookup"><span data-stu-id="8a943-169">To use the portal to create a channel</span></span>
<span data-ttu-id="8a943-170">W tej sekcji przedstawiono, jak użyć opcji **Szybkie tworzenie** do utworzenia kanału przekazującego.</span><span class="sxs-lookup"><span data-stu-id="8a943-170">This section shows how to use the **Quick Create** option to create a pass-through channel.</span></span>

<span data-ttu-id="8a943-171">Więcej szczegółowych informacji dotyczących kanałów przekazujących można znaleźć w temacie [Transmisja strumieniowa na żywo za pomocą koderów lokalnych tworzących strumienie o różnej szybkości transmisji bitów](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="8a943-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="8a943-172">W witrynie [Azure Portal](https://portal.azure.com/) wybierz swoje konto usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="8a943-172">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="8a943-173">W oknie **Ustawienia** kliknij przycisk **Transmisja strumieniowa na żywo**.</span><span class="sxs-lookup"><span data-stu-id="8a943-173">In the **Settings** window, click **Live streaming**.</span></span> 
   
    ![Wprowadzenie](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="8a943-175">Zostanie wyświetlone okno **Transmisja strumieniowa na żywo**.</span><span class="sxs-lookup"><span data-stu-id="8a943-175">The **Live streaming** window appears.</span></span>
3. <span data-ttu-id="8a943-176">Kliknij przycisk **Szybkie tworzenie**, aby utworzyć kanał w formie przekazywania za pomocą protokołu pozyskiwania RTMP.</span><span class="sxs-lookup"><span data-stu-id="8a943-176">Click **Quick Create** to create a pass-through channel with the RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="8a943-177">Zostanie wyświetlone okno **UTWÓRZ NOWY KANAŁ**.</span><span class="sxs-lookup"><span data-stu-id="8a943-177">The **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="8a943-178">Nadaj nazwę nowemu kanałowi, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8a943-178">Give the new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="8a943-179">Spowoduje to utworzenie kanału przekazującego za pomocą protokołu pozyskiwania RTMP.</span><span class="sxs-lookup"><span data-stu-id="8a943-179">This creates a pass-through channel with the RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="8a943-180">Tworzenie wydarzeń</span><span class="sxs-lookup"><span data-stu-id="8a943-180">Create events</span></span>
1. <span data-ttu-id="8a943-181">Wybierz kanał, do którego chcesz dodać wydarzenie.</span><span class="sxs-lookup"><span data-stu-id="8a943-181">Select a channel to which you want to add an event.</span></span>
2. <span data-ttu-id="8a943-182">Naciśnij przycisk **Wydarzenie na żywo**.</span><span class="sxs-lookup"><span data-stu-id="8a943-182">Press **Live Event** button.</span></span>

![Wydarzenie](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="8a943-184">Pobieranie adresów URL pozyskiwania</span><span class="sxs-lookup"><span data-stu-id="8a943-184">Get ingest URLs</span></span>
<span data-ttu-id="8a943-185">Po utworzeniu kanału można pobrać adresy URL pozyskiwania, które należy udostępnić koderowi na żywo.</span><span class="sxs-lookup"><span data-stu-id="8a943-185">Once the channel is created, you can get ingest URLs that you will provide to the live encoder.</span></span> <span data-ttu-id="8a943-186">Koder używa tych adresów URL do wprowadzenia strumienia na żywo.</span><span class="sxs-lookup"><span data-stu-id="8a943-186">The encoder uses these URLs to input a live stream.</span></span>

![Utworzone](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-the-event"></a><span data-ttu-id="8a943-188">Oglądanie wydarzenia</span><span class="sxs-lookup"><span data-stu-id="8a943-188">Watch the event</span></span>
<span data-ttu-id="8a943-189">Aby oglądać wydarzenie, kliknij przycisk **Oglądaj** w witrynie Azure Portal lub skopiuj adres URL przesyłania strumieniowego i użyj wybranego odtwarzacza.</span><span class="sxs-lookup"><span data-stu-id="8a943-189">To watch the event, click **Watch** in the Azure portal or copy the streaming URL and use a player of your choice.</span></span> 

![Utworzone](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="8a943-191">Po zatrzymaniu wydarzenia na żywo jest ono automatycznie konwertowane na zawartość na żądanie.</span><span class="sxs-lookup"><span data-stu-id="8a943-191">Live event automatically get converted to on-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="8a943-192">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="8a943-192">Clean up</span></span>
<span data-ttu-id="8a943-193">Więcej szczegółowych informacji dotyczących kanałów przekazujących można znaleźć w temacie [Transmisja strumieniowa na żywo za pomocą koderów lokalnych tworzących strumienie o różnej szybkości transmisji bitów](media-services-live-streaming-with-onprem-encoders.md).</span><span class="sxs-lookup"><span data-stu-id="8a943-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="8a943-194">Kanał można zatrzymać tylko wtedy, jeśli wszystkie wydarzenia/programy na kanale zostały zatrzymane.</span><span class="sxs-lookup"><span data-stu-id="8a943-194">A channel can be stopped only when all events/programs on the channel have been stopped.</span></span>  <span data-ttu-id="8a943-195">Po zatrzymaniu kanału opłaty nie są naliczane.</span><span class="sxs-lookup"><span data-stu-id="8a943-195">Once the Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="8a943-196">W razie potrzeby ponownego uruchomienia kanał będzie miał ten sam adres URL pozyskiwania, więc nie trzeba będzie ponownie konfigurować kodera.</span><span class="sxs-lookup"><span data-stu-id="8a943-196">When you need to start it again, it will have the same ingest URL so you won't need to reconfigure your encoder.</span></span>
* <span data-ttu-id="8a943-197">Kanał można usunąć tylko wtedy, gdy wszystkie wydarzenia na żywo na kanale zostały usunięte.</span><span class="sxs-lookup"><span data-stu-id="8a943-197">A channel can be deleted only when all live events on the channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="8a943-198">Wyświetlanie zarchiwizowanej zawartości</span><span class="sxs-lookup"><span data-stu-id="8a943-198">View archived content</span></span>
<span data-ttu-id="8a943-199">Nawet po zatrzymaniu i usunięciu wydarzenia użytkownicy będą mogli przesyłać strumieniowo zarchiwizowaną zawartość wideo na żądanie tak długo, jak zasoby nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="8a943-199">Even after you stop and delete the event, the users would be able to stream your archived content as a video on demand, for as long as you do not delete the asset.</span></span> <span data-ttu-id="8a943-200">Nie można usunąć elementu zawartości, jeśli jest on używany przez wydarzenie. Najpierw należy usunąć wydarzenie.</span><span class="sxs-lookup"><span data-stu-id="8a943-200">An asset cannot be deleted if it is used by an event; the event must be deleted first.</span></span> 

<span data-ttu-id="8a943-201">Aby zarządzać elementami zawartości, wybierz pozycję **Ustawienie** i kliknij przycisk **Elementy zawartości**.</span><span class="sxs-lookup"><span data-stu-id="8a943-201">To manage your assets, select **Setting** and click **Assets**.</span></span>

![Elementy zawartości](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="8a943-203">Następny krok</span><span class="sxs-lookup"><span data-stu-id="8a943-203">Next step</span></span>
<span data-ttu-id="8a943-204">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="8a943-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8a943-205">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="8a943-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

