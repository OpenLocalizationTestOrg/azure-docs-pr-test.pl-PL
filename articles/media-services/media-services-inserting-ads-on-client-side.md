---
title: Wstawianie reklam po stronie klienta | Dokumentacja firmy Microsoft
description: "W tym temacie przedstawiono sposób wstawiania reklam po stronie klienta."
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
ms.openlocfilehash: 52ba731f88c630830560e3cf8406ba2e9613c8a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="inserting-ads-on-the-client-side"></a><span data-ttu-id="a5fd2-103">Wstawianie reklam po stronie klienta</span><span class="sxs-lookup"><span data-stu-id="a5fd2-103">Inserting ads on the client side</span></span>
<span data-ttu-id="a5fd2-104">Ten temat zawiera informacje na temat sposobu Wstaw różnych typów reklam po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-104">This topic contains information on how to insert various types of ads on the client side.</span></span>

<span data-ttu-id="a5fd2-105">Informacje na temat zamkniętego podpisów i ad obsługi w wideo transmisji strumieniowej na żywo, zobacz [obsługiwane kodowane i standardy wstawiania Ad](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span><span class="sxs-lookup"><span data-stu-id="a5fd2-105">For information about closed captioning and ad support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span></span>

> [!NOTE]
> <span data-ttu-id="a5fd2-106">Azure Media Player nie obsługuje obecnie reklam.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-106">Azure Media Player does not currently support Ads.</span></span>
> 
> 

## <span data-ttu-id="a5fd2-107"><a id="insert_ads_into_media"></a>Wstawianie reklam do multimediów</span><span class="sxs-lookup"><span data-stu-id="a5fd2-107"><a id="insert_ads_into_media"></a>Inserting Ads into your Media</span></span>
<span data-ttu-id="a5fd2-108">Usługa Azure Media Services obsługuje wstawiania reklam za pośrednictwem platformy Windows Media: struktur odtwarzaczy.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-108">Azure Media Services provides support for ad insertion through the Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="a5fd2-109">Struktur odtwarzaczy z obsługą ad są dostępne dla urządzeń z systemem Windows 8, Silverlight, Windows Phone 8 i iOS.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-109">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="a5fd2-110">Każdy framework player zawiera przykładowy kod, który pokazuje, jak wdrożyć aplikacja odtwarzacza. Istnieją trzy różne rodzaje reklamy, które można wstawić do nośnika: listy.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-110">Each player framework contains sample code that shows you how to implement a player application.There are three different kinds of ads you can insert into your media:list.</span></span>

* <span data-ttu-id="a5fd2-111">**Liniowy** — pełna reklam ramki Wstrzymaj głównego wideo.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-111">**Linear** – full frame ads that pause the main video.</span></span>
* <span data-ttu-id="a5fd2-112">**Rożne** — nakładki reklamy, które są wyświetlane podczas odtwarzania wideo głównego, zwykle logo lub inne statyczny obraz umieszczony odtwarzacza.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-112">**Nonlinear** – overlay ads that are displayed as the main video is playing, usually a logo or other static image placed within the player.</span></span>
* <span data-ttu-id="a5fd2-113">**Pomocnik** — reklam wyświetlanych poza odtwarzacza.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-113">**Companion** – ads that are displayed outside of the player.</span></span>

<span data-ttu-id="a5fd2-114">Usługa AD można umieścić w dowolnym momencie wideo głównych osi czasu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-114">Ads can be placed at any point in the main video’s time line.</span></span> <span data-ttu-id="a5fd2-115">Odtwarzacz musi sprawdzić, kiedy odtwarzać ad i które reklam, aby odtworzyć.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-115">You must tell the player when to play the ad and which ads to play.</span></span> <span data-ttu-id="a5fd2-116">Jest to realizowane przy użyciu zestawu standardowych plików opartych na języku XML: wideo Ad Service szablonu (VAST), cyfrowy wideo wielu Ad listy odtwarzania (VMAP) nośnika abstrakcyjny sekwencjonowania szablonu (MASZTÓW) i cyfrowy wideo Player Ad interfejsu definicji (VPAID).</span><span class="sxs-lookup"><span data-stu-id="a5fd2-116">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="a5fd2-117">Pliki PRZEWAŻAJĄCA określają, jakie reklam, aby wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-117">VAST files specify what ads to display.</span></span> <span data-ttu-id="a5fd2-118">Pliki VMAP Określ, kiedy do odtwarzania różnych reklam i zawierać PRZEWAŻAJĄCA XML.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-118">VMAP files specify when to play various ads and contain VAST XML.</span></span> <span data-ttu-id="a5fd2-119">Pliki MASZTÓW są reklam sekwencji, których może również zawierać PRZEWAŻAJĄCA XML w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-119">MAST files are another way to sequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="a5fd2-120">Pliki VPAID zdefiniuj interfejs między odtwarzacza wideo i ad lub serwera usługi ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-120">VPAID files define an interface between the video player and the ad or ad server.</span></span>

<span data-ttu-id="a5fd2-121">Każdy framework player zmieniło i wszystkie będą opisane w temacie własny.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-121">Each player framework works differently and each will be covered in its own topic.</span></span> <span data-ttu-id="a5fd2-122">W tym temacie opisano podstawowe mechanizmy, które służy do wstawiania reklam. Aplikacji odtwarzacza wideo żądania reklam z serwera ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-122">This topic will describe the basic mechanisms used to insert ads.Video player applications request ads from an ad server.</span></span> <span data-ttu-id="a5fd2-123">Serwer ad może odpowiadać na kilka sposobów:</span><span class="sxs-lookup"><span data-stu-id="a5fd2-123">The ad server can respond in a number of ways:</span></span>

* <span data-ttu-id="a5fd2-124">Zwraca PRZEWAŻAJĄCA plik</span><span class="sxs-lookup"><span data-stu-id="a5fd2-124">Return a VAST file</span></span>
* <span data-ttu-id="a5fd2-125">Zwraca plik VMAP (z osadzonych VAST)</span><span class="sxs-lookup"><span data-stu-id="a5fd2-125">Return a VMAP file (with embedded VAST)</span></span>
* <span data-ttu-id="a5fd2-126">Zwraca plik MASZTÓW (z osadzonych VAST)</span><span class="sxs-lookup"><span data-stu-id="a5fd2-126">Return a MAST file (with embedded VAST)</span></span>
* <span data-ttu-id="a5fd2-127">Zwraca PRZEWAŻAJĄCA plik z VPAID reklam</span><span class="sxs-lookup"><span data-stu-id="a5fd2-127">Return a VAST file with VPAID ads</span></span>

### <a name="using-a-video-ad-service-template-vast-file"></a><span data-ttu-id="a5fd2-128">Przy użyciu pliku szablonu (VAST) usługi Ad wideo</span><span class="sxs-lookup"><span data-stu-id="a5fd2-128">Using a Video Ad Service Template (VAST) File</span></span>
<span data-ttu-id="a5fd2-129">PRZEWAŻAJĄCA pliku Określa, jakie ad lub reklam, aby wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-129">A VAST file specifies what ad or ads to display.</span></span> <span data-ttu-id="a5fd2-130">Następujący kod XML jest przykładowy plik PRZEWAŻAJĄCA liniowej AD:</span><span class="sxs-lookup"><span data-stu-id="a5fd2-130">The following XML is an example of a VAST file for a linear ad:</span></span>

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

<span data-ttu-id="a5fd2-131">Liniowy ad jest opisane przez <**liniowy**> elementu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-131">The linear ad is described by the <**Linear**> element.</span></span> <span data-ttu-id="a5fd2-132">Określa czas trwania ad, śledzenia zdarzeń, kliknij go, kliknij przycisk śledzenia i liczbę **MediaFile** elementów.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-132">It specifies the duration of the ad, tracking events, click through, click tracking, and a number of **MediaFile** elements.</span></span> <span data-ttu-id="a5fd2-133">Zdarzenia śledzenia są określone w <**TrackingEvents**> element i umożliwić serwera ad do śledzenia różnych zdarzeń występujących podczas wyświetlania ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-133">Tracking events are specified within the <**TrackingEvents**> element and allow an ad server to track various events that occur while viewing the ad.</span></span> <span data-ttu-id="a5fd2-134">W takim przypadku początek środkowego zakończeniu i rozwiń listę zdarzeń są śledzone.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-134">In this case the start, midpoint, complete, and expand events are tracked.</span></span> <span data-ttu-id="a5fd2-135">Zdarzenia uruchamiania występuje, gdy usługi ad jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-135">The start event occurs when the ad is displayed.</span></span> <span data-ttu-id="a5fd2-136">Zdarzenie środkowego występuje, gdy co najmniej się, że wyświetlił 50% ad osi czasu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-136">The midpoint event occurs when at least 50% of the ad’s timeline has been viewed.</span></span> <span data-ttu-id="a5fd2-137">Zdarzenie ukończenia występuje, gdy usługi ad zostało uruchomione na końcu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-137">The complete event occurs when the ad has run to the end.</span></span> <span data-ttu-id="a5fd2-138">Rozwiń zdarzenie występuje, gdy użytkownik rozwija odtwarzacza wideo do pełnego ekranu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-138">The Expand event occurs when the user expands the video player to full screen.</span></span> <span data-ttu-id="a5fd2-139">Clickthroughs są określane za pomocą <**przeglądowego**> w elemencie <**VideoClicks**> element i określa identyfikator URI zasobu do wyświetlenia, gdy użytkownik kliknie ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-139">Clickthroughs are specified with a <**ClickThrough**> element within a <**VideoClicks**> element and specifies a URI to a resource to display when the user clicks on the ad.</span></span> <span data-ttu-id="a5fd2-140">ClickTracking jest określona w <**ClickTracking**> elementu również w <**VideoClicks**> element i umożliwia określenie zasobu śledzenia odtwarzacza na żądanie, gdy użytkownik kliknie ad . <**MediaFile**> elementy Określ informacje dotyczące określonego kodowania AD.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-140">ClickTracking is specified in a <**ClickTracking**> element, also within the <**VideoClicks**> element and specifies a tracking resource for the player to request when the user clicks on the ad.The <**MediaFile**> elements specify information about a specific encoding of an ad.</span></span> <span data-ttu-id="a5fd2-141">Gdy istnieje więcej niż jeden <**MediaFile**> elementu odtwarzacza wideo można wybrać optymalne kodowanie dla platformy.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-141">When there is more than one <**MediaFile**> element, the video player can choose the best encoding for the platform.</span></span> 

<span data-ttu-id="a5fd2-142">Liniowy reklam mogą być wyświetlane w określonej kolejności.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-142">Linear ads can be displayed in a specified order.</span></span> <span data-ttu-id="a5fd2-143">W tym celu należy dodać dodatkowe <Ad> elementy VAST pliku i określić kolejność przy użyciu atrybutu sekwencji.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-143">To do this, add additional <Ad> elements to the VAST file and specify the order using the sequence attribute.</span></span> <span data-ttu-id="a5fd2-144">Poniższy przykład przedstawia to:</span><span class="sxs-lookup"><span data-stu-id="a5fd2-144">The following example illustrates this:</span></span>

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

<span data-ttu-id="a5fd2-145">Rożne reklam są określone w <Creative> również element.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-145">Nonlinear ads are specified in a <Creative> element as well.</span></span> <span data-ttu-id="a5fd2-146">W poniższym przykładzie przedstawiono <Creative> element, który opisuje rożne ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-146">The following example shows a <Creative> element that describes a nonlinear ad.</span></span>

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


<span data-ttu-id="a5fd2-147"><**NonLinearAds**> element może zawierać co najmniej jeden <**NonLinear**> elementy, które opisują rożne ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-147">The <**NonLinearAds**> element can contain one or more <**NonLinear**> elements, each of which can describe a nonlinear ad.</span></span> <span data-ttu-id="a5fd2-148"><**NonLinear**> element określa zasobu dla rożne ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-148">The <**NonLinear**> element specifies the resource for the nonlinear ad.</span></span> <span data-ttu-id="a5fd2-149">Zasób może być <**StaticResouce**>, <**IFrameResource**>, lub <**HTMLResouce**>.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-149">The resource can be a <**StaticResouce**>, an <**IFrameResource**>, or an <**HTMLResouce**>.</span></span><span data-ttu-id="a5fd2-150"> <**StaticResource**> opisuje zasób w innym języku niż HTML i definiuje atrybut creativeType, który określa sposób wyświetlania zasobu:</span><span class="sxs-lookup"><span data-stu-id="a5fd2-150"> <**StaticResource**> describes a non-HTML resource and defines a creativeType attribute that specifies how the resource is displayed:</span></span>

<span data-ttu-id="a5fd2-151">Obraz/gif, image/jpeg, obrazu/png — zasobu jest wyświetlana w formacie HTML <**img**> tagu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-151">Image/gif, image/jpeg, image/png – the resource is displayed in an HTML <**img**> tag.</span></span>

<span data-ttu-id="a5fd2-152">Application/x-javascript — zasobu jest wyświetlana w formacie HTML <**skryptu**> tagu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-152">Application/x-javascript – the resource is displayed in an HTML <**script**> tag.</span></span>

<span data-ttu-id="a5fd2-153">Application/x-shockwave-flash — zasobu jest wyświetlany w Flash player.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-153">Application/x-shockwave-flash – the resource is displayed in a Flash player.</span></span>

<span data-ttu-id="a5fd2-154">**IFrameResource** opisuje zasobu HTML, który może być wyświetlany w elementu IFrame.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-154">**IFrameResource** describes an HTML resource that can be displayed in an IFrame.</span></span> <span data-ttu-id="a5fd2-155">**HTMLResource** opisuje fragment kodu HTML, który można wstawiać do strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-155">**HTMLResource** describes a piece of HTML code that can be inserted into a web page.</span></span> <span data-ttu-id="a5fd2-156">**TrackingEvents** Określ śledzenia zdarzeń i identyfikator URI żądania po wystąpieniu zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-156">**TrackingEvents** specify tracking events and the URI to request when the event occurs.</span></span> <span data-ttu-id="a5fd2-157">W tym przykładzie zdarzenia acceptInvitation i Zwiń są śledzone.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-157">In this sample the acceptInvitation and collapse events are tracked.</span></span> <span data-ttu-id="a5fd2-158">Aby uzyskać więcej informacji na temat **NonLinearAds** elementu i jego elementów podrzędnych, zobacz IAB.NET/VAST.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-158">For more information on the **NonLinearAds** element and its children, see IAB.NET/VAST.</span></span> <span data-ttu-id="a5fd2-159">Należy pamiętać, że **TrackingEvents** element znajduje się w **NonLinearAds** elementu zamiast **NonLinear** elementu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-159">Note that the **TrackingEvents** element is located within the **NonLinearAds** element rather than the **NonLinear** element.</span></span>

<span data-ttu-id="a5fd2-160">Pomocnik reklam są zdefiniowane w <CompanionAds> elementu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-160">Companion ads are defined within a <CompanionAds> element.</span></span> <span data-ttu-id="a5fd2-161"><CompanionAds> Element może zawierać jeden lub więcej <Companion> elementów.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-161">The <CompanionAds> element can contain one or more <Companion> elements.</span></span> <span data-ttu-id="a5fd2-162">Każdy <Companion> elementu opisuje ad pomocnika i może zawierać <StaticResource>, <IFrameResource>, lub <HTMLResource> określono w taki sam sposób jak rożne ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-162">Each <Companion> element describes a companion ad and can contain a <StaticResource>, <IFrameResource>, or <HTMLResource> which are specified in the same way as in a nonlinear ad.</span></span> <span data-ttu-id="a5fd2-163">PRZEWAŻAJĄCA plik może zawierać wiele pomocnika reklam i aplikacja odtwarzacza można wybrać najodpowiedniejszy ad do wyświetlenia.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-163">A VAST file can contain multiple companion ads and the player application can choose the most appropriate ad to display.</span></span> <span data-ttu-id="a5fd2-164">Aby uzyskać więcej informacji o VAST, zobacz [3.0 PRZEWAŻAJĄCA](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="a5fd2-164">For more information about VAST, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span>

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a><span data-ttu-id="a5fd2-165">Przy użyciu wielu pliku listy odtwarzania (VMAP) Ad cyfrowy wideo</span><span class="sxs-lookup"><span data-stu-id="a5fd2-165">Using a Digital Video Multiple Ad Playlist (VMAP) File</span></span>
<span data-ttu-id="a5fd2-166">Pliku VMAP umożliwia określenie, kiedy występują podziały ad, jak długo trwa każdego podziału ile reklam mogą być wyświetlane w ramach podziału i jakie typy reklam mogą być wyświetlane podczas podziału.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-166">A VMAP file allows you to specify when ad breaks occur, how long each break is, how many ads can be displayed within a break, and what types of ads may be displayed during a break.</span></span> <span data-ttu-id="a5fd2-167">Poniższy przykładowy plik VMAP, który definiuje podział pojedynczego ad:</span><span class="sxs-lookup"><span data-stu-id="a5fd2-167">The following in an example VMAP file that defines a single ad break:</span></span>

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

<span data-ttu-id="a5fd2-168">Rozpoczyna się od pliku VMAP <VMAP> element, który zawiera co najmniej jeden <AdBreak> elementy Definiowanie podziału ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-168">A VMAP file begins with a <VMAP> element that contains one or more <AdBreak> elements, each defining an ad break.</span></span> <span data-ttu-id="a5fd2-169">Każdy podziału ad Określa typ podziału, identyfikator podziału i przesunięcie czasu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-169">Each ad break specifies a break type, break ID, and time offset.</span></span> <span data-ttu-id="a5fd2-170">Atrybut breakType Określa typ ad, która może być odtwarzany podczas przerwy: liniowych, rożne, lub wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-170">The breakType attribute specifies the type of ad that can be played during the break: linear, nonlinear, or display.</span></span> <span data-ttu-id="a5fd2-171">Wyświetlenie mapy reklam PRZEWAŻAJĄCA pomocnika reklam.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-171">Display ads map to VAST companion ads.</span></span> <span data-ttu-id="a5fd2-172">Można określić więcej niż jeden typ ad w postaci listy rozdzielanej przecinkami (bez spacji).</span><span class="sxs-lookup"><span data-stu-id="a5fd2-172">More than one ad type can be specified in a comma (no spaces) separated list.</span></span> <span data-ttu-id="a5fd2-173">BreakID jest opcjonalny identyfikator usługi ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-173">The breakID is an optional identifier for the ad.</span></span> <span data-ttu-id="a5fd2-174">TimeOffset Określa, kiedy powinny być wyświetlane ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-174">The timeOffset specifies when the ad should be displayed.</span></span> <span data-ttu-id="a5fd2-175">Można ją określić w jednym z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="a5fd2-175">It can be specified in one of the following ways:</span></span>

1. <span data-ttu-id="a5fd2-176">Godzina w formacie hh: mm: lub GG:mm:ss.mmm .mmm w przypadku milisekund.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-176">Time – in hh:mm:ss or hh:mm:ss.mmm format where .mmm is milliseconds.</span></span> <span data-ttu-id="a5fd2-177">Wartość tego atrybutu określa czas od początku wideo osi czasu na początku podziału ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-177">The value of this attribute specifies the time from the beginning of the video timeline to the beginning of the ad break.</span></span>
2. <span data-ttu-id="a5fd2-178">Wartość procentowa — w formacie n %, gdzie n to odsetek wideo osi czasu do odtwarzania przed odtwarzanie ad</span><span class="sxs-lookup"><span data-stu-id="a5fd2-178">Percentage – in n% format where n is the percentage of the video timeline to play before playing the ad</span></span>
3. <span data-ttu-id="a5fd2-179">Rozpoczęcie i zakończenie — Określa, że usługi ad powinna być wyświetlana przed lub po wideo został wyświetlony</span><span class="sxs-lookup"><span data-stu-id="a5fd2-179">Start/End – specifies that an ad should be displayed before or after the video has been displayed</span></span>
4. <span data-ttu-id="a5fd2-180">Umieść — określa kolejność podziały ad, gdy czas przerwy ad jest nieznany, takie jak transmisja strumieniowa na żywo.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-180">Position – specifies the order of ad breaks when the timing of the ad breaks is unknown, such as in live streaming.</span></span> <span data-ttu-id="a5fd2-181">Kolejność każdego podziału ad jest określona w formacie #n, gdzie n to liczba całkowita mniejsza od 1.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-181">The order of each ad break is specified in the #n format where n is an integer 1 or greater.</span></span> <span data-ttu-id="a5fd2-182">1 oznacza, że powinien zostać odtworzone ad przy okazji pierwszego, 2 oznacza ad powinna zostać odtworzone przy okazji drugi i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-182">1 signifies the ad should be played at the first opportunity, 2 signifies the ad should be played at the second opportunity and so on.</span></span>

<span data-ttu-id="a5fd2-183">W ramach <**AdBreak**> element może być jedną <**AdSource**> elementu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-183">Within the <**AdBreak**> element there can be one <**AdSource**> element.</span></span> <span data-ttu-id="a5fd2-184"><**AdSource**> element zawiera następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="a5fd2-184">The <**AdSource**> element contains the following attributes:</span></span>

1. <span data-ttu-id="a5fd2-185">Identyfikator — Określa identyfikator źródła usługi ad</span><span class="sxs-lookup"><span data-stu-id="a5fd2-185">Id – specifies an identifier for the ad source</span></span>
2. <span data-ttu-id="a5fd2-186">allowMultipleAds — wartość logiczna określająca, czy można wyświetlić wiele reklam podczas podziału ad</span><span class="sxs-lookup"><span data-stu-id="a5fd2-186">allowMultipleAds – a Boolean value that specifies whether multiple ads can be displayed during the ad break</span></span>
3. <span data-ttu-id="a5fd2-187">followRedirects — opcjonalna wartość logiczna określająca, czy należy przestrzegać odtwarzacza wideo przekierowuje w odpowiedzi usługi ad</span><span class="sxs-lookup"><span data-stu-id="a5fd2-187">followRedirects – an optional Boolean value that specifies if the video player should honor redirects within an ad response</span></span>

<span data-ttu-id="a5fd2-188"><**AdSource**> element udostępnia odtwarzacz odpowiedzi ad wbudowanego lub odwołanie do odpowiedzi ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-188">The <**AdSource**> element provides the player an inline ad response or a reference to an ad response.</span></span> <span data-ttu-id="a5fd2-189">Nazwa może zawierać jedną z następujących elementów:</span><span class="sxs-lookup"><span data-stu-id="a5fd2-189">It can contain one of the following elements:</span></span>

* <span data-ttu-id="a5fd2-190"><VASTAdData>Wskazuje, że odpowiedź PRZEWAŻAJĄCA ad jest osadzony w pliku VMAP</span><span class="sxs-lookup"><span data-stu-id="a5fd2-190"><VASTAdData> indicates a VAST ad response is embedded within the VMAP file</span></span>
* <span data-ttu-id="a5fd2-191"><AdTagURI>Identyfikator URI, który odwołuje się do odpowiedzi ad z innego systemu</span><span class="sxs-lookup"><span data-stu-id="a5fd2-191"><AdTagURI> a URI that references an ad response from another system</span></span>
* <span data-ttu-id="a5fd2-192"><CustomAdData>-dowolnego ciągu tego respresents-PRZEWAŻAJĄCA odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a5fd2-192"><CustomAdData> -an arbitrary string that respresents a non-VAST response</span></span>

<span data-ttu-id="a5fd2-193">W tym przykładzie odpowiedzi w wierszu ad zostanie określony z <VASTAdData> element, który zawiera odpowiedzi PRZEWAŻAJĄCA ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-193">In this example an in-line ad response is specified with a <VASTAdData> element that contains a VAST ad response.</span></span> <span data-ttu-id="a5fd2-194">Aby uzyskać więcej informacji na temat innych elementów zobacz [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span><span class="sxs-lookup"><span data-stu-id="a5fd2-194">For more information about the other elements, see [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span></span>

<span data-ttu-id="a5fd2-195"><**AdBreak**> element może również zawierać jedną <**TrackingEvents**> elementu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-195">The <**AdBreak**> element can also contain one <**TrackingEvents**> element.</span></span> <span data-ttu-id="a5fd2-196"><**TrackingEvents**> element służy do śledzenia początek lub koniec podziału ad lub czy wystąpił błąd podczas podziału ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-196">The <**TrackingEvents**> element allows you to track the start or end of an ad break or whether an error occurred during the ad break.</span></span> <span data-ttu-id="a5fd2-197"><**TrackingEvents**> elementu zawiera jeden lub więcej <**śledzenia**> elementów, z których każdy określa zdarzenia śledzenia i śledzenia identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-197">The <**TrackingEvents**> element contains one or more <**Tracking**> elements, each of which specifies a tracking event and a tracking URI.</span></span> <span data-ttu-id="a5fd2-198">Zdarzenia śledzenia możliwe są:</span><span class="sxs-lookup"><span data-stu-id="a5fd2-198">The possible tracking events are:</span></span>

1. <span data-ttu-id="a5fd2-199">breakStart — śledzi początku podziału ad</span><span class="sxs-lookup"><span data-stu-id="a5fd2-199">breakStart – tracks the beginning of an ad break</span></span>
2. <span data-ttu-id="a5fd2-200">breakEnd — sprawdzenie jego ukończenia podziału ad</span><span class="sxs-lookup"><span data-stu-id="a5fd2-200">breakEnd – track the completion of an ad break</span></span>
3. <span data-ttu-id="a5fd2-201">Błąd — śledzi wystąpił błąd, który wystąpił podczas podziału ad</span><span class="sxs-lookup"><span data-stu-id="a5fd2-201">error – tracks an error that occurred during the ad break</span></span>

<span data-ttu-id="a5fd2-202">W poniższym przykładzie przedstawiono plik VMAP określający zdarzenia śledzenia</span><span class="sxs-lookup"><span data-stu-id="a5fd2-202">The following example shows a VMAP file that specifies tracking events</span></span>

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

<span data-ttu-id="a5fd2-203">Aby uzyskać więcej informacji na temat <**TrackingEvents**> elementu i jego elementów podrzędnych, zobacz http://iab.org/VMAP.pdf</span><span class="sxs-lookup"><span data-stu-id="a5fd2-203">For more information on the <**TrackingEvents**> element and its children, see http://iab.org/VMAP.pdf</span></span>

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a><span data-ttu-id="a5fd2-204">Przy użyciu abstrakcyjny nośnika, sekwencjonowania pliku szablonu (MASZTÓW)</span><span class="sxs-lookup"><span data-stu-id="a5fd2-204">Using a Media Abstract Sequencing Template (MAST) File</span></span>
<span data-ttu-id="a5fd2-205">Plik MASZTÓW umożliwia określenie wyzwalaczy, które określają, kiedy jest wyświetlany przy użyciu usług ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-205">A MAST file allows you to specify triggers that define when an ad is displayed.</span></span> <span data-ttu-id="a5fd2-206">Oto przykładowy plik MASZTÓW, który zawiera wyzwalacze ad zbiorczego sprzed, ad zbiorczego pośredniej i ad po zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-206">The following is an example MAST file that contains triggers for a pre roll ad, a mid-roll ad, and a post-roll ad.</span></span>

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
            <!--This 'resets' the trigger for the next clip-->
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



<span data-ttu-id="a5fd2-207">Rozpoczyna się od pliku MASZTÓW **MASZTÓW** element, który zawiera jeden **wyzwalaczy** elementu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-207">A MAST file begins with a **MAST** element that contains one **triggers** element.</span></span> <span data-ttu-id="a5fd2-208"><triggers> Elementu zawiera jeden lub więcej **wyzwalacza** elementów, które określają, kiedy można odtwarzać przy użyciu usług ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-208">The <triggers> element contains one or more **trigger** elements that define when an ad should be played.</span></span> 

<span data-ttu-id="a5fd2-209">**Wyzwalacza** element zawiera **startConditions** elementu, którego Określ rozpoczęcia ad do odtwarzania.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-209">The **trigger** element contains a **startConditions** element which specify when an ad should begin to play.</span></span> <span data-ttu-id="a5fd2-210">**StartConditions** elementu zawiera jeden lub więcej <condition> elementów.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-210">The **startConditions** element contains one or more <condition> elements.</span></span> <span data-ttu-id="a5fd2-211">Podczas każdego <condition> zwraca wartość true, wyzwalacz zainicjowaniu lub odwołane, w zależności od czy <condition> jest zawarty w **startConditions** lub **endConditions** — element odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-211">When each <condition> evaluates to true a trigger is initiated or revoked depending upon whether the <condition> is contained within a **startConditions** or **endConditions** element respectively.</span></span> <span data-ttu-id="a5fd2-212">Gdy wiele <condition> elementy znajdują się, są traktowane jako niejawne OR, warunki obliczane do wartości true spowoduje, że trigger, aby zainicjować.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-212">When multiple <condition> elements are present, they are treated as an implicit OR, any condition evaluating to true will cause the trigger to initiate.</span></span> <span data-ttu-id="a5fd2-213"><condition>elementy mogą być zagnieżdżone.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-213"><condition> elements can be nested.</span></span> <span data-ttu-id="a5fd2-214">Gdy podrzędny <condition> elementy są zdefiniowane, są traktowane jak i niejawne, wszystkie warunki musi zwrócić wartość true dla wyzwalacza do zainicjowania.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-214">When child <condition> elements are preset, they are treated as an implicit AND, all conditions must evaluate to true for the trigger to initiate.</span></span> <span data-ttu-id="a5fd2-215"><condition> Element zawiera następujące atrybuty, które definiują warunek:</span><span class="sxs-lookup"><span data-stu-id="a5fd2-215">The <condition> element contains the following attributes that define the condition:</span></span> 

1. <span data-ttu-id="a5fd2-216">**Typ** — Określa typ zdarzenia lub warunku właściwości</span><span class="sxs-lookup"><span data-stu-id="a5fd2-216">**type** – specifies the type of condition, event or property</span></span>
2. <span data-ttu-id="a5fd2-217">**Nazwa** — nazwa właściwości lub zdarzeń, które mają być użyte podczas obliczania</span><span class="sxs-lookup"><span data-stu-id="a5fd2-217">**name** – the name of the property or event to be used during evaluation</span></span>
3. <span data-ttu-id="a5fd2-218">**wartość** — wartość, która będzie porównywany właściwości</span><span class="sxs-lookup"><span data-stu-id="a5fd2-218">**value** – the value that a property will be evaluated against</span></span>
4. <span data-ttu-id="a5fd2-219">**operator** — operacji do użycia podczas obliczania: EQ (równości), NEQ (różne), GTR (większe), GEQ (większe lub równe), LT (poniżej), LEQ (mniejsze niż lub równe), MOD (modulo)</span><span class="sxs-lookup"><span data-stu-id="a5fd2-219">**operator** – the operation to use during evaluation: EQ (equal), NEQ (not equal), GTR (greater), GEQ (greater or equal), LT (Less than), LEQ (less than or equal), MOD (modulo)</span></span>

<span data-ttu-id="a5fd2-220">**endConditions** również zawierać <condition> elementów.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-220">**endConditions** also contain <condition> elements.</span></span> <span data-ttu-id="a5fd2-221">Jeśli wynikiem warunku jest PRAWDA wyzwalacza zostanie zresetowany. <trigger> Zawiera również element <sources> element, który zawiera co najmniej jeden <source> elementów.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-221">When a condition evaluates to true the trigger is reset.The <trigger> element also contains a <sources> element that contains one or more <source> elements.</span></span> <span data-ttu-id="a5fd2-222"><source> Elementy Definiowanie identyfikator URI odpowiedzi usługi ad i typ odpowiedzi ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-222">The <source> elements define the URI to the ad response and the type of ad response.</span></span> <span data-ttu-id="a5fd2-223">W tym przykładzie identyfikatora URI znajduje się na OGROMNĄ odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-223">In this example a URI is given to a VAST response.</span></span> 

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


### <a name="using-video-player-ad-interface-definition-vpaid"></a><span data-ttu-id="a5fd2-224">Przy użyciu odtwarzacza wideo-Ad definicji interfejsu (VPAID)</span><span class="sxs-lookup"><span data-stu-id="a5fd2-224">Using Video Player-Ad Interface Definition (VPAID)</span></span>
<span data-ttu-id="a5fd2-225">VPAID to interfejs API umożliwiający jednostki ad pliku wykonywalnego do komunikowania się z odtwarzacza wideo.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-225">VPAID is an API for enabling executable ad units to communicate with a video player.</span></span> <span data-ttu-id="a5fd2-226">Dzięki temu ad wysokiej interaktywnego środowiska.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-226">This allows highly interactive ad experiences.</span></span> <span data-ttu-id="a5fd2-227">Użytkownik może interakcyjnie ad i ad może odpowiadać na akcje wykonywane przez Podgląd.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-227">The user can interact with the ad and the ad can respond to actions taken by the viewer.</span></span> <span data-ttu-id="a5fd2-228">Na przykład ad mogą być wyświetlane przyciski umożliwiające użytkownika wyświetlić więcej informacji lub dłużej wersji ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-228">For example an ad may display buttons that allow the user to view more information or a longer version of the ad.</span></span> <span data-ttu-id="a5fd2-229">Odtwarzacza wideo musi obsługiwać interfejs API VPAID i ad pliku wykonywalnego musi implementować interfejs API.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-229">The video player must support the VPAID API and the executable ad must implement the API.</span></span> <span data-ttu-id="a5fd2-230">Gdy odtwarzacza zażąda się, że usługi ad z serwera ad serwera mogą odpowiadać za pomocą PRZEWAŻAJĄCA odpowiedzi, który zawiera VPAID ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-230">When a player requests an ad from an ad server the server may respond with a VAST response that contains a VPAID ad.</span></span>

<span data-ttu-id="a5fd2-231">Wykonywalny ad jest tworzony w kodu, który musi zostać wykonana w środowisko uruchomieniowe, takie jak Adobe Flash™ lub JavaScript, które mogą być wykonywane w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-231">An executable ad is created in code that must be executed in a runtime environment such as Adobe Flash™ or JavaScript that can be executed in a web browser.</span></span> <span data-ttu-id="a5fd2-232">Po powrocie z serwera ad PRZEWAŻAJĄCA odpowiedzi zawierające VPAID ad wartość apiFramework atrybutu w <MediaFile> element musi być "VPAID".</span><span class="sxs-lookup"><span data-stu-id="a5fd2-232">When an ad server returns a VAST response containing a VPAID ad, the value of the apiFramework attribute in the <MediaFile> element must be “VPAID”.</span></span> <span data-ttu-id="a5fd2-233">Ten atrybut określa, że zawarte ad jest VPAID ad pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-233">This attribute specifies that the contained ad is a VPAID executable ad.</span></span> <span data-ttu-id="a5fd2-234">Atrybut type musi mieć ustawioną typ MIME pliku wykonywalnego, takie jak "application/x-shockwave-flash" lub "application/x-javascript".</span><span class="sxs-lookup"><span data-stu-id="a5fd2-234">The type attribute must be set to the MIME type of the executable, such as “application/x-shockwave-flash” or “application/x-javascript”.</span></span> <span data-ttu-id="a5fd2-235">Poniższy fragment kodu przedstawia XML <MediaFile> element na podstawie PRZEWAŻAJĄCA odpowiedzi zawierające VPAID ad pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-235">The following XML snippet shows the <MediaFile> element from a VAST response containing a VPAID executable ad.</span></span> 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI to executable ad -->
       </MediaFile>
    </MediaFiles>


<span data-ttu-id="a5fd2-236">Można zainicjować pliku wykonywalnego ad przy użyciu <AdParameters> w elemencie <Linear> lub <NonLinear> elementów w PRZEWAŻAJĄCA odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-236">An executable ad can be initialized using the <AdParameters> element within the <Linear> or <NonLinear> elements in a VAST response.</span></span> <span data-ttu-id="a5fd2-237">Aby uzyskać więcej informacji na temat <AdParameters> elementu, zobacz [3.0 PRZEWAŻAJĄCA](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="a5fd2-237">For more information on the <AdParameters> element, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span> <span data-ttu-id="a5fd2-238">Aby uzyskać więcej informacji na temat interfejsu API VPAID, zobacz [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span><span class="sxs-lookup"><span data-stu-id="a5fd2-238">For more information about the VPAID API, see [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span></span>

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a><span data-ttu-id="a5fd2-239">Wdrażanie systemu Windows lub Windows Phone 8 Player z obsługą usługi Ad</span><span class="sxs-lookup"><span data-stu-id="a5fd2-239">Implementing a Windows or Windows Phone 8 Player with Ad Support</span></span>
<span data-ttu-id="a5fd2-240">Platforma Microsoft Media: Framework Player dla systemu Windows 8 i Windows Phone 8 zawiera kolekcję przykładowej aplikacji, które opisano sposób wdrożenia aplikacji odtwarzacza wideo, za pomocą środowiska.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-240">The Microsoft Media Platform: Player Framework for Windows 8 and Windows Phone 8 contains a collection of sample applications that show you how to implement a video player application using the framework.</span></span> <span data-ttu-id="a5fd2-241">Możesz pobrać Player Framework i przykłady z [Framework Player dla systemu Windows 8 i Windows Phone 8](https://playerframework.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="a5fd2-241">You can download the Player Framework and the samples from [Player Framework for Windows 8 and Windows Phone 8](https://playerframework.codeplex.com).</span></span>

<span data-ttu-id="a5fd2-242">Po otwarciu rozwiązania Microsoft.PlayerFramework.Xaml.Samples pojawi się liczba folderów w ramach projektu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-242">When you open the Microsoft.PlayerFramework.Xaml.Samples solution you will see a number of folders within the project.</span></span> <span data-ttu-id="a5fd2-243">Folder reklamy zawiera przykładowy kod dotyczą tworzenia odtwarzacza wideo z obsługą usługi ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-243">The Advertising folder contains the sample code relevant to creating a video player with ad support.</span></span> <span data-ttu-id="a5fd2-244">Wewnątrz reklamy folder jest XAML/cs pliki, które przedstawiają sposób wstawiania reklam w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-244">Inside the Advertising folder is a number of XAML/cs files each of which show how to insert ads in a different way.</span></span> <span data-ttu-id="a5fd2-245">Poniższa lista zawiera opis każdego:</span><span class="sxs-lookup"><span data-stu-id="a5fd2-245">The following list describes each:</span></span>

* <span data-ttu-id="a5fd2-246">AdPodPage.xaml przedstawia sposób wyświetlania pod ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-246">AdPodPage.xaml Shows how to display an ad pod.</span></span>
* <span data-ttu-id="a5fd2-247">AdSchedulingPage.xaml pokazano, jak zaplanować reklam.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-247">AdSchedulingPage.xaml Shows how to schedule ads.</span></span>
* <span data-ttu-id="a5fd2-248">FreeWheelPage.xaml przedstawia sposób użycia wtyczki FreeWheel można zaplanować reklam.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-248">FreeWheelPage.xaml Shows how to use the FreeWheel plugin to schedule ads.</span></span>
* <span data-ttu-id="a5fd2-249">MastPage.xaml pokazano, jak zaplanować reklam z plikiem MASZTÓW.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-249">MastPage.xaml Shows how to schedule ads with a MAST file.</span></span>
* <span data-ttu-id="a5fd2-250">ProgrammaticAdPage.xaml pokazano, jak programowo zaplanować reklam do klipu wideo.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-250">ProgrammaticAdPage.xaml Shows how to programmatically schedule ads into a video.</span></span>
* <span data-ttu-id="a5fd2-251">ScheduleClipPage.xaml pokazano, jak zaplanować ad bez PRZEWAŻAJĄCA pliku.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-251">ScheduleClipPage.xaml Shows how to schedule an ad without a VAST file.</span></span>
* <span data-ttu-id="a5fd2-252">VastLinearCompanionPage.xaml pokazuje sposób wstawiania w układzie liniowych i ad pomocnika.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-252">VastLinearCompanionPage.xaml Shows how to insert a linear and companion ad.</span></span>
* <span data-ttu-id="a5fd2-253">VastNonLinearPage.xaml pokazuje, jak można wstawić ad liniowej.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-253">VastNonLinearPage.xaml Shows how to insert a non-linear ad.</span></span>
* <span data-ttu-id="a5fd2-254">VmapPage.xaml pokazano, jak określić reklam z plikiem VMAP.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-254">VmapPage.xaml Shows how to specify ads with a VMAP file.</span></span>

<span data-ttu-id="a5fd2-255">Każda z tych próbek używa klasy MediaPlayer zdefiniowane przez platformę player.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-255">Each of these samples uses the MediaPlayer class defined by the player framework.</span></span> <span data-ttu-id="a5fd2-256">Większość przykładów za pomocą wtyczki obsługę różnych formatach odpowiedzi ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-256">Most samples use plugins that add support for various ad response formats.</span></span> <span data-ttu-id="a5fd2-257">Przykładowe ProgrammaticAdPage programowo współdziała z wystąpienia elementu MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-257">The ProgrammaticAdPage sample programmatically interacts with a MediaPlayer instance.</span></span>

### <a name="adpodpage-sample"></a><span data-ttu-id="a5fd2-258">Przykładowe AdPodPage</span><span class="sxs-lookup"><span data-stu-id="a5fd2-258">AdPodPage Sample</span></span>
<span data-ttu-id="a5fd2-259">W przykładzie użyto AdSchedulerPlugin, aby zdefiniować, kiedy należy wyświetlić przy użyciu usług ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-259">This sample uses the AdSchedulerPlugin to define when to display an ad.</span></span> <span data-ttu-id="a5fd2-260">W tym przykładzie anonsu pośredniej zbiorczego jest zaplanowane do odtwarzania po 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-260">In this example a mid-roll advertisement is scheduled to be played after 5 seconds.</span></span> <span data-ttu-id="a5fd2-261">Pod ad (grupa reklam, aby wyświetlić w kolejności) jest określona w pliku PRZEWAŻAJĄCA zwrócony z serwera usługi ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-261">The ad pod (a group of ads to display in order) is specified in a VAST file returned from an ad server.</span></span> <span data-ttu-id="a5fd2-262">Identyfikator URI do OGROMNYCH plików jest określona w <RemoteAdSource> elementu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-262">The URI to the VAST file is specified in the <RemoteAdSource> element.</span></span>

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

<span data-ttu-id="a5fd2-263">Aby uzyskać więcej informacji o AdSchedulerPlugin, zobacz [reklamy w ramach odtwarzacza w systemie Windows 8 i Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span><span class="sxs-lookup"><span data-stu-id="a5fd2-263">For more information about the AdSchedulerPlugin, see [Advertising in the Player Framework on Windows 8 and Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span></span>

### <a name="adschedulingpage"></a><span data-ttu-id="a5fd2-264">AdSchedulingPage</span><span class="sxs-lookup"><span data-stu-id="a5fd2-264">AdSchedulingPage</span></span>
<span data-ttu-id="a5fd2-265">W tym przykładzie użyto także AdSchedulerPlugin.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-265">This sample also uses the AdSchedulerPlugin.</span></span> <span data-ttu-id="a5fd2-266">Planowana trzy reklam, ad wstępne zbiorczego ad zbiorczego pośredniej i ad po zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-266">It schedules three ads, a pre-roll ad, a mid-roll ad, and a post-roll ad.</span></span> <span data-ttu-id="a5fd2-267">Identyfikator URI do VAST dla każdej usługi ad jest określona w <RemoteAdSource> elementu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-267">The URI to the VAST for each ad is specified in a <RemoteAdSource> element.</span></span>

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


### <a name="freewheelpage"></a><span data-ttu-id="a5fd2-268">FreeWheelPage</span><span class="sxs-lookup"><span data-stu-id="a5fd2-268">FreeWheelPage</span></span>
<span data-ttu-id="a5fd2-269">W przykładzie użyto FreeWheelPlugin, która określa atrybut źródłowy, który określa identyfikator URI, który wskazuje plik SmartXML, który określa ad zawartości, a także informacje o planowaniu ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-269">This sample uses the FreeWheelPlugin which specifies a Source attribute that specifies a URI that points to a SmartXML file that specifies ad content as well as ad scheduling information.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a><span data-ttu-id="a5fd2-270">MastPage</span><span class="sxs-lookup"><span data-stu-id="a5fd2-270">MastPage</span></span>
<span data-ttu-id="a5fd2-271">W przykładzie użyto MastSchedulerPlugin, która pozwala na użycie pliku MASZTÓW.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-271">This sample uses the MastSchedulerPlugin that allows you to use a MAST file.</span></span> <span data-ttu-id="a5fd2-272">Atrybut źródłowy określa lokalizację pliku MASZTÓW.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-272">The Source attribute specifies the location of the MAST file.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a><span data-ttu-id="a5fd2-273">ProgrammaticAdPage</span><span class="sxs-lookup"><span data-stu-id="a5fd2-273">ProgrammaticAdPage</span></span>
<span data-ttu-id="a5fd2-274">W tym przykładzie programowo współdziała z MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-274">This sample programmatically interacts with the MediaPlayer.</span></span> <span data-ttu-id="a5fd2-275">Plik ProgrammaticAdPage.xaml tworzy MediaPlayer:</span><span class="sxs-lookup"><span data-stu-id="a5fd2-275">The ProgrammaticAdPage.xaml file instantiates the MediaPlayer:</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

<span data-ttu-id="a5fd2-276">Plik ProgrammaticAdPage.xaml.cs tworzy AdHandlerPlugin dodaje TimelineMarker, aby określić ad powinna być wyświetlana, a następnie dodanie obsługi dla zdarzenia MarkerReached ładuje RemoteAdSource określenie identyfikatora URI do OGROMNYCH plików, a następnie odgrywa ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-276">The ProgrammaticAdPage.xaml.cs file creates an AdHandlerPlugin, adds a TimelineMarker to specify when an ad should be displayed, and then adds a handler for the MarkerReached event which loads a RemoteAdSource specifying a URI to a VAST file, and then plays the ad.</span></span>

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

### <a name="scheduleclippage"></a><span data-ttu-id="a5fd2-277">ScheduleClipPage</span><span class="sxs-lookup"><span data-stu-id="a5fd2-277">ScheduleClipPage</span></span>
<span data-ttu-id="a5fd2-278">W przykładzie użyto AdSchedulerPlugin można zaplanować ad pośredniej zbiorczego, określając plik wmv, który zawiera usługi ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-278">This sample uses the AdSchedulerPlugin to schedule a mid-roll ad by specifying a .wmv file that contains the ad.</span></span>

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

### <a name="vastlinearcompanionpage"></a><span data-ttu-id="a5fd2-279">VastLinearCompanionPage</span><span class="sxs-lookup"><span data-stu-id="a5fd2-279">VastLinearCompanionPage</span></span>
<span data-ttu-id="a5fd2-280">W tym przykładzie przedstawiono metodę zastosowania AdSchedulerPlugin można zaplanować pośredniej zbiorczego liniowej usługi ad z usługą Active Directory pomocnika.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-280">This sample illustrates how to use the AdSchedulerPlugin to schedule a mid-roll linear ad with an companion ad.</span></span> <span data-ttu-id="a5fd2-281"><RemoteAdSource> Element określa lokalizację pliku PRZEWAŻAJĄCA.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-281">The <RemoteAdSource> element specifies the location of the VAST file.</span></span>

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

### <a name="vastlinearnonlinearpage"></a><span data-ttu-id="a5fd2-282">VastLinearNonLinearPage</span><span class="sxs-lookup"><span data-stu-id="a5fd2-282">VastLinearNonLinearPage</span></span>
<span data-ttu-id="a5fd2-283">W przykładzie użyto AdSchedulerPlugin można zaplanować liniowej i inne usługi ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-283">This sample uses the AdSchedulerPlugin to schedule a linear and a non-linear ad.</span></span> <span data-ttu-id="a5fd2-284">Lokalizacja pliku PRZEWAŻAJĄCA zostanie określony z <RemoteAdSource> elementu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-284">The VAST file location is specified with the <RemoteAdSource> element.</span></span>

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

### <a name="vmappage"></a><span data-ttu-id="a5fd2-285">VMAPPage</span><span class="sxs-lookup"><span data-stu-id="a5fd2-285">VMAPPage</span></span>
<span data-ttu-id="a5fd2-286">Przykłady tego używa VmapSchedulerPlugin można zaplanować przy użyciu pliku VMAP reklam.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-286">This samples uses the VmapSchedulerPlugin to schedule ads using a VMAP file.</span></span> <span data-ttu-id="a5fd2-287">Identyfikator URI do pliku VMAP jest określony w atrybucie źródła <VmapSchedulerPlugin> elementu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-287">The URI to the VMAP file is specified in the Source attribute of the <VmapSchedulerPlugin> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a><span data-ttu-id="a5fd2-288">Implementacja systemu iOS odtwarzacza wideo z obsługą usługi Ad</span><span class="sxs-lookup"><span data-stu-id="a5fd2-288">Implementing an iOS Video Player with Ad Support</span></span>
<span data-ttu-id="a5fd2-289">Platforma Microsoft Media: Framework odtwarzacza dla systemu iOS zawiera kolekcję przykładowej aplikacji, które opisano sposób wdrożenia aplikacji odtwarzacza wideo, za pomocą środowiska.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-289">The Microsoft Media Platform: Player Framework for iOS contains a collection of sample applications that show you how to implement a video player application using the framework.</span></span> <span data-ttu-id="a5fd2-290">Możesz pobrać Player Framework i przykłady z [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="a5fd2-290">You can download the Player Framework and the samples from [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span></span> <span data-ttu-id="a5fd2-291">Strona github zawiera łącze do stron typu Wiki, zawierający dodatkowe informacje w ramach odtwarzacza i wprowadzenie do przykładu player: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="a5fd2-291">The github page has a link to a Wiki that contains additional information on the player framework and an introduction to the player sample: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span></span>

### <a name="scheduling-ads-with-vmap"></a><span data-ttu-id="a5fd2-292">Planowanie reklam z VMAP</span><span class="sxs-lookup"><span data-stu-id="a5fd2-292">Scheduling Ads with VMAP</span></span>
<span data-ttu-id="a5fd2-293">Poniższy przykład przedstawia sposób tworzenia harmonogramu przy użyciu pliku VMAP reklam.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-293">The following example shows how to schedule ads using a VMAP file.</span></span>

    // How to schedule an Ad using VMAP.
    //First download the VMAP manifest

    if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVMAP.xml"]])
            {
                [self logFrameworkError];
            }
            else
            {
                // Schedule a list of ads using the downloaded VMAP manifest
                if (![framework scheduleVMAPWithManifest:manifest])
                {
                    [self logFrameworkError];
                }          
            }

### <a name="scheduling-ads-with-vast"></a><span data-ttu-id="a5fd2-294">Planowanie reklam z VAST</span><span class="sxs-lookup"><span data-stu-id="a5fd2-294">Scheduling Ads with VAST</span></span>
<span data-ttu-id="a5fd2-295">Poniższy przykład pokazuje, jak można zaplanować późne wiązanie PRZEWAŻAJĄCA ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-295">The following sample shows how to schedule a late binding VAST ad.</span></span>

    //Example:3 How to schedule a late binding VAST ad.
    // set the start time for the ad
    adLinearTime.startTime = 13;
    adLinearTime.duration = 0;
    // Specify the URI of the VAST file
    NSString *vastAd1=@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml";
    // Create an AdInfo object
     AdInfo *vastAdInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URL to VAST file
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

   <span data-ttu-id="a5fd2-296">Poniższy przykład pokazuje, jak można zaplanować wczesne ad PRZEWAŻAJĄCA powiązania.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-296">The following sample shows how to schedule an early binding VAST ad.</span></span>
<span data-ttu-id="a5fd2-297">Przykład: 4 harmonogram wczesnego wiązania PRZEWAŻAJĄCA ad //Download VAST plik, jeśli (! [[ framework.adResolver downloadManifest: & manifestu withURL: [URLWithString nsurl OCZEKIWANEGO: @"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) {[self logFrameworkError];} else {adLinearTime.startTime = 7; adLinearTime.duration = 0;</span><span class="sxs-lookup"><span data-stu-id="a5fd2-297">//Example:4 Schedule an early binding VAST ad //Download the VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span></span>

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

<span data-ttu-id="a5fd2-298">Poniższy przykład przedstawia sposób wstawiania ad za pomocą nierównej Wytnij edycji (rz)</span><span class="sxs-lookup"><span data-stu-id="a5fd2-298">The following sample shows how to insert an ad using Rough Cut Editing (RCE)</span></span>

    //Example:1 How to use RCE.
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

<span data-ttu-id="a5fd2-299">Poniższy przykład przedstawia sposób tworzenia harmonogramu pod ad.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-299">The following example shows how to schedule an ad pod.</span></span>

    //Example:5 Schedule an ad Pod.
    // Set start time for ad
    adLinearTime.startTime = 23;
    adLinearTime.duration = 0;

    // Specify URL to content
    NSString *adpodSt1=@"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    // Create an AdInfo instance
    AdInfo *adpodInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URI to ad content
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

<span data-ttu-id="a5fd2-300">Poniższy przykład pokazuje, jak można zaplanować-trwałe ad pośredniej zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-300">The following example shows how to schedule a non-sticky mid-roll ad.</span></span> <span data-ttu-id="a5fd2-301">Ad trwałe tylko zostanie odtworzony po niezależnie od wszelkich znalezienia wykonuje przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-301">A non-sticky ad is only played once regardless of any seeking the viewer performs.</span></span>

    //Example:6 Schedule a single non sticky mid roll Ad
    // specify URL to content
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

<span data-ttu-id="a5fd2-302">Poniższy przykład pokazuje, jak można zaplanować jego umocowania ad pośredniej zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-302">The following example shows how to schedule a sticky mid-roll ad.</span></span> <span data-ttu-id="a5fd2-303">Trwałe ad będą wyświetlane zawsze, gdy zostanie osiągnięty określonego punktu w wideo na osi czasu.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-303">A sticky ad will be displayed each time the specified point on the video timeline is reached.</span></span>

    //Example:7 Schedule a single sticky mid roll Ad
    NSString *stickyAd=@"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *stickyAdInfo = [[[AdInfo alloc] init] autorelease];
    // set URI to ad
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


<span data-ttu-id="a5fd2-304">Poniższy przykład pokazuje, jak można zaplanować ad końcu pliku.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-304">The following sample shows how to schedule a post-roll ad.</span></span>

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

<span data-ttu-id="a5fd2-305">Poniższy przykład pokazuje, jak można zaplanować ad wstępne zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-305">The following sample shows how to schedule a pre-roll ad.</span></span>

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

<span data-ttu-id="a5fd2-306">Poniższy przykład pokazuje, jak można zaplanować ad nakładki pośredniej zbiorczego.</span><span class="sxs-lookup"><span data-stu-id="a5fd2-306">The following sample shows how to schedule a mid-roll overlay ad.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="a5fd2-307">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="a5fd2-307">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a5fd2-308">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="a5fd2-308">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="a5fd2-309">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a5fd2-309">See Also</span></span>
[<span data-ttu-id="a5fd2-310">Opracowywanie aplikacji odtwarzacza wideo</span><span class="sxs-lookup"><span data-stu-id="a5fd2-310">Develop video player applications</span></span>](media-services-develop-video-players.md)

