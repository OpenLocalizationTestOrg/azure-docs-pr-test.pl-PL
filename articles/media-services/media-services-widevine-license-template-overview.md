---
title: "Omówienie szablon licencji aaaWidevine | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera omówienie używany licencji Widevine tooconfigure szablonu licencji Widevine."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0e6f1f05-7ed6-4ed6-82a0-0cc2182b075a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 67a6ae38cf3d3c21e1b7282aef15f79b21776414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="widevine-license-template-overview"></a>Omówienie szablonu licencji Widevine
## <a name="overview"></a>Omówienie
Usługa Azure Media Services umożliwia teraz tooconfigure i żądania licencji Widevine. Gdy hello player użytkownik końcowy podejmie próbę tooplay zawartość chroniona Widevine, żądanie jest wysłane toohello licencji dostarczania usługi tooobtain licencji. Jeśli usługa licencji hello zatwierdza Żądanie hello, wystawia licencję hello, która jest wysłane toohello klienta i mogą być używane toodecrypt i play hello określonej zawartości.

Żądania licencji Widevine jest w formacie JSON wiadomości.  

>[!NOTE]
> Możesz wybrać toocreate pusty komunikat z nie wartości po prostu "{}" i zostanie utworzony szablon licencji z wszystkimi wartościami domyślnymi. domyślne Hello działa w większości przypadków. Na przykład w MS na podstawie licencji dostarczania scenariusze, które powinny być zawsze domyślnie. Jeśli potrzebujesz hello tooset "dostawca" i "content_id" wartości dostawcy muszą pasować do poświadczeń Widevine firmy Google.

    {  
       “payload”:“<license challenge>”,
       “content_id”: “<content id>” 
       “provider”: ”<provider>”
       “allowed_track_types”:“<types>”,
       “content_key_specs”:[  
          {  
             “track_type”:“<track type 1>”
          },
          {  
             “track_type”:“<track type 2>”
          },
          …
       ],
       “policy_overrides”:{  
          “can_play”:<can play>,
          “can persist”:<can persist>,
          “can_renew”:<can renew>,
          “rental_duration_seconds”:<rental duration>,
          “playback_duration_seconds”:<playback duration>,
          “license_duration_seconds”:<license duration>,
          “renewal_recovery_duration_seconds”:<renewal recovery duration>,
          “renewal_server_url”:”<renewal server url>”,
          “renewal_delay_seconds”:<renewal delay>,
          “renewal_retry_interval_seconds”:<renewal retry interval>,
          “renew_with_usage”:<renew with usage>
       }
    }

## <a name="json-message"></a>Komunikat JSON
| Nazwa | Wartość | Opis |
| --- | --- | --- |
| ładunek |Ciąg kodowany jako Base64 |żądanie licencji Hello wysłane przez klienta. |
| content_id |Ciąg kodowany jako Base64 |Identyfikator używany do każdego content_key_specs.track_type tooderive KeyId(s) oraz kluczy zawartości. |
| Dostawcy |Ciąg |Używane toolook się zasad i zawartości kluczy. Jeśli MS klucza dostawy jest używane w celu dostarczania licencji Widevine, ten parametr zostanie zignorowany. |
| nazwa_zasady |Ciąg |Nazwa zasady wcześniej zarejestrowane. Optional (Opcjonalność) |
| allowed_track_types |wyliczenia |SD_ONLY lub SD_HD. Formanty, które zawartości kluczy powinien być uwzględniany w licencji |
| content_key_specs |Tablica JSON struktur, zobacz **specyfikacji klucz zawartości** poniżej |Skuteczniejszą kontrolę na tooreturn kluczy zawartości. Aby uzyskać więcej informacji, zobacz zawartości specyfikacja klucza poniżej.  Można określić tylko jeden allowed_track_types i content_key_specs. |
| use_policy_overrides_exclusively |Wartość logiczna. wartość PRAWDA lub FAŁSZ |Użyj zasad atrybuty określone w policy_overrides i pominąć wszystkie zapisane wcześniej zasady. |
| policy_overrides |Struktura JSON, zobacz **zasady zastępują** poniżej |Ustawienia zasad dla tej licencji.  W przypadku hello ten zasób ma wstępnie zdefiniowane zasady, te określonej wartości będą używane. |
| session_init |Struktura JSON, zobacz **inicjowania sesji** poniżej |Opcjonalne dane przekazywane toolicense. |
| parse_only |Wartość logiczna. wartość PRAWDA lub FAŁSZ |żądanie licencji Hello jest analizowana, ale żadna licencja jest wystawiony. Jednak wartości formularza hello licencji żądania jest zwracany w odpowiedzi hello. |

