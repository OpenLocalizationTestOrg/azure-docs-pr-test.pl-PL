---
title: "Usługi Azure AD v2 Windows Desktop pobieranie rozpoczęte — Konfiguracja | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 4065727aef04d7969d438c6ef79127bb44568be1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="2d645-103">Konfigurowanie projektu</span><span class="sxs-lookup"><span data-stu-id="2d645-103">Set up your project</span></span>

<span data-ttu-id="2d645-104">Ta sekcja zawiera instrukcje krok po kroku dotyczące sposobu tworzenia nowego projektu aby zademonstrować sposób integracji aplikacji .NET pulpitu systemu Windows (XAML) z *logowania z firmą Microsoft* aby mogła zbadać interfejsów API sieci Web, która wymaga tokenu.</span><span class="sxs-lookup"><span data-stu-id="2d645-104">This section provides step-by-step instructions for how to create a new project to demonstrate how to integrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="2d645-105">Aplikacji utworzonych przez ten przewodnik przedstawia przycisk Wykres i wyświetlić wyniki na ekranie i przycisk wylogowania.</span><span class="sxs-lookup"><span data-stu-id="2d645-105">The application created by this guide exposes a button to graph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="2d645-106">Preferowane jest zamiast tego Pobierz ten przykładowy projekt programu Visual Studio?</span><span class="sxs-lookup"><span data-stu-id="2d645-106">Prefer to download this sample's Visual Studio project instead?</span></span> <span data-ttu-id="2d645-107">[Pobieranie projektu](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) i przejść [kroku konfiguracji](#create-an-application-express) skonfigurować przykładowy kod przed wykonaniem.</span><span class="sxs-lookup"><span data-stu-id="2d645-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="2d645-108">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="2d645-108">Create your application</span></span>
1. <span data-ttu-id="2d645-109">W programie Visual Studio:`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="2d645-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="2d645-110">W obszarze *szablony*, wybierz pozycję`Visual C#`</span><span class="sxs-lookup"><span data-stu-id="2d645-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="2d645-111">Wybierz `WPF App` (lub *aplikacji WPF* w zależności od wersji programu Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="2d645-111">Select `WPF App` (or *WPF Application* depending on the version of your Visual Studio)</span></span>

## <a name="add-the-microsoft-authentication-library-msal-to-your-project"></a><span data-ttu-id="2d645-112">Dodaj do projektu biblioteki uwierzytelniania firmy Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="2d645-112">Add the Microsoft Authentication Library (MSAL) to your project</span></span>
1. <span data-ttu-id="2d645-113">W programie Visual Studio:`Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="2d645-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="2d645-114">Skopiuj/Wklej następujące opcje w oknie Konsola Menedżera pakietów:</span><span class="sxs-lookup"><span data-stu-id="2d645-114">Copy/paste the following in the Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="2d645-115">Powyżej pakiet instaluje biblioteki uwierzytelniania firmy Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="2d645-115">The package above installs the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="2d645-116">MSAL obsługuje pobieranie, buforowanie i odświeżanie toskens użytkownika, które umożliwiają dostęp do interfejsów API chronione przez usługi Azure Active Directory w wersji 2.</span><span class="sxs-lookup"><span data-stu-id="2d645-116">MSAL handles acquiring, caching and refreshing user toskens used to access APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-the-code-to-initialize-msal"></a><span data-ttu-id="2d645-117">Dodaj kod, aby zainicjować MSAL</span><span class="sxs-lookup"><span data-stu-id="2d645-117">Add the code to initialize MSAL</span></span>
<span data-ttu-id="2d645-118">Ten krok ułatwia tworzenie klasy do obsługi interakcji z biblioteką MSAL, takie jak Obsługa tokenów.</span><span class="sxs-lookup"><span data-stu-id="2d645-118">This step will help you create a class to handle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="2d645-119">Otwórz `App.xaml.cs` plik i dodać odwołanie do biblioteki MSAL do klasy:</span><span class="sxs-lookup"><span data-stu-id="2d645-119">Open the `App.xaml.cs` file and add the reference for MSAL library to the class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="2d645-120">Aktualizacja klasy aplikacji do następującego:</span><span class="sxs-lookup"><span data-stu-id="2d645-120">Update the App class to the following:</span></span>
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is the clientId of your app registration. 
    //You have to replace the below with the Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a><span data-ttu-id="2d645-121">Tworzenie aplikacji interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="2d645-121">Create your application’s UI</span></span>
<span data-ttu-id="2d645-122">Poniższa sekcja przedstawia, jak aplikacja może zapytać serwera chronionego wewnętrznej bazy danych, takich jak Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="2d645-122">The section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="2d645-123">Plik MainWindow.xaml należy utworzyć automatycznie w ramach szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="2d645-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="2d645-124">Otwórz ten plik ten plik, a następnie postępuj zgodnie z instrukcjami poniżej:</span><span class="sxs-lookup"><span data-stu-id="2d645-124">Open this file this file and then follow the instructions below:</span></span>

<span data-ttu-id="2d645-125">Zastąp aplikacji `<Grid>` być następujące:</span><span class="sxs-lookup"><span data-stu-id="2d645-125">Replace your application’s `<Grid>` with be the following:</span></span>

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
