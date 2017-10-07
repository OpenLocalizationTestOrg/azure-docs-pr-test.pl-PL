---
title: "Oświadczenia mapowanie w usłudze Azure Active Directory (publicznej wersji zapoznawczej) | Dokumentacja firmy Microsoft"
description: "Na tej stronie opisano mapowania oświadczenia usługi Azure Active Directory."
services: active-directory
author: billmath
manager: femila
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: billmath
ms.openlocfilehash: ff07b9954d5c2ce71ab0ffd0db49fde15f323586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="claims-mapping-in-azure-active-directory-public-preview"></a>Oświadczenia mapowanie w usłudze Azure Active Directory (publicznej wersji zapoznawczej)

>[!NOTE]
>Ta funkcja zastępuje i zastępuje hello [oświadczeń dostosowania](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-claims-customization) oferowane za pośrednictwem portalu hello dzisiaj. W przypadku dostosowania oświadczeń przy użyciu portalu hello dodatkowo toohello wykres PowerShell — metoda szczegółowe w tym dokumencie na powitania sam aplikację, wystawiony dla tej aplikacji będzie ignorować konfiguracji hello w portalu hello tokenów.
Konfiguracje wprowadzone przy użyciu metody hello szczegółowo opisane w tym dokumencie nie zostaną odzwierciedlone w portalu hello.

Ta funkcja jest używana przez administratorów dzierżawy toocustomize hello oświadczeń wysyłanego w tokenach dla określonej aplikacji w swojej dzierżawy. Można użyć oświadczeń mapowanie zasad do:

- Wybierz, jakie oświadczenia są uwzględnione w tokenach.
- Tworzenie typów oświadczeń, które jeszcze nie istnieje.
- Wybierz lub zmień hello źródło danych emitowanych w określonych oświadczeń.

>[!NOTE]
>Ta funkcja jest obecnie w wersji zapoznawczej. Można przygotować toorevert lub Usuń wszystkie zmiany. Funkcja Hello jest dostępna w żadnych subskrypcji usługi Azure Active Directory (Azure AD) w publicznej wersji zapoznawczej. Gdy funkcja hello staje się ogólnie dostępna, niektórych aspektów funkcji hello mogą jednak wymagać subskrypcję usługi Azure Active Directory premium.

## <a name="claims-mapping-policy-type"></a>Mapowanie typu zasad oświadczeń
W usłudze Azure AD **zasad** obiekt reprezentuje zestaw reguł wymuszane na poszczególnych aplikacji lub na wszystkie aplikacje w organizacji. Każdego typu zasad ma unikatowy strukturę, z zestawem właściwości, które są następnie stosowane toowhich tooobjects, które są przypisane.

Oświadczenia A mapowania zasad jest typem **zasad** obiekt, który modyfikuje hello oświadczeń emitowanych w tokenów wystawionych dla określonych aplikacji.

## <a name="claim-sets"></a>W zestawie oświadczeń
Istnieją pewne zestawy oświadczeń, które określają, jak i kiedy są używane w tokenach.

### <a name="core-claim-set"></a>Podstawowy zestaw oświadczeń
Oświadczenia w podstawowej hello oświadczenia, zestawu są obecne w każdym tokenu, niezależnie od zasady. Te oświadczenia również są traktowane jako ograniczona i nie może być modyfikowany.

### <a name="basic-claim-set"></a>Zestaw oświadczeń podstawowe
zestaw oświadczeń podstawowe Hello zawiera hello oświadczenia, które są emitowane domyślnie tokeny (w dodanie toohello podstawowy zestaw oświadczeń). Te oświadczenia mogą pominięcia lub modyfikować za pomocą oświadczeń hello mapowanie zasad.

### <a name="restricted-claim-set"></a>Zestaw oświadczeń ograniczone
Nie można zmodyfikować ograniczeniami oświadczeń przy użyciu zasad. Witaj źródła danych nie można zmienić, a nie transformacja jest stosowana podczas generowania tych oświadczeń.

