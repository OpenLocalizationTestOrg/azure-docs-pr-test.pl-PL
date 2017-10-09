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
# <a name="widevine-license-template-overview"></a><span data-ttu-id="8d0f3-103">Omówienie szablonu licencji Widevine</span><span class="sxs-lookup"><span data-stu-id="8d0f3-103">Widevine license template overview</span></span>
## <a name="overview"></a><span data-ttu-id="8d0f3-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8d0f3-104">Overview</span></span>
<span data-ttu-id="8d0f3-105">Usługa Azure Media Services umożliwia teraz tooconfigure i żądania licencji Widevine.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-105">Azure Media Services now enables you tooconfigure and request Widevine licenses.</span></span> <span data-ttu-id="8d0f3-106">Gdy hello player użytkownik końcowy podejmie próbę tooplay zawartość chroniona Widevine, żądanie jest wysłane toohello licencji dostarczania usługi tooobtain licencji.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-106">When hello end user player tries tooplay your Widevine protected content, a request is sent toohello license delivery service tooobtain a license.</span></span> <span data-ttu-id="8d0f3-107">Jeśli usługa licencji hello zatwierdza Żądanie hello, wystawia licencję hello, która jest wysłane toohello klienta i mogą być używane toodecrypt i play hello określonej zawartości.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-107">If hello license service approves hello request, it issues hello license which is sent toohello client and can be used toodecrypt and play hello specified content.</span></span>

<span data-ttu-id="8d0f3-108">Żądania licencji Widevine jest w formacie JSON wiadomości.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-108">Widevine license request is formatted as a JSON message.</span></span>  

>[!NOTE]
> <span data-ttu-id="8d0f3-109">Możesz wybrać toocreate pusty komunikat z nie wartości po prostu "{}" i zostanie utworzony szablon licencji z wszystkimi wartościami domyślnymi.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-109">You can choose toocreate an empty message with no values just "{}" and a license template will be created with all defaults.</span></span> <span data-ttu-id="8d0f3-110">domyślne Hello działa w większości przypadków.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-110">hello default works for most cases.</span></span> <span data-ttu-id="8d0f3-111">Na przykład w MS na podstawie licencji dostarczania scenariusze, które powinny być zawsze domyślnie.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-111">For example, for MS based license delivery scenarios that should always be default.</span></span> <span data-ttu-id="8d0f3-112">Jeśli potrzebujesz hello tooset "dostawca" i "content_id" wartości dostawcy muszą pasować do poświadczeń Widevine firmy Google.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-112">If you do need tooset hello "provider" and "content_id" values, a provider must match Google's Widevine credentials.</span></span>

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

