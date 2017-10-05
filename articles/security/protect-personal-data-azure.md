---
title: Ochrona danych osobowych w Microsoft Azure | Dokumentacja firmy Microsoft
description: "Pierwszego artykułu serii artykuły ułatwiają korzystanie z platformy Azure do ochrony danych osobowych"
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
ms.openlocfilehash: dfb046374397c8a19672ce6b67741903fff6e178
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a><span data-ttu-id="f5fc2-103">Ochrona danych osobowych w Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f5fc2-103">Protect personal data in Microsoft Azure</span></span>

<span data-ttu-id="f5fc2-104">W tym artykule przedstawiono serię artykuły, które ułatwiają użyć usług i technologii zabezpieczeń platformy Azure do ochrony danych osobowych.</span><span class="sxs-lookup"><span data-stu-id="f5fc2-104">This article introduces a series of articles that help you use Azure security technologies and services to protect personal data.</span></span> <span data-ttu-id="f5fc2-105">Jest to decydujące znaczenie dla wielu firmowych i inicjatyw zgodności i nadzór nad branżowych.</span><span class="sxs-lookup"><span data-stu-id="f5fc2-105">This is a key requirement for many corporate and industry compliance and governance initiatives.</span></span> <span data-ttu-id="f5fc2-106">Scenariusz, problem instrukcji i firmy cele są uwzględniane w tutaj.</span><span class="sxs-lookup"><span data-stu-id="f5fc2-106">The scenario, problem statement and company goals are included here.</span></span>

## <a name="scenario-and-problem-statement"></a><span data-ttu-id="f5fc2-107">Scenariusz i problem — instrukcja</span><span class="sxs-lookup"><span data-stu-id="f5fc2-107">Scenario and problem statement</span></span>

<span data-ttu-id="f5fc2-108">Firma rejs dużych, siedzibą w Stanach Zjednoczonych rozwija operacjach oferowanie trasy w DS, Adriatyku i Bałtyckiego mórz, jak również brytyjskich.</span><span class="sxs-lookup"><span data-stu-id="f5fc2-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="f5fc2-109">Aby zapewnić obsługę tych działań, ustawił mniejszych rejs wiersze na podstawie we Włoszech, Niemczech, Dania i Zjednoczone Królestwo</span><span class="sxs-lookup"><span data-stu-id="f5fc2-109">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span>

<span data-ttu-id="f5fc2-110">Przez firmę Microsoft Azure do przechowywania danych firmowych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f5fc2-110">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="f5fc2-111">Może to obejmować pracowników i/lub klienta informacje takie jak:</span><span class="sxs-lookup"><span data-stu-id="f5fc2-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="f5fc2-112">adresy</span><span class="sxs-lookup"><span data-stu-id="f5fc2-112">addresses</span></span>
- <span data-ttu-id="f5fc2-113">Numery telefonów</span><span class="sxs-lookup"><span data-stu-id="f5fc2-113">phone numbers</span></span>
- <span data-ttu-id="f5fc2-114">Numery identyfikacyjne podatku</span><span class="sxs-lookup"><span data-stu-id="f5fc2-114">tax identification numbers</span></span>
- <span data-ttu-id="f5fc2-115">Inne informacje</span><span class="sxs-lookup"><span data-stu-id="f5fc2-115">medical information</span></span>
- <span data-ttu-id="f5fc2-116">informacje o karcie kredytowej</span><span class="sxs-lookup"><span data-stu-id="f5fc2-116">credit card information</span></span>

<span data-ttu-id="f5fc2-117">Firma musi ochrony prywatności pracowników i klientów danych podczas przesyłania danych dostępne dla tych działów, które go potrzebują.</span><span class="sxs-lookup"><span data-stu-id="f5fc2-117">The company must protect the privacy of employee and customer data while making data accessible to those departments that need it.</span></span> <span data-ttu-id="f5fc2-118">(na przykład lista płac i zastrzeżenia działów)</span><span class="sxs-lookup"><span data-stu-id="f5fc2-118">(such as payroll and reservations departments)</span></span>

## <a name="company-goals"></a><span data-ttu-id="f5fc2-119">Cele firmy</span><span class="sxs-lookup"><span data-stu-id="f5fc2-119">Company goals</span></span> 

- <span data-ttu-id="f5fc2-120">Źródła danych, które zawierają dane osobowe użytkownika są szyfrowane, gdy znajdującej się w magazynie w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f5fc2-120">Data sources that contain personal data are encrypted when residing in cloud storage.</span></span>