#### <a name="table-1-json-web-token-jwt-restricted-claim-set"></a>Tabela 1: Tokenu Web JSON (JWT) ograniczony zestaw oświadczeń
|Typ oświadczenia (nazwa)|
| ----- |
|_claim_names|
|_claim_sources|
|' access_token '|
|account_type|
|acr|
|Aktora|
|actortoken|
|AIO|
|altsecid|
|AMR|
|app_chain|
|app_displayname|
|app_res|
|appctx|
|appctxsender|
|Identyfikator aplikacji|
|appidacr|
|Potwierdzenia|
|at_hash|
|lub|
|auth_data|
|auth_time|
|authorization_code|
|azp|
|azpacr|
|c_hash|
|ca_enf|
|DW|
|cert_token_use|
|client_id|
|cloud_graph_host_name|
|cloud_instance_name|
|opcją cnf|
|Kod|
|funkcje sterowania|
|credential_keys|
|Renderowanie po stronie klienta|
|csr_type|
|Identyfikator urządzenia|
|dns_names|
|domain_dns_name|
|domain_netbios_name|
|e_exp|
|Adres e-mail|
|punkt końcowy|
|enfpolids|
|EXP|
|expires_on|
|Typ grant_type|
|Wykres|
|group_sids|
|grupy|
|hasgroups|
|hash_alg|
|home_oid|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/AuthenticationInstant|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/AuthenticationMethod|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/Expiration|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/EXPIRED|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/emailaddress|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/name|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/NameIdentifier|
|IAT|
|identityprovider|
|IDP|
|in_corp|
|Wystąpienie|
|adres_IP|
|isbrowserhostedapp|
|iss|
|jwk|
|key_id|
|key_type|
|mam_compliance_url|
|mam_enrollment_url|
|mam_terms_of_use_url|
|mdm_compliance_url|
|mdm_enrollment_url|
|mdm_terms_of_use_url|
|nameid|
|NBF|
|netbios_name|
|Identyfikator jednorazowy|
|Identyfikator OID|
|on_prem_id|
|onprem_sam_account_name|
|onprem_sid|
|openid2_id|
|hasło|
|platf|
|polids|
|pop_jwk|
|preferred_username|
|previous_refresh_token|
|primary_sid|
|Identyfikator PUID|
|pwd_exp|
|pwd_url|
|redirect_uri|
|refresh_token|
|refreshtoken|
|request_nonce|
|Zasobów|
|Rola|
|role|
|Zakres|
|punkt połączenia usługi|
|Identyfikator SID|
|Podpis|
|signin_state|
|src1|
|src2|
|Sub|
|tbid|
|tenant_display_name|
|tenant_region_scope|
|thumbnail_photo|
|TID|
|tokenAutologonEnabled|
|trustedfordelegation|
|unique_name|
|nazwy UPN|
|user_setting_sync_url|
|nazwa użytkownika|
|uti|
|VER|
|verified_primary_email|
|verified_secondary_email|
|wids|
|win_ver|

#### <a name="table-2-security-assertion-markup-language-saml-restricted-claim-set"></a>Tabela 2: Security (Assertion Markup Language SAML) ograniczony zestaw oświadczeń
|Typ oświadczenia (URI)|
| ----- |
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/Expiration|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/EXPIRED|
|http://schemas.microsoft.com/Identity/Claims/accesstoken|
|http://schemas.microsoft.com/Identity/Claims/openid2_id|
|http://schemas.microsoft.com/Identity/Claims/identityprovider|
|http://schemas.microsoft.com/Identity/Claims/objectidentifier|
|http://schemas.microsoft.com/Identity/Claims/PUID|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/NameIdentifier [MR1] |
|http://schemas.microsoft.com/Identity/Claims/tenantid|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/AuthenticationInstant|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/AuthenticationMethod|
|http://schemas.microsoft.com/accesscontrolservice/2010/07/Claims/identityprovider|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/groups|
|http://schemas.microsoft.com/Claims/groups.Link|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/role|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/wids|
|http://schemas.microsoft.com/2014/09/devicecontext/Claims/iscompliant|
|http://schemas.microsoft.com/2014/02/devicecontext/Claims/isknown|
|http://schemas.microsoft.com/2012/01/devicecontext/Claims/ismanaged|
|http://schemas.microsoft.com/2014/03/psso|
|http://schemas.microsoft.com/Claims/authnmethodsreferences|
|http://schemas.xmlsoap.org/ws/2009/09/Identity/Claims/Actor|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/samlissuername|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/confirmationkey|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/windowsaccountname|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/primarygroupsid|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/primarysid|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/authorizationdecision|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/Authentication|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/SID|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/denyonlyprimarygroupsid|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/denyonlyprimarysid|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/denyonlysid|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/denyonlywindowsdevicegroup|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/windowsdeviceclaim|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/windowsdevicegroup|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/windowsfqbnversion|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/windowssubauthority|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/windowsuserclaim|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/x500distinguishedname|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/UPN|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/GroupSID|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/SPN|
|http://schemas.microsoft.com/WS/2008/06/Identity/Claims/ispersistent|
|http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/privatepersonalidentifier|
|http://schemas.microsoft.com/Identity/Claims/SCOPE|

