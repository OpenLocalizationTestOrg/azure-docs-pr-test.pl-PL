---
title: "Jak przypisać użytkowników do aplikacji | Dokumentacja firmy Microsoft"
description: "Zrozumienie, jak użytkownicy zostaną przypisane do aplikacji w Twojej dzierżawie"
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
ms.openlocfilehash: 916238ba402a2555bac620d7f08e02799d981ae0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-assign-users-to-applications"></a><span data-ttu-id="f28a9-103">Jak przypisać użytkowników do aplikacji</span><span class="sxs-lookup"><span data-stu-id="f28a9-103">How to assign users to applications</span></span>

<span data-ttu-id="f28a9-104">Ten artykuł ułatwia zrozumienie, jak użytkownicy zostaną przypisane do aplikacji w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="f28a9-104">This article help you to understand how users get assigned to an application in your tenant.</span></span>

## <a name="how-do-users-get-assigned-to-an-application-in-azure-ad"></a><span data-ttu-id="f28a9-105">Jak użytkownicy zostaną przypisane do aplikacji w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="f28a9-105">How do users get assigned to an application in Azure AD?</span></span>

<span data-ttu-id="f28a9-106">Aby użytkownik mógł uzyskać dostęp do aplikacji ich należy przypisać do niej w określony sposób.</span><span class="sxs-lookup"><span data-stu-id="f28a9-106">For a user to access an application, they must first be assigned to it in some way.</span></span> <span data-ttu-id="f28a9-107">Przypisanie może zostać wykonana przez administratora, delegata biznesowych lub czasami użytkownik samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="f28a9-107">Assignment can be performed by an administrator, a business delegate, or sometimes, the user themselves.</span></span> <span data-ttu-id="f28a9-108">Poniżej opisano sposoby, które użytkownicy mogą zostać przypisani do aplikacji:</span><span class="sxs-lookup"><span data-stu-id="f28a9-108">Below describes the ways users can get assigned to applications:</span></span>

1.  <span data-ttu-id="f28a9-109">Administrator [przypisuje użytkownika](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) bezpośrednio w aplikacji</span><span class="sxs-lookup"><span data-stu-id="f28a9-109">An administrator [assigns a user](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) to the application directly</span></span>

2.  <span data-ttu-id="f28a9-110">Administrator [przypisuje grupę](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) czy użytkownik jest członkiem do aplikacji, w tym:</span><span class="sxs-lookup"><span data-stu-id="f28a9-110">An administrator [assigns a group](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) that the user is a member of to the application, including:</span></span>

  * <span data-ttu-id="f28a9-111">Grupy, która była synchronizowana z lokalnymi</span><span class="sxs-lookup"><span data-stu-id="f28a9-111">A group that was synchronized from on-premises</span></span>

  * <span data-ttu-id="f28a9-112">Grupy zabezpieczeń statycznych utworzone w chmurze</span><span class="sxs-lookup"><span data-stu-id="f28a9-112">A static security group created in the cloud</span></span>

  * <span data-ttu-id="f28a9-113">A [grupy zabezpieczeń dynamiczne](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) utworzone w chmurze</span><span class="sxs-lookup"><span data-stu-id="f28a9-113">A [dynamic security group](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) created in the cloud</span></span>

  * <span data-ttu-id="f28a9-114">Grupy usługi Office 365 utworzone w chmurze</span><span class="sxs-lookup"><span data-stu-id="f28a9-114">An Office 365 group created in the cloud</span></span>

  * <span data-ttu-id="f28a9-115">[Wszyscy użytkownicy](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) grupy</span><span class="sxs-lookup"><span data-stu-id="f28a9-115">The [All Users](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) group</span></span>

3.  <span data-ttu-id="f28a9-116">Administrator włączy [samoobsługi dostęp do aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) Aby zezwolić użytkownikowi na dodawanie aplikacji przy użyciu [panelu dostępu aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Dodaj aplikację** funkcji **bez zatwierdzenia biznesowa**</span><span class="sxs-lookup"><span data-stu-id="f28a9-116">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**</span></span>

4.  <span data-ttu-id="f28a9-117">Administrator włączy [samoobsługi dostęp do aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) Aby zezwolić użytkownikowi na dodawanie aplikacji przy użyciu [panelu dostępu aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Dodaj aplikację** funkcji, ale tylko w**i pobieraniu z zestawu wybranych osób zatwierdzających biznesowa**</span><span class="sxs-lookup"><span data-stu-id="f28a9-117">An administrator enables [Self-service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to allow a user to add an application using the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Add App** feature, but only w**ith prior approval from a selected set of business approvers**</span></span>

5.  <span data-ttu-id="f28a9-118">Administrator włączy [Samoobsługowe zarządzanie grupami](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) zezwolić użytkownikowi do dołączenia do grupy aplikacji przypisany do **bez zatwierdzenia biznesowa**</span><span class="sxs-lookup"><span data-stu-id="f28a9-118">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to **without business approval**</span></span>

6.  <span data-ttu-id="f28a9-119">Administrator włączy [Samoobsługowe zarządzanie grupami](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) zezwolić użytkownikowi do dołączenia do grupy, która aplikacja jest przypisany do, ale tylko **o pobieraniu z zestawu wybranych osób zatwierdzających biznesowa**</span><span class="sxs-lookup"><span data-stu-id="f28a9-119">An administrator enables [Self-service Group Management](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) to allow a user to join a group that an application is assigned to, but only **with prior approval from a selected set of business approvers**</span></span>

7.  <span data-ttu-id="f28a9-120">Administrator powoduje przypisanie licencji użytkownika bezpośrednio do pierwszej aplikacji firm, takie jak [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="f28a9-120">An administrator assigns a license to a user directly for a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

8.  <span data-ttu-id="f28a9-121">Administrator przypisuje licencję do grupy czy użytkownik jest członkiem do pierwszej strony aplikacji, tak samo, jak [Microsoft Office 365](http://products.office.com/)</span><span class="sxs-lookup"><span data-stu-id="f28a9-121">An administrator assigns a license to a group that the user is a member of to a first party application, like [Microsoft Office 365](http://products.office.com/)</span></span>

9.  <span data-ttu-id="f28a9-122">[Administratora zgadza się na aplikacji](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) mają być używane przez wszystkich użytkowników, a następnie użytkownik loguje się do aplikacji</span><span class="sxs-lookup"><span data-stu-id="f28a9-122">An [administrator consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to be used by all users and then a user signs in to the application</span></span>

10. <span data-ttu-id="f28a9-123">Użytkownik [zgadza się na aplikacji](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) się logując się do aplikacji</span><span class="sxs-lookup"><span data-stu-id="f28a9-123">A user [consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) themselves by signing in to the application</span></span>

## <a name="next-steps"></a><span data-ttu-id="f28a9-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f28a9-124">Next steps</span></span>
[<span data-ttu-id="f28a9-125">Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f28a9-125">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
