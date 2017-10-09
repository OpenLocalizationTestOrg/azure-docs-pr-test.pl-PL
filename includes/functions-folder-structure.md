
wszystkie funkcje hello w danej funkcji aplikacji Hello kod znajduje się w folderze głównym, który zawiera plik konfiguracji hosta i co najmniej jeden podfolderów, z których każdy zawiera kodu hello osobnych funkcji, jak hello poniższy przykład:

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

Witaj *host.json* plik zawiera niektóre konfiguracji specyficznych dla środowiska uruchomieniowego i znajduje się w folderze głównym hello hello funkcji aplikacji. Aby uzyskać informacje na temat ustawień, które są dostępne, zobacz [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) w hello WebJobs.Script repozytorium stron typu wiki.

Każda funkcja ma folder, który zawiera jeden lub więcej plików kodu, konfiguracji function.json hello i innych zależności.

