# Instrukcje dla repozytorium lab01

## Inicjowanie repozytorium

1. **Inicjowanie pustego repozytorium:**
   ```bash
   git init
  
**Dodawanie plików do śledzenia:**
git add .
*Tworzenie pierwszego commita:*
git commit -m "Pierwszy commit: Inicjalizacja projektu"

**Pobieranie zmian z serwera**
*Dodawanie zdalnego repozytorium:*
git remote add origin <adres-url-repozytorium>
*Pobieranie zmian z głównej gałęzi (np. master):*
git pull origin master

**Wgranie nowych zmian**
*Dodawanie zmian do śledzenia:*
git add .
*Tworzenie commita z wprowadzonymi zmianami:*
git commit -m "Opis wprowadzonych zmian"
*Wysyłanie zmian na serwer:*
git push origin master

**Upewnij się, że dostosowujesz adres URL zdalnego repozytorium oraz nazwę gałęzi głównej (jeśli nie jest to `master`) do swojego przypadku.**
