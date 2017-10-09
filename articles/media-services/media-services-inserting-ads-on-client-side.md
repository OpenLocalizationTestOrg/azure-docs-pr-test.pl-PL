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
# <a name="inserting-ads-on-hello-client-side"></a><span data-ttu-id="4cbf2-103">Wstawiania reklam na powitania po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="4cbf2-103">Inserting ads on hello client side</span></span>
<span data-ttu-id="4cbf2-104">Ten temat zawiera informacje na temat tooinsert różne rodzaje reklam na powitania po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-104">This topic contains information on how tooinsert various types of ads on hello client side.</span></span>

<span data-ttu-id="4cbf2-105">Informacje na temat zamkniętego podpisów i ad obsługi w wideo transmisji strumieniowej na żywo, zobacz [obsługiwane kodowane i standardy wstawiania Ad](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span><span class="sxs-lookup"><span data-stu-id="4cbf2-105">For information about closed captioning and ad support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span></span>

> [!NOTE]
> <span data-ttu-id="4cbf2-106">Azure Media Player nie obsługuje obecnie reklam.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-106">Azure Media Player does not currently support Ads.</span></span>
> 
> 

## <span data-ttu-id="4cbf2-107"><a id="insert_ads_into_media"></a>Wstawianie reklam do multimediów</span><span class="sxs-lookup"><span data-stu-id="4cbf2-107"><a id="insert_ads_into_media"></a>Inserting Ads into your Media</span></span>
<span data-ttu-id="4cbf2-108">Usługa Azure Media Services obsługuje wstawiania reklam za pośrednictwem platformy Media Windows hello: struktur odtwarzaczy.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-108">Azure Media Services provides support for ad insertion through hello Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="4cbf2-109">Struktur odtwarzaczy z obsługą ad są dostępne dla urządzeń z systemem Windows 8, Silverlight, Windows Phone 8 i iOS.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-109">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="4cbf2-110">Każdy framework player zawiera przykładowy kod, przedstawiający sposób tooimplement aplikacja odtwarzacza. Istnieją trzy różne rodzaje reklamy, które można wstawić do nośnika: listy.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-110">Each player framework contains sample code that shows you how tooimplement a player application.There are three different kinds of ads you can insert into your media:list.</span></span>

* <span data-ttu-id="4cbf2-111">**Liniowy** — pełne reklam ramki Wstrzymaj hello głównego wideo.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-111">**Linear** – full frame ads that pause hello main video.</span></span>
* <span data-ttu-id="4cbf2-112">**Rożne** — nakładki reklamy, które są wyświetlane podczas odtwarzania wideo głównego hello, zwykle logo lub inne statyczny obraz umieszczony hello player.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-112">**Nonlinear** – overlay ads that are displayed as hello main video is playing, usually a logo or other static image placed within hello player.</span></span>
* <span data-ttu-id="4cbf2-113">**Pomocnik** — reklam wyświetlanych poza hello player.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-113">**Companion** – ads that are displayed outside of hello player.</span></span>

<span data-ttu-id="4cbf2-114">Usługa AD można umieścić w dowolnym momencie hello wideo głównych osi czasu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-114">Ads can be placed at any point in hello main video’s time line.</span></span> <span data-ttu-id="4cbf2-115">Gdy tooplay hello ad, które należy wskazać hello player tooplay reklam.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-115">You must tell hello player when tooplay hello ad and which ads tooplay.</span></span> <span data-ttu-id="4cbf2-116">Jest to realizowane przy użyciu zestawu standardowych plików opartych na języku XML: wideo Ad Service szablonu (VAST), cyfrowy wideo wielu Ad listy odtwarzania (VMAP) nośnika abstrakcyjny sekwencjonowania szablonu (MASZTÓW) i cyfrowy wideo Player Ad interfejsu definicji (VPAID).</span><span class="sxs-lookup"><span data-stu-id="4cbf2-116">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="4cbf2-117">Pliki PRZEWAŻAJĄCA określają, jakie toodisplay reklam.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-117">VAST files specify what ads toodisplay.</span></span> <span data-ttu-id="4cbf2-118">Pliki VMAP Określ, kiedy tooplay różnych reklam i zawierać PRZEWAŻAJĄCA XML.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-118">VMAP files specify when tooplay various ads and contain VAST XML.</span></span> <span data-ttu-id="4cbf2-119">Pliki MASZTÓW są inny sposób toosequence reklam, które również mogą zawierać PRZEWAŻAJĄCA XML.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-119">MAST files are another way toosequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="4cbf2-120">Pliki VPAID zdefiniuj interfejs między hello odtwarzacza wideo i hello ad lub serwera usługi ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-120">VPAID files define an interface between hello video player and hello ad or ad server.</span></span>

<span data-ttu-id="4cbf2-121">Każdy framework player zmieniło i wszystkie będą opisane w temacie własny.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-121">Each player framework works differently and each will be covered in its own topic.</span></span> <span data-ttu-id="4cbf2-122">W tym temacie opisano hello podstawowe mechanizmy używane tooinsert reklam. Aplikacji odtwarzacza wideo żądania reklam z serwera ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-122">This topic will describe hello basic mechanisms used tooinsert ads.Video player applications request ads from an ad server.</span></span> <span data-ttu-id="4cbf2-123">Serwer ad Hello może odpowiadać na kilka sposobów:</span><span class="sxs-lookup"><span data-stu-id="4cbf2-123">hello ad server can respond in a number of ways:</span></span>

* <span data-ttu-id="4cbf2-124">Zwraca PRZEWAŻAJĄCA plik</span><span class="sxs-lookup"><span data-stu-id="4cbf2-124">Return a VAST file</span></span>
* <span data-ttu-id="4cbf2-125">Zwraca plik VMAP (z osadzonych VAST)</span><span class="sxs-lookup"><span data-stu-id="4cbf2-125">Return a VMAP file (with embedded VAST)</span></span>
* <span data-ttu-id="4cbf2-126">Zwraca plik MASZTÓW (z osadzonych VAST)</span><span class="sxs-lookup"><span data-stu-id="4cbf2-126">Return a MAST file (with embedded VAST)</span></span>
* <span data-ttu-id="4cbf2-127">Zwraca PRZEWAŻAJĄCA plik z VPAID reklam</span><span class="sxs-lookup"><span data-stu-id="4cbf2-127">Return a VAST file with VPAID ads</span></span>

### <a name="using-a-video-ad-service-template-vast-file"></a><span data-ttu-id="4cbf2-128">Przy użyciu pliku szablonu (VAST) usługi Ad wideo</span><span class="sxs-lookup"><span data-stu-id="4cbf2-128">Using a Video Ad Service Template (VAST) File</span></span>
<span data-ttu-id="4cbf2-129">PRZEWAŻAJĄCA pliku Określa, jakie ad lub toodisplay reklam.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-129">A VAST file specifies what ad or ads toodisplay.</span></span> <span data-ttu-id="4cbf2-130">Hello następujący kod XML jest przykładowy plik PRZEWAŻAJĄCA liniowej AD:</span><span class="sxs-lookup"><span data-stu-id="4cbf2-130">hello following XML is an example of a VAST file for a linear ad:</span></span>

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

<span data-ttu-id="4cbf2-131">ad liniowej Hello jest opisany przez hello <**liniowy**> elementu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-131">hello linear ad is described by hello <**Linear**> element.</span></span> <span data-ttu-id="4cbf2-132">Określa czas trwania hello hello AD, śledzenia zdarzeń, kliknij go, kliknij przycisk śledzenia i liczbę **MediaFile** elementów.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-132">It specifies hello duration of hello ad, tracking events, click through, click tracking, and a number of **MediaFile** elements.</span></span> <span data-ttu-id="4cbf2-133">Zdarzenia śledzenia są określone w hello <**TrackingEvents**> element i umożliwić tootrack serwera ad różnych zdarzeń występujących podczas wyświetlania hello ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-133">Tracking events are specified within hello <**TrackingEvents**> element and allow an ad server tootrack various events that occur while viewing hello ad.</span></span> <span data-ttu-id="4cbf2-134">W takim przypadku hello start, punkt środkowy zakończeniu i rozwiń zdarzenia są śledzone.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-134">In this case hello start, midpoint, complete, and expand events are tracked.</span></span> <span data-ttu-id="4cbf2-135">zdarzenia uruchamiania Hello występuje, gdy hello ad jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-135">hello start event occurs when hello ad is displayed.</span></span> <span data-ttu-id="4cbf2-136">Witaj środkowego zdarzenie wystąpi, gdy co najmniej się, że wyświetlił 50% hello ad osi czasu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-136">hello midpoint event occurs when at least 50% of hello ad’s timeline has been viewed.</span></span> <span data-ttu-id="4cbf2-137">Zdarzenie ukończenia Hello występuje, gdy hello ad zostało uruchomione toohello zakończenia.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-137">hello complete event occurs when hello ad has run toohello end.</span></span> <span data-ttu-id="4cbf2-138">Hello rozwiń zdarzenie wystąpi, gdy użytkownik hello rozszerza hello odtwarzacza wideo toofull ekranu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-138">hello Expand event occurs when hello user expands hello video player toofull screen.</span></span> <span data-ttu-id="4cbf2-139">Clickthroughs są określane za pomocą <**przeglądowego**> w elemencie <**VideoClicks**> element i określa identyfikator URI tooa zasobów toodisplay po kliknięciu przez użytkownika hello na powitania ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-139">Clickthroughs are specified with a <**ClickThrough**> element within a <**VideoClicks**> element and specifies a URI tooa resource toodisplay when hello user clicks on hello ad.</span></span> <span data-ttu-id="4cbf2-140">ClickTracking jest określona w <**ClickTracking**> elementu również w ramach hello <**VideoClicks**> element i umożliwia określenie zasobu śledzenia toorequest player powitania po kliknięciu hello użytkownika na powitania ad.hello <**MediaFile**> elementy Określ informacje dotyczące określonego kodowania AD.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-140">ClickTracking is specified in a <**ClickTracking**> element, also within hello <**VideoClicks**> element and specifies a tracking resource for hello player toorequest when hello user clicks on hello ad.hello <**MediaFile**> elements specify information about a specific encoding of an ad.</span></span> <span data-ttu-id="4cbf2-141">Gdy istnieje więcej niż jeden <**MediaFile**> elementu odtwarzacza wideo hello można wybrać hello optymalne kodowanie hello platformy.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-141">When there is more than one <**MediaFile**> element, hello video player can choose hello best encoding for hello platform.</span></span> 

<span data-ttu-id="4cbf2-142">Liniowy reklam mogą być wyświetlane w określonej kolejności.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-142">Linear ads can be displayed in a specified order.</span></span> <span data-ttu-id="4cbf2-143">toodo, dodanie dodatkowych <Ad> toohello elementy VAST pliku i określić kolejność hello przy użyciu atrybutu sekwencji hello.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-143">toodo this, add additional <Ad> elements toohello VAST file and specify hello order using hello sequence attribute.</span></span> <span data-ttu-id="4cbf2-144">Witaj poniższy przykład przedstawia to:</span><span class="sxs-lookup"><span data-stu-id="4cbf2-144">hello following example illustrates this:</span></span>

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

<span data-ttu-id="4cbf2-145">Rożne reklam są określone w <Creative> również element.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-145">Nonlinear ads are specified in a <Creative> element as well.</span></span> <span data-ttu-id="4cbf2-146">powitania po przykładzie <Creative> element, który opisuje rożne ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-146">hello following example shows a <Creative> element that describes a nonlinear ad.</span></span>

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


<span data-ttu-id="4cbf2-147">Witaj <**NonLinearAds**> element może zawierać co najmniej jeden <**NonLinear**> elementy, które opisują rożne ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-147">hello <**NonLinearAds**> element can contain one or more <**NonLinear**> elements, each of which can describe a nonlinear ad.</span></span> <span data-ttu-id="4cbf2-148">Witaj <**NonLinear**> element określa zasobów hello hello rożne AD.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-148">hello <**NonLinear**> element specifies hello resource for hello nonlinear ad.</span></span> <span data-ttu-id="4cbf2-149">Witaj zasób może być <**StaticResouce**>, <**IFrameResource**>, lub <**HTMLResouce**>.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-149">hello resource can be a <**StaticResouce**>, an <**IFrameResource**>, or an <**HTMLResouce**>.</span></span><span data-ttu-id="4cbf2-150"> <**StaticResource**> opisuje zasób w innym języku niż HTML i definiuje atrybut creativeType, który określa sposób wyświetlania zasobów hello:</span><span class="sxs-lookup"><span data-stu-id="4cbf2-150"> <**StaticResource**> describes a non-HTML resource and defines a creativeType attribute that specifies how hello resource is displayed:</span></span>

<span data-ttu-id="4cbf2-151">Obraz/gif, image/jpeg, obrazu/png — hello zasobów jest wyświetlana w formacie HTML <**img**> tagu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-151">Image/gif, image/jpeg, image/png – hello resource is displayed in an HTML <**img**> tag.</span></span>

<span data-ttu-id="4cbf2-152">Application/x-javascript — hello zasobów jest wyświetlana w formacie HTML <**skryptu**> tagu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-152">Application/x-javascript – hello resource is displayed in an HTML <**script**> tag.</span></span>

<span data-ttu-id="4cbf2-153">Application/x-shockwave-flash — hello zasobów jest wyświetlana w Flash player.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-153">Application/x-shockwave-flash – hello resource is displayed in a Flash player.</span></span>

<span data-ttu-id="4cbf2-154">**IFrameResource** opisuje zasobu HTML, który może być wyświetlany w elementu IFrame.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-154">**IFrameResource** describes an HTML resource that can be displayed in an IFrame.</span></span> <span data-ttu-id="4cbf2-155">**HTMLResource** opisuje fragment kodu HTML, który można wstawiać do strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-155">**HTMLResource** describes a piece of HTML code that can be inserted into a web page.</span></span> <span data-ttu-id="4cbf2-156">**TrackingEvents** określić zdarzenia śledzenia i hello toorequest identyfikatora URI, gdy wystąpi zdarzenie hello.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-156">**TrackingEvents** specify tracking events and hello URI toorequest when hello event occurs.</span></span> <span data-ttu-id="4cbf2-157">W tej próbki hello acceptInvitation i zwijanie zdarzenia są śledzone.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-157">In this sample hello acceptInvitation and collapse events are tracked.</span></span> <span data-ttu-id="4cbf2-158">Aby uzyskać więcej informacji na temat hello **NonLinearAds** elementu i jego elementów podrzędnych, zobacz IAB.NET/VAST.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-158">For more information on hello **NonLinearAds** element and its children, see IAB.NET/VAST.</span></span> <span data-ttu-id="4cbf2-159">Należy pamiętać, że hello **TrackingEvents** element znajduje się w obrębie hello **NonLinearAds** elementu zamiast hello **NonLinear** elementu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-159">Note that hello **TrackingEvents** element is located within hello **NonLinearAds** element rather than hello **NonLinear** element.</span></span>

<span data-ttu-id="4cbf2-160">Pomocnik reklam są zdefiniowane w <CompanionAds> elementu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-160">Companion ads are defined within a <CompanionAds> element.</span></span> <span data-ttu-id="4cbf2-161">Witaj <CompanionAds> element może zawierać jeden lub więcej <Companion> elementów.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-161">hello <CompanionAds> element can contain one or more <Companion> elements.</span></span> <span data-ttu-id="4cbf2-162">Każdy <Companion> elementu opisuje ad pomocnika i może zawierać <StaticResource>, <IFrameResource>, lub <HTMLResource> ujętych w hello sam sposób jak w rożne ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-162">Each <Companion> element describes a companion ad and can contain a <StaticResource>, <IFrameResource>, or <HTMLResource> which are specified in hello same way as in a nonlinear ad.</span></span> <span data-ttu-id="4cbf2-163">PRZEWAŻAJĄCA plik może zawierać wiele pomocnika reklam i aplikacja odtwarzacza hello można wybrać najodpowiedniejszy toodisplay ad hello.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-163">A VAST file can contain multiple companion ads and hello player application can choose hello most appropriate ad toodisplay.</span></span> <span data-ttu-id="4cbf2-164">Aby uzyskać więcej informacji o VAST, zobacz [3.0 PRZEWAŻAJĄCA](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="4cbf2-164">For more information about VAST, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span>

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a><span data-ttu-id="4cbf2-165">Przy użyciu wielu pliku listy odtwarzania (VMAP) Ad cyfrowy wideo</span><span class="sxs-lookup"><span data-stu-id="4cbf2-165">Using a Digital Video Multiple Ad Playlist (VMAP) File</span></span>
<span data-ttu-id="4cbf2-166">Plik VMAP pozwala toospecify wystąpieniu podziały ad, jak długo trwa każdego podziału ile reklam mogą być wyświetlane w ramach podziału i jakie typy reklam mogą być wyświetlane podczas podziału.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-166">A VMAP file allows you toospecify when ad breaks occur, how long each break is, how many ads can be displayed within a break, and what types of ads may be displayed during a break.</span></span> <span data-ttu-id="4cbf2-167">powitania po w przykładowy plik VMAP, który definiuje podział pojedynczego ad:</span><span class="sxs-lookup"><span data-stu-id="4cbf2-167">hello following in an example VMAP file that defines a single ad break:</span></span>

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

<span data-ttu-id="4cbf2-168">Rozpoczyna się od pliku VMAP <VMAP> element, który zawiera co najmniej jeden <AdBreak> elementy Definiowanie podziału ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-168">A VMAP file begins with a <VMAP> element that contains one or more <AdBreak> elements, each defining an ad break.</span></span> <span data-ttu-id="4cbf2-169">Każdy podziału ad Określa typ podziału, identyfikator podziału i przesunięcie czasu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-169">Each ad break specifies a break type, break ID, and time offset.</span></span> <span data-ttu-id="4cbf2-170">Atrybut breakType Hello Określa typ hello AD, która może być odtwarzany podczas podziału hello: liniowych, rożne, lub wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-170">hello breakType attribute specifies hello type of ad that can be played during hello break: linear, nonlinear, or display.</span></span> <span data-ttu-id="4cbf2-171">Wyświetlania reklam mapy tooVAST pomocnika reklam.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-171">Display ads map tooVAST companion ads.</span></span> <span data-ttu-id="4cbf2-172">Można określić więcej niż jeden typ ad w postaci listy rozdzielanej przecinkami (bez spacji).</span><span class="sxs-lookup"><span data-stu-id="4cbf2-172">More than one ad type can be specified in a comma (no spaces) separated list.</span></span> <span data-ttu-id="4cbf2-173">Hello breakID jest opcjonalny identyfikator hello ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-173">hello breakID is an optional identifier for hello ad.</span></span> <span data-ttu-id="4cbf2-174">Hello timeOffset Określa, kiedy powinny być wyświetlane hello ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-174">hello timeOffset specifies when hello ad should be displayed.</span></span> <span data-ttu-id="4cbf2-175">Można ją określić w jednym z hello następujące sposoby:</span><span class="sxs-lookup"><span data-stu-id="4cbf2-175">It can be specified in one of hello following ways:</span></span>

1. <span data-ttu-id="4cbf2-176">Godzina w formacie hh: mm: lub GG:mm:ss.mmm .mmm w przypadku milisekund.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-176">Time – in hh:mm:ss or hh:mm:ss.mmm format where .mmm is milliseconds.</span></span> <span data-ttu-id="4cbf2-177">wartość tego atrybutu Hello określa czas hello od początku hello hello wideo osi czasu rozpoczęcia toohello hello ad podziału.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-177">hello value of this attribute specifies hello time from hello beginning of hello video timeline toohello beginning of hello ad break.</span></span>
2. <span data-ttu-id="4cbf2-178">Procent — w formacie n %, gdzie n to hello odsetek hello tooplay wideo osi czasu przed odtwarzanie hello ad</span><span class="sxs-lookup"><span data-stu-id="4cbf2-178">Percentage – in n% format where n is hello percentage of hello video timeline tooplay before playing hello ad</span></span>
3. <span data-ttu-id="4cbf2-179">Rozpoczęcie i zakończenie — Określa, że usługi ad powinna być wyświetlana przed lub po hello wideo został wyświetlony</span><span class="sxs-lookup"><span data-stu-id="4cbf2-179">Start/End – specifies that an ad should be displayed before or after hello video has been displayed</span></span>
4. <span data-ttu-id="4cbf2-180">Umieść — określa kolejność hello podziałów ad, gdy czas hello podziały ad hello jest nieznany, takie jak transmisja strumieniowa na żywo.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-180">Position – specifies hello order of ad breaks when hello timing of hello ad breaks is unknown, such as in live streaming.</span></span> <span data-ttu-id="4cbf2-181">kolejność Hello każdego podziału ad jest określana w formacie hello #n, gdzie n to liczba całkowita mniejsza od 1.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-181">hello order of each ad break is specified in hello #n format where n is an integer 1 or greater.</span></span> <span data-ttu-id="4cbf2-182">1 oznacza, że powinien zostać odtworzone hello ad przy okazji pierwszego hello, 2 oznacza hello ad powinna zostać odtworzone przy okazji drugi hello i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-182">1 signifies hello ad should be played at hello first opportunity, 2 signifies hello ad should be played at hello second opportunity and so on.</span></span>

<span data-ttu-id="4cbf2-183">W ramach hello <**AdBreak**> element może być jedną <**AdSource**> elementu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-183">Within hello <**AdBreak**> element there can be one <**AdSource**> element.</span></span> <span data-ttu-id="4cbf2-184">Witaj <**AdSource**> element zawiera hello następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="4cbf2-184">hello <**AdSource**> element contains hello following attributes:</span></span>

1. <span data-ttu-id="4cbf2-185">Identyfikator — Określa identyfikator źródła ad hello</span><span class="sxs-lookup"><span data-stu-id="4cbf2-185">Id – specifies an identifier for hello ad source</span></span>
2. <span data-ttu-id="4cbf2-186">allowMultipleAds — wartość logiczna określająca, czy wiele reklam mogą być wyświetlane podczas hello ad podziału</span><span class="sxs-lookup"><span data-stu-id="4cbf2-186">allowMultipleAds – a Boolean value that specifies whether multiple ads can be displayed during hello ad break</span></span>
3. <span data-ttu-id="4cbf2-187">followRedirects — opcjonalna wartość logiczna określająca, czy hello odtwarzacza wideo należy przestrzegać przekierowuje w odpowiedzi usługi ad</span><span class="sxs-lookup"><span data-stu-id="4cbf2-187">followRedirects – an optional Boolean value that specifies if hello video player should honor redirects within an ad response</span></span>

<span data-ttu-id="4cbf2-188">Witaj <**AdSource**> element udostępnia odtwarzacz hello odpowiedzi ad wbudowanego lub odpowiedź ad tooan odwołania.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-188">hello <**AdSource**> element provides hello player an inline ad response or a reference tooan ad response.</span></span> <span data-ttu-id="4cbf2-189">Nazwa może zawierać jeden hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4cbf2-189">It can contain one of hello following elements:</span></span>

* <span data-ttu-id="4cbf2-190"><VASTAdData>Wskazuje, że odpowiedź PRZEWAŻAJĄCA ad jest osadzony w pliku VMAP hello</span><span class="sxs-lookup"><span data-stu-id="4cbf2-190"><VASTAdData> indicates a VAST ad response is embedded within hello VMAP file</span></span>
* <span data-ttu-id="4cbf2-191"><AdTagURI>Identyfikator URI, który odwołuje się do odpowiedzi ad z innego systemu</span><span class="sxs-lookup"><span data-stu-id="4cbf2-191"><AdTagURI> a URI that references an ad response from another system</span></span>
* <span data-ttu-id="4cbf2-192"><CustomAdData>-dowolnego ciągu tego respresents-PRZEWAŻAJĄCA odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="4cbf2-192"><CustomAdData> -an arbitrary string that respresents a non-VAST response</span></span>

<span data-ttu-id="4cbf2-193">W tym przykładzie odpowiedzi w wierszu ad zostanie określony z <VASTAdData> element, który zawiera odpowiedzi PRZEWAŻAJĄCA ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-193">In this example an in-line ad response is specified with a <VASTAdData> element that contains a VAST ad response.</span></span> <span data-ttu-id="4cbf2-194">Aby uzyskać więcej informacji na temat hello innych elementów zobacz [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span><span class="sxs-lookup"><span data-stu-id="4cbf2-194">For more information about hello other elements, see [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span></span>

<span data-ttu-id="4cbf2-195">Witaj <**AdBreak**> element może również zawierać jedną <**TrackingEvents**> elementu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-195">hello <**AdBreak**> element can also contain one <**TrackingEvents**> element.</span></span> <span data-ttu-id="4cbf2-196">Witaj <**TrackingEvents**> element pozwala tootrack hello początek lub koniec podziału ad lub czy wystąpił błąd podczas hello ad podziału.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-196">hello <**TrackingEvents**> element allows you tootrack hello start or end of an ad break or whether an error occurred during hello ad break.</span></span> <span data-ttu-id="4cbf2-197">Witaj <**TrackingEvents**> elementu zawiera jeden lub więcej <**śledzenia**> elementów, z których każdy określa zdarzenia śledzenia i śledzenia identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-197">hello <**TrackingEvents**> element contains one or more <**Tracking**> elements, each of which specifies a tracking event and a tracking URI.</span></span> <span data-ttu-id="4cbf2-198">zdarzenia śledzenia możliwe Hello są:</span><span class="sxs-lookup"><span data-stu-id="4cbf2-198">hello possible tracking events are:</span></span>

1. <span data-ttu-id="4cbf2-199">breakStart — śledzi hello początku podziału ad</span><span class="sxs-lookup"><span data-stu-id="4cbf2-199">breakStart – tracks hello beginning of an ad break</span></span>
2. <span data-ttu-id="4cbf2-200">breakEnd — Śledź hello zakończenia podziału ad</span><span class="sxs-lookup"><span data-stu-id="4cbf2-200">breakEnd – track hello completion of an ad break</span></span>
3. <span data-ttu-id="4cbf2-201">Błąd — śledzi wystąpił błąd, który wystąpił podczas hello ad podziału</span><span class="sxs-lookup"><span data-stu-id="4cbf2-201">error – tracks an error that occurred during hello ad break</span></span>

<span data-ttu-id="4cbf2-202">Hello poniższy przykład przedstawia plik VMAP, który określa zdarzenia śledzenia</span><span class="sxs-lookup"><span data-stu-id="4cbf2-202">hello following example shows a VMAP file that specifies tracking events</span></span>

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

<span data-ttu-id="4cbf2-203">Aby uzyskać więcej informacji na temat hello <**TrackingEvents**> elementu i jego elementów podrzędnych, zobacz http://iab.org/VMAP.pdf</span><span class="sxs-lookup"><span data-stu-id="4cbf2-203">For more information on hello <**TrackingEvents**> element and its children, see http://iab.org/VMAP.pdf</span></span>

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a><span data-ttu-id="4cbf2-204">Przy użyciu abstrakcyjny nośnika, sekwencjonowania pliku szablonu (MASZTÓW)</span><span class="sxs-lookup"><span data-stu-id="4cbf2-204">Using a Media Abstract Sequencing Template (MAST) File</span></span>
<span data-ttu-id="4cbf2-205">Plik MASZTÓW umożliwia toospecify wyzwalaczy, które określają, kiedy jest wyświetlany przy użyciu usług ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-205">A MAST file allows you toospecify triggers that define when an ad is displayed.</span></span> <span data-ttu-id="4cbf2-206">Witaj poniżej znajduje się przykładowy plik MASZTÓW, który zawiera wyzwalacze ad zbiorczego sprzed, ad zbiorczego pośredniej i ad po zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-206">hello following is an example MAST file that contains triggers for a pre roll ad, a mid-roll ad, and a post-roll ad.</span></span>

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



<span data-ttu-id="4cbf2-207">Rozpoczyna się od pliku MASZTÓW **MASZTÓW** element, który zawiera jeden **wyzwalaczy** elementu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-207">A MAST file begins with a **MAST** element that contains one **triggers** element.</span></span> <span data-ttu-id="4cbf2-208">Witaj <triggers> elementu zawiera jeden lub więcej **wyzwalacza** elementów, które określają, kiedy można odtwarzać przy użyciu usług ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-208">hello <triggers> element contains one or more **trigger** elements that define when an ad should be played.</span></span> 

<span data-ttu-id="4cbf2-209">Witaj **wyzwalacza** element zawiera **startConditions** elementu, którego Określ rozpoczęcia tooplay ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-209">hello **trigger** element contains a **startConditions** element which specify when an ad should begin tooplay.</span></span> <span data-ttu-id="4cbf2-210">Witaj **startConditions** elementu zawiera jeden lub więcej <condition> elementów.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-210">hello **startConditions** element contains one or more <condition> elements.</span></span> <span data-ttu-id="4cbf2-211">Podczas każdego <condition> ocenia tootrue wyzwalacza jest inicjowane lub odwołane, w zależności od czy hello <condition> jest zawarty w **startConditions** lub **endConditions** — element odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-211">When each <condition> evaluates tootrue a trigger is initiated or revoked depending upon whether hello <condition> is contained within a **startConditions** or **endConditions** element respectively.</span></span> <span data-ttu-id="4cbf2-212">Gdy wiele <condition> elementy znajdują się, są traktowane jako niejawne OR, wszelkie warunku obliczania tootrue spowoduje, że tooinitiate wyzwalacza hello.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-212">When multiple <condition> elements are present, they are treated as an implicit OR, any condition evaluating tootrue will cause hello trigger tooinitiate.</span></span> <span data-ttu-id="4cbf2-213"><condition>elementy mogą być zagnieżdżone.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-213"><condition> elements can be nested.</span></span> <span data-ttu-id="4cbf2-214">Gdy podrzędny <condition> elementy są zdefiniowane, są traktowane jak i niejawne, wszystkie warunki musi ocenić tootrue dla hello tooinitiate wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-214">When child <condition> elements are preset, they are treated as an implicit AND, all conditions must evaluate tootrue for hello trigger tooinitiate.</span></span> <span data-ttu-id="4cbf2-215">Witaj <condition> element zawiera następujące atrybuty definiujące warunek hello hello:</span><span class="sxs-lookup"><span data-stu-id="4cbf2-215">hello <condition> element contains hello following attributes that define hello condition:</span></span> 

1. <span data-ttu-id="4cbf2-216">**Typ** — Określa typ hello zdarzenia lub warunku właściwości</span><span class="sxs-lookup"><span data-stu-id="4cbf2-216">**type** – specifies hello type of condition, event or property</span></span>
2. <span data-ttu-id="4cbf2-217">**Nazwa** — Witaj nazwa hello właściwości lub zdarzenia toobe używany podczas obliczania</span><span class="sxs-lookup"><span data-stu-id="4cbf2-217">**name** – hello name of hello property or event toobe used during evaluation</span></span>
3. <span data-ttu-id="4cbf2-218">**wartość** — Witaj wartość, która będzie porównywany właściwości</span><span class="sxs-lookup"><span data-stu-id="4cbf2-218">**value** – hello value that a property will be evaluated against</span></span>
4. <span data-ttu-id="4cbf2-219">**operator** — Witaj toouse operacji podczas obliczania: EQ (równości), NEQ (różne), GTR (większe), GEQ (większe lub równe), LT (poniżej), LEQ (mniejsze niż lub równe), MOD (modulo)</span><span class="sxs-lookup"><span data-stu-id="4cbf2-219">**operator** – hello operation toouse during evaluation: EQ (equal), NEQ (not equal), GTR (greater), GEQ (greater or equal), LT (Less than), LEQ (less than or equal), MOD (modulo)</span></span>

<span data-ttu-id="4cbf2-220">**endConditions** również zawierać <condition> elementów.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-220">**endConditions** also contain <condition> elements.</span></span> <span data-ttu-id="4cbf2-221">Jeśli wynikiem warunku jest tootrue hello wyzwalacza jest reset.hello <trigger> zawiera również element <sources> element, który zawiera co najmniej jeden <source> elementów.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-221">When a condition evaluates tootrue hello trigger is reset.hello <trigger> element also contains a <sources> element that contains one or more <source> elements.</span></span> <span data-ttu-id="4cbf2-222">Witaj <source> elementy zdefiniuj hello URI toohello ad odpowiedzi i typ hello ad odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-222">hello <source> elements define hello URI toohello ad response and hello type of ad response.</span></span> <span data-ttu-id="4cbf2-223">W tym przykładzie identyfikatora URI otrzymuje tooa PRZEWAŻAJĄCA odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-223">In this example a URI is given tooa VAST response.</span></span> 

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


### <a name="using-video-player-ad-interface-definition-vpaid"></a><span data-ttu-id="4cbf2-224">Przy użyciu odtwarzacza wideo-Ad definicji interfejsu (VPAID)</span><span class="sxs-lookup"><span data-stu-id="4cbf2-224">Using Video Player-Ad Interface Definition (VPAID)</span></span>
<span data-ttu-id="4cbf2-225">VPAID to interfejs API umożliwiający toocommunicate jednostki ad pliku wykonywalnego z odtwarzacza wideo.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-225">VPAID is an API for enabling executable ad units toocommunicate with a video player.</span></span> <span data-ttu-id="4cbf2-226">Dzięki temu ad wysokiej interaktywnego środowiska.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-226">This allows highly interactive ad experiences.</span></span> <span data-ttu-id="4cbf2-227">Hello użytkownik może interakcyjnie hello ad i hello ad mogą odpowiadać tooactions wykonywaną przez hello podglądu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-227">hello user can interact with hello ad and hello ad can respond tooactions taken by hello viewer.</span></span> <span data-ttu-id="4cbf2-228">Na przykład ad mogą być wyświetlane przyciski umożliwiające tooview użytkownika hello więcej informacji lub dłużej wersji hello ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-228">For example an ad may display buttons that allow hello user tooview more information or a longer version of hello ad.</span></span> <span data-ttu-id="4cbf2-229">odtwarzacza wideo Hello musi obsługiwać hello VPAID interfejsu API i hello ad pliku wykonywalnego musi implementować interfejs API hello.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-229">hello video player must support hello VPAID API and hello executable ad must implement hello API.</span></span> <span data-ttu-id="4cbf2-230">Gdy odtwarzacza zażąda ad z powitania serwera ad mogą odpowiadać za pomocą PRZEWAŻAJĄCA odpowiedzi, który zawiera VPAID ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-230">When a player requests an ad from an ad server hello server may respond with a VAST response that contains a VPAID ad.</span></span>

<span data-ttu-id="4cbf2-231">Wykonywalny ad jest tworzony w kodu, który musi zostać wykonana w środowisko uruchomieniowe, takie jak Adobe Flash™ lub JavaScript, które mogą być wykonywane w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-231">An executable ad is created in code that must be executed in a runtime environment such as Adobe Flash™ or JavaScript that can be executed in a web browser.</span></span> <span data-ttu-id="4cbf2-232">Po powrocie z serwera ad PRZEWAŻAJĄCA odpowiedzi zawierające VPAID ad hello wartość atrybutu apiFramework hello w hello <MediaFile> element musi być "VPAID".</span><span class="sxs-lookup"><span data-stu-id="4cbf2-232">When an ad server returns a VAST response containing a VPAID ad, hello value of hello apiFramework attribute in hello <MediaFile> element must be “VPAID”.</span></span> <span data-ttu-id="4cbf2-233">Ten atrybut określa danej reklamy hello zawarty jest VPAID ad pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-233">This attribute specifies that hello contained ad is a VPAID executable ad.</span></span> <span data-ttu-id="4cbf2-234">Atrybut typu Hello musi być ustawiona toohello typ MIME hello pliku wykonywalnego, takie jak "application/x-shockwave-flash" lub "application/x-javascript".</span><span class="sxs-lookup"><span data-stu-id="4cbf2-234">hello type attribute must be set toohello MIME type of hello executable, such as “application/x-shockwave-flash” or “application/x-javascript”.</span></span> <span data-ttu-id="4cbf2-235">Witaj następujący fragment kodu XML zawiera hello <MediaFile> element na podstawie PRZEWAŻAJĄCA odpowiedzi zawierające VPAID ad pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-235">hello following XML snippet shows hello <MediaFile> element from a VAST response containing a VPAID executable ad.</span></span> 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


<span data-ttu-id="4cbf2-236">Można zainicjować pliku wykonywalnego ad przy użyciu hello <AdParameters> elementu w obrębie hello <Linear> lub <NonLinear> elementów w PRZEWAŻAJĄCA odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-236">An executable ad can be initialized using hello <AdParameters> element within hello <Linear> or <NonLinear> elements in a VAST response.</span></span> <span data-ttu-id="4cbf2-237">Aby uzyskać więcej informacji na temat hello <AdParameters> elementu, zobacz [3.0 PRZEWAŻAJĄCA](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="4cbf2-237">For more information on hello <AdParameters> element, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span> <span data-ttu-id="4cbf2-238">Aby uzyskać więcej informacji na temat hello VPAID interfejsu API, zobacz [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span><span class="sxs-lookup"><span data-stu-id="4cbf2-238">For more information about hello VPAID API, see [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span></span>

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a><span data-ttu-id="4cbf2-239">Wdrażanie systemu Windows lub Windows Phone 8 Player z obsługą usługi Ad</span><span class="sxs-lookup"><span data-stu-id="4cbf2-239">Implementing a Windows or Windows Phone 8 Player with Ad Support</span></span>
<span data-ttu-id="4cbf2-240">Witaj platformy Media firmy Microsoft: Framework Player dla systemu Windows 8 i Windows Phone 8 zawiera kolekcję przykładowe aplikacje, które pokazują, jak tooimplement aplikacji odtwarzacza wideo przy użyciu hello framework.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-240">hello Microsoft Media Platform: Player Framework for Windows 8 and Windows Phone 8 contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="4cbf2-241">Możesz pobrać hello Player Framework i hello przykłady z [Framework Player dla systemu Windows 8 i Windows Phone 8](https://playerframework.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="4cbf2-241">You can download hello Player Framework and hello samples from [Player Framework for Windows 8 and Windows Phone 8](https://playerframework.codeplex.com).</span></span>

<span data-ttu-id="4cbf2-242">Po otwarciu rozwiązania Microsoft.PlayerFramework.Xaml.Samples hello pojawi się liczba folderów w ramach hello projektu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-242">When you open hello Microsoft.PlayerFramework.Xaml.Samples solution you will see a number of folders within hello project.</span></span> <span data-ttu-id="4cbf2-243">folder reklamy Hello zawiera hello przykładowy kod odpowiednich toocreating odtwarzacza wideo z obsługą usługi ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-243">hello Advertising folder contains hello sample code relevant toocreating a video player with ad support.</span></span> <span data-ttu-id="4cbf2-244">Folder reklamy hello wewnątrz jest liczba XAML/cs plików każdy program jak tooinsert reklam w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-244">Inside hello Advertising folder is a number of XAML/cs files each of which show how tooinsert ads in a different way.</span></span> <span data-ttu-id="4cbf2-245">następujące listy Hello opisano poszczególne:</span><span class="sxs-lookup"><span data-stu-id="4cbf2-245">hello following list describes each:</span></span>

* <span data-ttu-id="4cbf2-246">AdPodPage.xaml pokazuje sposób pod toodisplay ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-246">AdPodPage.xaml Shows how toodisplay an ad pod.</span></span>
* <span data-ttu-id="4cbf2-247">Pokazuje AdSchedulingPage.xaml jak tooschedule reklam.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-247">AdSchedulingPage.xaml Shows how tooschedule ads.</span></span>
* <span data-ttu-id="4cbf2-248">FreeWheelPage.xaml pokazuje, jak toouse hello FreeWheel wtyczki tooschedule reklam.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-248">FreeWheelPage.xaml Shows how toouse hello FreeWheel plugin tooschedule ads.</span></span>
* <span data-ttu-id="4cbf2-249">Pokazuje MastPage.xaml jak tooschedule reklam z plikiem MASZTÓW.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-249">MastPage.xaml Shows how tooschedule ads with a MAST file.</span></span>
* <span data-ttu-id="4cbf2-250">ProgrammaticAdPage.xaml pokazuje, jak zaplanować reklam tooprogrammatically do klipu wideo.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-250">ProgrammaticAdPage.xaml Shows how tooprogrammatically schedule ads into a video.</span></span>
* <span data-ttu-id="4cbf2-251">Pokazuje ScheduleClipPage.xaml jak tooschedule ad bez PRZEWAŻAJĄCA pliku.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-251">ScheduleClipPage.xaml Shows how tooschedule an ad without a VAST file.</span></span>
* <span data-ttu-id="4cbf2-252">Pokazuje VastLinearCompanionPage.xaml jak tooinsert liniowej i ad pomocnika.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-252">VastLinearCompanionPage.xaml Shows how tooinsert a linear and companion ad.</span></span>
* <span data-ttu-id="4cbf2-253">Pokazuje VastNonLinearPage.xaml jak tooinsert ad liniowej.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-253">VastNonLinearPage.xaml Shows how tooinsert a non-linear ad.</span></span>
* <span data-ttu-id="4cbf2-254">Pokazuje VmapPage.xaml jak toospecify reklam z plikiem VMAP.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-254">VmapPage.xaml Shows how toospecify ads with a VMAP file.</span></span>

<span data-ttu-id="4cbf2-255">Każda z tych próbek używa klasy MediaPlayer hello zdefiniowane przez platformę player hello.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-255">Each of these samples uses hello MediaPlayer class defined by hello player framework.</span></span> <span data-ttu-id="4cbf2-256">Większość przykładów za pomocą wtyczki obsługę różnych formatach odpowiedzi ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-256">Most samples use plugins that add support for various ad response formats.</span></span> <span data-ttu-id="4cbf2-257">Przykładowe ProgrammaticAdPage Hello programowo współdziała z wystąpienia elementu MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-257">hello ProgrammaticAdPage sample programmatically interacts with a MediaPlayer instance.</span></span>

### <a name="adpodpage-sample"></a><span data-ttu-id="4cbf2-258">Przykładowe AdPodPage</span><span class="sxs-lookup"><span data-stu-id="4cbf2-258">AdPodPage Sample</span></span>
<span data-ttu-id="4cbf2-259">W przykładzie użyto toodefine AdSchedulerPlugin powitania po toodisplay ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-259">This sample uses hello AdSchedulerPlugin toodefine when toodisplay an ad.</span></span> <span data-ttu-id="4cbf2-260">W tym przykładzie anonsu pośredniej zbiorczego jest zaplanowane toobe odtworzony po 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-260">In this example a mid-roll advertisement is scheduled toobe played after 5 seconds.</span></span> <span data-ttu-id="4cbf2-261">Witaj ad pod (grupa toodisplay reklam w kolejności) jest określone w pliku PRZEWAŻAJĄCA zwrócony z serwera usługi ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-261">hello ad pod (a group of ads toodisplay in order) is specified in a VAST file returned from an ad server.</span></span> <span data-ttu-id="4cbf2-262">Plik PRZEWAŻAJĄCA toohello URI Hello jest określona w hello <RemoteAdSource> elementu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-262">hello URI toohello VAST file is specified in hello <RemoteAdSource> element.</span></span>

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

<span data-ttu-id="4cbf2-263">Aby uzyskać więcej informacji na temat hello AdSchedulerPlugin, zobacz [reklamy w hello Framework Player w systemie Windows 8 i Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span><span class="sxs-lookup"><span data-stu-id="4cbf2-263">For more information about hello AdSchedulerPlugin, see [Advertising in hello Player Framework on Windows 8 and Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span></span>

### <a name="adschedulingpage"></a><span data-ttu-id="4cbf2-264">AdSchedulingPage</span><span class="sxs-lookup"><span data-stu-id="4cbf2-264">AdSchedulingPage</span></span>
<span data-ttu-id="4cbf2-265">W tym przykładzie użyto także hello AdSchedulerPlugin.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-265">This sample also uses hello AdSchedulerPlugin.</span></span> <span data-ttu-id="4cbf2-266">Planowana trzy reklam, ad wstępne zbiorczego ad zbiorczego pośredniej i ad po zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-266">It schedules three ads, a pre-roll ad, a mid-roll ad, and a post-roll ad.</span></span> <span data-ttu-id="4cbf2-267">Witaj URI toohello VAST dla każdej usługi ad jest określona w <RemoteAdSource> elementu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-267">hello URI toohello VAST for each ad is specified in a <RemoteAdSource> element.</span></span>

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


### <a name="freewheelpage"></a><span data-ttu-id="4cbf2-268">FreeWheelPage</span><span class="sxs-lookup"><span data-stu-id="4cbf2-268">FreeWheelPage</span></span>
<span data-ttu-id="4cbf2-269">W przykładzie użyto hello FreeWheelPlugin, która określa atrybut źródłowy, który określa identyfikator URI tego pliku SmartXML tooa punktów, które określa ad zawartości, a także informacje o harmonogramie ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-269">This sample uses hello FreeWheelPlugin which specifies a Source attribute that specifies a URI that points tooa SmartXML file that specifies ad content as well as ad scheduling information.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a><span data-ttu-id="4cbf2-270">MastPage</span><span class="sxs-lookup"><span data-stu-id="4cbf2-270">MastPage</span></span>
<span data-ttu-id="4cbf2-271">W przykładzie użyto hello MastSchedulerPlugin umożliwiający toouse MASZTÓW pliku.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-271">This sample uses hello MastSchedulerPlugin that allows you toouse a MAST file.</span></span> <span data-ttu-id="4cbf2-272">atrybut źródłowy Hello Określa lokalizację hello hello MASZTÓW pliku.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-272">hello Source attribute specifies hello location of hello MAST file.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a><span data-ttu-id="4cbf2-273">ProgrammaticAdPage</span><span class="sxs-lookup"><span data-stu-id="4cbf2-273">ProgrammaticAdPage</span></span>
<span data-ttu-id="4cbf2-274">W tym przykładzie programowo współdziała z hello MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-274">This sample programmatically interacts with hello MediaPlayer.</span></span> <span data-ttu-id="4cbf2-275">Plik ProgrammaticAdPage.xaml Hello tworzy hello MediaPlayer:</span><span class="sxs-lookup"><span data-stu-id="4cbf2-275">hello ProgrammaticAdPage.xaml file instantiates hello MediaPlayer:</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

<span data-ttu-id="4cbf2-276">Plik ProgrammaticAdPage.xaml.cs Hello tworzy AdHandlerPlugin, dodaje TimelineMarker toospecify, gdy usługi ad powinna być wyświetlana, a następnie dodanie obsługi dla zdarzenia MarkerReached hello, który ładuje RemoteAdSource określenie pliku PRZEWAŻAJĄCA tooa identyfikator URI, a następnie odgrywa Witaj ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-276">hello ProgrammaticAdPage.xaml.cs file creates an AdHandlerPlugin, adds a TimelineMarker toospecify when an ad should be displayed, and then adds a handler for hello MarkerReached event which loads a RemoteAdSource specifying a URI tooa VAST file, and then plays hello ad.</span></span>

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

### <a name="scheduleclippage"></a><span data-ttu-id="4cbf2-277">ScheduleClipPage</span><span class="sxs-lookup"><span data-stu-id="4cbf2-277">ScheduleClipPage</span></span>
<span data-ttu-id="4cbf2-278">W przykładzie użyto hello AdSchedulerPlugin tooschedule ad pośredniej zbiorczego, określając plik wmv, który zawiera hello ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-278">This sample uses hello AdSchedulerPlugin tooschedule a mid-roll ad by specifying a .wmv file that contains hello ad.</span></span>

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

### <a name="vastlinearcompanionpage"></a><span data-ttu-id="4cbf2-279">VastLinearCompanionPage</span><span class="sxs-lookup"><span data-stu-id="4cbf2-279">VastLinearCompanionPage</span></span>
<span data-ttu-id="4cbf2-280">W tym przykładzie pokazano, jak toouse hello AdSchedulerPlugin tooschedule pośredniej zbiorczego liniowej usługi ad z usługą Active Directory pomocnika.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-280">This sample illustrates how toouse hello AdSchedulerPlugin tooschedule a mid-roll linear ad with an companion ad.</span></span> <span data-ttu-id="4cbf2-281">Witaj <RemoteAdSource> element określa lokalizację hello hello PRZEWAŻAJĄCA pliku.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-281">hello <RemoteAdSource> element specifies hello location of hello VAST file.</span></span>

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

### <a name="vastlinearnonlinearpage"></a><span data-ttu-id="4cbf2-282">VastLinearNonLinearPage</span><span class="sxs-lookup"><span data-stu-id="4cbf2-282">VastLinearNonLinearPage</span></span>
<span data-ttu-id="4cbf2-283">W przykładzie użyto hello AdSchedulerPlugin tooschedule w układzie liniowych i inne usługi ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-283">This sample uses hello AdSchedulerPlugin tooschedule a linear and a non-linear ad.</span></span> <span data-ttu-id="4cbf2-284">Lokalizacja pliku PRZEWAŻAJĄCA Hello jest określany za pomocą hello <RemoteAdSource> elementu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-284">hello VAST file location is specified with hello <RemoteAdSource> element.</span></span>

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

### <a name="vmappage"></a><span data-ttu-id="4cbf2-285">VMAPPage</span><span class="sxs-lookup"><span data-stu-id="4cbf2-285">VMAPPage</span></span>
<span data-ttu-id="4cbf2-286">Reklam tooschedule VmapSchedulerPlugin hello przy użyciu pliku VMAP korzysta z tej próbki.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-286">This samples uses hello VmapSchedulerPlugin tooschedule ads using a VMAP file.</span></span> <span data-ttu-id="4cbf2-287">Hello URI toohello VMAP pliku jest określona w atrybut źródłowy hello hello <VmapSchedulerPlugin> elementu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-287">hello URI toohello VMAP file is specified in hello Source attribute of hello <VmapSchedulerPlugin> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a><span data-ttu-id="4cbf2-288">Implementacja systemu iOS odtwarzacza wideo z obsługą usługi Ad</span><span class="sxs-lookup"><span data-stu-id="4cbf2-288">Implementing an iOS Video Player with Ad Support</span></span>
<span data-ttu-id="4cbf2-289">Witaj platformy Media firmy Microsoft: Framework odtwarzacza dla systemu iOS zawiera kolekcję przykładowe aplikacje, które pokazują, jak tooimplement aplikacji odtwarzacza wideo przy użyciu hello framework.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-289">hello Microsoft Media Platform: Player Framework for iOS contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="4cbf2-290">Możesz pobrać hello Player Framework i hello przykłady z [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="4cbf2-290">You can download hello Player Framework and hello samples from [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span></span> <span data-ttu-id="4cbf2-291">Hello github strona ma tooa łącza typu Wiki, zawierający dodatkowe informacje dotyczące hello player framework i przykładowe player toohello wprowadzenie: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="4cbf2-291">hello github page has a link tooa Wiki that contains additional information on hello player framework and an introduction toohello player sample: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span></span>

### <a name="scheduling-ads-with-vmap"></a><span data-ttu-id="4cbf2-292">Planowanie reklam z VMAP</span><span class="sxs-lookup"><span data-stu-id="4cbf2-292">Scheduling Ads with VMAP</span></span>
<span data-ttu-id="4cbf2-293">powitania po przykładzie pokazano, jak przy użyciu pliku VMAP reklam tooschedule.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-293">hello following example shows how tooschedule ads using a VMAP file.</span></span>

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

### <a name="scheduling-ads-with-vast"></a><span data-ttu-id="4cbf2-294">Planowanie reklam z VAST</span><span class="sxs-lookup"><span data-stu-id="4cbf2-294">Scheduling Ads with VAST</span></span>
<span data-ttu-id="4cbf2-295">Hello następujące przykładowe pokazuje, jak tooschedule późne wiązanie PRZEWAŻAJĄCA ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-295">hello following sample shows how tooschedule a late binding VAST ad.</span></span>

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

   <span data-ttu-id="4cbf2-296">Hello następujące przykładowe pokazuje, jak tooschedule wczesne ad PRZEWAŻAJĄCA powiązania.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-296">hello following sample shows how tooschedule an early binding VAST ad.</span></span>
<span data-ttu-id="4cbf2-297">Przykład: 4 harmonogram wczesnego wiązania PRZEWAŻAJĄCA ad //Download hello VAST plik, jeśli (! [[ framework.adResolver downloadManifest: & manifestu withURL: [URLWithString nsurl OCZEKIWANEGO: @"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) {[self logFrameworkError];} else {adLinearTime.startTime = 7; adLinearTime.duration = 0;</span><span class="sxs-lookup"><span data-stu-id="4cbf2-297">//Example:4 Schedule an early binding VAST ad //Download hello VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span></span>

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

<span data-ttu-id="4cbf2-298">Hello następujące przykładowe pokazuje, jak tooinsert ad za pomocą nierównej Wytnij edycji (rz)</span><span class="sxs-lookup"><span data-stu-id="4cbf2-298">hello following sample shows how tooinsert an ad using Rough Cut Editing (RCE)</span></span>

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

<span data-ttu-id="4cbf2-299">Witaj poniższy przykład przedstawia sposób pod tooschedule ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-299">hello following example shows how tooschedule an ad pod.</span></span>

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

<span data-ttu-id="4cbf2-300">powitania po przykładzie pokazano, jak tooschedule-trwałe ad pośredniej zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-300">hello following example shows how tooschedule a non-sticky mid-roll ad.</span></span> <span data-ttu-id="4cbf2-301">Ad trwałe tylko zostanie odtworzony po niezależnie od wszelkich wyszukiwania hello wykonuje podglądu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-301">A non-sticky ad is only played once regardless of any seeking hello viewer performs.</span></span>

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

<span data-ttu-id="4cbf2-302">powitania po przykładzie pokazano, jak tooschedule trwałe ad pośredniej zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-302">hello following example shows how tooschedule a sticky mid-roll ad.</span></span> <span data-ttu-id="4cbf2-303">Trwałe ad będą wyświetlane zawsze, gdy określony hello osiągnięciu punktu w hello wideo na osi czasu.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-303">A sticky ad will be displayed each time hello specified point on hello video timeline is reached.</span></span>

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


<span data-ttu-id="4cbf2-304">Hello następujące przykładowe pokazuje, jak tooschedule ad końcu pliku.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-304">hello following sample shows how tooschedule a post-roll ad.</span></span>

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

<span data-ttu-id="4cbf2-305">Hello następujące przykładowe pokazuje, jak tooschedule ad wstępne zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-305">hello following sample shows how tooschedule a pre-roll ad.</span></span>

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

<span data-ttu-id="4cbf2-306">Witaj następujące przykładowe pokazuje, jak tooschedule pośredniej zbiorczego nakładki ad.</span><span class="sxs-lookup"><span data-stu-id="4cbf2-306">hello following sample shows how tooschedule a mid-roll overlay ad.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="4cbf2-307">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="4cbf2-307">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4cbf2-308">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="4cbf2-308">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="4cbf2-309">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4cbf2-309">See Also</span></span>
[<span data-ttu-id="4cbf2-310">Opracowywanie aplikacji odtwarzacza wideo</span><span class="sxs-lookup"><span data-stu-id="4cbf2-310">Develop video player applications</span></span>](media-services-develop-video-players.md)

