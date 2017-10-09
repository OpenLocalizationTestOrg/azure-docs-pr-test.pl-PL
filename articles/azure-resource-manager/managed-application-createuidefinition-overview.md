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
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="bd15b-103">Wprowadzenie do korzystania z CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="bd15b-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="bd15b-104">Tym dokumencie przedstawiono podstawowe pojęcia hello CreateUiDefinition, używany przez interfejs użytkownika hello Azure toogenerate portalu hello służący do tworzenia aplikacji zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="bd15b-104">This document introduces hello core concepts of a CreateUiDefinition, which is used by hello Azure portal toogenerate hello user interface for creating a managed application.</span></span>

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

<span data-ttu-id="bd15b-105">CreateUiDefinition zawsze zawiera trzy właściwości:</span><span class="sxs-lookup"><span data-stu-id="bd15b-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="bd15b-106">Program obsługi</span><span class="sxs-lookup"><span data-stu-id="bd15b-106">handler</span></span>
* <span data-ttu-id="bd15b-107">Wersja</span><span class="sxs-lookup"><span data-stu-id="bd15b-107">version</span></span>
* <span data-ttu-id="bd15b-108">parameters</span><span class="sxs-lookup"><span data-stu-id="bd15b-108">parameters</span></span>

<span data-ttu-id="bd15b-109">Dla zarządzanych aplikacji obsługi powinna zawsze być `Microsoft.Compute.MultiVm`, a hello najnowsza wersja obsługiwana wersja to `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="bd15b-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and hello latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="bd15b-110">Schemat Hello hello parametry właściwości zależy od kombinacji hello hello określona Obsługa i wersji.</span><span class="sxs-lookup"><span data-stu-id="bd15b-110">hello schema of hello parameters property depends on hello combination of hello specified handler and version.</span></span> <span data-ttu-id="bd15b-111">W przypadku zarządzanych aplikacji hello obsługiwane właściwości są `basics`, `steps`, i `outputs`.</span><span class="sxs-lookup"><span data-stu-id="bd15b-111">For managed applications, hello supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="bd15b-112">Witaj podstawy i kroki właściwości zawierają hello _elementy_ — takich jak pola tekstowe i listę rozwijaną - toobe wyświetlane w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bd15b-112">hello basics and steps properties contain hello _elements_ - like textboxes and dropdowns - toobe displayed in hello Azure portal.</span></span> <span data-ttu-id="bd15b-113">dane wyjściowe Hello, wartości danych wyjściowych hello toomap używana jest właściwość hello określonych elementów toohello parametry szablonu wdrożenia usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="bd15b-113">hello outputs property is used toomap hello output values of hello specified elements toohello parameters of hello Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="bd15b-114">W tym `$schema` jest zalecane, ale opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="bd15b-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="bd15b-115">Jeśli jest określony, wartość hello `version` musi odpowiadać wersji hello w hello `$schema` identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="bd15b-115">If specified, hello value for `version` must match hello version within hello `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="bd15b-116">Podstawy</span><span class="sxs-lookup"><span data-stu-id="bd15b-116">Basics</span></span>
<span data-ttu-id="bd15b-117">krok podstawy Hello jest zawsze hello pierwszego kroku kreatora hello generowane, gdy CreateUiDefinition analizuje hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bd15b-117">hello Basics step is always hello first step of hello wizard generated when hello Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="bd15b-118">Ponadto określone elementy hello toodisplaying w `basics`, hello portal injects elementy dla użytkowników toochoose hello subskrypcji, grupy zasobów i lokalizację hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="bd15b-118">In addition toodisplaying hello elements specified in `basics`, hello portal injects elements for users toochoose hello subscription, resource group, and location for hello deployment.</span></span> <span data-ttu-id="bd15b-119">Ogólnie rzecz biorąc elementy, które zapytania dla całego wdrożenia parametry, takie jak hello nazwę klastra lub administratora poświadczeń, należy go w tym kroku.</span><span class="sxs-lookup"><span data-stu-id="bd15b-119">Generally, elements that query for deployment-wide parameters, like hello name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="bd15b-120">Jeśli element zachowanie zależy od subskrypcji, grupy zasobów lub lokalizacji użytkownika hello, tego elementu nie można użyć w podstawy.</span><span class="sxs-lookup"><span data-stu-id="bd15b-120">If an element's behavior depends on hello user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="bd15b-121">Na przykład **Microsoft.Compute.SizeSelector** zależy od użytkownika hello subskrypcji i lokalizacji toodetermine hello listę dostępnych rozmiarów.</span><span class="sxs-lookup"><span data-stu-id="bd15b-121">For example, **Microsoft.Compute.SizeSelector** depends on hello user's subscription and location toodetermine hello list of available sizes.</span></span> <span data-ttu-id="bd15b-122">W związku z tym **Microsoft.Compute.SizeSelector** można używać tylko w krokach.</span><span class="sxs-lookup"><span data-stu-id="bd15b-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="bd15b-123">Ogólnie rzecz biorąc, tylko elementy w hello **Microsoft.Common** przestrzeni nazw mogą być używane w podstawy.</span><span class="sxs-lookup"><span data-stu-id="bd15b-123">Generally, only elements in hello **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="bd15b-124">Mimo że niektóre elementy w innych przestrzeniach nazw (takich jak **Microsoft.Compute.Credentials**) które nie są zależne od kontekstu użytkownika hello, nadal jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="bd15b-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on hello user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="bd15b-125">Kroki</span><span class="sxs-lookup"><span data-stu-id="bd15b-125">Steps</span></span>
<span data-ttu-id="bd15b-126">Właściwość kroki Hello może zawierać zero lub więcej toodisplay dodatkowe kroki po podstawy, z których każdy zawiera jeden lub więcej elementów.</span><span class="sxs-lookup"><span data-stu-id="bd15b-126">hello steps property can contain zero or more additional steps toodisplay after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="bd15b-127">Rozważ dodanie czynności na roli lub warstwy aplikacji hello wdrażany.</span><span class="sxs-lookup"><span data-stu-id="bd15b-127">Consider adding steps per role or tier of hello application being deployed.</span></span> <span data-ttu-id="bd15b-128">Na przykład dodać krok dla danych wejściowych dla węzłów głównych hello i krok dla hello węzłów procesu roboczego w klastrze.</span><span class="sxs-lookup"><span data-stu-id="bd15b-128">For example, add a step for inputs for hello master nodes, and a step for hello worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="bd15b-129">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="bd15b-129">Outputs</span></span>
<span data-ttu-id="bd15b-130">Witaj portalu Azure używa hello `outputs` elementy toomap właściwości z `basics` i `steps` toohello parametry szablonu wdrożenia usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="bd15b-130">hello Azure portal uses hello `outputs` property toomap elements from `basics` and `steps` toohello parameters of hello Azure Resource Manager deployment template.</span></span> <span data-ttu-id="bd15b-131">Hello klucze tego słownika hello nazwy parametrów szablonu hello są i wartości hello to właściwości obiektów danych wyjściowych powitania od hello odwołuje się do elementów.</span><span class="sxs-lookup"><span data-stu-id="bd15b-131">hello keys of this dictionary are hello names of hello template parameters, and hello values are properties of hello output objects from hello referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="bd15b-132">Funkcje</span><span class="sxs-lookup"><span data-stu-id="bd15b-132">Functions</span></span>
<span data-ttu-id="bd15b-133">Podobnie za[szablonu funkcji](resource-group-template-functions.md) w usługi Azure Resource Manager (oba składni i funkcji), CreateUiDefinition zapewnia funkcje do pracy z wejściami i wyjściami elementów, jak również funkcje takie jak warunków.</span><span class="sxs-lookup"><span data-stu-id="bd15b-133">Similar too[template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd15b-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bd15b-134">Next steps</span></span>
<span data-ttu-id="bd15b-135">CreateUiDefinition sam ma prosty schematu.</span><span class="sxs-lookup"><span data-stu-id="bd15b-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="bd15b-136">głębokość rzeczywistych Hello go pochodzi z wszystkie hello obsługiwane elementy i funkcje, które hello następujące dokumenty opisano szczegółowo niezwykłych:</span><span class="sxs-lookup"><span data-stu-id="bd15b-136">hello real depth of it comes from all hello supported elements and functions, which hello following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="bd15b-137">Elementy</span><span class="sxs-lookup"><span data-stu-id="bd15b-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="bd15b-138">Funkcje</span><span class="sxs-lookup"><span data-stu-id="bd15b-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="bd15b-139">Bieżącego schematu JSON dla CreateUiDefinition jest dostępnych tutaj: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="bd15b-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="bd15b-140">Nowszych wersji będą dostępne na powitania tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="bd15b-140">Later versions will be available at hello same location.</span></span> <span data-ttu-id="bd15b-141">Zastąp hello `0.1.2-preview` część adresu URL hello i hello `version` wartość o identyfikatorze wersji hello mają toouse.</span><span class="sxs-lookup"><span data-stu-id="bd15b-141">Replace hello `0.1.2-preview` portion of hello URL and hello `version` value with hello version identifier you intend toouse.</span></span> <span data-ttu-id="bd15b-142">identyfikatory wersji Hello obecnie obsługiwane są `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, i `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="bd15b-142">hello currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>
