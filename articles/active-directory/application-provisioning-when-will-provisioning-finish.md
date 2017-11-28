---
title: "Inicjowanie obsługi użytkowników dla aplikacji w galerii Azure AD jest lub więcej godzin z argumentami | Dokumentacja firmy Microsoft"
description: "Jak dowiedzieć się, dlaczego inicjowania obsługi administracyjnej do aplikacji może trwać dłużej niż oczekiwano"
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
ms.openlocfilehash: 183d60cbbbc8d02f7cd3cacc160453c45717ef0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="user-provisioning-to-an-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="09f6a-103">Inicjowanie obsługi użytkowników dla aplikacji w galerii Azure AD jest lub więcej godzin z argumentami</span><span class="sxs-lookup"><span data-stu-id="09f6a-103">User provisioning to an Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="09f6a-104">Podczas włączania najpierw automatyczne Inicjowanie obsługi administracyjnej dla aplikacji, początkowej synchronizacji może potrwać od 20 minut do kilku godzin, zależnie od rozmiaru katalogu usługi Azure AD i liczbę użytkowników w zakresie obsługi.</span><span class="sxs-lookup"><span data-stu-id="09f6a-104">When first enabling automatic provisioning for an application, the initial sync can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="09f6a-105">Kolejne synchronizacje po początkowej synchronizacji można szybciej, jak znaki wodne, przedstawiające stan obu systemów po początkowej synchronizacji, poprawa wydajności kolejne synchronizacje magazyny inicjowania obsługi usługi.</span><span class="sxs-lookup"><span data-stu-id="09f6a-105">Subsequent syncs after the initial sync be faster, as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-improve-provisioning-performance"></a><span data-ttu-id="09f6a-106">Jak poprawić wydajność inicjowania obsługi administracyjnej</span><span class="sxs-lookup"><span data-stu-id="09f6a-106">How to improve provisioning performance</span></span>

<span data-ttu-id="09f6a-107">Jeśli synchronizacji początkowej trwa dłużej niż kilka godzin, jest jedyną operacją, której można wykonać, aby poprawić wydajność:</span><span class="sxs-lookup"><span data-stu-id="09f6a-107">If the initial sync is taking more than a few hours, there is one thing you can do to improve performance:</span></span>

-   <span data-ttu-id="09f6a-108">**Filtry zakresu użytkownika.**</span><span class="sxs-lookup"><span data-stu-id="09f6a-108">**User scoping filters.**</span></span> <span data-ttu-id="09f6a-109">Filtry zakresu umożliwiają dostosowywanie dane inicjowania obsługi usługi wyodrębnia z usługi Azure AD przez filtrowanie na podstawie wartości atrybutu określonych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="09f6a-109">Scoping filters allow you to fine tune the data that the provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="09f6a-110">Aby uzyskać więcej informacji na filtrami zakresów, zobacz [udostępniania aplikacji na podstawie atrybutów z filtrami zakresów](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="09f6a-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09f6a-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="09f6a-111">Next steps</span></span>
[<span data-ttu-id="09f6a-112">Automatyzowanie użytkownika alokowania i anulowania alokowania do aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09f6a-112">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

