Utwórz poświadczenia wdrażania z hello [ustawiono użytkownika wdrożenia aplikacji sieci Web az](/cli/azure/webapp/deployment/user#set) polecenia.

Użytkownik wdrożenia jest wymagana dla FTP i lokalnych aplikacji sieci web tooa wdrożenia Git. Witaj, nazwę użytkownika i hasło są poziomu kont. _Różnią się one od poświadczeń subskrypcji platformy Azure._

Zastąp następujące polecenie, w hello  *\<nazwa użytkownika >* i  *\<hasło >* nową nazwę użytkownika i hasło. Witaj, nazwa użytkownika musi być unikatowa. Witaj hasło musi mieć co najmniej ośmiu znaków, przy użyciu dwóch hello następujące trzy elementy: liter, cyfr, symboli. 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

Jeśli otrzymasz ` 'Conflict'. Details: 409` błąd, username hello zmiany. Jeśli wystąpił błąd ` 'Bad Request'. Details: 400`, użyj silniejszego hasła.

Ten użytkownik wdrożenia jest tworzony tylko jeden raz. Można go używać we wszystkich wdrożeniach platformy Azure.

> [!NOTE]
> Nazwa użytkownika hello rekordu i hasło. Należy je aplikacji sieci web toodeploy hello później.
>
>