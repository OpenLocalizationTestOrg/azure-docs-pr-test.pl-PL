---
title: "aaaSet zapasowej Azure Key Vault z rotacją kluczy end-to-end i inspekcji | Dokumentacja firmy Microsoft"
description: "Użyj tego jak tootoohelp, Pobierz skonfigurowane z rotacją kluczy i monitorowania dzienniki magazynu kluczy."
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a>Konfigurowanie kompleksowej wymiany i inspekcji kluczy w usłudze Azure Key Vault
## <a name="introduction"></a>Wprowadzenie
Po utworzeniu magazynu kluczy, będzie możliwe toostart przy użyciu tego toostore magazynu kluczy i kluczy tajnych. Aplikacje nie muszą już toopersist Twojego kluczy ani kluczy tajnych, ale raczej zażąda je z magazynu kluczy hello zgodnie z potrzebami. Dzięki temu można tooupdate kluczy i kluczy tajnych bez wpływu na powitania zachowanie aplikacji, która otwiera szerokości możliwości wokół klucza, a tajny zarządzania.

W tym artykule przedstawiono przykład użycia usługi Azure Key Vault toostore klucz tajny, w tym przypadku klucz konta magazynu Azure, który jest dostępny przez aplikację. Ilustruje też implementacji zaplanowane obrotu tego klucza konta magazynu. Na koniec przeprowadzi przez Pokaz sposobu toomonitor hello dzienników inspekcji magazynu kluczy i zgłaszanie alertów po nieoczekiwany żądań.

> [!NOTE]
> W tym samouczku nie jest zamierzone tooexplain szczegółów hello początkowej konfiguracji magazynu kluczy. Te informacje można znaleźć w temacie [Rozpoczynanie pracy z usługą Azure Key Vault](key-vault-get-started.md). Aby uzyskać instrukcje Międzyplatformowego interfejsu wiersza polecenia, zobacz [Zarządzanie Key Vault przy użyciu interfejsu wiersza polecenia](key-vault-manage-with-cli2.md).
>
>

## <a name="set-up-key-vault"></a>Konfigurowanie usługi Key Vault
tooenable tooretrieve aplikacji klucza tajnego z magazynu kluczy, należy najpierw utworzyć klucz tajny hello i przekaż go tooyour magazynu. Można to zrobić przez uruchamianie sesji programu PowerShell systemu Azure i zalogowanie tooyour konto platformy Azure z hello następujące polecenie:

```powershell
Login-AzureRmAccount
```

W oknie wyskakującym przeglądarki hello wprowadź nazwę użytkownika konta platformy Azure i hasło. PowerShell pobierze wszystkie subskrypcje hello, które są skojarzone z tym kontem. Używa programu PowerShell hello pierwszego domyślnie.

Jeśli masz wiele subskrypcji może być toospecify Witaj, który został użyty toocreate Twojego magazynu kluczy. Wprowadź powitania po toosee hello subskrypcje dla swojego konta:

```powershell
Get-AzureRmSubscription
```

toospecify hello subskrypcji, która jest skojarzona z magazynem kluczy hello, który będziesz rejestrować, wpisz:

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

Ponieważ w tym artykule przedstawiono przechowywania jako klucz tajny klucz konta magazynu, należy pobrać ten klucz konta magazynu.

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

Po pobraniu klucz tajny (w tym przypadku klucz konta magazynu), należy przekonwertować tej tooa bezpieczny ciąg, a następnie utwórz klucz tajny z daną wartością, w magazynie kluczy.

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
Następnie Pobierz hello identyfikatora URI dla hello klucz tajny, który został utworzony. Służy to w kolejnym kroku podczas wywoływania tooretrieve magazynu kluczy hello klucz tajny. Uruchom następujące polecenia programu PowerShell hello i zanotuj wartość Identyfikatora hello, która jest klucz tajny hello identyfikatora URI:

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a>Konfigurowanie aplikacji hello
Teraz, po klucz tajny przechowywane można użyć tooretrieve kodu i użyć go. Istnieje kilka czynności, wymagane tooachieve to. Witaj pierwszy i Najważniejszy krok jest rejestrowanie aplikacji w usłudze Azure Active Directory i następnie informuje usługi Key Vault informacje o aplikacji, dzięki czemu można zezwolić żądań od aplikacji.

