---
title: "aaaUnderstand zabezpieczeń Centrum IoT Azure | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera — jak toocontrol dostępu tooIoT Centrum dla aplikacji dla urządzeń i aplikacji zaplecza. Zawiera informacje na temat tokeny zabezpieczające i pomoc techniczna dla certyfikatów X.509."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 717726328a6bb5c5c334a123d0abfed711b2c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="control-access-tooiot-hub"></a>Kontrola dostępu tooIoT Centrum

W tym artykule opisano opcje hello zabezpieczania Centrum IoT. Centrum IoT używa *uprawnienia* punktu końcowego Centrum IoT toogrant dostępu tooeach. Uprawnienia ograniczyć hello dostępu tooan Centrum IoT oparta na funkcjach.

W tym artykule opisano:

* Witaj różne uprawnienia można przyznanie tooaccess zaplecza aplikacji lub urządzenia tooa Centrum IoT.
* Witaj tokeny proces i hello uwierzytelniania używa tooverify uprawnienia.
* Jak tooscope poświadczeń toolimit dostęp do toospecific zasobów.
* Obsługa Centrum IoT certyfikatów X.509.
* Urządzeń niestandardowych mechanizmów uwierzytelniania, korzystających z istniejących rejestrów tożsamość urządzenia lub schematy uwierzytelniania.

### <a name="when-toouse"></a>Gdy toouse

Musisz mieć odpowiednie uprawnienia tooaccess wszelkie punkty końcowe Centrum IoT hello. Na przykład urządzenie musi zawierać token zawierający poświadczenia zabezpieczeń, wraz z każdej wiadomości wysyła tooIoT koncentratora.

## <a name="access-control-and-permissions"></a>Kontrola dostępu i uprawnienia

