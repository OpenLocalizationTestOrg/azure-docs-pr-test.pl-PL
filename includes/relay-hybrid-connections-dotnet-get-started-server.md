### <a name="create-a-console-application"></a><span data-ttu-id="3e2fa-101">Tworzenie aplikacji konsolowej</span><span class="sxs-lookup"><span data-stu-id="3e2fa-101">Create a console application</span></span>

<span data-ttu-id="3e2fa-102">Najpierw uruchom program Visual Studio i utwórz nowy projekt **Aplikacja konsoli (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="3e2fa-102">First, launch Visual Studio and create a new **Console App (.NET Framework)** project.</span></span>

### <a name="add-hello-relay-nuget-package"></a><span data-ttu-id="3e2fa-103">Dodaj pakiet NuGet przekazywania hello</span><span class="sxs-lookup"><span data-stu-id="3e2fa-103">Add hello Relay NuGet package</span></span>

1. <span data-ttu-id="3e2fa-104">Kliknij prawym przyciskiem myszy projekt hello nowo utworzony, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="3e2fa-104">Right-click hello newly created project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="3e2fa-105">Kliknij przycisk hello **Przeglądaj** kartę, a następnie wyszukaj "Microsoft.Azure.Relay" i wybierz hello **Microsoft Azure przekazywania** elementu.</span><span class="sxs-lookup"><span data-stu-id="3e2fa-105">Click hello **Browse** tab, then search for "Microsoft.Azure.Relay" and select hello **Microsoft Azure Relay** item.</span></span> <span data-ttu-id="3e2fa-106">Kliknij przycisk **zainstalować** toocomplete hello instalacji, a następnie zamknij to okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="3e2fa-106">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

### <a name="write-some-code-tooreceive-messages"></a><span data-ttu-id="3e2fa-107">Napisanie kodu tooreceive wiadomości</span><span class="sxs-lookup"><span data-stu-id="3e2fa-107">Write some code tooreceive messages</span></span>

1. <span data-ttu-id="3e2fa-108">Zamień istniejące hello `using` instrukcji u góry pliku Program.cs hello następujący hello hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="3e2fa-108">Replace hello existing `using` statements at hello top of hello Program.cs file with hello following `using` statements:</span></span>
   
    ```csharp
    using System;
    using System.IO;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Relay;
    ```
2. <span data-ttu-id="3e2fa-109">Dodaj toohello stałe `Program` klasy dla szczegóły połączenia hybrydowe hello.</span><span class="sxs-lookup"><span data-stu-id="3e2fa-109">Add constants toohello `Program` class for hello hybrid connection details.</span></span> <span data-ttu-id="3e2fa-110">Zastąp symbole zastępcze hello w nawiasach wartości hello uzyskane podczas tworzenia połączenia hybrydowego hello.</span><span class="sxs-lookup"><span data-stu-id="3e2fa-110">Replace hello placeholders in brackets with hello values you obtained when creating hello hybrid connection.</span></span> <span data-ttu-id="3e2fa-111">Należy się toouse hello przestrzeni nazw w pełni kwalifikowaną nazwę:</span><span class="sxs-lookup"><span data-stu-id="3e2fa-111">Be sure toouse hello fully qualified namespace name:</span></span>
   
    ```csharp
    private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
    private const string ConnectionName = "{HybridConnectionName}";
    private const string KeyName = "{SASKeyName}";
    private const string Key = "{SASKey}";
    ```
3. <span data-ttu-id="3e2fa-112">Dodaj następujące metody o nazwie hello `ProcessMessagesOnConnection` toohello `Program` klasy:</span><span class="sxs-lookup"><span data-stu-id="3e2fa-112">Add hello following method called `ProcessMessagesOnConnection` toohello `Program` class:</span></span>
   
    ```csharp
    // Method is used tooinitiate connection
    private static async void ProcessMessagesOnConnection(HybridConnectionStream relayConnection, CancellationTokenSource cts)
    {
        Console.WriteLine("New session");
   
        // hello connection is a fully bidrectional stream. 
        // We put a stream reader and a stream writer over it 
        // which allows us tooread UTF-8 text that comes from 
        // hello sender and toowrite text replies back.
        var reader = new StreamReader(relayConnection);
        var writer = new StreamWriter(relayConnection) { AutoFlush = true };
        while (!cts.IsCancellationRequested)
        {
            try
            {
                // Read a line of input until a newline is encountered
                var line = await reader.ReadLineAsync();
   
                if (string.IsNullOrEmpty(line))
                {
                    // If there's no input data, we will signal that 
                    // we will no longer send data on this connection
                    // and then break out of hello processing loop.
                    await relayConnection.ShutdownAsync(cts.Token);
                    break;
                }
   
                // Output hello line on hello console
                Console.WriteLine(line);
   
                // Write hello line back toohello client, prepending "Echo:"
                await writer.WriteLineAsync($"Echo: {line}");
            }
            catch (IOException)
            {
                // Catch an IO exception that is likely caused because
                // hello client disconnected.
                Console.WriteLine("Client closed connection");
                break;
            }
        }
   
        Console.WriteLine("End session");
   
        // Closing hello connection
        await relayConnection.CloseAsync(cts.Token);
    }
    ```
4. <span data-ttu-id="3e2fa-113">Dodaj inną metodę o nazwie `RunAsync` toohello `Program` klasy, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="3e2fa-113">Add another method called `RunAsync` toohello `Program` class, as follows:</span></span>
   
    ```csharp
    private static async Task RunAsync()
    {
        var cts = new CancellationTokenSource();
   
        var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
        var listener = new HybridConnectionListener(new Uri(string.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
        // Subscribe toohello status events
        listener.Connecting += (o, e) => { Console.WriteLine("Connecting"); };
        listener.Offline += (o, e) => { Console.WriteLine("Offline"); };
        listener.Online += (o, e) => { Console.WriteLine("Online"); };
   
        // Opening hello listener will establish hello control channel to
        // hello Azure Relay service. hello control channel will be continuously 
        // maintained and reestablished when connectivity is disrupted.
        await listener.OpenAsync(cts.Token);
        Console.WriteLine("Server listening");
   
        // Providing callback for cancellation token that will close hello listener.
        cts.Token.Register(() => listener.CloseAsync(CancellationToken.None));
   
        // Start a new thread that will continuously read hello console.
        new Task(() => Console.In.ReadLineAsync().ContinueWith((s) => { cts.Cancel(); })).Start();
   
        // Accept hello next available, pending connection request. 
        // Shutting down hello listener will allow a clean exit with 
        // this method returning null
        while (true)
        {
            var relayConnection = await listener.AcceptConnectionAsync();
            if (relayConnection == null)
            {
                break;
            }
   
            ProcessMessagesOnConnection(relayConnection, cts);
        }
   
        // Close hello listener after we exit hello processing loop
        await listener.CloseAsync(cts.Token);
    }
    ```
5. <span data-ttu-id="3e2fa-114">Dodaj powitania po wierszu kodu toohello `Main` w hello metody `Program` klasy:</span><span class="sxs-lookup"><span data-stu-id="3e2fa-114">Add hello following line of code toohello `Main` method in hello `Program` class:</span></span>
   
    ```csharp
    RunAsync().GetAwaiter().GetResult();
    ```
   
    <span data-ttu-id="3e2fa-115">Oto jak powinien wyglądać uzupełniony plik Program.cs:</span><span class="sxs-lookup"><span data-stu-id="3e2fa-115">Here is what your completed Program.cs file should look like:</span></span>
   
    ```csharp
    namespace Server
    {
        using System;
        using System.IO;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.Azure.Relay;
   
        public class Program
        {
            private const string RelayNamespace = "{RelayNamespace}.servicebus.windows.net";
            private const string ConnectionName = "{HybridConnectionName}";
            private const string KeyName = "{SASKeyName}";
            private const string Key = "{SASKey}";
   
            public static void Main(string[] args)
            {
                RunAsync().GetAwaiter().GetResult();
            }
   
            private static async Task RunAsync()
            {
                var cts = new CancellationTokenSource();
   
                var tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(KeyName, Key);
                var listener = new HybridConnectionListener(new Uri(string.Format("sb://{0}/{1}", RelayNamespace, ConnectionName)), tokenProvider);
   
                // Subscribe toohello status events
                listener.Connecting += (o, e) => { Console.WriteLine("Connecting"); };
                listener.Offline += (o, e) => { Console.WriteLine("Offline"); };
                listener.Online += (o, e) => { Console.WriteLine("Online"); };
   
                // Opening hello listener will establish hello control channel to
                // hello Azure Relay service. hello control channel will be continuously 
                // maintained and reestablished when connectivity is disrupted.
                await listener.OpenAsync(cts.Token);
                Console.WriteLine("Server listening");
   
                // Providing callback for cancellation token that will close hello listener.
                cts.Token.Register(() => listener.CloseAsync(CancellationToken.None));
   
                // Start a new thread that will continuously read hello console.
                new Task(() => Console.In.ReadLineAsync().ContinueWith((s) => { cts.Cancel(); })).Start();
   
                // Accept hello next available, pending connection request. 
                // Shutting down hello listener will allow a clean exit with 
                // this method returning null
                while (true)
                {
                    var relayConnection = await listener.AcceptConnectionAsync();
                    if (relayConnection == null)
                    {
                        break;
                    }
   
                    ProcessMessagesOnConnection(relayConnection, cts);
                }
   
                // Close hello listener after we exit hello processing loop
                await listener.CloseAsync(cts.Token);
            }
   
            private static async void ProcessMessagesOnConnection(HybridConnectionStream relayConnection, CancellationTokenSource cts)
            {
                Console.WriteLine("New session");
   
                // hello connection is a fully bidrectional stream. 
                // We put a stream reader and a stream writer over it 
                // which allows us tooread UTF-8 text that comes from 
                // hello sender and toowrite text replies back.
                var reader = new StreamReader(relayConnection);
                var writer = new StreamWriter(relayConnection) { AutoFlush = true };
                while (!cts.IsCancellationRequested)
                {
                    try
                    {
                        // Read a line of input until a newline is encountered
                        var line = await reader.ReadLineAsync();
   
                        if (string.IsNullOrEmpty(line))
                        {
                            // If there's no input data, we will signal that 
                            // we will no longer send data on this connection
                            // and then break out of hello processing loop.
                            await relayConnection.ShutdownAsync(cts.Token);
                            break;
                        }
   
                        // Output hello line on hello console
                        Console.WriteLine(line);
   
                        // Write hello line back toohello client, prepending "Echo:"
                        await writer.WriteLineAsync($"Echo: {line}");
                    }
                    catch (IOException)
                    {
                        // Catch an IO exception that is likely caused because
                        // hello client disconnected.
                        Console.WriteLine("Client closed connection");
                        break;
                    }
                }
   
                Console.WriteLine("End session");
   
                // Closing hello connection
                await relayConnection.CloseAsync(cts.Token);
            }
        }
    }
    ```

