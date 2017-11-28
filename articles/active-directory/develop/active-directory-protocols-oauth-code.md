---
title: "Witaj aaaUnderstand przepływu kodu autoryzacji protokołu OAuth 2.0 w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooauthorize wiadomości toouse HTTP dostępu tooweb aplikacji i interfejsów API sieci web w dzierżawie przy użyciu usługi Azure Active Directory i OAuth 2.0."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: de3412cb-5fde-4eca-903a-4e9c74db68f2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4a6fe67d786a5fcb87d1059c2e94ba0c88d26cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# Autoryzowanie dostępu tooweb aplikacji przy użyciu protokołu OAuth 2.0 i usługi Azure Active Directory
Azure Active Directory (Azure AD) używa protokołu OAuth 2.0 tooenable tooauthorize dostępu tooweb aplikacji i interfejsów API sieci web w dzierżawie usługi Azure AD. Ten przewodnik jest niezależny od języka i opisano sposób toosend i odbieranie wiadomości HTTP bez przy użyciu dowolnej z naszych bibliotekach open source.

Witaj przepływu kodu autoryzacji protokołu OAuth 2.0 jest opisany w [sekcji 4.1 specyfikacji hello OAuth 2.0](https://tools.ietf.org/html/rfc6749#section-4.1). Tooperform używane uwierzytelnianie i autoryzację w większości typów aplikacji, w tym aplikacje sieci web i jest natywnie zainstalowane aplikacje.

[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)]

## Przepływ autoryzacji OAuth 2.0
Na wysokim poziomie hello przepływ całego autoryzacji dla aplikacji wygląda nieco następująco:

![Przepływu kodu autoryzacji OAuth](media/active-directory-protocols-oauth-code/active-directory-oauth-code-flow-native-app.png)

