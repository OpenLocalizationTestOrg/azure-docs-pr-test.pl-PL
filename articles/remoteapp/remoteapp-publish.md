---
title: "aaaPublish aplikacji w usłudze Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toopublish aplikacji i zasobów w usłudze Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a><span data-ttu-id="15518-103">Jak toopublish aplikacji w usłudze RemoteApp</span><span class="sxs-lookup"><span data-stu-id="15518-103">How toopublish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="15518-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="15518-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="15518-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="15518-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="15518-106">Po utworzeniu kolekcji usługi RemoteApp, potrzebujesz aplikacji hello toopublish lub zasoby, które chcesz toomake dostępne dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="15518-106">After you create your RemoteApp collection, you need toopublish hello apps or resources that you want toomake available for your users.</span></span> <span data-ttu-id="15518-107">Witaj obrazy szablonów zapewnionej w ramach subskrypcji mieć tylko kilka aplikacji opublikowanych przez domyślnie — tooshare hello inne aplikacje, należy toopublish je.</span><span class="sxs-lookup"><span data-stu-id="15518-107">hello template images provided with your subscription only have a few apps published by default - tooshare hello other apps, you need toopublish them.</span></span>

> [!NOTE]
> <span data-ttu-id="15518-108">Potrzebujesz tooupdate aplikacji?</span><span class="sxs-lookup"><span data-stu-id="15518-108">Do you need tooupdate an app?</span></span> <span data-ttu-id="15518-109">Będziesz potrzebować zbyt[obraz powitania aktualizacji](remoteapp-update.md) pierwszy.</span><span class="sxs-lookup"><span data-stu-id="15518-109">You'll need too[update hello image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="15518-110">Na powitania **publikowania** w portalu hello, kliknij pozycję **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="15518-110">On hello **Publishing** tab in hello portal, click **Publish**.</span></span> <span data-ttu-id="15518-111">Można dodać aplikację z obrazu szablonu **Start** menu lub podaj hello ścieżki toowhere hello aplikacja jest zainstalowana na powitania obrazu szablonu.</span><span class="sxs-lookup"><span data-stu-id="15518-111">You can either add an app from your template image's **Start** menu or provide hello path toowhere hello app is installed on hello template image.</span></span> <span data-ttu-id="15518-112">Jeśli wybierzesz tooadd z hello **Start** menu, wybierz z listy hello toopublish aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="15518-112">If you choose tooadd from hello **Start** menu, choose hello app toopublish from hello list.</span></span> <span data-ttu-id="15518-113">Jeśli wybierzesz tooprovide hello ścieżki toohello aplikacji, wprowadź nazwę aplikacji hello i hello ścieżki toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="15518-113">If you choose tooprovide hello path toohello app, enter a name for hello app and hello path toohello app.</span></span> <span data-ttu-id="15518-114">Używania zmiennych w ścieżce hello — na przykład "% systemdrive %" zamiast "c:\".</span><span class="sxs-lookup"><span data-stu-id="15518-114">Use variables in hello path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="15518-115">Jeśli chcesz tooadd aplikacji z hello **Start** menu, należy toohave *dodane toohello tej aplikacji **Start** menu w obrazie szablonu.*</span><span class="sxs-lookup"><span data-stu-id="15518-115">If you want tooadd your app from hello **Start** menu, you need toohave *added that app toohello **Start** menu on your template image.*</span></span> <span data-ttu-id="15518-116">W przeciwnym razie RemoteApp zostanie wyświetlony tylko co *jest* na powitania **Start** należy mylić menu, a.</span><span class="sxs-lookup"><span data-stu-id="15518-116">Otherwise, RemoteApp will only see what *is* on hello **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="15518-117">toomake się, że aplikacja jest w hello **Start** menu, umieść plik skrótu - **lnk** — znajduje się w folderze Start\Programy %systemdrive%\ProgramData\Microsoft\Windows\Start hello.</span><span class="sxs-lookup"><span data-stu-id="15518-117">toomake sure your app is in hello **Start** menu, place a shortcut file - **.lnk** - inside hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="15518-118">Jeśli nie pamiętasz toohello aplikacji hello tooadd **Start** menu podczas tworzenia szablonu hello wybierz tooadd hello ścieżki toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="15518-118">If you forgot tooadd hello app toohello **Start** menu when you created hello template, choose tooadd hello path toohello app.</span></span> <span data-ttu-id="15518-119">(Lub Utwórz ponownie obrazu szablonu, ale jest dość nieco więcej pracy).</span><span class="sxs-lookup"><span data-stu-id="15518-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 