## <a name="json-message"></a><span data-ttu-id="8d0f3-113">Komunikat JSON</span><span class="sxs-lookup"><span data-stu-id="8d0f3-113">JSON message</span></span>
| <span data-ttu-id="8d0f3-114">Nazwa</span><span class="sxs-lookup"><span data-stu-id="8d0f3-114">Name</span></span> | <span data-ttu-id="8d0f3-115">Wartość</span><span class="sxs-lookup"><span data-stu-id="8d0f3-115">Value</span></span> | <span data-ttu-id="8d0f3-116">Opis</span><span class="sxs-lookup"><span data-stu-id="8d0f3-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d0f3-117">ładunek</span><span class="sxs-lookup"><span data-stu-id="8d0f3-117">payload</span></span> |<span data-ttu-id="8d0f3-118">Ciąg kodowany jako Base64</span><span class="sxs-lookup"><span data-stu-id="8d0f3-118">Base64 encoded string</span></span> |<span data-ttu-id="8d0f3-119">żądanie licencji Hello wysłane przez klienta.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-119">hello license request sent by a client.</span></span> |
| <span data-ttu-id="8d0f3-120">content_id</span><span class="sxs-lookup"><span data-stu-id="8d0f3-120">content_id</span></span> |<span data-ttu-id="8d0f3-121">Ciąg kodowany jako Base64</span><span class="sxs-lookup"><span data-stu-id="8d0f3-121">Base64 encoded string</span></span> |<span data-ttu-id="8d0f3-122">Identyfikator używany do każdego content_key_specs.track_type tooderive KeyId(s) oraz kluczy zawartości.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-122">Identifier used tooderive KeyId(s) and Content Key(s) for each content_key_specs.track_type.</span></span> |
| <span data-ttu-id="8d0f3-123">Dostawcy</span><span class="sxs-lookup"><span data-stu-id="8d0f3-123">provider</span></span> |<span data-ttu-id="8d0f3-124">Ciąg</span><span class="sxs-lookup"><span data-stu-id="8d0f3-124">string</span></span> |<span data-ttu-id="8d0f3-125">Używane toolook się zasad i zawartości kluczy.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-125">Used toolook up content keys and policies.</span></span> <span data-ttu-id="8d0f3-126">Jeśli MS klucza dostawy jest używane w celu dostarczania licencji Widevine, ten parametr zostanie zignorowany.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-126">If MS key delivery is used for Widevine license delivery, this parameter is ignored.</span></span> |
| <span data-ttu-id="8d0f3-127">nazwa_zasady</span><span class="sxs-lookup"><span data-stu-id="8d0f3-127">policy_name</span></span> |<span data-ttu-id="8d0f3-128">Ciąg</span><span class="sxs-lookup"><span data-stu-id="8d0f3-128">string</span></span> |<span data-ttu-id="8d0f3-129">Nazwa zasady wcześniej zarejestrowane.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-129">Name of a previously registered policy.</span></span> <span data-ttu-id="8d0f3-130">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="8d0f3-130">Optional</span></span> |
| <span data-ttu-id="8d0f3-131">allowed_track_types</span><span class="sxs-lookup"><span data-stu-id="8d0f3-131">allowed_track_types</span></span> |<span data-ttu-id="8d0f3-132">wyliczenia</span><span class="sxs-lookup"><span data-stu-id="8d0f3-132">enum</span></span> |<span data-ttu-id="8d0f3-133">SD_ONLY lub SD_HD.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-133">SD_ONLY or SD_HD.</span></span> <span data-ttu-id="8d0f3-134">Formanty, które zawartości kluczy powinien być uwzględniany w licencji</span><span class="sxs-lookup"><span data-stu-id="8d0f3-134">Controls which content keys should be included in a license</span></span> |
| <span data-ttu-id="8d0f3-135">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="8d0f3-135">content_key_specs</span></span> |<span data-ttu-id="8d0f3-136">Tablica JSON struktur, zobacz **specyfikacji klucz zawartości** poniżej</span><span class="sxs-lookup"><span data-stu-id="8d0f3-136">array of JSON structures, see **Content Key Specs** below</span></span> |<span data-ttu-id="8d0f3-137">Skuteczniejszą kontrolę na tooreturn kluczy zawartości.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-137">A finer grained control on what content keys tooreturn.</span></span> <span data-ttu-id="8d0f3-138">Aby uzyskać więcej informacji, zobacz zawartości specyfikacja klucza poniżej.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-138">See Content Key Spec below for details.</span></span>  <span data-ttu-id="8d0f3-139">Można określić tylko jeden allowed_track_types i content_key_specs.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-139">Only one of allowed_track_types and content_key_specs can be specified.</span></span> |
| <span data-ttu-id="8d0f3-140">use_policy_overrides_exclusively</span><span class="sxs-lookup"><span data-stu-id="8d0f3-140">use_policy_overrides_exclusively</span></span> |<span data-ttu-id="8d0f3-141">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-141">boolean.</span></span> <span data-ttu-id="8d0f3-142">wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="8d0f3-142">true or false</span></span> |<span data-ttu-id="8d0f3-143">Użyj zasad atrybuty określone w policy_overrides i pominąć wszystkie zapisane wcześniej zasady.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-143">Use policy attributes specified by policy_overrides and omit all previously stored policy.</span></span> |
| <span data-ttu-id="8d0f3-144">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="8d0f3-144">policy_overrides</span></span> |<span data-ttu-id="8d0f3-145">Struktura JSON, zobacz **zasady zastępują** poniżej</span><span class="sxs-lookup"><span data-stu-id="8d0f3-145">JSON structure, see **Policy Overrides** below</span></span> |<span data-ttu-id="8d0f3-146">Ustawienia zasad dla tej licencji.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-146">Policy settings for this license.</span></span>  <span data-ttu-id="8d0f3-147">W przypadku hello ten zasób ma wstępnie zdefiniowane zasady, te określonej wartości będą używane.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-147">In hello event this asset has a pre-defined policy, these specified values will be used.</span></span> |
| <span data-ttu-id="8d0f3-148">session_init</span><span class="sxs-lookup"><span data-stu-id="8d0f3-148">session_init</span></span> |<span data-ttu-id="8d0f3-149">Struktura JSON, zobacz **inicjowania sesji** poniżej</span><span class="sxs-lookup"><span data-stu-id="8d0f3-149">JSON structure, see **Session Initialization** below</span></span> |<span data-ttu-id="8d0f3-150">Opcjonalne dane przekazywane toolicense.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-150">Optional data passed toolicense.</span></span> |
| <span data-ttu-id="8d0f3-151">parse_only</span><span class="sxs-lookup"><span data-stu-id="8d0f3-151">parse_only</span></span> |<span data-ttu-id="8d0f3-152">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-152">boolean.</span></span> <span data-ttu-id="8d0f3-153">wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="8d0f3-153">true or false</span></span> |<span data-ttu-id="8d0f3-154">żądanie licencji Hello jest analizowana, ale żadna licencja jest wystawiony.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-154">hello license request is parsed but no license is issued.</span></span> <span data-ttu-id="8d0f3-155">Jednak wartości formularza hello licencji żądania jest zwracany w odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-155">However, values form hello license request are returned in hello response.</span></span> |

