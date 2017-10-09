<span data-ttu-id="dfd76-101">Utwórz poświadczenia wdrażania z hello [ustawiono użytkownika wdrożenia aplikacji sieci Web az](/cli/azure/webapp/deployment/user#set) polecenia.</span><span class="sxs-lookup"><span data-stu-id="dfd76-101">Create deployment credentials with hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command.</span></span>

<span data-ttu-id="dfd76-102">Użytkownik wdrożenia jest wymagana dla FTP i lokalnych aplikacji sieci web tooa wdrożenia Git.</span><span class="sxs-lookup"><span data-stu-id="dfd76-102">A deployment user is required for FTP and local Git deployment tooa web app.</span></span> <span data-ttu-id="dfd76-103">Witaj, nazwę użytkownika i hasło są poziomu kont.</span><span class="sxs-lookup"><span data-stu-id="dfd76-103">hello user name and password are account level.</span></span> <span data-ttu-id="dfd76-104">_Różnią się one od poświadczeń subskrypcji platformy Azure._</span><span class="sxs-lookup"><span data-stu-id="dfd76-104">_They are different from your Azure subscription credentials._</span></span>

<span data-ttu-id="dfd76-105">Zastąp następujące polecenie, w hello  *\<nazwa użytkownika >* i  *\<hasło >* nową nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="dfd76-105">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="dfd76-106">Witaj, nazwa użytkownika musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="dfd76-106">hello user name must be unique.</span></span> <span data-ttu-id="dfd76-107">Witaj hasło musi mieć co najmniej ośmiu znaków, przy użyciu dwóch hello następujące trzy elementy: liter, cyfr, symboli.</span><span class="sxs-lookup"><span data-stu-id="dfd76-107">hello password must be at least eight characters long, with two of hello following three elements: letters, numbers, symbols.</span></span> 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="dfd76-108">Jeśli otrzymasz ` 'Conflict'. Details: 409` błąd, username hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="dfd76-108">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="dfd76-109">Jeśli wystąpił błąd ` 'Bad Request'. Details: 400`, użyj silniejszego hasła.</span><span class="sxs-lookup"><span data-stu-id="dfd76-109">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

<span data-ttu-id="dfd76-110">Ten użytkownik wdrożenia jest tworzony tylko jeden raz. Można go używać we wszystkich wdrożeniach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dfd76-110">You create this deployment user only once; you can use it for all your Azure deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="dfd76-111">Nazwa użytkownika hello rekordu i hasło.</span><span class="sxs-lookup"><span data-stu-id="dfd76-111">Record hello user name and password.</span></span> <span data-ttu-id="dfd76-112">Należy je aplikacji sieci web toodeploy hello później.</span><span class="sxs-lookup"><span data-stu-id="dfd76-112">You need them toodeploy hello web app later.</span></span>
>
>