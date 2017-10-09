---
title: "aaaConsume Azure zarządzanych aplikacji w witrynie marketplace | Dokumentacja firmy Microsoft"
description: "Toocreate Describeshow Azure zarządzanych aplikacji, która jest dostępna za pośrednictwem hello Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 9ae6e11a3f63eb58a9f3199364b5606a7afe5618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="consume-azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="fc0ad-103">Korzystanie z platformy Azure zarządzanych aplikacji hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="fc0ad-103">Consume Azure managed applications in hello Marketplace</span></span>

<span data-ttu-id="fc0ad-104">Zgodnie z opisem w hello [zarządzanych aplikacji — omówienie](managed-application-overview.md) artykuł, istnieją dwa scenariusze hello zakończenia tooend środowisko.</span><span class="sxs-lookup"><span data-stu-id="fc0ad-104">As discussed in hello [Managed Application overview](managed-application-overview.md) article, there are two scenarios in hello end tooend experience.</span></span> <span data-ttu-id="fc0ad-105">Jest hello wydawcy lub dostawcy, którzy chcą toocreate zarządzanej aplikacji do użycia przez klientów.</span><span class="sxs-lookup"><span data-stu-id="fc0ad-105">One is hello publisher or vendor who wants toocreate a managed application for use by customers.</span></span> <span data-ttu-id="fc0ad-106">Hello jest drugi odbiorcy końcowego hello lub odbiorcy hello hello zarządzanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fc0ad-106">hello second is hello end customer or hello consumer of hello managed application.</span></span> <span data-ttu-id="fc0ad-107">W tym artykule omówiono hello drugi scenariusz.</span><span class="sxs-lookup"><span data-stu-id="fc0ad-107">This article covers hello second scenario.</span></span> <span data-ttu-id="fc0ad-108">Opisuje, jak mogą wdrażać zarządzanej aplikacji z hello Microsoft Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="fc0ad-108">It describes how you can deploy a managed application from hello Microsoft Azure Marketplace.</span></span>

## <a name="create-from-hello-marketplace"></a><span data-ttu-id="fc0ad-109">Utwórz na podstawie hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="fc0ad-109">Create from hello Marketplace</span></span>

<span data-ttu-id="fc0ad-110">Wdrażanie zarządzanych aplikacji z portalu Marketplace hello jest podobne toodeploying dowolny typ zasobów z hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="fc0ad-110">Deploying a managed application from hello Marketplace is similar toodeploying any type of resources from hello Marketplace.</span></span> 

<span data-ttu-id="fc0ad-111">W portalu hello wybierz **+ nowy** i wyszukaj hello typu toodeploy rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="fc0ad-111">In hello portal, select **+ New** and search for hello type of solution toodeploy.</span></span> <span data-ttu-id="fc0ad-112">Dostępne opcje hello zaznacz hello, co potrzebne.</span><span class="sxs-lookup"><span data-stu-id="fc0ad-112">From hello available options, select hello one you need.</span></span>

![wyszukiwanie rozwiązania](./media/managed-application-consume-marketplace/search-apps.png)

<span data-ttu-id="fc0ad-114">Przejrzyj podsumowanie hello aplikacji hello, a następnie wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fc0ad-114">Review hello summary of hello application, and select **Create**.</span></span>

![Tworzenie aplikacji zarządzanych](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

<span data-ttu-id="fc0ad-116">Podobnie jak inne rozwiązanie są prezentowane z wartościami tooprovide pola.</span><span class="sxs-lookup"><span data-stu-id="fc0ad-116">Like any other solution, you are presented with fields tooprovide values for.</span></span> <span data-ttu-id="fc0ad-117">Te pola zależy od typu hello zarządzaną aplikację, którą utworzysz.</span><span class="sxs-lookup"><span data-stu-id="fc0ad-117">These fields vary by hello type of managed application you create.</span></span> 

## <a name="view-support-information"></a><span data-ttu-id="fc0ad-118">Wyświetl informacje pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="fc0ad-118">View support information</span></span>

<span data-ttu-id="fc0ad-119">Po wdrożeniu aplikacji zarządzanej ma wyświetlać hello informacje pomocy technicznej dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="fc0ad-119">After your managed application has deployed, view hello support information for hello application.</span></span> <span data-ttu-id="fc0ad-120">W bloku zarządzanej aplikacji hello znajduje się hello informacje pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="fc0ad-120">In hello managed application blade, hello support information is listed.</span></span>

![Obsługa](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a><span data-ttu-id="fc0ad-122">Wyświetlanie uprawnień wydawcy</span><span class="sxs-lookup"><span data-stu-id="fc0ad-122">View publisher permissions</span></span>

<span data-ttu-id="fc0ad-123">uzyskuje dostęp do zasobów tooyour Hello dostawcy, która zarządza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fc0ad-123">hello vendor that manages your application is granted access tooyour resources.</span></span> <span data-ttu-id="fc0ad-124">Wybierz uprawnienia, toosee **autoryzacje**.</span><span class="sxs-lookup"><span data-stu-id="fc0ad-124">toosee those permissions, select **Authorizations**.</span></span>

![Zezwolenia](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a><span data-ttu-id="fc0ad-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fc0ad-126">Next steps</span></span>

* <span data-ttu-id="fc0ad-127">Uzyskać informacji dotyczących publikowania aplikacji zarządzanej w hello Marketplace, zobacz [Azure zarządzanych aplikacji w witrynie Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="fc0ad-127">For information about publishing a managed application in hello Marketplace, see [Azure Managed Applications in Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="fc0ad-128">toopublish zarządzane aplikacje, które są tylko dostępne toousers w organizacji, zobacz [tworzenie i publikowanie aplikacji zarządzanych katalogu usługi](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="fc0ad-128">toopublish managed applications that are only available toousers in your organization, see [Create and publish Service Catalog Managed Application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="fc0ad-129">tooconsume zarządzane aplikacje, które są tylko dostępne toousers w organizacji, zobacz [korzystać z aplikacji zarządzanych katalogu usługi](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="fc0ad-129">tooconsume managed applications that are only available toousers in your organization, see [Consume a Service Catalog Managed Application](managed-application-consumption.md).</span></span>
