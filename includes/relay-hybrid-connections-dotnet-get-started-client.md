### <a name="create-a-console-application"></a><span data-ttu-id="5854b-101">Tworzenie aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="5854b-101">Create a console application</span></span>

<span data-ttu-id="5854b-102">Najpierw uruchom program Visual Studio i utwórz nowy projekt **Aplikacja konsoli (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="5854b-102">First, launch Visual Studio and create a new **Console App (.NET Framework)** project.</span></span>

### <a name="add-hello-relay-nuget-package"></a><span data-ttu-id="5854b-103">Dodaj pakiet NuGet przekazywania hello</span><span class="sxs-lookup"><span data-stu-id="5854b-103">Add hello Relay NuGet package</span></span>

1. <span data-ttu-id="5854b-104">Kliknij prawym przyciskiem myszy projekt hello nowo utworzony, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5854b-104">Right-click hello newly created project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="5854b-105">Kliknij przycisk hello **Przeglądaj** kartę, a następnie wyszukaj "Microsoft.Azure.Relay" i wybierz hello **Microsoft Azure przekazywania** elementu.</span><span class="sxs-lookup"><span data-stu-id="5854b-105">Click hello **Browse** tab, then search for "Microsoft.Azure.Relay" and select hello **Microsoft Azure Relay** item.</span></span> <span data-ttu-id="5854b-106">Kliknij przycisk **zainstalować** toocomplete hello instalacji, a następnie zamknij to okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="5854b-106">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

### <a name="write-some-code-toosend-messages"></a><span data-ttu-id="5854b-107">Napisanie kodu toosend wiadomości</span><span class="sxs-lookup"><span data-stu-id="5854b-107">Write some code toosend messages</span></span>

1. <span data-ttu-id="5854b-108">Zamień istniejące hello `using` instrukcji u góry pliku Program.cs hello następujący hello hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="5854b-108">Replace hello existing `using` statements at hello top of hello Program.cs file with hello following `using` statements:</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
    ```
2. <span data-ttu-id="5854b-109">Dodaj toohello stałe `Program` klasy dla szczegóły połączenia hybrydowe hello.</span><span class="sxs-lookup"><span data-stu-id="5854b-109">Add constants toohello `Program` class for hello hybrid connection details.</span></span> <span data-ttu-id="5854b-110">Zastąp symbole zastępcze hello w nawiasach wartości hello uzyskane podczas tworzenia połączenia hybrydowego hello.</span><span class="sxs-lookup"><span data-stu-id="5854b-110">Replace hello placeholders in brackets with hello values you obtained when creating hello hybrid connection.</span></span> <span data-ttu-id="5854b-111">Należy się toouse hello przestrzeni nazw w pełni kwalifikowaną nazwę:</span><span class="sxs-lookup"><span data-stu-id="5854b-111">Be sure toouse hello fully qualified namespace name:</span></span>
   
    ```csharp
    private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
    private const string ConnectionName = "{HybridConnectionName}";
    private const string KeyName = "{SASKeyName}";
    private const string Key = "{SASKey}";
    ```
3. <span data-ttu-id="5854b-112">Dodaj następujące metody toohello hello `Program` klasy:</span><span class="sxs-lookup"><span data-stu-id="5854b-112">Add hello following method toohello `Program` class:</span></span>
   
    ```csharp
    private static async Task RunAsync()
    {
        Console.WriteLine("Enter lines of text toosend toohello server with ENTER");
   
        // Create a new hybrid connection client
        var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
        var client = new HybridConnectionClient(new Uri(String.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
        // Initiate hello connection
        var relayConnection = await client.CreateConnectionAsync();
   
        // We run two concurrent loops on hello connection. One 
        // reads input from hello console and writes it toohello connection 
        // with a stream writer. hello other reads lines of input from hello 
        // connection with a stream reader and writes them toohello console. 
        // Entering a blank line will shut down hello write task after 
        // sending it toohello server. hello server will then cleanly shut down
        // hello connection which will terminate hello read task.
   
        var reads = Task.Run(async () => {
            // Initialize hello stream reader over hello connection
            var reader = new StreamReader(relayConnection);
            var writer = Console.Out;
            do
            {
                // Read a full line of UTF-8 text up toonewline
                string line = await reader.ReadLineAsync();
                // if hello string is empty or null, we are done.
                if (String.IsNullOrEmpty(line))
                    break;
                // Write toohello console
                await writer.WriteLineAsync(line);
            }
            while (true);
        });
   
        // Read from hello console and write toohello hybrid connection
        var writes = Task.Run(async () => {
            var reader = Console.In;
            var writer = new StreamWriter(relayConnection) { AutoFlush = true };
            do
            {
                // Read a line form hello console
                string line = await reader.ReadLineAsync();
                // Write hello line out, also when it's empty
                await writer.WriteLineAsync(line);
                // Quit when hello line was empty
                if (String.IsNullOrEmpty(line))
                    break;
            }
            while (true);
        });
   
        // Wait for both tasks toocomplete
        await Task.WhenAll(reads, writes);
        await relayConnection.CloseAsync(CancellationToken.None);
    }
    ```
4. <span data-ttu-id="5854b-113">Dodaj powitania po wierszu kodu toohello `Main` w hello metody `Program` klasy.</span><span class="sxs-lookup"><span data-stu-id="5854b-113">Add hello following line of code toohello `Main` method in hello `Program` class.</span></span>
   
    ```csharp
    RunAsync().GetAwaiter().GetResult();
    ```
   
    <span data-ttu-id="5854b-114">Oto jak powinien wyglądać plik Program.cs.</span><span class="sxs-lookup"><span data-stu-id="5854b-114">Here is what your Program.cs should look like.</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
   
    namespace Client
    {
        class Program
        {
            private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
            private const string ConnectionName = "{HybridConnectionName}";
            private const string KeyName = "{SASKeyName}";
            private const string Key = "{SASKey}";
   
            static void Main(string[] args)
            {
                RunAsync().GetAwaiter().GetResult();
            }
   
            private static async Task RunAsync()
            {
                Console.WriteLine("Enter lines of text toosend toohello server with ENTER");
   
                // Create a new hybrid connection client
                var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
                var client = new HybridConnectionClient(new Uri(String.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
                // Initiate hello connection
                var relayConnection = await client.CreateConnectionAsync();
   
                // We run two conucrrent loops on hello connection. One 
                // reads input from hello console and writes it toohello connection 
                // with a stream writer. hello other reads lines of input from hello 
                // connection with a stream reader and writes them toohello console. 
                // Entering a blank line will shut down hello write task after 
                // sending it toohello server. hello server will then cleanly shut down
                // hello connection which will terminate hello read task.
   
                var reads = Task.Run(async () => {
                    // Initialize hello stream reader over hello connection
                    var reader = new StreamReader(relayConnection);
                    var writer = Console.Out;
                    do
                    {
                        // Read a full line of UTF-8 text up toonewline
                        string line = await reader.ReadLineAsync();
                        // If hello string is empty or null, we are done.
                        if (String.IsNullOrEmpty(line))
                            break;
                        // Write toohello console
                        await writer.WriteLineAsync(line);
                    }
                    while (true);
                });
   
                // Read from hello console and write toohello hybrid connection
                var writes = Task.Run(async () => {
                    var reader = Console.In;
                    var writer = new StreamWriter(relayConnection) { AutoFlush = true };
                    do
                    {
                        // Read a line form hello console
                        string line = await reader.ReadLineAsync();
                        // Write hello line out, also when it's empty
                        await writer.WriteLineAsync(line);
                        // Quit when hello line was empty
                        if (String.IsNullOrEmpty(line))
                            break;
                    }
                    while (true);
                });
   
                // Wait for both tasks toocomplete
                await Task.WhenAll(reads, writes);
                await relayConnection.CloseAsync(CancellationToken.None);
            }
        }
    }
    ```

