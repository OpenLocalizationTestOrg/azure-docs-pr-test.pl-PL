---
title: "toouse aaaHow magazynu obiektów Blob z Xamarin | Dokumentacja firmy Microsoft"
description: "Witaj biblioteki klienta magazynu Azure dla platformy Xamarin umożliwia deweloperom toocreate z systemem iOS, Android i z ich interfejsami użytkownika natywnych aplikacji ze Sklepu Windows. Ten samouczek pokazuje, jak toouse Xamarin toocreate aplikacji, która korzysta z magazynu obiektów Blob platformy Azure."
services: storage
documentationcenter: xamarin
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 44cb845d-cf78-4942-95b8-952da4f9a2c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 688484fc560b5c89ed1692f5cbf5713aa8fc90a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-xamarin"></a>Jak toouse magazynu obiektów Blob z Xamarin
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a>Omówienie
Xamarin umożliwia deweloperom toouse udostępnionego C# codebase toocreate z systemem iOS, Android i z ich interfejsami użytkownika natywnych aplikacji ze Sklepu Windows. W tym samouczku przedstawiono sposób toouse magazynu obiektów Blob platformy Azure przy użyciu aplikacji Xamarin. Jeśli chcesz toolearn więcej informacji na temat usługi Azure Storage przed rozpoczęciem pracy hello kod, zobacz [tooMicrosoft wprowadzenie usługi Azure Storage](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a>Tworzenie nowej aplikacji platformy Xamarin
W tym samouczku możemy utworzyć aplikację, która jest przeznaczony dla systemu Android, iOS i Windows. Ta aplikacja będzie po prostu utworzyć kontener i przekazać obiekt blob do tego kontenera. Będziemy używać programu Visual Studio z systemu Windows, ale powitalne tego samego learnings można zastosować podczas tworzenia aplikacji za pomocą platformy Xamarin Studio na macOS.

Wykonaj te kroki toocreate aplikacji:

