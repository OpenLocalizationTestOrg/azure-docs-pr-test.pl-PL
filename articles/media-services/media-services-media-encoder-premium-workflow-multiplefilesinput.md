---
title: "aaaMultiple wejściowych plików i właściwości składnika za pomocą kodera Premium - Azure | Dokumentacja firmy Microsoft"
description: "W tym temacie wyjaśniono, jak toouse setRuntimeProperties toouse wprowadzania wielu plików i przekaż procesor multimediów Media Encoder Premium w przepływie pracy toohello danych niestandardowych."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: 7fb35bdd-9891-4401-a65b-ef3cc8190e8a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: xpouyat;anilmur;juliako
ms.openlocfilehash: e14d10fbf9669e0b88e5ba1c519f1ba5e0bafdd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="de73d-103">Używanie wielu plików wejściowych i właściwości składnika za pomocą kodera — wersja Premium</span><span class="sxs-lookup"><span data-stu-id="de73d-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="de73d-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="de73d-104">Overview</span></span>
<span data-ttu-id="de73d-105">Istnieją scenariusze, w których może być konieczne właściwości składnika toocustomize, określ zawartość XML listy klip lub wysyłania wielu plików wejściowych podczas przesyłania zadania hello **Media Encoder Premium w przepływie pracy** procesor multimediów.</span><span class="sxs-lookup"><span data-stu-id="de73d-105">There are scenarios in which you might need toocustomize component properties, specify Clip List XML content, or send multiple input files when you submit a task with hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="de73d-106">Przykłady to:</span><span class="sxs-lookup"><span data-stu-id="de73d-106">Some examples are:</span></span>

