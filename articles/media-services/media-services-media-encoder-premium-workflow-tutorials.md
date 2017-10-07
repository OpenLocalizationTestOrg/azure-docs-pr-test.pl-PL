---
title: "Samouczki Media Encoder Premium w przepływie pracy aaaAvanced"
description: "Ten dokument zawiera wskazówki, które pokazują, jak tooperform zaawansowanych zadań z przepływem pracy Premium koder nośników, a także sposób toocreate złożonych przepływów pracy za pomocą projektanta przepływów pracy."
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a><span data-ttu-id="5d08e-103">Zaawansowane samouczki Media Encoder Premium w przepływie pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-103">Advanced Media Encoder Premium Workflow tutorials</span></span>
## <a name="overview"></a><span data-ttu-id="5d08e-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="5d08e-104">Overview</span></span>
<span data-ttu-id="5d08e-105">Ten dokument zawiera wskazówki, które pokazują jak przepływów toocustomize z **projektanta przepływów pracy**.</span><span class="sxs-lookup"><span data-stu-id="5d08e-105">This document contains walkthroughs that show how toocustomize workflows with  **Workflow Designer**.</span></span> <span data-ttu-id="5d08e-106">Pliki można znaleźć hello rzeczywiste przepływu pracy [tutaj](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span><span class="sxs-lookup"><span data-stu-id="5d08e-106">You can find hello actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span></span>  

## <a name="toc"></a><span data-ttu-id="5d08e-107">SPIS TREŚCI</span><span class="sxs-lookup"><span data-stu-id="5d08e-107">TOC</span></span>
<span data-ttu-id="5d08e-108">obejmuje Hello następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="5d08e-108">hello following topics are covered:</span></span>

* [<span data-ttu-id="5d08e-109">Kodowanie MXF do pojedynczej szybkości transmisji bitów MP4</span><span class="sxs-lookup"><span data-stu-id="5d08e-109">Encoding MXF into a single bitrate MP4</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [<span data-ttu-id="5d08e-110">Uruchamianie nowego przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-110">Starting a new workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [<span data-ttu-id="5d08e-111">Przy użyciu hello wejście pliku multimediów</span><span class="sxs-lookup"><span data-stu-id="5d08e-111">Using hello Media File Input</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [<span data-ttu-id="5d08e-112">Zapoznanie się strumieni nośnika</span><span class="sxs-lookup"><span data-stu-id="5d08e-112">Inspecting media streams</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [<span data-ttu-id="5d08e-113">Dodawanie koder wideo dla. Generowanie pliku MP4</span><span class="sxs-lookup"><span data-stu-id="5d08e-113">Adding a video encoder for .MP4 file generation</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [<span data-ttu-id="5d08e-114">Kodowania hello strumieniem audio</span><span class="sxs-lookup"><span data-stu-id="5d08e-114">Encoding hello audio stream</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [<span data-ttu-id="5d08e-115">Strumienie multipleksowania Audio i wideo do kontenera MP4</span><span class="sxs-lookup"><span data-stu-id="5d08e-115">Multiplexing Audio and Video streams into an MP4 container</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [<span data-ttu-id="5d08e-116">Zapisywanie pliku MP4 hello</span><span class="sxs-lookup"><span data-stu-id="5d08e-116">Writing hello MP4 file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [<span data-ttu-id="5d08e-117">Tworzenie zasobów usługi multimediów z pliku wyjściowego hello</span><span class="sxs-lookup"><span data-stu-id="5d08e-117">Creating a Media Services Asset from hello output file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [<span data-ttu-id="5d08e-118">Test hello Zakończono lokalnie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-118">Test hello finished workflow locally</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [<span data-ttu-id="5d08e-119">Kodowanie MXF do multibitrate MP4s - dynamicznego tworzenia pakietów włączone</span><span class="sxs-lookup"><span data-stu-id="5d08e-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [<span data-ttu-id="5d08e-120">Dodanie jednego lub więcej dodatkowych danych wyjściowych MP4</span><span class="sxs-lookup"><span data-stu-id="5d08e-120">Adding one or more additional MP4 outputs</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [<span data-ttu-id="5d08e-121">Konfigurowanie nazwy wyjściowego pliku hello</span><span class="sxs-lookup"><span data-stu-id="5d08e-121">Configuring hello file output names</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [<span data-ttu-id="5d08e-122">Dodawanie oddzielne ścieżkę Audio</span><span class="sxs-lookup"><span data-stu-id="5d08e-122">Adding a separate Audio Track</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [<span data-ttu-id="5d08e-123">Dodawanie hello. Plik SMIL ISM</span><span class="sxs-lookup"><span data-stu-id="5d08e-123">Adding hello .ISM SMIL File</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [<span data-ttu-id="5d08e-124">Kodowanie MXF do multibitrate MP4 — rozszerzone planu</span><span class="sxs-lookup"><span data-stu-id="5d08e-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [<span data-ttu-id="5d08e-125">Tooenhance omówienie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-125">Workflow overview tooenhance</span></span>](#workflow-overview-to-enhance)
  * [<span data-ttu-id="5d08e-126">Konwencje nazewnictwa plików</span><span class="sxs-lookup"><span data-stu-id="5d08e-126">File Naming Conventions</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [<span data-ttu-id="5d08e-127">Właściwości składnika publikacji na powitania głównego przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-127">Publishing component properties onto hello workflow root</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [<span data-ttu-id="5d08e-128">Wygenerowano plik wyjściowy, który nazwy zależne od wartości właściwości opublikowanych</span><span class="sxs-lookup"><span data-stu-id="5d08e-128">Have generated output file names rely on published property values</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [<span data-ttu-id="5d08e-129">Dodawanie danych wyjściowych MP4 toomultibitrate miniatur</span><span class="sxs-lookup"><span data-stu-id="5d08e-129">Adding thumbnails toomultibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [<span data-ttu-id="5d08e-130">Miniatur tooadd omówienie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-130">Workflow overview tooadd thumbnails to</span></span>](#workflow-overview-to-add-thumbnails-to)
  * [<span data-ttu-id="5d08e-131">Dodawanie kodowania JPG</span><span class="sxs-lookup"><span data-stu-id="5d08e-131">Adding JPG Encoding</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [<span data-ttu-id="5d08e-132">Zajmujących się konwersji przestrzeń kolorów</span><span class="sxs-lookup"><span data-stu-id="5d08e-132">Dealing with Color Space conversion</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [<span data-ttu-id="5d08e-133">Zapisywanie hello miniatur</span><span class="sxs-lookup"><span data-stu-id="5d08e-133">Writing hello thumbnails</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [<span data-ttu-id="5d08e-134">Wykrywanie błędów w przepływie pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-134">Detecting errors in a workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [<span data-ttu-id="5d08e-135">Zakończono przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-135">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [<span data-ttu-id="5d08e-136">Na podstawie czasu przycinanie multibitrate MP4 danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="5d08e-136">Time-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [<span data-ttu-id="5d08e-137">Dodawanie przycinanie do toostart omówienie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-137">Workflow overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [<span data-ttu-id="5d08e-138">Przy użyciu hello przycinarka strumienia</span><span class="sxs-lookup"><span data-stu-id="5d08e-138">Using hello Stream Trimmer</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [<span data-ttu-id="5d08e-139">Zakończono przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-139">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [<span data-ttu-id="5d08e-140">Wprowadzenie hello składnika uwzględnione w skryptach</span><span class="sxs-lookup"><span data-stu-id="5d08e-140">Introducing hello Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [<span data-ttu-id="5d08e-141">Obsługa skryptów w ramach przepływu pracy: Witaj świecie</span><span class="sxs-lookup"><span data-stu-id="5d08e-141">Scripting within a workflow: hello world</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [<span data-ttu-id="5d08e-142">Przycinanie multibitrate MP4 dane wyjściowe na podstawie ramki</span><span class="sxs-lookup"><span data-stu-id="5d08e-142">Frame-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [<span data-ttu-id="5d08e-143">Omówienie toostart Dodawanie przycinanie do planu</span><span class="sxs-lookup"><span data-stu-id="5d08e-143">Blueprint overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [<span data-ttu-id="5d08e-144">Przy użyciu hello klip listy XML</span><span class="sxs-lookup"><span data-stu-id="5d08e-144">Using hello Clip List XML</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [<span data-ttu-id="5d08e-145">Modyfikowanie listy klip hello ze składnika uwzględnione w skryptach</span><span class="sxs-lookup"><span data-stu-id="5d08e-145">Modifying hello clip list from a Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [<span data-ttu-id="5d08e-146">Dodawanie właściwości wygody ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="5d08e-146">Adding a ClippingEnabled convenience property</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <span data-ttu-id="5d08e-147"><a id="MXF_to_MP4"></a>Kodowanie MXF do pojedynczej szybkości transmisji bitów MP4</span><span class="sxs-lookup"><span data-stu-id="5d08e-147"><a id="MXF_to_MP4"></a>Encoding MXF into a single bitrate MP4</span></span>
<span data-ttu-id="5d08e-148">W tym przewodniku utworzymy o pojedynczej szybkości transmisji bitów. Plik MP4 o AAC-HE zakodowane audio z. Plik wejściowy MXF.</span><span class="sxs-lookup"><span data-stu-id="5d08e-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span></span>

### <span data-ttu-id="5d08e-149"><a id="MXF_to_MP4_start_new"></a>Uruchamianie nowego przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-149"><a id="MXF_to_MP4_start_new"></a>Starting a new workflow</span></span>
<span data-ttu-id="5d08e-150">Otwórz projektanta przepływów pracy i wybierz pozycję "Planu Transkodowanie pliku"-"nowy obszar roboczy"-""</span><span class="sxs-lookup"><span data-stu-id="5d08e-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span></span>

<span data-ttu-id="5d08e-151">Witaj nowego przepływu pracy będą wyświetlane 3 elementów:</span><span class="sxs-lookup"><span data-stu-id="5d08e-151">hello new workflow will show 3 elements:</span></span>

* <span data-ttu-id="5d08e-152">Podstawowym pliku źródłowym</span><span class="sxs-lookup"><span data-stu-id="5d08e-152">Primary Source File</span></span>
* <span data-ttu-id="5d08e-153">Obcina listę XML</span><span class="sxs-lookup"><span data-stu-id="5d08e-153">Clip List XML</span></span>
* <span data-ttu-id="5d08e-154">Zawartości pliku wyjściowej</span><span class="sxs-lookup"><span data-stu-id="5d08e-154">Output File/Asset</span></span>  

![Nowy przepływ pracy kodowania](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

<span data-ttu-id="5d08e-156">*Nowy przepływ pracy kodowania*</span><span class="sxs-lookup"><span data-stu-id="5d08e-156">*New Encoding Workflow*</span></span>

### <span data-ttu-id="5d08e-157"><a id="MXF_to_MP4_with_file_input"></a>Przy użyciu hello wejście pliku multimediów</span><span class="sxs-lookup"><span data-stu-id="5d08e-157"><a id="MXF_to_MP4_with_file_input"></a>Using hello Media File Input</span></span>
<span data-ttu-id="5d08e-158">W kolejności tooaccept naszych wejściowy plik jedną rozpoczyna się od dodawania składnika nośnika pliku wejściowego.</span><span class="sxs-lookup"><span data-stu-id="5d08e-158">In order tooaccept our input media file, one starts with adding a Media File Input component.</span></span> <span data-ttu-id="5d08e-159">tooadd przepływu pracy toohello składnika, poszukaj jej w polu wyszukiwania w repozytorium hello i przeciągnij hello potrzeby wpis na hello okienku projektanta.</span><span class="sxs-lookup"><span data-stu-id="5d08e-159">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span> <span data-ttu-id="5d08e-160">Wykonaj dla hello nośnika pliku wejściowego i połączyć hello podstawowy plik źródłowy składnika toohello Filename wprowadzania numeru pin z hello nośnika pliku wejściowego.</span><span class="sxs-lookup"><span data-stu-id="5d08e-160">Do this for hello Media File Input and connect hello Primary Source File component toohello Filename input pin from hello Media File Input.</span></span>

![Pliku multimedialnego połączonych danych wejściowych](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

<span data-ttu-id="5d08e-162">*Pliku multimedialnego połączonych danych wejściowych*</span><span class="sxs-lookup"><span data-stu-id="5d08e-162">*Connected Media File Input*</span></span>

<span data-ttu-id="5d08e-163">Zanim przejdziemy wiele więcej, musisz najpierw projektanta przepływów pracy toohello tooindicate jakie przykładowy plik chcielibyśmy toouse toodesign naszych przepływu pracy z.</span><span class="sxs-lookup"><span data-stu-id="5d08e-163">Before we can do much else, we'll first need tooindicate toohello workflow designer what sample file we'd like toouse toodesign our workflow with.</span></span> <span data-ttu-id="5d08e-164">toodo tak, kliknij przycisk hello tła okienka projektanta i poszukaj hello właściwości głównej pliku źródłowego w okienku po prawej stronie właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-164">toodo so, click hello designer pane background and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="5d08e-165">Kliknij ikonę folderu hello i przepływ pracy hello tootest pliku hello wybierz żądany z.</span><span class="sxs-lookup"><span data-stu-id="5d08e-165">Click hello folder icon and select hello desired file tootest hello workflow with.</span></span> <span data-ttu-id="5d08e-166">Natychmiast po zakończeniu hello wejściowy plik nośnika składnik będzie sprawdzenie pliku hello i wypełnić jego dane wyjściowe numerów PIN tooreflect hello plik, który go inspekcji.</span><span class="sxs-lookup"><span data-stu-id="5d08e-166">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file it inspected.</span></span>

![Dane wejściowe pliku multimedialnego wypełnione](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

<span data-ttu-id="5d08e-168">*Dane wejściowe pliku multimedialnego wypełnione*</span><span class="sxs-lookup"><span data-stu-id="5d08e-168">*Populated Media File Input*</span></span>

<span data-ttu-id="5d08e-169">Gdy to określa co wejściowej chcielibyśmy toowork z, program nie nakazuje jeszcze gdzie hello kodowane dane wyjściowe powinny przejdź do.</span><span class="sxs-lookup"><span data-stu-id="5d08e-169">While this specifies with what input we'd like toowork with, it doesn't tell yet where hello encoded output should go to.</span></span> <span data-ttu-id="5d08e-170">Podobne powitalne toohow podstawowy plik źródłowy został skonfigurowany, skonfiguruj teraz hello właściwość zmiennej folderu wyjściowego, tuż pod.</span><span class="sxs-lookup"><span data-stu-id="5d08e-170">Similar toohow hello Primary Source File was configured, now configure hello Output Folder Variable property, just below it.</span></span>

![Skonfigurowanych właściwości dane wejściowe i wyjściowe](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

<span data-ttu-id="5d08e-172">*Skonfigurowanych właściwości dane wejściowe i wyjściowe*</span><span class="sxs-lookup"><span data-stu-id="5d08e-172">*Configured Input and Output properties*</span></span>

### <span data-ttu-id="5d08e-173"><a id="MXF_to_MP4_streams"></a>Zapoznanie się strumieni nośnika</span><span class="sxs-lookup"><span data-stu-id="5d08e-173"><a id="MXF_to_MP4_streams"></a>Inspecting media streams</span></span>
<span data-ttu-id="5d08e-174">Często jest potrzebne, że tooknow tak jak wygląd strumienia hello przechodzi przez hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="5d08e-174">Often it's desired tooknow how hello stream looks like that flows through hello workflow.</span></span> <span data-ttu-id="5d08e-175">tooinspect strumienia w dowolnym momencie w przepływie pracy hello, wystarczy kliknąć danych wyjściowych lub wejściowych numeru pin na dowolnym hello składników.</span><span class="sxs-lookup"><span data-stu-id="5d08e-175">tooinspect a stream at any point in hello workflow, just click an output or input pin on any of hello components.</span></span> <span data-ttu-id="5d08e-176">W takim przypadku spróbuj kliknięcie hello końcówka wyjściowa nieskompresowanym wideo z naszych danych wejściowych pliku nośnika.</span><span class="sxs-lookup"><span data-stu-id="5d08e-176">In this case, try clicking on hello Uncompressed Video output pin from our Media File Input.</span></span> <span data-ttu-id="5d08e-177">Okno dialogowe będzie otwarcie umożliwiający tooinspect hello wychodzącego wideo.</span><span class="sxs-lookup"><span data-stu-id="5d08e-177">A dialog will open up that allows tooinspect hello outbound video.</span></span>

![Zapoznanie się hello wideo nieskompresowanych danych wyjściowych numeru pin](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

<span data-ttu-id="5d08e-179">*Zapoznanie się hello wideo nieskompresowanych danych wyjściowych numeru pin*</span><span class="sxs-lookup"><span data-stu-id="5d08e-179">*Inspecting hello Uncompressed Video output pin*</span></span>

<span data-ttu-id="5d08e-180">W tym przypadku informuje nas na przykład czy możemy Cię zajmujących się wprowadzania 1920 x 1080 pikseli na 24 klatek na sekundę w 4: próbkowania 2:2 film prawie 2 minuty.</span><span class="sxs-lookup"><span data-stu-id="5d08e-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span></span>

### <span data-ttu-id="5d08e-181"><a id="MXF_to_MP4_file_generation"></a>Dodawanie koder wideo dla. Generowanie pliku MP4</span><span class="sxs-lookup"><span data-stu-id="5d08e-181"><a id="MXF_to_MP4_file_generation"></a>Adding a video encoder for .MP4 file generation</span></span>
<span data-ttu-id="5d08e-182">Należy pamiętać, że teraz, wiele końcówek wyjściowych nieskompresowanych Audio i wideo nieskompresowanych są dostępne do użycia w naszym wejście pliku nośnika.</span><span class="sxs-lookup"><span data-stu-id="5d08e-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span></span> <span data-ttu-id="5d08e-183">W kolejności tooencode hello przychodzących wideo, w tym przypadku należy kodowania składnika - generowania. Pliki mp4.</span><span class="sxs-lookup"><span data-stu-id="5d08e-183">In order tooencode hello inbound video, we need an encoding component - in this case for generating .MP4 files.</span></span>

<span data-ttu-id="5d08e-184">tooencode hello tooH.264 strumienia wideo, dodać powierzchni projektanta składników toohello hello AVC koder wideo.</span><span class="sxs-lookup"><span data-stu-id="5d08e-184">tooencode hello video stream tooH.264, add hello AVC Video Encoder component toohello designer surface.</span></span> <span data-ttu-id="5d08e-185">Ten składnik przyjmuje Dekompresuj strumienia wideo o jako dane wejściowe, a następnie dostarcza AVC skompresowanego strumienia wideo na jego końcówka wyjściowa.</span><span class="sxs-lookup"><span data-stu-id="5d08e-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span></span>

![Odłączony kodera AVC](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

<span data-ttu-id="5d08e-187">*Odłączony kodera AVC*</span><span class="sxs-lookup"><span data-stu-id="5d08e-187">*Unconnected AVC Encoder*</span></span>

<span data-ttu-id="5d08e-188">Jego właściwości określają, jak dokładnie kodowanie hello wykonywana.</span><span class="sxs-lookup"><span data-stu-id="5d08e-188">Its properties determine how hello encoding exactly happens.</span></span> <span data-ttu-id="5d08e-189">Załóżmy ma informacje o niektórych hello ważniejsze ustawienia:</span><span class="sxs-lookup"><span data-stu-id="5d08e-189">Let's have a look at some of hello more important settings:</span></span>

* <span data-ttu-id="5d08e-190">Dane wyjściowe szerokości i wysokości danych wyjściowych: je określić rozdzielczość hello hello zakodowane wideo.</span><span class="sxs-lookup"><span data-stu-id="5d08e-190">Output width and Output height: these determine hello resolution of hello encoded video.</span></span> <span data-ttu-id="5d08e-191">W tym przypadku Użyjmy 640 x 360</span><span class="sxs-lookup"><span data-stu-id="5d08e-191">In our case let's go with 640x360</span></span>
* <span data-ttu-id="5d08e-192">Szybkość klatek: toopassthrough zestaw, który będzie po prostu przyjmuje szybkość klatek hello źródła, jest możliwe toooverride takim jednak.</span><span class="sxs-lookup"><span data-stu-id="5d08e-192">Frame Rate: when set toopassthrough it will just adopt hello source frame rate, it's possible toooverride this though.</span></span> <span data-ttu-id="5d08e-193">Należy pamiętać, że takie konwersji szybkość klatek jest nie ruchu — równoważone.</span><span class="sxs-lookup"><span data-stu-id="5d08e-193">Note that such framerate conversion is not motion-compensated.</span></span>
* <span data-ttu-id="5d08e-194">Profil i poziom: te określenia profilu hello AVC i poziom.</span><span class="sxs-lookup"><span data-stu-id="5d08e-194">Profile and Level: these determine hello AVC profile and level.</span></span> <span data-ttu-id="5d08e-195">tooconveniently uzyskać więcej informacji o różnych poziomach hello i profile, kliknij ikonę znaku zapytania hello na powitania koder wideo AVC składnika i strona pomocy hello wyświetli szczegółowe informacje o każdym z poziomów hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-195">tooconveniently get more information about hello different levels and profiles, click hello question mark icon on hello AVC Video Encoder component and hello help page will show more detail about each of hello levels.</span></span> <span data-ttu-id="5d08e-196">Dla naszej próbki Użyjmy Main profilu na poziomie 3.2 (domyślnie: hello).</span><span class="sxs-lookup"><span data-stu-id="5d08e-196">For our sample, let's go with Main Profile at level 3.2 (hello default).</span></span>
* <span data-ttu-id="5d08e-197">Oceń tryb kontroli i szybkości transmisji bitów (KB/s): w naszym scenariuszu będziemy wybrać stałej szybkości transmisji bitów (CBR) dane wyjściowe w 1200 kb/s</span><span class="sxs-lookup"><span data-stu-id="5d08e-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span></span>
* <span data-ttu-id="5d08e-198">Format wideo: jest to o hello VUI (wideo użyteczność informacje) pobiera zapisywane do strumienia H.264 hello (dekodowania informacji po stronie, które mogą być używane przez wyświetlanie hello tooenhance dekoder, ale nie są niezbędne toocorrectly):</span><span class="sxs-lookup"><span data-stu-id="5d08e-198">Video Format: this is about hello VUI (Video Usability Information) that gets written into hello H.264 stream (side information that might be used by a decoder tooenhance hello display but not essential toocorrectly decode):</span></span>
* <span data-ttu-id="5d08e-199">NTSC (typowa dla Stanów Zjednoczonych lub Japonii przy użyciu 30 kl. / s)</span><span class="sxs-lookup"><span data-stu-id="5d08e-199">NTSC (typical for US or Japan, using 30 fps)</span></span>
* <span data-ttu-id="5d08e-200">PAL (typowa dla Europy, przy użyciu 25 kl. / s)</span><span class="sxs-lookup"><span data-stu-id="5d08e-200">PAL (typical for Europe, using 25 fps)</span></span>
* <span data-ttu-id="5d08e-201">Tryb rozmiaru GOP: skonfigurujemy o stałym rozmiarze GOP dla naszych celów z klucza interwałem równym 2 sekundy z GOPs zamknięte.</span><span class="sxs-lookup"><span data-stu-id="5d08e-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span></span> <span data-ttu-id="5d08e-202">To zapewnia zgodność z hello, który udostępnia funkcję dynamicznego tworzenia pakietów usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="5d08e-202">This ensures compatibility with hello dynamic packaging Azure Media Services provides.</span></span>

<span data-ttu-id="5d08e-203">toofeed naszych kodera AVC połączyć końcówka wyjściowa hello nieskompresowanym wideo z hello nośnika pliku wejściowego składnika toohello nieskompresowanym wideo wprowadzania numeru pin z hello AVC kodera.</span><span class="sxs-lookup"><span data-stu-id="5d08e-203">toofeed our AVC encoder, connect hello Uncompressed Video output pin from hello Media File Input component toohello Uncompressed Video input pin from hello AVC encoder.</span></span>

![Połączone kodera AVC](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

<span data-ttu-id="5d08e-205">*Połączone kodera AVC Main*</span><span class="sxs-lookup"><span data-stu-id="5d08e-205">*Connected AVC Main encoder*</span></span>

### <span data-ttu-id="5d08e-206"><a id="MXF_to_MP4_audio"></a>Kodowania hello strumieniem audio</span><span class="sxs-lookup"><span data-stu-id="5d08e-206"><a id="MXF_to_MP4_audio"></a>Encoding hello audio stream</span></span>
<span data-ttu-id="5d08e-207">Na tym etapie firma Microsoft, są zakodowane wideo, ale hello oryginalnego strumieniem audio nieskompresowanych nadal wymaga toobe skompresowane.</span><span class="sxs-lookup"><span data-stu-id="5d08e-207">At this point, we have encoded video but hello original uncompressed audio stream still needs toobe compressed.</span></span> <span data-ttu-id="5d08e-208">W tym znajdują się z AAC kodowania hello składnika kodera AAC (Dolby).</span><span class="sxs-lookup"><span data-stu-id="5d08e-208">For this we'll go with AAC encoding by hello AAC Encoder (Dolby) component.</span></span> <span data-ttu-id="5d08e-209">Dodaj toohello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="5d08e-209">Add it toohello workflow.</span></span>

![Odłączony kodera AVC](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

<span data-ttu-id="5d08e-211">*Odłączony AAC kodera*</span><span class="sxs-lookup"><span data-stu-id="5d08e-211">*Unconnected AAC encoder*</span></span>

<span data-ttu-id="5d08e-212">Teraz występuje niezgodność: istnieje tylko jeden nieskompresowanych audio wprowadzania numeru pin z hello kodera AAC podczas więcej niż prawdopodobnie hello nośnika plik wejściowy ma dwa różne nieskompresowane strumieniem audio dostępne: jeden dla hello lewego kanału audio i jeden dla hello prawo.</span><span class="sxs-lookup"><span data-stu-id="5d08e-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from hello AAC Encoder while more than likely hello Media File Input will have two different uncompressed audio stream available: one for hello left audio channel and one for hello right.</span></span> <span data-ttu-id="5d08e-213">(Jeśli jest zajmujących dźwięk przestrzenny, który jest kanały 6). Dlatego nie jest możliwe toodirectly połączenie z hello audio ze źródła danych wejściowych plików nośnika hello kodera audio AAC hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible toodirectly connect hello audio from hello Media File Input source into hello AAC audio encoder.</span></span> <span data-ttu-id="5d08e-214">Witaj składnika AAC oczekuje tak zwane "przeplotem" strumieniem audio: pojedynczy strumień, który ma zarówno atrybut hello po lewej i hello kanały prawo przeplatana ze sobą.</span><span class="sxs-lookup"><span data-stu-id="5d08e-214">hello AAC component expects a so-called "interleaved" audio stream: a single stream that has both hello left and hello right channels interleaved with each other.</span></span> <span data-ttu-id="5d08e-215">Po wiemy z naszych pliku nośnika źródłowego które ścieżki audio na pozycji w źródle hello firma Microsoft może wygenerować takie przeplotem strumieniem audio z hello poprawnie przypisano prelegenta pozycji lewy i prawy.</span><span class="sxs-lookup"><span data-stu-id="5d08e-215">Once we know from our source media file which audio tracks are on what position in hello source, we can generate such interleaved audio stream with hello correctly assigned speaker positions for left and right.</span></span>

<span data-ttu-id="5d08e-216">Najpierw należy jedną toogenerated przeplotem strumienia z hello wymagane źródła audio kanałów.</span><span class="sxs-lookup"><span data-stu-id="5d08e-216">First one will want toogenerated an interleaved stream from hello required source audio channels.</span></span> <span data-ttu-id="5d08e-217">składnik Interleaver strumień Audio Hello obsłuży to firmie Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5d08e-217">hello Audio Stream Interleaver component will handle this for us.</span></span> <span data-ttu-id="5d08e-218">Dodaj ją toohello przepływu pracy i połącz dane wyjściowe audio hello z hello wejście pliku multimediów do niego.</span><span class="sxs-lookup"><span data-stu-id="5d08e-218">Add it toohello workflow and connect hello audio outputs from hello Media File Input into it.</span></span>

![Połączone Interleaver strumieniem Audio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

<span data-ttu-id="5d08e-220">*Połączone Interleaver strumieniem Audio*</span><span class="sxs-lookup"><span data-stu-id="5d08e-220">*Connected Audio Stream Interleaver*</span></span>

<span data-ttu-id="5d08e-221">Teraz, gdy mamy przeplotem strumieniem audio, będziemy nadal nie określić gdzie tooassign hello lewego lub prawego osoby mówiącej pozycji.</span><span class="sxs-lookup"><span data-stu-id="5d08e-221">Now that we have an interleaved audio stream, we still didn't specify where tooassign hello left or right speaker positions to.</span></span> <span data-ttu-id="5d08e-222">To zamówienie toospecify, możemy wykorzystać hello Assigner stanowisko osoby mówiącej.</span><span class="sxs-lookup"><span data-stu-id="5d08e-222">In order toospecify this, we can leverage hello Speaker Position Assigner.</span></span>

![Dodawanie Assigner stanowisko osoby mówiącej](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

<span data-ttu-id="5d08e-224">*Dodawanie Assigner stanowisko osoby mówiącej*</span><span class="sxs-lookup"><span data-stu-id="5d08e-224">*Adding a Speaker Position Assigner*</span></span>

<span data-ttu-id="5d08e-225">Skonfigurować hello Assigner stanowisko osoby mówiącej do użycia przy użyciu stereo strumień wejściowy za pomocą kodera ustawień wstępnych filtru "Custom" i hello kanału ustawień o nazwie "2.0 (L, R)".</span><span class="sxs-lookup"><span data-stu-id="5d08e-225">Configure hello Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and hello Channel Preset called "2.0 (L,R)".</span></span> <span data-ttu-id="5d08e-226">(Spowoduje to przypisanie hello prelegenta po lewej stronie pozycji toochannel 1 i hello prelegenta prawa pozycja toochannel 2.)</span><span class="sxs-lookup"><span data-stu-id="5d08e-226">(This will assign hello left speaker position toochannel 1 and hello right speaker position toochannel 2.)</span></span>

<span data-ttu-id="5d08e-227">Połącz dane wyjściowe hello hello Assigner stanowisko osoby mówiącej toohello danych wejściowych hello AAC kodera.</span><span class="sxs-lookup"><span data-stu-id="5d08e-227">Connect hello output of hello Speaker Position Assigner toohello input of hello AAC Encoder.</span></span> <span data-ttu-id="5d08e-228">Następnie należy wskazać toowork kodera AAC hello "2.0 (L, R)" zdefiniowane kanału, który będzie wówczas traktował toodeal stereo dźwięku jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="5d08e-228">Then, tell hello AAC Encoder toowork with a "2.0 (L,R)" Channel Preset, so it knows toodeal with stereo audio as input.</span></span>

### <span data-ttu-id="5d08e-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Strumienie multipleksowania Audio i wideo do kontenera MP4</span><span class="sxs-lookup"><span data-stu-id="5d08e-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing Audio and Video streams into an MP4 container</span></span>
<span data-ttu-id="5d08e-230">Podany naszych AVC zakodowanego strumienia wideo i naszych AAC zakodowane strumieniem audio, firma Microsoft może zarówno do przechwytywania. Kontener MP4.</span><span class="sxs-lookup"><span data-stu-id="5d08e-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span></span> <span data-ttu-id="5d08e-231">proces Hello łączenie różnych strumieni w jedno jest nazywany "Multipleksowanie" (lub "muxing").</span><span class="sxs-lookup"><span data-stu-id="5d08e-231">hello process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span></span> <span data-ttu-id="5d08e-232">W takim przypadku możemy Cię z przeplotem hello audio i wideo strumieni hello w jednej spójnej. Pakiet MP4.</span><span class="sxs-lookup"><span data-stu-id="5d08e-232">In this case we're interleaving hello audio and hello video streams in a single coherent .MP4 package.</span></span> <span data-ttu-id="5d08e-233">Hello składnik, który koordynuje ten formularz. Kontener MP4 jest nazywany hello multiplekser ISO MPEG-4.</span><span class="sxs-lookup"><span data-stu-id="5d08e-233">hello component that coordinates this for an .MP4 container is called hello ISO MPEG-4 Multiplexer.</span></span> <span data-ttu-id="5d08e-234">Dodaj jeden toohello powierzchni projektanta i połącz zarówno hello koder wideo AVC i hello kodera AAC tooits w danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="5d08e-234">Add one toohello designer surface and connect both hello AVC Video Encoder and hello AAC Encoder tooits inputs.</span></span>

![Połączone MPEG4 multiplekser](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

<span data-ttu-id="5d08e-236">*Połączone MPEG4 multiplekser*</span><span class="sxs-lookup"><span data-stu-id="5d08e-236">*Connected MPEG4 Multiplexer*</span></span>

### <span data-ttu-id="5d08e-237"><a id="MXF_to_MP4_writing_mp4"></a>Zapisywanie pliku MP4 hello</span><span class="sxs-lookup"><span data-stu-id="5d08e-237"><a id="MXF_to_MP4_writing_mp4"></a>Writing hello MP4 file</span></span>
<span data-ttu-id="5d08e-238">Podczas zapisywania pliku wyjściowego, składnik dane wyjściowe pliku hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="5d08e-238">When writing an output file, hello File Output component is used.</span></span> <span data-ttu-id="5d08e-239">Możemy połączyć się z tym toohello dane wyjściowe hello multiplekser ISO MPEG-4, tak, aby jego dane wyjściowe pobiera zapisywane toodisk.</span><span class="sxs-lookup"><span data-stu-id="5d08e-239">We can connect this toohello output of hello ISO MPEG-4 Multiplexer so that its output gets written toodisk.</span></span> <span data-ttu-id="5d08e-240">toodo, Połącz hello kontenera (MPEG-4) dane wyjściowe numeru pin toohello zapisu wejściowy kod pin hello pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="5d08e-240">toodo this, connect hello Container (MPEG-4) output pin toohello Write input pin of hello File Output.</span></span>

![Połączone dane wyjściowe pliku](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

<span data-ttu-id="5d08e-242">*Połączone dane wyjściowe pliku*</span><span class="sxs-lookup"><span data-stu-id="5d08e-242">*Connected File Output*</span></span>

<span data-ttu-id="5d08e-243">Witaj nazwę pliku, który będzie używany jest określana przez hello właściwości pliku.</span><span class="sxs-lookup"><span data-stu-id="5d08e-243">hello filename that will be used is determined by hello File property.</span></span> <span data-ttu-id="5d08e-244">Tej właściwości mogą być zapisane na stałe tooa danej wartości, co prawdopodobnie będą tooset go za pomocą wyrażenia zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="5d08e-244">While that property can be hardcoded tooa given value, most likely one will want tooset it through an expression instead.</span></span>

<span data-ttu-id="5d08e-245">przepływ pracy hello toohave automatycznie określić dane wyjściowe hello plików właściwość name z wyrażenia, kliknij hello przycisku następnej nazwy pliku toohello (toohello folderu dalej).</span><span class="sxs-lookup"><span data-stu-id="5d08e-245">toohave hello workflow automatically determine hello output File name property from an expression, click hello buton next toohello File name (next toohello folder icon).</span></span> <span data-ttu-id="5d08e-246">Z hello menu rozwijane, a następnie wybierz pozycję "Wyrażenie".</span><span class="sxs-lookup"><span data-stu-id="5d08e-246">From hello drop down menu then select "Expression".</span></span> <span data-ttu-id="5d08e-247">Zostanie wyświetlone okno edytora wyrażeń hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-247">This will bring up hello expression editor.</span></span> <span data-ttu-id="5d08e-248">Najpierw wyczyść zawartość hello hello edytora.</span><span class="sxs-lookup"><span data-stu-id="5d08e-248">Clear hello contents of hello editor first.</span></span>

![Pusty edytora wyrażeń](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

<span data-ttu-id="5d08e-250">*Pusty edytora wyrażeń*</span><span class="sxs-lookup"><span data-stu-id="5d08e-250">*Empty Expression Editor*</span></span>

<span data-ttu-id="5d08e-251">Edytor wyrażeń Hello umożliwia tooenter literał, mieszane z co najmniej jedną zmienną.</span><span class="sxs-lookup"><span data-stu-id="5d08e-251">hello expression editor allows tooenter any literal value, mixed with one or more variables.</span></span> <span data-ttu-id="5d08e-252">Zmienne zaczynać się znak dolara ($).</span><span class="sxs-lookup"><span data-stu-id="5d08e-252">Variables start with a dollar sign.</span></span> <span data-ttu-id="5d08e-253">Jak naciśniesz klawisz $ hello Edytor hello zostaną wyświetlone w polu listy rozwijanej dzięki szerokiemu wyborowi dostępnych zmiennych.</span><span class="sxs-lookup"><span data-stu-id="5d08e-253">As you hit hello $ key, hello editor will show a dropdown box with a choice of available variables.</span></span> <span data-ttu-id="5d08e-254">W tym przypadku użyjemy kombinację zmiennej katalog wyjściowy hello oraz zmienna nazwy pliku wejściowego podstawowego hello:</span><span class="sxs-lookup"><span data-stu-id="5d08e-254">In our case we'll use a combination of hello output directory variable and hello base input file name variable:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Wypełnione limit edytora wyrażeń](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

<span data-ttu-id="5d08e-256">*Wypełnione limit edytora wyrażeń*</span><span class="sxs-lookup"><span data-stu-id="5d08e-256">*Filled out Expression Editor*</span></span>

> [!NOTE]
> <span data-ttu-id="5d08e-257">W kolejności toosee Zobacz pliku wyjściowego zadania kodowania na platformie Azure, należy podać wartość w edytorze wyrażenie hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-257">In order toosee see an output file of your encoding job in Azure, you must provide a value in hello expression editor.</span></span>
>
>

<span data-ttu-id="5d08e-258">Po potwierdzeniu hello wyrażenie za pomocą ok okna właściwości hello będzie podglądu toowhat wartość hello pliku właściwości rozwiązuje w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="5d08e-258">When you confirm hello expression by hitting ok, hello property window will preview toowhat value hello File property resolves at this point in time.</span></span>

![Wynikiem rozpoznania wyrażenia pliku jest katalog wyjściowy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

<span data-ttu-id="5d08e-260">*Wynikiem rozpoznania wyrażenia pliku jest katalog wyjściowy*</span><span class="sxs-lookup"><span data-stu-id="5d08e-260">*File Expression resolves output dir*</span></span>

### <span data-ttu-id="5d08e-261"><a id="MXF_to_MP4_asset_from_output"></a>Tworzenie zasobów usługi multimediów z pliku wyjściowego hello</span><span class="sxs-lookup"><span data-stu-id="5d08e-261"><a id="MXF_to_MP4_asset_from_output"></a>Creating a Media Services Asset from hello output file</span></span>
<span data-ttu-id="5d08e-262">Gdy firma Microsoft ma zapisywanie pliku wyjściowego MP4, potrzebujemy nadal tooindicate czy ten plik należy toohello output zasobów, które usługi media services wygeneruje wyniku wykonania ten przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="5d08e-262">While we have written an MP4 output file, we still need tooindicate that this file belongs toohello output asset which media services will generate as a result of executing this workflow.</span></span> <span data-ttu-id="5d08e-263">toothis celu hello węzła zawartości pliku wyjściowej na kanwie przepływu pracy hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="5d08e-263">toothis end, hello Output File/Asset node on hello workflow canvas is used.</span></span> <span data-ttu-id="5d08e-264">Wszystkie pliki przychodzące do tego węzła spowoduje, że część hello wynikowy zasobów usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="5d08e-264">All incoming files into this node will make part of hello resulting Azure Media Services asset.</span></span>

<span data-ttu-id="5d08e-265">Połącz hello dane wyjściowe pliku składnika toohello zawartości pliku wyjściowej składnika toofinish hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="5d08e-265">Connect hello File Output component toohello Output File/Asset component toofinish hello workflow.</span></span>

![Zakończono przepływu pracy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

<span data-ttu-id="5d08e-267">*Zakończono przepływu pracy*</span><span class="sxs-lookup"><span data-stu-id="5d08e-267">*Finished Workflow*</span></span>

### <span data-ttu-id="5d08e-268"><a id="MXF_to_MP4_test"></a>Test hello Zakończono lokalnie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-268"><a id="MXF_to_MP4_test"></a>Test hello finished workflow locally</span></span>
<span data-ttu-id="5d08e-269">workflow hello tootest lokalnie, kliknij przycisk play hello na powitania narzędzi u góry hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-269">tootest hello workflow locally, hit hello play button in hello toolbar at hello top.</span></span> <span data-ttu-id="5d08e-270">Po zakończeniu wykonywania przepływu pracy hello inspekcję hello dane wyjściowe generowane w folderze wyjściowym hello skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="5d08e-270">When hello workflow finished executing, inspect hello output generated in hello configured output folder.</span></span> <span data-ttu-id="5d08e-271">Zobaczysz, że plik wyjściowy MP4, które zakodowano z pliku źródła danych wejściowych MXF hello Zakończono hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-271">You'll see hello finished MP4 output file that was encoded from hello MXF input source file.</span></span>

## <span data-ttu-id="5d08e-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Kodowanie MXF do MP4 - multibitrate włączoną funkcję dynamicznego tworzenia pakietów</span><span class="sxs-lookup"><span data-stu-id="5d08e-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span></span>
<span data-ttu-id="5d08e-273">W tym przewodniku utworzymy zestaw wielu plików MP4 z algorytmem AAC audio z jednej. Plik wejściowy MXF.</span><span class="sxs-lookup"><span data-stu-id="5d08e-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span></span>

<span data-ttu-id="5d08e-274">Do użycia w połączeniu z funkcji dynamicznego tworzenia pakietów hello oferowanych przez usługi Azure Media Services, wielu plików MP4 wyrównane GOP każdego różne szybkości transmisji bitów i rozwiązanie będzie konieczne toobe generowane podczas wyjścia zasobów wielokrotnej szybkości transmisji bitów jest pożądana.</span><span class="sxs-lookup"><span data-stu-id="5d08e-274">When a multi-bitrate asset output is desired for use in combination with hello Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need toobe generated.</span></span> <span data-ttu-id="5d08e-275">Dlatego hello toodo [kodowanie MXF do pojedynczej szybkości transmisji bitów MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) wskazówki zapewnia dobry punkt wyjścia.</span><span class="sxs-lookup"><span data-stu-id="5d08e-275">toodo so, hello [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span></span>

![Uruchamianie przepływu pracy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

<span data-ttu-id="5d08e-277">*Uruchamianie przepływu pracy*</span><span class="sxs-lookup"><span data-stu-id="5d08e-277">*Starting Workflow*</span></span>

### <span data-ttu-id="5d08e-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Dodanie jednego lub więcej dodatkowych danych wyjściowych MP4</span><span class="sxs-lookup"><span data-stu-id="5d08e-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adding one or more additional MP4 outputs</span></span>
<span data-ttu-id="5d08e-279">Każdy plik MP4 w naszym wynikowy zasobów usługi Azure Media Services będzie obsługiwać różne szybkości transmisji bitów i rozdzielczość.</span><span class="sxs-lookup"><span data-stu-id="5d08e-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span></span> <span data-ttu-id="5d08e-280">Możemy dodać co najmniej jeden MP4 dane wyjściowe pliki toohello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="5d08e-280">Let's add one or more MP4 output files toohello workflow.</span></span>

<span data-ttu-id="5d08e-281">toomake czy mamy hello wszystkich naszych wideo koderów utworzone za pomocą tych samych ustawień, jego najodpowiedniejszym tooduplicate hello już istniejącą koder wideo AVC i skonfigurować kombinację inną rozdzielczość i szybkość transmisji bitów (Dodajmy jedną 960 x 540 na 25 klatek na sekundę w 2,5 MB/s).</span><span class="sxs-lookup"><span data-stu-id="5d08e-281">toomake sure we have all our video encoders created with hello same settings, it's most convenient tooduplicate hello already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span></span> <span data-ttu-id="5d08e-282">tooduplicate hello istniejących kodera kopiowania wklej go na powierzchni projektanta hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-282">tooduplicate hello existing encoder, copy paste it on hello designer surface.</span></span>

<span data-ttu-id="5d08e-283">Połącz hello wideo nieskompresowanych danych wyjściowych kod pin hello wejście pliku multimediów do naszego nowego składnika AVC.</span><span class="sxs-lookup"><span data-stu-id="5d08e-283">Connect hello Uncompressed Video output pin of hello Media File Input into our new AVC component.</span></span>

![Drugi kodera AVC połączone](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

<span data-ttu-id="5d08e-285">*Drugi kodera AVC połączone*</span><span class="sxs-lookup"><span data-stu-id="5d08e-285">*Second AVC encoder connected*</span></span>

<span data-ttu-id="5d08e-286">Teraz dostosowania hello konfiguracji dla naszego nowego AVC koder toooutput 960 x 540 2,5 MB/s.</span><span class="sxs-lookup"><span data-stu-id="5d08e-286">Now adapt hello configuration for our new AVC encoder toooutput 960x540 at 2,5 Mbps.</span></span> <span data-ttu-id="5d08e-287">(Użyj właściwości "dane wyjściowe szerokości", "Dane wyjściowe height" i "Szybkości transmisji bitów (KB/s)" to).</span><span class="sxs-lookup"><span data-stu-id="5d08e-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span></span>

<span data-ttu-id="5d08e-288">Podane chcemy toouse hello wynikowy zasobów wraz z usługi Azure Media Services dynamicznego tworzenia pakietów, hello punktu końcowego przesyłania strumieniowego musi toobe może generować z tych plików MP4 HLS/podzielonej zawartości MP4/DASH fragmentów, które są dokładnie wyrównany tooeach innych w sposób czy klientów, którzy są przełączanie między różne szybkości transmisji bitów Pobierz pojedynczy smooth ciągłego wideo i audio środowisko.</span><span class="sxs-lookup"><span data-stu-id="5d08e-288">Given we want toouse hello resulting asset together with Azure Media Services' dynamic packaging, hello streaming endpoint needs toobe capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned tooeach other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span></span> <span data-ttu-id="5d08e-289">toomake to zrobić, potrzebujemy tooensure, że w właściwości hello zarówno koderów AVC hello rozmiar GOP ("grupa obrazów") dla oba pliki MP4 wartość too2 sekund, które można to zrobić:</span><span class="sxs-lookup"><span data-stu-id="5d08e-289">toomake that happen, we need tooensure that, in hello properties of both AVC encoders hello GOP ("group of pictures") size for both MP4 files is set too2 seconds, which can be done by:</span></span>

* <span data-ttu-id="5d08e-290">Ustawianie rozmiaru GOP tooFixed Tryb rozmiaru GOP hello i</span><span class="sxs-lookup"><span data-stu-id="5d08e-290">setting hello GOP Size Mode tooFixed GOP size and</span></span>
* <span data-ttu-id="5d08e-291">Witaj Interwał ramki klucza tootwo sekund.</span><span class="sxs-lookup"><span data-stu-id="5d08e-291">hello Key Frame Interval tootwo seconds.</span></span>
* <span data-ttu-id="5d08e-292">również ustawić hello tooensure GOP tooClosed GOP IDR kontroli, które stoją wszystkich GOP na ich własnych bez zależności</span><span class="sxs-lookup"><span data-stu-id="5d08e-292">also set hello GOP IDR Control tooClosed GOP tooensure all GOP's are standing on their own without dependencies</span></span>

<span data-ttu-id="5d08e-293">toomake naszych wygodne toounderstand przepływu pracy, Zmień nazwę pierwszego kodera AVC hello zbyt "koder wideo AVC 640 x 360 1200 kb/s" i hello drugi kodera AVC "koder wideo AVC 960 x 540 2500 KB/s".</span><span class="sxs-lookup"><span data-stu-id="5d08e-293">toomake our workflow convenient toounderstand, rename hello first AVC encoder too"AVC Video Encoder 640x360 1200kbps" and hello second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span></span>

<span data-ttu-id="5d08e-294">Teraz należy dodać drugi multiplekser ISO MPEG-4, a drugi dane wyjściowe pliku.</span><span class="sxs-lookup"><span data-stu-id="5d08e-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span></span> <span data-ttu-id="5d08e-295">Połącz hello multiplekser toohello nowe AVC koder i upewnij się, że dane wyjściowe są kierowane do hello pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="5d08e-295">Connect hello multiplexer toohello new AVC encoder and make sure its output is directed into hello File Output.</span></span> <span data-ttu-id="5d08e-296">Także połączyć nowy toohello dane wyjściowe kodera audio AAC hello multiplekser w danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="5d08e-296">Then also connect hello AAC audio encoder output toohello new multiplexer's input.</span></span> <span data-ttu-id="5d08e-297">Hello pliku wyjściowego z kolei będzie tooadd węzła zawartości pliku wyjściowej połączonych toohello on toohello zasobów usługi nośnika, który zostanie utworzony.</span><span class="sxs-lookup"><span data-stu-id="5d08e-297">hello File Output in turn can then be connected toohello Output File/Asset node tooadd it toohello Media Services Asset that will be created.</span></span>

![Drugi Muxer i dane wyjściowe pliku połączone](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

<span data-ttu-id="5d08e-299">*Drugi Muxer i dane wyjściowe pliku połączone*</span><span class="sxs-lookup"><span data-stu-id="5d08e-299">*Second Muxer and File Output connected*</span></span>

<span data-ttu-id="5d08e-300">Zgodność z dynamicznego tworzenia pakietów usługi Azure Media Services skonfiguruj hello multiplekser w trybie fragmentu tooGOP liczby lub czasu trwania, a następnie ustaw GOPs hello na too1 fragmentu.</span><span class="sxs-lookup"><span data-stu-id="5d08e-300">For compatibility with Azure Media Services dynamic packaging, configure hello multiplexer's Chunk Mode tooGOP count or duration and set hello GOPs per chunk too1.</span></span> <span data-ttu-id="5d08e-301">(Musi to być domyślny hello).</span><span class="sxs-lookup"><span data-stu-id="5d08e-301">(This should be hello default.)</span></span>

![Tryby fragmentu Muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

<span data-ttu-id="5d08e-303">*Tryby fragmentu Muxer*</span><span class="sxs-lookup"><span data-stu-id="5d08e-303">*Muxer Chunk Modes*</span></span>

<span data-ttu-id="5d08e-304">Uwaga: możesz toorepeat ten proces dla innych szybkości transmisji bitów i rozpoznawania kombinacji ma toohave dodać toohello zasobów w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5d08e-304">Note: you may want toorepeat this process for any other bitrate and resolution combinations you want toohave added toohello asset output.</span></span>

### <span data-ttu-id="5d08e-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Konfigurowanie nazwy wyjściowego pliku hello</span><span class="sxs-lookup"><span data-stu-id="5d08e-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configuring hello file output names</span></span>
<span data-ttu-id="5d08e-306">Istnieje więcej niż jeden zasób danych wyjściowych toohello pojedynczy plik dodany.</span><span class="sxs-lookup"><span data-stu-id="5d08e-306">We have more than one single file added toohello output asset.</span></span> <span data-ttu-id="5d08e-307">Zapewnia to konieczność toomake czy powitalne nazwy plików dla każdego hello output plików różnią się od siebie i może nawet stosowana Konwencja nazewnictwa plików, dlatego okazuje się od nazwy pliku hello co w przypadku pracy nad.</span><span class="sxs-lookup"><span data-stu-id="5d08e-307">This provides a need toomake sure hello filenames for each of hello output files are different from each other and maybe even apply a file-naming convention so it becomes clear from hello file name what you're dealing with.</span></span>

<span data-ttu-id="5d08e-308">Nazywanie pliku danych wyjściowych można sterować za pomocą wyrażenia w Projektancie hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-308">File output naming can be controlled through expressions in hello designer.</span></span> <span data-ttu-id="5d08e-309">Otwórz okienko właściwości hello do jednego ze składników danych wyjściowych w pliku hello a hello edytora wyrażeń dla hello właściwości pliku.</span><span class="sxs-lookup"><span data-stu-id="5d08e-309">Open hello property pane for one of hello File Output components and open hello expression editor for hello File property.</span></span> <span data-ttu-id="5d08e-310">Nasze pierwszy plik wyjściowy został skonfigurowany za pomocą następującego wyrażenia hello (zobacz hello samouczek dotyczący z [MXF tooa pojedynczej szybkości transmisji bitów danych wyjściowych MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span><span class="sxs-lookup"><span data-stu-id="5d08e-310">Our first output file was configured through hello following expression (see hello tutorial for going from [MXF tooa single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

<span data-ttu-id="5d08e-311">Oznacza to, że nasze filename jest określany przez dwie zmienne: hello output toowrite katalogu w i hello podstawowa nazwa pliku źródłowego.</span><span class="sxs-lookup"><span data-stu-id="5d08e-311">This means that our filename is determined by two variables: hello output directory toowrite in and hello source file base name.</span></span> <span data-ttu-id="5d08e-312">była Hello jest udostępniany jako właściwość hello głównego przepływu pracy i ostatnie hello jest określany przez hello pliku przychodzących.</span><span class="sxs-lookup"><span data-stu-id="5d08e-312">hello former is exposed as a property on hello workflow root and hello latter is determined by hello incoming file.</span></span> <span data-ttu-id="5d08e-313">Należy pamiętać, że katalog wyjściowy hello, które jest używane do testowania lokalnego; Ta właściwość zostanie zastąpiona hello aparatu przepływu pracy podczas wykonywania przepływu pracy hello przez procesor multimediów oparte na chmurze hello w usłudze Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="5d08e-313">Note that hello output directory is what you use for local testing; this property will be overridden by hello workflow engine when hello workflow is executed by hello cloud-based media processor in Azure Media Services.</span></span>
<span data-ttu-id="5d08e-314">toogive oba pliki wyjście nazewnictwa spójności danych wyjściowych, hello zmiany pliku najpierw wyrażenie nazewnictwa:</span><span class="sxs-lookup"><span data-stu-id="5d08e-314">toogive both our output files a consistent output naming, change hello first file naming expression to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="5d08e-315">a drugi hello do:</span><span class="sxs-lookup"><span data-stu-id="5d08e-315">and hello second to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="5d08e-316">Wykonanie pośrednich testu toomake się, że poprawnie są generowane zarówno pliki wyjściowe MP4.</span><span class="sxs-lookup"><span data-stu-id="5d08e-316">Execute an intermediate test run toomake sure both MP4 output files are properly generated.</span></span>

### <span data-ttu-id="5d08e-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Dodawanie oddzielne ścieżkę Audio</span><span class="sxs-lookup"><span data-stu-id="5d08e-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adding a separate Audio Track</span></span>
<span data-ttu-id="5d08e-318">Jako zajmiemy się później gdy firma Microsoft generuje toogo plik .ism z naszych pliki wyjściowe MP4, zostanie również wymagamy tylko dźwięk plik MP4 jako ścieżka audio hello do naszej adaptacyjnego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="5d08e-318">As we'll see later when we generate an .ism file toogo with our MP4 output files, we will also require a audio-only MP4 file as hello audio track for our adaptive streaming.</span></span> <span data-ttu-id="5d08e-319">toocreate ten plik, Dodaj dodatkowe muxer toohello przepływu pracy (ISO-MPEG-4 multiplekser) i połącz końcówka wyjściowa hello AAC kodera przy jego wprowadzania numeru pin dla ścieżki 1.</span><span class="sxs-lookup"><span data-stu-id="5d08e-319">toocreate this file, add an additional muxer toohello workflow (ISO-MPEG-4 Multiplexer) and connect hello AAC encoder's output pin with its input pin for Track 1.</span></span>

![Audio Muxer dodane](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

<span data-ttu-id="5d08e-321">*Audio Muxer dodane*</span><span class="sxs-lookup"><span data-stu-id="5d08e-321">*Audio Muxer Added*</span></span>

<span data-ttu-id="5d08e-322">Utwórz innego strumienia wychodzącego toooutput hello dane wyjściowe pliku składnika z hello muxer i skonfiguruj hello wyrażenie nazewnictwa plików jako:</span><span class="sxs-lookup"><span data-stu-id="5d08e-322">Create a third File Output component toooutput hello outbound stream from hello muxer and configure hello file naming expression as:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Audio Muxer tworzenia pliku wyjściowego](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

<span data-ttu-id="5d08e-324">*Audio Muxer tworzenia pliku wyjściowego*</span><span class="sxs-lookup"><span data-stu-id="5d08e-324">*Audio Muxer creating File Output*</span></span>

### <span data-ttu-id="5d08e-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Dodawanie hello. Plik SMIL ISM</span><span class="sxs-lookup"><span data-stu-id="5d08e-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adding hello .ISM SMIL File</span></span>
<span data-ttu-id="5d08e-326">Dla toowork dynamicznego tworzenia pakietów hello w połączeniu z obu MP4 plików (i hello tylko dźwięk MP4) w naszym zasobów usługi Media Services, potrzebujemy również pliku manifestu (skrót pliku "SMIL": synchronizowane języka integrację multimediów).</span><span class="sxs-lookup"><span data-stu-id="5d08e-326">For hello dynamic packaging toowork in combination with both MP4 files (and hello audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span></span> <span data-ttu-id="5d08e-327">Ten plik wskazuje tooAzure Media Services, które pliki MP4 są dostępne dla dynamicznego tworzenia pakietów, które z tych tooconsider przesyłania strumieniowego audio hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-327">This file indicates tooAzure Media Services what MP4 files are available for dynamic packaging and which of those tooconsider for hello audio streaming.</span></span> <span data-ttu-id="5d08e-328">Typowy pliku manifestu zestawu MP4 w jednym strumieniem audio wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="5d08e-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

<span data-ttu-id="5d08e-329">zawiera plik .ism Hello w instrukcji switch tooeach odwołanie poszczególnych plików wideo hello MP4 i dodatkowo plik dźwiękowy toothose również jednej (lub więcej) odwołuje się do tooan MP4, zawiera tylko hello audio.</span><span class="sxs-lookup"><span data-stu-id="5d08e-329">hello .ism file contains within a switch statement, a reference tooeach of hello individual MP4 video files and in addition toothose also one (or more) audio file references tooan MP4 that only contains hello audio.</span></span>

<span data-ttu-id="5d08e-330">Generowanie pliku manifestu hello naszego zestawu w MP4 może odbywać się za pośrednictwem składnik o nazwie "AMS manifestu Writer" hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-330">Generating hello manifest file for our set of MP4's can be done through a component called hello "AMS Manifest Writer".</span></span> <span data-ttu-id="5d08e-331">toouse, przeciągnij go na powierzchnię hello i połączyć końcówek wyjściowych "Zapisu ukończone" hello z hello trzy dane wyjściowe pliku składniki toohello AMS manifestu modułu zapisywania danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="5d08e-331">toouse it, drag it onto hello surface and connect hello "Write Complete" output pins from hello three File Output components toohello AMS Manifest Writer input.</span></span> <span data-ttu-id="5d08e-332">Następnie upewnij się, że tooconnect hello dane wyjściowe hello toohello AMS manifestu zapisywania zawartości pliku wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="5d08e-332">Then make sure tooconnect hello output of hello AMS Manifest Writer toohello Output File/Asset.</span></span>

<span data-ttu-id="5d08e-333">Zgodnie z naszym innym składnikom pliku wyjściowego, skonfiguruj Nazwa wyjściowego pliku .ism hello z wyrażeniem:</span><span class="sxs-lookup"><span data-stu-id="5d08e-333">As with our other file output components, configure hello .ism file output name with an expression:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

<span data-ttu-id="5d08e-334">Nasze Zakończono przepływu pracy wygląda hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="5d08e-334">Our finished workflow looks like hello below:</span></span>

![Zakończono MXF toomultibitrate MP4 przepływu pracy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

<span data-ttu-id="5d08e-336">*Zakończono MXF toomultibitrate MP4 przepływu pracy*</span><span class="sxs-lookup"><span data-stu-id="5d08e-336">*Finished MXF toomultibitrate MP4 workflow*</span></span>

## <span data-ttu-id="5d08e-337"><a id="MXF_to__multibitrate_MP4"></a>Kodowanie MXF do multibitrate MP4 — rozszerzone planu</span><span class="sxs-lookup"><span data-stu-id="5d08e-337"><a id="MXF_to__multibitrate_MP4"></a>Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>
<span data-ttu-id="5d08e-338">W hello [przepływu pracy w poprzednim przewodniku](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) możemy przedstawiono sposób pojedynczego zasobu wejściowego MXF mogą być konwertowane na zawartości wyjściowej z plików MP4 wielokrotnej szybkości transmisji bitów, plik MP4 tylko audio i plik manifestu do użycia w połączeniu z usługi Azure Media Dynamiczne tworzenie pakietów usług.</span><span class="sxs-lookup"><span data-stu-id="5d08e-338">In hello [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span></span>

<span data-ttu-id="5d08e-339">W tym przewodniku opisano jak niektóre aspekty hello można usprawniać i wprowadzone wygodniejsze.</span><span class="sxs-lookup"><span data-stu-id="5d08e-339">This walkthrough will show how some of hello aspects can be enhanced and made more convenient.</span></span>

### <span data-ttu-id="5d08e-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Tooenhance omówienie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Workflow overview tooenhance</span></span>
![Multibitrate MP4 tooenhance przepływu pracy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

<span data-ttu-id="5d08e-342">*Multibitrate MP4 tooenhance przepływu pracy*</span><span class="sxs-lookup"><span data-stu-id="5d08e-342">*Multibitrate MP4 workflow tooenhance*</span></span>

### <span data-ttu-id="5d08e-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>Konwencje nazewnictwa plików</span><span class="sxs-lookup"><span data-stu-id="5d08e-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>File Naming Conventions</span></span>
<span data-ttu-id="5d08e-344">W przepływie pracy poprzedniej hello możemy określić proste wyrażenie jako podstawy hello generowania nazwy pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="5d08e-344">In hello previous workflow we specified a simple expression as hello basis for generating output file names.</span></span> <span data-ttu-id="5d08e-345">Mimo że mamy powielania niektórych: wszystkie składniki pliku danych wyjściowych poszczególnych hello hello określone takie wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="5d08e-345">We have some duplication though: all of hello hello individual output file components specified such expression.</span></span>

<span data-ttu-id="5d08e-346">Na przykład składnik dane wyjściowe pliku naszych hello pierwszy plik wideo jest skonfigurowany z tego wyrażenia:</span><span class="sxs-lookup"><span data-stu-id="5d08e-346">For example, our file output component for hello first video file is configured with this expression:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="5d08e-347">Natomiast w przypadku hello drugi wyjście wideo, mamy wyrażeń, takich jak:</span><span class="sxs-lookup"><span data-stu-id="5d08e-347">While for hello second output video, we have an expression like:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="5d08e-348">Nie będą czyszczący mniej błędów podatnych na błędy i bardziej wygodne, jeśli firma Microsoft może. Usuń niektóre tego duplikowania i Postaramy przeprowadzanie łatwiejszych do skonfigurowania zamiast tego?</span><span class="sxs-lookup"><span data-stu-id="5d08e-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span></span> <span data-ttu-id="5d08e-349">Możemy szczęście: hello projektanta wyrażenie możliwości w połączeniu z właściwościami niestandardowymi toocreate możliwości hello w naszym głównym przepływu pracy będą Przekaż nam dodatkową warstwę wygody.</span><span class="sxs-lookup"><span data-stu-id="5d08e-349">Luckily we can: hello designer's expression capabilities in combination with hello ability toocreate custom properties on our workflow root will give us an added layer of convenience.</span></span>

<span data-ttu-id="5d08e-350">Załóżmy, że firma Microsoft będzie dysków filename konfiguracji od szybkości transmisji bitów hello hello poszczególnych plików MP4.</span><span class="sxs-lookup"><span data-stu-id="5d08e-350">Let's assume we'll drive filename configuration from hello bitrates of hello individual MP4 files.</span></span> <span data-ttu-id="5d08e-351">Te szybkości transmisji bitów, firma Microsoft będzie celem tooconfigure w jednej centralnej umieścić (na główny hello naszych wykresu), z której będziesz mieć dostęp do generowania o nazwy pliku tooconfigure i dysku.</span><span class="sxs-lookup"><span data-stu-id="5d08e-351">These bitrates we'll aim tooconfigure in one central place (on hello root of our graph), from where they'll be accessed tooconfigure and drive file name generation.</span></span> <span data-ttu-id="5d08e-352">toodo, Rozpoczniemy publikując hello właściwości szybkości transmisji bitów z obu AVC koderów toohello głównego naszych przepływu pracy, tak że staje się dostępny z obu głównego hello również od koderów hello AVC.</span><span class="sxs-lookup"><span data-stu-id="5d08e-352">toodo this, we start by publishing hello bitrate property from both AVC encoders toohello root of our workflow, so that it becomes accessible from both hello root as well as from hello AVC encoders.</span></span> <span data-ttu-id="5d08e-353">(Nawet jeśli wyświetlane w dwóch różnych miejsc, jest tylko jedna wartość podstawowej).</span><span class="sxs-lookup"><span data-stu-id="5d08e-353">(Even if displayed in two different spots, there's only one underlying value.)</span></span>

### <span data-ttu-id="5d08e-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Właściwości składnika publikacji na powitania głównego przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publishing component properties onto hello workflow root</span></span>
<span data-ttu-id="5d08e-355">Otwórz hello pierwszy AVC kodera, przejdź toohello właściwości szybkości transmisji bitów (KB/s) i z listy rozwijanej hello Wybieranie polecenia Opublikuj.</span><span class="sxs-lookup"><span data-stu-id="5d08e-355">Open hello first AVC encoder, go toohello Bitrate (kbps) property and from hello dropdown choose Publish.</span></span>

![Właściwość publikacji szybkości transmisji bitów hello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

<span data-ttu-id="5d08e-357">*Właściwość publikacji szybkości transmisji bitów hello*</span><span class="sxs-lookup"><span data-stu-id="5d08e-357">*Publishing hello bitrate property*</span></span>

<span data-ttu-id="5d08e-358">Skonfiguruj hello publikowania okna dialogowego toopublish toohello głównego naszych wykresu przepływu pracy z opublikowana nazwa "video1bitrate" i nazwę wyświetlaną do odczytu "Wideo 1 szybkości transmisji bitów".</span><span class="sxs-lookup"><span data-stu-id="5d08e-358">Configure hello publish dialog toopublish toohello root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span></span> <span data-ttu-id="5d08e-359">Konfigurowanie niestandardowej nazwy grupy o nazwie "Przesyłania strumieniowego szybkości transmisji bitów" i kliknij przycisk Publikuj.</span><span class="sxs-lookup"><span data-stu-id="5d08e-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span></span>

![Właściwość publikacji szybkości transmisji bitów hello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

<span data-ttu-id="5d08e-361">*Okno dialogowe publikowania właściwości szybkości transmisji bitów*</span><span class="sxs-lookup"><span data-stu-id="5d08e-361">*Publishing dialog for bitrate property*</span></span>

<span data-ttu-id="5d08e-362">Powtórz hello takie same właściwości szybkości transmisji bitów hello hello drugie kodera AVC i nadaj mu nazwę "video2bitrate" o nazwie wyświetlanej "Wideo 2 szybkości transmisji bitów", w hello sam niestandardowe grupy "Przesyłania strumieniowego szybkości transmisji bitów".</span><span class="sxs-lookup"><span data-stu-id="5d08e-362">Repeat hello same for hello bitrate property of hello second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in hello same custom group "Streaming Bitrates".</span></span>

<span data-ttu-id="5d08e-363">Jeśli mamy teraz sprawdzić właściwości głównej hello przepływu pracy, widzimy naszej grupy niestandardowe z powitalne widoczne dwie właściwości opublikowane.</span><span class="sxs-lookup"><span data-stu-id="5d08e-363">If we now inspect hello workflow root properties, we'll see our custom group with hello two published properties show up.</span></span> <span data-ttu-id="5d08e-364">Oba zdarzenie odzwierciedla wartość hello ich odpowiednich AVC kodera szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="5d08e-364">Both are reflecting hello value of their respective AVC encoder bitrate.</span></span>

![Właściwości opublikowanych szybkości transmisji bitów w katalogu głównym przepływu pracy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

<span data-ttu-id="5d08e-366">Zawsze, gdy chcemy tooaccess te właściwości z kodu lub wyrażenie, możemy to zrobić następująco:</span><span class="sxs-lookup"><span data-stu-id="5d08e-366">Whenever we want tooaccess these properties from code or from an expression, we can do so like this:</span></span>

* <span data-ttu-id="5d08e-367">z wbudowanego kodu ze składnika bezpośrednio pod głównego hello: node.getPropertyAsString('.. / video1bitrate ", null)</span><span class="sxs-lookup"><span data-stu-id="5d08e-367">from inline code from a component right below hello root: node.getPropertyAsString('../video1bitrate',null)</span></span>
* <span data-ttu-id="5d08e-368">w wyrażeniu: ${ROOT_video1bitrate}</span><span class="sxs-lookup"><span data-stu-id="5d08e-368">within an expression: ${ROOT_video1bitrate}</span></span>

<span data-ttu-id="5d08e-369">Umożliwia zakończenie grupy "Przesyłania strumieniowego szybkości transmisji bitów" hello publikując naszych ścieżki audio szybkości transmisji bitów w nim również.</span><span class="sxs-lookup"><span data-stu-id="5d08e-369">Let's complete hello "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span></span> <span data-ttu-id="5d08e-370">W ramach właściwości hello hello AAC kodera Wyszukaj hello ustawienie szybkości transmisji bitów i wybierz publikowania tooit dalej hello listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="5d08e-370">Within hello properties of hello AAC Encoder, search for hello Bitrate setting and select Publish from hello dropdown next tooit.</span></span> <span data-ttu-id="5d08e-371">Publikowanie głównego toohello hello wykresu o nazwie "audio1bitrate" i nazwie "Audio 1 szybkości transmisji bitów" w naszej grupy niestandardowe "Przesyłania strumieniowego szybkości transmisji bitów" wyświetlanej.</span><span class="sxs-lookup"><span data-stu-id="5d08e-371">Publish toohello root of hello graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span></span>

![Okno dialogowe publikowania audio szybkości transmisji bitów](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

<span data-ttu-id="5d08e-373">*Okno dialogowe publikowania audio szybkości transmisji bitów*</span><span class="sxs-lookup"><span data-stu-id="5d08e-373">*Publishing dialog for audio bitrate*</span></span>

![Wynikowa właściwości audio i wideo w folderze głównym](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

<span data-ttu-id="5d08e-375">*Wynikowa właściwości audio i wideo w folderze głównym*</span><span class="sxs-lookup"><span data-stu-id="5d08e-375">*Resulting video and audio props on root*</span></span>

<span data-ttu-id="5d08e-376">Zauważ, że zmiana któregoś z tych trzech wartości również ponownie konfiguruje i zmiany hello wartości na powitania odpowiednie składniki są one połączone z (i w przypadku, gdy publikowane z).</span><span class="sxs-lookup"><span data-stu-id="5d08e-376">Note that changing any of those three values also re-configures and changes hello values on hello respective components they are linked with (and where published from).</span></span>

### <span data-ttu-id="5d08e-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Wygenerowano plik wyjściowy, który nazwy zależne od wartości właściwości opublikowanych</span><span class="sxs-lookup"><span data-stu-id="5d08e-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Have generated output file names rely on published property values</span></span>
<span data-ttu-id="5d08e-378">Zamiast hardcoding naszych nazwy wygenerowanego pliku możemy można teraz zmienić naszych wyrażenia nazwy pliku na każdym toorely składników danych wyjściowych w pliku hello na powitania szybkości transmisji bitów właściwości, które firma Microsoft właśnie opublikowany w katalogu głównym wykres hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of hello File Output components toorely on hello bitrate properties we just published on hello graph root.</span></span> <span data-ttu-id="5d08e-379">Począwszy od pierwszego wyjście pliku znaleźć hello właściwości pliku i edytować wyrażenie hello następująco:</span><span class="sxs-lookup"><span data-stu-id="5d08e-379">Starting with our first file output, find hello File property and edit hello expression like this:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

<span data-ttu-id="5d08e-380">można uzyskać dostępu do i wprowadzone za pomocą dolara hello na klawiaturze hello w okna wyrażenie hello Hello innych parametrów w tym wyrażeniu.</span><span class="sxs-lookup"><span data-stu-id="5d08e-380">hello different parameters in this expression can be accessed and entered by hitting hello dollar sign on hello keyboard while in hello expression window.</span></span> <span data-ttu-id="5d08e-381">Jeden z parametrów dostępnych hello jest właściwość naszych video1bitrate, co możemy wcześniej publikowane.</span><span class="sxs-lookup"><span data-stu-id="5d08e-381">One of hello available parameters is our video1bitrate property which we published earlier.</span></span>

![Uzyskiwanie dostępu do parametrów w wyrażeniu](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

<span data-ttu-id="5d08e-383">*Uzyskiwanie dostępu do parametrów w wyrażeniu*</span><span class="sxs-lookup"><span data-stu-id="5d08e-383">*Accessing parameters within an expression*</span></span>

<span data-ttu-id="5d08e-384">Witaj identyczne dane wyjściowe pliku hello naszych drugi wideo:</span><span class="sxs-lookup"><span data-stu-id="5d08e-384">Do hello same for hello file output for our second video:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

<span data-ttu-id="5d08e-385">i dla danych wyjściowych w pliku tylko do dźwięk hello:</span><span class="sxs-lookup"><span data-stu-id="5d08e-385">and for hello audio-only file output:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

<span data-ttu-id="5d08e-386">Jeżeli zmienimy teraz hello szybkości transmisji bitów dla każdego hello wideo lub audio plików, konfiguracja zostanie zmieniona kodera odpowiednich hello i Konwencji nazwę pliku na podstawie szybkości transmisji bitów hello będą honorowane wszystkie automatyczne.</span><span class="sxs-lookup"><span data-stu-id="5d08e-386">If we now change hello bitrate for any of hello video or audio files, hello respective encoder will be reconfigured and hello bitrate-based file name convention will be honored all automatic.</span></span>

## <span data-ttu-id="5d08e-387"><a id="thumbnails_to__multibitrate_MP4"></a>Dodawanie danych wyjściowych MP4 toomultibitrate miniatur</span><span class="sxs-lookup"><span data-stu-id="5d08e-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adding thumbnails toomultibitrate MP4 output</span></span>
<span data-ttu-id="5d08e-388">Począwszy od przepływu pracy, który generuje [multibitrate MP4 wyjściowymi MXF wejściowych](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), możemy teraz będzie wyszukiwania na dodawanie danych wyjściowych toohello miniatur.</span><span class="sxs-lookup"><span data-stu-id="5d08e-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails toohello output.</span></span>

### <span data-ttu-id="5d08e-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Miniatur tooadd omówienie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Workflow overview tooadd thumbnails to</span></span>
![Multibitrate MP4 toostart przepływu pracy z](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

<span data-ttu-id="5d08e-391">*Multibitrate MP4 toostart przepływu pracy z*</span><span class="sxs-lookup"><span data-stu-id="5d08e-391">*Multibitrate MP4 workflow toostart from*</span></span>

### <span data-ttu-id="5d08e-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Dodawanie kodowania JPG</span><span class="sxs-lookup"><span data-stu-id="5d08e-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adding JPG Encoding</span></span>
<span data-ttu-id="5d08e-393">Puls Hello naszych miniatur generacji będą hello składnika kodera JPG, toooutput stanie JPG — pliki.</span><span class="sxs-lookup"><span data-stu-id="5d08e-393">hello heart of our thumbnail generation will be hello JPG Encoder component, able toooutput JPG files.</span></span>

![Koder JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

<span data-ttu-id="5d08e-395">*Koder JPG*</span><span class="sxs-lookup"><span data-stu-id="5d08e-395">*JPG Encoder*</span></span>

<span data-ttu-id="5d08e-396">Firma Microsoft nie można jednak bezpośrednio połączyć naszych strumienia wideo nieskompresowanych z hello wejście pliku multimediów do kodera JPG hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-396">We cannot however directly connect our Uncompressed Video stream from hello Media File Input into hello JPG encoder.</span></span> <span data-ttu-id="5d08e-397">Zamiast tego oczekuje się, że toobe przekazać poszczególnych klatek.</span><span class="sxs-lookup"><span data-stu-id="5d08e-397">Instead, it expects toobe handed individual frames.</span></span> <span data-ttu-id="5d08e-398">To, możemy za pośrednictwem składnika brama ramki wideo hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-398">This, we can do through hello Video Frame Gate component.</span></span>

![Łączenie koder ramki bramy toohello JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

<span data-ttu-id="5d08e-400">*Łączenie koder ramki bramy toohello JPG*</span><span class="sxs-lookup"><span data-stu-id="5d08e-400">*Connecting a frame gate toohello JPG encoder*</span></span>

<span data-ttu-id="5d08e-401">Brama ramki powitania po co tyle sekund lub ramki umożliwia toopass klatki.</span><span class="sxs-lookup"><span data-stu-id="5d08e-401">hello frame gate once every so many seconds or frames allows a video frame toopass.</span></span> <span data-ttu-id="5d08e-402">czas interwału i hello Hello przesunięcia, z którym dzieje się to można skonfigurować we właściwościach hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-402">hello interval and hello time offset with which this happens is configurable in hello properties.</span></span>

![Właściwości ramki bramy wideo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

<span data-ttu-id="5d08e-404">*Właściwości ramki bramy wideo*</span><span class="sxs-lookup"><span data-stu-id="5d08e-404">*Video Frame Gate properties*</span></span>

<span data-ttu-id="5d08e-405">Umożliwia utworzenie miniatury co minutę przez ustawienie hello tryb tooTime (w sekundach) i hello too60 interwału.</span><span class="sxs-lookup"><span data-stu-id="5d08e-405">Let's create a thumbnail every minute by setting hello mode tooTime (seconds) and hello Interval too60.</span></span>

### <span data-ttu-id="5d08e-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Zajmujących się konwersji przestrzeń kolorów</span><span class="sxs-lookup"><span data-stu-id="5d08e-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Dealing with Color Space conversion</span></span>
<span data-ttu-id="5d08e-407">Gdy logiczne wydaje zarówno teraz może być połączony PIN nieskompresowanym wideo hello ramki bramy i hello wejście pliku multimediów, możemy otrzyma ostrzeżenie, jeśli firma Microsoft może to zrobić.</span><span class="sxs-lookup"><span data-stu-id="5d08e-407">While it would seem logical both Uncompressed Video pins of hello frame gate and hello Media File Input can now be connected, we would get a warning if we would do so.</span></span>

![Koloru okna wprowadzania komunikat o błędzie](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

<span data-ttu-id="5d08e-409">*Koloru okna wprowadzania komunikat o błędzie*</span><span class="sxs-lookup"><span data-stu-id="5d08e-409">*Input color space error*</span></span>

<span data-ttu-id="5d08e-410">Jest to spowodowane sposób hello w kolorze, które informacje jest reprezentowane w naszym oryginalnego raw nieskompresowanych strumienia wideo, pochodzące z naszych MXF różni się od jakiego hello JPG Koder oczekuje.</span><span class="sxs-lookup"><span data-stu-id="5d08e-410">This is because hello way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what hello JPG Encoder is expecting.</span></span> <span data-ttu-id="5d08e-411">Więcej w szczególności tak zwane "przestrzeń kolorów" "RGB" lub "Skali szarości" jest oczekiwany tooflow w.</span><span class="sxs-lookup"><span data-stu-id="5d08e-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected tooflow in.</span></span> <span data-ttu-id="5d08e-412">Oznacza to, że dla ruchu przychodzącego strumienia wideo o tym hello wideo ramki bramy w należy toohave konwersji zastosowana jako pierwsza dotyczące jego przestrzeń kolorów.</span><span class="sxs-lookup"><span data-stu-id="5d08e-412">This means that hello Video Frame Gate's inbound video stream will need toohave a conversion applied regarding its color space first.</span></span>

<span data-ttu-id="5d08e-413">Przeciągnij na powitania przepływu pracy hello konwertera miejsca kolor - Intel i podłącz go tooour ramki bramy.</span><span class="sxs-lookup"><span data-stu-id="5d08e-413">Drag onto hello workflow hello Color Space Converter - Intel and connect it tooour frame gate.</span></span>

![Łączenie konwertera miejsca kolorów](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

<span data-ttu-id="5d08e-415">*Łączenie konwertera miejsca kolorów*</span><span class="sxs-lookup"><span data-stu-id="5d08e-415">*Connecting a Color Space Convertor*</span></span>

<span data-ttu-id="5d08e-416">W oknie właściwości hello wybierz hello BGR 24 wpisu z listy wstępnie ustawionych hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-416">In hello properties window, pick hello BGR 24 entry from hello Preset list.</span></span>

### <span data-ttu-id="5d08e-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Zapisywanie hello miniatur</span><span class="sxs-lookup"><span data-stu-id="5d08e-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Writing hello thumbnails</span></span>
<span data-ttu-id="5d08e-418">Inne niż filmie MP4, hello kodera JPG, dane wyjściowe obejmują składnika więcej niż jeden plik.</span><span class="sxs-lookup"><span data-stu-id="5d08e-418">Different from our MP4 video's, hello JPG Encoder component will output more than one file.</span></span> <span data-ttu-id="5d08e-419">W kolejności toodeal z tym, można użyć składnika zapisywania pliku JPG wyszukiwania sceny: go otrzymuje hello przychodzące miniatur JPG i zapisać je, przy kończyły przez inną liczbę nazw plików.</span><span class="sxs-lookup"><span data-stu-id="5d08e-419">In order toodeal with this, a Scene Search JPG File Writer component can be used: it will take hello incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span></span> <span data-ttu-id="5d08e-420">(numer hello zwykle wskazuje hello liczbę sekund/jednostek w strumieniu hello, który hello miniatur zostało pobranych z).</span><span class="sxs-lookup"><span data-stu-id="5d08e-420">(hello number typically indicating hello number of seconds/units in hello stream which hello thumbnail was drawn from.)</span></span>

![Wprowadzenie hello zapisywania pliku JPG wyszukiwania sceny](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

<span data-ttu-id="5d08e-422">*Wprowadzenie hello zapisywania pliku JPG wyszukiwania sceny*</span><span class="sxs-lookup"><span data-stu-id="5d08e-422">*Introducing hello Scene Search JPG File Writer*</span></span>

<span data-ttu-id="5d08e-423">Właściwość ścieżki do folderu wyjściowego hello skonfigurować za pomocą wyrażenia hello: ${ROOT_outputWriteDirectory}</span><span class="sxs-lookup"><span data-stu-id="5d08e-423">Configure hello Output Folder Path property with hello expression: ${ROOT_outputWriteDirectory}</span></span>

<span data-ttu-id="5d08e-424">i hello właściwość prefiks nazwy pliku:</span><span class="sxs-lookup"><span data-stu-id="5d08e-424">and hello Filename Prefix property with:</span></span>

    ${ROOT_sourceFileBaseName}_thumb_

<span data-ttu-id="5d08e-425">Prefiks Hello określa sposób nazywania hello miniatur plików.</span><span class="sxs-lookup"><span data-stu-id="5d08e-425">hello prefix will determine how hello thumbnail files are being named.</span></span> <span data-ttu-id="5d08e-426">One będą kończyły się słowem numer wskazujące hello położeniu wskaźnika w strumieniu hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-426">They will be suffixed with a number indicating hello thumb's position in hello stream.</span></span>

![Właściwości składnika zapisywania pliku JPG wyszukiwania sceny](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

<span data-ttu-id="5d08e-428">*Właściwości składnika zapisywania pliku JPG wyszukiwania sceny*</span><span class="sxs-lookup"><span data-stu-id="5d08e-428">*Scene Search JPG File Writer properties*</span></span>

<span data-ttu-id="5d08e-429">Połącz hello zapisywania pliku JPG wyszukiwania sceny toohello zawartości pliku wyjściowej węzła.</span><span class="sxs-lookup"><span data-stu-id="5d08e-429">Connect hello Scene Search JPG File Writer toohello Output File/Asset node.</span></span>

### <span data-ttu-id="5d08e-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Wykrywanie błędów w przepływie pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detecting errors in a workflow</span></span>
<span data-ttu-id="5d08e-431">Połącz dane wejściowe hello hello kolor miejsca konwertera toohello raw nieskompresowanych wideo danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5d08e-431">Connect hello input of hello color space converter toohello raw uncompressed video output.</span></span> <span data-ttu-id="5d08e-432">Teraz wykonać testy lokalne powitania przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="5d08e-432">Now perform a local test run for hello workflow.</span></span> <span data-ttu-id="5d08e-433">Istnieje przepływu pracy hello szansa nagle zatrzyma, wykonywanie i oznaczać z czerwonego obramowania na powitania składnik, który wystąpił błąd:</span><span class="sxs-lookup"><span data-stu-id="5d08e-433">There's a good chance hello workflow will suddenly stop executing and indicate with a red outline on hello component that encountered an error:</span></span>

![Błąd konwertera miejsca kolorów](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

<span data-ttu-id="5d08e-435">*Błąd konwertera miejsca kolorów*</span><span class="sxs-lookup"><span data-stu-id="5d08e-435">*Color Space Converter error*</span></span>

<span data-ttu-id="5d08e-436">Kliknij ikonę "E" hello nieco red hello prawym górnym rogu hello konwertera miejsca kolor składnika toosee, co to jest przyczyna hello hello kodowania próba nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="5d08e-436">Click hello little red "E" icon in hello top right corner of hello Color Space Converter component toosee what's hello reason hello encoding attempt failed.</span></span>

![Okno dialogowe kolorów konwertera miejsca](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

<span data-ttu-id="5d08e-438">*Okno dialogowe kolorów konwertera miejsca*</span><span class="sxs-lookup"><span data-stu-id="5d08e-438">*Color Space Converter error dialog*</span></span>

<span data-ttu-id="5d08e-439">Monitor przechodzi w stan, jak widać, że hello przychodzące przestrzeń kolorów na standardowe dla konwertera miejsca kolor hello ma rec601 toobe naszych żądanego konwersji YUV tooRGB.</span><span class="sxs-lookup"><span data-stu-id="5d08e-439">It turns out, as you can see, that hello incoming color space standard for hello color space converter has toobe rec601 for our requested conversion of YUV tooRGB.</span></span> <span data-ttu-id="5d08e-440">Najwyraźniej naszych strumienia nie oznacza jego rec601.</span><span class="sxs-lookup"><span data-stu-id="5d08e-440">Apparently our stream doesn't indicate it's rec601.</span></span> <span data-ttu-id="5d08e-441">(ZAL 601 jest standardem kodowania naprzemiennych analogowy sygnały wideo w formie cyfrowej wideo.</span><span class="sxs-lookup"><span data-stu-id="5d08e-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span></span> <span data-ttu-id="5d08e-442">Określa aktywnego regionu, obejmujące 720 jasności oraz 360 próbki chrominance w jednym wierszu.</span><span class="sxs-lookup"><span data-stu-id="5d08e-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span></span> <span data-ttu-id="5d08e-443">kolor Hello kodowanie system jest nazywany YCbCr 4:2:2.)</span><span class="sxs-lookup"><span data-stu-id="5d08e-443">hello color encoding system is known as YCbCr 4:2:2.)</span></span>

<span data-ttu-id="5d08e-444">toofix, firma Microsoft będzie wskazuje na metadanych hello naszych strumienia, który możemy Cię zajmujących rec601 zawartości.</span><span class="sxs-lookup"><span data-stu-id="5d08e-444">toofix this, we'll indicate on hello metadata of our stream that we're dealing with rec601 content.</span></span> <span data-ttu-id="5d08e-445">toodo, dlatego użyjemy komponent Updater typu danych wideo, który będzie testujemy Between naszych raw źródła i hello kolor miejsca konwersji składnika.</span><span class="sxs-lookup"><span data-stu-id="5d08e-445">toodo so we'll use a Video Data Type Updater component, which we'll put in between our raw source and hello color space conversion component.</span></span> <span data-ttu-id="5d08e-446">Tej aktualizacji typu danych umożliwia ręcznej aktualizacji hello niektórych danych wideo właściwości typu.</span><span class="sxs-lookup"><span data-stu-id="5d08e-446">This data type updater allows for hello manual update of certain video data type properties.</span></span> <span data-ttu-id="5d08e-447">Skonfiguruj tooindicate kolor miejsca Standard "Rec 601".</span><span class="sxs-lookup"><span data-stu-id="5d08e-447">Configure it tooindicate a Color Space Standard of "Rec 601".</span></span> <span data-ttu-id="5d08e-448">Spowoduje to hello Updater typu danych wideo tootag hello strumienia z przestrzeń kolorów "Rec 601" hello, jeśli nie było żadnych przestrzeń kolorów jeszcze zdefiniowana.</span><span class="sxs-lookup"><span data-stu-id="5d08e-448">This will cause hello Video Data Type Updater tootag hello stream with hello "Rec 601" color space if there was no color space defined yet.</span></span> <span data-ttu-id="5d08e-449">(Nie zastąpi on metadane, chyba że zaznaczono pole wyboru zastąpienie hello.)</span><span class="sxs-lookup"><span data-stu-id="5d08e-449">(It will not override any existing metadata, unless hello Override checkbox was checked.)</span></span>

![Aktualizowanie kolor miejsce na standardowej na powitania Updater typu danych](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

<span data-ttu-id="5d08e-451">*Aktualizowanie kolor miejsce na standardowej na powitania Updater typu danych*</span><span class="sxs-lookup"><span data-stu-id="5d08e-451">*Updating Color Space Standard on hello Data Type Updater*</span></span>

### <span data-ttu-id="5d08e-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Zakończono przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Finished Workflow</span></span>
<span data-ttu-id="5d08e-453">Teraz, gdy naszych naszych przepływ pracy został zakończony, wykonaj inną toosee uruchomienia testu, przekaż go.</span><span class="sxs-lookup"><span data-stu-id="5d08e-453">Now that our our workflow is finished, do another test run toosee it pass.</span></span>

![Zakończono przepływu pracy dla danych wyjściowych mp4 wielu z miniaturami](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

<span data-ttu-id="5d08e-455">*Zakończono przepływu pracy dla danych wyjściowych mp4 wielu z miniaturami*</span><span class="sxs-lookup"><span data-stu-id="5d08e-455">*Finished workflow for multi-mp4 output with thumbnails*</span></span>

## <span data-ttu-id="5d08e-456"><a id="time_based_trim"></a>Na podstawie czasu przycinanie multibitrate MP4 danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="5d08e-456"><a id="time_based_trim"></a>Time-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="5d08e-457">Począwszy od przepływu pracy, który generuje [multibitrate MP4 wyjściowymi MXF wejściowych](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), możemy teraz będzie wyszukiwania do przycinanie hello źródła wideo oparte na sygnatury czasowe.</span><span class="sxs-lookup"><span data-stu-id="5d08e-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on time-stamps.</span></span>

### <span data-ttu-id="5d08e-458"><a id="time_based_trim_start"></a>Dodawanie przycinanie do toostart omówienie przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-458"><a id="time_based_trim_start"></a>Workflow overview toostart adding trimming to</span></span>
![Uruchamianie przepływu pracy tooadd przycinanie do](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

<span data-ttu-id="5d08e-460">*Uruchamianie przepływu pracy tooadd przycinanie do*</span><span class="sxs-lookup"><span data-stu-id="5d08e-460">*Starting workflow tooadd trimming to*</span></span>

### <span data-ttu-id="5d08e-461"><a id="time_based_trim_use_stream_trimmer"></a>Przy użyciu hello przycinarka strumienia</span><span class="sxs-lookup"><span data-stu-id="5d08e-461"><a id="time_based_trim_use_stream_trimmer"></a>Using hello Stream Trimmer</span></span>
<span data-ttu-id="5d08e-462">składnik przycinarka strumienia Hello umożliwia tootrim hello początek i koniec strumienia wejściowego podstawą informacji (sekundy, minuty,...). Przycinarka Hello nie obsługuje przycinania na podstawie ramki.</span><span class="sxs-lookup"><span data-stu-id="5d08e-462">hello Stream Trimmer component allows tootrim hello beginning and ending of an input stream base on timing information (seconds, minutes, ...). hello trimmer does not support frame-based trimming.</span></span>

![Przycinarka do strumienia](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

<span data-ttu-id="5d08e-464">*Przycinarka do strumienia*</span><span class="sxs-lookup"><span data-stu-id="5d08e-464">*Stream Trimmer*</span></span>

<span data-ttu-id="5d08e-465">Zamiast bezpośrednio łączenie koderów hello AVC i osoby mówiącej pozycji assigner toohello wejście pliku nośnika, będzie testujemy Between tych hello przycinarka strumienia.</span><span class="sxs-lookup"><span data-stu-id="5d08e-465">Instead of linking hello AVC encoders and speaker position assigner toohello Media File Input directly, we'll put in between those hello stream trimmer.</span></span> <span data-ttu-id="5d08e-466">(Jeden hello sygnał wideo i drugi dla hello przeplotu sygnału dźwiękowego).</span><span class="sxs-lookup"><span data-stu-id="5d08e-466">(One for hello video signal and one for hello interleaved audio signal.)</span></span>

![Umieść przycinarka strumienia między nimi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

<span data-ttu-id="5d08e-468">*Umieść przycinarka strumienia między nimi*</span><span class="sxs-lookup"><span data-stu-id="5d08e-468">*Put Stream Trimmer in between*</span></span>

<span data-ttu-id="5d08e-469">Skonfigurujmy przycinarka hello, dzięki czemu będą przetwarzane są jedynie wideo i audio między 15 sekund i 60 sekund na powitania wideo.</span><span class="sxs-lookup"><span data-stu-id="5d08e-469">Let's configure hello trimmer so that we will only process video and audio between 15 seconds and 60 seconds in hello video.</span></span>

<span data-ttu-id="5d08e-470">Przejdź do właściwości toohello hello przycinarka strumienia wideo i skonfigurować czas rozpoczęcia (15 s) i właściwości godzina zakończenia (60s).</span><span class="sxs-lookup"><span data-stu-id="5d08e-470">Go toohello properties of hello Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span></span> <span data-ttu-id="5d08e-471">toomake się, że zarówno naszych przycinarka audio i wideo są zawsze skonfigurowanego toohello sam rozpoczęcia i zakończenia wartości, firma Microsoft opublikuje tych głównego toohello hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="5d08e-471">toomake sure both our audio and video trimmer are always configured toohello same start and end values, we will publish those toohello root of hello workflow.</span></span>

![Publikowanie właściwości czasu rozpoczęcia z przycinarka strumienia](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

<span data-ttu-id="5d08e-473">*Publikowanie właściwości czasu rozpoczęcia z przycinarka strumienia*</span><span class="sxs-lookup"><span data-stu-id="5d08e-473">*Publish start time property from Stream Trimmer*</span></span>

![Okna dialogowego właściwości publikowania dla godziny rozpoczęcia](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

<span data-ttu-id="5d08e-475">*Okna dialogowego właściwości publikowania dla godziny rozpoczęcia*</span><span class="sxs-lookup"><span data-stu-id="5d08e-475">*Publish property dialog for start time*</span></span>

![Okna dialogowego właściwości publikowania dla godzina zakończenia](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

<span data-ttu-id="5d08e-477">*Okna dialogowego właściwości publikowania dla godzina zakończenia*</span><span class="sxs-lookup"><span data-stu-id="5d08e-477">*Publish property dialog for end time*</span></span>

<span data-ttu-id="5d08e-478">Jeśli mamy teraz sprawdzić głównego hello naszych przepływu pracy, obie właściwości będzie starannie wyświetlane i można skonfigurować z tego miejsca.</span><span class="sxs-lookup"><span data-stu-id="5d08e-478">If we now inspect hello root of our workflow, both properties will be neatly displayed and configurable from there.</span></span>

![Opublikowanych właściwości dostępne w folderze głównym](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

<span data-ttu-id="5d08e-480">*Opublikowanych właściwości dostępne w folderze głównym*</span><span class="sxs-lookup"><span data-stu-id="5d08e-480">*Published properties available on root*</span></span>

<span data-ttu-id="5d08e-481">Teraz Otwórz właściwości przycinanie hello z hello przycinarka audio i skonfigurować zarówno rozpoczęcia i zakończenia z wyrażeniem, które odwołuje się toohello opublikowane właściwości w katalogu głównym hello naszych przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="5d08e-481">Now open hello trimming properties from hello audio trimmer and configure both start and end times with an expression that refers toohello published properties on hello root of our workflow.</span></span>

<span data-ttu-id="5d08e-482">Czas rozpoczęcia przycinanie audio hello:</span><span class="sxs-lookup"><span data-stu-id="5d08e-482">For hello audio trimming start time:</span></span>

    ${ROOT_TrimmingStartTime}

<span data-ttu-id="5d08e-483">i jego czas zakończenia:</span><span class="sxs-lookup"><span data-stu-id="5d08e-483">and for its end time:</span></span>

    ${ROOT_TrimmingEndTime}

### <span data-ttu-id="5d08e-484"><a id="time_based_trim_finish"></a>Zakończono przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-484"><a id="time_based_trim_finish"></a>Finished Workflow</span></span>
![Zakończono przepływu pracy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

<span data-ttu-id="5d08e-486">*Zakończono przepływu pracy*</span><span class="sxs-lookup"><span data-stu-id="5d08e-486">*Finished Workflow*</span></span>

## <span data-ttu-id="5d08e-487"><a id="scripting"></a>Wprowadzenie hello składnika uwzględnione w skryptach</span><span class="sxs-lookup"><span data-stu-id="5d08e-487"><a id="scripting"></a>Introducing hello Scripted Component</span></span>
<span data-ttu-id="5d08e-488">Składniki inicjowanych przez skrypty można wykonywanie skryptów dowolnego podczas fazy wykonywania hello naszych przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="5d08e-488">Scripted Components can execute arbitrary scripts during hello execution phases of our workflow.</span></span> <span data-ttu-id="5d08e-489">Istnieją cztery różne skrypty, które mogą być wykonywane każdego z określonych parametrów i miejsca w cyklu życia hello przepływu pracy:</span><span class="sxs-lookup"><span data-stu-id="5d08e-489">There are four different scripts that can be executed, each with specific characteristics and their own place in hello workflow life-cycle:</span></span>

* <span data-ttu-id="5d08e-490">**commandScript**</span><span class="sxs-lookup"><span data-stu-id="5d08e-490">**commandScript**</span></span>
* <span data-ttu-id="5d08e-491">**realizeScript**</span><span class="sxs-lookup"><span data-stu-id="5d08e-491">**realizeScript**</span></span>
* <span data-ttu-id="5d08e-492">**processInputScript**</span><span class="sxs-lookup"><span data-stu-id="5d08e-492">**processInputScript**</span></span>
* <span data-ttu-id="5d08e-493">**lifeCycleScript**</span><span class="sxs-lookup"><span data-stu-id="5d08e-493">**lifeCycleScript**</span></span>

<span data-ttu-id="5d08e-494">w dokumentacji Hello hello inicjowanych przez skrypty składnika przechodzi bardziej szczegółowo dla każdego z powyższych hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-494">hello documentation of hello Scripted Component goes in more detail for each of hello above.</span></span> <span data-ttu-id="5d08e-495">W [hello następujących sekcji](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** skryptów składnika jest używane tooconstruct xml cliplist na bieżąco hello podczas uruchamiania przepływu pracy hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-495">In [hello following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** scripting component is used tooconstruct a cliplist xml on hello fly when hello workflow starts.</span></span> <span data-ttu-id="5d08e-496">Ten skrypt jest wywoływana podczas instalacji składnika hello, który odbywa się tylko raz w cyklu jego życia.</span><span class="sxs-lookup"><span data-stu-id="5d08e-496">This script is called during hello component setup, which happens only once in it's lifecycle.</span></span>

### <span data-ttu-id="5d08e-497"><a id="scripting_hello_world"></a>Obsługa skryptów w ramach przepływu pracy: Witaj świecie</span><span class="sxs-lookup"><span data-stu-id="5d08e-497"><a id="scripting_hello_world"></a>Scripting within a workflow: hello world</span></span>
<span data-ttu-id="5d08e-498">Przeciągnij składnik inicjowanych przez skrypty na powierzchnię projektanta hello i jego nazwa zostanie zmieniona (na przykład "SetClipListXML").</span><span class="sxs-lookup"><span data-stu-id="5d08e-498">Drag a Scripted Component onto hello designer surface and rename it (for example, "SetClipListXML").</span></span>

![Dodawanie skryptowej składnika](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="5d08e-500">*Dodawanie skryptowej składnika*</span><span class="sxs-lookup"><span data-stu-id="5d08e-500">*Adding a Scripted Component*</span></span>

<span data-ttu-id="5d08e-501">Gdy sprawdzić właściwości hello hello składnika uwzględnione w skryptach, cztery typy inny skrypt zostaną wyświetlone powitalne, każdy inny skrypt tooa można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="5d08e-501">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Przy użyciu skryptu właściwości składnika](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="5d08e-503">*Przy użyciu skryptu właściwości składnika*</span><span class="sxs-lookup"><span data-stu-id="5d08e-503">*Scripted Component properties*</span></span>

<span data-ttu-id="5d08e-504">Wyczyść hello processInputScript i Otwórz Edytor hello hello realizeScript.</span><span class="sxs-lookup"><span data-stu-id="5d08e-504">Clear hello processInputScript and open hello editor for hello realizeScript.</span></span> <span data-ttu-id="5d08e-505">Teraz możemy konfiguracji i gotowe toostart skryptów.</span><span class="sxs-lookup"><span data-stu-id="5d08e-505">Now we're set up and ready toostart scripting.</span></span>

<span data-ttu-id="5d08e-506">Skrypty są zapisywane w Groovy, dynamicznie skompilowanej język skryptów dla platformy Java hello, który zachowuje zgodność z językiem Java.</span><span class="sxs-lookup"><span data-stu-id="5d08e-506">Scripts are written in Groovy, a dynamically compiled scripting language for hello Java platform that retains compatibility with Java.</span></span> <span data-ttu-id="5d08e-507">W rzeczywistości większość kodu języka Java jest prawidłowym kodem Groovy.</span><span class="sxs-lookup"><span data-stu-id="5d08e-507">Actually, most Java code is valid Groovy code.</span></span>

<span data-ttu-id="5d08e-508">Napisz skrypt groovy proste hello world w kontekście hello naszych realizeScript.</span><span class="sxs-lookup"><span data-stu-id="5d08e-508">Let's write a simple hello world groovy script in hello context of our realizeScript.</span></span> <span data-ttu-id="5d08e-509">Wprowadź poniżej hello w edytorze hello:</span><span class="sxs-lookup"><span data-stu-id="5d08e-509">Enter hello following in hello editor:</span></span>

    node.log("hello world");

<span data-ttu-id="5d08e-510">Teraz można wykonać uruchomienia testu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="5d08e-510">Now execute a local test run.</span></span> <span data-ttu-id="5d08e-511">Po tym przebiegu inspekcji (za pośrednictwem karty systemu hello na hello inicjowanych przez skrypty składnika) hello właściwości dzienników.</span><span class="sxs-lookup"><span data-stu-id="5d08e-511">After this run, inspect (through hello System tab on hello Scripted Component) hello Logs property.</span></span>

![Witaj świecie dziennika w danych wyjściowych](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

<span data-ttu-id="5d08e-513">*Witaj świecie dziennika w danych wyjściowych*</span><span class="sxs-lookup"><span data-stu-id="5d08e-513">*Hello world log output*</span></span>

<span data-ttu-id="5d08e-514">Obiekt węzła Hello, który nazywamy metoda rejestrowania hello, odnosi się tooour bieżącego "węzła" lub hello składnika, który jest firma Microsoft skryptów w.</span><span class="sxs-lookup"><span data-stu-id="5d08e-514">hello node object we call hello log method on, refers tooour current "node" or hello component we're scripting within.</span></span> <span data-ttu-id="5d08e-515">Każdy składnik ma tak hello możliwości toooutput rejestrowania danych, dostępna za pośrednictwem karty system hello. W takim przypadku możemy output literał ciągu powitania "hello world".</span><span class="sxs-lookup"><span data-stu-id="5d08e-515">Every component as such has hello ability toooutput logging data, available through hello system tab. In this case, we output hello string literal "hello world".</span></span> <span data-ttu-id="5d08e-516">Tutaj toounderstand ważne jest, że to może okazać się toobe nieoceniony narzędzia debugowania, zapewniając wgląd, na jakich skryptów hello jest rzeczywiście ten.</span><span class="sxs-lookup"><span data-stu-id="5d08e-516">Important toounderstand here is that this can prove toobe an invaluable debugging tool, providing you with insight on what hello script is actually doing.</span></span>

<span data-ttu-id="5d08e-517">Od w naszym środowisku skryptów mamy także tooproperties dostępu na inne składniki.</span><span class="sxs-lookup"><span data-stu-id="5d08e-517">From within our scripting environment, we also have access tooproperties on other components.</span></span> <span data-ttu-id="5d08e-518">Wypróbuj:</span><span class="sxs-lookup"><span data-stu-id="5d08e-518">Try this:</span></span>

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

<span data-ttu-id="5d08e-519">Nasze okno Dziennik wyświetli nam hello następujące:</span><span class="sxs-lookup"><span data-stu-id="5d08e-519">Our log window will show us hello following:</span></span>

![Dane wyjściowe dziennika do uzyskiwania dostępu do ścieżki węzła](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

<span data-ttu-id="5d08e-521">*Dane wyjściowe dziennika do uzyskiwania dostępu do ścieżki węzła*</span><span class="sxs-lookup"><span data-stu-id="5d08e-521">*Log output for accessing node paths*</span></span>

## <span data-ttu-id="5d08e-522"><a id="frame_based_trim"></a>Przycinanie multibitrate MP4 dane wyjściowe na podstawie ramki</span><span class="sxs-lookup"><span data-stu-id="5d08e-522"><a id="frame_based_trim"></a>Frame-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="5d08e-523">Począwszy od przepływu pracy, który generuje [multibitrate MP4 wyjściowymi MXF wejściowych](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), możemy teraz będzie wyszukiwania do przycinanie hello źródła wideo na podstawie liczby ramki.</span><span class="sxs-lookup"><span data-stu-id="5d08e-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on frame counts.</span></span>

### <span data-ttu-id="5d08e-524"><a id="frame_based_trim_start"></a>Omówienie toostart Dodawanie przycinanie do planu</span><span class="sxs-lookup"><span data-stu-id="5d08e-524"><a id="frame_based_trim_start"></a>Blueprint overview toostart adding trimming to</span></span>
![Dodawanie przycinanie do toostart przepływu pracy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

<span data-ttu-id="5d08e-526">*Dodawanie przycinanie do toostart przepływu pracy*</span><span class="sxs-lookup"><span data-stu-id="5d08e-526">*Workflow toostart adding trimming to*</span></span>

### <span data-ttu-id="5d08e-527"><a id="frame_based_trim_clip_list"></a>Przy użyciu hello klip listy XML</span><span class="sxs-lookup"><span data-stu-id="5d08e-527"><a id="frame_based_trim_clip_list"></a>Using hello Clip List XML</span></span>
<span data-ttu-id="5d08e-528">Wszystkie poprzednie samouczki przepływu pracy My używamy hello składnika nośnika pliku wejściowego jako naszych wideo źródło danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="5d08e-528">In all previous workflow tutorials, we used hello Media File Input component as our video input source.</span></span> <span data-ttu-id="5d08e-529">W tym scenariuszu określonych, będzie używany składnik źródłowy listy klip hello zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="5d08e-529">For this specific scenario though, we'll be using hello Clip List Source component instead.</span></span> <span data-ttu-id="5d08e-530">Należy pamiętać, że nie należy hello preferowana metoda działania; tylko hello klip źródło listy jest używane w przypadku toodo rzeczywista Przyczyna tak (podobnie jak w hello poniżej przypadek, w którym czynione korzystanie z możliwości przycinanie listy klip hello).</span><span class="sxs-lookup"><span data-stu-id="5d08e-530">Note that this should not be hello preferred way of working; only use hello Clip List Source when there's a real reason toodo so (like in hello below case, where we're making use of hello clip list trimming capabilities).</span></span>

<span data-ttu-id="5d08e-531">tooswitch z naszych toohello wejściowy plik nośnika źródła listy klip, przeciągnij składnik źródłowy listy klip hello na powierzchni projektowej hello i połącz hello klip listy numeru pin toohello klip listy XML węzła XML hello projektanta przepływów pracy.</span><span class="sxs-lookup"><span data-stu-id="5d08e-531">tooswitch from our Media File Input toohello Clip List Source, drag hello Clip List Source component onto hello design surface and connect hello Clip List XML pin toohello Clip List XML node of hello workflow designer.</span></span> <span data-ttu-id="5d08e-532">Powinno to spowodować wypełnienie hello źródła listy klip z końcówek wyjściowych, zgodnie z tooour wejściowy plik wideo.</span><span class="sxs-lookup"><span data-stu-id="5d08e-532">This should populate hello Clip List Source with output pins, according tooour input video.</span></span> <span data-ttu-id="5d08e-533">Obecnie łączyć hello nieskompresowanych Audio i wideo nieskompresowanych numerów PIN z toohello źródła listy klip hello hello odpowiednich koderów AVC i Interleaver strumień Audio.</span><span class="sxs-lookup"><span data-stu-id="5d08e-533">Now connect hello Uncompressed Video and Uncompressed Audio pins from hello hello Clip List Source toohello respective AVC Encoders and Audio Stream Interleaver.</span></span> <span data-ttu-id="5d08e-534">Teraz Usuń hello wejściowy plik nośnika.</span><span class="sxs-lookup"><span data-stu-id="5d08e-534">Now remove hello Media File Input.</span></span>

![Zastąpione hello wejście pliku multimediów hello klip listy źródłowej](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

<span data-ttu-id="5d08e-536">*Zastąpione hello wejście pliku multimediów hello klip listy źródłowej*</span><span class="sxs-lookup"><span data-stu-id="5d08e-536">*Replaced hello Media File Input with hello Clip List Source*</span></span>

<span data-ttu-id="5d08e-537">składnik źródłowy listy klip Hello przyjmuje jako dane wejściowe "Klip listy XML".</span><span class="sxs-lookup"><span data-stu-id="5d08e-537">hello Clip List Source component takes as its input a "Clip List XML".</span></span> <span data-ttu-id="5d08e-538">Podczas wybierania tootest pliku źródłowego hello z lokalnie, ten klip listy xml jest wypełniana automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="5d08e-538">When selecting hello source file tootest with locally, this clip list xml is auto-populated for you.</span></span>

![Wypełnione automatycznie klip XML listy właściwości](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

<span data-ttu-id="5d08e-540">*Wypełnione automatycznie klip XML listy właściwości*</span><span class="sxs-lookup"><span data-stu-id="5d08e-540">*Auto-populated Clip List XML property*</span></span>

<span data-ttu-id="5d08e-541">Wyszukiwania nieco bliżej toohello xml, to, jak wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="5d08e-541">Looking a bit closer toohello xml, this is how it looks like:</span></span>

![Okno dialogowe listy klip Edycja](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

<span data-ttu-id="5d08e-543">*Okno dialogowe listy klip Edycja*</span><span class="sxs-lookup"><span data-stu-id="5d08e-543">*Edit clip list dialog*</span></span>

<span data-ttu-id="5d08e-544">To nie odzwierciedlać możliwości hello hello klip listy XML.</span><span class="sxs-lookup"><span data-stu-id="5d08e-544">This however does not reflect hello capabilities of hello clip list xml.</span></span> <span data-ttu-id="5d08e-545">Jedną z opcji naszym jest tooadd elementu "Przycinanie" w obszarze źródło audio, jak i wideo hello:</span><span class="sxs-lookup"><span data-stu-id="5d08e-545">One option we have is tooadd a "Trim" element under both hello video and audio source, like this:</span></span>

![Dodawanie listy klip toohello przycinania elementu](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

<span data-ttu-id="5d08e-547">*Dodawanie listy klip toohello przycinania elementu*</span><span class="sxs-lookup"><span data-stu-id="5d08e-547">*Adding a trim element toohello clip list*</span></span>

<span data-ttu-id="5d08e-548">Jeśli zmodyfikować xml listy klip hello takie powyżej i wykonać lokalnego uruchomienia testu, zobaczysz hello wideo został poprawnie przycięty od 10 do 20 sekund hello wideo.</span><span class="sxs-lookup"><span data-stu-id="5d08e-548">If you modify hello clip list xml like this above and perform a local test run, you'll see hello video correctly been trimmed between 10 and 20 seconds in hello video.</span></span>

<span data-ttu-id="5d08e-549">Sprzeczne toowhat odbywa się po wykonaniu przebiegu lokalnego, ale tego samego xml cliplist nie miałoby hello sam wpływ, po zastosowaniu w przepływ pracy uruchamiany w usłudze Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="5d08e-549">Contrary toowhat happens when you do a local run though, this very same cliplist xml would not have hello same effect when applied in a workflow that runs in Azure Media Services.</span></span> <span data-ttu-id="5d08e-550">Po wygenerowaniu koder Premium Azure jest uruchamiana, hello cliplist xml za każdym razem, gdy ponownie, oparte na powitania pliku wejściowego hello kodowanie podano zadania.</span><span class="sxs-lookup"><span data-stu-id="5d08e-550">When Azure Premium Encoder starts, hello cliplist xml is generated every time again, based on hello input file hello encoding job was given.</span></span> <span data-ttu-id="5d08e-551">Oznacza to, że wszelkie zmiany, nie na powitania xml Niestety zostanie przesłonięte.</span><span class="sxs-lookup"><span data-stu-id="5d08e-551">This means that any changes we do on hello xml would unfortunately be overridden.</span></span>

<span data-ttu-id="5d08e-552">xml cliplist hello toocounter są czyszczone po uruchomieniu zadania kodowania, firma Microsoft może ponownie wygenerować go na bieżąco hello zaraz po rozpoczęcia hello naszych przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="5d08e-552">toocounter hello cliplist xml being wiped when an encoding job is started, we can re-generate it on hello fly just after hello start of our workflow.</span></span> <span data-ttu-id="5d08e-553">Takie akcje niestandardowe mogą być pobierane przez co to jest nazywany "Inicjowanych przez skrypty Component".</span><span class="sxs-lookup"><span data-stu-id="5d08e-553">Such custom actions can be taken through what is called a "Scripted Component".</span></span> <span data-ttu-id="5d08e-554">Aby uzyskać więcej informacji, zobacz [Introducing hello inicjowanych przez skrypty składnika](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span><span class="sxs-lookup"><span data-stu-id="5d08e-554">For more information, see [Introducing hello Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span></span>

<span data-ttu-id="5d08e-555">Przeciągnij składnik inicjowanych przez skrypty na powierzchnię projektanta hello i zmień jego nazwę za "SetClipListXML".</span><span class="sxs-lookup"><span data-stu-id="5d08e-555">Drag a Scripted Component onto hello designer surface and rename it too"SetClipListXML".</span></span>

![Dodawanie skryptowej składnika](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="5d08e-557">*Dodawanie skryptowej składnika*</span><span class="sxs-lookup"><span data-stu-id="5d08e-557">*Adding a Scripted Component*</span></span>

<span data-ttu-id="5d08e-558">Gdy sprawdzić właściwości hello hello składnika uwzględnione w skryptach, cztery typy inny skrypt zostaną wyświetlone powitalne, każdy inny skrypt tooa można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="5d08e-558">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Przy użyciu skryptu właściwości składnika](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="5d08e-560">*Przy użyciu skryptu właściwości składnika*</span><span class="sxs-lookup"><span data-stu-id="5d08e-560">*Scripted Component properties*</span></span>

### <span data-ttu-id="5d08e-561"><a id="frame_based_trim_modify_clip_list"></a>Modyfikowanie listy klip hello ze składnika uwzględnione w skryptach</span><span class="sxs-lookup"><span data-stu-id="5d08e-561"><a id="frame_based_trim_modify_clip_list"></a>Modifying hello clip list from a Scripted Component</span></span>
<span data-ttu-id="5d08e-562">Zanim firma Microsoft może ponownie zapisać hello cliplist xml, który jest generowany podczas uruchamiania przepływu pracy, potrzebujemy toohave dostępu toohello cliplist xml właściwości i zawartość.</span><span class="sxs-lookup"><span data-stu-id="5d08e-562">Before we can re-write hello cliplist xml that is generated during workflow startup, we'll need toohave access toohello cliplist xml property and contents.</span></span> <span data-ttu-id="5d08e-563">Firma Microsoft może zrobić następująco:</span><span class="sxs-lookup"><span data-stu-id="5d08e-563">We can do so like this:</span></span>

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Przychodzące listy klip rejestrowany](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

<span data-ttu-id="5d08e-565">*Przychodzące listy klip rejestrowany*</span><span class="sxs-lookup"><span data-stu-id="5d08e-565">*Incoming clip list being logged*</span></span>

<span data-ttu-id="5d08e-566">Najpierw musimy toodetermine sposób z punktu, który do punktu, który chcemy tootrim hello wideo.</span><span class="sxs-lookup"><span data-stu-id="5d08e-566">First we need a way toodetermine from which point till which point we want tootrim hello video.</span></span> <span data-ttu-id="5d08e-567">Publikowanie tego użytkownika bez technical wygodne toohello hello przepływu pracy, toomake głównego toohello dwie właściwości hello wykresu.</span><span class="sxs-lookup"><span data-stu-id="5d08e-567">toomake this convenient toohello less-technical user of hello workflow, publish two properties toohello root of hello graph.</span></span> <span data-ttu-id="5d08e-568">toodo, kliknij prawym przyciskiem myszy powierzchnię projektanta hello i wybierz opcję "Dodaj właściwość":</span><span class="sxs-lookup"><span data-stu-id="5d08e-568">toodo this, right click hello designer surface and select "Add Property":</span></span>

* <span data-ttu-id="5d08e-569">Pierwszą właściwością: "ClippingTimeStart" typu: "Kod CZASOWY"</span><span class="sxs-lookup"><span data-stu-id="5d08e-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span></span>
* <span data-ttu-id="5d08e-570">Drugie właściwości: "ClippingTimeEnd" typu: "Kod CZASOWY"</span><span class="sxs-lookup"><span data-stu-id="5d08e-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span></span>

![Okno dialogowe właściwości Dodawanie czas uruchomienia wycinka](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

<span data-ttu-id="5d08e-572">*Okno dialogowe właściwości Dodawanie czas uruchomienia wycinka*</span><span class="sxs-lookup"><span data-stu-id="5d08e-572">*Add Property dialog for clipping start time*</span></span>

![Opublikowane wycinka właściwości czasu w katalogu głównym przepływu pracy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

<span data-ttu-id="5d08e-574">*Opublikowane wycinka właściwości czasu w katalogu głównym przepływu pracy*</span><span class="sxs-lookup"><span data-stu-id="5d08e-574">*Published clipping time props on workflow root*</span></span>

<span data-ttu-id="5d08e-575">Skonfiguruj zarówno właściwości tooa odpowiednią wartość:</span><span class="sxs-lookup"><span data-stu-id="5d08e-575">Configure both properties tooa suitable value:</span></span>

![Skonfiguruj hello wycinka właściwości rozpoczęcia i zakończenia](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

<span data-ttu-id="5d08e-577">*Skonfiguruj hello wycinka właściwości rozpoczęcia i zakończenia*</span><span class="sxs-lookup"><span data-stu-id="5d08e-577">*Configure hello clipping start and end properties*</span></span>

<span data-ttu-id="5d08e-578">Teraz z naszych skryptu, możemy uzyskać dostęp do obie właściwości, takie jak to:</span><span class="sxs-lookup"><span data-stu-id="5d08e-578">Now, from within our script, we can access both properties, like this:</span></span>

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Okno Dziennik przedstawiający początek i koniec wycinka](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

<span data-ttu-id="5d08e-580">*Okno Dziennik przedstawiający początek i koniec wycinka*</span><span class="sxs-lookup"><span data-stu-id="5d08e-580">*Log window showing start and end of clipping*</span></span>

<span data-ttu-id="5d08e-581">Umożliwia analizowanie ciągów kod czasowy hello w formie wygodniejsze toouse, przy użyciu proste wyrażenie regularne:</span><span class="sxs-lookup"><span data-stu-id="5d08e-581">Let's parse hello timecode strings into a more convenient toouse form, using a simple regular expression:</span></span>

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Okno Dziennik z danych wyjściowych przeanalizowany kod czasowy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

<span data-ttu-id="5d08e-583">*Okno Dziennik z danych wyjściowych przeanalizowany kod czasowy*</span><span class="sxs-lookup"><span data-stu-id="5d08e-583">*Log window with output of parsed timecode*</span></span>

<span data-ttu-id="5d08e-584">Dzięki tym informacjom wykonywanego mamy teraz zmodyfikować hello cliplist xml tooreflect hello rozpoczęcia i zakończenia dla hello potrzeby dokładnych ramki wycinka filmu hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-584">With this information at hand, we can now modify hello cliplist xml tooreflect hello start and end times for hello desired frame-accurate clipping of hello movie.</span></span>

![Elementy przycinania tooadd kodu skryptu](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

<span data-ttu-id="5d08e-586">*Elementy przycinania tooadd kodu skryptu*</span><span class="sxs-lookup"><span data-stu-id="5d08e-586">*Script code tooadd trim elements*</span></span>

<span data-ttu-id="5d08e-587">Zostało to zrobić za pomocą operacje na ciągach normalne manipulowanie.</span><span class="sxs-lookup"><span data-stu-id="5d08e-587">This was done through normal string manipulation operations.</span></span> <span data-ttu-id="5d08e-588">Hello wynikowy klipu listy xml nie są zapisywane właściwości clipListXML toohello hello głównego przepływu pracy za pomocą metody "setProperty" hello.</span><span class="sxs-lookup"><span data-stu-id="5d08e-588">hello resulting modified clip list xml is written back toohello clipListXML property on hello workflow root through hello "setProperty" method.</span></span> <span data-ttu-id="5d08e-589">Okno Dziennik powitania po innego testu będzie pokazują hello następujące:</span><span class="sxs-lookup"><span data-stu-id="5d08e-589">hello log window after another test run would show us hello following:</span></span>

![Rejestrowanie hello wynikowej listy clip](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

<span data-ttu-id="5d08e-591">*Rejestrowanie hello wynikowej listy clip*</span><span class="sxs-lookup"><span data-stu-id="5d08e-591">*Logging hello resulting clip list*</span></span>

<span data-ttu-id="5d08e-592">Czy toosee uruchomienia testu, jak strumienie audio i wideo hello została obcięta.</span><span class="sxs-lookup"><span data-stu-id="5d08e-592">Do a test-run toosee how hello video and audio streams have been clipped.</span></span> <span data-ttu-id="5d08e-593">Jak należy to zrobić więcej niż jednego uruchomienia testu z różnymi wartościami dla punktów przycinania hello, można zauważyć, że te będą nie brane pod uwagę jednak!</span><span class="sxs-lookup"><span data-stu-id="5d08e-593">As you'll do more than one test-run with different values for hello trimming points, you'll notice that those will not be taken into account however!</span></span> <span data-ttu-id="5d08e-594">Hello przyczyną tego błędu jest tego projektanta hello, w odróżnieniu od hello Azure środowiska uruchomieniowego, jest nie zastąpienie hello cliplist xml każdego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="5d08e-594">hello reason for this is that hello designer, unlike hello Azure runtime, does NOT override hello cliplist xml every run.</span></span> <span data-ttu-id="5d08e-595">Oznacza to, że tylko hello pierwszego uruchomienia ustawiono hello i wylogowywanie punktów, spowoduje hello xml tootransform, wszystkie inne hello razy naszych klauzuli guard (jeśli (clipListXML.indexOf ("<trim>") == -1)) uniemożliwi dodanie kolejnego przycinania hello przepływu pracy element, gdy istnieje już istnieje.</span><span class="sxs-lookup"><span data-stu-id="5d08e-595">This means that only hello very first time you have set hello in and out points, will cause hello xml tootransform, all hello other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent hello workflow from adding another trim element when there's already one present.</span></span>

<span data-ttu-id="5d08e-596">toomake naszych przepływu pracy wygodne tootest lokalnie, firma Microsoft najlepsze dodać niektóre porządkowania DOM kodu, który sprawdza, czy przycinania element został już istnieje.</span><span class="sxs-lookup"><span data-stu-id="5d08e-596">toomake our workflow convenient tootest locally, we best add some house-keeping code that inspects if a trim element was already present.</span></span> <span data-ttu-id="5d08e-597">Jeśli tak, możemy go usuń, aby móc kontynuować, modyfikując xml hello hello nowymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="5d08e-597">If so, we can remove it before continuing by modifying hello xml with hello new values.</span></span> <span data-ttu-id="5d08e-598">Zamiast przy użyciu zwykłego działań na ciągach, jest prawdopodobnie bezpieczniejsze toodo to za pośrednictwem obiektu rzeczywistych xml modelu analizy.</span><span class="sxs-lookup"><span data-stu-id="5d08e-598">Rather than using plain string manipulations, it's probably safer toodo this through real xml object model parsing.</span></span>

<span data-ttu-id="5d08e-599">Zanim jednak możemy dodać taki kod, poprosimy Cię o tooadd liczba instrukcje import u hello najpierw uruchomić naszych skryptu:</span><span class="sxs-lookup"><span data-stu-id="5d08e-599">Before we can add such code though, we'll need tooadd a number of import statements at hello start of our script first:</span></span>

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

<span data-ttu-id="5d08e-600">Następnie można dodać hello wymagane czyszczenie kodu:</span><span class="sxs-lookup"><span data-stu-id="5d08e-600">After this, we can add hello required cleaning code:</span></span>

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

<span data-ttu-id="5d08e-601">Ten kod przechodzi powyżej punktu hello jaką dodamy hello przycinania elementy toohello cliplist xml.</span><span class="sxs-lookup"><span data-stu-id="5d08e-601">This code goes just above hello point at which we add hello trim elements toohello cliplist xml.</span></span>

<span data-ttu-id="5d08e-602">Na tym etapie firma Microsoft mogą uruchamiać i modyfikować naszych przepływu pracy jako ile chcemy przy jednoczesnym zachowaniu hello zmiany zostały zastosowane kiedykolwiek czasu.</span><span class="sxs-lookup"><span data-stu-id="5d08e-602">At this point, we can run and modify our workflow as much as we want while having hello changes applied ever time.</span></span>    

### <span data-ttu-id="5d08e-603"><a id="frame_based_trim_clippingenabled_prop"></a>Dodawanie właściwości wygody ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="5d08e-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adding a ClippingEnabled convenience property</span></span>
<span data-ttu-id="5d08e-604">Jak nie powinny zawsze toohappen przycinanie, umożliwia Zakończ poza naszych przepływu pracy, dodając wygodny Flaga wartości logicznej, która wskazuje, czy chcemy tooenable przycinanie / wycinka.</span><span class="sxs-lookup"><span data-stu-id="5d08e-604">As you might not always want trimming toohappen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want tooenable trimming / clipping.</span></span>

<span data-ttu-id="5d08e-605">Podobnie jak przed, publikuje nowy katalog główny toohello właściwości, naszych przepływu pracy o nazwie "ClippingEnabled" typu "BOOLEAN".</span><span class="sxs-lookup"><span data-stu-id="5d08e-605">Just as before, publish a new property toohello root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span></span>

![Właściwości włączenia wycinka opublikowane](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

<span data-ttu-id="5d08e-607">*Właściwości włączenia wycinka opublikowane*</span><span class="sxs-lookup"><span data-stu-id="5d08e-607">*Published a property for enabling clipping*</span></span>

<span data-ttu-id="5d08e-608">Hello poniżej klauzuli guard proste możemy Sprawdź, czy wymagana jest przycinanie i zdecyduj, czy naszej listy klip jako takie wymaga toobe zmodyfikowane lub nie.</span><span class="sxs-lookup"><span data-stu-id="5d08e-608">With hello below simple guard clause, we can check if trimming is required and decide if our clip list as such needs toobe modified or not.</span></span>

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <span data-ttu-id="5d08e-609"><a id="code"></a>Kompletny kod</span><span class="sxs-lookup"><span data-stu-id="5d08e-609"><a id="code"></a>Complete code</span></span>
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a><span data-ttu-id="5d08e-610">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="5d08e-610">Also see</span></span>
[<span data-ttu-id="5d08e-611">Wprowadzenie do kodowania w Azure Media Services w wersji Premium</span><span class="sxs-lookup"><span data-stu-id="5d08e-611">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[<span data-ttu-id="5d08e-612">Jak tooUse Premium kodowania w usłudze Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="5d08e-612">How tooUse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[<span data-ttu-id="5d08e-613">Kodowanie zawartości na żądanie przy użyciu usługi Azure Media</span><span class="sxs-lookup"><span data-stu-id="5d08e-613">Encoding On-Demand Content with Azure Media Service</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

[<span data-ttu-id="5d08e-614">Formaty i kodeki usługi Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="5d08e-614">Media Encoder Premium Workflow Formats and Codecs</span></span>](media-services-premium-workflow-encoder-formats.md)

[<span data-ttu-id="5d08e-615">Przykładowe pliki przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="5d08e-615">Sample workflow files</span></span>](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[<span data-ttu-id="5d08e-616">Narzędzia usługi Azure Media Services Explorer</span><span class="sxs-lookup"><span data-stu-id="5d08e-616">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="5d08e-617">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="5d08e-617">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5d08e-618">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="5d08e-618">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
