---
title: "Zarządzanie kontami usługi Azure Media przy użyciu programu PowerShell"
description: "Dowiedz się, jak zarządzać kontami usługi Azure Media Services za pomocą poleceń cmdlet programu PowerShell."
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: 3d999d9e27844bc0164cc3572522b9ec022118a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a>Zarządzanie kontami usługi Azure Media przy użyciu programu PowerShell
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> Aby można było utworzyć konto usługi Azure Media Services, musi mieć konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Bezpłatna wersja próbna platformy Azure</a>.
> 
> 

## <a name="overview"></a>Omówienie
Ten artykuł zawiera listę poleceń cmdlet programu Azure PowerShell dla usługi Azure Media Services (AMS) w ramach usługi Azure Resource Manager. Istnieją polecenia cmdlet w **Microsoft.Azure.Commands.Media** przestrzeni nazw.

## <a name="versions"></a>Wersje
**ApiVersion**: "2015-10-01"

## <a name="new-azurermmediaservice"></a>New-AzureRmMediaService
Tworzy usługę nośnika.

### <a name="syntax"></a>Składnia
Zestaw parametrów: StorageAccountIdParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

Zestaw parametrów: StorageAccountsParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a>Parametry
**-ResourceGroupName &lt;ciągu&gt;**

Określa nazwę grupy zasobów, do którego należy ta usługa multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |0 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-AccountName &lt;ciągu&gt;**

Określa nazwę usługi multimediów.

| Aliasy | Nazwa |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |1 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-Lokalizacji &lt;ciągu&gt;**

Określa lokalizację zasobów usługi multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |2 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-StorageAccountId &lt;ciągu&gt;**

Określa konto magazynu głównego, który skojarzony z usługą media.

* Nowe konto magazynu (utworzone przy użyciu interfejsu API usługi Resource Manager) obsługiwany tylko przez system.
* Konto magazynu musi istnieć i ma tę samą lokalizację w usłudze media.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |3 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Nazwa zestawu parametrów |StorageAccountIdParamSet |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Określa kont magazynu, które są skojarzone z usługą media.

* Nowe konto magazynu (utworzone przy użyciu interfejsu API usługi Resource Manager) obsługiwany tylko przez system.
* Konto magazynu musi istnieć i ma tę samą lokalizację w usłudze media.
* Tylko jedno konto magazynu można określić jako podstawowy.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |3 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Nazwa zestawu parametrów |StorageAccountsParamSet |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-Znaczniki &lt;Hashtable&gt;**

Określa tablicy skrótów tagów, które są skojarzone z usługą media.