* <span data-ttu-id="de73d-107">Zastępując tekst wideo i ustawianie wartości tekstowej hello (na przykład hello bieżącą datę) w czasie wykonywania dla każdego wejściowego wideo.</span><span class="sxs-lookup"><span data-stu-id="de73d-107">Overlaying text on video and setting hello text value (for example, hello current date) at runtime for each input video.</span></span>
* <span data-ttu-id="de73d-108">Dostosowywanie hello klip listy XML (toospecify jednego lub kilku źródła plików, lub bez przycinania, itp.).</span><span class="sxs-lookup"><span data-stu-id="de73d-108">Customizing hello Clip List XML (toospecify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="de73d-109">Nakładanie obraz logo na powitania wejściowy plik wideo, gdy wideo hello jest zaszyfrowana.</span><span class="sxs-lookup"><span data-stu-id="de73d-109">Overlaying a logo image on hello input video while hello video is encoded.</span></span>
* <span data-ttu-id="de73d-110">Wiele kodowanie języka audio.</span><span class="sxs-lookup"><span data-stu-id="de73d-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="de73d-111">Witaj toolet **Media Encoder Premium w przepływie pracy** wiedzieć, że podczas tworzenia zadania hello lub wysyłania wielu plików wejściowych zmieniasz niektórych właściwości w przepływie pracy hello, masz toouse w ciągu konfiguracji, który zawiera  **setRuntimeProperties** i/lub **transcodeSource**.</span><span class="sxs-lookup"><span data-stu-id="de73d-111">toolet hello **Media Encoder Premium Workflow** know that you are changing some properties in hello workflow when you create hello task or send multiple input files, you have toouse a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="de73d-112">W tym temacie opisano sposób toouse je.</span><span class="sxs-lookup"><span data-stu-id="de73d-112">This topic explains how toouse them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="de73d-113">Składnia ciągu konfiguracji</span><span class="sxs-lookup"><span data-stu-id="de73d-113">Configuration string syntax</span></span>
<span data-ttu-id="de73d-114">tooset ciągu konfiguracji Hello w hello kodowania zadań używa dokument XML, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="de73d-114">hello configuration string tooset in hello encoding task uses an XML document that looks like this:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<transcodeRequest>
  <transcodeSource>
  </transcodeSource>
  <setRuntimeProperties>
    <property propertyPath="Media File Input/filename" value="VideoFileName.mp4" />
  </setRuntimeProperties>
</transcodeRequest>
```

<span data-ttu-id="de73d-115">Witaj poniżej znajduje się kod hello C#, służącą do odczytywania z pliku konfiguracji XML hello, zmodyfikuj go przy użyciu hello filename prawo wideo i przekazuje je toohello zadań w ramach zadania:</span><span class="sxs-lookup"><span data-stu-id="de73d-115">hello following is hello C# code that reads hello XML configuration from a file, update it with hello right video filename and passes it toohello task in a job:</span></span>

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass tooit hello name of hello 
// processor toouse for hello specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with hello encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify hello input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset toocontain hello results of hello job. 
// This output is specified as AssetCreationOptions.None, which 
// means hello output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a><span data-ttu-id="de73d-116">Dostosowywanie właściwości składnika</span><span class="sxs-lookup"><span data-stu-id="de73d-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="de73d-117">Właściwość z wartością proste</span><span class="sxs-lookup"><span data-stu-id="de73d-117">Property with a simple value</span></span>
<span data-ttu-id="de73d-118">W niektórych przypadkach jest przydatne toocustomize właściwości składnika wraz z hello pliku przepływu pracy, który będzie toobe wykonywane przez przepływ pracy Premium kodera multimediów.</span><span class="sxs-lookup"><span data-stu-id="de73d-118">In some cases, it is useful toocustomize a component property together with hello workflow file that is going toobe executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="de73d-119">Załóżmy, że przeznaczona tekst nakładki przepływu pracy na pliki wideo i hello tekstu (na przykład hello bieżącą datę) powinien toobe zestawu w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="de73d-119">Suppose you designed a workflow that overlays text on your videos, and hello text (for example, hello current date) is supposed toobe set at runtime.</span></span> <span data-ttu-id="de73d-120">Można to zrobić, wysyłając toobe tekst hello Ustaw jako hello nową wartość dla właściwości text hello hello nakładki składnika z hello kodowania zadań.</span><span class="sxs-lookup"><span data-stu-id="de73d-120">You can do this by sending hello text toobe set as hello new value for hello text property of hello overlay component from hello encoding task.</span></span> <span data-ttu-id="de73d-121">Ten mechanizm toochange można użyć innych właściwości składnika w przepływie pracy hello (takie jak pozycja hello lub kolor nakładki hello, hello szybkości transmisji bitów kodera hello AVC itp.).</span><span class="sxs-lookup"><span data-stu-id="de73d-121">You can use this mechanism toochange other properties of a component in hello workflow (such as hello position or color of hello overlay, hello bitrate of hello AVC encoder, etc.).</span></span>

<span data-ttu-id="de73d-122">**setRuntimeProperties** jest używane toooverride właściwości w składnikach hello hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="de73d-122">**setRuntimeProperties** is used toooverride a property in hello components of hello workflow.</span></span>

<span data-ttu-id="de73d-123">Przykład:</span><span class="sxs-lookup"><span data-stu-id="de73d-123">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text tooImage Converter/text" value="Today is Friday hello 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a><span data-ttu-id="de73d-124">Właściwość wartości XML</span><span class="sxs-lookup"><span data-stu-id="de73d-124">Property with an XML value</span></span>
<span data-ttu-id="de73d-125">Hermetyzuj tooset właściwości, która oczekuje wartości XML przy użyciu `<![CDATA[ and ]]>`.</span><span class="sxs-lookup"><span data-stu-id="de73d-125">tooset a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="de73d-126">Przykład:</span><span class="sxs-lookup"><span data-stu-id="de73d-126">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

> [!NOTE]
> <span data-ttu-id="de73d-127">Upewnij się, że tooput karetki zwracać tuż po `<![CDATA[`.</span><span class="sxs-lookup"><span data-stu-id="de73d-127">Make sure not tooput a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="de73d-128">wartości propertyPath</span><span class="sxs-lookup"><span data-stu-id="de73d-128">propertyPath value</span></span>
<span data-ttu-id="de73d-129">W poprzednich przykładach hello została hello propertyPath "/ Media pliku danych wejściowych/filename" lub "/ inactiveTimeout" lub "clipListXml".</span><span class="sxs-lookup"><span data-stu-id="de73d-129">In hello previous examples, hello propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="de73d-130">To jest ogólnie rzecz biorąc, hello nazwy składnika hello, a następnie nazwę hello hello właściwości.</span><span class="sxs-lookup"><span data-stu-id="de73d-130">This is, in general, hello name of hello component, then hello name of hello property.</span></span> <span data-ttu-id="de73d-131">Hello ścieżki może zawierać więcej lub mniej poziomów, takie jak "/ primarySourceFile" (ponieważ właściwość hello jest głównym hello hello przepływu pracy) lub "/ wideo przetwarzania/grafiki nakładki/nieprzezroczystość" (ponieważ hello nakładki znajduje się w grupie).</span><span class="sxs-lookup"><span data-stu-id="de73d-131">hello path can have more or fewer levels, like "/primarySourceFile" (because hello property is at hello root of hello workflow) or "/Video Processing/Graphic Overlay/Opacity" (because hello Overlay is in a group).</span></span>    

<span data-ttu-id="de73d-132">toocheck hello ścieżki i nazwy właściwości, użyj hello Akcja przycisku, który jest od razu, obok każdej właściwości.</span><span class="sxs-lookup"><span data-stu-id="de73d-132">toocheck hello path and property name, use hello action button that is immediately beside each property.</span></span> <span data-ttu-id="de73d-133">Można kliknąć ten przycisk, akcji i wybierz **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="de73d-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="de73d-134">Wyświetli możesz hello rzeczywistej nazwy właściwości hello i natychmiast powyżej, hello przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="de73d-134">This will show you hello actual name of hello property, and immediately above it, hello namespace.</span></span>

![Akcja i edytowanie](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Właściwość](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="de73d-137">Wiele plików wejściowych</span><span class="sxs-lookup"><span data-stu-id="de73d-137">Multiple input files</span></span>
<span data-ttu-id="de73d-138">Każde zadanie, aby przesłać toohello **Media Encoder Premium w przepływie pracy** wymaga dwóch zasobów:</span><span class="sxs-lookup"><span data-stu-id="de73d-138">Each task that you submit toohello **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="de73d-139">Witaj najpierw jest *zasobów przepływu pracy* zawierający plik przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="de73d-139">hello first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="de73d-140">Pliki przepływu pracy można zaprojektować przy użyciu hello [projektanta przepływów pracy](media-services-workflow-designer.md).</span><span class="sxs-lookup"><span data-stu-id="de73d-140">You can design workflow files by using hello [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="de73d-141">Witaj drugim jest *multimedialnej* zawierający hello nośnika pliki, które mają tooencode.</span><span class="sxs-lookup"><span data-stu-id="de73d-141">hello second one is a *Media Asset* that contains hello media file(s) that you want tooencode.</span></span>

<span data-ttu-id="de73d-142">Gdy wysyłasz wielu toohello pliki nośnika **Media Encoder Premium w przepływie pracy** Zastosuj następujące ograniczenia hello kodera,:</span><span class="sxs-lookup"><span data-stu-id="de73d-142">When you're sending multiple media files toohello **Media Encoder Premium Workflow** encoder, hello following constraints apply:</span></span>

* <span data-ttu-id="de73d-143">Wszystkie nośniki hello pliki muszą być w hello sam *multimedialnej*.</span><span class="sxs-lookup"><span data-stu-id="de73d-143">All hello media files must be in hello same *Media Asset*.</span></span> <span data-ttu-id="de73d-144">Używanie wielu zasobów nośnika nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="de73d-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="de73d-145">Należy ustawić plik podstawowy hello w tej zawartości nośnika (najlepiej, jeśli jest to hello głównego pliku wideo, który hello kodera monitu tooprocess).</span><span class="sxs-lookup"><span data-stu-id="de73d-145">You must set hello primary file in this Media Asset (ideally, this is hello main video file that hello encoder is asked tooprocess).</span></span>
* <span data-ttu-id="de73d-146">Jest konieczne toopass danych konfiguracji, który zawiera hello **setRuntimeProperties** i/lub **transcodeSource** elementu toohello procesora.</span><span class="sxs-lookup"><span data-stu-id="de73d-146">It is necessary toopass configuration data that includes hello **setRuntimeProperties** and/or **transcodeSource** element toohello processor.</span></span>
  * <span data-ttu-id="de73d-147">**setRuntimeProperties** jest właściwość filename hello toooverride używane lub inna właściwość w składnikach hello hello przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="de73d-147">**setRuntimeProperties** is used toooverride hello filename property or another property in hello components of hello workflow.</span></span>
  * <span data-ttu-id="de73d-148">**transcodeSource** jest używane toospecify hello zawartości XML listy obiektów.</span><span class="sxs-lookup"><span data-stu-id="de73d-148">**transcodeSource** is used toospecify hello Clip List XML content.</span></span>

<span data-ttu-id="de73d-149">Połączenia w przepływie pracy hello:</span><span class="sxs-lookup"><span data-stu-id="de73d-149">Connections in hello workflow:</span></span>

* <span data-ttu-id="de73d-150">Możesz użyć jednego lub kilku składników danych wejściowych plików nośnika i planowanie toouse **setRuntimeProperties** toospecify hello nazwy pliku, a następnie nie podłączaj hello plik podstawowy składnik numeru pin toothem.</span><span class="sxs-lookup"><span data-stu-id="de73d-150">If you use one or several Media File Input components and plan toouse **setRuntimeProperties** toospecify hello file name, then do not connect hello primary file component pin toothem.</span></span> <span data-ttu-id="de73d-151">Upewnij się, że istnieje połączenie między hello plik podstawowy obiekt i hello Input(s) pliku nośnika.</span><span class="sxs-lookup"><span data-stu-id="de73d-151">Make sure that there is no connection between hello primary file object and hello Media File Input(s).</span></span>
* <span data-ttu-id="de73d-152">Jeśli wolisz toouse XML listy obiektów i jeden składnik źródło nośnika, a następnie mogą jednocześnie połączyć ze sobą.</span><span class="sxs-lookup"><span data-stu-id="de73d-152">If you prefer toouse Clip List XML and one Media Source component, then you can connect both together.</span></span>

![Brak połączenia z podstawowym pliku źródłowym tooMedia plik danych wejściowych](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="de73d-154">*Brak połączenia z tooMedia plik podstawowy hello składników danych wejściowych plików, jeśli używana jest właściwość filename hello tooset setRuntimeProperties.*</span><span class="sxs-lookup"><span data-stu-id="de73d-154">*There is no connection from hello primary file tooMedia File Input component(s) if you use setRuntimeProperties tooset hello filename property.*</span></span>

![Połączenie z tooClip klip listy XML listy źródłowej](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="de73d-156">*Możesz łączyć tooMedia klip listy XML źródła i użyj transcodeSource.*</span><span class="sxs-lookup"><span data-stu-id="de73d-156">*You can connect Clip List XML tooMedia Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="de73d-157">Przytnij dostosowania XML listy</span><span class="sxs-lookup"><span data-stu-id="de73d-157">Clip List XML customization</span></span>
<span data-ttu-id="de73d-158">Można określić hello klip listy XML w przepływie pracy hello w czasie wykonywania za pomocą **transcodeSource** w konfiguracji hello ciągu XML.</span><span class="sxs-lookup"><span data-stu-id="de73d-158">You can specify hello Clip List XML in hello workflow at runtime by using **transcodeSource** in hello configuration string XML.</span></span> <span data-ttu-id="de73d-159">Wymaga to hello XML listy klip numeru pin toobe połączone toohello źródło nośnika dla składnika w przepływie pracy hello.</span><span class="sxs-lookup"><span data-stu-id="de73d-159">This requires hello Clip List XML pin toobe connected toohello Media Source component in hello workflow.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <transcodeSource>
      <clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
      </clipList>
    </transcodeSource>
    <setRuntimeProperties>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="de73d-160">Jeśli chcesz toouse /primarySourceFile toospecify te dane wyjściowe hello tooname właściwości plików za pomocą "Wyrażenia", a następnie zalecamy przekazanie hello klip listy XML jako właściwość *po* właściwości /primarySourceFile hello, tooavoid o hello listy klip ma zostać zastąpione przez ustawienie /primarySourceFile hello.</span><span class="sxs-lookup"><span data-stu-id="de73d-160">If you want toospecify /primarySourceFile toouse this property tooname hello output files by using 'Expressions', then we recommend passing hello Clip List XML as a property *after* hello /primarySourceFile property, tooavoid having hello Clip List be overridden by hello /primarySourceFile setting.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="c:\temp\start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="de73d-161">Z dodatkowych przycinanie dokładne ramki:</span><span class="sxs-lookup"><span data-stu-id="de73d-161">With additional frame-accurate trimming:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a><span data-ttu-id="de73d-162">Przykład 1: Nakładki obrazów na powitania wideo</span><span class="sxs-lookup"><span data-stu-id="de73d-162">Example 1 : Overlay an image on top of hello video</span></span>

### <a name="presentation"></a><span data-ttu-id="de73d-163">Prezentacji</span><span class="sxs-lookup"><span data-stu-id="de73d-163">Presentation</span></span>
<span data-ttu-id="de73d-164">Należy wziąć pod uwagę przykładem, w której ma zostać toooverlay obraz logo na powitania wejściowy plik wideo podczas wideo hello jest zaszyfrowana.</span><span class="sxs-lookup"><span data-stu-id="de73d-164">Consider an example in which you want toooverlay a logo image on hello input video while hello video is encoded.</span></span> <span data-ttu-id="de73d-165">W tym przykładzie hello wejściowy plik wideo ma nazwę "Microsoft_HoloLens_Possibilities_816p24.mp4" i hello logo nosi nazwę "logo.png".</span><span class="sxs-lookup"><span data-stu-id="de73d-165">In this example, hello input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and hello logo is named "logo.png".</span></span> <span data-ttu-id="de73d-166">Należy wykonać następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="de73d-166">You should perform hello following steps:</span></span>

* <span data-ttu-id="de73d-167">Utwórz zasób przepływu pracy z plikiem przepływu pracy hello (zobacz poniższy przykład hello).</span><span class="sxs-lookup"><span data-stu-id="de73d-167">Create a Workflow Asset with hello workflow file (see hello following example).</span></span>
* <span data-ttu-id="de73d-168">Utwórz zasób nośnika, który zawiera dwa pliki: MyInputVideo.mp4 jako hello plik podstawowy i MyLogo.png.</span><span class="sxs-lookup"><span data-stu-id="de73d-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as hello primary file and MyLogo.png.</span></span>
* <span data-ttu-id="de73d-169">Wyślij toohello zadania przepływu pracy Premium kodera multimediów nośnika zasoby procesora z powyższych hello danych wejściowych i określ powitania po ciągu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="de73d-169">Send a task toohello Media Encoder Premium Workflow media processor with hello above input assets and specify hello following configuration string.</span></span>

<span data-ttu-id="de73d-170">Konfiguracja:</span><span class="sxs-lookup"><span data-stu-id="de73d-170">Configuration:</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="de73d-171">W powyższym przykładzie hello hello nazwę pliku wideo hello są wysyłane toohello wejście pliku multimediów składnika i hello primarySourceFile właściwości.</span><span class="sxs-lookup"><span data-stu-id="de73d-171">In hello example above, hello name of hello video file is sent toohello Media File Input component and hello primarySourceFile property.</span></span> <span data-ttu-id="de73d-172">Witaj nazwę pliku logo hello są wysyłane tooanother nośnika plik danych wejściowych składnika graficzne nakładki toohello połączonych.</span><span class="sxs-lookup"><span data-stu-id="de73d-172">hello name of hello logo file is sent tooanother Media File Input that is connected toohello graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="de73d-173">Nazwa pliku wideo Hello są wysyłane toohello primarySourceFile właściwości.</span><span class="sxs-lookup"><span data-stu-id="de73d-173">hello video file name is sent toohello primarySourceFile property.</span></span> <span data-ttu-id="de73d-174">Witaj przyczyną tego błędu jest toouse tej właściwości w przepływie pracy hello do tworzenia nazwy pliku wyjściowego poprawne hello przy użyciu wyrażenia, np.</span><span class="sxs-lookup"><span data-stu-id="de73d-174">hello reason for this is toouse this property in hello workflow for building hello correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="de73d-175">Tworzenie krok przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="de73d-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="de73d-176">Poniżej przedstawiono hello toocreate czynności przepływu pracy, który przyjmuje dwa pliki jako dane wejściowe: i obrazu wideo.</span><span class="sxs-lookup"><span data-stu-id="de73d-176">Here are hello steps toocreate a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="de73d-177">Będzie ona nakładki hello obrazu na powitania wideo.</span><span class="sxs-lookup"><span data-stu-id="de73d-177">It will overlay hello image on top of hello video.</span></span>

<span data-ttu-id="de73d-178">Otwórz **projektanta przepływów pracy** i wybierz **pliku** > **nowy obszar roboczy** > **planu Transkodowanie**.</span><span class="sxs-lookup"><span data-stu-id="de73d-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="de73d-179">Witaj nowy przepływ pracy zawiera trzy elementy:</span><span class="sxs-lookup"><span data-stu-id="de73d-179">hello new workflow shows three elements:</span></span>

* <span data-ttu-id="de73d-180">Podstawowym pliku źródłowym</span><span class="sxs-lookup"><span data-stu-id="de73d-180">Primary Source File</span></span>
* <span data-ttu-id="de73d-181">Obcina listę XML</span><span class="sxs-lookup"><span data-stu-id="de73d-181">Clip List XML</span></span>
* <span data-ttu-id="de73d-182">Zawartości pliku wyjściowej</span><span class="sxs-lookup"><span data-stu-id="de73d-182">Output File/Asset</span></span>  

![Nowy przepływ pracy kodowania](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="de73d-184">*Nowy przepływ pracy kodowania*</span><span class="sxs-lookup"><span data-stu-id="de73d-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="de73d-185">W pliku wejściowego nośnika hello tooaccept kolejności Rozpocznij od dodania składnika nośnika pliku wejściowego.</span><span class="sxs-lookup"><span data-stu-id="de73d-185">In order tooaccept hello input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="de73d-186">tooadd przepływu pracy toohello składnika, poszukaj jej w polu wyszukiwania w repozytorium hello i przeciągnij hello potrzeby wpis na hello okienku projektanta.</span><span class="sxs-lookup"><span data-stu-id="de73d-186">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span>

<span data-ttu-id="de73d-187">Następnie dodaj toobe pliku wideo hello używanych do projektowania przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="de73d-187">Next, add hello video file toobe used for designing your workflow.</span></span> <span data-ttu-id="de73d-188">toodo tak, kliknij przycisk hello tła okienka w Projektancie przepływów pracy i poszukaj hello właściwości głównej pliku źródłowego w okienku po prawej stronie właściwości hello.</span><span class="sxs-lookup"><span data-stu-id="de73d-188">toodo so, click hello background pane in Workflow Designer and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="de73d-189">Kliknij ikonę folderu hello i wybierz hello odpowiedniego pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="de73d-189">Click hello folder icon and select hello appropriate video file.</span></span>

![Źródłowy plik podstawowy](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="de73d-191">*Źródłowy plik podstawowy*</span><span class="sxs-lookup"><span data-stu-id="de73d-191">*Primary File Source*</span></span>

<span data-ttu-id="de73d-192">Następnie określ plik wideo hello hello składnika danych wejściowych pliku nośnika.</span><span class="sxs-lookup"><span data-stu-id="de73d-192">Next, specify hello video file in hello Media File Input component.</span></span>   

![Źródło danych wejściowych plików multimedialnych](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="de73d-194">*Źródło danych wejściowych plików multimedialnych*</span><span class="sxs-lookup"><span data-stu-id="de73d-194">*Media File Input Source*</span></span>

<span data-ttu-id="de73d-195">Natychmiast po zakończeniu hello wejściowy plik nośnika składnik będzie sprawdzenie pliku hello i wypełnić jego dane wyjściowe numerów PIN tooreflect hello pliku, który go inspekcji.</span><span class="sxs-lookup"><span data-stu-id="de73d-195">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file that it inspected.</span></span>

<span data-ttu-id="de73d-196">Witaj następnym krokiem jest tooadd tooRec.709 "Updater typu danych wideo" toospecify hello kolor miejsca.</span><span class="sxs-lookup"><span data-stu-id="de73d-196">hello next step is tooadd a "Video Data Type Updater" toospecify hello color space tooRec.709.</span></span> <span data-ttu-id="de73d-197">Dodaj "Wideo Format konwertera" ustawiony typ układu/układu tooData = planarnych można konfigurować.</span><span class="sxs-lookup"><span data-stu-id="de73d-197">Add a "Video Format Converter" that is set tooData Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="de73d-198">Spowoduje to przekonwertowanie hello strumienia wideo o tooa formacie, który można podjąć jako źródło hello nakładki składnika.</span><span class="sxs-lookup"><span data-stu-id="de73d-198">This will convert hello video stream tooa format that can be taken as a source of hello overlay component.</span></span>

![wideo Updater typu danych i Format konwertera](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="de73d-200">*Aktualizator typu danych wideo i konwertera formatu*</span><span class="sxs-lookup"><span data-stu-id="de73d-200">*Video Data Type Updater and Format Converter*</span></span>

![Typ układu = planarnych można konfigurować](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<span data-ttu-id="de73d-202">*Typ układu jest konfigurowalne planarnych*</span><span class="sxs-lookup"><span data-stu-id="de73d-202">*Layout type is Configurable Planar*</span></span>

<span data-ttu-id="de73d-203">Następnie dodaj składnik nakładka wideo i połącz hello (nieskompresowanych) wideo numeru pin toohello (nieskompresowanych) wideo numeru pin hello nośnika plików wejściowych.</span><span class="sxs-lookup"><span data-stu-id="de73d-203">Next, add a Video Overlay component and connect hello (uncompressed) video pin toohello (uncompressed) video pin of hello media file input.</span></span>

<span data-ttu-id="de73d-204">Dodaj inny wejście nośnika (tooload hello logo plik), kliknij ten składnik i zmień jego nazwę za "Logo dane wejściowe w pliku nośnika", a następnie wybierz obraz (plik PNG na przykład) we właściwości pliku hello.</span><span class="sxs-lookup"><span data-stu-id="de73d-204">Add another Media File Input (tooload hello logo file), click on this component and rename it too"Media File Input Logo", and select an image (a .png file for example) in hello file property.</span></span> <span data-ttu-id="de73d-205">Połącz hello nieskompresowanych obrazu numeru pin toohello nieskompresowanych obrazu kod pin hello nakładki.</span><span class="sxs-lookup"><span data-stu-id="de73d-205">Connect hello Uncompressed image pin toohello Uncompressed image pin of hello overlay.</span></span>

![Nakładki źródła pliku składnika i obrazów](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="de73d-207">*Nakładki źródła pliku składnika i obrazów*</span><span class="sxs-lookup"><span data-stu-id="de73d-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="de73d-208">Jeśli chcesz, aby toomodify hello położenie logo hello na powitania wideo (na przykład może być tooposition go na 10 procent wylogowuje na górze hello lewym rogu hello wideo), wyczyść pole wyboru "Ręcznego wprowadzania" hello.</span><span class="sxs-lookup"><span data-stu-id="de73d-208">If you want toomodify hello position of hello logo on hello video (for example, you might want tooposition it at 10 percent off of hello top left corner of hello video), clear hello "Manual Input" check box.</span></span> <span data-ttu-id="de73d-209">Można to zrobić, ponieważ używają składnika danych wejściowych plik nośnika tooprovide hello logo pliku toohello nakładki.</span><span class="sxs-lookup"><span data-stu-id="de73d-209">You can do this because you are using a Media File Input tooprovide hello logo file toohello overlay component.</span></span>

![Pozycja nakładki](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="de73d-211">*Pozycja nakładki*</span><span class="sxs-lookup"><span data-stu-id="de73d-211">*Overlay position*</span></span>

<span data-ttu-id="de73d-212">tooencode hello tooH.264 strumienia wideo, dodać hello koder wideo AVC i powierzchni projektanta składników toohello AAC kodera.</span><span class="sxs-lookup"><span data-stu-id="de73d-212">tooencode hello video stream tooH.264, add hello AVC Video Encoder and AAC encoder components toohello designer surface.</span></span> <span data-ttu-id="de73d-213">Połącz hello numerów PIN.</span><span class="sxs-lookup"><span data-stu-id="de73d-213">Connect hello pins.</span></span>
<span data-ttu-id="de73d-214">Ustaw hello AAC koder i wybierz Format Audio konwersji/ustawienie: 2.0 (L, R).</span><span class="sxs-lookup"><span data-stu-id="de73d-214">Set up hello AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![Kodery audio i wideo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="de73d-216">*Kodery audio i wideo*</span><span class="sxs-lookup"><span data-stu-id="de73d-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="de73d-217">Teraz Dodaj hello **ISO Mpeg-4 multiplekser** i **dane wyjściowe pliku** składników i podłącz hello numerów PIN, jak pokazano.</span><span class="sxs-lookup"><span data-stu-id="de73d-217">Now add hello **ISO Mpeg-4 Multiplexer** and **File Output** components and connect hello pins as shown.</span></span>

![MP4 multiplekser i danych wyjściowych w pliku](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="de73d-219">*MP4 multiplekser i danych wyjściowych w pliku*</span><span class="sxs-lookup"><span data-stu-id="de73d-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="de73d-220">Należy tooset hello nazwę pliku wyjściowego hello.</span><span class="sxs-lookup"><span data-stu-id="de73d-220">You need tooset hello name for hello output file.</span></span> <span data-ttu-id="de73d-221">Kliknij przycisk hello **dane wyjściowe pliku** wyrażenia hello składnika i edycja pliku hello:</span><span class="sxs-lookup"><span data-stu-id="de73d-221">Click hello **File Output** component and edit hello expression for hello file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Nazwa pliku wyjściowego](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="de73d-223">*Nazwa pliku wyjściowego*</span><span class="sxs-lookup"><span data-stu-id="de73d-223">*File output name*</span></span>

<span data-ttu-id="de73d-224">Można uruchomić przepływu pracy hello lokalnie toocheck, czy działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="de73d-224">You can run hello workflow locally toocheck that it is running correctly.</span></span>

<span data-ttu-id="de73d-225">Po jej zakończeniu, można go uruchomić w usłudze Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="de73d-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="de73d-226">Najpierw przygotować zasobów w usłudze Azure Media Services z dwoma plikami w nim: hello plików wideo i hello logo.</span><span class="sxs-lookup"><span data-stu-id="de73d-226">First, prepare an asset in Azure Media Services with two files in it: hello video file and hello logo.</span></span> <span data-ttu-id="de73d-227">Można to zrobić za pomocą hello .NET lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="de73d-227">You can do this by using hello .NET or REST API.</span></span> <span data-ttu-id="de73d-228">Również można to zrobić za pomocą portalu Azure hello lub [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span><span class="sxs-lookup"><span data-stu-id="de73d-228">You can also do this by using hello Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="de73d-229">W tym samouczku przedstawiono sposób toomanage zasobów z AMSE.</span><span class="sxs-lookup"><span data-stu-id="de73d-229">This tutorial shows you how toomanage assets with AMSE.</span></span> <span data-ttu-id="de73d-230">Istnieją dwa sposoby tooadd pliki tooan zasobów:</span><span class="sxs-lookup"><span data-stu-id="de73d-230">There are two ways tooadd files tooan asset:</span></span>

* <span data-ttu-id="de73d-231">Utwórz folder lokalny, skopiuj hello dwa pliki i przeciągnij i upuść hello folderu toohello **zasobów** kartę.</span><span class="sxs-lookup"><span data-stu-id="de73d-231">Create a local folder, copy hello two files in it, and drag and drop hello folder toohello **Asset** tab.</span></span>
* <span data-ttu-id="de73d-232">Przekazywanie pliku wideo hello jako zasób, wyświetlane informacje o zasobie hello, przejdź na kartę Pliki toohello i przekazać plik dodatkowy (logo).</span><span class="sxs-lookup"><span data-stu-id="de73d-232">Upload hello video file as an asset, display hello asset information, go toohello files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="de73d-233">Upewnij się, że tooset plik podstawowy w hello zasobów (hello głównego pliku wideo).</span><span class="sxs-lookup"><span data-stu-id="de73d-233">Make sure tooset a primary file in hello asset (hello main video file).</span></span>

![Pliki zasobów w AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="de73d-235">*Pliki zasobów w AMSE*</span><span class="sxs-lookup"><span data-stu-id="de73d-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="de73d-236">Wybierz hello zasobów, a tooencode go za pomocą kodera Premium.</span><span class="sxs-lookup"><span data-stu-id="de73d-236">Select hello asset and choose tooencode it with Premium Encoder.</span></span> <span data-ttu-id="de73d-237">Przekaż hello przepływu pracy i zaznacz go.</span><span class="sxs-lookup"><span data-stu-id="de73d-237">Upload hello workflow and select it.</span></span>

<span data-ttu-id="de73d-238">Kliknij hello przycisk toopass danych toohello procesora i dodaj następujące właściwości środowisko uruchomieniowe hello tooset XML hello:</span><span class="sxs-lookup"><span data-stu-id="de73d-238">Click hello button toopass data toohello processor, and add hello following XML tooset hello runtime properties:</span></span>

![Koder Premium w AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="de73d-240">*Koder Premium w AMSE*</span><span class="sxs-lookup"><span data-stu-id="de73d-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="de73d-241">Następnie wklej powitania po danych XML.</span><span class="sxs-lookup"><span data-stu-id="de73d-241">Then, paste hello following XML data.</span></span> <span data-ttu-id="de73d-242">Należy toospecify hello nazwę pliku wideo hello hello wejście pliku multimediów i primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="de73d-242">You need toospecify hello name of hello video file for both hello Media File Input and primarySourceFile.</span></span> <span data-ttu-id="de73d-243">Określ nazwę hello hello nazwę pliku dla hello logo zbyt.</span><span class="sxs-lookup"><span data-stu-id="de73d-243">Specify hello name of hello file name for hello logo too.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

![setRuntimeProperties](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture20_amsexmldata.png)

<span data-ttu-id="de73d-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="de73d-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="de73d-246">Jeśli używasz hello toocreate zestawu .NET SDK i uruchom zadanie hello, dane XML ma toobe przekazywane jako parametry konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="de73d-246">If you use hello .NET SDK toocreate and run hello task, this XML data has toobe passed as hello configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="de73d-247">Po zakończeniu zadania hello plik hello MP4 w hello danych wyjściowych zasobów wyświetla nakładki hello!</span><span class="sxs-lookup"><span data-stu-id="de73d-247">After hello job is complete, hello MP4 file in hello output asset displays hello overlay!</span></span>

![Nakładki na powitania wideo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="de73d-249">*Nakładki na powitania wideo*</span><span class="sxs-lookup"><span data-stu-id="de73d-249">*Overlay on hello video*</span></span>

<span data-ttu-id="de73d-250">Możesz pobrać hello przykładowego przepływu pracy z [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span><span class="sxs-lookup"><span data-stu-id="de73d-250">You can download hello sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="de73d-251">Przykład 2: Wiele audio kodowanie</span><span class="sxs-lookup"><span data-stu-id="de73d-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="de73d-252">Przykładem wiele wersji językowych audio kodowania workfkow jest dostępna w [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span><span class="sxs-lookup"><span data-stu-id="de73d-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="de73d-253">Ten folder zawiera przykładowy przepływ pracy, które mogą być używane tooencode MXF pliku tooa MP4 wielu plików zasobów z wielu ścieżek audio.</span><span class="sxs-lookup"><span data-stu-id="de73d-253">This folder contains a sample workflow which can be used tooencode a MXF file tooa multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="de73d-254">Ten przepływ pracy przyjęto założenie, że plik MXF hello zawiera jedną ścieżkę audio; dodatkowe ścieżki audio Hello powinien zostać przekazany jako osobne pliki audio (WAV lub MP4...).</span><span class="sxs-lookup"><span data-stu-id="de73d-254">This workflow assumes that hello MXF file contains one audio track ; hello additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="de73d-255">tooencode, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="de73d-255">tooencode, please follow these steps:</span></span>

* <span data-ttu-id="de73d-256">Utwórz zasób usługi Media Services z pliku MXF hello i hello Audio plików (0 too18 audio).</span><span class="sxs-lookup"><span data-stu-id="de73d-256">Create a Media Services asset with hello MXF file and hello Audio files (0 too18 audio files).</span></span>
* <span data-ttu-id="de73d-257">Upewnij się, że plik MXF hello jest ustawiony jako plik podstawowy.</span><span class="sxs-lookup"><span data-stu-id="de73d-257">Make sure that hello MXF file is set as a primary file.</span></span>
* <span data-ttu-id="de73d-258">Utwórz zadania i zadania przy użyciu hello koder Premium przepływu pracy procesora.</span><span class="sxs-lookup"><span data-stu-id="de73d-258">Create a job and a task using hello Premium Workflow Encoder processor.</span></span> <span data-ttu-id="de73d-259">Za pomocą przepływu pracy hello podane (MultiMP4-1080p-19audio-v1.workflow).</span><span class="sxs-lookup"><span data-stu-id="de73d-259">Use hello workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="de73d-260">Przekaż hello setruntime.xml danych toohello zadań (Jeśli używasz Eksploratora usługi Azure Media, przycisk "Przekaż przepływ pracy toohello danych xml" hello).</span><span class="sxs-lookup"><span data-stu-id="de73d-260">Pass hello setruntime.xml data toohello task (if you use Azure Media Services Explorer, use hello “pass xml data toohello workflow” button).</span></span>
  * <span data-ttu-id="de73d-261">Zaktualizuj hello danych toospecify hello poprawny plik nazwy i języków tagów XML.</span><span class="sxs-lookup"><span data-stu-id="de73d-261">Please update hello XML data toospecify hello correct file names and languages tags.</span></span>
  * <span data-ttu-id="de73d-262">przepływ pracy Hello ma audio składniki o nazwie tooAudio Audio 1 18.</span><span class="sxs-lookup"><span data-stu-id="de73d-262">hello workflow has audio components named Audio 1 tooAudio 18.</span></span>
  * <span data-ttu-id="de73d-263">RFC5646 znacznik języka hello jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="de73d-263">RFC5646 is supported for hello language tag.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
<transcodeRequest>
  <setRuntimeProperties>
    <property propertyPath="Media File Input Video/filename" value="MainVideo.mxf" />
    <property propertyPath="Language/language_code" value="en" />
    <property propertyPath="/primarySourceFile" value="MainVideo.mxf" />
    <property propertyPath="Audio 1/Media File Input/filename" value="french-audio.wav" />
    <property propertyPath="Audio 1/Language/language_code" value="fr" />
    <property propertyPath="Audio 2/Media File Input/filename" value="german-audio.wav" />
    <property propertyPath="Audio 2/Language/language_code" value="de" />
    <property propertyPath="Audio 3/Media File Input/filename" value="japanese-audio.wav" />
    <property propertyPath="Audio 3/Language/language_code" value="ja" />
  </setRuntimeProperties>
</transcodeRequest>
```

* <span data-ttu-id="de73d-264">Hello zakodowane zasobów będzie zawierać ścieżek audio multi języka i tych ścieżek powinien być możliwy w programie Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="de73d-264">hello encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="de73d-265">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="de73d-265">See also</span></span>
* [<span data-ttu-id="de73d-266">Wprowadzenie do kodowania w Azure Media Services w wersji Premium</span><span class="sxs-lookup"><span data-stu-id="de73d-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="de73d-267">Jak toouse Premium kodowania w usłudze Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="de73d-267">How toouse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="de73d-268">Kodowanie zawartości na żądanie za pomocą usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="de73d-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="de73d-269">Koderów-dekoderów i formaty Media Encoder Premium w przepływie pracy</span><span class="sxs-lookup"><span data-stu-id="de73d-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="de73d-270">Przykładowe pliki przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="de73d-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="de73d-271">Narzędzia usługi Azure Media Services Explorer</span><span class="sxs-lookup"><span data-stu-id="de73d-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="de73d-272">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="de73d-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="de73d-273">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="de73d-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
