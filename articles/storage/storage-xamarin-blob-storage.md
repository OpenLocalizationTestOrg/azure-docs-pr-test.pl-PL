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
ms.openlocfilehash: 751f66d1d2392c8bcf6e5f8d1b185af73582fab3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-xamarin"></a><span data-ttu-id="fde9f-104">Jak toouse magazynu obiektów Blob z Xamarin</span><span class="sxs-lookup"><span data-stu-id="fde9f-104">How toouse Blob Storage from Xamarin</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a><span data-ttu-id="fde9f-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="fde9f-105">Overview</span></span>
<span data-ttu-id="fde9f-106">Xamarin umożliwia deweloperom toouse udostępnionego C# codebase toocreate z systemem iOS, Android i z ich interfejsami użytkownika natywnych aplikacji ze Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="fde9f-106">Xamarin enables developers toouse a shared C# codebase toocreate iOS, Android, and Windows Store apps with their native user interfaces.</span></span> <span data-ttu-id="fde9f-107">W tym samouczku przedstawiono sposób toouse magazynu obiektów Blob platformy Azure przy użyciu aplikacji Xamarin.</span><span class="sxs-lookup"><span data-stu-id="fde9f-107">This tutorial shows you how toouse Azure Blob storage with a Xamarin application.</span></span> <span data-ttu-id="fde9f-108">Jeśli chcesz toolearn więcej informacji na temat usługi Azure Storage przed rozpoczęciem pracy hello kod, zobacz [tooMicrosoft wprowadzenie usługi Azure Storage](storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fde9f-108">If you'd like toolearn more about Azure Storage, before diving into hello code, see [Introduction tooMicrosoft Azure Storage](storage-introduction.md).</span></span>

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a><span data-ttu-id="fde9f-109">Tworzenie nowej aplikacji platformy Xamarin</span><span class="sxs-lookup"><span data-stu-id="fde9f-109">Create a new Xamarin Application</span></span>
<span data-ttu-id="fde9f-110">W tym samouczku możemy utworzyć aplikację, która jest przeznaczony dla systemu Android, iOS i Windows.</span><span class="sxs-lookup"><span data-stu-id="fde9f-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span></span> <span data-ttu-id="fde9f-111">Ta aplikacja będzie po prostu utworzyć kontener i przekazać obiekt blob do tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="fde9f-111">This app will simply create a container and upload a blob into this container.</span></span> <span data-ttu-id="fde9f-112">Będziemy używać programu Visual Studio z systemu Windows, ale powitalne tego samego learnings można zastosować podczas tworzenia aplikacji za pomocą platformy Xamarin Studio na macOS.</span><span class="sxs-lookup"><span data-stu-id="fde9f-112">We'll be using Visual Studio on Windows, but hello same learnings can be applied when creating an app using Xamarin Studio on macOS.</span></span>

<span data-ttu-id="fde9f-113">Wykonaj te kroki toocreate aplikacji:</span><span class="sxs-lookup"><span data-stu-id="fde9f-113">Follow these steps toocreate your application:</span></span>

