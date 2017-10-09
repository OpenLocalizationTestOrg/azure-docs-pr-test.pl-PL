---
title: dane osobowe aaaProtect na platformie Microsoft Azure | Dokumentacja firmy Microsoft
description: "Najpierw artykuł w szeregu toohelp artykuły użyć danych osobowych Azure tooprotect"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: cbffd3872552cbd0f12539535898c41ecf7789e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a><span data-ttu-id="9cfbf-103">Ochrona danych osobowych w Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9cfbf-103">Protect personal data in Microsoft Azure</span></span>

<span data-ttu-id="9cfbf-104">W tym artykule przedstawiono serię artykuły, które ułatwiają użyć zabezpieczeń platformy Azure technologii i usług tooprotect danych osobowych.</span><span class="sxs-lookup"><span data-stu-id="9cfbf-104">This article introduces a series of articles that help you use Azure security technologies and services tooprotect personal data.</span></span> <span data-ttu-id="9cfbf-105">Jest to decydujące znaczenie dla wielu firmowych i inicjatyw zgodności i nadzór nad branżowych.</span><span class="sxs-lookup"><span data-stu-id="9cfbf-105">This is a key requirement for many corporate and industry compliance and governance initiatives.</span></span> <span data-ttu-id="9cfbf-106">Scenariusz Hello problem instrukcji i firmy cele są uwzględniane w tutaj.</span><span class="sxs-lookup"><span data-stu-id="9cfbf-106">hello scenario, problem statement and company goals are included here.</span></span>

## <a name="scenario-and-problem-statement"></a><span data-ttu-id="9cfbf-107">Scenariusz i problem — instrukcja</span><span class="sxs-lookup"><span data-stu-id="9cfbf-107">Scenario and problem statement</span></span>

<span data-ttu-id="9cfbf-108">Firma rejs dużych, siedzibą w Stanach Zjednoczonych hello, rozwija trasy toooffer jego operacji w Śródziemnego hello, Adriatyku i Bałtyckiego mórz, jak również hello brytyjskich.</span><span class="sxs-lookup"><span data-stu-id="9cfbf-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="9cfbf-109">toosupport tych działań uzyskała mniejszych rejs wiersze na podstawie we Włoszech Niemczech, Dania i hello Zjednoczone Królestwo</span><span class="sxs-lookup"><span data-stu-id="9cfbf-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span>

<span data-ttu-id="9cfbf-110">Witaj firma korzysta z danych firmowych toostore Microsoft Azure w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="9cfbf-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="9cfbf-111">Może to obejmować pracowników i/lub klienta informacje takie jak:</span><span class="sxs-lookup"><span data-stu-id="9cfbf-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="9cfbf-112">adresy</span><span class="sxs-lookup"><span data-stu-id="9cfbf-112">addresses</span></span>
- <span data-ttu-id="9cfbf-113">Numery telefonów</span><span class="sxs-lookup"><span data-stu-id="9cfbf-113">phone numbers</span></span>
- <span data-ttu-id="9cfbf-114">Numery identyfikacyjne podatku</span><span class="sxs-lookup"><span data-stu-id="9cfbf-114">tax identification numbers</span></span>
- <span data-ttu-id="9cfbf-115">Inne informacje</span><span class="sxs-lookup"><span data-stu-id="9cfbf-115">medical information</span></span>
- <span data-ttu-id="9cfbf-116">informacje o karcie kredytowej</span><span class="sxs-lookup"><span data-stu-id="9cfbf-116">credit card information</span></span>

<span data-ttu-id="9cfbf-117">Hello firmy muszą chronić prywatność hello pracowników i klientów danych podczas przesyłania danych dostępny toothose działów, które go potrzebują.</span><span class="sxs-lookup"><span data-stu-id="9cfbf-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="9cfbf-118">(na przykład lista płac i zastrzeżenia działów)</span><span class="sxs-lookup"><span data-stu-id="9cfbf-118">(such as payroll and reservations departments)</span></span>

## <a name="company-goals"></a><span data-ttu-id="9cfbf-119">Cele firmy</span><span class="sxs-lookup"><span data-stu-id="9cfbf-119">Company goals</span></span> 

- <span data-ttu-id="9cfbf-120">Źródła danych, które zawierają dane osobowe użytkownika są szyfrowane, gdy znajdującej się w magazynie w chmurze.</span><span class="sxs-lookup"><span data-stu-id="9cfbf-120">Data sources that contain personal data are encrypted when residing in cloud storage.</span></span>

