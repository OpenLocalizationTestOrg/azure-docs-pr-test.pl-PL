---
title: "aaaAdd tooyour użytkownika kolekcji usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd użytkowników tooyour kolekcji usługi Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 6b751fd2-2b11-499f-a2eb-12cb47f3129b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 0ae88e04c8bfc2ed55dc963945ed7e9ff687b603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-user-tooyour-azure-remoteapp-collection"></a><span data-ttu-id="3e427-103">Jak tooadd tooyour użytkownika kolekcji usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="3e427-103">How tooadd a user tooyour Azure RemoteApp collection</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3e427-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="3e427-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3e427-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="3e427-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3e427-106">Zanim użytkownicy mogą zobaczyć i użyć aplikacji w usłudze Azure RemoteApp, należy je uzyskać dostępu do kolekcji tooyour toogrant.</span><span class="sxs-lookup"><span data-stu-id="3e427-106">Before your users can see and use your apps in Azure RemoteApp, you have toogrant them access tooyour collection.</span></span> <span data-ttu-id="3e427-107">To jest część łatwe hello: na powitania **dostępu użytkownika** , wprowadź informacje o koncie hello hello użytkownika, a następnie kliknij znacznik wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="3e427-107">This is hello easy part: On hello **User Access** tab, enter hello account information for hello user, and then click hello check mark.</span></span>

<span data-ttu-id="3e427-108">Jakie informacje o koncie potrzebujesz?</span><span class="sxs-lookup"><span data-stu-id="3e427-108">What account information do you need?</span></span> <span data-ttu-id="3e427-109">Witaj typ kolekcji to zależy od utworzonego (w chmurze czy hybrydowa) i określa, czy używasz usługi Office 365 ProPlus w tej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="3e427-109">That depends on hello type of collection you created (cloud or hybrid) and whether you are using Office 365 ProPlus in that collection.</span></span>

## <a name="supported-user-identities"></a><span data-ttu-id="3e427-110">Tożsamości użytkowników obsługiwanych</span><span class="sxs-lookup"><span data-stu-id="3e427-110">Supported user identities</span></span>
<span data-ttu-id="3e427-111">typy kolekcji różnych Hello (w chmurze i hybrydowa) obsługuje tooapplications dostępu przy użyciu tożsamości innego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3e427-111">hello different collection types (cloud vs. hybrid) support using different user identities for access tooapplications.</span></span>  

<span data-ttu-id="3e427-112">Dla kolekcji hybrydowej RemoteApp możesz muszą tooset się infrastruktury domeny usługi Active Directory, lokalne i dzierżawy usługi Azure Active Directory o integracji katalogów (i opcjonalnie logowanie jednokrotne).</span><span class="sxs-lookup"><span data-stu-id="3e427-112">For a hybrid collection of RemoteApp, you need tooset up an Active Directory domain infrastructure on premises and an Azure Active Directory tenant with Directory Integration (and optionally single sign-on).</span></span> <span data-ttu-id="3e427-113">Ponadto należy toocreate niektóre obiekty usługi Active Directory w katalogu lokalnym hello.</span><span class="sxs-lookup"><span data-stu-id="3e427-113">Additionally, you need toocreate some Active Directory objects in hello on-premises directory.</span></span>  

<span data-ttu-id="3e427-114">Dla kolekcji usługi RemoteApp w chmurze każdy użytkownik, który ma obsługiwać tożsamości usługi Azure Active Directory może zostać przydzielony tooinclude tooRemoteApp dostępu użytkownika Accounts firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3e427-114">For a cloud collection of RemoteApp, any user that has Azure Active Directory support identities can be granted user access tooRemoteApp tooinclude Microsoft Accounts.</span></span>  <span data-ttu-id="3e427-115">Zobacz hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="3e427-115">See hello table below.</span></span>

<span data-ttu-id="3e427-116">Użytkownicy usługi Office 365 korzystają z usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3e427-116">Office 365 users are Azure Active Directory users.</span></span> <span data-ttu-id="3e427-117">Jeśli dysponują hybrydowe usługi Azure Active Directory, katalog zsynchronizowany kont, ich może otrzymać dostępu użytkowników w ramach wdrożenia hybrydowego usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3e427-117">If they have Azure Active Directory hybrid, Directory synchronized accounts, they can be granted user access in a RemoteApp hybrid deployment.</span></span>   

<span data-ttu-id="3e427-118">Korzystając z tej tabeli, jako odwołanie szybki, dla której tożsamość jest obsługiwana w kolekcji i jakie są wymagania dotyczące usługi Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="3e427-118">You can use this table as a quick reference for which identity is supported in your collection and what hello Active Directory requirements are.</span></span>

