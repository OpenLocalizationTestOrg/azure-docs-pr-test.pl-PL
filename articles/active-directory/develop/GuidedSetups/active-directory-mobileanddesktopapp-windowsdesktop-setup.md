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
## <a name="set-up-your-project"></a><span data-ttu-id="fd224-103">Konfigurowanie projektu</span><span class="sxs-lookup"><span data-stu-id="fd224-103">Set up your project</span></span>

<span data-ttu-id="fd224-104">Ta sekcja zawiera instrukcje krok po kroku toocreate nowe toodemonstrate projektu jak toointegrate .NET pulpitu systemu Windows aplikacji (XAML) z *logowania z firmą Microsoft* aby mogła zbadać interfejsów API sieci Web, która wymaga tokenu.</span><span class="sxs-lookup"><span data-stu-id="fd224-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="fd224-105">Aplikacja Hello utworzone przez ten przewodnik przedstawia przycisk toograph i Pokaż wyników na ekranie i przycisk wylogowania.</span><span class="sxs-lookup"><span data-stu-id="fd224-105">hello application created by this guide exposes a button toograph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="fd224-106">Preferowane projektu Visual Studio tego przykładu toodownload zamiast niego?</span><span class="sxs-lookup"><span data-stu-id="fd224-106">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="fd224-107">[Pobieranie projektu](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) i pominąć toohello [kroku konfiguracji](#create-an-application-express) przykładowy kod hello tooconfigure przed wykonaniem.</span><span class="sxs-lookup"><span data-stu-id="fd224-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="fd224-108">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="fd224-108">Create your application</span></span>
1. <span data-ttu-id="fd224-109">W programie Visual Studio:`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="fd224-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="fd224-110">W obszarze *szablony*, wybierz pozycję`Visual C#`</span><span class="sxs-lookup"><span data-stu-id="fd224-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="fd224-111">Wybierz `WPF App` (lub *aplikacji WPF* w zależności od wersji hello programu Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="fd224-111">Select `WPF App` (or *WPF Application* depending on hello version of your Visual Studio)</span></span>

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="fd224-112">Dodaj projekt tooyour biblioteki uwierzytelniania firmy Microsoft (MSAL) hello</span><span class="sxs-lookup"><span data-stu-id="fd224-112">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1. <span data-ttu-id="fd224-113">W programie Visual Studio:`Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="fd224-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="fd224-114">Skopiuj/Wklej następujący hello w oknie konsoli Menedżera pakietów hello:</span><span class="sxs-lookup"><span data-stu-id="fd224-114">Copy/paste hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="fd224-115">Pakiet HELLO powyżej instaluje hello biblioteki uwierzytelniania firmy Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="fd224-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="fd224-116">MSAL obsługuje pobieranie, buforowanie i odświeżanie użytkownika tooaccess toskens używać interfejsów API chronione przez usługi Azure Active Directory w wersji 2.</span><span class="sxs-lookup"><span data-stu-id="fd224-116">MSAL handles acquiring, caching and refreshing user toskens used tooaccess APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-hello-code-tooinitialize-msal"></a><span data-ttu-id="fd224-117">Dodaj hello kodu tooinitialize MSAL</span><span class="sxs-lookup"><span data-stu-id="fd224-117">Add hello code tooinitialize MSAL</span></span>
<span data-ttu-id="fd224-118">Ten krok ułatwia tworzenie interakcji toohandle klasy z biblioteki MSAL, takie jak Obsługa tokenów.</span><span class="sxs-lookup"><span data-stu-id="fd224-118">This step will help you create a class toohandle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="fd224-119">Otwórz hello `App.xaml.cs` i Dodaj odwołanie hello MSAL biblioteki toohello klasy:</span><span class="sxs-lookup"><span data-stu-id="fd224-119">Open hello `App.xaml.cs` file and add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="fd224-120">Zaktualizuj następujące toohello klasy aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="fd224-120">Update hello App class toohello following:</span></span>
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

## <a name="create-your-applications-ui"></a><span data-ttu-id="fd224-121">Tworzenie aplikacji interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="fd224-121">Create your application’s UI</span></span>
<span data-ttu-id="fd224-122">Poniższa sekcja Hello pokazuje, jak aplikacja może zapytać serwera chronionego wewnętrznej bazy danych, takich jak Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="fd224-122">hello section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="fd224-123">Plik MainWindow.xaml należy utworzyć automatycznie w ramach szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="fd224-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="fd224-124">Otwórz ten plik ten plik, a następnie wykonaj poniższe instrukcje hello:</span><span class="sxs-lookup"><span data-stu-id="fd224-124">Open this file this file and then follow hello instructions below:</span></span>

<span data-ttu-id="fd224-125">Zastąp aplikacji `<Grid>` być hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="fd224-125">Replace your application’s `<Grid>` with be hello following:</span></span>

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
