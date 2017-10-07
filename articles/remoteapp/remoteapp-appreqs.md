---
title: "aaaApp wymagania dotyczące usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o wymaganiach dotyczących powitania dla aplikacji, które mają toouse w usłudze Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fa2bcdaab457a6fbee8ac52a81d1c4154bbdce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="app-requirements"></a><span data-ttu-id="fa201-103">Wymagania aplikacji</span><span class="sxs-lookup"><span data-stu-id="fa201-103">App requirements</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fa201-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="fa201-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="fa201-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="fa201-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="fa201-106">Usługa Azure RemoteApp obsługuje przesyłania strumieniowego 32-bitowy lub 64-bitowej aplikacji systemu Windows za pomocą obrazu systemu Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="fa201-106">Azure RemoteApp supports streaming 32-bit or 64-bit Windows-based applications from a Windows Server 2012 R2 image.</span></span> <span data-ttu-id="fa201-107">Większość istniejących 32-bitowy lub 64-bitowej aplikacji systemu Windows uruchom "jako" w usłudze Azure RemoteApp (usług pulpitu zdalnego lub wcześniej znane jako usługi terminalowe) środowiska.</span><span class="sxs-lookup"><span data-stu-id="fa201-107">Most existing 32-bit or 64-bit Windows-based applications run "as is" in Azure RemoteApp (Remote Desktop Services or formerly known as Terminal Services) environment.</span></span> <span data-ttu-id="fa201-108">Jednak ma różnicy między zainstalowany, a także — niektóre aplikacje działać prawidłowo i wykonaj, podczas gdy inne osoby nie.</span><span class="sxs-lookup"><span data-stu-id="fa201-108">However, there is a difference between running and running well - some applications function correctly and perform well, while others do not.</span></span> <span data-ttu-id="fa201-109">Witaj następujących informacji zawiera wskazówki dotyczące tworzenia aplikacji w środowisku usług pulpitu zdalnego i testowania zgodności tooensure.</span><span class="sxs-lookup"><span data-stu-id="fa201-109">hello following information provides guidance for developing applications in a Remote Desktop Services environment and testing tooensure compatibility.</span></span>

<span data-ttu-id="fa201-110">Porada: Trwają prace nad tworzenia przykłady pracy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fa201-110">Tip: We're working on creating some working examples of apps for you.</span></span> <span data-ttu-id="fa201-111">Zostanie wyświetlone nowe tematy, które omówiono w nim przy użyciu programu Microsoft Access, QuickBooks i App-V w usłudze RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fa201-111">You'll see new topics that discuss using Microsoft Access, QuickBooks, and App-V in RemoteApp.</span></span>

## <a name="requirements"></a><span data-ttu-id="fa201-112">Wymagania</span><span class="sxs-lookup"><span data-stu-id="fa201-112">Requirements</span></span>
<span data-ttu-id="fa201-113">Te trzy wymagania, jeśli zostały wykonane, Pomoc aplikacji Uruchom również w usłudze RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="fa201-113">These three requirements, if followed, help your application run well in RemoteApp:</span></span>

