# convertir_image_en_SVG

Ce script est comme un assistant de conversion d'images. Il vous demande de choisir une image sur votre ordinateur. Une fois que vous avez choisi une image, 
il la prépare en la simplifiant et en mettant en évidence les parties importantes. Il fait cela en transformant l'image en noir et blanc, où tout ce qui est 
assez sombre devient noir et tout ce qui est assez clair devient blanc. Ensuite, il utilise un outil appelé "potrace" pour transformer cette image simplifiée 
en une image vectorielle, qui est un type d'image que vous pouvez agrandir autant que vous le souhaitez sans perdre de qualité. Enfin, il sauvegarde cette 
nouvelle image vectorielle à côté de votre image originale.

![Capture du 2023-07-22 14-40-21](https://github.com/danydube1971/convertir_image_en_SVG/assets/74633244/7ab99589-a3ee-45bb-a228-5f589f026cd7)


1. Le script commence par importer les modules nécessaires : `os`, `cv2` (OpenCV), `subprocess`, `tkinter`, `filedialog`, `Image` et `numpy`.
2. La fonction `select_file()` est définie. Elle crée une fenêtre de sélection de fichiers à l'aide de `tkinter` et `filedialog`, permet à l'utilisateur de
   choisir un fichier, puis renvoie le chemin complet de ce fichier.
3. Ensuite, la fonction `convert_to_svg(file_path, threshold=128)` est définie. Elle prend en entrée un chemin de fichier et un seuil (par défaut à 128).
   Cette fonction fait le travail principal du script :
   - Elle lit l'image à partir du chemin de fichier en utilisant `cv2.imread(file_path, cv2.IMREAD_GRAYSCALE)`. L'image est lue en niveaux de gris.
   - Elle applique ensuite un seuil à l'image avec la fonction `cv2.threshold()`. Tous les pixels avec une intensité de gris inférieure au seuil
     sont mis à zéro (noir), et ceux avec une intensité supérieure sont mis à 255 (blanc). Cela permet de simplifier l'image et de mettre en évidence les parties importantes.
   - L'image est ensuite inversée avec `cv2.bitwise_not()`. Cela est nécessaire car `potrace`, l'outil utilisé pour la vectorisation, considère le blanc
     comme l'objet et le noir comme l'arrière-plan.
   - L'image inversée est enregistrée en format `.bmp` car `potrace` ne fonctionne qu'avec des images bitmap.
   - La commande `potrace` est alors appelée pour convertir l'image bitmap en une image SVG. La sortie est enregistrée avec le même nom que le fichier
     d'origine, mais avec '_vect.svg' ajouté à la fin.
   - Enfin, l'image `.bmp` temporaire est supprimée.
6. Le point d'entrée principal du script, `if __name__ == '__main__':`, appelle `select_file()` pour obtenir un chemin de fichier de l'utilisateur,
   puis appelle `convert_to_svg(path)` pour convertir l'image sélectionnée en une image SVG.
   
Voilà donc ce que fait le script, étape par étape. Il permet à l'utilisateur de sélectionner une image, l'inverse, lui applique un seuil, 
puis l'envoie à Potrace pour être convertie en une image vectorielle SVG.

**Pré-requis pour utiliser le script :**

Vous devez installer les librairies suivantes: 

**apt-get install potrace python3-tk python3-pip**

**pip3 install opencv-python-headless pyautogui**

------------------
# Comment utiliser le script

Dans un terminal, exécuter le script avec la commande:

**python3 "Convertir image en SVG_détaillé.py"**

