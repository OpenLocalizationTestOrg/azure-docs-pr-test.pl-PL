---
title: "Wiele plików wejściowych i właściwości składnika za pomocą kodera Premium - Azure | Dokumentacja firmy Microsoft"
description: "W tym temacie wyjaśniono, jak używać setRuntimeProperties korzystanie z wielu plików wejściowych i przekazywanie danych niestandardowych do przepływu pracy Premium kodera multimediów procesor multimediów."
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
ms.openlocfilehash: df1ee5089a0af6ffce1431b658843fcb34a66ce5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="4151d-103">Używanie wielu plików wejściowych i właściwości składnika za pomocą kodera — wersja Premium</span><span class="sxs-lookup"><span data-stu-id="4151d-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="4151d-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="4151d-104">Overview</span></span>
<span data-ttu-id="4151d-105">Istnieją scenariusze, w których może być konieczne dostosowanie właściwości składnika, określ zawartość XML listy klip lub wysłać wielu plików wejściowych podczas przesyłania zadania z **Media Encoder Premium w przepływie pracy** procesor multimediów.</span><span class="sxs-lookup"><span data-stu-id="4151d-105">There are scenarios in which you might need to customize component properties, specify Clip List XML content, or send multiple input files when you submit a task with the **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="4151d-106">Przykłady to:</span><span class="sxs-lookup"><span data-stu-id="4151d-106">Some examples are:</span></span>

