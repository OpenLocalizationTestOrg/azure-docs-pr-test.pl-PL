---
title: aaaMFA software development kit aplikacji niestandardowych | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak toodownload i użyj hello weryfikacji dwuetapowej tooenable zestawu SDK usługi Azure MFA dla aplikacji niestandardowych."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a>Tworzenie usługi Multi-Factor Authentication w aplikacje niestandardowe (SDK)

Transakcja procesów aplikacji w dzierżawie usługi Azure AD lub hello Hello Azure Multi-Factor Authentication Software Development Kit (SDK) umożliwia tworzenie weryfikacji dwuetapowej bezpośrednio do logowania.

Witaj SDK usługi Multi-Factor Authentication jest dostępna w C#, Visual Basic (.NET), Java, Perl, PHP i Ruby. Witaj SDK udostępnia alokowania otokę weryfikacji dwuetapowej. Obejmuje on wszystko, co potrzebne toowrite kodu, w tym pliki kodu źródłowego komentarze, przykładowe pliki i szczegółowe plik ReadMe. Każdy zestaw SDK zawiera również certyfikat i klucz prywatny szyfrowania transakcje, które są unikatowe tooyour dostawca uwierzytelniania MFA. Tak długo, jak długo ma dostawcy, możesz pobrać hello zestawu SDK w formatach i języków tyle zgodnie z potrzebami.

Struktura Hello hello interfejsów API w hello SDK usługi Multi-Factor Authentication jest proste. Należy wywołać interfejs API tooan hello opcja wieloskładnikowego parametrów (takie jak tryb weryfikacji) i danych użytkownika (na przykład toocall numeru telefonu hello lub toovalidate numer PIN hello) jednej funkcji. Witaj interfejsów API wykonuje wywołanie funkcji hello toohello żądania usługi sieci web opartej na chmurze usługi systemu Azure Multi-Factor Authentication. Wszystkie wywołania musi zawierać certyfikatu prywatnego toohello odwołania, który znajduje się w każdym zestawu SDK.

Ponieważ hello interfejsów API nie mają toousers access zarejestrowane w usłudze Azure Active Directory, musisz podać informacje o użytkowniku w pliku lub bazy danych. Hello interfejsów API oferuje również funkcje zarządzania rejestracji lub użytkownika, więc należy toobuild tych procesów do aplikacji.

> [!IMPORTANT]
> toodownload hello zestawu SDK, należy toocreate dostawcy usługi Azure Multi-Factor Authentication, nawet jeśli użytkownik ma licencje usługi Azure MFA, usługi AAD Premium lub pakietu EMS. W tym celu należy utworzyć dostawcy usługi Azure Multi-Factor Authentication, a już licencji, należy się hello toocreate dostawcy z hello **każdego włączonego użytkownika** modelu. Następnie połącz hello dostawcy toohello katalog, który zawiera hello licencje usługi Azure MFA, Azure AD Premium lub pakietu EMS. Taka konfiguracja powoduje, że rozliczenie jest przeprowadzane tylko jeśli masz więcej unikatowych użytkowników przy użyciu hello SDK niż hello liczbę licencji użytkownika.


## <a name="download-hello-sdk"></a>Pobierz hello zestawu SDK
Pobieranie hello zestawu SDK usługi Azure Multi-Factor wymaga [dostawcy uwierzytelniania wieloskładnikowego Azure](multi-factor-authentication-get-started-auth-provider.md).  Wymaga pełnej Azure subskrypcji, nawet jeśli należą do firmy licencje usługi Azure MFA, Azure AD Premium lub pakietu Enterprise Mobility Suite.  Witaj toodownload zestawu SDK, przejdź toohello Portal zarządzania usługą Multi-Factor. Hello portal można osiągnąć przez zarządzanie hello dostawcy uwierzytelniania wieloskładnikowego bezpośrednio lub przez kliknięcie przycisku hello **"Portal toohello Przejdź"** łącze na stronie ustawień usługi MFA hello.

### <a name="download-from-hello-azure-classic-portal"></a>Pobierz z hello klasycznego portalu Azure
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com) jako Administrator.
2. Po lewej stronie powitania, wybierz **usługi Active Directory**.
3. Na stronie usługi Active Directory hello na górnym umożliwia hello **dostawców uwierzytelniania wieloskładnikowego**
4. U dołu hello wybierz **Zarządzaj**. Zostanie otwarta nowa strona.
5. Na powitania po lewej, u dołu hello kliknij **SDK**.
   <center>![Pobierz](./media/multi-factor-authentication-sdk/download.png)</center>
6. Wybierz język hello i kliknij jeden łączy do pobierania hello.
7. Zapisz hello pobierania.

### <a name="download-from-hello-service-settings"></a>Pobierz z hello ustawienia usługi
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com) jako Administrator.
2. Po lewej stronie powitania, wybierz **usługi Active Directory**.
3. Kliknij dwukrotnie wystąpienie usługi Azure AD.
4. Na powitania kliknij górny **Konfiguruj**
5. W obszarze usługi Multi-Factor authentication, zaznacz **Zarządzaj ustawieniami usługi**
   ![Pobierz](./media/multi-factor-authentication-sdk/download2.png)
6. Na stronie ustawień usługi hello u dołu ekranu hello powitania kliknij **Przejdź toohello portal**. Zostanie otwarta nowa strona.
   ![Pobieranie](./media/multi-factor-authentication-sdk/download3a.png)
