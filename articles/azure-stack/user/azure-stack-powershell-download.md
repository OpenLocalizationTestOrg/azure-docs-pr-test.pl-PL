---
title: "Pobieranie narzędzia Azure stosu z serwisu GitHub | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak pobrać narzędzia niezbędne do pracy z stosu Azure."
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: 28F360AD-789A-488D-965F-FC6E6CCF3329
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: mabrigg
ms.openlocfilehash: d4f8a8d73f8e2ea321cb6cc1deda2301033b249d
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="download-azure-stack-tools-from-github"></a>Pobieranie narzędzia Azure stosu z usługi GitHub

Narzędzia AzureStack to repozytorium GitHub obsługującego moduły programu PowerShell, które służy do zarządzania i wdrażania zasobów Azure stosu. Można pobrać i użyć te moduły programu PowerShell Azure stosu Development Kit lub klient zewnętrznych z systemem windows, jeśli planujesz nawiązać połączenie z siecią VPN. Aby uzyskać te narzędzia, Klonuj repozytorium GitHub lub folder AzureStack narzędzia pobierania za pomocą następującego skryptu:

```PowerShell
# Change directory to the root directory 
cd \

# Download the tools archive
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

# Expand the downloaded files
expand-archive master.zip `
  -DestinationPath . `
  -Force

# Change to the tools directory
cd AzureStack-Tools-master

```

## <a name="functionalities-provided-by-the-modules"></a>Funkcje udostępniane przez moduły

Repozytorium narzędzia AzureStack zawiera moduły programu PowerShell, które obsługuje następujące funkcje Azure stosu:  

| Funkcjonalność | Opis | kto może używać tego modułu? |
| --- | --- | --- |
| [Funkcje dotyczące chmury](azure-stack-validate-templates.md) | Ten moduł służy do skorzystaj z możliwości chmury chmury. Na przykład możesz też uzyskać funkcji chmury, takich jak wersja interfejsu API, zasobów usługi Azure Resource Manager, rozszerzeń maszyny Wirtualnej itp. stos Azure i chmury Azure za pomocą tego modułu. | Chmura administratorów i użytkowników. |
| [Zasada Menedżera zasobów Azure stosu](azure-stack-policy-module.md) | Ten moduł służy do konfigurowania subskrypcji platformy Azure lub grupy zasobów platformy Azure z tej samej wersji i usługi dostępności jako stosu Azure. | Użytkowników i administratorów chmury |
| [Łączenie z Azure stosu](azure-stack-connect-azure-stack.md) | Używaj tego modułu, aby połączyć się z wystąpieniem stosu Azure za pomocą programu PowerShell i do konfigurowania połączeń sieci VPN Azure stosu. | Użytkowników i administratorów chmury |
| [Moduł sprawdzania poprawności szablonu](azure-stack-validate-templates.md) | Używaj tego modułu, aby sprawdzić, czy istniejącego lub nowego szablonu można wdrożyć do stosu Azure. | Użytkowników i administratorów chmury |


## <a name="next-steps"></a>Następne kroki
* [Konfigurowanie środowiska PowerShell użytkownika Azure stosu](azure-stack-powershell-configure-user.md)   
* [Nawiązywanie połączeń zestaw deweloperski stosu Azure za pośrednictwem sieci VPN](azure-stack-connect-azure-stack.md)  
