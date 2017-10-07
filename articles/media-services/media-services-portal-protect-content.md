---
title: "zasady ochrony zawartości aaaConfiguring za pomocą hello portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono sposób toouse hello tooconfigure portalu Azure zasady ochrony zawartości. Witaj artykule jest także przedstawiono sposób dynamicznego szyfrowania tooenable trwałych."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a>Konfigurowanie zasad ochrony zawartości przy użyciu hello portalu Azure
> [!NOTE]
> toocomplete tego samouczka jest potrzebne konto platformy Azure. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
> 
> 

## <a name="overview"></a>Omówienie
Microsoft Azure Media Services (AMS) umożliwia toosecure możesz z hello razem, gdy opuszczą komputera za pośrednictwem przechowywania, przetwarzania i dostarczania multimediów. Usługa Media Services umożliwia toodeliver zawartości szyfrowane dynamicznie z Standard AES (Advanced Encryption) (przy użyciu 128-bitowe klucze szyfrowania), szyfrowania common encryption (CENC) za pomocą PlayReady lub Widevine DRM i FairPlay firmy Apple. 

AMS udostępnia usługę dostarczania licencji DRM i AES wyczyść klucze tooauthorized klientów. Witaj portalu Azure pozwala toocreate jedną **zasady autoryzacji klucza/licencji** dla wszystkich typów szyfrowania.

W tym artykule przedstawiono sposób tooconfigure zawartości zasady ochrony z hello portalu Azure. Witaj artykule jest także przedstawiono sposób tooapply szyfrowania dynamicznego tooyour zasoby.


