---
title: "aaaFederating wielu usługi Azure AD z jednym usług AD FS | Dokumentacja firmy Microsoft"
description: "W tym dokumencie przedstawiono sposób toofederate wielu usługi Azure AD z jednym usług AD FS."
keywords: federate, ADFS, AD FS, multiple tenants, single AD FS, one ADFS, multi-tenant federation, multi-forest adfs, aad connect, federation, cross-tenant federation
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 442192896b3b13f7bf9388396cd3769e194329d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="d69ad-104">Federowanie wielu wystąpień usługi Azure AD przy użyciu jednego wystąpienia usługi AD FS</span><span class="sxs-lookup"><span data-stu-id="d69ad-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="d69ad-105">Pojedyncza farma usługi AD FS o wysokiej dostępności może federować wiele lasów, jeśli istnieje między nimi dwukierunkowa relacja zaufania.</span><span class="sxs-lookup"><span data-stu-id="d69ad-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="d69ad-106">Wiele lasów może lub nie może odpowiadać toohello usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d69ad-106">These multiple forests may or may not correspond toohello same Azure Active Directory.</span></span> <span data-ttu-id="d69ad-107">Ten artykuł zawiera instrukcje jak tooconfigure federacji między pojedynczego wdrożenia usług AD FS i więcej niż jeden lasach toodifferent tej synchronizacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d69ad-107">This article provides instructions on how tooconfigure federation between a single AD FS deployment and more than one forests that sync toodifferent Azure AD.</span></span>

![Federacja wielu dzierżaw z jedną usługą AD FS](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="d69ad-109">W tym scenariuszu nie jest obsługiwane zapisywanie zwrotne urządzeń ani automatyczne dołączanie urządzeń.</span><span class="sxs-lookup"><span data-stu-id="d69ad-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="d69ad-110">Azure AD Connect nie może być federacyjnego tooconfigure używane w tym scenariuszu, jak Azure AD Connect można skonfigurować Federacji domen w jednej usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d69ad-110">Azure AD Connect cannot be used tooconfigure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="d69ad-111">Kroki umożliwiające federowanie usługi AD FS z wieloma usługami Azure AD</span><span class="sxs-lookup"><span data-stu-id="d69ad-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="d69ad-112">Należy rozważyć domeny contoso.com w usłudze Azure Active Directory contoso.onmicrosoft.com już jest Sfederowane przy użyciu hello usług AD FS lokalnie zainstalowane w środowisku usługi Active Directory lokalnymi contoso.com.</span><span class="sxs-lookup"><span data-stu-id="d69ad-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with hello AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="d69ad-113">Fabrikam.com to domena w usłudze Azure Active Directory fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="d69ad-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

##<a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="d69ad-114">Krok 1. Ustanów dwukierunkową relację zaufania</span><span class="sxs-lookup"><span data-stu-id="d69ad-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="d69ad-115">Usługi AD FS w użytkownicy mogli tooauthenticate toobe contoso.com fabrikam.com potrzeby dwukierunkową relację zaufania między contoso.com i fabrikam.com. Wykonaj wytyczne hello na tym [artykułu](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello dwukierunkowe zaufanie.</span><span class="sxs-lookup"><span data-stu-id="d69ad-115">For AD FS in contoso.com toobe able tooauthenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com. Follow hello guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello two-way trust.</span></span>
 
##<a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="d69ad-116">Krok 2. Zmodyfikuj ustawienia federacji domeny contoso.com</span><span class="sxs-lookup"><span data-stu-id="d69ad-116">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="d69ad-117">Witaj wystawca domyślne ustawiony tooAD pojedynczej domeny federacyjnej FS jest "http://ADFSServiceFQDN/adfs/services/trust", na przykład "http://fs.contoso.com/adfs/services/trust".</span><span class="sxs-lookup"><span data-stu-id="d69ad-117">hello default issuer set for a single domain federated tooAD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="d69ad-118">Usługa Azure Active Directory wymaga unikatowego wystawcy dla każdej domeny federacyjnej.</span><span class="sxs-lookup"><span data-stu-id="d69ad-118">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="d69ad-119">Ponieważ hello tej samej usługi AD FS będzie toofederate dwie domeny, wartości wystawcy hello musi toobe zmodyfikować tak, aby jest unikatowa dla każdej domeny usług AD FS federates w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d69ad-119">Since hello same AD FS is going toofederate two domains, hello issuer value needs toobe modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="d69ad-120">Na serwerze hello usług AD FS Otwórz program Azure AD PowerShell i wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d69ad-120">On hello AD FS server, open Azure AD PowerShell and perform hello following steps:</span></span>
 
<span data-ttu-id="d69ad-121">Połącz toohello usługi Azure Active Directory zawierającą hello domeny contoso.com Connect MsolService hello federacyjnego ustawienia aktualizacji dla domeny contoso.com Update MsolFederatedDomain - DomainName contoso.com — SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="d69ad-121">Connect toohello Azure Active Directory that contains hello domain contoso.com Connect-MsolService Update hello federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="d69ad-122">Wystawca w ustawienia Federacji domen hello zostaną zmienione za "http://contoso.com/adfs/services/trust" i wystawiania oświadczenia, reguła zostanie dodany do hello Azure AD zaufania jednostki uzależnionej tooissue hello poprawną wartość issuerId oparta na powitania sufiks nazwy UPN.</span><span class="sxs-lookup"><span data-stu-id="d69ad-122">Issuer in hello domain federation setting will be changed too"http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for hello Azure AD Relying Party Trust tooissue hello correct issuerId value based on hello UPN suffix.</span></span>
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="d69ad-123">Krok 3. Sfederuj domenę fabrikam.com z usługą AD FS</span><span class="sxs-lookup"><span data-stu-id="d69ad-123">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="d69ad-124">W programie Azure AD powershell sesja wykonać hello następujące kroki: Połącz tooAzure usługi Active Directory zawiera hello fabrikam.com domeny</span><span class="sxs-lookup"><span data-stu-id="d69ad-124">In Azure AD powershell session perform hello following steps: Connect tooAzure Active Directory that contains hello domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="d69ad-125">Konwertuj toofederated domeny fabrikam.com zarządzane hello:</span><span class="sxs-lookup"><span data-stu-id="d69ad-125">Convert hello fabrikam.com managed domain toofederated:</span></span>

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="d69ad-126">Witaj powyżej operacji będzie Federację hello fabrikam.com domeny z hello tej samej usługi AD FS.</span><span class="sxs-lookup"><span data-stu-id="d69ad-126">hello above operation will federate hello domain fabrikam.com with hello same AD FS.</span></span> <span data-ttu-id="d69ad-127">Ustawienia domeny hello można sprawdzić, za pomocą Get MsolDomainFederationSettings dla obu domen.</span><span class="sxs-lookup"><span data-stu-id="d69ad-127">You can verify hello domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d69ad-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d69ad-128">Next steps</span></span>
[<span data-ttu-id="d69ad-129">Łączenie usługi Active Directory z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d69ad-129">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
