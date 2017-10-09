<span data-ttu-id="6490d-101">Platforma Azure określi wersję hello toouse języka Python dla swojego środowiska wirtualnego z powitania po priorytet:</span><span class="sxs-lookup"><span data-stu-id="6490d-101">Azure will determine hello version of Python toouse for its virtual environment with hello following priority:</span></span>

1. <span data-ttu-id="6490d-102">Wersja określona w pliku runtime.txt w folderze głównym hello</span><span class="sxs-lookup"><span data-stu-id="6490d-102">version specified in runtime.txt in hello root folder</span></span>
2. <span data-ttu-id="6490d-103">Wersja określona przez ustawienie języka Python w konfiguracji aplikacji sieci web hello (hello **ustawienia** > **ustawienia aplikacji** bloku aplikacji sieci web w portalu Azure hello)</span><span class="sxs-lookup"><span data-stu-id="6490d-103">version specified by Python setting in hello web app configuration (hello **Settings** > **Application Settings** blade for your web app in hello Azure Portal)</span></span>
3. <span data-ttu-id="6490d-104">Python-2.7 jest domyślnym hello, jeśli nie określono żadnego z powyższych hello są</span><span class="sxs-lookup"><span data-stu-id="6490d-104">python-2.7 is hello default if none of hello above are specified</span></span>

<span data-ttu-id="6490d-105">Prawidłowe wartości dla zawartości hello</span><span class="sxs-lookup"><span data-stu-id="6490d-105">Valid values for hello contents of</span></span> 

    \runtime.txt

<span data-ttu-id="6490d-106">są:</span><span class="sxs-lookup"><span data-stu-id="6490d-106">are:</span></span>

* <span data-ttu-id="6490d-107">python-2.7</span><span class="sxs-lookup"><span data-stu-id="6490d-107">python-2.7</span></span>
* <span data-ttu-id="6490d-108">python-3.4</span><span class="sxs-lookup"><span data-stu-id="6490d-108">python-3.4</span></span>

<span data-ttu-id="6490d-109">Jeśli hello wersja mikro (trzecia cyfra) jest określona, zostanie zignorowana.</span><span class="sxs-lookup"><span data-stu-id="6490d-109">If hello micro version (third digit) is specified, it is ignored.</span></span>

