---
title: "aaaManage kont usługi Azure Media przy użyciu programu PowerShell"
description: "Dowiedz się, jak toomanage usługi Azure Media Services kont za pomocą poleceń cmdlet programu PowerShell."
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
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a>Zarządzanie kontami usługi Azure Media przy użyciu programu PowerShell
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toobe stanie toocreate konta usługi Azure Media Services, musi mieć konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Bezpłatna wersja próbna platformy Azure</a>.
> 
> 

## <a name="overview"></a>Omówienie
Ten artykuł zawiera listę poleceń cmdlet programu Azure PowerShell hello Azure Media Services (AMS) w ramach usługi Azure Resource Manager hello. polecenia cmdlet Hello istnieje w hello **Microsoft.Azure.Commands.Media** przestrzeni nazw.

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

Określa nazwę hello hello toowhich grupy zasobów, której należy ta usługa multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |0 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-AccountName &lt;ciągu&gt;**

Określa nazwę usługi multimediów hello hello.

| Aliasy | Nazwa |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |1 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-Lokalizacji &lt;ciągu&gt;**

Określa lokalizację zasobów hello hello media service.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |2 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-StorageAccountId &lt;ciągu&gt;**

Określa konto magazynu głównego, który skojarzony z usługą media hello.

* Nowe konto magazynu (utworzone z hello interfejsu API usługi Resource Manager) obsługiwany tylko przez system.
* Witaj konta magazynu musi istnieć i ma hello tej samej lokalizacji z usługą media hello.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |3 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Nazwa zestawu parametrów |StorageAccountIdParamSet |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Określa kont magazynu, które są skojarzone z usługą media hello.

* Nowe konto magazynu (utworzone z hello interfejsu API usługi Resource Manager) obsługiwany tylko przez system.
* Witaj konta magazynu musi istnieć i ma hello tej samej lokalizacji z usługą media hello.
* Tylko jedno konto magazynu można określić jako podstawowy.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |3 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Nazwa zestawu parametrów |StorageAccountsParamSet |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-Znaczniki &lt;Hashtable&gt;**

Określa tablicy skrótów hello tagów, które są skojarzone z usługą media hello.

