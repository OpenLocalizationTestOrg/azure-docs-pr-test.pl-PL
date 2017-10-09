---
title: "aaaAzure AD v2 Windows Desktop wprowadzenie — Instalator | Dokumentacja firmy Microsoft"
description: "Jak aplikacje .NET pulpitu systemu Windows (XAML) można wywołać interfejsu API, które wymagają tokenów dostępu przez punkt końcowy w wersji 2 usługi Azure Active Directory"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 097ea99bef01e15edaa5ff914ff4e18392b77c5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Konfigurowanie projektu

Ta sekcja zawiera instrukcje krok po kroku toocreate nowe toodemonstrate projektu jak toointegrate .NET pulpitu systemu Windows aplikacji (XAML) z *logowania z firmą Microsoft* aby mogła zbadać interfejsów API sieci Web, która wymaga tokenu.

Aplikacja Hello utworzone przez ten przewodnik przedstawia przycisk toograph i Pokaż wyników na ekranie i przycisk wylogowania.

> Preferowane projektu Visual Studio tego przykładu toodownload zamiast niego? [Pobieranie projektu](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) i pominąć toohello [kroku konfiguracji](#create-an-application-express) przykładowy kod hello tooconfigure przed wykonaniem.


### <a name="create-your-application"></a>Tworzenie aplikacji
1. W programie Visual Studio:`File` > `New` > `Project`<br/>
2. W obszarze *szablony*, wybierz pozycję`Visual C#`
3. Wybierz `WPF App` (lub *aplikacji WPF* w zależności od wersji hello programu Visual Studio)

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Dodaj projekt tooyour biblioteki uwierzytelniania firmy Microsoft (MSAL) hello
1. W programie Visual Studio:`Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Skopiuj/Wklej następujący hello w oknie konsoli Menedżera pakietów hello:

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> Pakiet HELLO powyżej instaluje hello biblioteki uwierzytelniania firmy Microsoft (MSAL). MSAL obsługuje pobieranie, buforowanie i odświeżanie użytkownika tooaccess toskens używać interfejsów API chronione przez usługi Azure Active Directory w wersji 2.

## <a name="add-hello-code-tooinitialize-msal"></a>Dodaj hello kodu tooinitialize MSAL
Ten krok ułatwia tworzenie interakcji toohandle klasy z biblioteki MSAL, takie jak Obsługa tokenów.

1. Otwórz hello `App.xaml.cs` i Dodaj odwołanie hello MSAL biblioteki toohello klasy:

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Zaktualizuj następujące toohello klasy aplikacji hello:
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is hello clientId of your app registration. 
    //You have tooreplace hello below with hello Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a>Tworzenie aplikacji interfejsu użytkownika
Poniższa sekcja Hello pokazuje, jak aplikacja może zapytać serwera chronionego wewnętrznej bazy danych, takich jak Microsoft Graph. Plik MainWindow.xaml należy utworzyć automatycznie w ramach szablonu projektu. Otwórz ten plik ten plik, a następnie wykonaj poniższe instrukcje hello:

Zastąp aplikacji `<Grid>` być hello poniżej:

```xml
<Grid>
    <StackPanel Background="Azure">
        <StackPanel Orientation="Horizontal" HorizontalAlignment="Right">
            <Button x:Name="CallGraphButton" Content="Call Microsoft Graph API" HorizontalAlignment="Right" Padding="5" Click="CallGraphButton_Click" Margin="5" FontFamily="Segoe Ui"/>
            <Button x:Name="SignOutButton" Content="Sign-Out" HorizontalAlignment="Right" Padding="5" Click="SignOutButton_Click" Margin="5" Visibility="Collapsed" FontFamily="Segoe Ui"/>
        </StackPanel>
        <Label Content="API Call Results" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="ResultText" TextWrapping="Wrap" MinHeight="120" Margin="5" FontFamily="Segoe Ui"/>
        <Label Content="Token Info" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="TokenInfoText" TextWrapping="Wrap" MinHeight="70" Margin="5" FontFamily="Segoe Ui"/>
    </StackPanel>
</Grid>
```
