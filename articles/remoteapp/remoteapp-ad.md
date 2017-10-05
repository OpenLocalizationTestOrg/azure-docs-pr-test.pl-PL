---
title: "Usługi Azure AD i wymagania usługi Active Directory dla usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować usługi Active Directory do pracy z usługą Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 78008a032faa93795cc02b720d68a0c6f5f16e9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="569d3-103">Usługi Azure AD i wymagania usługi Active Directory dla usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="569d3-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="569d3-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="569d3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="569d3-105">Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="569d3-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="569d3-106">Kolekcji hybrydowej usługi Azure RemoteApp lub kolekcji w chmurze, która ma zostać utworzona Federacja za pomocą AD Connect należy wykonać następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="569d3-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want to federate using AD Connect, you need to do the following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="569d3-107">Łączenie usługi Azure AD i usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="569d3-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="569d3-108">Jeśli chcesz połączyć z dzierżawy usługi Azure AD i środowiska lokalnej usługi Active Directory, należy użyć AD Connect.</span><span class="sxs-lookup"><span data-stu-id="569d3-108">If you want to connect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="569d3-109">Spowoduje przejście tylko [4 kliknięć](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) nawiązać dwa katalogi.</span><span class="sxs-lookup"><span data-stu-id="569d3-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) to connect the two directories.</span></span>

<span data-ttu-id="569d3-110">Uwaga — synchronizacja katalogów jest wymagana dla kolekcji hybrydowej.</span><span class="sxs-lookup"><span data-stu-id="569d3-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="569d3-111">Upewnij się, że Twoje "@domain.com" zgodny</span><span class="sxs-lookup"><span data-stu-id="569d3-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="569d3-112">Przed rozpoczęciem pracy upewnij się, że nazwa UPN lasu lokalnego zgodny z sufiksem domeny domenę usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="569d3-112">Before you get started, make sure that the UPN for your on-premises forest matches the suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="569d3-113">Po skonfigurowaniu sufiks nazwy UPN domeny w usłudze Azure AD wszystkich użytkowników logujących się do usługi Azure RemoteApp będzie zalogować się jako "użytkownik @<the suffix you set up>."</span><span class="sxs-lookup"><span data-stu-id="569d3-113">After you set up the UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<the suffix you set up>."</span></span> <span data-ttu-id="569d3-114">Upewnij się, że użytkownicy mogą również Zaloguj się za pomocą takie same user@suffix w domenie lokalnej.</span><span class="sxs-lookup"><span data-stu-id="569d3-114">Make sure that users can also log in with the same user@suffix into the on-premises domain.</span></span> <span data-ttu-id="569d3-115">W niektórych przypadkach skonfigurowaniem jedną nazwę domeny w usłudze Azure AD podczas określania sufiksu inną domenę dla użytkownika na — lokalnej</span><span class="sxs-lookup"><span data-stu-id="569d3-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for the user on-prem.</span></span> <span data-ttu-id="569d3-116">W takim przypadku użytkowników nie będzie można połączyć się z dowolnym komputerów przyłączonych do domeny lub zasobów za pomocą usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="569d3-116">In this case, your users won't be able to connect to any domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="569d3-117">Na przykład skonfigurować sufiks domeny Twojej nazwy UPN w usłudze AAD jako contoso.com, ale niektórzy użytkownicy korzystają z lokalnej usługi Active są skonfigurowane do logowania się przy użyciu @contoso.uk, nie będzie mógł poprawnie Zaloguj się do kolekcji ARA tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="569d3-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured to log in with @contoso.uk, then those users will not be able to correctly log into the ARA collection.</span></span> <span data-ttu-id="569d3-118">Użytkownicy nazwy UPN w usłudze AAD i AD muszą być takie same, dla nazwy logowania w celu umożliwienia"</span><span class="sxs-lookup"><span data-stu-id="569d3-118">Users UPN in AAD and AD must be the same for the login to be possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="569d3-119">Tworzenie obiektów dla usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="569d3-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="569d3-120">Należy także utworzyć następujące lokalną obiektów usługi Active Directory:</span><span class="sxs-lookup"><span data-stu-id="569d3-120">You also need to create the following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="569d3-121">Konto usługi, aby zapewnić dostęp do zasobów domeny dla programów RemoteApp przez dołączenie do domeny lokalnej RDSH punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="569d3-121">A service account to provide access to domain resources for RemoteApp programs by joining RDSH end points to the on-premises domain.</span></span>
* <span data-ttu-id="569d3-122">Jednostki organizacyjnej (OU) zawierają obiekty komputera usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="569d3-122">An Organizational Unit (OU) to contain RemoteApp machine objects.</span></span> <span data-ttu-id="569d3-123">Użyj jednostki organizacyjnej, jest zalecane (lecz nie wymagane) izolowanie kont i zasad, które będą używane z usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="569d3-123">Use of the OU is recommended (but not required) to isolate the accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="569d3-124">Oba te obiekty potrzebne podczas tworzenia kolekcji usługi RemoteApp, dlatego należy najpierw wykonać następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="569d3-124">You need both of these objects when you create your RemoteApp collection, so be sure to do these steps first.</span></span>