> [!NOTE]
> Jeśli używasz zasad ochrony hello Azure classic portal toocreate hello zasad nie może występować w hello [portalu Azure](https://portal.azure.com/). Jednak wszystkie hello starego zasady nadal istnieje. Można sprawdzić za pomocą hello zestawu .NET SDK usługi Azure Media Services lub hello [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) narzędzia (toosee hello zasad, kliknij prawym przyciskiem myszy na powitania zasobów -> Wyświetl informacje (F4) -> -> kartę kluczy zawartości, kliknij polecenie Kliknij na powitania klucza). 
> 
> Tooencrypt zawartości przy użyciu nowych zasad, należy skonfigurować je z hello portalu Azure, kliknij przycisk Zapisz i ponowne zastosowanie szyfrowania dynamicznego. 
> 
> 

## <a name="start-configuring-content-protection"></a>Rozpocząć konfigurowanie ochrony zawartości
toouse hello portalu toostart Konfigurowanie ochrony zawartości, konto globalne tooyour AMS hello następujące:

1. W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.
2. Wybierz **ustawienia** > **zawartości ochrony**.

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a>Zasady autoryzacji klucza/licencji
AMS obsługuje wiele sposobów uwierzytelniania użytkowników, którzy tworzą żądania licencji lub klucza. zasady autoryzacji klucza zawartości Hello musi być skonfigurowane przez użytkownika i spełnione przez klienta w kolejności hello klucz/licencji toobe delived toohello klienta. Witaj zasady autoryzacji klucza zawartości może mieć jeden lub więcej ograniczeń: **Otwórz** lub **tokenu** ograniczeń.

Witaj portalu Azure pozwala toocreate jedną **zasady autoryzacji klucza/licencji** dla wszystkich typów szyfrowania.

### <a name="open"></a>Otwarty
Otwórz ograniczeń oznacza, że hello system będzie dostarczać hello tooanyone klucza, który wysyła żądanie klucza. To ograniczenie mogą być przydatne do celów testowych. 

### <a name="token"></a>Token
Witaj zasadzie ograniczenia tokenu musi towarzyszyć token wystawiony przez Secure Token Service (STS). Usługa Media Services obsługuje tokenów w i hello proste tokenów sieci Web (SWT) format tokenu Web JSON (JWT). Usługi Media Services nie zapewnia bezpieczny tokenu usługi. Można utworzyć niestandardowy STS lub korzystać z usługi Microsoft Azure ACS tooissue tokenów. Witaj STS musi być skonfigurowany toocreate podpisany token hello określony klucz i wystawianie oświadczeń, określonych w konfiguracji ograniczenia tokenu hello. Hello Media Services, który zwróci usługi dostarczania klucza żądanej powitania klienta toohello (licencji lub klucza) Jeśli hello token jest prawidłowy i hello oświadczenia w hello token dopasowania tych skonfigurowane dla hello (licencji lub klucza).

Podczas konfigurowania hello zasadzie ograniczenia tokenu, należy określić klucz podstawowy weryfikacji hello, wystawcy i parametry odbiorców. klucz podstawowy weryfikacji Hello zawiera hello klucza, że hello token została podpisana z, wystawcy hello bezpiecznego tokenu usługi, która wystawia hello token. odbiorców Hello (nazywane również zakres) opisano hello celem hello token lub hello zasobów hello tokenu zezwala na dostęp do. Hello usługa Media Services klucza dostawy weryfikuje, czy te wartości w tokenie hello są takie same wartości hello hello szablonu.

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a>Szablon praw PlayReady
Aby uzyskać szczegółowe informacje o szablonie prawa PlayReady hello, zobacz [nośnika — omówienie szablon licencji PlayReady usług](media-services-playready-license-template-overview.md).

### <a name="non-persistent"></a>Inne niż stałe
Jeśli skonfigurujesz licencji jako trwałe go tylko przechowywana w pamięci podczas hello player używa hello licencji.  

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a>Stałe
Jeśli skonfigurujesz licencji hello jako trwałe jest zapisywany w magazynu trwałego na powitania klienta.

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a>Szablon praw Widevine
Aby uzyskać szczegółowe informacje o szablonie prawa Widevine hello, zobacz [omówienie szablonu licencji Widevine](media-services-widevine-license-template-overview.md).

### <a name="basic"></a>Podstawowa
Po wybraniu **podstawowe**, zostanie utworzony szablon hello z wszystkie wartości domyślne.

### <a name="advanced"></a>Advanced
Aby uzyskać szczegółowe informacje na temat Opcja Zaawansowane konfiguracje Widevine, zobacz [to](media-services-widevine-license-template-overview.md) tematu.

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a>Konfiguracja FairPlay
tooenable FairPlay szyfrowania, należy tooprovide hello aplikacji certyfikat i klucz tajny aplikacji (poproś) za pomocą opcji konfiguracji FairPlay hello. Aby uzyskać szczegółowe informacje o konfiguracji FairPlay i wymagania, zobacz [to](media-services-protect-hls-with-fairplay.md) artykułu.

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a>Zastosowanie szyfrowania dynamicznego tooyour zasobów
tootake korzystać z szyfrowania dynamicznego, należy tooencode pliku źródłowego do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów.

### <a name="select-an-asset-that-you-want-tooencrypt"></a>Wybierz zasób, które mają tooencrypt
Wybierz wszystkie zasoby, toosee **ustawienia** > **zasoby**.

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a>Szyfrowanie AES lub DRM
Po naciśnięciu **Szyfruj** na zasób, dostępne są dwie opcje: **AES** lub **DRM**. 

#### <a name="aes"></a>AES
Wyczyść klucza szyfrowania zostanie włączona na wszystkich protokołów transmisji strumieniowej AES: Smooth Streaming, HLS i MPEG-DASH.

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a>DRM
Po wybraniu karty DRM hello dostępne są różne opcje zasady ochrony zawartości (co należy skonfigurować już) + zestaw protokoły przesyłania strumieniowego.

* **PlayReady i Widevine z MPEG-DASH** -będzie dynamicznego szyfrowania strumienia MPEG-DASH PlayReady i Widevine DRMs.
* **PlayReady i Widevine z MPEG-DASH + FairPlay z HLS** -dynamicznie są szyfrowane możesz strumieni MPEG-DASH PlayReady i Widevine DRMs. Również są szyfrowane strumienie HLS z FairPlay.
* **PlayReady tylko w przypadku funkcji Smooth Streaming, HLS i MPEG-DASH** -będzie dynamicznego szyfrowania Smooth Streaming, HLS, strumieni MPEG-DASH z PlayReady DRM.
* **Widevine tylko z MPEG-DASH** -dynamicznego szyfrowania należy MPEG-DASH z Widevine DRM.
* **FairPlay tylko z HLS** -będzie dynamicznego szyfrowania strumienia HLS z FairPlay.

tooenable FairPlay szyfrowania, należy tooprovide hello aplikacji certyfikat i klucz tajny aplikacji (poproś) za pomocą opcji konfiguracji FairPlay bloku ustawienia ochrony zawartości hello hello.

![Ochrona zawartości](./media/media-services-portal-content-protection/media-services-content-protection009.png)

Po wprowadzeniu wybór szyfrowania hello naciśnij **Zastosuj**.

>[!NOTE] 
>Jeśli planujesz tooplay AES szyfrowane HLS w programie Safari, zobacz [ten blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).

## <a name="next-steps"></a>Następne kroki
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