- <span data-ttu-id="9cfbf-121">Osobiste dane przesyłane z jednej lokalizacji tooanother są szyfrowane podczas przesyłania w danych.</span><span class="sxs-lookup"><span data-stu-id="9cfbf-121">Personal data that is transferred from one location tooanother is encrypted while in-transit.</span></span> <span data-ttu-id="9cfbf-122">Jest to wartość true, jeśli dane hello podróżuje hello sieci wirtualnej lub hello Internet między hello firmowym centrum danych i hello chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="9cfbf-122">This is true if hello data is traveling across hello virtual network or across hello Internet between hello corporate datacenter and hello Azure cloud.</span></span>

- <span data-ttu-id="9cfbf-123">Poufność i integralność danych osobowych jest chroniona przed nieautoryzowanym dostępem przez silnej tożsamości, zarządzania i technologie kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="9cfbf-123">Confidentiality and integrity of personal data is protected from unauthorized access by strong identity management and access control technologies.</span></span>

- <span data-ttu-id="9cfbf-124">Dane osobowe jest chronione przed ujawnieniem za pośrednictwem naruszenia danych za pośrednictwem monitorowanie luk w zabezpieczeniach i zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="9cfbf-124">Personal data is protected from exposure via data breach via monitoring for vulnerabilities and threats.</span></span>

- <span data-ttu-id="9cfbf-125">Witaj stan zabezpieczeń usługi Azure przechowywania lub dane osobowe jest oceniane tooidentify toobetter możliwości ochrony danych osobowych.</span><span class="sxs-lookup"><span data-stu-id="9cfbf-125">hello security state of Azure services that store or transmit personal data is assessed tooidentify opportunities toobetter protect personal data.</span></span>

## <a name="data-protection-guidance"></a><span data-ttu-id="9cfbf-126">Wskazówki dotyczące ochrony danych</span><span class="sxs-lookup"><span data-stu-id="9cfbf-126">Data protection guidance</span></span>

<span data-ttu-id="9cfbf-127">Witaj następujące artykuły zawierają techniczne tooguidance jak, które mogą pomóc osiągnąć powyższe cele ochrony w danych osobowych hello:</span><span class="sxs-lookup"><span data-stu-id="9cfbf-127">hello following articles contain technical how-tooguidance that will help you attain hello personal data protection goals listed above:</span></span>

- [<span data-ttu-id="9cfbf-128">Technologii szyfrowania Azure</span><span class="sxs-lookup"><span data-stu-id="9cfbf-128">Azure encryption technologies</span></span>](protect-personal-data-at-rest.md)

- [<span data-ttu-id="9cfbf-129">Technologii szyfrowania Azure</span><span class="sxs-lookup"><span data-stu-id="9cfbf-129">Azure encryption technologies</span></span>](protect-personal-data-in-transit-encryption.md)

- [<span data-ttu-id="9cfbf-130">Azure technologii tożsamościami i dostępem</span><span class="sxs-lookup"><span data-stu-id="9cfbf-130">Azure identity and access technologies</span></span>](protect-personal-data-identity-access-controls.md)

- [<span data-ttu-id="9cfbf-131">Technologie zabezpieczeń sieci platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9cfbf-131">Azure network security technologies</span></span>](protect-personal-data-network-security.md)

- [<span data-ttu-id="9cfbf-132">Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="9cfbf-132">Azure Security Center</span></span>](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a><span data-ttu-id="9cfbf-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9cfbf-133">Next steps</span></span>

- [<span data-ttu-id="9cfbf-134">Witryna informacji zabezpieczeń platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9cfbf-134">Azure Security Information Site</span></span>](https://aka.ms/AzureSecInfo)

- [<span data-ttu-id="9cfbf-135">Centrum zaufania Microsoft</span><span class="sxs-lookup"><span data-stu-id="9cfbf-135">Microsoft Trust Center</span></span>](https://www.microsoft.com/TrustCenter/default.aspx)

- [<span data-ttu-id="9cfbf-136">Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="9cfbf-136">Azure Security Center</span></span>](https://azure.microsoft.com/services/security-center/)

- [<span data-ttu-id="9cfbf-137">Blog zespołu ds. zabezpieczeń platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9cfbf-137">Azure Security Team Blog</span></span>](https://www.azuresecurityorg)

- [<span data-ttu-id="9cfbf-138">Blog w witrynie Azure.com - zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="9cfbf-138">Azure.com Blog - Security</span></span>](https://azure.microsoft.com/blog/topics/security/)
