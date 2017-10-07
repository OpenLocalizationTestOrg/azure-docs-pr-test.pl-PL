---
title: "aaaPermissions w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak Centrum zabezpieczeń Azure używa toousers uprawnienia tooassign kontroli dostępu opartej na rolach i identyfikuje hello dozwolonych akcji dla każdej roli."
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a>Uprawnienia w Centrum zabezpieczeń Azure

Centrum zabezpieczeń Azure używa [kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md), która zapewnia [wbudowane role](../active-directory/role-based-access-built-in-roles.md) mogą być przypisane toousers, grup i usług Azure.

Centrum zabezpieczeń ocenia konfiguracji hello problemy z zabezpieczeniami tooidentify zasobów i luk w zabezpieczeniach. W Centrum zabezpieczeń widoczne są tylko informacje dotyczące zasobów tooa po przypisaniu roli hello właściciela, współautora lub czytelnika dla grupy zasobów lub subskrypcji hello należącą do zasobu.

Dodanie ról toothese istnieją dwa określonych ról Centrum zabezpieczeń:

* **Czytnik zabezpieczeń**: użytkownika, który należy do roli toothis ma prawa tooSecurity Centrum przeglądania. Użytkownik Hello można wyświetlić zalecenia, alertów, zasad zabezpieczeń i stanów zabezpieczeń, ale nie można wprowadzić zmian.
* **Administrator zabezpieczeń**: użytkownika, który należy do roli toothis ma takie same prawa jako hello czytnika zabezpieczeń hello można również zaktualizować hello zasady zabezpieczeń i odrzucać alerty i zalecenia.

> [!NOTE]
> role zabezpieczeń Hello, czytnika zabezpieczeń i Administrator zabezpieczeń mają dostęp tylko w Centrum zabezpieczeń. role zabezpieczeń Hello nie mają dostępu tooother obszary usługi Azure, takiego jak magazyn, sieci Web i mobilnych lub Internetu rzeczy.
>
>

## <a name="roles-and-allowed-actions"></a>Role i dozwolonych akcji

Witaj Poniższa tabela przedstawia role i dozwolonych akcji w Centrum zabezpieczeń. X oznacza, że akcja hello jest dozwolona dla tej roli.

| Rola | Edytowanie zasad zabezpieczeń | Zastosuj zalecenia dotyczące zabezpieczeń zasobu | Odrzucać alerty i zalecenia | Wyświetlanie alertów i zalecenia |
|:--- |:---:|:---:|:---:|:---:|
| Właściciel subskrypcji | X | X | X | X |
| Współautor subskrypcji | X | X | X | X |
| Właściciel grupy zasobów | -- | X | -- | X |
| Współautor grupy zasobów | -- | X | -- | X |
| Czytelnik | -- | -- | -- | X |
| Administrator zabezpieczeń | X | -- | X | X |
| Czytnik zabezpieczeń | -- | -- | -- | X |

> [!NOTE]
> Firma Microsoft zaleca, aby przypisać hello najbardziej ograniczająca rola potrzebne dla użytkowników toocomplete ich zadań. Na przykład przypisać hello czytnika roli toousers tylko dowiedzieć tooview hello kondycja zabezpieczeń zasobów, ale nie podejmować działań, np. stosować zaleceń ani edytować zasad.
>
>

## <a name="next-steps"></a>Następne kroki
W tym artykule wyjaśniono, jak Centrum zabezpieczeń używa toousers uprawnienia tooassign RBAC oraz zidentyfikować hello dozwolonych akcji dla każdej roli. Teraz, kiedy znasz przypisań ról hello potrzebne toomonitor hello stan zabezpieczeń subskrypcji, edytować zasady zabezpieczeń i stosować zalecenia, Dowiedz się, jak:

- [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń](security-center-policies.md)
- [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń](security-center-recommendations.md)
- [Monitorowanie kondycji zabezpieczeń hello zasobów platformy Azure](security-center-monitoring.md)
- [Zarządzanie i reagowanie na alerty toosecurity w Centrum zabezpieczeń](security-center-managing-and-responding-alerts.md)
- [Monitorowanie rozwiązań partnerskich zabezpieczeń](security-center-partner-solutions.md)