| <span data-ttu-id="3e427-119">Konta użytkowników</span><span class="sxs-lookup"><span data-stu-id="3e427-119">User accounts</span></span> | <span data-ttu-id="3e427-120">Chmura</span><span class="sxs-lookup"><span data-stu-id="3e427-120">Cloud</span></span> | <span data-ttu-id="3e427-121">Połączenie hybrydowe</span><span class="sxs-lookup"><span data-stu-id="3e427-121">Hybrid</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e427-122">Konto Microsoft</span><span class="sxs-lookup"><span data-stu-id="3e427-122">Microsoft Account</span></span> |<span data-ttu-id="3e427-123">Tak</span><span class="sxs-lookup"><span data-stu-id="3e427-123">Yes</span></span> |<span data-ttu-id="3e427-124">Nie</span><span class="sxs-lookup"><span data-stu-id="3e427-124">No</span></span> |
| <span data-ttu-id="3e427-125">Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="3e427-125">Azure Active Directory (Azure AD)</span></span> | | |
| <span data-ttu-id="3e427-126">Azure AD cloud</span><span class="sxs-lookup"><span data-stu-id="3e427-126">Azure AD cloud only</span></span> |<span data-ttu-id="3e427-127">Tak</span><span class="sxs-lookup"><span data-stu-id="3e427-127">Yes</span></span> |<span data-ttu-id="3e427-128">Nie</span><span class="sxs-lookup"><span data-stu-id="3e427-128">No</span></span> |
| <span data-ttu-id="3e427-129">Synchronizacja z synchronizacją haseł</span><span class="sxs-lookup"><span data-stu-id="3e427-129">ADsync with password sync</span></span> |<span data-ttu-id="3e427-130">Tak</span><span class="sxs-lookup"><span data-stu-id="3e427-130">Yes</span></span> |<span data-ttu-id="3e427-131">Tak</span><span class="sxs-lookup"><span data-stu-id="3e427-131">Yes</span></span> |
| <span data-ttu-id="3e427-132">ADsync bez synchronizacji haseł</span><span class="sxs-lookup"><span data-stu-id="3e427-132">ADsync without password sync</span></span> |<span data-ttu-id="3e427-133">Tak</span><span class="sxs-lookup"><span data-stu-id="3e427-133">Yes</span></span> |<span data-ttu-id="3e427-134">Nie</span><span class="sxs-lookup"><span data-stu-id="3e427-134">No</span></span> |
| <span data-ttu-id="3e427-135">Synchronizacja z usługami AD FS</span><span class="sxs-lookup"><span data-stu-id="3e427-135">ADsync with AD FS</span></span> |<span data-ttu-id="3e427-136">Tak</span><span class="sxs-lookup"><span data-stu-id="3e427-136">Yes</span></span> |<span data-ttu-id="3e427-137">Tak</span><span class="sxs-lookup"><span data-stu-id="3e427-137">Yes</span></span> |
| <span data-ttu-id="3e427-138">[Azure 3rd firm obsługiwanych dostawców tożsamości](https://msdn.microsoft.com/library/azure/jj679342.aspx) (przykład Ping)</span><span class="sxs-lookup"><span data-stu-id="3e427-138">[3rd-party Azure supported identity providers](https://msdn.microsoft.com/library/azure/jj679342.aspx)  (example Ping)</span></span> |<span data-ttu-id="3e427-139">Tak</span><span class="sxs-lookup"><span data-stu-id="3e427-139">Yes</span></span> |<span data-ttu-id="3e427-140">Tak</span><span class="sxs-lookup"><span data-stu-id="3e427-140">Yes</span></span> |
| <span data-ttu-id="3e427-141">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="3e427-141">Multi-Factor Authentication</span></span> |<span data-ttu-id="3e427-142">Tak</span><span class="sxs-lookup"><span data-stu-id="3e427-142">Yes</span></span> |<span data-ttu-id="3e427-143">Tak</span><span class="sxs-lookup"><span data-stu-id="3e427-143">Yes</span></span> |

<span data-ttu-id="3e427-144">Zapoznaj się z [więcej informacji](remoteapp-ad.md) o konfigurowaniu usługi Active Directory do usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3e427-144">Check out [more information](remoteapp-ad.md) about configuring Active Directory for RemoteApp.</span></span>

> [!NOTE]
> <span data-ttu-id="3e427-145">Hello użytkowników usługi Azure Active Directory muszą pochodzić z dzierżawy hello, który został skojarzony z subskrypcją.</span><span class="sxs-lookup"><span data-stu-id="3e427-145">hello Azure Active Directory users must be from hello tenant that's associated with your subscription.</span></span> <span data-ttu-id="3e427-146">(Można wyświetlać i modyfikować subskrypcji na powitania **ustawienia** kartę w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="3e427-146">(You can view and modify your subscription on hello **Settings** tab in hello portal.</span></span> <span data-ttu-id="3e427-147">Zobacz [dzierżawy usługi Azure Active Directory hello zmiany używanej przez usługę RemoteApp](remoteapp-changetenant.md) Aby uzyskać więcej informacji.)</span><span class="sxs-lookup"><span data-stu-id="3e427-147">See [Change hello Azure Active Directory tenant used by RemoteApp](remoteapp-changetenant.md) for more information.)</span></span>
> 
> 

## <a name="office-365-proplus-user-account-information"></a><span data-ttu-id="3e427-148">Informacje o koncie usługi Office 365 ProPlus użytkownika</span><span class="sxs-lookup"><span data-stu-id="3e427-148">Office 365 ProPlus user account information</span></span>
<span data-ttu-id="3e427-149">Jeśli używasz obrazu szablonu usługi Office 365 ProPlus hello w kolekcji *lub* Jeśli utworzony niestandardowy obraz, który korzysta z usługi Office 365 są dozwolone tylko tooadd usługi Azure Active Directory użytkowników, którzy mają subskrypcji usługi Office 365 dla hello Domyślna domena Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3e427-149">If you are using hello Office 365 ProPlus template image in your collection *or* if you created a custom image that uses Office 365, you are only allowed tooadd Azure Active Directory users that have Office 365 subscriptions for hello default domain of your subscription.</span></span> <span data-ttu-id="3e427-150">Zobacz [przy użyciu usługi Office 365 z usługą Azure RemoteApp](remoteapp-o365.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="3e427-150">See [Using Office 365 with Azure RemoteApp](remoteapp-o365.md) for more information.</span></span>

