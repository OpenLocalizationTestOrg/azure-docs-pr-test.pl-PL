---
title: "Jak używać magazynu obiektów Blob z Xamarin | Dokumentacja firmy Microsoft"
description: "Biblioteka klienta magazynu Azure dla platformy Xamarin umożliwia deweloperom tworzenie systemu iOS, Android i aplikacji ze Sklepu Windows z ich interfejsy macierzystego użytkownika. W tym samouczku pokazano, jak program Xamarin, aby utworzyć aplikację, która korzysta z magazynu obiektów Blob platformy Azure."
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
ms.openlocfilehash: 5ff4d86082c03dcd7098743a984a97aa70232d1d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-xamarin"></a><span data-ttu-id="de33e-104">Jak używać magazynu obiektów Blob z Xamarin</span><span class="sxs-lookup"><span data-stu-id="de33e-104">How to use Blob Storage from Xamarin</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a><span data-ttu-id="de33e-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="de33e-105">Overview</span></span>
<span data-ttu-id="de33e-106">Aby utworzyć systemu iOS, Android i aplikacji ze Sklepu Windows za pomocą ich interfejsów użytkownika natywnego bazy kodu Xamarin umożliwiają deweloperom Użyj udostępnionych C#.</span><span class="sxs-lookup"><span data-stu-id="de33e-106">Xamarin enables developers to use a shared C# codebase to create iOS, Android, and Windows Store apps with their native user interfaces.</span></span> <span data-ttu-id="de33e-107">Ten samouczek pokazuje, jak używać magazynu obiektów Blob platformy Azure przy użyciu aplikacji Xamarin.</span><span class="sxs-lookup"><span data-stu-id="de33e-107">This tutorial shows you how to use Azure Blob storage with a Xamarin application.</span></span> <span data-ttu-id="de33e-108">Jeśli chcesz dowiedzieć się więcej na temat usługi Azure Storage, przed rozpoczęciem pracy z kodem, zobacz [wprowadzenie do usługi Microsoft Azure Storage](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="de33e-108">If you'd like to learn more about Azure Storage, before diving into the code, see [Introduction to Microsoft Azure Storage](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a><span data-ttu-id="de33e-109">Tworzenie nowej aplikacji platformy Xamarin</span><span class="sxs-lookup"><span data-stu-id="de33e-109">Create a new Xamarin Application</span></span>
<span data-ttu-id="de33e-110">W tym samouczku możemy utworzyć aplikację, która jest przeznaczony dla systemu Android, iOS i Windows.</span><span class="sxs-lookup"><span data-stu-id="de33e-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span></span> <span data-ttu-id="de33e-111">Ta aplikacja będzie po prostu utworzyć kontener i przekazać obiekt blob do tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="de33e-111">This app will simply create a container and upload a blob into this container.</span></span> <span data-ttu-id="de33e-112">Będziemy używać programu Visual Studio w systemie Windows, ale sam learnings można zastosować podczas tworzenia aplikacji za pomocą platformy Xamarin Studio na macOS.</span><span class="sxs-lookup"><span data-stu-id="de33e-112">We'll be using Visual Studio on Windows, but the same learnings can be applied when creating an app using Xamarin Studio on macOS.</span></span>

<span data-ttu-id="de33e-113">Wykonaj następujące kroki, aby utworzyć aplikację:</span><span class="sxs-lookup"><span data-stu-id="de33e-113">Follow these steps to create your application:</span></span>