* <span data-ttu-id="4151d-107">Zastępując tekst na wideo i ustawianie wartości tekstowej (na przykład data bieżąca) w czasie wykonywania dla każdego wejściowego wideo.</span><span class="sxs-lookup"><span data-stu-id="4151d-107">Overlaying text on video and setting the text value (for example, the current date) at runtime for each input video.</span></span>
* <span data-ttu-id="4151d-108">Dostosowywanie XML listy klip (Aby określić jedną lub kilka plików źródłowych z lub bez przycinania, itp.).</span><span class="sxs-lookup"><span data-stu-id="4151d-108">Customizing the Clip List XML (to specify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="4151d-109">Gdy wideo jest zaszyfrowana, zastępując obraz logo na wejściowego pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="4151d-109">Overlaying a logo image on the input video while the video is encoded.</span></span>
* <span data-ttu-id="4151d-110">Wiele kodowanie języka audio.</span><span class="sxs-lookup"><span data-stu-id="4151d-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="4151d-111">Aby umożliwić **Media Encoder Premium w przepływie pracy** wiedzieć, że niektóre właściwości w przepływie pracy jest zmieniany podczas tworzenia zadania lub wysyłania wielu plików wejściowych, należy użyć ciągu konfiguracji, który zawiera  **setRuntimeProperties** i/lub **transcodeSource**.</span><span class="sxs-lookup"><span data-stu-id="4151d-111">To let the **Media Encoder Premium Workflow** know that you are changing some properties in the workflow when you create the task or send multiple input files, you have to use a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="4151d-112">W tym temacie opisano sposób korzystania z nich.</span><span class="sxs-lookup"><span data-stu-id="4151d-112">This topic explains how to use them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="4151d-113">Składnia ciągu konfiguracji</span><span class="sxs-lookup"><span data-stu-id="4151d-113">Configuration string syntax</span></span>
<span data-ttu-id="4151d-114">Ciąg konfiguracji można ustawić w zadaniu kodowania używa dokument XML, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="4151d-114">The configuration string to set in the encoding task uses an XML document that looks like this:</span></span>

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

<span data-ttu-id="4151d-115">Oto kod C#, który odczytuje plik XML konfiguracji z pliku, go zaktualizować z użyciem nazwy pliku prawo wideo i przekazuje je do zadań w ramach zadania:</span><span class="sxs-lookup"><span data-stu-id="4151d-115">The following is the C# code that reads the XML configuration from a file, update it with the right video filename and passes it to the task in a job:</span></span>

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass to it the name of the 
// processor to use for the specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with the encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify the input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset to contain the results of the job. 
// This output is specified as AssetCreationOptions.None, which 
// means the output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a><span data-ttu-id="4151d-116">Dostosowywanie właściwości składnika</span><span class="sxs-lookup"><span data-stu-id="4151d-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="4151d-117">Właściwość z wartością proste</span><span class="sxs-lookup"><span data-stu-id="4151d-117">Property with a simple value</span></span>
<span data-ttu-id="4151d-118">W niektórych przypadkach warto dostosować właściwości składnika wraz z pliku przepływu pracy, który ma być wykonywane przez przepływ pracy Premium kodera multimediów.</span><span class="sxs-lookup"><span data-stu-id="4151d-118">In some cases, it is useful to customize a component property together with the workflow file that is going to be executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="4151d-119">Załóżmy, że przeznaczona tekst nakładki przepływu pracy na pliki wideo i tekst (na przykład data bieżąca) powinien można ustawić w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="4151d-119">Suppose you designed a workflow that overlays text on your videos, and the text (for example, the current date) is supposed to be set at runtime.</span></span> <span data-ttu-id="4151d-120">Można to zrobić, wysyłając tekst, który ma być ustawiona jako nową wartość właściwości text składnika nakładkę z zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="4151d-120">You can do this by sending the text to be set as the new value for the text property of the overlay component from the encoding task.</span></span> <span data-ttu-id="4151d-121">Mechanizm ten umożliwia zmienić inne właściwości składnika w przepływie pracy (na przykład położenia lub kolor nakładki, szybkości transmisji bitów kodera AVC itp.).</span><span class="sxs-lookup"><span data-stu-id="4151d-121">You can use this mechanism to change other properties of a component in the workflow (such as the position or color of the overlay, the bitrate of the AVC encoder, etc.).</span></span>

<span data-ttu-id="4151d-122">**setRuntimeProperties** służy do zastępowania właściwość składniki przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="4151d-122">**setRuntimeProperties** is used to override a property in the components of the workflow.</span></span>

<span data-ttu-id="4151d-123">Przykład:</span><span class="sxs-lookup"><span data-stu-id="4151d-123">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text To Image Converter/text" value="Today is Friday the 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a><span data-ttu-id="4151d-124">Właściwość wartości XML</span><span class="sxs-lookup"><span data-stu-id="4151d-124">Property with an XML value</span></span>
<span data-ttu-id="4151d-125">Aby ustawić właściwości, która oczekuje wartości XML, Hermetyzowanie przy użyciu `<![CDATA[ and ]]>`.</span><span class="sxs-lookup"><span data-stu-id="4151d-125">To set a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="4151d-126">Przykład:</span><span class="sxs-lookup"><span data-stu-id="4151d-126">Example:</span></span>

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
> <span data-ttu-id="4151d-127">Upewnij się, że nie można umieścić powrotu karetki tuż po `<![CDATA[`.</span><span class="sxs-lookup"><span data-stu-id="4151d-127">Make sure not to put a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="4151d-128">wartości propertyPath</span><span class="sxs-lookup"><span data-stu-id="4151d-128">propertyPath value</span></span>
<span data-ttu-id="4151d-129">W poprzednich przykładach, została propertyPath "/ Media pliku danych wejściowych/filename" lub "/ inactiveTimeout" lub "clipListXml".</span><span class="sxs-lookup"><span data-stu-id="4151d-129">In the previous examples, the propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="4151d-130">To jest ogólnie rzecz biorąc, nazwy składnika, a następnie nazwę właściwości.</span><span class="sxs-lookup"><span data-stu-id="4151d-130">This is, in general, the name of the component, then the name of the property.</span></span> <span data-ttu-id="4151d-131">Ścieżka może mieć więcej lub mniej poziomy, tak samo, jak "/ primarySourceFile" (ponieważ jest właściwość w katalogu głównym przepływu pracy) lub "/ wideo przetwarzania/grafiki nakładki/nieprzezroczystość" (ponieważ nakładki znajduje się w grupie).</span><span class="sxs-lookup"><span data-stu-id="4151d-131">The path can have more or fewer levels, like "/primarySourceFile" (because the property is at the root of the workflow) or "/Video Processing/Graphic Overlay/Opacity" (because the Overlay is in a group).</span></span>    

<span data-ttu-id="4151d-132">Aby sprawdzić ścieżki i nazwy właściwości, użyj przycisku akcji, który jest od razu obok każdej właściwości.</span><span class="sxs-lookup"><span data-stu-id="4151d-132">To check the path and property name, use the action button that is immediately beside each property.</span></span> <span data-ttu-id="4151d-133">Można kliknąć ten przycisk, akcji i wybierz **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="4151d-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="4151d-134">Spowoduje to wyświetlenie rzeczywistą nazwą właściwości oraz od razu nad nim przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="4151d-134">This will show you the actual name of the property, and immediately above it, the namespace.</span></span>

![Akcja i edytowanie](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Właściwość](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="4151d-137">Wiele plików wejściowych</span><span class="sxs-lookup"><span data-stu-id="4151d-137">Multiple input files</span></span>
<span data-ttu-id="4151d-138">Każdego zadania, które można przesłać do **Media Encoder Premium w przepływie pracy** wymaga dwóch zasobów:</span><span class="sxs-lookup"><span data-stu-id="4151d-138">Each task that you submit to the **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="4151d-139">Pierwsza z nich jest *zasobów przepływu pracy* zawierający plik przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="4151d-139">The first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="4151d-140">Pliki przepływu pracy można zaprojektować przy użyciu [projektanta przepływów pracy](media-services-workflow-designer.md).</span><span class="sxs-lookup"><span data-stu-id="4151d-140">You can design workflow files by using the [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="4151d-141">Drugim jest *multimedialnej* zawierający pliki nośnika, który chcesz kodować.</span><span class="sxs-lookup"><span data-stu-id="4151d-141">The second one is a *Media Asset* that contains the media file(s) that you want to encode.</span></span>

<span data-ttu-id="4151d-142">Gdy wysyłasz wiele plików multimedialnych **Media Encoder Premium w przepływie pracy** kodera, obowiązują następujące ograniczenia:</span><span class="sxs-lookup"><span data-stu-id="4151d-142">When you're sending multiple media files to the **Media Encoder Premium Workflow** encoder, the following constraints apply:</span></span>

* <span data-ttu-id="4151d-143">Wszystkie pliki multimedialne musi być w tej samej *multimedialnej*.</span><span class="sxs-lookup"><span data-stu-id="4151d-143">All the media files must be in the same *Media Asset*.</span></span> <span data-ttu-id="4151d-144">Używanie wielu zasobów nośnika nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="4151d-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="4151d-145">Plik podstawowy musi być ustawiona w tej zawartości nośnika (najlepiej, jeśli jest to główny plik wideo, który musi przetworzyć koder).</span><span class="sxs-lookup"><span data-stu-id="4151d-145">You must set the primary file in this Media Asset (ideally, this is the main video file that the encoder is asked to process).</span></span>
* <span data-ttu-id="4151d-146">Należy przekazać dane konfiguracji, który zawiera **setRuntimeProperties** i/lub **transcodeSource** element do procesora.</span><span class="sxs-lookup"><span data-stu-id="4151d-146">It is necessary to pass configuration data that includes the **setRuntimeProperties** and/or **transcodeSource** element to the processor.</span></span>
  * <span data-ttu-id="4151d-147">**setRuntimeProperties** służy do zastępowania właściwość filename lub inna właściwość w części przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="4151d-147">**setRuntimeProperties** is used to override the filename property or another property in the components of the workflow.</span></span>
  * <span data-ttu-id="4151d-148">**transcodeSource** służy do określania zawartości XML listy obiektów.</span><span class="sxs-lookup"><span data-stu-id="4151d-148">**transcodeSource** is used to specify the Clip List XML content.</span></span>

<span data-ttu-id="4151d-149">Połączenia w przepływie pracy:</span><span class="sxs-lookup"><span data-stu-id="4151d-149">Connections in the workflow:</span></span>

* <span data-ttu-id="4151d-150">Możesz użyć jednego lub kilku składników danych wejściowych plików nośnika i planowane jest użycie **setRuntimeProperties** Aby określić nazwę pliku, następnie nie numer pin plik podstawowy składnik się z nimi łączyć.</span><span class="sxs-lookup"><span data-stu-id="4151d-150">If you use one or several Media File Input components and plan to use **setRuntimeProperties** to specify the file name, then do not connect the primary file component pin to them.</span></span> <span data-ttu-id="4151d-151">Upewnij się, że istnieje połączenie między obiektem plik podstawowy i Input(s) pliku nośnika.</span><span class="sxs-lookup"><span data-stu-id="4151d-151">Make sure that there is no connection between the primary file object and the Media File Input(s).</span></span>
* <span data-ttu-id="4151d-152">Jeśli wolisz korzystać XML listy obiektów i jeden składnik źródło nośnika, a następnie mogą jednocześnie połączyć ze sobą.</span><span class="sxs-lookup"><span data-stu-id="4151d-152">If you prefer to use Clip List XML and one Media Source component, then you can connect both together.</span></span>

![Żadne połączenie z podstawowym pliku źródłowym wejście pliku multimediów](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="4151d-154">*Brak połączenia z podstawowego pliku do składników danych wejściowych pliku nośnika, jeśli używasz setRuntimeProperties można ustawić właściwość filename.*</span><span class="sxs-lookup"><span data-stu-id="4151d-154">*There is no connection from the primary file to Media File Input component(s) if you use setRuntimeProperties to set the filename property.*</span></span>

![Połączenie z listy klip XML należy przyciąć listy źródłowej](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="4151d-156">*Można nawiązać XML listy klip źródło nośnika i używać transcodeSource.*</span><span class="sxs-lookup"><span data-stu-id="4151d-156">*You can connect Clip List XML to Media Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="4151d-157">Przytnij dostosowania XML listy</span><span class="sxs-lookup"><span data-stu-id="4151d-157">Clip List XML customization</span></span>
<span data-ttu-id="4151d-158">Można określić XML listy klip w przepływie pracy w czasie wykonywania za pomocą **transcodeSource** w konfiguracji ciągu XML.</span><span class="sxs-lookup"><span data-stu-id="4151d-158">You can specify the Clip List XML in the workflow at runtime by using **transcodeSource** in the configuration string XML.</span></span> <span data-ttu-id="4151d-159">Wymaga to XML listy klip numeru pin do podłączenia do składnika źródło nośnika w przepływie pracy.</span><span class="sxs-lookup"><span data-stu-id="4151d-159">This requires the Clip List XML pin to be connected to the Media Source component in the workflow.</span></span>

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

<span data-ttu-id="4151d-160">Jeśli chcesz określić /primarySourceFile do tej właściwości należy użyć nazwy plików wyjściowych za pomocą "Wyrażeń", a następnie zalecamy przekazanie XML listy klip jako właściwość *po* właściwości /primarySourceFile, aby uniknąć klip Lista zostać zastąpione przez ustawienie /primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="4151d-160">If you want to specify /primarySourceFile to use this property to name the output files by using 'Expressions', then we recommend passing the Clip List XML as a property *after* the /primarySourceFile property, to avoid having the Clip List be overridden by the /primarySourceFile setting.</span></span>

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

<span data-ttu-id="4151d-161">Z dodatkowych przycinanie dokładne ramki:</span><span class="sxs-lookup"><span data-stu-id="4151d-161">With additional frame-accurate trimming:</span></span>

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

## <a name="example-1--overlay-an-image-on-top-of-the-video"></a><span data-ttu-id="4151d-162">Przykład 1: Nakładki obrazów na górze wideo</span><span class="sxs-lookup"><span data-stu-id="4151d-162">Example 1 : Overlay an image on top of the video</span></span>

### <a name="presentation"></a><span data-ttu-id="4151d-163">Prezentacji</span><span class="sxs-lookup"><span data-stu-id="4151d-163">Presentation</span></span>
<span data-ttu-id="4151d-164">Rozważmy przykład, w którym chcesz nałożyć obraz logo na wejściowego pliku wideo, gdy wideo jest zakodowany.</span><span class="sxs-lookup"><span data-stu-id="4151d-164">Consider an example in which you want to overlay a logo image on the input video while the video is encoded.</span></span> <span data-ttu-id="4151d-165">W tym przykładzie wejściowy plik wideo ma nazwę "Microsoft_HoloLens_Possibilities_816p24.mp4" i logo o nazwie "logo.png".</span><span class="sxs-lookup"><span data-stu-id="4151d-165">In this example, the input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and the logo is named "logo.png".</span></span> <span data-ttu-id="4151d-166">Należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4151d-166">You should perform the following steps:</span></span>

* <span data-ttu-id="4151d-167">Utwórz zasób przepływu pracy z plikiem przepływu pracy (zobacz poniższy przykład).</span><span class="sxs-lookup"><span data-stu-id="4151d-167">Create a Workflow Asset with the workflow file (see the following example).</span></span>
* <span data-ttu-id="4151d-168">Utwórz zasób nośnika, który zawiera dwa pliki: MyInputVideo.mp4 jako plik podstawowy i MyLogo.png.</span><span class="sxs-lookup"><span data-stu-id="4151d-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as the primary file and MyLogo.png.</span></span>
* <span data-ttu-id="4151d-169">Wysyłanie zadania do przepływu pracy Premium kodera multimediów procesor multimediów z powyższych zasobów wejściowych i określić następujący ciąg konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4151d-169">Send a task to the Media Encoder Premium Workflow media processor with the above input assets and specify the following configuration string.</span></span>

<span data-ttu-id="4151d-170">Konfiguracja:</span><span class="sxs-lookup"><span data-stu-id="4151d-170">Configuration:</span></span>

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

<span data-ttu-id="4151d-171">W powyższym przykładzie nazwa pliku wideo są wysyłane do składników danych wejściowych pliku nośnika, a właściwość primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="4151d-171">In the example above, the name of the video file is sent to the Media File Input component and the primarySourceFile property.</span></span> <span data-ttu-id="4151d-172">Nazwa pliku logo są wysyłane do innego nośnika plik danych wejściowych jest podłączony do składnika graficzne nakładki.</span><span class="sxs-lookup"><span data-stu-id="4151d-172">The name of the logo file is sent to another Media File Input that is connected to the graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="4151d-173">Nazwa pliku wideo są wysyłane do właściwości primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="4151d-173">The video file name is sent to the primarySourceFile property.</span></span> <span data-ttu-id="4151d-174">Przyczyną tego jest tej właściwości należy użyć w przepływie pracy umożliwiające tworzenie za pomocą wyrażenia, na przykład nazwa pliku poprawne dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="4151d-174">The reason for this is to use this property in the workflow for building the correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="4151d-175">Tworzenie krok przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="4151d-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="4151d-176">Poniżej przedstawiono kroki, aby utworzyć przepływ pracy, który przyjmuje dwa pliki jako dane wejściowe: i obrazu wideo.</span><span class="sxs-lookup"><span data-stu-id="4151d-176">Here are the steps to create a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="4151d-177">Będzie ona nakładki obrazu na górze wideo.</span><span class="sxs-lookup"><span data-stu-id="4151d-177">It will overlay the image on top of the video.</span></span>

<span data-ttu-id="4151d-178">Otwórz **projektanta przepływów pracy** i wybierz **pliku** > **nowy obszar roboczy** > **planu Transkodowanie**.</span><span class="sxs-lookup"><span data-stu-id="4151d-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="4151d-179">Nowy przepływ pracy zawiera trzy elementy:</span><span class="sxs-lookup"><span data-stu-id="4151d-179">The new workflow shows three elements:</span></span>

* <span data-ttu-id="4151d-180">Podstawowym pliku źródłowym</span><span class="sxs-lookup"><span data-stu-id="4151d-180">Primary Source File</span></span>
* <span data-ttu-id="4151d-181">Obcina listę XML</span><span class="sxs-lookup"><span data-stu-id="4151d-181">Clip List XML</span></span>
* <span data-ttu-id="4151d-182">Zawartości pliku wyjściowej</span><span class="sxs-lookup"><span data-stu-id="4151d-182">Output File/Asset</span></span>  

![Nowy przepływ pracy kodowania](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="4151d-184">*Nowy przepływ pracy kodowania*</span><span class="sxs-lookup"><span data-stu-id="4151d-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="4151d-185">Aby zaakceptować pliku wejściowego nośnika, Rozpocznij od dodania składnika nośnika pliku wejściowego.</span><span class="sxs-lookup"><span data-stu-id="4151d-185">In order to accept the input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="4151d-186">Aby dodać składnik do przepływu pracy, poszukaj jej w polu wyszukiwania w repozytorium i przeciągnij żądaną pozycję okienku projektanta.</span><span class="sxs-lookup"><span data-stu-id="4151d-186">To add a component to the workflow, look for it in the Repository search box and drag the desired entry onto the designer pane.</span></span>

<span data-ttu-id="4151d-187">Następnie dodaj plik wideo do zastosowania w przypadku projektowania przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="4151d-187">Next, add the video file to be used for designing your workflow.</span></span> <span data-ttu-id="4151d-188">Aby to zrobić, kliknij w okienku tła w Projektancie przepływów pracy i poszukaj właściwości w okienku po prawej stronie właściwości w podstawowym pliku źródłowym.</span><span class="sxs-lookup"><span data-stu-id="4151d-188">To do so, click the background pane in Workflow Designer and look for the Primary Source File property on the right-hand property pane.</span></span> <span data-ttu-id="4151d-189">Kliknij ikonę folderu i wybierz odpowiedniego pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="4151d-189">Click the folder icon and select the appropriate video file.</span></span>

![Źródłowy plik podstawowy](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="4151d-191">*Źródłowy plik podstawowy*</span><span class="sxs-lookup"><span data-stu-id="4151d-191">*Primary File Source*</span></span>

<span data-ttu-id="4151d-192">Następnie określ plik wideo w składniku wejściowy plik nośnika.</span><span class="sxs-lookup"><span data-stu-id="4151d-192">Next, specify the video file in the Media File Input component.</span></span>   

![Źródło danych wejściowych plików multimedialnych](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="4151d-194">*Źródło danych wejściowych plików multimedialnych*</span><span class="sxs-lookup"><span data-stu-id="4151d-194">*Media File Input Source*</span></span>

<span data-ttu-id="4151d-195">Natychmiast po zakończeniu składnika danych wejściowych plików nośnika sprawdź plik i wypełnić jego końcówek wyjściowych, aby odzwierciedlić pliku, który go inspekcji.</span><span class="sxs-lookup"><span data-stu-id="4151d-195">As soon as this is done, the Media File Input component will inspect the file and populate its output pins to reflect the file that it inspected.</span></span>

<span data-ttu-id="4151d-196">Następnym krokiem jest można dodać "wideo danych typu Updater" Aby określić przestrzeń kolorów na Rec.709.</span><span class="sxs-lookup"><span data-stu-id="4151d-196">The next step is to add a "Video Data Type Updater" to specify the color space to Rec.709.</span></span> <span data-ttu-id="4151d-197">Dodaj "Wideo Format konwertera" ustawioną na układ układ danych typu = planarnych można konfigurować.</span><span class="sxs-lookup"><span data-stu-id="4151d-197">Add a "Video Format Converter" that is set to Data Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="4151d-198">Spowoduje to przekonwertowanie strumienia wideo do formatu, który można podjąć jako źródło składnika nakładki.</span><span class="sxs-lookup"><span data-stu-id="4151d-198">This will convert the video stream to a format that can be taken as a source of the overlay component.</span></span>

![wideo Updater typu danych i Format konwertera](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="4151d-200">*Aktualizator typu danych wideo i konwertera formatu*</span><span class="sxs-lookup"><span data-stu-id="4151d-200">*Video Data Type Updater and Format Converter*</span></span>

![Typ układu = planarnych można konfigurować](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<span data-ttu-id="4151d-202">*Typ układu jest konfigurowalne planarnych*</span><span class="sxs-lookup"><span data-stu-id="4151d-202">*Layout type is Configurable Planar*</span></span>

<span data-ttu-id="4151d-203">Następnie dodaj składnik nakładka wideo i połączyć (nieskompresowanych) wideo numeru pin (nieskompresowanych) wideo wejściowego pliku nośnika.</span><span class="sxs-lookup"><span data-stu-id="4151d-203">Next, add a Video Overlay component and connect the (uncompressed) video pin to the (uncompressed) video pin of the media file input.</span></span>

<span data-ttu-id="4151d-204">Dodaj inny nośnik plik danych wejściowych (można załadować pliku logo), kliknij ten składnik i zmień jego nazwę na "Logo dane wejściowe w pliku nośnika", a następnie wybierz obraz (plik PNG na przykład) właściwości pliku.</span><span class="sxs-lookup"><span data-stu-id="4151d-204">Add another Media File Input (to load the logo file), click on this component and rename it to "Media File Input Logo", and select an image (a .png file for example) in the file property.</span></span> <span data-ttu-id="4151d-205">Połączyć pin nieskompresowanych obrazu nieskompresowanych obrazu nakładki.</span><span class="sxs-lookup"><span data-stu-id="4151d-205">Connect the Uncompressed image pin to the Uncompressed image pin of the overlay.</span></span>

![Nakładki źródła pliku składnika i obrazów](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="4151d-207">*Nakładki źródła pliku składnika i obrazów*</span><span class="sxs-lookup"><span data-stu-id="4151d-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="4151d-208">Jeśli chcesz zmodyfikować pozycji logo na wideo (na przykład możesz chcieć umieść go na 10 procent wylogowuje na lewym górnym rogu wideo), usuń zaznaczenie pola wyboru "Ręcznego wprowadzania".</span><span class="sxs-lookup"><span data-stu-id="4151d-208">If you want to modify the position of the logo on the video (for example, you might want to position it at 10 percent off of the top left corner of the video), clear the "Manual Input" check box.</span></span> <span data-ttu-id="4151d-209">Można to zrobić, ponieważ pozwala udostępnić plik logo do składnika nakładki używasz wejściowy plik nośnika.</span><span class="sxs-lookup"><span data-stu-id="4151d-209">You can do this because you are using a Media File Input to provide the logo file to the overlay component.</span></span>

![Pozycja nakładki](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="4151d-211">*Pozycja nakładki*</span><span class="sxs-lookup"><span data-stu-id="4151d-211">*Overlay position*</span></span>

<span data-ttu-id="4151d-212">Do kodowania strumienia wideo H.264, należy dodać składniki kodera koder wideo AVC i AAC powierzchnię projektanta.</span><span class="sxs-lookup"><span data-stu-id="4151d-212">To encode the video stream to H.264, add the AVC Video Encoder and AAC encoder components to the designer surface.</span></span> <span data-ttu-id="4151d-213">Połącz numerów PIN.</span><span class="sxs-lookup"><span data-stu-id="4151d-213">Connect the pins.</span></span>
<span data-ttu-id="4151d-214">Ustaw kodera AAC i wybierz Format Audio konwersji/ustawienie: 2.0 (L, R).</span><span class="sxs-lookup"><span data-stu-id="4151d-214">Set up the AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![Kodery audio i wideo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="4151d-216">*Kodery audio i wideo*</span><span class="sxs-lookup"><span data-stu-id="4151d-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="4151d-217">Teraz Dodaj **ISO Mpeg-4 multiplekser** i **dane wyjściowe pliku** składników i podłącz numery PIN, jak pokazano.</span><span class="sxs-lookup"><span data-stu-id="4151d-217">Now add the **ISO Mpeg-4 Multiplexer** and **File Output** components and connect the pins as shown.</span></span>

![MP4 multiplekser i danych wyjściowych w pliku](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="4151d-219">*MP4 multiplekser i danych wyjściowych w pliku*</span><span class="sxs-lookup"><span data-stu-id="4151d-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="4151d-220">Należy określić nazwę dla pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="4151d-220">You need to set the name for the output file.</span></span> <span data-ttu-id="4151d-221">Kliknij przycisk **dane wyjściowe pliku** składnika i edycji wyrażenia dla pliku:</span><span class="sxs-lookup"><span data-stu-id="4151d-221">Click the **File Output** component and edit the expression for the file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Nazwa pliku wyjściowego](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="4151d-223">*Nazwa pliku wyjściowego*</span><span class="sxs-lookup"><span data-stu-id="4151d-223">*File output name*</span></span>

<span data-ttu-id="4151d-224">Można uruchomić przepływu pracy lokalnie w celu sprawdzenia, czy działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="4151d-224">You can run the workflow locally to check that it is running correctly.</span></span>

<span data-ttu-id="4151d-225">Po jej zakończeniu, można go uruchomić w usłudze Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="4151d-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="4151d-226">Najpierw przygotować zasobów w usłudze Azure Media Services z dwoma plikami w nim: plik wideo i logo.</span><span class="sxs-lookup"><span data-stu-id="4151d-226">First, prepare an asset in Azure Media Services with two files in it: the video file and the logo.</span></span> <span data-ttu-id="4151d-227">Można to zrobić przy użyciu platformy .NET lub interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="4151d-227">You can do this by using the .NET or REST API.</span></span> <span data-ttu-id="4151d-228">Można to także zrobić przy użyciu portalu Azure lub [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span><span class="sxs-lookup"><span data-stu-id="4151d-228">You can also do this by using the Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="4151d-229">Ten samouczek pokazuje, jak zarządzać zasobami za pomocą AMSE.</span><span class="sxs-lookup"><span data-stu-id="4151d-229">This tutorial shows you how to manage assets with AMSE.</span></span> <span data-ttu-id="4151d-230">Istnieją dwa sposoby dodawania plików do zawartości:</span><span class="sxs-lookup"><span data-stu-id="4151d-230">There are two ways to add files to an asset:</span></span>

* <span data-ttu-id="4151d-231">Utwórz folder lokalny, skopiuj dwa pliki i przeciągnij i upuść folder **zasobów** kartę.</span><span class="sxs-lookup"><span data-stu-id="4151d-231">Create a local folder, copy the two files in it, and drag and drop the folder to the **Asset** tab.</span></span>
* <span data-ttu-id="4151d-232">Przekazywanie pliku wideo jako zasób, wyświetlane informacje o zasobie, przejdź do karty pliki i przekazać plik dodatkowy (logo).</span><span class="sxs-lookup"><span data-stu-id="4151d-232">Upload the video file as an asset, display the asset information, go to the files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="4151d-233">Upewnij się ustawić plik podstawowy w zasobów (główny plik wideo).</span><span class="sxs-lookup"><span data-stu-id="4151d-233">Make sure to set a primary file in the asset (the main video file).</span></span>

![Pliki zasobów w AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="4151d-235">*Pliki zasobów w AMSE*</span><span class="sxs-lookup"><span data-stu-id="4151d-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="4151d-236">Wybierz element zawartości, a następnie wybierz kodować je za pomocą kodera Premium.</span><span class="sxs-lookup"><span data-stu-id="4151d-236">Select the asset and choose to encode it with Premium Encoder.</span></span> <span data-ttu-id="4151d-237">Przekaż przepływu pracy i zaznacz go.</span><span class="sxs-lookup"><span data-stu-id="4151d-237">Upload the workflow and select it.</span></span>

<span data-ttu-id="4151d-238">Kliknij przycisk, aby przekazać dane do procesora, a następnie dodaj następujący kod XML można ustawić właściwości środowisko uruchomieniowe:</span><span class="sxs-lookup"><span data-stu-id="4151d-238">Click the button to pass data to the processor, and add the following XML to set the runtime properties:</span></span>

![Koder Premium w AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="4151d-240">*Koder Premium w AMSE*</span><span class="sxs-lookup"><span data-stu-id="4151d-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="4151d-241">Następnie wklej poniższe dane XML.</span><span class="sxs-lookup"><span data-stu-id="4151d-241">Then, paste the following XML data.</span></span> <span data-ttu-id="4151d-242">Należy określić nazwę pliku wideo wejście pliku multimediów i primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="4151d-242">You need to specify the name of the video file for both the Media File Input and primarySourceFile.</span></span> <span data-ttu-id="4151d-243">Określ nazwę pliku dla logo zbyt.</span><span class="sxs-lookup"><span data-stu-id="4151d-243">Specify the name of the file name for the logo too.</span></span>

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

<span data-ttu-id="4151d-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="4151d-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="4151d-246">Użycie zestawu .NET SDK do tworzenia i uruchamiania zadania, dane XML musi być przekazywane jako parametry konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4151d-246">If you use the .NET SDK to create and run the task, this XML data has to be passed as the configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="4151d-247">Po zakończeniu zadania plik MP4 elementu zawartości wyjściowej Wyświetla nakładki!</span><span class="sxs-lookup"><span data-stu-id="4151d-247">After the job is complete, the MP4 file in the output asset displays the overlay!</span></span>

![Nakładka wideo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="4151d-249">*Nakładka wideo*</span><span class="sxs-lookup"><span data-stu-id="4151d-249">*Overlay on the video*</span></span>

<span data-ttu-id="4151d-250">Możesz pobrać przykładowym przepływie pracy z [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span><span class="sxs-lookup"><span data-stu-id="4151d-250">You can download the sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="4151d-251">Przykład 2: Wiele audio kodowanie</span><span class="sxs-lookup"><span data-stu-id="4151d-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="4151d-252">Przykładem wiele wersji językowych audio kodowania workfkow jest dostępna w [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span><span class="sxs-lookup"><span data-stu-id="4151d-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="4151d-253">Ten folder zawiera przykładowy przepływ pracy, który może służyć do kodowania pliku MXF do wielu zasobów plików MP4 z wielu ścieżek audio.</span><span class="sxs-lookup"><span data-stu-id="4151d-253">This folder contains a sample workflow which can be used to encode a MXF file to a multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="4151d-254">Ten przepływ pracy zakłada, że plik MXF zawiera jedną ścieżkę audio; dodatkowe ścieżki audio powinien zostać przekazany jako osobne pliki audio (WAV lub MP4...).</span><span class="sxs-lookup"><span data-stu-id="4151d-254">This workflow assumes that the MXF file contains one audio track ; the additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="4151d-255">Do kodowania, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4151d-255">To encode, please follow these steps:</span></span>

* <span data-ttu-id="4151d-256">Utwórz zasób usługi Media Services z pliku MXF i plików Audio (pliki audio 0-18).</span><span class="sxs-lookup"><span data-stu-id="4151d-256">Create a Media Services asset with the MXF file and the Audio files (0 to 18 audio files).</span></span>
* <span data-ttu-id="4151d-257">Upewnij się, że plik MXF jest ustawiony jako plik podstawowy.</span><span class="sxs-lookup"><span data-stu-id="4151d-257">Make sure that the MXF file is set as a primary file.</span></span>
* <span data-ttu-id="4151d-258">Utwórz zadania i zadania przy użyciu procesora koder Premium przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="4151d-258">Create a job and a task using the Premium Workflow Encoder processor.</span></span> <span data-ttu-id="4151d-259">Użyj podane przepływu pracy (MultiMP4-1080p-19audio-v1.workflow).</span><span class="sxs-lookup"><span data-stu-id="4151d-259">Use the workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="4151d-260">Przekazywanie danych setruntime.xml zadania (Jeśli używasz Azure Media Services Explorer, kliknij przycisk "przekazywania danych xml do przepływu pracy").</span><span class="sxs-lookup"><span data-stu-id="4151d-260">Pass the setruntime.xml data to the task (if you use Azure Media Services Explorer, use the “pass xml data to the workflow” button).</span></span>
  * <span data-ttu-id="4151d-261">Zaktualizuj danych XML do określenia tagów prawidłowej nazwy i języków.</span><span class="sxs-lookup"><span data-stu-id="4151d-261">Please update the XML data to specify the correct file names and languages tags.</span></span>
  * <span data-ttu-id="4151d-262">Przepływ pracy ma audio składniki o nazwie Audio 1-Audio 18.</span><span class="sxs-lookup"><span data-stu-id="4151d-262">The workflow has audio components named Audio 1 to Audio 18.</span></span>
  * <span data-ttu-id="4151d-263">RFC5646 jest obsługiwany przez język znaczników.</span><span class="sxs-lookup"><span data-stu-id="4151d-263">RFC5646 is supported for the language tag.</span></span>

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

* <span data-ttu-id="4151d-264">Tych ścieżek należy wybieranych w programie Azure Media Player i zakodowanym elementem zawartości będzie zawierać ścieżek audio multi języka.</span><span class="sxs-lookup"><span data-stu-id="4151d-264">The encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="4151d-265">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4151d-265">See also</span></span>
* [<span data-ttu-id="4151d-266">Wprowadzenie do kodowania w Azure Media Services w wersji Premium</span><span class="sxs-lookup"><span data-stu-id="4151d-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="4151d-267">Jak używać Premium kodowania w usłudze Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="4151d-267">How to use Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="4151d-268">Kodowanie zawartości na żądanie za pomocą usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="4151d-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="4151d-269">Koderów-dekoderów i formaty Media Encoder Premium w przepływie pracy</span><span class="sxs-lookup"><span data-stu-id="4151d-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="4151d-270">Przykładowe pliki przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="4151d-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="4151d-271">Narzędzia usługi Azure Media Services Explorer</span><span class="sxs-lookup"><span data-stu-id="4151d-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="4151d-272">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="4151d-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4151d-273">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="4151d-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
