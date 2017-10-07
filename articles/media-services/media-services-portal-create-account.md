---
title: "aaaCreate konta usługi Azure Media Services z hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki hello tworzenia konta usługi Azure Media Services z hello portalu Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: c551e158-aad6-47b4-931e-b46260b3ee4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: juliako
ms.openlocfilehash: fdad93d5d470fc08380670ec0f6c2d33468b1492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-media-services-account-using-hello-azure-portal"></a>Tworzenie konta usługi Azure Media Services przy użyciu hello portalu Azure
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toocomplete tego samouczka jest potrzebne konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Witaj portalu Azure umożliwia tooquickly Tworzenie konta usługi Azure Media Services (AMS). Możesz użyć tooaccess Twojego konta usługi Media Services, który toostore można włączyć, szyfrowania, zakodować, zarządzanie i przesyłanie strumieniowe zawartości na platformie Azure. W czasie hello Utwórz konto usługi Media Services, możesz również utworzyć skojarzone konto magazynu (lub użyć istniejącego) hello — w tym samym regionie geograficznym jako hello konta usługi Media Services.

W tym artykule opisano niektóre typowe pojęcia i przedstawiono, jak konto toocreate Media Services z hello portalu Azure.

## <a name="concepts"></a>Pojęcia
Uzyskiwanie dostępu do usługi Media Services wymaga dwóch skojarzonych kont:

* Konto usługi Media Services. Twoje zapewnia konta dostęp tooa zbiór oparte na chmurze usługi Media Services, które są dostępne w systemie Azure. Na koncie usługi Media Services nie jest przechowywana zawartość multimedialna. Zamiast tego są przechowywane metadane dotyczące zawartości multimedialnej hello oraz zadania przetwarzania multimediów na Twoim koncie. W czasie hello tworzenia hello konta możesz wybrać dostępny region usługi Media Services. Wybrany region Hello jest centrum danych, która przechowuje hello rekordów metadanych dla konta.
  
* Konto usługi Azure Storage. Konta magazynu musi znajdować się w hello tym samym regionie geograficznym jako hello konta usługi Media Services. Podczas tworzenia konta usługi Media Services można wybrać istniejące konto magazynu w hello tego samego regionu, lub można utworzyć nowe konto magazynu w hello tego samego regionu. Jeśli usuniesz konto usługi Media Services, obiekty BLOB hello w powiązanym koncie magazynu nie zostaną usunięte.

> [!NOTE]
> Aby uzyskać informacje na temat dostępności funkcji usługi Azure Media Services w różnych regionach, zobacz temat opisujący [dostępność funkcji usługi AMS w centrach danych](scenarios-and-availability.md#availability).

## <a name="create-an-ams-account"></a>Tworzenie konta AMS
kroki Hello w tej sekcji Pokaż jak konto toocreate AMS.

1. Zaloguj się w hello [portalu Azure](https://portal.azure.com/).
2. Kliknij pozycję **+Nowe** > **Sieci Web i mobilność** > **Media Services**.
   
    ![Tworzenie usługi Media Services](./media/media-services-create-account/media-services-new1.png)
3. Na stronie **TWORZENIE KONTA USŁUGI MEDIA SERVICES** wprowadź wymagane wartości.
   
    ![Tworzenie usługi Media Services](./media/media-services-create-account/media-services-new3.png)
   
   1. W **nazwa konta**, wprowadź nazwę nowego konta usługi AMS hello hello. Nazwa konta usługi Media Services jest wszystkie małe litery i cyfry, bez spacji i długości 3 znaków too24.
   2. W ramach subskrypcji Wybieranie spośród hello różnych subskrypcji Azure mających dostęp do.
   3. W **grupy zasobów**, wybierz hello nowy lub istniejący zasób.  Grupa zasobów jest kolekcją zasobów, które mają ten sam cykl życia, uprawnienia i zasady. Więcej informacji można znaleźć [tutaj](../azure-resource-manager/resource-group-overview.md#resource-groups).
   4. W **lokalizacji**, wybierz hello region geograficzny, które będzie używane toostore hello nośników i rekordów metadanych dla konta usługi Media Services. Ten region będzie używana tooprocess i przesyłania strumieniowego multimediów. W polu listy rozwijanej hello są wyświetlane tylko hello dostępne regiony usługi Media Services. 
   5. W **konta magazynu**, wybierz magazyn obiektów blob magazynu konta tooprovide hello zawartości multimedialnej z konta usługi Media Services. Można wybrać istniejące konto magazynu w hello tego samego regionu geograficznego konta usługi Media Services, lub można utworzyć konta magazynu. Nowe konto magazynu jest tworzony w hello sam region. reguły powitania dla konta magazynu, że nazwy są hello takie same jak w przypadku konta usługi Media Services.
      
       Więcej informacji o magazynie można znaleźć [tutaj](../storage/common/storage-introduction.md).
   6. Wybierz **toodashboard numeru Pin** toosee hello postęp wdrażania konta hello.
4. Kliknij przycisk **Utwórz** u dołu hello hello formularza.
   
    Po pomyślnym utworzeniu konta hello ładuje stronę przeglądu. W hello przesyłania strumieniowego punktu końcowego tabeli hello konto będzie mieć domyślnego punktu końcowego w hello przesyłania strumieniowego **zatrzymane** stanu. 

    >[!NOTE]
    >Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu. 
   
## <a name="toomanage-your-ams-account"></a>toomanage Twojego konta usługi AMS

toomanage kontem AMS (na przykład połączenie programowe toohello interfejsu API usług AMS, przekazywania plików wideo, kodowania elementów zawartości, skonfiguruj ochronę zawartości, monitorowania postępu zadania) wybierz **ustawienia** na powitania po lewej stronie portalu hello. Z hello **ustawienia**, przejdź tooone bloków dostępne hello (na przykład: **dostępu do interfejsu API**, **zasoby**, **zadania**, **Zawartości ochrony**).


## <a name="next-steps"></a>Następne kroki

Teraz możesz przekazać pliki na konto usługi AMS. Więcej informacji znajduje się na stronie [Przekazywanie plików](media-services-portal-upload-files.md).

Jeśli planujesz tooaccess interfejsu API usług AMS programowo, zobacz [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md).

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

