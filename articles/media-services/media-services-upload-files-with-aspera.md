---
title: "pliki aaaUpload do konta usługi Azure Media Services przy użyciu Aspera | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki hello przekazywania plików do konta magazynu, który jest skojarzony z kontem usługi Media Services przy użyciu hello ** Aspera serwera na żądanie ** usługi na platformie Azure."
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a>Przekazywanie plików do konta usługi Media Services przy użyciu hello Aspera serwera na żądanie usługi na platformie Azure

## <a name="overview"></a>Omówienie

**Aspera** to oprogramowanie do szybkiego transferowania plików. Usługa **Aspera Server On Demand** dla platformy Azure umożliwia szybkie przekazywanie i pobieranie dużych plików bezpośrednio do i z magazynu obiektów blob platformy Azure. Aby uzyskać informacje o **Aspera na żądanie**, zobacz hello [chmury Aspera](http://cloud.asperasoft.com/) lokacji. 
  
**Serwer Aspera na żądanie** Azure jest dostępne do zakupu od hello [witrynę Azure marketplace](https://azure.microsoft.com/en-us/marketplace/). W celu toocomplete zakupu **Aspera serwera na żądanie** dla platformy Azure, należy zalogować się do portalu Azure Marketplace z swojego identyfikatora Windows Live.

Ten samouczek przedstawia kroki hello przekazywania plików do konta magazynu, który jest skojarzony z kontem usługi Media Services przy użyciu hello **Aspera serwera na żądanie** usługi na platformie Azure. 

Przykład działania toouse Azure z Aspera i usługi Media Services można znaleźć [tutaj](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).

>[!NOTE]
>Brak limitu toohello maksymalny obsługiwany rozmiar pliku do przetwarzania w usłudze Azure Media Services procesory multimediów (MP). Zobacz [to](media-services-quotas-and-limitations.md) tematu, aby uzyskać szczegółowe informacje dotyczące limitu rozmiaru pliku hello.
>

## <a name="prerequisites"></a>Wymagania wstępne 

toocomplete tego samouczka należy:

* Identyfikator usługi Windows Live
* [Konto platformy Azure](https://azure.microsoft.com). Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/). 
* [Konto usługi Azure Media Services](media-services-portal-create-account.md).

## <a name="purchase-aspera-on-demand-for-azure"></a>Kupowanie usługi Aspera On Demand dla platformy Azure

Po użytkownik zalogował się do portalu Azure Marketplace, należy wykonać te podstawowe kroki toocomplete zakupie Aspera na żądanie dla platformy Azure.

1. Wyszukaj nazwę Aspera i wybierz pozycję „Server On Demand”.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. Przejrzyj hello plany subskrypcji i kliknij przycisk "Utwórz konto"

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. Wprowadź szczegóły powitania serwera na żądanie subskrypcji.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. Polecenie hello **warstwy cenowej** i wybierz odpowiednią woluminu miesięczne hello sub panelu. W hello **planowanie szczegóły** panelu, wybierz opcję **OK**. Następnie w hello **wybierz warstwę cenową** panelu, kliknij przycisk **wybierz**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. Polecenie **postanowienia prawne** tooview i zaakceptuj postanowienia prawne hello hello sub panelu. Po przejrzeniu hello postanowienia prawne, kliknij przycisk **zakupu**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. Ukończ zakupu hello klikając **Utwórz**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. Hello Azure pulpitu nawigacyjnego ogłaszamy, że jest inicjowania obsługi usługi hello.  Po zakończeniu z inicjowaniem obsługi administracyjnej przez wyszukiwanie w Twoich zasobów dla nazwy hello hello usługi można znaleźć hello nową subskrypcję. Po znalezieniu hello usługi, podwójne kliknięcie portalu zarządzania usługami hello toolaunch.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. Uruchom program hello Aspera management portal. Po znalezieniu nowej usługi Aspera mogą uzyskać dostęp do portalu zarządzania toohello, klikając hello usługi.  Zostanie uruchomiony nowy panel. Od w tym nowym panelu należy tooclick na powitania **Nazwa zasobu** z nowej usługi.  W hello następującego zrzutu ekranu Nazwa zasobu hello jest "AsperaTransferDemo". Po kliknięciu hello Nazwa zasobu jest uruchamiana innego panelu. W tym nowo uruchomionym panelu zobaczysz link „Zarządzaj”. Polecenie hello portalu zarządzania Aspera hello toolaunch link "Zarządzaj".

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. Klikając hello zarządzać link, zostanie wyświetlona strona rejestracji toohello, co jest wymagane tooaccess hello usługi.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. W tym momencie powinien mieć dostęp toohello Aspera portalu zarządzania usługami, gdzie można utworzyć klucze dostępu, Pobierz Aspera klientów i licencji, Wyświetl użycie i Dowiedz się więcej o hello interfejsów API.

    Witaj Poniższy zrzut ekranu przedstawia hello tworzenia dostępu. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    Witaj Poniższy zrzut ekranu przedstawia raportowanie interfejsów w portalu hello hello użycia. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a>Przekazywanie plików za pomocą usługi Aspera

1. Pobierz i zainstaluj oprogramowanie klienckie Aspera hello:
    
    * [Wtyczka przeglądarki](http://downloads.asperasoft.com/connect2/)
    * [Klient wzbogacony](http://downloads.asperasoft.com/en/downloads/2)

2. Przeprowadź pierwszy transfer. Kolejność toouse hello Aspera klienta tootransfer z hello Aspera transfer service niezbędne są następujące hello toocomplete: 

    1. Utwórz klucz dostępu za pomocą portalu Aspera hello.  
    2. Pobieranie, instalacji i licencji hello Aspera klienta (oprogramowania można znaleźć w portalu Aspera hello).  

    >[!NOTE]
    >Przeczytaj przewodnik klienta Aspera hello informacji o konfiguracji.
    
    3. Pobrać niektóre informacje o koncie magazynu, który jest skojarzony z Twoim kontem multimediów Azure przy użyciu hello [portalu Azure](https://portal.azure.com/). W szczególności nazwy i klucza, a nazwa kontenera obiektów blob magazynu hello w toowhich ma tooplace zawartości. 

        * informacje dotyczące tooget hello magazynu z portalu hello: znaleźć konta magazynu, kliknij hello klawisze dostępu, a kopia klucza nazwy i hello hello Twojego konta.
        * Nazwa kontenera hello tooget: znaleźć konta magazynu, wybierz opcję **obiekty BLOB**, wybierz pozycję hello nazwa kontenera hello tooupload hello zawartość do. 

    Poniżej przedstawiono zrzut ekranu powitania klienta Aspera hello **Menedżera połączeń** gdzie należy określić typ magazynu "Azure" hello i poświadczenia, a także hello kontenera obiektów blob.

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a>Zasoby

Witaj następujące zasoby zostały wymienione w tym artykule. 

* [Nawiązywanie połączenia z wtyczką przeglądarki](http://downloads.asperasoft.com/connect2/)
* [Przewodnik po nawiązywaniu połączeń](http://downloads.asperasoft.com/en/documentation/8)
* [Klient usługi Aspera](http://downloads.asperasoft.com/en/downloads/2)
* [Podręcznik klienta](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a>Następne kroki

Możesz teraz [kopiować obiekty blob z konta magazynu na konto usługi AMS](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