## <a name="content-key-specs"></a>Dane techniczne klucz zawartości
Jeśli istnieje już istniejących zasad, nie ma żadnych toospecify potrzeby żadnego hello wartości w hello specyfikacja klucza zawartości.  Witaj wstępnie istniejące zasady skojarzone z tą zawartością będzie toodetermine używane hello dane wyjściowe ochrony, takie jak HDCP i CGMS.  Jeśli wcześniej istniejących zasad nie jest zarejestrowany w powitania serwera licencji Widevine, hello dostawcy zawartości można wstrzyknąć hello wartości do hello żądanie licencji.   

Każdy content_key_specs należy określić dla wszystkich ścieżek, niezależnie od hello use_policy_overrides_exclusively opcji. 

| Nazwa | Wartość | Opis |
| --- | --- | --- |
| content_key_specs. track_type |Ciąg |Nazwa typu ścieżki. Jeśli content_key_specs jest określony w żądaniu licencji hello, upewnij się, że toospecify, śledzić wszystkie typy jawnie. Błąd toodo tak spowoduje niepowodzenie tooplayback ostatnich 10 sekund. |
| content_key_specs  <br/> security_level |UInt32 |Definiuje wymagania dotyczące niezawodności klienta dla odtwarzania. <br/> 1 - opartych na oprogramowaniu whitebox kryptograficznego jest wymagana. <br/> 2 - kryptograficznego oprogramowania i zaciemnionego dekodera jest wymagana. <br/> 3 - hello materiału i szyfrowania operacje kluczy muszą być wykonywane w środowisku kopii zaufanego wykonywania sprzętu. <br/> 4 - hello kryptograficznych i dekodowania zawartości muszą być wykonywane w środowisku kopii zaufanego wykonywania sprzętu.  <br/> 5 - hello kryptograficznego, dekodowania i wszystkie obsługi hello nośnika (skompresowanym i nieskompresowanym) musi obsługiwać w środowisku kopii zaufanego wykonywania sprzętu. |
| content_key_specs <br/> required_output_protection.hdc |String — jeden z: HDCP_V2 HDCP_NONE, HDCP_V1, |Wskazuje, czy jest wymagane HDCP |
| content_key_specs <br/>key |Base64 <br/>ciąg kodowany jako |Toouse klucza zawartości dla tej ścieżki. Jeśli zostanie określona, hello track_type lub key_id jest wymagana.  Ta opcja umożliwia dostawcy zawartości hello tooinject hello klucz zawartości dla tej ścieżki, zamiast czekać na serwer licencji Widevine Generowanie lub wyszukiwania klucza. |
| content_key_specs.key_id |Kodowany w formacie Base64 ciąg binarny, 16 bajtów |Unikatowy identyfikator dla hello klucza. |

