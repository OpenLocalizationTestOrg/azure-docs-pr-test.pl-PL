---
title: "Transmisja strumieniowa na żywo podręczniku rozwiązywania problemów | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera sugestie dotyczące rozwiązywania problemów transmisji strumieniowej na żywo."
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
ms.openlocfilehash: fa91baf7c494941fccf0e6ca38b930f3c2a521ce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="caee3-103">Przewodnik rozwiązywania problemów z transmisją strumieniową na żywo</span><span class="sxs-lookup"><span data-stu-id="caee3-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="caee3-104">Ten temat zawiera sugestie dotyczące rozwiązywania problemów, transmisji strumieniowej na żywo.</span><span class="sxs-lookup"><span data-stu-id="caee3-104">This topic gives suggestions on how to troubleshoot some live streaming problems.</span></span>

## <a name="issues-related-to-on-premises-encoders"></a><span data-ttu-id="caee3-105">Problemy związane z koderów lokalnych</span><span class="sxs-lookup"><span data-stu-id="caee3-105">Issues related to on-premises encoders</span></span>
<span data-ttu-id="caee3-106">W tej sekcji przedstawiono sugestie dotyczące rozwiązywania problemów związanych z koderów lokalnych, które są skonfigurowane do wysyłania do kanałów AMS, które są włączone dla kodowanie na żywo o pojedynczej szybkości transmisji.</span><span class="sxs-lookup"><span data-stu-id="caee3-106">This section gives suggestions on how to troubleshoot problems related to on-premises encoders that are configured to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-to-see-logs"></a><span data-ttu-id="caee3-107">Problem: Chcesz zobaczyć dzienniki</span><span class="sxs-lookup"><span data-stu-id="caee3-107">Problem: Would like to see logs</span></span>
* <span data-ttu-id="caee3-108">**Potencjalny problem**: nie można Znajdź kodera dzienników, która może pomóc w debugowaniu problemów.</span><span class="sxs-lookup"><span data-stu-id="caee3-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="caee3-109">**Telestream Wirecast**: zwykle można znaleźć dzienniki w obszarze C:\Users\{username} \AppData\Roaming\Wirecast\\</span><span class="sxs-lookup"><span data-stu-id="caee3-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="caee3-110">**Stanie wolnym Live**: można znaleźć zawiera łącza do dzienników w portalu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="caee3-110">**Elemental Live**: You can find has links to logs on the management portal.</span></span> <span data-ttu-id="caee3-111">Polecenie **Statystyka**, następnie **dzienniki**.</span><span class="sxs-lookup"><span data-stu-id="caee3-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="caee3-112">Na **pliki dziennika** strony, zostanie wyświetlona lista dzienników dla wszystkich elementów LiveEvent; wybierz jedną dopasowania bieżącej sesji.</span><span class="sxs-lookup"><span data-stu-id="caee3-112">On the **Log Files** page, you will see a list of logs for all the LiveEvent items; select the one matching your current session.</span></span> 
  * <span data-ttu-id="caee3-113">**Flash Media Live Encoder**: można znaleźć **katalog dziennika...**  przechodząc do **kodowanie dziennika** kartę.</span><span class="sxs-lookup"><span data-stu-id="caee3-113">**Flash Media Live Encoder**: You can find the **Log Directory...** by navigating to the **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="caee3-114">Problem: Nie jest dostępna opcja wyprowadzania progresywnego strumienia</span><span class="sxs-lookup"><span data-stu-id="caee3-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="caee3-115">**Potencjalny problem**: koder używany nie zostać automatycznie bez przeplotu.</span><span class="sxs-lookup"><span data-stu-id="caee3-115">**Potential issue**: The encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="caee3-116">**Kroki rozwiązywania problemów**: Poszukaj usuwania przeplotu opcji w interfejsie kodera.</span><span class="sxs-lookup"><span data-stu-id="caee3-116">**Troubleshooting steps**: Look for a de-interlacing option within the encoder interface.</span></span> <span data-ttu-id="caee3-117">Po włączeniu cofnąć przeplot Sprawdź ponownie ustawienia wyjściowej progresywnego.</span><span class="sxs-lookup"><span data-stu-id="caee3-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-to-connect"></a><span data-ttu-id="caee3-118">Problem: Nastąpiła kilka ustawień wyjściowej koder i nadal nie można nawiązać połączenia.</span><span class="sxs-lookup"><span data-stu-id="caee3-118">Problem: Tried several encoder output settings and still unable to connect.</span></span>
