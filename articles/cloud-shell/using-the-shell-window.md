---
title: "okna powłoki chmury Azure (wersja zapoznawcza) hello aaaUsing | Dokumentacja firmy Microsoft"
description: "Okna powłoki chmury Azure hello wskazówki."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: juluk
ms.openlocfilehash: 571db3c8e177799a9e05f38a7cf8d2a4d5f8c8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cloud-shell-window"></a><span data-ttu-id="8396a-103">Przy użyciu okna powłoki chmury Azure hello</span><span class="sxs-lookup"><span data-stu-id="8396a-103">Using hello Azure Cloud Shell window</span></span>

<span data-ttu-id="8396a-104">W tym dokumencie opisano, jak toouse hello okna powłoki chmury.</span><span class="sxs-lookup"><span data-stu-id="8396a-104">This document explains how toouse hello Cloud Shell window.</span></span>

## <a name="concurrent-sessions"></a><span data-ttu-id="8396a-105">Równoczesnych sesji</span><span class="sxs-lookup"><span data-stu-id="8396a-105">Concurrent sessions</span></span>
<span data-ttu-id="8396a-106">Zezwalając tooexist każdej sesji procesów odrębnych Bash w chmurze powłoki umożliwia wielu równoczesnych sesji na kartach przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="8396a-106">Cloud Shell enables multiple concurrent sessions across browser tabs by allowing each session tooexist as a separate Bash process.</span></span>
<span data-ttu-id="8396a-107">Jeśli kończenie sesji, upewnij się, tooexit z okna każdej sesji jako każdy proces przebiega niezależnie, chociaż są uruchamiane w hello sam maszyny.</span><span class="sxs-lookup"><span data-stu-id="8396a-107">If exiting a session, be sure tooexit from each session window as each process runs independently although they run on hello same machine.</span></span>

## <a name="restart-cloud-shell"></a><span data-ttu-id="8396a-108">Ponownie uruchom powłokę chmury</span><span class="sxs-lookup"><span data-stu-id="8396a-108">Restart Cloud Shell</span></span>
![](media/recycle.png)
> [!WARNING]
> <span data-ttu-id="8396a-109">Ponowne uruchamianie powłoki chmurze spowoduje zresetowanie stan maszyny i wszystkie pliki nie utrwalone przez plik udziału zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="8396a-109">Restarting Cloud Shell will reset machine state and any files not persisted by your file share will be lost.</span></span>

* <span data-ttu-id="8396a-110">Kliknij ikonę ponownego uruchomienia hello na powitania narzędzi tooreceive nowego środowiska chmury powłoki.</span><span class="sxs-lookup"><span data-stu-id="8396a-110">Click hello restart icon on hello toolbar tooreceive a new Cloud Shell environment.</span></span>

## <a name="minimize--maximize-cloud-shell-window"></a><span data-ttu-id="8396a-111">Minimalizowanie & maksymalizowanie okna powłoki chmury</span><span class="sxs-lookup"><span data-stu-id="8396a-111">Minimize & maximize Cloud Shell window</span></span>
![](media/minmax.png)
* <span data-ttu-id="8396a-112">Kliknij przycisk hello zminimalizować ikonę na powitania górnego prawego powitalne okno toohide go.</span><span class="sxs-lookup"><span data-stu-id="8396a-112">Click hello minimize icon on hello top right of hello window toohide it.</span></span> <span data-ttu-id="8396a-113">Ponownie kliknij przycisk hello ikona powłoki chmury toounhide.</span><span class="sxs-lookup"><span data-stu-id="8396a-113">Click hello Cloud Shell icon again toounhide.</span></span>
* <span data-ttu-id="8396a-114">Kliknij przycisk hello zmaksymalizować wysokość toomax okna tooset ikony.</span><span class="sxs-lookup"><span data-stu-id="8396a-114">Click hello maximize icon tooset window toomax height.</span></span> <span data-ttu-id="8396a-115">tooprevious okna toorestore rozmiar, kliknij przycisk Przywróć.</span><span class="sxs-lookup"><span data-stu-id="8396a-115">toorestore window tooprevious size, click restore.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="8396a-116">Kopiowanie i wklejanie</span><span class="sxs-lookup"><span data-stu-id="8396a-116">Copy and paste</span></span>
* <span data-ttu-id="8396a-117">System Windows: `Ctrl-insert` toocopy i `Shift-insert` toopaste.</span><span class="sxs-lookup"><span data-stu-id="8396a-117">Windows: `Ctrl-insert` toocopy and `Shift-insert` toopaste.</span></span> <span data-ttu-id="8396a-118">Kliknij prawym przyciskiem myszy listy rozwijanej można również włączyć kopiowania i wklejania.</span><span class="sxs-lookup"><span data-stu-id="8396a-118">Right-click dropdown can also enable copy/paste.</span></span>
  * <span data-ttu-id="8396a-119">FireFox/IE może obsługuje uprawnienia do Schowka.</span><span class="sxs-lookup"><span data-stu-id="8396a-119">FireFox/IE may not support clipboard permissions properly.</span></span>
* <span data-ttu-id="8396a-120">System Mac OS: `Cmd-c` toocopy i `Cmd-v` toopaste.</span><span class="sxs-lookup"><span data-stu-id="8396a-120">Mac OS: `Cmd-c` toocopy and `Cmd-v` toopaste.</span></span> <span data-ttu-id="8396a-121">Kliknij prawym przyciskiem myszy listy rozwijanej można również włączyć kopiowania i wklejania.</span><span class="sxs-lookup"><span data-stu-id="8396a-121">Right-click dropdown can also enable copy/paste.</span></span>

## <a name="resize-cloud-shell-window"></a><span data-ttu-id="8396a-122">Zmień rozmiar okna powłoki chmury</span><span class="sxs-lookup"><span data-stu-id="8396a-122">Resize Cloud Shell window</span></span>
* <span data-ttu-id="8396a-123">Kliknij i przeciągnij hello górnej krawędzi paska narzędzi hello w górę lub w dół okna powłoki chmury hello tooresize.</span><span class="sxs-lookup"><span data-stu-id="8396a-123">Click and drag hello top edge of hello toolbar up or down tooresize hello Cloud Shell window.</span></span>

## <a name="scrolling-text-display"></a><span data-ttu-id="8396a-124">Przewijanie wyświetlanej tekstu</span><span class="sxs-lookup"><span data-stu-id="8396a-124">Scrolling text display</span></span>
* <span data-ttu-id="8396a-125">Przewiń do myszy lub dotykową toomove terminali tekstu.</span><span class="sxs-lookup"><span data-stu-id="8396a-125">Scroll with your mouse or touchpad toomove terminal text.</span></span>

## <a name="exit-command"></a><span data-ttu-id="8396a-126">Exit — polecenie</span><span class="sxs-lookup"><span data-stu-id="8396a-126">Exit command</span></span>
<span data-ttu-id="8396a-127">Uruchomiona `exit` kończy hello aktywnej sesji.</span><span class="sxs-lookup"><span data-stu-id="8396a-127">Running `exit` terminates hello active session.</span></span> <span data-ttu-id="8396a-128">Dzieje się tak domyślnie po upływie 20 minut bez interakcji.</span><span class="sxs-lookup"><span data-stu-id="8396a-128">This behavior occurs by default after 20 minutes without interaction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8396a-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8396a-129">Next steps</span></span>
[<span data-ttu-id="8396a-130">Szybki Start powłoki chmury</span><span class="sxs-lookup"><span data-stu-id="8396a-130">Cloud Shell Quickstart</span></span>](quickstart.md)
