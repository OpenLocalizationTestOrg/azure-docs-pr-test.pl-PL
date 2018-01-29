---
title: Ocena Azure stosu Development Kit | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak wdrożyć Azure stosu Development Kit do celów oceny."
services: azure-stack
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 01/22/2018
ms.author: jeffgilb
ms.custom: mvc
ms.openlocfilehash: 4ad2e0a91e2fd5023417722fc0a1a6fae93960d0
ms.sourcegitcommit: 5ac112c0950d406251551d5fd66806dc22a63b01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/23/2018
---
# <a name="quickstart-evaluate-the-azure-stack-development-kit"></a>Szybki Start: Ocena Azure stosu Development Kit

*Dotyczy: Azure stosu Development Kit*

[Azure stosu Development Kit](azure-stack-poc.md) jest środowiskiem badań i rozwoju, które można wdrożyć do oceny i Wykaż stosu Azure funkcji i usług. Można go pobrać działa prawidłowo, należy przygotować środowisko sprzętu i uruchamiać skrypty, niektóre (to potrwa kilka godzin). Po wykonaniu tej można Zaloguj się do portali administratora i użytkownika do zarządzania stosu Azure i przetestować oferty. 

1. [**Planowanie sprzętu, oprogramowania i sieci**](azure-stack-deploy.md). Komputer, który obsługuje zestaw deweloperski (Programowanie hosta kit) musi spełniać sprzętu, oprogramowania i wymagania dotyczące sieci. Należy również wybrać opcję przy użyciu usługi Azure Active Directory lub usług federacyjnych Active Directory. Należy przestrzegać wymagań wstępnych przed rozpoczęciem wdrażania, dzięki czemu proces instalacji uruchamia się sprawnie. 

2. [**Pobierać i wyodrębniać pakietu wdrożeniowego**](azure-stack-run-powershell-script.md#download-and-extract-the-development-kit). Możesz pobrać pakiet wdrożeniowy hosta zestawu rozwoju lub do innego komputera. Pliki wyodrębnionego wdrożenia podjąć 60 GB wolnego miejsca na dysku, więc za pomocą innego komputera może pomóc zmniejszyć wymagania sprzętowe dla hosta development kit.

3. [**Przygotowanie hosta zestawu programowanie** ](azure-stack-run-powershell-script.md) za pomocą Instalatora. Po wykonaniu tego kroku hosta zestawu programowanie uruchomi się do Cloudbuilder.vhdx (pliki wirtualnego dysku twardego zawierającego rozruchowego systemu operacyjnego i stosu Azure instalacja).

4. [**Wdrażanie zestaw deweloperski** ](azure-stack-run-powershell-script.md) na hoście development kit.

5. Wdrożenia stosu Azure korzysta z usługi Azure Active Directory, należy [zarejestrować stosu Azure w usłudze Azure](azure-stack-register.md) , co pozwala [pobieranie elementów witrynę Azure marketplace](azure-stack-download-azure-marketplace-item.md) stos Azure.

Po wykonaniu tych czynności, będziesz mieć Środowisko deweloperskie zestawu z portali zarówno administratora, jak i użytkowników. Następnie można [połączenia i zaloguj się na](azure-stack-connect-azure-stack.md) do portalu. Następnie można uruchomić wdrażania dostawców zasobów, tworzenie [oferuje](azure-stack-key-features.md#regions-services-plans-offers-and-subscriptions)i wypełniania stosu Azure [marketplace](azure-stack-marketplace.md).
