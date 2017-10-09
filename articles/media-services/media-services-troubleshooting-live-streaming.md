---
title: "Transmisja strumieniowa na żywo w przewodniku aaaTroubleshooting | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera sugestie dotyczące sposobu tootroubleshoot live problemów przesyłania strumieniowego."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8549bae947ff3b225ce624220d1e48b63f90208c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="85937-103">Przewodnik rozwiązywania problemów z transmisją strumieniową na żywo</span><span class="sxs-lookup"><span data-stu-id="85937-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="85937-104">Ten temat zawiera sugestie dotyczące tootroubleshoot niektóre na żywo, przesyłanie strumieniowe problemów.</span><span class="sxs-lookup"><span data-stu-id="85937-104">This topic gives suggestions on how tootroubleshoot some live streaming problems.</span></span>

## <a name="issues-related-tooon-premises-encoders"></a><span data-ttu-id="85937-105">Problemy związane z koderów lokalnych tooon</span><span class="sxs-lookup"><span data-stu-id="85937-105">Issues related tooon-premises encoders</span></span>
<span data-ttu-id="85937-106">W tej sekcji przedstawiono sugestie dotyczące sposobu tootroubleshoot koderów pokrewne lokalnych tooon problemów, które są skonfigurowane toosend kanałami tooAMS strumienia pojedynczej szybkości transmisji bitów, obsługującymi kodowanie na żywo.</span><span class="sxs-lookup"><span data-stu-id="85937-106">This section gives suggestions on how tootroubleshoot problems related tooon-premises encoders that are configured toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-toosee-logs"></a><span data-ttu-id="85937-107">Problem: Chcieliby toosee dzienniki</span><span class="sxs-lookup"><span data-stu-id="85937-107">Problem: Would like toosee logs</span></span>
* <span data-ttu-id="85937-108">**Potencjalny problem**: nie można Znajdź kodera dzienników, która może pomóc w debugowaniu problemów.</span><span class="sxs-lookup"><span data-stu-id="85937-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="85937-109">**Telestream Wirecast**: zwykle można znaleźć dzienniki w obszarze C:\Users\{username} \AppData\Roaming\Wirecast\\</span><span class="sxs-lookup"><span data-stu-id="85937-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="85937-110">**Stanie wolnym Live**: można znaleźć ma toologs łącza na powitania portalu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="85937-110">**Elemental Live**: You can find has links toologs on hello management portal.</span></span> <span data-ttu-id="85937-111">Polecenie **Statystyka**, następnie **dzienniki**.</span><span class="sxs-lookup"><span data-stu-id="85937-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="85937-112">Na powitania **pliki dziennika** strony, zostanie wyświetlona lista dzienników dla wszystkich hello elementów LiveEvent; wybierz hello jedną dopasowania bieżącej sesji.</span><span class="sxs-lookup"><span data-stu-id="85937-112">On hello **Log Files** page, you will see a list of logs for all hello LiveEvent items; select hello one matching your current session.</span></span> 
  * <span data-ttu-id="85937-113">**Flash Media Live Encoder**: można znaleźć hello **katalog dziennika...**  przechodząc toohello **kodowanie dziennika** kartę.</span><span class="sxs-lookup"><span data-stu-id="85937-113">**Flash Media Live Encoder**: You can find hello **Log Directory...** by navigating toohello **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="85937-114">Problem: Nie jest dostępna opcja wyprowadzania progresywnego strumienia</span><span class="sxs-lookup"><span data-stu-id="85937-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="85937-115">**Potencjalny problem**: koder hello używane automatycznie nie bez przeplotu..</span><span class="sxs-lookup"><span data-stu-id="85937-115">**Potential issue**: hello encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="85937-116">**Kroki rozwiązywania problemów**: Poszukaj usuwania przeplotu opcji w interfejsie kodera hello.</span><span class="sxs-lookup"><span data-stu-id="85937-116">**Troubleshooting steps**: Look for a de-interlacing option within hello encoder interface.</span></span> <span data-ttu-id="85937-117">Po włączeniu cofnąć przeplot Sprawdź ponownie ustawienia wyjściowej progresywnego.</span><span class="sxs-lookup"><span data-stu-id="85937-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a><span data-ttu-id="85937-118">Problem: Nastąpiła kilka ustawień wyjściowej koder i tooconnect nadal nie.</span><span class="sxs-lookup"><span data-stu-id="85937-118">Problem: Tried several encoder output settings and still unable tooconnect.</span></span>