## <a name="content-key-specs"></a><span data-ttu-id="8d0f3-156">Dane techniczne klucz zawartości</span><span class="sxs-lookup"><span data-stu-id="8d0f3-156">Content Key Specs</span></span>
<span data-ttu-id="8d0f3-157">Jeśli istnieje już istniejących zasad, nie ma żadnych toospecify potrzeby żadnego hello wartości w hello specyfikacja klucza zawartości.  Witaj wstępnie istniejące zasady skojarzone z tą zawartością będzie toodetermine używane hello dane wyjściowe ochrony, takie jak HDCP i CGMS.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-157">If a pre-existing policy exist, there is no need toospecify any of hello values in hello Content Key Spec.  hello pre-existing policy associated with this content will be used toodetermine hello output protection such as HDCP and CGMS.</span></span>  <span data-ttu-id="8d0f3-158">Jeśli wcześniej istniejących zasad nie jest zarejestrowany w powitania serwera licencji Widevine, hello dostawcy zawartości można wstrzyknąć hello wartości do hello żądanie licencji.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-158">If a pre-existing policy is not registered with hello Widevine License Server, hello content provider can inject hello values into hello license request.</span></span>   

<span data-ttu-id="8d0f3-159">Każdy content_key_specs należy określić dla wszystkich ścieżek, niezależnie od hello use_policy_overrides_exclusively opcji.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-159">Each content_key_specs must be specified for all tracks, regardless of hello option use_policy_overrides_exclusively.</span></span> 

