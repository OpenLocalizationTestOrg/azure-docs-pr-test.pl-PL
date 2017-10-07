---
title: "Konto magazynu platformy Azure z usługą Azure CDN aaaIntegrate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse zawartości hello Azure Content Delivery Network (CDN) toodeliver wysokiej przepustowości przez buforowanie obiektów blob z usługi Magazyn Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a>Integracja z usługą Azure CDN konta magazynu platformy Azure
Sieci CDN może być włączone toocache zawartości z magazynu Azure. Oferuje deweloperom globalne rozwiązanie umożliwiające dostarczanie zawartości wysokiej przepustowości przez buforowanie obiektów blob i zawartości statycznej wystąpień obliczeń w węzłach fizycznych hello USA, Europa, Azji, Australii i Ameryka Południowa.

## <a name="step-1-create-a-storage-account"></a>Krok 1: Utwórz konto magazynu
Użyj hello następujące procedury toocreate nowe konto magazynu dla subskrypcji platformy Azure. Konto magazynu zapewnia dostęp do usług magazynu platformy Azure. Konto magazynu Hello reprezentuje hello najwyższy poziom przestrzeń nazw hello dla uzyskiwania dostępu do poszczególnych składników usługi Magazyn Azure hello: obiektów Blob usługi, usługi kolejki i usługi tabeli. Aby uzyskać więcej informacji, zobacz toohello [tooMicrosoft wprowadzenie usługi Azure Storage](../storage/common/storage-introduction.md).

toocreate konta magazynu musi być hello administrator usługi albo współadministratorem dla hello skojarzone subskrypcji.

> [!NOTE]
> Istnieje kilka metod, można użyć toocreate konto magazynu, w tym hello portalu Azure i programu Powershell.  W tym samouczku będziemy używać hello portalu Azure.  
> 
> 

**toocreate konto magazynu dla subskrypcji platformy Azure**

