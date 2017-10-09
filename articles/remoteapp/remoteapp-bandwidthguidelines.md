---
title: "przepustowość sieci trybu RemoteApp aaaAzure — ogólne wytyczne | Dokumentacja firmy Microsoft"
description: "Zrozumienie wskazówki przepustowości sieci podstawowej dla kolekcji usługi Azure RemoteApp i aplikacji."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a><span data-ttu-id="9fcfb-103">Azure RemoteApp przepustowość sieci — ogólne wytyczne (Jeśli użytkownik nie może przetestować własnych)</span><span class="sxs-lookup"><span data-stu-id="9fcfb-103">Azure RemoteApp network bandwidth - general guidelines (if you can't test your own)</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9fcfb-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="9fcfb-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9fcfb-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="9fcfb-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9fcfb-106">Jeśli nie masz hello czas lub możliwości hello toorun [testy przepustowości sieci](remoteapp-bandwidthtests.md) usługi Azure RemoteApp, poniżej przedstawiono kilka wskazówek dość ogólny, które mogą ułatwić oszacowanie przepustowość sieci dla poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9fcfb-106">If you do not have hello time or capability toorun hello [network bandwidth tests](remoteapp-bandwidthtests.md) for Azure RemoteApp, here are some fairly generic guidelines that can help you estimate network bandwidth per user.</span></span>

<span data-ttu-id="9fcfb-107">Jeśli masz kombinację tych scenariuszy, nie zaleca się niczego najwyżej (do) 10 MB/s jako hello minimalnej przepustowości dla nowoczesnych aplikacji podłączonej do Internetu w środowisku zdalnym.</span><span class="sxs-lookup"><span data-stu-id="9fcfb-107">If you have a mix of these scenarios, we don't recommend anything less than (or equal to) 10 MB/s as hello MINIMUM network bandwidth for modern Internet-connected apps in a remote environment.</span></span> <span data-ttu-id="9fcfb-108">(Mimo że zgodnie z opisem, nie gwarantuje to lepiej niż średni użytkowników.)</span><span class="sxs-lookup"><span data-stu-id="9fcfb-108">(Although, as discussed, this will not guarantee a better than average user experience.)</span></span>

## <a name="complex-powerpoint-simple-powerpoint"></a><span data-ttu-id="9fcfb-109">PowerPoint złożonych, prosty programu PowerPoint</span><span class="sxs-lookup"><span data-stu-id="9fcfb-109">Complex PowerPoint, simple PowerPoint</span></span>
<span data-ttu-id="9fcfb-110">Usługa Azure RemoteApp jest najlepiej w sieci LAN 100 MB.</span><span class="sxs-lookup"><span data-stu-id="9fcfb-110">Azure RemoteApp does best on 100 MB LAN.</span></span> <span data-ttu-id="9fcfb-111">W hello 10 MB/s profilu sieci, gdy zakłócenia powyżej 120 ms jest większa niż % 5, hello użytkownika zostanie wyświetlony średni środowisko.</span><span class="sxs-lookup"><span data-stu-id="9fcfb-111">At hello 10 MB/s network profile, when jitter above 120 ms is more than 5%, hello user will see an average experience.</span></span> <span data-ttu-id="9fcfb-112">Na 1 MB/s hello różnych jest glaring — na przykład w ramach pokazu slajdów, hello użytkownika może nie być wyświetlana animowane przejścia na wszystkich ponieważ ramki są pomijane.</span><span class="sxs-lookup"><span data-stu-id="9fcfb-112">At 1 MB/s hello different is glaring - for example, in a slide show, hello user might not see animated transitions at all because frames are skipped.</span></span>

## <a name="internet-explorer-mixed-pdf-pdf-text"></a><span data-ttu-id="9fcfb-113">Mieszany programu Internet Explorer, PDF, PDF, tekst</span><span class="sxs-lookup"><span data-stu-id="9fcfb-113">Internet Explorer, mixed PDF, PDF, Text</span></span>
<span data-ttu-id="9fcfb-114">Profil sieci usługi 10 MB/s jest Zamknij tooLAN w większości aspektów.</span><span class="sxs-lookup"><span data-stu-id="9fcfb-114">10 MB/s network profile is close tooLAN in most aspects.</span></span> <span data-ttu-id="9fcfb-115">1 MB/s zapewni OK środowisko, mimo że może być niektórych zakłócenia, gdy użytkownik przewinie, gdy istnieją obrazy na ekranie powitania.</span><span class="sxs-lookup"><span data-stu-id="9fcfb-115">1 MB/s will provide an OK experience, although there may be some jitter when a user scrolls while there are images on hello screen.</span></span>

## <a name="flash-video-youtube"></a><span data-ttu-id="9fcfb-116">Flash wideo (YouTube)</span><span class="sxs-lookup"><span data-stu-id="9fcfb-116">Flash video (YouTube)</span></span>
<span data-ttu-id="9fcfb-117">100 MB/s LAN zapewnia hello najlepsze doświadczenia, gdy 10 MB/s jest dopuszczalne (znaczenie firma Microsoft nadąża z szybkość klatek hello, ale zwiększa zakłóceń).</span><span class="sxs-lookup"><span data-stu-id="9fcfb-117">100 MB/s LAN provides hello best experience, while 10 MB/s is acceptable (meaning we keep up with hello frame rate but jitter increases).</span></span> <span data-ttu-id="9fcfb-118">1 MB/s zakłócenia jest bardzo wysoka i zauważalne.</span><span class="sxs-lookup"><span data-stu-id="9fcfb-118">At 1 MB/s, jitter is very high and noticeable.</span></span>

## <a name="word-typing-word-remote-input"></a><span data-ttu-id="9fcfb-119">Wpisz (Word zdalnego danych wejściowych) w programie Word</span><span class="sxs-lookup"><span data-stu-id="9fcfb-119">Word typing (Word remote input)</span></span>
<span data-ttu-id="9fcfb-120">Jest to scenariusz użycia niskiej przepustowości.</span><span class="sxs-lookup"><span data-stu-id="9fcfb-120">This is a low-bandwidth usage scenario.</span></span> <span data-ttu-id="9fcfb-121">256 KB/s udostępniamy tak dobrze doświadczenia jako sieci LAN.</span><span class="sxs-lookup"><span data-stu-id="9fcfb-121">At 256 KB/s we provide as good of an experience as LAN.</span></span>

## <a name="learn-more"></a><span data-ttu-id="9fcfb-122">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="9fcfb-122">Learn more</span></span>
* [<span data-ttu-id="9fcfb-123">Szacowanie użycia przepustowości sieci usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="9fcfb-123">Estimate Azure RemoteApp network bandwidth usage</span></span>](remoteapp-bandwidth.md)
* [<span data-ttu-id="9fcfb-124">Usługa Azure RemoteApp — jak przepustowości sieci i jakości środowisko pracy ze sobą?</span><span class="sxs-lookup"><span data-stu-id="9fcfb-124">Azure RemoteApp - how do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="9fcfb-125">Usługa Azure RemoteApp — tseting użycie przepustowości sieci z niektórych typowych scenariuszy</span><span class="sxs-lookup"><span data-stu-id="9fcfb-125">Azure RemoteApp - tseting your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)

