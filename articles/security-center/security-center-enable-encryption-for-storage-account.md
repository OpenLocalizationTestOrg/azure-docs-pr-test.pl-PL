---
title: "szyfrowanie aaaEnable dla konta magazynu w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zaleceń Centrum zabezpieczeń Azure ** włączenie szyfrowania dla usługi Azure magazynu konta **."
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
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="57a9d-103">Włącz szyfrowanie dla konta magazynu Azure w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="57a9d-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="57a9d-104">Centrum zabezpieczeń Azure może zalecić Włącz szyfrowanie usługi Magazyn Azure dla przechowywanych danych.</span><span class="sxs-lookup"><span data-stu-id="57a9d-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="57a9d-105">Szyfrowanie usługi Magazyn (SSE) polega na szyfrowanie danych hello, gdy jest ona zapisywana tooAzure magazynu i odszyfrowywania danych hello przed pobierania.</span><span class="sxs-lookup"><span data-stu-id="57a9d-105">Storage Service Encryption (SSE) works by encrypting hello data when it is written tooAzure storage and decrypting hello data before retrieval.</span></span>  <span data-ttu-id="57a9d-106">SSE jest obecnie dostępny tylko dla hello usługi obiektów Blob platformy Azure i może służyć do blokowe i stronicowe obiekty BLOB i uzupełnialnych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="57a9d-106">SSE is currently available only for hello Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="57a9d-107">toolearn więcej, zobacz [szyfrowanie usługi Magazyn danych magazynowanych](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="57a9d-107">toolearn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="57a9d-108">Po włączeniu szyfrowania, tylko nowe dane są szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="57a9d-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="57a9d-109">Wszystkie istniejące obiekty BLOB na koncie magazynu pozostać niezaszyfrowana.</span><span class="sxs-lookup"><span data-stu-id="57a9d-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="57a9d-110">tooencrypt istniejące obiekty BLOB, zobacz hello [często zadawane pytania dotyczące magazynu usługi szyfrowania](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span><span class="sxs-lookup"><span data-stu-id="57a9d-110">tooencrypt existing blobs, see hello [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="57a9d-111">Szyfrowanie usługi Magazyn jest obsługiwana tylko na kontach magazynu Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="57a9d-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="57a9d-112">Klasycznych kont magazynu nie są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="57a9d-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="57a9d-113">hello toounderstand klasycznego i modeli wdrażania usługi Resource Manager, zobacz [modele wdrażania Azure](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="57a9d-113">toounderstand hello classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="57a9d-114">Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="57a9d-114">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="57a9d-115">Ten dokument nie jest przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="57a9d-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="57a9d-116">Implementowanie hello zalecenia</span><span class="sxs-lookup"><span data-stu-id="57a9d-116">Implement hello recommendation</span></span>
1. <span data-ttu-id="57a9d-117">W hello **zalecenia** bloku, wybierz opcję **Włącz szyfrowanie dla konta magazynu Azure**.</span><span class="sxs-lookup"><span data-stu-id="57a9d-117">In hello **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="57a9d-118">![Włączanie szyfrowania dla konta magazynu][1]</span><span class="sxs-lookup"><span data-stu-id="57a9d-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="57a9d-119">Witaj **Włącz szyfrowanie magazynu** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="57a9d-119">hello **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="57a9d-120">Ten blok lista kont magazynu Azure hello wyłączonym szyfrowanie magazynu.</span><span class="sxs-lookup"><span data-stu-id="57a9d-120">This blade lists hello Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="57a9d-121">W tym przykładzie załóżmy wybierz **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="57a9d-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="57a9d-122">![Włącz szyfrowanie magazynu][2]</span><span class="sxs-lookup"><span data-stu-id="57a9d-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="57a9d-123">Witaj **szyfrowania** bloku **storageacct1** otwiera.</span><span class="sxs-lookup"><span data-stu-id="57a9d-123">hello **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="57a9d-124">Wybierz **włączone**.</span><span class="sxs-lookup"><span data-stu-id="57a9d-124">Select **Enabled**.</span></span>
   <span data-ttu-id="57a9d-125">![Blok szyfrowania][3]</span><span class="sxs-lookup"><span data-stu-id="57a9d-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="57a9d-126">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="57a9d-126">Select **Save**.</span></span>

<span data-ttu-id="57a9d-127">Teraz ma włączone szyfrowanie magazynu dla **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="57a9d-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="57a9d-128">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="57a9d-128">See also</span></span>
<span data-ttu-id="57a9d-129">Ten dokument pokazano, jak tooimplement hello Centrum zabezpieczeń zalecenie "Włącz szyfrowanie dla konta magazynu Azure."</span><span class="sxs-lookup"><span data-stu-id="57a9d-129">This document showed you how tooimplement hello Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="57a9d-130">toolearn więcej informacji na temat szyfrowanie usługi Magazyn Azure, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="57a9d-130">toolearn more about Azure Storage Service Encryption, see hello following:</span></span>

* [<span data-ttu-id="57a9d-131">Szyfrowanie usługi Magazyn Azure dla przechowywanych danych</span><span class="sxs-lookup"><span data-stu-id="57a9d-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="57a9d-132">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="57a9d-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="57a9d-133">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="57a9d-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="57a9d-134">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="57a9d-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="57a9d-135">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="57a9d-135">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="57a9d-136">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="57a9d-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="57a9d-137">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="57a9d-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="57a9d-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.</span><span class="sxs-lookup"><span data-stu-id="57a9d-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