Można przyznać [uprawnienia](#iot-hub-permissions) w hello następujące sposoby:

* **Zasady dostępu do udostępnionego Centrum IoT na poziomie**. Zasady dostępu współdzielonego, można przyznać dowolną kombinację [uprawnienia](#iot-hub-permissions). Zasady można definiować w hello [portalu Azure][lnk-management-portal], lub programowo, używając hello [interfejsy API REST dostawcy zasobów Centrum IoT][lnk-resource-provider-apis]. Nowo utworzone Centrum IoT ma hello następujące zasady domyślne:

  * **iothubowner**: zasady z wszystkie uprawnienia.
  * **Usługa**: zasady z **ServiceConnect** uprawnienia.
  * **urządzenie**: zasady z **DeviceConnect** uprawnienia.
  * **registryRead**: zasady z **RegistryRead** uprawnienia.
  * **registryReadWrite**: zasady z **RegistryRead** i RegistryWrite uprawnienia.
  * **Poświadczenia zabezpieczeń na urządzenie**. Zawiera każdego centrum IoT [rejestru tożsamości][lnk-identity-registry]. Dla każdego urządzenia w rejestrze tej tożsamości można skonfigurować poświadczenia zabezpieczeń, które przyznać **DeviceConnect** uprawnień zakresie punkty końcowe toohello odpowiednie urządzenie.

Na przykład w typowej rozwiązania IoT:

* składnika zarządzania urządzeniami Hello używa hello *registryReadWrite* zasad.
* składnik procesora zdarzeń Hello używa hello *usługi* zasad.
* składnika logiki biznesowej urządzenia środowiska wykonawczego Hello używa hello *usługi* zasad.
* Poszczególne urządzenia łączą, przy użyciu poświadczeń przechowywanych w rejestrze tożsamości Centrum IoT hello.

> [!NOTE]
> Zobacz [uprawnienia](#iot-hub-permissions) Aby uzyskać szczegółowe informacje.

## <a name="authentication"></a>Authentication

Centrum IoT Azure udziela dostępu tooendpoints weryfikując token przed hello udostępnionych zasady dostępu i poświadczenia zabezpieczeń rejestru tożsamości.

Poświadczenia zabezpieczeń, takie jak klucze symetryczne, nigdy nie są przesyłane przez sieć hello.

> [!NOTE]
> Witaj Centrum IoT Azure dostawcy zasobów jest chronione przy użyciu subskrypcji platformy Azure, są wszystkich dostawców w hello [usługi Azure Resource Manager][lnk-azure-resource-manager].

Aby uzyskać więcej informacji o tym, jak tooconstruct i używania tokenów zabezpieczających, zobacz [tokeny zabezpieczające Centrum IoT][lnk-sas-tokens].

### <a name="protocol-specifics"></a>Szczegóły protokołu

Każdy obsługiwanych protokołów, takich jak MQTT, AMQP i HTTP, transport tokenów na różne sposoby.

Używając MQTT hello CONNECT pakiet ma hello deviceId jak hello ClientId, {iothubhostname} / {deviceId} hello pole nazwy użytkownika i tokenu sygnatury dostępu Współdzielonego, w polu hasła hello. {iothubhostname} powinna hello pełne CName z Centrum IoT hello (na przykład devices.net contoso.azure).

Korzystając z [AMQP][lnk-amqp], obsługuje Centrum IoT [zwykły SASL] [ lnk-sasl-plain] i [AMQP oświadczenia na podstawie-zabezpieczeń] [ lnk-cbs].

Jeśli używasz protokołu AMQP oświadczenia na podstawie — zabezpieczeń, określa hello standardowe jak tootransmit tych tokenów.

Dla zwykłego SASL hello **username** może być:

* `{policyName}@sas.root.{iothubName}`Jeśli przy użyciu tokenów poziomie Centrum IoT.
* `{deviceId}@sas.{iothubname}`Jeśli przy użyciu tokenów zakres urządzeń.

W obu przypadkach pole hasła hello zawiera hello token, zgodnie z opisem w [tokeny zabezpieczające Centrum IoT][lnk-sas-tokens].

HTTP wykonuje uwierzytelnianie przy tym nieprawidłowy token w hello **autoryzacji** nagłówek żądania.

#### <a name="example"></a>Przykład

Nazwa użytkownika (DeviceId jest rozróżniana wielkość liter):`iothubname.azure-devices.net/DeviceId`

Hasło (token Generowanie sygnatury dostępu Współdzielonego z hello [explorer urządzenia] [ lnk-device-explorer] narzędzie):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`

> [!NOTE]
> Witaj [Azure IoT SDK] [ lnk-sdks] automatycznie generować tokeny podczas łączenia toohello usługi. W niektórych przypadkach hello Azure IoT SDK nie obsługują wszystkie protokoły hello lub wszystkich metod uwierzytelniania hello.

### <a name="special-considerations-for-sasl-plain"></a>Uwagi dotyczące SASL zwykły

Korzystając z protokołu AMQP zwykły SASL, klienta nawiązującego połączenie tooan Centrum IoT można użyć jednego tokenu dla każdego połączenia TCP. Po wygaśnięciu tokenu hello hello połączenie TCP zakończy połączenie z usługą hello i wyzwala ponownego połączenia. To zachowanie, gdy nie powodować problemy dla aplikacji zaplecza, jest uszkodzenia aplikacji urządzenia dla hello z następujących powodów:

* Bramy ze łączyć imieniu wiele urządzeń. Przy użyciu zwykłego SASL, mają toocreate różne połączenia TCP dla każdego urządzenia łączenie tooan Centrum IoT. W tym scenariuszu znacznie zwiększa hello zużycia energii i zasobów sieciowych i zwiększa hello opóźnienie połączenia każdego urządzenia.
* Ograniczone zasobów urządzeń dotkną hello zwiększone użycie tooreconnect zasobów po każdym wygaśnięcia tokenu.

## <a name="scope-iot-hub-level-credentials"></a>Zakres poświadczeń na poziomie Centrum IoT

Zakres zasad zabezpieczeń na poziomie Centrum IoT można określić, tworząc tokenów z ograniczeniami identyfikator URI zasobu. Na przykład wiadomości powitania od punktu końcowego toosend urządzenia do chmury przy użyciu urządzenia jest **/devices/ {deviceId} / wiadomości/zdarzenia**. Można także użyć zasady dostępu współdzielonego z poziomu Centrum IoT z **DeviceConnect** toosign uprawnienia tokenu, w których resourceURI jest **/devices/ {deviceId}**. Ta metoda tworzy token, który jest tylko komunikaty toosend można używać w imieniu urządzenia **deviceId**.

Mechanizm ten jest podobny toohello [zasad wydawcy usługi Event Hubs][lnk-event-hubs-publisher-policy]i umożliwia tooimplement niestandardowe metody uwierzytelniania.

## <a name="security-tokens"></a>Tokeny zabezpieczające

Centrum IoT używa zabezpieczeń tokeny tooauthenticate urządzeń i usług tooavoid wysyłania kluczy umieszczonego hello. Ponadto tokeny zabezpieczające są ograniczone w czas ważności i zakres. [Zestawy Azure SDK IoT] [ lnk-sdks] automatycznie generować tokeny bez konieczności żadnej specjalnej konfiguracji. Niektóre scenariusze wymaga toogenerate i korzystać bezpośrednio tokenów zabezpieczających. Takie scenariusze obejmują:

* Witaj bezpośredniego użycia hello powierzchni MQTT AMQP i HTTP.
* Witaj implementacji wzorca usługi tokenu hello, zgodnie z objaśnieniem w [uwierzytelnianie urządzenia niestandardowe][lnk-custom-auth].

Centrum IoT umożliwia również tooauthenticate urządzenia z Centrum IoT przy użyciu [certyfikatów X.509][lnk-x509].

### <a name="security-token-structure"></a>Struktura tokenu zabezpieczeń

Należy używać zabezpieczeń tokeny toogrant ograniczonym czasie dostępu usługi i toodevices toospecific funkcji w Centrum IoT. tooget autoryzacji tooconnect tooIoT koncentratora, urządzeń i usług musi wysyłanie tokenów zabezpieczających, podpisany dostępu współdzielonego lub klucza symetrycznego. Klucze te są przechowywane za pomocą tożsamości urządzenia w rejestrze tożsamości hello.

Podpisany token dostępu współdzielonego przyznaje klucza dostępu tooall hello funkcji skojarzonych z uprawnieniami zasad dostępu hello udostępnionych. Podpisany token hello symetrycznego klucza przyznaje tylko urządzenia tożsamości **DeviceConnect** uprawnienie hello skojarzone tożsamości urządzenia.

token zabezpieczający Hello ma hello następującego formatu:

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

Poniżej przedstawiono hello oczekiwanych wartości:

| Wartość | Opis |
| --- | --- |
| {sygnatury} |Ciąg HMAC SHA256 podpisu formularza hello: `{URL-encoded-resourceURI} + "\n" + expiry`. **Ważne**: klucz hello jest zdekodować z formatu base64 i użyć jako klucza tooperform hello HMAC SHA256 obliczeń. |
| {resourceURI} |Prefiks identyfikatora URI (według segmentu) hello punktów końcowych, które mogą być udostępniane z tym tokenem, począwszy od nazwy hosta Centrum IoT hello (nie protocol). Na przykład: `myHub.azure-devices.net/devices/device1` |
| {wygaśnięcia} |Ciągi UTF8 liczbę sekund od czasu UTC 00:00:00 epoki hello na 1 stycznia 1970. |
| {URL-zakodowane resourceURI} |Małe przypadek kodowania adresów URL identyfikator URI zasobu małe litery hello |
| {policyName} |Nazwa Hello hello udostępnionego toowhich zasad dostępu, który odwołuje się ten token. Brak w przypadku hello token odwołuje się poświadczenia toodevice rejestru. |

**Uwaga na prefiksie**: Prefiks URI hello jest obliczana przez segment, a nie przez znak. Na przykład `/a/b` był prefiksem dla `/a/b/c` , ale nie dla `/a/bc`.

Witaj następujący fragment kodu Node.js zawiera funkcji o nazwie **generateSasToken** czy oblicza hello tokenu z wejść hello `resourceUri, signingKey, policyName, expiresInMins`. Hello kolejnych sekcjach szczegółowo opisano sposób tooinitialize hello różnych komponentów o inny token hello przypadki użycia.

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

Jako porównanie hello równoważne toogenerate kodu języka Python, który token zabezpieczający jest:

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> Ponieważ hello czas ważności tokenu hello jest weryfikowane na komputerach Centrum IoT, odejście hello zegara hello hello maszyny, które generuje hello token musi być minimalny.

### <a name="use-sas-tokens-in-a-device-app"></a>Używanie tokeny sygnatury dostępu Współdzielonego w aplikacji urządzeń

Istnieją dwa sposoby tooobtain **DeviceConnect** uprawnienia z Centrum IoT z tokenów zabezpieczających: Użyj [klucza symetrycznego urządzenia z rejestru tożsamości hello](#use-a-symmetric-key-in-the-identity-registry), lub użyj [udostępniony klucz dostępu](#use-a-shared-access-policy).

Należy pamiętać, że wszystkie funkcje dostępne z urządzeń jest udostępniany przez projekt w punktach końcowych z prefiksem `/devices/{deviceId}`.

> [!IMPORTANT]
> Jedynym sposobem Hello, że Centrum IoT uwierzytelnia określonego urządzenia używa hello klucza symetrycznego tożsamości urządzenia. W przypadkach, gdy zasady dostępu współdzielonego jest używane tooaccess funkcjonalności, hello rozwiązania należy wziąć pod uwagę wystawiania tokenu zabezpieczającego hello jako zaufany podskładnika składnika hello.

punkty końcowe skierowane do urządzenia Hello są (niezależnie od protokołu hello):

| Endpoint | Funkcjonalność |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |Wysyłanie wiadomości urządzenia do chmury. |
| `{iot hub host name}/devices/{deviceId}/devicebound` |Komunikaty chmury do urządzenia. |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a>Użyj klucza symetrycznego w rejestrze tożsamości hello

Podczas korzystania z urządzenia tożsamości toogenerate klucza symetrycznego token, hello Nazwa_zasady (`skn`) element hello token zostanie pominięty.

Na przykład token utworzony tooaccess wszystkie funkcje urządzenia powinien mieć hello następujące parametry:

* Identyfikator URI zasobu: `{IoT hub name}.azure-devices.net/devices/{device id}`,
* Klucz podpisujący: dowolnego klucza symetrycznego dla hello `{device id}` tożsamości,
* Brak nazwy zasad
* wszelkie czas wygaśnięcia.

Przykładem przy użyciu hello poprzedzających funkcja Node.js może być:

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

Witaj, zapewniającej dostęp do funkcji tooall device1 nastąpiłoby:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> Jego jest możliwe toogenerate token sygnatury dostępu Współdzielonego przy użyciu platformy .NET hello [explorer urządzenia] [ lnk-device-explorer] narzędzie lub hello i platform, na podstawie węzła [explorer Centrum iothub] [ lnk-iothub-explorer] narzędzia wiersza polecenia.

### <a name="use-a-shared-access-policy"></a>Użyj zasad dostępu współdzielonego

Podczas tworzenia tokenu z zasad dostępu współdzielonego, ustaw hello `skn` pole Nazwa toohello hello zasad. Ta zasada musi udzielić hello **DeviceConnect** uprawnienia.

Witaj dwa główne scenariusze korzystania z funkcji urządzenia tooaccess zasady dostępu współdzielonego są:

* [chmury bramy protokołu][lnk-endpoints],
* [token usługi] [ lnk-custom-auth] używane tooimplement schematy uwierzytelniania niestandardowego.

Od hello zasady dostępu współdzielonego może potencjalnie przyznanie dostępu tooconnect jako dowolnego urządzenia podczas tworzenia tokenów zabezpieczających jest ważne toouse hello poprawne zasobów identyfikatora URI. To ustawienie jest szczególnie ważne w przypadku tokenów usług, które mają tooscope hello token tooa określonego urządzenia przy użyciu identyfikatora URI zasobu hello. Ten punkt jest mniej istotne dla bramy protokołu, ponieważ są one już pośredniczących ruchu dla wszystkich urządzeń.

Na przykład usługi tokenu przy użyciu wstępnie utworzonej hello udostępnionych zasady dostępu o nazwie **urządzenia** utworzyć token z hello następujące parametry:

* Identyfikator URI zasobu: `{IoT hub name}.azure-devices.net/devices/{device id}`,
* Klucz podpisujący: jeden z kluczy hello hello `device` zasad,
* Nazwa zasad: `device`,
* wszelkie czas wygaśnięcia.

Przykładem przy użyciu hello poprzedzających funkcja Node.js może być:

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

Witaj, zapewniającej dostęp do funkcji tooall device1 nastąpiłoby:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

Brama protokołu można użyć hello token takie same dla wszystkich urządzeń, wystarczy wybrać ustawienie zbyt hello identyfikator URI zasobu`myhub.azure-devices.net/devices`.

### <a name="use-security-tokens-from-service-components"></a>Używaj tokenów zabezpieczeń z składniki usługi

Składniki usługi można generować tylko tokeny zabezpieczające, za pomocą zasad dostępu współdzielonego udzielanie hello odpowiednie uprawnienia, zgodnie z objaśnieniem wcześniej.

Poniżej przedstawiono funkcje usługi hello narażone na powitania punktów końcowych:

| Endpoint | Funkcjonalność |
| --- | --- |
| `{iot hub host name}/devices` |Tworzenie, aktualizowanie, pobrać i usuwania tożsamości urządzenia. |
| `{iot hub host name}/messages/events` |Komunikaty urządzenia do chmury. |
| `{iot hub host name}/servicebound/feedback` |Otrzymasz opinię komunikatów chmury do urządzenia. |
| `{iot hub host name}/devicebound` |Wysyłanie wiadomości chmury do urządzenia. |

Na przykład usługi generowania przy użyciu wstępnie utworzonej hello udostępnionych zasady dostępu o nazwie **registryRead** utworzyć token z hello następujące parametry:

* Identyfikator URI zasobu: `{IoT hub name}.azure-devices.net/devices`,
* Klucz podpisujący: jeden z kluczy hello hello `registryRead` zasad,
* Nazwa zasad: `registryRead`,
* wszelkie czas wygaśnięcia.

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

wynik Hello, którym przyznano dostęp tooread wszystkich tożsamości urządzenia, będzie:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a>Obsługiwane certyfikaty X.509

Można użyć dowolnego tooauthenticate certyfikatu X.509 urządzenie z Centrum IoT. Certyfikaty obejmują:

* **Istniejący certyfikat X.509**. Urządzenie może już być skojarzone z nim certyfikatu X.509. Witaj urządzenie może używać tego certyfikatu tooauthenticate z Centrum IoT.
* **A własnym wygenerowany i X-509 certyfikat z podpisem własnym**. Producenta urządzenia lub wewnętrznych narzędzia wdrażania można wygenerować tych certyfikatów i przechowywać hello odpowiadające im klucze prywatne (i certyfikatu) na urządzeniu hello. Można użyć narzędzia, takie jak [OpenSSL] [ lnk-openssl] i [Windows SelfSignedCertificate] [ lnk-selfsigned] narzędzie do tego celu.
* **Podpisany przez urząd certyfikacji certyfikatu X.509**. tooidentify urządzenia oraz uwierzytelniania go z Centrum IoT, można użyć certyfikatu X.509 wygenerowany i podpisany przez urząd certyfikacji (CA). Centrum IoT sprawdza tylko tym palca hello przedstawione zgodny z odciskiem palca hello skonfigurowane. Centrum IotHub nie można zweryfikować łańcucha certyfikatów hello.

Urządzenie może użyć certyfikatu X.509 lub tokenu zabezpieczającego dla uwierzytelniania, ale nie oba.

### <a name="register-an-x509-certificate-for-a-device"></a>Zarejestruj certyfikat X.509 dla urządzenia

Witaj [Azure IoT usługi SDK dla języka C#] [ lnk-service-sdk] (wersja 1.0.8+) obsługuje rejestrowanie urządzenia, który używa certyfikatu X.509 do uwierzytelniania. Innych interfejsów API, takich jak importu/eksportu urządzeń obsługuje także certyfikaty X.509.

### <a name="c-support"></a>C\# pomocy technicznej

Witaj **RegistryManager** klasa udostępnia tooregister sposób programowy urządzenia. W szczególności hello **AddDeviceAsync** i **UpdateDeviceAsync** metody umożliwiają tooregister i zaktualizować urządzenie w hello rejestru tożsamości Centrum IoT. Te dwie metody przyjmują **urządzenia** wystąpienia jako dane wejściowe. Witaj **urządzenia** klasa zawiera **uwierzytelniania** właściwość, która umożliwia toospecify podstawowych i pomocniczych X.509 odciski palców certyfikatu. Odcisk palca Hello reprezentuje wartości skrótu SHA-1 certyfikatu X.509 hello (przechowywane przy użyciu kodowania binarnego DER). Masz hello możliwość określenia podstawowego odcisk palca lub dodatkowej odcisk palca lub oba. Odciski palców podstawowych i pomocniczych są obsługiwane toohandle certyfikatu przerzucania scenariuszy.

> [!NOTE]
> Centrum IoT nie wymagają lub zapisać całą hello X.509 certyfikatu, tylko hello odcisk palca.

Poniżej przedstawiono przykładowe C\# kodu tooregister fragment urządzenia przy użyciu certyfikatu X.509:

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a>Użyj certyfikatu X.509 podczas operacji w czasie wykonywania

Witaj [urządzenia Azure IoT SDK dla platformy .NET] [ lnk-client-sdk] (wersja 1.0.11+) obsługuje hello przy użyciu certyfikatów X.509.

### <a name="c-support"></a>C\# pomocy technicznej

Witaj klasy **DeviceAuthenticationWithX509Certificate** obsługuje hello tworzenie **DeviceClient** wystąpienia za pomocą certyfikatu X.509. Certyfikat X.509 Hello musi być w formacie PFX (nazywany również PKCS #12) hello, który zawiera klucz prywatny hello.

Oto fragment kodu próbki:

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a>Uwierzytelnianie urządzeń niestandardowych

Można użyć hello Centrum IoT [rejestru tożsamości] [ lnk-identity-registry] dostępu i poświadczenia zabezpieczeń na urządzenie tooconfigure można kontrolować przy użyciu [tokenów] [ lnk-sas-tokens] . Jeśli rozwiązania IoT już schemat rejestru i/lub uwierzytelnianie tożsamości niestandardowej, należy rozważyć utworzenie *token usługi* toointegrate tej infrastruktury z Centrum IoT. W ten sposób można użyć innych funkcji IoT w rozwiązaniu.

Token usługi to usługa w chmurze niestandardowych. Używa Centrum IoT *udostępnionych zasad dostępu* z **DeviceConnect** toocreate uprawnienia *zakres urządzeń* tokenów. Tokeny te umożliwiają Centrum IoT tooyour tooconnect urządzenia.

![Kroki hello usługi tokenu wzorca][img-tokenservice]

Oto główne kroki hello hello usługi tokenu wzorca:

1. Tworzenie zasad dostępu do udostępnionego Centrum IoT z **DeviceConnect** uprawnienia Centrum IoT. Te zasady można tworzyć w hello [portalu Azure] [ lnk-management-portal] lub programowo. Hello usługi tokenu używa tej zasady tokeny hello toosign tworzonego.
1. Gdy urządzenie musi tooaccess Centrum IoT, żądań podpisany token z usługą tokenu. Hello urządzenia mogą uwierzytelniać za pomocą tożsamości urządzenia hello toodetermine schemat tożsamość niestandardowa rejestru/uwierzytelniania używany toocreate hello token hello usługi tokenu.
1. Usługa tokenu Hello zwraca token. Witaj token jest tworzona przy użyciu `/devices/{deviceId}` jako `resourceURI`, z `deviceId` jako urządzenie hello jest uwierzytelniane. Usługa tokenu Hello używa hello dostępu współdzielonego zasad tooconstruct hello tokenu.
1. Witaj urządzenie używa tokenu hello bezpośrednio z Centrum IoT hello.

> [!NOTE]
> Można użyć klasy .NET hello [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] lub hello Klasa Java [IotHubServiceSasToken] [ lnk-java-sas] toocreate tokenu w usłudze tokenu.

Usługa tokenu Hello można ustawić wygaśnięcia tokenu hello zgodnie z potrzebami. Po wygaśnięciu tokenu hello Centrum IoT hello serwery hello połączenie z urządzeniem. Następnie hello urządzenia należy zażądać nowego tokenu z usługi tokenu hello. Czas wygaśnięcia krótki zwiększa obciążenie hello hello urządzeniu i na powitania usługi tokenu.

Dla koncentratora tooyour tooconnect urządzenia, należy nadal go dodać toohello rejestru tożsamości Centrum IoT — mimo że hello urządzenie korzysta z tokenu i nie tooconnect klucza urządzenia. W związku z tym można kontynuować kontroli dostępu na urządzeniu toouse przez włączenie lub wyłączenie tożsamości urządzenia w hello [rejestru tożsamości][lnk-identity-registry]. Takie podejście zmniejsza ryzyko hello używania tokenów z wygaśnięcia długi czas.

### <a name="comparison-with-a-custom-gateway"></a>Porównanie z bramą niestandardowych

Wzorzec usługi tokenu Hello jest hello zalecany sposób tooimplement schemat rejestru/uwierzytelniania tożsamość niestandardowa z Centrum IoT. Ten wzorzec jest zalecane, ponieważ Centrum IoT nadal toohandle większość hello rozwiązania ruchu. Jednak jeśli schemat uwierzytelniania niestandardowego hello więc jest sprzężony z protokołem hello, mogą wymagać *bram* tooprocess wszystkie hello ruchu. Przykładem takiej sytuacji jest przy użyciu[zabezpieczeń TLS (Transport Layer) i kluczy wstępnych (PSKs)][lnk-tls-psk]. Aby uzyskać więcej informacji, zobacz hello [bramy protokołu] [ lnk-protocols] tematu.

## <a name="reference-topics"></a>Tematy odwołań:

Witaj następujące tematy dokumentacji zapewniają więcej informacji na temat kontrolowania dostępu tooyour IoT hub.

## <a name="iot-hub-permissions"></a>Centrum IoT uprawnień

Witaj Poniższa tabela zawiera listę uprawnień hello można użyć Centrum IoT tooyour dostępu toocontrol.

| Uprawnienie | Uwagi |
| --- | --- |
| **RegistryRead** |Przyznaje dostęp do odczytu toohello tożsamości rejestru. Aby uzyskać więcej informacji, zobacz [rejestru tożsamości][lnk-identity-registry]. <br/>To uprawnienie jest używany przez usługi w chmurze zaplecza. |
| **RegistryReadWrite** |Udziela dostępu odczytu i zapisu toohello rejestrze tożsamości. Aby uzyskać więcej informacji, zobacz [rejestru tożsamości][lnk-identity-registry]. <br/>To uprawnienie jest używany przez usługi w chmurze zaplecza. |
| **ServiceConnect** |Przyznaje dostęp komunikacji usługi połączonej toocloud i monitorowania punktów końcowych. <br/>Przyznaje uprawnienia tooreceive urządzenia do chmury wiadomości wysyłania wiadomości chmury do urządzenia i pobrać hello odpowiadającego potwierdzeń dostarczenia. <br/>Przyznaje uprawnienia tooretrieve dostarczanie potwierdzeń pliku operacji przekazywania. <br/>Przyznaje uprawnienia tooaccess urządzenia twins tooupdate tagów i odpowiednie właściwości pobierania właściwości zgłoszone, a następnie uruchom zapytania. <br/>To uprawnienie jest używany przez usługi w chmurze zaplecza. |
| **DeviceConnect** |Udziela dostępu do punktów końcowych toodevice uwzględniającym. <br/>Przyznaje uprawnienia toosend urządzenia do chmury wiadomości i odbieranie wiadomości chmury do urządzenia. <br/>Przyznaje uprawnienia tooperform przekazywania pliku z urządzenia. <br/>Przyznaje uprawnienia tooreceive urządzenia potrzebne dwie właściwości powiadomień i aktualizacji urządzenia dwie właściwości zgłoszony. <br/>Przyznaje uprawnienia tooperform pliku operacji przekazywania. <br/>To uprawnienie jest używany przez urządzenia. |

## <a name="additional-reference-material"></a>Odwołanie dodatkowe materiały

Inne tematy referencyjne w hello Centrum IoT — przewodnik dewelopera obejmują:

* [Punkty końcowe Centrum IoT] [ lnk-endpoints] opisuje hello różnych punktów końcowych, które udostępnia każdego centrum IoT dla operacji zarządzania i środowiska wykonawczego.
* [Ograniczenia przepustowości i przydziały] [ lnk-quotas] opisuje przydziały hello i ograniczanie zachowań stosowane toohello usługi IoT Hub.
* [Zestawy Azure IoT urządzenia i usługi SDK] [ lnk-sdks] list hello języka różnych zestawów SDK, można użyć podczas opracowywania aplikacji usług i urządzeń, które współdziałają z Centrum IoT.
* [Język zapytań Centrum IoT] [ lnk-query] opisuje tooretrieve informacji z Centrum IoT temat zadań i twins urządzenia można używać języka kwerend hello.
* [Obsługa MQTT Centrum IoT] [ lnk-devguide-mqtt] zamieszczono więcej informacji o obsłudze Centrum IoT hello MQTT protokołu.

## <a name="next-steps"></a>Następne kroki

Teraz wiesz już, jak toocontrol uzyskują dostęp do Centrum IoT, może Cię zainteresować następujące tematy przewodnik dewelopera Centrum IoT hello:

* [Urządzenie twins toosynchronize stanu i konfiguracji][lnk-devguide-device-twins]
* [Wywoływanie metody bezpośrednio na urządzeniu][lnk-devguide-directmethods]
* [Planowanie zadań na wielu urządzeniach][lnk-devguide-jobs]

Jeśli chcesz tootry niektórych hello pojęcia opisane w tym artykule, mogą być zainteresowane hello następujące samouczki Centrum IoT:

* [Rozpoczynanie pracy z Centrum IoT Azure][lnk-getstarted-tutorial]
* [Jak komunikaty toosend chmury do urządzenia z Centrum IoT][lnk-c2d-tutorial]
* [Jak tooprocess Centrum IoT urządzenia do chmury wiadomości][lnk-d2c-tutorial]

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