## <a name="claims-mapping-policy-properties"></a>Mapowanie właściwości zasad oświadczeń
Użyj właściwości hello mapowania toocontrol zasad, jakie oświadczenia są emitowane i gdzie danych hello są uzyskiwane z oświadczeń. Jeśli żadne zasady nie jest ustawiona, hello system wystawia tokeny zawierającego zestaw oświadczeń core hello, hello podstawowego zestawu oświadczeń i wszelkie oświadczenia opcjonalne, które aplikacji hello wybrał tooreceive.

### <a name="include-basic-claim-set"></a>Obejmują zestaw oświadczeń podstawowe

**Ciąg:** IncludeBasicClaimSet

**Typ danych:** wartość logiczną (True lub False)

**Podsumowanie:** ta właściwość określa, czy zestaw oświadczeń podstawowe hello jest uwzględnione w tokenach wpływ tych zasad. 

- Jeśli zestaw tooTrue, wszystkich oświadczeń w zestawie oświadczeń podstawowe hello są emitowane w tokenach wpływ hello zasad. 
- Jeśli zestaw tooFalse, oświadczeniami w zestawie oświadczeń podstawowe hello nie są w tokenach hello nie zostały indywidualnie dodane we właściwości schematu oświadczeń hello hello takie same zasady.

>[!NOTE] 
>Oświadczenia w podstawowej hello oświadczenia, zestawu są obecne w każdym tokenu, niezależnie od tego, co ta właściwość jest ustawiona na. 

### <a name="claims-schema"></a>Schemat oświadczeń

**Ciąg:** ClaimsSchema

**Typ danych:** obiektu blob JSON z jednego lub więcej wpisów schematu oświadczeń