## <a name="policy-overrides"></a>Zastąpienia zasad
| Nazwa | Wartość | Opis |
| --- | --- | --- |
| policy_overrides. can_play |Wartość logiczna. wartość PRAWDA lub FAŁSZ |Wskazuje, że odtwarzanie hello zawartości jest dozwolone. Domyślna to false. |
| policy_overrides. can_persist |Wartość logiczna. wartość PRAWDA lub FAŁSZ |Wskazuje, że licencji hello może być utrwalona toonon pamięć w trybie offline. Domyślna to false. |
| policy_overrides. can_renew |wartość logiczną PRAWDA lub FAŁSZ |Wskazuje, że odnowienia licencji jest dozwolone. Jeśli PRAWDA, czas trwania hello hello licencji można przedłużyć pulsu. Domyślna to false. |
| policy_overrides. license_duration_seconds |Int64 |Wskazuje hello przedział czasu dla określonych licencji. Wartość 0 oznacza brak bez czasu trwania toohello limit. Domyślna to 0. |
| policy_overrides. rental_duration_seconds |Int64 |Określa przedział czasu hello podczas odtwarzania jest dozwolone. Wartość 0 oznacza brak bez czasu trwania toohello limit. Domyślna to 0. |
| policy_overrides. playback_duration_seconds |Int64 |Witaj, wyświetlanie przedziale czasu, po uruchomieniu odtwarzania w hello okres licencji. Wartość 0 oznacza brak bez czasu trwania toohello limit. Domyślna to 0. |
| policy_overrides. renewal_server_url |Ciąg |Wszystkie żądania pulsu (odnowienia) ta licencja jest skierowana toohello określony adres URL. To pole jest używane tylko, jeśli can_renew ma wartość true. |
| policy_overrides. renewal_delay_seconds |Int64 |Liczbę sekund po license_start_time, przed próbą najpierw odnawiania. To pole jest używane tylko, jeśli can_renew ma wartość true. Wartość domyślna to 0 |
| policy_overrides. renewal_retry_interval_seconds |Int64 |Określa opóźnienie hello w sekundach między żądań odnowienia kolejnych licencji, w razie awarii. To pole jest używane tylko, jeśli can_renew ma wartość true. |
| policy_overrides. renewal_recovery_duration_seconds |Int64 |Okno Hello czasu, w którym odtwarzanie jest dozwolony toocontinue podczas odnawiania jest próba, jeszcze nie powiodło się ze względu toobackend problemów z serwerem licencji hello. Wartość 0 oznacza brak bez czasu trwania toohello limit. To pole jest używane tylko, jeśli can_renew ma wartość true. |
| policy_overrides. renew_with_usage |wartość logiczną PRAWDA lub FAŁSZ |Wskazuje, że licencji hello są przesyłane do odnowienia, po uruchomieniu użycia. To pole jest używane tylko, jeśli can_renew ma wartość true. |

## <a name="session-initialization"></a>Inicjowanie sesji
| Nazwa | Wartość | Opis |
| --- | --- | --- |
| provider_session_token |Ciąg kodowany jako Base64 |Token sesji jest przekazany z powrotem do licencji hello i będą istnieć w kolejnych odnowienia.  poza sesji nie zachowa Hello tokenu sesji. |
| provider_client_token |Ciąg kodowany jako Base64 |Token toosend klienta ponownie hello licencji odpowiedzi.  Jeśli żądanie licencji hello zawiera token klienta, ta wartość jest ignorowana. token klienta Hello będzie trwało poza sesji licencji. |
| override_provider_client_token |Wartość logiczna. wartość PRAWDA lub FAŁSZ |Jeśli wartość FAŁSZ i hello żądanie licencji zawiera token klienta, użyj hello tokenu z żądania hello, nawet wtedy, gdy określono token klienta w tej struktury.  Jeśli PRAWDA, należy zawsze używać tokenu hello określone w tej struktury. |

## <a name="configure-your-widevine-licenses-using-net-types"></a>Konfigurowanie licencji Widevine przy użyciu typów .NET
Usługa Media Services udostępnia interfejsów API architektury .NET, które umożliwiają skonfigurowanie licencji Widevine. 

### <a name="classes-as-defined-in-hello-media-services-net-sdk"></a>Klasy zgodnie z definicją w hello .NET SDK usługi Media Services
Oto Hello hello definicje typów.

    public class WidevineMessage
    {
        public WidevineMessage();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public AllowedTrackTypes? allowed_track_types { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public ContentKeySpecs[] content_key_specs { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public object policy_overrides { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum AllowedTrackTypes
    {
        SD_ONLY = 0,
        SD_HD = 1
    }
    public class ContentKeySpecs
    {
        public ContentKeySpecs();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string key_id { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public RequiredOutputProtection required_output_protection { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public int? security_level { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string track_type { get; set; }
    }

    public class RequiredOutputProtection
    {
        public RequiredOutputProtection();

        public Hdcp hdcp { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum Hdcp
    {
        HDCP_NONE = 0,
        HDCP_V1 = 1,
        HDCP_V2 = 2
    }

### <a name="example"></a>Przykład
powitania po przykładzie pokazano, jak toouse interfejsów API architektury .NET tooconfigure proste licencji Widevine.

    private static string ConfigureWidevineLicenseTemplate()
    {
        var template = new WidevineMessage
        {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                new ContentKeySpecs
                {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                }
            },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
        };

        string configuration = JsonConvert.SerializeObject(template);
        return configuration;
    }


## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zobacz też
[Za pomocą PlayReady i Widevine dynamicznie Common Encryption](media-services-protect-with-drm.md)