1. Zaloguj się toohello [Azure Portal](https://portal.azure.com).
2. W górnym lewym rogu hello, wybierz **nowy**. W hello **nowy** zaznacz pozycję **dane i magazyn**, następnie kliknij przycisk **konta magazynu**.
    
    Witaj **utworzyć konto magazynu** zostanie wyświetlony blok.   

    ![Tworzenie konta magazynu][create-new-storage-account]  

3. W hello **nazwa** wpisz nazwę domeny podrzędnej. Ten wpis może zawierać 3 do 24 małych liter i cyfr.
   
    Ta wartość staje się nazwa hosta hello w hello identyfikator URI, który jest wykorzystywana do adresowania obiektów Blob, kolejki lub tabeli zasobów hello subskrypcji. Aby rozwiązać zasobu kontenera w hello usługa Blob, czy korzystania z identyfikatora URI hello zgodny z formatem, gdzie  *&lt;StorageAccountLabel&gt;*  odwołuje się wartość toohello wpisane w **wprowadź adres URL**:
   
    http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mojkontener&gt;*
   
    **Ważne:** hello adresu URL etykiety formularze hello poddomeny konta magazynu hello identyfikatora URI i musi być unikatowa wśród wszystkich usług hostowanych na platformie Azure.
   
    Ta wartość jest również używana jako nazwa hello tego konta magazynu w portalu hello lub podczas uzyskiwania dostępu do tego konta programowo.
4. Pozostaw ustawienia domyślne hello **modelu wdrażania**, **konta rodzaju**, **wydajności**, i **replikacji**. 
5. Wybierz hello **subskrypcji** czy konto magazynu hello będą używane z.
6. Wybierz lub utwórz **grupę zasobów**.  Więcej informacji na temat grup zasobów znajduje się w temacie [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Wybierz lokalizację dla konta magazynu.
8. Kliknij przycisk **Utwórz**. proces tworzenia konta magazynu hello Hello może potrwać kilka minut toocomplete.

## <a name="step-2-enable-cdn-for-hello-storage-account"></a>Krok 2: Włączanie CDN dla konta magazynu hello

Dzięki integracji najnowsze hello można teraz włączyć CDN dla konta magazynu bez opuszczania rozszerzenia portalu magazynu. 

1. Wybierz konto magazynu hello, wyszukiwanie "CDN" lub przewiń w dół menu nawigacji po lewej stronie powitania, a następnie kliknij przycisk "Azure CDN".
    
    Witaj **Azure CDN** zostanie wyświetlony blok.

    ![CDN Włącz nawigacji][cdn-enable-navigation]
    
2. Utwórz nowy punkt końcowy wprowadzając hello wymagane informacje
    - **Profil CDN**: można utworzyć nowy lub użyć istniejącego profilu.
    - **Warstwa cenowa**: wystarczy tooselect warstwy cenowej w przypadku utworzenia nowego profilu CDN.
    - **Nazwa punktu końcowego CDN**: Wprowadź nazwę punktu końcowego na wybór.

    > [!TIP]
    > punkt końcowy CDN Hello utworzona domyślnie używa hello nazwa hosta konta magazynu jako źródła.

    ! [tworzenie punktu końcowego cdn nowego] [cdn — nowy — utworzenie punktu końcowego]

3. Po utworzeniu nowy punkt końcowy hello będą widoczne w powyższej listy punktów końcowych hello.

    ![nowy punkt końcowy sieci CDN w warstwie magazynu][cdn-storage-new-endpoint]

> [!NOTE]
> Można także przejść tooAzure CDN rozszerzenia tooenable CDN. [Samouczek](#Tutorial-cdn-create-profile).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a>Krok 3: Włącz dodatkowe funkcje CDN

Z bloku "Azure CDN" konto magazynu kliknij punkt końcowy CDN hello z hello listy tooopen CDN konfiguracji bloku. Można włączyć dodatkowe funkcje sieci CDN w celu dostarczania, na przykład kompresji, ciąg zapytania geograficznie filtrowania. Można również dodać niestandardową domenę mapowania tooyour — punkt końcowy CDN i włączyć domeny niestandardowej HTTPS.
    
![Konfiguracja sieci CDN w warstwie magazynu CDN][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a>Krok 4: Dostęp do zawartości w sieci CDN
tooaccess pamięci podręcznej zawartości na powitania CDN, użyj hello adresu CDN zawarte w portalu hello. Hello adres pamięci podręcznej blob będzie podobne toohello następujące czynności:

http://<*EndpointName*\>.azureedge.net/ <*myPublicContainer*\>/<*element BlobName*\>

> [!NOTE]
> Po włączeniu konta magazynu tooa dostępu do sieci CDN wszystkich publicznie dostępnych obiektów kwalifikują się do buforowania krawędzi CDN. Po zmodyfikowaniu obiektu, który jest aktualnie w pamięci podręcznej hello CDN hello nową zawartość nie będzie dostępne za pośrednictwem hello CDN dopóki hello CDN odświeża jego zawartości, gdy hello buforowane okres czasu wygaśnięcia zawartości.
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a>Krok 5: Usuń zawartość z hello CDN
Jeśli nie chcesz już toocache obiektu w hello Azure sieci dostarczania zawartości (CDN), można wykonać jedną z hello następujące kroki:

* Możesz wprowadzić hello prywatnego kontenera zamiast publicznego. Zobacz [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiekty BLOB](../storage/blobs/storage-manage-access-to-resources.md) Aby uzyskać więcej informacji.
* Można wyłączyć lub usunąć punkt końcowy CDN hello przy użyciu hello portalu zarządzania.
* Można zmodyfikować Twojej usługi hostowanej toono dłużej odpowiedź toorequests dla obiekt hello.

Obiekt w sieci CDN hello już pamięci podręcznej pozostaje w pamięci podręcznej aż do okresu hello time-to-live dla obiekt hello lub punktu końcowego hello jest wyczyszczone. Po wygaśnięciu okresu time-to-live hello hello CDN sprawdzi toosee, czy punkt końcowy CDN hello jest nadal ważny i nadal anonimowo dostępny obiekt hello. Jeśli nie, obiekt hello już być buforowane.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Jak tooa CDN zawartości tooMap domeny niestandardowe](cdn-map-content-to-custom-domain.md)
* [Włącz protokół HTTPS dla domeny niestandardowej](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
