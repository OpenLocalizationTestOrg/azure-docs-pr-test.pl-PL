---
title: "aaaAzure obliczeniowe — rozszerzenie diagnostyczne systemu Linux | Dokumentacja firmy Microsoft"
description: "Jak tooconfigure hello metryki toocollect rozszerzenia diagnostycznych Linux Azure (LAD) i rejestrowanie zdarzeń z maszyn wirtualnych systemu Linux działających na platformie Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a>Użyj rozszerzenia diagnostycznych Linux toomonitor metryki i dzienniki

W tym dokumencie opisano w wersji 3.0 oraz nowszych z hello rozszerzenia diagnostyczne systemu Linux.

> [!IMPORTANT]
> Informacje o wersji 2.3 i starsze, zobacz [tego dokumentu](./classic/diagnostic-extension-v2.md).

## <a name="introduction"></a>Wprowadzenie

Hello rozszerzenia diagnostycznych Linux pomaga użytkownika monitorowanie hello kondycja maszyny wirtualnej systemu Linux uruchomiony w systemie Microsoft Azure. Ma hello następujące możliwości:

* Zbiera metryki wydajności systemu z hello maszyny Wirtualnej i zapisuje je w określonej tabeli w ramach konta magazynu wyznaczonego.
* Pobiera zdarzenia dziennika z syslog i przechowuje je w określonej tabeli w Witaj wyznaczone konta magazynu.
* Umożliwia użytkownikom toocustomize hello danych metryki, które są zbierane i przekazać.
* Umożliwia użytkownikom toocustomize hello syslog urządzeń i poziomy ważności zdarzeń, które są zbierane i przekazać.
* Umożliwia użytkownikom tooupload określony dziennik pliki tooa magazynu wyznaczonego tabeli.
* Obsługuje wysyłanie metryki i dziennik zdarzeń tooarbitrary EventHub punktów końcowych i formacie JSON obiekty BLOB w Witaj wyznaczone konta magazynu.

To rozszerzenie współpracuje z obu modeli wdrażania platformy Azure.

## <a name="installing-hello-extension-in-your-vm"></a>Instalowanie hello rozszerzenia w maszynie Wirtualnej

To rozszerzenie można włączyć za pomocą poleceń cmdlet programu Azure PowerShell hello skryptów wiersza polecenia platformy Azure i szablony wdrożenia usługi Azure. Aby uzyskać więcej informacji, zobacz [funkcji rozszerzenia](./extensions-features.md).

Witaj portalu Azure nie może być używane tooenable ani skonfigurować LAD 3.0. Zamiast tego instaluje i konfiguruje wersji 2.3. Wykresy portalu Azure i alerty pracować z danymi obie wersje hello rozszerzenia.

Te instrukcje instalacji i [do pobrania Przykładowa konfiguracja](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) LAD 3.0 można skonfigurować:

* Przechwytywanie i magazynu hello same metryki dostarczonych przez LAD 2.3;
* Przechwyć zbiór przydatne metryki systemu plików, nowe tooLAD 3.0;
* Przechwyć hello domyślnej syslog kolekcji włączane przez LAD 2.3;
* Włącz hello Azure portalu obsługi wykresów i alerty na metryki maszyny Wirtualnej.

do pobrania konfiguracji Hello jest tylko przykładowe; Zmodyfikuj go toosuit własnych potrzeb.

### <a name="prerequisites"></a>Wymagania wstępne