* <span data-ttu-id="caee3-119">**Potencjalny problem**: Azure kodowania kanału nie zostało prawidłowo zresetowane.</span><span class="sxs-lookup"><span data-stu-id="caee3-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="caee3-120">**Kroki rozwiązywania problemów**: Upewnij się, że koder jest już Wypychanie do AMS, Zatrzymaj i zresetować kanału.</span><span class="sxs-lookup"><span data-stu-id="caee3-120">**Troubleshooting steps**: Make sure the encoder is no longer pushing to AMS, stop and reset the channel.</span></span> <span data-ttu-id="caee3-121">Raz uruchomić ponownie, spróbuj się połączyć kodera przy użyciu nowych ustawień.</span><span class="sxs-lookup"><span data-stu-id="caee3-121">Once running again, try connecting your encoder with the new settings.</span></span> <span data-ttu-id="caee3-122">Jeśli to nadal nie rozwiąże problemu, spróbuj utworzyć nowy kanał całkowicie, czasami kanałów może zostać uszkodzony po kilku nieudanych próbach.</span><span class="sxs-lookup"><span data-stu-id="caee3-122">If this still does not correct the issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="caee3-123">**Potencjalny problem**: rozmiar GOP lub klatki ustawienia nie są optymalne.</span><span class="sxs-lookup"><span data-stu-id="caee3-123">**Potential issue**: The GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="caee3-124">**Kroki rozwiązywania problemów**: interwał rozmiaru lub klatki kluczowej GOP zalecane jest 2 sekundy.</span><span class="sxs-lookup"><span data-stu-id="caee3-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="caee3-125">Niektóre kodery obliczyć tego ustawienia w liczbę ramek, podczas gdy inne sekund.</span><span class="sxs-lookup"><span data-stu-id="caee3-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="caee3-126">Na przykład: podczas wyprowadzania 30 klatek na sekundę, rozmiar GOP byłoby 60 ramki, który jest odpowiednikiem 2 sekundy.</span><span class="sxs-lookup"><span data-stu-id="caee3-126">For example: When outputting 30fps, the GOP size would be 60 frames, which is equivalent to 2 seconds.</span></span>  
* <span data-ttu-id="caee3-127">**Potencjalny problem**: blokuje porty zamkniętego strumienia.</span><span class="sxs-lookup"><span data-stu-id="caee3-127">**Potential issue**: Closed ports are blocking the stream.</span></span> 
  
    <span data-ttu-id="caee3-128">**Kroki rozwiązywania problemów**: podczas przesyłania strumieniowego za pośrednictwem protokołu RTMP, sprawdź ustawienia zapory i/lub serwera proxy, aby upewnić się, że porty wyjściowe 1935 i 1936 są otwarte.</span><span class="sxs-lookup"><span data-stu-id="caee3-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings to confirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="caee3-129">Korzystając z RTP przesyłania strumieniowego, upewnij się, że jest otwarty port wychodzący 2010.</span><span class="sxs-lookup"><span data-stu-id="caee3-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-the-encoder-to-stream-with-the-rtp-protocol-there-is-no-place-to-enter-a-host-name"></a><span data-ttu-id="caee3-130">Problem: Konfigurowanie kodera do strumienia przy użyciu protokołu RTP, nie ma żadnych miejscu wprowadź nazwę hosta.</span><span class="sxs-lookup"><span data-stu-id="caee3-130">Problem: When configuring the encoder to stream with the RTP protocol, there is no place to enter a host name.</span></span>
* <span data-ttu-id="caee3-131">**Potencjalny problem**: wiele RTP kodery nie zezwalaj na dla nazwy hosta i adresu IP musi zostać pobrany.</span><span class="sxs-lookup"><span data-stu-id="caee3-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need to be acquired.</span></span>  
  
    <span data-ttu-id="caee3-132">**Kroki rozwiązywania problemów**: Aby znaleźć adres IP, otwórz wiersz polecenia na każdym komputerze.</span><span class="sxs-lookup"><span data-stu-id="caee3-132">**Troubleshooting steps**: To find the IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="caee3-133">Aby to zrobić w systemie Windows, otwórz uruchamiania wykonywania (WIN + R), a następnie wpisz "cmd" Aby otworzyć.</span><span class="sxs-lookup"><span data-stu-id="caee3-133">To do this in Windows, open the Run launcher (WIN + R) and type “cmd” to open.</span></span>  
  
    <span data-ttu-id="caee3-134">Po otwarciu w wierszu polecenia wpisz "Ping [nazwa hosta AMS]".</span><span class="sxs-lookup"><span data-stu-id="caee3-134">Once the command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="caee3-135">Nazwa hosta mogą być uzyskane, pomijając numer portu z Azure adresu URL pozyskiwania, jak w poniższym przykładzie wyróżniono:</span><span class="sxs-lookup"><span data-stu-id="caee3-135">The host name can be derived by omitting the port number from the Azure Ingest URL, as highlighted in the following example:</span></span> 
  
    <span data-ttu-id="caee3-136">RTP://Test2-amstest009.RTP.Channel.mediaservices.Windows.NET:2010 /</span><span class="sxs-lookup"><span data-stu-id="caee3-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="caee3-138">Jeśli po wykonaniu kroków, które nadal nie można pomyślnie przesyłania strumieniowego, należy przesłać biletu pomocy technicznej przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="caee3-138">If after following the troubleshooting steps you still cannot successfully stream, submit a support ticket using the Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="caee3-139">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="caee3-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="caee3-140">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="caee3-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

