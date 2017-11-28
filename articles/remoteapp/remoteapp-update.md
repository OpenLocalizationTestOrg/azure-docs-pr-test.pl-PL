---
title: "aaaUpdate kolekcji usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooupdate kolekcji usługi Azure RemoteApp"
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
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="8c22e-103">Aktualizowanie kolekcji w usłudze Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="8c22e-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8c22e-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8c22e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8c22e-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="8c22e-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8c22e-106">Dostarczane przez czas natychmiastową, gdy są potrzebne aplikacji hello tooupdate lub obrazu w kolekcji usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8c22e-106">There will come a time, inevitably, when you need tooupdate hello apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="8c22e-107">Jeśli używasz obrazów hello uwzględnionych w subskrypcji usługi Azure RemoteApp w chmurowym lub hybrydowym kolekcji, wszystkie aktualizacje są obsługiwane przez usługi Azure RemoteApp, więc można umieścić łatwe.</span><span class="sxs-lookup"><span data-stu-id="8c22e-107">If you are using one of hello images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="8c22e-108">Jeśli używasz niestandardowego obrazu (Aby zbudować od początku lub utworzonej przez zmodyfikowanie jeden z naszych obrazów) jest odpowiada za obsługę obrazu hello i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8c22e-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining hello image and apps.</span></span> <span data-ttu-id="8c22e-109">Jeśli potrzebujesz tooupdate obrazu lub dowolną z aplikacji hello w nim, należy toocreate nowych, zaktualizowanych wersji hello obrazu, a następnie zastąp hello istniejącego obrazu w kolekcji z tego nowego zaktualizowanego obrazu.</span><span class="sxs-lookup"><span data-stu-id="8c22e-109">If you need tooupdate your image or any of hello apps inside it, you need toocreate a new, updated version of hello image, and then replace hello existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="8c22e-110">Tak jak uzyskać o aktualizowaniu kolekcji?</span><span class="sxs-lookup"><span data-stu-id="8c22e-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="8c22e-111">Jest bardzo prosta:</span><span class="sxs-lookup"><span data-stu-id="8c22e-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="8c22e-112">Obraz powitania aktualizacji używane w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="8c22e-112">Update hello image that you used in your collection.</span></span> <span data-ttu-id="8c22e-113">Zastosuj wszelkie poprawki lub wymagane aktualizacje, a następnie zapisz go z nową nazwą.</span><span class="sxs-lookup"><span data-stu-id="8c22e-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="8c22e-114">[Przekaż](remoteapp-uploadimage.md) lub [zaimportować](remoteapp-image-on-azurevm.md) tooRemoteApp tego obrazu.</span><span class="sxs-lookup"><span data-stu-id="8c22e-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image tooRemoteApp.</span></span>
3. <span data-ttu-id="8c22e-115">Teraz, na stronie kolekcji powitania kliknij **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="8c22e-115">Now, on hello collection page, click **Update**.</span></span>
4. <span data-ttu-id="8c22e-116">Wybierz nowy obraz powitania od hello **obrazu szablonu** listy.</span><span class="sxs-lookup"><span data-stu-id="8c22e-116">Choose hello new image from hello **Template Image** list.</span></span>
5. <span data-ttu-id="8c22e-117">Poniżej przedstawiono część trudnych hello — jak potrzebny toodecide toodeal z wszyscy użytkownicy, którzy aktualnie używają aplikacji hello kolekcji.</span><span class="sxs-lookup"><span data-stu-id="8c22e-117">Here's hello tricky part - you need toodecide how toodeal with any users that are currently using an app in hello collection.</span></span> <span data-ttu-id="8c22e-118">Masz hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="8c22e-118">You have hello following choices:</span></span>
   
   * <span data-ttu-id="8c22e-119">**Daj użytkownikom 60 minut po aktualizacji hello**.</span><span class="sxs-lookup"><span data-stu-id="8c22e-119">**Give users 60 minutes after hello update**.</span></span> <span data-ttu-id="8c22e-120">Natychmiast po zakończeniu aktualizacji hello Azure RemoteApp wyświetli komunikat tooany użytkownicy aktywni, informacją toosave ich pracy i dziennika Wyłącz i ponownie zalogować.</span><span class="sxs-lookup"><span data-stu-id="8c22e-120">As soon as hello update is finished, Azure RemoteApp will display a message tooany active users telling them toosave their work and log off and log back in.</span></span> <span data-ttu-id="8c22e-121">Po 60 minutach aktywni użytkownicy, którzy nie logowali się poza zostaną automatycznie wylogowani.</span><span class="sxs-lookup"><span data-stu-id="8c22e-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="8c22e-122">Użytkownicy mogą natychmiast zalogować ponownie.</span><span class="sxs-lookup"><span data-stu-id="8c22e-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="8c22e-123">**Wyloguj użytkowników natychmiast**.</span><span class="sxs-lookup"><span data-stu-id="8c22e-123">**Sign users out immediately**.</span></span> <span data-ttu-id="8c22e-124">Natychmiast po zakończeniu aktualizacji hello Wyloguj wszystkich użytkowników automatycznie bez ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="8c22e-124">As soon as hello update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="8c22e-125">Ta opcja może spowodować utratę danych przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8c22e-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="8c22e-126">One jednak natychmiast ponownie toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8c22e-126">However, they can reconnect toohello app immediately.</span></span>
6. <span data-ttu-id="8c22e-127">Kliknij przycisk Aktualizuj hello toostart znacznik wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="8c22e-127">Click hello check mark toostart hello update.</span></span>

