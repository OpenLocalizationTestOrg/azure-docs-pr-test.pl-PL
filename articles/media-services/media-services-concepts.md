---
title: "Pojęcia dotyczące usługi Media Services aaaAzure | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera omówienie koncepcji usługi multimediów Azure"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: dcefc8bc-e2ea-4b38-a643-9010f4436fb5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: juliako
ms.openlocfilehash: 0a45deff32336dfcf778552f720c1ea21927951b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-concepts"></a>Azure Media Services pojęcia
Ten temat zawiera omówienie hello najważniejsze pojęcia usługi Media Services.

## <a id="assets"></a>Zasoby i magazynu
### <a name="assets"></a>Elementy zawartości
[Zasobów](https://docs.microsoft.com/rest/api/media/operations/asset) zawiera (w tym wideo, audio, obrazy, kolekcje miniatur, ścieżek tekstu i pliki napisów) pliki cyfrowe i hello metadane dotyczące tych plików. Po hello pliki cyfrowe są przekazywane do elementu zawartości, mogą być używane w hello Media Services kodowania i przesyłania strumieniowego przepływów pracy.

Zasób jest mapowanych tooa kontenera obiektów blob na koncie magazynu Azure hello i pliki hello w hello zasobów są przechowywane jako blokowych obiektów blob w tym kontenerze. Stronicowe obiekty BLOB nie są obsługiwane przez usługi Azure Media Services.

Podczas podejmowania decyzji o jakie tooupload zawartości nośnika i magazynu w zasób, zastosuj hello następujące zagadnienia:

* Zasób powinien zawierać tylko jedną, unikatową wystąpienie zawartości nośnika. Na przykład pojedynczy edycji epizodu TV, filmów lub anonsu.
* Zasób nie może zawierać wielu wersji lub edycji pliku audiowizualnych. Przykładem niepoprawne użycie trwałego czy próba toostore więcej niż jeden odcinek TV, anonsu lub różnych kątów kamery z jednym produkcji wewnątrz elementu zawartości. Przechowywanie wielu wersji lub edycji pliku audiowizualnych w zasób może spowodować problemy podczas przesyłania zadania kodowania, przesyłanie strumieniowe i zabezpieczania hello dostarczania zasobów hello później w przepływie pracy hello.  

### <a name="asset-file"></a>Plik zasobów
[AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) reprezentuje rzeczywisty plik wideo lub audio, który jest przechowywany w kontenerze obiektów blob. Plik zasobów zawsze jest skojarzony z zasobem i zasobów może zawierać jeden lub wiele plików. Witaj Media Encoder usług zadanie nie powiedzie się, jeśli obiekt pliku zasobu nie jest skojarzony z pliku cyfrowego w kontenerze obiektów blob.

Witaj **AssetFile** wystąpienia oraz plik multimedialna hello są dwa różne obiekty. wystąpienia AssetFile Hello zawiera metadane dotyczące plików multimedialnych hello, a plik multimedialny hello zawiera zawartość multimedialna hello.

Zawartość hello toochange kontenerów obiektów blob, które zostały wygenerowane przez usługę Media Services bez korzystania z interfejsów API usługi Media nie powinny podejmować.

### <a name="asset-encryption-options"></a>Opcje szyfrowania zasobów
W zależności od typu hello zawartości ma tooupload, magazynu i osiągnąć, usługa Media Services udostępnia różne opcje szyfrowania, które są dostępne.

>[!NOTE]
>Szyfrowanie nie jest stosowane. Jest to wartość domyślna hello. Korzystając z tej opcji zawartość nie jest chroniona w trakcie przesyłania lub przechowywania w magazynie.

Jeśli planujesz toodeliver MP4 przy użyciu pobierania progresywnego, użyj tej opcji tooupload zawartości.

**StorageEncrypted** — Użyj tej opcji tooencrypt zawartości lokalnie za pomocą szyfrowania AES 256-bitową, a następnie przekaż tooAzure magazynu, w którym są przechowywane szyfrowane, gdy. Elementy zawartości chronione przy użyciu szyfrowania magazynu są automatycznie bez szyfrowania i umieszczana w poprzednich tooencoding systemu szyfrowania plików i opcjonalnie ponownie szyfrowane przed toouploading zwrotnym w formie nowego elementu zawartości wyjściowej. Witaj pierwotnym zastosowaniem szyfrowania magazynu jest toosecure Twojego wysokiej jakości multimedialnych plików wejściowych pomocą silnego szyfrowania rest na dysku. 

W kolejności toodeliver zasób zaszyfrowanych magazynu należy skonfigurować zasady dostarczania zasobów hello będzie wówczas traktował Media Services sposób toodeliver zawartości. Aby mogła być przesłana strumieniowo zawartości, hello i przesyłania strumieniowego szyfrowania magazynu hello usuwa strumieni zawartości przy użyciu hello określone zasady dostarczania (na przykład AES, PlayReady lub bez szyfrowania). 

**CommonEncryptionProtected** — Użyj tej opcji, jeśli chcesz tooencrypt (lub przekazywania już zaszyfrowany) zawartości ze wspólnego szyfrowania lub technologii PlayReady DRM (na przykład, Smooth Streaming chronione za pomocą technologii PlayReady DRM).

**EnvelopeEncryptionProtected** — Użyj tej opcji, jeśli chcesz tooprotect (lub przekazywania już chroniony) HTTP Live Streaming (HLS) szyfrowane z szyfrowania AES (Advanced Standard). Podczas przekazywania HLS już zaszyfrowany z użyciem standardu AES go musi mieć został zaszyfrowany za Transform Manager.

### <a name="access-policy"></a>Zasady dostępu
[AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy) definiuje uprawnienia (na przykład odczytu, zapisu i listy) i czas trwania dostępu tooan zasobów. Zazwyczaj użytkownik przejdzie lokalizatora tooa AccessPolicy obiektu, który będzie wówczas używane tooaccess hello plików znajdujących się w zasób.

>[!NOTE]
>Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy). Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / dostęp uprawnień, na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (zasady — przekazywanie). Aby uzyskać więcej informacji, zobacz [ten](media-services-dotnet-manage-entities.md#limit-access-policies) temat.

### <a name="blob-container"></a>Kontener obiektów blob
Kontener obiektów blob zawiera grupowanie zestawu obiektów blob. Kontenerów obiektów blob są używane w usłudze Media Services jako granic punktu kontroli dostępu i lokalizatorów dostępu sygnatury dostępu Współdzielonego na zasoby. Konto magazynu Azure może zawierać nieograniczoną liczbę kontenerów obiektów blob. Kontener może przechowywać nieograniczoną liczbę obiektów blob.

>[!NOTE]
> Zawartość hello toochange kontenerów obiektów blob, które zostały wygenerowane przez usługę Media Services bez korzystania z interfejsów API usługi Media nie powinny podejmować.
> 
> 

### <a id="locators"></a>Lokalizatory
[Lokalizator](https://docs.microsoft.com/rest/api/media/operations/locator)s Podaj hello tooaccess punktu wejścia plików znajdujących się w zasób. Zasady dostępu jest używana toodefine hello uprawnienia i czas trwania, że klient ma tooa dostęp do danego zasobu. Lokalizatory może mieć wiele relacji tooone przy użyciu zasad dostępu, takie różnych lokalizatory zapewniają godziny rozpoczęcia różne, a klienci toodifferent typów połączeń, podczas gdy przy użyciu wszystkich hello uprawnienie i ustawienia czasu trwania; Jednak ze względu na ograniczenia zasad dostępu współdzielonego ustawione przez usług magazynu platformy Azure, nie może mieć więcej niż pięć lokalizatorów unikatowy skojarzone z danym zawartości w tym samym czasie. 

Usługa Media Services obsługuje dwa typy lokalizatorów: lokalizatory OnDemandOrigin używane toostream nośnika (na przykład MPEG DASH, HLS lub Smooth Streaming) lub pobrać progresywnie nośników i Locator adres URL SAS, tooupload używane lub pobierania nośnika pliki to\from magazynu Azure. 

>[!NOTE]
>Tworząc Lokalizator OnDemandOrigin nie można używać Hello listy uprawnień (AccessPermissions.List). 

### <a name="storage-account"></a>Konto magazynu
Wszystkie tooAzure dostępu do magazynu odbywa się za pomocą konta magazynu. Konto usługi Media można skojarzyć z co najmniej jedno konto magazynu. Konto może zawierać nieograniczoną liczbę kontenerów, dopóki ich łączny rozmiar jest w obszarze 500TB na konto magazynu.  Usługa Media Services udostępnia narzędzia tooallow poziomu zestawu SDK możesz toomanage wielu kont magazynu i obciążenia saldo dystrybucji hello elementów zawartości podczas przekazywania toothese konta na podstawie metryk lub losowych dystrybucji. Aby uzyskać więcej informacji, zapoznaj się z praca [usługi Azure Storage](https://msdn.microsoft.com/library/azure/dn767951.aspx). 

## <a name="jobs-and-tasks"></a>Zadań i zadań
A [zadania](https://https://docs.microsoft.com/rest/api/media/operations/job) jest zwykle używana tooprocess (na przykład indeksu lub zakodować) prezentacji audio i wideo. W przypadku przetwarzania wiele plików wideo, należy utworzyć zadania dla każdego toobe wideo zakodowany.

Zadanie zawiera metadane dotyczące przetwarzania hello toobe wykonywane. Każde zadanie zawiera co najmniej jeden [zadań](https://docs.microsoft.com/rest/api/media/operations/task), które Określ zadanie przetwarzania atomic, jego zasobów wejściowych, wyjściowych zasoby, procesor multimediów i jej powiązane ustawienia. Zadania w ramach danego zadania można połączyć ze sobą, gdzie zawartości wyjściowej hello jednego zadania jest podawana jako hello danych wejściowych zasobu toohello następnego zadania. W ten sposób jedno zadanie może zawierać wszystkie niezbędne do przedstawienia nośnika przetwarzania hello.

## <a id="encoding"></a>Kodowanie
Azure Media Services udostępnia wiele opcji hello kodowania nośnika w chmurze hello.

Podczas uruchamiania z programem Media Services, jest ważne toounderstand hello różnica między koderów-dekoderów i plik formatu.
Kodery-dekodery hello oprogramowania, które implementuje algorytmy kompresji i dekompresji hello formatów plików są kontenery zawierających hello skompresowane wideo.

Usługa Media Services udostępnia funkcję dynamicznego tworzenia pakietów, co pozwala toodeliver Twojego o adaptacyjnej szybkości bitowej MP4 lub Smooth Streaming zakodowane zawartości w formatach transmisji strumieniowej obsługiwanych przez usługę Media Services (MPEG DASH, HLS, Smooth Streaming) bez konieczności toore pakietów w tych formatach transmisji strumieniowej.

Zaletą tootake [dynamicznego tworzenia pakietów](media-services-dynamic-packaging-overview.md), należy tooencode (źródłowy) mezzanine do zestawu plików MP4 lub Smooth Streaming plików i ma co najmniej jeden standardowy lub premium przesyłania strumieniowego punktu końcowego w stanie uruchomionym.

Usługa Media Services obsługuje następujące kodery na żądanie, które zostały opisane w tym artykule hello:

* [Usługa Media Encoder Standard](media-services-encode-asset.md#media-encoder-standard)
* [Przepływ pracy usługi Media Encoder w warstwie Premium](media-services-encode-asset.md#media-encoder-premium-workflow)

Informacje o obsługiwanych koderów znajdują się w temacie [koderów](media-services-encode-asset.md).

## <a name="live-streaming"></a>Przesyłanie strumieniowe na żywo
W usłudze Azure Media Services kanał reprezentuje potok przetwarzania zawartości transmisji strumieniowej na żywo. Kanał otrzymuje na żywo wejściowych strumieni w jeden z dwóch sposobów:

* Na lokalny koder na żywo wysyła wielokrotnej szybkości transmisji bitów RTMP lub Smooth Streaming (pofragmentowany MP4) toohello kanału. Można użyć następujących koderów na żywo, które udostępniają wielokrotnej szybkości transmisji bitów Smooth Streaming hello: MediaExcel, Ateme, Wyobraź sobie komunikacji, Envivio, Cisco i Elemental. Witaj następujące kodery na żywo wysyłają pliki RTMP: Adobe Flash kodera na żywo, Telestream Wirecast, Teradek, Haivision i Tricaster koderów. Witaj pozyskiwane strumienie są przekazywane za pośrednictwem kanałów bez żadnych późniejszych transkodowanie i kodowania. Gdy żądanie, Media Services oferuje hello toocustomers strumienia.
* Strumień o pojedynczej szybkości transmisji bitów (w jednym z następujących formatów hello: RTP (MPEG-TS)), protokołu RTMP lub Smooth Streaming (pofragmentowany MP4)) są wysyłane toohello kanału, który jest włączone tooperform live encoding w usłudze Media Services. Witaj kanał wykonuje następnie kodowanie na żywo przychodzącego hello pojedynczej szybkości transmisji bitów strumienia tooa wielokrotnej szybkości transmisji bitów (adaptacyjnej) strumienia wideo. Gdy żądanie, Media Services oferuje hello toocustomers strumienia.

### <a name="channel"></a>Kanał
W usłudze Media Services [kanału](https://docs.microsoft.com/rest/api/media/operations/channel)s są zobowiązani do przetwarzania zawartości transmisji strumieniowej na żywo. Kanał zawiera ono wejściowy punkt końcowy (adres URL pozyskiwania) następnie podaj tooa transcoder na żywo. kanał Hello odbiera strumienie na żywo wejściowe z hello transcoder na żywo i udostępnia go do przesyłania strumieniowego za pośrednictwem jednego lub więcej punkty końcowe. Kanały udostępniają punktu końcowego podglądu (adres URL w wersji zapoznawczej) Użyj toopreview, a następnie sprawdź strumienia, zanim dalszego przetwarzania i dostarczania.

Możesz uzyskać hello pozyskiwania adresu URL i adresu URL w wersji zapoznawczej hello podczas tworzenia kanału hello. tooget tych adresów URL kanału hello nie ma toobe w stanie hello uruchomiona. Gdy wszystko jest gotowe toostart przekazywanie danych z transcoder na żywo do kanału hello, hello kanału musi być uruchomiona. Po uruchomieniu hello na żywo transcoder wprowadzania danych można wyświetlić podgląd strumienia.

Każde konto usługi Media Services może zawierać wiele kanałów, wiele programów i wielu punkty końcowe. W zależności od potrzeb przepustowości i zabezpieczeń hello StreamingEndpoint usługi może być dedykowany tooone lub więcej kanałów. Wszelkie StreamingEndpoint można ściąganie danych z dowolnego kanału.

### <a name="program-event"></a>Program (zdarzenie)
A [programu (zdarzenie)](https://docs.microsoft.com/rest/api/media/operations/program) pozwala toocontrol hello publikowania i przechowywania segmentów strumienia na żywo. Kanały zarządzają programami (zdarzeń). Witaj relacja kanału i programu jest podobne nośnika tootraditional, gdzie kanał ma stały strumień zawartości, a program zdarzeń zakresie toosome upłynął, w tym kanale.
Można określić hello liczbę godzin zawartości hello rejestrowane tooretain hello programu przez ustawienie hello **ArchiveWindowLength** właściwości. Tę wartość można ustawić z co najmniej 5 minut tooa maksymalnie 25 godzin.

ArchiveWindowLength decyduje również hello maksymalną ilość czasu, klienci mogą zwrócić wstecz od bieżącego położenia na żywo hello. Programy mogą być transmitowane hello określoną ilość czasu, ale zawartość, która wykracza poza długość okna hello jest stale odrzucana. Ta wartość tej właściwości określa również, jak długo klient hello mogą być manifesty.

Każdy program (zdarzenie) jest skojarzony z zasobem. program hello toopublish należy utworzyć Lokalizator dla hello skojarzonych zasobów. Lokalizator umożliwi toobuild adresu URL przesyłania strumieniowego, która może zapewnić tooyour klientów.

Kanał obsługuje toothree jednocześnie uruchomione programy, dzięki czemu można tworzyć wiele archiwów hello samego strumienia przychodzącego. Dzięki temu toopublish i archiwum różnych części wydarzenia zgodnie z potrzebami. Na przykład konkretnym wymaganiom biznesowym jest tooarchive sześciu godzin programu, ale toobroadcast ostatnich 10 minut. tooaccomplish, należy toocreate dwa jednocześnie uruchomione programy. Jeden program ustawiono tooarchive sześciu godzin zdarzenia hello, ale hello program nie został opublikowany. Hello inny program jest zestaw tooarchive przez 10 minut i ten program zostanie opublikowany.

Aby uzyskać więcej informacji, zobacz:

* [Praca z kanałami, że włączono tooPerform Live kodowania za pomocą usługi Azure Media Services](media-services-manage-live-encoder-enabled-channels.md)
* [Praca z kanałami odbierającymi strumień na żywo o różnych szybkościach transmisji bitów z koderów lokalnych](media-services-live-streaming-with-onprem-encoders.md)
* [Przydziały i ograniczenia](media-services-quotas-and-limitations.md).

## <a name="protecting-content"></a>Ochrona zawartości
### <a name="dynamic-encryption"></a>Szyfrowania dynamicznego
Usługa Azure Media Services umożliwia toosecure możesz z hello razem, gdy opuszczą komputera za pośrednictwem przechowywania, przetwarzania i dostarczania multimediów. Usługa Media Services umożliwia toodeliver zawartości dynamicznie szyfrowany za pomocą Standard AES (Advanced Encryption) (przy użyciu kluczy szyfrowania 128-bitowe) i szyfrowania common encryption (CENC) za pomocą PlayReady i Widevine DRM. Usługi Media Services udostępnia usługę dostarczania kluczy AES i klientów tooauthorized licencji PlayReady.

Obecnie można zaszyfrować hello następujących formatów przesyłania strumieniowego: HLS, MPEG DASH i Smooth Streaming. Nie można zaszyfrować pobierania progresywnego.

Jeśli chcesz dla usługi Media Services tooencrypt zasób, należy tooassociate klucza szyfrowania (CommonEncryption lub EnvelopeEncryption) z zawartości i również skonfigurować zasady autoryzacji klucza hello.

Chcąc toostream zasób zaszyfrowanych magazynu, należy skonfigurować zasady dostarczania zasobów hello w kolejności toospecify sposób toodeliver zawartości.

Gdy odtwarzacza zażąda strumienia, usługa Media Services używa hello określony toodynamically klucza szyfrowania zawartości przy użyciu koperty (z użyciem standardu AES) lub szyfrowania wspólnych (za pomocą PlayReady lub Widevine). toodecrypt hello strumienia, hello odtwarzacza zażąda hello klucza z usługi dostarczania klucza hello. toodecide czy hello użytkownik jest autoryzowany tooget hello klucza, usługi hello ocenia zasady autoryzacji hello określonych hello klucza.

### <a name="token-restriction"></a>Ograniczenia tokenu
Witaj zasady autoryzacji klucza zawartości może mieć jeden lub więcej ograniczeń: Otwórz, token ograniczenia lub ograniczenia adresów IP. Witaj zasadzie ograniczenia tokenu musi towarzyszyć token wystawiony przez Secure Token Service (STS). Usługa Media Services obsługuje tokenów w i hello proste tokenów sieci Web (SWT) format tokenu Web JSON (JWT). Usługi Media Services nie zapewnia bezpieczny tokenu usługi. Można utworzyć niestandardowy STS lub korzystać z usługi Microsoft Azure ACS tooissue tokenów. Witaj STS musi być skonfigurowany toocreate podpisany token hello określony klucz i wystawianie oświadczeń, określonych w konfiguracji ograniczenia tokenu hello. Hello Media Services, który zwróci usługi dostarczania klucza żądanej powitania klienta toohello (licencji lub klucza) Jeśli hello token jest prawidłowy i hello oświadczenia w hello token dopasowania tych skonfigurowane dla hello (licencji lub klucza).

Podczas konfigurowania hello zasadzie ograniczenia tokenu, należy określić klucz podstawowy weryfikacji hello, wystawcy i parametry odbiorców. klucz podstawowy weryfikacji Hello zawiera hello klucza, że hello token została podpisana z, wystawcy hello bezpiecznego tokenu usługi, która wystawia hello token. odbiorców Hello (nazywane również zakres) opisano hello celem hello token lub hello zasobów hello tokenu zezwala na dostęp do. Hello usługa Media Services klucza dostawy weryfikuje, czy te wartości w tokenie hello są takie same wartości hello hello szablonu.

Aby uzyskać więcej informacji zobacz następujące artykuły hello:

[Ochrona zawartości omówienie](media-services-content-protection-overview.md)
[Chroń za pomocą AES-128](media-services-protect-with-aes128.md)
[Chroń za pomocą DRM](media-services-protect-with-drm.md)

## <a name="delivering"></a>Dostarczanie
### <a id="dynamic_packaging"></a>Funkcję dynamicznego tworzenia pakietów
Podczas pracy z usługi Media Services, zalecane jest tooencode plików mezzanine do adaptacyjnej szybkości bitowej MP4 ustawiona, a następnie wykonać konwersję hello pożądany format toohello przy użyciu hello [dynamicznego tworzenia pakietów](media-services-dynamic-packaging-overview.md).

### <a name="streaming-endpoint"></a>Punkt końcowy przesyłania strumieniowego
StreamingEndpoint reprezentuje przesyłania strumieniowego usługa, która zapewnia zawartości bezpośrednio tooa aplikacja odtwarzacza klienta lub tooa Content Delivery Network (CDN) w celu dalszej dystrybucji (Azure Media Services udostępnia teraz hello Azure CDN integracji.) hello strumienia wychodzącego z usługą punktu końcowego przesyłania strumieniowego może być strumień na żywo lub element zawartości wideo na żądanie w ramach konta usługi Media Services. Wybierz klientów usługi Media Services **standardowe** przesyłania strumieniowego punktu końcowego, jeden lub więcej **Premium** punkty końcowe, zgodnie z potrzebami tootheir przesyłania strumieniowego. Standardowego punktu końcowego przesyłania strumieniowego jest odpowiednia dla większości obciążeń przesyłania strumieniowego. 

Standardowy punkt końcowy przesyłania strumieniowego jest odpowiedni dla większości obciążeń przesyłania strumieniowego. Standardowe punkty końcowe przesyłania strumieniowego oferują hello elastyczność toodeliver Twojego toovirtually zawartości każdego urządzenia za pomocą dynamicznego tworzenia pakietów w HLS i MPEG-DASH, Smooth Streaming, a także szyfrowania dynamicznego Microsoft PlayReady, Google Widevine Fairplay firmy Apple , a AES128.  One również skalować z bardzo małych toovery dużych grup odbiorców tysiące równoczesnych podglądy dzięki integracji usługi Azure CDN. Jeśli masz zaawansowane obciążenia lub przesyłania strumieniowego wymagania dotyczące pojemności nie mieszczą się toostandard przesyłania strumieniowego punktu końcowego przepływności docelowych lub mają pojemność hello toocontrol musi hello StreamingEndpoint usługi toohandle rosnącym przepustowości, zaleca się jednostki skalowania tooallocate (znanej także jako premium jednostki przesyłania strumieniowego).

Zaleca się toouse dynamicznego tworzenia pakietów i/lub szyfrowania dynamicznego.

>[!NOTE]
>Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu. 

Aby uzyskać więcej informacji, zobacz [ten](media-services-portal-manage-streaming-endpoints.md) temat.

Domyślnie może zawierać maksymalnie too2 punktów końcowych przesyłania strumieniowego na koncie usługi Media Services. Zobacz toorequest wyższy limit [przydziały i ograniczenia](media-services-quotas-and-limitations.md).

Rozliczenie jest przeprowadzane tylko gdy Twoje StreamingEndpoint jest w stanie uruchomienia.

### <a name="asset-delivery-policy"></a>Zasady dostarczania elementu zawartości
Jeden z hello kroków w hello dostarczania zawartości w przepływie pracy jest skonfigurowanie usługi Media Services [zasady dostarczania zasobów ](https://docs.microsoft.com/rest/api/media/operations/assetdeliverypolicy), które mają toobe strumieniowo. zasady dostarczania elementu zawartości Hello informuje usługi Media Services sposób dla Twojego toobe zasobów dostarczyć: w przypadku protokołu przesyłania strumieniowego powinno zawartości dynamicznie umieszczone (na przykład, MPEG DASH, HLS, Smooth Streaming lub wszystkie), czy chcesz toodynamically szyfrowanie zawartości i w jaki sposób (koperty lub szyfrowania common encryption).

Jeśli masz magazynu trwałego zaszyfrowane, aby mogła być przesłana strumieniowo zawartości, hello i przesyłania strumieniowego szyfrowania magazynu hello usuwa strumieni zawartości przy użyciu hello określone zasady dostarczania. Na przykład toodeliver zawartości zaszyfrowanych za pomocą klucza szyfrowania zestaw hello zasad typu tooDynamicEnvelopeEncryption Advanced Encryption (Standard AES). tooremove szyfrowanie magazynu i zasobów hello strumienia w hello Wyczyść, należy ustawić hello zasad typu tooNoDynamicEncryption.

### <a name="progressive-download"></a>Pobierania progresywnego
Pobierania progresywnego umożliwia toostart odtwarzania multimediów przed hello cały plik został pobrany. Można tylko wczytać pliku MP4.

>[!NOTE]
>Musi odszyfrowania zaszyfrowanych zasoby, w razie potrzeby dla nich toobe dostępne dla pobierania progresywnego.

adresy URL pobierania tooprovide użytkownikom progresywnego, należy najpierw utworzyć Lokalizator OnDemandOrigin. Tworzenie lokalizatora hello, zapewnia hello podstawowa ścieżka toohello zasobów. Następnie należy tooappend hello nazwę pliku MP4. Na przykład:

http://amstest1.Streaming.mediaservices.Windows.NET/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

### <a name="streaming-urls"></a>Adresy URL przesyłania strumieniowego
Przesyłanie strumieniowe z tooclients zawartości. tooprovide użytkowników z adresami URL przesyłania strumieniowego, najpierw należy utworzyć Lokalizator OnDemandOrigin. Tworzenie lokalizatora hello, zapewnia hello podstawowej zasobów toohello ścieżka zawiera zawartość hello ma toostream. Jednak toobe stanie toostream ta zawartość należy toomodify dalsze tej ścieżki. tooconstruct pełne toohello adres URL przesyłania strumieniowego pliku manifestu, musi łączyć hello lokalizatora ścieżki wartość i hello (filename.ism) Nazwa pliku manifestu. Następnie dołącz /Manifest i odpowiedni format (w razie potrzeby) toohello lokalizatora ścieżki.

Można również strumienia zawartości za pośrednictwem połączenia SSL. toodo, upewnij się, że uruchamiania adresy URL przesyłania strumieniowego z protokołu HTTPS. Obecnie usługa AMS nie obsługuje protokołu SSL z domen niestandardowych.  

>[!NOTE]
>Można tylko strumienia za pośrednictwem protokołu SSL Jeśli hello, z którego dostarczać zawartość z punktu końcowego przesyłania strumieniowego został utworzony po 10 września 2014 r. Jeśli Twoje adresy URL przesyłania strumieniowego są oparte na powitania utworzone po 10 września punkty końcowe przesyłania strumieniowego, hello adres URL zawiera "streaming.mediaservices.windows.net" (nowy format hello). Adresy URL przesyłania strumieniowego zawierające "origin.mediaservices.windows.net" (stary format hello) nie obsługują protokołu SSL. Jeśli adres URL jest w starym formacie hello i chcesz toobe toostream mogli za pośrednictwem protokołu SSL, należy utworzyć nowy punkt końcowy przesyłania strumieniowego. Użyj adresów URL tworzone w oparciu hello nowych przesyłania strumieniowego punktu końcowego toostream zawartości za pośrednictwem protokołu SSL.

następujące listy Hello opisano różnych formatach przesyłania strumieniowego i zawiera przykłady:

* Smooth Streaming

{nazwa punktu końcowego przesyłania strumieniowego-nazwa konta usługi Media Services}.streaming.mediaservices.windows.net/{identyfikator lokalizatora}/{nazwa pliku}.ism/Manifest

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest

* MPEG DASH

{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=mpd-time-csf) przesyłania strumieniowego

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest(format=mpd-Time-CSF)

* Apple HTTP Live przesyłania strumieniowego V4 (HLS)

{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=m3u8-aapl) przesyłania strumieniowego

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest(format=m3u8-aapl)

* Apple HTTP Live przesyłania strumieniowego V3 (HLS)

{name}.streaming.mediaservices.windows.net/{locator konta usługi media Nazwa punktu końcowego ID}/{filename}.ism/Manifest(format=m3u8-aapl-v3) przesyłania strumieniowego

http://testendpoint-testaccount.Streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest(format=m3u8-aapl-v3)

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