1. <span data-ttu-id="fde9f-114">Jeśli nie jest jeszcze, Pobierz i zainstaluj [Xamarin dla Visual Studio](https://www.xamarin.com/download).</span><span class="sxs-lookup"><span data-stu-id="fde9f-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span></span>
2. <span data-ttu-id="fde9f-115">Otwórz program Visual Studio, a utworzona pusta aplikacja (Native przenośne): **Plik > Nowy > Projekt > i Platform > App(Native Portable) puste**.</span><span class="sxs-lookup"><span data-stu-id="fde9f-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span></span>
3. <span data-ttu-id="fde9f-116">Kliknij prawym przyciskiem myszy w okienku Eksplorator rozwiązań hello rozwiązania i wybierz **Zarządzaj pakietami NuGet dla rozwiązania**.</span><span class="sxs-lookup"><span data-stu-id="fde9f-116">Right-click your solution in hello Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="fde9f-117">Wyszukaj **WindowsAzure.Storage** i zainstaluj hello najnowszej wersji stabilnej tooall projektów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="fde9f-117">Search for **WindowsAzure.Storage** and install hello latest stable version tooall projects in your solution.</span></span>
4. <span data-ttu-id="fde9f-118">Tworzenie i uruchamianie projektu.</span><span class="sxs-lookup"><span data-stu-id="fde9f-118">Build and run your project.</span></span>

<span data-ttu-id="fde9f-119">Teraz powinien mieć aplikację, która pozwala tooclick przycisku, który zwiększa licznik.</span><span class="sxs-lookup"><span data-stu-id="fde9f-119">You should now have an application that allows you tooclick a button which increments a counter.</span></span>

## <a name="create-container-and-upload-blob"></a><span data-ttu-id="fde9f-120">Tworzenie kontenera i przekazania obiektu blob</span><span class="sxs-lookup"><span data-stu-id="fde9f-120">Create container and upload blob</span></span>
<span data-ttu-id="fde9f-121">Następnie w obszarze Twojej `(Portable)` projektu, dodasz kod zbyt`MyClass.cs`.</span><span class="sxs-lookup"><span data-stu-id="fde9f-121">Next, under your `(Portable)` project, you'll add some code too`MyClass.cs`.</span></span> <span data-ttu-id="fde9f-122">Ten kod tworzy kontener i wysyła do tego kontenera obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="fde9f-122">This code creates a container and uploads a blob into this container.</span></span> <span data-ttu-id="fde9f-123">`MyClass.cs`powinna wyglądać hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="fde9f-123">`MyClass.cs` should look like hello following:</span></span>

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

<span data-ttu-id="fde9f-124">Upewnij się, że tooreplace "your_account_name_here" i "your_account_key_here" z nazwy własnego konta i klucz konta.</span><span class="sxs-lookup"><span data-stu-id="fde9f-124">Make sure tooreplace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span></span> 

<span data-ttu-id="fde9f-125">Z systemu iOS, Android i Windows Phone projekty wszystkie mają odwołań tooyour Przenoścnego projektu — co oznacza, że pisania kodu udostępnionych w jednym Umieść i używać go we wszystkich projektach.</span><span class="sxs-lookup"><span data-stu-id="fde9f-125">Your iOS, Android, and Windows Phone projects all have references tooyour Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span></span> <span data-ttu-id="fde9f-126">Można teraz dodawać powitania po wierszu kodu tooeach projektu toostart skorzystaj:`MyClass.performBlobOperation()`</span><span class="sxs-lookup"><span data-stu-id="fde9f-126">You can now add hello following line of code tooeach project toostart taking advantage: `MyClass.performBlobOperation()`</span></span>

### <a name="xamarinappdroid--mainactivitycs"></a><span data-ttu-id="fde9f-127">XamarinApp.Droid > MainActivity.cs</span><span class="sxs-lookup"><span data-stu-id="fde9f-127">XamarinApp.Droid > MainActivity.cs</span></span>

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

### <a name="xamarinappios--viewcontrollercs"></a><span data-ttu-id="fde9f-128">XamarinApp.iOS > ViewController.cs</span><span class="sxs-lookup"><span data-stu-id="fde9f-128">XamarinApp.iOS > ViewController.cs</span></span>

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

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a><span data-ttu-id="fde9f-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="fde9f-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span></span>

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

## <a name="run-hello-application"></a><span data-ttu-id="fde9f-130">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="fde9f-130">Run hello application</span></span>
<span data-ttu-id="fde9f-131">Można teraz uruchomić tę aplikację w emulatorze systemu Android i Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="fde9f-131">You can now run this application in an Android or Windows Phone emulator.</span></span> <span data-ttu-id="fde9f-132">Można również uruchomić tę aplikację w emulatorze systemu iOS, ale wymaga to Mac.</span><span class="sxs-lookup"><span data-stu-id="fde9f-132">You can also run this application in an iOS emulator, but this will require a Mac.</span></span> <span data-ttu-id="fde9f-133">Aby uzyskać szczegółowe instrukcje na jak toodo, przeczytaj dokumentację hello [łączenie programu Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span><span class="sxs-lookup"><span data-stu-id="fde9f-133">For specific instructions on how toodo this, please read hello documentation for [connecting Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span></span>

<span data-ttu-id="fde9f-134">Po uruchomieniu aplikacji spowoduje utworzenie kontenera hello `mycontainer` na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="fde9f-134">Once you run your app, it will create hello container `mycontainer` in your Storage account.</span></span> <span data-ttu-id="fde9f-135">Powinien on zawierać hello blob `myblob`, mającego tekst hello `Hello, world!`.</span><span class="sxs-lookup"><span data-stu-id="fde9f-135">It should contain hello blob, `myblob`, which has hello text, `Hello, world!`.</span></span> <span data-ttu-id="fde9f-136">Można to sprawdzić za pomocą hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="fde9f-136">You can verify this by using hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fde9f-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fde9f-137">Next steps</span></span>
<span data-ttu-id="fde9f-138">W tym samouczku przedstawiono sposób toocreate aplikację i platform w programie Xamarin używającą usługi Azure Storage, w szczególności koncentrujących się na jednym ze scenariuszy w magazynie obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="fde9f-138">In this tutorial, you learned how toocreate a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span></span> <span data-ttu-id="fde9f-139">Jednak możesz to zrobić dużo więcej nie tylko magazynu obiektów Blob, lecz również z tabeli, plików i magazynowania kolejki.</span><span class="sxs-lookup"><span data-stu-id="fde9f-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span></span> <span data-ttu-id="fde9f-140">Sprawdź następujące artykuły toolearn więcej hello:</span><span class="sxs-lookup"><span data-stu-id="fde9f-140">Please check out hello following articles toolearn more:</span></span>

* [<span data-ttu-id="fde9f-141">Rozpoczynanie pracy z usługą Azure Blob Storage przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="fde9f-141">Get started with Azure Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="fde9f-142">Rozpoczynanie pracy z usługą Azure Table Storage przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="fde9f-142">Get started with Azure Table storage using .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="fde9f-143">Rozpoczynanie pracy z usługą Azure Queue Storage przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="fde9f-143">Get started with Azure Queue storage using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="fde9f-144">Rozpoczynanie pracy z usługą Azure File Storage w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="fde9f-144">Get started with Azure File storage on Windows</span></span>](storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

