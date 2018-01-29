---
title: "Azure zarządzanych aplikacji CredentialsCombo elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opis elementu Microsoft.Compute.CredentialsCombo interfejsu użytkownika dla aplikacji Azure"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/12/2017
ms.author: tomfitz
ms.openlocfilehash: d8faa36aca762bc8d787d5750fcf7efdbaf986ea
ms.sourcegitcommit: 3ab5ea589751d068d3e52db828742ce8ebed4761
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/27/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a>Element Microsoft.Compute.CredentialsCombo interfejsu użytkownika
Grupa formantów z wbudowanych weryfikacji dla systemu Windows i Linux hasła i klucze publiczne SSH. Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](publish-service-catalog-app.md).

## <a name="ui-sample"></a>Przykład interfejsu użytkownika
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a>Schemat
Jeśli `osPlatform` jest **Windows**, zostanie użyta następującego schematu:
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
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

Jeśli `osPlatform` jest **Linux**, zostanie użyta następującego schematu:
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
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
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
- Jeśli `constraints.required` ustawiono **true**, a następnie hasło lub pola tekstowego klucza publicznego SSH musi zawierać wartości można pomyślnie zweryfikować. Wartość domyślna to **true**.
- Jeśli `options.hideConfirmation` ma ustawioną wartość **true**, a następnie drugie pole tekstowe potwierdzania hasła jest ukryty. Wartość domyślna to **false**.
- Jeśli `options.hidePassword` ustawiono **true**, a następnie opcję uwierzytelniania za pomocą hasła jest ukryty. Można go używać tylko wtedy, gdy `osPlatform` jest **Linux**. Wartość domyślna to **false**.
- Dodatkowe ograniczenia dotyczące dozwolonych haseł można zaimplementować przy użyciu `customPasswordRegex` właściwości. Ciąg w `customValidationMessage` jest wyświetlane, gdy hasło niestandardowego sprawdzania poprawności zakończy się niepowodzeniem. Wartość domyślna dla obu właściwości to **null**.

## <a name="sample-output"></a>Przykładowe dane wyjściowe
Jeśli `osPlatform` jest **Windows**, lub użytkownik podał hasła zamiast klucz publiczny SSH, a następnie oczekuje następujące dane wyjściowe:

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

Jeśli użytkownik podał klucz publiczny SSH, jest oczekiwany następujące dane wyjściowe:
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a>Następne kroki
* Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [zarządzanej aplikacji Azure — omówienie](overview.md).
* Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](create-uidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](create-uidefinition-elements.md).
