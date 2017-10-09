---
title: aaaAuthenticating i autoryzacji z Power BI Embedded
description: "Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a>Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded

korzysta z usługi Power BI Embedded Hello **klucze** i **tokenów aplikacji** do uwierzytelniania i autoryzacji, zamiast jawnego użytkownika końcowego uwierzytelniania. W tym modelu aplikacji zarządza uwierzytelniania i autoryzacji dla użytkowników końcowych. W razie potrzeby aplikacji tworzy i wysyła żądanego raportu hello tokenów aplikacji hello, które informuje toorender naszej usługi. Ten projekt nie wymaga toouse Twojej aplikacji usługi Azure Active Directory do uwierzytelniania i autoryzacji, użytkowników, mimo że nadal można.

## <a name="two-ways-tooauthenticate"></a>Dwa sposoby tooauthenticate

**Klucz** — można używać kluczy dla wszystkich wywołań interfejsu API REST osadzonych Power BI. klucze Hello znajdują się w hello **portalu Azure** , klikając **wszystkie ustawienia** , a następnie **klucze dostępu**. Zawsze należy traktować klucz, tak jakby był on hasła. Te klucze mają toomake uprawnienia wywołać jakiegokolwiek interfejsu API REST dla kolekcji określonego obszaru roboczego.

toouse klucza na wywołanie interfejsu REST Dodaj powitania po nagłówek autoryzacji:            

    Authorization: AppKey {your key}

**Tokenu aplikacji** -tokenów aplikacji są używane dla wszystkich żądań osadzania. Są one zaprojektowane toobe Uruchom po stronie klienta, dzięki czemu są ograniczone tooa pojedynczy raport i jej najlepsze praktyki tooset czas wygaśnięcia.

Tokenów aplikacji są JWT (JSON Web Token), który jest podpisany przez jeden z kluczy.

Token aplikacji może zawierać powitania po oświadczeń:

| Claim | Opis |
| --- | --- |
| **VER** |Wersja Hello tokenu aplikacji hello. 0.2.0 jest hello bieżącej wersji. |
| **lub** |Witaj przeznaczony odbiorcy tokenu hello. Do użytku w usłudze Power BI Embedded: "https://analysis.windows.net/powerbi/api". |
| **iss** |Ciąg wskazujący aplikacji hello wystawiony hello token. |
| **Typ** |Typ Hello tokenu aplikacji, która jest tworzona. Bieżący typ hello obsługiwane tylko **osadzić**. |
| **WCN** |Token hello nazwę kolekcji obszaru roboczego zostało wystawione. |
| **bazy danych WID** |Token hello identyfikator obszaru roboczego zostało wystawione. |
| **Identyfikator RID** |Token hello Identyfikatora raportu zostało wystawione. |
| **Nazwa użytkownika** (opcjonalnie) |Używane zabezpieczenia na poziomie wiersza, jest to ciąg, który może ułatwić identyfikację hello użytkownika, stosując zasady zabezpieczenia na poziomie wiersza. |
| **role** (opcjonalnie) |Ciąg zawierający tooselect ról hello podczas stosowania zasad zabezpieczeń na poziomie wiersza. Przekazywanie więcej niż jednej roli, powinien zostać przekazany jako tablica ciągu. |
| **punkt połączenia usługi** (opcjonalnie) |Ciąg zawierający hello zakresy uprawnień. Przekazywanie więcej niż jednej roli, powinien zostać przekazany jako tablica ciągu. |
| **EXP** (opcjonalnie) |Wskazuje czas hello, w których hello wygaśnięcia tokenu. Te mają być przekazywane w jako systemu Unix sygnatur czasowych. |
| **NBF** (opcjonalnie) |Wskazuje czas hello, w których hello token zaczyna się ważny. Te mają być przekazywane w jako systemu Unix sygnatur czasowych. |

Przykładowy token aplikacji będzie wyglądać następująco:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

Gdy zdekodowany, ekran będzie wyglądać następująco:

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

