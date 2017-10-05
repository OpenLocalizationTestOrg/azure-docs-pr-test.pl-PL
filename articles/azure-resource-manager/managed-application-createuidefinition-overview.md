---
title: "Zrozumienie Tworzenie definicji interfejsu użytkownika dla aplikacji zarządzanych platformy Azure | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tworzenia definicji interfejsu użytkownika dla aplikacji Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 176b891538f85c5638a2321561c3d8bd377d245b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-createuidefinition"></a>Wprowadzenie do korzystania z CreateUiDefinition
Tym dokumencie przedstawiono podstawowe pojęcia CreateUiDefinition, który jest używany w portalu Azure do generowania interfejsu użytkownika do tworzenia zarządzanej aplikacji.

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

CreateUiDefinition zawsze zawiera trzy właściwości: 

* Program obsługi
* Wersja
* Parametry

Dla zarządzanych aplikacji obsługi powinna zawsze być `Microsoft.Compute.MultiVm`, a najnowszą obsługiwaną wersję `0.1.2-preview`.

Schemat właściwości parametrów zależy od kombinacja określona Obsługa i wersji. Dla zarządzanych aplikacji są obsługiwane właściwości `basics`, `steps`, i `outputs`. Zawiera właściwości podstawy i kroki _elementy_ — takich jak pola tekstowe i listę rozwijaną - mają być wyświetlane w portalu Azure. Właściwość wyniki służy do mapowania wartości określonych elementów danych wyjściowych do parametrów szablonu wdrożenia usługi Azure Resource Manager.

W tym `$schema` jest zalecane, ale opcjonalne. Jeśli określona wartość `version` musi być zgodna z wersją w `$schema` identyfikatora URI.

## <a name="basics"></a>Podstawy
Krok podstawy zawsze jest to pierwszy etap kreatora generowane, gdy CreateUiDefinition analizuje portalu Azure. Oprócz wyświetlania elementów określonych w `basics`, portalu injects elementy użytkownicy wybiorą subskrypcji, grupy zasobów i lokalizacji dla wdrożenia. Ogólnie rzecz biorąc elementy, które kwerendy parametry dla całego wdrożenia, takie jak nazwa klastra lub administratora poświadczeń, należy go w tym kroku.

Jeśli element zachowanie zależy od subskrypcji, grupy zasobów lub lokalizacji użytkownika, tego elementu nie można użyć w podstawy. Na przykład **Microsoft.Compute.SizeSelector** jest zależny od subskrypcji i lokalizacji, aby określić listę dostępnych rozmiarów użytkownika. W związku z tym **Microsoft.Compute.SizeSelector** można używać tylko w krokach. Ogólnie rzecz biorąc, tylko elementy w **Microsoft.Common** przestrzeni nazw mogą być używane w podstawy. Mimo że niektóre elementy w innych przestrzeniach nazw (takich jak **Microsoft.Compute.Credentials**) które nie są zależne od kontekstu użytkownika, nadal jest dozwolone.

## <a name="steps"></a>Kroki
Właściwość czynności może zawierać zero lub więcej dodatkowych czynności w celu wyświetlenia po podstawy, z których każdy zawiera jeden lub więcej elementów. Rozważ dodanie czynności na roli lub warstwy aplikacji wdrażany. Na przykład dodać krok dla danych wejściowych dla węzłów głównych i krok dla węzłów procesu roboczego w klastrze.

## <a name="outputs"></a>dane wyjściowe
Azure portal używa `outputs` właściwości, aby zamapować elementy z `basics` i `steps` parametrów szablonu wdrażania Menedżera zasobów Azure. Klucze tego słownika są nazwy parametrów szablonu, a wartości to właściwości obiektów danych wyjściowych z elementów.

## <a name="functions"></a>Funkcje
Podobnie jak [szablonu funkcji](resource-group-template-functions.md) w usługi Azure Resource Manager (oba składni i funkcji), CreateUiDefinition zapewnia funkcje do pracy z wejściami i wyjściami elementów, jak również funkcje takie jak warunków.

## <a name="next-steps"></a>Następne kroki
CreateUiDefinition sam ma prosty schematu. Rzeczywistą liczbę pochodzi z obsługiwane elementy i funkcje, które w następujących dokumentach opisano szczegółowo niezwykłych:

- [Elementy](managed-application-createuidefinition-elements.md)
- [Funkcje](managed-application-createuidefinition-functions.md)

Bieżącego schematu JSON dla CreateUiDefinition jest dostępnych tutaj: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json. 

Nowszych wersji będą dostępne w tej samej lokalizacji. Zastąp `0.1.2-preview` część adresu URL i `version` wartość o identyfikatorze wersji mają być używane. Identyfikatory aktualnie obsługiwana wersja to `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, i `0.1.2-preview`.