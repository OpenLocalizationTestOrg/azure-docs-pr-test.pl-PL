---
title: "aaaUnderstand Tworzenie definicji interfejsu użytkownika dla aplikacji zarządzanych platformy Azure | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toocreate definicji interfejsu użytkownika dla aplikacji zarządzanych platformy Azure"
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
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a>Wprowadzenie do korzystania z CreateUiDefinition
Tym dokumencie przedstawiono podstawowe pojęcia hello CreateUiDefinition, używany przez interfejs użytkownika hello Azure toogenerate portalu hello służący do tworzenia aplikacji zarządzanych.

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
* parameters

Dla zarządzanych aplikacji obsługi powinna zawsze być `Microsoft.Compute.MultiVm`, a hello najnowsza wersja obsługiwana wersja to `0.1.2-preview`.

Schemat Hello hello parametry właściwości zależy od kombinacji hello hello określona Obsługa i wersji. W przypadku zarządzanych aplikacji hello obsługiwane właściwości są `basics`, `steps`, i `outputs`. Witaj podstawy i kroki właściwości zawierają hello _elementy_ — takich jak pola tekstowe i listę rozwijaną - toobe wyświetlane w hello portalu Azure. dane wyjściowe Hello, wartości danych wyjściowych hello toomap używana jest właściwość hello określonych elementów toohello parametry szablonu wdrożenia usługi Azure Resource Manager hello.

W tym `$schema` jest zalecane, ale opcjonalne. Jeśli jest określony, wartość hello `version` musi odpowiadać wersji hello w hello `$schema` identyfikatora URI.

## <a name="basics"></a>Podstawy
krok podstawy Hello jest zawsze hello pierwszego kroku kreatora hello generowane, gdy CreateUiDefinition analizuje hello portalu Azure. Ponadto określone elementy hello toodisplaying w `basics`, hello portal injects elementy dla użytkowników toochoose hello subskrypcji, grupy zasobów i lokalizację hello wdrożenia. Ogólnie rzecz biorąc elementy, które zapytania dla całego wdrożenia parametry, takie jak hello nazwę klastra lub administratora poświadczeń, należy go w tym kroku.

Jeśli element zachowanie zależy od subskrypcji, grupy zasobów lub lokalizacji użytkownika hello, tego elementu nie można użyć w podstawy. Na przykład **Microsoft.Compute.SizeSelector** zależy od użytkownika hello subskrypcji i lokalizacji toodetermine hello listę dostępnych rozmiarów. W związku z tym **Microsoft.Compute.SizeSelector** można używać tylko w krokach. Ogólnie rzecz biorąc, tylko elementy w hello **Microsoft.Common** przestrzeni nazw mogą być używane w podstawy. Mimo że niektóre elementy w innych przestrzeniach nazw (takich jak **Microsoft.Compute.Credentials**) które nie są zależne od kontekstu użytkownika hello, nadal jest dozwolone.

## <a name="steps"></a>Kroki
Właściwość kroki Hello może zawierać zero lub więcej toodisplay dodatkowe kroki po podstawy, z których każdy zawiera jeden lub więcej elementów. Rozważ dodanie czynności na roli lub warstwy aplikacji hello wdrażany. Na przykład dodać krok dla danych wejściowych dla węzłów głównych hello i krok dla hello węzłów procesu roboczego w klastrze.

## <a name="outputs"></a>dane wyjściowe
Witaj portalu Azure używa hello `outputs` elementy toomap właściwości z `basics` i `steps` toohello parametry szablonu wdrożenia usługi Azure Resource Manager hello. Hello klucze tego słownika hello nazwy parametrów szablonu hello są i wartości hello to właściwości obiektów danych wyjściowych powitania od hello odwołuje się do elementów.

## <a name="functions"></a>Funkcje
Podobnie za[szablonu funkcji](resource-group-template-functions.md) w usługi Azure Resource Manager (oba składni i funkcji), CreateUiDefinition zapewnia funkcje do pracy z wejściami i wyjściami elementów, jak również funkcje takie jak warunków.

## <a name="next-steps"></a>Następne kroki
CreateUiDefinition sam ma prosty schematu. głębokość rzeczywistych Hello go pochodzi z wszystkie hello obsługiwane elementy i funkcje, które hello następujące dokumenty opisano szczegółowo niezwykłych:

- [Elementy](managed-application-createuidefinition-elements.md)
- [Funkcje](managed-application-createuidefinition-functions.md)

Bieżącego schematu JSON dla CreateUiDefinition jest dostępnych tutaj: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json. 

Nowszych wersji będą dostępne na powitania tej samej lokalizacji. Zastąp hello `0.1.2-preview` część adresu URL hello i hello `version` wartość o identyfikatorze wersji hello mają toouse. identyfikatory wersji Hello obecnie obsługiwane są `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, i `0.1.2-preview`.
