---
title: "aaaUser inicjowania obsługi usługi Azure AD tooan galerii aplikacji jest lub więcej godzin z argumentami | Dokumentacja firmy Microsoft"
description: "Jak toofind się, dlaczego Inicjowanie obsługi administracyjnej tooyour aplikacji może trwać dłużej niż oczekiwano"
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
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="da017-103">Inicjowanie obsługi administracyjnej tooan usługi Azure AD galerii aplikacji użytkownika jest lub więcej godzin z argumentami</span><span class="sxs-lookup"><span data-stu-id="da017-103">User provisioning tooan Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="da017-104">Podczas włączania najpierw automatyczne Inicjowanie obsługi administracyjnej dla aplikacji, hello początkowej synchronizacji może potrwać od godziny tooseveral 20 minut, w zależności od wielkości hello hello katalog usługi Azure AD i hello liczbę użytkowników w zakresie obsługi.</span><span class="sxs-lookup"><span data-stu-id="da017-104">When first enabling automatic provisioning for an application, hello initial sync can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="da017-105">Kolejne synchronizacje po początkowej synchronizacji hello przebiegać szybciej, jak znaki wodne, przedstawiające stan hello obu systemów po początkowej synchronizacji hello, poprawa wydajności kolejne synchronizacje magazyny hello inicjowania obsługi usługi.</span><span class="sxs-lookup"><span data-stu-id="da017-105">Subsequent syncs after hello initial sync be faster, as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-tooimprove-provisioning-performance"></a><span data-ttu-id="da017-106">Jak tooimprove inicjowania obsługi administracyjnej wydajności</span><span class="sxs-lookup"><span data-stu-id="da017-106">How tooimprove provisioning performance</span></span>

<span data-ttu-id="da017-107">Jeśli hello początkowej synchronizacji trwa dłużej niż kilka godzin, należy co możesz zrobić tooimprove wydajności:</span><span class="sxs-lookup"><span data-stu-id="da017-107">If hello initial sync is taking more than a few hours, there is one thing you can do tooimprove performance:</span></span>

-   <span data-ttu-id="da017-108">**Filtry zakresu użytkownika.**</span><span class="sxs-lookup"><span data-stu-id="da017-108">**User scoping filters.**</span></span> <span data-ttu-id="da017-109">Filtry zakresu pozwalają toofine strojenia hello dane, które hello inicjowania obsługi administracyjnej wyodrębnia usługi z usługi Azure AD przez filtrowanie na podstawie wartości atrybutu określonych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="da017-109">Scoping filters allow you toofine tune hello data that hello provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="da017-110">Aby uzyskać więcej informacji na filtrami zakresów, zobacz [udostępniania aplikacji na podstawie atrybutów z filtrami zakresów](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="da017-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="da017-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="da017-111">Next steps</span></span>
[<span data-ttu-id="da017-112">Automatyzowanie Inicjowanie obsługi użytkowników i anulowania zastrzeżenia tooSaaS aplikacji za pomocą usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="da017-112">Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

