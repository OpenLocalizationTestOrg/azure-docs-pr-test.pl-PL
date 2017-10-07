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
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a>Zaawansowane samouczki Media Encoder Premium w przepływie pracy
## <a name="overview"></a>Omówienie
Ten dokument zawiera wskazówki, które pokazują jak przepływów toocustomize z **projektanta przepływów pracy**. Pliki można znaleźć hello rzeczywiste przepływu pracy [tutaj](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).  

## <a name="toc"></a>SPIS TREŚCI
obejmuje Hello następujące tematy:

* [Kodowanie MXF do pojedynczej szybkości transmisji bitów MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [Uruchamianie nowego przepływu pracy](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [Przy użyciu hello wejście pliku multimediów](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [Zapoznanie się strumieni nośnika](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [Dodawanie koder wideo dla. Generowanie pliku MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [Kodowania hello strumieniem audio](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [Strumienie multipleksowania Audio i wideo do kontenera MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [Zapisywanie pliku MP4 hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [Tworzenie zasobów usługi multimediów z pliku wyjściowego hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [Test hello Zakończono lokalnie przepływu pracy](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [Kodowanie MXF do multibitrate MP4s - dynamicznego tworzenia pakietów włączone](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [Dodanie jednego lub więcej dodatkowych danych wyjściowych MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [Konfigurowanie nazwy wyjściowego pliku hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [Dodawanie oddzielne ścieżkę Audio](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [Dodawanie hello. Plik SMIL ISM](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [Kodowanie MXF do multibitrate MP4 — rozszerzone planu](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [Tooenhance omówienie przepływu pracy](#workflow-overview-to-enhance)
  * [Konwencje nazewnictwa plików](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [Właściwości składnika publikacji na powitania głównego przepływu pracy](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [Wygenerowano plik wyjściowy, który nazwy zależne od wartości właściwości opublikowanych](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [Dodawanie danych wyjściowych MP4 toomultibitrate miniatur](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [Miniatur tooadd omówienie przepływu pracy](#workflow-overview-to-add-thumbnails-to)
  * [Dodawanie kodowania JPG](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [Zajmujących się konwersji przestrzeń kolorów](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [Zapisywanie hello miniatur](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [Wykrywanie błędów w przepływie pracy](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [Zakończono przepływu pracy](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [Na podstawie czasu przycinanie multibitrate MP4 danych wyjściowych](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [Dodawanie przycinanie do toostart omówienie przepływu pracy](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [Przy użyciu hello przycinarka strumienia](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [Zakończono przepływu pracy](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [Wprowadzenie hello składnika uwzględnione w skryptach](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [Obsługa skryptów w ramach przepływu pracy: Witaj świecie](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [Przycinanie multibitrate MP4 dane wyjściowe na podstawie ramki](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [Omówienie toostart Dodawanie przycinanie do planu](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [Przy użyciu hello klip listy XML](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [Modyfikowanie listy klip hello ze składnika uwzględnione w skryptach](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [Dodawanie właściwości wygody ClippingEnabled](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <a id="MXF_to_MP4"></a>Kodowanie MXF do pojedynczej szybkości transmisji bitów MP4
W tym przewodniku utworzymy o pojedynczej szybkości transmisji bitów. Plik MP4 o AAC-HE zakodowane audio z. Plik wejściowy MXF.

### <a id="MXF_to_MP4_start_new"></a>Uruchamianie nowego przepływu pracy
Otwórz projektanta przepływów pracy i wybierz pozycję "Planu Transkodowanie pliku"-"nowy obszar roboczy"-""

Witaj nowego przepływu pracy będą wyświetlane 3 elementów:

* Podstawowym pliku źródłowym
* Obcina listę XML
* Zawartości pliku wyjściowej  

![Nowy przepływ pracy kodowania](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

*Nowy przepływ pracy kodowania*

### <a id="MXF_to_MP4_with_file_input"></a>Przy użyciu hello wejście pliku multimediów
W kolejności tooaccept naszych wejściowy plik jedną rozpoczyna się od dodawania składnika nośnika pliku wejściowego. tooadd przepływu pracy toohello składnika, poszukaj jej w polu wyszukiwania w repozytorium hello i przeciągnij hello potrzeby wpis na hello okienku projektanta. Wykonaj dla hello nośnika pliku wejściowego i połączyć hello podstawowy plik źródłowy składnika toohello Filename wprowadzania numeru pin z hello nośnika pliku wejściowego.

![Pliku multimedialnego połączonych danych wejściowych](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

*Pliku multimedialnego połączonych danych wejściowych*

Zanim przejdziemy wiele więcej, musisz najpierw projektanta przepływów pracy toohello tooindicate jakie przykładowy plik chcielibyśmy toouse toodesign naszych przepływu pracy z. toodo tak, kliknij przycisk hello tła okienka projektanta i poszukaj hello właściwości głównej pliku źródłowego w okienku po prawej stronie właściwości hello. Kliknij ikonę folderu hello i przepływ pracy hello tootest pliku hello wybierz żądany z. Natychmiast po zakończeniu hello wejściowy plik nośnika składnik będzie sprawdzenie pliku hello i wypełnić jego dane wyjściowe numerów PIN tooreflect hello plik, który go inspekcji.

![Dane wejściowe pliku multimedialnego wypełnione](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

*Dane wejściowe pliku multimedialnego wypełnione*

Gdy to określa co wejściowej chcielibyśmy toowork z, program nie nakazuje jeszcze gdzie hello kodowane dane wyjściowe powinny przejdź do. Podobne powitalne toohow podstawowy plik źródłowy został skonfigurowany, skonfiguruj teraz hello właściwość zmiennej folderu wyjściowego, tuż pod.

![Skonfigurowanych właściwości dane wejściowe i wyjściowe](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

*Skonfigurowanych właściwości dane wejściowe i wyjściowe*

### <a id="MXF_to_MP4_streams"></a>Zapoznanie się strumieni nośnika
Często jest potrzebne, że tooknow tak jak wygląd strumienia hello przechodzi przez hello przepływu pracy. tooinspect strumienia w dowolnym momencie w przepływie pracy hello, wystarczy kliknąć danych wyjściowych lub wejściowych numeru pin na dowolnym hello składników. W takim przypadku spróbuj kliknięcie hello końcówka wyjściowa nieskompresowanym wideo z naszych danych wejściowych pliku nośnika. Okno dialogowe będzie otwarcie umożliwiający tooinspect hello wychodzącego wideo.

![Zapoznanie się hello wideo nieskompresowanych danych wyjściowych numeru pin](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

*Zapoznanie się hello wideo nieskompresowanych danych wyjściowych numeru pin*

W tym przypadku informuje nas na przykład czy możemy Cię zajmujących się wprowadzania 1920 x 1080 pikseli na 24 klatek na sekundę w 4: próbkowania 2:2 film prawie 2 minuty.

### <a id="MXF_to_MP4_file_generation"></a>Dodawanie koder wideo dla. Generowanie pliku MP4
Należy pamiętać, że teraz, wiele końcówek wyjściowych nieskompresowanych Audio i wideo nieskompresowanych są dostępne do użycia w naszym wejście pliku nośnika. W kolejności tooencode hello przychodzących wideo, w tym przypadku należy kodowania składnika - generowania. Pliki mp4.

tooencode hello tooH.264 strumienia wideo, dodać powierzchni projektanta składników toohello hello AVC koder wideo. Ten składnik przyjmuje Dekompresuj strumienia wideo o jako dane wejściowe, a następnie dostarcza AVC skompresowanego strumienia wideo na jego końcówka wyjściowa.

![Odłączony kodera AVC](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

*Odłączony kodera AVC*

Jego właściwości określają, jak dokładnie kodowanie hello wykonywana. Załóżmy ma informacje o niektórych hello ważniejsze ustawienia:

* Dane wyjściowe szerokości i wysokości danych wyjściowych: je określić rozdzielczość hello hello zakodowane wideo. W tym przypadku Użyjmy 640 x 360
* Szybkość klatek: toopassthrough zestaw, który będzie po prostu przyjmuje szybkość klatek hello źródła, jest możliwe toooverride takim jednak. Należy pamiętać, że takie konwersji szybkość klatek jest nie ruchu — równoważone.
* Profil i poziom: te określenia profilu hello AVC i poziom. tooconveniently uzyskać więcej informacji o różnych poziomach hello i profile, kliknij ikonę znaku zapytania hello na powitania koder wideo AVC składnika i strona pomocy hello wyświetli szczegółowe informacje o każdym z poziomów hello. Dla naszej próbki Użyjmy Main profilu na poziomie 3.2 (domyślnie: hello).
* Oceń tryb kontroli i szybkości transmisji bitów (KB/s): w naszym scenariuszu będziemy wybrać stałej szybkości transmisji bitów (CBR) dane wyjściowe w 1200 kb/s
* Format wideo: jest to o hello VUI (wideo użyteczność informacje) pobiera zapisywane do strumienia H.264 hello (dekodowania informacji po stronie, które mogą być używane przez wyświetlanie hello tooenhance dekoder, ale nie są niezbędne toocorrectly):
* NTSC (typowa dla Stanów Zjednoczonych lub Japonii przy użyciu 30 kl. / s)
* PAL (typowa dla Europy, przy użyciu 25 kl. / s)
* Tryb rozmiaru GOP: skonfigurujemy o stałym rozmiarze GOP dla naszych celów z klucza interwałem równym 2 sekundy z GOPs zamknięte. To zapewnia zgodność z hello, który udostępnia funkcję dynamicznego tworzenia pakietów usługi Azure Media Services.

toofeed naszych kodera AVC połączyć końcówka wyjściowa hello nieskompresowanym wideo z hello nośnika pliku wejściowego składnika toohello nieskompresowanym wideo wprowadzania numeru pin z hello AVC kodera.

![Połączone kodera AVC](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

*Połączone kodera AVC Main*

### <a id="MXF_to_MP4_audio"></a>Kodowania hello strumieniem audio
Na tym etapie firma Microsoft, są zakodowane wideo, ale hello oryginalnego strumieniem audio nieskompresowanych nadal wymaga toobe skompresowane. W tym znajdują się z AAC kodowania hello składnika kodera AAC (Dolby). Dodaj toohello przepływu pracy.

![Odłączony kodera AVC](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

*Odłączony AAC kodera*

Teraz występuje niezgodność: istnieje tylko jeden nieskompresowanych audio wprowadzania numeru pin z hello kodera AAC podczas więcej niż prawdopodobnie hello nośnika plik wejściowy ma dwa różne nieskompresowane strumieniem audio dostępne: jeden dla hello lewego kanału audio i jeden dla hello prawo. (Jeśli jest zajmujących dźwięk przestrzenny, który jest kanały 6). Dlatego nie jest możliwe toodirectly połączenie z hello audio ze źródła danych wejściowych plików nośnika hello kodera audio AAC hello. Witaj składnika AAC oczekuje tak zwane "przeplotem" strumieniem audio: pojedynczy strumień, który ma zarówno atrybut hello po lewej i hello kanały prawo przeplatana ze sobą. Po wiemy z naszych pliku nośnika źródłowego które ścieżki audio na pozycji w źródle hello firma Microsoft może wygenerować takie przeplotem strumieniem audio z hello poprawnie przypisano prelegenta pozycji lewy i prawy.

Najpierw należy jedną toogenerated przeplotem strumienia z hello wymagane źródła audio kanałów. składnik Interleaver strumień Audio Hello obsłuży to firmie Microsoft. Dodaj ją toohello przepływu pracy i połącz dane wyjściowe audio hello z hello wejście pliku multimediów do niego.

![Połączone Interleaver strumieniem Audio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

*Połączone Interleaver strumieniem Audio*

Teraz, gdy mamy przeplotem strumieniem audio, będziemy nadal nie określić gdzie tooassign hello lewego lub prawego osoby mówiącej pozycji. To zamówienie toospecify, możemy wykorzystać hello Assigner stanowisko osoby mówiącej.

![Dodawanie Assigner stanowisko osoby mówiącej](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

*Dodawanie Assigner stanowisko osoby mówiącej*

Skonfigurować hello Assigner stanowisko osoby mówiącej do użycia przy użyciu stereo strumień wejściowy za pomocą kodera ustawień wstępnych filtru "Custom" i hello kanału ustawień o nazwie "2.0 (L, R)". (Spowoduje to przypisanie hello prelegenta po lewej stronie pozycji toochannel 1 i hello prelegenta prawa pozycja toochannel 2.)

Połącz dane wyjściowe hello hello Assigner stanowisko osoby mówiącej toohello danych wejściowych hello AAC kodera. Następnie należy wskazać toowork kodera AAC hello "2.0 (L, R)" zdefiniowane kanału, który będzie wówczas traktował toodeal stereo dźwięku jako dane wejściowe.

### <a id="MXF_to_MP4_audio_and_fideo"></a>Strumienie multipleksowania Audio i wideo do kontenera MP4
Podany naszych AVC zakodowanego strumienia wideo i naszych AAC zakodowane strumieniem audio, firma Microsoft może zarówno do przechwytywania. Kontener MP4. proces Hello łączenie różnych strumieni w jedno jest nazywany "Multipleksowanie" (lub "muxing"). W takim przypadku możemy Cię z przeplotem hello audio i wideo strumieni hello w jednej spójnej. Pakiet MP4. Hello składnik, który koordynuje ten formularz. Kontener MP4 jest nazywany hello multiplekser ISO MPEG-4. Dodaj jeden toohello powierzchni projektanta i połącz zarówno hello koder wideo AVC i hello kodera AAC tooits w danych wejściowych.

![Połączone MPEG4 multiplekser](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

*Połączone MPEG4 multiplekser*

### <a id="MXF_to_MP4_writing_mp4"></a>Zapisywanie pliku MP4 hello
Podczas zapisywania pliku wyjściowego, składnik dane wyjściowe pliku hello jest używany. Możemy połączyć się z tym toohello dane wyjściowe hello multiplekser ISO MPEG-4, tak, aby jego dane wyjściowe pobiera zapisywane toodisk. toodo, Połącz hello kontenera (MPEG-4) dane wyjściowe numeru pin toohello zapisu wejściowy kod pin hello pliku wyjściowego.

![Połączone dane wyjściowe pliku](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

*Połączone dane wyjściowe pliku*

Witaj nazwę pliku, który będzie używany jest określana przez hello właściwości pliku. Tej właściwości mogą być zapisane na stałe tooa danej wartości, co prawdopodobnie będą tooset go za pomocą wyrażenia zamiast tego.

przepływ pracy hello toohave automatycznie określić dane wyjściowe hello plików właściwość name z wyrażenia, kliknij hello przycisku następnej nazwy pliku toohello (toohello folderu dalej). Z hello menu rozwijane, a następnie wybierz pozycję "Wyrażenie". Zostanie wyświetlone okno edytora wyrażeń hello. Najpierw wyczyść zawartość hello hello edytora.

![Pusty edytora wyrażeń](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

*Pusty edytora wyrażeń*

Edytor wyrażeń Hello umożliwia tooenter literał, mieszane z co najmniej jedną zmienną. Zmienne zaczynać się znak dolara ($). Jak naciśniesz klawisz $ hello Edytor hello zostaną wyświetlone w polu listy rozwijanej dzięki szerokiemu wyborowi dostępnych zmiennych. W tym przypadku użyjemy kombinację zmiennej katalog wyjściowy hello oraz zmienna nazwy pliku wejściowego podstawowego hello:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Wypełnione limit edytora wyrażeń](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

*Wypełnione limit edytora wyrażeń*

> [!NOTE]
> W kolejności toosee Zobacz pliku wyjściowego zadania kodowania na platformie Azure, należy podać wartość w edytorze wyrażenie hello.
>
>

Po potwierdzeniu hello wyrażenie za pomocą ok okna właściwości hello będzie podglądu toowhat wartość hello pliku właściwości rozwiązuje w tym momencie.

![Wynikiem rozpoznania wyrażenia pliku jest katalog wyjściowy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

*Wynikiem rozpoznania wyrażenia pliku jest katalog wyjściowy*

### <a id="MXF_to_MP4_asset_from_output"></a>Tworzenie zasobów usługi multimediów z pliku wyjściowego hello
Gdy firma Microsoft ma zapisywanie pliku wyjściowego MP4, potrzebujemy nadal tooindicate czy ten plik należy toohello output zasobów, które usługi media services wygeneruje wyniku wykonania ten przepływ pracy. toothis celu hello węzła zawartości pliku wyjściowej na kanwie przepływu pracy hello jest używany. Wszystkie pliki przychodzące do tego węzła spowoduje, że część hello wynikowy zasobów usługi Azure Media Services.

Połącz hello dane wyjściowe pliku składnika toohello zawartości pliku wyjściowej składnika toofinish hello przepływu pracy.

![Zakończono przepływu pracy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

*Zakończono przepływu pracy*

### <a id="MXF_to_MP4_test"></a>Test hello Zakończono lokalnie przepływu pracy
workflow hello tootest lokalnie, kliknij przycisk play hello na powitania narzędzi u góry hello. Po zakończeniu wykonywania przepływu pracy hello inspekcję hello dane wyjściowe generowane w folderze wyjściowym hello skonfigurowane. Zobaczysz, że plik wyjściowy MP4, które zakodowano z pliku źródła danych wejściowych MXF hello Zakończono hello.

## <a id="MXF_to_MP4_with_dyn_packaging"></a>Kodowanie MXF do MP4 - multibitrate włączoną funkcję dynamicznego tworzenia pakietów
W tym przewodniku utworzymy zestaw wielu plików MP4 z algorytmem AAC audio z jednej. Plik wejściowy MXF.

Do użycia w połączeniu z funkcji dynamicznego tworzenia pakietów hello oferowanych przez usługi Azure Media Services, wielu plików MP4 wyrównane GOP każdego różne szybkości transmisji bitów i rozwiązanie będzie konieczne toobe generowane podczas wyjścia zasobów wielokrotnej szybkości transmisji bitów jest pożądana. Dlatego hello toodo [kodowanie MXF do pojedynczej szybkości transmisji bitów MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) wskazówki zapewnia dobry punkt wyjścia.

![Uruchamianie przepływu pracy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

*Uruchamianie przepływu pracy*

### <a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Dodanie jednego lub więcej dodatkowych danych wyjściowych MP4
Każdy plik MP4 w naszym wynikowy zasobów usługi Azure Media Services będzie obsługiwać różne szybkości transmisji bitów i rozdzielczość. Możemy dodać co najmniej jeden MP4 dane wyjściowe pliki toohello przepływu pracy.

toomake czy mamy hello wszystkich naszych wideo koderów utworzone za pomocą tych samych ustawień, jego najodpowiedniejszym tooduplicate hello już istniejącą koder wideo AVC i skonfigurować kombinację inną rozdzielczość i szybkość transmisji bitów (Dodajmy jedną 960 x 540 na 25 klatek na sekundę w 2,5 MB/s). tooduplicate hello istniejących kodera kopiowania wklej go na powierzchni projektanta hello.

Połącz hello wideo nieskompresowanych danych wyjściowych kod pin hello wejście pliku multimediów do naszego nowego składnika AVC.

![Drugi kodera AVC połączone](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

*Drugi kodera AVC połączone*

Teraz dostosowania hello konfiguracji dla naszego nowego AVC koder toooutput 960 x 540 2,5 MB/s. (Użyj właściwości "dane wyjściowe szerokości", "Dane wyjściowe height" i "Szybkości transmisji bitów (KB/s)" to).

Podane chcemy toouse hello wynikowy zasobów wraz z usługi Azure Media Services dynamicznego tworzenia pakietów, hello punktu końcowego przesyłania strumieniowego musi toobe może generować z tych plików MP4 HLS/podzielonej zawartości MP4/DASH fragmentów, które są dokładnie wyrównany tooeach innych w sposób czy klientów, którzy są przełączanie między różne szybkości transmisji bitów Pobierz pojedynczy smooth ciągłego wideo i audio środowisko. toomake to zrobić, potrzebujemy tooensure, że w właściwości hello zarówno koderów AVC hello rozmiar GOP ("grupa obrazów") dla oba pliki MP4 wartość too2 sekund, które można to zrobić:

* Ustawianie rozmiaru GOP tooFixed Tryb rozmiaru GOP hello i
* Witaj Interwał ramki klucza tootwo sekund.
* również ustawić hello tooensure GOP tooClosed GOP IDR kontroli, które stoją wszystkich GOP na ich własnych bez zależności

toomake naszych wygodne toounderstand przepływu pracy, Zmień nazwę pierwszego kodera AVC hello zbyt "koder wideo AVC 640 x 360 1200 kb/s" i hello drugi kodera AVC "koder wideo AVC 960 x 540 2500 KB/s".

Teraz należy dodać drugi multiplekser ISO MPEG-4, a drugi dane wyjściowe pliku. Połącz hello multiplekser toohello nowe AVC koder i upewnij się, że dane wyjściowe są kierowane do hello pliku wyjściowego. Także połączyć nowy toohello dane wyjściowe kodera audio AAC hello multiplekser w danych wejściowych. Hello pliku wyjściowego z kolei będzie tooadd węzła zawartości pliku wyjściowej połączonych toohello on toohello zasobów usługi nośnika, który zostanie utworzony.

![Drugi Muxer i dane wyjściowe pliku połączone](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

*Drugi Muxer i dane wyjściowe pliku połączone*

Zgodność z dynamicznego tworzenia pakietów usługi Azure Media Services skonfiguruj hello multiplekser w trybie fragmentu tooGOP liczby lub czasu trwania, a następnie ustaw GOPs hello na too1 fragmentu. (Musi to być domyślny hello).

![Tryby fragmentu Muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

*Tryby fragmentu Muxer*

Uwaga: możesz toorepeat ten proces dla innych szybkości transmisji bitów i rozpoznawania kombinacji ma toohave dodać toohello zasobów w danych wyjściowych.

### <a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Konfigurowanie nazwy wyjściowego pliku hello
Istnieje więcej niż jeden zasób danych wyjściowych toohello pojedynczy plik dodany. Zapewnia to konieczność toomake czy powitalne nazwy plików dla każdego hello output plików różnią się od siebie i może nawet stosowana Konwencja nazewnictwa plików, dlatego okazuje się od nazwy pliku hello co w przypadku pracy nad.

Nazywanie pliku danych wyjściowych można sterować za pomocą wyrażenia w Projektancie hello. Otwórz okienko właściwości hello do jednego ze składników danych wyjściowych w pliku hello a hello edytora wyrażeń dla hello właściwości pliku. Nasze pierwszy plik wyjściowy został skonfigurowany za pomocą następującego wyrażenia hello (zobacz hello samouczek dotyczący z [MXF tooa pojedynczej szybkości transmisji bitów danych wyjściowych MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

Oznacza to, że nasze filename jest określany przez dwie zmienne: hello output toowrite katalogu w i hello podstawowa nazwa pliku źródłowego. była Hello jest udostępniany jako właściwość hello głównego przepływu pracy i ostatnie hello jest określany przez hello pliku przychodzących. Należy pamiętać, że katalog wyjściowy hello, które jest używane do testowania lokalnego; Ta właściwość zostanie zastąpiona hello aparatu przepływu pracy podczas wykonywania przepływu pracy hello przez procesor multimediów oparte na chmurze hello w usłudze Azure Media Services.
toogive oba pliki wyjście nazewnictwa spójności danych wyjściowych, hello zmiany pliku najpierw wyrażenie nazewnictwa:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

a drugi hello do:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

Wykonanie pośrednich testu toomake się, że poprawnie są generowane zarówno pliki wyjściowe MP4.

### <a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Dodawanie oddzielne ścieżkę Audio
Jako zajmiemy się później gdy firma Microsoft generuje toogo plik .ism z naszych pliki wyjściowe MP4, zostanie również wymagamy tylko dźwięk plik MP4 jako ścieżka audio hello do naszej adaptacyjnego przesyłania strumieniowego. toocreate ten plik, Dodaj dodatkowe muxer toohello przepływu pracy (ISO-MPEG-4 multiplekser) i połącz końcówka wyjściowa hello AAC kodera przy jego wprowadzania numeru pin dla ścieżki 1.

![Audio Muxer dodane](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

*Audio Muxer dodane*

Utwórz innego strumienia wychodzącego toooutput hello dane wyjściowe pliku składnika z hello muxer i skonfiguruj hello wyrażenie nazewnictwa plików jako:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Audio Muxer tworzenia pliku wyjściowego](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

*Audio Muxer tworzenia pliku wyjściowego*

### <a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Dodawanie hello. Plik SMIL ISM
Dla toowork dynamicznego tworzenia pakietów hello w połączeniu z obu MP4 plików (i hello tylko dźwięk MP4) w naszym zasobów usługi Media Services, potrzebujemy również pliku manifestu (skrót pliku "SMIL": synchronizowane języka integrację multimediów). Ten plik wskazuje tooAzure Media Services, które pliki MP4 są dostępne dla dynamicznego tworzenia pakietów, które z tych tooconsider przesyłania strumieniowego audio hello. Typowy pliku manifestu zestawu MP4 w jednym strumieniem audio wygląda następująco:

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

zawiera plik .ism Hello w instrukcji switch tooeach odwołanie poszczególnych plików wideo hello MP4 i dodatkowo plik dźwiękowy toothose również jednej (lub więcej) odwołuje się do tooan MP4, zawiera tylko hello audio.

Generowanie pliku manifestu hello naszego zestawu w MP4 może odbywać się za pośrednictwem składnik o nazwie "AMS manifestu Writer" hello. toouse, przeciągnij go na powierzchnię hello i połączyć końcówek wyjściowych "Zapisu ukończone" hello z hello trzy dane wyjściowe pliku składniki toohello AMS manifestu modułu zapisywania danych wejściowych. Następnie upewnij się, że tooconnect hello dane wyjściowe hello toohello AMS manifestu zapisywania zawartości pliku wyjściowej.

Zgodnie z naszym innym składnikom pliku wyjściowego, skonfiguruj Nazwa wyjściowego pliku .ism hello z wyrażeniem:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

Nasze Zakończono przepływu pracy wygląda hello poniżej:

![Zakończono MXF toomultibitrate MP4 przepływu pracy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

*Zakończono MXF toomultibitrate MP4 przepływu pracy*

## <a id="MXF_to__multibitrate_MP4"></a>Kodowanie MXF do multibitrate MP4 — rozszerzone planu
W hello [przepływu pracy w poprzednim przewodniku](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) możemy przedstawiono sposób pojedynczego zasobu wejściowego MXF mogą być konwertowane na zawartości wyjściowej z plików MP4 wielokrotnej szybkości transmisji bitów, plik MP4 tylko audio i plik manifestu do użycia w połączeniu z usługi Azure Media Dynamiczne tworzenie pakietów usług.

W tym przewodniku opisano jak niektóre aspekty hello można usprawniać i wprowadzone wygodniejsze.

### <a id="MXF_to_multibitrate_MP4_overview"></a>Tooenhance omówienie przepływu pracy
![Multibitrate MP4 tooenhance przepływu pracy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

*Multibitrate MP4 tooenhance przepływu pracy*

### <a id="MXF_to__multibitrate_MP4_file_naming"></a>Konwencje nazewnictwa plików
W przepływie pracy poprzedniej hello możemy określić proste wyrażenie jako podstawy hello generowania nazwy pliku wyjściowego. Mimo że mamy powielania niektórych: wszystkie składniki pliku danych wyjściowych poszczególnych hello hello określone takie wyrażenie.

Na przykład składnik dane wyjściowe pliku naszych hello pierwszy plik wideo jest skonfigurowany z tego wyrażenia:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

Natomiast w przypadku hello drugi wyjście wideo, mamy wyrażeń, takich jak:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

Nie będą czyszczący mniej błędów podatnych na błędy i bardziej wygodne, jeśli firma Microsoft może. Usuń niektóre tego duplikowania i Postaramy przeprowadzanie łatwiejszych do skonfigurowania zamiast tego? Możemy szczęście: hello projektanta wyrażenie możliwości w połączeniu z właściwościami niestandardowymi toocreate możliwości hello w naszym głównym przepływu pracy będą Przekaż nam dodatkową warstwę wygody.

Załóżmy, że firma Microsoft będzie dysków filename konfiguracji od szybkości transmisji bitów hello hello poszczególnych plików MP4. Te szybkości transmisji bitów, firma Microsoft będzie celem tooconfigure w jednej centralnej umieścić (na główny hello naszych wykresu), z której będziesz mieć dostęp do generowania o nazwy pliku tooconfigure i dysku. toodo, Rozpoczniemy publikując hello właściwości szybkości transmisji bitów z obu AVC koderów toohello głównego naszych przepływu pracy, tak że staje się dostępny z obu głównego hello również od koderów hello AVC. (Nawet jeśli wyświetlane w dwóch różnych miejsc, jest tylko jedna wartość podstawowej).

### <a id="MXF_to__multibitrate_MP4_publishing"></a>Właściwości składnika publikacji na powitania głównego przepływu pracy
Otwórz hello pierwszy AVC kodera, przejdź toohello właściwości szybkości transmisji bitów (KB/s) i z listy rozwijanej hello Wybieranie polecenia Opublikuj.

![Właściwość publikacji szybkości transmisji bitów hello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

*Właściwość publikacji szybkości transmisji bitów hello*

Skonfiguruj hello publikowania okna dialogowego toopublish toohello głównego naszych wykresu przepływu pracy z opublikowana nazwa "video1bitrate" i nazwę wyświetlaną do odczytu "Wideo 1 szybkości transmisji bitów". Konfigurowanie niestandardowej nazwy grupy o nazwie "Przesyłania strumieniowego szybkości transmisji bitów" i kliknij przycisk Publikuj.

![Właściwość publikacji szybkości transmisji bitów hello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

*Okno dialogowe publikowania właściwości szybkości transmisji bitów*

Powtórz hello takie same właściwości szybkości transmisji bitów hello hello drugie kodera AVC i nadaj mu nazwę "video2bitrate" o nazwie wyświetlanej "Wideo 2 szybkości transmisji bitów", w hello sam niestandardowe grupy "Przesyłania strumieniowego szybkości transmisji bitów".

Jeśli mamy teraz sprawdzić właściwości głównej hello przepływu pracy, widzimy naszej grupy niestandardowe z powitalne widoczne dwie właściwości opublikowane. Oba zdarzenie odzwierciedla wartość hello ich odpowiednich AVC kodera szybkości transmisji bitów.

![Właściwości opublikowanych szybkości transmisji bitów w katalogu głównym przepływu pracy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

Zawsze, gdy chcemy tooaccess te właściwości z kodu lub wyrażenie, możemy to zrobić następująco:

* z wbudowanego kodu ze składnika bezpośrednio pod głównego hello: node.getPropertyAsString('.. / video1bitrate ", null)
* w wyrażeniu: ${ROOT_video1bitrate}

Umożliwia zakończenie grupy "Przesyłania strumieniowego szybkości transmisji bitów" hello publikując naszych ścieżki audio szybkości transmisji bitów w nim również. W ramach właściwości hello hello AAC kodera Wyszukaj hello ustawienie szybkości transmisji bitów i wybierz publikowania tooit dalej hello listy rozwijanej. Publikowanie głównego toohello hello wykresu o nazwie "audio1bitrate" i nazwie "Audio 1 szybkości transmisji bitów" w naszej grupy niestandardowe "Przesyłania strumieniowego szybkości transmisji bitów" wyświetlanej.

![Okno dialogowe publikowania audio szybkości transmisji bitów](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

*Okno dialogowe publikowania audio szybkości transmisji bitów*

![Wynikowa właściwości audio i wideo w folderze głównym](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

*Wynikowa właściwości audio i wideo w folderze głównym*

Zauważ, że zmiana któregoś z tych trzech wartości również ponownie konfiguruje i zmiany hello wartości na powitania odpowiednie składniki są one połączone z (i w przypadku, gdy publikowane z).

### <a id="MXF_to__multibitrate_MP4_output_files"></a>Wygenerowano plik wyjściowy, który nazwy zależne od wartości właściwości opublikowanych
Zamiast hardcoding naszych nazwy wygenerowanego pliku możemy można teraz zmienić naszych wyrażenia nazwy pliku na każdym toorely składników danych wyjściowych w pliku hello na powitania szybkości transmisji bitów właściwości, które firma Microsoft właśnie opublikowany w katalogu głównym wykres hello. Począwszy od pierwszego wyjście pliku znaleźć hello właściwości pliku i edytować wyrażenie hello następująco:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

można uzyskać dostępu do i wprowadzone za pomocą dolara hello na klawiaturze hello w okna wyrażenie hello Hello innych parametrów w tym wyrażeniu. Jeden z parametrów dostępnych hello jest właściwość naszych video1bitrate, co możemy wcześniej publikowane.

![Uzyskiwanie dostępu do parametrów w wyrażeniu](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

*Uzyskiwanie dostępu do parametrów w wyrażeniu*

Witaj identyczne dane wyjściowe pliku hello naszych drugi wideo:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

i dla danych wyjściowych w pliku tylko do dźwięk hello:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

Jeżeli zmienimy teraz hello szybkości transmisji bitów dla każdego hello wideo lub audio plików, konfiguracja zostanie zmieniona kodera odpowiednich hello i Konwencji nazwę pliku na podstawie szybkości transmisji bitów hello będą honorowane wszystkie automatyczne.

## <a id="thumbnails_to__multibitrate_MP4"></a>Dodawanie danych wyjściowych MP4 toomultibitrate miniatur
Począwszy od przepływu pracy, który generuje [multibitrate MP4 wyjściowymi MXF wejściowych](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), możemy teraz będzie wyszukiwania na dodawanie danych wyjściowych toohello miniatur.

### <a id="thumbnails_to__multibitrate_MP4_overview"></a>Miniatur tooadd omówienie przepływu pracy
![Multibitrate MP4 toostart przepływu pracy z](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

*Multibitrate MP4 toostart przepływu pracy z*

### <a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Dodawanie kodowania JPG
Puls Hello naszych miniatur generacji będą hello składnika kodera JPG, toooutput stanie JPG — pliki.

![Koder JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

*Koder JPG*

Firma Microsoft nie można jednak bezpośrednio połączyć naszych strumienia wideo nieskompresowanych z hello wejście pliku multimediów do kodera JPG hello. Zamiast tego oczekuje się, że toobe przekazać poszczególnych klatek. To, możemy za pośrednictwem składnika brama ramki wideo hello.

![Łączenie koder ramki bramy toohello JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

*Łączenie koder ramki bramy toohello JPG*

Brama ramki powitania po co tyle sekund lub ramki umożliwia toopass klatki. czas interwału i hello Hello przesunięcia, z którym dzieje się to można skonfigurować we właściwościach hello.

![Właściwości ramki bramy wideo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

*Właściwości ramki bramy wideo*

Umożliwia utworzenie miniatury co minutę przez ustawienie hello tryb tooTime (w sekundach) i hello too60 interwału.

### <a id="thumbnails_to__multibitrate_MP4_color_space"></a>Zajmujących się konwersji przestrzeń kolorów
Gdy logiczne wydaje zarówno teraz może być połączony PIN nieskompresowanym wideo hello ramki bramy i hello wejście pliku multimediów, możemy otrzyma ostrzeżenie, jeśli firma Microsoft może to zrobić.

![Koloru okna wprowadzania komunikat o błędzie](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

*Koloru okna wprowadzania komunikat o błędzie*

Jest to spowodowane sposób hello w kolorze, które informacje jest reprezentowane w naszym oryginalnego raw nieskompresowanych strumienia wideo, pochodzące z naszych MXF różni się od jakiego hello JPG Koder oczekuje. Więcej w szczególności tak zwane "przestrzeń kolorów" "RGB" lub "Skali szarości" jest oczekiwany tooflow w. Oznacza to, że dla ruchu przychodzącego strumienia wideo o tym hello wideo ramki bramy w należy toohave konwersji zastosowana jako pierwsza dotyczące jego przestrzeń kolorów.

Przeciągnij na powitania przepływu pracy hello konwertera miejsca kolor - Intel i podłącz go tooour ramki bramy.

![Łączenie konwertera miejsca kolorów](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

*Łączenie konwertera miejsca kolorów*

W oknie właściwości hello wybierz hello BGR 24 wpisu z listy wstępnie ustawionych hello.

### <a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Zapisywanie hello miniatur
Inne niż filmie MP4, hello kodera JPG, dane wyjściowe obejmują składnika więcej niż jeden plik. W kolejności toodeal z tym, można użyć składnika zapisywania pliku JPG wyszukiwania sceny: go otrzymuje hello przychodzące miniatur JPG i zapisać je, przy kończyły przez inną liczbę nazw plików. (numer hello zwykle wskazuje hello liczbę sekund/jednostek w strumieniu hello, który hello miniatur zostało pobranych z).

![Wprowadzenie hello zapisywania pliku JPG wyszukiwania sceny](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

*Wprowadzenie hello zapisywania pliku JPG wyszukiwania sceny*

Właściwość ścieżki do folderu wyjściowego hello skonfigurować za pomocą wyrażenia hello: ${ROOT_outputWriteDirectory}

i hello właściwość prefiks nazwy pliku:

    ${ROOT_sourceFileBaseName}_thumb_

Prefiks Hello określa sposób nazywania hello miniatur plików. One będą kończyły się słowem numer wskazujące hello położeniu wskaźnika w strumieniu hello.

![Właściwości składnika zapisywania pliku JPG wyszukiwania sceny](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

*Właściwości składnika zapisywania pliku JPG wyszukiwania sceny*

Połącz hello zapisywania pliku JPG wyszukiwania sceny toohello zawartości pliku wyjściowej węzła.

### <a id="thumbnails_to__multibitrate_MP4_errors"></a>Wykrywanie błędów w przepływie pracy
Połącz dane wejściowe hello hello kolor miejsca konwertera toohello raw nieskompresowanych wideo danych wyjściowych. Teraz wykonać testy lokalne powitania przepływu pracy. Istnieje przepływu pracy hello szansa nagle zatrzyma, wykonywanie i oznaczać z czerwonego obramowania na powitania składnik, który wystąpił błąd:

![Błąd konwertera miejsca kolorów](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

*Błąd konwertera miejsca kolorów*

Kliknij ikonę "E" hello nieco red hello prawym górnym rogu hello konwertera miejsca kolor składnika toosee, co to jest przyczyna hello hello kodowania próba nie powiodła się.

![Okno dialogowe kolorów konwertera miejsca](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

*Okno dialogowe kolorów konwertera miejsca*

Monitor przechodzi w stan, jak widać, że hello przychodzące przestrzeń kolorów na standardowe dla konwertera miejsca kolor hello ma rec601 toobe naszych żądanego konwersji YUV tooRGB. Najwyraźniej naszych strumienia nie oznacza jego rec601. (ZAL 601 jest standardem kodowania naprzemiennych analogowy sygnały wideo w formie cyfrowej wideo. Określa aktywnego regionu, obejmujące 720 jasności oraz 360 próbki chrominance w jednym wierszu. kolor Hello kodowanie system jest nazywany YCbCr 4:2:2.)

toofix, firma Microsoft będzie wskazuje na metadanych hello naszych strumienia, który możemy Cię zajmujących rec601 zawartości. toodo, dlatego użyjemy komponent Updater typu danych wideo, który będzie testujemy Between naszych raw źródła i hello kolor miejsca konwersji składnika. Tej aktualizacji typu danych umożliwia ręcznej aktualizacji hello niektórych danych wideo właściwości typu. Skonfiguruj tooindicate kolor miejsca Standard "Rec 601". Spowoduje to hello Updater typu danych wideo tootag hello strumienia z przestrzeń kolorów "Rec 601" hello, jeśli nie było żadnych przestrzeń kolorów jeszcze zdefiniowana. (Nie zastąpi on metadane, chyba że zaznaczono pole wyboru zastąpienie hello.)

![Aktualizowanie kolor miejsce na standardowej na powitania Updater typu danych](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

*Aktualizowanie kolor miejsce na standardowej na powitania Updater typu danych*

### <a id="thumbnails_to__multibitrate_MP4_finish"></a>Zakończono przepływu pracy
Teraz, gdy naszych naszych przepływ pracy został zakończony, wykonaj inną toosee uruchomienia testu, przekaż go.

![Zakończono przepływu pracy dla danych wyjściowych mp4 wielu z miniaturami](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

*Zakończono przepływu pracy dla danych wyjściowych mp4 wielu z miniaturami*

## <a id="time_based_trim"></a>Na podstawie czasu przycinanie multibitrate MP4 danych wyjściowych
Począwszy od przepływu pracy, który generuje [multibitrate MP4 wyjściowymi MXF wejściowych](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), możemy teraz będzie wyszukiwania do przycinanie hello źródła wideo oparte na sygnatury czasowe.

### <a id="time_based_trim_start"></a>Dodawanie przycinanie do toostart omówienie przepływu pracy
![Uruchamianie przepływu pracy tooadd przycinanie do](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

*Uruchamianie przepływu pracy tooadd przycinanie do*

### <a id="time_based_trim_use_stream_trimmer"></a>Przy użyciu hello przycinarka strumienia
składnik przycinarka strumienia Hello umożliwia tootrim hello początek i koniec strumienia wejściowego podstawą informacji (sekundy, minuty,...). Przycinarka Hello nie obsługuje przycinania na podstawie ramki.

![Przycinarka do strumienia](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

*Przycinarka do strumienia*

Zamiast bezpośrednio łączenie koderów hello AVC i osoby mówiącej pozycji assigner toohello wejście pliku nośnika, będzie testujemy Between tych hello przycinarka strumienia. (Jeden hello sygnał wideo i drugi dla hello przeplotu sygnału dźwiękowego).

![Umieść przycinarka strumienia między nimi](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

*Umieść przycinarka strumienia między nimi*

Skonfigurujmy przycinarka hello, dzięki czemu będą przetwarzane są jedynie wideo i audio między 15 sekund i 60 sekund na powitania wideo.

Przejdź do właściwości toohello hello przycinarka strumienia wideo i skonfigurować czas rozpoczęcia (15 s) i właściwości godzina zakończenia (60s). toomake się, że zarówno naszych przycinarka audio i wideo są zawsze skonfigurowanego toohello sam rozpoczęcia i zakończenia wartości, firma Microsoft opublikuje tych głównego toohello hello przepływu pracy.

![Publikowanie właściwości czasu rozpoczęcia z przycinarka strumienia](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

*Publikowanie właściwości czasu rozpoczęcia z przycinarka strumienia*

![Okna dialogowego właściwości publikowania dla godziny rozpoczęcia](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

*Okna dialogowego właściwości publikowania dla godziny rozpoczęcia*

![Okna dialogowego właściwości publikowania dla godzina zakończenia](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

*Okna dialogowego właściwości publikowania dla godzina zakończenia*

Jeśli mamy teraz sprawdzić głównego hello naszych przepływu pracy, obie właściwości będzie starannie wyświetlane i można skonfigurować z tego miejsca.

![Opublikowanych właściwości dostępne w folderze głównym](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

*Opublikowanych właściwości dostępne w folderze głównym*

Teraz Otwórz właściwości przycinanie hello z hello przycinarka audio i skonfigurować zarówno rozpoczęcia i zakończenia z wyrażeniem, które odwołuje się toohello opublikowane właściwości w katalogu głównym hello naszych przepływu pracy.

Czas rozpoczęcia przycinanie audio hello:

    ${ROOT_TrimmingStartTime}

i jego czas zakończenia:

    ${ROOT_TrimmingEndTime}

### <a id="time_based_trim_finish"></a>Zakończono przepływu pracy
![Zakończono przepływu pracy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

*Zakończono przepływu pracy*

## <a id="scripting"></a>Wprowadzenie hello składnika uwzględnione w skryptach
Składniki inicjowanych przez skrypty można wykonywanie skryptów dowolnego podczas fazy wykonywania hello naszych przepływu pracy. Istnieją cztery różne skrypty, które mogą być wykonywane każdego z określonych parametrów i miejsca w cyklu życia hello przepływu pracy:

* **commandScript**
* **realizeScript**
* **processInputScript**
* **lifeCycleScript**

w dokumentacji Hello hello inicjowanych przez skrypty składnika przechodzi bardziej szczegółowo dla każdego z powyższych hello. W [hello następujących sekcji](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** skryptów składnika jest używane tooconstruct xml cliplist na bieżąco hello podczas uruchamiania przepływu pracy hello. Ten skrypt jest wywoływana podczas instalacji składnika hello, który odbywa się tylko raz w cyklu jego życia.

### <a id="scripting_hello_world"></a>Obsługa skryptów w ramach przepływu pracy: Witaj świecie
Przeciągnij składnik inicjowanych przez skrypty na powierzchnię projektanta hello i jego nazwa zostanie zmieniona (na przykład "SetClipListXML").

![Dodawanie skryptowej składnika](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Dodawanie skryptowej składnika*

Gdy sprawdzić właściwości hello hello składnika uwzględnione w skryptach, cztery typy inny skrypt zostaną wyświetlone powitalne, każdy inny skrypt tooa można skonfigurować.

![Przy użyciu skryptu właściwości składnika](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Przy użyciu skryptu właściwości składnika*

Wyczyść hello processInputScript i Otwórz Edytor hello hello realizeScript. Teraz możemy konfiguracji i gotowe toostart skryptów.

Skrypty są zapisywane w Groovy, dynamicznie skompilowanej język skryptów dla platformy Java hello, który zachowuje zgodność z językiem Java. W rzeczywistości większość kodu języka Java jest prawidłowym kodem Groovy.

Napisz skrypt groovy proste hello world w kontekście hello naszych realizeScript. Wprowadź poniżej hello w edytorze hello:

    node.log("hello world");

Teraz można wykonać uruchomienia testu lokalnego. Po tym przebiegu inspekcji (za pośrednictwem karty systemu hello na hello inicjowanych przez skrypty składnika) hello właściwości dzienników.

![Witaj świecie dziennika w danych wyjściowych](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

*Witaj świecie dziennika w danych wyjściowych*

Obiekt węzła Hello, który nazywamy metoda rejestrowania hello, odnosi się tooour bieżącego "węzła" lub hello składnika, który jest firma Microsoft skryptów w. Każdy składnik ma tak hello możliwości toooutput rejestrowania danych, dostępna za pośrednictwem karty system hello. W takim przypadku możemy output literał ciągu powitania "hello world". Tutaj toounderstand ważne jest, że to może okazać się toobe nieoceniony narzędzia debugowania, zapewniając wgląd, na jakich skryptów hello jest rzeczywiście ten.

Od w naszym środowisku skryptów mamy także tooproperties dostępu na inne składniki. Wypróbuj:

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

Nasze okno Dziennik wyświetli nam hello następujące:

![Dane wyjściowe dziennika do uzyskiwania dostępu do ścieżki węzła](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

*Dane wyjściowe dziennika do uzyskiwania dostępu do ścieżki węzła*

## <a id="frame_based_trim"></a>Przycinanie multibitrate MP4 dane wyjściowe na podstawie ramki
Począwszy od przepływu pracy, który generuje [multibitrate MP4 wyjściowymi MXF wejściowych](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), możemy teraz będzie wyszukiwania do przycinanie hello źródła wideo na podstawie liczby ramki.

### <a id="frame_based_trim_start"></a>Omówienie toostart Dodawanie przycinanie do planu
![Dodawanie przycinanie do toostart przepływu pracy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

*Dodawanie przycinanie do toostart przepływu pracy*

### <a id="frame_based_trim_clip_list"></a>Przy użyciu hello klip listy XML
Wszystkie poprzednie samouczki przepływu pracy My używamy hello składnika nośnika pliku wejściowego jako naszych wideo źródło danych wejściowych. W tym scenariuszu określonych, będzie używany składnik źródłowy listy klip hello zamiast tego. Należy pamiętać, że nie należy hello preferowana metoda działania; tylko hello klip źródło listy jest używane w przypadku toodo rzeczywista Przyczyna tak (podobnie jak w hello poniżej przypadek, w którym czynione korzystanie z możliwości przycinanie listy klip hello).

tooswitch z naszych toohello wejściowy plik nośnika źródła listy klip, przeciągnij składnik źródłowy listy klip hello na powierzchni projektowej hello i połącz hello klip listy numeru pin toohello klip listy XML węzła XML hello projektanta przepływów pracy. Powinno to spowodować wypełnienie hello źródła listy klip z końcówek wyjściowych, zgodnie z tooour wejściowy plik wideo. Obecnie łączyć hello nieskompresowanych Audio i wideo nieskompresowanych numerów PIN z toohello źródła listy klip hello hello odpowiednich koderów AVC i Interleaver strumień Audio. Teraz Usuń hello wejściowy plik nośnika.

![Zastąpione hello wejście pliku multimediów hello klip listy źródłowej](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

*Zastąpione hello wejście pliku multimediów hello klip listy źródłowej*

składnik źródłowy listy klip Hello przyjmuje jako dane wejściowe "Klip listy XML". Podczas wybierania tootest pliku źródłowego hello z lokalnie, ten klip listy xml jest wypełniana automatycznie dla Ciebie.

![Wypełnione automatycznie klip XML listy właściwości](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

*Wypełnione automatycznie klip XML listy właściwości*

Wyszukiwania nieco bliżej toohello xml, to, jak wygląda następująco:

![Okno dialogowe listy klip Edycja](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

*Okno dialogowe listy klip Edycja*

To nie odzwierciedlać możliwości hello hello klip listy XML. Jedną z opcji naszym jest tooadd elementu "Przycinanie" w obszarze źródło audio, jak i wideo hello:

![Dodawanie listy klip toohello przycinania elementu](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

*Dodawanie listy klip toohello przycinania elementu*

Jeśli zmodyfikować xml listy klip hello takie powyżej i wykonać lokalnego uruchomienia testu, zobaczysz hello wideo został poprawnie przycięty od 10 do 20 sekund hello wideo.

Sprzeczne toowhat odbywa się po wykonaniu przebiegu lokalnego, ale tego samego xml cliplist nie miałoby hello sam wpływ, po zastosowaniu w przepływ pracy uruchamiany w usłudze Azure Media Services. Po wygenerowaniu koder Premium Azure jest uruchamiana, hello cliplist xml za każdym razem, gdy ponownie, oparte na powitania pliku wejściowego hello kodowanie podano zadania. Oznacza to, że wszelkie zmiany, nie na powitania xml Niestety zostanie przesłonięte.

xml cliplist hello toocounter są czyszczone po uruchomieniu zadania kodowania, firma Microsoft może ponownie wygenerować go na bieżąco hello zaraz po rozpoczęcia hello naszych przepływu pracy. Takie akcje niestandardowe mogą być pobierane przez co to jest nazywany "Inicjowanych przez skrypty Component". Aby uzyskać więcej informacji, zobacz [Introducing hello inicjowanych przez skrypty składnika](media-services-media-encoder-premium-workflow-tutorials.md#scripting).

Przeciągnij składnik inicjowanych przez skrypty na powierzchnię projektanta hello i zmień jego nazwę za "SetClipListXML".

![Dodawanie skryptowej składnika](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Dodawanie skryptowej składnika*

Gdy sprawdzić właściwości hello hello składnika uwzględnione w skryptach, cztery typy inny skrypt zostaną wyświetlone powitalne, każdy inny skrypt tooa można skonfigurować.

![Przy użyciu skryptu właściwości składnika](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Przy użyciu skryptu właściwości składnika*

### <a id="frame_based_trim_modify_clip_list"></a>Modyfikowanie listy klip hello ze składnika uwzględnione w skryptach
Zanim firma Microsoft może ponownie zapisać hello cliplist xml, który jest generowany podczas uruchamiania przepływu pracy, potrzebujemy toohave dostępu toohello cliplist xml właściwości i zawartość. Firma Microsoft może zrobić następująco:

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Przychodzące listy klip rejestrowany](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

*Przychodzące listy klip rejestrowany*

Najpierw musimy toodetermine sposób z punktu, który do punktu, który chcemy tootrim hello wideo. Publikowanie tego użytkownika bez technical wygodne toohello hello przepływu pracy, toomake głównego toohello dwie właściwości hello wykresu. toodo, kliknij prawym przyciskiem myszy powierzchnię projektanta hello i wybierz opcję "Dodaj właściwość":

* Pierwszą właściwością: "ClippingTimeStart" typu: "Kod CZASOWY"
* Drugie właściwości: "ClippingTimeEnd" typu: "Kod CZASOWY"

![Okno dialogowe właściwości Dodawanie czas uruchomienia wycinka](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

*Okno dialogowe właściwości Dodawanie czas uruchomienia wycinka*

![Opublikowane wycinka właściwości czasu w katalogu głównym przepływu pracy](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

*Opublikowane wycinka właściwości czasu w katalogu głównym przepływu pracy*

Skonfiguruj zarówno właściwości tooa odpowiednią wartość:

![Skonfiguruj hello wycinka właściwości rozpoczęcia i zakończenia](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

*Skonfiguruj hello wycinka właściwości rozpoczęcia i zakończenia*

Teraz z naszych skryptu, możemy uzyskać dostęp do obie właściwości, takie jak to:

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Okno Dziennik przedstawiający początek i koniec wycinka](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

*Okno Dziennik przedstawiający początek i koniec wycinka*

Umożliwia analizowanie ciągów kod czasowy hello w formie wygodniejsze toouse, przy użyciu proste wyrażenie regularne:

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

*Okno Dziennik z danych wyjściowych przeanalizowany kod czasowy*

Dzięki tym informacjom wykonywanego mamy teraz zmodyfikować hello cliplist xml tooreflect hello rozpoczęcia i zakończenia dla hello potrzeby dokładnych ramki wycinka filmu hello.

![Elementy przycinania tooadd kodu skryptu](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

*Elementy przycinania tooadd kodu skryptu*

Zostało to zrobić za pomocą operacje na ciągach normalne manipulowanie. Hello wynikowy klipu listy xml nie są zapisywane właściwości clipListXML toohello hello głównego przepływu pracy za pomocą metody "setProperty" hello. Okno Dziennik powitania po innego testu będzie pokazują hello następujące:

![Rejestrowanie hello wynikowej listy clip](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

*Rejestrowanie hello wynikowej listy clip*

Czy toosee uruchomienia testu, jak strumienie audio i wideo hello została obcięta. Jak należy to zrobić więcej niż jednego uruchomienia testu z różnymi wartościami dla punktów przycinania hello, można zauważyć, że te będą nie brane pod uwagę jednak! Hello przyczyną tego błędu jest tego projektanta hello, w odróżnieniu od hello Azure środowiska uruchomieniowego, jest nie zastąpienie hello cliplist xml każdego uruchomienia. Oznacza to, że tylko hello pierwszego uruchomienia ustawiono hello i wylogowywanie punktów, spowoduje hello xml tootransform, wszystkie inne hello razy naszych klauzuli guard (jeśli (clipListXML.indexOf ("<trim>") == -1)) uniemożliwi dodanie kolejnego przycinania hello przepływu pracy element, gdy istnieje już istnieje.

toomake naszych przepływu pracy wygodne tootest lokalnie, firma Microsoft najlepsze dodać niektóre porządkowania DOM kodu, który sprawdza, czy przycinania element został już istnieje. Jeśli tak, możemy go usuń, aby móc kontynuować, modyfikując xml hello hello nowymi wartościami. Zamiast przy użyciu zwykłego działań na ciągach, jest prawdopodobnie bezpieczniejsze toodo to za pośrednictwem obiektu rzeczywistych xml modelu analizy.

Zanim jednak możemy dodać taki kod, poprosimy Cię o tooadd liczba instrukcje import u hello najpierw uruchomić naszych skryptu:

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

Następnie można dodać hello wymagane czyszczenie kodu:

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

Ten kod przechodzi powyżej punktu hello jaką dodamy hello przycinania elementy toohello cliplist xml.

Na tym etapie firma Microsoft mogą uruchamiać i modyfikować naszych przepływu pracy jako ile chcemy przy jednoczesnym zachowaniu hello zmiany zostały zastosowane kiedykolwiek czasu.    

### <a id="frame_based_trim_clippingenabled_prop"></a>Dodawanie właściwości wygody ClippingEnabled
Jak nie powinny zawsze toohappen przycinanie, umożliwia Zakończ poza naszych przepływu pracy, dodając wygodny Flaga wartości logicznej, która wskazuje, czy chcemy tooenable przycinanie / wycinka.

Podobnie jak przed, publikuje nowy katalog główny toohello właściwości, naszych przepływu pracy o nazwie "ClippingEnabled" typu "BOOLEAN".

![Właściwości włączenia wycinka opublikowane](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

*Właściwości włączenia wycinka opublikowane*

Hello poniżej klauzuli guard proste możemy Sprawdź, czy wymagana jest przycinanie i zdecyduj, czy naszej listy klip jako takie wymaga toobe zmodyfikowane lub nie.

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <a id="code"></a>Kompletny kod
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


## <a name="also-see"></a>Zobacz też
[Wprowadzenie do kodowania w Azure Media Services w wersji Premium](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[Jak tooUse Premium kodowania w usłudze Azure Media Services](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[Kodowanie zawartości na żądanie przy użyciu usługi Azure Media](media-services-encode-asset.md#media-encoder-premium-workflow)

[Formaty i kodeki usługi Media Encoder Premium Workflow](media-services-premium-workflow-encoder-formats.md)

[Przykładowe pliki przepływu pracy](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[Narzędzia usługi Azure Media Services Explorer](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
