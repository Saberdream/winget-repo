# Mon dépôt Winget (exemple)

Ce dépôt contient des manifests pour le **Windows Package Manager (winget)**.  
Il permet d’ajouter une source personnalisée afin d’installer des applications qui ne sont pas présentes dans le dépôt officiel de Microsoft.

---

## 📂 Structure du dépôt


mon-winget-repo/ ├── manifests/ │   └── Contoso/ │       └── HelloWorldApp/ │           └── 1.0.0/ │               └── HelloWorldApp.yaml └── README.md


- `manifests/` : dossier racine des manifests Winget  
- `Contoso/HelloWorldApp/1.0.0/` : hiérarchie **éditeur / application / version**  
- `HelloWorldApp.yaml` : manifest décrivant l’application  

---

## 📄 Exemple de manifest

```
yaml
Id: Contoso.HelloWorldApp
Name: Hello World App
Publisher: Contoso Ltd
Version: 1.0.0
License: MIT
InstallerType: exe
Installers:
  - Architecture: x64
    InstallerUrl: https://example.com/helloworldapp-1.0.0-x64.exe
    InstallerSha256: 0123456789ABCDEF0123456789ABCDEF0123456789ABCDEF0123456789ABCDEF
ManifestType: singleton
ManifestVersion: 1.5.0
```

👉 Le champ InstallerSha256 doit être calculé avec PowerShell :

`Get-FileHash .\helloworldapp-1.0.0-x64.exe -Algorithm SHA256`

⚙️ Utilisation

1. Ajouter la source
```
winget source add -n MonDepot -a https://github.com/Saberdream/winget-repo
winget source update
```

2. Vérifier les sources disponibles

winget source list

3. Installer une application depuis ce dépôt

`winget install Contoso.HelloWorldApp`

🤝 Contribuer

1. Forkez le dépôt
2. Ajoutez vos manifests dans le dossier manifests/ en respectant la hiérarchie
3. Vérifiez vos fichiers YAML avec YamlValidator ou winget validate
4. Proposez une Pull Request

📌 Notes

Ce dépôt est un exemple pédagogique.

Pour un usage en production, pensez à héberger vos installeurs sur un serveur fiable et sécurisé.

Respectez toujours les licences des logiciels que vous distribuez.
