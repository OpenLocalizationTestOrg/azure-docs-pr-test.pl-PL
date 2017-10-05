---
title: "Aktualizowanie kolekcji usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak aktualizowanie kolekcji usługi Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 454d78445d6092aec9eaa383e4c50cf15195848c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="8d9a4-103">Aktualizowanie kolekcji w usłudze Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="8d9a4-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8d9a4-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8d9a4-105">Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="8d9a4-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8d9a4-106">Dostarczane przez czas natychmiastową, gdy są potrzebne do aktualizacji aplikacji lub obrazu w kolekcji usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-106">There will come a time, inevitably, when you need to update the apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="8d9a4-107">Jeśli używasz jednego z obrazów zawartych w ramach subskrypcji usługi Azure RemoteApp w chmurowym lub hybrydowym kolekcji, wszystkie aktualizacje są obsługiwane przez usługi Azure RemoteApp, więc można umieścić łatwe.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-107">If you are using one of the images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="8d9a4-108">Jeśli używasz niestandardowego obrazu (Aby zbudować od początku lub utworzonej przez zmodyfikowanie jeden z naszych obrazów) jest odpowiedzialny za obsługę obrazu i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining the image and apps.</span></span> <span data-ttu-id="8d9a4-109">Musisz zaktualizować obrazu lub dowolną z aplikacji w nim, należy utworzyć nowych, zaktualizowanych wersji obrazu, a następnie zastąp istniejący obraz w kolekcji z tego nowego zaktualizowanego obrazu.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-109">If you need to update your image or any of the apps inside it, you need to create a new, updated version of the image, and then replace the existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="8d9a4-110">Tak jak uzyskać o aktualizowaniu kolekcji?</span><span class="sxs-lookup"><span data-stu-id="8d9a4-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="8d9a4-111">Jest bardzo prosta:</span><span class="sxs-lookup"><span data-stu-id="8d9a4-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="8d9a4-112">Aktualizowanie obrazu, który został użyty w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-112">Update the image that you used in your collection.</span></span> <span data-ttu-id="8d9a4-113">Zastosuj wszelkie poprawki lub wymagane aktualizacje, a następnie zapisz go z nową nazwą.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="8d9a4-114">[Przekaż](remoteapp-uploadimage.md) lub [zaimportować](remoteapp-image-on-azurevm.md) obrazu do usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image to RemoteApp.</span></span>
3. <span data-ttu-id="8d9a4-115">Teraz, na stronie pobierania kliknij **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-115">Now, on the collection page, click **Update**.</span></span>
4. <span data-ttu-id="8d9a4-116">Wybierz nowy obraz z **obrazu szablonu** listy.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-116">Choose the new image from the **Template Image** list.</span></span>
5. <span data-ttu-id="8d9a4-117">W tym miejscu jest wymagana - należy określić sposób postępowania w przypadku wszystkich użytkowników, którzy aktualnie używają aplikacji w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-117">Here's the tricky part - you need to decide how to deal with any users that are currently using an app in the collection.</span></span> <span data-ttu-id="8d9a4-118">Masz następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="8d9a4-118">You have the following choices:</span></span>
   
   * <span data-ttu-id="8d9a4-119">**Daj użytkownikom 60 minut po aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-119">**Give users 60 minutes after the update**.</span></span> <span data-ttu-id="8d9a4-120">Natychmiast po zakończeniu aktualizacji usługi Azure RemoteApp zostanie wyświetlony komunikat do wszystkich aktywnych użytkowników informacją o zapisanie pracy i wylogowanie i ponowne zalogowanie.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-120">As soon as the update is finished, Azure RemoteApp will display a message to any active users telling them to save their work and log off and log back in.</span></span> <span data-ttu-id="8d9a4-121">Po 60 minutach aktywni użytkownicy, którzy nie logowali się poza zostaną automatycznie wylogowani.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="8d9a4-122">Użytkownicy mogą natychmiast zalogować ponownie.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="8d9a4-123">**Wyloguj użytkowników natychmiast**.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-123">**Sign users out immediately**.</span></span> <span data-ttu-id="8d9a4-124">Natychmiast po zakończeniu aktualizacji Wyloguj wszystkich użytkowników automatycznie bez ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-124">As soon as the update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="8d9a4-125">Ta opcja może spowodować utratę danych przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="8d9a4-126">Jednak można ponownym połączeniu aplikacji natychmiast.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-126">However, they can reconnect to the app immediately.</span></span>
6. <span data-ttu-id="8d9a4-127">Kliknij znacznik wyboru, aby rozpocząć aktualizację.</span><span class="sxs-lookup"><span data-stu-id="8d9a4-127">Click the check mark to start the update.</span></span>