1. Jeśli nie jest jeszcze, Pobierz i zainstaluj [Xamarin dla Visual Studio](https://www.xamarin.com/download).
2. Otwórz program Visual Studio, a utworzona pusta aplikacja (Native przenośne): **Plik > Nowy > Projekt > i Platform > App(Native Portable) puste**.
3. Kliknij prawym przyciskiem myszy w okienku Eksplorator rozwiązań hello rozwiązania i wybierz **Zarządzaj pakietami NuGet dla rozwiązania**. Wyszukaj **WindowsAzure.Storage** i zainstaluj hello najnowszej wersji stabilnej tooall projektów w rozwiązaniu.
4. Tworzenie i uruchamianie projektu.

Teraz powinien mieć aplikację, która pozwala tooclick przycisku, który zwiększa licznik.

## <a name="create-container-and-upload-blob"></a>Tworzenie kontenera i przekazania obiektu blob
Następnie w obszarze Twojej `(Portable)` projektu, dodasz kod zbyt`MyClass.cs`. Ten kod tworzy kontener i wysyła do tego kontenera obiektu blob. `MyClass.cs`powinna wyglądać hello następujące czynności:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Threading.Tasks;

namespace XamarinApp
{
    public class MyClass
    {
        public MyClass ()
        {
        }

        public static async Task performBlobOperation()
        {
            // Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here");

            // Create hello blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference tooa previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create hello container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference tooa blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create hello "myblob" blob with hello text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

Upewnij się, że tooreplace "your_account_name_here" i "your_account_key_here" z nazwy własnego konta i klucz konta. 

Z systemu iOS, Android i Windows Phone projekty wszystkie mają odwołań tooyour Przenoścnego projektu — co oznacza, że pisania kodu udostępnionych w jednym Umieść i używać go we wszystkich projektach. Można teraz dodawać powitania po wierszu kodu tooeach projektu toostart skorzystaj:`MyClass.performBlobOperation()`

### <a name="xamarinappdroid--mainactivitycs"></a>XamarinApp.Droid > MainActivity.cs

```csharp
using Android.App;
using Android.Widget;
using Android.OS;

namespace XamarinApp.Droid
{
    [Activity (Label = "XamarinApp.Droid", MainLauncher = true, Icon = "@drawable/icon")]
    public class MainActivity : Activity
    {
        int count = 1;

        protected override async void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);

            button.Click += delegate {
                button.Text = string.Format ("{0} clicks!", count++);
            };

            await MyClass.performBlobOperation();
            }
        }
    }
}
```

### <a name="xamarinappios--viewcontrollercs"></a>XamarinApp.iOS > ViewController.cs

```csharp
using System;
using UIKit;

namespace XamarinApp.iOS
{
    public partial class ViewController : UIViewController
    {
        int count = 1;

        public ViewController (IntPtr handle) : base (handle)
        {
        }

        public override async void ViewDidLoad ()
        {
            int count = 1;

            public ViewController (IntPtr handle) : base (handle)
            {
            }

            public override async void ViewDidLoad ()
            {
                base.ViewDidLoad ();
                // Perform any additional setup after loading hello view, typically from a nib.
                Button.AccessibilityIdentifier = "myButton";
                Button.TouchUpInside += delegate {
                    var title = string.Format ("{0} clicks!", count++);
                    Button.SetTitle (title, UIControlState.Normal);
                };

                await MyClass.performBlobOperation();
            }

            public override void DidReceiveMemoryWarning ()
            {
                base.DidReceiveMemoryWarning ();
                // Release any cached data, images, etc that aren't in use.
            }
        }
    }
}
```

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a>XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// hello Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated toowithin a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        int count = 1;

        public MainPage()
        {
            this.InitializeComponent();

            this.NavigationCacheMode = NavigationCacheMode.Required;
        }

        /// <summary>
        /// Invoked when this page is about toobe displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used tooconfigure hello page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about toobe displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used tooconfigure hello page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling hello hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using hello NavigationHelper provided by some templates,
                // this event is handled for you.
                Button.Click += delegate {
                    var title = string.Format("{0} clicks!", count++);
                    Button.Content = title;
                };

                await MyClass.performBlobOperation();
            }
        }
    }
}
```

## <a name="run-hello-application"></a>Uruchamianie aplikacji hello
Można teraz uruchomić tę aplikację w emulatorze systemu Android i Windows Phone. Można również uruchomić tę aplikację w emulatorze systemu iOS, ale wymaga to Mac. Aby uzyskać szczegółowe instrukcje na jak toodo, przeczytaj dokumentację hello [łączenie programu Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)

Po uruchomieniu aplikacji spowoduje utworzenie kontenera hello `mycontainer` na koncie magazynu. Powinien on zawierać hello blob `myblob`, mającego tekst hello `Hello, world!`. Można to sprawdzić za pomocą hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/).

## <a name="next-steps"></a>Następne kroki
W tym samouczku przedstawiono sposób toocreate aplikację i platform w programie Xamarin używającą usługi Azure Storage, w szczególności koncentrujących się na jednym ze scenariuszy w magazynie obiektów Blob. Jednak możesz to zrobić dużo więcej nie tylko magazynu obiektów Blob, lecz również z tabeli, plików i magazynowania kolejki. Sprawdź następujące artykuły toolearn więcej hello:

* [Rozpoczynanie pracy z usługą Azure Blob Storage przy użyciu platformy .NET](storage-dotnet-how-to-use-blobs.md)
* [Rozpoczynanie pracy z usługą Azure Table Storage przy użyciu platformy .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Rozpoczynanie pracy z usługą Azure Queue Storage przy użyciu platformy .NET](../queues/storage-dotnet-how-to-use-queues.md)
* [Rozpoczynanie pracy z usługą Azure File Storage w systemie Windows](../files/storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

