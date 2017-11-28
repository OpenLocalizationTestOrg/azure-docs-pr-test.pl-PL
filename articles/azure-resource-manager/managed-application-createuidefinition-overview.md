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
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="d9053-103">Wprowadzenie do korzystania z CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="d9053-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="d9053-104">Tym dokumencie przedstawiono podstawowe pojęcia CreateUiDefinition, który jest używany w portalu Azure do generowania interfejsu użytkownika do tworzenia zarządzanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9053-104">This document introduces the core concepts of a CreateUiDefinition, which is used by the Azure portal to generate the user interface for creating a managed application.</span></span>

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

<span data-ttu-id="d9053-105">CreateUiDefinition zawsze zawiera trzy właściwości:</span><span class="sxs-lookup"><span data-stu-id="d9053-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="d9053-106">Program obsługi</span><span class="sxs-lookup"><span data-stu-id="d9053-106">handler</span></span>
* <span data-ttu-id="d9053-107">Wersja</span><span class="sxs-lookup"><span data-stu-id="d9053-107">version</span></span>
* <span data-ttu-id="d9053-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="d9053-108">parameters</span></span>

<span data-ttu-id="d9053-109">Dla zarządzanych aplikacji obsługi powinna zawsze być `Microsoft.Compute.MultiVm`, a najnowszą obsługiwaną wersję `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="d9053-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and the latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="d9053-110">Schemat właściwości parametrów zależy od kombinacja określona Obsługa i wersji.</span><span class="sxs-lookup"><span data-stu-id="d9053-110">The schema of the parameters property depends on the combination of the specified handler and version.</span></span> <span data-ttu-id="d9053-111">Dla zarządzanych aplikacji są obsługiwane właściwości `basics`, `steps`, i `outputs`.</span><span class="sxs-lookup"><span data-stu-id="d9053-111">For managed applications, the supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="d9053-112">Zawiera właściwości podstawy i kroki _elementy_ — takich jak pola tekstowe i listę rozwijaną - mają być wyświetlane w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d9053-112">The basics and steps properties contain the _elements_ - like textboxes and dropdowns - to be displayed in the Azure portal.</span></span> <span data-ttu-id="d9053-113">Właściwość wyniki służy do mapowania wartości określonych elementów danych wyjściowych do parametrów szablonu wdrożenia usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d9053-113">The outputs property is used to map the output values of the specified elements to the parameters of the Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="d9053-114">W tym `$schema` jest zalecane, ale opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="d9053-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="d9053-115">Jeśli określona wartość `version` musi być zgodna z wersją w `$schema` identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="d9053-115">If specified, the value for `version` must match the version within the `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="d9053-116">Podstawy</span><span class="sxs-lookup"><span data-stu-id="d9053-116">Basics</span></span>
<span data-ttu-id="d9053-117">Krok podstawy zawsze jest to pierwszy etap kreatora generowane, gdy CreateUiDefinition analizuje portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d9053-117">The Basics step is always the first step of the wizard generated when the Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="d9053-118">Oprócz wyświetlania elementów określonych w `basics`, portalu injects elementy użytkownicy wybiorą subskrypcji, grupy zasobów i lokalizacji dla wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d9053-118">In addition to displaying the elements specified in `basics`, the portal injects elements for users to choose the subscription, resource group, and location for the deployment.</span></span> <span data-ttu-id="d9053-119">Ogólnie rzecz biorąc elementy, które kwerendy parametry dla całego wdrożenia, takie jak nazwa klastra lub administratora poświadczeń, należy go w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="d9053-119">Generally, elements that query for deployment-wide parameters, like the name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="d9053-120">Jeśli element zachowanie zależy od subskrypcji, grupy zasobów lub lokalizacji użytkownika, tego elementu nie można użyć w podstawy.</span><span class="sxs-lookup"><span data-stu-id="d9053-120">If an element's behavior depends on the user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="d9053-121">Na przykład **Microsoft.Compute.SizeSelector** jest zależny od subskrypcji i lokalizacji, aby określić listę dostępnych rozmiarów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d9053-121">For example, **Microsoft.Compute.SizeSelector** depends on the user's subscription and location to determine the list of available sizes.</span></span> <span data-ttu-id="d9053-122">W związku z tym **Microsoft.Compute.SizeSelector** można używać tylko w krokach.</span><span class="sxs-lookup"><span data-stu-id="d9053-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="d9053-123">Ogólnie rzecz biorąc, tylko elementy w **Microsoft.Common** przestrzeni nazw mogą być używane w podstawy.</span><span class="sxs-lookup"><span data-stu-id="d9053-123">Generally, only elements in the **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="d9053-124">Mimo że niektóre elementy w innych przestrzeniach nazw (takich jak **Microsoft.Compute.Credentials**) które nie są zależne od kontekstu użytkownika, nadal jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="d9053-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on the user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="d9053-125">Kroki</span><span class="sxs-lookup"><span data-stu-id="d9053-125">Steps</span></span>
<span data-ttu-id="d9053-126">Właściwość czynności może zawierać zero lub więcej dodatkowych czynności w celu wyświetlenia po podstawy, z których każdy zawiera jeden lub więcej elementów.</span><span class="sxs-lookup"><span data-stu-id="d9053-126">The steps property can contain zero or more additional steps to display after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="d9053-127">Rozważ dodanie czynności na roli lub warstwy aplikacji wdrażany.</span><span class="sxs-lookup"><span data-stu-id="d9053-127">Consider adding steps per role or tier of the application being deployed.</span></span> <span data-ttu-id="d9053-128">Na przykład dodać krok dla danych wejściowych dla węzłów głównych i krok dla węzłów procesu roboczego w klastrze.</span><span class="sxs-lookup"><span data-stu-id="d9053-128">For example, add a step for inputs for the master nodes, and a step for the worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="d9053-129">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="d9053-129">Outputs</span></span>
<span data-ttu-id="d9053-130">Azure portal używa `outputs` właściwości, aby zamapować elementy z `basics` i `steps` parametrów szablonu wdrażania Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="d9053-130">The Azure portal uses the `outputs` property to map elements from `basics` and `steps` to the parameters of the Azure Resource Manager deployment template.</span></span> <span data-ttu-id="d9053-131">Klucze tego słownika są nazwy parametrów szablonu, a wartości to właściwości obiektów danych wyjściowych z elementów.</span><span class="sxs-lookup"><span data-stu-id="d9053-131">The keys of this dictionary are the names of the template parameters, and the values are properties of the output objects from the referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="d9053-132">Funkcje</span><span class="sxs-lookup"><span data-stu-id="d9053-132">Functions</span></span>
<span data-ttu-id="d9053-133">Podobnie jak [szablonu funkcji](resource-group-template-functions.md) w usługi Azure Resource Manager (oba składni i funkcji), CreateUiDefinition zapewnia funkcje do pracy z wejściami i wyjściami elementów, jak również funkcje takie jak warunków.</span><span class="sxs-lookup"><span data-stu-id="d9053-133">Similar to [template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9053-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d9053-134">Next steps</span></span>
<span data-ttu-id="d9053-135">CreateUiDefinition sam ma prosty schematu.</span><span class="sxs-lookup"><span data-stu-id="d9053-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="d9053-136">Rzeczywistą liczbę pochodzi z obsługiwane elementy i funkcje, które w następujących dokumentach opisano szczegółowo niezwykłych:</span><span class="sxs-lookup"><span data-stu-id="d9053-136">The real depth of it comes from all the supported elements and functions, which the following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="d9053-137">Elementy</span><span class="sxs-lookup"><span data-stu-id="d9053-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="d9053-138">Funkcje</span><span class="sxs-lookup"><span data-stu-id="d9053-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="d9053-139">Bieżącego schematu JSON dla CreateUiDefinition jest dostępnych tutaj: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="d9053-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="d9053-140">Nowszych wersji będą dostępne w tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="d9053-140">Later versions will be available at the same location.</span></span> <span data-ttu-id="d9053-141">Zastąp `0.1.2-preview` część adresu URL i `version` wartość o identyfikatorze wersji mają być używane.</span><span class="sxs-lookup"><span data-stu-id="d9053-141">Replace the `0.1.2-preview` portion of the URL and the `version` value with the version identifier you intend to use.</span></span> <span data-ttu-id="d9053-142">Identyfikatory aktualnie obsługiwana wersja to `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, i `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="d9053-142">The currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>