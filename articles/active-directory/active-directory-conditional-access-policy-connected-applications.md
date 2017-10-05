---
title: "Konfigurowanie zasad dostępu warunkowego opartego na urządzenia usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania zasad dostępu warunkowego opartego na urządzenia usługi Azure Active Directory."
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
ms.openlocfilehash: a26c40351c6b982fd90acb4bf06220ef3f79f399
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a><span data-ttu-id="72e08-103">Konfigurowanie zasad dostępu warunkowego opartego na urządzenia usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72e08-103">Configure Azure Active Directory device-based conditional access policies</span></span>

<span data-ttu-id="72e08-104">Z [dostępu warunkowego w usłudze Azure Active Directory (Azure AD)](active-directory-conditional-access-azure-portal.md), można dostosować sposób autoryzowani użytkownicy mają dostęp do zasobów.</span><span class="sxs-lookup"><span data-stu-id="72e08-104">With [Azure Active Directory (Azure AD) conditional access](active-directory-conditional-access-azure-portal.md), you can fine-tune how authorized users can access your resources.</span></span> <span data-ttu-id="72e08-105">Na przykład ograniczyć dostęp do niektórych zasobów do zaufanych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="72e08-105">For example, you limit the access to certain resources to trusted devices.</span></span> <span data-ttu-id="72e08-106">Zasady dostępu warunkowego, która wymaga zaufanego urządzenia jest nazywana zasad dostępu warunkowego opartego na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="72e08-106">A conditional access policy that requires a trusted device is also known as device-based conditional access policy.</span></span>

<span data-ttu-id="72e08-107">Ten temat zawiera informacje dotyczące sposobu konfigurowania zasad dostępu warunkowego opartego na urządzeniu dla Azure AD połączonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="72e08-107">This topic provides you with information on how to configure device-based conditional access policies for Azure AD-connected applications.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="72e08-108">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="72e08-108">Before you begin</span></span>

<span data-ttu-id="72e08-109">Ties dostępu warunkowego opartego na urządzeniu **dostępu warunkowego dla usługi Azure AD** i **zarządzania urządzeniami usługi Azure AD razem**.</span><span class="sxs-lookup"><span data-stu-id="72e08-109">Device-based conditional access ties **Azure AD conditional access** and **Azure AD device management together**.</span></span> <span data-ttu-id="72e08-110">Jeśli nie masz doświadczenia z jednym z tych obszarów jeszcze, najpierw należy przeczytać następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="72e08-110">If you are not familiar with one of these areas yet, you should read the following topics, first:</span></span>

- <span data-ttu-id="72e08-111">**[Dostęp warunkowy w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal.md)**  — ten temat zawiera omówienie pojęć dotyczących dostępu warunkowego i terminologię pokrewne.</span><span class="sxs-lookup"><span data-stu-id="72e08-111">**[Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)** - This topic provides you with a conceptual overview of conditional access and the related terminology.</span></span>

- <span data-ttu-id="72e08-112">**[Wprowadzenie do zarządzania urządzeniami w usłudze Azure Active Directory](device-management-introduction.md)**  — ten temat zawiera omówienie różnych opcji, należy podłączyć urządzenia z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72e08-112">**[Introduction to device management in Azure Active Directory](device-management-introduction.md)** - This topic gives you an overview of the various options you have to connect devices with Azure AD.</span></span> 


## <a name="trusted-devices"></a><span data-ttu-id="72e08-113">Zaufanych urządzeń</span><span class="sxs-lookup"><span data-stu-id="72e08-113">Trusted devices</span></span>

<span data-ttu-id="72e08-114">W świecie pierwszy mobile, najpierw chmury Azure Active Directory umożliwia logowanie jednokrotne do urządzeń, aplikacji i usług z dowolnego miejsca.</span><span class="sxs-lookup"><span data-stu-id="72e08-114">In a mobile-first, cloud-first world, Azure Active Directory enables single sign-on to devices, apps, and services from anywhere.</span></span> <span data-ttu-id="72e08-115">Dla niektórych zasobów w danym środowisku, udzielanie dostępu do odpowiednich użytkowników może nie być wystarczająca.</span><span class="sxs-lookup"><span data-stu-id="72e08-115">For certain resources in your environment, granting access to the right users might not be good enough.</span></span> <span data-ttu-id="72e08-116">Oprócz odpowiednich użytkowników może również wymagać zaufanego urządzenia ma być używany do uzyskania dostępu do zasobu.</span><span class="sxs-lookup"><span data-stu-id="72e08-116">In addition to the right users, you might also require a trusted device to be used to access a resource.</span></span> <span data-ttu-id="72e08-117">W danym środowisku, można zdefiniować zaufanego urządzenia oparte na następujących składników:</span><span class="sxs-lookup"><span data-stu-id="72e08-117">In your environment, you can define what a trusted device is based on the following components:</span></span>

