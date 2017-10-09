---
title: "aaaEnable przezroczystego szyfrowania danych w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** włączyć przezroczysty danych szyfrowania **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="8d02e-103">Włącz przezroczystego szyfrowania danych w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="8d02e-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="8d02e-104">Centrum zabezpieczeń Azure zaleca Włącz funkcji przezroczystego szyfrowania danych (TDE) baz danych SQL, jeśli nie jest już włączona funkcji TDE.</span><span class="sxs-lookup"><span data-stu-id="8d02e-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="8d02e-105">Funkcji TDE chroni dane i pomaga spełnić wymagania zgodności przez zaszyfrowanie bazy danych, skojarzonych kopii zapasowych i plików dziennika transakcji w stanie spoczynku, bez konieczności wprowadzania zmian tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8d02e-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes tooyour application.</span></span> <span data-ttu-id="8d02e-106">więcej Zobacz toolearn [przezroczystego szyfrowania danych z bazy danych SQL Azure](https://msdn.microsoft.com/library/dn948096).</span><span class="sxs-lookup"><span data-stu-id="8d02e-106">toolearn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="8d02e-107">To zalecenie dotyczy toohello usługi Azure SQL. nie zawiera SQL uruchomionych na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="8d02e-107">This recommendation applies toohello Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="8d02e-108">Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="8d02e-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="8d02e-109">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="8d02e-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="8d02e-110">Implementowanie hello zalecenia</span><span class="sxs-lookup"><span data-stu-id="8d02e-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="8d02e-111">W hello **zalecenia** bloku, wybierz opcję **włączyć przezroczystego szyfrowania danych**.</span><span class="sxs-lookup"><span data-stu-id="8d02e-111">In hello **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="8d02e-112">![Włączanie technologii Transparent Data Encryption][1]</span><span class="sxs-lookup"><span data-stu-id="8d02e-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="8d02e-113">Spowoduje to otwarcie hello **włączyć przezroczystego szyfrowania danych w bazach danych SQL** bloku.</span><span class="sxs-lookup"><span data-stu-id="8d02e-113">This opens hello **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="8d02e-114">Wybierz tooenable bazy danych SQL funkcji TDE.</span><span class="sxs-lookup"><span data-stu-id="8d02e-114">Select a SQL database tooenable TDE on.</span></span>
   <span data-ttu-id="8d02e-115">![Wybierz bazy danych SQL tooenable funkcji TDE na][2]</span><span class="sxs-lookup"><span data-stu-id="8d02e-115">![Select SQL DB tooenable TDE on][2]</span></span>
3. <span data-ttu-id="8d02e-116">Na powitania **przezroczystego szyfrowania danych** bloku, wybierz opcję **ON** szyfrowania danych i wybierz **zapisać** hello wstążce top hello bloku.</span><span class="sxs-lookup"><span data-stu-id="8d02e-116">On hello **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in hello top ribbon of hello blade.</span></span>
   <span data-ttu-id="8d02e-117">![Włączanie funkcji TDE][3]</span><span class="sxs-lookup"><span data-stu-id="8d02e-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="8d02e-118">Po włączeniu funkcji TDE hello wybrana baza danych SQL, hello **stanu szyfrowania** zmieni się zbyt**zaszyfrowane**.</span><span class="sxs-lookup"><span data-stu-id="8d02e-118">Once TDE is enabled on hello selected SQL database, hello **Encryption status** will change too**Encrypted**.</span></span>    

   ![Stan szyfrowania][4]

## <a name="see-also"></a><span data-ttu-id="8d02e-120">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="8d02e-120">See also</span></span>
<span data-ttu-id="8d02e-121">W tym artykule pokazano, jak tooimplement hello zalecenia Centrum zabezpieczeń "Włącz przezroczystego szyfrowania danych."</span><span class="sxs-lookup"><span data-stu-id="8d02e-121">This article showed you how tooimplement hello Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="8d02e-122">toolearn więcej informacji na temat funkcji SQL TDE znaleźć hello w następujących tematach:</span><span class="sxs-lookup"><span data-stu-id="8d02e-122">toolearn more about SQL TDE, see hello following:</span></span>

* [<span data-ttu-id="8d02e-123">Przezroczystego szyfrowania danych z bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="8d02e-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="8d02e-124">Rozpoczynanie pracy z przezroczystym danych szyfrowania (funkcji TDE)</span><span class="sxs-lookup"><span data-stu-id="8d02e-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="8d02e-125">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="8d02e-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="8d02e-126">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="8d02e-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="8d02e-127">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8d02e-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="8d02e-128">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8d02e-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="8d02e-129">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="8d02e-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="8d02e-130">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="8d02e-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="8d02e-131">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="8d02e-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="8d02e-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) --hello najnowsze zabezpieczeń platformy Azure i informacji.</span><span class="sxs-lookup"><span data-stu-id="8d02e-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