- <span data-ttu-id="f5fc2-121">Osobiste dane przesyłane z jednej lokalizacji do innej są szyfrowane podczas przesyłania w danych.</span><span class="sxs-lookup"><span data-stu-id="f5fc2-121">Personal data that is transferred from one location to another is encrypted while in-transit.</span></span> <span data-ttu-id="f5fc2-122">Jest to wartość true, jeśli dane są przesyłane przez sieć wirtualną lub przez Internet między firmowym centrum danych i w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="f5fc2-122">This is true if the data is traveling across the virtual network or across the Internet between the corporate datacenter and the Azure cloud.</span></span>

- <span data-ttu-id="f5fc2-123">Poufność i integralność danych osobowych jest chroniona przed nieautoryzowanym dostępem przez silnej tożsamości, zarządzania i technologie kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="f5fc2-123">Confidentiality and integrity of personal data is protected from unauthorized access by strong identity management and access control technologies.</span></span>

- <span data-ttu-id="f5fc2-124">Dane osobowe jest chronione przed ujawnieniem za pośrednictwem naruszenia danych za pośrednictwem monitorowanie luk w zabezpieczeniach i zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="f5fc2-124">Personal data is protected from exposure via data breach via monitoring for vulnerabilities and threats.</span></span>

- <span data-ttu-id="f5fc2-125">Stan zabezpieczeń usługi Azure przechowywania lub dane osobowe jest oceniane w celu określenia możliwości w celu lepszej ochrony danych osobowych.</span><span class="sxs-lookup"><span data-stu-id="f5fc2-125">The security state of Azure services that store or transmit personal data is assessed to identify opportunities to better protect personal data.</span></span>

## <a name="data-protection-guidance"></a><span data-ttu-id="f5fc2-126">Wskazówki dotyczące ochrony danych</span><span class="sxs-lookup"><span data-stu-id="f5fc2-126">Data protection guidance</span></span>

<span data-ttu-id="f5fc2-127">Poniższe artykuły zawierają wskazówki porad techniczne, które mogą pomóc osiągnąć cele ochrony danych osobowych wymienionych powyżej:</span><span class="sxs-lookup"><span data-stu-id="f5fc2-127">The following articles contain technical how-to guidance that will help you attain the personal data protection goals listed above:</span></span>

- [<span data-ttu-id="f5fc2-128">Technologii szyfrowania Azure</span><span class="sxs-lookup"><span data-stu-id="f5fc2-128">Azure encryption technologies</span></span>](protect-personal-data-at-rest.md)

- [<span data-ttu-id="f5fc2-129">Technologii szyfrowania Azure</span><span class="sxs-lookup"><span data-stu-id="f5fc2-129">Azure encryption technologies</span></span>](protect-personal-data-in-transit-encryption.md)

- [<span data-ttu-id="f5fc2-130">Azure technologii tożsamościami i dostępem</span><span class="sxs-lookup"><span data-stu-id="f5fc2-130">Azure identity and access technologies</span></span>](protect-personal-data-identity-access-controls.md)

- [<span data-ttu-id="f5fc2-131">Technologie zabezpieczeń sieci platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f5fc2-131">Azure network security technologies</span></span>](protect-personal-data-network-security.md)

- [<span data-ttu-id="f5fc2-132">Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f5fc2-132">Azure Security Center</span></span>](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a><span data-ttu-id="f5fc2-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f5fc2-133">Next steps</span></span>

- [<span data-ttu-id="f5fc2-134">Witryna informacji zabezpieczeń platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f5fc2-134">Azure Security Information Site</span></span>](https://aka.ms/AzureSecInfo)

- [<span data-ttu-id="f5fc2-135">Centrum zaufania Microsoft</span><span class="sxs-lookup"><span data-stu-id="f5fc2-135">Microsoft Trust Center</span></span>](https://www.microsoft.com/TrustCenter/default.aspx)

- [<span data-ttu-id="f5fc2-136">Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f5fc2-136">Azure Security Center</span></span>](https://azure.microsoft.com/services/security-center/)

- [<span data-ttu-id="f5fc2-137">Blog zespołu ds. zabezpieczeń platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f5fc2-137">Azure Security Team Blog</span></span>](https://www.azuresecurityorg)

- [<span data-ttu-id="f5fc2-138">Blog w witrynie Azure.com - zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="f5fc2-138">Azure.com Blog - Security</span></span>](https://azure.microsoft.com/blog/topics/security/)