7. Na powitania po lewej, u dołu hello kliknij **SDK**.
8. Wybierz język hello i kliknij jeden łączy do pobierania hello.
9. Zapisz hello pobierania.

## <a name="whats-in-hello-sdk"></a>Co to jest w hello zestawu SDK
Witaj zestaw SDK zawiera hello następujące elementy:

* **PLIK README**. W tym artykule wyjaśniono, jak toouse hello interfejsy API uwierzytelniania wieloskładnikowego w nowej lub istniejącej aplikacji.
* **Pliki źródłowe** uwierzytelnianie wieloskładnikowe
* **Certyfikat klienta** użyć toocommunicate z hello usługi Multi-Factor Authentication
* **Klucz prywatny** hello certyfikatu
* **Wyniki wywołania.** Lista kody rezultatów połączeń. tooopen ten plik, użyj aplikacji przy użyciu tekstu, takich jak program WordPad. Użyj hello wywołać tootest kody wyników i rozwiązywania problemów z hello stosowania uwierzytelniania wieloskładnikowego w aplikacji. Nie są one kodów stanu uwierzytelniania.
* **Przykłady.** Przykładowy kod Podstawowa implementacja pracy usługi Multi-Factor Authentication.

> [!WARNING]
> certyfikat klienta na powitania jest unikatowy certyfikat prywatny wygenerowany specjalnie dla Ciebie. Udostępnij lub nie utracić tego pliku. Jest tooensuring klucza zabezpieczeń hello komunikacji z usługą Multi-Factor Authentication hello.

## <a name="code-sample"></a>Przykład kodu
Ten przykładowy kod przedstawia sposób toouse hello interfejsów API w hello Azure Multi-Factor Authentication SDK tooadd Tryb standardowy głosu wywoływania aplikacji tooyour weryfikacji. Telefon hello użytkownika odpowiada tooby naciśnięcie klawisza # hello jest tryb standardowy.

W tym przykładzie użyto hello C# .NET 2.0 SDK usługi Multi-Factor Authentication w podstawowej aplikacji ASP.NET w logice C# po stronie serwera, ale hello proces jest podobny w innych językach. Ponieważ hello zestaw SDK zawiera pliki źródłowe, pliki wykonywalne nie można skompilować plików hello i odwoływać je lub umieścić je bezpośrednio w aplikacji.

> [!NOTE]
> Podczas wdrażania usługi Multi-Factor Authentication, użyj hello dodatkowe metody (Rozmowa telefoniczna lub wiadomości tekstowej) jako dodatkowej lub trzeciorzędny weryfikacji toosupplement metodę uwierzytelniania podstawowego (nazwa użytkownika i hasło). Te metody nie są zaprojektowane jako metody uwierzytelniania podstawowego.

### <a name="code-sample-overview"></a>Omówienie przykładowy kod
Ten przykładowy kod dla prostą aplikację sieci web pokaz używa połączenia telefonicznego z uwierzytelnianiem # klucza odpowiedzi tooverify hello użytkownika. Współczynnik ten telefon jest określany w usłudze Multi-Factor Authentication jako tryb standardowy.

Hello kod po stronie klienta nie ma żadnych elementów specyficznych dla usługi Multi-Factor Authentication. Ponieważ hello dodatkowych czynników autoryzacji są niezależne od hello podstawowego uwierzytelniania, można dodawać je bez zmieniania hello istniejącego logowania interfejsu. Hello interfejsów API w hello SDK Multi-Factor umożliwiają dostosowanie hello środowisko użytkownika, ale może nie być konieczny toochange niczego w ogóle.

Kod po stronie serwera Hello dodaje Tryb standardowy uwierzytelniania w kroku 2. Tworzy obiekt PfAuthParams z parametrami hello, które są wymagane do weryfikacji Tryb standardowy: nazwa_użytkownika, telefonu numer i tryb i hello ścieżki toohello certyfikatu klienta (CertFilePath), który jest wymagany w każdym wywołaniu. Aby demonstracyjne wszystkich parametrów w PfAuthParams, zobacz hello przykładowy plik w hello zestawu SDK.

Następnie kod hello przekazuje hello PfAuthParams obiektu toohello pf_authenticate() funkcji. Wartość zwracana Hello wskazuje hello powodzenie lub niepowodzenie uwierzytelniania hello. Witaj parametrów, callStatus oraz identyfikator błędu, zawierają informacje wynik wywołania dodatkowe. kody rezultatów połączeń Hello są udokumentowane w pliku wyników wywołania hello w hello zestawu SDK.

Ta implementacja minimalnego można pisać w zaledwie kilku wierszach. Jednak w kodzie produkcyjnym, można dołączyć dokładniejsze obsługi błędów kodu dodatkowej bazy danych i lepszą obsługę użytkowników.

### <a name="web-client-code"></a>Kod klienta sieci Web
Oto Hello kodu klienta sieci web dla strony pokaz.

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a>Kod po stronie serwera
Uwierzytelnianie wieloskładnikowe hello następującego kodu po stronie serwera, jest skonfigurowany i uruchamiania w kroku 2. Rozmowy telefonicznej użytkownika hello toowhich odpowiada naciskając klawisz # hello jest tryb standardowy (MODE_STANDARD).

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