**Podsumowanie:** właściwość ta definiuje, jakie oświadczenia są obecne w tokeny hello wpływ zasad hello, oprócz toohello podstawowego zestawu oświadczeń i hello core zestawu oświadczeń.
Dla każdego schematu oświadczeń wpisu zdefiniowane w tej właściwości niektóre informacje są wymagane. Należy określić, których pochodzą dane hello (**wartość** lub **pary Ident/**), i który dane hello oświadczenia jest emitowany jako (**typu oświadczenia**).

### <a name="claim-schema-entry-elements"></a>Elementy schematu wpisu oświadczeń

**Wartość:** hello wartość elementu definiuje wartości statycznej jako hello toobe danych emitowanych w hello oświadczeń.

**Identyfikator źródłowego/para:** hello źródła i identyfikator elementy zdefiniowane, gdzie danych hello hello oświadczenia są uzyskiwane z. 

element źródłowy Hello musi mieć ustawiony tooone hello poniżej: 


- "użytkownika": hello danych hello oświadczeń jest właściwością obiektu użytkownika hello. 
- "aplikacja": hello danych hello oświadczeń jest właściwość nazwy głównej usługi aplikacji (klienta) hello. 
- "zasobu": hello danych hello oświadczeń jest właściwość nazwy głównej usługi zasobów hello.
- "audience": hello dane oświadczeń hello jest właściwością na powitania nazwy głównej usługi będący hello odbiorców tokenu hello (albo powitania klienta lub zasób nazwy głównej usługi).
- "firmy": hello danych hello oświadczeń jest właściwością w obiekcie firmy hello zasobów dzierżawy.
- "transformacji": hello danych hello oświadczeń, pochodzi z przekształcania oświadczeń (patrz sekcja hello "przekształcania oświadczeń" w dalszej części tego artykułu). 

Jeśli źródło hello jest przekształcania, hello **TransformationID** elementu muszą być zawarte w tej definicji oświadczenia.

elementu ID Hello identyfikuje, które właściwości w źródle hello zawiera wartość hello hello oświadczenia. Witaj poniższej tabeli wymieniono wartości hello identyfikatora jest nieprawidłowa dla każdej wartości źródła.

#### <a name="table-3-valid-id-values-per-source"></a>Tabela 3: Prawidłowy identyfikator wartości dla każdego źródła
|Element źródłowy|ID|Opis|
|-----|-----|-----|
|Użytkownik|nazwisko|Nazwa rodziny|
|Użytkownik|Imię|Imię|
|Użytkownik|Nazwa wyświetlana|Nazwa wyświetlana|
|Użytkownik|Identyfikator obiektu|Identyfikator obiektu|
|Użytkownik|Poczty|Adres e-mail|
|Użytkownik|userPrincipalName|Główna nazwa użytkownika|
|Użytkownik|Dział|Dział|
|Użytkownik|onpremisessamaccountname|Dla nazwy konta Sam lokalne|
|Użytkownik|Nazwa NetBIOS|Nazwa NetBios|
|Użytkownik|NazwaDomenyDNS|Nazwa domeny DNS|
|Użytkownik|onpremisesecurityidentifier|Identyfikator zabezpieczeń lokalnych|
|Użytkownik|Nazwa firmy|Nazwa organizacji|
|Użytkownik|adres|Ulica|
|Użytkownik|KodPocztowy|Kod pocztowy|
|Użytkownik|preferredlanguange|Preferowany język|
|Użytkownik|onpremisesuserprincipalname|lokalną nazwą UPN|
|Użytkownik|mailnickname|Pseudonim poczty|
|Użytkownik|extensionattribute1|Atrybut rozszerzenia 1|
|Użytkownik|extensionattribute2|Atrybut rozszerzenia 2|
|Użytkownik|extensionattribute3|Atrybut rozszerzenia 3|
|Użytkownik|extensionattribute4|Atrybut rozszerzenia 4|
|Użytkownik|extensionattribute5|Atrybut rozszerzenia 5|
|Użytkownik|extensionattribute6|Atrybut rozszerzenia 6|
|Użytkownik|extensionattribute7|Atrybut rozszerzenia 7|
|Użytkownik|extensionattribute8|Atrybut rozszerzenia 8|
|Użytkownik|extensionattribute9|Atrybut rozszerzenia 9|
|Użytkownik|extensionattribute10|Atrybut rozszerzenia 10|
|Użytkownik|extensionattribute11|Atrybut rozszerzenia 11|
|Użytkownik|extensionattribute12|Atrybut rozszerzenia 12|
|Użytkownik|extensionattribute13|Atrybut rozszerzenia 13|
|Użytkownik|extensionattribute14|Atrybut rozszerzenia 14|
|Użytkownik|extensionattribute15|Atrybut rozszerzenia 15|
|Użytkownik|othermail|Inne poczty|
|Użytkownik|Kraju|Kraj|
|Użytkownik|city|Miasto|
|Użytkownik|state|Stan|
|Użytkownik|stanowisko|Stanowisko|
|Użytkownik|Identyfikator pracownika|Identyfikator pracownika|
|Użytkownik|facsimiletelephonenumber|Numer telefonu faksów|
|Aplikacja, zasobu, grupy odbiorców|Nazwa wyświetlana|Nazwa wyświetlana|
|Aplikacja, zasobu, grupy odbiorców|obiekty|Identyfikator obiektu|
|Aplikacja, zasobu, grupy odbiorców|tags|Etykieta nazwy głównej usługi|
|Firma|tenantcountry|Dzierżawcy kraju|

**TransformationID:** hello TransformationID element musi być podane tylko wtedy, gdy hello elementu źródła jest ustawiona zbyt "transformacji".

- Ten element musi być zgodna hello elementu Identyfikatora wpisu przekształcania hello hello **ClaimsTransformation** właściwość, która określa, jak jest generowany hello danych dla tego oświadczenia.

**Typ oświadczenia:** hello **JwtClaimType** i **SamlClaimType** elementy zdefiniować, które oświadczenia, ten wpis schematu oświadczenie odnosi się do.

- Witaj JwtClaimType musi zawierać nazwę hello toobe oświadczeń hello emitowanych w tokenów Jwt.
- Witaj SamlClaimType musi zawierać hello URI hello oświadczeń toobe wysyłanego w tokenach SAML.

>[!NOTE]
>Nazwy i identyfikatory URI oświadczeń w hello ograniczony oświadczenie set nie można używać elementów typu oświadczenia hello. Aby uzyskać więcej informacji zobacz hello sekcji "Wyjątki i ograniczenia" w dalszej części tego artykułu.

### <a name="claims-transformation"></a>Przekształcanie oświadczeń

**Ciąg:** ClaimsTransformation

**Typ danych:** obiektu blob JSON z jednego lub więcej wpisów przekształcania 

**Podsumowanie:** używać tej właściwości tooapply wspólnego przekształcenia toosource danych, danych wyjściowych hello toogenerate oświadczenia określone w hello schematu oświadczeń.

**Identyfikator:** Użyj hello identyfikator elementu tooreference tego wpisu przekształcania hello TransformationID oświadczeń schematu wejścia. Ta wartość musi być unikatowa dla każdego wpisu transformacji w ramach tych zasad.

**TransformationMethod:** identyfikuje hello TransformationMethod element operacji, które jest wykonywane toogenerate hello danych hello oświadczenia.

Oparte na wybranej metody hello, oczekiwano zestaw danych wejściowych i wyjściowych. Są one zdefiniowane przy użyciu hello **InputClaims**, **InputParameters** i **OutputClaims** elementów.

#### <a name="table-4-transformation-methods-and-expected-inputs-and-outputs"></a>Tabela 4: Metody przekształcania, a oczekiwano wejścia i wyjścia
|TransformationMethod|Oczekiwano danych wejściowych|Oczekiwane dane wyjściowe|Opis|
|-----|-----|-----|-----|
|Join|ciąg1, ciąg2, separatora|outputClaim|Sprzężenia Wprowadź ciągi za pomocą separatora między nimi. Na przykład: ciąg1: "foo@bar.com", ciąg2: "piaskownicy", separatora: "." powoduje outputClaim: "foo@bar.com.sandbox"|
|ExtractMailPrefix|Poczty|outputClaim|Wyodrębnia hello lokalną część adresu e-mail. Na przykład: poczty: "foo@bar.com" powoduje outputClaim: "foo". Jeśli nr @ znak jest obecny, następnie ciąg wejściowy orignal hello jest zwracany, ponieważ jest.|

**InputClaims:** użyć InputClaims elementu toopass hello danych z transformację tooa oświadczeń schematu wejścia. Zawiera dwa atrybuty: **ClaimTypeReferenceId** i **TransformationClaimType**.

- **ClaimTypeReferenceId** jest połączony z identyfikator elementu hello oświadczeń schematu wpisu toofind hello odpowiednich oświadczeń przychodzących. 
- **TransformationClaimType** jest używane toogive wprowadzania toothis unikatową nazwę. Ta nazwa musi być zgodna jedno z wejść hello Oczekiwano metody przekształcania hello.

**InputParameters:** Użyj toopass element InputParameters transformację tooa stałej wartości. Zawiera dwa atrybuty: **wartość** i **identyfikator**.

- **Wartość** jest przekazywany hello toobe rzeczywistej wartości stałej.
- **Identyfikator** jest używane toogive wprowadzania toothis unikatową nazwę. Ta nazwa musi być zgodna jedno z wejść hello Oczekiwano metody przekształcania hello.

**OutputClaims:** OutputClaims elementu toohold hello dane generowane przez transformację przy użyciu, a powiązanie jej tooa oświadczeń schematu wejścia. Zawiera dwa atrybuty: **ClaimTypeReferenceId** i **TransformationClaimType**.

- **ClaimTypeReferenceId** jest połączony z hello identyfikator oświadczeń wychodzących odpowiednie hello toofind wpis hello oświadczeń schematu.
- **TransformationClaimType** jest używane toogive wyjściowego toothis unikatową nazwę. Ta nazwa musi pasować wyjść hello Oczekiwano metody przekształcania hello.

### <a name="exceptions-and-restrictions"></a>Wyjątki i ograniczenia

**SAML NameID i UPN:** hello atrybutów, z których źródła hello NameID i UPN wartości i hello oświadczeń przekształcenia, które są dozwolone, są ograniczone.

#### <a name="table-5-attributes-allowed-as-a-data-source-for-saml-nameid"></a>Tabela 5: Atrybuty dozwolone jako źródło danych dla SAML NameID
|Element źródłowy|ID|Opis|
|-----|-----|-----|
|Użytkownik|Poczty|Adres e-mail|
|Użytkownik|userPrincipalName|Główna nazwa użytkownika|
|Użytkownik|onpremisessamaccountname|Dla nazwy konta Sam lokalne|
|Użytkownik|Identyfikator pracownika|Identyfikator pracownika|
|Użytkownik|extensionattribute1|Atrybut rozszerzenia 1|
|Użytkownik|extensionattribute2|Atrybut rozszerzenia 2|
|Użytkownik|extensionattribute3|Atrybut rozszerzenia 3|
|Użytkownik|extensionattribute4|Atrybut rozszerzenia 4|
|Użytkownik|extensionattribute5|Atrybut rozszerzenia 5|
|Użytkownik|extensionattribute6|Atrybut rozszerzenia 6|
|Użytkownik|extensionattribute7|Atrybut rozszerzenia 7|
|Użytkownik|extensionattribute8|Atrybut rozszerzenia 8|
|Użytkownik|extensionattribute9|Atrybut rozszerzenia 9|
|Użytkownik|extensionattribute10|Atrybut rozszerzenia 10|
|Użytkownik|extensionattribute11|Atrybut rozszerzenia 11|
|Użytkownik|extensionattribute12|Atrybut rozszerzenia 12|
|Użytkownik|extensionattribute13|Atrybut rozszerzenia 13|
|Użytkownik|extensionattribute14|Atrybut rozszerzenia 14|
|Użytkownik|extensionattribute15|Atrybut rozszerzenia 15|

#### <a name="table-6-transformation-methods-allowed-for-saml-nameid"></a>Tabela 6: Metody przekształcania dozwolony dla SAML NameID
|TransformationMethod|Ograniczenia|
| ----- | ----- |
|ExtractMailPrefix|Brak|
|Join|sufiks Hello jest dołączony musi być zweryfikowanej domeny hello zasobów dzierżawy.|

### <a name="custom-signing-key"></a>Niestandardowe klucza podpisywania
Niestandardowy klucz podpisujący musi być przypisany toohello obiekt główny usługi dla mapowania efekt tootake zasad oświadczeń. Wszystkie wystawione tokeny, które wpływ zasad hello są podpisane przy użyciu tego klucza. Aplikacje muszą być skonfigurowane tooaccept tokeny podpisane przy użyciu tego klucza. Dzięki temu potwierdzenia, że tokeny zostały zmodyfikowane przez hello twórca hello oświadczeń zasady mapowania. Chroni to aplikacje z oświadczeń mapowanie zasad utworzonych przez złośliwych osób.

### <a name="cross-tenant-scenarios"></a>Scenariusze między dzierżawy
Mapowanie zasad oświadczeń nie należy stosować tooguest użytkowników. Jeśli użytkownik-Gość prób tooaccess aplikacji z oświadczeń tooits zasad przypisanych mapowanie usługi podmiot zabezpieczeń, hello domyślny token wystawiony (hello zasada nie ma znaczenia).

## <a name="claims-mapping-policy-assignment"></a>Mapowanie przypisania zasad oświadczeń
Wskazuje, że mapowania zasad można przypisać tylko obiekty główne tooservice.

### <a name="example-claims-mapping-policies"></a>Przykład oświadczeń mapowania zasad

W usłudze Azure AD wiele scenariuszy współbieżnie, gdy można dostosować oświadczeń wysyłanego w tokenach podmiotów określonej usługi. W tej sekcji możemy przeprowadzenie kilka typowych scenariuszy, które mogą pomóc Ci ujmij jak toouse hello oświadczeń mapowania typu zasad.

#### <a name="prerequisites"></a>Wymagania wstępne
Następujące przykłady hello służy do tworzenia, aktualizacji, łączenie i usuwania zasad dla nazwy główne usług. W przypadku nowych tooAzure AD zalecamy Poznaj jak tooget usługi Azure AD dzierżawy przed przystąpieniem do tych przykładów. 

tooget pracę, hello następujące kroki:


1. Pobierz najnowsze hello [modułu Azure AD PowerShell publicznej wersji zapoznawczej](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.127).
2.  Uruchom toosign polecenia Connect hello w tooyour konta administratora usługi Azure AD. Uruchom to polecenie za każdym razem, należy uruchomić nową sesję.
    
     ``` powershell
    Connect-AzureAD -Confirm
    
    ```
3.  toosee wszystkie zasady, które zostały utworzone w organizacji, hello uruchom następujące polecenie. Firma Microsoft zaleca uruchomienie tego polecenia po większości operacji w hello następujących scenariuszy, oczekiwano toocheck, które zasady są tworzone jako.
   
    ``` powershell
        Get-AzureADPolicy
    
    ```
#### <a name="example-create-and-assign-a-policy-tooomit-hello-basic-claims-from-tokens-issued-tooa-service-principal"></a>Przykład: Utworzyć i przypisać zasady tooomit hello podstawowe oświadczeń z nazwy głównej usługi tooa tokeny wystawione.
W tym przykładzie utworzyć zasadę, która usuwa zestaw oświadczeń podstawowe hello z tokenów wystawionych toolinked nazwy główne usług.


1. Utwórz mapowania zasad oświadczeń. Ta zasada, połączone toospecific nazwy główne usług, usuwa zestaw oświadczeń podstawowe hello z tokenów.
    1. toocreate hello zasad, uruchom to polecenie: 
    
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"false"}}') -DisplayName "OmitBasicClaims” -Type "ClaimsMappingPolicy"
    ```
    2. toosee, które nowe zasady, a zasady hello tooget ObjectId, hello uruchom następujące polecenie:
    
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Przypisz hello zasad tooyour service principal. Należy również hello tooget ObjectId Twojej nazwy głównej usługi. 
    1.  toosee nazwy główne usług wszystkich organizacji, można zbadać Microsoft Graph. Lub, w Eksploratorze Azure AD Graph Zaloguj tooyour konto usługi Azure AD.
    2.  Jeśli masz hello ObjectId Twojej usługi głównej, uruchom hello następujące polecenie:  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-tooinclude-hello-employeeid-and-tenantcountry-as-claims-in-tokens-issued-tooa-service-principal"></a>Przykład: Utwórz i przypisz tooinclude zasad hello identyfikator pracownika i TenantCountry oświadczenia w tokenach wystawianych tooa nazwy głównej usługi.
W tym przykładzie należy utworzyć zasadę, która dodaje hello identyfikator pracownika i TenantCountry tootokens wystawiony toolinked nazwy główne usług. Identyfikator pracownika Hello jest emitowany jako typ oświadczenia nazwy hello zarówno tokeny SAML i tokenów Jwt. Witaj TenantCountry jest emitowany jako typ zarówno tokeny SAML i tokenów Jwt oświadczenia hello kraju. W tym przykładzie w dalszym ciągu tooinclude hello podstawowe oświadczenia w tokenach hello.

1. Utwórz mapowania zasad oświadczeń. Ta zasada toospecific połączonej nazwy główne usług, dodaje hello identyfikator pracownika i TenantCountry tootokens oświadczeń.
    1. toocreate hello zasad, uruchom to polecenie:  
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema": [{"Source":"user","ID":"employeeid","SamlClaimType":"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name","JwtClaimType":"name"},{"Source":"company","ID":" tenantcountry ","SamlClaimType":" http://schemas.xmlsoap.org/ws/2005/05/identity/claims/country ","JwtClaimType":"country"}]}}') -DisplayName "ExtraClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. toosee, które nowe zasady, a zasady hello tooget ObjectId, hello uruchom następujące polecenie:
     
     ``` powershell  
    Get-AzureADPolicy
    ```
2.  Przypisz hello zasad tooyour service principal. Należy również hello tooget ObjectId Twojej nazwy głównej usługi. 
    1.  toosee nazwy główne usług wszystkich organizacji, można zbadać Microsoft Graph. Lub, w Eksploratorze Azure AD Graph Zaloguj tooyour konto usługi Azure AD.
    2.  Jeśli masz hello ObjectId Twojej usługi głównej, uruchom hello następujące polecenie:  
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
#### <a name="example-create-and-assign-a-policy-that-uses-a-claims-transformation-in-tokens-issued-tooa-service-principal"></a>Przykład: Utworzyć i przypisać zasady, która używa nazwy głównej usługi tooa tokenów wystawionych przekształcania oświadczeń.
W tym przykładzie utworzysz zasady, które emituje oświadczenia niestandardowego "JoinedData" czy tooJWTs wystawiony toolinked nazwy główne usług. To oświadczenie zawiera wartość powstały hello danych przechowywanych w hello extensionattribute1 atrybutu dla obiektu użytkownika hello o ".sandbox". W tym przykładzie Wyłączamy hello oświadczeń podstawowe w hello tokenów.


1. Utwórz mapowania zasad oświadczeń. Ta zasada toospecific połączonej nazwy główne usług, dodaje hello identyfikator pracownika i TenantCountry tootokens oświadczeń.
    1. toocreate hello zasad, uruchom to polecenie: 
     
     ``` powershell
    New-AzureADPolicy -Definition @('{"ClaimsMappingPolicy":{"Version":1,"IncludeBasicClaimSet":"true", "ClaimsSchema":[{"Source":"user","ID":"extensionattribute1"},{"Source":"transformation","ID":"DataJoin","TransformationId":"JoinTheData","JwtClaimType":"JoinedData"}],"ClaimsTransformation":[{"ID":"JoinTheData","TransformationMethod":"Join","InputClaims":[{"ClaimTypeReferenceId":"extensionattribute1","TransformationClaimType":"string1"}], "InputParameters": [{"Id":"string2","Value":"sandbox"},{"Id":"separator","Value":"."}],"OutputClaims":[{"ClaimTypeReferenceId":"DataJoin","TransformationClaimType":"outputClaim"}]}]}}') -DisplayName "TransformClaimsExample” -Type "ClaimsMappingPolicy"
    ```
    
    2. toosee, które nowe zasady, a zasady hello tooget ObjectId, hello uruchom następujące polecenie: 
     
     ``` powershell
    Get-AzureADPolicy
    ```
2.  Przypisz hello zasad tooyour service principal. Należy również hello tooget ObjectId Twojej nazwy głównej usługi. 
    1.  toosee nazwy główne usług wszystkich organizacji, można zbadać Microsoft Graph. Lub, w Eksploratorze Azure AD Graph Zaloguj tooyour konto usługi Azure AD.
    2.  Jeśli masz hello ObjectId Twojej usługi głównej, uruchom hello następujące polecenie: 
     
     ``` powershell
    Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
    ```