* Przykład: @{"tag1"="wartość1";" tag2 "=: wartość2"}

| Aliasy | Brak |
| --- | --- |
| Wymagane? |wartość false |
| Pozycja? |o nazwie |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

**&lt;Właściwość CommandParameters&gt;**

To polecenie cmdlet obsługuje typowe parametry: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction i -WarningVariable.

### <a name="inputs"></a>Dane wejściowe
Typ danych wejściowych to typ obiektów, które można przekazać w potoku do polecenia cmdlet.

### <a name="outputs"></a>dane wyjściowe
Typ danych wyjściowych to typ obiektów emitowanych przez polecenie cmdlet.

## <a name="set-azurermmediaservice"></a>Set-AzureRmMediaService
Aktualizacje usługi multimediów.

### <a name="syntax"></a>Składnia
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a>Parametry
**-ResourceGroupName &lt;ciągu&gt;**

Określa nazwę grupy zasobów, do którego należy ta usługa multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |0 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-AccountName &lt;ciągu&gt;**

Określa nazwę usługi multimediów.

| Aliasy | Nazwa |
| --- | --- |
| Wymagane? |True |
| Pozycja? |1 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |False |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Określa kont magazynu, które są skojarzone z usługą media.

* Nowe konto magazynu (utworzone przy użyciu interfejsu API usługi Resource Manager) obsługiwany tylko przez system.
* Konto magazynu musi istnieć i ma tę samą lokalizację w usłudze media.
* Tylko jedno konto magazynu można określić jako podstawowy.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |wartość false |
| Pozycja? |o nazwie |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Nazwa zestawu parametrów |StorageAccountsParamSet |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-Znaczniki &lt;Hashtable&gt;**

Określa tablicy skrótów tagów, które są skojarzone z tą usługą multimediów.

* Tagi, które są skojarzone z usługą media są zastępowane podana przez klienta.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |False |
| Pozycja? |o nazwie |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**&lt;Właściwość CommandParameters&gt;**

To polecenie cmdlet obsługuje typowe parametry: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction i -WarningVariable.

### <a name="inputs"></a>Dane wejściowe
Typ danych wejściowych to typ obiektów, które można przekazać w potoku do polecenia cmdlet.

### <a name="outputs"></a>dane wyjściowe
Typ danych wyjściowych to typ obiektów emitowanych przez polecenie cmdlet.

## <a name="remove-azurermmediaservice"></a>Remove-AzureRmMediaService
Usuwa usługi multimediów.

### <a name="syntax"></a>Składnia
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametry
**-ResourceGroupName &lt;ciągu&gt;**

Określa nazwę grupy zasobów, do którego należy ta usługa multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |0 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-AccountName &lt;ciągu&gt;**

Określa nazwę usługi multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |2 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |False |

**&lt;Właściwość CommandParameters&gt;**

To polecenie cmdlet obsługuje typowe parametry: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction i -WarningVariable.

### <a name="inputs"></a>Dane wejściowe
Typ danych wejściowych to typ obiektów, które można przekazać w potoku do polecenia cmdlet.

### <a name="outputs"></a>dane wyjściowe
Typ danych wyjściowych to typ obiektów emitowanych przez polecenie cmdlet.

## <a name="get-azurermmediaservice"></a>Get-AzureRmMediaService
Pobiera wszystkie usługi media services w grupie zasobów lub usług media o podanej nazwie.

### <a name="syntax"></a>Składnia
ParameterSet: ResourceGroupParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

ParameterSet: AccountNameParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametry
**-ResourceGroupName &lt;ciągu&gt;**

Określa nazwę grupy zasobów, do którego należy ta usługa multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |0 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Nazwa zestawu parametrów |ResourceGroupParameterSet, AccountNameParameterSet |

Akceptowanie symboli wieloznacznych?   wartość false

**-AccountName &lt;ciągu&gt;**

Określa nazwę usługi multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |1 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Nazwa zestawu parametrów |AccountNameParameterSet |
| Akceptowanie symboli wieloznacznych? |wartość false |

**&lt;Właściwość CommandParameters&gt;**

To polecenie cmdlet obsługuje typowe parametry: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction i -WarningVariable.

### <a name="inputs"></a>Dane wejściowe
Typ danych wejściowych to typ obiektów, które można przekazać w potoku do polecenia cmdlet.

### <a name="outputs"></a>dane wyjściowe
Typ danych wyjściowych to typ obiektów emitowanych przez polecenie cmdlet.

## <a name="get-azurermmediaservicekeys"></a>Get-AzureRmMediaServiceKeys
Pobiera klucze usługi multimediów.

### <a name="syntax"></a>Składnia
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametry
**-ResourceGroupName &lt;ciągu&gt;**

Określa nazwę grupy zasobów, do którego należy ta usługa multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |0 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-AccountName &lt;ciągu&gt;**

Określa nazwę usługi multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |1 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**&lt;Właściwość CommandParameters&gt;**

To polecenie cmdlet obsługuje typowe parametry: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction i -WarningVariable.

### <a name="inputs"></a>Dane wejściowe
Typ danych wejściowych to typ obiektów, które można przekazać w potoku do polecenia cmdlet.

### <a name="outputs"></a>dane wyjściowe
Typ danych wyjściowych to typ obiektów emitowanych przez polecenie cmdlet.

## <a name="set-azurermmediaservicekey"></a>Set-AzureRmMediaServiceKey
Generuje ponownie klucz podstawowy lub pomocniczy usługi multimediów.

### <a name="syntax"></a>Składnia
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a>Parametry
**-ResourceGroupName &lt;ciągu&gt;**

Określa nazwę grupy zasobów, do którego należy ta usługa multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |0 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-AccountName &lt;ciągu&gt;**

Określa nazwę usługi multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |1 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-KeyType &lt;Właściwość KeyType&gt;**

Określa typ klucza usługi multimediów.

* Podstawowy lub pomocniczy

| Aliasy | Brak |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |2 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

**&lt;Właściwość CommandParameters&gt;**

To polecenie cmdlet obsługuje typowe parametry: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction i -WarningVariable.

### <a name="inputs"></a>Dane wejściowe
Typ danych wejściowych to typ obiektów, które można przekazać w potoku do polecenia cmdlet.

### <a name="outputs"></a>dane wyjściowe
Typ danych wyjściowych to typ obiektów emitowanych przez polecenie cmdlet.

## <a name="sync-azurermmediaservicestoragekeys"></a>Sync-AzureRmMediaServiceStorageKeys
Synchronizuje klucze konta magazynu dla konta magazynu skojarzone z usługą media.

### <a name="syntax"></a>Składnia
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametry
**-ResourceGroupName &lt;ciągu&gt;**

Określa nazwę grupy zasobów, do którego należy ta usługa multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |0 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-AccountName &lt;ciągu&gt;**

Określa nazwę usługi multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |1 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-StorageAccountId &lt;ciągu&gt;**

Określa konto magazynu skojarzonych z usługą media.

| Aliasy | Identyfikator |
| --- | --- |
| Wymagane? |Wartość true |
| Pozycja? |2 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**&lt;Właściwość CommandParameters&gt;**

To polecenie cmdlet obsługuje typowe parametry: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction i -WarningVariable.

### <a name="inputs"></a>Dane wejściowe
Typ danych wejściowych to typ obiektów, które można przekazać w potoku do polecenia cmdlet.

### <a name="outputs"></a>dane wyjściowe
Typ danych wyjściowych to typ obiektów emitowanych przez polecenie cmdlet.

## <a name="next-step"></a>Następny krok
Zapoznaj się z ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

