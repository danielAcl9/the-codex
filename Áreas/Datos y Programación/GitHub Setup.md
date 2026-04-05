[[Datos y Programación]]

### Instalar GitHub por primera vez

1. Crear una clave SSH
![[Key_GitHub.png]]
### Conectar una carpeta con un repositorio

```
#En el símbolo del sistema o cualquier otra consola

git init -> *Inicializa el repositorio*
git remote add origin <link del repositorio> -> *Conecta con el repo de Git (Ya debe estar creado)*
git status -> *Para revisar la rama de trabajo, debería ser main.*
```

### Añadir archivos

```
git add . -> *Añade todos los archivos del directorio actual, que no estén siento ignorados por un gitignore*	
git commit -m "Mensaje" -> *El commit con su mensaje **obligatorio***
git push origin main
```

---

### Otros

```
pip freeze > requirements.txt
pip install -r req *tab->*

git checkout main -> *Cambiar de branch a main*
git fetch -> *para traer todo del git*
```

---

### Conventional commits

![[ConventionalCommits.png]]