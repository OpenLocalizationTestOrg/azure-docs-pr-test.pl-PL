
## <a name="set-up-your-project"></a>Konfigurowanie projektu

W tej sekcji Utwórz nowy projekt w celu zademonstrowania sposobu integracji aplikacji .NET pulpitu systemu Windows (XAML) z *logowania z firmą Microsoft* , dzięki czemu aplikacja może wysyłać zapytania interfejsów API sieci Web, które wymagają tokenu.

Przycisk, które są używane do wywoływania wykresu, obszar, aby wyświetlić wyniki na ekranie, a przycisk wylogowania wyświetlane w aplikacji, utworzonej za pomocą tego przewodnika.

> [!NOTE]
> Preferowane jest zamiast tego Pobierz ten przykładowy projekt programu Visual Studio? [Pobieranie projektu](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip)i przejdź do [kroku konfiguracji](#create-an-application-express) do skonfigurowania przykładowy kod, przed jego wykonania.
>

Aby utworzyć aplikację, wykonaj następujące czynności:
1. W programie Visual Studio, wybierz **pliku** > **nowy** > **projektu**.
2. W obszarze **szablony**, wybierz pozycję **Visual C#**.
3. Wybierz **aplikacji WPF** lub **aplikacji WPF**, w zależności od wersji programu Visual Studio w wersji używasz.

## <a name="add-msal-to-your-project"></a>Dodaj MSAL do projektu
1. W programie Visual Studio, wybierz **narzędzia** > **Menedżera pakietów NuGet**> **Konsola Menedżera pakietów**.
2. W oknie Konsola Menedżera pakietów Wklej następującego polecenia programu Azure PowerShell:

    ```powershell
    Install-Package Microsoft.Identity.Client -Pre
    ```

    > [!NOTE] 
    > To polecenie powoduje zainstalowanie biblioteki uwierzytelniania firmy Microsoft. MSAL obsługuje pobieranie, buforowanie i odświeżanie tokenów użytkownika, które umożliwiają dostęp do interfejsów API, które są chronione przez usługi Azure Active Directory w wersji 2.
    >

## <a name="add-the-code-to-initialize-msal"></a>Dodaj kod, aby zainicjować MSAL
W tym kroku możesz utworzyć klasę do obsługi interakcji z MSAL, takie jak Obsługa tokenów.

1. Otwórz *App.xaml.cs* pliku, a następnie dodaj odwołanie do MSAL do klasy:

    ```csharp
    using Microsoft.Identity.Client;
    ```
<!-- Workaround for Docs conversion bug -->

2. Aktualizacja klasy aplikacji do następującego:

    ```csharp
    public partial class App : Application
    {
        //Below is the clientId of your app registration. 
        //You have to replace the below with the Application Id for your app registration
        private static string ClientId = "your_client_id_here";

        public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

    }
    ```

## <a name="create-the-application-ui"></a>Tworzenie aplikacji interfejsu użytkownika
W tej sekcji przedstawiono, jak aplikacja może zapytać chronionego serwera zaplecza, takich jak Microsoft Graph. 

A *MainWindow.xaml* automatycznie można utworzyć pliku w ramach szablonu projektu. Otwórz ten plik, a następnie zastąp aplikacji  *\<siatki >* węzła z następującym kodem:

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