1. <span data-ttu-id="de33e-114">Jeśli nie jest jeszcze, Pobierz i zainstaluj [Xamarin dla Visual Studio](https://www.xamarin.com/download).</span><span class="sxs-lookup"><span data-stu-id="de33e-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span></span>
2. <span data-ttu-id="de33e-115">Otwórz program Visual Studio, a utworzona pusta aplikacja (Native przenośne): **Plik > Nowy > Projekt > i Platform > App(Native Portable) puste**.</span><span class="sxs-lookup"><span data-stu-id="de33e-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span></span>
3. <span data-ttu-id="de33e-116">Kliknij prawym przyciskiem myszy rozwiązanie, w okienku Eksplorator rozwiązań i wybierz **Zarządzaj pakietami NuGet dla rozwiązania**.</span><span class="sxs-lookup"><span data-stu-id="de33e-116">Right-click your solution in the Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="de33e-117">Wyszukaj **WindowsAzure.Storage** i zainstaluj najnowszą wersję stabilna do wszystkich projektów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="de33e-117">Search for **WindowsAzure.Storage** and install the latest stable version to all projects in your solution.</span></span>
4. <span data-ttu-id="de33e-118">Tworzenie i uruchamianie projektu.</span><span class="sxs-lookup"><span data-stu-id="de33e-118">Build and run your project.</span></span>

<span data-ttu-id="de33e-119">Teraz powinien mieć aplikację, która umożliwia kliknięcie przycisku, który zwiększa licznik.</span><span class="sxs-lookup"><span data-stu-id="de33e-119">You should now have an application that allows you to click a button which increments a counter.</span></span>

## <a name="create-container-and-upload-blob"></a><span data-ttu-id="de33e-120">Tworzenie kontenera i przekazania obiektu blob</span><span class="sxs-lookup"><span data-stu-id="de33e-120">Create container and upload blob</span></span>
<span data-ttu-id="de33e-121">Następnie w obszarze Twojej `(Portable)` projektu, dodasz kod służący do `MyClass.cs`.</span><span class="sxs-lookup"><span data-stu-id="de33e-121">Next, under your `(Portable)` project, you'll add some code to `MyClass.cs`.</span></span> <span data-ttu-id="de33e-122">Ten kod tworzy kontener i wysyła do tego kontenera obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="de33e-122">This code creates a container and uploads a blob into this container.</span></span> <span data-ttu-id="de33e-123">`MyClass.cs`powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="de33e-123">`MyClass.cs` should look like the following:</span></span>

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

            // Create the blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference to a previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create the container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference to a blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create the "myblob" blob with the text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

<span data-ttu-id="de33e-124">Upewnij się zastąpić "your_account_name_here" i "your_account_key_here" Nazwa rzeczywista konta i klucz konta.</span><span class="sxs-lookup"><span data-stu-id="de33e-124">Make sure to replace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span></span> 

<span data-ttu-id="de33e-125">Z systemu iOS, Android i Windows Phone, wszystkie projekty odwołują się do projektu przenośnych — co oznacza, że pisania kodu udostępnionych w jednej Umieść i używać go we wszystkich projektach.</span><span class="sxs-lookup"><span data-stu-id="de33e-125">Your iOS, Android, and Windows Phone projects all have references to your Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span></span> <span data-ttu-id="de33e-126">Następujący wiersz kodu można teraz dodać do każdego projektu, aby uruchomić wykorzystaniu:`MyClass.performBlobOperation()`</span><span class="sxs-lookup"><span data-stu-id="de33e-126">You can now add the following line of code to each project to start taking advantage: `MyClass.performBlobOperation()`</span></span>

### <a name="xamarinappdroid--mainactivitycs"></a><span data-ttu-id="de33e-127">XamarinApp.Droid > MainActivity.cs</span><span class="sxs-lookup"><span data-stu-id="de33e-127">XamarinApp.Droid > MainActivity.cs</span></span>

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

            // Set our view from the "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from the layout resource,
            // and attach an event to it
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

### <a name="xamarinappios--viewcontrollercs"></a><span data-ttu-id="de33e-128">XamarinApp.iOS > ViewController.cs</span><span class="sxs-lookup"><span data-stu-id="de33e-128">XamarinApp.iOS > ViewController.cs</span></span>

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
                // Perform any additional setup after loading the view, typically from a nib.
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

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a><span data-ttu-id="de33e-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="de33e-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span></span>

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated to within a Frame.
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
        /// Invoked when this page is about to be displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used to configure the page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about to be displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used to configure the page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling the hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using the NavigationHelper provided by some templates,
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

## <a name="run-the-application"></a><span data-ttu-id="de33e-130">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="de33e-130">Run the application</span></span>
<span data-ttu-id="de33e-131">Można teraz uruchomić tę aplikację w emulatorze systemu Android i Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="de33e-131">You can now run this application in an Android or Windows Phone emulator.</span></span> <span data-ttu-id="de33e-132">Można również uruchomić tę aplikację w emulatorze systemu iOS, ale wymaga to Mac.</span><span class="sxs-lookup"><span data-stu-id="de33e-132">You can also run this application in an iOS emulator, but this will require a Mac.</span></span> <span data-ttu-id="de33e-133">Aby uzyskać szczegółowe instrukcje na temat to zrobić, przeczytaj dokumentację [łączenie programu Visual Studio na komputerze Mac.](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span><span class="sxs-lookup"><span data-stu-id="de33e-133">For specific instructions on how to do this, please read the documentation for [connecting Visual Studio to a Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span></span>

<span data-ttu-id="de33e-134">Po uruchomieniu aplikacji będzie utworzyć kontener `mycontainer` na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="de33e-134">Once you run your app, it will create the container `mycontainer` in your Storage account.</span></span> <span data-ttu-id="de33e-135">Powinien on zawierać obiektów blob, `myblob`, który ma tekstu, `Hello, world!`.</span><span class="sxs-lookup"><span data-stu-id="de33e-135">It should contain the blob, `myblob`, which has the text, `Hello, world!`.</span></span> <span data-ttu-id="de33e-136">Można to sprawdzić za pomocą [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="de33e-136">You can verify this by using the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="de33e-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="de33e-137">Next steps</span></span>
<span data-ttu-id="de33e-138">W tym samouczku przedstawiono sposób tworzenia aplikacji i platform w Xamarin, która używa usługi Azure Storage, w szczególności koncentrujących się na jednym ze scenariuszy w magazynie obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="de33e-138">In this tutorial, you learned how to create a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span></span> <span data-ttu-id="de33e-139">Jednak możesz to zrobić dużo więcej nie tylko magazynu obiektów Blob, lecz również z tabeli, plików i magazynowania kolejki.</span><span class="sxs-lookup"><span data-stu-id="de33e-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span></span> <span data-ttu-id="de33e-140">Sprawdź następujące artykuły, aby dowiedzieć się więcej:</span><span class="sxs-lookup"><span data-stu-id="de33e-140">Please check out the following articles to learn more:</span></span>

* [<span data-ttu-id="de33e-141">Rozpoczynanie pracy z usługą Azure Blob Storage przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="de33e-141">Get started with Azure Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="de33e-142">Rozpoczynanie pracy z usługą Azure Table Storage przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="de33e-142">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="de33e-143">Rozpoczynanie pracy z usługą Azure Queue Storage przy użyciu platformy .NET</span><span class="sxs-lookup"><span data-stu-id="de33e-143">Get started with Azure Queue storage using .NET</span></span>](../queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="de33e-144">Rozpoczynanie pracy z usługą Azure File Storage w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="de33e-144">Get started with Azure File storage on Windows</span></span>](../files/storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

