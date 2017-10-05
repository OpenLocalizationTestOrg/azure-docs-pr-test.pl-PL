---
title: "Wymagania dotyczące aplikacji dla usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o wymaganiach dotyczących aplikacji, które mają być używane w usłudze Azure RemoteApp"
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
ms.openlocfilehash: 13d42df97ea2b090180f5865a4eac25945f9f34c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="app-requirements"></a><span data-ttu-id="11f5b-103">Wymagania aplikacji</span><span class="sxs-lookup"><span data-stu-id="11f5b-103">App requirements</span></span>
> [!IMPORTANT]
> <span data-ttu-id="11f5b-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="11f5b-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="11f5b-105">Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="11f5b-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="11f5b-106">Usługa Azure RemoteApp obsługuje przesyłania strumieniowego 32-bitowy lub 64-bitowej aplikacji systemu Windows za pomocą obrazu systemu Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="11f5b-106">Azure RemoteApp supports streaming 32-bit or 64-bit Windows-based applications from a Windows Server 2012 R2 image.</span></span> <span data-ttu-id="11f5b-107">Większość istniejących 32-bitowy lub 64-bitowej aplikacji systemu Windows uruchom "jako" w usłudze Azure RemoteApp (usług pulpitu zdalnego lub wcześniej znane jako usługi terminalowe) środowiska.</span><span class="sxs-lookup"><span data-stu-id="11f5b-107">Most existing 32-bit or 64-bit Windows-based applications run "as is" in Azure RemoteApp (Remote Desktop Services or formerly known as Terminal Services) environment.</span></span> <span data-ttu-id="11f5b-108">Jednak ma różnicy między zainstalowany, a także — niektóre aplikacje działać prawidłowo i wykonaj, podczas gdy inne osoby nie.</span><span class="sxs-lookup"><span data-stu-id="11f5b-108">However, there is a difference between running and running well - some applications function correctly and perform well, while others do not.</span></span> <span data-ttu-id="11f5b-109">Poniżej znajdują się wskazówki dotyczące tworzenia aplikacji w środowisku usług pulpitu zdalnego i testy w celu zapewnienia zgodności.</span><span class="sxs-lookup"><span data-stu-id="11f5b-109">The following information provides guidance for developing applications in a Remote Desktop Services environment and testing to ensure compatibility.</span></span>

<span data-ttu-id="11f5b-110">Porada: Trwają prace nad tworzenia przykłady pracy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="11f5b-110">Tip: We're working on creating some working examples of apps for you.</span></span> <span data-ttu-id="11f5b-111">Zostanie wyświetlone nowe tematy, które omówiono w nim przy użyciu programu Microsoft Access, QuickBooks i App-V w usłudze RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="11f5b-111">You'll see new topics that discuss using Microsoft Access, QuickBooks, and App-V in RemoteApp.</span></span>

## <a name="requirements"></a><span data-ttu-id="11f5b-112">Wymagania</span><span class="sxs-lookup"><span data-stu-id="11f5b-112">Requirements</span></span>
<span data-ttu-id="11f5b-113">Te trzy wymagania, jeśli zostały wykonane, Pomoc aplikacji Uruchom również w usłudze RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="11f5b-113">These three requirements, if followed, help your application run well in RemoteApp:</span></span>