* Przykład: @{"tag1"="wartość1";" tag2 "=: wartość2"}

| Aliasy | Brak |
| --- | --- |
| Wymagana? |wartość false |
| Pozycja? |o nazwie |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

**&lt;Właściwość CommandParameters&gt;**

To polecenie cmdlet obsługuje typowe parametry hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction i - WarningVariable.

### <a name="inputs"></a>Dane wejściowe
Typ danych wejściowych Hello jest typu hello hello obiekty przekazać toohello polecenia cmdlet.

### <a name="outputs"></a>dane wyjściowe
Typ danych wyjściowych Hello jest emituje typu hello hello obiektów, które hello polecenia cmdlet.

## <a name="set-azurermmediaservice"></a>Set-AzureRmMediaService
Aktualizacje usługi multimediów.

### <a name="syntax"></a>Składnia
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a>Parametry
**-ResourceGroupName &lt;ciągu&gt;**

Określa nazwę hello hello toowhich grupy zasobów, której należy ta usługa multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |0 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-AccountName &lt;ciągu&gt;**

Określa nazwę usługi multimediów hello hello.

| Aliasy | Nazwa |
| --- | --- |
| Wymagana? |True |
| Pozycja? |1 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |False |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Określa kont magazynu, które są skojarzone z usługą media hello.

* Nowe konto magazynu (utworzone z hello interfejsu API usługi Resource Manager) obsługiwany tylko przez system.
* Witaj konta magazynu musi istnieć i ma hello tej samej lokalizacji z usługą media hello.
* Tylko jedno konto magazynu można określić jako podstawowy.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |wartość false |
| Pozycja? |o nazwie |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Nazwa zestawu parametrów |StorageAccountsParamSet |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-Znaczniki &lt;Hashtable&gt;**

Określa tablicy skrótów hello tagów, które są skojarzone z tą usługą media.

* Witaj tagi, które są skojarzone z usługą media hello są zastępowane wartość określoną przez powitania klienta.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |False |
| Pozycja? |o nazwie |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**&lt;Właściwość CommandParameters&gt;**

To polecenie cmdlet obsługuje typowe parametry hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction i - WarningVariable.

### <a name="inputs"></a>Dane wejściowe
Typ danych wejściowych Hello jest typu hello hello obiekty przekazać toohello polecenia cmdlet.

### <a name="outputs"></a>dane wyjściowe
Typ danych wyjściowych Hello jest emituje typu hello hello obiektów, które hello polecenia cmdlet.

## <a name="remove-azurermmediaservice"></a>Remove-AzureRmMediaService
Usuwa usługi multimediów.

### <a name="syntax"></a>Składnia
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametry
**-ResourceGroupName &lt;ciągu&gt;**

Określa nazwę hello hello toowhich grupy zasobów, której należy ta usługa multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |0 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-AccountName &lt;ciągu&gt;**

Określa nazwę usługi multimediów hello hello.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |2 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |False |

**&lt;Właściwość CommandParameters&gt;**

To polecenie cmdlet obsługuje typowe parametry hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction i - WarningVariable.

### <a name="inputs"></a>Dane wejściowe
Typ danych wejściowych Hello jest typu hello hello obiekty przekazać toohello polecenia cmdlet.

### <a name="outputs"></a>dane wyjściowe
Typ danych wyjściowych Hello jest emituje typu hello hello obiektów, które hello polecenia cmdlet.

## <a name="get-azurermmediaservice"></a>Get-AzureRmMediaService
Pobiera wszystkie usługi media services w grupie zasobów lub usług media o podanej nazwie.

### <a name="syntax"></a>Składnia
ParameterSet: ResourceGroupParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

ParameterSet: AccountNameParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametry
**-ResourceGroupName &lt;ciągu&gt;**

Określa nazwę hello hello toowhich grupy zasobów, której należy ta usługa multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |0 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Nazwa zestawu parametrów |ResourceGroupParameterSet, AccountNameParameterSet |

Akceptowanie symboli wieloznacznych?   wartość false

**-AccountName &lt;ciągu&gt;**

Określa nazwę usługi multimediów hello hello.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |1 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Nazwa zestawu parametrów |AccountNameParameterSet |
| Akceptowanie symboli wieloznacznych? |wartość false |

**&lt;Właściwość CommandParameters&gt;**

To polecenie cmdlet obsługuje typowe parametry hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction i - WarningVariable.

### <a name="inputs"></a>Dane wejściowe
Typ danych wejściowych Hello jest typu hello hello obiekty przekazać toohello polecenia cmdlet.

### <a name="outputs"></a>dane wyjściowe
Typ danych wyjściowych Hello jest emituje typu hello hello obiektów, które hello polecenia cmdlet.

## <a name="get-azurermmediaservicekeys"></a>Get-AzureRmMediaServiceKeys
Pobiera klucze usługi multimediów.

### <a name="syntax"></a>Składnia
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametry
**-ResourceGroupName &lt;ciągu&gt;**

Określa nazwę hello hello toowhich grupy zasobów, której należy ta usługa multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |0 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-AccountName &lt;ciągu&gt;**

Określa nazwę usługi multimediów hello hello.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |1 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**&lt;Właściwość CommandParameters&gt;**

To polecenie cmdlet obsługuje typowe parametry hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction i - WarningVariable.

### <a name="inputs"></a>Dane wejściowe
Typ danych wejściowych Hello jest typu hello hello obiekty przekazać toohello polecenia cmdlet.

### <a name="outputs"></a>dane wyjściowe
Typ danych wyjściowych Hello jest emituje typu hello hello obiektów, które hello polecenia cmdlet.

## <a name="set-azurermmediaservicekey"></a>Set-AzureRmMediaServiceKey
Generuje ponownie klucz podstawowy lub pomocniczy usługi multimediów.

### <a name="syntax"></a>Składnia
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a>Parametry
**-ResourceGroupName &lt;ciągu&gt;**

Określa nazwę hello hello toowhich grupy zasobów, której należy ta usługa multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |0 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-AccountName &lt;ciągu&gt;**

Określa nazwę usługi multimediów hello hello.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |1 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-KeyType &lt;Właściwość KeyType&gt;**

Określa typ klucza hello hello media service.

* Podstawowy lub pomocniczy

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |2 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

**&lt;Właściwość CommandParameters&gt;**

To polecenie cmdlet obsługuje typowe parametry hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction i - WarningVariable.

### <a name="inputs"></a>Dane wejściowe
Typ danych wejściowych Hello jest typu hello hello obiekty przekazać toothe polecenia cmdlet.

### <a name="outputs"></a>dane wyjściowe
Typ danych wyjściowych Hello jest emituje typu hello hello obiektów, które hello polecenia cmdlet.

## <a name="sync-azurermmediaservicestoragekeys"></a>Sync-AzureRmMediaServiceStorageKeys
Synchronizuje klucze konta magazynu dla konta magazynu skojarzone z usługą media hello.

### <a name="syntax"></a>Składnia
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametry
**-ResourceGroupName &lt;ciągu&gt;**

Określa nazwę hello hello toowhich grupy zasobów, której należy ta usługa multimediów.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |0 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-AccountName &lt;ciągu&gt;**

Określa nazwę usługi multimediów hello hello.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |1 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**-StorageAccountId &lt;ciągu&gt;**

Określa konto magazynu hello skojarzonych z usługą media hello.

| Aliasy | Identyfikator |
| --- | --- |
| Wymagana? |Wartość true |
| Pozycja? |2 |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |True(ByPropertyName) |
| Akceptowanie symboli wieloznacznych? |wartość false |

**&lt;Właściwość CommandParameters&gt;**

To polecenie cmdlet obsługuje typowe parametry hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction i - WarningVariable.

### <a name="inputs"></a>Dane wejściowe
Typ danych wejściowych Hello jest typu hello hello obiekty przekazać toohello polecenia cmdlet.

### <a name="outputs"></a>dane wyjściowe
Typ danych wyjściowych Hello jest emituje typu hello hello obiektów, które hello polecenia cmdlet.

## <a name="next-step"></a>Następny krok
Zapoznaj się z ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

