---
title: "Włącz szyfrowanie dla konta magazynu w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument zawiera implementowania zaleceń Centrum zabezpieczeń Azure ** włączenie szyfrowania dla usługi Azure magazynu konta **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: b7b2e8a12cbab68da9c8fcc348e8e3c543607007
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="a86c1-103">Włącz szyfrowanie dla konta magazynu Azure w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="a86c1-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="a86c1-104">Centrum zabezpieczeń Azure może zalecić Włącz szyfrowanie usługi Magazyn Azure dla przechowywanych danych.</span><span class="sxs-lookup"><span data-stu-id="a86c1-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="a86c1-105">Szyfrowanie usługi Magazyn (SSE) polega na szyfrowaniu danych podczas ich zapisywania w magazynie Azure i odszyfrowywania danych przed pobierania.</span><span class="sxs-lookup"><span data-stu-id="a86c1-105">Storage Service Encryption (SSE) works by encrypting the data when it is written to Azure storage and decrypting the data before retrieval.</span></span>  <span data-ttu-id="a86c1-106">SSE jest obecnie dostępny tylko dla usługi obiektów Blob platformy Azure i może służyć do blokowe i stronicowe obiekty BLOB i uzupełnialnych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="a86c1-106">SSE is currently available only for the Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="a86c1-107">Aby dowiedzieć się więcej, zobacz [szyfrowanie usługi Magazyn danych magazynowanych](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="a86c1-107">To learn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="a86c1-108">Po włączeniu szyfrowania, tylko nowe dane są szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="a86c1-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="a86c1-109">Wszystkie istniejące obiekty BLOB na koncie magazynu pozostać niezaszyfrowana.</span><span class="sxs-lookup"><span data-stu-id="a86c1-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="a86c1-110">Aby zaszyfrować istniejące obiekty BLOB, zobacz [często zadawane pytania dotyczące magazynu usługi szyfrowania](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span><span class="sxs-lookup"><span data-stu-id="a86c1-110">To encrypt existing blobs, see the [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="a86c1-111">Szyfrowanie usługi Magazyn jest obsługiwana tylko na kontach magazynu Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="a86c1-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="a86c1-112">Klasycznych kont magazynu nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="a86c1-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="a86c1-113">Aby poznać klasycznego i modeli wdrażania usługi Resource Manager, zobacz [modele wdrażania Azure](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="a86c1-113">To understand the classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a86c1-114">Informacje na temat usługi przedstawiono w tym dokumencie za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a86c1-114">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="a86c1-115">Ten dokument nie jest przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="a86c1-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="a86c1-116">Wykonania zalecenia</span><span class="sxs-lookup"><span data-stu-id="a86c1-116">Implement the recommendation</span></span>
1. <span data-ttu-id="a86c1-117">W **zalecenia** bloku, wybierz opcję **Włącz szyfrowanie dla konta magazynu Azure**.</span><span class="sxs-lookup"><span data-stu-id="a86c1-117">In the **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="a86c1-118">![Włączanie szyfrowania dla konta magazynu][1]</span><span class="sxs-lookup"><span data-stu-id="a86c1-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="a86c1-119">**Włącz szyfrowanie magazynu** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="a86c1-119">The **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="a86c1-120">Ten blok zawiera listę kontami magazynu Azure, w których Magazyn, szyfrowanie jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="a86c1-120">This blade lists the Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="a86c1-121">W tym przykładzie załóżmy wybierz **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="a86c1-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="a86c1-122">![Włącz szyfrowanie magazynu][2]</span><span class="sxs-lookup"><span data-stu-id="a86c1-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="a86c1-123">**Szyfrowania** bloku **storageacct1** otwiera.</span><span class="sxs-lookup"><span data-stu-id="a86c1-123">The **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="a86c1-124">Wybierz **włączone**.</span><span class="sxs-lookup"><span data-stu-id="a86c1-124">Select **Enabled**.</span></span>
   <span data-ttu-id="a86c1-125">![Blok szyfrowania][3]</span><span class="sxs-lookup"><span data-stu-id="a86c1-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="a86c1-126">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a86c1-126">Select **Save**.</span></span>

<span data-ttu-id="a86c1-127">Teraz ma włączone szyfrowanie magazynu dla **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="a86c1-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="a86c1-128">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a86c1-128">See also</span></span>
<span data-ttu-id="a86c1-129">Ten dokument pokazano sposób wykonania zalecenia Centrum zabezpieczeń "Włącz szyfrowanie dla konta magazynu Azure".</span><span class="sxs-lookup"><span data-stu-id="a86c1-129">This document showed you how to implement the Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="a86c1-130">Aby dowiedzieć się więcej na temat szyfrowanie usługi Magazyn Azure, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="a86c1-130">To learn more about Azure Storage Service Encryption, see the following:</span></span>

* [<span data-ttu-id="a86c1-131">Szyfrowanie usługi Magazyn Azure dla przechowywanych danych</span><span class="sxs-lookup"><span data-stu-id="a86c1-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="a86c1-132">Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="a86c1-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="a86c1-133">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — informacje o sposobie konfigurowania zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="a86c1-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="a86c1-134">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a86c1-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="a86c1-135">[Reagowanie na alerty zabezpieczeń w Centrum zabezpieczeń Azure i zarządzanie nimi](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak reagowania na alerty zabezpieczeń i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="a86c1-135">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="a86c1-136">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a86c1-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="a86c1-137">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="a86c1-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="a86c1-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.</span><span class="sxs-lookup"><span data-stu-id="a86c1-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
