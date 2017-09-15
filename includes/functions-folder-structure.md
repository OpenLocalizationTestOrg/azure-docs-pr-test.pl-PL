
<span data-ttu-id="7200c-101">Kod dla wszystkich funkcji w danej funkcji aplikacji znajduje się w folderze głównym, który zawiera plik konfiguracji hosta i co najmniej jeden podfolderów, z których każdy zawiera kod osobnych funkcji, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="7200c-101">The code for all of the functions in a given function app lives in a root folder that contains a host configuration file and one or more subfolders, each of which contain the code for a separate function, as in the following example:</span></span>

```
wwwroot
 | - host.json
 | - mynodefunction
 | | - function.json
 | | - index.js
 | | - node_modules
 | | | - ... packages ...
 | | - package.json
 | - mycsharpfunction
 | | - function.json
 | | - run.csx
```

<span data-ttu-id="7200c-102">*Host.json* plik zawiera niektóre konfiguracji specyficznych dla środowiska uruchomieniowego i znajduje się w folderze głównym funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7200c-102">The *host.json* file contains some runtime-specific configuration and sits in the root folder of the function app.</span></span> <span data-ttu-id="7200c-103">Aby uzyskać informacje na temat ustawień, które są dostępne, zobacz [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) w witrynie wiki WebJobs.Script repozytorium.</span><span class="sxs-lookup"><span data-stu-id="7200c-103">For information on settings that are available, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in the WebJobs.Script repository wiki.</span></span>

<span data-ttu-id="7200c-104">Każda funkcja ma folder, który zawiera jeden lub więcej plików kodu, konfiguracji function.json i innych zależności.</span><span class="sxs-lookup"><span data-stu-id="7200c-104">Each function has a folder that contains one or more code files, the function.json configuration and other dependencies.</span></span>