> [!NOTE]
> Aplikacja musi być utworzone na powitania takie same dzierżawy usługi Azure Active Directory jako magazynu kluczy.
>
>

Otwórz kartę aplikacji hello Azure Active Directory.

![Otwarte aplikacje w usłudze Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

Wybierz **dodać** tooadd tooyour aplikacji usługi Azure Active Directory.

![Wybierz przycisk Dodaj](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

Pozostaw typ aplikacji hello jako **interfejsu API sieci WEB i/lub aplikacji sieci WEB** i nadaj nazwę aplikacji.

![Nazwa hello aplikacji](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

Nadaj aplikacji **adres URL logowania** i **identyfikator URI aplikacji**. Mogą to być dowolnych znaków dla tego pokazu i mogą zostać zmienione później w razie potrzeby.

![Podaj wymagane identyfikatorów URI](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

Po dodaniu aplikacji hello tooAzure usługi Active Directory zostanie wyświetlona na stronie aplikacji hello. Kliknij przycisk hello **Konfiguruj** karcie, a następnie znajdź i skopiuj hello **identyfikator klienta** wartość. Zwróć uwagę na powitania Identyfikatora klienta dla kolejnych krokach.

Następnie wygeneruj klucz dla aplikacji, może współdziałać z usługą Azure Active Directory. Można go utworzyć w obszarze hello **klucze** części hello **konfiguracji** kartę. Zanotuj klucz hello nowo wygenerowane z aplikacji Azure Active Directory do użycia w kolejnym kroku.

![Klucze aplikacji usługi Azure Active Directory](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

Zanim zostanie nawiązana wszystkie wywołania z aplikacji do magazynu kluczy hello, musi Poinformuj hello magazyn kluczy o aplikacji i ich uprawnienia. Witaj poniższe polecenie pobiera nazwę magazynu hello i hello identyfikator klienta aplikacji usługi Azure Active Directory i przyznaje **uzyskać** magazynu kluczy tooyour dostępu dla aplikacji hello.

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

W tym momencie jest gotowy toostart tworzenia połączeń aplikacji. W aplikacji należy zainstalować toointeract wymagane pakiety NuGet hello z usługi Azure Key Vault i Azure Active Directory. Za pomocą konsoli Menedżera pakietów programu Visual Studio hello wprowadź hello następujące polecenia. Na powitania pisania tego artykułu, hello bieżącej wersji pakietu usługi Azure Active Directory hello jest 3.10.305231913, dzięki czemu może mają tooconfirm hello najnowszej wersji i odpowiednio zaktualizować.

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

W kodzie aplikacji Utwórz metodę hello toohold klasy na potrzeby uwierzytelniania usługi Azure Active Directory. W tym przykładzie tej klasy, nosi **witryny**. Dodaj następujące hello instrukcję using:

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Następnie dodaj hello poniższych token JWT hello tooretrieve metody z usługi Azure Active Directory. Łatwość utrzymania można toomove hello ustalony ciągami w konfiguracji sieci web lub aplikacji.

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

Dodaj toocall wymagany kod hello magazyn kluczy i pobrać poufną wartość. Najpierw należy dodać następujące hello instrukcję using:

```csharp
using Microsoft.Azure.KeyVault;
```

Dodaj tooinvoke wywołania metody hello magazyn kluczy i pobrać klucz tajny. W przypadku tej metody musisz podać hasło hello identyfikator URI, który został zapisany w poprzednim kroku. Należy zwrócić uwagę użycie hello hello **GetToken** metody z hello **witryny** klasy utworzone wcześniej.

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

Po uruchomieniu aplikacji, użytkownik powinien teraz autoryzowany tooAzure usługi Active Directory i następnie pobierania poufną wartość z usługi Azure Key Vault.

## <a name="key-rotation-using-azure-automation"></a>Obracanie klucza przy użyciu usługi Automatyzacja Azure
Istnieją różne opcje wdrażania strategii obrotu wartości, które są przechowywane jako klucze tajne usługi Azure Key Vault. Klucze tajne można obracać jako część ręczny proces, ich może zostać obrócona programowo przy użyciu interfejsu API lub może zostać obrócona i skryptów automatyzacji. Dla celów hello w tym artykule, można za pomocą programu Azure PowerShell połączone z toochange usługi Automatyzacja Azure klucza dostępu konta magazynu Azure. Następnie zaktualizuje klucza tajnego klucza magazynu z tego nowego klucza.

tooallow usługi Automatyzacja Azure tooset tajny wartości w magazynie kluczy, należy uzyskać identyfikator klienta hello hello połączenia o nazwie AzureRunAsConnection, który został utworzony podczas ustanawiania wystąpienia usługi Automatyzacja Azure. Ten identyfikator można znaleźć, wybierając **zasoby** z wystąpieniem usługi Automatyzacja Azure. Z tego miejsca, możesz wybrać **połączeń** , a następnie wybierz hello **AzureRunAsConnection** usługi zasady. Zwróć uwagę na powitania **identyfikator aplikacji**.

![Identyfikator klienta usługi Automatyzacja Azure](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

W **zasoby**, wybierz **modułów**. Z **modułów**, wybierz pozycję **galerii**, a następnie wyszukaj i **importu** zaktualizowane wersje każdego hello następujących modułów:

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> Na powitania pisania tego artykułu, hello toobe wcześniej dostrzeżone modułów potrzebne aktualizowana tylko dla następującego skryptu hello. Jeśli okaże się, że zadanie usługi Automatyzacja nie działa prawidłowo, upewnij się, że został zaimportowany wszystkie niezbędne moduły oraz ich zależności.
>
>

Po pobraniu Identyfikatora aplikacji hello połączenia usługi Automatyzacja Azure, należy wskazać magazynu kluczy czy tej aplikacji ma dostęp do kluczy tajnych z tooupdate w magazynie. Można to zrobić z hello następującego polecenia programu PowerShell:

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

Następnie wybierz pozycję **Runbook** w wystąpieniu usługi Automatyzacja Azure, a następnie wybierz **Dodaj element Runbook**. Wybierz pozycję **Szybkie tworzenie**. Nazwa elementu runbook i wybierz **PowerShell** jako hello typ elementu runbook. Masz hello tooadd opcja opis. Na koniec kliknij **Utwórz**.

![Tworzenie elementu runbook](./media/keyvault-keyrotation/Create_Runbook.png)

Wklej hello następującego skryptu programu PowerShell w okienku Edytora hello na nowy element runbook:

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

W okienku Edytora hello wybierz **okienku testu** tootest skryptu. Po hello skrypt jest uruchamiany bez błędów, można wybrać **publikowania**, a następnie można zastosować harmonogram dla elementu runbook hello w okienku konfiguracji elementu runbook hello.

## <a name="key-vault-auditing-pipeline"></a>Potok inspekcji usługi Key Vault
Po skonfigurowaniu magazynu kluczy można włączyć inspekcję toocollect dzienniki na żądania dostępu do magazynu kluczy toohello. Te dzienniki są przechowywane w wyznaczonym konta magazynu Azure i można ściągnąć, monitorowania i analizy. Hello następujący scenariusz używa usługę Azure functions, aplikacje logiki platformy Azure i toocreate dzienniki inspekcji magazynu kluczy toosend potok wiadomości e-mail w przypadku aplikacji, która pasuje do Identyfikatora aplikacji hello hello aplikacji sieci web pobiera kluczy tajnych z magazynu hello.

Najpierw należy włączyć rejestrowanie w magazynie kluczy. Można to zrobić za pomocą następujących poleceń programu PowerShell hello (szczegółowe informacje są widoczne w [klucza magazynu rejestrowania](key-vault-logging.md)):

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

Po włączeniu to rozpoczęcia zbierania do konta magazynu wyznaczonego hello dzienniki inspekcji. Te dzienniki zawiera zdarzenia o jak i kiedy są dostępne z magazynów kluczy i przez kogo.

> [!NOTE]
> Dostępne informacji rejestrowania 10 minut od hello operacji magazynu kluczy. Zwykle jest krótszy.
>
>

Witaj, następnym krokiem jest zbyt[Utwórz kolejkę Azure Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md). Jest to, gdzie są usuwane, dzienniki inspekcji magazynu kluczy. Gdy komunikaty dziennika inspekcji hello znajdują się w kolejce hello, aplikację logiki hello przejmuje je i działa na nich. Tworzenie usługi service bus z hello następujące kroki:

1. Tworzenie przestrzeni nazw usługi Service Bus (Jeśli masz już konto, które mają toouse w tym celu przejdź tooStep 2).
2. Przeglądaj toohello usługi service bus w hello portalu Azure i nazw hello wybierz żądane toocreate hello kolejki w.
3. Wybierz **nowy** i wybierz polecenie **usługi Service Bus > kolejki** i wprowadź szczegóły hello wymagane.
4. Wybierz informacje o połączeniu usługi Service Bus hello Wybieranie hello przestrzeni nazw, a następnie klikając polecenie **informacje o połączeniu**. Informacje te będą potrzebne dla hello następnej sekcji.

Następnie [Tworzenie funkcji platformy Azure](../azure-functions/functions-create-first-azure-function.md) dzienniki magazynu kluczy toopoll poziomu hello konta magazynu i odebrania nowych zdarzeń. Jest to funkcja, która zostanie wywołany zgodnie z harmonogramem.

toocreate funkcji platformy Azure, wybierz **nowy > aplikacji funkcji** w hello portalu Azure. Podczas tworzenia można użyć istniejącego planu obsługi lub Utwórz nową. Można również wybrać do obsługi dynamicznej. Więcej informacji na temat funkcji hosting opcje można znaleźć w folderze [jak tooscale usługi Azure Functions](../azure-functions/functions-scale.md).

Po utworzeniu hello funkcji platformy Azure, przejdź tooit i wybierz czasomierz funkcji i C\#. Następnie kliknij przycisk **tworzenia tej funkcji**.

![Blok funkcji Start Azure](./media/keyvault-keyrotation/Azure_Functions_Start.png)

Na powitania **opracowanie** karcie, Zastąp kod run.csx hello hello poniżej:

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> Utwórz zmienne hello tooreplace się, że w hello poprzedzających konta magazynu tooyour toopoint kodu, w której zapisywane są dzienniki magazynu kluczy hello, hello usługi service bus, który został utworzony wcześniej, a hello dzienniki magazynu magazynu kluczy toohello określonej ścieżki.
>
>

Funkcja Hello przejmuje hello najnowszego pliku dziennika z konta magazynu hello gdzie hello magazynu kluczy dziennikach, chwyty hello najnowsze zdarzenia z tego pliku i umieszcza je tooa kolejki usługi Service Bus. Ponieważ pojedynczy plik może mieć wiele zdarzeń, należy utworzyć plik sync.txt funkcja hello również analizuje toodetermine hello sygnaturę czasową ostatniego zdarzenia hello, która została pobrana. Dzięki temu, że nie push hello tego samego zdarzenia wiele razy. Ten plik sync.txt zawiera sygnaturę czasową dla ostatniego zdarzenia napotkano hello. Hello dzienniki, gdy załadowano, mieć toobe sortowane oparte na powitania sygnatury czasowej tooensure są uporządkowane poprawnie.

Dla tej funkcji możemy odwoływać kilka dodatkowych bibliotek, które nie są dostępne fabrycznej hello w usługi Azure Functions. tooinclude, potrzebujemy toopull usługi Azure Functions je przy użyciu narzędzia NuGet. Wybierz hello **Wyświetl pliki** opcji.

![Wyświetlanie plików](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

I Dodaj plik o nazwie project.json o następującej zawartości:

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
Po **zapisać**, usługi Azure Functions pobierze hello wymagane pliki binarne.

Przełącz toohello **integracji** karcie i nadaj hello czasomierza parametru toouse zrozumiałej nazwy, w obrębie hello funkcji. W hello poprzedzających kodu, oczekuje hello toobe czasomierza o nazwie *myTimer*. Określ [wyrażenie CRON](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) w następujący sposób: 0 \* \* \* \* \* dla czasomierza hello, który spowoduje, że toorun funkcja hello raz na minutę.

Takie same na hello **integracji** , Dodaj danych wejściowych typu hello **magazyn obiektów Blob Azure**. Spowoduje to punktu toohello sync.txt pliku, który zawiera hello sygnatura czasowa ostatniego zdarzenia hello przeglądał przez funkcję hello. Będzie dostępna w ramach funkcji hello według nazwy parametru hello. W hello poprzedzających kodu, wprowadzania magazynu obiektów Blob Azure hello oczekuje toobe nazwę parametru hello *inputBlob*. Wybierz konto magazynu hello której będą znajdować się plik sync.txt hello (może być hello tej samej lub innego konta magazynu). W polu Ścieżka hello Podaj ścieżkę hello, w którym znajduje się plik hello w formacie hello {container-name}/path/to/sync.txt.

Dodaj dane wyjściowe typu hello *magazyn obiektów Blob Azure* danych wyjściowych. Spowoduje to punktu toohello sync.txt pliku, który zdefiniowano w danych wejściowych hello. To jest używany przez hello funkcja toowrite hello sygnatura czasowa ostatniego zdarzenia hello przeglądał. Witaj poprzedni kod oczekuje tego toobe parametr o nazwie *Blob_wyj*.

W tym momencie funkcja hello jest gotowy. Upewnij się tooswitch toohello Wstecz **opracowanie** karcie i Zapisz hello kodu. Sprawdź okno danych wyjściowych hello występują błędy kompilacji i odpowiednio je poprawić. Jeśli kompiluje kod hello, hello kodu powinny teraz być sprawdzenie dzienniki magazynu kluczy hello co minutę i wypychanie żadnych nowych zdarzeń na powitania zdefiniowano kolejki usługi Service Bus. Informacje o rejestrowaniu zapisać okno Dziennik toohello każdym wyzwoleniu hello funkcja powinna zostać wyświetlona.

### <a name="azure-logic-app"></a>Aplikacja logiki platformy Azure
Następnie należy utworzyć aplikację logiki platformy Azure, która przejmuje hello zdarzeń czy funkcja hello wypycha toohello kolejki usługi Service Bus, analizuje hello zawartości i wysyła wiadomość e-mail na podstawie warunku filtrowanego.

[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md) przechodząc zbyt**nowy > aplikacji logiki**.

Po utworzeniu aplikacji logiki hello Przejdź tooit i wybierz polecenie **Edytuj**. Edytora hello logikę aplikacji, wybierz **kolejką usługi Service Bus** , a następnie wprowadź tooconnect poświadczeń użytkownika usługi Service Bus go toohello kolejki.

![Magistrala usług aplikacji logiki platformy Azure](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

Następnie wybierz **Dodaj warunek**. W warunku hello Przełącz toohello Zaawansowany edytor i wprowadź powitania po kod, zastępując APP_ID hello rzeczywiste APP_ID aplikacji sieci web:

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

To wyrażenie zasadniczo zwraca **false** Jeśli hello *appid* z hello zdarzenia przychodzącego (czyli hello treści wiadomości powitania usługi Service Bus) nie jest hello *appid* z hello aplikacja.

Teraz utworzymy działania na podstawie **Jeśli nie, nic nie rób**.

![Azure aplikacji logiki, wybierz akcję](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

Dla akcji hello wybierz **usługi Office 365 — wysyłanie wiadomości e-mail**. Wypełnianie toocreate pola hello toosend wiadomości e-mail podczas hello zdefiniowany warunek zwraca **false**. Jeśli nie masz usługi Office 365, może wyglądać na alternatyw tooachieve hello takie same wyniki.

W tym momencie masz potok tooend zakończenia, który wyszukuje nowe dzienniki inspekcji magazynu kluczy raz na minutę. Umieszcza on nowe dzienniki znajdzie tooa kolejką usługi service bus. Aplikacja logiki Hello jest wyzwalane, gdy nowy komunikat znajdzie się w kolejce hello. Jeśli hello *appid* w hello zdarzeń nie jest zgodna identyfikator aplikacji hello wywoływania aplikacji hello, wysyła wiadomość e-mail.
