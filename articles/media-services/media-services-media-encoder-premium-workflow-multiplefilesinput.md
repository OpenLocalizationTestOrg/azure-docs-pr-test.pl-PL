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
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a>Używanie wielu plików wejściowych i właściwości składnika za pomocą kodera — wersja Premium
## <a name="overview"></a>Omówienie
Istnieją scenariusze, w których może być konieczne właściwości składnika toocustomize, określ zawartość XML listy klip lub wysyłania wielu plików wejściowych podczas przesyłania zadania hello **Media Encoder Premium w przepływie pracy** procesor multimediów. Przykłady to:

* Zastępując tekst wideo i ustawianie wartości tekstowej hello (na przykład hello bieżącą datę) w czasie wykonywania dla każdego wejściowego wideo.
* Dostosowywanie hello klip listy XML (toospecify jednego lub kilku źródła plików, lub bez przycinania, itp.).
* Nakładanie obraz logo na powitania wejściowy plik wideo, gdy wideo hello jest zaszyfrowana.
* Wiele kodowanie języka audio.

Witaj toolet **Media Encoder Premium w przepływie pracy** wiedzieć, że podczas tworzenia zadania hello lub wysyłania wielu plików wejściowych zmieniasz niektórych właściwości w przepływie pracy hello, masz toouse w ciągu konfiguracji, który zawiera  **setRuntimeProperties** i/lub **transcodeSource**. W tym temacie opisano sposób toouse je.

## <a name="configuration-string-syntax"></a>Składnia ciągu konfiguracji
tooset ciągu konfiguracji Hello w hello kodowania zadań używa dokument XML, który wygląda następująco:

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

Witaj poniżej znajduje się kod hello C#, służącą do odczytywania z pliku konfiguracji XML hello, zmodyfikuj go przy użyciu hello filename prawo wideo i przekazuje je toohello zadań w ramach zadania:

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

## <a name="customizing-component-properties"></a>Dostosowywanie właściwości składnika
### <a name="property-with-a-simple-value"></a>Właściwość z wartością proste
W niektórych przypadkach jest przydatne toocustomize właściwości składnika wraz z hello pliku przepływu pracy, który będzie toobe wykonywane przez przepływ pracy Premium kodera multimediów.

Załóżmy, że przeznaczona tekst nakładki przepływu pracy na pliki wideo i hello tekstu (na przykład hello bieżącą datę) powinien toobe zestawu w czasie wykonywania. Można to zrobić, wysyłając toobe tekst hello Ustaw jako hello nową wartość dla właściwości text hello hello nakładki składnika z hello kodowania zadań. Ten mechanizm toochange można użyć innych właściwości składnika w przepływie pracy hello (takie jak pozycja hello lub kolor nakładki hello, hello szybkości transmisji bitów kodera hello AVC itp.).

**setRuntimeProperties** jest używane toooverride właściwości w składnikach hello hello przepływu pracy.

Przykład:

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

### <a name="property-with-an-xml-value"></a>Właściwość wartości XML
Hermetyzuj tooset właściwości, która oczekuje wartości XML przy użyciu `<![CDATA[ and ]]>`.

Przykład:

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
> Upewnij się, że tooput karetki zwracać tuż po `<![CDATA[`.

### <a name="propertypath-value"></a>wartości propertyPath
W poprzednich przykładach hello została hello propertyPath "/ Media pliku danych wejściowych/filename" lub "/ inactiveTimeout" lub "clipListXml".
To jest ogólnie rzecz biorąc, hello nazwy składnika hello, a następnie nazwę hello hello właściwości. Hello ścieżki może zawierać więcej lub mniej poziomów, takie jak "/ primarySourceFile" (ponieważ właściwość hello jest głównym hello hello przepływu pracy) lub "/ wideo przetwarzania/grafiki nakładki/nieprzezroczystość" (ponieważ hello nakładki znajduje się w grupie).    

toocheck hello ścieżki i nazwy właściwości, użyj hello Akcja przycisku, który jest od razu, obok każdej właściwości. Można kliknąć ten przycisk, akcji i wybierz **Edytuj**. Wyświetli możesz hello rzeczywistej nazwy właściwości hello i natychmiast powyżej, hello przestrzeni nazw.

