---
title: "Korzystanie z platformy Azure zarządzanych aplikacji w witrynie marketplace | Dokumentacja firmy Microsoft"
description: "Describeshow do tworzenia aplikacji zarządzanych platformy Azure, która jest dostępna za pośrednictwem portalu Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: baf456740bddd562391ed64d707f990c8921d710
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="consume-azure-managed-applications-in-the-marketplace"></a><span data-ttu-id="2425d-103">Korzystanie z platformy Azure zarządzanych aplikacji w witrynie Marketplace</span><span class="sxs-lookup"><span data-stu-id="2425d-103">Consume Azure managed applications in the Marketplace</span></span>

<span data-ttu-id="2425d-104">Zgodnie z opisem w [zarządzanych aplikacji — omówienie](managed-application-overview.md) artykuł, istnieją dwa scenariusze w środowisku pełnego.</span><span class="sxs-lookup"><span data-stu-id="2425d-104">As discussed in the [Managed Application overview](managed-application-overview.md) article, there are two scenarios in the end to end experience.</span></span> <span data-ttu-id="2425d-105">Jest wydawcy lub dostawcy, który chce utworzyć zarządzanej aplikacji do użycia przez klientów.</span><span class="sxs-lookup"><span data-stu-id="2425d-105">One is the publisher or vendor who wants to create a managed application for use by customers.</span></span> <span data-ttu-id="2425d-106">Drugim jest odbiorcy końcowego lub odbiorcy zarządzanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2425d-106">The second is the end customer or the consumer of the managed application.</span></span> <span data-ttu-id="2425d-107">W tym artykule omówiono drugi scenariusz.</span><span class="sxs-lookup"><span data-stu-id="2425d-107">This article covers the second scenario.</span></span> <span data-ttu-id="2425d-108">Opisuje, jak można wdrożyć zarządzanej aplikacji z portalu Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2425d-108">It describes how you can deploy a managed application from the Microsoft Azure Marketplace.</span></span>

## <a name="create-from-the-marketplace"></a><span data-ttu-id="2425d-109">Tworzenie z poziomu portalu Marketplace</span><span class="sxs-lookup"><span data-stu-id="2425d-109">Create from the Marketplace</span></span>

<span data-ttu-id="2425d-110">Wdrażanie zarządzanych aplikacji z portalu Marketplace jest podobny do wdrażania dowolnego typu zasobów z witryny Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2425d-110">Deploying a managed application from the Marketplace is similar to deploying any type of resources from the Marketplace.</span></span> 

<span data-ttu-id="2425d-111">W portalu, wybierz **+ nowy** i wyszukaj typu rozwiązania do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="2425d-111">In the portal, select **+ New** and search for the type of solution to deploy.</span></span> <span data-ttu-id="2425d-112">Wybierz ten, który należy z dostępnych opcji.</span><span class="sxs-lookup"><span data-stu-id="2425d-112">From the available options, select the one you need.</span></span>

![wyszukiwanie rozwiązania](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="2425d-114">Przejrzyj podsumowanie aplikacji, a następnie wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2425d-114">Review the summary of the application, and select **Create**.</span></span>

![Tworzenie aplikacji zarządzanych](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="2425d-116">Podobnie jak inne rozwiązanie są prezentowane z polami podać wartości.</span><span class="sxs-lookup"><span data-stu-id="2425d-116">Like any other solution, you are presented with fields to provide values for.</span></span> <span data-ttu-id="2425d-117">Te pola różnią się od typu tworzonych zarządzanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2425d-117">These fields vary by the type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="2425d-118">Wyświetl informacje pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="2425d-118">View support information</span></span>

<span data-ttu-id="2425d-119">Po wdrożeniu aplikacji zarządzanej ma wyświetlać informacje pomocy technicznej dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2425d-119">After your managed application has deployed, view the support information for the application.</span></span> <span data-ttu-id="2425d-120">W bloku zarządzanej aplikacji znajduje się informacje pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="2425d-120">In the managed application blade, the support information is listed.</span></span>

![Obsługa](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="2425d-122">Wyświetlanie uprawnień wydawcy</span><span class="sxs-lookup"><span data-stu-id="2425d-122">View publisher permissions</span></span>

<span data-ttu-id="2425d-123">Dostawcy, która zarządza aplikacji uzyskuje dostęp do zasobów.</span><span class="sxs-lookup"><span data-stu-id="2425d-123">The vendor that manages your application is granted access to your resources.</span></span> <span data-ttu-id="2425d-124">Aby wyświetlić te uprawnienia, wybierz **autoryzacje**.</span><span class="sxs-lookup"><span data-stu-id="2425d-124">To see those permissions, select **Authorizations**.</span></span>

![Zezwolenia](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="2425d-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2425d-126">Next steps</span></span>

* <span data-ttu-id="2425d-127">Informacje o publikowaniu zarządzanej aplikacji w witrynie Marketplace, zobacz [Azure zarządzanych aplikacji w witrynie Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="2425d-127">For information about publishing a managed application in the Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="2425d-128">Aby opublikować zarządzanych aplikacji, które są dostępne tylko dla użytkowników w organizacji, zobacz [tworzenie i publikowanie aplikacji zarządzanych katalogu usługi](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="2425d-128">To publish managed applications that are only available to users in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="2425d-129">Aby korzystać z aplikacji zarządzanych, które są dostępne tylko dla użytkowników w organizacji, zobacz [korzystać z aplikacji zarządzanych katalogu usługi](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="2425d-129">To consume managed applications that are only available to users in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>