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
ms.openlocfilehash: 4dbdb2dc11bdc515fb3856dd45203868122c7726
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a>Ochrona danych osobowych w Microsoft Azure

W tym artykule przedstawiono serię artykuły, które ułatwiają użyć usług i technologii zabezpieczeń platformy Azure do ochrony danych osobowych. Jest to decydujące znaczenie dla wielu firmowych i inicjatyw zgodności i nadzór nad branżowych. Scenariusz, problem instrukcji i firmy cele są uwzględniane w tutaj.

## <a name="scenario-and-problem-statement"></a>Scenariusz i problem — instrukcja

Firma rejs dużych, siedzibą w Stanach Zjednoczonych rozwija operacjach oferowanie trasy w DS, Adriatyku i Bałtyckiego mórz, jak również brytyjskich. Aby zapewnić obsługę tych działań, ustawił mniejszych rejs wiersze na podstawie we Włoszech, Niemczech, Dania i Zjednoczone Królestwo

Przez firmę Microsoft Azure do przechowywania danych firmowych w chmurze. Może to obejmować informacje klienta i/lub pracowników, takich jak:

- adresy
- Numery telefonów
- Numery identyfikacyjne podatku
- informacje o karcie kredytowej

Firmy muszą chronić poufności danych klienta i pracowników, podczas udostępniania danych dostępne dla tych działów, które go potrzebują. (na przykład lista płac i zastrzeżenia działów)

## <a name="company-goals"></a>Cele firmy 

- Źródła danych, które zawierają dane osobowe użytkownika są szyfrowane, gdy znajdującej się w magazynie w chmurze.

- Osobiste dane przesyłane z jednej lokalizacji do innej są szyfrowane podczas przesyłania w danych. Jest to wartość true, jeśli dane są przesyłane przez sieć wirtualną lub przez Internet między firmowym centrum danych i w chmurze Azure.

- Poufność i integralność danych osobowych jest chroniona przed nieautoryzowanym dostępem przez silnej tożsamości, zarządzania i technologie kontroli dostępu.

- Dane osobowe jest chronione przed ujawnieniem za pośrednictwem naruszenia danych za pośrednictwem monitorowanie luk w zabezpieczeniach i zagrożeń.

- Stan zabezpieczeń usługi Azure przechowywania lub dane osobowe jest oceniane w celu określenia możliwości w celu lepszej ochrony danych osobowych.

## <a name="data-protection-guidance"></a>Wskazówki dotyczące ochrony danych

Poniższe artykuły zawierają wskazówki porad techniczne, które mogą pomóc osiągnąć cele ochrony danych osobowych wymienionych powyżej:

- [Technologii szyfrowania Azure](protect-personal-data-at-rest.md)

- [Technologii szyfrowania Azure](protect-personal-data-in-transit-encryption.md)

- [Azure technologii tożsamościami i dostępem](protect-personal-data-identity-access-controls.md)

- [Technologie zabezpieczeń sieci platformy Azure](protect-personal-data-network-security.md)

- [Azure Security Center](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a>Następne kroki

- [Witryna informacji zabezpieczeń platformy Azure](https://aka.ms/AzureSecInfo)

- [Centrum zaufania Microsoft](https://www.microsoft.com/TrustCenter/default.aspx)

- [Azure Security Center](https://azure.microsoft.com/services/security-center/)

- [Blog zespołu ds. zabezpieczeń platformy Azure](https://www.azuresecurityorg)

- [Blog w witrynie Azure.com - zabezpieczeń](https://azure.microsoft.com/blog/topics/security/)
