---
title: "Praca w tym samym środowisku usługi Office 365 na dowolnym urządzeniu z usługą Azure RemoteApp | Microsoft Docs"
description: "Dowiedz się, jak udostępniać użytkownikom dowolną aplikację Office 365 przy użyciu usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 584c781c97097cda3c1455ade05cba8659f11073
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="93843-103">Praca w tym samym środowisku usługi Office 365 na dowolnym urządzeniu z usługą Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="93843-103">Get the same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="93843-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="93843-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="93843-105">Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="93843-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="93843-106">W tym artykule opisano sposób wdrażania usługi Office 365 na dowolnym urządzeniu w firmie.</span><span class="sxs-lookup"><span data-stu-id="93843-106">This article will cover how to deploy Office 365 on any device in your company.</span></span> <span data-ttu-id="93843-107">Użytkownicy mogą korzystać z tych samych możliwości i środowiska interfejsu użytkownika na urządzeniach Apple oraz z systemami Android i Windows.</span><span class="sxs-lookup"><span data-stu-id="93843-107">Your users can get the same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="93843-108">Osiągniemy ten cel dzięki usłudze Azure RemoteApp, obsługując usługę Office 365 na skalowalnych maszynach wirtualnych platformy Azure, z którymi użytkownicy mogą nawiązywać połączenie.</span><span class="sxs-lookup"><span data-stu-id="93843-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="93843-109">Ten zestaw maszyn wirtualnych nazywamy „kolekcją w chmurze”.</span><span class="sxs-lookup"><span data-stu-id="93843-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="93843-110">Tworzenie kolekcji w chmurze</span><span class="sxs-lookup"><span data-stu-id="93843-110">Create a cloud collection</span></span>
<span data-ttu-id="93843-111">Najpierw, po utworzeniu konta platformy Azure, przejdź do usługi **RemoteApp**, klikając link po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="93843-111">First after you have created an Azure account, navigate to **RemoteApp** by clicking on the link on the left side.</span></span>
<span data-ttu-id="93843-112">![Wyświetlanie usługi Azure RemoteApp w witrynie Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="93843-112">![Showing Azure RemoteApp on the Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="93843-113">Następnie kontynuuj, klikając pozycję **nowe** w dolnej części ekranu i „szybko tworząc” kolekcję.</span><span class="sxs-lookup"><span data-stu-id="93843-113">Then continue by clicking **new** on the bottom and "quick creating" a collection.</span></span> <span data-ttu-id="93843-114">Podaj nazwę, region, subskrypcję, plan i obraz „Office Proffesional 2013” udostępniony przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="93843-114">Provide a name, the region, the subscription, the plan and the image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="93843-115">![Okno dialogowe tworzenia](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="93843-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="93843-116">Gdy wypełnisz formularz, powinien rozpocząć się proces tworzenia kolekcji.</span><span class="sxs-lookup"><span data-stu-id="93843-116">Once you finish the form the collection creation process should start.</span></span> <span data-ttu-id="93843-117">Może on potrwać mniej więcej godzinę.</span><span class="sxs-lookup"><span data-stu-id="93843-117">This may take up to an hour or so.</span></span>

![Oczekiwanie](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="93843-119">Po zakończeniu procesu ekran będzie wyglądać podobnie do poniższego.</span><span class="sxs-lookup"><span data-stu-id="93843-119">Once the process is done, it will look something like this.</span></span> <span data-ttu-id="93843-120">Po kliknięciu pozycji **Publikowanie** zobaczysz, że większość aplikacji pakietu Office została już opublikowana.</span><span class="sxs-lookup"><span data-stu-id="93843-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="93843-121">![Utworzona kolekcja](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="93843-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![Opublikowane aplikacje](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="93843-123">W tym miejscu możesz także dodać więcej użytkowników z dostępem do tej kolekcji, klikając pozycję **Dostęp użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="93843-123">At this point you can also add more users that have access to this collection by clicking **User Access**.</span></span>
<span data-ttu-id="93843-124">![Konfigurowanie dostępu użytkowników](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="93843-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="93843-125">Teraz spróbujmy nawiązać połączenie z usługą Office 365.</span><span class="sxs-lookup"><span data-stu-id="93843-125">Now let's try out connecting to Office 365!</span></span>

## <a name="connect-to-office-365"></a><span data-ttu-id="93843-126">Łączenie z usługą Office 365</span><span class="sxs-lookup"><span data-stu-id="93843-126">Connect to Office 365</span></span>
<span data-ttu-id="93843-127">Przejdź do strony [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), przewiń w dół i kliknij pozycję **Pobierz klientów**, aby zainstalować klienta usługi Azure RemoteApp na aktualnie używanym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="93843-127">We'll head over to [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** to install the Azure RemoteApp client on the device you're on.</span></span> <span data-ttu-id="93843-128">Poniższe zrzuty ekranu dotyczą systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="93843-128">The screenshots below are for Windows.</span></span>

<span data-ttu-id="93843-129">Po uruchomieniu aplikacji zostanie wyświetlony monit o zalogowanie przy użyciu konta Microsoft (zwanego wcześniej „Live ID”). Zaloguj się za pomocą konta używanego jako konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="93843-129">Once the application starts you'll be asked to sign in with your Microsoft account (formerly called a "Live ID"), use the same one as your Azure account for now.</span></span> <span data-ttu-id="93843-130">Po zalogowaniu zobaczysz powiadomienia o nowych zaproszeniach. Kliknij w tym miejscu, aby wyświetlić listę podobną do poniższej.</span><span class="sxs-lookup"><span data-stu-id="93843-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="93843-131">Zaakceptuj zaproszenie odpowiadające adresowi e-mail właściciela konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="93843-131">Accept the invitation that matches your Azure account owner email.</span></span>

![Nowe zaproszenie](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="93843-133">Ekran z nowymi zaproszeniami wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="93843-133">What it looks like when there are new invitations.</span></span>

![Akceptowanie zaproszenia](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="93843-135">Po zaakceptowaniu zaproszenia w kliencie usługi Azure RemoteApp powinny być widoczne wszystkie aplikacje pakietu Office.</span><span class="sxs-lookup"><span data-stu-id="93843-135">Once you accept the invitation you should see all the Office apps in the Azure RemoteApp client.</span></span>

![Lista aplikacji](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="93843-137">Kliknięcie dowolnej aplikacji powinno spowodować jej uruchomienie na maszynie wirtualnej platformy Azure. Wszystko gotowe.</span><span class="sxs-lookup"><span data-stu-id="93843-137">When you click on any of these the application should start on the Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="93843-138">Owocnej pracy.</span><span class="sxs-lookup"><span data-stu-id="93843-138">Enjoy!</span></span>

![uruchamianie](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