Brak dostępnych metod w hello zestawów SDK, które ułatwia tworzenie apptokens. Na przykład dla platformy .NET można przyjrzeć się hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) klasy i hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) metody.

Dla hello zestawu .NET SDK, mogą odwoływać się za[zakresy](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).

## <a name="scopes"></a>Zakresy

Tokeny osadzania można toorestrict użycia zasobów hello, który zapewnia dostęp do. Z tego powodu można wygenerować token z zakresu uprawnień.

Oto Hello hello dostępnych zakresów dla Power BI Embedded.

|Zakres|Opis|
|---|---|
|Dataset.Read|Udostępnia uprawnienie tooread hello określony zestaw danych.|
|Dataset.Write|Udostępnia uprawnienie toowrite toohello określony zestaw danych.|
|Dataset.ReadWrite|Udostępnia uprawnienie zapisu i tooread toohello określonego zestawu danych.|
|Report.Read|Udostępnia uprawnienie tooview hello określony raport.|
|Report.ReadWrite|Zapewnia możliwość tooview uprawnień i edytowanie hello określonego raportu.|
|Workspace.Report.Create|Zapewnia nowy raport w hello określony toocreate uprawnień obszaru roboczego.|
|Workspace.Report.Copy|Udostępnia uprawnienie tooclone istniejącego raportu w hello określony obszar roboczy.|

Przy użyciu spacji między zakresy hello podobnie następującej hello, możesz podać wiele zakresów.

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

**Wymagane oświadczenia - zakresów**

punkt połączenia usługi: scopesClaim {scopesClaim} może być ciąg lub tablica ciągów, biorąc pod uwagę hello dozwolone uprawnienia tooworkspace zasobów (raport, zestaw danych itp.)

Token dekodowane, z zakresów zdefiniowanych, będzie wyglądać podobnie następujące toohello.

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a>Operacje i zakresy

|Operacja|Zasób docelowy|Token uprawnień|
|---|---|---|
|Tworzenie nowego raportu oparte na zestawie danych (w pamięci).|Zestaw danych|Dataset.Read|
|Tworzenie nowego raportu oparte na zestawie danych (w pamięci) i Zapisz hello raportu.|Zestaw danych|* Dataset.Read<br>* Workspace.Report.Create|
|Wyświetlanie i Eksploruj/edytowanie (w pamięci) istniejącego raportu. Report.Read oznacza Dataset.Read. To nie zezwala na edycję toosave uprawnienia.|Raport|Report.Read|
|Edytuj i zapisuj istniejącego raportu.|Raport|Report.ReadWrite|
|Zapisz kopię raportu (Zapisz jako).|Raport|* Report.Read<br>* Workspace.Report.Copy|

## <a name="heres-how-hello-flow-works"></a>Oto, jak działa hello przepływu
1. Skopiuj hello interfejsu API klucze tooyour aplikacji. Można uzyskać klucze hello **Azure Portal**.
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. Token deklaracji rozkazujących oświadczenia i ma czasu wygaśnięcia.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. Pobiera podpisany token kluczy dostępu do interfejsu API.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. Użytkownik żąda tooview raportu.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. Token została zweryfikowana za pomocą kluczy dostępu do interfejsu API.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. Usługa Power BI Embedded wysyła toouser raportu.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

Po **Power BI Embedded** wysyła użytkownika toohello raportu hello użytkownika można wyświetlić raport hello w niestandardowych aplikacji. Na przykład, jeśli importowany hello [analizowania sprzedaży PBIX dane przykładowe](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello przykładową aplikację sieci web będzie wyglądać następująco:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a>Zobacz też

[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Rozpoczęcie pracy z przykładem Microsoft Power BI Embedded](power-bi-embedded-get-started-sample.md)  
[Typowe scenariusze Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Wprowadzenie do programu Microsoft Power BI Embedded](power-bi-embedded-get-started.md)  
[Usługa Power BI CSharp repozytorium Git](https://github.com/Microsoft/PowerBI-CSharp)  
Masz więcej pytań? [Spróbuj hello Power BI społeczności](http://community.powerbi.com/)

