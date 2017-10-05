---
title: "Zawartość zestawu SDK aplikacji uniwersalnych systemu Windows"
description: "Dowiedz się więcej o zawartość zestawu SDK systemu Windows uniwersalnej aplikacji dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8fa1b701-1c2b-4aec-940c-06c974ef5405
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b28d525ab16487b963772e23fdecd11f94dcabd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-content"></a><span data-ttu-id="7183d-103">Zawartość zestawu SDK aplikacji uniwersalnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="7183d-103">Windows Universal Apps SDK content</span></span>
<span data-ttu-id="7183d-104">Ten dokument wymieniono i opisano zawartości wdrożone przez zestaw SDK aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7183d-104">This document lists and describes the content deployed by the SDK in your application.</span></span>

## <a name="the-resources-folder"></a><span data-ttu-id="7183d-105">`/Resources` Folderu</span><span class="sxs-lookup"><span data-stu-id="7183d-105">The `/Resources` folder</span></span>
<span data-ttu-id="7183d-106">Ten folder zawiera wszystkie zasoby, które wymaga usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7183d-106">This folder contains all the resources that Mobile Engagement needs.</span></span> <span data-ttu-id="7183d-107">Można również dostosować je do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7183d-107">You can also customize them to fit your app.</span></span>

* <span data-ttu-id="7183d-108">`EngagementConfiguration.xml`Plik konfiguracji Mobile Engagement, jest to, gdzie można dostosować ustawienia usługi Mobile Engagement (parametry połączenia usługi Mobile Engagement, awarii raportu...).</span><span class="sxs-lookup"><span data-stu-id="7183d-108">`EngagementConfiguration.xml` : The Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span></span>

### <a name="html-folder"></a><span data-ttu-id="7183d-109">folder polecenia</span><span class="sxs-lookup"><span data-stu-id="7183d-109">/html folder</span></span>
* <span data-ttu-id="7183d-110">`EngagementNotification.html`: `Notification` Widok html projektu dla transparentach w aplikacji w sieci web.</span><span class="sxs-lookup"><span data-stu-id="7183d-110">`EngagementNotification.html` : The `Notification` web view html design for in-app banners.</span></span>
* <span data-ttu-id="7183d-111">`EngagementAnnouncement.html`: `Announcement` Widoku projektowanie html w aplikacji międzysegmentowe widoków witryn sieci web.</span><span class="sxs-lookup"><span data-stu-id="7183d-111">`EngagementAnnouncement.html` : The `Announcement` web view html design for in-app interstitial views.</span></span>

### <a name="images-folder"></a><span data-ttu-id="7183d-112">/images folder</span><span class="sxs-lookup"><span data-stu-id="7183d-112">/images folder</span></span>
* <span data-ttu-id="7183d-113">`EngagementIconNotification.png`: Brand ikona wyświetlana po lewej stronie powiadomienia, Zastąp to jedno z ikoną marki.</span><span class="sxs-lookup"><span data-stu-id="7183d-113">`EngagementIconNotification.png` : The brand icon displayed at the left of a notification, replace this one by your brand icon.</span></span>
* <span data-ttu-id="7183d-114">`EngagementIconOk.png`: `Ok` Ikona zasięgu zawartości stron dla przycisku akcji lub sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="7183d-114">`EngagementIconOk.png` : The `Ok` icon of the reach content pages for the action or validation button.</span></span>
* <span data-ttu-id="7183d-115">`EngagementIconNOK.png`: `NOK` Ikona przycisk weryfikacji zawartości stron w zasięgu jest wyłączony.</span><span class="sxs-lookup"><span data-stu-id="7183d-115">`EngagementIconNOK.png` : The `NOK` icon used when the validation button of the reach content pages is disabled.</span></span>
* <span data-ttu-id="7183d-116">`EngagementIconClose.png`: `Close` Ikony powiadomień reach i zawartość dla przycisku odrzucenia.</span><span class="sxs-lookup"><span data-stu-id="7183d-116">`EngagementIconClose.png` : The `Close` icon of the reach notifications and contents for the dismiss button.</span></span>

### <a name="overlay-folder"></a><span data-ttu-id="7183d-117">/overlay folder</span><span class="sxs-lookup"><span data-stu-id="7183d-117">/overlay folder</span></span>
* <span data-ttu-id="7183d-118">`EngagementPageOverlay.cs`Strona nakładki odpowiedzialny za dodawanie stopnia zaangażowania osiągnąć w aplikacji interfejsu użytkownika Służącego do jej podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="7183d-118">`EngagementPageOverlay.cs` : The overlay page responsible for adding the Engagement reach in-app UI to its child.</span></span>