1. <span data-ttu-id="11f5b-114">Aplikacje, które spełniają wszystkie [wymagania dotyczące certyfikacji dla systemu Windows aplikacji klasycznych](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) i być zgodne z [wytycznych programowania usług pulpitu zdalnego](https://msdn.microsoft.com/library/aa383490.aspx) będzie miał pełną zgodność z usługą RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="11f5b-114">Applications that meet all [Certification requirements for Windows desktop apps](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) and adhere to [Remote Desktop Services programming guidelines](https://msdn.microsoft.com/library/aa383490.aspx) will have complete compatibility with RemoteApp.</span></span>
2. <span data-ttu-id="11f5b-115">Aplikacje powinny nigdy nie przechowują dane lokalnie w obrazie lub wystąpienia usługi RemoteApp, które mogą zostać utracone.</span><span class="sxs-lookup"><span data-stu-id="11f5b-115">Applications should never store data locally on the image or RemoteApp instances that can be lost.</span></span>  <span data-ttu-id="11f5b-116">Po utworzeniu kolekcji usługi RemoteApp wystąpienia są klonowane i są bezstanowych i powinien zawierać wyłącznie aplikacje.</span><span class="sxs-lookup"><span data-stu-id="11f5b-116">After you create a RemoteApp collection, the instances are cloned and are stateless and should only contain applications.</span></span> <span data-ttu-id="11f5b-117">Przechowywanie danych w zewnętrznym źródle lub w profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="11f5b-117">Store data in an external source or within the user's profile.</span></span>
3. <span data-ttu-id="11f5b-118">Niestandardowe obrazy nigdy nie powinna zawierać dane, które mogą zostać utracone.</span><span class="sxs-lookup"><span data-stu-id="11f5b-118">Custom images should never contain data that can be lost.</span></span>  

## <a name="testing-your-apps"></a><span data-ttu-id="11f5b-119">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="11f5b-119">Testing your apps</span></span>
<span data-ttu-id="11f5b-120">Wykonaj następujące kroki w celu testowania aplikacji:</span><span class="sxs-lookup"><span data-stu-id="11f5b-120">Use these steps to testing applications:</span></span>

1. <span data-ttu-id="11f5b-121">Instalowanie systemu Windows Server 2012 R2 i aplikacji</span><span class="sxs-lookup"><span data-stu-id="11f5b-121">Install Windows Server 2012 R2 and your application</span></span>
2. <span data-ttu-id="11f5b-122">Włączanie pulpitu zdalnego</span><span class="sxs-lookup"><span data-stu-id="11f5b-122">Enable Remote Desktop</span></span>
3. <span data-ttu-id="11f5b-123">Utwórz dwa konta użytkownika, Użytkownik_a i Użytkownik_b Dodawanie oba konta użytkownika do grupy zabezpieczeń usług pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="11f5b-123">Create two user accounts, UserA and UserB, adding both user accounts to the Remote Desktop security group.</span></span>
4. <span data-ttu-id="11f5b-124">Sprawdź zgodność wiele sesji, ustanawiając dwóch jednoczesnych RDS sesji do komputera podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="11f5b-124">Check multi-session compatibility by establishing two simultaneous RDS sessions to the PC while launching the application.</span></span>
5. <span data-ttu-id="11f5b-125">Sprawdź poprawność zachowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="11f5b-125">Validate app behavior</span></span>

## <a name="application-development-guidelines"></a><span data-ttu-id="11f5b-126">Wskazówki dotyczące programowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="11f5b-126">Application development guidelines</span></span>
<span data-ttu-id="11f5b-127">Skorzystaj z poniższych wskazówek do opracowywania aplikacji dla usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="11f5b-127">Use the following guidelines for developing applications for RemoteApp.</span></span>

### <a name="multiple-users"></a><span data-ttu-id="11f5b-128">Wielu użytkowników</span><span class="sxs-lookup"><span data-stu-id="11f5b-128">Multiple users</span></span>
* <span data-ttu-id="11f5b-129">Instalowanie [dla pojedynczego użytkownika ](https://msdn.microsoft.com/library/aa380661.aspx)można tworzyć problemy w środowisku wielodostępnym.</span><span class="sxs-lookup"><span data-stu-id="11f5b-129">Installing an [application for a single user ](https://msdn.microsoft.com/library/aa380661.aspx)can create problems in a multiuser environment.</span></span>
* <span data-ttu-id="11f5b-130">Aplikacje powinny [przechowywania informacji o użytkowniku](https://msdn.microsoft.com/library/aa383452.aspx) w lokalizacjach specyficzne dla użytkownika, niezależnie od globalne informacje, która ma zastosowanie do wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="11f5b-130">Applications should [store user-specific information](https://msdn.microsoft.com/library/aa383452.aspx) in user-specific locations, separately from global information that applies to all users.</span></span>
* <span data-ttu-id="11f5b-131">RemoteApp używa wielu [przestrzeni nazw dla obiektów jądra](https://msdn.microsoft.com/library/aa382954.aspx); globalnej przestrzeni nazw jest używana głównie przez usługi w aplikacji klient/serwer.</span><span class="sxs-lookup"><span data-stu-id="11f5b-131">RemoteApp uses multiple [namespaces for kernel objects](https://msdn.microsoft.com/library/aa382954.aspx); a global namespace is used primarily by services in client/server applications.</span></span>
* <span data-ttu-id="11f5b-132">Nie jest bezpieczne przyjęto założenie, że nazwa komputera lub [adres IP](https://msdn.microsoft.com/library/aa382942.aspx) przypisane do komputera są skojarzone z pojedynczego użytkownika, ponieważ wielu użytkowników może być zalogowany jednocześnie z serwerem hosta sesji usług pulpitu zdalnego (Host sesji usług pulpitu zdalnego).</span><span class="sxs-lookup"><span data-stu-id="11f5b-132">It is not safe to assume that the computer name or the [IP address](https://msdn.microsoft.com/library/aa382942.aspx) assigned to the computer are associated with a single user because multiple users can be logged on simultaneously to a Remote Desktop Session Host (RD Session Host) server.</span></span>

### <a name="performance"></a><span data-ttu-id="11f5b-133">Wydajność</span><span class="sxs-lookup"><span data-stu-id="11f5b-133">Performance</span></span>
* <span data-ttu-id="11f5b-134">Wyłącz [efekty graficzne](https://msdn.microsoft.com/library/aa380822.aspx) przed dodaniem aplikacji do usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="11f5b-134">Disable [graphic effects](https://msdn.microsoft.com/library/aa380822.aspx) before you add your app to RemoteApp.</span></span>
* <span data-ttu-id="11f5b-135">Aby zmaksymalizować dostępności procesora CPU dla wszystkich użytkowników, albo wyłącz [zadania w tle ](https://msdn.microsoft.com/library/aa380665.aspx) lub Utwórz zadania tła wydajne, które nie są obciążający zasoby.</span><span class="sxs-lookup"><span data-stu-id="11f5b-135">To maximize CPU availability for all users, either disable [background tasks ](https://msdn.microsoft.com/library/aa380665.aspx) or create efficient background tasks that are not resource-intensive.</span></span>
* <span data-ttu-id="11f5b-136">Należy dostosować i zrównoważenia aplikacji [wątku użycia](https://msdn.microsoft.com/library/aa383520.aspx) w środowisku wielodostępnym, wieloprocesorowych.</span><span class="sxs-lookup"><span data-stu-id="11f5b-136">You should tune and balance application [thread usage](https://msdn.microsoft.com/library/aa383520.aspx) for a multiuser, multiprocessor environment.</span></span>
* <span data-ttu-id="11f5b-137">Aby zoptymalizować wydajność, dobrym rozwiązaniem dla aplikacji jest [wykryć](https://msdn.microsoft.com/library/aa380798.aspx) czy są uruchomione w sesji klienta.</span><span class="sxs-lookup"><span data-stu-id="11f5b-137">To optimize performance, it is good practice for applications to [detect](https://msdn.microsoft.com/library/aa380798.aspx) whether they are running in a client session.</span></span>

