# Stats base de données Vostok

## au 2 janvier 2025

## script

```
#!/bin/bash

# Répertoire parent
SEARCH_DIR=".."

# Date limite : il y a 2 ans
DATE_LIMIT=$(date -d '2 years ago' +%s)

countGenre=0
countRecents=0
countCH=0
countGE=0
countF=0
countH=0

# Générer un horodatage pour le fichier de log (format YYYY-MM-DD_HH-MM-SS)
timestamp=$(date +"%Y-%m-%d_%H-%M-%S")

# Spécifier le fichier de log
log_file="scan_results_$timestamp.txt"

# Rediriger tous les messages dans le fichier de log
exec > "$log_file" 2>&1

# Ajouter un en-tête au fichier de log
echo "Début de l'analyse des fichiers audio à $timestamp"

# Traitement des fichiers avec find et redirection vers awk pour comptage
find "$SEARCH_DIR" -maxdepth 1 -type f \( -iname "*.mp3" -o -iname "*.wav" -o -iname "*.flac" -o -iname "*.aac" -o -iname "*.ogg" -o -iname "*.m4a" -o -iname "*.wma" \) -print0 | while IFS= read -r -d '' file; do
    # Obtenir la date de création (timestamp)
    file_creation=$(stat -c %W "$file")  # Utilisation de %W pour obtenir la date de création
	
	# Extraire le tag "genre" avec ffprobe
    genre=$(ffprobe -v quiet -show_entries format_tags=genre -of default=noprint_wrappers=1:nokey=1 "$file")
    
    # Nettoyer le genre (supprimer les espaces avant et après)
    genre=$(echo "$genre" | xargs)
    
	echo ""
	echo ""
	echo $file
	echo $genre 
	
    # Vérifier si le genre commence par "V " (V suivi d'un espace)
    if [[ "$genre" == V\ * ]]; then
        echo "genre ok !!"
		((countGenre++))
		
		 # Obtenir la date de création (timestamp)
		file_creation=$(stat -c %W "$file")  # Utilisation de %W pour obtenir la date de création
		 # Si la date de création est valide et inférieure à la limite
		if [ "$file_creation" -gt "$DATE_LIMIT" ]; then
			echo "date ok !!"
			((countRecents++))
			echo $countRecents
			
			# Extraire le tag "title" avec ffprobe
			title=$(ffprobe -v quiet -show_entries format_tags=title -of default=noprint_wrappers=1:nokey=1 "$file")
    
			# Nettoyer le titre (supprimer les espaces avant et après)
			title=$(echo "$title" | xargs)
			
			# récupérer le grouping (en fait ISRF)
			grouping=$(ffprobe -v quiet -show_entries format_tags=ISRF -of default=noprint_wrappers=1:nokey=1 "$file")
			
			echo "grouping : $grouping"
    
			# Nettoyer le grouping (supprimer les espaces avant et après)
			grouping=$(echo "$grouping" | xargs)
			
			# Vérifier si le nom du fichier ou le titre contient [CH]
			if [[ "$file" == *"[CH]"* ]] || [[ "$title" == *"[CH]"* ]]; then
				echo "CH ****"
				((countCH++))
			fi
			
			# Vérifier si le nom du fichier ou le titre contient [GE]
			if [[ "$file" == *"[GE]"* ]] || [[ "$title" == *"[GE]"* ]]; then
				echo "GE *****"
				((countGE++))
			fi
			
			# Vérifier si le grouping contient H
			if [[ "$grouping" == *"H"* ]]; then
				echo "H !!!!"
				((countH++))
			fi
			
			# Vérifier si le grouping contient F
			if [[ "$grouping" == *"F"* ]]; then
				echo "F !!!!"
				((countF++))
			fi
		fi
		echo "Nombre de fichiers avec genre commençant par 'V ': $countGenre"
		echo "Nombre de fichiers avec genre OK et date de création < 2 ans : $countRecents"
		echo "Nombre de fichiers avec ces deux critères et [CH] : $countCH"
		echo "Nombre de fichiers avec ces deux critères et [GE] : $countGE"
		echo "Nombre de fichiers avec ces deux critères et grouping H : $countH"
		echo "Nombre de fichiers avec ces deux critères et grouping F : $countF"
    fi
done

# Afficher le nombre de fichiers correspondant
echo ""
echo ""
echo ""
echo ""
echo "*********************************************************************************"
echo "TOTAUX : "
echo "Nombre de fichiers avec genre commençant par 'V ': $countGenre"
echo "Nombre de fichiers avec genre OK et date de création < 2 ans : $countRecents"
echo "Nombre de fichiers avec ces deux critères et [CH] : $countCH"
echo "Nombre de fichiers avec ces deux critères et [GE] : $countGE"
echo "Nombre de fichiers avec ces deux critères et grouping H : $countH"
echo "Nombre de fichiers avec ces deux critères et grouping F : $countF"
```