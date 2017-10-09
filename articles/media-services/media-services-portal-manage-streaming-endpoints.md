---
title: "punkty końcowe z portalu Azure hello przesyłania strumieniowego aaaManage | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób toomanage punktów końcowych przesyłania strumieniowego z hello portalu Azure."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a>Zarządzanie punktów końcowych przesyłania strumieniowego z hello portalu Azure

W tym temacie przedstawiono sposób toouse hello punktów końcowych przesyłania strumieniowego toomanage portalu Azure. 

>[!NOTE]
>Upewnij się, że hello tooreview [omówienie](media-services-streaming-endpoints-overview.md) tematu. 

Aby uzyskać informacje o sposobie tooscale hello punktu końcowego przesyłania strumieniowego, zobacz [to](media-services-portal-scale-streaming-endpoints.md) tematu.

## <a name="start-managing-streaming-endpoints"></a>Rozpocznij zarządzanie punktów końcowych przesyłania strumieniowego 

toostart Zarządzanie punktów końcowych przesyłania strumieniowego dla Twojego konta, hello następujące.

1. W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.
2. W hello **ustawienia** bloku, wybierz opcję **punkty końcowe przesyłania strumieniowego**.
   
    ![Punkt końcowy przesyłania strumieniowego](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> Rozliczenie jest przeprowadzane tylko w przypadku przesyłania strumieniowego punktu końcowego jest w stanie uruchomienia.

## <a name="adddelete-a-streaming-endpoint"></a>Dodawanie/Usuwanie punktu końcowego przesyłania strumieniowego

>[!NOTE]
>Nie można usunąć domyślnej Hello punktu końcowego przesyłania strumieniowego.

tooadd/usuwania przesyłania strumieniowego punktu końcowego za pomocą hello portalu Azure, hello następujące:

1. tooadd punktu końcowego przesyłania strumieniowego, kliknij przycisk hello **+ punktu końcowego** u góry hello hello strony. 

    Jeśli planujesz toohave może ma wiele punktów końcowych przesyłania strumieniowego innego CDN lub CDN oraz bezpośredni dostęp do.

2. Naciśnij klawisz toodelete punktu końcowego przesyłania strumieniowego, **usunąć** przycisku.      
3. Kliknij przycisk hello **Start** hello toostart przycisk punktu końcowego przesyłania strumieniowego.
   
    ![Punkt końcowy przesyłania strumieniowego](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <a id="configure_streaming_endpoints"></a>Konfigurowanie hello punktu końcowego przesyłania strumieniowego
Punktu końcowego przesyłania strumieniowego umożliwia hello tooconfigure następujące właściwości:

* Kontrola dostępu
* Kontrola pamięci podręcznej
* Granic lokacji zasad dostępu

Aby uzyskać szczegółowe informacje na temat tych właściwości, zobacz [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).

Można skonfigurować punktu końcowego przesyłania strumieniowego, wykonując następujące hello:

1. Wybierz hello ma tooconfigure punktu końcowego przesyłania strumieniowego.
2. Kliknij przycisk **ustawienia**.

Krótki opis pola hello się poniżej.

![Punkt końcowy przesyłania strumieniowego](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. Maksymalna pamięć podręczna zasad: okres istnienia pamięci podręcznej tooconfigure używane zasoby obsługiwane za pomocą tego punktu końcowego przesyłania strumieniowego. Jeśli wartość nie jest ustawiona, używana jest domyślna hello. wartości domyślne Hello można zdefiniować w taki sposób, bezpośrednio w magazynie Azure. Jeśli włączono Azure CDN hello punktu końcowego przesyłania strumieniowego, nie należy ustawiać hello pamięci podręcznej zasad wartość tooless niż 600 sekund.  
2. Dozwolone adresy IP: używane adresy IP toospecify, których mogliby tooconnect toohello opublikowane punktu końcowego przesyłania strumieniowego. Jeśli nie określono adresów IP, dowolnego adresu IP będą mogli tooconnect. Adresy IP można określić jako pojedynczy adres IP (na przykład "10.0.0.1"), zakresu adresów IP przy użyciu adresu IP i maski podsieci CIDR (na przykład "10.0.0.1/22") lub zakres adresów IP przy użyciu adresu IP i maski podsieci dziesiętną kropkami (na przykład 10.0.0.1 () 255.255.255.0) ").
3. Konfiguracja Akamai podpis nagłówka uwierzytelniania: używane toospecify konfiguracji podpis nagłówka uwierzytelniania żądania z Akamai serwerów. Wygaśnięcia jest w formacie UTC.

## <a name="scale-your-premium-streaming-endpoint"></a>Skalowanie programu Premium punktu końcowego przesyłania strumieniowego

Aby uzyskać więcej informacji, zobacz [ten](media-services-portal-scale-streaming-endpoints.md) temat.

## <a id="enable_cdn"></a>Włącz integrację usługi Azure CDN

Podczas tworzenia nowego konta integracji przesyłania strumieniowego punktu końcowego usługi Azure CDN domyślny jest domyślnie włączona.

Jeśli chcesz później hello toodisable/enable CDN, przesyłania strumieniowego punktu końcowego musi należeć do hello **zatrzymana** stanu. Między hello wszystkich punktów POP w sieci CDN może potrwać godziny too2 tooget integracji usługi Azure CDN hello włączone i toobe zmiany hello active. Jednak można uruchomić punktu końcowego oraz strumienia bez przerw w działaniu przesyłania z hello punktu końcowego przesyłania strumieniowego i po ukończeniu integracji hello strumienia hello są dostarczane z hello CDN. Podczas inicjowania obsługi administracyjnej okres hello będzie punktu końcowego przesyłania strumieniowego w **uruchamianie** stanu i użytkownik może obserwować degredad wydajności.

Integracja usługi CDN jest włączona we wszystkich execpt centrach danych platformy Azure hello Chin i regiony rządu federalnego.

Po włączeniu hello **kontroli dostępu**, **niestandardowej nazwy hosta** i **uwierzytelnianie za pomocą sygnatury Akamai** konfiguracja zostanie wyłączona.
 
> [!IMPORTANT]
> Integracja usługi Azure Media Services z usługą Azure CDN jest wdrażana w **Azure CDN from Verizon** standardu punkty końcowe przesyłania strumieniowego. Punkty końcowe przesyłania strumieniowego Premium można skonfigurować przy użyciu wszystkich **Azure CDN ceny warstw i dostawców**. Aby uzyskać więcej informacji na temat funkcji usługi Azure CDN, zobacz hello [Omówienie usługi CDN](../cdn/cdn-overview.md).
 
### <a name="additional-considerations"></a>Dodatkowe zagadnienia

* Po włączeniu przesyłania strumieniowego punktu końcowego CDN klientów nie można żądać zawartości bezpośrednio z hello źródła. Należy tootest możliwości hello zawartości z lub bez sieci CDN w warstwie można utworzyć innego przesyłania strumieniowego punktu końcowego, który nie jest włączona w sieci CDN.
* Twoje przesyłania strumieniowego pozostaje nazwę hosta punktu końcowego hello sam po włączeniu usługi CDN. Nie trzeba toomake każdy przepływ pracy usług, zmiany tooyour nośnika po włączeniu usługi CDN. Na przykład jeśli Twoje przesyłania strumieniowego hosta punktu końcowego jest strasbourg.streaming.mediaservices.windows.net, po włączeniu usługi CDN, dokładnie tej samej nazwy hosta hello jest używany.
* Dla nowych punktów końcowych przesyłania strumieniowego można włączyć CDN za tworzenie nowego punktu końcowego; istniejące punkty końcowe przesyłania strumieniowego wymaga punktu końcowego hello stop toofirst, a następnie Włącz/Wyłącz hello CDN.
* Standardowego punktu końcowego przesyłania strumieniowego można skonfigurować tylko za pomocą **dostawcy sieci CDN w warstwie standardowa Verizon** za pomocą portalu zarządzania Azure. Jednak można włączyć innych dostawców usługi Azure CDN przy użyciu interfejsów API REST.

## <a name="configure-cdn-profile"></a>Skonfiguruj profil CDN

Można skonfigurować profil CDN hello, wybierając hello **Zarządzanie CDN** przycisk od góry hello.

![Punkt końcowy przesyłania strumieniowego](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a>Następne kroki
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

