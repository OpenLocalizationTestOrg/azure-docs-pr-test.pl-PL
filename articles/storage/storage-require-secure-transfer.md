---
title: "Wymaga zapewnienia bezpiecznego transferu w usłudze Azure Storage | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat funkcji \"Wymaga zapewnienia bezpiecznego transferu\" dla usługi Azure Storage i jak je włączyć."
services: storage
documentationcenter: na
author: fhryo-msft
manager: Jason.Hogg
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/20/2017
ms.author: fryu
ms.openlocfilehash: bc5b7fc79869c632db96958f17aaf953a5fd3b19
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="require-secure-transfer"></a>Wymaganie bezpiecznego transferu

Opcja "Bezpieczny transfer wymagane" podnosi poziom bezpieczeństwa konta magazynu, zezwalając tylko żądania do konta magazynu z bezpiecznych połączeń. Na przykład podczas wywoływania interfejsów API REST, aby uzyskać dostęp do konta magazynu, należy połączyć przy użyciu protokołu HTTPS. Wszystkie żądania przy użyciu protokołu HTTP są odrzucane po włączeniu "Bezpieczny transfer wymagane".

Usługa pliki Azure jest używana, każde połączenie bez szyfrowania nie powiedzie się po włączeniu "Bezpieczny transfer wymagane". W tym scenariuszy przy użyciu protokołu SMB 2.1, SMB 3.0 bez szyfrowania i niektórych odmian klient protokołu SMB w systemie Linux. 

Domyślnie opcja "Bezpieczny transfer wymagane" jest wyłączona.

> [!NOTE]
> Ponieważ Magazyn Azure nie obsługuje protokołu HTTPS dla niestandardowych nazw domen, ta opcja nie została zastosowana podczas korzystania z niestandardowej nazwy domeny.

## <a name="enable-secure-transfer-required-in-the-azure-portal"></a>Włącz "Bezpieczny transfer wymagane" w portalu Azure

Można włączyć "bezpieczny transfer wymagane" ustawienie zarówno podczas tworzenia konta magazynu w [portalu Azure](https://portal.azure.com), a w przypadku istniejących kont magazynu.

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a>Wymaga zapewnienia bezpiecznego transferu podczas tworzenia konta magazynu

1. Otwórz **utworzyć konto magazynu** bloku w portalu Azure.
1. W obszarze **bezpieczny transfer wymagane**, wybierz pozycję **włączone**.

  ![Zrzut ekranu](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a>Wymaga zapewnienia bezpiecznego transferu do istniejącego konta magazynu

1. Wybierz istniejące konto magazynu w portalu Azure.
1. Wybierz **konfiguracji** w obszarze **ustawienia** w bloku menu konta magazynu.
1. W obszarze **bezpieczny transfer wymagane**, wybierz pozycję **włączone**.

  ![Zrzut ekranu](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a>Włącz "Bezpieczny transfer wymagane" programowo

Nazwa ustawienia to _supportsHttpsTrafficOnly_ we właściwościach konta magazynu. Można włączyć "Zapewnienia bezpiecznego transferu wymagane" Ustawianie za pomocą interfejsu API REST, narzędzi lub biblioteki:

* **Interfejs API REST** (wersja: 2016-12-01): [wersji pakietu](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)
* **PowerShell** (wersja: 4.1.0): [wersji pakietu](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)
* **Interfejs wiersza polecenia** (wersja: 2.0.11): [wersji pakietu](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)
* **NodeJS** (wersja: 1.1.0): [wersji pakietu](https://www.npmjs.com/package/azure-arm-storage/)
* **Zestaw .NET SDK** (wersja: 6.3.0): [wersji pakietu](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)
* **Zestaw SDK Python** (wersja: 1.1.0): [wersji pakietu](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)
* **Zestaw SDK dopisków fonetycznych** (wersja: 0.11.0): [wersji pakietu](https://rubygems.org/gems/azure_mgmt_storage)

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a>Włącz "Zapewnienia bezpiecznego transferu wymagane" Ustawianie za pomocą interfejsu API REST

Aby ułatwić testowanie za pomocą interfejsu API REST, można użyć [ArmClient](https://github.com/projectkudu/ARMClient) wywoływanie z wiersza polecenia.

 Aby sprawdzić ustawienie przy użyciu interfejsu API REST służy poniżej wiersza polecenia:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

W odpowiedzi, można znaleźć _supportsHttpsTrafficOnly_ ustawienie. Przykład:

```Json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}",
  "kind": "Storage",
  ...
  "properties": {
    ...
    "supportsHttpsTrafficOnly": false
  },
  "type": "Microsoft.Storage/storageAccounts"
}
```

Aby włączyć ustawienie przy użyciu interfejsu API REST służy poniżej wiersza polecenia:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
Przykład Input.json:
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a>Następne kroki
Magazyn Azure oferuje rozbudowany zestaw funkcji zabezpieczeń, które razem umożliwiają deweloperom tworzenie bezpiecznych aplikacji. Aby uzyskać więcej informacji, odwiedź stronę [przewodnik zabezpieczeń magazynu](storage-security-guide.md).