| <span data-ttu-id="8d0f3-160">Nazwa</span><span class="sxs-lookup"><span data-stu-id="8d0f3-160">Name</span></span> | <span data-ttu-id="8d0f3-161">Wartość</span><span class="sxs-lookup"><span data-stu-id="8d0f3-161">Value</span></span> | <span data-ttu-id="8d0f3-162">Opis</span><span class="sxs-lookup"><span data-stu-id="8d0f3-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d0f3-163">content_key_specs.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-163">content_key_specs.</span></span> <span data-ttu-id="8d0f3-164">track_type</span><span class="sxs-lookup"><span data-stu-id="8d0f3-164">track_type</span></span> |<span data-ttu-id="8d0f3-165">Ciąg</span><span class="sxs-lookup"><span data-stu-id="8d0f3-165">string</span></span> |<span data-ttu-id="8d0f3-166">Nazwa typu ścieżki.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-166">A track type name.</span></span> <span data-ttu-id="8d0f3-167">Jeśli content_key_specs jest określony w żądaniu licencji hello, upewnij się, że toospecify, śledzić wszystkie typy jawnie.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-167">If content_key_specs is specified in hello license request, make sure toospecify all track types explicitly.</span></span> <span data-ttu-id="8d0f3-168">Błąd toodo tak spowoduje niepowodzenie tooplayback ostatnich 10 sekund.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-168">Failure toodo so will result in failure tooplayback past 10 seconds.</span></span> |
| <span data-ttu-id="8d0f3-169">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="8d0f3-169">content_key_specs</span></span>  <br/> <span data-ttu-id="8d0f3-170">security_level</span><span class="sxs-lookup"><span data-stu-id="8d0f3-170">security_level</span></span> |<span data-ttu-id="8d0f3-171">UInt32</span><span class="sxs-lookup"><span data-stu-id="8d0f3-171">uint32</span></span> |<span data-ttu-id="8d0f3-172">Definiuje wymagania dotyczące niezawodności klienta dla odtwarzania.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-172">Defines client robustness requirements for playback.</span></span> <br/> <span data-ttu-id="8d0f3-173">1 - opartych na oprogramowaniu whitebox kryptograficznego jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-173">1 - Software-based whitebox crypto is required.</span></span> <br/> <span data-ttu-id="8d0f3-174">2 - kryptograficznego oprogramowania i zaciemnionego dekodera jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-174">2 - Software crypto and an obfuscated decoder is required.</span></span> <br/> <span data-ttu-id="8d0f3-175">3 - hello materiału i szyfrowania operacje kluczy muszą być wykonywane w środowisku kopii zaufanego wykonywania sprzętu.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-175">3 - hello key material and crypto operations must be performed within a hardware backed trusted execution environment.</span></span> <br/> <span data-ttu-id="8d0f3-176">4 - hello kryptograficznych i dekodowania zawartości muszą być wykonywane w środowisku kopii zaufanego wykonywania sprzętu.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-176">4 - hello crypto and decoding of content must be performed within a hardware backed trusted execution environment.</span></span>  <br/> <span data-ttu-id="8d0f3-177">5 - hello kryptograficznego, dekodowania i wszystkie obsługi hello nośnika (skompresowanym i nieskompresowanym) musi obsługiwać w środowisku kopii zaufanego wykonywania sprzętu.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-177">5 - hello crypto, decoding and all handling of hello media (compressed and uncompressed) must be handled within a hardware backed trusted execution environment.</span></span> |
| <span data-ttu-id="8d0f3-178">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="8d0f3-178">content_key_specs</span></span> <br/> <span data-ttu-id="8d0f3-179">required_output_protection.hdc</span><span class="sxs-lookup"><span data-stu-id="8d0f3-179">required_output_protection.hdc</span></span> |<span data-ttu-id="8d0f3-180">String — jeden z: HDCP_V2 HDCP_NONE, HDCP_V1,</span><span class="sxs-lookup"><span data-stu-id="8d0f3-180">string - one of: HDCP_NONE, HDCP_V1, HDCP_V2</span></span> |<span data-ttu-id="8d0f3-181">Wskazuje, czy jest wymagane HDCP</span><span class="sxs-lookup"><span data-stu-id="8d0f3-181">Indicates whether HDCP is require</span></span> |
| <span data-ttu-id="8d0f3-182">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="8d0f3-182">content_key_specs</span></span> <br/><span data-ttu-id="8d0f3-183">key</span><span class="sxs-lookup"><span data-stu-id="8d0f3-183">key</span></span> |<span data-ttu-id="8d0f3-184">Base64</span><span class="sxs-lookup"><span data-stu-id="8d0f3-184">Base64</span></span> <br/><span data-ttu-id="8d0f3-185">ciąg kodowany jako</span><span class="sxs-lookup"><span data-stu-id="8d0f3-185">encoded string</span></span> |<span data-ttu-id="8d0f3-186">Toouse klucza zawartości dla tej ścieżki. Jeśli zostanie określona, hello track_type lub key_id jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-186">Content key toouse for this track. If specified, hello track_type or key_id is required.</span></span>  <span data-ttu-id="8d0f3-187">Ta opcja umożliwia dostawcy zawartości hello tooinject hello klucz zawartości dla tej ścieżki, zamiast czekać na serwer licencji Widevine Generowanie lub wyszukiwania klucza.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-187">This option allows hello content provider tooinject hello content key for this track instead of letting Widevine license server generate or lookup a key.</span></span> |
| <span data-ttu-id="8d0f3-188">content_key_specs.key_id</span><span class="sxs-lookup"><span data-stu-id="8d0f3-188">content_key_specs.key_id</span></span> |<span data-ttu-id="8d0f3-189">Kodowany w formacie Base64 ciąg binarny, 16 bajtów</span><span class="sxs-lookup"><span data-stu-id="8d0f3-189">Base64 encoded string  binary, 16 bytes</span></span> |<span data-ttu-id="8d0f3-190">Unikatowy identyfikator dla hello klucza.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-190">Unique identifier for hello key.</span></span> |

