---
title: "zapewnienia bezpiecznego transferu aaaRequire w usłudze Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o funkcji \"Wymaga zapewnienia bezpiecznego transferu\" hello usługi Azure Storage i jak tooenable go."
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
ms.openlocfilehash: 27f745c5e771b50213c1dbb39dee081947be1f39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="require-secure-transfer"></a>Wymaganie bezpiecznego transferu

Opcja Hello "zapewnienia bezpiecznego transferu wymagane" zwiększa bezpieczeństwo hello konta magazynu, zezwalając tylko żądania toohello konta magazynu z bezpiecznych połączeń. Na przykład podczas wywoływania interfejsów API REST tooaccess Twojego konta magazynu, należy połączyć przy użyciu protokołu HTTPS. Wszystkie żądania przy użyciu protokołu HTTP są odrzucane po włączeniu "Bezpieczny transfer wymagane".

Korzystając z usługi pliki Azure hello, każde połączenie bez szyfrowania nie powiedzie się, gdy "Bezpieczny transfer wymagane" jest włączona. W tym scenariuszy przy użyciu protokołu SMB 2.1, SMB 3.0 bez szyfrowania i niektórych odmian powitania klienta SMB w systemie Linux. 

Domyślnie opcja hello "zapewnienia bezpiecznego transferu wymagane" jest wyłączona.

> [!NOTE]
> Ponieważ Magazyn Azure nie obsługuje protokołu HTTPS dla niestandardowych nazw domen, ta opcja nie została zastosowana podczas korzystania z niestandardowej nazwy domeny.

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a>Włącz "Zapewnienia bezpiecznego transferu wymagane" w hello portalu Azure

Można włączyć hello "zapewnienia bezpiecznego transferu wymagane" zarówno ustawienie podczas tworzenia konta magazynu w hello [portalu Azure](https://portal.azure.com), a w przypadku istniejących kont magazynu.

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a>Wymaga zapewnienia bezpiecznego transferu podczas tworzenia konta magazynu

1. Otwórz hello **utworzyć konto magazynu** bloku w hello portalu Azure.
1. W obszarze **bezpieczny transfer wymagane**, wybierz pozycję **włączone**.

  ![Zrzut ekranu](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a>Wymaga zapewnienia bezpiecznego transferu do istniejącego konta magazynu

1. Wybierz istniejące konto magazynu w hello portalu Azure.
1. Wybierz **konfiguracji** w obszarze **ustawienia** w bloku menu konta magazynu hello.
1. W obszarze **bezpieczny transfer wymagane**, wybierz pozycję **włączone**.

  ![Zrzut ekranu](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a>Włącz "Bezpieczny transfer wymagane" programowo

Nazwa ustawienia Hello jest _supportsHttpsTrafficOnly_ we właściwościach konta magazynu. Można włączyć "Zapewnienia bezpiecznego transferu wymagane" Ustawianie za pomocą interfejsu API REST, narzędzi lub biblioteki:

* **Interfejs API REST** (wersja: 2016-12-01): [wersji pakietu](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)
* **PowerShell** (wersja: 4.1.0): [wersji pakietu](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)
* **Interfejs wiersza polecenia** (wersja: 2.0.11): [wersji pakietu](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)
* **NodeJS** (wersja: 1.1.0): [wersji pakietu](https://www.npmjs.com/package/azure-arm-storage/)
* **Zestaw .NET SDK** (wersja: 6.3.0): [wersji pakietu](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)
* **Zestaw SDK Python** (wersja: 1.1.0): [wersji pakietu](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)
* **Zestaw SDK dopisków fonetycznych** (wersja: 0.11.0): [wersji pakietu](https://rubygems.org/gems/azure_mgmt_storage)

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a>Włącz "Zapewnienia bezpiecznego transferu wymagane" Ustawianie za pomocą interfejsu API REST

toosimplify testowanie za pomocą interfejsu API REST, można użyć [ArmClient](https://github.com/projectkudu/ARMClient) toocall z wiersza polecenia.

 Możesz użyć poniżej ustawienia hello toocheck wiersza polecenia z hello interfejsu API REST:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

W odpowiedzi hello można znaleźć _supportsHttpsTrafficOnly_ ustawienie. Przykład:

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

Możesz użyć poniżej ustawienia hello tooenable wiersza polecenia z hello interfejsu API REST:

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
Usługa Azure Storage zapewnia rozbudowany zestaw funkcji zabezpieczeń, które razem umożliwiają deweloperom toobuild bezpiecznych aplikacji. Aby uzyskać więcej informacji, odwiedź stronę hello [przewodnik zabezpieczeń magazynu](storage-security-guide.md).
