---
title: "informacje o wersji usługi aaaMedia | Dokumentacja firmy Microsoft"
description: "Informacje o wersji usługi multimediów"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ca2d7af-1cf0-45fa-9585-3b73f3ee057d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: media
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: c365b1133987267173ec858298c4c6de62744946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-release-notes"></a>Informacje o wersji usługi Azure Media Services
Te informacje o wersji zawierają podsumowanie zmian z poprzednich wersji i znane problemy.

> [!NOTE]
> Firma Microsoft ma toohear klientów i skoncentrować się na rozwiązywanie problemów, które dotyczy. tooreport problem lub zadać pytania, Opublikuj w hello [Forum MSDN usług Media Azure].
> 
> 

## <a id="issues"></a>Obecnie znane problemy
### <a id="general_issues"></a>Ogólne problemy dotyczące usługi Media Services
| Problem | Opis |
| --- | --- |
| Nie podano kilka typowych nagłówków HTTP w hello interfejsu API REST. |W przypadku tworzenia aplikacji usługi Media Services przy użyciu hello interfejsu API REST, stwierdzisz, że niektóre typowe pola nagłówka HTTP (w tym CLIENT-REQUEST-ID REQUEST-ID, a ZWRACANY-CLIENT-REQUEST-ID) nie są obsługiwane. nagłówki Hello zostanie dodana w przyszłej aktualizacji. |
| Kodowanie procent jest niedozwolone. |Usługi Media Services używa wartości hello hello właściwość IAssetFile.Name podczas kompilowania adresów URL dla hello przesyłania strumieniowego zawartości (na przykład http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Z tego powodu kodowania procent jest niedozwolone. Hello wartość hello **nazwa** właściwość nie może mieć jedną z następujących przyczyn hello [procent kodowanie zarezerwowanych znaków](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! * "();: @& = + $, /? [] % #". Ponadto może istnieć tylko jeden "." dla hello rozszerzenia nazwy pliku. |
| Witaj ListBlobs metodę, która jest częścią wersji zestawu SDK usługi Magazyn Azure hello 3.x nie powiedzie się. |Usługa Media Services generuje adresy URL SAS oparte na powitania [2012-02-12](https://docs.microsoft.com/rest/api/storageservices/Version-2012-02-12) wersji. Toouse zestawu SDK usługi Magazyn Azure toolist BLOB w kontenerze obiektów blob, należy użyć hello [CloudBlobContainer.ListBlobs](http://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.listblobs.aspx) metodę, która jest częścią zestawu SDK usługi Magazyn Azure w wersji 2.x. Witaj ListBlobs metodę, która jest częścią wersji zestawu SDK usługi Magazyn Azure hello 3.x zakończy się niepowodzeniem. |
| Mechanizm ograniczania usługi Media Services ogranicza hello użycie zasobów dla aplikacji, które należy nadmiernego żądania toohello usługi. Usługa Hello może zwróciła kod stanu HTTP Usługa niedostępna (503) hello. |Aby uzyskać więcej informacji, zobacz opis hello kod stanu HTTP hello 503 w hello [kodów błędów systemu Azure Media Services](media-services-encoding-error-codes.md) tematu. |
| Podczas wykonywania zapytania jednostek, istnieje limit 1000 jednostek zwracane w tym samym czasie, ponieważ publiczny v2 REST ogranicza wyniki too1000 wyników zapytania. |Należy toouse **Pomiń** i **zająć** (.NET) / **górnej** (REST) zgodnie z opisem w [w tym przykładzie .NET](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) i [tego interfejsu API REST przykład](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). |
| Niektórzy klienci mogą napotkać problemem powtarzania tag w manifeście Smooth Streaming hello. |Więcej informacji znajduje się w [tej](media-services-deliver-content-overview.md#known-issues) sekcji. |
| Azure obiekty .NET SDK usługi Media Services nie może być serializowany i w związku z tym nie działają z buforowaniem Azure. |Jeśli spróbujesz tooserialize hello SDK AssetCollection obiektu tooadd go tooAzure buforowanie, wyjątek zostanie zgłoszony. |
| Niepowodzenie zadania kodowania zawierające ciąg komunikatu "etap: DownloadFile. Kod: System.NullReferenceException ". |Witaj typowej kodowania przepływu pracy jest tooan wejściowych plików wideo tooupload wejściowe zasobów i przedstawia jedną lub więcej zadania kodowania w tym wprowadzić zasobów, bez konieczności modyfikacji dalsze, że dane wejściowe zasobów. Jednak Jeśli zmodyfikujesz hello wejściowych zasobów (na przykład przez dodawanie/usuwanie/zmiana nazwy plików w ramach hello zasobów), a następnie kolejne zadania może zakończyć się niepowodzeniem z powodu błędu DownloadFile. Obejście Hello jest toodelete hello wejściowych zasobów i ponownie przekazać dane wejściowe pliki tooa nowego elementu zawartości. |

## <a id="rest_version_history"></a>Historia wersji interfejsu API REST
Aby uzyskać informacje o hello Historia wersji interfejsu API REST usługi Media, zobacz [dokumentacja interfejsu API REST usługi Azure Media Services].

## <a name="june-2017-release"></a>2017 czerwca zlecenia

Usługa Media Services obsługuje teraz [usługi Azure Active Directory (Azure AD)-uwierzytelniania opartego na](media-services-use-aad-auth-to-access-ams-api.md).

> [!IMPORTANT]
> Obecnie usługa Media Services obsługuje hello Azure kontroli dostępu usługi uwierzytelniania modelu. Jednak na 1 czerwca 2018 zostaną wycofane autoryzacji kontroli dostępu. Zaleca się, jak najszybciej migracji model uwierzytelniania toohello usługi Azure AD.

## <a name="march-2017-release"></a>2017 marca zlecenia

Teraz możesz używać usługi Azure Media Standard zbyt[automatycznego generowania drabinę szybkości transmisji bitów](media-services-autogen-bitrate-ladder-with-mes.md) przez określenie "Adaptacyjne przesyłanie strumieniowe" hello ustawienia wstępnego ciągu podczas tworzenia zadania kodowania. "Adaptacyjnego przesyłania strumieniowego" jest hello zalecane ustawienia domyślne, jeśli chcesz tooencode wideo do przesyłania strumieniowego z usługi Media Services. Jeśli potrzebujesz toocustomize ustawienie wstępne kodowania dla konkretnego scenariusza, można przejść do [te](media-services-mes-presets-overview.md) ustawienia.

Można teraz używać usługi Azure Media Standard lub Media Encoder Premium w przepływie pracy zbyt[Tworzenie zadania kodowania, które generuje fragmentów fMP4](media-services-generate-fmp4-chunks.md). 


## <a name="febuary-2017-release"></a>Febuary 2017 zlecenia

Uruchamianie 1 kwietnia 2017 dowolnego rekordu zadania konta starsze niż 90 dni zostaną automatycznie usunięte, wraz z jego skojarzonych rekordów zadań, nawet jeśli hello całkowita liczba rekordów jest poniżej hello maksymalny limit przydziału. Jeśli potrzebujesz informacji zadania lub zadanie hello tooarchive, można użyć kodu hello opisane [tutaj](media-services-dotnet-manage-entities.md).

## <a name="january-2017-release"></a>Wersja stycznia 2017 r

W programie Microsoft Azure Media Services (AMS), **punktu końcowego przesyłania strumieniowego** reprezentuje usługę przesyłania strumieniowego, który może dostarczyć zawartości bezpośrednio tooa aplikacja odtwarzacza klienta lub tooa Content Delivery Network (CDN) w celu dalszej dystrybucji. Usługa Media Services udostępnia również bezproblemową integrację usługi Azure CDN. Hello strumienia wychodzącego z usługi StreamingEndpoint może być strumień na żywo, wideo na żądanie lub pobierania progresywnego zawartości na koncie usługi Media Services. Każde konto usługi Azure Media Services zawiera domyślne StreamingEndpoint. Dodatkowe punkty końcowe mogą być tworzone w ramach konta hello. Istnieją dwie wersje punkty końcowe, 1.0 i 2.0. Począwszy od stycznia 2017 10, wszystkie nowo utworzonego konta usługi AMS zostaną uwzględnione w wersji 2.0 **domyślne** StreamingEndpoint. Dodanie konta toothis punkty końcowe przesyłania strumieniowego dodatkowe będzie także w wersji 2.0. Ta zmiana nie ma wpływu na istniejące konta hello; istniejące punkty końcowe będą w wersji 1.0 i może być uaktualniony tooversion 2.0. Ta zmiana będzie zmiany zachowania, rozliczeń i funkcji (Aby uzyskać więcej informacji, zobacz [to](media-services-streaming-endpoints-overview.md) tematu).

Ponadto, począwszy od wersji hello 2.15, usługi Azure Media Services dodane hello następujące właściwości toohello punktu końcowego przesyłania strumieniowego jednostki: **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**. Aby uzyskać szczegółowe informacje o tych właściwości, zobacz [to](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint). 

## <a name="december-2016-release"></a>Wersja grudnia 2016

Usługa Azure Media Services umożliwia teraz tooaccess danych telemetrii/metryki dla swoich usług. Bieżąca wersja AMS Hello umożliwia zbierania danych telemetrycznych dla kanału na żywo, StreamingEndpoint, i na żywo jednostek archiwum. Aby uzyskać więcej informacji, zobacz [ten](media-services-telemetry-overview.md) temat.

## <a id="july_changes16"></a>Wersja z lipca 2016 r.
### <a name="updates-toomanifest-file-ism-generated-by-encoding-tasks"></a>Aktualizacje toomanifest pliku (*. ISM) generowany przez kodowania zadań
Podczas kodowania zadań jest przesłanych tooMedia Encoder Standard lub usługi Azure Media Encoder, generuje zadania kodowania hello [przesyłania strumieniowego pliku manifestu](media-services-deliver-content-overview.md) (* .ism) plików w hello output zasobów. Z najnowszej wersji usługi hello została zaktualizowana składnia hello przesyłania strumieniowego pliku manifestu.

> [!NOTE]
> Składnia Hello hello przesyłania strumieniowego pliku manifestu (.ism) jest zarezerwowany do użytku wewnętrznego i jest toochange podmiotu w przyszłych wersjach. Nie zmodyfikuj lub modyfikowania hello zawartość tego pliku.
> 
> 

### <a name="a-new-client-manifest-ismc-file-is-generated-in-hello-output-asset-when-an-encoding-task-outputs-one-or-more-mp4-files"></a>Nowy klient manifestu (*. Plik ISMC) jest generowany w hello output zasobów, gdy jeden lub więcej plików MP4 wyniki kodowania zadań
Począwszy od hello najnowszej wersji usługi, po zakończeniu zadania kodowania, które generuje jeden lub więcej plików MP4, hello hello wyjściowe zasobów zawiera również przesyłania strumieniowego pliku manifestu (*.ismc) klienta. plik .ismc Hello pomaga w zwiększeniu wydajności hello dynamiczne przesyłania strumieniowego. 

> [!NOTE]
> Składnia Hello pliku manifestu (.ismc) powitania klienta jest zarezerwowany do użytku wewnętrznego i jest toochange podmiotu w przyszłych wersjach. Nie zmodyfikuj lub modyfikowania hello zawartość tego pliku.
> 
> 

Aby uzyskać więcej informacji, zobacz [to](https://blogs.msdn.microsoft.com/randomnumber/2016/07/08/encoder-changes-within-azure-media-services-now-create-ismc-file/) blogu.

### <a name="known-issues"></a>Znane problemy
Niektórzy klienci mogą napotkać problemem powtarzania tag w manifeście Smooth Streaming hello. Więcej informacji znajduje się w [tej](media-services-deliver-content-overview.md#known-issues) sekcji.

## <a id="apr_changes16"></a>Wersja kwietnia 2016
### <a name="azure-media-analytics"></a>Analiza multimediów Azure
Azure Media Servces wprowadzono analizy multimediów Azure, zaawansowane analizy wideo. Aby uzyskać szczegółowe informacje, zobacz [Omówienie usługi Azure Media Services Analytics](media-services-analytics-overview.md).

### <a name="apple-fairplay-preview"></a>Apple FairPlay (wersja zapoznawcza)
Usługi Azure Media Services teraz umożliwia toodynamically można zaszyfrować Twojej HTTP Live Streaming (HLS) zawartości ze FairPlay firmy Apple. Umożliwia także tooclients licencje FairPlay toodeliver usługi AMS licencji dostarczania. Aby uzyskać szczegółowe informacje, zobacz [tooStream użycia usługi Azure Media Services HLS zawartości chronione przy użyciu firmy Apple FairPlay ](media-services-protect-hls-with-fairplay.md).

## <a id="feb_changes16"></a>Wersja lutego 2016
najnowszą wersję Hello Azure Media Services SDK dla platformy .NET (3.5.3) zawiera poprawkę pokrewne Widevine. Witaj problem został: AssetDeliveryPolicy nie można użyć ponownie dla wielu zasobów szyfrowane przy użyciu metody Widevine. Jako część tego hello Poprawka usterki następujące właściwości dodano toohello zestawu SDK: **WidevineBaseLicenseAcquisitionUrl**.

    Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
        new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
    {
        {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl,"http://testurl"},

    };

## <a id="jan_changes_16"></a>Wersja styczeń 2016
Zastrzeżone jednostki kodowania zmieniona pomyłek tooreduce z nazwami kodera.

Hello podstawowa, standardowa i Premium kodowania jednostki zarezerwowanego są tooS1 zmieniono nazwę, S2, i odpowiednio jednostki, zarezerwowane S3.  Klienci korzystający z podstawowych RUs kodowanie dzisiaj będą widzieli S1 jako etykieta hello w portalu Azure (i w hello BOM) podczas Standard i Premium zobaczą etykiety hello S2 i S3 odpowiednio. 

## <a id="dec_changes_15"></a>Wersja grudnia 2015 r.

### <a name="azure-media-encoder-deprecation-announcement"></a>Azure Media Encoder amortyzacja anonsu

Azure Media Encoder będzie przestarzałe, począwszy od wersji hello Media Encoder Standard około 12 miesięcy.

### <a name="azure-sdk-for-php"></a>Zestaw Azure SDK dla języka PHP
nową wersję hello opublikowane zespołu zestawu Azure SDK Hello [zestaw Azure SDK for PHP](http://github.com/Azure/azure-sdk-for-php) pakiet, który zawiera aktualizacje i nowe funkcje dla usługi Microsoft Azure Media Services. W szczególności hello Azure Media Services SDK dla programu PHP, teraz obsługuje hello najnowszych [zawartości ochrony](media-services-content-protection-overview.md) funkcji: dynamicznego szyfrowania AES i DRM (PlayReady i Widevine) z i bez ograniczeń tokenu. Obsługuje także skalowanie [jednostki kodowania](media-services-dotnet-encoding-units.md).

Aby uzyskać więcej informacji, zobacz:

* Witaj [Microsoft Azure Media Services SDK dla programu PHP](http://southworks.com/blog/2015/12/09/new-microsoft-azure-media-services-sdk-for-php-release-available-with-new-features-and-samples/) blogu.
* następujące Hello [przykłady kodu](http://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices) toohelp ułatwiające rozpoczęcie pracy szybko:
  * **vodworkflow_aes.php**: jest to plik PHP, który pokazuje sposób toouse dynamicznego szyfrowania AES-128 i usługi dostarczania klucza. Jest on oparty na przykład .NET hello wyjaśniono w [to](media-services-protect-with-aes128.md) artykułu.
  * **vodworkflow_aes.php**: jest to plik PHP, który pokazuje sposób toouse szyfrowania dynamicznego PlayReady i usługi dostarczania licencji. Jest on oparty na przykład .NET hello wyjaśniono w [to](media-services-protect-with-drm.md) artykułu.
  * **scale_encoding_units.php**: jest to plik PHP, który pokazuje, jak kodowanie tooscale zastrzeżone jednostki.

## <a id="nov_changes_15"></a>Listopad 2015 r.
Usługa Azure Media Services udostępnia teraz usługi dostarczania licencji Google Widevine w chmurze hello. Aby uzyskać więcej informacji, zobacz zbyt[ten blog anonsu](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/). Zobacz też [w tym samouczku](media-services-protect-with-drm.md) i [repozytorium GitHub](http://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm). 

Należy pamiętać, że usługi dostarczania licencji Widevine pochodzącymi z usługami multimediów Azure w wersji zapoznawczej. Aby uzyskać więcej informacji, zobacz [ten blog](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/).

## <a id="oct_changes_15"></a>Października 2015 r.
Azure Media Services (AMS) jest teraz na żywo w hello następujących centrach danych: Brazylia Południowa, Indie Zachodnie, Indie Południowe i Indie środkowe. Teraz możesz używać hello portalu Azure za[tworzenia kont usługi multimediów](media-services-portal-create-account.md) i wykonywania różnych zadań opisanych [tutaj](https://azure.microsoft.com/documentation/services/media-services/). Jednak w tych centrach danych nie jest obsługiwana funkcja Live Encoding. Ponadto nie wszystkie typy jednostek zarezerwowanych do celów związanych z kodowaniem są dostępne w tych centrach danych.

* Brazylia Południowa: dostępne są wyłącznie podstawowe i standardowe jednostki zarezerwowane do celów związanych z kodowaniem
* Indie Zachodnie, Indie Południowe i Indie Środkowe: dostępne są wyłącznie podstawowe jednostki zarezerwowane do celów związanych z kodowaniem

## <a id="september_changes_15"></a>Września 2015 r.
* AMS teraz oferty hello tooprotect możliwość zarówno wideo na żądanie (VOD), jak i strumienie na żywo przy użyciu technologii Widevine DRM modułowych. Można użyć następującego toohelp partnerów usługi dostarczania dostarczania licencji Widevine hello: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/). Aby uzyskać więcej informacji, zobacz [ten blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/).
  
    Można użyć [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (począwszy od wersji hello 3.5.1) lub REST API tooconfigure Twojego toouse AssetDeliveryConfiguration Widevine.  
* AMS dodano obsługę wideo ProRes firmy Apple. Możesz teraz przekazać pliki wideo źródła QuickTime korzystających z ProRes firmy Apple lub inne kodery-dekodery. Aby uzyskać więcej informacji, zobacz [ten blog](https://azure.microsoft.com/blog/announcing-support-for-apple-prores-videos-in-azure-media-services/).
* Można teraz używać Media Encoder Standard toodo podrzędna wycinka i na żywo wyodrębniania do archiwum. Aby uzyskać więcej informacji, zobacz [ten blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).
* wprowadzono następujące aktualizacje filtrowania Hello: 
  
  * Można teraz używać formatu Apple HTTP Live Streaming (HLS) z tylko dźwięk filtru. Ta aktualizacja pozwala tooremove Śledź tylko dźwięk, określając (tylko dźwięk = false) w adresie URL hello.
  * Definiowanie filtrów trwałych, jest teraz dostępna toocombine możliwości wielu (się too3) filtry w jeden adres URL.
    
    Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blogu.
* AMS obsługuje teraz-ramki w HLS w wersji 4. Obsługa ramki optymalizuje operacje szybkie przewijanie do przodu i do tyłu. Domyślnie wszystkie dane wyjściowe v4 HLS zawierają listy odtwarzania ramki (EXT-X-I-FRAME-STREAM-INF).
  
    Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blogu.

## <a id="august_changes_15"></a>Sierpnia 2015 r.
* SDK usługi Azure Media Services dla wersji Java V0.8.0 i nowe próbki są teraz dostępne. Aby uzyskać więcej informacji, zobacz:
  
  * [Wpis w blogu](http://southworks.com/blog/2015/08/25/microsoft-azure-media-services-sdk-for-java-v0-8-0-released-and-new-samples-available/)
  * [Repozytorium przykłady w języku Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
* Azure Media Player aktualizacji z obsługą wielu audio strumienia. Aby uzyskać więcej informacji, zobacz:
  * [Wpis w blogu](https://azure.microsoft.com/blog/2015/08/13/azure-media-player-update-with-multi-audio-stream-support/)

## <a id="july_changes_15"></a>Wersja z lipca 2015 r.
* Informuje o hello ogólnej dostępności usługi Media Encoder Standard. Aby uzyskać więcej informacji, zobacz [ten wpis w blogu](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/).
  
    Media Encoder Standard używa ustawienia opisane w [to](http://go.microsoft.com/fwlink/?LinkId=618336) sekcji. Należy pamiętać, że podczas korzystania z ustawienia domyślne dla koduje 4k, należy pobrać hello **Premium** zastrzeżone typu jednostki. Aby uzyskać więcej informacji, zobacz [jak tooScale kodowanie](media-services-scale-media-processing-overview.md).
* Podpisy w czasie rzeczywistym na żywo i usługi Azure Media Services Player. Aby uzyskać więcej informacji, zobacz [ten wpis w blogu](https://azure.microsoft.com/blog/2015/07/08/live-real-time-captions-with-azure-media-services-and-player/)

### <a name="media-services-net-sdk-updates"></a>Aktualizacje zestawu SDK .NET usługi Media Services
Azure SDK .NET usługi Media Services jest teraz wersji 3.4.0.0. w tej wersji dodano Hello następujące funkcje:  

* Obsługa zaimplementowanym archiwum na żywo. Należy pamiętać, że nie można pobrać zawartości, który zawiera archiwum na żywo.
* Obsługa zaimplementowanym filtrów dynamicznych.
* Zaimplementowane funkcje, które umożliwia kontenera magazynu tookeep użytkowników podczas usuwania zasobów.
* Poprawki błędów związanych z zasadami tooretry kanałów.
* Włączone **Media Encoder Premium w przepływie pracy**.

## <a id="june_changes_15"></a>Czerwca 2015 r.
### <a name="media-services-net-sdk-updates"></a>Aktualizacje zestawu SDK .NET usługi Media Services
Azure SDK .NET usługi Media Services jest teraz wersji 3.3.0.0. w tej wersji dodano Hello następujące funkcje:  

* Obsługa specyfikacji OpenId Connect odnajdywania
* obsługę przerzucania kluczy po stronie dostawcy tożsamości. 

Jeśli używasz dostawcy tożsamości, który udostępnia dokument OpenID Connect (jako hello czy następujących dostawców: usługi Azure Active Directory, Google, Salesforce), można nakazać podpisywania klucze do sprawdzania poprawności tokenu JWT z tooobtain usługi Azure Media Services Protokołu OpenID connect specyfikacji odnajdywania. 

Aby uzyskać więcej informacji, zobacz [przy użyciu Json klawiszy sieci Web z OpenID Connect toowork — dane odnajdywania z JWT token uwierzytelniania w usłudze Azure Media Services](http://gtrifonov.com/2015/06/07/using-json-web-keys-from-openid-connect-discovery-spec-to-work-with-jwt-token-authentication-in-azure-media-services/).

## <a id="may_changes_15"></a>Maja 2015 r.
Anonsowanie hello następujące nowe funkcje:

* [Podgląd Live Encoding w usłudze Media Services](media-services-manage-live-encoder-enabled-channels.md)
* [Dynamiczne manifestu](media-services-dynamic-manifest-overview.md)
* [Podgląd procesor multimediów Azure Media Hyperlapse](https://azure.microsoft.com/blog/?p=286281&preview=1&_ppp=61e1a0b3db)

## <a id="april_changes_15"></a>Wersji z kwietnia 2015 r.
### <a name="general-media-services-updates"></a>Usługi multimediów ogólne aktualizacji
* [Anonsowanie Azure Media Player](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/).
* Począwszy od Media Services REST 2.10, kanałów, które są skonfigurowane tooingest protokołu RTMP są tworzone z podstawowej i adresy URL pozyskiwania pomocniczej. Aby uzyskać więcej informacji, zobacz [konfiguracje pozyskiwania kanału](media-services-live-streaming-with-onprem-encoders.md#channel_input)
* Aktualizacje indeksatora multimediów Azure
* Obsługa języka hiszpańskiego
* Nowy format xml konfiguracji

Aby uzyskać więcej informacji, zobacz [ten blog](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).

### <a name="media-services-net-sdk-updates"></a>Aktualizacje zestawu SDK .NET usługi Media Services
Azure SDK .NET usługi Media Services jest teraz wersji 3.2.0.0.

Witaj poniżej przedstawiono niektóre aktualizacje hello klientów:

* **Fundamentalne zmiany**: zmienić **TokenRestrictionTemplate.Issuer** i **TokenRestrictionTemplate.Audience** toobe typu string.
* Aktualizacje dotyczące toocreating ponawiania niestandardowych zasad.
* Poprawki błędów związanych z toouploading/pobierania plików.
* Witaj **MediaServicesCredentials** klasy akceptuje teraz tooauthenticate punkt końcowy kontroli dostępu do podstawowego i pomocniczego przed.

## <a id="march_changes_15"></a>Wersja marca 2015 roku
### <a name="general-media-services-updates"></a>Usługi multimediów ogólne aktualizacji
* Usługa Media Services udostępnia teraz integracji usługi Azure CDN. toosupport hello integracji hello **CdnEnabled** właściwość została dodana zbyt**StreamingEndpoint**.  **CdnEnabled** mogą być używane z interfejsów API REST, począwszy od wersji 2.9 (Aby uzyskać więcej informacji, zobacz [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)).  **CdnEnabled** mogą być używane z zestawu .NET SDK, począwszy od wersji 3.1.0.2 (Aby uzyskać więcej informacji, zobacz [StreamingEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.istreamingendpoint\(v=azure.10\).aspx)).
* Ogłoszenie **Media Encoder Premium w przepływie pracy**. Aby uzyskać więcej informacji, zobacz [wprowadzenie Premium kodowania w usłudze Azure Media Services](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/).

## <a id="february_changes_15"></a>Lutego 2015 r.
### <a name="general-media-services-updates"></a>Usługi multimediów ogólne aktualizacji
Interfejs API REST usługi multimediów jest teraz wersji 2.9. Począwszy od tej wersji, można włączyć hello Azure CDN integracji z punktów końcowych przesyłania strumieniowego. Aby uzyskać więcej informacji, zobacz [StreamingEndpoint](https://msdn.microsoft.com/library/dn783468.aspx).

## <a id="january_changes_15"></a>Stycznia 2015 r.
### <a name="general-media-services-updates"></a>Usługi multimediów ogólne aktualizacji
Powiadomienia o ogólne dostępności (GA) ochrony zawartości w przypadku szyfrowania dynamicznego. Aby uzyskać więcej informacji, zobacz [usługi Azure Media Services zwiększa bezpieczeństwo przesyłania strumieniowego z technologią ogólne dostępności DRM](https://azure.microsoft.com/blog/2015/01/29/azure-media-services-enhances-streaming-security-with-general-availability-of-drm-technology/).

### <a name="media-services-net-sdk-updates"></a>Aktualizacje zestawu SDK .NET usługi Media Services
Azure SDK .NET usługi Media Services jest teraz wersji 3.1.0.1.

Ta wersja oznaczone hello Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization.TokenRestrictionTemplate Konstruktor jako przestarzałe. Nowy Konstruktor Hello przyjmuje TokenType jako argument.

    TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);


## <a id="december_changes_14"></a>Wersja z grudnia 2014
### <a name="general-media-services-updates"></a>Usługi multimediów ogólne aktualizacji
* Niektóre aktualizacje i nowe funkcje zostały dodane toohello procesora Azure Media indeksatora. Aby uzyskać więcej informacji, zobacz [informacje o wersji usługi Azure Media indeksatora wersji 1.1.6.7](https://azure.microsoft.com/blog/2014/12/03/azure-media-indexer-version-1-1-6-7-release-notes/).
* Dodaje nowy interfejs API REST umożliwiający tooupdate zastrzeżone jednostki kodowania: [EncodingReservedUnitType z POZOSTAŁĄ](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype).
* Dodano Obsługa mechanizmu CORS usługi dostarczania klucza.
* Ulepszenia wydajności kwerendy opcji zasad autoryzacji zostały wykonane.
* W centrum danych Chin hello [adres URL dostawy klucza](https://docs.microsoft.com/rest/api/media/operations/contentkey#get_delivery_service_url) jest teraz na klienta (podobnie jak w innych centrach danych).
* Dodano HLS automatycznie docelowego czasu trwania. W trakcie transmisji strumieniowych na żywo, HLS zawsze jest dostarczana dynamicznie. Domyślnie usługi Media Services automatycznie oblicza oparte na powitania klatki kluczowej interwału (KeyFrameInterval), nazywana także tooas grupy obrazów — GOP, odebrane z kodera na żywo hello HLS segmentu współczynnik opakowania (FragmentsPerSegment). Aby uzyskać więcej informacji, zobacz [Praca z usługi Azure Media Services transmisji strumieniowej na żywo].

### <a name="media-services-net-sdk-updates"></a>Aktualizacje zestawu SDK .NET usługi Media Services
* [Azure SDK .NET usługi Media Services](http://www.nuget.org/packages/windowsazure.mediaservices/) jest teraz wersji 3.1.0.0.
* Uaktualnić hello .net SDK too.NET zależności 4.5 Framework.
* Dodaje nowy interfejs API umożliwiający tooupdate zastrzeżone jednostki kodowania. Aby uzyskać więcej informacji, zobacz [aktualizowanie typ jednostki zarezerwowane i zwiększenie RUs kodowanie przy użyciu platformy .NET](media-services-dotnet-encoding-units.md).
* Dodano JWT (JSON Web Token) obsługę uwierzytelniania tokenu. Aby uzyskać więcej informacji, zobacz [JWT token uwierzytelniania w usłudze Azure Media Services i szyfrowania dynamicznego](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/).
* Dodano względną przesunięć BeginDate i ExpirationDate w szablonie licencji PlayReady hello.

## <a id="november_changes_14"></a>Listopadzie 2014 roku
* Usługa Media Services obecnie umożliwia tooingest funkcja live Smooth Streaming (FMP4) zawartości za pośrednictwem połączenia SSL. tooingest za pośrednictwem protokołu SSL, upewnij się, że hello tooupdate pozyskiwania tooHTTPS adres URL.  Należy zauważyć, że obecnie AMS nie obsługuje protokołu SSL z domen niestandardowych.  Aby uzyskać więcej informacji na temat transmisja strumieniowa na żywo, zobacz [Praca z usługi Azure Media Services transmisji strumieniowej na żywo].
* Nie można obecnie pozyskiwania RTMP strumień na żywo, za pośrednictwem połączenia SSL.
* Można tylko strumienia za pośrednictwem protokołu SSL Jeśli hello, z którego dostarczać zawartość z punktu końcowego przesyłania strumieniowego został utworzony po 10 września 2014 r. Jeśli Twoje adresy URL przesyłania strumieniowego są oparte na powitania utworzone po 10 września punkty końcowe przesyłania strumieniowego, hello adres URL zawiera "streaming.mediaservices.windows.net" (nowy format hello). Adresy URL przesyłania strumieniowego zawierające "origin.mediaservices.windows.net" (stary format hello) nie obsługują protokołu SSL. Jeśli adres URL jest w starym formacie hello i chcesz toobe toostream mogli za pośrednictwem protokołu SSL, [utworzyć nowy punkt końcowy przesyłania strumieniowego](media-services-portal-manage-streaming-endpoints.md). Użyj adresów URL tworzone w oparciu hello nowych przesyłania strumieniowego punktu końcowego toostream zawartości za pośrednictwem protokołu SSL.

## <a id="october_changes_14"></a>Wersji z października 2014 r.
### <a id="new_encoder_release"></a>Koder wersji usługi multimediów
Informuje o nowej wersji nośnika usługi Azure Media Encoder hello. Z hello najnowsze Azure Media Encoder tylko naliczona opłata za output GB, ale w przeciwnym razie kodera nowe hello jest funkcji zgodny z poprzednich kodera hello. Aby uzyskać więcej informacji [szczegóły cennika usługi Media Services]).

### <a id="oct_sdk"></a>Zestaw .NET SDK usługi multimediów
SDK usługi Media Services dla platformy .NET, rozszerzenia jest teraz wersji 2.0.0.3.

SDK usługi Media Services dla platformy .NET jest teraz wersji 3.0.0.8.

wprowadzono następujące zmiany Hello:

* Refaktoryzacja klas zasad ponawiania.
* Dodawanie nagłówków żądań toohttp ciąg agenta użytkownika.
* Dodawanie kroku kompilacji przywracania nuget.
* Naprawianie cert toouse x509 testy scenariusza z repozytorium.
* Sprawdzanie poprawności ustawienia po zakończeniu aktualizowania kanału i przesyłania strumieniowego.

### <a name="new-github-repository-toohost-media-services-samples"></a>Nowe próbki Media Services toohost repozytorium GitHub
Przykłady znajdują się w [repozytorium GitHub przykłady Azure Media Services](https://github.com/Azure/Azure-Media-Services-Samples).

## <a id="september_changes_14"></a>Września 2014 roku
Metadane Media Services REST jest teraz wersji 2.7. Aby uzyskać więcej informacji na temat hello najnowsze aktualizacje REST, zobacz [dokumentacja interfejsu API REST usługi Azure Media Services].

SDK usługi Media Services dla platformy .NET jest teraz wersji 3.0.0.7

### <a id="sept_14_breaking_changes"></a>Fundamentalne zmiany
* **Pochodzenie** zmieniono zbyt[StreamingEndpoint].
* Zmiana hello domyślnym zachowaniem podczas używania hello **portalu Azure** tooencode, a następnie opublikować pliki MP4.

Wcześniej, korzystając z toopublish klasycznego portalu Azure hello element zawartości wideo pojedynczego pliku MP4 adres URL SAS zostałyby utworzone (adresy URL SAS pozwalają toodownload hello wideo z magazynu obiektów blob). Obecnie podczas Użyj hello tooencode klasycznego portalu Azure, a następnie opublikować element zawartości wideo pojedynczego pliku MP4, hello wygenerowany adres URL punktów tooan usługi Azure Media Services punktu końcowego przesyłania strumieniowego.  Ta zmiana nie wpływa na wideo MP4, bezpośrednio przekazane tooMedia usług i opublikowanych bez kodowany w usłudze Azure Media Services.

Obecnie masz hello następujące dwie opcje toosolve hello problem.

* Włącz jednostki przesyłania strumieniowego i użyj dynamicznego tworzenia pakietów toostream hello plik MP4 zasobów jako prezentację płynnego przesyłania strumieniowego.
* Utwórz toodownload adres url SAS (lub stopniowo odtwarzania) hello plik MP4. Aby uzyskać więcej informacji o tym, jak toocreate lokalizatora SAS, zobacz [dostarczanie zawartości].

### <a id="sept_14_GA_changes"></a>Nowych funkcji/scenariuszy, które są częścią wersja Ogólnodostępna
* **Procesor multimediów indeksatora**. Aby uzyskać więcej informacji, zobacz [indeksowania plików multimedialnych na pliki z usługi Azure Media indeksatora].
* Witaj [StreamingEndpoint] jednostki obecnie umożliwia tooadd nazwy domen niestandardowych (hosta).
  
    Toobe nazwa domeny niestandardowej używany jako hello Media Services przesyłania strumieniowego Nazwa punktu końcowego należy tooyour nazwy hosta niestandardowego tooadd punktu końcowego przesyłania strumieniowego. Użyj hello interfejsów API REST usługi Media lub zestawu .NET SDK tooadd niestandardowych nazw hostów.
  
    Zastosuj Hello następujące zagadnienia:
  
  * Musi mieć prawa własności hello hello niestandardowej nazwy domeny.
  * własność Hello hello nazwa domeny musi zostać zweryfikowany przez usługi Azure Media Services. domeny hello toovalidate, utworzyć rekord CName, który mapuje <MediaServicesAccountId>.<parent domain> tooverifydns. < mediaservices-dns strefy >. 
  * Należy utworzyć inny CName, który mapuje nazwę hosta StreamingEndpont hello hosta niestandardowego nazwę (na przykład sports.contoso.com) tooyour Media Services (na przykład amstest.streaming.mediaservices.windows.net).

    Aby uzyskać więcej informacji, zobacz hello **CustomHostNames** właściwości w hello [StreamingEndpoint] tematu.

### <a id="sept_14_preview_changes"></a>Nowe funkcje/scenariusze, które są częścią hello publicznej wersji zapoznawczej
* Podgląd transmisji strumieniowej na żywo. Aby uzyskać więcej informacji, zobacz [Praca z usługi Azure Media Services transmisji strumieniowej na żywo].
* Usługa klucza dostawy. Aby uzyskać więcej informacji, zobacz [za pomocą dynamicznego szyfrowania AES-128 i klucz usługi dostarczania].
* Dynamicznego szyfrowania AES. Aby uzyskać więcej informacji, zobacz [za pomocą dynamicznego szyfrowania AES-128 i klucz usługi dostarczania].
* Usługi dostarczania licencji PlayReady. Aby uzyskać więcej informacji, zobacz [za pomocą szyfrowania dynamicznego PlayReady i usługi dostarczania licencji].
* Szyfrowanie PlayReady dynamicznie. Aby uzyskać więcej informacji, zobacz [za pomocą szyfrowania dynamicznego PlayReady i usługi dostarczania licencji].
* Szablon licencji PlayReady usługi multimediów. Aby uzyskać więcej informacji, zobacz [nośnika — omówienie szablon licencji PlayReady usług].
* Przesyłanie strumieniowe magazynu szyfrowane zasoby. Aby uzyskać więcej informacji, zobacz [zawartości szyfrowane przesyłania strumieniowego magazynu].

## <a id="august_changes_14"></a>W wersji 2014 r. sierpnia
Podczas kodowania zasób zawartości wyjściowej jest generowany po zakończeniu zadania kodowania hello. Do tej wersji usługi Azure Media Services Encoder wyprodukowanych metadanych o zasobach danych wyjściowych. Począwszy od tej wersji kodera hello również tworzy metadane dotyczące zasobów wejściowych. Aby uzyskać więcej informacji, zobacz hello [metadanych danych wejściowych] i [metadanych dane wyjściowe] tematów.

## <a id="july_changes_14"></a>Lipiec 2014 roku
Witaj następujące poprawki zostały wprowadzone dla hello Azure Media Services Pakowarka i modułu szyfrującego:

* Tylko dźwięk jest odtwarzany po transmisja strumieniowa na żywo transmultipleksing tooHTTP zasobów archiwum na żywo — problem został rozwiązany i teraz odtwarzania audio i wideo.
* Podczas tworzenia pakietu zasobów tooHTTP transmisji strumieniowej na żywo i AES 128-bitowego szyfrowania koperty, hello spakowane strumieni nie są odtwarzane na urządzeniach z systemem Android — ten problem został rozwiązany i strumienia spakowanych hello odtwarza na urządzeniach z systemem Android, które obsługują HTTP transmisji strumieniowej na żywo.

## <a id="may_changes_14"></a>Maja 2014 roku
### <a id="may_14_changes"></a>Usługi multimediów ogólne aktualizacji
Można teraz używać [dynamicznego tworzenia pakietów] toostream HTTP Live Streaming (HLS) w wersji 3. toostream HLS w wersji 3, Dodaj hello następującego formatu toohello pochodzenia lokalizatora ścieżki: * .ism/manifest(format=m3u8-aapl-v3). Aby uzyskać więcej informacji, zobacz [blogu Nick Drouin].

Dynamiczne tworzenie pakietów, teraz również obsługuje dostarczanie HLS (w wersji 3 i 4) szyfrowany za pomocą PlayReady oparte na Smooth Streaming statycznie zaszyfrowane za pomocą PlayReady. Aby uzyskać informacje na temat tooencrypt Smooth Streaming z PlayReady, zobacz [ochrona Smooth Stream przy użyciu usług PlayReady].

### <a name="may_14_donnet_changes"></a>Aktualizacje zestawu SDK .NET usługi Media Services
hello wersji SDK .NET usługi Media Services 3.0.0.5 obejmuje Hello następujące ulepszenia:

* Lepsze szybkość i odporności przekazywania/pobierania zasoby nośnika.
* Ulepszenia w obsłudze wyjątków logiki i przejściowy ponownych prób: 
  
  * Błąd przejściowy logikę wykrywania i ponów próbę udoskonalone wyjątków spowodowanych przez zapytanie, trwa zapisywanie zmian, przekazywanie lub pobieranie plików. 
  * Podczas pobierania wyjątki sieci Web (na przykład podczas żądania tokenu usługi ACS), zauważysz, że błędy krytyczne kończą się niepowodzeniem szybciej teraz.

Aby uzyskać więcej informacji, zobacz [ponów logikę hello SDK usługi Media Services dla platformy .NET].

## <a id="april_changes_14"></a>Wersja kodera kwietnia 2014 r.
### <a name="april_14_enocer_changes"></a>Koder aktualizacje usługi multimediów
* Dodano obsługę pobierania plików AVI utworzone za pomocą edytora rożne EDIUS doliny trawy hello, gdzie hello wideo jest lekkim skompresowane za pomocą kodera-dekodera doliny trawy HQ/HQX. Aby uzyskać więcej informacji, zobacz [hello trawy doliny ogłasza EDIUS 7 przesyłania strumieniowego za pośrednictwem chmury].
* Dodano obsługę Określanie hello konwencję nazewnictwa plików hello utworzonego przez hello Media Encoder. Aby uzyskać więcej informacji, zobacz [kontrolowanie Media Service kodera nazw plików wyjściowych].
* Dodano obsługę nakładki wideo lub audio. Aby uzyskać więcej informacji, zobacz [tworzenie nakładki].
* Dodano obsługę razem łączenia wielu segmentach wideo. Aby uzyskać więcej informacji, zobacz [łączenia segmentów wideo].
* Stałe związane z usterki tootranscoding MP4s, w którym został zakodowany hello audio MPEG-1 Audio warstwy 3 (alias MP3).

## <a id="jan_feb_changes_14"></a>Stycznia/lutego 2014 roku
### <a name="jan_fab_14_donnet_changes"></a>Zestaw .NET SDK 3.0.0.1, 3.0.0.2 i 3.0.0.3 usługi Azure Media Services
zmiany Hello w 3.0.0.1 i 3.0.0.2 obejmują:

* Rozwiązane problemy związane z toousage kwerend LINQ z instrukcji OrderBy.
* Podziel rozwiązań testu w [GitHub] do testów opartych na jednostki i oparta na scenariuszu.

Aby uzyskać więcej informacji o zmianach hello, zobacz: [zwalnia Azure .NET SDK usługi Media Services 3.0.0.1 i 3.0.0.2].

Witaj następujące zmiany wprowadzono w 3.0.0.3:

* Uaktualnionej wersji toouse zależności magazynu platformy Azure 3.0.3.0. 
* Rozwiązany problem zgodności z poprzednimi wersjami 3.0. *.* wersje. 

## <a id="december_changes_13"></a>Wersja grudniu 2013
### <a name="dec_13_donnet_changes"></a>Zestaw .NET SDK 3.0.0.0 usługi Azure Media Services
> [!NOTE]
> wersje 3.0.x.x nie są zgodne z wersjami 2.4.x.x.
> 
> 

najnowszą wersję Hello hello SDK usługi Media Services jest teraz 3.0.0.0. Można pobrać najnowszy pakiet hello Nuget lub uzyskać bitów hello z [GitHub].

Począwszy od zestawu SDK usługi Media Services w wersji 3.0.0.0 hello, można użyć ponownie hello [Azure Active Directory kontroli dostępu usługi (ACS)] tokenów. Aby uzyskać więcej informacji, zobacz hello "ponowne użycie kontroli usługi tokeny dostępu" części hello [połączenie usług tooMedia z hello SDK usługi Media Services dla platformy .NET] tematu.

### <a name="dec_13_donnet_ext_changes"></a>2.0.0.0 rozszerzenia zestawu .NET SDK usługi Azure Media Services
Witaj rozszerzenia SDK .NET usługi Azure Media Services to zestaw metod rozszerzeń i funkcji pomocniczych, które będą uprościć kod i stał się łatwiejsze toodevelop w usłudze Azure Media Services. Możesz uzyskać najnowsze bitów hello z [rozszerzenia SDK .NET usługi Azure Media Services].

## <a id="november_changes_13"></a>Wersja listopad 2013
### <a name="nov_13_donnet_changes"></a>Zmiany zestawu SDK .NET usługi Azure Media Services
Począwszy od tej wersji, hello SDK usługi Media Services dla platformy .NET obsługuje błędów przejściowych błędów, które mogą wystąpić podczas wprowadzania warstwy interfejsu API REST usług Media toohello wywołania.

## <a id="august_changes_13"></a>Wersja sierpnia 2013
### <a name="aug_13_powershell_changes"></a>Nośnik: usługi poleceń cmdlet programu PowerShell wchodzi w skład narzędzi zestawu Sdk platformy Azure
Hello następującego polecenia cmdlet programu PowerShell usługi multimediów są objęte [azure-sdk-tools].

* Get-AzureMediaServices 
  
    Na przykład `Get-AzureMediaServicesAccount`.
* New-AzureMediaServicesAccount 
  
    Na przykład `New-AzureMediaServicesAccount -Name “MediaAccountName” -Location “Region” -StorageAccountName “StorageAccountName”`.
* New-AzureMediaServicesKey 
  
    Na przykład `New-AzureMediaServicesKey -Name “MediaAccountName” -KeyType Secondary -Force`.
* Remove-AzureMediaServicesAccount 
  
    Na przykład `Remove-AzureMediaServicesAccount -Name “MediaAccountName” -Force`.

## <a id="june_changes_13"></a>Wersja czerwca 2013
### <a name="june_13_general_changes"></a>Zmiany usługi Azure Media Services
zmiany Hello wymienionych w tej sekcji są aktualizacje zawarte w powitalne zwalnia czerwca 2013 Media Services.

* Toolink możliwości magazynu wielu kont tooa konta usługi Media. 
  
    Konto magazynu
  
    Asset.StorageAccountName i Asset.StorageAccount
* Możliwość tooupdate Job.Priority. 
* Powiadomienia dotyczące jednostki i właściwości: 
  
    JobNotificationSubscription
  
    NotificationEndPoint
  
    Zadanie
* Asset.Uri 
* Locator.Name 

### <a name="june_13_dotnet_changes"></a>Zmiany usługi Azure .NET SDK usługi Media Services
Witaj następujące zmiany są uwzględniane w czerwca 2013 zwalnia SDK usługi Media Services. Witaj najnowsze SDK usługi Media Services jest dostępna w witrynie GitHub.

* Począwszy od wersji hello 2.3.0.0, hello SDK usługi Media Services obsługuje łączenia wielu tooa kont magazynu konta usługi Media Services. Witaj następujące interfejsy API obsługuje tę funkcję:
  
    Witaj IStorageAccount typu.
  
    Witaj Microsoft.WindowsAzure.MediaServices.Client.CloudMediaContext.StorageAccounts właściwości.
  
    Witaj właściwości konto magazynu.
  
    Witaj StorageAccountName właściwości.
  
    Aby uzyskać więcej informacji, zobacz [Zarządzanie zasoby usługi multimediów między wiele kont magazynu].
* Powiadomienie związane z interfejsów API. Począwszy od wersji hello 2.2.0.0 masz hello możliwości toolisten tooAzure kolejki magazynu powiadomienia. Aby uzyskać więcej informacji, zobacz [powiadomienia zadanie obsługi usług Media].
  
    Witaj Microsoft.WindowsAzure.MediaServices.Client.IJob.JobNotificationSubscriptions właściwości.
  
    Witaj Microsoft.WindowsAzure.MediaServices.Client.INotificationEndPoint typu.
  
    Witaj Microsoft.WindowsAzure.MediaServices.Client.IJobNotificationSubscription typu.
  
    Witaj Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointCollection typu.
  
    Witaj Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointType typu.
  
    Witaj Microsoft.WindowsAzure.MediaServices.Client.NotificationJobState typu.
* Zależność od hello Azure magazynu klienta SDK 2.0 (Microsoft.WindowsAzure.StorageClient.dll).
* Zależność od OData 5.5 (Microsoft.Data.OData.dll).

## <a id="december_changes_12"></a>Wersja grudnia 2012
### <a name="dec_12_dotnet_changes"></a>Zmiany usługi Azure .NET SDK usługi Media Services
* IntelliSense: Dodaje brakujące dokumentacji Intellisense dla wielu typów.
* Microsoft.Practices.TransientFaultHandling.Core: Rozwiązano problem, gdy hello SDK nadal miały zależności tooan stara wersja tego zestawu. Witaj teraz odwołuje się do wersji 5.1.1209.1 tego zestawu SDK.

Rozwiązuje problemy znalezione w hello listopad 2012 SDK:

* IAsset.Locators.Count: Ta liczba jest teraz prawidłowo raportowane na nowe interfejsy IAsset po usunięciu wszystkich lokalizatorów.
* IAssetFile.ContentFileSize: Ta wartość jest teraz prawidłowo ustawione po przesłaniu przez IAssetFile.Upload(filepath).
* IAssetFile.ContentFileSize: Ta właściwość teraz można ustawić podczas tworzenia pliku zasobów. Było wcześniej tylko do odczytu.
* IAssetFile.Upload(filepath): Rozwiązano problem, gdy ta metoda przekazywania synchronicznego zostało wyrzucanie hello następujący błąd podczas przekazywania wielu plików toohello zasobów. Witaj błąd "serwer nie powiodło się Żądanie hello tooauthenticate. Upewnij się, że hello wartość nagłówka autoryzacji jest sformatowany poprawnie tym podpisu hello. "
* IAssetFile.UploadAsync: Rozwiązano problem, w którym nie więcej niż 5 plików można przekazać jednocześnie.
* IAssetFile.UploadProgressChanged: To zdarzenie jest teraz udostępniany przez hello zestawu SDK.
* IAssetFile.DownloadAsync (ciąg, BlobTransferClient, ILocator, CancellationToken): przeciążenie tej metody jest teraz udostępniany.
* IAssetFile.DownloadAsync: Rozwiązano problem, w którym nie więcej niż 5 można pobrać plików jednocześnie.
* IAssetFile.Delete(): Rozwiązano problem, w którym wywoływania operacji delete może zgłosić wyjątek, jeśli nie przekazano pliku dla hello IAssetFile.
* Zadania: Rozwiązano problem gdzie łańcucha "MP4 tooSmooth strumieni zadania" z "Zadania ochrony PlayReady" przy użyciu szablonu zadania nie spowodować wszystkie zadania w ogóle.
* EncryptionUtils.GetCertificateFromStore(): Ta metoda nie jest już zgłasza wyjątek odwołania zerowego powodu niepowodzenia tooa znajdowanie hello certyfikatu opartego na problemy z konfiguracją certyfikatu.

## <a id="november_changes_12"></a>Wersja listopad 2012
Witaj zmiany wymienione w tej sekcji zostały aktualizacje zawarte w hello listopad 2012 (wersja 2.0.0.0) zestawu SDK. Te zmiany mogą wymagać żadnego kodu napisane dla hello czerwca 2012 w wersji zapoznawczej SDK wersji toobe modyfikacji lub napisany od nowa.

* Elementy zawartości
  
    IAsset.Create(assetName) jest hello tylko zasobów tworzenia funkcji. Nie jest już IAsset.Create operacji przekazywania plików jako część hello wywołania metody. Użyj IAssetFile do przekazywania.
  
    Metoda IAsset.Publish Hello i wartość wyliczenia AssetState.Publish hello zostały usunięte z hello usługi SDK. Kod korzystający z tą wartością musi być zapisany ponownie.
* FileInfo
  
    Ta klasa została usunięta i zastępuje IAssetFile.
  
    IAssetFiles
  
    IAssetFile zastępuje FileInfo i działa w różny sposób. toouse, Utwórz wystąpienie obiektu IAssetFiles hello, a następnie przekazywania pliku przy użyciu hello SDK usługi Media Services lub hello zestawu SDK usługi Magazyn Azure. mogą być używane po przeciążenia IAssetFile.Upload Hello:
  
  * IAssetFile.Upload(filePath): Synchroniczna metoda, która blokuje hello wątku i jest zalecane tylko w przypadku przekazywania jednego pliku.
  * IAssetFile.UploadAsync (filePath, blobTransferClient, lokalizatora, cancellationToken): metody asynchronicznej. Jest to mechanizm przekazywania hello preferowany. 
    
    Znaną usterką: przy użyciu hello cancellationToken rzeczywiście anulowanie operacji przekazywania hello; jednak hello stan anulowania zadań hello może być dowolną liczbę stanów. Należy poprawnie catch i obsługi wyjątków.
* Lokalizatory
  
    Hello wersji określonego źródła zostały usunięte. kontekst Hello specyficzne dla sygnatury dostępu Współdzielonego. Locators.CreateSasLocator (zasobów, accessPolicy) zostaną oznaczone jako przestarzałe lub usunięty przez po Zobacz lokalizatorów hello nowych funkcji w sekcji zaktualizowane zachowania.

## <a id="june_changes_12"></a>Wersja zapoznawcza czerwiec 2012
Nowość w wersji listopada hello hello SDK został Hello następujące funkcje.

* Usuwanie jednostek
  
    IAsset, IAssetFile, ILocator, IAccessPolicy, IContentKey obiekty są teraz usuwane na poziomie obiektu hello, tj. IObject.Delete() zamiast usuwania w kolekcji, która jest cloudMediaContext.ObjCollection.Delete(objInstance) hello.
* Lokalizatory
  
    Lokalizatory musi zostać utworzone przy użyciu metody CreateLocator hello i używać wartości wyliczenia LocatorType.SAS lub LocatorType.OnDemandOrigin hello jako argument dla określonego typu lokalizatora hello ma toocreate.
  
    TooLocators toomake zostały dodane nowe właściwości go łatwiejsze tooobtain można używać identyfikatorów URI dla zawartości. Zostało to one lokalizatorów przeznaczone tooprovide większą elastyczność przyszłych rozszerzeń innych firm co zwiększa łatwość użycia dla aplikacji klienckich.
* Obsługa metod asynchronicznych
  
    Dodano obsługę asynchronicznej metody tooall.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

<!-- Anchors. -->

<!-- Images. -->

<!--- URLs. --->
[Forum MSDN usług Media Azure]: http://social.msdn.microsoft.com/forums/azure/home?forum=MediaServices
[dokumentacja interfejsu API REST usługi Azure Media Services]: https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference
[szczegóły cennika usługi Media Services]: http://azure.microsoft.com/pricing/details/media-services/
[metadanych danych wejściowych]: http://msdn.microsoft.com/library/azure/dn783120.aspx
[metadanych dane wyjściowe]: http://msdn.microsoft.com/library/azure/dn783217.aspx
[dostarczanie zawartości]: http://msdn.microsoft.com/library/azure/hh973618.aspx
[indeksowania plików multimedialnych na pliki z usługi Azure Media indeksatora]: http://msdn.microsoft.com/library/azure/dn783455.aspx
[StreamingEndpoint]: http://msdn.microsoft.com/library/azure/dn783468.aspx
[Praca z usługi Azure Media Services transmisji strumieniowej na żywo]: http://msdn.microsoft.com/library/azure/dn783466.aspx
[za pomocą dynamicznego szyfrowania AES-128 i klucz usługi dostarczania]: http://msdn.microsoft.com/library/azure/dn783457.aspx
[za pomocą szyfrowania dynamicznego PlayReady i usługi dostarczania licencji]: http://msdn.microsoft.com/library/azure/dn783467.aspx
[Preview features]: http://azure.microsoft.com/services/preview/
[nośnika — omówienie szablon licencji PlayReady usług]: http://msdn.microsoft.com/library/azure/dn783459.aspx
[zawartości szyfrowane przesyłania strumieniowego magazynu]: http://msdn.microsoft.com/library/azure/dn783451.aspx
[Azure portal]: https://manage.windowsazure.com
[dynamicznego tworzenia pakietów]: http://msdn.microsoft.com/library/azure/jj889436.aspx
[blogu Nick Drouin]: http://blog-ndrouin.azurewebsites.net/hls-v3-new-old-thing/
[ochrona Smooth Stream przy użyciu usług PlayReady]: http://msdn.microsoft.com/library/azure/dn189154.aspx
[ponów logikę hello SDK usługi Media Services dla platformy .NET]: http://msdn.microsoft.com/library/azure/dn745650.aspx
[hello trawy doliny ogłasza EDIUS 7 przesyłania strumieniowego za pośrednictwem chmury]: http://www.streamingmedia.com/Producer/Articles/ReadArticle.aspx?ArticleID=96351&utm_source=dlvr.it&utm_medium=twitter
[kontrolowanie Media Service kodera nazw plików wyjściowych]: http://msdn.microsoft.com/library/azure/dn303341.aspx
[tworzenie nakładki]: http://msdn.microsoft.com/library/azure/dn640496.aspx
[łączenia segmentów wideo]: http://msdn.microsoft.com/library/azure/dn640504.aspx
[zwalnia Azure .NET SDK usługi Media Services 3.0.0.1 i 3.0.0.2]: http://www.gtrifonov.com/2014/02/07/windows-azure-media-services-.net-sdk-3.0.0.2-release/
[Azure Active Directory kontroli dostępu usługi (ACS)]: http://msdn.microsoft.com/library/hh147631.aspx
[połączenie usług tooMedia z hello SDK usługi Media Services dla platformy .NET]: http://msdn.microsoft.com/library/azure/jj129571.aspx
[rozszerzenia SDK .NET usługi Azure Media Services]: https://github.com/Azure/azure-sdk-for-media-services-extensions/tree/dev
[azure-sdk-tools]: https://github.com/Azure/azure-sdk-tools
[GitHub]: https://github.com/Azure/azure-sdk-for-media-services
[Zarządzanie zasoby usługi multimediów między wiele kont magazynu]: http://msdn.microsoft.com/library/azure/dn271889.aspx
[powiadomienia zadanie obsługi usług Media]: http://msdn.microsoft.com/library/azure/dn261241.aspx