## <a name="policy-overrides"></a><span data-ttu-id="8d0f3-191">Zastąpienia zasad</span><span class="sxs-lookup"><span data-stu-id="8d0f3-191">Policy Overrides</span></span>
| <span data-ttu-id="8d0f3-192">Nazwa</span><span class="sxs-lookup"><span data-stu-id="8d0f3-192">Name</span></span> | <span data-ttu-id="8d0f3-193">Wartość</span><span class="sxs-lookup"><span data-stu-id="8d0f3-193">Value</span></span> | <span data-ttu-id="8d0f3-194">Opis</span><span class="sxs-lookup"><span data-stu-id="8d0f3-194">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d0f3-195">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-195">policy_overrides.</span></span> <span data-ttu-id="8d0f3-196">can_play</span><span class="sxs-lookup"><span data-stu-id="8d0f3-196">can_play</span></span> |<span data-ttu-id="8d0f3-197">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-197">boolean.</span></span> <span data-ttu-id="8d0f3-198">wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="8d0f3-198">true or false</span></span> |<span data-ttu-id="8d0f3-199">Wskazuje, że odtwarzanie hello zawartości jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-199">Indicates that playback of hello content is allowed.</span></span> <span data-ttu-id="8d0f3-200">Domyślna to false.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-200">Default is false.</span></span> |
| <span data-ttu-id="8d0f3-201">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-201">policy_overrides.</span></span> <span data-ttu-id="8d0f3-202">can_persist</span><span class="sxs-lookup"><span data-stu-id="8d0f3-202">can_persist</span></span> |<span data-ttu-id="8d0f3-203">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-203">boolean.</span></span> <span data-ttu-id="8d0f3-204">wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="8d0f3-204">true or false</span></span> |<span data-ttu-id="8d0f3-205">Wskazuje, że licencji hello może być utrwalona toonon pamięć w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-205">Indicates that hello license may be persisted toonon-volatile storage for offline use.</span></span> <span data-ttu-id="8d0f3-206">Domyślna to false.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-206">Default is false.</span></span> |
| <span data-ttu-id="8d0f3-207">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-207">policy_overrides.</span></span> <span data-ttu-id="8d0f3-208">can_renew</span><span class="sxs-lookup"><span data-stu-id="8d0f3-208">can_renew</span></span> |<span data-ttu-id="8d0f3-209">wartość logiczną PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="8d0f3-209">boolean true or false</span></span> |<span data-ttu-id="8d0f3-210">Wskazuje, że odnowienia licencji jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-210">Indicates that renewal of this license is allowed.</span></span> <span data-ttu-id="8d0f3-211">Jeśli PRAWDA, czas trwania hello hello licencji można przedłużyć pulsu.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-211">If true, hello duration of hello license can be extended by heartbeat.</span></span> <span data-ttu-id="8d0f3-212">Domyślna to false.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-212">Default is false.</span></span> |
| <span data-ttu-id="8d0f3-213">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-213">policy_overrides.</span></span> <span data-ttu-id="8d0f3-214">license_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="8d0f3-214">license_duration_seconds</span></span> |<span data-ttu-id="8d0f3-215">Int64</span><span class="sxs-lookup"><span data-stu-id="8d0f3-215">int64</span></span> |<span data-ttu-id="8d0f3-216">Wskazuje hello przedział czasu dla określonych licencji.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-216">Indicates hello time window for this specific license.</span></span> <span data-ttu-id="8d0f3-217">Wartość 0 oznacza brak bez czasu trwania toohello limit.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-217">A value of 0 indicates that there is no limit toohello duration.</span></span> <span data-ttu-id="8d0f3-218">Domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-218">Default is 0.</span></span> |
| <span data-ttu-id="8d0f3-219">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-219">policy_overrides.</span></span> <span data-ttu-id="8d0f3-220">rental_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="8d0f3-220">rental_duration_seconds</span></span> |<span data-ttu-id="8d0f3-221">Int64</span><span class="sxs-lookup"><span data-stu-id="8d0f3-221">int64</span></span> |<span data-ttu-id="8d0f3-222">Określa przedział czasu hello podczas odtwarzania jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-222">Indicates hello time window while playback is permitted.</span></span> <span data-ttu-id="8d0f3-223">Wartość 0 oznacza brak bez czasu trwania toohello limit.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-223">A value of 0 indicates that there is no limit toohello duration.</span></span> <span data-ttu-id="8d0f3-224">Domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-224">Default is 0.</span></span> |
| <span data-ttu-id="8d0f3-225">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-225">policy_overrides.</span></span> <span data-ttu-id="8d0f3-226">playback_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="8d0f3-226">playback_duration_seconds</span></span> |<span data-ttu-id="8d0f3-227">Int64</span><span class="sxs-lookup"><span data-stu-id="8d0f3-227">int64</span></span> |<span data-ttu-id="8d0f3-228">Witaj, wyświetlanie przedziale czasu, po uruchomieniu odtwarzania w hello okres licencji.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-228">hello viewing window of time once playback starts within hello license duration.</span></span> <span data-ttu-id="8d0f3-229">Wartość 0 oznacza brak bez czasu trwania toohello limit.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-229">A value of 0 indicates that there is no limit toohello duration.</span></span> <span data-ttu-id="8d0f3-230">Domyślna to 0.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-230">Default is 0.</span></span> |
| <span data-ttu-id="8d0f3-231">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-231">policy_overrides.</span></span> <span data-ttu-id="8d0f3-232">renewal_server_url</span><span class="sxs-lookup"><span data-stu-id="8d0f3-232">renewal_server_url</span></span> |<span data-ttu-id="8d0f3-233">Ciąg</span><span class="sxs-lookup"><span data-stu-id="8d0f3-233">string</span></span> |<span data-ttu-id="8d0f3-234">Wszystkie żądania pulsu (odnowienia) ta licencja jest skierowana toohello określony adres URL.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-234">All heartbeat (renewal) requests for this license shall be directed toohello specified URL.</span></span> <span data-ttu-id="8d0f3-235">To pole jest używane tylko, jeśli can_renew ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-235">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="8d0f3-236">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-236">policy_overrides.</span></span> <span data-ttu-id="8d0f3-237">renewal_delay_seconds</span><span class="sxs-lookup"><span data-stu-id="8d0f3-237">renewal_delay_seconds</span></span> |<span data-ttu-id="8d0f3-238">Int64</span><span class="sxs-lookup"><span data-stu-id="8d0f3-238">int64</span></span> |<span data-ttu-id="8d0f3-239">Liczbę sekund po license_start_time, przed próbą najpierw odnawiania.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-239">How many seconds after license_start_time, before renewal is first attempted.</span></span> <span data-ttu-id="8d0f3-240">To pole jest używane tylko, jeśli can_renew ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-240">This field is only used if can_renew is true.</span></span> <span data-ttu-id="8d0f3-241">Wartość domyślna to 0</span><span class="sxs-lookup"><span data-stu-id="8d0f3-241">Default is 0</span></span> |
| <span data-ttu-id="8d0f3-242">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-242">policy_overrides.</span></span> <span data-ttu-id="8d0f3-243">renewal_retry_interval_seconds</span><span class="sxs-lookup"><span data-stu-id="8d0f3-243">renewal_retry_interval_seconds</span></span> |<span data-ttu-id="8d0f3-244">Int64</span><span class="sxs-lookup"><span data-stu-id="8d0f3-244">int64</span></span> |<span data-ttu-id="8d0f3-245">Określa opóźnienie hello w sekundach między żądań odnowienia kolejnych licencji, w razie awarii.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-245">Specifies hello delay in seconds between subsequent license renewal requests, in case of failure.</span></span> <span data-ttu-id="8d0f3-246">To pole jest używane tylko, jeśli can_renew ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-246">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="8d0f3-247">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-247">policy_overrides.</span></span> <span data-ttu-id="8d0f3-248">renewal_recovery_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="8d0f3-248">renewal_recovery_duration_seconds</span></span> |<span data-ttu-id="8d0f3-249">Int64</span><span class="sxs-lookup"><span data-stu-id="8d0f3-249">int64</span></span> |<span data-ttu-id="8d0f3-250">Okno Hello czasu, w którym odtwarzanie jest dozwolony toocontinue podczas odnawiania jest próba, jeszcze nie powiodło się ze względu toobackend problemów z serwerem licencji hello.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-250">hello window of time, in which playback is allowed toocontinue while renewal is attempted, yet unsuccessful due toobackend problems with hello license server.</span></span> <span data-ttu-id="8d0f3-251">Wartość 0 oznacza brak bez czasu trwania toohello limit.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-251">A value of 0 indicates that there is no limit toohello duration.</span></span> <span data-ttu-id="8d0f3-252">To pole jest używane tylko, jeśli can_renew ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-252">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="8d0f3-253">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-253">policy_overrides.</span></span> <span data-ttu-id="8d0f3-254">renew_with_usage</span><span class="sxs-lookup"><span data-stu-id="8d0f3-254">renew_with_usage</span></span> |<span data-ttu-id="8d0f3-255">wartość logiczną PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="8d0f3-255">boolean true or false</span></span> |<span data-ttu-id="8d0f3-256">Wskazuje, że licencji hello są przesyłane do odnowienia, po uruchomieniu użycia.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-256">Indicates that hello license shall be sent for renewal when usage is started.</span></span> <span data-ttu-id="8d0f3-257">To pole jest używane tylko, jeśli can_renew ma wartość true.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-257">This field is only used if can_renew is true.</span></span> |

