W usłudze Cloud Shell utwórz poświadczenia wdrożenia za pomocą polecenia [az webapp deployment user set](/cli/azure/webapp/deployment/user?view=azure-cli-latest#az_webapp_deployment_user_set). Użytkownik wdrożenia jest wymagany do wdrożenia protokołu FTP i lokalnego narzędzia Git w aplikacji internetowej. Nazwa użytkownika i hasło są określane na poziomie konta. _Różnią się one od poświadczeń subskrypcji platformy Azure._

W poniższym przykładzie Zastąp  *\<nazwa użytkownika >* i  *\<hasło >* (w tym nawiasy) przy użyciu nowej nazwy użytkownika i hasła. Nazwa użytkownika musi być unikatowa. Hasło musi mieć długość co najmniej ośmiu znaków i zawierać dwa z następujących trzech elementów: litery, cyfry, symbole. 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

Jeśli wystąpił błąd ` 'Conflict'. Details: 409`, zmień nazwę użytkownika. Jeśli wystąpił błąd ` 'Bad Request'. Details: 400`, użyj silniejszego hasła.

Ten użytkownik wdrożenia jest tworzony tylko jeden raz. Można go używać we wszystkich wdrożeniach platformy Azure.

> [!NOTE]
> Zapisz nazwę użytkownika i hasło. Będą one potrzebne później do wdrożenia aplikacji internetowej.
>
>