* **Agenta systemu Linux platformy Azure w wersji 2.2.0 lub nowszym**. Większość obrazów Galeria Linux maszyny Wirtualnej Azure zawierają wersję 2.2.7 lub nowszym. Uruchom `/usr/sbin/waagent -version` tooconfirm hello wersji zainstalowanej na powitania maszyny Wirtualnej. Jeśli hello maszyna wirtualna jest uruchomiona starszą wersję agenta gościa hello, wykonaj [tych instrukcji](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate go.
* **Interfejs wiersza polecenia platformy Azure**. [Konfigurowanie hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) środowiska na tym komputerze.
* Witaj wget polecenia, jeśli nie masz jeszcze go: Uruchom `sudo apt-get install wget`.
* Istniejącą subskrypcję platformy Azure i istniejącego magazynu konta w niej toostore hello danych.

### <a name="sample-installation"></a>Przykładowe instalacji

Wprowadź poprawne parametry hello na powitania pierwsze trzy wiersze, a następnie wykonaj ten skrypt jako katalogu głównego:

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

adres URL Hello hello Przykładowa konfiguracja i jego zawartość są toochange podmiotu. Pobierz kopię pliku JSON hello ustawienia portalu i dostosować go do potrzeb. Wszystkie szablony lub automatyzacji, który można skonstruować należy używać własną kopię zamiast pobierania zawsze tego adresu URL.

### <a name="updating-hello-extension-settings"></a>Aktualizowanie ustawień rozszerzenia hello

Po zmianie ustawienia publiczne lub chronione, na których je wdrożyć toohello maszyny Wirtualnej, uruchamiając hello tego samego polecenia. Zmiana niczego w ustawieniach hello hello zaktualizowane ustawienia są wysyłane toohello rozszerzenia. LAD ponowne załadowanie konfiguracji hello i uruchamia się ponownie.

### <a name="migration-from-previous-versions-of-hello-extension"></a>Migracja z poprzednich wersji rozszerzenia hello

Najnowsza wersja rozszerzenia hello Hello jest **3.0**. **Wszystkie starsze wersje (2.x) są przestarzałe i mogą być publikowane na wcześniejsze niż 31 lipca 2018**.

> [!IMPORTANT]
> To rozszerzenie wprowadzono istotne zmiany toohello konfiguracji hello rozszerzenia. Taka zmiana nastąpiła zabezpieczeń hello tooimprove rozszerzenia hello; w związku z tym zapewnienia zgodności z 2.x nie można wykonać konserwacji. Ponadto hello wydawcy rozszerzenia dla tego rozszerzenia jest inny niż hello wydawcy dla wersji 2.x hello.
>
> toomigrate z 2.x toothis nowa wersja rozszerzenia hello, należy odinstalować rozszerzenia starego hello (w obszarze hello starej nazwy wydawcy), a następnie zainstaluj w wersji 3 hello rozszerzenia.

Zalecenia:

* Uaktualnianie wersji pomocniczej automatyczne włączone, należy zainstalować rozszerzenie hello.
  * W klasycznym modelu wdrażania maszyn wirtualnych należy określić "3.*" jako wersja hello instalowania rozszerzenia hello za pośrednictwem interfejsu wiersza polecenia XPLAT platformy Azure lub programu Powershell.
  * We wdrożeniu usługi Azure Resource Manager modelu maszyn wirtualnych, obejmują ""autoUpgradeMinorVersion": true" w szablonie wdrożenia maszyny Wirtualnej hello.
* Użyj nowego/innego konta magazynu dla LAD 3.0. Istnieje kilka małych niezgodności między LAD 2.3 i LAD 3.0 powodujących, że udostępnianie powodującymi konta:
  * LAD 3.0 przechowuje zdarzenia dziennika systemowego w tabeli z inną nazwą.
  * Witaj counterSpecifier ciągów dla `builtin` metryki różnią się w LAD 3.0.

## <a name="protected-settings"></a>Ustawienia chronionego

Ten zestaw informacji o konfiguracji zawiera poufne informacje, które powinny być chronione w widoku publicznych, na przykład poświadczenia magazynu. Te ustawienia są przesyłane tooand przechowywane przez rozszerzenie hello w postaci zaszyfrowanej.

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

Nazwa | Wartość
---- | -----
storageAccountName | Nazwa Hello hello konta magazynu, w którym dane są zapisywane przez rozszerzenie hello.
storageAccountEndPoint | identyfikowanie hello chmury, w których hello konto magazynu istnieje punkt końcowy hello (opcjonalnie). Jeśli to ustawienie jest nieobecne, LAD domyślnie toohello chmurze publicznej Azure `https://core.windows.net`. toouse konto magazynu platformy Azure w Niemczech, Azure dla instytucji rządowych lub chińskiej wersji platformy Azure, w związku z tym Ustaw tę wartość.
storageAccountSasToken | [Tokenu sygnatury dostępu Współdzielonego konta](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) usług obiektów Blob i tabeli (`ss='bt'`), odpowiednich toocontainers i obiektów (`srt='co'`), która przyznaje dodać, tworzenie listy, aktualizacji i uprawnienia do zapisu (`sp='acluw'`). Czy *nie* obejmują hello wiodące znak zapytania (?).
mdsdHttpProxy | (opcjonalnie) Informacje potrzebne serwera proxy HTTP tooenable toohello tooconnect rozszerzenia hello określone konto magazynu i punktu końcowego.
sinksConfig | (opcjonalnie) Szczegółowe informacje o alternatywnych miejsc docelowych toowhich metryki i zdarzenia mogą być dostarczane. Witaj szczegółowe informacje dotyczące każdego ujścia danych obsługiwane przez rozszerzenie hello zostały omówione w kolejnych sekcjach hello.

Można łatwo utworzyć hello wymagane tokenu sygnatury dostępu Współdzielonego za pośrednictwem portalu Azure hello.

1. Wybierz toowhich konta magazynu ogólnego przeznaczenia hello ma hello toowrite rozszerzenia
1. Wybierz opcję "Udostępniania sygnatury dostępu" z menu po lewej stronie powitania części ustawień hello
1. Wprowadź odpowiednie części hello, jak opisano wcześniej
1. Kliknij przycisk "Generowanie sygnatury dostępu Współdzielonego" hello.

![Obraz](./media/diagnostic-extension/make_sas.png)

Kopiuj hello wygenerowany SAS do pola storageAccountSasToken hello; Usuń znaku zapytania wiodące hello ("?").

### <a name="sinksconfig"></a>sinksConfig

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

Ta sekcja opcjonalna definiuje dodatkowe rozszerzenia hello toowhich wysyła informacje hello zebrane miejsc docelowych. Tablica "sink" Hello zawiera obiekt dla każdego obiektu sink dodatkowe dane. Określa atrybut "typ" hello innych atrybutów w obiekcie hello Hello.

Element | Wartość
------- | -----
name | Ciąg używany toorefer toothis ujścia innym miejscu w konfiguracji rozszerzenia hello.
type | Typ Hello definiowanego obiektu sink. Określa hello inne wartości (jeśli istnieją) w wystąpień tego typu.

Wersja 3.0 hello rozszerzenia diagnostycznych Linux obsługuje dwa typy zbiornika: EventHub i JsonBlob.

#### <a name="hello-eventhub-sink"></a>obiekt sink EventHub Hello

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

wpis "sasURL" Hello zawiera hello, który powinien zostać opublikowany, pełny adres URL, w tym tokenu sygnatury dostępu Współdzielonego dla hello danych toowhich Centrum zdarzeń. LAD wymaga sygnatury dostępu Współdzielonego nazewnictwa zasadę, która umożliwia hello wysyłania oświadczeń. Przykład:

* Tworzenie przestrzeni nazw usługi Event Hubs, o nazwie`contosohub`
* Tworzenie Centrum zdarzeń w przestrzeni nazw hello o nazwie`syslogmsgs`
* Tworzenie zasad dostępu współużytkowanego na powitania Centrum zdarzeń o nazwie `writer` czy umożliwia hello wysyłania oświadczeń

Jeśli utworzono sygnatury dostępu Współdzielonego dobra do północy czasu UTC 1 stycznia 2018 hello sasURL wartość może być:

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

Aby uzyskać więcej informacji na temat generowania tokeny sygnatury dostępu Współdzielonego usługi Event hubs, zobacz [tej strony sieci web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).

#### <a name="hello-jsonblob-sink"></a>obiekt sink JsonBlob Hello

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

Dane skierowane tooa JsonBlob ujście są przechowywane w obiekty BLOB w magazynie Azure. Każde wystąpienie LAD tworzy obiektu blob co godzinę dla każdej nazwy obiektu sink. Każdy obiekt blob jest zawsze zawiera nieprawidłową składnię tablicy JSON obiektu. Nowe wpisy są automatycznie dodawane toohello tablicy. Obiekty BLOB są przechowywane w kontenerze z hello takie same nazwy jako hello ujścia. Witaj zasady usługi Azure storage dla nazwy kontenera obiektów blob zastosować toohello nazwy wychwytywanie JsonBlob: od 3 do 63 małe znaki alfanumeryczne ASCII lub łączniki.

## <a name="public-settings"></a>Ustawienia publicznego

Ta struktura zawiera bloki różnych ustawień kontrolujących hello informacje zebrane przez rozszerzenie hello. Każde ustawienie jest opcjonalne. Jeśli określisz `ladCfg`, należy także określić `StorageAccount`.

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

Element | Wartość
------- | -----
Konto magazynu | Nazwa Hello hello konta magazynu, w którym dane są zapisywane przez rozszerzenie hello. Muszą być takie same nazwy, jak określono w hello hello [chronionych ustawień](#protected-settings).
mdsdHttpProxy | (opcjonalnie) Sam jak hello [chronionych ustawień](#protected-settings). wartość publicznego Hello jest zastępowany przez wartość prywatnego hello, jeśli ustawiona. Umieść ustawienia serwera proxy, które zawierają klucz tajny, takie jak hasła, w hello [chronionych ustawień](#protected-settings).

pozostałe elementy Hello są szczegółowo opisane w hello następujące sekcje.

### <a name="ladcfg"></a>ladCfg

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

Wychwytywanie tego opcjonalne struktury formanty hello zbierania metryk i dziennikach toohello dostarczania danych do usługi i tooother metryk usługi Azure. Należy określić `performanceCounters` lub `syslogEvents` lub oba. Należy określić hello `metrics` struktury.

Element | Wartość
------- | -----
eventVolume | (opcjonalnie) Formanty hello liczby partycji w tabeli magazynu hello utworzone. Musi mieć jedną z `"Large"`, `"Medium"`, lub `"Small"`. Jeśli nie zostanie określony, wartością domyślną hello jest `"Medium"`.
sampleRateInSeconds | (opcjonalnie) hello domyślny interwał między kolekcję pierwotnych metryki (unaggregated). częstotliwość próbkowania Hello najmniejsza obsługiwana jest 15 sekund. Jeśli nie zostanie określony, wartością domyślną hello jest `15`.

#### <a name="metrics"></a>metrics

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

Element | Wartość
------- | -----
resourceId | Identyfikator zasobu usługi Azure Resource Manager Hello hello maszyny Wirtualnej lub hello skalowania maszyny wirtualnej ustawić hello toowhich, do której należy maszyna wirtualna. To ustawienie musi być także określona, jeśli wszystkie zbiornika JsonBlob jest używane w konfiguracji hello.
scheduledTransferPeriod | częstotliwość Hello są agregacji metryki toobe obliczana i przekazywane tooAzure metryki, wyrażona jako czas jest 8601. okres transfer z najmniejszą Hello jest 60 sekund, czyli PT1M. Należy określić co najmniej jeden scheduledTransferPeriod.

Przykłady powitalne metryk określone w sekcji liczniki wydajności hello są gromadzone co 15 sekund lub częstotliwość próbkowania hello jawnie zdefiniowany dla licznika hello. Jeśli występuje wiele częstotliwości scheduledTransferPeriod (co w przykładzie hello), każdy agregacji jest obliczana niezależnie.

#### <a name="performancecounters"></a>liczniki wydajności

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

Ta sekcja opcjonalna steruje hello zbiór metryki. Przykłady pierwotnych są agregowane dla wszystkich [scheduledTransferPeriod](#metrics) tooproduce te wartości:

* Średnia
* Minimalna
* Maksymalna
* wartości zbierane przez ostatnie
* Liczba próbek pierwotnych używane toocompute hello agregacji

Element | Wartość
------- | -----
sink — obiekty | (opcjonalnie) Rozdzielana przecinkami lista nazw wychwytywanie toowhich wysyłanych LAD w zagregowanych wynikach metryki. Wszystkie metryki zagregowane są zbiornika tooeach opublikowane na liście. Zobacz [sinksConfig](#sinksconfig). Przykład: `"EHsink1, myjsonsink"`.
type | Określa dostawcę rzeczywiste hello hello metryki.
Klasy | Wraz z "licznika" identyfikuje hello określonej metryki w obszarze nazw hello dostawcy.
Licznik | Wraz z "class" identyfikuje hello określonej metryki w obszarze nazw hello dostawcy.
counterSpecifier | Identyfikuje hello określonej metryki w hello Azure metryki w obszarze nazw.
Warunek | (opcjonalnie) Stosuje określone wystąpienie hello obiektu toowhich hello metryki wybiera lub wybiera hello agregacji we wszystkich wystąpieniach tego obiektu. Aby uzyskać więcej informacji, zobacz hello [ `builtin` definicji metryk](#metrics-supported-by-builtin).
sampleRate | JEST interwałem 8601, która ustawia współczynnik hello pobierane pierwotnych próbek ta metryka. Jeśli nie jest ustawiona, hello kolekcji interwał jest ustawiany przez wartość hello [sampleRateInSeconds](#ladcfg). częstotliwość próbkowania obsługiwanych z najkrótszego Hello wynosi 15 sekund (PT15S).
jednostki | Powinien być jednym z tych ciągów: "Count", "B", "Seconds", "%", "CountPerSecond", "BytesPerSecond", "Milisekund". Definiuje jednostkę hello hello metryki. Konsumenci danych zebranych hello oczekiwać hello zbierane dane wartości toomatch tej jednostki. LAD są ignorowane w tym polu.
Nazwa wyświetlana | toobe etykiety (w języku hello określonego przez skojarzony ustawień regionalnych hello ustawienie) Hello dołączony toothis danych metryk usługi Azure. LAD są ignorowane w tym polu.

Hello counterSpecifier jest umownym identyfikatorem. Konsumenci metryk, takich jak hello wykresów portalu Azure i alerty funkcji, użyj counterSpecifier jako hello "klucza", który identyfikuje metrykę lub wystąpienia metryki. Aby uzyskać `builtin` metryki, zalecane jest użycie counterSpecifier wartości, które zaczynają się od `/builtin/`. Jeśli są zbierane konkretne wystąpienie metrykę, zaleca się Dołącz identyfikator hello hello wystąpienia toohello counterSpecifier wartości. Kilka przykładów:

* `/builtin/Processor/PercentIdleTime`-Bezczynności uśredniona wszystkich rdzeni
* `/builtin/Disk/FreeSpace(/mnt)`-Wolnego miejsca dla systemu plików z katalogu/mnt hello
* `/builtin/Disk/FreeSpace`— Wolne miejsce uśredniona wszystkie zainstalowane systemy plików

LAD ani hello portalu Azure oczekuje hello counterSpecifier wartość toomatch żadnych wzorca. Być zgodne w konstrukcji counterSpecifier wartości.

Po określeniu `performanceCounters`, LAD zawsze zapisuje tabeli tooa danych w magazynie Azure. Możesz można mieć hello takie same dane zapisane tooJSON obiekty BLOB i/lub centra zdarzeń, ale nie można wyłączyć zapisywanie tabeli tooa danych. Wszystkie wystąpienia toouse skonfigurowanego diagnostycznych rozszerzenia hello hello tego samego konta magazynu, nazwę i punktu końcowego, dodaj ich toohello metryki i dzienniki tej samej tabeli. Jeśli pisania zbyt wiele maszyn wirtualnych toohello, który można ograniczyć tej samej partycji tabeli, Azure zapisuje toothat partycji. ustawienie powoduje, że wpisy toobe eventVolume Hello rozmieszczenie do 1 (mała liczba godzin), 10 (średnia liczba godzin) lub 100 (duży) różnych partycji. Zwykle, "Medium" wystarcza nie jest ograniczany ruch sieciowy tooensure. Funkcja Azure metryki Hello hello portalu Azure wykorzystuje hello danych w tej tabeli tooproduce wykresy lub tootrigger alertów. Nazwa tabeli Hello jest złączeniem hello te ciągi:

* `WADMetrics`
* Witaj "scheduledTransferPeriod" dla hello zagregowane wartościami przechowywanymi w tabeli hello
* `P10DV2S`
* Data, w postaci hello "RRRRMMDD", która zmienia co 10 dni

Przykłady obejmują `WADMetricsPT1HP10DV2S20170410` i `WADMetricsPT1MP10DV2S20170609`.

#### <a name="syslogevents"></a>syslogEvents

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

Ta sekcja opcjonalna steruje kolekcji hello dziennika zdarzeń z dziennika systemowego. W przypadku pominięcia sekcji hello zdarzenia dziennika systemowego nie są przechwytywane w ogóle.

Kolekcja syslogEventConfiguration Hello ma jeden wpis dla każdego obiektu syslog zainteresowań. W przypadku minSeverity "NONE" dla określonego obiektu lub tego obiektu nie ma w elemencie hello w ogóle, żadne zdarzenia z tym zakładzie są przechwytywane.

Element | Wartość
------- | -----
sink — obiekty | Rozdzielana przecinkami lista nazw wychwytywanie toowhich osobny dziennik zdarzeń są publikowane. Wszystkie zdarzenia dziennika spełniające hello ograniczenia syslogEventConfiguration są zbiornika tooeach opublikowane na liście. Przykład: "EHforsyslog"
facilityName | Nazwę obiektu syslog (takich jak "dziennika\_użytkownika" lub "dziennika\_LOCAL0"). Zobacz sekcję "funkcje" hello hello [strony man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) hello pełnej listy.
minSeverity | Poziom ważności syslog (takich jak "dziennika\_błąd" lub "dziennika\_informacje"). Zobacz sekcję "poziomu" hello hello [strony man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) hello pełnej listy. rozszerzenie Hello przechwytuje urządzenie toohello zdarzeń wysłanych w lub powyżej hello określony poziom.

Po określeniu `syslogEvents`, LAD zawsze zapisuje tabeli tooa danych w magazynie Azure. Możesz można mieć hello takie same dane zapisane tooJSON obiekty BLOB i/lub centra zdarzeń, ale nie można wyłączyć zapisywanie tabeli tooa danych. Hello partycjonowania zachowanie dla tej tabeli jest taki sam, jak opisano dla hello `performanceCounters`. Nazwa tabeli Hello jest złączeniem hello te ciągi:

* `LinuxSyslog`
* Data, w postaci hello "RRRRMMDD", która zmienia co 10 dni

Przykłady obejmują `LinuxSyslog20170410` i `LinuxSyslog20170609`.

### <a name="perfcfg"></a>perfCfg

Określa tę sekcję, wykonanie dowolnego [OMI](https://github.com/Microsoft/omi) zapytania.

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

Element | Wartość
------- | -----
przestrzeń nazw | (opcjonalnie) hello OMI przestrzeń nazw, w ramach których hello można wykonać zapytania. Jeśli nie zostanie podany, hello wartość domyślna to "główny/scx", implementowane przez hello [programu System Center i platform dostawców](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).
query | Wykonano toobe zapytania OMI Hello.
Tabela | tabeli magazynu systemu Azure hello (opcjonalnie), Witaj wyznaczone konta magazynu (zobacz [chronionych ustawień](#protected-settings)).
frequency | (opcjonalnie) hello liczbę sekund między wykonanie hello zapytania. Wartość domyślna to 300 (5 minut); wartość minimalna wynosi 15 sekund.
sink — obiekty | (opcjonalnie) Powinien zostać opublikowany przecinkami lista nazw dodatkowe wychwytywanie toowhich raw Przykładowe metryki wyników. Bez agregacji te przykłady pierwotnych jest obliczana przez rozszerzenie hello lub metryk usługi Azure.

Należy określić albo "Tabela" lub "sink" i/lub.

### <a name="filelogs"></a>fileLogs

Formanty hello przechwytywania plików dziennika. LAD przechwytuje nowych wierszy tekstu, ponieważ są one zapisywane toohello plików i zapisuje je w tootable wierszy i/lub dowolnej określonej wychwytywanie (JsonBlob lub EventHub).

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

Element | Wartość
------- | -----
Plik | Witaj pełną nazwę ścieżki toobe pliku dziennika hello obserwowane i przechwyceniu. Hello pathname nazwę jednego pliku; Nie można jej nazwę katalogu lub zawierać symbole wieloznaczne.
Tabela | tabeli magazynu systemu Azure hello (opcjonalnie), w magazynie Witaj wyznaczone konta (określone w konfiguracji hello chroniony), do nowych wierszy z powitalne "tail" hello pliku są zapisywane.
sink — obiekty | (opcjonalnie) Wysyłane przecinkami lista nazw dodatkowe wychwytywanie toowhich dziennika wierszy.

Należy określić albo "Tabela" lub "sink" i/lub.

## <a name="metrics-supported-by-hello-builtin-provider"></a>Obsługiwane przez dostawcę wbudowane hello metryk

Dostawca metryki wbudowane Hello jest źródłem metryki najbardziej interesujące tooa szeroką gamę użytkowników. Te metryki można podzielić na pięć szerokie klasy:

* Procesor
* Memory (Pamięć)
* Sieć
* System plików
* Dysk

### <a name="builtin-metrics-for-hello-processor-class"></a>wbudowane metryki hello procesora — klasa

Hello klasy procesora metryk udostępnia informacje na temat użycia procesora w hello maszyny Wirtualnej. Podczas agregowania wartości procentowych, wynik hello jest średnią hello przez wszystkie procesory. W dwa podstawowe maszyny Wirtualnej Jeśli jeden rdzeń był zajęty 100% i hello innych był bezczynny, 100% hello zgłosił, że PercentIdleTime będzie równa 50. Jeśli 50% zajęty dla każdego rdzenia hello takie same, hello zgłosił wynik będzie również wartość równa 50. Cztery podstawowe maszyny Wirtualnej z jednego rdzenia 100% jest zajęty i hello innym bezczynny, hello zgłosił, że PercentIdleTime jest 75.

Licznik | Znaczenie
------- | -------
PercentIdleTime | Procent czasu, w oknie agregacji hello czy procesory zostały wykonywania pętli bezczynności hello jądra
percentProcessorTime | Procent czasu wykonania wątku czynnego
PercentIOWaitTime | Procent czasu oczekiwania na toocomplete operacji We/Wy
PercentInterruptTime | Procent czasu wykonywania sprzęt i oprogramowanie przerwań i wywołań DPC (opóźnione wywołania procedur)
PercentUserTime | Czynnego czasu w oknie agregacji hello hello procent czasu spędzony w użytkownika więcej przy normalnym priorytecie
PercentNiceTime | Czynnego czasu hello procentowym priorytetem obniżona (nieuprzywilejowany)
PercentPrivilegedTime | Czynnego czasu hello procentowym w trybie uprzywilejowanym (jądra)

Witaj pierwsze cztery liczniki powinien Suma too100%. Hello ostatnie trzy liczniki również Suma too100%; Suma hello PercentProcessorTime, PercentIOWaitTime i PercentInterruptTime ich podziału.

Ustaw tooobtain pojedynczego Metryka zagregowane wszystkich procesorów `"condition": "IsAggregate=TRUE"`. tooobtain metryki dla konkretny procesor, takie jak drugi procesor logiczny hello z czterech podstawowych maszyny Wirtualnej, należy ustawić `"condition": "Name=\\"1\\""`. Numery procesorów logicznych znajdują się w zakresie hello `[0..n-1]`.

### <a name="builtin-metrics-for-hello-memory-class"></a>wbudowane metryki hello pamięci — klasa

Hello klasy pamięci metryk zawiera informacje o wykorzystanie pamięci, stronicowania i wymiany.

Licznik | Znaczenie
------- | -------
AvailableMemory | Dostępnej pamięci fizycznej w MiB
PercentAvailableMemory | Dostępna pamięć fizyczna jako procent całkowitej ilości pamięci
UsedMemory | W użyciu pamięć fizyczna (MiB)
PercentUsedMemory | W użyciu pamięć fizyczna jako procent całkowitej ilości pamięci
PagesPerSec | Całkowita liczba stronicowania (odczyt/zapis)
PagesReadPerSec | Strony odczytywać kopii magazynu (pliku wymiany, pliku programu, pliku mapowanego itp.)
PagesWrittenPerSec | Przechowywanie stron zapisanych toobacking (pliku wymiany, pliku mapowanego itp.)
AvailableSwap | Obszar wymiany nieużywane (MiB)
PercentAvailableSwap | Obszar wymiany nieużywane jako procent całkowitego obszaru wymiany
UsedSwap | W użyciu obszar wymiany (MiB)
PercentUsedSwap | W obsłudze obszaru wymiany w procentach całkowitego obszaru wymiany

Ta klasa metryki ma tylko jedno wystąpienie. atrybut "warunku" Hello nie zawiera przydatne ustawień i powinny być pominięte.

### <a name="builtin-metrics-for-hello-network-class"></a>wbudowane metryki hello sieci — klasa

Hello klasy metryki sieci zawiera informacje dotyczące aktywności sieci dla poszczególnych interfejsów od uruchomienia. LAD nie ujawnia przepustowości metryk, które mogą być pobierane z hosta metryki.

Licznik | Znaczenie
------- | -------
BytesTransmitted | Całkowita liczba bajtów wysłanych od momentu rozruchu
BytesReceived | Całkowita liczba bajtów odebranych od rozruchu
BytesTotal | Całkowita liczba bajtów wysyłane lub odbierane od rozruchu
PacketsTransmitted | Łączna liczba pakietów wysłanych od momentu rozruchu
PacketsReceived | Całkowita liczba pakietów otrzymanych od rozruchu
TotalRxErrors | Liczba błędów od rozruchu
TotalTxErrors | Liczba transmisji błędów od rozruchu
TotalCollisions | Liczba kolizji zgłoszone przez porty sieciowe powitania od rozruchu

 Mimo że ta klasa jest instancji, LAD nie obsługuje przechwytywania metryki sieci zagregowane we wszystkich urządzeń sieciowych. Ustaw tooobtain hello metryki dla określonego interfejsu, takich jak eth0, `"condition": "InstanceID=\\"eth0\\""`.

### <a name="builtin-metrics-for-hello-filesystem-class"></a>wbudowane metryki hello klasy systemu plików

Witaj klasy Filesystem metryk udostępnia informacje na temat użycia systemu plików. Wartości bezwzględne i procent ma być zgłaszane będą wyświetlane tooan zwykłego użytkownika (a nie głównego).

Licznik | Znaczenie
------- | -------
FreeSpace | Dostępnego miejsca na dysku w bajtach
UsedSpace | Używane miejsce na dysku w bajtach
PercentFreeSpace | Wartość procentowa wolnego miejsca
PercentUsedSpace | Procent wykorzystania miejsca
PercentFreeInodes | Wartość procentowa węzłów i nieużywanych
PercentUsedInodes | Wartość procentowa przydzielonych (w użyciu) węzły i sumowane przez wszystkie systemy plików
BytesReadPerSecond | Bajtów odczytanych na sekundę
BytesWrittenPerSecond | Bajtów zapisanych na sekundę
BytesPerSecond | Bajty odczytu lub zapisu na sekundę
ReadsPerSecond | Operacje odczytu na sekundę
WritesPerSecond | Zapis operacji na sekundę
TransfersPerSecond | Operacje odczytu lub zapisu na sekundę

Wartości zagregowane we wszystkich systemach plików można uzyskać przez ustawienie `"condition": "IsAggregate=True"`. Wartości dla określonego zainstalowany system plików, takich jak "/ mnt", można uzyskać przez ustawienie `"condition": 'Name="/mnt"'`.

### <a name="builtin-metrics-for-hello-disk-class"></a>wbudowane metryki hello klasy dysku

Witaj klasy dysku metryk zawiera informacje na temat użycia urządzenia dysku. Te statystyki mają zastosowanie toohello cały dysk. Jeśli istnieje wiele systemów plików na urządzeniu, hello liczników dla tego urządzenia to w rzeczywistości zagregowane we wszystkich z nich.

Licznik | Znaczenie
------- | -------
ReadsPerSecond | Operacje odczytu na sekundę
WritesPerSecond | Zapis operacji na sekundę
TransfersPerSecond | Całkowita liczba operacji na sekundę
AverageReadTime | Średnia liczba sekund na operacja odczytu
AverageWriteTime | Średnia liczba sekund na operację zapisu
AverageTransferTime | Średnia liczba sekund na operację
AverageDiskQueueLength | Średnia liczba operacji w kolejce dysku
ReadBytesPerSecond | Liczba bajtów odczytanych na sekundę
WriteBytesPerSecond | Liczba bajtów zapisanych na sekundę
BytesPerSecond | Liczba bajtów odczytywanych lub zapisywanych na sekundę

Zagregowane wartości na wszystkich dyskach można uzyskać przez ustawienie `"condition": "IsAggregate=True"`. Ustaw tooget informacje dotyczące określonego urządzenia (na przykład/dev/sdf1), `"condition": "Name=\\"/dev/sdf1\\""`.

## <a name="installing-and-configuring-lad-30-via-cli"></a>Instalowanie i konfigurowanie LAD 3.0 za pomocą interfejsu wiersza polecenia

Zakładając, że są chronione ustawienia w pliku hello PrivateConfig.json oraz informacje o konfiguracji publicznego jest PublicConfig.json, uruchom następujące polecenie:

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

polecenie Hello przyjęto założenie, że używasz tryb zarządzania zasobami Azure hello (arm) hello wiersza polecenia platformy Azure. tooconfigure LAD wdrożenia klasycznego modelu (ASM), maszynach wirtualnych, Przełącz zbyt trybu "asm" (`azure config mode asm`) i pominąć hello Nazwa grupy zasobów w poleceniu hello. Aby uzyskać więcej informacji, zobacz hello [dokumentacji interfejsu wiersza polecenia i platform](https://docs.microsoft.com/azure/xplat-cli-connect).

## <a name="an-example-lad-30-configuration"></a>Przykład LAD 3.0 konfiguracji

Oparte na powitania poprzedzających definicje, tutaj jego Przykładowa konfiguracja rozszerzenia LAD 3.0 wyjaśnienie niektórych. tooapply przykładowym scenariuszu tooyour powinien korzystać z własnej nazwy konta magazynu, uwzględniając tokenu sygnatury dostępu Współdzielonego i tokeny EventHubs sygnatury dostępu Współdzielonego.

### <a name="privateconfigjson"></a>PrivateConfig.json

Skonfiguruj te ustawienia prywatnych:

* Konto magazynu
* zgodnego tokenu sygnatury dostępu Współdzielonego konta
* wychwytywanie kilka (JsonBlob lub EventHubs z tokenami SAS)

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a>PublicConfig.json

Te ustawienia publicznego spowodować LAD do:

* Przekaż procent procesora czasu i używać miejsca na dysku metryki toohello `WADMetrics*` tabeli
* Przekazywanie komunikatów z toohello zakładzie "użytkownika" i ważność "informacje" syslog `LinuxSyslog*` tabeli
* Przekaż raw OMI zapytania wyników (PercentProcessorTime i PercentIdleTime) toohello o nazwie `LinuxCPU` tabeli
* Przekaż dołączany wiersze w pliku `/var/log/myladtestlog` toohello `MyLadTestLog` tabeli

W każdym przypadku również przekazywania danych do:

* Magazyn obiektów Blob Azure (nazwa kontenera jest zdefiniowany w ujściu JsonBlob hello)
* Punkt końcowy EventHubs (jak określono w ujściu EventHubs hello)

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

Witaj `resourceId` hello konfiguracji musi odpowiadać czy skali maszyny wirtualnej maszyny Wirtualnej lub hello hello ustawiony.

* Metryki platformy Azure, wykresów i alerty wie resourceId hello z hello pracy maszyny Wirtualnej. Oczekuje toofind hello danych dla maszyny Wirtualnej przy użyciu hello resourceId hello wyszukiwania klucza.
* Jeśli używasz platformy Azure skalowania automatycznego resourceId hello w konfiguracji automatycznego skalowania hello musi być zgodna z resourceId hello używane przez LAD.
* Hello resourceId jest wbudowana w hello nazwy JsonBlobs napisane przez LAD.

## <a name="view-your-data"></a>Wyświetlanie danych

Dane dotyczące wydajności hello tooview portalu Azure lub Ustaw alerty:

![Obraz](./media/diagnostic-extension/graph_metrics.png)

Witaj `performanceCounters` danych zawsze są przechowywane w tabeli magazynu Azure. Interfejsy API usługi Azure Storage są dostępne dla wielu języków i platform.

Dane wysyłane wychwytywanie tooJsonBlob są przechowywane w obiekty BLOB na koncie magazynu hello o nazwie w hello [chronionych ustawień](#protected-settings). Będzie można korzystać z danych obiektu blob hello przy użyciu dowolnego interfejsów API magazynu obiektów Blob Azure.

Ponadto można użyć tych danych hello tooaccess narzędzi interfejsu użytkownika w usłudze Azure Storage:

* Eksplorator serwera programu Visual Studio.
* [Eksplorator usługi Storage platformy Microsoft Azure](https://azurestorageexplorer.codeplex.com/ "Eksploratora usługi Azure Storage").

Ta migawka sesji Eksploratora usługi Microsoft Azure Storage pokazuje hello wygenerowane tabele usługi Azure Storage i kontenery z rozszerzeniem LAD 3.0 poprawnie skonfigurowana na testowej maszynie Wirtualnej. Obraz powitania nie jest zgodna z hello [Przykładowa konfiguracja LAD 3.0](#an-example-lad-30-configuration).

![Obraz](./media/diagnostic-extension/stg_explorer.png)

Zobacz hello odpowiednich [dokumentacji EventHubs](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn jak tooconsume komunikaty opublikowane tooan EventHubs endpoint.

## <a name="next-steps"></a>Następne kroki

* Tworzenie metryk alertów w [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) dla metryki hello zbierania.
* Utwórz [monitorowania wykresy](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) dla Twojego metryki.
* Dowiedz się, jak za[utworzyć zestaw skali maszyny wirtualnej](/azure/virtual-machines/linux/tutorial-create-vmss) przy użyciu programu Skalowanie automatyczne toocontrol metryki.