1. <span data-ttu-id="fa201-114">Aplikacje, które spełniają wszystkie [wymagania dotyczące certyfikacji dla systemu Windows aplikacji klasycznych](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) i stosować zbyt[wytycznych programowania usług pulpitu zdalnego](https://msdn.microsoft.com/library/aa383490.aspx) będzie miał pełną zgodność z usługą RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fa201-114">Applications that meet all [Certification requirements for Windows desktop apps](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) and adhere too[Remote Desktop Services programming guidelines](https://msdn.microsoft.com/library/aa383490.aspx) will have complete compatibility with RemoteApp.</span></span>
2. <span data-ttu-id="fa201-115">Aplikacje powinny nigdy nie przechowywać dane lokalnie w obrazie hello lub wystąpienia usługi RemoteApp, które mogą zostać utracone.</span><span class="sxs-lookup"><span data-stu-id="fa201-115">Applications should never store data locally on hello image or RemoteApp instances that can be lost.</span></span>  <span data-ttu-id="fa201-116">Po utworzeniu kolekcji usługi RemoteApp wystąpień hello są klonowane i są bezstanowych i powinien zawierać wyłącznie aplikacje.</span><span class="sxs-lookup"><span data-stu-id="fa201-116">After you create a RemoteApp collection, hello instances are cloned and are stateless and should only contain applications.</span></span> <span data-ttu-id="fa201-117">Przechowywanie danych w zewnętrznym źródle lub w profilu użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="fa201-117">Store data in an external source or within hello user's profile.</span></span>
3. <span data-ttu-id="fa201-118">Niestandardowe obrazy nigdy nie powinna zawierać dane, które mogą zostać utracone.</span><span class="sxs-lookup"><span data-stu-id="fa201-118">Custom images should never contain data that can be lost.</span></span>  

## <a name="testing-your-apps"></a><span data-ttu-id="fa201-119">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="fa201-119">Testing your apps</span></span>
<span data-ttu-id="fa201-120">Użyj tych aplikacji tootesting kroki:</span><span class="sxs-lookup"><span data-stu-id="fa201-120">Use these steps tootesting applications:</span></span>

1. <span data-ttu-id="fa201-121">Instalowanie systemu Windows Server 2012 R2 i aplikacji</span><span class="sxs-lookup"><span data-stu-id="fa201-121">Install Windows Server 2012 R2 and your application</span></span>
2. <span data-ttu-id="fa201-122">Włączanie pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="fa201-122">Enable Remote Desktop</span></span>
3. <span data-ttu-id="fa201-123">Utwórz dwa konta użytkownika, Użytkownik_a i Użytkownik_b Dodawanie zarówno grupy zabezpieczeń Użytkownicy kont toohello pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="fa201-123">Create two user accounts, UserA and UserB, adding both user accounts toohello Remote Desktop security group.</span></span>
4. <span data-ttu-id="fa201-124">Sprawdź zgodność wielu sesji podczas uruchamiania aplikacji hello, ustanawiając dwóch jednoczesnych toohello sesji usług pulpitu zdalnego komputera.</span><span class="sxs-lookup"><span data-stu-id="fa201-124">Check multi-session compatibility by establishing two simultaneous RDS sessions toohello PC while launching hello application.</span></span>
5. <span data-ttu-id="fa201-125">Sprawdź poprawność zachowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="fa201-125">Validate app behavior</span></span>

## <a name="application-development-guidelines"></a><span data-ttu-id="fa201-126">Wskazówki dotyczące programowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="fa201-126">Application development guidelines</span></span>
<span data-ttu-id="fa201-127">Użyj hello następujące wytyczne dotyczące tworzenia aplikacji dla usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fa201-127">Use hello following guidelines for developing applications for RemoteApp.</span></span>

### <a name="multiple-users"></a><span data-ttu-id="fa201-128">Wielu użytkowników</span><span class="sxs-lookup"><span data-stu-id="fa201-128">Multiple users</span></span>
* <span data-ttu-id="fa201-129">Instalowanie [dla pojedynczego użytkownika ](https://msdn.microsoft.com/library/aa380661.aspx)można tworzyć problemy w środowisku wielodostępnym.</span><span class="sxs-lookup"><span data-stu-id="fa201-129">Installing an [application for a single user ](https://msdn.microsoft.com/library/aa380661.aspx)can create problems in a multiuser environment.</span></span>
* <span data-ttu-id="fa201-130">Aplikacje powinny [przechowywania informacji o użytkowniku](https://msdn.microsoft.com/library/aa383452.aspx) w lokalizacjach specyficzne dla użytkownika, oddzielnie z globalnego informacji dotyczący tooall użytkowników.</span><span class="sxs-lookup"><span data-stu-id="fa201-130">Applications should [store user-specific information](https://msdn.microsoft.com/library/aa383452.aspx) in user-specific locations, separately from global information that applies tooall users.</span></span>
* <span data-ttu-id="fa201-131">RemoteApp używa wielu [przestrzeni nazw dla obiektów jądra](https://msdn.microsoft.com/library/aa382954.aspx); globalnej przestrzeni nazw jest używana głównie przez usługi w aplikacji klient/serwer.</span><span class="sxs-lookup"><span data-stu-id="fa201-131">RemoteApp uses multiple [namespaces for kernel objects](https://msdn.microsoft.com/library/aa382954.aspx); a global namespace is used primarily by services in client/server applications.</span></span>
* <span data-ttu-id="fa201-132">Nie jest bezpieczne tooassume, który hello nazwę komputera lub hello [adres IP](https://msdn.microsoft.com/library/aa382942.aspx) przypisanej toohello komputera są skojarzone z pojedynczego użytkownika, ponieważ wielu użytkowników może być zalogowany jednocześnie tooa hosta sesji usług pulpitu zdalnego (sesji usług pulpitu zdalnego Serwer hosta).</span><span class="sxs-lookup"><span data-stu-id="fa201-132">It is not safe tooassume that hello computer name or hello [IP address](https://msdn.microsoft.com/library/aa382942.aspx) assigned toohello computer are associated with a single user because multiple users can be logged on simultaneously tooa Remote Desktop Session Host (RD Session Host) server.</span></span>

### <a name="performance"></a><span data-ttu-id="fa201-133">Wydajność</span><span class="sxs-lookup"><span data-stu-id="fa201-133">Performance</span></span>
* <span data-ttu-id="fa201-134">Wyłącz [efekty graficzne](https://msdn.microsoft.com/library/aa380822.aspx) przed dodaniem tooRemoteApp Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fa201-134">Disable [graphic effects](https://msdn.microsoft.com/library/aa380822.aspx) before you add your app tooRemoteApp.</span></span>
* <span data-ttu-id="fa201-135">dostępność toomaximize procesora CPU dla wszystkich użytkowników, albo wyłącz [zadania w tle ](https://msdn.microsoft.com/library/aa380665.aspx) lub Utwórz zadania tła wydajne, które nie są obciążający zasoby.</span><span class="sxs-lookup"><span data-stu-id="fa201-135">toomaximize CPU availability for all users, either disable [background tasks ](https://msdn.microsoft.com/library/aa380665.aspx) or create efficient background tasks that are not resource-intensive.</span></span>
* <span data-ttu-id="fa201-136">Należy dostosować i zrównoważenia aplikacji [wątku użycia](https://msdn.microsoft.com/library/aa383520.aspx) w środowisku wielodostępnym, wieloprocesorowych.</span><span class="sxs-lookup"><span data-stu-id="fa201-136">You should tune and balance application [thread usage](https://msdn.microsoft.com/library/aa383520.aspx) for a multiuser, multiprocessor environment.</span></span>
* <span data-ttu-id="fa201-137">wydajność toooptimize jest dobrym rozwiązaniem dla aplikacji za[wykryć](https://msdn.microsoft.com/library/aa380798.aspx) czy są uruchomione w sesji klienta.</span><span class="sxs-lookup"><span data-stu-id="fa201-137">toooptimize performance, it is good practice for applications too[detect](https://msdn.microsoft.com/library/aa380798.aspx) whether they are running in a client session.</span></span>

