---
title: reklam aaaInserting po stronie klienta hello | Dokumentacja firmy Microsoft
description: "W tym temacie przedstawiono sposób reklam tooinsert na hello po stronie klienta."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 65c9c747-128e-497e-afe0-3f92d2bf7972
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: e6eab4aa92918ad734db8ac3a4e7818d02ed7fe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="inserting-ads-on-hello-client-side"></a>Wstawiania reklam na powitania po stronie klienta
Ten temat zawiera informacje na temat tooinsert różne rodzaje reklam na powitania po stronie klienta.

Informacje na temat zamkniętego podpisów i ad obsługi w wideo transmisji strumieniowej na żywo, zobacz [obsługiwane kodowane i standardy wstawiania Ad](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).

> [!NOTE]
> Azure Media Player nie obsługuje obecnie reklam.
> 
> 

## <a id="insert_ads_into_media"></a>Wstawianie reklam do multimediów
Usługa Azure Media Services obsługuje wstawiania reklam za pośrednictwem platformy Media Windows hello: struktur odtwarzaczy. Struktur odtwarzaczy z obsługą ad są dostępne dla urządzeń z systemem Windows 8, Silverlight, Windows Phone 8 i iOS. Każdy framework player zawiera przykładowy kod, przedstawiający sposób tooimplement aplikacja odtwarzacza. Istnieją trzy różne rodzaje reklamy, które można wstawić do nośnika: listy.

* **Liniowy** — pełne reklam ramki Wstrzymaj hello głównego wideo.
* **Rożne** — nakładki reklamy, które są wyświetlane podczas odtwarzania wideo głównego hello, zwykle logo lub inne statyczny obraz umieszczony hello player.
* **Pomocnik** — reklam wyświetlanych poza hello player.

Usługa AD można umieścić w dowolnym momencie hello wideo głównych osi czasu. Gdy tooplay hello ad, które należy wskazać hello player tooplay reklam. Jest to realizowane przy użyciu zestawu standardowych plików opartych na języku XML: wideo Ad Service szablonu (VAST), cyfrowy wideo wielu Ad listy odtwarzania (VMAP) nośnika abstrakcyjny sekwencjonowania szablonu (MASZTÓW) i cyfrowy wideo Player Ad interfejsu definicji (VPAID). Pliki PRZEWAŻAJĄCA określają, jakie toodisplay reklam. Pliki VMAP Określ, kiedy tooplay różnych reklam i zawierać PRZEWAŻAJĄCA XML. Pliki MASZTÓW są inny sposób toosequence reklam, które również mogą zawierać PRZEWAŻAJĄCA XML. Pliki VPAID zdefiniuj interfejs między hello odtwarzacza wideo i hello ad lub serwera usługi ad.

Każdy framework player zmieniło i wszystkie będą opisane w temacie własny. W tym temacie opisano hello podstawowe mechanizmy używane tooinsert reklam. Aplikacji odtwarzacza wideo żądania reklam z serwera ad. Serwer ad Hello może odpowiadać na kilka sposobów:

* Zwraca PRZEWAŻAJĄCA plik
* Zwraca plik VMAP (z osadzonych VAST)
* Zwraca plik MASZTÓW (z osadzonych VAST)
* Zwraca PRZEWAŻAJĄCA plik z VPAID reklam