- <span data-ttu-id="72e08-118">[Platform urządzeń](active-directory-conditional-access-azure-portal.md#device-platforms) na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="72e08-118">The [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) on a device</span></span>
- <span data-ttu-id="72e08-119">Określa, czy urządzenie jest zgodne</span><span class="sxs-lookup"><span data-stu-id="72e08-119">Whether a device is compliant</span></span>
- <span data-ttu-id="72e08-120">Określa, czy urządzenie jest przyłączony do domeny</span><span class="sxs-lookup"><span data-stu-id="72e08-120">Whether a device is domain-joined</span></span> 

<span data-ttu-id="72e08-121">[Platform urządzeń](active-directory-conditional-access-azure-portal.md#device-platforms) charakteryzuje się systemu operacyjnego, który działa na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="72e08-121">The [device platforms](active-directory-conditional-access-azure-portal.md#device-platforms) is characterized by the operating system that is running on your device.</span></span> <span data-ttu-id="72e08-122">W zasadach dostępu warunkowego opartego na urządzeniu można ograniczyć dostęp do niektórych zasobów do konkretnych platform sprzętowych.</span><span class="sxs-lookup"><span data-stu-id="72e08-122">In your device-based conditional access policy, you can limit access to certain resources to specific device platforms.</span></span>



<span data-ttu-id="72e08-123">W zasadach dostępu warunkowego opartego na urządzeniu można wymagać zaufanych urządzeń może być oznaczony jako zgodne.</span><span class="sxs-lookup"><span data-stu-id="72e08-123">In a device-based conditional access policy, you can require trusted devices to be marked as compliant.</span></span>

![Aplikacje w chmurze](./media/active-directory-conditional-access-policy-connected-applications/24.png)

<span data-ttu-id="72e08-125">Urządzenia może być oznaczony jako zgodne w katalogu przez:</span><span class="sxs-lookup"><span data-stu-id="72e08-125">Devices can be marked as compliant in the directory by:</span></span>

- <span data-ttu-id="72e08-126">Usługi Intune</span><span class="sxs-lookup"><span data-stu-id="72e08-126">Intune</span></span> 
- <span data-ttu-id="72e08-127">System zarządzania urządzeniami przenośnymi innej firmy, która integruje się z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="72e08-127">A third-party mobile device management system that integrates with Azure AD</span></span>  

<span data-ttu-id="72e08-128">Tylko urządzenia, które są połączone z usługą Azure AD może być oznaczony jako zgodne.</span><span class="sxs-lookup"><span data-stu-id="72e08-128">Only devices that are connected to Azure AD can be marked as compliant.</span></span> <span data-ttu-id="72e08-129">Podłącz urządzenie do usługi Azure Active Directory, masz następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="72e08-129">To connect a device to Azure Active Directory, you have the following options:</span></span> 

- <span data-ttu-id="72e08-130">Azure AD w zarejestrowany</span><span class="sxs-lookup"><span data-stu-id="72e08-130">Azure AD registered</span></span>
- <span data-ttu-id="72e08-131">Azure AD dołączony</span><span class="sxs-lookup"><span data-stu-id="72e08-131">Azure AD joined</span></span>
- <span data-ttu-id="72e08-132">Hybrydowe przyłączonych do usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="72e08-132">Hybrid Azure AD joined</span></span>

    ![Aplikacje w chmurze](./media/active-directory-conditional-access-policy-connected-applications/26.png)

<span data-ttu-id="72e08-134">Jeśli masz nakłady zasobów lokalnej usługi Active Directory (AD), można rozważyć urządzeń, które nie są podłączone do usługi Azure AD, ale przyłączony do usługi AD jako zaufane.</span><span class="sxs-lookup"><span data-stu-id="72e08-134">If you have an on-premises Active Directory (AD) footprint, you might consider devices that are not connected to Azure AD but joined to your AD to be trusted.</span></span>

![Aplikacje w chmurze](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a><span data-ttu-id="72e08-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="72e08-136">Next steps</span></span>

<span data-ttu-id="72e08-137">Przed skonfigurowaniem zasad dostępu warunkowego opartego na urządzeniu w danym środowisku, należy podjąć przyjrzeć się [najlepszych rozwiązań dotyczących dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="72e08-137">Before configuring a device-based conditional access policy in your environment, you should take a look at the [best practices for conditional access in Azure Active Directory](active-directory-conditional-access-best-practices.md).</span></span>

