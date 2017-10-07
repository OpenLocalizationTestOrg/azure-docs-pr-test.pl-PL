---
title: "aaaUsing udostępnionych sygnatur dostępu (SAS) w usłudze Azure Storage | Dokumentacja firmy Microsoft"
description: "Dowiedz się toouse udostępnionego dostępu podpisów (SAS) toodelegate dostępu tooAzure magazynu zasobów, w tym obiekty BLOB, kolejek, tabel i plików."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 46fd99d7-36b3-4283-81e3-f214b29f1152
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/18/2017
ms.author: marsma
ms.openlocfilehash: 5b75a3c25bcfb9f1ceb81f31dc2d42376bd105cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-shared-access-signatures-sas"></a>Przy użyciu sygnatury dostępu współdzielonego (SAS)

Sygnatury dostępu współdzielonego (SAS) zapewnia sposób toogrant ograniczony dostęp tooobjects na koncie magazynu klientów tooother bez narażania klucz konta. W tym artykule firma Microsoft Podaj omówienie modelu SAS hello, przejrzyj SAS najlepszych rozwiązań i przyjrzyj się przykłady.

Dla dodatkowych przykładów kodu poza tymi przedstawionych w tym miejscu przy użyciu sygnatury dostępu Współdzielonego, zobacz [wprowadzenie do magazynu obiektów Blob Azure w programie .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) i inne przykłady, które są dostępne w hello [przykłady kodu Azure](https://azure.microsoft.com/documentation/samples/?service=storage) biblioteki. Możesz pobrać hello przykładowe aplikacje i uruchamiać je lub Przeglądaj hello kodu w witrynie GitHub.

## <a name="what-is-a-shared-access-signature"></a>Co to jest sygnatury dostępu współdzielonego?
Sygnatury dostępu współdzielonego zapewnia dostęp delegowany tooresources na koncie magazynu. Z sygnatury dostępu Współdzielonego można przyznać się, że klienci uzyskują dostęp do tooresources na koncie magazynu bez udostępniania klucze Twojego konta. To jest hello punkt klucza przy użyciu sygnatury dostępu współdzielonego w aplikacjach — sygnatury dostępu Współdzielonego jest tooshare bezpieczny sposób zasobów magazynu bez naruszania klucze Twojego konta.

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

Sygnatury dostępu Współdzielonego zapewnia kontrolę nad hello typu dostępu, który można przyznać tooclients mających hello SAS, w tym:

* Interwał powitania za pośrednictwem których hello jest prawidłowa, w tym hello czas rozpoczęcia i czas wygaśnięcia hello sygnatury dostępu Współdzielonego.
* Witaj uprawnienia przyznane przez hello sygnatury dostępu Współdzielonego. Na przykład sygnatury dostępu Współdzielonego dla obiekt blob może udzielić odczytu i zapisu obiektu blob toothat uprawnień, ale nie usunąć uprawnienia.
* Opcjonalne adres IP lub zakres adresów IP, z których Magazyn Azure będzie akceptować hello sygnatury dostępu Współdzielonego. Na przykład może określić zakres adresów IP należących do organizacji tooyour.
* Protokół Hello służącym magazynu Azure będzie akceptować hello sygnatury dostępu Współdzielonego. Możesz użyć tego tooclients opcjonalny parametr toorestrict dostępu przy użyciu protokołu HTTPS.

## <a name="when-should-you-use-a-shared-access-signature"></a>Kiedy należy używać sygnatury dostępu współdzielonego
Sygnatury dostępu Współdzielonego można używać, gdy chce tooprovide tooresources dostępu na kliencie tooany konta magazynu nie posiada kluczy dostępu do konta magazynu. Twoje konto magazynu obejmuje zarówno klucz dostępu podstawowych i pomocniczych, które przyznać dostęp administracyjny tooyour konta i wszystkie zasoby w niej. Żaden z tych kluczy udostępnianie otwiera możliwości toohello Twojego konta złośliwego lub brak dbałości o ich użycia. Sygnatury dostępu współdzielonego zapewniają bezpieczne alternatywę umożliwiającą klientom tooread, zapisu i usuwania danych na koncie magazynu, zgodnie z toohello uprawnienia, które zostały jawnie przyznane uprawnienia i bez potrzeby klucza konta.

Typowy scenariusz, w których sygnatury dostępu Współdzielonego jest użyteczny to usługa, gdzie użytkownicy odczytu i zapisu konta magazynu tooyour własnych danych. W scenariuszu, w którym konta magazynu są przechowywane dane użytkownika istnieją dwa wzorce projektowe typowe:

1. Klienci przekazywania i pobierania danych za pomocą usługi frontonu serwera proxy, który przeprowadza uwierzytelnianie. Ta usługa proxy frontonu ma możliwość hello sprawdzania poprawności reguł biznesowych, ale w przypadku dużych ilości danych lub dużej liczby transakcji, tworzenie usługi, które mogą być skalowane toomatch żądanie może być kosztowne lub trudne.

  ![Diagram scenariusza: Usługa frontonu serwera proxy](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png)   

1. Usługi LDS uwierzytelnia powitania klienta, w razie potrzeby, a następnie generuje sygnaturę dostępu Współdzielonego. Po hello klient odbierze hello SAS, uzyskiwania dostępu do zasobów konta magazynu bezpośrednio z uprawnień hello określonego przez hello SAS oraz interwału hello dozwoloną hello sygnatury dostępu Współdzielonego. Witaj SAS zmniejsza potrzebę hello routingu wszystkich danych za pośrednictwem usługi Serwer proxy frontonu hello.

  ![Diagram scenariusza: sygnatury dostępu Współdzielonego usługi dostawcy](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png)   

Wiele usług rzeczywistych może używać hybrydowego te dwie metody. Na przykład niektóre dane może przetworzyć i zweryfikować za pośrednictwem serwera proxy frontonu hello, podczas gdy inne dane zapisane i/lub odczytać bezpośrednio przy użyciu sygnatury dostępu Współdzielonego.

Ponadto należy toouse obiektu źródłowego SAS tooauthenticate hello w operacji kopiowania w niektórych scenariuszach:

* Podczas kopiowania obiektu blob tooanother obiektów blob, która znajduje się w innego konta magazynu, należy użyć SAS tooauthenticate hello źródłowego obiektu blob. Opcjonalnie można użyć SAS tooauthenticate hello docelowego obiektu blob również.
* Podczas kopiowania pliku tooanother, który znajduje się w innego konta magazynu, należy użyć pliku źródłowego hello tooauthenticate sygnatury dostępu Współdzielonego. Opcjonalnie można użyć SAS tooauthenticate hello pliku docelowego oraz.
* Podczas kopiowania pliku tooa obiektu blob lub obiektu blob tooa pliku, należy użyć SAS tooauthenticate hello obiektu źródłowego, nawet jeśli hello obiekty źródłowy i docelowy znajdują się w hello same konta magazynu.

## <a name="types-of-shared-access-signatures"></a>Rodzaje sygnatur dostępu współdzielonego
Można utworzyć dwa rodzaje sygnatur dostępu współdzielonego:

* **Usługa sygnatury dostępu Współdzielonego.** Obiekty delegowane sygnatury dostępu Współdzielonego usługi Hello dostępu tooa zasobu tylko w jednej z usług magazynu hello: hello usługi obiektów Blob, kolejki, tabeli lub pliku. Zobacz [konstruowania sygnatury dostępu Współdzielonego usługi](https://msdn.microsoft.com/library/dn140255.aspx) i [przykłady sygnatury dostępu Współdzielonego usługi](https://msdn.microsoft.com/library/dn140256.aspx) Aby uzyskać szczegółowe informacje na temat tworzenia tokenu sygnatury dostępu Współdzielonego usługi hello.
* **Sygnatura dostępu Współdzielonego konta.** delegaty sygnatury dostępu Współdzielonego konta Hello dostępu tooresources w co najmniej jednej usługi magazynu hello. Wszystkie operacje hello dostępne za pomocą sygnatury dostępu Współdzielonego usługi są także dostępne za pośrednictwem konta sygnatury dostępu Współdzielonego. Ponadto konto hello SAS, możesz delegować toooperations dostępu, które mają zastosowanie tooa podane usługi, takie jak **pobierania/ustawiania właściwości usługi** i **uzyskać statystyki usługi**. Możesz również delegować dostęp tooread, zapisu i operacji usuwania kontenerów obiektów blob, tabel, kolejek i udziałów plików, które nie są dozwolone z sygnatury dostępu Współdzielonego usługi. Zobacz [konstruowania SAS konta](https://msdn.microsoft.com/library/mt584140.aspx) Aby uzyskać szczegółowe informacje na temat tworzenia tokenu sygnatury dostępu Współdzielonego konta hello.

## <a name="how-a-shared-access-signature-works"></a>Jak działa sygnatury dostępu współdzielonego
Sygnatury dostępu współdzielonego jest podpisem identyfikator URI, który wskazuje tooone lub więcej zasobów magazynu i zawiera token, który zawiera specjalnego zestawu parametrów zapytania. Hello token wskazuje, jak hello zasoby mogą być używane w taki sposób, przez powitania klienta. Jeden z parametrów zapytania hello, hello podpisu, jest utworzone na podstawie parametrów SAS hello i podpisany kluczem konta hello. Ta sygnatura jest używany przez usługi Azure Storage tooauthenticate hello sygnatury dostępu Współdzielonego.

Oto przykład identyfikatora URI połączenia SAS, identyfikator URI zasobu hello przedstawiający i tokenu sygnatury dostępu Współdzielonego hello:

![Składniki identyfikatora URI sygnatury dostępu Współdzielonego](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png)   

Witaj tokenu sygnatury dostępu Współdzielonego jest ciągiem generowania na powitania *klienta* po stronie (zobacz hello [przykłady SAS](#sas-examples) sekcji Przykłady kodu). Token sygnatury dostępu Współdzielonego, które można wygenerować z biblioteki klienta magazynu hello, na przykład nie będzie śledzona przez usługi Azure Storage w dowolny sposób. Można utworzyć nieograniczoną liczbę tokeny sygnatury dostępu Współdzielonego na powitania po stronie klienta.

Gdy klient poda tooAzure identyfikatora URI połączenia SAS magazynu jako część żądania, usługa hello sprawdza hello SAS parametrów i tooverify podpis jest nieprawidłowy dla uwierzytelniania hello żądania. Jeśli usługa hello sprawdza, czy ten podpis hello jest prawidłowy, Żądanie hello jest uwierzytelniony. W przeciwnym razie hello żądanie zostało odrzucone z kodem błędu 403 (Dostęp zabroniony).

## <a name="shared-access-signature-parameters"></a>Parametry sygnatury dostępu współdzielonego
Sygnatura dostępu Współdzielonego konta Hello tokeny sygnatury dostępu Współdzielonego usługi obejmują kilka wspólnych parametrów i kilka parametrów również wziąć, czy są różne.

### <a name="parameters-common-tooaccount-sas-and-service-sas-tokens"></a>Tooaccount wspólne parametry sygnatury dostępu Współdzielonego i tokeny sygnatury dostępu Współdzielonego usługi
* **Wersja interfejsu API** opcjonalny parametr określający żądania hello tooexecute toouse wersji hello magazynu usługi.
* **Wersja usługi** wymaganym parametrem, który określa Żądanie hello tooauthenticate toouse wersji hello magazynu usługi.
* **Godzina rozpoczęcia.** Jest to czas hello, w których hello SAS staje się nieprawidłowy. czas rozpoczęcia Hello sygnatury dostępu współdzielonego jest opcjonalne. W przypadku pominięcia czas rozpoczęcia hello SAS zaczyna się natychmiast. Witaj czas rozpoczęcia musi być wyrażony w formacie UTC (Coordinated Universal Time), z specjalne oznaczeniem UTC ("Z"), na przykład `1994-11-05T13:15:30Z`.
* **Czas wygaśnięcia.** Jest to hello czasu po upływie którego hello skojarzenia zabezpieczeń nie jest już prawidłowy. Najlepszym rozwiązaniem jest Określ czas wygaśnięcia dla sygnatury dostępu Współdzielonego lub powiązać ją z zasadami dostępu przechowywane. Witaj czas wygaśnięcia musi być wyrażony w formacie UTC (Coordinated Universal Time) z specjalne oznaczeniem UTC ("Z"), na przykład `1994-11-05T13:15:30Z` (Zobacz więcej poniżej).
* **Uprawnienia.** uprawnienia Hello określone w elemencie hello SAS wskazują, jakie operacje powitania klienta można wykonywać względem zasobów magazynu hello przy użyciu hello sygnatury dostępu Współdzielonego. Uprawnienia dostępne są różne dla konta sygnatury dostępu Współdzielonego i sygnatury dostępu Współdzielonego usługi.
* **ADRES IP.** Opcjonalny parametr określający adres IP lub zakres adresów IP poza platformą Azure (zobacz sekcję hello [stan konfiguracji sesji Routing](../../expressroute/expressroute-workflows.md#routing-session-configuration-state) dla Express Route) z żądaniach tooaccept.
* **Protokół.** Opcjonalny parametr, który określa protokół hello dozwoloną dla żądania. Możliwe wartości to zarówno protokołu HTTPS i HTTP (`https,http`), czyli tylko wartość domyślną hello lub HTTPS (`https`). Należy pamiętać, że HTTP tylko nie jest dozwoloną wartość.
* **Podpis.** Podpis Hello jest tworzony z hello innych parametrów, określony jako część tokenu i ponownie szyfrowane. Został on użyty hello tooauthenticate sygnatury dostępu Współdzielonego.

### <a name="parameters-for-a-service-sas-token"></a>Parametry dla tokenu sygnatury dostępu Współdzielonego usługi
* **Zasobów pamięci masowej.** Zasobów magazynu, dla których możesz delegować dostęp za pomocą usługi SAS obejmują:
  * Kontenery i obiekty BLOB
  * Udziały plików i plików
  * Kolejki
  * Tabele i zakresy jednostek do tabeli.

### <a name="parameters-for-an-account-sas-token"></a>Parametry dla tokenu sygnatury dostępu Współdzielonego konta
* **Usługi lub usług.** Sygnatura dostępu Współdzielonego konta można delegować dostępu tooone lub więcej usług magazynu hello. Na przykład można utworzyć konto sygnatury dostępu Współdzielonego czy delegatów dostępu toohello usługi obiektów Blob i plików. Lub można utworzyć sygnatury dostępu Współdzielonego, że delegatów dostępu tooall cztery usługi (obiektu Blob, kolejki, tabel i plików).
* **Typy zasobów magazynu.** Sygnatura dostępu Współdzielonego konta dotyczy tooone lub więcej grup zasobów magazynu, a nie konkretnego zasobu. Można utworzyć konta SAS toodelegate dostępu do:
  * API poziomu usług jest wywoływana względem zasobów konta magazynu hello. Przykłady obejmują **pobierania/ustawiania właściwości usługi**, **uzyskać statystyki usługi**, i **listy kontenerów/kolejki/tabel/udziałów**.
  * Interfejsy API kontenera niskiego poziomu, nazywane hello kontenera obiektów dla poszczególnych usług: obiektów blob w kontenerach, kolejek, tabel i udziałów plików. Przykłady obejmują **tworzenia/usuwania kontenera**, **tworzenia/usuwania kolejki**, **tworzenia/usuwania tabeli**, **tworzenia/usuwania udziału**i  **Wyświetl listę obiektów blob/pliki i katalogi**.
  * API na poziomie obiektu jest wywoływana względem obiektów blob, wiadomości w kolejce jednostek tabeli i plików. Na przykład **umieszczanie obiektu Blob**, **jednostki zapytania**, **pobrać wiadomości**, i **Utwórz plik**.

## <a name="examples-of-sas-uris"></a>Przykłady identyfikatorów URI sygnatury dostępu Współdzielonego

### <a name="service-sas-uri-example"></a>Przykładowy identyfikator URI sygnatury dostępu Współdzielonego usługi

Oto przykład usługi identyfikatora URI połączenia SAS, która zapewnia odczytu i zapisu obiektu blob tooa uprawnienia. Tabela Hello dzieli każdej części hello URI toounderstand jak przyczynia się toohello sygnatury dostępu Współdzielonego:

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| Nazwa | Część SAS | Opis |
| --- | --- | --- |
| Identyfikator URI obiektu blob |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |adres Hello hello obiektu blob. Należy pamiętać, że przy użyciu protokołu HTTPS jest zdecydowanie zalecane. |
| Wersja usługi magazynu |`sv=2015-04-05` |Dla magazynu usług wersji 2012-02-12, a później, ten parametr wskazuje hello toouse wersji. |
| Godzina rozpoczęcia |`st=2015-04-29T22%3A18%3A26Z` |Określona w formacie UTC. Jeśli hello SAS toobe prawidłowy natychmiast, należy pominąć hello czas rozpoczęcia. |
| Czas wygaśnięcia |`se=2015-04-30T02%3A23%3A26Z` |Określona w formacie UTC. |
| Zasób |`sr=b` |zasób Hello jest obiektu blob. |
| Uprawnienia |`sp=rw` |Witaj uprawnienia przyznane przez hello SAS obejmują Read (r) i zapisu (w). |
| Zakres adresów IP |`sip=168.1.5.60-168.1.5.70` |Witaj zakres adresów IP, z których będą akceptowane żądania. |
| Protokół |`spr=https` |Dozwolone są tylko żądania przy użyciu protokołu HTTPS. |
| Podpis |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |Używane tooauthenticate dostępu toohello blob. Podpis Hello jest HMAC obliczona ciąg do logowania i klucz przy użyciu algorytm SHA256 hello, a następnie kodowany w formacie Base64. |

### <a name="account-sas-uri-example"></a>Przykład identyfikatora URI połączenia SAS konta

Oto przykład konta SAS czy używa hello tego samego typowych parametrów w tokenie hello. Ponieważ te parametry są opisane powyżej, ich nie zostały opisane w tym miejscu. Tylko hello parametrów, które są określone tooaccount, SAS są opisane w poniższej tabeli hello.

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| Nazwa | Część SAS | Opis |
| --- | --- | --- |
| Identyfikator URI zasobu |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |Witaj punkt końcowy usługi Blob, wraz z parametrami pobierania właściwości usługi (jeśli jest wywoływana z GET) lub właściwości usługi (jeśli jest wywoływana z ZESTAWEM). |
| Usługi |`ss=bf` |Hello SAS dotyczy toohello obiektów Blob oraz usługi plików |
| Typy zasobów |`srt=s` |Witaj SAS dotyczy operacji na poziomie tooservice. |
| Uprawnienia |`sp=rw` |uprawnienia Hello udzielić dostępu tooread i operacji zapisu. |

Biorąc pod uwagę, że są ograniczone uprawnienia toohello poziomu usługi, dostępne operacje przy użyciu tego skojarzenia zabezpieczeń są **pobrać właściwości usługi Blob** (odczyt) i **ustawić właściwości usługi Blob** (zapis). Jednak z zasobem inny identyfikator URI hello tego samego tokenu sygnatury dostępu Współdzielonego mogą być również używane toodelegate dostępu zbyt**uzyskać statystyki usługi Blob** (odczyt).

## <a name="controlling-a-sas-with-a-stored-access-policy"></a>Kontrolowanie SAS z zasadami dostępu przechowywane
Sygnatury dostępu współdzielonego, można wykonać jedną z dwóch formach:

* **Ad hoc sygnatury dostępu Współdzielonego:** podczas tworzenia sygnatury dostępu Współdzielonego ad hoc, godzina rozpoczęcia hello, czas wygaśnięcia i uprawnienia dla hello SAS są określone w hello identyfikatora URI połączenia SAS (lub domniemanych, w przypadku hello, gdy zostanie pominięty czas rozpoczęcia). Ten typ sygnatury dostępu Współdzielonego można utworzyć jako konto SAS lub sygnatury dostępu Współdzielonego usługi.
* **Sygnatury dostępu Współdzielonego z zasad dostępu przechowywanej:** zasady dostępu do przechowywanych jest zdefiniowany w kontenerze zasobów--kontenera obiektów blob, tabeli, kolejki, lub udziału--plików i mogą być używane toomanage ograniczenia dla co najmniej jeden sygnatur dostępu współdzielonego. Po skojarzeniu sygnatury dostępu Współdzielonego za pomocą zasad dostępu przechowywane, hello SAS dziedziczy ograniczenia hello — czas rozpoczęcia hello, czas wygaśnięcia i uprawnień — zdefiniowane zasady dostępu hello przechowywane.

> [!NOTE]
> Obecnie sygnatura dostępu Współdzielonego konta musi być SAS ad hoc. Przechowywane dostępu, zasady nie są jeszcze obsługiwane dla konta sygnatury dostępu Współdzielonego.

Witaj różnica pomiędzy formularzami Witaj dwie ważne jest jeden scenariusz klucza: odwołania. Ponieważ identyfikator URI sygnatury dostępu Współdzielonego jest adres URL, każdy użytkownik, który uzyskuje hello SAS może być używany, niezależnie od tego, który został pierwotnie utworzony. Sygnatury dostępu Współdzielonego zostanie opublikowana publicznie, może służyć każdy hello world. Sygnatury dostępu Współdzielonego udziela dostępu tooresources tooanyone posiadającym go, dopóki jedna z następujących czterech zdarzeń sytuacji:

1. czas wygaśnięcia Hello określony na powitania osiągnięty sygnatury dostępu Współdzielonego.
2. czas wygaśnięcia Hello określone zasady dostępu hello przechowywane odwołuje się hello osiągnięty SAS (jeśli istnieje odwołanie do zasad dostępu do przechowywanych i określa czas wygaśnięcia). Może to występować, ponieważ hello czasu lub zmodyfikowano zasady dostępu hello przechowywane z upływem czasu w przeszłości, hello, czyli hello toorevoke jednokierunkowych SAS.
3. Witaj przechowywane odwołuje hello SAS jest usuwane, który jest inny sposób hello toorevoke SAS zasad dostępu. Należy pamiętać, że jeśli dokładnie ponownego tworzenia zasad dostępu hello przechowywane z tej samej nazwy, wszystkie istniejące SAS hello tokeny będą ponownie prawidłowe uprawnienia zgodnie z toohello skojarzone z tej zasady dostępu do przechowywanych (przy założeniu, że czas wygaśnięcia hello na powitania nie przeszło SAS). Czy mają zostać toorevoke hello SAS, mieć czy toouse inną nazwę ponownego tworzenia zasad dostępu hello z upływem czasu w przyszłości hello.
4. ponownego wygenerowania klucza konta Hello, który był używany toocreate hello SAS. Trwa ponowne generowanie klucza konta spowoduje, że wszystkie składniki aplikacji przy użyciu tego klucza toofail tooauthenticate dopóki te są aktualizowane toouse hello albo inne klucz prawidłowe konto lub hello konta nowo wygenerowano ponownie klucz.

> [!IMPORTANT]
> Identyfikator URI sygnatury dostępu współdzielonego jest skojarzony z sygnaturą hello klucza toocreate używane konto hello i hello skojarzonych zasad dostępu przechowywanych (jeśli istnieje). Jeśli określono żadnych zasad dostępu przechowywane, hello tylko sposób toorevoke sygnatury dostępu współdzielonego jest klucz konta hello toochange.

## <a name="authenticating-from-a-client-application-with-a-sas"></a>Uwierzytelniania z aplikacji klienta z sygnatury dostępu Współdzielonego
Klient, który znajduje się w posiadaniu sygnatury dostępu Współdzielonego, można użyć hello SAS tooauthenticate żądanie konta magazynu, dla którego nie posiadają hello klucze konta. Sygnatury dostępu Współdzielonego może być uwzględniona w parametrach połączenia lub używana bezpośrednio z hello odpowiedniego konstruktora lub metody.

### <a name="using-a-sas-in-a-connection-string"></a>W parametrach połączenia przy użyciu sygnatury dostępu Współdzielonego
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a>Przy użyciu sygnatury dostępu Współdzielonego w konstruktorze lub — metoda
Kilka konstruktorów biblioteki klienta magazynu Azure i przeciążenia metody oferują parametrem sygnatury dostępu Współdzielonego, aby mógł uwierzytelnić żądania usługi toohello za pomocą sygnatury dostępu Współdzielonego.

Na przykład tutaj identyfikator URI sygnatury dostępu Współdzielonego jest używane toocreate tooa odwołanie do blokowego obiektu blob. Hello sygnatury dostępu Współdzielonego zapewnia hello poświadczeń tylko potrzebnych dla hello żądania. odwołanie obiektu blob bloku Hello są używane do operacji zapisu:

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with hello specified name toohello container.
// If hello blob does not exist, it will be created. If it does exist, it will be overwritten.
try
{
    MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    msWrite.Position = 0;
    using (msWrite)
    {
        await blob.UploadFromStreamAsync(msWrite);
    }

    Console.WriteLine("Create operation succeeded for SAS {0}", sasUri);
    Console.WriteLine();
}
catch (StorageException e)
{
    if (e.RequestInformation.HttpStatusCode == 403)
    {
        Console.WriteLine("Create operation failed for SAS {0}", sasUri);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    else
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}

```

## <a name="best-practices-when-using-sas"></a>Najlepsze rozwiązania przy użyciu sygnatury dostępu Współdzielonego
Korzystając z sygnatury dostępu współdzielonego w aplikacji, należy toobe pamiętać o dwa potencjalne zagrożenia:

* Przeciek sygnatury dostępu Współdzielonego może służyć każdego, kto uzyskuje, które potencjalnie może naruszyć bezpieczeństwo Twojego konta magazynu.
* Jeśli aplikacja kliencka tooa wygaśnie, a aplikacja hello jest tooretrieve nowe SAS z usługi sygnatury dostępu Współdzielonego, można utrudniona funkcjonalność aplikacji hello.

Witaj poniższe zalecenia dotyczące używania sygnatur dostępu współdzielonego mogą pomóc ograniczyć te zagrożenia:

1. **Zawsze używać protokołu HTTPS** toocreate lub rozkładanie sygnatury dostępu Współdzielonego. Sygnatury dostępu Współdzielonego jest przekazywane za pośrednictwem protokołu HTTP, przechwycone osoba przeprowadzająca atak typu man-in--middle jest możliwe tooread hello SAS, a następnie użyć jej w tak samo, jak hello przeznaczone się, że użytkownik może mieć potencjalnie również dane poufne lub dopuszczające uszkodzenia danych hello złośliwy użytkownik.
2. **Odwołanie przechowywane zasady dostępu, jeśli jest to możliwe.** Przechowywane hello opcja toorevoke uprawnienia bez konieczności klucze konta magazynu hello tooregenerate podać zasad dostępu. Ustaw wygaśnięcia hello na bardzo daleko w hello przyszłych (lub nieskończone) i zapewnić, że regularnie zaktualizował toomove go dalej do przyszłych hello.
3. **Użyj najbliższej przyszłości czas wygaśnięcia na ad hoc SAS.** W ten sposób nawet w przypadku złamania zabezpieczeń sygnatury dostępu Współdzielonego, jest prawidłowa tylko dla przez krótki czas. Takie rozwiązanie jest szczególnie ważne, jeśli nie może odwoływać się zasady dostępu do przechowywanych. Czas wygaśnięcia najbliższej przyszłości także ograniczać hello ilość danych, które mogą być zapisywane tooa blob ograniczając hello czas dostępne tooupload tooit.
4. **Mieć automatycznie odnawiaj hello SAS w razie potrzeby klientów.** Klientów należy odnawiać hello SAS oraz przed wygaśnięciem hello, w kolejności czas tooallow ponownych prób, jeśli usługa hello dostarczanie hello SAS jest niedostępna. Jeśli Twoje SAS oznacza toobe używany dla niewielkiej liczby natychmiastowe, tej operacji, które są oczekiwane toobe zakończona w ciągu okresu wygaśnięcia hello, a następnie może to być konieczne, gdyż hello, który nie jest oczekiwany toobe odnowiony. Jednak jeśli klient, który jest regularnie wysyłający żądania za pomocą sygnatury dostępu Współdzielonego, następnie hello możliwości wygaśnięcia wejścia play. Hello kluczowa jest konieczność hello toobalance hello SAS toobe krótkotrwałą (jak wcześniej wspomniano) z tooensure potrzeby hello, który hello klienta żąda wczesne odnawiania za mało (tooavoid przerw w działaniu powodu toohello SAS wygasające przed toosuccessful odnawiania).
5. **Należy zachować ostrożność, czas rozpoczęcia sygnatury dostępu Współdzielonego.** Należy ustawić czas rozpoczęcia hello na sygnatury dostępu Współdzielonego za**teraz**, następnie powodu zegara tooclock (różnice w bieżącej godziny zgodnie z maszyny toodifferent), błędy można zaobserwować sporadycznie dla hello pierwszych kilku minut. Ogólnie rzecz biorąc Ustaw toobe czas rozpoczęcia hello co najmniej 15 minut w przeszłości hello. Lub nie należy ustawiać go, który ułatwi prawidłowe natychmiast we wszystkich przypadkach. zwykle dotyczy to również — czas tooexpiry Hello należy pamiętać, że można zaobserwować się too15 minut zegara pochylenia w żadnym kierunku na każde żądanie. W przypadku klientów przy użyciu REST wersji wcześniejszych too2012-02-12 hello maksymalny czas trwania SAS, która nie odwołuje się do zasad dostępu do przechowywanych jest 1 godziny, a wszystkie zasady Określanie długoterminowych niż który zakończy się niepowodzeniem.
6. **Być określonych toobe zasobów hello dostęp.** Najlepszym rozwiązaniem bezpieczeństwa jest tooprovide użytkownika z hello minimalne wymagane uprawnienia. Jeśli użytkownik potrzebuje tylko pojedynczy element tooa dostęp do odczytu, nadawaj im dostęp do odczytu toothat pojedynczej jednostki i jednostki tooall dostępu nie odczytu/zapisu/usuwania. Ułatwia to również zmniejszyć hello uszkodzenia, jeśli sygnatury dostępu Współdzielonego zostanie naruszony, ponieważ hello SAS ma mniej energii w ręce hello osoby atakującej, która.
7. **Dowiedz się, że Twoje konto będą naliczane za bez użycia, w tym odbywa się za pomocą sygnatury dostępu Współdzielonego.** Jeśli podasz blob tooa dostęp do zapisu, użytkownik może wybrać tooupload obiektu blob 200GB. Jeśli zostały podane je również dostęp do odczytu, mogą one toodownload 10 razy zaciąganie 2 TB wyjście kosztuje dla Ciebie. Ponownie, podaj ograniczone uprawnienia toohelp ograniczyć potencjalne akcje hello złośliwych użytkowników. Użyj tej tooreduce sygnatury dostępu Współdzielonego to zagrożenie (ale być świadoma zegara na czas zakończenia hello).
8. **Sprawdzanie poprawności danych napisane przy użyciu sygnatury dostępu Współdzielonego.** Gdy aplikacja kliencka zapisuje konta magazynu tooyour danych, należy pamiętać, że mogą być problemy z tymi danymi. Jeśli aplikacja wymaga, aby czy danych można sprawdzić poprawności lub autoryzacji, zanim zostanie toouse gotowe, możesz wykonać tej weryfikacji po zapisaniu hello danych i zanim zostanie on użyty przez aplikację. Takie rozwiązanie chroni także uszkodzony lub złośliwymi danych zapisywanych tooyour konta przez użytkownika, który prawidłowo nabyte hello SAS lub przez użytkownika, wykorzystaniu ujawnione sygnatury dostępu Współdzielonego.
9. **Nie używaj sygnatury dostępu Współdzielonego.** Czasami hello ryzyko związane z określoną operację względem konta magazynu przeważają korzyści hello SAS. W takich operacjach Tworzenie usługi warstwy środkowej, która zapisuje konta magazynu tooyour po wykonaniu firm reguły sprawdzania poprawności, uwierzytelnianie i inspekcji. Czasami jest także prostsze dostępu toomanage w inny sposób. Na przykład, jeśli chcesz toomake wszystkie obiekty BLOB w kontenerze publicznie do odczytu, możesz wprowadzić hello kontenera publicznego, zamiast zapewnienie dostępu klienta tooevery sygnatury dostępu Współdzielonego.
10. **Za pomocą toomonitor analityka magazynu aplikacji.** Umożliwia rejestrowanie i metryki tooobserve chwilowo wzrastają wszelkie błędy uwierzytelniania powodu tooan awarii w sieci SAS dostawcy usługi toohello przypadkowego usunięcia lub zasady dostępu przechowywane. Zobacz hello [Blog zespołu usługi Magazyn Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) Aby uzyskać dodatkowe informacje.

## <a name="sas-examples"></a>Przykłady SAS
Poniżej przedstawiono kilka przykładów oba rodzaje sygnatur dostępu współdzielonego, sygnatura dostępu Współdzielonego konta i usługi.

toorun tych C# przykładach trzeba hello tooreference następujące pakiety NuGet w projekcie:

* [Biblioteka klienta usługi Azure Storage dla platformy .NET](http://www.nuget.org/packages/WindowsAzure.Storage), wersja 6.x lub nowszego (toouse konto SAS).
* [Azure Configuration Manager](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

Aby uzyskać dodatkowe przykłady, które pokazują, jak toocreate i test sygnatury dostępu Współdzielonego, zobacz [przykłady kodu platformy Azure dla magazynu](https://azure.microsoft.com/documentation/samples/?service=storage).

### <a name="example-create-and-use-an-account-sas"></a>Przykład: Tworzenie i używanie sygnatury dostępu Współdzielonego konta
Witaj poniższy przykład kodu tworzy konto sygnatury dostępu Współdzielonego, który jest prawidłowy dla usług plików i hello obiektów Blob i zapewnia hello klienta uprawnienia do odczytu, zapisu i listy uprawnień poziomu usług tooaccess interfejsów API. Sygnatura dostępu Współdzielonego konta Hello ogranicza tooHTTPS protokołu hello, więc Żądanie hello musi zostać wykonane z protokołu HTTPS.

```csharp
static string GetAccountSASToken()
{
    // toocreate hello account SAS, you need toouse your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for hello account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return hello SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

tooaccess sygnatury dostępu Współdzielonego konta hello toouse poziomu usług interfejsów API usługi Blob hello, skonstruować obiektu Blob klienta przy użyciu sygnatury dostępu Współdzielonego hello i hello końcowego magazynu obiektów Blob dla konta magazynu.

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using hello SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and hello account name toocreate a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set hello service properties for hello Blob client created with hello SAS.
    blobClientWithSAS.SetServiceProperties(new ServiceProperties()
    {
        HourMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        MinuteMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        Logging = new LoggingProperties()
        {
            LoggingOperations = LoggingOperations.All,
            RetentionDays = 14,
            Version = "1.0"
        }
    });

    // hello permissions granted by hello account SAS also permit you tooretrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a>Przykład: Tworzenie zasad dostępu przechowywane
Witaj poniższy kod tworzy zasady przechowywane dostępu do kontenera. Można użyć ograniczenia toospecify zasad dostępu hello sygnatury dostępu Współdzielonego w kontenerze hello usługi lub jego obiektów blob.

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // hello access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
        // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get hello container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a>Przykład: Tworzenie usługi SAS w kontenerze
Witaj następującego kodu tworzy sygnatury dostępu Współdzielonego w kontenerze. Jeśli podano nazwę hello istniejących zasad dostępu przechowywane, tej zasady są skojarzone z hello sygnatury dostępu Współdzielonego. Jeśli nie zasady przechowywane dostępu, zostanie następnie hello kod tworzy SAS ad hoc na powitania kontenera.

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello container. In this case, all of hello constraints for the
        // shared access signature are specified on hello stored access policy, which is provided by name.
        // It is also possible toospecify some constraints on an ad-hoc SAS and others on hello stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a>Przykład: Tworzenie sygnatury dostępu Współdzielonego usługi na obiektu blob
Hello następującego kodu tworzy SAS obiektu blob. Jeśli podano nazwę hello istniejących zasad dostępu przechowywane, tej zasady są skojarzone z hello sygnatury dostępu Współdzielonego. Jeśli nie zasady przechowywane dostępu, zostanie następnie hello kod tworzy SAS ad hoc na powitania obiektu blob.

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference tooa blob within hello container.
    // Note that hello blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello blob. In this case, all of hello constraints for the
        // shared access signature are specified on hello container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a>Podsumowanie
Sygnatury dostępu współdzielonego są przydatne zapewniające z ograniczonymi uprawnieniami tooyour tooclients konta magazynu, który nie powinien mieć hello klucz konta. Są one tak, to ważna część hello model zabezpieczeń dla dowolnej aplikacji przy użyciu usługi Azure Storage. Jeśli wykonujesz najlepszych rozwiązań hello wymienione w tym miejscu można użyć SAS tooprovide większą elastyczność tooresources dostępu na koncie magazynu bez naruszania zabezpieczeń hello aplikacji.

## <a name="next-steps"></a>Następne kroki
* [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiektów blob](../blobs/storage-manage-access-to-resources.md)
* [Delegowanie dostępu za pomocą sygnatury dostępu współdzielonego](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Wprowadzenie do tabeli i kolejki SAS](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
