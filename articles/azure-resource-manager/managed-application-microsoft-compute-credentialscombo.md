---
title: "aaaAzure zarządzanych aplikacji CredentialsCombo elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opisuje hello elementu Microsoft.Compute.CredentialsCombo interfejsu użytkownika dla aplikacji Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: d44a3929ebb7a5ff78b72f9eaeb6e52b098e266f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="86676-103">Element Microsoft.Compute.CredentialsCombo interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="86676-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="86676-104">Grupa formantów z wbudowanych weryfikacji dla systemu Windows i Linux hasła i klucze publiczne SSH.</span><span class="sxs-lookup"><span data-stu-id="86676-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="86676-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="86676-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="86676-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="86676-106">UI sample</span></span>
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="86676-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="86676-108">Schema</span></span>
<span data-ttu-id="86676-109">Jeśli `osPlatform` jest **Windows**, hello następującego schematu zostanie użyty:</span><span class="sxs-lookup"><span data-stu-id="86676-109">If `osPlatform` is **Windows**, then hello following schema is used:</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": {
    "password": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

<span data-ttu-id="86676-110">Jeśli `osPlatform` jest **Linux**, hello następującego schematu zostanie użyty:</span><span class="sxs-lookup"><span data-stu-id="86676-110">If `osPlatform` is **Linux**, then hello following schema is used:</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "authenticationType": "Authentication type",
    "password": "Password",
    "confirmPassword": "Confirm password",
    "sshPublicKey": "SSH public key"
  },
  "toolTip": {
    "authenticationType": "",
    "password": "",
    "sshPublicKey": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="86676-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="86676-111">Remarks</span></span>
- <span data-ttu-id="86676-112">`osPlatform`należy określić i mogą być **Windows** lub **Linux**.</span><span class="sxs-lookup"><span data-stu-id="86676-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="86676-113">Jeśli `constraints.required` ustawiono zbyt**true**, następnie hello hasła lub pola tekstowego klucza publicznego SSH musi zawierać wartości toovalidate pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="86676-113">If `constraints.required` is set too**true**, then hello password or SSH public key text boxes must contain values toovalidate successfully.</span></span> <span data-ttu-id="86676-114">Witaj, wartość domyślna to **true**.</span><span class="sxs-lookup"><span data-stu-id="86676-114">hello default value is **true**.</span></span>
- <span data-ttu-id="86676-115">Jeśli `options.hideConfirmation` ustawiono zbyt**true**, a następnie hello drugie pole tekstowe potwierdzania hasła użytkownika hello jest ukryty.</span><span class="sxs-lookup"><span data-stu-id="86676-115">If `options.hideConfirmation` is set too**true**, then hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="86676-116">Witaj, wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="86676-116">hello default value is **false**.</span></span>
- <span data-ttu-id="86676-117">Jeśli `options.hidePassword` ustawiono zbyt**true**, a następnie uwierzytelniania hasła toouse opcji hello jest ukryty.</span><span class="sxs-lookup"><span data-stu-id="86676-117">If `options.hidePassword` is set too**true**, then hello option toouse password authentication is hidden.</span></span> <span data-ttu-id="86676-118">Można go używać tylko wtedy, gdy `osPlatform` jest **Linux**.</span><span class="sxs-lookup"><span data-stu-id="86676-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="86676-119">Wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="86676-119">The default value is **false**.</span></span>
- <span data-ttu-id="86676-120">Dodatkowe ograniczenia na powitania dozwolone haseł można zaimplementować przy użyciu hello `customPasswordRegex` właściwości.</span><span class="sxs-lookup"><span data-stu-id="86676-120">Additional constraints on hello allowed passwords can be implemented by using hello `customPasswordRegex` property.</span></span> <span data-ttu-id="86676-121">ciąg Hello `customValidationMessage` jest wyświetlane, gdy hasło niestandardowego sprawdzania poprawności zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="86676-121">hello string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="86676-122">Witaj wartością domyślną dla obu właściwości jest **null**.</span><span class="sxs-lookup"><span data-stu-id="86676-122">hello default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="86676-123">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="86676-123">Sample output</span></span>
<span data-ttu-id="86676-124">Jeśli `osPlatform` jest **Windows**, lub hello użytkownik podał hasła zamiast klucz publiczny SSH, a następnie hello następujące dane wyjściowe Oczekiwano:</span><span class="sxs-lookup"><span data-stu-id="86676-124">If `osPlatform` is **Windows**, or hello user provided a password instead of an SSH public key, then hello following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="86676-125">Jeśli użytkownik hello podany klucz publiczny SSH, następnie hello następujące dane wyjściowe Oczekiwano:</span><span class="sxs-lookup"><span data-stu-id="86676-125">If hello user provided an SSH public key, then hello following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="86676-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86676-126">Next steps</span></span>
* <span data-ttu-id="86676-127">Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="86676-127">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="86676-128">Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="86676-128">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="86676-129">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="86676-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