![Akcja i edytowanie](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Właściwość](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a>Wiele plików wejściowych
Każde zadanie, aby przesłać toohello **Media Encoder Premium w przepływie pracy** wymaga dwóch zasobów:

* Witaj najpierw jest *zasobów przepływu pracy* zawierający plik przepływu pracy. Pliki przepływu pracy można zaprojektować przy użyciu hello [projektanta przepływów pracy](media-services-workflow-designer.md).
* Witaj drugim jest *multimedialnej* zawierający hello nośnika pliki, które mają tooencode.

Gdy wysyłasz wielu toohello pliki nośnika **Media Encoder Premium w przepływie pracy** Zastosuj następujące ograniczenia hello kodera,:

* Wszystkie nośniki hello pliki muszą być w hello sam *multimedialnej*. Używanie wielu zasobów nośnika nie jest obsługiwane.
* Należy ustawić plik podstawowy hello w tej zawartości nośnika (najlepiej, jeśli jest to hello głównego pliku wideo, który hello kodera monitu tooprocess).
* Jest konieczne toopass danych konfiguracji, który zawiera hello **setRuntimeProperties** i/lub **transcodeSource** elementu toohello procesora.
  * **setRuntimeProperties** jest właściwość filename hello toooverride używane lub inna właściwość w składnikach hello hello przepływu pracy.
  * **transcodeSource** jest używane toospecify hello zawartości XML listy obiektów.

Połączenia w przepływie pracy hello:

* Możesz użyć jednego lub kilku składników danych wejściowych plików nośnika i planowanie toouse **setRuntimeProperties** toospecify hello nazwy pliku, a następnie nie podłączaj hello plik podstawowy składnik numeru pin toothem. Upewnij się, że istnieje połączenie między hello plik podstawowy obiekt i hello Input(s) pliku nośnika.
* Jeśli wolisz toouse XML listy obiektów i jeden składnik źródło nośnika, a następnie mogą jednocześnie połączyć ze sobą.

![Brak połączenia z podstawowym pliku źródłowym tooMedia plik danych wejściowych](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

*Brak połączenia z tooMedia plik podstawowy hello składników danych wejściowych plików, jeśli używana jest właściwość filename hello tooset setRuntimeProperties.*

![Połączenie z tooClip klip listy XML listy źródłowej](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

*Możesz łączyć tooMedia klip listy XML źródła i użyj transcodeSource.*

### <a name="clip-list-xml-customization"></a>Przytnij dostosowania XML listy
Można określić hello klip listy XML w przepływie pracy hello w czasie wykonywania za pomocą **transcodeSource** w konfiguracji hello ciągu XML. Wymaga to hello XML listy klip numeru pin toobe połączone toohello źródło nośnika dla składnika w przepływie pracy hello.

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

Jeśli chcesz toouse /primarySourceFile toospecify te dane wyjściowe hello tooname właściwości plików za pomocą "Wyrażenia", a następnie zalecamy przekazanie hello klip listy XML jako właściwość *po* właściwości /primarySourceFile hello, tooavoid o hello listy klip ma zostać zastąpione przez ustawienie /primarySourceFile hello.

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

Z dodatkowych przycinanie dokładne ramki:

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

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a>Przykład 1: Nakładki obrazów na powitania wideo

### <a name="presentation"></a>Prezentacji
Należy wziąć pod uwagę przykładem, w której ma zostać toooverlay obraz logo na powitania wejściowy plik wideo podczas wideo hello jest zaszyfrowana. W tym przykładzie hello wejściowy plik wideo ma nazwę "Microsoft_HoloLens_Possibilities_816p24.mp4" i hello logo nosi nazwę "logo.png". Należy wykonać następujące kroki hello:

* Utwórz zasób przepływu pracy z plikiem przepływu pracy hello (zobacz poniższy przykład hello).
* Utwórz zasób nośnika, który zawiera dwa pliki: MyInputVideo.mp4 jako hello plik podstawowy i MyLogo.png.
* Wyślij toohello zadania przepływu pracy Premium kodera multimediów nośnika zasoby procesora z powyższych hello danych wejściowych i określ powitania po ciągu konfiguracji.

Konfiguracja:

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

W powyższym przykładzie hello hello nazwę pliku wideo hello są wysyłane toohello wejście pliku multimediów składnika i hello primarySourceFile właściwości. Witaj nazwę pliku logo hello są wysyłane tooanother nośnika plik danych wejściowych składnika graficzne nakładki toohello połączonych.

> [!NOTE]
> Nazwa pliku wideo Hello są wysyłane toohello primarySourceFile właściwości. Witaj przyczyną tego błędu jest toouse tej właściwości w przepływie pracy hello do tworzenia nazwy pliku wyjściowego poprawne hello przy użyciu wyrażenia, np.

### <a name="step-by-step-workflow-creation"></a>Tworzenie krok przepływu pracy
Poniżej przedstawiono hello toocreate czynności przepływu pracy, który przyjmuje dwa pliki jako dane wejściowe: i obrazu wideo. Będzie ona nakładki hello obrazu na powitania wideo.

Otwórz **projektanta przepływów pracy** i wybierz **pliku** > **nowy obszar roboczy** > **planu Transkodowanie**.

Witaj nowy przepływ pracy zawiera trzy elementy:

* Podstawowym pliku źródłowym
* Obcina listę XML
* Zawartości pliku wyjściowej  

![Nowy przepływ pracy kodowania](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

*Nowy przepływ pracy kodowania*

W pliku wejściowego nośnika hello tooaccept kolejności Rozpocznij od dodania składnika nośnika pliku wejściowego. tooadd przepływu pracy toohello składnika, poszukaj jej w polu wyszukiwania w repozytorium hello i przeciągnij hello potrzeby wpis na hello okienku projektanta.

Następnie dodaj toobe pliku wideo hello używanych do projektowania przepływu pracy. toodo tak, kliknij przycisk hello tła okienka w Projektancie przepływów pracy i poszukaj hello właściwości głównej pliku źródłowego w okienku po prawej stronie właściwości hello. Kliknij ikonę folderu hello i wybierz hello odpowiedniego pliku wideo.

![Źródłowy plik podstawowy](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

*Źródłowy plik podstawowy*

Następnie określ plik wideo hello hello składnika danych wejściowych pliku nośnika.   

![Źródło danych wejściowych plików multimedialnych](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

*Źródło danych wejściowych plików multimedialnych*

Natychmiast po zakończeniu hello wejściowy plik nośnika składnik będzie sprawdzenie pliku hello i wypełnić jego dane wyjściowe numerów PIN tooreflect hello pliku, który go inspekcji.

Witaj następnym krokiem jest tooadd tooRec.709 "Updater typu danych wideo" toospecify hello kolor miejsca. Dodaj "Wideo Format konwertera" ustawiony typ układu/układu tooData = planarnych można konfigurować. Spowoduje to przekonwertowanie hello strumienia wideo o tooa formacie, który można podjąć jako źródło hello nakładki składnika.

![wideo Updater typu danych i Format konwertera](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

*Aktualizator typu danych wideo i konwertera formatu*

![Typ układu = planarnych można konfigurować](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

*Typ układu jest konfigurowalne planarnych*

Następnie dodaj składnik nakładka wideo i połącz hello (nieskompresowanych) wideo numeru pin toohello (nieskompresowanych) wideo numeru pin hello nośnika plików wejściowych.

Dodaj inny wejście nośnika (tooload hello logo plik), kliknij ten składnik i zmień jego nazwę za "Logo dane wejściowe w pliku nośnika", a następnie wybierz obraz (plik PNG na przykład) we właściwości pliku hello. Połącz hello nieskompresowanych obrazu numeru pin toohello nieskompresowanych obrazu kod pin hello nakładki.

![Nakładki źródła pliku składnika i obrazów](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

*Nakładki źródła pliku składnika i obrazów*

Jeśli chcesz, aby toomodify hello położenie logo hello na powitania wideo (na przykład może być tooposition go na 10 procent wylogowuje na górze hello lewym rogu hello wideo), wyczyść pole wyboru "Ręcznego wprowadzania" hello. Można to zrobić, ponieważ używają składnika danych wejściowych plik nośnika tooprovide hello logo pliku toohello nakładki.

![Pozycja nakładki](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

*Pozycja nakładki*

tooencode hello tooH.264 strumienia wideo, dodać hello koder wideo AVC i powierzchni projektanta składników toohello AAC kodera. Połącz hello numerów PIN.
Ustaw hello AAC koder i wybierz Format Audio konwersji/ustawienie: 2.0 (L, R).

![Kodery audio i wideo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

*Kodery audio i wideo*

Teraz Dodaj hello **ISO Mpeg-4 multiplekser** i **dane wyjściowe pliku** składników i podłącz hello numerów PIN, jak pokazano.

![MP4 multiplekser i danych wyjściowych w pliku](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

*MP4 multiplekser i danych wyjściowych w pliku*

Należy tooset hello nazwę pliku wyjściowego hello. Kliknij przycisk hello **dane wyjściowe pliku** wyrażenia hello składnika i edycja pliku hello:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Nazwa pliku wyjściowego](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

*Nazwa pliku wyjściowego*

Można uruchomić przepływu pracy hello lokalnie toocheck, czy działa prawidłowo.

Po jej zakończeniu, można go uruchomić w usłudze Azure Media Services.

Najpierw przygotować zasobów w usłudze Azure Media Services z dwoma plikami w nim: hello plików wideo i hello logo. Można to zrobić za pomocą hello .NET lub interfejsu API REST. Również można to zrobić za pomocą portalu Azure hello lub [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).

W tym samouczku przedstawiono sposób toomanage zasobów z AMSE. Istnieją dwa sposoby tooadd pliki tooan zasobów:

* Utwórz folder lokalny, skopiuj hello dwa pliki i przeciągnij i upuść hello folderu toohello **zasobów** kartę.
* Przekazywanie pliku wideo hello jako zasób, wyświetlane informacje o zasobie hello, przejdź na kartę Pliki toohello i przekazać plik dodatkowy (logo).

> [!NOTE]
> Upewnij się, że tooset plik podstawowy w hello zasobów (hello głównego pliku wideo).

![Pliki zasobów w AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

*Pliki zasobów w AMSE*

Wybierz hello zasobów, a tooencode go za pomocą kodera Premium. Przekaż hello przepływu pracy i zaznacz go.

Kliknij hello przycisk toopass danych toohello procesora i dodaj następujące właściwości środowisko uruchomieniowe hello tooset XML hello:

![Koder Premium w AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

*Koder Premium w AMSE*

Następnie wklej powitania po danych XML. Należy toospecify hello nazwę pliku wideo hello hello wejście pliku multimediów i primarySourceFile. Określ nazwę hello hello nazwę pliku dla hello logo zbyt.

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

*setRuntimeProperties*

Jeśli używasz hello toocreate zestawu .NET SDK i uruchom zadanie hello, dane XML ma toobe przekazywane jako parametry konfiguracji hello.

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

Po zakończeniu zadania hello plik hello MP4 w hello danych wyjściowych zasobów wyświetla nakładki hello!

![Nakładki na powitania wideo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

*Nakładki na powitania wideo*

Możesz pobrać hello przykładowego przepływu pracy z [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).

## <a name="example-2--multiple-audio-language-encoding"></a>Przykład 2: Wiele audio kodowanie

Przykładem wiele wersji językowych audio kodowania workfkow jest dostępna w [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).

Ten folder zawiera przykładowy przepływ pracy, które mogą być używane tooencode MXF pliku tooa MP4 wielu plików zasobów z wielu ścieżek audio.

Ten przepływ pracy przyjęto założenie, że plik MXF hello zawiera jedną ścieżkę audio; dodatkowe ścieżki audio Hello powinien zostać przekazany jako osobne pliki audio (WAV lub MP4...).

tooencode, wykonaj następujące czynności:

* Utwórz zasób usługi Media Services z pliku MXF hello i hello Audio plików (0 too18 audio).
* Upewnij się, że plik MXF hello jest ustawiony jako plik podstawowy.
* Utwórz zadania i zadania przy użyciu hello koder Premium przepływu pracy procesora. Za pomocą przepływu pracy hello podane (MultiMP4-1080p-19audio-v1.workflow).
* Przekaż hello setruntime.xml danych toohello zadań (Jeśli używasz Eksploratora usługi Azure Media, przycisk "Przekaż przepływ pracy toohello danych xml" hello).
  * Zaktualizuj hello danych toospecify hello poprawny plik nazwy i języków tagów XML.
  * przepływ pracy Hello ma audio składniki o nazwie tooAudio Audio 1 18.
  * RFC5646 znacznik języka hello jest obsługiwana.

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

* Hello zakodowane zasobów będzie zawierać ścieżek audio multi języka i tych ścieżek powinien być możliwy w programie Azure Media Player.

## <a name="see-also"></a>Zobacz też
* [Wprowadzenie do kodowania w Azure Media Services w wersji Premium](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [Jak toouse Premium kodowania w usłudze Azure Media Services](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [Kodowanie zawartości na żądanie za pomocą usługi Azure Media Services](media-services-encode-asset.md#media-encoder-premium-workflow)
* [Koderów-dekoderów i formaty Media Encoder Premium w przepływie pracy](media-services-premium-workflow-encoder-formats.md)
* [Przykładowe pliki przepływu pracy](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [Narzędzia usługi Azure Media Services Explorer](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
