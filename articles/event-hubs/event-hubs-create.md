---
title: "aaaCreate Centrum zdarzeń platformy Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie przestrzeni nazw usługi Azure Event Hubs i Centrum zdarzeń za pomocą hello portalu Azure"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a><span data-ttu-id="7e094-103">Tworzenie przestrzeni nazw usługi Event Hubs i Centrum zdarzeń za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7e094-103">Create an Event Hubs namespace and an event hub using hello Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="7e094-104">Tworzenie przestrzeni nazw usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="7e094-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="7e094-105">Zaloguj się na toohello [portalu Azure][Azure portal]i kliknij przycisk **nowy** na powitania lewym górnym rogu ekranu hello.</span><span class="sxs-lookup"><span data-stu-id="7e094-105">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
1. <span data-ttu-id="7e094-106">Kliknij przycisk **Internetu rzeczy**, a następnie kliknij przycisk **usługi Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="7e094-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="7e094-107">W hello **tworzenie przestrzeni nazw** bloku, wprowadź nazwę przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="7e094-107">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="7e094-108">system powitania od razu sprawdza toosee, jeśli nazwa hello jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="7e094-108">hello system immediately checks toosee if hello name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="7e094-109">Po co czy hello przestrzeni nazw jest dostępna, należy wybrać hello cenowym (Basic lub Standard).</span><span class="sxs-lookup"><span data-stu-id="7e094-109">After making sure hello namespace name is available, choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="7e094-110">Ponadto Wybierz subskrypcję platformy Azure, lokalizacji i grupy zasobów w zasobów hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="7e094-110">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> 
1. <span data-ttu-id="7e094-111">Kliknij przycisk **Utwórz** toocreate hello w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="7e094-111">Click **Create** toocreate hello namespace.</span></span> <span data-ttu-id="7e094-112">Toowait może mieć kilka minut, aż hello systemu toofully Zapewnij hello zasoby.</span><span class="sxs-lookup"><span data-stu-id="7e094-112">You may have toowait a few minutes for hello system toofully provision hello resources.</span></span>
2. <span data-ttu-id="7e094-113">Witaj portalu obszarów nazw kliknij na liście hello nowo utworzonego obszaru nazw.</span><span class="sxs-lookup"><span data-stu-id="7e094-113">In hello portal list of namespaces, click hello newly created namespace.</span></span>
2. <span data-ttu-id="7e094-114">Kliknij przycisk **zasady dostępu współużytkowanego**, a następnie kliknij przycisk **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="7e094-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="7e094-115">Kliknij przycisk hello toocopy przycisku Kopiuj hello **RootManageSharedAccessKey** Schowka toohello ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="7e094-115">Click hello copy button toocopy hello **RootManageSharedAccessKey** connection string toohello clipboard.</span></span> <span data-ttu-id="7e094-116">Zapisz te parametry połączenia w tymczasowej lokalizacji, takiego jak Notatnik, toouse później.</span><span class="sxs-lookup"><span data-stu-id="7e094-116">Save this connection string in a temporary location, such as Notepad, toouse later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="7e094-117">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="7e094-117">Create an event hub</span></span>

1. <span data-ttu-id="7e094-118">Na liście przestrzeni nazw usługi Event Hubs hello kliknij hello nowo utworzonego obszaru nazw.</span><span class="sxs-lookup"><span data-stu-id="7e094-118">In hello Event Hubs namespace list, click hello newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="7e094-119">W bloku przestrzeni nazw powitania kliknij **usługi Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="7e094-119">In hello namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="7e094-120">U góry hello hello bloku, kliknij przycisk **dodać Centrum zdarzeń**.</span><span class="sxs-lookup"><span data-stu-id="7e094-120">At hello top of hello blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="7e094-121">Wpisz nazwę Centrum zdarzeń, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7e094-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="7e094-122">Centrum zdarzeń został utworzony i uzyskano parametry połączenia hello muszą toosend i odbierania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7e094-122">Your event hub is now created, and you have hello connection strings you need toosend and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e094-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7e094-123">Next steps</span></span>
<span data-ttu-id="7e094-124">toolearn więcej informacji na temat usługi Event Hubs, odwiedź te linki:</span><span class="sxs-lookup"><span data-stu-id="7e094-124">toolearn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="7e094-125">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="7e094-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="7e094-126">Omówienie interfejsu API usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="7e094-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/