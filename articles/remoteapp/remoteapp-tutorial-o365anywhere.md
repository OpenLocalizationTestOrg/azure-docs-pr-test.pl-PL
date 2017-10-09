---
title: "aaaGet hello tym samym środowisku usługi Office 365 na dowolnym urządzeniu za pomocą usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooshare dowolną aplikację Office 365 z użytkownikami przy użyciu usługi Azure RemoteApp."
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
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="d4ea6-103">Get hello sam środowisku usługi Office 365 na dowolnym urządzeniu za pomocą usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="d4ea6-103">Get hello same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d4ea6-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d4ea6-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d4ea6-106">W tym artykule opisano sposób toodeploy usługi Office 365 na dowolnym urządzeniu w firmie.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-106">This article will cover how toodeploy Office 365 on any device in your company.</span></span> <span data-ttu-id="d4ea6-107">Użytkowników można uzyskać hello takie same możliwości i interfejsu użytkownika występuje w systemach Android, firmy Apple i systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-107">Your users can get hello same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="d4ea6-108">Osiągniemy ten cel dzięki usłudze Azure RemoteApp, obsługując usługę Office 365 na skalowalnych maszynach wirtualnych platformy Azure, z którymi użytkownicy mogą nawiązywać połączenie.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="d4ea6-109">Ten zestaw maszyn wirtualnych nazywamy „kolekcją w chmurze”.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="d4ea6-110">Tworzenie kolekcji w chmurze</span><span class="sxs-lookup"><span data-stu-id="d4ea6-110">Create a cloud collection</span></span>
<span data-ttu-id="d4ea6-111">Najpierw po utworzeniu konta platformy Azure, przejdź zbyt**RemoteApp** , klikając łącze hello na powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-111">First after you have created an Azure account, navigate too**RemoteApp** by clicking on hello link on hello left side.</span></span>
<span data-ttu-id="d4ea6-112">![Wyświetlanie usługi Azure RemoteApp na powitania portalu Azure](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="d4ea6-112">![Showing Azure RemoteApp on hello Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="d4ea6-113">Kontynuuj, klikając **nowe** na dole hello i "szybko tworząc" kolekcję.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-113">Then continue by clicking **new** on hello bottom and "quick creating" a collection.</span></span> <span data-ttu-id="d4ea6-114">Podaj nazwę, hello region, hello subskrypcji, hello plan i obraz powitania "Office Proffesional 2013", który firma Microsoft udostępnia.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-114">Provide a name, hello region, hello subscription, hello plan and hello image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="d4ea6-115">![Okno dialogowe tworzenia](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="d4ea6-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="d4ea6-116">Po zakończeniu należy uruchomić proces tworzenia kolekcji hello formularza hello.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-116">Once you finish hello form hello collection creation process should start.</span></span> <span data-ttu-id="d4ea6-117">To może potrwać godzinę tooan.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-117">This may take up tooan hour or so.</span></span>

![Oczekiwanie](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="d4ea6-119">Po zakończeniu procesu hello ekran będzie wyglądać następująco.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-119">Once hello process is done, it will look something like this.</span></span> <span data-ttu-id="d4ea6-120">Po kliknięciu pozycji **Publikowanie** zobaczysz, że większość aplikacji pakietu Office została już opublikowana.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="d4ea6-121">![Utworzona kolekcja](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="d4ea6-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![Opublikowane aplikacje](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="d4ea6-123">W tym momencie można również dodać więcej użytkowników, którzy mają dostęp toothis kolekcji, klikając **dostępu użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-123">At this point you can also add more users that have access toothis collection by clicking **User Access**.</span></span>
<span data-ttu-id="d4ea6-124">![Konfigurowanie dostępu użytkowników](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="d4ea6-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="d4ea6-125">Teraz spróbujmy łączenie tooOffice 365!</span><span class="sxs-lookup"><span data-stu-id="d4ea6-125">Now let's try out connecting tooOffice 365!</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="d4ea6-126">Połącz tooOffice 365</span><span class="sxs-lookup"><span data-stu-id="d4ea6-126">Connect tooOffice 365</span></span>
<span data-ttu-id="d4ea6-127">Przejdź przez zbyt[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), przewiń w dół i kliknij przycisk **klientów pobrać** tooinstall hello Azure RemoteApp klienta na powitania urządzenia możesz teraz.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-127">We'll head over too[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** tooinstall hello Azure RemoteApp client on hello device you're on.</span></span> <span data-ttu-id="d4ea6-128">Witaj poniższe zrzuty ekranu dotyczą systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-128">hello screenshots below are for Windows.</span></span>

<span data-ttu-id="d4ea6-129">Po uruchomieniu aplikacji hello użytkownik zostanie zapytany toosign przy użyciu swojego konta Microsoft (nazywanych wcześniej "Live ID"), użyj hello używanego jako konto platformy Azure dla teraz.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-129">Once hello application starts you'll be asked toosign in with your Microsoft account (formerly called a "Live ID"), use hello same one as your Azure account for now.</span></span> <span data-ttu-id="d4ea6-130">Po zalogowaniu zobaczysz powiadomienia o nowych zaproszeniach. Kliknij w tym miejscu, aby wyświetlić listę podobną do poniższej.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="d4ea6-131">Zaakceptuj zaproszenie hello, odpowiadające adresowi e-mail właściciela konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-131">Accept hello invitation that matches your Azure account owner email.</span></span>

![Nowe zaproszenie](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="d4ea6-133">Ekran z nowymi zaproszeniami wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="d4ea6-133">What it looks like when there are new invitations.</span></span>

![Akceptowanie zaproszenia](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="d4ea6-135">Po zaakceptowaniu zaproszenia hello powinny być widoczne wszystkie aplikacje pakietu Office hello powitania klienta usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-135">Once you accept hello invitation you should see all hello Office apps in hello Azure RemoteApp client.</span></span>

![Lista aplikacji](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="d4ea6-137">Po kliknięciu na żadnym z tych aplikacji hello należy uruchomić na powitania maszyny wirtualnej platformy Azure i powinno być wszystko gotowe!</span><span class="sxs-lookup"><span data-stu-id="d4ea6-137">When you click on any of these hello application should start on hello Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="d4ea6-138">Owocnej pracy.</span><span class="sxs-lookup"><span data-stu-id="d4ea6-138">Enjoy!</span></span>

![uruchamianie](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