## <a name="session-initialization"></a><span data-ttu-id="8d0f3-258">Inicjowanie sesji</span><span class="sxs-lookup"><span data-stu-id="8d0f3-258">Session Initialization</span></span>
| <span data-ttu-id="8d0f3-259">Nazwa</span><span class="sxs-lookup"><span data-stu-id="8d0f3-259">Name</span></span> | <span data-ttu-id="8d0f3-260">Wartość</span><span class="sxs-lookup"><span data-stu-id="8d0f3-260">Value</span></span> | <span data-ttu-id="8d0f3-261">Opis</span><span class="sxs-lookup"><span data-stu-id="8d0f3-261">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8d0f3-262">provider_session_token</span><span class="sxs-lookup"><span data-stu-id="8d0f3-262">provider_session_token</span></span> |<span data-ttu-id="8d0f3-263">Ciąg kodowany jako Base64</span><span class="sxs-lookup"><span data-stu-id="8d0f3-263">Base64 encoded string</span></span> |<span data-ttu-id="8d0f3-264">Token sesji jest przekazany z powrotem do licencji hello i będą istnieć w kolejnych odnowienia.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-264">This session token is passed back in hello license and will exist in subsequent renewals.</span></span>  <span data-ttu-id="8d0f3-265">poza sesji nie zachowa Hello tokenu sesji.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-265">hello session token will not persist beyond sessions.</span></span> |
| <span data-ttu-id="8d0f3-266">provider_client_token</span><span class="sxs-lookup"><span data-stu-id="8d0f3-266">provider_client_token</span></span> |<span data-ttu-id="8d0f3-267">Ciąg kodowany jako Base64</span><span class="sxs-lookup"><span data-stu-id="8d0f3-267">Base64 encoded string</span></span> |<span data-ttu-id="8d0f3-268">Token toosend klienta ponownie hello licencji odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-268">Client token toosend back in hello license response.</span></span>  <span data-ttu-id="8d0f3-269">Jeśli żądanie licencji hello zawiera token klienta, ta wartość jest ignorowana.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-269">If hello license request contains a client token, this value is ignored.</span></span> <span data-ttu-id="8d0f3-270">token klienta Hello będzie trwało poza sesji licencji.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-270">hello client token will persist beyond license sessions.</span></span> |
| <span data-ttu-id="8d0f3-271">override_provider_client_token</span><span class="sxs-lookup"><span data-stu-id="8d0f3-271">override_provider_client_token</span></span> |<span data-ttu-id="8d0f3-272">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-272">boolean.</span></span> <span data-ttu-id="8d0f3-273">wartość PRAWDA lub FAŁSZ</span><span class="sxs-lookup"><span data-stu-id="8d0f3-273">true or false</span></span> |<span data-ttu-id="8d0f3-274">Jeśli wartość FAŁSZ i hello żądanie licencji zawiera token klienta, użyj hello tokenu z żądania hello, nawet wtedy, gdy określono token klienta w tej struktury.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-274">If false and hello license request contains a client token, use hello token from hello request even if a client token was specified in this structure.</span></span>  <span data-ttu-id="8d0f3-275">Jeśli PRAWDA, należy zawsze używać tokenu hello określone w tej struktury.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-275">If true, always use hello token specified in this structure.</span></span> |