## Kod autoryzacji żądania
przepływu kodu autoryzacji Hello rozpoczyna się od klienta hello kierowanie hello użytkownika toohello `/authorize` punktu końcowego. W tym żądaniu powitania klienta wskazuje uprawnienia hello musi tooacquire hello użytkownika. Punkty końcowe hello OAuth 2.0 można uzyskać ze strony aplikacji w klasycznym portalu Azure w hello **Wyświetl punkty końcowe** przycisk w szufladzie dolnej hello.

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&resource=https%3A%2F%2Fservice.contoso.com%2F
&state=12345
```

| Parametr |  | Opis |
| --- | --- | --- |
| Dzierżawy |Wymagane |Witaj `{tenant}` wartość w ścieżce hello hello żądania mogą być używane toocontrol, który można zalogować się do aplikacji hello.  Witaj dozwolone wartości to identyfikatory dzierżawy, na przykład `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` lub `contoso.onmicrosoft.com` lub `common` tokenów niezależny od dzierżawcy |
| client_id |Wymagane |Program Hello identyfikator aplikacji przypisany tooyour aplikacji został zarejestrowany z usługą Azure AD. To można znaleźć w portalu Azure hello. Kliknij przycisk **usługi Active Directory**, kliknij katalog hello, wybierz aplikację hello, a następnie kliknij przycisk **Konfiguruj** |
| response_type |Wymagane |Musi zawierać `code` dla przepływu kodu autoryzacji hello. |
| redirect_uri |Zalecane |Witaj redirect_uri aplikacji, w którym można wysłanych i odebranych przez aplikację odpowiedzi uwierzytelniania.  Dokładnie musi odpowiadać jedną redirect_uris hello, który został zarejestrowany w portalu hello, z wyjątkiem musi być zakodowane w adresie url.  Dla aplikacji natywnych i przenośnych, należy używać wartość domyślną hello `urn:ietf:wg:oauth:2.0:oob`. |
| response_mode |Zalecane |Określa metodę hello, który ma być używane toosend hello wynikowy tooyour tyłu tokenu aplikacji.  Może być `query` lub `form_post`. |
| state |Zalecane |Wartość zawarte w żądaniu hello, który jest także zwracany w odpowiedzi tokenu hello. Losowo generowany unikatową wartość jest zazwyczaj używana w przypadku [zapobieganie fałszerstwie żądania międzywitrynowego](http://tools.ietf.org/html/rfc6749#section-10.12).  Stan Hello jest również używane tooencode informacji na temat stanu hello użytkownika w aplikacji hello przed wystąpieniem hello żądania uwierzytelniania, takie jak strona hello lub widok, które były na. |
| Zasobów |Opcjonalne |Witaj identyfikator URI aplikacji hello składnika web API (zabezpieczonych zasobów). Witaj toofind identyfikator URI aplikacji hello interfejsu API sieci web, w hello portalu Azure, kliknij przycisk **usługi Active Directory**, kliknij katalog hello, kliknij przycisk aplikacji hello, a następnie kliknij przycisk **Konfiguruj**. |
| wiersz |Opcjonalne |Określ typ hello interakcji z użytkownikiem, który jest wymagany.<p> Prawidłowe wartości to: <p> *logowania*: hello użytkownik powinien być zostanie wyświetlony monit o tooreauthenticate. <p> *zgoda*: zgody użytkownika przyznano, ale wymaga toobe aktualizacji. Witaj, użytkownik powinien być zostanie wyświetlony monit o tooconsent. <p> *admin_consent*: administrator powinien być tooconsent zostanie wyświetlony monit o imieniu wszyscy użytkownicy w organizacji |
| login_hint |Opcjonalne |Może być pole adresu e-mail/nazwa użytkownika hello używane wypełnienia toopre hello strony logowania dla użytkownika hello, jeśli znasz swoją nazwę użytkownika wcześniejsze.  Aplikacje często tego parametru należy użyć podczas ponownego uwierzytelniania, już o wyodrębnić hello username z poprzednich logowanie przy użyciu hello `preferred_username` oświadczeń. |
| domain_hint |Opcjonalne |Zawiera wskazówki dotyczące dzierżawy hello lub domeny, która hello użytkownika powinien użyć toosign w. wartość Hello hello domain_hint jest domeną zarejestrowanych hello dzierżawcy. Jeśli jest dostępna dzierżawa hello federacyjnych tooan lokalnego katalogu, AAD przekierowuje serwer federacyjny toohello określonego dzierżawcę. |

> [!NOTE]
> Hello użytkownika w przypadku organizacji, administrator organizacji hello można wyrazić zgodę lub odrzucić w imieniu użytkownika hello lub zezwolenie na powitania tooconsent użytkownika. Hello użytkownik otrzymuje hello opcja tooconsent tylko wtedy, gdy hello administrator pozwala.
>
>

W tym momencie hello użytkownik jest pytany, tooenter ich poświadczeń i uprawnień toohello zgody wskazane hello `scope` parametr zapytania. Po hello użytkownik jest uwierzytelniany i udziela zgody, usługi Azure AD wysyła aplikacji tooyour odpowiedzi na powitania `redirect_uri` adresu w żądaniu.

### Odpowiedź oznaczająca Powodzenie
Odpowiedź oznaczająca Powodzenie może wyglądać następująco:

```
GET  HTTP/1.1 302 Found
Location: http://localhost/myapp/?code= AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA&session_state=7B29111D-C220-4263-99AB-6F6E135D75EF&state=D79E5777-702E-4260-9A62-37F75FF22CCE
```

| Parametr | Opis |
| --- | --- |
| admin_consent |wartość Hello ma wartość PRAWDA, jeśli administrator zgodę tooa zgody żądania wiersza. |
| Kod |Kod autoryzacji Hello żądać aplikacji hello. zasób docelowy hello aplikacji Hello można używać toorequest kod autoryzacji hello tokenu dostępu. |
| session_state |Unikatowa wartość, która identyfikuje hello bieżącą sesję użytkownika. Ta wartość jest identyfikatorem GUID, ale powinien być traktowany jako wartość przezroczystości, która została przekazana bez badania. |
| state |Jeśli parametr Stan jest uwzględniony w żądaniu hello, hello tej samej wartości powinny być wyświetlane w hello odpowiedzi. Dobrym rozwiązaniem dla tooverify aplikacji hello, że wartości stanu hello hello żądań i odpowiedzi są identyczne, przed użyciem odpowiedź hello jest. Dzięki temu toodetect [atakami opartymi na fałszowanie żądań między witrynami (CSRF)](https://tools.ietf.org/html/rfc6749#section-10.12) przed powitania klienta. |

### Odpowiedzi na błąd
Odpowiedzi na błędy mogą być również wysyłane toohello `redirect_uri` tak, aby aplikacja hello można je odpowiednią obsługę.

```
GET http://localhost:12345/?
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Parametr | Opis |
| --- | --- |
| error |Wartość kodu błędu, zdefiniowane w sekcji 5.2 hello [OAuth 2.0 autoryzacji Framework](http://tools.ietf.org/html/rfc6749). Hello dalej tabeli opisano kody błędów hello, które zwraca usługi Azure AD. |
| error_description |Bardziej szczegółowy opis błędu hello. Ten komunikat nie ma toobe przyjazny dla użytkownika końcowego. |
| state |Witaj stan wartość jest liczbą losowo generowany-ponownie wysyłany w żądaniu hello i zwracany w hello odpowiedzi tooprevent między witrynami (CSRF) fałszerstwie żądania. |

#### Kody błędów dla błędów punktu końcowego autoryzacji
Witaj poniższej tabeli opisano hello różnych kody błędów, które mogą być zwracane w hello `error` parametru hello odpowiedzi na błąd.

| Kod błędu: | Opis | Akcja klienta |
| --- | --- | --- |
| invalid_request |Błąd protokołu, takie jak brak wymaganego parametru. |Usuń i ponownie prześlij żądanie hello. Jest to błąd programowanie i zwykle zostanie przechwycony podczas testowania początkowej. |
| unauthorized_client |Witaj aplikację klienta nie jest dozwolone toorequest kod autoryzacji. |Zazwyczaj dzieje się tak, gdy aplikacja kliencka hello nie jest zarejestrowany w usłudze Azure AD lub dzierżawy usługi Azure AD toohello użytkownika nie została dodana. aplikacji Hello można monitować użytkownika hello z instrukcji dotyczących instalowania aplikacji hello i dodanie go tooAzure AD. |
| ACCESS_DENIED |Odmowa zgody właściciel zasobu |Aplikacja kliencka Hello powiadamiać hello użytkownika, którego nie można kontynuować, chyba że użytkownik hello zgadza. |
| unsupported_response_type |w żądaniu hello powitania serwera autoryzacji nie obsługuje hello typ odpowiedzi. |Usuń i ponownie prześlij żądanie hello. Jest to błąd programowanie i zwykle zostanie przechwycony podczas testowania początkowej. |
| server_error |Witaj serwer napotkał nieoczekiwany błąd. |Ponów żądanie hello. Te błędy może wynikać z tymczasowego warunków. Aplikacja kliencka Hello może wyjaśnić toohello użytkownika czy ze względu na tymczasowy błąd tooa jest opóźnione odpowiedzi. |
| temporarily_unavailable |Serwer Hello tymczasowo jest zbyt zajęty toohandle hello żądania. |Ponów żądanie hello. Aplikacja kliencka Hello może wyjaśnić toohello użytkownika czy ze względu na tymczasowy warunek tooa jest opóźnione odpowiedzi. |
| invalid_resource |zasób docelowy Hello jest nieprawidłowy, ponieważ nie istnieje, nie można znaleźć usługi Azure AD lub nie została poprawnie skonfigurowana. |Oznacza to, że hello zasobu, jeśli istnieje, nie został skonfigurowany w dzierżawie powitalnych. aplikacji Hello można monitować użytkownika hello z instrukcji dotyczących instalowania aplikacji hello i dodanie go tooAzure AD. |

## Użyj toorequest kod autoryzacji hello token dostępu
Teraz, gdy zostały nabyte kod autoryzacji i mieć odpowiednie uprawnienia udzielone przez użytkownika hello możesz zrealizować hello kod dostępu tokenu toohello żądanego zasobu, wysyłając toohello żądania POST `/token` punktu końcowego:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded
grant_type=authorization_code
&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrqqf_ZT_p5uEAEJJ_nZ3UmphWygRNy2C3jJ239gV_DBnZ2syeg95Ki-374WHUP-i3yIhv5i-7KU2CEoPXwURQp6IVYMw-DjAOzn7C3JCu5wpngXmbZKtJdWmiBzHpcO2aICJPu1KvJrDLDP20chJBXzVYJtkfjviLNNW7l7Y3ydcHDsBRKZc3GuMQanmcghXPyoDg41g8XbwPudVh7uCmUponBQpIhbuffFP_tbV8SNzsPoFz9CLpBCZagJVXeqWoYMPe2dSsPiLO9Alf_YIe5zpi-zY4C3aLw5g9at35eZTfNd0gBRpR5ojkMIcZZ6IgAA
&redirect_uri=https%3A%2F%2Flocalhost%2Fmyapp%2F
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=p@ssw0rd

//NOTE: client_secret only required for web apps
```

| Parametr |  | Opis |
| --- | --- | --- |
| Dzierżawy |Wymagane |Witaj `{tenant}` wartość w ścieżce hello hello żądania mogą być używane toocontrol, który można zalogować się do aplikacji hello.  Witaj dozwolone wartości to identyfikatory dzierżawy, na przykład `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` lub `contoso.onmicrosoft.com` lub `common` tokenów niezależny od dzierżawcy |
| client_id |Wymagane |Program Hello identyfikator aplikacji przypisany tooyour aplikacji został zarejestrowany z usługą Azure AD. To można znaleźć w hello klasycznego portalu Azure. Kliknij przycisk **usługi Active Directory**, kliknij katalog hello, wybierz aplikację hello, a następnie kliknij przycisk **Konfiguruj** |
| Typ grant_type |Wymagane |Musi być `authorization_code` dla przepływu kodu autoryzacji hello. |
| Kod |Wymagane |Witaj `authorization_code` uzyskanego w poprzedniej sekcji hello |
| redirect_uri |Wymagane |Witaj sam `redirect_uri` wartości, które były używane tooacquire hello `authorization_code`. |
| client_secret |wymagane dla aplikacji sieci web |Witaj klucz tajny aplikacji utworzonej w portalu rejestracji aplikacji hello dla aplikacji.  Nie należy można użyć w natywnej aplikacji, ponieważ client_secrets nie może być niezawodnie przechowywanych na urządzeniach.  Jest to wymagane dla aplikacji sieci web i interfejsów API, którym hello możliwości toostore hello sieci web `client_secret` bezpiecznie na powitania po stronie serwera. |
| Zasobów |wymagane, jeśli określony w żądaniu kodu autoryzacji, else opcjonalne |Witaj identyfikator URI aplikacji hello składnika web API (zabezpieczonych zasobów). |

Kliknij toofind hello identyfikator URI aplikacji w portalu zarządzania Azure, hello **usługi Active Directory**kliknij katalog hello, kliknij przycisk aplikacji hello, a następnie kliknij przycisk **Konfiguruj**.

### Odpowiedź oznaczająca Powodzenie
Usługi Azure AD zwraca token dostępu po pomyślnej odpowiedzi. wywołania sieci toominimize z powitania klienta aplikacji i ich skojarzonych opóźnienia, powitania klienta aplikacji powinien buforowane tokenów dostępu przez okres istnienia tokenu hello, określonego w hello odpowiedzi protokołu OAuth 2.0. toodetermine hello okres istnienia tokenu, użyj albo hello `expires_in` lub `expires_on` wartości parametrów.

Jeśli zasobu interfejsu API sieci web zwraca `invalid_token` kodu błędu, może to oznaczać, że zasobów hello stwierdził wygaśnięcia tego tokenu hello. Jeśli czas zegara powitania klienta i zasobów są różne (znane jako "czas pochylenia"), zasobu hello może należy rozważyć hello token toobe wygasł przed hello token jest wyczyszczone z pamięci podręcznej powitania klienta. W takim przypadku należy wyczyścić hello tokenu z pamięci podręcznej hello, nawet jeśli jest nadal w jego obliczeniowej okres istnienia.

Odpowiedź oznaczająca Powodzenie może wyglądać następująco:

```
{
  "access_token": " eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1388444763",
  "resource": "https://service.contoso.com/",
  "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA",
  "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
  "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC83ZmU4MTQ0Ny1kYTU3LTQzODUtYmVjYi02ZGU1N2YyMTQ3N2UvIiwiaWF0IjoxMzg4NDQwODYzLCJuYmYiOjEzODg0NDA4NjMsImV4cCI6MTM4ODQ0NDc2MywidmVyIjoiMS4wIiwidGlkIjoiN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlIiwib2lkIjoiNjgzODlhZTItNjJmYS00YjE4LTkxZmUtNTNkZDEwOWQ3NGY1IiwidXBuIjoiZnJhbmttQGNvbnRvc28uY29tIiwidW5pcXVlX25hbWUiOiJmcmFua21AY29udG9zby5jb20iLCJzdWIiOiJKV3ZZZENXUGhobHBTMVpzZjd5WVV4U2hVd3RVbTV5elBtd18talgzZkhZIiwiZmFtaWx5X25hbWUiOiJNaWxsZXIiLCJnaXZlbl9uYW1lIjoiRnJhbmsifQ."
}

```

| Parametr | Opis |
| --- | --- |
| ' access_token ' |token dostępu do żądanego Hello. Aplikacja Hello można użyć tego toohello tokenu tooauthenticate zabezpieczonych zasobów, takich jak interfejsu API sieci web. |
| token_type |Wskazuje wartość tokenu typu hello. Hello tylko typ, czy obsługa usługi Azure AD jest elementu nośnego. Aby uzyskać więcej informacji dotyczących tokenów elementu nośnego, zobacz [Framework autoryzacji OAuth2.0: użycie tokenu elementu nośnego (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt) |
| expires_in |Jak długo hello token dostępu jest nieprawidłowy (w sekundach). |
| expires_on |Witaj czas wygaśnięcia tokenu dostępu hello. Data Hello jest reprezentowany jako hello liczbę sekund z rokiem 1970-01-01T0:0:0Z UTC czasu wygaśnięcia hello. Ta wartość jest używane toodetermine hello okres istnienia pamięci podręcznej tokenów. |
| Zasobów |Witaj identyfikator URI aplikacji hello składnika web API (zabezpieczonych zasobów). |
| Zakres |Aplikacja kliencka toohello przyznane uprawnienia personifikacji. Witaj domyślne uprawnienia `user_impersonation`. Właściciel Hello hello zabezpieczonych zasobów można zarejestrować dodatkowych wartości w usłudze Azure AD. |
| refresh_token |Token odświeżania OAuth 2.0. Aplikacja Hello można użyć tego tokeny dostępu dodatkowe tooacquire tokenu po wygaśnięciu tokenu dostępu bieżącego hello.  Odśwież tokeny są to długotrwałe i mogą być używane tooretain tooresources dostępu przez dłuższy czas. |
| żądaniu |Niepodpisane JSON Web Token (JWT). base64Url może aplikacji Hello dekodowania hello segmenty tokenu toorequest informacje o hello użytkownik zalogowany. aplikacji Hello można buforować hello wartości i wyświetlić je, ale nie należy polegać na nich autoryzacji lub granic zabezpieczeń. |

### Oświadczenia tokenu JWT
token JWT Hello hello wartości hello `id_token` parametr może zostać odczytany na powitania po oświadczeń:

```
{
 "typ": "JWT",
 "alg": "none"
}.
{
 "aud": "2d4d11a2-f814-46a7-890a-274a72a7309e",
 "iss": "https://sts.windows.net/7fe81447-da57-4385-becb-6de57f21477e/",
 "iat": 1388440863,
 "nbf": 1388440863,
 "exp": 1388444763,
 "ver": "1.0",
 "tid": "7fe81447-da57-4385-becb-6de57f21477e",
 "oid": "68389ae2-62fa-4b18-91fe-53dd109d74f5",
 "upn": "frank@contoso.com",
 "unique_name": "frank@contoso.com",
 "sub": "JWvYdCWPhhlpS1Zsf7yYUxShUwtUm5yzPmw_-jX3fHY",
 "family_name": "Miller",
 "given_name": "Frank"
}.
```

Aby uzyskać więcej informacji na temat tokenów sieci web JSON, zobacz hello [Specyfikacja wersji roboczej JWT IETF](http://go.microsoft.com/fwlink/?LinkId=392344). Aby uzyskać więcej informacji na temat hello typy tokenów i oświadczeń, przeczytaj [obsługiwany Token i typy oświadczeń](active-directory-token-and-claims.md)

Witaj `id_token` parametr zawiera hello następujące typy oświadczeń:

| Typ oświadczenia | Opis |
| --- | --- |
| lub |Grupy odbiorców hello tokenu. Po wystawieniu tokenu hello aplikacji klienckiej tooa odbiorców hello jest hello `client_id` powitania klienta. |
| EXP |Czas wygaśnięcia. Witaj czas wygaśnięcia tokenu hello. Witaj tokenu toobe prawidłowe, hello bieżącej daty/godziny musi być mniejsza lub równa toohello `exp` wartość. czas Hello jest reprezentowany jako hello liczba sekund od 1 stycznia 1970 (1970-01-01T0:0:0Z) UTC, dopóki hello czasu hello token został wystawiony. |
| family_name |Użytkownika imienia lub nazwiska. Aplikacja Hello można wyświetlić tę wartość. |
| given_name |Imię użytkownika. Aplikacja Hello można wyświetlić tę wartość. |
| IAT |Wygenerowane w czasie. czas powitania po hello JWT został wystawiony. czas Hello jest reprezentowany jako hello liczba sekund od 1 stycznia 1970 (1970-01-01T0:0:0Z) UTC, dopóki hello czasu hello token został wystawiony. |
| iss |Identyfikuje Witaj wystawca tokenów |
| NBF |Nie wcześniej niż czas. Witaj godzina, kiedy hello token skuteczne. Dla hello tokenu toobe prawidłowe hello bieżącej daty/godziny wartość musi być większy lub równy toohello Nbf. czas Hello jest reprezentowany jako hello liczba sekund od 1 stycznia 1970 (1970-01-01T0:0:0Z) UTC, dopóki hello czasu hello token został wystawiony. |
| Identyfikator OID |Identyfikator obiektu (ID) hello obiektu użytkownika w usłudze Azure AD. |
| Sub |Identyfikator podmiotu tokenu. Jest to identyfikator trwałe i modyfikować dla opisuje hello hello tokenu użytkownika. Użyj tej wartości w ramach buforowania logiki. |
| TID |Dzierżawy dzierżawy hello Azure AD, która wystawiła hello token identyfikator (ID). |
| unique_name |Unikatowy identyfikator, który może być wyświetlanych toohello użytkownika. Jest to zwykle główna nazwa użytkownika (UPN). |
| nazwy UPN |Główna nazwa użytkownika hello użytkownika. |
| VER |Wersja. Wersja Hello hello tokenu JWT, zwykle 1.0. |

### Odpowiedzi na błąd
błędy programu endpoint wydawania tokenów Hello są kody błędów HTTP, ponieważ powitania klienta wywołania bezpośrednio hello wydawania tokenów punktu końcowego. Ponadto kod stanu toohello HTTP, punkt końcowy wystawiania tokenu usługi Azure AD hello również zwraca dokument JSON z obiektów, które opisują hello błąd.

Przykładowa odpowiedź błędu może wyglądać następująco:

```
{
  "error": "invalid_grant",
  "error_description": "AADSTS70002: Error validating credentials. AADSTS70008: hello provided authorization code or refresh token is expired. Send a new interactive authorization request for this user and resource.\r\nTrace ID: 3939d04c-d7ba-42bf-9cb7-1e5854cdce9e\r\nCorrelation ID: a8125194-2dc8-4078-90ba-7b6592a7f231\r\nTimestamp: 2016-04-11 18:00:12Z",
  "error_codes": [
    70002,
    70008
  ],
  "timestamp": "2016-04-11 18:00:12Z",
  "trace_id": "3939d04c-d7ba-42bf-9cb7-1e5854cdce9e",
  "correlation_id": "a8125194-2dc8-4078-90ba-7b6592a7f231"
}
```
| Parametr | Opis |
| --- | --- |
| error |Ciąg kodu błędu mogą być używane tooclassify typów błędów występujących, która może być używana tooreact tooerrors. |
| error_description |Komunikat o błędzie, które mogą ułatwić dewelopera zidentyfikować hello głównej przyczyny błędu uwierzytelniania. |
| error_codes |Lista specyficzne dla usługi STS kody błędów, które mogą pomóc w diagnostyce. |
| sygnatura czasowa |czas Hello, w którym wystąpił błąd hello. |
| trace_id |Unikatowy identyfikator dla żądania hello, które mogą pomóc w diagnostyce. |
| correlation_id |Unikatowy identyfikator dla żądania hello, które mogą pomóc w diagnostyce między składnikami. |

#### Kody stanu HTTP
Witaj Poniższa tabela zawiera listę kodów stanu hello HTTP, które hello zwraca punkt końcowy wydawania tokenów. W niektórych przypadkach, kod błędu hello jest wystarczające toodescribe hello odpowiedzi, ale jeśli występują błędy, należy hello tooparse towarzyszące JSON dokumentów i sprawdź, czy jego kod błędu.

| Kod HTTP | Opis |
| --- | --- |
| 400 |Domyślny kod HTTP. Używane w większości przypadków i jest zwykle powodu tooa źle sformułowane żądanie. Usuń i ponownie prześlij żądanie hello. |
| 401 |Uwierzytelnianie nie powiodło się. Na przykład żądania hello brakuje parametru client_secret hello. |
| 403 |Autoryzacja nie powiodła się. Na przykład hello użytkownik nie ma uprawnień tooaccess hello zasobów. |
| 500 |Wystąpił błąd wewnętrzny w hello usług. Ponów żądanie hello. |

#### Kody błędów dla punktu końcowego tokena błędów
| Kod błędu: | Opis | Akcja klienta |
| --- | --- | --- |
| invalid_request |Błąd protokołu, takie jak brak wymaganego parametru. |Usuń i ponownie prześlij żądanie hello |
| invalid_grant |Kod autoryzacji Hello jest nieprawidłowa lub wygasła. |Spróbuj nowe toohello żądania `/authorize` punktu końcowego |
| unauthorized_client |Witaj uwierzytelniany klient nie ma uprawnień toouse udzielić autoryzacji tego typu. |Zazwyczaj dzieje się tak, gdy aplikacja kliencka hello nie jest zarejestrowany w usłudze Azure AD lub dzierżawy usługi Azure AD toohello użytkownika nie została dodana. aplikacji Hello można monitować użytkownika hello z instrukcji dotyczących instalowania aplikacji hello i dodanie go tooAzure AD. |
| invalid_client |Uwierzytelnianie klienta nie powiodło się. |powitania klienta poświadczenia są nieprawidłowe. toofix, administrator aplikacji hello aktualizuje hello poświadczeń. |
| unsupported_grant_type |powitania serwera autoryzacji nie obsługuje typ przydziału hello autoryzacji. |Zmień hello przyznać typu w żądaniu hello. Tego typu błędu powinien wystąpić tylko podczas programowania i być wykryte podczas testowania początkowej. |
| invalid_resource |zasób docelowy Hello jest nieprawidłowy, ponieważ nie istnieje, nie można znaleźć usługi Azure AD lub nie została poprawnie skonfigurowana. |Oznacza to, że hello zasobu, jeśli istnieje, nie został skonfigurowany w dzierżawie powitalnych. aplikacji Hello można monitować użytkownika hello z instrukcji dotyczących instalowania aplikacji hello i dodanie go tooAzure AD. |
| interaction_required |Żądanie hello wymaga interakcji użytkownika. Na przykład krok dodatkowego uwierzytelniania jest wymagany. | Zamiast żądanie nieinterakcyjnym, ponów próbę przy użyciu żądania autoryzacji interakcyjne dla hello sam zasobów. |
| temporarily_unavailable |Serwer Hello tymczasowo jest zbyt zajęty toohandle hello żądania. |Ponów żądanie hello. Aplikacja kliencka Hello może wyjaśnić toohello użytkownika czy ze względu na tymczasowy warunek tooa jest opóźnione odpowiedzi. |

## Użyj zasobu hello tooaccess tokenu dostępu hello
Teraz, zostały pomyślnie uzyskano `access_token`, można hello token w tooWeb żądań interfejsów API, umieszczając ją hello `Authorization` nagłówka. Witaj [RFC 6750](http://www.rfc-editor.org/rfc/rfc6750.txt) specyfikacji wyjaśniono, jak toouse tokenów elementu nośnego w tooaccess żądań HTTP chronionych zasobów.

### Przykładowe żądanie
```
GET /data HTTP/1.1
Host: service.contoso.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ
```

### Odpowiedzi na błąd
Zabezpieczonych zasobów, które implementuje kody stanu HTTP problem RFC 6750. Jeśli Żądanie hello nie ma poświadczeń uwierzytelniania lub brak odpowiedzi hello z tokenu, hello obejmuje `WWW-Authenticate` nagłówka. Gdy żądanie nie powiodło się, serwer zasobów hello odpowie kod stanu HTTP hello i kod błędu.

następujące Hello jest przykładem odpowiedzi nie powiodło się, gdy żądanie klienta hello nie obejmuje tokenu elementu nośnego hello:

```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer authorization_uri="https://login.microsoftonline.com/contoso.com/oauth2/authorize",  error="invalid_token",  error_description="hello access token is missing.",
```

#### Błąd parametrów
| Parametr | Opis |
| --- | --- |
| authorization_uri |Witaj identyfikator URI (fizycznych punktu końcowego) powitania serwera autoryzacji. Ta wartość służy również jako odnośnik kluczy tooget więcej informacji o serwerze hello z punktu końcowego odnajdywania. <p><p> powitania klienta należy zweryfikować tego hello serwera autoryzacji jest zaufany. Jeśli zasobów hello jest chroniony przez usługę Azure AD, jest wystarczające tooverify, hello adres URL rozpoczynający się od https://login.microsoftonline.com lub innego nazwy hosta, który obsługuje usługę Azure AD. Zasób specyficznego dla dzierżawy zawsze powinna zwrócić identyfikatora URI autoryzacji specyficznego dla dzierżawy. |
| error |Wartość kodu błędu, zdefiniowane w sekcji 5.2 hello [OAuth 2.0 autoryzacji Framework](http://tools.ietf.org/html/rfc6749). |
| error_description |Bardziej szczegółowy opis błędu hello. Ten komunikat nie ma toobe przyjazny dla użytkownika końcowego. |
| resource_id |Zwraca hello Unikatowy identyfikator zasobu hello. powitania klienta aplikacji można użyć tego identyfikatora jako wartość hello hello `resource` parametr podczas żądania tokenu hello zasobu. <p><p> Ważne jest, aby hello tooverify aplikacji klienta tej wartości, w przeciwnym razie złośliwe usługi mogą być stanie tooinduce **"podniesienia uprawnień"** ataków <p><p> Witaj zalecane strategii uniemożliwia ataku jest tooverify, który hello `resource_id` dopasowań hello base hello sieci web adres URL interfejsu API, który uzyskiwany. Na przykład, jeśli jest uzyskiwany https://service.contoso.com/data hello `resource_id` może być htttps://service.contoso.com/. Aplikacja kliencka Hello musi odrzucania `resource_id` nie zaczynające się od podstawowego adresu URL hello chyba, że jest identyfikatorem hello tooverify niezawodnej alternatywny sposób. |

#### Kody błędów schematu elementu nośnego
Witaj specyfikacji RFC 6750 definiuje następujące błędy zasobów, które użycia nagłówka WWW-Authenticate hello i schematu elementu nośnego w odpowiedzi hello hello.

| Kod stanu HTTP | Kod błędu: | Opis | Akcja klienta |
| --- | --- | --- | --- |
| 400 |invalid_request |Witaj żądania nie jest poprawnie sformułowany. Na przykład może być brak parametru lub przy użyciu hello tego samego parametru dwa razy. |Usuń błąd hello i ponów żądanie hello. Tego typu błędu powinien wystąpić tylko podczas programowania i wykryty w początkowej testowania. |
| 401 |invalid_token |token dostępu Hello jest brakujące, nieprawidłowe lub został odwołany. wartość Hello hello error_description parametru zapewnia dodatkowe szczegóły. |Zażądać nowego tokenu z powitania serwera autoryzacji. Jeśli nowy token hello nie powiedzie się, wystąpił nieoczekiwany błąd. Wysyłanie użytkownika toohello komunikat błędu i ponów próbę po losowego opóźnienia. |
| 403 |insufficient_scope |token dostępu Hello nie zawiera hello personifikacji uprawnienia wymagane tooaccess hello zasobu. |Wysłać nowe żądanie toohello autoryzacji punktu końcowego autoryzacji. Jeśli odpowiedź hello zawiera parametr zakresu hello, należy użyć wartości zakresu hello w zasobie toohello żądania hello. |
| 403 |insufficient_access |temat Hello hello tokenu nie ma hello uprawnienia, które są wymagane tooaccess hello zasobów. |Witaj Monituj użytkownika toouse innego konta lub toohello uprawnienia toorequest określony zasób. |

## Odświeżanie hello tokeny dostępu
Tokeny dostępu są krótkim okresie i musi zostać odświeżona po wygasną toocontinue uzyskiwania dostępu do zasobów. Można odświeżać hello `access_token` poprzez przesłanie innego `POST` żądania toohello `/token` punktu końcowego, ale teraz podając hello `refresh_token` zamiast hello `code`.

Odśwież tokenów nie ma określonego okresy istnienia. Zazwyczaj hello okresy istnienia tokenów odświeżania są stosunkowo długo. Jednak w niektórych przypadkach tokenów odświeżania wygaśnie, były odwołane lub Brak wystarczających uprawnień dla akcji hello potrzebne. Aplikacja wymaga tooexpect i uchwytem błędy zwrócone przez punkt końcowy wydawania tokenów hello poprawnie.

Po otrzymaniu odpowiedzi z powodu błędu tokenu odświeżania odrzucić bieżący token odświeżania hello i poproś o nowy kod autoryzacji lub tokenu dostępu. W szczególności, gdy przy użyciu odświeżenia token w hello przepływ udzielania kodu autoryzacji, jeśli otrzymasz odpowiedź z hello `interaction_required` lub `invalid_grant` kody błędów, Odrzuć hello token odświeżania i poproś o nowy kod autoryzacji.

Toohello żądania próbki **specyficznego dla dzierżawy** punktu końcowego (można również użyć hello **wspólnej** punktu końcowego) tooget nowy token dostępu za pomocą tokenu odświeżania wygląda następująco:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&grant_type=refresh_token
&resource=https%3A%2F%2Fservice.contoso.com%2F
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

### Odpowiedź oznaczająca Powodzenie
Odpowiedź oznaczająca Powodzenie tokenu będą wyglądać jak:

```
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1460404526",
  "resource": "https://service.contoso.com/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1THdqcHdBSk9NOW4tQSJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0MDg2MywibmJmIjoxMzg4NDQwODYzLCJleHAiOjEzODg0NDQ3NjMsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6IjY4Mzg5YWUyLTYyZmEtNGIxOC05MWZlLTUzZGQxMDlkNzRmNSIsInVwbiI6ImZyYW5rbUBjb250b3NvLmNvbSIsInVuaXF1ZV9uYW1lIjoiZnJhbmttQGNvbnRvc28uY29tIiwic3ViIjoiZGVOcUlqOUlPRTlQV0pXYkhzZnRYdDJFYWJQVmwwQ2o4UUFtZWZSTFY5OCIsImZhbWlseV9uYW1lIjoiTWlsbGVyIiwiZ2l2ZW5fbmFtZSI6IkZyYW5rIiwiYXBwaWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctODkwYS0yNzRhNzJhNzMwOWUiLCJhcHBpZGFjciI6IjAiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJhY3IiOiIxIn0.JZw8jC0gptZxVC-7l5sFkdnJgP3_tRjeQEPgUn28XctVe3QqmheLZw7QVZDPCyGycDWBaqy7FLpSekET_BftDkewRhyHk9FW_KeEz0ch2c3i08NGNDbr6XYGVayNuSesYk5Aw_p3ICRlUV1bqEwk-Jkzs9EEkQg4hbefqJS6yS1HoV_2EsEhpd_wCQpxK89WPs3hLYZETRJtG5kvCCEOvSHXmDE6eTHGTnEgsIk--UlPe275Dvou4gEAwLofhLDQbMSjnlV5VLsjimNBVcSRFShoxmQwBJR_b2011Y5IuD6St5zPnzruBbZYkGNurQK63TJPWmRd3mbJsGM0mf3CUQ",
  "refresh_token": "AwABAAAAv YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfcUl4VBbiSHZyd1NVZG5QTIOcbObu3qnLutbpadZGAxqjIbMkQ2bQS09fTrjMBtDE3D6kSMIodpCecoANon9b0LATkpitimVCrl PM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4rTfgV29ghDOHRc2B-C_hHeJaJICqjZ3mY2b_YNqmf9SoAylD1PycGCB90xzZeEDg6oBzOIPfYsbDWNf621pKo2Q3GGTHYlmNfwoc-OlrxK69hkha2CF12azM_NYhgO668yfmVCrl-NyfN3oyG4ZCWu18M9-vEou4Sq-1oMDzExgAf61noxzkNiaTecM-Ve5cq6wHqYQjfV9DOz4lbceuYCAA"
}
```
| Parametr | Opis |
| --- | --- |
| token_type |Typ tokenu Hello. wartość Hello tylko obsługiwane jest **elementu nośnego**. |
| expires_in |Witaj pozostały okres istnienia tokenu hello w sekundach. Typowe wartości to 3600 (jedna godzina). |
| expires_on |Witaj daty i godziny, na którym wygaśnięcia tokenu hello. Data Hello jest reprezentowany jako hello liczbę sekund z rokiem 1970-01-01T0:0:0Z UTC czasu wygaśnięcia hello. |
| Zasobów |Identyfikuje hello zabezpieczonych zasobów hello tokenu dostępu mogą być używane tooaccess. |
| Zakres |Aplikację native client toohello przyznane uprawnienia personifikacji. uprawnienia domyślne Hello jest **user_impersonation**. właściciel zasobu docelowego hello Hello można zarejestrować alternatywne wartości w usłudze Azure AD. |
| ' access_token ' |Witaj nowego tokenu dostępu, który odebrał żądanie. |
| refresh_token |Nowe refresh_token OAuth 2.0, które mogą być używane toorequest nowe tokeny dostępu po wygaśnięciu hello jedną w tej odpowiedzi. |

### Odpowiedzi na błąd
Przykładowa odpowiedź błędu może wyglądać następująco:

```
{
  "error": "invalid_resource",
  "error_description": "AADSTS50001: hello application named https://foo.microsoft.com/mail.read was not found in hello tenant named 295e01fc-0c56-4ac3-ac57-5d0ed568f872.  This can happen if hello application has not been installed by hello administrator of hello tenant or consented tooby any user in hello tenant.  You might have sent your authentication request toohello wrong tenant.\r\nTrace ID: ef1f89f6-a14f-49de-9868-61bd4072f0a9\r\nCorrelation ID: b6908274-2c58-4e91-aea9-1f6b9c99347c\r\nTimestamp: 2016-04-11 18:59:01Z",
  "error_codes": [
    50001
  ],
  "timestamp": "2016-04-11 18:59:01Z",
  "trace_id": "ef1f89f6-a14f-49de-9868-61bd4072f0a9",
  "correlation_id": "b6908274-2c58-4e91-aea9-1f6b9c99347c"
}
```

| Parametr | Opis |
| --- | --- |
| error |Ciąg kodu błędu mogą być używane tooclassify typów błędów występujących, która może być używana tooreact tooerrors. |
| error_description |Komunikat o błędzie, które mogą ułatwić dewelopera zidentyfikować hello głównej przyczyny błędu uwierzytelniania. |
| error_codes |Lista specyficzne dla usługi STS kody błędów, które mogą pomóc w diagnostyce. |
| sygnatura czasowa |czas Hello, w którym wystąpił błąd hello. |
| trace_id |Unikatowy identyfikator dla żądania hello, które mogą pomóc w diagnostyce. |
| correlation_id |Unikatowy identyfikator dla żądania hello, które mogą pomóc w diagnostyce między składnikami. |

Opis i kody błędów hello hello zalecana Akcja klienta, zobacz [kody błędów dla błędów punktu końcowego tokena](#error-codes-for-token-endpoint-errors).
