---
title: "Weryfikacja dwuetapowa i usługi AD FS — Azure MFA | Microsoft Docs"
description: "Ta strona dotyczy usługi Azure Multi-Factor Authentication i zawiera informacje umożliwiające rozpoczęcie korzystania z usługi Azure MFA i usług AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 28aede545c738137ff04257214e4a3f42792d85c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="e7c6d-103">Wprowadzenie do usługi Azure Multi-Factor Authentication i usług Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="e7c6d-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="e7c6d-104"><center>![Chmura](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="e7c6d-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="e7c6d-105">W przypadku organizacji, które sfederowały lokalną usługę Active Directory z usługą Azure Active Directory za pomocą usług AD FS, dostępne są dwie opcje używania usługi Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="e7c6d-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="e7c6d-106">Zabezpieczenie zasobów w chmurze za pomocą usługi Azure Multi-Factor Authentication lub usług Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="e7c6d-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="e7c6d-107">Zabezpieczenie zasobów w chmurze i zasobów lokalnych przy użyciu serwera usługi Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="e7c6d-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="e7c6d-108">Poniższa tabela zawiera podsumowanie obsługi weryfikacji w przypadku zabezpieczania zasobów za pomocą usługi Azure Multi-Factor Authentication i usług AD FS</span><span class="sxs-lookup"><span data-stu-id="e7c6d-108">The following table summarizes the verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="e7c6d-109">Proces weryfikacji — aplikacje korzystające z przeglądarki</span><span class="sxs-lookup"><span data-stu-id="e7c6d-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="e7c6d-110">Proces weryfikacji — aplikacje niekorzystające z przeglądarki</span><span class="sxs-lookup"><span data-stu-id="e7c6d-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e7c6d-111">Zabezpieczanie zasobów usługi Azure AD za pomocą usługi Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="e7c6d-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="e7c6d-112">Pierwszy etap weryfikacji odbywa się lokalnie przy użyciu usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="e7c6d-112">The first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="e7c6d-113">Drugi etap polega na użyciu metody telefonicznej, która obejmuje uwierzytelnianie w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e7c6d-113">The second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="e7c6d-114">Zabezpieczanie zasobów usługi Azure AD za pomocą usług Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="e7c6d-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="e7c6d-115">Pierwszy etap weryfikacji odbywa się lokalnie przy użyciu usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="e7c6d-115">The first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="e7c6d-116">Drugi etap odbywa się lokalnie i polega na uznaniu oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="e7c6d-116">The second step is performed on-premises by honoring the claim.</span></span></li> |

<span data-ttu-id="e7c6d-117">Zastrzeżenia dotyczące haseł aplikacji używanych przez użytkowników federacyjnych:</span><span class="sxs-lookup"><span data-stu-id="e7c6d-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="e7c6d-118">Hasła aplikacji są weryfikowane przy użyciu uwierzytelniania w chmurze, co pozwala pominąć federację.</span><span class="sxs-lookup"><span data-stu-id="e7c6d-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="e7c6d-119">Federacja jest aktywnie używana tylko podczas konfigurowania hasła aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e7c6d-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="e7c6d-120">Ustawienia lokalnej kontroli dostępu klienta nie są uznawane przez hasła aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e7c6d-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="e7c6d-121">Nie będzie można lokalnie rejestrować uwierzytelniania haseł aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e7c6d-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="e7c6d-122">Wyłączenie/usunięcie konta przy użyciu narzędzia do synchronizacji katalogów może potrwać do 3 godzin, powodując opóźnienie wyłączenia/usunięcia haseł aplikacji w tożsamości w chmurze.</span><span class="sxs-lookup"><span data-stu-id="e7c6d-122">Account disable/deletion may take up to three hours for directory sync, delaying disable/deletion of app passwords in the cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7c6d-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e7c6d-123">Next steps</span></span>
<span data-ttu-id="e7c6d-124">Aby uzyskać informacje dotyczące konfigurowania usługi Azure Multi-Factor Authentication lub serwera usługi Azure Multi-Factor Authentication z usługami AD FS, zobacz poniższe artykuły:</span><span class="sxs-lookup"><span data-stu-id="e7c6d-124">For information on setting up either Azure Multi-Factor Authentication or the Azure Multi-Factor Authentication Server with AD FS, see the following articles:</span></span>

* [<span data-ttu-id="e7c6d-125">Zabezpieczanie zasobów w chmurze przy użyciu usługi Azure Multi-Factor Authentication i usług AD FS</span><span class="sxs-lookup"><span data-stu-id="e7c6d-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="e7c6d-126">Zabezpieczanie zasobów w chmurze i lokalnych przy użyciu serwera usługi Azure Multi-Factor Authentication i usług AD FS systemu Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="e7c6d-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="e7c6d-127">Zabezpieczanie zasobów w chmurze i zasobów lokalnych przy użyciu serwera usługi Azure Multi-Factor Authentication i usług AD FS 2.0</span><span class="sxs-lookup"><span data-stu-id="e7c6d-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
