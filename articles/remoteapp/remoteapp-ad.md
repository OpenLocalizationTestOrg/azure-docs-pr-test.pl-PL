---
title: "aaaAzure AD + wymagania usługi Active Directory dla usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset się toowork usługi Active Directory z usługą Azure RemoteApp."
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
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="32eb3-103">Usługi Azure AD i wymagania usługi Active Directory dla usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="32eb3-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="32eb3-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="32eb3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="32eb3-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="32eb3-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="32eb3-106">Kolekcji hybrydowej usługi Azure RemoteApp lub kolekcji w chmurze, które mają toofederate za pomocą AD Connect należy toodo hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="32eb3-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want toofederate using AD Connect, you need toodo hello following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="32eb3-107">Łączenie usługi Azure AD i usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="32eb3-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="32eb3-108">Tooconnect dzierżawy usługi Azure AD i środowiska lokalnej usługi Active Directory, należy użyć AD Connect.</span><span class="sxs-lookup"><span data-stu-id="32eb3-108">If you want tooconnect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="32eb3-109">Spowoduje przejście tylko [4 kliknięć](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello dwa katalogi.</span><span class="sxs-lookup"><span data-stu-id="32eb3-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello two directories.</span></span>

<span data-ttu-id="32eb3-110">Uwaga — synchronizacja katalogów jest wymagana dla kolekcji hybrydowej.</span><span class="sxs-lookup"><span data-stu-id="32eb3-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="32eb3-111">Upewnij się, że Twoje "@domain.com" zgodny</span><span class="sxs-lookup"><span data-stu-id="32eb3-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="32eb3-112">Przed rozpoczęciem upewnij się, że hello nazwy UPN użytkownika lokalnego lasu dopasowań hello sufiksu domeny usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32eb3-112">Before you get started, make sure that hello UPN for your on-premises forest matches hello suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="32eb3-113">Po skonfigurowaniu sufiks domeny hello nazwy UPN w usłudze Azure AD wszystkich użytkowników logujących się do usługi Azure RemoteApp będzie zalogować się jako "użytkownik @<hello suffix you set up>."</span><span class="sxs-lookup"><span data-stu-id="32eb3-113">After you set up hello UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<hello suffix you set up>."</span></span> <span data-ttu-id="32eb3-114">Upewnij się, że użytkownicy mogą również Zaloguj się za pomocą hello takie same user@suffix w domenie lokalnej hello.</span><span class="sxs-lookup"><span data-stu-id="32eb3-114">Make sure that users can also log in with hello same user@suffix into hello on-premises domain.</span></span> <span data-ttu-id="32eb3-115">W niektórych przypadkach skonfigurowaniem jedną nazwę domeny w usłudze Azure AD podczas określania sufiksu inną domenę dla hello użytkownika na — lokalnej</span><span class="sxs-lookup"><span data-stu-id="32eb3-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for hello user on-prem.</span></span> <span data-ttu-id="32eb3-116">W takim przypadku użytkowników nie będzie możliwe tooconnect tooany przyłączonych do domeny komputerów lub zasobów za pomocą usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="32eb3-116">In this case, your users won't be able tooconnect tooany domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="32eb3-117">Na przykład skonfigurować sufiks domeny Twojej nazwy UPN w usłudze AAD jako contoso.com, ale niektórzy użytkownicy korzystają z lokalnej usługi Active są toolog skonfigurowany przy użyciu @contoso.uk, a następnie te użytkownicy nie będą mogli toocorrectly Zaloguj się do hello ARA kolekcji.</span><span class="sxs-lookup"><span data-stu-id="32eb3-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured toolog in with @contoso.uk, then those users will not be able toocorrectly log into hello ARA collection.</span></span> <span data-ttu-id="32eb3-118">Użytkownicy muszą mieć nazwy UPN w usłudze AAD i AD hello takie same dla możliwości toobe logowania hello"</span><span class="sxs-lookup"><span data-stu-id="32eb3-118">Users UPN in AAD and AD must be hello same for hello login toobe possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="32eb3-119">Tworzenie obiektów dla usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="32eb3-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="32eb3-120">Należy również hello toocreate po lokalnych obiektów usługi Active Directory:</span><span class="sxs-lookup"><span data-stu-id="32eb3-120">You also need toocreate hello following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="32eb3-121">Usługa konta tooprovide dostępu toodomain zasobów dla programów RemoteApp przez dołączenie RDSH punktów końcowych toohello lokalnej domeny.</span><span class="sxs-lookup"><span data-stu-id="32eb3-121">A service account tooprovide access toodomain resources for RemoteApp programs by joining RDSH end points toohello on-premises domain.</span></span>
* <span data-ttu-id="32eb3-122">Jednostki organizacyjnej (OU) toocontain RemoteApp obiekty komputera.</span><span class="sxs-lookup"><span data-stu-id="32eb3-122">An Organizational Unit (OU) toocontain RemoteApp machine objects.</span></span> <span data-ttu-id="32eb3-123">Użycie hello jednostki Organizacyjnej jest konta hello tooisolate zalecane (ale nie są wymagane) i zasad, które będą używane z usługą RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="32eb3-123">Use of hello OU is recommended (but not required) tooisolate hello accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="32eb3-124">Oba te obiekty potrzebne podczas tworzenia kolekcji usługi RemoteApp, więc najpierw należy toodo się, że te kroki.</span><span class="sxs-lookup"><span data-stu-id="32eb3-124">You need both of these objects when you create your RemoteApp collection, so be sure toodo these steps first.</span></span>