### <a name="using-a-video-ad-service-template-vast-file"></a>Przy użyciu pliku szablonu (VAST) usługi Ad wideo
PRZEWAŻAJĄCA pliku Określa, jakie ad lub toodisplay reklam. Hello następujący kod XML jest przykładowy plik PRZEWAŻAJĄCA liniowej AD:

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="115571748">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://www.myserver.com/tracking-resource]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <TrackingEvents>
                  <Tracking event="start"><![CDATA[http://www.myserver.com/start-tracking-resource]]></Tracking>
                  <Tracking event="midpoint"><![CDATA[http://www.myserver.com/midpoint-tracking-resource]]></Tracking>
                  <Tracking event="complete"><![CDATA http://www.myserver.com/complete-tracking-resource]]></Tracking>
                  <Tracking event="expand"><![CDATA[http://www.myserver.com/expand-tracking-resource]]></Tracking>
                </TrackingEvents>
                <VideoClicks>
                  <ClickThrough id="Atlas Redirect"><![CDATA[http://www.myserver.com/click-resource]]></ClickThrough>
                  <ClickTracking id="Spare"></ClickTracking>
                </VideoClicks>
                <MediaFiles>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_200_4x3.wmv]]>
                  </MediaFile>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_300_4x3.wmv]]>
                  </MediaFile>
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
          <Extensions>
            <Extension type="Atlas">
            </Extension>
          </Extensions>
        </InLine>
      </Ad>
    </VAST>

ad liniowej Hello jest opisany przez hello <**liniowy**> elementu. Określa czas trwania hello hello AD, śledzenia zdarzeń, kliknij go, kliknij przycisk śledzenia i liczbę **MediaFile** elementów. Zdarzenia śledzenia są określone w hello <**TrackingEvents**> element i umożliwić tootrack serwera ad różnych zdarzeń występujących podczas wyświetlania hello ad. W takim przypadku hello start, punkt środkowy zakończeniu i rozwiń zdarzenia są śledzone. zdarzenia uruchamiania Hello występuje, gdy hello ad jest wyświetlany. Witaj środkowego zdarzenie wystąpi, gdy co najmniej się, że wyświetlił 50% hello ad osi czasu. Zdarzenie ukończenia Hello występuje, gdy hello ad zostało uruchomione toohello zakończenia. Hello rozwiń zdarzenie wystąpi, gdy użytkownik hello rozszerza hello odtwarzacza wideo toofull ekranu. Clickthroughs są określane za pomocą <**przeglądowego**> w elemencie <**VideoClicks**> element i określa identyfikator URI tooa zasobów toodisplay po kliknięciu przez użytkownika hello na powitania ad. ClickTracking jest określona w <**ClickTracking**> elementu również w ramach hello <**VideoClicks**> element i umożliwia określenie zasobu śledzenia toorequest player powitania po kliknięciu hello użytkownika na powitania ad.hello <**MediaFile**> elementy Określ informacje dotyczące określonego kodowania AD. Gdy istnieje więcej niż jeden <**MediaFile**> elementu odtwarzacza wideo hello można wybrać hello optymalne kodowanie hello platformy. 

Liniowy reklam mogą być wyświetlane w określonej kolejności. toodo, dodanie dodatkowych <Ad> toohello elementy VAST pliku i określić kolejność hello przy użyciu atrybutu sekwencji hello. Witaj poniższy przykład przedstawia to:

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="1" sequence="0">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad1trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
      <Ad id="2" sequence="1">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad2trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:30</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
    </VAST>

Rożne reklam są określone w <Creative> również element. powitania po przykładzie <Creative> element, który opisuje rożne ad.

    <Creative id="video" sequence="1" AdID="">
      <NonLinearAds>
        <NonLinear width="216" height="121" minSuggestedDuration="00:00:15">
          <StaticResource creativeType="image/png"><![CDATA[http://myserver/images/image.png]]></StaticResource>
          <StaticResource creativeType="image/jpg"><![CDATA[http://myserver/images/image.jpg]]></StaticResource>
        </NonLinear>
        <TrackingEvents>
             <Tracking event="acceptInvitation"><![CDATA[http://myserver/tracking/trackingID]></Tracking>
             <Tracking event="collapse"><![CDATA[http://myserver/tracking/trackingID2]]></Tracking>
         </TrackingEvents>
       </NonLinearAds>
    </Creative>


Witaj <**NonLinearAds**> element może zawierać co najmniej jeden <**NonLinear**> elementy, które opisują rożne ad. Witaj <**NonLinear**> element określa zasobów hello hello rożne AD. Witaj zasób może być <**StaticResouce**>, <**IFrameResource**>, lub <**HTMLResouce**>. <**StaticResource**> opisuje zasób w innym języku niż HTML i definiuje atrybut creativeType, który określa sposób wyświetlania zasobów hello:

Obraz/gif, image/jpeg, obrazu/png — hello zasobów jest wyświetlana w formacie HTML <**img**> tagu.

Application/x-javascript — hello zasobów jest wyświetlana w formacie HTML <**skryptu**> tagu.

Application/x-shockwave-flash — hello zasobów jest wyświetlana w Flash player.

**IFrameResource** opisuje zasobu HTML, który może być wyświetlany w elementu IFrame. **HTMLResource** opisuje fragment kodu HTML, który można wstawiać do strony sieci web. **TrackingEvents** określić zdarzenia śledzenia i hello toorequest identyfikatora URI, gdy wystąpi zdarzenie hello. W tej próbki hello acceptInvitation i zwijanie zdarzenia są śledzone. Aby uzyskać więcej informacji na temat hello **NonLinearAds** elementu i jego elementów podrzędnych, zobacz IAB.NET/VAST. Należy pamiętać, że hello **TrackingEvents** element znajduje się w obrębie hello **NonLinearAds** elementu zamiast hello **NonLinear** elementu.

Pomocnik reklam są zdefiniowane w <CompanionAds> elementu. Witaj <CompanionAds> element może zawierać jeden lub więcej <Companion> elementów. Każdy <Companion> elementu opisuje ad pomocnika i może zawierać <StaticResource>, <IFrameResource>, lub <HTMLResource> ujętych w hello sam sposób jak w rożne ad. PRZEWAŻAJĄCA plik może zawierać wiele pomocnika reklam i aplikacja odtwarzacza hello można wybrać najodpowiedniejszy toodisplay ad hello. Aby uzyskać więcej informacji o VAST, zobacz [3.0 PRZEWAŻAJĄCA](http://www.iab.net/media/file/VASTv3.0.pdf).

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a>Przy użyciu wielu pliku listy odtwarzania (VMAP) Ad cyfrowy wideo
Plik VMAP pozwala toospecify wystąpieniu podziały ad, jak długo trwa każdego podziału ile reklam mogą być wyświetlane w ramach podziału i jakie typy reklam mogą być wyświetlane podczas podziału. powitania po w przykładowy plik VMAP, który definiuje podział pojedynczego ad:

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
              <Ad id="115571748">
                <InLine>
                  <AdSystem version="2.0 alpha">Atlas</AdSystem>
                  <AdTitle>Unknown</AdTitle>
                  <Description>Unknown</Description>
                  <Survey></Survey>
                  <Error></Error>
                  <Impression id="Atlas"><![CDATA[http://view.atdmt.com/000/sview/115571748/direct;ai.201582527;vt.2/01/634364885739970673]]></Impression>
                  <Creatives>
                    <Creative id="video" sequence="0" AdID="">
                      <Linear>
                        <Duration>00:00:32</Duration>
                        <MediaFiles>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_200_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_300_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_500" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="500" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_500_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_700" maintainAspectRatio="true" scaleable="true" delivery="progressive" bitrate="700" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv]]>
                          </MediaFile>
                        </MediaFiles>
                      </Linear>
                    </Creative>
                  </Creatives>
                </InLine>
              </Ad>
            </VAST>
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

Rozpoczyna się od pliku VMAP <VMAP> element, który zawiera co najmniej jeden <AdBreak> elementy Definiowanie podziału ad. Każdy podziału ad Określa typ podziału, identyfikator podziału i przesunięcie czasu. Atrybut breakType Hello Określa typ hello AD, która może być odtwarzany podczas podziału hello: liniowych, rożne, lub wyświetlić. Wyświetlania reklam mapy tooVAST pomocnika reklam. Można określić więcej niż jeden typ ad w postaci listy rozdzielanej przecinkami (bez spacji). Hello breakID jest opcjonalny identyfikator hello ad. Hello timeOffset Określa, kiedy powinny być wyświetlane hello ad. Można ją określić w jednym z hello następujące sposoby:

1. Godzina w formacie hh: mm: lub GG:mm:ss.mmm .mmm w przypadku milisekund. wartość tego atrybutu Hello określa czas hello od początku hello hello wideo osi czasu rozpoczęcia toohello hello ad podziału.
2. Procent — w formacie n %, gdzie n to hello odsetek hello tooplay wideo osi czasu przed odtwarzanie hello ad
3. Rozpoczęcie i zakończenie — Określa, że usługi ad powinna być wyświetlana przed lub po hello wideo został wyświetlony
4. Umieść — określa kolejność hello podziałów ad, gdy czas hello podziały ad hello jest nieznany, takie jak transmisja strumieniowa na żywo. kolejność Hello każdego podziału ad jest określana w formacie hello #n, gdzie n to liczba całkowita mniejsza od 1. 1 oznacza, że powinien zostać odtworzone hello ad przy okazji pierwszego hello, 2 oznacza hello ad powinna zostać odtworzone przy okazji drugi hello i tak dalej.

W ramach hello <**AdBreak**> element może być jedną <**AdSource**> elementu. Witaj <**AdSource**> element zawiera hello następujące atrybuty:

1. Identyfikator — Określa identyfikator źródła ad hello
2. allowMultipleAds — wartość logiczna określająca, czy wiele reklam mogą być wyświetlane podczas hello ad podziału
3. followRedirects — opcjonalna wartość logiczna określająca, czy hello odtwarzacza wideo należy przestrzegać przekierowuje w odpowiedzi usługi ad

Witaj <**AdSource**> element udostępnia odtwarzacz hello odpowiedzi ad wbudowanego lub odpowiedź ad tooan odwołania. Nazwa może zawierać jeden hello następujące elementy:

* <VASTAdData>Wskazuje, że odpowiedź PRZEWAŻAJĄCA ad jest osadzony w pliku VMAP hello
* <AdTagURI>Identyfikator URI, który odwołuje się do odpowiedzi ad z innego systemu
* <CustomAdData>-dowolnego ciągu tego respresents-PRZEWAŻAJĄCA odpowiedzi

W tym przykładzie odpowiedzi w wierszu ad zostanie określony z <VASTAdData> element, który zawiera odpowiedzi PRZEWAŻAJĄCA ad. Aby uzyskać więcej informacji na temat hello innych elementów zobacz [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).

Witaj <**AdBreak**> element może również zawierać jedną <**TrackingEvents**> elementu. Witaj <**TrackingEvents**> element pozwala tootrack hello początek lub koniec podziału ad lub czy wystąpił błąd podczas hello ad podziału. Witaj <**TrackingEvents**> elementu zawiera jeden lub więcej <**śledzenia**> elementów, z których każdy określa zdarzenia śledzenia i śledzenia identyfikatora URI. zdarzenia śledzenia możliwe Hello są:

1. breakStart — śledzi hello początku podziału ad
2. breakEnd — Śledź hello zakończenia podziału ad
3. Błąd — śledzi wystąpił błąd, który wystąpił podczas hello ad podziału

Hello poniższy przykład przedstawia plik VMAP, który określa zdarzenia śledzenia

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <!--Inline VAST -->
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
          <vmap:Tracking event="breakend">
            http://MyServer.com/breakend.gif
          </vmap:Tracking>
          <vmap:Tracking event="error">
            http://MyServer.com/error.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

Aby uzyskać więcej informacji na temat hello <**TrackingEvents**> elementu i jego elementów podrzędnych, zobacz http://iab.org/VMAP.pdf

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a>Przy użyciu abstrakcyjny nośnika, sekwencjonowania pliku szablonu (MASZTÓW)
Plik MASZTÓW umożliwia toospecify wyzwalaczy, które określają, kiedy jest wyświetlany przy użyciu usług ad. Witaj poniżej znajduje się przykładowy plik MASZTÓW, który zawiera wyzwalacze ad zbiorczego sprzed, ad zbiorczego pośredniej i ad po zbiorczego.

    <MAST xsi:schemaLocation="http://openvideoplayer.sf.net/mast http://openvideoplayer.sf.net/mast/mast.xsd" xmlns="http://openvideoplayer.sf.net/mast" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <triggers>
        <trigger id="preroll" description="preroll every item"  >
          <startConditions>
            <condition type="event" name="OnItemStart" />
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="midroll" description="midroll at 15 sec."  >
          <startConditions>
            <condition type="property" name="Position" value="00:00:15.0" operator="GEQ" />
          </startConditions>
          <endConditions>
            <condition type="event" name="OnItemEnd"/>
            <!--This 'resets' hello trigger for hello next clip-->
          </endConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="postroll" description="postroll"  >
          <startConditions>
            <condition type="event" name="OnItemEnd"/>
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>
      </triggers>
    </MAST>



Rozpoczyna się od pliku MASZTÓW **MASZTÓW** element, który zawiera jeden **wyzwalaczy** elementu. Witaj <triggers> elementu zawiera jeden lub więcej **wyzwalacza** elementów, które określają, kiedy można odtwarzać przy użyciu usług ad. 

Witaj **wyzwalacza** element zawiera **startConditions** elementu, którego Określ rozpoczęcia tooplay ad. Witaj **startConditions** elementu zawiera jeden lub więcej <condition> elementów. Podczas każdego <condition> ocenia tootrue wyzwalacza jest inicjowane lub odwołane, w zależności od czy hello <condition> jest zawarty w **startConditions** lub **endConditions** — element odpowiednio. Gdy wiele <condition> elementy znajdują się, są traktowane jako niejawne OR, wszelkie warunku obliczania tootrue spowoduje, że tooinitiate wyzwalacza hello. <condition>elementy mogą być zagnieżdżone. Gdy podrzędny <condition> elementy są zdefiniowane, są traktowane jak i niejawne, wszystkie warunki musi ocenić tootrue dla hello tooinitiate wyzwalacza. Witaj <condition> element zawiera następujące atrybuty definiujące warunek hello hello: 

1. **Typ** — Określa typ hello zdarzenia lub warunku właściwości
2. **Nazwa** — Witaj nazwa hello właściwości lub zdarzenia toobe używany podczas obliczania
3. **wartość** — Witaj wartość, która będzie porównywany właściwości
4. **operator** — Witaj toouse operacji podczas obliczania: EQ (równości), NEQ (różne), GTR (większe), GEQ (większe lub równe), LT (poniżej), LEQ (mniejsze niż lub równe), MOD (modulo)

**endConditions** również zawierać <condition> elementów. Jeśli wynikiem warunku jest tootrue hello wyzwalacza jest reset.hello <trigger> zawiera również element <sources> element, który zawiera co najmniej jeden <source> elementów. Witaj <source> elementy zdefiniuj hello URI toohello ad odpowiedzi i typ hello ad odpowiedzi. W tym przykładzie identyfikatora URI otrzymuje tooa PRZEWAŻAJĄCA odpowiedzi. 

    <trigger id="postroll" description="postroll"  >
      <startConditions>
        <condition/>
      </startConditions>
      <sources>
        <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
          <sources />
        </source>
      </sources>
    </trigger>


### <a name="using-video-player-ad-interface-definition-vpaid"></a>Przy użyciu odtwarzacza wideo-Ad definicji interfejsu (VPAID)
VPAID to interfejs API umożliwiający toocommunicate jednostki ad pliku wykonywalnego z odtwarzacza wideo. Dzięki temu ad wysokiej interaktywnego środowiska. Hello użytkownik może interakcyjnie hello ad i hello ad mogą odpowiadać tooactions wykonywaną przez hello podglądu. Na przykład ad mogą być wyświetlane przyciski umożliwiające tooview użytkownika hello więcej informacji lub dłużej wersji hello ad. odtwarzacza wideo Hello musi obsługiwać hello VPAID interfejsu API i hello ad pliku wykonywalnego musi implementować interfejs API hello. Gdy odtwarzacza zażąda ad z powitania serwera ad mogą odpowiadać za pomocą PRZEWAŻAJĄCA odpowiedzi, który zawiera VPAID ad.

Wykonywalny ad jest tworzony w kodu, który musi zostać wykonana w środowisko uruchomieniowe, takie jak Adobe Flash™ lub JavaScript, które mogą być wykonywane w przeglądarce sieci web. Po powrocie z serwera ad PRZEWAŻAJĄCA odpowiedzi zawierające VPAID ad hello wartość atrybutu apiFramework hello w hello <MediaFile> element musi być "VPAID". Ten atrybut określa danej reklamy hello zawarty jest VPAID ad pliku wykonywalnego. Atrybut typu Hello musi być ustawiona toohello typ MIME hello pliku wykonywalnego, takie jak "application/x-shockwave-flash" lub "application/x-javascript". Witaj następujący fragment kodu XML zawiera hello <MediaFile> element na podstawie PRZEWAŻAJĄCA odpowiedzi zawierające VPAID ad pliku wykonywalnego. 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


Można zainicjować pliku wykonywalnego ad przy użyciu hello <AdParameters> elementu w obrębie hello <Linear> lub <NonLinear> elementów w PRZEWAŻAJĄCA odpowiedzi. Aby uzyskać więcej informacji na temat hello <AdParameters> elementu, zobacz [3.0 PRZEWAŻAJĄCA](http://www.iab.net/media/file/VASTv3.0.pdf). Aby uzyskać więcej informacji na temat hello VPAID interfejsu API, zobacz [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a>Wdrażanie systemu Windows lub Windows Phone 8 Player z obsługą usługi Ad
Witaj platformy Media firmy Microsoft: Framework Player dla systemu Windows 8 i Windows Phone 8 zawiera kolekcję przykładowe aplikacje, które pokazują, jak tooimplement aplikacji odtwarzacza wideo przy użyciu hello framework. Możesz pobrać hello Player Framework i hello przykłady z [Framework Player dla systemu Windows 8 i Windows Phone 8](https://playerframework.codeplex.com).

Po otwarciu rozwiązania Microsoft.PlayerFramework.Xaml.Samples hello pojawi się liczba folderów w ramach hello projektu. folder reklamy Hello zawiera hello przykładowy kod odpowiednich toocreating odtwarzacza wideo z obsługą usługi ad. Folder reklamy hello wewnątrz jest liczba XAML/cs plików każdy program jak tooinsert reklam w inny sposób. następujące listy Hello opisano poszczególne:

* AdPodPage.xaml pokazuje sposób pod toodisplay ad.
* Pokazuje AdSchedulingPage.xaml jak tooschedule reklam.
* FreeWheelPage.xaml pokazuje, jak toouse hello FreeWheel wtyczki tooschedule reklam.
* Pokazuje MastPage.xaml jak tooschedule reklam z plikiem MASZTÓW.
* ProgrammaticAdPage.xaml pokazuje, jak zaplanować reklam tooprogrammatically do klipu wideo.
* Pokazuje ScheduleClipPage.xaml jak tooschedule ad bez PRZEWAŻAJĄCA pliku.
* Pokazuje VastLinearCompanionPage.xaml jak tooinsert liniowej i ad pomocnika.
* Pokazuje VastNonLinearPage.xaml jak tooinsert ad liniowej.
* Pokazuje VmapPage.xaml jak toospecify reklam z plikiem VMAP.

Każda z tych próbek używa klasy MediaPlayer hello zdefiniowane przez platformę player hello. Większość przykładów za pomocą wtyczki obsługę różnych formatach odpowiedzi ad. Przykładowe ProgrammaticAdPage Hello programowo współdziała z wystąpienia elementu MediaPlayer.

### <a name="adpodpage-sample"></a>Przykładowe AdPodPage
W przykładzie użyto toodefine AdSchedulerPlugin powitania po toodisplay ad. W tym przykładzie anonsu pośredniej zbiorczego jest zaplanowane toobe odtworzony po 5 sekund. Witaj ad pod (grupa toodisplay reklam w kolejności) jest określone w pliku PRZEWAŻAJĄCA zwrócony z serwera usługi ad. Plik PRZEWAŻAJĄCA toohello URI Hello jest określona w hello <RemoteAdSource> elementu.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">

        <mmppf:MediaPlayer.Plugins>
            <ads:AdSchedulerPlugin>
                <ads:AdSchedulerPlugin.Advertisements>

                    <ads:MidrollAdvertisement Time="00:00:05">
                        <ads:MidrollAdvertisement.Source>
                            <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_adpod.xml" Type="vast"/>
                        </ads:MidrollAdvertisement.Source>
                    </ads:MidrollAdvertisement>

                </ads:AdSchedulerPlugin.Advertisements>
            </ads:AdSchedulerPlugin>
            <ads:AdHandlerPlugin/>
        </mmppf:MediaPlayer.Plugins>
    </mmppf:MediaPlayer>

Aby uzyskać więcej informacji na temat hello AdSchedulerPlugin, zobacz [reklamy w hello Framework Player w systemie Windows 8 i Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)

### <a name="adschedulingpage"></a>AdSchedulingPage
W tym przykładzie użyto także hello AdSchedulerPlugin. Planowana trzy reklam, ad wstępne zbiorczego ad zbiorczego pośredniej i ad po zbiorczego. Witaj URI toohello VAST dla każdej usługi ad jest określona w <RemoteAdSource> elementu.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:PrerollAdvertisement>
                                <ads:PrerollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PrerollAdvertisement.Source>
                            </ads:PrerollAdvertisement>

                            <ads:MidrollAdvertisement Time="00:00:15">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                            <ads:PostrollAdvertisement>
                                <ads:PostrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PostrollAdvertisement.Source>
                            </ads:PostrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>


### <a name="freewheelpage"></a>FreeWheelPage
W przykładzie użyto hello FreeWheelPlugin, która określa atrybut źródłowy, który określa identyfikator URI tego pliku SmartXML tooa punktów, które określa ad zawartości, a także informacje o harmonogramie ad.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a>MastPage
W przykładzie użyto hello MastSchedulerPlugin umożliwiający toouse MASZTÓW pliku. atrybut źródłowy Hello Określa lokalizację hello hello MASZTÓW pliku.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a>ProgrammaticAdPage
W tym przykładzie programowo współdziała z hello MediaPlayer. Plik ProgrammaticAdPage.xaml Hello tworzy hello MediaPlayer:

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

Plik ProgrammaticAdPage.xaml.cs Hello tworzy AdHandlerPlugin, dodaje TimelineMarker toospecify, gdy usługi ad powinna być wyświetlana, a następnie dodanie obsługi dla zdarzenia MarkerReached hello, który ładuje RemoteAdSource określenie pliku PRZEWAŻAJĄCA tooa identyfikator URI, a następnie odgrywa Witaj ad.

    public sealed partial class ProgrammaticAdPage : Microsoft.PlayerFramework.Samples.Common.LayoutAwarePage
        {
            AdHandlerPlugin adHandler;

            public ProgrammaticAdPage()
            {
                this.InitializeComponent();
                adHandler = new AdHandlerPlugin();
                player.Plugins.Add(new AdHandlerPlugin());
                player.Markers.Add(new TimelineMarker() { Time = TimeSpan.FromSeconds(5), Type = "myAd" });
                player.MarkerReached += pf_MarkerReached;
            }

            async void pf_MarkerReached(object sender, TimelineMarkerRoutedEventArgs e)
            {
                if (e.Marker.Type == "myAd")
                {
                    var adSource = new RemoteAdSource() { Type = VastAdPayloadHandler.AdType, Uri = new Uri("http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml") };
                    //var adSource = new AdSource() { Type = DocumentAdPayloadHandler.AdType, Payload = SampleAdDocument };
                    var progress = new Progress<AdStatus>();
                    try
                    {
                        await player.PlayAd(adSource, progress, CancellationToken.None);
                    }
                    catch { /* ignore */ }
                }
            }

### <a name="scheduleclippage"></a>ScheduleClipPage
W przykładzie użyto hello AdSchedulerPlugin tooschedule ad pośredniej zbiorczego, określając plik wmv, który zawiera hello ad.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.cloudapp.net/html5/media/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:AdSource Type="clip">
                                        <ads:AdSource.Payload>
                                            <ads:ClipAdPayload MediaSource="http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv" MimeType="video/x-ms-wmv" />
                                        </ads:AdSource.Payload>
                                    </ads:AdSource>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearcompanionpage"></a>VastLinearCompanionPage
W tym przykładzie pokazano, jak toouse hello AdSchedulerPlugin tooschedule pośredniej zbiorczego liniowej usługi ad z usługą Active Directory pomocnika. Witaj <RemoteAdSource> element określa lokalizację hello hello PRZEWAŻAJĄCA pliku.

    <mmppf:MediaPlayer Grid.Row="1"  x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_companions.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearnonlinearpage"></a>VastLinearNonLinearPage
W przykładzie użyto hello AdSchedulerPlugin tooschedule w układzie liniowych i inne usługi ad. Lokalizacja pliku PRZEWAŻAJĄCA Hello jest określany za pomocą hello <RemoteAdSource> elementu.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_nonlinear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vmappage"></a>VMAPPage
Reklam tooschedule VmapSchedulerPlugin hello przy użyciu pliku VMAP korzysta z tej próbki. Hello URI toohello VMAP pliku jest określona w atrybut źródłowy hello hello <VmapSchedulerPlugin> elementu.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a>Implementacja systemu iOS odtwarzacza wideo z obsługą usługi Ad
Witaj platformy Media firmy Microsoft: Framework odtwarzacza dla systemu iOS zawiera kolekcję przykładowe aplikacje, które pokazują, jak tooimplement aplikacji odtwarzacza wideo przy użyciu hello framework. Możesz pobrać hello Player Framework i hello przykłady z [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework). Hello github strona ma tooa łącza typu Wiki, zawierający dodatkowe informacje dotyczące hello player framework i przykładowe player toohello wprowadzenie: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).

### <a name="scheduling-ads-with-vmap"></a>Planowanie reklam z VMAP
powitania po przykładzie pokazano, jak przy użyciu pliku VMAP reklam tooschedule.

    // How tooschedule an Ad using VMAP.
    //First download hello VMAP manifest

    if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVMAP.xml"]])
            {
                [self logFrameworkError];
            }
            else
            {
                // Schedule a list of ads using hello downloaded VMAP manifest
                if (![framework scheduleVMAPWithManifest:manifest])
                {
                    [self logFrameworkError];
                }          
            }

### <a name="scheduling-ads-with-vast"></a>Planowanie reklam z VAST
Hello następujące przykładowe pokazuje, jak tooschedule późne wiązanie PRZEWAŻAJĄCA ad.

    //Example:3 How tooschedule a late binding VAST ad.
    // set hello start time for hello ad
    adLinearTime.startTime = 13;
    adLinearTime.duration = 0;
    // Specify hello URI of hello VAST file
    NSString *vastAd1=@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml";
    // Create an AdInfo object
     AdInfo *vastAdInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URL tooVAST file
    vastAdInfo1.clipURL = [NSURL URLWithString:vastAd1];
    // set running time of ad
    vastAdInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    vastAdInfo1.mediaTime.clipBeginMediaTime = 0;
    vastAdInfo1.mediaTime.clipEndMediaTime = 10;
    vastAdInfo1.policy = @"policy for late binding VAST";
    // specify ad type
    vastAdInfo1.type = AdType_Midroll;
    vastAdInfo1.appendTo=-1;
    adIndex = 0;
    // schedule ad
    if (![framework scheduleClip:vastAdInfo1 atTime:adLinearTime forType:PlaylistEntryType_VAST andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

   Hello następujące przykładowe pokazuje, jak tooschedule wczesne ad PRZEWAŻAJĄCA powiązania.
Przykład: 4 harmonogram wczesnego wiązania PRZEWAŻAJĄCA ad //Download hello VAST plik, jeśli (! [[ framework.adResolver downloadManifest: & manifestu withURL: [URLWithString nsurl OCZEKIWANEGO: @"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) {[self logFrameworkError];} else {adLinearTime.startTime = 7; adLinearTime.duration = 0;

        // Create AdInfo instance
        AdInfo *vastAdInfo2 = [[[AdInfo alloc] init] autorelease];
        vastAdInfo2.mediaTime = [[[MediaTime alloc] init] autorelease];
        vastAdInfo2.policy = @"policy for early binding VAST";
        // specify ad type
        vastAdInfo2.type = AdType_Midroll;
        vastAdInfo2.appendTo=-1;
        // schedule ad
        if (![framework scheduleVASTClip:vastAdInfo2 withManifest:manifest atTime:adLinearTime andGetClipId:&adIndex])
        {
            [self logFrameworkError];
        }
    }

Hello następujące przykładowe pokazuje, jak tooinsert ad za pomocą nierównej Wytnij edycji (rz)

    //Example:1 How toouse RCE.
    // specify manifest for ad content
    NSString *secondContent=@"http://wamsblureg001orig-hs.cloudapp.net/6651424c-a9d1-419b-895c-6993f0f48a26/The%20making%20of%20Microsoft%20Surface-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // specify ad length
    mediaTime.currentPlaybackPosition = 0;
    mediaTime.clipBeginMediaTime = 0;
    mediaTime.clipEndMediaTime = 80;
    // append ad content
    if (![framework appendContentClip:[NSURL URLWithString:secondContent] withMediaTime:mediaTime andGetClipId:&clipId])
    {
        [self logFrameworkError];
    }

Witaj poniższy przykład przedstawia sposób pod tooschedule ad.

    //Example:5 Schedule an ad Pod.
    // Set start time for ad
    adLinearTime.startTime = 23;
    adLinearTime.duration = 0;

    // Specify URL toocontent
    NSString *adpodSt1=@"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    // Create an AdInfo instance
    AdInfo *adpodInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URI tooad content
    adpodInfo1.clipURL = [NSURL URLWithString:adpodSt1];
    // Set ad running time
    adpodInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    adpodInfo1.mediaTime.clipBeginMediaTime = 0;
    adpodInfo1.mediaTime.clipEndMediaTime = 17;
    adpodInfo1.policy = @"policy for ad pod 1";
    // Set ad type
    adpodInfo1.type = AdType_Midroll;
    adpodInfo1.appendTo=-1;
    adIndex = 0;
    // Schedule ad
    if (![framework scheduleClip:adpodInfo1 atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

powitania po przykładzie pokazano, jak tooschedule-trwałe ad pośredniej zbiorczego. Ad trwałe tylko zostanie odtworzony po niezależnie od wszelkich wyszukiwania hello wykonuje podglądu.

    //Example:6 Schedule a single non sticky mid roll Ad
    // specify URL toocontent
    NSString *oneTimeAd=@"http://wamsblureg001orig-hs.cloudapp.net/5389c0c5-340f-48d7-90bc-0aab664e5f02/Windows%208_%20You%20and%20Me%20Together-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // create an AdInfo instance
    AdInfo *oneTimeInfo = [[[AdInfo alloc] init] autorelease];
    // set URL of ad
    oneTimeInfo.clipURL = [NSURL URLWithString:oneTimeAd];
    oneTimeInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    oneTimeInfo.mediaTime.clipBeginMediaTime = 0;
    oneTimeInfo.mediaTime.clipEndMediaTime = -1;
    oneTimeInfo.policy = @"policy for one-time ad";
    // set ad start time
    adLinearTime.startTime = 43;
    adLinearTime.duration = 0;
    // set ad type
    oneTimeInfo.type = AdType_Midroll;
    // non sticky ad
    oneTimeInfo.deleteAfterPlayed = YES;
    // schedule ad
    if (![framework scheduleClip:oneTimeInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

powitania po przykładzie pokazano, jak tooschedule trwałe ad pośredniej zbiorczego. Trwałe ad będą wyświetlane zawsze, gdy określony hello osiągnięciu punktu w hello wideo na osi czasu.

    //Example:7 Schedule a single sticky mid roll Ad
    NSString *stickyAd=@"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *stickyAdInfo = [[[AdInfo alloc] init] autorelease];
    // set URI tooad
    stickyAdInfo.clipURL = [NSURL URLWithString:stickyAd];
    stickyAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    stickyAdInfo.mediaTime.clipBeginMediaTime = 0;
    stickyAdInfo.mediaTime.clipEndMediaTime = 15;
    stickyAdInfo.policy = @"policy for sticky mid-roll ad";
    // set ad start time
    adLinearTime.startTime = 64;
    adLinearTime.duration = 0;
    // set ad type
    stickyAdInfo.type = AdType_Midroll;
    stickyAdInfo.deleteAfterPlayed = NO;
    // schedule ad
    if (![framework scheduleClip:stickyAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }


Hello następujące przykładowe pokazuje, jak tooschedule ad końcu pliku.

    //Example:8 Schedule Post Roll Ad
    NSString *postAdURLString=@"http://wamsblureg001orig-hs.cloudapp.net/aa152d7f-3c54-487b-ba07-a58e0e33280b/wp-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *postAdInfo = [[[AdInfo alloc] init] autorelease];
    postAdInfo.clipURL = [NSURL URLWithString:postAdURLString];
    postAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    postAdInfo.mediaTime.clipBeginMediaTime = 0;
    // set ad length
    postAdInfo.mediaTime.clipEndMediaTime = 45;
    postAdInfo.policy = @"policy for post-roll ad";
    // set ad type
    postAdInfo.type = AdType_Postroll;
    adLinearTime.duration = 0;
    if (![framework scheduleClip:postAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Hello następujące przykładowe pokazuje, jak tooschedule ad wstępne zbiorczego.

    //Example:9 Schedule Pre Roll Ad
    NSString *adURLString = @"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 40; //You could play a portion of an Ad. Yeh!
    adInfo.mediaTime.clipEndMediaTime = 59;
    adInfo.policy = @"policy for pre-roll ad";
    adInfo.appendTo = -1;
    adInfo.type = AdType_Preroll;
    adLinearTime.duration = 0;
    // schedule ad
    if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Witaj następujące przykładowe pokazuje, jak tooschedule pośredniej zbiorczego nakładki ad.

    // Example10: Schedule a Mid Roll overlay Ad
    NSString *adURLString = @"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    //Create AdInfo instance
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 0;
    // specify ad length
    adInfo.mediaTime.clipEndMediaTime = 20;
    adInfo.policy = @"policy for mid-roll overlay ad";
    adInfo.appendTo = -1;
    // specify ad type
    adInfo.type = AdType_Midroll;
    // specify ad start time & duration
    adLinearTime.startTime = 300;
    adLinearTime.duration = 20;
    // schedule ad            if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }



## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zobacz też
[Opracowywanie aplikacji odtwarzacza wideo](media-services-develop-video-players.md)

