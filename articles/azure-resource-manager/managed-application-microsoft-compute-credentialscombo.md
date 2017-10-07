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
# <a name="microsoftcomputecredentialscombo-ui-element"></a>Element Microsoft.Compute.CredentialsCombo interfejsu użytkownika
Grupa formantów z wbudowanych weryfikacji dla systemu Windows i Linux hasła i klucze publiczne SSH. Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Przykład interfejsu użytkownika
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a>Schemat
Jeśli `osPlatform` jest **Windows**, hello następującego schematu zostanie użyty:
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

Jeśli `osPlatform` jest **Linux**, hello następującego schematu zostanie użyty:
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

## <a name="remarks"></a>Uwagi
- `osPlatform`należy określić i mogą być **Windows** lub **Linux**.
- Jeśli `constraints.required` ustawiono zbyt**true**, następnie hello hasła lub pola tekstowego klucza publicznego SSH musi zawierać wartości toovalidate pomyślnie. Witaj, wartość domyślna to **true**.
- Jeśli `options.hideConfirmation` ustawiono zbyt**true**, a następnie hello drugie pole tekstowe potwierdzania hasła użytkownika hello jest ukryty. Witaj, wartość domyślna to **false**.
- Jeśli `options.hidePassword` ustawiono zbyt**true**, a następnie uwierzytelniania hasła toouse opcji hello jest ukryty. Można go używać tylko wtedy, gdy `osPlatform` jest **Linux**. Wartość domyślna to **false**.
- Dodatkowe ograniczenia na powitania dozwolone haseł można zaimplementować przy użyciu hello `customPasswordRegex` właściwości. ciąg Hello `customValidationMessage` jest wyświetlane, gdy hasło niestandardowego sprawdzania poprawności zakończy się niepowodzeniem. Witaj wartością domyślną dla obu właściwości jest **null**.

## <a name="sample-output"></a>Przykładowe dane wyjściowe
Jeśli `osPlatform` jest **Windows**, lub hello użytkownik podał hasła zamiast klucz publiczny SSH, a następnie hello następujące dane wyjściowe Oczekiwano:

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

Jeśli użytkownik hello podany klucz publiczny SSH, następnie hello następujące dane wyjściowe Oczekiwano:
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a>Następne kroki
* Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).
* Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).
