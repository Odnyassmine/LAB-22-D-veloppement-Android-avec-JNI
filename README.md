# JNIDemo - Laboratoire JNI & NDK Android

Ce projet est une application Android de démonstration illustrant l'utilisation du **JNI (Java Native Interface)** pour faire communiquer du code Java avec du code natif **C++**.

## 🎯 Objectifs pédagogiques
- Configurer un projet Android avec le support **NDK** et **CMake**.
- Déclarer et appeler des méthodes natives depuis Java.
- Manipuler des types de données simples et complexes (String, Tableaux).
- Gérer le chargement des bibliothèques partagées (`.so`).
- Utiliser la journalisation native avec `__android_log_print` (Logcat).

## 🚀 Fonctionnalités
L'application réalise quatre démonstrations interactives :
1.  **Hello JNI** : Appel d'une fonction simple renvoyant une chaîne de caractères depuis le C++.
2.  **Calcul de Factoriel** : Calcul intensif en natif avec gestion d'erreurs (négatifs et overflow).
3.  **Inversion de Chaîne** : Passage d'un objet `String` Java vers C++, inversion via la STL (`std::reverse`), et retour vers Java.
4.  **Somme de Tableau** : Manipulation d'un tableau d'entiers (`int[]`) transmis au code natif.

## 🛠 Architecture Technique
- **Java** (`MainActivity.java`) : Déclare les méthodes `native` et charge la bibliothèque.
- **C++** (`native-lib.cpp`) : Implémente la logique métier en utilisant les headers JNI.
- **CMake** (`CMakeLists.txt`) : Script de construction définissant la compilation de la bibliothèque `native-lib`.
- **NDK** : Ensemble d'outils utilisé pour compiler le code C++ pour les architectures Android (arm64-v8a, x86_64, etc.).

## 📂 Structure du projet
```text
app/
├── src/main/cpp/
│   ├── CMakeLists.txt      # Configuration de build native
│   └── native-lib.cpp      # Code source C++ (JNI)
├── src/main/java/.../
│   └── MainActivity.java   # Point d'entrée Java et declarations native
└── src/main/res/layout/
    └── activity_main.xml   # Interface utilisateur
```

## 📝 Installation et Configuration
1.  Ouvrez le projet dans **Android Studio**.
2.  Assurez-vous que le **NDK (Side by side)** et **CMake** sont installés via le *SDK Manager* (onglet SDK Tools).
3.  Synchronisez le projet avec Gradle.
4.  Lancez l'application sur un terminal ou émulateur.

## 📊 Tests et Résultats attendus
| Fonction | Entrée | Résultat attendu |
| :--- | :--- | :--- |
| `helloFromJNI` | - | "Hello from C++ via JNI !" |
| `factorial` | 10 | 3628800 |
| `reverseString` | "JNI is powerful!" | "!lufrewop si INJ" |
| `sumArray` | {10, 20, 30, 40, 50} | 150 |

## 🔍 Debugging
Les logs natifs sont envoyés vers le **Logcat** avec le tag `JNI_DEMO`.
Exemple de sortie :
```text
I/JNI_DEMO: Appel de helloFromJNI depuis le natif
I/JNI_DEMO: Factoriel de 10 calcule en natif = 3628800
I/JNI_DEMO: String inversee = !lufrewop si INJ
I/JNI_DEMO: Somme du tableau = 150
```

## ⚠️ Bonnes Pratiques Appliquées
- **Gestion des ressources** : Utilisation systématique de `ReleaseStringUTFChars` et `ReleaseIntArrayElements` pour éviter les fuites de mémoire native.
- **Sécurité** : Vérification des pointeurs nuls (`nullptr`) côté natif.
- **Interopérabilité** : Utilisation de `extern "C"` pour éviter le *name mangling* C++.