## <a name="configure-your-widevine-licenses-using-net-types"></a><span data-ttu-id="8d0f3-276">Konfigurowanie licencji Widevine przy użyciu typów .NET</span><span class="sxs-lookup"><span data-stu-id="8d0f3-276">Configure your Widevine licenses using .NET types</span></span>
<span data-ttu-id="8d0f3-277">Usługa Media Services udostępnia interfejsów API architektury .NET, które umożliwiają skonfigurowanie licencji Widevine.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-277">Media Services provides .NET APIs that let you configure your Widevine licenses.</span></span> 

### <a name="classes-as-defined-in-hello-media-services-net-sdk"></a><span data-ttu-id="8d0f3-278">Klasy zgodnie z definicją w hello .NET SDK usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="8d0f3-278">Classes as defined in hello Media Services .NET SDK</span></span>
<span data-ttu-id="8d0f3-279">Oto Hello hello definicje typów.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-279">hello following are hello definitions of these types.</span></span>

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

### <a name="example"></a><span data-ttu-id="8d0f3-280">Przykład</span><span class="sxs-lookup"><span data-stu-id="8d0f3-280">Example</span></span>
<span data-ttu-id="8d0f3-281">powitania po przykładzie pokazano, jak toouse interfejsów API architektury .NET tooconfigure proste licencji Widevine.</span><span class="sxs-lookup"><span data-stu-id="8d0f3-281">hello following example shows how toouse .NET APIs tooconfigure  a simple Widevine license.</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="8d0f3-282">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="8d0f3-282">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8d0f3-283">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="8d0f3-283">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="8d0f3-284">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="8d0f3-284">See also</span></span>
[<span data-ttu-id="8d0f3-285">Za pomocą PlayReady i Widevine dynamicznie Common Encryption</span><span class="sxs-lookup"><span data-stu-id="8d0f3-285">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

