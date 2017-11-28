---
title: "zasady dostępu warunkowego opartego na urządzenia usługi Azure Active Directory aaaConfigure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zasady dostępu warunkowego opartego na urządzeniach usługi Azure Active Directory tooconfigure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="86b7e-103">Konfigurowanie zasad dostępu warunkowego opartego na urządzenia usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86b7e-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="86b7e-104">Z [dostępu warunkowego w usłudze Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md), można dostosować sposób autoryzowani użytkownicy mają dostęp do zasobów.</span><span class="sxs-lookup"><span data-stu-id="86b7e-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="86b7e-105">Na przykład można ograniczyć hello toocertain zasobów tootrusted urządzeń.</span><span class="sxs-lookup"><span data-stu-id="86b7e-105">For example, you limit hello access toocertain resources tootrusted devices.</span></span> <span data-ttu-id="86b7e-106">Zasady dostępu warunkowego, która wymaga zaufanego urządzenia jest nazywana zasad dostępu warunkowego opartego na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="86b7e-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="86b7e-107">Ten temat zawiera informacje o jak zasady dla aplikacji połączone AD Azure dostępu warunkowego opartego na urządzeniach tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="86b7e-107">This topic provides you with information on how tooconfigure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="86b7e-108">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="86b7e-108">Before you begin</span></span>

<span data-ttu-id="86b7e-109">Ties dostępu warunkowego opartego na urządzeniu **dostępu warunkowego dla usługi Azure AD** i **zarządzania urządzeniami usługi Azure AD razem**.</span><span class="sxs-lookup"><span data-stu-id="86b7e-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="86b7e-110">Jeśli nie masz doświadczenia z jednym z tych obszarów jeszcze, należy przeczytać następujące tematy, najpierw hello:</span><span class="sxs-lookup"><span data-stu-id="86b7e-110">If you are not familiar with one of these areas yet, you should read hello following topics, first:</span></span>

- <span data-ttu-id="86b7e-111">**[Dostęp warunkowy w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal.md)**  — w tym temacie przedstawiono u omówienie warunkowego dostępu i hello terminologii pokrewne.</span><span class="sxs-lookup"><span data-stu-id="86b7e-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and hello related terminology.</span></span>

- <span data-ttu-id="86b7e-112">**[Wprowadzenie toodevice zarządzania w usłudze Azure Active Directory](device-management-introduction.md)**  — ten temat zawiera omówienie programu hello różne opcje masz tooconnect urządzeń z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86b7e-112">**[Introduction toodevice management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of hello various options you have tooconnect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="86b7e-113">Zaufanych urządzeń</span><span class="sxs-lookup"><span data-stu-id="86b7e-113">Trusted devices</span></span>

<span data-ttu-id="86b7e-114">W świecie pierwszy mobile, najpierw chmury Azure Active Directory umożliwia toodevices rejestracji jednokrotnej, aplikacji i usług z dowolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="86b7e-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="86b7e-115">Dla niektórych zasobów w danym środowisku, udzielanie dostępu wybranym użytkownikom toohello może nie być wystarczająca.</span><span class="sxs-lookup"><span data-stu-id="86b7e-115">For certain resources in your environment, granting access toohello right users might not be good enough.</span></span> <span data-ttu-id="86b7e-116">Ponadto toohello odpowiednich użytkowników, użytkownik może wymagać toobe zaufanego urządzenia używane tooaccess zasobu.</span><span class="sxs-lookup"><span data-stu-id="86b7e-116">In addition toohello right users, you might also require a trusted device toobe used tooaccess a resource.</span></span> <span data-ttu-id="86b7e-117">W danym środowisku, można zdefiniować, co to jest oparta na zaufanym urządzeniu hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="86b7e-117">In your environment, you can define what a trusted device is based on hello following components:</span></span>

- <span data-ttu-id="86b7e-118">Witaj [platform urządzeń](active-directory-conditional-access-azure-portal.md#device-platforms) na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="86b7e-118">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="86b7e-119">Określa, czy urządzenie jest zgodne</span><span class="sxs-lookup"><span data-stu-id="86b7e-119">Whether a device is compliant</span></span>
- <span data-ttu-id="86b7e-120">Określa, czy urządzenie jest przyłączony do domeny</span><span class="sxs-lookup"><span data-stu-id="86b7e-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="86b7e-121">Witaj [platform urządzeń](active-directory-conditional-access-azure-portal.md#device-platforms) charakteryzuje się hello systemu operacyjnego, który działa na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="86b7e-121">hello [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by hello operating system that is running on your device.</span></span> <span data-ttu-id="86b7e-122">W zasadach dostępu warunkowego opartego na urządzeniu można ograniczyć platform urządzeń toospecific dostępu toocertain zasobów.</span><span class="sxs-lookup"><span data-stu-id="86b7e-122">In your device-based conditional access policy, you can limit access toocertain resources toospecific device platforms.</span></span>



<span data-ttu-id="86b7e-123">W zasadach dostępu warunkowego opartego na urządzeniu można wymagać toobe zaufanych urządzeń oznaczone jako zgodne.</span><span class="sxs-lookup"><span data-stu-id="86b7e-123">In a device-based conditional access policy, you can require trusted devices toobe marked as compliant.</span></span>

![Aplikacje w chmurze](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="86b7e-125">Urządzenia może być oznaczony jako zgodne w katalogu hello przez:</span><span class="sxs-lookup"><span data-stu-id="86b7e-125">Devices can be marked as compliant in hello directory by:</span></span>

- <span data-ttu-id="86b7e-126">Usługi Intune</span><span class="sxs-lookup"><span data-stu-id="86b7e-126">Intune</span></span> 
- <span data-ttu-id="86b7e-127">System zarządzania urządzeniami przenośnymi innej firmy, która integruje się z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="86b7e-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="86b7e-128">Tylko urządzenia, które są połączone tooAzure AD może być oznaczony jako zgodne.</span><span class="sxs-lookup"><span data-stu-id="86b7e-128">Only devices that are connected tooAzure AD can be marked as compliant.</span></span> <span data-ttu-id="86b7e-129">tooconnect tooAzure urządzenia usługi Active Directory, masz hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="86b7e-129">tooconnect a device tooAzure Active Directory, you have hello following options:</span></span> 

- <span data-ttu-id="86b7e-130">Azure AD w zarejestrowany</span><span class="sxs-lookup"><span data-stu-id="86b7e-130">Azure AD registered</span></span>
- <span data-ttu-id="86b7e-131">Azure AD dołączony</span><span class="sxs-lookup"><span data-stu-id="86b7e-131">Azure AD joined</span></span>
- <span data-ttu-id="86b7e-132">Hybrydowe przyłączonych do usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="86b7e-132">Hybrid Azure AD joined</span></span>

    ![Aplikacje w chmurze](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="86b7e-134">Jeśli masz nakłady zasobów lokalnej usługi Active Directory (AD), można rozważyć urządzeń, które nie są połączone tooAzure AD, ale toobe sprzężonych tooyour AD zaufane.</span><span class="sxs-lookup"><span data-stu-id="86b7e-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected tooAzure AD but joined tooyour AD toobe trusted.</span></span>

![Aplikacje w chmurze](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="86b7e-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86b7e-136">Next steps</span></span>

<span data-ttu-id="86b7e-137">Przed skonfigurowaniem zasad dostępu warunkowego opartego na urządzeniu w danym środowisku, należy podjąć przyjrzeć się hello [najlepszych rozwiązań dotyczących dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="86b7e-137">Before configuring a device-based conditional access policy in your environment, you should take a look at hello [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

