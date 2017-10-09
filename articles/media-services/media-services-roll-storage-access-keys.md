---
title: "klucze dostępu aaaUpdate Media Services po wycofanie magazynu | Dokumentacja firmy Microsoft"
description: "W tym artykule umożliwiają wskazówki dotyczące sposobu tooupdate Media Services po wycofanie magazynu klucze dostępu."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a892ebb0-0ea0-4fc8-b715-60347cc5c95b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: milanga;cenkdin;juliako
ms.openlocfilehash: 26fa7a75a73397842aaebda59516a00f68ab97f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a>Aktualizacja usługi Media Services po wycofanie kluczy dostępu do magazynu

Podczas tworzenia nowego konta usługi Azure Media Services (AMS), należy także tooselect usługi Azure Storage to znaczy konta używane toostore zawartości nośnika. Można dodać więcej niż jeden magazyn kont tooyour konta usługi Media Services. W tym temacie przedstawiono sposób toorotate magazynu kluczy. Pokazuje też, jak magazynu tooadd kont konta usługi media tooa. 

w tym temacie opisano akcje hello tooperform, należy używać [ARM interfejsów API](https://docs.microsoft.com/rest/api/media/mediaservice) i [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).  Aby uzyskać więcej informacji, zobacz [jak toomanage Azure zasobów przy użyciu programu PowerShell i Menedżera zasobów](../azure-resource-manager/powershell-azure-resource-manager.md).

## <a name="overview"></a>Omówienie

Po utworzeniu nowego konta magazynu Azure generuje dwa klucze dostępu do magazynu 512-bitowe, które są używane tooauthenticate uzyskać dostęp do konta magazynu tooyour. tookeep bardziej bezpieczne, zalecane jest tooperiodically połączenia z magazynem ponownie wygenerować i obracania klucz dostępu do magazynu. Dwa klucze dostępu (podstawowych i pomocniczych) są dostarczane w kolejności tooenable możesz toomaintain połączeń toohello konto magazynu przy użyciu jednej dostępu klucza podczas ponownego generowania hello drugi klucz dostępu. Ta procedura jest również nazywany "stopniowego klucze dostępu".

Usługi Media Services zależy od podane tooit klucza magazynu. W szczególności lokalizatorów hello, które są używane toostream lub pobrać zasobów są zależne od klucz dostępu do magazynu określony hello. Po utworzeniu konta usługi AMS ma zależność na klucz dostępu do magazynu podstawowego hello domyślnie, ale jako użytkownik można zaktualizować hello klucz magazynu, który ma AMS. Należy się upewnić się, że toolet Media Services wiedzieć, który klucza toouse wykonując kroki opisane w tym temacie.  

>[!NOTE]
> Jeśli masz wiele kont magazynu, można zastosować tę procedurę za pomocą każdego konta magazynu. kolejność Hello, w którym obracania magazynu kluczy nie jest stały. Można obrócić klucza pomocniczego hello najpierw i następnie hello podstawowy klucz lub na odwrót.
>
> Przed wykonaniem kroków opisanych w tym temacie na koncie produkcji, upewnij się, że tootest je na koncie produkcji wstępnej.
>

## <a name="steps-toorotate-storage-keys"></a>Kroki toorotate magazynu kluczy 
 
 1. Zmień hello magazynu klucza podstawowego konta za pomocą polecenia cmdlet programu powershell hello lub [Azure](https://portal.azure.com/) portalu.
 2. Wywołaj polecenie cmdlet AzureRmMediaServiceStorageKeys synchronizacji z odpowiednie parametry tooforce nośnika konta toopick się klucze konta magazynu
 
    Witaj poniższy przykład pokazuje, jak toosync kluczy toostorage kont.
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. Zaczekaj godzinę. Sprawdź, czy działają hello scenariusze przesyłania strumieniowego.
 4. Zmiana klucza pomocniczego konta magazynu za pomocą polecenia cmdlet programu powershell hello lub portalu Azure.
 5. Wywołanie synchronizacji AzureRmMediaServiceStorageKeys powershell za pomocą odpowiednich parametrów tooforce nośnika konta toopick się nowych kluczy kont magazynu. 
 6. Zaczekaj godzinę. Sprawdź, czy działają hello scenariusze przesyłania strumieniowego.
 
### <a name="a-powershell-cmdlet-example"></a>Przykład polecenia cmdlet programu powershell 

Witaj poniższym przykładzie pokazano, jak tooget hello konta magazynu i zsynchronizować go z kontem hello AMS.

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a>Konto tooyour AMS kont magazynu tooadd kroki

Witaj poniższy temat opisuje sposób magazynu tooadd kont konta tooyour AMS: [dołączyć wiele tooa kont magazynu konta usługi Media Services](meda-services-managing-multiple-storage-accounts.md).

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>Potwierdzenia
Chcielibyśmy hello tooacknowledge od osób, które przyczyniły się do tworzenia tego dokumentu: Seva Titov Cenk Dingiloglu, Gada Mediolan.