* <span data-ttu-id="85937-119">**Potencjalny problem**: Azure kodowania kanału nie zostało prawidłowo zresetowane.</span><span class="sxs-lookup"><span data-stu-id="85937-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="85937-120">**Kroki rozwiązywania problemów**: Upewnij się, że koder hello jest już wypychanie tooAMS, Zatrzymaj i zresetować hello kanału.</span><span class="sxs-lookup"><span data-stu-id="85937-120">**Troubleshooting steps**: Make sure hello encoder is no longer pushing tooAMS, stop and reset hello channel.</span></span> <span data-ttu-id="85937-121">Raz uruchomić ponownie, spróbuj się połączyć kodera hello nowe ustawienia.</span><span class="sxs-lookup"><span data-stu-id="85937-121">Once running again, try connecting your encoder with hello new settings.</span></span> <span data-ttu-id="85937-122">Jeśli to nadal nie rozwiąże problemu hello, spróbuj utworzyć nowy kanał całkowicie, czasami kanałów może zostać uszkodzony po kilku nieudanych próbach.</span><span class="sxs-lookup"><span data-stu-id="85937-122">If this still does not correct hello issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="85937-123">**Potencjalny problem**: rozmiar GOP hello lub klatki ustawienia nie są optymalne.</span><span class="sxs-lookup"><span data-stu-id="85937-123">**Potential issue**: hello GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="85937-124">**Kroki rozwiązywania problemów**: interwał rozmiaru lub klatki kluczowej GOP zalecane jest 2 sekundy.</span><span class="sxs-lookup"><span data-stu-id="85937-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="85937-125">Niektóre kodery obliczyć tego ustawienia w liczbę ramek, podczas gdy inne sekund.</span><span class="sxs-lookup"><span data-stu-id="85937-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="85937-126">Na przykład: podczas wyprowadzania 30 klatek na sekundę, hello GOP rozmiar będzie 60 klatek, która jest równoważne too2 sekund.</span><span class="sxs-lookup"><span data-stu-id="85937-126">For example: When outputting 30fps, hello GOP size would be 60 frames, which is equivalent too2 seconds.</span></span>  
* <span data-ttu-id="85937-127">**Potencjalny problem**: porty zamkniętego blokują hello strumienia.</span><span class="sxs-lookup"><span data-stu-id="85937-127">**Potential issue**: Closed ports are blocking hello stream.</span></span> 
  
    <span data-ttu-id="85937-128">**Kroki rozwiązywania problemów**: podczas przesyłania strumieniowego za pośrednictwem protokołu RTMP, sprawdź zaporę i/lub otwartych portów wychodzących 1935 i 1936 tooconfirm ustawienia serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="85937-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings tooconfirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="85937-129">Korzystając z RTP przesyłania strumieniowego, upewnij się, że jest otwarty port wychodzący 2010.</span><span class="sxs-lookup"><span data-stu-id="85937-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a><span data-ttu-id="85937-130">Problem: Podczas konfigurowania hello koder toostream z hello protokołu RTP, brak miejsca tooenter nazwę hosta.</span><span class="sxs-lookup"><span data-stu-id="85937-130">Problem: When configuring hello encoder toostream with hello RTP protocol, there is no place tooenter a host name.</span></span>
* <span data-ttu-id="85937-131">**Potencjalny problem**: wiele RTP kodery nie zezwalaj na dla nazwy hosta i adresu IP, należy uzyskać toobe.</span><span class="sxs-lookup"><span data-stu-id="85937-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need toobe acquired.</span></span>  
  
    <span data-ttu-id="85937-132">**Kroki rozwiązywania problemów**: toofind hello adres IP, otwórz wiersz polecenia na każdym komputerze.</span><span class="sxs-lookup"><span data-stu-id="85937-132">**Troubleshooting steps**: toofind hello IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="85937-133">toodo to w systemie Windows, otwórz hello uruchamiania wykonywania (WIN + R), a następnie wpisz tooopen "cmd".</span><span class="sxs-lookup"><span data-stu-id="85937-133">toodo this in Windows, open hello Run launcher (WIN + R) and type “cmd” tooopen.</span></span>  
  
    <span data-ttu-id="85937-134">Po otwarciu hello wiersza polecenia, wpisz "Ping [nazwa hosta AMS]".</span><span class="sxs-lookup"><span data-stu-id="85937-134">Once hello command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="85937-135">Nazwa hosta Hello mogą pochodzić, pomijając hello numer portu z hello adresu URL pozyskiwania Azure, jako wyróżniane na powitania poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="85937-135">hello host name can be derived by omitting hello port number from hello Azure Ingest URL, as highlighted in hello following example:</span></span> 
  
    <span data-ttu-id="85937-136">RTP://Test2-amstest009.RTP.Channel.mediaservices.Windows.NET:2010 /</span><span class="sxs-lookup"><span data-stu-id="85937-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="85937-138">Jeśli po wykonaniu hello kroki rozwiązywania problemów, które nadal nie można pomyślnie przesyłania strumieniowego, należy przesłać biletu pomocy technicznej za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="85937-138">If after following hello troubleshooting steps you still cannot successfully stream, submit a support ticket using hello Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="85937-139">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="85937-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="85937-140">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="85937-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

