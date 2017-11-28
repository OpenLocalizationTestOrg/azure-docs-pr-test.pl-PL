---
title: "tooapplications użytkowników tooAssign aaaHow | Dokumentacja firmy Microsoft"
description: "Zrozumienie, jak użytkownicy zostaną przypisane tooan aplikacji w Twojej dzierżawie"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a><span data-ttu-id="bbf4a-103">Jak tooassign tooapplications użytkowników</span><span class="sxs-lookup"><span data-stu-id="bbf4a-103">How tooassign users tooapplications</span></span>

<span data-ttu-id="bbf4a-104">W tym artykule pomocy toounderstand jak użytkownicy zostaną przypisane tooan aplikacji w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="bbf4a-104">This article help you toounderstand how users get assigned tooan application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a><span data-ttu-id="bbf4a-105">Jak użytkownicy zostaną przypisane tooan aplikacji w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="bbf4a-105">How do users get assigned tooan application in Azure AD?</span></span>

<span data-ttu-id="bbf4a-106">Dla tooaccess użytkownika aplikacji one należy przypisać tooit w określony sposób.</span><span class="sxs-lookup"><span data-stu-id="bbf4a-106">For a user tooaccess an application, they must first be assigned tooit in some way.</span></span> <span data-ttu-id="bbf4a-107">Przypisanie może zostać wykonana przez administratora, delegat biznesowych lub czasami użytkownika hello samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="bbf4a-107">Assignment can be performed by an administrator, a business delegate, or sometimes, hello user themselves.</span></span> <span data-ttu-id="bbf4a-108">Poniżej opisano sposoby hello, które użytkownicy mogą zostać przypisani tooapplications:</span><span class="sxs-lookup"><span data-stu-id="bbf4a-108">Below describes hello ways users can get assigned tooapplications:</span></span>

1.  <span data-ttu-id="bbf4a-109">Administrator [przypisuje użytkownika](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello aplikacji bezpośrednio</span><span class="sxs-lookup"><span data-stu-id="bbf4a-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello application directly</span></span>

2.  <span data-ttu-id="bbf4a-110">Administrator [przypisuje grupę](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) hello użytkownik jest członkiem toohello aplikacji, w tym:</span><span class="sxs-lookup"><span data-stu-id="bbf4a-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that hello user is a member of toohello application, including:</span></span>

  * <span data-ttu-id="bbf4a-111">Grupy, która była synchronizowana z lokalnymi</span><span class="sxs-lookup"><span data-stu-id="bbf4a-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="bbf4a-112">Grupy zabezpieczeń statycznych utworzone w chmurze hello</span><span class="sxs-lookup"><span data-stu-id="bbf4a-112">A static security group created in hello cloud</span></span>

  * <span data-ttu-id="bbf4a-113">A [grupy zabezpieczeń dynamiczne](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) utworzone w chmurze hello</span><span class="sxs-lookup"><span data-stu-id="bbf4a-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in hello cloud</span></span>

  * <span data-ttu-id="bbf4a-114">Grupy usługi Office 365 utworzone w chmurze hello</span><span class="sxs-lookup"><span data-stu-id="bbf4a-114">An Office 365 group created in hello cloud</span></span>

  * <span data-ttu-id="bbf4a-115">Witaj [wszyscy użytkownicy](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) grupy</span><span class="sxs-lookup"><span data-stu-id="bbf4a-115">hello [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="bbf4a-116">Administrator włączy [samoobsługi dostęp do aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow tooadd użytkownika, przy użyciu aplikacji hello [panelu dostępu aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Dodaj aplikację** funkcji **bez zatwierdzenia biznesowa**</span><span class="sxs-lookup"><span data-stu-id="bbf4a-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="bbf4a-117">Administrator włączy [samoobsługi dostęp do aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow tooadd użytkownika, przy użyciu aplikacji hello [panelu dostępu aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Dodaj aplikację** funkcji, ale tylko w **i pobieraniu z zestawu wybranych osób zatwierdzających biznesowa**</span><span class="sxs-lookup"><span data-stu-id="bbf4a-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow a user tooadd an application using hello [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="bbf4a-118">Administrator włączy [Samoobsługowe zarządzanie grupami](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow toojoin użytkownika grupy aplikacji przypisany zbyt**bez zatwierdzenia biznesowa**</span><span class="sxs-lookup"><span data-stu-id="bbf4a-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned too**without business approval**</span></span>

6.  <span data-ttu-id="bbf4a-119">Administrator włączy [Samoobsługowe zarządzanie grupami](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow toojoin użytkownika grupę, której aplikacja jest przypisany do, ale tylko **o pobieraniu z zestawu wybranych osób zatwierdzających biznesowa**</span><span class="sxs-lookup"><span data-stu-id="bbf4a-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow a user toojoin a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="bbf4a-120">Administrator przypisuje tooa licencji użytkownika bezpośrednio do pierwszej strony aplikacji, tak samo, jak [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="bbf4a-120">An administrator assigns a license tooa user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="bbf4a-121">Przypisuje administratora grupy tooa licencji, która hello użytkownika jest członkiem tooa pierwszej aplikacji firm, takich jak [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="bbf4a-121">An administrator assigns a license tooa group that hello user is a member of tooa first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="bbf4a-122">[Administrator wyrazi na to zgody aplikacji tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe używane przez wszystkich użytkowników, a następnie użytkownik loguje się toohello aplikacji</span><span class="sxs-lookup"><span data-stu-id="bbf4a-122">An [administrator consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe used by all users and then a user signs in toohello application</span></span>

10. <span data-ttu-id="bbf4a-123">Użytkownik [zgadza aplikacji tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) się po zarejestrowaniu się w aplikacji toohello</span><span class="sxs-lookup"><span data-stu-id="bbf4a-123">A user [consents tooan application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in toohello application</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbf4a-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bbf4a-124">Next steps</span></span>
[<span data-ttu-id="bbf4a-125">Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbf4a-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
