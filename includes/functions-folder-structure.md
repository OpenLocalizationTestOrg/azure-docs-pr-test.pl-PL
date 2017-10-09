
<span data-ttu-id="c905f-101">wszystkie funkcje hello w danej funkcji aplikacji Hello kod znajduje się w folderze głównym, który zawiera plik konfiguracji hosta i co najmniej jeden podfolderów, z których każdy zawiera kodu hello osobnych funkcji, jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="c905f-101">hello code for all of hello functions in a given function app lives in a root folder that contains a host configuration file and one or more subfolders, each of which contain hello code for a separate function, as in hello following example:</span></span>

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

<span data-ttu-id="c905f-102">Witaj *host.json* plik zawiera niektóre konfiguracji specyficznych dla środowiska uruchomieniowego i znajduje się w folderze głównym hello hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c905f-102">hello *host.json* file contains some runtime-specific configuration and sits in hello root folder of hello function app.</span></span> <span data-ttu-id="c905f-103">Aby uzyskać informacje na temat ustawień, które są dostępne, zobacz [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) w hello WebJobs.Script repozytorium stron typu wiki.</span><span class="sxs-lookup"><span data-stu-id="c905f-103">For information on settings that are available, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) in hello WebJobs.Script repository wiki.</span></span>

<span data-ttu-id="c905f-104">Każda funkcja ma folder, który zawiera jeden lub więcej plików kodu, konfiguracji function.json hello i innych zależności.</span><span class="sxs-lookup"><span data-stu-id="c905f-104">Each function has a folder that contains one or more code files, hello function.json configuration and other dependencies.</span></span>

